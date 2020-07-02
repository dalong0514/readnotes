# 0206. Enterprise Patterns

PHP is, first and foremost, a language designed for the Web. And, because of its extensive support for objects, we can take advantage of patterns hatched in the context of other object-oriented languages, particularly Java.

I develop a single example in this chapter, using it to illustrate the patterns I cover. Remember, though, that by choosing to use one pattern, you are not committed to using all of the patterns that work well with it. Nor should you feel that the implementations presented here are the only way you might go about deploying these patterns. Rather, you should use the examples here to help you understand the thrust of the patterns described, feeling free to extract what you need for your projects.

Because of the amount of material to cover, this is one this book’s longest and most involved chapters, and it may be a challenge to traverse it in one sitting. It is divided into an introduction and two main parts. These dividing lines might make good break points.

I also describe the individual patterns in the「Architecture Overview」section. Although these are interdependent to some extent, you should be able to jump straight to any particular pattern and work through it independently, moving on to related patterns at your leisure.

This chapter will cover several key topics:

Architecture overview: An introduction to the layers that typically comprise an enterprise application

Registry pattern: Managing application data

Presentation layer: Tools for managing and responding to requests and for presenting data to the user

Business logic layer: Getting to the real purpose of your system, which is addressing business problems

Architecture Overview

With a lot of ground to cover, let’s kick off with an overview of the patterns to come, followed by an introduction to building layered, or tiered, applications.

The PatternsI will explore several patterns in this chapter. You may read from start to finish or dip into those patterns that fit your needs or pique your interest:

Registry: This pattern is useful for making data available to all classes in a process. Through careful use of serialization, it can also be used to store information across a session or even across instances of an application.

Front Controller: Use this for larger systems in which you know that you will need as much flexibility as possible in managing many different views and commands.

Application Controller: Create a class to manage view logic and command selection.

Template View: Create pages that manage display and user interface only, incorporating dynamic information into display markup with as little raw code as possible.

Page Controller: Lighter weight but less flexible than Front Controller, Page Controller addresses the same need. Use this pattern to manage requests and handle view logic if you want fast results and your system is unlikely to grow substantially in complexity.

Transaction Script: When you want to get things done fast, with minimal up-front planning, fall back on procedural library code for your application logic. This pattern does not scale well.

•	 Domain Model: At the opposite pole from Transaction Script, use this pattern to 

build object-based models of your business participants and processes.

 the Command pattern is not described individually here (i wrote about it in Chapter 11); however, it 

 ■ Note is encountered once again in both the Front Controller and application Controller patterns.

Applications and LayersMany (most, in fact) of the patterns in this chapter are designed to promote the independent operation of several distinct tiers in an application. Just as classes represent specializations of responsibilities, so do the tiers of an enterprise system, albeit on a coarser scale. Figure 12-1 shows a typical breakdown of the layers in a system.

Figure 12-1.  The layers, or tiers, in a typical enterprise system

The structure shown in Figure 12-1 is not written in stone: some of these tiers may be combined, 

and different strategies can be used for communication between them, depending on the complexity of your system. Nonetheless, Figure 12-1 illustrates a model that emphasizes flexibility and reuse, and many enterprise applications follow it to a large extent.

The view layer contains the interface that a system’s users actually see and interact with. It is responsible for presenting the results of a user’s request and providing the mechanism by which the next request can be made to the system.

The command and control layer processes the request from the user. Based on this analysis, it delegates to the business logic layer any processing required in order to fulfill the request. It then chooses which view is best suited to present the results to the user. In practice, this and the view layer are often combined into a single presentation layer. Even so, the role of display should be strictly separated from those of request handling and business logic invocation.

The business logic layer is responsible for seeing to the business of a request. It performs any required calculations and marshals the resulting data.

The data layer insulates the rest of the system from the mechanics of saving and acquiring persistent information. In some systems, the command and control layer uses the data layer to acquire the business objects with which it needs to work. In other systems, the data layer is hidden as much as possible.

So what is the point of dividing a system in this way? As with so much else in this book, the answer lies with decoupling. By keeping business logic independent of the view layer, you make it possible to add new interfaces to your system with little or no rewriting.

Imagine a system for managing event listings (this will be a very familiar example by the end of the 

chapter). The end user will naturally require a slick HTML interface. Administrators maintaining the system may require a command-line interface for building into automated systems. At the same time, you may be developing versions of the system to work with cell phones and other handheld devices. You may even begin to consider SOAP or a RESTful API.

If you originally combined the underlying logic of your system with the HTML view layer (which is still a common strategy), these requirements would trigger an instant rewrite. If, on the other hand, you had created a tiered system, you would be able to bolt on new presentation strategies without the need to reconsider your business logic and data layers.

By the same token, persistence strategies are subject to change. Once again, you should be able to 

switch between storage models with minimal impact on the other tiers in a system.

Testing is another good reason for creating systems with separate tiers. Web applications are 

notoriously hard to test. In an insufficiently tiered system, automated tests must negotiate the HTML interface at one end and risk triggering random queries to a database at the other, even when their focus is aimed at neither of these areas. Although any testing is better than none, such tests are necessarily haphazard. In a tiered system, on the other hand, the classes that face other tiers are often written so that they extend an abstract superclass or implement an interface. This supertype can then support polymorphism. In a test context, an entire tier can be replaced by a set of dummy objects (often called「stubs」or「mock」objects). In this way, you can test business logic using a fake data layer, for example. You can read more about testing in Chapter 18.

Layers are useful even if you think that testing is for wimps and your system will only ever have a single 

interface. By creating tiers with distinct responsibilities, you build a system whose constituent parts are easier to extend and debug. You limit duplication by keeping code with the same kinds of responsibility in one place (rather than lacing a system with database calls, for example, or with display strategies). Adding to such a system is relatively easy because your changes tend to be nicely vertical, as opposed to messily horizontal.

A new feature, in a tiered system, might require a new interface component, additional request 

handling, some more business logic, and an amendment to your storage mechanism. That’s vertical change. In a nontiered system, you might add your feature and then remember that five separate pages reference your amended database table. Or was it six? There may be dozens of places where your new interface may potentially be invoked, so you need to work through your system, adding code for that. This is horizontal amendment.

In reality, of course, you never entirely escape from horizontal dependencies of this sort, especially when it comes to navigation elements in the interface. A tiered system can help to minimize the need for horizontal amendment, however.

 ■ Note  While many of these patterns have been around for a while (patterns reflect well-tried practices, after all), the names and boundaries are drawn either from Martin Fowler’s key work on enterprise patterns, Patterns of Enterprise Application Architecture (addison-Wesley professional, 2002), or from the influential Core J2EE Patterns: Best Practices and Design Strategies (prentice hall, 2001) by alur et al. For the sake of consistency,  i have tended to use Fowler’s naming conventions where the two sources diverge.

All the examples in this chapter revolve around a fictional listings system with the whimsical-sounding 

name,「Woo,」which stands for something like「What’s On Outside.」

Participants of the system include venues (e.g., theaters, clubs, or cinemas), spaces (e.g., screen 1 or the 

stage upstairs) and events (e.g., The Long Good Friday or The Importance of Being Earnest).

The operations I will cover include creating a venue, adding a space to a venue, and listing all venues in 

the system.

Remember that the aim of this chapter is to illustrate key enterprise design patterns and not to build a working system. Reflecting the interdependent nature of design patterns, most of these examples overlap to a large extent with code examples, making good use of ground covered elsewhere in the chapter. As this code is mainly designed to demonstrate enterprise patterns, much of it does not fulfill all the criteria demanded by a production system. In particular, I omit error checking where it might stand in the way of clarity. You should approach the examples as a means of illustrating the patterns they implement, rather than as building blocks in a framework or application.

Cheating Before We Start

Most of the patterns in this book find a natural place in the layers of an enterprise architecture. But some patterns are so basic that they stand outside of this structure. The Registry pattern is a good example of this. In fact, Registry is a powerful way of breaking out of the constraints laid down by layering. It is the exception that allows for the smooth running of the rule.

RegistryThe Registry pattern is all about providing system-wide access to objects. These days, it is almost an article of faith that globals are bad. Like other sins, though, global data is fatally attractive. This is so much the case that object-oriented architects have felt it necessary to reinvent globals under a new name. You encountered the Singleton pattern in Chapter 9, although it is true that singleton objects do not suffer from all the ills that beset global variables. In particular, you cannot overwrite a singleton by accident. Singletons, then, are  low-fat globals. You should remain suspicious of singleton objects, though, because they invite you to anchor your classes into a system, thereby introducing coupling.

280

Chapter 12 ■ enterprise patterns

Nevertheless, singletons are so useful at times that many programmers (including me) can’t bring 

themselves to give them up.

The ProblemAs you have seen, many enterprise systems are divided into layers, with each layer communicating with its neighbors only through tightly defined conduits. This separation of tiers makes an application flexible. You can replace or otherwise develop each tier with the minimum impact on the rest of the system. What happens, though, when you acquire information in a tier that you later need in another noncontiguous layer?

Let’s say that I acquire configuration data in an ApplicationHelper class:

// listing 12.01class ApplicationHelper{    public function getOptions(): array    {        $optionfile = __DIR__ . "/data/woo_options.xml";

        if (! file_exists($optionfile)) {            throw new AppException("Could not find options file");        }

        $options = simplexml:load_file($optionfile);        $dsn = (string) $options->dsn;        // what do we do with this now?        // ...    }}

Acquiring the information is easy enough, but how would I get it to the data layer, where it is later used? 

And what about all the other configuration information I must disseminate throughout my system?One answer would be to pass this information around the system from object to object: from a 

controller object responsible for handling requests; to objects in the business logic layer; and finally, to an object responsible for talking to the database.

This is entirely feasible. In fact, you could pass the ApplicationHelper object itself around or, 

alternatively, a more specialized Context object. Either way, contextual information is transmitted through the layers of your system to the object or objects that need it.

The tradeoff is that, in order to do this, you must alter the interface of all the objects that relay the 

context object, whether they need to use it or not. Clearly, this undermines loose coupling to some extent.

The Registry pattern provides an alternative that is not without its own consequences.A registry is simply a class that provides access to data (usually, but not exclusively, objects) via static methods (or via instance methods on a singleton). Every object in a system, therefore, has access to these objects.

