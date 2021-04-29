Management

Data is what makes our React components come to life. The user interface for recipes that we built in the last chapter is useless without the array of recipes. It's the recipes and the ingredients along with clear instructions that makes such an app worthwhile. Our user interfaces are tools that creators will use to generate content. In order to build the best tools possible for our content creators, we'll need to know how to effectively manipulate and change data.

In the last chapter, we constructed a component tree: a hierarchy of components that data was able to flow through as properties. Properties are half of the picture. State is the other half. The state of a React application is driven by data that has the ability to change. Introducing state to the recipe application could make it possible for chefs to create new recipes, modify existing recipes, and remove old ones.

State and properties have a relationship with each other. When we work with React applications, we gracefully compose components that are tied together based on this relationship. When the state of a component tree changes, so do the properties. The new data flows through the tree, causing specific leaves and branches to render to reflect the new content.

In this chapter, we're going to bring applications to life by introducing

state. We'll learn to create stateful components and how state can be sent down a component tree and user interactions back up the component tree. We'll learn techniques for collecting form data from users. And we'll take a look at the various ways in which we can separate concerns within our applications by introducing stateful context providers.

Building a Star Rating Component

We would all be eating terrible food and watching terrible movies without the five-star rating system. If we plan on letting users drive the content on our website, we'll need a way to know if that content is any good or not. That makes the StarRating component one of the most important React components you'll ever build (see Figure 6-1).

Figure 6-1. StarRating component

The StarRating component will allow users to rate content based on a specific number of stars. Content that's no good gets one star. Highly recommended content gets five stars. Users can set the rating for specific content by clicking on a specific star. First, we'll need a star, and we can get one from react-icons:

npm i react-icons

react-icons is an npm library that contains hundreds of SVG icons that are distributed as React components. By installing it, we just installed several popular icon libraries that contain hundreds of common SVG icons. You can browse all the icons in the library. We're going to use the star icon from the Font Awesome collection: import React from "react";

import { FaStar } from "react-icons/fa"; export default function StarRating() {

return [

<FaStar color="red" />,

<FaStar color="red" />,

<FaStar color="red" />,

<FaStar color="grey" />,

<FaStar color="grey" />

];

}

Here, we've created a StarRating component that renders five SVG

stars that we've imported from react-icons. The first three stars are filled in with red, and the last two are grey. We render the stars first because seeing them gives us a roadmap for what we'll have to build.

A selected star should be filled in with red, and a star that's not selected should be greyed out. Let's create a component that automatically files the stars based upon the selected property: const Star = ({ selected = false }) => (

<FaStar color={selected ? "red" : "grey"} />

);

The Star component renders an individual star and uses the selected

property to fill it with the appropriate color. If the selected property is not passed to this component, we'll assume that the star should not be selected and by default will be filled in with grey.

The 5-star rating system is pretty popular, but a 10-star rating system is far more detailed. We should allow developers to select the total number of stars they wish to use when they add this component to their app. This can be accomplished by adding a totalStars property to the StarRating component:

const createArray = length => [...Array(length)]; export default function StarRating({ totalStars = 5 }) {

return createArray(totalStars).map((n, i) => <Star key={i} />);

}

Here, we added the createArray function from Chapter 2. All we have to do is supply the length of the array that we want to create and we get a new array at that length. We use this function with the totalStars property to create an array of a specific length. Once we have an array, we can map over it and render Star components. By default, totalStars is equal to 5, which means this component will render 5 grey stars, as shown in Figure 6-2.

Figure 6-2. Five stars are displayed

The useState Hook

It's time to make the StarRating component clickable, which will allow our users to change the rating. Since the rating is a value that will change, we'll store and change that value using React state. We incorporate state into a function component using a React feature called Hooks. Hooks contain reusable code logic that is separate from the component tree. They allow us to hook up functionality to our components. React ships with several built-in hooks we can use out of the box. In this case, we want to add state to our React component, so the first hook we'll work with is React's useState hook. This hook is already available in the react package; we simply need to import it: import React, { useState } from "react"; import { FaStar } from "react-icons/fa"; The stars the user has selected represents the rating. We'll create a state variable called selectedStars, which will hold the user's rating.

We'll create this variable by adding the useState hook directly to the StarRating component:

export default function StarRating({ totalStars = 5 }) {

const [selectedStars] = useState(3);

return (

<>

{createArray(totalStars).map((n, i) => (

<Star key={i} selected={selectedStars > i} />

))}

<p>

{selectedStars} of {totalStars} stars

</p>

</>

);

}

We just hooked this component up with state. The useState hook is a

function that we can invoke to return an array. The first value of that array is the state variable we want to use. In this case, that variable is selectedStars, or the number of stars the StarRating will color red.

useState returns an array. We can take advantage of array destructuring, which allows us to name our state variable whatever we like. The value we send to the useState function is the default value for the state variable. In this case, selectedStars will initially be set to 3, as shown in Figure 6-3.

Figure 6-3. Three of five stars are selected

In order to collect a different rating from the user, we'll need to allow them to click on any of our stars. This means we'll need to make the stars clickable by adding an onClick handler to the FaStar component:

const Star = ({ selected = false, onSelect = f => f }) => (

<FaStar color={selected ? "red" : "grey"} onClick={onSelect} />

);

