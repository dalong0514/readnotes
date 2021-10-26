## 1201. Final Thoughts

· · · in which I tie it all together, analyze what is holding back technology advancement, and suggest some areas where holding back might not be a bad idea.

1201 最终的想法

这一章我将把所有这一切都联系在一起，分析是什么阻碍了技术的进步，并会说明在一些领域里出现某些阻碍因素或许并不是什么糟糕的事情。

### 12.1 Dualism

The few readers who have gotten this far (thank you!) are probably wondering how I have avoided mentioning Descartes'dualism, the mind-body separation. I've built a whole story about how layers of modeling result in a divorce between software and the physics on which it runs. Software is a model, and I've repeatedly cautioned against confusing the model with the thing being modeled, the map with the territory. A map is a model, and the territory is the physical world being modeled. Isn't my stance the Cartesian dualism all over again, where I've just replaced「mind」with「model」?

A model is physical, in both its physical form as in a paper map and in its mental form, our human conception of a map. Mental states exist in a physical brain. Take away or damage the brain, and the mental states vanish. So even the mental form is physical. Some philosophers call this point of view「physicalism.」It holds that all phenomena in the world, including mental states, arise from physical processes. I caution the reader, however, against assuming that this means we can explain all physical phenomena. We can't, but even without being able to explain it, everything is physical, and no fundamental mind-body dualism exists.

To a scientist, the inability to explain the physical world is profoundly disconcerting. It undermines the positivist agenda. To「explain」a physical phenomenon, according to the positivist philosophy of science, is to construct a (preferably formal or mathematical) model of that phenomenon, a「theory.」Following Popper, the theory must be falsifiable by experiment. But Gödel has shown that any formal system capable of self-reference 1 will be either incomplete or inconsistent ( chapter 9 ). Hawking points out that any explanation of physical phenomena takes the form of mental states that live in the very physical world that they explain. Thus, any theory that explains all physical phenomena must be capable of self-reference and hence will be either incomplete or inconsistent. Hawking argues that all the models we have of the physical world today are both incomplete and inconsistent.

Reinforcing Hawking and Gödel, Wolpert uses a similar self-embedding to conclude that predicting the future is impossible even in a deterministic world ( chapter 10 ). Even basic mathematics becomes suspect. Popper struggled with reconciling the truth of mathematical equations with his falsifiability criterion for science ( chapter 1 ). Consider the equation 1 + 1 = 2. Can any imaginable experiment falsify this equation? If not, then according to Popper's theory, the equation is not a scientific theory.

Tarski elaborated Gödel's incompleteness to show that no formal system capable of self-reference can define its own notion of truth ( chapter 9 ). If you combine this result with the premise that the physical world can be modeled formally, the essential positivist agenda, then there can be no notion of truth in the world. Positivism collapses into a steaming pile of negativism.

But I am an engineer not a scientist. I work in Simon's「sciences of the artificial」( chapter 1 ). I am glad some scientists are trying to model the natural world in great detail, but that is their agenda not mine. In my world, self-reference is a source of power not a source of weakness. For example, we can use software to build simulation models of semiconductor physics to improve the design of the transistors that ultimately run the software.

I don't need to explain everything in the physical world. In fact, quite the contrary. My agenda is to create things that have never before existed in the physical world. You have to admit that it would be hard to explain things that don't yet exist. I simply don't buy the Platonic extreme which assumes that all those things already exist in some separate reality and are just waiting to be discovered ( chapter 1 ).

The self-scaffolding that arises when there are many layers of separation from the physical reality, as there are in digital technology ( chapters 4 and 5 ), gives us no small measure of freedom to create. As humans, thinking machines, we can pretend that we operate in an artificial world of models, separate from physics, use our imagination, and invent clever artifacts and even whole new paradigms. Such new paradigms layer further abstractions on top of the existing ones ( chapter 6 ), furthering the illusion of model-body separation and enabling yet more creativity. Even if those abstractions have limitations, as the notion of computation does ( chapter 8 ), there are far fewer limitations to the semantics that we, as humans, can associate with these abstractions ( chapter 9 ). This bootstrapping of models and the endless possibilities for their meanings are fundamentally powerful and rely on self-reference. Arguably, the very incompleteness of self-referential systems is what enables creativity. It ensures that we will never be finished.

Once we recognize that technology is fundamentally a creative enterprise and a partnership between man and machine, then the personalities and idiosyncrasies of the creators of any particular technology become important. We must not treat technologies as dry Platonic facts that have always existed in some other world, waiting to be discovered. Instead, they are cultural, dynamic ideas, subject to fashion, politics, and human foibles. To me, this makes technology much more interesting.

As cultural artifacts, technologies evolve through collective mutation, through design and invention, more than through discovery. Discovery implies an event, the Aha! moment where some preexisting fact becomes known to an individual. The discoverer may be much heralded for a contribution to humanity, but the presumption is that the discoverer as an individual is irrelevant to the fact that has been discovered. Invention and design are not like that. They are less likely to be discrete events, Aha! moments, and they are more likely to come about, like many cultural forces, through the contributions of a large number of people.

To be effective, large numbers of people building collective wisdom must operate within a common mental framework, a「paradigm」to use the word of Thomas Kuhn. Kuhn's paradigms provide the conceptual framework for scientific thought, and Kuhn's theory is that science progresses more through paradigm shifts than through accretion of knowledge. As with science, in technology, common paradigms enable collective development of technologies and interoperability of technologies. Also as with science, paradigm shifts disrupt the equilibria. Accretion of knowledge, normal engineering, coexists with technology revolution, paradigm shift, a process of punctuated equilibrium, to use a term from evolutionary biology.

However, differences in the role of paradigms in science versus engineering do exist. Paradigm shifts are relatively rare in science, for example, Newton's mechanics, Einstein's theory of relativity, and quantum theory. In technology, however, paradigm shifts are relatively frequent. Consider, for example, the richness of styles of programming languages ( chapter 5 ) and their radically different perspectives on computation. Each constitutes a paradigm, and acceptance of that paradigm is necessary to build technologies using those languages.

Of course, a programming language reflects a relatively small paradigm that adheres to a bigger, more durable paradigm. The notion of computation, as developed by Turing, Church, von Neumann, and others during the twentieth century, constitutes a paradigm that persists over time scales more comparable to scientific paradigms. Paradigm shifts coexist with more stable paradigms, a process enabled by the deep layering of paradigms, where one is built on another. There is much less such layering in science, resulting in less frequent and more disruptive paradigm shifts. To be effective, technologists must accept disruption, and to be innovative, technologists must embrace and even seek disruption.

Because of the layering of paradigms, perhaps ironically, the stability of a paradigm at one layer can facilitate change at another layer. For example, because instruction set architectures have changed little in 40 years, they provide a stable platform that decouples the astonishing advances in the underlying semiconductor technology from the creative invention of new programming languages. The relatively stable intermediate layer enables rapid progress in both the layer below and the layer above by insulating these layers from one another.

Scientific paradigms get institutionalized through textbooks, courses, conferences, and a common culture. So do technology paradigms, but in addition, the technology may encode its own paradigms. We particularly see this in software, where, for example, compilers, which translate programs written in a programming language into machine code, can be written in the very languages they compile. This self-scaffolding of paradigms is part of what enables a deep layering because paradigms become precise enough to be built on with confidence.

Digital technologies, layered from the semiconductor physics of transistors up through the sociotechnical phenomenon of Wikipedia and to the「collective, metazoan organism」of a server farm, have been particularly disruptive and powerful for several intertwined reasons. Their discrete and algorithmic nature makes deterministic models ( chapter 10 ) practical and useful. The fact that we can make transistors that switch discretely, on and off, abstracting the messy sloshing of electrons that underlies the physics, enables deterministic, formal, mathematical models with powerful analytical properties and repeatable behaviors. The fact that we can put billions of these transistors into tiny spaces and switch them on and off billions of times per second enables the construction of enormously complex behaviors out of what is ultimately trivially simple, on or off.

The power of digital technologies has created an enthusiasm about them that has spilled over into the world of physics and neuroscience, where legions of serious scholars are convinced that the universe and everything in it, including human cognition, is a Turing computation. But the set of all Turing computations is a tiny set, albeit an infinite one ( chapter 8 ). The sum total of all the things we can do with software is countable, and countable sets are the smallest of all infinite sets that we know about ( chapter 9 ). If we are to accept that nature has for some reason constrained itself to operate only in this smallest of all infinite sets, then we should insist, with great determination, on evidence. The evidence is not there, and we don't even know what sorts of experiments would supply that evidence ( chapter 11 ).

