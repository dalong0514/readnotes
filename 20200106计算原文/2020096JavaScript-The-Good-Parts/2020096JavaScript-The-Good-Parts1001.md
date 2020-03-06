—William Shakespeare, Love’s Labor’s Lost

I was invited last year to contribute a chapter to Andy Oram’s and Greg Wilson’s Beautiful Code (O’Reilly), an anthology on the theme of beauty as expressed in computer programs. I wanted to write my chapter in JavaScript. I wanted to use it to present something abstract, powerful, and useful to show that the language was up to it. And I wanted to avoid the browser and other venues in which JavaScript is typecast. I wanted to show something respectable with some heft to it.

I immediately thought of Vaughn Pratt’s Top Down Operator Precedence parser, which I use in JSLint (see Appendix C). Parsing is an important topic in computing.

The ability to write a compiler for a language in itself is still a test for the complete-ness of a language.

I wanted to include all of the code for a parser in JavaScript that parses JavaScript.

But my chapter was just one of 30 or 40, so I felt constrained in the number of pages I could consume. A further complication was that most of my readers would have no experience with JavaScript, so I also would have to introduce the language and its peculiarities.

So, I decided to subset the language. That way, I wouldn’t have to parse the whole language, and I wouldn’t have to describe the whole language. I called the subset Simplified JavaScript. Selecting the subset was easy: it included just the features that I needed to write a parser. This is how I described it in Beautiful Code: Simplified JavaScript is just the good stuff, including: Functions as first class objects

Functions in Simplified JavaScript are lambdas with lexical scoping.

98

Dynamic objects with prototypal inheritance Objects are class-free. We can add a new member to any object by ordinary assignment. An object can inherit members from another object.

Object literals and array literals

This is a very convenient notation for creating new objects and arrays. JavaScript literals were the inspiration for the JSON data interchange format.

The subset contained the best of the Good Parts. Even though it was a small language, it was very expressive and powerful. JavaScript has lots of additional features that really don’t add very much, and as you’ll find in the appendixes that follow, it has a lot of features with negative value. There was nothing ugly or bad in the subset. All of that fell away.

Simplified JavaScript isn’t strictly a subset. I added a few new features. The simplest was adding pi as a simple constant. I did that to demonstrate a feature of the parser.

I also demonstrated a better reserved word policy and showed that reserved words are unnecessary. In a function, a word cannot be used as both a variable or parameter name and a language feature. You can use a word for one or the other, and the programmer gets to choose. That makes a language easier to learn because you don’t need to be aware of features you don’t use. And it makes the language easier to extend because it isn’t necessary to reserve more words to add new features.

I also added block scope. Block scope is not a necessary feature, but not having it confuses experienced programmers. I included block scope because I anticipated that my parser would be used to parse languages that are not JavaScript, and those languages would do scoping correctly. The code I wrote for the parser is written in a style that doesn’t care if block scope is available or not. I recommend that youwrite that way, too.

When I started thinking about this book, I wanted to take the subset idea further, to show how to take an existing programming language and make significant improvements to it by making no changes except to exclude the low-value features.

We see a lot of feature-driven product design in which the cost of features is not properly accounted. Features can have a negative value to consumers because they make the products more difficult to understand and use. We are finding that people like products that just work. It turns out that designs that just work are much harder to produce than designs that assemble long lists of features.

Features have a specification cost, a design cost, and a development cost. There is a testing cost and a reliability cost. The more features there are, the more likely one will develop problems or will interact badly with another. In software systems, there is a storage cost, which was becoming negligible, but in mobile applications is becoming significant again. There are ascending performance costs because Moore’s Law doesn’t apply to batteries.

Beautiful Features

|

99

Features have a documentation cost. Every feature adds pages to the manual, increasing training costs. Features that offer value to a minority of users impose a cost on all users. So, in designing products and programming languages, we want to get the core features—the good parts—right because that is where we create most of the value.

We all find the good parts in the products that we use. We value simplicity, and when simplicity isn’t offered to us, we make it ourselves. My microwave oven has tons of features, but the only ones I use are cook and the clock. And setting the clock is a struggle. We cope with the complexity of feature-driven design by finding and sticking with the good parts.

It would be nice if products and programming languages were designed to have only good parts.

100

|

Chapter 10: Beautiful Features

Appendix A

APPENDIX A

Awful Parts1

That will prove awful both in deed and word.