The term「Registry」is drawn from Fowler’s Patterns of Enterprise Application Architecture; but, as with 

all patterns, implementations pop up everywhere. In The Pragmatic Programmer: from Journeyman to Master (Addison-Wesley Professional, 1999), David Hunt and David Thomas liken a registry class to a police incident-notice board. Detectives on one shift leave evidence and sketches on the board, which are then picked up by new detectives on another shift. I have also seen the Registry pattern called Whiteboard and Blackboard.

281

Chapter 12 ■ enterprise patterns

ImplementationFigure 12-2 shows a Registry object that stores and serves Request objects.

Figure 12-2.  A simple registry

Here is this class in code form:

// listing 12.02class Registry{    private static $instance = null;    private $request;

    private function __construct()    {    }

    public static function instance(): self    {        if (is_null(self::$instance)) {            self::$instance = new self();        }

        return self::$instance;    }

    public function getRequest(): Request    {        if (is_null($this->request)) {            $this->request = new Request();        }

        return $this->request;    }}

// listing 12.03class Request{}

282

Chapter 12 ■ enterprise patterns

You can then access the same Request from any part of your system:

// listing 12.04$reg = Registry::instance();print_r($reg->getRequest());

As you can see, the Registry is simply a singleton (see Chapter 9 if you need a reminder about singleton classes). The code creates and returns a sole instance of the Registry class via the instance() method. This can then be used to retrieve a Request object.

I have been known to throw caution to the wind and use a key-based system, like this:

// listing 12.05class Registry{    private static $instance=null;    private $values = [];

    private function __construct()    {    }

    public static function instance(): self    {        if (is_null(self::$instance)) {            self::$instance = new self();        }

        return self::$instance;    }

    public function get(string $key)    {        if (isset($this->values[$key])) {            return $this->values[$key];        }

        return null;    }

    public function set(string $key, $value)    {        $this->values[$key] = $value;    }}

The benefit here is that you don’t need to create methods for every object you wish to store and serve. 

The downside, though, is that you reintroduce global variables by the back door. The use of arbitrary strings as keys for the objects you store means that there is nothing stopping one part of your system from overwriting a key/value pair when adding an object. I have found it useful to use this map-like structure during development, and then shift over to explicitly named methods when I’m clear about the data I am going to need to store and retrieve.

283

Chapter 12 ■ enterprise patterns

 ■ Note  the registry pattern is not the only way of managing the services a system requires. in Chapter 10, we covered a similar strategy named Dependency injection, which is used in popular frameworks like symfony.

You can also use registry objects as factories for common objects in your system. Instead of storing a provided object, the Registry class creates an instance and then caches the reference. It may do some setup behind the scenes as well, perhaps retrieving data from a configuration file or combining a number of objects:

// listing 12.06

    // class Registry

    private $treeBuilder = null;    private $conf = null;

    // ...

    public function treeBuilder(): TreeBuilder    {        if (is_null($this->treeBuilder)) {            $this->treeBuilder = new TreeBuilder($this->conf()->get('treedir'));        }

        return $this->treeBuilder;    }

    public function conf(): Conf    {        if (is_null($this->conf)) {            $this->conf = new Conf();        }

        return $this->conf;    }

TreeBuilder and Conf are just dummy classes, included to demonstrate a point. A client class that 

needs a TreeBuilder object can simply call Registry::treeBuilder(), without bothering itself with the complexities of initialization. Such complexities may include application-level data such as the dummy Conf object, and most classes in a system should be insulated from them.

Registry objects can be useful for testing, too. The static instance() method can be used to serve up a child of the Registry class, primed with dummy objects. Here’s how I might amend instance() to achieve this:

// listing 12.07

    // class Registry

    private static $testmode = false;

    // ...

284

Chapter 12 ■ enterprise patterns

    public static function testMode(bool $mode = true)    {        self::$instance = null;        self::$testmode = $mode;    }

    public static function instance(): self    {        if (is_null(self::$instance)) {            if (self::$testmode) {                self::$instance = new MockRegistry();            } else {                self::$instance = new self();            }        }

        return self::$instance;    }

When you need to put your system through its paces, you can use test mode to switch in a fake 

registry. This can serve up stubs (objects that fake a real environment for testing purposes) or mocks (similar objects that also analyze calls made to them and assess them for correctness):

// listing 12.08Registry::testMode();$mockreg = Registry::instance();

You can read more about mock and stub objects in Chapter 18.

Registry, Scope, and PHPThe term scope is often used to describe the visibility of an object or value in the context of code structures. The lifetime of a variable can also be measured over time. There are three levels of scope you might consider in this sense. The standard is the period covered by an HTTP request. PHP also provides built-in support for session variables. These are serialized and saved to the file system or the database at the end of a request, and then restored at the start of the next. A session ID stored in a cookie or passed around in query strings is used to keep track of the session owner. Because of this, you can think of some variables as having session scope. You can take advantage of this by storing some objects between requests, saving a trip to the database. Clearly, you need to be careful that you don’t end up with multiple versions of the same object, so you may need to consider a locking strategy when you check an object that also exists in a database into a session.

In other languages, notably Java and Perl (running on the ModPerl Apache module), there is the concept of application scope. Variables that occupy this space are available across all instances of the application. This is fairly alien to PHP; but in larger applications, it might be considered useful to have access to an application-wide space for accessing configuration variables.

In previous editions of this book, I demonstrated examples of session- and application-scoped registry classes; but in the ten years or so since I first wrote that sample code, I have never had cause to use anything but a request-scoped registry. There is an initialization cost to this per-request approach, but you will typically use caching strategies to manage this.

285

Chapter 12 ■ enterprise patterns

ConsequencesRegistry objects make their data globally available. This means that any class that acts as a client for a registry will exhibit a dependency that is not declared in its interface. This can become a serious problem if you begin to rely on Registry objects for lots of the data in your system. Registry objects are best used sparingly, for a well-defined set of data items.

The Presentation Layer

When a request hits your system, you must interpret the requirement it carries, invoke any business logic needed, and finally, return a response. For simple scripts, this whole process often takes place entirely inside the view itself, with only the heavyweight logic and persistence code split off into libraries.

 a view is an individual element in the view layer. it can be a php page (or a collection of composed 

 ■ Note view elements) whose primary responsibility is to display data and provide the mechanism by which new requests can be generated by the user. it could also be a template in a system such as twig.

As systems grow in size, this default strategy becomes less tenable with request processing, business 

logic invocation, and view dispatch logic necessarily duplicated from view to view.

In this section, I look at strategies for managing these three key responsibilities of the presentation layer. Because the boundaries between the view layer and the command and control layer are often fairly blurred, it makes sense to treat them together under the common term,「presentation layer.」

Front ControllerThis pattern is diametrically opposed to the traditional PHP application with its multiple points of entry. The Front Controller pattern presents a central point of access for all incoming requests, ultimately delegating to a view the task of presenting results back to the user. This is a key pattern in the Java enterprise community. It is covered in great detail in Core J2EE Patterns: Best Practices and Design Strategies, which remains one of the most influential enterprise patterns resources. The pattern is not universally loved in the PHP community, partly because of the overhead that initialization sometimes incurs.

Most systems I write tend to gravitate toward the Front Controller. That is, I may not deploy the entire pattern to start with, but I will be aware of the steps necessary to evolve my project into a Front Controller implementation should I need the flexibility it affords.

The ProblemWhere requests are handled at multiple points throughout a system, it is hard to keep duplication from the code. You may need to authenticate a user, translate terms into different languages, or simply access common data. When a request requires common actions from view to view, you may find yourself copying and pasting operations. This can make alteration difficult, as a simple amendment may need to be deployed across several points in your system. For this reason, it becomes easy for some parts of your code to fall out of alignment with others. Of course, a first step might be to centralize common operations into library code, but you are still left with the calls to the library functions or methods distributed throughout your system.Difficulty in managing the progression from view to view is another problem that can arise in a system 

where control is distributed among its views. In a complex system, a submission in one view may lead to any number of result pages, according to the input and the success of any operations performed at the logic layer. Forwarding from view to view can get messy, especially if the same view might be used in different flows.

286

Chapter 12 ■ enterprise patterns

ImplementationAt heart, the Front Controller pattern defines a central point of entry for every request. It processes the request and uses it to select an operation to perform. Operations are often defined in specialized command objects organized according to the Command pattern.

Figure 12-3 shows an overview of a Front Controller implementation.

Figure 12-3.  A Controller class and a command hierarchy

In fact, you are likely to deploy a few helper classes to smooth the process, but let’s begin with the core 

participants. Here is a simple Controller class:

// listing 12.09class Controller{    private $reg;

    private function __construct()    {        $this->reg = Registry::instance();    }

    public static function run()    {        $instance = new Controller();        $instance->init();        $instance->handleRequest();    }

    private function init()    {        $this->reg->getApplicationHelper()->init();    }

    private function handleRequest()    {        $request = $reg->getRequest();

287

Chapter 12 ■ enterprise patterns

        $resolver = new CommandResolver();        $cmd = $resolver->getCommand($request);        $cmd->execute($request);    }}

Simplified as this is, and bereft of error handling, there isn’t much more to the Controller class. A 

controller sits at the tip of a system, delegating to other classes. It is these other classes that do most of the work. run() is merely a convenience method that calls init() and handleRequest(). It is static, and the constructor is private, so the only option for client code is to kick off execution of the system. I usually do this in a file called index.php that contains only a few of lines of code:

// listing 12.10require_once(__DIR__ . "/../../../vendor/autoload.php");

use \popp\ch12\batch05\Controller;

Controller::run();

Notice that nasty looking require statement. It is really only there so that the rest of the system can live in ignorance of the need for requiring files. The autoload.php script is automatically generated by Composer. It manages the logic for loading class files, as needed. If that meant nothing to you, don’t worry; we cover autoloading in much more detail in Chapter 16.

The distinction between the init() and handleRequest() methods is really one of category in PHP. In 

some languages, init() would be run only at application startup, and handleRequest() or an equivalent would be run for each user request. This class observes the same distinction between setup and request handling, even though init() is called for each request.

The init() method makes a call to a class called ApplicationHelper via the Registry class, which is referenced by the Controller’s $reg property. The ApplicationHelper class manages configuration data for the application as a whole. Controller::init() calls a method in ApplicationHelper, also called init(), which, as you will see, initializes data used by the application.

