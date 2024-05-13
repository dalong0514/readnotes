## 0801. Computers That Learn and Adapt

The computer programs I have so far described operate according to fixed rules supplied by the programmer. They have no way of inventing new rules themselves, or of improving the ones they are given. The chess-playing programs, if their programmers do not tinker with them, will keep making the same mistakes over and over, no matter how many games of chess they play. In this sense, computers are completely predictable; it is in this sense that computers can「do only what they are programmed to do」 — a point often raised by the defenders of humankind in the「man vs. machine」debate.

But not all software is this inflexible. It is possible to write programs that improve with experience. When they operate with such programs, computers can learn from their mistakes and correct their own errors. They accomplish this by making use of feedback. Any system based on feedback needs three kinds of information:

1 What is the desired state (the goal )?

2 What is the difference between the current state and the desired state (the error )?

3 What actions will reduce the difference between the current state and the goal state (the response ).

The feedback system adjusts the response, according to the error, to achieve the goal. The simplest and most familiar examples of feedback systems are not learning systems but control systems; the household thermostat is a good example. This feedback system recognizes only two possible errors and produces only two possible responses. The goal is to maintain a particular temperature, and the possible errors are that the temperature is either too hot or too cold. The responses are predetermined: if the temperature is too cold, the response is to turn on the furnace; if the temperature is too hot, the response is to turn the furnace off. Since the thermostat can only turn the furnace on or off, the response has nothing to do with the magnitude of the error. (This is a fact that I have repeatedly tried to explain to various members of my household, who insist on turning the thermostat all the way up to 90 degrees whenever the house is too cold, in hopes that somehow things will warm up faster; this tactic does not help. The thermostat can only turn the furnace on; it cannot turn it up.)

In principle, however, there is no reason why a home heating thermostat could not respond in proportion to the error. Such a system would require a method of adjusting the output of the furnace, rather than just turning it on or off. The apparatus would doubtless be more complicated and expensive, but it would ensure that the temperature was more precisely maintained. Such proportional control thermostats are used today in systems that control delicate industrial processes. Some household appliances — certain models of Japanese washing machines, for example — also use proportional control (or an approximation of it), a feature often advertised as fuzzy logic.

Another example of a system that uses proportional control is the automatic-pilot system that guides an airplane. The goal in this case is to keep the plane pointed in a given direction. A direction finder, such as a compass, measures the error in the direction the plane is traveling. The autopilot responds by making an adjustment in the position of the rudder of the plane in proportion to the size and direction of the error. Thus a slight deviation in course will result in only a slight change in the rudder position, but a major deviation, such as the swerving produced by a shift in the wind, will result in a large change in the setting of the rudder. If the automatic pilot system did not use proportional control but instead pushed the rudder all the way to the left or all the way to the right in the fashion of the home thermostat, the airplane would oscillate back and forth in an uncomfortable and probably dangerous manner.

In all of these feedback systems, the connection between error and response is fixed. The sensitivity of the response is predetermined by the design of the control system. But it is also possible to design an even more flexible feedback system, in which the response of the system adapts with time. In this case, the parameters of an initial feedback system are adjusted by a second feedback system. If the second feedback system adapts and improves over time, the system can be said to have「learned」the parameters of control.

Consider, for example, how a human pilot learns to fly an airplane. Typically, the student pilot oversteers at first — that is, overcorrects for every error. The pilot is using something like the system the thermostat uses to control the heat: if the plane is too far to the left, turn right; if it is too far to the right, turn left. Since there is a delay between turning the control rudder and the response of the plane, the system begins to oscillate. The pilot needs to learn how to move the rudder in proportion to the error, and this requires gauging the sensitivity of the response. The pilot learns this parameter through another feedback system; in this case, the goal of the feedback is to keep the plane on the correct course without oscillations, and the error is the degree of oscillation. The response is to adjust the response of the primary feedback system — that is, to adjust the amount that the control rudder is moved in order to correct a given erroneous angle in the plane's heading. Whenever the pilot's first feedback system is oscillating, he reduces its responsiveness. He increases its responsiveness if the plane begins to drift off course. Once the pilot learns the correct sensitivity, he can keep the plane on course without any oscillation.

