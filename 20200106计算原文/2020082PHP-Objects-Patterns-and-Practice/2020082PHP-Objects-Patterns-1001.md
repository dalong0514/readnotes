Patterns for Flexible Object Programming

With strategies for generating objects covered, we’re free now to look at some strategies for structuring classes and objects. I will focus in particular on the principle that composition provides greater flexibility than inheritance. The patterns I examine in this chapter are once again drawn from the Gang of Four catalog.

This chapter will cover a trio of patterns:

•	

•	

•	

The Composite pattern: Composing structures in which groups of objects can be used as if they were individual objects

The Decorator pattern: A flexible mechanism for combining objects at runtime to extend functionality

The Facade pattern: Creating a simple interface to complex or variable systems

Structuring Classes to Allow Flexible Objects

Way back in Chapter 4, I said that beginners often confuse objects and classes. This was only half true. In fact, most of the rest of us occasionally scratch our heads over UML class diagrams, attempting to reconcile the static inheritance structures they show with the dynamic object relationships their objects will enter into off the page.

Remember the pattern principle,「Favor composition over inheritance」? This principle distills this tension between the organization of classes and objects. In order to build flexibility into our projects, we structure our classes so that their objects can be composed into useful structures at runtime.

This is a common theme running through the first two patterns of this chapter. Inheritance is an 

important feature in both, but part of its importance lies in providing the mechanism by which composition can be used to represent structures and extend functionality.

The Composite Pattern

The Composite pattern is perhaps the most extreme example of inheritance deployed in the service of composition. It is a simple and yet breathtakingly elegant design. It is also fantastically useful. Be warned, though; it is so neat, you might be tempted to overuse this strategy.

211

Chapter 10 ■ patterns for flexible objeCt programming

The Composite pattern is a simple way of aggregating and then managing groups of similar objects so that an individual object is indistinguishable to a client from a collection of objects. The pattern is, in fact, very simple, but it is also often confusing. One reason for this is the similarity in structure of the classes in the pattern to the organization of its objects. Inheritance hierarchies are trees, beginning with the super class at the root, and branching out into specialized subclasses. The inheritance tree of classes laid down by the Composite pattern is designed to allow the easy generation and traversal of a tree of objects.

If you are not already familiar with this pattern, you have every right to feel confused at this point. Let’s try an analogy to illustrate the way that single entities can be treated in the same way as collections of things. Given broadly irreducible ingredients such as cereals and meat (or soya if you prefer), we can make a food product—a sausage, for example. We then act on the result as a single entity. Just as we eat, cook, buy, or sell meat, we can eat, cook, buy, or sell the sausage that the meat in part composes. We might take the sausage and combine it with the other composite ingredients to make a pie, thereby rolling a composite into a larger composite. We behave in the same way to the collection as we do to the parts. The Composite pattern helps us to model this relationship between collections and components in our code.

The ProblemManaging groups of objects can be quite a complex task, especially if the objects in question might also contain objects of their own. This kind of problem is very common in coding. Think of invoices, with line items that summarize additional products or services, or things-to-do lists with items that themselves contain multiple subtasks. In content management, we can’t move for trees of sections, pages, articles, or media components. Managing these structures from the outside can quickly become daunting.

Let’s return to a previous scenario. I am designing a system based on a game called Civilization. A player 

can move units around hundreds of tiles that make up a map. Individual counters can be grouped together to move, fight, and defend themselves as a unit. Here I define a couple of unit types:

// listing 10.01

abstract class Unit{    abstract public function bombardStrength(): int;}

class Archer extends Unit{    public function bombardStrength(): int    {        return 4;    }}

class LaserCannonUnit extends Unit{    public function bombardStrength(): int    {        return 44;    }}

212

Chapter 10 ■ patterns for flexible objeCt programming

The Unit class defines an abstract bombardStrength() method, which sets the attack strength of a 

unit bombarding an adjacent tile. I implement this in both the Archer and LaserCannonUnit classes. These classes would also contain information about movement and defensive capabilities, but I’ll keep things simple. I could define a separate class to group units together, like this:

// listing 10.02

class Army{    private $units = [];

    public function addUnit(Unit $unit)    {        array_push($this->units, $unit);    }

    public function bombardStrength(): int    {        $ret = 0;        foreach ($this->units as $unit) {            $ret += $unit->bombardStrength();        }        return $ret;    }}

// listing 10.03$unit1 = new Archer();$unit2 = new LaserCannonUnit();$army = new Army();$army->addUnit($unit1);$army->addUnit($unit2);print $army->bombardStrength();

The Army class has an addUnit() method that accepts a Unit object. Unit objects are stored in an array 

property called $units. I calculate the combined strength of my army in the bombardStrength() method. This simply iterates through the aggregated Unit objects, calling the bombardStrength() method of  each one.

This model is perfectly acceptable, as long as the problem remains as simple as this. What happens, though, if I were to add some new requirements? Let’s say that an army should be able to combine with other armies. Each army should retain its own identity so that it can disentangle itself from the whole at a later date. The Arch Duke’s brave forces might share common cause today with General Soames’s assault upon the exposed flank of the enemy, but a domestic rebellion may send his army scurrying home at any time. For this reason, I can’t just decant the units from each army into a new force.

213

Chapter 10 ■ patterns for flexible objeCt programming

I could amend the Army class to accept Army objects as well as Unit objects:

// listing 10.04

    public function addArmy(Army $army)    {        array_push($this->armies, $army);    }

Then I’d need to amend the bombardStrength() method to iterate through all armies as well as units:

// listing 10.05    public function bombardStrength(): int    {        $ret = 0;        foreach ($this->units as $unit) {            $ret += $unit->bombardStrength();        }        foreach ($this->armies as $army) {            $ret += $army->bombardStrength();        }        return $ret;    }

This additional complexity is not too problematic at the moment. Remember, though, I would need to 

do something similar in methods like defensiveStrength(), movementRange(), and so on. My game is going to be richly featured. Already the business group is calling for troop carriers that can hold up to ten units to improve their movement range on certain terrains. Clearly, a troop carrier is similar to an army in that it groups units. It also has its own characteristics. I could further amend the Army class to handle TroopCarrier objects, but I know that there will be a need for still more unit groupings. It is clear that I need a more flexible model.

Let’s look again at the model I have been building. All the classes I created shared the need for a 

bombardStrength() method. In effect, a client does not need to distinguish between an army, a unit, or a troop carrier. They are functionally identical. They need to move, attack, and defend. Those objects that contain others need to provide methods for adding and removing them. These similarities lead us to an inevitable conclusion. Because container objects share an interface with the objects that they contain, they are naturally suited to share a type family.

ImplementationThe Composite pattern defines a single inheritance hierarchy that lays down two distinct sets of responsibilities. We have already seen both of these in our example. Classes in the pattern must support a common set of operations as their primary responsibility. For us, that means the bombardStrength() method. Classes must also support methods for adding and removing child objects.

Figure 10-1 shows a class diagram that illustrates the Composite pattern as applied to our problem.

214

Chapter 10 ■ patterns for flexible objeCt programming

Figure 10-1.  The Composite pattern

As you can see, all the units in this model extend the Unit class. A client can be sure, then, that any Unit object will support the bombardStrength() method. So, an Army can be treated in exactly the same way as an Archer.

The Army and TroopCarrier classes are composites: they are designed to hold Unit objects. The Archer and LaserCannon classes are leaves, designed to support unit operations, but not to hold other Unit objects. There is actually an issue as to whether leaves should honor the same interface as composites, as they do in Figure 10-1. The diagram shows TroopCarrier and Army aggregating other units, even though the leaf classes are also bound to implement addUnit(). I will return to this question shortly. Here is the abstract Unit class:

// listing 10.06abstract class Unit{    abstract public function addUnit(Unit $unit);    abstract public function removeUnit(Unit $unit);    abstract public function bombardStrength(): int;}

As you can see, I lay down the basic functionality for all Unit objects here. Now, let’s see how a 

composite object might implement these abstract methods:

// listing 10.07

class Army extends Unit{    private $units = [];

    public function addUnit(Unit $unit)    {        if (in_array($unit, $this->units, true)) {            return;        }

215

Chapter 10 ■ patterns for flexible objeCt programming

        $this->units[] = $unit;    }

    public function removeUnit(Unit $unit)    {        $idx = array_search($unit, $this->units, true);        if (is_int($idx)) {            array_splice($this->units, $idx, 1, []);        }    }

    public function bombardStrength(): int    {        $ret = 0;        foreach ($this->units as $unit) {            $ret += $unit->bombardStrength();        }        return $ret;    }}

The addUnit() method checks whether I have already added the same Unit object before storing it in 

the private $units array property. removeUnit() uses a similar check to remove a given Unit object from the property.

Army objects, then, can store Units of any kind, including other Army objects, or leaves such as Archer or LaserCannonUnit. Because all units are guaranteed to support bombardStrength(), our Army::bombardStrength() method simply iterates through all the child Unit objects stored in the $units property, calling the same method on each.

One problematic aspect of the Composite pattern is the implementation of add and remove 

functionality. The classic pattern places add() and remove() methods in the abstract super class. This ensures that all classes in the pattern share a common interface. As you can see here, though, it also means that leaf classes must provide an implementation:

// listing 10.08

class UnitException extends \Exception{}

// listing 10.09

class Archer extends Unit{    public function addUnit(Unit $unit)    {        throw new UnitException(get_class($this) . " is a leaf");    }

    public function removeUnit(Unit $unit)    {        throw new UnitException(get_class($this) . " is a leaf");    }

216

Chapter 10 ■ patterns for flexible objeCt programming

    public function bombardStrength(): int    {        return 4;    }}

I do not want to make it possible to add a Unit object to an Archer object, so I throw exceptions if addUnit() or removeUnit() are called. I will need to do this for all leaf objects, so I could perhaps improve my design by replacing the abstract addUnit()/removeUnit() methods in Unit with default implementations like the one in the preceding example:

// listing 10.10

abstract class Unit{    public function addUnit(Unit $unit)    {        throw new UnitException(get_class($this) . " is a leaf");    }

    public function removeUnit(Unit $unit)    {        throw new UnitException(get_class($this) . " is a leaf");    }

    abstract public function bombardStrength(): int;}

// listing 10.11

class Archer extends Unit{    public function bombardStrength(): int    {        return 4;    }}

This removes duplication in leaf classes, but has the drawback that a composite is not forced at compile time 

to provide an implementation of addUnit() and removeUnit(), which could cause problems down the line.I will look in more detail at some of the problems presented by the Composite pattern in the next 

section. Let’s end this section by examining some of its benefits:

•	

•	

Flexibility: Because everything in the Composite pattern shares a common supertype, it is very easy to add new composite or leaf objects to the design without changing a program’s wider context.

Simplicity: A client using a Composite structure has a straightforward interface. There is no need for a client to distinguish between an object that is composed of others and a leaf object (except when adding new components). A call to Army::bombardStrength() may cause a cascade of delegated calls behind the scenes; but to the client, the process and result are exactly equivalent to those associated with calling Archer::bombardStrength().

217

Chapter 10 ■ patterns for flexible objeCt programming

•	

•	

Implicit reach: Objects in the Composite pattern are organized in a tree. Each composite holds references to its children. An operation on a particular part of the tree, therefore, can have a wide effect. We might remove a single Army object from its Army parent and add it to another. This simple act is wrought on one object, but it has the effect of changing the status of the Army object’s referenced Unit objects and of their own children.

Explicit reach: Tree structures are easy to traverse. They can be iterated in order to gain information or to perform transformations. We will look at a particularly powerful technique for this in the next chapter when we deal with the Visitor pattern.

