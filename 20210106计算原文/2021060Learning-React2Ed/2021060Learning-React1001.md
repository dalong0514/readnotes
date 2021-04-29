Chapter 10. React Testing

In order to keep up with our competitors, we must move quickly while ensuring quality. One vital tool that allows us to do this is unit testing.

Unit testing makes it possible to verify that every piece, or unit, of our application functions as intended.1

One benefit of practicing functional techniques is that they lend themselves to writing testable code. Pure functions are naturally testable. Immutability is easily testable. Composing applications out of small functions designed for specific tasks produces testable functions or units of code.

In this section, we'll demonstrate techniques that can be used to unit test React applications. This chapter will not only cover testing, but also tools that can be used to help evaluate and improve your code and your tests.

ESLint

In most programming languages, code needs to be compiled before you can run anything. Programming languages have pretty strict rules about coding style and will not compile until the code is formatted appropriately. JavaScript does not have those rules and does not come with a compiler. We write code, cross our fingers, and run it in the browser to see if it works or not. The good news is that there are tools

we can use to analyze our code and make us stick to specific formatting guidelines.

The process of analyzing JavaScript code is called hinting or linting.

JSHint and JSLint are the original tools used to analyze JavaScript and provide feedback about formatting. ESLint is the latest code linter that supports emerging JavaScript syntax. Additionally, ESLint is pluggable. This means we can create and share plug-ins that can be added to ESLint configurations to extend its capabilities.

ESLint is supported out of the box with Create React App, and we've already seen lint warnings and errors appear in the console.

We'll be working with a plug-in called eslint-plugin-react. This plug-in will analyze our JSX and React syntax in addition to our JavaScript.

Let's install eslint as a dev dependency. We can install eslint with npm:

npm install eslint --save-dev

# or

yarn add eslint --dev

Before we use ESLint, we'll need to define some configuration rules that we can agree to follow. We'll define these in a configuration file that's located in our project root. This file can be formatted as JSON or YAML. YAML is a data serialization formation like JSON but with less syntax, making it a little easier for humans to read.

ESLint comes with a tool that helps us set up configuration. There are several companies that have created ESLint config files that we can use as a starting point, or we can create our own.

We can create an ESLint configuration by running eslint --init and answering some questions about our coding style:

npx eslint --init

How would you like to configure ESLint?

To check syntax and find problems

What type of modules does your project use?

JavaScript modules (import/export)

Which framework does your project use?

React

Does your project use TypeScript?

N

Where does your code run? (Press space to select, a to toggle all, i to invert selection)

Browser

What format do you want your config file to be in?

JSON

Would you like to install them now with npm?

Y

After npx eslint --init runs, three things happen:

1. eslint-plugin-react is installed locally to the

./node_modules folder.

2. These dependencies are automatically added to the

package.json file.

3. A configuration file, .eslintrc.json, is created and added to the

root of our project.

If we open .eslintrc.json, we'll see an object of settings:

{

"env" : {

"browser" : true,

"es6" : true

},

"extends" : [

"eslint:recommended",

"plugin:react/recommended"

],

"globals" : {

"Atomics" : "readonly",

"SharedArrayBuffer" : "readonly"

},

"parserOptions" : {

"ecmaFeatures" : {

"jsx" : true

},

"ecmaVersion" : 2018,

"sourceType" : "module"

},

"plugins" : ["react"],

"rules" : {}

}

Importantly, if we look at the extends key, we'll see that our --init command initalized defaults for eslint and react. This means that we don't have to manually configure all of the rules. Instead, those rules are provided to us.

Let's test our ESLint configuration and these rules by creating a sample.js file:

const gnar = "gnarly";

const info = ({

file = __filename,

dir = __dirname

}) => (

<p>

{dir}: {file}

</p>

);

switch (gnar) {

default:

console.log("gnarly");

break;

}

This file has some issues, but nothing that would cause errors in the browser. Technically, this code works just fine. Let's run ESLint on this file and see what feedback we get based on our customized rules: npx eslint sample.js

3:7 error 'info' is assigned a value but never used no-unused-vars 4:3 error 'file' is missing in props validation react/prop-types 4:10 error 'filename' is not defined no-undef

5:3 error 'dir' is missing in props validation react/prop-types 5:9 error 'dirname' is not defined no-undef

7:3 error 'React' must be in scope when using JSX react/react-in-jsx-scope

✖ 6 problems (6 errors, 0 warnings)

ESLint has performed a static analysis of our code and is reporting some issues based on our configuration choices. There are errors about property validation, and ESLint also complains about __filename and __dirname because it does not automatically include Node.js globals.

And finally, ESLint's default React warnings let us know that React

must be in scope when using JSX.

The command eslint . will lint our entire directory. To do this, we'll most likely require that ESLint ignore some JavaScript files. The

.eslintignore file is where we can add files or directories for ESLint to ignore:

dist/assets/

sample.js

This .eslintignore file tells ESLint to ignore our new sample.js file as well as anything in the dist/assets folder. If we don't ignore the assets folder, ESLint will analyze the client bundle.js file, and it will probably find a lot to complain about in that file.

Let's add a script to our package.json file for running ESLint:

{

"scripts" : {

"lint" : "eslint ."

}

}

