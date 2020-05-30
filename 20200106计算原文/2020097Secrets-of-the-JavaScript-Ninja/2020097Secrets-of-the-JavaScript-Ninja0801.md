# 0801. Controlling access to objects

This chapter covers: 1) Using getters and setters to control access to object properties. 2) Controlling access to objects through proxies. 3) Using proxies for cross-cutting concerns.

In the previous chapter, you saw that JavaScript objects are dynamic collections of properties. We can easily add new properties, change the values of properties, and even completely remove existing properties. In many situations (for example, when validating property values, logging, or displaying data in the UI), we need to be able to monitor exactly what’s going on with our objects. So in this chapter, you’ll learn techniques for controlling access to and monitoring all of the changes that occur in your objects.

We’ll start with getters and setters, methods that control access to specific object properties. You first saw these methods in action in chapters 5 and 7. In this chapter, you’ll see some of their built-in language support and how to use them for logging, performing data validation, and defining computed properties. 

We’ll continue with proxies, a completely new type of object introduced in ES6. These objects control access to other objects. You’ll learn how they work and how to use them to great effect to easily expand your code with cross-cutting concerns such as performance measurement or logging, and how to avoid null exceptions by autopopulating object properties. Let’s start the journey with something we already know to a certain degree: getters and setters.

..............................................................

Do you know?

What are some of the benefits of accessing a property’s value through getters and setters?

What is the main difference between proxies and getters and setters?

What are proxy traps? Name three types of trap.

..............................................................

## 8.1 Controlling access to properties with getters and setters

In JavaScript, objects are relatively simple collections of properties. The primary way to keep track of our program state is by modifying those properties. For example, consider the following code:

function Ninja (level) { this.skillLevel = level; } const ninja = new Ninja(100);

Here we define a Ninja constructor that creates ninja objects with a property skill-Level. Later, if we want to change the value of that property, we can write the following code: ninja.skillLevel = 20.

That’s all nice and convenient, but what happens in the following cases?

We want to safeguard against accidental mistakes, such as assigning unanticipated data. For example, we want to stop ourselves from doing something like assigning a value of a wrong type: ninja.skillLevel = "high".

We want to log all changes to the skillLevel property.

We need to show the value of our skillLevel property somewhere in the UI of our web page. Naturally, we want to present the last, up-to-date value of the property, but how can we easily do this?

We can handle all of these cases elegantly with getter and setter methods.

In chapter 5, you saw a glimpse of getters and setters as a means of mimicking private object properties in JavaScript through closures. Let’s revisit the material you’ve learned so far, by working with ninjas that have a private skillLevel property accessible only through getters and setters, as shown in the following listing.

Listing 8.1

Using getters and setters to guard private properties

function Ninja () { let skillLevel;

Defines a private skillLevel variable Controlling access to properties with getters and setters

201

The getter method controls access to our private skillLevel variable.

this.getSkillLevel = () => skillLevel; this.setSkillLevel = value => { skillLevel = value; };

The setter method controls the values we can assign to skillLevel.

} const ninja = new Ninja(); ninja.setSkillLevel(100); assert(ninja.getSkillLevel() === 100, "Our ninja is at level 100!");

Sets a new value of skillLevel through the setter method

Retrieves the value of skillLevel with the getter method

We define a Ninja constructor that creates ninjas with a “private” skillLevel variable accessible only through our getSkillLevel and setSkillLevel methods: The property value can be obtained only through the getSkillLevel method, whereas a new property value can be set only through the setSkillLevel method (remember chapter 5 on closures?).

Now, if we want to log all read attempts of the skillLevel property, we expand the getSkillLevel method; and if we want to react to all write attempts, we expand the setSkillLevel method, as in the following snippet:

function Ninja () {

let skillLevel; this.getSkillLevel = () => {

Using getters, we can know whenever code accesses a property.

report("Getting skill level value");

return skillLevel; }; this.setSkillLevel = value => {

report("Modifying skillLevel property from:", skillLevel, "to: ", value);

skillLevel = value; }

}

Using setters, we can know whenever code wants to set a new value to a property.

This is great. We can easily react to all interactions with our properties by plugging in, for example, logging, data validation, or other side effects such as UI modifications.

But one nagging concern might be popping into your mind. The skillLevel property is a value property; it references data (the number 100), and not a function. Unfortunately, in order to take advantage of all the benefits of controlled access, all our interactions with the property have to be made by explicitly calling the associated methods, which is, to be honest, slightly awkward.

Luckily, JavaScript has built-in support for true getters and setters: properties that are accessed as normal data properties (for example, ninja.skillLevel), but that are methods that can compute the value of a requested property, validate the passed-in value, or whatever else we need them to do. Let’s take a look at this built-in support. 202

CHAPTER 8

Controlling access to objects

8.1.1 Defining getters and setters

In JavaScript, getter and setter methods can be defined in two ways:

■ ■

By specifying them within object literals or within ES6 class definitions By using the built-in Object.defineProperty method

Explicit support for getters and setters has existed for quite some time now, since the days of ES5. As always, let’s explore the syntax through an example. In this case, we have an object storing a list of ninjas, and we want to be able to get and set the first ninja in the list.

Listing 8.2

Defining getters and setters in object literals

