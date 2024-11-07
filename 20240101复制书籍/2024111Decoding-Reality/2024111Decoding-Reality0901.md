Vlatko Vedral.(2018).2024111Decoding-Reality.Oxford University Press => 0901Surfing the Waves: Hyper-Fast Computers

## 0901Surfing the Waves: Hyper-Fast Computers

Who hasn't heard of a computer? In a society entirely dominated by these transistor infested boxes there are probably only a few remaining isolated tribes in the Amazon or around the Kalahari that have not been affected. From organizing our finances, flying a plane, warming up food, controlling our heartbeat (for some), these devices are prevalent in each and every aspect of our society. Whether we are talking about personal computers, mainframe computers, or the embedded computers that we find in our mobile phones or microwave ovens, it is very hard to even imagine a world without them.

The term computer, however, means more than just your average Apple Mac or PC. A computer, at its most basic level, is any object that can take instructions, and perform computations based on those instructions. In this sense computation is not limited to a machine or mechanical apparatus; atomic physical phenomena or living organisms are also perfectly valid forms of computers (and in many cases far more powerful than what we can achieve through current models). We'll discuss alternative models of computation later in this chapter.

Computers come in a variety of shapes and sizes and some are not always identifiable as computers at all (would you consider your fridge a computer?). Some are capable of doing millions of calculations in a single second, while others may take long periods of time to do even the most simple calculations. But theoretically, anything one computer is capable of doing, another computer is also capable of doing. Given the right instructions, and sufficient memory, the computer found in your fridge could, for example, simulate Microsoft Windows. The fact that it might be ridiculous to waste time using the embedded computer in your fridge to do anything other than what it was designed for is irrelevant – the point is that it obeys the same model of computation as every other computer and can therefore – by hook or by crook – eventually achieve the same result.

This notion is based on what is now called the Church–Turing thesis (dating back to 1936), a hypothesis about the nature of mechanical calculation devices, such as electronic computers. Alan Turing and Alonzo Church introduced the formalization of an algorithm and a ‘purely mechanical' model for computing, that all modern computers today obey. The thesis claims that any calculation that is at all possible to perform can in fact be performed by an algorithm running on their computational model (which assumes that sufficient time and storage space are available). This leads us to the notion of a universal computer, on which all modern computers are based.

The drive for miniaturization of computing technology cannot have gone unnoticed. In particular, computers have been getting smaller (and hence faster, as closer circuitry means less distance to travel) ever since the first computer was built by von Neumann in the 1940s. In the late 1950s the then chairman and co-founder of Intel, Gordon Moore, noticed a very interesting and remarkable trend: every two years or so computers tend to double in their speed and memory. Moore noted this trend in one of his reports and this has since become known as Moore's law.

But why has Moore's law been upheld in the last 50 years? It certainly is not a natural law as it depends on the existence of humans and is largely related to factors within our control. Perhaps instead it should therefore be known as ‘Moore's trend' or ‘Moore's observation'. Some people more cynical of the computing industry may even say that Moore's law has been correct because of Moore (CEO of Intel, remember). By noting the law, he effectively set the standard for other companies. Given that Intel have such a dominant position within the microchip industry, Moore's law is thus a bit of a self-fulfilling prophecy.

If technology continues to abide by Moore's law, then the continually shrinking size of circuitry packed onto silicon chips would eventually reach a point where individual elements would be no larger than a few atoms. Then what? Where do we go from there? How small and fast can computers be?

Surely, however, there is a natural limitation to this exponential growth. At the moment we are using about 100 electrons to encode one bit of information. But in about 10 years time, we may be using one electron to encode one bit of information. Can we go beyond this and what is the ultimate limit? If physics tells us anything, it's that we should never be too dogmatic about our conclusions. History is littered with ‘no-go' statements which are later proven to ‘go' (e.g. remember Lord Kelvin's statement that machines heavier than air cannot fly, said only 30 years before the Wright brothers proved him wrong). So even as we find the ultimate limit to computation, there is already inherent uncertainty as to how long this limit will hold.

To understand the ultimate limits we first need to understand what computers are all about. Well, it is simple: computers are all about processing bits. The computers we have at present use the laws of Boolean logic to shift, change, and reshuffle bits (i.e. zeros and ones). George Boole published his Boolean algebra in 1854 with a complete system that allowed computational processes to be mathematically modelled. Remember that Shannon used this in the construction of his communication process. The implementation of Boolean logic currently is in terms of transistors, however there are a variety of plausible alternatives. As we know, classical bits, by definition, exist in one of two different states at any given time – a zero or a one. With quantum mechanics, however, we are permitted to have a zero and a one at the same time present in one physical system. In fact, we are permitted to have an infinite range of states between zero and one – which we called a qubit. The number of states a qubit could occupy is infinite because in principle we can tweak the ratio of probabilities in which the states 0 and 1 occur to any desired accuracy. When with certainty we have either 0 or 1 then this reduces to the classical case.

Also, in line with Moore's trend, at the atomic scale the physical laws that govern the behaviour and properties of the transistor circuitry (which is based on semiconductor technology) are inherently quantum mechanical in nature, not classical. Thus the question of whether a new kind of computer could be devised based on the principles of quantum physics is therefore not a forced endeavour but a necessary and natural next step.

It is also interesting to note how transistors, which are the ‘neurons' of all computers, work by exploiting properties of semiconductors. The explanation of how semiconductors function is entirely quantum mechanical in nature; it simply cannot be understood classically. Are we thus to conclude that classical physics cannot explain how classical computers work? Or are we to say that classical computers are, in fact, quantum computers?

The fact is that classical information processing can be a good approximation to reality at the macroscopic scale, and that sometimes the high level of detail that it offers is sufficient for everyday purposes. In fact it's not unlikely; had we not have been near the quantum limit now, where we are forced to start looking at computing with individual atoms, perhaps there would not have been even the same degree of motivation behind researching into quantum computers and the underlying quantum information theory.

Quantum computation, as it is, is an extremely exciting and rapidly growing field of investigation. An increasing number of researchers, with a whole spectrum of different backgrounds, ranging from physics, via computing sciences and information theory to mathematics and philosophy, are involved in researching properties of quantum-based computation.

That the laws of classical physics lead us to completely different constraints on information processing than computation based on quantum mechanics, was first realized by an American physicist, Richard Feynman. Later and somewhat independently, this idea was extended significantly by his British colleague, David Deutsch. Both being students of the remarkable John Wheeler, whom we met in Chapter 1, it is perhaps not surprising that they were driven by the same question of the fundamental link between physics and computation.

Two of the most successful applications of quantum computing are in the factorization of large numbers and searching a large database. The first problem is important, as much of modern day cryptography is based on the difficulty of factoring large prime numbers (we will discuss this later), and the second problem is important because any problem in Nature can be reduced to a search for the correct answer amongst several (or a few million) incorrect answers. Searches are so ubiquitous that they range from you searching for a file on your computer to a plant searching for a molecule in order to convert the Sun's energy to useful work (we'll discuss this later, too).