The handleRequest() method uses a CommandResolver to acquire a Command object, which it runs by 

calling Command::execute().

ApplicationHelperThe ApplicationHelper class is not essential to Front Controller. Most implementations must acquire basic configuration data, though, so I should develop a strategy for this. Here is a simple ApplicationHelper:

// listing 12.11class ApplicationHelper{    private $config = __DIR__ . "/data/woo_options.ini";    private $reg;

    public function __construct()    {        $this->reg = Registry::instance();    }

288

Chapter 12 ■ enterprise patterns

    public function init()    {        $this->setupOptions();

        if (isset($_SERVER['REQUEST_METHOD'])) {            $request = new HttpRequest();        } else {            $request = new CliRequest();        }

        $this->reg->setRequest($request);    }

    private function setupOptions()    {        if (! file_exists($this->config)) {            throw new AppException("Could not find options file");        }

        $options = parse_ini_file($this->config, true);

        $conf = new Conf($options['config']);        $this->reg->setConf($conf);

        $commands = new Conf($options['commands']);        $this->reg->setCommands($commands);    }}

This class simply reads a configuration file and adds various objects to a registry, thereby making them 

available to the wider system. The init() method calls a private method—setupOptions()—which reads an .ini file and passes two arrays (each in an instance of an array wrapper named Conf) to the Registry object. There is nothing to Conf but a get() and a set() method—although more sophisticated configuration classes might manage searching for and parsing files, as well as managing the found data. One of these Conf arrays is intended to hold general configuration values—and that is passed to Registry::setConf(). The other array is for mapping URL paths to Command classes, and I pass that to Registry::setCommands().

The init() method also attempts to discover whether the application is being run in a web context or on the command line (by checking for the existence of $_SERVER['REQUEST_METHOD']). It passes a distinct Request subclass to the Registry object, depending on the result of that test.

Since Registry classes do very little but store and serve up objects, they do not make for exciting source 

code listings. For the sake of completeness, though, here are the additional Registry methods used or implied by the ApplicationHelper:

// listing 12.12    // must be initialized by some smarter component    public function setRequest(Request $request)    {        $this->request = $request;    }

    public function getRequest(): Request    {        if (is_null($this->request)) {

289

Chapter 12 ■ enterprise patterns

            throw new \Exception("No Request set");        }

        return $this->request;    }

    public function getApplicationHelper(): ApplicationHelper    {        if (is_null($this->applicationHelper)) {            $this->applicationHelper = new ApplicationHelper();        }

        return $this->applicationHelper;    }

    public function setConf(Conf $conf)    {        $this->conf = $conf;    }

    public function getConf(): Conf    {        if (is_null($this->conf)) {            $this->conf = new Conf();        }

        return $this->conf;    }

    public function setCommands(Conf $commands)    {        $this->commands = $commands;    }

    public function getCommands(): Conf    {        return $this->commands;    }

Here is the simple configuration file:

[config]dsn=sqlite:/var/popp/src/ch12/batch05/data/woo.db

[commands]/=\popp\ch12\batch05\DefaultCommand

CommandResolverA controller needs a way of deciding how to interpret an HTTP request, so that it can invoke the right code to fulfill that request. You could easily include this logic within the Controller class itself, but I prefer to use a specialist class for the purpose. That makes it easy to refactor for polymorphism, if necessary.

290

Chapter 12 ■ enterprise patterns

A Front Controller often invokes application logic by running a Command object (I introduced the 

Command pattern in Chapter 11). The Command is chosen according to the request URL (using either the URL path or, less frequently these days, a GET parameter). Either way, you end up with a token or pattern which can be used for Command selection. There is more than one way of using a URL to select a command. For example, you can test the token against a configuration file or data structure (a logical strategy). Or, you can test it directly against class files on the file system (a physical strategy).

You saw an example of a command factory that used a physical strategy in the last chapter. This time, I 

will take the logical approach, mapping URL fragments to Command classes:

// listing 12.13class CommandResolver{    private static $refcmd = null;    private static $defaultcmd = DefaultCommand::class;

    public function __construct()    {        // could make this configurable        self::$refcmd = new \ReflectionClass(Command::class);    }

    public function getCommand(Request $request): Command    {        $reg = Registry::instance();        $commands = $reg->getCommands();        $path = $request->getPath();

        $class = $commands->get($path);

        if (is_null($class)) {            $request->addFeedback("path '$path' not matched");            return new self::$defaultcmd();        }

        if (! class_exists($class)) {            $request->addFeedback("class '$class' not found");            return new self::$defaultcmd();        }

        $refclass = new \ReflectionClass($class);

        if (! $refclass->isSubClassOf(self::$refcmd)) {            $request->addFeedback("command '$refclass' is not a Command");            return new self::$defaultcmd();        }

        return $refclass->newInstance();    }}

This simple class acquires a Conf object from the registry and uses the URL path (provided by the 

Request::getPath() method) to attempt to get a class name. If the class name is found, and if the class both exists and extends the Command base class, then it is instantiated and returned.

291

Chapter 12 ■ enterprise patterns

If any of these conditions are not met, the getCommand() method degrades gracefully by serving up a 

default Command object.

A more sophisticated implementation (e.g., like the ones used by the routing logic in Silex and Symfony) 

would allow for wildcards in these paths.

You may wonder why this code takes it on trust that the Command class it locates does not require 

parameters:

return $refclass->newInstance();

The answer to this lies in the signature of the Command class itself:

// listing 12.14abstract class Command{    final public function __construct()    {    }

    public function execute(Request $request)    {        $this->doExecute($request);    }

    abstract public function doExecute(Request $request);}

By declaring the constructor method final, I make it impossible for a child class to override it. No 

Command class, therefore, will ever require arguments to its constructor.

When creating command classes, you should be careful to keep them as devoid of application logic 

as you possibly can. As soon as they begin to do application-type stuff, you’ll find that they turn into a kind of tangled transaction script and duplication will soon creep in. Commands are a kind of relay station: they should interpret a request, call into the domain to juggle some objects, and then lodge data for the presentation layer. As soon as they begin to do anything more complicated than this, it’s probably time to refactor. The good news is that refactoring is relatively easy. It’s not hard to spot when a command is trying to do too much, and the solution is usually clear: move that functionality down to a helper or domain class.

RequestRequests are magically handled for us by PHP and neatly packaged up in superglobal arrays. You might have noticed that I still use a class to represent a request. A Request object is passed to CommandResolver, and later on, to Command.

Why do I not let these classes simply query the $_REQUEST, $_POST, or $_GET arrays for themselves?  

I could do that, of course, but by centralizing request operations in one place, I open up new options.

You could, for example, apply filters to the incoming request. Or, as the next example shows, you could gather request parameters from somewhere other than an HTTP request, allowing the application to be run from the command line or from a test script.

The Request object is also a useful repository for data that needs to be communicated to the view layer. 

In fact, many systems offer a separate Response object for that purpose, but we will keep things lean here.

Here is a simple Request superclass:

// listing 12.15abstract class Request

292

Chapter 12 ■ enterprise patterns

{    protected $properties;    protected $feedback = [];    protected $path = "/";

    public function __construct()    {        $this->init();    }

    abstract public function init();

    public function setPath(string $path)    {        $this->path = $path;    }

    public function getPath(): string    {        return $this->path;    }

    public function getProperty(string $key)    {        if (isset($this->properties[$key])) {            return $this->properties[$key];        }

        return null;    }

    public function setProperty(string $key, $val)    {        $this->properties[$key] = $val;    }

    public function addFeedback(string $msg)    {        array_push($this->feedback, $msg);    }

    public function getFeedback(): array    {        return $this->feedback;    }

    public function getFeedbackString($separator = "\n"): string    {        return implode($separator, $this->feedback);    }

293

Chapter 12 ■ enterprise patterns

    public function clearFeedback()    {        $this->feedback = [];    }}

As you can see, most of this class is taken up with mechanisms for setting and acquiring properties. 

The init() method is responsible for populating the private $properties array, and it will be handled by child classes. It’s important to note that this example implementation ignores request methods—not something you would ever want to do in the real world. A full implementation should manage GET, POST, and PUT arrays, as well as provide a unified query mechanism. Once you have a Request object, you should be able to access a parameter via the getProperty() method, which accepts a key string and returns the corresponding value (as stored in the $properties array). You can also add data via setProperty().

The class also manages a $feedback array. This is a simple conduit through which controller classes can 

pass messages to the user. In a fuller implementation, we would likely want to differentiate between error and informational messages.

You may remember that ApplicationHelper instantiates one of HttpRequest and CliRequest. Here is 

the first of these:

// listing 12.16class HttpRequest extends Request{    public function init()    {        // we're conveniently ignoring POST/GET/etc distinctions        // don't do that in the real world!        $this->properties = $_REQUEST;        $this->path = $_SERVER['PATH_INFO'];        $this->path = (empty($this->path)) ? "/" : $this->path;    }}

CliRequest takes argument pairs from the command line in the form key=value and breaks them out 

into properties. It also detects an argument with a path: prefix and assigns the provided value to the object’s $path property:

// listing 12.17class CliRequest extends Request{    public function init()    {        $args = $_SERVER['argv'];

        foreach ($args as $arg) {            if (preg_match("/^path:(\S+)/", $arg, $matches)) {                $this->path = $matches[1];            } else {                if (strpos($arg, '=')) {                    list($key, $val) = explode("=", $arg);                    $this->setProperty($key, $val);                }

294

Chapter 12 ■ enterprise patterns

            }        }

        $this->path = (empty($this->path)) ? "/" : $this->path;    }}

A CommandYou have already seen the Command base class, and Chapter 11 covered the Command pattern in detail, so there’s no need to go too deep into Commands. Let’s round things off, though, with a simple, concrete Command object:

// listing 12.18class DefaultCommand extends Command{    public function doExecute(Request $request)    {        $request->addFeedback("Welcome to WOO");        include(__DIR__ . "/main.php");    }}

This is the Command object that is served up by CommandResolver if no explicit request for a particular 

Command is received.

As you may have noticed, the abstract base class implements execute() itself, calling down to 

the doExecute() implementation of its child class. This allows us to add setup and cleanup code to all commands, simply by altering the base class.

