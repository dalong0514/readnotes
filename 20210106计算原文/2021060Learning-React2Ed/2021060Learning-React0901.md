# 0901. Suspense

This is the least important chapter in this book. At least, that's what we've been told by the React team. They didn't specifically say,「this is the least important chapter, don't write it.」They've only issued a series of tweets warning educators and evangelists that much of their work in this area will very soon be outdated. All of this will change.

It could be said that the work the React team has done with Fiber, Suspense, and concurrent mode represents the future of web development. This work may change the way browsers interpret JavaScript. That sounds pretty important. We're saying that this is the least important chapter in this book because the community hype for Suspense is high; we need to say it to balance out your expectations.

The APIs and patterns that make up Suspense are not the single overarching theory that defines how all things large and small should operate.

Suspense is a just a feature. You may not ever need to use it. It's being designed to solve specific problems that Facebook experiences working at scale. We don't all have the same problems as Facebook, so we may want to think twice before reaching for those tools as the solution to all our problems. They may unnecessarily introduce complexity where complexity is not needed. Plus, this is all going to change. Concurrent mode is an experimental feature, and the React team has issued stern warnings about trying to use it in production. In

fact, most of these concepts involve using hooks. If you don't see yourself developing custom hooks on a daily basis, you'll probably never need to know about these features. Much of the mechanics involving Suspense can be abstracted away in hooks.

In light of these three paragraphs of downplay, the concepts covered in this chapter are exciting. If used correctly, they could someday help us create better user experiences. If you own or maintain a React library of hooks and/or components, you may find these concepts valuable.

They'll help you fine-tune your custom hooks to allow for better feedback and prioritization.

In this chapter, we'll build another small app to demonstrate some of these features. We'll essentially rebuild the app from Chapter 8, but this time with a little more structure. For example, we'll be using a SiteLayout component:

export default function SiteLayout({

children,

menu = c => null

}) {

return (

<div className="site-container">

<div>{menu}</div>

<div>{children}</div>

</div>

);

}

SiteLayout will rendered within the App component to help us compose our UI:

export default function App() {

return (

<SiteLayout menu={<p>Menu</p>}>

<>

<Callout>Callout</Callout>

<h1>Contents</h1>

<p>This is the main part of the example layout</p>

</>

</SiteLayout>

);

}

This component will be used to give our layout some style, as shown in

Figure 9-1.

Specifically, it will allow us to clearly see where and when specific components are rendered.

Figure 9-1. Sample layout

Error Boundaries

Thus far, we haven't done the best job with handling errors. An error thrown anywhere in our component tree will take down the entire application. Larger component trees only further complicate our project and complicate debugging it. Sometimes, it can be hard to pinpoint where an error has occurred, especially when they occur within components that we didn't write.

Error boundaries are components that can be used to prevent errors from crashing the entire app. They also allow us to render sensible error messages in production. Because errors can be handled by a single component, they could potentially track errors within the application and report them to an issue management system.

Currently, the only way to make an error boundary component is to use a class component. Like most topics in this chapter, this too will eventually change. In the future, creating error boundaries could be possible with a hook or some other solution that doesn't require creating a class. For now, here's an example of an ErrorBoundary component:

import React, { Component } from "react"; export default class ErrorBoundary extends Component {

state = { error: null };

static getDerivedStateFromError(error) {

return { error };

}

render() {

const { error } = this.state;

const { children, fallback } = this.props;

if (error) return <fallback error={error} />; return children;

}

}

This is a class component. It stores state differently, and it doesn't use hooks. Instead, it has access to specific methods that are invoked during different times throughout the component life cycle.

getDerivedStateFromError is one of those methods. It is invoked when an error occurs anywhere within the children during the render process. When an error occurs, the value for state.error is set.

Where there's an error, the fallback component is rendered, and that error is passed to the component as a property.

Now we can use this component in our tree to capture errors and render a fallback component if they occur. For example, we could wrap our entire application with an error boundary:

function ErrorScreen({ error }) {

//

// Here you can handle or track the error before rendering the message

//

return (

<div className="error">

<h3>We are sorry... something went wrong</h3>

<p>We cannot process your request at this moment.</p>

<p>ERROR: {error.message}</p>

</div>

);

}

