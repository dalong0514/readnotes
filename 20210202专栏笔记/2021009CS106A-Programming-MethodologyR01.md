## 记忆时间

## 目录

0101 Why is the class called Programming Methodology?

0201 Running a Karel Program

## CS106A-Programming-Methodology-Lecture0101

Topics: Welcome to CS106A, Course Staff, Why is the class called Programming Methodology?, Are you in the right class?, Class Logistics, Assignments and Grading, Extensions, Midterm and Final, Grade Breakdown, The Honor Code, Why Karel?

Instructor (Mehran Sahami): Alrighty. If you could have a seat, please, we need to get started. There are still a bunch of people coming in the back. Come on down and try to find a seat somewhere. If you can't find a seat, sit in the aisle as long as you're not a fire marshal. Anyone here a fire marshal? Good. We're fine. Come on in and sit in the aisles.

So welcome to CS106A. If you don't think you should be in CS106A, you think you should be somewhere different, now is probably a good time to go, not that I would discourage anyone from taking this class. I think we'll have a lovely time in here. But this class is CS106A or E70A, so if you're, like, "Wait. I thought I was in E70A," you're fine. They're the same class; it's the same thing. No worries, okay?

There's four handouts. They're in the back. If you haven't already gotten the handouts because you came in and you sat down, don't worry. You can pick them up on the way out. They're the same handouts. They'll still be there.

So just a quick introduction. That's what the first four handouts actually give you. They give you a little bit of an introduction to the class, what we're gonna cover, some logistics for the class and some other stuff. I'm gonna go over all that today so we can sort of get a good idea for where we're at, okay?

So just a quick show of hands before we get into a bunch of things in the class. This is kind of an intro-programming course; well, it is. I shouldn't say it's kind of an introprogramming course. It is an intro-programming course. And it's always good to get an idea as to how much familiarity you may have beforehand, okay? So just quick show of hands. How many people can recognize a computer that's on? Good, good. That's the prerequisite for this class.

So if you're worried about how much previous experience you've had or your friend who, like, worked their way through high school by programming for Google or whatever, don't worry about it because all you need to know in here is basically either how to turn a computer on or to recognize a computer that's on if you were to walk up to it and it were already to be on, all right?

So but a little bit more seriously, how many people have actually used a computer for anything? All right. I would expect most of you.

So now, we begin to bump it up a notch. How many people have used it for word processing? Okay. Most folks.

How many people have done web browsing? Yeah, I won't ask you what you look at, all right? It's just I don't wanna know.

How many people have actually created a web page? Okay. Fair number. How many people have done any kind of programming before? Fair number. All right.

How about how many folks have done actually programmed in Java before? All right. A few folks.

How about another language, C, C++, BASIC, anyone program in BASIC? Yeah, oh, I love — that was the first language I learned, and it was kind of like the warm and fuzzy, and I felt good. There was actually people who argued that if you learn BASIC as your first language, you're brain damaged, then you're just beyond help. But if that's the case, we're all in the boat together because I'm probably brain damaged as well. The truth is I probably am, but that's a whole different story.

All right. So one thing you should know kind of up front is actually this course is gonna be provided eventually somewhere down the line as part of Stanford School of Engineering Free Course Initiative, which means not only are we recording this course to broadcast to a bunch of companies and industry who are watching this course, but we're eventually gonna provide it free to the world.

So how does that impact your life? And on the average day, it doesn't at all. The only way it does impact your life is just so you should know, the lawyers told me to tell you that your voice, should you ask a question, may actually be recorded as part of the video. As a result, your voice may end up going out to thousands of people or millions of people in the world. If you have an issue with that, come talk to me. If you don't, everything is just fine, all right?

Don't worry. We're not gonna put your picture up or anything like that. You might wanna be on the video, like, "Hey, ma, I'm on TV." We decided that we're just gonna not show anyone actually on the video, but your voice may actually get recorded, okay?

Now, along those lines, you may also notice there are some microphones in the room. So when you wanna ask a question, please make sure to use the microphone because that's not only good for people in here to be able to hear your question, it's also good for all the folks that this is getting broadcast to because not only are we gonna broadcast to the world, but there's actually some folks who are sort of watching this live now in various companies in Silicon Valley.

So it's real important that you actually use the microphone, so just remember that. And every once in a while, I might get on your case and be, like, "Please use the microphone." I'm not trying to be argumentative or anything. I just wanna make sure we pick up all the audio, all right?

So with that said, a little bit of an introduction. That's kind of a way of background. I didn't give you any sort of introduction. So just to introduce myself, my name's Mehran Sahami. I'm the professor for the class. Don't call my Professor Sahami, way too formal. Don't call me Mr. Sahami. That, I think of my dad. And don't call me Mrs. Sahami, or we're gonna have issues, all right? So just call me Mehran. We'll get along. It's just fine, all right? It's to keep things a little bit more informal, but that way it's a little bit easier to discuss stuff as you go along.

There is also a head TA for the class, Ben Newman, who's standing up there. Get to know Ben. He has all the real power in this class. I'm just kind of the monkey that gets up here and gives the lectures. But Ben really is the one who's got all the power.

Along with the head TA for the class, we have a large section leading staff. So the section leaders here, could you stand up if you're here? They're kind of all over the place, some over here, some over there, and some over there. As you can see, there's a pretty large number of folks. And this isn't even all of them. We sort of have more — we just can't stuff them all into the room — who are section leaders for the class, and these folks are all here to make sure that everyone in this class has as good an experience as possible when we're sort of going through the class.

And the best way to reach all of us is email. So on Handout No. 1, you get my email and Ben's email. We'll tell you how to sign up for section. That's how you'll meet your section leader and get your section leader's email. That will all be coming soon. But email really is kind of a happy form of communication to get a hold of us, okay?

So with that said, I wanna tell you a little bit about this class and kind of what we're gonna do in here and what you should expect and make sure that you don't feel scared off by this class, okay? Because it really is meant to sort of be an interesting time.

But one question that comes up is why is this class called Programming Methodology, right? Why don't we just call this class, like, Programming with Java? And the real reason for that is that programming methodology is about good software engineering principles. It's about something that's much larger than just programming.

So some people, like, they'll go and get a book somewhere and they'll think they learned how to program by just reading the book. And they're, like, "Oh, I know how to program. Isn't that great?" And it's, like, yeah, you might know the mechanics of the language, but the mechanics of the language are nothing compared to understanding the software engineering principles that go into actually developing a software system.

And that's what you're gonna learn about in this class. You're gonna learn a lot of those principles. But in order to be able to use those principles and apply them, you also need to have the language to program in, and that language that we're gonna use in this class is Java.

So the way I like to think about it and the way I tell a lot of people is writing a good program or learning how to program is like learning to be a good essay writer. And you're, like, "Oh, but part of the reason I'm taking this class, Mehran, is that I don't like writing essays." That's fine. It's okay. Trust me. I didn't like writing essays either. But the whole point is that when you write an essay, it's not a formulated kind of thing. You're, like, "Well, what about five-paragraph essays?" Yeah, just block that from your mind. That was a bad time, right? That was just, like, '70s education at work. It's not a formulated kind of thing.

There's an art to writing an essay, right? In order to write an essay, you need to know a language. You need to know English or German or Hindi or whatever language you wanna use, but then you use that language to write an essay. Just knowing the language doesn't make you a good essay writer though. Being a good essay writer makes you a good essay writer.

So that's the same difference in programming and software engineering. Knowing the language, in order to be a good programmer, like a good essayist, you need to know a language to write your programs in, whether that be Java or C or C++ or whatever. Here we're gonna use Java.

But just knowing the language doesn't make you a good software engineer and doesn't make you understand what the principles are of writing good software, which is what you're also gonna get in this class in addition to the language, and that's kind of a key thing to stress.

So if you're sort of worried, if you were kind of looking around and you saw a bunch of people raising their hands when I asked, "Do you have any previous programming experience?" and some folks raised their hands, and you got a little worried and you're like, "Oh, am I gonna be in some sense at a disadvantage because I haven't done any programming before?" The answer, plain and simple, is no, okay? You're gonna learn everything you need to learn from the first principle because as a matter of fact, in some cases you might be in slightly better shape. That's not necessarily to say that that's the way it will be.

But how many people are Star Wars fans? Just wondering. Anyone? I'm talking about the old-school, original, like, three movies. Those were so good, and we're not — no George R. Binks here, all right? So if you remember — and sort of I'm a big Star Wars fan, and that's just a whole separate point. But in the second movie, Yoda actually said something which I thought was quite profound, which is he says sometimes you have to unlearn what you have learned.

And one of the things we actually find is that some people who are self-taught programmers, some of them are just fine, and some of them are very good. But some of them have picked up some really bad habits along the way, and it's like being a bad essay writer. And to go from being a bad essay writer to a good essay writer, in some cases, can actually be harder than from not being an essay writer to being a good essay writer because you have to unlearn the bad habits.

So if you're worried about, "Oh, I've had no previous experience," don't worry. You're okay, blank slate, you're just fine. And now if you're thinking, "Oh, I have some previous experience. Do I have bad habits?" Don't worry. You'll be fine, too, okay? So it's all gonna work out.

So the next question that kind of comes up — hopefully that helps put some of your fears aside. Another one of the things is that we really strive to make everyone successful in this class, okay? At some other schools, people wanna do computer science or they wanna do an engineering major or whatever. And you come into the first day of class, and they say, "Oh, only one third of you are actually gonna make it through this program. And look to the person to your left and look to the person to your right, and only one of you will make it through." And you're, like, "Oh, man, that's real nice." It's not like that here.

As a matter of fact, we want all of you to be extremely successful in this class, which is why we have a huge course staff, which is why over years and years we've refined how we do a lot of the teaching in this class to make sure you have the best possible experience and to make sure that everyone gets through.

And the important thing about that is that you're not competing against anyone except yourself in this class. It's not like we're gonna have a curve and we're gonna say, "Oh, we have a certain number of "F"s and a certain number of "D"s and a certain number of "C"s." All we really have going into it is an expectation that when you get out of here, there's a set of stuff we want you to know. And if you know that stuff well, you get an "A." And if everyone knows that stuff well, everyone gets an "A." And I got no problems with that. Registrar might have a problem with that, but that's okay. You don't need to worry about that.

So you don't need to think about, oh, is someone else doing better than you or whatever. And we'll talk about issues of collaboration in just a little bit. All you need to think about is learning the stuff yourself as well as you possibly can, and you'll be just fine and you'll get a good grade, okay? So that's really all we ask, which is not a trivial amount, right? It requires you to really understand the material.

So another question that comes up is are you in the right place, right? This isn't the only introductory programming class at Stanford. And so I wanna spend a little bit of time making sure you actually are in the right place by going over some of the different options.

So right now, as you know, you're in CS106A. And CS106A, we're sort of happy over here, right? As a matter of fact, we're not only happy, we're happy and we're also a little bit loopy, right? There is no previous programming experience required, as I mentioned, right? All you need to know is basically if you can get to a computer and know how to figure out that it's on, you're in good shape.

