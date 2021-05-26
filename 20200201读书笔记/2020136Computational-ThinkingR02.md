## 记忆时间

2021-05-25

## 目录

0501 Software Engineering

0601 Designing for Humans

0701 Computational Science

0801 Teaching Computational Thinking for All

0901 Future Computation

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

## 0701. Computational Science

The sciences do not try to explain, they hardly even try to interpret, they mainly make models.

—— John von Neumann (1955)

Computational science refers to the branches of every scientific field that specializes in using computation, such as computational physics, bioinformatics, and digital humanities. Although numerical methods have been a feature of science for centuries, simulation of complex systems was rarely viable before computers. Scientists developed mathematical models, usually expressed as sets of differential equations, but unless they could find closed-form solutions to the equations, the complexity of the models usually blocked them from any effective method to calculate the results. Although computers slowly began to invade all fields of science in the 1950s, the supercomputers in the 1980s were a tipping point in mustering the computing power to solve a rapidly increasing number of these equations by simulation. This led to an explosion of simulation models in science, some of which made discoveries that earned Nobel Prizes. By the mid-1980s, many scientists were counting computer simulation as a new way to do science, alongside the traditional ways of theory and experiment.

In the 1980s, scientists from many fields came together to formulate「grand challenge problems」 — problems for which their models gave solutions that required massive computations. By extrapolating Moore's law on the doubling chip speed every two years, they were able to predict with considerable accuracy when computation was going to yield solutions of these challenges. For example, aeronautics engineers projected that by 1995 they could design a safe commercial airliner using simulation as a substitute for wind tunnel testing — and the Boeing company achieved this with its 777 aircraft, which flew its first test flights in 1994.

Computer simulations got so good they could be used as experimental platforms. With simulations, scientists were able to explore the behavior of complex systems for which there were no analytical models. Simulations also opened the door for a new way of exploring the inner workings of the nature: by interpreting natural processes as information processes and simulating them in order to understand how they work.

The computational turn of science and its new methods and tools were widely adopted and the change was radical. Computational methods were described as the most significant scientific paradigm shift since quantum mechanics. The computational-science revolution ushered in a new wave of computational thinking. But unlike the previous waves of CT — which were initiated by computer scientists — scientists in other fields initiated the new CT wave. Computational science became a major driving force in the development of CT outside computing.

During the 1980s and the 1990s, computational thinking provided the mental toolbox for the new computational sciences — co-developed across many fields. In fields where natural phenomena could be interpreted as information processes, CT became a must-have skill for researchers. In an ironic twist, where previous scientists had argued that computing is not a science because there are no natural information processes, the new generation of computational scientists found information processes all over nature. And like computer scientists of the 1950s and 1960s, computational scientists learned CT from the practice of designing computations to explore phenomena and solve problems in their fields.

In this chapter, we describe how computational thinking became central to sciences, explain a number of CT practices in computational science, and discuss the new ways in which computational scientists interpret their subject matter. The electronic computing age brought some remarkable advances to science in three aspects: simulation, information interpretation of nature, and numerical methods.

### 7.1 Science and Computation: Old Friends

Science and computation have been old friends for centuries. Through most of the history of science and technology, two sorts of scientist roles have been common. One is the experimenter, who gathers data to explore and isolate phenomena, describe recurrences, and reveal when a hypothesis works and when it does not. The other is the theoretician, who designs mathematical models to explain what is already known and uses the models to make predictions about what is not known. The two roles were active in the sciences well before computers came on the scene.

2『科学家里的三类角色，做一张任意卡片。（2021-05-25）』—— 已完成

Both roles used computation. The experimenters produced data that had to be analyzed, classified, and fit to known mathematically formulated laws. The theoreticians used calculus to formulate mathematical models of physical processes. In either case, they could not deal with very large problems because the computations were too extensive and complex.

A third role emerged: scientists who saw new opportunities using computers as simulators that neither the experimenters nor the theoreticians used. The computing pioneers at the Moore School, home of the ENIAC, argued early on that computer simulation could make any computer into a laboratory. They saw the evaluation of models and the production of data for analysis as a new frontier of science. Crossing that frontier required new ways of incorporating modeling and simulation into research, as well as new kinds of computational thinking directly relevant to science.

Large-scale modeling and simulation required significant upgrades to mathematical software. Numerical analysts, a branch of early computer scientists, were heavily involved in the quest to improve mathematical software to efficiently calculate mathematical models on computers. They were especially concerned with representing numbers and performing long calculations in machines that could only offer finite precision; controlling round-off errors and increasing computational speed were major concerns.

In the late 1980s, John Rice, a pioneer of mathematical software, estimated that mathematical software had improved in performance by a factor of 10^12 since the 1950s. Of that improvement, 10^6 was due to faster hardware and another 10^6 due to better algorithms. Moore's law was only part of the reason numerical methods got better. The ingenuity of the numerical analysts did the rest.

The idea of using calculus to evaluate mathematical models must have seemed obvious to the modelers because their equations were typically differential equations. Many physical processes could be described by relating the value of a function at a point to the values of the function at neighboring points. For example, a modeler who knew that the rate of change of function f(t) was another function g(t) could calculate the values of f(t) in a series of small time steps of size Δt with the difference equation f(t+Δt) = f(t) + g(t)Δt. The sequence of Δt-separated time points is a time-series sample of the function. This idea is easily extended to functions over space coordinates (x,y) by relating f(x,y) to f(x+Δx,y) and f(x,y+Δy) on a two-dimensional grid. John von Neumann, the polymath who helped design the first stored program computers, described algorithms for solving systems of differential equations on discrete grids.

Because of the complexity of computations involved in these simulations, high-performance supercomputers became very important in the sciences. Only those computers had sufficient power to numerically solve differential equations over complex grids. With supercomputers, computational scientists cracked the grand challenge problems articulated in the late 1980s.

For centuries, theory and experiment were the two modes of doing science. Supercomputers changed this, opening a new approach to doing science based on computational exploration and modeling. It was the most significant scientific paradigm shift since quantum mechanics. The computational science revolution ushered in a new wave of computational thinking.

As computing invaded science, something unexpected happened. Instead of computing becoming more like other sciences, other sciences became more like computing. Scientists who used computers found themselves thinking differently — computationally — and routinely designing new ways to advance science. By simulating air flows around a wing with the Navier-Stokes equation discretized to a grid surrounding an aircraft, aeronautical engineers eliminated the need for wind tunnels and many test flights. Astronomers simulated the collisions of galaxies. Macroeconomists simulated scenarios in national and global economies. Chemists simulated the deterioration of space probe heat shields on entering an atmosphere. Simulation allowed scientists to reach where theory and experiment could not. It became a new way of doing science. Scientists became computational explorers as well as experimenters and theoreticians.

Just as numerical analysis enabled better simulation, better simulation enabled another new scientific paradigm: information process interpretation of phenomena in the world. Much can be learned about a physical process by interpreting it as an information process and simulating the information process on a computer. For example, it has become a mainstay of modern biology, notably with sequencing and editing genes. [1] For the quantities modeled, the real process behaves as if it were an information process. The simulation and interpretive approaches are often combined, as when the information process provides a simulation for the physical process it models.

For centuries, theory and experiment were the two modes of doing science. Supercomputers changed this, opening a new approach to doing science based on computational exploration and modeling. It was the most significant scientific paradigm shift since quantum mechanics. The computational science revolution ushered in a new wave of computational thinking.

