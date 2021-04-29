# 0701. Enhancing Components with Hooks

Rendering is the heartbeat of a React application. When something changes (props, state), the component tree rerenders, reflecting the latest data as a user interface. So far, useState has been our workhorse for describing how our components should be rendering. But we can do more. There are more Hooks that define rules about why and when rendering should happen. There are more Hooks that enhance rendering performance. There are always more Hooks to help us out.

In the last chapter, we introduced useState, useRef, and useContext, and we saw that we could compose these Hooks into our own custom Hooks: useInput and useColors. There's more where that came from, though. React comes with more Hooks out of the box. In this chapter, we're going to take a closer look at useEffect, useLayoutEffect, and useReducer. All of these are vital when building applications.

We'll also look at useCallback and useMemo, which can help optimize our components for performance.

Introducing useEffect

We now have a good sense of what happens when we render a component. A component is simply a function that renders a user interface. Renders occur when the app first loads and when props and

state values change. But what happens when we need to do something after a render? Let's take a closer look.

Consider a simple component, the Checkbox. We're using useState to set a checked value and a function to change the value of checked: setChecked. A user can check and uncheck the box, but how might we alert the user that the box has been checked? Let's try this with an alert, as it's a great way to block the thread:

import React, { useState } from "react"; function Checkbox() {

const [checked, setChecked] = useState(false); alert(`checked: ${checked.toString()}`);

return (

<>

<input

type="checkbox"

value={checked}

onChange={() => setChecked(checked => !checked)}

/>

{checked ? "checked" : "not checked"}

</>

);

};

We've added the alert before the render to block the render. The component will not render until the user clicks the OK button on the alert box. Because the alert is blocking, we don't see the next state of the checkbox rendered until clicking OK.

That isn't the goal, so maybe we should place the alert after the return?

function Checkbox {

const [checked, setChecked] = useState(false); return (

<>

<input

type="checkbox"

value={checked}

onChange={() => setChecked(checked => !checked)}

/>

{checked ? "checked" : "not checked"}

</>

);

alert(`checked: ${checked.toString()}`);

};

Scratch that. We can't call alert after the render because the code will never be reached. To ensure that we see the alert as expected, we can use useEffect. Placing the alert inside of the useEffect function means that the function will be called after the render, as a side effect: function Checkbox {

const [checked, setChecked] = useState(false); useEffect(() => {

alert(`checked: ${checked.toString()}`);

});

return (

<>

<input

type="checkbox"

value={checked}

onChange={() => setChecked(checked => !checked)}

/>

{checked ? "checked" : "not checked"}

</>

);

};

We use useEffect when a render needs to cause side effects. Think of a side effect as something that a function does that isn't part of the return. The function is the Checkbox. The Checkbox function renders UI. But we might want the component to do more than that. Those things we want the component to do other than return UI are called effects.

An alert, a console.log, or an interaction with a browser or native API is not part of the render. It's not part of the return. In a React app, though, the render affects the results of one of these events. We can use useEffect to wait for the render, then provide the values to an alert or a console.log:

useEffect(() => {

console.log(checked ? "Yes, checked" : "No, not checked");

});

Similarly, we could check in with the value of checked on render and then set that to a value in localStorage:

useEffect(() => {

localStorage.setItem("checkbox-value", checked);

});

We might also use useEffect to focus on a specific text input that has been added to the DOM. React will render the output, then call useEffect to focus the element:

useEffect(() => {

txtInputRef.current.focus();

});

On render, the txtInputRef will have a value. We can access that value in the effect to apply the focus. Every time we render, useEffect has access to the latest values from that render: props, state, refs, etc.

Think of useEffect as being a function that happens after a render.

When a render fires, we can access the current state values within our component and use them to do something else. Then, once we render again, the whole thing starts over. New values, new renders, new effects.

The Dependency Array

useEffect is designed to work in conjunction with other stateful Hooks like useState and the heretofore unmentioned useReducer, which we promise to discuss later in the chapter. React will rerender the component tree when the state changes. As we've learned, useEffect will be called after these renders.

Consider the following, where the App component has two separate state values:

import React, { useState, useEffect } from "react"; import "./App.css";

function App() {

const [val, set] = useState("");

const [phrase, setPhrase] = useState("example phrase"); const createPhrase = () => {

setPhrase(val);

set("");

};

useEffect(() => {

console.log(`typing "${val}"`);

});

useEffect(() => {

console.log(`saved phrase: "${phrase}"`);

});

return (

<>

<label>Favorite phrase:</label>

<input

value={val}

placeholder={phrase}

onChange={e => set(e.target.value)}

/>

<button onClick={createPhrase}>send</button>

</>

);

}