But what 106A does is it's a real rigorous class. You learn programming in here, and you learn it in a way that makes you ready to be an engineer if you so choose to be an engineer. That's not to say you're all gonna be engineers. I would love for all of you to be computer science majors, but statistics in the past show only about 6 percent of you will be computer science majors. That's not because we turn anyone off to computer science; it's because we make programming accessible to so many people that you don't have to be a computer science or a Double E or even an engineering major to do extremely well in the class.

And we actually have sort of a significant percentage of the entire campus undergraduate student body at Stanford actually goes through this class and does well, okay? So don't worry if you're, like, "Oh, but I'm not really a CS person." I hope we'll turn you into one by the end of the class. No, it's okay. But you'll be prepared if that's what you wanna do. So this leads into a whole engineering sequence that can go on to other engineering majors or the computer science majors.

If you're, like, "Huh, I'm not sure if that's really what I wanna do. As a matter of fact, I'm so sure that's not what I wanna do, I only wanna get the general educational requirement out of the way, and I'm positive there is nothing else I wanna do. Really, no matter how much I like it, like, there is no way you're gonna drag me into anything that would involve anything remotely techie." They're the class CS105. And this is happy, yeah, this is kind of, oh, we're happy in our little happy world. And I don't wanna say it's holding hands and singing, "Kumbaya," because that's not what it is. It's a real class. But it's meant to be a general educational requirement, right? It doesn't lead into the 106s. It's meant to be its own self-contained class. You do some Java script in there. You do a little bit of what computers are about.

Computers in society is a good time. We all hold hands. We're all happy. I don't teach the class, so I don't actually hold hands. But it's a fun time, okay? It just doesn't lead to anything else. So think of this as kind of a terminal class, right? So it's sort of like, well, we'll hook you up to the IV drip.

And you're, like, "Well, 106A, you told me I don't need any previous background. Well, hey, Mehran, I got lots of background. I got so much background, it hurts. I got AP background, I got working through school doing software engineering background. I'm not sure I should be here." That could be the case.

We have another class called CS106X, and as the "X" kind of implies, it's sort of the extreme games version of the class. No, it stands for accelerated, right, because "A" was already taken, so we had to come up with something else. So the way CS106X works is it really is a very fast-paced class. It's meant for people who've got previous AP exam credit, like, got a 4 or 5 on the AP, or have had significant and prior programming experience before.

If you're not sure which one of these classes is for you, you can come talk to me afterwards, or I'd also encourage you, you could go to pick up the syllabus for CS106X and compare it to CS106A. This class is all in C++. And if you're thinking, "Hey, Mehran, I'm doing 106A. I wanna learn Java and C++," don't worry. You'll eventually, if you so choose, take a class called CS106B, which is where this class sort of leads to, which is C++ and all of the other stuff you would have learned in this accelerated class, okay? So you still certainly have that course path.

So don't let anyone make you think — I know a lot of times, and especially for Stanford students, you come in here and you're, like, "Well, every class I took in high school was like an honors or an AP class, or if it wasn't an honors or an AP class, like, I had to tie half my brain before my head because I'm just that hardcore." And so everyone just wants to, like, do the most hardcore thing they can, right? And what I'm here to tell you is that you shouldn't necessarily think about it that way. You should think about it as where you feel most comfortable.

Some number of years ago, let's just say greater than 10, maybe 15, I was sitting where you're sitting right now, literally. I was in CS106A in Terman Auditorium as a freshman, okay? It was perfectly fine. It worked out. I went to grad school, did the faculty thing. It's just fine. It will open your doors to CS. You're not at any kind of disadvantage by starting here. So know where you've been, literally. Like, that seat right there was where I was most of the time. So just something to keep in mind in terms of the different options that are actually available to you.

Now, with that said, let's just assume for the rest of this lecture that this is the right place for you. And if it's not, well, afterwards we can kind of talk about it, or if you really are convinced now that it's not the right place, you can feel free and try to scramble over 20 of your classmates and actually leave the room, which is probably impossible.

All right. So a few other things you should know, some mechanics. So Handout No. 1, should you wanna follow along at home, is the class web page. And so all the stuff that we think of as course materials, including online copies of the handouts, things that you'll need to do for the assignments, announcements related to the class are all on the class web page, which is www.stanford.edu/class/cs106a. And because that's just kind of a whole bunch to remember, we make your life easy and so there is an equivalent form of the URL, which is just cs106a.stanford.edu, which is the easy thing to remember. You put that in, it'll take you to the class web page, okay?

And you should check that regularly because all the announcements and handouts we'll give out hard copies of all the handouts in class, but should you happen to miss class for whatever reason, you wanna go print whatever copies of the handouts we're actually giving out, you can find them all on the web page, okay?

Now, there's this funky thing about units. So you may have noticed that this class is for three to five units, and that kind of brings up the natural question, "Should I take it for three or five units?" If you're an undergrad, you take it for five units, end of story. That's life in the city. Congratulations. Five units.

If you're a graduate student, you can have the option of taking it for three units if you want, if you're gonna run into some unit cap. It doesn't change the amount of work you have to do. Welcome to graduate school. Same work, fewer units. So that's just the way life is. If you have a unit cap and you're a grad student, in three units you can take it if you want. You can take it for five if you want as well. If you're an undergrad, you take it for five, all right?

So why is it five units? And you might think, "Hey, this class only meets three times a week. How come it's five units?" Well, it actually has a fourth meeting every week, which is your section, and that's something you should sign up for. So how you actually sign up for your section is sections are at a bunch of different times. You don't sign up for them in Axess, even though they're all kind of listed in the time schedule. That's not where you sign up for them. In Axess, you just sign up for the class.

How you sign up for a section is you go to a website, cs198.stanford.edu/section and this will give us a list of preferences for section times that you wanna sign up for, and there's some matching process that goes on. It takes all your preferences into consideration with the whole system, and eventually you get an email by sometime early next week that tells you what section you're in. And section's 50 minutes, once a week. It's required to go to. It's actually gonna be part of your class participation grade, which we'll talk about in just a bit, okay?

When do these sign-ups happen? They happen between 5:00 p.m. this Thursday is when they go up. So if you try to go there now, you can't sign up. Remember 5:00 p.m. Thursday. So they're up, and then they're down at 5:00 p.m. on Sunday, okay? So make sure you sign up probably this weekend. If you're planning on being out of town this weekend, you wanna sign up before you go. Sign up early, but don't sign up often because you only need one section, okay?

If you're an SCPD student — every once in a while you'll hear me refer to SCPD students. That stands for Stanford Center for Professional Development. They are the folks in industry who actually take this class via broadcast. If you're an SCPD student, you're automatically enrolled for a section, so you don't actually need to do this, and your section will meet at — so for SCPD — and if you're wondering what an SCPD student is, you're not one, okay? So SCPD section meets Friday from 1:15 to 2:05. It meets live, if you wanna go there live, in Skilling Auditorium. But if you're watching it remotely, it meets on Channel E2. I know it seems weird to say it meets on channel — what does that mean? It meets on Channel E2, okay? That is grammatically the correct way of saying it.

All right. So there's a little bit more administrative stuff. Now, textbooks, right? Textbooks, there's nothing quite like the extortion that is textbooks. So there are two textbooks that are required for this class. Well, one's a course reader and one's a textbook.

The course reader is called, Karel the Robot Learns Java. You can pick it up at the bookstore. It's relatively cheap. It was actually written by Eric Roberts here. And surprisingly enough, the textbook for the class was also written by Eric Roberts, The Art and Science of Java, which is available now in your local bookstore, including the bookstore on campus, so you can go and pick up a copy of this. So both these things you actually wanna have because they're required for the class. We'll go through all of them. We'll go through basically everything except the last chapter of this book. So you sort of get your money's worth. We're just gonna do it a little bit out of order, but we'll go through the whole thing, okay?

1-2『原来第一个「Karel the Robot Learns Java」不是书籍，是这门课的一个独有资料，已下载作为本书的附件。已下载书籍「2021074The-Art-and-Science-of-Java」。（2021-04-25）』

So email, how many of you have email accounts? All right. I will ask the reverse question because I think at this point, some people just don't wanna put up their hands. How many people don't have email accounts? Odd how that is not the complement of the folks who had their hands up previously. Email's required for this class. Chances are, by being at Stanford, you've already gotten an email account through your SUNet ID, but if you don't have an email account, get an email account and that's how you'll stay in contact with us. That's how we'll stay in contact with you, except we'll also meet with you live in person, but email is kind of the general method for communication.

As a matter of fact, for your first assignment, and part of your first assignment is to send us an email, just because we love you and we don't get enough email as it is. So you need to have an email account to be able to do that. So if you have not already, you can kind of get ahead of the game and go set up your email account. Now, don't worry. You'll get the first assignment next time. So you still get, like, two days of breathing space before your assignment goes out, okay?

There is also gonna be lots of handouts in the class. They'll be either given out in class, well, they will be given out in class, but we'll also post them online in case you miss them.

And how much real work do you do in this class? That's always kind of an interesting question. So let's talk a little bit about assignments and a little bit of other logistical things. So assignments, we'll just call them the dreaded assigns. There are seven programming assignments. And if you look at the syllabus Handout No. 2, it tells you when all of them are due all the way through by day, so you can plan out your whole quarter. It's just that much fun, okay?

And these seven programming assignments are weighted slightly more toward the last assignments because the assignments will tend to get more complicated. That doesn't necessarily mean there'll be more programming; it just means conceptually, they'll become more complicated, so we tend to weigh them more toward the end of the class. So the later assignments count more than the early assignments.

How you're gonna be actually doing your programming is using a little tool called Eclipse. And Eclipse thankfully is free, so you don't have to pay for it. As a matter of fact, you can download it from the CS106A website. And if you're wondering how you do that, don't worry. We'll give you a handout next class that explains to you the whole grueling process of downloading and installing Eclipse.

And you can use this either on the Mac or the PC. So if you have your own computer, you can certainly work on this yourself. You just download it to your own machine. We'll explain the whole process in a handout. If you don't have your own computer, the public computer clusters on campus will have Eclipse installed on them, and so you can use Eclipse there. So you're sort of happy to go either way, okay?

Now, the important thing, remember I mentioned that whole notion of software engineering in the class, and that's something we take really seriously, so seriously as a matter of fact that when you turn in your assignments, one thing we could do is we could take your assignments and we could just kind of look at it and go, "Yeah, interesting, 'B.' Here you go. Thanks for playing." And you don't learn a whole lot from them. So in order to actually learn a lot from your assignments, we could take your assignment and write a whole bunch of comments on it and hand it back to you. Even that's kind of not enough.

What really is a little bit more that makes it more fun is every week after you turn in your assignment and your section leader looks it over and grades it, you'll actually meet with your section leader for about 10 to 15 minutes every week or every time an assignment is due to actually go over in something referred to as interactive grading.

And it's a chance to sit there and talk with an actual human being about what's good in your assignment, what are some of the things you need to work on, what are some of the software engineering principles you need to develop. And that way, you can really sort of get more detailed information and be able to ask questions to develop yourself as a programmer as well as get help if you need help, okay?

And that's in addition to going to section, going to class and all that stuff. So it's another 15 minutes a week. You'll actually schedule that time with your section leader on a regular basis when you're gonna have interactive grading or just affectionately referred to as IGs because at Stanford, everything's just short and we just can't say, like, psychology; we have to say psyche. So it's IG. Just remember that, all right?

