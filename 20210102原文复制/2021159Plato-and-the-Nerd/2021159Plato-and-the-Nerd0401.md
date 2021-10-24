## 0401 Hardware Is Ephemeral

· · · in which I show that hardware is soft, a transient expression of ideas, and those ideas are more durable than the hardware itself. And in which I trace the layered paradigms that make possible digital machines made with billions of transistors.

0401 硬件快速演化

在本章，我会说明硬件也是软的，以及一种比硬件本身生命力更持久的思想的短暂表达。同时，我在本章还追溯了使数十亿晶体管组成数字机器成为可能的分层范式。

### 4.1 Hard and Soft

Steven Connor, professor of modern literature and theory at Birkbeck, University of London, credits the French philosopher Michel Serres, now a Professor of French at Stanford, with developing a subtle and beautiful theory of「the hard and the soft.」Serres' thesis, according to Connor, is woven throughout his prolific writings, many of which have not been translated into English. Connor comments that it is difficult to quote Serres, so I will quote Connor instead:

[T]he contrast between the hard and the soft refers to this distinction between the domain of nature, the object of attention of what we call the「hard sciences,」and the domain of culture. The hard means the given, as opposed to the made. It means the physical, as opposed to the conceptual. It means hardware as opposed to software. It means object as opposed to idea, form as opposed to information, world as opposed to word. (Connor, 2009)

Connor finds allusions in Serres' writings to an astonishing array of oppositions between hard and soft, including body and language, science and humanities, things and signs, physical and conceptual, object and idea, form and information, physics and language, a stone and a ghost, motors and information theory, the manual and the digital, sound and meaning, bridge and hyphen, energy and information, flesh and word, the real and the virtual, forces and codes, solids and geometry, objective and subjective, war and religion, a book and a story, or sound and music.

But Serres does not succumb to Platonicity, requiring a sharp delineation between the hard and the soft. Quite the contrary. According to Connor,

Serres's principal effort is to allow his reader to grasp [the] intermixture [of the hard and the soft.] … The hard can always evaporate into the soft, the soft calcify into the hard. (Connor, 2009)

In Serres' own words (translated from the French by Connor),

Hard things display a soft side; material, of course, they engram and programme themselves like software. There is software [ logiciel ] in the hardware [ matériel ]. (Serres, 2003, p. 73)

We then find the more subtle oppositions between the hard and the soft, such as wax and wax, nature and nature, ropes and ropes, or mathematics and mathematics. Each of these, depending on its role and use, can be either hard or soft.「Hardness in softness and softness in hardness,」according to Serres.

Following Serres, the three-word summary of this chapter would need to be「hardware and hardware.」Hardware is both hard and soft. I will argue that for an engineer who works with digital technology, hardware is merely an ephemeral expression of an idea, lasting longer than a spoken word, which vanishes from the room in a few milliseconds, but still ephemeral, in the grand scheme. The ideas articulated by the hardware, in contrast, although undoubtably mutating and evolving, can last a long time indeed. These ideas are expressed using layers of paradigms that shape and constrain the ideas in ways that even the designer of the hardware is not aware of.

In the rest of this chapter, I outline the layers of modeling used specifically for computer hardware. With apologies to the reader, I confess that the rest of this chapter is a bit of a nerd storm. If you are an impatient reader, or you have no interest in hardware, and you are willing to grant my basic thesis, then please feel free to skip reading the rest of this chapter.

My basic thesis is that the hardware of modern computers is far too complex to design directly. Layers of abstraction are essential, and except for the bottom layer, semiconductor physics, none of these layers is given to us by nature. They are all human constructions, paradigms in Kuhn's sense that frame our thinking about hardware design.

Moreover, I claim that these paradigms, despite having no physical form, are more durable than the hardware. Paradigm shifts are difficult for humans. They can also be quite costly because changes in technology paradigms can mean significant retooling. Software that supports design, such as hardware description languages and their compilers, may have to be redesigned with significant paradigm shifts. Even manufacturing plants may have to change.

Nevertheless, the layering of paradigms makes paradigm shifts easier than they would otherwise be. The design of a microprocessor, for example, often does not need to change when moving to a new semiconductor technology. The emphasis of this chapter is on how this layering of paradigms enables creativity and technological advances. In chapter 6 , I will explain how technological advances trigger paradigm shifts.

If you persist in reading this chapter, my primary goal is to show a reader with little or no prior exposure to electronics how the basic operations of an application such as Wikipedia are realized by transistors operating as switches. This explanation cannot be given all at once. It has to be built up in layers. Otherwise, the complexity is simply too much for the human brain. But starting from an abstraction of a single transistor as a switch, we quickly get to abstractions that when realized in a chip require thousands, millions, and billions of transistors. My goal is to show how these layered abstractions enable such scaling up.

4.1 硬和软

史蒂文·康纳是伦敦大学伯克贝克学院现代文学和理论专业的教授，他认为斯坦福大学的法语教授、法国哲学家米歇尔·塞尔创立了一套精妙而漂亮的「硬和软」的理论。据康纳所说，塞尔的论题贯穿于他的多部作品之中，其中许多作品尚未被翻译成英文。康纳评论说，要引用塞尔的原文是有点儿难度的，所以我在这里就引用了康纳的一段文字：

「硬」和「软」的对比指的是自然领域和文化领域的区别，自然领域是我们所说的「硬科学」关注的对象。硬指的是给予的，而不是制造的。它指的是物质上的，而不是概念上的。它指的是硬件而不是软件。它指的是对象而不是想法，是形式而不是信息，是物理世界而不是文字。（康纳，2009）

康纳在塞尔的著作中发现了一系列令人吃惊的硬和软的经典对立情形，包括身体与语言、科学与人文、事物与符号、物理的与概念的、对象与想法、形式与信息、物理与语言、石头与鬼魂、发动机与信息论、手册与数字、声音与意义、桥梁与连字符、能量与信息、肉体与文字、真实与虚拟、力量与代码、立方体与几何学、客观与主观、战争与宗教、一本书与一个故事以及声音与音乐等等。

然而，塞尔并未屈从于柏拉图主义，那需要在硬和软之间有一个清晰的界限。恰恰相反，康纳表示：

塞尔的主要成就是，允许他的读者领悟（硬和软）是可以相互转换的…… 硬的总是能蒸发成软的，而软的也常常可以钙化为硬的。（康纳，2009 年）

塞尔在自己的著作中提道（康纳翻译自法语）：

硬的东西常常显示出软的一面；当然，材料本身就像软件一样可以被记忆和编程。硬件（法语 matériel）中有软件（法语 logiciel）。（塞尔，2003:73）