const ninjaCollection = { ninjas: ["Yoshi", "Kuma", "Hattori"], get firstNinja(){ report("Getting firstNinja"); return this.ninjas[0]; }, set firstNinja(value){ report("Setting firstNinja"); this.ninjas[0] = value; } };

Defines a getter method for the firstNinja property that returns the first ninja in our collection and logs a message

Defines a setter method for the firstNinja property that modifies the first ninja in our collection and logs a message

Accesses the firstNinja property as if it were a standard object property

assert(ninjaCollection.firstNinja === "Yoshi", "Yoshi is the first ninja"); ninjaCollection.firstNinja = "Hachi"; assert(ninjaCollection.firstNinja === "Hachi"

&& ninjaCollection.ninjas[0] === "Hachi",

"Now Hachi is the first ninja");

Modifies the firstNinja property as if it were a standard object property

Tests that the property modification is stored

This example defines a ninjaCollection object that has a standard property, ninjas, which references an array of ninjas, and a getter and a setter for the property firstNinja. The general syntax for getters and setters is shown in figure 8.1.

Define a getter method by prefixing the property name with the get keyword.

Define a setter method by prefixing the property name with the set keyword.

Implicitly call the getter by reading the property value.

A getter doesn’t receive any arguments.

obj = { get name()

...

{

}, set name(value)

{

A setter receives one argument (the right side of an assignment expression).

...

} };

obj.name

obj.name =

"Yoshi"

Implicitly call the setter by assigning a value to a property.

Figure 8.1 The syntax for defining getters and setters. Prefix the property name with either the get or the set keyword. Controlling access to properties with getters and setters

203

As you can see, we define a getter property by prefixing the name with a get keyword, and a setter property with a set keyword.

In listing 8.2, both the getter and the setter log a message. In addition, the getter returns the value of the ninja at index 0, and the setter assigns a new value to the ninja at the same index:

get firstNinja(){ report("Getting firstNinja"); return this.ninjas[0]; }, set firstNinja(value){

report("Setting firstNinja");

this.ninjas[0] = value; }

Next, we test that accessing the getter property returns the first ninja, Yoshi:

assert(ninjaCollection.firstNinja === "Yoshi", "Yoshi is the first ninja");

Notice that the getter property is accessed as if it were a standard object property (and not as the method that it is).

After we access a getter property, the associated getter method is implicitly called, the message Getting firstNinja is logged, and the value of the ninja at index 0 is returned.

We continue by taking advantage of our setter method, and writing to the firstNinja property, again, just as we would assign a new value to a normal object property:

ninjaCollection.firstNinja = "Hachi";

Similar to the previous case, because the firstNinja property has a setter method, whenever we assign a value to that property, the setter method is implicitly called. This logs the message Setting firstNinja and modifies the value of the ninja at index 0.

Finally, we can test that our modification has done the work and that the new value of the ninja at index 0 can be accessed both through the ninjas collection and through our getter method:

assert(ninjaCollection.firstNinja === "Hachi"

&& ninjaCollection.ninjas[0] === "Hachi",

"Now Hachi is the first ninja");

Figure 8.2 shows the output generated by listing 8.2. When we access a property with a getter (for example, through ninjaCollection.firstNinja), the getter method is immediately called, and in this case, the message Getting firstNinja is logged. Later, we test that the output is Yoshi and that the message Yoshi is the first ninja is logged. We proceed similarly by assigning a new value to the firstNinja property, 204

CHAPTER 8

Controlling access to objects

Figure 8.2 The output from listing 8.2: if a property has a getter and a setter method, the getter method is implicitly called whenever we read the property value, and the setter method is called whenever we assign a new value to the property.

and as we can see in the output, this implicitly triggers the execution of the setter method, which outputs the message Setting firstNinja.

An important point to take from all this is that native getters and setters allow us to specify properties that are accessed as standard properties, but that are methods whose execution is triggered immediately when the property is accessed. This is further emphasized in figure 8.3.

const ninjaCollection = { ninjas: ["Yoshi", "Kuma", "Hattori"],

get firstNinja() {

Execution context stack

report("Getting firstNinja");

return this.ninjas[0];

}, ...

};

assert(ninjaCollection.firstNinja === "Yoshi",

"Yoshi is the first ninja");

get firstNinja execution context

Global execution context

Accessing a getter property immediately triggers the execution of the matching getter method!

The getter method is called, and a matching execution context is created and pushed on the stack. The process is the same as when a standard function is called.

Figure 8.3 Accessing a property with a getter method implicitly calls the matching getter. The process is the same as if this were a standard method call, and the getter method gets executed. A similar thing happens when we assign a value to a property through a setter method.

This syntax for defining a getter and a setter is straightforward, so it’s no wonder that we can use the exact same syntax to define getters and setters in other situations. The following example uses ES6 classes.

Listing 8.3

Using getters and setters with ES6 classes

class NinjaCollection { constructor(){

this.ninjas = ["Yoshi", "Kuma", "Hattori"];

} Controlling access to properties with getters and setters

get firstNinja(){ report("Getting firstNinja"); return this.ninjas[0]; } set firstNinja(value){ report("Setting firstNinja"); this.ninjas[0] = value; } } const ninjaCollection = new NinjaCollection(); assert(ninjaCollection.firstNinja === "Yoshi", "Yoshi is the first ninja"); ninjaCollection.firstNinja = "Hachi"; assert(ninjaCollection.firstNinja === "Hachi" "Now Hachi is the first ninja");