And then how are these things graded? So the other thing we could do is I told you we could just write "B" and hand it back to you. But we found that that's not really great because people get all wrapped around the axle about the grade.

And so for a while, we did numbers and we're, like, huh, why don't we give a number between 1 and 20? And so what happens there? People get all wrapped around the axle about numbers.

So then we thought, huh, what was a happier time when we were in school? I remember when we were in school, and we used to get back assignments and they had, like, smiley faces on them. Well, we can't do that because then it doesn't appear to be a rigorous Stanford class.

So instead of the smiley face, we come up with something else, which looks surprisingly like this. It's kind of involved to actually draw, so I need to erase the board to do it. Check. That's kind of the beginning of our grading scale, okay? And the way our grading scale works is we start off with a check in the middle, which says this is a pretty solid program. It meets all the requirements for the program. Maybe it's got a little problem here or there, but it's a check. Then we have sort of two grades on the two sides of it: check plus and check minus.

Check plus is, like, solid. You did a great job; you got everything right; things look good, a nice style in your program, nice software engineering, and the program works flawlessly. Good job. This is like total "A." Check is kind of like, yeah, you're sort of there. It's kind of like "A" minus, "B" plus, maybe on some occasions "B." But it's kind of like it's pretty good work; you're in pretty good shape here. And so a lot of grades in this class ends up being check pluses and checks, and if that's the case, you're perfectly fine grade-wise.

Check minus, as you can imagine, this is kind of thinking about "B," "B" minus. It's, yeah, there are some slightly more significant problems with your program.

But that's not where it ends, right, because we wanna be able to even shoot for in some sense bigger gustoes. There was a plus and a minus. So plus is like, oh, nice job, kind of a hearty pat on the back. If you get pluses all the way through on all your assignments, you're in a pretty good candidate to get an "A" plus.

And minus, like, just take good over here and replace it with bad, it's kind of like, oh, bad times, right, or maybe, you know — but even there was, like, more significant problems with this program or just the style on the program is just really bad. But even there, we don't stop. And you're, like, "Come on, man. Like, I thought the whole reason was to simplify this." Don't worry.

And it gets even better because we have a plus-plus and a minus-minus. And at this point, we've run out of board space, so we can't go any further. But a plus-plus is just outrageous, right? It's the kind of thing — so this is the kind of thing your section leader can't actually give you without coming and talking to Ben and I first because they get a program that just goes — it has to actually exceed the requirements for the assignment. It's by a long shot. Like, you'll get all your assignment requirements, and what we encourage you to do is you can do a grade assignment and get everything right and have good style, and you'll be in this category. And for the later assignments, you may be in this category if it's flawless.

But we'll actually — if you want to go for the plus-plus, go beyond the assignment requirements. And the way we think about the plus-plus, it's a program that makes you weep in a good way. It's just like your section leader sees it, and they're just, like, this is so good, I've gotta show someone else. And they come and show Ben and I, and we're, like, sitting there looking at this on a monitor, and, like, tears are just welling in our eyes, and there was, like, soft violin music playing in the background and we get out the wine and cheese. So this is just, like, this is the kind of thing that gets you, like, remembered and the, oh, if you want a letter of recommendation, just ask because you got a plus-plus. Like, oh, it's awesome, right?

There are very few of these in a quarter. So just by sort of way of comparison, in a class this size, probably throughout the span of the whole quarter, I'd expect there to be maybe ten plus-pluses, I mean, ten assignment plus-pluses, not ten students who get plus-pluses across the board. So it's really something to strive for, but if you strive for it, like, we're giving you the credit for it. And this gets remembered and you get, like, extra credit and everything.

So we're left with this, right? This assignment also makes you weep, but not in the good way, right? It makes you kind of weep in the sense, like, I look at them and I'm, like, oh, man, like, what did I teach? Like, where did I go wrong, right? I, like, blame myself. I blame you a little bit, but I blame myself. And this is really just, like, the program is just, like, it's a shell. Like, there really wasn't much effort that was put into it. Yeah, you slapped something together or it doesn't really work, that whole deal.

And then if you don't turn anything in, we do kind of reserve the zero to distinguish from the "made really bad effort" versus "didn't make any effort at all." And we just won't talk about these, right? Let's just hope we can avoid those if possible. But that's kind of how the grading scale works now.

Now, at the same time, I trust all of you to be responsible people. And every once in a while, something bad happens to a good person, and there's an assignment that you'd like to be able to turn in, but for whatever reason, you can't turn in on time. And I just wanna treat you like adults. I don't want you to have to worry about coming in and asking for an extension or, like, "Oh, I had this really hard thing in another class, and I couldn't do it at the same time." Up front, everyone gets two free extensions, okay? So in terms of late days — we refer to these as late days, strangely enough — you get two free ones.

What a late day is, is a class day. They're not 24-hour days, but class days. So if something is due on a Wednesday, you turned in on a Friday, that's a late day. That's one. You turn it in on the following Monday, that's two late days. You can split up your two late days among two different assignments. You can use them both on one assignment.

But we encourage you to not use them at all because if you use your late days, you fall behind in the class. The way you should think about these things are these are preapproved extensions. They're not the kind of thing where you just think, "Oh, yeah, I'm not gonna do the assignment because I wanna go and play Frisbee golf," right? Think of it, well, you wouldn't come ask me for an extension — you might, but you probably wouldn't ask me for an extension if you're, like, "Hey, hey, Mehran, can I turn in the assignment, like, on Wednesday because I'm playing Frisbee golf this afternoon," right? If you would feel embarrassed asking that question, you probably don't wanna use one of your free late days. But something happens like, oh, it's a tough week, you've got midterms in other classes and you got this assignment due or whatever, that's a good time to use it. So we just trust you. And most people, we actually encourage you not to use them because it just makes you fall behind in the class.

Because we trust you and we give you these two up front, getting extensions beyond your two free class days is virtually impossible because we sort of up front said, hey, it's your responsibility. We're giving you two freebies. We're not gonna give you a third extension. Imagine if you had to come ask us for three extensions. By the third one, we'd be, like, okay, what's going on, which is why we don't necessarily give extensions beyond these two.

The only time we might give an extension beyond the two free ones is for something major, like death in the family or, like, serious medical problems that might require surgery or something like that. Every once in a while, unfortunately, that happens. I hope it doesn't happen in this class. But those are the only kinds of things that we give extensions to beyond the two free late days.

Importantly, don't ask your section leader for extensions. They cannot grant you extensions. Only Ben, who has all the power in this class, can give extensions, which is why you should get to know Ben and then hopefully you won't need to talk to him about extensions, okay?

So other thing to keep in mind is that three days late is the max. Beyond three days late, which is basically one class week, if you think about late days being class days, we will not accept an assignment. And the reason for that is at a certain point, you're so late, you're better off just doing the next assignment, letting the old one go. So to sort of enforce that policy, after three days, we don't accept that assignment late anymore. It's just gonna be a zero if it's not turned in, okay? And that just kind of forces you to keep up.

Couple other minor things, well, I shouldn't say they're minor things. They're actually kind of important. Exams: There's two exams in this class. There's a midterm and a final. Both of them are, well, I shouldn't say both. The midterm is out of class. It's from 7:00 to 8:30 p.m. on Tuesday, October 30. And it's on the syllabus. It's there. It's on the syllabus; it's on Handout No. 1. We repeat it multiple times. The date will eventually be announced when we get close to the midterm.

But if you have a conflict with this time, you need to send me email, okay? You can send me email a little closer to the midterm because I'll announce it again for people who have conflicts. But since it's an out-of-class exam, you need to send me email if you have a conflict. I'll get all the constraints from people who have conflicts and try to schedule an alternate time if there's enough people with conflicts. But 7:00 to 8:30 is when you need to know about the midterm. And to make up for the fact that we have an out-of-class midterm, I actually give you sort of a belated free day, which is the Friday of the week of the midterm, we don't have class to make up for the fact that we made you come to the midterm outside of class. But the midterm's an hour and a half, and we can't compress time. If we could, we'd have different issues. We can't compress time and fit it into a 50 minute class, which is why it's out of class, but you get a free day for it, all right?

Last but not least, few things about grading. Grading, one of those things as you might be able to tell from this little board over here or something, if I didn't have to do it, I wouldn't do it because honestly, as corny as this sounds, I just believe in the love of learning. Like, I think if you're passionate about something, you just go do it and you learn it. But I'm naïve, and so that's not the way learning always works. So sometimes we actually need grading to make sure that learning takes place.

And so this is how your grade breaks down: Forty-five percent of your grade is on the programming assignments, okay? Fifteen percent is the midterm, which we'll just call the mid because we like to abbreviate everything. Thirty percent is the final. It's a three-hour final exam in the regular final time slot for this class.

If you think or are under the delusion that you should take two classes at the same time, that's a bad idea because their final exams are at the same time, okay? So you should not take two classes as the same time because our final exam is scheduled for — I believe it's December 13, which is a Thursday, 12:15 to 3:15. That's the regular final exam slot for this class. And any other class at the same time will conflict with that slot. Thirty percent of your grade is the final.

And that, if you add it all up, it's not just that I'm bad with math. It's because 10 percent of your grade is actually participation. And this is things like did you go to your interactive grading sessions? Did you regularly attend section? Did you participate in section? Did you participate in class, right?

And so, in order to help you participate in class, there's a little incentive to participate in class, which is sugar in the afternoon. So someone raise their hand. All right. Yeah, sometimes I'm not a good shot. And this will tell you, if you're sitting in the back of the room, I can't throw a Kit Kat back there because they're a little too light. Oh, yeah, sorry. If you sit in the back of the room, the roof prevents me from actually being able to hit you. So if you want the food, come up. But if you ask questions in class, hey, that's a good time. It's just a little way to be able to reward you for actually participating in class or to keep your blood sugar up if you need it, all right?

So that's participation. It's 10 percent of your grade, and as a matter of fact, at the end of the quarter, I ask every one of your section leaders to actually tell me how much you participated in class, and some of them just say, "Oh, this person was wonderful. They came every time. They participated. It's just a great thing." And that helps your grade out a lot, okay? Now, the final thing, and as you can kind of tell, most of the time, I'm not the most serious person in the world. I just like to have fun with things, and I think it's important for you to have fun with things. There is just one place where I get real serious, and it's one place where Stanford gets real serious. Anyone wanna guess what that is? Plagiarism and the honor code. As a matter of fact, that's what we call a social. So we had someone down here who got it and then a whole bunch of people who I don't know, so we just spray. All right.

So the honor code, in terms of the honor code, the question comes up is what is the honor code all about, and how does that affect working in groups and computer science, etc.? Does that mean we shouldn't talk to each other? No. The answer to all those is no, okay? If you look at Handout No. 4, which is all about the honor code, we encourage you to talk to each other. We encourage you to talk about concepts in the class, talk about different strategies to problems, to think about the ways that you could potentially approach some problem or the way different control constructs when we eventually get to them work in the class. And discussion is perfectly fine, especially among the course staff, but also amongst yourselves. That's a great thing.

So where do we draw the line? And we try to make a bright line for where you've crossed the line for the honor code, which is don't share code, plain and simple, in any respect, okay? Don't give a file to someone else that's got your code in it. Don't get code from someone else. Don't look at someone else's printout. Don't give them a printout.

