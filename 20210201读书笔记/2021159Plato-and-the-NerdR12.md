## 记忆时间

## 目录

0401 Hardware Is Ephemeral

0501 Software Endures

0601 Evolution and Revolution

## 0401. Hardware Is Ephemeral

· · · in which I show that hardware is soft, a transient expression of ideas, and those ideas are more durable than the hardware itself. And in which I trace the layered paradigms that make possible digital machines made with billions of transistors.

0401 硬件快速演化

在本章，我会说明硬件也是软的，以及一种比硬件本身生命力更持久的思想的短暂表达。同时，我在本章还追溯了使数十亿晶体管组成数字机器成为可能的分层范式。

### 4.1 Hard and Soft

Steven Connor, professor of modern literature and theory at Birkbeck, University of London, credits the French philosopher Michel Serres, now a Professor of French at Stanford, with developing a subtle and beautiful theory of「the hard and the soft.」Serres' thesis, according to Connor, is woven throughout his prolific writings, many of which have not been translated into English. Connor comments that it is difficult to quote Serres, so I will quote Connor instead:

[T] he contrast between the hard and the soft refers to this distinction between the domain of nature, the object of attention of what we call the「hard sciences,」and the domain of culture. The hard means the given, as opposed to the made. It means the physical, as opposed to the conceptual. It means hardware as opposed to software. It means object as opposed to idea, form as opposed to information, world as opposed to word. (Connor, 2009)

Connor finds allusions in Serres' writings to an astonishing array of oppositions between hard and soft, including body and language, science and humanities, things and signs, physical and conceptual, object and idea, form and information, physics and language, a stone and a ghost, motors and information theory, the manual and the digital, sound and meaning, bridge and hyphen, energy and information, flesh and word, the real and the virtual, forces and codes, solids and geometry, objective and subjective, war and religion, a book and a story, or sound and music.

But Serres does not succumb to Platonicity, requiring a sharp delineation between the hard and the soft. Quite the contrary. According to Connor,

Serres's principal effort is to allow his reader to grasp [the] intermixture [of the hard and the soft.] … The hard can always evaporate into the soft, the soft calcify into the hard. (Connor, 2009)

In Serres' own words (translated from the French by Connor),

Hard things display a soft side; material, of course, they engram and programme themselves like software. There is software [logiciel] in the hardware [matériel]. (Serres, 2003, p. 73)

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

2『硬件既是硬的也是软的，做一张反常识卡片。（2021-10-24）』—— 已完成

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

In the late 1970s, Carver Mead of Caltech and Lynn Conway, [1] then at Xerox PARC, wrote a textbook called Introduction to VLSI System Design [2] that revolutionized the field by introducing the use of scalable「design rules.」Their approach is now universally called the Mead-Conway approach to circuit design.

The design rules define standard layout patterns according to a variable parameter called λ (the Greek letter lambda), which is the minimum distance between features in a layout. The 22-nm Intel process used to fabricate the Haswell chips shown in figure 3.2 , for example, has λ = 22 × 10 −9 meters. With these design rules, chip designers can reuse layouts over and over again, greatly simplifying the design process, even as the feature sizes in chips keep declining.

Figure 4.2 Die photo (left) and packaged product photo (right) of an NXP 74AHC00, which contains four 2-input CMOS NAND gates. [Die photo by Mikhail Svarichevsky of ZeptoBars, licensed under Creative Commons Attribution 3.0 Unported License.]

Mead and Conway triggered a paradigm shift, and as with most paradigm shifts, they met with some resistance. Diehard circuit designers insisted that they could design better chips without the constraints imposed by the Mead-Conway approach. They refused to accept this「freedom from choice.」Such designers have almost entirely vanished. Today, you may find them in corners of the industry designing specialized chips or performing research on fabrication technologies.

The use of design rules enables a separation between the chip designers and semiconductor physicists. The physicists can specify the design rules, and software can synthesize the masks. This separation also enabled new business models, where chips are fabricated by「silicon foundries,」companies such as TSMC (for Taiwan Semiconductor Manufacturing Company) or GLOBALFOUNDRIES, that just need to publish their design rules to their customers. Because of the Mead-Conway approach, system design companies can be「fabless,」not needing to invest the multiple billions of dollars that it takes to open a fab to make chips. Instead, they contract with the silicon foundries to make their chips.

[1] To emphasize that paradigms are invented by humans, and sometimes interesting humans, I feel compelled to point out that before working at Xerox Parc, Lynn Conway had been fired by IBM in 1968 after announcing her intention to transition from a male to a female gender role. I cannot even begin to imagine the courage this must have required at that time. She has since become a vocal advocate for transgender rights.

[2] The term Very Large Scale Integration (VLSI) started to come into use in the 1970s when chips began to have thousands of transistors. The term is still used for chips with billions of transistors.

4.2 半导体

现代微处理器是由硅晶体和被称为掺杂剂的杂质精心制成的。这些晶体被雕刻成微小的图案和形状，就像图 3.1 所示的「晶圆厂」中的产品。在晶圆厂，穿着连体防尘服的人们会在无尘室里制造硅晶片，这是因为哪怕是最小的灰尘都会毁掉一个芯片。晶圆厂的产品是图 3.2 所示的硅晶片，这些硅晶片被切割成单个的裸片，然后裸片被置入一个塑料或陶瓷的封装里，并将金属引脚从封装中引出。

当通过金属引脚向芯片施加电压时，就产生了电流。此时，我们就可以用欧姆定律、法拉第定律以及其他一些模型来理解发生了什么。例如，一个场效应晶体管是使用电场来改变硅片中「沟道」的阻值的。当电阻低时，晶体管就是「导通」的，而当电阻高时，晶体管就会「截止」。因为这种材料可以导电，也可以不导电，所以它既不是绝缘体也不是导电体，故而被称为「半导体」。

最终，电流是电子的运动，电压和电场是由电子聚集或空出一个区域产生的。可以说，微处理器的行为就是电子在硅材料中的流动。

半导体物理学是一门深奥的技术专业，它更多是科学而非工程。在这个专业化世界中，物理世界的事实占主导地位。尽管如此，各种设计模型层出不穷，这使得设计者能够重复使用经验法则来设计有用的电子电路，而无须深入了解这一物理学。这些设计模型构成了一个范式，而这种范式使一个行业的发展能够超越实验室中一次性的科学实验。

从原则上讲，芯片设计人员可以通过详细地说明如何构造一个结构来设计类似于图 3.1 所示的结构。这种设计采用了一套「掩膜」的形式，在光刻中其被用来「打印」芯片。例如，图 4.1 给出了某个掩膜设计的一部分。该掩膜说明了硅晶体的哪些区域应掺杂哪些掺杂剂，哪些区域应该覆盖多晶硅，以及哪些区域应该覆盖金属。到了 20 世纪 70 年代末，当一个芯片上放置 2 万个晶体管成为可能时，手工为每个电路设计这样的掩膜就变得非常不切实际了。

图 4.1 四晶体管的 CMOS 与非门掩膜设计及其逻辑符号。

图 4.1 所示的版图只给出了 4 个晶体管。图 4.2 给出了一个裸片，其包含 4 个类似于图 4.1 所示的设计实例。

那个芯片上只有 16 个晶体管。芯片的外围有一组较大的管脚，这使得可以将线路焊接到芯片上，并连接到封装芯片外部的金属引脚上。

20 世纪 70 年代末，加州理工学院的卡弗·米德和当时在施乐帕克研究中心工作的琳·康维共同编写了名为《超大规模集成电路导论》的教科书，这本书通过引入对可伸缩「设计规则」的使用在该领域掀起了一场革命。他们的方法现在被普遍称为米德-康维方法。

他们提出的设计规则是根据一个称作 λ（希腊字母 lambda）的变量参数来定义标准版图的模式。该参数是一个版图中特征图层之间的最小距离。例如，用于制造图 3.2 所示 Haswell 芯片的 22 纳米英特尔制程中，λ=22×10^-9 米。有了这些设计规则之后，芯片设计者可以反复使用这些版图，即使是芯片的特征尺寸一直在减小。

米德和康维引发了一次范式转换。如同大多数范式转换的情形一样，他们也遇到一些阻力。一些固执的电路设计者坚持认为，他们可以设计出更好的芯片，而不受米德-康维方法的限制。他们拒绝接受这种「选择的自由」。当然，这样的设计师现在几乎已经完全消失了。今天，你也许会在行业的边缘部门发现他们的身影，在设计专门的芯片或者在从事制造技术的研究。

图 4.2 NXP 74AHC00 的裸片图（左边）和封装后的产品图（右边），该芯片有 4 个 2 路输入的 CMOS 与非门。（裸片图由 ZeptoBars 的米哈伊尔·斯瓦利切夫斯基提供，由知识共享署名许可 3.0 未移植版授权。）

设计规则的使用使芯片的设计者和半导体物理学家这两类人得以分离。物理学家可以制定设计规则，软件可以合成一组掩膜。这种职能上的分离也催生了新的商业模式。在这种模式下，芯片由「硅晶圆代工厂」制造，如台湾积体电路制造股份有限公司（台积电）或者格罗方德半导体股份有限公司等。这些公司只需要向它们的客户发布它们的设计规则就可以了。由于米德-康维方法的使用，系统设计公司可以「没有晶圆厂」，也不需要投资数十亿美元开设晶圆厂来生产芯片。相反，它们与硅晶圆代工厂签订合同，让这些工厂制造芯片。

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

Figure 4.3 Circuit diagram for an inverter logic gate (left). When the input voltage is high (3 volts), the lower transistor is on (center). When the input voltage is low (0 volts), the upper transistor is on (right).

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

Figure 4.4 Circuit diagram for a NAND logic gate and its logic symbol. When both inputs A and B are high, the output is low. Otherwise, the output is high.

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

开关电路和逻辑间的联系显然是由克劳德·香农首先完全建立起来的。香农是一位电气工程师，他将以信息论之父出现在第 7 章。1938 年，22 岁的香农是麻省理工学院一名硕士生。他写的一篇硕士论文，很可能是有史以来最有影响力的硕士论文（香农，1938）。在这篇论文中，他给出了电子开关可以通过多种方式的连接来实现任何符号逻辑功能的结论。例如，人们可以用电子开关表示这样的命题，「如果 y 为真且 z 为假，或者，如果 y 为假且 z 为真，则 x 为真」。香农表明，这种逻辑命题可以用英国数学家乔治·布尔在 19 世纪创建的逻辑代数来设计、分析和优化。从那时起，这种电路就被称为布尔逻辑电路了。香农在撰写他的硕士论文时，电子开关是用机械继电器或真空管来实现的，晶体管在那时还没有被发现。尽管晶体管 20 世纪 20 年代就被发明了（见第 1 章），但它并没有被人们广泛地认识或使用。

另外，还有一些其他有用的布尔逻辑门。例如，一个与门可能有两个输入和一个输出。与门以如下的这个符号表示：

当两个输入都是 1 时，输出为 1；否则，输出为 0。一个与非门相当于一个与门的后面跟着一个「非」门。它的表示符号如下：

图 4.4 给出了与非门的一个实现。如果你现在已经了解了图 4.3 中反相器的工作原理，你可能就可以理解与非门是如何工作的了。香农使用机械继电器作为开关设计了类似的门。

如果任何一个输入为 1，则或门的输出为 1，其不像与门那样是要所有的输入都为 1。有两个输入的异或门的输出为 1 时，如果其中的一个输入为 1，那么另一个输入为 0。换句话说，异或门可以确定输入是否不同。这里，我就不再额外列举它们的实现及符号了。

图 4.4 与非门及其逻辑符号的电路图。当两个输入 A 和 B 都为高电压时，输出为低电压，否则输出为高电压。

到目前为止，我们对我们目标的维基百科系统有了三个抽象层次：1）我们有待构建系统的物理对象，如图 3.1 中所示的那些晶体管，设计规则使我们不必为每个设备提供详细的几何参数；2）图 4.3 所示的电路图，将晶体管抽象成开关；3）一些逻辑门，与图 4.3 中右侧的类似，将一个电路抽象为一个逻辑函数。每一层都有自己的范式，有自己的词汇和符号。但是，我们距离建立维基百科系统还有很长的路要走。让我们继续，我保证我们一定会实现这个目标！

### 4.5 Logic Diagrams

Figure 4.5 shows a logic diagram with 67 logic gates (abstracting roughly 400 transistors that are needed to realize these gates). Some of the gates are inverters like the one in figure 4.3 , and the rest are other gates representing logical AND, OR, NAND, NOR, and XOR functions. You need not study this diagram, but rather let's use it to get a sense of this level of abstraction toward the design of Wikipedia.

This diagram specifies the design of an arithmetic logic unit (ALU), an important part of any microprocessor. The inputs to this ALU are four-bit binary numbers. They come into the ALU on lines labeled A 0 · · · A 3 and B 0 · · · B 3 at the top. Each input wire carries one bit. [3] There are various outputs at the bottom, including, for example, one output wire labeled A = B . This output tells us whether the two four-bit inputs are equal. Hence, one of the functions performed by an ALU is to compare two numbers for equality. This ALU can also add and subtract two binary numbers, among other functions. In his master's thesis, Shannon showed a simpler but similar adder circuit and showed that each output from such a circuit could be expressed using Boole's symbolic logic algebra.

Figure 4.5 Logic diagram for four-bit ALU (Arithmetic Logic Unit). [Image licensed under CC BY-SA 3.0 by Poil, via WikiMedia Commons. From https://commons.wikimedia.org/w/index.php?curid=168473 .]

In a Wikipedia search, each character that I type in a search box to look up a topic is represented by a number, typically an 8- or 16-bit number, not a 4-bit number, so we will need a bigger ALU. But the bigger ALU follows the same principles as this 4-bit ALU, and its logic diagram would be far more intimidating.

To find a page that satisfies my search, Wikipedia needs to compare numbers for equality. The search mechanism is more sophisticated than just comparing numbers, but without being able to compare numbers, it would not be possible to do the search. So we have the first real connection between the hardware and the application, albeit still a tenuous one. We still have a ways to go.

Notice that only by spanning the four levels of abstraction that we have looked at so far can we understand why the world of computers is so obsessed with binary numbers. The reason is simple. Transistors are either on or off. Two states, two numbers, 0 and 1, false and true. That's all we've got, so we have to work with it. There is no 2.

A typical microprocessor today has a much more complicated ALU than this. Today's microprocessors operate on 32- or 64-bit numbers, not 4-bit numbers, so the size of this circuit will be at least 16 times bigger, comprising perhaps 1,000 gates and 6,400 transistors instead of 67 and 400. Typically it is much larger than that, offering many more functions. Clearly a model like that in figure 4.5 becomes unwieldy. You are probably now quite grateful that I didn't show you the logic diagram for the ALU in the laptop computer that I'm using to write this book. It would look similar but with many more gates.

Note that when a logic diagram like that in figure 4.5 is first created by an engineer, although it is a model, no physical realization exists of which it is a model. This underscores the point made in chapter 2 that the model serves a different purpose than a typical scientific model. It can't be true that the value of the model lies in how well it matches the physical system that it models because that physical system does not yet exist. The value of the model does depend, however, on our ability to construct a physical system whose behavior will match the model. Indeed, the magic of digital technology is that we know how to construct circuits that can match the logic of the model figure 4.5 with almost perfect fidelity, performing the specified operations a billion times per second for years!

3 Shannon credits John Tukey, a mathematician at Princeton and Bell Labs, for the word「bit,」a shortening of「binary digit」(Shannon, 1948).

4.5 逻辑图

图 4.5 给出了一个有 67 个逻辑门的逻辑图（要实现这些逻辑门的功能大约需要 400 个晶体管）。其中一些逻辑门是图 4.3 所示的反相器，其余的是代表与、或、与非、或非和异或函数的逻辑门。读者并不需要花时间研究这个图，但是，我们可以利用它来了解维基百科设计中的抽象层次。

该图给定了算术逻辑单元的设计。如我们所知，算术逻辑单元是任何微处理器的重要组成部分。这个算术逻辑单元的输入是 4 位二进制数。它们进入顶部标记为 A0…A3 和 B0…B3 的输入线。每条输入线携带一个比特。底部有一些不同的输出，例如，有一根标记为 A=B 的输出线。这条输出线告诉我们这两个输入的 4 位数是否相等。因此，算术逻辑单元执行的功能之一是比较两个数是否相等。这个算术逻辑单元还有加减两个二进制数以及其他一些功能。在他的硕士论文中，香农展示了一种简单但相似的加法器电路，并指出，这样一个电路的每个输出都可以用布尔的符号逻辑代数来表示。

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

Figure 4.6 Digital machine model of the main pipeline of simple microprocessor (after Patterson and Hennessy, 1996).

Figure 4.6 is not a logic diagram. There are no logic gates. Each box represents a component that is realized with many logic gates. The「wires」in this diagram are not simple wires either. The two「wires」into the ALU, for example, represent not one wire, but 32- or 64 wires, depending on whether this is a 32- or 64-bit ALU.

A key idea in the design shown in figure 4.6 is the separation of a memory that stores the program from the logic circuits that execute the program. Earlier computers might have been programmed by actually rewiring the logic circuits, for example, using patch panels with cables and plugs. An architecture with a program memory separated from an ALU, almost universal in computers today, is called a von Neumann architecture, after the Hungarian-American mathematician and computer scientist John von Neumann. Von Neumann first described this style of architecture in an incomplete report titled First Draft of a Report on the EDVAC , dated June 30, 1945. Von Neumann had been working on the Manhattan Project, developing the mathematical models for atomic bombs, and was consulting with a project run by the University of Pennsylvania to design a computer called EDVAC (for Electronic Discrete Variable Automatic Computer). The EDVAC was made with vacuum tubes and used a binary (base 2) representation for numbers, unlike its predecessor the ENIAC, which used a decimal (base 10) representation. Although von Neumann is listed as the only author on the report, it appears that many others from Penn had contributed significantly to this design, so referring to this architecture as a von Neumann architecture may once again reflect our need for heroes more than it accurately represents history. [4]

Today, digital designers often assemble designs using hardware components such as ALUs that are reasonably standardized. The ALU shown in figure 4.5 is in fact a standard design called a 74181. Dating back to the 1970s, a series of standard component designs were produced by various manufacturers as a series called the 7400 series, and the four-bit ALU in figure 4.5 was a member of that series. Today, semiconductor manufacturers and computer-aided design (CAD) software provide libraries of standard cells that designers can use to assemble designs. More complex cells are often called simply IP, for intellectual property, and are sold as commodities to designers to use as components in designs.

The tall grey boxes in figure 4.6 represent latches or registers . A latch is a circuit that, when triggered by the tick of clock, records its inputs. It then holds the input value at its output until the next tick of the clock. In the computer that I am using to write this book, the clock ticks 2.6 billion times per second. At this clock rate, the ALU is presented with an input that lasts only 1 / 2.6 × 10 9 seconds or about 1/3 of a nanosecond. In that 1/3 of a nanosecond, its gates determine the value of its output so that on the next tick of the clock, the result of the ALU computation can be recorded by the downstream latch.

This clocked style of design is known as synchronous digital logic . It is synchronous in that, conceptually, all the latches are clocked simultaneously. The synchronous digital logic paradigm abstracts away the propagation delays within and between logic gates. As long as the gates are fast enough to correctly perform their function within a clock period, 1/3 of a nanosecond, there is no need to worry about the exact time delay of each gate. The delay can be ignored. The paradigm of logic gates becomes a simple one: they perform their logic function instantaneously.

Figure 4.6 is clearly much more abstract than the logic diagram in figure 4.5 . Chip designers call this style of diagram a register transfer level (RTL) diagram. I will call it more simply a digital machine because it is a machine operating on words made up of bits. The diagram describes the structure of the microprocessor at the level of operations performed on 32- or 64-bit words and numbers that are exchanged between relatively complicated components. Today's CPUs are actually quite a lot more complex than the one shown in figure 4.6 . The Intel Haswell line of processors, for example, has up to 19 stages of latches rather than the four shown in figure 4.6 . Moreover, these CPUs get combined with complicated hierarchical memory systems. Then they get assembled into servers that contain several CPUs. Then those get assembled into data centers with many thousands of servers and elaborate networks. Only then do we have the hardware for a system such as Wikipedia.

We now have four levels of abstraction, but we still don't have a word processor, much less a system such as Wikipedia. All we have is the hardware . We still have to figure out how to tell the hardware what to do. At this point, we need to make a transition from the world of hardware to the world of software. There will be several more levels of abstraction on the software side. I will discuss those in the next chapter. Bear with me. We will get there.

Notice that all four levels of abstraction have existed essentially in their current form for decades. But it would be hard to find any physical piece of such hardware that is several decades old, except in a museum. The abstractions are more durable than the hardware.

The layering of the abstractions is essential to technological progress. When King, Bokor, and Hu introduced the FinFET in 2001, and when it went into production in 2014, the only effect on the other layers is that now they had more transistors to work with. No paradigm change was needed at the upper levels because a FinFET, like previous transistors, makes a pretty good switch. It's just smaller and faster, and it uses less power. This creates opportunities at the upper levels, and as I will explain in chapter 6 , these opportunities can in fact trigger a crisis that will result in a paradigm shift. But such a「crisis of opportunity」does not demand a change at the upper levels. It just enables one.

4 For a wonderful chronicle of von Neumann's pioneering contributions to computation, see George Dyson's 2012 book, Turing's Cathedral (Dyson, 2012).

4.6 数字机器

图 4.5 所示的算术逻辑单元仅是微处理器众多部件中的一个。如果一个 32 位或 64 位算术逻辑单元本身太过复杂而无法用逻辑图表示，那么微处理器自然也会特别复杂。那么，工程师又是如何设计一个微处理器的呢？

我们可以将一个算术逻辑单元进一步抽象为如图 4.6 所示的单个组件。在图的中间靠右有一个形状比较奇怪的框，上面标有「ALU」（或者更准确地说，是标记为「ALU」的框），它代表着图 4.5 所示的逻辑图的 32 位或 64 位版本。类似地，图中的其他方框相应地表示包含了数千甚至数百万个晶体管的复杂逻辑。受过计算机架构艺术培训的人，很容易读懂这张图。这个人可以告诉你每个方框的功能。在这里，我不打算这样做，但我将尝试解释图的总体风格。

图 4.6 表示的是微处理器的心脏 —— CPU（中央处理单元）。它从左到右给出了构成计算机程序的指令序列的 4 个执行阶段。在最左侧，图中的组件从「指令存储器」中取指令（二进制数形式）。其右侧紧邻的译码阶段使用逻辑门来确定如何控制 CPU 的各个部分，包括算术逻辑单元，以便它执行指令所要求的功能。例如，如果一个指令想要对两个数字进行加法操作，那么译码器将构造控制输入以便执行加法操作。标记为「执行」的第三阶段使用算术逻辑单元来执行程序所要求的功能。第四阶段的标记为「访存」，该阶段将把指令的执行结果存储到存储器中，或者用指令的执行结果作为从存储器中读取数据的地址。

图 4.6 简单微处理器主流水线的数字机器模型（继帕特森和亨尼西之后，1996)。

图 4.6 并非一个逻辑图，里面没有逻辑门。每个方框代表一个用许多逻辑门实现的组件。图里面的「连线」也不是简单的线路。例如，接入算术逻辑单元的两根「连线」代表的并不是一条线路，而是代表了 32 条或 64 条线路，这取决于它是 32 位还是 64 位的算术逻辑单元。

图 4.6 所示设计的一个关键思想是，将存储程序的存储器与执行程序的逻辑电路分离开来。早期的计算机可能是通过对逻辑电路的重新布线来编程的，例如，使用带有电缆和插头的接线板。将程序存储器与算术逻辑单元分离的体系结构在今天的计算机中几乎普遍存在，这种结构被称为冯·诺依曼体系结构，以美籍匈牙利数学家和计算机科学家约翰·冯·诺依曼的名字命名。

冯·诺依曼在一份题为「离散变量自动电子计算机（EDVAC）报告」（1945 年 6 月 30 日）的不完整初稿中第一次描述了这种系统结构的风格。冯·诺依曼一直致力于「曼哈顿计划」，并创建了原子弹的数学模型，还与宾夕法尼亚州立大学的一个项目开展合作，设计了一台名为 EDVAC 的计算机。EDVAC 是用真空管制成的，并使用二进制（以 2 为基数）表示数字，而它的前身电子数字积分计算机（ENIAC）使用十进制（以 10 为基数）表示。虽然冯·诺依曼是该报告的唯一作者，但似乎很多其他来自宾夕法尼亚州立大学的人员都对这个设计做出了重大贡献。因此，把该体系结构称为冯·诺依曼体系结构可能再次反映了我们对于英雄的需要，而并非它准确地代表了历史。

今天，数字化的设计师通常使用相当标准化的硬件组件（如算术逻辑单元）来组装这些设计。图 4.5 所示的算术逻辑单元实际上就是一个被称为 74181 的标准设计。早在 20 世纪 70 年代，诸多的制造商就生产了被称为 7400 系列的标准组件。图 4.5 中的 4 位算术逻辑单元就是该系列中的一员。今天，半导体制造商和计算机辅助设计（CAD）软件提供了标准的元件库，设计师可以直接用它们组装设计。更复杂的元件通常被称为 IP 核，即知识产权核，常被作为商品出售给设计师，并被用作设计中的组件。

在图 4.6 中相对较高的灰色框代表锁存器或寄存器。锁存器是一种电路，当其被时钟触发时，就会记录它的输入。然后，它将把输入值保持在输出端，直到时钟的下一个嘀嗒到来。在我用来撰写这本书的计算机中，时钟每秒嘀嗒 26 亿次。在这样的时钟频率下，算术逻辑单元的输入仅持续 1/2.6×10^9 或大约 1/3 纳秒。在 1/3 纳秒的时间里，它的那些逻辑门会决定它的输出值，以便算术逻辑单元的计算结果可以在时钟的下一个嘀嗒被下游的锁存器记录下来。

这种计时式的设计被称为同步数字逻辑。这是同步的，因为从概念上来说，所有锁存器都是同步计时的。同步数字逻辑范式将逻辑门内部和逻辑门之间的传播延迟抽象出来。只要逻辑门的速度足够快，就能在 1/3 纳秒的时钟周期内正确地执行它们的功能，那么，没必要担心每个逻辑门的确切时间延迟。延迟可以被忽略。逻辑门的范式变得很简单：它们会立即执行它们的逻辑功能。

图 4.6 显然比图 4.5 中的逻辑图要更抽象。芯片设计者将这种样式的图称为寄存器传输级（RTL）图。我则简单地称它为数字机器，因为它是一台操作由比特组成的文字的机器。该图描述了微处理器在 32 位或 64 位文字和数字上执行操作的层次上的结构。这些文字和数字是在相对复杂的组件之间交换的。实际上，今天的 CPU 要比图 4.6 中所示的设计复杂得多。例如，英特尔 Haswell 系列处理器最多有 19 个锁存器阶段，而不是图 4.6 所示的 4 个阶段。此外，这些 CPU 与复杂的分层存储系统相结合，之后，它们被组装到包含多个 CPU 的服务器中。然后，这些服务器被部署到拥有数千个服务器和复杂网络的数据中心。只有这样，我们才能拥有像维基百科那样的复杂系统的硬件。

我们现在有 4 个抽象层次，但是我们仍然没有文字处理器，更不用说像维基百科那样的系统了。我们有的只是硬件，我们仍然需要弄清楚如何告诉硬件做什么。在这一点上，我们需要从硬件世界过渡到软件世界。在软件方面，还会有更多的抽象层次。我将在下一章讨论这些问题。请大家继续保持耐心，我们就要到达目的地了。

请注意，从本质上说，所有 4 个抽象层次都以其当前形式存在了几十年。但是，除非在博物馆里，否则读者很难找到几十年前的硬件实物。然而，抽象的生命力比硬件更持久。

这些抽象的分层对技术的进步至关重要。在当金智杰、博科尔和胡正明三位于 2001 年推出鳍式场效应晶体管，以及这种晶体管在 2014 年实际投入生产时，对其他层造成的唯一影响只是它们现在有了更多的晶体管可供使用。不需要改变上层的范式，因为一个鳍式场效应晶体管就像以前的晶体管一样也可作为一个相当好的开关，只是体积更小，速度更快，耗电也更少了。这为上面的那些层创造了机会。正如我将在第 6 章解释的，实际上，这些机会可以引发一场危机，并导致范式的转换。但这种「机会危机」并不要求上面的那些层做出改变，它只是激活了一个而已。

