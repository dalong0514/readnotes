Objects, Patterns, Practice

From object basics through design pattern principles, and on to tools and techniques, this book has focused on a single objective: the successful PHP project.

In this chapter, I recap some of the topics I have covered and points made throughout the book:

•	

PHP and objects: How PHP continues to increase its support for object-oriented programming, and how to leverage these features

•	 Objects and design: Summarizing some OO design principles•	•	

Patterns: What makes them cool

Pattern principles: A recap of the guiding object-oriented principles that underlie many patterns

•	

The tools for the job: Revisiting the tools I have described, and checking out a few I haven’t

Objects

As you saw in Chapter 2, for a long time objects were something of an afterthought in the PHP world. Support was rudimentary, to say the least, in PHP 3, with objects barely more than associative arrays in fancy dress. Although things improved radically for the object enthusiast with PHP 4, there were still significant problems. Not the least of these was that by default, objects were assigned and passed by reference.

The introduction of PHP 5 finally dragged objects center stage. You could still program in PHP without 

ever declaring a class, but the language was finally optimized for object-oriented design. PHP 7 rounded this out, introducing long-awaited features such as scalar and return type declarations. Probably for reasons of backward compatibility, a few popular frameworks remain essentially procedural in nature (notably WordPress); by-and-large, however, most new PHP projects today are object-oriented.

In Chapters 3, 4, and 5, I looked at PHP’s object-oriented support in detail. Here are some of the new 

features PHP has introduced since version 5: reflection, exceptions, private and protected methods and properties, the __toString() method, the static modifier, abstract classes and methods, final methods and properties, interfaces, iterators, interceptor methods, type declarations, the const modifier, passing by reference, __clone(), the __construct() method, late static binding, namespaces, and anonymous classes. The extensive length of this incomplete list reveals the degree to which the future of PHP is bound up with object-oriented programming.

The Zend Engine 2 and PHP 5 have made object-oriented design central to the PHP project, opening up 

the language to a new set of developers and opening up new possibilities for existing devotees.

In Chapter 6, I looked at the benefits that objects can bring to the design of your projects. Because objects 

and design are one of the central themes of this book, it is worth recapping some conclusions in detail.

525

Chapter 22 ■ ObjeCts, patterns, praCtiCe

ChoiceThere is no law that says you have to develop with classes and objects only. Well-designed object-oriented code provides a clean interface that can be accessed from any client code, whether procedural or object-oriented. Even if you have no interest in writing objects (unlikely if you are still reading this book), you will probably find yourself using them, if only as a client of Composer packages.

Encapsulation and DelegationObjects mind their own business and get on with their allotted tasks behind closed doors. They provide an interface through which requests and results can be passed. Any data that need not be exposed, and the dirty details of implementation, are hidden behind this front.

This gives object-oriented and procedural projects different shapes. The controller in an  

object-oriented project is often surprisingly sparse, consisting of a handful of instantiations that acquire objects and invocations that call up data from one set and pass it on to another.

A procedural project, on the other hand, tends to be much more interventionist. The controlling logic 

descends into implementation to a greater extent, referring to variables, measuring return values, and taking turns along different pathways of operation according to circumstance.

DecouplingTo decouple is to remove interdependence between components, so that making a change to one component does not necessitate changes to others. Well-designed objects are self-enclosed. That is, they do not need to refer outside of themselves to recall a detail they learned in a previous invocation.

By maintaining an internal representation of state, objects reduce the need for global variables—a 

notorious cause of tight coupling. In using a global variable, you bind one part of a system to another. If a component (whether a function, a class, or a block of code) refers to a global variable, there is a risk that another component will accidentally use the same variable name and substitute its value for the first. There is a chance that a third component will come to rely on the value in the variable as set by the first. Change the way that the first component works, and you may cause the third to stop working. The aim of object-oriented design is to reduce such interdependence, making each component as self-sufficient as possible.

Another cause of tight coupling is code duplication. When you must repeat an algorithm in different parts of your project, you will find tight coupling. What happens when you come to change the algorithm? Clearly you must remember to change it everywhere it occurs. Forget to do this, and your system is in trouble.

