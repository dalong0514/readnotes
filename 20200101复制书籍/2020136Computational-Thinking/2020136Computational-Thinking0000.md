Computational Thinking

Peter J. Denning and Matti Tedre

The MIT Press | Cambridge, Massachusetts | London, England

© 2019 The Massachusetts Institute of Technology

## Series Foreword

The MIT Press Essential Knowledge series offers accessible, concise, beautifully produced pocket-size books on topics of current interest. Written by leading thinkers, the books in this series deliver expert overviews of subjects that range from the cultural and the historical to the scientific and the technical.

In today’s era of instant information gratification, we have ready access to opinions, rationalizations, and superficial descriptions. Much harder to come by is the foundational knowledge that informs a principled understanding of the world. Essential Knowledge books fill that need. Synthesizing specialized subject matter for nonspecialists and engaging critical topics through fundamentals, each of these compact volumes offers readers a point of access to complex ideas.

2-3『

找了下该系列的书籍：[The MIT Press Essential Knowledge series | The MIT Press](https://mitpress.mit.edu/books/series/mit-press-essential-knowledge-series)，有时间好好刷选一下，作为一个好书单。

随意翻了下，看到一本合胃口的书，已下载书籍「2020137Algorithms」。（2020-12-31）

』—— 未完成

Bruce Tidor

Professor of Biological Engineering and Computer Science

Massachusetts Institute of Technology

## Preface

A computer revolution is in full swing. The invasion of computing into every part of our lives has brought enormous benefits including email, internet, World Wide Web, Amazon’s e-commerce, Kahn Academy, Uber’s taxi hailing, Google’s maps, trip navigators, smartphones, real-time translators, and apps by the millions. At the same time it has also brought enormous concerns including possible loss of jobs to automation, mass surveillance, collapse of critical infrastructure, cyber war, mass sales of personal data, invasions of advertising, loss of privacy, polarization of politics, loss of civility and respectful listening, and exacerbated income inequality.

A lot of people are having trouble coming to grips with all this. Can they reap the benefits without the downside costs? Can they lead a meaningful life if computerization suddenly threatens to obsolete a lifetime of learning? What should their children learn about computing to enable them to move and prosper in the new world?

Computational thinking is a new term that has recently entered public discourse as people struggle with these questions. It holds the hope that we can think clearly about the powers and dangers of mass computing, and that we can learn to design computers, software, and networks to maximize the benefits and minimize the risks. Parents are already amazed at how facile their children seem to be in the digital world. Is computational thinking the recipe for giving our children a proper education in this world?

We designed this book to be an edifying conversation to help you understand what computational thinking is so that you will be in a better position to answer these questions for yourself.

The first thing to understand is that a substantial part of daily discourse is shaped by the wide adoption of computers. This is nothing new; our ancestors’ ways of thinking about the world were shaped by the technologies of previous revolutions. In the industrial age, for example, people regularly used expressions like:

「He blew a gasket,」「I’m humming on all pistons,」「It’s a high pressure environment,」and「I had to blow off steam.」

Today we hear expressions like:

「My DNA programs me to do it this way,」「Our laws are algorithms for running our society,」「My brain is hardware and my mind software,」and「My brain crashed, I need to reboot.」

Just as in the industrial age, the new idioms of the computer age reveal more about our popular culture than they do about the technology.

Like the Greek god Janus, computational thinking has two faces, one that looks behind and explains all that has happened, and one that looks ahead to what can be designed. We invoke both faces when we want to get computers to do jobs for us. On the back-facing side, we need to understand the mechanics of how computers work, how they are controlled by algorithms, how we can express algorithms in a programming language, and how we can combine many software modules into working systems. On the forward-facing side, we need sensibilities to understand the context in which users of our software are working. We want our software to be valuable to them and not to cause harm to them or their environment. Thus, computational thinking guides us to understand the technology available to us and to design software to do a job or solve a problem.

Computational thinking is not only something programmers must know, but it is also a thinking tool for understanding our technology-infused social world. It increases our awareness of how our everyday digital tools work, grounds our cyber ethics, and improves our resilience against various threats such as algorithm-driven attempts to guide our behavior, personally tailored fake news, viral powers of social media, and massive, data-intensive analysis of our movements. What is more, computational thinking has irrevocably changed the tools, methods, and epistemology of science. Learning CT has many benefits beyond programming.

If you try to understand what computational thinking is from media accounts, you will hear a story of problem solving with algorithms, along with the ability to think at the many levels of abstraction needed to solve problems. The story is flavored with images of joyous children having fun programming and playing games in which they simulate algorithms. Indeed, our teachers have learned much about computational thinking from teaching computing to children, and they have developed superb ways of teaching fundamental computing insights to newcomers. In this book, we call this「CT for beginners.」

But the K–12 education insights and debates barely scratch the surface of computational thinking. At the more advanced levels, computational thinking concerns the design of hardware, networks, storage systems, operating systems, and the cloud. Its historical predecessors have organized human teams to do large computations, organized production lines in manufacturing, guided lawmakers, and specified the rules of bureaucracies. It has developed styles attuned to major areas where computing plays a critical role, such as artificial intelligence, large data analytics, software engineering, and computational science. We will show you all this by examining the kinds of computational thinking needed to deal with these different dimensions of computing. A much more advanced kind of computational thinking is needed to deal with these areas. We call it「CT for professionals.」

Computational thinking is sometimes portrayed as a universal approach to problem solving. Take a few programming courses, the story in the popular media goes, and you will be able to solve problems in any field. Would that this were true! Your ability to solve a problem for someone depends on your understanding of their context in which the problem exists. For instance, you cannot build simulations of aircraft in flight without understanding fluid dynamics. You cannot program searches through genome databases without understanding the biology of the genome and the methods of collecting the data. Computational thinking is powerful, but not universal.

Computational thinking illuminates a fundamental difference in the ways that humans and machines process information. Machines can process information at billions or trillions of calculations per second, whereas humans do well at one calculation per second. Machines process with no understanding of the data they are processing, whereas humans do and can correct errors on the fly. Machines can transform a mistake in an algorithm into a costly disaster before any human has a chance to react. Thinkers in the philosophy of mind, neuropsychology, cognitive science, and artificial intelligence have studied these differences and shown us how fundamentally dissimilar they are. Although some human tasks like searching and sorting can be eased by applying algorithms to them, most computational thinking in the big picture is concerned with machine computation.

2『上面计算机思维和人的思维，做一张主题卡片。』—— 已完成

Think for a moment about the speed issue. A typical computer can, in 1 second, perform a billion calculations and draw a complex image on the screen. A human would need 100 years to carry out the same steps at human speed. Humans obviously draw pictures much faster than that, but machine designers have yet to imitate that human capacity. If humans had no help from computers, we would have no real time graphics. Nearly everything we see software doing is made possible by the incredible speeds of computers. These machines, not humans executing algorithms on their own, are the reason for the computer revolution. Computing machines do the humanly impossible.

While this may send a thrill up your neck, it ought also to send a shiver down your spine. Modern aircraft are controlled by networks of computers performing billions of calculations per second. A mistake in an algorithm can cause the control system to send the aircraft into a death spiral long before the human pilot can react. Early Apollo missions and more recent Mars missions were aborted and lost due to errors in their software. Mistakes in algorithms can be deadly and costly. How can we know that the algorithms running critical systems can be trusted to work properly, bringing benefits and low risk of harm? We need clear thinking to help us find our way through this maze of complexity. This requires an advanced form of CT that is not learned from children’s simulation games.「CT for professionals」is deadly serious.

Our account of CT in this book encompasses all the flavors of CT from beginners to professionals, and in major subfields such as software engineering and computational science. We aim to describe CT in all its richness, breadth, and depth. We want to celebrate the work of expert professionals who take on the hard challenges of getting complex systems to perform reliably and safely, and the kinds of thinking they bring that enables them to have achieved such a good track record. We also want to celebrate the work of expert educators who are working to ease the first steps into computational thinking in K–12 schools and lay the foundation to provide everyone the means for coping in the digital world. Those two, basic CT for beginners and advanced CT for professionals, work together to produce a rich tapestry of computational thought.

Peter J. Denning

Salinas, California, August 2018

Matti Tedre

Joensuu, Finland, August 2018

## Acknowledgments

Peter: Many thanks to Dorothy Denning, my wife, who listened to my many speeches about computing for nearly 50 years and kept me channeled in productive directions. Much appreciation to my friend Fernando Flores, for teaching me how to read history for the concerns that emerge from it and thus discern different stages of computational thinking over the centuries. To the founders of computing and computing education whom I met through ACM, including Eckert, Mauchly, Perlis, Newell, Simon, Forsythe, Conte, Wilkes, Hamming, Knuth, and Dijkstra. To my teachers at MIT who turned this electrical engineer into one of the first holders of a computer science degree, especially Fano, Corbato, Dennis, Saltzer, Scherr, and Zadeh. To my many colleagues in computer science and engineering over the years, too numerous to mention by name here, who engaged me in edifying conversations about computing.

Matti: I am grateful to all those who have helped me develop my own computational thinking: my old teachers, mentors, and past and present colleagues from all walks of research. I feel privileged to have gained a wealth of computing insights from working in universities in six countries on three continents. I am also thankful to my friends and colleagues from the field of history and philosophy of computer science—too many to be listed here. I wish to especially thank Maarten Bullynck, Edgar Daylight, Liesbeth De Mol, Lauri Malmi, John Pajunen, Giuseppe Primiero, and Simon (as well as ANR PROGRAMme ANR-17-CE38-0003-01 partners) for inspiring conversations, feedback, and collaboration on material directly related to this book. My work was partially supported by the Association of Finnish Non-fiction Writers.

Acknowledgment of prior publishers: Parts of chapter 5 are adapted from the following sources: Great Principles of Computing by Peter Denning and Craig Martell (MIT Press, 2015);「The Forgotten Engineer」by Peter Denning (Communications of the ACM 60, 12 [December 2017]: 20–23), and「Computing as Engineering」by Matti Tedre (Journal of Universal Computer Science 15, 8: 1642–1658). Parts of chapter 6 are adapted from:「Software Quality」by Peter Denning (Communications of the ACM 59, 9 [September 2016]: 23–25;「Design Thinking」by Peter Denning (Communications of the ACM 56, 12 [December 2013]: 29–31; and Great Principles of Computing. Parts of chapter 7 have been adapted from「Computational Thinking in Science」by Peter Denning (American Scientist 105 [January–February 2017): 13–17.

## Contents

Series Foreword

Preface

Acknowledgments

1 What Is Computational Thinking?

2 Computational Methods

3 Computing Machines

4 Computer Science

5 Software Engineering

6 Designing for Humans

7 Computational Science

8 Teaching Computational Thinking for All

9 Future Computation

Epilogue: Lessons Learned

Glossary

Notes

References and Further Reading

Index