If you have two people who are sitting looking at the same screen together, that code can't belong to both of you. It belongs to one of you. I don't know which one, but it becomes an honor code violation. So you shouldn't both — two people shouldn't be staring at the monitor together. If it ever gets to the point where you're looking at someone else's code, that's where you're gonna reach an issue, okay? Discuss as much as you want. That's great. Write your own code. That's all we care about.

And you're, like, "Well, what is code, Mehran? What does that word mean?" Code is geek speak for your program, so when you program, the program that you write is what we affectionately refer to as code. And the idea of programming is what we refer to as coding, strangely enough. Computer scientists need to make everything more complicated than it really is so we can get people under the illusion that they should pay us lots of money to do what we do. I mean, you're, like, "Oh, I just write programs." And they're, like, "Oh, yeah, I should pay you half." And you're, like, "No, no, no. I write code." And they're, like, "Oh, yeah." Suddenly, it's much more impressive. So don't share code.

The other thing is if you talk to other people, like if you have a study group to talk about solution approaches or you go, let's say, talk to the TA or your section leader to how you should approach a problem, and they give you a lot of hints as to how to do it, cite collaboration. So cite and collaboration gets you out of trouble. Any collaboration that you cite you cannot be held responsible for under the honor code. You can actually copy someone else's program and say, "I copied this program from Mary Smith." And I'll look at that and say, "They cited it," and it will warm the cockles of my heart. And Mary Smith will get full credit, and you'll get a zero because you copied your program from Mary Smith, but it's not an honor code violation because you cited the work, okay? So the bottom line is keep yourself safe and cite your collaborations. And I guarantee you most of the time, you'll be just fine.

Now, you might wonder why do I make such a big deal about this. And the reason I make a big deal about this is for a while, thankfully it's not true anymore, but for a while, the computer science department actually had more honor code violations than the rest of the university combined. Take everything else in the university, put them all together, they were like over here. And we're, like, we're computer science, which is not a fun distinction to have, let me tell you.

And you might wonder why is that? Is that because computer science people are just mischievous and dishonest? No. It's because it's easier to catch honor code violations in computer science. We have a whole bunch of tools that allow us — then we take all your programs and we run them through this tool, and it compares them not only to everyone else in here, but, like, to everyone from the last, like, X years where X is the large number of people who've ever gone through the classes, right? And it's an extremely good tool from finding where honor code violations happen, from where they don't. And it doesn't find spurious violations.

To be honest, I've never lost an honor code case. When I find an honor code case, it is blatant. And you take it to judicial affairs, and they look at it, and they're, like, yeah, this is blatant. And I take it to the student, and every student I've ever confronted them with never said, "No, no, no. I didn't cheat." They said, "You caught me," okay? So it's blatant.

It's not like, oh, there's some little line in it, "Oh, am I gonna need to worry about an honor code violation?" Remember those rules, you have nothing to worry about in this class. It's people who go and, like, fish out printouts from the recycle bins and copy other people's code that are the people we catch, right? It's blatant cheating that we catch. But we catch it. We catch it all the time. So I hope, I pray it doesn't happen in this class.

But the reason I make a big deal about it is historically if I look at the evidence, it happens and we catch it. And when we catch it, we're required by the university to prosecute. And I feel bad because usually it's someone who just made a bad call, like, they were up way too late the night before working on something else, and they're not thinking straight. And rather than just taking a late day or turning in their assignment late and getting a slight penalty on it beyond their two free late days, they decide to cheat. And that's just always the wrong call, okay? So you just don't wanna put yourself in that situation. So I get real serious about it for a moment, and hopefully it won't be an issue and we can just kind of go on, okay?

So with that said, that's a whole bunch of logistical stuff. Any questions about the logistics of this class or anything I just talked about? Uh huh? 

Student: You had briefly mentioned the late penalty.

Instructor (Mehran Sahami): Oh, the late penalty, good point. So remember our little bucket scale. If you go beyond your two free late days, every day you turn in an assignment late beyond those, it drops down one bucket. So let's say you already used your two free late days on Assignment No. 1. And on Assignment No. 2, you turned in something one day late and you would have gotten a check normally, it becomes a check minus. So that's how it is. It's one bucket per late day beyond your two free ones. Uh huh?

Student: Are the sections first come, first served?

Instructor (Mehran Sahami): Yeah, the sign-ups, well, they take into consideration your preference, but part of your preference is to do the match is first come, first served. So you wanna sign up early. Oh, thanks for your honesty. As a matter of fact, I dig honesty, all right? Any other questions? It's just honesty's cool. Uh huh?

Student: How much time should we plan on studying [inaudible]?

Instructor (Mehran Sahami): Oh, good question. How much time should you plan? And this is something that I say for classes in general at Stanford, which is not always true, which is take the number of units that a class is, multiply it by three. That's how many hours you'll spend per week in that class, total, on average. So what that means is in 106A, a 5 unit class, you multiply by 3, you get 15. Five of those hours are roughly spent between class, section, interactive grading, other stuff. That means on average about ten hours a week will be spent on your assignments in this class. Again, that's an average.

Sometimes when I go to computer science conferences, I sit there and joke around with plans. And we're, like, "Oh, how long did your assignments take?" And I say, "Oh, on average, ten hours." And what I really mean when I say on average 10 hours is they take between 3 and 45, okay? It's a large variance event, right? Ten is the average. Some people take a really long time. Some people get through it really quickly, but that's about the average you can plan for. Uh huh? Another question?

Student: [Inaudible] late days [inaudible] class days?

Instructor (Mehran Sahami): Yeah, all late days are class days, so the free ones — the halfway mark's really my reach. That's about it. All right.

So I do wanna give you your very beginning of an introduction to programming before we sort of break for the day. How are we doing on time? And so in order to kind of see this, there's a few things that we wanna keep in mind.

Actually, let me show you a little picture, okay? Sometimes when we talk about writing programs, we talk about debugging programs, right? How many people ever heard the term debugging or bugs in programs? A bug in a program is an error in a program, so sometimes when you hear us say, "Oh, come see," like, your section leader to help debug or see the helpers in LaIR.

That's another thing. In the Tresidder computer cluster is the LaIR. It's a computer cluster that we have helpers there to help you get through this class. What is it? Sunday through Thursday, every week, from around 2:00 in the afternoon 'til midnight every day, okay, to help you get through the class. So that's a good place if, you know, you can work in your dorm room certainly, but if you also want help, go to the Tresidder computer cluster, and there will be helpers there. There's a little queue you sign up for to get help, and that's a great place, and it's all explained in Handout No. 1, but that's just something to keep in mind.

Where the term debugging comes from, it turns out this is an apocryphal story, but I'll tell you anyway. Back in the days of yore, in 1945 actually, there was a computer called the Mark II at Harvard. And there was a woman named Grace Murray Hopper. Anyone ever heard of Grace Murray Hopper? A few folks. She was actually the first woman who was an admiral in the navy. And she was also one of the very early pioneers of computer programming. She did a lot of computer programming when she was actually a captain, and she was stationed at Harvard as part of some sort of navy thing. I don't know why, but that's what happened.

And they had this huge computer there, and they were noticing the computer was on the fritz, and they couldn't understand what was wrong. And this is one of these big old machines in the days of yore that has vacuum tubes and stuff inside it. So they walked inside the computer, right, because then you could actually open it up and walk inside your computer.

And they saw this, and I don't know if you can see that, but that's a moth. It was a moth that had sort of given its life to be immortalized because it had actually shorted out across two relays in the computer and was causing these sort of errors to happen on the fritz. And so they took the bug out, and once they actually plucked this little charred bug out of there, the computer started working fine again, and she taped it in her log book.

And this log book's actually preserved in the Smithsonian Institution now, which is where all this comes from. Here's all the standard disclaimer information: "Image used under fair use for education purposes. Use of this image is exempt from Creative Commons and other licenses," just so you know. Now the lawyers are happy. But this is where we think of sort of the modern term debugging actually came from.

Now, it turns out the actual story is that the term debugging came from the 1800s, in the late 1800s from mechanical devices. People actually referred to debugging as fixing mechanical devices. But this is kind of the apocryphal story for how it comes up in computer science.

Now, with that said, what is the platform in which you're gonna sort of do your first debugging or your first work on? We talked about Java, but in fact in this class, we're not gonna start with Java. We're gonna start with something even sort of simpler than Java because as I mentioned, sometimes what happens in computer science is people learn all the features of some language. And they think just knowing the language makes them a good software engineer. And they get so worried about all the features of the language that they don't kind of think about the big picture.

And so there was a guy named Rich Pattis, who oddly enough was actually a grad student at the time at Stanford, and he said, "You know what? If we're gonna teach computer science, when we first start out, why don't we have people not worry about all of the different commands of the language and all the different things they can do? Let's start with something really simple so you can learn all the commands real quick. And then you've mastered everything there is to master about that language, and you can focus on the software engineering concepts." And it turns out to be a brilliant idea, which has actually been adopted by a bunch of people.

And so Rich, who's a wonderfully friendly guy — sometime if we get him to come to Stanford, I'll introduce you; he's just very nice — came up with this thing called Karel the Robot. And the term, "Karel" actually comes from Karel Capek. Anyone know who he is? Oh, free candy. Uh huh?

Student: He coined the term, "robot."

Instructor (Mehran Sahami): He coined the term, "robot." He was a Czech playwright who actually wrote a play called, "RUR," which was about robots. And the word robot actually comes from a Czech word, the Czech word for work. And so the robot is named after Karel. And some people say Karl, which is kind of actually closer to I believe if — I don't know if there's anyone who speaks Czech in the room — but closer to the actual pronunciation. But we say Karel these days because it's kind of like gender neutral, okay?

And so Karel the Robot is basically this robot that lives in a really simple world. And so I'll show you all that you can meet Karel the Robot. He's friendly; he's fun. I'll show you Karel the Robot. So we gotta get Karel running. He's at the factory. He's getting souped up. We're energizing Karel. You gotta add some color to it. Otherwise — all right. We're begging for him. Come on, Karel. There he is. Oh, yeah. That's Karel the Robot. He looks like one of the old Macintoshes if you remember the original Macintoshes that look like a lunch pail, except he's got legs. One sticks out his back. That's just the way it is.

And the way Karel works is he lives in a grid. To you, it may not be exciting, but to Karel, it's way exciting. So Karel lives in this little grid, and the way the grid works is there are streets and avenues in the grid. Streets run horizontally, so this is First Street, Second Street, Third Street. And then over here, we have avenues, First Avenue, Second Avenue, Third Avenue, Fourth Avenue, Fifth Avenue. It's kind of like Karel lives in Manhattan if you wanna think about it that way, okay? So Karel always is on one of these corners. So right now, he's at the corner of First Street and First Avenue, or we just refer to it as 1 1 if you wanna think about sort of Cartesian coordinates, right? But just think of them as streets and avenues. That's where Karel lives. And Karel can move around in this world. There's a bunch of things that Karel can do. He can take steps forward. He can turn around to face different directions, and he can sense certain things about his world. So there's some things that exist in Karel's world, okay? Things like walls that Karel cannot move through, right, so his world has walls all around it that he can't go through, so he can't fall off the end of the world. And there's other walls like this one if Karel were over here, he can't step through that wall.