Here, we modified the star to contain an onSelect property. Check it out: this property is a function. When a user clicks on the FaStar component, we'll invoke this function, which can notify its parent that a star has been clicked. The default value for this function is f => f.

This is simply a fake function that does nothing; it just returns whatever argument was sent to it. However, if we do not set a default function and the onSelect property is not defined, an error will occur when we click the FaStar component because the value for onSelect must be a function. Even though f => f does nothing, it is a function, which means it can be invoked without causing errors. If an onSelect property is not defined, no problem. React will simply invoke the fake function and nothing will happen.

Now that our Star component is clickable, we'll use it to change the state of the StarRating:

export default function StarRating({ totalStars = 5 }) {

const [selectedStars, setSelectedStars] = useState(0); return (

<>

{createArray(totalStars).map((n, i) => (

<Star

key={i}

selected={selectedStars > i}

onSelect={() => setSelectedStars(i + 1)}

/>

))}

<p>

{selectedStars} of {totalStars} stars

</p>

</>

);

}

In order to change the state of the StarRating component, we'll need a function that can modify the value of selectedStars. The second item in the array that's returned by the useState hook is a function that can be used to change the state value. Again, by destructuring this

array, we can name that function whatever we like. In this case, we're calling it setSelectedStars, because that's what it does: it sets the value of selectedStars.

The most important thing to remember about Hooks is that they can cause the component they're hooked into to rerender. Every time we invoke the setSelectedStars function to change the value of selectedStars, the StarRating function component will be

reinvoked by the hook, and it will render again, this time with a new value for selectedStars. This is why Hooks are such a killer feature.

When data within the hook changes, they have the power to rerender the component they're hooked into with new data.

The StarRating component will be rerendered every time a user clicks a Star. When the user clicks the Star, the onSelect property of that star is invoked. When the onSelect property is invoked, we'll invoke the setSelectedStars function and send it the number of the star that was just selected. We can use the i variable from the map function to help us calculate that number. When the map function renders the first Star, the value for i is 0. This means that we need to add 1 to this value to get the correct number of stars. When setSelectedStars is invoked, the StarRating component is invoked with a the value for selectedStars, as shown in Figure 6-4.

Figure 6-4. Hooks in React developer tools

The React developer tools will show you which Hooks are

incorporated with specific components. When we render the StarRating component in the browser, we can view debugging information about that component by selecting it in the developer tools.

In the column on the right, we can see that the StarRating component incorporates a state Hook that has a value of 2. As we interact with the app, we can watch the state value change and the component tree rerender with the corresponding number of stars selected.

REACT STATE THE「OLD WAY」

In previous versions of React, before v16.8.0, the only way to add state to a component was to use a class component. This required not only a lot of syntax, but it also made it more difficult to reuse functionality across components. Hooks were designed to solve problems presented with class components by providing a solution to incorporate functionality into function components.

The following code is a class component. This was the original StarRating component that was printed in the first edition of this book:

import React, { Component } from "react";

export default class StarRating extends Component {

constructor(props) {

super(props);

this.state = {

starsSelected: 0

};

this.change = this.change.bind(this);

}

change(starsSelected) {

this.setState({ starsSelected });

}

render() {

const { totalStars } = this.props;

const { starsSelected } = this.state;

return (

<div>

{[...Array(totalStars)].map((n, i) => (

<Star

key={i}

selected={i < starsSelected}

onClick={() => this.change(i + 1)}

/>

))}

<p>

{starsSelected} of {totalStars} stars

</p>

</div>

);

}

}

This class component does the same thing as our function component with noticeably more code.

Additionally, it introduces more confusion thorough the use of the this keyword and function binding.

As of today, this code still works. We're no longer covering class components in this book because they're no longer needed. Function components and Hooks are the future of React, and we're not looking back. There could come a day where class components are officially deprecated, and this code will no longer be supported.

Refactoring for Advanced Reusability

Right now, the Star component is ready for production. You can use it across several applications when you need to obtain a rating from a user. However, if we were to ship this component to npm so that anyone in the world could use it to obtain ratings from users, we may want to consider handling a couple more use cases.

First, let's consider the style property. This property allows you to add CSS styles to elements. It is highly possible that a future developer, even yourself, could come across the need to modify the style of your entire container. They may attempt to do something like this:

export default function App() {

return <StarRating style={{ backgroundColor: "lightblue" }} />;

}

All React elements have style properties. A lot of components also

have style properties. So attempting to modify the style for the entire component seems sensible.

All we need to do is collect those styles and pass them down to the StarRating container. Currently, the StarRating does not have a single container because we are using a React fragment. To make this work, we'll have to upgrade from a fragment to a div element and pass the styles to that div:

export default function StarRating({ style = {}, totalStars = 5 }) {

const [selectedStars, setSelectedStars] = useState(0); return (

<div style={{ padding: "5px", ...style }}>

{createArray(totalStars).map((n, i) => (

<Star

key={i}

selected={selectedStars > i}

onSelect={() => setSelectedStars(i + 1)}

/>

))}

<p>

{selectedStars} of {totalStars} stars

</p>

</div>

);

}

In the code above, we replaced the fragment with a div element and then applied styles to that div element. By default we assign that div a padding of 5px, and then we use the spread operator to apply the rest of the properties from the style object to the div style.

