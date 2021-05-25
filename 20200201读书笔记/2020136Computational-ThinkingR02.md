## 记忆时间

2021-05-25

## 目录

0501 Software Engineering

0601 Designing for Humans

## 0501. Software Engineering

Software engineering is the part of computer science that is too difficult for the computer scientist.

—— Fritz Bauer (1971)

At 9:10 p.m. on July 22, 1962, access arms retracted from the 33-meter-tall Mariner I rocket that stood on the launch pad in Cape Canaveral. On top sat a hexagonal magnesium frame packed with high-tech electronics for gathering, analyzing, computing, and communicating scientific data, and an operating system to keep all the systems alive. Destined for Venus, Mariner I was the first of a series of 10 interplanetary NASA probes to do flyby surveys of Mars, Mercury, and Venus. It was the first flyby of another planet in history. Years of work by thousands of people planning, calculating, designing, testing, and building the vessel culminated at that moment. Mariner I was also aiming to get the US ahead of the Soviet Union in the space race. Ten minutes and dozens of checks later the flight control gave a go for final countdown.

Seconds after the rocket fired off toward a new world, monitoring equipment started to indicate problems. The rocket's system for tracking and sending velocity data did not work correctly. The ground control computers were supposed to take over — usually no big deal, as that is what backup systems are for. But somewhere in the long time it took to develop the computer system, someone had missed a tiny punctuation detail in the program, which led the computer to base its decisions on raw data instead of data smoothed over a time window. That error led the rocket to overcompensate for minor perturbations in its trajectory, steering it uncontrollably toward inhabited areas and shipping lanes. At 293 seconds after the liftoff, ground control had no choice but to send a destruct command to the vehicle. Tons of metal, high-tech electronics, and rocket fuel rained down into the Atlantic Ocean.

Initial reports of what caused the massively publicized failure were out within a week, mostly citing that small mistake in the computer program. The New York Times headline was,「For Want of Hyphen Venus Rocket Is Lost.」That sobering moment pushed the concept of programming error into the public consciousness. Many people's eyes opened to the potentially disastrous consequences of software failure. By the end of the 1960s, reports of software problems were commonplace. Software errors impaired reliability, undercut productivity, and sometimes posed serious dangers.

Software developers realized that the era's computational thinking was not capable of delivering reliable and dependable software. Most CT was about thinking in the small — practices and thinking tools for single programmers. There was nothing in CT for thinking in the large — practices and thinking tools for teams of programmers developing large-scale production systems with long life spans and large user bases. Here in this chapter we investigate the important shift of scale in computational thinking and the difficulties it caused.

### 5.1 Software Crises

The early years of the stored-program computer were a triumph of computer engineering. Hardware development, from the「computing super-brain」to the「awesome thinking machine,」made the headlines. The press featured room-sized reckoning behemoths weighing tens of tons that operated a thousand times faster than the previous computing machinery and, most importantly, could calculate thousands of times faster than the world's best mathematicians. Mathematics and logic were celebrated as the feature that distinguished humans from beasts — and now machines could do both.

The early enthusiasm for computers soon moved beyond「makin' numbers」 — as one computing pioneer called scientific computing — to processing data in symbols that can stand for any information at all. Magazines and newspapers gave examples of computers doing tasks that were previously seen as the sole province of humans: one group programmed the computer to play checkers, another chess, another to automatically prove theorems in the monumental Principia Mathematica, and another built a mechanical mouse that searched its way through a maze. The uses of computers in business, science, and engineering applications multiplied each year. All these advances came from software. The computer revolution began with hardware, but soon became a revolution of software.

The size and complexity of computer programs grew rapidly. Dark clouds began to hover over software development. Developers were becoming painfully aware of great difficulties in their ability to make production-quality software — software that was dependable, reliable, usable, safe, and secure. The intellectual and management tools developed up to that time were not powerful enough to build such software. Developers began to speak of a「software crisis.」

In two famous meetings sponsored by NATO in 1968 and 1969, software developers turned to engineering for a solution to the frequent and sometimes catastrophic failures of software. The movement was labeled「software engineering.」Engineering had long traditions for consistently producing reliable systems. It was rare for bridges to fall, planes to crash, or infrastructure to fail massively. Software engineers rapidly began to import and develop engineering ways into software development and software product management.

An early focus in software engineering was the design of「abstractions,」which are simplified models of something complicated with a simple interface. Good abstractions hide the details of the machinery implementing them, allowing programmers to debug them without having to dig into the details of underlying machines. For example, a file is presented as a container of a string of bits with two operations, read and write; its complicated implementation as records scattered across a hard disk is completely hidden. Designing hierarchies of abstractions is seen as the only way to master the enormous complexity of software. Finding good abstractions is an essential design skill for programmers and software engineers. Programming languages that allow programmers to express their abstractions are essential. [1]

1-2『这里的信息有一次刷新了对「抽象」的认知。驾驭复杂软件系统的唯一办法是抽象，做一张主题卡片。（2021-05-24）』—— 已完成

In his classic book The Mythical Man-Month (1975), the software pioneer Fred Brooks noted two dimensions for transforming programs into production systems. One was the generalization of a single software program to a system of interacting programs. The other was the addition of structures and components that provided guarantees to make the software reliable. His rule of thumb was that movement in either dimension tripled the effort. Movement in both dimensions was needed to achieve reliable production systems — a total of nine times the effort of creating a single program.

Software developers, having become aware of such a wide gap between basic programming and production systems, had to find new practices of CT to close it. They developed a trove of new forms of CT: new practices for decomposition, complexity, information structures, causality, closing semantic gaps, data abstraction, data structures, encapsulation, information hiding, recursion, project management, and software life cycles. Aspects of theoretical computer science, notably complexity theory and automatic theorem proving, became helpful in this arena.

The movement described by Brooks can be characterized as moving from computational thinking in the small (designing and writing single programs) to computational thinking in the large (designing software systems and managing the software projects that build them from design and into production and maintenance).

1 Niklaus Wirth, software pioneer and the designer of the popular language Pascal, gives an excellent account of the development of programming practices and their supporting languages (Wirth 2008).

### 5.2 Science and Engineering in Computing

