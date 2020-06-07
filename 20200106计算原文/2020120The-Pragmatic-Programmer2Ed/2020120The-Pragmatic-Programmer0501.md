Life doesn’t stand still. Neither can the code that we write. In

order to keep up with today’s near-frantic pace of change, we

need to make every effort to write code that’s as loose—as

flexible—as possible. Otherwise we may find our code quickly

becoming outdated, or too brittle to fix, and may ultimately be

left behind in the mad dash toward the future.

Back in Topic 11, Reversibility we talked about the perils of

irreversible decisions. In this chapter, we’ll tell you how to make

reversible decisions, so your code can stay flexible and

adaptable in the face of an uncertain world.

First we look at coupling—the dependencies between bits of

code. Topic 28, Decoupling shows how to keep separate

concepts separate, decreasing coupling.

Next, we’ll look at different techniques you can use when Topic

29, Juggling the Real World. We’ll examine four different

strategies to help manage and react to events—a critical aspect

of modern software applications.

Traditional procedural and object-oriented code might be too

tightly coupled for your purposes. In Topic 30, Transforming

Programming, we’ll take advantage of the more flexible and clearer style offered by function pipelines, even if your language doesn’t support them directly.

Common object-oriented style can tempt you with another trap.

Don’t fall for it, or you’ll end up paying a hefty Topic 31,

Inheritance Tax. We’ll explore better alternatives to keep your code flexible and easier to change.

And of course a good way to stay flexible is to write less code.

Changing code leaves you open to the possibility of introducing new bugs. Topic 32, Configuration will explain how to move details out of the code completely, where they can be changed more safely and easily.

All these techniques will help you write code that bends and doesn’t break.

Topic 28

Decoupling

In Topic 8, The Essence of Good

Design we claim that using good

When we try to pick

design principles will make the

out anything by itself,

code you write easy to change.

we find it hitched to

Coupling is the enemy of change,

everything else in the

because it links together things

Universe.

that must change in parallel. This

makes change more difficult:

John Muir, My First Summer

either you spend time tracking

in the Sierra

down all the parts that need

changing, or you spend time

wondering why things broke when you changed「just one thing」

and not the other things to which it was coupled.

When you are designing something you want to be rigid, a

bridge or a tower perhaps, you couple the components together: images/links-01.png

The links work together to make the structure rigid.

Compare that with something like this:

images/links-02.png

Here there’s no structural rigidity: individual links can change and others just accommodate it.

When you’re designing bridges, you want them to hold their

shape; you need them to be rigid. But when you’re designing

software that you’ll want to change, you want exactly the

opposite: you want it to be flexible. And to be flexible, individual components should be coupled to as few other components as

possible.

And, to make matters worse, coupling is transitive: if A is

coupled to B and C, and B is coupled to M and N, and C to X and Y, then A is actually coupled to B, C, M, N, X, and Y.

This means there’s a simple principle you should follow:

Tip 44

Decoupled Code Is Easier to Change

Given that we don’t normally code using steel beams and rivets, just what does it mean to decouple code? In this section we’ll talk about:

Train wrecks—chains of method calls

Globalization—the dangers of static things

Inheritance—why subclassing is dangerous

To some extent this list is artificial: coupling can occur just about any time two pieces of code share something, so as you read what follows keep an eye out for the underlying patterns so you can apply them to your code. And keep a lookout for some of the symptoms of coupling:

Wacky dependencies between unrelated modules or libraries.

「Simple」changes to one module that propagate through unrelated modules in the system or break stuff elsewhere in the system.

Developers who are afraid to change code because they aren’t sure what might be affected.

Meetings where everyone has to attend because no one is sure who will be affected by a change.

TRAIN WRECKS

We’ve all seen (and probably written) code like this:

public void applyDiscount(customer, order_id, discount) {

totals = customer

.orders

.find(order_id)

.getTotals();

totals.grandTotal = totals.grandTotal - discount;

totals.discount = discount;

}

We’re getting a reference to some orders from a customer

object, using that to find a particular order, and then getting the set of totals for the order. Using those totals, we subtract the discount from the order grand total and also update them with that discount.

This chunk of code is traversing five levels of abstraction, from customer to total amounts. Ultimately our top-level code has to

know that a customer object exposes orders, that the orders have a find method that takes an order id and returns an order, and that the order object has a totals object which has getters and setters for grand totals and discounts. That’s a lot of implicit knowledge. But worse, that’s a lot of things that cannot change in the future if this code is to continue to work. All the cars in a train are coupled together, as are all the methods and attributes in a train wreck.

Let’s imagine that the business decides that no order can have a discount of more than 40%. Where would we put the code that

enforces that rule?

You might say it belongs in the applyDiscount function we just wrote. That’s certainly part of the answer. But with the code the way it is now, you can’t know that this is the whole answer. Any piece of code, anywhere, could set fields in the totals object, and if the maintainer of that code didn’t get the memo, it wouldn’t be checking against the new policy.

One way to look at this is to think about responsibilities. Surely the totals object should be responsible for managing the totals.

And yet it isn’t: it’s really just a container for a bunch of fields that anyone can query and update.

The fix for that is to apply something we call:

Tip 45

Tell, Don’t Ask

This principle says that you shouldn’t make decisions based on the internal state of an object and then update that object.

Doing so totally destroys the benefits of encapsulation and, in

doing so, spreads the knowledge of the implementation throughout the code. So the first fix for our train wreck is to delegate the discounting to the total object:

public void applyDiscount(customer, order_id, discount) {

customer

.orders

.find(order_id)

.getTotals()

.applyDiscount(discount);

}

We have the same kind of tell-don’t-ask (TDA) issue with the customer object and its orders: we shouldn’t fetch its list of orders and search them. We should instead get the order we

want directly from the customer:

public void applyDiscount(customer, order_id, discount) {

customer

.findOrder(order_id)

.getTotals()

.applyDiscount(discount);

}

The same thing applies to our order object and its totals. Why should the outside world have to know that the implementation of an order uses a separate object to store its totals?

public void applyDiscount(customer, order_id, discount) {

customer

.findOrder(order_id)

.applyDiscount(discount);

}

And this is where we’d probably stop.

At this point you might be thinking that TDA would make us

add an applyDiscountToOrder(order_id) method to customers. And, if

followed slavishly, it would.

But TDA is not a law of nature; it’s just a pattern to help us recognize problems. In this case, we’re comfortable exposing the fact that a customer has orders, and that we can find one of those orders by asking the customer object for it. This is a pragmatic decision.

In every application there are certain top-level concepts that are universal. In this application, those concepts include customers and orders. It makes no sense to hide orders totally inside customer objects: they have an existence of their own. So we have no problem creating APIs that expose order objects.

The Law of Demeter

People often talk about something called the Law of Demeter, or LoD, in relation to coupling. The LoD is a set of guidelines[37]

written in the late ’80s by Ian Holland. He created them to help developers on the Demeter Project keep their functions cleaner and decoupled.

The LoD says that a method defined in a class C should only call:

Other instance methods in C

Its parameters

Methods in objects that it creates, both on the stack and in the heap Global variables

In the first edition of this book we spent some time describing the LoD. In the intervening 20 years the bloom has faded on

that particular rose. We now don’t like the「global variable」

clause (for reasons we’ll go into in the next section). We also discovered that it’s difficult to use this in practice: it’s a little like having to parse a legal document whenever you call a method.

However, the principle is still sound. We just recommend a

somewhat simpler way of expressing almost the same thing:

Tip 46

Don’t Chain Method Calls

Try not to have more than one「.」when you access something.

And access something also covers cases where you use intermediate variables, as in the following code:

# This is pretty poor style

amount = customer.orders.last().totals().amount;

# and so is this…

orders = customer.orders;

last = orders.last();

totals = last.totals();

amount = totals.amount;

There’s a big exception to the one-dot rule: the rule doesn’t apply if the things you’re chaining are really, really unlikely to change. In practice, anything in your application should be

considered likely to change. Anything in a third-party library should be considered volatile, particularly if the maintainers of that library are known to change APIs between releases.

Libraries that come with the language, however, are probably pretty stable, and so we’d be happy with code such as:

people

.sort_by {|person| person.age }

.first(10)

.map {| person | person.name }

That Ruby code worked when we wrote the first edition, 20

years ago, and will likely still work when we enter the home for old programmers (any day now…).

Chains and Pipelines

In Topic 30, Transforming Programming we talk about composing functions into pipelines. These pipelines transform data, passing it from one function to the next. This is not the same as a train wreck of method calls, as we are not relying on hidden implementation details.

That’s not to say that pipelines don’t introduce some coupling: they do. The format of the data returned by one function in a pipeline must be compatible with the format accepted by the

next.

Our experience is that this form of coupling is far less a barrier to changing the code than the form introduced by train wrecks.

THE EVILS OF GLOBALIZATION

Globally accessible data is an insidious source of coupling

between application components. Each piece of global data acts as if every method in your application suddenly gained an

additional parameter: after all, that global data is available inside every method.

Globals couple code for many reasons. The most obvious is that a change to the implementation of the global potentially affects all the code in the system. In practice, of course, the impact is fairly limited; the problem really comes down to knowing that you’ve found every place you need to change.

Global data also creates coupling when it comes to teasing your

code apart.

Much has been made of the benefits of code reuse. Our

experience has been that reuse should probably not be a

primary concern when creating code, but the thinking that goes into making code reusable should be part of your coding

routine. When you make code reusable, you give it clean

interfaces, decoupling it from the rest of your code. This allows you to extract a method or module without dragging everything else along with it. And if your code uses global data, then it becomes difficult to split it out from the rest.

You’ll see this problem when you’re writing unit tests for code that uses global data. You’ll find yourself writing a bunch of setup code to create a global environment just to allow your test to run.

Tip 47

Avoid Global Data

Global Data Includes Singletons

In the previous section we were careful to talk about global data and not global variables. That’s because people often tell us

「Look! No global variables. I wrapped it all as instance data in a singleton object or global module.」

Try again, Skippy. If all you have is a singleton with a bunch of exported instance variables, then it’s still just global data. It just has a longer name.

So then folks take this singleton and hide all the data behind methods. Instead of coding Config.log_level they now say

Config.log_level() or Config.getLogLevel(). This is better, because it

means that your global data has a bit of intelligence behind it. If you decide to change the representation of log levels, you can maintain compatibility by mapping between the new and old in the Config API. But you still have only the one set of

configuration data.

Global Data Includes External Resources

Any mutable external resource is global data. If your application uses a database, datastore, file system, service API, and so on, it risks falling into the globalization trap. Again, the solution is to make sure you always wrap these resources behind code that

you control.

If It’s Important Enough to Be Global, Wrap It in

Tip 48

an API

INHERITANCE ADDS COUPLING

The misuse of subclassing, where a class inherits state and

behavior from another class, is so important that we discuss it in its own section, Topic 31, Inheritance Tax.

AGAIN, IT’S ALL ABOUT CHANGE

Coupled code is hard to change: alterations in one place can have secondary effects elsewhere in the code, and often in hard-to-find places that only come to light a month later in

production.

Keeping your code shy: having it only deal with things it directly knows about, will help keep your applications decoupled, and that will make them more amenable to change.