然后，我们又在硬和软之间发现了更为微妙的对立关系，例如，蜡和蜡、自然和自然、绳子和绳子，或者数学和数学。根据作用和用途的不同，上述例子中的每一方既可以是硬的，也可以是软的。按照塞尔的观点，「硬中有软，软中有硬」。

在塞尔的观点之后，我想简要地概括一下本章的内容 ——「硬件和硬件」，意思是硬件既是硬的也是软的。我要说的是，对于一个从事数字技术工作的工程师来说，硬件仅仅是一种思想的短暂表达，它的持续时间也许只稍稍长过一个几毫秒内就会从房间里消失的口语表达词语，但在宏大的计划中仍然是短暂的。相比之下，硬件所表达的思想，尽管总是处在不断的变化和演变之中，但确实可以持续很长的时间。这些思想是通过分层的范式来表达的。这些范式以设计者都不知道的方式形成和约束着这些思想。

在本章的其余部分，我将概要阐述专门用于计算机硬件的建模层。感到抱歉的是，我承认本章后续内容会像一场技术呆子的头脑风暴。如果你是个急性子或者对硬件不感兴趣，并且同意我的基本论点，那么请直接跳过这部分内容。

我的基本论点是，现代计算机的硬件过于复杂，根本无法直接进行设计。因此，抽象层是必不可少的，除了最低层的半导体物理层之外，所有其他的层都不是大自然赋予我们的。它们都是人类构建的，是库恩所指意义上构建我们对硬件设计的思路的范式。

此外，我还想表明，尽管这些范式没有物理形式，却比硬件本身的生命力更持久。范式的转换对人类来说是一件十分困难的事情。它们也可能会有很高的代价，因为技术范式的转换可能意味着重大的重组。用以支持设计的软件，例如硬件描述语言及其编译器，可能必须被重新设计并进行重大的范式转换，甚至就连制造工厂也可能不得不进行改变。

尽管如此，范式的分层使得范式的转换比其他情况下的转换要更容易。例如，微处理器的设计在转向一种新的半导体技术时，通常不需要进行改变。本章的重点在于这种范式的分层是如何激发创造力和推动技术进步的。在第 6 章，我将进一步解释技术进步是如何引发范式转换的。

如果你坚持阅读本章的内容，那么我可以先告诉你我的主要目标是，向那些很少或根本没有接触过电子技术的读者展示诸如维基百科这样的一个应用程序是如何以晶体管为开关实现基本操作的。关于这个过程的解释不可能一下子就给出来，它必须是分层的。否则，人类大脑就要应对过于复杂的事物了。但是，从把单个晶体管抽象为一个开关开始，我们很快就得到了在芯片中实现时需要的成千上万、数百万和数十亿个晶体管的抽象。我的目标是向读者展示这些分层的抽象是如何实现这种扩展的。

### 4.2 Semiconductors

Modern microprocessors are made from silicon crystals with carefully introduced impurities called dopants. The crystals are sculpted into tiny patterns and shapes like those shown in figure 3.1 in a「fab,」a facility where people in bunny suits shepherd silicon wafers through clean rooms, where even the tiniest speck of dust can ruin a chip. The output of a fab is a wafer like that shown in figure 3.2 , which is then cut up into individual dies that are inserted into a plastic or ceramic package with metal pins coming out.

When electrical voltages are applied to the chip through the metal pins, currents flow, and models such as Ohm's law, Faraday's law, and quite a few others can be used to understand what happens. A field-effect transistor (FET), for example, uses an electric field to vary the resistance of a「channel」in silicon. When the resistance is low, the transistor is「on.」When the resistance is high, the transistor is「off.」Because the material may or may not conduct electricity, it is neither an insulator nor a conductor, so it is called a「semiconductor.」

Figure 4.1 Mask design for a four-transistor CMOS NAND gate.

Ultimately, an electrical current is the movement of electrons, and voltages and electric fields arise from electrons piling up in or vacating a location. The behavior of a microprocessor, therefore, is at its root electrons sloshing around in silicon.

Semiconductor physics is a deeply technical specialization that is more science than engineering. In this specialization, the facts of the physical world dominate. Nevertheless, patterns of design have emerged, enabling designers to reuse patterns with rules of thumb to design useful electronic circuits without a deep understanding of the physics. These design patterns constitute a paradigm, and such a paradigm enables an industry to evolve beyond one-off science experiments in the lab.

A chip designer can, in principle, design structures like those in figure 3.1 by carefully specifying how to construct the structure. Such a design takes the form of a set of「masks」that are used in a lithographic process to「print」the chip. An example of a small portion of a mask is shown in figure 4.1 . This mask specifies which regions of the silicon crystal should be doped with which dopant, which regions should be covered with polycrystalline silicon, and which regions should be covered with metal. By the late 1970s, when it had become possible to put on the order of 20,000 transistors on a chip, it became impractical to manually design such masks for each circuit.

The layout in figure 4.1 specifies only four transistors. Figure 4.2 shows a die that contains four instances of a similar design to that shown in figure 4.1 . That chip has only 16 transistors. The large pads around the periphery of the chip are provided so that wires can be soldered to the chip and connected to metal pins on the exterior of the packaged chip, shown on the right in the figure.

In the late 1970s, Carver Mead of Caltech and Lynn Conway, 1 then at Xerox PARC, wrote a textbook called Introduction to VLSI System Design 2 that revolutionized the field by introducing the use of scalable「design rules.」Their approach is now universally called the Mead-Conway approach to circuit design.

The design rules define standard layout patterns according to a variable parameter called λ (the Greek letter lambda), which is the minimum distance between features in a layout. The 22-nm Intel process used to fabricate the Haswell chips shown in figure 3.2 , for example, has λ = 22 × 10 −9 meters. With these design rules, chip designers can reuse layouts over and over again, greatly simplifying the design process, even as the feature sizes in chips keep declining.

Figure 4.2

Die photo (left) and packaged product photo (right) of an NXP 74AHC00, which contains four 2-input CMOS NAND gates. [Die photo by Mikhail Svarichevsky of ZeptoBars, licensed under Creative Commons Attribution 3.0 Unported License.]

Mead and Conway triggered a paradigm shift, and as with most paradigm shifts, they met with some resistance. Diehard circuit designers insisted that they could design better chips without the constraints imposed by the Mead-Conway approach. They refused to accept this「freedom from choice.」Such designers have almost entirely vanished. Today, you may find them in corners of the industry designing specialized chips or performing research on fabrication technologies.