The term「computational science」and its associated term「computational thinking」came into use during the 1980s. In 1982, Kenneth Wilson received a Nobel Prize in physics for developing computational models that produced startling new discoveries about phase changes in materials. He designed computational methods to evaluate the equations of renormalization groups, which he used to observe how a material changes phase, such as the direction of the magnetic force in a ferrimagnet. He launched a campaign to win recognition and respect for computational science. He argued that all scientific disciplines had「grand challenge」problems that would yield to massive computation. [2] He and other visionaries used the term「computational science」for the emerging branches of science that made computation their primary method. Many of them saw computation as a new paradigm of science, complementing the traditional paradigms of theory and experiment. Convinced by the benefits computational thinking would bring to science, they launched a political movement to secure funding for computational science research, culminating in the High Performance Computing Act (HPCA) passed in 1991 by the US Congress, and bringing computational thinking in science into public view.

It is noteworthy that computational science and computational thinking in science emerged from within the scientific fields — they were not imported from computer science. In fact, computer scientists were slow to join the movement. Whereas numerical analysts often felt like outcasts from mathematics in the 1950s, and outcasts from computing in the 1970s, they were natural participants in computational science. Fortunately, this mood did not last; numerical analysts are important members of the computing field.

Computation has proved so productive for advancement of science and for engineering that virtually every field of science and engineering has developed a「computational」branch. In many fields the computational branch has grown to be critical for the field. For example, biology is seen as an information science. [3] Chemists design molecules and simulate them to find out how they would fare under real conditions. Pharmaceutical companies test molecules by simulation to learn if they would be effective against certain diseases. Computational methods are spreading into traditionally non-experimental fields, such as humanities and social sciences. This trend will continue. Computation will invade deeper into every field.

Because CT has advanced science — by providing better methods of numerical analysis, advanced simulations, and the information interpretation of physical processes — many people will decide to learn the skills required of computational designers and thinkers.

1 Baltimore (2001).

2 Wilson (1989).

3 Baltimore (2001).

2『 Baltimore 的那篇论文没下载到，意外发现份资料，作为本书的附件。已下载「附件01Interview-with David-Baltimore」。（2021-05-25）』

### 7.2 Computational Thinking in Science

Computational thinking in science has two aspects. First, mental skills facilitate the design of computational models for natural processes and for methods of evaluating models. The phrase「modeling and simulation」comes up frequently for this aspect of CT in science. Computing terminology gained favor among computational scientists because it distinguished the new computational methods of conducting science from the traditional methods of theory and experiment.

The second aspect of CT in science is a skill of interpreting the world in terms of information processes. Instead of asking computing's question — Can an information process be efficiently automated? — computational scientists ask: Can a simulated information process replicate a real process? What kind of information process creates an observed phenomenon? What computational mechanism is behind an observed process? For instance, many biologists study DNA and protein interactions in terms of information processes with the hope of designing future DNA that heals diseases and lengthens life. Physicists hope that by interpreting physics as information processes, they can learn about hard-to-detect particles from simulations of particles.

We see then that CT in computational science has a different orientation from CT in computer science. Much of computational science is concerned with using modeling and simulation to explore phenomena, test hypotheses, and make predictions in its respective fields. Much of computer science is concerned with designing algorithms to solve problems. Scientists and engineers who design simulations are often not formulating problem statements; they are investigating the behaviors of phenomena. Computing people are often not using simulations to understand how nature works; they are designing software to do jobs for users.

Computing people and scientists looking to collaborate ought to keep this distinction in mind. The collaboration will work better if the computer people develop an understanding of the science domain, and the scientists an understanding of the computing domain. For example, one of us (Peter) personally witnessed a disconnect between computational and computer scientists in the 1980s. A team of PhD computational fluid dynamics scientists invited PhD computer scientists to join them, only to discover that the computer scientists did not understand enough fluid dynamics to be useful. They were not able to think computational fluid dynamics with the same facility as the fluid dynamicists. The fluid dynamics scientists wound up treating the computer scientists like programmers rather than peers, much to the chagrin of the computer scientists.

### 7.3 Computational Models

The term「computational model」can also be a source of misunderstanding. To a scientist, computational models are sets of equations, often differential equations, that describe a physical process; the equations can be used computationally to generate numerical data about the process. Simulations are often the algorithms that do this. In contrast, a computational model in computing means an abstract machine that runs programs written in a programming language. The Turing machine is frequently cited in computing as the fundamental theoretical model of all computation, even though it is too primitive to be useful for most purposes.

Scientists routinely use abstract machines in the computing sense because every one of the familiar programming languages is associated with an abstract machine. For example, the FORTRAN language presents an abstract machine that is particularly good at evaluating mathematical expressions. The Java language presents an abstract machine that hosts a large number of autonomous「objects」that concurrently send and receive messages from each other. The C++ language also has objects but is closer to the actual machine and thus gives more efficient executable code.

The computational models in computational science are realized as abstract machines that bring a replica of a natural information process to life. The simulations are the executions of programs that implement those abstract machines.

### 7.4 Modeling and Simulation

Computational science has a rich trove of methods for modeling, simulating, and interpreting natural processes. We will consider five examples that illustrate the range and we will point out some key CT features of the models and the simulations.

#### 7.4.1 Mandelbrot Set

Many simulations walk through all the points on a grid, computing a function at each point, and then visualizing the result by assigning colors to the numbers on the grid points. The Mandelbrot set is a good example of a computation that reveals behaviors no one suspected by inspecting the equations. In the Mandelbrot visualization, for each point on a grid, the computer calculates a series of values based on a simple equation over complex numbers, and assigns colors to those points: if the calculated series converges (stays within some limits), color the point black, and if the series diverges, color it blue or yellow. Now repeat this for all points on the grid. [4]

When each point's color is assigned to a pixel, the Mandelbrot set appears on a graphics screen. No one suspected that such a simple computation would yield such a beautiful, mysterious object (see the figure below). One can select a small square anywhere on the graphic, zoom in on it, cover it with a grid and calculate all its grid-point colors — and see more copies of the Mandelbrot set appear at smaller scales. Each new zoom reveals more sets. It never ends. Mandelbrot called this self-replicating behavior at all scales「fractals.」

The fractal idea (self-similarity at different scales of measurement) was the key to Ken Wilson's renormalization group algorithms that yielded new discoveries in physics when simulated on a supercomputer, and it won him a Nobel Prize. The fractal idea is used in visualization systems to compute realistic graphic images, such as trees or horizons, rapidly.

4 For the more mathematically inclined, the Mandelbrot set is the points in the complex plane at which the series of values of a function converges. A complex number is represented as a+bi, where i=sqrt(-1) and i2 = -1. The equation of the series is z(n+1) = z2(n)+c where z(n) and c are complex numbers. Having chosen a value of c, compute a series of z(n)-values starting with z(0)=c. (You may need to go to an algebra refresher for algorithms to multiply complex numbers.) If the z(n) sequence converges (stays within a short radius of c for all n), color the chosen value of c black. If it diverges color c blue or yellow. Now repeat this for all c points on a grid.

#### 7.4.2 Telephone Engineers

