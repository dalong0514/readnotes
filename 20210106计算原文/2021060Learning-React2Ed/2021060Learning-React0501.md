Chapter 5. React with JSX

In the last chapter, we dove deep into how React works, breaking down our React applications into small reusable pieces called components.

These components render trees of elements and other components.

Using the createElement function is a good way to see how React works, but as React developers, that's not what we do. We don't go around composing complex, barely readable trees of JavaScript syntax and call it fun. In order to work efficiently with React, we need one more thing: JSX.

JSX combines the JS from JavaScript and the X from XML. It is a JavaScript extension that allows us to define React elements using a tag-based syntax directly within our JavaScript code. Sometimes JSX

is confused with HTML because they look similar. JSX is just another way of creating React elements, so you don't have to pull your hair out looking for the missing comma in a complex createElement call.

In this chapter, we're going to discuss how to use JSX to construct a React application.

React Elements as JSX

Facebook's React team released JSX when they released React to provide a concise syntax for creating complex DOM trees with attributes. They also hoped to make React more readable like HTML

and XML. In JSX, an element's type is specified with a tag. The tag's attributes represent the properties. The element's children can be added between the opening and closing tags.

You can also add other JSX elements as children. If you have an unordered list, you can add child list item elements to it with JSX tags.

It looks very similar to HTML:

<ul>

<li> 1 lb Salmon</li>

<li> 1 cup Pine Nuts</li>

<li> 2 cups Butter Lettuce</li>

<li> 1 Yellow Squash</li>

<li> 1/2 cup Olive Oil</li>

<li> 3 Cloves of Garlic</li>

</ul>

JSX works with components as well. Simply define the component using the class name. We pass an array of ingredients to the IngredientsList as a property with JSX, as shown in Figure 5-1.

Figure 5-1. Creating the IngredientsList with JSX

When we pass the array of ingredients to this component, we need to surround it with curly braces. This is called a JavaScript expression, and we must use these when passing JavaScript values to components

as properties. Component properties will take two types: either a string or a JavaScript expression. JavaScript expressions can include arrays, objects, and even functions. In order to include them, you must surround them in curly braces.

JSX Tips

JSX might look familiar, and most of the rules result in syntax that's similar to HTML. However, there are a few considerations you should understand when working with JSX.

NESTED COMPONENTS

JSX allows you to add components as children of other components.

For example, inside the IngredientsList, we can render another component called Ingredient multiple times:

<IngredientsList>

<Ingredient />

<Ingredient />

<Ingredient />

</IngredientsList>

CLASSNAME

Since class is a reserved word in JavaScript, className is used to define the class attribute instead:

<h1 className="fancy" > Baked Salmon</h1> JAVASCRIPT EXPRESSIONS

JavaScript expressions are wrapped in curly braces and indicate where variables will be evaluated and their resulting values returned. For

example, if we want to display the value of the title property in an element, we can insert that value using a JavaScript expression. The variable will be evaluated and its value returned:

<h1>{title}</h1>

Values of types other than string should also appear as JavaScript expressions:

<input type="checkbox" defaultChecked={false} /> EVALUATION

The JavaScript that's added in between the curly braces will get evaluated. This means that operations such as concatenation or addition will occur. This also means that functions found in JavaScript expressions will be invoked:

<h1> {"Hello" + title}</h1>

<h1> {title.toLowerCase().replace}</h1> Mapping Arrays with JSX

JSX is JavaScript, so you can incorporate JSX directly inside of JavaScript functions. For example, you can map an array to JSX

elements:

<ul>

{props.ingredients.map((ingredient, i) => (

<li key="{i}">{ingredient}</li>

))}

</ul>

JSX looks clean and readable, but it can't be interpreted with a browser. All JSX must be converted into createElement calls.

Luckily, there's an excellent tool for this task: Babel.

Babel

Many software languages require you to compile your source code.

JavaScript is an interpreted language: the browser interprets the code as text, so there's no need to compile JavaScript. However, not all browsers support the latest JavaScript syntax, and no browser supports JSX syntax. Since we want to use the latest features of JavaScript along with JSX, we're going to need a way to convert our fancy source code into something that the browser can interpret. This process is called compiling, and it's what Babel is designed to do.

The first version of the project was called 6to5, and it was released in September 2014. 6to5 was a tool that could be used to convert ES6

syntax to ES5 syntax, which was more widely supported by web browsers. As the project grew, it aimed to be a platform to support all of the latest changes in ECMAScript. It also grew to support converting JSX into JavaScript. The project was renamed Babel in February 2015.