There's also something referred to as beepers in Karel's world. And what a beeper is, is it's like a big diamond, okay? But what a beeper really is, is basically just some marker that he puts in the world. You can think of a beeper like a piece of candy. And Karel just goes around, like, putting pieces of candy in the world. As a matter of fact, not only does he put pieces of candy in the world, he carries around a whole bag of candy.

So he has a beeper bag with him, and sometimes that bag has a whole bunch of beepers in it; sometimes it only has one beeper; sometimes, it's sad Karel, and he has no beepers. But he's still got the bag. There just don't happen to be any beepers in it. So he can potentially, if he come across a beeper in his world, he can pick it up and put it in his bag, or he can take, if he's got beepers in his bag, he can take them out of his bag and put them places in the world. And corners in the world can have either zero — if they have no beepers, they just appear like a little dot — or one or more beepers on them that Karel can potentially pick up, okay?

So any questions about beepers or Karel having a little bag of beepers? And that's it. That's Karel. That's his world. His world, we can make it larger if we want. We can put in walls in different places. We can put beepers in different places. We can have Karel be in a different place.

But starting next time, what you're gonna realize is with this extremely simple world, there's actually some complicated things you can do. And after about a week — so this first week, we're gonna focus on Karel — you'll notice that Karel is actually a very nice, gentle introduction into Java. And a lot of the concepts that we learn, sort of software engineering concepts using Karel, will translate over to the Java world, okay? So any questions about Karel or any of the other logistics that you've actually heard about in the class?

Alrighty then. Welcome to 106A. I'll see you on Wednesday.

## CS106A-Programming-Methodology-Lecture0201

Topics: Handout Information, Section Sign-up, Karel Commands, An Algorithm vs Program, Syntax of a Karel Program, Running a Karel Program, Creating Methods, SuperKarel, A for Loop, A While Loop, Karel Conditions, If Statement, Putting it All Together.

1『整节课是围绕 Karel 这个小软件做演示的，目前觉得研读的话性价比太低，先跳过。（2021-04-25）』

Instructor (Mehran Sahami): Alrighty, welcome back to CS106A. If you're stuck in the back, just come on down, have a seat. Originally, I thought maybe we would have slightly fewer people today than last time, but that appears not to be the case. So while we're waiting, everyone loves babies, so I decided to put – that's Karel, the Robot, the early days.

No, this actually – my son, and yeah, I know. He's a little bit older now but, like, he's got these little robot pajamas and he runs around all the time. So I'm like, oh, it's Karel, The Robot, and my wife looks at me like, it's your son. But that's a whole different issue.

Anyway, a few administrative announcements before we start. A couple things, there are four more handouts today, just because we like consistency. Four last time, there's four this time. They're all in the back. If you didn't already pick them up, you can pick them up after class, but they have all the information about downloading Eclipse, which is the environment that you're going to use for programming in this class, both for Karel and for Java.

There is also a special handout in there just on using Karel, so it talks about how Karel works in the Eclipse environment, and so you can get all set up with that. And so after today, you'll know how Karel works and you'll have the environment to use it. So surprisingly enough, you also get your first assignment today, which is actually in two parts.

So the assignment, the real assignment is the programming part, which is due on Friday of next week, October 5th. There is also an email part to it, where the email part is, we ask all of you kind folks to send an email to Ben, the head TA, myself, and also your section leader. So Ben and I get a whole bunch of mail, your section leader will hopefully get a little bit less mail.

But you won't actually know your section leader until after you go to your first section next week, which is why that part of the assignment is not actually due until basically one minute before midnight on Sunday. So I didn't make it midnight, just because then there's always confusion, midnight, which night? So 11:59 p.m. on Sunday, October 7th is when you should send that email.

That's not really the critical part of the assignment. The critical part of the assignment is the programming problems, which are actually all due in class on Friday. Okay, and then there's one last assignment, or one last handout, which is about how you actually submit your work in this class. You'll submit your work both electronically and in hard copy. The electronic copy, so that your section leader can run it and verify it. The hard copy is so that they can actually write comments on it, and then you'll do interactive grading with them as well. A couple other quick announcements. The website, in case you weren't here on Monday and you don't know what handouts I'm talking about, and you don't know where to get them, go to the class website, cs106A.stanford.edu. There will be electronic copies in PDF format of all the handouts there, so you can get caught up if today is your first day.

You also need to sign up for a section. As we mentioned last time, section signups start tomorrow, 5:00 p.m. Sign up early if you want to have the most flexibility in terms of time, because look around, there's a whole bunch of people in this class. It's going to fill up quickly. So if you have constraints, sign up quickly, and the place you sign up is CS 198, not CS 106A, but CS198.stanford.edu/section. The 198 folks are the folks who lovingly run all of the sections and coordinate the whole program.

Last, but not least, just a word on the readings that I didn't mention last time. On the syllabus, you'll notice that pretty much for every day, or most days in the quarter, there is some sort of reading associated with it. That's the reading assignment that you should have done by that day's lecture, because that's what we will cover in that day's lecture.

So for today it should be the first three chapters of the Karel book, or the course reader. And if you're like, oh my God, I'm already three chapters behind, don't worry, it's like 20 pages or something. It's pretty lightweight, but you should do the readings by that time in class. So any questions about anything we covered last time, which is mostly logistics, or any of the sort of administrivia?

All righty, then let's get started on the real content. So you remember from the time before, we talked a little bit about Karel, the Robot, and here is Karel in that world that I showed you before. And there were avenues that run north-south, and streets that run east-west, and little beepers in the world. And Karen can face different directions, and there's walls.

And so now, we want to think about how do we actually program Karel. How do we get this little guy to do something interesting in the world? Okay, and it turns out there are four commands that Karel understands, okay, and those are pretty straightforward.

So here they are. You're going to get all of Karel's vocabulary in, like, one minute. There's a command called move, and move basically moves Karel one spot forward in the direction he's facing. So if he's on corner one, one, and he moves one spot forward, he's facing east. So he'll move over to two, one, basically. So one corner forward in the direction he's facing.

Karel also started being a good democrat, knows how to turn left. So he turns left. This is a lower case T, this is an upper case L. So turning left changes his direction by 90 degrees in the left hand of whichever way he's facing. So if he's facing east now, and he turns left, he will be facing north. And then he can turn left again and he'll be facing west.

Okay, now, question? 

Student: [Inaudible]?

Instructor (Mehran Sahami): There is no space here. These are all one word. Good question, and I love it when you make it easy. All right, so besides turning left, there's also B-person Karel's world, and if he couldn't do anything with beepers, they wouldn't be interesting. So he can pick up beepers, which interestingly enough is called pickBeeper, again lower case P, upper case B, all one word, and there is putBeeper.

And what these do is pickBeeper, if Karel happens to be on a corner that has a Beeper on it, he picks up that Beeper, and stuffs it in his Beeper bag, in which case the count in his Beeper bag goes up by one. Or if it's infinite, it remains infinite, because he's got a real big Beeper bag, and sometimes he can infinitely many Beepers in there. It's just – we can talk about the infinity of Karel's Beeper bags some other time, but if you're interested, it's fascinating.

And he can also putBeeper, which means he can go to a corner and be like, "Hey, I'm just feeling happy. I'm going to put a Beeper down, say, on that corner right there." Except you can't throw the beepers, right. Karel's kind of limited. He's got, you know, if you look at him he's got no arms. He's got legs. No arms, so basically all he can do is he sort of like drops the little Beeper where he's at. So this puts it on the corner that he's at.

And these things are what we refer to as methods. Okay, methods are basically some instruction that we can call, okay, or use, like move, or turn left, or pickBeeper, or putBeeper. And what we say is Karel responds to this method. What we're doing is we're invoking, or we're calling a particular method on Karel, and he takes some action, which is basically what that method specifies to do.

Okay, so if we kind of think about this program, or if we kind of think about this world, maybe we want Karel to do something. So here's the initial configuration of the world. Maybe what we want Karel to do is pick up this beeper, drop it off at this corner, and end up at this corner facing to the east. And you can think about how we might do that with some of the instructions we have.

So what we want the final configuration of the world to look like, and I'll just put Karel at blinding speed. You can actually control Karel's speed here with this little slider. So I'm going to just show you the end configuration by running Karel so fast you can't even see it. It's just – he's blindingly fast. He's just that good, okay.

And so that's what we want to get to. Notice he's still facing east, but he's picked up that beeper that was on that corner at two, one, and moved it over to the corner at four, two. Okay, and so how might we do this? Right, so one thing we could consider is, what was the initial state of the world again?

So I'm just going to run this program again, and here I have a clip set up, which is your handout number five explains how to get this. But if I want to run a program, there is these two little running person icons, or as you might notice, we even have our own menu in Eclipse, because Stanford's just that much fun, okay.

So under the Stanford menu, we have these two options for run. Import project is explained in the handout, is what you'll use. We'll give you some initial stuff for Karel that you'll start with, and you'll use import project to get it into Eclipse. But once it's there, we can run it, and so what we're going to do is say run this particular Karel program. So it's get – and we'll go through all this – it's get and go.

And this is our first Karel program that we want to run, and it's sort of, here's the initial world again, all big and happy. So I'm going to shrink this down a little bit, so we can see it over here on the side, while we think about what commands Karel would need to execute to kind of get to that final state we just talked about.

And over here, happily enough, let me resize a little bit, is our first file, which is empty right now, that we're going to write our first Karel program. So what commands might we consider Karel actually doing from the list you have here, to sort of affect what we want to happen in the world?

Student: [Inaudible].

Instructor (Mehran Sahami): Yeah, so we want to move. Okay, and then what do we want to do?

Student: [Inaudible].

Instructor (Mehran Sahami):PickBeeper, then move. Notice at that point we could have actually done something else. This is part of the art of programming. There's actually many ways to solve the problem. We're just going to happen to pick one. So we've moved. We've picked the beeper. We've moved again, and now what do we do?

Student: Go to the left.

Instructor (Mehran Sahami): Turn left. What happens if we turn left?

Student: [Inaudible].

Instructor (Mehran Sahami):Right, then what are we going to do?

Student: Move.

Instructor (Mehran Sahami):Move. And now what do we want?

Student: [Inaudible]. 

Instructor (Mehran Sahami): Yeah, conceptually what we'd like to do is turn right, right? At this point, Karel's like, "No, man. I'm just, you know, I'm left wing. What can I do? I turn left. That's what I do." And you kind of think about it, and you say, "That's all right, because really the world is just one big spectrum, and if you go around far enough to one side, you end up on the other." So if we make you turn left three times, that's equivalent to essentially turning 90 degrees to the right.

So here, we turn left, turn left, and turn left. All right, now what do we do?

Student: Move.

Instructor (Mehran Sahami): Move. So we sort of go up the step. PutBeeper and move to the last spot. Now, at this point we'd like to think, oh good times, we can just run this and it's a Karel program, and life is happy. In fact, this is not a valid Karel program. What this is, is an algorithm.

This is a recipe for doing something, and we'll talk in a lot more detail about different algorithms on Friday. But the way you can think of distinguishing between an algorithm and a program is an algorithm is essentially the recipe for doing something. The program is something that is valid syntactically according to the rules of the language.