Additionally, we may find developers who attempt to implement other common properties properties to the entire star rating:

export default function App() {

return (

<StarRating

style={{ backgroundColor: "lightblue" }}

onDoubleClick={e => alert("double click")}

/>

);

}

In this sample, the user is trying to add a double-click method to the entire StarRating component. If we feel it is necessary, we can also pass this method along with any other properties down to our containing div:

export default function StarRating({ style = {}, totalStars = 5, ...props

}) {

const [selectedStars, setSelectedStars] = useState(0); return (

<div style={{ padding: 5, ...style }} {...props}>

...

</div>

);

}

The first step is to collect any and all properties that the user may be attempting to add to the StarRating. We gather these properties using the spread operator: ...props. Next, we'll pass all of these remaining properties down to the div element: {...props}.

By doing this, we make two assumptions. First, we are assuming that users will add only those properties that are supported by the div element. Second, we are assuming that our user can't add malicious properties to the component.

This is not a blanket rule to apply to all of your components. In fact, it's only a good idea to add this level of support in certain situations.

The real point is that it's important to think about how the consumers of your component may try to use it in the future.

State in Component Trees

It's not a great idea to use state in every single component. Having state data distributed throughout too many of your components will make it harder to track down bugs and make changes within your application. This occurs because it's hard to keep track of where the state values live within your component tree. It's easier to understand your application's state, or state for a specific feature, if you manage it from one location. There are several approaches to this methodology, and the first one we'll analyze is storing state at the root of the component tree and passing it down to child components via props.

Let's build a small application that can be used to save a list of colors.

We'll call the app the「Color Organizer」, and it will allow users to associate a list of colors with a custom title and rating. To get started, a sample dataset may look like the following:

[

{

"id" : "0175d1f0-a8c6-41bf-8d02-df5734d829a4",

"title" : "ocean at dusk",

"color" : "#00c4e2",

"rating" : 5

},

{

"id" : "83c7ba2f-7392-4d7d-9e23-35adbe186046",

"title" : "lawn",

"color" : "#26ac56",

"rating" : 3

},

{

"id" : "a11e3995-b0bd-4d58-8c48-5e49ae7f7f23",

"title" : "bright red",

"color" : "#ff0000",

"rating" : 0

}

]

The color-data.json file contains an array of three colors. Each color has an id, title, color, and rating. First, we'll create a UI consisting of React components that will be used to display this data in a browser. Then we'll allow the users to add new colors as well as rate and remove colors from the list.

Sending State Down a Component Tree

In this iteration, we'll store state in the root of the Color Organizer, the App component, and pass the colors down to child components to handle the rendering. The App component will be the only component within our application that holds state. We'll add the list of colors to the App with the useState hook:

import React, { useState } from "react"; import colorData from "./color-data.json"; import ColorList from "./ColorList.js";

export default function App() {

const [colors] = useState(colorData);

return <ColorList colors={colors} />;

}

The App component sits at the root of our tree. Adding useState to this component hooks it up with state management for colors. In this example, the colorData is the array of sample colors from above. The App component uses the colorData as the initial state for colors.

From there, the colors are passed down to a component called the ColorList:

import React from "react";

import Color from "./Color";

export default function ColorList({ colors = [] }) {

if(!colors.length) return <div>No Colors Listed.</div>; return (

<div>

{

colors.map(color => <Color key={color.id} {...color} />)

}

</div>

);

}

The ColorList receives the colors from the App component as props.

If the list is empty, this component will display a message to our users.

When we have a color array, we can map over it and pass the details about each color farther down the tree to the Color component: export default function Color({ title, color, rating }) {

return (

<section>

<h1>{title}</h1>

<div style={{ height: 50, backgroundColor: color }} />

<StarRating selectedStars={rating} />

</section>

);

}

The Color component expects three properties: title, color, and rating. These values are found in each color object and were passed to this component using the spread operator <Color {...color} />.

This takes each field from the color object and passes it to the Color component as a property with the same name as the object key. The Color component displays these values. The title is rendered inside of an h1 element. The color value is displayed as the

backgroundColor for a div element. The rating is passed farther down the tree to the StarRating component, which will display the rating visually as selected stars:

export default function StarRating({ totalStars = 5, selectedStars = 0 })

{

return (

<>

{createArray(totalStars).map((n, i) => (

<Star

key={i}

selected={selectedStars > i}

/>

))}

<p>

{selectedStars} of {totalStars} stars

</p>

</>

);

}

This StarRating component has been modified. We've turned it into a pure component. A pure component is a function component that does not contain state and will render the same user interface given the same props. We made this component a pure component because the state for color ratings are stored in the colors array at the root of the component tree. Remember that the goal of this iteration is to store

state in a single location and not have it distributed through many different components within the tree.

NOTE

It is possible for the StarRating component to hold its own state and receive state from a parent component via props. This is typically necessary when distributing components for wider use by the community. We demonstrate this technique in the next chapter when we cover the useEffect hook.

At this point, we've finished passing state down the component tree from the App component all the way to each Star component that's filled red to visually represent the rating for each color. If we render the app based on the color-data.json file that was listed previously, we should see our colors in the browser, as shown in Figure 6-5.

Figure 6-5. Color Organizer rendered in the browser Sending Interactions Back up a Component Tree