Babel is used in production at Facebook, Netflix, PayPal, Airbnb, and more. Previously, Facebook had created a JSX transformer that was their standard, but it was soon retired in favor of Babel.

There are many ways of working with Babel. The easiest way to get started is to include a link to the Babel CDN directly in your HTML,

which will compile any code in script blocks that have a type of

「text/babel.」Babel will compile the source code on the client before running it. Although this may not be the best solution for production, it's a great way to get started with JSX:

<!DOCTYPE html>

<html>

<head>

<meta charset="utf-8" />

<title> React Examples</title>

</head>

<body>

<div id="root" ></div>

<!-- React Library & React DOM -->

<script

src="https://unpkg.com/react@16.8.6/umd/react.development.js" >

</script>

<script

src="https://unpkg.com/react-dom@16.8.6/umd/react-dom.development.js" >

</script>

<script

src="https://unpkg.com/@babel/standalone/babel.min.js" >

</script>

<script type="text/babel" >

// JSX code here. Or link to separate JavaScript file that contains JSX.

</script>

</body>

</html>

CONSOLE WARNING IN THE BROWSER WITH

IN-BROWSER BABEL

When using the in-browser transformer, you'll see a warning that says to precompile scripts for production. Don't worry about that warning for the purposes of this and any other small demos. We'll upgrade to production-ready Babel later in the chapter.

Recipes as JSX

JSX provides us with a nice, clean way to express React elements in our code that makes sense to us and is immediately readable by developers. The drawback of JSX is that it's not readable by the browser. Before our code can be interpreted by the browser, it needs to be converted from JSX into JavaScript.

This data array contains two recipes, and this represents our application's current state:

const data = [

{

name: "Baked Salmon",

ingredients: [

{ name: "Salmon", amount: 1, measurement: "l lb" },

{ name: "Pine Nuts", amount: 1, measurement: "cup" },

{ name: "Butter Lettuce", amount: 2, measurement: "cups" },

{ name: "Yellow Squash", amount: 1, measurement: "med" },

{ name: "Olive Oil", amount: 0.5, measurement: "cup" },

{ name: "Garlic", amount: 3, measurement: "cloves" }

],

steps: [

"Preheat the oven to 350 degrees.",

"Spread the olive oil around a glass baking dish.",

"Add the yellow squash and place in the oven for 30 mins.",

"Add the salmon, garlic, and pine nuts to the dish.",

"Bake for 15 minutes.",

"Remove from oven. Add the lettuce and serve."

]

},

{

name: "Fish Tacos",

ingredients: [

{ name: "Whitefish", amount: 1, measurement: "l lb" },

{ name: "Cheese", amount: 1, measurement: "cup" },

{ name: "Iceberg Lettuce", amount: 2, measurement: "cups" },

{ name: "Tomatoes", amount: 2, measurement: "large" },

{ name: "Tortillas", amount: 3, measurement: "med" }

],

steps: [

"Cook the fish on the grill until cooked through.",

"Place the fish on the 3 tortillas.",

"Top them with lettuce, tomatoes, and cheese."

]

}

];

The data is expressed in an array of two JavaScript objects. Each object contains the name of the recipe, a list of the ingredients required, and a list of steps necessary to cook the recipe.

We can create a UI for these recipes with two components: a Menu component for listing the recipes and a Recipe component that describes the UI for each recipe. It's the Menu component that we'll render to the DOM. We'll pass our data to the Menu component as a property called recipes:

// The data, an array of Recipe objects

const data = [ ... ];

// A function component for an individual Recipe

function Recipe (props) {

...

}

// A function component for the Menu of Recipes

function Menu (props) {

...

}

// A call to ReactDOM.render to render our Menu into the current DOM

ReactDOM.render(

<Menu recipes={data} title="Delicious Recipes" />, document.getElementById("root")

);

The React elements within the Menu component are expressed as JSX.

Everything is contained within an article element. A header element, an h1 element, and a div.recipes element are used to describe the DOM for our menu. The value for the title property will be displayed as text within the h1:

function Menu(props) {

return (

<article>

<header>

<h1>{props.title}</h1>

</header>

<div className="recipes" />

</article>

);

}

Inside of the div.recipes element, we add a component for each recipe:

<div className="recipes">

