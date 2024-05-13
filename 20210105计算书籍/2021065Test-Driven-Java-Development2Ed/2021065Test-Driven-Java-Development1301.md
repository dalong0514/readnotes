This chapter tackles a possible solution for this, which is using Jenkins. A virtual machine with an instance of Jenkins was configured to automate some of the repetitive tasks that were draining time from the team.

Once the problems have been addressed, TDD becomes really handy. Every new feature developed in the TDD way will be more than covered by tests, then future changes on that feature will be run against the test suite, and this will fail if one of the tests is not satisfied.

[ 291 ]

Other Books You May Enjoy

If you enjoyed this book, you may be interested in these other books by Packt: Java 9 High Performance

Mayur Ramgir, Nick Samoylov

ISBN: 978-1-78712-078-5

Work with JIT compilers

Understand the usage of profiling tools

Generate JSON with code examples

Leverage the command-line tools to speed up application development

Build microservices in Java 9

Explore the use of APIs to improve application code

Speed up your application with reactive programming and concurrency

Other Books You May Enjoy

Test-Driven iOS Development with Swift 4 - Third Edition

Dr. Dominik Hauser

ISBN: 978-1-78847-570-9

Implement TDD in Swift application development

Find bugs before you enter code using the TDD approach

Use TDD to build models, view controllers, and views

Test network code with asynchronous tests and stubs

Write code that is a joy to read and maintain

Develop functional tests to ensure the app works as planned

[ 293 ]

Other Books You May Enjoy

Leave a review - let other readers know what

you think

Please share your thoughts on this book with others by leaving a review on the site that you bought it from. If you purchased the book from Amazon, please leave us an honest review on this book's Amazon page. This is vital so that other potential readers can see and use your unbiased opinion to make purchasing decisions, we can understand what our customers think about our products, and our authors can see your feedback on the title that they have worked with Packt to create. It will only take a few minutes of your time, but is valuable to other potential customers, our authors, and Packt. Thank you!

[ 294 ]

Index

A

advantages 12

disadvantages 12

acceptance criteria 190

reference link 223

acceptance test-driven development (ATDD) 13

acceptance tests 87

C

Alexandria project

call extraction, Alexandria project

about 222

constructor, parameterizing 236, 237

black-box testing 223

new feature, adding 237, 239

call, extracting 234, 236

call override, Alexandria project

call, overriding 234, 236

constructor, parameterizing 236, 237

legacy code algorithm, applying 228

new feature, adding 237, 239

new feature, adding 223

Clover

preliminary investigation 224, 225, 226

reference link 272

primitive obsession, removing with status as int

Cobertura

239, 242

reference link 272

spike testing 223

code coverage

technical comments 223

reference link 214

application debugging

code refactoring 86

avoiding 17

code smell

Awesome Gambling Corp

reference link 211

about 275

commands, remote-controlled ship development

codebase, exploring 275, 278

combined commands 106, 107

conclusions 280

single commands 104, 105

production, deployments 279, 280

Connect 4 game

release procedure 278, 279

about 117

B

reference link 117

requirements 117

Bamboo

constructor chaining 236

reference link 267

continuous delivery

behavior-driven development (BDD)

about 245, 246, 282

about 12, 185, 189, 190

builds, automating 286, 288

book store 193, 195, 196

continuous integration, implementing 282

narrative 190, 191

example 290

scenarios 191, 192, 193

executing 289, 290

specifications 186

improvements 281

black-box testing

Jenkins installation 283, 285, 286

about 11

test coverage, increasing 281

G

continuous deployment (CD) 282

continuous integration (CI) 16, 245, 246, 279

Gradle project

curl

setting up, in IntelliJ IDEA 55, 58

reference link 228

Grizzly

reference link 232

D

H

DbUnit

reference link 228

helper classes 95, 96

dependency injection 137, 226

Hudson

Don't Repeat Yourself (DRY) principle

reference link 267

reference link 115

I

E

infrastructure team (IT) 279

environment

integration tests 87, 164

setting up, with Gradle 55

IntelliJ IDEA

setting up, with JUnit 55

Gradle project, setting up 55, 58

executable documentation 15, 16, 17

Java project, setting up 55, 58

extract 219

Extreme Programming (XP)

J

about 8

Java Code Coverage (JaCoCo)

reference link 85

reference link 272

Java Functional Programming

F

environment, setting up 170

Feature Flags 247

Java project

Feature Flipping 247

setting up, in IntelliJ IDEA 55, 58

feature toggles, example

JBehave stories, writing

