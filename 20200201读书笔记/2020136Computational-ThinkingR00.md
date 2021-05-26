## 记忆时间

## 卡片

### 0101. 主题卡 —— 计算机思维和人的思维的区别

Computational thinking illuminates a fundamental difference in the ways that humans and machines process information. Machines can process information at billions or trillions of calculations per second, whereas humans do well at one calculation per second. Machines process with no understanding of the data they are processing, whereas humans do and can correct errors on the fly. Machines can transform a mistake in an algorithm into a costly disaster before any human has a chance to react. Thinkers in the philosophy of mind, neuropsychology, cognitive science, and artificial intelligence have studied these differences and shown us how fundamentally dissimilar they are. Although some human tasks like searching and sorting can be eased by applying algorithms to them, most computational thinking in the big picture is concerned with machine computation.

2『上面计算机思维和人的思维，做一张主题卡片。』—— 已完成

### 0102. 主题卡 —— 计算机不能做的事

总结一下（2021-05-22）：

场景一：只有很少一分部问题是能有计算机解决的。现实中只有一分部问题是「可计算」的，「可计算」的问题中也只有一分部问题是消耗比较少的「计算资源」的问题。

场景二：缺少业务知识。计算知识必须结合业务知识才能解决实际问题。

场景三：缺少计算机知识。认为「计算机」本身的基础知识不重要。

场景四：认为计算机是「智能」的。是使用计算机的「人」才是智能的，计算机只是工具。

信息源自「2020136Computational-Thinking0101.md」

In our enthusiasm for computational thinking, we need to be careful to avoid wishful thinking. Perhaps the first and most common wish is that we can get computers to do any job we can conceive of. This wish cannot be realized because there are many jobs that are impossible for computers. For example, there is no algorithm that will inspect another algorithm and tell us whether it terminates or loops forever. Every programming student longs for such an algorithm to help with debugging. It was logically impossible in 1936 when Alan Turing proved it so, and it is still impossible today.

1-2『这里的信息阐述了「计算机」不能做的事，列举了 4 中不能「计算」的场景，等同于吴军之前一直强调的「计算机边界」问题。做一张主题卡片。（2021-05-04）补充：首先，现实中的很多问题是「不可计算」的。其次，很多「可计算」的问题需要耗费很多「资源」，比如 NP 问题，典型如配送距离最短路线。（2021-05-22）』—— 已完成

Even if we stick to logically possible jobs, there are many that cannot be done in a reasonable time — they are intractable. One famous example is the traveling salesman problem, which is to find the shortest tour on a map of a country that visits each city just once. An algorithm to compute this would be of great value in the package delivery industry. The simplest way to find the shortest tour is to enumerate all possible tours and select the shortest. For a small set of 100 cities, this would take 10^130 years on the world's fastest supercomputer. For comparison the age of the universe is on the order of 10^10 years. Even the「simplest way」can be impossible! Algorithms analysts have identified thousands of common problems that are intractable in this way.

1『又看到经典的 NP 问题。（2021-05-04）』

The picture gets even more confusing because in most cases there are fast algorithms to find an approximate answer. They are called heuristics. Take, for example, the problem of finding the shortest tour connecting all 24,978 cities in Sweden. The enumeration algorithm for the traveling salesman problem would take on the order of 10^100,000 years! But in 2004 a team at the University of Waterloo using heuristics for optimization found a shortest tour and proved it to be correct. Their solution used 85 years of processing time spread over a cluster of machines that took several months to complete the job.

Computational thinkers need to develop enough experience and skill to know when jobs are impossible or intractable, and look for good heuristics to solve them.

A second example of wishful thinking is to believe that learning how to program in a computer science course or a coding-intensive workshop will enable you to solve problems in any field that uses computation. No, you will need to learn something about the other field too. For example, even if you have studied search algorithms in a programming course, you are not likely to be able to be useful to a genomics project until you have learned genome biology and the significance of biological data.

A third example of wishful thinking is to believe that computers are not essential to CT — that we can think about how to solve problems with algorithms and not be concerned with the computers that run the algorithms. But this is not so. When a computer does not have sufficient memory to hold all your data, you will seek ways to divide your problem into subsets that will fit. When a single processor does not have sufficient processing power, you will seek a computer with multiple parallel processors and algorithms that divide the computation among them. When the computer is too slow, you will look inside to find a bottlenecked component and either upgrade it or find a new algorithm that does not use that component. Even if your computer has sufficient memory, adequate processing power, and no bottlenecks, other aspects can limit your problem-solving progress, notably the speed of the internal clock, which paces the machine to perform computational steps in an orderly and predictable way. But some new machines, notably quantum computers and neural nets, have no clocks: How shall we think about programming them?

A fourth example of wishful thinking is to believe the computer is smart. If you are imprecise in translating human steps into program steps, your computation will contain errors that could cause disasters. Computers are incredibly dumb. They perform mindless, mechanical steps extremely fast but they have no understanding of what the steps mean. The only errors they can correct are the ones you anticipate and provide with corrective algorithms. You are the source of the intelligence; the computer amplifies your intelligence but has none of its own.

We advise you to approach CT with humility. It is a learned skill. Our brains do not naturally think computationally. Keep your perspective on the capabilities of computers and algorithms to do jobs, on the need to learn something about the application domain you want to design for, on the dependency of computation on computers, and the abject lack of intelligence in the machine.

### 0103. 主题卡 ——  CT 6 大核心元素

信息源自「2020136Computational-Thinking0101.md」

Our objective in this book is to lay out the magnificent fullness of computational thinking and its precepts about computation and to dispel misunderstandings about the strengths and limits of computing.

Computational thinking evolved from ancient origins over 4,500 years ago to its present, highly developed, professional state. The long quest for computing machines throughout the ages was driven not only by the need to speed up computation, but also to eliminate human errors, which were common when easily bored or distracted humans performed many repetitive calculations. A special thinking skill evolved to accomplish this.

