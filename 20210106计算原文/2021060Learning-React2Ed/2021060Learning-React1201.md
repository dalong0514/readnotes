# 1201. React and the Server

So far, we've built small applications with React that run entirely in the browser. They've collected data in the browser and saved the data using browser storage. This makes sense because React is a view layer; it's intended to render UI. However, most applications require at least the existence of some sort of a backend, and we will need to understand how to structure applications with a server in mind.

Even if you have a client application that's relying entirely on cloud services for the backend, you still need to get and send data to these services. There are specific places where these transactions should be made and libraries that can help you deal with the latency associated with HTTP requests.

Additionally, React can be rendered isomorphically, which means that it can be in platforms other than the browser. This means we can render our UI on the server before it ever gets to the browser. Taking advantage of server rendering, we can improve the performance, portability, and security of our applications.

We start this chapter with a look at the differences between isomorphism and universalism and how both concepts relate to React.

Next, we'll look at how to make an isomorphic application using universal JavaScript. Finally, we'll improve the color organizer by

adding a server and rendering the UI on the server first.

Isomorphic Versus Universal

The terms isomorphic and universal are often used to describe applications that work on both the client and the server. Although these terms are used interchangeably to describe the same application, there's a subtle difference between them that's worth investigating.

Isomorphic applications are applications that can be rendered on multiple platforms. Universal code means that the exact same code can run in multiple environments.1

Node.js will allow us to reuse the same code we've written in the browser in other applications such as servers, CLIs, and even native applications. Let's take a look at some universal JavaScript: const userDetails = response => {

const login = response.login;

console.log(login);

};

The printNames function is universal. The exact same code can be invoked in the browser or on a server. This means that if we constructed a server with Node.js, we could potentially reuse code between the two environments. Universal JavaScript is JavaScript that can run on the server or in the browser without error (see Figure 12-1).

Figure 12-1. Client and server domains

Client and Server Domains

The server and the client are completely different domains, so all of our JavaScript code won't automatically work between them. Let's take a look at creating an AJAX request with the browser:

fetch("https://api.github.com/users/moonhighway")

.then(res => res.json())

.then(console.log);

Here, we're making a fetch request to the GitHub API, converting the response to JSON, then calling a function on the JSON results to parse it.

However, if we try to run the exact same code with Node.js, we get an error:

fetch("https://api.github.com/users/moonhighway")

^

ReferenceError: fetch is not defined

at Object.<anonymous> (/Users/eveporcello/Desktop/index.js:7:1) at Module.\_compile (internal/modules/cjs/loader.js:1063:30) at Object.Module.\_extensions..js

(internal/modules/cjs/loader.js:1103:10)

at Module.load (internal/modules/cjs/loader.js:914:32)

at Function.Module.\_load (internal/modules/cjs/loader.js:822:14) at Function.Module.runMain (internal/modules/cjs/loader.js:1143:12) at internal/main/run_main_module.js:16:11

This error occurs because Node.js does not have a built-in fetch function like the browser does. With Node.js, we can use isomorphic-fetch from npm, or use the built-in https module. Since we've already used the fetch syntax, let's incorporate isomorphic-fetch: npm install isomorphic-fetch

Then we'll just import isomorphic-fetch with no changes to the code:

const fetch = require("isomorphic-fetch"); const userDetails = response => {

const login = response.login;

console.log(login);

};

fetch("https://api.github.com/users/moonhighway")

.then(res => res.json())

.then(userDetails);

Loading data from an API with Node.js requires the use of core modules. It requires different code. In these samples, the userDetails function is universal, so the same function works in both environments.

This JavaScript file is now isomorphic. It contains universal JavaScript.

All of the code is not universal, but the file itself will work in both environments. It can run it with Node.js or include it in a <script> tag in the browser.

Let's take a look at the Star component. Is this component universal?

function Star({

selected = false,

onClick = f => f

}) {

return (

<div

className={

selected ? "star selected" : "star"

}

onClick={onClick}

></div>

);

}

Sure it is; remember, the JSX compiles to JavaScript. The Star component is simply a function:

function Star({

selected = false,

onClick = f => f

}) {

return React.createElement("div", {

className: selected

? "star selected"

: "star",

onClick: onClick

});

}