Although digital technologies are severely limited compared with what is likely possible in the physical world (unless we accept digital physics), they are nevertheless exceedingly powerful, particularly when combined with the human notion of semantics ( chapter 9 ). In fact, I claim that there are much more serious obstacles to overcome than the intrinsic incompleteness of these models. I examine these obstacles in the next section.

12.1 二元论

坚持读到这里的少数读者（谢谢！）可能想知道我是如何避免提及笛卡儿的二元论的，即身心分离。如前所述，关于建模分层如何导致软件和支撑其运行的物理硬件相分离，我已经构造了一个完整的故事。软件其实就是模型。我已经在本书中反复强调过，不要把模型与被建模的事物，或者不要将地图和地域混为一谈。地图是一个模型，而地域代表了被建模的物理世界。难道我的观点不再是笛卡儿式的二元论了吗？我只不过是用「模型」代替了「心智」。

模型是具有物理性的，无论是纸质地图的物理形式，还是人脑中的地图概念。精神状态存在于生理上的大脑当中。

一旦大脑消失或者被损坏，精神状态也就随即消失了。所以说，就连精神形态本身也具有物理性。一些哲学家称这种观点为「物理主义」。该观点认为，世界上的一切现象，包括精神状态在内，都是由物理过程产生的。然而，我需要提醒读者，不要认为这就意味着我们可以解释所有的物理现象，实际上我们无法做到。但是即使无法解释一切物理现象，它们也是物理的，根本不存在身心对立的二元论。

对一位科学家来说，无法解释物理世界将令他们深感不安，因为这会破坏实证主义的常规做法。按照实证主义的科学哲学，要「解释」一种物理现象，就要为这种现象构建一个（最好是形式化的或数学的）模型，即一种「理论」。由波普尔的观点，这一理论必须通过实验的证伪。但是哥德尔已经证明，任何能够自我参照的形式系统要么是不完备的，要么是不相容的（详见第 9 章）。霍金指出，任何对物理现象的解释，都采用了存在于它们所解释物理世界中的精神状态的形式。任何解释所有物理现象的理论都必须能够自我参照，因此这些理论要么是不完备的，要么是不相容的。正如霍金指出的那样，现在我们拥有的物理世界的所有模型都是不完备且不相容的。

沃尔珀特利用类似的自嵌入方式得出一个结论，即使在一个确定性的世界里，预测未来也是不可能的事情（见第 10 章）。甚至，连基础数学也变得令人怀疑。他的观点强化了霍金和哥德尔的立场。波普尔曾努力调和数学方程中的真理与他的科学可证伪性标准（见第 1 章）。我们来看 1+1=2 这个等式。有没有任何可以想到的实验能够证伪这个等式呢？如果没有，那么根据波普尔的理论，这个等式就不是一个科学理论。

塔尔斯基详细地阐述了哥德尔的不完备性，以表明任何能够自我参照的形式系统都不能定义它自己的真理概念（见第 9 章）。如果你把这一结果与物理世界可以被形式化建模（这是实证主义的基本主题）这一前提结合起来，世界上就不可能存在真理的概念了。实证主义崩塌成了一大堆的否定主义。

然而，我是工程师，不是科学家。我在西蒙所说的「人工科学」（见第 1 章）范畴里工作。我很高兴一些科学家正在试图为我们详细地建模自然界。但是，这只是他们的工作主题，而并非是我的。在我的世界里，自我参照是力量的源泉，而非软弱的来源。例如，我们可以使用软件来建立半导体物理的仿真模型，以改进最终运行该软件的晶体管的设计。

我不需要解释物理世界中的一切。事实上，恰恰相反，我的计划是要创造物理世界中从未存在过的东西。你必须承认，要去解释尚未存在的事物是非常困难的。只是，我不相信柏拉图式的极端观点，极端地认为所有这些事物都已经存在于某个独立的现实中，正等着被发现（详见第 1 章）。

就像数字技术里的情形一样（见第 4 章和第 5 章），当存在许多从物理世界分离的层次时，数字技术就会出现自我支撑，这赋予我们发挥自由创造的巨大空间。作为人类，思考的机器，我们可以假想我们是在一个由模型组成的人工世界中运行，我们独立于物理世界，运用我们的想象力，发明智能的人工制品甚至是全新的范式。这些新的范式层在现有范式层的基础上进一步抽象（详见第 6 章），进一步加深了模型 — 实体分离的现象，并激发出更多的创造力。即使这些抽象具有局限性，就像计算的概念一样（见第 8 章），对我们人类用来和这些抽象进行关联的语义的限制也会少得多（见第 9 章）。从根本上说，这种模型的自举及其意义的无限可能性是非常强大的，这些都依赖于自我参照。可以论证的是，自我参照系统的不完备性恰恰是激发创造力的源泉，它确保我们的创造永远不会终结。

一旦我们认识到技术从根本上来说是一种创造性的事业以及人与机器之间的伙伴关系，任何特定技术的创造者的个性和特质就会变得非常重要。我们绝不能把技术当作乏味的柏拉图式事实，认为它们存在于其他某个世界，正等待着被发现。相反，我们应该将技术视为文化的、动态的思想，它们受制于时尚、政治以及人类的局限性。对我来说，这样去理解会使技术变得更加有趣。

作为一种文化产物，技术是通过群体变异、通过设计与发明而不是通过发现不断进化的。发现仅意味着一个事件，即某个人在突然了解到某个预先存在的事实而发出惊叹「啊哈！」的那个时刻。发现者可能会被认为对人类有很大贡献，但假设是，发现者作为一个个体与被发现的事实无关。发明和设计不是这样的，它们不太可能是离散的事件。那些「啊哈！」的时刻和许多文化产品一样，更有可能是通过大量的人类贡献而产生的。

为了更为高效，大量建立集体智慧的人们必须在一个共同的思想框架内合作，用托马斯·库恩的话说就是同一个「范式」。库恩的范式为科学思维提供了概念性框架，而且库恩的理论认为，科学的进步更多是通过范式的转换而不是知识的积累达成的。与科学一样，在技术中，共同的范式使发展技术的集体开发和互操作成为可能。和科学一样，技术范式的转换也会破坏平衡。知识积累这一常态工程是与技术革命和范式转换（用进化生物学的术语说，是一个间断平衡的过程）并存的。

然而，范式在科学与工程中的作用确实存在差异。范式转换在科学领域相对罕见，例如，牛顿力学、爱因斯坦相对论和量子理论。然而，在技术方面，范式的转换则相对频繁。例如，我们来考虑编程语言风格的丰富性（见第 5 章）以及它们对计算的截然不同的视角，每一种语言都构成了一种范式，而接受该范式对于使用这些语言来构建技术是十分必要的。

当然，编程语言代表的是一个相对较小的范式，它依附于一个更庞大、更持久的范式。如图灵、丘奇、冯·诺依曼和其他人在 20 世纪发展起来的计算概念，就构成了一种与科学范式一样持久的范式。范式转换与更稳定的范式共存，这是一个由范式的深度分层所支持的过程，其中，一个范式是建立在另一个范式之上的。相较而言，在科学中这样的分层要少得多，这将导致出现频率低但破坏性更强的范式转换。要想更为有效，技术人员必须接受这种颠覆，要想创新，技术人员必须接受甚至是寻求颠覆。

也许具有讽刺意味的是，由于范式的分层，一个分层上的范式的稳定性可以促进另一分层上的范式发生变化。例如，由于指令集体系架构在这 40 年里几乎没有变化，它们便提供了一个稳定的平台，将底层半导体技术的惊人进步与新型编程语言的创造性发明成功地分离开来。相对稳定的中间层将这些层相互隔离，从而使得上下两层都能快速地发展。

科学范式通过教材、课程、会议和共同的文化被制度式地固化下来。技术范式也是如此。但除此之外，技术还可能编码自己的范式。我们在软件中尤其可以看到这一点。例如，将编程语言编写的程序转换成机器码的编译器，就能用它们所编译的语言来编写。这种范式的自我支撑是实现深度分层的一部分，因为范式已经变得足够精确，可以作为可信任的基础。