{props.recipes.map((recipe, i) => (

<Recipe

key={i}

name={recipe.name}

ingredients={recipe.ingredients}

steps={recipe.steps}

/>

))}

</div>

In order to list the recipes within the div.recipes element, we use

curly braces to add a JavaScript expression that will return an array of children. We can use the map function on the props.recipes array to return a component for each object within the array. As mentioned previously, each recipe contains a name, some ingredients, and cooking instructions (steps). We'll need to pass this data to each Recipe as props. Also remember that we should use the key property to uniquely identify each element.

You could also refactor this to use spread syntax. The JSX spread operator works like the object spread operator. It will add each field of the recipe object as a property of the Recipe component. The syntax here will supply all properties to the component:

{

props.recipes.map((recipe, i) => <Recipe key={i} {...recipe} />);

}

Remember that this shortcut will provide all the properties to the Recipe component. This could be a good thing but might also add too many properties to the component.

Another place we can make a syntax improvement to our Menu component is where we take in the props argument. We can use object destructuring to scope the variables to this function. This allows us to access the title and recipes variables directly, no longer having to prefix them with props:

function Menu({ title, recipes }) {

return (

<article>

<header>

<h1>{title}</h1>

</header>

<div className="recipes">

{recipes.map((recipe, i) => (

<Recipe key={i} {...recipe} />

))}

</div>

</article>

);

}

Now let's code the component for each individual recipe:

function Recipe({ name, ingredients, steps }) {

return (

<section id={name.toLowerCase().replace(/ /g, "-")}>

<h1>{name}</h1>

<ul className="ingredients">

{ingredients.map((ingredient, i) => (

<li key={i}>{ingredient.name}</li>

))}

</ul>

<section className="instructions">

<h2>Cooking Instructions</h2>

{steps.map((step, i) => (

<p key={i}>{step}</p>

))}

</section>

</section>

);

}

Each recipe has a string for the name, an array of objects for ingredients, and an array of strings for the steps. Using object destructuring, we can tell this component to locally scope those fields by name so we can access them directly without having to use props.name, props.ingredients, or props.steps.

The first JavaScript expression we see is being used to set the id

attribute for the root section element. It's converting the recipe's name to a lowercase string and globally replacing spaces with dashes.

The result is that「Baked Salmon」will be converted to「baked-salmon」

(and likewise, if we had a recipe with the name「Boston Baked Beans,」

it would be converted to「boston-baked-beans」) before it's used as the id attribute in our UI. The value for name is also being displayed in an h1 as a text node.

Inside of the unordered list, a JavaScript expression is mapping each ingredient to an li element that displays the name of the ingredient.

Within our instructions section, we see the same pattern being used to return a paragraph element where each step is displayed. These map functions are returning arrays of child elements.

The complete code for the application should look like this: const data = [

{

name: "Baked Salmon",

ingredients: [

{ name: "Salmon", amount: 1, measurement: "l lb" },

{ name: "Pine Nuts", amount: 1, measurement: "cup" },

{ name: "Butter Lettuce", amount: 2, measurement: "cups" },

{ name: "Yellow Squash", amount: 1, measurement: "med" },

{ name: "Olive Oil", amount: 0.5, measurement: "cup" },

{ name: "Garlic", amount: 3, measurement: "cloves" }

],

steps: [

"Preheat the oven to 350 degrees.",

"Spread the olive oil around a glass baking dish.",

"Add the yellow squash and place in the oven for 30 mins.",

"Add the salmon, garlic, and pine nuts to the dish.",

"Bake for 15 minutes.",

"Remove from oven. Add the lettuce and serve."

]

},

{

name: "Fish Tacos",

ingredients: [

{ name: "Whitefish", amount: 1, measurement: "l lb" },

{ name: "Cheese", amount: 1, measurement: "cup" },

{ name: "Iceberg Lettuce", amount: 2, measurement: "cups" },

{ name: "Tomatoes", amount: 2, measurement: "large" },

{ name: "Tortillas", amount: 3, measurement: "med" }

],

steps: [

"Cook the fish on the grill until hot.",

"Place the fish on the 3 tortillas.",

"Top them with lettuce, tomatoes, and cheese."

]

}

];

function Recipe({ name, ingredients, steps }) {

return (

<section id={name.toLowerCase().replace(/ /g, "-")}>

<h1>{name}</h1>

<ul className="ingredients">

{ingredients.map((ingredient, i) => (

<li key={i}>{ingredient.name}</li>

))}

</ul>

<section className="instructions">

<h2>Cooking Instructions</h2>

{steps.map((step, i) => (

<p key={i}>{step}</p>

))}

</section>

</section>

);

}

