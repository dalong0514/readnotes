## 记忆时间

## 目录

0601 React State Management

0701 Enhancing Components with Hooks

## 0601. React State Management

Data is what makes our React components come to life. The user interface for recipes that we built in the last chapter is useless without the array of recipes. It's the recipes and the ingredients along with clear instructions that makes such an app worthwhile. Our user interfaces are tools that creators will use to generate content. In order to build the best tools possible for our content creators, we'll need to know how to effectively manipulate and change data.

In the last chapter, we constructed a component tree: a hierarchy of components that data was able to flow through as properties. Properties are half of the picture. State is the other half. The state of a React application is driven by data that has the ability to change. Introducing state to the recipe application could make it possible for chefs to create new recipes, modify existing recipes, and remove old ones.

2『 State 和 Property 在 React 的数据「地图」上各占半壁江山。做一张主题卡片。（2021-05-04）』—— 已完成

State and properties have a relationship with each other. When we work with React applications, we gracefully compose components that are tied together based on this relationship. When the state of a component tree changes, so do the properties. The new data flows through the tree, causing specific leaves and branches to render to reflect the new content.

In this chapter, we're going to bring applications to life by introducing state. We'll learn to create stateful components and how state can be sent down a component tree and user interactions back up the component tree. We'll learn techniques for collecting form data from users. And we'll take a look at the various ways in which we can separate concerns within our applications by introducing stateful context providers.

### 6.1 Building a Star Rating Component

We would all be eating terrible food and watching terrible movies without the five-star rating system. If we plan on letting users drive the content on our website, we'll need a way to know if that content is any good or not. That makes the StarRating component one of the most important React components you'll ever build (see Figure 6-1).

Figure 6-1. StarRating component

The StarRating component will allow users to rate content based on a specific number of stars. Content that's no good gets one star. Highly recommended content gets five stars. Users can set the rating for specific content by clicking on a specific star. First, we'll need a star, and we can get one from react-icons:

```
npm i react-icons
```

react-icons is an npm library that contains hundreds of SVG icons that are distributed as React components. By installing it, we just installed several popular icon libraries that contain hundreds of common SVG icons. You can browse all the icons in the library. We're going to use the star icon from the Font Awesome collection: 

```js
import React from "react";
import { FaStar } from "react-icons/fa"; 
export default function StarRating() {
  return [
    <FaStar color="red" />,
    <FaStar color="red" />,
    <FaStar color="red" />,
    <FaStar color="grey" />,
    <FaStar color="grey" />
  ];
}
```

Here, we've created a StarRating component that renders five SVG stars that we've imported from react-icons. The first three stars are filled in with red, and the last two are grey. We render the stars first because seeing them gives us a roadmap for what we'll have to build.

A selected star should be filled in with red, and a star that's not selected should be greyed out. Let's create a component that automatically files the stars based upon the selected property: 

```js
const Star = ({ selected = false }) => (
  <FaStar color={selected ? "red" : "grey"} />
);
```

The Star component renders an individual star and uses the selected property to fill it with the appropriate color. If the selected property is not passed to this component, we'll assume that the star should not be selected and by default will be filled in with grey.

The 5-star rating system is pretty popular, but a 10-star rating system is far more detailed. We should allow developers to select the total number of stars they wish to use when they add this component to their app. This can be accomplished by adding a totalStars property to the StarRating component:

```js
const createArray = length => [...Array(length)]; 

export default function StarRating({ totalStars = 5 }) {
  return createArray(totalStars).map((n, i) => <Star key={i} />);
}
```

Here, we added the createArray function from Chapter 2. All we have to do is supply the length of the array that we want to create and we get a new array at that length. We use this function with the totalStars property to create an array of a specific length. Once we have an array, we can map over it and render Star components. By default, totalStars is equal to 5, which means this component will render 5 grey stars, as shown in Figure 6-2.

Figure 6-2. Five stars are displayed

### 6.2 The useState Hook

It's time to make the StarRating component clickable, which will allow our users to change the rating. Since the rating is a value that will change, we'll store and change that value using React state. We incorporate state into a function component using a React feature called Hooks. Hooks contain reusable code logic that is separate from the component tree. They allow us to hook up functionality to our components. React ships with several built-in hooks we can use out of the box. In this case, we want to add state to our React component, so the first hook we'll work with is React's useState hook. This hook is already available in the react package; we simply need to import it: 

```js
import React, { useState } from "react"; 
import { FaStar } from "react-icons/fa"; 
```

The stars the user has selected represents the rating. We'll create a state variable called selectedStars, which will hold the user's rating. We'll create this variable by adding the useState hook directly to the StarRating component:

```js
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
```

We just hooked this component up with state. The useState hook is a function that we can invoke to return an array. The first value of that array is the state variable we want to use. In this case, that variable is selectedStars, or the number of stars the StarRating will color red.

useState returns an array. We can take advantage of array destructuring, which allows us to name our state variable whatever we like. The value we send to the useState function is the default value for the state variable. In this case, selectedStars will initially be set to 3, as shown in Figure 6-3.

Figure 6-3. Three of five stars are selected

In order to collect a different rating from the user, we'll need to allow them to click on any of our stars. This means we'll need to make the stars clickable by adding an onClick handler to the FaStar component:

```js
const Star = ({ selected = false, onSelect = f => f }) => (
  <FaStar color={selected ? "red" : "grey"} onClick={onSelect} />
);
```

Here, we modified the star to contain an onSelect property. Check it out: this property is a function. When a user clicks on the FaStar component, we'll invoke this function, which can notify its parent that a star has been clicked. The default value for this function is f => f.

This is simply a fake function that does nothing; it just returns whatever argument was sent to it. However, if we do not set a default function and the onSelect property is not defined, an error will occur when we click the FaStar component because the value for onSelect must be a function. Even though f => f does nothing, it is a function, which means it can be invoked without causing errors. If an onSelect property is not defined, no problem. React will simply invoke the fake function and nothing will happen.

Now that our Star component is clickable, we'll use it to change the state of the StarRating:

```js
export default function StarRating({ totalStars = 5 }) {
  const [selectedStars, setSelectedStars] = useState(0); 
  return (
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
```

In order to change the state of the StarRating component, we'll need a function that can modify the value of selectedStars. The second item in the array that's returned by the useState hook is a function that can be used to change the state value. Again, by destructuring this array, we can name that function whatever we like. In this case, we're calling it setSelectedStars, because that's what it does: it sets the value of selectedStars.

The most important thing to remember about Hooks is that they can cause the component they're hooked into to rerender. Every time we invoke the setSelectedStars function to change the value of selectedStars, the StarRating function component will be reinvoked by the hook, and it will render again, this time with a new value for selectedStars. This is why Hooks are such a killer feature.

When data within the hook changes, they have the power to rerender the component they're hooked into with new data.

2『钩子的核心作用在于重新渲染，做一张主题卡片。（2021-05-08）』—— 已完成

The StarRating component will be rerendered every time a user clicks a Star. When the user clicks the Star, the onSelect property of that star is invoked. When the onSelect property is invoked, we'll invoke the setSelectedStars function and send it the number of the star that was just selected. We can use the i variable from the map function to help us calculate that number. When the map function renders the first Star, the value for i is 0. This means that we need to add 1 to this value to get the correct number of stars. When setSelectedStars is invoked, the StarRating component is invoked with a the value for selectedStars, as shown in Figure 6-4.

Figure 6-4. Hooks in React developer tools

The React developer tools will show you which Hooks are incorporated with specific components. When we render the StarRating component in the browser, we can view debugging information about that component by selecting it in the developer tools.

In the column on the right, we can see that the StarRating component incorporates a state Hook that has a value of 2. As we interact with the app, we can watch the state value change and the component tree rerender with the corresponding number of stars selected.

REACT STATE THE「OLD WAY」

In previous versions of React, before v16.8.0, the only way to add state to a component was to use a class component. This required not only a lot of syntax, but it also made it more difficult to reuse functionality across components. Hooks were designed to solve problems presented with class components by providing a solution to incorporate functionality into function components.

The following code is a class component. This was the original StarRating component that was printed in the first edition of this book:

```js
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
```

This class component does the same thing as our function component with noticeably more code. Additionally, it introduces more confusion thorough the use of the this keyword and function binding.

As of today, this code still works. We're no longer covering class components in this book because they're no longer needed. Function components and Hooks are the future of React, and we're not looking back. There could come a day where class components are officially deprecated, and this code will no longer be supported.

### 6.3 Refactoring for Advanced Reusability

Right now, the Star component is ready for production. You can use it across several applications when you need to obtain a rating from a user. However, if we were to ship this component to npm so that anyone in the world could use it to obtain ratings from users, we may want to consider handling a couple more use cases.

First, let's consider the style property. This property allows you to add CSS styles to elements. It is highly possible that a future developer, even yourself, could come across the need to modify the style of your entire container. They may attempt to do something like this:

```js
export default function App() {
  return <StarRating style={{ backgroundColor: "lightblue" }} />;
}
```

All React elements have style properties. A lot of components also have style properties. So attempting to modify the style for the entire component seems sensible.