RELATED SECTIONS INCLUDE

Topic 8, The Essence of Good Design

Topic 9, DRY—The Evils of Duplication

Topic 10, Orthogonality

Topic 11, Reversibility

Topic 29, Juggling the Real World

Topic 30, Transforming Programming

Topic 31, Inheritance Tax

Topic 32, Configuration

Topic 33, Breaking Temporal Coupling

Topic 34, Shared State Is Incorrect State

Topic 35, Actors and Processes

Topic 36, Blackboards

We discuss Tell, Don’t Ask in our 2003 Software Construction article The Art of Enbugging. [38]

Topic 29

Juggling the Real World

In the old days, when your authors

still had their boyish good looks,

Things don’t just

computers were not particularly

happen; they are made

flexible. We’d typically organize

to happen.

the way we interacted with them

based on their limitations.

John F. Kennedy

Today, we expect more: computers

have to integrate into our world,

not the other way around. And our world is messy: things are constantly happening, stuff gets moved around, we change our minds, …. And the applications we write somehow have to work out what to do.

This section is all about writing these responsive applications.

We’ll start off with the concept of an event.

EVENTS

An event represents the availability of information. It might come from the outside world: a user clicking a button, or a stock quote update. It might be internal: the result of a calculation is ready, a search finishes. It can even be something as trivial as fetching the next element in a list.

Whatever the source, if we write applications that respond to events, and adjust what they do based on those events, those

applications will work better in the real world. Their users will find them to be more interactive, and the applications

themselves will make better use of resources.

But how can we write these kinds of applications? Without some kind of strategy, we’ll quickly find ourselves confused, and our applications will be a mess of tightly coupled code.

Let’s look at four strategies that help.

1. Finite State Machines

2. The Observer Pattern

3. Publish/Subscribe

4. Reactive Programming and Streams

FINITE STATE MACHINES

Dave finds that he writes code using a Finite State Machine

(FSM) just about every week. Quite often, the FSM

implementation will be just a couple of lines of code, but those few lines help untangle a whole lot of potential mess.

Using an FSM is trivially easy, and yet many developers shy

away from them. There seems to be a belief that they are

difficult, or that they only apply if you’re working with

hardware, or that you need to use some hard-to-understand

library. None of these are true.

The Anatomy of a Pragmatic FSM

A state machine is basically just a specification of how to handle events. It consists of a set of states, one of which is the current state. For each state, we list the events that are significant to that state. For each of those events, we define the new current state of the system.

For example, we may be receiving multipart messages from a

websocket. The first message is a header. This is followed by any number of data messages, followed by a trailing message. This could be represented as an FSM like this:

images/events_simple_fsm.png

We start in the「Initial state.」If we receive a header message, we transition to the「Reading message」state. If we receive anything else while we’re in the initial state (the line labeled with an asterisk) we transition to the「Error」state and we’re done.

While we’re in the「Reading message」state, we can accept

either data messages, in which case we continue reading in the same state, or we can accept a trailer message, which transitions us to the「Done」state. Anything else causes a transition to the error state.

The neat thing about FSMs is that we can express them purely as data. Here’s a table representing our message parser:

images/event_simple_fsm_table.png

The rows in the table represent the states. To find out what to do when an event occurs, look up the row for the current state, scan along for the column representing the event, the contents of that cell are the new state.

The code that handles it is equally simple:

event/simple_fsm.rb

TRANSITIONS = {

1

:

initial: { header: :reading},

-

reading: { data: :reading, trailer: :done},

-

}

-

5

:

state = :initial

-

-

while state != :done && state != :error

-

msg = get_next_message()

-

state = TRANSITIONS[state][msg.msg_type] || :error

1

0

:

end

-

The code that implements the transitions between states is on line 10. It indexes the transition table using the current state, and then indexes the transitions for that state using the message type. If there is no matching new state, it sets the state to :error.

Adding Actions

A pure FSM, such as the one we were just looking at, is an event stream parser. Its only output is the final state. We can beef it up by adding actions that are triggered on certain transitions.

For example, we might need to extract all of the strings in a source file. A string is text between quotes, but a backslash in a string escapes the next character, so "Ignore \"quotes\"" is a single string. Here’s an FSM that does this:

images/event_string_fsm.png

This time, each transition has two labels. The top one is the

event that triggers it, and the bottom one is the action to take as we move between states.

We’ll express this in a table, as we did last time. However, in this case each entry in the table is a two-element list containing the next state and the name of an action:

event/strings_fsm.rb

TRANSITIONS = {

# current new state action to take

#---------------------------------------------------------

look_for_string: {

'"' => [ :in_string, :start_new_string ],

:default => [ :look_for_string, :ignore ],

},

in_string: {

'"' => [ :look_for_string, :finish_current_string ],

'\\' => [ :copy_next_char, :add_current_to_string ],

:default => [ :in_string, :add_current_to_string ],

},

copy_next_char: {

:default => [ :in_string, :add_current_to_string ],

},

}

We’ve also added the ability to specify a default transition, taken if the event doesn’t match any of the other transitions for this state.

Now let’s look at the code:

event/strings_fsm.rb

state = :look_for_string

result = []

while ch = STDIN.getc

state, action = TRANSITIONS[state][ch] || TRANSITIONS[state][ :default]

case action

when :ignore

when :start_new_string

result = []

when :add_current_to_string

result << ch

when :finish_current_string

puts result.join

end

end

This is similar to the previous example, in that we loop through the events (the characters in the input), triggering transitions.

But it does more than the previous code. The result of each

transition is both a new state and the name of an action. We use the action name to select the code to run before we go back

around the loop.

This code is very basic, but it gets the job done. There are many other variants: the transition table could use anonymous

functions or function pointers for the actions, you could wrap the code that implements the state machine in a separate class, with its own state, and so on.

There’s nothing to say that you have to process all the state transitions at the same time. If you’re going through the steps to sign up a user on your app, there’s likely to be a number of transitions as they enter their details, validate their email, agree to the 107 different legislated warnings that online apps must now give, and so on. Keeping the state in external storage, and using it to drive a state machine, is a great way to handle these kind of workflow requirements.

State Machines Are a Start

State machines are underused by developers, and we’d like to encourage you to look for opportunities to apply them. But they don’t solve all the problems associated with events. So let’s move on to some other ways of looking at the problems of

juggling events.

THE OBSERVER PATTERN

In the observer pattern we have a source of events, called the observable and a list of clients, the observers, who are interested in those events.

An observer registers its interest with the observable, typically by passing a reference to a function to be called. Subsequently, when the event occurs, the observable iterates down its list of observers and calls the function that each passed it. The event is given as a parameter to that call.

Here’s a simple example in Ruby. The Terminator module is used to terminate the application. Before it does so, however, it notifies all its observers that the application is going to exit.[39]

They might use this notification to tidy up temporary resources, commit data, and so on:

event/observer.rb

module Terminator

CALLBACKS = []

def self.register(callback)

CALLBACKS << callback

end

def self.exit(exit_status)

CALLBACKS.each { |callback| callback.(exit_status) }

exit!(exit_status)

end

end

Terminator.register(-> (status) { puts "callback 1 sees #{ status }" })

Terminator.register(-> (status) { puts "callback 2 sees #{ status }" })

Terminator.exit(99)

$ ruby event/observer.rb

callback 1 sees 99

callback 2 sees 99

There’s not much code involved in creating an observable: you push a function reference onto a list, and then call those

functions when the event occurs. This is a good example of

when not to use a library.

The observer/observable pattern has been used for decades, and it has served us well. It is particularly prevalent in user interface systems, where the callbacks are used to inform the application that some interaction has occurred.

But the observer pattern has a problem: because each of the

observers has to register with the observable, it introduces coupling. In addition, because in the typical implementation the callbacks are handled inline by the observable, synchronously, it can introduce performance bottlenecks.

This is solved by the next strategy, Publish/Subscribe.

PUBLISH/SUBSCRIBE

Publish/Subscribe (pubsub) generalizes the observer pattern, at the same time solving the problems of coupling and

performance.

In the pubsub model, we have publishers and subscribers.

These are connected via channels. The channels are

implemented in a separate body of code: sometimes a library, sometimes a process, and sometimes a distributed

infrastructure. All this implementation detail is hidden from your code.

Every channel has a name. Subscribers register interest in one or more of these named channels, and publishers write events to them. Unlike the observer pattern, the communication

between the publisher and subscriber is handled outside your code, and is potentially asynchronous.

Although you could implement a very basic pubsub system

yourself, you probably don’t want to. Most cloud service

providers have pubsub offerings, allowing you to connect

applications around the world. Every popular language will

have at least one pubsub library.

Pubsub is a good technology for decoupling the handling of

asynchronous events. It allows code to be added and replaced, potentially while the application is running, without altering existing code. The downside is that it can be hard to see what is going on in a system that uses pubsub heavily: you can’t look at a publisher and immediately see which subscribers are involved with a particular message.

Compared to the observer pattern, pubsub is a great example of reducing coupling by abstracting up through a shared interface (the channel). However, it is still basically just a message passing system. Creating systems that respond to combinations of events will need more than this, so let’s look at ways we can add a time dimension to event processing.

REACTIVE PROGRAMMING, STREAMS, AND EVENTS

If you’ve ever used a spreadsheet, then you’ll be familiar with reactive programming. If a cell contains a formula which refers to a second cell, then updating that second cell causes the first to update as well. The values react as the values they use change.

There are many frameworks that can help with this kind of

data-level reactivity: in the realm of the browser React and Vue.js are current favorites (but, this being JavaScript, this information will be out-of-date before this book is even

printed).

It’s clear that events can also be used to trigger reactions in code, but it isn’t necessarily easy to plumb them in. That’s where streams come in.

Streams let us treat events as if they were a collection of data.

It’s as if we had a list of events, which got longer when new events arrive. The beauty of that is that we can treat streams just like any other collection: we can manipulate, combine,

filter, and do all the other data-ish things we know so well. We can even combine event streams and regular collections. And

streams can be asynchronous, which means your code gets the

opportunity to respond to events as they arrive.

The current de facto baseline for reactive event handling is defined on the site http://reactivex.io, which defines a language-agnostic set of principles and documents some

common implementations. Here we’ll use the RxJs library for

JavaScript.

Our first example takes two streams and zips them together: the

result is a new stream where each element contains one item from the first input stream and one item from the other. In this case, the first stream is simply a list of five animal names. The second stream is more interesting: it’s an interval timer which generates an event every 500ms. Because the streams are

zipped together, a result is only generated when data is available on both, and so our result stream only emits a value every half second:

event/rx0/index.js

import * as Observable from 'rxjs'

import { logValues } from "../rxcommon/logger.js"

let animals = Observable. of( "ant" , "bee" , "cat" , "dog" , "elk" )

let ticker = Observable.interval(500)

let combined = Observable.zip(animals, ticker)

combined.subscribe(next => logValues(JSON.stringify(next))) This code uses a simple logging function[40] which adds items to a list in the browser window. Each item is timestamped with the time in milliseconds since the program started to run. Here’s what it shows for our code:

images/events_rxjs_0.png