When the first telephone exchanges were designed in the early 1900s, telephone engineers confronted a serious design issue. In a town of K customers, there are potentially K2 connections. Guaranteeing every customer could connect to any other customer at any time they desired would be hopelessly complex and expensive, especially since most of the time most of the customers are not talking at all. To control the complexity and cost, engineers decided to build switches that would handle up to N calls at once (N is substantially less than K). This of course brings a risk that a customer cannot get a dial tone if the exchange is already carrying N calls. The design question was how to choose N so that the probability of encountering the busy signal is small, for example 0.001. A random walk computational model yields an answer. The model has states n = 0, 1, 2, ... , N representing the number of calls in progress up to a maximum of N, here N = 10. Requests to initiate new calls are occurring randomly at rate λ. Individual callers hang up randomly at rate μ. Each new-call arrival increases the state by 1 and each hang-up decreases it by 1. The state diagram in the figure below represents the movement through the possible states. Telephone engineers define p(n) the fraction of time the system is in state n and can prove a difference equation p(n) = (λ/nμ)p(n–1). They calculate all the probabilities by guessing p(0), calculating each p(n) from its predecessor p(n-1), and then normalizing so that the sum of all p(n) is 1. Then they find the largest N so that p(N) is below the target threshold. For example, if they find p(N) = 0.001 when N = 10, they predict that a new caller has a chance 0.001 of not getting a dial tone when the exchange capacity is 10 calls.

A key idea here was modeling the physical process with a state space representing all the possible states of the system, connected by transitions representing the random rates of flow between pairs of states. By invoking a flow balance principle — total flow into a state equals total flow out — engineers got a set of equations relating the proportions of time p(s) each state s is occupied. They can then calculate the values of p(s) by applying the equations. This form of modeling is very common in queueing theory and system performance evaluation because all the measures of interest, such as throughput, response time, and overflow probabilities, are easy to calculate from the p(s).

#### 7.4.3 Doctor's Waiting Room

Engineers have also used state space models to build controllers of systems. In this example (see the figure below), a doctor wishes to build an electronic controller for her office, which consists of a four-person waiting room and a one-person treatment room. Patients enter the waiting room and sit down. As soon as the doctor is free, she calls the next patient into the treatment room. When done, the patient departs by a separate door. The doctor wants an indicator lamp to glow in the treatment room when patients are waiting, and another to glow in the waiting room when she is busy treating someone. The engineer designing the controller uses a computational model with states (n,t) where n = 0,1,2,3,4 is the number in the waiting room and t = 0,1 is the number in the treatment room. The controller implements the state diagram above. The indicator lamp in the treatment room glows whenever n > 0, and the lamp in the waiting room whenever t > 0. State transitions occur at three events: patient arrival (a), patient departure (d), and patient called by the doctor (c). Sensors located in the three office doors signal these events.

In this case the model is not used to evaluate probabilities of state occupancies, but to plan the states and transitions of an electronic circuit. It is of course possible to interpret the state diagram as in the previous example, where a, b, and c are flow rates between the states.

#### 7.4.4 Aircraft Simulation

Aeronautics engineers use simulations from computational fluid dynamics to model airflows around proposed aircraft. They have become so good at this that they can test new aircraft designs without wind tunnels and space shuttle designs without test flights. The first step is to build a 3-D mesh of the space surrounding the aircraft (see the figure on the following page). The spacing of the grid points is smaller near the fuselage where the changes in air movement are greatest. Then the differential equations of airflow are converted to difference equations on the mesh, and a supercomputer grinds out the profiles of the flow field and forces on each part of the aircraft over time. The numerical results are converted to shaded images (as shown in the figure on the next page) to visualize where the stresses on the aircraft are greatest.

This form of modeling is common in science. A physical process is modeled as differential equations that relate the values of the process at a point in space to the values of the process at close neighbors. The space in which the process is to be studied is modeled with a mesh. The difference equation is used to relate each mesh point value to its immediate neighbors. A graphical display converts the field of values on the grid to a colored picture. The whole mesh can be recomputed for the next time step, giving an animated visualization.

#### 7.4.5 Genetic Algorithms

Since the 1950s, various geneticists experimented with computer simulations of biological evolution, studying how various traits are passed on and how a population evolves to adapt to its circumstances. In 1975 John Holland adapted the idea of these simulations as a general method for finding near optimal solutions to complex problems in many domains. The idea, depicted in the flow diagram in the figure below, is to develop a population of candidate solutions to the problem, encoded as bit-strings. Each bit-string is evaluated by a fitness function and the most-fit members of the population are selected for reproduction by mutation and crossover. A bit-string is modified by mutation when one or several of its bits are randomly flipped. A pair of bit-strings are modified by crossover by selecting a random breakpoint and exchanging the two tails of the strings. This generates a new population. The process is iterated many times until there are no further improvements in the most-fit individuals or until the computational budget is exhausted. This process is surprisingly good at finding near-optimal solutions to optimization problems whose direct solutions would otherwise be intractable.

### 7.5 Grand Challenges and Wicked Problems

Computing has changed dramatically since the time when computational modeling grew up. In the 1980s, the hosting system for grand-challenge models was a supercomputer. Today the hosting system is the cloud — a massively distributed system of data and processing resources around the world. Commercial cloud services allow users to mobilize immense storage and processing power they need just when they need it. In addition, users are no longer constrained to deal with finite computations — those that start, compute, deliver their output, and stop. Instead devices now tap endless flows of data and processing power as needed and users count on the whole thing to keep operating indefinitely. With so much cheap, massive computing power, more people can be computational designers and tackle grand-challenge problems.

Yet there are important limits to what all this computing power can do. One limit is that most computational methods have a sharp focus — they are very good at the particular task for which they were designed, but not for seemingly similar tasks. That limit can often be overcome with a new design that closes a gap in the old design. Facial recognition is an example. A decade ago, methods of detecting and recognizing faces in images were not very good — people had to look at the images themselves. Today, deep learning (neural network) algorithms have been used to design very reliable automated face recognizers, overcoming the earlier gap. These recognizers are trained by showing them a large number of cases of labeled images. But recognizers are「fragile」in the sense that no one knows how the machine will do when presented with inputs outside the training sets. Overcoming fragility has motivated computational scientists to look at machines that learn without training sets. A recent example is a machine that learned to play the board game Go by competing against other machines, eventually becoming good enough to beat the world's highest-ranked Go player in a five-game match.

Self-learning machines have raised another concern: explainability. Designers and users want to know how the machine reached its conclusion. The idea that a machine can reach a conclusion makes sense when algorithms are seen as step-by-step procedures because the result can be explained by examining the steps followed. But when the algorithms are not step-by-step procedures, as with face recognizers and Go, that is not possible. All there is inside is an inscrutable, complex mass of connections. It is really the same problem with fellow humans — how do we explain why we do certain things? If asked directly, we may not know, and it certainly cannot be figured out by dissecting our brains. Other ways are needed to know when machines can be trusted and when not. Machine learning–related computational thinking is still in its infancy.

Another limit to what can be done with computing power concerns the many problems that cannot be solved at all with computation. We gave examples in chapter 3, which are either not computational at all, or so complex that they are forever beyond any computing power we can muster. But complexity is not the only barrier. Another is that some problems are inherently outside of science and technology and cannot be solved by scientific and technological methods. A favorite category is「wicked problems」 — especially issues in the interactions of social communities and technologies. They defy solution when factions have enough power to defeat a proposal they dislike but not enough power to form a consensus. Examples are many: Millions of「clean」cars collectively produce unhealthy smog in dense cities. New information technology fosters the growth of income inequality where designers reap much more bounty than users. STEM education struggles to learn how to prepare students to face great uncertainty about the future of work, societal safety nets, technology, and climate change. The solutions to these problems are not scientific, technical, or computational but will emerge from social cooperation among the groups that now offer competing and conflicting approaches. Although computational thinking can help by visualizing the large-scale effects of individual actions, only social consensus and social action can resolve wicked problems.