The development of computational thinking opened six important dimensions that are characteristic of CT today.

2『 CT 6 大核心元素。做一张主题卡片。（2021-05-04）』—— 已完成

1 Methods. Mathematicians and engineers developed methods for computing and reasoning that non-experts could put to work simply by following directions.

2 Machines. Inventors looked for machines to automate computational procedures for the purpose of greater speed of calculation and reduction of human errors in carrying out computations. This led eventually to the invention of the digital electronic computer that harnesses the movement of electrons in circuits to carry out computations.

3 Computing Education. University educators formed computer science to study and codify computation and its ways of thinking and practicing for institutions, businesses, science, and engineering.

4 Software Engineering. Software developers formed software engineering to overcome rampant problems with errors and unreliability in software, especially large software systems such as major applications and operating systems.

5 Design. Designers bring sensibilities and responsiveness to concerns, interests, practices, and history in user communities.

6 Computational Science. Scientists formed computational science to bring computing into science, not only to support the traditions of theory and experiment, but also to offer revolutionary new ways of interpreting natural processes and conducting scientific investigations.

These six dimensions are like different windows looking at CT. Each window offers a particular angle of looking. Some aspects of CT may be visible through two windows, but each in a different light. In the next six chapters we will examine CT in relation to each dimension above. We round out with a semifinal chapter on CT in modern general education and a concluding chapter about the future of CT.

Chapter 2: CT related to algorithmic procedures to automate processes

Chapter 3: CT related to computing machinery

Chapter 4: CT related to the theory of computing and academic discipline

Chapter 5: CT related to building large software systems

Chapter 6: CT related to designing for humans

Chapter 7: CT related to all the sciences

Chapter 8: Teaching CT for all

Chapter 9: The future of CT

We offer our stories of these dimensions to show you the power of CT and the ways in which it might help you in your work with computers and computation. Computational thinking evolved from ancient origins over 4,500 years ago to its present, highly developed, professional state. The long quest for computing machines was driven not only by the need for speed, but also to eliminate human errors.

### 0104. 主题卡 —— 驾驭复杂软件系统的唯一办法是抽象

信息源自「2020136Computational-Thinking0501.md」

An early focus in software engineering was the design of「abstractions,」which are simplified models of something complicated with a simple interface. Good abstractions hide the details of the machinery implementing them, allowing programmers to debug them without having to dig into the details of underlying machines. For example, a file is presented as a container of a string of bits with two operations, read and write; its complicated implementation as records scattered across a hard disk is completely hidden. Designing hierarchies of abstractions is seen as the only way to master the enormous complexity of software. Finding good abstractions is an essential design skill for programmers and software engineers. Programming languages that allow programmers to express their abstractions are essential. [1]

1-2『这里的信息有一次刷新了对「抽象」的认知。驾驭复杂软件系统的唯一办法是抽象，做一张主题卡片。（2021-05-24）』—— 已完成

In his classic book The Mythical Man-Month (1975), the software pioneer Fred Brooks noted two dimensions for transforming programs into production systems. One was the generalization of a single software program to a system of interacting programs. The other was the addition of structures and components that provided guarantees to make the software reliable. His rule of thumb was that movement in either dimension tripled the effort. Movement in both dimensions was needed to achieve reliable production systems — a total of nine times the effort of creating a single program.

Software developers, having become aware of such a wide gap between basic programming and production systems, had to find new practices of CT to close it. They developed a trove of new forms of CT: new practices for decomposition, complexity, information structures, causality, closing semantic gaps, data abstraction, data structures, encapsulation, information hiding, recursion, project management, and software life cycles. Aspects of theoretical computer science, notably complexity theory and automatic theorem proving, became helpful in this arena.

The movement described by Brooks can be characterized as moving from computational thinking in the small (designing and writing single programs) to computational thinking in the large (designing software systems and managing the software projects that build them from design and into production and maintenance).

1 Niklaus Wirth, software pioneer and the designer of the popular language Pascal, gives an excellent account of the development of programming practices and their supporting languages (Wirth 2008).

As they gained familiarity with the practices of programming, language designers developed higher-level languages, such as FORTRAN and COBOL around 1958. These languages enabled programmers to express algorithmic statements that were automatically translated by compiler into machine code; they relieved programmers of the burden of direct machine code programming. When they saw that programmers often started by designing the data structures and then a small set of subroutines that performed operations on the structures, language designers enunciated the practice of data abstraction. Data abstraction matured into object-oriented programming languages. Data abstraction has become another key feature of CT: it hides internal mechanisms of program components, while allowing the use of those components through well-defined interfaces. With data abstraction, programmers can focus more easily on what the components do rather than how they do it.

2『补充进「抽象」主题卡片里。（2021-05-25）』—— 已完成

Today's CT inherits many precepts for programming methodology including modularity, abstraction, information hiding, hierarchical composition, recursion, design patterns, managing digital objects, visualization, verification, and debugging. These conceptual tools require great skill and experience at design. Design has emerged as one of the major areas of development in computing; we will discuss it in depth in chapter 6. CT precepts on languages, methodology, and operating systems all aid productivity and confine or eliminate errors.

### 0105. 主题卡 —— 工程和科学的三大区别

信息源自「2020136Computational-Thinking0501.md」

We have found three distinctions between engineering and science particularly helpful to understand the contributions each can make to software production. The first concerns the nature of their work. Engineers design and build technologies that serve useful purposes, whereas scientists search for laws explaining and predicting phenomena. Design is among the most commonly used words of engineering, whereas it is uncommon in science. Design in engineering is a process of finding practical, safe, cost-effective implementations. Scientists concentrate on finding and validating recurrences, engineers on listening to clients and proposing technologies of value to them.

2『工程和科学的三大区别，做一张主题卡片。（2021-05-24）』—— 已完成

