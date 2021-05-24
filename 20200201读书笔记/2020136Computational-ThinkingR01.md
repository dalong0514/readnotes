## 记忆时间

## 目录

0101 What Is Computational Thinking?

0201 Computational Methods

## 0101. What Is Computational Thinking?

An algorithm is a set of rules for getting a specific output from a specific input. Each step must be so precisely defined that it can be translated into computer language and executed by machine.

—— Donald Knuth (1977)

What is a computer? Most people will answer it is an electronic black box that does amazing things by collecting, storing, retrieving, and transforming data. Almost all our devices and gadgets are computers: phones, tablets, desktops, web pages, watches, navigators, thermometers, medical devices, clocks, televisions, DVD players, WiFi networks. Our services are software — bookstores, retail stores, banks, transportation, Uber, hotel reservations, Airbnb, filmmaking, entertainment, Dropbox, online courses, Google searches — and almost all run by unseen computers across an unseen worldwide network called「the cloud.」Computers have brought enormous benefits — new jobs, access to information, economic development, national defense, improvements in health, and much more. They have brought, as well, worrying concerns — job losses, globalization, privacy, surveillance, and more. It looks like everything that can be digitized is being digitized and computers are everywhere storing and transforming that information. A computer revolution is truly upon us.

How shall we think about all this? What do we need to understand about computers? What must we do to put a computer to work for us? How do computers shape the way we see the world? What new do we see? What is the role of programming? What are computers not good for?

### 1.1 The Power and Value of Computation

Computational thinking (here abbreviated CT) offers some answers to these questions. Much of CT is specifically oriented on figuring out how to get a computer to do a job for us — how to control a complex electronic device to do a job reliably without causing damage or harm. Algorithms are the procedures that specify how the computer should do a job. Although humans can carry out algorithms, they cannot do so nearly as fast as a machine; modern computers can do a trillion steps in the time it takes a human to do one step. The magic is nothing more than a machine executing large numbers of very simple computations very fast. Programs are the bridge: algorithms encoded in special-purpose languages that translate to machine instructions that control a computer.

But CT reaches further than automation. Information and computational processes have become a way of understanding natural and social phenomena. Much of CT today is oriented toward learning how the world works. A growing number of biologists, physicists, chemists, and other scientists are looking at their subject matter through a computational lens; professionals in the arts, humanities, and social sciences are joining in. Computer simulation enables previously impossible virtual experiments. The「information interpretation」of the world offers conceptual and empirical tools that no other approach does.

CT also advises us about jobs that computers cannot do in any reasonable amount of time. Or at all — some jobs are impossible for computers. Many social, political, and economic problems are beyond the pale of computers. By understanding the limits of computing, we can avoid the trap of looking to computing technology to solve such problems.

Obviously, designing a program or a machine to do so much in such a short time is a daunting design task that demands its own way of thinking if we are to have any confidence that the machine does the job without error. Indeed, understanding users, and designing systems specifically for them, turns out to be one of the great challenges of modern computing. Design is one of the central concerns of CT.

### 1.2 Defining Computational Thinking

Computational thinking has become a buzzword with a multitude of definitions. We have distilled the spirit of the multitude into this definition used throughout this book:

Computational thinking is the mental skills and practices for:

1 designing computations that get computers to do jobs for us, and

2 explaining and interpreting the world as a complex of information processes.

1-2『这里作者对 CT 下了定义，做一张术语卡片。（2021-05-04）』—— 已完成

The design aspect reflects the engineering tradition of computing in which people build methods and machines to help other people. The explanation aspect reflects the science tradition of computing in which people seek to understand how computation works and how it shows up in the world. Design features immersion in the community being helped, explanation features being a dispassionate external observer. In principle, it is possible to design computations without explaining them, or explain computations without designing them. In practice, these two aspects go hand in hand.