It would be possible to build an automatic pilot that uses a second feedback system to adjust its own parameters, as described here. In this case, the autopilot could be said to have「learned」to fly the plane, in the same way that the human pilot learns. As far as I know, such adaptive autopilot systems are not used in real airplanes, but if they were they would have certain advantages. If the airplane sustained damage that caused a change in the responsiveness of the plane, such as a partly broken rudder, the autopilot would be able to adapt to this new situation. It might even be able to adapt if the connections to the rudder's control motor were accidentally reversed, so that the signal that normally turns the airplane right instead turned it left. Like a human pilot, the autopilot would require a fair amount of time to adjust to such a radical change in circumstances.

0801 能自我学习和进化的计算机

然而，并非所有的程序都是一成不变的。我们可以编写出随着经验的积累而不断完善的程序。当计算机运行这样的程序时，它们能够从错误中积累经验，并纠正问题。计算机可以通过反馈系统来实现这一功能。任何基于反馈机制的系统都需要如下三类信息：

1、什么是理想的状态（目标）？

2、当前状态和理想状态之间有什么差异（误差）？

3、采取什么样的行动会减少当前状态和理想状态之间的差异（响应）？

反馈系统根据误差来调整响应动作，以实现目标。最简单和最常见的反馈系统不是学习系统，而是控制系统，典型的例子就是家用暖气系统中的恒温器。该反馈系统只能识别两种类型的误差，以及采取两种类型的响应动作。该系统的目标是维持特定的室内温度，两种可能的误差分别是室温太高和室温太低。响应动作是预先确定的，即如果温度太低，启动电热装置；如果温度太高，则关闭电热装置。由于恒温器只能开启或者关闭电热装置，因此响应动作与误差的大小无关。我曾多次向我的家人解释这一事实。当房间里的温度变得很低时，他们坚持将恒温器调到最大值，希望让屋内更快暖和起来。然而，这个办法并不起作用，因为恒温器只能开启电热装置，并不能提高其温度。

然而，从原理上来说，家用暖气系统中的恒温器并不是不能按照误差比例来调节输出。若想实现这一点，系统还要能调节电热装置的输出大小，而不是只能开启或者关闭电热装置。这种装置无疑会变得更加复杂和昂贵，不过，它能够更加精准地控制室温。如今这种比例控制恒温器已用于控制复杂的工业过程系统。一些家用电器也采用了比例控制或者与之类似的方法，例如某些型号的日本洗衣机，这种特性通常被称为模糊逻辑（fuzzy logic）。

使用比例控制系统的另一个例子是飞机的自动驾驶系统，例如，我们的目标是让飞机保持固定的飞行方向。测向仪（例如罗盘）会测量飞机飞行方向的误差。自动驾驶仪会通过调整飞机的方向舵来做出响应，其大小和方向与误差的大小和方向成正比。因此，轻微的方向误差只会使方向舵发生轻微的变动，而巨大的方向误差会使方向舵发生较大的变动，例如，风向突然转变所导致的飞机大幅度转向。如果自动驾驶系统没有采用比例控制，而是和家用取暖系统中的恒温器一样，只能使方向舵左移或右移，那么飞机就会剧烈摇晃，而且也非常危险。

在上述的所有反馈系统中，误差和响应动作之间的关系是固定的。控制系统预先设定了响应的灵敏度。不过，也可以设计出一种更灵活的反馈系统，其响应动作可以随着时间的变化而变化。在这种情况下，第一个反馈系统的参数可以由第二个反馈系统来调整。如果第二个反馈系统随着时间的不断变化而改进，那么该系统便「学会」了控制参数。

我们以人类飞行员学习驾驶飞机的过程为例。在通常情况下，飞行员最初都会过度转向，也就是说，对每个误差都会矫枉过正。此时飞行员使用的策略和恒温器的控温系统类似：如果飞机向左偏得太远，则向右转；如果飞机向右偏得太远，就向左转。由于飞机转向舵的转向和飞机方向的改变之间存在时间上的延迟，因此系统开始左右摇晃。飞行员需要学习如何根据误差的大小按比例来改变方向舵，这需要估计方向舵的响应灵敏度。飞行员可以通过另一个反馈系统来掌握该灵敏度的参数。在这个反馈系统中，反馈的目标是让飞机保持正确的航向且不出现摇晃，系统和误差是摇晃的程度，系统的响应动作是调整第一个反馈系统的响应动作，也就是说，调整方向舵以纠正飞机航向偏离角所导致的位移量。当飞行员的第一个反馈系统开始摇晃时，第二个反馈系统就会减少响应输出；当飞机开始偏离航向时，就会增加响应输出。一旦飞行员适应了飞机的灵敏度，他就能让飞机在不出现任何摇晃的情况下保持正确航向。