The second main distinction is how scientists and engineers regard knowledge. Scientists treat knowledge as data and information that have been organized into a「body of knowledge,」which is then available for anyone to use. The scientific method for creating knowledge is a process of standard, disinterested observers gathering and weighing evidence in support of claims that might be added to the body. Engineers treat knowledge as skillful practices that enable design and building of tools and technologies. Engineers are not outside observers; they are immersed in the communities of use. They embody practices for building, maintaining, and repairing technologies; attending to reliability, dependability, and safety in the context of use; and following engineering standards and codes of ethics.

The third main distinction concerns the role of abstractions and models. Science emphasizes models, and engineering emphasizes machines and artifacts. There is a fundamental distinction between modeling machines and building them. Abstractions are useful for what they leave out. Machines are useful for what they leave in. Hardware and software are interchangeable to the theorist, but not to the engineer.

The familiar phrase「the devil is in the details」is an engineer's motto. Engineers must get the details right for systems to work. Scientists want to eliminate the details so that the recurrences stand out.

These differences explain why it has been hard to design software engineering education that actually produces capable software developers. Many software engineering groups are in computer science departments that emphasize the science over engineering. The same balancing problem haunts computational thinking, too: when one or the other worldview dominates, the synergies are lost.

### 0106. 主题卡 —— Design Principles, Patterns, and Hints

信息源自「2020136Computational-Thinking0501.md」

The goals of programming in the large were summarized as the five DRUSS objectives – dependable, reliable, usable, safe, and secure. To achieve these goals software developers work with three kinds of computational thinking practices: design principles, patterns, and hints.

1-2『补充进 DRUSS 术语卡片，并且新增一张「Design Principles, Patterns, and Hints」主题卡片。（2021-05-25）』—— 已完成

Design principles are descriptions of skills and strategies that developers follow when making design decisions. The principles guide them toward designs that meet the five DRUSS objectives.

Design patterns are descriptions of common situations a programmer is likely to encounter. They offer guidance on how to structure the program, or on the process of writing it, for best results.

Design hints are rules of thumb or morsels of advice, most useful to those with advanced skills at systems development.


The goals of programming in the large were summarized as the five DRUSS objectives – dependable, reliable, usable, safe, and secure. To achieve these goals software developers work with three kinds of computational thinking practices: design principles, patterns, and hints.

1-2『补充进 DRUSS 术语卡片，并且新增一张「Design Principles, Patterns, and Hints」主题卡片。（2021-05-25）』—— 已完成

Design principles are descriptions of skills and strategies that developers follow when making design decisions. The principles guide them toward designs that meet the five DRUSS objectives.

Design patterns are descriptions of common situations a programmer is likely to encounter. They offer guidance on how to structure the program, or on the process of writing it, for best results.

Design hints are rules of thumb or morsels of advice, most useful to those with advanced skills at systems development.

Principles

The classic paper by Jerome Saltzer and Michael Schroeder about information protection is an excellent example of design principles (see table 5.1). [6] Design principles are ways of thinking about the total system of software components, in order to achieve the DRUSS objectives and reduce compromise of sensitive information. The principles are embodied in the skills and ways of thinking that system developers acquire over time from building complex computing systems. They apply to any large system that accommodates many users and service processes.

2『已下载论文「2021041The protection of information in computer systems」并存入 Zotero，这篇 Paper 有 66 页。（2021-05-25）』—— 已完成

Table 5.1 Information Protection Principles of Saltzer and Schroeder

| Principle | Directive |
| --- | --- |
| Economy of mechanism | Keep the design simple and small. |
| Fail-safe defaults | Deny access by default; grant access only by explicit permission. |
| Complete mediation | Check every access to every object. |
| Open design | Do not depend on attackers being ignorant of the design. |
| Separation of privilege | Grant access based on more than one piece of information. |
| Least privilege | Force every process to operate with the minimum privileges needed for its task. |
| Least common mechanism | Make shared state information inaccessible to individual processes, lest one corrupt it. |
| Psychological acceptability | Protection should be easy to use, at least as easy as not using it. |

Patterns

In the early 1990s a group of programmers founded the「software pattern community」movement, inspired by the design-pattern idea of building architect Christopher Alexander. [7] Their idea was that if they could describe a common pattern of software use that has been solved by skilled programmers, they could distill the pattern's essence so that other programmers can imitate it. A software pattern characterizes a large number of situations a programmer is likely to encounter and offers guidance on how to structure the program to best fit the pattern. [8] The number of recognized patterns runs in dozens. Examples are the singleton pattern, which limits the number of instances of an object to one, and the iterator pattern, which implements sequential access to data elements. The pattern community appeals to a sense of empiricism because its members are relentless about testing ideas with potential users and learning from the feedback.

1-2『有一次看到了「设计模式」起源的信息，起源于建筑行业，墙里开花墙外香。已下载书籍「」。而且又见到了四人帮的设计模式经典书籍，已下载书籍「2019087Design-Patterns」。（2021-05-25）』

Hints

Butler Lampson, a superb and accomplished designer, summarized a number of guidelines for advanced designers of operating systems. [9] He said:「Designing a computer system is very different from designing an algorithm. The external interface is less precisely defined, more complex, and more subject to change. The system has much more internal structure and hence many internal interfaces. And the measure of success is unclear.」He said the less skilled designers often flounder in seas of possibilities, not knowing how a current choice will affect future choices of the performance of the system. He called his statements「design hints」because they are judgments skilled designers learn to make over time; they emphasize the considerable art in designing. 

2『已下载论文「2021042Hints for computer system design」并存入 Zotero。（2021-05-25）』

In table 5.2 we list Lampson's hints for three dimensions of system development (rows) and major aspects of the DRUSS objectives (columns). Though they may appear as generalities, they are quite meaningful in shaping the CT skills of advanced designers.

Table 5.2 Lampson's Design Hints