Computations are complex series of numerical calculations and symbol manipulations. Examples of numerical calculations are the basic arithmetic operations (add, subtract, multiply, divide) and the basic trigonometric functions (sine, cosine, and tangent). Examples of symbolic manipulations are logical comparison of numbers or symbols, decisions of what instructions to do next, or substitutions of one string of letters and numbers for another. Amazing computations can be carried out when trillions of such simple operations are arranged in the proper order — for example, forecasting tomorrow's weather, deciding where to drill for oil, designing the wings of an aircraft with enough lift to fly, finding which physical places are most likely to be visited by a person, calling for a taxi, or figuring out which two people would make a great couple.

Computers are agents that carry out the operations of a computation. They follow programs of instructions for doing arithmetic and logic operations. Computers can be humans or machines. Humans can follow programs, but are nowhere near as fast or as error-free as machines. Machines can perform computational feats well beyond human capabilities.

We use the word「job」to refer to any task that someone considers valuable. Today many people look to computers (actually, computations performed by computers) to get jobs done. They seek automation of jobs that could not be done without the aid of a machine. Computers are now getting good enough at some routine jobs so that loss of employment to automation has become an important social concern.

We do not equate「doing a job」with automation. Well-defined, routine jobs can be automated, but ill-defined jobs such as「meeting a concern」cannot. CT can help with jobs that cannot be automated. In the design chapter we will discuss the kind of CT that does this.

There is clearly a special thinking skill required to successfully design programs and machines capable of enormous computations and to understand natural information processes through computation. This skill — computational thinking, or CT — is not a set of concepts for programming. Instead, CT comprises ways of thinking and practicing that are sharpened and honed through practice. CT is a very rich skill set: at the end of this chapter we outline the six dimensions of computational thinking that you will encounter in this book: machines, methods, computing education, software engineering, design, and computational science.

### 1.3 Wishful Thinking

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

### 1.4 Emergence of CT over Millennia

It might seem that CT is a product of the electronic computer age that began in the 1940s. Well, not really. Before the modern computer age there was a profession of mathematically trained experts who performed complex calculations as teams. They were called「computers.」They were by no means the first: the term「computer,」meaning「one who computes,」dates back to the early 1600s. The first electronic computing machines were called automatic computers to distinguish them from the human variety. Human computers and, even more so, the leaders of human computing teams, obviously engaged in computational thinking. So, many aspects of CT existed before electronic computers. Well before.

Primitive forms of CT as methods of calculation were recorded from around 1800 to 1600 BCE among the Babylonians, who wrote down general procedures for solving mathematical problems. Their rule-following procedures have features that we, from today's perspective, would label as forms of CT. Similarly, the Egyptian engineers who built the pyramids beginning around 2700 BCE obviously knew a lot about geometry and were able to calculate the dimensions and angles of stones for each part of the pyramid and of the leverage of ropes, pulleys, and rollers to move the stones into position. Computing is an ancient human practice.

Over the ages since ancient times, mathematicians sought to spell out procedures for ever more advanced calculations, moving beyond calculating merchant transactions and the geometry of structures, to trigonometry, astronomic predictions, celestial navigation, solving algebraic equations, and eventually computing with the calculus of Newton and Leibniz. By formalizing computing procedures, mathematicians made their expertise available to non-experts who simply had to follow directions of carrying out simple arithmetic operations in the proper order. A special class of those directions is today called an algorithm — a key concept in modern computing. The term「algorithm」comes to us from the Persian mathematician Muhammad ibn Mūsā al-Khwārizmī who, around 800 CE, discussed how to formulate mathematical procedures and gave examples such as finding the greatest common divisor of a set of numbers.

