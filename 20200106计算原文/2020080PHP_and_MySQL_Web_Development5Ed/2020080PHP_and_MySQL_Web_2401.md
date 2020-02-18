25Using PHP and MySQL for Large Projects

In the earlier parts of this book, we discussed various components of and uses for PHP and MySQL. Although we tried to make all the examples interesting and relevant, they were reasonably simple, consisting of a few scripts and rarely more than 100 or so lines of code.

When you are building real-world web applications, writing code is rarely this simple. In the early days of the web, an「interactive」website had a form that sent e-mail and that was it. However, these days, websites have become web applications—that is, regular pieces of software delivered over the web. This change in focus means a change in scale. Websites grow from a handful of short scripts to thousands and thousands of lines of code. Projects of this size require planning and management just like any other software development project.

Before we look at the projects in this part of the book, let’s look at some of the techniques that can be used to manage sizable web projects. Developing, managing, and scaling web sites and web applications is an art form in and of itself, and getting it right is obviously difficult: You can see this by observation in the marketplace, and in the web applications you use every day, as no one is immune to the difficulties.

Key topics covered in this chapter include

 ■ Applying software engineering to web development

 ■ Planning and running a web application project

 ■ Reusing code

 ■ Writing maintainable code

 ■ Implementing version control

 ■ Choosing a development environment

 ■ Documenting your project

 ■ Prototyping

 ■ Separating logic, content, and presentation: PHP, HTML, and CSS

 ■ Optimizing code

530

Chapter 25  Using PHP and MySQL for Large Projects 

Applying Software Engineering to Web DevelopmentIn brief, software engineering is the application of a systematic, quantifiable approach to software development. That is, it is the application of engineering principles to software development.

Software engineering is also an approach that is noticeably lacking in many web projects for two main reasons. The first reason is that traditional web development is often managed in the same way as the development of written reports. It is an exercise in document structure, graphic design, and production. This is a document-oriented paradigm, and the approach is all well and good for static sites of small to medium size. But as the amount of dynamic content in websites increases to the level in which the websites offer services rather than documents, this paradigm no longer fits. Many people do not think to use software engineering practices for a web project at all.

The second reason software engineering practices are often not used is that web application development is different from traditional software application development in many ways. First, web developers deal with much shorter lead times and a constant pressure to have the site built now. Software engineering is all about performing tasks in an orderly, planned manner and spending time on planning. With web projects, often the perception is that you don’t have the time to plan.

When you fail to plan web projects, you end up with the same problems you do when you fail to plan any software project: buggy applications, missed deadlines, and unreadable code. The trick, then, is in finding the parts of software engineering that work in the discipline of web application development, and discarding the parts that don’t.

Planning and Running a Web Application ProjectThere is no best methodology or project life cycle for web projects. There are, however, a number of things you should consider doing for your project. We list them here and discuss some of them in more detail in the following sections. These considerations are in a specific order, but you don’t have to follow this order if it doesn’t suit your project. The emphasis here is on being aware of the issues and choosing techniques that will work for you.

 ■ Before you begin, think about what you are trying to build. Think about the goal. 

Think about who is going to use your web application—that is, your targeted audience. Many technically perfect web projects fail because nobody checked whether users were interested in such an application in the first place.

 ■ Try to break down your application into components. What parts or process steps does 

your application have? How will each of those components work? How will they fit together? Drawing up scenarios, storyboards, and use cases will be useful for figuring out these components and steps.

Reusing Code

531

 ■ After you have a list of components, see which of them already exist. If a prewritten 

module has that functionality, consider using it. Don’t forget to look inside and outside your organization for existing code. Particularly in the open-source community, many preexisting code components are freely available for use. Determine what code you have to write from scratch and roughly how big that job is, before committing to it.

 ■ Make decisions about process issues. By process issues, we mean, for example, 