## 0501. Software Endures

· · · in which I argue that the layers of paradigms for software are so deep that the physical world largely becomes irrelevant; that software reflects the personalities and idiosyncrasies of its creators; that software endures much better than hardware in no small part because it encodes its own layered paradigms; and that connected machines in server farms dream.

0501 软件的持久力

在这一章，我会讨论软件的范式层次如此之深，以至物理世界在很大程度上变得无关紧要了；软件反映了其创造者的个性和特质；软件在很大程度上要比硬件耐久，这是因为它编码了自己的分层范式；在服务器群组之梦中连接的机器。

### 5.1 Self-Scaffolding

In principle, engineers who wish to write programs could set individual bits in the program memory to get the hardware to do their bidding. In practice, this would be mind-numbingly tedious. A typical program might consist of, say, 10 million bits stored in program memory. That's a lot of zeros and ones. No human could write those zeros and ones without making many, many errors.

The bit patterns that constitute a program are called machine code . They are meant for the machine to read, not for the human designer to write. So how do they get written? How does a human designer build a program like a word processor or a system like Wikipedia? Here's where the next stack of abstractions comes into play, those focused on software.

A modern computer program will typically consist of hundreds or thousands of「modules」or「packages,」each of which consists of dozens or hundreds of「classes,」each of which has dozens or hundreds of「methods,」each of which has dozens or hundreds of lines of code. The lines of code are written in a programming language that is translated by a compiler into machine code (often indirectly, first translating into another language, then another language, then to machine code). These layers of design are essential to being able to form any sort of understanding of the behavior of the program.

Way back in 1972, Edsger Dijkstra, a Dutch computer scientist, then a mathematics professor at the Eindhoven University of Technology in The Netherlands, described software as a「hierarchical system,」which he defined by analogy, We understand walls in terms of bricks, bricks in terms of crystals, crystals in terms of molecules, etc. (Dijkstra, 1972)

He then observed that the number of levels in such hierarchical abstractions is small unless the「ratio between the largest and the smallest grain」is large. The number of molecules in a wall is very large, and yet Dijkstra gives us only four layers.

For the structure of programs, the ratio between a bit of machine code and a program may easily be in the millions. However, in addition, there is layering in the temporal behavior of a program. An individual line of code may execute in a few nanoseconds, whereas the overall function of the program may span hours, days, or months. Dijkstra comments on this ratio:

I do not know of any other technology covering a ratio of 10 10 or more: the computer, by virtue of its fantastic speed, seems to be the first to provide us with an environment where highly hierarchical artifacts are both possible and necessary. (Dijkstra, 1972)

To assess Dijkstra's「ratio between the largest and the smallest grain」for software, we need to combine three effects. A computer program may have a million lines of code and get translated into a few million bits of machine code. The machine code is executed on a chip that has billions of transistors, each acting as a switch. And these switches are switching billions of times per second. If the smallest grain is the switching of a transistor and the largest is the computer program, then the ratio is at least 10 24 or

1,000,000,000,000,000,000,000,000.

This number is large for something made by humans. Hence, by the time we get to software, we are quite distant from the physical world.

At this point, it ceases to be useful to think of software as a physical phenomenon. It is instead what Hal Abelson and Gerry Sussman call「procedural epistemology」in their introductory computer science book, Structure and Interpretation of Computer Programs (Abelson and Sussman, 1996). Software becomes an abstract medium for human creativity and craftsmanship and starts to more closely resemble Searle's cognitive phenomena than the physical phenomena out of which it originates. Software becomes a medium for human expression, not just technical, but also cultural, literary, and artistic. It is of course ultimately realized in the physical world by electrons sloshing around. In words that Connor calls「startlingly sacramental,」Serres invokes the Bible when talking about the coalescence of the soft model of software and hard matter that it runs on:

Et verbum caro factum est . (Serres, 2001, p. 78)

And the word was made flesh.

With such a huge difference in scale of the largest and smallest grain sizes, layers of modeling become essential. Unlike the scientific effort that Searle criticizes to explain preexisting sociological phenomena such as money in terms of neurophysiology, our enterprise here is engineering not science. We only need to explain the phenomena we construct, not ones given to us by nature. As humans, we construct software and all the layers below, down to the transistors. It is much easier to explain a phenomenon that we have constructed in terms of a lower level phenomenon that we have also constructed, particularly because the lower level phenomenon was constructed in part to support the upper level one.

Each layer of modeling is governed by a paradigm. A programming language, for example, is such a paradigm. It shapes the programmer's thinking and provides the framework for procedural epistemology. The programming language is a human invention and often reflects the creativity and idiosyncrasies of its inventors.

As a paradigm, a programming language has an interesting property. Specifically, the language can be used, and often is used, to encode its own paradigm. Specifically, a program is translated into a lower level language, such as machine code, by a compiler. Assuming that the machine code is well defined, the compiler encodes the meaning of the programming language and hence encodes its paradigm. But the compiler can usually be written in the very language that it compiles! In fact, it is a common litmus test for a language to be deemed worthy that it be able to encode its own compiler. According to Wikipedia, at least the following languages have compilers written in their own language: BASIC, ALGOL, C, D, Pascal, PL/I, Factor, Haskell, Modula-2, Oberon, OCaml, Common Lisp, Scheme, Go, Java, Rust, Python, Scala, Nim, and Eiffel.

This kind of self-scaffolding of paradigms, I believe, is unique to software among other technologies. It seems to approach Searle's description of sociological phenomena, where「the concept that names the phenomenon is itself a constituent of the phenomenon.」And it pervades software from the lowest to the highest layer. At the lowest layer, a microprocessor includes a「boot loader,」a tiny built-in program that is executed when the microprocessor is first powered up. The term「boot loader」is a reference to bootstrapping, a term that, according to Wikipedia,