All we need to do is collect those styles and pass them down to the StarRating container. Currently, the StarRating does not have a single container because we are using a React fragment. To make this work, we'll have to upgrade from a fragment to a div element and pass the styles to that div:

```js
export default function StarRating({ style = {}, totalStars = 5 }) {
  const [selectedStars, setSelectedStars] = useState(0); 
  return (
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
```

In the code above, we replaced the fragment with a div element and then applied styles to that div element. By default we assign that div a padding of 5px, and then we use the spread operator to apply the rest of the properties from the style object to the div style.

Additionally, we may find developers who attempt to implement other common properties properties to the entire star rating:

```js
export default function App() {
  return (
    <StarRating
      style={{ backgroundColor: "lightblue" }}
      onDoubleClick={e => alert("double click")}
    />
  );
}
```

In this sample, the user is trying to add a double-click method to the entire StarRating component. If we feel it is necessary, we can also pass this method along with any other properties down to our containing div:

```js
export default function StarRating({ style = {}, totalStars = 5, ...props}) {
  const [selectedStars, setSelectedStars] = useState(0); 
  return (
    <div style={{ padding: 5, ...style }} {...props}>
    ...
    </div>
  );
}
```

The first step is to collect any and all properties that the user may be attempting to add to the StarRating. We gather these properties using the spread operator: `...props`. Next, we'll pass all of these remaining properties down to the div element: `{...props}`.

By doing this, we make two assumptions. First, we are assuming that users will add only those properties that are supported by the div element. Second, we are assuming that our user can't add malicious properties to the component. This is not a blanket rule to apply to all of your components. In fact, it's only a good idea to add this level of support in certain situations.

The real point is that it's important to think about how the consumers of your component may try to use it in the future.

### 6.4 State in Component Trees

It's not a great idea to use state in every single component. Having state data distributed throughout too many of your components will make it harder to track down bugs and make changes within your application. This occurs because it's hard to keep track of where the state values live within your component tree. It's easier to understand your application's state, or state for a specific feature, if you manage it from one location. There are several approaches to this methodology, and the first one we'll analyze is storing state at the root of the component tree and passing it down to child components via props.

1-3『这里的信息，跟 React 官网那个「井字棋」的教程关联上了，状态数据的管理一层层抽象到父组件里去。（2021-05-08）』

Let's build a small application that can be used to save a list of colors. We'll call the app the「Color Organizer」, and it will allow users to associate a list of colors with a custom title and rating. To get started, a sample dataset may look like the following:

```js
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
```

The color-data.json file contains an array of three colors. Each color has an id, title, color, and rating. First, we'll create a UI consisting of React components that will be used to display this data in a browser. Then we'll allow the users to add new colors as well as rate and remove colors from the list.

#### 6.4.1 Sending State Down a Component Tree

In this iteration, we'll store state in the root of the Color Organizer, the App component, and pass the colors down to child components to handle the rendering. The App component will be the only component within our application that holds state. We'll add the list of colors to the App with the useState hook:

```js
import React, { useState } from "react"; 
import colorData from "./color-data.json"; 
import ColorList from "./ColorList.js";

export default function App() {
  const [colors] = useState(colorData);
  return <ColorList colors={colors} />;
}
```

The App component sits at the root of our tree. Adding useState to this component hooks it up with state management for colors. In this example, the colorData is the array of sample colors from above. The App component uses the colorData as the initial state for colors.

From there, the colors are passed down to a component called the ColorList:

```js
import React from "react";
import Color from "./Color";

export default function ColorList({ colors = [] }) {
  if(!colors.length) return <div>No Colors Listed.</div>; 
  return (
    <div>
      { colors.map(color => <Color key={color.id} {...color} />) }
    </div>
  );
}
```

The ColorList receives the colors from the App component as props. If the list is empty, this component will display a message to our users. When we have a color array, we can map over it and pass the details about each color farther down the tree to the Color component: 

```js
export default function Color({ title, color, rating }) {
  return (
    <section>
      <h1>{title}</h1>
      <div style={{ height: 50, backgroundColor: color }} />
      <StarRating selectedStars={rating} />
    </section>
  );
}
```

The Color component expects three properties: title, color, and rating. These values are found in each color object and were passed to this component using the spread operator `<Color {...color} />`.

This takes each field from the color object and passes it to the Color component as a property with the same name as the object key. The Color component displays these values. The title is rendered inside of an h1 element. The color value is displayed as the backgroundColor for a div element. The rating is passed farther down the tree to the StarRating component, which will display the rating visually as selected stars:

```js
export default function StarRating({ totalStars = 5, selectedStars = 0 }) {
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
```

This StarRating component has been modified. We've turned it into a pure component. A pure component is a function component that does not contain state and will render the same user interface given the same props. We made this component a pure component because the state for color ratings are stored in the colors array at the root of the component tree. Remember that the goal of this iteration is to store state in a single location and not have it distributed through many different components within the tree.

NOTE: It is possible for the StarRating component to hold its own state and receive state from a parent component via props. This is typically necessary when distributing components for wider use by the community. We demonstrate this technique in the next chapter when we cover the useEffect hook.

At this point, we've finished passing state down the component tree from the App component all the way to each Star component that's filled red to visually represent the rating for each color. If we render the app based on the color-data.json file that was listed previously, we should see our colors in the browser, as shown in Figure 6-5.

Figure 6-5. Color Organizer rendered in the browser 

#### 6.4.2 Sending Interactions Back up a Component Tree

So far, we've rendered a representation of the colors array as UI by composing React components and passing data down the tree from parent component to child component via props. What happens if we want to remove a color from the list or change the rating of a color in our list? The colors are stored in state at the root of our tree. We'll need to collect interactions from child components and send them back up the tree to the root component where we can change the state.

For instance, let's say we wanted to add a Remove button next to each color's title that would allow users to remove colors from state. We would add that button to the Color component:

```js
import { FaTrash } from "react-icons/fa"; 

export default function Color({ id, title, color, rating, onRemove = f => f }) {
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
```

Here, we've modified the color by adding a button that will allow users to remove colors. First, we imported a trash can icon from react-icons. Next, we wrapped the FaTrash icon in a button. Adding an onClick handler to this button allows us to invoke the onRemove function property, which has been added to our list of properties along with the id. When a user clicks the Remove button, we'll invoke removeColor and pass it the id of the color that we want to remove.

That is why the id value has also been gathered from the Color component's properties.

This solution is great because we keep the Color component pure. It doesn't have state and can easily be reused in a different part of the app or another application altogether. The Color component is not concerned with what happens when a user clicks the Remove button. All it cares about is notifying the parent that this event has occurred and passing the information about which color the user wishes to remove. It's now the parent's responsibility to handle this event: 

```js
export default function ColorList({ colors = [], onRemoveColor = f => f }) {
  if (!colors.length) return <div>No Colors Listed. (Add a Color)</div>; 
  return (
    colors.map(color => (
      <Color key={color.id} {...color} onRemove={onRemoveColor} />
    ))
  )
}
```

The Color component's parent is the ColorList. This component also doesn't have access to state. Instead of removing the color, it simply passes the event up to its parent. It accomplishes this by adding an onRemoveColor function property. If a Color component invokes the onRemove property, the ColorList will in turn invoke its onRemoveColor property and send the responsibility for removing the color up to its parent. The color's id is still being passed to the onRemoveColor function.

The parent of the ColorList is the App. This component is the component that has been hooked up with state. This is where we can capture the color id and remove the color in state:

```js
export default function App() {
  const [colors, setColors] = useState(colorData);
  return (
    <ColorList
      colors={colors}
      onRemoveColor={id => {
        const newColors = colors.filter(color => color.id !== id); 
        setColors(newColors);
      }}
    />
  );
}
```

First, we add a variable for setColors. Remember that the second argument in the array returned by useState is a function we can use to modify the state. When the ColorList raises an onRemoveColor event, we capture the id of the color to remove from the arguments and use it to filter the list of colors to exclude the color the user wants to remove.

Next, we change the state. We use the setColors function to change change the array of colors to the newly filtered array.

Changing the state of the colors array causes the App component to be rerendered with the new list of colors. Those new colors are passed to the ColorList component, which is also rerendered. It will render Color components for the remaining colors and our UI will reflect the changes we've made by rendering one less color.

If we want to rate the colors that are stored in the App components state, we'll have to repeat the process with an onRate event. First, we'll collect the new rating from the individual star that was clicked and pass that value to the parent of the StarRating:

```js
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
```

Then, we'll grab the rating from the onRate handler we added to the StarRating component. We'll then pass the new rating along with the id of the color to be rated up to the Color component's parent via another onRate function property:

```js
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
```

In the ColorList component, we'll have to capture the onRate event from individual color components and pass them up to its parent via the onRateColor function property:

```js
export default function ColorList({
  colors = [],
  onRemoveColor = f => f,
  onRateColor = f => f
  }) {
  if (!colors.length) return <div>No Colors Listed. (Add a Color)</div>; 
  return (
    <div className="color-list">
    {
      colors.map(color => (
        <Color
          key={color.id}
          {...color}
          onRemove={onRemoveColor}
          onRate={onRateColor}
        />
      ))
    }
    </div>
  )
}
```