So why does quantum mechanics help here? Why can't we do these with our normal everyday computers? Well the point is that, yes we can, and we do use our computers for these purposes, but as the size of the prime factor or list to be searched grows, it takes longer and longer to get an answer. Quantum physics helps with these kinds of problems, because unlike a conventional computer which checks each possibility one at a time, quantum physics allows us to check multiple possibilities simultaneously.

Enter another couple of illustrious employees of Bell Laboratories, Peter Shor and Lov Grover (to add to Claude Shannon, whom we met earlier). Whilst Shannon was looking at the optimization of messages sent over a telephone wire, Shor, in 1992, was looking in more detail at the security of these messages.

Security is important in many aspects of life. Just as you want your credit card details to be secure when you are paying for something, governments and various companies want their documents to be securely stored and unavailable to the public or other governments or companies. As we discussed in Chapter 8, secrecy in the modern world is based on the notion that something is ‘computationally secure', i.e. it is secure in the sense that to break the code would require an inordinate amount of computing time and power. For, example, it is very easy for computers to multiply two numbers. You can check it yourself. Take two one-hundred digit long numbers (they are huge, like for example the number 100000000000000 000000000000000000000000000000000000000000000 0000000000000000000000000000000000000000) and ask a computer to multiply them together. This, the computer will be able to execute in a split second, and you'll hardly notice that it's taken any time at all.

