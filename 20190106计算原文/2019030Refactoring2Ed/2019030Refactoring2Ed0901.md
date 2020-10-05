# 0901. Organizing Data

Data structures play an important role in our programs, so it’s no great shock that I Tutorialshave a clutch of refactorings that focus on them. A value that’s used for different purposes is a breeding ground for confusion and bugs—so, when I see one, I use Split Offers Variable & Deals (240) to separate the usages. As with any program element, getting a variable’s name right is tricky and important, so Rename Variable (137) is often my Highlights friend. But sometimes the best thing I can do with a variable is to get rid of it completely—with Replace Derived Variable with Query (248).

Settings

I often find problems in a code base due to a confusion between references and values, Support so I use Change Reference to Value (252) and Change Value to Reference (256) to change between these styles.

Sign Out

SPLIT VARIABLE

formerly: Remove Assignments to Parameters

formerly: Split Temp Motivation

Variables have various uses. Some of these uses naturally lead to the variable being assigned to several times. Loop variables change for each run of a loop (such as the i in for (let i=0; i<10; i++)). Collecting variables store a value that is built up during the method.

Many other variables are used to hold the result of a long­winded bit of code for easy reference later. These kinds of variables should be set only once. If they are set more than once, it is a sign that they have more than one responsibility within the method. Any variable with more than one responsibility should be replaced with multiple variables, one for each responsibility. Using a variable for two different things is very confusing for the reader.

Mechanics

Change the name of the variable at its declaration and first assignment.

If the later assignments are of the form i = i + something, that is a collecting variable, so don’t split it. A collecting variable is often used for calculating sums, string concatenation, writing to a stream, or adding to a collection.

If possible, declare the new variable as immutable.

Change all references of the variable up to its second assignment. Test.

Repeat in stages, at each stage renaming the variable at the declaration and changing references until the next assignment, until you reach the final assignment.

Example

For this example, I compute the distance traveled by a haggis. From a standing start, a haggis experiences an initial force. After a delay, a secondary force kicks in to further accelerate the haggis. Using the common laws of motion, I can compute the distance traveled as follows:

Click here to view code image

function distanceTravelled (scenario, time) {

let result; let acc = scenario.primaryForce / scenario.mass; let primaryTime = Math.min(time, scenario.delay); result = 0.5 * acc * primaryTime * primaryTime; let secondaryTime = time ­ scenario.delay; if (secondaryTime > 0) {

let primaryVelocity = acc * scenario.delay;

acc = (scenario.primaryForce + scenario.secondaryForce) / scenario.mass;

result += primaryVelocity * secondaryTime + 0.5 * acc * secondaryTime * seco } return result;

}

A nice awkward little function. The interesting thing for our example is the way the variable acc is set twice. It has two responsibilities: one to hold the initial acceleration from the first force and another later to hold the acceleration from both forces. I want to split this variable.

When trying to understand how a variable is used, it’s handy if my editor can highlight all occurrences of a symbol within a function or file. Most modern editors can do this pretty easily.

I start at the beginning by changing the name of the variable and declaring the new name as const. Then, I change all references to the variable from that point up to the next assignment. At the next assignment, I declare it:

Click here to view code image function distanceTravelled (scenario, time) {

let result; const primaryAcceleration = scenario.primaryForce / scenario.mass; let primaryTime = Math.min(time, scenario.delay); result = 0.5 * primaryAcceleration * primaryTime * primaryTime; let secondaryTime = time ­ scenario.delay; if (secondaryTime > 0) {

let primaryVelocity = primaryAcceleration * scenario.delay;

let acc = (scenario.primaryForce + scenario.secondaryForce) / scenario.mass;

result += primaryVelocity * secondaryTime + 0.5 * acc * secondaryTime * seco } return result;

}

I choose the new name to represent only the first use of the variable. I make it const to ensure it is only assigned once. I can then declare the original variable at its second assignment. Now I can compile and test, and all should work.

I continue on the second assignment of the variable. This removes the original variable name completely, replacing it with a new variable named for the second use.

Click here to view code image