The use of design rules enables a separation between the chip designers and semiconductor physicists. The physicists can specify the design rules, and software can synthesize the masks. This separation also enabled new business models, where chips are fabricated by「silicon foundries,」companies such as TSMC (for Taiwan Semiconductor Manufacturing Company) or GLOBALFOUNDRIES, that just need to publish their design rules to their customers. Because of the Mead-Conway approach, system design companies can be「fabless,」not needing to invest the multiple billions of dollars that it takes to open a fab to make chips. Instead, they contract with the silicon foundries to make their chips.

4.2 半导体

现代微处理器是由硅晶体和被称为掺杂剂的杂质精心制成的。这些晶体被雕刻成微小的图案和形状，就像图 3.1 所示的「晶圆厂」中的产品。在晶圆厂，穿着连体防尘服的人们会在无尘室里制造硅晶片，这是因为哪怕是最小的灰尘都会毁掉一个芯片。晶圆厂的产品是图 3.2 所示的硅晶片，这些硅晶片被切割成单个的裸片，然后裸片被置入一个塑料或陶瓷的封装里，并将金属引脚从封装中引出。

当通过金属引脚向芯片施加电压时，就产生了电流。此时，我们就可以用欧姆定律、法拉第定律以及其他一些模型来理解发生了什么。例如，一个场效应晶体管是使用电场来改变硅片中「沟道」的阻值的。当电阻低时，晶体管就是「导通」的，而当电阻高时，晶体管就会「截止」。因为这种材料可以导电，也可以不导电，所以它既不是绝缘体也不是导电体，故而被称为「半导体」。

最终，电流是电子的运动，电压和电场是由电子聚集或空出一个区域产生的。可以说，微处理器的行为就是电子在硅材料中的流动。

半导体物理学是一门深奥的技术专业，它更多是科学而非工程。在这个专业化世界中，物理世界的事实占主导地位。尽管如此，各种设计模型层出不穷，这使得设计者能够重复使用经验法则来设计有用的电子电路，而无须深入了解这一物理学。这些设计模型构成了一个范式，而这种范式使一个行业的发展能够超越实验室中一次性的科学实验。

从原则上讲，芯片设计人员可以通过详细地说明如何构造一个结构来设计类似于图 3.1 所示的结构。这种设计采用了一套「掩膜」的形式，在光刻中其被用来「打印」芯片。例如，图 4.1 给出了某个掩膜设计的一部分。该掩膜说明了硅晶体的哪些区域应掺杂哪些掺杂剂，哪些区域应该覆盖多晶硅，以及哪些区域应该覆盖金属。到了 20 世纪 70 年代末，当一个芯片上放置 2 万个晶体管成为可能时，手工为每个电路设计这样的掩膜就变得非常不切实际了。

图 4.1 四晶体管的 CMOS 与非门掩膜设计及其逻辑符号。

图 4.1 所示的版图只给出了 4 个晶体管。图 4.2 给出了一个裸片，其包含 4 个类似于图 4.1 所示的设计实例。

那个芯片上只有 16 个晶体管。芯片的外围有一组较大的管脚，这使得可以将线路焊接到芯片上，并连接到封装芯片外部的金属引脚上。

20 世纪 70 年代末，加州理工学院的卡弗·米德和当时在施乐帕克研究中心工作的琳·康维共同编写了名为《超大规模集成电路导论》的教科书，这本书通过引入对可伸缩「设计规则」的使用在该领域掀起了一场革命。他们的方法现在被普遍称为米德 — 康维方法。

他们提出的设计规则是根据一个称作 λ（希腊字母 lambda）的变量参数来定义标准版图的模式。该参数是一个版图中特征图层之间的最小距离。例如，用于制造图 3.2 所示 Haswell 芯片的 22 纳米英特尔制程中，λ=22×10-9

米。有了这些设计规则之后，芯片设计者可以反复使用这些版图，即使是芯片的特征尺寸一直在减小。

米德和康维引发了一次范式转换。如同大多数范式转换的情形一样，他们也遇到一些阻力。一些固执的电路设计者坚持认为，他们可以设计出更好的芯片，而不受米德 — 康维方法的限制。他们拒绝接受这种「选择的自由」。当然，这样的设计师现在几乎已经完全消失了。今天，你也许会在行业的边缘部门发现他们的身影，在设计专门的芯片或者在从事制造技术的研究。

图 4.2 NXP 74AHC00 的裸片图（左边）和封装后的产品图（右边），该芯片有 4 个 2 路输入的 CMOS 与非门。（裸片图由 ZeptoBars 的米哈伊尔·斯瓦利切夫斯基提供，由知识共享署名许可 3.0 未移植版授权。）

设计规则的使用使芯片的设计者和半导体物理学家这两类人得以分离。物理学家可以制定设计规则，软件可以合成一组掩膜。这种职能上的分离也催生了新的商业模式。在这种模式下，芯片由「硅晶圆代工厂」制造，如台湾积体电路制造股份有限公司（台积电）或者格罗方德半导体股份有限公司等。这些公司只需要向它们的客户发布它们的设计规则就可以了。由于米德 — 康维方法的使用，系统设计公司可以「没有晶圆厂」，也不需要投资数十亿美元开设晶圆厂来生产芯片。相反，它们与硅晶圆代工厂签订合同，让这些工厂制造芯片。

### 4.3 Digital Switches

Although transistors can be used for other things (e.g., to amplify a signal), most of the transistors in a microprocessor are used as digital switches. This means that we can understand the behavior of a circuit by understanding whether the transistors are「on」or「off.」We don't really have to worry about the behaviors in between.

The following is a standard symbol used to represent a field-effect transistor (FET) like that in figure 3.1 :

The transistor has a control input wire (called the gate) that is used to turn the transistor on or off. Each transistor has two additional terminals (called the source and drain). When a transistor is「on,」we model its behavior as a simple wire connecting the source and the drain. When it is「off,」we model its behavior as disconnecting the same two terminals.

The voltage at the gate determines whether the transistor is on or off. For the above transistor, when the gate voltage is sufficiently higher than the source voltage, the transistor is on. Otherwise, it is off.

A「complementary」transistor can also be made, one that is turned on when the gate voltage is sufficiently lower than the source voltage. Such a transistor is shown with a circle at the gate:

A technology that combines these two types of transistors is called a CMOS technology, for complementary metal oxide semiconductor. The MOS part of this acronym is actually obsolete. It originates from the structure originally used to make these transistors, but the name persists nevertheless. CMOS has ceased to be an acronym in the culture of semiconductor technology. It is simply a noun, pronounced「sea moss.」