A common cause of code duplication is the parallel conditional. If your project needs to do things 

in one way according to a particular circumstance (e.g., running on Linux), and another according to an alternative circumstance (e.g., running on Windows), you will often find the same if/else clauses popping up in different parts of your system. If you add a new circumstance together with strategies for handling it (MacOS), you must ensure that all conditionals are updated.

Object-oriented programming provides a technique for handling this problem. You can replace 

conditionals with polymorphism. Polymorphism, also known as class switching, is the transparent use of different subclasses according to circumstance. Because each subclass supports the same interface as the common superclass, the client code neither knows nor cares which particular implementation it is using.

Conditional code is not banished from object-oriented systems; it is merely minimized and centralized. 

Conditional code of some kind must be used to determine which particular subtypes are to be served up to clients. This test, though, generally takes place once, and in one place, thus reducing coupling.

526

Chapter 22 ■ ObjeCts, patterns, praCtiCe

ReusabilityEncapsulation promotes decoupling, which promotes reuse. Components that are self-sufficient and communicate with wider systems only through their public interface can often be moved from one system and used in another without change.

In fact, this is rarer than you might think. Even nicely orthogonal code can be project-specific. When 

creating a set of classes for managing the content of a particular web site, for example, it is worth taking some time in the planning stage to look at those features that are specific to your client, and those that might form the foundation for future projects with content management at their heart.

Another tip for reuse: centralize those classes that might be used in multiple projects. Do not, in other 

words, copy a nicely reusable class into a new project. This will cause tight coupling on a macro level, as you will inevitably end up changing the class in one project and forgetting to do so in another. You would do better to manage common classes in a central repository that can be shared by your projects.

AestheticsThis is not going to convince anyone who is not already convinced, but to me, object-oriented code is aesthetically pleasing. The messiness of implementation is hidden away behind clean interfaces, making an object a thing of apparent simplicity to its client.

I love the neatness and elegance of polymorphism, so that an API allows you to manipulate vastly 

different objects that nonetheless perform interchangeably and transparently—the way that objects can be stacked up neatly or slotted into one another like children’s blocks.

Of course, there are those who argue that the converse is true. Object-oriented code can manifest 

itself as an explosion of classes all so decoupled from one another that piecing together their relationships can be a headache. This is a code smell in its own right. It is often tempting to build factories that produce factories that produce factories, until your code resembles a hall of mirrors. Sometimes it makes sense to do the simplest thing that works, and then refactor in just enough elegance for testing and flexibility. Let the problem space determine your solution, rather than a list of best practices.

 the rigid application of so-called best practice is also often an issue in project management, too. 

 ■ Note Whenever the use of a technique or a process begins to resemble ritual, applied automatically and inflexibly, it’s worth taking a moment to investigate the reasoning behind your current approach. it could be you’re drifting from the realm of tools to that of the cargo cult.

It is also worth mentioning that a beautiful solution is not always the best, or most efficient. It is 

tempting to use a full-blown object-oriented solution where a quick script or a few system calls might have gotten the job done.

Patterns

Recently, a Java programmer applied for a job in a company with which I have some involvement. In his cover letter, he apologized for only having used patterns for a couple of years. This assumption that design patterns are a recent discovery—a transformative advance—is testament to the excitement they have generated. In fact, it is likely that this experienced coder has been using patterns for a lot longer than he thinks.

527

Chapter 22 ■ ObjeCts, patterns, praCtiCe

Patterns describe common problems and tested solutions. Patterns name, codify, and organize real-

world best practice. They are not components of an invention or clauses in a doctrine. A pattern would not be valid if it did not describe practices that are already common at the time of hatching.

Remember that the concept of a pattern language originated in the field of architecture. People 

were building courtyards and arches for thousands of years before patterns were proposed as a means of describing solutions to problems of space and function.

Having said that, it is true that design patterns often provoke the kind of emotions associated with 

