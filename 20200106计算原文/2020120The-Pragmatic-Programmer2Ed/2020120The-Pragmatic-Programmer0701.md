At the very beginning of a project, you and the team need to learn the requirements. Simply being told what to do or

listening to users is not enough: read Topic 45, The

Requirements Pit and learn how to avoid the common traps and pitfalls.

Conventional wisdom and constraint management are the

topics of Topic 46, Solving Impossible Puzzles. Whether you are performing requirements, analysis, coding, or testing, difficult problems will crop up. Most of the time, they won’t be as

difficult as they first appear to be.

And when that impossible project comes up, we like to turn to our secret weapon: Topic 47, Working Together. And by

「working together」we don’t mean sharing a massive

requirements document, flinging heavily cc’d emails or

enduring endless meetings. We mean solving problems together while coding. We’ll show you who you need and how to start.

Even though the Agile Manifesto begins with「Individuals and interactions over processes and tools,」virtually all「agile」

projects begin with an ironic discussion of which process and which tools they’ll use. But no matter how well thought out it is,

and regardless of which「best practices」it includes, no method can replace thinking. You don’t need any particular process or tool, what you do need is the Topic 48, The Essence of Agility.

With these critical issues sorted out before the project gets under way, you can be better positioned to avoid「analysis

paralysis」and actually begin—and complete—your successful

project.

Topic 45

The Requirements Pit

Many books and tutorials refer to

requirements gathering as an

Perfection is achieved,

early phase of the project. The

not when there is

word「gathering」seems to imply a

nothing left to add

tribe of happy analysts, foraging

but when there is

for nuggets of wisdom that are

nothing left to take

lying on the ground all around

away...

them while the Pastoral Symphony

plays gently in the background.

Antoine de St. Exupery, Wind,

「Gathering」implies that the

Sand, and Stars, 1939

requirements are already there—

you need merely find them, place

them in your basket, and be

merrily on your way.

It doesn’t quite work that way. Requirements rarely lie on the surface. Normally, they’re buried deep beneath layers of

assumptions, misconceptions, and politics. Even worse, often they don’t really exist at all.

Tip 75

No One Knows Exactly What They Want

THE REQUIREMENTS MYTH

In the early days of software, computers were more valuable (in terms of amortized cost per hour) than the people who worked with them. We saved money by trying to get things correct the

first time. Part of that process was trying to specify exactly what we were going to get the machine to do. We’d start by getting a specification of the requirements, parlay that into a design document, then into flowcharts and pseudo code, and finally

into code. Before feeding it into a computer, though, we’d spend time desk checking it.

It cost a lot of money. And that cost meant that people only tried to automate something when they knew exactly what they

wanted. As early machines were fairly limited, the scope of

problems they solved was constrained: it was actually possible to understand the whole problem before you started.

But that is not the real world. The real world is messy,

conflicted, and unknown. In that world, exact specifications of anything are rare, if not downright impossible.

That’s where we programmers come in. Our job is to help

people understand what they want. In fact, that’s probably our most valuable attribute. And it’s worth repeating:

Programmers Help People Understand What They

Tip 76

Want

PROGRAMMING AS THERAPY

Let’s call the people who ask us to write software our clients.

The typical client comes to us with a need. The need may be

strategic, but it is just as likely to be a tactical issue: a response to a current problem. The need may be for a change to an

existing system or it may ask for something new. The need will sometimes be expressed in business terms, and sometimes in

technical ones.

The mistake new developers often make is to take this

statement of need and implement a solution for it.

In our experience, this initial statement of need is not an

absolute requirement. The client may not realize this, but it is really an invitation to explore.

Let’s take a simple example.

You work for a publisher of paper and electronic books. You’re given a new requirement:

Shipping should be free on all orders costing $50 or more.

Stop for a second and imagine yourself in that position. What’s the first thing that comes to mind?

The chances are very good that you had questions:

Does the $50 include tax?

Does the $50 include current shipping charges?

Does the $50 have to be for paper books, or can the order also include ebooks?

What kind of shipping is offered? Priority? Ground?

What about international orders?

How often will the $50 limit change in the future?

That’s what we do. When given something that seems simple,

we annoy people by looking for edge cases and asking about

them.

The chances are the client will have already thought of some of these, and just assumed that the implementation would work

that way. Asking the question just flushes that information out.

But other questions will likely be things that the client hadn’t previously considered. That’s where things get interesting, and where a good developer learns to be diplomatic.

You:

We were wondering about the $50 total. Does that

include what we’d normally charge for shipping?

Client:

Of course. It’s the total they’d pay us.

You:

That’s nice and simple for our customers to understand: I

can see the attraction. But I can see some less scrupulous

customers trying to game that system.

Client:

How so?

You:

Well, let’s say they buy a book for $25, and then select

overnight shipping, the most expensive option. That’ll

likely be about $30, making the whole order $55. We’d

then make the shipping free, and they’d get overnight

shipping on a $25 book for just $25.

(At this point the experienced developer stops. Deliver

facts, and let the client make the decisions,) Client:

Ouch. That certainly wasn’t what I intended; we’d lose

money on those orders. What are the options?

And this starts an exploration. Your role in this is to interpret what the client says and to feed back to them the implications.

This is both an intellectual process and a creative one: you’re thinking on your feet and you’re contributing to a solution that is likely to be better than one that either you or the client would have produced alone.

REQUIREMENTS ARE A PROCESS

In the previous example, the developer took the requirements and fed-back a consequence to the client. This initiated the exploration. During that exploration, you are likely to come up with more feedback as the client plays with different solutions.

This is the reality of all requirements gathering:

Tip 77

Requirements Are Learned in a Feedback Loop

Your job is to help the client understand the consequences of their stated requirements. You do that by generating feedback, and letting them use that feedback to refine their thinking.

In the previous example, the feedback was easy to express in words. Sometimes that’s not the case. And sometimes you

honestly won’t know enough about the domain to be as specific as that.

In those cases, Pragmatic Programmers rely on the「is this what

you meant?」school of feedback. We produce mockups and prototypes, and let the client play with them. Ideally the things we produce are flexible enough that we can change them during our discussions with the client, letting us respond to「that isn’t what I meant」with「so more like this?」

Sometimes these mockups can be thrown together in an hour or so. They are obviously just hacks to get an idea across.

But the reality is that all of the work we do is actually some form of mockup. Even at the end of a project we’re still interpreting what our client wants. In fact, by that point we’re likely to have more clients: the QA people, operations, marketing, and maybe even test groups of customers.

So the Pragmatic Programmer looks at all of the project as a requirements gathering exercise. That’s why we prefer short

iterations; ones that end with direct client feedback. This keeps us on track, and makes sure that if we do go in the wrong direction, the amount of time lost is minimized.

WALK IN YOUR CLIENT’S SHOES

There’s a simple technique for getting inside your clients’ heads that isn’t used often enough: become a client. Are you writing a system for the help desk? Spend a couple of days monitoring the phones with an experienced support person. Are you

automating a manual stock control system? Work in the

warehouse for a week. [70]

As well as giving you insight into how the system will really be used, you’d be amazed at how the request「May I sit in for a week while you do your job?’’ helps build trust and establishes a basis for communication with your clients. Just remember not

to get in the way!

Tip 78

Work with a User to Think Like a User

Gathering feedback is also the time to start to build a rapport with your client base, learning their expectations and hopes for the system you are building. See Topic 52, Delight Your Users, for more.

REQUIREMENTS VS. POLICY

Let’s imagine that while discussing a Human Resources system, a client says「Only an employee’s supervisors and the personnel department may view that employee’s records.」Is this

statement truly a requirement? Perhaps today, but it embeds

business policy in an absolute statement.

Business policy? Requirement? It’s a relatively subtle