Notice the timestamps: we’re getting one event from the stream every 500ms. Each event contains a serial number (created by the interval observable) and the name of the next animal from the list. Watching it live in a browser, the log lines appear at every half second.

Event streams are normally populated as events occur, which

implies that the observables that populate them can run in

parallel. Here’s an example that fetches information about users from a remote site. For this we’ll use https://reqres.in, a public site that provides an open REST interface. As part of its API, we can fetch data on a particular (fake) user by performing a GET

request to users/«id». Our code fetches the users with the IDs 3, 2, and 1:

event/rx1/index.js

import * as Observable from 'rxjs'

import { mergeMap } from 'rxjs/operators'

import { ajax } from 'rxjs/ajax'

import { logValues } from "../rxcommon/logger.js"

let users = Observable. of(3, 2, 1)

let result = users.pipe(

mergeMap((user) => ajax.getJSON( `https://reqres.in/api/users/${user} `))

)

result.subscribe(

resp => logValues(JSON.stringify(resp.data)),

err => console.error(JSON.stringify(err))

)

The internal details of the code are not too important. What’s exciting is the result, shown in the following screenshot:

images/events_three_users.png

Look at the timestamps: the three requests, or three separate streams, were processed in parallel, The first to come back, for id 2, took 82ms, and the next two came back 50 and 51ms later.

Streams of Events Are Asynchronous Collections

In the previous example, our list of user IDs (in the observable users) was static. But it doesn’t have to be. Perhaps we want to collect this information when people log in to our site. All we have to do is to generate an observable event containing their user ID when their session is created, and use that observable instead of the static one. We’d then be fetching details about the

users as we received these IDs, and presumably storing them somewhere.

This is a very powerful abstraction: we no longer need to think about time as being something we have to manage. Event

streams unify synchronous and asynchronous processing

behind a common, convenient API.

EVENTS ARE UBIQUITOUS

Events are everywhere. Some are obvious: a button click, a

timer expiring. Other are less so: someone logging in, a line in a file matching a pattern. But whatever their source, code that’s crafted around events can be more responsive and better

decoupled than its more linear counterpart.

RELATED SECTIONS INCLUDE

Topic 28, Decoupling

Topic 36, Blackboards

EXERCISES

Exercise 19 (possible answer)

In the FSM section we mentioned that you could move the

generic state machine implementation into its own class. That class would probably be initialized by passing in a table of transitions and an initial state.

Try implementing the string extractor that way.

Exercise 20 (possible answer)

Which of these technologies (perhaps in combination) would be a good fit for the following situations:

If you receive three network interface down events within five minutes, notify the operations staff.

If it is after sunset, and there is motion detected at the bottom of the stairs followed by motion detected at the top of the stairs, turn on the upstairs lights.

You want to notify various reporting systems that an order was completed.

In order to determine whether a customer qualifies for a car loan, the application needs to send requests to three backend services and wait for the responses.

Topic 30

Transforming Programming

All programs transform data,

converting an input into an output.

If you can’t describe

And yet when we think about

what you are doing as

design, we rarely think about

a process, you don’t

creating transformations. Instead

know what you’re

we worry about classes and

doing.

modules, data structures and

algorithms, languages and

W. Edwards Deming, (attr)

frameworks.

We think that this focus on code

often misses the point: we need to get back to thinking of

programs as being something that transforms inputs into

outputs. When we do, many of the details we previously worried about just evaporate. The structure becomes clearer, the error handling more consistent, and the coupling drops way down.

To start our investigation, let’s take the time machine back to the 1970s and ask a Unix programmer to write us a program

that lists the five longest files in a directory tree, where longest means「having the largest number of lines.」

You might expect them to reach for an editor and start typing in C. But they wouldn’t, because they are thinking about this in terms of what we have (a directory tree) and what we want (a list of files). Then they’d go to a terminal and type something like:

$ find . -type f | xargs wc -l | sort -n | tail -5

This is a series of transformations:

find . -type f

Write a list of all the files (-type f) in or below the current directory (.) to standard output.

xargs wc -l

Read lines from standard input and arrange for them all

to be passed as arguments to the command wc -l. The wc

program with the -l option counts the number of lines in

each of its arguments and writes each result as「count

filename」to standard output.

sort -n

Sort standard input assuming each line starts with a

number (-n), writing the result to standard output.

tail -5

Read standard input and write just the last five lines to

standard output.

Run this in our book’s directory and we get

470 ./test_to_build.pml

487 ./dbc.pml

719 ./domain_languages.pml

727 ./dry.pml

9561 total

That last line is the total number of lines in all the files (not just those shown), because that’s what wc does. We can strip it off by requesting one more line from tail, and then ignoring the last line:

$ find . -type f | xargs wc -l | sort -n | tail -6 | head -5

470 ./debug.pml

470 ./test_to_build.pml

487 ./dbc.pml

719 ./domain_languages.pml

727 ./dry.pml

images/wc-pipeline.png

Figure 1. The find pipeline as a series of

transformations

Let’s look at this in terms of the data that flows between the individual steps. Our original requirement,「top 5 files in terms

of lines,」becomes a series of transformations (also show in the

figure).

directory name

→ list of files

→ list with line numbers

→ sorted list

→ highest five + total

→ highest five

It’s almost like an industrial assembly line: feed raw data in one

end and the finished product (information) comes out the other.

And we like to think about all code this way.

Programming Is About Code, But Programs Are

Tip 49

About Data

FINDING TRANSFORMATIONS

Sometimes the easiest way to find the transformations is to start with the requirement and determine its inputs and outputs.

Now you’ve defined the function representing the overall

program. You can then find steps that lead you from input to output. This is a top-down approach.

For example, you want to create a website for folks playing word games that finds all the words that can be made from a set of letters. Your input here is a set of letters, and your output is a list of three-letter words, four-letter words, and so on:

"lvyin"

is transformed to →

3 => ivy, lin, nil, yin

4 => inly, liny, viny

5 => vinyl

(Yes, they are all words, at least according to the macOS

dictionary.)

The trick behind the overall application is simple: we have a dictionary which groups words by a signature, chosen so that all

words containing the same letters will have the same signature.

The simplest signature function is just the sorted list of letters in the word. We can then look up an input string by generating a signature for it, and then seeing which words (if any) in the dictionary have that same signature.

Thus the anagram finder breaks down into four separate transformations:

Ste

Transformation

Sample data

p

Step

Initial input

"ylvin"

0:

Step

All combinations of three or more letters

1:

vin, viy,

vil, vny, vnl, vyl, iny, inl, iyl,

nyl, viny,

vinl, viyl, vnyl, inyl, vinyl

Step

Signatures of the combinations

2:

inv, ivy, ilv, nvy,

lnv, lvy, iny, iln, ily, lny, invy,

ilnv, ilvy,

lnvy, ilny, ilnvy

Step

3:

List of all dictionary words which match

ivy, yin, nil, lin, viny, liny, inly,

any of the

vinyl

signatures

Step

Words grouped by length

4:

3 => ivy, lin, nil, yin

4 => inly, liny, viny

5 => vinyl

Transformations All the Way Down

Let’s start by looking at step 1, which takes a word and creates a list of all combinations of three or more letters. This step can itself be expressed as a list of transformations:

Step

Transformation

Sample data

Step 1.0:

Initial input

"vinyl"

Step 1.1:

Convert to characters

v, i, n, y, l

Step 1.2:

Get all subsets

[],

[v],

[i],

…

[v,i],

[v,n],

[v,y],

…

[v,i,n],

[v,i,y],

…

[v,n,y,l],

[i,n,y,l],

[v,i,n,y,l]

Step 1.3:

Only those longer than three characters

[v,i,n],

[v,i,y],

…

[i,n,y,l],

[v,i,n,y,l]

Step 1.4:

Convert back to strings

[vin,viy, … inyl,vinyl]

We’ve now reached the point where we can easily implement

each transformation in code (using Elixir in this case):

function-pipelines/anagrams/lib/anagrams.ex

defp all_subsets_longer_than_three_characters(word) do

word

|> String.codepoints()

|> Comb.subsets()

|> Stream.filter(fn subset -> length(subset) >= 3 end)

|> Stream.map(&List.to_string(&1))

end

What’s with the |> Operator?

Elixir, along with many other functional languages, has a

pipeline operator, sometimes called a forward pipe or just a pipe.[41] All it does is take the value on its left and insert it as the first parameter of the function on its right, so

"vinyl" |> String.codepoints |> Comb.subsets() is the same as writing

Comb.subsets(String.codepoints( "vinyl" ))

(Other languages may inject this piped value as the last parameter of the next function—it largely depends on the style of the built-in libraries.)

You might think that this is just syntactic sugar. But in a very real way the pipeline operator is a revolutionary opportunity to think differently. Using a pipeline means that you’re

automatically thinking in terms of transforming data; each time you see |> you’re actually seeing a place where data is flowing between one transformation and the next.

Many languages have something similar: Elm, F#, and Swift

have |>, Clojure has -> and ->> (which work a little differently), R

has %>%. Haskell both has pipe operators and makes it easy to declare new ones. As we write this, there’s talk of adding |> to JavaScript.

If your current language supports something similar, you’re in luck. If it doesn’t, see Language X Doesn’t Have Pipelines.

Anyway, back to the code.

Keep on Transforming…

Now look at Step 2 of the main program, where we convert the subsets into signatures. Again, it’s a simple transformation—a list of subsets becomes a list of signatures:

Step

Transformation

Sample data

Step 2.0:

initial input

vin, viy, … inyl, vinyl

Step 2.1:

convert to signatures

inv, ivy … ilny, inlvy

The Elixir code in the following listing is just as simple:

function-pipelines/anagrams/lib/anagrams.ex

defp as_unique_signatures(subsets) do

subsets

|> Stream.map(&Dictionary.signature_of/1)

end

Now we transform that list of signatures: each signature gets mapped to the list of known words with the same signature, or nil if there are no such words. We then have to remove the nils and flatten the nested lists into a single level:

function-pipelines/anagrams/lib/anagrams.ex

defp find_in_dictionary(signatures) do

signatures

|> Stream.map(&Dictionary.lookup_by_signature/1)

|> Stream.reject(&is_nil/1)

|> Stream.concat(&(&1))

end

Step 4, grouping the words by length, is another simple

transformation, converting our list into a map where the keys are the lengths, and the values are all words with that length:

function-pipelines/anagrams/lib/anagrams.ex

defp group_by_length(words) do

words

|> Enum.sort()

|> Enum.group_by(&String.length/1)

end

Language X Doesn't Have Pipelines

Pipelines have been around for a long time, but only in niche languages. They’ve only moved into the mainstream recently, and many popular languages still don’t support the concept.

The good news is that thinking in transformations doesn’t require a particular language syntax: it’s more a philosophy of design. You still construct your code as transformations, but you write them as a series of assignments: const content = File.read(file_name);

const lines = find_matching_lines(content, pattern)

const result = truncate_lines(lines)

It’s a little more tedious, but it gets the job done.

Putting It All Together

We’ve written each of the individual transformations. Now it’s time to string them all together into our main function:

function-pipelines/anagrams/lib/anagrams.ex

def anagrams_in(word) do

word

|> all_subsets_longer_than_three_characters()