Now ESLint can be run any time we want with npm run lint, and it will analyze all of the files in our project except the ones we've ignored.

ESLint Plug-Ins

There are a multitude of plug-ins that can be added to your ESLint configuration to help you as you're writing code. For a React project, you'll definitely want to install eslint-plugin-react-hooks, a plug-

in to enforce the rules of React Hooks. This package was released by the React team to help fix bugs related to Hooks usage.

Start by installing it:

npm install eslint-plugin-react-hooks --save-dev

# OR

yarn add eslint-plugin-react-hooks --dev

Then, open the .eslintrc.json file and add the following:

{

"plugins": [

// ...

"react-hooks"

],

"rules": {

"react-hooks/rules-of-hooks": "error",

"react-hooks/exhaustive-deps": "warn"

}

}

This plug-in will check to ensure that functions that start with the word

「use」(assumed to be a hook) are following the rules of Hooks.

Once this has been added, we'll write some sample code to test the plug-in. Adjust the code in sample.js. Even though this code won't run, we're testing to see if the plug-in is working appropriately: function gnar() {

const [nickname, setNickname] = useState(

"dude"

);

return <h1>gnarly</h1>;

}

Several errors will pop up from this code, but most importantly, there's the error that lets us know we're trying to call useState in a function that isn't a component or a hook:

4:35 error React Hook "useState" is called in function "gnar" that is neither

a React function component nor a custom React Hook function react-hooks/rules-of-hooks

These shoutouts will help us along the way as we learn the ins and outs of working with Hooks.

Another useful ESLint plug-in to incorporate into your projects is eslint-plugin-jsx-a11y. A11y is a numeronym, which means that there are 11 letters between the「a」and the「y」in accessibility. When we consider accessibility, we build tools, websites, and technologies that can be used by people with disabilities.

This plug-in will analyze your code and ensure that it's not breaking any accessibility rules. Accessibility should be an area of focus for all of us, and working with this plug-in will promote good practices when writing accessible React applications.

To install, we'll use npm or yarn again:

npm install eslint-plugin-jsx-a11y

// or

yarn add eslint-plugin-jsx-a11y

Then we'll add to our config, .eslintrc.json:

{

"extends" : [

// ...

"plugin:jsx-a11y/recommended"

],

"plugins" : [

// ...

"jsx-a11y"

]

}

Now let's test it. We'll adjust our sample.js file to include an image tag that has no alt property. In order for an image to pass a lint check, it must have an alt prop or an empty string if the image doesn't affect the user's understanding of the content:

function Image() {

return <img src="/img.png" />;

}

If we run lint again with npm run lint, we'll see that there's a new error that's called by the jsx/a11y plug-in:

5:10 error img elements must have an alt prop, either with meaningful text,

or an empty string for decorative images

There are many other ESLint plug-ins you can use to statically analyze your code, and you could spend weeks tuning your ESLint config to perfection. If you're looking to take yours to the next level, there are many useful resources in the Awesome ESLint repository.

Prettier

Prettier is an opinionated code formatter you can use on a range of

projects. The effect Prettier has had on the day-to-day work of web developers since its release has been pretty incredible. Based on historical records, arguing over syntax filled 87% of an average JavaScript developer's day, but now Prettier handles code formatting and defining the rules around what code syntax should be used per project. The time savings are significant. Also, if you've ever unleashed Prettier on a Markdown table, the quick, crisp formatting that occurs is a pretty incredible sight to behold.

ESLint used to be in charge of code formatting for many projects, but now there's a clear delineation of responsibilities. ESLint handles code-quality concerns. Prettier handles code formatting.

To make Prettier work with ESLint, we'll tinker with the configuration of our project a bit more. You can install Prettier globally to get started:

sudo npm install -g prettier

Now you can use Prettier anywhere on any project.

Configuring Prettier by Project

To add a Prettier configuration file to your project, you can create a

.prettierrc file. This file will describe the project defaults:

{

"semi": true,

"trailingComma": none,

"singleQuote": false,

"printWidth": 80

}

These are our preferred defaults, but of course, choose what makes most sense to you. For more Prettier formatting options, check out

Prettier's documentation.

Let's replace what currently lives in our sample.js file with some code to format:

console.log("Prettier Test")

Now let's try running the Prettier CLI from the Terminal or Command Prompt:

prettier --check "sample.js"

Prettier runs the test and shows us the following message: Code style issues found in the above file(s). Forgot to run

Prettier? To run it from the CLI, we can pass the write flag: prettier --write "sample.js"

Once we do this, we'll see an output of a certain number of milliseconds that it took Prettier to format the file. If we open the file, we'll see that the content has changed based on the defaults supplied in the .prettierrc file. If you're thinking that this process seems laborious and could be sped up, you're right. Let's start automating!

First, we'll integrate ESLint and Prettier by installing a config tool and a plug-in:

npm install eslint-config-prettier eslint-plugin-prettier --save-dev The config (eslint-config-prettier) turns off any ESLint rules that

could conflict with Prettier. The plug-in (eslint-plugin-prettier) integrates Prettier rules into ESLint rules. In other words, when we run our lint script, Prettier will run, too.

We'll incorporate these tools into .eslintrc.json:

{

"extends": [

// ...

"plugin:prettier/recommended"

],

"plugins": [

//,

"prettier"],

"rules": {

// ...

"prettier/prettier": "error"

}

}

Make sure to break some formatting rules in your code to ensure that Prettier is working. For example, in sample.js:

console.log("Prettier Test");

Running the lint command npm run lint will yield the following output:

1:13 error Replacè'Prettier·Test')` with `"Prettier·Test");`

prettier/prettier

All of the errors were found. Now you can run the Prettier write command and sweep the formatting for one file:

prettier --write "sample.js"

Or for all of the JavaScript files in certain folders: prettier --write "src/*.js"

Prettier in VSCode

If you're using VSCode, it's highly recommended that you set up Prettier in your editor. Configuration is fairly quick and will save you a lot of time as you're writing code.

You'll first want to install the VSCode extension for Prettier. Just follow this link and click Install. Once installed, you can run Prettier with Control + Command + P on a Mac or Ctrl + Shift + P on a PC to manually format a file or highlighted bit of code. For even better results, you can format your code on Save. This involves adding some settings to VSCode.

To access these settings, select the Code menu, then Preferences, then Settings. (Or Command + comma on a Mac or Ctrl + comma on a PC, if you're in a hurry.) Then you can click on the small paper icon in the upper right-hand corner to open the VSCode settings as JSON. You'll want to add a few helpful keys here:

{

"editor.formatOnSave" : true

}

Now when you save any file, Prettier will format it based on the

.prettierrc defaults! Pretty killer. You can also search Settings for Prettier options to set up defaults in your editor if you want to enforce formatting, even if your project doesn't contain a .prettierrc config file.

If you're using a different editor, Prettier likely supports that, too. For

instructions specific to other code editors, check out the Editor

Integration section of the docs.

Typechecking for React Applications

When you're working with a larger application, you may want to incorporate typechecking to help pinpoint certain types of bugs. There are three main solutions for typechecking in React apps: the prop-types library, Flow, and TypeScript. In the next section, we'll take a closer look at how you might set up these tools to increase code quality.

PropTypes

In the first edition of this book, PropTypes were part of the core React library and were the recommended way to add typechecking to your application. Today, due to the emergence of other solutions like Flow and TypeScript, the functionality has been moved to its own library to make React's bundle size smaller. Still, PropTypes are a widely used solution.

To add PropTypes to your app, install the prop-types library: npm install prop-types --save-dev

We'll test this by creating a minimal App component that renders the name of a library:

import React from "react";

import ReactDOM from "react-dom";

function App({ name }) {

return (

<div>

<h1>{name}</h1>

</div>

);

}

ReactDOM.render(

<App name="React" />,

document.getElementById("root")

);

Then we'll import the prop-types library and use App.propTypes to define which type each property should be:

import PropTypes from "prop-types";

function App({ name }) {

return (

<div>

<h1>{name}</h1>

</div>

);

}

App.propTypes = {

name: PropTypes.string

};

The App component has one property name and should always be a string. If an incorrect type value is passed as the name, an error will be thrown. For example, if we used a boolean:

ReactDOM.render(

<App name="React" />,

document.getElementById("root")

);

Our console would report a problem back to us:

Warning: Failed prop type: Invalid prop name of type boolean supplied to App,

expected string. in App

When a value of an incorrect type is provided for a property, the warning only appears in development mode. The warnings and broken renders won't appear in production.

Other types are available, of course, when validating properties. We could add a boolean for whether or not a technology was used at a company:

function App({ name, using }) {

return (

<div>

<h1>{name}</h1>

<p>

{using ? "used here" : "not used here"}

</p>

</div>

);

}

App.propTypes = {

name: PropTypes.string,

using: PropTypes.bool

};

ReactDOM.render(

<App name="React" using={true} />, document.getElementById("root")

);

The longer list of type checks includes: PropTypes.array

PropTypes.object

PropTypes.bool

PropTypes.func

PropTypes.number

PropTypes.string

PropTypes.symbol

Additionally, if you want to ensure that a value was provided, you can chain .isRequired onto the end of any of these options. For example, if a string must be supplied, you'd use:

App.propTypes = {

name: PropTypes.string.isRequired

};

ReactDOM.render(

<App />,

document.getElementById("root")

);

Then, if you fail to provide a value for this field, the following warning will appear in the console:

index.js:1 Warning: Failed prop type: The prop name is marked as required in App,

but its value is undefined.

There also may be situations where you don't care what the value is, as long as a value is provided. In that case, you can use any. For example:

App.propTypes = {

name: PropTypes.any.isRequired

};

This means that a boolean, string, number––anything––could be supplied. As long as name is not undefined, the typecheck will succeed.

In addition to the basic typechecks, there are a few other utilities that are useful for many real-world situations. Consider a component where there are two status options: Open and Closed:

function App({ status }) {

return (

<div>

<h1>

We're {status === "Open" ? "Open!" : "Closed!"}

</h1>

</div>

);

}

ReactDOM.render(

<App status="Open" />,

document.getElementById("root")

);

Status is a string, so we might be inclined to use the string check: App.propTypes = {

status: PropTypes.string.isRequired

};

That works well, but if other string values besides Open and Closed are passed in, the property will be validated. The type of check we actually

want to enforce is an enum check. An enumeration type is a restricted list of options for a particular field or property. We'll adjust the propTypes object like so:

App.propTypes = {

status: PropTypes.oneOf(["Open", "Closed"])

};

Now if anything other than the values from the array that's passed to PropTypes.oneOf is supplied, a warning will appear.

For all the options you can configure for PropTypes in your React app, check out the documentation.

Flow

Flow is a typechecking library that's used and maintained by Facebook Open Source. It's a tool that checks for errors via static type annotations. In other words, if you create a variable that's a particular type, Flow will check to be sure that that value used is the correct type.

Let's fire up a Create React App project:

npx create-react-app in-the-flow

Then we'll add Flow to the project. Create React App doesn't assume you want to use Flow, so it doesn't ship with the library, but it's smooth to incorporate:

npm install --save flow-bin

Once installed, we'll add an npm script to run Flow when we type npm

run flow. In package.json, just add this to the scripts key:

{

"scripts" : {

"start" : "react-scripts start",

"build" : "react-scripts build",

"test" : "react-scripts test",

"eject" : "react-scripts eject",

"flow" : "flow"

}

}

Now running the flow command will run typechecking on our files.

Before we can use it, though, we need to create a .flowconfig file. To do so, we run:

npm run flow init

This creates a skeleton of a configuration file that looks like this:

[ignore]

[include]

[libs]

[lints]

[options]

[strict]

In most cases, you'll leave this blank to use Flow's defaults. If you want to configure Flow beyond the basics, you can explore more options in the documentation.

One of the coolest features of Flow is that you can adopt Flow

incrementally. It can feel overwhelming to have to add typechecking to an entire project. With Flow, this isn't a requirement. All you need to do is add the line //@flow to the top of any files you want to typecheck, then Flow will automatically only check those files.

Another option is to add the VSCode extension for Flow to help with code completion and parameter hints. If you have Prettier or a linting tool set up, this will help your editor handle the unexpected syntax of Flow. You can find that in the marketplace.

Let's open the index.js file and, for the sake of simplicity, keep everything in the same file. Make sure to add //@flow to the top of the file:

//@flow

import React from "react";

import ReactDOM from "react-dom";

function App(props) {

return (

<div>

<h1>{props.item}</h1>

</div>

);

}

ReactDOM.render(

<App item="jacket" />,

document.getElementById("root")

);

Now we'll define the types for the properties:

type Props = {

item: string

};

function App(props: Props) {

//...

}

Then run Flow npm run flow. In certain versions of Flow, you may see this warning:

Cannot call ReactDOM.render with root bound to container because null [1]

is

incompatible with Element [2]

This warning exists because if document.getElementById("root") returns null, the app will crash. To safeguard against this (and to clear the error), we can do one of two things. The first approach is to use an if statement to check to see that root is not null:

const root = document.getElementById("root"); if (root !== null) {

ReactDOM.render(<App item="jacket" />, root);

}

Another option is to add a typecheck to the root constant using Flow syntax:

const root = document.getElementById("root"); ReactDOM.render(<App item="jacket" />, root); In either case, you'll clear the error and see that your code is free of errors!

No errors!

We could trust this fully, but trying to break it feels like a good idea.

Let's pass a different property type to the app:

ReactDOM.render(<App item={3} />, root);

Cool, we broke it! Now we get an error that reads:

Cannot create App element because number [1] is incompatible with string

[2]

in property item.

Let's switch it back and add another property for a number. We'll also adjust the component and property definitions:

type Props = {

item: string,

cost: number

};

function App(props: Props) {

return (

<div>

<h1>{props.item}</h1>

<p>Cost: {props.cost}</p>

</div>

);

}

ReactDOM.render(

<App item="jacket" cost={249} />,

root

);

Running this works, but what if we removed the cost value?

ReactDOM.render(<App item="jacket" />, root); We'll immediately get an error:

Cannot create App element because property cost is missing in props [1]

but

exists in Props [2].

If cost is truly not a required value, we can make it optional in the property definitions using the question mark after the property name, cost?:

type Props = {

item: string,

cost?: number

};

If we run it again, we don't see the error.

That's the tip of the iceberg with all of the different features that Flow has to offer. To learn more and to stay on top of the changes in the library, head over to the documentation site.

TypeScript

TypeScript is another popular tool for typechecking in React applications. It's an open source superset of JavaScript, which means that it adds additional features to the language. Created at Microsoft, TypeScript is designed to be used for large apps to help developers find bugs and iterate more quickly on projects.

TypeScript has a growing allegiance of supporters, so the tooling in the ecosystem continues to improve. One tool that we're already familiar

with is Create React App, which has a TypeScript template we can use.

Let's set up some basic typechecking, similar to what we did with PropTypes and Flow, to get a sense of how we can start using it in our own apps.

We'll start by generating yet another Create React App, this time with some different flags:

npx create-react-app my-type --template typescript

Now let's tour the features of our scaffolded project. Notice in the src directory that the file extensions are .ts or .tsx now. We'll also find a

.tsconfig.json file, which contains all of our TypeScript settings. More on that in a bit.

Also, if you take a look at the package.json file, there are new dependencies listed and installed related to TypeScript, like the library itself and type definitions for Jest, React, ReactDOM, and more. Any dependency that starts with @types/ describes the type definitions for a library. That means that the functions and methods in the library are typed so that we don't have to describe all of the library's types.

NOTE

If your project doesn't include the TypeScript features, you might be using an old version of Create React App. To get rid of this, you can run npm uninstall -g create-react-app.

Let's try dropping our component from the Flow lesson into our

project. Just add the following to the index.ts file: import React from "react";

import ReactDOM from "react-dom";

function App(props) {

return (

<div>

<h1>{props.item}</h1>

</div>

);

}

ReactDOM.render(

<App item="jacket" />,

document.getElementById("root")

);

If we run the project with npm start, we should see our first TypeScript error. This is to be expected at this point:

Parameter 'props' implicitly has an 'any' type.

This means we need to add type rules for this App component. We'll start by defining types just as we did earlier for the Flow component.

The item is a string, so we'll add that to the AppProps type: type AppProps = {

item: string;

};

ReactDOM.render(

<App item="jacket" />,

document.getElementById("root")

);

Then we'll reference AppProps in the component:

function App(props: AppProps) {

return (

<div>

<h1>{props.item}</h1>

</div>

);

}

Now the component will render with no TypeScript issues. It's also possible to destructure props if we'd like to:

function App({ item }: AppProps) {

return (

<div>

<h1>{item}</h1>

</div>

);

}

We can break this by passing a value of a different type as the item property:

ReactDOM.render(

<App item={1} />,

document.getElementById("root")

);

This immediately triggers an error:

Type 'number' is not assignable to type 'string'.

The error also tells us the exact line where there's a problem. This is extremely useful as we're debugging.

TypeScript helps with more than just property validation, though. We

can use TypeScript's type inference to help us do typechecking on hook values.

Consider a state value for a fabricColor with an initial state of purple. The component might look like this:

type AppProps = {

item: string;

};

function App({ item }: AppProps) {

const [fabricColor, setFabricColor] = useState(

"purple"

);

return (

<div>

<h1>

{fabricColor} {item}

</h1>

<button

onClick={() => setFabricColor("blue")}

>

Make the Jacket Blue

</button>

</div>

);

}

Notice that we haven't added anything to the type definitions object.

Instead, TypeScript is inferring that the type for the fabricColor should match the type of its initial state. If we try setting the fabricColor with a number instead of another string color blue, an error will be thrown:

<button onClick={() => setFabricColor(3)}>

The error looks like this:

Argument of type '3' is not assignable to parameter of type string.

TypeScript is hooking us up with some pretty low-effort typechecking for this value. Of course, you can customize this further, but this should give you a start toward adding typechecking to your applications.

For more on TypeScript, check out the official docs and the amazing

React+TypeScript Cheatsheets on GitHub.

Test-Driven Development

Test-driven development, or TDD, is a practice—not a technology. It does not mean that you simply have tests for your application. Rather, it's the practice of letting the tests drive the development process. In order to practice TDD, you should follow these steps:

Write the tests first

This is the most critical step. You declare what you're building and how it should work first in a test. The steps you'll use to test are red, green, and gold.

Run the tests and watch them fail (red)

Run the tests and watch them fail before you write the code.

Write the minimal amount of code required to make the tests pass (green)

Focus specifically on making each test pass; do not add any functionality beyond the scope of the test.

Refactor both the code and the tests (gold) Once the tests pass, it's time to take a closer look at your code and your tests. Try to express your code as simply and as beautifully as possible.2

TDD gives us an excellent way to approach a React application, particularly when testing Hooks. It's typically easier to think about how a Hook should work before actually writing it. Practicing TDD

will allow you to build and certify the entire data structure for a feature or application independent of the UI.

TDD and Learning

If you're new to TDD, or new to the language you're testing, you may find it challenging to write a test before writing code. This is to be expected, and it's OK to write the code before the test until you get the hang of it. Try to work in small batches: a little bit of code, a few tests, and so on. Once you get used to writing tests, it will be easier to write the tests first.

For the remainder of this chapter, we'll be writing tests for code that already exists. Technically, we're not practicing TDD. However, in the next section, we'll pretend that our code does not already exist so we can get a feel for the TDD workflow.

Incorporating Jest

Before we can get started writing tests, we'll need to select a testing framework. You can write tests for React with any JavaScript testing

framework, but the official React docs recommend testing with Jest, a JavaScript test runner that lets you access the DOM via JSDOM.

Accessing the DOM is important because you want to be able to check what is rendered with React to ensure your application is working correctly.

Create React App and Testing

Projects that have been initialized with Create React App already come with the jest package installed. We can create another Create React App project to get started, or use an existing one:

npx create-react-app testing

Now we can start thinking about testing with a small example. We'll create two new files in the src folder: functions.js and functions.test.js.

Remember, Jest is already configured and installed in Create React App, so all you need to do is start writing tests. In functions.test.js, we'll stub the tests. In other words, we'll write what we think the function should do.

We want our function to take in a value, multiply it by two, and return it. So we'll model that in the test. The test function is the function that Jest provides to test a single piece of functionality:

functions.test.js

test("Multiplies by two", () => {

expect();

});

The first argument, Multiplies by two, is the test name. The second argument is the function that contains what should be tested and the third (optional) argument specifies a timeout. The default timeout is five seconds.

The next thing we'll do is stub the function that will multiply numbers by two. This function will be referred to as our system under test ( SUT). In functions.js, create the function: export default function timesTwo() {...}

We'll export it so that we can use the SUT in the test. In the test file, we want to import the function, and we'll use expect to write an assertion. In the assertion, we'll say that if we pass 4 to the timesTwo function, we expect that it should return 8:

import { timesTwo } from "./functions";

test("Multiplies by two", () => {

expect(timesTwo(4)).toBe(8);

});

Jest「matchers」are returned by the expect function and used to verify results. To test the function, we'll use the .toBe matcher. This verifies that the resulting object matches the argument sent to .toBe.

Let's run the tests and watch them fail using npm test or npm run test. Jest will provide specific details on each failure, including a stack trace:

FAIL src/functions.test.js

✕ Multiplies by two (5ms)

● Multiplies by two

expect(received).toBe(expected) // Object.is equality

Expected: 8

Received: undefined

2 |

3 | test("Multiplies by two", () => {

> 4 | expect(timesTwo(4)).toBe(8);

| ^

5 | });

6 |

at Object.<anonymous> (src/functions.test.js:4:23)

Test Suites: 1 failed, 1 total

Tests: 1 failed, 1 total

Snapshots: 0 total

Time: 1.048s

Ran all test suites related to changed files.

Taking the time to write the tests and run them to watch them fail shows us that our tests are working as intended. This failure feedback represents our to-do list. It's our job to write the minimal code required to make our tests pass.

Now if we add the proper functionality to the functions.js file, we can make the tests pass:

export function timesTwo(a) {

return a * 2;

}

The .toBe matcher has helped us test for equality with a single value.

If we want to test an object or array, we could use .toEqual. Let's go through another cycle with our tests. In the test file, we'll test for equality of an array of objects.

We have a list of menu items from the Guy Fieri restaurant in Las Vegas. It's important that we build an object of their ordered items so the customer can get what they want and know what they're supposed to pay. We'll stub the test first:

test("Build an order object", () => {

expect();

});

Then we'll stub our function:

export function order(items) {

// ...

}

Now we'll use the order function in the test file. We'll also assume that we have a starter list of data for an order that we need to transform: import { timesTwo, order } from "./functions"; const menuItems = [

{

id: "1",

name: "Tatted Up Turkey Burger",

price: 19.5

},

{

id: "2",

name: "Lobster Lollipops",

price: 16.5

},

{

id: "3",

name: "Motley Que Pulled Pork Sandwich",

price: 21.5

},

{

id: "4",

name: "Trash Can Nachos",

price: 19.5

}

];

test("Build an order object", () => {

expect(order(menuItems));

});

Remember that we'll use toEqual because we're checking the value of an object instead of an array. What do we want the result to equal?

Well, we want to create an object that looks like this:

const result = {

orderItems: menuItems,

total: 77

};

So we just add that to the test and use it in the assertion: test("Build an order object", () => {

const result = {

orderItems: menuItems,

total: 77

};

expect(order(menuItems)).toEqual(result);

});

Now we'll complete the function in the functions.js file: export function order(items) {

const total = items.reduce(

(price, item) => price + item.price,

0

);

return {

orderItems: items,

total

};

}

And when we check out the terminal, we'll find that are tests are now passing! Now this might feel like a trivial example, but if you were fetching data, it's likely that you'd test for shape matches of arrays and objects.

Another commonly used function with Jest is describe(). If you've used other testing libraries, you might have seen a similar function before. This function is typically used to wrap several related tests. For example, if we had a few tests for similar functions, we could wrap them in a describe statement:

describe("Math functions", () => {

test("Multiplies by two", () => {

expect(timesTwo(4)).toBe(8);

});

test("Adds two numbers", () => {

expect(sum(4, 2)).toBe(6);

});

test("Subtracts two numbers", () => {

expect(subtract(4, 2)).toBe(2);

});

});

When you wrap tests in the describe statement, the test runner creates a block of tests, which makes the testing output in the terminal look more organized and easier to read:

Math functions

✓ Multiplies by two

✓ Adds two numbers

✓ Subtracts two numbers (1ms)

As you write more tests, grouping them in describe blocks might be a useful enhancement.

This process represents a typical TDD cycle. We wrote the tests first, then wrote code to make the tests pass. Once the tests pass, we can take a closer look at the code to see if there's anything that's worth refactoring for clarity or performance. This approach is very effective when working with JavaScript (or really any other language).

Testing React Components

Now that we have a basic understanding of the process behind writing tests, we can start to apply these techniques to component testing in React.

React components provide instructions for React to follow when creating and managing updates to the DOM. We can test these components by rendering them and checking the resulting DOM.

We're not running our tests in a browser; we're running them in the terminal with Node.js. Node.js does not have the DOM API that comes standard with each browser. Jest incorporates an npm package called jsdom that's used to simulate a browser environment in Node.js, which is essential for testing React components.

For each component test, it's likely that we'll need to render our React

component tree to a DOM element. To demonstrate this workflow, let's revisit our Star component in Star.js:

import { FaStar } from "react-icons/fa"; export default function Star({ selected = false }) {

return (

<FaStar color={selected ? "red" : "grey"} id="star" />

);

}

Then in index.js, we'll import and render the star: import Star from "./Star";

ReactDOM.render(

<Star />,

document.getElementById("root")

);

Now let's write our test. We already wrote the code for the star, so we won't be partaking in TDD here. If you had to incorporate tests into your existing apps, this is how you'd do it. In a new file called Star.test.js, start by importing React, ReactDOM, and the Star: import React from "react";

import ReactDOM from "react-dom";

import Star from "./Star";

test("renders a star", () => {

const div = document.createElement("div"); ReactDOM.render(<Star />, div);

});

We'll also want to write the tests. Remember, the first argument we

supply to test is the name of the test. Then we're going to perform some setup by creating a div that we can render the star to with ReactDOM.render. Once the element is created, we can write the assertion:

test("renders a star", () => {

const div = document.createElement("div"); ReactDOM.render(<Star />, div);

expect(div.querySelector("svg")).toBeTruthy();

});

We'll expect that if we try to select an svg element inside of the created div, the result will be truthy. When we run the test, we should see that the test passes. Just to verify that we aren't getting a valid assertion when we shouldn't be, we can change the selector to find something fake and watch the test fail:

expect(

div.querySelector("notrealthing")

).toBeTruthy();

The documentation provides more detail about all of the custom matchers that are available so that you can test exactly what you want to test.

When you generated your React project, you may have noticed that a few packages from @testing-library were installed in addition to the basics like React and ReactDOM. React Testing Library is a project that was started by Kent C. Dodds as a way to enforce good testing practices and to expand the testing utilities that were part of the React ecosystem. Testing Library is an umbrella over many testing packages

for libraries like Vue, Svelte, Reason, Angular, and more—it's not just for React.

One potential reason you might choose React Testing Library is to get better error messages when a test fails. The current error we see when we test the assertion:

expect(

div.querySelector("notrealthing")

).toBeTruthy();

is:

expect(received).toBeTruthy()

Received: null

Let's punch this up by adding React Testing Library. It's already installed in our Create React App project. To begin, we'll import the toHaveAttribute function from @testing-library/jest-dom:

import { toHaveAttribute } from "@testing-library/jest-dom"; From there, we want to extend the functionality of expect to include this function:

expect.extend({ toHaveAttribute });

Now instead of using toBeTruthy, which gives us hard-to-read messages, we can use toHaveAttribute:

test("renders a star", () => {

const div = document.createElement("div");

ReactDOM.render(<Star />, div);

expect(

div.querySelector("svg")

).toHaveAttribute("id", "hotdog");

});

Now when we run the tests, we see an error telling us exactly what's what:

expect(element).toHaveAttribute("id", "hotdog")

// element.getAttribute("id") === "hotdog"

Expected the element to have attribute:

id="hotdog"

Received:

id="star"

It should be pretty straightforward to fix this now:

expect(div.querySelector("svg")).toHaveAttribute(

"id",

"star"

);

Using more than one of the custom matchers just means that you need to import, extend, and use:

import {

toHaveAttribute,

toHaveClass

} from "@testing-library/jest-dom";

expect.extend({ toHaveAttribute, toHaveClass });

expect(you).toHaveClass("evenALittle");

There's an even faster way to do this, though. If you find yourself

importing too many of these matchers to list or keep track of, you can import the extend-expect library:

import "@testing-library/jest-dom/extend-expect";

// Remove this --> expect.extend({ toHaveAttribute, toHaveClass }); The assertions will continue to run as expected (pun intended). Another fun fact about Create React App is that, in a file called setupTests.js that ships with CRA, there's a line that has already included the extend-expect helpers. If you look at the src folder, you'll see that setupTests.js contains:

// jest-dom adds custom jest matchers for asserting on DOM nodes.

// allows you to do things like:

// expect(element).toHaveTextContent(/react/i)

// learn more: https://github.com/testing-library/jest-dom import "@testing-library/jest-dom/extend-expect"; So if you're using Create React App, you don't even have to include the import in your test files.

Queries

Queries are another feature of the React Testing Library that allow you to match based on certain criteria. In order to demonstrate using a query, let's adjust the Star component to include a title. This will allow us to write a common style of test—one that matches based on text:

export default function Star({ selected = false }) {

return (

<>

<h1>Great Star</h1>

<FaStar

id="star"

color={selected ? "red" : "grey"}

/>

</>

);

}

Let's pause to think about what we're trying to test. We want the component to render, and now we want to test to see if the h1 contains the correct text. A function that's part of React Testing Library, render, will help us do just that. render will replace our need to use ReactDOM.render(), so the test will look a bit different. Start by importing render from React Testing Library:

import { render } from "@testing-library/react"; render will take in one argument: the component or element that we want to render. The function returns an object of queries that can be used to check in with values in that component or element. The query we'll use is getByText, which will find the first matching node for a query and throw an error if no elements match. To return a list of all matching nodes, use getAllBy to return an array:

test("renders an h1", () => {

const { getByText } = render(<Star />);

const h1 = getByText(/Great Star/);

expect(h1).toHaveTextContent("Great Star");

});

getByText finds the h1 element via the regular expression that's passed to it. Then we use the Jest matcher toHaveTextContent to describe what text the h1 should include.

Run the tests, and they'll pass. If we change the text passed to the toHaveTextContent() function, the test will fail.

Testing Events

Another important part of writing tests is testing events that are part of components. Let's use and test the Checkbox component we created in

Chapter 7:

export function Checkbox() {

const [checked, setChecked] = useReducer(

checked => !checked,

false

);

return (

<>

<label>

{checked ? "checked" : "not checked"}

<input

type="checkbox"

value={checked}

onChange={setChecked}

/>

</label>

</>

);

}

This component uses useReducer to toggle a checkbox. Our aim here is to create an automated test that will click this checkbox and change the value of checked from the default false to true. Writing a test to check the box will also fire useReducer and test the hook.

Let's stub the test:

import React from "react"; test("Selecting the checkbox should change the value of checked to true", () => {

// .. write a test

});

The first thing we need to do is select the element that we want to fire the event on. In other words, which element do we want to click on with the automated test? We'll use one of Testing Library's queries to find the element we're looking for. Since the input has a label, we can use getByLabelText():

import { render } from "@testing-library/react"; import { Checkbox } from "./Checkbox";

test("Selecting the checkbox should change the value of checked to true", () => {

const { getByLabelText } = render(<Checkbox />);

});

When the component first renders, its label text reads not checked, so we can search via a regular expression to find a match with the string: test("Selecting the checkbox should change the value of checked to true", () => {

const { getByLabelText } = render(<Checkbox />); const checkbox = getByLabelText(/not checked/);

});

Currently, this regex is case sensitive, so if you wanted to search for any case, you could add an i to the end of it. Use that technique with caution depending on how permissive you want the query selection to be:

const checkbox = getByLabelText(/not checked/i); Now we have our checkbox selected. All we need to do now is fire the event (click the checkbox) and write an assertion to make sure that the checked property is set to true when the checkbox is clicked: mport { render, fireEvent } from "@testing-library/react"

test("Selecting the checkbox should change the value of checked to true", () => {

const { getByLabelText } = render(<Checkbox />); const checkbox = getByLabelText(/not checked/i);

fireEvent.click(checkbox);

expect(checkbox.checked).toEqual(true);

});

You also could add the reverse toggle to this checkbox test by firing the event again and checking that the property is set to false on toggle. We changed the name of the test to be more accurate: test("Selecting the checkbox should toggle its value", () => {

const { getByLabelText } = render(<Checkbox />); const checkbox = getByLabelText(/not checked/i);

fireEvent.click(checkbox);

expect(checkbox.checked).toEqual(true);

fireEvent.click(checkbox);

expect(checkbox.checked).toEqual(false);

});

In this case, selecting the checkbox is pretty easy. We have a label we can use to find the input we want to check. In the event that you don't have such an easy way to access a DOM element, Testing Library gives you another utility you can use to check in with any DOM

element. You'll start by adding an attribute to the element you want to

select:

<input

type="checkbox"

value={checked}

onChange={setChecked}

data-testid="checkbox" // Add the data-testid= attribute

/>

Then use the query getByTestId:

test("Selecting the checkbox should change the value of checked to true", () => {

const { getByTestId } = render(<Checkbox />); const checkbox = getByTestId("checkbox"); fireEvent.click(checkbox);

expect(checkbox.checked).toEqual(true);

});

This will do the same thing but is particularly useful when reaching out to DOM elements that are otherwise difficult to access.

Once this Checkbox component is tested, we can confidently incorporate it into the rest of the application and reuse it.

Using Code Coverage

Code coverage is the process of reporting on how many lines of code have actually been tested. It provides a metric that can help you decide when you've written enough tests.

Jest ships with Istanbul, a JavaScript tool used to review your tests and generate a report that describes how many statements, branches, functions, and lines have been covered.

To run Jest with code coverage, simply add the coverage flag when you run the jest command:

npm test -- --coverage

This report tells you how much of your code in each file has been executed during the testing process and reports on all files that have been imported into tests.

Jest also generates a report that you can run in your browser, which provides more details about what code has been covered by tests. After running Jest with coverage reporting, you'll notice that a coverage folder has been added to the root. In a web browser, open this file:

/coverage/lcov-report/index.html. It will show you your code coverage in an interactive report.

This report tells you how much of the code has been covered, as well as the individual coverage based on each subfolder. You can drill down into a subfolder to see how well the individual files within have been covered. If you select the components/ui folder, you'll see how well your user interface components are covered by testing.

You can see which lines have been covered in an individual file by clicking on the filename.

Code coverage is a great tool to measure the reach of your tests. It's one benchmark to help you understand when you've written enough unit tests for your code. It's not typical to have 100% code coverage in every project. Shooting for anything above 85% is a good target.3

Testing can often feel like an extra step, but the tooling around React testing has never been better. Even if you don't test all of your code, starting to think about how to incorporate testing practices can help you save time and money when building production-ready applications.

For a brief introduction to unit testing, see Martin Fowler's article,「Unit Testing」.

1

For more on this development pattern, see Jeff McWherter's and James Bender's「Red,

2 Green, Refactor」.

See Martin Fowler's article,「Test-Coverage」.

3

