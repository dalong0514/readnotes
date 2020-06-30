# PHP Standards

Unless you are a lawyer or a health inspector, the topic of standards probably does not make your heart race. However, what standards help us achieve is worth getting excited about. Standards promote interoperability, and that gives us access to a vast array of compatible tools and framework components.

This chapter will cover several important aspects of standards:

PHP Standards Recommendations: Their origins and purpose

•	 Why standards: What are standards and why they matter•	•	•	•	

PSR-1: The Basic Coding Standard

PSR-2: The Coding Style Guide

PSR-4: Autoloading

Why Standards?

Design patterns interoperate. That is built in at their core. A problem described in a design pattern suggests a particular solution, which in turn generates architectural consequences. These are then well addressed by new patterns. Patterns also help developers to interoperate because they provide a shared vocabulary. Object-oriented systems tend to privilege the principle of playing nice.

As we increasingly share each other’s components though, this informal tendency towards 

interoperability is not always enough. As we have seen, Composer (or our package management system of choice) allows us to mix and match tools in our projects. These components may be designed as standalone libraries, or they may be pieces from a wider framework. Either way, once deployed in our system, they must be capable of working beside and in collaboration with any number of other components. By adhering to core standards, we make it less likely that our work will run into compatibility issues.

In some senses, the nature of a standard is less important than the fact that it is adhered to. Personally, for 

example, I don’t love every aspect of the PSR-2 style guidelines. In most circumstances, including this book, I have adopted the standard. Other developers on my teams will hopefully find my code easier to work with because they will find it in a format that is familiar. For other standards, such as autoloading, failure to observe a common standard will result in components that may not work together at all without additional middleware.Standards are probably not the most exciting aspect of programming. However there is an interesting contradiction at their core. It may seem that a standard closes down creativity. After all, standards tell you want you can and can’t do. You must comply. You might think that this is hardly the stuff of innovation. And yet we owe the great flowering of creativity that the internet has ushered into our lives to the fact that every node on this network of networks conforms to open standards. Proprietary systems stuck within walled gardens are necessarily limited in scope and often in longevity—no matter how clever their code or slick their interfaces. The internet, with its shared protocols, ensures that any site can link to any other site. Most 

385

Chapter 15 ■ php StandardS

browsers support standard HTML, CSS, and JavaScript. The interfaces we can build within these standards are not always the most impressive we might imagine (though the limitations are much less than they were); still, abiding by them enables us to maximize the reach of our work.

Used well, standards promote openness, cooperation, and, ultimately, creativity. This is true, even if a 

standard itself enforces some limitations.

What Are PHP Standards Recommendations?

At the 2009 PHP Tek conference, a group of framework developers formed an organization they called the PHP Framework Interop Group (PHP-Fig). Since then, developers have come on board from other key components. Their purpose was to build standards, so that their systems could better co-exist.

The group vote on standards proposals which progress from Draft, through Review, and finally, to 

Accepted status.

Table 15-1 lists the current standards at the time of this writing.

Table 15-1.  Accepted PHP Standards Recommendations

PSR Number

Name

Description

1

2

34

6

7

Basic Coding Standard

Coding Style Guide

Logger InterfaceAutoloading Standard

Caching Interface

Fundamentals such as PHP tags and basic naming conventionsCode formatting, including rules for placement of braces, argument lists, etc.Rules for log levels and logger behaviorsConventions for naming classes and namespaces, as well as their mapping to the filesystemRules for cache management, including data types, cache item lifetime, error handling, etc.

HTTP Message Interfaces

Conventions for HTTP requests and responses

But that’s not all. There are also draft proposals in the works, including one for inline documentation 

(PSR-5), another style guide (PSR-12), and a standard for hypermedia links (PSR-13).

Why PSR in Particular?So, why choose one standard and not another? It happens that the PHP Framework Interop Group—the originators of PSRs—has a pretty great pedigree, and the standards themselves therefore make sense. But also, these are the standards that the major frameworks and components are adopting. If you are using Composer to add functionality to your projects, you are already consuming code that complies with PSRs. By using its conventions for autoloading and its style guides, you are likely building code that is ready for collaboration with other people and components.

