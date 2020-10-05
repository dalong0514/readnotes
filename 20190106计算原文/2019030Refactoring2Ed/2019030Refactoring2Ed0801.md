# 0801. Moving Features

So far, the refactorings have been about creating, removing, and renaming program Tutorialselements. Another important part of refactoring is moving elements between contexts. I use Move Function (198) to move functions between classes and other modules. Fields Offers can & Deals move too, with Move Field (207).

I Highlights also move individual statements around. I use Move Statements into Function (213) and Move Statements to Callers (217) to move them in or out of functions, as well as SettingsSlide Statements (223) to move them within a function. Sometimes, I can take some

statements that match an existing function and use Replace Inline Code with Function Support Call (222) to remove the duplication.

Sign Two Out refactorings I often do with loops are Split Loop (227), to ensure a loop does only

one thing, and Replace Loop with Pipeline (231) to get rid of a loop entirely.

And then there’s the favorite refactoring of many a fine programmer: Remove Dead Code (237). Nothing is as satisfying as applying the digital flamethrower to superfluous

statements.

MOVE FUNCTION

formerly: Move Method Motivation

The heart of a good software design is its modularity—which is my ability to make most modifications to a program while only having to understand a small part of it. To get this modularity, I need to ensure that related software elements are grouped together and the links between them are easy to find and understand. But my understanding of how to do this isn’t static—as I better understand what I’m doing, I learn how to best group together software elements. To reflect that growing understanding, I need to move elements around.

All functions live in some context; it may be global, but usually it’s some form of a module. In an object­oriented program, the core modular context is a class. Nesting a function within another creates another common context. Different languages provide varied forms of modularity, each creating a context for a function to live in.

One of the most straightforward reasons to move a function is when it references elements in other contexts more than the one it currently resides in. Moving it together with those elements often improves encapsulation, allowing other parts of the software to be less dependent on the details of this module.

Similarly, I may move a function because of where its callers live, or where I need to call it from in my next enhancement. A function defined as a helper inside another function may have value on its own, so it’s worth moving it to somewhere more accessible. A method on a class may be easier for me to use if shifted to another.

Deciding to move a function is rarely an easy decision. To help me decide, I examine the current and candidate contexts for that function. I need to look at what functions call this one, what functions are called by the moving function, and what data that function uses. Often, I see that I need a new context for a group of functions and create one with Combine Functions into Class (144) or Extract Class (182). Although it can be difficult to decide where the best place for a function is, the more difficult this choice, often the less it matters. I find it valuable to try working with functions in one context, knowing I’ll learn how well they fit, and if they don’t fit I can always move them later.

Mechanics

Examine all the program elements used by the chosen function in its current context. Consider whether they should move too.

If I find a called function that should also move, I usually move it first. That way, moving a clusters of functions begins with the one that has the least dependency on the others in the group.

If a high­level function is the only caller of subfunctions, then you can inline those functions into the high­level method, move, and reextract at the destination.

Check if the chosen function is a polymorphic method.

If I’m in an object­oriented language, I have to take account of super­ and subclass declarations.

Copy the function to the target context. Adjust it to fit in its new home.

If the body uses elements in the source context, I need to either pass those elements as parameters or pass a reference to that source context.

Moving a function often means I need to come up with a different name that works better in the new context.

Perform static analysis.

Figure out how to reference the target function from the source context.

Turn the source function into a delegating function.

Test.

Consider Inline Function (115) on the source function.

The source function can stay indefinitely as a delegating function. But if its callers can just as easily reach the target directly, then it’s better to remove the middle man.

Example: Moving a Nested Function to Top Level Example: Moving a Nested Function to Top Level

I’ll begin with a function that calculates the total distance for a GPS track record. Click here to view code image

function trackSummary(points) {

const totalTime = calculateTime(); const totalDistance = calculateDistance(); const pace = totalTime / 60 / totalDistance ; return {

time: totalTime,

distance: totalDistance,

pace: pace };

function calculateDistance() { let result = 0;

for (let i = 1; i < points.length; i++) {

result += distance(points[i­1], points[i]);

} return result;

}

function distance(p1,p2) { ... } function radians(degrees) { ... } function calculateTime() { ... }

}

I’d like to move calculateDistance to the top level so I can calculate distances for tracks without all the other parts of the summary.

I begin by copying the function to the top level.

Click here to view code image

function trackSummary(points) {

const totalTime = calculateTime(); const totalDistance = calculateDistance(); const pace = totalTime / 60 / totalDistance ; return {

time: totalTime,

distance: totalDistance,

pace: pace };

function calculateDistance() { let result = 0; for (let i = 1; i < points.length; i++) {

result += distance(points[i­1], points[i]); } return result; } ...

function distance(p1,p2) { ... } function radians(degrees) { ... } function calculateTime() { ... }

}

function top_calculateDistance() { let result = 0; result += distance(points[i­1], points[i]); } return result; }

for (let i = 1; i < points.length; i++) {

When I copy a function like this, I like to change the name so I can distinguish them both in the code and in my head. I don’t want to think about what the right name should be right now, so I create a temporary name.

The program still works, but my static analysis is rightly rather upset. The new function has two undefined symbols: distance and points. The natural way to deal with points is to pass it in as a parameter.

Click here to view code image

function top_calculateDistance(points) { let result = 0; result += distance(points[i­1], points[i]); } return result; }