A scientific revolution began in the mid-1500s. For much of the time since, there was little practical difference between science and engineering; scientists look for principles of phenomena and engineers built technologies that exploited the phenomena. Many scientists were engineers and many engineers were scientists. The sharp distinction we see today between science and engineering is recent. [2] The distinction was introduced in the late 1940s when Vannevar Bush advocated the establishment of the US National Science Foundation for government support of basic research. Since that time, academic programs have come to define engineering as the「application of science and mathematics to solve problems of use to people」 — in effect defining engineering as a subset of science. This definition hides the unique contributions engineering can make to software. It obscures the need for interaction between the science and engineering sides of computing to make software reliable.

2『这里的 Engineering 的定义，做一张术语卡片。（2021-05-24）』—— 已完成

We have found three distinctions between engineering and science particularly helpful to understand the contributions each can make to software production. The first concerns the nature of their work. Engineers design and build technologies that serve useful purposes, whereas scientists search for laws explaining and predicting phenomena. Design is among the most commonly used words of engineering, whereas it is uncommon in science. Design in engineering is a process of finding practical, safe, cost-effective implementations. Scientists concentrate on finding and validating recurrences, engineers on listening to clients and proposing technologies of value to them.

2『工程和科学的三大区别，做一张主题卡片。（2021-05-24）』—— 已完成

The second main distinction is how scientists and engineers regard knowledge. Scientists treat knowledge as data and information that have been organized into a「body of knowledge,」which is then available for anyone to use. The scientific method for creating knowledge is a process of standard, disinterested observers gathering and weighing evidence in support of claims that might be added to the body. Engineers treat knowledge as skillful practices that enable design and building of tools and technologies. Engineers are not outside observers; they are immersed in the communities of use. They embody practices for building, maintaining, and repairing technologies; attending to reliability, dependability, and safety in the context of use; and following engineering standards and codes of ethics.

The third main distinction concerns the role of abstractions and models. Science emphasizes models, and engineering emphasizes machines and artifacts. There is a fundamental distinction between modeling machines and building them. Abstractions are useful for what they leave out. Machines are useful for what they leave in. Hardware and software are interchangeable to the theorist, but not to the engineer.

The familiar phrase「the devil is in the details」is an engineer's motto. Engineers must get the details right for systems to work. Scientists want to eliminate the details so that the recurrences stand out.

These differences explain why it has been hard to design software engineering education that actually produces capable software developers. Many software engineering groups are in computer science departments that emphasize the science over engineering. The same balancing problem haunts computational thinking, too: when one or the other worldview dominates, the synergies are lost.

2 Stokes (1997).

### 5.3 Computational Thinking in the Small

A computing pioneer who worked with one of the first computers wrote in his memoir that he still remembered the day when he suddenly realized he would be spending most of the rest of his life looking for mistakes in his own programs. [3] In the 1950s, everyone came to believe this — it was very hard to write programs that worked correctly. Programming was unexplored territory to everyone. Initially, all the first programmers could do was borrow ideas and techniques from other fields and use their ingenuity to get programs to work. Nothing seemed to help avoid making errors while programming. What was earlier envisaged to be a straightforward translation of high-level algorithmic plans to machine instructions was found to be a complex of challenges from incomplete problem specifications, machine idiosyncrasies, poor performance, memory limitations, and debugging. Getting computers work turned out to be an endless cycle of accommodations to surprises and obstacles.

As a result, programming in the 1950s developed an aura of mystique. Programming language pioneers remembered that aura vividly in their memoirs. One wrote that programming in the 1950s was「a black art, a private arcane matter involving only a programmer, a problem, a computer, and perhaps a small library of subroutines. ... Programmers started to regard themselves as members of a priesthood guarding skills and mysteries far too complex for ordinary mortals.」Another described later how the programmers of the 1950s loved their obscure codes and tricks. [4] Yet another wrote that it took until the 1960s before programming started to evolve from a craft to a science. He marveled at how, despite their「primitive」way of thinking about programming, programmers of the 1950s were able to create so many useful programs. [5] Computational thinking of the early computer era was rich but fragmented, and focused on making single programs work on specific machinery.

Many pioneers of computing worked to make the programmer's job easier and less error-prone. They did this by developing and refining programming methodology and programming languages, and by designing sophisticated operating systems. Their innovations began with structural principles for modularity in the machines of the 1950s, which led to computational thinkers starting to increasingly think in terms of subroutines, macros that abbreviated often-used pieces of code, separately compiled modules, linkers that combine compiled modules into full programs, libraries of ready-to-run executable modules, and version control systems that tracked all the software modules built and modified by a team. All these tools helped manage program complexity and reduce errors.

As they gained familiarity with the practices of programming, language designers developed higher-level languages, such as FORTRAN and COBOL around 1958. These languages enabled programmers to express algorithmic statements that were automatically translated by compiler into machine code; they relieved programmers of the burden of direct machine code programming. When they saw that programmers often started by designing the data structures and then a small set of subroutines that performed operations on the structures, language designers enunciated the practice of data abstraction. Data abstraction matured into object-oriented programming languages. Data abstraction has become another key feature of CT: it hides internal mechanisms of program components, while allowing the use of those components through well-defined interfaces. With data abstraction, programmers can focus more easily on what the components do rather than how they do it.

2『补充进「抽象」主题卡片里。（2021-05-25）』—— 已完成

Operating systems designers contributed a raft of important precepts to CT during that same era. Operating systems allow many users to share a single machine by scheduling resources, resolving conflicts, allocating memory among user programs, and multiplexing computing jobs on the processors. Operating systems designers introduced the idea of a system being a「society of cooperating processes,」where a process is an independently executing program in private memory that cannot be accessed by other processes, and where each process stands by to perform a specific service when requested. Operating systems designers invented virtual memory to automate data transfers between memory levels, file systems to store and protect user data, and interprocess messaging systems to exchange data and requests. They invented kernels to provide a professionally built and highly trusted set of programs for all basic operating system functions. Kernels isolated processes and prevented errors in any one from affecting any other.

Today's CT inherits many precepts for programming methodology including modularity, abstraction, information hiding, hierarchical composition, recursion, design patterns, managing digital objects, visualization, verification, and debugging. These conceptual tools require great skill and experience at design. Design has emerged as one of the major areas of development in computing; we will discuss it in depth in chapter 6. CT precepts on languages, methodology, and operating systems all aid productivity and confine or eliminate errors.

Many of those practices became so ingrained in CT that for decades computational problem-solvers have considered them to be basic building blocks of CT. These engineering developments complemented the mathematical side of programming, which in those days focused on structuring programs to facilitate formal proof of their correctness and practices such as the use of recursion.