And so Karel actually has some specific rules to its language that we have to apply to these statements to make them look a little bit different, so they follow the valid syntax of Karel. And that's what we're going to do now. We're just going to kind of go through this step by step, okay.

So one of the things we'd like to be able to do is, first of all, we want these to be valid commands. Right now, they're not valid commands. To turn a command into a valid command, or what we would refer to as a method call in Karel, after the name of the command we put an open paren and a close paren, and then a semicolon.

Okay, so move, open paren, close paren, semicolon is actually the valid move command, or move method invocation for Karel, and we do that for all these things. So to save a little bit of time, I'm just going to copy this and just go through and paste until the cows come home. Let's do a little paste there. Oh, it didn't copy. All right, let's try that again. We do a little paste, a little paste.

So we're going to go and turn all of these into valid Karel commands. Okay, so now you might think, okay they're all valid Karel commands. Are we ready to actually run this Karel program? And it turns out no, we're not yet ready to run – this is not yet a valid Karel program.

What makes it a valid Karel program is we need a few more things. One of those things is, we need to tell Karel where to start running. And you look at this and you're like, what does that mean? Like, doesn't he just start at the top? Does Karel start somewhere in the middle? No, what it really means is that we're going to do is encapsulate a set of instructions inside something that tells Karel, hey, this is what you're going to execute. And the way we do that is we create something called a run method, and the syntax for that looks a little bit archaic, but basically it says, public, void, run, open paren, close paren, and then we put a brace. And that first brace says everything that you will now see until the closing brace is all part of what we refer to as the body for this thing called run.

So we come down here to the bottom and we put a closing brace, and everything between the open brace and the close brace is referred to the body, or what's actually executed when we do a run. Okay, so get to know where the brace keys on your keyboard are. They will come in very hand in programming, because you'll use them all the time.

One thing we also do with this is we're going to actually insert some tabs to make it easier for the human to read this program. Okay, so when we put in tabs, suddenly everything that's inside the body of run gets tabbed in, and when I look at it visually, it's much more appealing. I can just tell all the things that are actually inside run.

Okay, so we tab those in there and now we have the body of run is inside the braces. What we've actually done is created a new method. Well, run is here, is we defined for Karel a new method called run. And run is a very special method because that's where Karel begins running.

What he says is when he starts up, he comes into the world, he's like a brand new baby. He's like, "Hey, I'm here. I'm in the world. What do I do?" And he's preprogrammed to go find the method called run and start executing from the beginning of it. So he does executed in a top down manner, but he needs to have this run thing.

And so you might see them say, "All right, we're ready to go. Fire up Karel, right. I'm slipping a shrimp on the barbie." I'm sitting here barbequing while Karel's going and moving the beeper. It's like, no, we're not quite there yet. You're like, oh, what else do we need?

Okay, so one thing that we need is we need to take Karel. Karel is actually implemented in Java. If you've done some Java programming before, some of the syntax already looks familiar to you. If you haven't done any Java before, it's perfectly fine. You don't need to know anything about Java. What you do need to know about Karel is that Karel is defined in what we refer to as a class.

Karel is sort of a class of robot. There's kind of like the Karel 1000, kind of comes of the assembly line, and what we'd like to do is take those Karel 1000s and sort of mold them into our own version, which does some set of instructions that we'd like it to do. So in order to sort of say, "I want to create my own version of Karel," what we do is we create a class, and again we say public, and we say class now, instead of void.

So far, all you need to worry about, the stuff that's in purple, public void, and public class, is just kind of the standard syntax of Karel. And later on, all of this stuff will make sense what it actually means, but right now just think of it as standard syntax, and just put it there, and life is good.

Public class, we now need to give this Karel program, in some sense, a name, and what we're going to name it, for lack of any better name, is we could call it our Karel program, because we did it together. It's kind of a collective process. So our Karel program, and at this point we're not done.

We need to actually say – you might have noticed after I type this why suddenly all this red showed up on the side of the editor. And it's like, oh, bad times, dogs and cats sleeping together, like what's going to happen? Well, what happens is we're creating our Karel program and it says, "Okay, you're creating Karel program," but it doesn't even know anything about the basic Karel 1000.

It needs to somehow know that this Karel program is creating a version of the Karel 1000. We'll call it the Karel 1001, and the way we specify this is we say that our Karel program extends Karel, which is sort of the basic Karel that actually exists and has these predefined instructions in it.

So we say public Karel, our Karel program extends Karel, and now we need to, again, encompass what our Karel, our particular class Karel is going to be running. So we put this inside braces and we say, "Yeah, this whole run thing is part of our Karel program." So we put another brace at the end, and to make it more readable, we go through one more time. Don't want to put a tab there, and tab everything so that it's nicely readable by a person.

Okay, so all this stuff now gets tabbed over one more spot, and even this brace over here gets tabbed one more spot. So now you can see, everything here is part of the run method, because it's nicely tabbed in. We can tell that, and all this stuff here is all part of the body of run, and all of it's encapsulated inside our Karel program.

Student: [Inaudible]?

Instructor (Mehran Sahami): Why is there a space, you mean like down here?]

Student: Yeah.

Instructor (Mehran Sahami):Just for readability. We don't actually need it. There doesn't need to be a space, but that's a good question. Oh, nice bank. I like that. Feel free to bank. If someone – you're on the rebound and I'll set you up for the rebound, just because you were the first one to do it. All right, so, and you might say, "Okay, now we've got our Karel program. We've got our run method. Are we ready for Karel?"

Okay, and you think we're ready for Karel, and someone's calling, saying, "You're ready for Karel. Do it." What I would actually encourage you to do is take a moment and turn off your cell phones, unless your doctor. I actually would tell this to my students all the time.

I had one student who was a doctor once, and he says, "Actually, your class is when I'm on call, and if my phone rings, that means, like, someone's dying. So can I keep it on?" And I was like, hmm, yeah, okay. So he got an exception, but other than that, I'd encourage you to turn your cell phones, unless you have a really cool ring. Then you can leave it on.

All right, so at this point, you might say, "Oh, we're ready to run it," but even now, we're not ready to run it. And the reason why we're not ready to run it is, where does this Karel thing come from to begin with, right? Someone, somewhere had to say, "Hey, I'm going to build the original version of Karel that you're now extending."

And that actually comes from a place called Stanford.Karel. So what we do is we add a line called import, Stanford.Karel.*, and we put a little semicolon at the end of it. And what this tells us is, hey, go and get everything that Stanford's previously defined about Karel.

And when we get to Java, this'll become much more clear, but for right now, all you can think of that import's meaning is, go get me all the standard Karel stuff that Stanford's already done for me. And that defines this thing called Karel, which now we're extending in our Karel program. Uh huh?

Student: What is the semicolon for?

Instructor (Mehran Sahami): The semicolons always come at the end of the line and Karel's syntax, what they mean is this is the end of one statement. So at the end of the import, for example, that says import the stuff, that's the end of a statement, or for move, or pickBeeper, or turn left, that's the end of a statement. So we put a semicolon. Uh huh?

Student: Do the stars mean anything?

Instructor (Mehran Sahami): Do stars mean anything? Yeah, that star at the end of Stanford.Karel.* is actually important, and in a couple weeks you'll understand why. For right now, it just means get everything associated with Stanford.Karel. Uh huh?

Student: So then, is the run program [inaudible]?

Instructor (Mehran Sahami): It's all part of run. So when Karel starts up, and you'll see that in just a second, we start – we go to run and we just start executing the statements from run. So let's actually run this and see what happens, and I'll take a couple more questions in a second.

So we go up to our little run icon here. Actually, before we do that, let me cancel this, because we already have a running program over here. So let's quit out of the running program and come here, and say run. And sometimes if you actually happen to write multiple Karel programs, and you hit the run, then this guy sort of looks like he's running with smoke all around him, which means he's running really fast. That means run the last program I was running.

The guy without smoke around him means, run one of the programs that I tell you to run, and it might give you a list if you have multiple programs. Here we're going to pick first Karel program, okay. So yes, we'll go ahead and save the resource because we forgot to save our file, and here is life.

And we'll run it slowly, and so we start the program, and there goes Karel. Woo-hoo! Congratulations. You are now all computer programs. Okay, because you got Karel to do what you wanted to do, and you're like, "Oh, that's so good. Let's do it again." And so you're like, "Yeah, let me start the program again." Wah-wah-wah, thanks for playing.

What happened? It tried to execute the same program again, but the world was in a different state, right? Karel was facing that wall, and the first thing we said is, "Hey, Karel, move." And he's like, "Okay." He's a little happy, scrappy robot. He doesn't know anything about the world, and he just, wham, into the wall. Thanks for playing. Dead Karel.

All right, no, because Karel's blocked, okay, and you get this little bug on top of Karel. It's like Alfred Hitchcock, the birds, he's just being, like, harangued by this little bug. But what that means is Karel tried to do something in the world that the world would not allow him to do, and this is what happens if you try to walk through a wall, or try to pick up a beeper from a corner where it doesn't exist, or you try to put down a beeper and your beeper bag happens to be empty, that's the kind of error you'll get.

So if you want to start this program again, you need to load world – and we happen to have first Karel program, you need to reload your world and then you can start it again from that point. Okay, so any questions about our first Karel program? Uh huh?

Student: [Inaudible]?

Instructor (Mehran Sahami): Yeah, he's moving basically from one grid point to the next grind point. So he just moves one step at a time. Uh huh?

Student:Is Karel case sensitive?

Instructor (Mehran Sahami): Karel is case sensitive, yes. Everything you type will be case sensitive. My throwing is case sensitive as well, and evidently, that was the wrong case. All right, so something else we'd like to be able to do with Karel, and a few people already pointed out is, "Hey, we created this thing called run. That's kind of cool. Can I create other stuff?" And as a matter of fact, you can, because that's just how snazzy Karel is. And one thing, you might look at this and be like, "Ooh, ooh, ooh, I know what I want to create." What would you want to create if you could create a new command?

Student: Turn right.

Instructor (Mehran Sahami): Turn right. Right? That's a social, right? Everyone wants to turn right. All right, except the person who actually said, "Turn right." So what we can do is we can have a similar syntax that allows us to create new methods in Karel, like the run method actually is the place where Karel will always start. But we can create new methods that we could use, and so maybe we want to create a turn right.

So we could say void, sorry, here we'd say private void. Voice – sometimes typing is bad, especially when your hands are a little chalky. So run – you'll notice run is always public void run. For all the other commands that we're going to do as far as Karel's concerned, we're going to use private void, and the name of the command.

So we'll call this turn right, and this command will have a body, and what is the body of the turn right command going to be?

Student: Turn left.

Instructor (Mehran Sahami): Turn left three times. So I'm just going to copy from here and paste into – and the indenting even works out right. Rock on, right? And what I've now done – I'll go ahead and save this – is I've created a new command for Karel called turn right. So anywhere else in my program, I can now say, "Turn right," like here are these three turn lefts. I can replace them. Let me just get rid of them, and I'll replace them with a turn right, and I'll appropriately indent that.

And what that means is, as you're executing the program, you move, you pickBeeper, you move, you turn left, you move. When you get to turn right, it says, "Let me pause where I saw that turn right. I will go to the turn right method body and run all the instructions that are in that body, and then I will return back to where I left off.