Defines a getter and a setter within an ES6 class

&& ninjaCollection.ninjas[0] === "Hachi",

205

This modifies the code from listing 8.2 to include ES6 classes. We keep all the tests to verify that the example still works as expected.

We don’t always have to define both a getter and a setter for a given property. For example, often we’ll want to provide only a getter. If in that case we still attempt to write a value to that property, the exact behavior depends on whether the code is in strict or nonstrict mode. If the code is in nonstrict mode, assigning a value to a property with only a getter achieves nothing; the JavaScript engine will silently ignore our request. If, on the other hand, the code is in strict mode, the JavaScript engine will throw a type error, indicating that we’re trying to assign a value to a property that has a getter but no setter.

NOTE

Although specifying getters and setters through ES6 classes and object literals is easy, you’ve probably noticed something missing. Traditionally, getters and setters are used to control access to private object properties, as in listing 8.1. Unfortunately, as we already know from chapter 5, JavaScript doesn’t have private object properties. Instead, we can mimic them through closures, by defining variables and specifying object methods that will close over those variables. Because with object literals and classes our getter and setter methods aren’t created within the same function scope as variables that we could use for private object properties, we can’t do this. Luckily, there’s an alternative way, through the Object.defineProperty method.

In chapter 7, you saw that the Object.defineProperty method can be used to define new properties by passing in a property descriptor object. Among other things, the property descriptor can include a get and a set property that define the property’s getter and setter methods.

We’ll use this feature to modify listing 8.1 to implement built-in getters and setters that control access to a “private” object property, as shown in the following listing. 206

CHAPTER 8

Controlling access to objects

Listing 8.4

Defining getters and setters with Object.defineProperty

Defines a constructor function

Uses the built-in Object.defineProperty to define a skillLevel property

function Ninja() { let _skillLevel = 0;

Defines a “private” variable that will be accessible through function closures

Object.defineProperty(this, 'skillLevel', { get: () => { report("The get method is called"); A get method that will be called whenever we read return _skillLevel; the skillLevel property. }, set: value => { report("The set method is called"); A set method that will be called _skillLevel = value; whenever we assign a value to } the skillLevel property.

});

}

Creates a new Ninja instance

const ninja = new Ninja();

The private variable isn’t accessible directly, but through the skillLevel getter.

assert(typeof ninja._skillLevel === "undefined", "We cannot access a 'private' property"); assert(ninja.skillLevel === 0, "The getter works fine!");

ninja.skillLevel = 10; assert(ninja.skillLevel === 10, "The value was updated");

The set method is implicitly called when assigning to the skillLevel property.

In this example, we first define a Ninja constructor function with a _skillLevel variable that we’ll use as a private variable, just as in listing 8.1.

Next, on the newly created object, referenced by the this keyword, we define a skillLevel property by using the built-in Object.defineProperty method:

Object.defineProperty(this, 'skillLevel', { get: () => { report("The get method is called"); return _skillLevel; }, set: value => { report("The set method is called"); _skillLevel = value; } });

Because we want the skillLevel property to control access to a private variable, we specify a get and a set method that will be called whenever the property is accessed.

Notice that, unlike getters and setters specified on object literals and classes, the get and set methods defined through Object.defineProperty are created in the same scope as the “private” skillLevel variable. Both methods create a closure Controlling access to properties with getters and setters

207

around the private variable, and we can access that private variable only through these two methods.

The rest of the code works exactly as in the previous examples. We create a new Ninja instance and check that we can’t access the private variable directly. Instead, all interactions have to go through the getter and setter, which we now use just as if they were standard object properties:

Activates the getter method

ninja.skillLevel === 0 ninja.skillLevel = 10

Activates the setter method

As you can see, the approach with Object.defineProperty is more verbose and complicated than getters and setters in object literals and classes. But in certain cases, when we need private object properties, it’s well worth it.

Regardless of the way we define them, getters and setters allow us to define object properties that are used like standard object properties, but are methods that can execute additional code whenever we read or write to a particular property. This is an incredibly useful feature that enables us to perform logging, validate assignment values, and even notify other parts of the code when certain changes occur. Let’s explore some of these applications.

8.1.2 Using getters and setters to validate property values

As we’ve established so far, a setter is a method that’s executed whenever we write a value to the matching property. We can take advantage of setters to perform an action whenever code attempts to update the value of a property. For example, one of the things we can do is validate the passed-in value. Take a look at the following code, which ensures that our skillLevel property can be assigned only integer values.

Listing 8.5

Validating property value assignments with setters

function Ninja() { let _skillLevel = 0;

Checks whether the passed-in value is an integer. If it isn’t, an exception is thrown.

Object.defineProperty(this, 'skillLevel', { get: () => _skillLevel, set: value => { if(!Number.isInteger(value)){ throw new TypeError("Skill level should be a number"); } _skillLevel = value; } });

}

const ninja = new Ninja();

ninja.skillLevel = 10; assert(ninja.skillLevel === 10, "The value was updated");

We can assign an integer value to the property. 208

CHAPTER 8

Controlling access to objects

try { ninja.skillLevel = "Great"; fail("Should not be here"); } catch(e){

pass("Setting a non-integer value throws an exception"); }

Trying to assign a noninteger value (in this case, a string) results in an exception thrown from the setter method.