386

Chapter 15 ■ php StandardS

 ■ Note  One set of standards is not inherently superior to another. When you choose whether to adopt a standard, your choice may be driven by your judgment of the recommendation’s merits. alternatively, you might make a pragmatic choice based on the context within which you are working. If you’re working in the Wordpress community, for example, you might want to adopt the style defined in the Core Contributor handbook at https://make.wordpress.org/core/handbook/best-practices/coding-standards/php/. Such a choice is part of the point of standards, which are all about the cooperation of people and software.

PSRs are a good bet because they are supported by key framework and component projects, including 

Phing, Composer, PEAR, Symfony, and Zend 2. Like patterns, standards are infectious—you’re probably already benefiting from them.

Who Are PSRs for?Ostensibly PSRs are designed for the creators of frameworks. The fact that the membership of the PHP-Fig group rapidly widened to include the creators of tools as well as frameworks, however, shows that standards have wide relevance. That said, unless you are creating a logger, you may not need to worry too much about the details of PSR-3 (beyond ensuring any logging tool you use is itself compliant). On the other hand, if you’ve read the rest of this book, chances are you are as likely to be creating tools as you are to be consuming them. So, it’s also likely that you’ll find something relevant to you either in the present standards or the standards to come.

And then there are the standards that matter to all of us. Unglamorous as style guides are, for example, 

they are relevant to every programmer. And while the rules that govern autoloading really apply to those who create autoloaders (and the main game in town is probably Composer’s), they also fundamentally affect how we organize our classes, our packages, and our files.

For these reasons, I will focus on coding style and autoloading for the rest of this chapter.

Coding with Style

I tend to find pull request comments like「your braces are in the wrong place」disproportionately irritating. Such input often seems nitpicky and perilously close to bike-shedding.

 In case you have not come across it, the verb「to bike-shed」refers to the tendency in some 

 ■ Note reviewers to criticize unimportant elements of a project under scrutiny. the implication is that such elements are chosen because they fit within the scope of the commenter’s competence. So, given a skyscraper to assess, a particular manager might focus, not on the vast and complex tower of glass and steel, but on the much easier to comprehend bike shed around the back. Wikipedia has a good history of the term: https://en.wikipedia.org/wiki/Law_of_triviality

387

Chapter 15 ■ php StandardS

And yet I have come to see that conforming to a common style can help improve the quality of code. 

This is mainly a matter of readability (regardless of the reasoning behind a particular rule). If a team abides by the same rules for indentations, brace placement, argument lists, and so on, then a developer can quickly assess and contribute to a colleague’s code.

So, for this edition of the book, I committed to edit all code examples so that they conform to PSR-1 

and PSR-2. I have asked my colleague and technical editor Paul Tregoing to hold me to that, too. This was a promise that was so easy to make at the planning stage—and much more effort than I expected. This brings me to the first style guide lesson I learned. If possible, adopt a standard early for your project. Refactoring to a code style will likely tie up resources and make it hard to examine code differences that span The Time of the Great Reformat.

So what changes have I had to apply? Let’s start with the basics.

PSR-1 Basic Coding StandardThese are the fundamentals for PHP code. You can find them in detail at http://www.php-fig.org/psr/psr-1/. Let’s break them down.

Opening and Closing TagsFirst of all, a PHP section should open either with <?php or <?=. In other words, the short opening tag, <?, should not be used, nor should any other variation. A section should close with ?> only (or, as we shall see in the next section, no tag at all).

Side EffectsA PHP file should declare classes, interfaces, functions, and the like, or it should perform an action (such as reading or writing to a file or sending output to the browser); however, it should not do both. If you are accustomed to using require_once() to include other class files, this will trip you up straight away because the act of including another file is a side effect. Just as patterns beget patterns, so standards tend to require other standards. The correct way to handle class dependencies is through a PSR-4 compliant autoloader.

So, is it legal for a class you declare to write to a file in one of its methods? That is perfectly acceptable because the effect is not kicked off by the file’s inclusion. In other words, it’s an execution effect not a side effect.