3 Wilkes, in Metropolis, Howlett, and Rota (1980).

4 Wirth (2008).

5 Dijkstra (1980).

### 5.4 Software Development Drifts into a Crisis

With all these advances in CT, why did a software crisis develop? In the 1950s computing, the machine was the product. Software — as the control programs for the machines — was not something to be packaged and sold. Most programmers focused on programs for their personal or immediate workgroup use, but not on programs to use outside their organization. The computational thinking tools for「programming in the small」supported personal use well, but not large-scale development of complex software products.

A software industry began to evolve from a few software contractors in the 1950s to corporate software developers in the 1960s, and then to mass-market software in the 1970s and beyond. In each of these decades, the revenues of the software industry grew tenfold.

In the 1960s software developers found that selling software was no gravy train. More and more software projects ended up late, over budget, bug-ridden to a point of being useless, or never delivered at all. Post-delivery software maintenance, improvement, and bug fixing were costly, difficult, and sometimes infeasible. Software systems frequently contained lurking bugs that made their applications unsafe for humans or caused expensive failures such as the loss of the Mariner spacecraft.

Software developers who had little familiarity with the target domain often caused large gaps between customer needs and the functions of computational systems. Software developers found that the known principles of design were not up to the task of providing dependable, reliable, usable, safe, and secure software — known as the DRUSS objectives. Professional programmers realized that their computational-thinking skills did not scale up well: something was qualitatively different about a program written by a single programmer and a system that required a team of 300 programmers.

2『软件开发的 DRUSS 目标，做一张术语卡片。（2021-05-25）』—— 已完成

Software companies tried to minimize these problems in two ways. One was to hire highly skilled programmers who could produce many times more code per day with significantly fewer errors than entry-level programmers. Salaries for good programmers shot up: software developers became one of the highest-paid professions in the US.

The other way was to abdicate liability for errors. Software companies adopted a「non-warranty」 — licensing the software to a user only after the user agreed that the company would not be liable for damages caused by errors in the code. This policy contributed strongly to public disillusionment with the computer revolution.

Leading software developers admitted that their tools for programming in the small were simply not up to programming in the large. They had passed the limits of reliable software construction. A number of leading software industry figures, academics, and software developers declared a software crisis and organized the 1968–1969 NATO conferences to address it.

### 5.5 Computational Thinking in the Large

What happens when we go from single programs with single users to systems of many programs with many users? The skills and competences required to write a program of a thousand lines of code are different from those to build software of a million lines of code. The main reason is that large software systems have to be built by teams. Software developers had to learn how to organize and manage teams for successful software development.

Fred Brooks was the manager of a team of 300 programmers who built the IBM 360 operating system in the 1960s. Their system eventually grew to a massive 10 million lines of code. In his book, The Mythical Man-Month (1975), Brooks documented his experience in detail and gave rules of thumb of CT for organizing and designing large systems. One of his famous observations is that time and people do not trade off equally: a team of 12 programmers cannot complete in a month a job that took a single programmer 12 months. Another is that the structure of the software winds up resembling the organization that built it. Brooks concluded that managing the team was a greater challenge than the technology problems the team had to solve.

2『人月神话那本书里，Brooks 对大型软件开发的 2 个洞见，做一张任意卡片。（2021-05-25）』—— 已完成

Although the attendees at the NATO conferences agreed that there was a major「software problem」and that engineering principles might help, they had little agreement on what kind of engineering would do the job. The traditional engineers looked to fault tolerant design, systems thinking, and project management. Theoretically oriented computer scientists looked to mathematical proof (formal verification) to establish that software met its specifications without error and introduced methods such as structured programming and algorithms analysis to facilitate understanding and proofs of programs.

Neither approach made much of a dent in the software problem. Traditional systems engineering did not work well because of a crucial difference between software and large physical systems, such as bridges, buildings, planes, and ships: an error in a single bit of code can cause catastrophic failure such as the crash of a rocket whereas the loss of a minute sliver of material might degrade a large system but would not crash it. Mathematical proof did not work well because it was too difficult for large systems, it said nothing about human aspects such as usability, and it did not address problems in the hardware such as component failures or noise corrupting signals. The software pioneers Brian Randell and Fred Brooks were among the most prescient in saying why software systems are so much harder. Randell said the problem was not programming per se but「multi-person development of multi-version programs.」Brooks, in his 1975 book, said that productizing a program by turning it into a system that could be used safely and reliably by non-programmers was far more challenging than writing the program in the first place.

### 5.6 Design Principles, Patterns, and Hints

Skillful design can make enormous improvements in the size and complexity of software. Operating systems are a good example. Modern operating systems such as Windows 10, MacOS X, or Linux approach 100 million lines of code. It is a triumph of software engineering to produce such systems with very good reliability. All these systems contain a「kernel,」the set of software functions for very basic operations in the system such as starting execution of a program, exchanging messages between programs, or reading files. The functions of kernels have changed little since the 1970s but kernel sizes have exploded from around 20 thousand instructions in early systems to 20 million today — a factor of 1000. The increased size has increased vulnerability to attacks. Nicklaus Wirth attributes this to waste of cheap resources — processor cycles and storage bits. He wrote:

This waste has become ever-present and represents a grave lack of sense for quality. Inefficiency of programs is easily covered up by obtaining faster processors, and poor data design by the use of larger storage devices. But their side effect is a decrease of quality — of reliability, robustness, and ease of use. Good, careful design is time consuming, costly. But it is still cheaper than unreliable, difficult software, when the cost of「maintenance」is factored in. The trend is disquieting, and so is the complacency of customers. (Wirth 2008)

The goals of programming in the large were summarized as the five DRUSS objectives – dependable, reliable, usable, safe, and secure. To achieve these goals software developers work with three kinds of computational thinking practices: design principles, patterns, and hints.

1-2『补充进 DRUSS 术语卡片，并且新增一张「Design Principles, Patterns, and Hints」主题卡片。（2021-05-25）』—— 已完成

Design principles are descriptions of skills and strategies that developers follow when making design decisions. The principles guide them toward designs that meet the five DRUSS objectives.

Design patterns are descriptions of common situations a programmer is likely to encounter. They offer guidance on how to structure the program, or on the process of writing it, for best results.

Design hints are rules of thumb or morsels of advice, most useful to those with advanced skills at systems development.

#### 5.6.1 Principles

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