This example is a straightforward extension to listing 8.4. The only major difference is that now, whenever a new value is assigned to the skillLevel property, we check whether the passed-in value is an integer. If it isn’t, an exception is thrown, and the private _skillLevel variable won’t be modified. If everything went okay and an integer value is received, we end up with a new value of the private _skillLevel variable:

set: value => { if(!Number.isInteger(value)){ throw new TypeError("Skill level should be a number"); } _skillLevel = value; }

When testing this code, we first check that all goes okay if we assign an integer:

ninja.skillLevel = 10; assert(ninja.skillLevel === 10, "The value was updated");

And then we test the situation in which we mistakenly assign a value of another type, such as a string. In that case, we should end up with an exception.

try { ninja.skillLevel = "Great"; fail("Should not be here"); } catch(e){

pass("Setting a non-integer value throws an exception"); }

This is how you avoid all those silly little bugs that happen when a value of the wrong type ends up in a certain property. Sure, it adds overhead, but that’s a price that we sometimes have to pay to safely use a highly dynamic language such as JavaScript.

This is just one example of the usefulness of setter methods; there are many more that we won’t explicitly explore. For example, you can use the same principle to track value history, perform logging, provide change notification, and more.

8.1.3 Using getters and setters to define computed properties

In addition to being able to control access to certain object properties, getters and setters can be used to define computed properties, properties whose value is calculated per request. Computed properties don’t store a value; they provide a get and/or a set method to retrieve and set other properties indirectly. In the following example, the object has two properties, name and clan, which we’ll use to compute the property fullTitle. Controlling access to properties with getters and setters

209

Listing 8.6

Defining computed properties

const shogun = { name: "Yoshiaki", clan: "Ashikaga", get fullTitle(){ return this.name + " " + this.clan; }, set fullTitle(value) { const segments = value.split(" "); this.name = segments[0]; this.clan = segments[1]; } };

Defines a getter method on a fullTitle property of an object literal that calculates the value by concatenating two object properties

Defines a setter method on a fullTitle property of an object literal that splits the passed-in value and updates two standard properties

assert(shogun.name === "Yoshiaki", "Our shogun Yoshiaki"); assert(shogun.clan === "Ashikaga", "Of clan Ashikaga"); assert(shogun.fullTitle === "Yoshiaki Ashikaga", "The full name is now Yoshiaki Ashikaga");

shogun.fullTitle = "Ieyasu Tokugawa"; assert(shogun.name === "Ieyasu", "Our shogun Ieyasu"); assert(shogun.clan === "Tokugawa", "Of clan Tokugawa"); assert(shogun.fullTitle === "Ieyasu Tokugawa", "The full name is now Ieyasu Tokugawa");

Assigning a value to the fullTitle property calls the set method, which computes and assigns new values to the name and clan properties.

The name and clan properties are normal properties whose values are directly obtained. Accessing the fullTitle property calls the get method, which computes the value.

Here we define a shogun object, with two standard properties, name and clan. In addition, we specify a getter and a setter method for a computed property, fullTitle:

const shogun = { name: "Yoshiaki", clan: "Ashikaga", get fullTitle(){ return this.name + " " + this.clan; }, set fullTitle(value) { const segments = value.split(" "); this.name = segments[0]; this.clan = segments[1]; } };

The get method computes the value of the fullTitle property, on request, by concatenating the name and clan properties. The set method, on the other hand, uses the built-in split method, available to all strings, to split the assigned string into segments by the space character. The first segment represents the name and is assigned to the name property, whereas the second segment represents the clan and is assigned to the clan property. 210

CHAPTER 8

Controlling access to objects

This takes care of both routes: Reading the fullTitle property computes its value, and writing to the fullTitle property modifies the properties that constitute the property value.

To be honest, we don’t have to use computed properties. A method called getFullTitle could be equally useful, but computed properties can improve the conceptual clarity of our code. If a certain value (in this case, the fullTitle value) depends only on the internal state of the object (in this case, on the name and clan properties), it makes perfect sense to represent it as a data field, a property, instead of a function.

This concludes our exploration of getters and setters. You’ve seen that they’re a useful addition to the language that can help us deal with logging, data validation, and detecting changes in property values. Unfortunately, sometimes this isn’t enough. In certain cases, we need to control all types of interactions with our objects, and for this, we can use a completely new type of object: a proxy.

8.2 Using proxies to control access

A proxy is a surrogate through which we control access to another object. It enables us to define custom actions that will be executed when an object is being interacted with—for example, when a property value is read or set, or when a method is called. You can think of proxies as almost a generalization of getters and setters; but with each getter and setter, you control access to only a single object property, whereas proxies enable you to generically handle all interactions with an object, including even method calls.

We can use proxies when we’d traditionally use getters and setters, such as for logging, data validation, and computed properties. But proxies are even more powerful. They allow us to easily add profiling and performance measurements to our code, autopopulate object properties in order to avoid pesky null exceptions, and to wrap host objects such as the DOM in order to reduce cross-browser incompatibilities.

Proxies are introduced by ES6. For current browser support, see http://mng.bz/9uEM.

NOTE

In JavaScript, we can create proxies by using the built-in Proxy constructor. Let’s start simple, with a proxy that intercepts all attempts to read and write to properties of an object.

Listing 8.7

Creating proxies with the Proxy constructor

The emperor is our target object.