综上所述，我们可以制造出利用第二个反馈系统来调整其自身参数的自动驾驶仪。在这种情况下，我们可以说这个自动驾驶仪「学会」了驾驶飞机，其学习方式与人类飞行员的学习方式一样。据我所知，真实的飞机上并没有使用这种自适应性自动驾驶系统。不过，如果它们能得到应用，一定具有优势。如果飞机受到了损坏，并导致飞机的响应性能发生故障，比如飞机转向舵部分失效，那么自动驾驶仪便能够应对这种特殊情况。如果飞机转向舵的控制电机意外反转，导致让飞机右转的信号反而让飞机左转，那么自动驾驶仪也能够应对这种情况。和人类飞行员一样，自动驾驶仪需要相当长的时间来适应环境中出现的剧烈变化。

### 8.1 Tranining the Computer

This basic notion of feedback is central to all learning systems, although it often takes a more complicated form than the self-adjusting automatic pilot. Often, feedback in computer programs is provided by training with the help of examples. The trainer (usually a human being) plays the role of a teacher, and the program becomes a student. A classical example of a trained learning system is a program written by the AI pioneer Patrick Winston, which learns the definition of concepts like「arch」from a series of positive and negative examples provided by an instructor. Winston's program learns new concepts by looking at simple line drawings of piles of blocks. The program is able to analyze such drawings and generate symbolic descriptions of the piles of blocks: for example,「Two touching cubes, supporting a wedge.」The trainer shows the program some examples of block configurations that form arches and another set of examples that do not, telling the program which are examples of「arch」and which are not. Initially, the program has no definition for the concept of「arch,」but as it is shown these positive and negative examples, it begins to formulate a working definition. Each time the program is shown a new example, it tests its working definition against the new example. If the definition sufficiently describes a positive example, or rules out a negative example, the program does not modify the definition. If the definition is in error, it is modified to fit the example.

Here is a scenario of how the program learns the definition of「arch」from a few examples. Assume that the first example the program is shown is a positive example: example A in Figure 25 , two upright rectangular blocks supporting a triangle. To start, the program will have to make an initial guess at formulating the definition of an arch. This initial guess does not need to be accurate, because it will be refined by future examples. Let's assume that the program uses the shapes of the blocks as its initial guess at a definition:「An arch is two rectangular blocks and a triangular block.」The second example the program is shown might be the same blocks, all lying down (example C in Figure 25 ). This is a negative example — that is, an example of something that is not an arch. Since the program's initial working definition mistakenly identifies this negative example as an arch, it will modify its definition to exclude the example. The program does this by identifying differences between the definition and the example and using them to add restrictions to the definition. In this case, the difference is in the relationships of the blocks, so an improved definition will include these relationships:「An arch is two upright rectangular blocks supporting a triangular block.」Now let's say the trainer supplies another positive example (B in Figure 25 ). This example uses a rectangular block at the top, instead of a triangular one. Since the program's working definition is not broad enough to include this positive example, the program will generalize its definition of「arch」to allow other shapes.

FIGURE 25 Positive and negative examples of arches

After being shown these examples and a few others, the program will converge on the following definition of an arch:「A prismatic body supported by two upright blocks that do not touch one another.」Each element of the definition has been learned by making some kind of mistake, and the definition has been adjusted accordingly. Once the program converges on the right definition, it stops making mistakes and leaves its definition unchanged. It can then correctly identify as an arch any arch it is shown, even if it has never seen that particular set of blocks before. It has learned the concept of「arch.」

训练计算机

反馈这一基本概念对所有学习系统来说都至关重要，尽管它通常比具备自动调整能力的自动驾驶系统更加复杂。通常来说，计算机程序中的反馈作用是通过不断训练样本而获得的。训练员（通常是人）扮演着教师的角色，程序则是学生。人工智能领域的先驱帕特里克·温斯顿（Patrick Winston）曾经编写过一个程序，它能从训练员提供的一系列正样本和负样本中学习「拱门」等概念，该程序是训练学习系统的经典案例。温斯顿设计的程序通过观察一组用简单的线条画成的块来学习新概念。该程序能够分析这些线条画的特点，并生成这些块的符号化描述。例如，「两个互相接触的立方体支撑着一个楔形体」。训练员会向程序展示一些构成拱门结构的模型示例，以及其他无法构成拱门结构的模型示例，以此告知程序哪些结构是「拱门」，哪些结构不是。最初，程序并没有关于「拱门」的定义，但当它看过这些正样本和负样本之后，便会开始形成有效的定义。每当给程序展示一个新样本时，它都会用这个定义来审核该样本。如果这个定义能准确地描述正样本或者排除负样本，那么程序就无须修改这个定义。如果这个定义出了错，就需要修改以匹配新样本。

