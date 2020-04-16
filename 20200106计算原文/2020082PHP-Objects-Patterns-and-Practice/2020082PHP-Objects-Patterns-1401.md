Good (and Bad) Practice

So far in this book, I have focused on coding, concentrating particularly on the role of design in building flexible and reusable tools and applications. Development doesn’t end with code, however. It is possible to come away from books and courses with a solid understanding of a language, yet still encounter problems when it comes to running and deploying a project.

In this chapter, I will move beyond code to introduce some of the tools and techniques that form the 

underpinnings of a successful development process. This chapter will cover the following:

Build: Creating and deploying packages

Third-party packages: Where to get them and when to use them

•	•	•	 Version control: Bringing harmony to the development process•	 Documentation: Writing code that is easy to understand, use, and extend•	 Unit testing: A tool for automated bug detection and prevention•	•	 Vagrant: A tool that uses virtualization, so that all developers can work with a system 

Standards: Why it's sometimes good to follow the herd

that resembles a production environment, no matter their hardware or OS

•	

Continuous integration: Using this practice and set of tools to automate project builds and tests, as well as to be alerted of problems as they occur

Beyond Code

When I first graduated from working on my own and took a place in a development team, I was astonished at how much stuff other developers seemed to have to know. Good-natured arguments simmered endlessly over issues of vital-seeming importance: Which is the best text editor? Should the team standardize on an integrated development environment? Should we impose a coding standard? How should we test our code? Should we document as we develop? Sometimes these issues seemed more important than the code itself, and my colleagues seemed to have acquired their encyclopedic knowledge of the domain through some strange process of osmosis.

The books I had read on PHP, Perl, and Java certainly didn’t stray from the code itself to any great extent. 

As I have already discussed, most books on programming platforms rarely diverge from their tight focus on functions and syntax to take in code design. If design is off topic, you can be sure that wider issues such as version control and testing are rarely discussed. This is not a criticism—if a book professes to cover the main features of a language, it should be no surprise that this is all it does.

377

Chapter 14 ■ Good (and Bad) praCtiCe

In learning about code, however, I found that I had neglected many of the mechanics of a project’s day-

to-day life. I discovered that some of these details were critical to the success or failure of projects I helped develop. In this chapter, and in more detail in coming chapters, I will look beyond code to explore some of the tools and techniques on which the success of your projects may depend.

Borrowing a Wheel

When faced with a challenging but discrete requirement in a project (the need to parse a particular format, perhaps, or to use a novel protocol in talking to a remote server), there is a lot to be said for building a component that addresses the need. It can also be one of the best ways to learn your craft. In creating a package, you gain insight into a problem and file away new techniques that might have wider application. You invest at once in your project and in your own skills. By keeping functionality internal to your system, you can save your users from having to download third-party packages. Occasionally, too, you may sidestep thorny licensing issues. There’s nothing like the sense of satisfaction you can get when you test a component you designed yourself and find that, wonder of wonders, it works—it does exactly what you wrote on the tin.

There is a dark side to all this, of course. Many packages represent an investment of thousands of 

man-hours: a resource that you may not have on hand. You may be able to address this by developing only the functionality needed specifically by your project, whereas a third-party tool might fulfill a myriad of other needs, as well. The question remains, however: if a freely available tool exists, why are you squandering your talents in reproducing it? Do you have the time and resources to develop, test, and debug your package? Might not this time be better deployed elsewhere?

I am one of the worst offenders when it comes to wheel reinvention. Picking apart problems and 

inventing solutions to them is a fundamental part of what we do as coders. Getting down to some serious architecture is a more rewarding prospect than writing some glue to stitch together three or four existing components. When this temptation comes over me, I remind myself of projects past. Although the choice to build from scratch has never killed a project in my experience, I have seen it devour schedules and murder profit margins. There I sit with a manic gleam in my eye, hatching plots and spinning class diagrams, failing to notice as I obsess over the details of my component that the big picture is now a distant memory.

Now, when I map out a project, I try to develop a feel for what belongs inside the codebase and what should be treated as a third-party requirement. For example, your application may generate (or read) an RSS feed; and you may need to validate e-mail addresses and automate mailouts, authenticate users, or read from a standard-format configuration file. All of these needs can be fulfilled by external packages.

In previous versions of this book, I suggested that PEAR (PHP Extension and Application Repository) 

