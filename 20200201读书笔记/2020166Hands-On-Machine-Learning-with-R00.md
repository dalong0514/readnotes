# 2020166Hands-On-Machine-Learning-with-R00

## 记忆时间

## 卡片

### 0101. 主题卡——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡——Machine Learning

Machine Learning is the science (and art) of programming computers so they can learn from data. Here is a slightly more general definition:

[Machine Learning is the] field of study that gives computers the ability to learn without being explicitly programmed.

—Arthur Samuel, 1959

And a more engineering-oriented one:

A computer program is said to learn from experience E with respect to some task T and some performance measure P, if its performance on T, as measured by P, improves with experience E.

—Tom Mitchell, 1997

For example, your spam filter is a Machine Learning program that can learn to flag spam given examples of spam emails (e.g., flagged by users) and examples of regular (nonspam, also called “ham”) emails. The examples that the system uses to learn are called the training set. Each training example is called a training instance (or sample). In this case, the task T is to flag spam for new emails, the experience E is the training data, and the performance measure P needs to be defined; for example, you can use the ratio of correctly classified emails. This particular performance measure is called accuracy and it is often used in classification tasks. If you just download a copy of Wikipedia, your computer has a lot more data, but it is not suddenly better at any task. Thus, it is not Machine Learning.

2『机器学习的定义，做一张术语卡片。』——已完成

### 0202. 术语卡——

### 0203. 术语卡——

### 0301. 人名卡——Aurélien Géron

Aurélien Géron，本书作者，机器学习领域的大牛。文笔很好的作者。

Aurélien Géron is a Machine Learning consultant. A former Googler, he led the YouTube video classification team from 2013 to 2016. He was also a founder and CTO of Wifirst from 2002 to 2012, a leading Wireless ISP in France; and a founder and CTO of Polyconseil in 2001, the firm that now manages the electric car sharing service Autolib’.

Before this he worked as an engineer in a variety of domains: finance (JP Morgan and Société Générale), defense (Canada’s DOD), and healthcare (blood transfusion). He published a few technical books (on C++, WiFi, and internet architectures), and was a Computer Science lecturer in a French engineering school.

A few fun facts: he taught his three children to count in binary with their fingers (up to 1023), he studied microbiology and evolutionary genetics before going into software engineering, and his parachute didn’t open on the second jump.

### 0401. 金句卡——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 行动卡——

行动卡是能够指导自己的行动的卡。

### 0601. 任意卡——

最后还有一张任意卡，记录个人阅读感想。

## Preface

1『明显又是一个文笔很好的作者，读了几段下来感觉很舒服。（2020-11-18）』

### 01. The Machine Learning Tsunami

In 2006, Geoffrey Hinton et al. published a paper [1] showing how to train a deep neural network capable of recognizing handwritten digits with state-of-the-art precision (>98%). They branded this technique “Deep Learning.” Training a deep neural net was widely considered impossible at the time, [2] and most researchers had abandoned the idea since the 1990s. This paper revived the interest of the scientific community and before long many new papers demonstrated that Deep Learning was not only possible, but capable of mind-blowing achievements that no other Machine Learning (ML) technique could hope to match (with the help of tremendous computing power and great amounts of data). This enthusiasm soon extended to many other areas of Machine Learning.

Fast-forward 10 years and Machine Learning has conquered the industry: it is now at the heart of much of the magic in today’s high-tech products, ranking your web search results, powering your smartphone’s speech recognition, recommending videos, and beating the world champion at the game of Go. Before you know it, it will be driving your car.

1『目前的理解，machine learning 其实在 1990s 年代被提出来了，印象中就是西蒙提出来的，但局限于当时计算机的性能（无法高效处理大批量数据），一直找不到实际应用。但在 06 年，Geoffrey Hinton 的论文又点燃了 ML 的实际应用。（2020-11-18）』