由于几个相互交织的复杂原因，数字技术，其分层从晶体管的半导体物理学到维基百科的社会技术现象，再到服务器集群的「群体后生生物」，已经具有特别大的破坏性和强大威力。它们的离散性和算法式特质使得确定性模型（详见第 10 章）更为实用和有用。我们能够制造抽象了物质中杂乱的电子流动且离散地进行开、关（导通、截至）操作的晶体管，这一事实使得确定性、形式化的数学模型能够拥有强大的分析属性和可重复行为。而我们可以将数十亿这样的晶体管放置到微小的空间，并以每秒数十亿次的速度打开或关闭它们，这一事实又使得我们能够基于极为简单的开关操作构造出极其复杂的行为。

数字技术的力量激发了人们对它们的热情。这种热情已经蔓延到物理学和神经科学领域。在那里，众多虔诚的学者相信宇宙和宇宙中的一切，包括人类的认知，都是一种图灵计算。然而，所有图灵计算构成的这个集合只是一个极小的集合，尽管它是无限的（见第 8 章）。我们可以用软件做的所有事情的总和都是可数的，而可数集合是我们所知道的所有无限集合中最小的（见第 9 章）。如果我们要接受大自然出于某种原因限制自身只能在所有无限集合中的这个最小可数集合上运行这种说法，那么我们应该提供强有力的证据。然而，这样的证据并不存在，我们甚至都不知道什么样的实验能够提供这样的证据（见第 11 章）。

虽然与物理世界中可能存在的事物相比，这些数字技术是非常有限的（除非我们接受数字物理学的存在），但它们仍然是极其强大的技术，特别是与人类的语义概念相结合时（见第 9 章）。事实上，我认为有比这些模型内在的不完备性更为严重的障碍需要克服。我将在下一节研究这些障碍。

### 12.2 Obstacles

The most serious obstacle to overcome is that, despite its amazing capabilities, the human brain is really quite limited. The fact is, we cannot remember as much as computers can. We cannot read as fast. We cannot perform calculations as fast, and we make many more errors. Nevertheless, in partnership with computers and networks, we can do amazing things, such as carry around in our pockets nearly everything humans have ever published.

Digital technology gives humans an astonishingly rich medium for creativity, rich enough that we are nowhere near saturating what can be done with today's technology, never mind tomorrow's. Creativity comes at its own rate, however, slowed again by our brain's propensity to be dominated by our unknown knowns ( chapter 2 ). We resist new paradigms, even as the technology makes possible a firehose of new paradigms ( chapter 6 ).

In digital technology, every layer of abstraction except the lowest, semiconductor physics, is a human invention. By the time we get through several layers of abstraction for hardware and then software, we are so many orders of magnitude removed from the physics that physics becomes almost irrelevant ( chapter 3 ). We enter the world of models, human-constructed abstractions. Software becomes more like mathematics and less like natural science, subject only to its own rules. To be sure, we need useful rules, but we need not insist that they not be self-referential. In fact, they must be self-referential to be expressive, as Gödel showed.

All of the modeling paradigms that humans have invented so far have limitations. Software can only perform「effective computation,」to use Turing's phrase, a tiny subset of the processes that are possible in the physical world ( chapter 8 ). Digital technology exists within only the smallest of the infinite sets identified by Cantor ( chapter 9 ). We can go beyond software and build machines that form a cyberphysical partnership, leveraging the strengths of each ( chapter 6 ). Partnering computers with other physical machines enables us to overcome other human limitations, such as our limited ability to communicate. We write with 10 slow fingers, and we speak using a mere 10 kilohertz of audio bandwidth. Physical machines have no such limitations. Think of the partnerships among artists, computers, digital displays, and the human visual system when you watch a computer-generated movie such as Avatar . These partnerships achieve a degree of human-to-human communication never before possible.

We will never be able overcome one killer limitation by ourselves: models are useful to humans only if humans can understand them. Although our brains are truly remarkable machines, they have enormous difficulty with models of even modest complexity and sophistication. There are no doubt models in this book that even the most learned reader will have some difficulty with because the span of specializations that I talk about is so vast. Yet what I talk about in this book barely scratches the surface. The models actually used by specialists in any of the areas I touch on are vastly more sophisticated and cognitively challenging than my oversimplifications might lead you to believe.

Specialization is necessary to enable sophisticated modeling because of our brains' limitations, but it comes at a cost. Kuhn observes that the「paraphernalia of specialization」(specialized journals, professional societies, technical conferences, academic departments, curricula) acquire a prestige of their own and create an inertia against new paradigms (Kuhn, 1962, p. 19). Thus, specialization creates resistance to change.

Because our brains can only fit so much, specialization leads to fragmentation, where insights in one specialty become inaccessible to the others. It can be quite difficult for scientists and engineers to work across specialties. Wulf, writing about Alexander von Humboldt, points out that Humboldt's integrative, cross-disciplinary approach to science went out of fashion ( chapter 2 ), leading to Humboldt being largely forgotten by the scientific community. She observes that「this growing specialization provided a tunnel vision that focused in on ever greater detail, but ignored the global view that would later become Humboldt's hallmark」(Wulf, 2015, p. 22).

With this tunnel vision, specialists know more and more about less and less, until they eventually know everything about nothing. Then they become professors, and the courses they teach become barriers, weeding out unsuspecting undergraduates who simply aren't prepared for the sophistication of the specialty. The professors love their specialty, they want to teach it, and they cannot see that it is esoteric; the arcane and complex analytical methods they have developed are neither easily learned nor easily applied to practical problems. Their discipline fragments into further specialties, and each professor loses the big picture. None is qualified to teach the big picture, and anyway, his or her colleagues would consider any such big picture to be「Mickey Mouse,」too easy and unsophisticated to be worthy of their time.

The fragmentation created by specialization is particularly damaging in view of the degree to which technology shapes and pervades our culture. Every person on the planet, regardless of his or her own intellectual predilections, is affected by technology. Yet many intellectuals discount the value of understanding technology. I do not see how a true humanist today can understand society without understanding technology. It seems to me that studying contemporary culture without technology is like studying literature without language. Yet that seems to be what many people do.

My own alma mater, Yale University, a paragon of the arts and sciences, is a case in point. In 1992, a few years after I graduated with a double major in Computer Science and what they called「Engineering and Applied Science,」Provost Frank Turner suddenly proposed to eliminate almost all of engineering at Yale.「Applied science」was, to Turner, an intellectual afterthought, not nearly as important as science itself. In his view, applying science was all that engineering did. The closure of engineering didn't happen, but it was dramatic at the time and created quite a firestorm among some of the alumni. Turner was a「historian of the ideas that shaped Western civilization,」according to a Yale News memorial published in 2010. Today, I don't see how you could possibly study the ideas that shape Western civilization without studying technology.

Yet technology is not easy to understand. We have probably all had the experience of feeling dumb when we can't figure out something about our computer or home network, and some wizard in India explains to us how to fix the problem. We feel as if we should have known what the wizard knows or should have been able to figure it out. Yet the wizard's knowledge is not about fundamental facts about the world. It is about the language and culture of a specific, idiosyncratic technology. In a pluralistic world, we can't all understand all the languages and cultures that exist. Each specialization has its own parochial gurus.

Specialization gets further amplified by the publish or perish mentality of academia. The most highly regarded publishable results in academic journals are the ones that solve long-standing open problems. In a more specialized field, it is much clearer what the open problems are. The open problems are harder to solve, so you get more respect for solving them. And only a long-standing specialty can have long-standing open problems. In interdisciplinary work and in work in an immature field, by contrast, often the real innovation comes from formulating a problem that has not been previously recognized. However, if the newly formulated problem turns out to be easy to solve, then any academic paper describing the solution will likely be rejected under peer review because the solution is「obvious.」

Even technology can slow innovation. Software has the rather remarkable property that it tends to encode its own paradigms ( chapter 5 ). When a new software paradigm emerges, it inevitably comes with a suite of languages and tools that quickly accumulate sufficient mass and complexity to become immovable. These make the paradigm durable but sometimes too durable.

On May 25, 2016, the U.S. General Accounting Office released a report stating that more than 70% of the U.S. government's information technology budget is spent on「operations of maintenance」rather than「development, modernization, and enhancement.」This amounts to about $65 billion per year, much of which is spent on outdated languages and hardware, some as much as 50 years old. The report cites U.S. Department of Defense use of 8-inch floppy disks and U.S. Treasury Department use of assembly code. Hardware, languages, and tools become an impediment to innovation because change is difficult.