We can render this component directly in the browser, or render it in a different environment and capture the HTML output as a string.

ReactDOM has a renderToString method that we can use to render UI to an HTML string:

// Renders html directly in the browser

ReactDOM.render(<Star />);

// Renders html as a string

let html = ReactDOM.renderToString(<Star />); We can build isomorphic applications that render components on different platforms, and we can architect these applications in a way that reuses JavaScript code universally across multiple environments.

Additionally, we can build isomorphic applications using other languages such as Go or Python—we're not restricted to Node.js.

Server Rendering React

Using the ReactDOM.renderToString method allows us to render UI on the server. Servers are powerful; they have access to all kinds of resources that browsers do not. Servers can be secure and access secure data. You can use all of these added benefits to your advantage by

rendering initial content on the server.

The app we'll server render is our Recipes app that we built in

Chapter 5. You can run Create React App and place this code over the contents of the index.js file:

import React from "react";

import ReactDOM from "react-dom";

import "./index.css";

import { Menu } from "./Menu";

const data = [

{

name: "Baked Salmon",

ingredients: [

{

name: "Salmon",

amount: 1,

measurement: "lb"

},

{

name: "Pine Nuts",

amount: 1,

measurement: "cup"

},

{

name: "Butter Lettuce",

amount: 2,

measurement: "cups"

},

{

name: "Yellow Squash",

amount: 1,

measurement: "med"

},

{

name: "Olive Oil",

amount: 0.5,

measurement: "cup"

},

{

name: "Garlic",

amount: 3,

measurement: "cloves"

}

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

{

name: "Whitefish",

amount: 1,

measurement: "l lb"

},

{

name: "Cheese",

amount: 1,

measurement: "cup"

},

{

name: "Iceberg Lettuce",

amount: 2,

measurement: "cups"

},

{

name: "Tomatoes",

amount: 2,

measurement: "large"

},

{

name: "Tortillas",

amount: 3,

measurement: "med"

}

],

steps: [

"Cook the fish on the grill until hot.",

"Place the fish on the 3 tortillas.",

"Top them with lettuce, tomatoes, and cheese."

]

}

];

ReactDOM.render(

<Menu

recipes={data}

title="Delicious Recipes"

/>,

document.getElementById("root")

);

