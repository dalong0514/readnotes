# 0204. Patterns for Flexible Object Programming

With strategies for generating objects covered, we’re free now to look at some strategies for structuring classes and objects. I will focus in particular on the principle that composition provides greater flexibility than inheritance. The patterns I examine in this chapter are once again drawn from the Gang of Four catalog.

This chapter will cover a trio of patterns: 1) The Composite pattern: Composing structures in which groups of objects can be used as if they were individual objects. 2) The Decorator pattern: A flexible mechanism for combining objects at runtime to extend functionality. 3) The Facade pattern: Creating a simple interface to complex or variable systems.

## 4.1 Structuring Classes to Allow Flexible Objects

Way back in Chapter 4, I said that beginners often confuse objects and classes. This was only half true. In fact, most of the rest of us occasionally scratch our heads over UML class diagrams, attempting to reconcile the static inheritance structures they show with the dynamic object relationships their objects will enter into off the page.

Remember the pattern principle,「Favor composition over inheritance」? This principle distills this tension between the organization of classes and objects. In order to build flexibility into our projects, we structure our classes so that their objects can be composed into useful structures at runtime.

This is a common theme running through the first two patterns of this chapter. Inheritance is an important feature in both, but part of its importance lies in providing the mechanism by which composition can be used to represent structures and extend functionality.

在第 4 章中，我曾说过初学者常常对对象和类感到困惑。这也不全对。事实上，即使不是初学者，有时也会大伤脑筋，比如我们会尝试让 UML 类图中描述的静态继承结构与这些类的动态对象的关系保持一致，有时这个目标并不容易实现。你还记得「组合优于继承」这个模式原则吗？该原则体现了类和对象之间的组织弹性。为了使项目更具灵活性，我们需要将类按一定结构组织起来，以便它们的对象在代码运行时能被构建为有用的结构。这是本章前两个模式的共同主题。继承在这两个模式中很重要，但是组合所提供的描述结构及扩展功能的机制也很重要。

1『将类按一定的结构组织起来，便于它们的对象在运行时被构建成有用的结构。这个信息直觉上很重要，目前没吃透。（2020-09-04）』

## 4.2 The Composite Pattern

The Composite pattern is perhaps the most extreme example of inheritance deployed in the service of composition. It is a simple and yet breathtakingly elegant design. It is also fantastically useful. Be warned, though; it is so neat, you might be tempted to overuse this strategy.

The Composite pattern is a simple way of aggregating and then managing groups of similar objects so that an individual object is indistinguishable to a client from a collection of objects. The pattern is, in fact, very simple, but it is also often confusing. One reason for this is the similarity in structure of the classes in the pattern to the organization of its objects. Inheritance hierarchies are trees, beginning with the super class at the root, and branching out into specialized subclasses. The inheritance tree of classes laid down by the Composite pattern is designed to allow the easy generation and traversal of a tree of objects.

组合模式也许是将继承用于组合对象的最极端的例子。组合模式的设计思想简单而又非常优雅，并且非常实用。但要注意的是，因为这个模式很好用，你也许会经不起诱惑而过度使用它。组合模式可以很好地聚合和管理许多相似的对象，因而对客户端代码来说，一个独立对象和一个对象集合是没有差别的。虽然该模式实际上非常简单，但还是经常令人感到迷惑。其中一个原因就是模式中类的结构和对象的组织结构非常相似。组合模式中继承的层级结构是树型结构，由根部的基类开始，分支到各个不同的子类，在其继承树中可以轻松地生成枝叶，也可以很容易地遍历整个对象树中的对象。

If you are not already familiar with this pattern, you have every right to feel confused at this point. Let’s try an analogy to illustrate the way that single entities can be treated in the same way as collections of things. Given broadly irreducible ingredients such as cereals and meat (or soya if you prefer), we can make a food product—a sausage, for example. We then act on the result as a single entity. Just as we eat, cook, buy, or sell meat, we can eat, cook, buy, or sell the sausage that the meat in part composes. We might take the sausage and combine it with the other composite ingredients to make a pie, thereby rolling a composite into a larger composite. We behave in the same way to the collection as we do to the parts. The Composite pattern helps us to model this relationship between collections and components in our code.

如果你以前不熟悉这个模式，也许会感到有些困惑。让我们举例说明，单个物体有时可以被当成一个集合来看待。例如，用谷类和肉类（或者是你更加喜欢的大豆）可以制作一种食物香肠。然后我们将香肠当做单个物体来处理。就像我们可以食用、烹调、购买或者出售肉类一样，我们也可以食用、烹调、购买或者出售由肉类组成的香肠。我们也许会用香肠和其他组合成分来制作馅饼，从而将一个组合物合成一个更大的组合物。在这个例子中，我们处理组件的方式和处理集合的方式是一样的。组合模式有助于我们为集合和组件之间的关系建立模型。

1『

很佩服作者以及译者的表述能力，上面的这段信息算是把「组合模式」弄清楚了，再结合「王铮的设计模式专栏」里提到的，四人帮的原话：

Compose objects into tree structure to represent part-whole hierarchies. Composite lets client treat individual objects and compositions of objects uniformly.

将一组对象组织（Compose）成树形结构，以表示一种「部分 - 整体」的层次结构。组合让客户端（代指代码的使用者）可以统一单个对象和组合对象的处理逻辑。

』

### 4.2.1 The Problem

Managing groups of objects can be quite a complex task, especially if the objects in question might also contain objects of their own. This kind of problem is very common in coding. Think of invoices, with line items that summarize additional products or services, or things-to-do lists with items that themselves contain multiple subtasks. In content management, we can’t move for trees of sections, pages, articles, or media components. Managing these structures from the outside can quickly become daunting.

Let’s return to a previous scenario. I am designing a system based on a game called Civilization. A player can move units around hundreds of tiles that make up a map. Individual counters can be grouped together to move, fight, and defend themselves as a unit. Here I define a couple of unit types:

管理一组对象是很复杂的，当对象中可能还包含着它们自己的对象时尤其如此。这类问题在开发中非常常见。比如发票中会包含描述产品或服务的条目，或者待办事宜列表会包含多个子任务。在 CMS（Content Management System，内容管理系统）中，我们无法离开页面、文章、多媒体组件等。从外部来管理这些结构相当困难。让我们回到之前虚构的一个场景，我们以一个叫做「文明」的游戏为基础设计一个系统。玩家可以在一个由大量区块所组成的地图上移动战斗单元。独立的单元可被组合起来一起移动、战斗和防守。我们先定义一些战斗单元的类型。

```php
// listing 10.01

abstract class Unit {    
    abstract public function bombardStrength(): int;
}

class Archer extends Unit {
    public function bombardStrength(): int {        
        return 4;    
    }
}

class LaserCannonUnit extends Unit {    
    public function bombardStrength(): int {        
        return 44;    
    }
}
```

The Unit class defines an abstract bombardStrength() method, which sets the attack strength of a unit bombarding an adjacent tile. I implement this in both the Archer and LaserCannonUnit classes. These classes would also contain information about movement and defensive capabilities, but I’ll keep things simple. I could define a separate class to group units together, like this:

```php
// listing 10.02

class Army {    
    private $units = [];

    public function addUnit(Unit $unit)    {        
        array_push($this->units, $unit);    
    }

    public function bombardStrength(): int    {        
    $ret = 0;        
    foreach ($this->units as $unit) {            
        $ret += $unit->bombardStrength();        
    }        
    return $ret;    
    }
}

// listing 10.03

$unit1 = new Archer();
$unit2 = new LaserCannonUnit();
$army = new Army();
$army->addUnit($unit1);
$army->addUnit($unit2);
print $army->bombardStrength();
```

The Army class has an addUnit() method that accepts a Unit object. Unit objects are stored in an array property called \$units. I calculate the combined strength of my army in the bombardStrength() method. This simply iterates through the aggregated Unit objects, calling the bombardStrength() method of  each one.

This model is perfectly acceptable, as long as the problem remains as simple as this. What happens, though, if I were to add some new requirements? Let’s say that an army should be able to combine with other armies. Each army should retain its own identity so that it can disentangle itself from the whole at a later date. The Arch Duke’s brave forces might share common cause today with General Soames’s assault upon the exposed flank of the enemy, but a domestic rebellion may send his army scurrying home at any time. For this reason, I can’t just decant the units from each army into a new force.

如果问题一直如此简单，那么这样的模型还是非常令人满意的。但是当我们加入一些新的需求，会发生什么呢？比如军队应该可以与其他军队进行合并。同时，每个军队都会有它自己的 ID，这样军队以后还能从整编中解散出来。比如今天大公爵（Archduke）和 Soames 将军的勇士们可能一起并肩作战，但是当国内发生叛乱时，公爵可能会在任何时候将它的军队调回。因此，我们不能仅支持将军队与军队合并，还要能够在必要的时候再把原来的军队抽离出来。我们可以修改 Army 类，使之可以像添加 Unit 对象一样添加 Army 对象

I could amend the Army class to accept Army objects as well as Unit objects:

```php
// listing 10.04

public function addArmy(Army $army) {        
    array_push($this->armies, $army);    
}
```

Then I’d need to amend the bombardStrength() method to iterate through all armies as well as units:

```php
// listing 10.05   

 public function bombardStrength(): int {        
    $ret = 0;        
    foreach ($this->units as $unit) {            
        $ret += $unit->bombardStrength();        
    }        
    foreach ($this->armies as $army) {            
        $ret += $army->bombardStrength();        
    }        
    return $ret;    
 }
```

This additional complexity is not too problematic at the moment. Remember, though, I would need to do something similar in methods like defensiveStrength(), movementRange(), and so on. My game is going to be richly featured. Already the business group is calling for troop carriers that can hold up to ten units to improve their movement range on certain terrains. Clearly, a troop carrier is similar to an army in that it groups units. It also has its own characteristics. I could further amend the Army class to handle TroopCarrier objects, but I know that there will be a need for still more unit groupings. It is clear that I need a more flexible model.

Let’s look again at the model I have been building. All the classes I created shared the need for a bombardStrength() method. In effect, a client does not need to distinguish between an army, a unit, or a troop carrier. They are functionally identical. They need to move, attack, and defend. Those objects that contain others need to provide methods for adding and removing them. These similarities lead us to an inevitable conclusion. Because container objects share an interface with the objects that they contain, they are naturally suited to share a type family.

此时，这个新的需求（即添加和抽取军队）还不算太复杂。但是记住，我们还需要对 defensiveStrength()、movementRange() 等方法做相似的修改。慢慢地，我们的游戏会变得越来越完善。现在客户提出了新要求：运兵船可以支持最多 10 个战斗单元以改进它们在某些地形上的活动范围。显然，运兵船与用于组合战斗单元的 Army 对象相似，但它也有一些自己的特性。虽然我们能够通过改进 Army 类来处理 TroopCarrier 对象，但是我们知道以后可能会有更多对部队进行组合的需求。显然，我们需要一个更灵活的模型。

让我们再回顾一下已经建立的这个模型。所有已创建的类都需要 bombardStrength() 方法。实际上，客户端代码并不需要去区分对象是 army、unit 还是 troop carrier 类型。就功能上说，它们都是相同的：它们都要移动、攻击和防御。这些包含其他对象的对象需要提供添加和移除其他对象的方法。这些相似性会给我们带来一个必然的结论：因为容器对象与它们包含的对象共享同一个接口，所以它们应该共享同一个类型家族。

### 4.2.2 Implementation

The Composite pattern defines a single inheritance hierarchy that lays down two distinct sets of responsibilities. We have already seen both of these in our example. Classes in the pattern must support a common set of operations as their primary responsibility. For us, that means the bombardStrength() method. Classes must also support methods for adding and removing child objects.

组合模式定义了一个单根继承体系，使具有截然不同职责的集合可以并肩工作。在之前的例子中我们已看到以上两点。组合模式中的类必须支持一个共同的操作集，以将其作为它们的首要职责。对我们来说，bombardStrength() 方法便支持这样的操作。类同时必须拥有添加和删除子对象的方法。

Figure 10-1 shows a class diagram that illustrates the Composite pattern as applied to our problem.

As you can see, all the units in this model extend the Unit class. A client can be sure, then, that any Unit object will support the bombardStrength() method. So, an Army can be treated in exactly the same way as an Archer.

The Army and TroopCarrier classes are composites: they are designed to hold Unit objects. The Archer and LaserCannon classes are leaves, designed to support unit operations, but not to hold other Unit objects. There is actually an issue as to whether leaves should honor the same interface as composites, as they do in Figure 10-1. The diagram shows TroopCarrier and Army aggregating other units, even though the leaf classes are also bound to implement addUnit(). I will return to this question shortly. Here is the abstract Unit class:

可以看到，模型中的所有部队单位都扩展自 Unit 类。然后，客户端代码可以肯定任何 unit 对象都支持 bombardStrength() 方法，因此完全可以像处理 Archer 对象那样处理 Army 对象。Army 和 TroopCarrier 类都被设计为组合对象，用于包含 Unit 对象。Archer 和 LaserCannon 类则是局部对象 1，具有部队单位的操作功能，但不能包含其他 Unit 对象。这里有个问题，就是局部对象是否需要遵循与图 10-1 所示的组合对象同样的接口。图 10-1 中的 TroopCarrier 和 Army 实现了与其他作战单元的组合，而即使在局部类中，也实现了 addUnit() 方法。我们稍后将讨论这个问题。

1 也称为树叶对象。称为树叶是因为组合模式为树型结构，组合对象为枝干，单独存在的对象为树叶。树叶对象应该是最小单位，其中不能包含其他对象。一一译者注

1『悟了悟了，在组合模式里，「组合对象」是树干，单独存在的对象（叶子对象）是树叶，叶子对象是不能再包含其他对象的。（2020-09-10）』

```php
// listing 10.06

abstract class Unit {    
    abstract public function addUnit(Unit $unit);    
    abstract public function removeUnit(Unit $unit);    
    abstract public function bombardStrength(): int;
}
```

As you can see, I lay down the basic functionality for all Unit objects here. Now, let’s see how a composite object might implement these abstract methods:

```php
// listing 10.07

class Army extends Unit {    
    private $units = [];

    public function addUnit(Unit $unit) {        
        if (in_array($unit, $this->units, true)) {            
            return;        
        }
        $this->units[] = $unit;    
    }

    public function removeUnit(Unit $unit) {        
        $idx = array_search($unit, $this->units, true);        
        if (is_int($idx)) {            
            array_splice($this->units, $idx, 1, []);        
        }    
    }

    public function bombardStrength(): int {        
        $ret = 0;        
        foreach ($this->units as $unit) {            
            $ret += $unit->bombardStrength();        
        }        
        return $ret;    
    }
}
```