|> as_unique_signatures()

|> find_in_dictionary()

|> group_by_length()

end

Does it work? Let’s try it:

iex(1)> Anagrams.anagrams_in "lyvin"

%{

3 => ["ivy", "lin", "nil", "yin"],

4 => ["inly", "liny", "viny"],

5 => ["vinyl"]

}

WHY IS THIS SO GREAT?

Let’s look at the body of the main function again:

word

|> all_subsets_longer_than_three_characters()

|> as_unique_signatures()

|> find_in_dictionary()

|> group_by_length()

It’s simply a chain of the transformations needed to meet our requirement, each taking input from the previous

transformation and passing output to the next. That comes

about as close to literate code as you can get.

But there’s something deeper, too. If your background is object-oriented programming, then your reflexes demand that you

hide data, encapsulating it inside objects. These objects then chatter back and forth, changing each other’s state. This

introduces a lot of coupling, and it is a big reason that OO

systems can be hard to change.

Tip 50

Don’t Hoard State; Pass It Around

In the transformational model, we turn that on its head. Instead of little pools of data spread all over the system, think of data as a mighty river, a flow. Data becomes a peer to functionality: a pipeline is a sequence of code → data → code → data…. The

data is no longer tied to a particular group of functions, as it is in a class definition. Instead it is free to represent the unfolding progress of our application as it transforms its inputs into its outputs. This means that we can greatly reduce coupling: a

function can be used (and reused) anywhere its parameters

match the output of some other function.

Yes, there is still a degree of coupling, but in our experience it’s more manageable than the OO-style of command and control.

And, if you’re using a language with type checking, you’ll get compile-time warnings when you try to connect two

incompatible things.

WHAT ABOUT ERROR HANDLING?

So far our transforms have worked in a world where nothing

goes wrong. How can we use them in the real world, though? If we can only build linear chains, how can we add all that

conditional logic that we need for error checking?

There are many ways of doing this, but they all rely on a basic convention: we never pass raw values between transformations.

Instead, we wrap them in a data structure (or type) which also tells us if the contained value is valid. In Haskell, for example, this wrapper is called Maybe. In F# and Scala it’s Option.

How you use this concept is language specific. In general,

though, there are two basic ways of writing the code: you can

handle checking for errors inside your transformations or outside them.

Elixir, which we’ve used so far, doesn’t have this support built in. For our purposes this is a good thing, as we get to show an implementation from the ground up. Something similar should

work in most other languages.

First, Choose a Representation

We need a representation for our wrapper (the data structure that carries around a value or an error indication). You can use structures for this, but Elixir already has a pretty strong

convention: functions tend to return a tuple containing either

{:ok, value} or {:error, reason}. For example, File.open returns either :ok and an IO process or :error and a reason code:

iex(1)> File.open( "/etc/passwd" )