We humans have a penchant for automating routine procedures. So it has been for computational procedures: inventors sought machines that would automate computation for the purposes of greater speed and fewer errors. Building machines to carry out these procedures turned out to be much harder than specifying the procedures. Pascal designed and built an arithmetic machine in the 1600s that was able to add and subtract. It could multiply only in the hands of a human operator who understood repeated addition. It could not do division. Napier invented the logarithm, which became the principle of the slide rule — an aid for calculation that continued well into the second half of the 1900s. It could not add or subtract. In 1819 Babbage designed a machine of gears, shafts, and wheels that could calculate tables of arithmetic numbers such as logarithms. In the 1890 US census, Hollerith's punched card machines tabulated large amounts of data and, after its founding in 1924, IBM became wealthy from selling tabulating machines. In the 1920s engineers designed analog computers to calculate continuous functions by simulating them with circuits and gears. Designers of mechanical analog and digital computers were obviously computational thinkers. But even the analog computer idea is ancient, dating back to the Greek orrery, a mechanical device used to calculate planetary positions in 100 BCE.

Computing throughout the ages required computational thinking to design computational procedures and machines to automate them. The long quest for computing machines was driven not only by the need to speed up computation, but to eliminate human errors, which were common when easily bored or distracted humans performed many repetitive calculations. The designers believed automated machines would overcome the sources of error in calculations. Today we know better: while machines have eliminated some kinds of error, a whole horizon of new errors has appeared. Computing machines have become so complex that we do not know how much trust we can place on them.

Seeds of computational thinking advanced in sophistication over those many centuries. But only when the electronic computer became an industry in the 1950s did computer designers and programmers find an impetus to develop CT as a professional concern. These professionals gravitated to software because they could easily alter a machine's function by reprogramming the software. The emerging computing industry sought programmers and engineers schooled in computational thinking and practice. Educators inquired into how to teach them. The computer science (CS) field that emerged by 1960 inherited the responsibility for defining and teaching CT.

Throughout this book, we present many examples from the history of computing to illustrate the needs to which CT responded, the new possibilities for actions CT enabled, and the dramatic mind shifts CT caused in how we see automation, science, and the world. Although CT as a way of thinking has existed for thousands of years, the term「computational thinking」is relatively new: the first occurrence we are aware of is from 1980.

### 1.5 Emergence of Education Movement for CT in K–12 Schools

The first computer science (CS) department was founded at Purdue in 1962. Academic computer science matured along a bumpy and challenging path. Many universities were initially skeptical whether the new field was really new or scholarly enough; it looked rather like a branch of electrical engineering or applied mathematics. Many computer science departments were formed only after pitched political battles in their universities. Despite the political difficulties, the growth was steady. By 1980 there were about 120 CS departments in the US alone. Today all major and many smaller universities have one.

During the first 40 years, most of the concerns of practitioners in computing were focused on getting the technology to work. Everything we today consider a core technology had to be invented, designed, tested, and retested — take, for example, programming languages, operating systems, networks, graphics, databases, robotics, and artificial intelligence. One of the central elements of CT, designing reliable computing technologies, became a standard during those times.

In the 1980s, computing experienced a dramatic opening as scientists in all fields brought computation and computational thinking into mainstream science. At first, they used computation to simulate existing theoretical models or numerically tabulate and analyze data from experiments. But they soon discovered that thinking in terms of computation opened a door to a whole new way of organizing scientific investigation — CT led to Nobel Prizes for discoveries that had previously eluded scientists. Many declared computation a third pillar of science, alongside theory and experiment. CT was extended to designing computations throughout science, especially in response to「grand challenge」questions posed by leaders in the different fields. Every field of science eventually declared it had a computational branch, such as computational physics, bioinformatics, computational chemistry, digital humanities, or computational sociology.

Computer scientists had mixed reactions to these developments. Remembering their battle scars from forming departments, some were quite sensitive to the public image of computer science and wanted to control it. Some regarded the computational science movement as a means to hijack computer science by scientists who had previously expressed skepticism about computer science. As a result, computer scientists had a strong motivation to help the public understand the technology and theory of computing. Computer science educators worked with K–12 educators to define computer literacy courses, but these were not very popular. Around the year 2000 some educators proposed a more sophisticated approach they called「fluency with information technology」; high school teachers adopted a popular textbook in that area. Even with the success of the fluency approach, few high schools adopted a computer course. Computer science educators continued to seek ways to penetrate K–12 school systems and expose every student to computing.

