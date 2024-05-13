## Preface

Initially, all processing used to happen on the server's side and simple output was the response to web browsers. Nowadays, there are so many JavaScript frameworks and libraries that help readers to create charts, animations, simulations, and so on. By the time a project finishes or reaches a stable state, so much JavaScript code has already been written that changing and maintaining it further is tedious. At this point comes the importance of automated testing, and more specifically, developing all that code in a test-driven environment. Test-driven development is a methodology that makes testing the central part of the design process—before writing code, developers decide upon the conditions that code must meet to pass a test. The end goal is to help the readers understand the importance and process of using TDD as a part of the development.

This book starts with the details of test-driven development, its importance, need, and benefits. Later, the book introduces popular tools and frameworks, such as YUI, Karma, QUnit, DalekJS, JsUnit, and so on, to utilize Jasmine, Mocha, and Karma for advanced concepts such as feature detection, server-side testing, and patterns. We are going to understand, write, run tests, and further debug our programs. The book concludes with best practices in JavaScript testing. By the end of the book, the readers will know why they should test, how to do it most efficiently, and will have a number of versatile tests (and methods to devise new tests) so they can get to work immediately.

What this book covers:

Chapter 1, Overview of TDD, introduces the test-driven development, its life cycle, benefits, and myths.

Chapter 2, Testing Concepts, brings the TDD life cycle into action using Yahoo User Interface (YUI) Tests, and explains how unit testing can be done for JavaScript.

Chapter 3, Testing Tools, introduces JsUnit, QUnit, Karma, and DalekJS, which are some of the popular unit testing frameworks for JavaScript.

Chapter 4, Jasmine, introduces behavior-driven development and the Jasmine framework, its setup, usage, and customization, along with several features that a good unit testing framework should cover.

Chapter 5, JsTestDriver, showcases the JsTestDriver unit testing tool and its integration with IDE.

Chapter 6, Feature Detection, explores has.js and Modernizr JavaScript libraries for feature detection and explains why feature detection should have preference over browser detection.

Chapter 7, Observer Design Pattern, explains the observer pattern for JavaScript and its role in the test-driven development.

Chapter 8, Testing with Server-Side JS, covers server-side JavaScript unit testing using Node.js, Mocha, and Chai while using MongoDB as a database.

Chapter 9, Best Practices, lists best practices used to unit test JavaScript and also helps to make a good choice among popular unit testing frameworks and tools by explaining the features.