was the way to go for packages. Times change, though, and the PHP world has very definitely moved to the Composer dependency manager and its default repository, Packagist (https://packagist.org). Because Composer manages packages on a per-project basis, it is less prone to the dreaded dependency hell syndrome (where different packages require incompatible versions of the same library). Besides, the fact that all the action has moved to Composer/Packagist means that you’re more likely to find what you’re looking for there. What’s more, many of the PEAR packages are available through Packagist (https://packagist.org/packages/pear/).

So, once you have defined your needs, your first stop should be the Packagist site. You can then use Composer to install your package and to manage package dependencies. I will cover Composer in more detail in the next chapter.

To give you some idea of what’s available using Composer and Packagist, here are just a few of the 

things you can do with the packages you’ll find there:

•	 Cache output with pear/cache_lite•	•	•	

Extract RSS feeds with simplepie/simplepie

Test the efficiency of your code with the athletic/athletic benchmark library

Abstract the details of database access with doctrine/dbal

378

Chapter 14 ■ Good (and Bad) praCtiCe

•	•	•	

Send mail with attachments with pear/mail

Parse configuration file formats with symfony/config

Parse and manipulate URLs with jwage/purl

The Packagist website provides a powerful search facility. You may find packages that address your 

needs there, or you may need to cast your net wider using a search engine. Either way, you should always take time to assess existing packages before setting out to potentially reinvent that wheel.

The fact that you have a need—and that a package exists to address it—should not be the start and end of your deliberations. Although it is preferable to use a package where it will save you otherwise unnecessary development, in some cases it can add overhead without real gain. Your client’s need for your application to send mail, for example, does not mean that you should automatically use the pear/mail package. PHP provides a perfectly good mail() function, so this would probably be your first stop. As soon as you realize that you have a requirement to validate all e-mail addresses according to the RFC822 standard and that the design team wants to send image attachments with the e-mails, you may begin to weigh the options differently. As it happens, pear/mail supports both these features (the latter in conjunction with mail_mime).Many programmers, myself included, often place too much emphasis on the creation of original code, 

sometimes to the detriment of their projects.

 the unwillingness to use third party tools and solutions is often built-in at the institutional level. this 

 ■ Note tendency to treat external products with suspicion is sometimes known as the not invented here syndrome.

This emphasis on authorship may be one reason that there often seems to be more creation than actual 

use of reusable code.

Effective programmers see original code as just one of the tools available to aid them in engineering a project’s successful outcome. Such programmers look at the resources they have at hand and deploy them effectively. If a package exists to take some strain, then that is a win. To steal and paraphrase an aphorism from the Perl world: good coders are lazy.

Playing Nice

The truth of Sartre’s famous dictum that「Hell is other people」is proved on a daily basis in some software projects. This might describe the relationship between clients and developers, symptomized by the many ways that lack of communication leads to creeping features and skewed priorities. But the cap fits, too, for happily communicative and cooperative team members when it comes to sharing code.

As soon as a project has more than one developer, version control becomes an issue. A single coder 

may work on code in place, saving a copy of her working directory at key points in development. Introduce another programmer to the mix, and this strategy breaks down in minutes. If the new developer works in the same development directory, then there is a real chance that one programmer will overwrite the work of his colleague when saving, unless both are very careful to always work on different files.

Alternatively, our two developers can each take a version of the codebase to work on separately. That works fine until the moment comes to reconcile the two versions. Unless the developers have worked on entirely different sets of files, the task of merging two or more development strands rapidly becomes an enormous headache.

This is where Git, Subversion, and similar tools come in. Using a version control system, you can check out your own version of a codebase and work on it until you are happy with the result. You can then update your version with any changes that your colleagues have been making. The version control software will automatically merge these changes into your files, notifying you of any conflicts it cannot handle. Once you have tested this new hybrid, you can save it to the central repository, making it available to other developers.

379

Chapter 14 ■ Good (and Bad) praCtiCe

Version control systems provide you with other benefits. They keep a complete record of all stages of a project, so you can roll back to, or grab a snapshot of, any point in the project’s lifetime. You can also create branches, so that you can maintain a public release at the same time as a bleeding-edge development version.

Once you have used version control on a project, you will not want to attempt another without it. 

Working simultaneously with multiple branches of a project can be a conceptual challenge, especially at first, but the benefits soon become clear. Version control is just too useful to live without. I cover Git in Chapter 17.

Giving Your Code Wings

Have you ever seen your code grounded because it is just too hard to build? This is especially true for projects that are developed in place. Such projects settle into their context, with passwords and directories, databases and helper application invocations programmed right into the code. Deploying a project of this kind can be a major undertaking, with teams of programmers picking through source code to amend settings, so that they fit the new environment.

This problem can be eased to some degree by providing a centralized configuration file or class so that settings can be changed in one place. But even then, build can be a chore. The difficulty or ease of installation will have a major impact upon the popularity of any application you distribute. It will also impede or encourage multiple and frequent deployments during development.

As with any repetitive and time-consuming task, build should be automated. A build tool can determine default values for install locations, check and change permissions, create databases, and initialize variables, among other tasks. In fact, a build tool can do just about anything you need to get an application from a source directory in a distribution to full deployment.

This doesn’t absolve the user from the responsibility for adding information about his environment to 

the code, of course, but it can make the process as easy as answering a few questions or providing a couple of command line switches.

Cloud products such as Amazon’s EC2 have made it possible to create test and staging environments, as needed. Good build and install solutions are essential in order to take full advantage of these resources. It’s no good being able to provision a server on an automated basis if you can’t also deploy your system on the fly.

There are various build tools available to the developer. Both PEAR and Composer manage installation 

(PEAR centrally, and Composer to a local vendor directory). You can create your own packages for either system, which can then be downloaded and installed by users with ease. Build is about much more than the process of placing file A in location B, however.

In Chapter 19, I will look at an application called Phing. This open source project is a port of the popular Ant build tool that is written in and for Java. Phing is written in and for PHP, but it’s architecturally similar to Ant and uses the same XML format for its build files.

Composer performs a limited number of tasks extremely well and offers the simplest possible 

configuration. Phing is more daunting at first, but with the tradeoff of immense flexibility. Not only can you use Phing to automate anything from file copying to XSLT transformation, you can easily write and incorporate your own tasks, should you need to extend the tool. Phing is written using PHP’s object-oriented features, and its design emphasizes modularity and ease of extension.

Build tools and those designed for package or dependency management are far from mutually 

exclusive. Typically, a build tool is used during development to run tests, perform project housekeeping, and to prepare the packages that are ultimately deployed via PEAR, Composer, or even distribution based–package management systems like RPM and Apt.

Standards

I mentioned previously that this book is shifting its focus in this edition from PEAR to Composer. Is this because Composer is much better than PEAR? I do love lots of things about Composer, and these might swing the decision on their own. The principal reason the book is shifting, though, is that everyone else has 

380

Chapter 14 ■ Good (and Bad) praCtiCe

shifted. Composer has become the standard for dependency management. That is crucial because it means that when I find a package at Packagist, I am also likely to find all its dependencies and related packages. I’ll even find many of the PEAR packages there.

Choosing a standard for dependency management, then, ensures availability and interoperability. But standards apply beyond packages and dependencies to the ways that systems work and to the ways that we code. If we agree on protocols, then our systems and teams can integrate seamlessly with one another. And, as more and more components mix across more and more systems, that is increasingly essential.

Where a definitive way of handling, say, logging, is needed, it is obviously ideal that we adopt the best protocol. But the quality of the recommendation (which will dictate formats, log levels, etc.) is possibly less important than the fact that we all comply with it. It’s no good implementing the best standard if you’re the only person doing it.

In chapter 15, I discuss standards in more detail with particular reference to a set of recommendations 

managed by the PHP-FIG group. These PSRs (PHP Standards Recommendations) cover everything from caching to security. In the chapter, I will focus on PSR-1 and PSR-2, recommendations which address the thorny issue of coding style (where do you like to put your braces? And how do you feel about someone else telling you to change the way you do it?). Then I move on to the absolute boon of PSR-4, which covers autoloading (support for PSR-4 is another area in which Composer excels).

Vagrant

What operating system does your team use? Some organizations mandate a particular combination of hardware and software, of course. Often, though, there will be a mix. One developer may have a development machine running Fedora. Another might swear by his MacBook, and a third may stick with his Windows box (he probably likes it for gaming).

Chances are, the production system will run on something else entirely—CentOS, perhaps.It can be a pain getting a system to work across multiple platforms, and it can be a risk if none of those 

platforms resemble the production system. You really don’t want to discover issues related to the production OS after you’ve gone live. In practice, of course, you’ll likely deploy to a staging environment first. Even so, wouldn’t it be better to catch these problems early?

Vagrant is a technology that uses virtualization to give all team members a development environment 

that is as close as possible to production. Getting up and running should be as simple as invoking a command or two and, best of all, everyone can stick with their favorite machines and distributions (I’m a Fedora guy, for the record).

I cover Vagrant in Chapter 20.

Testing

When you create a class, you are probably pretty sure that it works. You will, after all, have put it through its paces during development. You’ll also have run your system with the component in place, checking that it integrates well, and that your new functionality is available and performing as expected.

Can you be sure that your class will carry on working as expected though? That might seem like a silly question. After all, you’ve checked your code once; why should it stop working arbitrarily? Well, of course it won’t; nothing happens arbitrarily, and if you never add another line of code to your system, you can probably breathe easy. If, on the other hand, your project is active, then it’s inevitable that your component’s context will change and highly likely that the component itself will be altered in any number of ways.

Let’s look at these issues in turn. First, how can changing a component’s context introduce errors? Even in a system where components are nicely decoupled from one another, they remain interdependent. Objects used by your class return values, perform actions, and accept data. If any of these behaviors change, the effects on the operation of your class might cause the kind of error that’s easy to catch—the kind where your system falls over with a convenient error message that includes a file name and line number. Much more 

381

Chapter 14 ■ Good (and Bad) praCtiCe

insidious, though, is the kind of change that does not cause an engine-level error, but nonetheless confuses your component. If your class makes an assumption based on another class’s data, a change in that data might cause it to make a wrong decision. Your class is now in error and without a change to a line of code.And it’s likely that you will go on altering the class you’ve just completed. Often, these changes will be 

minor and obvious—so minor, in fact, that you won’t feel the need to run through the careful checks you performed during development. You’ll have probably forgotten them all, anyhow, unless you kept them in some way (perhaps commented out at the bottom of your class file as I sometimes do). Small changes, though, have a way of causing large unintended consequences—consequences that might have been caught had you thought to put a test harness in place.

A test harness is a set of automated tests that can be applied to your system as a whole or to its individual 

classes. Well deployed, a test harness helps you to prevent bugs from occurring and from recurring. A single change may cause a cascade of errors, and the test harness can help you to locate and eliminate these. This means you can make changes with some confidence that you are not breaking anything. It is quite satisfying to make an improvement to your system and then see a list of failed tests. These are all errors that might have been propagated within your system, but now it won’t have to suffer them.

Continuous Integration

Have you ever made a schedule that made everything okay? You start with an assignment: code maybe, or a school project. It’s big and scary, and failure lurks. But you get out a sheet of paper, and you slice it up into manageable tasks. You determine the books to read and the components to write. Maybe you highlight the tasks in different colors. Individually, none of the tasks is actually that scary, it turns out. And gradually, as you plan, you conquer the deadline. As long as you do a little bit every day, you’ll be fine. You can relax.

Sometimes, though, that schedule takes on a talismanic power. You hold it up like a shield, to protect yourself from doubt, and from the creeping fear that perhaps this time you’ll crash and burn. And it’s only after several weeks that you realize the schedule is not magic on its own. You actually have to do the work, too. By then, of course, lulled by the schedule’s reassuring power, you have let things slide. There’s nothing for it but to make a new schedule. This time it will be less reassuring.

Testing and building are like that, too. You have to run your tests. You have to build your projects, and 

build them in fresh environments regularly; otherwise, the magic won’t work.

And if writing tests is a pain, running them can be a chore, especially as they gain in complexity and failures interrupt your plans. Of course, if you were running them more often, you’d probably have fewer failures, and those you did have would stand a good chance of relating to new code that’s fresh in your mind.

It’s easy to get comfortable in a sandbox. After all, you’ve got all your toys there: little scriptlets that 

make your life easy, development tools, and useful libraries. The trouble is, your project may be getting too comfortable in your sandbox, too. It may begin to rely on uncommitted code, or dependencies that you have left out of your build files. That means it’s broken anywhere else but where you work.

The only answer is to build, build, and build again. And do it in a reasonably virgin environment each time.Of course, it’s all very well to advise this; it’s quite another matter to do it. Coders as a breed tend to like 

to code. They want to keep the meetings and the housekeeping to a minimum. That’s where Continuous Integration (CI) comes in. CI is both a practice and a set of tools to make the practice as easy as it possibly can be. Ideally, builds and tests should be entirely automatic, or at least launchable from a single command or click. Any problems will be tracked, and you will be notified before an issue becomes too serious. I will talk more about CI in Chapter 21.

382

Chapter 14 ■ Good (and Bad) praCtiCe

Summary

A developer’s aim is always to deliver a working system. Writing good code is an essential part of this aim’s fulfillment, but it is not the whole story.

In this chapter, I introduced dependency management with Composer and Packagist. I also discussed 

two great aids to collaboration: Vagrant and version control. I covered why version control requires automated build, and I introduced Phing, a PHP implementation of Ant, a Java build tool. Finally, I discussed software testing and introduced CI, a set of tools to automate build and testing.

383

CHAPTER 15