Often, you really see the benefit of a pattern only from the client’s perspective, so here are a couple of 

armies:

// listing 10.12

// create an army$main_army = new Army();

// add some units$main_army->addUnit(new Archer());$main_army->addUnit(new LaserCannonUnit());

// create a new army$sub_army = new Army();

// add some units$sub_army->addUnit(new Archer());$sub_army->addUnit(new Archer());$sub_army->addUnit(new Archer());

// add the second army to the first$main_army->addUnit($sub_army);

// all the calculations handled behind the scenesprint "attacking with strength: {$main_army->bombardStrength()}\n";

I create a new Army object and add some primitive Unit objects. I repeat the process for a second Army 

object that I then add to the first. When I call Unit::bombardStrength() on the first Army object, all the complexity of the structure that I have built up is entirely hidden.

ConsequencesIf you’re anything like me, you would have heard alarm bells ringing when you saw the code extract for the Archer class. Why do we put up with these redundant addUnit() and removeUnit() methods in leaf classes that do not need to support them? An answer of sorts lies in the transparency of the Unit type.

If a client is passed a Unit object, it knows that the addUnit() method will be present. The Composite 

pattern principle that primitive (leaf) classes have the same interface as composites is upheld. This does not actually help you much because you still do not know how safe you might be calling addUnit() on any Unit object you might come across.

218

Chapter 10 ■ patterns for flexible objeCt programming

If I move these add/remove methods down so that they are available only to composite classes, then 

passing a Unit object to a method leaves me with the problem that I do not know by default whether or not it supports addUnit(). Nevertheless, leaving booby-trapped methods lying around in leaf classes makes me uncomfortable. It adds no value and confuses a system’s design because the interface effectively lies about its own functionality.

You can split composite classes off into their own CompositeUnit subtype quite easily. First of all, I 

excise the add/remove behavior from Unit:

// listing 10.13

abstract class Unit{    public function getComposite()    {        return null;    }

    abstract public function bombardStrength(): int;}

Notice the new getComposite() method. I will return to this in a little while. Now, I need a new abstract 

class to hold addUnit() and removeUnit(). I can even provide default implementations:

// listing 10.14

abstract class CompositeUnit extends Unit{    private $units = [];

    public function getComposite(): CompositeUnit    {        return $this;    }

    public function addUnit(Unit $unit)    {        if (in_array($unit, $this->units, true)) {            return;        }

        $this->units[] = $unit;    }

    public function removeUnit(Unit $unit)    {        $idx = array_search($unit, $this->units, true);        if (is_int($idx)) {            array_splice($this->units, $idx, 1, []);        }    }

219

Chapter 10 ■ patterns for flexible objeCt programming

    public function getUnits(): array    {        return $this->units;    }}

The CompositeUnit class is declared abstract, even though it does not itself declare an abstract method. 

It does, however, extend Unit, and it does not implement the abstract bombardStrength() method. Army (and any other composite classes) can now extend CompositeUnit. The classes in my example are now organized as in Figure 10-2.

Figure 10-2.  Moving add/remove methods out of the base class

The annoying, useless implementations of add/remove methods in the leaf classes are gone, but the 

client must still check to see whether it has a CompositeUnit before it can use addUnit().

This is where the getComposite() method comes into its own. By default, this method returns a null value. Only in a CompositeUnit class does it return CompositeUnit. So if a call to this method returns an object, we should be able to call addUnit() on it. Here’s a client that uses this technique:

// listing 10.15

class UnitScript{    public static function joinExisting(        Unit $newUnit,        Unit $occupyingUnit    ): CompositeUnit {        $comp = $occupyingUnit->getComposite();        if (! is_null($comp)) {            $comp->addUnit($newUnit);        } else {            $comp = new Army();

220

Chapter 10 ■ patterns for flexible objeCt programming

            $comp->addUnit($occupyingUnit);            $comp->addUnit($newUnit);        }        return $comp;    }}

The joinExisting() method accepts two Unit objects. The first is a newcomer to a tile, and the second 

is a prior occupier. If the second Unit is a CompositeUnit, then the first will attempt to join it. If not, then a new Army will be created to cover both units. I have no way of knowing at first whether the $occupyingUnit argument contains a CompositeUnit. A call to getComposite() settles the matter, though. If getComposite() returns an object, I can add the new Unit object to it directly. If not, I create the new Army object and add both.

I could simplify this model further by having the Unit::getComposite() method return an Army object 

prepopulated with the current Unit. Or I could return to the previous model (which did not distinguish structurally between composite and leaf objects) and have Unit::addUnit() do the same thing: create an Army object and add both Unit objects to it. This is neat, but it presupposes that you know in advance the type of composite you would like to use to aggregate your units. Your business logic will determine the kinds of assumptions you can make when you design methods like getComposite() and addUnit().

These contortions are symptomatic of a drawback to the Composite pattern. Simplicity is achieved by 

ensuring that all classes are derived from a common base. The benefit of simplicity is sometimes bought at a cost to type safety. The more complex your model becomes, the more manual type checking you are likely to have to do. Let’s say that I have a Cavalry object. If the rules of the game state that you cannot put a horse on a troop carrier, I have no automatic way of enforcing this with the Composite pattern:

// listing 10.16

class TroopCarrier extends CompositeUnit{    public function addUnit(Unit $unit)    {        if ($unit instanceof Cavalry) {            throw new UnitException("Can't get a horse on the vehicle");        }        parent::addUnit($unit);    }

    public function bombardStrength(): int    {        return 0;    }}

I am forced to use the instanceof operator to test the type of the object passed to addUnit(). If you 

have too many special cases of this kind, the drawbacks of the pattern begin to outweigh its benefits. Composite works best when most of the components are interchangeable.

Another issue to bear in mind is the cost of some Composite operations. The Army::bombardStrength() 

method is typical in that it sets off a cascade of calls to the same method down the tree. For a large tree with lots of subarmies, a single call can cause an avalanche behind the scenes. bombardStrength() is not itself very expensive, but what would happen if some leaves performed a complex calculation to arrive at their return values? One way around this problem is to cache the result of a method call of this sort in the parent 

221

Chapter 10 ■ patterns for flexible objeCt programming

object, so that subsequent invocations are less expensive. You need to be careful, though, to ensure that the cached value does not grow stale. You should devise strategies to wipe any caches whenever any operations take place on the tree. This may require that you give child objects references to their parents.

Finally, a note about persistence. The Composite pattern is elegant, but it doesn’t lend itself neatly to storage in a relational database. This is because, by default, you access the entire structure only through a cascade of references. To construct a Composite structure from a database in the natural way, you would have to make multiple expensive queries. You can get around this problem by assigning an ID to the whole tree, so that all components can be drawn from the database in one go. Having acquired all the objects, however, you would still have the task of recreating the parent/child references, which themselves would have to be stored in the database. This is not difficult, but it is somewhat messy.

Although Composites sit uneasily with relational databases, they lend themselves very well indeed to 

storage in XML. This is because XML elements are often themselves composed of trees of subelements.

Composite in SummarySo the Composite pattern is useful when you need to treat a collection of things in the same way as you would an individual, either because the collection is intrinsically like a component (armies and archers), or because the context gives the collection the same characteristics as the component (line items in an invoice). Composites are arranged in trees, so an operation on the whole can affect the parts, and data from the parts is transparently available via the whole. The Composite pattern makes such operations and queries transparent to the client. Trees are easy to traverse (as we shall see in the next chapter). It is easy to add new component types to Composite structures.

On the downside, Composites rely on the similarity of their parts. As soon as we introduce complex 

rules as to which composite object can hold which set of components, our code can become hard to manage. Composites do not lend themselves well to storage in relational databases, but are well suited to XML persistence.

The Decorator Pattern

While the Composite pattern helps us to create a flexible representation of aggregated components, the Decorator pattern uses a similar structure to help us to modify the functionality of concrete components. Once again, the key to this pattern lies in the importance of composition at runtime. Inheritance is a neat way of building on characteristics laid down by a parent class. This neatness can lead you to hard-code variation into your inheritance hierarchies, often causing inflexibility.

The ProblemBuilding all your functionality into an inheritance structure can result in an explosion of classes in a system. Even worse, as you try to apply similar modifications to different branches of your inheritance tree, you are likely to see duplication emerge.

Let’s return to our game. Here, I define a Tile class and a derived type:

// listing 10.17

abstract class Tile{    abstract public function getWealthFactor(): int;}

222

Chapter 10 ■ patterns for flexible objeCt programming

// listing 10.18class Plains extends Tile{    private $wealthfactor = 2;

    public function getWealthFactor(): int    {        return $this->wealthfactor;    }}

A tile represents a square on which my units might be found. Each tile has certain characteristics. In 

this example, I have defined a getWealthFactor() method that affects the revenue a particular square might generate if owned by a player. As you can see, Plains objects have a wealth factor of 2. Obviously, tiles manage other data. They might also hold a reference to image information, so that the board can be drawn. Once again, I’ll keep things simple here.

I need to modify the behavior of the Plains object to handle the effects of natural resources and human abuse. I wish to model the occurrence of diamonds on the landscape, and the damage caused by pollution. One approach might be to inherit from the Plains object:

// listing 10.19

class DiamondPlains extends Plains{    public function getWealthFactor(): int    {        return parent::getWealthFactor() + 2;    }}

// listing 10.20

class PollutedPlains extends Plains{    public function getWealthFactor(): int    {        return parent::getWealthFactor() - 4;    }}

I can now acquire a polluted tile very easily:

// listing 10.21

$tile = new PollutedPlains();print $tile->getWealthFactor();

You can see the class diagram for this example in Figure 10-3.

223

Chapter 10 ■ patterns for flexible objeCt programming

Figure 10-3.  Building variation into an inheritance tree

This structure is obviously inflexible. I can get plains with diamonds. I can get polluted plains. But can 

I get them both? Clearly not, unless I am willing to perpetrate the horror that is PollutedDiamondPlains. This situation can only get worse when I introduce the Forest class, which can also have diamonds and pollution.

This is an extreme example, of course, but the point is made. Relying entirely on inheritance to define 

your functionality can lead to a multiplicity of classes and a tendency toward duplication.

Let’s take a more commonplace example at this point. Serious web applications often have to perform a range of actions on a request before a task is initiated to form a response. You might need to authenticate the user, for example, and to log the request. Perhaps you should process the request to build a data structure from raw input. Finally, you must perform your core processing. You are presented with the same problem.

You can extend the functionality of a base ProcessRequest class with additional processing in a derived LogRequest class, in a StructureRequest class, and in an AuthenticateRequest class. You can see this class hierarchy in Figure 10-4.

Figure 10-4.  More hard-coded variations

224

Chapter 10 ■ patterns for flexible objeCt programming

What happens, though, when you need to perform logging and authentication, but not data 

preparation? Do you create a LogAndAuthenticateProcessor class? Clearly, it is time to find a more flexible solution.

ImplementationRather than use only inheritance to solve the problem of varying functionality, the Decorator pattern uses composition and delegation. In essence, Decorator classes hold an instance of another class of their own type. A Decorator will implement an operation so that it calls the same operation on the object to which it has a reference before (or after) performing its own actions. In this way, it is possible to build a pipeline of Decorator objects at runtime.

Let’s rewrite our game example to illustrate this:

abstract class Tile{    abstract public function getWealthFactor(): int;}

class Plains extends Tile{    private $wealthfactor = 2;

    public function getWealthFactor(): int    {        return $this->wealthfactor;    }}

// listing 10.22

abstract class TileDecorator extends Tile{    protected $tile;

    public function __construct(Tile $tile)    {        $this->tile = $tile;    }}