A turning point came in 2006 when Jeannette Wing, then starting as an assistant director at the US National Science Foundation (NSF), reformulated the quest from fluency to computational thinking. She proposed that CT was a style of thinking that everyone needed to learn in the computing age. At the NSF she mobilized significant resources to train teachers, upgrade the Advanced Placement test, design new「CS principles」first-courses for colleges, define CT for the K–12 education sector, and issue curriculum recommendations for K–12 schools. This「CS for all」movement has achieved much greater penetration of computing into K–12 schools than any of its predecessors.

The definitions of CT that have emerged from the post-2006 CT movement have moved conspicuously into the public view. But many public definitions, especially as interpreted to us by policymakers, are quite narrow compared to the notions of CT developed over the earlier centuries of computing. Mainstream media occasionally give a misinformed view of the scope and influence of computing. They have led people unfamiliar with computing to make inflated claims about the power of CT that will mislead students and others into making promises about computers they cannot deliver.

### 1.6 Our Objectives in This Book

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

## 0201. Computational Methods

If controversies were to arise, there would be no more need of disputation between two philosophers than between two accountants. For it would suffice to take their pencils in their hands, to sit down to their slates, and to say to each other (with a friend as witness if they liked): Let us calculate.

—— Leibniz, in Russell's translation (1937)

When Peter was age 10, his twinkly-eyed math teacher told him he could read minds.「How could you do that?」Peter asked. The teacher said,「Here, I'll show you. Think of a number. Double it. Add 8. Divide by 2. Subtract your original number. Now concentrate hard on the answer. ... There, I see it. The answer is 4.」Peter was so astonished he insisted that the teacher show him how to do this.「Well,」said the teacher,「it's just math. Let's say X is your number. Then I got you to calculate the expression (2X+8)÷2–X = 4. Your initial number was subtracted out. The answer is always half the number I told you to add.」Peter had many fine moments reading the minds of his family and friends with this method. He also got hooked on mathematics and computing.

This is one of many mathematical methods handed down over many generations. Methods like this are behind a pack of「automatic tricks」used by magicians, where the trickster leads the subject through a series of steps to an answer known to the trickster and believed by the subject to be a secret. The sleights of mind to accomplish this are in the math steps known to the trickster but not the subject. They work for any trickster who follows the directions, even if the trickster has no idea why the directions work.

Many other methods with a more serious purpose were handed down through the ages. One of the earliest methods, taught to many schoolchildren today, comes from the Greek mathematician Euclid around 300 BCE. He gave a method to find the greatest common divisor (GCD) of two numbers, which is the largest integer that divides both numbers. Euclid found a clever reduction rule by noticing that the GCD of two numbers divides their difference. He repeatedly replaced the larger number with their difference, until both were the same. For example, GCD(48,18) = GCD(30,18) = GCD(12,18) = GCD(12,6) = GCD(6,6) = 6. This method was used to reduce fractions. Today it is among the basic methods underlying cryptography.

Another famous method dating back to the Greeks was the Sieve of Eratosthenes, used to find all the prime numbers up to a limit. This method begins with a list of all the integers from 2 to the limit. It then crosses out all the multiples of 2, then all multiples of 3, then of 5, and so on. After each round of elimination, a new prime will be revealed; the next round crosses out all its multiples. This is a very efficient method to find small primes and has been adapted to finding large primes for keys in modern cryptographic systems.

The Greeks were also interested in calculating the areas of shapes. They did so by finding ways to tile the shapes with simple forms such as squares or triangles, and then successively reducing the dimensions of the forms until the original shape is almost completely filled with them. This method, first recorded in the period 400–350 BCE, was a precursor to better methods introduced in the modern calculus two thousand years later.

