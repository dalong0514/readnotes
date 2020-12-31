# 0101. What Is Computational Thinking?

An algorithm is a set of rules for getting a specific output from a specific input. Each step must be so precisely defined that it can be translated into computer language and executed by machine.

—Donald Knuth (1977)

What is a computer? Most people will answer it is an electronic black box that does amazing things by collecting, storing, retrieving, and transforming data. Almost all our devices and gadgets are computers: phones, tablets, desktops, web pages, watches, navigators, thermometers, medical devices, clocks, televisions, DVD players, WiFi networks. Our services are software—bookstores, retail stores, banks, transportation, Uber, hotel reservations, Airbnb, filmmaking, entertainment, Dropbox, online courses, Google searches—and almost all run by unseen computers across an unseen worldwide network called「the cloud.」Computers have brought enormous benefits—new jobs, access to information, economic development, national defense, improvements in health, and much more. They have brought, as well, worrying concerns—job losses, globalization, privacy, surveillance, and more. It looks like everything that can be digitized is being digitized and computers are everywhere storing and transforming that information. A computer revolution is truly upon us.

How shall we think about all this? What do we need to understand about computers? What must we do to put a computer to work for us? How do computers shape the way we see the world? What new do we see? What is the role of programming? What are computers not good for?

The Power and Value of Computation

Computational thinking (here abbreviated CT) offers some answers to these questions. Much of CT is specifically oriented on figuring out how to get a computer to do a job for us—how to control a complex electronic device to do a job reliably without causing damage or harm. Algorithms are the procedures that specify how the computer should do a job. Although humans can carry out algorithms, they cannot do so nearly as fast as a machine; modern computers can do a trillion steps in the time it takes a human to do one step. The magic is nothing more than a machine executing large numbers of very simple computations very fast. Programs are the bridge: algorithms encoded in special-purpose languages that translate to machine instructions that control a computer.

But CT reaches further than automation. Information and computational processes have become a way of understanding natural and social phenomena. Much of CT today is oriented toward learning how the world works. A growing number of biologists, physicists, chemists, and other scientists are looking at their subject matter through a computational lens; professionals in the arts, humanities, and social sciences are joining in. Computer simulation enables previously impossible virtual experiments. The「information interpretation」of the world offers conceptual and empirical tools that no other approach does.

CT also advises us about jobs that computers cannot do in any reasonable amount of time. Or at all—some jobs are impossible for computers. Many social, political, and economic problems are beyond the pale of computers. By understanding the limits of computing, we can avoid the trap of looking to computing technology to solve such problems.

Obviously, designing a program or a machine to do so much in such a short time is a daunting design task that demands its own way of thinking if we are to have any confidence that the machine does the job without error. Indeed, understanding users, and designing systems specifically for them, turns out to be one of the great challenges of modern computing. Design is one of the central concerns of CT.

Defining Computational Thinking

Computational thinking has become a buzzword with a multitude of definitions. We have distilled the spirit of the multitude into this definition used throughout this book:

Computational thinking is the mental skills and practices for

•	designing computations that get computers to do jobs for us, and

•	explaining and interpreting the world as a complex of information processes.

The design aspect reflects the engineering tradition of computing in which people build methods and machines to help other people. The explanation aspect reflects the science tradition of computing in which people seek to understand how computation works and how it shows up in the world. Design features immersion in the community being helped, explanation features being a dispassionate external observer. In principle, it is possible to design computations without explaining them, or explain computations without designing them. In practice, these two aspects go hand in hand.

Computations are complex series of numerical calculations and symbol manipulations. Examples of numerical calculations are the basic arithmetic operations (add, subtract, multiply, divide) and the basic trigonometric functions (sine, cosine, and tangent). Examples of symbolic manipulations are logical comparison of numbers or symbols, decisions of what instructions to do next, or substitutions of one string of letters and numbers for another. Amazing computations can be carried out when trillions of such simple operations are arranged in the proper order—for example, forecasting tomorrow’s weather, deciding where to drill for oil, designing the wings of an aircraft with enough lift to fly, finding which physical places are most likely to be visited by a person, calling for a taxi, or figuring out which two people would make a great couple.

Computers are agents that carry out the operations of a computation. They follow programs of instructions for doing arithmetic and logic operations. Computers can be humans or machines. Humans can follow programs, but are nowhere near as fast or as error-free as machines. Machines can perform computational feats well beyond human capabilities.

We use the word「job」to refer to any task that someone considers valuable. Today many people look to computers (actually, computations performed by computers) to get jobs done. They seek automation of jobs that could not be done without the aid of a machine. Computers are now getting good enough at some routine jobs so that loss of employment to automation has become an important social concern.