| - | Correctness & Fit | Speed | Fault Tolerance |
| --- | ---- | ---- | --- |
| Use cases | Separate normal and worst cases | Safety first, Shed load, End-to-end | End-to-end |
| Interface | Keep it simple, Do one thing well, Don't generalize, Get it right, Don't hide power, Use procedure arguments, Leave it to the client, Keep interface stable, Keep a place to stand | Make it fast, Split resources, Static analysis, Dynamic translation | End-to-end, Log updates, Make actions atomic |
| Implementation | Plan to throw one away, Keep secrets, Reuse a good idea, Divide and conquer | Cache answers, Use hints, Use brute force, Compute in background, Batch processing | Make actions atomic, Use hints |

### 0107. 主题卡 —— No Silver Bullet

信息源自「2020136Computational-Thinking0501.md」

In 1987, Frederick Brooks wrote「No Silver Bullet,」a famous assessment of progress in software engineering since 1968. His conclusions held important lessons for CT. He said that two main complexity factors affect our ability to produce reliable software. The limitations of the technology are the first factor, but they can be overcome by improved technologies, such as high-level programming languages, interactive program development environments, visualization of control and data flow, faster hardware, and better operating systems.

The second factor is our own mental ability to comprehend the essence of complex problems. Coping with complexity is intrinsic to software design and construction and will never go away. The design problem, Brooks said, is mostly conceptual — getting an intellectual grasp on the functions of the system to provide and organize a simple and elegant design.

2『布鲁克斯在人月神话里提出的「No Silver Bullet」做一张主题卡片。（2021-05-25）』—— 人月神话

To address it, we need to grow large systems in relatively easy increments, reuse existing software as much as possible, and make more use of rapid prototyping to gain early feedback before technical decisions are locked. Most of all, Brooks said, we need to「cultivate great designers.」He saw coping with complexity as an essential skill requiring great mastery. Brooks famously wrote that there is「no silver bullet」that will kill the werewolf of complexity in software development.

### 0201. 术语卡 —— Computational thinking 

信息源自「2020136Computational-Thinking0101.md」

Computational thinking is the mental skills and practices for:

1 designing computations that get computers to do jobs for us, and

2 explaining and interpreting the world as a complex of information processes.

1-2『这里作者对 CT 下了定义，做一张术语卡片。（2021-05-04）』—— 已完成

The design aspect reflects the engineering tradition of computing in which people build methods and machines to help other people. The explanation aspect reflects the science tradition of computing in which people seek to understand how computation works and how it shows up in the world. Design features immersion in the community being helped, explanation features being a dispassionate external observer. In principle, it is possible to design computations without explaining them, or explain computations without designing them. In practice, these two aspects go hand in hand.

Computations are complex series of numerical calculations and symbol manipulations. Examples of numerical calculations are the basic arithmetic operations (add, subtract, multiply, divide) and the basic trigonometric functions (sine, cosine, and tangent). Examples of symbolic manipulations are logical comparison of numbers or symbols, decisions of what instructions to do next, or substitutions of one string of letters and numbers for another. Amazing computations can be carried out when trillions of such simple operations are arranged in the proper order — for example, forecasting tomorrow's weather, deciding where to drill for oil, designing the wings of an aircraft with enough lift to fly, finding which physical places are most likely to be visited by a person, calling for a taxi, or figuring out which two people would make a great couple.

There is clearly a special thinking skill required to successfully design programs and machines capable of enormous computations and to understand natural information processes through computation. This skill — computational thinking, or CT — is not a set of concepts for programming. Instead, CT comprises ways of thinking and practicing that are sharpened and honed through practice. CT is a very rich skill set: at the end of this chapter we outline the six dimensions of computational thinking that you will encounter in this book: machines, methods, computing education, software engineering, design, and computational science.

### 0202. 术语卡 —— Engineering

application of science and mathematics to solve problems of use to people.

信息源自「2020136Computational-Thinking0501.md」

A scientific revolution began in the mid-1500s. For much of the time since, there was little practical difference between science and engineering; scientists look for principles of phenomena and engineers built technologies that exploited the phenomena. Many scientists were engineers and many engineers were scientists. The sharp distinction we see today between science and engineering is recent. [2] The distinction was introduced in the late 1940s when Vannevar Bush advocated the establishment of the US National Science Foundation for government support of basic research. Since that time, academic programs have come to define engineering as the「application of science and mathematics to solve problems of use to people」 — in effect defining engineering as a subset of science. This definition hides the unique contributions engineering can make to software. It obscures the need for interaction between the science and engineering sides of computing to make software reliable.

2『这里的 Engineering 的定义，做一张术语卡片。（2021-05-24）』—— 已完成

### 0203. 术语卡 —— DRUSS 目标

信息源自「2020136Computational-Thinking0501.md」

Software developers who had little familiarity with the target domain often caused large gaps between customer needs and the functions of computational systems. Software developers found that the known principles of design were not up to the task of providing dependable, reliable, usable, safe, and secure software — known as the DRUSS objectives. Professional programmers realized that their computational-thinking skills did not scale up well: something was qualitatively different about a program written by a single programmer and a system that required a team of 300 programmers.

2『软件开发的 DRUSS 目标，做一张术语卡片。（2021-05-25）』—— 已完成

The goals of programming in the large were summarized as the five DRUSS objectives – dependable, reliable, usable, safe, and secure. To achieve these goals software developers work with three kinds of computational thinking practices: design principles, patterns, and hints.

1-2『补充进 DRUSS 术语卡片，并且新增一张「Design Principles, Patterns, and Hints」主题卡片。（2021-05-25）』—— 已完成

### 0301. 人名卡 —— Frederick Brooks

Frederick Brooks

### 0401. 金句卡 —— Good judgment comes from experience, and experience comes from bad judgment

信息源自「2020136Computational-Thinking0601.md」

Descriptions of software entities that abstract away their complexity often abstract away their essence. Good judgment comes from experience, and experience comes from bad judgment.

—— Frederick Brooks (1986)

### 0401. 金句卡 —— The sciences do not try to explain, they hardly even try to interpret, they mainly make models

信息源自「2020136Computational-Thinking0701.md」

The sciences do not try to explain, they hardly even try to interpret, they mainly make models.