So far, we've rendered a representation of the colors array as UI by composing React components and passing data down the tree from parent component to child component via props. What happens if we want to remove a color from the list or change the rating of a color in our list? The colors are stored in state at the root of our tree. We'll need to collect interactions from child components and send them back up the tree to the root component where we can change the state.

For instance, let's say we wanted to add a Remove button next to each color's title that would allow users to remove colors from state. We would add that button to the Color component:

import { FaTrash } from "react-icons/fa"; export default function Color({ id, title, color, rating, onRemove = f => f }) {

return (

<section>

<h1>{title}</h1>

<button onClick={() => onRemove(id)}>

<FaTrash />

</button>

<div style={{ height: 50, backgroundColor: color }} />

<StarRating selectedStars={rating} />

</section>

);

}

Here, we've modified the color by adding a button that will allow users to remove colors. First, we imported a trash can icon from react-

icons. Next, we wrapped the FaTrash icon in a button. Adding an onClick handler to this button allows us to invoke the onRemove function property, which has been added to our list of properties along with the id. When a user clicks the Remove button, we'll invoke removeColor and pass it the id of the color that we want to remove.

That is why the id value has also been gathered from the Color component's properties.

This solution is great because we keep the Color component pure. It doesn't have state and can easily be reused in a different part of the app or another application altogether. The Color component is not concerned with what happens when a user clicks the Remove button.

All it cares about is notifying the parent that this event has occurred and passing the information about which color the user wishes to remove. It's now the parent's responsibility to handle this event: export default function ColorList({ colors = [], onRemoveColor = f => f

}) {

if (!colors.length) return <div>No Colors Listed. (Add a Color)</div>; return (

colors.map(color => (

<Color key={color.id} {...color} onRemove={onRemoveColor} />

)

}

</div>

);

}

The Color component's parent is the ColorList. This component also doesn't have access to state. Instead of removing the color, it simply passes the event up to its parent. It accomplishes this by adding an

onRemoveColor function property. If a Color component invokes the onRemove property, the ColorList will in turn invoke its

onRemoveColor property and send the responsibility for removing the color up to its parent. The color's id is still being passed to the onRemoveColor function.

The parent of the ColorList is the App. This component is the component that has been hooked up with state. This is where we can capture the color id and remove the color in state:

export default function App() {

const [colors, setColors] = useState(colorData);

return (

<ColorList

colors={colors}

onRemoveColor={id => {

const newColors = colors.filter(color => color.id !== id); setColors(newColors);

}}

/>

);

}

First, we add a variable for setColors. Remember that the second argument in the array returned by useState is a function we can use to modify the state. When the ColorList raises an onRemoveColor event, we capture the id of the color to remove from the arguments and use it to filter the list of colors to exclude the color the user wants to remove.

Next, we change the state. We use the setColors function to change change the array of colors to the newly filtered array.

Changing the state of the colors array causes the App component to be

rerendered with the new list of colors. Those new colors are passed to the ColorList component, which is also rerendered. It will render Color components for the remaining colors and our UI will reflect the changes we've made by rendering one less color.

If we want to rate the colors that are stored in the App components state, we'll have to repeat the process with an onRate event. First, we'll collect the new rating from the individual star that was clicked and pass that value to the parent of the StarRating:

export default function StarRating({

totalStars = 5,

selectedStars = 0,

onRate = f => f

}) {

return (

<>

{createArray(totalStars).map((n, i) => (

<Star

key={i}

selected={selectedStars > i}

onSelect={() => onRate(i + 1)}

/>

))}

</>

);

}

Then, we'll grab the rating from the onRate handler we added to the StarRating component. We'll then pass the new rating along with the id of the color to be rated up to the Color component's parent via another onRate function property:

export default function Color({

id,

title,

color,

rating,

onRemove = f => f,

onRate = f => f

}) {

return (

<section>

<h1>{title}</h1>

<button onClick={() => onRemove(id)}>

<FaTrash />

</button>

<div style={{ height: 50, backgroundColor: color }} />

<StarRating

selectedStars={rating}

onRate={rating => onRate(id, rating)}

/>

</section>

);

}

In the ColorList component, we'll have to capture the onRate event from individual color components and pass them up to its parent via the onRateColor function property:

export default function ColorList({

colors = [],

onRemoveColor = f => f,

onRateColor = f => f

}) {

if (!colors.length) return <div>No Colors Listed. (Add a Color)</div>; return (

<div className="color-list">

{

colors.map(color => (

<Color

key={color.id}

{...color}

onRemove={onRemoveColor}

onRate={onRateColor}

/>

)

}

</div>

);

}

Finally, after passing the event up through all of these components, we'll arrive at the App, where state is stored and the new rating can be saved:

export default function App() {

const [colors, setColors] = useState(colorData);

return (

<ColorList

colors={colors}

onRateColor={(id, rating) => {

const newColors = colors.map(color =>

color.id === id ? { ...color, rating } : color

);

setColors(newColors);

}}

onRemoveColor={id => {

const newColors = colors.filter(color => color.id !== id); setColors(newColors);

}}

/>

);

}

The App component will change color ratings when the ColorList invokes the onRateColor property with the id of the color to rate and the new rating. We'll use those values to construct an array of new colors by mapping over the existing colors and changing the rating for the color that matches the id property. Once we send the newColors to

the setColors function, the state value for colors will change and the App component will be invoked with a new value for the colors array.

Once the state of our colors array changes, the UI tree is rendered with the new data. The new rating is reflected back to the user via red stars. Just as we passed data down a component tree via props, interactions can be passed back up the tree along with data via function properties.

Building Forms

For a lot of us, being a web developer means collecting large amounts of information from users with forms. If this sounds like your job, then you'll be building a lot of form components with React. All of the HTML form elements that are available to the DOM are also available as React elements, which means that you may already know how to render a form with JSX:

<form>

<input type="text" placeholder="color title..." required />

<input type="color" required />

<button> ADD</button>

</form>

This form element has three child elements: two input elements and a button. The first input element is a text input that will be used to collect the title value for new colors. The second input element is an HTML color input that will allow users to pick a color from a color wheel. We'll be using basic HTML form validation, so we've marked both inputs as required. The ADD button will be used to add a new color.

Using Refs

When it's time to build a form component in React, there are several patterns available to you. One of these patterns involves accessing the DOM node directly using a React feature called refs. In React, a ref is an object that stores values for the lifetime of a component. There are several use cases that involve using refs. In this section, we'll look at how we can access a DOM node directly with a ref.

React provides us with a useRef hook that we can use to create a ref.

We'll use this hook when building the AddColorForm component: import React, { useRef } from "react";

export default function AddColorForm({ onNewColor = f => f }) {

const txtTitle = useRef();

const hexColor = useRef();

const submit = e => { ... }

return (...)

}

First, when creating this component, we'll also create two refs using the useRef hook. The txtTitle ref will be used to reference the text input we've added to the form to collect the color title. The hexColor ref will be used to access hexadecimal color values from the HTML

color input. We can set the values for these refs directly in JSX using the ref property:

return (

<form onSubmit={submit}>

<input ref={txtTitle} type="text" placeholder="color title..."

required />

<input ref={hexColor} type="color" required />

<button>ADD</button>

</form>

);

}

Here, we set the value for the txtTitle and hexColor refs by adding the ref attribute to these input elements in JSX. This creates a current field on our ref object that references the DOM element directly. This provides us access to the DOM element, which means we can capture its value. When the user submits this form by clicking the ADD button, we'll invoke the submit function:

const submit = e => {

e.preventDefault();

const title = txtTitle.current.value;

const color = hexColor.current.value;

onNewColor(title, color);

txtTitle.current.value = "";

hexColor.current.value = "";

};

When we submit HTML forms, by default, they send a POST request to the current URL with the values of the form elements stored in the body. We don't want to do that. This is why the first line of code in the submit function is e.preventDefault(), which prevents the browser from trying to submit the form with a POST request.

Next, we capture the current values for each of our form elements using their refs. These values are then passed up to this component's parent via the onNewColor function property. Both the title and the hexadecimal value for the new color are passed as function arguments.

Finally, we reset the value attribute for both inputs to clear the data

and prepare the form to collect another color.

Did you notice the subtle paradigm shift that has occurred by using refs? We're mutating the value attribute of DOM nodes directly by setting them equal to "" empty strings. This is imperative code. The AddColorForm is now what we call an uncontrolled component because it uses the DOM to save the form values. Sometimes using uncontrolled component can get you out of problems. For instance, you may want to share access to a form and its values with code outside of React. However, a controlled component is a better approach.

Controlled Components

In a controlled component, the from values are managed by React and not the DOM. They do not require us to use refs. They do not require us to write imperative code. Adding features like robust form validation is much easier when working with a controlled component.

Let's modify the AddColorForm by giving it control over the form's state:

import React, { useState } from "react"; export default function AddColorForm({ onNewColor = f => f }) {

const [title, setTitle] = useState("");

const [color, setColor] = useState("#000000"); const submit = e => { ... };

return ( ... );

}

First, instead of using refs, we're going to save the values for the title

and color using React state. We'll create variables for title and color. Additionally, we'll define the functions that can be used to change state: setTitle and setColor.

Now that the component controls the values for title and color, we can display them inside of the form input elements by setting the value attribute. Once we set the value attribute of an input element, we'll no longer be able to change with the form. The only way to change the value at this point would be to change the state variable every time the user types a new character in the input element. That's exactly what we'll do:

<form onSubmit={submit}>

<input

value={title}

onChange={event => setTitle(event.target.value)}

type="text"

placeholder="color title..."

required

/>

<input

value={color}

onChange={event => setColor(event.target.value)}

type="color"

required

/>

<button>ADD</button>

</form>

}

This controlled component now sets the value of both input elements using the title and color from state. Whenever these elements raise an onChange event, we can access the new value using the event argument. The event.target is a reference to the DOM element, so we can obtain the current value of that element with

event.target.value. When the title changes, we'll invoke setTitle to change the title value in state. Changing that value will cause this component to rerender, and we can now display the new value for title inside the input element. Changing the color works exactly the same way.

When it's time to submit the form, we can simply pass the state values for title and color to the onNewColor function property as arguments when we invoke it. The setTitle and setColor functions can be used to reset the values after the new color has been passed to the parent component:

const submit = e => {

e.preventDefault();

onNewColor(title, color);

setTitle("");

setColor("");

};