We do not equate「doing a job」with automation. Well-defined, routine jobs can be automated, but ill-defined jobs such as「meeting a concern」cannot. CT can help with jobs that cannot be automated. In the design chapter we will discuss the kind of CT that does this.

There is clearly a special thinking skill required to successfully design programs and machines capable of enormous computations and to understand natural information processes through computation. This skill—computational thinking, or CT—is not a set of concepts for programming. Instead, CT comprises ways of thinking and practicing that are sharpened and honed through practice. CT is a very rich skill set: at the end of this chapter we outline the six dimensions of computational thinking that you will encounter in this book: machines, methods, computing education, software engineering, design, and computational science.

Wishful Thinking

In our enthusiasm for computational thinking, we need to be careful to avoid wishful thinking. Perhaps the first and most common wish is that we can get computers to do any job we can conceive of. This wish cannot be realized because there are many jobs that are impossible for computers. For example, there is no algorithm that will inspect another algorithm and tell us whether it terminates or loops forever. Every programming student longs for such an algorithm to help with debugging. It was logically impossible in 1936 when Alan Turing proved it so, and it is still impossible today.

Even if we stick to logically possible jobs, there are many that cannot be done in a reasonable time—they are intractable. One famous example is the traveling salesman problem, which is to find the shortest tour on a map of a country that visits each city just once. An algorithm to compute this would be of great value in the package delivery industry. The simplest way to find the shortest tour is to enumerate all possible tours and select the shortest. For a small set of 100 cities, this would take 10130 years on the world’s fastest supercomputer. For comparison the age of the universe is on the order of 1010 years. Even the「simplest way」can be impossible! Algorithms analysts have identified thousands of common problems that are intractable in this way.

The picture gets even more confusing because in most cases there are fast algorithms to find an approximate answer. They are called heuristics. Take, for example, the problem of finding the shortest tour connecting all 24,978 cities in Sweden. The enumeration algorithm for the traveling salesman problem would take on the order of 10100,000 years! But in 2004 a team at the University of Waterloo using heuristics for optimization found a shortest tour and proved it to be correct. Their solution used 85 years of processing time spread over a cluster of machines that took several months to complete the job.

Computational thinkers need to develop enough experience and skill to know when jobs are impossible or intractable, and look for good heuristics to solve them.

A second example of wishful thinking is to believe that learning how to program in a computer science course or a coding-intensive workshop will enable you to solve problems in any field that uses computation. No, you will need to learn something about the other field too. For example, even if you have studied search algorithms in a programming course, you are not likely to be able to be useful to a genomics project until you have learned genome biology and the significance of biological data.

A third example of wishful thinking is to believe that computers are not essential to CT—that we can think about how to solve problems with algorithms and not be concerned with the computers that run the algorithms. But this is not so. When a computer does not have sufficient memory to hold all your data, you will seek ways to divide your problem into subsets that will fit. When a single processor does not have sufficient processing power, you will seek a computer with multiple parallel processors and algorithms that divide the computation among them. When the computer is too slow, you will look inside to find a bottlenecked component and either upgrade it or find a new algorithm that does not use that component. Even if your computer has sufficient memory, adequate processing power, and no bottlenecks, other aspects can limit your problem-solving progress, notably the speed of the internal clock, which paces the machine to perform computational steps in an orderly and predictable way. But some new machines, notably quantum computers and neural nets, have no clocks: How shall we think about programming them?

A fourth example of wishful thinking is to believe the computer is smart. If you are imprecise in translating human steps into program steps, your computation will contain errors that could cause disasters. Computers are incredibly dumb. They perform mindless, mechanical steps extremely fast but they have no understanding of what the steps mean. The only errors they can correct are the ones you anticipate and provide with corrective algorithms. You are the source of the intelligence; the computer amplifies your intelligence but has none of its own.

We advise you to approach CT with humility. It is a learned skill. Our brains do not naturally think computationally. Keep your perspective on the capabilities of computers and algorithms to do jobs, on the need to learn something about the application domain you want to design for, on the dependency of computation on computers, and the abject lack of intelligence in the machine.

Emergence of CT over Millennia

It might seem that CT is a product of the electronic computer age that began in the 1940s. Well, not really. Before the modern computer age there was a profession of mathematically trained experts who performed complex calculations as teams. They were called「computers.」They were by no means the first: the term「computer,」meaning「one who computes,」dates back to the early 1600s. The first electronic computing machines were called automatic computers to distinguish them from the human variety. Human computers and, even more so, the leaders of human computing teams, obviously engaged in computational thinking. So, many aspects of CT existed before electronic computers. Well before.