function Menu({ title, recipes }) {

return (

<article>

<header>

<h1>{title}</h1>

</header>

<div className="recipes">

{recipes.map((recipe, i) => (

<Recipe key={i} {...recipe} />

))}

</div>

</article>

);

}

ReactDOM.render(

<Menu recipes={data} title="Delicious Recipes" />, document.getElementById("root")

);

When we run this code in the browser, React will construct a UI using our instructions with the recipe data as shown in Figure 5-2.

If you're using Google Chrome and have the React Developer Tools Extension installed, you can take a look at the present state of the component tree. To do this, open the developer tools and select the Components tab, as shown in Figure 5-3.

Here we can see the Menu and its child elements. The data array contains two objects for recipes, and we have two Recipe elements.

Each Recipe element has properties for the recipe name, ingredients, and steps. The ingredients and steps are passed down to their own components as data.

The components are constructed based on the application's data being passed to the Menu component as a property. If we change the recipes array and rerender our Menu component, React will change this DOM

as efficiently as possible.

Figure 5-2. Delicious Recipes output

Figure 5-3. Resulting virtual DOM in React Developer Tools React Fragments

In the previous section, we rendered the Menu component, a parent component that rendered the Recipe component. We want to take a moment to look at a small example of rendering two sibling components using a React fragment. Let's start by creating a new component called Cat that we'll render to the DOM at the root: function Cat({ name }) {

return <h1>The cat's name is {name}</h1>;

}

ReactDOM.render(<Cat name="Jungle" />, document.getElementById("root")); This will render the h1 as expected, but what might happen if we added a p tag to the Cat component at the same level as the h1?

function Cat({ name }) {

return (

<h1>The cat's name is {name}</h1>

<p>He's good.</p>

);

}

Immediately, we'll see an error in the console that reads Adjacent JSX

elements must be wrapped in an enclosing tag and

recommends using a fragment. This is where fragments come into play! React will not render two or more adjacent or sibling elements as a component, so we used to have to wrap these in an enclosing tag like a div. This led to a lot of unnecessary tags being created, though, and a bunch of wrappers without much purpose. If we use a React fragment,

we can mimic the behavior of a wrapper without actually creating a new tag.

Start by wrapping the adjacent tags, the h1 and p, with a React.Fragment tag:

function Cat({ name }) {

return (

<React.Fragment>

<h1>The cat's name is {name}</h1>

<p>He's good.</p>

</React.Fragment>

);

}

Adding this clears the warning. You also can use a fragment shorthand to make this look even cleaner:

function Cat({ name }) {

return (

<>

<h1>The cat's name is {name}</h1>

<p>He's good.</p>

</>

);

}

If you look at the DOM, the fragment is not visible in the resulting tree:

<div id="root" >

<h1> The cat's name is Jungle</h1>

<p> He's good</p>

</div>

Fragments are a relatively new feature of React and do away with the need for extra wrapper tags that can pollute the DOM.

Intro to webpack

Once we start working with React in real projects, there are a lot of questions to consider: How do we want to deal with JSX and ESNext transformation? How can we manage our dependencies? How can we optimize our images and CSS?

Many different tools have emerged to answer these questions, including Browserify, gulp, Grunt, Prepack, and more. Due to its features and widespread adoption by large companies, webpack has also emerged as one of the leading tools for bundling.

The React ecosystem has matured to include tools like create-react-app, Gatsby, and Code Sandbox. When you use these tools, a lot of the details about how the code gets compiled are abstracted away. For the remainder of this chapter, we are going to set up our own webpack build. This day in age, understanding that your JavaScript/React code is being compiled by something like webpack is vital, but knowing how to compile your JavaScript/React with something like webpack is not as important. We understand if you want to skip ahead.

Webpack is billed as a module bundler. A module bundler takes all of our different files (JavaScript, LESS, CSS, JSX, ESNext, and so on) and turns them into a single file. The two main benefits of bundling are modularity and network performance.

Modularity will allow you to break down your source code into parts, or modules, that are easier to work with, especially in a team environment.

Network performance is gained by only needing to load one dependency in the browser: the bundle. Each script tag makes an HTTP request, and there's a latency penalty for each HTTP request.

Bundling all the dependencies into a single file allows you to load everything with one HTTP request, thereby avoiding additional latency.

