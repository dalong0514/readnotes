Automated Build with Phing

If version control is one side of the coin, then automated build is the other. Version control allows multiple developers to work collaboratively on a single project. With many coders each deploying a project in her own space, automated build soon becomes essential. One developer may have her web-facing directory in /usr/local/apache/htdocs; another might use /home/bibble/public_html. Developers may use different database passwords, library directories, or mail mechanisms. A flexible codebase might easily accommodate all of these differences, but the effort of changing settings and manually copying directories around your file system to get things working would soon become tiresome—especially if you need to install code in progress several times a day (or several times an hour).

You have already seen that Composer automates package installation. You’ll almost certainly want to 

deliver a project to an end user via a Composer or PEAR package because that mechanism is straightforward for the user and because package-management systems handle dependencies. But there’s a lot of work that might need automating before a package has been created. You may need to generate template-generated code, for example. You should run tests and provide mechanisms for creating and updating database tables. Finally, you may want to automate the creation of a production-ready package. In this chapter, I introduce you to Phing, which handles just such jobs. This chapter will cover the following:

Properties: Setting and getting data

•	 Getting and installing Phing: Who builds the builder?•	•	•	•	

Types: Describing complex parts of a project

Targets: Breaking a build into callable, interdependent sets of functionality

Tasks: The things that get stuff done

What Is Phing?

Phing is a PHP tool for building projects. It is very closely modeled on the hugely popular (and very powerful) Java tool called Ant. Ant was so named because it is small but capable of constructing things that are very large indeed. Both Phing and Ant use an XML file (usually named build.xml) to determine what to do in order to install or otherwise work with a project.

The PHP world really needs a good build solution. Serious developers have had a number of options in the past. First, it is possible to use make, the ubiquitous Unix build tool that is still used for most C and Perl projects. However, make is extremely picky about syntax and requires quite a lot of shell knowledge, up to and including scripting—this can be challenging for some PHP programmers who have not come to programming via the Unix or Linux command line. What’s more, make provides very few built-in tools for common build operations such as transforming file names and contents. It is really just a glue for shell commands. This makes it hard to write programs that will install across platforms. Not all environments will have the same version of make, or even have it at all. Even if you have make, you may not have all the commands the makefile (the configuration file that drives make) requires.

465

Chapter 19 ■ automated Build with phing

Phing’s relationship with make is illustrated in its name: Phing stands for PHing Is Not Gnu make. This 

playful recursion is a common coder’s joke (for example, GNU itself stands for Gnu is Not Unix).

Phing is a native PHP application that interprets a user-created XML file in order to perform operations 

on a project. Such operations would typically involve the copying of files from a distribution directory to various destination directories, but there is much more to Phing. Phing can be used to generate documentation, run tests, invoke commands, run arbitrary PHP code, create packages, replace keywords in files, strip comments, and generate tar/gzipped package releases. Even if Phing does not yet do what you need, it is designed to be easily extensible.

Because Phing is itself a PHP application, all you need to run it is a recent PHP engine. As Phing is an 

application for installing PHP applications, the presence of a PHP executable is a reasonably safe bet.

Getting and Installing Phing

If it is difficult to install an install tool, then something is surely wrong! However, assuming that you have PHP 5 or better on your system (and if you haven’t, this isn’t the book for you!), installation of Phing could not be easier.

You can acquire and install Phing with two simple commands:

$ pear channel-discover pear.phing.info$ pear install phing/phing

This will install Phing as a PEAR package. You should have write permission for your PEAR directories, 

which, on most Unix or Linux systems, will mean running the command as the root user.

 at the time of this writing, phing installed with pear is broken due to a namespacing issue. this problem 

 ■ Note will likely be resolved by the time you read this. if not, however, we have had good results using Composer.

You can also install Phing with Composer. You should add this to your composer.json file:

{    "require-dev": {        "phing/phing": "2.*"    }}

If you run into any installation problems, you should visit the download page at http://phing.info/

trac/wiki/Users/Download. You will find plenty of installation instructions there.

Composing the Build Document

You should now be ready to get cracking with Phing! Let’s test things out:

$ phing -v

Phing 2.14.0

The -v flag to the phing command causes the script to return version information. By the time you 

read this, the version number may have changed, but you should see a similar message when you run the command on your system.

466

Chapter 19 ■ automated Build with phing

 if you installed phing using Composer, the runnable script file will be installed in your local  

 ■ Note vendor/bin/ directory. to run phing you should either add this directory to your $PATH environment variable or use an explicit path to the executable.

Now I’ll run the phing command without arguments:

$ phing

Buildfile: build.xml does not exist!

As you can see, Phing is lost without instructions. By default, it will look for a file called build.xml. Let’s 

build a minimal document so that we can at least make that error message go away:

<?xml version="1.0"?><!-- build xml -->

<project name="megaquiz" default="main">    <target name="main"/></project>

This is the bare minimum you can get away with in a build file. If we save the previous example as 

build.xml and run phing again, we should get some more interesting output:

$ phing

Buildfile: /home/bob/working/megaquiz/build.xmlWarning: target 'main' has no tasks or dependencies

megaquiz > main:

BUILD FINISHED

Total time: 1.3404 second

A lot of effort to achieve precisely nothing, you may think, but we have to start somewhere! As you can see, Phing also helpfully points out there’s nothing very useful about this build file. Look again at that build file. Because we are dealing with XML, I include an XML declaration. As you probably know, XML comments look like this:

<!-- this is an XML comment. OK? -->

So, because it’s a comment, the second line in my build file is ignored. You can put as many comments as you like in your build files, and as they grow, you should make full use of this fact. Large build files can be hard to follow without suitable comments.

467

Chapter 19 ■ automated Build with phing

The real start of any build file is the project element. The project element can include up to five 

attributes. Of these, name and default are compulsory. The name attribute establishes the project’s name; default defines a target to run if none are specified on the command line. An optional description attribute can provide summary information. You can specify the context directory for the build using a basedir attribute. If this is omitted, the current working directory will be assumed. Finally, you can specify the minimum version of the Phing application with which the build file should work using phingVersion. You can see these attributes summarized in Table 19-1.

Table 19-1.  The Attributes of the Project Element

Attribute

Required

Description

Default Value

name

description

YesNoYesdefaultphingVersion No

The name of the projectA brief project summaryThe default target to runThe minimum version of Phing to run against

NoneNoneNoneNone

basedir

No

The file system context in which build will run

Current directory (.)

Once I have defined a project element, I must create at least one target—the one I reference in the 

default attribute.

TargetsTargets are similar, in some senses, to functions. A target is a set of actions grouped together to achieve an objective: to copy a directory from one place another, for example, or to generate documentation.

In my previous example, I included a bare-minimum implementation for a target:

<target name="main"/>

