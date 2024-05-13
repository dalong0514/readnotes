# 0205. Object Tools

As we have seen, PHP supports object-oriented programming through language constructs such as classes and methods. The language also provides wider support through functions and classes designed to help you work with objects. In this chapter, we will look at some tools and techniques that you can use to organize, test, and manipulate objects and classes.

This chapter will cover the following tools and techniques: 1) Namespaces: Organize your code into discrete package-like compartments. 2) Include paths: Setting central accessible locations for your library code. 3) Class and object functions: Functions for testing objects, classes, properties, and methods. 4) The Reflection API: A powerful suite of built-in classes that provide unprecedented access to class information at runtime.

## 5.1 PHP and Packages

A package is a set of related classes, usually grouped together in some way. Packages can be used to separate parts of a system from one another. Some programming languages formally recognize packages and provide them with distinct namespaces. PHP has no native concept of a package, but as of PHP 5.3, it introduced namespaces. I’ll look at this feature in the next section. I’ll also take a look at the old way of organizing classes into package-like structures.

### 5.1.1 PHP Packages and Namespaces

Although PHP does not intrinsically support the concept of a package, developers have traditionally used both naming schemes and the filesystem to organize their code into package-like structures. 

Until PHP 5.3, developers were forced to name their files in a global context. In other words, if you named a class ShoppingBasket, it would become instantly available across your system. This caused two major problems. First, and most damaging, was the possibility of naming collisions. You might think that this is unlikely. After all, all you have to do is remember to give all your classes unique names, right? The trouble is, we all rely increasingly on library code. This is a good thing, of course, because it promotes code reuse. But assume your project does this:

```php
// listing 05.01

require_once __DIR__ . "/../useful/Outputter.php";
class Outputter {    
    // output data
}
```

Now assume you incorporate the included file at useful/Outputter.php:

```php
// listing 05.02

class Outputter{    //}
```

Well, you can guess what will happen, right? This happens:

```
PHP Fatal error:  Cannot declare class Outputter because the name is already in use in  /var/popp/src/ch05/batch01/useful/Outputter.php on line 4
```

Back before the introduction of namespaces, there was a conventional workaround to this problem. The answer was to prepend package names to class names, so that class names were guaranteed to be unique:

```php
// listing 05.03
// my/Outputer.php

require_once __DIR__ . "/../useful/Outputter.php";
class my_Outputter{    // output data}

// listing 05.04
// useful/Outputter.php

class useful_Outputter{    //}
```

The problem here was that, as projects got more involved, class names grew longer and longer. It was not an enormous problem, but it resulted in issues with code readability, and made it harder to hold classnames in your head while you worked. Many cumulative coding hours were lost to typos. If you’re maintaining legacy code, you may well still see code that follows this convention. For that reason, I’ll return briefly to the old way of handling packages later in this chapter.

#### 5.1.1.1 Namespaces to the Rescue

PHP 5.3 introduced namespaces. In essence, a namespace is a bucket in which you can place your classes, functions, and variables. Within a namespace you can access these items without qualification. From outside, you must either import the namespace, or reference it, in order to access the items it contains.

Confused? An example should help. Here I rewrite the previous example using namespaces:

// listing 05.05namespace my;

require_once __DIR__ . "/../useful/Outputter.php";

class Outputter{    // output data}

// listing 05.06namespace useful;

class Outputter{    //}

Notice the namespace keyword. As you might expect, this keyword establishes a namespace. If you are using this feature, then the namespace declaration must be the first statement in its file. I have created two namespaces: my and useful. Typically, though, you’ll want to have deeper namespaces. You’ll start with an organization or project identifier. Then you’ll want to further qualify this by package. PHP lets you declare nested namespaces. To do this, you simply use a backslash character to divide each level:

// listing 05.07namespace popp\ch05\batch04\util;

class Debug{    public static function helloWorld()    {        print "hello from Debug\n";    }}

You will typically use a name related to a product or organisation to define a repository. I might use 

one of my domains: getinstance.com, for example. Because a domain name is unique to its owner, this is a trick that Java developers typically use for their package names. They invert domain names so that they run from the most generic to the most specific. Alternatively, I might use the namespace I have chosen for code examples in this book: popp, for the book name. Once I’ve identified my repository, I might go on to define packages. In this case, I use the chapter and then a numbered batch. This allows me to organise groups of examples into discrete buckets. So at this point in the chapter, I am at popp\ch05\batch04. Finally, I can further organise code by category. I’ve gone with util.

So how would I call the method? In fact, it depends where you’re doing the calling from. If you are 

calling the method from within the namespace, you can go ahead and call the method directly:

Debug::helloWorld();

This is known as an unqualified name. Because I’m already in the popp\ch05\batch04\util 

namespace, I don’t have to prepend any kind of path to the class name. If I were accessing the class from outside of a namespaced context, I could do this:

\popp\ch05\batch04\Debug::helloworld();

What output would I get from the following code:

namespace main;

popp\ch05\batch04\Debug::helloworld();

That’s a trick question. In fact, this is my output:

PHP Fatal error:  Class 'popp\ch05\batch04\Debug' not found in...

That’s because I’m using a relative namespace here. PHP is looking below the namespace main for 

popp\ch05\batch04\util and not finding it. Just as you can make absolute URLs and filepaths by starting off with a separator, so you can with namespaces. This version of the example fixes the previous error:

namespace main;

\popp\ch05\batch04\Debug::helloworld();

That leading backslash tells PHP to begin its search at the root, and not from the current namespace.But aren’t namespaces supposed to help you cut down on typing? The Debug class declaration is 

shorter, certainly, but those calls are just as wordy as they would have been with the old naming convention. You can get around this with the use keyword. This allows you to alias other namespaces within the current namespace. Here’s an example:

namespace main;use popp\ch05\batch04\util;util\Debug::helloWorld();

The popp\ch05\batch04\util namespace is imported and implicitly aliased to util. Notice that I 

didn’t begin with a leading backslash character. The argument to use is searched from global space and not from the current namespace. If I don’t want to reference a namespace at all, I can import the Debug class itself:

namespace main;use popp\ch05\batch04\util\Debug;Debug::helloWorld();

This is the convention that is most often used. But what would happen if I already had a Debug class in the calling namespace? Here is such a class:

// listing 05.08namespace popp\ch05\batch04;

class Debug{    public static function helloWorld()    {        print "hello from popp\\ch05\\batch04\\Debug\n";    }}

And here is some calling code from the popp\ch05\batch04 namespace which references both Debug 

classes:

namespace popp\ch05\batch04;

use popp\ch05\batch04\util\Debug;use popp\ch05\batch04\Debug;

Debug::helloWorld();

As you might expect, this causes a fatal error:

PHP Fatal error:  Cannot use popp\ch05\batch04\Debug as Debug because the name is already in use in...

So I seem to have come full circle, arriving back at class name collisions. Luckily, there’s an answer for 

this problem. I can make my alias explicit:

namespace main;

use popp\ch05\batch04\Debug as coreDebug;coreDebug::helloWorld();

By using the as clause to use, I am able to change the Debug alias to coreDebug.If you are writing code in a namespace, and you want to access a class that resides in global  

(non-namespaced) space, you can simply precede the name with a backslash. Here’s a class declared in global space:

// listing 05.09class Lister{    public static function helloWorld()    {        print "hello from global\n";    }}

And here’s some namespaced code:

// listing 05.10namespace popp\ch05\batch04\util;

class Lister{    public static function helloWorld()    {        print "hello from " . __NAMESPACE__ . "\n";    }}

// listing 05.11namespace popp\ch05\batch04;

Lister::helloWorld();  // access local\Lister::helloWorld(); // access global

The namespaced code declares its own Lister class. The client code, in the same namespace, uses an 

unqualified name to access the local version. A name qualified with a single backslash accesses a class in global space.

Here’s the output from the previous fragment:

hello from popp\ch05\batch04\utilhello from global

It’s worth showing because it demonstrates the operation of the __NAMESPACE__ constant. This will 

output the current namespace, and it’s useful in debugging.

You can declare more than one namespace in the same file using the syntax you have already seen. You 

can also use an alternative syntax that uses braces with the namespace keyword:

// listing 05.12namespace com\getinstance\util {