Computational thinking is a powerful force within science. It emphasizes the「computational way」of doing science and makes its practitioners into skilled computational designers (and thinkers) in their fields of science. It brings forth new information interpretations in a diversity of disciplines. Computational thinkers in sciences spend much of their time modeling physical processes, designing solution methods for those processes, running simulations, and visualizing the results.

### References and Further Reading

Aho, Al. (2011). Computation and computational thinking.

Akera, Atshushi. (2007). Calculating a Natural World: Scientists, Engineers, and Computers During the Rise of U.S. Cold War Research. MIT Press.

Baltimore, David. (2001). How biology became an information science. In The Invisible Future. Peter Denning, ed., pp. 43–46. McGraw-Hill.

Denning, Peter. (2017). Remaining trouble spots with computational thinking. Communications of the ACM 60 (6) (June): 33–39.

Wilson, Ken. (1989). Grand challenges to computational science. In Future Generation Computer Systems, pp. 33–35. Elsevier.

Wolfram, Stephen. (2002). A New Kind of Science. Wolfram Media.

## 0801. Teaching Computational Thinking for All

My basic idea is that programming is the most powerful medium of developing the sophisticated and rigorous thinking needed for mathematics, for grammar, for physics, for statistics, and all the「hard」subjects. Maybe I would even include philosophy and historical analysis. In short, I believe more than ever that programming should be a key part of the intellectual development of people growing up.

—— Seymour Papert (Papert, 2005)

Through the 1990s, CT education was mostly the purview of universities; very little CT education was available elsewhere. Pre-college K–12 schools had a scattering of computer courses; most focused on computer literacy and a handful on programming. A tipping point came after 2000 when many people saw how pervasive computing was in everyday work and home life. Educators and policymakers began to agree that understanding the mechanisms of digitalization is an important 21st-century skill.

The previously obscure notion of the algorithm entered everyday conversation as people cited value they had received from algorithms on their web searches, income tax preparation, online shopping, spreadsheets, neatly formatted documents, display-ready presentations, and computerized courses, and then later on smartphones, social networks, ride hailing, short-term renting, dating, finding friends, and much more. It seemed that understanding how it all works is central for coping in the modern world. It was finally time to bring computing to the K–12 level of education.

### 8.1 Computing Education

Getting computing education to K–12 schools was a struggle of a whole different order from getting computing education into universities. Numerous pilot projects to introduce computers in schools foundered because few teachers had any experience with computers and there was little political support in school boards. By the 1980s, a sea change began as more parents and teachers acquired home computers and came to see the growing importance of computing in their own work. The「computer literacy」courses introduced at that time were generally disappointing from the CT perspective because they focused on the use of tools like word processors and spreadsheets, not on programming.

Getting computing education to K-12 schools was a struggle of a whole different order from getting computing education into universities. Courses on computer literacy, later fluency, did not take hold. A computational thinking movement started in 2006 that energized educators and school boards to bring computer courses into all K-12 schools.

In the late 1990s, at the same time when the internet started to become a household commodity, a new education movement favoring「fluency with information technology」over literacy gained momentum and was supported by a popular textbook of the same name. It was an attractive notion that fluency with language and practices of computing would be a powerful asset in the emerging digitalized world. Bringing computing education to schools would enable children to become smart users of computing technology and would introduce them to the limitations and risks of algorithmic processes behind emerging functions such as online purchasing, Internet searching, news services, communication, and later social media. Despite its attraction, the fluency movement did not produce a widespread change in computing education in K–12 schools.

Then, in 2006, Jeannette Wing proposed that computational thinking is what everyone wants; not literacy or fluency. [1] She struck a resonant chord. In the next several years at the US National Science Foundation (NSF), she mobilized $48 million in resources and convinced many people to bring computer courses into all K–12 schools. Their major successes included getting education organizations to issue definitions of CT and associated curricula at different grade levels; training teachers in CS principles; starting a new family of CS-principles introductory courses at universities; and developing a new Advanced Placement curriculum and exam to interface high schools to these new introductory courses. CT went mainstream.

But as suggested above, this success was not easy. School boards in K–12 institutions had a long history of reluctance to add a computing curriculum in their schools. The CT movement brought a turn of mind to many school boards. Without that movement, we would not be talking about computational thinking in K–12 education at the scale we do it today. In this chapter, we will interpret the progression of computing education as a series of waves that started with the form of CT available in the 1950s (algorithmizing and mathematical problem solving), moved to Papert's Mindstorms, then to literacy and fluency, and culminated most recently in a modern version of CT designed for children in schools.

1 Wing (2006)

1-2『

这篇计算机思维的论文之前在多个场合看到过，自己 2019 年下载了的「2019016Computational thinking」并存入了 Zotero。YouTube 也有 Wing 的一个视频，结合起来一起看。（2021-05-25）

