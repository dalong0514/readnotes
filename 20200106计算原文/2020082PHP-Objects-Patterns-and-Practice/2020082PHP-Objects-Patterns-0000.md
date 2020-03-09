PHP Objects, Patterns, and Practice

Build powerful code by mastering PHP’s object-oriented enhancements, design patterns, and essential development tools—Fifth Edition—Matt Zandstra

Copyright © 2016 by Matt Zandstra

## About the Author

Matt Zandstra has worked as a web programmer, consultant, and writer for over two decades. He was a senior developer at Yahoo! working both in London and Silicon Valley. He now earns his living as a freelance consultant and writer. Before writing PHP Objects, Patterns, and Practice, he was the author of three editions of SAMS Teach Yourself PHP in 24 Hours (Sams Publishing, 1999) and a contributor to DHTML Unleashed (Sams.net Publishing, 1997). He has written articles for Linux Magazine, Zend.com, IBM DeveloperWorks, and php|architect Magazine, among others. Matt also studies literature and writes fiction. He holds MA degrees in Creative Writing from both Manchester University and the University of East Anglia. When he’s not studying or freelancing at various locations around the UK, Matt lives in Brighton with his wife, Louise, and two children, Holly and Jake. 

## About the Technical Reviewer

Paul Tregoing has worked in ops and development in a variety of environments for nearly twenty years. He worked at Yahoo! for five years as a senior developer on the frontpage team, there he generated his first PHP using Perl. Other employers include Bloomberg, Schlumberger and the British Antarctic Survey, where he became intimate with thousands of penguins.

He now works as a freelance engineer for various clients, small and large, building multi-tiered web apps using PHP, Javascript, and many other technologies. Paul is a voracious consumer of science fiction and fantasy, and harbours not-so-secret ambitions to try his hand at writing in the near future. He lives in Cambridge, UK with this wife and children.

## Introduction

When I first conceived of this book, object-oriented design in PHP was an esoteric topic. The intervening years have not only seen the inexorable rise of PHP as an object-oriented language, but also the march of the framework. Frameworks are incredibly useful, of course. They manage the guts and the glue of many (perhaps, these days, most) web applications. What’s more, they often exemplify precisely the principles of design that this book explores.

There is, though, a danger for developers here, as there is in all useful APIs. This is the fear that one might find oneself relegated to userland, forced to wait for remote gurus to fix bugs or add features at their whim. It’s a short step from this standpoint to a kind of exile in which one is left regarding the innards of a framework as advanced magic, and one’s own work as not much more than a minor adornment stuck up on top of a mighty unknowable infrastructure.

Although I’m an inveterate reinventor of wheels, the thrust of my argument is not that we should all throw away our frameworks and build MVC applications from scratch (at least not always). It is rather that, as developers, we should understand the problems that frameworks solve, and the strategies they use to solve them. We should be able to evaluate frameworks not only functionally but in terms of the design decisions their creators have made, and to judge the quality of their implementations. And yes, when the conditions are right, we should go ahead and build our own spare and focused applications, and, over time, compile our own libraries of reusable code.

I hope this book goes some way toward helping PHP developers apply design-oriented insights to their platforms and libraries, and provides some the conceptual tools needed when it’s time to go it alone.