distinction, but it’s one that will have profound implications for the developers. If the requirement is stated as「Only supervisors and personnel can view an employee record,」the developer may end up coding an explicit test every time the application

accesses this data. However, if the statement is「Only

authorized users may access an employee record,」the developer will probably design and implement some kind of access control system. When policy changes (and it will), only the metadata for that system will need to be updated. In fact, gathering

requirements in this way naturally leads you to a system that is well factored to support metadata.

In fact, there’s a general rule here:

Tip 79

Policy Is Metadata

Implement the general case, with the policy information as an example of the type of thing the system needs to support.

REQUIREMENTS VS. REALITY

In a January 1999 Wired magazine article,[71] producer and musician Brian Eno described an incredible piece of technology

—the ultimate mixing board. It does anything to sound that can be done. And yet, instead of letting musicians make better

music, or produce a recording faster or less expensively, it gets in the way; it disrupts the creative process.

To see why, you have to look at how recording engineers work.

They balance sounds intuitively. Over the years, they develop an innate feedback loop between their ears and their fingertips—

sliding faders, rotating knobs, and so on. However, the interface to the new mixer didn’t leverage off those abilities. Instead, it forced its users to type on a keyboard or click a mouse. The functions it provided were comprehensive, but they were

packaged in unfamiliar and exotic ways. The functions the

engineers needed were sometimes hidden behind obscure

names, or were achieved with nonintuitive combinations of

basic facilities.

This example also illustrates our belief that successful tools adapt to the hands that use them. Successful requirements

gathering takes this into account. And this is why early

feedback, with prototypes or tracer bullets, will let your clients say「yes, it does what I want, but not how I want.」

DOCUMENTING REQUIREMENTS

We believe that the best requirements documentation, perhaps

the only requirements documentation, is working code.

But that doesn’t mean that you can get away without

documenting your understanding of what the client wants. It

just means that those documents are not a deliverable: they are not something that you give to a client to sign off on. Instead, they are simply mileposts to help guide the implementation

process.

Requirements Documents Are Not for Clients

In the past, both Andy and Dave have been on projects that

produced incredibly detailed requirements. These substantial documents expanded on the client’s initial two-minute

explanation of what was wanted, producing inch-thick

masterpieces full of diagrams and tables. Things were specified to the point where there was almost no room for ambiguity in the implementation. Given sufficiently powerful tools, the

document could actually be the final program.

Creating these documents was a mistake for two reasons. First, as we’ve discussed, the client doesn’t really know what they want up front. So when we take what they say and expand it into what is almost a legal document, we are building an incredibly complex castle on quicksand.

You might say「but then we take the document to the client and they sign off on it. We’re getting feedback.」And that leads us to the second problem with these requirement specifications: the client never reads them.

The client uses programmers because, while the client is

motivated by solving a high-level and somewhat nebulous

problem, programmers are interested in all the details and

nuances. The requirements document is written for developers, and contains information and subtleties that are sometimes

incomprehensible and frequently boring to the client.

Submit a 200-page requirements document, and the client will likely heft it to decide if it weighs enough to be important, they may read the first couple of paragraphs (which is why the first two paragraphs are always titled Management Summary), and they may flick through the rest, sometimes stopping when

there’s a neat diagram.

This isn’t putting the client down. But giving them a large

technical document is like giving the average developer a copy of the Iliad in Homeric Greek and asking them to code the video game from it.

Requirements Documents Are for Planning

So we don’t believe in the monolithic, heavy-enough-to-stun-

an-ox, requirements document. We do, however, know that

requirements have to be written down, simply because

developers on a team need to know what they’ll be doing.

What form does this take? We favor something that can fit on a real (or virtual) index card. These short descriptions are often called user stories. They describe what a small portion of the application should do from the perspective of a user of that functionality.

When written this way, the requirements can be placed on a

board and moved around to show both status and priority.

You might think that a single index card can’t hold the

information needed to implement a component of the

application. You’d be right. And that’s part of the point. By keeping this statement of requirements short, you’re

encouraging developers to ask clarifying questions. You’re

enhancing the feedback process between clients and coders

before and during the creation of each piece of code.

OVERSPECIFICATION

Another big danger in producing a requirements document is

being too specific. Good requirements are abstract. Where

requirements are concerned, the simplest statement that

accurately reflects the business need is best. This doesn’t mean you can be vague—you must capture the underlying semantic

invariants as requirements, and document the specific or

current work practices as policy.

Requirements are not architecture. Requirements are not

design, nor are they the user interface. Requirements are need.

JUST ONE MORE WAFER-THIN MINT…

Many project failures are blamed on an increase in scope—also known as feature bloat, creeping featurism, or requirements

creep. This is an aspect of the boiled-frog syndrome from Topic 4, Stone Soup and Boiled Frogs. What can we do to prevent requirements from creeping up on us?

The answer (again) is feedback. If you’re working with the client in iterations with constant feedback, then the client will

experience first-hand the impact of「just one more feature.」

They’ll see another story card go up on the board, and they’ll get to help choose another card to move into the next iteration to make room. Feedback works both ways.

MAINTAIN A GLOSSARY

As soon as you start discussing requirements, users and domain experts will use certain terms that have specific meaning to them. They may differentiate between a「client」and a

「customer,」for example. It would then be inappropriate to use either word casually in the system.

Create and maintain a project glossary—one place that defines all the specific terms and vocabulary used in a project. All participants in the project, from end users to support staff, should use the glossary to ensure consistency. This implies that the glossary needs to be widely accessible—a good argument for online documentation.

Tip 80

Use a Project Glossary

It’s hard to succeed on a project if users and developers call the same thing by different names or, even worse, refer to different things by the same name.

RELATED SECTIONS INCLUDE

Topic 5, Good-Enough Software

Topic 7, Communicate!

Topic 11, Reversibility

Topic 13, Prototypes and Post-it Notes

Topic 23, Design by Contract

Topic 43, Stay Safe Out There

Topic 44, Naming Things

Topic 46, Solving Impossible Puzzles

Topic 52, Delight Your Users

EXERCISES

Exercise 33 (possible answer)

Which of the following are probably genuine requirements?

Restate those that are not to make them more useful (if

possible).

1. The response time must be less than ~500ms.

2. Modal windows will have a gray background.

3. The application will be organized as a number of front-end processes and a back-end server.

4. If a user enters non-numeric characters in a numeric field, the system will flash the field background and not accept them.

5. The code and data for this embedded application must fit within 32Mb.

CHALLENGES

Can you use the software you are writing? Is it possible to have a good feel for requirements without being able to use the software yourself?

Pick a non-computer-related problem you currently need to solve.

Generate requirements for a noncomputer solution.

Topic 46

Solving Impossible Puzzles

Every now and again, you will find

yourself embroiled in the middle of

Gordius, the King of

a project when a really tough

Phrygia, once tied a

puzzle comes up: some piece of

knot that no one could

engineering that you just can’t get

untie. It was said that

a handle on, or perhaps some bit

whoever solved the

of code that is turning out to be

riddle of the Gordian

much harder to write than you

Knot would rule all of

thought. Maybe it looks

Asia. So along comes

impossible. But is it really as hard

as it seems?

Alexander the Great,

who chops the knot to

Consider real-world puzzles—

bits with his sword.

those devious little bits of wood,

Just a little different

wrought iron, or plastic that seem

interpretation of the

to turn up as Christmas presents

requirements, that’s

or at garage sales. All you have to

all…. And he did end

do is remove the ring, or fit the T-

up ruling most of Asia.

shaped pieces in the box, or

whatever.

So you pull on the ring, or try to

put the Ts in the box, and quickly

discover that the obvious solutions just don’t work. The puzzle can’t be solved that way. But even though it’s obvious, that doesn’t stop people from trying the same thing—over and over—

thinking there must be a way.