<ErrorBoundary fallback={ErrorScreen}>

<App />

</ErrorBoundary>;

The ErrorScreen provides a gentle message for our users that an error has occurred. It renders some details about the error. It also gives us a place to potentially track errors that occur anywhere within our app. If an error does occur within the app, this component will be rendered instead of a black screen. We can make this component look nice with a little CSS:

.error {

background-color: #efacac;

border: double 4px darkred;

color: darkred;

padding: 1em;

}

To test this out we're going to create a component we can use to intentionally cause errors. BreakThings always throws an error: const BreakThings = () => {

throw new Error("We intentionally broke something");

};

Error boundaries can be composed. Sure, we wrapped the App component in an ErrorBoundary, but we can also wrap individual components within the App with Error:

return (

<SiteLayout

menu={

<ErrorBoundary fallback={ErrorScreen}>

<p>Site Layout Menu</p>

<BreakThings />

</ErrorBoundary>

}

>

<ErrorBoundary fallback={ErrorScreen}>

<Callout>Callout<BreakThings /></Callout>

</ErrorBoundary>

<ErrorBoundary fallback={ErrorScreen}>

<h1>Contents</h1>

<p> this is the main part of the example layout</p>

</ErrorBoundary>

</SiteLayout>

Each ErrorBoundary will render a fallback if an error occurs anywhere within their children. In this case, we used the BreakThings component in the menu and within the Callout. This would result in rendering the ErrorScreen twice, as we can see in Figure 9-2.

We can see that the ErrorBoundaries are rendered in place. Notice that the two errors that have occurred have been contained to their regions. The boundaries are like walls that prevent these errors from attacking the rest of the application. Despite intentionally throwing two errors, the contents are still rendered without issue.

Figure 9-2. ErrorBoundaries

In Figure 9-3, we can observe what happens when we move the BreakThings component to only the contents.

Figure 9-3. Error

Now we see the menu and the callout being rendered without issue, but the contents has rendered an error to notify the user that an error has occurred.

Inside of the render method in the ErrorBoundary class component, we can make the fallback property optional. When it's not included, we'll simply use our ErrorScreen component:

render() {

const { error } = this.state;

const { children } = this.props;

if (error && !fallback) return <ErrorScreen error={error} />; if (error) return <fallback error={error} />; return children;

}

This is a good solution for handling errors consistently across an application. Now, we just have to wrap specific parts of our component tree with an ErrorBoundary and let the component handle the rest:

<ErrorBoundary>

<h1>&lt;Contents /&gt;</h1>

<p> this is the main part of the example layout</p>

<BreakThings />

</ErrorBoundary>

Error boundaries are not only a good idea — they're essential for retaining users in production, and they'll prevent some small bug in a relatively unimportant component from bringing down the entire application.

Code Splitting

If the applications you're working on are small now, chances are they won't stay that way. A lot of the applications you work on will eventually contain massive codebases with hundreds, maybe even thousands, of components. Most of your users could be accessing your applications via their phones on potentially slow networks. They can't wait for the entire codebase of your application to successfully download before React completes its first render.

Code splitting provides us with a way to split our codebase into manageable chunks and then load those chunks as they're needed. To exemplify the power of code splitting, we'll add a user agreement screen to our application:

export default function Agreement({ onAgree = f => f }) {

return (

<div>

<p>Terms...</p>

<p>These are the terms and stuff. Do you agree?</p>

<button onClick={onAgree}>I agree</button>

</div>

);

}

Next, we'll move the rest of our codebase from a component called App to a component called Main, and we'll place that component in its own file:

import React from "react";

import ErrorBoundary from "./ErrorBoundary"; const SiteLayout = ({ children, menu = c => null }) => {

return (

<div className="site-container">

<div>{menu}</div>

<div>{children}</div>

</div>

);

};

const Menu = () => (

<ErrorBoundary>

<p style={{ color: "white" }}>TODO: Build Menu</p>

</ErrorBoundary>

);

const Callout = ({ children }) => (

<ErrorBoundary>

<div className="callout">{children}</div>

</ErrorBoundary>

);

export default function Main() {

return (

<SiteLayout menu={<Menu />}>

<Callout>Welcome to the site</Callout>

<ErrorBoundary>

<h1>TODO: Home Page</h1>

<p>Complete the main contents for this home page</p>

</ErrorBoundary>

</SiteLayout>

);

}

So Main is where the current site layout is rendered. Now we'll modify the App component to render the Agreement until the user agrees to it.

When they agree, we'll unmount the Agreement component and render the Main website component:

import React, { useState } from "react"; import Agreement from "./Agreement";

import Main from "./Main";

import "./SiteLayout.css";

export default function App() {

const [agree, setAgree] = useState(false);

if (!agree)

return <Agreement onAgree={() => setAgree(true)} />; return <Main />;

}

Initially, the only component that's rendered is the Agreement component. Once the user agrees, the value for agree changes to true, and the Main component is rendered. The issue is that all code for the Main component and all of its children is packaged into a single JavaScript file: the bundle. That means that users have to wait for this codebase to download completely before the Agreement component is initially rendered.

We can put off loading the main component until it has rendered by declaring it using React.lazy instead of initially importing it: const Main = React.lazy(() => import("./Main")); We're telling React to wait to load the codebase for the Main component until it's initially rendered. When it is rendered, it will be imported at that time using the import function.

Importing code during runtime is just like loading anything else from the internet. First, the request for the JavaScript code is pending. Then it's either successful, and a JavaScript file is returned, or it fails, causing an error to occur. Just like we need to notify a user that we're in the process of loading data, we'll need to let the user know that we're in the process of loading code.

Introducing: The Suspense Component

Once again, we find ourselves in a situation where we're managing an asynchronous request. This time, we have the Suspense component to help us out. The Suspense component works much like the

ErrorBoundary component. We wrap it around specific components in our tree. Instead of falling back to an error message when an error occurs, the Suspense component renders a loading message when lazy loading occurs.

We can modify the app to lazy load the Main component with the following code:

import React, { useState, Suspense, lazy } from "react"; import Agreement from "./Agreement";

import ClimbingBoxLoader from "react-spinners/ClimbingBoxLoader"; const Main = lazy(() => import("./Main")); export default function App() {

const [agree, setAgree] = useState(false);

if (!agree)

return <Agreement onAgree={() => setAgree(true)} />; return (

<Suspense fallback={<ClimbingBoxLoader />}>

<Main />

</Suspense>

);

}

Now the app initially only loads the codebase for React, the Agreement component, and the ClimbingBoxLoader. React will hold off on loading the Main component until the user agrees to the agreement.

The Main component has been wrapped in a Suspense component. As soon as the user agrees to the agreement, we start loading the codebase for the Main component. Because the request for this codebase is pending, the Suspense component will render the

ClimbingBoxLoader in its place until the codebase has successfully loaded. Once that happens, the Suspense component will unmount the ClimbingBoxLoader and render the Main component.

NOTE

React Spinners is a library of animated loading spinners that indicate that something is loading or that the app is working. For the remainder of this chapter, we'll be sampling different loader components from this library. Make sure you

install this library: npm i react-spinners.

What happens when the internet connection goes down before trying to load the Main component? Well, we'll have an error on our hands. We can handle that by wrapping our Suspense component within an ErrorBoundary:

<ErrorBoundary fallback={ErrorScreen}>

<Suspense fallback={<ClimbingBoxLoader />}>

<Main />

</Suspense>

</ErrorBoundary>

The composition of these three components gives us a way to handle most asynchronous requests. We have a solution for pending: the Suspense component will render a loader animation while the request for the source code is pending. We have a solution for the failed state: if an error occurs while loading the Main component, it will be caught and handled by the ErrorBoundary. We even have a solution for success: if the request is successful, we'll render the Main component.

Using Suspense with Data

In the last chapter, we built a useFetch hook and a Fetch component to help us handle the three states involved with making a GitHub request: pending, success, and fail. That was our solution. We think it was pretty cool. However, in the last section, we handled these three states by elegantly composing the ErrorBoundary and Suspense components. That was for lazy loading JavaScript source code, but we can use the same pattern to help us load data.

Let's say we have a Status component that's capable of rendering some sort of status message:

import React from "react";

const loadStatus = () => "success - ready"; function Status() {

const status = loadStatus();

return <h1>status: {status}</h1>;

}

This component invokes the loadStatus function to retrieve the current status message. We can render the Status component in our App component:

export default function App() {

return (

<ErrorBoundary>

<Status />

</ErrorBoundary>

);

}

If we were to run this code as-is, we would see our successful status message, as shown in Figure 9-4.

Figure 9-4. Success: everything works

When we rendered the Status component within the App component, we were good React developers because we wrapped the Status component inside of an error boundary. Now if something goes wrong while loading the status, the ErrorBoundary will fall back to the default error screen. To demonstrate this, let's cause an error inside of the loadStatus function:

const loadStatus = () => {

throw new Error("something went wrong");

};

Now when we run our application, we see the expected output. The ErrorBoundary caught our error and rendered a message to the user instead (Figure 9-5).

Figure 9-5. Fail: error boundary triggered

So far, everything is working as suspected. We've composed the Status component inside of an ErrorBoundary, and the combination of these two components is handling two of the three promise states: success or rejected.「Rejected」is the official promise term for a failed or error state.

We have two of the three states covered. What about the third state?

Pending? That state can be triggered by throwing a promise: const loadStatus = () => {

throw new Promise(resolves => null);

};

If we throw a promise from the loadStatus function, we'll see a special type of error in the browser (Figure 9-6).

This error is telling us that a pending state was triggered, but there is no Suspense component configured somewhere higher in the tree.

Whenever we throw a promise from a React app, we need a Suspense component to handle rendering a fallback:

export default function App() {

return (

<Suspense fallback={<GridLoader />}>

<ErrorBoundary>

<Status />

</ErrorBoundary>

</Suspense>

);

}

Figure 9-6. Throw promise

Now we have the right component composition to handle all three states. The loadStatus function is still throwing a promise, but there's now a Suspense component configured somewhere higher in the tree to handle it. When we throw the promise, we're telling React that we're

waiting on a pending promise. React responds by rendering the fallback GridLoader component (Figure 9-7).

Figure 9-7. GridLoader

When loadStatus successfully returns a result, we'll render the Status component as planned. If something goes wrong (if

loadStatus throws an error), we have it covered with an

