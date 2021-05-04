## 记忆时间

## 卡片

### 0101. 主题卡 —— 计算机思维和人的思维的区别

Computational thinking illuminates a fundamental difference in the ways that humans and machines process information. Machines can process information at billions or trillions of calculations per second, whereas humans do well at one calculation per second. Machines process with no understanding of the data they are processing, whereas humans do and can correct errors on the fly. Machines can transform a mistake in an algorithm into a costly disaster before any human has a chance to react. Thinkers in the philosophy of mind, neuropsychology, cognitive science, and artificial intelligence have studied these differences and shown us how fundamentally dissimilar they are. Although some human tasks like searching and sorting can be eased by applying algorithms to them, most computational thinking in the big picture is concerned with machine computation.

2『上面计算机思维和人的思维，做一张主题卡片。』—— 已完成

### 0102. 主题卡 —— 计算机不能做的事

信息源自「2020136Computational-Thinking0101.md」

In our enthusiasm for computational thinking, we need to be careful to avoid wishful thinking. Perhaps the first and most common wish is that we can get computers to do any job we can conceive of. This wish cannot be realized because there are many jobs that are impossible for computers. For example, there is no algorithm that will inspect another algorithm and tell us whether it terminates or loops forever. Every programming student longs for such an algorithm to help with debugging. It was logically impossible in 1936 when Alan Turing proved it so, and it is still impossible today.

1-2『这里的信息阐述了「计算机」不能做的事，列举了 4 中不能「计算」的场景，等同于吴军之前一直强调的「计算机边界」问题。做一张主题卡片。（2021-05-04）』—— 已完成

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

### 0201. 术语卡 —— Computational thinking 

信息源自「2020136Computational-Thinking0101.md」

Computational thinking is the mental skills and practices for:

1 designing computations that get computers to do jobs for us, and

2 explaining and interpreting the world as a complex of information processes.

1-2『这里作者对 CT 下了定义，做一张术语卡片。（2021-05-04）』—— 已完成

The design aspect reflects the engineering tradition of computing in which people build methods and machines to help other people. The explanation aspect reflects the science tradition of computing in which people seek to understand how computation works and how it shows up in the world. Design features immersion in the community being helped, explanation features being a dispassionate external observer. In principle, it is possible to design computations without explaining them, or explain computations without designing them. In practice, these two aspects go hand in hand.

Computations are complex series of numerical calculations and symbol manipulations. Examples of numerical calculations are the basic arithmetic operations (add, subtract, multiply, divide) and the basic trigonometric functions (sine, cosine, and tangent). Examples of symbolic manipulations are logical comparison of numbers or symbols, decisions of what instructions to do next, or substitutions of one string of letters and numbers for another. Amazing computations can be carried out when trillions of such simple operations are arranged in the proper order — for example, forecasting tomorrow's weather, deciding where to drill for oil, designing the wings of an aircraft with enough lift to fly, finding which physical places are most likely to be visited by a person, calling for a taxi, or figuring out which two people would make a great couple.

There is clearly a special thinking skill required to successfully design programs and machines capable of enormous computations and to understand natural information processes through computation. This skill — computational thinking, or CT — is not a set of concepts for programming. Instead, CT comprises ways of thinking and practicing that are sharpened and honed through practice. CT is a very rich skill set: at the end of this chapter we outline the six dimensions of computational thinking that you will encounter in this book: machines, methods, computing education, software engineering, design, and computational science.

### 0202. 术语卡 ——

### 0203. 术语卡 ——

### 0301. 人名卡 ——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

### 0401. 金句卡 ——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 行动卡 ——

行动卡是能够指导自己的行动的卡。

### 0601. 数据信息卡 ——

### 0701. 任意卡 ——

最后还有一张任意卡，记录个人阅读感想。

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

Most of what software does for us is made possible by the incomprehensible speed gap between computers and humans—billions to trillions times faster. Even though humans can execute computational steps, they could not carry out most of these computations in their lifetimes. The machines can literally do the humanly impossible. While it is true that humans can personally perform algorithms for some information processing tasks, the revolutions of the computer age are not about where people can perform algorithms in their own lives, but about what computers are able to do for them.

### Lesson 4: Advanced CT is domain dependent

For advanced tasks, you need to understand the domain in which you want to figure out how to get a computer to do a job for you. For example, an expert programmer who knows nothing about quantum physics will have little to offer to a team of physicists working on a quantum computer. Similarly, working with the nature's complex algorithms in biology requires considerable understanding of biological processes. Algorithmic models in chemistry require deep familiarity with the corresponding chemical processes. Building an information system for a hospital requires extensive understanding of the institutional, informational, and workflow processes in the hospital context. Much of advanced computational thinking is context-specific and tightly tied to the application domain.

### Lesson 5: CT has changed the tools, methods, and epistemology of science

Computational thinking has fostered a revolution in science. Scientists in all fields have found that CT is a new method of doing science, different from the classic methods of theory and experiment. They came to this discovery in the 1980s when they began using supercomputers to crack scientific「grand challenges.」This was a profound paradigm shift that enabled many new scientific discoveries. Each field developed its own strain of CT that was not imported from computer science. Computer science CT has been enriched by its collaboration with the computational sciences.

### Lesson 6: The public face of CT is that of elementary CT

CT is billed for K–12 curriculum purposes as a set of concepts and rules for programming. But many professionals see CT as a design skill, and many natural scientists see it as an advanced method of scientific interpretation. Like all skills, you can be a beginner, advanced beginner, competent, proficient, expert, or master. Many debates about what CT「really」is seem to collapse different skill levels of CT within the same debate. For example, K–12 teachers argue for curricula that are almost solely aimed at beginners and that contain a small, teachable set of CT insights, practices, and skills. Other advocates argue for CT as advanced, professional skills that require many years of practice and experience. Failing to make the distinction leads to conflicts—for example, the hype about how learning programming opens career paths is silent about what professional computational designers do. Education efforts are important on all levels from K–12 through university and beyond.

### Lesson 7: Beginner and professional CT together comprise a rich tapestry of computational thought

Educators in K–12 schools have developed an impressive「CT for beginners」—insights and methods for teaching computing to newcomers. Professional software systems designers and scientists have developed an impressive「CT for professionals」—advanced methods for designing and building complex software that works reliably and safely, and for conducting scientific investigations. The synergy between these two aspects of computational thinking has propelled the computer revolution.

### Lesson 8: Change is an inseparable part of CT

There has never been a consensus about what computational thinking「really」is. There may never be a full consensus. During every decade in the modern history of computing there would be different answers to questions about the essence of computational thinking. Advances in computing keep computational thinking in constant change. We should embrace the lack of a fixed definition as a sign of the vitality of the field rather than our own failure to understand an eternal truth.