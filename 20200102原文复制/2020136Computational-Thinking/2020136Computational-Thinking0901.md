# 0901. Future Computation

Technology is part of our civilization. Sometimes people talk about conflict between humans and machines, and you can see that in a lot of science fiction. But the machines we're creating are not some invasion from Mars. We create these tools to expand our own reach.

—— Ray Kurzweil (2013)

Computational thinking is an ongoing quest to capture computing's ways of thinking and practicing. It is in never-ending flux, constantly renewing itself. Although many of the central CT precepts are very old, evolution of computing practice and technological state-of-the-art have affected how we see CT and what is central to CT. For instance, ever-evolving software development suites, new languages, and cloud services are shifting computational design tasks away from lower-level programming operations toward higher and higher levels of abstraction — thereby making computing jobs more design-intensive. Traditional programming is losing its role as the primary interface to computations; instead, domain-specific and intelligent tools are enabling more and more users to harness the potential of computers without programming them. CT expands well beyond programming and software development.

We will discuss some of the forces that are shaping our world and their likely effects on how we see computing and think about it. We will also discuss some important questions that CT cannot help us with. CT has its limits.

## 9.1 New Computational Models

One of the most obvious reasons why CT is changing is that computing technologies are changing. Throughout the long reign of Moore's law for silicon chips, the basic architecture of chips in computers and mobile devices has remained true to the von Neumann design from 1945 — separate memory and processing units, with a processor stepping through instructions stored in memory. The notion of「computational steps」in the modern definitions of CT comes from this design as well as from Alan Turing's definitions of computing.

But Moore's law cannot be sustained because of the physics of silicon and the nature of the chip-making process.1 For this reason, researchers have been searching for new technologies that might supersede silicon-based von Neumann architectures and continue the exponential growth rate of information processing speed. Quantum computers, neural networks, reversible computers, DNA computers, memristor computers, and a few others are prime candidates. Each technology defines a new computational model that is the target for designers.

Consider, for instance, the D-wave, a commercial quantum computer.2 It is designed to solve a set of equations, well known in physics as the Ising Model, which describe how certain systems settle into minimum energy states. Programming a D-wave computer means to encode the problem as a set of Ising equations and to input the coefficients into the machine; execution means to let the machine settle into a minimum energy state corresponding to the solution of the equations (a few microseconds); readout consists of reading the qubits (quantum bits) of the machine and interpreting them as the answer. There is no concept here of an「instruction set」or of programming as「designing a sequence of steps.」Most computer scientists, on being shown how to set up the D-wave machine for the first time, experience a mind tilt — the process is nothing like the programming process they have known all their professional lives.3 Trained physicists have much less trouble understanding the machine. The current working definition of CT — formulating a problem so that it can be solved as a series of computational steps — fails to describe the computational thinking this machine involves.

DNA computing is another technology being investigated. In 1994 researchers performed an experiment in which they encoded possible paths in a map into strands of DNA, and then used the chemical methods of the day to evolve the initial mixture into one where the majority of strands represented the shortest tour of the map.4 Considerable progress has been made with this technology. In 2016, another research team used the modern CRISPR gene editing technique to insert an image into the DNA of a bacterium. Computer scientists trained to think in terms of computational steps have more trouble than molecular biologists understanding how DNA computing works.

These examples illustrate CT has expanded beyond the idea of problem solving with computational steps. Our broader definition — designing computations that get computers to do jobs for us, as well as explaining and interpreting the world as a complex of information processes — is closer to the mark.

## 9.2 Design

The ongoing increase in the importance of design is another reason CT is changing. Computational thinking is no longer confined to developing programs and algorithms to solve computational problems. Only a small portion of apps development, for example, is concerned with algorithms; the bulk of the work focuses on design of systems to deal with the concerns of a community. Design in this sense is an ongoing interaction between designers and users, watching their reactions to prototype software, evaluating what works and what does not work, and adapting the software accordingly. This is a much broader view of design than the「blueprint,」the「plan,」or the「setup of an experiment」views of early programming and software engineering communities. It is a skill set that combines sensibilities to moods and histories in communities with deep knowledge of existing technologies and other useful components. Design requires understanding humans in their communities as much as it requires understanding technology.

One effect of new designs in computing has been the automation of many cognitive tasks that as recently as a decade ago were considered out of reach of computing machinery. This kind of automation is displacing workers and has caused great concern that many current jobs could be automated, putting many people out of work. The flip side of the coin, however, is that the new technologies breed new problems that require new designs — creating new jobs for designers.

