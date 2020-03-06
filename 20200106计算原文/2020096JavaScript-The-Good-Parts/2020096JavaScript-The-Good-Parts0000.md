JavaScript: The Good Parts

by Douglas Crockford

Copyright © 2008 Yahoo! Inc. All rights reserved.

## Preface

If we offend, it is with our good will

That you should think, we come not to offend,

But with good will. To show our simple skill,

That is the true beginning of our end.

—William Shakespeare, A Midsummer Night’s Dream

This is a book about the JavaScript programming language. It is intended for programmers who, by happenstance or curiosity, are venturing into JavaScript for the first time. It is also intended for programmers who have been working with JavaScript at a novice level and are now ready for a more sophisticated relationship with the language. JavaScript is a surprisingly powerful language. Its unconventionality presents some challenges, but being a small language, it is easily mastered.

My goal here is to help youto learn to think in JavaScript. I will show youthe components of the language and start you on the process of discovering the ways those components can be put together. This is not a reference book. It is not exhaustive about the language and its quirks. It doesn’t contain everything you’ll ever need to know. That stuff you can easily find online. Instead, this book just contains the things that are really important.

This is not a book for beginners. Someday I hope to write a JavaScript: The First Parts book, but this is not that book. This is not a book about Ajax or web programming. The focus is exclusively on JavaScript, which is just one of the languages the web developer must master.

This is not a book for dummies. This book is small, but it is dense. There is a lot of material packed into it. Don’t be discouraged if it takes multiple readings to get it.

Your efforts will be rewarded.

xi

Conventions Used in This Book

The following typographical conventions are used in this book: Italic

Indicates new terms, URLs, filenames, and file extensions.

Constant width

Indicates computer coding in a broad sense. This includes commands, options, variables, attributes, keys, requests, functions, methods, types, classes, modules, properties, parameters, values, objects, events, event handlers, XML and XHTML tags, macros, and keywords.

Constant width bold

Indicates commands or other text that should be typed literally by the user.

Using Code Examples

This book is here to help youget your job done. In general, youmay use the code in this book in your programs and documentation. You do not need to contact us for permission. For example, writing a program that uses several chunks of code from this book does not require permission. Selling or distributing a CD-ROM of examples from O’Reilly books does require permission. Answering a question by citing this book and quoting example code does not require permission. Incorporating a significant amount of example code from this book into your product’s documentation does require permission.

We appreciate, but do not require, attribution. An attribution usually includes the title, author, publisher, and ISBN. For example:「JavaScript: The Good Parts by Douglas Crockford. Copyright 2008 Yahoo! Inc., 978-0-596-51774-8.」

If you feel your use of code examples falls outside fair use or the permission given here, feel free to contact us at permissions@oreilly.com.

Safari® Books Online

When yousee a Safari® Books Online icon on the cover of your favorite technology book, that means the book is available online through the O’Reilly Network Safari Bookshelf.

Safari offers a solution that’s better than e-books. It’s a virtual library that lets you easily search thousands of top tech books, cut and paste code samples, download chapters, and find quick answers when you need the most accurate, current information. Try it for free at http://safari.oreilly.com.

xii

|

Preface

How to Contact Us

Please address comments and questions concerning this book to the publisher: O’Reilly Media, Inc.

1005 Gravenstein Highway North

Sebastopol, CA 95472

800-998-9938 (in the United States or Canada)

707-829-0515 (international or local)

707-829-0104 (fax)

We have a web page for this book, where we list errata, examples, and any additional information. You can access this page at:

http://www.oreilly.com/catalog/9780596517748/

To comment or ask technical questions about this book, send email to:

bookquestions@oreilly.com

For more information about our books, conferences, Resource Centers, and the O’Reilly Network, see our web site at:

http://www.oreilly.com/

Acknowledgments

I want to thank the reviewers who pointed out my many egregious errors. There are few things better in life than having really smart people point out your blunders. It is even better when they do it before you go public. Thank you, Steve Souders, Bill Scott, Julien Lecomte, Stoyan Stefanov, Eric Miraglia, and Elliotte Rusty Harold.

I want to thank the people I worked with at Electric Communities and State Software who helped me discover that deep down there was goodness in this language, especially Chip Morningstar, Randy Farmer, John La, Mark Miller, Scott Shattuck, and Bill Edney.

I want to thank Yahoo! Inc. for giving me time to work on this project and for being such a great place to work, and thanks to all members of the Ajax Strike Force, past and present. I also want to thank O’Reilly Media, Inc., particularly Mary Treseler, Simon St.Laurent, and Sumita Mukherji for making things go so smoothly.

Special thanks to Professor Lisa Drake for all those things she does. And I want to thank the guys in ECMA TC39 who are struggling to make ECMAScript a better language.

Finally, thanks to Brendan Eich, the world’s most misunderstood programming language designer, without whom this book would not have been necessary.