coding standards, directory structures, management of version control, development environment, documentation level and standards, and task allocations to team members. This step is ignored too often in web projects, and much time is wasted going back and retrofitting code to standards, documenting after the fact, and so on.

 ■ Build a prototype based on all the previous information. Show it to users. Iterate almost 

incessantly, but be mindful of a definition of「done」that works for your organization.

 ■ Remember that, throughout this process, it is important and useful to separate content 

and logic in your application. We explain this idea in more detail shortly.

 ■ Make any optimizations you think are necessary.

 ■ As you go, test your web application as thoroughly as you would any traditional software 

development project.

Reusing CodeProgrammers (and not just those in web application development) often make the mistake of rewriting code that already exists. When you know what application components you need or—on a smaller scale—what functions you need, check what’s available before beginning development.

One of the strengths of PHP as a language is its large built-in function library. Always check to see whether an existing function does what you are trying to do. Finding the one you want usually isn’t too hard. A good way to do this is to browse the PHP manual by function group, at http://php.net/manual/en/funcref.php. 

Sometimes programmers rewrite functions accidentally because they haven’t looked in the manual to see whether an existing function supplies the functionality they need. We highly recommend you always keep the PHP manual bookmarked, no matter your experience level, as it is a rich resource. Take note, however, that the online manual is updated quite frequently, including annotations and comments from the PHP developer community. Within the manual, you will likely find sample code from other users that answers the same questions you might have after reading a function’s basic manual page. The PHP manual also may contain bug reports and workarounds before they are fixed or even officially documented.

You can reach the English-language version of the PHP manual at http://www.php.net/manual/en/.

Some programmers who come from a different language background might be tempted to write wrapper functions to essentially rename PHP’s functions to match the language with which they are familiar. This practice is sometimes called syntactic sugar. It’s a bad idea; it makes your 

532

Chapter 25  Using PHP and MySQL for Large Projects 

code harder for others to read and maintain. If you’re learning a new language, you should learn how to use it properly. In addition, adding a level of function call in this manner slows down your code. All things considered, you should avoid this approach.

If you find that the functionality you require is not in the main PHP library, you have two choices. If you need something relatively simple, you can choose to write your own function or object. However, if you’re looking at building a fairly complex piece of functionality—such as a shopping cart, web email system, or web forums—you should not be surprised to find that somebody else has probably already built it. One of the strengths of working in the open-source community is that code for application components such as these is often freely available. If you find a component similar to the one you want to build, even if it isn’t exactly right, you can look at the source code as a starting point for modification or for building your own.

If you end up developing your own functions or components, you should seriously consider making them available to the PHP community after you have finished. This principle keeps the PHP developer community such a helpful, active, and knowledgeable group.

Writing Maintainable CodeThe issue of maintainability is often overlooked in web applications, particularly because programmers often write them in a hurry. Getting started on the code and getting it finished quickly sometimes seem more important than planning it first. However, a little time invested up front can save you a lot of time further down the road when you’re ready to build the next iteration of an application.

Coding StandardsMost large organizations have coding standards—guidelines to the house style for choosing file and variable names, guidelines for commenting code, guidelines for indenting code, and so on.

Because of the document paradigm often applied to web development, coding standards have sometimes been overlooked in this area. If you are coding on your own or in a small team, you can easily underestimate the importance of coding standards. Don’t overlook such standards because your team and project might grow, and it might grow too quickly for you to reasonably document after the fact. Then you will end up not only with a mess on your hands, but also a bunch of programmers who can’t make heads or tails of any of the existing code, and so they will strike out on their own and likely make the situation even worse.

Defining Naming ConventionsThe goals of defining a naming convention are

 ■ To make the code easy to read. If you define variables and function names sensibly, 

you should be able to virtually read code as you would an English sentence, or at least pseudocode.

 ■ To make identifier names easy to remember. If your identifiers are consistently formatted, 

remembering what you called a particular variable or function will be easier.

Writing Maintainable Code