about 248, 252

reference link 194

Fibonacci service, implementing 252, 253, 255

JBehave

template engine, working with 255, 256, 258,

about 197

259

final validation 207, 209

Feature Toggles

pending steps 198, 199, 200

about 247

runner 197

FF4J 247

steps 201, 202, 203, 204, 205, 206, 207

Togglz 247

Jenkins

FF4J

reference link 267

reference link 247

JUnit

Fibonacci's sequence

@AfterMethod annotation 91

reference link 252

@BeforeClass annotation 91

functional tests 87

@BeforeMethod annotation 91

functions

@Test annotation 89

about 174

@Test(expectedExceptions = SomeClass.class)

Reverse Polish Notation (RPN) 175

annotation argument 91

reference link 92

[ 296 ]

versus TestNG 91

N

K

null class 170, 171

kata exercise 222

O

keep it simple, stupid (KISS)

about 88, 268

Occam's razor principle

reference link 115

reference link 115

Optional class

L

about 171, 173

legacy code algorithm, applying

example 171

about

orientation, remote-controlled ship development

228

BookRepository dependency, injecting

direction, keeping in memory 97

234

end-to-end test cases, writing

implementation 98

228, 230, 231

test cases, automating

position, keeping in memory 97

232, 233

legacy code change algorithm

refactoring 98

217

legacy code change algorithm, applying

override call 219

about 217

P

change points, identifying 217

dependencies, breaking 219, 220, 221

partial mocking 150

test points, finding 218, 219

players, Tic-Tac-Toe game

tests, writing 221

player O 71

legacy code

player X 70, 71

about 211

X's turn, checking 72

example 212, 213, 214

police syndrome 14

lack of dependency injection 216

Postman

recognition 215, 216

reference link 228

legacy kata

preliminary investigation

about 222

about 224, 225, 226

Alexandria project 222

candidates, finding for refactoring 226

new feature, introduction 227

M

primitive obsession

markdown

reference link 240

reference link

Principles of OOD

188

Mars Rover

reference link 116

92

method reference

product owner (PO) 223

182

Minimum Viable Product (MVP) 191

Q

mocking

about 14, 140

quality assurance (QA)

features 141

about 13, 278

mock objects 142, 143

versus quality checking 13

terminology 141, 142

Mockito

R

about 143

red-green-refactor process

about 8, 9, 10, 58, 262

[ 297 ]

implementation code, writing 59

keep it simple, stupid (KISS) 115

last test failure, confirming 59

Occam's razor principle 115

refactoring 60

You Ain't Gonna Need It principle 114

repeating 60

SOLID principles

test, writing 59

dependency inversion principle 116

tests, executing 59, 60

interface segregation principle 116

remote-controlled ship development

liskov substitution principle 116

about 93

open-closed principle 116

backward moves 99, 101

single responsibility principle 116

commands 103

specifications, Behavior-Driven Development (BDD)

forward moves 99, 101

documentation 187

helper classes 95, 96

documentation, for coders 188

obstacles detection 111

documentation, for non-coders 189

orientation 96, 97

spheric maps, remote-controlled ship development

project setup 93, 95

map boundaries 110

ship, rotating 102

planet information 108, 109

spheric maps, representing 107

Spring Boot

starting point 96, 97

reference link 248

remote-controlled ship

store moves, Tic-Tac-Toe v2

requirements 92

clear state between games 155

REpresentational State Transfer (REST) 278

DB name, specifying 146

requisites, Reverse Polish Notation (RPN)

drop operation feedback 156

complex operations 179, 180

error handling 154, 156

invalid input, handling 176

items, adding to Mongo collection 149, 150, 151

single operations 177

name, defining for Mongo collection 147

RestAssured

operation feedback, adding 153

reference link 233

store turn, Tic-Tac-Toe v2

Reverse Polish Notation (RPN)

alternate players 162, 163

about 175

collection, creating 158, 159

requisites 175, 176

current move, storing 159

Rule feature, JUnit

error handling 161

reference link 62

strategy pattern

reference link

S

217

Streams

Selenide

about 181

reference link 201

filter function 181

Selenium

flatMap function 182, 183

reference link 200

map function 182

ship rotation, remote-controlled ship development

reduce function 183

specification, for turning left 102

reference link 181

specification, for turning right 103

software design

T

114

software design principles

TDD best practices

about 114

about 263

Don't Repeat Yourself (DRY) principle 115

development practices 268, 269, 271

[ 298 ]

naming conventions 264, 265

Thymeleaf

processes 266, 267