val is a state variable that represents the value of the input field. The val changes every time the value of the input field changes. It causes the component to render every time the user types a new character.

When the user clicks the Send button, the val of the text area is saved as the phrase, and the val is reset to "", which empties the text field.

This works as expected, but the useEffect hook is invoked more times than it should be. After every render, both useEffect Hooks are called:

typing "" // First Render saved phrase: "example phrase" // First Render typing "S" // Second Render saved phrase: "example phrase" // Second Render typing "Sh" // Third Render saved phrase: "example phrase" // Third Render

typing "Shr" // Fourth Render saved phrase: "example phrase" // Fourth Render typing "Shre" // Fifth Render saved phrase: "example phrase" // Fifth Render typing "Shred" // Sixth Render saved phrase: "example phrase" // Sixth Render We don't want every effect to be invoked on every render. We need to associate useEffect hooks with specific data changes. To solve this problem, we can incorporate the dependency array. The dependency array can be used to control when an effect is invoked:

useEffect(() => {

console.log(`typing "${val}"`);

}, [val]);

useEffect(() => {

console.log(`saved phrase: "${phrase}"`);

}, [phrase]);

We've added the dependency array to both effects to control when they're invoked. The first effect is only invoked when the val value has changed. The second effect is only invoked when the phrase value has changed. Now, when we run the app and take a look at the console, we'll see more efficient updates occurring:

typing "" // First Render saved phrase: "example phrase" // First Render typing "S" // Second Render typing "Sh" // Third Render typing "Shr" // Fourth Render typing "Shre" // Fifth Render typing "Shred" // Sixth Render typing "" // Seventh Render saved phrase: "Shred" // Seventh Render Changing the val value by typing into the input only causes the first

effect to fire. When we click the button, the phrase is saved and the val is reset to "".

It's an array after all, so it's possible to check multiple values in the dependency array. Let's say we wanted to run a specific effect any time either the val or phrase has changed:

useEffect(() => {

console.log("either val or phrase has changed");

}, [val, phrase]);

If either of those values changes, the effect will be called again. It's also possible to supply an empty array as the second argument to a useEffect function. An empty dependency array causes the effect to be invoked only once after the initial render:

useEffect(() => {

console.log("only once after initial render");

}, []);

Since there are no dependencies in the array, the effect is invoked for the initial render. No dependencies means no changes, so the effect will never be invoked again. Effects that are only invoked on the first render are extremely useful for initialization:

useEffect(() => {

welcomeChime.play();

}, []);

If you return a function from the effect, the function will be invoked when the component is removed from the tree:

useEffect(() => {

welcomeChime.play();

return () => goodbyeChime.play();

}, []);

This means that you can use useEffect for setup and teardown. The empty array means that the welcome chime will play once on first render. Then, we'll return a function as a cleanup function to play a goodbye chime when the component is removed from the tree.

This pattern is useful in many situations. Perhaps we'll subscribe to a news feed on first render. Then we'll unsubscribe from the news feed with the cleanup function. More specifically, we'll start by creating a state value for posts and a function to change that value, called setPosts. Then we'll create a function, addPosts, that will take in the newest post and add it to the array. Then we can use useEffect to subscribe to the news feed and play the chime. Plus, we can return the cleanup functions, unsubscribing and playing the goodbye chime: const [posts, setPosts] = useState([]);

const addPost = post => setPosts(allPosts => [post, ...allPosts]); useEffect(() => {

newsFeed.subscribe(addPost);

welcomeChime.play();

return () => {

newsFeed.unsubscribe(addPost);

goodbyeChime.play();

};

}, []);

This is a lot going on in useEffect, though. We might want to use a separate useEffect for the news feed events and another useEffect

for the chime events:

useEffect(() => {

newsFeed.subscribe(addPost);

return () => newsFeed.unsubscribe(addPost);

}, []);

useEffect(() => {

welcomeChime.play();

return () => goodbyeChime.play();

}, []);

Splitting functionality into multiple useEffect calls is typically a good idea. But let's enhance this even further. What we're trying to create here is functionality for subscribing to a news feed that plays different jazzy sounds for subscribing, unsubscribing, and whenever there's a new post. Everyone loves lots of loud sounds right? This is a case for a custom hook. Maybe we should call it useJazzyNews:

const useJazzyNews = () => {

const [posts, setPosts] = useState([]);

const addPost = post => setPosts(allPosts => [post, ...allPosts]); useEffect(() => {

newsFeed.subscribe(addPost);

return () => newsFeed.unsubscribe(addPost);

}, []);

useEffect(() => {

welcomeChime.play();

return () => goodbyeChime.play();

}, []);

return posts;

};

Our custom hook contains all of the functionality to handle a jazzy news feed, which means that we can easily share this functionality with our components. In a new component called NewsFeed, we'll use the custom hook:

function NewsFeed({ url }) {

const posts = useJazzyNews();

return (

<>

<h1>{posts.length} articles</h1>

{posts.map(post => (

<Post key={post.id} {...post} />

))}

</>

);

}

Deep Checking Dependencies

So far, the dependencies we've added to the array have been strings.

JavaScript primitives like strings, booleans, numbers, etc., are comparable. A string would equal a string as expected:

if ("gnar" === "gnar") {

console.log("gnarly!!");

}

However, when we start to compare objects, arrays, and functions, the comparison is different. For example, if we compared two arrays: if ([1, 2, 3] !== [1, 2, 3]) {

console.log("but they are the same");

}

These arrays [1,2,3] and [1,2,3] are not equal, even though they look identical in length and in entries. This is because they are two different instances of a similar-looking array. If we create a variable to hold this array value and then compare, we'll see the expected output: const array = [1, 2, 3];

if (array === array) {

console.log("because it's the exact same instance");

}

In JavaScript, arrays, objects, and functions are the same only when they're the exact same instance. So how does this relate to the useEffect dependency array? To demonstrate this, we're going to need a component we can force to render as much as we want. Let's build a hook that causes a component to render whenever a key is pressed:

const useAnyKeyToRender = () => {

const [, forceRender] = useState();

useEffect(() => {

window.addEventListener("keydown", forceRender); return () => window.removeEventListener("keydown", forceRender);

}, []);

};

At minimum, all we need to do to force a render is invoke a state change function. We don't care about the state value. We only want the state function: forceRender. (That's why we added the comma using array destructuring. Remember, from Chapter 2?) When the component first renders, we'll listen for keydown events. When a key is pressed, we'll force the component to render by invoking forceRender. As

we've done before, we'll return a cleanup function where we stop listening to keydown events. By adding this hook to a component, we can force it to rerender simply by pressing a key.

With the custom hook built, we can use it in the App component (and any other component for that matter! Hooks are cool.):

function App() {

useAnyKeyToRender();

useEffect(() => {

console.log("fresh render");

});

return <h1>Open the console</h1>;

}

Every time we press a key, the App component is rendered. useEffect demonstrates this by logging「fresh render」to the console every time the App is rendered. Let's adjust useEffect in the App component to reference the word value. If word changes, we'll rerender: const word = "gnar";

useEffect(() => {

console.log("fresh render");

}, [word]);

Instead of calling useEffect on every keydown event, we would only call this after first render and any time the word value changes. It doesn't change, so subsequent rerenders don't occur. Adding a primitive or a number to the dependency array works as expected. The effect is invoked once.

What happens if instead of a single word, we use an array of words?

const words = ["sick", "powder", "day"]; useEffect(() => {

console.log("fresh render");

}, [words]);

The variable words is an array. Because a new array is declared with each render, JavaScript assumes that words has changed, thus invoking the「fresh render」effect every time. The array is a new instance each time, and this registers as an update that should trigger a rerender.

Declaring words outside of the scope of the App would solve the problem:

const words = ["sick", "powder", "day"]; function App() {

useAnyKeyToRender();

useEffect(() => {

console.log("fresh render");

}, [words]);

return <h1>component</h1>;

}

The dependency array in this case refers to one instance of words that's declared outside of the function. The「fresh render」effect does not get called again after the first render because words is the same instance as the last render. This is a good solution for this example, but it's not always possible (or advisable) to have a variable defined outside of the scope of the function. Sometimes the value passed to the dependency array requires variables in scope. For example, we might need to create

the words array from a React property like children: function WordCount({ children = "" }) {

useAnyKeyToRender();

const words = children.split(" ");

useEffect(() => {

console.log("fresh render");

}, [words]);

return (

<>

<p>{children}</p>

<p>

<strong>{words.length} - words</strong>

</p>

</>

);

}

