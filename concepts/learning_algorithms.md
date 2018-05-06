# Optimization Algorithms

_This section is largely adapt from Ian Goodfellow's Deep Learning textbook and Andrew Ng's Deep Learning Specialization Coursera series, all credits belong to them._

## Table of Contents

* [How Learning Differs From Traditional Optimization Problem](https://github.com/robert8138/deep-learning-deliberate-practice/blob/master/concepts/learning_algorithms.md#how-learning-differs-from-traditional-optimization-problem)

* [Challenges in Neural Network Optimization](https://github.com/robert8138/deep-learning-deliberate-practice/blob/master/concepts/learning_algorithms.md#challenges-in-neural-network-optimization)
	* [Ill-conditioning Hessian Matrix](https://github.com/robert8138/deep-learning-deliberate-practice/blob/master/concepts/learning_algorithms.md#ill-conditioning)
	* [Local Minima](https://github.com/robert8138/deep-learning-deliberate-practice/blob/master/concepts/learning_algorithms.md#local-minima)
	* [Saddle Points](https://github.com/robert8138/deep-learning-deliberate-practice/blob/master/concepts/learning_algorithms.md#saddle-points)
	* [Gradient Cliffs](https://github.com/robert8138/deep-learning-deliberate-practice/blob/master/concepts/learning_algorithms.md#gradient-cliffs)
	* [Vanishing and Exploding Gradients](https://github.com/robert8138/deep-learning-deliberate-practice/blob/master/concepts/learning_algorithms.md#vanishing-and-exploding-gradients)

* [Gradient Descent](https://github.com/robert8138/deep-learning-deliberate-practice/blob/master/concepts/learning_algorithms.md#gradient-descient): Batch, Stochastic, Mini-batch

* [More Advanced Gradient-based Methods](https://github.com/robert8138/deep-learning-deliberate-practice/blob/master/concepts/learning_algorithms.md#more-advanced-gradient-based-methods)
	* [Momentum](https://github.com/robert8138/deep-learning-deliberate-practice/blob/master/concepts/learning_algorithms.md#sgd-with-momentum)
	* [RMSprop](https://github.com/robert8138/deep-learning-deliberate-practice/blob/master/concepts/learning_algorithms.md#sgd-with-rmsprop)
	* [Adam](https://github.com/robert8138/deep-learning-deliberate-practice/blob/master/concepts/learning_algorithms.md#adam)
	* [Comparison of All SGD-style Optimization Above](https://github.com/robert8138/deep-learning-deliberate-practice/blob/master/concepts/learning_algorithms.md#comparison-of-all-sgd-style-optimization-above)

* [Babysitting the Learning Process](https://github.com/robert8138/deep-learning-deliberate-practice/blob/master/concepts/learning_algorithms.md#babysitting-the-learning-process)
	* [Loss Function](https://github.com/robert8138/deep-learning-deliberate-practice/blob/master/concepts/learning_algorithms.md#loss-function)
	* [Training error v.s. Validation error](https://github.com/robert8138/deep-learning-deliberate-practice/blob/master/concepts/learning_algorithms.md#train-vs-validation-error)
	* [Decrease Learning Rate](https://github.com/robert8138/deep-learning-deliberate-practice/blob/master/concepts/learning_algorithms.md#learning-rate)

## How Learning Differs From Traditional Optimization Problem

Optimization algorithms used for training of deep models diﬀer from traditional optimization algorithms in several ways. Machine learning usually acts indirectly. In most machine learning scenarios, we care about some performance measure `P`, that is deﬁned with respect to the test set and may also be intractable. We therefore optimize `P` only indirectly. We reduce a diﬀerent cost function `J(θ)` in the hope that doing so will improve `P`. This is in contrast to pure optimization, where minimizing `J` is a goal in and of itself.

More formally, we would usually prefer to minimize the corresponding objective function where the expectation (of generalization error) is taken across the data-generating distribution `p_data` rather than just over the ﬁnite training set, we call this true expectation **risk**. If we know the true underlying distribution, risk minimization would be an optimization task solvable by an optimization algorithm.

![Risk Minimization](pictures/risk_minimization.png)

When we do not know `pdata(x, y)` but only have a training set of samples, however, we have a machine learning problem. The simplest way to convert a machine learning problem back into an optimization problem is to minimize the expected loss on the training set. This means replacing the true distribution `p(x, y)` with the empirical distribution `ˆp(x, y)` deﬁned by the training set. We now minimize the **empirical risk**. 

![Empirical Risk Minimization](pictures/empirical_risk_minimization.png)

The training process based on minimizing this average training error is known as **empirical risk minimization**. In this setting, machine learning is still very similar to straightforward optimization. Rather than optimizing the risk directly, we optimize the empirical risk and hope that the risk decreases signiﬁcantly as well. A variety of theoretical results establish conditions under which the true risk can be expected to decrease by various amounts.

The relationship between generalization error and training error is a deep topic, and I think Professor Yaser Abu-Mostafa's Caltech course: [Lecture 7](http://work.caltech.edu/slides/slides07.pdf) has a fantastic explanation for this (using VC dimensions, Vapnik-Chervonenkis Inequality, and Probability bounds).

![VC Bound](pictures/vc_bound.png)


## Challenges in Neural Network Optimization

There are many potential issues with Neural Network Optimization, we list a few main ones here:

### Ill-conditioning

The condition number of a matrix is defined as the ratio of the `largest eigenvalue` / `smallest eigenvalue`. A matrix is ill-conditioning when this ratio is really big. Geometrically, this means the contour of the function is very long and narrow. This makes gradient descent inefficient, because the gradient direction is usually orthogonal to the direction of the local minima (see pictures above). This concept is explained well in this [Quora answer](https://www.quora.com/What-does-it-mean-to-have-a-poorly-conditioned-Hessian-matrix).


![ill conditioning](pictures/ill_conditioning.png)

Mathematically, learning becomes very slow despite the presence of a strong gradient because the learning rate must be shrunk to compensate for even stronger curvature (i.e. the decrease in the loss function is over-compensated by the increase in the curvature). In cases where we suspect the Hessian matrix is ill-conditioned, one should monitor the squared gradient norm `gTg` and `gTHg` terms.

### Local Minima

One of the most prominent features of a convex optimization problem is that it can be reduced to the problem of ﬁnding a local minimum. Any local minimum is guaranteed to be a global minimum. Some convex functions have a ﬂat region at the bottom rather than a single global minimum point, but any point within such a ﬂat region is an acceptable solution. When optimizing a convex function, we know that we have reached a good solution if we ﬁnd a critical point of any kind.

With nonconvex functions, such as neural nets, it is possible to have many local minima. Indeed, nearly any deep model is essentially guaranteed to have an extremely large number of local minima. As we will see, however, this is not necessarily a major problem, because experts now suspect that, for suﬃciently large neural networks, **most local minima have a low cost function value**, and that it is not important to ﬁnd a true global minimum rather than to ﬁnd a point in parameter space that has low but not minimal cost.

### Saddle Points

Nowadays, it's generally believe that in a high dimensional model like Neural Network, local minima is less of a problem, there are **more chances of seeing saddle points**. Why are there more presence of saddle points than local minima? 

Here is the intuition: At a saddle point, the Hessian matrix has both positive and negative eigenvalues, whereas the Hessian matrix at a local minimum has only positive eigenvalues. Imagine that the sign of each eigenvalue is generated by ﬂipping a coin, it's much easier to get a saddle point than to have all signs to be positive (local minima).

What are the implications of the proliferation of saddle points for training algorithms? For ﬁrst-order optimization, algorithms that use only gradient information, the situation is unclear. The gradient can often become very small near a saddle point. On the other hand, gradient descent empirically seems able to escapesaddle points in many cases.

### Gradient Cliffs

![Gradient Cliff](pictures/gradient_cliff.png)

Neural networks with many layers often have extremely steep regions resembling cliﬀs. These result from the multiplication of several large weights together. On the face of an extremely steep cliﬀ structure, the gradient update step can move the parameters extremely far, usually jumping oﬀ the cliﬀ structure altogether.

The typical solution to avoid updating by a large gradient direction is to use **gradient clipping**. The gradient clipping heuristic intervenes to reduce the step size, making it less likely to go outside the region where the gradient indicatesthe direction of approximately steepest descent.

### Vanishing and Exploding Gradients

Another diﬃculty that neural network optimization algorithms must overcomearises when the computational graph becomes extremely deep is the vanishing/exploding gradient problems. This is especially relevant for Recurrent Neural Network (RNN), where the same weight matrix `W` is being applied in each time step. Andrej Karpathy explained this problem in his blog post ["Yes, you should understand backprop"](https://medium.com/@karpathy/yes-you-should-understand-backprop-e2f06eab496b) really well.

![Power Matrix](pictures/power_matrix.png)

Intuitively, the vanishing and exploding gradient problem refers to the fact that gradients through such a graph are also scaled according to `Diag(\lambda)^t`. Vanishing gradients make it diﬃcult to know which direction the parameters should move to improve the cost function, while exploding gradients can make learning unstable. 

There are different solutions for this problem. In the case of exploding gradient, as we mentioned earlier, gradient clipping (a hack) is the most effective strategy now. For vanishing gradient, many new NN architecture has been proposed (think GRU, LSTM, ResNet) to add a gradient highway for identity gradient to flow through.


## Gradient Descient

Andrew's DL specialization, especially [Course 2: Improving Deep Neural Networks: Hyperparameter tuning, Regularization and Optimization](https://www.coursera.org/learn/deep-neural-network/home/welcome), in my opinion, does the best job in explaining the topics of optimization and graident descient. 

After learning the basics about Neural Network, the parameters involved, and the loss function formulation, the main concept is then to minimize the loss function, given the input parameters. This is fundamentally an optimization problem. Because the functional form of a Nueral Network can be unwieldy, numerical optimizations are the best way to approach this.

Of all the numerical approaches, *gradient descent* is one of the most fundamental approaches, but many additional ideas have been developed, such as **momentum**, **RMSProp**, **ADAM**, all aim to speed up the process for the graident to reach the minimum. 

* [**Understand Gradient Descent**](http://cs231n.github.io/optimization-1/): By now, I kind of take this for granted already. But Stanford's CS 231N did a good job in explaining how we can approach optimization (random search, random local search, or follow the graident). It can be shown, mathematically, that moving in the direction of the gradient, is the most efficient.

* **How Far Should I move my gradient?** _The choice of how many training examples to process to update the gradient can be a very important choice_.

	* **Batch Gradient Descent**: This is known as taking one complete pass of the training data TOGETHER, and calculating the gradient over the entire training data, and update gradient once. We can do this efficiently using vectorization, but sometimes we can overshoot because the gradient takes a large step.

	* **Stochastic Gradient Descent**: The other extreme, where we take one example as ONE pass, so we are only calculating the gradient over one training example. The advantage of this is that we can move by a mini-step, but then we lose all the advantages of vectorization.

	* **Mini-batch Gradient Descent**: This is the preferred choice, where we take mini-batches of the training data, so we do not take a complete pass of the entire training data. Instead, we take small batches of it, so it might take several rounds before we take one pass (i.e. one epoch). The advantage is that we can average out the gradient direction where it has high variance, while enjoying vectorization.

![Mini-batch SGD](pictures/sgd.png)

## More Advanced Gradient-based Methods

Deep Learning researchers have been doing a lot of work to speed up the optimization routines, but it turns out that a lot of them do not generalized well, the ones that do generalized well involved calculating the **expoential weighted averages** of the first and second moment of the gradients.

### Exponential Weighted Average

[**Exponential Weighted Average**](https://www.coursera.org/learn/deep-neural-network/lecture/Ud7t0/understanding-exponentially-weighted-averages): I love Andrew's explanation on this topic, it's the math behind these newer optimization routines. The idea is that we will take the exponential weighted average of the first & second moment of the gradient, to smooth up the updates.

![Exponential Weighted Average](pictures/exponential_weighted_average.png)

### SGD with Momentum

[**Gradient Descent Momentum**](https://www.coursera.org/learn/deep-neural-network/lecture/y0m1f/gradient-descent-with-momentum): The key idea is to imagine that you have a optimization problem with ill conditioning of the Hessian Matrix (geometrically, this corresponds to a very narrow, long countour surface area with steep walls). 

![Momentum Geometry](pictures/momentum_geometry.png)

Without momentum, typical gradient descent would just traverse and oscillate between the sides of the walls, but with momentum , it will average out / smooth out the gradients using exponential weighted average, to make the gradient more centered / less brittle. Essentially, instead of updating by `learning_rate * gradient`, we update `learning_rate * exponential_weighted_avg(gradient)`

![Momentum](pictures/momentum.png)

### SGD with RMSprop

![RMSprop Geometry](pictures/rms_prop_geometry.png)

[**Gradient Descent with RMSprop**](https://www.coursera.org/learn/deep-neural-network/lecture/BhJlm/rmsprop): The key idea is to update less aggressively on gradient directions that are volatile, and update more aggressively on gradient directions that are stable. Instead of updating by `learning_rate * gradient`, we update `learning_rate * gradient / exponential_weighted_avg(gradient ** 2)`

![RMSprop](pictures/rmsprop.png)

### ADAM

[**ADAM**](https://www.coursera.org/learn/deep-neural-network/lecture/w9VCZ/adam-optimization-algorithm): This combines Momentum & RMSprop, so not only do we average out the brittle gradient direction, we update more aggressively on gradient directions that are stable, and less aggressively on gradient directions that are volatile. Update by `learning rate * exponential_weighted_avg(gradient) / exponential_weighted_avg(gradient ** 2)`

![ADAM](pictures/adam.png)

### Comparison of All SGD-style Optimization Above

The [notes from CS 231N](http://cs231n.stanford.edu/slides/2017/cs231n_2017_lecture7.pdf) are fantastic, so I would suggest to look over the slides to reinforce the idea beyond these fancy optimization algorithms.

## Babysitting the Learning Process

There are multiple useful quantities you should monitor during training of a neural network. These plots are the window into the training process and should be utilized to get intuitions about different hyperparameter settings and how they should be changed for more efficient learning.

The x-axis of the plots below are always in units of epochs, which measure how many times every example has been seen during training in expectation (e.g. one epoch means that every example has been seen once). It is preferable to track epochs rather than iterations since the number of iterations depends on the arbitrary setting of batch size.

### Loss function

The first quantity that is useful to track during training is the loss, as it is evaluated on the individual batches during the forward pass. Below is a cartoon diagram showing the loss over time, and especially what the shape might tell you about the learning rate:

![Loss](pictures/loss_over_epoch.png)

### Train v.s. Validation Error

This is the most classic diagnostic, where we compare the gap between training and error:

* If validation accuracy is much lower than training accuracy, it suggests that there is strong overfitting, in such case we should apply regularization.

* If validation accuracy is about the same as training accuracy and they are both low, this might suggest that the model is underfitting and we should increase the model capacity.

![Accuracy over time](pictures/acc_over_epoch.png)

### Learning Rate

In training deep networks, it is usually helpful to anneal the learning rate over time. Good intuition to have in mind is that with a high learning rate, the system contains too much kinetic energy and the parameter vector bounces around chaotically, unable to settle down into deeper, but narrower parts of the loss function. Knowing when to decay the learning rate can be tricky: Decay it slowly and you’ll be wasting computation bouncing around chaotically with little improvement for a long time. But decay it too aggressively and the system will cool too quickly, unable to reach the best position it can. There are three common types of implementing the learning rate decay: 

* **Step Decay**: Reduce the learning rate by some factor every few epochs. Typical values might be reducing the learning rate by a half every 5 epochs, or by 0.1 every 20 epochs. These numbers depend heavily on the type of problem and the model. One heuristic you may see in practice is to watch the validation error while training with a fixed learning rate, and reduce the learning rate by a constant (e.g. 0.5) whenever the validation error stops improving.

* **Exponential decay**: has the mathematical form `α=α0e−kt`, where `α0`, `k` are hyperparameters and `t` is the iteration number (but you can also use units of epochs).

* **1/t decay**: has the mathematical form `α=α0/(1+kt)` where `a0`, `k` are hyperparameters and `t` is the iteration number.

In practice, we find that the step decay is slightly preferable because the hyperparameters it involves (the fraction of decay and the step timings in units of epochs) are more interpretable than the hyperparameter k. Lastly, if you can afford the computational budget, err on the side of slower decay and train for a longer time.

One last quantity you might want to track is the ratio of the `update magnitudes` to the `value magnitudes`. Note: updates, not the raw gradients (e.g. in vanilla sgd this would be the gradient multiplied by the learning rate). You might want to evaluate and track this ratio for every set of parameters independently. A rough heuristic is that this ratio should be somewhere around `1e-3`. If it is lower than this then the learning rate might be too low. If it is higher then the learning rate is likely too high. 

![Decrease Learning Rate](pictures/decrease_learning_rate.png)