As you can see, a target must define at least a name attribute. I have made use of this in the project 

element. Because the default element points to the main target, this target will be invoked whenever Phing is run without command-line arguments. This was confirmed by the output:

megaquiz > main:

Targets can be organized to depend on one another. By setting up a dependency between one target 

and another, you tell Phing that the first target should not run before the target it depends on has been run. Now, I’ll add a dependency to my build file:

<?xml version="1.0"?><!-- build xml -->

<project name="megaquiz"         default="main">    <target name="runfirst" />    <target name="runsecond" depends="runfirst"/>    <target name="main" depends="runsecond"/></project>

468

Chapter 19 ■ automated Build with phing

As you can see, I have introduced a new attribute for the target element. depends tells Phing that the referenced target should be executed before the current one, so I might want a target that copies certain files to a directory to be invoked before one that runs a transformation on all files in that directory. I added two new targets in the example: runsecond, on which main depends; and runfirst, on which runsecond depends. Here’s what happens when I run Phing with this build file:

$ phing

Buildfile: /home/bob/working/megaquiz/build.xmlWarning: target 'runfirst' has no tasks or dependencies

megaquiz > runfirst:megaquiz > runsecond:megaquiz > main:

BUILD FINISHED

Total time: 0.3029 seconds

As you can see, the dependencies are honored. Phing encounters the main target, sees its dependency, 

and moves back to runsecond. runsecond has its own dependency, and Phing invokes runfirst. Having satisfied its dependency, Phing can invoke runsecond. Finally, main is invoked. The depends attribute can reference more than one target at a time. A comma-separated list of dependencies can be provided, and each will be honored in turn.

Now that I have more than one target to play with, I can override the project element’s default attribute 

from the command line:

$ phing runsecond

Buildfile: /home/bob/working/megaquiz/build.xmlWarning: target 'runfirst' has no tasks or dependencies

megaquiz > runfirst:megaquiz > runsecond:

BUILD FINISHED

Total time: 0.2671 seconds

By passing in a target name, I cause the default attribute to be ignored. The target matching my 

argument is invoked instead (as well as the target on which it depends). This is useful for invoking specialized tasks, such as cleaning up a build directory or running post-install scripts.

The target element also supports an optional description attribute, to which you can assign a brief 

description of the target’s purpose:

<?xml version="1.0"?><!-- build xml -->

<project name="megaquiz"         default="main"

469

Chapter 19 ■ automated Build with phing

         description="A quiz engine">    <target name="runfirst"            description="The first target" />    <target name="runsecond"            depends="runfirst"            description="The second target" />    <target name="main"            depends="runsecond"            description="The main target" /></project>

Adding a description to your targets makes no difference to the normal build process. If the user runs 

Phing with a -projecthelp flag, however, the descriptions will be used to summarize the project:

$ phing -projecthelp

Buildfile: /home/bob/working/megaquiz/build.xmlWarning: target 'runfirst' has no tasks or dependenciesA quiz engineDefault target:------------------------------------------------------------------------------- main       The main target

Main targets:------------------------------------------------------------------------------- main       The main target runfirst   The first target runsecond  The second target

Notice that I added the description attribute to the project element, too. If you want to hide a target from a listing like this, you can add a hidden attribute. This is useful for targets that provide housekeeping functionality, but which should not be invoked directly from the command line:

    <target name="housekeeping" hidden="true">        <!-- useful things that should not be called directly -->    </target>

PropertiesPhing allows you to set such values using the property element.

Properties are similar to global variables in a script. As such, they are often declared toward the top of a project to make it easy for developers to work out what’s what in the build file. Here I create a build file that works with database information:

<?xml version="1.0"?><!-- build xml -->

<project name="megaquiz"         default="main">

470

Chapter 19 ■ automated Build with phing

    <property name="dbname" value="megaquiz" />    <property name="dbpass" value="default" />    <property name="dbhost" value="localhost" />

    <target name="main">        <echo>database: ${dbname}</echo>        <echo>pass:     ${dbpass}</echo>        <echo>host:     ${dbhost}</echo>    </target></project>

I introduced a new element: property. property requires name and value attributes. Notice also that 

I have added this to the main target. echo is an example of a task. I will explore tasks more fully in the next section. For now, though, it’s enough to know that echo does exactly what you would expect—it causes its contents to be output. Notice the syntax used to reference the value of a property here. By using a dollar sign, and wrapping the property name in curly brackets, you tell Phing to replace the string with the property value:

${propertyname}

All this build file achieves is to declare three properties and to print them to standard output. Here it is 

in action:

$ phing

Buildfile: /home/bob/working/megaquiz/build.xml

megaquiz > main:

     [echo] database: megaquiz     [echo] pass:     default     [echo] host:     localhost

BUILD FINISHED

Total time: 0.4402 seconds

Now that I have introduced properties, I can wrap up my exploration of targets. The target element accepts two additional attributes: if and unless. Each of these should be set with the name of a property. When you use if with a property name, the target will only be executed if the given property is set. If the property is not set, the target will exit silently. Here, I comment out the dbpass property and make the main task require it using the if attribute:

    <property name="dbname"  value="megaquiz" />    <!--<property name="dbpass"  value="default" />-->    <property name="dbhost" value="localhost" />

    <target name="main" if="dbpass">        <echo>database: ${dbname}</echo>        <echo>pass:     ${dbpass}</echo>        <echo>host:     ${dbhost}</echo>    </target>

471

Chapter 19 ■ automated Build with phing

Let’s run phing again:

$ phing

Buildfile: /home/bob/working/megaquiz/build.xmlmegaquiz > main:

BUILD FINISHED

Total time: 0.2628 seconds

As you can see, I have raised no error, but the main task did not run. Why might I want to do this? There is another way of setting properties in a project. They can be specified on the command line. You tell Phing that you are passing it a property with the -D flag followed by a property assignment. So the argument should look like this:

-Dname=value

In my example, I want the dbname property to be made available via the command line:

$ phing -Ddbpass=userset

Buildfile: /home/bob/working/megaquiz/build.xml

megaquiz > main:

     [echo] database: megaquiz     [echo] pass:     userset     [echo] host:     localhost

BUILD FINISHED

Total time: 0.4611 seconds

The if attribute of the main target is satisfied that the dbpass property is present, and the target is 

allowed to execute.

As you might expect, the unless attribute is the opposite of if. If a property is set and it is referenced 

in a target’s unless attribute, then the target will not run. This is useful if you want to make it possible to suppress a particular target from the command line. So I might add something like this to the main target:

<target name="main" unless="suppressmain">

main will be executed unless a suppressmain property is present:

$ phing -Dsuppressmain=yes

I have wrapped up the target element; Table 19-2 shows a summary of its attributes.

472

Chapter 19 ■ automated Build with phing