Of course, all disciplines resist change. Kuhn says,「Normal science, for example, often suppresses fundamental novelties because they are necessarily subversive of its basic commitments」(Kuhn, 1962, p. 5). When the「basic commitments」become codified in a suite of million-line computer programs, the inertia can become even harder to overcome.

It is not just the technologists resisting change but also consumers of technology. Humans become used to a means of interaction with machines, and change can become impossible. For example, the brake and accelerator pedals on cars were designed at a time when these controls had direct mechanical and hydraulic couplings with the brakes and throttle. People learned to drive using these controls. Today, the pedals send commands to a computer, which mediates the commands, possibly changing them before passing them on to the brakes and throttle. For example, the computer may apply different amounts of braking to each wheel to improve stability and prevent skidding. In an electric car, instead of a single throttle, each wheel may have its own electric motor, and the computer may individually control these motors. If humans were to control each wheel with direct mechanical linkages, then the car would have to have eight pedals, four for the brakes and four for the accelerators, and only an octopus could drive.

Car manufacturers could have invented entirely new ways for humans to command the car, for example, using a joystick rather than a steering wheel, but such changes would be resisted by the customers. Humans learned to drive with the old style of controls, and unlearning something is often harder than learning something new. Consequently, car manufacturers today have to work pretty hard to design the pedals so that they feel as if they are connected directly to mechanical and hydraulic actuators. The pedals even push back the way a hydraulic control would, but it is likely that a computer rather than an oil-filled cylinder is determining how much to push back.

A prevalent but misleading view is that human-computer interfaces should be「intuitive.」There is nothing intuitive about the pedals in a car. There is nothing intuitive about interacting with a computer. All of the interaction mechanisms we use today are learned. I am reminded of an episode of the TV series,「Star Trek,」where the crew of the Enterprise travels back in time to the late 1980s. The engineer, Scotty, needs to use a vintage 1980s computer to solve a problem. So he starts talking to the computer:「Computer. Computer. Computer !」The computer, of course, does not respond. One of the vintage 1980s engineers picks up a mouse and hands it to Scotty, saying,「You have to use this.」Scotty, looking embarrassed, says,「Oh yes, of course.」He picks up the mouse and begins speaking into it as if it were a microphone:「Computer. Computer. Computer !」The computer mouse was a brilliant invention, and we have assimilated that paradigm, but there is nothing intuitive about it.

Unfortunately, the way we teach technology tends to ignore the inventive nature of technology. I use「we」here to refer to myself and my colleagues, professors at universities and institutes of technology. We teach technology as if it were a collection of facts and truths, Platonic Ideals that exist timeless and independent of humans, waiting to be discovered. A consequence of this style of teaching is that we reinforce the philosophy that values discovery over invention and invention over design ( chapter 1 ).

If what discoverers discover has already existed in the Platonic Good, then the discoverers should not be important as individuals. The discoverers' personalities and predilections cannot possibly have any influence on the nature of the facts and truths they discover. Kuhn observes that this tendency to disconnect ideas from their originators is「ingrained in the ideology of the scientific profession,」and he quotes Alfred North Whitehead, saying,「A science that hesitates to forget its founders is lost」(Kuhn, 1962, p. 138). If all worthwhile facts and truths are already out there, waiting to be discovered, then the most valuable contribution an individual can make is simply to bring into light some fact or truth that was previously in darkness.

When talking about technology rather than science, I couldn't disagree more with Whitehead. Almost all「facts and truths」about technology are actually human inventions. As it stands today, technology reflects a chaotic Darwinian evolution of sometimes quirky and idiosyncratic ideas. Understanding the origin of these ideas is essential to being able to think critically about them, and thinking critically about the ideas is essential to technology revolutions.

The fact that we value invention over design can also present an obstacle to creativity. The emphasis on novelty over quality, where「new is better than good,」is an academic rathole. No respected academic journal would have published a paper describing the iPhone because every element of the technology already existed in other products. Yet the iPhone was a momentous contribution to humanity, whereas the vast majority of what is published in academic journals is not.

Creative people capable of such contributions may be repelled by technology, perceiving the discipline of engineering as a trade, requiring professional training on well-understood techniques, applying methods known in science, and tweaking and optimizing existing designs ( chapter 1 ). Indeed, much of engineering is「normal engineering」( chapter 6 ), just as much of science is what Kuhn calls「normal science.」Yet most of engineering is quite far from the drudgery that this view implies because it involves creating things that have never before existed. In fact, engineers tend to use their own technology to automate the drudgery, for example, using compilers to translate programs into machine code ( chapter 5 ). I hope I have convinced the reader that engineering is indeed an intellectual and a creative discipline.

Creativity is enabled by the richness of possibilities offered by so many layers of modeling and so many modeling paradigms, but this same richness can overwhelm. It is difficult for humans to comprehend the alternatives, so instead they latch onto those paradigms nearest at hand. By definition, paradigms frame our thinking. Yet in framing our thinking, they also constrain our thinking, limiting our choices. With digital technology, this「freedom from choice,」as Sangiovanni-Vincentelli calls it, is essential to designing anything that uses billions of transistors that can switch on and off billions of times per second. Any given individual will have assimilated only a few of the relevant paradigms and will resist straying from these. The resulting fragmentation of the engineering community limits communication between engineers and reinforces sects and their parochial thinking.

It may seem that a reasonable counterforce to this fragmentation is the development of international standards. These can lead to a community coalescing around a common language, principle, or approach. Yet there are costs. One is that the making of international standards is a messy, political, and possibly even corrupt process ( chapter 6 ). Such flawed processes do not usually lead to good technical decisions, particularly when the standard concerns relatively immature technologies.

Standards can also suppress competition among ideas. The U.S. Department of Defense, for example, in an effort to promote standards, for many years forced contractors and researchers to use the Ada programming language, the VHDL hardware description language, and the Microsoft Windows operating system. Ironically, this was occurring while the U.S. Department of Commerce was suing Microsoft for monopolistic practices. In the 1990s, I was involved in a DARPA research project that had the goal of improving the way high-performance signal processing hardware and software was designed, but DARPA required the participants in the project to use VHDL, a particular language for specifying hardware design. However, a language frames the thinking of the designers, so this mandate limited the possible alternatives for innovation. It ruled out one of the key avenues toward innovation in digital technologies, namely, the development of new languages.

Despite many efforts to standardize, digital technology remains a rich and dynamic ecosystem of competing alternative paradigms. In no small part, this is because a given target system or device may have many useful models. For example, a microprocessor chip may be modeled as a three-dimensional geometry of doped silicon, as a computer program specifying software for the chip to run, or anything in between (semiconductor physics, logic gates, instruction set architecture, etc.). These models are all abstractions of the same chip and its function, and they serve different purposes. Which model to use depends on the goal.

Every model is constructed within some modeling paradigm that is typically codified by languages and tools. The languages provide a syntax by which the model is specified (how it is written down or otherwise rendered in physical form) and the semantics (what a given rendition means). The choice of modeling framework has profound consequences. For example, a language for describing three-dimensional shapes is not well suited for modeling the dynamics of a circuit (how the voltages and currents change over time).

Models have many uses, and their intended use should frame the choice of modeling paradigm. They can be used for humans to share ideas asynchronously, like documents. In this case, they need to be simple and use a notation that has been agreed on. Models can be used for specification of a design, in which case simplicity may not be as important as completeness. A computer program that omits a few lines in the name of simplicity will likely not be a useful program. Models can be used for analysis of designs, in which case the formal and mathematical properties of the modeling language can be a dominant concern. Informal languages admit too many possible interpretations to be useful for analysis, even if they are useful for human-to-human communication.

However, humans don't typically choose paradigms. Paradigms are assimilated slowly, often subconsciously, or are drummed in by educators who are likely too specialized to know the alternatives. As a consequence, engineers typically build models using the paradigms they know regardless of whether these are the right choices. This may explain why so many projects fail ( chapter 6 ).