Of course, there isn’t. The solution lies elsewhere. The secret to solving the puzzle is to identify the real (not imagined)

constraints, and find a solution therein. Some constraints are absolute; others are merely preconceived notions. Absolute constraints must be honored, however distasteful or stupid they may appear to be.

On the other hand, as Alexander proved, some apparent

constraints may not be real constraints at all. Many software problems can be just as sneaky.

DEGREES OF FREEDOM

The popular buzz-phrase「thinking outside the box」encourages us to recognize constraints that might not be applicable and to ignore them. But this phrase isn’t entirely accurate. If the「box」

is the boundary of constraints and conditions, then the trick is to find the box, which may be considerably larger than you think.

The key to solving puzzles is both to recognize the constraints placed on you and to recognize the degrees of freedom you do have, for in those you’ll find your solution. This is why some puzzles are so effective; you may dismiss potential solutions too readily.

For example, can you connect all of the dots in the following puzzle and return to the starting point with just three straight lines—without lifting your pen from the paper or retracing your steps ( Math Puzzles & Games [Hol92])?

You must challenge any preconceived notions and evaluate

whether or not they are real, hard-and-fast constraints.

It’s not whether you think inside the box or outside the box. The

problem lies in finding the box—identifying the real constraints.

Tip 81

Don’t Think Outside the Box— Find the Box

When faced with an intractable problem, enumerate all the

possible avenues you have before you. Don’t dismiss anything,

no matter how unusable or stupid it sounds. Now go through

the list and explain why a certain path cannot be taken. Are you

sure? Can you prove it?

Consider the Trojan horse—a novel solution to an intractable

problem. How do you get troops into a walled city without being

discovered? You can bet that「through the front door」was

initially dismissed as suicide.

Categorize and prioritize your constraints. When woodworkers

begin a project, they cut the longest pieces first, then cut the

smaller pieces out of the remaining wood. In the same manner,

we want to identify the most restrictive constraints first, and fit

the remaining constraints within them.

By the way, a solution to the Four Posts puzzle is shown at the

end of the book.

GET OUT OF YOUR OWN WAY!

Sometimes you will find yourself working on a problem that

seems much harder than you thought it should be. Maybe it

feels like you’re going down the wrong path—that there must be an easier way than this! Perhaps you are running late on the schedule now, or even despair of ever getting the system to work because this particular problem is「impossible.」

This is an ideal time to do something else for a while. Work on something different. Go walk the dog. Sleep on it.

Your conscious brain is aware of the problem, but your

conscious brain is really pretty dumb (no offense). So it’s time to give your real brain, that amazing associative neural net that lurks below your consciousness, some space. You’ll be amazed how often the answer will just pop into your head when you

deliberately distract yourself.

If that sounds too mystical for you, it isn’t. Psychology Today[72]

reports:

To put it plainly—people who were distracted did better on a complex problem-solving task than people who put in conscious effort.

If you’re still not willing to drop the problem for a while, the next best thing is probably finding someone to explain it to.

Often, the distraction of simply talking about it will lead you to enlightenment.

Have them ask you questions such as:

Why are you solving this problem?

What’s the benefit of solving it?

Are the problems you’re having related to edge cases? Can you eliminate them?

Is there a simpler, related problem you can solve?

This is another example of Rubber Ducking in practice.

FORTUNE FAVORS THE PREPARED MIND

Louis Pasteur is reported to have said:

Dans les champs de l’observation le hasard ne favorise que les esprits préparés.

(When it comes to observation, fortune favors the prepared mind.)

That is true for problem solving, too. In order to have those eureka! moments, your nonconscious brain needs to have plenty of raw material; prior experiences that can contribute to an answer.

A great way to feed your brain is to give it feedback on what works and what doesn’t work as you do your daily job. And we describe a great way to do that using an Engineering Daybook (Topic 22, Engineering Daybooks).

And always remember the advice on the cover of The

Hitchhiker’s Guide to the Galaxy: DON’T PANIC.

RELATED SECTIONS INCLUDE

Topic 5, Good-Enough Software

Topic 37, Listen to Your Lizard Brain

Topic 45, The Requirements Pit

Andy wrote an entire book about this kind of thing: Pragmatic

Thinking and Learning: Refactor Your Wetware [Hun08].

CHALLENGES

Take a hard look at whatever difficult problem you are embroiled in today. Can you cut the Gordian knot? Do you have to do it this way?

Do you have to do it at all?

Were you handed a set of constraints when you signed on to your current project? Are they all still applicable, and is the

interpretation of them still valid?

Topic 47

Working Together

It was one of those「impossible」

projects, the kind you hear about

I’ve never met a

that sounds both exhilarating and

human being who

terrifying at the same time. An

would want to read

ancient system was approaching

17,000 pages of

end-of-life, the hardware was

documentation, and if

physically going away, and a

there was, I’d kill him

brand-new system had to be

to get him out of the

crafted that would match the

gene pool.

(often undocumented) behavior

exactly. Many hundreds of

millions of dollars of other

Joseph Costello, President of

Cadence

people’s money would pass

through this system, and the

deadline from inception to

deployment was on the order of months.

And that is where Andy and Dave first met. An impossible

project with a ridiculous deadline. There was only one thing that made the project a roaring success. The expert who had

managed this system for years was sitting right there in her office, just across the hall from our broom closet–sized

development room. Continuously available for questions,

clarifications, decisions, and demos.

Throughout this book we recommend working closely with

users; they are part of your team. On that first project together,

we practiced what now might be called pair programming or mob programming: one person typing code while one or more other team members comment, ponder, and solve problems

together. It’s a powerful way of working together that

transcends endless meetings, memos, and overstuffed legalistic documentation prized for weight over usefulness.

And that’s what we really mean by「working with」: not just

asking questions, having discussions, and taking notes, but

asking questions and having discussions while you’re actually coding.

Conway's Law

In 1967, Melvin Conway introduced an idea in How do Committees Invent? [Con68]

which would become known as Conway’s Law:

Organizations which design systems are constrained to produce designs which are copies of the communication structures of these organizations.

That is, the social structures and communication pathways of the team and the organization will be mirrored in the application, website, or product being developed.

Various studies have shown strong support for this idea. We’ve witnessed it first-hand countless times—for example, in teams where no one talks to each other at all, resulting in siloed, "stove-pipe" systems. Or teams that were split into two, resulting in a client/server or frontend/backend division.

Studies also offer support for the reverse principle: you can deliberately structure your team the way you want your code to look. For example, geographically distributed teams are shown to tend toward more modular, distributed software.

But most importantly, development teams that include users will produce software that clearly reflects that involvement, and teams that don’t bother will reflect that, too.

PAIR PROGRAMMING

Pair programming is one of the practices of eXtreme

Programming that has become popular outside of XP itself. In pair programming, one developer operates the keyboard, and

the other does not. Both work on the problem together, and can switch typing duties as needed.

There are many benefits to pair programming. Different people bring different backgrounds and experience, different problem-solving techniques and approaches, and differing levels of focus and attention to any given problem. The developer acting as

typist must focus on the low-level details of syntax and coding style, while the other developer is free to consider higher-level issues and scope. While that might sound like a small

distinction, remember that we humans have only so much brain bandwidth. Fiddling around with typing esoteric words and

symbols that the compiler will grudgingly accept takes a fair bit of our own processing power. Having a second developer’s full brain available during the task brings a lot more mental power to bear.

The inherent peer-pressure of a second person helps against

moments of weakness and bad habits of naming variables foo

and such. You’re less inclined to take a potentially embarrassing shortcut when someone is actively watching, which also results in higher-quality software.

MOB PROGRAMMING

And if two heads are better than one, what about having a dozen diverse people all working on the same problem at the same

time, with one typist?

Mob programming, despite the name, does not involve torches or pitchforks. It’s an extension of pair programming that