Computational design is now a skill that you can have in any field besides your primary disciplinary skills. You do not have to be a computer scientist to be a computational designer. Computational design captures the spirit of today's computing revolution better than computational thinking does. Past technology revolutions showed us that the new technologies ultimately created more jobs than they displaced. The current computing revolutions in machine learning and app development are producing new jobs for designers while rendering obsolete some existing jobs by automating them. To help smooth the transitions, governments should help more with training and education programs so that displaced workers can learn the design skills of the new jobs.

The new emphasis on design is rejuvenating the engineering aspect of computing, which is much more sensitive to design than the science side is. The engineering side brings to computational thinking concerns about reliability, fault tolerance, architecture, and systems that are sidelined in the theory- and algorithm-oriented definitions of CT. What is more, it brings to CT human concerns, such as recognizing the social worlds that are embracing computing, adopting a design into a community's practice, recognizing ethical issues brought forth by technology side effects, and providing means that human judgment and care influence the actions of machines.

## 9.3 Machine Learning

Neural networks, first articulated in the 1940s as possible models for electronic computers, have become the main technology behind artificial intelligence (AI) and data analytics today. The neural network was a mathematical model in which a neuron「fired」when the combination of signals from other neurons exceeded its built-in threshold; the「fired」neuron entered an excited state that was then communicated to other neurons. The motivation for imitating the brain was that automatic computers might do human tasks better when built of similar components. Of course, a circuit of these neuron models is nothing like a real brain. The logic circuits of the first computers ran much faster than neural circuits. Today the situation is different: we now know how to use cheap graphics cards to speed up neural network calculations. IBM and Intel now market chips that are even faster; they recognize that a new way of thinking is needed to put their chips to best use and they offer courses in the operation and use of their chips.

Early neural networks were small and easily confused when presented with new inputs not in their training sets. Modern neural networks consist of many layers, have much higher capacity, and are less easily confused. Thanks to graphics processing chips, trained neural networks of many layers respond to inputs almost instantaneously. Since layers, nodes, and connection weights do not change after the network is trained, performance does not depend on the data input. As neural network implementations typically do not have loops, they run in a constant time with constant memory spaces. That means that neural networks can be used in real-time applications with deadlines much more reliably than traditional programs.

A big attraction of neural networks is that they are「trained」rather than「programmed.」For example, we do not have very reliable algorithms for face recognition, but neural networks can be trained to recognize given faces quite reliably. These networks are often called「self-programmed」because no programmer specifies the internal weights — although the weight-adjusting algorithm used in training can be viewed as an automatic programmer. For many problems, it is much easier to find or create suitable training data than to write a rule-based program. As mentioned in previous chapters, a big issue with neural networks is that there is no way to「explain」how the network generated an output, as is possible with traditional programs. Knowing the reasons behind a conclusion is important in many application areas such as medical diagnosis; neural networks confound that. CT has already had to adjust to include the tools used to build and train neural networks. Bigger challenges lie ahead with assessing the reliability and security of neural networks.

Another big attraction is that neural networks can be trained by having them interact with other neural networks instead of given data sets. The network for AlphaGo, which beat the world champion Go player in 2017, was trained by having it play against another AlphaGo network; it learned Go from play rather than from training on a large set of recorded Go games. This way of training networks by letting them learn from each other has the potential to be game changing.

## 9.4 Human-Computer Teaming

Garry Kasparov, the world champion chess grandmaster, was defeated in 1997 by IBM's Deep Blue computer. That game marks a milestone in chess because it was the first time a computer program beat a grandmaster. Kasparov had played several previous matches against lesser computers, winning them all.

Kasparov did not declare the game of chess dead. Instead, he invented a new kind of chess, Advanced Chess. In Advanced Chess, the two players of a match are each assisted by a computer. Before committing to the next move, the human player consults the computer program to gain insights into the possible effects of moves. The computer-assisted chess players played better chess than when they played without computers, but also better chess than computers alone played.

The notion that a human-computer team can always perform better than a very good machine is controversial. There are reports of recent Advanced Chess tournaments in which teams did poorly compared to matches between computers without humans. In medicine, diagnosticians teamed with computers do not always perform as well as the very best diagnostic computer.