1『上面几个数组操作的函数值得借鉴，意外收获，哈哈。而且老版书中 removeUnit() 里是通过匿名函数实现的，新版的这个实现应该更好，不然作者不会做此更新的。（2020-09-05）回复：1）数组内没有该元素，增加进去。2）删除数组内的某个元素。这两个功能实现可以借鉴到其他地方去。（2020-09-10）』

The addUnit() method checks whether I have already added the same Unit object before storing it in the private \$units array property. removeUnit() uses a similar check to remove a given Unit object from the property.

Army objects, then, can store Units of any kind, including other Army objects, or leaves such as Archer or LaserCannonUnit. Because all units are guaranteed to support bombardStrength(), our Army::bombardStrength() method simply iterates through all the child Unit objects stored in the \$units property, calling the same method on each.

1『这里闻到了「多态」的味道，鸭子理论，因为这些类具有相同的行为 bombardStrength()，所以可以互相替换。（2020-09-10）』

One problematic aspect of the Composite pattern is the implementation of add and remove functionality. The classic pattern places add() and remove() methods in the abstract super class. This ensures that all classes in the pattern share a common interface. As you can see here, though, it also means that leaf classes must provide an implementation:

然后 Army 对象可保存任何类型的 Unit 对象，包括 Army 对象本身或者如 Archer 或 LaserCannonUnit 这样的局部对象。因为所有的部队单位都保证支持 bombardStrength() 方法，所以我们的 Army::bombardStrength() 方法只需遍历 Units 属性，调用每个 Unit 对象的 bombardStrength() 方法，就可以计算出整军队总的攻击强度。组合模式的一个问题是如何实现 add() 和 remove() 方法。一般的组合模式会在抽象超类中添加 add() 和 remove() 方法。这可以确保模式中的所有类都共享同一个接口，但这同时也意味着局部类必须也实现这些方法。

```php
// listing 10.08

class UnitException extends \Exception{}

// listing 10.09

class Archer extends Unit {    
    public function addUnit(Unit $unit) {        
        throw new UnitException(get_class($this) . " is a leaf");    
    }

    public function removeUnit(Unit $unit) {        
        throw new UnitException(get_class($this) . " is a leaf");    
    }

    public function bombardStrength(): int    {       
        return 4;    
    }
}
```

1『这种通过添加「异常」的处理方式，很多地方有看到，值得借鉴。（2020-09-10）』

I do not want to make it possible to add a Unit object to an Archer object, so I throw exceptions if addUnit() or removeUnit() are called. I will need to do this for all leaf objects, so I could perhaps improve my design by replacing the abstract addUnit()/removeUnit() methods in Unit with default implementations like the one in the preceding example:

```php
// listing 10.10

abstract class Unit { 
   
    public function addUnit(Unit $unit) {        
        throw new UnitException(get_class($this) . " is a leaf");    
    }

    public function removeUnit(Unit $unit) {        
        throw new UnitException(get_class($this) . " is a leaf");    
    }

    abstract public function bombardStrength(): int;
}

// listing 10.11

class Archer extends Unit {    
        public function bombardStrength(): int {        
            return 4;    
        }
}
```

This removes duplication in leaf classes, but has the drawback that a composite is not forced at compile time to provide an implementation of addUnit() and removeUnit(), which could cause problems down the line. I will look in more detail at some of the problems presented by the Composite pattern in the next section. Let’s end this section by examining some of its benefits:

这样做可以去除局部类中的重复代码，但是同时组合类不再需要强制性地实现 addUnit() 和  removeUnit() 方法了，这可能会带来问题。在下一节中，我们会深入讨论组合模式所带来的一些问题。现在先让我们回顾一下组合模式所带来的益处。

1. Flexibility: Because everything in the Composite pattern shares a common supertype, it is very easy to add new composite or leaf objects to the design without changing a program’s wider context.

2. Simplicity: A client using a Composite structure has a straightforward interface. There is no need for a client to distinguish between an object that is composed of others and a leaf object (except when adding new components). A call to Army::bombardStrength() may cause a cascade of delegated calls behind the scenes; but to the client, the process and result are exactly equivalent to those associated with calling Archer::bombardStrength().

3. Implicit reach: Objects in the Composite pattern are organized in a tree. Each composite holds references to its children. An operation on a particular part of the tree, therefore, can have a wide effect. We might remove a single Army object from its Army parent and add it to another. This simple act is wrought on one object, but it has the effect of changing the status of the Army object’s referenced Unit objects and of their own children.

4. Explicit reach: Tree structures are easy to traverse. They can be iterated in order to gain information or to perform transformations. We will look at a particularly powerful technique for this in the next chapter when we deal with the Visitor pattern.

1、灵活：因为组合模式中的一切类都共享了同一个父类型，所以可以轻松地在设计中添加新的组合对象或者局部对象，而无需大范围地修改代码。

2、简单：使用组合结构的客户端代码只需设计简单的接口。客户端代码没有必要区分一个对象是组合对象还是局部对象（除了添加新组件时）。客户端代码调用 Army::bombardStrength() 方法时也许会产生一些幕后的委托调用，但是对于客户端代码而言，无论是过程还是效果，都和调用 Army::bombardStrength() 方法是完全相同的。

3、隐式到达：组合模式中的对象通过树型结构组织。每个组合对象中都保存着对子对象的引用。因此对树中某部分的一个小操作可能会产生很大的影响。比如我们可能会将一个父 Army 对象的某个子 Army 对象删除，并将其添加到另外一个父 Army 对象上去。这个简单的动作看似只对子 Army 对象产生作用，但实际上却影响了子 Army 对象中所引用的 unit 对象及其子对象的状态。

4、显式到达：树型结构可轻松遍历。可以通过迭代树型结构来获取组合对象和局部对象的信息，或对组合对象和局部对象执行批量处理。在下一章中，我们在处理访问者模式时会看到一个与此相关的强大技术。

Often, you really see the benefit of a pattern only from the client’s perspective, so here are a couple of armies:

```php
// listing 10.12

// create an army
$main_army = new Army();

// add some units
$main_army->addUnit(new Archer());
$main_army->addUnit(new LaserCannonUnit());

// create a new army
$sub_army = new Army();

// add some units
$sub_army->addUnit(new Archer());
$sub_army->addUnit(new Archer());
$sub_army->addUnit(new Archer());

// add the second army to the first
$main_army->addUnit($sub_army);

// all the calculations handled behind the scenes
print "attacking with strength: {$main_army->bombardStrength()}\n";
```

I create a new Army object and add some primitive Unit objects. I repeat the process for a second Army object that I then add to the first. When I call Unit::bombardStrength() on the first Army object, all the complexity of the structure that I have built up is entirely hidden.

### 4.2.3 Consequences

If you’re anything like me, you would have heard alarm bells ringing when you saw the code extract for the Archer class. Why do we put up with these redundant addUnit() and removeUnit() methods in leaf classes that do not need to support them? An answer of sorts lies in the transparency of the Unit type.