reference link 248

tools 272

Tic-Tac-Toe game

test double 14, 87

board boundaries 65, 66, 67

test-driven development (TDD)

code coverage 81, 82

testable code design 11

developing 61

about 6, 7, 8, 262, 263

integration test 165, 167

features 10

pieces, placing 62, 64

red-green-refactor process 8, 9, 10

pieces, placing on unoccupied spaces 67, 68

test-first implementation, of Connect 4 game

reference link 61

about 126

requirements 61

board 127

tie condition 79, 80

discs 128

two players support, adding 69, 70

Hamcrest, using 126

win conditions, adding 72, 73, 74, 75, 76, 77, 78

output 131

Tic-Tac-Toe v2 game, developing

player shifts 130

about 144

win condition, scenarios 133, 134, 135

moves, storing 145

test-last implementation, of Connect 4 game

turn, storing 157

about 118

Tic-Tac-Toe v2 game

board 118, 119

requirements 143

discs 119, 120

time to market (TTM) 6

output 121

Togglz

player shifts 120

reference link 247

win condition, scenarios 122, 124, 126

Travis

testing

reference link 267

about 11

black-box testing 11

U

quality checking, versus quality assurance 13

unit testing

white-box testing 12

about 85

TestNG

limitations 86

@AfterClass annotation 91

need for 86

@AfterGroups annotation 90

with test-driven development (TDD) 88

@AfterSuite annotation 90

user acceptance tests 118

@AfterTest annotation 90

@BeforeGroups annotation 90

W

@BeforeSuite annotation 90

white-box testing

@BeforeTest annotation 90

about 12

@Test annotation 89

advantages 12

@Test(enable = false) annotation argument 91

disadvantages 13

about 89

reference link 92

Y

versus JUnit 91

tests

YAML Ain't Markup Language (YAML) 249

separation, in Gradle 164, 165

You Ain't Gonna Need It principle

thimblerig service 275

reference link 114

Document Outline

Cover

Title Page

Copyright and Credits

Packt Upsell

Contributors

Table of Contents

Preface

Chapter 1: Why Should I Care for Test-Driven Development? Why TDD? Understanding TDD

Red-Green-Refactor

Speed is the key

It's not about testing

Testing Black-box testing

White-box testing

The difference between quality checking and quality assurance

Better tests

Mocking

Executable documentation

No debugging

Summary

Chapter 2: Tools, Frameworks, and Environments Git

Virtual machines Vagrant

Docker

Build tools

The integrated development environment The IDEA demo project

Unit-testing frameworks JUnit

TestNG

Hamcrest and AssertJ Hamcrest

AssertJ

Code coverage tools JaCoCo

Mocking frameworks Mockito

EasyMock

Extra power for mocks

User interface testing Web-testing frameworks

Selenium

Selenide

Behavior-driven development JBehave

Cucumber

Summary

Chapter 3: Red-Green-Refactor – From Failure Through Success until Perfection Setting up the environment with Gradle and JUnit Setting up Gradle/Java project in IntelliJ IDEA

The Red-Green-Refactor process Writing a test

Running all the tests and confirming that the last one is failing

Writing the implementation code

Running all the tests

Refactoring

Repeating

Tic-Tac-Toe game requirements

Developing Tic-Tac-Toe Requirement 1 – placing pieces Test – board boundaries I

Implementation

Test – board boundaries II

Implementation

Test – occupied spot

Implementation

Refactoring

Requirement 2 – adding two-player support Test – X plays first

Implementation

Test – O plays right after X

Implementation

Test – X plays right after O

Requirement 3 – adding winning conditions Test – by default there's no winner

Implementation

Test – winning condition I

Implementation

Refactoring

Test – winning condition II

Implementation

Test – winning condition III

Implementation

Test – winning condition IV

Implementation

Refactoring

Requirement 4 – tie conditions Test – handling a tie situation

Implementation

Refactoring

Code coverage

More exercises

Summary

Chapter 4: Unit Testing – Focusing on What You Do and Not on What Has Been Done Unit testing What is unit testing?

Why unit testing?

Code refactoring

Why not use unit tests exclusively?

Unit testing with TDD

TestNG The @Test annotation

The @BeforeSuite, @BeforeTest, @BeforeGroups, @AfterGroups, @AfterTest, and @AfterSuite annotations

The @BeforeClass and @AfterClass annotations

The @BeforeMethod and @AfterMethod annotations

The @Test(enable = false) annotation argument

The @Test(expectedExceptions = SomeClass.class) annotation argument