function App() {

return <WordCount>You are not going to believe this but...</WordCount>;

}

The App component contains some words that are children of the WordCount component. The WordCount component takes in children as a property. Then we set words in the component equal to an array of those words that we've called .split on. We would hope that the component will rerender only if words changes, but as soon as we press a key, we see the dreaded「fresh render」words appearing in the console.

Let's replace that feeling of dread with one of calm, because the React team has provided us a way to avoid these extra renders. They

wouldn't hang us out to dry like that. The solution to this problem is, as you might expect, another hook: useMemo.

useMemo invokes a function to calculate a memoized value. In computer science in general, memoization is a technique that's used to improve performance. In a memoized function, the result of a function call is saved and cached. Then, when the function is called again with the same inputs, the cached value is returned. In React, useMemo allows us to compare the cached value against itself to see if it has actually changed.

The way useMemo works is that we pass it a function that's used to calculate and create a memoized value. useMemo will only recalculate that value when one of the dependencies has changed. First, let's import the useMemo hook:

import React, { useEffect, useMemo } from "react"; Then we'll use the function to set words:

const words = useMemo(() => {

const words = children.split(" ");

return words;

}, []);

useEffect(() => {

console.log("fresh render");

}, [words]);

useMemo invokes the function sent to it and sets words to the return value of that function. Like useEffect, useMemo relies on a dependency array:

const words = useMemo(() => children.split(" ")); When we don't include the dependency array with useMemo, the words are calculated with every render. The dependency array controls when the callback function should be invoked. The second argument sent to the useMemo function is the dependency array and should contain the children value:

function WordCount({ children = "" }) {

useAnyKeyToRender();

const words = useMemo(() => children.split(" "), [children]); useEffect(() => {

console.log("fresh render");

}, [words]);

return (...);

}

The words array depends on the children property. If children changes, we should calculate a new value for words that reflects that change. At that point, useMemo will calculate a new value for words when the component initially renders and if the children property changes.

The useMemo hook is a great function to understand when you're creating React applications.

useCallback can be used like useMemo, but it memoizes functions instead of values. For example:

const fn = () => {

console.log("hello");

console.log("world");

};

useEffect(() => {

console.log("fresh render");

fn();

}, [fn]);

fn is a function that logs「Hello」then「World.」It is a dependency of useEffect, but just like words, JavaScript assumes fn is different every render. Therefore, it triggers the effect every render. This yields a

「fresh render」for every key press. It's not ideal.

Start by wrapping the function with useCallback:

const fn = useCallback(() => {

console.log("hello");

console.log("world");

}, []);

useEffect(() => {

console.log("fresh render");

fn();

}, [fn]);

useCallback memoizes the function value for fn. Just like useMemo and useEffect, it also expects a dependency array as the second argument. In this case, we create the memoized callback once because the dependency array is empty.

Now that we have an understanding of the uses and differences between useMemo and useCallback, let's improve our useJazzyNews hook. Every time there's a new post, we'll call newPostChime.play().

In this hook, posts are an array, so we'll need to use useMemo to memoize the value:

const useJazzyNews = () => {

const [_posts, setPosts] = useState([]);

const addPost = post => setPosts(allPosts => [post, ...allPosts]); const posts = useMemo(() => _posts, [_posts]);

useEffect(() => {

newPostChime.play();

}, [posts]);

useEffect(() => {

newsFeed.subscribe(addPost);

return () => newsFeed.unsubscribe(addPost);

}, []);

useEffect(() => {

welcomeChime.play();

return () => goodbyeChime.play();

}, []);

return posts;

};

Now, the useJazzyNews hook plays a chime every time there's a new post. We made this happen with a few changes to the hook. First, const [posts, setPosts] was renamed to const [_posts,

setPosts]. We'll calculate a new value for posts every time _posts change.

Next, we added the effect that plays the chime every time the post array changes. We're listening to the news feed for new posts. When a new post is added, this hook is reinvoked with _posts reflecting that

new post. Then, a new value for post is memoized because _posts have changed. Then the chime plays because this effect is dependent on posts. It only plays when the posts change, and the list of posts only changes when a new one is added.

Later in the chapter, we'll discuss the React Profiler, a browser extension for testing performance and rendering of React components.

There, we'll dig into more detail about when to use useMemo and useCallback. (Spoiler alert: sparingly!)

When to useLayoutEffect