    class Debug    {        public static function helloWorld()        {            print "hello from Debug\n";        }    }}

namespace other {

    \com\getinstance\util\Debug::helloWorld();}

If you must combine multiple namespaces in the same file, then this is the recommended practice. 

Usually, however, it’s considered best practice to define namespaces on a per-file basis.

 ■ Note  You can’t use both the brace and line namespace syntaxes in the same file. You must choose one and stick to it throughout.

Using the File System to Simulate PackagesWhichever version of PHP you use, you should organize classes using the file system, which affords a kind of package structure. For example, you might create util and business directories and include class files with the require_once() statement, like this:

require_once('business/Customer.php');require_once('util/WebTools.php');

You could also use include_once() with the same effect. The only difference between the include() and require() statements lies in their handling of errors. A file invoked using require() will bring down your entire process when you meet an error. The same error encountered via a call to include() will merely generate a warning and end execution of the included file, leaving the calling code to continue. This makes require() and require_once() the safe choice for including library files, and include() and include_once() useful for operations like templating.

 ■ Note  require() and require_once() are actually statements, not functions. this means that you can omit the brackets when using them. personally, I prefer to use brackets anyway, but if you follow suit, be prepared to be bored by pedants eager to explain your mistake.

Figure 5-1 shows the util and business packages from the point of view of the Nautilus file manager.

Figure 5-1.  PHP packages organized using the file system

 ■ Note  require_once() accepts a path to a file and includes it evaluated in the current script. the function will only incorporate its target if it has not already been incorporated elsewhere. this one-shot approach is particularly useful when accessing library code because it prevents the accidental redefinition of classes and functions. this can happen when the same file is included by different parts of your script in a single process using a function like require() or include().

It is customary to use require() and require_once() in preference to the similar include() and  include_once() functions. this is because a fatal error encountered in a file accessed with the require() functions takes down the entire script. the same error encountered in a file accessed using the include() functions will cause the execution of the included file to cease, but will only generate a warning in the calling script. the former, more drastic behavior, is safer.

there is an overhead associated with the use of require_once() when compared with require(). If you need to squeeze every last millisecond out of your system, you may like to consider using require() instead. as is so often the case, this is a tradeoff between efficiency and convenience.

As far as PHP is concerned, there is nothing special about this structure. You are simply placing library 

scripts in different directories. It does lend itself to clean organization, and can be used in parallel with either namespaces or a naming convention.

Naming the PEAR WayBack before namespaces were introduced, developers were forced to resort to conventions in order to avoid class name collisions. The most common of these, as we have seen, was the fake namespacing maintained by PEAR developers.

 ■ Note  pear stands for the php extension and application repository. It is an officially maintained archive of packages and tools that add to php’s functionality. Core pear packages are included in the php distribution, and others can be added using a simple command-line tool. You can browse the pear packages at  http://pear.php.net.

PEAR uses the file system to define its packages as I have described. Before namespaces were 

introduced, every class was named according to its package path, with each directory name separated by an underscore character.

For example, PEAR includes a package called XML, which has an RPC subpackage. The RPC package 

contains a file called Server.php. The class defined inside Server.php is not called Server, as you might expect. Without namespaces, that would sooner or later clash with another Server class elsewhere in the PEAR project or in a user’s code. Instead, the class is named XML_RPC_Server. This approach made for unattractive class names. It did, however, make code easy to read because a class name always described its own context.

Include PathsWhen you organize your components, there are two perspectives that you should bear in mind. I have covered the first, where files and directories are placed on the filesystem. But you should also consider the way that components access one another. I have glossed over the issue of include paths so far in this section. When you include a file, you could refer to it using a relative path from the current working directory or an absolute path on the file system.

 ■ Note  although it is important to understand the way that include paths work and the issues involved in requiring files, it is also important to bear in mind that many modern systems no longer rely upon require statements at the class level. Instead, they use a combination of autoload and namespaces. I will cover autoload below, and then look in more detail at practical autoload recommendations and tools in Chapters 15 and 16.

The examples you have seen so far have occasionally specified a fixed relationship the requiring and 

required files:

require_once(__DIR__ . '/../useful/Outputter.php');

This works quite nicely, except that it hardcodes the relationship between files. There must always be a 

useful directory alongside the calling class’s containing directory.

Perhaps the worst approach is the tortuous relative path:

require_once('../../projectlib/business/User.php');

This is problematic because the path specified here is not relative to the file that contains this require_once 

statement, but to a configured calling context (often, but not always, the current working directory). Paths like this are a recipe for confusion (and in my experience almost always a sign that a system will need considerable improvement in other areas, too).You could use an absolute path, of course:

require_once('/home/john/projectlib/business/User.php');

This will work for a single instance—but it’s brittle. By specifying paths in this much detail, you freeze 

the library file into a particular context. Whenever you install the project on a new server, all require statements will need changing to account for a new file path. This can make libraries hard to relocate and impractical to share among projects without making copies. In either case, you lose the package idea in all the additional directories. Is it the business package, or is it the projectlib/business package?

If you must manually include files in your code, the neatest approach is to decouple the invoking code 

from the library:

business/User.php

The preceding snippet can be referenced from anywhere on a system. You can do this with the include 

path. This is a list of directories that PHP searches when attempting to require a file. You can add to this list by altering the include_path directive. include_path is usually set in PHP’s central configuration file, php.ini. It defines a list of directories separated by colons on Unix-like systems and semicolons on Windows systems:

include_path = ".:/usr/local/lib/php-libraries"

If you’re using Apache, you can also set include_path in the server application’s configuration file 

(usually called httpd.conf) or a per-directory Apache configuration file (usually called .htaccess) with this syntax:

php_value  include_path  value    .:/usr/local/lib/php-libraries