533

Variable names should describe the data they contain. If you are storing somebody’s surname, call it $surname. In general, strike a balance between length and readability. For example, storing the name in $n makes it easy to type, but the code is difficult to understand. Storing the name in $surname_of_the_current_user is more informative, but it’s a lot to type (and therefore easier to make a typing error) and doesn’t really add that much value.

You need to make a decision on capitalization. Variable names are case sensitive in PHP, as we’ve mentioned previously. You need to decide whether your variable names will be all  lowercase, all uppercase, or a mix—for example, capitalizing the first letters of words. We tend to use all lowercase letters and separate words with underscores (sometimes called「snake case」) because this scheme is the easiest to remember for us. Some organizations will settle on a  standard of lowerCamelCase or UpperCamelCase for multiword variable names; at the end of the day it really doesn’t matter what standard you use, as long as it is standardized within your codebase. You might also want to set a sensible maximum limit of two to three words in a  variable name.

Distinguishing between variables and constants with case is also a good idea. A common scheme is to use all lowercase for variables (for example, $result) and all uppercase for constants (for example, PI).

One bad practice some programmers use is to have two variables with the same name but different capitalization just because they can, such as $name and $Name. We hope it is obvious why this practice is a terrible idea.

It is also best to avoid amusing capitalization schemes such as $WaReZ because no one will be able to remember how it works.

Function names have many of the same considerations as variable names, with a couple of extras. Function names should generally be verb oriented. Consider built-in PHP functions such as addslashes() or mysqli_connect(), which describe what they are going to do to or with the parameters they are passed. This naming scheme greatly enhances code readability. Notice that these two functions have a different naming scheme for dealing with multiword function names. PHP’s functions are inconsistent in this regard, partly as a result of having been written by a large group of people, but mostly because many function names have been adopted unchanged from various different languages and APIs.

Unlike variable names, function names are not case sensitive in PHP. You should probably stick to a particular format anyway when creating your own functions, just to avoid confusion within the code (or your organization).

Additionally, you might want to consider using the module-naming scheme used in many PHP modules—that is, prefixing the name of functions with the module name. For example, all the improved MySQL functions begin with mysqli_, and all the IMAP functions begin with imap_. If, for example, you have a shopping cart module in your code, you could prefix the function in that module with cart_.

Note, however, that when PHP provides both a procedural and an object-oriented interface, the function names are different. Usually, the procedural ones use snake case (my_function()) and the object-oriented ones use lowerCamelCase (myFunction()).

534

Chapter 25  Using PHP and MySQL for Large Projects 

In the end, the conventions and standards you use when writing code don’t really matter, as long as you apply some consistent guidelines within your codebase and your team.

Commenting Your CodeAll programs should be commented to a sensible level. You might ask what level of comment-ing is sensible. Generally, you should consider adding a comment to each of the following items:

 ■ Files, whether complete scripts or include files—Each file should have a comment 

stating what this file is, what it’s for, who wrote it, and when it was updated.

 ■ Functions—Function comments should specify what the function does, what input it 

expects, and what it returns.

 ■ Classes—Comments should describe the purpose of the class. Class methods should have 

the same types and levels of comments as any other functions.

 ■ Chunks of code within a script or function—We often find it useful to write a script by beginning with a set of pseudocode-style comments and then filling in the code for each section. So an initial script might resemble this:<?// validate input data// send to database// report results?>

This commenting scheme is quite handy because after you’ve ﬁ lled in all the sections with function calls or whatever else you need, your code is already commented to a  certain extent.

 ■ Complex code or hacks—When performing some task takes you all day, or you have to do it in a weird way, write a comment explaining why you used that approach. This way, when you next look at the code, you won’t be scratching your head and thinking,「What on earth was that supposed to do?」

Here’s another general guideline to follow: Comment as you go. You might think you will come back and comment your code when you are finished with a project, but we can guarantee you this will not happen, unless you have far less punishing development timetables and more  self-discipline than we (and most developers) do.