Finally, after passing the event up through all of these components, we'll arrive at the App, where state is stored and the new rating can be saved:

```js
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
        const newColors = colors.filter(color => color.id !== id); 
        setColors(newColors);
      }}
    />
  );
}
```

The App component will change color ratings when the ColorList invokes the onRateColor property with the id of the color to rate and the new rating. We'll use those values to construct an array of new colors by mapping over the existing colors and changing the rating for the color that matches the id property. Once we send the newColors to the setColors function, the state value for colors will change and the App component will be invoked with a new value for the colors array.

Once the state of our colors array changes, the UI tree is rendered with the new data. The new rating is reflected back to the user via red stars. Just as we passed data down a component tree via props, interactions can be passed back up the tree along with data via function properties.

### 6.5 Building Forms

For a lot of us, being a web developer means collecting large amounts of information from users with forms. If this sounds like your job, then you'll be building a lot of form components with React. All of the HTML form elements that are available to the DOM are also available as React elements, which means that you may already know how to render a form with JSX:

```html
<form>
  <input type="text" placeholder="color title..." required />
  <input type="color" required />
  <button> ADD </button>
</form>
```

This form element has three child elements: two input elements and a button. The first input element is a text input that will be used to collect the title value for new colors. The second input element is an HTML color input that will allow users to pick a color from a color wheel. We'll be using basic HTML form validation, so we've marked both inputs as required. The ADD button will be used to add a new color.

#### 6.5.1 Using Refs

When it's time to build a form component in React, there are several patterns available to you. One of these patterns involves accessing the DOM node directly using a React feature called refs. In React, a ref is an object that stores values for the lifetime of a component. There are several use cases that involve using refs. In this section, we'll look at how we can access a DOM node directly with a ref.

React provides us with a useRef hook that we can use to create a ref. We'll use this hook when building the AddColorForm component: 

```js
import React, { useRef } from "react";

export default function AddColorForm({ onNewColor = f => f }) {
  const txtTitle = useRef();
  const hexColor = useRef();
  const submit = e => { ... }
  return (...)
}
```

First, when creating this component, we'll also create two refs using the useRef hook. The txtTitle ref will be used to reference the text input we've added to the form to collect the color title. The hexColor ref will be used to access hexadecimal color values from the HTML color input. We can set the values for these refs directly in JSX using the ref property:

```js
return (
  <form onSubmit={submit}>
    <input ref={txtTitle} type="text" placeholder="color title..."
    required />
    <input ref={hexColor} type="color" required />
    <button>ADD</button>
  </form>
  );
}
```

Here, we set the value for the txtTitle and hexColor refs by adding the ref attribute to these input elements in JSX. This creates a current field on our ref object that references the DOM element directly. This provides us access to the DOM element, which means we can capture its value. When the user submits this form by clicking the ADD button, we'll invoke the submit function:

```js
const submit = e => {
  e.preventDefault();
  const title = txtTitle.current.value;
  const color = hexColor.current.value;
  onNewColor(title, color);
  txtTitle.current.value = "";
  hexColor.current.value = "";
};
```

When we submit HTML forms, by default, they send a POST request to the current URL with the values of the form elements stored in the body. We don't want to do that. This is why the first line of code in the submit function is e.preventDefault(), which prevents the browser from trying to submit the form with a POST request.

Next, we capture the current values for each of our form elements using their refs. These values are then passed up to this component's parent via the onNewColor function property. Both the title and the hexadecimal value for the new color are passed as function arguments.

Finally, we reset the value attribute for both inputs to clear the data and prepare the form to collect another color.

Did you notice the subtle paradigm shift that has occurred by using refs? We're mutating the value attribute of DOM nodes directly by setting them equal to "" empty strings. This is imperative code. The AddColorForm is now what we call an uncontrolled component because it uses the DOM to save the form values. Sometimes using uncontrolled component can get you out of problems. For instance, you may want to share access to a form and its values with code outside of React. However, a controlled component is a better approach.

#### 6.5.2 Controlled Components

In a controlled component, the from values are managed by React and not the DOM. They do not require us to use refs. They do not require us to write imperative code. Adding features like robust form validation is much easier when working with a controlled component. Let's modify the AddColorForm by giving it control over the form's state:

```js
import React, { useState } from "react"; 

export default function AddColorForm({ onNewColor = f => f }) {
  const [title, setTitle] = useState("");
  const [color, setColor] = useState("#000000"); 
  const submit = e => { ... };
  return ( ... );
}
```

First, instead of using refs, we're going to save the values for the title and color using React state. We'll create variables for title and color. Additionally, we'll define the functions that can be used to change state: setTitle and setColor.

Now that the component controls the values for title and color, we can display them inside of the form input elements by setting the value attribute. Once we set the value attribute of an input element, we'll no longer be able to change with the form. The only way to change the value at this point would be to change the state variable every time the user types a new character in the input element. That's exactly what we'll do:

```js
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
```

This controlled component now sets the value of both input elements using the title and color from state. Whenever these elements raise an onChange event, we can access the new value using the event argument. The event.target is a reference to the DOM element, so we can obtain the current value of that element with event.target.value. When the title changes, we'll invoke setTitle to change the title value in state. Changing that value will cause this component to rerender, and we can now display the new value for title inside the input element. Changing the color works exactly the same way.

When it's time to submit the form, we can simply pass the state values for title and color to the onNewColor function property as arguments when we invoke it. The setTitle and setColor functions can be used to reset the values after the new color has been passed to the parent component:

```js
const submit = e => {
  e.preventDefault();
  onNewColor(title, color);
  setTitle("");
  setColor("");
}; 
```

It's called a controlled component because React controls the state of the form. It's worth pointing out that controlled form components are rerendered, a lot. Think about it: every new character typed in the title field causes the AddColorForm to rerender. Using the color wheel in the color picker causes this component to rerender way more than the title field because the color value repeatedly changes as the user drags the mouse around the color wheel. This is OK — React is designed to handle this type of workload. Hopefully, knowing that controlled components are rerendered frequently will prevent you from adding some long and expensive process to this component. At the very least, this knowledge will come in handy when you're trying to optimize your React components.

#### 6.5.3 Creating Custom Hooks

When you have a large form with a lot of input elements, you may be tempted to copy and paste these two lines of code:

```js
value={title}
onChange={event => setTitle(event.target.value)}
```

It might seem like you're working faster by simply copying and pasting these properties into every form element while tweaking the variable names along the way. However, whenever you copy and paste code, you should hear a tiny little alarm sound in your head. Copying and pasting code suggests that there's something redundant enough to abstract away in a function.

We can package the details necessary to create controlled form components into a custom hook. We could create our own useInput hook where we can abstract away the redundancy involved with creating controlled form inputs:

```js
import { useState } from "react";

export const useInput = initialValue => {
  const [value, setValue] = useState(initialValue);
  return [
    { value, onChange: e => setValue(e.target.value) },
    () => setValue(initialValue)
  ];
};
```

This is a custom hook. It doesn't take a lot of code. Inside of this hook, we're still using the useState hook to create a state value. Next, we return an array. The first value of the array is the object that contains the same properties we were tempted to copy and paste: the value from state along with an onChange function property that changes that value in state. The second value in the array is a function that can be reused to reset the value back to its initial value. We can use our hook inside of the AddColorForm:

```js
import React from "react";
import { useInput } from "./hooks";

export default function AddColorForm({ onNewColor = f => f }) {
  const [titleProps, resetTitle] = useInput(""); 
  const [colorProps, resetColor] = useInput("#000000"); 
  const submit = event => { ... }
  return ( ... )
}
```

The useState hook is encapsulated within our useInput hook. We can obtain the properties for both the title and the color by destructuring them from the first value of the returned array. The second value of this array contains a function we can use to reset the value property back to its initial value, an empty string. The titleProps and colorProps are ready to be spread into their corresponding input elements:

```js
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
```

Spreading these properties from our custom hook is much more fun than pasting them. Now both the title and the color inputs are receiving properties for their value and onChange events. We've used our hook to create controlled form inputs without worrying about the underlying implementation details. The only other change we need to make is when this form is submitted:

```js
const submit = event => {
  event.preventDefault();
  onNewColor(titleProps.value, colorProps.value);
  resetTitle();
  resetColor();
};
```

Within the submit function, we need to be sure to grab the value for both the title and the color from their properties. Finally, we can use the custom reset functions that were returned from the useInput hook.

Hooks are designed to be used inside of React components. We can compose hooks within other hooks because eventually the customized hook will be used inside of a component. Changing the state within this hook still causes the AddColorForm to rerender with new values for titleProps or colorProps.

#### 6.5.4 Adding Colors to State

Both the controlled form component and the uncontrolled from component pass the values for title and color to the parent component via the onNewColor function. The parent doesn't care whether we used a controlled component or an uncontrolled component; it only wants the values for the new color.

Let's add the AddColorForm, whichever one you choose, to the the App component. When the onNewColor property is invoked, we'll save the new color in state:

```js
import React, { useState } from "react"; 
import colorData from "./color-data.json"; 
import ColorList from "./ColorList.js";
import AddColorForm from "./AddColorForm"; 
import { v4 } from "uuid";

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
```

When a new color is added, the onNewColor property is invoked. The title and hexadecimal value for the new color are passed to this function as arguments. We use these arguments to create a new array of colors. First, we spread the current colors from state into the new array. Then we add an entirely new color object using the title and color values. Additionally, we set the rating of the new color to 0 because it has not yet been rated. We also use the v4 function found in the uuid package to generate a new unique id for the color. Once we have an array of colors that contains our new color, we save it to state by invoking setColors. This causes the App component to rerender with a new array of colors. That new array will be used to update the UI. We'll see the new color at bottom of the list.

With this change, we've completed the first iteration of the Color Organizer. Users can now add new colors to the list, remove colors from the list, and rate any existing color on that list.

### 6.6 React Context

Storing state in one location at the root of our tree was an important pattern that helped us all be more successful with early versions of React. Learning to pass state both down and up a component tree via properties is a necessary right of passage for any React developer — it's something we should all know how to do. However, as React evolved and our component trees got larger, following this principle slowly became more unrealistic. It's hard for many developers to maintain state in a single location at the root of a component tree for a complex application. Passing state down and up the tree through dozens of components is tedious and bug ridden.

The UI elements that most of us work on are complex. The root of the tree is often very far from the leaves. This puts data the application depends on many layers away from the components that use the data.

Every component must receive props that they only pass to their children. This will bloat our code and make our UI harder to scale.

Passing state data through every component as props until it reaches the component that needs to use it is like taking the train from San Francisco to DC. On the train, you'll pass through every state, but you won't get off until you reach your destination (see Figure 6-6).

Figure 6-6. Train from San Francisco to DC

It's obviously more efficient to fly from San Francisco to DC. This way, you don't have to pass through every state — you simply fly over them (Figure 6-7).

Figure 6-7. Flight from San Francisco to DC

In React, context is like jet-setting for your data. You can place data in React context by creating a context provider. A context provider is a React component you can wrap around your entire component tree or specific sections of your component tree. The context provider is the departing airport where your data boards the plane. It's also the airline hub. All flights depart from that airport to different destinations. Each destination is a context consumer. The context consumer is the React component that retrieves the data from context. This is the destination airport where your data lands, deplanes, and goes to work.

Using context still allows to us store state data in a single location, but it doesn't require us to pass that data through a bunch of components that don't need it.

#### 6.6.1 Placing Colors in Context

In order to use context in React, we must first place some data in a context provider and add that provider to our component tree. React comes with a function called createContext that we can use to create a new context object. This object contains two components: a context Provider and a Consumer.

Let's place the default colors found in the color-data.json file into context. We'll add context to the index.js file, the entry point of our application:

```js
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
```

Using createContext, we created a new instance of React context that we named ColorContext. The color context contains two components: ColorContext.Provider and ColorContext.Consumer. We need to use the provider to place the colors in state. We add data to context by setting the value property of the Provider. In this scenario, we added an object containing the colors to context. Since we wrapped the entire App component with the provider, the array of colors will made available to any context consumers found in our entire component tree.

It's important to notice that we've also exported the ColorContext from this location. This is necessary because we will need to access the ColorContext.Consumer when we want to obtain the colors from context.

NOTE: A context Provider doesn't always have to wrap an entire application. It's not only OK to wrap specific sections components with a context Provider, it can make your application more efficient. The Provider will only provide context values to its children. It's OK to use multiple context providers. In fact, you may be using context providers in your React app already without even knowing it. Many npm packages designed to work with React use context behind the scenes.

Now that we're providing the colors value in context, the App component no longer needs to hold state and pass it down to its children as props. We've made the App component a「flyover」component. The Provider is the App component's parent, and it's providing the colors in context. The ColorList is the App component's child, and it can obtain the colors directly on its own. So the app doesn't need to touch the colors at all, which is great because the App component itself has nothing to do with colors. That responsibility has been delegated farther down the tree.

We can remove a lot of lines of code from the App component. It only needs to render the AddColorForm and the ColorList. It no longer has to worry about the data:

```js
import React from "react";
import ColorList from "./ColorList.js";
import AddColorForm from "./AddColorForm"; 

export default function App() {
  return (
  <>
    <AddColorForm />
    <ColorList />
  </>
  );
}
```

#### 6.6.2 Retrieving Colors with useContext

The addition of Hooks makes working with context a joy. The useContext hook is used to obtain values from context, and it obtains those values we need from the context Consumer. The ColorList component no longer needs to obtain the array of colors from its properties. It can access them directly via the useContext hook: 

```js
import React, { useContext } from "react";
import { ColorContext } from "./";
import Color from "./Color";

export default function ColorList() {
  const { colors } = useContext(ColorContext);
  if (!colors.length) return <div>No Colors Listed. (Add a Color)</div>; 
  return (
    <div className="color-list">
      {
        colors.map(color => <Color key={color.id} {...color} />)
      }
    </div>
  );
}
```

Here, we've modified the ColorList component and removed the colors=[] property because the colors are being retrieved from context. The useContext hook requires the context instance to obtain values from it. The ColorContext instance is being imported from the index.js file where we create the context and add the provider to our component tree. The ColorList can now construct a user interface based on the data that has been provided in context.

USING CONTEXT CONSUMER

The Consumer is accessed within the useContext hook, which means that we no longer have to work directly with the consumer component. Before Hooks, we would have to obtain the colors from context using a pattern called render props within the context consumer. Render props are passed as arguments to a child function. The following example is how you would use the consumer to obtain the colors from context:

```js
export default function ColorList() {
  return (
    <ColorContext.Consumer>
    {context => {
      if (!context.colors.length) return <div>No Colors Listed. (Add a Color)</div>; 
      return (
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
```

#### 6.6.3 Stateful Context Providers

The context provider can place an object into context, but it can't mutate the values in context on its own. It needs some help from a parent component. The trick is to create a stateful component that renders a context provider. When the state of the stateful component changes, it will rerender the context provider with new context data.

Any of the context providers' children will also be rerendered with the new context data. The stateful component that renders the context provider is our custom provider. That is: that's the component that will be used when it's time to wrap our App with the provider. In a brand-new file, let's create a ColorProvider:

```js
import React, { createContext, useState } from "react"; 
import colorData from "./color-data.json";
const ColorContext = createContext();

export default function ColorProvider ({ children }) {
  const [colors, setColors] = useState(colorData);
  return (
    <ColorContext.Provider value={{ colors, setColors }}>
      {children}
    </ColorContext.Provider>
  );
};
```

The ColorProvider is a component that renders the ColorContext.Provider. Within this component, we've created a state variable for colors using the useState hook. The initial data for colors is still being populated from color-data.json. Next, the ColorProvider adds the colors from state to context using the value property of the ColorContext.Provider. Any children rendered within the ColorProvider will be wrapped by the ColorContext.Provider and will have access to the colors array from context.

You may have noticed that the setColors function is also being added to context. This gives context consumers the ability to change the value for colors. Whenever setColors is invoked, the colors array will change. This will cause the ColorProvider to rerender, and our UI will update itself to display the new colors array.

Adding setColors to context may not be the best idea. It invites other developers and you to make mistakes later on down the road when using it. There are only three options when it comes to changing the value of the colors array: users can add colors, remove colors, or rate colors. It's a better idea to add functions for each of these operations to context. This way, you don't expose the setColors function to consumers; you only expose functions for the changes they're allowed to make:

```js
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
  const removeColor = id => setColors(colors.filter(color => color.id !== id));
  return (
    <ColorContext.Provider value={{ colors, addColor, removeColor, rateColor }}>
      {children}
    </ColorContext.Provider>
  );
};
```

That looks better. We added functions to context for all of the operations that can be made on the colors array. Now, any component within our tree can consume these operations and make changes to colors using simple functions that we can document.

#### 6.6.4 Custom Hooks with Context

There's one more killer change we can make. The introduction of Hooks has made it so that we don't have to expose context to consumer components at all. Let's face it: context can be confusing for team members who aren't reading this book. We can make everything much easier for them by wrapping context in a custom hook. Instead of exposing the ColorContext instance, we can create a hook called useColors that returns the colors from context:

```js
import React, { createContext, useState, useContext } from "react"; 
import colorData from "./color-data.json"; 
import { v4 } from "uuid";

const ColorContext = createContext();
export const useColors = () => useContext(ColorContext); 
```

This one simple change has a huge impact on architecture. We've wrapped all of the functionality necessary to render and work with stateful colors in a single JavaScript module. Context is contained to this module yet exposed through a hook. This works because we return context using the useContext hook, which has access to the ColorContext locally in this file. It's now appropriate to rename this module color-hooks.js and distribute this functionality for wider use by the community.

Consuming colors using the ColorProvider and the useColors hook is a joyous event. This is why we program. Let's take this hook out for a spin in the current Color Organizer app. First, we need to wrap our App component with the custom ColorProvider. We can do this in the index.js file:

```js
import React from "react";
import { ColorProvider } from "./color-hooks.js"; 
import { render } from "react-dom";
import App from "./App";

render(
  <ColorProvider>
    <App />
  </ColorProvider>,
  document.getElementById("root")
);
```

Now, any component that's a child of the App can obtain the colors from the useColors hook. The ColorList component needs to access the colors array to render the colors on the screen:

```js
import React from "react";
import Color from "./Color";
import { useColors } from "./color-hooks"; 

export default function ColorList() {
  const { colors } = useColors();
  return ( ... );
}
```

We've removed any references to context from this component. Everything it needs is now being provided from our hook. The Color component could use our hook to obtain the functions for rating and removing colors directly:

```js
import React from "react";
import StarRating from "./StarRating";
import { useColors } from "./color-hooks"; 

export default function Color({ id, title, color, rating }) {
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
```

Now, the Color component no longer needs to pass events to the parent via function props. It has access to the rateColor and removeColor functions in context. They're easily obtained through the useColors hook. This is a lot of fun, but we're not finished yet. The AddColorForm can also benefit from the useColors hook:

```js
import React from "react";
import { useInput } from "./hooks";
import { useColors } from "./color-hooks"; 

export default function AddColorForm() {
  const [titleProps, resetTitle] = useInput(""); 
  const [colorProps, resetColor] = useInput("#000000"); const { addColor } = useColors();
  const submit = e => {
    e.preventDefault();
    addColor(titleProps.value, colorProps.value);
    resetTitle();
    resetColor();
  };
  return ( ... );
}
```

The AddColorForm component can add colors directly with the addColor function. When colors are added, rated, or removed, the state of the colors value in context will change. When this change happens, the children of the ColorProvider are rerendered with new context data. All of this is happening through a simple hook.

Hooks provide software developers with the stimulation they need to stay motivated and enjoy frontend programming. This is primarily because they're an awesome tool for separating concerns. Now, React components only need to concern themselves with rendering other React components and keeping the user interface up to date. React Hooks can concern themselves with the logic required to make the app work. Both the UI and Hooks can be developed separately, tested separately, and even deployed separately. This is all very good news for React.

We've only scratched the surface of what can be accomplished with Hooks. In the next chapter, we'll dive a little deeper.

## 0701. Enhancing Components with Hooks

Rendering is the heartbeat of a React application. When something changes (props, state), the component tree rerenders, reflecting the latest data as a user interface. So far, useState has been our workhorse for describing how our components should be rendering. But we can do more. There are more Hooks that define rules about why and when rendering should happen. There are more Hooks that enhance rendering performance. There are always more Hooks to help us out.

In the last chapter, we introduced useState, useRef, and useContext, and we saw that we could compose these Hooks into our own custom Hooks: useInput and useColors. There's more where that came from, though. React comes with more Hooks out of the box. In this chapter, we're going to take a closer look at useEffect, useLayoutEffect, and useReducer. All of these are vital when building applications.

We'll also look at useCallback and useMemo, which can help optimize our components for performance.

### 7.1 Introducing useEffect

We now have a good sense of what happens when we render a component. A component is simply a function that renders a user interface. Renders occur when the app first loads and when props and state values change. But what happens when we need to do something after a render? Let's take a closer look.

Consider a simple component, the Checkbox. We're using useState to set a checked value and a function to change the value of checked: setChecked. A user can check and uncheck the box, but how might we alert the user that the box has been checked? Let's try this with an alert, as it's a great way to block the thread:

```js
import React, { useState } from "react"; 
function Checkbox() {
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
```

We've added the alert before the render to block the render. The component will not render until the user clicks the OK button on the alert box. Because the alert is blocking, we don't see the next state of the checkbox rendered until clicking OK.

That isn't the goal, so maybe we should place the alert after the return?

```js
function Checkbox {
  const [checked, setChecked] = useState(false); 
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
  alert(`checked: ${checked.toString()}`);
};
```

Scratch that. We can't call alert after the render because the code will never be reached. To ensure that we see the alert as expected, we can use useEffect. Placing the alert inside of the useEffect function means that the function will be called after the render, as a side effect: 

```js
function Checkbox {
  const [checked, setChecked] = useState(false); 
  useEffect(() => {
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
```

We use useEffect when a render needs to cause side effects. Think of a side effect as something that a function does that isn't part of the return. The function is the Checkbox. The Checkbox function renders UI. But we might want the component to do more than that. Those things we want the component to do other than return UI are called effects.

An alert, a console.log, or an interaction with a browser or native API is not part of the render. It's not part of the return. In a React app, though, the render affects the results of one of these events. We can use useEffect to wait for the render, then provide the values to an alert or a console.log:

```js
useEffect(() => {
  console.log(checked ? "Yes, checked" : "No, not checked");
});
```

Similarly, we could check in with the value of checked on render and then set that to a value in localStorage:

```js
useEffect(() => {
  localStorage.setItem("checkbox-value", checked);
});
```

We might also use useEffect to focus on a specific text input that has been added to the DOM. React will render the output, then call useEffect to focus the element:

```js
useEffect(() => {
  txtInputRef.current.focus();
});
```

On render, the txtInputRef will have a value. We can access that value in the effect to apply the focus. Every time we render, useEffect has access to the latest values from that render: props, state, refs, etc.

Think of useEffect as being a function that happens after a render. When a render fires, we can access the current state values within our component and use them to do something else. Then, once we render again, the whole thing starts over. New values, new renders, new effects.

#### 7.1.1 The Dependency Array

useEffect is designed to work in conjunction with other stateful Hooks like useState and the heretofore unmentioned useReducer, which we promise to discuss later in the chapter. React will rerender the component tree when the state changes. As we've learned, useEffect will be called after these renders. Consider the following, where the App component has two separate state values:

```js
import React, { useState, useEffect } from "react"; 
import "./App.css";

function App() {
  const [val, set] = useState("");
  const [phrase, setPhrase] = useState("example phrase"); 
  const createPhrase = () => {
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
```

val is a state variable that represents the value of the input field. The val changes every time the value of the input field changes. It causes the component to render every time the user types a new character. When the user clicks the Send button, the val of the text area is saved as the phrase, and the val is reset to "", which empties the text field.

This works as expected, but the useEffect hook is invoked more times than it should be. After every render, both useEffect Hooks are called:

```
typing "" // First Render 
saved phrase: "example phrase" // First Render 
typing "S" // Second Render 
saved phrase: "example phrase" // Second Render 
typing "Sh" // Third Render 
saved phrase: "example phrase" // Third Render
typing "Shr" // Fourth Render
saved phrase: "example phrase" // Fourth Render 
typing "Shre" // Fifth Render 
saved phrase: "example phrase" // Fifth Render 
typing "Shred" // Sixth Render 
saved phrase: "example phrase" // Sixth Render 
```

We don't want every effect to be invoked on every render. We need to associate useEffect hooks with specific data changes. To solve this problem, we can incorporate the dependency array. The dependency array can be used to control when an effect is invoked:

```js
useEffect(() => {
    console.log(`typing "${val}"`);
}, [val]);

useEffect(() => {
  console.log(`saved phrase: "${phrase}"`);
}, [phrase]);
```

We've added the dependency array to both effects to control when they're invoked. The first effect is only invoked when the val value has changed. The second effect is only invoked when the phrase value has changed. Now, when we run the app and take a look at the console, we'll see more efficient updates occurring:

```
typing "" // First Render 
saved phrase: "example phrase" // First Render 
typing "S" // Second Render typing "Sh" // Third Render 
typing "Shr" // Fourth Render typing "Shre" // Fifth Render 
typing "Shred" // Sixth Render typing "" // Seventh Render 
saved phrase: "Shred" // Seventh Render 
```

Changing the val value by typing into the input only causes the first effect to fire. When we click the button, the phrase is saved and the val is reset to "". It's an array after all, so it's possible to check multiple values in the dependency array. Let's say we wanted to run a specific effect any time either the val or phrase has changed:

```js
useEffect(() => {
  console.log("either val or phrase has changed");
}, [val, phrase]);
```

If either of those values changes, the effect will be called again. It's also possible to supply an empty array as the second argument to a useEffect function. An empty dependency array causes the effect to be invoked only once after the initial render:

```js
useEffect(() => {
  console.log("only once after initial render");
}, []);
```

Since there are no dependencies in the array, the effect is invoked for the initial render. No dependencies means no changes, so the effect will never be invoked again. Effects that are only invoked on the first render are extremely useful for initialization:

```js
useEffect(() => {
  welcomeChime.play();
}, []);
```

If you return a function from the effect, the function will be invoked when the component is removed from the tree:

```js
useEffect(() => {
  welcomeChime.play();
  return () => goodbyeChime.play();
}, []);
```

This means that you can use useEffect for setup and teardown. The empty array means that the welcome chime will play once on first render. Then, we'll return a function as a cleanup function to play a goodbye chime when the component is removed from the tree.

This pattern is useful in many situations. Perhaps we'll subscribe to a news feed on first render. Then we'll unsubscribe from the news feed with the cleanup function. More specifically, we'll start by creating a state value for posts and a function to change that value, called setPosts. Then we'll create a function, addPosts, that will take in the newest post and add it to the array. Then we can use useEffect to subscribe to the news feed and play the chime. Plus, we can return the cleanup functions, unsubscribing and playing the goodbye chime: 