The execute() method is passed a Request object that gives access to user input, as well as to the 

setFeedback() method. DefaultCommand makes use of this to set a welcome message.

Finally, the command dispatches control to a view, simply by calling include(). Embedding the map from command to view in the Command classes is the simplest dispatch mechanism; but for small systems, it can be perfectly adequate. A more flexible strategy can be seen in the「Application Controller」section.

The file, main.php, contains some HTML and a call into the Request object to check for any feedback (I’ll cover views in more detail, shortly). I now have all the components in place to run the system. Here’s what I see:

<html><head><title>Woo! it's Woo!</title></head><body>

<table><tr><td>Welcome to WOO</td></tr></table>

</body></html>

295

Chapter 12 ■ enterprise patterns

As you can see, the feedback message set by the default command has found its way into the output. 

Let’s review the full process that leads to this outcome.

OverviewIt is possible that the detail of the classes covered in this section might disguise the simplicity of the Front Controller pattern. Figure 12-4 shows a sequence diagram that illustrates the life cycle of a request.

Figure 12-4.  The front controller in operation

As you can see, the front controller delegates initialization to the ApplicationHelper object (which could use caching to short-circuit any expensive setup). The Controller then acquires a Command object from the CommandResolver object. Finally, it invokes Command::execute() to kick off the application logic.In this implementation of the pattern, the Command itself is responsible for delegating to the view layer. 

You can see a refinement of this in the next section.

ConsequencesFront Controller is not for the fainthearted. It does require a lot of up-front development before you begin to see benefits. This is a serious drawback if your project requires fast turnaround, or if it is small enough that the Front Controller framework would weigh in heavier than the rest of the system.

Having said that, once you have successfully deployed a Front Controller in one project, you will find that you can reuse it for others with lightning speed. You can abstract much of its functionality into library code, effectively building yourself a reusable framework.

The requirement that all configuration information be loaded up for every request is another 

drawback. All approaches will suffer from this to some extent, but Front Controller often requires additional information, such as logical maps of commands and views.

This overhead can be eased considerably by caching such data. The most efficient way of doing this is to add the data to your system as native PHP. This is fine if you are the sole maintainer of a system; but if you have nontechnical users, you may need to provide a configuration file. You can still automate the 

296

Chapter 12 ■ enterprise patterns

native PHP approach, though, by creating a system that reads a configuration file and then builds PHP data structures, which it writes to a cache file. Once the native PHP cache has been created, the system will use it in preference to the configuration file until a change is made and the cache must be rebuilt.

On the plus side, Front Controller centralizes the presentation logic of your system. This means that you 

can exert control over the way that requests are processed and views are selected in one place (well, in one set of classes, anyway). This reduces duplication and decreases the likelihood of bugs.

Front Controller is also very extensible. Once you have a core up and running, you can add new Command 

classes and views very easily.

In this example, commands handled their own view dispatch. If you use the Front Controller pattern 

with an object that helps with view (and possibly command) selection, then the pattern allows for excellent control over navigation, which is harder to maintain elegantly when presentation control is distributed throughout a system. I cover such an object in the next section.

Application ControllerAllowing commands to invoke their own views is acceptable for smaller systems, but it is not ideal. It is preferable to decouple your commands from your view layer as much as possible.

An application controller takes responsibility for mapping requests to commands, and commands to 

views. This decoupling means that it becomes easier to switch in alternative sets of views without changing the codebase. It also allows the system owner to change the flow of the application, again without the need for touching any internals. By allowing for a logical system of Command resolution, the pattern also makes it easier for the same Command to be used in different contexts within a system.

The ProblemRemember the nature of the example problem. An administrator needs to be able to add a venue to the system and to associate a space with it. The system might, therefore, support the AddVenue and AddSpace commands. According to the examples so far, these commands would be selected using a direct map from a path (/addvenue) to a class (AddVenue).

Broadly speaking, a successful call to the AddVenue command should lead to an initial call to the 

AddSpace command. This relationship might be hard-coded into the classes themselves, with AddVenue invoking AddSpace on success. AddSpace might then include a view that contains the form for adding the space to the venue.

Both commands may be associated with at least two different views, a core view for presenting the 

input form and an error or「thank you」screen. According to the logic already discussed, the Command classes themselves would include those views (using conditional tests to decide which view to present in which circumstances).

This level of hard-coding is fine, as long as the commands will always be used in the same way. It begins 

to break down, though, if I want a special view for AddVenue in some circumstances, and if I want to alter the logic by which one command leads to another (perhaps one flow might include an additional screen between a successful venue addition and the start of a space addition). If each of your commands is only used once, in one relationship to other commands and with one view, then you should hard-code your commands’ relationship with each other and their views. Otherwise, you should read on.

An application controller class can take over this logic, freeing up Command classes to concentrate on 

their job, which is to process input, invoke application logic, and handle any results.

ImplementationAs always, the key to this pattern is the interface. An application controller is a class (or a set of classes) that the front controller can use to acquire commands based on a user request and to find the right view to present after the command has been run. You can see the bare bones of this relationship in Figure 12-5.

297

Chapter 12 ■ enterprise patterns

Figure 12-5.  The Application Controller pattern

As with all patterns in this chapter, the aim is to make things as simple as possible for the client  

code—hence the spartan front controller class. Behind the interface, though, I must deploy an implementation. The approach laid out here is just one way of doing it. As you work through this section, remember that the essence of the pattern lies in the way that the participants (the application controller, the commands, and the views) interact—and not with the specifics of this implementation.

Let’s begin with the code that uses the application controller.

The Front ControllerHere is how the FrontController might work with the AppController class (simplified and stripped of error handling):

// listing 12.19

    // Controller    private function __construct()    {        $this->reg = Registry::instance();    }

    public function handleRequest()    {        $request = $this->reg->getRequest();        $controller = new AppController();        $cmd = $controller->getCommand($request);        $cmd->execute($request);        $view = $controller->getView($request);        $view->render($request);    }

Moving on from the previous example, the principal difference is that, in addition to changing a class 

name from CommandResolver to AppController (admittedly a somewhat cosmetic move), we now retrieve a ViewComponent as well as a Command object. Notice that this code uses a registry object to acquire the Request object. We might also store the AppController object in the Registry—even if it isn’t used elsewhere by other components. Classes that avoid direct instantiation are generally more flexible and easier to test.

298

Chapter 12 ■ enterprise patterns

So by what logic does the AppController know which view to associate with which command? As 

always with object-oriented code, the interface is more important than the implementation. Let’s fill in a possible approach, however.

Implementation OverviewA Command class might demand a different view according to different stages of operation. The default view for the AddVenue command might be a data input form. If the user adds the wrong kind of data, the form may be presented again, or an error page may be shown. If all goes well, and the venue is created in the system, then I may wish to forward to another in a chain of Command objects: AddSpace, perhaps.

The Command objects tell the system of their current state by setting a status flag. Here are the flags that 

this minimal implementation recognizes (set as a property in the Command superclass):

// listing 12.20

    const CMD_DEFAULT = 0;    const CMD_OK = 1;    const CMD_ERROR = 2;    const CMD_INSUFFICIENT_DATA = 3;

The application controller finds and instantiates the correct Command class using the Request object. 

Once it has been run, the Command will be associated with a status. This combination of Command and status can be compared against a data structure to determine which command should be run next, or—if no more commands should be run—which view to serve up.

The Configuration FileThe system’s owner can determine the way that commands and views work together by setting a set of configuration directives. Here is an extract:

    <control>

        <command path="/" class="\popp\ch12\batch06\DefaultCommand">            <view name="main" />            <status value="CMD_ERROR">                <view name="error" />            </status>        </command>

        <command path="/listvenues" class="\popp\ch12\batch06\ListVenues">            <view name="listvenues" />        </command>

        <command path="/quickaddvenue" class="\popp\ch12\batch06\AddVenue">            <view name="quickadd" />        </command>

        <command path="/addvenue" class="\popp\ch12\batch06\AddVenue">            <view name="addvenue" />            <status value="CMD_OK">

299

Chapter 12 ■ enterprise patterns

                <forward path="/addspace" />            </status>        </command>

        <command path="/addspace" class="\popp\ch12\batch06\AddSpace">            <view name="addspace" />            <status value="CMD_OK">                <forward path="/listvenues" />            </status>        </command>

    </control>

This XML fragment shows one strategy for abstracting the flow of commands and their relationship to 

views from the Command classes themselves. The directives are all contained within a control element.

Each command element defines path and class attributes which describe basic command mapping. The logic for views is more complex, however. A view element at the top level of a command defines a default relationship. In other words, if no more specific condition is matched, this view will be used for a command. The status elements define these specific conditions. Their value attributes should match one of the command statuses you have seen. When a command’s execution renders a CMD_OK status, for example, if an equivalent status has been defined in the XML document, the corresponding view element will be used.

A view element defines a name attribute. This value is used to build a path to a template file which can 

then be included.

A command or a status element might contain a forward element instead of a view. The WOO system treats a forward as a special kind of view which, instead of rendering a template, reinvokes the application with a new path.

Let’s work through a fragment of this XML in the light of that explanation:

        <command path="/addvenue" class="\popp\ch12\batch06\AddVenue">            <view name="addvenue" />            <status value="CMD_OK">                <forward path="/addspace" />            </status>        </command>

When the system is invoked with the /addvenue path, the AddVenue command is called. It then 

generates a status value—one of CMD_DEFAULT, CMD_OK, CMD_ERROR, or CMD_INSUFFICIENT_DATA. For any status but CMD_OK, the addvenue template will be invoked. If the command returns CMD_OK status, however, the condition is matched. The status element could simply contain another view that would be included in place of the default. Here, though, the forward element comes into play. By forwarding to another command, the configuration file delegates all responsibility for handling views to the new element. The system will then begin again with the /addspace path in a new request.

Parsing the Configuration FileThanks to the SimpleXML extension, we don’t have to do any actual parsing—that is handled for us. All that is left is to traverse the SimpleXML data structure and build our own data. Here is a class named ViewComponentCompiler that does just that:

// listing 12.21class ViewComponentCompiler

300

Chapter 12 ■ enterprise patterns