Table 19-2.  The Attributes of the Target Element

Attribute

Required

Description

name

depends

if

unless

logskipped

hidden

description

YesNoNoNoNo

No

No

The name of the targetTargets on which the current dependsExecute target only if given property is presentExecute target only if given property is not presentIf a target is skipped (e.g., because of if / unless), add a notification to outputHide target from lists and summaries

A short summary of the target’s purpose

When a property is set on the command line, it overrides any and all property declarations within the 

build file. There is another condition in which a property value can be overwritten. By default, if a property is declared twice, the original value will have primacy. You can alter this behavior by setting an attribute called override in the second property element. Here’s an example:

<?xml version="1.0"?><!-- build xml -->

<project name="megaquiz"         default="main">

    <property name="dbpass"  value="default" />

    <target name="main">        <property name="dbpass" override="yes" value="specific" />        <echo>pass:     ${dbpass}</echo>    </target>

</project>

I set a property called dbpass, giving it the initial value "default". In the main target I set the property once again, adding an override attribute set to "yes" and providing a new value. The new value is reflected in the output:

$ phing

Buildfile: /home/bob/working/megaquiz/build.xml

megaquiz > main:

     [echo] pass:     specific

BUILD FINISHED

473

Chapter 19 ■ automated Build with phing

If I had not set the override element in the second property element, the original value of "default" 

would have stayed in place. It is important to note that targets are not functions: there is no concept of local scope. If you override a property within a task, it remains overridden for all other tasks throughout the build file. You could get around this, of course, by storing a property value in a temporary property before overriding, and then resetting it when you have finished working locally.

So far, I have dealt with properties that you define yourself. Phing also provides built-in properties. You 

reference these in exactly the same way that you would reference properties you have declared yourself. Here’s an example:

<?xml version="1.0"?><!-- build xml -->

<project name="megaquiz"         default="main">

    <target name="main">        <echo>name:     ${phing.project.name}</echo>        <echo>base:     ${project.basedir}</echo>        <echo>home:     ${user.home}</echo>        <echo>pass:     ${env.DBPASS}</echo>    </target>

</project>

I reference just a few of the built-in Phing properties. phing.project.name resolves to the name of the project as defined in the name attribute of the project element; project.basedir gives the starting directory; and user.home provides the executing user’s home directory (this is useful for providing default install locations).

Finally, the env prefix in a property reference indicates an operating system environment variable. So by 

specifying ${env.DBPASS}, I am looking for an environment variable called DBPASS. Here I run Phing on this file:

$ phing

Buildfile: /home/bob/working/megaquiz/build.xml

megaquiz > main:

     [echo] name:     megaquiz     [echo] base:     /home/bob/working/megaquiz     [echo] home:     /home/bob     [echo] pass:     ${env.DBPASS}

BUILD FINISHED

Total time: 0.1120 seconds

Notice that the final property has not been translated. This is the default behavior when a property is 

not found—the string referencing the property is left untransformed. If I set the DBPASS environment variable and run again, I should see the variable reflected in the output:

474

Chapter 19 ■ automated Build with phing

$ export DBPASS=wooshpoppow$ phing

Buildfile: /home/bob/working/megaquiz/build.xml

megaquiz > main:     ...     [echo] pass:     whooshpoppow

BUILD FINISHED

Total time: 0.2852 seconds

So now you have seen three ways of setting a property: the property element, a command-line 

argument, and an environment variable.

There is a fourth approach that complements these. You can use a separate file to specify property values. As my projects grow in complexity, I tend to favor this approach. Let’s return to a basic build file:

<?xml version="1.0"?><!-- build xml -->

<project name="megaquiz"         default="main">

    <target name="main">        <echo>database: ${dbname}</echo>        <echo>pass:     ${dbpass}</echo>        <echo>host:     ${dbhost}</echo>    </target></project>

As you can see, this build file simply outputs properties without first declaring them, or checking that 

their values exist. This is what I get when I run this with no arguments:

$ phing

...     [echo] database: ${dbname}     [echo] pass:     ${dbpass}     [echo] host:     ${dbhost}...

Now I’ll declare my properties in a separate file. I’ll call it megaquiz.properties:

dbname=filedbdbpass=filepassdbhost=filehost

Now I can apply this file to my build process with Phing’s propertyfile option:

475

Chapter 19 ■ automated Build with phing

$ phing -propertyfile megaquiz.properties

...     [echo] database: filedb     [echo] pass:     filepass     [echo] host:     filehost...

I find this mechanism much more convenient than managing long lists of command-line options. 

However, you do need to be careful not to check your property file into your version-control system!

You can use targets to ensure that properties are populated. Let’s say, for example, that my project 

requires a dbpass property. I would like the user to set dbpass on the command line (this always has priority over other property-assignment methods). Failing that, I should look for an environment variable. Finally, I should give up and go for a default value:

<?xml version="1.0"?><!-- build xml -->

<project name="megaquiz"         default="main">

    <target name="setenvpass" if="env.DBPASS" unless="dbpass">        <property name="dbpass" override="yes" value="${env.DBPASS}" />    </target>

    <target name="setpass" unless="dbpass" depends="setenvpass">        <property name="dbpass" override="yes" value="default" />    </target>

    <target name="main" depends="setpass">        <echo>pass:     ${dbpass}</echo>    </target>

</project>

So, as usual, the default target main is invoked first. This has a dependency set, so Phing goes back to the 

setpass target. setpass, though, depends on setenvpass, so I start there. setenvpass is configured to run only if dbpass has not been set and if env.DBPASS is present. If these conditions are met, then I set the dbpass property using the property element. At this stage then, dbpass is populated either by a command-line argument or by an environment variable. If neither of these were present, then the property would remain unset at this stage. The setpass target is now executed, but only if dbpass is not yet present. In this case, it sets the property to the default string: "default".

Conditionally Setting Property Values with the Condition TaskThe previous example set up quite a complex assignment logic. More often, however, you’ll need a simple default value. The condition task allows you to set a property’s value based upon configurable conditions. Here is an example:

476

Chapter 19 ■ automated Build with phing

<?xml version="1.0"?>

<!-- build xml -->

<project name="megaquiz"         default="main">

    <condition property="dbpass" value="default">        <not>            <isset property="dbpass" />        </not>    </condition>

    <target name="main">        <echo>pass:     ${dbpass}</echo>    </target>

</project>

The condition task requires a property attribute. It also optionally accepts a value attribute, which is assigned to the property if the nested test clause resolves to true. If no value attribute is provided, then the property will be set to true if the nested test resolves to true.

The test clause is one of a number of tags, some of which, like not in this example, accept their own 