[Jeannette Wing: Computational Thinking - YouTube](https://www.youtube.com/watch?v=YVEUOHw3Qb8)

视频也下载了「202101Computational-Thinking」存入了/Users/Daglas/Movies/dalong.KnowledgeVideo/2021009youtube。

』

### 8.2 General-Purpose Thinking Tools?

Academic education for automatic computing machinery began in the late 1940s, when computing pioneers started educational programs on numerical methods for computing on large-scale machines. These early efforts went mainstream in the 1950s when the mass production of stored-program computers created a demand for a large number of people who could program them. After the early entry by private companies, university educators started organizing conferences to discuss computing education in the mid-1950s. By 1960, some 150 US universities offered some training in computing. There was, however, no standard view on what people needed to know about computing; individual programs depended on local idiosyncrasies such as specific jobs, needs of businesses, personal agendas of the faculty, research contracts, and other stakeholder interests. [2]

Already in those early days some computing educators described their visions of computing as a thinking tool for learning — a tool to deal with problems and questions in many fields besides computer science. Alan Perlis, who founded the computer science department at Carnegie Mellon University, was an outspoken advocate for this vision. He said that computing would be automating processes in many fields, and people in those fields would be「algorithmizing.」With this term, he referred to mental skills for reasoning about problems and developing computational solutions. George Forsythe cited Perlis in his 1958 address for the Mathematical Association of America:「Whereas we think we know something when we learn it, and are convinced we know it when we can teach it, the fact is that we don't really know it until we can code it for an automatic computer!」A decade later, Forsythe echoed the claim that computing provides general-purpose mental tools that would serve a person for a lifetime. Both Perlis and Forsythe firmly believed that everyone in every field will benefit from learning computing's procedural ways of doing things. They believed that computational models would be useful in all fields.

The visions of computing education grew ever more ambitious about what CT will be able to achieve. Marvin Minsky, a famous pioneer in artificial intelligence, argued, in his 1969 Turing Award speech, that computing would surpass mathematics in importance for early education. [3] Donald Knuth, a pioneer in understanding algorithms, argued that teaching a computer to do something forces precision and leads to deeper understanding than traditional means of thinking. [4] Another pioneer argued that the modern successor to「the classical person」would be「Turing's person.」[5] Two famous computing educators wrote that computing's procedural epistemology is creating a revolution in how people think and express themselves. [6] All this optimism about computing skills transferring to general problem solving turned out to be premature, as we discuss next.

2 Tedre, Simon, and Malmi (2018).

3 Minsky (1970)

4 Knuth (1974).

5 Bolter (1984)

6 Abelson and Sussman (1996)

### 8.3 CT Is Not Easily Transferable

The first wave of bringing CT to K–12 schools focused on programming. In the mid-1960s, some US high schools got DEC PDP-8 minicomputers and enterprising teachers organized courses around them. Numerous initiatives for using computers in schools over the 1960s and 1970s led to a few notable innovations. For example, the Little Man Computer for teaching machine languages and computers to students was introduced in 1965; one of the early programming languages for children, Logo, was introduced in 1967; and the famous concept for Dynabook, a children's portable computer, was born in 1968. Although minicomputers and some microcomputers were common in the late 1970s, educators, lacking financial resources and political will, were unable to transform the pilot courses into a large-scale rollout to schools.

The Logo programming language was a standout among the many initiatives of the 1960s. It was not a stand-alone, general programming language. It was a part of an integrated framework of pedagogical, technological, and educational ideas designed by Seymour Papert based in his deeply grounded understanding of how children learn. His 1980 book Mindstorms, written after a decade of research and experimentation with Logo, was a milestone for computing education and teaching computational thinking. Papert coined the phrase「computational thinking」for the practice of procedural thinking he taught to children. He argued that learning is most effective when learners「construct knowledge」 — they acquire practices from being immersed in a world of practices. They build their knowledge from practicing it rather than being told. The learning theory of constructionism became very popular in education. Papert continued to advocate self-directed learning, project learning, meaningful representations, facilitation-based education, and the use of technology to support learning in the classroom. His ideas influenced the Lego company to design and market the children's programmable bricks called Lego Mindstorms.

Teaching fundamental computational thinking skills, such as programming and computer modeling, is much harder than teaching spreadsheets, word processing, and other application tools of computing. Despite the popularity of constructionism, the central idea of Mindstorms — the shift from「learning to program」to「programming to learn」 — was hard to market among teachers. How could we achieve universal teaching of computational thinking without enough willing teachers? Could we rely on a smaller set of interested teachers to teach everybody?

The hope that a small number of teachers could teach CT to everybody was paired with the transfer hypothesis. The hypothesis is a belief that CT is a metacognitive skill learned from programming; students who learn CT in one domain became better problem-solvers in other domains, too. This belief bolstered the position that teaching computing should be an essential element of K–12 education. The most enthusiastic supporters of the hypothesis made claims such as「the concept of procedure is the secret educators have so long been seeking,」and「the pedagogic value of algorithmic approach aids in the understanding of concepts of all kinds.」They argued that teaching programming improves generic thinking skills such as logical thinking and generally「sharpens the mind.」The transfer hypothesis would indeed be important if it could be validated.

Critics of the transfer hypothesis referred to a research base in developmental cognitive science, arguing that there was no evidence of skill-transfer from programming to other subjects. Research with adults did not support transfer of cognitive skills between domains. Programming itself is a complex network of skills including mathematical abilities, conditional reasoning, analogical reasoning, procedural thinking, temporal reasoning, and memory capacity. It was not clear which parts of this complex transferred or not. After much detailed investigation, education researchers eventually concluded there is not enough evidence to accept the transfer hypothesis. It was not compelling as a justification to teach computing in K–12 schools.

Given that the transfer hypothesis does not work, schools needed more teachers who understood CT and could teach it in different contexts. Few teachers understood computers well enough to do this. Teaching a computer literacy course might be within their reach, but that baby step would not qualify them to teach CT. In the mid-2000s, when the US NSF began supporting the training of more computing teachers, the shortage of qualified teachers began to abate.

### 8.4 From Literacy to Fluency

The early advocates of algorithmic thinking would be appalled at many of the「computer literacy」courses in the 1980s and 1990s, which focused on how to use desktop applications, such as word processors, spreadsheets, and sketchpads. Motivated students and teachers found these courses boring. Literacy with desktop software was a far cry from their aspirations to participate in and shape the computer revolution. The professional societies, including ACM, IEEE-CS, and the British Computer Society, offered to help K–12 educators develop computer courses with more depth, but got little buy-in. In 1999, a US National Research Council commission upped the ante, reframing the question from literacy to fluency. Fluency offered capabilities, concepts, and skills essential for some levels of computational thinking. The NRC initiative was paired with a textbook Fluency with Information Technology that became quite popular among high school teachers.

Many schools brought computing into their curricula for pragmatic reasons as they responded to demands from parents and school boards. They sought access to simulations and other teaching software, access to basic programming, participation in the Internet revolution, learning 21st-century skills, preparation for employment in STEM fields, broadened social participation, and a new means for children to express individual creativity. [7] Educators and parents were disposed toward these goals because they believed that learning programming teaches important skills no other subject does, and because they did not want their children to be at a disadvantage in a world increasingly dependent on skills with information and communication technology.

In the 2000s, the entry of programming and computational design into schools was also easier because of advances in programming methodology and technology and changes in what entry-level programmers needed to know. New languages such as Python were much easier to use and hid well the underlying details of the operating system and hardware. Graphical, drag-and-drop user interfaces were very successful. Powerful tools automated significant parts of the programming process.

With all these advancements in programming languages, tools, and methods, programming was accessible to more students and teachers than ever before. There were more opportunities for becoming fluent in computing. But even so, in 2010 many schools had no computer courses or Advanced Placement curriculum in computing. Gaining fluency was not powerful enough to be a driving force.

7 Guzdial (2015)

### 8.5 Computational Thinking Revived

Jeannette Wing's 2006 essay on computational thinking launched a new wave in the movement to provide computing courses for all students in K–12 schools. The term computational thinking resonated and inspired action where literacy and fluency had not. Wing mobilized significant resources at the NSF to bring a large number of researchers into investigations of CT in education, to train a large number of teachers for teaching CT, to mobilize private organizations to produce K–12 curriculum recommendations for CT, and to develop a new Advanced Placement curriculum and exam on computing principles. Wing's essay became one of the most cited in computing education, a rallying point in a global movement to penetrate CT into K–12 education.

Major organizations including CSTA (Computer Science Teachers Association), the British CAS (Computing at School), Code.org, and the Australian ACARA2 (Australian Curriculum, Assessment, and Reporting Authority) developed and recommended curriculum frameworks for K–12 CT. These organizations promoted coding clubs, coding boot camps, and the international movement called「Hour of Code.」CT became a key word gathering hundreds of thousands of hits in news stories, blog postings, book chapters, articles, research projects, and essays on computing education.

The rapid infusion of so many enthusiastic newcomers who were unfamiliar with the long prior history of CT led to considerable confusion about definitions and learning objectives of CT. Some invented new CT frameworks for K–12 schools from scratch, imperfectly reinventing ideas that had been discussed for decades, omitting important ideas, confusing CT with the use of applications, and incorporating into their dogma some serious misconceptions about computing and algorithms. This resulted in a variety of tensions between different groups that used CT. [8] Here are the some of the most common points of contention, many of which can be explained by differences between CT for beginners and CT for professionals — basic CT in K–12 is surely different from advanced CT in higher education — as well as different contexts of application:

1 Whether CT is limited to thinking about the mechanics of constructing algorithms — or includes thinking about machines, computational science, software engineering, and design.

2 Whether CT is mostly about programming — or also encompasses systems, networks, and architectures; or whether it is not really about any of those.

3 Whether the definition, that CT is the formulation of algorithms to solve problems, is too narrow a view of CT's scope.

4 Whether algorithms are only those that fit the strict definition from the theory of computing — or whether algorithms could also be more loosely defined.

5 Whether algorithms necessarily include an abstract machine in the background.

6 Whether algorithms are primarily directions for controlling machines — or are primarily means of expressing procedures.

7 Whether using computational tools teaches CT.

8 Whether carrying out daily step-by-step procedures is a manifestation of CT.

9 Whether CT is learned from practicing programming — or from well-designed learning activities that use steps and rules.

10 Whether learning CT in the context of computing transfers to problem-solving skills in other fields.

11 Whether CT is domain dependent — or is a meta-skill valid in all domains.

12 Whether computational processes are found in nature — or whether they are limited to algorithms and machines.

13 Whether information processing by computers differs from information processing done by humans — and whether「information processing agents」can include things such as molecules, DNA, or quarks.

14 Whether students' learning should be assessed from their demonstrating skill at designing computations — or from their knowledge of certain key concepts.

15 Whether satisfaction of customers with the job that software does should be part of the assessment of software success.

16 Whether K–12 CT education has to stick with strict definitions of computing — or could for pragmatic and pedagogical reasons take some liberties.

We have expressed our stance on these questions at various points throughout this book. We see CT as an old, rich human practice that has been perfected in the modern age of the electronic computer. We see CT as a mental discipline for thinking about designing computations of all kinds, a skill at the advanced levels honed and improved through extensive practice and experience. We see many different levels and styles of CT from basic computing skills and insights to highly advanced, specialized ones. We see that there are many good ways for teaching entry level CT. We see that ultimately nearly all CT will boil down to machine-realizability. We see CT as mostly domain dependent — for example, how you think about computation in biology is different from physics, chemistry, or humanities. We see as wishful the notion that CT is an innate human ability exercised daily by using computational tools and performing routine everyday procedures. We see the attempt to define algorithms as a set of possibly ambiguous steps resolved by human computers as a misunderstanding of computing.

We would like to point out one other movement to bring computing into K–12 schools. Known as CS Unplugged, [9] it seeks to teach computing concepts and practices through games, magic tricks, and activities. It was founded in the late 1990s by Tim Bell, Michael Fellows, and Ian Whitten. It has gained a worldwide following and influenced the design of the ACM K–12 and code.org curriculum recommendations.

In summary, we see plenty of room for a broad, pluralistic approach to teaching computational thinking while remaining faithful to computing's well-honed disciplinary ways of thinking and practicing. Most of all, we hope that all teachers of computing bring their students a good sense of the richness and beauty of the many dimensions of computation.

8 Denning (2017).

9 See [Computer Science Field Guide](https://csfieldguide.org.nz/en/) and [CS Unplugged](https://csunplugged.org/zh-hans/).

### References and Further Reading

Abelson, Harold, and Gerald J. Sussman. (1996). Structure and Interpretation of Computer Programs. 2nd edition. MIT Press.

Bolter, J. David. (1984). Turing's Man: Western Culture in the Computer Age. University of North Carolina Press.

Denning, Peter. (2017). Remaining trouble spots with computational thinking. Communications of the ACM 60 (6) (June): 33–39.

Guzdial, Mark. (2015). Learner-Centered Design of Computing Education: Research on Computing for Everyone. Synthesis Lectures on Human-Centered Informatics. Morgan & Claypool.

Kestenbaum, David. (2005). The challenges of IDC: What have we learned from our past? Communications of the ACM 48 (1): 35–38. [A conversation with Seymour Papert, Marvin Minsky, Alan Kay]

Knuth, Donald E. (1974). Computer science and its relation to mathematics. American Mathematical Monthly 81 (April): 323–343.

Lockwood, James, and Aidan Mooney. (2017). Computational Thinking in Education: Where Does It Fit? A Systematic Literary Review. Technical report, National University of Ireland Maynooth.

Minsky, Marvin. (1970). Form and content in computer science. Journal of the ACM 17 (2): 197–215.

Tedre, Matti, Simon, and Lauri Malmi. (2018). Changing aims of computing education: a historical survey. Computer Science Education, June.

Wing, Jeanette M. (2006). Computational thinking. Communications of the ACM 49 (3): 33–35.

## 0901. Future Computation

Technology is part of our civilization. Sometimes people talk about conflict between humans and machines, and you can see that in a lot of science fiction. But the machines we're creating are not some invasion from Mars. We create these tools to expand our own reach.

—— Ray Kurzweil (2013)

Computational thinking is an ongoing quest to capture computing's ways of thinking and practicing. It is in never-ending flux, constantly renewing itself. Although many of the central CT precepts are very old, evolution of computing practice and technological state-of-the-art have affected how we see CT and what is central to CT. For instance, ever-evolving software development suites, new languages, and cloud services are shifting computational design tasks away from lower-level programming operations toward higher and higher levels of abstraction — thereby making computing jobs more design-intensive. Traditional programming is losing its role as the primary interface to computations; instead, domain-specific and intelligent tools are enabling more and more users to harness the potential of computers without programming them. CT expands well beyond programming and software development.

We will discuss some of the forces that are shaping our world and their likely effects on how we see computing and think about it. We will also discuss some important questions that CT cannot help us with. CT has its limits.

### 9.1 New Computational Models

One of the most obvious reasons why CT is changing is that computing technologies are changing. Throughout the long reign of Moore's law for silicon chips, the basic architecture of chips in computers and mobile devices has remained true to the von Neumann design from 1945 — separate memory and processing units, with a processor stepping through instructions stored in memory. The notion of「computational steps」in the modern definitions of CT comes from this design as well as from Alan Turing's definitions of computing.

But Moore's law cannot be sustained because of the physics of silicon and the nature of the chip-making process. [1] For this reason, researchers have been searching for new technologies that might supersede silicon-based von Neumann architectures and continue the exponential growth rate of information processing speed. Quantum computers, neural networks, reversible computers, DNA computers, memristor computers, and a few others are prime candidates. Each technology defines a new computational model that is the target for designers.

Consider, for instance, the D-wave, a commercial quantum computer. [2] It is designed to solve a set of equations, well known in physics as the Ising Model, which describe how certain systems settle into minimum energy states. Programming a D-wave computer means to encode the problem as a set of Ising equations and to input the coefficients into the machine; execution means to let the machine settle into a minimum energy state corresponding to the solution of the equations (a few microseconds); readout consists of reading the qubits (quantum bits) of the machine and interpreting them as the answer. There is no concept here of an「instruction set」or of programming as「designing a sequence of steps.」Most computer scientists, on being shown how to set up the D-wave machine for the first time, experience a mind tilt — the process is nothing like the programming process they have known all their professional lives. [3] Trained physicists have much less trouble understanding the machine. The current working definition of CT — formulating a problem so that it can be solved as a series of computational steps — fails to describe the computational thinking this machine involves.

DNA computing is another technology being investigated. In 1994 researchers performed an experiment in which they encoded possible paths in a map into strands of DNA, and then used the chemical methods of the day to evolve the initial mixture into one where the majority of strands represented the shortest tour of the map. [4] Considerable progress has been made with this technology. In 2016, another research team used the modern CRISPR gene editing technique to insert an image into the DNA of a bacterium. Computer scientists trained to think in terms of computational steps have more trouble than molecular biologists understanding how DNA computing works.

These examples illustrate CT has expanded beyond the idea of problem solving with computational steps. Our broader definition — designing computations that get computers to do jobs for us, as well as explaining and interpreting the world as a complex of information processes — is closer to the mark.

1 Denning and Lewis (2017).

2 McGeoch (2014).

3 See Walter Tichy's interview with Catherine McGeoch, Ubiquity July 2017, for a worked example of an Ising equation and its encoding into a form for the D-wave machine to solve, https://ubiquity.acm.org/article.cfm?id=3084688.

4 Adleman (1994).

### 9.2 Design

The ongoing increase in the importance of design is another reason CT is changing. Computational thinking is no longer confined to developing programs and algorithms to solve computational problems. Only a small portion of apps development, for example, is concerned with algorithms; the bulk of the work focuses on design of systems to deal with the concerns of a community. Design in this sense is an ongoing interaction between designers and users, watching their reactions to prototype software, evaluating what works and what does not work, and adapting the software accordingly. This is a much broader view of design than the「blueprint,」the「plan,」or the「setup of an experiment」views of early programming and software engineering communities. It is a skill set that combines sensibilities to moods and histories in communities with deep knowledge of existing technologies and other useful components. Design requires understanding humans in their communities as much as it requires understanding technology.

One effect of new designs in computing has been the automation of many cognitive tasks that as recently as a decade ago were considered out of reach of computing machinery. This kind of automation is displacing workers and has caused great concern that many current jobs could be automated, putting many people out of work. The flip side of the coin, however, is that the new technologies breed new problems that require new designs — creating new jobs for designers.

Computational design is now a skill that you can have in any field besides your primary disciplinary skills. You do not have to be a computer scientist to be a computational designer. Computational design captures the spirit of today's computing revolution better than computational thinking does. Past technology revolutions showed us that the new technologies ultimately created more jobs than they displaced. The current computing revolutions in machine learning and app development are producing new jobs for designers while rendering obsolete some existing jobs by automating them. To help smooth the transitions, governments should help more with training and education programs so that displaced workers can learn the design skills of the new jobs.

The new emphasis on design is rejuvenating the engineering aspect of computing, which is much more sensitive to design than the science side is. The engineering side brings to computational thinking concerns about reliability, fault tolerance, architecture, and systems that are sidelined in the theory- and algorithm-oriented definitions of CT. What is more, it brings to CT human concerns, such as recognizing the social worlds that are embracing computing, adopting a design into a community's practice, recognizing ethical issues brought forth by technology side effects, and providing means that human judgment and care influence the actions of machines.

### 9.3 Machine Learning

Neural networks, first articulated in the 1940s as possible models for electronic computers, have become the main technology behind artificial intelligence (AI) and data analytics today. The neural network was a mathematical model in which a neuron「fired」when the combination of signals from other neurons exceeded its built-in threshold; the「fired」neuron entered an excited state that was then communicated to other neurons. The motivation for imitating the brain was that automatic computers might do human tasks better when built of similar components. Of course, a circuit of these neuron models is nothing like a real brain. The logic circuits of the first computers ran much faster than neural circuits. Today the situation is different: we now know how to use cheap graphics cards to speed up neural network calculations. IBM and Intel now market chips that are even faster; they recognize that a new way of thinking is needed to put their chips to best use and they offer courses in the operation and use of their chips.

Early neural networks were small and easily confused when presented with new inputs not in their training sets. Modern neural networks consist of many layers, have much higher capacity, and are less easily confused. Thanks to graphics processing chips, trained neural networks of many layers respond to inputs almost instantaneously. Since layers, nodes, and connection weights do not change after the network is trained, performance does not depend on the data input. As neural network implementations typically do not have loops, they run in a constant time with constant memory spaces. That means that neural networks can be used in real-time applications with deadlines much more reliably than traditional programs.

A big attraction of neural networks is that they are「trained」rather than「programmed.」For example, we do not have very reliable algorithms for face recognition, but neural networks can be trained to recognize given faces quite reliably. These networks are often called「self-programmed」because no programmer specifies the internal weights — although the weight-adjusting algorithm used in training can be viewed as an automatic programmer. For many problems, it is much easier to find or create suitable training data than to write a rule-based program. As mentioned in previous chapters, a big issue with neural networks is that there is no way to「explain」how the network generated an output, as is possible with traditional programs. Knowing the reasons behind a conclusion is important in many application areas such as medical diagnosis; neural networks confound that. CT has already had to adjust to include the tools used to build and train neural networks. Bigger challenges lie ahead with assessing the reliability and security of neural networks.

Another big attraction is that neural networks can be trained by having them interact with other neural networks instead of given data sets. The network for AlphaGo, which beat the world champion Go player in 2017, was trained by having it play against another AlphaGo network; it learned Go from play rather than from training on a large set of recorded Go games. This way of training networks by letting them learn from each other has the potential to be game changing.

### 9.4 Human-Computer Teaming

Garry Kasparov, the world champion chess grandmaster, was defeated in 1997 by IBM's Deep Blue computer. That game marks a milestone in chess because it was the first time a computer program beat a grandmaster. Kasparov had played several previous matches against lesser computers, winning them all.

Kasparov did not declare the game of chess dead. Instead, he invented a new kind of chess, Advanced Chess. In Advanced Chess, the two players of a match are each assisted by a computer. Before committing to the next move, the human player consults the computer program to gain insights into the possible effects of moves. The computer-assisted chess players played better chess than when they played without computers, but also better chess than computers alone played.

The notion that a human-computer team can always perform better than a very good machine is controversial. There are reports of recent Advanced Chess tournaments in which teams did poorly compared to matches between computers without humans. In medicine, diagnosticians teamed with computers do not always perform as well as the very best diagnostic computer.

Still, human-computer teaming has attracted a lot of attention in artificial intelligence research because it is capable of performing computations that no human or computer could do alone. An early example of this was the labeling of digital images with searchable keywords. Doing it by hand was far too slow to be useful for labeling images online. In 2006, Luis von Ahn of Carnegie Mellon University invented an online game where thousands of pairs of humans labeled the images presented to them; if their keywords matched, their labeled image went into the searchable database. The「labeling function」implemented by these human-computer teams had been thought to be non-computable. The human computer teams were more powerful than computers.

Human-computer teaming requires a different kind of computational thinking than traditional computer programming. We watch with great interest how the controversy over whether teams can outperform machines plays out in the future.

### 9.5 Technology Jumping

In 2006 Ray Kurzweil, a futurist and inventor of computing technologies, prophesied that by 2030 we will be able to build a computer the size of the brain, with the same number of neurons and connections as the brain. [5] Such a computer would, he envisioned, develop its own consciousness and superintelligence. How such computers would treat humanity is an unanswerable question. The best that can be said is that the new machines would have such different concerns from ours that we cannot fathom how they would treat us. That moment of their creation is called the singularity because of the utter unpredictability of what lies after an artificial intelligence develops consciousness.

Kurzweil arrived at his conclusion by extrapolating Moore's law, the prediction of Gordon Moore in 1965 that silicon chips would double in capacity about every two years for the same price. The computer chip industry has followed the law by doubling power every two years for over half a century. In many ways Moore's law is a triumph of computational thinking because chip engineers needed to think hard to find ever better ways to build computing circuits.

Kurzweil exploited the phenomenon of technology jumping in his analysis. Since the beginning of the information age in the early 1900s, he argued, the same doubling effect was observed in the technologies of the day, for example punched card machines or vacuum tube machines. When one technology could no longer produce the two-year doubling, another took over. Moore's law for silicon is actually the fifth wave of technologies displaying two-year doubling. Kurzweil has confidently predicted that more technology jumps will occur and sustain the trend, allowing him to predict the processing power available by 2030 and beyond, and arrive at the singularity.

Technology jumping is a standard practice of the computing industry. The adoption of a particular technology versus time almost always follows an S-curve with exponential growth until an inflection point, after which the growth slows down as the market saturates. Business leaders are sensitive to inflection points because a competitor with a better, exponentially growing technology can upend their businesses when their own growth slows. They try to anticipate inflection points by developing new technology in their research labs and jumping to it when their business reaches the inflection point. They can then ride the new technology wave during its exponential growth stage.

Although the singularity is a product of computing and computational thinking, it cannot be addressed with computational thinking, and we cannot improve our understanding of it through computational thinking.

5 Kurzweil (2006).

### 9.6 The Whole World Is a Computer Hypothesis

Some scientists have argued that information is the basis of all physics. Every particle and every interaction is the product of information flows and exchanges at a more fundamental level than the smallest particles known. In 2002, Stephen Wolfram, a physicist and inventor of the Mathematica program — a triumph of computational thinking in itself — published a big book in support of this claim. [6] In 2003, Nick Bostrom, a philosopher, argued for a possibility that we are characters in a simulation run by a much more intelligent species studying their ancestors. While other physicists see some merit in the claim that all particles and interactions can be explained with quantum mechanical probability waves, which are forms of information, they regard the idea that our world is a digital simulation as far-fetched. [7]

The whole-world-is-computer hypothesis appeals to those who believe that computational thinking and computing are pervasive without limits.

6 Wolfram (2002).

7 In April 2016, Scientific American magazine reported on a symposium of physicists and philosophers discussing the whole-world-is-computer hypothesis, giving the impression that they take more delight in entertaining themselves with the hypothesis than in the hypothesis itself. See [Are We Living in a Computer Simulation? - Scientific American](https://www.scientificamerican.com/article/are-we-living-in-a-computer-simulation/).

### 9.7 Ideological Fights over What Should Be Taught

There is a never-ending debate on what should be taught in a computing curriculum. There are two hot spots in the debate. One concerns the selection of programming language and programming framework that students should be introduced to. Should it be a language that is easy to learn and has the least-confusing structure and syntax, such as Python? Or should it be a language that is used by their future employers in industry, such as Java or Javascript? What are the benefits of starting with a framework that treats programs as sources of instructions for a machine (known as an「imperative」framework) compared to one treating programs as compositions of functions (known as a「functional」framework)? These debates have been a staple of computing faculty meetings since the 1960s and are not likely to abate in the years ahead.

The other hot spot is the tension between the ideals of science-mathematics and of engineering-design. The science-mathematics ideal teaches abstractions of things in the world and leaves it to the student to apply the abstraction to the case at hand. The engineering-design ideal focuses on all the details that a builder has to get right for the resulting program to be safe and reliable. The science-math view has had the upper hand for many years, but with the rise of design, the engineering view is gaining new currency. In reality, both traditions are important for the success of computing: the science and engineering sides need each other.

### 9.8 Reflection on the Emerging World

We write this book at the 50th anniversary of the first recommendations for developing a computing curriculum made by the ACM (Association for Computing Machinery), a society of computing professionals that we both belong to. That curriculum and its subsequent specifications were shaped by many factors noted in the previous chapters:

1 Strong emphasis on technology development from the beginning.

2 Wide resistance to forming computing departments from other academic departments that did not accept computing as a legitimate field.

3 Developing a computing community network at the dawn of the internet era.

4 Being torn by intense debates over the roles of science, math, and engineering in computing, manifested as struggles over how to teach software engineering and information technology, and how much to trust formal methods for software development.

5 Coming to grips with the emergence of computational science and now the penetration of computing into nearly every field of human endeavor.

6 The deaths and resurrections of artificial intelligence and its claims about automation and the future of humanity.

This battle-hardened inheritance does not help us with many of the pressing issues of the world emerging around us. The worldwide connectivity we helped bring about through the Internet has brought many benefits from shrinking the world and globalizing trade. But it has also spawned conflicts between non-state organizations and traditional nations, trade wars, protectionism, terrorism, widespread detachment, fake news, misinformation and disinformation, political polarization, and considerable unease and uncertainty about how to move in the world. Access to troves of information via the Internet has begun to show us that knowledge does not confer wisdom, and we long for wise leaders who have yet to appear. The promise of respectful information society enabled by the Internet has turned into polarized society enabled by social media. The world we encounter in our daily lives is full of surprises, unexpected events, and contingencies that not even our best learning machines and data analytics can help us with. We are now finding that many resources including sea and air access are contested among nations; we lack means to resolve the resulting disputes and we worry that the resulting conflicts could trigger wars or economic collapses. We see that collective human action affects the global environment but have yet to find ways to protect our environment we will bequeath to our children and grandchildren.

This leaves us with a big question: how shall we shape computing education so that our graduates can develop the design sensibilities, wisdom, and caring they will need to navigate in this world, of which they will be citizens? Our current curriculum, chock full of courses covering the 2013 body of knowledge, is not up to this task.

A place to start would be to open up space in our crowded curriculum to have conversations on big questions about the consequences of computing throughout the world. These conversations need to be interdisciplinary and intergenerational. Their purpose would not be to solve problems but think together — to edify — to develop mutual understanding, appreciation, and respect around these issues. Some examples of big questions ripe for edifying conversations attending computational thinking are:

Our battle-hardened notions of computational thinking do not help with many of the pressing issues of the world emerging around us. Access to troves of information via the Internet has begun to show us that knowledge does not confer wisdom.

1 What cannot be automated? What should be automated? How far can automation take us? Who gets to decide what is automated and what is not?

2 How can AI generate more jobs through automation than it displaces?

3 How can we help people whose jobs are displaced by software and hardware we have designed?

4 How do we cultivate good designers?

5 How can we increase trust on decisions by neural networks when given inputs outside their training sets?

6 How will we discourage the development of an automated surveillance society?

7 What technological solutions can be found to the cybersecurity problem?

8 How do we make our world work when computers have been embedded into almost all devices connected to the global network?

9 How does digital technology affect global politics, nationalism, balance of trade, climate change, and other issues of globalization?

10 In what ways will blockchains and cryptocurrencies affect our problems with trust in central authorities? Are they too expensive to maintain?

11 How do we protect societies that are deeply dependent on computing from an attack on a critical component of infrastructure, like the electric grid or the Internet?

12 How do we prepare people to appreciate the difference between wisdom and abundance of information?

13 What are the social implications of brain-computer interfaces and neural implants into our brains and bodies?

14 What economic avalanches are possible because multiple, interdependent technologies are dropping in cost exponentially?

We do not believe any of us has answers to any of these questions. But we need to be having the conversations about them. In so doing we need to embrace the mathematicians, scientists, sociologists, philosophers, anthropologists, lawyers, engineers, and everyone else in our field. It is time for us to think together about the design and impacts of our technology and so shape our future with wisdom and understanding. It is time to give up the old tensions that we inherited from times long past, and work together as brothers and sisters, mothers and fathers, old and young on these big questions.

### References and Further Reading

Adleman, Leonard M. (1994). Molecular computation of solutions to combinatorial problems. Science 266 (5187): 1021–1024.

Brynjolfsson, E., and McAfee, A. (2014). The Second Machine Age: Work, Progress, and Prosperity in a Time of Brilliant Technologies. W. W. Norton & Company.

Denning, Peter. J., and Ted G. Lewis. (2017). Exponential laws of computing growth. Communications of ACM 60 (1) (January): 54–65.

Friedman, Thomas. (2016). Thank You for Being Late. Farrar, Straus and Giroux.

Kelly, Kevin. (2017). The Inevitable: Understanding the 12 Technological Forces That Will Shape Our Future. Penguin Books.

Kurzweil, Ray. (2006). The Singularity Is Near. Penguin Books.

McGeoch, Catherine. (2014). Adiabatic Quantum Computation and Quantum Annealing. Synthesis Series on Quantum Computing. Morgan & Claypool.

Wolfram, Stephen. (2002). A New Kind of Science. Wolfram Media.