This switch model of a transistor is an approximation but a particularly useful one. It is a digital abstraction, cleanly separating exactly two states, on and off. The real transistor is not so clean: it is electrons sloshing around in silicon. Even good transistors fail to match the digital abstraction perfectly.

4.3 数字开关

虽然晶体管可以用于其他用途（例如放大信号），但微处理器中的大多数晶体管被用作数字开关。这意味着我们可以通过了解晶体管是「导通」还是「截止」来了解电路的行为。实际上，我们并不需要关心「中间的那些行为」。以下是用于表示图 3.1 所示场效应晶体管的标准符号：

晶体管有一根控制输入线（称为栅极），用于打开（导通）或关闭（截止）晶体管。每个晶体管还有其他两个端子（称为源极和漏极）。当晶体管「导通」时，我们将其行为建模为一根连接源极和漏极的简单导线。当它「截止」时，我们将其行为建模为断开的两个端子。

栅极上的电压决定了晶体管是导通还是截止的。对于上述晶体管来讲，当栅极电压比源极电压足够高时，晶体管就会导通。否则就是截止的。

我们还可以制造出一个「互补」的晶体管，当栅极电压比源极电压足够低时，晶体管就导通。该类晶体管的栅极处标有一个圆圈：

将这两种晶体管结合在一起的技术被称为 CMOS（互补金属氧化物半导体）技术。这个缩略词中的金属氧化物半导体（MOS）部分实际上已经过时了。它起源于最初用来制造这些晶体管的结构，但是这个名称现在仍然存在。CMOS 已不再是半导体技术文化中的缩略词了。它只是一个名词，发音为「sea moss」（海藻）。

晶体管的开关模型是一个近似模型，但是特别有用。它是一种数字式抽象，分为截然不同的两种状态 —— 导通和截止。但真正的晶体管并不那么清晰：它是在硅中流动的电子。即使再好的晶体管也无法完全匹配这个数字式的抽象。

### 4.4 Logic Gates

The digital switch model for a transistor provides a paradigm that we can use to build circuits that perform logic functions. Figure 4.3 shows a circuit diagram for an inverter , which converts a high voltage into a low one and, conversely, a low voltage into a high one. If a high voltage represents a digit 1 and a low voltage represents a digit 0, then an inverter converts 1 to 0 and 0 to 1. This is called a「logic gate」because it realizes a simple logical operation: negation.

Figure 4.3

Circuit diagram for an inverter logic gate (left). When the input voltage is high (3 volts), the lower transistor is on (center). When the input voltage is low (0 volts), the upper transistor is on (right).

The circuit is easy to understand even if you have never studied electrical circuits before. The two shaded boxes represent complementary FETs. The top transistor, the one with an extra circle, complements the lower one. In this circuit, the gates of the two transistors are connected together, so when one is off, the other is on.

The figure shows a voltage supplied to the terminal at the bottom of the figure of 0 volts. When the bottom transistor is on, the output will be connected to the 0 volt line, so the output voltage will be 0, as shown in the center diagram. The bottom transistor is on when the gate voltage is 3 volts. So if the input (the gate voltage) is 3 volts, then the output is 0 volts.

The voltage supplied to the top terminal is 3 volts. When the top transistor is on, this 3-volt line is directly connected to the output, so the voltage on the output will be 3 volts. This is illustrated at the right in the figure. The upper transistor is on when the input voltage is 0. So when the input is 0, the output is 3. Hence, the circuit indeed realizes an inverter, assuming that 3 volts represents the binary digit 1 and 0 volts represents the binary digit 0.

The transistor symbols in the diagram represent a simple model for some fairly complicated physics. The circuit is further abstracted to the logic symbol for an inverter:

This represents a digital「logic gate,」specifically an inverter. This abstraction has a particularly simple meaning. When the input is the binary digit 1, the output is the binary digit 0 and vice versa.

An inverter is also called a NOT gate because it can be viewed as realizing a logical negation. If the digit 1 represents「true」and the digit 0 represents「false,」then the NOT gate converts truth to falsehood and vice versa. When using such a symbol, we no longer explicitly show the supply voltages (connected to the top and bottom terminals). Those are implied.

The connection between switching circuits and logic was apparently first made fully by Claude Shannon, an electrical engineer who will appear again in chapter 7 as the father of information theory. In 1940, Shannon was a 22-year-old master's student at MIT. He wrote a master's thesis that may well be the most influential master's thesis ever written (Shannon, 1940). In his thesis, he showed that electrical switches could be interconnected in a variety of ways to realize any symbolic logic function. For example, one could express with electrical switches a statement such as,「 x is true if y is true and z is false or if y is false and z is true.」Shannon showed that such logic statements could be designed, analyzed, and optimized using an algebra for logic that had been developed in the previous century by the English mathematician George Boole. Ever since, such circuits have been referred to as Boolean logic circuits. When Shannon was working on his master's thesis, electrical switches were realized using either mechanical relays or vacuum tubes. The transistor hadn't been discovered yet, and although it had already been invented in the 1920s (see chapter 1 ), it was not widely known or used.

There are a few other useful Boolean logic gates. For example, an AND gate may have two inputs and one output. An AND gate is represented with this symbol:

When both inputs are 1, the output is 1. Otherwise, the output is 0. A NAND gate is equivalent to an AND gate followed by a NOT. It has the following symbol:

An implementation of a NAND gate is shown in figure 4.4 ; if you now understand how the inverter in figure 4.3 works, then you can probably figure out how the NAND gate works. Shannon designed similar gates using mechanical relays as switches.

An OR gate produces output 1 if any input is 1, rather than if all inputs are 1, as in an AND gate. An XOR (exclusive OR) gate with two inputs produces 1 if exactly one of the inputs is 1 and the other is 0. In other words, XOR determines whether the inputs differ. I will spare you the implementations of these and even their symbols.

Figure 4.4

Circuit diagram for a NAND logic gate and its logic symbol. When both inputs A and B are high, the output is low. Otherwise, the output is high.

So far, we have three levels of abstraction toward our goal of a Wikipedia system: We have the physical object out of which we will build the system, transistors such as those in figure 3.1 , with design rules that free us from having to give detailed geometries for each device; circuit diagrams as in figure 4.3 that abstract transistors as switches; and gates like that at the right in figure 4.3 that abstract the circuit as a logic function. Each of these layers has its own paradigm, with its own lexicon and symbology. But we are still nowhere near being able to build Wikipedia. Let's keep going. I promise we will get there!

4.4 逻辑门