nested elements. I used the isset element, which returns true if the referenced property is set. Because I want to assign a value to the dbpass property if it is not set, I need to negate this result by wrapping it in the not tag. This inverts the resolution of the tag it contains. So, in terms of PHP syntax, the condition task in my example is analogous to this:

if (! isset($dbpass)) {    $dbpass = "default";}

TypesYou may think that having looked at properties, you are now through with data. In fact, Phing supports a set of special elements called types. These encapsulate different kinds of information useful to the build process.

FileSetLet’s say that you need to represent a directory in your build file. This is a common situation as you might imagine. You could use a property to represent this directory, certainly, but you’d run into problems straightaway if your developers use different platforms that support distinct directory separators. The answer is the FileSet data type. FileSet is platform independent, so if you represent a directory with forward slashes in the path, they will be automatically translated behind the scenes into backslashes when the build is run on a Windows machine. You can define a minimal fileset element like this:

    <fileset dir="src/lib" />

477

Chapter 19 ■ automated Build with phing

As you can see, I use the dir attribute to set the directory I wish to represent. You can optionally add an 

id attribute, so that you can refer to the fileset later on:

    <fileset dir="src/lib" id="srclib">

The FileSet data type is particularly useful in specifying types of documents to include or exclude. 

When installing a set of files, you may not wish those that match a certain pattern to be included. You can handle conditions like this in an excludes attribute:

    <fileset dir="src/lib" id="srclib"         excludes="**/*_test.php **/*Test.php" />

Notice the syntax I have used in the excludes attribute. Double asterisks represent any directory or subdirectory within src/lib. A single asterisk represents zero or more characters. So I am specifying that I would like to exclude files that end in _test.php or Test.php in all directories below the starting point defined in the dir attribute. The excludes attribute accepts multiple patterns separated by white space.I can apply the same syntax to an includes attribute. Perhaps my src/lib directories contain many 

non-PHP files that are useful to developers, but which should not find their way into an installation. I could exclude those files, of course, but it might be simpler just to define the kinds of files I can include. In this case, if a file doesn’t end in .php, it isn’t going to be installed:

    <fileset dir="src/lib" id="srclib"         excludes="**/*_test.php **/*Test.php"         includes="**/*.php" />

As you build up include and exclude rules, your fileset element is likely to become overly long. 

Luckily, you can pull out individual exclude rules and place each one in its own exclude subelement. You can do the same for include rules. I can now rewrite my FileSet like this:

    <fileset dir="src/lib" id="srclib">        <exclude name="**/*_test.php" />        <exclude name="**/*Test.php" />        <include name="**/*.php" />    </fileset>

You can see some of the attributes of the fileset element in Table 19-3.

Table 19-3.  Some Attributes of the Fileset Element

Attribute

Required

Description

refid

NoNodirexpandsymboliclinks NoNoincludes

excludes

No

Current fileset is a reference to fileset of given IDThe starting directoryIf set to 'true' follow symbolic linksA comma-separated list of patterns—those that match will be included

A comma-separated list of patterns—those that match will be excluded

478

Chapter 19 ■ automated Build with phing

PatternSetAs you build up patterns in your fileset elements (and in others), there is a danger that you will begin to repeat groups of exclude and include elements. In my previous example, I defined patterns for test files and regular code files. I may add to these over time (perhaps I wish to include .conf and .inc extensions to my definition of code files). If I define other fileset elements that also use these patterns, I will be forced to make any adjustments across all relevant fileset elements.

You can overcome this problem by grouping patterns into patternset elements. The patternset 

element groups include and exclude elements so that they can be referenced later from within other types. Here I extract the include and exclude elements from my fileset example and add them to patternset elements:

    <patternset id="inc_code">        <include name="**/*.php" />        <include name="**/*.inc" />        <include name="**/*.conf" />    </patternset>

    <patternset id="exc_test">        <exclude name="**/*_test.php" />        <exclude name="**/*Test.php" />    </patternset>

I create two patternset elements, setting their id attributes to inc_code and exc_test respectively. 

inc_code contains the include elements for including code files, and exc_test contains the exclude files for excluding test files. I can now reference these patternset elements within a fileset:

    <fileset dir="src/lib" id="srclib">        <patternset refid="inc_code" />        <patternset refid="exc_test" />    </fileset>

To reference an existing patternset, you must use another patternset element. The second element must set a single attribute: refid. The refid attribute should refer to the id of the patternset element you wish to use in the current context. In this way, I can reuse patternset elements across different fileset elements:

    <fileset dir="src/views" id="srcviews">        <patternset refid="inc_code" />    </fileset>

Any changes I make to the inc_code patternset will automatically update any types that use it. As with 

FileSet, you can place exclude rules either in an excludes attribute or a set of exclude subelements. The same is true of include rules.

Some patternset element attributes are summarized in Table 19-4.

479

Chapter 19 ■ automated Build with phing

Table 19-4.  Some Attributes of the Patternset Element

Attribute

Required

Description

id

excludes

includes

refid

NoNoNo

No

A unique handle for referring to the elementA list of patterns for exclusionA list of patterns for inclusion

Current patternset is a reference to patternset of given ID

FilterChainThe types that I have encountered so far have provided mechanisms for selecting sets of files. FilterChain, by contrast, provides a flexible mechanism for transforming the contents of text files.

In common with all types, defining a filterchain element does not in itself cause any changes to take place. The element and its children must first be associated with a task—that is, an element that tells Phing to take a course of action. I will return to tasks a little later.

A filterchain element groups any number of filters together. Filters operate on files like a pipeline—the first alters its file and passes its results on to the second, which makes its own alterations, and so on. By combining multiple filters in a filterchain element, you can effect flexible transformations.

Here I dive straight in and create a filterchain that removes PHP comments from any text passed to it:

<filterchain>    <stripphpcomments /></filterchain>

The StripPhpComments task does just what the name suggests. If you have provided detailed API 

documentation in your source code, you may have made life easy for developers, but you have also added a lot of dead weight to your project. Because all the work that matters takes place within your source directories, there is no reason why you should not strip out comments on installation.

 if you use a build tool for your projects, ensure that no-one makes changes in the installed code. the 

 ■ Note installer will copy over any altered files, and the changes will be lost. i have seen it happen.

Let’s sneak a peek at the next section and place the filterchain element in a task:

    <target name="main">        <copy todir="build/lib">            <fileset refid="srclib"/>            <filterchain>                <stripphpcomments />            </filterchain>        </copy>    </target>

The Copy task is probably the one you get most use out of. It copies files from place to place. As you can see, I define the destination directory in the todir attribute. The source of the files is defined by the fileset element I created in the previous section. Then comes the filterchain element. Any file copied by the Copy task will have this transformation applied to it.

480

Chapter 19 ■ automated Build with phing

Phing supports filters for many operations, including stripping new lines (StripLineBreaks) and 