We understand that the render always comes before useEffect. The render happens first, then all effects run in order with full access to all of the values from the render. A quick look at the React docs will point out that there's another type of effect hook: useLayoutEffect.

useLayoutEffect is called at a specific moment in the render cycle. The series of events is as follows:

1. Render

2. useLayoutEffect is called

3. Browser paint: the time when the component's elements are actually added to the DOM

4. useEffect is called

This can be observed by adding some simple console messages: import React, { useEffect, useLayoutEffect } from "react"; function App() {

useEffect(() => console.log("useEffect")); useLayoutEffect(() => console.log("useLayoutEffect")); return <div>ready</div>;

}

In the App component, useEffect is the first hook, followed by useLayoutEffect. We see that useLayoutEffect is invoked before useEffect:

useLayoutEffect

useEffect

useLayoutEffect is invoked after the render but before the browser paints the change. In most circumstances, useEffect is the right tool for the job, but if your effect is essential to the browser paint (the appearance or placement of the UI elements on the screen), you may want to use useLayoutEffect. For instance, you may want to obtain the width and height of an element when the window is resized: function useWindowSize {

const [width, setWidth] = useState(0);

const [height, setHeight] = useState(0);

const resize = () => {

setWidth(window.innerWidth);

setHeight(window.innerHeight);

};

useLayoutEffect(() => {

window.addEventListener("resize", resize);

resize();

return () => window.removeEventListener("resize", resize);

}, []);

return [width, height];

};

The width and height of the window is information that your component may need before the browser paints. useLayoutEffect is used to calculate the window's width and height before the paint.

Another example of when to use useLayoutEffect is when tracking the position of the mouse:

function useMousePosition {

const [x, setX] = useState(0);

const [y, setY] = useState(0);

const setPosition = ({ x, y }) => {

setX(x);

setY(y);

};

useLayoutEffect(() => {

window.addEventListener("mousemove", setPosition); return () => window.removeEventListener("mousemove", setPosition);

}, []);

return [x, y];

};

It's highly likely that the x and y position of the mouse will be used when painting the screen. useLayoutEffect is available to help calculate those positions accurately before the paint.

Rules to Follow with Hooks

As you're working with Hooks, there are a few guidelines to keep in mind that can help avoid bugs and unusual behavior:

Hooks only run in the scope of a component

Hooks should only be called from React components. They can

also be added to custom Hooks, which are eventually added to components. Hooks are not regular JavaScript—they're a React pattern, but they're starting to be modeled and incorporated in other libraries.

It's a good idea to break functionality out into multiple Hooks In our earlier example with the Jazzy News component, we split everything related to subscriptions into one effect and everything related to sound effects into another effect. This immediately made the code easier to read, but there was another benefit to doing this.

Since Hooks are invoked in order, it's a good idea to keep them small. Once invoked, React saves the values of Hooks in an array so the values can be tracked. Consider the following component: function Counter() {

const [count, setCount] = useState(0);

const [checked, toggle] = useState(false);

useEffect(() => {

...

}, [checked]);

useEffect(() => {

...

}, []);

useEffect(() => {

...

}, [count]);

return ( ... )

}

The order of Hook calls is the same for each and every render:

[count, checked, DependencyArray, DependencyArray, DependencyArray]

Hooks should only be called at the top level

Hooks should be used at the top level of a React function. They cannot be placed into conditional statements, loops, or nested functions. Let's adjust the counter:

function Counter() {

const [count, setCount] = useState(0);

if (count > 5) {

const [checked, toggle] = useState(false);

}

useEffect(() => {

...

});

if (count > 5) {

useEffect(() => {

...

});

}

useEffect(() => {

...

});

return ( ... )

}

When we use useState within the if statement, we're saying that the hook should only be called when the count value is greater than 5. That will throw off the array values. Sometimes the array will be: [count, checked, DependencyArray, 0,

DependencyArray]. Other times: [count, DependencyArray,

1]. The index of the effect in that array matters to React. It's how values are saved.

Wait, so are we saying that we can never use conditional logic in React applications anymore? Of course not! We just have to organize these conditionals differently. We can nest if statements, loops, and other conditionals within the hook:

function Counter() {

const [count, setCount] = useState(0);

const [checked, toggle] =

useState(

count => (count < 5)

? undefined

: !c,

(count < 5) ? undefined

);

useEffect(() => {

...

});

useEffect(() => {

if (count < 5) return;

...

});

useEffect(() => {

...

});

return ( ... )

}

