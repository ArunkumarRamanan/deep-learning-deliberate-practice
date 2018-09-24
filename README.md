# Deep Learning Deliberate Practice

In 2018, I will take on a new learning project - to deliberately **learn** and **practice** Deep Learning.

## Some Inspirations

From Andrew Ng and his [answer](https://www.quora.com/How-should-you-start-a-career-in-Machine-Learning) on Quora:

> Every Saturday, you will have a choice between staying at home and reading research papers/implementing algorithms, vs. watching TV. If you spend all Saturday working, there probably won't be any short-term reward, and your current boss won't even know or say "nice work." Also, after that Saturday of hard work, you're not actually that much better at machine learning. But here's the secret: If you do this not just for one weekend, but instead study consistently for a year, then you will become very good.

Anecdotal story: Aside from taking his CS 229 at Stanford when I was a student there, I've ran into him several times at different cafes around South Bay on Saturdays, and everytime I saw him, he was either working or learning something, very inspiring!

## Recap on Previous Learning Projects

In early 2016, I made the [decision](https://medium.com/@rchang/advice-for-new-and-junior-data-scientists-2ab02396cf5b) to transition from Type A Data Scientist to Type B Data scientist. As I started taking on less inference work and more data engineering and machine learning projects. I took on a [leanring project](https://github.com/robert8138/python-deliberate-practice) in late 2016 to switch from R to Python. This was a "pre-requisite" for me to succeed at Airbnb because doing Data Engineering or building Machine Learning models at Airbnb are generally much easier with Python. This small learning project turned out to be one of the best investments that I made for my technical growth at Airbnb.

Because of this investment, I was able to march on and take on two very big projects ([Listing LTV](https://medium.com/airbnb-engineering/using-machine-learning-to-predict-value-of-homes-on-airbnb-9272d3d4739d) and Homes Metrics), both of which heavily involved Airflow and frameworks built on top of Airflow. Specifically, I was able to navigate the codebase of these frameworks, find bugs, and become a better user and collaborator with DE and ML Infra. Throughout the process, I learned a ton about how to build offline training, offline scoring ML models, and my knowledge in Data Engineering has increased dramatically. 

Interestingly, 2017 was the first year in my professional career where the majority of my technical growth came from on the job training rather than self study. This was one big experiment, but I think it paid off. This approach was also aligned with what Cal Newport and Scott Young advocate:

> The best approach wasn’t to try to persuade people to carve out huge chunks of their life for deliberate practice (which they were unable to do), but rather to carefully pick projects that would be able to simultaneously reach both goals: achieving a legitimate object of work and also pushing deliberate practice.

## Motivation for Learning DL

In early 2018, I have decided to transition to the Select team to focus on applied Machine Learning. Specifically, there is general buy-ins from the team, my future manager, and my immediate teammates that Machine Learning will be critical to scale the program in 2018. Among of the many areas that we can tackle on Select, one of which is to better leverage Airbnb's collection of Home images, and to do work like [categorizing Airbnb photos](https://medium.com/airbnb-engineering/categorizing-listing-photos-at-airbnb-f9483f3ab7e3) (not my work, though I am a consumer of this model). 

As a result, I foresee that the class of problems that I will be dealing with, fall closely under the realm of Deep Learning, and this is the best opportunity for me to achieve deliberate practice on an increasingly important skill that will allow us to unlock enormous business values in the future.

## Pursue Metrics that Matter

As I was thinking about success metrics for this DL Deliberate Learning Project, Cal Newport's [blog post](http://calnewport.com/blog/2015/06/16/pursue-metrics-that-matter/) came to mind again. His thesis is this: 

> When deciding to embrace a self-motivated ambition, choose a definition of success that your aunt in Peoria would understand and find impressive. This is not about succumbing to the status quo, but instead setting yourself up to receive the brutal but useful feedback needed to eventually start producing things too good to be ignored. 

His Advice: Focus on **Conventional Competitive Metrics** that will keep you brutually honest (e.g. Want to get good at writing, set a goal to publish a book; want to prove you are getting better at DL, try Hacker Rank test for deeplearning.ai [AI Bootcamp](https://www.deeplearning.ai/ai-bootcamp) to see if you are accepted, etc).

## Course Planning

Like any learning project, it is generally wise to take a week or two to compile the list of study materials, trial study them, and then finalize on the final curriculum. Luckily, this topic is so hot that there are already many useful obvious candidates or even reviews of these candidate courses. Here are a few:

### University Courses

* [Fast.ai](http://wiki.fast.ai/index.php/Main_Page): Top-down teaching approach by Jeremy Howard and Rachel Thomas
* [Coursera's Deep Learning Specialization](https://www.coursera.org/specializations/deep-learning): Bottom-up teaching approach
* [Stanford CS 231N: Convolutional Neural Network](http://cs231n.stanford.edu/syllabus.html): This is highly recommended by Jiaying and Heerad. This is probably also the most rigorous course of the three mentioned here because it's an actual Stanford Course. I was told the Homeworks are superb and I should definitely do them.
* [Stanford CS 224N: Natural Language Processing with Deep Learning](http://web.stanford.edu/class/cs224n/): Focus on NLP, word vector representations, window-based neural networks, recurrent neural networks, long-short-term-memory models, recursive neural networks, convolutional neural networks as well as some recent models involving a memory component.
* [Stanford CS 230: Deep Learning](http://cs230.stanford.edu/syllabus.html): This course is based on Andrew Ng's Coursera deep learning specialization courses, with additional materials taught during classroom settings. Great classroom notes and [Tutorials on Tensorflow](https://cs230-stanford.github.io/).

### Toolings: Keras & Tensorflow

A few words on why I choose to focus on Keras (for now): Rachel Thomas summarized her [reasons](http://www.fast.ai/2017/01/03/keras/) quite well (although fast.ai have moved to Pytorch since). It boils down to Keras has the most thoughtfully designed, expressive API. After just using tensorflow very briefly, I felt the same. Francis Chollet even wrote a blog post on his philosophy on [designing APIs](https://blog.keras.io/author/francois-chollet.html), which I thought was quite a good read. Finally, Keras is officially [integrated](http://www.fast.ai/2017/01/03/keras/) into tensorflow as a high level library.

* [Deep Learning with Python](https://www.manning.com/books/deep-learning-with-python): Deep Learning with Python introduces the field of deep learning using the Python language and the powerful Keras library. Written by Keras creator and Google AI researcher François Chollet, this book builds your understanding through intuitive explanations and practical examples. I heard a lot of great things about this book.

* [Stanford CS 20: Tensorflow for Deep Learning Research](http://web.stanford.edu/class/cs20si/): This course will cover the fundamentals and contemporary usage of the Tensorflow library for deep learning research. We aim to help students understand the graphical computational model of TensorFlow, explore the functions it has to offer, and learn how to build and structure models best suited for a deep learning project. Through the course, students will use TensorFlow to build models of different complexity, from simple linear/logistic regression to convolutional neural network and recurrent neural networks to solve tasks such as word embedding, translation, optical character recognition, reinforcement learning. Students will also learn best practices to structure a model and manage research experiments.

* [Coursera/Google Cloud ML Specialization](https://www.coursera.org/learn/intro-tensorflow): Introduction to Tensorflow

### Textbook

* [Deep Learning](http://www.deeplearningbook.org/): Written by Ian Goodfellow, Yoshua Bengio, and Aaron Courville. This is the book which covers in detail the mathematical underpinnings of many DL topics.

* [Deep Learning with Python](https://www.manning.com/books/deep-learning-with-python): Deep Learning with Python introduces the field of deep learning using the Python language and the powerful Keras library. Written by Keras creator and Google AI researcher François Chollet, this book builds your understanding through intuitive explanations and practical examples. I heard a lot of great things about this book.

### Blogs 

#### Deep Learning

* [Fast.ai](http://www.fast.ai/)
	* [What you need (Hardware, Software) for Deep Learning](http://www.fast.ai/2017/11/16/what-you-need/): This is a great introduction on the kind of hardware and software you need to do DL. In my opinion, it's probably a lot easier to just use a docker environment and launch a GPU on AWS (for hardware) and use a framework that has user friendly APIs so you can learn the major concepts (for software).
	* [How to learn deep learning (when you are not a computer science Ph.D)](https://vimeo.com/214233053)
	* [Fast.ai: An Introduction to Deep Learning for Tabular Data](http://www.fast.ai/2018/04/29/categorical-embeddings/)

* [Andrej Karpathy's blog](http://karpathy.github.io/)
	* [The Unreasonable Effectiveness of Recurrent Neural Networks](http://karpathy.github.io/2015/05/21/rnn-effectiveness/)
	* [Yes, you should understand backprop](https://medium.com/@karpathy/yes-you-should-understand-backprop-e2f06eab496b)

* [Colab](http://colah.github.io/): His intuitive explanation of DL topics are very well regarded, and something that I plan to revisit from time to time.
	* [Deep Learning & Representation]((https://colah.github.io/posts/2014-07-NLP-RNNs-Representations/))

* [Distill.pub: An Interactive, Visual Journal for Machine Learning Research](https://distill.pub/): The web has been around for almost 30 years. But you wouldn’t know it if you looked at most academic journals. They’re stuck in the early 1900s. PDFs are not an exciting form. Distill is taking the web seriously. A Distill article (at least in its ideal, aspirational form) isn’t just a paper. It’s an interactive medium that lets users – “readers” is no longer sufficient – work directly with machine learning models. See Distill.pub announcement [here](https://blog.ycombinator.com/distill-an-interactive-visual-journal-for-machine-learning-research/).

#### Machine Learning in General

* **Practical Machine Learning Advice From Google**
	* [Andrew Ng's ML Yearning - WIP](http://www.mlyearning.org/): This book is all about practical advice for how to tackle challenges in ML projects. He started off this project but got sidetracked by the Coursera DL specialization course. He is coming back to it now. I cannot emphasize how good this book is, all of my notes from reading this book are scribed [here](https://github.com/robert8138/deep-learning-deliberate-practice/blob/master/concepts/work_in_progress/structure_ml_project.md#yet-another-tool-to-diagnoise-bias-vs-variance-learning-curve).
	* [Rules of ML: Best Practice for ML Engineering](https://developers.google.com/machine-learning/rules-of-ml/): This document is intended to help those with a basic knowledge of machine learning get the benefit of best practices in machine learning from around Google. [PDF]((http://martin.zinkevich.org/rules_of_ml/rules_of_ml.pdf)) is also available.
	* [Machine Learning: The High-Interest Credit Card of Technical Debt](https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/43146.pdf): The goal of this paper is highlight several machine learning specific risk factors and design patterns to be avoided or refactored where possible. These include boundary erosion, entanglement, hidden feedback loops, undeclared consumers, data dependencies, changes in the external world, and a variety of system-level anti-patterns.
	* [The Hidden Technical Debt in Machine Learning Systems](https://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems.pdf): Machine learning offers a fantastically powerful toolkit for building useful complex prediction systems quickly. This paper argues it is dangerous to think of these quick wins as coming for free. Using the software engineering framework of technical debt, we find it is common to incur massive ongoing maintenance costs in real-world ML systems. We explore several ML-specific risk factors to account for in system design. These include boundary erosion, entanglement, hidden feedback loops, undeclared consumers, data dependencies, configuration issues, changes in the external world, and a variety of system-level anti-patterns.
	* [What’s your ML Test Score? A rubric for ML production systems](https://www.eecs.tufts.edu/~dsculley/papers/ml_test_score.pdf)

* **Practical Machine Learning Advice From Other Top Companies**
	* [Dimensions of Machine Learning Models](https://www.slideshare.net/SharathRao6/lessons-from-integrating-machine-learning-models-into-data-products): Less relevant to Deep Learning specifically, but this is still by far the best piece that I can find in categorizing different ML models (contextual data dimension v.s. latency requirement dimension). [Video](https://www.youtube.com/watch?v=wG5EyHYrJGE&t=891s) from DataEngConf2017 is also available.
	* [Facebook's Machine Learning Field Guide](https://research.fb.com/the-facebook-field-guide-to-machine-learning-video-series/): A very nice introduction to ML in the industry. I thought this is a pretty accurate description of things and considerations that I run into at work.
	* [The Two Cultures of Machine Learning Systems](https://medium.com/opendoor-labs/the-two-cultures-of-machine-learning-systems-c648db0bb4d8): How ML Engineers and Data Scientists approach ML differently

* **What Does a Machine Learning Engineer Do?**
	* [What is Hardcore Data Science – In Practice?](https://www.oreilly.com/ideas/what-is-hardcore-data-science-in-practice): The title is a bit misleading, but the content is pretty good. In particular, it talks about several high level mental model / picture how one would do modeling work that is a part of a ML system. The author does a good job explaining and highlights his approach in creating micro-services to containerize model as an API endpoint. This reminds of ML Infra at Airbnb. 
	* [What do machine learning practitioners actually do?](http://www.fast.ai/2018/07/12/auto-ml-1/): It's a 3-part blog post series where Rachel argued that architecture search in DL is actually a very niche / small component of a typical machine learning workflow. In explaining how she favors transfer learning over finding new architecture for each problem, she explains the workflow of real life ML projects. It really aligns with what I do in practice. [Part II](http://www.fast.ai/2018/07/16/auto-ml2/) and [Part III](http://www.fast.ai/2018/07/23/auto-ml-3/) are more about AutoML, interested readers can read this as well.
	* [What does a Machine Learning Engineer Do?](https://medium.com/@tomaszdudek/but-what-is-this-machine-learning-engineer-actually-doing-18464d5c699)


## To Keep Learning

### **Research Track**: 

* Try to implement basic neural network from scratch (e.g. CS 231N homeworks)
* Read a lot of papers from [arxiv](https://arxiv.org/), then try to replicate the results. From [Andrew](https://www.quora.com/I-want-to-pursue-machine-learning-as-a-career-but-not-sure-if-I-am-qualified-How-can-I-test-myself/answer/Andrew-Ng):

> To go even further, read research papers (follow ML leaders on twitter to see what papers they’re excited about). Even better, try to replicate the results in the research papers. Trying to replicating others’ results is a one of the most effective but under-appreciated ways to get good at AI. Also consider activities like online ML competitions, academic conferences, and keep reading books/blogs/papers.

* [Arxiv Sanity Checker](http://www.arxiv-sanity.com/): personalized newsfeed for Arxiv, Karpathy's project, to surface interesting research paper to you based on your like history.
* [Bay Area Deep Learning School 2016](https://www.youtube.com/playlist?list=PLrAXtmErZgOfMuxkACrYnD2fTgbzk2THW): A good overview of everything at Stanford, from 2 years ago
* [Getting started with reading Deep Learning Research papers: The Why and the How](https://towardsdatascience.com/getting-started-with-reading-deep-learning-research-papers-the-why-and-the-how-dfd1ac15dbc0)

### **Application Track**:

* Do it the Jeremy Howard / hacker way, try to map techniques to problems, or problems to techniques
* Check out [Cutting Edge Deep Learning for Coders: 2018 edition](http://www.fast.ai/2018/05/07/part2-launch/)
* A lot of opportunity to do this on my current team, since we have a lot of image-related tasks

### **Math Track**:

* [Computational Linear Algebra](http://www.fast.ai/2017/07/17/num-lin-alg/): A great course from fast.ai on computational linear algebra, heavily focused on applications of LA (e.g. SVD -> PCA, etc.)
* [Matrix Calculus for Deep Learning](http://parrt.cs.usfca.edu/doc/matrix-calculus/index.html): Also written by Jeremy Howard, I haven't checked it out, but this just reminded me of my undergraduate Math 105: Real Analysis and Measure Theory.
* [Learning Math for Machine Learning](https://blog.ycombinator.com/learning-math-for-machine-learning/)