So this program is exactly equivalent to the program we wrote before, now in terms of something called turn right, and just to prove that to you, we'll go ahead and run, and there it is, Karel does the equivalent of turn right and life is good. Okay, so we've created a new command called turn right. Question?

Student: [Inaudible]?

Instructor (Mehran Sahami): The location's not important. You can put it anywhere. I like to put it at the end, because that's convention in the book, but you can put it anywhere. Uh huh?

Student: [Inaudible]? 

Instructor (Mehran Sahami): Why is run always public? Because that's where things start, and for Karel to know where it is, like private's all the stuff you're sort of like, eh, I'm keeping it to myself. But Karel's like – he's, like, looking around. He's like, "Where do I run? What do I run? And so you got to say, "Oh, it's public. It's available to the whole world." And in a couple weeks when we get into Java, you'll see public and private rear their ugly heads again and it'll all be clear.

Uh huh?

Student: [Inaudible]?

Instructor (Mehran Sahami): Pardon?

Student: If you made that a public [inaudible]?

Instructor (Mehran Sahami):It would still run. It would be fine. It's just good programming style. See, there's all these things that we kind of will eventually get to, but we got to start somewhere. So we sort of start right in the middle and we're going to build up from there, and eventually we'll go back and fill in some of the pieces underneath.

Uh huh?

Student: Do you have to [inaudible]?

Instructor (Mehran Sahami): Run is where – has to be called run. That's where Karel always knows where to start, but everything else could be something else. Like, instead of turn right, I don't know, what's the French word for turn right, or the French two words for turn right? Anyone speak French?

Student: [Inaudible].

Instructor (Mehran Sahami): Exactly. We could have called it that if we wanted to, and then rather then turn right we would use that, and it would be fine. So all the other things besides run, we can name them whatever we want as long as we're consistent throughout.

All right, so we could also – you might say something else might be kind of fun to do is to have a command called turn around, for example, which turns Karel around 90 degrees. So we'll just do a little copy and paste magic and have turn around here. We might not actually use it in this program, but just to have, and turn around is actually just two turn lefts.

It turns Karel around, and if you really wanted to do it, you could do it as two turn rights, but that's kind of six turn lefts, and that's not really a good idea. Okay, so because turn right and turn around are such common things to do, we actually have a souped up version of Karel. It's sort of like Karel with the training wheels taken off, and he's bad, and he's buff, and he knows everything Karel knows, all four methods, plus two more, which is turn right and turn around built in. And that's super Karel.

So if we get rid of these and we say, "Hey, our Karel program, instead of extending Karel, is going to extend the super Karel model." Okay, oh, I know, it's dangerous, but it's okay. Super Karel, we've gotten rid of the turn right definition and the turn around definition, but if we run this now, start the program, Karel actually will do the right thing.

All right, let me quit out of this, unless my computer decides to freeze, and sometimes it decides to freeze, and that would be bad. All right, so at this point you're Karel programmers. You're rocking. You know all the Karel's methods. That's all he knows, at least for the time being, and you know how to actually make new commands by creating new definitions that have a body and the syntax around them to create new commands.

All right, so now what we're going to do is I want to ask you a philosophical question. I know, I guess you're like, this is a computer science class, why do we have to do philosophy in here? Because it's good for you, and the philosophical question is what is the downfall of the modern college student? Anyone know? You're like, what does that mean? You're like, I haven't fallen down yet. That's good. Hopefully it won't be that way.

But there is something, probably in your everyday life, that's just sitting there niggling. Uh huh?

Student: Procrastination.

Instructor (Mehran Sahami):Procrastination? It's related to that. What do you do to procrastinate in the morning?

Student: Sleep.

Instructor (Mehran Sahami): Sleep. Oh, sorry, yeah, and how do you prolong that?

Student: [Inaudible].

Instructor (Mehran Sahami): Snooze. And the thing about snooze is, it's amazing how quickly you can do math in the morning. I don't know about you, but my alarm has a nine-minute snooze on it. Why it's nine, I don't know, but it came out of the factory with a nine-minute snooze. And so you're, like, lying there.

I remember when I was a student, like, the dreaded, like, 10:00 a.m. class, 9:00 a.m. class. Heaven forbid you ever have a 9:00 a.m. class, and you're sitting there, and, like, the alarm goes off, and you're like, yeah, not going to brush my teeth today. Snooze. And then you think about it a little bit and nine minutes later, it goes off, and you're like, okay, it must be, like, 8:09 a.m. now. And then the math kicks in. You're like, if I don't take a shower, that's like two more whacks on the snooze bar, snooze, snooze. And now you're up to like 8:27 a.m. You're just doing this all while you're, like, have asleep, right. It's like calculus when you're fully awake, yeah, impossible. Snooze bar, you could have, like, your brain removed in a lobotomy and you could still figure it out.

But what the snooze bar actually gives you is a way of doing something a certain number of times when you want to be able to do it a certain number of times. And so you might say, "Hey, Karel, sometimes rather than just, like, telling you turn, left turn, left turn, left three times, can I just tell you to turn left three times? Is there some way of doing that?"

And in fact, in Karel there is, and it's something called a for-loop, and the syntax for this looks like this, for, just the word for, paren, int I equals zero. And so this might look a little bit strange, and if you've done some programming before, it won't look strange, and if you haven't done any programming, this is just the syntax. Just use it and feel good about it.

This is int I equals zero, semicolon, I is less than the number you want to count up to. So if I want to do something three times, I'd have a three here, but in general this could be any number that you want. Then another semicolon, and then an I followed by a plus and a plus with no spaces, and then a close paren.

And then after all that, you have a brace, an open brace, and there's a close brace down here, and everything that goes here is the body of what we refer to as the for-loop, and that body gets executed however many times you say here. It can be one instruction. It can be more than one instruction. So turn left could actually be defined – or turn right could be defined as for I equals zero, I less than three, I plus, plus, turn left.

And what this will do is it will execute this three times. I could have multiple instructions in here if I want to, and it would execute that whole set sequentially three times, but this is the equivalent of turn right. Okay, question?

Student: [Inaudible]?

Instructor (Mehran Sahami): So the spaces are, sorry, there is a space here. Well, you don't actually need a space there, but there are no spaces in here. So you need to have this space for sure. The rest of these spaces are basically optional, but we like to kind of space them out for it to make sense. You definitely should not have any spaces in the I plus, plus. There's no spaces in there. Uh huh?

Student: Is all of this syntax in the course reader?

Instructor (Mehran Sahami): It's all in the course reader, yeah. Yeah, so you don't need to worry about – if you want to take notes, that's great, but it's all kind of in the course reader if you want to follow along. So you can do something any number of times that you want, right, and it'll just count up. So this could be, like, if you wanted to, you could say, "Hey, turn left six times," and that's still the equivalent of turn right.

Or we can do the equivalent of snooze, which is that. Right, so basically what does snooze do? Nothing. You just sit there, and you spin around a few times, and you're kind of like in the same spot, facing the same direction when you were done. Okay, but anytime you want to do something some number of times, you can actually do it using this for construct.

And this is the way you should remember it. You're always just going to use this syntax in Karel, and the only thing that's going to change is this number of times that you want to do something. All right, so besides that there's also sometimes, though, where you don't know how many times beforehand you want to do something.

And you might say, "Huh, that's kind of weird. When would I not know how many times I want to do something?" Well, let's say I'm Karel, and I'm standing here, and there's a wall over there. And I know there's a wall somewhere over there, because my world is finite. It has to end at some point, but one told me how many steps it is to that wall.

So if I say, "Hey, I'm going to take ten steps to that wall using a for-loop." One, two, three, four, five, six, and then I'm like, oh, dead Karel, right, and that's a bad time. So sometimes, we just don't know when the program starts, and what we want to say is, "Do something while some condition is true," like, keep going forward as long as there's no wall in front of you. And when there's a wall in front of you, stop going forward.

All right, so the way we do that is something called a while-loop. So at this point, hopefully you're intimately familiar with all of Karel's instructions. And the way the while-loop works, while, because that's what you want to do something.

You want to do something while there is some condition that's true, is the syntax looks like this, while, and then a paren, and inside here we're going to have some condition. Okay, so I'm going to put a squiggly line under it. So you don't put the word condition. We're going to put a condition in there in just a second, a close paren, and then we're going to have some body inside braces, open brace, close brace.

Now, where do these conditions come from? So one thing we can think about is the notion of moving until we get to a wall. And so Karel, it turns out, has some things that he can sense about his world, which are conditions you can check to see if there's something going on in this world.

One of the things you can check is front is clear, and that's an open paren and a close paren, and so there's actually two parens. Lower case F, capital I, capital C, all one word. And so what that asks Karel to do is say, "Where you're standing right now is your front clear," which means is there a wall right in front of the direction you're facing. If your front is clear, so while your front is clear, what it does, it basically checks if the front is clear, and that's true, then it executes the body of the while loop. So we could say, for example, move here. And so what it's going to do is, while my front is clear I move and it's still clear, and it's still clear, and I just keep doing this.

And at some point, I move along, and my front is no longer clear at this point. Front is clear is no longer true, and so I stop. Okay, and basically at that point I stop executing this loop and I just pick up from right after the close brace. So I'm after I'm done executing a loop, whether it's a for-loop or a while-loop, I just pick up executing after that close brace.

Okay, so I could actually turn this, for example, into a new method, private, void, walk to wall, or we'll call it move to wall like that. And then anytime I basically want to tell Karel, "Just keep moving forward until you hit a wall," I just essentially invoke, or call the move to wall method, and it will just get me up until I get to a wall.

Now you might wonder, hey, where are all these conditions and what are all the conditions? So if we can get the overhead for just a second, I'll show you. Page 18 of your reader. So on page 18, there's the lovely table one. Oh, lovely table one, and these are all the conditions you can check in Karel. There's front is clear, left is clear, right is clear. So you can sort of check to your left and right.

There's no behind is clear. Important for babies, not for Karel. There's beepers present, which means is there a beeper, at least one on the corner that you're at. Are there beepers in your bag? Is your bag not empty? Are you facing north, east, south, or west? So you can check all those conditions.

You can also check the opposite of all the conditions, like front is blocked. So you can actually check, like while your front is blocked you might want to turn left, because you want to keep turning until eventually your front gets cleared up, and then maybe you go do something else. Or your left is blocked, or your right is blocked.

So these are all – I'm not going to go through them all, but they're all sort of obvious. They sort of give you the obvious information that you would expect about Karel's world, and they're all in your course reader on page 18.

All right, so given that you have these conditions you can check. Sometimes you want to do something while some condition is true, and as soon as this condition is no longer true, you stop executing. There's also sometimes that rather than doing something over and over, you just want to say, let me check some condition and if it's true, then do this one thing.

So I'm not going to do it as a loop, but I'm just going to done thing. Okay, and that's something called an if statement, and the way an if statement works is it's if, space, open paren, some condition, again I'll put this condition in squigglies, open brace, close brace, and this is the body. And it says, if some condition is true, then do what it's in the braces. And if it's not true, just completely skip over this and keep executing from right after the braces.