晶体管的数字开关模型提供了一个范式。我们可以用它来构建执行逻辑功能的电路。图 4.3 给出了反相器的电路图，它将高电压转换为低电压，或者相反。如果高电压表示数字 1 且低电压表示数字 0，那么，反相器就在 0 和 1 之间进行转换。这被称为「逻辑门」，因为它实现了一个简单的逻辑操作：否定。

图 4.3 一个反相器逻辑门的电路图（左图）。当输入为高电压（3 伏特）时，底部的晶体管导通（中间图）。当输入为低电压（0 伏特）时，顶部的晶体管导通（右图）。

即使你以前从未研究过电路，也能够很容易理解这个电路。两个阴影框表示两个互补的场效应晶体管。顶部多出一个圆圈的晶体管补充下部的晶体管。在这个电路中，两个晶体管的栅极连接在一起，所以当一个截止时，另一个就是导通的。

由图可知，其底部端子的供电电压为 0 伏特。当底部的晶体管导通时，输出将连接到 0 伏特线路上，如中间的图所示，那么输出电压为 0 伏特。当栅极电压为 3 伏特时，底部晶体管将导通。所以，如果输入电压（栅极电压）为 3 伏特，那么输出电压为 0 伏特。

图中，顶部终端的供电电压为 3 伏特。当顶部晶体管导通时，这条 3 伏特的线路会直接连接到输出端，此时，输出端的电压为 3 伏特，如图中的右图所示。当输入电压为 0 伏特时，上面的晶体管导通。当输入电压为 0 伏特时，输出电压为 3 伏特。因此，这个电路确实实现了一个反相器的作用，这里假设 3 伏特代表二进制数字 1，0 伏特代表二进制数字 0。

上图中的晶体管符号代表了一些相当复杂的物理对象的简单模型。该电路可以进一步抽象为一个反相器的逻辑符号，如下：

这个符号代表了一个数字式的「逻辑门」，具体来说就是一个反相器。这个抽象表达了一个特别简单的含义 —— 当输入为二进制数 1 时，输出为二进制数 0，反之亦然。

反相器也被称为非门，因为它可以被看作实现了逻辑否定。如果数字 1 表示「真」，数字 0 表示「假」，那么非门会将真转换为假，反之亦然。当使用这样的符号时，我们将不再明确地给出供电电压（指连接到顶部和底部端子）。这些都是隐含的。

开关电路和逻辑间的联系显然是由克劳德·香农首先完全建立起来的。香农是一位电气工程师，他将以信息论之父出现在第 7 章。1938 年，22 岁的香农是麻省理工学院一名硕士生。他写的一篇硕士论文，很可能是有史以来最有影响力的硕士论文（香农，1938）。在这篇论文中，他给出了电子开关可以通过多种方式的连接来实现任何符号逻辑功能的结论。例如，人们可以用电子开关表示这样的命题，「如果 y

为真且 z

为假，或者，如果 y

为假且 z

为真，则 x

为真」。香农表明，这种逻辑命题可以用英国数学家乔治·布尔在 19 世纪创建的逻辑代数来设计、分析和优化。从那时起，这种电路就被称为布尔逻辑电路了。香农在撰写他的硕士论文时，电子开关是用机械继电器或真空管来实现的，晶体管在那时还没有被发现。尽管晶体管 20 世纪 20 年代就被发明了（见第 1 章），但它并没有被人们广泛地认识或使用。

另外，还有一些其他有用的布尔逻辑门。例如，一个与门可能有两个输入和一个输出。与门以如下的这个符号表示：

当两个输入都是 1 时，输出为 1；否则，输出为 0。一个与非门相当于一个与门的后面跟着一个「非」门。它的表示符号如下：

图 4.4 给出了与非门的一个实现。如果你现在已经了解了图 4.3 中反相器的工作原理，你可能就可以理解与非门是如何工作的了。香农使用机械继电器作为开关设计了类似的门。

如果任何一个输入为 1，则或门的输出为 1，其不像与门那样是要所有的输入都为 1。有两个输入的异或门的输出为 1 时，如果其中的一个输入为 1，那么另一个输入为 0。换句话说，异或门可以确定输入是否不同。这里，我就不再额外列举它们的实现及符号了。

图 4.4 与非门及其逻辑符号的电路图。当两个输入 A 和 B 都为高电压时，输出为低电压，否则输出为高电压。

到目前为止，我们对我们目标的维基百科系统有了三个抽象层次：我们有待构建系统的物理对象，如图 3.1 中所示的那些晶体管，设计规则使我们不必为每个设备提供详细的几何参数；图 4.3 所示的电路图，将晶体管抽象成开关；一些逻辑门，与图 4.3 中右侧的类似，将一个电路抽象为一个逻辑函数。每一层都有自己的范式，有自己的词汇和符号。但是，我们距离建立维基百科系统还有很长的路要走。让我们继续，我保证我们一定会实现这个目标！

### 4.5 Logic Diagrams

Figure 4.5 shows a logic diagram with 67 logic gates (abstracting roughly 400 transistors that are needed to realize these gates). Some of the gates are inverters like the one in figure 4.3 , and the rest are other gates representing logical AND, OR, NAND, NOR, and XOR functions. You need not study this diagram, but rather let's use it to get a sense of this level of abstraction toward the design of Wikipedia.

This diagram specifies the design of an arithmetic logic unit (ALU), an important part of any microprocessor. The inputs to this ALU are four-bit binary numbers. They come into the ALU on lines labeled A 0 · · · A 3 and B 0 · · · B 3 at the top. Each input wire carries one bit. 3 There are various outputs at the bottom, including, for example, one output wire labeled A = B . This output tells us whether the two four-bit inputs are equal. Hence, one of the functions performed by an ALU is to compare two numbers for equality. This ALU can also add and subtract two binary numbers, among other functions. In his master's thesis, Shannon showed a simpler but similar adder circuit and showed that each output from such a circuit could be expressed using Boole's symbolic logic algebra.

Figure 4.5