ErrorBoundary. When loadStatus throws a promise, we trigger the pending state, which is handled by the Suspense component.

This is a pretty cool pattern, but wait…what do you mean,「throw a promise」?

Throwing Promises

In JavaScript, the throw keyword is technically for errors. You've probably used it many times in your own code:

throw new Error("inspecting errors");

This line of code causes an error. When this error goes unhandled, it crashes the whole app, as demonstrated in Figure 9-8.

Figure 9-8. Throwing an error

The error screen you see rendered in the browser is a development-mode feature of Create React App. Whenever you're in development mode, unhandled errors are caught and displayed directly on the screen. If you close this screen by clicking on the「X」in the upper right-hand corner, you'll see what your production users see when there's an error: nothing, a blank, white screen.

Unhandled errors are always visible in the console. All the red text we see in the console is information about the error we've thrown.

JavaScript is a pretty free-loving language. It lets us get away with a lot

of stuff that we can't get away with when using traditional typed languages. For example, in JavaScript, we can throw any type: throw "inspecting errors";

Here, we've thrown a string. The browser will tell us that something has gone uncaught, but it's not an error (Figure 9-9).

Figure 9-9. GridLoader

This time, when we threw a string, the Create React App error screen wasn't rendered inside the browser. React knows the difference between an error and a string.