—— John von Neumann (1955)

### 0501. 数据信息卡 ——

### 0601. 任意卡 —— 大型软件开发的 2 个洞见

信息源自「2020136Computational-Thinking0501.md」

Fred Brooks was the manager of a team of 300 programmers who built the IBM 360 operating system in the 1960s. Their system eventually grew to a massive 10 million lines of code. In his book, The Mythical Man-Month (1975), Brooks documented his experience in detail and gave rules of thumb of CT for organizing and designing large systems. One of his famous observations is that time and people do not trade off equally: a team of 12 programmers cannot complete in a month a job that took a single programmer 12 months. Another is that the structure of the software winds up resembling the organization that built it. Brooks concluded that managing the team was a greater challenge than the technology problems the team had to solve.

2『人月神话那本书里，Brooks 对大型软件开发的 2 个洞见，做一张任意卡片。（2021-05-25）』—— 已完成

### 0602. 任意卡 —— 科学家里的三类角色

信息源自「2020136Computational-Thinking0701.md」

Science and computation have been old friends for centuries. Through most of the history of science and technology, two sorts of scientist roles have been common. One is the experimenter, who gathers data to explore and isolate phenomena, describe recurrences, and reveal when a hypothesis works and when it does not. The other is the theoretician, who designs mathematical models to explain what is already known and uses the models to make predictions about what is not known. The two roles were active in the sciences well before computers came on the scene.

2『科学家里的三类角色，做一张任意卡片。（2021-05-25）』—— 已完成

Both roles used computation. The experimenters produced data that had to be analyzed, classified, and fit to known mathematically formulated laws. The theoreticians used calculus to formulate mathematical models of physical processes. In either case, they could not deal with very large problems because the computations were too extensive and complex.

A third role emerged: scientists who saw new opportunities using computers as simulators that neither the experimenters nor the theoreticians used. The computing pioneers at the Moore School, home of the ENIAC, argued early on that computer simulation could make any computer into a laboratory. They saw the evaluation of models and the production of data for analysis as a new frontier of science. Crossing that frontier required new ways of incorporating modeling and simulation into research, as well as new kinds of computational thinking directly relevant to science.

Large-scale modeling and simulation required significant upgrades to mathematical software. Numerical analysts, a branch of early computer scientists, were heavily involved in the quest to improve mathematical software to efficiently calculate mathematical models on computers. They were especially concerned with representing numbers and performing long calculations in machines that could only offer finite precision; controlling round-off errors and increasing computational speed were major concerns.

## Series Foreword

The MIT Press Essential Knowledge series offers accessible, concise, beautifully produced pocket-size books on topics of current interest. Written by leading thinkers, the books in this series deliver expert overviews of subjects that range from the cultural and the historical to the scientific and the technical.

In today's era of instant information gratification, we have ready access to opinions, rationalizations, and superficial descriptions. Much harder to come by is the foundational knowledge that informs a principled understanding of the world. Essential Knowledge books fill that need. Synthesizing specialized subject matter for nonspecialists and engaging critical topics through fundamentals, each of these compact volumes offers readers a point of access to complex ideas.

2-3『