下面这个例子说明了程序是如何从几个样本中学习「拱门」的定义的。假设展示给程序的第一个样本是一个正样本，即图 8-1 中的样本 A，其中，两个直立的长方体模块支撑着一个三角体模块。程序在形成拱门的定义时，首先需要做出一个初始猜测。这个初始猜测不必十分准确，因为它会根据未来的样本进行修改。假设程序将模块形状作为它对定义的初始猜测：拱门是两个长方体模块和一个三角体模块。假设展示给程序的第二个样本由相同的模块组成，但它们都倒在地面上，即图 8-1 中的样本 C，那么这便是一个负样本，也就是说，该样本不是一个拱门。然而，程序的初始定义却错误地将这个负样本识别为拱门，因此它需要改进定义，以将此样本排除在外。程序还可以识别出定义和样本之间的差异，并将此差异作为新的限制条件加入定义中。在这个例子中，两者之间的差异在于模块之间的位置关系，所以修正后的定义将包含这种关系：拱门是两个直立的长方体模块，上面支撑着一个三角体模块。假设现在训练员提供了另一个正样本，即图 8-1 中的样本 B。在这个样本中，顶部的模块为长方体模块，而非三角体模块。由于程序中的定义范围不够广泛，没有包含这个正样本，所以程序需要扩展其「拱门」的定义范围以涵盖其他形状。

广泛，没有包含这个正样本，所以程序需要扩展其「拱门」的定义范围以涵盖其他形状。

图 8-1 拱门的正样本和负样本

在给程序展示了各种样本之后，它会对拱门形成这样的定义：由两个互不接触的、直立的长方体支撑着一个棱形体。程序从错误中学习定义每个要素，并根据错误调整定义内容。一旦程序得到了正确的定义，它就不会再犯错误，定义也不会再有变动。此时，即使程序之前从未见过某个模块集，它也能够准确地识别出所有展示给它的拱门，因为它已经掌握了「拱门」的概念。

### 8.2 Neural Networks

Winston's program learns the concept of「arch,」but concepts like「touching,」「triangular block,」and「support」have been built into it from the beginning. Its representation of the world is specifically designed for piles of blocks. The search for a more general, universal representation scheme has led many researchers to computing systems with structures analogous to connected nets of biological neurons, such as occur in the brain. Such a system is called an artificial neural network.

A neural network is a simulated network of artificial neurons. This simulation may be performed on any kind of computer, but because the artificial neurons can operate concurrently, a parallel computer is the most natural place to execute it. Each artificial neuron has one output and a large number of inputs, perhaps hundreds or thousands. In the most common type of neural network, the signals between the neurons are binary — that is, either 1 or 0. The output of one neuron can be connected to the inputs of many others. Each input has a number associated with it, called its weight , which determines how much of an effect the input has upon the neuron's single output. This weight can be any number, positive or negative. The neuron's output is thus determined by a vote of the signals coming into its inputs, adjusted by the weights of the inputs. The neuron computes its output by multiplying each input signal by the input weight and summing the results; in other words, it adds up the weight of all the inputs that receive a 1 signal. If the weighted sum reaches a specific threshold, the output is 1; otherwise, the output is 0.

The function of an artificial neuron corresponds, very roughly, to the function of some types of real neurons in the brain. Real neurons also have one output and many inputs, and the input connections, called synapses , have different strengths (corresponding to the different input weights). A signal can either enhance or inhibit the firing of the neuron (corresponding to positive and negative weights), and the neuron will fire when the combined stimulation of the inputs is equal to or above some threshold. These are the senses in which an artificial neuron is analogous to a real one. There are also many ways in which a real neuron is much more complicated than an artificial one, but this simple artificial neuron is sufficient for building a system capable of learning.

The first thing to notice about artificial neurons is that they can be used to carry out the And, Or , and Invert operations. A neuron implements the Or function if the threshold is 1 and each of the input weights is equal to or greater than 1. A neuron with a threshold equal to the sum of the weights will implement the And function. Neurons with a single, negatively weighted input and a threshold of 0 will implement the Invert function. Since any logical function can be constructed by combining the And, Or , and Invert functions, a network of neurons can implement any Boolean function. Artificial neurons are universal building blocks.

