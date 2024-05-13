# 0601. Designing for Humans

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

## 6.1 What Is Design?

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

## 6.2 Software Quality and Satisfaction

In the 1970s, software engineers sought to make software quality measurable, on the time-honored premise that we get more of what we measure. They devised models for measuring software quality. Their models eventually became a standard of the ISO (International Standards Organization), and a central building block of computational thinking in software engineering. The ISO standards list 20 measurable factors to assess overall quality of a software system:

correctness | reliability | integrity | usability | efficiency | maintainability | testability | interoperability | flexibility | reusability | portability | clarity | modifiability | documentation | resilience | understandability | validity | functionality | generality | economy

These measures were all intended to be objectively measurable properties of the software. It is very hard to design a software system that scores high on all 20 factors. Two of the five traditional DRUSS objectives — security and safety — are not on this list because no one knew how to measure software for these aspects. No one said that quality is simple and straightforward.

The new and burgeoning market for apps has brought attention to quality as an assessment of users rather than as a property of the software. Quality is in the eye of the beholder. Much more attention is paid to design in the sense that Winograd has defined it. How do users assess quality — and, by implication, good design? Table 6.2 presents six distinct levels of satisfaction in the user's experience. [6]

Each level on the software quality ladder involves a skill level of computational thinking. The lowest levels are undisciplined use of CT; the highest levels are disciplined CT to design for customer practices, breakdowns, and evolving concerns. The higher the level, the more professional and advanced aspects of CT are involved. Ascending the ladder, CT skill extends its sensibilities from formal requirements to customer concerns and futures; the level of customer satisfaction rises.

6 Denning (2016).

### Level −1: No Trust

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

### Level 0: Cynical Satisfaction

Many customers trust some but not all the claims made by the software maker — enough to be cynically willing to use it. Much software is released with bugs and security vulnerabilities, which the developers fix only after hearing customer complaints and bug reports. User forums are rife with stories about how the software has failed them and with requests for workarounds and fixes; representatives of the developers are usually nowhere to be seen in these forums.

Using some intermediate CT practices, developers get their software working despite design flaws and holes that demand workarounds. The developers may tolerate their disorganized and haphazard development environment because they are under strong pressure to get something workable to market before the competition, they believe that customers will tolerate many bugs, and they evade liability with no-responsibility license agreements customers must sign to unlock software. This approach is common in the software industry. It is coming under fire because the many bugs are also security vulnerabilities. Cynical customers have no loyalty and will desert to another producer who makes a better offer.

### Level 1: Software Fulfills All Basic Promises

The customer assesses that the producer has delivered exactly what was promised and agreed to. This level of basic integrity relies on more advanced programming and software engineering CT. The ISO standard addresses this level well. Software developers at this level are often standards-oriented and their practices are aimed at producing consistent, reliable products.

### Level 2: Software Fits Environment

At this level, the design extends beyond meeting the stated requirements. It aims to align the software with existing customer practices and it honors cultural sensibilities and other social norms. The customer assesses that the software is a seamless fit to the customer's environment. The bank ATM is a good example of this kind of alignment. The ATM implements familiar bank transactions, enabling customers to use an ATM immediately without having to learn anything special or new. The customer has the experience that the software improves the customer's ability to get work done and to carry out important tasks.

### Level 3: Software Produces No Negative Consequences

At this level, the designer has examined a range of possible ways that the software could produce breakdowns for the customers and builds in operating rules and checks to avoid them. After a period of use, customers encounter no unforeseen problems causing disruption or losses. Customers assess that the product's design has been well thought out and that it anticipates problems that were not apparent at the outset. The software does not produce negative consequences that often arise on the lower quality levels, such as vulnerabilities to hackers and malware, vulnerabilities to user mistakes without the provision to cancel actions or back out to a previous good state, interference with the organization's practices, wasted effort for only marginal productivity gains, and frustration with other negative consequences to customers or their organizations.

At this level, designers may also include functions that the customer did not ask for but that will spare future frustration. Continuous backup systems are one example; the user can retrieve any previous version of a file and can transfer an entire file system to a new computer quickly. Utilities that rebuild damaged files or directories are another example. Still another example are internal management controls that allow the designer to continue to work with the customer after the software is installed in order to modify the software in case negative consequences are discovered. These actions — anticipation of breakdowns and availability of repair services after delivery — are essential for a software producer to earn the user's satisfaction at this level. Programming and software engineering CT do not orient software developers to this direction; design-oriented CT is required.