The components will live in a new file called Menu.js: function Recipe({ name, ingredients, steps }) {

return (

<section

id={name.toLowerCase().replace(/ /g, "-")}

>

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

export function Menu({ title, recipes }) {

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

Throughout the book, we've rendered components on the client. Client-side rendering is typically the first approach we'll use when building an app. We serve up the Create React App build folder, and the browser runs the HTML and makes calls to the script.js file to load any JavaScript.

Doing this can be time consuming. The user might have to wait to see anything load for a few seconds depending on their network speed.

Using Create React App with an Express server, we can create a hybrid experience of client- and server-side rendering.

We're rendering a Menu component that renders several recipes. The first change we'll make to this app is to use ReactDOM.hydrate instead of ReactDOM.render.

These two functions are the same except hydrate is used to add content to a container that was rendered by ReactDOMServer. The order of operations will look like this:

1. Render a static version of the app, allowing users to see that something has happened and the page has「loaded.」

2. Make the request for the dynamic JavaScript.

3. Replace the static content with the dynamic content.

4. User clicks on something and it works.

We're rehydrating the app after a server-side render. By rehydrate, we mean statically loading the content as static HTML and then loading the JavaScript. This allows users to experience perceived performance.

They'll see that something is happening on the page, and that makes them want to stay on the page.

Next, we need to set up our project's server, and we'll use Express, a lightweight Node server. Install it first:

npm install express

Then we'll create a server folder called server and create an index.js file inside of that. This file will build a server that will serve up the build folder but also preload some static HTML content: import express from "express";

const app = express();

app.use(express. static("./build"));

This imports and statically serves the build folder. Next, we want to

use renderToString from ReactDOM to render the app as a static HTML string:

import React from "react";

import ReactDOMServer from "react-dom/server"; import { Menu } from "../src/Menu.js";

const PORT = process.env.PORT || 4000;

app.get("/*", (req, res) => {

const app = ReactDOMServer.renderToString(

<Menu />

);

});

app.listen(PORT, () =>

console.log(

`Server is listening on port ${PORT}`

)

);

We'll pass the Menu component to this function because that's what we want to render statically. We then want to read the static index.html file from the built client app, inject the app's content in the div, and send that as the response to the request:

app.get("/*", (req, res) => {

const app = ReactDOMServer.renderToString(

<Menu />

);

const indexFile = path.resolve(

"./build/index.html"

);

fs.readFile(indexFile, "utf8", (err, data) => {

return res.send(

data.replace(

'<div id="root"></div>',

`<div id="root">${app}</div>`

)

);

});

});

Once we've completed this, we'll need to do some configuration with webpack and Babel. Remember, Create React App can take care of compiling and building out of the box, but we need to set up and enforce different rules with the server project.

Start by installing a few dependencies (OK, a lot of dependencies): npm install @babel/core @babel/preset-env babel-loader nodemon npm-run-all

webpack webpack-cli webpack-node-externals

With Babel installed, let's create a .babelrc with some presets:

{

"presets" : ["@babel/preset-env", "react-app"]

}

You'll add react-app because the project uses Create React App, and it has already been installed.

Next, add a webpack configuration file for the server called webpack.server.js:

const path = require("path");

const nodeExternals = require("webpack-node-externals"); module.exports = {

entry: "./server/index.js",

target: "node",

externals: [nodeExternals()],

output: {

path: path.resolve("build-server"),

filename: "index.js"

},

module: {

rules: [

{

test: /\.js$/,

use: "babel-loader"

}

]

}

};

The babel-loader will transform JavaScript files as expected, and nodeExternals will scan the node_modules folder for all node_modules names. Then, it will build an external function that tells webpack not to bundle those modules or any submodules.

Also, you might run into a webpack error due to a version conflict between the version you've installed with Create React App and the version we just installed. To fix the conflict, just add a .env file to the root of the project and add:

SKIP_PREFLIGHT_CHECK=true

Finally, we can add a few extra npm scripts to run our dev commands:

{

"scripts" : {

//...

"dev:build-server" : "NODE_ENV=development webpack --config webpack.server.js

--mode=development -w",

"dev:start" : "nodemon ./server-build/index.js",

"dev" : "npm-run-all --parallel build dev:*"

}

}

1. dev:build-server: Passes development as an environment variable and runs webpack with the new server config.

2. dev:start: Runs the server file with nodemon, which will listen for any changes.

3. dev: Runs both processes in parallel.

Now when we run npm run dev, both of the processes will run. You should be able to see the app running on localhost:4000. When the app runs, the content will load in sequence, first as prerendered HTML

and then with the JavaScript bundle.

Using a technique like this can mean faster load times and will yield a boost in perceived performance. With users expecting page-load times of two seconds or less, any improved performance can mean the difference between users using your website or bouncing to a competitor.

Server Rendering with Next.js

Another powerful and widely used tool in the server rendering ecosystem is Next.js. Next is an open source technology that was released by Zeit to help engineers write server-rendered apps more easily. This includes features for intuitive routing, statically optimizing, automatic splitting, and more. In the next section, we'll take a closer look at how to work with Next.js to enable server rendering in our app.

To start, we'll create a whole new project, running the following commands:

mkdir project-next

cd project-next

npm init -y

npm install --save react react-dom next

mkdir pages

Then we'll create some npm scripts to run common commands more easily:

{

//...

"scripts" : {

"dev" : "next",

"build" : "next build",

"start" : "next start"

}

}

In the pages folder, we'll create an index.js file. We'll write our component, but we won't worry about importing React or ReactDOM.

Instead, we'll just write a component:

export default function Index() {

return (

<div>

<p>Hello everyone!</p>

</div>

);

}

Once we've created this, we can run npm run dev to see the page running on localhost:3000. It displays the expected component.

You'll also notice there's a small lightning bolt icon in the lower righthand corner of the screen. Hovering over this will display a button that reads Prerendered Page. When you click on it, it will take you to documentation about the Static Optimization Indicator. This means that the page fits the criteria for automatic static optimization, meaning that it can be prerendered. There are no data requirements that block it. If a page is automatically statically optimized (a mouthful, but useful!), the page is faster to load because there's no server-side effort needed. The page can be streamed from a CDN, yielding a super-fast user experience. You don't have to do anything to pick up on this performance enhancement.

What if the page does have data requirements? What if the page cannot be prerendered? To explore this, let's make our app a bit more robust and build toward a component that fetches some remote data from an API. In a new file called Pets.js:

export default function Pets() {

return <h1>Pets!</h1>;

}

To start, we'll render an h1. Now we can visit localhost:3000/pets to see that our page is now loaded on that route. That's good, but we can improve this by adding links and a layout component that will display the correct content for each page. We'll create a header that can be used on both pages and will display links:

import Link from "next/link";

export default function Header() {

return (

<div>

<Link href="/">

<a>Home</a>

</Link>

<Link href="/pets">

<a>Pets</a>

</Link>

</div>

);

}

The Link component is a wrapper around a couple of links. These look similar to the links we created with React Router. We can also add a style to each of the <a> tags:

const linkStyle = {

marginRight: 15,

color: "salmon"

};

export default function Header() {

return (

<div>

<Link href="/">

<a style={linkStyle}>Home</a>

</Link>

<Link href="/pets">

<a style={linkStyle}>Pets</a>

</Link>

</div>

);

}

Next, we'll incorporate the Header component into a new file called Layout.js. This will dynamically display the component based on the correct route:

import Header from "./Header";

export function Layout(props) {

return (

<div>

<Header />

{props.children}

</div>

);

}

The Layout component will take in props and display any additional content in the component underneath the Header. Then in each page, we can create content blocks that can be passed to the Layout component when rendered. For example, the index.js file would now look like this:

import Layout from "./Layout";

export default function Index() {

return (

<Layout>

<div>

<h1>Hello everyone!</h1>

</div>

</Layout>

);

}

We'll do the same in the Pets.js file:

import Layout from "./Layout";

export default function Pets() {

return (

<Layout>

<div>

<h1>Hey pets!</h1>

</div>

</Layout>

);

}

Now if we visit the homepage, we should see the header, then when we click the Pets link, we should see the Pets page.

When we click on the lightning bolt button in the lower righthand corner, we'll notice that these pages are still being prerendered. This is to be expected as we continue to render static content. Let's use the Pets page to load some data and see how this changes.

To start, we'll install isomorphic-unfetch like we did earlier in the chapter:

npm install isomorphic-unfetch

We'll use this to make a fetch call to the Pet Library API. Start by importing it in the Pages.js file:

import fetch from "isomorphic-unfetch";

Then we're going to add a function called getInitialProps. This will handle fetching and loading the data:

Pets.getInitialProps = async function() {

const res = await fetch(

`http://pet-library.moonhighway.com/api/pets`

);

const data = await res.json();

return {

pets: data

};

};

When we return the data as the value for pets, we then can map over the data in the component.

Adjust the component to map over the pets property: export default function Pets(props) {

return (

<Layout>

<div>

<h1>Pets!</h1>

<ul>

{props.pets.map(pet => (

<li key={pet.id}>{pet.name}</li>

))}

</ul>

</div>

</Layout>

);

}

If getInitialProps is present in the component, Next.js will render the page in response to each request. This means that the page will be server-side rendered instead of statically prerendered, so the data from the API will be current on each request.

Once we're satisfied with the state of the application, we can run a build with npm run build. Next.js is concerned with performance, so it will give us a full rundown of the number of kilobytes present for each file. This is a quick spot-check for unusually large files.

Next to each file, we'll see an icon for whether a site is server-rendered at runtime (λ), automatically rendered as HTML (○), or automatically generated as static HTML + JSON (●).

Once you've built the app, you can deploy it. Next.js is an open source product of Zeit, a cloud-hosting provider, so the experience of deploying with Zeit is the most straightforward. However, you can use

many different hosting providers to deploy your application.

To recap, there are some important bits of terminology that are important to understand when setting out to build your own apps: CSR (client-side rendering)

Rendering an app in a browser, generally using the DOM. This is what we do with an unmodified Create React App.

SSR (server-side rendering)

Rendering a client-side or universal app to HTML on the server.

Rehydration

Loading JavaScript views on the client to reuse the server-rendered HTML's DOM tree and data.

Prerendering

Running a client-side application at build time and capturing initial state as static HTML.

Gatsby

Another popular site generator that's based on React is Gatsby. Gatsby is taking over the world as a straightforward way to create a content-driven website. It aims to offer smarter defaults to manage concerns like performance, accessibility, image handling, and more. And if you're reading this book, it's likely that you might work on a Gatsby project at some point!

Gatsby is used for a range of projects, but it's often used to build

content-driven websites. In other words, if you have a blog or static content, Gatsby is a great choice, particularly now that you know React. Gatsby can also handle dynamic content like loading data from APIs, integration with frameworks, and more.

In this section, we'll start building a quick Gatsby site to demonstrate how it works. Essentially, we'll build our small Next.js app as a Gatsby app:

npm install -g gatsby-cli

gatsby new pets

If you have yarn installed globally, the CLI will ask you whether to use yarn or npm. Either is fine. Then you'll change directory into the pets folder:

cd pets

Now you can start the project with gatsby develop. When you visit localhost:8000, you'll see your Gatsby starter site running. Now you can take a tour of the files.

If you open up the project's src folder, you'll see three subfolders: components, images, and pages.

Within the pages folder, you'll find a 404.js error page, an index.js page (the page that renders when you visit localhost:8000), and a page-2.js that renders the content of the second page.

If you visit the components folder, this where the magic of Gatsby is located. Remember when we built the Header and Layout components

with Next.js? Both of these components are already created as templates in the components folder.

A few particularly interesting things to note:

layout.js

This contains the Layout component. It uses the useStaticQuery hook to query some data about the site using GraphQL.

seo.js

This component lets us access the page's metadata for search engine optimization purposes.

If you add additional pages to the pages folder, this will add additional pages to your site. Let's try it and add a page-3.js file to the pages folder. Then we'll add the following code to that file to stand up a quick page:

import React from "react";

import { Link } from "gatsby";

import Layout from "../components/layout"; import SEO from "../components/seo";

const ThirdPage = () => (

<Layout>

<SEO title="Page three" />

<h1>Hi from the third page</h1>

<Link to="/">Go back to the homepage</Link>

</Layout>

);

export default ThirdPage;

We'll use the Layout component to wrap the content so that it's displayed as children. Not only does Layout display the dynamic content, but as soon as we create it, the page is autogenerated.

That's the tip of the iceberg with what you can do with Gatsby, but we'll leave you with some information about some of its additional features:

Static content

You can build your site as static files, which can be deployed without a server.

CDN support

It's possible to cache your site on CDNs all over the world to improve performance and availability.

Responsive and progressive images

Gatsby loads images as blurry placeholders, then fades in the full assets. This tactic, popularized by Medium, allows users to see something rendering before the full resource is available.

Prefetching of linked pages

All of the content needed to load the next page will load in the background before you click on the next link.

All of these features and more are used to ensure a seamless user experience. Gatsby has made a lot of decisions for you. That could be good or bad, but these constraints aim to let you focus on your content.

## React in the Future

While Angular, Ember, and Vue continue to have substantial marketshare in the JavaScript ecosystem, it's hard to argue with the fact that React is currently the most widely used and influential library for building JavaScript apps. In addition to the library itself, the wider JavaScript community, as evidenced particularly by Next.js and Gatsby, has embraced React as the tool of choice.

So where do we go from here? We'd encourage you to use these skills to build your own projects. If you're looking to build mobile applications, you can check out React Native. If you're looking to declaratively fetch data, you can check out GraphQL. If you're looking to build content-based websites, dig deeper into Next.js and Gatsby.

There are a number of avenues you can travel down, but these skills you've picked up in React will serve you well as you set out to build your own applications. When you're doing so, we hope that this book will serve as a reference and a foundation. Although React and its related libraries will almost certainly go through changes, these are stable tools that you can feel confident about using right away.

Building apps with React and functional, declarative JavaScript is a lot of fun, and we can't wait to see what you'll build.

Gert Hengeveld,「Isomorphism vs Universal JavaScript」, Medium.