Here, I have declared Tile and Plains classes as before, but I have also introduced a new class: 

TileDecorator. This does not implement getWealthFactor(), so it must be declared abstract. I define a constructor that requires a Tile object, which it stores in a property called $tile. I make this property protected so that child classes can gain access to it. Now I’ll redefine the Pollution and Diamond classes:

// listing 10.23

class DiamondDecorator extends TileDecorator{    public function getWealthFactor(): int    {

225

Chapter 10 ■ patterns for flexible objeCt programming

        return $this->tile->getWealthFactor() + 2;    }}

// listing 10.24

class PollutionDecorator extends TileDecorator{    public function getWealthFactor(): int    {        return $this->tile->getWealthFactor() - 4;    }}

Each of these classes extends TileDecorator. This means that they have a reference to a Tile object. When getWealthFactor() is invoked, each of these classes invokes the same method on its Tile reference before making its own adjustment.

By using composition and delegation like this, you make it easy to combine objects at runtime. 

Because all the objects in the pattern extend Tile, the client does not need to know which combination it is working with. It can be sure that a getWealthFactor() method is available for any Tile object, whether it is decorating another behind the scenes or not:

// listing 10.25

$tile = new Plains();print $tile->getWealthFactor(); // 2

Plains is a component. It simply returns 2:

// listing 10.26

$tile = new DiamondDecorator(new Plains());print $tile->getWealthFactor(); // 4

DiamondDecorator has a reference to a Plains object. It invokes getWealthFactor() before adding its 

own weighting of 2:

// listing 10.27

$tile = new PollutionDecorator(new DiamondDecorator(new Plains()));print $tile->getWealthFactor(); // 0

PollutionDecorator has a reference to a DiamondDecorator object, which has its own Tile reference.You can see the class diagram for this example in Figure 10-5.

226

Chapter 10 ■ patterns for flexible objeCt programming

Figure 10-5.  The Decorator pattern

This model is very extensible. You can add new decorators and components very easily. With lots of 

decorators, you can build very flexible structures at runtime. The component class, Plains in this case, can be significantly modified in many ways without the need to build the totality of the modifications into the class hierarchy. In plain English, this means you can have a polluted Plains object that has diamonds, without having to create a PollutedDiamondPlains object.

The Decorator pattern builds up pipelines that are very useful for creating filters. The java.io package 

makes great use of decorator classes. The client coder can combine decorator objects with core components to add filtering, buffering, compression, and so on to core methods like read(). My web request example can also be developed into a configurable pipeline. Here’s a simple implementation that uses the Decorator pattern:

// listing 10.28

class RequestHelper{}

// listing 10.29

abstract class ProcessRequest{    abstract public function process(RequestHelper $req);}

// listing 10.30

class MainProcess extends ProcessRequest{    public function process(RequestHelper $req)    {        print __CLASS__ . ": doing something useful with request\n";    }}

227

Chapter 10 ■ patterns for flexible objeCt programming

// listing 10.31

abstract class DecorateProcess extends ProcessRequest{    protected $processrequest;

    public function __construct(ProcessRequest $pr)    {        $this->processrequest = $pr;    }}

As before, we define an abstract superclass (ProcessRequest), a concrete component (MainProcess), 

and an abstract decorator (DecorateProcess). MainProcess::process() does nothing but report that it has been called. DecorateProcess stores a ProcessRequest object on behalf of its children. Here are some simple concrete decorator classes:

// listing 10.32

class LogRequest extends DecorateProcess{    public function process(RequestHelper $req)    {        print __CLASS__ . ": logging request\n";        $this->processrequest->process($req);    }}

// listing 10.33

class AuthenticateRequest extends DecorateProcess{    public function process(RequestHelper $req)    {        print __CLASS__ . ": authenticating request\n";        $this->processrequest->process($req);    }}

// listing 10.34

class StructureRequest extends DecorateProcess{    public function process(RequestHelper $req)    {        print __CLASS__ . ": structuring request data\n";        $this->processrequest->process($req);    }}

Each process() method outputs a message before calling the referenced ProcessRequest object’s own process() method. You can now combine objects instantiated from these classes at runtime to build filters 

228

that perform different actions on a request, and in different orders. Here’s some code to combine objects from all these concrete classes into a single filter:

Chapter 10 ■ patterns for flexible objeCt programming

// listing 10.35

$process = new AuthenticateRequest(new StructureRequest(    new LogRequest(        new MainProcess()    )));$process->process(new RequestHelper());

This code gives the following output:

popp\ch10\batch07\AuthenticateRequest: authenticating requestpopp\ch10\batch07\StructureRequest: structuring request datapopp\ch10\batch07\LogRequest: logging requestpopp\ch10\batch07\MainProcess: doing something useful with request

 this example is, in fact, also an instance of an enterprise pattern called intercepting filter. 

 ■ Note intercepting filter is described in Core J2EE Patterns: Best Practices and Design Strategies (prentice hall, 2001) by alur et al.

ConsequencesLike the Composite pattern, Decorator can be confusing. It is important to remember that both composition and inheritance are coming into play at the same time. So LogRequest inherits its interface from ProcessRequest, but it is acting as a wrapper around another ProcessRequest object.

Because a decorator object forms a wrapper around a child object, it helps to keep the interface as 

sparse as possible. If you build a heavily featured base class, then decorators are forced to delegate to all public methods in their contained object. This can be done in the abstract decorator class, but it still introduces the kind of coupling that can lead to bugs.

Some programmers create decorators that do not share a common type with the objects they modify. As long as they fulfill the same interface as these objects, this strategy can work well. You get the benefit of being able to use the built-in interceptor methods to automate delegation (implementing __call() to catch calls to nonexistent methods and invoking the same method on the child object automatically). However, by doing this, you also lose the safety afforded by class type checking. In our examples so far, client code can demand a Tile or a ProcessRequest object in its argument list and be certain of its interface, whether or not the object in question is heavily decorated.

The Facade Pattern

You may have had occasion to stitch third-party systems into your own projects in the past. Whether or not the code is object oriented, it will often be daunting, large, and complex. Your own code, too, may become a challenge to the client programmer who needs only to access a few features. The Facade pattern is a way of providing a simple, clear interface to complex systems.

229

Chapter 10 ■ patterns for flexible objeCt programming

The ProblemSystems tend to evolve large amounts of code that is really only useful within the system itself. Just as classes define clear public interfaces and hide their guts away from the rest of the world, so should well-designed systems. However, it is not always clear which parts of a system are designed to be used by client code and which are best hidden.

As you work with subsystems (like web forums or gallery applications), you may find yourself making 

calls deep into the logic of the code. If the subsystem code is subject to change over time, and your code interacts with it at many different points, you may find yourself with a serious maintenance problem as the subsystem evolves.

Similarly, when you build your own systems, it is a good idea to organize distinct parts into separate 

tiers. Typically, you may have a tier responsible for application logic, another for database interaction, another for presentation, and so on. You should aspire to keep these tiers as independent of one another as you can, so that a change in one area of your project will have minimal repercussions elsewhere. If code from one tier is tightly integrated into code from another, then this objective is hard to meet.

Here is some deliberately confusing procedural code that makes a song-and-dance routine of the 

simple process of getting log information from a file and turning it into object data:

// listing 10.36

function getProductFileLines($file){    return file($file);}