#### 5.6.2 Patterns

In the early 1990s a group of programmers founded the「software pattern community」movement, inspired by the design-pattern idea of building architect Christopher Alexander. [7] Their idea was that if they could describe a common pattern of software use that has been solved by skilled programmers, they could distill the pattern's essence so that other programmers can imitate it. A software pattern characterizes a large number of situations a programmer is likely to encounter and offers guidance on how to structure the program to best fit the pattern. [8] The number of recognized patterns runs in dozens. Examples are the singleton pattern, which limits the number of instances of an object to one, and the iterator pattern, which implements sequential access to data elements. The pattern community appeals to a sense of empiricism because its members are relentless about testing ideas with potential users and learning from the feedback.

1-2『有一次看到了「设计模式」起源的信息，起源于建筑行业，墙里开花墙外香。已下载书籍「」。而且又见到了四人帮的设计模式经典书籍，已下载书籍「2019087Design-Patterns」。（2021-05-25）』

#### 5.6.3 Hints

Butler Lampson, a superb and accomplished designer, summarized a number of guidelines for advanced designers of operating systems. [9] He said:「Designing a computer system is very different from designing an algorithm. The external interface is less precisely defined, more complex, and more subject to change. The system has much more internal structure and hence many internal interfaces. And the measure of success is unclear.」He said the less skilled designers often flounder in seas of possibilities, not knowing how a current choice will affect future choices of the performance of the system. He called his statements「design hints」because they are judgments skilled designers learn to make over time; they emphasize the considerable art in designing. 

2『已下载论文「2021042Hints for computer system design」并存入 Zotero。（2021-05-25）』

In table 5.2 we list Lampson's hints for three dimensions of system development (rows) and major aspects of the DRUSS objectives (columns). Though they may appear as generalities, they are quite meaningful in shaping the CT skills of advanced designers.

Table 5.2 Lampson's Design Hints

| - | Correctness & Fit | Speed | Fault Tolerance |
| --- | ---- | ---- | --- |
| Use cases | Separate normal and worst cases | Safety first, Shed load, End-to-end | End-to-end |
| Interface | Keep it simple, Do one thing well, Don't generalize, Get it right, Don't hide power, Use procedure arguments, Leave it to the client, Keep interface stable, Keep a place to stand | Make it fast, Split resources, Static analysis, Dynamic translation | End-to-end, Log updates, Make actions atomic |
| Implementation | Plan to throw one away, Keep secrets, Reuse a good idea, Divide and conquer | Cache answers, Use hints, Use brute force, Compute in background, Batch processing | Make actions atomic, Use hints |

6 Saltzer and Schroeder (1975).

7 Alexander (1979).

8 Gamma et al. (1994).

9 Lampson (1983).

### 5.7 Design Principles for Software

The software engineering literature records a large number of design principles that have been widely studied and found to be strongly supportive of good design. The very best of these principles have been encoded as structures that appear in languages, application programs, and operating systems. They are mentioned frequently in discussions of CT and their roots lie in many different intellectual traditions described in earlier chapters of this book. They are in three main categories:

1 Hierarchical aggregation.

2 Virtual machines.

3 Clients-servers.

These structures are intended as tools to help with recurrent patterns that designers encounter.

#### 5.7.1 Hierarchical Aggregation

Hierarchical aggregation means that objects (identifiable software and hardware components) consist of groups of smaller objects connected by well-defined interfaces. You can interact with an object as a unity through its interface and not be concerned with its individual parts. When you do look inside, you need not be concerned with what is going on in the external environment. Thus, there is a hierarchy with smaller aggregates making up larger aggregates. Aggregates at every level of the hierarchy are insulated from lower- and higher-level details.

There is a long list of aspects of hierarchical modularity. Decomposition means to subdivide a large system into smaller, manageable components. Modularity is a process of implementing the components as modules that can be designed separately, compiled separately, stored separately, and then assembled into the full system. The modules interact across precisely defined interfaces. Modules can be stored in libraries and reused for other purposes. Abstraction means to define a simplified version of something and to state the operations (functions) that apply to it. Levels are a structural form in which peer components share a common interface. [10] Information hiding conceals the details of an implementation from users, protecting users against errors caused by changes in the details and protecting the module from errors caused by external changes. Encapsulation goes further, by shielding anything outside an untrusted module from errors within the module.

The object concept is an advanced form of encapsulation; it originated with a programming practice called「data abstraction」in the 1960s and evolved into over a hundred sophisticated object-oriented languages today. An object is an abstract entity that can be viewed and altered only through a defined set of operations. Its internal structure and state are hidden. For example, a file appears to users as a container of a sequence of bits and can be acted on only with the open, close, read, or write operations; its hidden internal structure is a set of records scattered across a disk. The disk structure of a file is irrelevant to users and hence hidden from them. A class of objects is a set of objects with the same interface; the classes are organized into a hierarchy of their own. Novice programmers often find objects confusing because they do not yet understand abstract machines, information hiding, and synchronization.

10 The levels principle was first used by Edsger Dijkstra in 1968 to organize the software of an operating system. It facilitated a correctness proof of the system because each level depended only on its components and the correctness of the lower levels, but not the higher levels. The discipline of designing a system as levels leads to much smaller and more easily verified systems.

#### 5.7.2 Virtual Machines

A virtual machine is a simulation of one computer by another. Alan Turing's universal machine was the first example. Today the term virtual machine is used in a number of ways. First, it means the simulation of any abstract computing machine; it is the platform on which computations can run.

Second, virtual machines are simulations of hardware computers. The virtual machine has subroutines that carry out the effect of the machine instructions on the hardware computer. This idea came into practice in the late 1950s when a second generation of computers began to replace the first generation. The new computers had to run all the software written for previous versions of the computer. Accordingly, manufacturers provided an「emulation mode」in which the new computer could simulate the instructions of the older computer it replaced. The emulation mode has matured in the form of VMware and Hyper-V, which simulate entire computers running their own operating systems. The ubiquitous Java Virtual Machines (JVM) emulate Java on any commercial machine by executing the Java「byte code」produced by Java compilers, allowing great portability of Java programs.

Third, virtual machines are simulations of a host machine within separate memory partitions of the host machine. This is the organizing principle of the IBM VM 370 and later operating systems. The IBM virtual machine is a complete simulation of an IBM mainframe, identical in every way to the original except that it has a reduced main memory. This approach allows the virtual machine to run at nearly the same speed as the real machine; there is no significant performance loss.