IndentingAs in any programming language, you should indent your code in a sensible and consistent fashion. Writing code is like laying out a résumé or business letter. Indenting makes your code easier to read and faster to understand.

In general, any program block that belongs inside a control structure should be indented from the surrounding code. The degree of indenting should be noticeable (that is, more than one space) 

Writing Maintainable Code

535

but not excessive. We generally think the use of tabs should be avoided, but this is a battle that has been waged for decades among developers. Although easy to type, tabs consume a lot of screen space on many people’s monitors. Instead, we use an indent level of two to three spaces for all projects.

The way you lay out your curly braces is also an issue. The two most common schemes followed are:

Scheme 1:

if (condition) {  // do something}

Scheme 2:

if (condition){  // do something else}

Which one you use is up to you. The scheme you choose should, again, be used consistently throughout a project to avoid confusion. Throughout this book, we tend to use the second scheme.

Breaking Up CodeGiant monolithic code is awful. Some people create one huge script that does everything in one giant switch statement. Now, we love switch statements and they have their place, but it is far better to break up the code into functions and/or classes and put related items into include files wherever possible. You can, for example, put all your database-related functions in a file called db_functions.php.

Reasons for breaking up your code into sensible chunks include the following:

 ■ It makes your code easier to read and understand, both for yourself later on, and for 

anyone who might join your project later.

 ■ It makes your code more reusable and minimizes redundancy. For example, with the 

aforementioned db_functions.php file, you could reuse it in every script in which you need to connect to your database. If you need to change the way this works, you have to change it in only one place.

 ■ It facilitates teamwork. If the code is broken into components, you can then assign responsibility for the individual components to team members. It also means that you can avoid the situation in which one programmer is waiting for another to finish working on GiantScript.php so that she can go ahead with her own work.

At the start of any project, spend some time thinking about how you are going to break up a project into components. This process requires drawing lines between areas of functionality, 

536

Chapter 25  Using PHP and MySQL for Large Projects 

and therefore isn’t always a quick planning session, but you should not get bogged down in this because it might change after you start working on a project. Think of the planning as iterative as well. You also need to decide which components need to be built first, which components depend on other components, and what your timeline will be for developing all of them.

Even if all team members will be working on all pieces of the code, it’s generally a good idea to assign primary responsibility for each component to a specific person. Ultimately, this person would be responsible if something goes wrong with his or her component. Someone should also take on the job of build manager—that is, the person who makes sure that all the components are on track and working with the rest of the components. This person usually also manages version control; we discuss this task in more detail later in the chapter. This person can be the project manager, or this task can be allocated as a separate responsibility to a developer.

Using a Standard Directory StructureWhen starting a web development project, you need to think about how your component structure will be reflected in your website’s directory structure. Just as it is a bad idea to have one giant script containing all functionality, it’s also usually a bad idea to have one giant directory containing everything necessary for the website to run.

Decide how you are going to split up your directory structure between components, logic, content, and shared code libraries. Document your structure and make sure that all the people working on the project have access to this documentation so that they can find what they need.

Documenting and Sharing In-House FunctionsAs you develop function libraries, you need to make them available to other programmers on your team. Very often, we have seen every programmer on a team write his or her own set of database, date, or debugging functions. This scheme is a time waster. You should make functions and classes available to others via shared libraries or code repositories.

Remember that even if code is stored in an area or directory commonly available to your team members, they won’t know it’s there unless you tell them. Develop a system for documenting in-house function libraries and make it available to programmers on your team.

Implementing Version ControlVersion control is the art of concurrent change management as applied to software development. Version control systems generally act as a central repository or archive and supply a controlled interface for accessing and sharing your code (and possibly documentation).

Imagine a situation in which you try to improve some code but instead accidentally break it and can’t roll it back to the way it was, no matter how hard you try. Or you or a client decides that an earlier version of the site was better. Or you need to go back to a previous version of a document for legal reasons.

Choosing a Development Environment

537

Imagine another situation in which two members of your programming team want to work on the same file. They both might open and edit the file at the same time, overwriting each other’s changes. They both might have a copy that they work on locally and change in different ways. If you have thought about these things happening, one programmer might be sitting around doing nothing while he or she waits for another to finish editing a file.

You can solve all these problems with a version control system. Such systems can track changes to each file in the repository so that you can see not only the current state of a file, but also the way it looked at any given time in the past. This feature allows you to roll back broken code to a known working version. You can tag a particular set of file instances as a release version, meaning that you can continue development on the code but get access to a copy of the currently released version at any time.

Version control systems also assist multiple programmers in working on code together. Each programmer can get a copy of the code in the repository (called checking it out) and when he or she makes changes, these changes can be merged back into the repository (checked in or  committed). Version control systems can therefore track who made each change to a system.

These systems usually have a facility for managing concurrent updates. This means that two programmers can actually modify the same file at the same time. For example, imagine that John and Mary have both checked out a copy of the most recent release of their project. John finishes his changes to a particular file and checks it in. Mary also changes that file and tries to check it in as well. If the changes they have made are not in the same part of the file, the version control system will merge the two versions of the file. If the changes conflict with each other, Mary will be notified and shown the two different versions. She can then adjust her version of the code to avoid the conflicts.

Several version control systems are available for use, some free and open source, and some proprietary. Some popular systems are Subversion (http://subversion.apache.org), Mercurial (http://mercurial.selenic.com), and Git (http://www.git-scm.com). If your web hosting service or internal IT organization enables you to install any of these tools, your team could create its own repositories and use a GUI or command-line client to connect to it.

However, for users or even organizations who want to get started with version control but don’t necessarily want or need all the extra installation and maintenance overhead that goes with a self-hosted solution, there are several SaaS version control systems that can even be used free for personal and open-source projects. These hosted solutions aren’t just for individuals, as companies and organizations both big and small use distributed version control systems such as GitHub (http://github.com) or Bitbucket (http://www.bitbucket.org).

Choosing a Development EnvironmentThe previous discussion of version control brings up the more general topic of development environments. All you really need are a text editor and browser for testing, but programmers are often more productive when using an Integrated Development Environment (IDE).

Some free and open-source IDEs with PHP support are Eclipse (https://eclipse.org/pdt/) and NetBeans (https://netbeans.org/). Currently, though, the most feature-rich PHP IDEs are 

538

Chapter 25  Using PHP and MySQL for Large Projects 

commercial products; namely, Zend Studio from Zend (http://www.zend.com/), Komodo from ActiveState (http://www.activestate.com/), PhpStorm from JetBrains (https://www.jetbrains.com/phpstorm/), and PHPEd from NuSphere (http://www.nusphere.com/) are all very popular and have a free trial you can explore before you settle on an IDE for yourself or your team.

Documenting Your ProjectsYou can produce many different kinds of documentation for your programming projects including, but not limited to, the following:

 ■ Design documentation

 ■ Technical documentation/developer’s guide

 ■ Data dictionary (including class documentation)

 ■ User’s guide (although most web applications should be self-explanatory)

Our goal here is not to teach you how to write technical documentation but to suggest that you make your life easier by automating part of the process.

Some languages enable you to automatically generate some of these documents—particularly technical documentation and data dictionaries. For example, javadoc generates a tree of HTML files containing prototypes and descriptions of class members for Java programs.

Quite a few utilities of this type are available for PHP, including the following leading projects:

 ■ PHPDocumentor 2 available from http://www.phpdoc.org/

 ■ PHPDocumentor 2 gives similar output to javadoc and works quite robustly. It has 

an active development team and was the result of a merger of two previously competing products.

 ■ phpDox, available from http://phpdox.de/

 ■ phpDox also produces a rich set of code-level documentation and additional useful code 

metrics such as cyclomatic complexity.

PrototypingPrototyping is a development life cycle commonly used for developing web applications. A prototype is a useful tool for working out customer requirements. Usually, it is a simplified, partially working version of an application that can be used in discussions with clients and as the basis of the final system. Often, multiple iterations over a prototype produce the final application. The advantage of this approach is that it lets you work closely with clients or end users to produce a system that they will be pleased with and have some ownership of.

Separating Logic and Content

539

To be able to「knock together」a prototype quickly, you need some particular skills and tools. A component-based approach works well in such situations. If you have access to a set of preexisting components, both in-house and publicly available, you will be able to do this much more quickly. Another useful tool for rapid development of prototypes is templates. We look at these tools in the next section.

You will encounter two main problems using a prototyping approach. You need to be aware of what these problems are so that you can avoid them and use this approach to its maximum potential.

The first problem is that programmers often find it difficult to throw away the code that they have written for one reason or another. Prototypes are often written quickly, and with the benefit of hindsight, you can see that you have not built a prototype in the optimal, or even in a near optimal, way. Clunky sections of code can be fixed, but if the overall structure is wrong, you are in trouble. The problem is that web applications are often built under enormous time pressure, and you might not have time to fix it. You are then stuck with a poorly designed system that is difficult to maintain.

You can avoid this problem by doing a little planning, as we discussed earlier in this chapter. Remember, too, that sometimes it is easier to scrap something and start again than to try to fix the problem. Although starting over might seem like something you don’t have time for, it will often save you a lot of pain later.

The second problem with prototyping is that a system can end up being an eternal prototype. Every time you think you’re finished, your client suggests some more improvements or addi-tional functionality or updates to the site. This feature creep can stop you from ever signing off on a project.

To avoid this problem, draw up a project plan with a fixed number of iterations and a date after which no new functionality can be added without replanning, budgeting, and scheduling.

Separating Logic and ContentYou are probably familiar with the idea of using HTML to describe a web document’s structure and cascading style sheets (CSS) to describe its appearance. This idea of separating presentation from content can be extended to scripting. In general, sites will be easier to use and maintain in the long run if you can separate logic from content from presentation. This process boils down to separating your PHP and HTML (and its included CSS and JavaScript).

For simple projects with a small number of lines of code or scripts, separating content and logic can be more trouble than it’s worth. As your projects become bigger, it is essential to find a way to separate logic and content. If you don’t do this, your code will become increasingly difficult to maintain. If you or the powers that be decide to apply a new design to your website and a lot of HTML is embedded in your code, changing the design will be a nightmare.

540

Chapter 25  Using PHP and MySQL for Large Projects 

Three basic approaches to separating logic and content follow:

 ■ Use include files to store different parts of the content. This approach is simplistic, but if your site is mostly static, it can work quite well. This type of approach was explained in the TLA Consulting example in Chapter 5,「Reusing Code and Writing Functions.」

 ■ Use a function or class API with a set of member functions to plug dynamic content into 

static page templates. We looked at this approach in Chapter 6,「Object-Oriented PHP.」

 ■ Use a template system. Such systems parse static templates and use regular expressions 

to replace placeholder tags with dynamic data. The main advantage of this approach is that if somebody else designs your templates, such as a graphics designer, he or she doesn’t have to know anything about PHP code at all. You should be able to use supplied templates with minimum modification.

A number of template engines are available. One of the oldest and still probably the most popular one is Smarty, available from http://www.smarty.net/. A few other interesting PHP template engines are Twig (http://twig.sensiolabs.org/) and Plates (http://platesphp.com/). Take a look at these and others out there to get a sense for what might be useful to you and your organization.

Optimizing CodeIf you come from a non-web programming background, optimization can seem really important. When PHP is used, most of a user’s wait for a web application comes from connection and download times. Optimization of your code has little effect on these times.

Using Simple OptimizationsYou can introduce a few simple optimizations that will make a difference in connection and download times. Many of these changes, described here, relate to applications that integrate a database such as MySQL with your PHP code:

 ■ Reduce database connections. Connecting to a database is often the slowest part of any 

script.

 ■ Speed up database queries. Reduce the number of queries that you make and make sure 

that they are optimized. With a complex (and therefore slow) query, there is usually more than one way to solve your problem. Run your queries from the database’s command-line interface and experiment with different approaches to speed up things. In MySQL, you can use the EXPLAIN statement to see where a query might be going astray. (Use of this statement is discussed in Chapter 12,「Advanced MySQL Administration.」) In general, the principle is to minimize joins and maximize use of indexes.

 ■ Minimize generation of static content from PHP. If every piece of HTML you produce 

comes from echo or print(), page generation will take a good deal longer. (This is one of the arguments for shifting toward separate logic and content, as described previously.) 

Testing

541

This tip also applies to generating image buttons dynamically: You might want to use PHP to generate the buttons once and then reuse them as required. If you are generating purely static pages from functions or templates every time a page loads, consider running the functions or using the templates once and saving the result.

 ■ Use string functions instead of regular expressions where possible. They are faster.

TestingReviewing and testing code is another basic point of software engineering that is often overlooked in web development. It’s easy enough to try running the system with two or three test cases and then say,「Yup, it works fine.」This mistake is commonly made. Ensure that you have extensively tested and reviewed several scenarios before making the project production ready.

We suggest two approaches you can use to reduce the bug level of your code. (You can never eliminate bugs altogether, but you can certainly eliminate or minimize most of them.)

First, adopt a practice of code review within your team. Code review is the process in which another programmer or team of programmers looks at your code and suggests improvements. This type of analysis often suggests

 ■ Errors you have missed

 ■ Test cases you have not considered

 ■ Optimization

 ■ Improvements in security

 ■ Existing components you could use to improve a piece of code

 ■ Additional functionality

Even if you work alone, finding a「code buddy」who is in the same situation and reviewing code for each other can be a good thing.

Second, we suggest you find testers for your web applications who represent the end users of the product. The primary difference between web applications and desktop applications is that anyone and everyone will use web applications. You shouldn’t make assumptions that users will be familiar with computers. You can’t supply them with a thick manual or quick reference card. Instead, you have to make web applications self-documenting and self-evident. You must think about the ways in which users will want to use your application. Usability is absolutely paramount.

Understanding the problems that naive end users will encounter can be really difficult if you are an experienced programmer or web surfer. One way to address this problem is to find testers who represent the typical user.

542

Chapter 25  Using PHP and MySQL for Large Projects 

One way we have done this in the past is to release web applications on a beta-only basis. When you think you have the majority of the bugs out, publicize the application to a small group of test users and get a low volume of traffic through the site. Offer free services to the first 100 users in return for feedback about the site. We guarantee you that they will come up with some combination of data or usage you have not considered. If you are building a website for a client company, it can often supply a good set of naive users by getting staff at the company to work through the site. (This approach has the intrinsic benefit of increasing the client’s sense of ownership in the site.) 

Further ReadingThere is a great deal of material to cover in this area; basically, we are talking about the science of software engineering, about which many, many books have been written. For example, you might enjoy Software Engineering: A Practitioner’s Approach by Roger Pressman. Additionally, many of the topics we covered in this chapter are discussed in articles and whitepapers in the Resources section of the Zend website. You might consider going there for more information on the subject. Finally, if you found this chapter interesting, you might want to look at Extreme Programming (XP), which is a software development methodology aimed at domains where requirements change frequently, such as web development. You can learn more about Extreme Programming at http://www.extremeprogramming.org.

NextIn Chapter 26,「Debugging and Logging,」we look at different types of programming errors, PHP error messages, and techniques for finding errors.