A key challenge is that complex systems, such as the Airbus A350 ( chapter 6 ), have many conflicting modeling requirements. Models need to be combined in ways that their modeling paradigms do not admit easily. A model such as the iron wing prototype of the Airbus A350 ( figure 6.4 ) is able to combine many different aspects of the system in a single model. However, such a model is extremely expensive to construct. If we had better modeling languages and paradigms, then no such physical model would be necessary. A「virtual prototype,」which is a reasonably complete model constructed entirely in software, would (likely) be much less expensive. Virtual prototypes are used routinely today for billion-transistor silicon chips, where they work extremely well. Yet for complex cyberphysical systems such as the A350, it is difficult to build enough confidence using virtual prototypes alone.

I remind the reader that models are used differently by engineers and scientists ( chapter 2 ). For an engineer, the things being modeled are expected to imitate the model, whereas for scientists, it is the other way around. Engineers also use models in the scientific way, and scientists use models in the engineering way, but because these uses differ, it is important to understand how a model is being used. A logic gate is almost certainly going to be a poor model of a piece of silicon found in nature, for example, sand on a beach. Yet it is an exceptionally good model for a piece of silicon coming out of an Intel fab.

12.2 障碍

我们要克服的最为严重的障碍是，尽管人类大脑有着惊人的能力，但它实际上是相当有限的。事实在于，我们无法像计算机一样记住那么多的东西，不能读得像计算机那样快。我们也不能像计算机那样快速地进行计算，而且我们会犯更多的错误。尽管如此，当人类与计算机和网络协作的时候，我们还是可以做一些令人惊讶的事情，例如把人类曾经出版过的几乎所有文献全部装入我们的口袋。

数字技术为人类提供了一种极其丰富的创造媒介，它丰富到我们用今天的技术所能做的事情还远未饱和，就更不用说未来的新技术了。创造力是无穷的，然而，由于我们的大脑倾向于被未知的已知支配（详见第 2 章），所以我们的创造力再次放缓。我们会抵制新范式，即使技术已经使这些新范式成为可能（见第 6 章）。

在数字技术中，除了最低层（半导体物理学）之外，其他的每一层抽象都是人类的发明。当我们穿过了先硬件而后软件的几个抽象层时，我们已经抛开了物理学的影响，以至物理学变得几乎无关紧要了（见第 3 章）。我们进入了模型的世界，一个由人类构建的抽象的世界。软件变得更像数学，而不是自然科学，它们只服从于自己的规则。当然，我们需要有用的规则，但我们无须坚持认为它们不是自我参照的。事实上，它们必须是自我参照的，这样才能具有更好的表现力，就像哥德尔指出的那样。

迄今为止，人类发明的所有建模范式都有其局限性。软件只能执行「有效的计算」，用图灵的话说，这是物理世界可能的过程的一个极小子集（见第 8 章）。数字技术只存在于康托尔指定的无限集合中的最小集合内（详见第 9 章）。我们可以超越软件，构造可以形成信息物理伙伴关系的机器，以充分利用两者各自的优势（见第 6 章）。计算机与其他物理机器的伙伴关系，使得我们能够克服人类的其他局限性，例如，我们有限的交流能力。我们只能用 10 根手指缓慢地写字，只能用 10 千赫的音频带宽讲话，等等。显然，机器通常没有这样的限制。请想一想，当你观看诸如《阿凡达》这样用计算机制作的电影时，请看看艺术家、计算机、数字显示器和人类视觉系统之间的伙伴关系吧。你会发现这些伙伴关系实现了人与人之间前所未有的交流方式。

我们自己永远无法克服这样一个致命的局限性：只有当人类真正能够理解模型的时候，模型才对人类有用。虽然我们的大脑确实是神奇的机器，但是它们在应对哪怕是中等复杂度的模型时，都存在着很大的困难。毫无疑问，本书的一些模型，让那些即使是最有学问的读者也觉得非常难以理解，这是因为我所讨论的专业化的跨度的确太大。其实，我在书中所进行的阐述大都比较基础和浅显。在我所涉及的任一领域里，领域专家们实际使用的模型都比我过度简化以能够让你相信的那些模型复杂得多，在认知上也更具挑战性。

由于我们大脑的局限性，专业化对于让我们能够开展复杂建模是必要的，但同时我们也要付出一定的代价。库恩指出，「专业化工具」（包括专业期刊、专业学会、技术会议、学术部门、专业课程等）获得了自己的声望，并创造了反对新范式的惯性（库恩，1962:19）。因此，专业化对变革产生了阻力。

因为我们的大脑容量只有这么多，所以专业化会导致碎片化，进而，一个专业领域中的见解对于其他专业领域来说会变得难以企及。对于科学家和工程师来说，跨专业工作是相当困难的。武尔夫在撰写有关亚历山大·冯·洪堡的文章时指出，洪堡提出的综合跨学科的方法已经过时了（见第 2 章），这导致洪堡基本上已经被科学群体遗忘了。她认为：「这种日益增长的专业化支撑的是一种越来越关注更多细节的狭隘视野，却忽视了后来成为洪堡标志性理念的全局观。」（武尔夫，2015:22）

在这种狭隘的视野下，专家们对越来越细小的事物了解得越来越深入，直到他们最终对一无所知的事情了如指掌。然后，他们成了教授，而他们所教授的课程成了障碍，难倒了那些「毫无戒备」且只是没有准备好面对复杂专业的本科生。教授们热爱他们的专业，他们想教授这些专业知识，却看不到专业的深奥；他们所开发的晦涩而复杂的分析方法，既不容易学习，也不容易在实际中应用。他们的学科被进一步细分为专业，每个教授都丢掉了大局和大体系。没有人有资格来教授这种大体系，而且，无论如何，他或她的同事都会认为这种大体系不过是「米老鼠」而已，它太简单、太不成熟了，不值得他们花时间去研究。

技术在塑造并渗透我们的文化时，专业化造成的碎片化尤其具有破坏性。这个星球上的每一个人，无论他（她）的智力水平如何，都会受到科技的影响。然而，许多知识分子都低估了理解技术的价值。我看不出今天任何一个真正的人文主义者如果不了解技术，如何能了解社会。在我看来，抛开技术研究当代文化就如同抛开语言去研究文学。然而，这似乎是许多人都在做的事情。

我的母校耶鲁大学就是一个很好的例子，它是艺术和科学的典范。1992 年，也就是在我获得「计算机科学」以及学校的「工程与应用科学」双学位几年以后，学校的教务长弗兰克·特纳突然提议取消耶鲁大学几乎所有的工程专业。对于特纳来说，「应用科学」并非基础性的，远不及科学本身那么重要。在他看来，应用科学是工程学所做的一切。当然，取消工程专业的提议最终并没有被采纳，但是这种提议在当时备受关注，并在一些校友中引起了轩然大波。耶鲁新闻 2010 年发表的一篇纪念文章称，特纳是一位「研究那些塑造了西方文明的思想的历史学家」。今天，如果不研究技术，我不知道你怎么可以研究塑造西方文明的思想。

然而，技术并不容易理解。我们可能都有过这样的经历，当我们无法解决个人电脑或家庭网络中的某个问题，而印度的某个巫师却向我们解释了如何解决这个问题时，我们会觉得对自己很无言。我们觉得我们本应该知道这个巫师所知道的事情，或者本应该能够解决这个问题。然而，巫师所掌握的知识并不是关于这个世界的基本事实。那是关于一种特殊技术的语言和文化。在这样一个多元的世界里，我们不可能理解所有的语言和文化。而每个专业化的领域，都会有自己的教区专家。

学术界中要么发表、要么毁灭的普遍心态进一步加剧了专业化。学术期刊上最受推崇的可发表成果，是那些解决了长期的开放性问题的成果。在一个更为专业的领域，开放性问题是什么就更明确了，但这些问题很难被解决。所以，如果你能解决这些问题，就会受到更多的尊重。只有长期存在的专业才会有长期存在的开放性问题。相比之下，在跨学科以及不成熟领域的工作中，真正的创新往往来自提出一个前人还没有认识到的问题。然而，如果新提出的问题很容易被解决，那么描述问题解决方案的学术论文就可能在同行评审中被拒绝，因为解决方案是「显而易见的」。

即使是技术也会减缓创新的步伐。软件有一个相当显著的特性，即它趋向于编码自己的范式（见第 5 章）。当一种新的软件范式出现时，它不可避免地会带来一套特定的语言和工具，这些语言和工具会迅速积累足够的规模和复杂性，从而变得不可撼动。这些都会使得这个范式具有耐久的生命力，但有时会过于耐久，进而阻碍了创新与发展。