Fourth, a virtual machine is a standard environment for implementing any program within an operating system. This idea was pioneered in the Multics system at MIT (1968) and the UNIX system at Bell Labs (1972). These operating systems featured many「processes,」each a program in execution on a virtual machine. The virtual machine was simply a standard template for providing input and output to a running program and connecting with any submachines it may have spawned. Every user program would be embedded into the standard virtual machine for execution.

#### 5.7.3 Clients and Servers

The client server model is a conceptually simple way to organize interactions between processes in a distributed (networked) computing system. A server is a process dedicated to performing a particular service on request. A client is another process that makes requests. Clients and servers are usually (but not always) on different hosts in a network. Their requests and responses are passed as messages through the network. For example, a network file server stores all the files of the network's users; client processes on user workstations send it requests to read and write files. An authentication server interacts with the login client on a user's workstation to process the user's credentials during login. A web server interacts with client browsers to send them web pages.

Although the client server idea is simple, its implementations are often far from simple. Designers must master many subtle details to get communications, error control, and synchronization working correctly.

### 5.8 No Silver Bullet

In 1987, Frederick Brooks wrote「No Silver Bullet,」a famous assessment of progress in software engineering since 1968. His conclusions held important lessons for CT. He said that two main complexity factors affect our ability to produce reliable software. The limitations of the technology are the first factor, but they can be overcome by improved technologies, such as high-level programming languages, interactive program development environments, visualization of control and data flow, faster hardware, and better operating systems.

The second factor is our own mental ability to comprehend the essence of complex problems. Coping with complexity is intrinsic to software design and construction and will never go away. The design problem, Brooks said, is mostly conceptual — getting an intellectual grasp on the functions of the system to provide and organize a simple and elegant design.

2『布鲁克斯在人月神话里提出的「No Silver Bullet」做一张主题卡片。（2021-05-25）』—— 人月神话

To address it, we need to grow large systems in relatively easy increments, reuse existing software as much as possible, and make more use of rapid prototyping to gain early feedback before technical decisions are locked. Most of all, Brooks said, we need to「cultivate great designers.」He saw coping with complexity as an essential skill requiring great mastery. Brooks famously wrote that there is「no silver bullet」that will kill the werewolf of complexity in software development.

The「software problem」articulated in the NATO conferences was mostly concerned with programmer productivity and the chronic problem of errors causing unreliable programs. Since those days new developments have added to the complexities of software design. These include:

The main factor impeding reliable software is our own mental ability to comprehend the essence of complex problems. Coping with complexity is intrinsic to software design and construction and will never go away.

Malware and intruders: Criminals and hackers intentionally hunt for bugs in complex programs and exploit them for theft of data, destruction of data, and even ransoms to unlock purposely encrypted data.

Fault tolerance: Even if the software has been proved to be correct, the proof depends on assumptions that the underlying hardware always works as intended. Hardware itself is now so complex that proving it correct is a major challenge of its own. Many hardware bugs have been detected in supposedly well-tested chips. Not only that, but hardware can wear out and start malfunctioning because of component failures or because unexpected events in the world throw it into unstable states. Hardware engineers have increasingly been concerned with fault tolerance, that is, designs that tolerate such faults — for example, a system that shuts itself down rather than perform a critical operation incorrectly. This kind of hardware fault tolerance, which involves extra circuits that monitor each other, cannot be done with any software structure. Software correctness proofs are not sufficient for correct operation.

Secure hardware: Most attacks on computer systems occur at the lowest levels of the kernel and network where efficient dynamic monitoring is most difficult to do. In the 1960s there was considerable interest in hardware design that would facilitate information protection by limiting the spread of errors and blocking software attempts to circumvent permissions. Highly advanced architectures were designed that enabled encapsulation of untrusted programs and severely limited error propagation.

Unfortunately, these advances were lost in the「RISC revolution」of the 1980s. To build faster CPUs, computer designers eliminated hundreds of instructions from CPUs, reducing them to highly simplified, very fast chips. They called the new generation of chips Reduced Instruction Set Computers (RISC). The reductions eliminated the hardware extensions for encapsulating and monitoring software.

Today, security experts want to reinstate the extra hardware monitoring to block the low-level attacks by malware and intruders. Secure hardware is making a comeback. A complicating factor is the fact that many companies outsource production of their chips, making it possible for third parties to insert backdoors into the hardware that allow intruders easy access to the system.

Machine learning algorithms: The recent explosion of artificial intelligence (AI) is due primarily to rapid growth in neural network technologies. When the training process of a neural network is done, no one knows why the internal connection weights are what they are or how to prove the network is correct for untrained inputs. Similarly, there are no hardware monitors to detect when a neural network is about to go bad. This has been called the fragility problem: To what extent can we trust the AI to do the right thing when presented with inputs outside its training data?

Safety: Many software systems are used in safety critical applications, where an error in the software can cause catastrophic loss of life or property.

Mass production of diverse software applications: Today's mobile apps, games, desktop widgets, and network-based systems have little in common with the software of the 1960s and 1970s. There was little outsourcing of software development to trusted third parties. There were no large networks of application developers selling through app stores before the early 2000s; the Apple and Android stores now offer millions of apps.

Computational thinking is being constantly challenged to grow and deal with these contemporary problems.

### References and Further Reading

Alexander, Christopher. (1979). The Timeless Way of Building. Oxford University Press.

Brooks, Frederick P. Jr. (1975). The Mythical Man-Month. (20th anniversary edition, 1995). Addison-Wesley.

Brooks, Frederick P. Jr. (1987). No silver bullet: Essence and accidents of software engineering. IEEE Computer 20 (4): 10–19.

Campbell-Kelly, Martin. (2003). From Airline Reservations to Sonic the Hedgehog. MIT Press.

Denning, Peter. (2018). Interview with David Parnas. Communications of ACM 61 (6) (June).

Ensmenger, Nathan L. (2010). The Computer Boys Take Over: Computers, Programmers, and the Politics of Technical Expertise. MIT Press.

Gamma, Erich, Richard Helm, Ralph Johnson, and John Vlissides. (1994). Design Patterns: Elements of Reusable Object-Oriented Software. Addison-Wesley.

Koen, Billy V. (2003). Discussion of the Method: Conducting the Engineer's Approach to Problem Solving. Oxford University Press.