Aside from code compilation, webpack also can handle:

Code splitting

Splits up your code into different chunks that can be loaded when you need them. Sometimes these are called rollups or layers; the aim is to break up code as needed for different pages or devices.

Minification

Removes whitespace, line breaks, lengthy variable names, and unnecessary code to reduce the file size.

Feature Flagging

Sends code to one or more—but not all—environments when

testing out features.

Hot Module Replacement (HMR)

Watches for changes in source code. Changes only the updated modules immediately.

The Recipes app we built earlier in this chapter has some limitations that webpack will help us alleviate. Using a tool like webpack to statically build client JavaScript makes it possible for teams to work together on large-scale web applications. We can also gain the

following benefits by incorporating the webpack module bundler: Modularity

Using the module pattern to export modules that will later be imported or required by another part of the application makes source code more approachable. It allows development teams to work together, by allowing them to create and work with separate files that will be statically combined into a single file before sending to production.

Composition

With modules, we can build small, simple, reusable React

components that we can compose efficiently into applications.

Smaller components are easier to comprehend, test, and reuse.

They're also easier to replace down the line when enhancing applications.

Speed

Packaging all the application's modules and dependencies into a single client bundle will reduce the load time of an application because there's latency associated with each HTTP request.

Packaging everything together in a single file means that the client will only need to make a single request. Minifying the code in the bundle will improve load time as well.

Consistency

Since webpack will compile JSX and JavaScript, we can start using tomorrow's JavaScript syntax today. Babel supports a wide range of ESNext syntax, which means we don't have to worry about whether the browser supports our code. It allows developers to consistently use cutting-edge JavaScript syntax.

Creating the Project

To demonstrate how we might set up a React project from scratch, let's go ahead and create a new folder on our computer called recipes-app: mkdir recipes-app

cd recipes-app

For this project, we're going to go through the following steps: 1. Create the project.

2. Break down the recipe app into components that live in different files.

3. Set up a webpack build that incorporates Babel.

CREATE-REACT-APP

There's a tool called Create React App that can be used to autogenerate a React project with all of this preconfigured. We're going to take a closer look at what's happening behind the scenes before abstracting these steps away with a tool.

1. CREATE THE PROJECT

Next, we'll create the project and package.json file with npm, sending the -y flag to use all of the defaults. We'll also install webpack, webpack-cli, react, and react-dom:

npm init -y

npm install react react-dom serve

If we're using npm 5, we don't need to send the --save flag when installing. Next, we'll create the following directory structure to house

the components:

recipes-app (folder)

> node_modules (already added with npm install command)

> package.json (already added with npm init command)

> package-lock.json (already added with npm init command)

> index.html

> /src (folder)

> index.js

> /data (folder)

> recipes.json

> /components (folder)

> Recipe.js

> Instructions.js

> Ingredients.js

FILE ORGANIZATION

There's no one way to organize the files in a React project. This is just one possible strategy.

2. BREAK COMPONENTS INTO MODULES

Currently, the Recipe component is doing quite a bit. We're displaying the name of the recipe, constructing an unordered list of ingredients, and displaying the instructions, with each step getting its own paragraph element. This component should be placed in the Recipe.js file. In any file where we're using JSX, we'll need to import React at the top:

// ./src/components/Recipe.js

import React from "react";

export default function Recipe({ name, ingredients, steps }) {

return (

<section id="baked-salmon">

<h1>{name}</h1>

<ul className="ingredients">

{ingredients.map((ingredient, i) => (

<li key={i}>{ingredient.name}</li>

))}

</ul>

<section className="instructions">

<h2>Cooking Instructions</h2>

{steps.map((step, i) => (

<p key={i}>{step}</p>

))}

</section>

</section>

);

}

A more functional approach to the Recipe component would be to break it down into smaller, more focused function components and compose them together. We can start by pulling the instructions out into their own component and creating a module in a separate file we can use for any set of instructions.

In that new file called Instructions.js, create the following component:

// ./src/components/Instructions.js

import React from "react";

export default function Instructions({ title, steps }) {

return (

<section className="instructions">

<h2>{title}</h2>

{steps.map((s, i) => (

<p key={i}>{s}</p>

))}

</section>

);

}

Here, we've created a new component called Instructions. We'll pass the title of the instructions and the steps to this component. This way, we can reuse this component for「Cooking Instructions,」「Baking Instructions,」「Prep Instructions,」or a「Pre-cook Checklist」—anything that has steps.

