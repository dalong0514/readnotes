# 2020021Machine-Learning-By-Andrew-NgR00

[Welcome | Coursera](https://www.coursera.org/learn/machine-learning/lecture/RKFpn/welcome)

[Lecture 1.1 — What Is Machine Learning — [ Machine Learning | Andrew Ng ] - YouTube](https://www.youtube.com/watch?v=PPLop4L2eGk&list=PLLssT5z_DsK-h9vYZkQkYNWcItqhlRJLN&index=1)

## 记忆时间

## 卡片

### 0101. 主题卡——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡——Machine Learning

Two definitions of Machine Learning are offered. Arthur Samuel described it as: "the field of study that gives computers the ability to learn without being explicitly programmed." This is an older, informal definition.

Tom Mitchell provides a more modern definition: "A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P, if its performance at tasks in T, as measured by P, improves with experience E."

Here's a definition of what is machine learning as due to Arthur Samuel. He defined machine learning as the field of study that gives computers the ability to learn without being explicitly learned. Samuel's claim to fame was that back in the 1950, he wrote a checkers playing program and the amazing thing about this checkers playing program was that Arthur Samuel himself wasn't a very good checkers player. But what he did was he had to programmed maybe tens of thousands of games against himself, and by watching what sorts of board positions tended to lead to wins and what sort of board positions tended to lead to losses, the checkers playing program learned over time what are good board positions and what are bad board positions. And eventually learn to play checkers better than the Arthur Samuel himself was able to. 

1『晕死，这里的英文名 Samuel 就是自己超级推崇的天才「赫伯特·西蒙」，哈哈。（2020-11-15）』

This was a remarkable result. Arthur Samuel himself turns out not to be a very good checkers player. But because a computer has the patience to play tens of thousands of games against itself, no human has the patience to play that many games. By doing this, a computer was able to get so much checkers playing experience that it eventually became a better checkers player than Arthur himself.

This is a somewhat informal definition and an older one. Here's a slightly more recent definition by Tom Mitchell who's a friend of Carnegie Melon. So Tom defines machine learning by saying that a well-posed learning problem is defined as follows. He says, a computer program is said to learn from experience E with respect to some task T and some performance measure P, if its performance on T, as measured by P, improves with experience E. I actually think he came out with this definition just to make it rhyme. For the checkers playing examples, the experience E would be the experience of having the program play tens of thousands of games itself. The task T would be the task of playing checkers, and the performance measure P will be the probability that wins the next game of checkers against some new opponent.

On top is a definition of machine learning by Tom Mitchell. Let's say your email program watches which emails you do or do not mark as spam. So in an email client like this, you might click the Spam button to report some email as spam but not other emails. And based on which emails you mark as spam, say your email program learns better how to filter spam email. What is the task T in this setting? In a few seconds, the video will pause and when it does so, you can use your mouse to select one of these four radio buttons to let me know which of these four you think is the right answer to this question.

So hopefully you got that this is the right answer, classifying emails is the task T. In fact, this definition defines a task T performance measure P and some experience E. And so, watching you label emails as spam or not spam, this would be the experience E and and the fraction of emails correctly classified, that might be a performance measure P. And so on the task of systems performance, on the performance measure P will improve after the experience E.

In this class, I hope to teach you about various different types of learning algorithms. There are several different types of learning algorithms. The main two types are what we call supervised learning and unsupervised learning. I'll define what these terms mean more in the next couple videos. 

### 0202. 术语卡——

### 0203. 术语卡——

### 0301. 人名卡——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

### 0401. 金句卡——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 信息数据卡——

行动卡是能够指导自己的行动的卡。

### 0601. 任意卡——

最后还有一张任意卡，记录个人阅读感想。

### 链接汇总

[Welcome | Coursera](https://www.coursera.org/learn/machine-learning/lecture/RKFpn/welcome)

[Machine Learning - complete course notes](http://www.holehouse.org/mlclass/index.html)

[Lecture 1.1 — What Is Machine Learning — [ Machine Learning | Andrew Ng ] - YouTube](https://www.youtube.com/watch?v=PPLop4L2eGk&list=PLLssT5z_DsK-h9vYZkQkYNWcItqhlRJLN&index=1)

### 课程概述

这些课程专为已有一定基础（基本的编程知识，熟悉 Python、对机器学习有基本了解），想要尝试进入人工智能领域的计算机专业人士准备。介绍显示：「深度学习是科技业最热门 的技能之一，本课程将帮你掌握深度学习。」

在这 5 堂课中，学生将可以学习到深度学习的基础，学会构建神经网络，并用在包括吴恩达本人在内的多位业界顶尖专家指导下创建自己的机器学习项目。Deep Learning Specialization 对卷积神经网络（CNN）、递归神经网络（RNN）、长短期记忆（LSTM）等深度学习常用的网络结构、工具和知识都有涉及。

课程中也会有很多实操项目，帮助学生更好地应用自己学到的深度学习技术，解决真实世界问题。这些项目将涵盖医疗、自动驾驶、和自然语言处理等时髦领域，以及音乐生成等等。Coursera 上有一些特定方向和知识的资料，但一直没有比较全面、深入浅出的深度学习课程 ——《深度学习专业》的推出补上了这一空缺。

课程的语言是 Python，使用的框架是 Google 开源的 TensorFlow。最吸引人之处在于，课程导师就是吴恩达本人，两名助教均来自斯坦福计算机系。完成课程所需时间根据不同的学习进度，大约需要 3-4 个月左右。学生结课后，Coursera 将授予他们 Deep Learning Specialization 结业证书。

「我们将帮助你掌握深度学习，理解如何应用深度学习，在人工智能业界开启你的职业生涯。」吴恩达在课程页面中提到。

本人黄海广博士，以前写过吴恩达老师的机器学习个人笔记。有朋友报名了课程，下载了这次课程的视频给大家分享。Coursera 的字幕不全，同学们在学习上感觉非常不方便，因此我找志同道合的朋友翻译和整理字幕，中英文字幕来自于由我和曹骁威同学组织爱好者翻译，希望对大家有所帮助。（备注：自网易公开课翻译深度学习课程后，我们不再翻译）

目前我正在组织团队整理中文笔记，由热心的朋友无偿帮忙制作整理，并持续更新。我 们的团队的劳动致力于 AI 在国内的推广，不会损害 Coursera 以及吴恩达老师的商业利益。

### 吴恩达的公开信

朋友们，我在做三个全新的 AI 项目。现在，我十分兴奋地宣布其中的第一个：deeplearning.ai，一个立志于扩散 AI 知识的项目。该项目在 Coursera 上发布了一系列深度学习课程，这些课程将帮助你掌握深度学习、对它高效地应用，并打造属于你自己的 AI 事业。

1、AI 是新一轮电力革命。就像一百年前电力改造了每个主流行业，当今的 AI 技术在做着相同的事。好几个大型科技公司都设立了 AI 部门，用 AI 革新他们的业务。接下来的几年里，各个行业、规模大小各不相同的公司也都会意识到 —— 在由 AI 驱动的未来，他们必须成为其中的一份子。

2、创建由 AI 驱动的社会。我希望，我们可以建立一个由 AI 驱动的社会：让每个人看得起病，给每个孩子个性化的教育，让所有人都能坐上价格亲民的自动驾驶汽车，并向男人和女人提供有意义的工作。总而言之，是一个让每个人的生活变得更好的社会。

但是，任何一个公司都不可能单独完成这些任务。就像现在每一个计算机专业的毕业生都知道怎么用云，将来，每个程序员也必须懂得怎么用 AI。用深度学习改善人类生活的方法有数百万种，社会也需要数百万个人 —— 即来自世界各国的你们，来创造出了不起的 AI 系统。不管你是加州的一个软件工程师，一名中国的研究员，还是印度的 ML 工程师，我希望都能用深度学习来解决世界上的各种挑战。

3、你会学到什么。任何一个掌握了机器学习基础知识的人，都可以学习这五门系列课程，它们组成了 Coursera 的全新深度学习专业。你会学到深度学习的基础，理解如何创建神经网络，学习怎么成功地领导机器学习项目。你会学习卷积神经网络、 RNNs、LSTM、Adam、Dropout、BatchNorm、Xavier/He initialization 以及更多。学习过程中，你会接触到医疗、自动驾驶、读手语、音乐生成、 自然语言处理的案例。

你不仅会掌握深度学习理论，还会看到它是怎样在行业应用落地的。你会在 Python 和 TensorFlow 里试验这些想法，你还会听到各位深度学习领袖人物的意见，他们会分享各自的学习经历，并提供职业规划建议。当你拿到 Coursera 的深度学习专业证书，就可以自信得把「深度学习」四个字写进你的简历。加入我，建立一个由 AI 驱动的社会。从 2011 年到现在，已经有 180 万人加入了我的机器学习课程。当时，我和四名斯坦福的学生发布了这门课程，它随即成为了 Coursera 的第一门公开课。那之后，我受到你们之中许多人的启发 —— 当我看到你们是如何努力地理解机器学习，开发优秀的 AI 系统，并开启令人惊艳的事业。我希望深度学习专业能帮助你们实现更了不起的事，让你们为社会贡献更多，在职业道路上走得更远。我希望大家和我一道，建立一个由 AI 驱动的社会。我会通知大家另外两个项目的进展，并不断探索，为全世界 AI 社区的每一个人提供更多支持的途径。