```js
const [posts, setPosts] = useState([]);
const addPost = post => setPosts(allPosts => [post, ...allPosts]); 

useEffect(() => {
  newsFeed.subscribe(addPost);
  welcomeChime.play();
  return () => {
    newsFeed.unsubscribe(addPost);
    goodbyeChime.play();
  };
}, []);
```

This is a lot going on in useEffect, though. We might want to use a separate useEffect for the news feed events and another useEffect for the chime events:

```js
useEffect(() => {
  newsFeed.subscribe(addPost);
  return () => newsFeed.unsubscribe(addPost);
}, []);

useEffect(() => {
  welcomeChime.play();
  return () => goodbyeChime.play();
}, []);
```

Splitting functionality into multiple useEffect calls is typically a good idea. But let's enhance this even further. What we're trying to create here is functionality for subscribing to a news feed that plays different jazzy sounds for subscribing, unsubscribing, and whenever there's a new post. Everyone loves lots of loud sounds right? This is a case for a custom hook. Maybe we should call it useJazzyNews:

```js
const useJazzyNews = () => {
  const [posts, setPosts] = useState([]);
  const addPost = post => setPosts(allPosts => [post, ...allPosts]); 

  useEffect(() => {
    newsFeed.subscribe(addPost);
    return () => newsFeed.unsubscribe(addPost);
  }, []);
  
  useEffect(() => {
    welcomeChime.play()
    return () => goodbyeChime.play();
  }, []);
  return posts;
};
```

Our custom hook contains all of the functionality to handle a jazzy news feed, which means that we can easily share this functionality with our components. In a new component called NewsFeed, we'll use the custom hook:

```js
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
```

#### 7.1.2 Deep Checking Dependencies

So far, the dependencies we've added to the array have been strings. JavaScript primitives like strings, booleans, numbers, etc., are comparable. A string would equal a string as expected:

```js
if ("gnar" === "gnar") {
  console.log("gnarly!!");
}
```

However, when we start to compare objects, arrays, and functions, the comparison is different. For example, if we compared two arrays: 

```
if ([1, 2, 3] !== [1, 2, 3]) {
  console.log("but they are the same");
}
```

These arrays [1,2,3] and [1,2,3] are not equal, even though they look identical in length and in entries. This is because they are two different instances of a similar-looking array. If we create a variable to hold this array value and then compare, we'll see the expected output:

```js
const array = [1, 2, 3];
if (array === array) {
  console.log("because it's the exact same instance");
}
```

In JavaScript, arrays, objects, and functions are the same only when they're the exact same instance. So how does this relate to the useEffect dependency array? To demonstrate this, we're going to need a component we can force to render as much as we want. Let's build a hook that causes a component to render whenever a key is pressed:

```js
const useAnyKeyToRender = () => {
  const [, forceRender] = useState();
  useEffect(() => {
    window.addEventListener("keydown", forceRender); 
    return () => window.removeEventListener("keydown", forceRender);
  }, []);
};
```

At minimum, all we need to do to force a render is invoke a state change function. We don't care about the state value. We only want the state function: forceRender. (That's why we added the comma using array destructuring. Remember, from Chapter 2?) When the component first renders, we'll listen for keydown events. When a key is pressed, we'll force the component to render by invoking forceRender. As we've done before, we'll return a cleanup function where we stop listening to keydown events. By adding this hook to a component, we can force it to rerender simply by pressing a key.

With the custom hook built, we can use it in the App component (and any other component for that matter! Hooks are cool.):

```js
function App() {
  useAnyKeyToRender();
  useEffect(() => {
    console.log("fresh render");
  });
  return <h1>Open the console</h1>;
}
```

Every time we press a key, the App component is rendered. useEffect demonstrates this by logging「fresh render」to the console every time the App is rendered. Let's adjust useEffect in the App component to reference the word value. If word changes, we'll rerender: 

```js
const word = "gnar";
useEffect(() => {
  console.log("fresh render");
}, [word]);
```

Instead of calling useEffect on every keydown event, we would only call this after first render and any time the word value changes. It doesn't change, so subsequent rerenders don't occur. Adding a primitive or a number to the dependency array works as expected. The effect is invoked once. What happens if instead of a single word, we use an array of words?

```js
const words = ["sick", "powder", "day"]; 
useEffect(() => {
  console.log("fresh render");
}, [words]);
```

The variable words is an array. Because a new array is declared with each render, JavaScript assumes that words has changed, thus invoking the「fresh render」effect every time. The array is a new instance each time, and this registers as an update that should trigger a rerender. Declaring words outside of the scope of the App would solve the problem:

```js
const words = ["sick", "powder", "day"]; 
function App() {
  useAnyKeyToRender();
  useEffect(() => {
    console.log("fresh render");
  }, [words]);
  return <h1>component</h1>;
}
```

1-3『

这里的信息让自己理解了，之前写数据流文档页面时，先初始化数据再渲染钩子的实现。

```js
  const store = useLocalStore(() => new Store())

  useEffect(() => {
    store.initDocumentData()
  }, [store])

  return (
    <div className={styles.homeContainer}>
      <Tabs defaultActiveKey="0" type="card" onChange={store.getExplainContent}>
        <TabPane tab="流程相关说明" key="0">
          <div dangerouslySetInnerHTML={{__html: store.tab_content }}/>
        </TabPane>
        <TabPane tab="布置相关说明" key="1">
          <div dangerouslySetInnerHTML={{__html: store.tab_content }}/>
        </TabPane>
        <TabPane tab="技巧汇总" key="2">
          <div dangerouslySetInnerHTML={{__html: store.tab_content }}/>
        </TabPane>
        <TabPane tab="版本更新" key="3">
          <div dangerouslySetInnerHTML={{__html: store.tab_content }}/>
        </TabPane>
        <TabPane tab="bug 修复" key="4">
          <div dangerouslySetInnerHTML={{__html: store.tab_content }}/>
        </TabPane>
      </Tabs>
    </div>
  )
})
```

』

The dependency array in this case refers to one instance of words that's declared outside of the function. The「fresh render」effect does not get called again after the first render because words is the same instance as the last render. This is a good solution for this example, but it's not always possible (or advisable) to have a variable defined outside of the scope of the function. Sometimes the value passed to the dependency array requires variables in scope. For example, we might need to create the words array from a React property like children: 

```js
function WordCount({ children = "" }) {
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
```

The App component contains some words that are children of the WordCount component. The WordCount component takes in children as a property. Then we set words in the component equal to an array of those words that we've called `.split` on. We would hope that the component will rerender only if words changes, but as soon as we press a key, we see the dreaded「fresh render」words appearing in the console.

Let's replace that feeling of dread with one of calm, because the React team has provided us a way to avoid these extra renders. They wouldn't hang us out to dry like that. The solution to this problem is, as you might expect, another hook: useMemo.

useMemo invokes a function to calculate a memoized value. In computer science in general, memoization is a technique that's used to improve performance. In a memoized function, the result of a function call is saved and cached. Then, when the function is called again with the same inputs, the cached value is returned. In React, useMemo allows us to compare the cached value against itself to see if it has actually changed.

The way useMemo works is that we pass it a function that's used to calculate and create a memoized value. useMemo will only recalculate that value when one of the dependencies has changed. First, let's import the useMemo hook:

```js
import React, { useEffect, useMemo } from "react"; 
```

Then we'll use the function to set words:

```js
const words = useMemo(() => {
  const words = children.split(" ");
  return words;
}, []);

useEffect(() => {
  console.log("fresh render");
}, [words]);
```

useMemo invokes the function sent to it and sets words to the return value of that function. Like useEffect, useMemo relies on a dependency array:

```js
const words = useMemo(() => children.split(" ")); 
```

When we don't include the dependency array with useMemo, the words are calculated with every render. The dependency array controls when the callback function should be invoked. The second argument sent to the useMemo function is the dependency array and should contain the children value:

```js
function WordCount({ children = "" }) {
  useAnyKeyToRender();
  const words = useMemo(() => children.split(" "), [children]); 
  useEffect(() => {
    console.log("fresh render");
  }, [words]);
  return (...);
}
```

The words array depends on the children property. If children changes, we should calculate a new value for words that reflects that change. At that point, useMemo will calculate a new value for words when the component initially renders and if the children property changes.

The useMemo hook is a great function to understand when you're creating React applications. useCallback can be used like useMemo, but it memoizes functions instead of values. For example:

```js
const fn = () => {
  console.log("hello");
  console.log("world");
};
  
useEffect(() => {
  console.log("fresh render");
  fn();
}, [fn]);
```

fn is a function that logs「Hello」then「World.」It is a dependency of useEffect, but just like words, JavaScript assumes fn is different every render. Therefore, it triggers the effect every render. This yields a「fresh render」for every key press. It's not ideal. Start by wrapping the function with useCallback:

```js
const fn = useCallback(() => {
  console.log("hello");
  console.log("world");
}, []);
  
useEffect(() => {
  console.log("fresh render");
  fn();
}, [fn]);
```