So what kind of file might perform actions rather than declare classes? Think of the script that kicks off 

an application.

Here is a listing that performs actions as a direct result of inclusion:

// listing 15.01// index.phpnamespace popp\ch15\batch01;

require_once(__DIR__ . "/../../../vendor/autoload.php");

$tree = new Tree();print "loaded " . get_class($tree) . "\n";

Here is a PHP file that declares a class with no side effects:

// listing 15.02

388

Chapter 15 ■ php StandardS

// Tree.phpnamespace popp\ch15\batch01;

class Tree{}

 In other chapters, I largely omit namespace declarations and use directives in order to focus on the 

 ■ Note code. Since this chapter is about the mechanics of formatting class files, I will include namespace and use statements where appropriate.

NamingClasses must be declared in upper camel case, also known as studly caps. In other words, a class name should begin with a capital letter. The rest of the name should be lowercase unless it consists of multiple words. In this instance, each word should begin with an uppercase letter, like this:

class MyClassName

Properties can be named in any way, although consistency is called for. I tend to use camel case, an 

approach similar to studly caps, but without the leading capital letter:

private $myPropertyName

Methods must be declared in camel case:

public function myMethodName()

Class constants must be upper case, with words separated by underscores:

const MY_NAME_IS = 'matt';

More Rules and an ExampleClasses, namespaces, and files should be declared in accordance with the PSR-4 autoloading standard. We will come to that later in the chapter, however. PHP documents should be saved as UTF-8 encoded files.

Finally, for PSR-1, let’s get it all wrong—and then put it right. Here is a class file that breaks all the rules:

<?// listing 15.03

class conf_reader {    const ModeFile = 1;    const Mode_DB = 2;    private $conf_file;    private $confValues= [];