JavaScript lets us throw any type, which means we can throw a promise:

throw new Promise(resolves => null);

Now the browser is telling us that something has gone uncaught. It's not an error, it's a promise, as shown in Figure 9-10.

Figure 9-10. Throwing a promise

To throw a promise within the React component tree, we'll do so first in a loadStatus function:

const loadStatus = () => {

console.log("load status");

throw new Promise(resolves => setTimeout(resolves, 3000));

};

If we use this loadStatus function inside a React component, a promise is thrown, then somewhere farther up the tree is caught by the Suspense component. That's right: JavaScript allows us to throw any type, which also means that we can catch any type.

Consider the following example:

safe(loadStatus);

function safe(fn) {

try {

fn();

} catch (error) {

if (error instanceof Promise) {

error.then(() => safe(fn));

} else {

throw error;

}

}

}

We're sending the loadStatus function a safe function, which makes safe a higher-order function. loadStatus becomes fn within the scope of the safe function. The safe function tries to invoke the fn that's passed as the argument. In this case, safe tries to invoke loadStatus. When it does, loadStatus throws a promise, an intentional delay of three seconds. That promise is immediately caught and becomes error within the scope of the catch block. We can check to see if the error is a promise, and in this case, it is. Now we can wait for that promise to resolve and then attempt to call safe again with the same loadStatus function.