Logic diagram for four-bit ALU (Arithmetic Logic Unit). [Image licensed under CC BY-SA 3.0 by Poil, via WikiMedia Commons. From https://commons.wikimedia.org/w/index.php?curid=168473 .]

In a Wikipedia search, each character that I type in a search box to look up a topic is represented by a number, typically an 8- or 16-bit number, not a 4-bit number, so we will need a bigger ALU. But the bigger ALU follows the same principles as this 4-bit ALU, and its logic diagram would be far more intimidating.

To find a page that satisfies my search, Wikipedia needs to compare numbers for equality. The search mechanism is more sophisticated than just comparing numbers, but without being able to compare numbers, it would not be possible to do the search. So we have the first real connection between the hardware and the application, albeit still a tenuous one. We still have a ways to go.

Notice that only by spanning the four levels of abstraction that we have looked at so far can we understand why the world of computers is so obsessed with binary numbers. The reason is simple. Transistors are either on or off. Two states, two numbers, 0 and 1, false and true. That's all we've got, so we have to work with it. There is no 2.

A typical microprocessor today has a much more complicated ALU than this. Today's microprocessors operate on 32- or 64-bit numbers, not 4-bit numbers, so the size of this circuit will be at least 16 times bigger, comprising perhaps 1,000 gates and 6,400 transistors instead of 67 and 400. Typically it is much larger than that, offering many more functions. Clearly a model like that in figure 4.5 becomes unwieldy. You are probably now quite grateful that I didn't show you the logic diagram for the ALU in the laptop computer that I'm using to write this book. It would look similar but with many more gates.

Note that when a logic diagram like that in figure 4.5 is first created by an engineer, although it is a model, no physical realization exists of which it is a model. This underscores the point made in chapter 2 that the model serves a different purpose than a typical scientific model. It can't be true that the value of the model lies in how well it matches the physical system that it models because that physical system does not yet exist. The value of the model does depend, however, on our ability to construct a physical system whose behavior will match the model. Indeed, the magic of digital technology is that we know how to construct circuits that can match the logic of the model figure 4.5 with almost perfect fidelity, performing the specified operations a billion times per second for years!

4.5 逻辑图

图 4.5 给出了一个有 67 个逻辑门的逻辑图（要实现这些逻辑门的功能大约需要 400 个晶体管）。其中一些逻辑门是图 4.3 所示的反相器，其余的是代表与、或、与非、或非和异或函数的逻辑门。读者并不需要花时间研究这个图，但是，我们可以利用它来了解维基百科设计中的抽象层次。

该图给定了算术逻辑单元的设计。如我们所知，算术逻辑单元是任何微处理器的重要组成部分。这个算术逻辑单元的输入是 4 位二进制数。它们进入顶部标记为 A

0…A

3 和 B

0…B

3 的输入线。每条输入线携带一个比特。底部有一些不同的输出，例如，有一根标记为 A=B

的输出线。这条输出线告诉我们这两个输入的 4 位数是否相等。因此，算术逻辑单元执行的功能之一是比较两个数是否相等。这个算术逻辑单元还有加减两个二进制数以及其他一些功能。在他的硕士论文中，香农展示了一种简单但相似的加法器电路，并指出，这样一个电路的每个输出都可以用布尔的符号逻辑代数来表示。

图 4.5 四位算术逻辑单元（ALU）的逻辑图。（该图为 CC BY-SA 3.0 授权图片，由帕奥通过维基共享资源网站发布。图片网址为 https://commons.wikimedia.org/w/index.php?curid=168473。）

在维基百科的搜索过程中，我在搜索框中输入的每个字符都用一个数字来表示，通常是 8 位或 16 位的数字，而不是 4 位的，所以我们需要一个更大的算术逻辑单元。但是，更大的算术逻辑单元遵循与这个 4 位的算术逻辑单元相同的原理，而且它的逻辑图一定会更令人生畏。

要找到一个能满足我搜索要求的页面，维基百科需要比较数字是否相等。搜索机制比只是数字的比较要复杂得多。但是，如果不能比较数字，就不可能进行搜索。因此，尽管这是一个脆弱的连接，但也是我们在硬件和应用程序之间第一次真正的连接。我们还有很长的路要走。

请注意，只有跨越截至目前我们所看到的 4 个抽象层，我们才能理解为什么计算机世界如此痴迷于二进制数。其实原因很简单，因为晶体管有两种状态，要么导通要么截止。两种状态对应两个数字 0 和 1，对应两个逻辑状态假和真。这是我们所拥有的，所以我们必须用它们去工作，而没有 2 这样的其他数字。

现在，一个典型的微处理器的算术逻辑单元要比这个结构复杂得多。今天的微处理器的操作系统是 32 位或 64 位数，而不是 4 位数，所以这个电路的规模至少要比上面的电路大 16 倍，包括大约 1 000 个逻辑门和 6 400 个晶体管，而不是 67 个逻辑门和 400 个晶体管。通常情况下，它的规模还要更大，并提供更多的功能。很显然，像图 4.5 那样的模型会变得非常难以处理。你现在也许会十分感激我，因为我没有给你展示我在写本书时所用笔记本电脑上的算术逻辑单元的逻辑图。它看起来可能与之前所给出的逻辑图很相似，但它有更多的逻辑门。

请注意，当工程师首先创建了一个图 4.5 所示的逻辑图时，尽管它是一个模型，但是它所建模的物理实现并不存在。这强调了第 2 章提出的观点 —— 该模型与典型的科学模型具有不同的目的。这个模型的价值不可能取决于它与它所建模的物理系统的匹配程度，因为那个物理系统还不存在。然而，这个模型的价值的确取决于我们构建一个行为与模型相匹配的物理系统的能力。事实上，数字技术的神奇之处就在于，我们知道如何构造出与图 4.5 所示模型几乎完全匹配的电路，并且让它在数年的时间里以每秒 10 亿次的速度执行指定的操作！

### 4.6 Digital Machines

The ALU of figure 4.5 is just one of many pieces of a microprocessor. If a 32-or 64-bit ALU by itself is too complex to represent with a logic diagram, then certainly a microprocessor will also be too complex. So how does an engineer design a microprocessor?

An ALU can be further abstracted into a single component, as it is in figure 4.6 . Near the middle of the diagram is a funny-shaped box labeled「ALU」(or more accurately, labeled「 」) that represents a 32- or 64-bit version of the logic diagram shown in figure 4.5 . The other boxes in the diagram similarly represent complex logic with many thousands or even millions of transistors. This diagram is easily readable to someone trained in the art of computer architecture. That person could tell you what each of the boxes does. I will not attempt to do that here, but instead I will try to explain the overall style of the diagram.

Figure 4.6 represents the heart of a microprocessor, its central processing unit (CPU). It shows, left to right, four stages of the execution of a sequence of instructions that comprise a computer program. At the very left, the components in the diagram fetch instructions from the「instruction memory,」where the program is stored (in the form of binary numbers). The decode stage immediately to the right uses logic gates to figure out how to control various parts of the CPU, including the ALU, so that it performs the function demanded by an instruction. For example, if an instruction wants to add two numbers, then the decoder will construct the control input for the ALU to perform addition. The third stage, labeled「execute,」uses the ALU to perform the function demanded by the program. The fourth stage, labeled「memory,」stores the result of the instruction in memory or uses the result of an instruction as an address for data to fetch from memory.

Figure 4.6

Digital machine model of the main pipeline of simple microprocessor (after Patterson and Hennessy, 1996).

Figure 4.6 is not a logic diagram. There are no logic gates. Each box represents a component that is realized with many logic gates. The「wires」in this diagram are not simple wires either. The two「wires」into the ALU, for example, represent not one wire, but 32- or 64 wires, depending on whether this is a 32- or 64-bit ALU.

A key idea in the design shown in figure 4.6 is the separation of a memory that stores the program from the logic circuits that execute the program. Earlier computers might have been programmed by actually rewiring the logic circuits, for example, using patch panels with cables and plugs. An architecture with a program memory separated from an ALU, almost universal in computers today, is called a von Neumann architecture, after the Hungarian-American mathematician and computer scientist John von Neumann. Von Neumann first described this style of architecture in an incomplete report titled First Draft of a Report on the EDVAC , dated June 30, 1945. Von Neumann had been working on the Manhattan Project, developing the mathematical models for atomic bombs, and was consulting with a project run by the University of Pennsylvania to design a computer called EDVAC (for Electronic Discrete Variable Automatic Computer). The EDVAC was made with vacuum tubes and used a binary (base 2) representation for numbers, unlike its predecessor the ENIAC, which used a decimal (base 10) representation. Although von Neumann is listed as the only author on the report, it appears that many others from Penn had contributed significantly to this design, so referring to this architecture as a von Neumann architecture may once again reflect our need for heroes more than it accurately represents history. 4

Today, digital designers often assemble designs using hardware components such as ALUs that are reasonably standardized. The ALU shown in figure 4.5 is in fact a standard design called a 74181. Dating back to the 1970s, a series of standard component designs were produced by various manufacturers as a series called the 7400 series, and the four-bit ALU in figure 4.5 was a member of that series. Today, semiconductor manufacturers and computer-aided design (CAD) software provide libraries of standard cells that designers can use to assemble designs. More complex cells are often called simply IP, for intellectual property, and are sold as commodities to designers to use as components in designs.

The tall grey boxes in figure 4.6 represent latches or registers . A latch is a circuit that, when triggered by the tick of clock, records its inputs. It then holds the input value at its output until the next tick of the clock. In the computer that I am using to write this book, the clock ticks 2.6 billion times per second. At this clock rate, the ALU is presented with an input that lasts only 1 / 2.6 × 10 9 seconds or about 1/3 of a nanosecond. In that 1/3 of a nanosecond, its gates determine the value of its output so that on the next tick of the clock, the result of the ALU computation can be recorded by the downstream latch.

This clocked style of design is known as synchronous digital logic . It is synchronous in that, conceptually, all the latches are clocked simultaneously. The synchronous digital logic paradigm abstracts away the propagation delays within and between logic gates. As long as the gates are fast enough to correctly perform their function within a clock period, 1/3 of a nanosecond, there is no need to worry about the exact time delay of each gate. The delay can be ignored. The paradigm of logic gates becomes a simple one: they perform their logic function instantaneously.

Figure 4.6 is clearly much more abstract than the logic diagram in figure 4.5 . Chip designers call this style of diagram a register transfer level (RTL) diagram. I will call it more simply a digital machine because it is a machine operating on words made up of bits. The diagram describes the structure of the microprocessor at the level of operations performed on 32- or 64-bit words and numbers that are exchanged between relatively complicated components. Today's CPUs are actually quite a lot more complex than the one shown in figure 4.6 . The Intel Haswell line of processors, for example, has up to 19 stages of latches rather than the four shown in figure 4.6 . Moreover, these CPUs get combined with complicated hierarchical memory systems. Then they get assembled into servers that contain several CPUs. Then those get assembled into data centers with many thousands of servers and elaborate networks. Only then do we have the hardware for a system such as Wikipedia.

We now have four levels of abstraction, but we still don't have a word processor, much less a system such as Wikipedia. All we have is the hardware . We still have to figure out how to tell the hardware what to do. At this point, we need to make a transition from the world of hardware to the world of software. There will be several more levels of abstraction on the software side. I will discuss those in the next chapter. Bear with me. We will get there.

Notice that all four levels of abstraction have existed essentially in their current form for decades. But it would be hard to find any physical piece of such hardware that is several decades old, except in a museum. The abstractions are more durable than the hardware.

The layering of the abstractions is essential to technological progress. When King, Bokor, and Hu introduced the FinFET in 2001, and when it went into production in 2014, the only effect on the other layers is that now they had more transistors to work with. No paradigm change was needed at the upper levels because a FinFET, like previous transistors, makes a pretty good switch. It's just smaller and faster, and it uses less power. This creates opportunities at the upper levels, and as I will explain in chapter 6 , these opportunities can in fact trigger a crisis that will result in a paradigm shift. But such a「crisis of opportunity」does not demand a change at the upper levels. It just enables one.

4.6 数字机器

图 4.5 所示的算术逻辑单元仅是微处理器众多部件中的一个。如果一个 32 位或 64 位算术逻辑单元本身太过复杂而无法用逻辑图表示，那么微处理器自然也会特别复杂。那么，工程师又是如何设计一个微处理器的呢？

我们可以将一个算术逻辑单元进一步抽象为如图 4.6 所示的单个组件。在图的中间靠右有一个形状比较奇怪的框，上面标有「ALU」（或者更准确地说，是标记为「ALU」的框），它代表着图 4.5 所示的逻辑图的 32 位或 64 位版本。类似地，图中的其他方框相应地表示包含了数千甚至数百万个晶体管的复杂逻辑。受过计算机架构艺术培训的人，很容易读懂这张图。这个人可以告诉你每个方框的功能。在这里，我不打算这样做，但我将尝试解释图的总体风格。

图 4.6 表示的是微处理器的心脏 ——CPU（中央处理单元）。它从左到右给出了构成计算机程序的指令序列的 4 个执行阶段。在最左侧，图中的组件从「指令存储器」中取指令（二进制数形式）。其右侧紧邻的译码阶段使用逻辑门来确定如何控制 CPU 的各个部分，包括算术逻辑单元，以便它执行指令所要求的功能。例如，如果一个指令想要对两个数字进行加法操作，那么译码器将构造控制输入以便执行加法操作。标记为「执行」的第三阶段使用算术逻辑单元来执行程序所要求的功能。第四阶段的标记为「访存」，该阶段将把指令的执行结果存储到存储器中，或者用指令的执行结果作为从存储器中读取数据的地址。

图 4.6 简单微处理器主流水线的数字机器模型（继帕特森和亨尼西之后，1996)。

