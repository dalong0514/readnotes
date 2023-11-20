## 0301. Should You Learn Math to Get a Job in AI?

How much math do you need to know to be a machine learning engineer?

Is math a foundational skill for AI? It’s always nice to know more math! But there’s so much to learn that, realistically, it’s necessary to prioritize. Here’s how you might go about strengthening your math background.

To figure out what’s important to know, I find it useful to ask what you need to know to make the decisions required for the work you want to do. At DeepLearning.AI, we frequently ask, “What does someone need to know to accomplish their goals?” The goal might be building a machine learning model, architecting a system, or passing a job interview.

Understanding the math behind algorithms you use is often helpful, since it enables you to debug them. But the depth of knowledge that’s useful changes over time. As machine learning techniques mature and become more reliable and turnkey, they require less debugging, and a shallower understanding of the math involved may be sufficient to make them work.

For instance, in an earlier era of machine learning, linear algebra libraries for solving linear systems of equations (for linear regression) were immature. I had to understand how these libraries worked so I could choose among different libraries and avoid numerical roundoff pitfalls. But this became less important as numerical linear algebra libraries matured.

Deep learning is still an emerging technology, so when you train a neural network and the optimization algorithm struggles to converge, understanding the math behind gradient descent, momentum, and the Adam optimization algorithm will help you make better decisions. Similarly, if your neural network does something funny — say, it makes bad predictions on images of a certain resolution, but not others — understanding the math behind neural network architectures puts you in a better position to figure out what to do.

Of course, I also encourage learning driven by curiosity. If something interests you, go ahead and learn it regardless of how useful it might turn out to be! Maybe this will lead to a creative spark or technical breakthrough.

在 AI 找工作该不该学数学？

做一名机器学习工程师需要懂多少数学？

数学是人工智能的基础技能吗？多懂点数学总是好的！但是要学的东西太多了，实际上，有必要分清轻重缓急。以下是你如何加强你的数学背景。

为了弄清楚什么是重要的，我发现询问你需要知道什么来为你想做的工作做出决定是很有用的。在 DeepLearning.AI，我们经常问：「一个人需要知道什么来完成他们的目标？」目标可能是建立一个机器学习模型，构建一个系统，或者通过一次工作面试。

理解您所使用的算法背后的数学原理通常很有帮助，因为它使您能够调试它们。但是有用的知识深度会随着时间而变化。随着机器学习技术的成熟，变得更加可靠和交钥匙，它们需要更少的调试，对所涉及的数学有更浅的理解可能足以使它们工作。

例如，在机器学习的早期时代，用于求解线性方程组（用于线性回归）的线性代数库是不成熟的。我必须了解这些库是如何工作的，这样我才能在不同的库中进行选择，避免数字舍入陷阱。但是随着数值线性代数库的成熟，这变得不那么重要了。

深度学习仍然是一项新兴技术，所以当你训练一个神经网络，优化算法难以收敛时，理解梯度下降、动量和 Adam 优化算法背后的数学将有助于你做出更好的决策。类似地，如果你的神经网络做了一些有趣的事情 —— 比如说，它对某个分辨率的图像做出了糟糕的预测，但对其他分辨率的图像却没有 —— 理解神经网络架构背后的数学可以让你更好地找出该做什么。

当然，我也鼓励好奇心驱动的学习。如果某样东西让你感兴趣，那就去学习它，不管它有多有用！也许这会带来创造性的火花或技术突破。