What do we expect to happen when we invoke the safe function recursively with a function that creates a promise that causes a three-second delay? We get a delayed loop, as shown in Figure 9-11.

Figure 9-11. An unfortunate loop

The safe function is invoked, the promise is caught, we wait three seconds for the promise to resolve, then we call safe again with the same function, and the cycle starts all over again. Every three seconds, the string「load status」is printed to the console. How many times you watch that happen depends upon how patient you are.

We didn't make this endless recursive loop to test your patience; we made it to demonstrate a point. Watch what happens when we use this new loadStatus function in conjunction with our Status component from earlier:

const loadStatus = () => {

console.log("load status");

throw new Promise(resolves => setTimeout(resolves, 3000));

};

function Status() {

const status = loadStatus();

return <h1>status: {status}</h1>;

}

export default function App() {

return (

<Suspense fallback={<GridLoader />}>

<ErrorBoundary>

<Status />

</ErrorBoundary>

</Suspense>

);

}

Because loadStatus is throwing a promise, the GridLoader

animation renders on the screen. When you take a look at the console,

the results are once again testing your patience (Figure 9-12).

Figure 9-12. Suspense recursion

We see the same pattern as we did with the safe function. The Suspense component knows that a promise was thrown. It will render the fallback component. Then the Suspense component waits for the thrown promise to be resolved, just like the safe function did. Once resolved, the Suspense component rerenders the Status component.

When Status renders again, it calls loadStatus and the whole process repeats itself. We see「load status」printed to the console, every three seconds, endlessly, forever.

An endless loop is typically not the desired output. It isn't for React, either. It's important to know that, when we throw a promise, it's caught by the Suspense component, and we enter into a pending state until the promise has been resolved.

Building Suspenseful Data Sources

A Suspenseful data source needs to provide a function that handles all the states associated with loading data: pending, success, and error. The loadStatus function can only return or throw one type at a time. We need the loadStatus function to throw a promise when the data is loading, return a response when the data is successful, or throw an error if something goes wrong:

function loadStatus() {

if (error) throw error;

if (response) return response;

throw promise;

}

We'll need a place to declare error, response, and promise. We also need to make sure that these variables are scoped appropriately and do not collide with other requests. The solution is to define loadStatus using a closure:

const loadStatus = (function() {

let error, promise, response;

return function() {

if (error) throw error;

if (response) return response;

throw promise;

};

})();

This is a closure. The scope of the error, promise, and response are closed off from any code outside of the function where they're defined.

When we declare loadStatus, an anonymous function is declared and

immediately invoked: fn() is the same as (fn)(). The value of loadStatus becomes the inner function that's returned. The loadStatus function now has access to error, promise, and response, but the rest of our JavaScript world does not.

Now all we need to do is handle the values for error, response, and promise. The promise will be pending for three seconds before it's successfully resolved. When the promise resolves, the value for response will be set to「success.」We'll catch any errors or promise rejections and use them to set the error value:

const loadStatus = (function() {

let error, response;

const promise = new Promise(resolves =>

setTimeout(resolves, 3000)

)

.then(() => (response = "success"))

. catch(e => (error = e));

return function() {

if (error) throw error;

if (response) return response;

throw pending;

};

})();