Lampson, Butler. (1983). Hints for computer system design. Proc. ACM Symposium on Operating Systems Principles, 33–48.

Metropolis, N., J. Howlett, and Gian-Carlo Rota, eds. (1980). A History of Computing in the Twentieth Century: A Collection of Essays with Introductory Essay and Indexes. Academic Press.

Mitcham, Carl. (1994). Thinking Through Technology: The Path Between Engineering and Philosophy. University of Chicago Press.

Saltzer, Jerome H., and Michael D. Schroeder. (1975). Protection of information computer systems. Proceedings of the IEEE 63 (9) (September): 1278–1308.

Stokes, Donald E. (1997). Pasteur's Quadrant — Basic Science and Technological Innovation. Brookings Institution Press.

Wirth, Niklaus. (2008). A brief history of software engineering. IEEE Annals of the History of Computing, 30 (3): 32–39.

## 0601. Designing for Humans

Descriptions of software entities that abstract away their complexity often abstract away their essence. Good judgment comes from experience, and experience comes from bad judgment.

—— Frederick Brooks (1986)

We are searching for some kind of harmony between two intangibles: a form which we have not yet designed and a context which we cannot properly describe. Making simulations of what you're going to build is tremendously useful if you can get feedback from them that will tell you where you've gone wrong and what you can do about it.

—— Christopher Alexander (1964)

Among computing's early pioneers, George Forsythe was one of the first to advocate that computing deals primarily with issues related to design: design of computers and systems, design of languages for processors and algorithms, and design of methods for representing and processing information. [1] Software engineers were among the first within computing to explicitly treat design as an essential part of the discipline's practice. For software engineers, design meant planning and construction of software products and systems that met their specifications and were safe and reliable. Design also meant creating tools to support software construction including related languages, editors, voice command and graphical interfaces, project management practices, version control systems, and development environments. [2] The recent proliferation of useful applications through commercial「app stores」has brought a lot of people who are not formally trained in software engineering into software design.

But there is more to design than building systems. Design is familiar in many fields including fashion, products, and architecture. It is a process of creating and shaping artifacts that address human concerns. In software, for example, design means crafting software that does jobs users want done. Software designers do far more than build to meet functional specifications. They intentionally support practices, worlds, contexts, and identities of the software's users. The famous success of the iPhone is attributed not only to its considerable technical prowess, but also to the identities and fashion statements iPhone users project. There have also been notorious failures attributed to poor design that promoted unsafe use of systems, such as aircraft panel displays that did not show the most needed information in emergencies. [3]

We discussed in chapter 5 how software engineers have accumulated much practical wisdom that is expressed with design principles, patterns, and hints, all in pursuit of the DRUSS (dependable, reliable, usable, safe, and secure) objectives. But design concerns go much further than just improving the software construction process.

Despite the successes of software engineering, software project failures and accidents continue to accumulate. Academics continue to struggle with software engineering curricula that can graduate professional software developers who can lead projects to completion without failure. David Parnas, a famous software pioneer, says that this academic quest is doomed in many departments because most curriculum attempts have tried to identify and teach a「software engineering body of knowledge」rather than the capabilities of proficient professional software designers. [4] Computing students are taught structural rules for software but not the design skills required to achieve good software. Table 6.1 summarizes the capabilities Parnas believes are the most important. All these capabilities are oriented toward the user communities and are not restricted to formal aspects of software development process. Design CT guides us to ways of building computing systems whose behaviors are useful and meaningful in their user communities.

Design is familiar in many fields including fashion, products, and architecture. It is a process of creating and shaping artifacts that address human concerns. In software, design means crafting software that does jobs users want done.

Table 6.1 Capabilities of Software Developers

1 Design human-computer interfaces.

2 Design and maintain multi-version, reusable software.

3 Ensure that software products meet quality and security standards.

4 Create and use models in system development.

5 Specify, predict, analyze, and evaluate performance.

6 Be disciplined in development and maintenance.

7 Use metrics in system development.

8 Manage complex projects.

1 Forsythe (1966).

2 Grudin (1990).

3 Leveson (1995).

4 Parnas and Denning (2018).

### 6.1 What Is Design?

Many software developers have turned to design for new thinking that would lead away from the software morass. The long history of design in computing has left many questions open for the designers: What is the difference between software engineering and design? Why has it taken 50 years for the early declarations on design to become a prominent concern? How important is design to CT?

The software engineering approach to design is a semiformal methodology to craft a set of modules and interfaces to achieve a stated functional purpose. The purpose is captured in a set of requirements, each a specific, testable statement. A traditional engineering process moves from requirements to a working, delivered system:

1 Requirements.

2 Formal specifications.

3 System construction.

4 Acceptance testing.

5 Delivery to the customer.

Software engineers can carry out this process in private, bypassing any interaction with the users in between the requirement and delivery stages. The process is attuned to the early notions in computing that software is machine-executable code for algorithms that meet given functional specifications, and that programmers need quiet time to get things right.

But experience has shown that the traditional engineering process is prone to break down with complex systems. Roughly a third of software projects deliver on time and within budget, another third deliver late or over budget, and the remainder never deliver. One of the biggest challenges is the sheer number of modules and interfaces that must be designed, programmed, tracked, and tested — modern operating systems, for example, consist of hundreds of thousands of modules. Another big challenge is getting the requirements right: many software projects meet their formal requirements only to be judged deficient by their customers. From the engineer's standpoint, a necessary requirement was left out. From the user's standpoint, the missing requirement was obvious to any member of the community. The disconnect is that something obvious to the community may not be obvious to the engineer, who was not aware of an issue that was part of unstated user context.

The software engineering approach to design is a semi-formal methodology to craft a set of modules and interfaces to achieve a stated functional purpose. The design approach focuses on the virtual world created by the software, the practices that engage users in that world, and the user concerns addressed by that world.

Engineers responded to these breakdowns by trying to improve the construction process. They developed sophisticated interview methods to elicit requirements from customers and thus minimize the risk that an important requirement was left out. They codified「design patterns」followed by successful designers, so that less experienced designers could avoid mistakes. They introduced「agile methods」for project management that explicitly involved customers through all stages of the engineering project. Agile product management often features many, rapidly iterated prototypes under constant review by teams that include customer representatives.

These process improvements slowed but did not stem the tide of system failures. Some designers advocated a radical shift of thinking. Terry Winograd, a pioneer in artificial intelligence and design, characterized the shift in this way: [5]