function distanceTravelled (scenario, time) {

let result; const primaryAcceleration = scenario.primaryForce / scenario.mass; let primaryTime = Math.min(time, scenario.delay); result = 0.5 * primaryAcceleration * primaryTime * primaryTime; let secondaryTime = time ­ scenario.delay; if (secondaryTime > 0) {

let primaryVelocity = primaryAcceleration * scenario.delay;

const secondaryAcceleration = (scenario.primaryForce + scenario.secondaryFor

result += primaryVelocity * secondaryTime +

0.5 * secondaryAcceleration * secondaryTime * secondaryTime; } return result;

}

I’m sure you can think of a lot more refactoring to be done here. Enjoy it. (I’m sure it’s better than eating the haggis—do you know what they put in those things?)

Example: Assigning to an Input Parameter

Another case of splitting a variable is where the variable is declared as an input parameter. Consider something like Click here to view code image

function discount (inputValue, quantity) { if (inputValue > 50) inputValue = inputValue ­ 2; if (quantity > 100) inputValue = inputValue ­ 1; return inputValue; }

Here inputValue is used both to supply an input to the function and to hold the result for the caller. (Since JavaScript has call­by­value parameters, any modification of inputValue isn’t seen by the caller.)

In this situation, I would split that variable.

Click here to view code image

function discount (originalInputValue, quantity) { let inputValue = originalInputValue; if (inputValue > 50) inputValue = inputValue ­ 2; if (quantity > 100) inputValue = inputValue ­ 1; return inputValue; }

I then perform Rename Variable (137) twice to get better names.

Click here to view code image

function discount (inputValue, quantity) { let result = inputValue; if (inputValue > 50) result = result ­ 2; if (quantity > 100) result = result ­ 1; return result; }

You’ll notice that I changed the second line to use inputValue as its data source. Although the two are the same, I think that line is really about applying the modification to the result value based on the original input value, not the (coincidentally same) value of the result accumulator.

RENAME FIELD Motivation

Names are important, and field names in record structures can be especially important when those record structures are widely used across a program. Data structures play a particularly important role in understanding. Many years ago Fred Brooks said, “Show me your flowcharts and conceal your tables, and I shall continue to be mystified. Show me your tables, and I won’t usually need your flowcharts; they’ll be obvious.” While I don’t see many people drawing flowcharts these days, the adage remains valid. Data structures are the key to understanding what’s going on.

Since these data structures are so important, it’s essential to keep them clear. Like anything else, my understanding of data improves the more I work on the software, so it’s vital that this improved understanding is embedded into the program.

You may want to rename a field in a record structure, but the idea also applies to classes. Getter and setter methods form an effective field for users of the class. Renaming them is just as important as with bare record structures.

Mechanics

If the record has limited scope, rename all accesses to the field and test; no need to do the rest of the mechanics.

If the record isn’t already encapsulated, apply Encapsulate Record (162).

Rename the private field inside the object, adjust internal methods to fit.

Test. If the constructor uses the name, apply Change Function Declaration (124) to rename it.

Apply Rename Function (124) to the accessors.

Example: Renaming a Field

I’ll start with a constant.

Click here to view code image

const organization = {name: "Acme Gooseberries", country: "GB"};

I want to change “name” to “title”. The object is widely used in the code base, and there are updates to the title in the code. So my first move is to apply Encapsulate Record (162).

Click here to view code image

class Organization { constructor(data) {

this._name = data.name;

this._country = data.country;

} get name() get country()

{return this._name;} {return this._country;}

set name(aString) {this._name = aString;}

set country(aCountryCode) {this._country = aCountryCode;}

} const organization = new Organization({name: "Acme Gooseberries", country: "GB"}

Now that I’ve encapsulated the record structure into the class, there are four places I need to look at for renaming: the getting function, the setting function, the constructor, and the internal data structure. While that may sound like I’ve increased my workload, it actually makes my work easier since I can now change these independently instead of all at once, taking smaller steps. Smaller steps mean fewer things to go wrong in each step—therefore, less work. It wouldn’t be less work if I never made mistakes—but not making mistakes is a fantasy I gave up on a long time ago.

Since I’ve copied the input data structure into the internal data structure, I need to separate them so I can work on them independently. I can do this by defining a separate field and adjusting the constructor and accessors to use it.

class Organization…

Click here to view code image

class Organization { constructor(data) {

this._title = data.name;

this._country = data.country;

} get name()

{return this._title;}

set name(aString) {this._title = aString;}

get country()

{return this._country;}

set country(aCountryCode) {this._country = aCountryCode;}

}

Next, I add support for using “title” in the constructor.

class Organization…

Click here to view code image

class Organization {

constructor(data) { this._title = (data.title !== undefined) ? data.title : data.name;

this._country = data.country;

} get name()

{return this._title;}

set name(aString) {this._title = aString;}

get country()

{return this._country;}

set country(aCountryCode) {this._country = aCountryCode;}

}

Now, callers of my constructor can use either name or title (with title taking precedence). I can now go through all constructor callers and change them one­by­one to use the new name.

Click here to view code image

const organization = new Organization({title: "Acme Gooseberries", country: "GB"

Once I’ve done all of them, I can remove the support for the name. class Organization…

Click here to view code image

class Organization { constructor(data) {

this._title = data.title;

this._country = data.country;

} get name()

{return this._title;}

set name(aString) {this._title = aString;}

get country()

{return this._country;}

set country(aCountryCode) {this._country = aCountryCode;}

}

Now that the constructor and data use the new name, I can change the accessors, which is as simple as applying Rename Function (124) to each one.

class Organization…

Click here to view code image

class Organization { constructor(data) {

this._title = data.title;

this._country = data.country;

} get title()

{return this._title;}

set title(aString) {this._title = aString;}

get country()

{return this._country;}

set country(aCountryCode) {this._country = aCountryCode;}

}

I’ve shown this process in its most heavyweight form needed for a widely used data structure. If it’s being used only locally, as in a single function, I can probably just rename the various properties in one go without doing encapsulation. It’s a matter of judgment when to apply to the full mechanics here—but, as usual with refactoring, if my tests break, that’s a sign I need to use the more gradual procedure.

Some languages allow me to make a data structure immutable. In this case, rather than encapsulating it, I can copy the value to the new name, gradually change the users, then remove the old name. Duplicating data is a recipe for disaster with mutable data structures; removing such disasters is why immutable data is so popular.

REPLACE DERIVED VARIABLE WITH QUERY REPLACE DERIVED VARIABLE WITH QUERY

Motivation

One of the biggest sources of problems in software is mutable data. Data changes can often couple together parts of code in awkward ways, with changes in one part leading to knock­on effects that are hard to spot. In many situations it’s not realistic to entirely remove mutable data—but I do advocate minimizing the scope of mutable data at much as possible.

One way I can make a big impact is by removing any variables that I could just as easily calculate. A calculation often makes it clearer what the meaning of the data is, and it is protected from being corrupted when you fail to update the variable as the source data changes.

A reasonable exception to this is when the source data for the calculation is immutable and we can force the result to being immutable too. Transformation operations that create new data structures are thus reasonable to keep even if they could be replaced with calculations. Indeed, there is a duality here between objects that wrap a data structure with a series of calculated properties and functions that transform one data structure into another. The object route is clearly better when the source data changes and you would have to manage the lifetime of the derived data structures. But if the source data is immutable, or the derived data is very transient, then both approaches are effective.

Mechanics Identify all points of update for the variable. If necessary, use Split Variable (240) to separate each point of update.

Create a function that calculates the value of the variable.

Use Introduce Assertion (302) to assert that the variable and the calculation give the same result whenever the variable is used.

If necessary, use Encapsulate Variable (132) to provide a home for the assertion. Test.

Replace any reader of the variable with a call to the new function.

Test.

Apply Remove Dead Code (237) to the declaration and updates to the variable.

Example

Here’s a small but perfectly formed example of ugliness: class ProductionPlan…

Click here to view code image

get production() {return this._production;} applyAdjustment(anAdjustment) {

this._adjustments.push(anAdjustment);

this._production += anAdjustment.amount; }

Ugliness is in the eye of beholder; here, I see ugliness in duplication—not the common duplication of code but duplication of data. When I apply an adjustment, I’m not just storing that adjustment but also using it to modify an accumulator. I can just calculate that value, without having to update it.

But I’m a cautious fellow. It is my hypothesis is that I can just calculate it—I can test that hypothesis by using Introduce Assertion (302):

class ProductionPlan…

Click here to view code image get production() { assert(this._production === this.calculatedProduction); return this._production; }

get calculatedProduction() { return this._adjustments .reduce((sum, a) => sum + a.amount, 0); }

With the assertion in place, I run my tests. If the assertion doesn’t fail, I can replace returning the field with returning the calculation:

class ProductionPlan…

Click here to view code image

get production() {

assert(this._production === this.calculatedProduction); return this.calculatedProduction;

}

Then Inline Function (115):

class ProductionPlan…

Click here to view code image

get production() { return this._adjustments .reduce((sum, a) => sum + a.amount, 0); }

I clean up any references to the old variable with Remove Dead Code (237):

class ProductionPlan…

Click here to view code image

applyAdjustment(anAdjustment) { this._adjustments.push(anAdjustment);

this._production += anAdjustment.amount;

}

Example: More Than One Source Example: More Than One Source

The above example is nice and easy because there’s clearly a single source for the value of production. But sometimes, more than one element can combine in the accumulator.

class ProductionPlan…

Click here to view code image

constructor (production) { this._production = production; this._adjustments = []; } get production() {return this._production;} applyAdjustment(anAdjustment) {

this._adjustments.push(anAdjustment);

this._production += anAdjustment.amount; }

If I do the same Introduce Assertion (302) that I did above, it will now fail for any case where the initial value of the production isn’t zero.

But I can still replace the derived data. The only difference is that I must first apply Split Variable (240).

Click here to view code image

constructor (production) { this._initialProduction = production; this._productionAccumulator = 0; this._adjustments = []; } get production() {

return this._initialProduction + this._productionAccumulator; }

Now I can Introduce Assertion (302):

class ProductionPlan…

Click here to view code image

get production() { assert(this._productionAccumulator === this.calculatedProductionAccumulator); return this._initialProduction + this._productionAccumulator;

}

get calculatedProductionAccumulator() { return this._adjustments .reduce((sum, a) => sum + a.amount, 0); }

and continue pretty much as before. I’d be inclined, however, to leave totalProductionAjustments as its own property, without inlining it.

CHANGE REFERENCE TO VALUE

inverse of: Change Value to Reference (256)

Motivation

When I nest an object, or data structure, within another I can treat the inner object as a reference or as a value. The difference is most obviously visible in how I handle updates of the inner object’s properties. If I treat it as a reference, I’ll update the inner object’s property keeping the same inner object. If I treat it as a value, I will replace the entire inner object with a new one that has the desired property.

If I treat a field as a value, I can change the class of the inner object to make it a Value Object [ mf­vo]. Value objects are generally easier to reason about, particularly because they are immutable. In general, immutable data structures are easier to deal with. I can pass an immutable data value out to other parts of the program and not worry that it might change without the enclosing object being aware of the change. I can replicate values around my program and not worry about maintaining memory links. Value objects are especially useful in distributed and concurrent systems.

This also suggests when I shouldn’t do this refactoring. If I want to share an object between several objects so that any change to the shared object is visible to all its collaborators, then I need the shared object to be a reference.

Mechanics

Check that the candidate class is immutable or can become immutable.

For each setter, apply Remove Setting Method (331).

Provide a value­based equality method that uses the fields of the value object.

Most language environments provide an overridable equality function for this purpose. Usually you must override a hashcode generator method as well.

Example

Imagine we have a person object that holds onto a crude telephone number.

class Person…

Click here to view code image

constructor() { this._telephoneNumber = new TelephoneNumber(); } get officeAreaCode() {return this._telephoneNumber.areaCode;} get officeNumber() {return this._telephoneNumber.number;}

set officeAreaCode(arg) {this._telephoneNumber.areaCode = arg;}

set officeNumber(arg) {this._telephoneNumber.number = arg;}

class TelephoneNumber…

Click here to view code image

get areaCode()

{return this._areaCode;}

set areaCode(arg) {this._areaCode = arg;} get number()

{return this._number;}

set number(arg) {this._number = arg;}

This situation is the result of an Extract Class (182) where the old parent still holds update methods for the new object. This is a good time to apply Change Reference to Value since there is only one reference to the new class.

The first thing I need to do is to make the telephone number immutable. I do this by applying Remove Setting Method (331) to the fields. The first step of Remove Setting Method (331) is to use Change Function Declaration (124) to add the two fields to the constructor and enhance the constructor to call the setters.

class TelephoneNumber…

Click here to view code image

constructor(areaCode, number) { this._areaCode = areaCode; this._number = number; }

Now I look at the callers of the setters. For each one, I need to change it to a reassignment. I start with the area code.

class Person…

Click here to view code image

get officeAreaCode() {return this._telephoneNumber.areaCode;} set officeAreaCode(arg) { this._telephoneNumber = new TelephoneNumber(arg, this.officeNumber); } get officeNumber() {return this._telephoneNumber.number;}

set officeNumber(arg) {this._telephoneNumber.number = arg;}

I then repeat that step with the remaining field.

class Person…

Click here to view code image

get officeAreaCode()

{return this._telephoneNumber.areaCode;} set officeAreaCode(arg) { this._telephoneNumber = new TelephoneNumber(arg, this.officeNumber); } get officeNumber() {return this._telephoneNumber.number;} set officeNumber(arg) {

this._telephoneNumber = new TelephoneNumber(this.officeAreaCode, arg); }

Now the telephone number is immutable, it is ready to become a true value. The citizenship test for a value object is that it uses value­based equality. This is an area where JavaScript falls down, as there is nothing in the language and core libraries that understands replacing a reference­based equality with a value­based one. The best I can do is to create my own equals method.

class TelephoneNumber…

Click here to view code image

equals(other) {

if (!(other instanceof TelephoneNumber)) return false; return this.areaCode === other.areaCode &&

this.number === other.number;

}

It’s also important to test it with something like

Click here to view code image

it('telephone equals', function() { assert( new TelephoneNumber("312", "555­0142") .equals(new TelephoneNumber("312", "555­0142"))); });

The unusual formatting I use here should make it obvious that they are the same constructor call.

The vital thing I do in the test is create two independent objects and test that they match as equal.

In most object­oriented languages, there is a built­in equality test that is supposed to be overridden for value­based equality. In Ruby, I can override the == operator; in Java, I override the Object.equals() method. And whenever I override an equality method, I usually need to override a hashcode generating method too (e.g., Object.hashCode() in Java) to ensure collections that use hashing work properly with my new value.

If the telephone number is used by more than one client, the procedure is still the same. As I apply Remove Setting Method (331), I’ll be modifying several clients instead of just one. Tests for non­equal telephone numbers, as well as comparisons to non­telephonenumbers and null values, are also worthwhile.

CHANGE VALUE TO REFERENCE

inverse of: Change Reference to Value (252)

Motivation

A data structure may have several records linked to the same logical data structure. I might read in a list of orders, some of which are for the same customer. When I have sharing like this, I can represent it by treating the customer either as a value or as a reference. With a value, the customer data is copied into each order; with a reference, there is only one data structure that multiple orders link to.

If the customer never needs to be updated, then both approaches are reasonable. It is, perhaps, a bit confusing to have multiple copies of the same data, but it’s common enough to not be a problem. In some cases, there may be issues with memory due to multiple copies—but, like any performance issue, that’s relatively rare.

The biggest difficulty in having physical copies of the same logical data occurs when I need to update the shared data. I then have to find all the copies and update them all. If I miss one, I’ll get a troubling inconsistency in my data. In this case, it’s often worthwhile to change the copied data into a single reference. That way, any change is visible to all the customer’s orders.

Changing a value to a reference results in only one object being present for an entity, and it usually means I need some kind of repository where I can access these objects. I then only create the object for an entity once, and everywhere else I retrieve it from the repository.

Mechanics

Create a repository for instances of the related object (if one isn’t already present).

Ensure the constructor has a way of looking up the correct instance of the related object.

Change the constructors for the host object to use the repository to obtain the related object. Test after each change.

Example

I’ll begin with a class that represents orders, which I might create from an incoming JSON document. Part of the order data is a customer ID from which I’m creating a customer object.

class Order…

Click here to view code image

constructor(data) { this._customer = new Customer(data.customer); // load other data } get customer() {return this._customer;}

this._number = data.number;

class Customer…

constructor(id) { this._id = id; } get id() {return this._id;} The customer object I create this way is a value. If I have five orders that refer to the customer ID of 123, I’ll have five separate customer objects. Any change I make to one of them will not be reflected in the others. Should I want to enrich the customer objects, perhaps by gathering data from a customer service, I’d have to update all five customers with the same data. Having duplicate objects like this always makes me nervous—it’s confusing to have multiple objects representing the same entity, such as a customer. This problem is particularly awkward if the customer object is mutable, which can lead to inconsistencies between the customer objects.

If I want to use the same customer object each time, I’ll need a place to store it. Exactly where to store entities like this will vary from application to application, but for a simple case I like to use a repository object [ mf­repos].

Click here to view code image

let _repositoryData;

export function initialize() { _repositoryData = {}; _repositoryData.customers = new Map(); }

export function registerCustomer(id) { if (! _repositoryData.customers.has(id)) _repositoryData.customers.set(id, new Customer(id)); return findCustomer(id); }

export function findCustomer(id) { return _repositoryData.customers.get(id); }

The repository allows me to register customer objects with an ID and ensures I only create one customer object with the same ID. With this in place, I can change the order’s constructor to use it.

Often, when doing this refactoring, the repository already exists, so I can just use it.

The next step is to figure out how the constructor for the order can obtain the correct customer object. In this case it’s easy, since the customer’s ID is present in the input data stream.

class Order…

Click here to view code image

constructor(data) {

this._number = data.number;

this._customer = registerCustomer(data.customer); // load other data

} get customer() {return this._customer;}

Now, any changes I make to the customer of one order will be synchronized across all the orders sharing the same customer.

For this example, I created a new customer object with the first order that referenced it. Another common approach is to get a list of customers, populate the repository with them, and then link to them as I read the orders. In that case, an order that contains a customer ID not in the repository would indicate an error.

One problem with this code is that the constructor body is coupled to the global repository. Globals should be treated with care—like a powerful drug, they can be beneficial in small doses but a poison if used too much. If I’m concerned about it, I can pass the repository as a parameter to the constructor.