2016 年 5 月 25 日，美国国家会计总署发布报告称，美国政府有超过 70% 的信息技术预算用于「运行维护」，而不是技术的「开发、现代化升级和优化增强」。这一预算高达每年 650 亿美元，其中大部分被用于维护过时的语言和硬件，其中有些甚至已经有 50 年历史了。该报告还援引了美国国防部使用 8 英寸软盘以及美国财政部使用汇编代码等一些案例。因此，我们可以说，硬件、语言和工具实际上已经成了创新的障碍，因为要改变已有的格局是相当困难的。

当然，所有的学科都抵制变革。库恩说，「例如，常态科学常常会抑制那些基础的新鲜事物，因为那些新鲜事物必然会颠覆其基本的信条」（库恩，1962:5）。当这些「基本的信条」被编码成一套数百万行的计算机程序时，这样的惯性会变得更难克服。

抵制变革的不仅有技术人员，还有技术的消费者。当人类习惯了与机器互动的一些方式时，改变就可能变得不那么容易了。例如，在设计汽车的刹车和油门踏板时，这些踏板通过机械和液压装置与刹车和油门直接耦合连接。人们学会使用这些控制装置驾驶汽车。

今天，这些踏板会向计算机发送指令，计算机对该指令进行调整，可能会在把指令传输给刹车和油门之前对其进行更改。例如，计算机可以对每个车轮施加不同的制动量，以提高行车的稳定性并防止打滑。在电动汽车中，每个车轮都有自己的电动机，而不是一个统一的油门，这样计算机就可以单独控制这些电动机。如果人类要通过直接的机械连接结构来控制每个车轮，汽车就必须安装 8 个踏板，4 个用于刹车，4 个用于加速器。看起来，只有一只八爪章鱼才能驾驶这样的一辆汽车。

汽车制造商本可以发明一种全新的方式让人类控制汽车。例如，使用操纵杆而不是方向盘，但是这样的改变可能会受到消费者的抵制。人类是用旧的控制方式来学习驾驶的，而忘记一些东西往往要比学习新的东西更加困难。因此，今天的汽车制造商必须非常努力地设计踏板，以便让消费者觉得踏板是直接连接到机械和液压执行器上的。踏板甚至可以按液压控制的方式反向弹起，但很可能是由计算机而不是由充油的液压缸决定弹起多少。

一种很普遍但有误导性的观点认为，人机接口应该是「直觉性的」。可是，汽车里的踏板没有任何直觉性可言。人与计算机的交互也没有任何直觉性可言。我们今天使用的所有交互机制都是学习到的。这使我想起电视连续剧《星际迷航》中的一集，在这一集中，企业号的船员穿越时空回到了 20 世纪 80 年代末。工程师斯科蒂需要使用一台 20 世纪 80 年代的老式计算机来解决一个问题。于是他开始对计算机说：「计算机，计算机，计算机！」当然，计算机没有反应。20 世纪 80 年代的一位工程师拿起一只鼠标递给斯科蒂，说：「你必须用这个。」斯科蒂显得有些尴尬，他说：「哦，是的，当然了。」于是他拿起鼠标，就像冲着麦克风一样对它说话：「计算机，计算机，计算机！」计算机鼠标是一项杰出的发明，我们已经接受了这个范式，但它同样没有任何的直觉性。

不幸的是，我们教授技术的方式往往忽视了技术所具有的创造特性。我在这里用「我们」指代我本人和我的同事们 —— 大学和技术学院的教授们。我们教授技术，就好像它们是事实和真理的集合，是独立于人类永恒存在的、等待人们去发现的柏拉图式理想。这种教学方式的后果就是，我们强调了发现重于发明、发明重于设计的哲学理念（见第 1 章）。

如果发现者所发现的东西已经存在于柏拉图式的善里，那么发现者作为个体就不应该是重要的。发现者的性格和偏好不可能对他们所发现的事实和真理的属性产生任何影响。库恩观察到，这种将观点与其提出者进行分离的倾向「在科学职业的意识形态中是根深蒂固的」，他引用阿尔弗雷德·诺尔司·怀特海的话说，「一门不愿意忘记其创始人的科学已经迷失了」（库恩，1962:138）。如果全部有价值的事实和真理都已经在那里并等待被发现，那么个体能做的最有价值的贡献就是把一些之前长期处于黑暗之中的事实或真理带入光明。

我个人完全不同意怀特海的观点。我认为几乎所有关于技术的「事实和真理」实际上都是人类的发明。就像今天的情况一样，技术有时反映了一种奇特想法的达尔文式无序进化。理解这些思想的起源对于批判性地思考它们是至关重要的，而批判性地思考这些思想又是技术革命的关键。

事实上，我们重发明而轻设计的做法也会成为抑制创造力的一个障碍。强调新颖性而轻视质量，即「新的胜过好的」，是学术上的一个鼠洞。不会有一个令人尊重的学术期刊会发表一篇描述苹果手机的文章，因为这项技术的每个元素都已经存在于其他产品之中了。然而，苹果手机确实是对人类的重大贡献，而学术期刊上发表的绝大多数文章却不是。

有能力做出这种贡献的富有创造力的人可能会被技术排斥，他们会把工程学科视为一个行业，其要求对熟知的技术进行专业培训，运用科学中已知的方法，并不断调整和优化现有的设计（见第 1 章）。事实上，正如很多科学都是库恩所说的「常态科学」那样，很多工程也都是「常态工程」（见第 6 章）。然而，大多数工程远不是这一观点所暗示的苦差，因为它包括了创造以前从未存在过的事物。事实上，工程师常常倾向于使用他们自己的技术让机器自动完成这些「苦差」，例如，使用编译器将程序转换成机器码（见第 5 章）。我希望我已经使读者们相信，工程学确实是一门充满智慧和创造性的学科。

如此之多的建模层次以及如此之多的建模范式，它们所提供的丰富可能性激发了创造力，但同样也可能让人类感到不知所措。人类很难理解这些替代方案，所以，他们仅仅能抓住那些离他们最近的范式。根据定义，范式构成了我们的思维。然而，它们在构建我们思维的同时，也限制了我们的思维，限制了我们的选择。有了数字技术，这种圣乔瓦尼 — 温琴泰利所称的「选择的自由」，对于设计任何使用数十亿个（每秒开关数十亿次的）晶体管这样的事物来说都是至关重要的。任何一个特定的个体都只吸收了一些相关的范式，并且会抵制对这些范式的偏离。由此导致的工程群体分裂，限制了工程师之间的交流，并强化了派别及其狭隘的思维。

国际标准的开发似乎是对抗这种分裂的一种可行力量。这可能会导致一个社区围绕一种共同的语言、原则或方法联合起来。然而，这是有代价的。其中的一个是，标准的制定可能是一个混乱的、政治的，甚至是导致腐败的过程（见第 6 章）。这种有缺陷的过程通常不会产生好的技术决策，特别是当这些标准涉及相对不够成熟的技术时。

标准还可能会抑制思想之间的竞争。例如，美国国防部为了推行其标准，多年来一直强迫承包商和研究人员使用 Ada 编程语言、VHDL 硬件描述语言以及微软的 Windows 操作系统。具有讽刺意味的是，同一时期，美国商务部正在起诉微软公司的垄断行为。20 世纪 90 年代，我参与了 DARPA 的一个研究项目，该项目的目标是改进高性能信号处理硬件和软件的设计方式，但 DARPA 要求项目的参与者必须使用 VHDL 语言，这是一种用于描述硬件设计的特定语言。然而，语言会塑造设计者的思维，所以这一强制要求实际上已经限制了可能的创新选项。因为这一要求破坏了数字技术创新的一个关键途径，即新语言的开发。

尽管我们为实现标准化付出了诸多努力，但是数字技术仍然是一个丰富而动态的生态系统，充满了各种相互竞争的替代范式。在很大程度上，这是因为一个给定的目标系统或设备可能会拥有许多有用的模型。例如，微处理器芯片可以被建模为掺杂硅的一个三维几何结构，一个描述芯片所运行软件的计算机程序，或者介于两者之间的任何东西（半导体物理学、逻辑门、指令集体系架构等等）。这些模型都是对同一个芯片及其功能的抽象，但是，它们具有不同的用途。具体使用哪种抽象则取决于具体的目标。