It's called a controlled component because React controls the state of the form. It's worth pointing out that controlled form components are rerendered, a lot. Think about it: every new character typed in the title field causes the AddColorForm to rerender. Using the color wheel in the color picker causes this component to rerender way more than the title field because the color value repeatedly changes as the user drags the mouse around the color wheel. This is OK—React is designed to handle this type of workload. Hopefully, knowing that controlled components are rerendered frequently will prevent you from adding some long and expensive process to this component. At the very least, this knowledge will come in handy when you're trying to

optimize your React components.

Creating Custom Hooks

When you have a large form with a lot of input elements, you may be tempted to copy and paste these two lines of code:

value={title}

onChange={event => setTitle(event.target.value)}

It might seem like you're working faster by simply copying and pasting these properties into every form element while tweaking the variable names along the way. However, whenever you copy and paste code, you should hear a tiny little alarm sound in your head. Copying and pasting code suggests that there's something redundant enough to abstract away in a function.

We can package the details necessary to create controlled form components into a custom hook. We could create our own useInput hook where we can abstract away the redundancy involved with creating controlled form inputs:

import { useState } from "react";

export const useInput = initialValue => {

const [value, setValue] = useState(initialValue);

return [

{ value, onChange: e => setValue(e.target.value) },

() => setValue(initialValue)

];

};

This is a custom hook. It doesn't take a lot of code. Inside of this hook,

we're still using the useState hook to create a state value. Next, we return an array. The first value of the array is the object that contains the same properties we were tempted to copy and paste: the value from state along with an onChange function property that changes that value in state. The second value in the array is a function that can be reused to reset the value back to its initial value. We can use our hook inside of the AddColorForm:

import React from "react";

import { useInput } from "./hooks";

export default function AddColorForm({ onNewColor = f => f }) {

const [titleProps, resetTitle] = useInput(""); const [colorProps, resetColor] = useInput("#000000"); const submit = event => { ... }

return ( ... )

}

The useState hook is encapsulated within our useInput hook. We can obtain the properties for both the title and the color by destructuring them from the first value of the returned array. The second value of this array contains a function we can use to reset the value property back to its initial value, an empty string. The titleProps and colorProps are ready to be spread into their corresponding input elements:

return (

<form onSubmit={submit}>

<input

{...titleProps}

type="text"

placeholder="color title..."

required

/>

<input {...colorProps} type="color" required />

<button>ADD</button>

</form>

);

}

Spreading these properties from our custom hook is much more fun than pasting them. Now both the title and the color inputs are receiving properties for their value and onChange events. We've used our hook to create controlled form inputs without worrying about the underlying implementation details. The only other change we need to make is when this form is submitted:

const submit = event => {

event.preventDefault();

onNewColor(titleProps.value, colorProps.value);

resetTitle();

resetColor();

};

Within the submit function, we need to be sure to grab the value for both the title and the color from their properties. Finally, we can use the custom reset functions that were returned from the useInput hook.

Hooks are designed to be used inside of React components. We can compose hooks within other hooks because eventually the customized hook will be used inside of a component. Changing the state within this hook still causes the AddColorForm to rerender with new values for titleProps or colorProps.

Adding Colors to State

Both the controlled form component and the uncontrolled from component pass the values for title and color to the parent component via the onNewColor function. The parent doesn't care whether we used a controlled component or an uncontrolled component; it only wants the values for the new color.

Let's add the AddColorForm, whichever one you choose, to the the App component. When the onNewColor property is invoked, we'll save the new color in state:

import React, { useState } from "react"; import colorData from "./color-data.json"; import ColorList from "./ColorList.js";

import AddColorForm from "./AddColorForm"; import { v4 } from "uuid";

export default function App() {

const [colors, setColors] = useState(colorData);

return (

<>

<AddColorForm

onNewColor={(title, color) => {

const newColors = [

...colors,

{

id: v4(),

rating: 0,

title,

color

}

];

setColors(newColors);

}}

/>

<ColorList .../>

</>

);

}

When a new color is added, the onNewColor property is invoked. The title and hexadecimal value for the new color are passed to this function as arguments. We use these arguments to create a new array of colors. First, we spread the current colors from state into the new array. Then we add an entirely new color object using the title and color values. Additionally, we set the rating of the new color to 0

because it has not yet been rated. We also use the v4 function found in the uuid package to generate a new unique id for the color. Once we have an array of colors that contains our new color, we save it to state by invoking setColors. This causes the App component to rerender with a new array of colors. That new array will be used to update the UI. We'll see the new color at bottom of the list.

With this change, we've completed the first iteration of the Color Organizer. Users can now add new colors to the list, remove colors from the list, and rate any existing color on that list.

React Context

Storing state in one location at the root of our tree was an important pattern that helped us all be more successful with early versions of React. Learning to pass state both down and up a component tree via properties is a necessary right of passage for any React developer—it's something we should all know how to do. However, as React evolved and our component trees got larger, following this principle slowly became more unrealistic. It's hard for many developers to maintain state in a single location at the root of a component tree for a complex

application. Passing state down and up the tree through dozens of components is tedious and bug ridden.

The UI elements that most of us work on are complex. The root of the tree is often very far from the leaves. This puts data the application depends on many layers away from the components that use the data.

Every component must receive props that they only pass to their children. This will bloat our code and make our UI harder to scale.