{    private static $defaultcmd = DefaultCommand::class;

    public function parseFile($file)    {        $options = \simplexml:load_file($file);        return $this->parse($options);    }

    public function parse(\SimpleXMLElement $options): Conf    {        $conf = new Conf();

        foreach ($options->control->command as $command) {            $path = (string)$command['path'];            $cmdstr = (string)$command['class'];            $path = (empty($path)) ? "/" : $path;            $cmdstr = (empty($cmdstr)) ? self::$defaultcmd : $cmdstr;            $pathobj = new ComponentDescriptor($path, $cmdstr);

            $this->processView($pathobj, 0, $command);

            if (isset($command->status) && isset($command->status['value'])) {                foreach ($command->status as $statusel) {                    $status = (string)$statusel['value'];                    $statusval = constant(Command::class . "::" . $status);

                    if (is_null($statusval)) {                        throw new AppException("unknown status: {$status}");                    }

                    $this->processView($pathobj, $statusval, $statusel);                }            }

            $conf->set($path, $pathobj);        }        return $conf;    }

    public function processView(ComponentDescriptor $pathobj, int $statusval, \SimpleXMLElement $el)    {        if (isset($el->view) && isset($el->view['name'])) {            $pathobj->setView($statusval, new TemplateViewComponent((string)$el->view['name']));        }

        if (isset($el->forward) && isset($el->forward['path'])) {            $pathobj->setView($statusval, new ForwardViewComponent((string)$el->forward['path']));        }    }}

301

Chapter 12 ■ enterprise patterns

The real action here takes place in the parse() method, which accepts a SimpleXMLElement object for 

traversal. I start by instantiating a Conf object (remember, this is just a wrapper around an array). Then I loop through the command elements in the XML. For each command, I extract the values of the path and class attributes, and I pass this data to the constructor of a ComponentDescriptor object. This object will manage the bundle of information associated with a command element—you’ll see the class soon.

Then I call a private method named processView(), passing it the ComponentDescriptor, a zero-

valued integer (because we’re handling the default status), and a reference to the current XML element (that is command right now). Depending on what it finds in the XML fragment, processView() either creates a TemplateViewComponent or a ForwardViewComponent, which it passes along to ComponentDescriptor::setView(). It may match nothing and make no call at all, of course—but that is probably inadvisable. —Perhaps we’d make it an error condition in a fuller implementation.

Back in parse(), I begin work on the status attributes. I call processView() once again—but this time with 

the integer that corresponds to the string in the status element’s value attribute. In other words, the string  CMD_OK becomes 1, CMD_ERROR becomes 2, and so on. PHP’s constant() method provides a neat way of making this conversion. So I pass processView() a non-zero integer this time around, as well as the status XML element.Once again processView() populates the ComponentDescriptor with any found ViewComponent objects.Finally, I store the ComponentDescriptor object in the Conf object, indexed by the command 

component’s path value.

Once the loop is finished, I return the Conf object.It may take a little re-reading before you can follow this flow; but in essence, the process is very 

simple: ViewComponentCompiler builds up an array (wrapped, as previously, in a Conf object) of ComponentDescriptor objects. Each ComponentDescriptor object maintains information about a path and a Command class, as well as an array of ViewComponent objects (managing template display or forwarding) indexed by a status value (0 for the default view).

Despite all this busywork, it is important to remember the high-level process is pretty simple. We are constructing the relationships between potential requests on the one hand, and commands and views on the other. Figure 12-6 shows this initialization process.

Figure 12-6.  Compiling commands and views

Managing the Component DataYou have seen that the compiled ComponentDescriptor objects are stored in a Conf object—essentially a getter and setter for an associative array. The keys here are the paths the system recognizes: /, for example, or /addvenue.

302

So let’s take a look at ComponentDescriptor, which manages command, view, and forward information:

Chapter 12 ■ enterprise patterns

// listing 12.22class ComponentDescriptor{    private $path;    private static $refcmd;    private $cmdstr;

    public function __construct(string $path, string $cmdstr)    {        self::$refcmd = new \ReflectionClass(Command::class);        $this->path = $path;        $this->cmdstr = $cmdstr;    }

    public function getCommand(): Command    {        return $this->resolveCommand($this->cmdstr);    }

    public function setView(int $status, ViewComponent $view)    {        $this->views[$status] = $view;    }

    public function getView(Request $request): ViewComponent    {        $status = $request->getCmdStatus();        $status = (is_null($status)) ? 0 : $status;

        if (isset($this->views[$status])) {            return $this->views[$status];        }

        if (isset($this->views[0])) {            return $this->views[0];        }

        throw new AppException("no view found");    }

    public function resolveCommand(string $class): Command    {        if (is_null($class)) {            throw new AppException("unknown class '$class'");        }

        if (! class_exists($class)) {            throw new AppException("class '$class' not found");        }

303

Chapter 12 ■ enterprise patterns

        $refclass = new \ReflectionClass($class);

        if (! $refclass->isSubClassOf(self::$refcmd)) {            throw new AppException("command '$class' is not a Command");        }

        return $refclass->newInstance();    }}

So you can see the storage and retrieval here, but there’s a little more work going on, too. Command information (the full class name for the Command) is added via the constructor, and only lazily converted into a Command object when getCommand() is called. This instantiation and checking takes place in a private method: resolveCommand(). The code here should look familiar—it’s actually stolen from (ahem … inspired by) the equivalent functionality in CommandResolver from earlier in the chapter.

Acquiring views is easier. Remember, each view component will have been stored via the setView() method. 

Behind the scenes, we now see that the ViewComponent objects are managed in an array property, $views, and indexed by an integer, a Command status value. When the getView() method is called by client code, we are passed a Request object in which the Command status may have been cached. We get at this value via a new convenience method, Request::getCmdStatus(). Armed with this, it’s simply a matter of checking the $views array for a corresponding ViewComponent element. If there is no match, we return the default, which is indexed by zero.

In this way, this little class provides all of the logic implied by a command element in the XML file.Because most of the real work is done by helper classes, the application controller itself is relatively thin. 

Let’s take a look:

// listing 12.23class AppController{    private static $defaultcmd = DefaultCommand::class;    private static $defaultview = "fallback";

    public function getCommand(Request $request): Command    {        try {            $descriptor = $this->getDescriptor($request);            $cmd = $descriptor->getCommand();        } catch (AppException $e) {            $request->addFeedback($e->getMessage());            return new self::$defaultcmd();        }

        return $cmd;    }

    public function getView(Request $request): ViewComponent    {        try {            $descriptor = $this->getDescriptor($request);            $view = $descriptor->getView($request);        } catch (AppException $e) {            return new TemplateViewComponent(self::$defaultview);        }

304

Chapter 12 ■ enterprise patterns

        return $view;    }

    private function getDescriptor(Request $request): ComponentDescriptor    {        $reg = Registry::instance();        $commands = $reg->getCommands();        $path = $request->getPath();        $descriptor = $commands->get($path);

        if (is_null($descriptor)) {            throw new AppException("no descriptor for {$path}", 404);        }

        return $descriptor;    }}

There is little actual logic in this class since most of the complexity has been pushed down to various 

helper classes. Both getCommand() and getView() call a private method, getDescriptor(), to acquire a ComponentDescriptor for the current request. The getDescriptor() method gets the current path from the Request object and uses it to extract a ComponentDescriptor object from a Conf object which is also stored by the registry and returned by getCommands(). Remember that this array of ComponentDescriptor objects was previously populated by the ViewComponentCompiler object with potential paths as keys.Once getCommand() and getView() have a ComponentDescriptor object, each can call its 

corresponding method. In getCommand(), we call ComponentDescriptor::getCommand(); in getView(), we call ComponentDescriptor::getView().

Before we move on, there are a few details to wrap up. Now that Command objects no longer invoke views, 

we need a mechanism for rendering templates. This is handled by TemplateViewComponent objects. These implement an interface, ViewComponent:

// listing 12.24interface ViewComponent{    public function render(Request $request);}

Why the interface? We treat both forwarding and template display as view processes. Here is 

TemplateViewDisplay:

// listing 12.25class TemplateViewComponent implements ViewComponent{    private $name = null;

    public function __construct(string $name)    {        $this->name = $name;    }

305

Chapter 12 ■ enterprise patterns

    public function render(Request $request)    {        $reg = Registry::instance();        $conf = $reg->getConf();        $path = $conf->get("templatepath");

        if (is_null($path)) {            throw new AppException("no template directory");        }

        $fullpath = "{$path}/{$this->name}.php";

        if (! file_exists($fullpath)) {            throw new AppException("no template at {$fullpath}");        }

        include($fullpath);    }}

This class is instantiated with a name—which it then uses at render() time, combined with a path-

configuration value, to include a template.

Here is ForwardViewComponent:

// listing 12.26class ForwardViewComponent implements ViewComponent{    private $path = null;

    public function __construct($path)    {        $this->path = $path;    }

    public function render(Request $request)    {        $request->forward($this->path);    }}

This class simply calls forward() on the provided Request object. The implementation of forward() varies depending upon the Request subtype. For HttpRequest, it is a matter of setting the Location header:

// listing 12.27

    // HttpRequest

    public function forward(string $path)    {        header("Location: {$path}");        exit;    }

306

For CliRequest we can’t rely on the server to handle forwarding, so we have to take a different 

Chapter 12 ■ enterprise patterns

approach:

// listing 12.28

    // CliRequest

    public function forward(string $path)    {        // tack the new path onto the end the argument list        // last argument wins        $_SERVER['argv'][] = "path:{$path}";        Registry::reset();        Controller::run();    }

We take advantage of the fact that, when the argument array is parsed for a path, the final match found 

is ultimately set on the Request. All we need do is add a path argument, clear the Registry, and run the controller from the top.

And that leads us full circle, an excellent moment for an overview!The strategies an application controller might use to acquire views and commands can vary 

considerably; the key is that these are hidden away from the wider system. Figure 12-7 shows the high-level process by which a Front Controller class uses an application controller to acquire first a Command object and then a view.

Figure 12-7.  Using an application controller to acquire commands and views

307

Chapter 12 ■ enterprise patterns

Note that the view that is rendered in Figure 12-7 could be one of ForwardViewComponent (which will 

start the process over again with a new path) or TemplateViewComponent (which will include a template file).

Remember that the data needed for the process of acquiring Command and ViewComponent objects in 

Figure 12-7 was compiled by our old friend, ApplicationHelper. As a reminder, here is the high-level code that achieved that:

// listing 12.29    private function setupOptions()    {

        //...

        $vcfile = $conf->get("viewcomponentfile");        $cparse = new ViewComponentCompiler();

        $commandandviewdata = $cparse->parseFile($vcfile);        $reg->setCommands($commandandviewdata);    }