We created a promise that's pending for three seconds. If the loadStatus function is invoked at any point during that time, the promise itself will be thrown. After the three seconds, the promise is successfully resolved and response is assigned a value. If you invoke loadStatus now, it will return the response:「success.」If something went wrong, then the loadStatus function would return the error.

The loadStatus function is our Suspenseful data source. It is capable of communicating its state with the Suspense architecture. The inner workings of loadStatus are hardcoded. It always resolves the same three-second delay promise. However, the mechanics of handling error, response, and promise are repeatable. We can wrap any promise with this technique to produce suspenseful data sources.

All we need to create a Suspenseful data source is a promise, so we can create a function that takes a promise as an argument and returns a Suspenseful data source. In this example, we call that function createResource:

const resource = createResource(promise);

const result = resource.read();

This code assumes that createResource(promise) will successfully create a resource object. This object has a read function, and we can invoke read as many times as we like. When the promise is resolved, read will return the resulting data. When the promise is pending, read will throw the promise. And if anything goes wrong, read will throw an error. This data source is ready to work with Suspense.

The createResource function looks a lot like our anonymous function from before:

function createResource(pending) {

let error, response;

pending.then(r => (response = r)). catch(e => (error = e)); return {

read() {

if (error) throw error;

if (response) return response;

throw pending;

}

};

}

This function still closes off the values for error and response, but it allows consumers to pass in a promise as an argument called pending.

When the pending promise is resolved, we capture the results with a

.then function. If the promise is rejected, we'll catch the error and use it to assign a value to the error variable.

The createResource function returns a resource object. This object contains a function called read. If the promise is still pending, then error and response will be undefined. So read throws the promise.

Invoking read when there's a value for error will cause that error to be thrown. Finally, invoking read when there's a response will yield whatever data was resolved by the promise. It doesn't matter how many times we call read — it will always accurately report on the state of our promise.

In order to test it out in a component, we'll need a promise, ideally one that sounds like the name of an '80s ski movie:

const threeSecondsToGnar = new Promise(resolves => setTimeout(() => resolves({ gnar: "gnarly!" }), 3000)

);

The threeSecondsToGnar promise waits three seconds before resolving to an object that has a field and value for gnar. Let's use this promise to create a Suspenseful data resource and use that data resource in a small React application:

const resource = createResource(threeSecondsToGnar); function Gnar() {

const result = resource.read();

return <h1>Gnar: {result.gnar}</h1>;

}

export default function App() {

return (

<Suspense fallback={<GridLoader />}>

<ErrorBoundary>

<Gnar />

</ErrorBoundary>

</Suspense>

);

}

React components can render a lot. The Gnar component will be rendered several times before it actually returns a response. Each time Gnar is rendered, resource.read() is invoked. The first time Gnar is rendered, a promise is thrown. That promise is handled by the Suspense component and a fallback component will be rendered.

When the promise has resolved, the Suspense component will attempt to render Gnar again. Gnar will invoke resource.read() again, but this time, assuming everything went OK, resource.read() will successfully return Gnar, which is used to render the state of Gnar in an h1 element. If something went wrong, resource.read() would have thrown an error, which would be handed by the ErrorBoundary.

As you can imagine, the createResource function can become quite robust. Our resource can attempt to handle errors. Maybe when there's a network error, the resource can wait a few seconds and automatically attempt to load the data again. Our resource could communicate with

other resources. Maybe we can log the performance statistics behind all of our resources. The sky's the limit. As long as we have a function that we can use to read the current state of that resource, we can do whatever we like with the resource itself.

At present, this is how Suspense works. This is how we can use the Suspense component with any type of asynchronous resource. This could all change, and we expect it to change. However, whatever the finalized API for Suspense ends up being, it will be sure to handle three states: pending, success, and fail.

The look at these Suspense APIs has been kind of high-level, and this was intentional because this stuff is experimental. It's going to change.

What's important to take away from this chapter is that React is always tinkering with ways to make React apps faster.