The education of computer professionals has often concentrated on the understanding of computational mechanisms, and on engineering methods that are intended to ensure that the mechanisms behave as the programmer intends. The focus is on the objects being designed: the hardware and software. The primary concern is to implement a specified functionality efficiently. When software engineers or programmers say that a piece of software works, they typically mean that it is robust, is reliable, and meets its functional specification. These concerns are indeed important. Any designer who ignores them does so at the risk of disaster.

But this inward-looking perspective, with its focus on function and construction, is one-sided. To design software that really works, we need to move from a constructor's-eye view to a designer's-eye view, taking the system, the users, and the context all together as a starting point. When a designer says that something works (for example, a layout for a book cover or a design for a housing complex), the term reflects a broader meaning. Good design produces an object that works for people in a context of values and needs, to produce quality results and a satisfying experience.

Winograd and others introduced the term virtual world for the focus of software design. Software creates a world — a context in which a user of the software perceives, acts, and responds to experiences. A user who enters the world and behaves according to its rules and logic is called an inhabitant because the world seems real during the time the user is in it. The key point is that the virtual world is not a mental construct of user or designer, it is an experience that seems real.

Online games are examples of virtual worlds. In them the players defeat monsters, seek out treasures, earn achievements for quests, and advance in level and experience. Many players say that the world of the game is as real as the everyday world when they are in it. These games create a world by having a definite purpose, a playing field and equipment, norms and values, rules for allowable and unallowable behavior, and strategies for winning or advancing. But the idea of creating a world is not limited to entertainment games. Today's social networks, and services such as Uber, Airbnb, and eBay, all look like multi-player games, where the possibilities available to you as a player evolve and shift according to the choices and actions of others. Even single-user software such as spreadsheets, word processors, and drawing programs all create worlds of their own in which there is a well-defined playing field and a set of basic rules and strategies for all to follow.

Since 2005, when Apple introduced the App Store and made iPhones infinitely customizable as users downloaded apps (applications) that suited them, there has been an explosion of software development of apps. The Apple and Android online app stores combined offer more than 6 million apps. Software has become a market commodity. Only the apps judged by their many customers as「high quality」make it in this market.

5 Winograd (1983).

### 6.2 Software Quality and Satisfaction

In the 1970s, software engineers sought to make software quality measurable, on the time-honored premise that we get more of what we measure. They devised models for measuring software quality. Their models eventually became a standard of the ISO (International Standards Organization), and a central building block of computational thinking in software engineering. The ISO standards list 20 measurable factors to assess overall quality of a software system:

correctness | reliability | integrity | usability | efficiency | maintainability | testability | interoperability | flexibility | reusability | portability | clarity | modifiability | documentation | resilience | understandability | validity | functionality | generality | economy

These measures were all intended to be objectively measurable properties of the software. It is very hard to design a software system that scores high on all 20 factors. Two of the five traditional DRUSS objectives — security and safety — are not on this list because no one knew how to measure software for these aspects. No one said that quality is simple and straightforward.

The new and burgeoning market for apps has brought attention to quality as an assessment of users rather than as a property of the software. Quality is in the eye of the beholder. Much more attention is paid to design in the sense that Winograd has defined it. How do users assess quality — and, by implication, good design? Table 6.2 presents six distinct levels of satisfaction in the user's experience. [6]

Each level on the software quality ladder involves a skill level of computational thinking. The lowest levels are undisciplined use of CT; the highest levels are disciplined CT to design for customer practices, breakdowns, and evolving concerns. The higher the level, the more professional and advanced aspects of CT are involved. Ascending the ladder, CT skill extends its sensibilities from formal requirements to customer concerns and futures; the level of customer satisfaction rises.

6 Denning (2016).

#### Level −1: No Trust

Customers do not trust the software. It may be buggy, crash their systems, hold their data for ransom, or carry malware. One might think customers would avoid untrusted software. But instead they do often use untrusted software — often after being lured by fraudulent pitches, phishing, visits to compromised websites, overwhelming desires for convenience, and the like. Programs at this level are often cobbled together without serious thought to the DRUSS objectives and many are aimed at exploiting customer weaknesses.

Table 6.2 Levels of Software Quality and Satisfaction Assessments

| - | Quality Level | Skill level of CT |
| --- | --- | --- |
| 4 | Software delights | Design software to anticipate evolution of customer practices and concerns after using the software |
| 3 | Software produces no negative consequences | Design software to avoid potential customer breakdowns |
| 2 | Software fits environment | Design software to align seamlessly with customer practices and social norms |
| 1 | Software fulfills all basic promises | Design software to meet all customer requirements via disciplined use of programming and software engineering CT |
| 0 | Some trust, begrudging use, cynical satisfaction | Design software with indifference toward the customer, modest CT discipline |
| -1 | No trusts | Exploit the customer, little CT discipline |

#### Level 0: Cynical Satisfaction

Many customers trust some but not all the claims made by the software maker — enough to be cynically willing to use it. Much software is released with bugs and security vulnerabilities, which the developers fix only after hearing customer complaints and bug reports. User forums are rife with stories about how the software has failed them and with requests for workarounds and fixes; representatives of the developers are usually nowhere to be seen in these forums.

Using some intermediate CT practices, developers get their software working despite design flaws and holes that demand workarounds. The developers may tolerate their disorganized and haphazard development environment because they are under strong pressure to get something workable to market before the competition, they believe that customers will tolerate many bugs, and they evade liability with no-responsibility license agreements customers must sign to unlock software. This approach is common in the software industry. It is coming under fire because the many bugs are also security vulnerabilities. Cynical customers have no loyalty and will desert to another producer who makes a better offer.

#### Level 1: Software Fulfills All Basic Promises

The customer assesses that the producer has delivered exactly what was promised and agreed to. This level of basic integrity relies on more advanced programming and software engineering CT. The ISO standard addresses this level well. Software developers at this level are often standards-oriented and their practices are aimed at producing consistent, reliable products.

#### Level 2: Software Fits Environment

At this level, the design extends beyond meeting the stated requirements. It aims to align the software with existing customer practices and it honors cultural sensibilities and other social norms. The customer assesses that the software is a seamless fit to the customer's environment. The bank ATM is a good example of this kind of alignment. The ATM implements familiar bank transactions, enabling customers to use an ATM immediately without having to learn anything special or new. The customer has the experience that the software improves the customer's ability to get work done and to carry out important tasks.