useCallback memoizes the function value for fn. Just like useMemo and useEffect, it also expects a dependency array as the second argument. In this case, we create the memoized callback once because the dependency array is empty.

Now that we have an understanding of the uses and differences between useMemo and useCallback, let's improve our useJazzyNews hook. Every time there's a new post, we'll call newPostChime.play(). In this hook, posts are an array, so we'll need to use useMemo to memoize the value:

```js
const useJazzyNews = () => {
  const [_posts, setPosts] = useState([]);
  const addPost = post => setPosts(allPosts => [post, ...allPosts]); 
  const posts = useMemo(() => _posts, [_posts]);
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
```

Now, the useJazzyNews hook plays a chime every time there's a new post. We made this happen with a few changes to the hook. First, const [posts, setPosts] was renamed to const `[_posts, setPosts]`. We'll calculate a new value for posts every time `_posts` change.

Next, we added the effect that plays the chime every time the post array changes. We're listening to the news feed for new posts. When a new post is added, this hook is reinvoked with `_posts` reflecting that new post. Then, a new value for post is memoized because `_posts` have changed. Then the chime plays because this effect is dependent on posts. It only plays when the posts change, and the list of posts only changes when a new one is added.

Later in the chapter, we'll discuss the React Profiler, a browser extension for testing performance and rendering of React components.

There, we'll dig into more detail about when to use useMemo and useCallback. (Spoiler alert: sparingly!)

#### 7.1.3 When to useLayoutEffect

We understand that the render always comes before useEffect. The render happens first, then all effects run in order with full access to all of the values from the render. A quick look at the React docs will point out that there's another type of effect hook: useLayoutEffect.

useLayoutEffect is called at a specific moment in the render cycle. The series of events is as follows:

1 Render.

2 useLayoutEffect is called.

3 Browser paint: the time when the component's elements are actually added to the DOM.

4 useEffect is called.

This can be observed by adding some simple console messages: 

```js
import React, { useEffect, useLayoutEffect } from "react"; 
function App() {
  useEffect(() => console.log("useEffect")); 
  useLayoutEffect(() => console.log("useLayoutEffect")); 
  return <div>ready</div>;
}
```

In the App component, useEffect is the first hook, followed by useLayoutEffect. We see that useLayoutEffect is invoked before useEffect:

```
useLayoutEffect
useEffect
```

1-2『全完可以用 useLayoutEffect 来改进之前的设计流说明文档的代码，把从服务器获取数据的异步函数放在渲染前。试了下，没有按自己预期的实现，待研究。（2021-05-09）』—— 未完成

useLayoutEffect is invoked after the render but before the browser paints the change. In most circumstances, useEffect is the right tool for the job, but if your effect is essential to the browser paint (the appearance or placement of the UI elements on the screen), you may want to use useLayoutEffect. For instance, you may want to obtain the width and height of an element when the window is resized: 

```js
function useWindowSize {
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
```

The width and height of the window is information that your component may need before the browser paints. useLayoutEffect is used to calculate the window's width and height before the paint. Another example of when to use useLayoutEffect is when tracking the position of the mouse:

```js
function useMousePosition {
  const [x, setX] = useState(0);
  const [y, setY] = useState(0);
  const setPosition = ({ x, y }) => {
    setX(x);
    setY(y);
  };
  
  useLayoutEffect(() => {
    window.addEventListener("mousemove", setPosition); 
    return () => window.removeEventListener("mousemove", setPosition);
  }, []);
  return [x, y];
};
```

It's highly likely that the x and y position of the mouse will be used when painting the screen. useLayoutEffect is available to help calculate those positions accurately before the paint.

#### 7.1.4 Rules to Follow with Hooks

As you're working with Hooks, there are a few guidelines to keep in mind that can help avoid bugs and unusual behavior:

2『钩子的常规法则，做一张主题卡片。（2021-05-09）』—— 已完成

1 Hooks only run in the scope of a component. Hooks should only be called from React components. They can also be added to custom Hooks, which are eventually added to components. Hooks are not regular JavaScript — they're a React pattern, but they're starting to be modeled and incorporated in other libraries.

2 It's a good idea to break functionality out into multiple Hooks. In our earlier example with the Jazzy News component, we split everything related to subscriptions into one effect and everything related to sound effects into another effect. This immediately made the code easier to read, but there was another benefit to doing this.

Since Hooks are invoked in order, it's a good idea to keep them small. Once invoked, React saves the values of Hooks in an array so the values can be tracked. Consider the following component: 

```js
function Counter() {
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
```

The order of Hook calls is the same for each and every render:

```js
[count, checked, DependencyArray, DependencyArray, DependencyArray]
```

3 Hooks should only be called at the top level. Hooks should be used at the top level of a React function. They cannot be placed into conditional statements, loops, or nested functions. Let's adjust the counter:

```js
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
```

When we use useState within the if statement, we're saying that the hook should only be called when the count value is greater than 5. That will throw off the array values. Sometimes the array will be: `[count, checked, DependencyArray, 0, DependencyArray]`. Other times: `[count, DependencyArray, 1]`. The index of the effect in that array matters to React. It's how values are saved.

Wait, so are we saying that we can never use conditional logic in React applications anymore? Of course not! We just have to organize these conditionals differently. We can nest if statements, loops, and other conditionals within the hook:

```js
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
```

Here, the value for checked is based on the condition that the count is greater than 5. When count is less than 5, the value for checked is undefined. Nesting this conditional inside the hook means that the hook remains on the top level, but the result is similar. The second effect enforces the same rules. If the count is less than 5, the return statement will prevent the effect from continuing to execute. This keeps the hook values array intact:

```js
[countValue, checkedValue, DependencyArray, DependencyArray, DependencyArray].
```

Like conditional logic, you need to nest asynchronous behavior inside of a hook. useEffect takes a function as the first argument, not a promise. So you can't use an async function as the first argument: `useEffect(async () => {})`. You can, however, create an async function inside of the nested function like this: 

```js
useEffect(() => {
  const fn = async () => {
    await SomePromise();
  };
  fn();
});
```

We created a variable, fn, to handle the async/await, then we called the function as the return. You can give this function a name, or you can use async effects as an anonymous function:

```js
useEffect(() => {
  (async () => {
    await SomePromise();
  })();
});
```

If you follow these rules, you can avoid some common gotchas with React Hooks. If you're using Create React App, there's an ESLint plug-in included called eslint-plugin-react-hooks that provides warning hints if you're in violation of these rules.

#### 7.1.5 Improving Code with useReducer

Consider the Checkbox component. This component is a perfect example of a component that holds simple state. The box is either checked or not checked. checked is the state value, and setChecked is a function that will be used to change the state. When the component first renders, the value of checked will be false:

```js
function Checkbox() {
  const [checked, setChecked] = useState(false); 
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
}
```

This works well, but one area of this function could be cause for alarm: 

```js
onChange={() => setChecked(checked => !checked)}
```

Look at it closely. It feels OK at first glance, but are we stirring up trouble here? We're sending a function that takes in the current value of checked and returns the opposite, !checked. This is probably more complex than it needs to be. Developers could easily send the wrong information and break the whole thing. Instead of handling it this way, why not provide a function as a toggle?

Let's add a function called toggle that will do the same thing: call setChecked and return the opposite of the current value of checked: 

```js
function Checkbox() {
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
```

This is better. onChange is set to a predictable value: the toggle function. We know what that function is going to do every time, everywhere it's used. We can still take this one step farther to yield even more predictable results each time we use the checkbox component. Remember the function we sent to setChecked in the toggle function?

```js
setChecked(checked => !checked);
```

We're going to refer to this function, checked => !checked, by a different name now: a reducer. A reducer function's most simple definition is that it takes in the current state and returns a new state. If checked is false, it should return the opposite, true. Instead of hardcoding this behavior into onChange events, we can abstract the logic into a reducer function that will always produce the same results.

Instead of useState in the component, we'll use useReducer: 

```js
function Checkbox() {
  const [checked, toggle] = useReducer(checked => !checked, false); 
  return (
    <>
      <input type="checkbox" value={checked} onChange={toggle} />
      {checked ? "checked" : "not checked"}
    </>
  );
}
```

useReducer takes in the reducer function and the initial state, false.

Then, we'll set the onChange function to setChecked, which will call the reducer function.

Our earlier reducer, checked => !checked, is a prime example of this. If the same input is provided to a function, the same output should be expected. This concept originates with Array.reduce in JavaScript.

reduce fundamentally does the same thing as a reducer: it takes in a function (to reduce all of the values into a single value) and an initial value and returns one value.

Array.reduce takes in a reducer function and an initial value. For each value in the numbers array, the reducer is called until one value is returned:

```js
const numbers = [28, 34, 67, 68];
numbers.reduce((number, nextNumber) => number + nextNumber, 0); // 197
```

The reducer sent to Array.reduce takes in two arguments. You can also send multiple arguments to a reducer function:

```js
function Numbers() {
  const [number, setNumber] = useReducer(
    (number, newNumber) => number + newNumber,
    0
  );
  return <h1 onClick={() => setNumber(30)}>{number}</h1>;
}
```