replacing tabs with spaces (TabToSpaces). There is even an XsltFilter for applying XSLT transformations to source files! Perhaps the most commonly used filter, however, is ReplaceTokens. This allows you to swap tokens in your source code for properties defined in your build file, whether pulled from environment variables or passed in on the command line. This is very useful for customizing an installation. It’s a good idea to centralize your tokens into a central configuration file for easy overview of the variable aspects of your project.

ReplaceTokens optionally accepts two attributes, begintoken and endtoken. You can use these to define 

the characters that delineate token boundaries. If you omit these, Phing will assume the default character of @. In order to recognize and replace tokens, you must add token elements to the replacetokens element. Now I’ll add a replacetokens element to my example:

    <copy todir="build/lib">        <fileset refid="srclib"/>        <filterchain>            <stripphpcomments />            <replacetokens>                <token key="dbname" value="${dbname}" />                <token key="dbhost" value="${dbhost}" />                <token key="dbpass" value="${dbpass}" />            </replacetokens>        </filterchain>    </copy>

As you can see, token elements require key and value attributes. Let’s see the effect of  

running this task with its transformations on a file in my project. The original file lives in a source directory, src/lib/Config.php:

/** * Quick and dirty Conf class**/class Config {    public $dbname ="@dbname@";    public $dbpass ="@dbpass@";    public $dbhost ="@dbhost@";}

Running my main target containing the Copy task defined previously gives the following output:

$ phing

Buildfile: /home/bob/working/megaquiz/build.xml

megaquiz > main:

     [copy] Copying 8 files to /home/bob/working/megaquiz/build/lib

BUILD FINISHED

Total time: 0.1413 seconds

The original file is untouched, of course, but thanks to the Copy task, it has been reproduced at build/

lib/Config.php:

481

Chapter 19 ■ automated Build with phing

class Config {    public $dbname ="megaquiz";    public $dbpass ="default";    public $dbhost ="localhost";}

Not only has the comment been removed, but the tokens have been replaced with their property 

equivalents.

TasksTasks are the elements in a build file that get things done. You won’t achieve much without using a task, which is why I have cheated and used a couple already. I’ll reintroduce these.

EchoThe Echo task is perfect for the obligatory「Hello World」example. In the real world, you can use it to tell the user what you are about to do or what you have done. You can also sanity-check your build process by displaying the values of properties. As you have seen, any text placed within the opening and closing tags of an echo element will be printed to the browser:

<echo>The pass is '${dbpass}', shhh!</echo>

Alternatively, you can add the output message to a msg attribute:

<echo msg="The pass is '${dbpass}', shhh!" />

This will have the identical effect of printing the following to standard output:

[echo] The pass is 'default', shhh!

CopyCopying is really what installation is all about. Typically, you will create one target that copies files from your source directories and assembles them in a temporary build directory. You will then have another target that copies the assembled (and transformed) files to their output locations. Breaking the installation into separate build and install phases is not absolutely necessary, but it does mean that you can check the results of the initial build before committing to overwriting production code. You can also change a property and install again to a different location without the need to run a potentially expensive copy/replace phase again.

At its simplest, the Copy task allows you to specify a source file and a destination directory or file:

<copy file="src/lib/Config.php" todir="build/conf" />

As you can see, I specify the source file using the file attribute. You may be familiar already with the 

todir attribute, which is used to specify the target directory. If the target directory does not exist, Phing will create it for you.

If you need to specify a target file, rather than a containing directory, you can use the tofile attribute 

instead of todir:

<copy file="src/lib/Config.php" tofile="build/conf/myConfig.php" />

482

Once again, the build/conf directory is created if necessary, but this time, Config.php is renamed to 

myConfig.php.

As you have seen, to copy more than one file at a time, you need to add a fileset element to copy:

Chapter 19 ■ automated Build with phing

        <copy todir="build/lib">            <fileset refid="srclib"/>        </copy>

The source files are defined by the srclib fileset element, so all you have to set in copy is the todir 

attribute.

Phing is smart enough to test whether or not your source file has been changed since the target file was created. If no change has been made, then Phing will not copy. This means that you can build many times, and only the files that have changed in the meantime will be installed. This is fine, as long as other things are not likely to change. If a file is transformed according to the configuration of a replacetokens element, for example, you may want to ensure that the file is transformed every time that the Copy task is invoked. You can do this by setting an overwrite attribute:

        <copy todir="build/lib" overwrite="yes">            <fileset refid="srclib"/>            <filterchain>                <stripphpcomments />                <replacetokens>                    <token key="dbpass" value="${dbpass}" />                </replacetokens>            </filterchain>        </copy>

Now whenever copy is run, the files matched by the fileset element are replaced whether or not the 

source has been recently updated.

You can see the copy element summarized in Table 19-5.

Table 19-5.  The Attributes of the Copy Element

Required

Description

Default Value

Attribute

todir

tofile

tstamp

None

None

false

false

false755

true

no

483

Yes (if tofile not present)Yes (if todir not present)No

Directory to copy into

The file to copy to

Match the timestamp of any file overwritten (it will appear unaltered)Match the permissions of any file overwrittenCopy empty directories overSet the (octal) modeBuild process will be stopped if an error encountered

Nopreservemodeincludeemptydirs NoNomodeNo

haltonerror

overwrite

No

Overwrite target if it already exists

Chapter 19 ■ automated Build with phing

InputYou have seen that the echo element is used to send output to the user. To gather input from the user, I have used separate methods involving the command line and an environment variable. These mechanisms are neither very structured nor interactive, however.

 one reason for allowing users to set values at build time is to allow for flexibility from build 

 ■ Note environment to build environment. in the case of database passwords, another benefit is that this sensitive data is not enshrined in the build file itself. of course, once the build has been run, the password will be saved into a source file, so it is up to the developer to ensure the security of his system!

The input element allows you to present the user with a prompt message. Phing then awaits input 

which it assigns it to a property. Here’s an example:

    <target name="setpass" unless="dbpass">        <input message="You don't seem to have set a db password"               propertyName="dbpass"               defaultValue="default"               promptChar=" >" />    </target>

    <target name="main" depends="setpass">        <echo>pass:     ${dbpass}</echo>    </target>

Once again, I have a default target: main. This depends on another target, setpass, which is responsible 

for ensuring that the dbpass property is populated. To this end, I use the target element’s unless attribute, which ensures that it will not run if dbpass is already set.

The setpass target consists of a single input task element. An input element can have a message 

attribute, which should contain a prompt for the user. The propertyName attribute is required and defines the property to be populated by user input. If the user presses Enter at the prompt without setting a value, the property is given a fallback value if the defaultValue attribute is set. Finally, you can customize the prompt character using the promptChar attribute—this provides a visual cue for the user to input data. Let’s run Phing using the previous targets:

$ phingBuildfile: /home/bob/working/megaquiz/build.xml

megaquiz > setpass:You don't seem to have set a db password [default] > mypassmegaquiz > main:     [echo] pass:     mypass

BUILD FINISHED

Total time: 6.0322 seconds

484

Chapter 19 ■ automated Build with phing

The input element is summarized in Table 19-6.

Table 19-6.  The Attributes of the Input Element

Attribute

Required

Description

propertyName

message

defaultValue

validArgs

promptChar

YesNoNoNo

No

The property to populate with user inputThe prompt messageA value to assign to the property if the user does not provide inputA list of acceptable input values separated by commas. If the user inputs a value that is not on this list Phing will re-present the prompt

A visual cue that the user should provide input

DeleteInstallation is generally about creating, copying, and transforming files. Deletion has its place as well, however. This is particularly the case when you wish to perform a clean install. As I have already discussed, files are generally only copied from source to destination for source files that have changed since the last build. By deleting a build directory, you ensure that the full compilation process will take place.

Here I delete a directory:

    <target name="clean">        <delete dir="build" />    </target>

When I run phing with the argument clean (the name of the target), my delete task element is invoked. 

Here’s Phing’s output:

$ phing clean

Buildfile: /home/bob/working/megaquiz/build.xmlmegaquiz > clean:   [delete] Deleting directory /home/bob/working/megaquiz/build

BUILD FINISHED

The delete element accepts an attribute, file, which can be used to point to a particular file. 

Alternatively, you can fine-tune your deletions by adding a fileset subelement to delete.

Summary

Serious development rarely happens all in one place. A codebase needs to be separated from its installation, so that work in progress does not pollute production code that needs to remain functional at all times. Version control allows developers to check out a project and work on it in their own space. This requires that they should be able to configure the project easily for their environments. Finally, and perhaps most importantly, the customer (even if the customer is yourself in a year’s time, when you’ve forgotten the ins-and-outs of your code) should be able to install your project after a glance at a Read Me file.

485

Chapter 19 ■ automated Build with phing

In this chapter, I have covered some of the basics of Phing, a fantastic tool, which brings much of the 

functionality of Apache Ant to the PHP world. I have only scratched the surface of Phing’s capabilities. Nevertheless, once you are up and running with the targets, tasks, types, and properties discussed here, you’ll find it easy to bolt on new elements for advanced features like creating tar/gzipped distributions, automatically generating PEAR package installations, and running PHP code directly from the build file.

If Phing does not satisfy all your build needs, you will discover that, like Ant, it is designed to be 

extensible—get out there and build your own tasks! Even if you don’t add to Phing, you should take some time to examine the source code. Phing is written entirely in object-oriented PHP, and its code is chock-full of design examples.

486

CHAPTER 20

Vagrant

Where do you run your code?

Maybe you have a development environment you have honed to perfection with a favorite editor and 

any number of useful development tools. Of course, your perfect set up for writing code is probably very different from the best system on which to run it. And that’s a challenge that Vagrant can help you with. Using Vagrant you get to work on your local machine and run your code on a system that’s all but identical to your production server. In this chapter I will show you how. We will cover the following:

Basic set up: From installation to choosing your first box

•	•	•	 Mounting host directories: Editing code on your host machine and having it available 

Logging in: Investigating your virtual machine with ssh

transparently in your Vagrant box

•	•	

Provisioning: Writing a script to install packages and configure Apache and MySQL

Set a hostname: Configuring your box so that you can access it using a custom hostname

The Problem

As always, let’s spend a little time defining the problem space. It is relatively easy, these days, to configure a LAMP stack on most desktop or laptop computers. Even so, a personal computer is unlikely to match your production environment. Is it running the same version of PHP? What about Apache and MySQL? If you’re using Elasticsearch, you may need to consider Java, too. The list soon grows. Developing against one set of tools on a particular platform can sometimes be problematic if your production stack is significantly different.

You might give up and shift your development to a remote machine—there are plenty of cloud vendors who will allow you to spin up a box quickly. But that’s not a free option, and, depending upon your editor of choice, a remote system may not integrate well with the development tools you wish to use.

So it may be worth the effort of matching the packages on your computer as closely as possible with 

those installed on the production system. The match won’t be perfect, but perhaps it will be good enough, and you’ll probably catch most issues on the staging server.

What happens, though, when you begin work on a second project with radically different requirements? 

We have seen that Composer does a great job of keeping dependencies separate, but there are still global packages like PHP, MySQL, and Apache to keep in line.

 ■ Note  If you decide to develop on remote systems, I recommend making the effort to learn how to use the vim editor. Despite its quirks, it is extremely powerful, and you can be 99% certain that either vim or its more basic ancestor vi will available on any Unix-like system you encounter.

487

Chapter 20 ■ Vagrant

Virtualization is a potential solution, and a good one. It can be a pain installing an operating system, 

though, and there can be considerable configuration hassles.

If only there were a tool that made creating a production-like development environment on a local 

machine really simple. OK, it’s obvious that now I’m going to say that just such a tool exists. Well, one does. It’s called Vagrant, and it is truly amazing.

A Little Setup

It is tempting to say that Vagrant gives you a development environment with a single command. That can be true—but you do have to install the requisite software first. Given that, and a configuration file that you can check out from your project’s version-control repository, launching a new environment truly can involve a single command.

Let’s get started with the setup first. Vagrant requires a virtualization platform. It supports several, but I will use VirtualBox. My host machine runs Fedora, but you can install VirtualBox on any Linux distribution and on OSX or Windows. You can find the download page at https://www.virtualbox.org/wiki/Downloads, together with instructions for your platform.

Once you have VirtualBox installed, you’ll need Vagrant, of course. The download page is at https://www.vagrantup.com/downloads.html. Once we have installed these applications, our next task will be to choose the box we’ll run our code on.

Choosing and Installing a Vagrant BoxProbably the easiest way to acquire a Vagrant box is to use the search interface at https://atlas.hashicorp.com/search. Since many production systems run CentOS, that’s what I will look for. You can see the fruits of my research in Figure 20-1.

Figure 20-1.  Searching for a Vagrant box

488

CentOS 6.7 looks about right for my needs. I now have enough information to get a Vagrant 

environment running. Usually when you run Vagrant, it will read a configuration file named Vagrantfile—but since I am starting from scratch, I need to ask Vagrant to generate one:

Chapter 20 ■ Vagrant

$ vagrant init bento/centos-6.7

A 'Vagrantfile' has been placed in this directory. You are nowready to 'vagrant up' your first virtual environment! Please readthe comments in the Vagrantfile as well as documentation on'vagrantup.com' for more information on using Vagrant.

As you can see, I pass Vagrant the name of the box I want to work with, and it uses this information to 