Many mathematicians used such methods to construct infinite series of simple terms that converged to some limit. Math books are filled with tables of series; mathematicians used them to replace long series with closed forms. One such example is the series , which gives a way to calculate the value of π, with greater precision when more terms are included.

The calculus, proposed independently by Newton and Leibniz around 1680, perfected the idea of approximating objects and curves by calculations over infinite series. The idea was to represent geometric forms and continuous curves with very small components that interacted locally — for example, fill the form with small boxes or model the curve as a series of tiny segments bound to their immediate neighbors with attractive forces. Then find a larger quantity such as area or length by adding the components. When the size of the components was allowed to approach zero, the expressions from these infinite sums would be exact. The rule of local interaction was represented as a derivative and the summation as an integral. Motivated by calculus, mathematicians evaluated functions by dividing time and space into small increments enumerated as a「grid」and iteratively calculated the value of a function at each grid point. This approach was a boon to physics, in which many mathematical models of physical phenomena were expressed as differential equations computable on finite grids.

Another famous mathematical method was the Gaussian elimination for solving systems of linear equations. Gauss worked with this method in the mid-1800s, although Chinese mathematicians knew it in 179 BCE. Very efficient forms of this algorithm are used in modern graphics displays to render three-dimensional objects in real time.

These few examples illustrate the richness and utility of the treasure trove of methods bequeathed to us over many centuries.

We can conclude from examining these methods that many were quite sophisticated. Their purpose was to capture, as a set of steps, what needed to be done in a complex calculation. Initially those steps were carried out by mathematicians, but with enough refinements a method could actually be used by anyone who could follow the directions. An important but subtle point is that the steps of the method had to be unambiguous. The less the ambiguity, the more trustworthy the method was in the hands of non-experts. It was a practice to reduce ambiguity by replacing fuzzy steps with precise chains of arithmetic and logic operations.

Beginning around 1650, some mathematicians started to look for machines to carry out the basic operations of common methods. Some methods were too complex to be easily remembered. Some methods needed to be iterated many times, and it was difficult for easily distracted human beings to complete them without errors. The machines would allow for much faster computation and fewer errors.

To build machines, mathematicians and inventors had to devise methods, such as the positioning of wheels and gears, to represent numbers with physical quantities. They also had to devise representations for logic steps such as a conditional jump or a loop. Today, representations of data and logic steps are important core elements of computational thinking. In the rest of this chapter we describe these aspects in more depth.

### 2.1 The Quest to Eliminate Intuition

The computational methods that evolved in the history of mathematics were intended to help builders, engineers, merchants, and scientists to calculate numbers. Ancient merchants invented number systems, accounting systems, and tools like the abacus to keep track of their businesses. Ancient engineers invented ways to build weapons of war and civilian structures of peace. All sought reliable methods of dealing with calculations involving large quantities of numbers so that their artifacts worked as intended and were dependable.

Their methods were handed down through apprenticeships and were worked mainly by experts. The experts developed rules-of-thumb, heuristics, learned hunches, and other intuitions that enabled them to solve problems that the uninitiated could not solve at all. The modern term「intuition」describes the expert's action of rapidly articulating a solution, based on extensive experience with similar situations. Intuition enables experts to find the essential core of the problem, skip unnecessary steps in solving it, and switch between solution approaches. Intuition is a manifestation of expertise and an enabler of new findings.

It might seem paradoxical then that throughout the ages much work in mathematics and logic has aimed at eliminating intuition from routine calculation and logical inference. Routine computing tasks were required to be as simple and「mechanical」as possible in order to always yield the same results regardless of who did the calculations. Mathematicians throughout history have sought to capture expertise into step-by-step procedures someone could follow with little training. Eliminating intuition from routine jobs did not mean eliminating experts, but rather making their expertise available to a large number of non-expert people.