    function read_conf() {

389

Chapter 15 ■ php StandardS

        // implementation    }}?>

Can you spot all the issues? First of all, I used a short opening tag. I also failed to declare a namespace (though we haven’t yet covered this requirement in detail). In naming my class, I used underscores and no capitals, rather than studly caps. And I used two formats for my constant names, neither of which are the required one—all capitals with words should be separated by underscores. Although both my property names were legal, I failed to make them consistent; specifically, I used underscores for $conf_file and camel case for $confValues. In naming my method, read_conf(), I used an underscore rather than camel case.

Let’s fix the problems:

<?php// listing 15.04

namespace popp\ch15\batch01;

class ConfReader {    const MODE_FILE = 1;    const MODE_DB = 2;    private $confFile;    private $confValues = [];

    function readConf() {        // implementation    }}

PSR-2 Coding Style GuideThe Coding Style Guide (PSR-2) builds upon PSR-1. Let’s jump in and look at some of the rules.

Starting and Ending a PHP DocumentWe have already seen that PSR-1 requires that PHP blocks open with <?php. PSR-2 stipulates that pure PHP files should not have an ending ?> tag, but should end with a single blank line. It’s all too easy to end a file with a closing tag, and then let an extra newline creep in. This can result in formatting bugs, as well as errors when you set HTTP headers (you cannot do this after content has already been sent to the browser).

namespace declarations should be followed by a blank line, and a block of use declarations should be 

followed by a blank line. Do not put more than one use declaration on the same line:

// listing 15.05

namespace popp\ch15\batch01;

use popp\ch10\batch06\DiamondDecorator;use popp\ch10\batch06\DiamondPlains;

// begin class

390

Chapter 15 ■ php StandardS

Starting and Ending a ClassThe class keyword, the class name, and extends and implements must all be placed on the same line. Where a class implements multiple interfaces, each interface name can be included on the same line as the class declaration, or it can be placed indented on its own line. If you choose to place your interface names on multiple lines, the first item must be placed on its own line rather than directly after the implements keyword. Class braces should begin on the line after the class declaration and end on their own line (directly after the class contents). So, a class declaration might look something like this:

// listing 15.06class EarthGame extends Game implements    Playable,    Savable{    // class body}

However, you could equally place the interface names on a single line:

class EarthGame extends Game implements Playable, Savable{    // class body}

Declaring PropertiesProperties must have a declared visibility (public, private, or protected). The var keyword is not acceptable. We have already covered the format for property names as part of PSR-1. You can use underscores, camel case, or studly case—but you should be consistent.

Starting and Ending a MethodAll methods must have a declared visibility (public, private, or protected). The visibility keyword must follow abstract or final, but precede static. Method arguments with default values should be placed at the end of the argument list.

Single Line DeclarationsMethod braces should begin on the line after the method name and end on their own line (directly after the method code). A list of method arguments should not begin or end with a space (i.e., they should snuggle in close to the wrapping parentheses). For each argument, the comma should be flush with the preceding argument name (or the default value), but it should then be followed by a space. Let’s clarify things with an example:

// listing 15.07

final public static function generateTile(int $diamondCount, bool $polluted = false){    // implementation}

391

Chapter 15 ■ php StandardS

Multi-line DeclarationsA single line method declaration is not practical in cases where there are many arguments. In this situation, you can break the argument list so that each argument (including type, argument variable, default value, and comma) is placed indented on its own line. In this case, the closing parenthesis should be placed on the line after the argument list, flush with the start of the method declaration. The opening brace should follow the closing parenthesis on the same line, separated by a space. The method body should begin on a new line. Once again, that sounds much more complicated that it is. An example should make it clearer:

// listing 15.08

    public function __construct(        int $size,        string $name,        bool $wraparound = false,        bool $aliens = false    ) {        // implementation    }

Lines and IndentationYou should use four spaces rather than tabs for indentation. It’s worth checking your editor settings—you can configure good editors to use spaces rather than a tab when you press the Tab key. You should also wrap your text before your line reaches 120 characters.

Calling Methods and FunctionsDo not place a space between the method name and the opening parenthesis. You can apply the same rules to the argument list in a method call as you do to the argument list in a method declaration. In other words, for a single line call leave no space after the opening parenthesis or before the closing parenthesis. A comma should follow directly after each argument, with a single space falling before the next one. If you need to use multiple lines for a method call, each argument should sit indented on its own line, and the closing parenthesis should fall on a new line:

// listing 15.09

        $earthgame = new EarthGame(            5,            "earth",            true,            true        );        $earthgame::generateTile(5, true);

392

Chapter 15 ■ php StandardS

Flow of ControlFlow control keywords (if, for, while, etc.) must be followed by a single space. However, the opening parenthesis must not be followed by a space. Similarly, the closing parenthesis must not be preceded by a space. So, the contents should be snug in their brackets. In contrast to class and (single line) function declarations, the opening brace for the flow control block should begin on the same line as the closing parenthesis. The closing brace should sit on its own line. Here’s a quick example:

// listing 15.10

        $tile = [];        for ($x = 0; $x < $diamondcount; $x++) {            if ($polluted) {                $tile[] = new PollutionDecorator(new DiamondDecorator(new Plains()));            } else {                $tile[] = new DiamondDecorator(new Plains());            }        }

Notice the space after both for and if. The for and if statements are flush to their parentheses. In both 

cases, the closing parenthesis is followed by a space and then the opening brace for the flow control body.

Checking and Fixing your CodeEven if this chapter covered every single directive in PSR-2, it would be hard to keep it all in your mind. After all, we have other things to think about—like the design and implementation of our systems. So, given that we have bought into the value of coding standards, how do we comply without using too much of our time or focus? We use a tool, of course.

PHP_CodeSniffer allows you to detect and even repair standards violations—and not just for PSR. You 

can get it by following the instructions at https://github.com/squizlabs/PHP_CodeSniffer. There are Composer and PEAR options, but here’s how you can download the PHP archive files:

curl -OL https://squizlabs.github.io/PHP_CodeSniffer/phpcs.phar

curl -OL https://squizlabs.github.io/PHP_CodeSniffer/phpcbf.phar

Why two downloads? The first is for phpcs, which diagnoses and reports on violations. The second is for phpcbf, which can fix a lot of them. Let’s put the tools through their paces. First, here is a scrappily formatted piece of code:

// listing 15.11namespace popp\ch15\batch01;

class ebookParser {    function __construct(string $path , $format=0 ) {        if ($format>1)            $this->setFormat( 1 );    }    function setformat(int $format) {        // do something with $format    }}

393

Chapter 15 ■ php StandardS

Rather than run through the problems here, let’s have PHP_CodeSniffer do it for us:

$ php phpcs.phar --standard=PSR2 src/ch15/batch01/phpcsBroken.php

----------------------------------------------------------------------FOUND 14 ERRORS AFFECTING 6 LINES----------------------------------------------------------------------  3 | ERROR | [x] There must be one blank line after the namespace    |       |     declaration  4 | ERROR | [ ] Class name "ebookParser" is not in camel caps    |       |     format  4 | ERROR | [x] Opening brace of a class must be on the line after    |       |     the definition  6 | ERROR | [ ] Visibility must be declared on method "__construct"  6 | ERROR | [x] Expected 0 spaces between argument "$path" and    |       |     comma; 1 found  6 | ERROR | [x] Incorrect spacing between argument "$format" and    |       |     equals sign; expected 1 but found 0  6 | ERROR | [x] Incorrect spacing between default value and equals    |       |     sign for argument "$format"; expected 1 but found 0  6 | ERROR | [x] Expected 0 spaces between argument "$format" and    |       |     closing bracket; 1 found  6 | ERROR | [x] Opening brace should be on a new line  7 | ERROR | [x] Inline control structures are not allowed  8 | ERROR | [x] Space after opening parenthesis of function call    |       |     prohibited  8 | ERROR | [x] Expected 0 spaces before closing bracket; 1 found 11 | ERROR | [ ] Visibility must be declared on method "setformat" 11 | ERROR | [x] Opening brace should be on a new line----------------------------------------------------------------------PHPCBF CAN FIX THE 11 MARKED SNIFF VIOLATIONS AUTOMATICALLY----------------------------------------------------------------------

That’s an exhausting number of problems for just a few lines of code. Luckily, as the output indicates, 

we can fix a lot of these with very little effort:

$ php phpcbf.phar --standard=PSR2 src/ch15/batch01/EbookParser.php

Processing EbookParser.php [PHP => 83 tokens in 15 lines]... DONE in 11ms (11 fixable violations)        => Fixing file: 0/11 violations remaining [made 4 passes]... DONE in 17msPatched 1 file

Now, if we run phpcs again, we’ll see that the situation is much improved:

$ php phpcs.phar --standard=PSR2 src/ch15/batch01/EbookParser.php

----------------------------------------------------------------------FOUND 3 ERRORS AFFECTING 3 LINES----------------------------------------------------------------------

394

Chapter 15 ■ php StandardS

  5 | ERROR | Class name "ebookParser" is not in camel caps format  8 | ERROR | Visibility must be declared on method "__construct" 15 | ERROR | Visibility must be declared on method "setformat"----------------------------------------------------------------------

I’ll go ahead and add the visibility declarations, and then change the name of the class—a quick job! 

And now I have a stylishly compliant code file:

// listing 15.12

namespace popp\ch15\batch01;

class EbookParser{    public function __construct(string $path, $format = 0)    {        if ($format > 1) {            $this->setFormat(1);        }    }

    private function setformat(int $format)    {        // do something with $format    }}

PSR-4 Autoloading

We looked at PHP’s support for autoloading in Chapter 5. In that chapter, we saw how we could use the spl_autoload_register() function to automatically require files based on the name of an as yet unloaded class. Although this is powerful, it is also a kind of behind the scenes magic. This is fine in a single project, but a recipe for great confusion if multiple components come together and all use different conventions for loading class files.

The Autoloading Standard (PSR-4) requires frameworks to conform to a common set of rules, thereby 

adding some discipline to the magic.

This is great news for developers. It means that we can more or less ignore the mechanics of requiring 

files, and focus instead on class dependencies.

The Rules that Matter to UsThe main purpose of PSR-4 is to define rules for autoloader developers. However, those rules inevitably determine the way we must declare namespaces and classes. Here are some of the basics.

A fully-qualified classname (that is, the name of a class, including its namespaces) must include an 

initial「vendor」namespace. So, a class must have at least one namespace.

395

Chapter 15 ■ php StandardS

Let’s say that our vendor namespace is popp. We can declare a class in this way:

// listing 15.13

namespace popp;

class Services{}

The fully-qualified class name for this class is popp\Services.The initial namespaces in a path must correspond to one or more base directories. We can use this to map a set of sub-namespaces to a starting directory. If, for example, we want to work with the namespace popp\library (and nothing else under the popp namespace), then we might map that to a top-level directory to spare us from having to maintain an empty popp/ directory.

Let’s set up a composer.json file to perform that mapping:

{    "autoload": {        "psr-4": {            "popp\\library\\": "mylib"        }    }  }

Notice that I don’t even need to call the base directory, "library". This is an arbitrary mapping of 

popp\library to the mylib directory. Now I can create a class file under the mylib directory:

// listing 15.14// mylib/LibraryCatalogue.php

namespace popp\library;

use popp\library\inventory\Book;

class LibraryCatalogue{    private $books = [];    public function addBook(Book $book)    {        $this->books[] = $book;    }}

In order to be found, the LibraryCatalogue class must be placed in a file with exactly the same name 

(with the obvious addition of the .php extension).

After a base directory (mylib) has been associated with initial namespaces (popp\library), there 

must then be a direct relation between subsequent directories and sub-namespaces. It happens that I have already referenced a class named popp\library\inventory\Book in my LibraryCatalogue class. That class file should therefore be placed in the mylib/inventory directory:

396

Chapter 15 ■ php StandardS

// listing 15.15// mylib/library/inventory/Book.php

namespace popp\library\inventory;

class Book{    // implementation}

Remember the rule that the initial namespaces in a path must correspond to one or more base 

directories? So far we have made a one-to-one relationship between popp\library and mylib. There’s actually no reason why we can’t map the popp\library namespace to more than one base directory. Let’s add a directory named additional to the mapping; here’s the amendment to composer.json:

{    "autoload": {        "psr-4": {            "popp\\library\\": ["mylib", "additional"]        }    }}

Now I can create the additional/inventory directories and a class to go in them:

// listing 15.16// additional/inventory/Ebook.phpnamespace popp\library\inventory;

class Ebook extends Book{    // implementation}

Next, let’s create a top-level runner script, index.php, to instantiate these classes:

// listing 15.17// index.php

require_once("vendor/autoload.php");

use popp\library\LibraryCatalogue;

// will be found under mylib/use popp\library\inventory\Book;

// will be found under additional/use popp\library\inventory\Ebook;

$catalogue = new LibraryCatalogue();$catalogue->addBook(new Book());$catalogue->addBook(new Ebook());

397

Chapter 15 ■ php StandardS

 ■ Note  You must use Composer to generate the autoload file, vendor/autoload.php, and this file must be included in some way before you gain access to the logic you have declared in composer.json. You can do this by running the command composer install. You can learn more about Composer in Chapter 15.

Remember the rule about side effects? A PHP file should declare classes, interfaces, functions, and the 

like; or, it should perform an action. However, it should not do both. This script falls into the taking action category. Crucially, it calls require_once() to include the autoload code generated using the configuration in the composer.json file. Thanks to this, all the classes are located, despite the fact that Ebook has been placed in an entirely separate base directory from the rest.

Why would I want to maintain two separate directories for the same core namespace? One possible 

reason is for unit tests that you want to keep separate from production code. You may also manage plug-ins and extensions that will not ship with every version of your system.

 Be sure to keep an eye on all the pSr standards at http://www.php-fig.org/psr/. this is a fast 

 ■ Note moving area, and you’ll likely find that standards relevant to you are on their way.

Summary

In this chapter, I wrestled a little with the possibility that standards are less than fantastically exciting—and then made a case for their power. Standards get integration issues out of our way, so that we can get on and do amazing things. I looked at PSR-1 and PSR-2, the standards for basic coding and for wider coding style. Next, I went on to discuss PSR-4, the standard for autoloaders. Finally, I worked through a Composer-based example that showed PSR-4 compliant autoloading in practice.

398

CHAPTER 16