If a client is passed a Unit object, it knows that the addUnit() method will be present. The Composite pattern principle that primitive (leaf) classes have the same interface as composites is upheld. This does not actually help you much because you still do not know how safe you might be calling addUnit() on any Unit object you might come across.

If I move these add/remove methods down so that they are available only to composite classes, then passing a Unit object to a method leaves me with the problem that I do not know by default whether or not it supports addUnit(). Nevertheless, leaving booby-trapped methods lying around in leaf classes makes me uncomfortable. It adds no value and confuses a system’s design because the interface effectively lies about its own functionality.

你也许会像我一样，在看到 Archer 类的代码时就想起了警报——为什么我们要把 addUnit() 和 removeUnit() 这样的冗余方法加到并不需要它们的局部类中？答案在于 Unit 类型的透明性。客户端代码在得到一个 Unit 对象时，知道其中一定包含 addUnit() 方法。组合模式的原则便是局部类和组合类具有同样的接口。不过这未必能真正帮助我们，因为我们仍然不知道调用 Unit 对象的 addUnit() 方法是否安全。如果我们将 add / remove 方法降到下一级对象中，以便这些方法仅在组合类中使用，那么又会产生另一个问题——使用 Unit 对象时，我们并不知道该对象是否默认支持 addUnit() 方法。但是，将冗余的类方法留在局部类中让人感到不舒服。这样做毫无意义而且给系统设计带来歧义，因为接口应该关注于自己独有的功能。

You can split composite classes off into their own CompositeUnit subtype quite easily. First of all, I excise the add/remove behavior from Unit:

```php
// listing 10.13

abstract class Unit {    
    public function getComposite() {        
        return null;    
    }

    abstract public function bombardStrength(): int;
}
```

Notice the new getComposite() method. I will return to this in a little while. Now, I need a new abstract class to hold addUnit() and removeUnit(). I can even provide default implementations:

1『拥有 addUnit() 和 removeUnit() 方法的抽象类，这里指的是 CompositeUnit，即一个「接口」。（2020-09-10）』

注意一下新增的 getComposite() 方法，不过我们稍后再来看这个方法。现在我们需要个新的拥有 addUnit() 和 removeUnit() 方法的抽象类。我们甚至可以给这两个方法加上默认实现：

```php
// listing 10.14

abstract class CompositeUnit extends Unit {    
    private $units = [];

    public function getComposite(): CompositeUnit    {        
        return $this;    
    }

    public function addUnit(Unit $unit) {        
        if (in_array($unit, $this->units, true)) {            
            return;        
        }
        $this->units[] = $unit;    
    }
    
    public function removeUnit(Unit $unit) {        
        $idx = array_search($unit, $this->units, true);        
        if (is_int($idx)) {            
            array_splice($this->units, $idx, 1, []);        
        }    
    }

    public function getUnits(): array {       
        return $this->units;    
    }
}
```

The CompositeUnit class is declared abstract, even though it does not itself declare an abstract method. It does, however, extend Unit, and it does not implement the abstract bombardStrength() method. Army (and any other composite classes) can now extend CompositeUnit. The classes in my example are now organized as in Figure 10-2.

Figure 10-2.  Moving add/remove methods out of the base class

The annoying, useless implementations of add/remove methods in the leaf classes are gone, but the client must still check to see whether it has a CompositeUnit before it can use addUnit().

This is where the getComposite() method comes into its own. By default, this method returns a null value. Only in a CompositeUnit class does it return CompositeUnit. So if a call to this method returns an object, we should be able to call addUnit() on it. Here’s a client that uses this technique:

1『方法 getComposite() 是点睛之笔！（2020-09-10）』

因为 CompositeUnit 类继承自 Unit 类，并没有实现抽象的 bombardStrength() 方法，所以  CompositeUnit 类也被声明为抽象的，虽然它本身并没有抽象方法。Army 类（或任何其他组合类）现在可扩展 CompositeUnit 了，而我们示例中的类现在将以图 10-2 的形式来组织。虽然我们删除了局部类中冗余、烦人的 add / remove 方法，但客户端代码在使用 addUnit() 方法前却仍必须检查对象是否为一个 CompositeUnit 类型的对象。

这就是添加 getComposite() 方法的原因。该方法默认返回一个 null 值，它仅在 CompositeUnit 类中才返回 CompositeUnit 本身。所以如果该方法返回一个对象，那么便可以调用它的  addUnit() 方法。下面是使用这种思路的客户端代码：

```php
// listing 10.15

class UnitScript {    
    public static function joinExisting (Unit $newUnit, Unit $occupyingUnit): CompositeUnit {        
        $comp = $occupyingUnit->getComposite();        
        if (! is_null($comp)) {            
            $comp->addUnit($newUnit);        
        } else {        
            $comp = new Army();
            $comp->addUnit($occupyingUnit);            
            $comp->addUnit($newUnit);        
            }        
        return $comp;    
    }
}
```

The joinExisting() method accepts two Unit objects. The first is a newcomer to a tile, and the second is a prior occupier. If the second Unit is a CompositeUnit, then the first will attempt to join it. If not, then a new Army will be created to cover both units. I have no way of knowing at first whether the \$occupyingUnit argument contains a CompositeUnit. A call to getComposite() settles the matter, though. If getComposite() returns an object, I can add the new Unit object to it directly. If not, I create the new Army object and add both.

I could simplify this model further by having the Unit::getComposite() method return an Army object prepopulated with the current Unit. Or I could return to the previous model (which did not distinguish structurally between composite and leaf objects) and have Unit::addUnit() do the same thing: create an Army object and add both Unit objects to it. This is neat, but it presupposes that you know in advance the type of composite you would like to use to aggregate your units. Your business logic will determine the kinds of assumptions you can make when you design methods like getComposite() and addUnit().

These contortions are symptomatic of a drawback to the Composite pattern. Simplicity is achieved by ensuring that all classes are derived from a common base. The benefit of simplicity is sometimes bought at a cost to type safety. The more complex your model becomes, the more manual type checking you are likely to have to do. Let’s say that I have a Cavalry object. If the rules of the game state that you cannot put a horse on a troop carrier, I have no automatic way of enforcing this with the Composite pattern:

joinExisting() 方法有两个 Unit 对象参数。第一个参数是一个区块的新来者，第二个参数是之前的占据者。如果第二个 Unit 对象是一个 CompositeUnit 对象，那么第一个 Unit 对象被添加给它。但如果不是的话，方法将会创建一个新 Army 对象并将这两个对象添加到 Army 对象中。我们一开始并不知道 occupyingUnit 参数是否包含 CompositeUnit 对象，但是通过调  getComposite() 可以解决这个问题。若 getComposite() 返回对象，那么我们可以直接添加新的 Unit 对象。如果不是，那么我们创建一个新的 Army 象，并将两个 Unit 对象都添加给它。

我们还可以进一步简化该模型，让 Unit::getComposite() 方法返回一个添加当前 Unit 的 Army 对象。或者也可以返回前面的模型（即不从结构上区分组合或局部对象），并用 Unit::addUnit() 方法来做同样的事情：创建一个 Army 对象，并将两个 Unit 对象都添加给它。虽然这样代码很简洁，但是这假设你已经预先知道了部队单元所要聚合的组合类型。当你设计如  getComposite() 和 addUnit() 这样的方法时，业务逻辑将决定你所能做的假设。