1 Available on Hinton’s home page at [Home Page of Geoffrey Hinton](http://www.cs.toronto.edu/~hinton/).

2 Despite the fact that Yann Lecun’s deep convolutional neural networks had worked well for image recognition since the 1990s, although they were not as general purpose.

2『在 Hinton 的主页里，正巧看到他在 nature 上发表的深度学习相关的论文，已下载作为本书附件「2020166附件0101-Nature-Deep-Review」。』

### 02. Machine Learning in Your Projects

So naturally you are excited about Machine Learning and you would love to join the party! Perhaps you would like to give your homemade robot a brain of its own? Make it recognize faces? Or learn to walk around?

Or maybe your company has tons of data (user logs, financial data, production data, machine sensor data, hotline stats, HR reports, etc.), and more than likely you could unearth some hidden gems if you just knew where to look; for example: 1) Segment customers and find the best marketing strategy for each group. 2) Recommend products for each client based on what similar clients bought. 3) Detect which transactions are likely to be fraudulent. 4) Forecast next year’s revenue. 5) And more.

Whatever the reason, you have decided to learn Machine Learning and implement it in your projects. Great idea!

### 03. Objective and Approach

This book assumes that you know close to nothing about Machine Learning. Its goal is to give you the concepts, the intuitions, and the tools you need to actually implement programs capable of learning from data. We will cover a large number of techniques, from the simplest and most commonly used (such as linear regression) to some of the Deep Learning techniques that regularly win competitions.

Rather than implementing our own toy versions of each algorithm, we will be using actual production-ready Python frameworks:

1. Scikit-Learn is very easy to use, yet it implements many Machine Learning algorithms efficiently, so it makes for a great entry point to learn Machine Learning.

2. TensorFlow is a more complex library for distributed numerical computation. It makes it possible to train and run very large neural networks efficiently by distributing the computations across potentially hundreds of multi-GPU servers. TensorFlow was created at Google and supports many of their large-scale Machine Learning applications. It was open sourced in November 2015.

3. Keras is a high level Deep Learning API that makes it very simple to train and run neural networks. It can run on top of either TensorFlow, Theano or Microsoft Cognitive Toolkit (formerly known as CNTK). TensorFlow comes with its own implementation of this API, called tf.keras, which provides support for some advanced TensorFlow features (e.g., to efficiently load data).