Now think about the ingredients. In the Recipe component, we're only displaying the ingredient names, but each ingredient in the data for the recipe has an amount and measurement as well. We'll create a component called Ingredient for this:

// ./src/components/Ingredient.js

import React from "react";

export default function Ingredient({ amount, measurement, name }) {

return (

<li>

{amount} {measurement} {name}

</li>

);

}

Here, we assume each ingredient has an amount, a measurement, and a name. We destructure those values from our props object and display them each in independent classed span elements.

Using the Ingredient component, we can construct an

IngredientsList component that can be used any time we need to display a list of ingredients:

// ./src/components/IngredientsList.js

import React from "react";

import Ingredient from "./Ingredient"; export default function IngredientsList({ list }) {

return (

<ul className="ingredients">

{list.map((ingredient, i) => (

<Ingredient key={i} {...ingredient} />

))}

</ul>

);

}

In this file, we first import the Ingredient component because we're going to use it for each ingredient. The ingredients are passed to this component as an array in a property called list. Each ingredient in the list array will be mapped to the Ingredient component. The JSX

spread operator is used to pass all the data to the Ingredient component as props.

Using spread operator:

<Ingredient {...ingredient} />

is another way of expressing:

<Ingredient

amount={ingredient.amount}

measurement={ingredient.measurement}

name={ingredient.name}

/>

So, given an ingredient with these fields:

let ingredient = {

amount: 1,

measurement: "cup",

name: "sugar"

};

We get:

<Ingredient amount={1} measurement="cup" name="sugar" /> Now that we have components for ingredients and instructions, we can compose recipes using these components:

// ./src/components/Recipe.js

import React from "react";

import IngredientsList from "./IngredientsList"; import Instructions from "./Instructions"; function Recipe({ name, ingredients, steps }) {

return (

<section id={name.toLowerCase().replace(/ /g, "-")}>

<h1>{name}</h1>

<IngredientsList list={ingredients} />

<Instructions title="Cooking Instructions" steps={steps} />

</section>

);

}

export default Recipe;

First, we import the components we're going to use: IngredientsList and Instructions. Now we can use them to create the Recipe component. Instead of a bunch of complicated code building out the entire recipe in one place, we've expressed our recipe more declaratively by composing smaller components. Not only is the code nice and simple, but it also reads well. This shows us that a recipe should display the name of the recipe, a list of ingredients, and some

cooking instructions. We've abstracted away what it means to display ingredients and instructions into smaller, simple components.

In a modular approach, the Menu component would look pretty similar.

The key difference is that it would live in its own file, import the modules it needs to use, and export itself:

// ./src/components/Menu.js

import React from "react";

import Recipe from "./Recipe";

function Menu({ recipes }) {

return (

<article>

<header>

<h1>Delicious Recipes</h1>

</header>

<div className="recipes">

{recipes.map((recipe, i) => (

<Recipe key={i} {...recipe} />

))}

</div>

</article>

);

}

export default Menu;

We still need to use ReactDOM to render the Menu component. The main file for the project is index.js. This will be responsible for rendering the component to the DOM.

Let's create this file:

// ./src/index.js

import React from "react"; import { render } from "react-dom";

import Menu from "./components/Menu";

import data from "./data/recipes.json";

render(<Menu recipes={data} />, document.getElementById("root")); The first four statements import the necessary modules for our app to work. Instead of loading react and react-dom via the script tag, we import them so webpack can add them to our bundle. We also need the Menu component and a sample data array that has been moved to a separate module. It still contains two recipes: Baked Salmon and Fish Tacos.

All of our imported variables are local to the index.js file. When we render the Menu component, we pass the array of recipe data to this component as a property.

The data is being pulled from the recipes.json file. This is the same data we used earlier in the chapter, but now it's following valid JSON

formatting rules:

// ./src/data/recipes.json