Every time we click on the h1, we'll add 30 to the total.

#### 7.1.6 useReducer to Handle Complex State

useReducer can help us handle state updates more predictably as state becomes more complex. Consider an object that contains user data: 

```js
const firstUser = {
  id: "0391-3233-3201",
  firstName: "Bill",
  lastName: "Wilson",
  city: "Missoula",
  state: "Montana",
  email: "bwilson@mtnwilsons.com",
  admin: false
};
```

Then we have a component called User that sets the firstUser as the initial state, and the component displays the appropriate data: 

```js
function User() {
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
```

A common error when managing state is to overwrite the state:

```js
<button
  onClick={() => {
  setUser({ admin: true });
  }}
>
  Make Admin
</button>
```

Doing this would overwrite state from firstUser and replace it with just what we sent to the setUser function: {admin: true}. This can be fixed by spreading the current values from user, then overwriting the admin value:

```js
<button
  onClick={() => {
    setUser({ ...user, admin: true });
  }}
  >
  Make Admin
</button>
```

This will take the initial state and push in the new key/values: {admin: true}. We need to rewrite this logic in every onClick, making it prone to error (we might forget to do this when we come back to the app tomorrow):

```js
function User() {
  const [user, setUser] = useReducer(
    (user, newDetails) => ({ ...user, ...newDetails }),
    firstUser
  );
  ...
}
```

Then we'll send the new state value, newDetails, to the reducer, and it will be pushed into the object:

```js
<button
  onClick={() => {
    setUser({ admin: true });
  }}
  >
    Make Admin
</button>
```

This pattern is useful when state has multiple subvalues or when the next state depends on a previous state. Teach everyone to spread, they'll spread for a day. Teach everyone to useReducer and they'll spread for life.

LEGACY SETSTATE AND USEREDUCER

In previous versions of React, we used a function called setState to update state. Initial state would be assigned in the constructor as an object:

```js
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
```

The older incarnation of setState merged state values. The same is true of useReducer: 

```js
const [state, setState] = useReducer(
  (state, newState) =>
  ({...state, ...newState}),
  initialState
);
<button onSubmit={() =>
  {setState({admin: true });}}
  Make Admin
</button>
</div>);
```

If you like this pattern, you can use legacy-set-state npm or useReducer.

The past few examples are simple applications for a reducer. In the next chapter, we'll dig deeper into reducer design patterns that can be used to simplify state management in your apps.

#### 7.1.7 Improving Component Performance

In a React application, components are rendered…usually a lot. Improving performance includes preventing unnecessary renders and reducing the time a render takes to propagate. React comes with tools to help us prevent unnecessary renders: memo, useMemo, and useCallback. We looked at useMemo and useCallback earlier in the chapter, but in this section, we'll go into more detail about how to use these Hooks to make your websites perform better.

The memo function is used to create pure components. As discussed in Chapter 3, we know that, given the same parameters, a pure function will always return the same result. A pure component works the same way. In React, a pure component is a component that always renders the same output, given the same properties. Let's create a component called Cat:

```js
const Cat = ({ name }) => {
  console.log(`rendering ${name}`);
  return <p>{name}</p>;
};
```

Cat is a pure component. The output is always a paragraph that displays the name property. If the name provided as a property is the same, the output will be the same:

```js
function App() {
  const [cats, setCats] = useState(["Biscuit", "Jungle", "Outlaw"]); 
  return (
    <>
      {cats.map((name, i) => (
        <Cat key={i} name={name} />
      ))}
      <button onClick={() => setCats([...cats, prompt("Name a cat")])}> 
        Add a Cat
      </button>
    </>
  );
}
```

This app uses the Cat component. After the initial render, the console reads:

```
rendering Biscuit
rendering Jungle
rendering Outlaw
```

When the「Add a Cat」button is clicked, the user is prompted to add a cat. If we add a cat named「Ripple,」we see that all Cat components are rerendered:

```
rendering Biscuit
rendering Jungle
rendering Outlaw
rendering Ripple
```

WARNING: This code works because prompt is blocking. This is just an example. Don't use prompt in a real app.

Every time we add a cat, every Cat component is rendered, but the Cat component is a pure component. Nothing changes about the output given the same prop, so there shouldn't be a render for each of these.

We don't want to rerender a pure component if the properties haven't changed. The memo function can be used to create a component that will only render when its properties change. Start by importing it from the React library and use it to wrap the current Cat component: 

```js
import React, { useState, memo } from "react"; 

const Cat = ({ name }) => {
  console.log(`rendering ${name}`);
  return <p>{name}</p>;
};
  
const PureCat = memo(Cat);
```

Here, we've created a new component called PureCat. PureCat will only cause the Cat to render when the properties change. Then we can replace the Cat component with PureCat in the App component:

```js
cats.map((name, i) => <PureCat key={i} name={name} />); 
```

Now, every time we add a new cat name, like「Pancake,」we see only one render in the console:

```
rendering Pancake
```

Because the names of the other cats have not changed, we don't render those Cat components. This is working well for a name property, but what if we introduce a function property to the Cat component?

```js
const Cat = memo(({ name, meow = f => f }) => {
  console.log(`rendering ${name}`);
  return <p onClick={() => meow(name)}>{name}</p>;
});
```

Every time a cat is clicked on, we can use this property to log a meow to the console:

```js
<PureCat key={i} name={name} meow={name => console.log(`${name} has meowed`)} />
```

When we add this change, PureCat no longer works as expected. It's always rendering every Cat component even though the name property remains the same. This is because of the added meow property. Unfortunately, every time we define the meow property as a function, it's always new function. To React, the meow property has changed, and the component is rerendered.

The memo function will allow us to define more specific rules around when this component should rerender:

```js
const RenderCatOnce = memo(Cat, () => true); 
const AlwaysRenderCat = memo(Cat, () => false); 
```

The second argument sent to the memo function is a predicate. A predicate is a function that only returns true or false. This function decides whether to rerender a cat or not. When it returns false, the Cat is rerendered. When this function returns true, the Cat will not be rerendered. No matter what, the Cat is always rendered at least once. This is why, with RenderCatOnce, it will render once and then never again. Typically, this function is used to check actual values: 

```js
const PureCat = memo(
  Cat,
  (prevProps, nextProps) => prevProps.name === nextProps.name
);
```

We can use the second argument to compare properties and decide if Cat should be rerendered. The predicate receives the previous properties and the next properties. These objects are used to compare the name property. If the name changes, the component will be rerendered. If the name is the same, it will be rerendered regardless of what React thinks about the meow property.

#### 7.1.8 shouldComponentUpdate and PureComponent

The concepts we're discussing are not new to React. The memo function is a new solution to a common problem. In previous versions of React, there was a method called shouldComponentUpdate. If present in the component, it was used to let React know under which circumstances the component should update. shouldComponentUpdate described which props or state would need to change for the component to

rerender. Once shouldComponentUpdate was part of the React library, it was embraced as a useful feature by many. So useful that the React team decided to create an alternate way of creating a component as a class. A class component would look like this:

```js
class Cat extends React.Component {
  render() {
    return (
      {name} is a good cat!
    )
  }
}
```

A PureComponent would look like this:

```js
class Cat extends React.PureComponent {
  render() {
    return (
      {name} is a good cat!
    )
  }
}
```

PureComponent is the same as React.memo, but PureComponent is only for class components; React.memo is only for function components.

useCallback and useMemo can be used to memoize object and function properties. Let's use useCallback in the Cat component: 

```js
const PureCat = memo(Cat);

function App() {
  const meow = useCallback(name => console.log(`${name} has meowed`, []); 
  return <PureCat name="Biscuit" meow={meow} />
}
```

In this case, we did not provide a property-checking predicate to memo(Cat). Instead, we used useCallback to ensure that the meow function had not changed. Using these functions can be helpful when dealing with too many rerenders in your component tree.

#### 7.1.9 When to Refactor

The last Hooks we discussed, useMemo and useCallback, along with the memo function, are commonly overused. React is designed to be fast. It's designed to have components render a lot. The process of optimizing for performance began when you decided to use React in the first place. It's fast. Any further refactoring should be a last step.

There are trade-offs to refactoring. Using useCallback and useMemo everywhere because it seems like a good idea might actually make your app less performant. You're adding more lines of code and developer hours to your application. When you refactor for performance, it's important to have a goal. Perhaps you want to stop the screen from freezing or flickering. Maybe you know there are some costly functions that are slowing the speed of your app unreasonably.

The React Profiler can be used to measure the performance of each of your components. The profiler ships with the React Developer Tools that you've likely installed already (available for Chrome and Firefox).

Always make sure your app works and you're satisfied with the codebase before refactoring. Over-refactoring, or refactoring before your app works, can introduce weird bugs that are hard to spot, and it might not be worth your time and focus to introduce these optimizations.

In the last two chapters, we've introduced many of the Hooks that ship with React. You've seen use cases for each hook, and you've created your own custom Hooks by composing other Hooks. Next, we'll build on these foundational skills by incorporating additional libraries and advanced patterns.