The Command ClassNow that commands are no longer responsible for invoking their templates, it’s worth looking briefly at the base class and the implementation. We have already seen the new statuses in the Command class, but there is an additional piece of housekeeping to note:

// listing 12.30abstract class Command{

    const CMD_DEFAULT = 0;    const CMD_OK = 1;    const CMD_ERROR = 2;    const CMD_INSUFFICIENT_DATA = 3;

    final public function __construct()    {    }

    public function execute(Request $request)    {        $status = $this->doExecute($request);        $request->setCmdStatus($status);    }

    abstract public function doExecute(Request $request): int;}

In a good example of the Template Method pattern, the execute() method calls the abstract 

doExecute() method, and caches the return value in the Request object. This will be used a little later by the ComponentDescriptor in selecting the correct view to return.

308

Chapter 12 ■ enterprise patterns

A Concrete CommandHere is how a simple AddVenue command might look:

// listing 12.31class AddVenue extends Command{    public function doExecute(Request $request): int    {        $name = $request->getProperty("venue_name");

        if (is_null($name)) {            $request->addFeedback("no name provided");            return self::CMD_INSUFFICIENT_DATA;        } else {            // do some stuff            $request->addFeedback("'{$name}' added");            return self::CMD_OK;        }

        return self::CMD_DEFAULT;    }}

In fact, this is missing functional code related to building a Venue object and saving it to a database, but we will get to all that. All that’s important at this point is the fact that the command returns different statuses, according to the circumstances. As we have already seen, different statuses will cause different views to be selected and returned by the application controller. So, if we’re using the example XML, when CMD_OK is returned, the forwarding mechanism will trigger forwarding to /addspace. This is triggered in this way only for /addvenue. If the request that caused this command to be invoked uses the path /quickaddvenue, then no forwarding will take place, and the quickaddvenue view will be displayed. The AddVenue command knows nothing of this, though. It sticks to its core responsibilities.

ConsequencesA fully featured instance of the Application Controller pattern can be a pain to set up because of the sheer amount of work that must go into acquiring and applying metadata that describes the relationships between command and request, command and command, and command and view.

For this reason, I tend to implement something like this only when my application tells me it is needed. 

I usually hear this whisper when I find myself adding conditionals to my commands that invoke different views or invoke other commands, according to the circumstances. It is at about this time that I feel that command flow and display logic are beginning to spiral out of my control.

Of course, an application controller can use all sorts of mechanisms to build its associations among 

commands and views, not just the approach I have taken here. Even if you’re starting off with a fixed relationship among a request string, a command name, and a view in all cases, you could still benefit from building an application controller to encapsulate this. It will give you considerable flexibility when you must refactor in order to accommodate more complexity.

309

Chapter 12 ■ enterprise patterns

Page ControllerMuch as I like the Front Controller pattern, it is not always the right approach to take. The investment in up-front design tends to reward the larger system and penalize simple, need-results-now projects. The Page Controller pattern will probably be familiar to you already as it is a common strategy. Nevertheless, it is worth exploring some of the issues.

The ProblemOnce again, the problem is your need to manage the relationship among request, domain logic, and presentation. This is pretty much a constant for enterprise projects. What differs, though, are the constraints placed on you.

If you have a relatively simple project, one in which big up-front design could threaten your deadline without adding huge amounts of value, Page Controller can be a good option for managing requests and views.

Let’s say that you want to present a page that displays a list of all venues in the Woo system. Even with the database retrieval code finished, without Front Controller already in place, I have a daunting task to get just this simple result.

The view is a list of venues; the request is for a list of venues. Errors permitting, the request does not 

lead to a new view, as you might expect in a complex task. The simplest thing that works here is to associate the view and the controller—often in the same page.

ImplementationAlthough the practical reality of Page Controller projects can become fiendish, the pattern is simple. Control is related to a view, or to a set of views. In the simplest case, this means that the control sits in the view itself, although it can be abstracted, especially when a view is closely linked with others (that is, when you might need to forward to different pages in different circumstances).

Here is the simplest flavor of Page Controller:

<?php// listing 12.32namespace popp\ch12\batch07;

try {    $venuemapper = new VenueMapper();    $venues = $venuemapper->findAll();} catch (\Exception $e) {    include('error.php');    exit(0);}

// default page follows?><html><head><title>Venues</title></head><body><h1>Venues</h1>

310

Chapter 12 ■ enterprise patterns

<?php foreach ($venues as $venue) { ?>    <?php print $venue->getName(); ?><br /><?php } ?>

</body></html>

This document has two elements to it. The view element handles display, while the controller  

element manages the request and invokes application logic. Even though view and controller inhabit the same page, they are rigidly separated.

There is very little to this example (aside from the database work going on behind the scenes, of which 

you’ll find more in the next chapter). The PHP block at the top of the page attempts to get a list of Venue objects, which it stores in the $venues global variable.

If an error occurs, the page delegates to a page called error.php by using include(), followed by 

exit() to kill any further processing on the current page. I could equally have used an HTTP forward. If no include takes place, then the HTML at the bottom of the page (the view) is shown.

Figure 12-8.  Page Controllers embedded in views

This will do as a quick test, but a system of any size or complexity will probably need more support  

than that.

The Page Controller code was previously implicitly separated from the view. Here, I make the break, 

starting with a rudimentary Page Controller base class:

// listing 12.33abstract class PageController{    abstract public function process();

    public function __construct()    {        $this->reg = Registry::instance();    }

    public function init()    {        if (isset($_SERVER['REQUEST_METHOD'])) {            $request = new HttpRequest();        } else {            $request = new CliRequest();        }

311

Chapter 12 ■ enterprise patterns

        $this->reg->setRequest($request);    }

    public function forward(string $resource)    {        $request = $this->getRequest();        $request->forward($resource);    }

    public function render(string $resource, Request $request)    {        include($resource);    }

    public function getRequest()    {        return $this->reg->getRequest();    }}

This class uses some of the tools that you have already looked at—in particular, the Request and 

Registry classes. The PageController class’s main roles are to provide access to a Request object and to manage the inclusion of views. This list of purposes would quickly grow in a real project as more child classes discover a need for common functionality.

A child class could live inside the view, and thereby display it by default as before. Or, it could stand 

separate from the view. The latter approach is cleaner, I think, so that’s the path that I take. Here is a PageController that attempts to add a new venue to the system:

// listing 12.34class AddVenueController extends PageController{    public function process()    {        $request = $this->getRequest();

        try {            $name = $request->getProperty('venue_name');

            if (is_null($request->getProperty('submitted'))) {                $request->addFeedback("choose a name for the venue");                $this->render(__DIR__ . '/view/add_venue.php', $request);            } elseif (is_null($name)) {                $request->addFeedback("name is a required field");                $this->render(__DIR__ . '/view/add_venue.php', $request);

                return;            } else {                // add to database                $this->forward('listvenues.php');            }

312

Chapter 12 ■ enterprise patterns

        } catch (Exception $e) {            $this->render(__DIR__.'/view/error.php', $request);        }    }}

The AddVenueController class only implements the process() method. process() is responsible for 

checking the user’s submission. If the user has not submitted a form, or has completed the form incorrectly, the default view (add_venue.php) is included, providing feedback and presenting the form. If I successfully add a new user, then the method invokes forward() to send the user to the ListVenues page controller.

Note the format I used for the view. I tend to differentiate view files from class files by using all 

lowercase file names in the former and camel case (running words together and using capital letters to show the boundaries) in the latter.

You may have noticed that there is nothing within the AddVenueController class that causes it to be 

run. I could place runner code within the same file, but this would make testing difficult (because the very act of including the class would execute its methods). For this reason, I create a runner script for each page. Here is addvenue.php:

// listing 12.35$addvenue = new AddVenueController();$addvenue->init();$addvenue->process();

Here is the view associated with the AddVenueController class:

<!-- listing 12.36 --><html><head><title>Add Venue</title></head><body><h1>Add Venue</h1>

<table><tr><td><?phpprint $request->getFeedbackString("</td></tr><tr><td>");?></td></tr></table>

<form action="/addvenue.php" method="get">    <input type="hidden" name="submitted" value="yes"/>    <input type="text" name="venue_name" /></form>

</body></html>

313

Chapter 12 ■ enterprise patterns

As you can see, the view does nothing but display data and provide the mechanism for generating a new 

request. The request is made to the PageController (via the /addvenue.php runner), not back to the view. Remember, it is the PageController class that is responsible for processing requests.

You can see an overview of this more complicated version of the Page Controller pattern in Figure 12-9.

Figure 12-9.  A Page Controller class hierarchy and its include relationships

ConsequencesThis approach has the great merit that it immediately makes sense to anyone with any web experience. I make a request for venues.php, and that is precisely what I get. Even an error is within the bounds of expectation, with「server error」and「page not found」pages an everyday reality.

Things get a little more complicated if you separate the view from the page controller class, but the near 

one-to-one relationship between the participants is clear enough.

A page controller includes its view once it has completed processing. In some circumstances, though, it forwards instead to another page controller. So, for example, when AddVenue successfully adds a venue, it no longer needs to display the addition form. Instead it delegates to ListVenues.

This is handled within the PageController by the forward() method which, like the 

ForwardViewComponent we have already seen, simply calls forward() on the Request.

Although a page controller class might delegate to Command objects, the benefit of doing so is not as 

marked as it is with Front Controller. Front Controller classes need to work out what the purpose of a request is; page controller classes already know this. The light request checking and logic layer calls that you would put in a Command sit just as easily in a page controller class, and you benefit from the fact that you do not need a mechanism to select your Command objects.

Duplication can be a problem, but the use of a common superclass can factor away a lot of that. You can 

also save on setup time because you can avoid loading data that you won’t need in the current context. Of course, you could do that with Front Controller, too, but the process of discovering what is needed, and what is not, would be much more complicated.

314

Chapter 12 ■ enterprise patterns