religious or political disputes. Devotees roam the corridors with an evangelistic gleam in their eye and a copy of the Gang of Four book under their arm. They accost the uninitiated and reel off pattern names like articles of faith. It is little wonder that some critics see design patterns as hype.

In languages such as Perl and PHP, patterns are also controversial because of their firm association with object-oriented programming. In a context in which objects are a design decision and not a given, associating oneself with design patterns amounts to a declaration of preference, not least because patterns beget more patterns, and objects beget more objects.

What Patterns Buy UsI introduced patterns in Chapter 7. Let’s reiterate some of the benefits that patterns can buy us.

Tried and TestedFirst of all, as I’ve noted, patterns are proven solutions to particular problems. Drawing an analogy between patterns and recipes is dangerous: recipes can be followed blindly, whereas patterns are「half-baked」(Martin Fowler) by nature and need more thoughtful handling. Nevertheless, both recipes and patterns share one important characteristic: they have been tried out and tested thoroughly before inscription.

Patterns Suggest Other PatternsPatterns have grooves and curves that fit one another. Certain patterns slot together with a satisfying click. Solving a problem using a pattern will inevitably have ramifications. These consequences can become the conditions that suggest complementary patterns. It is important, of course, to be careful that you are addressing real needs and problems when you choose related patterns, and not just building elegant but useless towers of interlocking code. It is tempting to build the programming equivalent of an architectural folly.

A Common VocabularyPatterns are a means of developing a common vocabulary for describing problems and solutions. Naming is important—it stands in for describing, and therefore lets us cover lots of ground very quickly. Naming, of course, also obscures meaning for those who do not yet share the vocabulary, which is one reason why patterns can be so infuriating at times.

Patterns Promote DesignAs discussed in the next section, patterns can encourage good design when used properly. There is an important caveat, of course. Patterns are not fairy dust.

528

Chapter 22 ■ ObjeCts, patterns, praCtiCe

Patterns and Principles of DesignDesign patterns are, by their nature, concerned with good design. Used well, they can help you build loosely coupled and flexible code. Pattern critics have a point, though, when they say that patterns can be overused by the newly infected. Because pattern implementations form pretty and elegant structures, it can be tempting to forget that good design always lies in fitness for purpose. Remember that patterns exist to address problems.

When I first started working with patterns, I found myself creating Abstract Factories all over my code. I 

needed to generate objects, and Abstract Factory certainly helped me to do that.

In fact, though, I was thinking lazily and making unnecessary work for myself. The sets of objects I 

needed to produce were indeed related, but they did not yet have alternative implementations. The classic Abstract Factory pattern is ideal for situations in which you have alternative sets of objects to generate according to circumstance. To make Abstract Factory work, you need to create factory classes for each type of object and a class to serve up the factory class. It’s exhausting just describing the process.

My code would have been much cleaner had I created a basic factory class, only refactoring to 

implement Abstract Factory if I found myself needing to generate a parallel set of objects.

The fact that you are using patterns does not guarantee good design. When developing, it is a good idea to bear in mind two expressions of the same principle: KISS (「Keep it simple, stupid」) and「Do the simplest thing that works.」eXtreme programmers also give us another, related, acronym: YAGNI.「You aren’t going to need it,」meaning that you should not implement a feature unless it is truly required.

With the warnings out of the way, I can resume my tone of breathless enthusiasm. As I laid out in Chapter 9, patterns tend to embody a set of principles that can be generalized and applied to all code.

Favor Composition over InheritanceInheritance relationships are powerful. We use inheritance to support runtime class switching (polymorphism), which lies at the heart of many of the patterns and techniques I explored in this book. By relying on solely on inheritance in design, though, you can produce inflexible structures that are prone to duplication.

Avoid Tight CouplingI have already talked about this issue in this chapter, but it is worth mentioning here for the sake of completeness. You can never escape the fact that change in one component may require changes in other parts of your project. You can, however, minimize this by avoiding both duplication (typified in our examples by parallel conditionals) and the overuse of global variables (or Singletons). You should also minimize the use of concrete subclasses when abstract types can be used to promote polymorphism. This last point leads us to another principle.