generate some minimal configuration.

If I open up the generated Vagrantfile document, I can see this (among much other boilerplate):

  # Every Vagrant development environment requires a box. You can search for  # boxes at https://atlas.hashicorp.com/search.  config.vm.box = "bento/centos-6.7"

At this point, I have only gotten as far as generating configuration. Next, I must run the all-important 

vagrant up command. If you work with Vagrant often, you will soon find this command very familiar. It kicks off your Vagrant session by downloading and provisioning your new box (if necessary), then booting it:

$ vagrant up

Because I am running this command for the first time with the bento/centos-6.7 virtual machine, 

Vagrant starts by downloading the box:

Bringing machine 'default' up with 'virtualbox' provider...==> default: Box 'bento/centos-6.7' could not be found. Attempting to find and install...    default: Box Provider: virtualbox    default: Box Version: >= 0==> default: Loading metadata for box 'bento/centos-6.7'    default: URL: https://atlas.hashicorp.com/bento/centos-6.7==> default: Adding box 'bento/centos-6.7' (v2.2.7) for provider: virtualbox    default: Downloading: https://atlas.hashicorp.com/bento/boxes/centos-6.7/versions/2.2.7/providers/virtualbox.box==> default: Successfully added box 'bento/centos-6.7' (v2.2.7) for 'virtualbox'!

Vagrant stores the box (under ~/.vagrant.d/boxes/ if you are running Linux) so that you won’t have to download it again on your system—even if you run multiple virtual machines. Then it configures and boots the machine (it provides lots of detail as it does so). Once it has finished running, I can test it out by logging in to my new machine:

$ vagrant ssh$ pwd

/home/vagrant

$ cat /etc/redhat-release

489

Chapter 20 ■ Vagrant

CentOS release 6.7 (Final)

We’re in! So what have we won? Well, we have access to a machine that somewhat resembles our 

production environment. Anything else? Quite a lot, in fact. I said earlier that I would like to edit files on my local machine but run them in a production-like space. Let’s set that up.

Mounting Local Directories on the Vagrant Box

Let’s put some sample files together. I ran my first vagrant init and vagrant up commands in a directory I named infrastructure. I will resurrect the webwoo project I used in Chapter 18 (a cut down version of the system I developed for Chapter 12). Putting all that together, my development environment looks a little like this:

ch20/    infrastructure/        Vagrantfile    webwoo/         AddVenue.php         index.php         Main.php         AddSpace.php

Our challenge is to set up the environment so that we can work with webwoo files locally, but run them 

transparently using a stack installed on the CentOS box. Depending upon our configuration, Vagrant will attempt to mount directories on the host machine within the guest box. In fact, Vagrant has already mounted one directory for us. Let’s check it out:

$ vagrant ssh

Last login: Tue Jul  5 15:36:19 2016 from 10.0.2.2

$ ls -a /vagrant

.  ..   .vagrant  Vagrantfile

So Vagrant has mounted the infrastructure directory as /vagrant on the box. That will come in handy 

when we write a script to provision the box. For now, though, let’s focus on mounting the webwoo directory. We can do this by editing Vagrantfile:

    config.vm.synced_folder "../webwoo", "/var/www/poppch20"

So with this directive, I am telling Vagrant to mount the webwoo directory on the guest box at /var/www/

poppch20. In order to see that in effect, I need to reboot the box. There’s a new command for this (which should be run on the host system and not within the virtual machine):

$ vagrant reload

The virtual machine shuts down and reboots cleanly. Vagrant mounts the infrastructure (/vagrant)

and webwoo (/var/www/poppch20) directories. Here’s an extract from the command’s output:

490

Chapter 20 ■ Vagrant

    ==> default: Mounting shared folders...    default: /vagrant => /home/mattz/ch20/infrastructure    default: /var/www/poppch20 => /home/mattz/ch20/webwoo

I can log in quickly to confirm that /var/www/poppch20 is in place:

$ vagrant ssh

Last login: Thu Jul  7 15:25:16 2016 from 10.0.2.2

$ ls /var/www/poppch20/

AddSpace.php  AddVenue.php  index.php  Main.php

So now I can run a sexy IDE on my local machine and have the changes it makes transparently available 

on the guest box!

Of course, placing files on a CentOS VM is not the same as running the system. A typical Vagrant box 

comes without too much pre-installed. The assumption is that the developer will want to customize the environment according to need and circumstance.

The next stage is to provision our box.

Provisioning