#### Level 3: Software Produces No Negative Consequences

At this level, the designer has examined a range of possible ways that the software could produce breakdowns for the customers and builds in operating rules and checks to avoid them. After a period of use, customers encounter no unforeseen problems causing disruption or losses. Customers assess that the product's design has been well thought out and that it anticipates problems that were not apparent at the outset. The software does not produce negative consequences that often arise on the lower quality levels, such as vulnerabilities to hackers and malware, vulnerabilities to user mistakes without the provision to cancel actions or back out to a previous good state, interference with the organization's practices, wasted effort for only marginal productivity gains, and frustration with other negative consequences to customers or their organizations.

At this level, designers may also include functions that the customer did not ask for but that will spare future frustration. Continuous backup systems are one example; the user can retrieve any previous version of a file and can transfer an entire file system to a new computer quickly. Utilities that rebuild damaged files or directories are another example. Still another example are internal management controls that allow the designer to continue to work with the customer after the software is installed in order to modify the software in case negative consequences are discovered. These actions — anticipation of breakdowns and availability of repair services after delivery — are essential for a software producer to earn the user's satisfaction at this level. Programming and software engineering CT do not orient software developers to this direction; design-oriented CT is required.

#### Level 4: Software Delights

At the highest level the software goes well beyond the customer's expectations and produces new, unexpected, sometimes surprising positive effects. The user expresses great delight with the product and often promotes it among others. The customer assesses that the producer understands the customer's world and contributes to the customer's well-being. Programming and software engineering CT cannot approach this because delight cannot be stated as formal requirements.

Very few software systems have produced genuine delight. Some early examples include the UNIX system, which was elegant and enabled powerful operations with simple commands; the Apple Macintosh, which brought a revolutionary, easy-to-use desktop with a bitmapped display; the DEC VAX VMS, which was amazingly stable and retained previous versions of files for fast recovery; VisiCalc, the first automated spreadsheet, which made easy accounting available to anyone; Lotus 1-2-3, a successor of VisiCalc, which enabled arbitrary formulas in cells and opened a new programming paradigm; Microsoft Word, which made professional document formatting easy and eventually banished most other word processors from the market; and some smartphones, which provide a reasonably secure environment to download apps that customize the device to the user's taste and identity.

Some smartphone apps have attained high delight ratings; for example, many airlines, publishers, and newspapers offer apps that give direct access to their content via a mobile device. Some apps give users access to networks where data from many others are aggregated to give the user something that saves a lot of time and anxiety. For example, Amazon created the Kindle reader service that enables users to purchase ebooks from the Amazon store and begin reading them instantly from any device with a Kindle app. Google and Apple maps use location information from smartphones to detect traffic congestion, overlay it on street maps, and propose alternate routes around congested areas. Blizzard Entertainment accumulated as many as 10 million subscribers to its World of Warcraft online game because of its rich complexity, easy entry, and detailed graphics. Uber allows users to hail rides whose drivers come to their exact location within minutes. In each case customers found they could do previously impossible things with the app than without, well beyond their expectations.

The interesting thing about these examples is that many of them failed important ISO metrics such as portability, speed, efficiency, or reliability. Yet customers ignored those shortcomings and became avid and loyal subscribers to the software developer.

Software developers are banking on new delights as artificial intelligence technology matures. Many people are looking forward to driverless cars, personal assistants that know your daily routines and overcome your forgetfulness, and virtual reality tools that allow you to tour distant places, train risk-free for a new skill or environment, or access new kinds of entertainment. Computational thinking that takes design deep into the organizational, human, and social aspects of computing have never been as important as today.

But delight is ephemeral if based only on the software itself. Having mastered the new environment, customers will expand horizons and expect more. Few would find the original UNIX, Macintosh, VMS, VisiCalc, or Word to be delightful today. Software producers now invest considerable effort into knowing their customers and anticipating what will delight next.

### 6.3 The Design Way of Computational Thinking

The software engineering way of computational thinking emphasizes the correct implementation of clearly stated functional requirements in software. Its success measures are properties observable in the software or its usage data.

The design way of computational thinking also emphasizes the construction of virtual worlds in which users can inhabit and achieve some purpose that is meaningful to them. Its success measures are assessments of satisfaction and quality by users.

Software engineering CT is especially useful for large systems that must perform reliably in safety critical environments. People want carefully engineered air traffic control systems, nuclear plant control systems, and Mars rovers. Design CT is especially useful for software that must fit customer communities, facilitate adoption, and deliver great value. Design CT does not abandon software engineering CT; it listens for opportunities to include delightful functions customers have not yet asked for.

As we described earlier in this chapter, to characterize design CT we have proposed six levels at which customers assess software quality and satisfaction. Program correctness is essential but produces satisfaction only at the first level. The highest level, delight, arises in the context of the relationship between the customer and software developer. The delighted customer will say that the developer has taken the trouble to understand the customer's work and business, is available to help with problems and to seize opportunities, may share some risks on new ventures, and generally cares for the customer. Software developers today look to designs and services that produce genuine delight. When they succeed we witness new waves of killer apps.

### References and Further Reading

Brooks, Frederick P. Jr. (1975). The Mythical Man-Month. (20th anniversary edition, 1995). Addison-Wesley.

Denning, Peter. (2016). Software quality. Communications of ACM 59 (9) (September): 23–25.

Forsythe, George E. (1966). A University's Educational Program in Computer Science. Technical Report No. CS39, May 18, 1966. Stanford University: Computer Science Department, School of Humanities and Sciences.

Grudin, Jonathan. (1990). The computer reaches out: The historical continuity of interface design. In CHI '90: Proceedings of the SIGCHI Conference on Human Factors in Computing Systems, 261–268. ACM.

Landwehr, Carl, et al. 2017. Software Systems Engineering Programmes: A Capability Approach. Journal of Systems and Software 125: 354–364.

Leveson, Nancy. (1995). SafeWare: System Safety and Computers. Addison-Wesley.

Norman, Donald A. (1993). Things That Make Us Smart. Basic Books.

Norman, Donald A. (2013). The Design of Everyday Things. First edition 1983. Basic Books.

Parnas, Dave, and Peter Denning. (2018). An interview with Dave Parnas. Communications of ACM 61 (6).

Winograd, Terry, and Flores, F. (1987). Understanding Computers and Cognition. Addison-Wesley.