 ■ Note  .htaccess files are particularly useful in web space provided by some hosting companies, which provide very limited access to the server environment.

When you use a filesystem function such as fopen() or require() with a nonabsolute path that 

does not exist relative to the current working directory, the directories in the include path are searched automatically, beginning with the first in the list (in the case of fopen(), you must include a flag in its argument list to enable this feature). When the target file is encountered, the search ends, and the file function completes its task.

So by placing a package directory in an include directory, you need only refer to packages and files in 

your require() statements.

require_once("business/User.php");

You may need to add a directory to the include_path so that you can maintain your own library 

directory. To do this, you can edit the php.ini file (remember that, for the PHP server module, you will need to restart your server for the changes to take effect).

If you do not have the privileges necessary to work with the php.ini file, you can set the include path from within your scripts using the set_include_path() function. set_include_path() accepts an include path (as it would appear in php.ini) and changes the include_path setting for the current process only. The php.ini file probably already defines a useful value for include_path, so rather than overwrite it, you can access it using the get_include_path() function and append your own directory. Here’s how you can add a directory to the current include path:

set_include_path(get_include_path() . PATH_SEPARATOR . "/home/john/phplib/");

The PATH_SEPARATOR constant will resolve to a colon on a Unix system and a semicolon on a Windows 

platform. So, for reasons of portability, its use is considered best practice.

AutoloadAlthough it’s neat to use require_once in conjunction with the include path, many developers are doing away with require statements altogether at a high level and relying instead on autoload.

To do this, you should organize your classes so that each sits in its own file. Each class file should bear 

a fixed relationship to the name of the class it contains, so you might define a ShopProduct class in a file named ShopProduct.php with directories corresponding to elements of the class’s namespace.

PHP 5 introduced autoload functionality to help automate the inclusion of class files. The default 

support is pretty basic but still useful. It can be invoked by calling a function named spl_autoload_register() with no arguments. If autoload functionality has been activated in this way, a special function named spl_autoload() will be invoked whenever an attempt is made to instantiate an unknown class. The spl_autoload() function will be passed the name of the class, and it will attempt to use this name (converted to lower case), together with a file extension (php or inc by default) to include the relevant class file.

Here’s a simple example:

spl_autoload_register();$writer = new Writer();

Assuming I have not already included a file containing a Writer object, this instantiation looks bound to fail. However, because I have set up autoloading, PHP will attempt to include a file named writer.php or writer.inc, and will then try the instantiation a second time. If one of these files exists, and contains a class named Writer, then all will be well.

This default behavior supports namespaces, substituting directory names for each package:

spl_autoload_register();$writer = new util\Writer();

The preceding code will find a file named writer.php (note the lowercase name) in a directory  

named util.

What if I happen to name my class files case-dependently? That is, what if I name them with the capital letters preserved? If I had placed the Writer class in a file named Writer.php, then the default implementation would have failed to find it.

Luckily, I can register my own custom function to handle different sets of conventions. In order to take advantage of this, I must pass a reference to a custom function to spl_autoload_register(). My autoload function should require a single argument. Then, if the PHP engine encounters an attempt to instantiate an unknown class, it will invoke this function, passing it the unknown class name as a string. It is up to the autoload function to define a strategy for locating and then including the missing class file. Once the autoload function has been invoked, PHP will attempt to instantiate the class once again.

Here’s a simple autoload function, together with a class to load:

// listing 05.13class Blah{    public function wave()    {        print "saying hi from root";    }}

// listing 05.14$basic = function ($classname) {    $file = __DIR__ . "/" . "{$classname}.php";    if (file_exists($file)) {        require_once($file);    }};

\spl_autoload_register($basic);

$blah = new Blah();$blah->wave();

Having failed to instantiate Blah initially, the PHP engine will see that I have registered an autoload 

function with spl_register_function() and pass it the string, "Blah". My implementation simply attempts to include the file Blah.php. This will only work, of course, if the file is in the same directory as the file in which the autoload function was declared. In a real-world example, I would have to combine include path configuration with my autoload logic (this is precisely what Composer’s autoload implementation does).

If I want to provide old school support, I might automate PEAR package includes:

// listing 05.15

class util_Blah{    public function wave()    {        print "saying hi from underscore file";    }}

// listing 05.16

$underscores = function ($classname) {    $path = str_replace('_', DIRECTORY_SEPARATOR, $classname);    $path = __DIR__ . "/$path";    if (file_exists("{$path}.php")) {        require_once("{$path}.php");    }};

\spl_autoload_register($underscores);

$blah = new util_Blah();$blah->wave();

As you can see, the autoload function matches underscores in the supplied $classname and replaces 

each with the DIRECTORY_SEPARATOR character (/ on Unix systems). I attempt to include the class file  (util/Blah.php). If the class file exists, and the class it contains has been named correctly, the object should be instantiated without an error. Of course, this does require the programmer to observe a naming convention that forbids the underscore character in a class name, except where it divides up packages.

What about namespaces? We’ve seen that the default autoload functionality supports namespaces. But 

if we override that default, it’s up to us to provide namespace support. This is just a matter matching and replacing backslash characters:

// listing 05.17namespace util;

class LocalPath{    public function wave()    {        print "hello from ".get_class();    }}

// listing 05.18$namespaces = function ($path) {    if (preg_match('/\\\\/', $path)) {        $path = str_replace('\\', DIRECTORY_SEPARATOR, $path);    }    if (file_exists("{$path}.php")) {        require_once("{$path}.php");    }};

\spl_autoload_register($namespaces);$obj = new util\LocalPath();$obj->wave();

The value that is passed to the autoload function is always normalized to a fully qualified name, without 

a leading backslash, so there is no need to worry about aliasing or relative namespaces at the point of instantiation.

What if I wanted to support both PEAR-style class names and namespaces? I could combine my autoload implementations into a single custom function. Or, I could use the fact that spl_autoload_register() stacks its autoload functions:

// listing 05.19\spl_autoload_register($namespaces);\spl_autoload_register($underscores);

$blah = new util_Blah();$blah->wave();

$obj = new util\LocalPath();$obj->wave();

When it encounters an unknown class, the PHP engine will invoke the autoload functions in turn, 

stopping when instantiation is possible, or when the all options have been exhausted.

There is obviously an overhead to this kind of stacking, so why does PHP support it? In a real world project, you’d likely combine the namespace and underscore strategies into a single function. However, components in large systems and in third-party libraries may need to register their own autoload mechanisms. Stacking allows multiple parts of a system to register autoload strategies independently, without overwriting one another. In fact, a library that only needs an autoload mechanism briefly can pass the name of its custom autoload function (or a reference to it, if the function is anonymous) to  spl_autoload_unregister() to clean up after itself!