· · · appears to have originated in the early 19th century United States (particularly in the phrase「pull oneself over a fence by one's bootstraps」), to mean an absurdly impossible action · · · [retrieved April 30, 2016]

At a much higher layer in software, I quoted earlier the Wikipedia page on Wikipedia, itself a form of self-scaffolding. At intermediate levels, to reboot an operating system, something all of us have done, is also a reference to bootstrapping. The operating system uses its own services to start the operating system itself.

In the rest of this chapter, I will explain a few of the layers of modeling that we commonly use in software technology. I hope these explanations will be somewhat less nerdy than the hardware layers of the previous chapter in part because they are more idiosyncratic. I will describe these layers not as facts about the world but as inventions by humans. But I again apologize in advance for the brief nerd storms that I have been unable to keep out of this book. As in the previous chapter, I will progress from lower layers to the upper ones.

5.1 自我支撑

编写程序的工程师原则上可以在程序存储器中设置单独的比特位，以使硬件能够执行他们的命令。在实践中，这是一件极其乏味的工作。一个典型的程序可能是程序存储器中的 1 000 万个比特位，那是很多很多的「0」和「1」。没有人能够在不犯很多很多错误的情况下写出这些「0」和「1」。

构成程序的比特模式被称为机器码。它们是供机器读取的，而不是让设计人员来编写的。那么它们又是怎么被编写出来的呢？设计人员是如何构建出一个文字处理器或维基百科这样的系统的？这就是下一组堆叠的抽象要发挥作用的地方了，它们聚焦于软件。

现代计算机程序通常由成百上千或成千上万个「模块」或「包」组成，其中每个「包」有数十或成百上千个「类」，每个「类」又有几十或成百上千个「方法」，而每个「方法」则有数十行或成百上千行代码。代码行是用某种编程语言编写的，并由编译器将其翻译成机器码（首先转换为另一种语言，然后再转换为机器码，这些转换通常是间接的）。设计中的这些层次对于能够从任何层理解程序的行为都是至关重要的。

早在 1972 年荷兰计算机科学家艾兹格·迪杰斯特拉在荷兰埃因霍芬理工大学任数学教授时，他就把软件描述为「分层系统」，并以下面的类比定义这个系统：

我们通过砖块来了解墙壁，通过晶体来了解砖块，通过分子来了解晶体。（迪杰斯特拉，1972）

然后，他注意到，除非「最大粒度与最小粒度之间的比率」较大，否则这种分层系统中的层数会很少。墙壁中的分子数量巨大，但是迪杰斯特拉只为我们给出了 4 个分层。

对于程序的结构而言，机器码的一个比特与一个程序之间的比率可能很容易就达到数百万。此外，程序的时间行为也是分层的。单行代码可以在几纳秒内完成执行，而程序的总体功能可能需要几个小时、几天或几个月。迪杰斯特拉对这一比率做了如下评论：

我不知道还有没有其他技术能具有 1010 或更大的比率：计算机以其惊人的速度，似乎是第一个为我们提供了一种环境，在这里高度分层的人工制品成为可能的和必要的。（迪杰斯特拉，1972）

为了评估迪杰斯特拉关于软件的「最大和最小粒度之间的比率」，我们需要综合考量三个因素。一个计算机程序可能包括 100 万行代码，并被翻译成几百万条机器码。机器码是在一个芯片上被执行的，该芯片上有数十亿个晶体管，每个晶体管充当一个开关。这些开关每秒切换数十亿次。如果最小粒度是晶体管的开关切换，最大的是计算机程序，那么它们之间的比率至少是 1024 或者下面这个数字：

1 000 000 000 000 000 000 000 000

这个数字对于人类制造的东西而言实在是太大了。因此，当我们开始接触软件的时候，我们实际上已经远离了物理世界。

此时，再把软件视为一种物理现象已经没用了。哈罗德·阿贝尔森和杰伊·萨斯曼在其计算机科学的入门书《计算机程序的构造和解释》中将软件称为「程序认识论」（阿贝尔森和萨斯曼，1996）。软件成为人类施展创造力和技能的一个抽象媒介，它更接近约翰·塞尔的认知现象，而不是作为其起源的物理现象。软件成为人类表达思想的媒介，不仅体现在技术上，还表现在文化、文学和艺术等方面。当然，它最终是通过物理世界的电子流动实现的。在康纳所说的「令人有些震惊的神圣感」中，当谈到软件的软模型和它所运行的硬物质的结合时，米歇尔·塞尔引用了《圣经》中的话：

道成了肉身。（米歇尔·塞尔，2001:78）

2『已下载书籍「2020167Structure-and-Interpretation-of-Computer-Programs」、「2020168Structure-and-Interpretation-of-Computer-Programs-JS」。（2021-10-25）』

由于最大和最小粒度在规模上的巨大差异，分层建模就变得至关重要了。我们致力于工程而不是科学，与塞尔批评的从神经生理学角度解释诸如金钱等先前存在的社会学现象的科学努力不同，我们在这里要关注的是工程而不是科学，我们只需要解释我们所构造的现象，而不是大自然赋予我们的那些现象。作为人类，我们构建软件及其下面的所有层，直到晶体管。用我们构造的一个较低层的现象来解释我们构造的现象要容易得多，特别是因为较低层的现象部分地是为了支持较高层的现象而构造的。

建模的每一层都会受到一个范式的支配。例如，编程语言就是这样一种范式。它塑造了程序员的思维，并为程序认识论提供了框架。编程语言是人类的发明，它通常反映了发明者的创造力和特质。

作为一种范式，编程语言具有一个有趣的特性。具体来说，编程语言可以而且经常被用来编码它自己的范式。例如，程序被编译器翻译成较低级别的语言，例如机器码。假设机器码是定义良好的，编译器就会对编程语言的含义进行编码，从而对其范式进行编码。但是编译器通常可以用它所编译的语言编写！事实上，一种语言能否对自己的编译器进行编码，是一种常见的试金石。根据维基百科，至少以下语言的编译器是用其本身编写的，包括 BASIC、ALGOL、C、D、Pascal、PL/I、Factor、Haskell、Modula-2、Oberon、OCaml、Common Lisp、Scheme、Go、Java、Rust、Python、Scala、Nim 以及 Eiffel。

我相信，这种范式的自我支撑是软件所特有的。这似乎接近塞尔对社会学现象的描述，「命名现象的概念本身就是现象的组成部分」。从最低层到最高层，软件都是如此。在最低层，微处理器包括了一个「引导加载程序」，这是一个很小的内置程序，该程序在微处理器第一次启动时被执行。「引导加载程序」一词指的是自引导（也称自举），在维基百科中有如下说明。

…… 这个词似乎起源于 19 世纪初的美国（特别是在「通过拽自己靴子上的鞋带，把自己提起来越过栅栏」这样的句子），指的是一个荒谬的不可能的行为……（2016 年 4 月 30 日检索）

站在软件的更高层次，我在前面引用了维基百科上的维基百科页面，它本身就是一种自我支撑的形式。在中间层次上，重新启动操作系统，这是我们所有人都做过的事情，也是指自引导。操作系统使用自己的服务启动操作系统本身。

在本章的其余部分，我将解释我们通常在软件技术中使用的建模层。我希望这些解释不会比前一章对硬件建模层的解释更乏味，部分原因是它们更为特殊。我不把这些层描述为关于世界的事实，而是把它们视为人类的发明。这部分也许还会涉及一些技术呆子式的头脑风暴。真是抱歉，为了让读者更好地理解这些内容，我不得不如此。和前一章一样，我将先从较低的层开始解释，逐步到更高的层次。

### 5.2 Instruction Set Architectures

Fred Brooks, working at IBM in the 1960s, is credited with developing the idea of an instruction set architecture (ISA), which abstracts what the hardware in a computer does. When a computer executes a program, it executes a sequence of instructions. An instruction may, for example, compare two numbers. Another instruction may specify which instruction to execute next based on the outcome of the comparison. The set of instructions that a computer can execute is called, not surprisingly, its「instruction set.」Before Brooks, every distinct model of computer had a different instruction set.

In the 1960s, IBM was developing a family of computers called the System/360 family. One of the goals of the System/360 project was to produce a diverse product line of computers that could all execute the same programs. That is, once you had a bit pattern to put into the instruction memory, that same bit pattern would work on an entry-level computer and on a more advanced, more expensive model. This means that multiple distinct hardware designs all need to interpret programs, stored as bit patterns, in the same way. The hardware could vary by executing programs faster or slower or by providing more or less memory, but the basic functionality of the program should be the same on all instances of the hardware.

To accomplish this, Brooks proposed a standardized「architecture,」a specification that defines a fixed instruction set and the bit pattern encoding each instruction. The resulting instruction set architecture is called the IBM System/360 ISA.

It's worth an aside to understand how different Fred Brook's world of computers was compared with ours today. A typical IBM 360, the model 25, could be rented for $5,330 a month or purchased for $253,000 in 1968 (equivalent to about $35,800 and $1.7 million in 2016). The model 25 was aimed at users of「small and medium sized computers」(IBM, 1968). In its largest configuration, its main memory contained 48,000 bytes (each byte is 8 bits). By contrast, the main memory on the laptop I am using to write this book has about 16 billion bytes, and the purchase price was about $2,000.

Despite the enormous differences in cost and scale, Brooks' basic idea of an ISA persists almost unchanged to this day. The ISA used in the laptop on which I am typing this text is called the「x86」instruction set. It was originally introduced in 1978 in the Intel 8086 microprocessor, about 10 years after the IBM 360 first appeared. A variant of the 8086 called the Intel 8088 was used in the first IBM PC, introduced in 1981, shown in figure 5.1 .

The x86 ISA grew over time, but it grew in a「backward compatible」way, meaning that an Intel 80186, 80286, 80386, 80486, and many other microprocessors could all execute programs that were written for the 8086. The Haswell processors shown in figure 3.2 are also x86 processors.

Figure 5.1 Original IBM Personal Computer, model 5150. [Image licensed under CC BY-SA 3.0 by Ruben de Rijcke. From https://commons.wikimedia.org/w/index.php?curid=9561543 .]

The astonishing persistence of the x86 ISA is a real testament to the power of Brooks' idea. Ironically, the hardware becomes transient, disposable after a few years, and the software endures for decades. Even the word「endure」underscores the irony because this word originates from the old French usage, where「dure」means「hard,」and to build a「durable」building, one builds it out of hard material such as stone. Yet in computing, software endures much better than hardware.

Let me illustrate how an ISA abstracts the hardware. Suppose, for example, that one of the tasks for the machine whose hardware is depicted in figure 4.6 is to compare two numbers. If the numbers are equal, then it should branch to a different part of the program. If the numbers are unequal, then it should continue executing the sequence of instructions that it is currently executing. This might be part of the search function on Wikipedia, for example, or a search for the occurrence of a word in a text.

Figure 5.2 shows a small segment of a program for an x86 machine. In the figure, each box represents an instruction. The machine executes the instructions one after the other, from top to bottom. The grey boxes represent arbitrary, unspecified instructions. Two specific instructions are shown. The first is

```
cmp eax, ebx
```

This instruction compares the contents of two registers named「eax」and「ebx.」These two registers contain 32-bit numbers; prior to executing this instruction, the program has presumably loaded these registers to contain the numbers representing the characters we are searching for. For example, the characters「Plat」can be loaded into a 32-bit register, assuming that each character is encoded with 8 bits.

Figure 5.2 Small fragment of x86 assembly code.

The previous instruction is written in assembly language, a textual specification that has to be translated into machine code. The machine code for this instruction is

0011010111010100

The text in the figure is translated into this binary representation by a program called an「assembler.」The「cmp」word is called a「mnemonic」because it is easier to remember than「0011010111010100.」

If I may digress briefly, I would like to comment on the culture of programmers. In the 1960s and 1970s, the memory in computers was much smaller than it is today. At that time, it was advantageous to represent an instruction with the mnemonic「cmp」rather than「compare」because「cmp」requires only 24 bits to store, whereas「compare」requires 56. Today, memory is plentiful, but engineers still feel compelled to use short cryptic mnemonics rather than complete words. They will write「fun」rather than「function,」「len」rather than「length,」and「buf」rather than「buffer.」I personally find this an amusing (and sometimes annoying) cultural relic.

The other instruction explicitly shown in figure 5.2 is

```
je label
```

The mnemonic「je」stands for「jump if equal,」and the argument「label」tells the assembler where in the program to jump to if the registers compared by the previous instruction are equal.

There are aspects of this design that seem quite arbitrary, besides the cosmetic choice of mnemonics. For example, why did the designers of the x86 instruction set choose to first compare and then jump in two separate instructions? Why didn't they combine these into a single instruction, such as

```
je eax, ebx, label
```

They could have done this, but it would have complicated the hardware design because now a single instruction needs to encode four things: the「jump if equal」command, the two registers to compare, and the destination address. The engineering problem that the designers of the x86 architecture were solving straddled two levels of abstraction: the hardware design at the digital machine level, as in figure 4.6 , and the instruction set that would be used to specify programs. The phenomenon of assembly language and the lower level phenomenon of the computer hardware affect each other with bidirectional causality.

Engineers who work at these levels are called「computer architects.」There is a long and rich history of architectures, most of which have not survived in the marketplace, and some of which operate in very different ways. So-called「dataflow computers,」for example, don't even specify programs as sequences of instructions (Arvind et al., 1991). Today, a small handful of instruction set architectures dominate (x86, ARM, SPARC, MIPS, RISC-V, and few others).

Although a computer architect operates at a level quite separated from the「sciences of the natural,」ample opportunity exists to use the scientific method to optimize computer architectures. Hennessy and Patterson (1990) revolutionized the field of computer architecture by advocating in their textbook a「quantitative approach,」which amounted to systematic use of experiments. A computer architect can form a hypothesis that a particular choice of instruction set design will improve performance and then design experiments to measure the performance on actual programs. This could be done using programs found「in the wild,」but these days it is done instead with standardized benchmark suites. The programs in such a suite are idealized models of real programs that attempt to capture their essential features.

The concept of an instruction set architecture brings us safely across the boundary from hardware to software. It is now possible to build applications by writing textual programs. But doing so in assembly language is not a good idea. The programs are too difficult to understand at such a low level of abstraction. To bring up the level of abstraction, computer scientists invented programming languages.

5.2 指令集体系架构

早在 20 世纪 60 年代，在 IBM（国际商业机器公司）工作的小弗雷德里克·布鲁克斯就创建了指令集体系架构（ISA）的概念。该架构对计算机硬件的功能进行了抽象。当计算机执行一个程序时，它执行一系列指令。例如，一条指令可能对两个数进行比较，另一条指令则可以根据比较的结果指定下一步要执行的指令。毫无疑问，一台计算机可以执行的一系列指令被称为它的「指令集」。在布鲁克斯之前，每一种不同的计算机模型都有不同的指令集。

在 20 世纪 60 年代，IBM 开发了一个名为 System/360 的计算机系列产品。System/360 项目的目标之一是生产能够执行相同程序的各种计算机产品线。也就是说，一旦你有一个可以放入指令存储器的比特模式，那么，同样的比特模式在入门级计算机、更高级更昂贵的计算机上都能运行。这意味着多种不同的硬件设计都需要以相同的方式解释存储为比特模式的程序。硬件可能因执行程序的快或慢、提供存储器的多或少而有所不同，但是在硬件的所有实例上，程序的基本功能都应该是相同的。

为了实现这一点，布鲁克斯提出了一个标准化的「体系结构」，它是一种定义了一个固定指令集和编码每条指令的比特模式的规范。之后产生的指令集体系结构被称为 IBM System/360 ISA。

值得一提的是，布鲁克斯的计算机世界与我们今天的相比有很大的不同，大家非常有必要知道这一点。作为典型的 IBM 360 系列计算机，model 25 在 1968 年可以以每月 5 330 美元的价格被租用，或以 25.3 万美元的价格被购买（相当于 2016 年的 3.58 万美元和 170 万美元）。model 25 的目标客户是「中小型计算机」用户（IBM，1968）。在其最大配置中，主存包含 4.8 万个字节（每个字节是 8 比特）。相比之下，我用来撰写这本书的笔记本电脑的主存大约有 160 亿个字节，这台电脑的售价约为 2 000 美元。

尽管在成本和规模上存在着巨大的差异，但布鲁克斯有关指令集体系架构的基本思想一直沿用至今。我正在输入当前内容的笔记本电脑使用的指令集体系结构被称为「x86」指令集。它最初是在 1978 年英特尔的 8086 型微处理器中被引入的，大约比 IBM 360 计算机的问世晚了 10 年。英特尔公司在 1981 年推出的第一台 IBM PC 中使用了 8086 型微处理器的一个变体 —— 英特尔 8088（如图 5.1 所示）。

图 5.1 IBM 最早的个人电脑，型号 5150。（图片由鲁本·德·里克提供，并获得 CC BY-SA 3.0 授权。图片来自 https://commons.wikimedia.org/w/index.php?curid=9561543。）

x86 指令集的规模随着时间的推移而不断增长，但它是以「向后兼容」的方式增长的。这意味着英特尔 80186、80286、80386、80486 和许多其他微处理器都可以执行为 8086 编写的程序。图 3.2 所示的 Haswell 系列处理器也是 x86 处理器。

x86 指令集体系架构惊人的生命力强有力地证明了布鲁克斯的想法的威力。具有讽刺意味的是，硬件的生命力变得短暂，用几年就得更换，而软件却可以持续使用几十年。甚至连「endure」这个词也凸显了讽刺意味，因为这个词源于古法语用法，「dure」的意思是「坚硬」（hard），而要建造一座「耐久的」建筑，就得使用石头等坚硬的材料。然而，在计算机领域，软件要比硬件耐久得多。

下面，我来说明指令集体系架构是如何抽象硬件的。举例来说，假设硬件如图 4.6 所示的机器的任务之一是比较两个数。如果这两个数相等，那么它应该跳转到程序的另一部分。如果不相等，则应继续执行当前正在执行的指令序列。例如，这可能就是维基百科搜索功能的一部分，或者是搜索文本中出现的一个单词的功能部分。

图 5.2 给出了 x86 计算机程序中的一个小片段。在图中，每个框代表一条指令。机器从上到下依次执行这些指令。灰色框表示任意的、未指定的指令。图中给出两个具体指令，其中的第一条是：

```
cmp eax, ebx
```

该指令比较两个寄存器「eax」和「ebx」的内容。这两个寄存器中存放了 32 位数；在执行这条指令之前，程序大概已经加载了这些寄存器，以包含表示我们正在搜索的字符的数字。例如，可以将字符串「Plat」加载到 32 位寄存器中，假设每个字符都采用 8 位编码。

图 5.2 x86 汇编代码的小片段

上面的指令是用汇编语言编写的，这是一种专业的文本规范，必须被翻译成机器码。这条指令的机器码为：

0011010111010100

图中的文本被称为「汇编器」的程序转换成这种二进制表示形式。

「cmp」这个词被称为「助记符」，因为它比「0011010111010100」更容易被记住。

请允许我稍稍拓展一下，我想谈谈程序员的文化。在 20 世纪 60 年代和 70 年代，计算机的存储器要比现在小得多。在当时，使用助记符「cmp」要比「compare」更有优势，因为存储「cmp」只需要 24 比特，而「compare」需要 56 比特。今天，计算机的存储容量大幅增加，但工程师仍然觉得必须使用简短而神秘的助记符而不是完整的单词。他们更愿意写「fun」、「len」和「buf」，而不是完整的「function」、「length」和「buffer」。我个人认为这是一个有趣（有时又有点儿令人讨厌）的文化遗产。

图 5.2 中明确给出的另一条指令是：

```
j e label
```

助记符「je」表示「如果相等就跳转」，参数「label」告诉汇编器，如果前一条指令所比较的寄存器是相等的，则程序要跳转到程序的哪个位置。

除了这种注重形式的助记符选择，这种设计还有一些方面看起来相当随意。例如，为什么 x86 指令集的设计者会选择在两条指令中进行先比较再跳转的操作呢？为什么他们不把这两步合并成一条指令呢？例如下面的指令：

```
j e eax, ebx, label
```

他们本来可以这样做，但是这会使硬件设计变得复杂，因为现在一条指令需要编码 4 种东西：「jump if equal」（如果相等就跳转）命令、要比较的两个寄存器以及目标地址。x86 架构的设计者要解决的工程问题跨着两个抽象层：数字机器层的硬件设计（如图 4.6 所示）和用于设计程序的指令集。汇编语言现象和计算机硬件底层现象受双向因果关系支配而相互影响。

工作在这些层的工程师被称为「计算机架构师」。计算机体系架构有着悠久而丰富的历史，其中大多数都没有在市场上留存下来，而其中的一些则以非常不同的方式运行着。例如，所谓「数据流计算机」甚至不把程序表示为指令序列（阿尔温德等，1991）。今天，只有少数指令集体系架构占据着主导地位（包括 x86、ARM、SPARC、MIPS、RISC-V 以及少数其他架构）。

尽管计算机架构师工作在一个与「自然科学」完全分离的层次上，但他们仍有大量的机会利用科学方法来优化计算机体系结构。亨尼西和帕特森（1990）在他们的教科书中开创性地提倡一种「定量方法」，即系统地使用实验，从而在计算机体系架构领域掀起了一场革命。

计算机架构师可以建立一种假设，即特定的指令集设计选择将提高计算机的性能，然后设计不同的实验来测量实际程序的性能。这可以通过一些非常规的测试程序完成，但是现在它是用标准化的基准测试套件来完成的。这种套件中的程序是真实程序的理想化模型，它们试图呈现这些真实程序的基本特性。

指令集体系架构的概念使我们安全地跨越了从硬件到软件的界限。现在，我们就可以通过编写文本程序来构建应用程序。但用汇编语言来构建应用程序并不是一个好主意。在这么低的抽象层上，要理解这些程序是非常困难的。为了提高抽象的层次，计算机科学家发明了编程语言。

### 5.3 Programming Languages

Fred Brooks, crediting Aristotle, in a famous paper titled No Silver Bullet—Essence and Accidents of Software Engineering , made a distinction between accidental complexity and essential complexity (Brooks, 1987). Essential complexity, Brooks argues, is the complexity inherent in the problem that we are asking the software to solve. Accidental complexity arises from the difficulties that「today attend [software] production but are not inherent.」

If I were asked to write this book using a keyboard with only two keys labeled「0」and「1,」I could, in principle, do so. The computer, after all, stores this entire book as a sequence of zeros and ones. But it would be difficult to write a book this way. The reality is that this book is difficult enough to write without having to deal with such accidental complexities.

Following Brooks, I would argue that the essential difficulties in writing this book center on how to weave an accessible story around highly technical topics. The technology I have at my disposal has probably removed nearly all of the accidental complexities around this task. I have a QWERTY keyboard, and I can touch type quite fast. I have excellent, free, open-source word processing software ( ).

When I can't recall what exactly it is that Fred Brooks said in his silver bullet paper, I just go to Google and search for「silver bullet,」and I quickly have the paper right in front of me. The only remaining difficulties are the essential ones that follow from the possibly quite controversial cases that I'm trying to make, including the one here, that technology development is a fundamentally creative human activity driven by culture and aesthetics and built on models that are human fabrications much more than discovered natural laws. Only the difficulty of making this case makes writing this book difficult.

The engineered systems that help me, my laptop computer, , Wikipedia, and Google, are human constructions of astonishing complexity. The engineers responsible for them relied on tools that also removed many of the accidental complexities, enabling them to focus on the essential complexities. Jimmy Wales and Larry Sanger, who created Wikipedia, did not write their programs in binary or even assembly language. In fact, they used several additional layers of models.

The next layer above ISAs and assembly language is the programming language. In late 1953, John W. Backus at IBM started a project to develop an easier language for expressing programs, particularly those extensively using mathematical expressions. The result of this project was Fortran, a language that endures to this day, with the latest update to the language occurring in 2008.

In Backus' time,「Fortran」was written「FORTRAN.」In fact, most everything was written using only capital letters because if you restrict the alphabet to only capital letters, then each letter can be encoded with fewer bits, saving memory. Like the curt mnemonics of assembly code, the use「all caps」became a bit of a cultural relic. My late colleague Chittoor Ramamoorthy, a charming man who went by「Ram」and contributed a great deal to the field of computer architecture, persisted until his death in 2016 in using only capital letters in all his communications, seemingly oblivious to the cultural shift where the use of all caps became yelling.

Figure 5.3 shows a single Fortran statement on a punched card. In the 1950s and 1960s, punched cards were both a storage medium (a stack of cards was a record of the program) and a data entry mechanism. This card reveals one of the key innovations of the Fortran language, which is the use of symbolic variable names rather than memory addresses to refer to numeric quantities that the program is to manipulate. Specifically, the Fortran statement on the card is

Z(1) = Y + W(1)

Figure 5.3 Punched card containing one Fortran statement. [Image licensed under CC BY-SA 2.5 by Arnold Reinhold, via Wikimedia Commons. From https://commons.wikimedia.org/wiki/File:FortranCardPROJ039.agr.jpg .]

Here, Y refers to a value that has presumably been previously assigned, perhaps using a Fortran statement such as

Y = 42

Z(1) and W(1) refer to the first values in arrays named Z and W. [1] Writing code this way removes the accidental complexity of having to decide where in memory these variables are to be located, choosing registers to temporarily store the values, giving instructions for loading the values from memory into registers, and finally giving the instruction to perform the add. The latter style is what would be required in assembly code.

A Fortran program is translated into assembly code (or directly into machine code) by a compiler. The compiler is responsible for deciding which registers are used for what and where in memory values are stored. Designing good compilers is quite an art, with many opportunities for optimization and experimentation.

But designing good programming languages is more subjective. Programming languages can develop fervent, almost religious followings. Followers of so-called「functional programming,」for example, are notorious for their zeal, advocating languages such as Haskell, named after logician Haskell Curry, and SML, Standard ML. SML is a descendant of ML (MetaLanguage), developed by Robin Milner, a prolific computer scientist and one of my personal heroes who did most of his work at the University of Edinburgh in Scotland and at Cambridge in England. These languages have an elegant mathematical way of specifying computation. Programs can be quite aesthetically pleasing, succinctly stating intent without over-specifying how the intent is to be realized. Nevertheless, among the pantheon of languages, pure functional languages have a small, albeit devoted following.

Much like natural language, programming languages shape the thinking of a programmer. As I mentioned earlier, Abelson and Sussman talk about computing as a「procedural epistemology」:

the study of the structure of knowledge from an imperative point of view, as opposed to the more declarative point of view taken by classical mathematical subjects. (Abelson and Sussman, 1996)

A program is imperative in the sense that it tells a computer what to do, as opposed to a mathematical equation, which tells what is. But there are many ways to tell a computer what to do.

A direct way to tell a computer what to do is to tell it how to do it. Computer scientists call a program「imperative」if it specifies a sequence of commands, giving a step-by-step procedure, a recipe that the computer is to follow. An imperative program directly represents knowledge as procedure, and like all knowledge, it is surely shaped by language. Most of the widely used programming languages, including Fortran, are imperative languages.

The functional languages, in contrast to imperative languages, adopt the declarative style of mathematics. In an imperative language, for example, the pair of statements

x = 1;

x = 42;

means to first assign the value 1 to variable x and then to change the value of the variable x to 42. [2] In a declarative language, these two statements are contradictory and will be rejected by a compiler. In a declarative language, the = operator has a different meaning. A statement x = 1 does not assign a value to a variable at a particular point in a procedure but rather declares that the symbol x means 1, not at a point in a procedure but always. The order in which such statements are given is irrelevant. In a declarative language, the two statements above are contradictory because x can't mean 1 and also mean 42. Their declarative style is distinctly different from the procedural, step-by-step style of imperative programs. It is perhaps ironic that despite claiming that software constitutes a「procedural epistemology」and「the study of the structure of knowledge from an imperative point of view,」Abelson and Sussman's book uses throughout a dialect of Lisp, a functional language originally developed by John McCarthy in the 1950s. Although a Lisp program tells a computer what to do (and hence is imperative in the broader sense of the word), it is a declarative language at its core.

Purely functional languages have been less successful than imperative languages, having only a small but devoted following. As Kuhn says,

As in political revolutions, so in paradigm choice—there is no standard higher than the assent of the relevant community. (Kuhn, 1962, p. 94)

Kuhn talks about scientific paradigms being incommensurable. They can be irreconcilable accounts of reality, where one paradigm cannot be understood or judged through the conceptual framework and terminology of the other. At their most basic level, programming languages are not incommensurable because they are all (today) essentially equivalent to Turing machines, which have an imperative flavor, and to Church's lambda calculus, which has a declarative flavor (see chapter 8 ). But programmers are usually not using these languages at such an elemental level, and when bundled with the libraries, tools, patterns, and idioms that accompany a language, they arguably do become incommensurable paradigms. Kuhn continues,

To be accepted as a paradigm, a theory must seem better than its competitors, but it need not, and in fact never does, explain all the facts with which it can be confronted. (Kuhn, 1962, p. 18)

Programming languages do not exist to explain facts but rather to realize algorithms. Any language will realize some algorithms better than others. This may help explain the cacophony of languages that prevail today. If you can indulge me, dear reader, I would like to explore that cacophony.

Wikipedia is realized by an open-source program called MediaWiki, which is written in the PHP programming language. The first version of MediaWiki was created in 2001 by Magnus Manske, then a student at the University of Cologne. His program was later named MediaWiki, a permutation of the name of its biggest user, the Wikimedia Foundation, which runs Wikipedia. As with a lot of open-source software, many people have contributed to MediaWiki since Manske's original design.

Why did Manske use PHP to program MediaWiki? PHP was originally created in 1994 by Rasmus Lerdorf, a Danish-Canadian programmer who worked at Yahoo. PHP is a「scripting language」specifically designed for building web pages. A scripting language is a programming language intended for specifying short scripts that automate tasks that would otherwise be performed by a human. Notice the layers of culture rather than just technology behind all this: scripting language, wiki, open source, web page. These things did not exist three decades ago, and they are much less new technologies than they are new cultures.

The acronym「PHP」originally stood for Personal Home Page, but according to the current developers, PHP now stands for「PHP: Hypertext Preprocessor.」The new name makes PHP a「backronym,」which is an acronym where the words are chosen to match the letters rather than vice versa. Moreover, the backronym is self-referential or recursive because the「P」stands for「PHP.」Recursion is one of the central tenets of computer science, one of the basic concepts taught in every introductory computer science class. So computer scientists like to pun with recursion.

The use of recursive acronyms was popularized by Richard Stallman with GNU, which stands for「GNU's not Unix!」Choosing a recursive backronym for PHP was, I suspect, a bow to Stallman. GNU is a collection of software that Stallman intended to eventually replace Unix, an operating system originally developed in the 1970s at Bell Labs by Ken Thompson, Dennis Ritchie, and others.

Richard Stallman ( figure 5.4 ) is one of the most influential individuals today in the world of software. Stallman is responsible for a great deal of software that is used worldwide for many purposes. He is also one of the most interesting characters in the story of software. Stallman's GNU project was, in part, a revolt against corporate America. He has spent much of his effort in recent years campaigning against all sorts of encumbrances on software, including software patents, digital rights management, software license agreements, nondisclosure agreements, activation keys, copy restriction, and binary executables that do not include the source code.

Figure 5.4 Richard Stallman in Vietnam. [Copyright by Richard Stallman, released under「CC-ND,」 https://stallman.org/photos/ .]

In 1985, Stallman launched the Free Software Foundation, which is committed to freeing software. Note my odd use of words; I didn't say it was committed to「free software,」which could be easily misunderstood as software that does not cost money. The cost of the software is irrelevant; Stallman uses「free」as in「freedom.」In fact, I'm convinced that Stallman anthropomorphizes software, and that his commitment is to freeing the software so the software can go wherever it likes and do whatever it likes, rather than freeing the humans that use software. The latter model, which is better represented by the Berkeley open-source software movement, allows humans to do whatever they like with open-source software. Stallman's model, however, constrains the humans to ensure that they never enslave the software. The copyright notice on GNU software, called the GNU General Public License (GPL), specifically requires that any uses and modifications of GPL'd software preserve the same open rights as the original. This style of copyright is sometimes called a「copyleft」presumably because of seemingly left-leaning politics compared with the right-wing corporate-dominated copyright.

I'm hoping that you can see that the world of software constitutes a diversity of cultures and a literature with parody, social commentary, language, and politics all playing a role, along with technology.

But I digress. My topic in this section is programming languages. Returning to PHP, the language used to create MediaWiki, Lerdorf did not intend PHP to be a new programming language. In an audio interview, Lerdorf noted,

I don't know how to stop it, there was never any intent to write a programming language · · · I have absolutely no idea how to write a programming language, I just kept adding the next logical step on the way. (Lerdorf, 2003)

It is not uncommon for major software artifacts to come about this way. They start as small, personal projects, and they grow organically. Lerdorf quipped,「I really don't like programming. I built this tool to program less so that I could just reuse code.」With this style of design, the personality and aesthetics of the original authors have a huge impact on the end product.

Besides PHP, several of the most widely used programming languages today, C, C++, C#, and Java, share many essential features with Fortran and with each other. Even so, crossing denominations is rare. A C++ programmer will fight any request to write a Java program and vice versa, often with dogmatic arguments of faith and aesthetics.

In his 1987 Silver Bullet article, Brooks argued that programming languages had advanced sufficiently to have removed nearly all the accidental complexity in programming. The remaining essential complexity, he said, accounted for what has become known as Brooks' law,

Adding manpower to a late software project makes it later.

Brooks first articulated this law in his 1975 book, The Mythical Man Month (Brooks, 1975), which is often credited for launching the field called「software engineering.」Brooks once quipped that his book is called「The Bible of Software Engineering」because「everybody quotes it, some people read it, and a few people go by it.」

But I believe that Brooks vastly underestimated the complexity of systems that were to come, and programming languages alone do not provide an appropriate level of modeling. Many modern software systems consist of millions of lines of code, vastly more than any human can comprehend at the level of the programming language. Instead, programs have to be designed and understood as compositions of subprograms, much the way hardware at the digital machine level abstracts the low-level logic gates.

If you study computer science today, you will likely learn to use only a small number of programming languages, maybe even only one. In my opinion, a software engineer who has mastered only one language is about as well educated as a medieval monk who has studied exactly one book. There is a great deal to be learned from even studying the extensive graveyard of programming languages that have faded from memory.

The following, for example, is a short program in the programming language APL, which I used in a class that I took at Yale in 1978:

x [ ← 5?10]

APL, which stands for A Programming Language, was developed by Kenneth Iverson in the late 1960s. Iverson received the Turing Award in 1979 for this work. At Yale, an entire computer room was equipped with special terminals that had keyboards that could make the characters in the previous program, such as and ←.

Iverson wanted a language that would concisely specify mathematical operations on entire arrays of data all at once. I can explain the prior program if you can tolerate a short but intense nerd storm. The inner expression 5?10 means, in APL, to create an array with five elements consisting of random numbers in the range 1 to 10 with no repetitions. For example, evaluating this expression in APL might yield the array [9,4,3,8,1]. The expression x ← 5?10 means that this array should become the value of the variable x. The operator represented by the symbol takes the array that is now the value of x, sorts it, and returns indices that can be used to retrieve the values in the array in numerical order. The construct x[ · · · ] then uses that array of indices to retrieve the values. So here is a sequence of evaluations that yields a result:

x [ x ← 5?10]

x [ x ← [9, 4, 3, 8, 1]]

x [ [9, 4, 3, 8, 1]]

x [[5, 3, 2, 4, 1]]

[1, 3, 4, 8, 9]

So this program generates an array with five random numbers and then sorts the array so that you get the numbers in increasing order. As you can see, APL programs can be quite cryptic, but they tend to be concise.

A graveyard language that takes the opposite approach is COBOL, after「common business-oriented language.」COBOL was designed in 1959 based on an earlier language developed by Grace Hopper, shown in figure 5.5 . Hopper was an early proponent of high-level programming languages that were portable, meaning that they could be compiled to execute on a variety of machines, even machines with different instruction set architectures.

COBOL was intended to have a syntax more like English than like mathematics, so it tends to replace symbol operators with words. For example, instead of the APL assignment statement x ← y, in COBOL you would say MOVE y TO x . For many years, COBOL was widely used for business applications such as banking, but today few new programs are written in COBOL.

COBOL and APL represent extremes in an exploration of programming paradigms. COBOL is verbose, using English-language words, with the idea that programs would be more readable by business people. APL is concise, cryptic, and requiring special keyboards. Both succumbed to the Darwinian competition of paradigms, dinosaurs that were once successful but are now largely extinct.

Many more languages are in the graveyard, including Algol, Pascal, PL/I, SNOBOL, Smalltalk, and Prolog. Each of these has interesting ideas and an interesting story. Algol introduced many features present in most modern imperative programming languages, including Java, C, C++, and C#. Pascal introduced the idea of compiling first into a virtual machine language (called byte code) and then executing that program in a program that simulates the virtual machine. This is a centerpiece of the widely used Java language today. SNOBOL, developed at Bell Labs by David Farber, Ralph Griswold, and Ivan Polonsky in the 1960s, introduced high-level manipulation of text, including parsing and pattern matching, a centerpiece of the widely used JavaScript language today, among others. Smalltalk was one of the earliest object-oriented languages, providing a way of structuring programs that is widely used today. Prolog is a「logic programming」language that elegantly expresses rule-based queries over structured data.

Figure 5.5 Rear Admiral Grace Hopper, 1906-1992. Hopper was an early proponent of portable programming languages and pioneered a style of programming where programs read more like English-language sentences than like mathematical expressions. [Image courtesy of the United States Navy.]

Each of these languages encodes a paradigm, a way of thinking about computation. These languages did not die the way Kuhn's scientific paradigms die. No crisis was created by anomalous observations that exposed discrepancies between the paradigm and the natural world. Rather, these languages either mutated into new species of languages (as in ALGOL and Pascal) or progressed toward extinction in a Darwinian competition of survival of the fittest or the most promiscuous (as in APL and COBOL).

[1] Fortran makes extensive use of arrays as a way to manage memory. For example, an array W with four integers might be declared and then initialized with the statements

INTEGER, DIMENSION(4) :: W

W = (/ 42, 43, 44, 45 /)

After these statements are executed, the value of W(1) is the integer 42, the value of W(2) is the integer 43, and so on.

[2] Among computer scientists, the number 42 is popular to use in examples because of Douglas Adams' Hitchhiker's Guide to the Galaxy , a 1978 BBC radio comedy series that later became a「trilogy」of five books. In that story, a special computer called Deep Thought is built to answer the「ultimate question of life, the universe, and everything.」The computer takes 7.5 million years to compute and check the answer, which turns out to be 42. The computer reports that the answer seems meaningless because the beings who programmed it never actually knew what the question was.

5.3 编程语言

小弗雷德里克·布鲁克斯信奉亚里士多德的理念，他在著名的论文《没有银弹：思考软件工程中的根本和次要问题》（以下简称《银弹》）中对偶然复杂性和本质复杂性进行了区分（布鲁克斯，1987）。布鲁克斯认为，本质复杂性是我们要求软件解决的问题所固有的复杂性。偶然复杂性源于「当今伴随（软件）生产而出现的非固有的」各种困难。

如果要求我只能用带有「0」和「1」两个键的键盘来撰写这本书，那么原则上我是可以这样做的。毕竟，计算机会将整本书存储为 0 和 1 的序列。但是，用这种方式写一本书肯定特别困难。事实上，在无须处理这种偶然复杂性的情况下，这本书本身就已经很难写了。

除了布鲁克斯所说的复杂性，我认为撰写本书的主要困难在于如何围绕非常技术化的主题来编织一个读者易理解的故事。我所掌握的技术可能已经消除了围绕这项任务的几乎所有的偶然复杂性。我有一个 QWERTY 键盘（全键盘），而且我打字相当快。

我还有优秀、免费且开源的文字处理软件（LATEX）。

当我记不起布鲁克斯在他的《银弹》论文中到底说了什么时，我就会去谷歌搜索「银弹」，很快这篇论文就呈现在我面前了。剩下的唯一困难就是一些本质性的困难了。这些困难来自我试图提出的一些可能颇有争议的问题，包括这里所说的一个问题，技术发展本质上是一种由文化和美学驱动的创造性的人类活动，它建立在人类构造的模型之上，而非被发现的自然法则的模型之上。仅是提出这个问题的困难就已经使得本书的写作变得非常有难度了。

1-2『上面的观点贯穿整本书：技术发展的本质是建立在人类构造的模型之上而非建立在人类发现的自然法则模型之上的。做一张主题卡片。（2021-10-25）』—— 已完成

帮助我写这本书的工程系统包括我的笔记本电脑、LATEX 排版软件、维基百科和谷歌，它们都是人类构建的复杂得惊人的系统。负责这些系统的工程师依赖于同样消除了许多偶然复杂性的那些工具，从而使他们能够专注于本质复杂性。创建维基百科的吉米·威尔士和拉里·桑格并没有用二进制甚至汇编语言编写他们的程序。事实上，他们使用了另外几个模型层。

指令集体系架构和汇编语言之上的一层是编程语言。1953 年年末，在 IBM 工作的约翰·W. 巴克斯启动了一个项目，开发了一种更简单的语言来表达程序，特别是那些广泛使用数学表达式的程序。这个项目的结果是产生了 Fortran 语言，它是一种一直沿用至今的语言。它的最新版本出现于 2008 年。

在巴克斯的时代，「Fortran」会被写成「FORTRAN」。事实上，大多数文本都是用大写字母写出的，因为如果把字母表限制为只用大写字母，每个字母就可以用更少的比特位来编码，从而节省存储器，就像汇编代码的简略助记符一样。字母「全部大写」也成了一种文化遗产。我的同事奇图尔·拉马莫西（Chittoor Ramamoorthy）生前是个很有魅力的人，常被称为「Ram」，他为计算机体系结构做出了很大的贡献。在 2016 年去世之前，他在所有的通信中一直坚持只使用大写字母，似乎并没有注意到这种文化的转变 —— 全部使用大写字母已经变得像一种大喊大叫了。

图 5.3 给出了打孔卡片上的一个 Fortran 语句。在 20 世纪 50 年代和 60 年代，打孔卡片既是一种存储介质（一叠卡片记录一个程序），也是一种数据输入机制。图中的这张卡片揭示了 Fortran 语言的一个关键性创新 —— 使用符号变量名而不是内存地址来指代程序要操作的数字量。具体来说，卡片上的 Fortran 语句是：

```
Z(1) = Y + W(1)
```

在这里，Y 指的是一个之前可能已经被赋值的值，可能使用了如下的 Fortran 语句：

```
Y = 42
```

图 5.3 包含一个 Fortran 语句的打孔卡片。（阿诺德·雷因霍尔德通过维基共享资源供图，并获得 CC BY-SA 2.5 授权。）

Z(1) 和 W(1) 分别是名为 Z 和 W 的数组中的第一个值，通过这种方式编写代码可以消除这样一些偶然复杂性：必须确定内存中这些变量的位置，选择寄存器临时存储这些值，给出将这些值从内存加载到寄存器的指令，以及最后给出执行加法操作的指令。后一种风格是汇编代码中所需要的。

Fortran 程序经由编译器转换为汇编代码（或直接转换为机器码）。编译器负责决定哪些寄存器用于存储什么，以及这些值存放在内存中的什么位置。好的编译器的设计是一门艺术，其中有很多优化和实验的机会。

但是，好的编程语言的设计更具有主观性特点。编程语言可以激发热情，甚至培养出虔诚的追随者。例如，所谓「函数式编程」的追随者曾因其热情而有些声名狼藉。他们推崇使用 Haskell（以逻辑学家哈斯凯尔·加里的名字命名）和 SML（标准 ML）等语言。SML 语言源于 ML（元语言），而 ML 是由罗宾·米尔纳开发的。米尔纳本人既是一位成果丰硕的计算机科学家，也是我心目中的一个英雄。他的大部分工作是在苏格兰爱丁堡大学和英国剑桥大学完成的。

这些语言使用一种优雅的数学方法来指定计算。这样的程序非常美观，简洁地陈述意图而不过分指定如何实现意图。尽管如此，在计算机语言的万神殿中，函数式语言只有一小部分忠实的追随者。

就像自然语言那样，编程语言塑造了程序员的思维。正如我在前面提到的，阿贝尔森和萨斯曼将计算作为一种「程序认识论」：

从命令式的观点研究知识的结构，而不是古典数学学科所采取的更具陈述性的观点。（阿贝尔森和萨斯曼，1996）

程序是命令式的，因为它告诉计算机要做什么，这与说明这是什么的数学方程相反。

但是，告诉计算机做什么的方法有很多。

告诉计算机做什么的直接方法是告诉它该如何去做。如果一个程序给定一个命令序列，并给出计算机所需遵循的逐步执行过程，计算机科学家就将其称为「命令式」程序。命令式程序直接将知识表示为程序式的过程，就像所有知识一样，它肯定是由语言塑造的。大多数被广泛使用的编程语言，包括 Fortran 语言在内，都是命令式语言。

与命令式语言不同，函数式语言采用数学的声明式风格。例如，如下是命令式语言中的两条语句：

```
x = 1

x = 42
```

其意味着，首先将值 1 赋给变量 x，然后将变量 x 的值更改为 42。在声明式语言里，这两条语句是矛盾的，并会被编译器拒绝。在声明式语言里，操作符「=」具有不同的含义。语句 x=1 不会在程序中的特定点给变量赋值，而是声明符号 x 表示 1，不是在某个点，而是始终。这与所给定的这种语句顺序是无关的。在声明式语言里，上述两个语句是矛盾的，因为 x 的值不能既表示 1，又表示 42。显然，它们的声明式风格与命令式程序的过程式、逐步式风格有着明显的不同。带有些许讽刺意味的是，尽管阿贝尔森和萨斯曼声称软件构成了一种「程序认识论」以及「从命令式的角度研究知识的结构」，但他们的书自始至终都在使用一种 Lisp 方言，这是一种最初由约翰·麦卡锡在 20 世纪 50 年代开发的函数式语言。虽然 Lisp 程序告诉计算机要做什么（因此从广义上理解也是命令式的），但它本质上是一种声明式语言。

函数式语言远远不如命令式语言成功，只有少数狂热的追随者。正如库恩说的那样：

对范式的选择也如政治革命一样 —— 没有什么标准能比得到相关团体的赞同更高了。（库恩，1962:94）

库恩认为科学范式之间是不可通约的。它们可以是对现实不可调和的描述，其中一种范式不能用另一种范式的概念框架和术语进行理解或判断。在最基本的层面上，编程语言并非不可通约，因为它们（如今）在本质上都等同于具有命令式风格的图灵机器以及丘奇具有声明式风格的 λ 演算（参见第 8 章）。但是程序员通常不会在这样一个基本层次上使用这些语言。当这些基本的编程语言与伴随一种语言的库、工具、模式和惯用用法捆绑在一起的时候，它们可能会成为不可通约的范式。库恩继续指出：

一种理论要被接受成为一种范式，它必须看起来比与它竞争的范式更好，但它不需要，而且事实上也永远不会解释它所能面对的所有事实。（库恩，1962：18）

编程语言的存在并不是为了解释事实，而是为了实现算法。任何语言都能比其他语言更好地实现一些算法。理解这一点可能有助于解释当今盛行的各种语言之间的不相容之处。亲爱的读者，请允许我探究一下这些不和谐的声音。

维基百科是基于一个名为 MediaWiki 的开源程序实现的，它是用 PHP 编程语言编写的。MediaWiki 的第一个版本由马格努斯·曼斯奇于 2001 年创建，当时他还是科隆大学的学生。他的程序后来被命名为 MediaWiki，这是它的最大用户、运行维基百科的维基媒体（Wikimedia）基金会的名字的变体。和许多开源软件一样，从曼斯奇的最初设计开始，有很多人对 MediaWiki 的发展做出了贡献。

为什么曼斯奇要使用 PHP 来编写 MediaWiki？PHP 最初是由在雅虎工作的加拿大籍丹麦程序员拉斯马斯·勒德尔夫于 1994 年创建的。PHP 是一种专门为构建网页而设计的「脚本语言」。脚本语言是一种用于编写短脚本的编程语言。这些脚本可以自动执行原本由人来执行的任务。就脚本语言、维基百科、开源和网页这一切而言，我们需要关注的不仅仅是技术层面，更要关注其背后的文化层面。这些东西在 30 年前并不存在，因此，与其说它们是新技术，不如说它们是新文化。

缩略词「PHP」最初代表的是个人主页（Personal Home Page），但在当今的开发人员中，PHP 现在代表「超级文本预处理器（HypertextPreprocessor）」。新名称使 PHP 成为「逆向首字母缩略词」，一个根据字母选择匹配单词而非相反的缩略词。此外，逆向首字母缩略语是自引用或递归的，因为字母「P」代表「PHP」。递归是计算机科学的核心原理之一，是计算机科学导论课中教授的基本概念之一。所以计算机科学家通常喜欢用递归来进行双关表达。

递归缩略词的使用是由理查德·斯托曼在 GNU（一款自由的操作系统）中推广的，其代表「GNU 不是 Unix！」我怀疑，为 PHP 选择一个递归的逆向首字母缩略词就是在向斯托曼致敬。GNU 是斯托曼打算最终取代 Unix 的一个软件集。如我们所知，Unix 最初是由肯·汤普逊、丹尼斯·里奇等人于 20 世纪 70 年代在贝尔实验室开发的一种操作系统。

理查德·斯托曼（图 5.4）是当今软件界最具影响力的人物之一。斯托曼领导了在世界各地被用于许多用途的大量软件的开发工作。他也是软件开发历史上最有趣的人物之一。斯托曼的 GNU 计划（也称革奴计划）在一定程度上是对美国企业界的反抗。最近几年，他花了大量精力反对软件上的各种权限障碍，包括软件专利、数字版权管理、软件许可协议、保密协议、激活密钥、复制限制和不包含源代码的二进制可执行文件等。

图 5.4 理查德·斯托曼在越南。（照片版权归理查德·斯托曼所有，照片经「CC-ND」许可发布，来自网站 https://stallman. org/photos/。）

1985 年，斯托曼成立了自由软件基金会，该基金会致力于推广自由软件。请注意这一用词，似乎有种很奇怪的感觉。我没有说它致力于「免费软件」，这很容易被误认为是免费的软件。软件的成本无关紧要。斯托曼在这里所用的 free 指的是「自由（freedom）」的意思。事实上，我确信斯托曼将软件进行了拟人化，他的承诺是给予软件自由，这样软件就可以去它想去的任何地方，做它想做的任何事，而不是给予使用软件的人以自由。以伯克利开源软件运动为代表的后一种模式，允许人们可以对开源软件为所欲为。然而，斯托曼的模式是限制人类的行为，其目的是确保人类永远不会奴役软件。GNU 软件的版权声明也被称为 GNU 通用公共许可证（GPL），特别要求对 GPL 软件的任何使用和修改都要保留与原始软件相同的开放权利。这种形式的版权（copyright）有时被称为「copyleft」。这大概是因为与偏右（right）企业主导的版权相比，其政治立场似乎是偏左（left）的。

我希望你能够看到软件的世界构成了文化上的多样性，也构成了一种文学，模仿、社会评论、语言和政治都与技术一起发挥作用。

不好意思，我又跑题了。本节的主题是编程语言。让我们还是继续 PHP 的话题 —— 用于创建 MediaWiki 的语言。勒德尔夫并不打算将 PHP 视为一种新的编程语言。勒德尔夫在一次音频采访中指出：

我不知道该怎么阻止它，我从来没有想过要写一种编程语言…… 我完全不知道怎么写一个程序语言，我只是在这个过程中不断地添加下一个逻辑步骤。（勒德尔夫，2003）

主要的软件产品都是以这种方式出现的，这并不稀奇。它们总是从个人的小项目开始，然后逐渐发展起来。勒德尔夫打趣道：「我真的不喜欢编程。我创建这个工具是为了少编程，这样我就可以重用代码了。」在这种设计风格下，原作者的个性和审美就对最终产品产生了巨大的影响。

除了 PHP 之外，目前使用最广泛的几种编程语言，如 C，C++，C# 和 Java，都与 Fortran 以及彼此之间共享许多基本特性。即便如此，它们也很难兼容。一个 C++ 程序员会拒绝编写 Java 程序，反之亦然。每种语言的程序员都常常带有某种信念和审美的教条性观点。

布鲁克斯在 1987 年发表的《银弹》一文中指出，编程语言已经取得了长足的进步，几乎消除了编程中所有的偶然复杂性。他说，剩下的本质复杂性解释了所谓的布鲁克斯定律，即向一个延迟的软件项目增加人力会使其进一步延迟。

布鲁克斯在他 1975 年出版的《人月神话》一书中首次阐明了这一定律。这本书通常被认为开启了一个被称为「软件工程」的领域。布鲁克斯曾经开玩笑说，他的书被称为「软件工程的圣经」，因为「每个人都引用这本书，有些人认真阅读它，还有一些人遵从它」。

但是，我相信布鲁克斯大大低估了即将到来的系统的复杂程度，而编程语言本身并不能提供一个合适的建模级别。许多现代软件系统具有数百万行代码，这远远超出任何人类可在编程语言的层次上理解的范围。因此，每个程序都必须被当作子程序的组合来设计和理解，这在很大程度上类似于数字机器层次的硬件抽象低层逻辑门的方式。

如果你今天学习计算机科学，那么你可能只学会使用少数几种编程语言，甚至可能只学会使用一种。在我看来，一个只掌握了一种编程语言的软件工程师，和一个只学过一本经书的中世纪僧侣差不多。其实，我们甚至可以从许多已经被淘汰的编程语言中学到许多知识。

例如，以下是以编程语言 APL 编写的一个短程序，1978 年我在耶鲁大学学习的一门课中就用过这个程序：

x

[x← 5?10]

APL 是一种编程语言（A Programming Language）的首字母缩略词，这一语言是肯尼思·艾弗森在 20 世纪 60 年代末开发的。1979 年，艾弗森因这项工作获得了图灵奖。在耶鲁大学，整个计算机机房都配备了带有特殊键盘的终端，可以输入上述程序中的字符，如和←。

艾弗森想要设计一种能够一次指定对整个数据数组进行数学运算的语言。如果你还能忍受短暂却有些强烈的技术呆子头脑风暴，请允许我在这里解释一下上面的程序。在 APL 中，内部表达式 5?10 表示要创建一个包括 5 个元素的数组，这些元素由 1 到 10 之间没有重复的随机数构成。例如，在 APL 语言中，这个表达式可能会产生数组 [9，4，3，8，1]。表达式 x

← 5?10 表示这个数组应该成为变量 x

的值。由符号表示的运算符获取当前是 x

的值的数组，对其进行排序，并返回可用于按数字顺序检索数组中的值的索引。随后，结构 x

[…] 使用该数组的索引来检索这些值。如下是由此产生的一系列结果：

x

[x

← 5?10]

x

[x

← [9, 4, 3, 8, 1]]

x

[[9, 4, 3, 8, 1]]

x

[[5, 3, 2, 4, 1]]

[1, 3, 4, 8, 9]

由此，这个程序生成了一个包含 5 个随机数的数组，然后对数组进行排序，这样就可以按递增顺序得到这些数。正如你看到的，APL 程序可能看起来相当晦涩，但是它们往往又非常简洁。

已被淘汰的 COBOL（common business-oriented language，面向商业的通用语言）语言采用了与 APL 截然相反的方法。COBOL 是在 1959 年格蕾丝·霍珀（见图 5.5）早期开发的语言基础上设计出来的。霍珀是可移植高级编程语言的早期支持者，这意味着这些编程语言可以被编译到各种机器上执行，甚至是具有不同指令集体系架构的机器上。

COBOL 的语法更像英语而非数学，因为它倾向于用单词代替符号运算符。例如，与 APL 赋值语句 x ← y 不同，在 COBOL 中，你可以写成「MOVE yTO x」。多年来，COBOL 被广泛应用于银行等商业领域。但现在很少有新的程序是用 COBOL 编写的。

图 5.5 格蕾丝·霍珀（1906—1992），美国前海军少将。霍珀是可移植编程语言的早期支持者，她开创的一种编程风格，使程序读起来更像英语句子而不是数学表达式。（该图片由美国海军提供。）

COBOL 和 APL 代表了探索编程范式的两个极端。COBOL 是冗长的，它使用英语单词编写程序，其思想是使得这种程序更易于被商业人士阅读。APL 则简洁、隐秘且需要特殊的键盘。当然，它们都屈从于达尔文式的范式竞争。正如恐龙这一曾经生机勃勃的物种，现在已经全部灭绝了。

还有许多已经被淘汰的语言，包括 Algol、Pascal、PL/I、SNOBOL、Smalltalk 和 Prolog。它们中的每一个都包含了有趣的想法和奇妙的故事。Algol 引入了包括 Java、C、C++ 和 C# 等大多数现代命令式编程语言中的许多特性。Pascal 引入了这样一种思想：首先将一个程序编译成虚拟机语言（它们被称为字节码），然后在模拟该虚拟机的程序中执行这个程序。这是当今广泛使用的 Java 语言的精髓。SNOBOL 是由大卫·法伯、拉尔夫·格里斯沃尔德和伊万·波隆斯基于 20 世纪 60 年代在贝尔实验室开发的。SNOBOL 引入了对文本的高级操作机制，包括解析和模式匹配等，而这正是当今广泛使用的 JavaScript 语言的核心。

Smalltalk 是最早的面向对象的语言之一，它提供了一种当今广泛运用的结构化程序设计方法。Prolog 是一种「逻辑编程」语言，它可以优雅地表达结构化数据中的基于规则的查询。

这些语言中的每一种都编码了一种范式 —— 一种关于计算的思维方式。这些语言范式并没有像库恩所说的科学范式那样消亡了。那些暴露了范式与自然界之间差异的反常的观察并没有造成危机。相反，这些语言要么变异成新的语言物种（如 Algol 和 Pascal 语言），要么在适者生存与混杂式达尔文竞争中渐渐走向灭绝（如 APL 和 COBOL）。

### 5.4 Operating Systems

Today, the word「operating system」means, to most people, one of three things: Apple's OS X, Microsoft's Windows, or Linux. Linux was originally developed in the early 1990s by Linus Torvalds, a Finnish (and later American) software engineer. Linux has become one of the most successful open-source software projects ever, with thousands of contributors and widespread adoption. Linux, like OS X, is based on the Unix operating system originally developed in the 1970s at Bell Labs by Ken Thompson and Dennis Ritchie, with contributions from many others. These three systems, OS X, Windows, and Linux, are the survivors of promiscuous evolution and competition over decades. Today, we should add iOS from Apple and Android from Google, operating systems designed specifically for smartphones and tablet computers.

I could write a great deal about operating systems, but instead I would just like to focus on how an operating system encodes one or more paradigms. A key feature of all these operating systems is the file system. In the hardware of a computer, various forms of memory store sequences of bytes, where each byte is a sequence of eight bits. The laptop computer on which I am writing this book has 16 gigabytes of volatile memory (memory that forgets its contents when you turn off the power) and one terabyte of nonvolatile memory. [3] The nonvolatile memory is sometimes called the「hard disk,」although these days it is more likely to be implemented using a type of semiconductor memory called a flash memory rather than the older spinning magnetic disk memory. As far as the hardware is concerned, the contents of the hard disk is just a sequence of a trillion bytes. The hardware can retrieve or update any single byte.

But a list of a trillion bytes, by itself, is not a useful way to organize information. Early operating system designers, such as Thompson and Ritchie, built into the operating system a way of encoding onto these disks a notion of a「file.」A file is a subset of the eight trillion bytes that forms a logical unit, and a file system supports assigning a name to the file and organizing files into hierarchical directories, which are also named. With the advent of graphical user interfaces, these directories acquired the metaphor of a「folder,」even though, for physical-world folders, folders that contain folders are rather awkward.

My key observation is that nothing in the computer hardware provides the notion of a file and the organization of files into directories. The software embodied in the operating system provides this notion.

The software that realizes the file system is quite clever. It does not even require that the contents of a file be contiguous in memory; the bytes of a file may be scattered all over the disk. The operating system software keeps track of which bytes belong to which file and what directory the file is logically contained in.

Once you have a file system to work with, you no longer need to worry about how your data is stored on a disk. You access the file as a single conceptual unit.

[3] Sixteen gigabytes is about 16 billion bytes, and a terabyte is about one trillion bytes.

5.4 操作系统

今天，对大多数人来说，「操作系统」一词意味着如下三者之一：苹果的 OS X、微软的 Windows 或 Linux。Linux 最初是由芬兰（后来加入美国国籍）软件工程师林纳斯·托瓦兹于 20 世纪 90 年代初开发的，现已经成为有史以来最成功的开源软件项目之一，有着成千上万的贡献者并被广泛使用。和 OSX 一样，Linux 也是基于 Unix 的操作系统。Unix 操作系统最初是由贝尔实验室的肯·汤普森和丹尼斯·里奇于 20 世纪 70 年代开发的，也有其他许多人为之做出了很多贡献。OS X、Windows 和 Linux 这三个系统是几十年来混杂进化和竞争的幸存者。今天，我们还应该加上苹果的 iOS 系统和谷歌的 Android 系统，它们是专门为智能手机和平板电脑设计的操作系统。

我可以写很多有关操作系统的文章，但我只想聚焦于一个操作系统会如何编码一个或多个范式。所有这些操作系统的一个关键特征是文件系统。在计算机的硬件中，各种形式的存储器存储字节序列，其中每个字节都是一个 8 比特的序列。我正用来撰写这本书的笔记本电脑有 16GB 的易失性存储器（当你关闭电源时就会忘记所有内容的存储器），以及 1TB 的非易失性存储器。非易失性存储器有时被称为「硬盘」，虽然现在它更有可能使用一种被称为闪存的半导体存储器，而不是老式的旋转磁盘存储器。就硬件而言，硬盘的内容只是 1 万亿字节的序列。硬件可以检索或更新任何一个字节。

但是，一个 1 万亿字节的列表本身并不是一种组织信息的有效方式。早期操作系统的设计者，如汤普森和里奇等，在操作系统中内置了一种将「文件」的概念编码在这些磁盘上的方法。文件是构成逻辑单元的 8 万亿字节的子集，文件系统支持为文件指定名称并将文件组织到层次化的目录中，这些目录也是被命名的。随着图形用户界面的出现，这些目录已被形象地称为「文件夹」。当然，在物理世界中，一个文件夹中又包含许多文件夹会令人相当尴尬。

我的主要观察是，计算机硬件中没有提供文件的概念以及将文件组织到目录中的方法，而以操作系统呈现的软件提供了这个概念。

实现文件系统的软件相当聪明，它甚至不要求文件的内容在存储器中是连续性的。从而，文件的字节可以散布在整个磁盘上。操作系统软件能够跟踪哪些字节属于哪个文件，以及该文件在逻辑上包含在哪个目录中。

一旦有了要使用的文件系统，你就不用再担心数据是如何存储在磁盘上的了。你可以将该文件作为一个概念单元来访问。

### 5.5 Libraries, Languages, and Dialects

Millions of lines of code get translated into millions of zeros and ones that coerce billions of transistors to regulate the sloshing of who-knows-how-many electrons. This is starting to sound like Carl Sagan, whose signature lines involving「billions and billions」frequented his PBS television series Cosmos: A Personal Voyage in the 1980s. Sagan was talking about stars and galaxies and often emphasized the incomprehensible range of possibilities, including extraterrestrial life, that such numbers imply.

Digital technology seems to have hit a threshold where the possibilities are limited more by the human imagination than by physical constraints imposed on us by the world. What can be accomplished by software far exceeds what we accomplish today, even without further technological improvements. Software has become a digital medium for creativity. I will explore this issue in more detail in chapter 6 , and what we cannot do with software in chapter 8 , but for now let's just focus on how to manage the vastness of the possibilities.

Modern programming languages do, as Brooks claimed, mitigate a great deal of accidental complexity, but not enough to build really interesting systems like Wikipedia. Just as digital machine designs are augmented with standard cell and IP libraries, languages are augmented with component libraries and entire subsystems. As of this writing (August 2016), the Java language, Standard Edition version 8, has 4,240 software components built in for use by software designers. A software engineer will use these components in much the same way that a hardware engineer will use standard cells or an architect premanufactured components such as windows and doors.

Such a library of components becomes like a rich vocabulary, jazzing up the expressiveness of the language. Computer scientists do not usually consider such a library to be part of the language but rather something living and evolving apart from the language. But the library could well have far greater impact on the productivity and creativity of designers than the language. The mechanisms and conventions by which components in the library interact become, in effect, at least a dialect and sometimes even a new language. It is difficult to read a program if you are not familiar with the components it is using, even if you are fluent in its language.

Consider another widely used programming language for web applications, JavaScript, originally developed in 10 days in May 1995 by Brendan Eich. At the time, Eich was working for Netscape, one of the first companies to try to capitalize on the World Wide Web. Netscape was founded as Mosaic Communications Corporation in 1994 by Jim Clark and Marc Andreessen but eventually lost the browser wars to Microsoft and disappeared. Netscape's browser eventually morphed into the widely used, open-source, community-developed Firefox browser.

JavaScript, unlike PHP, is designed to run in the browser rather than in the server. This means that if you access a web page from your laptop or smartphone, and the web page includes a JavaScript program, that program runs on your laptop computer or your smartphone not on the server computer hosting the web page. Many of the web pages you visit routinely include a JavaScript program. Like PHP, the design of the JavaScript language exhibits interesting idiosyncrasies that reflect personal aesthetic decisions made by the original author.

The vast majority of the most widely used websites make extensive use of JavaScript. However, it is difficult to design beautiful and sophisticated web pages with JavaScript alone. Web designers leverage an ecosystem with thousands of「modules」available to designers. Many of these are open-source modules collectively developed by the community, much the way a Wikipedia page is collectively developed.

One widely used JavaScript module for creating sophisticated web pages is jQuery, originally created by John Resig. If you are fluent in JavaScript but do not know anything about the jQuery module, then programs that use it will be unreadable to you. Indulge me to illustrate this.

The JavaScript language, unlike most other programming languages, allows variable names to begin with the dollar sign character, $. The jQuery module defines a single global variable that it calls simply $. That is, the name of the variable is a single character, the dollar sign. This variable gets widely used in programs. To those unfamiliar with this idiom, the program looks cryptic, as a text written in the cyrillic alphabet looks to an English speaker. But the dialect is much richer than implied by just this idiom. Consider the following short JavaScript program:

```
$(document).ready(function(){

$("#target").text("Hello World");

});
```

If you are fluent in the JavaScript language but unfamiliar with the jQuery module and the modules provided by today's browsers, then this program is completely unreadable. It makes as much sense as the following does to someone fluent in English: [4]

Twas brillig, and the slithy toves

Did gyre and gimble in the wabe

Like this poem, the JavaScript program's verse is vaguely familiar but oddly incomprehensible to the JavaScript programmer.

I will spare you the details, but the prior JavaScript program can be used together with an HTML file and a style sheet to create the rather trivial web page shown in figure 5.6 . HTML, for HyperText Markup Language, is a completely different language, originally developed in 1980 by Tim Berners-Lee, creator of the World Wide Web, while he was a contractor at CERN, the European Organization for Nuclear Research (the acronym comes from the French name). The HTML that works with the previous JavaScript program to define the web page in figure 5.6 is as follows:

Figure 5.6

Web page using three languages and one dialect to specify.

```
<!DOCTYPE html>

<html>

<body>

<div id="target"></div>

</body>

</html>
```

Notice the idiosyncratic use of symbols < , > , and / , which were borrowed by Berners-Lee from a documentation format being used internally at CERN at the time.

HTML is universally used today to specify the contents of web pages, along with yet another language called CSS, for Cascading Style Sheets, first proposed in 1994 by Håkon Wium Lie, who was working with Berners-Lee at CERN. To use the previous JavaScript program, HTML is used to define the web page layout, and CSS is used to define the styles used to render the page. For example, if we include the following CSS code:

```
#target {

color: red;

}
```

then the text「Hello World」will be rendered in red. Notice that the syntax of CSS is quite different from HTML, which is quite different from JavaScript.

The web page of figure 5.6 is constructed using three distinct languages, JavaScript, HTML, and CSS, and one dialect, jQuery, each idiosyncratic and designed largely by a single creative individual. This is perhaps not as culturally rich and diverse as, say, Jerusalem, but it is most certainly not just dispassionate, objective, soul-less technology. It has every element of human subjectivity and invention pervading it. And millions of people today use this particular combination of technologies to design sophisticated web pages.

Of course, we could create a web page like that in figure 5.6 using HTML alone, but there are good reasons for using this combination of technologies. Using JavaScript enables the web page to dynamically update the contents of the page, making it interact with the user. Using CSS separates visual presentation design elements from logical structure and functionality, modularizing the design better. Using jQuery mitigates the accidental complexity associated with the fact that web pages can take a long time (relative to computer speeds) to load from a server and provides convenient access to elements of the page.

Although these languages and dialects each originated with a single individual, all are now thriving open-source communities with hundreds of contributors. They have evolved into a form of collective wisdom, like Wikipedia, rather than individual wisdom, like the Encyclopedia Britannica.

The culture of these communities should make an interesting subject of study for a cultural anthropologist. Resig, for example, first introduced jQuery to the web development community at a conference called a BarCamp in 2006 in New York City. BarCamps might be characterized as the anarchists' conference, in that nobody and everybody organizes the conference. Unlike most professional conferences, which will have a prepublished agenda with all events and presentations defined by an organizing committee, BarCamp participants self-organize using the web, whiteboards, and Post-It notes.

The license history of jQuery also reflects an ongoing passionate debate about the nature of open-source software. It was originally released using a GPL-style license as promoted by Stallman (specifically the Creative Commons CC BY-SA 2.5 license) but was later released under a less restrictive Berkeley-style license called the MIT license.

But I digress again (it is hard to avoid… the background stories are really quite interesting). Let's return to the subject of how to manage the vastness of possibilities that software offers. Software technologies emerge chaotically in a Darwinian ecosystem of ideas. Like a real Darwinian ecosystem, not everyone will agree on what makes one idea more「fit」than another idea, and survival depends more on the ability to propagate than on technical fitness. Promiscuity, personality, money, and culture have enormous, incomprehensible effects.

One approach to understanding this problem is the anthropologists' approach, which is to study the culture as it emerges and attempt to extract wisdom from that study. Just as an anthropologist might use the evolution of natural language as a key part of that study, a software anthropologist might use the evolution of programming languages, with idioms, dialects, and clichés.

One pioneering software anthropology effort was carried out by Erich Gamma, Richard Helm, Ralph Johnson, and John Vlissides in their book on design patterns (Gamma et al., 1994). Widely known as the「gang of four,」these authors attempt to categorize a variety of widely used patterns and idioms in software construction. They credit Christopher Alexander, architect, for inspiring their approach. Alexander proposed a pattern language for buildings and cities, and they translated this approach to software. In a testament to the difficulty of this task, in their preface, the gang of four state:

A word of warning and encouragement: Don't worry if you don't understand this book completely on the first reading. We didn't understand it all on the first writing!

I probably should have included a similar statement in the preface to my book.

The cultural nature of software may help explain why software endures better than hardware. Culture changes much more slowly than technology. The fact that software encodes its own paradigms can also contribute to its durability. For example, although APL is an extinct language, it is easy to find a web page that, using a similar HTML, JavaScript, and CSS combination, presents you with a customized APL keyboard and evaluates any APL programs that you type in.

The cacophony of languages that prevail today is reminiscent of immature scientific fields. Kuhn describes the scientific study of electricity in the first half of the eighteenth century before it acquired its first universally accepted paradigm:

During that period there were almost as many views about the nature of electricity as there were important electrical experimenters, men like Hauksbee, Gray, Desaguliers, Du Fay, Nollett, Watson, Franklin, and others. (Kuhn, 1962, p. 14)

But even at that time, Kuhn says, these competing paradigms shared a common metaparadigm:

All their numerous concepts of electricity had something in common— they were partially derived from one or another version of the mechanico-corpuscular philosophy that guided all scientific research of the day. (Kuhn, 1962, p. 14)

The languages used in web technology today, PHP, JavaScript, jQuery, CSS, and HTML, all have a common「mechanico-corpuscular」core, specifically the Turing-Church notion of computation, considered in chapter 8.

[4] From Through the Looking-Glass, and What Alice Found There , a novel by Lewis Carroll, 1871.

5.5 库、语言和方言

数百万行代码被转换成数百万个 0 和 1，又迫使数十亿的晶体管去调节多得无法计数的流动电子。这听起来很像卡尔·萨根的标志性台词。20 世纪 80 年代美国公共广播公司播出的电视连续剧《卡尔·萨根的宇宙》中，他标志性的台词总是涉及「数十亿」这样巨大数字。萨根经常会在谈到恒星和星系时，强调这些巨大的数字所暗示的不可思议的可能性范畴，其中包括外星生命。

数字技术似乎已经达到了一个极限，其未来的可能性更多地受到人类想象力的限制，而不是自然世界强加给我们的物理约束。即使没有进一步的技术改进，软件所能完成的事情也远远超出我们今天所能完成的。软件已经成为激发创造力的数字媒介。我将在第 6 章更详细地探讨这个问题，并在第 8 章讨论软件的局限性，但现在还是让我们集中讨论如何管理这些巨大的可能性吧。

正如布鲁克斯所言，现代编程语言确实极大地降低了偶然复杂性，但还不足以构建像维基百科般有趣的系统。就像用标准元件和 IP 库增强数字机器一样，组件库和整个子系统也增强了语言。在撰写本书之时（2016 年 8 月），Java 语言标准版第 8 版中已经有 4 240 个软件组件可供软件设计人员使用。软件工程师使用这些组件的方式与硬件工程师使用标准元件，或者建筑师使用预制组件（如窗、门等）的方式非常相似。

这样一个组件库就像一个丰富的词汇表，可以大大提高语言的表现力。计算机科学家通常并不将这样的库当作语言的一部分，而是认为它们是与语言分离存在且不断发展的。但是，组件库对计算机设计人员的生产力和创造力所产生的影响要比语言的大很多。实际上，库中组件相互交互的机制和约定，至少差不多已成为一种方言，有时甚至成为一种新的语言。如果你不熟悉一个程序所使用的那些组件，那么，你即使精通它的语言，也很难读懂它。

我们来考虑另一种被广泛使用的万维网应用编程语言 ——JavaScript。该语言最初是由布兰登·艾奇于 1995 年 5 月在 10 天之内开发的。当时，艾奇正在为美国网景公司工作，该公司是最早尝试利用万维网的公司之一。该公司由吉姆·克拉克和马克·安德森于 1994 年创立，原名为马赛克通信公司（Mosaic Communications Corporation）。该公司最终在激烈的网络大战中输给了微软，之后就销声匿迹了。网景公司的浏览器最终演变成后来被广泛使用的、开源且由社区开发的火狐浏览器。

JavaScript 与 PHP 不同，它被设计成在浏览器中运行，而不是在服务器中运行。这意味着，如果用笔记本或智能手机访问一个网页，而该页面包含一个 JavaScript 程序的话，那么该程序是在你的笔记本电脑或智能手机上运行的，而不是在托管该网页的服务器上运行的。你经常访问的许多网页都会包含一个 JavaScript 程序。与 PHP 语言一样，JavaScript 语言的设计同样表现出一些有趣的特性。这些特性反映了原作者的个人审美风格。

绝大多数使用最广泛的网站都在使用 JavaScript 语言。然而，仅使用 JavaScript 语言是很难设计出美观又复杂的网页的。实际上，网页设计人员利用一个包含了数千个可供设计人员使用的「模块」的生态系统。其中许多都是社区集体开发的开源模块，就像维基百科页面是由集体开发的一样。

一个广泛用于创建复杂网页的 JavaScript 模块是 jQuery，它最初由约翰·瑞森创建。如果你精通 JavaScript 语言却对 jQuery 模块一无所知，那么你将无法理解使用 jQuery 模块的程序。请允许我在这里简要地说明一下。

与其他大多数编程语言不同，JavaScript 语言允许变量名以美元符号 $ 开头。jQuery 模块定义了一个简单称为 $ 的全局变量。也就是说，该变量的名称是单个字符，即美元符号。这个变量在程序中被广泛使用。对于那些不熟悉这个习语的人来说，这个程序看上去很神秘，就像一个说英语的人见到用西里尔字母写的文本一样。但方言比这个习语所蕴含的内容要丰富得多。我们来看看以下这个简短的 JavaScript 程序：

```
$(document).ready(function(){

$("#target").text("Hel

l

o World");    });
```

如果你精通 JavaScript 语言，但一点儿也不熟悉 jQuery 模块以及当今浏览器所提供的模块，那么你是完全读不懂这个程序的。那种感觉就像某个精通英语的人读到了下面这段话一样：

怪兽，烤晚餐肉时辰粘柔的三不像怪兽（Twas brillig, and the slithy toves），

围着日晷草坪转悠钻地洞（Did gyre and gimble in the wabe）。

就像上面这首诗一样，这段 JavaScript 程序的诗对于 JavaScript 程序员来说是似曾相识却难以理解的。

我就不在这里花时间谈论细节了，但是上面的 JavaScript 程序可以与一个 HTML 文件和样式表一起使用，以创建图 5.6 所示的非常简单的网页。HTML 是英语 HyperText Markup Language 的首字母缩略词，意思是超文本标记语言，这是一种完全不同的语言，它是由万维网的创始人蒂姆·伯纳斯·李于 1980 年开发的，当时他是欧洲核子研究组织（CERN，该缩略语源自该组织的法语名称）的承包商。与上面给出的 JavaScript 程序一起用来定义图 5.6 所示网页的 HTML 代码如下所示：

图 5.6 使用三种语言和一种方言规定的网页。

```
<!DOCTYPE html>

<html>  <body>   <div id="tar

g

et"></div>  </body>  </html>
```

注意符号 <、> 和 / 的特殊用法，这些符号是伯纳斯·李从当时欧洲核子研究组织内部使用的文档格式中借用来的。

今天，HTML 普遍用于描述网页的内容，另外还有一种被称为 CSS 的语言，用于制作样式层叠表（Cascading Style Sheets）。该语言是 1994 年由哈肯·维姆莱首次提出的，他当时与伯纳斯·李一起在欧洲核子研究组织工作。为了使用如前所述的 JavaScript 语言，得先使用 HTML 定义网页的布局，CSS 则用于定义该页面的样式。例如，如果我们包含以下 CSS 代码：

```
#target {

color:

red;   }
```

那么文本「Hello world」将显示为红色。请注意，CSS 的语法与 HTML 的非常不同，后者与 JavaScript 的语法也有很大的不同。

图 5.6 所示的网页是由三种不同的语言（JavaScript、HTML 和 CSS）以及另外一种方言 jQuery 构建的。每一种语言都非常独特，主要由一个有创造力的人设计。也许它不像耶路撒冷那般具有丰富多样的文化，但也绝不只是一种冷静、客观、无灵魂的技术。它有着人类的主体性并充满了创造性。今天，数以百万计的人使用这种特殊的技术组合来设计复杂的网页。

当然，我们可以单独使用 HTML 创建一个如图 5.6 所示的网页页面，但是也有充分的理由使用这种技术组合。使用 JavaScript 语言可以使网页动态地更新页面内容，使其能够与用户进行交互。使用 CSS 能够将视觉上的设计元素从逻辑结构和功能中分离出来，这也会使设计实现更好的模块化。由于从服务器加载网页可能需要很长的时间（与计算机的运行速度有关），所以使用 jQuery 语言可以减少这个长时间过程所带来的偶然复杂性，并提供对页面元素的便捷访问。

虽然这些语言和方言最初都源于个人，但它们有成千上万的贡献者，这使得它们今天能够在开源社区中蓬勃发展。它们已经演变成一种集体智慧的形式，就像维基百科，而不是像《不列颠百科全书》那样的个体智慧。

这些社区的文化应该能够成为文化人类学家研究的有趣课题。例如，2006 年在纽约召开的一次名为「BarCamp」的会议上，瑞森首次在万维网开发社区介绍了 jQuery。BarCamp 会议具有无政府主义者聚会的特征，没有人组织这个会议，但所有人都参与组织。与大多数专业会议不同的是，这类会议有一个预先公布的议程，由一个组织委员会安排所有的活动和演讲，BarCamp 的与会者使用网络、白板和便利贴自行组织会议。

jQuery 获得许可的历史也反映了一场关于开源软件本质的激烈争论。它最初使用斯托曼倡导的 GPL 风格许可进行发布（特别是知识共享 CC BY-SA2.5 许可），但后来才在限制更少的伯克利式（Berkeley-style）许可下发布，该许可也被称作 MIT 许可。

非常抱歉，我似乎又离题了（实际上这有些难以避免，因为这些背景故事真的很有趣）。让我们回到如何管理软件所提供的巨大可能性这一主题上吧。在达尔文思想生态中，软件技术的出现有些混乱。就如同一个真正的达尔文生态系统一样，并不是每个人都同意是某些因素让一个想法比另一个更「适合」，生存更依赖于传播能力而不是技术的适合程度。混杂、个性、资本以及文化等都有着不可思议的巨大影响。

有一种人类学家的方法可以帮助我们理解这个问题，换言之，在文化出现时就对其进行研究，并试图从中汲取智慧。正如人类学家可能将自然语言的演化作为这项研究的关键部分一样，软件人类学家可能会使用编程语言的演化，包括各种习语、方言和陈词滥调。

埃里克·伽玛、理查德·赫尔姆、拉尔夫·约翰逊和约翰·威利斯迪斯在他们共同撰写的《设计模式：可复用面向对象软件的基础》一书中进行了软件人类学的一项开创性工作（伽玛等人，1994）。他们被业内人士称为「四人组」。他们试图对软件构造中广泛使用的各种模式和习语进行分类。他们声称是建筑师克里斯托弗·亚历山大启发了他们的方法。建筑师亚历山大提出了一种关于建筑物和城市设计的模式语言。他们将亚历山大的这种方法转换至软件方面。为了证明这项任务的艰巨性，在该书的序言中，四位作者就这项任务的艰巨性做出如下陈述：

给你一个警告和鼓励：如果你在第一次阅读时发现不能完全理解这本书，那么，请不要担心。因为我们在第一次写的时候也没有完全理解！

我也许应该在我这本书的前言里加上类似的陈述。

软件的文化特性可能有助于解释为什么软件比硬件具有更耐久的生命力。文化的变迁远比技术的发展要缓慢得多。软件编码其自身的范式这一事实也有助于它的耐久性。例如，虽然 APL 是一种已被淘汰的编程语言，但是很容易找到一个使用类似于 HTML、JavaScript 和 CSS 组合的网页，这样的网页能为你提供一个定制的 APL 键盘，并能够处理你所输入的任何 APL 程序。

当今这些编程语言的不和谐现象让人想起了不成熟的科学领域。库恩描述了 18 世纪上半叶对电的科学研究，那时尚未形成第一个普遍被接受的范式：

在那个时期，关于电的本质的观点与当时开展电的实验的重要人员一样多，如霍克斯比、格雷、德萨吉利埃、杜菲、诺莱、沃森、富兰克林等人。（库恩，1962:14）

但即使在那个时候，库恩也认为，这些相互竞争的范式有一个共同的元范式：

这些范式对电的所有概念都有某些共同之处 —— 它们都部分地源于当时指导所有科学研究的机械粒子哲学的一个或另一个版本。（库恩，1962:14）

现在网络技术中使用的语言，如 PHP、JavaScript、jQuery、CSS 和 HTML 等，都有一个共同的「机械粒子」核心，特别是我们要在第 8 章中讨论的丘奇 — 图灵计算概念。

### 5.6 The Cloud

So far we have been talking about individual computers and the software that runs on them. But many of the most interesting uses of computers today are far too big for a single computer to handle. These applications run on computers housed in「server farms,」large facilities that can consume up to tens of megawatts of electricity. It is hard to get exact numbers, but various estimates indicate that, as of this writing (2016), Microsoft, Google, and Amazon have on the order of a million servers each in their data centers. Many companies operate perhaps an order of magnitude fewer servers, including Facebook, Yahoo, HP, IBM, eBay, Intel, Rackspace, and Akamai. Each server may contain tens of「cores,」individual computers that share certain resources among them, such as memory and network interfaces.

Taken together, this means that there are single software-based services, such as Facebook and Google search, that are running simultaneously on as many as millions of individual computers. These applications make extensive use of PHP, JavaScript, and more general-purpose programming languages like Java, discussed in the previous sections. But they overlay on these languages yet higher level paradigms to handle the distribution of tasks and data across many machines. Languages with curious names such as Pig Latin and frameworks such as ZooKeeper, Sqoop, and Oozie encode the design styles of these paradigms.

For example, Apache Hadoop is an open-source framework that has at its core a distributed file system for spreading data across servers and a realization of a pattern called MapReduce for delegating to servers chunks of a data processing operation. MapReduce was invented in 2004 (and patented) by Jeffrey Dean and Sanjay Ghemawat of Google, although as usual for inventions, the actual novelty is in dispute. MapReduce is strikingly similar to patterns that had existed previously in older software for distributed computing such as MPI (the Message Passing Interface) and database systems.

Hadoop forms an ecosystem of patterns and tools for the design of multiserver applications. Like many of its competitors, Hadoop assumes that hardware failures are common because with millions of servers failure will occur. Hardware gets virtualized so that applications can move from machine to machine with minimal disruption. An application may even move from one machine to another machine of an entirely different type, emphasizing the disconnect between the software and the physics of the hardware.

Server applications are often called on to handle truly vast amounts of data, much more than any single computer could handle at once. Consider Google search, for example, which returns in less than a second the results of searching billions of web pages and handles on the order of 40,000 searches per second (Pappas, 2016). How does Google do that? Storing the contents of the web on a computer and searching it each time a query comes in clearly will not work. There is just too much data.

The key to a web search is collecting and indexing the data ahead of time. A major part of the work of Google's servers is not actually responding to search requests but rather reading, indexing, and sorting web pages ahead of time and creating a massive distributed data structure. A「web crawler」finds a website, collects the words on it, and follows the links to other websites, all the while keeping track of link relationships between web pages. The collected data, including statistical features such as word proximity, word ordering, frequency of links, and link associations, are used to build a「memory」of the web that allows for quick recall.

In his book Turing's Cathedral , George Dyson draws a thought-provoking analogy:

The behavior of a search engine, when not actively conducting a search, resembles the activity of a dreaming brain. Associations made while「awake」are retraced and reinforced, while memories gathered while「awake」are replicated and moved around.

· · ·

In 1950, Turing asked us to「consider the question, ‘Can machines think?' 」Machines will dream first. (Dyson, 2012, p. 311)

Indeed, the human brain apparently uses sleep and dreaming to organize information. Does this mean that Google's million-server machines are a nascent intelligence in the process of building some form of cognition by organizing information about the world? I defer this difficult question until chapter 9 , where I confront the idea of a digital psyche.

There is quite a bit of sophistication (and secrecy) about how a search works exactly. But one thing is sure: when you perform a Google search, it is not a single computer that replies. Instead, your search is routed through a string of servers depending on the keywords and language patterns in the search so that the search query goes to where the organized data resides. No single server can store and access more than a tiny fraction of the「knowledge」that the servers build while dreaming, so no single computer can reasonably respond to an arbitrary search. The server that first sees your query will be random, based on which servers are available, but after that the query will be forwarded to servers based on keywords and patterns in your search.

Let's consider how much data is involved. First, the amount of data is constantly increasing. The content in the web grows, of course, but more interestingly (and disturbingly, like Orwell's Big Brother), a search engine will watch your every move and use correlations with your previous searches, your location, and even a learned model of your preferences to improve the search results (and to improve the likelihood that advertisements presented to you will be relevant to you). When you read and shop online, you are being read back. The data gathered gets fed into the dream machine to be organized.

It is hard to get solid numbers, but some 2016 estimates suggest that Google may be storing on the order of exabytes of data. One exabyte is 10 18 or

1,000,000,000,000,000,000.

That's a lot of data, and potentially all of it can be used to build models of the world, using, for example, the machine learning techniques considered in chapter 11 .

The web and users of the web provide a wealth of data for these servers to learn from, but that is not the only source. Software providers are systematically trying to shift all of our computing activity from our personal computers to servers in「the cloud.」This changes the business model of software from product to service but, more important, gives the software vendors more direct access to your data, to data about your use of their software, and to data about you.

Even legacy data is being uploaded to these servers. Printed material such as books and journals are being steadily digitized to be added to the online arsenal of information. In 2002, Google started a project to scan every book ever published. Dyson's description of this project is quite extraordinary:

At the time of my visit, my hosts [at Google] had just begun a project to digitize all the books in the world. Objections were immediately raised, not by the books' authors, who were mostly long dead, but by book lovers who feared that the books might somehow lose their souls. Others objected that copyright would be infringed. Books are strings of code. But they have mysterious properties like strings of DNA. Somehow the author captures a fragment of the universe, unravels it into a one-dimensional sequence, squeezes it through a keyhole, and hopes that a three-dimensional vision emerges in the reader's mind. The translation is never exact. In their combination of mortal, physical embodiment with immortal, disembodied knowledge, books have a life of their own. Are we scanning the books and leaving behind the souls? Or are we scanning the souls and leaving behind the books?

「We are not scanning all those books to be read by people,」an engineer revealed to me after lunch.「We are scanning them to be read by an [artificial intelligence].」(Dyson, 2012, p. 312)

Why stop at books? In 2006, Google bought YouTube for $1.6 billion. Because YouTube is a video-sharing website, it provides a truly vast arsenal of data about the world. In 2014, YouTube said that 300 hours of new videos were uploaded to the site each minute, on average. Although the technology for extracting useful information from video and images lags behind that for extracting information from text, we can be sure that the technology will improve. The machines will start to dream in color. As data from sensors comes online, for example, from connected cars, thermostats, and the whole Internet of Things world, what more can the machines learn? I examine this question in the next chapter.

5.6 云

到目前为止，我们一直都在谈论个人计算机及其运行的软件。然而，当今计算机有很多非常有趣的应用，这些应用远远超出一台计算机的处理能力。这些应用程序运行在「服务器集群」上，这些大型设施可以消耗高达几十兆瓦的电力。尽管很难得到确切的数据，但截至 2016 年我撰写这本书的时候，各种估计表明，微软、谷歌和亚马逊的数据中心大约有 100 万台服务器。许多公司运行的服务器数量可能要少一个数量级，例如脸书、雅虎、惠普、IBM、易贝、英特尔、Rackspace（一家全球领先的托管服务器及云计算提供商）和阿卡迈等。但是，每个服务器可能包含数十个「核」，即它们是共享诸如存储器和网络接口的一组独立的计算机。

总而言之，这意味着基于单个软件的一组服务（如脸书和谷歌搜索）能够同时运行在数百万台个人计算机上。这些应用程序普遍使用了 PHP、JavaScript 以及诸如 Java 等更为通用的编程语言，相关的这些内容已在前面的章节中讨论过。但是，它们覆盖了这些语言，并使用了更高层次的范式来处理任务和数据在许多机器上的分布。一些有着奇怪名字（如 Pig Latin）和框架（如 ZooKeeper、Sqoop 和 Oozie）的语言编码了这些范式的设计风格。

例如，Apache Hadoop 是一个开源框架，其核心是一个分布式文件系统，用于在服务器之间传输数据，同时，其实现了一个被称为 MapReduce 的模式，用于将一组数据处理操作的块委托给服务器。MapReduce 模式是由谷歌公司的杰弗里·迪安和桑贾伊·马沃特于 2004 年发明的（并获得了专利）。尽管与普通的发明一样，但其实际的新颖性仍然是具有争议的。MapReduce 与之前用于分布式计算的旧软件，如 MPI（消息传递接口），以及数据库系统中的模式惊人地相似。

Hadoop 形成了设计多服务器应用程序的模式和工具的生态系统。与它的诸多竞争对手一样，Hadoop 也假定硬件故障很常见，因为数以百万计的服务器中肯定会发生故障。由于硬件被虚拟化了，所以应用程序就可以从一台机器迁移到另一台机器，且会尽管少地影响程序执行。一个应用程序甚至可以从一台机器迁移到另一台类型完全不同的机器上，这实际上强调了软件与硬件之间的分离。

服务器应用程序经常被调用来处理真正的大规模数据，它们的能力要远远超过任何单台计算机一次可处理的数据量。以谷歌搜索引擎为例，它在不到 1 秒的时间内就可以返回对数十亿个网页的搜索结果，并以每秒 4 万次的速度进行处理（帕帕斯，2016）。那么，谷歌是如何做到这一点的呢？将网络内容存储在计算机上，并在查询请求每次到来时进行搜索，这种办法显然是不够的。这是因为要处理的数据实在是太多了。

网络搜索的关键是提前收集和索引数据。事实上，谷歌服务器的主要工作并不是真的去响应搜索请求，而是提前读取网页并进行索引和排序，同时创建一个庞大的分布式数据结构。一个「网络爬虫」找到一个网站，收集该网站上的关键词，并跟踪到其他网站的链接，同时跟踪网页之间的链接关系。收集到的数据包括了诸如单词接近度、单词排序、连接频率以及链接关联性等统计特性，它们被用来构建一个允许快速访问的网络「存储器」。

乔治·戴森在他所著的《图灵的大教堂》一书中，做了一个发人深省的类比：

在不主动进行搜索时，搜索引擎的行为就类似于做梦时大脑的活动。「清醒」时所产生的联想会被不断地追溯和强化，而「清醒」时收集的记忆会被复制和移动。

……

1950 年，图灵就让我们「思考这样一个问题，‘机器能思考吗'」，机器得先会做梦。（戴森，2012:311）

事实上，人类的大脑显然是通过睡眠和做梦来组织信息的。这是否意味着谷歌的百万台服务器是一种新生的智能，它们正在通过组织有关世界的信息来构建某种形式的认知？我把这个棘手的问题留到第 9 章再讨论，第 9 章将会涉及数字心灵的概念。

一次搜索到底是如何工作的，关于这一点还是有点儿复杂（和神秘）的。但有一件事是可以肯定的：当你使用谷歌进行搜索时，给出响应的肯定不是一台计算机。相反，你的搜索将根据搜索中的关键字和语言模式通过一连串服务器进行路由，这样搜索查询就可以到达有组织的数据所在的位置。没有任何一台服务器能够存储和访问服务器在做梦时所建立「知识」的哪怕是一小部分，因此，可以说没有一台计算机能够对任意的搜索做出合理的响应。首先接收到你的查询请求的服务器将是随机的，这主要取决于哪些服务器可用，但在此之后，这条查询请求将被基于你所搜索的关键字和模式转发到其他服务器上。

让我们来考虑一下到底会涉及多少数据。首先，数据量在不断增加。当然，网络上的内容不断增长，但更有趣（且更令人不安，就像奥威尔的哥哥那样）的是，搜索引擎将会关注你的一举一动，并使用与你之前搜索过的内容、你当前所在位置的关联性，甚至你的偏好的学习模型来改善搜索结果（同时，提高向你推送和你有关的广告的可能性）。当你在网上阅读和购物时，你的一举一动都被记录下来。这些被收集的数据会被输入将要被组织在一起做梦的机器中。

虽然很难得到确切的数据，但 2016 年的一些评估表明，谷歌可能存储了艾字节级的数据。1 艾字节是 1018 字节或 1 000 000 000 000 000 000。

这是规模巨大的数据，而且很可能所有的数据都可被用来构建世界的模型，例如，使用第 11 章提到的机器学习技术。

网络和网络用户提供了丰富的数据供这些服务器学习，但这并不是唯一的来源。软件提供商正在系统地尝试将我们所有的计算活动从我们的个人计算机迁移到「云」中的服务器上。这将改变软件从产品转为服务的业务模型，但更为重要的是，软件供应商可以更直接地访问你的数据、关于你使用其软件的数据以及关于你的数据。

甚至所有的遗留数据也都被上传到这些服务器上。诸如书籍和期刊等的印刷材料正在稳步走向数字化，从而可以被加入在线的信息库。2002 年，谷歌公司开始了一个扫描所有已出版图书的宏大项目。戴森对这个项目的描述非常特别：

在我访问的那段时间，我的雇主（在谷歌的）刚刚开始了一个将世界上所有书数字化的项目。反对的声音立即就出现了。反对之声不是来自那些早已辞世的书籍作者，而是来自广大的书迷。他们提出了强烈的反对意见，担心一旦数字化就会使这些书失去灵魂。还有一些人则说这会侵犯书的版权。书不过是一串代码，但是它们带有某些神秘的特性，就像基因序列一样。书的作者以某种方式捕捉到了宇宙的一个片段，并将其展开成一个一维的序列，然后把它挤进一个钥匙孔并希望在读者的脑海中呈现出一个三维的景象。当然，这种转换从来都不是百分百准确的。书籍将平凡的有形化身与不朽的无形知识结合在一起，从而拥有了它们自己的生命。我们是要扫描书本，并将其灵魂留下吗？或者我们是要扫描灵魂而把书本抛于脑后？

「我们扫描所有这些书，并不是让人们去阅读。」一位工程师在午餐后对我说，「我们扫描它们是为了让人工智能来阅读的。」（戴森，2012:312）

为什么止步于书籍？谷歌公司是不会仅仅满足于扫描图书的。2006 年，谷歌公司以 16 亿美元的巨资收购了 YouTube。如我们所知，YouTube 是一个视频分享网站，它提供了关于世界的海量数据。2014 年，YouTube 声称平均每分钟会有时长 300 小时的新视频上传到其网站。虽然从视频和图像中提取有用信息的技术落后于从文本中提取信息的技术，但我们可以肯定，该类技术将会得到改进。机器将开始做彩色的梦。随着在线获取传感器数据，例如来自联网汽车、恒温器以及整个物联网世界的数据技术的发展，机器还将学到什么呢？我将在下一章讨论这个问题。

## 0601. Evolution and Revolution

· · · in which I argue that technology revolutions differ from scientific revolutions in that paradigms appear and disappear much more rapidly; new paradigms do not necessarily replace old ones; and the crises that trigger new paradigms do not arise so much from the discovery of anomalies but rather from increasing complexity and technology-driven opportunity.

0601 进化与革命

我认为技术革命与科学革命的区别在于，其范式出现和消失的速度要快得多；同时，新范式不一定要取代旧范式；引发新范式的危机并不是因为异常现象的发现，而是因为复杂性以及由技术驱动的机遇在持续增加。

### 6.1 Normal Engineering

In his Structure of Scientific Revolutions , Thomas Kuhn calls the research that is firmly grounded in an established paradigm「normal science.」The LIGO gravitational wave detector discussed in chapter 1 , with its firm grounding in Einstein's general theory of relativity, despite its monumental scale, qualifies under Kuhn's scheme as normal science.

Kuhn asserts that adherence to a paradigm is essential to normal science:

Without commitment to a paradigm there could be no normal science. (Kuhn, 1962, p. 100)

He calls normal science「mopping up operations」and「puzzle solving」and asserts that this is what engages most scientists throughout their careers. The paradigms within which they operate provide the framework for these operations.

We can similarly define「normal engineering」to be the process of design and optimization within an established methodology and an established set of rules. Given a requirement for, say, a web page with some interactive features, a software engineer is hired to design the HTML and JavaScript code for the web page. This sort of engineering is easily and effectively outsourced, and a whole industry has emerged in India to carry out such normal engineering.

Although normal engineering is routine, it nevertheless demands skill and benefits from talent. When designing a web page, for example, aesthetics are often as important as functionality. Malcolm McCullough, in his 1996 book Abstracting Craft , focuses on this aspect of normal engineering, observing that digital media, including the technology for creating web pages and other digital artifacts, offer a whole new form of craftsmanship. Unlike the physical crafts of, say, pottery and woodworking, this form of craft works with abstract media, the zeros and ones of computing. But like the physical crafts, abstract craft admits mastery and aesthetics.

Although normal science certainly admits mastery, it is a real stretch to say it admits aesthetics. A scientist may object, observing correctly that personal taste is involved in the selection of experiments to perform, the manner in which they are performed, and the way the results are presented to the scientific community. I have to agree that there is aesthetics in all of this, but the end product of normal science is not an artifact subject to aesthetic judgment. It is, for example, the LIGO validation of Einstein's prediction of gravitational waves. The goal of such validation is not to please the human senses or to stir the soul. It is to reaffirm the Platonic truth of a prevailing paradigm in physics. Kuhn asserts that the object of normal science「is to solve a puzzle for whose very existence the validity of the paradigm must be assumed. Failure to achieve a solution discredits only the scientist and not the theory」(Kuhn, 1962, p. 80). How indeed would LIGO be viewed if it failed to detect any gravitational waves? Would it have undermined Einstein's theory of relativity? Probably not.

A failure to create an effective or successful interactive web page would discredit the software engineers assigned to the task. It would not undermine the paradigm of the web or of the HTML and JavaScript languages. Success in such a project requires some technology, but even more it requires craftsmanship.

Craftsmanship is human skill creating artifacts that did not previously exist. But the craftsmanship in normal engineering is distinctly different from innovation. A beautiful web page that is a pleasure to interact with is not necessarily innovative and almost certainly does not constitute an invention, just as normal science does not seek novelties:

Normal science does not aim at novelties of fact or theory and, when successful, finds none. (Kuhn, 1962, p. 52)

Craftsmanship and aesthetics can have as much or more impact on the success of an engineering task as innovation. One of the factors in the success of the iPhone is undoubtedly the aesthetic physical design, credited to Jonathan Ive. Amazingly, Apple managed to patent this design, stamping it as an invention. The patent contains one claim, the entire text of which is,「The ornamental design for a portable display device, as shown and described」(Akana et al., 2012). In my opinion, this is an abomination that goes against any reasonable notion of what constitutes an invention. The U.S. Patent and Trademark Office should be ashamed of itself.

Of course, not all of engineering admits aesthetics easily. The design of a sewage handling system for a building usually has only one aesthetic goal: make it invisible. Even so, occasionally even plumbing is used as an aesthetic medium. Witness the Pompidou Center in Paris, which exposes its guts in a bold and aesthetically driven reversal of conventional practice in architecture (see figure 6.1 ). But with digital media, aesthetic elements are much more common than in other branches of engineering.

As with any craft, mastery of digital media can have an enormous effect on the outcome of a project. But mastery of a craft is quite orthogonal to innovation. Innovation can occur within the framework of an established paradigm, of course. But a truly game-changing innovation, such as the stored-program computer credited to von Neumann or the World Wide Web credited to Berners-Lee, is more like Kuhn's paradigm shifts than like practice within a paradigm. These innovations change the practice of normal engineering for many successor engineers. The question I will address next is what brings about these paradigm shifts. It turns out that the situation in engineering is quite different from that in science.

Figure 6.1

The Pompidou Center in Paris exposes the building's mechanical functions for aesthetic reasons. The building was designed by Richard Rogers, Renzo Piano, Gianfranco Franchini, and their teams, and opened in 1977. [Image licensed under CC BY-SA 3.0 by「Reinraum.」From https://en.wikipedia.org/w/index.php?curid=37297406 .]

6.1 常态工程

在《科学革命的结构》一书中，托马斯·库恩称建立在既定范式基础上的科学研究是「常态科学」。我们在第 1 章讨论过的激光干涉引力波天文台探测器研究项目是建立在爱因斯坦广义相对论的坚实理论基础之上的，尽管该项科学研究规模巨大，但在库恩的理论体系下，仍然是一门常态科学。

库恩认为，坚持一种范式对于常态科学而言是必不可少的：

如果没有对一种范式的保证，就没有常态科学。（库恩，1962：100）

他称常态科学为「清扫行动」和「解除迷惑」，并断言这正是大多数科学家在其整个职业生涯中所从事的工作。他们所采用的范式为这些活动提供了指导框架。

我们可以类似地将「常态工程」定义为在一套既定的方法和一套既定的规则中进行设计和优化的过程。例如，如果一个网页需要具备某些交互功能，就应聘请一名软件工程师为该网页设计 HTML 和 JavaScript 代码。这类工程可以被很容易且有效地外包出去，例如，印度就形成了一个完整的行业从事这种常态工程。

虽然常态工程大都是常规工作，但它还是需要技能和人才的。例如，在设计网页时，它的审美性常常和它的功能性一样重要。马尔科姆·麦卡洛在他 1996 年出版的名为《抽象化工艺》（Abstracting Craft）的书中，重点阐释了常态工程这一主题。他观察到数字媒介，包括创建网页和其他数字产品的技术，提供了一种全新的工艺形式。例如，与陶艺和木工等的物理工艺不同，这种全新的工艺形式使用了 0 和 1 的计算这种抽象媒介。但是就像物理工艺一样，抽象工艺也是精湛并具有审美性的。

虽然常态科学肯定会考虑工艺的精湛性，但如果说它也会考虑美学的问题可能就有些夸大其词了。某位科学家可能会对此提出异议，他正确地观察到个人品位在选择要进行的实验、进行实验的方式以及向科学界呈现实验结果的方式中都有反映。我不得不承认，所有这一切都是有美学价值的，但是我们不能说常态科学的最终产物就是受美学判断支配的人工制品。例如，激光干涉引力波天文台探测器研究项目验证了爱因斯坦对引力波的预测。这种验证不是为了取悦人类的感官，也不是为了激发人类的灵感，而是为了重申物理学中主流范式的柏拉图式真理。库恩断言，常态科学的目标在于，「解决难题，就其存在而言，必须假定这个范式是有效的。未能找到解决办法只会使科学家蒙羞，而科学理论并不会受到什么影响」（库恩，1962:80）。如果激光干涉引力波天文台探测器研究项目探测不到任何引力波，那么人们将如何看待它？这会破坏爱因斯坦的相对论吗？我想大概不会。

如果不能成功地创建一个有效的交互式网页，就会使负责该任务的软件工程师名誉扫地。但是，这不会破坏万维网或 HTML 和 JavaScript 语言的范式。然而，要成功地完成这样一个任务需要一些技术，但更需要工艺。

工艺指的是人类创造以前不存在的人工制品的技能。但是，常态工程的工艺与创新有着明显的不同。一个出色的网页会让用户产生互动的乐趣，但它并不一定具有创新性，而且几乎肯定不构成一项发明，这与常态科学并不追求新奇性的道理是一样的：

2『这里看到了对工艺的定义，跟自己的本行业相关了，做一张术语卡片。（2021-10-24）』—— 已完成

常态科学不以新奇的事实或理论为目标。而且，当取得成功的时候，也根本找不出任何新奇的东西。（库恩，1962：52）

工艺、美学对工程任务能否成功的影响与创新一样大，甚至是更大。苹果手机成功的一个主要因素无疑是其充满美学的外观设计，这都要归功于乔纳森·伊夫。令人感到惊讶的是，苹果公司居然设法为这一设计申请了专利，并将其标榜为一项发明。该专利包含一个声明，全文是「如图所示和描述的便携式显示装置的外观设计」（赤名等人，2012）。在我看来，这是一个令人讨厌的声明，它有悖于任何关于发明的合理概念。美国专利和商标局应该为批准该项专利的行为感到羞愧。

当然，并非所有的工程都能轻易地接纳美学。例如，建筑物中污水处理系统的设计通常只会考虑一个美学目标：让该系统隐形。即使如此，有时甚至连管道也会被用作美学的媒介。看看巴黎蓬皮杜艺术中心那些大胆的、唯美主义的建筑设计风格吧，它们都大幅扭转了人们对传统建筑的刻板印象（见图 6.1）。但是随着数字媒介的产生，美学元素在工程学的其他分支领域里变得更为常见了。

图 6.1 出于美学原因，巴黎蓬皮杜艺术中心展示了建筑的机械功能。这座建筑由理查德·罗杰斯、伦佐·皮亚诺、吉安方克·法兰锲尼和他们的团队设计，并于 1977 年向公众开放。（图片由瑞恩拉姆提供，并获得 CC BY-SA 3.0 授权。图片来自 https://en.wikipara.org/w/index.php?curid=37297406。）

与任何工艺一样，对数字媒介的掌握也会对工程项目的结果产生巨大影响。然而，掌握一种工艺与技术上的创新是完全不相关的。

当然，创新可以在既定范式的框架内发生。但真正改变游戏规则的创新，如冯·诺依曼的存储程序式计算机或者伯纳斯·李的万维网等，更像是库恩所述的范式转换，而不是仅仅在一个范式中的实践。这些创新改变了许多后来的工程师在常态工程中的实践活动。我接下来要讨论的问题是，是什么导致了这些范式的转换。事实证明，工程领域的范式转换与科学领域的情况大不相同。

### 6.2 Crisis and Failure

Kuhn claims that scientific revolutions occur only after an accretion of anomalous observations made under the old paradigm creates a crisis and only when a new paradigm emerges to replace the old. These are not the forces that drive paradigm shifts in technology.

Paradigm shifts in technology occur for at least three reasons. First, the complexity of systems being engineered overwhelms our human ability to understand or control these systems. For example, programming languages emerged because writing correct machine or assembly code became impossibly difficult. Second, it becomes possible to do something that nobody imagined was possible before. For example, Google and other search engines enable nearly instantaneous search over everything humans have ever published. Third, complex social, political, and business forces can drive paradigm shifts in technology. Military needs, for example, essentially created aviation, nuclear weapons, and many other technologies, and military budgets provided most of the funding for the early development of computing.

Figure 6.2

In scientific revolutions, according to Kuhn, new paradigms typically replace old paradigms. In technology revolutions, new paradigms may be built on top of old paradigms, not replacing them so much as hiding them behind a layer of abstraction. (Photos of a sign with the likeness of Charles Darwin on Santa Cruz Island in the Galapagos.)

In section 3.2 , Complexity Simplified , I pointed out that one source of complexity is a large number of parts. Even simple parts with simple functions, such as transistors acting as switches, when there are enough of them, enable enormously complex functionality. Digital technology, rooted in these transistors, has been an enormous source of complexity-driven paradigm shifts for several decades.

In 1965, Gordon Moore, cofounder of Intel, [1] famously predicted that the number of components (transistors, resistors, diodes, and capacitors) in an integrated circuit would double every year for at least the next ten years. In 1975, he revised the forecast rate to double approximately every two years. This prediction, widely known as「Moore's law,」has been a guiding principle for the semiconductor industry ever since.

In practice, until around 2015, Moore's prediction held steady. The Intel 8080 was a single-chip microcomputer introduced in 1974 with approximately 4,400 transistors. According to Moore's law, therefore, a single-chip microcomputer in 2014 should contain 4,400 × 2 (2014−1974)/2 ≈ 4,610,000,000 transistors, which is remarkably close to the 5.56 billion transistors on the Intel Xeon Haswell-E5, introduced in 2014. Although the demise of Moore's law has been predicted many times, most industry observers seem to agree that as of 2015, it has finally significantly slowed.

This rapid acceleration of the capabilities of digital technology has created a steady stream of crises, where inevitably the models and mechanisms used to design and program systems repeatedly break down under the crush of additional capability. As far back as 1972, Edsger Dijkstra, wrote,

To put it quite bluntly: as long as there were no machines, programming was no problem at all; when we had a few weak computers, programming became a mild problem, and now we have gigantic computers, programming has become an equally gigantic problem. (Dijkstra, 1972)

And that was just 1972! If it was a gigantic problem then, then there is no word for what it is now.

Moore's law refers only to individual computers on individual silicon chips. Today, we find an extraordinary rise in the number of computing devices that are interconnected through networks. Around 1980, Robert Metcalfe, cofounder of 3Com and coinventor of Ethernet, the most widely used wired networking technology today, is said to have postulated what is now known as Metcalfe's law. This law states that the value of a network is proportional to the square of the number of compatible communicating devices on the network. So, for example, if a single isolated device is worth $1, then a network with 10 connected devices is worth

$1 × 10 2 = $100.

A network with 100 devices would be similarly worth $10,000, and with 1000 devices, $1,000,000. I'll let you calculate Metcalfe's assessment of the worth of the Internet today, which has roughly six billion connected devices.

And the number of connected devices is growing fast. Today, industry leaders breathlessly predict some 50 billion connected devices by 2020, due to the rise of the so-called Internet of Things (IoT). The IoT connects devices that are not first and foremost computers, such as thermostats, cars, door locks, climate control systems, and so on. As they give such predictions, you can almost see the visions of dollars dancing in their eyes.

Because value presumably follows from capability, I assume that Metcalfe would conclude that the capability of a network, not just the value, is also proportional to the square of the number of connected devices. Because complexity typically also follows from capability, we should not expect any slowing of crises over the next few years, even if Moore's law grinds to a halt. The crush of increasing complexity does not appear to be slowing.

In any technology, increasing complexity can create crises in two ways. First, designing reliable systems becomes harder. The tools and models that worked well at lower complexity strain until they break as the complexity increases. Second, perhaps as a consequence of the first, the likelihood that a design project will fail increases.

When I worked at Bell Labs in the early 1980s, a large project called AIS/Net 1000 intended to provide bridges between the disparate computing systems that existed at the time. At that time, interconnecting computers through networks was quite a new phenomenon, and as evidenced by Metcalfe's law, the value of such interconnections was recognized, at least by Metcalfe.

But these interconnections exposed many incompatibilities between the computer systems, particularly computer systems from different vendors. These systems had been designed to work in isolation. The binary bit patterns used to represent numbers and text, for example, were different. The order in which bits were arranged in memory differed. The protocols and speeds used to communicate differed. These differences meant that one computer often could not directly communicate with another, and even if it could, it would not interpret the bit patterns produced by the other correctly. In effect, each computer operated within its own paradigm, and the paradigms were incommensurable.

As computers became networked, these incompatibilities triggered a crisis. AIS/Net 1000 aimed to solve this problem by performing translations within the network, permitting the disparate paradigms to persist. When one computer sends a message to another, the message would be automatically translated during transport. Nobody would have to change how they did things, and AT&T would sell the glue that enabled interoperability. This was to be the Babel fish of networks. [2]

The project failed. AT&T wrote off more than $1 billion of development effort. It turns out that few customers were actually willing to pay for this service. Instead, the paradigms saw a Darwinian consolidation. Competing species were unable to coexist within the same ecosystem of networked computers.

Instead of a Babel fish, the Internet emerged. A key enabler for the Internet was the acceptance of the so-called Open Systems Interconnection (OSI) model. OSI is a layering of modeling paradigms, sketched in figure 6.3 . Like the layers in figure 3.3 , each level of the OSI model provides a conceptual framework for communication between computers. The lowest level, called the physical layer, is concerned with transporting sequences of bits from one place to another without concern for what the bits mean. The layers above this assign more meaning to the bits. For example, layer 6, the presentation layer, may treat a collection of, say, one million bits as an encoding of an image in a particular format, such as the standardized JPEG format widely used in digital cameras and on the web.

Kuhn talks about paradigms being incommensurable. In the OSI model, the terms「frame,」「packet,」「segment,」and「session」all refer to a finite collection of bits, but they all have different meanings at different levels. Understanding these different meanings is one of the most confusing parts about working with low-level networking software, in my experience. It is much easier to work at exactly one of these levels and not try to cross layers.

Calling the layers of the OSI model「paradigms」is perhaps a bit odd because they differ significantly from Kuhn's scientific paradigms. Like Kuhn's paradigms, they do provide a mental model for humans to understand how a system operates. For example, it is a different mental model to visualize one computer sending an image, a photograph, to another, versus visualizing one computer sending a stream of one million bits. But unlike Kuhn's paradigms, for these layers to work, their definition must be made absolutely precise. A misinterpretation of a single bit among one million bits may render an image unreadable. Kuhn's paradigms are much more robust; they can tolerate a certain amount of creative misunderstanding, which can sometimes form the engine for innovation or even paradigm shifts.

Figure 6.3 The OSI model for communication between computers.

It is not easy to make the OSI model layers precise. For computers on the Internet to reliably communicate, they all need to agree on precise meanings at every layer, down to the interpretations of each individual bit. The process of building the standards that codify this agreement can be a messy, political, and bureaucratic morass of conflicting national and business interests.

As a case in point, it may be helpful to understand how the OSI model came about. The OSI model is a joint effort of two standardization bodies, the International Organization for Standardization (ISO) and the Telecommunication Standardization Sector of the International Telecommunication Union (ITU-T, formerly CCITT), which had each separately developed similar models for communicating computers in the late 1970s. But similar models are not enough to get computers to communicate. The models have to be identical. Hence, these two bodies got together to publish a joint document, a process that no doubt involved considerable bickering over minutia.

To get a sense of all the competing interests that get involved, it may be helpful to understand how these standardization bodies are organized. The ISO is composed of representatives of various national standardization agencies from some 162 countries. The ITU-T, a United Nations agency, coordinates standards for telecommunications. In addition to representatives from many governments, these bodies include representatives from competing businesses, some of which will have already sunk considerable investments into the technologies being standardized. As a consequence, the battles that can emerge over standards development can be prolonged and painful, and the ensuing compromises can sometimes undermine the effectiveness of the resulting standards.

JPEG, one of the most commonly used encodings for photographs and a level-6 (presentation layer) standard in the OSI model, is an acronym for the Joint Photographic Experts Group, which created the standard. This group is a committee overlapping ISO/IEC JTC1 and ITU-T, the same organizations involved in the OSI model, except for the addition of the International Electrotechnical Commission (IEC). The IEC is a nongovernmental international standards organization that develops standards for electrical, electronic, and related technologies. Surely by now, from the barrage of acronyms, you see how bureaucratic all of this is.

As with many such standards, one of the complexities that arose with JPEG concerned intellectual property. A major challenge in establishing such international standards is to ensure that anyone can legally use the standard without infringing on the rights of someone else. There can be quite a bit of posturing during the development of a standard, where businesses will attempt to ensure that the use of the standard requires license payments to them for patents that they hold or where patents that they hold will give them a competitive advantage when implementing the standard. Organizations can even be quite sneaky about this, concealing their business interests from the standards body until it is too late to change the standard. As a result, standards often do not reflect the best technical solutions to a problem.

In the case of JPEG, after publication of the standard, several companies asserted that the standard infringed on patents that they held. In a collection of notable cases starting around 2007, a patent holding company called Global Patent Holdings, LLC, claimed that the act of downloading a JPEG image from a website or sending it through email infringed a patent that it held, U.S. Patent 5,253,341 by Rozmanith and Berinson (1993). A messy set of suits, countersuits, and threats ensued. According to a Wikipedia article on JPEG,

Global Patent Holdings had also used the '341 patent to sue or threaten outspoken critics of broad software patents. (https://en.wikipedia.org/wiki/JPEG , retrieved April 26, 2016)

After extensive battles, the U.S. Patent and Trademark Office issued a Reexamination Certificate in 2009 canceling all claims of the patent, asserting that prior art invalidated the claims. By this time, many organizations had wasted enormous amounts of money on completely nonproductive fights over intellectual property.

A patent holding company is a corporation that does not manufacture or sell products but just acquires and holds patents for the purpose of extracting royalty payments from companies that do sell products. Such companies are often called「patent trolls,」after the troll in the Norwegian fairy tale「Three Billy Goats Gruff」who eats anyone who tries to cross the bridge under which it lives.

The emergence of patent trolls has significantly changed the business climate for technology companies in the United States. An organization that produces a product and also owns a patent portfolio may be hesitant to sue another organization that also owns a patent portfolio because that other organization may countersue for patent infringement. But an organization that does not produce any products is much less vulnerable to countersuits. These organizations exist only for the purpose of siphoning money from organizations that produce products. In my opinion, they are parasites.

But I digress. The main point is that it is not only creativity that determines the nature of the layers of paradigms in a technology, but that complex business and political interests can also intervene. These layers, therefore, are not in any sense objective truths. They are the result of flawed and human processes.

AIS/Net 1000 failed to solve the crises created when incompatible computers started to become networked. That crisis has since been largely resolved through the emergence of the Internet, which depends on standardization of all levels of the OSI model. The so-called Internet Protocol (IP, not to be confused with intellectual property) is at level 3 in the OSI model, the network layer. All traffic in the Internet uses IP. A layer above, at the transport layer, is the widely used Transmission Control Protocol (TCP), which overlays on IP the concept of reliable transmission. Specifically, a TCP/IP packet sent to a computer must be acknowledged by that computer. The sending computer will repeatedly send the packet until it receives an acknowledgment. As a consequence, barring catastrophic failure in the network or in the sending or receiving computer, every sent packet is eventually received. TCP also ensures that packets sent in order are received in the same order. TCP is essential to email, among many other services.

Email, in turn, relies on another protocol called SMTP, for Simple Mail Transfer Protocol, a level-5 protocol (session layer). At this level, a sequence of TCP/IP packets is collected into a unit, an email message. The design of this protocol is greatly simplified by being able to assume the properties of the lower layers, specifically that packets are delivered reliably and in order. If you send a JPEG image by email, then the level-6 (presentation layer) protocol for JPEG image encoding defines the interpretation of the bits contained in the packets as an image.

The OSI model provides separation of concerns, where routing of packets, reliable delivery and ordering, email addressing and content, and encoding of the email payload are all separated. Each of the protocols involved is much easier to design and understand because it uses the properties of the layers below, and it avoids providing capabilities that will be provided by a layer above.

AIS/Net 1000 offered a solution to a crisis but it turned out not to be the solution that prevailed. I believe a key reason is the lack of separation of concerns. AIS/Net 1000 was to be the single solution to interconnectedness, whereas the OSI model made it possible for many competing solutions at each layer to fight it out, creating a Darwinian ecosystem with distinct niches within which solutions could compete.

There are other spectacular technology failures with similar reasons. Ed Cone blogs about the failure of the Federal Aviation Administration's (FAA's) Advanced Automation System (AAS) project, conceived in 1981 and terminated in 1994 (Cone, 2002). In this project, the FAA contracted IBM Federal Systems, a division of IBM later acquired by Lockheed Martin, to replace the nation's air traffic control system with a completely new modern design. According to Cone,「the FAA ultimately declared that $1.5 billion worth of hardware and software of the $2.6 billion spent was useless.」

The historical backdrop of the project is telling. In 1981, the air traffic controllers went on strike, and President Ronald Reagan summarily fired all 11,345 of them. This accentuated a crisis already under way created by an aging inflexible air traffic control system. Part of the solution was to be a system that was more automated, requiring fewer controllers to manage more planes.

Robert Britcher, who worked on the project at IBM Federal Systems, wrote about it in his book, The Limits of Software: People, Projects, and Perspectives , where he states that it「may have been the greatest debacle in the history of organized work」(Britcher, 1999, p. 163).

Why did it fail? Cone quotes Pete Marish, a senior analyst at the General Accounting Office:

It was basically a Big Bang approach, gigantic programs that would revolutionize overnight how [the] FAA did its work. (Cone, 2002)

Cone further quotes Bill Krampf, who worked on the project at IBM Federal Systems:

We entered [the] software phase without the requirements phase completed. (Cone, 2002)

Krampf's observation, however, is probably a misdiagnosis of the problem. I seriously doubt that completing the requirements phase before starting the work on software would have solved the problem. The idea of completing requirements before engaging in detailed design goes against the grain of one of today's most popular software engineering strategies, called「agile development.」In an agile process, requirements are developed along with the software through a series of incremental「sprints,」short development efforts with modest partial goals toward the overall project objective. An agile process directly involves the customer and expects requirements to evolve as the project evolves. This way of managing complexity is more realistic than doing specification before design.

Marish's diagnosis is likely more accurate. Wholesale technology replacements generally require too many concurrent paradigm shifts. Indeed, Cone attributes the failure to enormous optimism about emerging immature technology paradigms, including object-oriented design, distributed computing, and the Ada programming language. Cone writes,

AAS was supposed to be a showcase for Unix-based distributed computing and for development in Ada, a programming language created by the Air Force that became the state-sponsored religion in object-oriented technology, itself a relatively young methodology for writing code in self-contained, reusable chunks. (Cone, 2002)

I find the words「state-sponsored religion」fascinating; they reflect the dogmatic fervor that I frequently encounter in computer scientists who espouse devotion to one or another programming language.

Another dramatic failure of a large engineering project was the U.S. Army's Future Combat Systems (FCS) program. Although there were many reasons that this program failed, one was similar to the reason for the failure of the FAA's AAS program: the program was too ambitious about replacing too many systems all at once. According to a 2012 report by the RAND Corporation,

Compared to more traditional acquisition strategies, the [systems-of-systems] approach significantly increased both the complexity of the organizations needed to execute the FCS program and the technical challenges associated with system engineering, software engineering, and system integration. (Pernin et al., 2012)

The FCS program was launched in 2003 with an estimated cost of $92 billion (including the projected cost of a fleet of war-fighting vehicles). By 2009, when Defense Secretary Robert Gates announced that he wanted to scrap the core of the program, the suite of combat vehicles, the estimated cost had ballooned to some $200 billion.

AIS/Net 1000, the FAA's AAS program, and Army's FCS program were all attempting to solve enormously complex problems. When complexity becomes unmanageable, a crisis in the prevailing paradigms becomes apparent. AIS/Net 1000 had as its goal to ameliorate the crisis without inducing a paradigm shift. But that's not how it played out. Instead, the Internet emerged. The other two projects failed in part because they attempted to address crises with a wholesale replacement of many existing paradigms all at once. But technology paradigms grow more organically, more bottom up than top down. They are not imposed on engineers so much as discovered, nurtured, and grown by engineers.

Wholesale simultaneous replacement of several paradigms at once fails because each individual replacement has poor prospects of success. The fact is that most technology innovations fail. We tend to remember only the ones that succeed. It is often impossible to predict which of several competing technologies will eventually prevail, even when it seems clear which technology is more fit.

The layering of paradigms offers a fundamentally creative way to deal with a crisis of complexity. One solution is not to fix a broken paradigm, replacing it with a new one, but rather to build an entirely new paradigm on the scaffolding of the old. We build platforms on top of platforms. Because of separation of concerns, a layer in a paradigm can change, and the effects will only be felt one layer up. In the Internet, for example, at layer 3 of the OSI model, the world is in the midst of migrating from IP version 4 to IP version 6 (no version 5 was ever deployed).

The new version IPv6 changes quite a few fundamental things, including the addresses used to identify nodes in the Internet. IPv4, it turns out, provides only four billion distinct addresses. Given that there are already six billion devices on the Internet, this obviously creates problems. Considerable cleverness is required to reuse addresses without creating ambiguities. IPv6 increases the number of addresses to

2 128 = 340,282,366,920,938,463,463,374,607,431,768,211,456.

It simply would not be possible to make such a fundamental change without the separation of concerns offered by the OSI model. This change has no effect, for example, on the JPEG encoding of images transmitted over the Internet.

Similarly, the layers of digital technology in figure 3.3 provide separation of concerns that permits independent simultaneous evolution at all levels. For example, the shift to using FinFETs for transistors had no effect on the design of instruction set architectures, except perhaps to offer opportunities through added capability. I examine this question of opportunity next.

[1] Moore was one of the「traitorous eight」who left the Shockley Semiconductor Laboratory to found Fairchild Semiconductor and start Silicon Valley.

[2] Douglas Adams described the Babel fish in The Hitchhiker's Guide to the Galaxy . According to Adams,「The Babel fish is small, yellow, leech-like, and probably the oddest thing in the universe. It feeds on brain wave energy, absorbing all unconscious frequencies and then excreting telepathically a matrix formed from the conscious frequencies and nerve signals picked up from the speech centres of the brain, the practical upshot of which is that if you stick one in your ear, you can instantly understand anything said to you in any form of language: the speech you hear decodes the brain wave matrix.」

6.2 危机与失败

库恩认为，科学革命只有在旧范式下的异常情况积累到一定程度后才会发生，而且只有在出现新范式取代旧范式的时候才会发生。但是，这些并不是推动技术范式转换的驱动力。

导致技术范式转换的原因至少有三个。首先，正在设计的系统的复杂性超出我们人类理解或控制这些系统的能力。例如，编程语言的出现是因为编写正确的机器码或汇编代码变得异常困难。其次，去做一些以前没有人想象得到的事情开始变得可能。例如，谷歌和其他搜索引擎几乎可以即时搜索到人类发布过的任何内容。第三，复杂的社会、政治和商业力量可以推动技术范式的转换。例如，军事需求根本性地创造了航空、核武器和许多其他技术，同时军事预算也为计算机技术的早期发展提供了大部分资金。

在 3.2 节「简化的复杂性」中，我指出复杂性的一个来源是使用了大量的组件。即使是那些具有简单功能的简单组件，例如充当开关的晶体管，只要有足够的数量，也能实现极其复杂的功能。几十年来，植根于这些晶体管的数字技术一直是推动由复杂性所驱动的范式转换的主要原动力。

1965 年，英特尔的联合创始人戈登·摩尔做出一个著名的预测，集成电路中的元件（晶体管、电阻、二极管和电容）的数量将在未来，至少是 10 年内以每年翻一番的速度增长。1975 年，他又将预测的增长率修正为每两年翻一番。这就是人们熟知的「摩尔定律」。自提出之日起，该定律就一直是半导体行业的指导原则。

图 6.2 库恩认为，在科学革命中，新范式通常会取代旧范式。在技术革命中，新范式可能建立在旧范式的基础之上，将旧范式隐藏在一个抽象层之后，而不是彻底取代它们。（在加拉帕戈斯群岛的圣克鲁斯岛上，一幅带有查尔斯·达尔文肖像的标语照片。)

实际上，直到 2015 年左右，摩尔的预测一直保持稳定。英特尔 8080 是 1974 年推出的一款单片计算机（简称单片机），有大约 4 400 个晶体管。因此，根据摩尔定律，2014 年生产的一台单片机应该包含如下数量的晶体管：

400×2$^{(2014-1974)/2}$ ≈ 4 610 000 000

这个数值与 2014 年推出的英特尔 Xeon Haswell-E5 处理器上的 55.6 亿个晶体管的数量非常接近。尽管许多人都预言了摩尔定律的消亡，但是，大多数行业观察人士似乎都认为，直到 2015 年，摩尔定律所预测的增长速度才显著放缓。

数字技术能力的快速加速已经引发了一系列持续的危机。用于设计和编程系统的模型与机制在额外能力的挤压下会不可避免地反复崩溃。早在 1972 年，艾兹格·迪杰斯特拉曾写道：

坦率地说，只要没有机器，编程就根本不是问题；当我们有了几台功能较弱的计算机时，编程会成为微小的问题；而现在，我们有了强大的计算机，编程也随之变成了一个同样巨大的问题。（迪杰斯特拉，1972）

迪杰斯特拉说上面这段话的时候还只是 1972 年！如果这在当时已经是一个巨大的问题，就没有文字可以描述其现在达到的程度了。

摩尔定律只适用于基于单个硅芯片的单个计算机。今天，我们看到通过网络互连的计算设备的数量在急剧增长。大约在 1980 年，3Com 公司的联合创始人之一、以太网（以太网是当今使用最广泛的有线网络技术）的共同发明人罗伯特·梅特卡夫就提出了一个现在被称为梅特卡夫定律的推定。该定律认为，网络的价值与网络上兼容的通信设备的数量平方成正比。例如，如果单台设备的价值为 1 美元，那么一个连接 10 台设备的网络的价值就是：

1 美元 × 10^2 = 100 美元

以此类推，一个拥有 100 台设备的网络价值将会是 1 万美元，而一个有 1 000 台设备的网络价值为 100 万美元。现在我想让你计算一下梅特卡夫对今天的互联网估值，今天的互联网有大约 60 亿台连接的设备。

连接设备的数量还在快速增长。今天，由于所谓物联网（IoT）的兴起，行业领袖们预测到 2020 年将会有 500 亿台联网设备。物联网连接的并不是最重要的计算机设备，例如恒温器、汽车、门锁、空调等等。当他们给出这样的预测时，你几乎都可以看到美元在他们眼中舞动的样子。

因为价值可能来自容量，所以我假设梅特卡夫会得出这样的结论 —— 网络容量，不仅是网络的价值，也与所连接设备数量的平方成正比。由于复杂性通常也与容量相伴而生，因此，我们不应指望未来几年危机会有所减缓。即便是摩尔定律逐渐失效，日益增长的复杂性所引发的压力也不会减缓。

在任何技术中，日益增加的复杂性都会以两种方式导致危机。首先，设计可靠的系统变得更加困难。在复杂性较低时运行良好的工具和模型会随着复杂性的增加而不断受压，直至崩溃。其次，也许是前一个原因的结果，一个设计项目失败的可能性增加了。

20 世纪 80 年代初，当我在贝尔实验室工作时，有一个名为 AIS/Net 1000 的大型项目，该项目旨在为当时存在的不同计算系统提供连接的桥梁。当时，通过网络连接计算机还是一种相当新颖的现象，而且，正如梅特卡夫定律所表明的，这种互联的价值得到了认可。至少梅特卡夫认为如此。

但是，这种互联暴露了不同计算机系统之间的许多不兼容性，特别是来自不同供应商的计算机系统。原因在于这些系统都被设计成是独立工作的，例如用来表示数字和文本的二进制模式是各不相同的，这些比特在存储器中的排列顺序不同，用于通信的协议和速度不同，等等。这些差异意味着一台计算机通常无法与另一台计算机直接进行通信。即使可以，其也无法正确地解释由另一台计算机生成的比特模式。换句话说，每台计算机都在它自己的范式中运行，而这些范式是不可通约的。

随着计算机的网络化，这种不兼容引发了一场危机。AIS/Net 1000 项目旨在通过在网络中执行不同范式转换的机制来解决这个问题，从而允许不同的范式继续存在。当一台计算机向另一台计算机发送消息时，该消息将在传输过程中被自动转换。这样任何操作计算机的人都不需要改变自己的工作方式。这就是网络中的巴别鱼。然而，这个项目最终还是失败了。美国电话电报公司取消了超过 10 亿美元的开发经费。事实上，项目失败的主要原因在于，很少有客户愿意为这项服务付费。相反，这些不同的计算机系统的范式正好见证了达尔文主义的稳固。相互竞争的范式无法在同一个联网计算机的生态系统中共存。

小说中的巴别鱼并没有出现，而互联网出现了。开放系统互连（OSI）模型被接受是促成互联网诞生的一个关键因素。

OSI 是一个分层的建模范式，如图 6.3 所示。与图 3.3 所示的各层一样，OSI 模型的每一层都为计算机之间的通信提供了一个概念框架。最低层被称为物理层，负责将比特序列从一个位置传输到另一个位置，而不关心这些比特的具体含义。最低层之上的层赋予这些比特更多的意义。举例来说，第 6 层，即表示层，可以将 100 万比特的集合当作一种特定格式的图像编码，如在数码相机和网络上广泛使用的标准化 JPEG 格式。

库恩认为不同的范式之间是不可通约的。在 OSI 模型中，「帧」、「包」、「段」和「会话」都是指一个有限的比特集合，但它们都在不同的层次上，且具有不同的含义。以我个人的经验来说，理解这些不同的含义是使用低层次网络软件时最容易混淆的部分之一。在其中的一个具体层次上工作而不尝试跨越多个层次通常要容易很多。

把 OSI 模型的各个层称为「范式」也许令人感到奇怪，因为它们与库恩所说的科学范式有很大的不同。就像库恩提到的范式一样，它们也确实为人类理解系统如何运行提供了一个心智模型。例如，想象一台计算机向另一台计算机发送一幅图像（照片），是与想象一台计算机发送 100 万比特的数据流不同的心智模型。但与库恩的范式不同，要使这些层发挥作用，就必然要对它们进行绝对精确的定义。如果这 100 万比特中的一个被误读，那么也许会导致图像变得不可读。然而，库恩的范式要更具鲁棒性，它们能够容忍一定程度的创造性误读，这有时会形成创新的引擎，甚至会引起范式的转换。

7 应用层：应用程序直接使用的网络服务。

6 表示层：将比特模式解释为文本、图像、数字等。

5 会话层：将多个来回的数据父换视为一个单兀。

4 传输层：数据段的可靠传输。

3 网络层：在一个多结点网络对比特构成的数据包进行路由。

2 数据链路层：在两个结点之间传输一个比特帧。

1 物理层：有线或无线的比特流。

图 6.3 用于计算机间通信的 OSI 模型。

要使得 OSI 模型的这些层都非常精确并不是一件容易的事情。为了使互联网上的计算机能够可靠地通信，OSI 模型需要在每一层上就精确的含义达成一致，向下一直到对每个比特的解释。然而，制定这份标准协议的过程可能会牵扯太多的因素，它很可能会陷入一个混乱的、政治的、官僚主义的泥潭，因为这一协议与涉及的每个国家以及每个商业集团的利益都息息相关，这常常会引发利益上的冲突。

下面这个例子可能有助于我们了解 OSI 模型是如何产生的。OSI 模型是两个标准化机构共同努力的结果，即国际标准化组织（ISO）和国际电信联盟电信标准化部门（ITU-T，前身是国际电报电话咨询委员会 CCITT），它们在 20 世纪 70 年代末分别开发了类似的计算机通信模型。但是，类似的模型还不足以让计算机进行通信。模型必须是相同的，才能实现不同计算机之间的通信。因此，这两个机构联合发布了一份共同文件。很显然，这一过程无疑会涉及多个细节问题上的激烈争论。

为了了解所涉及的所有竞争利益，我们很有必要先了解一下这些标准化机构是如何组织的。国际标准化组织由来自 162 个国家的标准化机构的代表组成。ITU-T 是一个联合国机构，它主要负责协调电信标准。除了许多国家政府的代表，这些机构还包括来自竞争行业的代表，其中一些企业已经对正在标准化的技术投入了大量资金。因此，标准的制定是一个旷日持久且令人心力交瘁的过程，而随后的相互妥协有时会破坏所形成标准的效力。

JPEG 是最常用的图像编码，也是 OSI 模型第 6 层（表示层）中常用的一个标准，它是创建该标准的联合摄影专家组（Joint Photographic ExpertsGroup）的首字母缩略词。这个小组是一个由 ISO/IEC JTC1 和 ITU-T 交叉组成的委员会，除了加入国际电工委员会（IEC），这些组织也都是 OSI 模型的成员。IEC 是一个非政府性的国际标准组织，主要为电气、电子和相关技术制定标准。当然，看着这一连串的缩略词，我想读者们也能感受到这一切是多么官僚。

与许多此类的国际标准一样，JPEG 所带来的复杂性之一与知识产权有关。建立这种国际标准要面对的一个主要挑战就是，如何确保任何人在不侵犯他人权利的情况下合法地使用该标准。在制定一个标准的过程中，可能会出现相当多的不同立场，获得专利权的企业将试图确保这个标准的使用要为它们所拥有的专利支付许可费用，或者在实施标准时，使它们所拥有的专利具有竞争优势。有些组织甚至会在暗中这样做，并且会向标准机构隐瞒其商业利益，等到标准形成后就不好再改变了。因此，标准往往不能反映问题的最佳技术解决方案。

现在，我们来看看 JPEG 的情况，该标准发布后，一些公司声称该标准侵犯了它们持有的专利。在从 2007 年开始的一系列著名诉讼案件中，全球专利控股有限责任公司声称，从网站下载 JPEG 图像或通过电子邮件发送图像的行为侵犯了其所持有的一项美国专利，专利编号为 5253341，该专利是由罗茨马尼特和贝林森在 1993 年申请的。同一时期，一连串的诉讼、反诉讼和威胁接踵而至。维基百科上有如下关于 JPEG 的一篇文章：

全球专利控股有限责任公司还利用 341 这项专利起诉或者威胁那些对大量软件专利进行直言不讳的批评的人。（https://en.wikipedia.org/wiki/JPEG，2016 年 4 月 26 日检索。）

经过广泛而持久的斗争，2009 年，美国专利和商标局颁发了一份专利复审证书，撤销了该专利的所有权利主张，并声明现有技术已使得这些主张无效。至此，许多组织已经为这项完全没有成效的知识产权斗争浪费了大量的资金。

一家专利控股公司是指并不制造或销售产品，只是为了从销售产品的公司收取专利使用费而获取和持有专利的公司。这类公司通常被称为「专利巨魔」，这个名字取自挪威童话故事《三只山羊嘎啦嘎啦》里的巨魔，它住在一座大桥的下面，会吃掉任何试图经过那里的动物。

专利巨魔的出现极大地改变了美国科技公司的商业环境。一个生产产品并拥有专利组合的组织可能犹豫是否起诉另一个拥有专利组合的组织，因为被起诉的组织可能会对专利侵权提起反诉。但是，一个不生产任何产品的组织更不容易受到反诉。这些组织的存在只是为了从生产产品的组织那里攫取资金。在我看来，它们其实就是寄生虫。

我似乎又离题了。我要表达的一个主要观点是 —— 技术中那些范式层的性质不仅取决于创造力，而且会受到复杂的商业和政治利益因素的干扰。因此，可以这么说，这些层在任何意义上都不是什么客观真理，它们是有缺陷的，也是人为过程的结果。

AIS/Net 1000 项目没能解决彼此不兼容的计算机联网时所引发的危机。这场危机在很大程度上以互联网的出现而得到解决，互联网 OSI 模型中所有层的标准化。所谓互联网协议（Internet Protocol，缩写为 IP，不要与知识产权混淆）在 OSI 模型中处于第 3 层，即网络层。互联网上的所有流量都要使用该协议。网络层之上是传输层，该层中广泛使用传输控制协议（TCP），其在 IP 之上增加了可靠传输的概念。具体而言，发送到接收方计算机的 TCP/IP 数据包必须得到该计算机的确认。发送方计算机将重复发送该数据包，直到它接收到一个应答为止。因此，除非网络或者发送方、接收方计算机发生了灾难性故障，否则每个发送的数据包最终都会被接收。TCP 还确保按顺序发送的数据包将以相同的顺序被接收。TCP 对于电子邮件和许多其他服务来说是必不可少的。

而电子邮件则依赖于另一种 SMTP，即简单邮件传输协议。该协议位于第 5 层（会话层）。在这一层，TCP/IP 数据包序列被汇集到一个单元，即一个电子邮件消息。由于能够假定下面这些层的特性，特别是数据包是被可靠且有序地分发的，因此该协议的设计被大大简化了。如果你通过电子邮件发送 JPEG 图像，那么，用于 JPEG 图像编码的第 6 层（表示层）协议将会把包中包含的比特数据定义为图像。

OSI 模型对这些关注点进行了分离，其中，数据包的路由、可靠传输与排序、电子邮件地址和内容以及电子邮件内容的编码都是分开的。所涉及的每个协议都更易于设计和理解，因为它们使用下面各层的属性，并且避免了提供上面一层所应提供的功能。

AIS/Net 1000 项目为网络危机提供了一个解决方案，但事实证明，它并不是一个非常有优势的解决方案。我认为一个关键的原因是，它没有实现有效的分层。AIS/Net 1000 是实现互联的单一解决方案，而 OSI 模型使每一层的许多解决方案能够相互竞争，实现优胜劣汰，从而创造出一个类似于达尔文式的生态系统。在这个生态系统中，解决方案可以互相竞争。

还有其他一些引人注目的技术也有类似的失败原因。埃德·科恩在他的博客里讲述了美国联邦航空管理局（FAA）高级自动化系统（AAS）项目失败的原因。该项目于 1981 年开始构思，1994 年被迫终止（科恩，2002）。在这个项目中，联邦航空管理局与 IBM 联邦系统公司签约，以一种全新的现代设计来替代美国的空中交通控制系统。IBM 联邦系统公司是 IBM 的一个部门，后来被洛克希德·马丁公司收购。根据科恩的说法，「联邦航空管理局最终宣布，之前花费的 26 亿美元中，有大约 15 亿美元的硬件和软件是无用的」。

这个项目的背景很能说明问题。1981 年，美国空中交通管制管理人员举行大罢工，罗纳德·里根总统立即解雇了他们中的 11 345 人。这反而加剧了一场原本由老旧、僵化的空中交通管制系统引发的危机。所以，解决这场危机的方案之一是建立一个自动化程度更高的管制系统，以雇用更少的管制人员来管理更多的飞机。

罗伯特·布里彻曾经在 IBM 联邦系统公司参与过这个项目，他在《软件的局限性：人员、项目和视角》一书中写道，这「可能是有组织工作历史上最大的失败」（布里彻，1999:163）。

该项目为什么会失败？科恩引用了下面这段美国审计总署资深分析师皮特·马里什的话：

这基本上是一个大爆炸式的方法，如此庞大的项目将在一夜之间彻底改变美国联邦航空管理局的工作方式。（科恩，2002）

科恩还引用了在 IBM 联邦系统公司参加该项目工作的比尔·克兰普夫的一段话：

我们没有完成需求阶段，一下子就进入了软件阶段。（科恩，2002）

然而，我认为克兰普夫的观点可能是对这个问题的错误诊断。我非常怀疑在开始软件设计工作之前完成需求阶段的工作是否真的能解决问题。在进行详细设计之前完成需求的想法，与当今最流行的软件工程策略之一的「敏捷开发」理念背道而驰。在敏捷开发过程中，需求与软件是一起通过一系列的增量式「冲刺」开发形成的，这些冲刺是短暂的开发工作，且仅有部分目标是针对整个项目目标的。敏捷开发的过程会直接涉及客户，并期望需求随着项目的发展而不断得到完善。这种管理复杂性的方法比在设计之前制定规范更加现实。

我认为马里什对问题的诊断可能更为准确。大规模的技术替代通常需要同时对太多的范式进行转换。事实上，科恩将该项目的失败归因于对新兴的不成熟技术范式的过分乐观，其中包括面向对象设计、分布式计算和 Ada 编程语言等。科恩写道：

AAS 被认为是基于 Unix 操作系统的分布式计算以及采用 Ada 语言进行开发的一个展示窗口，Ada 是由美国空军创建的一种编程语言，后来成为由国家资助的面向对象技术的「教义」，其本身是一种相对年轻的方法，用于以自包含的、可重用的块来编写代码。（科恩，2002）

我觉得「国家资助的教义」这个说法很有趣，它反映了我常常在计算机科学家中见到的教条主义狂热。这些科学家忘我地献身于一种或另一种编程语言。

另一个大型工程项目的重大失败，是美国陆军的未来作战系统（FCS）计划。虽然这个工程项目失败的原因有很多，但其中有一个类似于联邦航空管理局 AAS 项目失败的原因：该计划过于雄心勃勃，想要一次更换太多的系统。兰德公司 2012 年的一份报告有如下描述：

与更为传统的获取策略相比，系统的系统（systems-of-systems）这一方法显著地增加了执行 FCS 计划所需组织的复杂性，同时也加大了与系统工程、软件工程和系统集成相关的技术挑战。（佩尔南等，2012）

FCS 计划于 2003 年启动，预计耗资 920 亿美元（包括一支作战车队的预算费用）。到了 2009 年，当国防部长罗伯特·盖茨宣布他想要废除这个计划的核心部分 —— 这支作战车队时，估计成本已经高达 2 000 亿美元了。

AIS/Net 1000 项目、联邦航空管理局的 AAS 项目以及美国陆军的 FCS 项目最初都雄心勃勃地想要解决极其复杂的问题。但是，当复杂性变得难以控制的时候，主流范式中的危机就变得显而易见了。AIS/Net 1000 的目标是在不引发范式转换的情况下缓解危机。但是，事情并未像预想的那样发展。相反，互联网出现了。另外两个项目的失败在某种程度上是因为它们都试图用大规模替换现有范式的方法来应对危机。然而，技术范式的发展更为有机，更自下而上，而非自上而下。与其说技术范式是强加给工程师的，不如说其是由工程师发现、培育并成长起来的。

大规模地同时替换多个范式肯定会导致失败，因为单个范式的转换前景很难立即成功。事实上，大多数技术创新都以失败告终。可是，我们往往只记得那些成功的例子。在现实中，即使有哪种技术看似更合适，其发展的结果也是很难预料的，人们往往无法预测几种相互竞争的技术中究竟哪种最终会占上风。

范式的分层提供了处理复杂性危机的基本的创造性方法。一种解决方案是，不去修复一个有缺陷的范式，而是以一个新范式取而代之，在旧范式的基础上建立一个全新的范式。也就是说，我们在平台之上构建平台。由于每个层分别关注各自的主要问题，范式中的一个层就可以发生变化，而且其影响只会被它上面的一层感知。例如，在互联网中，OSI 模型第 3 层的网络协议正处于从 IPv4 迁移到 IPv6（从来没有部署过 IPv5）的过程中。

新版本 IPv6 改变了很多基本的东西，包括用于识别互联网中结点的地址。事实证明，IPv4 只能提供 40 亿个不同的地址。考虑到现在互联网上已经有 60 亿台设备，这显然会引发问题。因为在不产生歧义的情况下，重用地址需要相当聪明的方法。IPv6 中，地址数目将会增加到如下数量：

2128 = 340 282 366 920 938 463 463 374 607 431 768 211 456。

如果没有 OSI 模型提供的分离式设计，就不可能做出这样的根本性改变。例如，这一变化对通过互联网传输图像的 JPEG 编码没有产生任何影响。

同样，图 3.3 中的数字技术层也提供了分离式设计，这允许在所有层次上同时进行独立的演化。例如，转向采用 FinFETs 作为晶体管的这一改变，不但不会对指令集体系架构的设计产生任何影响，还可能通过增加的功能提供更多的机遇。接下来，我就要研究一下机遇的问题。

### 6.3 Crisis and Opportunity

According to Kuhn, observations made in the course of normal science may reveal anomalies, inconsistencies with the prevailing paradigm that governs the normal science. These anomalies can create a crisis that leads to a paradigm shift. In engineering, it is not usually scientific observations that create a crisis. We have already seen that increasing complexity can trigger a crisis. A second trigger is opportunity.

Consider the introduction of the iPhone in 2007. At the time, two of the dominant producers of cell phones were Nokia, a Finnish company, and Research in Motion (RIM), a Canadian company, maker of the Blackberry. These two companies have drastically reduced visibility in the cell phone market today. I've already pointed out that the iPhone introduced no new technology. So why was it such a revolution, summarily overthrowing the old regime?

The「crisis」in the paradigm overthrown by the iPhone was not a crisis of complexity. It was a crisis of opportunity. At the time, cell phones were starting to be used for things other than making phone calls. The Blackberry had captured business markets with its built-in keyboard and email capability. Nokia phones were routinely used, primarily by young people, to send text messages, despite the incredible awkwardness of typing text on a 12-key numeric keypad. At the time, there were even contests for speed texting on such keypads because it required quite a bit of skill.

In 2007, wireless networks had modest ability to carry data, although the emphasis was still on carrying voice signals. That capability was exploited by the Blackberry and by the texting function on other phones, but phones were still primarily for making voice calls. Today, the ability to make voice calls seems like an incidental feature of a smartphone. When I want a voice call with my 20-year-old daughter, I need to exchange several text messages with her to arrange it. She acquiesces only in deference to my age. Her other communications are likely more through Snapchat and other services I've never heard of.

The iPhone came about through a realization of what was possible with the technology of the time. But the real revolution was not replacing the phones of the time with better phones. It was the introduction of a whole new platform, a new layer in the stack of layers of paradigms. Specifically, the real revolution was the introduction of the app development platform. With the introduction of the iPhone, Apple published the specifications that enabled millions of creative programmers around the world to develop applications for the phone and in 2008 launched the App Store to broker the sales of apps to customers.

The nature of a revolution is that its consequences usually cannot be anticipated, but after the revolution its consequences seem inevitable. It is easy to forget today that in 2007, most of us had never heard of apps and app stores, although, as usual with technology innovations, variants of the concept had existed at least since the 1990s. But Apple really made the concept take off. Apple's model has been emulated by every cell phone vendor that still has any significance, down to the details of copying the patented look of the phone, a move that has resulted in an endless string of patent infringement lawsuits and countersuits.

I am quite sure that if we could time travel back to 2007 and assemble the smartest, most creative experts worldwide in a room, they would not be able to anticipate even 10% of the functions that we routinely carry around in our pockets today: instant traffic reports worldwide (go ahead: check the traffic in Budapest right now), airline reservations, banking transactions (even check deposits), tide charts, worldwide weather forecasts, up-to-the-minute mass transit timetables, remote monitoring of our homes, a taxi service, restaurant reviews, a library with millions of books and journals, and many creative games. In addition to all those functions that never before existed, the device replaces several other devices that we previously would have to carry separately, including the phone, the music player, a flashlight, the keys to our house, the video entertainment device (remember the portable DVD player?), a compass, a calculator, an address book, our calendar, a camera, a radio, a notepad, and an alarm clock. Oh yes, and it also sends text messages and email.

The smartphone was not a consequence of a crisis of complexity, it was a consequence of opportunity enabled by millions of transistors on a chip, good digital radios, touch-screen interfaces, and the Internet, all preexisting technologies. The key to the revolution, the decisive battle that won the war, was the app development platform and the app store.

In recent years, we have seen an astonishing number of similarly disruptive revolutions. Amazon put thousands of bookstores out of business and is in the process of threatening the rest of retail. Uber and Lyft have undermined the taxi business. Lulu and other print-on-demand services are threatening the publishing industry. E-books are threatening Lulu and the rest of the printing industry. Libraries are increasingly irrelevant. Travel agencies have almost entirely vanished.

Each of these revolutions entails a paradigm shift. But paradigm shifts do not come easily to people, lending some stability and inertia. Even disruptive changes take some time to play out. According to Statista, an online statistics company, there were still about 28,000 bookstores in the United States in 2012. Although this number is down significantly from more than 38,000 in 2004, it is still a significant number.

Some paradigm shifts replace prior paradigms. Even for taxi services, for example, we are now more likely to summon them using a smartphone app or a web page than via a phone call. But all of these paradigm shifts also build on prior paradigms, leaving them unchanged. Smartphone technology, for example, relies heavily on Internet technology, the latter of which has hardly changed in response to this revolution. To be sure, there are small changes, such as better support at OSI levels 6 and 7 for small screens, but these changes are tiny. The prior paradigm provides a platform for the new paradigm, a situation rarely seen in the scientific paradigm shifts that Kuhn talks about. The transitivity of models makes this possible.

Many examples of failed paradigm shifts also exist. In the 1980s, for example, several university research projects and startup companies were going to disrupt the computer industry with dataflow computers, which presented an entirely different way to define an instruction set architecture (Arvind et al., 1991). These all failed. Perhaps a more curious example is the repeated failure of artificial intelligence (AI) as a field. AI has survived several boom and bust cycles, where unbridled enthusiasm is followed by disillusionment and collapse of investment. Starting in the late 1980s, AI experienced what some researchers in the field called an「AI winter,」an allusion to a nuclear winter, and had only fully recovered by about 2010. Perhaps dataflow computers will be similarly resurrected. Such failures fade quickly from our memory (except, of course, for the people most directly involved in the failures).

But failures are a normal and healthy part of intellectual inquiry. The rapid advances of digital technology provide a healthy, thriving ecosystem for mutation, adaptation, and extinction of paradigms. There need not be anything fundamentally wrong with a new paradigm that fails. Unlike scientific paradigms, technology paradigms are not held up to a standard of truth or concurrence with observations of the physical world. Their survival instead depends on many intangibles, including, perhaps most important, the readiness of the public and even the engineers to assimilate the paradigm.

6.3 危机与机遇

库恩认为，我们在常态科学中观察到的异常现象可能会揭示异常，其与常态科学的主流范式不一致。这些异常可能会导致一个范式转换的危机。在工程学中，通常并不是科学观察导致危机的产生。我们已经看到，日益增加的复杂性可能会引发一场危机。第二个触发危机的因素则是机遇。

让我们再来考虑 2007 年推出苹果手机时的情形。当时，手机的两个主要制造商分别是芬兰的诺基亚公司和加拿大的黑莓公司。今天这两家公司在手机市场上的知名度已经大不如前了。正如我已经指出的那样，苹果手机并没有引入任何新技术。那么，为什么它会成为一场革命，一下子就推翻了旧的格局呢？

被苹果手机颠覆的范式中的「危机」并不是一场由复杂性引发的危机，这是一场机遇危机。当时，除了打电话，手机也开始被用作他途 —— 这正是它能够快速发展的新机遇。黑莓手机凭借其内置的键盘和电子邮件功能占领了商业市场。尽管在 12 键数字键盘上输入文本令人觉得很不方便，诺基亚手机还是经常被用来发送短信，主要是年轻人在使用。在当时，甚至出现了在这种键盘上快速发送短信的竞赛，因为这需要相当多的技巧。

2007 年，无线网络具有了一定的数据传输能力，但主要是传输语音信号。黑莓和其他手机的短信功能都充分利用了这一功能，但手机仍然主要用于语音通话。今天，语音通话似乎只是智能手机的一个附带功能。当我想和我 20 岁的女儿通话时，我需要和她交换几条短信来安排这件事。她只是出于对我年龄的尊重而默许这样的安排。她的其他通信方式可能更多是 Snapchat（照片分享应用程序）和其他我从未听说过的应用程序。

苹果手机的出现，是因为人们意识到在当时的技术条件下什么是可能的。但是，真正的革命并不是用更好的手机取代当时的手机。真正的革命是指引入一个全新的平台，并在范式层的堆叠中形成一个新的范式层。具体来说，真正的革命是引入应用程序开发平台。随着苹果手机的推出，苹果公司发布了一系列规范，这使得全球数百万富有创造力的程序员能够为苹果手机开发各种应用程序。

2008 年，苹果公司推出了应用商店（App Store），从而向客户代理销售应用程序。

革命的本质在于，其后果通常是无法预料的，但在革命发生之后，其后果似乎又是不可避免的。今天我们也许已经淡忘了曾经发生的一些事情。

2007 年，我们中的大多数人从未听说过应用程序和应用商店。其实，这些概念与其他技术创新一样，其雏形概念至少在 20 世纪 90 年代就已经存在了。但是，苹果公司确实让这些概念迅速得到普及。并且，苹果公司的模式已经为每一个仍有影响力的手机厂商所效仿，甚至是复制手机外观专利的细节。此举导致了无穷无尽的专利侵权诉讼和反诉讼。

我可以肯定地说，如果我们回到 2007 年，把世界上最聪明、最具创造力的专家聚集在一个房间里，他们甚至都无法预测我们今天日常随身携带的手机中的 10% 的功能：全球即时交通报告（现在我们就可以查一下布达佩斯的交通状况）、机票预订、银行交易（甚至是查询银行存款余额）、潮汐图、全球天气预报、最新的公共交通时刻表，还有对自己家的远程监控、出租车服务、餐馆评论、一个拥有数百万本图书和期刊的数字图书馆，以及许多富有创意的游戏，等等。除了这些以前从未存在过的功能，这种设备还取代了我们以前必须单独携带的其他一些设备，包括电话、音乐播放器、手电筒、家里的钥匙、视频娱乐设备（还记得便携式 DVD 播放机吗）、指南针、计算器、地址簿、日历、照相机、收音机、记事本和闹钟。哦，是的，它还可以发送短信和电子邮件呢。

智能手机并不是一场复杂性危机的结果，而是芯片上的数以百万计的晶体管、良好的数字收音机、触摸屏接口和互联网等这些预先就已存在的技术所带来机遇的产物。这场科学革命赢得决定性胜利的关键，是应用程序开发平台和应用商店。

近年来，我们已经见证了数量惊人的类似颠覆性革命。亚马逊令数千家书店停业，并正在对其他零售业务构成威胁。优步（Uber）和来福车（Lyft）已经削弱了出租车业务。

Lulu 和其他的按需印刷服务正威胁着出版业的发展。而电子书又在威胁着 Lulu 和印刷业中的其他行业。昔日的图书馆变得越来越无关紧要。旅行社几乎就要消失了。

每发生一次这样的革命都需要经历一次范式的转换。但是，人们不再那么容易接受范式的转换，因为他们习惯于原来的范式，原来的范式具有一定的稳定性，并给人们带来一定的惰性。即使是颠覆性的转换，也需要一段时间才能完成，因为接受需要时间。根据 Statista（全球领先的数据统计互联网公司）的数据，2012 年美国仍有 2.8 万家书店。虽然这一数字大大低于 2004 年的 3.8 万家，但仍然是一个很大的数字。

一些范式的转换取代了以前的范式。以出租车服务为例，我们现在更有可能通过智能手机的应用程序或网页预约出租车，而不是通过打电话。但是，所有这些范式的转换都建立在先前的范式之上，并没有改变那些旧范式。例如，智能手机技术很大程度上依赖于互联网技术，然而，互联网技术几乎没有随着这场技术革命发生改变。当然，也出现了一些小的变化，例如 OSI 模型第 6 层和第 7 层现在可以更好地支持小屏幕，但是这些变化是很小的。先前的范式为新范式提供了一个平台，这种情况在库恩谈到的科学范式转换中很少出现。模型的传递性使这一切成为可能。

然而，也存在一些失败的范式转换。例如，在 20 世纪 80 年代，一些大学研究项目和初创公司尝试用数据流计算机颠覆当时的计算机行业，其中，数据流计算机提供了一种完全不同的方法来定义指令集体系架构（阿尔温德等，1991）。这些尝试都以失败告终。而人工智能（AI）作为一个领域的反复失败也许是一个更奇怪的案例。人工智能历经了好几个繁荣和萧条的发展周期，在这几个周期里，人们对它的狂热总是伴随着幻想的破灭和投资的失败。从 20 世纪 80 年代末开始，人工智能领域就经历了被该领域的一些研究人员称为「人工智能的寒冬」的阶段，它暗示了一个核冬天，直到 2010 年前后人工智能的发展才完全恢复。也许数据流计算机会以同样的方式复活。这样的失败很快就会从我们的记忆中消失（当然，那些与失败直接相关的人除外）。

然而，失败却是人工智能知识探索中一个正常和良性的过程。数字技术的迅速发展为范式的突变、适应和消亡提供了一个健康而繁荣的生态系统。一个新技术范式的失败并不是因为它有什么根本性错误。与科学范式不同，技术范式所秉承的并非真理式的标准，或是与物理世界的观察相一致的标准。相反，它们的存在往往取决于许多无形的因素，其中最重要的或许是，公众甚至工程师是否准备好接受这种范式。

### 6.4 Models in Crisis

Paradigm shifts in engineering are triggered primarily by crises of complexity and opportunity. These have been relentlessly driven for the last 50 years by the staggering advances in digital technology. They continue to be driven by the increasing interconnectedness of digital devices and penetration of computers into everything we use.

So where are the most pressing crises today? For this question, I can only speculate because I cannot see the future any better than anyone else. But I do see at least two substantial crises looming.

Let me start with a crisis of opportunity. With increasing interconnectedness comes rapidly increasing volumes of data about the state of the world, society, and individuals in society. For example, credit card companies already carefully track most of our purchases, missing only the ones where we pay cash. These companies construct models of our behavior and use those models for various purposes, including to disallow transactions that appear to be anomalous and hence may be fraudulent. For example, if you don't travel much, and a store in China tries to charge a purchase to your credit card, then the transaction is likely to be denied by the credit card company's computers. If you travel a lot, as I do, however, then this same transaction is more likely to be allowed. If you normally buy expensive scotch at boutique stores, then a purchase of Rotgut Moonshine at a store called Payroll Loans & Liquor is also likely to be denied.

These decisions are not made by humans; they are made by computers, the ones that dream (see section 5.6 ). The computers are running machine-learning algorithms that build models of your behavior by observing your transactions and then classify each subsequent transaction as anomalous or normal based on the probability that the model would generate such behavior.

The credit card example exhibits a contradiction that is common in big data applications. Although we probably appreciate that the credit card company attempts to prevent fraudulent use of our card, many of us find it creepy that the company has built a probabilistic model of our behavior. Similarly, we may like that a map app on our smartphone tells us about nearby restaurants, but we are likely not thrilled to learn that, as a consequence of using the app, Google's computers know where we are.

Now imagine that the computers in your car begin to communicate with the outside world. Some insurance programs already use such communicated information to vary your insurance bill based on usage and style of driving. What if the insurance company sells the information they get from your car to your credit card company? Metcalfe's law is based in part on the observation that aggregated data is more valuable than isolated data. The credit card company may now verify that your car is indeed parked at Payroll Loans & Liquor and either allow the transaction or report your car stolen.

The data being gathered about us by various organizations is growing at a staggering rate. In the United States, privacy laws intended to protect us from misuse of that data are ineffective because these laws have simply resulted in a barrage of small print that every organization is now required to throw at you, knowing that you will not read it. In fact, the U.S. government has exhibited a distinctly double standard, simultaneously trying to strengthen privacy laws and prevent encrypted data communication. Encryption, the government says, interferes with its ability to detect and prevent potential terrorist attacks. Indeed, it no doubt does. Again, we are faced with contradictory requirements.

Many organizations today are collecting but not effectively using vast amounts of data. Consulting and market research company Gartner calls「dark data」the「information assets that organizations collect, process and store in the course of their regular business activity, but generally fail to use for other purposes.」The subtext is that those same businesses are missing an opportunity. They should be mining the data. The data has value.

The research and consulting firm Forrester defines「perishable insights」as「urgent business situations (risks and opportunities) that firms can only detect and act on at a moment's notice.」Fraud detection for credit cards is just one example of such perishable insights. Once the transaction is allowed, the damage is done. We also saw another example of a perishable insight in chapter 1 in the Wikipedia vandalism detection algorithm, although that one has less privacy cost. More dramatically, dark data in health care and medicine could be much better used to get (literally) perishable insights.

I believe a crisis of opportunity exists today in converting data feeds into insights in time to make effective use of them while either ensuring privacy or at least preserving public trust that the loss of privacy will not be abused. Clearly, this problem is not just technical.

Contradictory requirements demand innovation. Consider that thermostats, door locks, television sets, watches, running shoes, football helmets, books, and, in fact, nearly everything around us is going online. And many devices are acquiring the ability to listen for spoken words and react to those words. And when you read an electronic book, it reads you back. Connecting those devices to the network is likely to deliver real value to us, including, for example, reducing our carbon footprint and vulnerability to terrorists. These potential benefits cannot be ignored. Neither can the risks. The situation is crying for a paradigm shift.

The second crisis I see looming is a crisis of complexity. This crisis is not just about increasing numbers of components but rather about the conjoining of engineered systems that have traditionally used different kinds of models to manage their own complexity.

Consider a modern commercial airplane such as the Airbus A350 or the Boeing 787. These systems are software-intensive with hundreds of microprocessors managing functions that include translating pilot commands into rudder movements, controlling the landing gear, managing cabin pressurization and airflow, managing electric power generation and distribution, and operating the passenger entertainment system. Such an aircraft is a much more complex system than, say, a data center handling Facebook pages. The latter only has to deal with bits and the heat generated by processing those bits. A data center is an information-processing system that can operate almost entirely within the models and paradigms of computer science. But an airplane design conjoins models of aeronautical, mechanical, electrical, and civil engineering, as well as those of computer science. In such a system, the structures of civil engineering interact with the flight dynamics of aeronautical engineering under the control of a software system (computer science) running a feedback control system (electrical engineering). The silos of specialization that are standard in engineering today become an obstacle because the models and paradigms developed in each of these disciplines are incommensurable.

Despite the enormous complexity and challenges of crossing so many silos, Boeing and Airbus both manage to make astonishingly safe and reliable airplanes. How? Today, their design processes and methods are extremely conservative, and regulatory oversight is heavy. Many rules must be followed to get an aircraft certified to carry civilian passengers.

However, these processes reveal some fundamental flaws in the engineering models and methodologies that are available today to aircraft engineers. A symptom of such flaws is a story I first heard from an engineer who had worked on the Boeing 777. This was Boeing's first fly-by-wire airliner, meaning that pilot controls are mediated by a computer. The 777 first entered into service in 1995. According to this engineer, as of the early 1990s, Boeing expected this model of aircraft to be in production for perhaps 50 years, to 2045. The engineer told me that in the early 1990s, Boeing purchased a 50-year supply of the microprocessors for the flight control system so they could use the same microprocessors for the entire production run of the aircraft.

Recall in chapter 4 my observation that hardware is ephemeral. In fact, any particular silicon chip is unlikely to remain in production for more than a few years. It becomes obsolete quickly under the pressure of Moore's law. And when a fab gets updated to leverage a new technology, such as the FinFET, it becomes impossible to produce an identical chip.

But why does Boeing need the chip to be identical? The whole point of the layering of paradigms of figure 3.3 is so that software designs are isolated from changes in the hardware. It should be enough to use any chip that can correctly execute the software for the control system.

But the flaw is in the notion of correctness. Starting at the instruction set architecture layer in figure 3.3 , and for all layers above that, what it means to correctly execute software has nothing to do with how long it takes to do anything. Timing of actions is not part of the programming paradigms used today.

But in a flight control system, the software is directly controlling physical actuators, and in the physical world, timing is important. In fact, in just about every model that an aeronautical, mechanical, or electrical engineer will use, timing of actions is central to the model. The paradigms used by these engineers are incommensurable with the paradigms used by computer scientists.

As a consequence, the layering of figure 3.3 fails to provide adequate abstractions, and hence fails to provide separation of concerns. Boeing is forced to operate without any layering, and hence has to ensure that every airplane carries exactly the same design all the way down to the semiconductor physics layer.

I have subsequently heard similar stories from engineers at Airbus, which has been making fly-by-wire aircraft for longer than Boeing. The engineers at Airbus tell me that they store the microprocessors in liquid nitrogen in an attempt to extend their shelf life by slowing down the natural diffusion processes of the dopants in the silicon.

The complexity of aircraft designs keeps increasing. A key objective in aircraft design is to decrease weight because this reduces fuel consumption, extends range, and improves the carbon footprint. One way to decrease weight is to use more advanced materials in the airframe and more flexible structures. But flexible structures require more tightly coordinated control systems. Timing discrepancies in control systems can create disastrous stresses on airframe structures.

Another way to decrease weight is to reduce the amount of wiring and hydraulic piping. This can be accomplished with more advanced networking, but essentially all of the layers in the OSI model of figure 6.3 above the physical layer also ignore timing, just like the software layers in figure 3.3 . As a consequence, aircraft manufacturers are unable to benefit from most of the advances in networking of the last 40 years.

Even with a fixed microprocessor, the fact that timing is irrelevant to correctness from the ISA up means that in software design, aircraft manufacturers also cannot use most of the innovations of computer science from the last 40 years. The FAA prohibits use of object-oriented languages, for example, in safety-critical software. Even interrupts, the standard way that all modern microprocessors get data in and send data out to the outside world, are prohibited. To be sure, interrupts create many subtle software problems. As far back as 1972, Edsger Dijkstra lamented,

[I]n one or two respects modern machinery is basically more difficult to handle than the old machinery. Firstly, we have got the interrupts, occurring at unpredictable and irreproducible moments; compared with the old sequential machine that pretended to be a fully deterministic automaton, this has been a dramatic change, and many a systems programmer's grey hair bears witness to the fact that we should not talk lightly about the logical problems created by that feature. (Dijkstra, 1972)

Despite this lament, to this day, interrupts remain the primary method for I/O and are central to every modern operating system design. Aircraft manufacturers, therefore, are also excluded from the last 40 years of advances in operating systems.

In view of the failure of most computer science innovations of the last 40 years to address the needs of aircraft designers, I am astonished at their remarkable safety track record. I have enormous respect for the engineers who design these planes. They are stuck with the prototype-and-test style of design that was used by Edison, unable to leverage the transitivity of models, and their prototypes are much more complex than Edison's prototypes.

Figure 6.4 shows a prototype of an Airbus A350, their newest model. Airbus calls this prototype an「iron wing.」The prototype includes all parts of an A350 except the airframe, cabin, and engines. This is why it doesn't look like an airplane. It is the guts without the skeleton or skin. The wiring is all exactly the same length as on the real aircraft. The hydraulic tubes are bent as on the real aircraft to get around the (missing) airframe structure. When running tests using this prototype, the same generators that are driven by the engines on the real aircraft are driven by artificial engines so that the prototype runs on its own power. This prototype is obviously much more complicated than Edison's lightbulbs, but it is exactly the same sort of concrete prototype.

Figure 6.4 An Airbus「iron wing」prototype of an A350.

Aircraft manufacturers are not alone in facing this problem. Modern cars are mostly「drive-by-wire」today, where the driver commands (pushing on the accelerator and brakes and turning the steering wheel) are mediated by a computer before going to the wheels or engine. Automotive designers face the same problems but with far fewer regulatory constraints. Their problems are only going to get worse as automation increases (lane keeping, automated accident prevention, and fully automated driving).

It doesn't stop there. Any modern factory is computer controlled and is similarly a safety-critical system where the timing of actions is essential to safety. Trains are computer controlled. Ventilation, lighting, and fire mitigation systems in buildings are computer controlled. Modern electric power grids, water distribution systems, and communication systems are computer controlled.

In 2006, Helen Gill of the U.S. National Science Foundation coined the term「cyberphysical systems」(CPS) for such systems that combine computing, networking, and physical dynamics. There is clearly today a crisis of complexity for such systems. She launched a major NSF initiative to fund research to address precisely the problems that I have indicated. This program continues, and progress is being made, albeit still primarily in research labs and not yet in industrial production. Gill recognized that conjoining the「cyber」world with the physical world created an enormous crisis of complexity, one that the existing paradigms were poorly equipped to deal with.

What is the origin of the term「cyber」in CPS? The related term「cyberspace」is attributed to William Gibson, who used the term in the novel Neuromancer , but the roots of the term CPS are older and deeper. It would be more accurate to view the terms「cyberspace」and「cyberphysical systems」as stemming from the same root,「cybernetics,」which was coined by Norbert Wiener (Wiener, 1948), an American mathematician who had a huge impact on the development of control systems theory. During World War II, Wiener pioneered technology for the automatic aiming and firing of anti-aircraft guns. Although the mechanisms he used did not involve digital computers, the principles are similar to those used today in computer-based feedback control systems. His control logic was effectively a computation, albeit one carried out with analog circuits and mechanical parts, and therefore cybernetics is the conjunction of physical processes, computation, and communication. Wiener derived the term from the Greek word for helmsman, governor, pilot, or rudder. The metaphor is apt for control systems.

The term CPS is sometimes confused with「cybersecurity,」which concerns the confidentiality, integrity, and availability of data and has no intrinsic connection with physical processes. The term「cybersecurity,」therefore, is about the security of cyberspace and is thus only indirectly connected to cybernetics. CPS certainly involves many challenging security and privacy concerns, but these are by no means the only concerns.

My own research at Berkeley includes some examples of NSF-funded research projects under the CPS program. One project that concluded in 2015, called the PRET project (for Performance with Repeatable Timing), designed an instruction set architecture that explicitly includes timing within its programming paradigm. In effect, this project reopened decisions that Fred Brooks made all the way back in the 1960s when he designed the System/360 ISA without any explicit control over timing. The project concluded with a demonstration that it is possible to achieve precise control over timing with no loss of performance and modest cost in hardware. If this architectural approach is adopted in industry, it will enable separation of concerns in the layering of figure 3.3 for cyberphysical systems.

A second example from my research group is a project we called PTIDES, which also concluded in 2015. This project addressed software that is distributed across networks, using the OSI model of figure 6.3 , but modifying the paradigms to explicitly control timing. But I will spare you the details.

Despite progress in the research labs, the crisis of complexity remains for cyberphysical systems, and the crisis of opportunity remains for data science. In the remaining chapters, I examine just how far we can push the layering of models. All the techniques we know of today have limitations, and understanding these limitations is essential to a complete understanding of technology revolutions. These limitations hint at opportunities for innovation.

6.4 危机中的模型

工程领域的范式转换主要是由复杂性和机遇引发的。在过去的 50 年里，数字技术的惊人进步极大地推动了范式的转换。数字设备日益互联的发展趋势以及计算机越来越渗透到我们日常生活中的现实，都成为工程领域范式转换的巨大驱动力。

那么，今天最紧迫的危机又在哪里？对于这个问题，我只能试着加以推测，因为在这个问题上，我的眼光并不比其他人更为独到。但是，我确实看到了至少有两场重大危机即将来临。

让我先从危机谈起。随着互联性的不断增长，有关世界、社会以及社会中个人状态的数据会迅速增加。例如，除了无法追踪我们以现金方式消费的信息，信用卡公司已经能够详细了解我们的大部分消费行为了。这些公司为我们的消费行为建立了模型，并将这些模型用于各种目的，包括可以禁止疑似欺诈的异常交易。例如，如果你不经常旅行，可是外国的一家商店试图从你的信用卡中扣除购物费用，那么信用卡公司的计算机可能会拒绝这笔交易。相反，如果你像我一样经常出差，那么同样的交易更有可能被允许。如果你经常在精品店购买昂贵的威士忌，那么你要是在 Payroll Loans &Liquor 这样的商店购买劣质酒的话，这笔交易同样有可能被拒绝。

上述这些决定不是由人类做出的，而是由那些会做梦的计算机做出的（详见 5.6 节）。计算机正在运行机器学习算法，它们通过观察你的交易状况构建你的行为模型，然后根据模型生成此类行为的概率，将每个后续的交易归类为异常和正常两类。

信用卡的例子展示了大数据应用中常见的矛盾。虽然我们非常理解信用卡公司这样做是为了防止客户的信用卡被盗刷，但是，当我们中的许多人发现，信用卡公司已经建立了我们行为的概率模型时，这将令人有些毛骨悚然。同样，我们可能会喜欢智能手机上的应用程序，它能够告诉我们附近的餐馆，但是，由于使用了该类应用程序，谷歌的计算机就会知道我们的具体位置。我想多数人在了解到这一点之后，一定不会觉得特别开心。

现在想象一下，你车里的电脑可以与外界进行通信。实际上，一些保险计划已经通过这些信息归纳出你的驾车风格和用车状况，从而改变你的保单。如果保险公司把从你的汽车中得到的相关信息卖给了你的信用卡公司，又会怎样呢？梅特卡夫定律部分地基于这样一种观点，即聚合数据比孤立数据更有价值。信用卡公司现在可能会核实你的车是否就停在 Payroll Loans & Liquor 商店外面，之后要么允许这笔买酒的交易，要么向警察局报告你的车被盗了。

各类机构都在以惊人的增长速度收集着与我们个人有关的各项数据。在美国，原本旨在保护我们私人数据不被滥用的隐私法变得徒劳无效了，因为这类法律只不过导致了大量印着密密麻麻小字体的法律文件的产生。现在，政府要求每个机构都必须向你出示这样的文件，当然，也很清楚你并不会去阅读这些文件。事实上，现在美国政府表现出明显的双重标准。它一方面试图加强隐私法的力度，同时又阻止加密的数据通信。政府表示，加密会干扰其侦测和防止潜在的恐怖袭击的能力。的确如此，这一点毫无疑问。

同样，我们再次面临相互矛盾的要求。

今天，许多机构都在收集大量的数据，但并没有有效地使用它们。咨询和市场研究公司高德纳将「机构在日常商业活动过程中收集、处理和存储的，但通常又不能用于其他目的信息资产」称为「暗数据」。其潜台词是这些企业正在错失一个机遇。它们应该好好挖掘这些数据，因为这些数据是非常有价值的。

从事研究和咨询的公司弗雷斯特将「稍纵即逝的洞察力」定义为「企业只有在得到通知后才能察觉和采取行动的各种紧急的商业情况（如风险和机会）」。信用卡欺诈检测只是这种稍纵即逝的洞察力的一个例子。交易一旦被允许，损失就会形成。我们在第 1 章还看到另一个稍纵即逝的洞察力的例子，是维基百科关于恶意破坏的检测算法，尽管这个例子的隐私成本更低。更引人注目的是，医疗和医药领域的暗数据可以被更好地用来获得（实实在在的）稍纵即逝的洞察力。

我相信，在及时将输入的数据转化为洞察力以有效利用它们的同时，确保隐私或者至少是保持公众的信任（隐私的丧失不会被滥用），是一个存在着机遇的危机，显然这个问题不仅仅是技术性的。

这些矛盾的要求呼唤着创新。让我们想想看，恒温器、门锁、电视机、手表、跑鞋、橄榄球头盔、书籍等等，我们周围几乎所有东西都被接入互联网。许多设备正在获得听取口语指令并对其迅速做出反应的能力。当你读一本电子书时，它也在阅读你，了解你的个人信息。将这些设备接入网络可能会给我们带来真正的价值，例如，减少我们的碳排放量和相对于恐怖分子的脆弱性。这些潜在的好处不容忽视。当然，其中的风险也不可小觑。这种情况迫切需要范式的转换。

我看到的第二个危机是一场复杂性的危机。这场危机不仅关系到组件数量的增加，而且关系到传统上使用不同模型来管理自身复杂性的工程系统的结合。

以现代商用飞机如空中客车 A350 或波音 787 为例，这些系统都是软件密集型的，拥有数百个微处理器以实现不同的功能，包括将飞行员的指令转换为舵机运动、控制起落架、管理机舱的增压和气流、管理发电和配电以及运行乘客娱乐系统等等。这样的飞机系统比处理脸书页面的数据中心要复杂得多。后者只需要处理比特数据以及因处理这些数据而产生的热量。数据中心是一个信息处理系统，它几乎完全可以在计算机科学的模型和范式中运行。但是，一架飞机的设计结合了航空、机械、电气和土木工程的模型，以及计算机科学的模型。在这样一个系统中，土木工程的结构与航空工程的飞行动力学在运行反馈控制系统（电气工程）的软件系统（计算机科学）控制下相互作用。在今天的工程体系中，专业化的「竖井」是标准的，这已成为一个障碍，因为每个学科开发的模型和范式是不可通约的。

尽管跨越如此多的「竖井」存在着巨大的复杂性和挑战，但波音公司和空客公司都设法成功地制造了安全可靠的飞机。它们是怎样做到这一点的呢？今天，它们的设计过程和方法都非常保密，并且监管很严格。想要获得运载民用乘客的许可证，必须严格遵守许多规则。

然而，这些过程揭示了工程模型和方法上的一些根本缺陷，这些缺陷对今天的飞机设计工程师而言仍然存在。这些缺陷中的一个问题是我从一位工程师所讲的故事中第一次得知的，这位工程师曾参与了波音 777 的设计工作。波音 777 是波音公司研制的第一架电传控制飞机，这意味着飞行的控制是由计算机实现的。波音 777 于 1995 年首次投入使用。根据这位工程师的描述，早在 20 世纪 90 年代初，波音公司就预计这种型号的飞机将生产 50 年，直至 2045 年。这位工程师告诉我，20 世纪 90 年代初，波音公司为飞行控制系统的制造购买了可用 50 年的微处理器，这样就可以在飞机的整个生产过程中使用相同的微处理器了。

请大家回想一下，我曾经在第 4 章提到硬件是短暂的。事实上，任何一种硅片的生产都不可能持续几年以上。在摩尔定律的压力下，它很快就会过时。当一家晶圆厂利用一项新技术（如 FinFET）更新其产品时，它就不可能再生产相同的芯片了。

但是，为什么波音公司需要相同的芯片呢？图 3.3 所示的范式分层的全部要点在于，使软件设计与硬件的变化分离开来。这样的话，使用任何能够正确执行控制系统软件的芯片就足够了。

但是，缺陷存在于正确性的概念上。从图 3.3 所示的指令集体系架构层开始，对于上面的所有层而言，正确执行软件的意义与其所要执行的动作所需的时间无关。动作的定时特性并未被包含在今天所使用的编程范式中。

但是在飞行控制系统中，软件直接控制物理执行器，而在物理世界，时间是很重要的因素。事实上，在航空、机械或电气工程师所要使用的每个模型中，动作的执行时间都是模型的核心。然而，这些工程师使用的范式与计算机科学家使用的范式是不可通约的。

因此，图 3.3 所示的分层未能提供足够的抽象逻辑，由此也就无法提供对这些关注点的分离。波音公司被迫在没有任何分层的情况下运作，因此就必须确保每架飞机的设计直到半导体物理层的设计都是完全相同的。

后来，我从空客公司的工程师那里又听到了类似的故事。空客公司制造电传控制飞机的时间比波音公司还要长。空客的工程师告诉我，他们把微处理器放在液氮中储存，试图让含有掺杂物在硅的自然扩散过程中能够延长保质期。

飞机设计的复杂性不断增加。飞机设计的一个关键目标是减少重量，因为这可以降低燃料的消耗，延长航程，并减少碳排放量。减轻重量的一种方法是在机身上使用更先进的材料和更灵活的结构。但是，灵活的结构需要更紧致的协调控制系统。控制系统中的定时差异会对机身结构形成巨大压力。

另一种减轻重量的方法是减少线缆和液压管道的数量。这可以通过更高级的网络来实现。然而，实际上，就像图 3.3 中的软件层一样，图 6.3 OSI 所示模型中物理层以上的所有层都忽略了定时的问题。因此，飞机制造商无法从过去 40 年的网络发展中获益。

即使是使用一款相同的微处理器，时间与指令集体系架构的正确性无关这一事实，也意味着在软件设计中，飞机制造商不能使用过去 40 年来计算机科学的大部分创新成果。联邦航空管理局禁止在安全关键软件中使用面向对象的语言。甚至作为所有现代微处理器获取数据并将数据发送到外部世界的标准方式，中断这一机制也是被禁止的。可以确定的是，中断会产生许多棘手的软件问题。早在 1972 年，艾兹格·迪杰斯特拉就感慨道：

从一两个方面来看，现代机器基本上要比老式机器更难操作。首先，我们拥有中断，其往往发生在不可预测和不可复制的时刻；与以往那些看上去像是确定性自动机的老式连续型机器相比，这是一个巨大的变化，而且，许多系统程序员头顶的白发都证明了这样一个事实，即我们不应该轻率地谈论由该特性所产生的逻辑问题。（迪杰斯特拉，1972）

尽管如此，直到今天中断仍然是输入 / 输出系统的主要方法，并且也是每个现代操作系统设计的核心。因此，飞机制造商也被排除在过去 40 年操作系统的进步之外了。

鉴于过去 40 年大多数计算机科学创新都未能满足飞机设计者的需求这一事实，我对其卓越的安全航行记录感到非常惊讶。我非常崇敬设计这些飞机的工程师。他们受困于爱迪生所使用的原型 — 测试设计风格，无法利用模型的传递性，而且他们的原型要比爱迪生的原型复杂得多。

图 6.4 给出了空客公司最新型号 A350 飞机的原型。空客公司称它为「铁鸟」。该原型包含了一架 A350 飞机除机身、机舱和发动机之外的所有部件。这就是它看起来不像一架飞机的原因，它是没有结构和蒙皮的一些内部装置。其内部的线缆长度与实际的飞机完全相同。液压管也像在实际飞机上那样弯曲着，以绕过（缺失的）机身结构。当使用这个原型进行测试时，在实际飞机上由发动机驱动的发电机由人工发动机驱动，因此这个原型可以依靠自己的动力运行。显然，这个原型要比爱迪生的灯泡复杂得多，但它是相同类型的具体原型。

面临这一难题的不仅仅是飞机制造商。现代汽车大多也是「线传控制」的，驾驶员的指令（踩油门、踩刹车和转动方向盘等）在进入车轮或发动机之前都是由计算机控制的。汽车设计师面临着同样的问题，但受到的监管约束要少很多。随着汽车自动化程度的提高（如车道保持、自动事故预防和全自动驾驶等），汽车设计师面临的问题只会变得更加糟糕。

图 6.4 空中客车 A350 的「铁鸟」原型。

我们所面临的问题不止于此。所有的现代工厂都是由计算机控制的，是类似的安全关键系统，在这种系统里，动作的定时特性对系统的可靠安全性而言尤为重要。火车是由计算机控制的，建筑物的通风、照明和防火系统是由计算机控制的，现代的电网、供水系统和污水处理系统也是由计算机控制的。

2006 年，美国国家科学基金会的海伦·吉尔创造了「信息物理系统」（Cyber-Physical System，简写为 CPS）一词，指的是那些将计算、网络和物理动力学结合在一起的系统。如今，这类系统显然面临着一场复杂性的危机。海伦·吉尔发起了一项美国国家科学基金会的重大提案，资助相关研究，以解决我之前已指出的问题。这一计划仍在继续，而且正在取得进展，尽管这些进展主要还集中在研究实验室里，而不是工业生产中。吉尔认识到，将「赛博」（cyber，此处也译为信息）世界与物理世界结合在一起，导致了巨大的复杂性危机，而现有的范式很难应对这一危机。

CPS 中「赛博」一词的起源是什么？与此相关的术语「赛博空间」（cyberspace，也译为网络空间）是威廉·吉布森在小说《神经漫游者》中使用的词语，但 CPS 这个词的词根有着更深的渊源。

更准确的说法是，「赛博空间」和「信息物理系统」源自同一个词根，即由美国数学家诺伯特·维纳（维纳，1948）创造的「控制论」（cybernetics）。维纳对控制系统理论的发展有着巨大的影响。在第二次世界大战期间，他发明了高射炮自动瞄准和射击技术。虽然他所使用的设计机制不涉及数字计算机，但其原理与今天在基于计算机的反馈控制系统中所使用的原理相似。他的控制逻辑实际上就是一种计算，尽管它是用模拟电路和机械部件实现的，因此，控制论是物理过程、计算和通信的结合。维纳是由希腊语中的舵手、总督、驾驶员或方向等词得出这个名词的。这个比喻很适合控制系统。

CPS 一词有时会与「赛博安全」（cybersecurity，也译为网络空间安全）相混淆，后者涉及数据的保密性、完整性和可用性，与物理过程没有内在的联系。因此，「赛博安全」一词是关于网络空间的安全，只是间接地与控制论有关联。当然，CPS 涉及许多具有挑战性的安全和隐私问题，但这并不是我们唯一要关注的。

我在伯克利大学的研究包括一些由美国国家科学基金会资助的 CPS 研究项目。2015 年，我完成了一个名为 PRET 的项目（for Performance withRepeatable Timing，简写为 PRET，致力于实现可重复定时的性能）。该项目设计了指令集体系架构，其编程范式中明确包括了定时功能。实际上，这个项目重新开启了弗雷德·布鲁克斯在 20 世纪 60 年代所做的决策，当时他设计了 System/360 ISA 系统，该系统没有任何明确的定时控制。该项目最后进行了一次演示，表明在不损失性能和硬件成本适中的情况下，可以实现对定时的精确控制。如果在工业领域中采用这种体系结构方法，它将能够为信息物理系统进行图 3.3 所示分层中的关注点分离。

第二个例子是我们课题组的 PTIDES 项目，也是在 2015 年完成的。该项目使用图 6.3 所示的 OSI 模型，解决了跨网络的分布式软件问题。但是，该项目修改了范式，以显式地控制定时。具体细节不再赘述。

尽管相关研究已在实验室里取得了一定的进展，但信息物理系统中的复杂性危机仍然存在，而数据科学的机遇危机也依然存在。在后续的章节中，我将进一步探究我们能够在多大程度上推进模型的分层。我们今天所掌握的所有技术都有其局限性，了解这些局限性对于全面理解技术革命至关重要，因为这些局限性也蕴含了创新的机会。