The modern ideas of symbolic information representation, symbol processing, unambiguous computational steps, basic arithmetic, algorithms, synchronization of computations, and systematic error checking are all inheritances from those many centuries. By showing how mechanization of calculations has been a key feature in numerous developments of computational methods, our aim is to reveal how many computational thinking skills have been an integral part of many other kinds of thinking long before modern computing. Many features and practices of computational thinking support the designing of computations in many fields, not just in today's computer science.

### 2.2 Numerical Representations and Numerical Methods

Computational thinking, like much of modern science, relies on a process of representing things in the world in numbers or other symbols. A representation is an arrangement of symbols in an agreed format; each representation stands for something. We frequently use numbers to represent quantities such as census data on populations, business accounting ledgers, or engineering measurements. But numbers are not the only kinds of representation. Scientists and engineers represent phenomena with equations, such as a linear algebraic matrix for rotating an object or a differential equation for planetary motion. They also represent objects with mechanical artifacts such as models of buildings, wind tunnels, or planetary orreries. Numbers, equations, and models underpin the scientific ideals of measurement, experimentation, and reproducibility of results. In the computing age, representations with non-numeric symbols have become ubiquitous — for example, a Java language program, a bitmap of an image, or a soundtrack of music. Today we use the term digitization for the process of encoding almost any information in the form of data representations that can be processed by computers.

It might seem paradoxical that throughout the ages much work in mathematics and logic has aimed at eliminating intuition from routine calculation and logical inference. Eliminating intuition from routine jobs did not mean eliminating experts, but rather making their expertise available to a large number of non-expert people.

Some skeptics did not trust these computational methods because numerical calculations were too susceptible to tiny errors in the precision of parameters and variables of the computation. This led the designers of methods to find constraints to keep accumulating errors within acceptable bounds. Today's computing machines have the same problems because the machines have limited precision (such as 32 or 64 bits) and round-off errors could accumulate in poorly designed algorithms. The calculus was a breakthrough because it allowed designers systematic ways to limit errors in their finite-difference calculations.

### 2.3 Decomposing Computing Tasks

During the time leading up to World War II, the US Army developed ever more sophisticated artillery that could fire shells over several miles. Gunners needed to know how to aim their artillery given the range, the difference of elevation, and the winds. The Army commissioned teams of human computers to work out firing tables for these guns. The gunners simply looked up the proper angle and direction to aim their guns, given their measurements of range, elevations, and winds.

One of the most well known of these teams comprised women working at Aberdeen Proving Grounds around 1940. They organized into assembly lines, each one doing a different stage of computation, until they compiled the firing tables. For tools they used mechanical calculators that do basic arithmetic (add, subtract, multiply, divide). They followed programs (i.e., sets of procedures) that managers established to divide the work and to govern which intermediate calculations moved from one human computer to the next. As trained mathematicians, the human computers were able to spot errors in their computations and thus keep the firing tables error free.

Today's computational thinking follows a similar pattern learned from those days:

1 Break the entire computation into pieces that could be done by separate, interacting computers.

2 Arrange the computers to optimize their communication and messaging patterns — for example into an assembly line or as a massive parallel fan-out and join.

3 Include error checks into their methods so that recipients could verify that their inputs and outputs were correct.

Modern software designers are familiar with these principles under the following names: distributed computing, parallelization, and error checking. But those practices were not originally developed for machines — they were developed for human computers.

The US Army wanted to perform these computations at much larger scales and much faster than human teams could at Aberdeen, so it commissioned the electronic computer project ENIAC at University of Pennsylvania to do this. The designers of ENIAC faced huge challenges, such as learning how to build reliable electronic circuits to carry out the same computations much faster, and learning how to design the control programs and algorithms to prevent errors from accumulating in the computations. The method of decomposition of the task into unambiguous steps that passed data between them moved from being a management principle at Aberdeen into a design principle for automatic computers.

Concern over errors grew as machines became larger and more complex. Today in computer science we still teach this old wisdom: errors can happen at any stage of the computing process, including describing the problem, preparing the formulas, setting the constants, communicating data, recording and retrieving the data, carrying out the prescribed steps, or displaying the results.