We don't know very much about how the human brain works, but in some parts of the brain it seems that new information is learned by modifying the strength of the synapses that connect the neurons. This is certainly the case in the lower organisms on which we perform experiments — for example, sea snails. Sea snails can be taught certain conditioned responses, and it can be shown that they learn the response by changing the strength of the synaptic connections between neurons. Assuming that human learning works the same way, you are (I hope) adjusting the connections in your brain as you read this book.

A network of artificial neurons can「learn」by changing the weights of its connections. A good example is a very simple type of neural network called a perceptron , which can learn to recognize patterns. The way perceptrons learn is indicative of how most neural networks operate. A perceptron is a network with two layers of neurons and a single output. Each input in the first layer is connected to a sensing device like a light detector, which measures the brightness of one spot on an image. Each input of the second layer is connected to an output from the first layer, as shown in Figure 26.

Imagine that we are trying to teach the perception to recognize the letter A, which we will accomplish by showing it a large number of positive and negative examples of an A. The goal is for the perceptron to adjust the weights of the second layer so that its output will be 1 if, and only if, it is shown the image of an A. It accomplishes this by adjusting those weights whenever it makes an error. Each neuron in the first layer of the perceptron looks at a small patch of whatever example is being presented. Each of these first-layer neurons is programmed to recognize a specific local feature, such as a particular corner or a line at a particular orientation; it does so by means of the fixed weights of its own inputs. For example, here is a pattern of negative and positive input weights for the receptive field of a first-layer neuron programmed to recognize a corner, such as the point at the top of a capital A:

The first layer of the perception contains thousands of such feature-detecting neurons, each one programmed to recognize a particular kind of local feature in a particular part of the receptive field. This first layer of neurons detects features in the image which are useful for distinguishing between any letters; serifs are easy to detect, so they make letters more recognizable to the perceptron, just as they make a particular letter easier for the human eye to identify.

FIGURE 26

Perceptron

The local-feature detectors in the first layer provide the evidence, and the weights of the second layer determine how to weigh this evidence. For example, a corner pointing upward in the upper part of the image is evidence in favor of an A, while a corner pointing downward in the middle is evidence against. The perceptron learns by adjusting the weights on the inputs to the second layer. The learning algorithm is very simple: whenever the trainer indicates that the perceptron has made a mistake, the perceptron will adjust all of the weights of all the inputs that voted in favor of the mistake in such a way as to make future mistakes less likely. For instance, if the perceptron incorrectly identifies an image as an A, the weights of all the inputs that voted in favor of the false conclusion will be decreased. If the perceptron fails to identify a real A, then the inputs that voted in favor of the A will be increased. If the perceptron has enough feature detectors of the right type, this training method will eventually cause the perceptron to learn to recognize A's.

The learning procedure of the perceptron is another example of feedback. The goal is to set the weights correctly, the errors are misidentifications of the training examples, and the response is to adjust the weights. Notice that perceptrons, like Winston's arch program, learn only by making mistakes. This is a characteristic of all feedback-based learning systems. Given enough training, this particular procedure will always converge upon a correct choice of weights, assuming that there is a set of weights that does the job. This makes the perceptron seem like the perfect pattern-recognition machine, but the catch is the assumption that there exists some correct pattern of weights that will accomplish the task. To recognize the letter A in various sizes, fonts, and positions, the perceptron needs a very rich set of feature detectors in the first layer.

FIGURE 27

Perceptron spiral

Perceptrons can learn to recognize any letter if they are given enough features to work with, but there are some types of patterns, more complex than letters, that cannot be recognized by summing together local features in any way. For example, simply by summing up the evidence of local patches, a perceptron cannot tell whether or not all the dark spots in an image are connected, because connectedness is a global property; no local feature, by itself, can serve as evidence for or against connectedness. Figure 27 , adapted from Marvin Minsky and Seymour Papert's book Perceptrons , demonstrates that connectedness cannot always be assessed just by looking at local features.

For these and other reasons, two-layer perceptrons are not the most practical neural networks for recognizing most types of patterns. More general neural networks, with more layers, are able to recognize more complicated patterns. Such networks use similar procedures for learning. Trained neural networks of this type are often used for tasks like image recognition and speech recognition — tasks that are difficult to specify by a fixed set of rules. For instance, the simple word-recognition systems that are built into many children's toys today are based on neural networks.

神经网络