Passing state data through every component as props until it reaches the component that needs to use it is like taking the train from San Francisco to DC. On the train, you'll pass through every state, but you won't get off until you reach your destination (see Figure 6-6).

Figure 6-6. Train from San Francisco to DC

It's obviously more efficient to fly from San Francisco to DC. This way, you don't have to pass through every state—you simply fly over them (Figure 6-7).

Figure 6-7. Flight from San Francisco to DC

In React, context is like jet-setting for your data. You can place data in React context by creating a context provider. A context provider is a React component you can wrap around your entire component tree or

specific sections of your component tree. The context provider is the departing airport where your data boards the plane. It's also the airline hub. All flights depart from that airport to different destinations. Each destination is a context consumer. The context consumer is the React component that retrieves the data from context. This is the destination airport where your data lands, deplanes, and goes to work.

Using context still allows to us store state data in a single location, but it doesn't require us to pass that data through a bunch of components that don't need it.

Placing Colors in Context

In order to use context in React, we must first place some data in a context provider and add that provider to our component tree. React comes with a function called createContext that we can use to create a new context object. This object contains two components: a context Provider and a Consumer.

Let's place the default colors found in the color-data.json file into context. We'll add context to the index.js file, the entry point of our application:

import React, { createContext } from "react";

import colors from "./color-data";

import { render } from "react-dom";

import App from "./App";

export const ColorContext = createContext();

render(

<ColorContext.Provider value={{ colors }}>

<App />

</ColorContext.Provider>,

document.getElementById("root")

);

Using createContext, we created a new instance of React context that we named ColorContext. The color context contains two components: ColorContext.Provider and ColorContext.Consumer. We need to use the provider to place the colors in state. We add data to context by setting the value property of the Provider. In this scenario, we added an object containing the colors to context. Since we wrapped the entire App component with the provider, the array of colors will made available to any context consumers found in our entire component tree.

It's important to notice that we've also exported the ColorContext from this location. This is necessary because we will need to access the ColorContext.Consumer when we want to obtain the colors from context.

NOTE

A context Provider doesn't always have to wrap an entire application. It's not only OK to wrap specific sections components with a context Provider, it can make your application more efficient. The Provider will only provide context values to its children.

It's OK to use multiple context providers. In fact, you may be using context providers in your React app already without even knowing it. Many npm packages designed to work with React use context behind the scenes.

Now that we're providing the colors value in context, the App component no longer needs to hold state and pass it down to its children as props. We've made the App component a「flyover」

component. The Provider is the App component's parent, and it's

providing the colors in context. The ColorList is the App component's child, and it can obtain the colors directly on its own. So the app doesn't need to touch the colors at all, which is great because the App component itself has nothing to do with colors. That responsibility has been delegated farther down the tree.

We can remove a lot of lines of code from the App component. It only needs to render the AddColorForm and the ColorList. It no longer has to worry about the data:

import React from "react";

import ColorList from "./ColorList.js";

import AddColorForm from "./AddColorForm"; export default function App() {

return (

<>

<AddColorForm />

<ColorList />

</>

);

}

Retrieving Colors with useContext

The addition of Hooks makes working with context a joy. The useContext hook is used to obtain values from context, and it obtains those values we need from the context Consumer. The ColorList component no longer needs to obtain the array of colors from its properties. It can access them directly via the useContext hook: import React, { useContext } from "react";

import { ColorContext } from "./";

import Color from "./Color";

export default function ColorList() {

const { colors } = useContext(ColorContext);

if (!colors.length) return <div>No Colors Listed. (Add a Color)</div>; return (

<div className="color-list">

{

colors.map(color => <Color key={color.id} {...color} />)

}

</div>

);

}

Here, we've modified the ColorList component and removed the colors=[] property because the colors are being retrieved from context. The useContext hook requires the context instance to obtain values from it. The ColorContext instance is being imported from the index.js file where we create the context and add the provider to our component tree. The ColorList can now construct a user interface based on the data that has been provided in context.

USING CONTEXT CONSUMER

The Consumer is accessed within the useContext hook, which means that we no longer have to work directly with the consumer component. Before Hooks, we would have to obtain the colors from context using a pattern called render props within the context consumer. Render props are passed as arguments to a child function. The following example is how you would use the consumer to obtain the colors from context:

export default function ColorList() {

return (

<ColorContext.Consumer>

{context => {

if (!context.colors.length)

return <div>No Colors Listed. (Add a Color)</div>; return (

<div className="color-list">

{

context.colors.map(color =>

<Color key={color.id} {...color} />)

}

</div>

)

}}

</ColorContext.Consumer>

)

}

Stateful Context Providers

The context provider can place an object into context, but it can't mutate the values in context on its own. It needs some help from a parent component. The trick is to create a stateful component that renders a context provider. When the state of the stateful component changes, it will rerender the context provider with new context data.

Any of the context providers' children will also be rerendered with the new context data.

The stateful component that renders the context provider is our custom provider. That is: that's the component that will be used when it's time to wrap our App with the provider. In a brand-new file, let's create a ColorProvider:

import React, { createContext, useState } from "react"; import colorData from "./color-data.json";

const ColorContext = createContext();

export default function ColorProvider ({ children }) {

const [colors, setColors] = useState(colorData);

return (

<ColorContext.Provider value={{ colors, setColors }}>

{children}

</ColorContext.Provider>

);

};