### 2.4 Rules for Reasoning

Designing computations around unambiguous steps is not enough to give confidence that computations are free from errors. The steps must be strung together to follow a plan. At any stage in the computation the plan must tell us unambiguously what the next step is. Deciding what the next step is should be an exercise in logic.

A long-established branch of mathematics and philosophy has been concerned with logic. Can we provide the means to develop long chains of reasoning to solve problems and to verify that a given chain of reasoning is valid? As their counterparts in calculation, logicians sought ways to formalize and automate reasoning. Philosophers such as René Descartes and Gottfried Leibniz in the 1600s sought a language that would completely formalize human inference and reduce misunderstandings. Their goal was to establish a standard way to express concepts and rules of inference to definitively establish the truth or falsity of statements. According to their vision, such a「language of thought」would bring an end to disagreements in all domains, because every debate could be resolved through pure logic.

Progress toward this dream was slow. A breakthrough came in the 1800s. George Boole (1815–1864) was fascinated by how well-formulated, mathematical symbol systems were able to provide results for problems nearly automatically once the correct values were set in the formula. [1] In his book, Laws of Thought (1854), he presented「an algebra of thought」paralleling the algebra of numbers. His logic included variables whose values could be either true or false. He could form logical expressions, which were formulas of variables connected by operators such as and, or, and not. Nearly nine decades later (1937), Claude Shannon showed how Boole's algebra could describe the function of relay circuits in telephone systems and other electrical circuits. Boolean algebra was perfected for electronic circuit design in the 1950s, where it provided a means to find the smallest circuit for a given logic function and a means to design the circuit to avoid race conditions, which are ambiguous outputs caused by signals changing at different speeds in different parts of the circuit. Boolean algebra became a fixture of computer circuit design.

1『这里看到了 2 个熟人。George Boole，布尔，布尔值。Claude Shannon，香农，信息论。（2021-05-24）』

Despite its merits, Boole's algebra of logic had some serious limitations. Sentences that refer to sets, such as「everybody with a gray hair,」while perfectly understandable in natural language, could not be expressed in Boolean logic. There was no way to generate a list of entities satisfying a formula; the concepts of「everybody」and「somebody」had no clear meaning. There were no rules for the important quantifiers all and some.

Gottlob Frege (1848–1925) presented a new system of logical inference,「language for pure thought」(1879), which today is called predicate logic. It included new quantifiers for all and some and closed gaps in Boolean logic. Frege's system also presented mechanical rules for symbol processing that could be followed without appealing to human intuition. Frege's predicate logic resembles a programming language in that it provides an artificial, formal language that presents unambiguous, deterministic, and mechanical rules for symbol processing.

3『戈特洛布·弗雷格 (Gottlob Frege)，著名德国数学家、逻辑学家和哲学家。是数理逻辑和分析哲学的奠基人。（2021-05-24）』

In the early 1900s it looked like the vision for a formal language of thought was about to be fulfilled. The merger of mathematics and logic gave rise to Russell and Whitehead's magnum opus Principia Mathematica (1910) and to logical empiricism in the sciences. But one element was still missing to achieve the dream: a method for definitively deciding whether a statement in predicate logic was true or false. The question for whether such a method exists became known as the「decision problem.」By the 1920s, it was taken as one of the major challenges in mathematics. Most mathematical logicians believed that a method existed, but no one could find it.

### 2.5 Mechanizing Computation

In 1935, a young Cambridge mathematics student was introduced to the decision problem. He became fascinated by the words a lecturer used to pose it: Was there a mechanical process for deciding, in a finite number of steps, whether a proposition in predicate logic is true or false? That student, Alan Turing (1912–1954), decided to develop a thoroughly mechanistic model of computing so that he could investigate the decision problem.