温斯顿设计的程序掌握了「拱门」的概念，不过，这是建立在其他诸如「接触」「三角体模块」「支撑」等概念从一开始就已输入程序的基础之上。这种表示方式是专为各种形状的模块设计的。为了寻求更通用的表示方案，许多研究人员开始研究类似于生物神经元网络（比如大脑中的神经网络）的计算系统，这种系统被称为人工神经网络。

人工神经网络是由人工神经元组成的模拟网络。该模拟任务可在任何类型的计算机上完成。由于人工神经元能够并行工作，因此并行计算机是执行该模拟任务的最佳工具。每个人工神经元都有一个输出和多个输入，其输入数目达到数百或者数千个。在最常见的神经网络类型中，神经元之间的信号是二进制的，即 1 或 0。一个神经元的输出可以连接至许多神经元的输入。神经元的每个输入有一个与之关联的数，被称为权重，它决定了该输入对神经元输出的影响程度。这个权重可以是任意数，正数和负数皆可。因此，神经元的输出由进入输入端的所有信号共同决定。神经元通过将每个输入信号值乘以输入权重，然后对所有的结果求和，最终得出输出。换句话说，它将所有接收到信号 1 的输入的权重都相加。如果权重之和达到某个阈值，则输出为 1；否则，输出为 0。

粗略地来说，人工神经元的功能相当于大脑中某类真正的神经元的功能。真正的神经元也拥有一个输出和多个输入，输入的连接点称为突触，它们的连接强度各不相同（对应于不同的输入权重）。信号可以强化或者抑制神经元的放电行为（对应于正数权重和负数权重），当输入的累积刺激等于或者高于某个阈值时，神经元就会放电。人工神经元和真正的神经元在上述几个方面是类似的。当然，真正的神经元比人工神经元复杂得多，不过，这种简单的人工神经元已经足以构建一种能够自我学习的系统了。

需要注意的是，人工神经元能用于执行「与」「或」「非」等逻辑运算。如果阈值为 1 且输入权重都等于或者大于 1，则人工神经元可以实现逻辑「或」的功能。如果一个人工神经元的输入权重之和等于阈值，便可以实现逻辑「与」的功能。如果人工神经元只有一个输入的权重为负且阈值为 0，则可以实现逻辑「非」的功能。由于通过「与」「或」「非」三种逻辑功能的组合可以构造出所有逻辑功能，因此神经元网络可以实现所有的布尔功能。人工神经元是一种通用构件。

我们还不太了解大脑是如何工作的，不过，某部分大脑似乎可以通过修改连接神经元的突触的强度来学习新知识。我们在低等生物（比如海螺）身上做了实验，情况就是如此。通过训练，海螺可以形成某些条件反射，并且证明了：它们是通过改变神经元之间突触的连接强度来获取这些条件反射的。假设人类的学习方式与之相同，那么当你阅读这本书时，你正在调整大脑神经元之间的连接，至少我希望是这样。

人工神经网络可以通过改变其连接的权重来进行学习。感知系统便是一个很好的例子，它是一种十分简单的神经网络，可以学会识别模式。感知系统的学习方式代表了大多数人工神经网络的运作方式。感知系统是一种具有两层神经元和单个输出的神经网络。第一层神经元的每个输入会连接到某个传感器上，例如用于测量图像上某点亮度的光线检测器；第二层神经元的每个输入与第一层神经元的输出相连，如图 8-2 所示。

图 8-2 感知系统

若想让感知系统识别出字母 A，我们就会通过给它展示字母「A」的大量正样本和负样本来实现。我们的目标是让感知系统调整第二层神经网络的权重，使得当且仅当给它展示字母 A 的图像时，其输出为 1。实现此目标的方法是，在它每次犯错后不断调整这些权重。无论给它展示何种样本，感知器第一层中的每个神经元都只关注其中的一小块区域。通过事先的设计，第一层神经网络中的每个神经元都能识别一种特定的局部特征，例如特定的角度或者特定方向的线条。神经元是依靠其本身输入的固定权重来实现这一点的。例如，图 8-3 展示的图像为第一层网络中某个神经元的感受野对应的权重模式，该感受野可以识别尖角，比如位于大写字母 A 顶部的一点。

图 8-3 某个神经元感受野对应的权重模式

感知系统中的第一层神经网络包含了数千个这样的特征检测神经元，每个神经元都能用于识别感受野中特定区域内的特定局部特征。第一层神经元检测图像中的特征，这些特征可用于区分不同的字母。字体中的衬线体易于检测，能让感知系统更容易地识别出字母，就像它们能使特定字母更容易被人眼识别出来一样。