 ■ Note  php supports __autoload(), a less powerful mechanism for managing automatic file includes. If you provide an implementation of the __autoload() function, php will call your function when it fails to locate a class. however, because this approach only supports http://www.php.net/spl_autoload_register, a single autoload function without stacking, it may be deprecated in future versions of php.

The Class and Object Functions

PHP provides a powerful set of functions for testing classes and objects. Why is this useful? After all, you probably wrote most of the classes you are using in your script.

In fact, you don’t always know at runtime about the classes that you are using. You may have designed a system to work transparently with third-party bolt-on classes, for example. In this case, you will typically instantiate an object given only a class name. PHP allows you to use strings to refer to classes dynamically, like this:

// listing 05.20namespace tasks;

class Task{    public function doSpeak()    {        print "hello\n";    }}

// listing 05.21$classname = "Task";require_once("tasks/{$classname}.php");$classname = "tasks\\$classname";$myObj = new $classname();$myObj->doSpeak();

This script might acquire the string I assign to $classname from a configuration file or by comparing a 

web request with the contents of a directory. You can then use the string to load a class file and instantiate an object. Notice that I’ve constructed a namespace qualification in this fragment.

Typically, you would do something like this when you want your system to be able to run user-created 

plug-ins. Before you do anything as risky as that in a real project, you would have to check that the class exists, that it has the methods you are expecting, and so on.

 ■ Note  even with safeguards in place, you should be extremely wary of dynamically installing third-party plug-in code. You should never automatically run code uploaded by users. any plug-in so installed would typically execute with the same privileges as your core code, so a malicious plug-in author could wreak havoc on your system.

this isn’t to say that plug-ins aren’t a fine idea. allowing third-party developers to enhance a core system can offer great flexibility. to ensure greater security, you might support a directory for plug-ins, but require that the code files be installed by a system’s administrator, either directly or from within a password-protected management environment. the administrator would either personally check the plug-in code before installation or would source plug-ins from a reputable repository. this is the way that the popular blogging platform, Wordpress, handles plug-ins.

Some class functions have been superseded by the more powerful Reflection API, which I will examine later in the chapter. Their simplicity and ease of use make them a first port of call in some instances, however.

Looking for ClassesThe class_exists() function accepts a string representing the class to check for and returns a Boolean true value if the class exists and false otherwise.

Using this function, I can make the previous fragment a little safer:

// listing 05.22$base = __DIR__;$classname = "Task";$path = "{$base}/tasks/{$classname}.php";if (! file_exists($path)) {    throw new \Exception("No such file as {$path}");}require_once($path);$qclassname = "tasks\\$classname";if (! class_exists($qclassname)) {    throw new Exception("No such class as $qclassname");}$myObj = new $qclassname();$myObj->doSpeak();

Of course, you can’t be sure that the class in question does not require constructor arguments. For 

that level of safety, you would have to turn to the Reflection API, covered later in the chapter. Nevertheless, class_exists() does allow you to check that the class exists before you work with it.

 ■ Note  remember, as stated previously, you should always be wary of any data provided by outside sources. test it and treat it before using it in any way. In the case of a file path, you should escape or remove dots and directory separators to prevent an unscrupulous user from changing directories and including unexpected files. however, when I describe ways of building systems that are easily extensible, these techniques generally cover a deployment’s owner (with the write privileges that implies), and not her external users.

You can also get an array of all classes defined in your script process using the get_declared_classes() 

function:

print_r(get_declared_classes());

This will list user-defined and built-in classes. Remember that it only returns the classes declared at the time of the function call. You may run require() or require_once() later on, and thereby add to the number of classes in your script.

Learning About an Object or ClassAs you know, you can constrain the object types of method arguments using class type hinting. Even with this tool, you can’t always be certain of an object’s type.

There are a number of basic tools available to check the type of an object. First of all, you can check the 

class of an object with the get_class() function. This accepts any object as an argument and returns its class name as a string:

// listing 05.23$product = self::getProduct();if (get_class($product) === 'popp\ch05\batch05\CdProduct') {    print "\$product is a CdProduct object\n";}

In the fragment, I acquire something from the getProduct() function. To be absolutely certain that it is 

a CdProduct object, I use the get_class() method.

 ■ Note 

I covered the CdProduct and BookProduct classes in Chapter 3.

Here’s the getProduct() function:

// listing 05.24    public static function getProduct()    {        return new CdProduct(            "Exile on Coldharbour Lane",            "The",            "Alabama 3",            10.99,            60.33        );    }

getProduct() simply instantiates and returns a CdProduct object. I will make good use of this function 

in this section.

The get_class() function is a very specific tool. You often want a more general confirmation of a class’s type. You may want to know that an object belongs to the ShopProduct family, but you don’t care whether its actual class is BookProduct or CdProduct. To this end, PHP provides the instanceof operator.