The ColorProvider is a component that renders the

ColorContext.Provider. Within this component, we've created a state variable for colors using the useState hook. The initial data for colors is still being populated from color-data.json. Next, the ColorProvider adds the colors from state to context using the value property of the ColorContext.Provider. Any children rendered within the ColorProvider will be wrapped by the

ColorContext.Provider and will have access to the colors array from context.

You may have noticed that the setColors function is also being added to context. This gives context consumers the ability to change the value for colors. Whenever setColors is invoked, the colors array will change. This will cause the ColorProvider to rerender, and our UI will update itself to display the new colors array.

Adding setColors to context may not be the best idea. It invites other developers and you to make mistakes later on down the road when using it. There are only three options when it comes to changing the value of the colors array: users can add colors, remove colors, or rate colors. It's a better idea to add functions for each of these operations to context. This way, you don't expose the setColors function to consumers; you only expose functions for the changes they're allowed to make:

export default function ColorProvider ({ children }) {

const [colors, setColors] = useState(colorData);

const addColor = (title, color) =>

setColors([

...colors,

{

id: v4(),

rating: 0,

title,

color

}

]);

const rateColor = (id, rating) =>

setColors(

colors.map(color => (color.id === id ? { ...color, rating } : color))

);

const removeColor = id => setColors(colors.filter(color => color.id !==

id));

return (

<ColorContext.Provider value={{ colors, addColor, removeColor, rateColor }}>

{children}

</ColorContext.Provider>

);

};

That looks better. We added functions to context for all of the operations that can be made on the colors array. Now, any component within our tree can consume these operations and make changes to colors using simple functions that we can document.

Custom Hooks with Context

There's one more killer change we can make. The introduction of Hooks has made it so that we don't have to expose context to consumer components at all. Let's face it: context can be confusing for team members who aren't reading this book. We can make everything much easier for them by wrapping context in a custom hook. Instead of exposing the ColorContext instance, we can create a hook called useColors that returns the colors from context:

import React, { createContext, useState, useContext } from "react"; import colorData from "./color-data.json"; import { v4 } from "uuid";

const ColorContext = createContext();

export const useColors = () => useContext(ColorContext); This one simple change has a huge impact on architecture. We've wrapped all of the functionality necessary to render and work with stateful colors in a single JavaScript module. Context is contained to this module yet exposed through a hook. This works because we return context using the useContext hook, which has access to the ColorContext locally in this file. It's now appropriate to rename this module color-hooks.js and distribute this functionality for wider use by the community.

Consuming colors using the ColorProvider and the useColors hook is a joyous event. This is why we program. Let's take this hook out for a spin in the current Color Organizer app. First, we need to wrap our App component with the custom ColorProvider. We can do this in the index.js file:

import React from "react";

import { ColorProvider } from "./color-hooks.js"; import { render } from "react-dom";

import App from "./App";

render(

<ColorProvider>

<App />

</ColorProvider>,

document.getElementById("root")

);

Now, any component that's a child of the App can obtain the colors from the useColors hook. The ColorList component needs to access the colors array to render the colors on the screen:

import React from "react";

import Color from "./Color";

import { useColors } from "./color-hooks"; export default function ColorList() {

const { colors } = useColors();

return ( ... );

}

We've removed any references to context from this component.

Everything it needs is now being provided from our hook. The Color component could use our hook to obtain the functions for rating and removing colors directly:

import React from "react";

import StarRating from "./StarRating";

import { useColors } from "./color-hooks"; export default function Color({ id, title, color, rating }) {

const { rateColor, removeColor } = useColors();

return (

<section>

<h1>{title}</h1>

<button onClick={() => removeColor(id)}>X</button>

<div style={{ height: 50, backgroundColor: color }} />

<StarRating

selectedStars={rating}

onRate={rating => rateColor(id, rating)}

/>

</section>

);

}

Now, the Color component no longer needs to pass events to the parent via function props. It has access to the rateColor and removeColor functions in context. They're easily obtained through the useColors hook. This is a lot of fun, but we're not finished yet. The AddColorForm can also benefit from the useColors hook:

import React from "react";

import { useInput } from "./hooks";

import { useColors } from "./color-hooks"; export default function AddColorForm() {

const [titleProps, resetTitle] = useInput(""); const [colorProps, resetColor] = useInput("#000000"); const { addColor } = useColors();

const submit = e => {

e.preventDefault();

addColor(titleProps.value, colorProps.value);

resetTitle();

resetColor();

};

return ( ... );

}

The AddColorForm component can add colors directly with the addColor function. When colors are added, rated, or removed, the state of the colors value in context will change. When this change happens, the children of the ColorProvider are rerendered with new context data. All of this is happening through a simple hook.

Hooks provide software developers with the stimulation they need to stay motivated and enjoy frontend programming. This is primarily because they're an awesome tool for separating concerns. Now, React

components only need to concern themselves with rendering other React components and keeping the user interface up to date. React Hooks can concern themselves with the logic required to make the app work. Both the UI and Hooks can be developed separately, tested separately, and even deployed separately. This is all very good news for React.

We've only scratched the surface of what can be accomplished with Hooks. In the next chapter, we'll dive a little deeper.

Chapter 7. Enhancing