involves more than just two developers. Proponents report great results using mobs to solve hard problems. Mobs can easily

include people not usually considered part of the development

team, including users, project sponsors, and testers. In fact, in our first「impossible」project together, it was a common sight for one of us to be typing while the other discussed the issue with our business expert. It was a small mob of three.

You might think of mob programming as tight collaboration with live coding.

WHAT SHOULD I DO?

If you’re currently only programming solo, maybe try pair

programming. Give it a minimum of two weeks, only a few

hours at a time, as it will feel strange at first. To brainstorm new ideas or diagnose thorny issues, perhaps try a mob

programming session.

If you are already pairing or mobbing, who’s included? Is it just developers, or do you allow members of your extended team to participate: users, testers, sponsors…?

And as with all collaboration, you need to manage the human

aspects of it as well as the technical. Here are just a few tips to get started:

Build the code, not your ego. It’s not about who’s brightest; we all have our moments, good and bad.

Start small. Mob with only 4-5 people, or start with just a few pairs, in short sessions.

Criticize the code, not the person.「Let’s look at this block」sounds much better than「you’re wrong.」

Listen and try to understand others’ viewpoints. Different isn’t wrong.

Conduct frequent retrospectives to try and improve for next time.

Coding in the same office or remote, alone, in pairs, or in mobs, are all effective ways of working together to solve problems. If you and your team have only ever done it one way, you might

want to experiment with a different style. But don’t just jump in with a naive approach: there are rules, suggestions, and

guidelines for each of these development styles. For instance, with mob programming you swap out the typist every 5-10

minutes.

Do some reading and research, from both textbook and

experience reports, and get a feel for the advantages and pitfalls you may encounter. You might want to start by coding a simple exercise, and not just jump straight into your toughest

production code.

But however you go about it, let us suggest one final piece of advice:

Tip 82

Don’t Go into the Code Alone

Topic 48

The Essence of Agility

Agile is an adjective: it’s how you

do something. You can be an agile

You keep using that

developer. You can be on a team

word, I do not think it

that adopts agile practices, a team

means

that responds to change and

what you think it

setbacks with agility. Agility is

means.

your style, not you.

Inigo Montoya, The Princess

Bride

Tip 83

Agile Is Not a Noun; Agile Is How You Do Things

As we write this, almost 20 years after the inception of the Manifesto for Agile Software Development,[73 ]we see many, many developers successfully applying its values. We see many fantastic teams who find ways to take these values and use them to guide what they do, and how they change what they do.

But we also see another side of agility. We see teams and

companies eager for off-the-shelf solutions: Agile-in-a-Box. And we see many consultants and companies all too happy to sell

them what they want. We see companies adopting more layers

of management, more formal reporting, more specialized

developers, and more fancy job titles which just mean「someone with a clipboard and a stopwatch. 」[74]

We feel that many people have lost sight of the true meaning of agility, and we’d like to see folks return to the basics.

Remember the values from the manifesto:

We are uncovering better ways of developing software by doing it and helping others do it. Through this work we have come to value:

Individuals and interactions over processes and tools Working software over comprehensive documentation

Customer collaboration over contract negotiation

Responding to change over following a plan

That is, while there is value in the items on the right, we value the items on the left more.

Anyone selling you something that increases the importance on things on the right over things on the left clearly doesn’t value the same things that we and the other manifesto writers did.

And anyone selling you a solution-in-a-box hasn’t read the

introductory statement. The values are motivated and informed by the continuous act of uncovering better ways to produce

software. This is not a static document. It’s suggestions for a generative process.

THERE CAN NEVER BE AN AGILE PROCESS

In fact, whenever someone says「do this, and you’ll be agile,」

they are wrong. By definition.

Because agility, both in the physical world and in software development, is all about responding to change, responding to the unknowns you encounter after you set out. A running

gazelle doesn’t go in a straight line. A gymnast makes hundreds of corrections a second as they respond to changes in their

environment and minor errors in their foot placement.

So it is with teams and individual developers. There is no single plan you can follow when you develop software. Three of the

four values tell you that. They’re all about gathering and

responding to feedback.

The values don’t tell you what to do. They tell you what to look for when you decide for yourself what to do.

These decisions are always contextual: they depend on who you are, the nature of your team, your application, your tooling, your company, your customer, the outside world; an incredibly large number of factors, some major and some trivial. No fixed, static plan can survive this uncertainty.

SO WHAT DO WE DO?

No one can tell you what to do. But we think we can tell you something about the spirit with which you do it. It all boils down to how you deal with uncertainty. The manifesto suggests that you do this by gathering and acting on feedback. So here’s our recipe for working in an agile way:

1. Work out where you are.

2. Make the smallest meaningful step towards where you want to be.

3. Evaluate where you end up, and fix anything you broke.

Repeat these steps until you’re done. And use them recursively, at every level of everything you do.

Sometimes even the most trivial-seeming decision becomes

important when you gather feedback.

「Now my code needs to get the account owner.

let user = accountOwner(accountID);

Hmmm… user is a useless name. I’ll make it owner.

let owner = accountOwner(accountID);

But now that feels a little redundant. What am I actually trying to do here? The story says that I’m sending this person an email, so I need to find their email address. Maybe I don’t need the whole account owner at all.

let email = emailOfAccountOwner(accountID);

By applying the feedback loop at a really low level (the naming of a variable) we’ve actually improved the design of the overall system, reducing the coupling between this code and the code that deals with accounts.

The feedback loop also applies at the highest level of a project.

Some of our most successful work has happened when we

started working on a client’s requirements, took a single step, and realized that what we were about to do wasn’t necessary, that the best solution didn’t even involve software.

This loop applies outside the scope of a single project. Teams should apply it to review their process and how well it worked. A team that doesn’t continuously experiment with their process is not an agile team.

AND THIS DRIVES DESIGN

In Topic 8, The Essence of Good Design we assert that the measure of design is how easy the result of that design is to change: a good design produces something that’s easier to

change than a bad design.

And this discussion about agility explains why that’s the case.

You make a change, and discover you don’t like it. Step 3 in our list says we have to be able to fix what we break. To make our feedback loop efficient, this fix has to be as painless as possible.

If it isn’t, we’ll be tempted to shrug it off and leave it unfixed.

We talk about this effect in Topic 3, Software Entropy. To make this whole agile thing work, we need to practice good design, because good design makes things easy to change. And if it’s easy to change, we can adjust, at every level, without any

hesitation.

That is agility.

RELATED SECTIONS INCLUDE

Topic 27, Don’t Outrun Your Headlights

Topic 40, Refactoring

Topic 50, Coconuts Don’t Cut It

CHALLENGES

The simple feedback loop isn’t just for software. Think of other decisions you’ve made recently. Could any of them have been

improved by thinking about how you might be able to undo

them if things didn’t take you in the direction you were going?

Can you think of ways you can improve what you do by

gathering and acting on feedback?

Footnotes

[70] Does a week sound like a long time? It really isn’t, particularly when you’re looking at processes in which management and workers occupy different worlds. Management will give you one view of how things operate, but when you get down on the floor, you’ll find a very different reality—one that will take time to assimilate.

[71] https://www.wired.com/1999/01/eno/

[72] https://www.psychologytoday.com/us/blog/your-brain-work/201209/stop-trying-

solve-problems

[73] https://agilemanifesto.org

[74] For more on just how bad that approach can be, see The Tyranny of Metrics [Mul18].

Copyright © 2020 Pearson Education, Inc.

Chapter 9

Pragmatic Projects

As your project gets under way, we need to move away from

issues of individual philosophy and coding to talk about larger, project-sized issues. We aren’t going to go into specifics of project management, but we will talk about a handful of critical areas that can make or break any project.