Once again, provisioning is directed by the Vagrantfile document. Vagrant supports several tools designed for provisioning machines, including chef (https://www.chef.io/chef/), puppet (https://puppet.com), and ansible (https://www.ansible.com). They’re all worth investigating. For the purposes of this example, though, I’m going to use a good old-fashioned shell script.

Once again I begin with Vagrantfile:

config.vm.provision "shell", path: "setup.sh"

This should be reasonably clear. I’m telling Vagrant to use a shell script to provision my box, and I 

specify setup.sh as the script which should be executed.

What you put in your shell script depends upon your requirements, of course. I’m going to begin by 

setting t couple of variables, and installing some packages:

#!/bin/bash

VAGRANTDIR=/vagrantSERVERDIR=/var/www/poppch20/

sudo rpm -Uvh https://mirror.webtatic.com/yum/el6/latest.rpmsudo yum install -y patchsudo yum install -y vim

sudo yum -q -y install mysql-serversudo yum -q -y install httpd;sudo yum -q -y install php70wsudo yum -q -y install php70w-mysql

491

Chapter 20 ■ Vagrant

sudo yum -q -y install php70w-xmlsudo yum -q -y install php70w-dom

PHP 7 is not available by default on CentOS 6. However, installing a yum repository from webtatic.

com provides access to a package named php70w and a stack of related extensions. I write my script to a file named setup.sh which I place in the infrastructure directory alongside Vagrantfile.

Now, how do I kick off the provisioning process? If the config.vm.provision directive and the setup.sh script had both been in place when I ran vagrant up, then the provisioning would have been automatic. As it is, I’ll now need to run it manually:

$ vagrant provision

This will spew an awful lot of information onto your terminal as the setup.sh script is run within the 

Vagrant box. Let’s see if it worked:

$ vagrant ssh$ php -v

PHP 7.0.7 (cli) (built: May 28 2016 08:26:36) ( NTS )Copyright (c) 1997-2016 The PHP GroupZend Engine v3.0.0, Copyright (c) 1998-2016 Zend Technologies

Setting Up the Web ServerOf course, even with MySQL and Apache installed, the system is not ready to be run. First of all, we should configure Apache. The easiest way to do this is to create a configuration file that can be copied into Apache’s conf.d directory. Let’s call the file poppch20.conf, and drop it into the infrastructure directory:

NameVirtualHost *:80

<VirtualHost *:80>    ServerAdmin matt@getinstance.com    DocumentRoot /var/www/poppch20    ServerName poppch20.vagrant.internal    ErrorLog logs/poppch20-error_log    CustomLog logs/poppch20-access_log common </VirtualHost>

<Directory /var/www/poppch20>AllowOverride all</Directory>

I’ll return to that hostname a little later. Leaving aside that tantalizing detail, this is enough to tell 

Apache about our /var/www/poppch20 directory and to set up logging. Of course, I’ll also have to update setup.sh to copy the configuration file at provision time:

sudo cp $VAGRANTDIR/poppch20.conf /etc/httpd/conf.d/sudo service httpd restartsudo /sbin/chkconfig httpd on

492

Chapter 20 ■ Vagrant

I copy the configuration file into place and restart the web server so that the configuration is picked up. I 

also run chkconfig to ensure that the server will be started at boot time.

After making this change, I can re-run this script:

$ vagrant provision

It’s important to note that those parts of the set up script we previously covered will also be re-run. When you 

create a provisioning script, you must design it so it can be executed repeatedly without serious repercussions. Luckily, Yum detects that my specified packages have already been installed and grumbles harmlessly, in part because I take the precaution of passing it -q flag, which keeps the complaints relatively muted.

Setting Up MySQLFor many applications you’ll need to make sure that a database is available and ready for connections. Here’s a simple addition to my setup script:

sudo service mysqld start/usr/bin/mysqladmin -s -u root password 'vagrant' || echo "** unable to create pass - probably already done"echo "CREATE DATABASE IF NOT EXISTS poppch20_vagrant" | mysql -u root -pvagrant# install data here if needed#echo "GRANT ALL PRIVILEGES  ON poppch20_vagrant.* TO'vagrant'@'localhost' IDENTIFIED BY 'vagrant'WITH GRANT OPTION" | mysql -u root -pvagrantecho "FLUSH PRIVILEGES" | mysql -u root -pvagrantsudo /sbin/chkconfig mysqld on

I start MySQL. Then I run the mysqladmin command to create a root password. This will fail after the first run because the password will already be set, so I use the -s flag to suppress error messages and print a message of my own if the command fails. Then I create a database, a user, and a password. Finally, I run chkconfig to ensure that the MySQL daemon will start at boot time.

With that in place, I can provision again, and then test my database:

$ vagrant provision

# much output

$ vagrant ssh$ mysql -uvagrant -pvagrant poppch20_vagrant

Welcome to the MySQL monitor.  Commands end with ; or \g.Your MySQL connection id is 9Server version: 5.1.73 Source distribution

Copyright (c) 2000, 2013, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or itsaffiliates. Other names may be trademarks of their respectiveowners.

493

Chapter 20 ■ Vagrant

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.mysql>

We now have a running database and a web server. It’s time to see the code in action.

Configuring a Host NameWe have logged in to our new production-like development environment several times, so networking is more or less taken care of. Even though I’ve configured a web server, I’ve yet to use it. That’s because we still need to support a hostname for our VM. So let’s add one to Vagrantfile:

config.vm.hostname = "poppch20.vagrant.internal"config.vm.network :private_network, ip: "192.168.33.148"

I invent a hostname and use the config.vm.hostname directive to add it. I also configure private 

networking with config.vm.network, assigning a static IP address. You should use private address space for this—an unused IP address beginning with 192.168 should work.

Because this is an invented hostname, we must configure our operating system to handle the resolution. 

On a Unix-like system that means editing a system file, /etc/hosts. In this case, I would add the following:

192.168.33.148  poppch20.vagrant.internal

Not overly onerous, but we are working towards a one-command install for our team, so it would be good to have a way of automating this step. Fortunately, Vagrant supports plug-ins, and the hostmanager plug-in does exactly what we need.

You can see what plug-ins are installed with this command:

$ vagrant plugin list

vagrant-login (1.0.1, system)vagrant-share (1.1.5, system)

To add a plug-in, you simply run the vagrant plugin install command:

$ vagrant plugin install vagrant-hostmanager

Installing the 'vagrant-hostmanager' plugin. This can take a few minutes...Installed the plugin 'vagrant-hostmanager (1.8.2)'!

Then you can explicitly tell the plug-in to update /etc/hosts, like this:

$ vagrant hostmanager

[default] Updating /etc/hosts file...

In order to make this process automatic for our team members, we should explicitly enable hostmanger 

in Vagrantfile:

 config.hostmanager.enabled = true

494

With the configuration changes in place, we should run vagrant reload in order to apply them.  

Then it’s the moment of truth! Will our system run in the browser? As you can see in Figure 20-2, the system should work just fine.

Chapter 20 ■ Vagrant

Figure 20-2.  Accessing a configured system on a Vagrant box

Wrapping It Up

So we have gone from nothing to a fully working development environment. Given that it took a chapter’s worth of effort to get here, it might seem like a bit of a cheat to say that Vagrant is quick and easy. There are two answers to that. First, once you have done this a few times, it becomes a pretty simple matter to spin up yet another Vagrant setup—certainly much easier than trying to juggle multiple dependency stacks by hand.

More importantly, though, the real speed and efficiency gain does not lie with the person who sets 

Vagrant up. Imagine a new developer coming in to your project expecting days' worth of downloads, configuration file edits, and wiki-clicking. Imagine telling her,「Install Vagrant and VirtualBox. Check out the code. From the infrastructure directory, run 'vagrant up'.」And that’s it! Compare that with some of the painful onboarding processes you have experienced or heard described.

Of course, we’ve only scratched the surface in this chapter. As you need to configure Vagrant to do more 

for you, the official site at https://www.vagrantup.com will provide you with all the support you need.

Table 20-1 provides a quick reminder of the Vagrant commands we encountered in this chapter.

495

Chapter 20 ■ Vagrant

Table 20-1.  Some Vagrant Commands

Command

vagrant up

vagrant reload

vagrant plugin list

vagrant plugin install <plugin-name>

vagrant provision

vagrant halt

vagrant init

vagrant destroy

Summary

Description

Boot the virtual machine and provision if not yet provisionedHalt the system and bring it back upList the installed plug-insInstall a plug-inRun the provision step again (useful if you have updated provision scripts)Gracefully shut down the virtual machineCreate a new Vagrantfile document

Destroy the virtual machine. Don’t worry, you can always start again with vagrant up!

In this chapter, I introduced Vagrant, the application that lets you work in a production-like development environment without sacrificing your authoring tools. I covered installation, the choosing of a distribution, and initial setup—including mounting your development directories. Once we had a virtual machine to play with, I moved on to the provisioning process—covering package installation, as well as database and web server configuration. Finally, I looked at hostname management, and I showed our system working in the browser!

496

CHAPTER 21