Turing started with the idea that, when calculating numbers, a human computer writes down a series of symbols on the paper. He represented the paper as a linear sequence of boxes each holding a single symbol. In calculating, the person moves attention from the current box to either of its nearest neighbors, possibly changing the symbol in the box. He assumed that the mind of the person doing the calculation was in one of a finite number of states, and that each of these basic moves on the paper was generated by a transition from the current state to a specified next state. This process continues until the calculation is complete. Turing took these basic actions — when in a given state, move left or right one box, read symbol at the current box, change the symbol in the current box, and move to the next state — as the basic mechanics of carrying out a computation. Clearly a machine could do these steps and keep track of the states. He noted that this machine modeled steps in calculating numbers or evaluating logic functions. After demonstrating how such a machine would work, Turing showed that there is one such machine that can simulate all others — implying that the machine model is a universal way to represent all calculations and proofs. He then proved that no machine could solve the decision problem because the very existence of a machine that could do so led to a logical paradox. This tour-de-force eventually made him famous for his「Turing machine」and its implications for computation.

A few years later, the electronic digital computer provided the means to automate calculation and proof — finally realizing, at least to some extent, the visions of mechanizing calculation and reasoning. Automation was the key to all these developments. To emphasize this, Turing called his machines a-machines, with「a」meaning「automatic.」Similarly, the engineers designing the first electronic computers in the 1940s, such as UNIVAC and BINAC, gave them names ending in「-AC」meaning「automatic computer.」Through the 1980s, computer science itself was often characterized as the science of automation. The key aspect of automation demands that a machine do the work without human intervention. The automatic computer is the ultimate realization of the old dream of making calculation available for the masses without requiring them to be experts in doing calculations.

Another key aspect of automation is recognizing that automatic computers cannot perform certain important tasks. Turing showed this when he proved no a-machine could exist to solve the decision problem. His same reasoning shows that problems of practical interest — such as determining whether a given computer program will halt or instead enter an infinite loop, or whether a given program contains a computer virus — cannot be solved by any machine. For this reason, a large segment of CT is concerned with how to provide partial solutions to problems that cannot be solved by automatic computers.

The automatic computer and the understandings of its limitations would not have been implemented without the merger of calculation and logic. It is no wonder many people consider logical thinking an essential element of computational thinking.

### 2.6 Computational Thinking Insights Come from Many Fields

It should be clear from this discussion of the origins of computational thinking that CT is not about how computer scientists think. Modern computer science is the last 1 percent of the historical timeline of computational thinking. Computer scientists inherited and then perfected computational thinking from a long line of mathematicians, natural philosophers, scientists, and engineers all interested in performing large calculations and complex inferences without error. CT is a feature of many fields, not only computing.

Logicians wished to create formal systems where one could start from the premises and, by following chains of substitutions within a formal system of rules, would always arrive at the same conclusions. The logical insights of Boole and Shannon — that a few logical operations can express the truth values of all propositional logic as well as the logical design of digital circuits — were driven by an old quest to banish all human emotion and judgment from logical inference. These insights are counted today as the first principles of computing. Frege's logical insight — predicate logic — presented a more powerful system of inference having many similarities with modern programming languages. Turing's insight into the essential features of automatic processing — that five actions and a finite number of states are enough for any computation — came from mathematical logic.

Other basic insights of computational thinking arose from science and engineering. Among the most important is the realization that most computations in science and technology require unimaginably long calculations that are well beyond the capabilities of a human team. The designers of computational methods to solve practical problems are obsessively concerned with controlling and limiting errors by making the computational steps simple and unambiguous and their connective logic unimpeachable.

The computer of today is the machine many sought throughout the ages to automate calculation and free it from the frailties of humans and the need for their intervention and judgment. Modern computing researchers and professionals embody this long history and excel at automating computations using the best methods available. However, as we will see in the next chapter, the wish of building real systems for very large, error-free computations has been exceedingly difficult to achieve.

The computer of today is the machine many sought throughout the ages to automate calculation and free it from the frailties of humans and the need for their intervention and judgment.