 ■ Note  php 4 did not support instanceof. Instead, it provided the is_a() function, which was deprecated in php 5.0 but restored to the fold with php 5.3.

The instanceof operator works with two operands, the object to test on the left of the keyword and the 

class or interface name on the right. It resolves to true if the object is an instance of the given type:

// listing 05.25$product = self::getProduct();if ($product instanceof \popp\ch05\batch05\CdProduct) {    print "\$product is an instance of CdProduct\n";}

Getting a Fully Qualified String Reference to a ClassNamespaces have cleaned up much that was ugly about object-oriented PHP. We no longer have to tolerate ridiculously long class names or risk naming collisions (legacy code aside). On the other hand, with aliasing and with relative namespace references, it can be a chore to resolve some class paths so that they are fully qualified.

Here are some examples of hard-to-resolve class names:

namespace mypackage;

use util as u;use util\db\Querier as q;class Local {}

// Resolve these:

// Aliased namespace//  u\Writer;

// Aliased class//  q;

// Class referenced in local context//  Local

It’s not too hard to work out how these class references resolve, but it would be a pain to write code to capture every possibility. Given u\Writer, for example, an automated resolver would need to know that u is aliased to util and is not a namespace in its own right. Helpfully, PHP 5.5 introduced the ClassName::class syntax. In other words, given a class reference, you can append a scope resolution operator and the class keyword to get the fully qualified class name:

print u\Writer::class . "\n";print q::class . "\n";print Local::class . "\n";

The preceding snippet outputs this:

util\Writerutil\db\Queriermypackage\Local

Learning About MethodsYou can acquire a list of all the methods in a class using the get_class_methods() function. This requires a class name and returns an array containing the names of all the methods in the class:

print_r(get_class_methods('\\popp\\ch04\\batch02\\BookProduct'));

Assuming the BookProduct class exists, you might see something like this:

Array(    [0] => __construct    [1] => getNumberOfPages    [2] => getSummaryLine    [3] => getPrice    [4] => setID    [5] => getProducerFirstName    [6] => getProducerMainName    [7] => setDiscount    [8] => getDiscount    [9] => getTitle    [10] => getProducer    [11] => getInstance)

In the example, I pass a class name to get_class_methods() and dump the returned array with the print_r() function. I could alternatively have passed an object to get_class_methods() with the same result. Only the names of public methods will be included in the returned list.

As you have seen, you can store a method name in a string variable and invoke it dynamically together 

with an object, like this:

// listing 05.26$product = self::getProduct(); // acquire an object$method = "getTitle";          // define a method nameprint $product->$method();     // invoke the method

Of course, this can be dangerous. What happens if the method does not exist? As you might expect, your 

script will fail with an error. You have already encountered one way of testing that a method exists:

if (in_array($method, get_class_methods($product))) {  print $product->$method(); // invoke the method}

I check that the method name exists in the array returned by get_class_methods() before invoking it. 

PHP provides more specialized tools for this purpose. You can check method names to some extent with two functions: is_callable() and method_exists(). is_callable() is the more sophisticated of the two functions. It accepts a string variable representing a function name as its first argument and returns true if the function exists and can be called. To apply the same test to a method, you should pass it an array in place of the function name. The array must contain an object or class name as its first element and the method name to check as its second element. The function will return true if the method exists in the class:

// listing 05.27if (in_array($method, get_class_methods($product))) {    print $product->$method(); // invoke the method}

is_callable() optionally accepts a second argument, a Boolean. If you set this to true, the function 

will only check the syntax of the given method or function name, not for its actual existence.

The method_exists() function requires an object (or a class name) and a method name, and returns 

true if the given method exists in the object’s class:

// listing 05.28if (method_exists($product, $method)) {    print $product->$method(); // invoke the method}

 ■ Caution  remember that the fact that a method exists does not mean that it will be callable.  method_exists() returns true for private and protected methods, as well as for public ones.

Learning About PropertiesJust as you can query the methods of a class, so can you query its fields. The get_class_vars() function requires a class name and returns an associative array. The returned array contains field names as its keys and field values as its values. Let’s apply this test to the CdProduct object. For the purposes of illustration, we add a public property to the class, CdProduct::$coverUrl:

print_r(get_class_vars('\\popp\\ch05\\batch05\\CdProduct'));

Only the public property is shown:

Array(    [coverUrl] => cover url)

Learning About InheritanceThe class functions also allow us to chart inheritance relationships. We can find the parent of a class, for example, with get_parent_class(). This function requires either an object or a class name, and it returns the name of the superclass, if any. If no such class exists—that is, if the class we are testing does not have a parent—then the function returns false.

print get_parent_class('\\popp\\ch04\\batch02\\BookProduct');

As you might expect, this yields the parent class: ShopProduct.We can also test whether a class is a descendent of another using the is_subclass_of() function. This requires a child object (or the name of a class) and the name of the parent class. The function returns true if the second argument is a superclass of the first argument:

// listing 05.29$product = self::getBookProduct(); // acquire an object

if (is_subclass_of($product, '\\popp\\ch04\\batch02\\ShopProduct')) {    print "BookProduct is a subclass of ShopProduct\n";}

is_subclass_of() will tell you only about class inheritance relationships. It will not tell you that a class 

implements an interface. For that, you should use the instanceof operator. Or, you can use a function that is part of the SPL (Standard PHP Library). class_implements() accepts a class name or an object reference, and returns an array of interface names:

// listing 05.30if (in_array('someInterface', class_implements($product))) {    print "BookProduct is an interface of someInterface\n";}

Method InvocationYou have already encountered an example in which I used a string to invoke a method dynamically:

$product = getProduct();   // acquire an object$method = "getTitle";      // define a method nameprint $product->$method(); // invoke the method

PHP also provides the call_user_func() method to achieve the same end. call_user_func() can invoke either methods or functions. To invoke a function, it requires a single string as its first argument:

$returnVal = call_user_func("myFunction");

To invoke a method, it requires an array. The first element of this should be an object, and the second 

should be the name of the method to invoke:

$returnVal = call_user_func([$myObj, "methodName"]);

You can pass any arguments that the target method or function requires in additional arguments to 

call_user_func(), like this:

// listing 05.31$product = self::getBookProduct(); // Acquire a BookProduct objectcall_user_func([$product, 'setDiscount'], 20);

This dynamic call is, of course, equivalent to this:

$product->setDiscount(20);

The call_user_func() method won’t change your life greatly because you can equally use a string 

directly in place of the method name, like this:

$method = "setDiscount";$product->$method(20);

Much more impressive, though, is the related call_user_func_array() function. This operates in the 

same way as call_user_func(), as far as selecting the target method or function is concerned. Crucially, though, it accepts any arguments required by the target method as an array.

 ■ Note  beware—arguments passed to a function or method using call_user_func() are not passed by reference.

So why is this useful? Occasionally you are given arguments in array form. Unless you know in advance 

the number of arguments you are dealing with, it can be difficult to pass them on. In Chapter 4, I looked at the interceptor methods that can be used to create delegator classes. Here’s a simple example of a __call() method:

// listing 05.32    public function __call($method, $args)    {        if (method_exists($this->thirdpartyShop, $method)) {            return $this->thirdpartyShop->$method();        }    }

As you have seen, the __call() method is invoked when an undefined method is called by client code. In this example, I maintain an object in a property called $thirdpartyShop. If I find a method in the stored object that matches the $method argument, I invoke it. I blithely assume that the target method does not require any arguments, which is where my problems begin. When I write the __call() method, I have no way of telling how large the $args array may be from invocation to invocation. If I pass $args directly to the delegate method, I will pass a single array argument, and not the separate arguments it may be expecting. call_user_func_array() solves the problem perfectly:

// listing 05.33    public function __call($method, $args)    {        if (method_exists($this->thirdpartyShop, $method)) {            return call_user_func_array(                [                     $this->thirdpartyShop,                     $method                ],                $args            );        }    }

The Reflection API

PHP’s Reflection API is to PHP what the java.lang.reflect package is to Java. It consists of built-in classes for analyzing properties, methods, and classes. It’s similar in some respects to existing object functions, such as get_class_vars(), but is more flexible and provides much greater detail. It’s also designed to work with PHP’s object-oriented features, such as access control, interfaces, and abstract classes, in a way that the older, more limited class functions are not.

Getting StartedThe Reflection API can be used to examine more than just classes. For example, the ReflectionFunction class provides information about a given function, and ReflectionExtension yields insight about an extension compiled into the language. Table 5-1 lists some of the classes in the API.

Table 5-1.  Some of the Classes in the Reflection API

Class

Reflection

ReflectionClass

ReflectionMethod

ReflectionParameter

ReflectionProperty

ReflectionFunction

ReflectionExtension

ReflectionException

Description

Provides a static export() method for summarizing class informationClass information and toolsClass method information and toolsMethod argument informationClass property informationFunction information and toolsPHP extension informationAn error class

ReflectionZendExtension

PHP Zend extension information

Between them, the classes in the Reflection API provide unprecedented runtime access to information 

about the objects, functions, and extensions in your scripts.

The Reflection API’s power and reach mean you should usually use it in preference to the class and 

object functions. You will soon find it indispensable as a tool for testing classes. You might want to generate class diagrams or documentation, for example, or you might want to save object information to a database, examining an object’s accessor (getter and setter) methods to extract field names. Building a framework that invokes methods in module classes according to a naming scheme is another use of Reflection.

Time to Roll up Your SleevesYou have already encountered some functions for examining the attributes of classes. These are useful but often limited. Here’s a tool that is up to the job. ReflectionClass provides methods that reveal information about every aspect of a given class, whether it’s a user-defined or internal class. The constructor of ReflectionClass accepts a class or interface name (or an object instance) as its sole argument:

// listing 05.34$prodclass = new \ReflectionClass('popp\\ch04\\batch02\\CdProduct');\Reflection::export($prodclass);

Once you’ve created a ReflectionClass object, you can use the Reflection utility class to dump 

information about CdProduct. Reflection has a static export() method that formats and dumps the data 

managed by a Reflection object (that is, any instance of a class that implements the Reflector interface, to be pedantic). Here’s an abridged extract from the output generated by a call to Reflection::export():

Class [ <user> class popp\ch04\batch02\CdProduct extends popp\ch04\batch02\ShopProduct ] {  @@ /var/popp/src/ch04/batch02/CdProduct.php 6-37

  - Constants [2] {    Constant [ integer AVAILABLE ] { 0 }    Constant [ integer OUT_OF_STOCK ] { 1 }  }

  - Static properties [0] {  }

  - Static methods [1] {     Method [ <user, inherits popp\ch04\batch02\ShopProduct> static public method  

getInstance ] {

      @@ /var/popp/src/ch04/batch02/ShopProduct.php 93 - 130

      - Parameters [2] {        Parameter #0 [ <required> integer $id ]        Parameter #1 [ <required> PDO $pdo ]      }      - Return [ popp\ch04\batch02\ShopProduct ]    }  }

  - Properties [3] {    Property [ <default> private $playLength ]    Property [ <default> public $status ]    Property [ <default> protected $price ]  }

  - Methods [11] {     Method [ <user, overwrites popp\ch04\batch02\ShopProduct, ctor> public method __

construct ] {

      @@ /var/popp/src/ch04/batch02/CdProduct.php 10 - 24

      - Parameters [5] {        Parameter #0 [ <required> string $title ]        Parameter #1 [ <required> string $firstName ]        Parameter #2 [ <required> string $mainName ]        Parameter #3 [ <required> float $price ]        Parameter #4 [ <required> integer $playLength ]      }    }...}

As you can see, Reflection::export() provides remarkable access to information about a class. 

Reflection::export() provides summary information about almost every aspect of CdProduct, including the access control status of properties and methods, the arguments required by every method, and the location of every method within the script document. Compare that with a more established debugging function. The var_dump() function is a general-purpose tool for summarizing data. You must instantiate an object before you can extract a summary, and even then, it provides nothing like the detail made available by Reflection::export():

// listing 05.35$cd = new CdProduct("cd1", "bob", "bobbleson", 4, 50);var_dump($cd);

Here’s the output:

object(popp\ch04\batch02\CdProduct)#17 (8) {  ["playLength":"popp\ch04\batch02\CdProduct":private]=>  int(50)  ["status"]=>  NULL  ["title":"popp\ch04\batch02\ShopProduct":private]=>  string(3) "cd1"  ["producerMainName":"popp\ch04\batch02\ShopProduct":private]=>  string(9) "bobbleson"  ["producerFirstName":"popp\ch04\batch02\ShopProduct":private]=>  string(3) "bob"  ["price":protected]=>  float(4)  ["discount":"popp\ch04\batch02\ShopProduct":private]=>  int(0)  ["id":"popp\ch04\batch02\ShopProduct":private]=>  int(0)}

var_dump() and its cousin print_r() are fantastically convenient tools for exposing the data in your 

scripts. For classes and functions, the Reflection API takes things to a whole new level, though.

Examining a ClassThe Reflection::export() method can provide a great deal of useful information for debugging, but we can use the API in more specialized ways. Let’s work directly with the Reflection classes.

You’ve already seen how to instantiate a ReflectionClass object:

$prodclass = new \ReflectionClass('popp\\ch04\\batch02\\CdProduct');

Next, I will use the ReflectionClass object to investigate CdProduct within a script. What kind of class 

is it? Can an instance be created? Here’s a function to answer these questions:

// listing 05.36

    // class ClassInfo    public static function getData(\ReflectionClass $class)    {        $details = "";        $name = $class->getName();        if ($class->isUserDefined()) {            $details .= "$name is user defined\n";        }        if ($class->isInternal()) {            $details .= "$name is built-in\n";        }        if ($class->isInterface()) {            $details .= "$name is interface\n";        }        if ($class->isAbstract()) {            $details .= "$name is an abstract class\n";        }        if ($class->isFinal()) {            $details .= "$name is a final class\n";        }        if ($class->isInstantiable()) {            $details .= "$name can be instantiated\n";        } else {            $details .= "$name can not be instantiated\n";        }

        if ($class->isCloneable()) {            $details .= "$name can be cloned\n";        } else {            $details .= "$name can not be cloned\n";        }        return $details;    }

// listing 05.37$prodclass = new \ReflectionClass('popp\\ch04\\batch02\\CdProduct');print ClassInfo::getData($prodclass);

I create a ReflectionClass object, assigning it to a variable called $prodclass by passing the 

CdProduct class name to ReflectionClass’s constructor. $prodclass is then passed to a method named ClassInfo::classData() that demonstrates some of the methods that can be used to query a class.

The methods should be self-explanatory, but here’s a brief description of some of them:

•	•	

ReflectionClass::getName() returns the name of the class being examined.

The ReflectionClass::isUserDefined() method returns true if the class has been declared in PHP code, and ReflectionClass::isInternal() yields true if the class is built-in.

•	

•	

•	

•	

You can test whether a class is abstract with ReflectionClass::isAbstract() and whether it’s an interface with ReflectionClass::isInterface().

If you want to get an instance of the class, you can test the feasibility of that with ReflectionClass::isInstantiable().

You can check whether a class is cloneable with the ReflectionClass::isCloneable() method.

You can even examine a user-defined class’s source code. The ReflectionClass object provides access to its class’s file name and to the start and finish lines of the class in the file.

Here’s a quick-and-dirty method that uses ReflectionClass to access the source of a class:

// listing 05.38class ReflectionUtil{    public static function getClassSource(\ReflectionClass $class): string    {        $path  = $class->getFileName();        $lines = file($path);        $from  = $class->getStartLine();        $to    = $class->getEndLine();        $len   = $to - $from + 1;        return implode(array_slice($lines, $from - 1, $len));    }}

// listing 05.39print ReflectionUtil::getClassSource(    new \ReflectionClass('popp\\ch04\\batch02\\CdProduct'));

ReflectionUtil is a simple class with a single static method, ReflectionUtil::getClassSource(). 

That method takes a ReflectionClass object as its only argument and returns the referenced class’s source code. ReflectionClass::getFileName() provides the path to the class’s file as an absolute path, so the code should be able to go right ahead and open it. file() obtains an array of all the lines in the file. ReflectionClass::getStartLine() provides the class’s start line; ReflectionClass::getEndLine() finds the final line. From there, it’s simply a matter of using array_slice() to extract the lines of interest.

To keep things brief, this code omits error handling. In a real-world application, you’d want to check 

arguments and result codes.

Examining MethodsJust as ReflectionClass is used to examine a class, a ReflectionMethod object examines a method.

You can acquire a ReflectionMethod in two ways. First, you can get an array of ReflectionMethod 

objects from ReflectionClass::getMethods(). Second, if you need to work with a specific method, ReflectionClass::getMethod() accepts a method name and returns the relevant ReflectionMethod object.

Here, we use ReflectionClass::getMethods() to put the ReflectionMethod class through its paces:

// listing 05.40$prodclass = new \ReflectionClass('popp\\ch04\\batch02\\CdProduct');$methods = $prodclass->getMethods();

foreach ($methods as $method) {    print ClassInfo::methodData($method);    print "\n----\n";}

// listing 05.41

    // class ClassInfo    public static function methodData(\ReflectionMethod $method)    {        $details = "";        $name = $method->getName();        if ($method->isUserDefined()) {            $details .= "$name is user defined\n";        }        if ($method->isInternal()) {            $details .= "$name is built-in\n";        }        if ($method->isAbstract()) {            $details .= "$name is abstract\n";        }        if ($method->isPublic()) {            $details .= "$name is public\n";        }        if ($method->isProtected()) {            $details .= "$name is protected\n";        }        if ($method->isPrivate()) {            $details .= "$name is private\n";        }        if ($method->isStatic()) {            $details .= "$name is static\n";        }        if ($method->isFinal()) {            $details .= "$name is final\n";        }        if ($method->isConstructor()) {            $details .= "$name is the constructor\n";        }        if ($method->returnsReference()) {            $details .= "$name returns a reference (as opposed to a value)\n";        }        return $details;    }

The code uses ReflectionClass::getMethods() to get an array of ReflectionMethod objects and then 

loops through the array, passing each object to methodData().

The names of the methods used in methodData() reflect their intent: the code checks whether the 

method is user-defined, built-in, abstract, public, protected, static, or final. You can also check whether the method is the constructor for its class and whether or not it returns a reference.

There’s one caveat: ReflectionMethod::returnsReference() doesn’t return true if the tested method simply returns an object, even though objects are passed and assigned by reference in PHP 5. Instead, ReflectionMethod::returnsReference() returns true only if the method in question has been explicitly declared to return a reference (by placing an ampersand character in front of the method name).

As you might expect, you can access a method’s source code using a technique similar to the one used 

previously with ReflectionClass:

// listing 05.42

    // class ReflectionUtil    public static function getMethodSource(\ReflectionMethod $method): string    {        $path  = $method->getFileName();        $lines = @file($path);        $from  = $method->getStartLine();        $to    = $method->getEndLine();        $len   = $to - $from + 1;        return implode(array_slice($lines, $from - 1, $len));    }

// listing 05.43$class = new \ReflectionClass('popp\\ch04\\batch02\\CdProduct');$method = $class->getMethod('getSummaryLine');print ReflectionUtil::getMethodSource($method);

Because ReflectionMethod provides us with getFileName(), getStartLine(), and getEndLine() 

methods, it’s a simple matter to extract the method’s source code.

Examining Method ArgumentsNow that method signatures can constrain the types of object arguments, the ability to examine the arguments declared in a method signature becomes immensely useful. The Reflection API provides the ReflectionParameter class just for this purpose. To get a ReflectionParameter object, you need the help of a ReflectionMethod object. The ReflectionMethod::getParameters() method returns an array of ReflectionParameter objects.

ReflectionParameter can tell you the name of an argument and whether the variable is passed by reference (that is, with a preceding ampersand in the method declaration). It can also tell you the class required by argument hinting and whether the method will accept a null value for the argument.

Here are some of ReflectionParameter’s methods in action:

// listing 05.44$class = new \ReflectionClass('popp\\ch04\\batch02\\CdProduct');

$method = $class->getMethod("__construct");$params = $method->getParameters();

foreach ($params as $param) {    print ClassInfo::argData($param) . "\n";}

// listing 05.45

    // class ClassInfo    public function argData(\ReflectionParameter $arg)    {        $details = "";        $declaringclass = $arg->getDeclaringClass();        $name  = $arg->getName();        $class = $arg->getClass();        $position = $arg->getPosition();        $details .= "\$$name has position $position\n";        if (! empty($class)) {            $classname = $class->getName();            $details .= "\$$name must be a $classname object\n";        }

        if ($arg->isPassedByReference()) {            $details .= "\$$name is passed by reference\n";        }

        if ($arg->isDefaultValueAvailable()) {            $def = $arg->getDefaultValue();            $details .= "\$$name has default: $def\n";        }

        if ($arg->allowsNull()) {            $details .= "\$$name can be null\n";        }

        return $details;    }

Using the ReflectionClass::getMethod() method, the code acquires a ReflectionMethod object. It then 

uses ReflectionMethod::getParameters() to get an array of ReflectionParameter objects. The argData() function uses the ReflectionParameter object it was passed to acquire information about the argument.

First, it gets the argument’s variable name with ReflectionParameter::getName(). The ReflectionParameter::getClass() method returns a ReflectionClass object if a hint’s been provided. The code checks whether the argument is a reference with isPassedByReference(); and finally, it looks for the availability of a default value, which it then adds to the return string.

Using the Reflection APIWith the basics of the Reflection API under your belt, you can now put the API to work.

Imagine that you’re creating a class that calls Module objects dynamically. That is, it can accept plug-

ins written by third parties that can be slotted into the application without the need for any hard-coding. To achieve this, you might define an execute() method in the Module interface or abstract base class, forcing all child classes to define an implementation. You could allow the users of your system to list Module classes 

in an external XML configuration file. Your system can use this information to aggregate a number of Module objects before calling execute() on each one.

What happens, however, if each Module requires different information to do its job? In that case, the 

XML file can provide property keys and values for each Module, and the creator of each Module can provide setter methods for each property name. Given that foundation, it’s up to your code to ensure that the correct setter method is called for the correct property name.

Here’s some groundwork for the Module interface and a couple of implementing classes:

// listing 05.46class Person{    public $name;

    public function __construct(string $name)    {        $this->name = $name;    }}

// listing 05.47interface Module{    public function execute();}

// listing 05.48class FtpModule implements Module{    public function setHost($host)    {        print "FtpModule::setHost(): $host\n";    }

    public function setUser($user)    {        print "FtpModule::setUser(): $user\n";    }

    public function execute()    {        // do things    }}

// listing 05.49class PersonModule implements Module{    public function setPerson(Person $person)    {        print "PersonModule::setPerson(): {$person->name}\n";    }

    public function execute()    {        // do things    }}

Here, PersonModule and FtpModule both provide empty implementations of the execute() method. Each class also implements setter methods that do nothing but report that they were invoked. The system lays down the convention that all setter methods must expect a single argument: either a string or an object that can be instantiated with a single string argument. The PersonModule::setPerson() method expects a Person object, so I include a Person class in my example.

To work with PersonModule and FtpModule, the next step is to create a ModuleRunner class. It will use a multidimensional array indexed by module name to represent configuration information provided in the XML file. Here’s that code:

// listing 05.50class ModuleRunner{    private $configData = [        "popp\\ch05\\batch08\\PersonModule" => ['person' => 'bob'],        "popp\\ch05\\batch08\\FtpModule"    => [            'host' => 'example.com',            'user' => 'anon'        ]    ];    private $modules = [];    // ...}

The ModuleRunner::$configData property contains references to the two Module classes. For each module element, the code maintains a subarray containing a set of properties. ModuleRunner’s init() method is responsible for creating the correct Module objects, as shown here:

// listing 05.51

    // class ModuleRunner    public function init()    {        $interface = new \ReflectionClass('popp\\ch05\\batch08\\Module');        foreach ($this->configData as $modulename => $params) {            $module_class = new \ReflectionClass($modulename);            if (! $module_class->isSubclassOf($interface)) {                throw new Exception("unknown module type: $modulename");            }            $module = $module_class->newInstance();            foreach ($module_class->getMethods() as $method) {                $this->handleMethod($module, $method, $params);                // we cover handleMethod() in a future listing!            }            array_push($this->modules, $module);        }    }

// listing 05.52$test = new ModuleRunner();$test->init();

The init() method loops through the ModuleRunner::$configData array, and for each module 

element, it attempts to create a ReflectionClass object. An exception is generated when ReflectionClass’s constructor is invoked with the name of a nonexistent class, so in a real-world context, I would include more error handling here. I use the ReflectionClass::isSubclassOf() method to ensure that the module class belongs to the Module type.

Before you can invoke the execute() method of each Module, an instance has to be created. That’s 

the purpose of ReflectionClass::newInstance(). That method accepts any number of arguments, which it passes on to the relevant class’s constructor method. If all’s well, it returns an instance of the class (for production code, be sure to code defensively: check that the constructor method for each Module object doesn’t require arguments before creating an instance).

ReflectionClass::getMethods() returns an array of all ReflectionMethod objects available for the 

class. For each element in the array, the code invokes the ModuleRunner::handleMethod() method. It then passes it a Module instance, the ReflectionMethod object, and an array of properties to associate with the Module. handleMethod() verifies and invokes the Module object’s setter methods:

// listing 05.53

    // class ModuleRunner    public function handleMethod(Module $module, \ReflectionMethod $method, $params)    {        $name = $method->getName();        $args = $method->getParameters();

        if (count($args) != 1 || substr($name, 0, 3) != "set") {            return false;        }

        $property = strtolower(substr($name, 3));

        if (! isset($params[$property])) {            return false;        }

        $arg_class = $args[0]->getClass();

        if (empty($arg_class)) {            $method->invoke($module, $params[$property]);        } else {            $method->invoke(                $module,                $arg_class->newInstance($params[$property])            );        }    }

handleMethod() first checks that the method is a valid setter. In the code, a valid setter method must be 

named setXXXX() and must declare one—and only one—argument.

Assuming that the argument checks out, the code then extracts a property name from the method 

name by removing set from the beginning of the method name and converting the resulting substring to lowercase characters. That string is used to test the $params array argument. This array contains the user-supplied properties that are to be associated with the Module object. If the $params array doesn’t contain the property, the code gives up and returns false.

If the property name extracted from the module method matches an element in the $params array, I can go ahead and invoke the correct setter method. To do that, the code must check the type of the first (and only) required argument of the setter method. The ReflectionParameter::getClass() method provides this information. If the method returns an empty value, the setter expects a primitive of some kind; otherwise, it expects an object.

To call the setter method, I need a new Reflection API method. ReflectionMethod::invoke() requires 

an object (or null for a static method) and any number of method arguments to pass on to the method it represents. ReflectionMethod::invoke() throws an exception if the provided object does not match its method. I call this method in one of two ways. If the setter method doesn’t require an object argument, I call ReflectionMethod::invoke() with the user-supplied property string. If the method requires an object, I use the property string to instantiate an object of the correct type, which is then passed to the setter.

The example assumes that the required object can be instantiated with a single string argument to its 

constructor. It’s best, of course, to check this before calling ReflectionClass::newInstance().

By the time that the ModuleRunner::init() method has run its course, the object has a store of Module 

objects, all primed with data. The class can now be given a method to loop through the Module objects, calling execute() on each one.

## Summary

In this chapter, I covered some of the techniques and tools that you can use to manage your libraries and classes. I explored PHP’s namespace feature. You saw that we can combine include paths, namespaces, autoload, and the file system to provide flexible organization for classes.

We also examined PHP’s object and class functions, before taking things to the next level with the powerful Reflection API. Finally, we used the Reflection classes to build a simple example that illustrates one of the potential uses that Reflection has to offer.