Here, the value for checked is based on the condition that the count is greater than 5. When count is less than 5, the value for checked is undefined. Nesting this conditional inside the hook means that the hook remains on the top level, but the result is similar. The second effect enforces the same rules. If the count is less than 5, the return statement will prevent the effect from continuing to execute. This keeps the hook values array intact:

[countValue, checkedValue, DependencyArray,

DependencyArray, DependencyArray].

Like conditional logic, you need to nest asynchronous behavior inside of a hook. useEffect takes a function as the first argument,

not a promise. So you can't use an async function as the first argument: useEffect(async () => {}). You can, however, create an async function inside of the nested function like this: useEffect(() => {

const fn = async () => {

await SomePromise();

};

fn();

});

We created a variable, fn, to handle the async/await, then we called the function as the return. You can give this function a name, or you can use async effects as an anonymous function:

useEffect(() => {

(async () => {

await SomePromise();

})();

});

If you follow these rules, you can avoid some common gotchas with React Hooks. If you're using Create React App, there's an ESLint plug-in included called eslint-plugin-react-hooks that provides warning hints if you're in violation of these rules.

Improving Code with useReducer

Consider the Checkbox component. This component is a perfect example of a component that holds simple state. The box is either

checked or not checked. checked is the state value, and setChecked is a function that will be used to change the state. When the component first renders, the value of checked will be false:

function Checkbox() {

const [checked, setChecked] = useState(false); return (

<>

<input

type="checkbox"

value={checked}

onChange={() => setChecked(checked => !checked)}

/>

{checked ? "checked" : "not checked"}

</>

);

}

This works well, but one area of this function could be cause for alarm: onChange={() => setChecked(checked => !checked)}

Look at it closely. It feels OK at first glance, but are we stirring up trouble here? We're sending a function that takes in the current value of checked and returns the opposite, !checked. This is probably more complex than it needs to be. Developers could easily send the wrong information and break the whole thing. Instead of handling it this way, why not provide a function as a toggle?

Let's add a function called toggle that will do the same thing: call setChecked and return the opposite of the current value of checked: function Checkbox() {

const [checked, setChecked] = useState(false);

function toggle() {

setChecked(checked => !checked);

}

return (

<>

<input type="checkbox" value={checked} onChange={toggle} />

{checked ? "checked" : "not checked"}

</>

);

}

This is better. onChange is set to a predictable value: the toggle function. We know what that function is going to do every time, everywhere it's used. We can still take this one step farther to yield even more predictable results each time we use the checkbox component. Remember the function we sent to setChecked in the toggle function?

setChecked(checked => !checked);

We're going to refer to this function, checked => !checked, by a different name now: a reducer. A reducer function's most simple definition is that it takes in the current state and returns a new state. If checked is false, it should return the opposite, true. Instead of hardcoding this behavior into onChange events, we can abstract the logic into a reducer function that will always produce the same results.

Instead of useState in the component, we'll use useReducer: function Checkbox() {

const [checked, toggle] = useReducer(checked => !checked, false); return (

<>

<input type="checkbox" value={checked} onChange={toggle} />

{checked ? "checked" : "not checked"}

</>

);

}

useReducer takes in the reducer function and the initial state, false.

Then, we'll set the onChange function to setChecked, which will call the reducer function.

Our earlier reducer, checked => !checked, is a prime example of this. If the same input is provided to a function, the same output should be expected. This concept originates with Array.reduce in JavaScript.

reduce fundamentally does the same thing as a reducer: it takes in a function (to reduce all of the values into a single value) and an initial value and returns one value.

Array.reduce takes in a reducer function and an initial value. For each value in the numbers array, the reducer is called until one value is returned:

const numbers = [28, 34, 67, 68];

numbers.reduce((number, nextNumber) => number + nextNumber, 0); // 197

The reducer sent to Array.reduce takes in two arguments. You can also send multiple arguments to a reducer function:

function Numbers() {

const [number, setNumber] = useReducer(

(number, newNumber) => number + newNumber,

0

);

return <h1 onClick={() => setNumber(30)}>{number}</h1>;

}

Every time we click on the h1, we'll add 30 to the total.

useReducer to Handle Complex State

useReducer can help us handle state updates more predictably as state becomes more complex. Consider an object that contains user data: const firstUser = {

id: "0391-3233-3201",

firstName: "Bill",

lastName: "Wilson",

city: "Missoula",

state: "Montana",

email: "bwilson@mtnwilsons.com",

admin: false

};