for (let i = 1; i < points.length; i++) {

I could do the same with distance, but perhaps it makes sense to move it together with calculateDistance. Here’s the relevant code:

function trackSummary…

Click here to view code image function distance(p1,p2) {

// haversine formula see http://www.movable­type.co.uk/scripts/latlong.html const EARTH_RADIUS = 3959; // in miles const dLat = radians(p2.lat) ­ radians(p1.lat); const dLon = radians(p2.lon) ­ radians(p1.lon); const a = Math.pow(Math.sin(dLat / 2),2) + Math.cos(radians(p2.lat)) * Math.cos(radians(p1.lat)) * Math.pow(Math.sin(dLon / 2), 2); const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1­a)); return EARTH_RADIUS * c;

} function radians(degrees) { return degrees * Math.PI / 180; }

I can see that distance only uses radians and radians doesn’t use anything inside its current context. So rather than pass the functions, I might as well move them too. I can make a small step in this direction by moving them from their current context to nest them inside the nested calculateDistance.

Click here to view code image

function trackSummary(points) {

const totalTime = calculateTime(); const totalDistance = calculateDistance(); const pace = totalTime / 60 / totalDistance ; return {

time: totalTime,

distance: totalDistance,

pace: pace };

function calculateDistance() { let result = 0;

for (let i = 1; i < points.length; i++) {

result += distance(points[i­1], points[i]);

} return result;

function distance(p1,p2) { ... } function radians(degrees) { ... }

}

By doing this, I can use both static analysis and testing to tell me if there are any complications. In this case all is well, so I can copy them over to top_calculateDistance. Click here to view code image

function top_calculateDistance(points) { let result = 0;

for (let i = 1; i < points.length; i++) {

result += distance(points[i­1], points[i]);

} return result;

function distance(p1,p2) { ... } function radians(degrees) { ... }

}

Again, the copy doesn’t change how the program runs, but does give me an opportunity for more static analysis. Had I not spotted that distance calls radians, the linter would have caught it at this step.

Now that I have prepared the table, it’s time for the major change—the body of the original calculateDistance will now call top_calculateDistance:

Click here to view code image

function trackSummary(points) {

const totalTime = calculateTime(); const totalDistance = calculateDistance(); const pace = totalTime / 60 / totalDistance ; return {

time: totalTime,

distance: totalDistance,

pace: pace };

function calculateDistance() { return top_calculateDistance(points); }

This is the crucial time to run tests to fully test that the moved function has bedded down in its new home.

With that done, it’s like unpacking the boxes after moving house. The first thing is to decide whether to keep the original function that’s just delegating or not. In this case, there are few callers and, as usual with nested functions, they are highly localized. So I’m happy to get rid of it. Click here to view code image

function trackSummary(points) {

const totalTime = calculateTime(); const totalDistance = top_calculateDistance(points); const pace = totalTime / 60 / totalDistance ; return {

time: totalTime,

distance: totalDistance,

pace: pace };

Now is also a good time to think about what I want the name to be. Since the top­level function has the highest visibility, I’d like it to have the best name. totalDistance seems like a good choice. I can’t use that immediately since it will be shadowed by the variable inside trackSummary—but I don’t see any reason to keep that anyway, so I use Inline Variable (123) on it.

Click here to view code image

function trackSummary(points) { const totalTime = calculateTime(); const pace = totalTime / 60 / totalDistance(points) ; return { time: totalTime, distance: totalDistance(points), pace: pace }; function totalDistance(points) { let result = 0;

for (let i = 1; i < points.length; i++) {

result += distance(points[i­1], points[i]);

} return result;

If I’d had the need to keep the variable, I’d have renamed it to something like totalDistanceCache or distance.

Since the functions for distance and radians don’t depend on anything inside totalDistance, I prefer to move them to top level too, putting all four functions at the top level.

Click here to view code image

function trackSummary(points) { ... } function totalDistance(points) { ... } function distance(p1,p2) { ... } function radians(degrees) { ... }

Some people would prefer to keep distance and radians inside totalDistance in order to restrict their visibility. In some languages that may be a consideration, but with ES 2015, JavaScript has an excellent module mechanism that’s the best tool for controlling function visibility. In general, I’m wary of nested functions—they too easily set up hidden data interrelationships that can get hard to follow.

Example: Moving between Classes

To illustrate this variety of Move Function, I’ll start here:

class Account…

Click here to view code image

get bankCharge() { let result = 4.5; if (this._daysOverdrawn > 0) result += this.overdraftCharge; return result; }

get overdraftCharge() {

if (this.type.isPremium) { const baseCharge = 10; if (this.daysOverdrawn <= 7) return baseCharge; else return baseCharge + (this.daysOverdrawn ­ 7) * 0.85; } else return this.daysOverdrawn * 1.75;

}

Coming up are changes that lead to different types of account having different algorithms for determining the charge. Thus it seems natural to move overdraftCharge to the account type class.

The first step is to look at the features that the overdraftCharge method uses and consider whether it is worth moving a batch of methods together. In this case I need the daysOverdrawn method to remain on the account class, because that will vary with individual accounts. Next, I copy the method body over to the account type and get it to fit.

class AccountType…

Click here to view code image

overdraftCharge(daysOverdrawn) {

if (this.isPremium) { const baseCharge = 10; if (daysOverdrawn <= 7) return baseCharge; else return baseCharge + (daysOverdrawn ­ 7) * 0.85; } else return daysOverdrawn * 1.75;

}

In order to get the method to fit in its new location, I need to deal with two call targets that change their scope. isPremium is now a simple call on this. With daysOverdrawn I have to decide—do I pass the value or do I pass the account? For the moment, I just pass the simple value but I may well change this in the future if I require more than just the days overdrawn from the account—especially if what I want from the account varies with the account type.

Next, I replace the original method body with a delegating call.

class Account…

Click here to view code image

get bankCharge() { let result = 4.5; if (this._daysOverdrawn > 0) result += this.overdraftCharge; return result; }

get overdraftCharge() { return this.type.overdraftCharge(this.daysOverdrawn); }

Then comes the decision of whether to leave the delegation in place or to inline overdraftCharge. Inlining results in:

class Account… Click here to view code image

get bankCharge() { let result = 4.5; if (this._daysOverdrawn > 0) result += this.type.overdraftCharge(this.daysOverdrawn); return result; }

In the earlier steps, I passed daysOverdrawn as a parameter—but if there’s a lot of data from the account to pass, I might prefer to pass the account itself.

class Account…

Click here to view code image

get bankCharge() { let result = 4.5; if (this._daysOverdrawn > 0) result += this.overdraftCharge; return result; }

get overdraftCharge() { return this.type.overdraftCharge(this); }

class AccountType…

Click here to view code image

overdraftCharge(account) {

if (this.isPremium) { const baseCharge = 10; if (account.day>sOverdrawn <= 7) return baseCharge; else return baseCharge + (account.daysOverdrawn ­ 7) * 0.85; } else return account.daysOverdrawn * 1.75;

}

MOVE FIELD Motivation

Programming involves writing a lot of code that implements behavior—but the strength of a program is really founded on its data structures. If I have a good set of data structures that match the problem, then my behavior code is simple and straightforward. But poor data structures lead to lots of code whose job is merely dealing with the poor data. And it’s not just messier code that’s harder to understand; it also means the data structures obscure what the program is doing.

So, data structures are important—but like most aspects of programming they are hard to get right. I do make an initial analysis to figure out the best data structures, and I’ve found that experience and techniques like domain­driven design have improved my ability to do that. But despite all my skill and experience, I still find that I frequently make mistakes in that initial design. In the process of programming, I learn more about the problem domain and my data structures. A design decision that is reasonable and correct one week can become wrong in another.

As soon as I realize that a data structure isn’t right, it’s vital to change it. If I leave my data structures with their blemishes, those blemishes will confuse my thinking and complicate my code far into the future.

I may seek to move data because I find I always need to pass a field from one record whenever I pass another record to a function. Pieces of data that are always passed to functions together are usually best put in a single record in order to clarify their relationship. Change is also a factor; if a change in one record causes a field in another record to change too, that’s a sign of a field in the wrong place. If I have to update the same field in multiple structures, that’s a sign that it should move to another place where it only needs to be updated once. I usually do Move Field in the context of a broader set of changes. Once I’ve moved a field, I find that many of the users of the field are better off accessing that data through the target object rather than the original source. I then change these with later refactorings. Similarly, I may find that I can’t do Move Field at the moment due to the way the data is used. I need to refactor some usage patterns first, then do the move.

In my description so far, I’m saying “record,” but all this is true of classes and objects too. A class is a record type with attached functions—and these need to be kept healthy just as much as any other data. The attached functions do make it easier to move data around, since the data is encapsulated behind accessor methods. I can move the data, change the accessors, and clients of the accessors will still work. So, this is a refactoring that’s easier to do if you have classes, and my description below makes that assumption. If I’m using bare records that don’t support encapsulation, I can still make a change like this, but it is more tricky.

Mechanics

Ensure the source field is encapsulated.

Test.

Create a field (and accessors) in the target.

Run static checks.

Ensure there is a reference from the source object to the target object.

An existing field or method may give you the target. If not, see if you can easily create a method that will do so. Failing that, you may need to create a new field in the source object that can store the target. This may be a permanent change, but you can also do it temporarily until you have done enough refactoring in the broader context.

Adjust accessors to use the target field.

If the target is shared between source objects, consider first updating the setter to modify both target and source fields, followed by Introduce Assertion (302) to detect inconsistent updates. Once you determine all is well, finish changing the accessors to use the target field.

Test. Remove the source field. Test.

Example

I’m starting here with this customer and contract: class Customer…

Click here to view code image

constructor(name, discountRate) { this._name = name; this._discountRate = discountRate; this._contract = new CustomerContract(dateToday()); } get discountRate() {return this._discountRate;} becomePreferred() {

this._discountRate += 0.03;

// other nice things } applyDiscount(amount) {

return amount.subtract(amount.multiply(this._discountRate)); }

class CustomerContract…

Click here to view code image

constructor(startDate) { this._startDate = startDate; }

I want to move the discount rate field from the customer to the customer contract. The first thing I need to use is Encapsulate Variable (132) to encapsulate access to the discount rate field.

class Customer…

Click here to view code image

constructor(name, discountRate) { this._name = name; this._setDiscountRate(discountRate); this._contract = new CustomerContract(dateToday());

} get discountRate() {return this._discountRate;}

_setDiscountRate(aNumber) {this._discountRate = aNumber;}

becomePreferred() { this._setDiscountRate(this.discountRate + 0.03); // other nice things } applyDiscount(amount) {

return amount.subtract(amount.multiply(this.discountRate)); }

I use a method to update the discount rate, rather than a property setter, as I don’t want to make a public setter for the discount rate.

I add a field and accessors to the customer contract.

class CustomerContract…

Click here to view code image

constructor(startDate, discountRate) { this._startDate = startDate; this._discountRate = discountRate; } get discountRate() {return this._discountRate;}

set discountRate(arg) {this._discountRate = arg;}

I now modify the accessors on customer to use the new field. When I did that, I got an error: “Cannot set property ’discountRate’ of undefined”. This was because _setDiscountRate was called before I created the contract object in the constructor. To fix that, I first reverted to the previous state, then used Slide Statements (223) to move the _setDiscountRate after creating the contract.

class Customer…

Click here to view code image

constructor(name, discountRate) { this._name = name; this._setDiscountRate(discountRate); this._contract = new CustomerContract(dateToday()); } I tested that, then changed the accessors again to use the contract.

class Customer…

Click here to view code image

get discountRate() {return this._contract.discountRate;}

_setDiscountRate(aNumber) {this._contract.discountRate = aNumber;}

Since I’m using JavaScript, there is no declared source field, so I don’t need to remove anything further.

Changing a Bare Record

This refactoring is generally easier with objects, since encapsulation provides a natural way to wrap data access in methods. If I have many functions accessing a bare record, then, while it’s still a valuable refactoring, it is decidedly more tricky.

I can create accessor functions and modify all the reads and writes to use them. If the field that’s being moved is immutable, I can update both the source and the target fields when I set its value and gradually migrate reads. Still, if possible, my first move would be to use Encapsulate Record (162) to turn the record into a class so I can make the change more easily.

Example: Moving to a Shared Object

Now, let’s consider a different case. Here’s an account with an interest rate:

class Account…

Click here to view code image

constructor(number, type, interestRate) { this._number = number; this._type = type; this._interestRate = interestRate; } get interestRate() {return this._interestRate;}

class AccountType…

constructor(nameString) {

this._name = nameString; }

I want to change things so that an account’s interest rate is determined from its account type.

The access to the interest rate is already nicely encapsulated, so I’ll just create the field and an appropriate accessor on the account type.

class AccountType…

Click here to view code image

constructor(nameString, interestRate) {

this._name = nameString;

this._interestRate = interestRate;

} get interestRate() {return this._interestRate;}

But there is a potential problem when I update the accesses from account. Before this refactoring, each account had its own interest rate. Now, I want all accounts to share the interest rates of their account type. If all the accounts of the same type already have the same interest rate, then there’s no change in observable behavior, so I’m fine with the refactoring. But if there’s an account with a different interest rate, it’s no longer a refactoring. If my account data is held in a database, I should check the database to ensure that all my accounts have the rate matching their type. I can also Introduce Assertion (302) in the account class.

class Account…

Click here to view code image

constructor(number, type, interestRate) { this._number = number; this._type = type; assert(interestRate === this._type.interestRate); this._interestRate = interestRate; } get interestRate() {return this._interestRate;}

I might run the system for a while with this assertion in place to see if I get an error. Or, instead of adding an assertion, I might log the problem. Once I’m confident that I’m not introducing an observable change, I can change the access, removing the update from the account completely.

class Account…

Click here to view code image

constructor(number, type) { this._number = number; this._type = type; } get interestRate() {return this._type.interestRate;}

MOVE STATEMENTS INTO FUNCTION

inverse of: Move Statements to Callers (217)

Motivation Motivation

Removing duplication is one of the best rules of thumb of healthy code. If I see the same code executed every time I call a particular function, I look to combine that repeating code into the function itself. That way, any future modifications to the repeating code can be done in one place and used by all the callers. Should the code vary in the future, I can easily move it (or some of it) out again with Move Statements to Callers (217).

I move statements into a function when I can best understand these statements as part of the called function. If they don’t make sense as part of the called function, but still should be called with it, I’ll simply use Extract Function (106) on the statements and the called function. That’s essentially the same process as I describe below, but without the inline and rename steps. It’s not unusual to do that and then, after later reflection, carry out those final steps.

Mechanics

If the repetitive code isn’t adjacent to the call of the target function, use Slide Statements (223) to get it adjacent.

If the target function is only called by the source function, just cut the code from the source, paste it into the target, test, and ignore the rest of these mechanics.

If you have more callers, use Extract Function (106) on one of the call sites to extract both the call to the target function and the statements you wish to move into it. Give it a name that’s transient, but easy to grep.

Convert every other call to use the new function. Test after each conversion.

When all the original calls use the new function, use Inline Function (115) to inline the original function completely into the new function, removing the original function.

Rename Function (124) to change the name of the new function to the same name

as the original function.

Or to a better name, if there is one.

Example

I’ll start with this code to emit HTML for data about a photo:

Click here to view code image

function renderPerson(outStream, person) {

const result = []; result.push(`<p>${person.name}</p>`); result.push(renderPhoto(person.photo)); result.push(`<p>title: ${person.photo.title}</p>`); result.push(emitPhotoData(person.photo)); return result.join("\n");

}

function photoDiv(p) {

return [ "<div>", `<p>title: ${p.title}</p>`, emitPhotoData(p), "</div>",

].join("\n");

}

function emitPhotoData(aPhoto) { const result = []; result.push(`<p>location: ${aPhoto.location}</p>`); result.push(`<p>date: ${aPhoto.date.toDateString()}</p>`); return result.join("\n"); }

This code shows two calls to emitPhotoData, each preceded by a line of code that is semantically equivalent. I’d like to remove this duplication by moving the title printing into emitPhotoData. If I had just the one caller, I would just cut and paste the code, but the more callers I have, the more I’m inclined to use a safer procedure.

I begin by using Extract Function (106) on one of the callers. I’m extracting the statements I want to move into emitPhotoData, together with the call to emitPhotoData itself.

Click here to view code image

function photoDiv(p) { return [ "<div>", zznew(p), "</div>",

].join("\n");

}

function zznew(p) { return [ `<p>title: ${p.title}</p>`, emitPhotoData(p),

].join("\n");

}

I can now look at the other callers of emitPhotoData and, one by one, replace the calls and the preceding statements with calls to the new function.

Click here to view code image

function renderPerson(outStream, person) { const result = []; result.push(`<p>${person.name}</p>`); result.push(renderPhoto(person.photo)); result.push(zznew(person.photo)); return result.join("\n"); }

Now that I’ve done all the callers, I use Inline Function (115) on emitPhotoData:

Click here to view code image

function zznew(p) {

return [ `<p>title: ${p.title}</p>`, `<p>location: ${p.location}</p>`, `<p>date: ${p.date.toDateString()}</p>`,

].join("\n");

}

and finish with Rename Function (124):

Click here to view code image

function renderPerson(outStream, person) { const result = []; result.push(`<p>${person.name}</p>`); result.push(renderPhoto(person.photo)); result.push(emitPhotoData(person.photo)); return result.join("\n"); }

function photoDiv(aPhoto) { return [ "<div>", emitPhotoData(aPhoto), "</div>",

].join("\n");

}

function emitPhotoData(aPhoto) {

return [ `<p>title: ${aPhoto.title}</p>`, `<p>location: ${aPhoto.location}</p>`, `<p>date: ${aPhoto.date.toDateString()}</p>`,

].join("\n");

}

I also make the parameter names fit my convention while I’m at it.

MOVE STATEMENTS TO CALLERS

inverse of: Move Statements into Function (213)

Motivation

Functions are the basic building block of the abstractions we build as programmers. And, as with any abstraction, we don’t always get the boundaries right. As a code base changes its capabilities—as most useful software does—we often find our abstraction boundaries shift. For functions, that means that what might once have been a cohesive, atomic unit of behavior becomes a mix of two or more different things.

One trigger for this is when common behavior used in several places needs to vary in some of its calls. Now, we need to move the varying behavior out of the function to its callers. In this case, I’ll use Slide Statements (223) to get the varying behavior to the beginning or end of the function and then Move Statements to Callers. Once the varying code is in the caller, I can change it when necessary.

Move Statements to Callers works well for small changes, but sometimes the boundaries between caller and callee need complete reworking. In that case, my best move is to use Inline Function (115) and then slide and extract new functions to form better boundaries.

Mechanics

In simple circumstances, where you have only one or two callers and a simple function to call from, just cut the first line from the called function and paste (and perhaps fit) it into the callers. Test and you’re done.

Otherwise, apply Extract Function (106) to all the statements that you don’t wish to move; give it a temporary but easily searchable name.

If the function is a method that is overridden by subclasses, do the extraction on all of them so that the remaining method is identical in all classes. Then remove the subclass methods.

Use Inline Function (115) on the original function.

Apply Change Function Declaration (124) on the extracted function to rename it to the original name.

Or to a better name, if you can think of one.

Example

Here’s a simple case: a function with two callers.

Click here to view code image

function renderPerson(outStream, person) { outStream.write(`<p>${person.name}</p>\n`); renderPhoto(outStream, person.photo); emitPhotoData(outStream, person.photo);

}

function listRecentPhotos(outStream, photos) { photos .filter(p => p.date > recentDateCutoff()) .forEach(p => {

outStream.write("<div>\n");

emitPhotoData(outStream, p);

outStream.write("</div>\n");

});

}

function emitPhotoData(outStream, photo) { outStream.write(`<p>title: ${photo.title}</p>\n`); outStream.write(`<p>date: ${photo.date.toDateString()}</p>\n`); outStream.write(`<p>location: ${photo.location}</p>\n`); }

I need to modify the software so that listRecentPhotos renders the location information differently while renderPerson stays the same. To make this change easier, I’ll use Move Statements to Callers on the final line.

Usually, when faced with something this simple, I’ll just cut the last line from renderPerson and paste it below the two calls. But since I’m explaining what to do in more tricky cases, I’ll go through the more elaborate but safer procedure.

My first step is to use emitPhotoData.

Extract Function (106) on the code that will remain in

Click here to view code image

function renderPerson(outStream, person) { outStream.write(`<p>${person.name}</p>\n`); renderPhoto(outStream, person.photo); emitPhotoData(outStream, person.photo); }

function listRecentPhotos(outStream, photos) { photos .filter(p => p.date > recentDateCutoff()) .forEach(p => {

outStream.write("<div>\n");

emitPhotoData(outStream, p);

outStream.write("</div>\n");

});

} function emitPhotoData(outStream, photo) { zztmp(outStream, photo); outStream.write(`<p>location: ${photo.location}</p>\n`); }

function zztmp(outStream, photo) { outStream.write(`<p>title: ${photo.title}</p>\n`); outStream.write(`<p>date: ${photo.date.toDateString()}</p>\n`); }

Usually, the name of the extracted function is only temporary, so I don’t worry about coming up with anything meaningful. However, it is helpful to use something that’s easy to grep. I can test at this point to ensure the code works over the function call boundary.

Now I use Inline Function (115), one call at a time. I start with renderPerson.

Click here to view code image

function renderPerson(outStream, person) { outStream.write(`<p>${person.name}</p>\n`); renderPhoto(outStream, person.photo); zztmp(outStream, person.photo); outStream.write(`<p>location: ${person.photo.location}</p>\n`); }

function listRecentPhotos(outStream, photos) { photos .filter(p => p.date > recentDateCutoff()) .forEach(p => {

outStream.write("<div>\n");

emitPhotoData(outStream, p);

outStream.write("</div>\n");

});

}

function emitPhotoData(outStream, photo) { zztmp(outStream, photo); outStream.write(`<p>location: ${photo.location}</p>\n`); }

function zztmp(outStream, photo) { outStream.write(`<p>title: ${photo.title}</p>\n`); outStream.write(`<p>date: ${photo.date.toDateString()}</p>\n`); }

I test again to ensure this call is working properly, then move onto the next. Click here to view code image

function renderPerson(outStream, person) { outStream.write(`<p>${person.name}</p>\n`); renderPhoto(outStream, person.photo); zztmp(outStream, person.photo); outStream.write(`<p>location: ${person.photo.location}</p>\n`); }

function listRecentPhotos(outStream, photos) { photos .filter(p => p.date > recentDateCutoff()) .forEach(p => {

outStream.write("<div>\n");

zztmp(outStream, p); outStream.write(`<p>location: ${p.location}</p>\n`);

outStream.write("</div>\n");

});

}

function emitPhotoData(outStream, photo) { zztmp(outStream, photo); outStream.write(`<p>location: ${photo.location}</p>\n`); }

function zztmp(outStream, photo) { outStream.write(`<p>title: ${photo.title}</p>\n`); outStream.write(`<p>date: ${photo.date.toDateString()}</p>\n`); }

Then I can delete the outer function, completing Inline Function (115).

Click here to view code image

function renderPerson(outStream, person) { outStream.write(`<p>${person.name}</p>\n`); renderPhoto(outStream, person.photo); zztmp(outStream, person.photo); outStream.write(`<p>location: ${person.photo.location}</p>\n`); }

function listRecentPhotos(outStream, photos) { photos .filter(p => p.date > recentDateCutoff()) .forEach(p => {

outStream.write("<div>\n");

zztmp(outStream, p); outStream.write(`<p>location: ${p.location}</p>\n`);

outStream.write("</div>\n");

}); }

function emitPhotoData(outStream, photo) {

zztmp(outStream, photo);

outStream.write(`<p>location: ${photo.location}</p>\n`);

}

function zztmp(outStream, photo) { outStream.write(`<p>title: ${photo.title}</p>\n`); outStream.write(`<p>date: ${photo.date.toDateString()}</p>\n`); }

I then rename zztmp back to the original name.

Click here to view code image

function renderPerson(outStream, person) { outStream.write(`<p>${person.name}</p>\n`); renderPhoto(outStream, person.photo); emitPhotoData(outStream, person.photo); outStream.write(`<p>location: ${person.photo.location}</p>\n`); }

function listRecentPhotos(outStream, photos) { photos .filter(p => p.date > recentDateCutoff()) .forEach(p => {

outStream.write("<div>\n");

emitPhotoData(outStream, p); outStream.write(`<p>location: ${p.location}</p>\n`);

outStream.write("</div>\n");

});

}

function emitPhotoData(outStream, photo) { outStream.write(`<p>title: ${photo.title}</p>\n`); outStream.write(`<p>date: ${photo.date.toDateString()}</p>\n`); }

REPLACE INLINE CODE WITH FUNCTION CALL Motivation

Functions allow me to package up bits of behavior. This is useful for understanding—a named function can explain the purpose of the code rather than its mechanics. It’s also valuable to remove duplication: Instead of writing the same code twice, I just call the function. Then, should I need to change the function’s implementation, I don’t have to track down similar­looking code to update all the changes. (I may have to look at the callers, to see if they should all use the new code, but that’s both less common and much easier.)

If I see inline code that’s doing the same thing that I have in an existing function, I’ll usually want to replace that inline code with a function call. The exception is if I consider the similarity to be coincidental—so that, if I change the function body, I don’t expect the behavior in this inline code to change. A guide to this is the name of the function. A good name should make sense in place of inline code I have. If the name doesn’t make sense, that may be because it’s a poor name (in which case I use Rename Function (124) to fix it) or because the function’s purpose is different to what I want in this case—so I shouldn’t call it.

I find it particularly satisfying to do this with calls to library functions—that way, I don’t even have to write the function body.

Mechanics

Replace the inline code with a call to the existing function.

Test.

SLIDE STATEMENTS SLIDE STATEMENTS

formerly: Consolidate Duplicate Conditional Fragments

Motivation

Code is easier to understand when things that are related to each other appear together. If several lines of code access the same data structure, it’s best for them to be together rather than intermingled with code accessing other data structures. At its simplest, I use Slide Statements to keep such code together. A very common case of this is declaring and using variables. Some people like to declare all their variables at the top of a function. I prefer to declare the variable just before I first use it.

Usually, I move related code together as a preparatory step for another refactoring, often an Extract Function (106). Putting related code into a clearly separated function is a better separation than just moving a set of lines together, but I can’t do the Extract Function (106) unless the code is together in the first place.

Mechanics

Identify the target position to move the fragment to. Examine statements between source and target to see if there is interference for the candidate fragment. Abandon action if there is any interference.

A fragment cannot slide backwards earlier than any element it references is declared.

A fragment cannot slide forwards beyond any element that references it. A fragment cannot slide over any statement that modifies an element it references.

A fragment that modifies an element cannot slide over any other element that references the modified element.

Cut the fragment from the source and paste into the target position.

Test.

If the test fails, try breaking down the slide into smaller steps. Either slide over less code or reduce the amount of code in the fragment you’re moving.

Example

When sliding code fragments, there are two decisions involved: what slide I’d like to do and whether I can do it. The first decision is very context­specific. On the simplest level, I like to declare elements close to where I use them, so I’ll often slide a declaration down to its usage. But almost always I slide some code because I want to do another refactoring—perhaps to get a clump of code together to Extract Function (106).

Once I have a sense of where I’d like to move some code, the next part is deciding if I can do it. This involves looking at the code I’m sliding and the code I’m sliding over: Do they interfere with each other in a way that would change the observable behavior of the program?

Consider the following fragment of code:

Click here to view code image

1 const pricingPlan = retrievePricingPlan(); 2 const order = retreiveOrder();

3 const baseCharge = pricingPlan.base;

4 let charge;

5 const chargePerUnit = pricingPlan.unit;

6 const units = order.units;

7 let discount; 8 charge = baseCharge + units * chargePerUnit; 9 let discountableUnits = Math.max(units ­ pricingPlan.discountThreshold, 0); 10 discount = discountableUnits * pricingPlan.discountFactor; 11 if (order.isRepeat) discount += 20; 12 charge = charge ­ discount; 13 chargeOrder(charge); The first seven lines are declarations, and it’s relatively easy to move these. For example, I may want to move all the code dealing with discounts together, which would involve moving line 7 (`let discount`) to above line 10 (`discount = ...`). Since a declaration has no side effects and refers to no other variable, I can safely move this forwards as far as the first line that references discount itself. This is also a common move—if I want to use Extract Function (106) on the discount logic, I’ll need to move the declaration down first.

I do similar analysis with any code that doesn’t have side effects. So I can take line 2 (`const order = ...`) and move it down to above line 6 (`const units = ...`) without trouble.

In this case, I’m also helped by the fact that the code I’m moving over doesn’t have side effects either. Indeed, I can freely rearrange code that lacks side effects to my heart’s content, which is one of the reasons why wise programmers prefer to use side­effectfree code as much as possible.

There is a wrinkle here, however. How do I know that line 2 is side­effect­free? To be sure, I’d need to look inside retrieveOrder() to ensure there are no side effects there (and inside any functions it calls, and inside any functions its functions call, and so on). In practice, when working on my own code, I know that I generally follow the Command­Query Separation [mf­cqs] principle, so any function that returns a value is free of side effects. But I can only be confident of that because I know the code base; if I were working in an unknown code base, I’d have to be more cautious. But I do try to follow the Command­Query Separation in my own code because it’s so valuable to know that code is free of side effects.

When sliding code that has a side effect, or sliding over code with side effects, I have to be much more careful. What I’m looking for is interference between the two code fragments. So, let’s say I want to slide line 11 (`if (order.isRepeat) ...`) down to the end. I’m prevented from doing that by line 12 because it references the variable whose state I’m changing in line 11. Similarly, I can’t take line 13 (`chargeOrder(charge)`) and move it up because line 12 modifies some state that line 13 references. However, I can slide line 8 (`charge = baseCharge + ...`) over lines 9–11 because there they don’t modify any common state.

The most straightforward rule to follow is that I can’t slide one fragment of code over another if any data that both fragments refer to is modified by either one. But that’s not a comprehensive rule; I can happily slide either of the following two lines over the other: a = a + 10;

a = a + 5;

But judging whether a slide is safe means I have to really understand the operations involved and how they compose.

Since I need to worry so much about updating state, I look to remove as much of it as I can. So with this code, I’d be looking to apply Split Variable (240) on charge before I indulge in any sliding around of that code.

Here, the analysis is relatively simple because I’m mostly just modifying local variables. With more complex data structures, it’s much harder to be sure when I get interference. So tests play an important role: Slide the fragment, run tests, see if things break. If my test coverage is good, I can feel happy with the refactoring. But if tests aren’t reliable, I need to be more wary—or, more likely, to improve the tests for the code I’m working on.

The most important consequence of a test failure after a slide is to use smaller slides: Instead of sliding over ten lines, I’ll just pick five, or slide up to what I reckon is a dangerous line. It may also mean that the slide isn’t worth it, and I need to work on something else first.

Example: Sliding with Conditionals

I can also do slides with conditionals. This will either involve removing duplicate logic when I slide out of a conditional, or adding duplicate logic when I slide in.

Here’s a case where I have the same statements in both legs of a conditional:

Click here to view code image

let result; if (availableResources.length === 0) {

result = createResource();

allocatedResources.push(result); } else {

result = availableResources.pop();

allocatedResources.push(result); } return result;

I can slide these out of the conditional, in which case they turn into a single statement outside of the conditional block. Click here to view code image

let result; if (availableResources.length === 0) {

result = createResource(); } else {

result = availableResources.pop(); } allocatedResources.push(result); return result;

In the reverse case, sliding a fragment into a conditional means repeating it in every leg of the conditional.

Further Reading

I’ve seen an almost identical refactoring under the name of Swap Statement [wakeswap]. Swap Statement moves adjacent fragments, but it only works with singlestatement fragments. You can think of it as Slide Statements where both the sliding fragment and the slid­over fragment are single statements. This refactoring appeals to me; after all, I’m always going on about taking small steps—steps that may seem ridiculously small to those new to refactoring.

But I ended up writing this refactoring with larger fragments because that is what I do. I only move one statement at a time if I’m having difficulty with a larger slide, and I rarely run into problems with larger slides. With more messy code, however, smaller slides end up being easier.

SPLIT LOOP Motivation

You often see loops that are doing two different things at once just because they can do that with one pass through a loop. But if you’re doing two different things in the same loop, then whenever you need to modify the loop you have to understand both things. By splitting the loop, you ensure you only need to understand the behavior you need to modify.

Splitting a loop can also make it easier to use. A loop that calculates a single value can just return that value. Loops that do many things need to return structures or populate local variables. I frequently follow a sequence of Split Loop followed by Extract Function (106). Many programmers are uncomfortable with this refactoring, as it forces you to execute the loop twice. My reminder, as usual, is to separate refactoring from optimization (Refactoring and Performance (64)). Once I have my code clear, I’ll optimize it, and if the loop traversal is a bottleneck, it’s easy to slam the loops back together. But the actual iteration through even a large list is rarely a bottleneck, and splitting the loops often enables other, more powerful, optimizations.

Mechanics

Copy the loop.

Identify and eliminate duplicate side effects.

Test.

When done, consider Extract Function (106) on each loop.

Example

I’ll start with a little bit of code that calculates the total salary and youngest age.

Click here to view code image

let youngest = people[0] ? people[0].age : Infinity; let totalSalary = 0; for (const p of people) {

if (p.age < youngest) youngest = p.age;

totalSalary += p.salary; }

return `youngestAge: ${youngest}, totalSalary: ${totalSalary}`;

It’s a very simple loop, but it’s doing two different calculations. To split them, I begin with just copying the loop.

Click here to view code image

let youngest = people[0] ? people[0].age : Infinity; let totalSalary = 0; for (const p of people) {

if (p.age < youngest) youngest = p.age;

totalSalary += p.salary; }

for (const p of people) { if (p.age < youngest) youngest = p.age; totalSalary += p.salary;

}

return `youngestAge: ${youngest}, totalSalary: ${totalSalary}`;

With the loop copied, I need to remove the duplication that would otherwise produce wrong results. If something in the loop has no side effects, I can leave it there for now, but it’s not the case with this example.

Click here to view code image

let youngest = people[0] ? people[0].age : Infinity; let totalSalary = 0; for (const p of people) {

if (p.age < youngest) youngest = p.age; totalSalary += p.salary;

}

for (const p of people) { if (p.age < youngest) youngest = p.age;

totalSalary += p.salary;

}

return `youngestAge: ${youngest}, totalSalary: ${totalSalary}`;

Officially, that’s the end of the Split Loop refactoring. But the point of Split Loop isn’t what it does on its own but what it sets up for the next move—and I’m usually looking to extract the loops into their own functions. I’ll use Slide Statements (223) to reorganize the code a bit first.

Click here to view code image

let totalSalary = 0; for (const p of people) { totalSalary += p.salary; }

let youngest = people[0] ? people[0].age : Infinity; for (const p of people) { if (p.age < youngest) youngest = p.age; }

return `youngestAge: ${youngest}, totalSalary: ${totalSalary}`;

Then I do a couple of Extract Function (106). Click here to view code image

return `youngestAge: ${youngestAge()}, totalSalary: ${totalSalary()}`;

function totalSalary() { let totalSalary = 0; for (const p of people) { totalSalary += p.salary; } return totalSalary; }

function youngestAge() { let youngest = people[0] ? people[0].age : Infinity; for (const p of people) { if (p.age < youngest) youngest = p.age; } return youngest; }

I can rarely resist Replace Loop with Pipeline (231) for the total salary, and there’s an obvious Substitute Algorithm (195) for the youngest age.

Click here to view code image

return `youngestAge: ${youngestAge()}, totalSalary: ${totalSalary()}`;

function totalSalary() { return people.reduce((total,p) => total + p.salary, 0); } function youngestAge() {

return Math.min(...people.map(p => p.age)); }

REPLACE LOOP WITH PIPELINE Motivation

Like most programmers, I was taught to use loops to iterate over a collection of objects. Increasingly, however, language environments provide a better construct: the collection pipeline. Collection Pipelines [mf­cp] allow me to describe my processing as a series of operations, each consuming and emitting a collection. The most common of these operations are map, which uses a function to transform each element of the input collection, and filter which uses a function to select a subset of the input collection for later steps in the pipeline. I find logic much easier to follow if it is expressed as a pipeline—I can then read from top to bottom to see how objects flow through the pipeline.

Mechanics

Create a new variable for the loop’s collection.

This may be a simple copy of an existing variable.

Starting at the top, take each bit of behavior in the loop and replace it with a collection pipeline operation in the derivation of the loop collection variable. Test after each change.

Once all behavior is removed from the loop, remove it. If it assigns to an accumulator, assign the pipeline result to the accumulator.

Example

I’ll begin with some data: a CSV file of data about our offices. Click here to view code image

office, country, telephone Chicago, USA, +1 312 373 1000 Beijing, China, +86 4008 900 505 Bangalore, India, +91 80 4064 9570 Porto Alegre, Brazil, +55 51 3079 3550 Chennai, India, +91 44 660 44766

... (more data follows)

The following function picks out the offices in India and returns their cities and telephone numbers:

Click here to view code image

function acquireData(input) {

const lines = input.split("\n"); let firstLine = true; const result = []; for (const line of lines) {

if (firstLine) {

firstLine = false;

continue;

}

if (line.trim() === "") continue;

const record = line.split(",");

if (record[1].trim() === "India") {

result.push({city: record[0].trim(), phone: record[2].trim()});

}

} return result;

}

I want to replace that loop with a collection pipeline.

My first step is to create a separate variable for the loop to work over. Click here to view code image function acquireData(input) {

const lines = input.split("\n"); let firstLine = true; const result = []; const loopItems = lines for (const line of loopItems) {

if (firstLine) {

firstLine = false;

continue;

}

if (line.trim() === "") continue;

const record = line.split(",");

if (record[1].trim() === "India") {

result.push({city: record[0].trim(), phone: record[2].trim()});

}

} return result;

}

The first part of the loop is all about skipping the first line of the CSV file. This calls for a slice, so I remove that first section of the loop and add a slice operation to the formation of the loop variable.

Click here to view code image

function acquireData(input) { const lines = input.split("\n");

let firstLine = true; const result = []; const loopItems = lines .slice(1); for (const line of loopItems) {

if (firstLine) {

firstLine = false;

continue;

}

if (line.trim() === "") continue;

const record = line.split(",");

if (record[1].trim() === "India") {

result.push({city: record[0].trim(), phone: record[2].trim()});

}

} return result;

}

As a bonus, this lets me delete firstLine—and I particularly enjoy deleting control variables. The next bit of behavior removes any blank lines. I can replace this with a filter operation.

Click here to view code image

function acquireData(input) {

const lines = input.split("\n"); const result = []; const loopItems = lines

.slice(1)

.filter(line => line.trim() !== "")

; for (const line of loopItems) {

if (line.trim() === "") continue;

const record = line.split(",");

if (record[1].trim() === "India") {

result.push({city: record[0].trim(), phone: record[2].trim()});

}

} return result;

}

When writing a pipeline, I find it best to put the terminal semicolon on its own line.

I use the map operation to turn lines into an array of strings—misleadingly called record in the original function, but it’s safer to keep the name for now and rename later.

Click here to view code image

function acquireData(input) {

const lines = input.split("\n"); const result = []; const loopItems = lines .slice(1) .filter(line => line.trim() !== "") .map(line => line.split(",")) ; for (const line of loopItems) { const record = line;.split(",");

if (record[1].trim() === "India") {

result.push({city: record[0].trim(), phone: record[2].trim()});

}

} return result;

}

Filter again to just get the India records: Click here to view code image

function acquireData(input) {

const lines = input.split("\n"); const result = []; const loopItems = lines .slice(1) .filter(line => line.trim() !== "") .map(line => line.split(",")) .filter(record => record[1].trim() === "India") ; for (const line of loopItems) { const record = line;

if (record[1].trim() === "India") {

result.push({city: record[0].trim(), phone: record[2].trim()});

}

} return result;

}

Map to the output record form:

Click here to view code image

function acquireData(input) {

const lines = input.split("\n"); const result = []; const loopItems = lines .slice(1) .filter(line => line.trim() !== "") .map(line => line.split(",")) .filter(record => record[1].trim() === "India") .map(record => ({city: record[0].trim(), phone: record[2].trim()})) ; for (const line of loopItems) { const record = line; result.push(line); } return result;

}

Now, all the loop does is assign values to the accumulator. So I can remove it and assign the result of the pipeline to the accumulator:

Click here to view code image

function acquireData(input) { const lines = input.split("\n"); const result = lines

.slice(1) .filter(line => line.trim() !== "") .map(line => line.split(",")) .filter(record => record[1].trim() === "India") .map(record => ({city: record[0].trim(), phone: record[2].trim()})) ;

for (const line of loopItems) {

const record = line;

result.push(line);

} return result;

}

That’s the core of the refactoring. But I do have some cleanup I’d like to do. I inlined result, renamed some lambda variables, and made the layout read more like a table.

Click here to view code image

function acquireData(input) {

const lines = input.split("\n"); return lines .slice (1) .filter .map (line => line.split(",")) .filter (fields => fields[1].trim() === "India") .map (fields => ({city: fields[0].trim(), phone: fields[2].trim()})) ;

(line

=>

line.trim()

!==

"

"

)

}

I thought about inlining lines too, but felt that its presence explains what’s happening.

Further Reading

For more examples on turning loops into pipelines, see my essay “Refactoring with Loops and Collection Pipelines” [mf­ref­pipe].

REMOVE DEAD CODE Motivation

When we put code into production, even on people’s devices, we aren’t charged by weight. A few unused lines of code don’t slow down our systems nor take up significant memory; indeed, decent compilers will instinctively remove them. But unused code is still a significant burden when trying to understand how the software works. It doesn’t carry any warning signs telling programmers that they can ignore this function as it’s never called any more, so they still have to spend time understanding what it’s doing and why changing it doesn’t seem to alter the output as they expected.

Once code isn’t used any more, we should delete it. I don’t worry that I may need it sometime in the future; should that happen, I have my version control system so I can always dig it out again. If it’s something I really think I may need one day, I might put a comment into the code that mentions the lost code and which revision it was removed in—but, honestly, I can’t remember the last time I did that, or regretted that I hadn’t done it.

Commenting out dead code was once a common habit. This was useful in the days before version control systems were widely used, or when they were inconvenient. Now, when I can put even the smallest code base under version control, that’s no longer needed.

Mechanics

If the dead code can be referenced from outside, e.g., when it’s a full function, do a search to check for callers.

Remove the dead code.

Test.