On the other hand, finding factors of a large number is very difficult. This is because there are simply many possibilities to explore. Imagine the 100. What are its factors? Two times 50 is equal to 100. But so is 4 times 25. Or 5 times 20, or 10 times 10. The number of factors grows quickly and finding all of them presents a great difficulty for any current (classical) computer (it's exponentially slower than multiplying numbers in the first place).

How is it that a quantum computer can factorize efficiently? The explanation, first presented by Shor and now known as Shor's algorithm, is that a quantum computer, by exploiting the quantum principle of superpositions, can exist in many different states at the same time. Imagine a single computer in a superposition of being in many different spatial locations at the same time. In each of those locations you can configure the machine to divide your number by a different number to search for factors. And this is a massive, stupendous speed-up, since one quantum computer is now simultaneously performing all these divisions, one in each different spatial location. And, if one of them is successful – we have our factors!

Have you ever wondered why your PIN (personal identification number) is secure when you withdraw money from an ATM machine (automatic teller)? How come that neither the bank staff nor the bank managed know your PIN? Why do they not obtain it when you type it into the ATM and steal your money?

The reason is that the ATM machine performs the following operation. When you type in your PIN with the intention of withdrawing the money, this (usually a four to six digit number) gets multiplied by a huge (say a 500 digit) number. The resulting number (a number 504 digits long) is than checked by the bank. And if it is in the database, you will be allowed to proceed with your transaction.

But, and this is the crucial but, the bank cannot figure out your PIN from the 504-digit long number that they have in their database. It would simply take them a very long time – longer than the age of the Universe with current computers!

The punch-line of all this is that, using a quantum computer, we can factorize numbers very quickly. If we have a quantum computer with 10,000 quantum bits, we could factor a 500-digit number in a few seconds. And that would be the end of most current security!

Lov Grover, on the other hand, in 1996, was interested in an altogether different problem. Grover wanted to know how to design an efficient search algorithm using the mass parallelism offered by a quantum computer. His idea can be explained through the following example: suppose that someone gives you access to a library containing a lot of unsorted books. If you want to find a particular book, then you simply have to search through all the books until you find the one you are looking for. If there are a million books to go through and, if it takes a second to check each book, that could take a long time indeed (one million seconds is equal to about two weeks)! A quantum computer could speed things up greatly and would only take a thousand seconds (instead of a million) – which is about a couple of hours – and this is what Grover managed to prove.

In a list with four entries (two bits of information labelled 00, 01, 10, 11) we would normally require a maximum of three searches to find the right one. This is because you would have to look at each of the elements and, if you are unlucky, the first three elements will not be the ones you are looking for. Quantum search can, on the other hand, search a four-element quantum database in only one step. As the size of the database increases so does the quantum advantage.

Searching a database of four elements and finding the one that we want is similar to tossing two coins and observing the result of both. The first coin toss would correspond to asking which half of the database the desired element is in (i.e. is it in the top half or the bottom half), and the second coin toss would then give you the exact desired element (i.e. of the two elements left, is it one element or the other). It is an inescapable conclusion that in classical physics (hence classical computing) you would need a minimum of two coin tosses or two steps to uniquely distinguish between four outcomes.

Using quantum computers, however, we can do this with half the effort, in only one step. This quantum computation is analogous to the example of a single photon going through two beam-splitters. There we also had four different possibilities (RR, PR, RP, PP), but we only needed a single photon to generate a definite single outcome. The quantum property of superposition allows one photon to explore four different possibilities at the same time, and ultimately, through interference of the different paths, will compress them into a definite single outcome (i.e. the element we are searching for). This logic can be generalized so that a quantum computer could be designed to scan any number of database elements much faster than a classical computer.

The fact that the search problem is one of the problems in which quantum computers offer a speed-up is particularly interesting given that nearly any problem can be phrased in terms of a search algorithm. For example, even if we consider factorization, this can be rephrased in terms of a search algorithm in the sense that we are searching through all possible factors that would give us the desired answer. In this case there may be more than one answer, but conceptually the problem is the same. Also, the factorization example is a good one, as in this case the search algorithm is proven to be not as efficient as Shor's algorithm. This is as expected. The search algorithm is a general algorithm and is applicable for any search problem, whereas Shor's factorization algorithm is specifically geared for the problem of factorization and does so using hidden properties related to the structure of the problem. Therefore, to put things into context, whilst quantum computation does offer a significantly more powerful computational model than classical computation, it is not implausible that there are classical problems that can still be more efficiently solved with a classical algorithm than with the general quantum search algorithm.

The main limitation of quantum computation geared towards solving classical problems is that we ultimately have to make a measurement in order to extract the answer, given that the question we are asking requires a definite answer. Whilst this measurement is necessary, it is an intrinsically probabilistic process and there is always a finite probability that our answer may be wrong. In some cases, such as Shor's algorithm, it is straightforward to classically verify whether the answer is correct, and if it's not we run the quantum computer again until we have success. In others we need to find more creative solutions. The reader need not get too distracted with this limitation as it's not a major obstacle to quantum computing in practice. A far more serious inefficiency is the effect of environmental noise which is, in practice, very difficult to control. Any quantum computation that wants to be more efficient than its classical counterpart has to be able to deal with both of these issues.

In addition to the factorizing and searching quantum algorithms there are a host of other more specialized problems that quantum computers could do significantly better than their classical counterparts. However, probably the most fascinating application of a quantum computer lies in simulating complex physical systems. Some systems are so complex, our atmosphere for example, that they are extremely difficult to simulate using present computers and take an enormous amount of time. In fact, even far simpler systems, such as simulating a physical system with 20 atoms, are already extremely difficult for a normal computer. At the same time these problems are very important to us and we would like answers within our lifetime. Of course, we simulate these problems today on normal computers, but we are unable to simulate them in their entirety and compromise by simulating only a few key features in order to get an answer within a reasonable period of time. We'd all like better predictions of climate, not just day by day, but also in the long run. Being able to predict the climate more accurately is not only important to make our lives more pleasant; it could be crucial for our survival on Earth. And for this, we definitely need better understanding of the evolution of various weather patterns.

Simulating other systems with quantum computers is a subject in its infancy. It lies in such uncharted territory that we don't even know any of its borders or limitations. I personally think that this area will explode in the future, but its real power is difficult to fully grasp at this stage.

Interestingly for engineers and computer scientists, all this quantum weirdness, far from being a hindrance, can be utilized for technological purposes to construct quantum computers that fundamentally use this weirdness to run much faster than any current computer can. Thinking of computation as a process that maximizes mutual information between the output and the input – i.e. the question being asked, we can think of the speed of computation as the rate of establishing mutual information, i.e. the rate of build up of correlations between the output and the input. Furthermore the fact that qubits offer a higher degree of mutual information than is possible with bits, directly translates into the quantum speed-up that we see in Shor's and Grover's algorithms.

The good news is that small-scale quantum computers have even already been experimentally realized. These quantum computers, although operating on a very limited basis, have still been successful in demonstrating a degree of speed-up beyond anything possible with classical computers.

In terms of the make up of quantum computers, qubits could be encoded in atoms, subatomic particles, many-atom clusters, in light, or indeed in some combination of these. However, none of these at present offer a medium to store, say, 1000 qubits in a superposition state, for long enough to assist with more complex calculations.

How far away are we from fully fledged quantum computers? By this, I mean how far are we from an implementation that can hold thousands or millions of qubits in a superposition? In short, the answer is quite far; the current record (depending on how you view it) is somewhere between 10 and 15 qubits. However, there are many ways of encoding information quantum mechanically simply because there are many different systems that could be used to encode quantum information, e.g. ions in an ion trap, photons in a cavity, free photons, nuclear spins in nuclear magnetic resonance, electron spins in electroparamagnetic resonance, and a whole host of solid state devices (such as superconductors). We are not short of candidates for implementation!

Experimental physicists these days have an almost perfect control of atoms. They can engineer all sort of things, such as isolating a single atom inside a very small trap (on the order of a million times smaller than a metre). How do they know that a single atom is sitting there? They know, because they can shine some laser light into this small area and if the laser light is reflected inside, this then allows them to see this atom.

So what can we perform with 10–15 qubits?. Not much that our existing computers cannot do. We can, and we have, multiplied two numbers, 3 and 5 to obtain 15. So that's a start! Anyone can of course do that, but the significance of these kinds of experiments is to show that this can be done at the quantum level, which is a whole new game. Conventional computers currently need some 10,000 atoms to achieve multiplication of 3 and 5. So, quantum computers are in this sense more efficient. What is a shame is that no current quantum technology knows how to compute with anything more than 15 qubits.

The question is: why is it difficult to scale up quantum computers? The answer to this question is the same as to the question we asked in Chapter 8, i.e. why don't we see quantum effects at the macroscopic level? The difficulty, simply stated, is that we need large systems to be in many different states at the same time in order that they demonstrate quantum behaviour. But, the larger the system, the more ways there are for the particular information about the state to leak out into the environment. And as soon as any information leaks out, superpositions, and with them quantum computers, are destroyed. The process of information leaking out can also be considered as the environment (i.e. what is outside of the system) performing a measurement to gather information about the state of the system. As we know from our discussion on cryptography this inevitably damages the quantum state in question. This process is known in technical parlance as decoherence. So basically, it is difficult to make large-scale quantum computers for the same reason that we don't see people in multiple places at the same time (unless after a few drinks).

An intriguing analogy here is with crime. Statistics indicate that most successful robbers are those who operate by themselves (women apparently do this more frequently than men and are therefore much more successful robbers). The point to this is that the more people you have in your gang, the bigger the chances that one of them will betray you for whatever reason. It makes intuitive sense somehow that the more people that possess the same information, the higher the probability that this information will get out. Well, you can think that it is exactly the same principle as with atoms – the more atoms there are in a superposition, the harder it is to stop one of them decohering to the environment.

This all sounds like bad news for quantum computers. Is it going to be impossible to make reliable large-scale quantum computers? The answer fortunately is ‘no'. Unlike the perfect crime, we can in fact have perfect quantum computers. How is this? The trick to achieve this is the same that makes DNA replication faithful, or at least faithful enough for life to propagate. The solution is redundancy!

If you want to have 100 useful quantum bits in your computer, then you have to build a 1000-qubit large quantum computer. This means that for every one qubit, you have an additional nine copies of that qubit, so, if the occasional one decoheres, you can still make a majority decision over the remaining nine. Quantum superpositions can thus be protected, and whilst there are more optimal ways of adding redundancy, this in essence is the key concept.

As I write these lines (summer 2008) we are already moving towards producing quantum computational microchips. Furthermore, this is happening right now and right here in Singapore (I say this as I am sitting down and sipping a double espresso in Spinelli's on the National University campus). On these microchips, experimental physicists are trying to integrate components involving super-cold atoms and coherent photons in small numbers. Micro-engineering has progressed so much in the last 20 years that it is amazing to see how much stuff can be packed onto a very small area of a two-dimensional chip. Making a fully quantum computational unit can easily take some 5–10 years to complete, but so much ingenuity has gone into the research here that the possibility of large quantum computers is a very real prospect!

As with living systems, the battle to build a quantum computer is ultimately a battle against entropy. The lower the overall entropy of an arbitrary physical system the higher the chances that its constituent atoms may be entangled. Typical atoms useful for quantum computation usually need to be at a temperature close to absolute zero (around 1 billionth of a kelvin). Furthermore, given that the temperature in the rest of the laboratory is 300 billion times higher than that, it's a constant battle. This is a kind of Maxwell's demon scenario, where a process needs to reduce the entropy of the system in order to get some useful information processing done.

A striking piece of evidence to show how quantum effects can be seen in some macroscopic objects was demonstrated by Syantani Ghosh and her colleagues in 2003. Ghosh showed that quantum superpositions between many atoms exist in a piece of salt involving billions of atoms and at temperatures of a few millikelvin. This was a huge shock because it showed that quantum phenomena, whose power was thought to be confined to the infinitesimal world of subatomic particles, can produce effects that remain measurable on macroscopic scales.

This discovery was so momentous, it was difficult for anyone to believe. In a paper I submitted in 2000 to Nature, the premier scientific journal, I made similar predictions and was duly laughed off the court. The fact that the prediction has now been borne out by Ghosh's experiment catapults the mystery of quantum information into the wider arena. Nature kindly sent me Ghosh's paper as they thought I would be pleased to know that one of my predictions turned out to be correct (it doesn't happen too often). Even better still, since Ghosh's results, a number of other results have demonstrated similar effects in other materials, some of them being at much higher temperatures than this (even, startlingly, at room temperature!).

We are now realizing that advanced quantum effects are much more ubiquitous in macroscopic systems and this gives us hope that one day we may find that Nature has already provided us with a quantum computer and all that is left for us to do is to program it. After all, Nature has already invented many tricks before us humans. Radar and error correction by redundancy are just two out of many such tricks used by living systems. Might it therefore be that somewhere there is a living system which harnesses the speed-up advantages of quantum computation? Even better, perhaps quantum computation is so ubiquitous that it takes place in every living cell.

There is continuing evidence that more and more natural processes must be based on quantum principles in order to function as they do. For example, we consider the process of photosynthesis, which is one of the key natural processes for maintaining life on Earth.

The reader will recall from Chapter 5 that all living beings are like thermodynamical engines similar to Maxwell's demons, whose crucial task is to battle the natural tendency to increase disorder. Life does that by absorbing highly disordered energy coming from the Sun and converting it to a more ordered and useful form. Photosynthesis is the name of the mechanism by which plants absorb, store, and use this light energy from the Sun. This energy is converted to an ordered form and used for the functioning of the cells. Recent fascinating experiments by Graham Fleming and his group at the University of Berkeley, California, suggest that quantum effects do matter in photosynthesis. Furthermore, they point out a close connection between the photosynthetic energy transfer and Grover's optimal quantum search algorithm. In other words, plants are so much more efficient than what we expected that maybe there is some underlying quantum information processing contributing. Biological plant efficiency is super-high, around 98% of radiation that hits the leaf does get stored efficiently. The best man-made photocells, on the other hand, can barely achieve a 20% efficiency. So there is an enormous difference; how do plants do it?

The complete answer is not entirely clear but the overall picture is this. When sunlight hits a surface that is not designed to carefully absorb and store it, the energy is usually dissipated to heat within the surface, or reflected. Either way, it is lost as far as any subsequent useful work is concerned. The dissipation within the surface happens because each atom in the surface acts independently of other atoms. When radiation is absorbed in this incoherent way, then all its useful properties vanish. What is needed is for the atoms and molecules in the surface to act in unison. And this is a feat that all green plants manage to achieve.

In order to understand how this happens, it is helpful to think of each molecule in a plant as a database element in Grover's search algorithm. All molecules vibrate as they interact with one another. When they are hit by light, they change their vibration and dynamics and what ensues implements Grover's dynamics with the energy ending up in the most stable configuration at the end (and this configuration is the database element that Grover's algorithm is meant to identify).

Admittedly, Fleming's experiments have been performed at low temperature (77 kelvin, while plants normally operate at 300 kelvin). Therefore, it is not entirely clear if any quantum effects can survive at the higher temperature. However, even the fact that there exists a real possibility that quantum computation has been implemented by living systems is a very exciting and growing area of research.

But things could be even grander. The most fascinating suggestion of all is that quantum theory may be necessary in the very basis of life itself. You will remember that in Chapter 4 I said that the information to replicate life is encoded into four different elements, which are just molecules labelled by A, C, T, and G. If we think of this as a very simple database, with four records, the task of a DNA replicator computer is to scan an arbitrary DNA strand and match the correct record from the database to each of the molecules. The database logic is that A is always paired with T, and C is always paired with G. This simulates the replication process in our cells, as each molecule on one DNA strand finds its companion on the new strand. In this way we can consider DNA replication analogous to a four-element database search problem.

An Indian physicist called Arvind asked the question in the late 1990s as to why Nature uses two bits (four molecules) to encode life. Wouldn't it be simpler just to use one bit (i.e. just two molecules)? This, as you may recall, was one of our big questions in Chapter 4. It seems odd to use two bits given that we know that everything can be done in terms of single bits and it seems intuitively simpler to use single bits, so why has Nature made the extra effort? Shouldn't Nature, starting from nothing, find it easier to stumble upon a singl-bit encoding, than a two-bit encoding? Arvind's answer is simple: It may be easier to come up with single bits, but there is a bigger quantum advantage in search when we have two quantum bits. With two quantum bits Grover's quantum search algorithm finds the solution in just one step. Therefore, if we optimize for the speed of replication, then two quantum bits allow for more efficient information processing than one classical bit in the same number of steps. So maybe this is what Nature was thinking.

Arvind's suggestion is very smart, but there is a crucial issue here: can DNA actually be a quantum computer? DNA is a macromolecule so it's not clear how this could be the case and how molecules could exist in many different states at the same time. Whether DNA is based on classical or quantum computing is, remarkably, not actually known. I say ‘remarkably' because DNA has been studied extensively for the last 60 years. We therefore have to be patient and leave this question open for the time being.

The picture that seems to be emerging is that larger and larger systems may be capable of exhibiting quantum effects under certain conditions. We are not sure, for example, if and how we can generalize this. Perhaps everything would exhibit quantum effects if we know how to look at them in the right way. So is it the case that any complex piece of matter or energy can potentially, under the right external conditions, be used as a quantum computer? If we take a step further and couple this to the Church–Turing thesis of the universal computing machine, what this could imply is that any piece of the Universe can simulate, in a more or less efficient manner, any other piece of the Universe. Perhaps even reality itself can be seen as the product of a complex multilayered quantum computation. This is, of course, a huge leap of faith but it will be the essence of our discussion in Chapter 12.

乘风破浪：超越极限的计算世界

谁没听说过计算机？在这个被电子设备密布的时代，除了几个与世隔绝的亚马逊丛林部落或喀拉哈里沙漠居民，几乎没有人能逃脱它们的影响。从管理财务、控制飞行，到加热食物、调节心跳（对某些植入设备的使用者），这些设备已渗透到社会生活的每一个角落。无论是个人电脑、大型主机，还是嵌入手机和微波炉的小型芯片，我们已经很难想象没有它们的世界。

「计算机」的概念远不止于普通的苹果 Mac 或 PC。从最基本的定义来看，计算机是指能够接收指令并根据指令执行运算的任何对象。在这个意义上，计算不仅限于机器或机械装置；原子物理现象和生物系统同样可以成为极其高效的计算载体（在许多情况下，它们的计算能力甚至远超我们当前的技术模型）。在本章后续内容中，我们将深入探讨这些另类的计算模式。

计算机以千奇百怪的外形存在，有些甚至让人根本想不到这是一台计算机（你会把冰箱想象成计算机吗？）。有些计算机能在转瞬间完成数百万次复杂运算，而另一些可能即使做最简单的计算也需要很长时间。然而，从计算理论的角度看，只要有正确的指令和充足的内存，任何一台计算机理论上都能完成另一台计算机能做的事情。打个比方，你家冰箱里的小型嵌入式计算机，完全可以模拟运行 Microsoft Windows 系统。虽然这听起来很荒谬，但重点并不在于实际应用，而是在于每台计算机都遵循相同的计算逻辑，理论上都有可能通过各种方式达成相同的计算目标。

在计算机科学的早期，数学家 Alan Turing 和 Alonzo Church 提出了一个划时代的理论 —— 丘奇 - 图灵命题（1936 年）。这个理论探讨了机械计算设备（如电子计算机）的基本运算能力。他们创立了算法的形式化定义，并提出了一种可以被所有现代计算机遵循的计算模型。这个理论的核心观点是：只要给定足够的时间和存储空间，任何可以想象的计算都可以通过算法实现。这一突破性进展奠定了通用计算机的理论基础，也是现代计算机科学的重要里程碑。

计算机技术微型化的发展历程早已引人注目。从冯·诺伊曼在 1940 年代制造第一台计算机开始，计算机就一直在不断缩小体积（同时也变得更快，因为电路距离越短，信号传输就越迅速）。在 1950 年代末，英特尔的董事长兼联合创始人戈登·摩尔发现了一个令人惊叹的规律：计算机的性能和存储能力大约每两年就会翻一番。这一观察被记录在他的报告中，后来人们将其称为「摩尔定律」。

有趣的是，摩尔定律为什么能在过去半个世纪中持续有效？这并非一个不变的自然规律，而更多地依赖于人类的技术创新和产业发展。一些科技评论家甚至认为，这更像是一个行业自我推动的趋势。作为英特尔的领导者，摩尔实际上为整个半导体产业设立了一个持续进步的标杆。由于英特尔在微芯片领域的领导地位，这个「定律」某种程度上已经成为了技术进步的一种自我实现的路径。

如果技术持续遵循摩尔定律，芯片上的电路元件将不断微型化，最终可能缩小到只有几个原子大小。到那时，我们将面临什么挑战？计算机还能进一步缩小和加快吗？

显然，这种指数级增长必然存在自然极限。当前，我们需要约 100 个电子来存储一个二进制信息（bit）。但在未来 10 年内，我们可能只需要一个电子就能存储同样的信息。我们还能继续突破这个极限吗？

物理学告诉我们一个重要道理：不要对科学结论过于武断。历史上有太多看似不可能的预言最终被推翻，就像凯尔文勋爵曾断言重于空气的机器不可能飞行，然而仅 30 年后，赖特兄弟就用实际行动证明了他的错误。即便我们找到了计算的终极极限，关于这个极限能维持多久，科学家们仍充满好奇与期待。

要真正理解计算机的极限，我们必须先搞清楚计算机的本质。其实很简单：计算机就是处理比特的机器。当前的计算机使用布尔逻辑定律来移动、转换和重新排列二进制数据（即零和一）。早在 1854 年，George Boole 就发表了布尔代数，为计算过程提供了数学建模的完整系统。Shannon 后来在通信理论中广泛应用了这一理论。

目前，布尔逻辑主要通过晶体管实现，但未来可能会出现多种替代技术。传统计算机中，比特只能处于两种状态之一 —— 零或一。而在量子世界里，情况变得更加有趣。量子力学允许一个系统同时存在零和一两种状态，这就是量子比特（qubit）的神奇之处。

与传统比特不同，量子比特可以在零和一之间存在无限多的中间状态。科学家们可以精确调整这些状态出现的概率，就像调音盘一样微调声音。只有当我们确定地观测到零或一时，量子比特才会表现得像传统计算机中的经典比特。

随着技术不断微缩，在原子尺度上，控制晶体管电路行为的物理定律已经从经典物理转向量子力学。基于半导体技术的晶体管电路，其本质特性完全由量子力学原理决定。因此，探索基于量子物理原理的新型计算机，不再是一种勉强的设想，而是技术发展的必然趋势。

值得关注的是，晶体管作为计算机的基本「神经元」，其工作原理依赖于半导体独特的量子特性。半导体的功能机制完全无法用传统的经典物理学解释，只能通过量子力学来阐释。这是否意味着经典物理学已经无法充分解释现代计算机的运行机制？换句话说，我们是否可以说，看似传统的计算机其实已经在某种程度上体现了量子计算的影子？

经典信息处理在宏观世界中能够相当准确地模拟现实，其细致入微的描述方法常常足以满足日常需求。实际上，如果我们没有迫近量子计算的边界 —— 需要开始研究以单个原子进行计算，可能对量子计算机和量子信息理论的研究热情也不会如此强烈。

量子计算是一个令人振奋且迅速发展的前沿领域。越来越多来自不同学科的研究者 —— 从物理学家、计算机科学家、信息理论专家，到数学家和哲学家 —— 都投入到探索量子计算的奇妙特性中。

经典物理学和量子力学在信息处理上的约束有着天壤之别，这一重大发现最早是由美国著名物理学家理查德·费曼提出的。随后，他的英国同事大卫·多伊奇在某种程度上独立地对这一思想进行了深入拓展。作为杰出物理学家约翰·惠勒的学生，两人都专注于探索物理学与计算之间的本质联系，这种学术追求似乎早已注定。

量子计算在两个领域展现出卓越的应用：大数因数分解和海量数据库搜索。第一个问题至关重要，因为现代密码学的安全性正是建立在大素数因数分解的复杂性之上（我们稍后会详细阐述）。第二个问题同样意义重大，因为自然界的诸多问题本质上都可以归结为在众多错误答案中寻找唯一正确答案的过程。搜索无处不在：从你在电脑上寻找文件，到植物搜寻分子以将太阳能转化为可用能量，无不如此。

为什么量子力学能在这些问题上提供帮助？为什么传统计算机无法胜任？事实上，传统计算机确实可以执行这些任务，但随着搜索规模的增大，计算时间会呈指数级增长。量子物理的独特之处在于，它不像传统计算机那样逐一检查每种可能性，而是能够同时并行地探索多种可能性。

在贝尔实验室，还有两位同样出类拔萃的科学家值得我们认识：Peter Shor 和 Lov Grover，他们与我们之前提到的 Claude Shannon 一脉相承。Shannon 当年致力于优化电话线传输的消息，而 Shor 则在 1992 年更进一步，深入研究了这些通信消息的安全性问题。

安全性在现代社会中扮演着至关重要的角色。就像个人希望在网上交易时保护信用卡信息一样，政府和企业也同样重视文件和数据的安全保护。在信息安全领域，我们通常使用「计算安全性」概念，意味着破解某个加密系统的成本和复杂度极高，以至于在实际操作中几乎不可能。

举个生动的例子，现代计算机在处理大数字运算时极其迅速。想象两个各有 100 位数字的超大数值相乘，对于计算机而言，这几乎是瞬间完成的任务。然而，反向操作 —— 将这个巨大的乘积分解为原始因子 —— 却可能需要数千年的计算时间，这正是计算安全性的关键所在。

在数学计算中，分解大数的因数是一个极其复杂的任务。想象数字 100，它有多种因数组合：2 乘 50、4 乘 25、5 乘 20、10 乘 10。随着数字变大，可能的因数组合呈指数级增长，这使得传统计算机在因数分解过程中变得极其缓慢。

量子计算机如何克服这一困难？这要归功于 Shor 提出的量子因数分解算法。量子计算的独特之处在于量子叠加原理（Quantum Superposition），它允许计算机同时存在于多个状态。简单来说，就像一台计算机能同时「存在」于多个空间位置，每个位置都在尝试用不同的数字去除目标数字，寻找其因数。

这种并行计算方式带来了革命性的计算速度提升。传统计算机需要逐一尝试，而量子计算机可以同时进行海量的计算，大大缩短了因数分解的时间。当其中一个计算路径成功找到因数时，问题即告解决。

你是否曾好奇，在自动取款机（ATM）取钱时，你的个人识别码（PIN）是如何保持安全的？为什么银行工作人员和管理者无法获知你的 PIN？为什么他们在你输入 PIN 时无法窃取你的资金？

这背后的机制非常巧妙。当你输入 PIN 准备取款时，这个通常 4 到 6 位的数字会与一个庞大的（约 500 位）数字相乘。乘积会生成一个 504 位长的数字，这个数字会被银行系统验证。只有当这个数字在银行的数据库中匹配时，交易才会被批准。

关键之处在于，银行无法从这个 504 位的数字反推你的原始 PIN。用传统计算机进行这样的计算，所需时间将远远超过宇宙的年龄！这种单向加密技术确保了 PIN 的安全性。

然而，量子计算（Quantum Computing）可能会彻底改变这一现状。如果我们拥有一台拥有 10,000 个量子比特（Quantum Bits）的量子计算机，那么对 500 位数字进行因数分解可能只需要几秒钟。这意味着当前的加密安全机制可能面临前所未有的挑战。

1996 年，Lov Grover 关注了一个与众不同的科学难题：如何利用量子计算机超强的并行计算能力，设计一种高效的搜索算法。他用一个生动的例子来解释这个想法：想象你获得了一个装满未分类书籍的图书馆的访问权。要找到一本特定的书，你必须挨个翻阅每一本书，直到找到你想要的那本。如果图书馆里有一百万本书，每本书检查需要一秒钟，那么这个过程将会异常漫长 —— 大约需要两周时间！而量子计算机可以极大地缩短这个搜索过程，将搜索时间从一百万秒缩减到仅仅一千秒，也就是几个小时。这正是 Grover 成功证明的惊人成果。

在一个包含四个条目的信息列表中（使用 00、01、10、11 表示的二进制信息），传统搜索通常需要最多三次查找才能定位目标。这是因为必须逐一检查每个元素，而在最坏的情况下，前三个元素都不是我们要找的。相比之下，量子搜索可以在单一步骤中快速定位四元素量子数据库中的目标。随着数据库规模扩大，量子搜索的优势也会逐渐增强。

搜索四元素数据库的过程，可以类比为掷两枚硬币并观察结果。第一次掷硬币相当于确定目标元素位于数据库的上半部分还是下半部分，第二次掷硬币则精确定位具体的目标元素。在经典物理学和传统计算模型中，要唯一确定四种可能结果，必然需要至少两次硬币投掷或两个搜索步骤。这凸显了传统计算与量子计算在搜索效率上的根本差异。

量子计算机展现了惊人的计算能力，能够以传统计算机一半的工作量，仅用一个步骤就完成复杂的搜索任务。这就像一个神奇的光子穿越双重光路时的奇特旅程：明明有四种可能的路径，但通过量子世界特有的「叠加」魔法，这个光子可以同时探索所有路径。

想象一下，传统计算就像是一个人一步步尝试每条路径，而量子计算就像是可以瞬间分身，并行地探索所有可能。最终，这些可能性会通过量子干涉神奇地「收敛」，精准地指向我们要找的目标。这种独特的计算方式意味着量子计算机可以比传统计算机快速得多地扫描海量数据，为复杂的搜索和计算问题提供革命性的解决方案。

搜索问题是量子计算机能提供显著加速的问题之一，这一特点尤其引人注目，因为几乎所有问题都可以转化为搜索算法。举例来说，即便是因数分解问题，也可以重新定义为一种搜索过程 —— 即在所有可能的因子中寻找能得到期望答案的组合。这种情况下可能存在多个答案，但问题的本质是相同的。

以因数分解为例特别有意义，因为在这个案例中，通用的量子搜索算法并不如专门的 Shor 算法高效。这一点并不令人意外。搜索算法是一种通用方法，可适用于任何搜索问题；而 Shor 算法则是为因数分解问题定制的，并利用了问题本身的特定结构特征。

为了更好地理解这一点，我们需要认识到：尽管量子计算提供了比经典计算更强大的计算模型，但并非所有问题都能从中获得显著收益。在某些情况下，传统的经典算法可能仍然是更高效的解决方案。

量子计算解决经典问题面临的主要挑战是，我们必须通过测量来获取最终答案，而测量过程本身具有固有的不确定性。这意味着每次测量都存在一定概率得到错误的结果。在 Shor 算法等场景中，我们可以轻松地用传统计算方法验证结果的准确性，如果发现不正确，就重新运行量子计算机直到获得正确答案。但在某些更复杂的情况下，研究人员需要寻找更富有创造性的解决方案。

不过，读者无需过分担心这一测量的不确定性，因为它并不构成量子计算的根本障碍。实际上，量子计算面临的更严峻挑战是如何控制环境噪声。任何希望超越传统计算效率的量子计算方案，都必须同时应对测量不确定性和环境噪声这两大技术难题。

除了分解和搜索量子算法外，量子计算机还能在众多专业领域展现出显著优势。其中最令人着迷的应用，可能要数模拟极其复杂的物理系统。比如我们的大气系统（由无数气象因素相互作用形成），用传统计算机模拟就极其困难，不仅计算时间长，还很难还原系统的真实复杂性。事实上，即便是一个只有 20 个原子的物理系统，对普通计算机来说也是一个巨大的挑战。

这些看似遥远的科学难题，实际上与我们的日常生活息息相关。我们迫切希望在有生之年获得准确的答案。目前，科学家只能在普通计算机上进行有限的模拟，通常只能捕捉系统的几个关键特征，而无法全面还原系统的真实运行机制。

准确预测气候变化不仅关乎我们的生活质量，更可能事关人类在地球上的生存。要实现这一目标，我们需要更深入地理解各种天气模式的演变规律。量子计算有望在这一领域为我们提供前所未有的洞察力。

用量子计算机模拟其他系统是一个新兴的研究领域。目前，这个领域还处于如此未知的状态，以至于我们甚至无法确定其边界和局限性。我个人相信这个领域将来会出现爆发性增长，但现阶段其真正的潜力还难以完全理解。

对于工程师和计算机科学家来说，量子系统中那些看似奇特的特性（量子奇异性），并非阻碍，反而可以被巧妙地应用于技术创新。这些特性可以用来构建量子计算机，通过利用量子世界的独特规律，使计算速度远远超越传统计算机。

如果我们将计算视为一个信息传递的过程，可以用输出和输入（即被询问的问题）之间的互信息（mutual information）来衡量。那么计算的速度，实际上就是建立这种互信息的速率，或者说是输出和输入之间关联程度的建立速率。更为关键的是，量子比特（qubits）能够提供比传统比特更高级别的互信息，这正是 Shor 和 Grover 算法中量子计算速度加速的根本原因。

好消息是，小规模的量子计算机已经在实验中成功实现。这些量子计算机虽然目前运行在非常有限的范围内，但已经成功展示了其计算速度远超传统经典计算机的潜力。

在量子计算机的构建中，量子比特（qubits）可以被编码在多种不同的物理系统中，包括单个原子、亚原子粒子、多原子簇、光子，甚至这些系统的混合形式。然而，当前的技术尚未找到能够稳定地将 1000 个量子比特保持在量子叠加状态的理想介质，这对于执行更复杂的量子计算至关重要。

我们距离完全成熟的量子计算机还有多远？更具体地说，距离能够在量子叠加态中保持成千上万或数百万个量子比特（qubits）还有多远？简单回答是：还很遥远。目前的记录（取决于统计方法）大约在 10 到 15 个量子比特之间。

不过，量子信息的编码方式十分丰富，这源于可用于量子信息存储的系统多种多样。这些系统包括：离子阱中的离子、腔体中的光子、自由光子、核磁共振中的核自旋、电子顺磁共振中的电子自旋，以及各类固态器件（如超导体）。科学家们拥有众多量子计算实现路径，只是尚未找到规模化的最佳方案。

现代实验物理学家已经能够近乎精确地控制原子。他们可以进行精密的微观工程，例如在极其微小的空间中（仅有一米的百万分之一大小）隔离单个原子。那么，他们如何确认这个区域内确实存在一个原子呢？答案是利用先进的激光探测技术：通过将激光束照射到这个微小区域，并观察光线的反射情况，科学家们就可以「看见」被隔离的原子。

量子计算的早期探索阶段能做些什么呢？目前使用 10-15 个量子比特（Qubits）能完成的计算并不多，基本上与传统计算机的能力相当。作为初步验证，科学家们已经成功地在量子计算机上完成了 3 乘 5 等基础运算。这看似微不足道，但其意义在于首次证明了在量子微观尺度上进行数学运算的可能性，这是传统计算技术的一个重大突破。

与传统计算机相比，量子计算机的优势初步显现：目前传统计算机需要约 10,000 个原子才能完成同样的乘法运算，而量子计算机在此方面显示出了更高的计算效率。然而，当前量子计算技术仍然面临着重大挑战 —— 目前尚未找到可靠的方法来处理超过 15 个量子比特的复杂计算。

为什么扩大量子计算机的规模如此困难？这个问题与我们此前探讨的「为什么我们无法在宏观世界观察到量子现象」本质上是一致的。

困难之处在于，要展示量子行为，我们需要大型系统能够同时存在于多个不同状态。但矛盾的是，系统越大，量子信息泄露到外部环境的可能性就越高。一旦量子信息「泄密」，量子系统中精妙的叠加状态（superpositions）就会立即崩溃，量子计算机也随之失效。

这个信息泄露的过程，本质上可以理解为外部环境在「窥探」系统的内部状态。就像一个好奇的侦探试图收集线索，环境通过各种微小的相互作用「测量」系统，而这种测量不可避免地会破坏脆弱的量子状态。科学家们称这一现象为「退相干」（decoherence）。

换个通俗的比喻，制造大规模量子计算机就像试图让一个人同时出现在多个地方 —— 听起来荒谬，但在量子世界中却是可能的。问题是，现实世界总是会不情不愿地将这种可能性「挤压」回单一状态。

这里有一个关于犯罪的有趣类比。统计数据显示，最成功的强盗往往是独自作案的人（有趣的是，女性似乎更擅长独自作案，因此犯罪成功率也更高）。其中的道理很简单：帮派成员越多，背叛的风险就越大。这就像是一个直觉上的判断：知道某个秘密的人越多，这个秘密被泄露的可能性就越高。这个原理看起来跟原子的量子行为惊人地相似 —— 处于叠加态（superposition）的原子越多，阻止它们与环境发生退相干（decoherence）就越困难。

听起来这简直是量子计算机的噩梦。那么，大规模可靠的量子计算机还有可能实现吗？值得庆幸的是，答案是肯定的。与不可能完成的完美犯罪不同，我们确实有希望制造出近乎完美的量子计算机。其中的秘诀，与 DNA 能够忠实地复制（或者说足以支持生命延续）的机制如出一辙 —— 那就是冗余！

如果你希望在量子计算机中获得 100 个可靠的量子比特，就需要构建一个包含 1000 个量子比特的大型量子计算机。这是因为对于每一个关键量子比特，还需要额外准备 9 个备份。当某个量子比特因为量子去相干（即量子态不稳定性）而失效时，系统仍然可以通过剩余的 9 个备份量子比特做出正确的计算判断。通过这种冗余设计，量子计算机可以有效地保护脆弱的量子叠加态。虽然还存在更先进的冗余方案，但这种方法体现了量子纠错的核心思想。

在 2008 年夏天写下这些文字时，我们已经在向量子计算微芯片的研发迈进。此刻，这项令人兴奋的技术正在新加坡如火如荼地进行（我正坐在国立大学校园的 Spinelli's 咖啡馆，一边品尝着浓郁的双份浓缩咖啡，一边见证着这一激动人心的时刻）。科学家们正在这些微芯片上尝试整合极低温原子和少量相干光子。过去 20 年间，微电子技术的进步令人惊叹 —— 科学家们能够在仅仅一个小小的二维芯片上集成如此多的精密元件。

虽然制造一个成熟的量子计算单元可能还需要 5-10 年的时间，但这里投入的智慧和创新已经让大型量子计算机从遥不可及变成了触手可及的现实！

构建量子计算机，犹如生命系统中的生存之战，本质上是与熵抗争的过程。在物理系统中，总熵越低，原子相互纠缠的可能性就越高。对于量子计算而言，有用的原子通常需要被冷却至接近绝对零度（约为十亿分之一开尔文）。更具挑战性的是，实验室其他区域的温度足足比这个极低温度高出 3000 亿倍，这意味着要维持如此低温，需要持续不断地「对抗」热量。这个过程颇似「麦克斯韦妖」—— 通过降低系统熵来实现信息处理的复杂机制。

2003 年，Syantani Ghosh 及其团队提供了一个令人惊叹的证据，展示了量子效应竟可能存在于宏观物体中。她的研究表明，在一块普通的盐晶体中，数十亿个原子可以在几毫开尔文的温度下，呈现出量子叠加状态。这一发现极大地冲击了科学界的认知：曾被认为仅限于亚原子微观世界的量子现象，实际上可以在宏观尺度上产生可观测的效果。

这项发现是如此惊人，以至于起初没有人敢相信。2000 年，我在世界顶级科学期刊《自然》上发表论文时提出了类似的预测，当时几乎遭到了同行的一致嘲笑。如今，Ghosh 的实验完美地验证了这一预测，不仅为量子信息研究带来了重大突破，也将这一神秘领域推向了科学的前沿。《自然》杂志特意将 Ghosh 的论文寄给了我，因为他们知道科学家最大的快乐莫过于看到自己的预言最终成真（这种机会可是难得得很）。更令人兴奋的是，继 Ghosh 的研究之后，陆续有科学家在不同材料中发现了类似的量子效应，其中一些研究甚至在极高温度下取得了突破，最让人瞠目结舌的是，这些现象竟然可以在常温下观测到！

近年来，科学家们惊喜地发现，量子世界的神奇现象远比我们想象的更加广泛地存在于宏观世界中。这一发现令人兴奋：或许自然界本身就是一台天生的量子计算机，我们人类要做的只是学会「解读」和「编程」。

自然界向来是最伟大的发明家。早在人类之前，它就已经熟练运用了许多令人惊叹的「绝技」，比如生物系统中的雷达定位和冗余纠错机制。那么，是否可能存在某些生命系统已经巧妙地利用了量子计算的超高速计算能力？更令人兴奋的是，量子计算可能已经深入到每一个微小的生命细胞中。

越来越多的科学证据表明，许多自然过程必须依靠量子力学原理才能维持其奇妙的运转。以光合作用为例，这一地球生命维持系统中的关键过程，其高效能量转换机制可能正是量子世界魔法的又一个绝佳证明。

读者可能还记得第 5 章的内容：所有生命都如同麦克斯韦妖设想的热力学引擎，其核心使命是抵抗自然世界走向混沌的趋势。生命通过一种巧妙的方式实现这一点 —— 吸收来自太阳的高度无序能量，并将其转化为更有序、更可用的形式。

光合作用就是植物吸收、储存和利用太阳光能的关键机制。在这个过程中，能量被精妙地转换为有序形式，并为细胞的运转提供动力。加州大学伯克利分校的 Graham Fleming 及其团队最近开展的令人惊叹的研究发现，量子效应在光合作用中扮演着远比人们想象更重要的角色。

更令人兴奋的是，研究人员发现光合能量转移与 Grover 最优量子搜索算法之间存在惊人的相似性。这意味着植物可能在进行某种复杂的量子信息处理，这解释了它们令人难以置信的高效率。事实上，植物光合作用的生物效率高达惊人的 98% —— 意味着落在叶子上的几乎所有太阳辐射都能被高效捕获和利用。相比之下，人类制造的太阳能电池板的效率仅仅徘徊在 20% 左右。

这种巨大的效率差异究竟源于何处？植物究竟是如何在量子尺度上如此精妙地利用能量的？这正是科学家们持续研究的迷人问题。

自然界中，能量的转换往往并不像我们期望的那样高效。想象一下，当阳光照射到普通表面时，大部分能量要么被转化为无用的热量，要么直接被反射回去，就像是一场能量的白白浪费。这是因为普通材料中的原子各自为政，无法协同工作。

而植物却有着令人惊叹的能量转换本领。它们就像是精心设计的能量「搬运工」，能够让每个分子都步调一致，宛如参与一场精密编排的能量接力。这个过程颇为巧妙，科学家们将其比喻为量子计算中的 Grover 搜索算法（一种高效的搜索方法）。当光线照射到植物叶片时，分子们会改变振动方式，最终将能量精确地引导到最稳定的状态，就像找到了最优解。

这种看似神奇的能量转换，正是植物生存和光合作用的关键所在。

诚然，Fleming 的实验是在低温（77 开尔文）下进行的，而植物通常在 300 开尔文的环境中运作。因此，目前尚不清楚量子效应是否能在更高温度下保持其特性。不过，即便仅仅是存在生物系统可能已实施量子计算的可能性，这也是一个极其前沿且充满潜力的研究方向，有望为理解生命系统的深层运作机制提供全新的视角。

但生命的奥秘可能远比我们想象的更加深奥。最令人着迷的观点是：量子理论可能是生命本质的关键。还记得第 4 章我提到的吗？复制生命的信息被编码在四种特定的分子中 —— 它们分别标记为 A、C、T 和 G。我们可以将这看作一个极其简单的数据库，包含四条记录。DNA 复制计算机的任务就是扫描任意 DNA 链，并为每个分子在数据库中找到其对应的配对。其逻辑很简单：A 总是与 T 配对，C 总是与 G 配对。这正是我们细胞内部复制过程的写照 —— 每个 DNA 链上的分子都会在新链上找到它的「伴侣」。换句话说，DNA 复制本质上是一个四元素的数据库搜索过程。

在 1990 年代末，一位印度物理学家 Arvind 提出了一个颇具洞察力的问题：生命为何要用两个比特（四种分子）来编码，而不是仅仅使用一个比特（两种分子）？这个问题在我们之前的讨论中曾经引起过广泛的思考。从直觉上看，既然我们知道所有信息都可以用单比特表示，那么使用两个比特似乎显得多余。自然在创造生命的过程中，难道不应该更倾向于发现最简单的编码方式吗？

Arvind 给出了一个令人惊讶的解释。虽然单比特编码看起来更简单，但在量子计算领域，两个量子比特实际具有惊人的优势。以 Grover 量子搜索算法为例，两个量子比特可以在单个步骤中找到解决方案，这意味着在相同的计算步骤中，两个量子比特的信息处理效率远高于传统的单比特。

换句话说，自然可能在信息处理的效率上做出了精妙的选择。这不仅仅是偶然，而是一种近乎智慧的优化策略。生命似乎已经找到了一种看似复杂但实际上更快速、更高效的信息编码方式。

Arvind 的建议非常巧妙，但这里存在一个关键性问题：DNA 真的能成为量子计算机吗？作为一种大分子，DNA 能否同时存在于多种不同状态，目前还不清楚。令人惊讶的是，尽管 DNA 已被科学家深入研究了 60 多年，但它究竟是基于经典计算还是量子计算仍然是个未解之谜。在这个问题上，我们还需要保持开放和耐心的态度，继续探索和研究。

随着研究的深入，一个有趣的图景正在浮现：在特定条件下，规模越大的系统越可能呈现量子效应。我们尚不确定如何推广这一发现。也许只要我们用正确的视角观察，一切事物都能展现量子特性。

这引发了一个有趣的问题：在合适的外部条件下，是否任何复杂的物质或能量都可能被用作量子计算机？如果将这一思路与丘奇-图灵论点（关于通用计算机的经典理论）相结合，我们可能会得出更惊人的结论：宇宙的每一个部分都能够或多或少地模拟宇宙的其他部分。更为大胆的是，现实本身可能就是一个复杂的多层量子计算过程。

当然，这是一个极具想象力的假设，我们将在第 12 章详细探讨这一观点。

### Key points

Quantum computers force a higher order of information processing than we can currently achieve. They are the smallest and fastest gadgets that the laws of physics currently allow us to construct.

They can solve some important problems for us that conventional computers cannot. Two instances are the factorization problem and the search problem. The former is used in various security protocols, the latter in many optimization techniques.

Quantum computers are not a distant dream. They are being built at present in many laboratories in the world.

Quantum effects are experimentally being seen in macroscopic objects such as pieces of solids and organic molecules in living systems.

关键要点：

量子计算机代表了一种超越当前计算能力的信息处理范式。它们是物理定律允许我们构建的最为精巧和高效的计算装置。

量子计算机能够解决传统计算机束手无策的重要问题。其中两个典型例子是因数分解问题（在密码学安全协议中广泛应用）和搜索问题（在多种优化技术中至关重要）。

量子计算机已经不再是遥不可及的科幻概念，而是正在世界各地的实验室中逐步变为现实。

科学家们已经开始在宏观尺度上观测量子效应，这些效应出现在固体材料和生物系统的有机分子中，为量子技术的发展提供了令人兴奋的可能性。