Code to an Interface, Not an ImplementationDesign your software components with clearly defined public interfaces that make the responsibility of each transparent. If you define your interface in an abstract superclass and have client classes demand and work with this abstract type, you then decouple clients from specific implementations.

Having said that, remember the YAGNI principle. If you start out with the need for only one 

implementation for a type, there is no immediate reason to create an abstract superclass. You can just as well define a clear interface in a single concrete class. As soon as you find that your single implementation is trying to do more than one thing at the same time, you can redesignate your concrete class as the abstract parent of two subclasses. Client code will be none the wiser, as it continues to work with a single type.

529

Chapter 22 ■ ObjeCts, patterns, praCtiCe

A classic sign that you may need to split an implementation and hide the resultant classes behind an 

abstract parent is the emergence of conditional statements in the implementation.

Encapsulate the Concept that VariesIf you find that you are drowning in subclasses, it may be that you should be extracting the reason for all this subclassing into its own type. This is particularly the case if the reason is to achieve an end that is incidental to your type’s main purpose.

Given a type UpdatableThing, for example, you may find yourself creating FtpUpdatableThing, 

HttpUpdatableThing, and FileSystemUpdatableThing subtypes. The responsibility of your type, though, is to be a thing that is updatable—the mechanism for storage and retrieval is incidental to this purpose. Ftp, Http, and FileSystem are the things that vary here, and they belong in their own type—let’s call it UpdateMechanism. UpdateMechanism will have subclasses for the different implementations. You can then add as many update mechanisms as you want without disturbing the UpdatableThing type, which remains focused on its core responsibility.

Notice also that I have replaced a static compile-time structure with a dynamic runtime arrangement 

here, bringing us (as if by accident) back to our first principle:「Favor composition over inheritance.」

Practice

The issues that I covered in this section of the book (and introduced in Chapter 14) are often ignored by texts and coders alike. In my own life as a programmer, I discovered that these tools and techniques were at least as relevant to the success of a project as design. There is little doubt that issues such as documentation and automated build are less revelatory in nature than wonders such as the Composite pattern.

 Let’s just remind ourselves of the beauty of Composite: a simple inheritance tree whose objects 

 ■ Note can be joined at runtime to form structures that are also trees, but are orders of magnitude more flexible and complex. Multiple objects share a single interface by which they are presented to the outside world. the interplay between simple and complex, multiple and singular, has got to get your pulse racing—that’s not just software design, it’s poetry.

Even if issues such as documentation and build, testing, and version control are more prosaic than 

patterns, they are no less important. In the real world, a fantastic design will not survive if multiple developers cannot easily contribute to it or understand the source. Systems become hard to maintain and extend without automated testing. Without build tools, no one is going to bother to deploy your work. As PHP’s user base widens, so does our responsibility as developers to ensure quality and ease-of-deployment.

A project exists in two modes. A project is its structures of code and functionality, and it is also set of 

files and directories, a ground for cooperation, a set of sources and targets, and a subject for transformation. In this sense, a project is a system from the outside as much as it is within its code. Mechanisms for build, testing, documentation, and version control require the same attention to detail as the code such mechanisms support. Focus on the metasystem with as much fervor as you do on the system itself.

TestingAlthough testing is part of the framework that one applies to a project from the outside, it is intimately integrated into the code itself. Because total decoupling is not possible, or even desirable, test frameworks are a powerful way of monitoring the ramifications of change. Altering the return type of a method could influence 

530

Chapter 22 ■ ObjeCts, patterns, praCtiCe

client code elsewhere, causing bugs to emerge weeks or months after the change is made. A test framework gives you half a chance of catching errors of this kind (the better the tests, the better the odds here).

Testing is also a tool for improving object-oriented design. Testing first (or at least concurrently) helps 

you to focus on a class’s interface and think carefully about the responsibility and behavior of every method. I introduced PHPUnit, which is used for testing, in Chapter 18.