Primitive forms of CT as methods of calculation were recorded from around 1800 to 1600 BCE among the Babylonians, who wrote down general procedures for solving mathematical problems. Their rule-following procedures have features that we, from today’s perspective, would label as forms of CT. Similarly, the Egyptian engineers who built the pyramids beginning around 2700 BCE obviously knew a lot about geometry and were able to calculate the dimensions and angles of stones for each part of the pyramid and of the leverage of ropes, pulleys, and rollers to move the stones into position. Computing is an ancient human practice.

Over the ages since ancient times, mathematicians sought to spell out procedures for ever more advanced calculations, moving beyond calculating merchant transactions and the geometry of structures, to trigonometry, astronomic predictions, celestial navigation, solving algebraic equations, and eventually computing with the calculus of Newton and Leibniz. By formalizing computing procedures, mathematicians made their expertise available to non-experts who simply had to follow directions of carrying out simple arithmetic operations in the proper order. A special class of those directions is today called an algorithm—a key concept in modern computing. The term「algorithm」comes to us from the Persian mathematician Muhammad ibn Mūsā al-Khwārizmī who, around 800 CE, discussed how to formulate mathematical procedures and gave examples such as finding the greatest common divisor of a set of numbers.

We humans have a penchant for automating routine procedures. So it has been for computational procedures: inventors sought machines that would automate computation for the purposes of greater speed and fewer errors. Building machines to carry out these procedures turned out to be much harder than specifying the procedures. Pascal designed and built an arithmetic machine in the 1600s that was able to add and subtract. It could multiply only in the hands of a human operator who understood repeated addition. It could not do division. Napier invented the logarithm, which became the principle of the slide rule—an aid for calculation that continued well into the second half of the 1900s. It could not add or subtract. In 1819 Babbage designed a machine of gears, shafts, and wheels that could calculate tables of arithmetic numbers such as logarithms. In the 1890 US census, Hollerith’s punched card machines tabulated large amounts of data and, after its founding in 1924, IBM became wealthy from selling tabulating machines. In the 1920s engineers designed analog computers to calculate continuous functions by simulating them with circuits and gears. Designers of mechanical analog and digital computers were obviously computational thinkers. But even the analog computer idea is ancient, dating back to the Greek orrery, a mechanical device used to calculate planetary positions in 100 BCE.

Computing throughout the ages required computational thinking to design computational procedures and machines to automate them. The long quest for computing machines was driven not only by the need to speed up computation, but to eliminate human errors, which were common when easily bored or distracted humans performed many repetitive calculations. The designers believed automated machines would overcome the sources of error in calculations. Today we know better: while machines have eliminated some kinds of error, a whole horizon of new errors has appeared. Computing machines have become so complex that we do not know how much trust we can place on them.

Seeds of computational thinking advanced in sophistication over those many centuries. But only when the electronic computer became an industry in the 1950s did computer designers and programmers find an impetus to develop CT as a professional concern. These professionals gravitated to software because they could easily alter a machine’s function by reprogramming the software. The emerging computing industry sought programmers and engineers schooled in computational thinking and practice. Educators inquired into how to teach them. The computer science (CS) field that emerged by 1960 inherited the responsibility for defining and teaching CT.

Throughout this book, we present many examples from the history of computing to illustrate the needs to which CT responded, the new possibilities for actions CT enabled, and the dramatic mind shifts CT caused in how we see automation, science, and the world. Although CT as a way of thinking has existed for thousands of years, the term「computational thinking」is relatively new: the first occurrence we are aware of is from 1980.

Emergence of Education Movement for CT in K–12 Schools

The first computer science (CS) department was founded at Purdue in 1962. Academic computer science matured along a bumpy and challenging path. Many universities were initially skeptical whether the new field was really new or scholarly enough; it looked rather like a branch of electrical engineering or applied mathematics. Many computer science departments were formed only after pitched political battles in their universities. Despite the political difficulties, the growth was steady. By 1980 there were about 120 CS departments in the US alone. Today all major and many smaller universities have one.

During the first 40 years, most of the concerns of practitioners in computing were focused on getting the technology to work. Everything we today consider a core technology had to be invented, designed, tested, and retested—take, for example, programming languages, operating systems, networks, graphics, databases, robotics, and artificial intelligence. One of the central elements of CT, designing reliable computing technologies, became a standard during those times.