{:ok, #PID<0.109.0>}

iex(2)> File.open( "/etc/wombat" )

{:error, :enoent}

We’ll use the :ok/:error tuple as our wrapper when passing things through a pipeline.

Then Handle It Inside Each Transformation

Let’s write a function that returns all the lines in a file that contain a given string, truncated to the first 20 characters. We want to write it as a transformation, so the input will be a file name and a string to match, and the output will be either an :ok tuple with a list of lines or an :error tuple with some kind of reason. The top-level function should look something like this:

function-pipelines/anagrams/lib/grep.ex

def find_all(file_name, pattern) do

File.read(file_name)

|> find_matching_lines(pattern)

|> truncate_lines()

end

There’s no explicit error checking here, but if any step in the pipeline returns an error tuple then the pipeline will return that error without executing the functions that follow.[42] We do this using Elixir’s pattern matching:

function-pipelines/anagrams/lib/grep.ex

defp find_matching_lines({ :ok, content}, pattern) do

content

|> String.split( ~r/\n/)

|> Enum.filter(&String.match?(&1, pattern))

|> ok_unless_empty()

end

defp find_matching_lines(error, _), do: error

# ----------

defp truncate_lines({ :ok, lines }) do

lines

|> Enum.map(&String.slice(&1, 0, 20))

|> ok()

end

defp truncate_lines(error), do: error

# ----------

defp ok_unless_empty([]), do: error( "nothing found" )

defp ok_unless_empty(result), do: ok(result)

defp ok(result), do: { :ok, result }

defp error(reason), do: { :error, reason }

Have a look at the function find_matching_lines. If its first parameter is an :ok tuple, it uses the content in that tuple to find

lines matching the pattern. However, if the first parameter is not an :ok tuple, the second version of the function runs, which just returns that parameter. This way the function simply

forwards an error down the pipeline. The same thing applies to truncate_lines.

We can play with this at the console:

iex> Grep.find_all "/etc/passwd" , ~r/www/

{:ok, ["_www:*:70:70:World W", "_wwwproxy:*:252:252:"]}

iex> Grep.find_all "/etc/passwd" , ~r/wombat/

{:error, "nothing found"}

iex> Grep.find_all "/etc/koala" , ~r/www/

{:error, :enoent}

You can see that an error anywhere in the pipeline immediately becomes the value of the pipeline.

Or Handle It in the Pipeline

You might be looking at the find_matching_lines and truncate_lines functions thinking that we’ve moved the burden of error

handling into the transformations. You’d be right. In a language which uses pattern matching in function calls, such as Elixir, the effect is lessened, but it’s still ugly.

It would be nice if Elixir had a version of the pipeline operator |> that knew about the :ok/:error tuples and which short-circuited execution when an error occurred. [43 ]But the fact that it doesn’t allows us to add something similar, and in a way that is

applicable to a number of other languages.

The problem we face is that when an error occurs we don’t want to run code further down the pipeline, and that we don’t want that code to know that this is happening. This means that we

need to defer running pipeline functions until we know that previous steps in the pipeline were successful. To do this, we’ll need to change them from function calls into function values that can be called later. Here’s one implementation:

function-pipelines/anagrams/lib/grep1.ex

defmodule Grep1 do

def and_then({ :ok, value }, func), do: func.(value)

def and_then(anything_else, _func), do: anything_else

def find_all(file_name, pattern) do

File.read(file_name)

|> and_then(&find_matching_lines(&1, pattern))

|> and_then(&truncate_lines(&1))

end

defp find_matching_lines(content, pattern) do

content

|> String.split( ~r/\n/)

|> Enum.filter(&String.match?(&1, pattern))

|> ok_unless_empty()

end

defp truncate_lines(lines) do

lines

|> Enum.map(&String.slice(&1, 0, 20))

|> ok()

end

defp ok_unless_empty([]), do: error( "nothing found" )

defp ok_unless_empty(result), do: ok(result)

defp ok(result), do: { :ok, result }

defp error(reason), do: { :error, reason }

end

The and_then function is an example of a bind function: it takes a value wrapped in something, then applies a function to that

value, returning a new wrapped value. Using the and_then function in the pipeline takes a little extra punctuation because Elixir needs to be told to convert function calls into function values, but that extra effort is offset by the fact that the transforming functions become simple: each just takes a value (and any extra parameters) and returns {:ok, new_value} or {:error, reason}.

TRANSFORMATIONS TRANSFORM PROGRAMMING

Thinking of code as a series of (nested) transformations can be a liberating approach to programming. It takes a while to get used to, but once you’ve developed the habit you’ll find your code becomes cleaner, your functions shorter, and your designs

flatter.

Give it a try.

RELATED SECTIONS INCLUDE

Topic 8, The Essence of Good Design

Topic 17, Shell Games

Topic 26, How to Balance Resources

Topic 28, Decoupling

Topic 35, Actors and Processes

EXERCISES

Exercise 21 (possible answer)

Can you express the following requirements as a top-level

transformation? That is, for each, identify the input and the output.

1. Shipping and sales tax are added to an order 2. Your application loads configuration information from a named file 3. Someone logs in to a web application

Exercise 22 (possible answer)

You’ve identified the need to validate and convert an input field from a string into an integer between 18 and 150. The overall transformation is described by

field contents as string

→ [validate & convert]

→ {:ok, value} | {:error, reason}

Write the individual transformations that make up validate & convert.

Exercise 23 (possible answer)

In Language X Doesn’t Have Pipelines we wrote:

const content = File.read(file_name);

const lines = find_matching_lines(content, pattern)

const result = truncate_lines(lines)

Many people write OO code by chaining together method calls, and might be tempted to write this as something like:

const result = content_of(file_name)

.find_matching_lines(pattern)

.truncate_lines()

What’s the difference between these two pieces of code? Which do you think we prefer?

Topic 31

Inheritance Tax

Do you program in an object-

oriented language? Do you use

You wanted a banana

inheritance?

but what you got was

a gorilla holding the

If so, stop! It probably isn’t what

banana and the entire

you want to do.

jungle.

Let’s see why.

Joe Armstrong

SOME BACKGROUND

Inheritance first appeared in Simula 67 in 1969. It was an

elegant solution to the problem of queuing multiple types of events on the same list. The Simula approach was to use

something called prefix classes. You could write something like this:

link CLASS car;

... implementation of car

link CLASS bicycle;

... implementation of bicycle

The link is a prefix class that adds the functionality of linked lists. This lets you add both cars and bicycles to the list of things waiting at (say) a traffic light. In current terminology, link would be a parent class.

The mental model used by Simula programmers was that the instance data and implementation of class link was prepended to the implementation of classes car and bicycle. The link part was almost viewed as being a container that carried around cars and bicycles. This gave them a form of polymorphism: cars and

bicycles both implemented the link interface because they both contained the link code.

After Simula came Smalltalk. Alan Kay, one of the creators of Smalltalk, describes in a 2019 Quora answer[44] why Smalltalk has inheritance:

So when I designed Smalltalk-72—and it was a lark for fun while thinking about Smalltalk-71—I thought it would be fun to use its Lisp-like dynamics to do experiments with「differential

programming」(meaning: various ways to accomplish「this is

like that except」).

This is subclassing purely for behavior.

These two styles of inheritance (which actually had a fair

amount in common) developed over the following decades. The

Simula approach, which suggested inheritance was a way of

combining types, continued in languages such as C++ and Java.

The Smalltalk school, where inheritance was a dynamic

organization of behaviors, was seen in languages such as Ruby and JavaScript.

So, now we’re faced with a generation of OO developers who use inheritance for one of two reasons: they don’t like typing, or they like types.

Those who don’t like typing save their fingers by using

inheritance to add common functionality from a base class into child classes: class User and class Product are both subclasses of ActiveRecord::Base.

Those who like types use inheritance to express the relationship between classes: a Car is-a-kind-of Vehicle.

Unfortunately both kinds of inheritance have problems.

PROBLEMS USING INHERITANCE TO SHARE CODE

Inheritance is coupling. Not only is the child class coupled to the parent, the parent’s parent, and so on, but the code that uses the child is also coupled to all the ancestors. Here’s an example:

class Vehicle

def initialize

@speed = 0

end

def stop

@speed = 0

end

def move_at(speed)

@speed = speed

end

end

class Car < Vehicle

def info

"I'm car driving at #{@speed }"

end

end

# top-level code

my_ride = Car.new

my_ride.move_at(30)

When the top-level calls my_car.move_at, the method being

invoked is in Vehicle, the parent of Car.

Now the developer in charge of Vehicle changes the API, so

move_at becomes set_velocity, and the instance variable @speed becomes @velocity.

An API change is expected to break clients of Vehicle class. But the top-level is not: as far as it is concerned it is using a Car.

What the Car class does in terms of implementation is not the concern of the top-level code, but it still breaks.

Similarly the name of an instance variable is purely an internal implementation detail, but when Vehicle changes it also (silently) breaks Car.

So much coupling.

Problems Using Inheritance to Build Types

Some folks view inheritance as a way of

defining new types. Their favorite design

diagram shows class hierarchies. They view

problems the way Victorian gentleman

scientists viewed nature, as something to be

broken down into categories.

Unfortunately, these diagrams soon grow into wall-covering

monstrosities, layer-upon-layer added in order to express the smallest nuance of differentiation between classes. This added complexity can make the application more brittle, as changes can ripple up and down many layers.

Even worse, though, is the multiple inheritance issue. A Car may be a kind of Vehicle, but it can also be a kind of Asset, InsuredItem, LoanCollateral and so on. Modeling this correctly would need

multiple inheritance.

C++ gave multiple inheritance a bad name in

the 1990s because of some questionable

disambiguation semantics. As a result, many

current OO languages don’t offer it. So, even

if you’re happy with complex type trees, you

won’t be able to model your domain

accurately anyway.

Tip 51

Don’t Pay Inheritance Tax

THE ALTERNATIVES ARE BETTER

Let us suggest three techniques that mean you should never

need to use inheritance again:

Interfaces and protocols

Delegation

Mixins and traits

Interfaces and Protocols

Most OO languages allow you to specify that a class implements one or more sets of behaviors. You could say, for example, that a Car class implements the Drivable behavior and the Locatable behavior. The syntax used for doing this varies: in Java, it might look like this:

public class Car implements Drivable, Locatable {

// Code for class Car. This code must include

// the functionality of both Drivable

// and Locatable

}

Drivable and Locatable are what Java calls interfaces; other languages call them protocols, and some call them traits (although this is not what we’ll be calling a trait later).

Interfaces are defined like this:

public interface Drivable {

double getSpeed();

void stop();

}

public interface Locatable() {

Coordinate getLocation();

boolean locationIsValid();

}

These declarations create no code: they simply say that any

class that implements Drivable must implement the two methods getSpeed and stop, and a class that’s Locatable must implement getLocation and locationIsValid. This means that our previous class definition of Car will only be valid if it includes all four of these methods.

What makes interfaces and protocols so powerful is that we can use them as types, and any class that implements the

appropriate interface will be compatible with that type. If Car and Phone both implement Locatable, we could store both in a list of locatable items:

List<Locatable> items = new ArrayList<>();

items.add(new Car(...));

items.add(new Phone(...));

items.add(new Car(...));

// ...

We can then process that list, safe in the knowledge that every item has getLocation and locationIsValid:

void printLocation(Locatable item) {

if (item.locationIsValid() {

print(item.getLocation().asString());

}

// ...

items.forEach(printLocation);

Tip 52

Prefer Interfaces to Express Polymorphism

Interfaces and protocols give us polymorphism without

inheritance.

Delegation

Inheritance encourages developers to create classes whose

objects have large numbers of methods. If a parent class has 20

methods, and the subclass wants to make use of just two of

them, its objects will still have the other 18 just lying around and callable. The class has lost control of its interface. This is a

common problem—many persistence and UI frameworks insist that application components subclass some supplied base class:

class Account < PersistenceBaseClass

end

The Account class now carries all of the persistence class’s API around with it. Instead, imagine an alternative using delegation, as in the following example:

class Account

def initialize(. . .)

@repo = Persister.for(self)

end

def save

@repo.save()

end

end

We now expose none of the framework API to the clients of our Account class: that decoupling is now broken. But there’s more.

Now that we’re no longer constrained by the API of the

framework we’re using, we’re free to create the API we need.

Yes, we could do that before, but we always ran the risk that the interface we wrote can be bypassed, and the persistence API used instead. Now we control everything.

Tip 53

Delegate to Services: Has-A Trumps Is-A

In fact, we can take this a step further. Why should an Account have to know how to persist itself? Isn’t its job to know and enforce the account business rules?

class Account

# nothing but account stuff

end

class AccountRecord

# wraps an account with the ability

# to be fetched and stored

end

Now we’re really decoupled, but it has come at a cost. We’re having to write more code, and typically some of it will be

boilerplate: it’s likely that all our record classes will need a find method, for example.

Fortunately, that’s what mixins and traits do for us.

Mixins, Traits, Categories, Protocol Extensions, …

As an industry, we love to give things names. Quite often we’ll give the same thing many names. More is better, right?

That’s what we’re dealing with when we look at mixins. The

basic idea is simple: we want to be able to extend classes and objects with new functionality without using inheritance. So we create a set of these functions, give that set a name, and then somehow extend a class or object with them. At that point,

you’ve created a new class or object that combines the

capabilities of the original and all its mixins. In most cases, you’ll be able to make this extension even if you don’t have access to the source code of the class you’re extending.

Now the implementation and name of this feature varies

between languages. We’ll tend to call them mixins here, but we really want you to think of this as a language-agnostic feature.

The important thing is the capability that all these

implementations have: merging functionality between existing things and new things.

As an example, let’s go back to our AccountRecord example. As we left it, an AccountRecord needed to know about both accounts and about our persistence framework. It also needed to delegate all the methods in the persistence layer that it wanted to expose to the outside world.

Mixins give us an alternative. First, we could write a mixin that implements (for example) two of three of the standard finder methods. We could then add them into AccountRecord as a mixin.

And, as we write new classes for persisted things, we can add the mixin to them, too:

mixin CommonFinders {

def find(id) { ... }

def findAll() { ... }

end

class AccountRecord extends BasicRecord with CommonFinders

class OrderRecord extends BasicRecord with CommonFinders We can take this a lot further. For example, we all know our business objects need validation code to prevent bad data from infiltrating our calculations. But exactly what do we mean by validation?

If we take an account, for example, there are probably many

different layers of validation that could be applied:

Validating that a hashed password matches one entered by the user Validating form data entered by the user when an account is

created

Validating form data entered by an admin person updating the user details

Validating data added to the account by other system components

Validating data for consistency before it is persisted A common (and we believe less-than-ideal) approach is to

bundle all the validations into a single class (the business object/persistence object) and then add flags to control which fire in which circumstances.

We think a better way is to use mixins to create specialized classes for appropriate situations:

class AccountForCustomer extends Account

with AccountValidations,AccountCustomerValidations

class AccountForAdmin extends Account

with AccountValidations,AccountAdminValidations

Here, both derived classes include validations common to all account objects. The customer variant also includes validations appropriate for the customer-facing APIs, while the admin

variant contained (the presumably less restrictive) admin

validations.

Now, by passing instances of AccountForCustomer or AccountForAdmin back and forth, our code automatically ensures the correct validation is applied.

Tip 54

Use Mixins to Share Functionality

INHERITANCE IS RARELY THE ANSWER

We’ve had a quick look at three alternatives to traditional class inheritance:

Interfaces and protocols

Delegation

Mixins and traits

Each of these methods may be better for you in different

circumstances, depending on whether your goal is sharing type information, adding functionality, or sharing methods. As with anything in programming, aim to use the technique that best

expresses your intent.

And try not to drag the whole jungle along for the ride.

RELATED SECTIONS INCLUDE

Topic 8, The Essence of Good Design

Topic 10, Orthogonality

Topic 28, Decoupling

CHALLENGES

The next time you find yourself subclassing, take a minute to examine the options. Can you achieve what you want with

interfaces, delegation, and/or mixins? Can you reduce coupling by doing so?

Topic 32

Configuration

When code relies on values that

may change after the application

Let all your things

has gone live, keep those values

have their places; let

external to the app. When your

each part of your

application will run in different

business have its time.

environments, and potentially for

different customers, keep the

Benjamin Franklin, Thirteen

environment- and customer-

Virtues, autobiography

specific values outside the app. In

this way, you’re parameterizing

your application; the code adapts to the places it runs.

Parameterize Your App Using External

Tip 55

Configuration

Common things you will probably want to put in configuration data include:

Credentials for external services (database, third party APIs, and so on)

Logging levels and destinations

Port, IP address, machine, and cluster names the app uses

Environment-specific validation parameters

Externally set parameters, such as tax rates

Site-specific formatting details

License keys

Basically, look for anything that you know will have to change that you can express outside your main body of code, and slap it into some configuration bucket.

STATIC CONFIGURATION

Many frameworks, and quite a few custom applications, keep

configuration in either flat files or database tables. If the information is in flat files, the trend is to use some off-the-shelf plain-text format. Currently YAML and JSON are popular for

this. Sometimes applications written in scripting languages use special purpose source-code files, dedicated to containing just configuration. If the information is structured, and is likely to be changed by the customer (sales tax rates, for example), it might be better to store it in a database table. And, of course, you can use both, splitting the configuration information

according to use.

Whatever form you use, the configuration is read into your

application as a data structure, normally when the application starts. Commonly, this data structure is made global, the

thinking being that this makes it easier for any part of the code to get to the values it holds.

We prefer that you don’t do that. Instead, wrap the

configuration information behind a (thin) API. This decouples your code from the details of the representation of

configuration.

CONFIGURATION-AS-A-SERVICE

While static configuration is common, we currently favor a

different approach. We still want configuration data kept external to the application, but rather than in a flat file or database, we’d like to see it stored behind a service API. This has a number of benefits:

Multiple applications can share configuration information, with authentication and access control limiting what each can see Configuration changes can be made globally

The configuration data can be maintained via a specialized UI The configuration data becomes dynamic

That last point, that configuration should be dynamic, is critical as we move toward highly available applications. The idea that we should have to stop and restart an application to change a single parameter is hopelessly out of touch with modern

realities. Using a configuration service, components of the

application could register for notifications of updates to

parameters they use, and the service could send them messages containing new values if and when they are changed.

Whatever form it takes, configuration data drives the runtime behavior of an application. When configuration values change, there’s no need to rebuild the code.

DON’T WRITE DODO-CODE

Without external configuration, your code is not as adaptable or flexible as it could be. Is this a bad thing? Well, out here in the real world, species that don’t adapt die.

The dodo didn’t adapt to the presence of humans and their

livestock on the island of Mauritius, and quickly became extinct.

[45]

[45] It was the first documented extinction of a species at the hand of man.

Don’t let your project (or your career) go the way of the dodo.

images/dodo.png

RELATED SECTIONS INCLUDE

Topic 9, DRY—The Evils of Duplication

Topic 14, Domain Languages

Topic 16, The Power of Plain Text

Topic 28, Decoupling

Don't Overdo It

In the first edition of this book, we suggested using configuration instead of code in a similar fashion, but apparently should have been a little more specific in our instructions. Any advice can be taken to extremes or used inappropriately, so here are a few cautions:

Don’t overdo it. One early client of ours decided that every single field in their application should be configurable. As a result, it took weeks to make even the smallest change, as you had to implement both the field and all the admin code to save and edit it. They had some 40,000 configuration variables and a coding nightmare on their hands.

Don’t push decisions to configuration out of laziness. If there’s genuine debate about whether a feature should work this way or that, or if it should be the users’ choice, try it out one way and get feedback on whether the decision was a good one.

Footnotes

[37] So it’s not really a law. It’s more like The Jolly Good Idea of Demeter.

[38] https://media.pragprog.com/articles/jan_03_enbug.pdf

[39] Yes, we know that Ruby already has this capability with its at_exit function.

[40] https://media.pragprog.com/titles/tpp20/code/event/rxcommon/logger.js

[41] It seems that the first use of the characters |> as a pipe dates to 1994, in a discussion about the language Isobelle/ML, archived at

https://blogs.msdn.microsoft.com/dsyme/2011/05/17/archeological-semiotics-the-

birth-of-the-pipeline-symbol-1994/

[42] We’ve taken a liberty here. Technically we do execute the following functions. We just don’t execute the code in them.

[43] In fact you could add such an operator to Elixir using its macro facility; an example of this is the Monad library in hex. You could also use Elixir’s with construct, but then you lose much of the sense of writing transformations that you get with pipelines.

[44] https://www.quora.com/What-does-Alan-Kay-think-about-inheritance-in-object-

oriented-programming

[45] It didn’t help that the settlers beat the placid (read: stupid) birds to death with clubs for sport.

Copyright © 2020 Pearson Education, Inc.

Chapter 6

Concurrency

Just so we’re all on the same page, let’s start with some

definitions:

Concurrency is when the execution of two or more pieces of code act as if they run at the same time. Parallelism is when they do run at the same time.

To have concurrency, you need to run code in an environment

that can switch execution between different parts of your code when it is running. This is often implemented using things such as fibers, threads, and processes.

To have parallelism, you need hardware that can do two things at once. This might be multiple cores in a CPU, multiple CPUs in a computer, or multiple computers connected together.

Everything Is Concurrent

It’s almost impossible to write code in a decent-sized system that doesn’t have concurrent aspects to it. They may be explicit, or they may be buried inside a library. Concurrency is a

requirement if you want your application to be able to deal with the real world, where things are asynchronous: users are

interacting, data is being fetched, external services are being called, all at the same time. If you force this process to be serial, with one thing happening, then the next, and so on, your system feels sluggish and you’re probably not taking full advantage of the power of the hardware on which it runs.

In this chapter we’ll look at concurrency and parallelism.

Developers often talk about coupling between chunks of code.

They’re referring to dependencies, and how those dependencies make things hard to change. But there’s another form of

coupling. Temporal coupling happens when your code imposes a sequence on things that is not required to solve the problem at hand. Do you depend on the「tick」coming before the「tock」?

Not if you want to stay flexible. Does your code access multiple back-end services sequentially, one after the other? Not if you

want to keep your customers. In Topic 33, Breaking Temporal

Coupling, we’ll look at ways of identifying this kind of temporal coupling.

Why is writing concurrent and parallel code so difficult? One reason is that we learned to program using sequential systems, and our languages have features that are relatively safe when used sequentially but become a liability once two things can

happen at the same time. One of the biggest culprits here is shared state. This doesn’t just mean global variables: any time two or more chunks of code hold references to the same piece of

mutable data, you have shared state. And Topic 34, Shared

State Is Incorrect State. The section describes a number of

workarounds for this, but ultimately they’re all error prone.

If that makes you feed sad, nil desperandum! There are better ways to construct concurrent applications. One of these is using the actor model, where independent processes, which share no data, communicate over channels using defined, simple,

semantics. We talk about both the theory and practice of this approach in Topic 35, Actors and Processes.

Finally, we’ll look at Topic 36, Blackboards. These are systems which act like a combination of an object store and a smart

publish/subscribe broker. In their original form, they never really took off. But today we’re seeing more and more

implementations of middleware layers with blackboard-like

semantics. Used correctly, these types of systems offer a serious amount of decoupling.

Concurrent and parallel code used to be exotic. Now it is

required.

Topic 33

Breaking Temporal Coupling

「What is temporal coupling all about?」, you may ask. It’s about time.

Time is an often ignored aspect of software architectures. The only time that preoccupies us is the time on the schedule, the time left until we ship—but this is not what we’re talking about here. Instead, we are talking about the role of time as a design element of the software itself. There are two aspects of time that are important to us: concurrency (things happening at the same time) and ordering (the relative positions of things in time).

We don’t usually approach programming with either of these

aspects in mind. When people first sit down to design an

architecture or write a program, things tend to be linear. That’s the way most people think— do this and then always do that. But thinking this way leads to temporal coupling: coupling in time.

Method A must always be called before method B; only one

report can be run at a time; you must wait for the screen to redraw before the button click is received. Tick must happen before tock.

This approach is not very flexible, and not very realistic.

We need to allow for concurrency and to think about decoupling any time or order dependencies. In doing so, we can gain

flexibility and reduce any time-based dependencies in many

areas of development: workflow analysis, architecture, design,

and deployment. The result will be systems that are easier to reason about, that potentially respond faster and more reliably.

LOOKING FOR CONCURRENCY

On many projects, we need to model and analyze the application workflows as part of the design. We’d like to find out what can happen at the same time, and what must happen in a strict order. One way to do this is to capture the workflow using a notation such as the activity diagram.[46]

Tip 56

Analyze Workflow to Improve Concurrency

An activity diagram consists of a set of actions drawn as

rounded boxes. The arrow leaving an action leads to either

another action (which can start once the first action completes) or to a thick line called a synchronization bar. Once all the actions leading into a synchronization bar are complete, you can then proceed along any arrows leaving the bar. An action with no arrows leading into it can be started at any time.

You can use activity diagrams to maximize parallelism by

identifying activities that could be performed in parallel, but aren’t.

For instance, we may be writing the software for a robotic piña colada maker. We’re told that the steps are:

1. Open blender

1. Close blender

2. Open piña colada mix

2. Liquefy for 1 minute

3. Put mix in blender

3. Open blender

4. Measure 1/2 cup white rum

4. Get glasses

5. Pour in rum

5. Get pink umbrellas

6. Add 2 cups of ice

6. Serve

However, a bartender would lose their job if they followed these steps, one by one, in order. Even though they describe these actions serially, many of them could be performed in parallel.

We’ll use the following activity diagram to capture and reason about potential concurrency.

images/pina-colada.png

It can be eye-opening to see where the dependencies really exist.

In this instance, the top-level tasks (1, 2, 4, 10, and 11) can all happen concurrently, up front. Tasks 3, 5, and 6 can happen in parallel later. If you were in a piña colada-making contest, these optimizations may make all the difference.

Faster Formatting

This book is written in plain text. To build the version to be printed, or an ebook, or whatever, that text is fed through a pipeline of processors. Some look for particular constructs (bibliography citations, index entries, special markup for tips, and so on).

Other processors operate on the document as a whole.

Many of the processors in the pipeline have to access external information (reading files, writing files, piping through external programs). All this relatively slow speed work gives us the opportunity to exploit concurrency: in fact each step in the pipeline executes concurrently, reading from the previous step and writing to the next.

In addition, some parts of the process are relatively processor intensive. One of these is the conversion of mathematical formulae. For various historical reasons each equation can take up to 500ms to convert. To speed things up, we take advantage of parallelism. Because each formula is independent of the others, we convert each in its own parallel process and collect the results back into the book as they become available.

As a result, the book builds much, much faster on multicore machines.

(And, yes, we did indeed discover a number of concurrency errors in our pipeline along the way….)

OPPORTUNITIES FOR CONCURRENCY

Activity diagrams show the potential areas of concurrency, but have nothing to say about whether these areas are worth

exploiting. For example, in the piña colada example, a bartender would need five hands to be able to run all the potential initial tasks at once.

And that’s where the design part comes in. When we look at the activities, we realize that number 8, liquify, will take a minute.

During that time, our bartender can get the glasses and

umbrellas (activities 10 and 11) and probably still have time to serve another customer.

And that’s what we’re looking for when we’re designing for

concurrency. We’re hoping to find activities that take time, but not time in our code. Querying a database, accessing an external

service, waiting for user input: all these things would normally stall our program until they complete. And these are all

opportunities to do something more productive than the CPU

equivalent of twiddling one’s thumbs.

OPPORTUNITIES FOR PARALLELISM

Remember the distinction: concurrency is a software

mechanism, and parallelism is a hardware concern. If we have multiple processors, either locally or remotely, then if we can split work out among them we can reduce the overall time

things take.

The ideal things to split this way are pieces of work that are relatively independent—where each can proceed without

waiting for anything from the others. A common pattern is to take a large piece of work, split it into independent chunks, process each in parallel, then combine the results.

An interesting example of this in practice is the way the

compiler for the Elixir language works. When it starts, it splits the project it is building into modules, and compiles each in parallel. Sometimes a module depends on another, in which

case its compilation pauses until the results of the other

module’s build become available. When the top-level module

completes, it means that all dependencies have been compiled.

The result is a speedy compilation that takes advantage of all the cores available.

IDENTIFYING OPPORTUNITIES IS THE EASY PART

Back to your applications. We’ve identified places where it will benefit from concurrency and parallelism. Now for the tricky part: how can we implement it safely. That’s the topic of the rest

of the chapter.

RELATED SECTIONS INCLUDE

Topic 10, Orthogonality

Topic 26, How to Balance Resources

Topic 28, Decoupling

Topic 36, Blackboards

CHALLENGES

How many tasks do you perform in parallel when you get ready for work in the morning? Could you express this in a UML activity diagram? Can you find some way to get ready more quickly by

increasing concurrency?

Topic 34

Shared State Is Incorrect State

You’re in your favorite diner. You finish your main course, and ask your server if there’s any apple pie left. He looks over his shoulder, sees one piece in the display case, and says yes. You order it and sigh contentedly.

Meanwhile, on the other side of the restaurant, another

customer asks their server the same question. She also looks, confirms there’s a piece, and that customer orders.

One of the customers is going to be disappointed.

Swap the display case for a joint bank account, and turn the waitstaff into point-of-sale devices. You and your partner both decide to buy a new phone at the same time, but there’s only enough in the account for one. Someone—the bank, the store, or you—is going to be very unhappy.

Tip 57

Shared State Is Incorrect State

The problem is the shared state. Each server in the restaurant looked into the display case without regard for the other. Each point-of-sale device looked at an account balance without

regard for the other.

NONATOMIC UPDATES

Let’s look at our diner example as if it were code:

images/pie_case.png

The two waiters operate concurrently (and, in real life, in

parallel). Let’s look at their code:

if display_case.pie_count > 0

promise_pie_to_customer()

display_case.take_pie()

give_pie_to_customer()

end

Waiter 1 gets the current pie count, and finds that it is one. He promises the pie to the customer. But at that point, waiter 2

runs. She also sees the pie count is one and makes the same

promise to her customer. One of the two then grabs the last

piece of pie, and the other waiter enters some kind of error state (which probably involves much grovelling).

The problem here is not that two processes can write to the

same memory. The problem is that neither process can

guarantee that its view of that memory is consistent. Effectively, when a waiter executes display_case.pie_count(), they copy the value from the display case into their own memory. If the value in the display case changes, their memory (which they are using to

make decisions) is now out of date.

This is all because the fetching and then updating the pie count is not an atomic operation: the underlying value can change in the middle.

So how can we make it atomic?

Semaphores and Other Forms of Mutual Exclusion

A semaphore is simply a thing that only one person can own at a time. You can create a semaphore and then use it to control

access to some other resource. In our example, we could create a semaphore to control access to the pie case, and adopt the convention that anyone who wants to update the pie case

contents can only do so if they are holding that semaphore.

Say the diner decides to fix the pie problem with a physical semaphore. They place a plastic Leprechaun on the pie case.

Before any waiter can sell a pie, they have to be holding the Leprechaun in their hand. Once their order has been completed (which means delivering the pie to the table) they can return the Leprechaun to its place guarding the treasure of the pies, ready to mediate the next order.

Let’s look at this in code. Classically, the operation to grab the semaphore was called P, and the operation to release it was called V. [47] Today we use terms such as lock/unlock, claim/release, and so on.

case_semaphore.lock()

if display_case.pie_count > 0

promise_pie_to_customer()

display_case.take_pie()

give_pie_to_customer()

end

case_semaphore.unlock()

This code assumes that a semaphore has already been created

and stored in the variable case_semaphore.

Let’s assume both waiters execute the code at the same time.

They both try to lock the semaphore, but only one succeeds. The one that gets the semaphore continues to run as normal. The

one that doesn’t get the semaphore is suspended until the

semaphore becomes available (the waiter waits…). When the

first waiter completes the order they unlock the semaphore and the second waiter continues running. They now see there’s no pie in the case, and apologize to the customer.

There are some problems with this approach. Probably the most significant is that it only works because everyone who accesses the pie case agrees on the convention of using the semaphore. If someone forgets (that is, some developer writes code that

doesn’t follow the convention) then we’re back in chaos.

Make the Resource Transactional

The current design is poor because it delegates responsibility for protecting access to the pie case to the people who use it. Let’s change it to centralize that control. To do this, we have to change the API so that waiters can check the count and also take a slice of pie in a single call:

slice = display_case.get_pie_if_available()

if slice

give_pie_to_customer()

end

To make this work, we need to write a method that runs as part of the display case itself:

def get_pie_if_available() ####

if @slices.size > 0 #

update_sales_data( :pie) #

return @slices.shift #

else # incorrect code!

false #

end #

end ####

This code illustrates a common misconception. We’ve moved

the resource access into a central place, but our method can still be called from multiple concurrent threads, so we still need to protect it with a semaphore:

def get_pie_if_available()

@case_semaphore.lock()

if @slices.size > 0

update_sales_data( :pie)

return @slices.shift

else

false

end

@case_semaphore.unlock()

end

Even this code might not be correct. If update_sales_data raises an exception, the semaphore will never get unlocked, and all future access to the pie case will hang indefinitely. We need to handle this:

def get_pie_if_available()

@case_semaphore.lock()

try {

if @slices.size > 0

update_sales_data( :pie)

return @slices.shift

else

false

end

}

ensure {

@case_semaphore.unlock()

}

end

Because this is such a common mistake, many languages

provide libraries that handle this for you:

def get_pie_if_available()

@case_semaphore.protect() {

if @slices.size > 0

update_sales_data( :pie)

return @slices.shift

else

false

end

}

end

MULTIPLE RESOURCE TRANSACTIONS

Our diner just installed an ice cream freezer. If a customer orders pie à la mode, the waiter will need to check that both pie and ice cream are available.

We could change the waiter code to something like:

slice = display_case.get_pie_if_available()

scoop = freezer.get_ice_cream_if_available()

if slice && scoop

give_order_to_customer()

end

This won’t work, though. What happens if we claim a slice of pie, but when we try to get a scoop of ice cream we find out there isn’t any? We’re now left holding some pie that we can’t do anything with (because our customer must have ice cream). And

the fact we’re holding the pie means it isn’t in the case, so it isn’t available to some other customer who (being a purist) doesn’t want ice cream with it.

We could fix this by adding a method to the case that lets us return a slice of pie. We’ll need to add exception handling to ensure we don’t keep resources if something fails:

slice = display_case.get_pie_if_available()

if slice

try {

scoop = freezer.get_ice_cream_if_available()

if scoop

try {

give_order_to_customer()

}

rescue {

freezer.give_back(scoop)

}

end

}

rescue {

display_case.give_back(slice)

}

end

Again, this is less than ideal. The code is now really ugly: working out what it actually does is difficult: the business logic is buried in all the housekeeping.

Previously we fixed this by moving the resource handling code into the resource itself. Here, though, we have two resources.

Should we put the code in the display case or the freezer?

We think the answer is「no」to both options. The pragmatic

approach would be to say that「apple pie à la mode」is its own resource. We’d move this code into a new module, and then the

client could just say「get me apple pie with ice cream」and it either succeeds or fails.

Of course, in the real world there are likely to be many

composite dishes like this, and you wouldn’t want to write new modules for each. Instead, you’d probably want some kind of

menu item which contained references to its components, and

then have a generic get_menu_item method that does the resource dance with each.

NON-TRANSACTIONAL UPDATES

A lot of attention is given to shared memory as a source of

concurrency problems, but in fact the problems can pop up

anywhere where your application code shares mutable

resources: files, databases, external services, and so on.

Whenever two or more instances of your code can access some

resource at the same time, you’re looking at a potential

problem.

Sometimes, the resource isn’t all that obvious. While writing this edition of the book we updated the toolchain to do more work in parallel using threads. This caused the build to fail, but in bizarre ways and random places. A common thread through

all the errors was that files or directories could not be found, even though they were really in exactly the right place.

We tracked this down to a couple of places in the code which temporarily changed the current directory. In the nonparallel version, the fact that this code restored the directory back was good enough. But in the parallel version, one thread would

change the directory and then, while in that directory, another thread would start running. That thread would expect to be in the original directory, but because the current directory is

shared between threads, that wasn’t the case.

The nature of this problem prompts another tip:

Tip 58

Random Failures Are Often Concurrency Issues

OTHER KINDS OF EXCLUSIVE ACCESS

Most languages have library support for some kind of exclusive access to shared resources. They may call it mutexes (for mutual exclusion), monitors, or semaphores. These are all implemented as libraries.

However, some languages have concurrency support built into

the language itself. Rust, for example, enforces the concept of data ownership; only one variable or parameter can hold a

reference to any particular piece of mutable data at a time.

You could also argue that functional languages, with their

tendency to make all data immutable, make concurrency

simpler. However, they still face the same challenges, because at some point they are forced to step into the real, mutable world.

DOCTOR, IT HURTS…

If you take nothing else away from this section, take this:

concurrency in a shared resource environment is difficult, and managing it yourself is fraught with challenges.

Which is why we’re recommending the punchline to the old

joke:

Doctor, it hurts when I do this.

Then don’t do that.

The next couple of sections suggest alternative ways of getting the benefits of concurrency without the pain.

RELATED SECTIONS INCLUDE

Topic 10, Orthogonality

Topic 28, Decoupling

Topic 38, Programming by Coincidence

Topic 35

Actors and Processes

Actors and processes offer

interesting ways of implementing

Without writers,

concurrency without the burden of

stories would not be

synchronizing access to shared

written,

memory.

Without actors, stories

could not be brought to

Before we get into them, however,

life.

we need to define what we mean.

And this is going to sound

Angie-Marie Delsante

academic. Never fear, we’ll be

working through it all in a short

while.

An actor is an independent virtual processor with its own local (and private) state. Each actor has a mailbox. When a message appears in the mailbox and the actor is idle, it kicks into life and processes the message. When it finishes processing, it processes another message in the mailbox, or, if the mailbox is empty, it goes back to sleep.

When processing a message, an actor can create other actors, send messages to other actors that it knows about, and create a new state that will become the current state when the next message is

processed.

A process is typically a more general-purpose virtual processor, often implemented by the operating system to facilitate

concurrency. Processes can be constrained (by convention) to behave like actors, and that’s the type of process we mean here.

ACTORS CAN ONLY BE CONCURRENT

There are a few things that you won’t find in the definition of actors:

There’s no single thing that’s in control. Nothing schedules what happens next, or orchestrates the transfer of information from the raw data to the final output.

The only state in the system is held in messages and in the local state of each actor. Messages cannot be examined except by being read by their recipient, and local state is inaccessible outside the actor.

All messages are one way—there’s no concept of replying. If you want an actor to return a response, you include your own mailbox address in the message you send it, and it will (eventually) send the response as just another message to that mailbox.

An actor processes each message to completion, and only processes one message at a time.

As a result, actors execute concurrently, asynchronously, and share nothing. If you had enough physical processors, you could run an actor on each. If you have a single processor, then some runtime can handle the switching of context between them.

Either way, the code running in the actors is the same.

Tip 59

Use Actors For Concurrency Without Shared State

A SIMPLE ACTOR

Let’s implement our diner using actors. In this case, we’ll have three (the customer, the waiter, and the pie case).

The overall message flow will look like this:

We (as some kind of external, God-like being) tell the customer that

they are hungry

In response, they’ll ask the waiter for pie

The waiter will ask the pie case to get some pie to the customer If the pie case has a slice available, it will send it to the customer, and also notify the waiter to add it to the bill

If there is no pie, the case tells the waiter, and the waiter apologizes to the customer

We’ve chosen to implement the code in JavaScript using the

Nact library. [48] We’ve added a little wrapper to this that lets us write actors as simple objects, where the keys are the message types that it receives and the values are functions to run when that particular message is received. (Most actor systems have a similar kind of structure, but the details depend on the host language.)

Let’s start with the customer. The customer can receive three messages:

You’re hungry (sent by the external context)

There’s pie on the table (sent by the pie case)

Sorry, there’s no pie (sent by the waiter)

Here’s the code:

concurrency/actors/index.js

const customerActor = {

'hungry for pie' : (msg, ctx, state) => {

return dispatch(state.waiter,

{ type: "order" , customer: ctx.self, wants: 'pie' })

},

'put on table' : (msg, ctx, _state) =>

console.log( `${ctx.self.name} sees " ${msg.food} " appear on the tablè),

'no pie left' : (_msg, ctx, _state) =>

console.log( `${ctx.self.name} sulks…`)

}

The interesting case is when we receive a ‘‘hungry for pie’」

message, where we then send a message off to the waiter. (We’ll see how the customer knows about the waiter actor shortly.)

Here’s the waiter’s code:

concurrency/actors/index.js

const waiterActor = {

"order" : (msg, ctx, state) => {

if (msg.wants == "pie" ) {

dispatch(state.pieCase,

{ type: "get slice" , customer: msg.customer, waiter: ctx.self })

}

else {

console.dir( `Don't know how to order ${msg.wants} `);

}

},

"add to order" : (msg, ctx) =>

console.log( `Waiter adds ${msg.food} to ${msg.customer.name} 's order`

),

"error" : (msg, ctx) => {

dispatch(msg.customer, { type: 'no pie left' , msg: msg.msg });

console.log( `\nThe waiter apologizes to ${msg.customer.name} : ${msg.msg} `)

}

};

When it receives the ’order’ message from the customer, it checks to see if the request is for pie. If so, it sends a request to the pie

case, passing references both to itself and the customer.

The pie case has state: an array of all the slices of pie it holds.

(Again, we see how that gets set up shortly.) When it receives a

’get slice’ message from the waiter, it sees if it has any slices left.

If it does, it passes the slice to the customer, tells the waiter to update the order, and finally returns an updated state,

containing one less slice. Here’s the code:

concurrency/actors/index.js

const pieCaseActor = {

'get slice' : (msg, context, state) => {

if (state.slices.length == 0) {

dispatch(msg.waiter,

{ type: 'error' , msg: "no pie left" , customer: msg.customer })

return state

}

else {

var slice = state.slices.shift() + " pie slice" ;

dispatch(msg.customer,

{ type: 'put on table' , food: slice });

dispatch(msg.waiter,

{ type: 'add to order' , food: slice, customer: msg.customer });

return state;

}

}

}

Although you’ll often find that actors are started dynamically by other actors, in our case we’ll keep it simple and start our actors manually. We will also pass each some initial state:

The pie case gets the initial list of pie slices it contains We’ll give the waiter a reference to the pie case

We’ll give the customers a reference to the waiter

concurrency/actors/index.js

const actorSystem = start();

let pieCase = start_actor(

actorSystem,

'pie-case' ,

pieCaseActor,

{ slices: [ "apple" , "peach" , "cherry" ] });

let waiter = start_actor(

actorSystem,

'waiter' ,

waiterActor,

{ pieCase: pieCase });

let c1 = start_actor(actorSystem, 'customer1' ,

customerActor, { waiter: waiter });

let c2 = start_actor(actorSystem, 'customer2' ,

customerActor, { waiter: waiter });

And finally we kick it off. Our customers are greedy. Customer 1

asks for three slices of pie, and customer 2 asks for two:

concurrency/actors/index.js

dispatch(c1, { type: 'hungry for pie' , waiter: waiter });

dispatch(c2, { type: 'hungry for pie' , waiter: waiter });

dispatch(c1, { type: 'hungry for pie' , waiter: waiter });

dispatch(c2, { type: 'hungry for pie' , waiter: waiter });

dispatch(c1, { type: 'hungry for pie' , waiter: waiter });

sleep(500)

.then(() => {

stop(actorSystem);

})

When we run it, we can see the actors communicating. [49] The order you see may well be different:

$ node index.js

customer1 sees "apple pie slice" appear on the table

customer2 sees "peach pie slice" appear on the table

Waiter adds apple pie slice to customer1's order

Waiter adds peach pie slice to customer2's order

customer1 sees "cherry pie slice" appear on the table

Waiter adds cherry pie slice to customer1's order

The waiter apologizes to customer1: no pie left

customer1 sulks…

The waiter apologizes to customer2: no pie left

customer2 sulks…

NO EXPLICIT CONCURRENCY

In the actor model, there’s no need to write any code to handle concurrency, as there is no shared state. There’s also no need to code in explicit end-to-end「do this, do that」logic, as the actors work it out for themselves based on the messages they receive.

There’s also no mention of the underlying architecture. This set of components work equally well on a single processor, on

multiple cores, or on multiple networked machines.

ERLANG SETS THE STAGE

The Erlang language and runtime are great examples of an actor implementation (even though the inventors of Erlang hadn’t

read the original Actor’s paper). Erlang calls actors processes, but they aren’t regular operating system processes. Instead, just like the actors we’ve been discussing, Erlang processes are

lightweight (you can run millions of them on a single machine), and they communicate by sending messages. Each is isolated

from the others, so there is no sharing of state.

In addition, the Erlang runtime implements a supervision system, which manages the lifetimes of processes, potentially restarting a process or set of processes in case of failure. And Erlang also offers hot-code loading: you can replace code in a

running system without stopping that system. And the Erlang system runs some of the world’s most reliable code, often citing nine nines availability.

But Erlang (and it’s progeny Elixir) aren’t unique—there are actor implementations for most languages. Consider using them for your concurrent implementations.

RELATED SECTIONS INCLUDE

Topic 28, Decoupling

Topic 30, Transforming Programming

Topic 36, Blackboards

CHALLENGES

Do you currently have code that uses mutual exclusion to protect shared data. Why not try a prototype of the same code written using actors?

The actor code for the diner only supports ordering slices of pie.

Extend it to let customers order pie à la mode, with separate agents managing the pie slices and the scoops of ice cream. Arrange things so that it handles the situation where one or the other runs out.

Topic 36

Blackboards

Consider how detectives might use

a blackboard to coordinate and

The writing is on the

solve a murder investigation. The

wall…

chief inspector starts off by setting

up a large blackboard in the

Daniel 5 (ref)

conference room. On it, she writes

a single question:

H. Dumpty (Male, Egg): Accident? Murder?

Did Humpty really fall, or was he pushed? Each detective may make contributions to this potential murder mystery by adding facts, statements from witnesses, any forensic evidence that might arise, and so on. As the data accumulates, a detective might notice a connection and post that observation or

speculation as well. This process continues, across all shifts, with many different people and agents, until the case is closed.

A sample blackboard is shown in the figure.

images/blackboard.png

Figure 2. Someone found a connection between

Humpty’s gambling debts and the phone logs.

Perhaps he was getting threatening phone calls.

Some key features of the blackboard approach are:

None of the detectives needs to know of the existence of any other detective—they watch the board for new information, and add their findings.

The detectives may be trained in different disciplines, may have different levels of education and expertise, and may not even work in the same precinct. They share a desire to solve the case, but

that’s all.

Different detectives may come and go during the course of the process, and may work different shifts.

There are no restrictions on what may be placed on the blackboard.

It may be pictures, sentences, physical evidence, and so on.

This is a form of laissez faire concurrency. The detectives are independent processes, agents, actors, and so on. Some store facts on the blackboard. Others take facts off the board, maybe combining or processing them, and add more information to the board. Gradually the board helps them come to a conclusion.

Computer-based blackboard systems were originally used in

artificial intelligence applications where the problems to be solved were large and complex—speech recognition, knowledge-based reasoning systems, and so on.

One of the first blackboard systems was David Gelernter’s

Linda. It stored facts as typed tuples. Applications could write new tuples into Linda, and query for existing tuples using a form of pattern matching.

Later came distributed blackboard-like systems such as

JavaSpaces and T Spaces. With these systems, you can store

active Java objects—not just data—on the blackboard, and

retrieve them by partial matching of fields (via templates and wildcards) or by subtypes. For example, suppose you had a type Author, which is a subtype of Person. You could search a

blackboard containing Person objects by using an Author template with a lastName value of「Shakespeare.’’ You’d get Bill

Shakespeare the author, but not Fred Shakespeare the gardener.

These systems never really took off, we believe, in part, because the need for the kind of concurrent cooperative processing

hadn’t yet developed.

A BLACKBOARD IN ACTION

Suppose we are writing a program to accept and process

mortgage or loan applications. The laws that govern this area are odiously complex, with federal, state, and local governments all having their say. The lender must prove they have disclosed certain things, and must ask for certain information—but must not ask certain other questions, and so on, and so on.

Beyond the miasma of applicable law, we also have the

following problems to contend with:

Responses can arrive in any order. For instance, queries for a credit check or title search may take a substantial amount of time, while items such as name and address may be available immediately.

Data gathering may be done by different people, distributed across different offices, in different time zones.

Some data gathering may be done automatically by other systems.

This data may arrive asynchronously as well.

Nonetheless, certain data may still be dependent on other data. For instance, you may not be able to start the title search for a car until you get proof of ownership or insurance.

The arrival of new data may raise new questions and policies.

Suppose the credit check comes back with a less than glowing report; now you need these five extra forms and perhaps a blood sample.

You can try to handle every possible combination and

circumstance using a workflow system. Many such systems

exist, but they can be complex and programmer intensive. As regulations change, the workflow must be reorganized: people may have to change their procedures and hard-wired code may

have to be rewritten.

A blackboard, in combination with a rules engine that

encapsulates the legal requirements, is an elegant solution to the difficulties found here. Order of data arrival is irrelevant: when a fact is posted it can trigger the appropriate rules.

Feedback is easily handled as well: the output of any set of rules can post to the blackboard and cause the triggering of yet more applicable rules.

Tip 60

Use Blackboards to Coordinate Workflow

MESSAGING SYSTEMS CAN BE LIKE BLACKBOARDS

As we’re writing this second edition, many applications are

constructed using small, decoupled services, all communicating via some form of messaging system. These messaging systems

(such as Kafka and NATS) do far more than simply send data

from A to B. In particular, they offer persistence (in the form of an event log) and the ability to retrieve messages through a form of pattern matching. This means you can use them both as a blackboard system and/or as a platform on which you can run a bunch of actors.

BUT IT’S NOT THAT SIMPLE…

The actor and/or blackboard and/or microservice approach to

architecture removes a whole class of potential concurrency

problems from your applications. But that benefit comes at a cost. These approaches are harder to reason about, because a lot

of the action is indirect. You’ll find it helps to keep a central repository of message formats and/or APIs, particularly if the repository can generate the code and documentation for you.

You’ll also need good tooling to be able to trace messages and facts as they progress through the system. (A useful technique is to add a unique trace id when a particular business function is initiated and then propagate it to all the actors involved. You’ll then be able to reconstruct what happens from the log files.) Finally, these kinds of system can be more troublesome to

deploy and manage, as there are more moving parts. To some

extent this is offset by the fact that the system is more granular, and can be updated by replacing individual actors, and not the whole system.

RELATED SECTIONS INCLUDE

Topic 28, Decoupling

Topic 29, Juggling the Real World

Topic 33, Breaking Temporal Coupling

Topic 35, Actors and Processes

EXERCISES

Exercise 24 (possible answer)

Would a blackboard-style system be appropriate for the

following applications? Why, or why not?

Image processing. You’d like to have a number of parallel processes grab chunks of an image, process them, and put the completed chunk back.

Group calendaring. You’ve got people scattered across the globe, in different time zones, and speaking different languages, trying to schedule a meeting.

Network monitoring tool. The system gathers performance statistics and collects trouble reports, which agents use to look for trouble in the system.

CHALLENGES

Do you use blackboard systems in the real world—the message

board by the refrigerator, or the big whiteboard at work? What makes them effective? Are messages ever posted with a consistent format? Does it matter?

Footnotes

[46] Although UML has gradually faded, many of its individual diagrams still exist in one form or another, including the very useful activity diagram. For more information on

all of the UML diagram types, see UML Distilled: A Brief Guide to the Standard Object

Modeling Language [Fow04].

[47] The names P and V come from the initial letters of Dutch words. However there is some discussion about exactly which words. The inventor of the technique, Edsger Dĳkstra, has suggested both passering and prolaag for P, and vrijgave and possibly verhogen for V.

[48] https://github.com/ncthbrt/nact

[49] In order to run this code you’ll also need our wrapper functions, which are not shown here. You can download them from

https://media.pragprog.com/titles/tpp20/code/concurrency/actors/index.js

Copyright © 2020 Pearson Education, Inc.

Chapter 7

While You Are Coding