而这正是组合模式缺陷的症状之一。简化的前提是使所有的类都继承同一个基类。简化的好处有时会以降低对象类型安全为代价。模型变得越复杂，你就不得不手动进行越多的类型检査。比如有一个 Cavalry（骑兵）对象，假设游戏规则规定不能将一匹马放到运兵船上，在组合模式中我们并没有自动化的方式来强制执行这个规则。

```php
// listing 10.16

class TroopCarrier extends CompositeUnit {    
    public function addUnit(Unit $unit) {        
        if ($unit instanceof Cavalry) {            
            throw new UnitException("Can't get a horse on the vehicle");        
        }        
        parent::addUnit($unit);    
    }

    public function bombardStrength(): int {        
        return 0;    
    }
}
```

I am forced to use the instanceof operator to test the type of the object passed to addUnit(). If you have too many special cases of this kind, the drawbacks of the pattern begin to outweigh its benefits. Composite works best when most of the components are interchangeable.

Another issue to bear in mind is the cost of some Composite operations. The Army::bombardStrength() method is typical in that it sets off a cascade of calls to the same method down the tree. For a large tree with lots of subarmies, a single call can cause an avalanche behind the scenes. bombardStrength() is not itself very expensive, but what would happen if some leaves performed a complex calculation to arrive at their return values? One way around this problem is to cache the result of a method call of this sort in the parent 

object, so that subsequent invocations are less expensive. You need to be careful, though, to ensure that the cached value does not grow stale. You should devise strategies to wipe any caches whenever any operations take place on the tree. This may require that you give child objects references to their parents.

这里我们不得不使用 instanceof 操作符来检査传给 addUnit() 方法的对象类型。特殊对象越来越多，组合模式开始渐渐显得弊大于利。在大部分局部对象可互换的情况下，组合模式才最适用。需要担心的另外一个问题是组合操作的成本。Army::bombardStrength() 方法便是典型的例子，该方法会逐级调用对象树中下级分支的方法。如果一个对象树中有大量子 Army 对象，一个简单的调用可能会导致系统崩溃。虽然 bombardStrength() 方法自身并不一定会带来多大的系统开销，但是如果一些局部对象为了获得返回值而执行一系列复杂的计算，那么会发生什么呢？解决问题的一个办法是在父级对象中缓存计算结果，这样可使接下来的调用减少系统开销。尽管如此，你还是需要小心地保证缓存值不会失效。因此你需要设计一个当对树进行操作时可移除过期缓存的策略，而这也许会要求你给子对象加上对父对象的引用。

1『确实，所以使用组合模式的前提是，树形对象结构。（2020-09-10）』

Finally, a note about persistence. The Composite pattern is elegant, but it doesn’t lend itself neatly to storage in a relational database. This is because, by default, you access the entire structure only through a cascade of references. To construct a Composite structure from a database in the natural way, you would have to make multiple expensive queries. You can get around this problem by assigning an ID to the whole tree, so that all components can be drawn from the database in one go. Having acquired all the objects, however, you would still have the task of recreating the parent/child references, which themselves would have to be stored in the database. This is not difficult, but it is somewhat messy.

Although Composites sit uneasily with relational databases, they lend themselves very well indeed to storage in XML. This is because XML elements are often themselves composed of trees of subelements.

Composite in SummarySo the Composite pattern is useful when you need to treat a collection of things in the same way as you would an individual, either because the collection is intrinsically like a component (armies and archers), or because the context gives the collection the same characteristics as the component (line items in an invoice). Composites are arranged in trees, so an operation on the whole can affect the parts, and data from the parts is transparently available via the whole. The Composite pattern makes such operations and queries transparent to the client. Trees are easy to traverse (as we shall see in the next chapter). It is easy to add new component types to Composite structures.

On the downside, Composites rely on the similarity of their parts. As soon as we introduce complex rules as to which composite object can hold which set of components, our code can become hard to manage. Composites do not lend themselves well to storage in relational databases, but are well suited to XML persistence.

最后，在对象持久化上需要注意一些地方。虽然组合模式是一个优雅的模式，但它并不能将自身轻松地存储到关系数据库里。这是因为在默认的情况下，你是通过级联引用来访问整个结构的。因此，按正常的途径从数据库构造一个组合结构，你将不得不使用多个昂贵的查询。我们可以通过给对象树中的每个节点赋于 ID 值来避免这个问题，于是所有组件都可从数据库中一次性取出。但是获得这些对象后，我们仍旧需要重建父子之间的引用关系，以便它们再保存回数据库虽然这不难，可并不优雅，甚至有些混乱。虽然组合模式难以使数据保存在关系型数据库中，但其数据却非常适合持久化为 XML。这是因为 XML 元素通常是由树型结构的子元素组合而成的。

如果你想像对待单个对象一样对待组合对象，那么组合模式十分有用。可能是因为组合对象本质上和局部对象（比如 Army 和 Archer）相似，也可能因为在环境中组合对象与局部对象（如发票中的条目）的特征相同。因为组合模式是树型结构，所以对整体的操作会影响到局部，而通过组合，对客户端代码来说局部的数据又是透明的。组合模式使这些操作和查询对客户端代码透明。对象树可以方便地进行遍历（在下一章中我们将可以看到）。你也可以轻松地在组合结构中加入新的组件类型。但另一方面，组合模式又依赖于其组成部分的简单性。随着我们引入复杂的规则，代码会变得越来越难以维护。组合模式不能很好地在关系数据库中保存数据，但却非常适合使用 XML 持久化。

## 4.3 The Decorator Pattern

While the Composite pattern helps us to create a flexible representation of aggregated components, the Decorator pattern uses a similar structure to help us to modify the functionality of concrete components. Once again, the key to this pattern lies in the importance of composition at runtime. Inheritance is a neat way of building on characteristics laid down by a parent class. This neatness can lead you to hard-code variation into your inheritance hierarchies, often causing inflexibility.

组合模式帮助我们聚合组件，而装饰模式则使用类似结构来帮助我们改变具体组件的功能。该模式同样体现了组合的重要性，但组合是在代码运行时实现的。继承是共享父类特性的一种简单的办法，但可能会使你将需要改变的特性硬编码到继承体系中，而这常会降低系统灵活性。

### 4.3.1 The Problem

Building all your functionality into an inheritance structure can result in an explosion of classes in a system. Even worse, as you try to apply similar modifications to different branches of your inheritance tree, you are likely to see duplication emerge.

将所有功能建立在继承体系上会导致系统中的类「爆炸式」增多。更糟糕的是，当你尝试对继承树上不同的分支做相似的修改时，代码可能会产生重复。

Let’s return to our game. Here, I define a Tile class and a derived type:


```php
// listing 10.17

abstract class Tile {    
    abstract public function getWealthFactor(): int;
}

// listing 10.18

class Plains extends Tile {    
    private $wealthfactor = 2;

    public function getWealthFactor(): int {        
        return $this->wealthfactor;    
    }
}
```

A tile represents a square on which my units might be found. Each tile has certain characteristics. In this example, I have defined a getWealthFactor() method that affects the revenue a particular square might generate if owned by a player. As you can see, Plains objects have a wealth factor of 2. Obviously, tiles manage other data. They might also hold a reference to image information, so that the board can be drawn. Once again, I’ll keep things simple here.

I need to modify the behavior of the Plains object to handle the effects of natural resources and human abuse. I wish to model the occurrence of diamonds on the landscape, and the damage caused by pollution. One approach might be to inherit from the Plains object:

我们定义了ー个 tile 类。tile 表示部队单元所在的一个区域。每个 tile 对象都有明确的特征。在本例中，我们定义了一个 getWealthFactor() 方法，用于计算当某个特定区域被一个玩家所占有后的收益。如你所见，Plains（平原）对象的财富系数是 2。显然，tile 对象还管理其他数据。它们也许会有对图片的引用，用于在屏幕上绘图。这里我们还是先保持简单。我们还需要修改 Pains 对象的行为，用于处理一些自然资源和人类滥用的效果。我们希望为地表钻石的分布和污染造成的破坏建模。有一个办法是从 Pains 对象派生：

```php
// listing 10.19

class DiamondPlains extends Plains {    
    public function getWealthFactor(): int {        
        return parent::getWealthFactor() + 2;    
    }
}

// listing 10.20

class PollutedPlains extends Plains {    
    public function getWealthFactor(): int {        
        return parent::getWealthFactor() - 4;    
    }
}
```

I can now acquire a polluted tile very easily:

```php
// listing 10.21

$tile = new PollutedPlains();
print $tile->getWealthFactor();
```

You can see the class diagram for this example in Figure 10-3.

Figure 10-3.  Building variation into an inheritance tree

This structure is obviously inflexible. I can get plains with diamonds. I can get polluted plains. But can I get them both? Clearly not, unless I am willing to perpetrate the horror that is PollutedDiamondPlains. This situation can only get worse when I introduce the Forest class, which can also have diamonds and pollution.

This is an extreme example, of course, but the point is made. Relying entirely on inheritance to define your functionality can lead to a multiplicity of classes and a tendency toward duplication.

Let’s take a more commonplace example at this point. Serious web applications often have to perform a range of actions on a request before a task is initiated to form a response. You might need to authenticate the user, for example, and to log the request. Perhaps you should process the request to build a data structure from raw input. Finally, you must perform your core processing. You are presented with the same problem.

You can extend the functionality of a base ProcessRequest class with additional processing in a derived LogRequest class, in a StructureRequest class, and in an AuthenticateRequest class. You can see this class hierarchy in Figure 10-4.

Figure 10-4.  More hard-coded variations

What happens, though, when you need to perform logging and authentication, but not data preparation? Do you create a LogAndAuthenticateProcessor class? Clearly, it is time to find a more flexible solution.

关于这个问题，我们再举一个更真实的例子。真正的 Web 应用要在返回响应给用户之前执行一系列操作，例如验证用户及记录请求等。也许还需要将请求中的原始输入处理成某种数据结构。最后，还必须执行核心操作。此时我们遇到了同样的问题。在派生的 LogRequest 类、StructureRequest 类和 AuthenticateRequest 类中，我们可以对基类 ProcessRequest 类的功能进行扩展，并加上额外的处理。你可以在图 10-4 中看到该层级关系。但是当需要执行记录和验证，而不需要准备数据时，该怎么办？创建一个 LogAndAuthenticateProcessor 类？显然，我们必须找出一个更灵活的方案。

### 4.3.2 Implementation

Rather than use only inheritance to solve the problem of varying functionality, the Decorator pattern uses composition and delegation. In essence, Decorator classes hold an instance of another class of their own type. A Decorator will implement an operation so that it calls the same operation on the object to which it has a reference before (or after) performing its own actions. In this way, it is possible to build a pipeline of Decorator objects at runtime.

1『装饰者模式，其实就是「组合优于继承」的一种具体实现方法。（2020-09-10）』

装饰模式使用组合和委托而不是只使用继承来解决功能变化的问题。实际上，Decorator 类会持有另外一个类的实例。Decorator 对象会实现与被调用对象的方法相对应的类方法。用这种办法可以在运行时创建一系列的 Decorator 对象。

Let’s rewrite our game example to illustrate this:

```php
abstract class Tile {    
    abstract public function getWealthFactor(): int;
}

class Plains extends Tile {    
    private $wealthfactor = 2;

    public function getWealthFactor(): int    {        
        return $this->wealthfactor;    
    }
}

// listing 10.22

abstract class TileDecorator extends Tile {    
    protected $tile;

    public function __construct(Tile $tile)    {        
        $this->tile = $tile;    
    }
}
```

Here, I have declared Tile and Plains classes as before, but I have also introduced a new class: TileDecorator. This does not implement getWealthFactor(), so it must be declared abstract. I define a constructor that requires a Tile object, which it stores in a property called \$tile. I make this property protected so that child classes can gain access to it. Now I’ll redefine the Pollution and Diamond classes:

1『子类继承一个抽象父类，如果该子类也是抽象类的话，就不需要实现抽象父类里的抽象方法了。（2020-09-10）』

```php
// listing 10.23

class DiamondDecorator extends TileDecorator {    
    public function getWealthFactor(): int {
        return $this->tile->getWealthFactor() + 2;    
    }
}

// listing 10.24

class PollutionDecorator extends TileDecorator {    
    public function getWealthFactor(): int {        
        return $this->tile->getWealthFactor() - 4;    
    }
}
```

Each of these classes extends TileDecorator. This means that they have a reference to a Tile object. When getWealthFactor() is invoked, each of these classes invokes the same method on its Tile reference before making its own adjustment. By using composition and delegation like this, you make it easy to combine objects at runtime. 

Because all the objects in the pattern extend Tile, the client does not need to know which combination it is working with. It can be sure that a getWealthFactor() method is available for any Tile object, whether it is decorating another behind the scenes or not:

这些类都扩展自 TileDecorator 类，这意味着它们拥有指向 Tile 对象的引用。当 getWealthFactor() 方法被调用时，这些类都会先调用所引用的 Tile 对象的 getWealthFactor() 方法，然后执行自己特有的操作。通过像这样使用组合和委托，可以在运行时轻松地合并对象。因为模式中所有的对象都扩展自 Tile，所以客户端代码并不需要知道内部是如何合并的。getWealthFactor() 方法在任何 Tile 对象中都是可用的，无论该对象是一个装饰器对象还是真正的 Tile 对象。

```php
// listing 10.25

$tile = new Plains();
print $tile->getWealthFactor(); // 2
```

Plains is a component. It simply returns 2:

```php
// listing 10.26

$tile = new DiamondDecorator(new Plains());
print $tile->getWealthFactor(); // 4
```

DiamondDecorator has a reference to a Plains object. It invokes getWealthFactor() before adding its own weighting of 2:

```php
// listing 10.27

$tile = new PollutionDecorator(new DiamondDecorator(new Plains()));
print $tile->getWealthFactor(); // 0
```

PollutionDecorator has a reference to a DiamondDecorator object, which has its own Tile reference.You can see the class diagram for this example in Figure 10-5.

Figure 10-5.  The Decorator pattern

This model is very extensible. You can add new decorators and components very easily. With lots of decorators, you can build very flexible structures at runtime. The component class, Plains in this case, can be significantly modified in many ways without the need to build the totality of the modifications into the class hierarchy. In plain English, this means you can have a polluted Plains object that has diamonds, without having to create a PollutedDiamondPlains object.

The Decorator pattern builds up pipelines that are very useful for creating filters. The java.io package makes great use of decorator classes. The client coder can combine decorator objects with core components to add filtering, buffering, compression, and so on to core methods like read(). My web request example can also be developed into a configurable pipeline. Here’s a simple implementation that uses the Decorator pattern:

这样的模型极具扩展性。我们可以非常轻松地添加新的装饰器或者新的组件。通过使用大量的装饰器，我们可以在运行时创建极为灵活的结构。本例中的组件类 Pains 的行为可以很方便地被改变，而不需要改动原来的类。通俗地说，这意味着不需要创建 PollutedDiamondPlains 对象，就可以构造一个拥有钻石并被污染的 Plains 对象。

饰模式所建立的管道对于创建过滤器非常有用。Java 的 IO 包便广泛使用了装饰器类。客户端程序员可将核心组件与装饰对象合并，从而对核心方法（如 read() 进行过滤、缓冲、压缩等操作。我们的 Web 请求示例也能被开发为一个具有可配置管道的模型。下面便是使用装饰模式的一个简单实现。

```php
// listing 10.28

class RequestHelper{}

// listing 10.29

abstract class ProcessRequest {    
    abstract public function process(RequestHelper $req);
}

// listing 10.30

class MainProcess extends ProcessRequest {    
    public function process(RequestHelper $req) {        
        print __CLASS__ . ": doing something useful with request\n";
    }
}

// listing 10.31

abstract class DecorateProcess extends ProcessRequest {    
    protected $processrequest;

    public function __construct(ProcessRequest $pr)    {        
    $this->processrequest = $pr;    
    }
}
```

As before, we define an abstract superclass (ProcessRequest), a concrete component (MainProcess), and an abstract decorator (DecorateProcess). MainProcess::process() does nothing but report that it has been called. DecorateProcess stores a ProcessRequest object on behalf of its children. Here are some simple concrete decorator classes:

```php
// listing 10.32

class LogRequest extends DecorateProcess {    
    public function process(RequestHelper $req) {        
        print __CLASS__ . ": logging request\n";        
        $this->processrequest->process($req);    
    }
}

// listing 10.33

class AuthenticateRequest extends DecorateProcess {    
    public function process(RequestHelper $req) {        
        print __CLASS__ . ": authenticating request\n";        
        $this->processrequest->process($req);    
    }
}

// listing 10.34

class StructureRequest extends DecorateProcess {    
    public function process(RequestHelper $req) {        
        print __CLASS__ . ": structuring request data\n";        
        $this->processrequest->process($req);    
    }
}
```

Each process() method outputs a message before calling the referenced ProcessRequest object’s own process() method. You can now combine objects instantiated from these classes at runtime to build filters that perform different actions on a request, and in different orders. Here’s some code to combine objects from all these concrete classes into a single filter:

装饰类的每个 process() 方法在调用引用的 ProcessRequest 对象的 process() 方法前输出条信息。现在我们可以在运行时合并这些类的初始对象，创建过滤器来对每一个请求按不同的顺序执行不同的操作。下面的代码将所有具体类的对象组合为一个过滤器。

```php
// listing 10.35

$process = new AuthenticateRequest(new StructureRequest(    
                                                            new LogRequest(        
                                                            new MainProcess()    
                                                            )));
$process->process(new RequestHelper());
```

This code gives the following output:

```
popp\ch10\batch07\
Authenticate
Request: authenticating request

popp\ch10\batch07\
StructureRequest: structuring request data

popp\ch10\batch07\
LogRequest: logging requestpopp

ch10\batch07\
MainProcess: doing something useful with request
```

■ Note: this example is, in fact, also an instance of an enterprise pattern called intercepting filter. intercepting filter is described in Core J2EE Patterns: Best Practices and Design Strategies (prentice hall, 2001) by alur et al.

### 4.3.3 Consequences

Like the Composite pattern, Decorator can be confusing. It is important to remember that both composition and inheritance are coming into play at the same time. So LogRequest inherits its interface from ProcessRequest, but it is acting as a wrapper around another ProcessRequest object.

Because a decorator object forms a wrapper around a child object, it helps to keep the interface as sparse as possible. If you build a heavily featured base class, then decorators are forced to delegate to all public methods in their contained object. This can be done in the abstract decorator class, but it still introduces the kind of coupling that can lead to bugs.

1『装饰者模式中，装饰类一定要简单，里面的方法要少，可以用一个简单的抽象类来作为装饰类。（2020-09-10）』

Some programmers create decorators that do not share a common type with the objects they modify. As long as they fulfill the same interface as these objects, this strategy can work well. You get the benefit of being able to use the built-in interceptor methods to automate delegation (implementing \_\_call() to catch calls to nonexistent methods and invoking the same method on the child object automatically). However, by doing this, you also lose the safety afforded by class type checking. In our examples so far, client code can demand a Tile or a ProcessRequest object in its argument list and be certain of its interface, whether or not the object in question is heavily decorated.

和组合模式一样，裝饰模式有时也会令人困惑。一定要记住：组合和继承通常都是同时使用的。因此，LogRequest 是继承自 ProcessRequest 的，但是却表现为对另外一个 ProcessRequest 对象的封装。因为裝饰对象作为子对象的包装，所以保持基类中的方法尽可能少是很重要的。如果一个基类具有大量特性，那么装饰对象不得不为它们包装的对象的所有 public 方法加上委托。你可以用一个抽象的装饰类来实现，不过这仍旧会带来耦合，并可能导致 bug 的出现。

有些程序员创建的装饰类与其中拥有的对象并不共享相同的对象类型。只要这些装饰类提供相同的接口，这个策略也是可行的。使用 PHP 内建的拦截方法来实现自动委托，可以带来很多好处（如通过实现 \_\_call() 方法来捕捉装饰类中不存在的方法，并自动调用子对象对应的相同的方法）。但是，这样的话会丧失类型检査带来的安全性。就我们的例子来说，客户端代码要求传入的参数是一个 Tile 或 ProcessRequest 对象，并能确定该对象可以提供某些接口，无论传入的对象是否经过大量装饰。

## 4.4 The Facade Pattern

You may have had occasion to stitch third-party systems into your own projects in the past. Whether or not the code is object oriented, it will often be daunting, large, and complex. Your own code, too, may become a challenge to the client programmer who needs only to access a few features. The Facade pattern is a way of providing a simple, clear interface to complex systems.

可能你曾经有过在项目中集成第三方代码的经历。无论第三方代码是否面向对象，集成通常都是巨大而且复杂的工作，很容易让人畏缩。而对一个客户程序员来说，你的代码也可能是一个挑战，即使他可能仅需要访问很小一部分特性。外观模式可以为复杂系统创建一个简单、清晰的接口。

### 4.4.1 The Problem

Systems tend to evolve large amounts of code that is really only useful within the system itself. Just as classes define clear public interfaces and hide their guts away from the rest of the world, so should well-designed systems. However, it is not always clear which parts of a system are designed to be used by client code and which are best hidden.

As you work with subsystems (like web forums or gallery applications), you may find yourself making calls deep into the logic of the code. If the subsystem code is subject to change over time, and your code interacts with it at many different points, you may find yourself with a serious maintenance problem as the subsystem evolves.

Similarly, when you build your own systems, it is a good idea to organize distinct parts into separate tiers. Typically, you may have a tier responsible for application logic, another for database interaction, another for presentation, and so on. You should aspire to keep these tiers as independent of one another as you can, so that a change in one area of your project will have minimal repercussions elsewhere. If code from one tier is tightly integrated into code from another, then this objective is hard to meet.