function getProductObjectFromId($id, $productname){    // some kind of database lookup    return new Product($id, $productname);}

function getNameFromLine($line){    if (preg_match("/.*-(.*)\s\d+/", $line, $array)) {        return str_replace('_', ' ', $array[1]);    }    return '';}

function getIDFromLine($line){    if (preg_match("/^(\d{1,3})-/", $line, $array)) {        return $array[1];    }    return -1;}

class Product{    public $id;    public $name;

230

Chapter 10 ■ patterns for flexible objeCt programming

    public function __construct($id, $name)    {        $this->id = $id;        $this->name = $name;    }}

Let’s imagine that the internals of this code are more complicated than they actually are, and that I am stuck with using it rather than rewriting it from scratch. For example, assume I have to turn a file that contains lines like these into an array of objects:

234-ladies_jumper 55532-gents_hat 44

To do so, I must call all of these functions (note that, for the sake of brevity, I don’t extract the final 

number, which represents a price):

// listing 10.37

$lines = getProductFileLines(__DIR__ . '/test2.txt');$objects = [];foreach ($lines as $line) {    $id = getIDFromLine($line);    $name = getNameFromLine($line);    $objects[$id] = getProductObjectFromID($id, $name);}

If I call these functions directly like this throughout my project, my code will become tightly wound into 

the subsystem it is using. This could cause problems if the subsystem changes, or if I decide to switch it out entirely. I really need to introduce a gateway between the system and the rest of our code.

ImplementationHere is a simple class that provides an interface to the procedural code you encountered in the previous section:

// listing 10.38

class ProductFacade{    private $products = [];

    public function __construct(string $file)    {        $this->file = $file;        $this->compile();    }

    private function compile()    {        $lines = getProductFileLines($this->file);

231

Chapter 10 ■ patterns for flexible objeCt programming

        foreach ($lines as $line) {            $id = getIDFromLine($line);            $name = getNameFromLine($line);            $this->products[$id] = getProductObjectFromID($id, $name);        }    }

    public function getProducts(): array    {        return $this->products;    }

    public function getProduct(string $id): \Product    {        if (isset($this->products[$id])) {            return $this->products[$id];        }        return null;    }}

From the point of view of the client code, access to Product objects from a log file is much simplified:

// listing 10.39

$facade = new ProductFacade(__DIR__ . '/test2.txt');$object = $facade->getProduct("234");

ConsequencesA Facade is really a very simple concept. It is just a matter of creating a single point of entry for a tier or subsystem. This has a number of benefits. It helps to decouple distinct areas in a project from one another. It is useful and convenient for client coders to have access to simple methods that achieve clear ends. It reduces errors by focusing the use of a subsystem in one place; changes to the subsystem should cause failure in a predictable location. Errors are also minimized by Facade classes in complex subsystems where client code might otherwise use internal functions incorrectly.

Despite the simplicity of the Facade pattern, it is all too easy to forget to use it, especially if you are familiar with the subsystem you are working with. There is a balance to be struck, of course. On the one hand, the benefit of creating simple interfaces to complex systems should be clear. On the other hand, one could abstract systems with reckless abandon, and then abstract the abstractions. If you are making significant simplifications for the clear benefit of client code, and/or shielding it from systems that might change, then you are probably right to implement the Facade pattern.

232

Chapter 10 ■ patterns for flexible objeCt programming

Summary

In this chapter, I looked at a few of the ways that classes and objects can be organized in a system. In particular, I focused on the principle that composition can be used to engender flexibility where inheritance fails. In both the Composite and Decorator patterns, inheritance is used to promote composition and to define a common interface that provides guarantees for client code.

You also saw delegation used effectively in these patterns. Finally, I looked at the simple but powerful Facade pattern. Facade is one of those patterns that many people have been using for years without having a name to give it. Facade lets you provide a clean point of entry to a tier or subsystem. In PHP, the Facade pattern is also used to create object wrappers that encapsulate blocks of procedural code.

233

CHAPTER 11

Performing and Representing Tasks

In this chapter, we get active. I look at patterns that help you to get things done, whether interpreting a mini-language or encapsulating an algorithm.

This chapter will walk you through several patterns:

•	

•	

•	

•	•	

•	

The Interpreter pattern: Building a mini-language interpreter that can be used to create scriptable applications

The Strategy pattern: Identifying algorithms in a system and encapsulating them into their own types

The Observer pattern: Creating hooks for alerting disparate objects about system events

The Visitor pattern: Applying an operation to all the nodes in a tree of objects

The Command pattern: Creating command objects that can be saved and passed around

The Null Object pattern: Using non-operational objects in place of null values.

The Interpreter Pattern

Languages are written in other languages (at least at first). PHP itself, for example, is written in C.  By the same token, odd as it may sound, you can define and run your own languages using PHP. Of course, any language you might create will be slow and somewhat limited. Nonetheless, mini-languages can be  very useful, as you will see in this chapter.

The ProblemWhen you create web (or command-line) interfaces in PHP, you give the user access to functionality. The trade-off in interface design is between power and ease-of-use. As a rule, the more power you give your user, the more cluttered and confusing your interface becomes. Good interface design can help a lot here, of course. But if 90 percent of users are using the same 30 percent of your features, the costs of piling on the functionality may outweigh the benefits. You may wish to consider simplifying your system for most users. But what of the power users, that ten percent who use your system’s advanced features? Perhaps you can accommodate them in a different way. By offering such users a domain language (often called a  DSL—Domain Specific Language), you might actually extend the power of your application.

235

Chapter 11 ■ performing and representing tasks

Of course, you have a programming language at hand right away. It’s called PHP. Here’s how you could 

allow your users to script your system:

$form_input = $_REQUEST['form_input'];// contains: "print file_get_contents('/etc/passwd');"eval($form_input);

This approach to making an application scriptable is clearly insane. Just in case the reasons are not 

blatantly obvious, they boil down to two issues: security and complexity. The security issue is well addressed in the example. By allowing users to execute PHP via your script, you are effectively giving them access to the server the script runs on. The complexity issue is just as big a drawback. No matter how clear your code is, the average user is unlikely to extend it easily and certainly not from the browser window.

A mini-language, though, can address both these problems. You can design flexibility into the language, 

reduce the possibility that the user can do damage, and keep things focused.

Imagine an application for authoring quizzes. Producers design questions and establish rules for 

marking the answers submitted by contestants. It is a requirement that quizzes must be marked without human intervention, even though some answers can be typed into a text field by users.

Here’s a Question:

How many members in the Design Patterns gang?

You can accept「four」or「4」as correct answers. You might create a web interface that allows a producer 

to use a regular Expression for marking responses:

^4|four$

Most producers are not hired for their knowledge of regular expressions, however. To make everyone’s 

life easier, you might implement a more user-friendly mechanism for marking responses:

$input equals "4" or $input equals "four"

You propose a language that supports variables, an operator called equals, and Boolean logic (or and 

and). Programmers love naming things, so let’s call it MarkLogic. It should be easy to extend, as you envisage lots of requests for richer features. Let’s leave aside the issue of parsing input for now and concentrate on a mechanism for plugging these elements together at runtime to produce an answer. This, as you might expect, is where the Interpreter pattern comes in.

ImplementationA language is made up of expressions (that is, things that resolve to a value). As you can see in Table 11-1, even a tiny language like MarkLogic needs to keep track of a lot of elements.

236

Chapter 11 ■ performing and representing tasks

Table 11-1.  Elements of the MarkLogic Grammar

Description

EBNF Name

Class Name

VariableString literalBoolean and

variable

VariableExpression

<stringLiteral>

LiteralExpression

andExpr

BooleanAndExpression

Boolean or

orExpr

BooleanOrExpression

Example

$input

"four"

$input equals '4' and $other equals '6'

$input equals '4' or $other equals '6'

Equality test

eqExpr

EqualsExpression

$input equals '4'

Table 11-1 lists EBNF names. So what is EBNF all about? It’s a notation that you can use to describe a language grammar. EBNF stands for Extended Backus-Naur Form. It consists of a series of lines (called productions), each one consisting of a name and a description that takes the form of references to other productions and to terminals (that is, elements that are not themselves made up of references to other productions). Here is one way of describing my grammar using EBNF:

expr     = operand { orExpr | andExpr }operand  = ( '(' expr ')' | ? string literal ? | variable ) { eqExpr }orExpr   = 'or' operandandExpr  = 'and' operandeqExpr   = 'equals' operandvariable = '$' , ? word ?

Some symbols have special meanings (that should be familiar from regular Expression notation): | means or, for example. You can group elements using brackets. So in the example, an Expression (expr) consists of an operand followed by zero or more of either orExpr or andExpr. An operand can be a bracketed Expression, a quoted string (I have omitted the production for this), or a variable followed by zero or more instances of eqExpr. Once you get the hang of referring from one production to another, EBNF becomes quite easy to read.

In Figure 11-1, I represent the elements of my grammar as classes.

237

Chapter 11 ■ performing and representing tasks

Figure 11-1.  The Interpreter classes that make up the MarkLogic language

As you can see, BooleanAndExpression and its siblings inherit from OperatorExpression. This is 

because these classes all perform their operations upon other Expression objects. VariableExpression and LiteralExpression work directly with values.

All Expression objects implement an interpret() method that is defined in the abstract base class, 

Expression. The interpret() method expects an InterpreterContext object that is used as a shared data store. Each Expression object can store data in the InterpreterContext object. The InterpreterContext will then be passed along to other Expression objects. So that data can be retrieved easily from the InterpreterContext, the Expression base class implements a getKey() method that returns a unique handle. Let’s see how this works in practice with an implementation of Expression:

// listing 11.01

abstract class Expression{    private static $keycount = 0;    private $key;

    abstract public function interpret(InterpreterContext $context);

    public function getKey()    {        if (! isset($this->key)) {            self::$keycount++;            $this->key = self::$keycount;        }

238

Chapter 11 ■ performing and representing tasks

        return $this->key;    }}

// listing 11.02

class LiteralExpression extends Expression{    private $value;

    public function __construct($value)    {        $this->value = $value;    }

    public function interpret(InterpreterContext $context)    {        $context->replace($this, $this->value);    }}

// listing 11.03

class InterpreterContext{    private $expressionstore = [];

    public function replace(Expression $exp, $value)    {        $this->expressionstore[$exp->getKey()] = $value;    }

    public function lookup(Expression $exp)    {        return $this->expressionstore[$exp->getKey()];    }}

// listing 11.04

$context = new InterpreterContext();$literal = new LiteralExpression('four');$literal->interpret($context);print $context->lookup($literal) . "\n";

Here’s the output:

four

239

Chapter 11 ■ performing and representing tasks

I’ll begin with the InterpreterContext class. As you can see, it is really only a front end for an associative array, $expressionstore, which I use to hold data. The replace() method accepts an Expression object as key and a value of any type, and then adds the pair to $expressionstore. It also provides a lookup() method for retrieving data.

The Expression class defines the abstract interpret() method and a concrete getKey() method that 

uses a static counter value to generate, store, and return an identifier.

This method is used by InterpreterContext::lookup() and InterpreterContext::replace() to 

index data.

The LiteralExpression class defines a constructor that accepts a value argument. The interpret() 

method requires a InterpreterContext object. I simply call replace(), using getKey() to define the key for retrieval and the $value property. This will become a familiar pattern as you examine the other Expression classes. The interpret() method always inscribes its results upon the InterpreterContext object.

I include some client code as well, instantiating both an InterpreterContext object and a 

LiteralExpression object (with a value of "four"). I pass the InterpreterContext object to  LiteralExpression::interpret(). The interpret() method stores the key/value pair in InterpreterContext, from where I retrieve the value by calling lookup().

Here’s the remaining terminal class. VariableExpression is a little more complicated:

// listing 11.05

class VariableExpression extends Expression{    private $name;    private $val;

    public function __construct($name, $val = null)    {        $this->name = $name;        $this->val = $val;    }

    public function interpret(InterpreterContext $context)    {        if (! is_null($this->val)) {            $context->replace($this, $this->val);            $this->val = null;        }    }

    public function setValue($value)    {        $this->val = $value;    }

    public function getKey()    {        return $this->name;    }}

240

Chapter 11 ■ performing and representing tasks

// listing 11.06

$context = new InterpreterContext();$myvar = new VariableExpression('input', 'four');$myvar->interpret($context);print $context->lookup($myvar) . "\n";// output: four

$newvar = new VariableExpression('input');$newvar->interpret($context);print $context->lookup($newvar) . "\n";// output: four

$myvar->setValue("five");$myvar->interpret($context);print $context->lookup($myvar) . "\n";// output: five

print $context->lookup($newvar) . "\n";// output: five

The VariableExpression class accepts both name and value arguments for storage in property 

variables. I provide the setValue() method, so that client code can change the value at any time.

The interpret() method checks whether or not the $val property has a nonnull value. If the $val 

property has a value, it sets it on the InterpreterContext. I then set the $val property to null. This is in case interpret() is called again after another identically named instance of VariableExpression has changed the value in the InterpreterContext object. This is quite a limited variable, accepting only string values. If you intend to extend your language, you should consider having it work with other Expression objects, so that it can contain the results of tests and operations. For now, though, VariableExpression will do the work I need of it. Notice that I have overridden the getKey() method, so that variable values are linked to the variable name and not to an arbitrary static ID.

Operator expressions in the language all work with two other Expression objects in order to 

get their job done. It makes sense, therefore, to have them extend a common superclass. Here is the OperatorExpression class:

// listing 11.07

abstract class OperatorExpression extends Expression{    protected $l_op;    protected $r_op;

    public function __construct(Expression $l_op, Expression $r_op)    {        $this->l_op = $l_op;        $this->r_op = $r_op;    }

    public function interpret(InterpreterContext $context)    {        $this->l_op->interpret($context);        $this->r_op->interpret($context);        $result_l = $context->lookup($this->l_op);

241

Chapter 11 ■ performing and representing tasks

        $result_r = $context->lookup($this->r_op);        $this->doInterpret($context, $result_l, $result_r);    }

    abstract protected function doInterpret(        InterpreterContext $context,        $result_l,        $result_r    );}

OperatorExpression is an abstract class. It implements interpret(), but it also defines the abstract 

dointerpret() method.

The constructor demands two Expression objects, $l_op and $r_op, which it stores in properties.The interpret() method begins by invoking interpret() on both its operand properties (if you have read the previous chapter, you might notice that I am creating an instance of the Composite pattern here). Once the operands have been run, interpret() still needs to acquire the values that this yields. It does this by calling InterpreterContext::lookup() for each property. It then calls dointerpret(), leaving it up to child classes to decide what to do with the results of these operations.

 dointerpret() is an instance of the template method pattern. in this pattern, a parent class both 

 ■ Note defines and calls an abstract method, leaving it up to child classes to provide an implementation. this can streamline the development of concrete classes, as shared functionality is handled by the superclass, leaving the children to concentrate on clean, narrow objectives.

Here’s the EqualsExpression class, which tests two Expression objects for equality:

// listing 11.08

class EqualsExpression extends OperatorExpression{    protected function doInterpret(        InterpreterContext $context,        $result_l,        $result_r    ) {            $context->replace($this, $result_l == $result_r);    }}

EqualsExpression only implements the dointerpret() method, which tests the equality of the operand results it has been passed by the interpret() method, placing the result in the InterpreterContext object.

To wrap up the Expression classes, here are BooleanOrExpression and BooleanAndExpression:

// listing 11.09

class BooleanOrExpression extends OperatorExpression{

242

Chapter 11 ■ performing and representing tasks

    protected function doInterpret(        InterpreterContext $context,        $result_l,        $result_r    ) {        $context->replace($this, $result_l || $result_r);    }}

// listing 11.10class BooleanAndExpression extends OperatorExpression{    protected function doInterpret(        InterpreterContext $context,        $result_l,        $result_r    ) {        $context->replace($this, $result_l && $result_r);    }}

Instead of testing for equality, the BooleanOrExpression class applies a logical or operation and stores 

the result of that via the InterpreterContext::replace() method. BooleanAndExpression, of course, applies a logical and operation.

I now have enough code to execute the mini-language fragment I quoted earlier. Here it is again:

$input equals "4" or $input equals "four"

Here’s how I can build this statement up with my Expression classes:

// listing 11.11

$context = new InterpreterContext();$input = new VariableExpression('input');$statement = new BooleanOrExpression(    new EqualsExpression($input, new LiteralExpression('four')),    new EqualsExpression($input, new LiteralExpression('4')));

I instantiate a variable called "input" but hold off on providing a value for it. I then create a 

BooleanOrExpression object that will compare the results from two EqualsExpression objects. The first of these objects compares the VariableExpression object stored in $input with a LiteralExpression containing the string "four"; the second compares $input with a LiteralExpression object containing the string "4".

Now, with my statement prepared, I am ready to provide a value for the input variable and run the code:

// listing 11.12

foreach (["four", "4", "52"] as $val) {    $input->setValue($val);    print "$val:\n";

243

Chapter 11 ■ performing and representing tasks

    $statement->interpret($context);    if ($context->lookup($statement)) {        print "top marks\n\n";    } else {        print "dunce hat on\n\n";    }}

In fact, I run the code three times, with three different values. The first time through, I set the temporary 

variable $val to "four", assigning it to the input VariableExpression object using its setValue() method. I then call interpret() on the topmost Expression object (the BooleanOrExpression object that contains references to all other expressions in the statement). Here are the internals of this invocation, step-by-step:

•	

•	

•	

•	

•	

•	

•	

•	

•	

$statement calls interpret() on its $l_op property (the first EqualsExpression object).

The first EqualsExpression object calls interpret() on its $l_op property (a reference to the input VariableExpression object, which is currently set to "four").

The input VariableExpression object writes its current value to the provided InterpreterContext object by calling InterpreterContext::replace().

The first EqualsExpression object calls interpret() on its $r_op property (a LiteralExpression object charged with the value "four").

The LiteralExpression object registers its key and its value with InterpreterContext.

The first EqualsExpression object retrieves the values for $l_op ("four") and $r_op ("four") from the InterpreterContext object.

The first EqualsExpression object compares these two values for equality, and then registers the result (true) and its key with the InterpreterContext object.

Back at the top of the tree, the $statement object (BooleanOrExpression) calls interpret() on its $r_op property. This resolves to a value (false, in this case) in the same way the $l_op property did.

The $statement object retrieves values for each of its operands from the InterpreterContext object and compares them using ||. It is comparing true and false, so the result is true. This final result is stored in the InterpreterContext object.

And all that is only for the first iteration through the loop. Here is the final output:

four:top marks

4:top marks

52:dunce hat on

244

Chapter 11 ■ performing and representing tasks

You may need to read through this section a few times before the process clicks. The old issue of object versus class trees might confuse you, here. Expression classes are arranged in an inheritance hierarchy, just as Expression objects are composed into a tree at runtime. As you read back through the code, keep this distinction in mind.

Figure 11-2 shows the complete class diagram for the example.

Figure 11-2.  The Interpreter pattern deployed

Interpreter IssuesOnce you set up the core classes for an Interpreter pattern implementation, it becomes easy to extend. The price you pay is in the sheer number of classes you could end up creating. For this reason, Interpreter is best applied to relatively small languages. If you have a need for a full programming language, you would do better to look for a third-party tool to use.

Because Interpreter classes often perform very similar tasks, it is worth keeping an eye on the classes 

you create with a view to factoring out duplication.

Many people approaching the Interpreter pattern for the first time are disappointed, after some initial 

excitement, to discover that it does not address parsing. This means that you are not yet in a position to offer your users a nice, friendly language. Chapter 24 contains some rough code to illustrate one strategy for parsing a mini-language.

The Strategy Pattern

Classes often try to do too much. It’s understandable: you create a class that performs a few related actions; and, as you code, some of these actions need to be varied according to the circumstances. At the same time, your class needs to be split into subclasses. Before you know it, your design is being pulled apart by competing forces.

245

Chapter 11 ■ performing and representing tasks

The ProblemSince I have recently built a marking language, I’m sticking with the quiz example. Quizzes need questions, so you build a Question class, giving it a mark() method. All is well until you need to support different marking mechanisms.

Imagine that you are asked to support the simple MarkLogic language, marking by straight match and 

regular Expression. Your first thought might be to subclass for these differences, as in Figure 11-3.

Figure 11-3.  Defining subclasses according to marking strategies

This would serve you well, as long as marking remains the only aspect of the class that varies. Imagine, 

though, that you are called on to support different kinds of questions: those that are text-based and those that support rich media. This presents you with a problem when it comes to incorporating these forces in one inheritance tree, as you can see in Figure 11-4.

Figure 11-4.  Defining subclasses according to two forces

246

Chapter 11 ■ performing and representing tasks

Not only have the number of classes in the hierarchy ballooned, but you also necessarily introduce 

repetition. Your marking logic is reproduced across each branch of the inheritance hierarchy.

Whenever you find yourself repeating an algorithm across siblings in an inheritance tree (whether 

through subclassing or repeated conditional statements), consider abstracting these behaviors into their own type.

ImplementationAs with all the best patterns, Strategy is simple and powerful. When classes must support multiple implementations of an interface (e.g., multiple marking mechanisms), the best approach is often to extract these implementations and place them in their own type, rather than to extend the original class to handle them.

So, in the example, your approach to marking might be placed in a Marker type. Figure 11-5 shows the 

new structure.

Figure 11-5.  Extracting algorithms into their own type

Remember the Gang of Four principle,「Favor composition over inheritance」? This is an excellent example. By defining and encapsulating the marking algorithms, you reduce subclassing and increase flexibility. You can add new marking strategies at any time without the need to change the Question classes at all. All Question classes know is that they have an instance of a Marker at their disposal, and that it is guaranteed by its interface to support a mark() method. The details of implementation are entirely somebody else’s problem.

Here are the Question classes rendered as code:

// listing 11.13

abstract class Question{    protected $prompt;    protected $marker;

    public function __construct(string $prompt, Marker $marker)

247

Chapter 11 ■ performing and representing tasks

    {        $this->prompt = $prompt;        $this->marker = $marker;    }

    public function mark(string $response): bool    {        return $this->marker->mark($response);    }}

// listing 11.14

class TextQuestion extends Question{    // do text question specific things}

// listing 11.15

class AVQuestion extends Question{    // do audiovisual question specific things}

As you can see, I have left the exact nature of the difference between TextQuestion and AVQuestion to the imagination. The Question base class provides all the real functionality, storing a prompt property and a Marker object. When Question::mark() is called with a response from the end user, the method simply delegates the problem solving to its Marker object.

Now it’s time to define some simple Marker objects:

// listing 11.16

abstract class Marker{    protected $test;

    public function __construct(string $test)    {        $this->test = $test;    }

    abstract public function mark(string $response): bool;}

// listing 11.17

class MarkLogicMarker extends Marker{    private $engine;

248

Chapter 11 ■ performing and representing tasks

    public function __construct(string $test)    {        parent::__construct($test);        $this->engine = new MarkParse($test);    }

    public function mark(string $response): bool    {        return $this->engine->evaluate($response);    }}

// listing 11.18

class MatchMarker extends Marker{    public function mark(string $response): bool    {        return ($this->test == $response);    }}

// listing 11.19

class RegexpMarker extends Marker{    public function mark(string $response): bool    {        return (preg_match("$this->test", $response) === 1);    }}

There should be little, if anything, that is particularly surprising about the Marker classes themselves. 

Note that the MarkParse object is designed to work with the simple parser developed in Chapter 24. The key here is in the structure that I have defined, rather than in the detail of the strategies themselves. I can swap RegexpMarker for MatchMarker, with no impact on the Question class.

Of course, you must still decide what method to use to choose between concrete Marker objects. I have 

seen two real-world approaches to this problem. In the first, producers used radio buttons to select the preferred marking strategy. In the second, the structure of the marking condition itself was used; that is, a match statement was left plain:

five

A MarkLogic statement was preceded by a colon:

:$input equals 'five'

And a regular Expression used forward slashes:

/f.ve/

249

Chapter 11 ■ performing and representing tasks

Here is some code to run the classes through their paces:

// listing 11.20

$markers = [      new RegexpMarker("/f.ve/"),    new MatchMarker("five"),    new MarkLogicMarker('$input equals "five"')];

foreach ($markers as $marker) {    print get_class($marker)."\n";    $question = new TextQuestion("how many beans make five", $marker);

    foreach (["five", "four"] as $response) {        print "    response: $response: ";        if ($question->mark($response)) {            print "well done\n";        } else {            print "never mind\n";        }    }}

I construct three strategy objects, using each in turn to help construct a TextQuestion object. The 

TextQuestion object is then tried against two sample responses.

Here is the output (including namespaces):

popp\ch11\batch02\RegexpMarker    response: five: well done    response: four: never mindpopp\ch11\batch02\MatchMarker    response: five: well done    response: four: never mindpopp\ch11\batch02\MarkLogicMarker    response: five: well done    response: five: never mind

In the example, I passed specific data (the $response variable) from the client to the strategy object via the mark() method. Sometimes, you may encounter circumstances in which you don’t always know in advance how much information the strategy object will require when its operation is invoked. You can delegate the decision as to what data to acquire by passing the strategy an instance of the client itself. The strategy can then query the client in order to build the data it needs.

The Observer Pattern

Orthogonality is a virtue I have described before. One of our objectives as programmers should be to build components that can be altered or moved with minimal impact on other components. If every change we make to one component necessitates a ripple of changes elsewhere in the codebase, the task of development can quickly become a spiral of bug creation and elimination.

250

Chapter 11 ■ performing and representing tasks

Of course, orthogonality is often just a dream. Elements in a system must have embedded references 

to other elements. You can, however, deploy various strategies to minimize this. You have seen various examples of polymorphism in which the client understands a component’s interface, but the actual component may vary at runtime.

In some circumstances, you may wish to drive an even greater wedge between components than this. 

Consider a class responsible for handling a user’s access to a system:

// listing 11.21

class Login{    const LOGIN_USER_UNKNOWN = 1;    const LOGIN_WRONG_PASS = 2;    const LOGIN_ACCESS = 3;

    private $status = [];

    public function handleLogin(string $user, string $pass, string $ip): bool    {        $isvalid=false;        switch (rand(1, 3)) {            case 1:                $this->setStatus(self::LOGIN_ACCESS, $user, $ip);                $isvalid = true;                break;            case 2:                $this->setStatus(self::LOGIN_WRONG_PASS, $user, $ip);                $isvalid = false;                break;            case 3:                $this->setStatus(self::LOGIN_USER_UNKNOWN, $user, $ip);                $isvalid = false;                break;        }

        print "returning ".(($isvalid)?"true":"false")."\n";

        return $isvalid;    }

    private function setStatus(int $status, string $user, string $ip)    {        $this->status = [$status, $user, $ip];    }

    public function getStatus(): array    {        return $this->status;    }}

251

Chapter 11 ■ performing and representing tasks

In a real-world example, of course, the handleLogin() method would validate the user against a storage 

mechanism. As it is, this class fakes the login process using the rand() function. There are three potential outcomes of a call to handleLogin(). The status flag may be set to LOGIN_ACCESS, LOGIN_WRONG_PASS, or LOGIN_USER_UNKNOWN.

Because the Login class is a gateway guarding the treasures of your business team, it may excite much interest during development and in the months beyond. Marketing might call you up and ask that you keep a log of IP addresses. You can add a call to your system’s Logger class:

// listing 11.22

    public function handleLogin(string $user, string $pass, string $ip): bool    {        switch (rand(1, 3)) {            case 1:                $this->setStatus(self::LOGIN_ACCESS, $user, $ip);                $isvalid = true;                break;            case 2:                $this->setStatus(self::LOGIN_WRONG_PASS, $user, $ip);                $isvalid = false;                break;            case 3:                $this->setStatus(self::LOGIN_USER_UNKNOWN, $user, $ip);                $isvalid = false;                break;        }

        Logger::logIP($user, $ip, $this->getStatus());

        return $isvalid;    }

Worried about security, the system administrators might ask for notification of failed logins. Once again, 

you can return to the login method and add a new call:

// listing 11.23

        if (! $isvalid) {            Notifier::mailWarning(                $user,                $ip,                $this->getStatus()            );        }

The business development team might announce a tie-in with a particular ISP, asking that a cookie be 

set when particular users log in. And so on, and so on.

These are all easy enough requests to fulfill, but addressing them comes at a cost to your design. The 

Login class soon becomes very tightly embedded into this particular system. You cannot pull it out and drop it into another product without going through the code line-by-line and removing everything that is specific to the old system. This isn’t too hard, of course, but then you are off down the road of cut-and-paste coding. 

252

Chapter 11 ■ performing and representing tasks

Now that you have two similar but distinct Login classes in your systems, you find that an improvement to one will necessitate the same changes in the other—until, inevitably and gracelessly, they fall out of alignment with one another.

So what can you do to save the Login class? The Observer pattern is a great fit here.

ImplementationAt the core of the Observer pattern is the unhooking of client elements (the observers) from a central class (the subject). Observers need to be informed when events occur that the subject knows about. At the same time, you do not want the subject to have a hardcoded relationship with its observer classes.

To achieve this, you can allow observers to register themselves with the subject. You give the Login class three new methods, attach(), detach(), and notify(), and enforce this using an interface called Observable:

// listing 11.24

interface Observable{    public function attach(Observer $observer);    public function detach(Observer $observer);    public function notify();}

// listing 11.25

class Login implements Observable{    private $observers = [];    private $storage;

    const LOGIN_USER_UNKNOWN = 1;    const LOGIN_WRONG_PASS   = 2;    const LOGIN_ACCESS       = 3;

    public function attach(Observer $observer)    {        $this->observers[] = $observer;    }

    public function detach(Observer $observer)    {        $this->observers = array_filter(            $this->observers,            function ($a) use ($observer) {                return (! ($a === $observer ));            }        );    }

253

Chapter 11 ■ performing and representing tasks

    public function notify()    {        foreach ($this->observers as $obs) {            $obs->update($this);        }    }    // ...}

So the Login class manages a list of observer objects. These can be added by a third party using 

the attach() method and removed via detach(). The notify() method is called to tell the observers that something of interest has happened. The method simply loops through the list of observers, calling update() on each one.

The Login class itself calls notify() from its handleLogin() method:

// listing 11.26

    public function handleLogin(string $user, string $pass, string $ip)    {        switch (rand(1, 3)) {            case 1:                $this->setStatus(self::LOGIN_ACCESS, $user, $ip);                $isvalid = true;                break;            case 2:                $this->setStatus(self::LOGIN_WRONG_PASS, $user, $ip);                $isvalid = false;                break;            case 3:                $this->setStatus(self::LOGIN_USER_UNKNOWN, $user, $ip);                $isvalid = false;                break;        }

        $this->notify();

        return $isvalid;    }

Here’s the interface for the Observer class:

// listing 11.27

interface Observer{    public function update(Observable $observable);}

Any object that uses this interface can be added to the Login class via the attach() method. Here’s a 

concrete instance:

254

Chapter 11 ■ performing and representing tasks

// listing 11.28

class LoginAnalytics implements Observer{    public function update(Observable $observable)    {        // not type safe!        $status = $observable->getStatus();        print __CLASS__ . ":    doing something with status info\n";    }}

Notice how the observer object uses the instance of Observable to get more information about the 

event. It is up to the subject class to provide methods that observers can query to learn about state. In this case, I have defined a method called getStatus() that observers can call to get a snapshot of the current state of play.

This addition also highlights a problem, though. By calling Login::getStatus(), the LoginAnalytics 

class assumes more knowledge than it safely can. It is making this call on an Observable object, but there’s no guarantee that this will also be a Login object. I have a couple of options here. I could extend the Observable interface to include a getStatus() declaration and perhaps rename it to something like ObservableLogin to signal that it is specific to the Login type.

Alternatively, I could keep the Observable interface generic and make the Observer classes responsible 

for ensuring that their subjects are of the correct type. They could even handle the chore of attaching themselves to their subject. Since there will be more than one type of Observer, and since I’m planning to perform some housekeeping that is common to all of them, here’s an abstract superclass to handle the donkey work:

// listing 11.29

abstract class LoginObserver implements Observer{    private $login;

    public function __construct(Login $login)    {        $this->login = $login;        $login->attach($this);    }

    public function update(Observable $observable)    {        if ($observable === $this->login) {            $this->doUpdate($observable);        }    }

    abstract public function doUpdate(Login $login);}

The LoginObserver class requires a Login object in its constructor. It stores a reference and calls 

Login::attach(). When update() is called, it checks that the provided Observable object is the correct 

255

Chapter 11 ■ performing and representing tasks

reference. It then calls a Template Method: doUpdate(). I can now create a suite of LoginObserver objects, all of which can be secure they are working with a Login object and not just any old Observable:

// listing 11.30

class SecurityMonitor extends LoginObserver{    public function doUpdate(Login $login)    {        $status = $login->getStatus();        if ($status[0] == Login::LOGIN_WRONG_PASS) {            // send mail to sysadmin            print __CLASS__ . ":    sending mail to sysadmin\n";        }    }}

// listing 11.31

class GeneralLogger extends LoginObserver{    public function doUpdate(Login $login)    {        $status = $login->getStatus();        // add login data to log        print __CLASS__ . ":    add login data to log\n";    }}

// listing 11.32

class PartnershipTool extends LoginObserver{    public function doUpdate(Login $login)    {        $status = $login->getStatus();        // check $ip address        // set cookie if it matches a list        print __CLASS__ . ":    set cookie if it matches a list\n";    }}

Creating and attaching LoginObserver classes is now achieved in one go at the time of instantiation:

$login = new Login();new SecurityMonitor($login);new GeneralLogger($login);new PartnershipTool($login);

So now I have created a flexible association between the subject classes and the observers. You can see 

the class diagram for the example in Figure 11-6.

256

Chapter 11 ■ performing and representing tasks

Figure 11-6.  The Observer pattern

PHP provides built-in support for the Observer pattern through the bundled SPL (Standard PHP 

Library) extension. The SPL is a set of tools that help with common, largely object-oriented problems. The Observer aspect of this OO Swiss Army knife consists of three elements: SplObserver, SplSubject, and SplObjectStorage. SplObserver and SplSubject are interfaces and exactly parallel the Observer and Observable interfaces shown in this section’s example. SplObjectStorage is a utility class designed to provide improved storage and removal of objects. Here’s an edited version of the Observer implementation:

// listing 11.33

class Login implements \SplSubject{    private $storage;    // ...

    public function __construct()    {        $this->storage = new \SplObjectStorage();    }

257

Chapter 11 ■ performing and representing tasks

    public function attach(\SplObserver $observer)    {        $this->storage->attach($observer);    }

    public function detach(\SplObserver $observer)    {        $this->storage->detach($observer);    }

    public function notify()    {        foreach ($this->storage as $obs) {            $obs->update($this);        }    }

    // ...}

// listing 11.34abstract class LoginObserver implements \SplObserver{    private $login;

    public function __construct(Login $login)    {        $this->login = $login;        $login->attach($this);    }

    public function update(\SplSubject $subject)    {        if ($subject === $this->login) {            $this->doUpdate($subject);        }    }

    abstract public function doUpdate(Login $login);}

There are no real differences, as far as SplObserver (which was Observer) and SplSubject (which was 

Observable) are concerned—except, of course, I no longer need to declare the interfaces, and I must alter my type hinting according to the new names. SplObjectStorage provides you with a really useful service, however. You may have noticed that, in my initial example, my implementation of Login::detach() applied array_filter (together with an anonymous function) to the $observers array, in order to find and remove the argument object. The SplObjectStorage class does this work for you under the hood. It implements attach() and detach() methods, and can be passed to foreach and iterated like an array.

258

Chapter 11 ■ performing and representing tasks

 You can read more about spL in the php documentation at http://www.php.net/spl. in particular, 

 ■ Note you will find many iterator tools there. i cover php’s built-in iterator interface in Chapter 13,「database patterns.」

Another approach to the problem of communicating between an Observable class and its Observer 

could be to pass specific state information via the update() method, rather than an instance of the subject class. For a quick-and-dirty solution, this is often the approach I would take initially. So in the example, update() would expect a status flag, the username, and IP address (probably in an array for portability), rather than an instance of Login. This saves you from having to write a state method in the Login class. On the other hand, where the subject class stores a lot of state, passing an instance of it to update() allows observers much more flexibility.

You could also lock down type completely, by making the Login class refuse to work with anything 

other than a specific type of observer class (LoginObserver, perhaps). If you want to do that, then you may consider some kind of runtime check on objects passed to the attach() method; otherwise, you may need to reconsider the Observable interface altogether.

Once again, I have used composition at runtime to build a flexible and extensible model. The Login 

class can be extracted from its context and dropped into an entirely different project without qualification. There, it might work with a different set of observers.

The Visitor Pattern

As you have seen, many patterns aim to build structures at runtime, following the principle that composition is more flexible than inheritance. The ubiquitous Composite pattern is an excellent example of this. When you work with collections of objects, you may need to apply various operations to the structure that involve working with each individual component. Such operations can be built into the components themselves. After all, components are often best placed to invoke one another.

This approach is not without issues. You do not always know about all the operations you may need to 

perform on a structure. If you add support for new operations to your classes on a case-by-case basis, you can bloat your interface with responsibilities that don’t really fit. As you might guess, the Visitor pattern addresses these issues.

The ProblemThink back to the Composite example from the previous chapter. For a game, I created an army of components such that the whole and its parts can be treated interchangeably. You saw that operations can be built into components. Typically, leaf objects perform an operation and composite objects call on their children to perform the operation:

// listing 11.35

class Army extends CompositeUnit{    public function bombardStrength(): int    {        $strength = 0;

259

Chapter 11 ■ performing and representing tasks

        foreach ($this->units() as $unit) {            $strength += $unit->bombardStrength();        }

        return $strength;    }}

// listing 11.36

class LaserCanonUnit extends Unit{    public function bombardStrength(): int    {        return 44;    }}

Where this operation is integral to the responsibility of the composite class, there is no problem. There 

are more peripheral tasks, however, that may not sit so happily on the interface.

Here’s an operation that dumps textual information about leaf nodes. It could be added to the abstract 

Unit class:

// listing 11.37

abstract class Unit{    // ...    public function textDump($num = 0): string    {        $txtout = "";        $pad = 4*$num;        $txtout .= sprintf("%{$pad}s", "");        $txtout .= get_class($this).": ";        $txtout .= "bombard: ".$this->bombardStrength()."\n";

        return $txtout;    }    // ...}

This method can then be overridden in the CompositeUnit class:

// listing 11.38

abstract class CompositeUnit extends Unit{    // ...    public function textDump($num = 0): string

260

Chapter 11 ■ performing and representing tasks

    {        $txtout = parent::textDump($num);        foreach ($this->units as $unit) {            $txtout .= $unit->textDump($num + 1);        }

        return $txtout;    }}

I could go on to create methods for counting the number of units in the tree, for saving components to a 

database, and for calculating the food units consumed by an army.

Why would I want to include these methods in the composite’s interface? There is only one really 

compelling answer. I include these disparate operations here because this is where an operation can gain easy access to related nodes in the composite structure.

Although it is true that ease of traversal is part of the Composite pattern, it does not follow that every 

operation that needs to traverse the tree should therefore claim a place in the Composite’s interface.

So these are the forces at work: I want to take full advantage of the easy traversal afforded by my object 

structure, but I want to do this without bloating the interface.

ImplementationI’ll begin with the interfaces. In the abstract Unit class, I define an accept() method:

// listing 11.39

abstract class Unit{    // ...    public function accept(ArmyVisitor $visitor)    {        $refthis = new \ReflectionClass(get_class($this));        $method = "visit".$refthis->getShortName();        $visitor->$method($this);    }

    protected function setDepth($depth)    {        $this->depth=$depth;    }

    public function getDepth()    {        return $this->depth;    }}

As you can see, the accept() method expects an ArmyVisitor object to be passed to it. PHP allows 

you dynamically to define the method on the ArmyVisitor you wish to call, so I construct a method name based on the name of the current class and invoke that method on the provided ArmyVisitor object. If the current class is Army, then I invoke ArmyVisitor::visitArmy(). If the current class is TroopCarrier, then 

261

Chapter 11 ■ performing and representing tasks

I invoke ArmyVisitor::visitTroopCarrier(). And so on. This saves me from implementing accept() on every leaf node in my class hierarchy. While I was in the area, I also added two methods of convenience: getDepth() and setDepth(). These can be used to store and retrieve the depth of a unit in a tree. setDepth() is invoked by the unit’s parent when it adds it to the tree from CompositeUnit::addUnit():

// listing 11.40

abstract class CompositeUnit extends Unit{    // ...

    public function addUnit(Unit $unit)    {        foreach ($this->units as $thisunit) {            if ($unit === $thisunit) {                return;            }        }

        $unit->setDepth($this->depth+1);        $this->units[] = $unit;    }

    public function accept(ArmyVisitor $visitor)    {        parent::accept($visitor);

        foreach ($this->units as $thisunit) {            $thisunit->accept($visitor);        }    }}

I included an accept() method in this fragment. This calls Unit::accept() to invoke the relevant vist() 

method on the provided ArmyVisitor object. Then it loops through any child objects calling accept(). In fact, because accept() overrides its parent operation, the accept() method allows me to do two things:

•	•	

Invoke the correct visitor method for the current component

Pass the visitor object to all the current element children via the accept() method (assuming the current component is composite)

I have yet to define the interface for ArmyVisitor. The accept() methods should give you some clue. The visitor class will define accept() methods for each of the concrete classes in the class hierarchy. This allows me to provide different functionality for different objects. In my version of this class, I also define a default visit() method that is automatically called if implementing classes choose not to provide specific handling for particular Unit classes:

// listing 11.41

abstract class ArmyVisitor{    abstract public function visit(Unit $node);

262

Chapter 11 ■ performing and representing tasks

    public function visitArcher(Archer $node)    {        $this->visit($node);    }

    public function visitCavalry(Cavalry $node)    {        $this->visit($node);    }

    public function visitLaserCanonUnit(LaserCanonUnit $node)    {        $this->visit($node);    }

    public function visitTroopCarrierUnit(TroopCarrierUnit $node)    {        $this->visit($node);    }

    public function visitArmy(Army $node)    {        $this->visit($node);    }}

So now it’s just a matter of providing implementations of ArmyVisitor, and I am ready to go. Here is the 

simple text dump code reimplemented as an ArmyVisitor object:

// listing 11.42

class TextDumpArmyVisitor extends ArmyVisitor{    private $text = "";

    public function visit(Unit $node)    {        $txt = "";        $pad = 4*$node->getDepth();        $txt .= sprintf("%{$pad}s", "");        $txt .= get_class($node).": ";        $txt .= "bombard: ".$node->bombardStrength()."\n";        $this->text .= $txt;    }

    public function getText()    {        return $this->text;    }}

263

Chapter 11 ■ performing and representing tasks

Let’s look at some client code, and then walk through the whole process:

// listing 11.43$main_army = new Army();$main_army->addUnit(new Archer());$main_army->addUnit(new LaserCanonUnit());$main_army->addUnit(new Cavalry());

$textdump = new TextDumpArmyVisitor();$main_army->accept($textdump);print $textdump->getText();

This code yields the following output:

Tax levied for popp\ch11\batch08\Army: 1Tax levied for popp\ch11\batch08\Archer: 2Tax levied for popp\ch11\batch08\LaserCanonUnit: 1Tax levied for popp\ch11\batch08\Cavalry: 3TOTAL: 7

I create an Army object. Because Army is composite, it has an addUnit() method, and I use this to add some 

more Unit objects. I then create the TextDumpArmyVisitor object, which I pass to Army::accept(). The accept() method constructs a method call and invokes TextDumpArmyVisitor::visitArmy(). In this case, I have provided no special handling for Army objects, so the call is passed on to the generic visit() method. visit() has been passed a reference to the Army object. It invokes its methods (including the newly added getDepth(), which tells anyone who needs to know how far down the object hierarchy the unit is) in order to generate summary data. The call to visitArmy() is complete, so the Army::accept() operation now calls accept() on its children in turn, passing the visitor along. In this way, the ArmyVisitor class visits every object in the tree.

With the addition of just a couple of methods, I have created a mechanism by which new functionality 

can be plugged into my composite classes without compromising their interface and without lots of duplicated traversal code.

On certain squares in the game, armies are subject to a tax. The tax collector visits the army and levies a fee for each unit it finds. Different units are taxable at different rates. Here’s where I can take advantage of the specialized methods in the visitor class:

// listing 11.44

class TaxCollectionVisitor extends ArmyVisitor{    private $due = 0;    private $report = "";

    public function visit(Unit $node)    {        $this->levy($node, 1);    }

    public function visitArcher(Archer $node)    {        $this->levy($node, 2);    }

264

Chapter 11 ■ performing and representing tasks

    public function visitCavalry(Cavalry $node)    {        $this->levy($node, 3);    }

    public function visitTroopCarrierUnit(TroopCarrierUnit $node)    {        $this->levy($node, 5);    }

    private function levy(Unit $unit, int $amount)    {        $this->report .= "Tax levied for " . get_class($unit);        $this->report .= ": $amount\n";        $this->due += $amount;    }

    public function getReport()    {        return $this->report;    }

    public function getTax()    {        return $this->due;    }}

In this simple example, I make no direct use of the Unit objects passed to the various visit methods. I 

do, however, use the specialized nature of these methods, levying different fees according to the specific type of the invoking Unit object.

Here’s some client code:

// listing 11.45

$main_army = new Army();$main_army->addUnit(new Archer());$main_army->addUnit(new LaserCanonUnit());$main_army->addUnit(new Cavalry());

$taxcollector = new TaxCollectionVisitor();$main_army->accept($taxcollector);print $taxcollector->getReport();print "TOTAL: ";print $taxcollector->getTax() . "\n";

The TaxCollectionVisitor object is passed to the Army object’s accept() method, as before. Once 

again, Army passes a reference to itself to the visitArmy() method, before calling accept() on its children. The components are blissfully unaware of the operations performed by their visitor. They simply collaborate with its public interface, each one passing itself dutifully to the correct method for its type.

265

Chapter 11 ■ performing and representing tasks

In addition to the methods defined in the ArmyVisitor class, TaxCollectionVisitor provides two 

summary methods, getReport() and getTax(). Invoking these provides the data you might expect:

Tax levied for popp\ch11\batch08\Army: 1Tax levied for popp\ch11\batch08\Archer: 2Tax levied for popp\ch11\batch08\LaserCanonUnit: 1Tax levied for popp\ch11\batch08\Cavalry: 3TOTAL: 7

Figure 11-7 shows the participants in this example.

Figure 11-7.  The Visitor pattern

Visitor IssuesThe Visitor pattern, then, is another pattern that combines simplicity and power. There are a few things to bear in mind when deploying this pattern, however.

First, although it is perfectly suited to the Composite pattern, Visitor can, in fact, be used with any collection of objects. So, you might use it with a list of objects where each object stores a reference to its siblings, for example.

By externalizing operations, you may risk compromising encapsulation. That is, you may need to expose 

the guts of your visited objects in order to let visitors do anything useful with them. You saw, for example, that for the first Visitor example, I was forced to provide an additional method in the Unit interface in order to provide information for TextDumpArmyVisitor objects. You also saw this dilemma previously in the Observer pattern.

Because iteration is separated from the operations that visitor objects perform, you must relinquish a 

degree of control. For example, you cannot easily create a visit() method that does something both before and after child nodes are iterated. One way around this would be to move responsibility for iteration into the visitor objects. The trouble with this is that you may end up duplicating the traversal code from visitor to visitor.

By default, I prefer to keep traversal internal to the visited classes, but externalizing it provides you with one distinct advantage. You can vary the way that you work through the visited classes on a visitor-by-visitor basis.

266

Chapter 11 ■ performing and representing tasks

The Command Pattern

In recent years, I have rarely completed a web project without deploying this pattern. Originally conceived in the context of graphical user interface design, command objects make for good enterprise application design, encouraging a separation between the controller (request and dispatch handling) and domain model (application logic) tiers. Put more simply, the Command pattern makes for systems that are well organized and easy to extend.

The ProblemAll systems must make decisions about what to do in response to a user’s request. In PHP, that decision-making process is often handled by a spread of point-of-contact pages. In selecting a page (feedback.php),  the user clearly signals the functionality and interface she requires. Increasingly, PHP developers are opting for a single-point-of-contact approach (as I will discuss in the next chapter). In either case, however, the receiver of a request must delegate to a tier more concerned with application logic. This delegation is particularly important in cases where the user can make requests to different pages. Without it, duplication inevitably creeps into the project.

So, imagine you have a project with a range of tasks that need performing. In particular, the system 

must allow some users to log in and others to submit feedback. You could create login.php and feedback.php pages that handle these tasks, instantiating specialist classes to get the job done. Unfortunately, user interface in a system rarely maps neatly to the tasks that the system is designed to complete. You may require login and feedback capabilities on every page, for example. If pages must handle many different tasks, then perhaps you should think of tasks as things that can be encapsulated. In doing this, you make it easy to add new tasks to your system, and you build a boundary between your system’s tiers. This brings us to the Command pattern.

ImplementationThe interface for a command object could not get much simpler. It requires a single method: execute().In Figure 11-8, I have represented Command as an abstract class. At this level of simplicity, it could be defined instead as an interface. I tend to use abstracts for this purpose because I often find that the base class can also provide useful common functionality for its derived objects.

Figure 11-8.  The Command class

There are up to three other participants in the Command pattern: the client, which instantiates the 

command object; the invoker, which deploys the object; and the receiver on which the command operates.The receiver can be given to the command in its constructor by the client, or it can be acquired from a factory object of some kind. I like the latter approach, keeping the constructor method clear of arguments. All Command objects can then be instantiated in exactly the same way.

Here’s the abstract base class:

// listing 11.46

abstract class Command

267

Chapter 11 ■ performing and representing tasks

{    abstract public function execute(CommandContext $context): bool;}

And here’s a concrete Command class:

// listing 11.47

class LoginCommand extends Command{    public function execute(CommandContext $context): bool    {        $manager = Registry::getAccessManager();        $user = $context->get('username');        $pass = $context->get('pass');        $user_obj = $manager->login($user, $pass);

        if (is_null($user_obj)) {            $context->setError($manager->getError());            return false;        }

        $context->addParam("user", $user_obj);

        return true;    }}

The LoginCommand is designed to work with an AccessManager object. AccessManager is an imaginary class that handles the nuts-and-bolts of logging users into the system. Notice that the Command::execute() method demands a CommandContext object—this is known as RequestHelper in Core J2EE Patterns: Best Practices and Design Strategies (Prentice Hall, 2001) by Alur et al. This is a mechanism by which request data can be passed to Command objects, and by which responses can be channeled back to the view layer. Using an object in this way is useful because I can pass different parameters to commands without breaking the interface. The CommandContext is essentially an object wrapper around an associative array variable, though it is frequently extended to perform additional helpful tasks. Here is a simple CommandContext implementation:

// listing 11.48

class CommandContext{    private $params = [];    private $error = "";

    public function __construct()    {        $this->params = $_REQUEST;    }

268

Chapter 11 ■ performing and representing tasks

    public function addParam(string $key, $val)    {        $this->params[$key] = $val;    }

    public function get(string $key): string    {        if (isset($this->params[$key])) {            return $this->params[$key];        }        return null;    }

    public function setError($error): string    {        $this->error = $error;    }

    public function getError(): string    {        return $this->error;    }}

So, armed with a CommandContext object, the LoginCommand can access request data: the submitted 

username and password. I use Registry, a simple class with static methods for generating common objects, to return the AccessManager object with which LoginCommand needs to work. If AccessManager reports an error, the command lodges the error message with the CommandContext object for use by the presentation layer, and returns false. If all is well, LoginCommand simply returns true. Note that Command objects do not themselves perform much logic. They check input, handle error conditions, and cache data, as well as calling on other objects to perform operations. If you find that application logic creeps into your command classes, it is often a sign that you should consider refactoring. Such code invites duplication, as it is inevitably copied and pasted between commands. You should at least look at where such functionality belongs. It may be best moved down into your business objects, or possibly into a Facade layer. In my example, I am still missing the client, the class that generates command objects, and the invoker, the class that works with the generated command. The easiest way of selecting which command to instantiate in a web project is by using a parameter in the request itself. Here is a simplified client:

// listing 11.49

class CommandFactory{    private static $dir = 'commands';

    public static function getCommand(string $action = 'Default'): Command    {        if (preg_match('/\W/', $action)) {            throw new Exception("illegal characters in action");        }

        $class = __NAMESPACE__ . "\\commands\\" . UCFirst(strtolower($action)) . "Command";

269

Chapter 11 ■ performing and representing tasks

        if (! class_exists($class)) {            throw new CommandNotFoundException("no '$class' class located");        }

        $cmd = new $class();

        return $cmd;    }}

The CommandFactory class simply looks for a particular class. A fully qualified class name is constructed 

using the CommandFactory class’s own namespace, the string '\commands\', and the CommandContext object’s $action parameter. The last item should have been passed to the system from the request. Thanks to Composer’s autoload magic, we don’t need to worry about explicitly requiring a class. If the class exists, then an object is instantiated and returned to the caller. I could add more error checking here, ensuring that the found class belongs to the Command family, and that the constructor expects no arguments; however, this version will do fine for my purposes. The strength of this approach is that you can create a discoverable Command object with the correct namespace at any time, and the system will immediately support it.

The invoker is now simplicity itself:

// listing 11.50

class Controller{    private $context;

    public function __construct()    {        $this->context = new CommandContext();    }

    public function getContext(): CommandContext    {        return $this->context;    }

    public function process()    {        $action = $this->context->get('action');        $action = ( is_null($action) ) ? "default" : $action;        $cmd = CommandFactory::getCommand($action);

        if (! $cmd->execute($this->context)) {            // handle failure        } else {            // success            // dispatch view        }    }}

270

Chapter 11 ■ performing and representing tasks

Here is some code to invoke the class:

// listing 11.51

$controller = new Controller();$context = $controller->getContext();

$context->addParam('action', 'login' );$context->addParam('username', 'bob' );$context->addParam('pass', 'tiddles' );$controller->process();

print $context->getError();

Before I call Controller::process(), I fake a web request by setting parameters on the CommandContext 

object instantiated in the controller’s constructor. The process() method acquires the "action" parameter (falling back to the string "default" if no action parameter is present). The method then delegates object instantiation to the CommandFactory object. It invokes execute() on the returned command. Notice how the controller has no idea about the command’s internals. It is this independence from the details of command execution that makes it possible for you to add new Command classes with a relatively small impact on this framework.

Here’s one more Command class:

// listing 11.52

class FeedbackCommand extends Command{    public function execute(CommandContext $context): bool    {        $msgSystem = Registry::getMessageSystem();        $email = $context->get('email');        $msg   = $context->get('msg');        $topic = $context->get('topic');        $result = $msgSystem->send($email, $msg, $topic);

        if (! $result) {            $context->setError($msgSystem->getError());            return false;        }

        return true;    }}

 i will return to the Command pattern in Chapter 12, with a fuller implementation of a Command factory 

 ■ Note class. the framework for running commands presented here is a simplified version of another pattern that you will encounter: the front Controller.

271

Chapter 11 ■ performing and representing tasks

This class will be run in response to a "feedback" action string, without the need for any changes in the 

controller or CommandFactory classes.

Figure 11-9 shows the participants of the Command pattern.

Figure 11-9.  Command pattern participants

The Null Object Pattern

Half the problems that programmers face seem to be related to type. That’s one reason PHP has increasingly supported type checks for method declarations and returns. If dealing with a variable that contains the wrong type is a problem, dealing with one that contains no type at all is at least as bad. This happens all the time, since so many functions return null when they fail to generate a useful value. You can avoid inflicting this issue on yourself and others by using the Null Object pattern in your projects. As you will see, while the other patterns in this chapter try to get stuff done, Null Object is designed to do nothing as gracefully as possible.

The ProblemIf your method has been charged with the task of finding an object, sometimes there is little to be done but to admit defeat. The information provided by the calling code may be stale or a resource may be unavailable. If 

272

Chapter 11 ■ performing and representing tasks

the failure is catastrophic, you might choose to throw an exception. Often, though, you’ll want to be a little more forgiving. In such a case, returning a null value might seem like a good way of signaling failure to the client.The problem here is that your method is breaking its contract. If it has committed to return an object 

with a certain method, then returning null forces the client code to adjust to unexpected circumstances.

Let’s return once again to our game. And let’s say that a class named TileForces keeps track of 

information about units on a particular tile. Our game maintains local saved information about the units in the system, and a component named UnitAcquisition is responsible for turning this metadata into an array of objects.

Here is the TileForces constructor:

// listing 11.53

class TileForces{    private $units = [];    private $x;    private $y;

    function __construct(int $x, int $y, UnitAcquisition $acq)    {        $this->x = $x;        $this->y = $x;        $this->units = $acq->getUnits($this->x, $this->y);    }    // ...}

The TileForces object does little but delegate to the provided UnitAcquisition object to get an array of 

Unit objects. Let’s build a fake UnitAcquisition object:

// listing 11.54

class UnitAcquisition{    function getUnits(int $x, int $y): array    {        // 1. looks up x and y in local data and gets a list of unit ids        // 2. goes off to a data source and gets full unit data        // here's some fake data        $army = new Army();        $army->addUnit(new Archer());        $found = [            new Cavalry(),            null,            new LaserCanonUnit(),            $army        ];

        return $found;    }}

273

Chapter 11 ■ performing and representing tasks

In this class, I hide the process of getting Unit data. Of course, in a real system, some actual look up would be performed here. I have contented myself with a few direct instantiations. Notice, though, that I embedded a sneaky null value in the $found array. This might happen, for example, if our network game client holds metadata that has fallen out of alignment with the state of data on a server.Armed with its array of Unit objects, TileForces can provide some functionality:

// listing 11.55

    // TileForces    public function firepower(): int    {        $power = 0;

        foreach($this->units as $unit) {            $power += $unit->bombardStrength();        }

        return $power;    }

Let’s put the code through its paces:

// listing 11.56

$acquirer = new UnitAcquisition();$tileforces = new TileForces(4, 2, $acquirer);$power = $tileforces->firepower();print "power is {$power}\n";

Thanks to that lurking null, this code causes an error:

Error: Call to a member function bombardStrength() on null

TileForces::firepower() cycles through its $units array, calling bombardStrength() on each Unit. 

The attempt to invoke a method on a null value, of course, causes an error.

The most obvious solution is to check each element of the array before working with it:

// listing 11.57

    // TileForces    public function firepower(): int    {        $power = 0;

        foreach ($this->units as $unit) {            if (! is_null($unit)) {                $power += $unit->bombardStrength();            }        }

        return $power;    }

274

Chapter 11 ■ performing and representing tasks

On its own, this isn’t too much of a problem. But imagine a version of TileForces that performs all sorts 

of operations on the elements in its $units property. As soon as we begin to replicate the is_null() check in multiple places, we are presented once again with a particular code smell. Often, the answer to parallel chunks of client code is to replace multiple conditionals with polymorphism. We can do that here, too.

ImplementationThe Null Object pattern allows us to delegate the doing of nothing to a class of an expected type. In this case, I will create a NullUnit class.

// listing 11.58

class NullUnit extends Unit{    public function bombardStrength(): int    {        return 0;    }

    public function getHealth(): int    {        return 0;    }

    public function getDepth(): int {        return 0;    }}

This implementation of Unit respects the interface, but does precisely nothing. Now, I can amend 

UnitAcquisition to create a NullUnit rather than use a null:

// listing 11.59

    public function getUnits(int $x, int $y): array    {        $army = new Army();        $army->addUnit(new Archer());

        $found = [            new Cavalry(),            new NullUnit(),            new LaserCanonUnit(),            $army        ];

    return $found;    }

275

Chapter 11 ■ performing and representing tasks

The client code in TileForces can call any methods it likes on a NullUnit object without problem or 

error:

// listing 11.60

    // TileForces    public function firepower(): int {        $power = 0;

        foreach($this->units as $unit) {            $power += $unit->bombardStrength();        }

        return $power;    }

Take a look at any substantial project and count up the number of inelegant checks that have been 

forced on its coders by methods that return null values. How many of those checks could be dispensed with if more of us used Null Object?

Of course, sometimes you will need to know that you are dealing with a null object. The most obvious way of doing this would be to test an object with the instanceof operator. That is even less elegant than the original is_null() call, however.

Perhaps the neatest solution is to add an isNull() method to both a base class (returning false) and to 

the Null Object (returning true):

// listing 11.61

if (! $unit->isNull()) {    // do something} else {    print "null - no action\n";}

That gives us the best of both worlds. Any method of a NullUnit object can be safely called. And any 

Unit object can be queried for null status.

Summary

In this chapter, I wrapped up my examination of the Gang of Four patterns, placing a strong emphasis on how to get things done. I began by showing you how to design a mini-language and build its engine with the Interpreter pattern.

In the Strategy pattern, you encountered another way of using composition to increase flexibility 

and reduce the need for repetitive subclassing. And with the Observer pattern, you learned how to solve the problem of notifying disparate and varying components about system events. You also revisited the Composite example; and with the Visitor pattern, learned how to pay a call on, and apply many operations to, every component in a tree. You even saw how the Command pattern can help you to build an extensible tiered system. Finally, you saved yourself a heap of checking for nulls with the Null Object pattern.

In the next chapter, I will step further beyond the Gang of Four to examine some patterns specifically 

oriented toward enterprise programming.

276

CHAPTER 12