### Level 4: Software Delights

At the highest level the software goes well beyond the customer's expectations and produces new, unexpected, sometimes surprising positive effects. The user expresses great delight with the product and often promotes it among others. The customer assesses that the producer understands the customer's world and contributes to the customer's well-being. Programming and software engineering CT cannot approach this because delight cannot be stated as formal requirements.

Very few software systems have produced genuine delight. Some early examples include the UNIX system, which was elegant and enabled powerful operations with simple commands; the Apple Macintosh, which brought a revolutionary, easy-to-use desktop with a bitmapped display; the DEC VAX VMS, which was amazingly stable and retained previous versions of files for fast recovery; VisiCalc, the first automated spreadsheet, which made easy accounting available to anyone; Lotus 1-2-3, a successor of VisiCalc, which enabled arbitrary formulas in cells and opened a new programming paradigm; Microsoft Word, which made professional document formatting easy and eventually banished most other word processors from the market; and some smartphones, which provide a reasonably secure environment to download apps that customize the device to the user's taste and identity.

Some smartphone apps have attained high delight ratings; for example, many airlines, publishers, and newspapers offer apps that give direct access to their content via a mobile device. Some apps give users access to networks where data from many others are aggregated to give the user something that saves a lot of time and anxiety. For example, Amazon created the Kindle reader service that enables users to purchase ebooks from the Amazon store and begin reading them instantly from any device with a Kindle app. Google and Apple maps use location information from smartphones to detect traffic congestion, overlay it on street maps, and propose alternate routes around congested areas. Blizzard Entertainment accumulated as many as 10 million subscribers to its World of Warcraft online game because of its rich complexity, easy entry, and detailed graphics. Uber allows users to hail rides whose drivers come to their exact location within minutes. In each case customers found they could do previously impossible things with the app than without, well beyond their expectations.

The interesting thing about these examples is that many of them failed important ISO metrics such as portability, speed, efficiency, or reliability. Yet customers ignored those shortcomings and became avid and loyal subscribers to the software developer.

Software developers are banking on new delights as artificial intelligence technology matures. Many people are looking forward to driverless cars, personal assistants that know your daily routines and overcome your forgetfulness, and virtual reality tools that allow you to tour distant places, train risk-free for a new skill or environment, or access new kinds of entertainment. Computational thinking that takes design deep into the organizational, human, and social aspects of computing have never been as important as today.

But delight is ephemeral if based only on the software itself. Having mastered the new environment, customers will expand horizons and expect more. Few would find the original UNIX, Macintosh, VMS, VisiCalc, or Word to be delightful today. Software producers now invest considerable effort into knowing their customers and anticipating what will delight next.

## 6.3 The Design Way of Computational Thinking

The software engineering way of computational thinking emphasizes the correct implementation of clearly stated functional requirements in software. Its success measures are properties observable in the software or its usage data.

The design way of computational thinking also emphasizes the construction of virtual worlds in which users can inhabit and achieve some purpose that is meaningful to them. Its success measures are assessments of satisfaction and quality by users.

Software engineering CT is especially useful for large systems that must perform reliably in safety critical environments. People want carefully engineered air traffic control systems, nuclear plant control systems, and Mars rovers. Design CT is especially useful for software that must fit customer communities, facilitate adoption, and deliver great value. Design CT does not abandon software engineering CT; it listens for opportunities to include delightful functions customers have not yet asked for.

As we described earlier in this chapter, to characterize design CT we have proposed six levels at which customers assess software quality and satisfaction. Program correctness is essential but produces satisfaction only at the first level. The highest level, delight, arises in the context of the relationship between the customer and software developer. The delighted customer will say that the developer has taken the trouble to understand the customer's work and business, is available to help with problems and to seize opportunities, may share some risks on new ventures, and generally cares for the customer. Software developers today look to designs and services that produce genuine delight. When they succeed we witness new waves of killer apps.

## References and Further Reading

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