Behind the scenes of a lot of this work is the way that React itself works — specifically, its reconciliation algorithm called Fiber.

Fiber

Throughout this book, we've talked about React components as being functions that return data as a UI. Every time this data changes (props, state, remote data, etc), we rely on React to rerender the component. If we click a star to rate a color, we assume that our UI will change, and we assume that it'll happen fast. We assume this because we trust React to make it happen. How exactly does this work though? To understand how React efficiently updates the DOM, let's take a closer look at how React works.

Consider that you're writing an article for your company blog. You want feedback, so you send the article to your coworker before you publish. They recommend a few quick changes, and now you need to incorporate those changes. You create a brand-new document, type out the entire article from scratch, and then add in the edits.

You're probably groaning at this unnecessary extra effort, but this is how a lot of libraries previously worked. To make an update, we'd get rid of everything, then start from scratch and rebuild the DOM during the update.

Now, you're writing another blog post and you send it to your coworker again. This time, you've modernized your article-writing process to use GitHub. Your coworker checks out a GitHub branch, makes the changes, and merges in the branch when they're finished.

Faster and more efficient.

This process is similar to how React works. When a change occurs, React makes a copy of the component tree as a JavaScript object. It looks for the parts of the tree that need to change and changes only those parts. Once complete, the copy of the tree (known as the work-in-progress tree) replaces the existing tree. It's important to reiterate that it uses the parts of the tree that are already there. For example, if we had to update an item in the list from red to green:

<ul>

<li>blue</li>

<li>purple</li>

<li>red</li>

</ul>

React would not get rid of the third li. Instead it would replace its children (red text) with green text. This is an efficient approach to updating and is the way that React has updated the DOM since its inception. There is a potential problem here, though. Updating the DOM is an expensive task because it's synchronous. We have to wait for all of the updates to be reconciled and then rendered before we can do other tasks on the main thread. In other words, we'd have to wait for React to recursively move through all of the updates, which could make the user experience seem unresponsive.

The React team's solution to this was a full rewrite of React's reconciliation algorithm, called Fiber. Fiber, released in version 16.0, rewrote the way that DOM updates worked by taking a more

asynchronous approach. The first change with 16.0 was the separation of the renderer and the reconciler. A renderer is the part of the library that handles rendering, and the reconciler is the part of the library that manages updates when they occur.

Separating the renderer from the reconciler was a big deal. The reconciliation algorithm was kept in React Core (the package you install to use React), and each rendering target was made responsible for rendering. In other words, ReactDOM, React Native, React 360, and more would be responsible for the logic of rendering and could be plugged into React's core reconciliation algorithm.

Another huge shift with React Fiber was its changes to the reconciliation algorithm. Remember our expensive DOM updates that blocked the main thread? This lengthy block of updates is called work

 — with Fiber, React split the work into smaller units of work called

fibers. A fiber is a JavaScript object that keeps track of what it's reconciling and where it is in the updating cycle.

Once a fiber (unit of work) is complete, React checks in with the main thread to make sure there's not anything important to do. If there is important work to do, React will give control to the main thread. When it's done with that important work, React will continue its update. If there's nothing critical to jump to on the main thread, React moves on to the next unit of work and renders those changes to the DOM.

To use the GitHub example from earlier, each fiber represents a commit on a branch, and when we check the branch back into the main branch, that represents the updated DOM tree. By breaking up the work of an update into chunks, Fiber allows priority tasks to jump the line for immediate handling by the main thread. The result is a user experience that feels more responsive.

If this was all Fiber did, it would be a success, but there's even more to it than that! In addition to the performance benefits of breaking work into smaller units, the rewrite also sets up exciting possibilities for the future. Fiber provides the infrastructure for prioritizing updates. In the longer term, the developer may even be able to tweak the defaults and decide which types of tasks should be given the highest priority. The process of prioritizing units of work is called scheduling; this concept underlies the experimental concurrent mode, which will eventually allow these units of work to be performed in parallel.

An understanding of Fiber is not vital to working with React in production, but the rewrite of its reconciliation algorithm provides interesting insight into how React works and how its contributors are thinking about the future.