Here is some deliberately confusing procedural code that makes a song-and-dance routine of the simple process of getting log information from a file and turning it into object data:

在系统中总会逐渐形成大量仅在系统自身内部有用的代码。系统也应该像类那样，提供定义清晰的公共接口，并对外隐藏内部结构。但是，系统中哪部分应该设置为公开，哪部分设置为隐藏并不容易决定。当使用子系统（如 Web 论坛或者图库）的代码时，你也许会发现自己过于深入地调用子系统的逻辑代码。如果子系统代码总是在不断变化，而你的代码却又在许多不同地方与子系统代码交互，那么随着子系统的发展，你也许会发现维护代码变得非常困难。

类似地，当你创建自己的系统时，将不同的部分分层是很好的做法。例如，你可能会把系统分为应用逻辑层、数据库交互层和表现层等。你应该尽可能地使这些分层互相独立，以便项目中某一部分的修改尽量不影响到其他地方。如果某层中的代码与另一层的代码存在耦合的话，那么这个目标就很难达成了。下面是一些故意让人混淆的不着边际的程序代码，其功能只是从文件中获取 log 信息并将它转换为对象数据。

```php
// listing 10.36

function getProductFileLines($file) {    
    return file($file);
}

function getProductObjectFromId($id, $productname) {    
    // some kind of database lookup    
    return new Product($id, $productname);
}

function getNameFromLine($line) {    
    if (preg_match("/.*-(.*)\s\d+/", $line, $array)) {        
        return str_replace('_', ' ', $array[1]);    
    }    
    return '';
}

function getIDFromLine($line) {    
    if (preg_match("/^(\d{1,3})-/", $line, $array)) {        
        return $array[1];    
    }    
    return -1;
}

class Product {    
    public $id;    
    public $name;

    public function __construct($id, $name) {        
        $this->id = $id;        
        $this->name = $name;    
    }
}
```

Let’s imagine that the internals of this code are more complicated than they actually are, and that I am stuck with using it rather than rewriting it from scratch. For example, assume I have to turn a file that contains lines like these into an array of objects:

假设上面代码的内部其实是更复杂的，这样我们可以继续使用它们而非从头开始重写。我们的目的是将包含类似下面数据的文件转换为一个对象数组。而我们必须调用所有这些方法（注意为了简单起见，我们并不计算出价格的最终数字）：

```
234-ladies_jumper 55
532-gents_hat 44
```

To do so, I must call all of these functions (note that, for the sake of brevity, I don’t extract the final number, which represents a price):

```php
// listing 10.37

$lines = getProductFileLines(__DIR__ . '/test2.txt');
$objects = [];
foreach ($lines as $line) {    
    $id = getIDFromLine($line);    
    $name = getNameFromLine($line);    
    $objects[$id] = getProductObjectFromID($id, $name);
}
```

If I call these functions directly like this throughout my project, my code will become tightly wound into the subsystem it is using. This could cause problems if the subsystem changes, or if I decide to switch it out entirely. I really need to introduce a gateway between the system and the rest of our code.

如果在项目中像这样直接调用这些方法，那么我们的代码会和子系统紧紧地耦合在一起。当子系统变化时，或者我们决定将其与子系统完全断开时，代码就会出问题。可见，我们需要在这些子系统和代码中引入一个入口。

### 4.4.2 Implementation

Here is a simple class that provides an interface to the procedural code you encountered in the previous section:

```php
// listing 10.38

class ProductFacade {    
    private $products = [];

    public function __construct(string $file) {        
        $this->file = $file;        
        $this->compile();    
    }

    private function compile() {        
        $lines = getProductFileLines($this->file);

        foreach ($lines as $line) {            
            $id = getIDFromLine($line);            
            $name = getNameFromLine($line);            
            $this->products[$id] = getProductObjectFromID($id, $name);        
        }    
    }

    public function getProducts(): array    {        
        return $this->products;    
    }

    public function getProduct(string $id): \Product {        
        if (isset($this->products[$id])) {            
            return $this->products[$id];        
        }        
        return null;    
    }
}
```

From the point of view of the client code, access to Product objects from a log file is much simplified:

```php
// listing 10.39

$facade = new ProductFacade(__DIR__ . '/test2.txt');
$object = $facade->getProduct("234");
```

1『门面模式，其实对面向对象编程范式中「封装性」的一个具体应用案例。』

### 4.4.3 Consequences

A Facade is really a very simple concept. It is just a matter of creating a single point of entry for a tier or subsystem. This has a number of benefits. It helps to decouple distinct areas in a project from one another. It is useful and convenient for client coders to have access to simple methods that achieve clear ends. It reduces errors by focusing the use of a subsystem in one place; changes to the subsystem should cause failure in a predictable location. Errors are also minimized by Facade classes in complex subsystems where client code might otherwise use internal functions incorrectly.

Despite the simplicity of the Facade pattern, it is all too easy to forget to use it, especially if you are familiar with the subsystem you are working with. There is a balance to be struck, of course. On the one hand, the benefit of creating simple interfaces to complex systems should be clear. On the other hand, one could abstract systems with reckless abandon, and then abstract the abstractions. If you are making significant simplifications for the clear benefit of client code, and/or shielding it from systems that might change, then you are probably right to implement the Facade pattern.

外观模式是一个十分简单的概念，它只是为一个分层或一个子系统创建一个单一的入口。这会带来许多好处。首先，有助于分离项目中的不同部分。其次，对于客户端开发者来说，访问代码变得简洁，非常方便。另外，由于只在一个地方调用子系统，减少了出错的可能性，并因此可以预估子系统修改带来的问题所在。Facades 类还能使客户端代码避免不正确地使用子系统中复杂的内部方法，从而减少错误的发生。

尽管外观模式十分简单，但你很容易忘记它，特别是在你熟悉所使用的子系统时。这里存在着某种平衡。一方面，为复杂系统创建简单接口的好处是明显的；另一方面，你可能会过度抽象系统。总之，如果你想获得简洁的客户端访问代码，或者想把系统中的修改对客户端代码隐藏，那么你也许应该实现外观模式。

## Summary

In this chapter, I looked at a few of the ways that classes and objects can be organized in a system. In particular, I focused on the principle that composition can be used to engender flexibility where inheritance fails. In both the Composite and Decorator patterns, inheritance is used to promote composition and to define a common interface that provides guarantees for client code.

You also saw delegation used effectively in these patterns. Finally, I looked at the simple but powerful Facade pattern. Facade is one of those patterns that many people have been using for years without having a name to give it. Facade lets you provide a clean point of entry to a tier or subsystem. In PHP, the Facade pattern is also used to create object wrappers that encapsulate blocks of procedural code.

在本章中，我们研究了类和对象的几种组织方式，其中特别关注了使用组合以得到继承无法达到的灵活性。在组合模式和装饰模式中，使用继承是为了更好地组合对象，并为客户端代码提供统一的接口。我们也可以看到在这些模式中委托是如何被有效使用的。最后，我们研究了简单却强大的外观模式。外观模式是众多模式中一个被很多人运用了多年却没有得到命名的模式。外观模式可以为一个分层或一个子系统提供一个简洁的入口。在 PHP 中，外观模式也可用于创建封装过程式代码块的对象封装器。