The real drawback to the pattern lies in situations where the paths through your views are complex—especially when the same view is used in different ways at different times (add and edit screens are a good example of this). You can find that you get tangled up in conditionals and state checking, and it becomes hard to get an overview of your system.

It is not impossible to start with Page Controller and move toward the Front Controller pattern, however. This is especially true if you are using a PageController superclass. As a rule of thumb, if I estimate a system should take me less than a week or so to complete, and that it isn’t going to need more phases in the future, I would choose Page Controller and benefit from the fast turnaround. If I were building a large project that needs to grow over time and has complex view logic, I would go for a Front Controller every time.

Template View and View HelperTemplate View is pretty much what you get by default in PHP, in that I can commingle presentation markup (HTML) and system code (native PHP). As I have said before, this is both a blessing and a curse because the ease with which these can be brought together represents a temptation to combine application and display logic in the same place—with potentially disastrous consequences.

In PHP then, programming the view is largely a matter of restraint. If it isn’t strictly a matter of display, 

treat any code with the greatest suspicion.

To this end, the View Helper pattern (Alur et al.) provides for a helper class that may be specific to a 

view or shared between multiple views to help with any tasks that require more than the smallest amount of code.

The ProblemThese days it is becoming rarer to find SQL queries and other business logic embedded directly in display pages, but it still happens. I have covered this particular evil in great detail in previous chapters, so I’ll keep this brief.

Web pages that contain too much code can be hard for web producers to work with, as presentation 

components become tangled up in loops and conditionals.

Business logic in the presentation forces you to stick with that interface. You can’t switch in a new view 

easily without porting across a lot of application code, too.

Systems that separate their views from their logic are also easier to test. This is because tests can be 

applied to the functionality of the logic layer in isolation of the noisy distractions of presentation.

Security issues often appear in systems which embed logic in their presentation layer, too. In such 

systems, because database queries and code to handle user input tends to be scattered in with tables and forms and lists, it becomes hard to identify potential hazards.

With many operations recurring from view to view, systems that embed application code in their 

templates tend to fall prey to duplication as the same code structures are pasted from page to page. Where this happens, bugs and maintenance nightmares surely follow.

To prevent this from happening, you should handle application processing elsewhere and allow views to manage presentation only. This is often achieved by making views the passive recipients of data. Where a view does need to interrogate the system, it is a good idea to provide a View Helper object to do any involved work on the view’s behalf.

ImplementationOnce you have created a wider framework, the view layer is not a massive programming challenge.  Of course, it remains a huge design and information-architecture issue, but that’s another book!

315

Chapter 12 ■ enterprise patterns

Template View was so named by Fowler. It is a staple pattern used by most enterprise programmers. In some languages, an implementation might involve cooking up a templating system that translates tags to values set by the system. You have that option in PHP, too. You could use a templating engine like the excellent Twig. My preferred option, though, is to use PHP’s existing functionality, but to use it with care.

In order for a view to have something to work with, it must be able to acquire data. I like to define a View 

Helper that views can use.

Here is a simple View Helper class:

// listing 12.37class ViewHelper{    public function sponsorList()    {        // do something complicated to get the sponsor list        return "Bob's Shoe Emporium";    }}

All this class does at present is provide a sponsor list string. Let’s assume that there is some relatively 

complex process to acquire or format this data that we should not embed in the template itself. You can extend it to provide additional functionality as your application evolves. If you find yourself doing something in a view that takes up more than a couple of lines, chances are it belongs in the View Helper. In a larger application, you may provide multiple View Helper objects in an inheritance hierarchy in order to provide different tools for different parts of your system.

I might acquire a View Helper from a factory of some kind—perhaps the registry. From the point of view 

of the template, the simplest approach is to make a helper instance available in the render() method:

// listing 12.38    public function render(string $resource, Request $request)    {        $vh = new ViewHelper();        // now the template will have the $vh variable        include($resource);    }

Here is a simple view that uses the View Helper:

<!-- listing 12.39 --><html><head><title>Venues</title></head><body><h1>Venues</h1>

<div>Proudly sponsored by: <?php echo $vh->sponsorList(); ?>

</div>

316

Chapter 12 ■ enterprise patterns

Listing venues

</body></html>

The view (list_venues.php) is granted a ViewHelper instance in the $vh variable. It calls the 

sponsorList() method and prints the results.

Clearly, this example doesn’t banish code from the view, but it does severely limit the amount and kind of coding that needs to be done. The page contains a simple print statement and will inevitably require other method calls as it grows in complexity, but a designer should be able to work around code of this kind with little or no effort.

Slightly more problematic are if statements and loops. These are difficult to delegate to a View Helper 

because they are usually bound up with formatted output. I tend to keep both simple conditionals and loops (which are very common in building tables that display rows of data) inside the Template View; but to keep them as simple as possible, I delegate things like test clauses, where possible.

ConsequencesThere is something slightly disturbing about the way that data is passed to the view layer, in that a view doesn’t really have a fixed interface that guarantees its environment. I tend to think of every view as entering into a contract with the system at large. The view effectively says to the application,「If I am invoked, then I have a right to access object This, object That, and object TheOther.」It is up to the application to ensure that this is the case.

You could make views stricter by providing accessor methods in the helper classes, but I have always found it easier to register objects dynamically for the view layer through a Request, Response, or Context object.

While templates are often essentially passive, populated with data resulting from the last request, there may be times when the view needs to make an ancillary request. The View Helper is a good place to provide this functionality, keeping any knowledge of the mechanism by which data is required hidden from the view itself. Even the View Helper should do as little work as possible, delegating to a command or contacting the domain layer via a facade.

 You saw the Facade pattern in Chapter 10. alur et al. look at one use of Facades in enterprise 

 ■ Note programming in the session Facade pattern (which is designed to limit fine-grained network transactions). Fowler also describes a pattern called service Layer, which provides a simple point of access to the complexities within a layer.

The Business Logic Layer

If the control layer orchestrates communication with the outside world and marshals a system’s response to it, the logic layer gets on with the business of an application. This layer should be as free as possible of the noise and trauma generated as query strings are analyzed, HTML tables are constructed, and feedback messages composed. Business logic is about doing the stuff that needs doing—the true purpose of the application. Everything else exists just to support these tasks.

317

Chapter 12 ■ enterprise patterns

In a classic object-oriented application, the business logic layer is often composed of classes that model 

the problems that the system aims to address. As you shall see, this is a flexible design decision. It also requires significant up-front planning.

Let’s begin, then, with the quickest way of getting a system up and running.

Transaction ScriptThe Transaction Script pattern (Patterns of Enterprise Application Architecture) describes the way that many systems evolve of their own accord. It is simple, intuitive, and effective, although it becomes less so as systems grow. A transaction script handles a request inline, rather than delegating to specialized objects. It is the quintessential quick fix. It is also a hard pattern to categorize because it combines elements from other layers in this chapter. I have chosen to present it as part of the business logic layer because the pattern’s motivation is to achieve the business aims of the system.

The ProblemEvery request must be handled in some way. As you have seen, many systems provide a layer that assesses and filters incoming data. Ideally, though, this layer should then call on classes that are designed to fulfill the request. These classes could be broken down to represent forces and responsibilities in a system, perhaps with a facade interface. This approach requires a certain amount of careful design, however. For some projects (typically small in scope and urgent in nature), such development overhead can be unacceptable. In this case, you may need to build your business logic into a set of procedural operations. Each operation will be crafted to handle a particular request.

The problem, then, is the need to provide a fast and effective mechanism for fulfilling a system’s 

objectives without a potentially costly investment in complex design.

The great benefit of this pattern is the speed with which you can get results. Each script takes input 

and manipulates the database to ensure an outcome. Beyond organizing related methods within the same class and keeping the Transaction Script classes in their own tier (that is, as independent as possible of the command, control, and view layers), there is little up-front design required.

While business logic layer classes tend to be clearly separated from the presentation layer, they are 

often more embedded in the data layer. This is because retrieving and storing data is key to the tasks that such classes often perform. You will see mechanisms for decoupling logic objects from the database later in the chapter. Transaction Script classes, though, usually know all about the database (although they can use gateway classes to handle the details of their actual queries).

ImplementationLet’s return to my events listing example. In this case, the system supports three relational database tables: venue, space, and event. A venue may have a number of spaces (e.g., a theater can have more than one stage, and a dance club may have different rooms). Each space plays host to many events. Here is the schema:

CREATE TABLE 'venue' (  'id' int(11) NOT NULL auto_increment,  'name' text,  PRIMARY KEY  ('id'))CREATE TABLE 'space' (  'id' int(11) NOT NULL auto_increment,

318

Chapter 12 ■ enterprise patterns

  'venue' int(11) default NULL,  'name' text,  PRIMARY KEY  ('id'))CREATE TABLE 'event' (  'id' int(11) NOT NULL auto_increment,  'space' int(11) default NULL,  'start' mediumtext,  'duration' int(11) default NULL,  'name' text,  PRIMARY KEY  ('id'))

Clearly, the system will need mechanisms for adding both venues and events. Each of these represents 

a single transaction. I could give each method its own class (and organize my classes according to the Command pattern that you encountered in Chapter 11). In this case, though, I am going to place the methods in a single class, albeit as part of an inheritance hierarchy. You can see the structure in Figure 12-10.

Figure 12-10.  A Transaction Script class with its superclass

So why does this example include an abstract superclass? In a script of any size, I would be likely to add 

more concrete classes to this hierarchy. Since most of these will share at least some core functionality, it makes sense to lodge this in a common parent.

In fact, this is a pattern in its own right (Fowler has named it Layer Supertype). Where classes in a layer share characteristics, it makes sense to group them into a single type, locating utility operations in the base class. You will see this a lot in the rest of this chapter.

In this case, the base class acquires a PDO object, which it stores in a property. It also provides methods 

for caching database statements and making queries:

// listing 12.40abstract class Base{    private $pdo;    private $config = __DIR__ . "/data/woo_options.ini";

319

Chapter 12 ■ enterprise patterns

    private $stmts = [];

    public function __construct()    {        $reg = Registry::instance();        $options = parse_ini_file($this->config, true);        $conf = new Conf($options['config']);        $reg->setConf($conf);        $dsn = $reg->getDSN();

        if (is_null($dsn)) {            throw new AppException("No DSN");        }

        $this->pdo = new \PDO($dsn);        $this->pdo->setAttribute(\PDO::ATTR_ERRMODE, \PDO::ERRMODE_EXCEPTION);    }

    public function getPdo(): \PDO    {        return $this->pdo;    }}