图 4.6 并非一个逻辑图，里面没有逻辑门。每个方框代表一个用许多逻辑门实现的组件。图里面的「连线」也不是简单的线路。例如，接入算术逻辑单元的两根「连线」代表的并不是一条线路，而是代表了 32 条或 64 条线路，这取决于它是 32 位还是 64 位的算术逻辑单元。

图 4.6 所示设计的一个关键思想是，将存储程序的存储器与执行程序的逻辑电路分离开来。早期的计算机可能是通过对逻辑电路的重新布线来编程的，例如，使用带有电缆和插头的接线板。将程序存储器与算术逻辑单元分离的体系结构在今天的计算机中几乎普遍存在，这种结构被称为冯·诺依曼体系结构，以美籍匈牙利数学家和计算机科学家约翰·冯·诺依曼的名字命名。冯·诺依曼在一份题为「离散变量自动电子计算机（EDVAC）报告」（1945 年 6 月 30 日）的不完整初稿中第一次描述了这种系统结构的风格。冯·诺依曼一直致力于「曼哈顿计划」，并创建了原子弹的数学模型，还与宾夕法尼亚州立大学的一个项目开展合作，设计了一台名为 EDVAC 的计算机。EDVAC 是用真空管制成的，并使用二进制（以 2 为基数）表示数字，而它的前身电子数字积分计算机（ENIAC）使用十进制（以 10 为基数）表示。虽然冯·诺依曼是该报告的唯一作者，但似乎很多其他来自宾夕法尼亚州立大学的人员都对这个设计做出了重大贡献。因此，把该体系结构称为冯·诺依曼体系结构可能再次反映了我们对于英雄的需要，而并非它准确地代表了历史。今天，数字化的设计师通常使用相当标准化的硬件组件（如算术逻辑单元）来组装这些设计。图 4.5 所示的算术逻辑单元实际上就是一个被称为 74181 的标准设计。早在 20 世纪 70 年代，诸多的制造商就生产了被称为 7400 系列的标准组件。图 4.5 中的 4 位算术逻辑单元就是该系列中的一员。今天，半导体制造商和计算机辅助设计（CAD）软件提供了标准的元件库，设计师可以直接用它们组装设计。更复杂的元件通常被称为 IP 核，即知识产权核，常被作为商品出售给设计师，并被用作设计中的组件。