Then we have a component called User that sets the firstUser as the initial state, and the component displays the appropriate data: function User() {

const [user, setUser] = useState(firstUser);

return (

<div>

<h1>

{user.firstName} {user.lastName} - {user.admin ? "Admin" :

"User"}

</h1>

<p>Email: {user.email}</p>

<p>

Location: {user.city}, {user.state}

</p>

<button>Make Admin</button>

</div>

);

}

A common error when managing state is to overwrite the state:

<button

onClick={() => {

setUser({ admin: true });

}}

>

Make Admin

</button>

Doing this would overwrite state from firstUser and replace it with just what we sent to the setUser function: {admin: true}. This can be fixed by spreading the current values from user, then overwriting the admin value:

<button

onClick={() => {

setUser({ ...user, admin: true });

}}

>

Make Admin

</button>

This will take the initial state and push in the new key/values: {admin: true}. We need to rewrite this logic in every onClick, making it prone to error (we might forget to do this when we come back to the app tomorrow):

function User() {

const [user, setUser] = useReducer(

(user, newDetails) => ({ ...user, ...newDetails }),

firstUser

);

...

}

Then we'll send the new state value, newDetails, to the reducer, and it will be pushed into the object:

<button

onClick={() => {

setUser({ admin: true });

}}

>

Make Admin

</button>

This pattern is useful when state has multiple subvalues or when the next state depends on a previous state. Teach everyone to spread, they'll spread for a day. Teach everyone to useReducer and they'll spread for life.

LEGACY SETSTATE AND USEREDUCER

In previous versions of React, we used a function called setState to update state. Initial state would be assigned in the constructor as an object:

class User extends React.Component {

constructor(props) {

super(props);

this.state = {

id: "0391-3233-3201",

firstName: "Bill",

lastName: "Wilson",

city: "Missoula",

state: "Montana",

email: "bwilson@mtnwilsons.com",

admin: false

};

}

}

<button onSubmit={() =>

{this.setState({admin: true });}}

Make Admin

</button>

The older incarnation of setState merged state values. The same is true of useReducer: const [state, setState] = useReducer(

(state, newState) =>

({...state, ...newState}),

initialState);

<button onSubmit={() =>

{setState({admin: true });}}

Make Admin

</button>

</div>);

If you like this pattern, you can use legacy-set-state npm or useReducer.

The past few examples are simple applications for a reducer. In the next chapter, we'll dig deeper into reducer design patterns that can be used to simplify state management in your apps.

Improving Component Performance

In a React application, components are rendered…usually a lot.

Improving performance includes preventing unnecessary renders and reducing the time a render takes to propagate. React comes with tools to help us prevent unnecessary renders: memo, useMemo, and useCallback. We looked at useMemo and useCallback earlier in the chapter, but in this section, we'll go into more detail about how to use these Hooks to make your websites perform better.

The memo function is used to create pure components. As discussed in

Chapter 3, we know that, given the same parameters, a pure function will always return the same result. A pure component works the same way. In React, a pure component is a component that always renders the same output, given the same properties.

Let's create a component called Cat:

const Cat = ({ name }) => {

console.log(`rendering ${name}`);

return <p>{name}</p>;

};

Cat is a pure component. The output is always a paragraph that displays the name property. If the name provided as a property is the same, the output will be the same:

function App() {

const [cats, setCats] = useState(["Biscuit", "Jungle", "Outlaw"]); return (

<>

{cats.map((name, i) => (

<Cat key={i} name={name} />

))}

<button onClick={() => setCats([...cats, prompt("Name a cat")])}> Add a Cat

</button>

</>

);

}

This app uses the Cat component. After the initial render, the console reads:

rendering Biscuit

rendering Jungle

rendering Outlaw

When the「Add a Cat」button is clicked, the user is prompted to add a cat.

If we add a cat named「Ripple,」we see that all Cat components are

rerendered:

rendering Biscuit

rendering Jungle

rendering Outlaw

rendering Ripple

WARNING

This code works because prompt is blocking. This is just an example. Don't use prompt in a real app.

Every time we add a cat, every Cat component is rendered, but the Cat component is a pure component. Nothing changes about the output given the same prop, so there shouldn't be a render for each of these.

We don't want to rerender a pure component if the properties haven't changed. The memo function can be used to create a component that will only render when its properties change. Start by importing it from the React library and use it to wrap the current Cat component: import React, { useState, memo } from "react"; const Cat = ({ name }) => {

console.log(`rendering ${name}`);

return <p>{name}</p>;

};