I use the Registry class to acquire a DSN string, which I pass to the PDO constructor. I make the PDO object available via a getter method: getPdo(). In fact, a lot of this work can be pushed back into the Registry object itself—a strategy you’ll see that I have adopted elsewhere in this chapter and the next.

Here is the start of the VenueManager class, which sets up my SQL statements:

// listing 12.41class VenueManager extends Base{

    private $addvenue = "INSERT INTO venue                          ( name )                          VALUES( ? )";

    private $addspace  = "INSERT INTO space                          ( name, venue )                          VALUES( ?, ? )";

    private $addevent =  "INSERT INTO event                          ( name, space, start, duration )                          VALUES( ?, ?, ?, ? )";

    // ...

Not much new here. These are the SQL statements that the transaction scripts will use. They 

are constructed in a format accepted by the PDO class’s prepare() method. The question marks are placeholders for the values that will be passed to execute(). Now it’s time to define the first method designed to fulfill a specific business need:

320

Chapter 12 ■ enterprise patterns

// listing 12.42

    // VenueManager

    public function addVenue(string $name, array $spaces): array    {        $pdo = $this->getPdo();        $ret = [];        $ret['venue'] = [$name];        $stmt = $pdo->prepare($this->addvenue);        $stmt->execute($ret['venue']);        $vid = $pdo->lastInsertId();

        $ret['spaces'] = [];

        $stmt = $pdo->prepare($this->addspace);        foreach ($spaces as $spacename) {            $values = [$spacename, $vid];            $stmt->execute($values);            $sid = $pdo->lastInsertId();            array_unshift($values, $sid);            $ret['spaces'][] = $values;        }

        return $ret;    }

As you can see, addVenue() requires a venue name and an array of space names. It uses these to 

populate the venue and space tables. It also creates a data structure that contains this information, along with the newly generated ID values for each row.

If there’s an error with this, remember, an exception is thrown. I don’t catch any exceptions here, so 

anything thrown by prepare() will also be thrown by this method. This is the result I want, although I should to make it clear that this method throws exceptions in my documentation.

Having created the venue row, I loop through $spaces, adding a row in the space table for each element. Notice that I include the venue ID as a foreign key in each of the space rows I create, associating the row with the venue.

The second transaction script is similarly straightforward:

// listing 12.43

    // VenueManager

    public function bookEvent(int $spaceid, string $name, int $time, int $duration)    {        $pdo = $this->getPdo();        $stmt = $pdo->prepare($this->addevent);        $stmt->execute([$name, $spaceid, $time, $duration]);    }

The purpose of this script is to add an event to the events table, associated with a space.

321

Chapter 12 ■ enterprise patterns

ConsequencesThe Transaction Script pattern is an effective way of getting good results fast. It is also one of those patterns many programmers have used for years without imagining it might need a name. With a few good helper methods like those I added to the base class, you can concentrate on application logic without getting too bogged down in database fiddle-faddling.

I have seen Transaction Script appear in a less welcome context. I thought I was writing a much more 

complex and object-heavy application than would usually suit this pattern. As the pressure of deadlines began to tell, I found that I was placing more and more logic in what was intended to be a thin facade onto a Domain Model (see the next section). Although the result was less elegant than I had wanted, I have to admit that the application did not appear to suffer for its implicit redesign.

In most cases, you would choose a Transaction Script approach with a small project when you are 

certain it isn’t going to grow into a large one. The approach does not scale well because duplication often begins to creep in as the scripts inevitably cross one another. You can go some way to factoring this out, of course, but you probably will not be able to excise it completely.

In my example, I decide to embed database code in the transaction script classes themselves. As you 

saw, though, the code wants to separate the database work from the application logic. I can make that break absolute by pulling it out of the class altogether and creating a gateway class whose role it is to handle database interactions on the system’s behalf.

Domain ModelThe Domain Model is the pristine logical engine that many of the other patterns in this chapter strive to create, nurture, and protect. It is an abstracted representation of the forces at work in your project. It’s a kind of plane of forms, where your business problems play out their nature unencumbered by nasty material issues like databases and web pages.

If that seems a little flowery, let’s bring it down to reality. A Domain Model is a representation of the real-world participants of your system. It is in the Domain Model that the object-as-thing rule of thumb is truer than elsewhere. Everywhere else, objects tend to embody responsibilities. In the Domain Model, they often describe a set of attributes, with added agency. They are things that do stuff.

The ProblemIf you have been using Transaction Script, you may find that duplication becomes a problem as different scripts need to perform the same tasks. That can be factored out to a certain extent, but over time, it’s easy to fall into cut-and-paste coding.

You can use a Domain Model to extract and embody the participants and process of your system. Rather than using a script to add space data to the database, and then associate event data with it, you can create Space and Event classes. Booking an event in a space can then become as simple as a call to Space::bookEvent(). A task like checking for a time clash becomes Event::intersects(), and so on.

Clearly, with an example as simple as Woo, a Transaction Script is more than adequate. But as domain logic gets more complex, the alternative of a Domain Model becomes increasingly attractive. Complex logic can be handled more easily, and you need less conditional code when you model the application domain.

ImplementationDomain Models can be relatively simple to design. Most of the complexity associated with the subject lies in the patterns that are designed to keep the model pure—that is, to separate it from the other tiers in the application.

322

Chapter 12 ■ enterprise patterns

Separating the participants of a Domain Model from the presentation layer is largely a matter of ensuring that they keep to themselves. Separating the participants from the data layer is much more problematic. Although the ideal is to consider a Domain Model only in terms of the problems it represents and resolves, the reality of the database is hard to escape.

It is common for Domain Model classes to map fairly directly to tables in a relational database, and 

this certainly makes life easier. Figure 12-11, for example, shows a class diagram that sketches some of the participants of the Woo system.

Figure 12-11.  An extract from a Domain Model

The objects in Figure 12-11 mirror the tables that were set up for the Transaction Script example. 

This direct association makes a system easier to manage, but it is not always possible, especially if you are working with a database schema that precedes your application. Such an association can itself be the source of problems. If you’re not careful, you can end up modeling the database, rather than the problems and forces you are attempting to address.

Just because a Domain Model often mirrors the structure of a database does not mean that its classes 

should have any knowledge of it. By separating the model from the database, you make the entire tier easier to test and less likely to be affected by changes of schema, or even changes of storage mechanism. It also focuses the responsibility of each class on its core tasks.

Here is a simplified Venue object, together with its parent class:

// listing 12.44abstract class DomainObject{    private $id;

323

Chapter 12 ■ enterprise patterns

    public function __construct(int $id)    {        $this->id = $id;    }

    public function getId(): int    {        return $this->id;    }

    public static function getCollection(string $type): Collection    {        // dummy implementation        return Collection::getCollection($type);    }

    public function markDirty()    {        // next chapter!    }}

// listing 12.45class Venue extends DomainObject{    private $name;    private $spaces;

    public function __construct(int $id, string $name)    {        $this->name = $name;        $this->spaces = self::getCollection(Space::class);        parent::__construct($id);    }

    public function setSpaces(SpaceCollection $spaces)    {        $this->spaces = $spaces;    }

    public function getSpaces(): SpaceCollection    {        return $this->spaces;    }

    public function addSpace(Space $space)    {        $this->spaces->add($space);        $space->setVenue($this);    }

324

Chapter 12 ■ enterprise patterns

    public function setName(string $name)    {        $this->name = $name;        $this->markDirty();    }

    public function getName(): string    {        return $this->name;    }}

There are a few points that distinguish this class from one intended to run without persistence. Instead of an array, I am using an object of type SpaceCollection to store any Space objects the Venue might contain (though it could be argued that a type-safe array is a bonus whether you are working with a database or not!). Because this class works with a special collection object rather than an array of Space objects, the constructor needs to instantiate an empty collection on startup. It does this by calling a static method on the layer supertype:

 $this->spaces = self::getCollection(Space::class);

I will return to this system’s collection objects and how to acquire them in the next chapter. For now, 

though, the superclass simply returns an empty array.

 ■ Note  in this chapter and the next, i will discuss amendments to both the Venue and Space objects. these are simple domain objects, and they share a common functional core. if you’re coding along, you should be able to apply concepts i discuss to either class. a Space class may not maintain a collection of Space objects for example, but it might manage Event objects in exactly the same way.

I expect an $id parameter in the constructor that I pass to the superclass for storage. It should come as 

no surprise to learn that the $id parameter represents the unique ID of a row in the database. Notice also that I call a method on the superclass called markDirty()(this will be covered when you encounter the Unit of Work pattern).

ConsequencesThe design of a Domain Model needs to be as simple or complicated as the business processes you need to emulate. The beauty of this is that you can focus on the forces in your problem as you design the model, handling issues like persistence and presentation in other layers—in theory, that is.

In practice, I think that most developers design their domain models with at least one eye on the 

database. No one wants to design structures that will force you (or, worse, your colleagues) into somersaults of convoluted code when it comes to getting your objects in and out of the database.

This separation between the Domain Model and the data layer comes at a considerable cost in terms 

of design and planning. It is possible to place database code directly in the model (although you would probably want to design a gateway to handle the actual SQL). For relatively simple models, especially if each class broadly maps to a table, this approach can be a real win, saving you the considerable design overhead of devising an external system for reconciling your objects with the database.

325

Chapter 12 ■ enterprise patterns

Summary

I have covered an enormous amount of ground here (although I have also left out a lot). You should not feel daunted by the sheer volume of code in this chapter. Patterns are meant to be used in the right circumstances, and combined when useful. Use those described in this chapter that you feel meet the needs of your project, and do not feel that you must build an entire framework before embarking on a project. On the other hand, there is enough material here to form the basis of a framework, or just as likely, to provide some insight into the architecture of some of the prebuilt frameworks you might choose to deploy.

And there’s more! I left you teetering on the edge of persistence, with just a few tantalizing hints about 

collections and mappers to tease you. In the next chapter, I will look at some patterns for working with databases and for insulating your objects from the details of data storage.

326

CHAPTER 13