在图 4.6 中相对较高的灰色框代表锁存器或寄存器。锁存器是一种电路，当其被时钟触发时，就会记录它的输入。然后，它将把输入值保持在输出端，直到时钟的下一个嘀嗒到来。在我用来撰写这本书的计算机中，时钟每秒嘀嗒 26 亿次。在这样的时钟频率下，算术逻辑单元的输入仅持续 1/2.6×109

或大约 1/3 纳秒。在 1/3 纳秒的时间里，它的那些逻辑门会决定它的输出值，以便算术逻辑单元的计算结果可以在时钟的下一个嘀嗒被下游的锁存器记录下来。

这种计时式的设计被称为同步数字逻辑。这是同步的，因为从概念上来说，所有锁存器都是同步计时的。同步数字逻辑范式将逻辑门内部和逻辑门之间的传播延迟抽象出来。只要逻辑门的速度足够快，就能在 1/3 纳秒的时钟周期内正确地执行它们的功能，那么，没必要担心每个逻辑门的确切时间延迟。延迟可以被忽略。逻辑门的范式变得很简单：它们会立即执行它们的逻辑功能。

图 4.6 显然比图 4.5 中的逻辑图要更抽象。芯片设计者将这种样式的图称为寄存器传输级（RTL）图。我则简单地称它为数字机器，因为它是一台操作由比特组成的文字的机器。该图描述了微处理器在 32 位或 64 位文字和数字上执行操作的层次上的结构。这些文字和数字是在相对复杂的组件之间交换的。实际上，今天的 CPU 要比图 4.6 中所示的设计复杂得多。例如，英特尔 Haswell 系列处理器最多有 19 个锁存器阶段，而不是图 4.6 所示的 4 个阶段。此外，这些 CPU 与复杂的分层存储系统相结合，之后，它们被组装到包含多个 CPU 的服务器中。然后，这些服务器被部署到拥有数千个服务器和复杂网络的数据中心。只有这样，我们才能拥有像维基百科那样的复杂系统的硬件。

我们现在有 4 个抽象层次，但是我们仍然没有文字处理器，更不用说像维基百科那样的系统了。我们有的只是硬件，我们仍然需要弄清楚如何告诉硬件做什么。在这一点上，我们需要从硬件世界过渡到软件世界。在软件方面，还会有更多的抽象层次。我将在下一章讨论这些问题。请大家继续保持耐心，我们就要到达目的地了。

请注意，从本质上说，所有 4 个抽象层次都以其当前形式存在了几十年。但是，除非在博物馆里，否则读者很难找到几十年前的硬件实物。然而，抽象的生命力比硬件更持久。

这些抽象的分层对技术的进步至关重要。在当金智杰、博科尔和胡正明三位于 2001 年推出鳍式场效应晶体管，以及这种晶体管在 2014 年实际投入生产时，对其他层造成的唯一影响只是它们现在有了更多的晶体管可供使用。不需要改变上层的范式，因为一个鳍式场效应晶体管就像以前的晶体管一样也可作为一个相当好的开关，只是体积更小，速度更快，耗电也更少了。这为上面的那些层创造了机会。正如我将在第 6 章解释的，实际上，这些机会可以引发一场危机，并导致范式的转换。但这种「机会危机」并不要求上面的那些层做出改变，它只是激活了一个而已。

__________

1 To emphasize that paradigms are invented by humans, and sometimes interesting humans, I feel compelled to point out that before working at Xerox Parc, Lynn Conway had been fired by IBM in 1968 after announcing her intention to transition from a male to a female gender role. I cannot even begin to imagine the courage this must have required at that time. She has since become a vocal advocate for transgender rights.

2 The term Very Large Scale Integration (VLSI) started to come into use in the 1970s when chips began to have thousands of transistors. The term is still used for chips with billions of transistors.

3 Shannon credits John Tukey, a mathematician at Princeton and Bell Labs, for the word「bit,」a shortening of「binary digit」(Shannon, 1948).

4 For a wonderful chronicle of von Neumann's pioneering contributions to computation, see George Dyson's 2012 book, Turing's Cathedral (Dyson, 2012).