So you might want to say, "Hey, I only want to pick up a beeper if I know a beeper exists in the world." So I sort of want to have a notion of having a safe pickup of a beeper. So I could say if beeper is present, which means there is a beeper, at least one on the corner that I'm at, then it's safe to pick a beeper.

Because if I didn’t necessarily check before, and I didn't know there was a beeper there for sure, I might try to pick up a beeper on some corner, and there isn't a beeper, and Karel blows up, and life is unhappy, and tears well in your eye, and the whole deal. All right, so if statement, that's just what we refer to it as kind of as an if statement. It's all lower case.

Now, sometimes what happens in life is you don't want to just say, "If something is true, then essentially what you want to do is this." You want to say, "If that thing is false, then I want to do something different." Okay, so you might want to say, "Hey, if there's a beeper present, I'm going to pick I up. But if there isn't one there, oh, Karel feels a little sad and he's going to put a beeper down to, like, plant a new tree because he wants to fight global warming."

So else and then we're going to have another body here, putBeeper, assuming that Karel has beepers in his bag. So what this says is, if there's a beeper present, then pick it up. If there is not a beeper present, it doesn't try to pick a beeper, it skips this part and does the part that's referred to by the else. So we'll put a beeper. So it will only execute one of these bodies, and which body it does depends on whether or not there are beepers present. If it's true, it's this one, if it's false, if that's one.

Question?

Student: Is that a space or a tab [inaudible]?

Instructor (Mehran Sahami): These are spaces here. So these are required to be spaces, and the syntax is also all in book too. So you can see where the spaces are there as well. Uh huh?

Student: Can you make multiple [inaudible]?

Instructor (Mehran Sahami):For the time being, you should just check one condition at a time. Now, you can actually sort of, what we refer to as nest, these kind of statements. So you could say, "If beeper is present," you might say, "Hey, if there's a beeper present there, that's some marker that I should move forward if there is not a wall in front of me." So what I want to do is, if there is a beeper present, what I now want to do is check to see if I can move forward. So if front is clear, move. And this is what we refer to as a nested expression. Notice how I sort of tabbed it in a little bit, so that it's kind of nested inside this other guy. What it means if check to see if beepers are present. If they're not present, then it skips this whole body and it just puts a beeper down.

If there is a beeper present, it's going to executed this body. Well, what is the body? It's another statement that says, "Is your front clear?" If your front is clear, you say, "Hey, I was on a beeper, and my front is clear. Now, I'll take a step forward." But if there was a beeper present, and my front was clear, or was not clear, I'm not going to take a step forward, in which case it doesn't do the if part. It finishes up and there's nothing else for it to do here. So it's done with this whole part and it's done with the whole if-else statement.

Okay, any questions about that, what's actually going on there, right? If beepers are present, you know you're only going to execute this part. This part is now a goner, because that's the else part, and beepers present was true. So to do this part, you come in here and you say, "Is front clear?" No, front's not clear. I have some wall in front of me.

Oh, okay, well I'm not going to do the move. Is there an else over here? No. This else is not attached here. This else is attached to this if that says, oh, there's no else. Okay, there's nothing else I should do. Are there any other statements over here that I should execute? No, I'm done with the whole body for this part. So it's done with the entire statement and it continues executing from down there.

Okay, so any questions about that? Uh huh?

Student: So is it every brace always comes in pairs?

Instructor (Mehran Sahami): Every brace comes in pairs. You always have an open brace and there's going to be some close brace that's going to define the body. Oh, that was the double. All right, so what we're going to do is we're going to put this all together in a big program.

Okay, so we're going to use all these things in a big program, and this program, I'll show you, is basically, Karel is going to run a little steeplechase. You're basically sort of like running hurdles, okay. So we're going to open up another program. Don't worry about all the details right now.

I'm just going to run this so I can show you what it looks like. So you can see what the world looks like and what we want Karel to do. So we're running, we're running, steeplechase. So what Karel's going to do here is they're the world that is always nine avenues long, and he knows that. It's always nine avenues long, which means there are, at most, eight steeples in the world, or eight hurdles.

The reason why we call them steeples as opposed to hurdles is because some of them are big. Some of them are just ginormous, and so what Karel needs to do is he needs to start here and end up over here, and run around every hurdle he encounters. So how are we going to do that using the stuff that we've learned, and putting it together into a larger program?

Well, the first thing we're going to do is we need to start with our friend, the run method. Right, so in the run method, all, Eclipse doesn't jump out in front of me. Right, so notice we have all the kind of other boilerplate that we want to have. We import Stanford Karel. We're going to have some public class we'll call steeplechase that extends super Karel. Right, all the stuff you've seen before as boilerplate.

We're going to define the run method and what the run method is going to do is, if you have nine avenues you need to go through, that means intervening the avenues, there's at most eight steeples. So I want you to do something eight times. So we're going to have a for-loop that executes eight times. What are you going to do inside there

Well, you have a choice. When you look at the world, either you're facing a steeple or you're not. So if we look over here, right, here Karel starts out facing a steeple, but after he jumps over it, hey it's clear. So he could actually move forward before jumping the next steeple. So that's essentially what we check for in the program. At every step, what we say is, "If your front is clear, there is no steeple for you to jump. So just move ahead.

But if your front is not clear, you got some work to do buddy. So jump hurdle." "And you're like, jump hurdle. I've been sitting here for 45 minutes. You never told me about jump hurdle. Where is jump hurdle?"

And I'm like, "Yeah, I didn't tell you about jump hurdle because we're going to write jump hurdle," and you're like, "Oh, yeah, new instruction that we create." So we're going to break our program down into smaller pieces. So what's jump hurdle about? How do we jump a hurdle?

Well, think about what you want to do to jump a hurdle, and I'll put it in the simplest possible terms. You want to ascend the hurdle. You want to go up. You want to move past the hurdle, and you want to descend the hurdle to come back down. You're like, "Yeah, thanks, Ron, that really helped a lot. How do I ascend and descend the hurdle, right?"

So what we're doing is we're breaking the program down into more and more steps, and notice this is reading like English. And the important thing to realize in programming is programming is not just about writing a program that the computer understands. Programming is about writing programs that people understand. I can't stress that enough. That's huge. That's what programming style is all about. It's what good software engineering is all about.

Writing a program that just works, that someone else can't read and understand, is actually really terrible software engineering. And I've seen software companies do this where some hotshot programmer comes along and they're like, "Oh, I'm great programmer." And they go and write some program to do something, and then it breaks. And then they come along and they say, "Hey, we need to actually get that program to do something slightly different, or we need to upgrade it. And it's written in terms of the code so badly that they can't do anything with it, and they throw it out completely, fire the programmer, and get a team of good software engineers to actually do it. I've actually seen that happen multiple times.

Okay, so write programs for people to read, not just for computers to read. Both of them need to be able to read it, but it's far more important that a person reads it and understands it, and that the computer still executes it correctly. But that's the first major software engineering principle to think about.

So how do we ascend and descend the hurdle? Move we knew about. Well, how do we ascend the hurdle? If you think about ascending the hurdle. Right, what that means is you're basically facing a wall, some wall that goes up some amount that you don't know.

Well, how am I going to get up that wall? I'm going to turn left, so now I'm looking up the wall. And guess what? If I put my right hand out against that wall and keep moving up along the wall, I can eventually get to a point where I've gotten to the top of that wall. So I turn left to face north, while my right is blocked, which is why that wall is there. I keep moving all the way up until my right is no longer blocked. That means I've extended all the way up the hurdle.

At this point, I'm still facing north. This guy's expecting me to face east, so I can move over the hurdle, right. If I'm facing north, I'm just going to step one more up. So I turn right at the end to now be way above the hurdle and be facing an open place where I can actually do that move.

So now, I do the move. I'm on the other side of the hurdle. I need to descend the hurdle. Well, how do I descend the hurdle? Ah, this is where our friend, move to wall, that we just wrote, comes in handy. So I'll show you both of these at the same time. If I want to descend, I'm at the top of the hurdle, I turn right.

So I'm looking south now, I'm looking down, and I just move all the way down to the wall. It hits the floor, and this is move to wall that we just wrote, right, while front is clear just moves. I move all the way down, and so when I move to wall and I get to the wall, I'm facing south. I want to turn left one last time so I'm facing forward to go again. Okay, so any questions about that?

Let me run Karel, so we can see if he's feeling up to the challenge. So here he is. We'll start the program. There he goes. Notice what he's doing. He goes over every hurdle. If his front is blocked, he goes up and over. Here's one where you can see it.

He goes all the way up until his right is clear. Then he moves and he comes all the way down until he hits the wall, and he keeps doing this. And if he does this eight times, he always ends up at the end because we know it's guaranteed to be nine avenues long. Uh huh? Student: [Inaudible]?

Instructor (Mehran Sahami): Yeah, good eye. So you might say, "Hey, before when Karel turned right and he was making three right and left turns, what's going on now?" It's super Karel, baby. We're loving it. Super Karel not only knows the three turn lefts, just turn right, but he's like, "Hey, forget turn left, man. I'm just turning right." So he knows, or she knows, or it knows, or whatever, that amorphous form in the sky knows.

Uh huh?

Student: [Inaudible]?

Instructor (Mehran Sahami):Good question, because that's not the specification of the program, right. So one question you could ask is, like, "Hey when I bought my word processor, I bought my word processor to, like, write essay with. So how come when I got my word processor," and this is a valid question to ask, "Why didn't it come with all the essays I needed to write at Stanford?" Right?

I mean, it would be nice if it did, right. I'd go pay the $400. I'd be like, woo hoo, super Karel, baby. I got super word processor. Right, because that's not the specification of the program. The specification of the program is to go over the hurdles one by one.

Now, just to see if – and you might say, "Oh, that’s kind of interesting, but does it just work on this one world?" So let's consider another world, super steeplechase. So we can load a world, say you can just click load world, and there are some worlds that we'll provide to you in your starter project, which is all explained in the handout.

Super steeplechase. So here's super steeplechase. Yeah, that might look familiar. More bars in more places, right. So here's Karel, right. This is like a world that 50 high. That's Karel down there and you're like, "Oh, man, you're really making," yeah, we're making him work. All right, so go little Karel. There he goes. Oh, oh, come on, give him a little encouragement. Go Karel, go Karel, go Karel.

Aw, yeah, because you can just speed him up if your program's running slow, but there he goes, right. Huge steeples, he's done, same program works. So the important lesson that comes from that is to think about the generality of the program, right.

You don't want to just write a program that works in one particular world, unless that's the only world you need to worry about. You want to generalize your program in a way so that it's using, in some sense, general principles that will apply to any world that meets your specifications. Right, it still needs to meet the specification. Our world is still nine avenues long and we know what the specification of the steeples are.

All right, so any quick questions before we go? Uh huh?

Student: So if you had the [inaudible]? 

Instructor (Mehran Sahami): No, because it's still just nine avenues. The for-loop counter stays the same, right. It's that while-loop that's actually going up and down the hurdles, because it doesn't know how big the hurdles are. Any other questions? 

Student: [Inaudible]?

Instructor (Mehran Sahami): That it's nine avenues and the hurdles are just pools, basically, of any length.

Student: [Inaudible].

Instructor (Mehran Sahami): Yeah, all right, I will see you on Friday. If you have any more questions, come on down.