The book favors a hands-on approach, growing an intuitive understanding of Machine Learning through concrete working examples and just a little bit of theory. While you can read this book without picking up your laptop, we highly recommend you experiment with the code examples available online as Jupyter notebooks at [ageron/handson-ml2: A series of Jupyter notebooks](https://github.com/ageron/handson-ml2).

1-2『上面的 git 仓库里有详细的使用说明，目前已经下载仓库放在根目录下的「MachienLearning」文件夹。（2020-11-11）』

### 04. Prerequisites

This book assumes that you have some Python programming experience and that you are familiar with Python’s main scientific libraries, in particular NumPy, Pandas, and Matplotlib. Also, if you care about what’s under the hood you should have a reasonable understanding of college-level math as well (calculus, linear algebra, probabilities, and statistics).

If you don’t know Python yet, http://learnpython.org/ is a great place to start. The official tutorial on python.org is also quite good. If you have never used Jupyter, Chapter 2 will guide you through installation and the basics: it is a great tool to have in your toolbox. If you are not familiar with Python’s scientific libraries, the provided Jupyter notebooks include a few tutorials. There is also a quick math tutorial for linear algebra.

1『哈哈，目前这些先决条件自己基本都满足。（2020-11-11）』

### 05. Roadmap

This book is organized in two parts. Part I, The Fundamentals of Machine Learning, covers the following topics:

1. What is Machine Learning? What problems does it try to solve? What are the main categories and fundamental concepts of Machine Learning systems?

2. The main steps in a typical Machine Learning project.

3. Learning by fitting a model to data.

4. Optimizing a cost function.

5. Handling, cleaning, and preparing data.

6. Selecting and engineering features.

7. Selecting a model and tuning hyperparameters using cross-validation.

8. The main challenges of Machine Learning, in particular underfitting and overfitting (the bias/variance tradeoff).

9. Reducing the dimensionality of the training data to fight the curse of dimensionality.

10. Other unsupervised learning techniques, including clustering, density estimation and anomaly detection.

11. The most common learning algorithms: Linear and Polynomial Regression, Logistic Regression, k-Nearest Neighbors, Support Vector Machines, Decision Trees, Random Forests, and Ensemble methods.

Part II, Neural Networks and Deep Learning, covers the following topics:

1. What are neural nets? What are they good for?

2. Building and training neural nets using TensorFlow and Keras.

3. The most important neural net architectures: feedforward neural nets, convolutional nets, recurrent nets, long short-term memory (LSTM) nets, autoencoders and generative adversarial networks (GANs).

4. Techniques for training deep neural nets.

5. Scaling neural networks for large datasets.

6. Learning strategies with Reinforcement Learning.

7. Handling uncertainty with Bayesian Deep Learning.

The first part is based mostly on Scikit-Learn while the second part uses TensorFlow and Keras.

Don’t jump into deep waters too hastily: while Deep Learning is no doubt one of the most exciting areas in Machine Learning, you should master the fundamentals first. Moreover, most problems can be solved quite well using simpler techniques such as Random Forests and Ensemble methods (discussed in Part I). Deep Learning is best suited for complex problems such as image recognition, speech recognition, or natural language processing, provided you have enough data, computing power, and patience.

### 06. Other Resources

Many resources are available to learn about Machine Learning. Andrew Ng’s ML course on Coursera and Geoffrey Hinton’s course on neural networks and Deep Learning are amazing, although they both require a significant time investment (think months).

There are also many interesting websites about Machine Learning, including of course Scikit-Learn’s exceptional User Guide. You may also enjoy Dataquest, which provides very nice interactive tutorials, and ML blogs such as those listed on Quora. Finally, the Deep Learning website has a good list of resources to learn more.

Of course there are also many other introductory books about Machine Learning, in particular:

1. Joel Grus, Data Science from Scratch (O’Reilly). This book presents the fundamentals of Machine Learning, and implements some of the main algorithms in pure Python (from scratch, as the name suggests).

2. Stephen Marsland, Machine Learning: An Algorithmic Perspective (Chapman and Hall). This book is a great introduction to Machine Learning, covering a wide range of topics in depth, with code examples in Python (also from scratch, but using NumPy).

3. Sebastian Raschka, Python Machine Learning (Packt Publishing). Also a great introduction to Machine Learning, this book leverages Python open source libraries (Pylearn 2 and Theano).

3. François Chollet, Deep Learning with Python (Manning). A very practical book that covers a large range of topics in a clear and concise way, as you might expect from the author of the excellent Keras library. It favors code examples over mathematical theory.

4. Yaser S. Abu-Mostafa, Malik Magdon-Ismail, and Hsuan-Tien Lin, Learning from Data (AMLBook). A rather theoretical approach to ML, this book provides deep insights, in particular on the bias/variance tradeoff (see Chapter 4).

5. Stuart Russell and Peter Norvig, Artificial Intelligence: A Modern Approach, 3rd Edition (Pearson). This is a great (and huge) book covering an incredible amount of topics, including Machine Learning. It helps put ML into perspective.

Finally, a great way to learn is to join ML competition websites such as Kaggle.com this will allow you to practice your skills on real-world problems, with help and insights from some of the best ML professionals out there.

3『

吴恩达的深度学习课：[Machine Learning | Coursera](https://www.coursera.org/learn/machine-learning)。

Geoffrey Hinton 的神经网络的课在 Coursera 上没找到，反而又看到吴恩达新出的神经网络课：[Neural Networks and Deep Learning | Coursera](https://www.coursera.org/learn/neural-networks-deep-learning)。

[User guide: contents — scikit-learn 0.23.2 documentation](https://scikit-learn.org/stable/user_guide.html)

[Learn R, Python and SQL for Data Science | Dataquest](https://www.dataquest.io/)

[Deep Learning](http://deeplearning.net/)

（2020-11-11）

』

### 10. Changes in the Second Edition

This second edition has five main objectives:

1 Cover additional topics: additional unsupervised learning techniques (including clustering, anomaly detection, density estimation and mixture models), additional techniques for training deep nets (including self-normalized networks), additional computer vision techniques (including the Xception, SENet, object detection with YOLO, and semantic segmentation using R-CNN), handling sequences using CNNs (including WaveNet), natural language processing using RNNs, CNNs and Transformers, generative adversarial networks, deploying TensorFlow models, and more.

2 Update the book to mention some of the latest results from Deep Learning research.

3 Migrate all TensorFlow chapters to TensorFlow 2, and use TensorFlow’s implementation of the Keras API (called tf.keras) whenever possible, to simplify the code examples.

4 Update the code examples to use the latest version of Scikit-Learn, NumPy, Pandas, Matplotlib and other libraries.

5 Clarify some sections and fix some errors, thanks to plenty of great feedback from readers.

Some chapters were added, others were rewritten and a few were reordered. Table P-1 shows the mapping between the 1 st edition chapters and the 2 nd edition chapters:

More specifically, here are the main changes for each 2 nd edition chapter (other than clarifications, corrections and code updates):

Chapter 1 

— Added a section on handling mismatch between the training set and the validation & test sets.

Chapter 2 

— Added how to compute a confidence interval.

— Improved the installation instructions (e.g., for Windows).

— Introduced the upgraded OneHotEncoder and the new ColumnTransformer.

Chapter 4 

— Explained the need for training instances to be Independent and Identically Distributed (IID).

Chapter 7 

— Added a short section about XGBoost.

Chapter 9, new chapter including:

— Clustering with K-Means, how to choose the number of clusters, how to use it for dimensionality reduction, semi-supervised learning, image segmentation, and more.

— The DBSCAN clustering algorithm and an overview of other clustering algorithms available in Scikit-Learn.

— Gaussian mixture models, the Expectation-Maximization (EM) algorithm, Bayesian variational inference, and how mixture models can be used for clustering, density estimation, anomaly detection and novelty detection.

— Overview of other anomaly detection and novelty detection algorithms.

Chapter 10 (mostly new) 

— Added an introduction to the Keras API, including all its APIs (Sequential, Functional and Subclassing), persistence and callbacks (including the Tensor Board callback).

Chapter 11 (many changes) — Introduced self-normalizing nets, the SELU activation function and Alpha Dropout.

— Introduced self-supervised learning.

— Added Nadam optimization.

— Added Monte-Carlo Dropout.

— Added a note about the risks of adaptive optimization methods.

— Updated the practical guidelines.

Chapter 12, completely rewritten chapter, including:

— A tour of TensorFlow 2 

— TensorFlow’s lower-level Python API 

— Writing custom loss functions, metrics, layers, models 

— Using auto-differentiation and creating custom training algorithms. 

— TensorFlow Functions and graphs (including tracing and autograph).

Chapter 13, new chapter, including:

— The Data API. 

— Loading/Storing data efficiently using TFRecords 

— The Features API (including an introduction to embeddings).

— An overview of TF Transform and TF Datasets 

— Moved the low-level implementation of the neural network to the exercises.

— Removed details about queues and readers that are now superseded by the Data API.

Chapter 14 

— Added Xception and SENet architectures.

— Added a Keras implementation of ResNet-34.

— Showed how to use pretrained models using Keras.

— Added an end-to-end transfer learning example.

— Added classification and localization.

— Introduced Fully Convolutional Networks (FCNs).

— Introduced object detection using the YOLO architecture. — Introduced semantic segmentation using R-CNN.

Chapter 15 

— Added an introduction to Wavenet.

— Moved the Encoder–Decoder architecture and Bidirectional RNNs to Chapter.

Chapter 16 

— Explained how to use the Data API to handle sequential data.

— Showed an end-to-end example of text generation using a Character RNN, using both a stateless and a stateful RNN.

— Showed an end-to-end example of sentiment analysis using an LSTM.

— Explained masking in Keras.

— Showed how to reuse pretrained embeddings using TF Hub.

— Showed how to build an Encoder–Decoder for Neural Machine Translation using TensorFlow Addons/seq2seq.

— Introduced beam search.

— Explained attention mechanisms.

— Added a short overview of visual attention and a note on explainability.

— Introduced the fully attention-based Transformer architecture, including positional embeddings and multi-head attention.

— Added an overview of recent language models (2018).

Chapters 17, 18 and 19: coming soon.