[

{

"name": "Baked Salmon",

"ingredients": [

{ "name": "Salmon", "amount": 1, "measurement": "lb" },

{ "name": "Pine Nuts", "amount": 1, "measurement": "cup" },

{ "name": "Butter Lettuce", "amount": 2, "measurement": "cups" },

{ "name": "Yellow Squash", "amount": 1, "measurement": "med" },

{ "name": "Olive Oil", "amount": 0.5, "measurement": "cup" },

{ "name": "Garlic", "amount": 3, "measurement": "cloves" }

],

"steps": [

"Preheat the oven to 350 degrees.",

"Spread the olive oil around a glass baking dish.",

"Add the yellow squash and place in the oven for 30 mins.",

"Add the salmon, garlic, and pine nuts to the dish.",

"Bake for 15 minutes.",

"Remove from oven. Add the lettuce and serve."

]

},

{

"name": "Fish Tacos",

"ingredients": [

{ "name": "Whitefish", "amount": 1, "measurement": "lb" },

{ "name": "Cheese", "amount": 1, "measurement": "cup" },

{ "name": "Iceberg Lettuce", "amount": 2, "measurement": "cups" },

{ "name": "Tomatoes", "amount": 2, "measurement": "large" },

{ "name": "Tortillas", "amount": 3, "measurement": "med" }

],

"steps": [

"Cook the fish on the grill until cooked through.",

"Place the fish on the 3 tortillas.",

"Top them with lettuce, tomatoes, and cheese."

]

}

]

Now that we've pulled our code apart into separate modules and files, let's create a build process with webpack that will put everything back together into a single file. You may be thinking,「Wait, we just did all of that work to break everything apart, and now we're going to use a tool to put it back together? Why on Earth…?」Splitting projects into separate files typically makes larger projects easier to manage because team members can work on separate components without overlap. It also means that files can be easier to test.

3. CREATING THE WEBPACK BUILD

In order to create a static build process with webpack, we'll need to install a few things. Everything we need can be installed with npm: npm install --save-dev webpack webpack-cli

Remember that we've already installed React and ReactDOM.

For this modular Recipes app to work, we're going to need to tell webpack how to bundle our source code into a single file. As of version 4.0.0, webpack does not require a configuration file to bundle a project. If we don't include a config file, webpack will run the defaults to package our code. Using a config file, though, means we'll be able to customize our setup. Plus, this shows us some of the magic of webpack instead of hiding it away. The default webpack configuration file is always webpack.config.js.

The starting file for our Recipes app is index.js. It imports React, ReactDOM, and the Menu.js file. This is what we want to run in the browser first. Wherever webpack finds an import statement, it will find the associated module in the filesystem and include it in the bundle. index.js imports Menu.js, Menu.js imports Recipe.js, Recipe.js imports Instructions.js and IngredientsList.js, and IngredientsList.js imports Ingredient.js. Webpack will follow this import tree and include all of these necessary modules in our bundle. Traversal through all these files creates what's called a dependency graph. A dependency is just something our app needs, like a component file, a library file like React, or an image. Picture each file we need as a circle on the graph, with webpack drawing all the lines between the circles to create the graph. That graph is the bundle.

IMPORT STATEMENTS

We're using import statements, which are not presently supported by most browsers or by Node.js. The reason import statements work is that Babel will convert them into require('module/path'); statements in our final code. The

require function is how CommonJS modules are typically loaded.

As webpack builds our bundle, we need to tell it to transform JSX to React elements.

The webpack.config.js file is just another module that exports a JavaScript literal object that describes the actions webpack should take.

The configuration file should be saved to the root folder of the project, right next to the index.js file:

// ./webpack.config.js

var path = require("path");

module.exports = {

entry: "./src/index.js",

output: {

path: path.join(__dirname, "dist", "assets"), filename: "bundle.js"

}

};

First, we tell webpack that our client entry file is ./src/index.js. It will automatically build the dependency graph based on import statements starting in that file. Next, we specify that we want to output a bundled JavaScript file to ./dist/bundle.js. This is where webpack will place the final packaged JavaScript.

Next, let's install the necessary Babel dependencies. We'll need babel-loader and @babel/core:

npm install babel-loader @babel/core --save-dev

The next set of instructions for webpack consists of a list of loaders to run on specified modules. This will be added to the config file under the module field:

module.exports = {

entry: "./src/index.js",

output: {

path: path.join(__dirname, "dist", "assets"), filename: "bundle.js"

},

module: {

rules: [{ test: /\.js$/, exclude: /node_modules/, loader: "babel-loader" }]

}

};

The rules field is an array because there are many types of loaders you can incorporate with webpack. In this example, we're only incorporating the babel-loader. Each loader is a JavaScript object.

The test field is a regular expression that matches the file path of each module that the loader should operate on. In this case, we're running the babel-loader on all imported JavaScript files except those found in the node_modules folder.

At this point, we need to specify presets for running Babel. When we set a preset, we tell Babel which transforms to perform. In other words, we can say,「Hey Babel. If you see some ESNext syntax here, go ahead and transform that code into syntax we're sure the browser understands. If you see some JSX, transform that too.」Start by installing the presets:

npm install @babel/preset-env @babel/preset-react --save-dev

Then create one more file at the root of the project: .babelrc:

{

"presets" : ["@babel/preset-env", "@babel/preset-react"]

}

All right! We've created something pretty cool: a project that resembles a real React app! Let's go ahead and run webpack to make sure this works.

Webpack is run statically. Typically, bundles are created before the app is deployed to the server. You can run it from the command line using npx:

npx webpack --mode development

Webpack will either succeed and create a bundle or fail and show you an error. Most errors have to do with broken import references. When debugging webpack errors, look closely at the filenames and file paths used in import statements.

You can also add an npm script to your package.json file to create a shortcut:

"scripts": {

"build": "webpack --mode production"

},

Then you can run the shortcut to generate the bundle:

npm run build

Loading the Bundle

We have a bundle, so now what? We exported the bundle to the dist folder. This folder contains the files we want to run on the web server.

The dist folder is where the index.html file should be placed. This file needs to include a target div element where the React Menu component will be mounted. It also requires a single script tag that will load our bundled JavaScript:

// ./dist/index.html

<!DOCTYPE html>

<html>

<head>

<meta charset="utf-8" />

<title> React Recipes App</title>

</head>

<body>

<div id="root" ></div>

<script src="bundle.js" ></script>

</body>

</html>

This is the home page for your app. It will load everything it needs from one file, one HTTP request: bundle.js. You'll need to deploy these files to your web server or build a web server application that will serve these files with something like Node.js or Ruby on Rails.

Source Mapping

Bundling our code into a single file can cause some setbacks when it comes time to debug the application in the browser. We can eliminate this problem by providing a source map. A source map is a file that maps a bundle to the original source files. With webpack, all we have to do is add a couple lines to our webpack.config.js file.

//webpack.config.js with source mapping

module.exports = {

...

devtool: "#source-map" // Add this option for source mapping

};

Setting the devtool property to '#source-map' tells webpack that you want to use source mapping. The next time you run webpack, you'll see that two output files are generated and added to the dist folder: the original bundle.js and bundle.js.map.

The source map is going to let you debug using your original source files. In the Sources tab of your browser's developer tools, you should find a folder named webpack://. Inside of this folder, you'll see all the source files in your bundle, as shown in Figure 5-4.

Figure 5-4. Sources panel of Chrome Developer Tools

You can debug from these files using the browser step-through

debugger. Clicking on any line number adds a breakpoint. Refreshing the browser will pause JavaScript processing when any breakpoints are reached in your source file. You can inspect scoped variables in the Scope panel or add variables to watch in the Watch panel.

Create React App

A pretty amazing tool to have at your disposal as a React developer is Create React App, a command-line tool that autogenerates a React project. Create React App was inspired by the Ember CLI project, and it lets developers get started with React projects quickly without the manual configuration of webpack, Babel, ESLint, and associated tools.

To get started with Create React App, install the package globally: npm install -g create-react-app

Then, use the command and the name of the folder where you'd like the app to be created:

create-react-app my-project

NPX

You can also use npx to run Create React App without the need for a global install. Simply run npx create-react-app my-project.

This will create a React project in that directory with just three dependencies: React, ReactDOM, and react-scripts. react-scripts was also created by Facebook and is where the real magic

happens. It installs Babel, ESLint, webpack, and more so that you don't have to configure them manually. Within the generated project folder, you'll also find a src folder containing an App.js file. Here, you can edit the root component and import other component files.

From within the my-react-project folder, you can run npm start. If you prefer, you can also run yarn start. This will start your application on port 3000.

You can run tests with npm test or yarn test. This runs all of the test files in the project in an interactive mode.

You can also run the npm run build command. Using yarn, run yarn build.

This will create a production-ready bundle that has been transformed and minified.

Create React App is a great tool for beginners and experienced React developers alike. As the tool evolves, more functionality will likely be added, so you can keep an eye on the changes on GitHub. Another way to get started with React without having to worry about setting up your own customized webpack build is to use CodeSandbox. CodeSandbox is an IDE that runs online at https://codesandbox.io.

In this chapter, we leveled up our React skills by learning about JSX.

We created components. We broke those components into a project structure, and we learned more about Babel and webpack. Now we're ready to take our knowledge of components to the next level. It's time

to talk about Hooks.

Chapter 6. React State