每个模型都是在某个用语言和工具编写的建模范式中构造出来的。这些语言提供了一种描述模型的语法（如何将模型以物理形式写下来或以其他方式呈现）和语义（一个给定的描述是什么含义）。同时，对建模框架的选择也具有深远的影响。例如，描述三维形状的语言并不适合建模电路的动力学（电压和电流如何随时间变化）。

模型具有多种用途，它们的预期用途支配着建模范式的选择。它们可以用于人类信息的异步共享，就像文档。在这种情况下，它们应该是简单的，并使用已达成一致的符号。模型也可以用于一个设计的规格说明，在这种情况下，简单性可能不如完备性那么重要。以简单性的名义省略了几行代码的计算机程序可能不是一个有用的程序。模型还可以用于对设计的分析，在这种情况下，建模语言的形式化和数学属性可能是主要的关注点。因为非形式化语言允许有太多可能的解释，所以不适合分析，即使它们对人与人之间的交流很有用。

然而，人类通常不会刻意去选择使用某种范式。范式常常是被人类缓慢地、下意识地接受的，或者是被那些可能太专业以至不知道还有其他选项的教育者灌输的。因此，工程师通常使用他们所知道的范式来构造模型，而不考虑这些范式是不是正确的选择。这也许可以解释为什么这么多的项目都失败了（见第 6 章）。

一个关键的挑战在于，诸如空客 A350（第 6 章）这样的复杂系统，通常会有多种相互冲突的建模需求。这些模型需要以其建模范式所不容易接受的方式进行组合。像空客 A350 的铁鸟原型（图 6.4）这样的模型能够将系统中许多不同的方面组合在一个单一的模型中。然而，构建这样一个模型的成本是极高的。如果我们有更好的建模语言和范式，就可以不需要这种昂贵的物理模型了。「虚拟样机」是一个完全用软件构建的相当完整的模型，它（很可能）要便宜得多。虚拟样机现在通常用在拥有数十亿晶体管的硅芯片上，它们在芯片上运行得非常好。然而，对于诸如 A350 这种复杂的信息物理系统来说，仅靠虚拟样机很难建立足够的可信度。

我曾提醒过读者，工程师和科学家对模型的使用是不同的（见第 2 章）。对于一个工程师来说，他期待被建模的东西能够模仿模型，而这对于科学家来说恰恰相反。工程师会以科学的方式使用模型，当然，科学家会以工程的方式使用模型。但是，由于这些用法是不同的，因此理解如何使用模型就变得非常重要。几乎可以肯定的是，逻辑门是自然界中一个硅块（如沙滩上的沙子）的糟糕模型。然而，对于英特尔晶圆厂生产的一个硅块来说，这是一个非常好的模型。

### 12.3 Autonomy and Intelligence

Today, some of the most exciting and scary technology developments involve autonomy and intelligence. Both of these terms anthropomorphize computers, a seriously questionable practice ( chapter 9 ). Autonomy refers to the ability that a system has to make decisions without human direction. Intelligence refers to the ability that a system has to exhibit human-like reactions that appear to leverage common knowledge about the world. In both cases, these are not binary properties that are either present or not in systems. Instead, if they are present at all, they are only present in degrees.

Consider self-driving cars, which exist already and will likely be widely available in some form soon. For self-driving cars, full autonomy is not even remotely desirable. Full autonomy would mean that the car accepts no direction at all from humans. You would not even be able to tell it where you want to go. It would simply go where it likes. I don't think a fully autonomous car will sell very well.

How about no autonomy? A car with no autonomy would require you to turn a crank to turn it on. Today, you press a button or turn a key, and a computer tells an electric starter motor to turn the crank for you. This is partial autonomy. It accepts a command from you, an expression of your desires (to turn on the car), and it takes over from there, performing the sequence of actions necessary to turn on the car. Today, that does not even necessarily turn on the engine. A modern braking system is similar, where a computer intervenes to coordinate the braking on the four wheels in a way that no human could do, even if we had four brake pedals.

A few days ago, I saw a flatbed truck go by carrying a nice relatively new car whose front end was completely smashed. This car was not a self-driving model, so almost certainly a human was at fault. My reaction surprised even me. I thought to myself,「That car should be ashamed of itself.」Clearly, I was anthropomorphizing the car, but the sentiment was valid. If my thinking had been more rational, I would have said to myself,「The designers of that car should be ashamed of themselves.」Today, there really is no excuse for putting cars on the road that will happily crash into the back end of the car in front of them. They should not do this, no matter what their human is telling them to do. We have the technology to solve that problem at a reasonable cost, particularly if we consider the cost of not doing it (e.g., insurance, health, and lives).

A car that refuses to crash is a good example of partial autonomy. The fact is, humans are not very good drivers. They get distracted easily, they get sleepy, they get drunk, and they get old. We have the technology to make much better drivers if we simply give the cars more autonomy.

Yet such a change is not without difficulties. There are ethical questions, for example. How should we program a computer to react when an accident is inevitable? Suppose that the choice is between killing a pedestrian and protecting the passenger or hitting a truck and killing the passenger. It will not do to say that we should program the computer to react as a human would because we don't know how to do that. Whatever software we write for self-driving cars, that software will have hidden in it the outcome of that quandary. Even the software engineers will likely not know what that outcome is.

Consider the goal that Travis Kalanick, CEO of Uber, announced in 2015 to eventually replace their contractor drivers with self-driving cars. There are of course the perennial questions about the impact that such automation has on employment. These questions are difficult, because history has shown that increased automation does not necessarily result in fewer people employed. 2 Consider another possible outcome of such automation. Today, the most effective way to deliver an improvised explosive device (IED) for a terrorist attack is in a car with a suicide bomber. Driverless Uber will eliminate the need for a suicide.

Let's consider an even more difficult question. It is well known that the United States uses unmanned drones as weapons systems, using them, for example, to kill known adversaries. These systems are partially autonomous. At a minimum, they can autonomously navigate to a waypoint circumventing terrain and obstacles. Do they make the decision to launch a lethal weapon autonomously? As far as we know (much of this is hidden behind the veil of classified information), today these decisions are still being made by humans. The humans assess the information obtained from the sensors and actively make the kill decision. Yet we have the technology to give these systems more autonomy.

My colleague at Berkeley Stuart Russell, a noted research leader in artificial intelligence and robotics, has been leading a campaign for an international treaty that would ban such lethal autonomous weapons systems, called LAWS. 3 It is an extremely difficult question how governments and society should react to these technical possibilities, but Russell makes a strong case for such a treaty.

Let's turn our attention to intelligence. First, let me point out that anthropomorphizing computers is not only unjustified by the technology ( chapter 9 ) but is also unreasonable. It is simply not true that we want our machines to exhibit human-like behavior. I really do not want to have to argue with my car about getting to school on time. It's hard enough to have that argument with my daughter.

Consider a Google search of the web. Does Google attempt to give human-like answers? Not really, thankfully. Instead, Google finds answers written by humans that are likely to be helpful. Try asking Google,「What is the meaning of life?」When I did this just now (May 29, 2016), the first hit on the list of possibly helpful pages is a link to a wonderful Wikipedia page on the subject. That page even includes a discussion of the answer「42」to this question (see footnote on page 84 ). Google is brokering for me the collective intelligence of humans. In my opinion, this does not in any way replace human intelligence. Quite the contrary, it augments human intelligence. I'm quite sure it makes me smarter because I have a really poor memory, and it improves the ability of humans to communicate with one another by democratizing publication. Everyone has a voice.

If we accept digital physics and the universality of software, which I don't ( chapter 8 ), then in principle we should be able to make computers that will make decisions at least as well as humans, for example, the kill decisions of LAWS. Digital physics implies that computers can be endowed with the same sense of identity, self-awareness, accountability, and feelings as a human because all of these things must be digitally replicable. But why would we want to delegate such decisions to computers that emulate humans? We have seven billion human brains on the planet as it is. Isn't that enough? We should instead be focusing on the ways in which technology complements human capabilities. Humans can keep seven numbers in short-term memory. The smartphone in your pocket can keep billions. Some decisions can be made better by computers, not by replicating human processes, but by exploiting their ability to evaluate millions or even billions of alternatives.

If we actually succeed in making computers behave like humans, I'm quite certain we will come to regret it. Humans, after all, don't really behave very well. What kinds of new wars will we find ourselves in? What if the computers decide to take humans out of the loop, as they do in The Matrix , the science fiction film trilogy?