As soon as you have more than one person working on a project, you need to establish some ground rules and delegate parts of the project accordingly. In Topic 49, Pragmatic Teams, we’ll show how to do this while honoring the Pragmatic philosophy.

The purpose of a software development method is to help

people work together. Are you and your team doing what works well for you, or are you only investing in the trivial surface artifacts, and not getting the real benefits you deserve? We’ll see why Topic 50, Coconuts Don’t Cut It and offer the true secret to success.

And of course none of that matters if you can’t deliver software consistently and reliably. That’s the basis of the magic trio of version control, testing, and automation: the Topic 51,

Pragmatic Starter Kit.

Ultimately, though, success is in the eye of the beholder—the sponsor of the project. The perception of success is what counts, and in Topic 52, Delight Your Users we’ll show you how to delight every project’s sponsor.

The last tip in the book is a direct consequence of all the rest. In Topic 53, Pride and Prejudice, we ask you to sign your work, and to take pride in what you do.

Topic 49

Pragmatic Teams

Even in 1985, the joke about

herding cats was getting old. By

At Group L, Stoffel

the time of the first edition at the

oversees six first-rate

turn of the century, it was

programmers, a

positively ancient. Yet it persists,

managerial challenge

because it has a ring of truth to it.

roughly comparable to

Programmers are a bit like cats:

herding cats.

intelligent, strong willed,

opinionated, independent, and

The Washington Post

often worshiped by the net.

Magazine, June 9, 1985

So far in this book we’ve looked at

pragmatic techniques that help an

individual be a better programmer. Can these methods work for teams as well, even for teams of strong-willed, independent

people? The answer is a resounding「yes!’’ There are advantages to being a pragmatic individual, but these advantages are

multiplied manyfold if the individual is working on a pragmatic team.

A team, in our view, is a small, mostly stable entity of its own.

Fifty people aren’t a team, they’re a horde. [75] Teams where members are constantly being pulled onto other assignments

and no one knows each other aren’t a team either, they are

merely strangers temporarily sharing a bus stop in the rain.

A pragmatic team is small, under 10-12 or so members.

Members come and go rarely. Everyone knows everyone well, trusts each other, and depends on each other.

Tip 84

Maintain Small, Stable Teams

In this section we’ll look briefly at how pragmatic techniques can be applied to teams as a whole. These notes are only a start.

Once you’ve got a group of pragmatic developers working in an enabling environment, they’ll quickly develop and refine their own team dynamics that work for them.

Let’s recast some of the previous sections in terms of teams.

NO BROKEN WINDOWS

Quality is a team issue. The most diligent developer placed on a team that just doesn’t care will find it difficult to maintain the enthusiasm needed to fix niggling problems. The problem is

further exacerbated if the team actively discourages the

developer from spending time on these fixes.

Teams as a whole should not tolerate broken windows—those

small imperfections that no one fixes. The team must take responsibility for the quality of the product, supporting

developers who understand the no broken windows philosophy we describe in Topic 3, Software Entropy, and encouraging those who haven’t yet discovered it.

Some team methodologies have a「quality officer」—someone to

whom the team delegates the responsibility for the quality of the deliverable. This is clearly ridiculous: quality can come only from the individual contributions of all team members. Quality is built in, not bolted on.

BOILED FROGS

Remember the apocryphal frog in the pan of water, back in

Topic 4, Stone Soup and Boiled Frogs? It doesn’t notice the gradual change in its environment, and ends up cooked. The

same can happen to individuals who aren’t vigilant. It can be difficult to keep an eye on your overall environment in the heat of project development.

It’s even easier for teams as a whole to get boiled. People

assume that someone else is handling an issue, or that the team leader must have OK’d a change that your user is requesting.

Even the best-intentioned teams can be oblivious to significant changes in their projects.

Fight this. Encourage everyone to actively monitor the

environment for changes. Stay awake and aware for increased

scope, decreased time scales, additional features, new

environments—anything that wasn’t in the original

understanding. Keep metrics on new requirements.[76] The team needn’t reject changes out of hand—you simply need to be

aware that they’re happening. Otherwise, it’ll be you in the hot water.

SCHEDULE YOUR KNOWLEDGE PORTFOLIO

In Topic 6, Your Knowledge Portfolio we looked at ways you should invest in your personal Knowledge Portfolio on your own time. Teams that want to succeed need to consider their

knowledge and skill investments as well.

If your team is serious about improvement and innovation, you need to schedule it. Trying to get things done「whenever there’s a free moment」means they will never happen. Whatever sort of

backlog or task list or flow you’re working with, don’t reserve it for only feature development. The team works on more than

just new features. Some possible examples include:

Old Systems Maintenance

While we love working on the shiny new system, there’s

likely maintenance work that needs to be done on the old

system. We’ve met teams who try and shove this work in

the corner. If the team is charged with doing these tasks,

then do them—for real.

Process Reflection and Refinement

Continuous improvement can only happen when you take

the time to look around, figure out what’s working and

not, and then make changes (see Topic 48, The Essence

of Agility). Too many teams are so busy bailing out water that they don’t have time to fix the leak. Schedule it. Fix

it.

New tech experiments

Don’t adopt new tech, frameworks, or libraries just

because「everyone is doing it,」or based on something

you saw at a conference or read online. Deliberately vet

candidate technologies with prototypes. Put tasks on the

schedule to try the new things and analyze results.

Learning and skill improvements

Personal learning and improvements are a great start,

but many skills are more effective when spread team-

wide. Plan to do it, whether it’s the informal brown-bag

lunch or more formal training sessions.

Tip 85

Schedule It to Make It Happen

COMMUNICATE TEAM PRESENCE

It’s obvious that developers in a team must talk to each other.

We gave some suggestions to facilitate this in Topic 7,

Communicate! . However, it’s easy to forget that the team itself has a presence within the organization. The team as an entity needs to communicate clearly with the rest of the world.

To outsiders, the worst project teams are those that appear

sullen and reticent. They hold meetings with no structure,

where no one wants to talk. Their emails and project documents are a mess: no two look the same, and each uses different

terminology.

Great project teams have a distinct personality. People look forward to meetings with them, because they know that they’ll see a well-prepared performance that makes everyone feel good.

The documentation they produce is crisp, accurate, and

consistent. The team speaks with one voice.[77 ]They may even have a sense of humor.

There is a simple marketing trick that helps teams communicate as one: generate a brand. When you start a project, come up

with a name for it, ideally something off-the-wall. (In the past, we’ve named projects after things such as killer parrots that prey on sheep, optical illusions, gerbils, cartoon characters, and mythical cities.) Spend 30 minutes coming up with a zany logo, and use it. Use your team’s name liberally when talking with people. It sounds silly, but it gives your team an identity to build on, and the world something memorable to associate with your work.

DON’T REPEAT YOURSELVES

In Topic 9, DRY—The Evils of Duplication, we talked about the difficulties of eliminating duplicated work between members of a team. This duplication leads to wasted effort, and can result in a maintenance nightmare.「Stovepipe」or「siloed」systems are common in these teams, with little sharing and a lot of

duplicated functionality.

Good communication is key to avoiding these problems. And by

「good」we mean instant and frictionless.

You should be able to ask a question of team members and get a more-or-less instant reply. If the team is co-located, this might be as simple as poking your head over the cube wall or down the hall. For remote teams, you may have to rely on a messaging

app or other electronic means.

If you have to wait a week for the team meeting to ask your

question or share your status, that’s an awful lot of friction.[78]

Frictionless means it’s easy and low-ceremony to ask questions, share your progress, your problems, your insights and

learnings, and to stay aware of what your teammates are doing.

Maintain awareness to stay DRY.

TEAM TRACER BULLETS

A project team has to accomplish many different tasks in

different areas of the project, touching a lot of different

technologies. Understanding requirements, designing