第一层神经元中的局部特征检测器提供证据，第二层神经元中的权重决定如何衡量这些证据。例如，图像上部指向上方的尖角是有利于识别字母 A 的证据，而图像中部指向下方的尖角则是不利证据。感知系统通过调整第二层输入的权重进行学习。学习算法十分简单：一旦训练员向感知系统指出出现的错误，它就会调整引发此次错误的所有输入的权重，以降低未来出现同样错误的可能性。例如，如果感知系统错误地将其他图像识别为 A，那么在输入中所有支持这一错误结论的输入权重都将减小；如果感知系统没能识别出真正的字母 A，那么在输入中所有支持字母 A 的输入权重将会增加。如果感知系统拥有足够多合适的特征检测器，那么这种训练方法最终会教会它如何识别出真正的字母 A。

感知系统的学习过程是反馈系统的一个例子，其目标是设定正确的权重，误差是对培训样本的错判，响应动作是不断地调整权重。需要注意的是，与温斯顿设计的「拱门」识别程序一样，感知系统只能通过犯错来学习。这是所有基于反馈的自学习系统的共同特点。假设预期的权重（利用该权重即可准确地完成任务）确实存在，那么只要给予足够的训练，这个反馈过程将始终收敛于正确的权重。虽然从这一点来看，感知系统似乎是一种完美的模式识别器，但关键的问题在于，这是建立在假设（存在一组正确的、能完成任务的权重）成功的基础之上的。为了识别出各种大小、字体和位置的字母 A，感知系统需要在第一层神经网络中安装大量特征检测器。

如果给予感知系统足够多的特征，它们就能够学会识别所有字母。不过，对于一些比字母更复杂的模式，感知系统无法以任何方式将局部特征综合起来识别它们。例如，如果只是简单地综合局部的斑点信息，那么感知系统便无法判断图像中的所有斑点是不是连通的，因为连通性是全局属性，局部特征不能作为支持或者不支持连通性的证据。图 8-4 截自马文·明斯基和西摩·佩伯特（Seymour Papert）的著作《感知系统》（Perceptrons），这本书指出，仅通过观察局部特征不能判断连通性。

图 8-4 螺线感知系统

出于各种原因，在识别大多数模式时，双层感知系统并不是最实用的神经网络。拥有更多层数的更通用的神经网络能够识别更复杂的模式。这类神经网络采用了类似的学习策略，它们通常用于诸如图像和语音识别之类的任务，这些任务难以通过一组固定的规则来描述。例如，许多儿童玩具中的简易词语识别系统就是建立在神经网络基础之上的。

### 8.3 Self-Organizing Systems

The disadvantage of a learning system based on positive and negative examples is that it requires a trainer to classify the examples. There is another type of neural network, which does not require a trainer — or, to put it another way, there are networks in which the training signals are generated by the network itself. Such a self-training network is a self-organizing system. Self-organizing systems have been studied for years (Alan Turing published important work in this area), but there has been a recent renewal of research activity in such systems, and even some new progress, partly because of the availability of faster computers. Like trained neural networks, self-organizing systems are a natural fit for parallel computers.

As an example of a self-organizing system that works, consider the problem of transmitting an image from the eye to the brain (see Figure 28 ). The retina, on which the image is projected, is a two-dimensional sheet of light-sensitive neurons. The image on the retina is transformed into a similar projected image in the brain by a bundle of neurons that transfers the image. If this bundle is wired imperfectly, then the projected image will be slightly scrambled, with each pixel in slightly the wrong place. I will describe a self-organizing artificial neural network that can learn to unscramble such a picture, restoring each pixel to its proper position. The unscrambler consists of a single layer of neurons arranged in a two-dimensional array. The outputs of these neurons form the corrected image. If the picture is scrambled only slightly, then each pixel in the scrambled image will be in the general neighborhood of its correct position. Each neuron's inputs look at a neighborhood of pixels in the scrambled image, and the neuron learns which of these pixels should be connected to the output in order to produce the unscrambled image. The neuron forms the connection by setting the weight of the correct input to 1 and the weight of its other inputs to 0.

FIGURE 28 Eye, with scrambled nerve bundle and unscrambler