In the 1980s, computing experienced a dramatic opening as scientists in all fields brought computation and computational thinking into mainstream science. At first, they used computation to simulate existing theoretical models or numerically tabulate and analyze data from experiments. But they soon discovered that thinking in terms of computation opened a door to a whole new way of organizing scientific investigation—CT led to Nobel Prizes for discoveries that had previously eluded scientists. Many declared computation a third pillar of science, alongside theory and experiment. CT was extended to designing computations throughout science, especially in response to「grand challenge」questions posed by leaders in the different fields. Every field of science eventually declared it had a computational branch, such as computational physics, bioinformatics, computational chemistry, digital humanities, or computational sociology.

Computer scientists had mixed reactions to these developments. Remembering their battle scars from forming departments, some were quite sensitive to the public image of computer science and wanted to control it. Some regarded the computational science movement as a means to hijack computer science by scientists who had previously expressed skepticism about computer science. As a result, computer scientists had a strong motivation to help the public understand the technology and theory of computing. Computer science educators worked with K–12 educators to define computer literacy courses, but these were not very popular. Around the year 2000 some educators proposed a more sophisticated approach they called「fluency with information technology」; high school teachers adopted a popular textbook in that area. Even with the success of the fluency approach, few high schools adopted a computer course. Computer science educators continued to seek ways to penetrate K–12 school systems and expose every student to computing.

A turning point came in 2006 when Jeannette Wing, then starting as an assistant director at the US National Science Foundation (NSF), reformulated the quest from fluency to computational thinking. She proposed that CT was a style of thinking that everyone needed to learn in the computing age. At the NSF she mobilized significant resources to train teachers, upgrade the Advanced Placement test, design new「CS principles」first-courses for colleges, define CT for the K–12 education sector, and issue curriculum recommendations for K–12 schools. This「CS for all」movement has achieved much greater penetration of computing into K–12 schools than any of its predecessors.

The definitions of CT that have emerged from the post-2006 CT movement have moved conspicuously into the public view. But many public definitions, especially as interpreted to us by policymakers, are quite narrow compared to the notions of CT developed over the earlier centuries of computing. Mainstream media occasionally give a misinformed view of the scope and influence of computing. They have led people unfamiliar with computing to make inflated claims about the power of CT that will mislead students and others into making promises about computers they cannot deliver.

Our Objectives in This Book

Our objective in this book is to lay out the magnificent fullness of computational thinking and its precepts about computation and to dispel misunderstandings about the strengths and limits of computing.

Computational thinking evolved from ancient origins over 4,500 years ago to its present, highly developed, professional state. The long quest for computing machines throughout the ages was driven not only by the need to speed up computation, but also to eliminate human errors, which were common when easily bored or distracted humans performed many repetitive calculations. A special thinking skill evolved to accomplish this.

The development of computational thinking opened six important dimensions that are characteristic of CT today.

•	Methods. Mathematicians and engineers developed methods for computing and reasoning that non-experts could put to work simply by following directions.

•	Machines. Inventors looked for machines to automate computational procedures for the purpose of greater speed of calculation and reduction of human errors in carrying out computations. This led eventually to the invention of the digital electronic computer that harnesses the movement of electrons in circuits to carry out computations.

•	Computing Education. University educators formed computer science to study and codify computation and its ways of thinking and practicing for institutions, businesses, science, and engineering.

•	Software Engineering. Software developers formed software engineering to overcome rampant problems with errors and unreliability in software, especially large software systems such as major applications and operating systems.

•	Design. Designers bring sensibilities and responsiveness to concerns, interests, practices, and history in user communities.

•	Computational Science. Scientists formed computational science to bring computing into science, not only to support the traditions of theory and experiment, but also to offer revolutionary new ways of interpreting natural processes and conducting scientific investigations.

These six dimensions are like different windows looking at CT. Each window offers a particular angle of looking. Some aspects of CT may be visible through two windows, but each in a different light.

In the next six chapters we will examine CT in relation to each dimension above. We round out with a semifinal chapter on CT in modern general education and a concluding chapter about the future of CT.

Chapter 2: CT related to algorithmic procedures to automate processes

Chapter 3: CT related to computing machinery

Chapter 4: CT related to the theory of computing and academic discipline

Chapter 5: CT related to building large software systems

Chapter 6: CT related to designing for humans

Chapter 7: CT related to all the sciences

Chapter 8: Teaching CT for all

Chapter 9: The future of CT

We offer our stories of these dimensions to show you the power of CT and the ways in which it might help you in your work with computers and computation.

Computational thinking evolved from ancient origins over 4,500 years ago to its present, highly developed, professional state. The long quest for computing machines was driven not only by the need for speed, but also to eliminate human errors.