architecture, coding for frontend and server, testing, all have to happen. But it’s a common misconception that these activities and tasks can happen separately, in isolation. They can’t.

Some methodologies advocate all sort of different roles and titles within the team, or create separate specialized teams entirely. But the problem with that approach is that it

introduces gates and handoffs. Now instead of a smooth flow from the team to deployment, you have artificial gates where the work stops. Handoffs that have to wait to be accepted.

Approvals. Paperwork. The Lean folks call this waste, and strive to actively eliminate it.

All of these different roles and activities are actually different views of the same problem, and artificially separating them can cause a boatload of trouble. For example, programmers who are two or three levels removed from the actual users of their code are unlikely to be aware of the context in which their work is used. They will not be able to make informed decisions.

With Topic 12, Tracer Bullets, we recommend developing individual features, however small and limited initially, that go end-to-end through the entire system. That means that you

need all the skills to do that within the team: frontend, UI/UX, server, DBA, QA, etc., all comfortable and accustomed to

working with each other. With a tracer bullet approach, you can implement very small bits of functionality very quickly, and get immediate feedback on how well your team communicates and

delivers. That creates an environment where you can make

changes and tune your team and process quickly and easily.

Tip 86

Organize Fully Functional Teams

Build teams so you can build code end-to-end, incrementally

and iteratively.

AUTOMATION

A great way to ensure both consistency and accuracy is to

automate everything the team does. Why struggle with code

formatting standards when your editor or IDE can do it for you automatically? Why do manual testing when the continuous

build can run tests automatically? Why deploy by hand when

automation can do it the same way every time, repeatably and reliably?

Automation is an essential component of every project team.

Make sure the team has skills at tool building to construct and deploy the tools that automate the project development and

production deployment.

KNOW WHEN TO STOP ADDING PAINT

Remember that teams are made up of individuals. Give each

member the ability to shine in their own way. Give them just enough structure to support them and to ensure that the project

delivers value. Then, like the painter in Topic 5, Good-Enough

Software, resist the temptation to add more paint.

RELATED SECTIONS INCLUDE

Topic 2, The Cat Ate My Source Code

Topic 7, Communicate!

Topic 12, Tracer Bullets

Topic 19, Version Control

Topic 50, Coconuts Don’t Cut It

Topic 51, Pragmatic Starter Kit

CHALLENGES

Look around for successful teams outside the area of software development. What makes them successful? Do they use any of the processes discussed in this section?

Next time you start a project, try convincing people to brand it. Give your organization time to become used to the idea, and then do a quick audit to see what difference it made, both within the team and externally.

You were probably once given problems such as「If it takes 4

workers 6 hours to dig a ditch, how long would it take 8 workers?」

In real life, however, what factors affect the answer if the workers were writing code instead? In how many scenarios is the time actually reduced?

Read The Mythical Man Month [Bro96] by Frederick Brooks. For extra credit, buy two copies so you can read it twice as fast.

Topic 50

Coconuts Don’t Cut It

The native islanders had never seen an airplane before, or met people such as these strangers. In return for use of their land, the strangers provided mechanical birds that flew in and out all day long on a「runway,」bringing incredible material wealth to their island home. The strangers mentioned something about

war and fighting. One day it was over and they all left, taking their strange riches with them.

The islanders were desperate to restore their good fortunes, and re-built a facsimile of the airport, control tower, and equipment using local materials: vines, coconut shells, palm fronds, and such. But for some reason, even though they had everything in place, the planes didn’t come. They had imitated the form, but not the content. Anthropologists call this a cargo cult.

All too often, we are the islanders.

It’s easy and tempting to fall into the cargo cult trap: by

investing in and building up the easily-visible artifacts, you hope to attract the underlying, working magic. But as with the original cargo cults of Melanesia,[79] a fake airport made out of coconut shells is no substitute for the real thing.

For example, we have personally seen teams that claim to be

using Scrum. But, upon closer examination, it turned out they were doing a daily stand up meeting once a week, with four-week iterations that often turned into six- or eight-week

iterations. They felt that this was okay because they were using a popular「agile」scheduling tool. They were only investing in the superficial artifacts—and even then, often in name only, as if

「stand up」or「iteration」were some sort of incantation for the superstitious. Unsurprisingly, they, too, failed to attract the real magic.

CONTEXT MATTERS

Have you or your team fallen in this trap? Ask yourself, why are you even using that particular development method? Or that

framework? Or that testing technique? Is it actually well-suited for the job at hand? Does it work well for you? Or was it adopted just because it was being used by the latest internet-fueled success story?

There’s a current trend to adopt the policies and processes of successful companies such as Spotify, Netflix, Stripe, GitLab, and others. Each have their own unique take on software

development and management. But consider the context: are

you in the same market, with the same constraints and

opportunities, similar expertise and organization size, similar management, and similar culture? Similar user base and

requirements?

Don’t fall for it. Particular artifacts, superficial structures, policies, processes, and methods are not enough.

Tip 87

Do What Works, Not What’s Fashionable

How do you know「what works」? You rely on that most

fundamental of Pragmatic techniques:

Try it.

Pilot the idea with a small team or set of teams. Keep the good bits that seem to work well, and discard anything else as waste or overhead. No one will downgrade your organization because it operates differently from Spotify or Netflix, because even they didn’t follow their current processes while they were growing.

And years from now, as those companies mature and pivot and

continue to thrive, they’ll be doing something different yet again.

That’s the actual secret to their success.

ONE SIZE FITS NO ONE WELL

The purpose of a software development methodology is to help

people work together. As we discuss in Topic 48, The Essence of

Agility, there is no single plan you can follow when you develop

software, especially not a plan that someone else came up with at another company.

Many certification programs are actually even worse than that: they are predicated on the student being able to memorize and follow the rules. But that’s not what you want. You need the ability to see beyond the existing rules and exploit possibilities for advantage. That’s a very different mindset from「but

Scrum/Lean/Kanban/XP/agile does it this way…」and so on.

Instead, you want to take the best pieces from any particular methodology and adapt them for use. No one size fits all, and current methods are far from complete, so you’ll need to look at more than just one popular method.

For example, Scrum defines some project management

practices, but Scrum by itself doesn’t provide enough guidance at the technical level for teams or at the portfolio/governance level for leadership. So where do you start?

Be Like Them!

We frequently hear software development leaders tell their staff,「We should operate like Netflix」(or one of these other leading companies). Of course you could do that.

First, get yourself a few hundred thousand servers and tens of millions of users...

THE REAL GOAL

The goal of course isn’t to「do Scrum,」「do agile,」「do Lean,」or what-have-you. The goal is to be in a position to deliver working software that gives the users some new capability at a moment’s notice. Not weeks, months, or years from now, but now. For many teams and organizations, continuous delivery feels like a lofty, unattainable goal, especially if you’re saddled with a process that restricts delivery to months, or even weeks. But as with any goal, the key is to keep aiming in the right direction.

images/delivery_times.png

If you’re delivering in years, try and shorten the cycle to

months. From months, cut it down to weeks. From a four-week

sprint, try two. From a two week sprint, try one. Then daily.

Then, finally, on demand. Note that being able to deliver on demand does not mean you are forced to deliver every minute of every day. You deliver when the users need it, when it makes business sense to do so.

Tip 88

Deliver When Users Need It

In order to move to this style of continuous development, you need a rock-solid infrastructure, which we discuss in the next topic, Topic 51, Pragmatic Starter Kit. You do development in the main trunk of your version control system, not in branches, and use techniques such as feature switches to roll out test features to users selectively.

Once your infrastructure is in order, you need to decide how to

organize the work. Beginners might want to start with Scrum for project management, plus the technical practices from eXtreme Programming (XP). More disciplined and experienced teams

might look to Kanban and Lean techniques, both for the team

and perhaps for larger governance issues.

But don’t take our word for it, investigate and try these