const emperor = { name: "Komei" }; const representative = new Proxy(emperor, {

Creates a proxy with the Proxy constructor that takes in the object the proxy wraps... Using proxies to control access

get: (target, key) => { report("Reading " + key + " through a proxy"); return key in target ? target[key] : "Don't bother the emperor!"

}, set: (target, key, value) => { report("Writing " + key + " through a proxy"); target[key] = value; } });

211

...and an object with traps that will be called when reading (get) and writing (set) to properties.

Accesses the name property both through the emperor object and through the proxy object

assert(emperor.name === "Komei", "The emperor's name is Komei"); assert(representative.name === "Komei", Accessing a non"We can get the name property through a proxy"); existing property

directly on the object returns undefined.

assert(emperor.nickname === undefined, "The emperor doesn’t have a nickname "); assert(representative.nickname === "Don't bother the emperor!",

Accessing a property through a proxy detects that the object doesn’t exist in our target object, so a warning message is returned.

"The proxy jumps in when we make inproper requests");

representative.nickname = "Tenno"; assert(emperor.nickname === "Tenno",

"The emperor now has a nickname"); assert(representative.nickname === "Tenno",

"The nickname is also accessible through the proxy");

Adds a property through the proxy. The property is accessible both through the target object and through the proxy.

We first create our base emperor object that has only a name property. Next, by using the built-in Proxy constructor, we wrap our emperor object (or target object, as it’s commonly called) into a proxy object named representative. During proxy construction, as a second argument, we also send an object that specifies traps, functions that will be called when certain actions are performed on an object:

const representative = new Proxy(emperor, { get: (target, key) => { report("Reading " + key + " through a proxy"); return key in target ? target[key] : "Don't bother the emperor!"

}, set: (target, key, value) => { report("Writing " + key + " through a proxy"); target[key] = value; } });

In this case, we’ve specified two traps: a get trap that will be called whenever we try to read a value of a property through the proxy, and a set trap that will be called whenever we set a property value through the proxy. The get trap performs the following functionality: If the target object has a property, that property is returned; and if the 212

CHAPTER 8

Controlling access to objects

object doesn’t have a property, we return a message warning our user not to bother the emperor with frivolous details.

get: (target, key) => { report("Reading " + key + " through a proxy"); return key in target ? target[key] : "Don't bother the emperor!" }

Next, we test that we can access the name property both directly through the target emperor object as well as through our proxy object:

assert(emperor.name === "Komei", "The emperor's name is Komei"); assert(representative.name === "Komei", "We can get the name property through a proxy");

If we access the name property directly through the emperor object, the value Komei is returned. But if we access the name property through the proxy object, the get trap is implicitly called. Because the name property is found in the target emperor object, the value Komei is also returned. See figure 8.4.

It’s important to emphasize that proxy traps are activated in the same way as getters and setters. As soon as we perform an action (for example, accessing a property value on a proxy), the matching trap gets implicitly called, and the JavaScript engine goes through a similar process as if we’ve explicitly invoked a function.

NOTE

On the other hand, if we access a nonexisting nickname property directly on the target emperor object, we’ll get, unsurprisingly, an undefined value. But if we try to access it through our proxy object, the get handler will be activated. Because the target

emperor

name: "Komei"

emperor.name //"Komei"

Calling emperor.name directly accesses the name property of the emperor object.

representative

get

emperor

name: "Komei"

representative.name //"Komei"

Calling proxy.name calls the proxy’s get trap, which in this case simply returns the value of the name property of the emperor object.

Figure 8.4 Accessing the name property directly (on the left) and indirectly, through a proxy (on the right) Using proxies to control access

213

emperor object doesn’t have a nickname property, the proxy’s get trap will return the Don't bother the emperor! message.

We’ll continue the example by assigning a new property through our proxy object: representative.nickname = "Tenno". Because the assignment is done through a proxy, and not directly, the set trap, which logs a message and assigns a property to our target emperor object, is activated:

set: (target, key, value) => { report("Writing " + key + " through a proxy"); target[key] = value; }

Naturally, the newly created property can be accessed both through the proxy object and the target object:

assert(emperor.nickname === "Tenno", "The emperor now has a nickname"); assert(representative.nickname === "Tenno",

"The nickname is also accessible through the proxy");

This is the gist of how to use proxies: Through the Proxy constructor, we create a proxy object that controls access to the target object by activating certain traps, whenever an operation is performed directly on a proxy.