Still, human-computer teaming has attracted a lot of attention in artificial intelligence research because it is capable of performing computations that no human or computer could do alone. An early example of this was the labeling of digital images with searchable keywords. Doing it by hand was far too slow to be useful for labeling images online. In 2006, Luis von Ahn of Carnegie Mellon University invented an online game where thousands of pairs of humans labeled the images presented to them; if their keywords matched, their labeled image went into the searchable database. The「labeling function」implemented by these human-computer teams had been thought to be non-computable. The human computer teams were more powerful than computers.

Human-computer teaming requires a different kind of computational thinking than traditional computer programming. We watch with great interest how the controversy over whether teams can outperform machines plays out in the future.

## 9.5 Technology Jumping

In 2006 Ray Kurzweil, a futurist and inventor of computing technologies, prophesied that by 2030 we will be able to build a computer the size of the brain, with the same number of neurons and connections as the brain.5 Such a computer would, he envisioned, develop its own consciousness and superintelligence. How such computers would treat humanity is an unanswerable question. The best that can be said is that the new machines would have such different concerns from ours that we cannot fathom how they would treat us. That moment of their creation is called the singularity because of the utter unpredictability of what lies after an artificial intelligence develops consciousness.

Kurzweil arrived at his conclusion by extrapolating Moore's law, the prediction of Gordon Moore in 1965 that silicon chips would double in capacity about every two years for the same price. The computer chip industry has followed the law by doubling power every two years for over half a century. In many ways Moore's law is a triumph of computational thinking because chip engineers needed to think hard to find ever better ways to build computing circuits.

Kurzweil exploited the phenomenon of technology jumping in his analysis. Since the beginning of the information age in the early 1900s, he argued, the same doubling effect was observed in the technologies of the day, for example punched card machines or vacuum tube machines. When one technology could no longer produce the two-year doubling, another took over. Moore's law for silicon is actually the fifth wave of technologies displaying two-year doubling. Kurzweil has confidently predicted that more technology jumps will occur and sustain the trend, allowing him to predict the processing power available by 2030 and beyond, and arrive at the singularity.

Technology jumping is a standard practice of the computing industry. The adoption of a particular technology versus time almost always follows an S-curve with exponential growth until an inflection point, after which the growth slows down as the market saturates. Business leaders are sensitive to inflection points because a competitor with a better, exponentially growing technology can upend their businesses when their own growth slows. They try to anticipate inflection points by developing new technology in their research labs and jumping to it when their business reaches the inflection point. They can then ride the new technology wave during its exponential growth stage.

Although the singularity is a product of computing and computational thinking, it cannot be addressed with computational thinking, and we cannot improve our understanding of it through computational thinking.

## 9.6 The Whole World Is a Computer Hypothesis

Some scientists have argued that information is the basis of all physics. Every particle and every interaction is the product of information flows and exchanges at a more fundamental level than the smallest particles known. In 2002, Stephen Wolfram, a physicist and inventor of the Mathematica program — a triumph of computational thinking in itself — published a big book in support of this claim.6 In 2003, Nick Bostrom, a philosopher, argued for a possibility that we are characters in a simulation run by a much more intelligent species studying their ancestors. While other physicists see some merit in the claim that all particles and interactions can be explained with quantum mechanical probability waves, which are forms of information, they regard the idea that our world is a digital simulation as far-fetched.7

The whole-world-is-computer hypothesis appeals to those who believe that computational thinking and computing are pervasive without limits.

## 9.7 Ideological Fights over What Should Be Taught

There is a never-ending debate on what should be taught in a computing curriculum. There are two hot spots in the debate. One concerns the selection of programming language and programming framework that students should be introduced to. Should it be a language that is easy to learn and has the least-confusing structure and syntax, such as Python? Or should it be a language that is used by their future employers in industry, such as Java or Javascript? What are the benefits of starting with a framework that treats programs as sources of instructions for a machine (known as an「imperative」framework) compared to one treating programs as compositions of functions (known as a「functional」framework)? These debates have been a staple of computing faculty meetings since the 1960s and are not likely to abate in the years ahead.

The other hot spot is the tension between the ideals of science-mathematics and of engineering-design. The science-mathematics ideal teaches abstractions of things in the world and leaves it to the student to apply the abstraction to the case at hand. The engineering-design ideal focuses on all the details that a builder has to get right for the resulting program to be safe and reliable. The science-math view has had the upper hand for many years, but with the rise of design, the engineering view is gaining new currency. In reality, both traditions are important for the success of computing: the science and engineering sides need each other.

## 9.8 Reflection on the Emerging World

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