approaches for yourself. Be careful, though, in overdoing it.

Overly investing in any particular methodology can leave you blind to alternatives. You get used to it. Soon it becomes hard to see any other way. You’ve become calcified, and now you can’t adapt quickly anymore.

Might as well be using coconuts.

RELATED SECTIONS INCLUDE

Topic 12, Tracer Bullets

Topic 27, Don’t Outrun Your Headlights

Topic 48, The Essence of Agility

Topic 49, Pragmatic Teams

Topic 51, Pragmatic Starter Kit

Topic 51

Pragmatic Starter Kit

Back when cars were a novelty, the

instructions for starting a Model-T

Civilization advances

Ford were more than two pages

by extending the

long. With modern cars, you just

number of important

push a button—the starting

operations we can

procedure is automatic and

perform without

foolproof. A person following a list

thinking.

of instructions might flood the

engine, but the automatic starter

Alfred North Whitehead

won’t.

Although software development is

still an industry at the Model-T stage, we can’t afford to go through two pages of instructions again and again for some

common operation. Whether it is the build and release

procedure, testing, project paperwork, or any other recurring task on the project, it has to be automatic and repeatable on any capable machine.

In addition, we want to ensure consistency and repeatability on the project. Manual procedures leave consistency up to chance; repeatability isn’t guaranteed, especially if aspects of the procedure are open to interpretation by different people.

After we wrote the first edition of The Pragmatic Programmer, we wanted to create more books to help teams develop software.

We figured we should start at the beginning: what are the most

basic, most important elements that every team needs regardless of methodology, language, or technology stack. And so the idea of the Pragmatic Starter Kit was born, covering these three critical and interrelated topics:

Version Control

Regression Testing

Full Automation

These are the three legs that support every project. Here’s how.

DRIVE WITH VERSION CONTROL

As we said in Topic 19, Version Control, you want to keep everything needed to build your project under version control.

That idea becomes even more important in the context of the

project itself.

First, it allows build machines to be ephemeral. Instead of one hallowed, creaky machine in the corner of the office that

everyone is afraid to touch,[80 ]build machines and/or clusters are created on demand as spot instances in the cloud.

Deployment configuration is under version control as well, so releasing to production can be handled automatically.

And that’s the important part: at the project level, version control drives the build and release process.

Use Version Control to Drive Builds, Tests, and

Tip 89

Releases

That is, build, test, and deployment are triggered via commits or

pushes to version control, and built in a container in the cloud.

Release to staging or production is specified by using a tag in your version control system. Releases then become a much

more low-ceremony part of every day life—true continuous

delivery, not tied to any one build machine or developer’s

machine.

RUTHLESS AND CONTINUOUS TESTING

Many developers test gently, subconsciously knowing where the code will break and avoiding the weak spots. Pragmatic

Programmers are different. We are driven to find our bugs now, so we don’t have to endure the shame of others finding our bugs later.

Finding bugs is somewhat like fishing with a net. We use fine, small nets (unit tests) to catch the minnows, and big, coarse nets (integration tests) to catch the killer sharks. Sometimes the fish manage to escape, so we patch any holes that we find, in hopes of catching more and more slippery defects that are

swimming about in our project pool.

Tip 90

Test Early, Test Often, Test Automatically

We want to start testing as soon as we have code. Those tiny minnows have a nasty habit of becoming giant, man-eating

sharks pretty fast, and catching a shark is quite a bit harder. So we write unit tests. A lot of unit tests.

In fact, a good project may well have more test code than production code. The time it takes to produce this test code is worth the effort. It ends up being much cheaper in the long run, and you actually stand a chance of producing a product with

close to zero defects.

Additionally, knowing that you’ve passed the test gives you a high degree of confidence that a piece of code is「done.’’

Tip 91

Coding Ain’t Done ’Til All the Tests Run

The automatic build runs all available tests. It’s important to aim to「test for real,」in other words, the test environment should match the production environment closely. Any gaps are where bugs breed.

The build may cover several major types of software testing: unit testing; integration testing; validation and verification; and performance testing.

This list is by no means complete, and some specialized projects will require various other types of testing as well. But it gives us a good starting point.

Unit Testing

A unit test is code that exercises a module. We covered this in Topic 41, Test to Code. Unit testing is the foundation of all the other forms of testing that we’ll discuss in this section. If the parts don’t work by themselves, they probably won’t work well together. All of the modules you are using must pass their own unit tests before you can proceed.

Once all of the pertinent modules have passed their individual tests, you’re ready for the next stage. You need to test how all the modules use and interact with each other throughout the

system.

Integration Testing

Integration testing shows that the major subsystems that make up the project work and play well with each other. With good contracts in place and well tested, any integration issues can be detected easily. Otherwise, integration becomes a fertile

breeding ground for bugs. In fact, it is often the single largest source of bugs in the system.

Integration testing is really just an extension of the unit testing we’ve described—you’re just testing how entire subsystems

honor their contracts.

Validation and Verification

As soon as you have an executable user interface or prototype, you need to answer an all-important question: the users told you what they wanted, but is it what they need?

Does it meet the functional requirements of the system? This, too, needs to be tested. A bug-free system that answers the

wrong question isn’t very useful. Be conscious of end-user

access patterns and how they differ from developer test data (for an example, see the story about brush strokes here).

Performance Testing

Performance or stress testing may be important aspects of the project as well.

Ask yourself if the software meets the performance

requirements under real-world conditions—with the expected

number of users, or connections, or transactions per second. Is it scalable?

For some applications, you may need specialized testing

hardware or software to simulate the load realistically.

Testing the Tests

Because we can’t write perfect software, it follows that we can’t write perfect test software either. We need to test the tests.

Think of our set of test suites as an elaborate security system, designed to sound the alarm when a bug shows up. How better

to test a security system than to try to break in?

After you have written a test to detect a particular bug, cause the bug deliberately and make sure the test complains. This

ensures that the test will catch the bug if it happens for real.

Tip 92

Use Saboteurs to Test Your Testing

If you are really serious about testing, take a separate branch of the source tree, introduce bugs on purpose, and verify that the tests will catch them. At a higher level, you can use something like Netflix’s Chaos Monkey[81] to disrupt (i.e.,「kill」) services and test your application’s resilience.

When writing tests, make sure that alarms sound when they

should.

Testing Thoroughly

Once you are confident that your tests are correct, and are

finding bugs you create, how do you know if you have tested the code base thoroughly enough?

The short answer is「you don’t,’’ and you never will. You might look to try coverage analysis tools that watch your code during

testing and keep track of which lines of code have been executed and which haven’t. These tools help give you a general feel for how comprehensive your testing is, but don’t expect to see 100%

coverage.[82]

Even if you do happen to hit every line of code, that’s not the whole picture. What is important is the number of states that your program may have. States are not equivalent to lines of code. For instance, suppose you have a function that takes two integers, each of which can be a number from 0 to 999:

int test(int a, int b) {

return a / (a + b);

}

In theory, this three-line function has 1,000,000 logical states, 999,999 of which will work correctly and one that will not

(when a + b equals zero). Simply knowing that you executed this line of code doesn’t tell you that—you would need to identify all possible states of the program. Unfortunately, in general this is a really hard problem. Hard as in,「The sun will be a cold hard lump before you can solve it.」

Tip 93

Test State Coverage, Not Code Coverage

Property-Based Testing

A great way to explore how your code handles unexpected states is to have a computer generate those states.

Use property-based testing techniques to generate test data according to the contracts and invariants of the code under test.

We cover this topic in detail in Topic 42, Property-Based

Testing.

TIGHTENING THE NET

Finally, we’d like to reveal the single most important concept in testing. It is an obvious one, and virtually every textbook says to do it this way. But for some reason, most projects still do not.

If a bug slips through the net of existing tests, you need to add a new test to trap it next time.