StandardsI am a contrarian by nature. I hate being told what to do. Words like compliance instantly invoke a fight-or-flight response in me. But, counter-intuitive as it may seem, standards drive innovation. That is because they drive interoperability. The rise of the Internet was fueled in part by the fact that open standards are built in to its core. Web sites can link to one another, and web servers can be reused in any domain because protocols are well-known and respected. A solution in a silo may be better than a widely accepted and applied standard, but what if the silo burns down? What if it is bought, and the new owner decides to charge for access? What happens when some people decide that the silo next door is better? In Chapter 16 I discussed PSR, PHP Standard Recommendations. I focused in particular on standards for autoloading, which have done much to clean up the way that PHP developers include classes. I also looked at PSR-2, the standard for coding style. Programmers have strong feelings about the placement of braces and the deployment of argument lists, but agreeing to abide by a common set of rules makes for readable and consistent code, and allows us to use tools to check and reformat our source files. In that spirit I have reformatted all code examples in this edition to comply with PSR-2.

Version ControlCollaboration is hard. Let’s face it: people are awkward. Programmers are even worse. Once you’ve sorted out the roles and tasks on your team, the last thing you want to deal with is clashes in the source code itself. As you saw in Chapter 17, Git (and similar tools such as CVS and Subversion) enable you to merge the work of multiple programmers into a single repository. Where clashes are unavoidable, Git flags the fact and points you to the source to fix the problem.

Even if you are a solo programmer, version control is a necessity. Git supports branching, so that you can maintain a software release and develop the next version at the same time, merging bug fixes from the stable release to the development branch.

Git also provides a record of every commit ever made on your project. This means that you can roll back 

by date or tag to any moment. This will save your project someday—believe me.

Automated BuildVersion control without automated build is of limited use. A project of any complexity takes work to deploy. Various files need to be moved to different places on a system, configuration files need to be transformed to have the right values for the current platform and database, and database tables need to be set up or transformed. I covered two tools designed for installation. The first, Composer (see Chapter 15), is ideal for standalone packages and small applications. The second build tool I covered was Phing (see Chapter 19), which is a tool with enough power and flexibility to automate the installation of the largest and most labyrinthine project.

Automated build transforms deployment from a chore to a matter of a line or two at the command line. With little effort, you can invoke your test framework and your documentation output from your build tool. If the needs of your developers do not sway you, bear in mind the pathetically grateful cries of your users as they discover that they need no longer spend an entire afternoon copying files and changing configuration fields every time you release a new version of your project.

531

Chapter 22 ■ ObjeCts, patterns, praCtiCe

Continuous IntegrationIt is not enough to be able to test and build a project; you have do it all the time. This becomes increasingly important as a project grows in complexity and you manage multiple branches. You should build and test the stable branch from which you make minor bug fix releases, an experimental development branch or two, and your main trunk. If you were to try to do all that manually, even with the aid of build and test tools, you’d never get around to any coding. Of course, all coders hate that, so build and testing inevitably get skimped on.

In Chapter 20, I looked at Continuous Integration, a practice and a set of tools that automate the build 

and test processes as much as possible.

What I MissedA few tool categories I have had to omit from this book due to time and space constraints are, nonetheless, supremely useful for any project. In most cases, there is more than one good tool for the job at hand so, although I’ll suggest one or two, you may want to spend some time talking with other developers and digging around with your favorite search engine before you make your choice.

If your project has more than one developer or even just an active client, then you will need a tool to 

track bugs and tasks. Like version control, a bug tracker is one of those productivity tools that, once you have tried it on a project, you cannot imagine not using. Trackers allow users to report problems with a project, but they are just as often used as a means of describing required features and allocating their implementation to team members.

You can get a snapshot of open tasks at any time, narrowing the search according to product, task owner, version number, and priority. Each task has its own page, in which you can discuss any ongoing issues. Discussion entries and changes in task status can be copied by mail to team members, so it’s easy to keep an eye on things without going to the tracker URL all the time.

There are many tools out there. Even after all this time, though, I usually return to the venerable Bugzilla 