The training algorithm for the unscrambler is based on the fact that images have a nonrandom structure. As discussed earlier, real images are not just random arrays of dots but pictures of the world, so nearby areas of the image tend to look the same. The unscrambler turns this statement around, by assuming that pixels that tend to look the same ought therefore to be near one another. The neurons in the unscrambler work by measuring the correlation of each of their inputs with the outputs of the neighboring neurons during exposure to a series of images. Whenever a neuron makes an「error」by firing differently from its neighbors, the neuron increases the weight of the inputs that match the outputs of its neighbors and decreases the weights of the other inputs. Of course, its neighbors are also learning their connections at the same time, so in the beginning it is a case of (so to speak) the blind leading the blind, but eventually some of the unscrambler neurons begin locking onto their correct inputs and thus become effective trainers for their neighbors. Again, the only neurons that are adjusted are those that have made mistakes. As the neurons train one another, an unscrambled image begins to emerge in the outputs, and eventually the network organizes itself to produce an image of perfect clarity.

The self-adjusting autopilot, Patrick Winston's arch program, the perception, and the unscrambler are just a few examples of systems that learn. All these systems are based on either external or internal feedbacks, and all learn by correcting their mistakes. The design of each of these systems was inspired by a biological system of similar function. In harvesting these products of evolution, we are like the fool in Aesop's fable,「The Goose That Laid the Golden Egg,」who chooses the eggs instead of the goose. In the next chapter, we shall discuss the goose.

自组织系统

基于正样本和负样本的学习系统有一个缺点，即它需要训练员对这些样本进行分类。不过，存在一种不需要训练员的神经网络，这类网络可以自己生成训练信号。这种可以自动训练的神经网络是一种自组织系统。关于自组织系统的研究已经持续多年了，艾伦·图灵就在该领域取得过重要成果。最近，这个系统又出现了新的研究动向，并取得了一些进展，部分原因在于计算机的运行速度更快了。和神经网络一样，自组织系统非常适合并行计算机。

将图像从眼睛传输至大脑的过程是有效自组织系统的一个很好的例子（见图 8-5）。首先，图像被投影到视网膜上，视网膜是一张由感光神经元组成的薄膜。然后，视网膜上的图像被一束可以传递图像的神经元传导至大脑，产生一个相同的投射映象。如果这束神经元的连接存在问题，那么投影图像就会出现一些扭曲，即每个像素点都位于错误的位置。有一种自组织神经网络可以学会复原图像，将每个像素点复原至正确的位置。该复原系统由以二维阵列形式排列的单层神经元组成，这些神经元的输出形成了校正后的图像。如果图像的扭曲程度比较轻微，那么扭曲的图像中的像素点就位于正确的位置附近。每个神经元的输入会关注扭曲图像中的某个局部区域内的像素点，并学习应该将哪些像素点连接至输出以复原图像。神经元将正确输入的权重设置为 1，将其他输入的权重设置为 0，从而形成上述连接关系。

图 8-5 眼睛、偏离的视神经束以及复原系统

复原系统的训练算法基于如下事实：图像的结构是非随机的。如前所述，真实的图像并不是由像素点组成的随机阵列，而是物理世界的图景。因此，图像中的局部区域看起来是相同的。复原系统会反过来利用该结论，它假设，看起来相同的像素点应该彼此接近。在处理一系列图像的过程中，复原系统中的神经元通过测量其输入与相邻神经元的输出的相关性来进行工作。每当某个神经元的输出与其相邻神经元的输出有所不同时，即当它犯错时，这个神经元会增加与相邻神经元的输出相匹配的输入的权重，并降低其他输入的权重。当然，这个神经元的相邻神经元同时也在学习自己的连接关系。所以，开始阶段的情况就相当于盲人给盲人引路，但最终有一些神经元开始固定它们的正确输入，从而成为其相邻神经元的有效训练员。同样，唯一需要调整的神经元是那些犯错的神经元。当神经元彼此训练时，原始图像就开始出现在神经元的输出中，并且神经网络最后会进行自我组织，以生成一幅非常清晰的图像。

自动调整的自动驾驶仪、温斯顿设计的「拱门」识别程序、感知系统以及图像复原系统只是自我学习系统的其中几个例子。所有这些系统都是基于外部或者内部的反馈，并且可以通过纠正错误来不断学习。上述每个系统的设计都受到了具有类似功能的生物系统的启发。在收获这些科技发展成果时，我们就像伊索寓言《会下金蛋的鹅》中的傻瓜一样，选择了金蛋而非下金蛋的鹅。在下一章中，我们会讨论「鹅」的问题。