const PureCat = memo(Cat);

Here, we've created a new component called PureCat. PureCat will only cause the Cat to render when the properties change. Then we can replace the Cat component with PureCat in the App component:

cats.map((name, i) => <PureCat key={i} name={name} />); Now, every time we add a new cat name, like「Pancake,」we see only one render in the console:

rendering Pancake

Because the names of the other cats have not changed, we don't render those Cat components. This is working well for a name property, but what if we introduce a function property to the Cat component?

const Cat = memo(({ name, meow = f => f }) => {

console.log(`rendering ${name}`);

return <p onClick={() => meow(name)}>{name}</p>;

});

Every time a cat is clicked on, we can use this property to log a meow to the console:

<PureCat key={i} name={name} meow={name => console.log(`${name} has meowed`)} />

When we add this change, PureCat no longer works as expected. It's always rendering every Cat component even though the name property remains the same. This is because of the added meow property.

Unfortunately, every time we define the meow property as a function, it's always new function. To React, the meow property has changed, and the component is rerendered.

The memo function will allow us to define more specific rules around when this component should rerender:

const RenderCatOnce = memo(Cat, () => true); const AlwaysRenderCat = memo(Cat, () => false); The second argument sent to the memo function is a predicate. A predicate is a function that only returns true or false. This function decides whether to rerender a cat or not. When it returns false, the Cat is rerendered. When this function returns true, the Cat will not be rerendered. No matter what, the Cat is always rendered at least once.

This is why, with RenderCatOnce, it will render once and then never again. Typically, this function is used to check actual values: const PureCat = memo(

Cat,

(prevProps, nextProps) => prevProps.name === nextProps.name

);

We can use the second argument to compare properties and decide if Cat should be rerendered. The predicate receives the previous properties and the next properties. These objects are used to compare the name property. If the name changes, the component will be rerendered. If the name is the same, it will be rerendered regardless of what React thinks about the meow property.

shouldComponentUpdate and PureComponent

The concepts we're discussing are not new to React. The memo function is a new solution to a common problem. In previous versions of React, there was a method called shouldComponentUpdate. If present in the component, it was used to let React know under which circumstances the component should update. shouldComponentUpdate described which props or state would need to change for the component to

rerender. Once shouldComponentUpdate was part of the React library, it was embraced as a useful feature by many. So useful that the React team decided to create an alternate way of creating a component as a class. A class component would look like this:

class Cat extends React.Component {

render() {

return (

{name} is a good cat!

)

}

}

A PureComponent would look like this:

class Cat extends React.PureComponent {

render() {

return (

{name} is a good cat!

)

}

}

PureComponent is the same as React.memo, but PureComponent is only for class components; React.memo is only for function components.

useCallback and useMemo can be used to memoize object and function properties. Let's use useCallback in the Cat component: const PureCat = memo(Cat);

function App() {

const meow = useCallback(name => console.log(`${name} has meowed`, []); return <PureCat name="Biscuit" meow={meow} />

}

In this case, we did not provide a property-checking predicate to memo(Cat). Instead, we used useCallback to ensure that the meow function had not changed. Using these functions can be helpful when dealing with too many rerenders in your component tree.

When to Refactor

The last Hooks we discussed, useMemo and useCallback, along with the memo function, are commonly overused. React is designed to be fast. It's designed to have components render a lot. The process of optimizing for performance began when you decided to use React in the first place. It's fast. Any further refactoring should be a last step.

There are trade-offs to refactoring. Using useCallback and useMemo everywhere because it seems like a good idea might actually make your app less performant. You're adding more lines of code and developer hours to your application. When you refactor for performance, it's important to have a goal. Perhaps you want to stop the screen from freezing or flickering. Maybe you know there are some costly functions that are slowing the speed of your app unreasonably.

The React Profiler can be used to measure the performance of each of your components. The profiler ships with the React Developer Tools that you've likely installed already (available for Chrome and Firefox).

Always make sure your app works and you're satisfied with the codebase before refactoring. Over-refactoring, or refactoring before your app works, can introduce weird bugs that are hard to spot, and it

might not be worth your time and focus to introduce these optimizations.

In the last two chapters, we've introduced many of the Hooks that ship with React. You've seen use cases for each hook, and you've created your own custom Hooks by composing other Hooks. Next, we'll build on these foundational skills by incorporating additional libraries and advanced patterns.