(http://www.bugzilla.org). Bugzilla is free and open source, and has all the features most developers could need. It is a downloadable product, so you will have to run it on your own server. It still looks a little Web 1.0, but it’s none the worse for that. If you do not want to host your own tracker, and you have or prefer your interfaces a little prettier (and have deeper pockets), you might look at the Atlassian’s SAAS solution, Jira (https://www.atlassian.com/software/jira).

For high level task tracking and project planning (especially if you’re interested in using a Kanban 

system), you might also look at Trello (http://www.trello.com).

A tracker is generally just one of a suite of collaboration tools you will want to use to share information 

around a project. At a price, you can use an integrated solution such as Basecamp (https://basecamp.com/) or Atlassian tools (https://www.atlassian.com/). Or you may choose to stitch together a tools ecosystem using a variety of tools. To facilitate communication within your team, for example, you will probably need a mechanism for chat or messaging. Perhaps the most popular tool for this at the time of this writing is Slack (https://www.slack.com). Slack is a multi-roomed web-based chat environment. If you’re old school like me, you might instantly think of IRC (Internet Relay Chat)—and you’d be right: there’s little you can do with Slack that you couldn’t do with IRC. Except that Slack is browser-based, easy-to-use, and has integration with other services already built-in. Slack is free unless you need premium features.

Speaking of old school, you might also consider using a mailing list for your project. My favorite mailing list software is Mailman (http://www.gnu.org/software/mailman/), which is free, relatively easy to install, and highly configurable.

For co-operatively editable text documents and spreadsheets, Google Docs (https://docs.google.

com/) is probably the easiest solution.

Your code is not as clear as you think it is. A stranger visiting a codebase for the first time can be faced 

with a daunting task. Even you, as author of the code, will eventually forget how it all hangs together. For inline documentation, you should look at phpDocumentor (https://www.phpdoc.org/) which allows you to document as you go, and automatically generates hyperlinked output. The output from phpDocumentor 

532

Chapter 22 ■ ObjeCts, patterns, praCtiCe

is particularly useful in an object-oriented context, as it allows the user to click around from class to class. As classes are often contained in their own files, reading the source directly can involve following complex trails from source file to source file.

Although inline documentation is important, projects also generate a broiling heap of written material. This includes usage instructions, consultation on future directions, client assets, meeting minutes, and party announcements. During the lifetime of a project, such materials are very fluid, and a mechanism is often needed to allow people to collaborate in their evolution.

A wiki (wiki is apparently Hawaiian for「very fast」) is the perfect tool for creating collaborative webs 

of hyperlinked documents. Pages can be created or edited at the click of a button, and hyperlinks are automatically generated for words that match page names. A wiki is another one of those tools that seems so simple, essential, and obvious that you are sure you probably had the idea first, but just didn’t get around to doing anything about it. There are a number of wikis to choose from. I have had good experience with PhpWiki, which can be downloaded from http://phpwiki.sourceforge.net, and DokuWiki, which you can find at http://wiki.splitbrain.org/wiki:dokuwiki.

Summary

In this chapter I wrapped things up, revisiting the core topics that make up the book. Although I haven’t tackled any concrete issues such as individual patterns or object functions here, this chapter should serve as a reasonable summary of this book’s concerns.

There is never enough room or time to cover all the material that one would like. Nevertheless, I hope 

that this book has served to make one argument: PHP is growing up. It is now one of the most popular programming languages in the world. I hope that PHP remains the hobbyist’s favorite language, and that many new PHP programmers are delighted to discover how far they can get with just a little code. At the same time, though, more and more professional teams are building large systems with PHP. Such projects deserve more than a just-do-it approach. Through its extension layer, PHP has always been a versatile language, providing a gateway to hundreds of applications and libraries. Its object-oriented support, on the other hand, gains you access to a different set of tools. Once you begin to think in objects, you can chart the hard-won experience of other programmers. You can navigate and deploy pattern languages developed with reference, not just to PHP, but to Smalltalk, C++, C#, or Java, too. It is our responsibility to meet this challenge with careful design and good practice. The future is reusable.

533

CHAPTER 23

Appendix A: Bibliography