TestNG versus JUnit summary

Remote-controlled ship requirements

Developing the remote-controlled ship Project setup

Helper classes

Requirement – starting point and orientation Specification – keeping position and direction in memory

Implementation

Refactoring

Requirement – forward and backward moves Specification – moving forward

Implementation

Specification – moving backward

Implementation

Requirement – rotating the ship Specification – turning left

Implementation

Specification – turning right

Implementation

Requirement – commands Specification – single commands

Implementation

Specification – combined commands

Implementation

Requirement – representing spheric maps Specification – planet information

Implementation

Refactoring

Specification – dealing with map boundaries

Implementation

Requirement – detecting obstacles

Summary

Chapter 5: Design – If It's Not Testable, It's Not Designed Well Why should we care about design? Design principles You Ain't Gonna Need It

Don't Repeat Yourself

Keep it simple, stupid

Occam's razor

SOLID principles

Connect 4 Requirements

Test-last implementation of Connect 4 Requirement 1 – the game's board

Requirement 2 – introducing discs

Requirement 3 – player shifts

Requirement 4 – the game's output

Requirement 5 – win conditions (I)

Requirement 6 – win condition (II)

Requirement 7 – win condition (III)

Requirement 8 – win condition (IV)

The TDD or test-first implementation Hamcrest

Requirement 1 – the game's board

Requirement 2 – introducing discs

Requirement 3 – player shifts

Requirement 4 – the game's output

Requirement 5 – win condition (I)

Requirement 6 – win condition (II)

Requirement 7 – win condition (III)

Requirement 8 – win condition (IV)

Final considerations

Summary

Chapter 6: Mocking – Removing External Dependencies Mocking Why mocks?

Terminology

Mock objects

Mockito

Tic-Tac-Toe v2 requirements

Developing Tic-Tac-Toe v2 Requirement 1 – store moves Specification – DB name

Implementation

Specification – a name for the Mongo collection

Implementation

Refactoring

Specification – adding items to the Mongo collection

Implementation

Specification – adding operation feedback

Implementation

Refactoring

Specification – error handling

Implementation

Specification – clear state between games

Implementation

Specification – drop operation feedback

Implementation

Specification – error handling

Implementation

Requirement 2 – store every turn Specification – creating new collection

Implementation

Specification refactoring

Specification – storing current move

Implementation

Specification – error handling

Implementation

Specification – alternate players

Implementation

Exercises

Integration tests Tests separation

The integration test

Summary

Chapter 7: TDD and Functional Programming – A Perfect Match Setting up the environment

Optional – dealing with uncertainty Example of Optional

Functions revisited Kata – Reverse Polish Notation Requirements Requirement – handling invalid input

Requirement – single operations

Requirement – complex operations

Streams filter

map

flatMap

reduce

Summary

Chapter 8: BDD – Working Together with the Whole Team Different specifications Documentation

Documentation for coders

Documentation for non-coders

Behavior-driven development Narrative

Scenarios

The book store BDD story

JBehave JBehave runner

Pending steps

Selenium and Selenide

JBehave steps

Final validation

Summary

Chapter 9: Refactoring Legacy Code – Making It Young Again Legacy code Legacy code example Other ways to recognize legacy code

A lack of dependency injection

The legacy code change algorithm

Applying the legacy code change algorithm Identifying change points

Finding test points

Breaking dependencies

Writing tests

The kata exercise Legacy kata

Description

Technical comments

Adding a new feature

Black-box or spike testing

Preliminary investigation How to find candidates for refactoring

Introducing the new feature

Applying the legacy code algorithm Writing end-to-end test cases

Automating the test cases

Injecting the BookRepository dependency

Extract and override call Parameterizing a constructor

Adding a new feature

Removing the primitive obsession with status as int

Summary

Chapter 10: Feature Toggles – Deploying Partially Done Features to Production Continuous integration, delivery, and deployment

Feature Toggles

A Feature Toggle example Implementing the Fibonacci service

Working with the template engine

Summary

Chapter 11: Putting It All Together TDD in a nutshell

Best practices Naming conventions

Processes

Development practices

Tools

Summary

Chapter 12: Leverage TDD by Implementing Continuous Delivery Case study – Awesome Gambling Corp Exploring the codebase

Release procedure

Deployments to production

Conclusions

Possible improvements Increasing test coverage

Implementing continuous integration

Towards continuous delivery Jenkins installation

Automating builds

First execution

What is next?

This is just the beginning

This does not have to be the end

Summary

Other Books You May Enjoy

Index

