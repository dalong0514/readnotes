Copyright © 2020 Alex Banks and Eve Porcello

## Preface

This book is for developers who want to learn the React library while learning the latest techniques currently emerging in the JavaScript language. This is an exciting time to be a JavaScript developer. The ecosystem is exploding with new tools, syntax, and best practices that promise to solve many of our development problems. Our aim with this book is to organize these techniques so you can get to work with React right away. We'll get into state management, React Router, testing, and server rendering, so we promise not to introduce only the basics and then throw you to the wolves.

This book does not assume any knowledge of React at all. We'll introduce all of React's basics from scratch. Similarly, we won't assume that you've worked with the latest JavaScript syntax. This will be introduced in Chapter 2 as a foundation for the rest of the chapters.

You'll be better prepared for the contents of the book if you're comfortable with HTML, CSS, and JavaScript. It's almost always best to be comfortable with these big three before diving into a JavaScript library.

Along the way, check out the GitHub repository. All of the examples are there and will allow you to practice hands-on.

### Conventions Used in This Book

The following typographical conventions are used in this book: 

Italic. Indicates new terms, URLs, email addresses, filenames, and file extensions.

Constant width. Used for program listings, as well as within paragraphs to refer to program elements such as variable or function names, databases, data types, environment variables, statements, and keywords.

Constant width bold. Shows commands or other text that should be typed literally by the user.

TIP: This element signifies a tip or suggestion.

NOTE: This element signifies a general note.

WARNING: This element indicates a warning or caution.

### Using Code Examples

Supplemental material (code examples, exercises, etc.) is available for download at https://github.com/moonhighway/learning-react. If you have a technical question or a problem using the code examples, please send email to bookquestions@oreilly.com.

1-2-3『

[MoonHighway/learning-react: The code samples for Learning React by Alex Banks and Eve Porcello, published by O'Reilly Media](https://github.com/moonhighway/learning-react)

已下载源码作为本书附件。（2021-04-29）

』

This book is here to help you get your job done. In general, if example code is offered with this book, you may use it in your programs and documentation. You do not need to contact us for permission unless you're reproducing a significant portion of the code. For example, writing a program that uses several chunks of code from this book does not require permission. Selling or distributing examples from O'Reilly books does require permission. Answering a question by citing this book and quoting example code does not require permission.

Incorporating a significant amount of example code from this book into your product's documentation does require permission.

We appreciate, but generally do not require, attribution. An attribution usually includes the title, author, publisher, and ISBN. For example:

「Learning React by Alex Banks and Eve Porcello (O'Reilly).

Copyright 2020 Alex Banks and Eve Porcello, 978-1-492-05172-5.」

If you feel your use of code examples falls outside fair use or the permission given above, feel free to contact us at

permissions@oreilly.com.

O'Reilly Online Learning

NOTE: For more than 40 years, O'Reilly Media has provided technology and business training, knowledge, and insight to help companies succeed.

Our unique network of experts and innovators share their knowledge and expertise through books, articles, and our online learning platform.

O'Reilly's online learning platform gives you on-demand access to live training courses, in-depth learning paths, interactive coding environments, and a vast collection of text and video from O'Reilly and 200+ other publishers. For more information, visit

http://oreilly.com.

How to Contact Us

Please address comments and questions concerning this book to the publisher:

O'Reilly Media, Inc.

1005 Gravenstein Highway North

Sebastopol, CA 95472

800-998-9938 (in the United States or Canada)

707-829-0515 (international or local)

707-829-0104 (fax)

We have a web page for this book, where we list errata, examples, and

any additional information. You can access this page at

https://oreil.ly/learningReact_2e.

Email bookquestions@oreilly.com to comment or ask technical questions about this book.

For news and information about our books and courses, visit

http://oreilly.com.

Find us on Facebook: http://facebook.com/oreilly

Follow us on Twitter: http://twitter.com/oreillymedia

Watch us on YouTube: http://www.youtube.com/oreillymedia

## Acknowledgments

Our journey with React wouldn't have started without some good old-fashioned luck. We used YUI when we created the training materials for the full-stack JavaScript program we taught internally at Yahoo.

Then in August 2014, development on YUI ended. We had to change all our course files, but to what? What were we supposed to use on the front-end now? The answer: React. We didn't fall in love with React immediately; it took us a couple hours to get hooked. It looked like React could potentially change everything. We got in early and got really lucky.

We appreciate the help of Angela Rufino and Jennifer Pollock for all the support in developing this second edition. We also want to

acknowledge Ally MacDonald for all her editing help in the first edition. We're grateful to our tech reviewers, Scott Iwako, Adam Rackis, Brian Sletten, Max Firtman, and Chetan Karande.

There's also no way this book could have existed without Sharon Adams and Marilyn Messineo. They conspired to purchase Alex's first computer, a Tandy TRS 80 Color Computer. It also wouldn't have made it to book form without the love, support, and encouragement of Jim and Lorri Porcello and Mike and Sharon Adams.

We'd also like to acknowledge Coffee Connexion in Tahoe City, California, for giving us the coffee we needed to finish this book, and its owner, Robin, who gave us the timeless advice:「A book on programming? Sounds boring!」