In this example, we’ve used the get and set traps, but many other built-in traps allow us to define handlers for various object actions (see http://mng.bz/ba55). For example:

■

■ ■ ■

The apply trap will be activated when calling a function, and the construct trap when using the new operator.

The get and set traps will be activated when reading/writing to a property.

The enumerate trap will be activated for for-in statements.

getPrototypeOf and setPrototypeOf will be activated for getting and setting the prototype value.

We can intercept many operations, but going through all of them is outside the scope of this book. For now, we turn our attention to a few operations that we can’t override: equality (== or ===), instanceof, and the typeof operator.

For example, the expression x == y (or a stricter x === y) is used to check whether x and y refer to identical objects (or are of the same value). This equality operator has some assumptions. For example, comparing two objects should always return the same value for the same two objects, which isn’t something that we can guarantee if that value is determined by a user-specified function. In addition, the act of comparing two objects shouldn’t give access to one of those objects, which would be the case if equality could be trapped. For similar reasons, the instanceof and the typeof operators can’t be trapped. 214

CHAPTER 8

Controlling access to objects

Now that we know how proxies work and how to create them, let’s explore some of their practical aspects, such as how to use proxies for logging, performance measurement, autopopulating properties, and implementing arrays that can be accessed with negative indexes. We’ll start with logging.

8.2.1 Using proxies for logging

One of the most powerful tools when trying to figure out how code works or when trying to get to the root of a nasty bug is logging, the act of outputting information that we find useful at a particular moment. We might, for example, want to know which functions are called, how long they’ve been executing, what properties are read or written to, and so on.

Unfortunately, when implementing logging, we usually scatter logging statements throughout the code. Take a look at the Ninja example used earlier in the chapter.

Listing 8.8

Logging without proxies

function Ninja() { let _skillLevel = 0;

Object.defineProperty(this, 'skillLevel', { get: () => { report("skillLevel get method is called"); return _skillLevel; }, set: value => { report("skillLevel set method is called"); _skillLevel = value; } });

We log whenever the skillLevel property is read...

...and whenever the skillLevel property is written to.

}

const ninja = new Ninja(); ninja.skillLevel; ninja.skillLevel = 4;

Reads the skillLevel property and triggers the get method

Writes to the skillLevel property and triggers the set method

We define a Ninja constructor function that adds a getter and a setter to the skill-Level property, which log all attempts of reading and writing to that property.

Notice that this isn’t an ideal solution. We’ve cluttered our domain code that deals with reading and writing to an object property with logging code. In addition, if in the future we need more properties on the ninja object, we have to be careful not to forget to add additional logging statements to each new property.

Luckily, one of the straightforward uses of proxies is to enable logging whenever we read or write to a property, but in a much nicer and cleaner way. Consider the following example. Using proxies to control access

215

Listing 8.9

Using proxies makes it easier to add logging to objects

Defines a function that takes a target object and makes it loggable

Creates a new proxy with that target object

Creates a new ninja object that will serve as our target object and make it loggable

function makeLoggable(target){

return new Proxy(target, { get: (target, property) => { report("Reading " + property); return target[property]; },

A get trap that logs property reads

set: (target, property, value) => { report("Writing value " + value + " to " + property); target[property] = value; } });

}

let ninja = { name: "Yoshi"}; ninja = makeLoggable(ninja);

A set trap that logs property writes

assert(ninja.name === "Yoshi", "Our ninja Yoshi"); ninja.weapon = "sword";

Reads and writes to our proxy object. These actions are logged by the proxy traps.

Here we define a makeLoggable function that takes a target object and returns a new Proxy that has a handler with a get and a set trap. These traps, besides reading and writing to the property, log the information about which property is read or written to.

Next, we create a ninja object with a name property, and we pass it to the makeLoggable function, in which it will be used as a target for a newly created proxy. We then assign the proxy back to the ninja identifier, overriding it. (Don’t worry, our original ninja object is kept alive as the target object of our proxy.)

Whenever we try to read a property (for example, with ninja.name), the get trap will be called, and the information about which property has been read will be logged. A similar thing will happen when writing to a property: ninja.weapon = "sword".

Notice how much easier and more transparent this is when compared to the standard way of using getters and setters. We don’t have to mix our domain code with our logging code, and there’s no need to add separate logging for each object property. Instead, all property reads and writes go through our proxy object trap methods. Logging has been specified in only one place and is reused as many times as necessary, on as many objects as necessary.

8.2.2 Using proxies for measuring performance

Besides being used for logging property accesses, proxies can be used for measuring the performance of function invocations, without even modifying the source code of a 216

CHAPTER 8

Controlling access to objects

function. Say we want to measure the performance of a function that calculates whether a number is a prime, as shown in the following listing.

Listing 8.10

Measuring performance with proxies

function isPrime(number){

if(number < 2) { return false; } for(let i = 2; i < number; i++) { if(number % i === 0) { return false; } } return true;

Defines a primitive implementation of the isPrime function

Wraps the isPrime function within a proxy

Starts a timer called isPrime

Stops the timer and outputs the result

} isPrime = new Proxy(isPrime, { Provides an apply trap that will

apply: (target, thisArg, args) => { be called whenever a proxy is

console.time("isPrime"); called as a function

const result = target.apply(thisArg, args); Invokes the target

console.timeEnd("isPrime"); function

return result;

} });

isPrime(1299827);

Calls the function. The call works the same as if we’d called the original function.

In this example, we have a simple isPrime function. (The exact function doesn’t matter; we’re using it as an example of a function whose execution can last a nontrivial amount of time.)

Now imagine that we need to measure the performance of the isPrime function, but without modifying its code. We could wrap the function into a proxy that has a trap that will be called whenever the function is called:

isPrime = new Proxy(isPrime, { apply: (target, thisArg, args) => { ...

} });

We use the isPrime function as the target object of a newly constructed proxy. In addition, we supply a handler with an apply trap that will be executed on function invocation.

Similarly, as in the previous example, we’ve assigned the newly created proxy to the isPrime identifier. In that way, we don’t have to change any of the code that calls the function whose execution time we want to measure; the rest of the program code is completely oblivious to our changes. (How’s that for some ninja stealth action?) Using proxies to control access

217

Whenever the isPrime function is called, that call is rerouted to our proxy’s apply trap, which will start a stopwatch with the built-in console.time method (remember chapter 1), call the original isPrime function, log the elapsed time, and finally return the result of the isPrime invocation.

8.2.3 Using proxies to autopopulate properties

In addition to simplifying logging, proxies can be used for autopopulating properties. For example, imagine that you have to model your computer’s folder structure, in which a folder object can have properties that can also be folders. Now imagine that you have to model a file at the end of a long path, such as this:

rootFolder.ninjasDir.firstNinjaDir.ninjaFile = "yoshi.txt";

To create this, you might write something along the following lines:

const rootFolder = new Folder(); rootFolder.ninjasDir = new Folder(); rootFolder.ninjasDir.firstNinjaDir = new Folder(); rootFolder.ninjasDir.firstNinjaDir.ninjaFile = "yoshi.txt";

Seems a tad more tedious than necessary, doesn’t it? This is where autopopulating properties comes into play; just take a look at the following example.

Listing 8.11

Autopopulating properties with proxies

function Folder() {

return new Proxy({}, { get: (target, property) => { report("Reading " + property);

Logs all readings to our object

if(!(property in target)) { target[property] = new Folder(); } return target[property];

If the accessed property doesn’t exist, we create it.

} });

}

const rootFolder = new Folder();

Whenever a property is accessed, the get trap, which creates a property if it doesn’t exist, is activated.

try { rootFolder.ninjasDir.firstNinjaDir.ninjaFile = "yoshi.txt"; pass("An exception wasn’t raised"); } No exception will be raised. catch(e){

fail("An exception has occurred"); } 218

CHAPTER 8

Controlling access to objects

Normally, if we consider only the following code, we’d expect an exception to be raised:

const rootFolder = new Folder(); rootFolder.ninjasDir.firstNinjaDir.ninjaFile = "yoshi.txt";

We’re accessing a property, firstNinjaDir, of an undefined property, ninjasDir, of the rootFolder object. But if we run the code, you see that all is well, as shown in figure 8.5.

This happens because we’re using proxies. Every time we access a property, the proxy get trap is activated. If our folder object already contains the requested property, its value is returned, and if it doesn’t, a new folder is created and assigned to the property. This is how two of our properties, ninjasDir and firstNinjaDir, are created. Requesting a value of an uninitialized property triggers its creation.

Figure 8.5 ing 8.11

The output of running the code from list-

Finally, we have a tool for ridding ourselves of some cases of the pesky null exception!

8.2.4 Using proxies to implement negative array indexes

In our day-to-day programming, we’ll usually work with a lot of arrays. Let’s explore how to take advantage of proxies to make our dealings with arrays a little more pleasant.

If your programming background is from languages such as Python, Ruby, or Perl, you might be used to negative array indexes, which enable you to use negative indexes to access array items from the back, as shown in the following snippet:

const ninjas = ["Yoshi", "Kuma", "Hattori"];

ninjas[0]; //"Yoshi" ninjas[1]; //"Kuma" ninjas[2]; //"Hattori"

ninjas[-1]; //"Hattori" ninjas[-2]; //"Kuma" ninjas[-3]; //"Yoshi"

Standard access to array items, with positive array indexes

Negative array indexes enable us to access array items from the back, starting with –1, which accesses the last array item.

Now compare the code that we normally use to access the last item in the array, ninjas [ninjas.length-1], with the code that we can use if our language of choice supports negative array indexes, ninjas[-1]. See how much more elegant this is?

Unfortunately, JavaScript doesn’t offer built-in support for negative array indexes, but we can mimic this ability through proxies. To explore this concept, we’ll look at a Using proxies to control access

219

slightly simplified version of code written by Sindre Sorhus (https://github.com/ sindresorhus/negative-array), as shown in the following listing.

Listing 8.12

Negative array indexes with proxies

If our target object isn’t an array, throw an exception.

Returns a new proxy that takes in the array and uses it as a proxy target

If the read index is a negative number, read from the back of the array, and if it’s a positive number, access it normally.

function createNegativeArrayProxy(array){

if (!Array.isArray(array)) { throw new TypeError('Expected an array'); }

The get trap is activated whenever an array index is read.

Turns the property name into a number with the unary plus operator

return new Proxy(array, { get: (target, index) => { index = +index; return target[index < 0 ? target.length + index : index]; }, set: (target, index, val) => { The set trap is activated whenever an array index is written to. index = +index; return target[index < 0 ? target.length + index : index] = val; } });

}

Creates a standard array

const ninjas = ["Yoshi", "Kuma", "Hattori"]; const proxiedNinjas = createNegativeArrayProxy(ninjas);

assert(ninjas[0] === "Yoshi" && ninjas[1] === "Kuma"

Checks that we can access array items through the original array as well as through the proxy

Passes it into our function that will create a proxy to that array

&&

ninjas[2]

===

"

Hattori"

,

"Array items accessed through positive indexes");

assert(proxiedNinjas[0] === "Yoshi" && proxiedNinjas[1] === "Kuma"

&& proxiedNinjas [2] === "Hattori", "Array items accessed through positive indexes on a proxy");

assert(typeof ninjas[-1] === "undefined" && typeof ninjas[-2] === "undefined"

&& typeof ninjas[-3] === "undefined",

Checks that we can’t access array items through negative indexes in a standard array...

"Items cannot be accessed through negative indexes on an array");

assert(proxiedNinjas[-1] === "Hattori"

&& proxiedNinjas[-2] === "Kuma"

&& proxiedNinjas[-3] === "Yoshi",

...but that we can do it through our proxy, because we’ve supplied a get trap that handles the case.

"But they can be accessed through negative indexes");

proxiedNinjas[-1] = "Hachi";

assert(proxiedNinjas[-1] === "Hachi" && ninjas[2] === "Hachi",

"Items can be changed through negative indexes");

We can also modify array items from the back, but only if we go through the proxy. 220

CHAPTER 8

Controlling access to objects

In this example, we define a function that will create a proxy for a passed-in array. Because we don’t want our proxy to work with other types of objects, we throw an exception in case the argument isn’t an array:

if (!Array.isArray(array)) { throw new TypeError('Expected an array'); }

We continue by creating and returning a new proxy with two traps, a get trap that will activate whenever we try to read an array item, and a set trap that will activate whenever we write to an array item:

return new Proxy(array, { get: (target, index) => { index = +index; return target[index < 0 ? target.length + index : index]; }, set: (target, index, val) => { index = +index; return target[index < 0 ? target.length + index : index] = val; } });

The trap bodies are similar. First, we turn the property into a number by using the unary plus operator (index = +index). Then, if the requested index is less than 0, we access array items from the back by anchoring to the length of the array, and if it’s greater than or equal to 0, we access the array item in a standard fashion.

Finally, we perform various tests to check that on normal arrays we can only access array items through positive array indexes, and that, if we use a proxy, we can both access and modify array items through negative indexes.

Now that you’ve seen how to use proxies to achieve some interesting features such as autopopulating object properties and accessing negative array indexes, which are outright impossible without proxies, let’s explore the most significant downside to proxies: performance issues.

8.2.5 Performance costs of proxies

As we already know, a proxy is a surrogate object through which we control access to another object. A proxy can define traps, functions that will be executed whenever a certain operation is performed on a proxy. And, as you’ve also seen, we can use these traps to implement useful functionalities such as logging, performance measurements, autopopulating properties, negative array indexes, and so on. Unfortunately, there’s also a downside. The fact that all our operations have to pass in through the proxy adds a layer of indirection that enables us to implement all these cool features, but at the same time it introduces a significant amount of additional processing that impacts performance. Summary

221

To test these performance issues, we can build on the negative array indexes example from listing 8.12 and compare the execution time when accessing items in a normal array versus accessing items through a proxy, as shown in the following listing.

Listing 8.13

Checking the performance limitations of proxies

function measure(items){ const startTime = new Date().getTime();

for(let i = 0; i < 500000; i++){

Accesses the items in our collection in a long-running loop

Measures the time it took for the long-running code to execute

Compares the running time when accessing the standard array versus when accessing through a proxy

items[0] === "Yoshi";

items[1] === "Kuma";

items[2] === "Hattori";

Gets the current time before running a long-running operation

} return new Date().getTime() - startTime;

}

const ninjas = ["Yoshi", "Kuma", "Hattori"];

const proxiedNinjas = createNegativeArrayProxy(ninjas);

console.log("Proxies are around",

Math.round(measure(proxiedNinjas)/ measure(ninjas)), "times slower");

Creates a standard array and a proxy for that array

Because a single operation of the code happens much too quickly to measure reliably, the code has to be executed many times to get a measurable value. Frequently, this count can be in the tens of thousands, or even millions, depending on the nature of the code being measured. A little trial and error lets us choose a reasonable value: in this case 500,000.

We also need to bracket the execution of the code with two new Date().getTime() timestamps: one before we start executing the target code, and one after. Their difference tells us how long the code took to perform. Finally, we can compare the results by calling the measure function on both the proxied array and the standard array.

On our machine, the results don’t fare well for proxies. It turns out that in Chrome, proxies are around 50 times slower; in Firefox, they’re about 20 times slower.

For now, we recommend that you be careful when using proxies. Although they allow you to be creative with controlling access to objects, that amount of control comes with performance issues. You can use proxies with code that’s not performance sensitive, but be careful when using them in code that’s executed a lot. As always, we recommend that you thoroughly test the performance of your code.

## 8.3 Summary

1. We can monitor our objects with getters, setters, and proxies.

2. By using accessor methods (getters and setters), we can control access to object properties.

    – Accessor properties can be defined by using the built-in Object.defineProperty method or with a special get and set syntax as parts of object literals or ES6 classes.

    – A get method is implicitly called whenever we try to read, whereas a set method is called whenever we assign a value to the matching object’s property.

    – Getter methods can be used to define computed properties, properties whose value is calculated on a per request basis, whereas setter methods can be used to achieve data validation and logging.

3. Proxies are an ES6 addition to JavaScript and are used to control other objects.

    – Proxies enable us to define custom actions that will be executed when an object is interacted with (for example, when a property is read or a function is called).

    – All interactions have to go through the proxy, which has traps that are triggered when a specific action occurs.

4. Use proxies to achieve elegant.

    – Logging.

    – Performance measurements.

    – Data validation.

    – Autopopulating object properties (thereby avoiding pesky null exceptions).

    – Negative array indexes. 

5. Proxies aren’t fast, so be careful when using them in code that’s executed a lot. We recommend that you do performance testing.