Autonomy and intelligence are about getting computers to do more for us. If we can orchestrate things so that what the computers do for us, on net, provides real benefits, then we come out ahead. However, it is unreasonable to expect there to be no costs. For this reason, technology development should not be left exclusively to the nerds, like me. I believe it is imperative for nonnerds to understand technology better so they can help guide its evolution in society, and it is imperative for the nerds to understand the cultural context of their work. These are the main reasons I wrote this book.



12.3 自主与智能

今天，一些非常令人兴奋又让人觉得有些可怕的技术发展都会涉及自主性和智能。这两个术语都将计算机拟人化了，这是一种非常值得质疑的做法（见第 8 章）。自主性是指一个系统在没有人类指导的情况下做出决策的能力。智能是指一个系统似乎利用了关于世界的常识，进而表现出类似人类反应的能力。在这两种情况下，它们都不是系统中要么存在要么不存在的二元对立的属性。相反，如果它们存在，它们就只是在某种程度上存在。

以自动驾驶汽车为例。这种汽车已经出现了，并且可能很快就会以某种形式被广泛使用。对于自动驾驶汽车来说，完全自主是遥不可及的。完全自主意味着汽车完全不受人类的干预，你甚至无法告诉它你想去哪里，因为它只会去它想去的地方。我不认为完全自主的汽车会卖得很好。

那么，没有自主性又会怎么样呢？没有一点儿自主性的汽车需要你转动曲柄才能启动。今天，你只要按下按钮或转动一下钥匙，计算机就会通知启动电机为你转动曲柄并启动汽车。这属于部分自主。计算机接受你的指令，即你所期望操作的一种表示（启动汽车），然后从此处进行接管，并执行一系列动作来启动汽车。今天，这甚至不需要启动引擎。现代的刹车系统与此类似，即使我们装上四个刹车踏板，计算机也会以一种人类无法做到的方式来干预并协调四个轮子的制动。

几天前，我看到一辆平板卡车运载着一辆相当不错的新车，新车的前端已被彻底撞烂了。显然，这辆车并不是自动驾驶类型的，所以几乎可以肯定这是人类的错误。我的反应让我感到惊讶。我心想：「那辆车应该为自己感到羞耻吧。」显然，我已经把车拟人化了，但这种感觉是正确的。如果我的想法能够再理性一些的话，我会对自己说：「那辆车的设计者们应该为他们自己感到羞耻。」今天，真的没有理由再让那些会「兴高采烈地」追尾前车的汽车上路了。它们不应该这样做，无论它们的主人告诉它们做什么。我们拥有以合理成本解决这个问题的技术，特别是当考虑到不这样做可能产生的巨大代价时（例如保险、健康和生命）。

拒绝撞车的汽车就是部分自主的一个很好的示例。事实上，人类并不是很好的驾驶员。他们很容易分心，昏昏欲睡，喝醉以及变老。只要我们给汽车赋予更多的自主性，我们就有技术来培养更好的驾驶员。

然而，这种变化并非没有困难。例如，存在着一些道德伦理问题。当事故不可避免时，我们应该如何编写程序使计算机做出合理的反应？假设有两种选择，一种是牺牲一个行人且保护这个乘客，另一种是撞上一辆卡车并牺牲这个乘客。不能因为我们不知道如何决定，就说我们应该让计算机像人类一样做出反应。无论我们为自动驾驶汽车编写了什么样的软件，该软件都会隐藏在这个困境的结果里。而且，即使是软件工程师，也可能不知道结果到底是什么。

再想想优步首席执行官特拉维斯·卡兰尼克在 2015 年宣布的发展目标，即最终要以自动驾驶汽车取代与其签约驾驶员。当然，有关这种自动化会对就业产生的影响，人们也一直存在着疑问。这些问题都很棘手，因为历史已经证明，自动化程度的提高并不一定会导致就业人数减少。让我们再来考虑一下自动化程度提高的另一个可能结果。如今，为恐怖袭击运送简易爆炸装置（IED）的最有效方式是在汽车里装上一个自杀式人体炸弹。是不是说，实现无人驾驶的优步将会消除对这种自杀方式的需要。

让我们来思考一个更困难的问题。众所周知，美国使用无人驾驶飞机作为武器系统，例如，用来杀死那些已知的敌人。这些系统也是半自主的。至少，它们可以绕开地形和障碍物并自主导航到一个地点。那么它们会自主决定发射致命武器吗？据我们所知（其中很大一部分信息是高度机密的），迄今为止，这些决定仍然是由人类做出的。人类评估从传感器中获得的信息，并主动做出攻击的决策。然而，我们拥有赋予这些系统更多自主性的技术。

我在伯克利的同事斯图尔特·拉塞尔，是人工智能和机器人研究领域的领军人物。他一直在领导一项运动，旨在制定一项禁止此类致命自主武器系统的国际条约，该条约被称为 LAWS。政府和社会应该如何应对这些技术的可能性是一个极其困难的问题，但拉塞尔为这样的一个条约提供了强有力的理由。

现在让我们把注意力转向智能。首先，我认为把计算机拟人化不仅在技术上是不合理的（见第 9 章），而且也是不切实际的。我们其实并不想让我们的机器表现出类似人类的行为。我真的不想就按时上学和我的车进行争论，和我女儿争论这个问题已经够难了。

我们还可以想想谷歌搜索的例子。谷歌在试图给出类似人类的答案吗？谢天谢地，它不会的。相反，谷歌会寻找那些由人类所写的有用答案。我们来试着问谷歌一个问题：「生命的意义是什么？」当我刚刚这么做的时候（是在 2016 年 5 月 29 日），谷歌给出了一组关于这个主题结果。其中，在有可能有用的页面列表上，第一个是一个关于这个主题的很棒的维基百科页面链接。

这个页面甚至还给出了对这个问题的答案「42」的讨论。谷歌是在为我代理人类的集体智慧。在我看来，这并不能取代人类的智能。恰恰相反，它增强了人类的智能。我可以十分肯定地说，这会让我变得更聪明，因为我的记忆力真的很差，而且它通过一种大众发行的方式提高了人类相互交流的能力。每个人都有发表自己言论的机会。

如果我们接受数字物理学和软件的普遍性（我并不接受，见第 8 章），那么从原则上说，我们应该能够制造出至少和人类一样能做出决策的计算机，例如，LAWS 的攻击决策。数字物理学意味着，计算机可以被赋予与人类相同的身份感、自我意识、责任感和情感，因为所有这些都必须是数字式可复制的。但是，我们为什么要把这样的决策委托给模仿人类的计算机去做呢？这个星球上已经有 70 亿的人类大脑了，难道还不够吗？相反，我们应该聚焦于研究利用技术扩充人类能力的方式。人类的短期记忆只能记住 7 个数字，然而你口袋里的智能手机却保存了数十亿计的信息。计算机可以做出一些更好的决策，并非通过复制人类的处理机制，而是利用它们评估数百万甚至数十亿选项的能力。

如果我们真的能成功地让计算机表现得像人类一样，我很肯定我们一定会后悔的。毕竟，人类并不是真的表现得很好。我们将发现自己置身于什么样的新战争之中？如果计算机决定把人类带出循环，就像它们在科幻电影三部曲《黑客帝国》中所做的那样，结果会怎么样？

赋予计算机自主和智能，就是想让计算机为我们做更多的事情。如果我们能精心设计，使得计算机在网络上为我们所做的事情能带来真正的益处，我们就会领先。然而，要实现这一切一定要付出代价，期待没有代价是不切实际的。因此，推动技术发展不应该仅仅是像我这样的技术呆子的事情。我认为，不是技术呆子的人们必须更好地理解技术，这样他们才能帮助并引导技术在社会中的发展，而技术呆子们则必须了解他们工作所处的文化背景 —— 这就是我写作本书的主要原因。

__________

1 I speak loosely here when I say「capable of self-reference.」The specific requirement is that the system be able to express Gödel's sentence. Gödel showed that any system rich enough to express arithmetic on the natural numbers is rich enough to express Gödel's sentence, and it is hard to imagine trying to use a theory for physics that is not at least this rich.

2 For a scary and pessimistic view of the question of whether technology will finally result in fewer jobs, see Ford (2015).

3 See http://www.cs.berkeley.edu/~russell/research/LAWS.html