Tip 94

Find Bugs Once

Once a human tester finds a bug, it should be the last time a human tester finds that bug. The automated tests should be

modified to check for that particular bug from then on, every time, with no exceptions, no matter how trivial, and no matter how much the developer complains and says,「Oh, that will

never happen again.」

Because it will happen again. And we just don’t have the time to go chasing after bugs that the automated tests could have found for us. We have to spend our time writing new code—and new

bugs.

FULL AUTOMATION

As we said at the beginning of this section, modern

development relies on scripted, automatic procedures. Whether you use something as simple as shell scripts with rsync and ssh, or full-featured solutions such as Ansible, Puppet, Chef, or Salt, just don’t rely on any manual intervention.

Once upon a time, we were at a client site where all the

developers were using the same IDE. Their system

administrator gave each developer a set of instructions on

installing add-on packages to the IDE. These instructions filled many pages—pages full of click here, scroll there, drag this, double-click that, and do it again.

Not surprisingly, every developer’s machine was loaded slightly differently. Subtle differences in the application’s behavior occurred when different developers ran the same code. Bugs

would appear on one machine but not on others. Tracking down version differences of any one component usually revealed a

surprise.

Tip 95

Don’t Use Manual Procedures

People just aren’t as repeatable as computers are. Nor should we expect them to be. A shell script or program will execute the same instructions, in the same order, time after time. It is under version control itself, so you can examine changes to the

build/release procedures over time as well (「but it used to work…」).

Everything depends on automation. You can’t build the project on an anonymous cloud server unless the build is fully

automatic. You can’t deploy automatically if there are manual steps involved. And once you introduce manual steps (「just for this one part…」) you’ve broken a very large window.[83]

With these three legs of version control, ruthless testing, and full automation, your project will have the firm foundation you need so you can concentrate on the hard part: delighting users.

RELATED SECTIONS INCLUDE

Topic 11, Reversibility

Topic 12, Tracer Bullets

Topic 17, Shell Games

Topic 19, Version Control

Topic 41, Test to Code

Topic 49, Pragmatic Teams

Topic 50, Coconuts Don’t Cut It

CHALLENGES

Are your nightly or continuous builds automatic, but deploying to production isn’t? Why? What’s special about that server?

Can you automatically test your project completely? Many teams are forced to answer「no.」Why? Is it too hard to define the acceptable results? Won’t this make it hard to prove to the sponsors that the project is「done」?

Is it too hard to test the application logic independent of the GUI?

What does this say about the GUI? About coupling?

Topic 52

Delight Your Users

Our goal as developers is to delight

users. That’s why we’re here. Not

When you enchant

to mine them for their data, or

people, your goal is not

count their eyeballs or empty their

to make money

wallets. Nefarious goals aside,

from them or to get

even delivering working software

them to do what you

in a timely manner isn’t enough.

want, but

That alone won’t delight them.

to fill them with great

delight.

Your users are not particularly

motivated by code. Instead, they

have a business problem that

Guy Kawasaki

needs solving within the context of

their objectives and budget. Their

belief is that by working with your team they’ll be able to do this.

Their expectations are not software related. They aren’t even implicit in any specification they give you (because that

specification will be incomplete until your team has iterated through it with them several times).

How do you unearth their expectations, then? Ask a simple

question:

How will you know that we’ve all been successful a month (or a year, or whatever) after this project is done?

You may well be surprised by the answer. A project to improve product recommendations might actually be judged in terms of customer retention; a project to consolidate two databases

might be judged in terms of data quality, or it might be about cost savings. But it’s these expectations of business value that really count—not just the software project itself. The software is only a means to these ends.

And now that you’ve surfaced some of the underlying

expectations of value behind the project, you can start thinking about how you can deliver against them:

Make sure everyone on the team is totally clear about these

expectations.

When making decisions, think about which path forward moves

closer to those expectations.

Critically analyze the user requirements in light of the expectations.

On many projects we’ve discovered that the stated「requirement」

was in fact just a guess at what could be done by technology: it was actually an amateur implementation plan dressed up as a

requirements document. Don’t be afraid to make suggestions that change the requirement if you can demonstrate that they will move the project closer to the objective.

Continue to think about these expectations as you progress through the project.

We’ve found that as our knowledge of the domain increases,

we’re better able to make suggestions on other things that could be done to address the underlying business issues. We strongly believe that developers, who are exposed to many different

aspects of an organization, can often see ways of weaving

different parts of the business together that aren’t always

obvious to individual departments.

Tip 96

Delight Users, Don’t Just Deliver Code

If you want to delight your client, forge a relationship with them where you can actively help solve their problems. Even though your title might be some variation of「Software Developer」or

「Software Engineer,」in truth it should be「Problem Solver.」

That’s what we do, and that’s the essence of a Pragmatic

Programmer.

We solve problems.

RELATED SECTIONS INCLUDE

Topic 12, Tracer Bullets

Topic 13, Prototypes and Post-it Notes

Topic 45, The Requirements Pit

Topic 53

Pride and Prejudice

Pragmatic Programmers don’t

shirk from responsibility. Instead,

You have delighted us

we rejoice in accepting challenges

long enough.

and in making our expertise well

known. If we are responsible for a

Jane Austen, Pride and

design, or a piece of code, we do a

Prejudice

job we can be proud of.

Tip 97

Sign Your Work

Artisans of an earlier age were proud to sign their work. You should be, too.

Project teams are still made up of people, however, and this rule can cause trouble. On some projects, the idea of code ownership can cause cooperation problems. People may become territorial, or unwilling to work on common foundation elements. The

project may end up like a bunch of insular little fiefdoms. You become prejudiced in favor of your code and against your

coworkers.

That’s not what we want. You shouldn’t jealously defend your code against interlopers; by the same token, you should treat other people’s code with respect. The Golden Rule (「Do unto

others as you would have them do unto you’’) and a foundation of mutual respect among the developers is critical to make this tip work.

Anonymity, especially on large projects, can provide a breeding ground for sloppiness, mistakes, sloth, and bad code. It

becomes too easy to see yourself as just a cog in the wheel, producing lame excuses in endless status reports instead of

good code.

While code must be owned, it doesn’t have to be owned by an

individual. In fact, Kent Beck’s eXtreme Programming[84]

recommends communal ownership of code (but this also

requires additional practices, such as pair programming, to

guard against the dangers of anonymity).

We want to see pride of ownership.「I wrote this, and I stand behind my work.」Your signature should come to be recognized as an indicator of quality. People should see your name on a piece of code and expect it to be solid, well written, tested, and documented. A really professional job. Written by a

professional.

A Pragmatic Programmer.

Thank you.

images/dave_and_andy.png

Footnotes

[75] As team size grows, communication paths grow at the rate of

, where

is the

number of team members. On larger teams, communication begins to break down and becomes ineffective.

[76] A burnup chart is better for this than the more usual burndown chart. With a burnup chart, you can clearly see how the additional features move the goalposts.

[77] The team speaks with one voice—externally. Internally, we strongly encourage lively, robust debate. Good developers tend to be passionate about their work.

[78] Andy has met teams who conduct their daily Scrum standups on Fridays.

[79] See https://en.wikipedia.org/wiki/Cargo_cult.

[80] We’ve seen this first-hand more times than you’d think.

[81] https://netflix.github.io/chaosmonkey

[82] For an interesting study of the correlation between test coverage and defects, see

Mythical Unit Test Coverage [ADSS18].

[83] Always remember Topic 3, Software Entropy. Always.

[84] http://www.extremeprogramming.org

Copyright © 2020 Pearson Education, Inc.

In the long run, we

shape our lives, and we

shape ourselves. The

process never ends

until we die. And the

choices we make are

ultimately our own

responsibility.

Eleanor Roosevelt

Chapter 10

Postface