找了下该系列的书籍：[The MIT Press Essential Knowledge series | The MIT Press](https://mitpress.mit.edu/books/series/mit-press-essential-knowledge-series)，有时间好好刷选一下，作为一个好书单。

随意翻了下，看到一本合胃口的书，已下载书籍「2020137Algorithms」。（2020-12-31）

』—— 未完成

## Preface

A computer revolution is in full swing. The invasion of computing into every part of our lives has brought enormous benefits including email, internet, World Wide Web, Amazon's e-commerce, Kahn Academy, Uber's taxi hailing, Google's maps, trip navigators, smartphones, real-time translators, and apps by the millions. At the same time it has also brought enormous concerns including possible loss of jobs to automation, mass surveillance, collapse of critical infrastructure, cyber war, mass sales of personal data, invasions of advertising, loss of privacy, polarization of politics, loss of civility and respectful listening, and exacerbated income inequality.

A lot of people are having trouble coming to grips with all this. Can they reap the benefits without the downside costs? Can they lead a meaningful life if computerization suddenly threatens to obsolete a lifetime of learning? What should their children learn about computing to enable them to move and prosper in the new world?

Computational thinking is a new term that has recently entered public discourse as people struggle with these questions. It holds the hope that we can think clearly about the powers and dangers of mass computing, and that we can learn to design computers, software, and networks to maximize the benefits and minimize the risks. Parents are already amazed at how facile their children seem to be in the digital world. Is computational thinking the recipe for giving our children a proper education in this world?

We designed this book to be an edifying conversation to help you understand what computational thinking is so that you will be in a better position to answer these questions for yourself.

The first thing to understand is that a substantial part of daily discourse is shaped by the wide adoption of computers. This is nothing new; our ancestors' ways of thinking about the world were shaped by the technologies of previous revolutions. In the industrial age, for example, people regularly used expressions like:

He blew a gasket, I'm humming on all pistons, It's a high pressure environment, and I had to blow off steam.

Today we hear expressions like:

My DNA programs me to do it this way, Our laws are algorithms for running our society, My brain is hardware and my mind software, and My brain crashed, I need to reboot.

Just as in the industrial age, the new idioms of the computer age reveal more about our popular culture than they do about the technology.

Like the Greek god Janus, computational thinking has two faces, one that looks behind and explains all that has happened, and one that looks ahead to what can be designed. We invoke both faces when we want to get computers to do jobs for us. On the back-facing side, we need to understand the mechanics of how computers work, how they are controlled by algorithms, how we can express algorithms in a programming language, and how we can combine many software modules into working systems. On the forward-facing side, we need sensibilities to understand the context in which users of our software are working. We want our software to be valuable to them and not to cause harm to them or their environment. Thus, computational thinking guides us to understand the technology available to us and to design software to do a job or solve a problem.

Computational thinking is not only something programmers must know, but it is also a thinking tool for understanding our technology-infused social world. It increases our awareness of how our everyday digital tools work, grounds our cyber ethics, and improves our resilience against various threats such as algorithm-driven attempts to guide our behavior, personally tailored fake news, viral powers of social media, and massive, data-intensive analysis of our movements. What is more, computational thinking has irrevocably changed the tools, methods, and epistemology of science. Learning CT has many benefits beyond programming.

If you try to understand what computational thinking is from media accounts, you will hear a story of problem solving with algorithms, along with the ability to think at the many levels of abstraction needed to solve problems. The story is flavored with images of joyous children having fun programming and playing games in which they simulate algorithms. Indeed, our teachers have learned much about computational thinking from teaching computing to children, and they have developed superb ways of teaching fundamental computing insights to newcomers. In this book, we call this「CT for beginners.」

But the K–12 education insights and debates barely scratch the surface of computational thinking. At the more advanced levels, computational thinking concerns the design of hardware, networks, storage systems, operating systems, and the cloud. Its historical predecessors have organized human teams to do large computations, organized production lines in manufacturing, guided lawmakers, and specified the rules of bureaucracies. It has developed styles attuned to major areas where computing plays a critical role, such as artificial intelligence, large data analytics, software engineering, and computational science. We will show you all this by examining the kinds of computational thinking needed to deal with these different dimensions of computing. A much more advanced kind of computational thinking is needed to deal with these areas. We call it「CT for professionals.」

Computational thinking is sometimes portrayed as a universal approach to problem solving. Take a few programming courses, the story in the popular media goes, and you will be able to solve problems in any field. Would that this were true! Your ability to solve a problem for someone depends on your understanding of their context in which the problem exists. For instance, you cannot build simulations of aircraft in flight without understanding fluid dynamics. You cannot program searches through genome databases without understanding the biology of the genome and the methods of collecting the data. Computational thinking is powerful, but not universal.

Computational thinking illuminates a fundamental difference in the ways that humans and machines process information. Machines can process information at billions or trillions of calculations per second, whereas humans do well at one calculation per second. Machines process with no understanding of the data they are processing, whereas humans do and can correct errors on the fly. Machines can transform a mistake in an algorithm into a costly disaster before any human has a chance to react. Thinkers in the philosophy of mind, neuropsychology, cognitive science, and artificial intelligence have studied these differences and shown us how fundamentally dissimilar they are. Although some human tasks like searching and sorting can be eased by applying algorithms to them, most computational thinking in the big picture is concerned with machine computation.

2『上面计算机思维和人的思维，做一张主题卡片。』—— 已完成

Think for a moment about the speed issue. A typical computer can, in 1 second, perform a billion calculations and draw a complex image on the screen. A human would need 100 years to carry out the same steps at human speed. Humans obviously draw pictures much faster than that, but machine designers have yet to imitate that human capacity. If humans had no help from computers, we would have no real time graphics. Nearly everything we see software doing is made possible by the incredible speeds of computers. These machines, not humans executing algorithms on their own, are the reason for the computer revolution. Computing machines do the humanly impossible.

While this may send a thrill up your neck, it ought also to send a shiver down your spine. Modern aircraft are controlled by networks of computers performing billions of calculations per second. A mistake in an algorithm can cause the control system to send the aircraft into a death spiral long before the human pilot can react. Early Apollo missions and more recent Mars missions were aborted and lost due to errors in their software. Mistakes in algorithms can be deadly and costly. How can we know that the algorithms running critical systems can be trusted to work properly, bringing benefits and low risk of harm? We need clear thinking to help us find our way through this maze of complexity. This requires an advanced form of CT that is not learned from children's simulation games.「CT for professionals」is deadly serious.

Our account of CT in this book encompasses all the flavors of CT from beginners to professionals, and in major subfields such as software engineering and computational science. We aim to describe CT in all its richness, breadth, and depth. We want to celebrate the work of expert professionals who take on the hard challenges of getting complex systems to perform reliably and safely, and the kinds of thinking they bring that enables them to have achieved such a good track record. We also want to celebrate the work of expert educators who are working to ease the first steps into computational thinking in K–12 schools and lay the foundation to provide everyone the means for coping in the digital world. Those two, basic CT for beginners and advanced CT for professionals, work together to produce a rich tapestry of computational thought.

Peter J. Denning | Salinas, California, August 2018

Matti Tedre | Joensuu, Finland, August 2018

## Epilogue: Lessons Learned

In the research for this book, we learned a few lessons that are worth summarizing here.

### Lesson 1: CT is an addition, not a replacement

Everyone thinks their own field's ways of thinking (and practicing) are valuable and worthy of learning in many other fields. Enthusiasts want to spread the gospel of success to other disciplines. The list of「thinkings」to be spread is long: computational thinking, logical thinking, economic thinking, systems thinking, physics thinking, mathematical thinking, engineering thinking, design thinking, computational thinking, and more.

Our conclusion is that computational thinking is often a welcome addition to other fields, but not a replacement for their ways of thinking and not a meta-skill for all fields.

### Lesson 2: CT is an old, well studied, and diverse topic

The term「computational thinking」(CT) became popular after the US National Science Foundation included it in a funding call in 2007. For many people it was the first time they heard arguments about the value of computing in education. CT seemed to be a new invention, a breakthrough portending a revolution in K–12 education. The truth is, human beings have been doing CT for over 4500 years. It has been advocated for K–12 education since the 1960s.

Some of the first「CT for K–12」curriculum designers attempted to build a「body of knowledge」for CT from scratch without being informed by the long history of computational thinking, including similar attempts to bring computing to schools. They unwittingly created some conceptual errors in their claims about the capabilities and character of CT. We are concerned because inflated expectations and conceptual problems can easily become a part of the CT folklore, and it may take years to dispel them. We urge computing educators to turn to the massive existing body of computing education research to clean this up.

### Lesson 3: The speed of computers is the main enabler of the computing revolution

Most of what software does for us is made possible by the incomprehensible speed gap between computers and humans — billions to trillions times faster. Even though humans can execute computational steps, they could not carry out most of these computations in their lifetimes. The machines can literally do the humanly impossible. While it is true that humans can personally perform algorithms for some information processing tasks, the revolutions of the computer age are not about where people can perform algorithms in their own lives, but about what computers are able to do for them.

### Lesson 4: Advanced CT is domain dependent

For advanced tasks, you need to understand the domain in which you want to figure out how to get a computer to do a job for you. For example, an expert programmer who knows nothing about quantum physics will have little to offer to a team of physicists working on a quantum computer. Similarly, working with the nature's complex algorithms in biology requires considerable understanding of biological processes. Algorithmic models in chemistry require deep familiarity with the corresponding chemical processes. Building an information system for a hospital requires extensive understanding of the institutional, informational, and workflow processes in the hospital context. Much of advanced computational thinking is context-specific and tightly tied to the application domain.

### Lesson 5: CT has changed the tools, methods, and epistemology of science

Computational thinking has fostered a revolution in science. Scientists in all fields have found that CT is a new method of doing science, different from the classic methods of theory and experiment. They came to this discovery in the 1980s when they began using supercomputers to crack scientific「grand challenges.」This was a profound paradigm shift that enabled many new scientific discoveries. Each field developed its own strain of CT that was not imported from computer science. Computer science CT has been enriched by its collaboration with the computational sciences.

### Lesson 6: The public face of CT is that of elementary CT

CT is billed for K–12 curriculum purposes as a set of concepts and rules for programming. But many professionals see CT as a design skill, and many natural scientists see it as an advanced method of scientific interpretation. Like all skills, you can be a beginner, advanced beginner, competent, proficient, expert, or master. Many debates about what CT「really」is seem to collapse different skill levels of CT within the same debate. For example, K–12 teachers argue for curricula that are almost solely aimed at beginners and that contain a small, teachable set of CT insights, practices, and skills. Other advocates argue for CT as advanced, professional skills that require many years of practice and experience. Failing to make the distinction leads to conflicts — for example, the hype about how learning programming opens career paths is silent about what professional computational designers do. Education efforts are important on all levels from K–12 through university and beyond.

### Lesson 7: Beginner and professional CT together comprise a rich tapestry of computational thought

Educators in K–12 schools have developed an impressive「CT for beginners」 — insights and methods for teaching computing to newcomers. Professional software systems designers and scientists have developed an impressive「CT for professionals」 — advanced methods for designing and building complex software that works reliably and safely, and for conducting scientific investigations. The synergy between these two aspects of computational thinking has propelled the computer revolution.

### Lesson 8: Change is an inseparable part of CT

There has never been a consensus about what computational thinking「really」is. There may never be a full consensus. During every decade in the modern history of computing there would be different answers to questions about the essence of computational thinking. Advances in computing keep computational thinking in constant change. We should embrace the lack of a fixed definition as a sign of the vitality of the field rather than our own failure to understand an eternal truth.

## Glossary

Abstraction: Simplifying complex phenomena by representing only their salient features, while omitting or hiding details.

Algorithm: Description of a method to compute a function, or more broadly, to solve a category of computational problems. All the steps are so precisely specified that a machine can perform them.

Artificial intelligence (AI): The subfield of computer science that investigates whether computers powered by appropriate software can be intelligent (strong AI), or whether computers can simulate human cognitive tasks with information processes (weak AI).

Automation: Using machines to replace human controllers of physical processes (such as chemical plants or manufacturing lines), to perform knowledge-work processes (such as reviewing documents or processing invoices), or to build a computer to perform a task, replacing humans who formerly performed the task.

Bit and Byte: A bit is the smallest unit of information that distinguishes between something being present (1) or not present (0). A byte is a set of 8 bits, allowing 128 possible combinations of 8 bits. Large enough combinations of bits can stand for anything that can be represented by discrete values, such as numbers, characters, patterns on a display, or colors.

Boolean algebra: The set of expressions that can be formed from logic variables (each representing a single true-false bit) combined with operators such as OR, AND, and NOT. Boolean expressions are used in programming languages to specify conditions under which a statement will be executed. They are also used to describe the functions of logic circuits inside computers.

Central processing unit (CPU): The hardware component of a computer that fetches and executes elementary instructions such as ADD, SUBTRACT, GO-TO, and COMPARE, and decides on what instructions are executed next. Other hardware components of a computer include the memory (which stores all data and instructions) and the input-output interface (which connects with the outside world).

Cloud: A worldwide network of storage systems and processing systems that can be accessed from anywhere just when and as needed. Users who rent data storage and processing time do not know where their data are physically stored and processed.

Compiler: A software program that translates programs written in a high-level programming language meant for humans into binary machine code meant for the processor.

Computational complexity: A subfield of computer science that investigates the intrinsic difficulty of solving problems. Difficulty is measured by the computational steps and memory space needed. Some problems like searching a list for a name are「easy」because they can be computed in time directly proportional to the length of the list. Some problems like finding the shortest tour of a set of cities are「hard」because in the worst case they require enumerating and measuring all the possible tours, the time for which grows exponentially fast as the number of cities and roads grows.

Computational model: The description of an abstract machine that performs algorithms—for example, a conventional computer chip that executes machine instructions one at a time, a neural network that recognizes faces in images, or a quantum computer that cracks cryptographic codes. In science and engineering, it also refers to a mathematical model of a physical process, which can be simulated or evaluated by a computer.

Computer: An entity, human or machine, that can perform calculations and symbol manipulations according to a set of precisely specified rules. From the 1600s to the 1930s,「computer」meant「a person who computes.」The first electronic computers in the 1940s were called「automatic computers.」The adjective「automatic」was dropped by the 1950s.

Data abstraction: A practice that originated with programmers in the 1960s to encapsulate a complicated data structure behind a simple interface. Users could access the data only through the interface; they could not directly access the memory holding the data. The view of the data seen through the interface is much simplified—hence the word abstraction. An example is a file, which looks to a user as a container of a linear string of bits; the interface allows only reading and writing. The actual file may be implemented as a set of blocks scattered around the storage medium, all hidden from the user.

Decision problem: A famous problem from mathematical logic in the early 1900s. Given a logical system consisting of axioms and rules for constructing proofs of propositions, is there an algorithm that will decide whether a given proposition is true? For a long time mathematicians believed there was such a procedure, but could not find it. In the 1930s a number of mathematicians, working independently from each other, formally defined the concept of algorithm and showed that there is no general solution to the decision problem.

Decomposition: Breaking a complex thing down to simpler, smaller parts that are easier to manage. In software, the parts become modules that are plugged together via interfaces.

Digitization: The work of constructing a binary coded representation of an entity. The representation could be processed by a computer. For example, the wave form of speech can be sampled 20,000 times a second, each sample producing a reading of the wave's amplitude and encoding it as a 16-bit value. The digitized speech can then be stored and processed on a computer.

DRUSS objectives: In software engineering, software systems that are dependable, reliable, usable, safe, and secure.

Encapsulation: Using interfaces to hide inner mechanisms and internal information from outside users in order to improve reusability, access restriction, protection of information from user errors, and maintainability.

Fractal: A term coined by mathematician Benoit Mandelbrot for sets that are self-similar at different scales. For example, the coast line of a country looks ragged in a satellite photo; it still looks ragged from a hang glider; and it still looks ragged under an up-close view of a wave rippling over the sand. Fractals have been used in graphics to draw complex objects from simple forms that can be repeated at all scales.

Generalization: Extending a solution to a broader class of similar problems.

Graphics processing unit (GPU): A chip included in a computer to run the graphical display. Modern GPUs can hold 3D representations of objects and can rotate them to any angle or slide them to any distance computationally, then project the resulting image on to the 2D screen, all in real time.

Heuristics: Procedures for finding approximate solutions to computationally intractable problems. For example, in chess we evaluate proposed moves by a point-counting system for pieces lost; that is much less computing-intensive than enumerating all possible future chessboards. Good heuristics give solutions that are very good most of the time.

if-then-else construct: A form of statement in a programming language that selects between two or more alternative paths in program code. For example,「if sum≥0 then color sum-value black else color sum-value red」is used by accountants to highlight negative numbers in red on their spreadsheets.

Intuition: An aspect of embodied expertise where the expert is able to know immediately how to deal with a situation, based on extensive past experience. The expert may know what to do but cannot explain why.

Logarithm: In mathematics, the logarithm of a given number is the exponent to which a fixed base must be raised to produce that number. Thus, the log-base-2 of 8 is 3 because 23=8. Logarithms are useful for multiplying numbers since the product of two numbers adds their exponents. Take, for example, multiplying 8 by 16. Because 23×24 = 27, we can take the base-2 logs of the two terms (here 3 and 4, respectively), add the logs (yielding 7), and raise the base 2 to the power of the resulting log (here 27). Slide rules multiply by adding the logs of the two multiplicands.

Logic circuits: The basic electronic circuits in a computer. They combine binary signals with operations AND, OR, and NOT and store the results in registers, which are processed by more logic circuits in the next clock cycle.

Machine code: The instructions of an algorithm encoded into binary codes that a computer can recognize and execute.

Neural network: A form of circuit that takes a very large bit pattern as input (such as the 12 megapixels in a photograph) and produces an output (such as faces recognized in the photo). The components of the network are designed to be loosely similar to the neurons in the brain. The network learns by being trained rather than being programmed.

Operating system: The control program that runs a computer system. It allows users to log in and access their data, protects user data from being accessed by others without permission, schedules the resources (CPU, disks, memory) among competing users, and provides an environment in which users can run their programs.

Qubits: The basic elements of a quantum computer. They are the quantum-world analog of bits in a conventional computer, but they have a peculiar property called superposition, which means they can be in the 0 and 1 states simultaneously. Superposition significantly increases their representational and computing power. They are represented by electron spins or magnetic fields.

Race conditions: Many electronic circuits have multiple paths connecting an input to a particular output. If a change of the input travels at different speeds over the different paths, the value of the output can fluctuate randomly depending on the order the signals arrive. That random fluctuation can cause malfunctions in downstream circuits that use the output. Race conditions can also appear in operating systems where two users attempt simultaneous access to a file and the final value of the file depends on which one went last.

Registers: Processor registers are the basic building blocks of storage within a CPU. A register consists of a set of flip-flops, which are small circuits that can store a 0 or 1. Thus, an 8-bit register is made of 8 flip-flops. The CPU instructions combine values in registers and store their results in other registers.

Representation: Computing relies heavily on one thing standing for (representing) something else. Computations require information to be represented in a digital form, such as two values of voltage in circuits or the presence or absence of perturbations on materials. We use 0 and 1 to represent those physical phenomena.

Simulation: Computer simulations rely on computational models of phenomena to track the behavior of those phenomena over time. The elements of a model are theories, variables, equations, parameters, and other known features of the phenomenon in order to faithfully characterize the modeled system. Simulation uses these model elements to see how the system changes from one time unit to the next.

Transfer hypothesis: The hypothesis that learning computational thinking in computer science transfers to problem-solving ability in other fields. The hypothesis would predict that a person who came to be a good problem solver in computer science would be able to solve problems in physics with the same expertise. There is little empirical evidence to support this hypothesis.

Truth values: The two allowed values「true」and「false」of a logic variable. When presented in numbers,「0」is typically interpreted as false and either「1」or any nonzero value as true.

Turing test: A test proposed in 1950 by Alan Turing to settle the question of whether a machine can think. A human observer carries on two text-based conversations, one via a connection to a computer, the other a connection to another human being. The observer does not know which is which. If the observer is unable to definitely identify the human (or machine) over a long period, the machine would be deemed intelligent.