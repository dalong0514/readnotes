## 记忆时间

## 目录

0401How React Works

0501React with JSX

## 0401. How React Works

So far on your journey, you've brushed up on the latest syntax. You've reviewed the functional programming patterns that guided React's creation. These steps have prepared you to take the next step, to do what you came here to do: to learn how React works. Let's get into writing some real React code.

When you work with React, it's more than likely that you'll be creating your apps with JSX. JSX is a tag-based JavaScript syntax that looks a lot like HTML. It's a syntax we'll dive deep into in the next chapter and continue to use for the rest of the book. To truly understand React, though, we need to understand its most atomic units: React elements.

From there, we'll get into React elements. From there, we'll get into React components by looking at how we can create custom components that compose other components and elements.

### 4.1 Page Setup

In order to work with React in the browser, we need to include two libraries: React and ReactDOM. React is the library for creating views. ReactDOM is the library used to actually render the UI in the browser.

Both libraries are available as scripts from the unpkg CDN (links are included in the following code). Let's set up an HTML document:

These are the minimum requirements for working with React in the browser. You can place your JavaScript in a separate file, but it must be loaded somewhere in the page after React has been loaded. We're going to be using the development version of React to see all of the error messages and warnings in the browser console. You can choose to use the minified production version using react.production.min.js and react-dom.production.min.js, which will strip away those warnings.

### 4.2 React Elements

HTML is simply a set of instructions that a browser follows when constructing the DOM. The elements that make up an HTML document become DOM elements when the browser loads HTML and renders the user interface. Let's say you have to construct an HTML hierarchy for a recipe. A possible solution for such a task might look something like this:

In HTML, elements relate to one another in a hierarchy that resembles a family tree. We could say that the root element (in this case, a section) has three children: a heading, an unordered list of ingredients, and a section for the instructions.

In the past, websites consisted of independent HTML pages. When the user navigated these pages, the browser would request and load different HTML documents. The invention of AJAX (Asynchronous JavaScript and XML) brought us the single-page application, or SPA. Since browsers could request and load tiny bits of data using AJAX, entire web applications could now run out of a single page and rely on JavaScript to update the user interface.

In an SPA, the browser initially loads one HTML document. As users navigate through the site, they actually stay on the same page. JavaScript destroys and creates a new user interface as the user interacts with the application. It may feel as though you're jumping from page to page, but you're actually still on the same HTML page, and JavaScript is doing the heavy lifting.

2『 SPA 做一张术语卡片。（2021-05-02）』—— 已完成

The DOM API is a collection of objects that JavaScript can use to interact with the browser to modify the DOM. If you've used document.createElement or document.appendChild, you've worked with the DOM API.

React is a library that's designed to update the browser DOM for us. We no longer have to be concerned with the complexities associated with building high-performing SPAs because React can do that for us. With React, we do not interact with the DOM API directly. Instead, we provide instructions for what we want React to build, and React will take care of rendering and reconciling the elements we've instructed it to create.

2『 DOM API（React DOM）是一个 JS 库，这个库帮我们跟浏览器的 DOM 打交道。React DOM 和 React elements 做一张术语卡片。（2021-05-02）』—— 已完成

The browser DOM is made up of DOM elements. Similarly, the React DOM is made up of React elements. DOM elements and React elements may look the same, but they're actually quite different. A React element is a description of what the actual DOM element should look like. In other words, React elements are the instructions for how the browser DOM should be created.

We can create a React element to represent an h1 using React.createElement:

```js
React.createElement("h1", { id: "recipe-0" }, "Baked Salmon"); 
```

The first argument defines the type of element we want to create. In this case, we want to create an h1 element. The second argument represents the element's properties. This h1 currently has an id of recipe-0. The third argument represents the element's children: any nodes that are inserted between the opening and closing tag (in this case, just some text).

During rendering, React will convert this element to an actual DOM element:

```html
<h1 id="recipe-0" > Baked Salmon</h1> 
```

The properties are similarly applied to the new DOM element: the properties are added to the tag as attributes, and the child text is added as text within the element. A React element is just a JavaScript literal that tells React how to construct the DOM element. If you were to log this element, it would look like this:

```json
{
  $$typeof: Symbol(React.element),
  "type": "h1",
  "key": null,
  "ref": null,
  "props": {id: "recipe-0", children: "Baked Salmon"},
  "_owner": null,
  "_store": {}
}
```

This is the structure of a React element. There are fields that are used by React: `_owner`, `_store`, and `$$typeof`. The key and ref fields are important to React elements, but we'll introduce those later. For now, let's take a closer look at the type and props fields.

The type property of the React element tells React what type of HTML or SVG element to create. The props property represents the data and child elements required to construct a DOM element. The children property is for displaying other nested elements as text.

CREATING ELEMENTS

We're taking a peek at the object that React.createElement returns. You won't actually create these elements by hand; instead, you'll use the React.createElement function.

### 4.3 ReactDOM

Once we've created a React element, we'll want to see it in the browser. ReactDOM contains the tools necessary to render React elements in the browser. ReactDOM is where we'll find the render method.

We can render a React element, including its children, to the DOM with ReactDOM.render. The element we want to render is passed as the first argument, and the second argument is the target node, where we should render the element:

```js
const dish = React.createElement("h1", null, "Baked Salmon"); 
ReactDOM.render(dish, document.getElementById("root"));
```

Rendering the title element to the DOM would add an h1 element to the div with the id of root, which we would already have defined in our HTML. We build this div inside the body tag:

```html
<body>
  <div id="root" >
    <h1> Baked Salmon</h1>
  </div>
</body>
```

Anything related to rendering elements to the DOM is found in the ReactDOM package. In versions of React earlier than React 16, you could only render one element to the DOM. Today, it's possible to render arrays as well. When the ability to do this was announced at ReactConf 2017, everyone clapped and screamed. It was a big deal.

This is what that looks like:

```js
const dish = React.createElement("h1", null, "Baked Salmon");
const dessert = React.createElement("h2", null, "Coconut Cream Pie"); 
ReactDOM.render([dish, dessert], document.getElementById("root")); 
```

This will render both of these elements as siblings inside of the root container. We hope you just clapped and screamed! In the next section, we'll get an understanding of how to use props.children.

2『如何同时渲染多个 React Elements，做一张任意卡片。（2021-05-02）』

#### 4.3.1 Children

React renders child elements using props.children. In the previous section, we rendered a text element as a child of the h1 element, and thus props.children was set to Baked Salmon. We could render other React elements as children, too, creating a tree of elements. This is why we use the term element tree: the tree has one root element from which many branches grow. Let's consider the unordered list that contains ingredients:

```html
<ul>
  <li> 2 lb salmon</li>
  <li> 5 sprigs fresh rosemary</li>
  <li> 2 tablespoons olive oil</li>
  <li> 2 small lemons</li>
  <li> 1 teaspoon kosher salt</li>
  <li> 4 cloves of chopped garlic</li>
</ul>
```

In this sample, the unordered list is the root element, and it has six children. We can represent this ul and its children with React.createElement:

```js
React.createElement( 
  "ul", 
  null, 
  React.createElement("li", null, "2 lb salmon"), 
  React.createElement("li", null, "5 sprigs fresh rosemary"), 
  React.createElement("li", null, "2 tablespoons olive oil"), 
  React.createElement("li", null, "2 small lemons"), 
  React.createElement("li", null, "1 teaspoon kosher salt"), 
  React.createElement("li", null, "4 cloves of chopped garlic") 
);
```

Every additional argument sent to the createElement function is another child element. React creates an array of these child elements and sets the value of props.children to that array. If we were to inspect the resulting React element, we would see each list item represented by a React element and added to an array called props.children. If you console log this element:

```js
const list = React.createElement( 
  "ul", 
  null, 
  React.createElement("li", null, "2 lb salmon"), 
  React.createElement("li", null, "5 sprigs fresh rosemary"), 
  React.createElement("li", null, "2 tablespoons olive oil"), 
  React.createElement("li", null, "2 small lemons"), 
  React.createElement("li", null, "1 teaspoon kosher salt"), 
  React.createElement("li", null, "4 cloves of chopped garlic") 
)
console.log(list)
```

The result will look like this:

```json
{
  "type": "ul",
  "props": {
    "children": [
      { "type": "li", "props": { "children": "2 lb salmon" } … },
      { "type": "li", "props": { "children": "5 sprigs fresh rosemary"} …},
      { "type": "li", "props": { "children": "2 tablespoons olive oil" } …},
      { "type": "li", "props": { "children": "2 small lemons"} … },
      { "type": "li", "props": { "children": "1 teaspoon kosher salt"} … },
      { "type": "li", "props": { "children": "4 cloves of chopped garlic"}… }
    ]
    ...
  }
}
```

We can now see that each list item is a child. Earlier in this chapter, we introduced HTML for an entire recipe rooted in a section element. To create this using React, we'll use a series of createElement calls: 

```js
React.createElement( 
  "section", 
  { id: "baked-salmon" }, 
  React.createElement("h1", null, "Baked Salmon"), 
  React.createElement( 
    "ul", 
    { className: "ingredients" }, 
    React.createElement("li", null, "2 lb salmon"), 
    React.createElement("li", null, "5 sprigs fresh rosemary"), 
    React.createElement("li", null, "2 tablespoons olive oil"), 
    React.createElement("li", null, "2 small lemons"), 
    React.createElement("li", null, "1 teaspoon kosher salt"), 
    React.createElement("li", null, "4 cloves of chopped garlic") 
  ), 
  React.createElement( 
    "section", { className: "instructions" }, 
    React.createElement("h2", null, "Cooking Instructions"), 
    React.createElement("p", null, "Preheat the oven to 375 degrees."), 
    React.createElement("p", null, "Lightly coat aluminum foil with oil."), 
    React.createElement("p", null, "Place salmon on foil."), 
    React.createElement( "p", null, "Cover with rosemary, sliced lemons, chopped garlic."), 
    React.createElement( "p", null, "Bake for 15-20 minutes until cooked through."), 
    React.createElement("p", null, "Remove from oven.")
  ) 
);
```

CLASSNAME IN REACT

Any element that has an HTML class attribute is using className for that property instead of class. Since class is a reserved word in JavaScript, we have to use className to define the class attribute of an HTML element. This sample is what pure React looks like. Pure React is ultimately what runs in the browser. A React app is a tree of React elements all stemming from a single root element. React elements are the instructions React will use to build a UI in the browser.

CONSTRUCTING ELEMENTS WITH DATA

The major advantage of using React is its ability to separate data from UI elements. Since React is just JavaScript, we can add JavaScript logic to help us build the React component tree. For example, ingredients can be stored in an array, and we can map that array to the React elements.

Let's go back and think about the unordered list for a moment: 

```js
React.createElement( 
  "ul", 
  null, 
  React.createElement("li", null, "2 lb salmon"), 
  React.createElement("li", null, "5 sprigs fresh rosemary"), 
  React.createElement("li", null, "2 tablespoons olive oil"), 
  React.createElement("li", null, "2 small lemons"), 
  React.createElement("li", null, "1 teaspoon kosher salt"), 
  React.createElement("li", null, "4 cloves of chopped garlic") 
);
```

The data used in this list of ingredients can easily be represented using a JavaScript array:

```js
const items = [ 
  "2 lb salmon", 
  "5 sprigs fresh rosemary", 
  "2 tablespoons olive oil", 
  "2 small lemons", 
  "1 teaspoon kosher salt", 
  "4 cloves of chopped garlic" 
];
```

We want to use this data to generate the correct number of list items without having to hard-code each one. We can map over the array and create list items for as many ingredients as there are:

```js
React.createElement( 
  "ul", { className: "ingredients" }, 
  items.map(ingredient => React.createElement("li", null, ingredient)) 
);
```

1-2『首次看到使用 map 函数生成 React Elements 数组，对我意义重大。做一张主题卡片。（2021-05-02）』—— 已完成

This syntax creates a React element for each ingredient in the array. Each string is displayed in the list item's children as text. The value for each ingredient is displayed as the list item. When running this code, you'll see a console warning like the one shown in Figure 4-1.

Figure 4-1. Console warning

When we build a list of child elements by iterating through an array, React likes each of those elements to have a key property. The key property is used by React to help it update the DOM efficiently. You can make this warning go away by adding a unique key property to each of the list item elements. You can use the array index for each ingredient as that unique value:

```js
React.createElement( 
  "ul", 
  { className: "ingredients" }, 
  items.map((ingredient, i) => 
    React.createElement("li", { key: i }, ingredient) ) 
);
```

We'll cover keys in more detail when we discuss JSX, but adding this to each list item will clear the console warning.

### 4.4 React Components

No matter its size, its contents, or what technologies are used to create it, a user interface is made up of parts. Buttons. Lists. Headings. All of these parts, when put together, make up a user interface. Consider a recipe application with three different recipes. The data is different in each box, but the parts needed to create a recipe are the same (see Figure 4-2).

Figure 4-2. Recipes app

In React, we describe each of these parts as a component. Components allow us to reuse the same structure, and then we can populate those structures with different sets of data.

When considering a user interface you want to build with React, look for opportunities to break down your elements into reusable pieces. For example, the recipes in Figure 4-3 have a title, ingredients list, and instructions. All are part of a larger recipe or app component. We could create a component for each of the highlighted parts: ingredients, instructions, and so on.

Figure 4-3. Each component is outlined: App, IngredientsList, Instructions 

Think about how scalable this is. If we want to display one recipe, our component structure will support this. If we want to display 10,000 recipes, we'll just create 10,000 new instances of that component.

We'll create a component by writing a function. That function will return a reusable part of a user interface. Let's create a function that returns an unordered list of ingredients. This time, we'll make dessert with a function called IngredientsList:

```js
function IngredientsList() {
  return React.createElement( 
    "ul", 
    { className: "ingredients" }, 
    React.createElement("li", null, "1 cup unsalted butter"), 
    React.createElement("li", null, "1 cup crunchy peanut butter"), 
    React.createElement("li", null, "1 cup brown sugar"), 
    React.createElement("li", null, "1 cup white sugar"), 
    React.createElement("li", null, "2 eggs"), 
    React.createElement("li", null, "2.5 cups all purpose flour"), 
    React.createElement("li", null, "1 teaspoon baking powder"), 
    React.createElement("li", null, "0.5 teaspoon salt") 
  );
}

ReactDOM.render( 
  React.createElement(IngredientsList, null, null), 
  document.getElementById("root") 
);
```

The component's name is IngredientsList, and the function outputs elements that look like this:

```js
<IngredientsList>
  <ul className="ingredients">
    <li>1 cup unsalted butter</li> 
    <li>1 cup crunchy peanut butter</li> 
    <li>1 cup brown sugar</li> 
    <li>1 cup white sugar</li> 
    <li>2 eggs</li> 
    <li>2.5 cups all purpose flour</li> 
    <li>1 teaspoon baking powder</li> 
    <li>0.5 teaspoon salt</li> 
  </ul> 
</IngredientsList>
```

This is pretty cool, but we've hardcoded this data into the component. What if we could build one component and then pass data into that component as properties? And then what if that component could render the data dynamically? Maybe someday that will happen!

2『下面有关创建 React Elements 时直接传递「数据」作为组件的属性，做一张主题卡片。（2021-05-02）』—— 已完成

Just kidding — that day is now. Here's an array of secretIngredients needed to put together a recipe:

```js
const secretIngredients = [
  "1 cup unsalted butter", 
  "1 cup crunchy peanut butter", 
  "1 cup brown sugar", 
  "1 cup white sugar", 
  "2 eggs", 
  "2.5 cups all purpose flour", 
  "1 teaspoon baking powder", 
  "0.5 teaspoon salt" 
];
```

Then we'll adjust the IngredientsList component to map over these items, constructing an li for however many items are in the items array:

```js
function IngredientsList() {
  return React.createElement( 
    "ul", 
    { className: "ingredients" }, 
    items.map((ingredient, i) => 
      React.createElement("li", { key: i }, ingredient) 
    ) 
  );
}
```

Then we'll pass those secretIngredients as a property called items, which is the second argument used in createElement:

```js
ReactDOM.render( 
  React.createElement(IngredientsList, { items: secretIngredients }, null),
  document.getElementById("root") 
);
```

Now, let's look at the DOM. The data property items is an array with eight ingredients. Because we made the li tags using a loop, we were able to add a unique key using the index of the loop:

```js
<IngredientsList items="[...]">
  <ul className="ingredients">
    <li key="0">1 cup unsalted butter</li> 
    <li key="1">1 cup crunchy peanut butter</li>
    <li key="2">1 cup brown sugar</li>
    <li key="3">1 cup white sugar</li>
    <li key="4">2 eggs</li>
    <li key="5">2.5 cups all purpose flour</li>
    <li key="6">1 teaspoon baking powder</li>
    <li key="7">0.5 teaspoon salt</li>
  </ul> 
</IngredientsList>
```

Creating our component this way will make the component more flexible. Whether the items array is one item or a hundred items long, the component will render each as a list item.

Another adjustment we can make here is to reference the items array from React props. Instead of mapping over the global items, we'll make items available on the props object. Start by passing props to the function, then mapping over props.items:

```js
function IngredientsList(props) {
  return React.createElement( 
    "ul", 
    { className: "ingredients" }, 
    props.items.map((ingredient, i) => 
      React.createElement("li", { key: i }, ingredient) 
    ) 
  );
}
```

We could also clean up the code a bit by destructuring items from props:

```js
function IngredientsList({ items }) { 
  return React.createElement( 
    "ul", 
    { className: "ingredients" }, 
    items.map((ingredient, i) => 
      React.createElement("li", { key: i }, ingredient) 
    ) 
  );
}
```

Everything that's associated with the UI for IngredientsList is encapsulated into one component. Everything we need is right there.

#### 4.4.1 React Components: A Historical Tour

Before there were function components, there were other ways to create components. While we won't spend a great deal of time on these approaches, it's important to understand the history of React components, particularly when dealing with these APIs in legacy codebases. Let's take a little historical tour of React APIs of times gone by.

TOUR STOP 1: CREATECLASS

When React was first made open source in 2013, there was one way to create a component: createClass. The use of React.createClass to create a component looks like this:

```js
const IngredientsList = React.createClass({
  displayName: "IngredientsList", 
  render() { 
    return React.createElement( 
      "ul", 
      { className: "ingredients" }, 
      this.props.items.map((ingredient, i) => 
        React.createElement("li", { key: i }, ingredient) 
      ) 
    ); 
  } 
});
```

Components that used createClass would have a render() method that described the React element(s) that should be returned and rendered. The idea of the component was the same: we'd describe a reusable bit of UI to render.

In React 15.5 (April 2017), React started throwing warnings if createClass was used. In React 16 (September 2017), React.createClass was officially deprecated and was moved to its own package, create-react-class.

TOUR STOP 2: CLASS COMPONENTS

When class syntax was added to JavaScript with ES 2015, React introduced a new method for creating React components. The React.Component API allowed you to use class syntax to create a new component instance:

```js
class IngredientsList extends React.Component {
  render() { 
    return React.createElement( 
      "ul", 
      { className: "ingredients" }, 
      this.props.items.map((ingredient, i) => 
        React.createElement("li", { key: i }, ingredient) 
      ) 
    );
  }
}
```

It's still possible to create a React component using class syntax, but be forewarned that React.Component is on the path to deprecation as well. Although it's still supported, you can expect this to go the way of React.createClass, another old friend who shaped you but who you won't see as often because they moved away and you moved on. From now on, we'll use functions to create components in this book and only briefly point out older patterns for reference.

## 0501. React with JSX

In the last chapter, we dove deep into how React works, breaking down our React applications into small reusable pieces called components. These components render trees of elements and other components.

Using the createElement function is a good way to see how React works, but as React developers, that's not what we do. We don't go around composing complex, barely readable trees of JavaScript syntax and call it fun. In order to work efficiently with React, we need one more thing: JSX.

JSX combines the JS from JavaScript and the X from XML. It is a JavaScript extension that allows us to define React elements using a tag-based syntax directly within our JavaScript code. Sometimes JSX is confused with HTML because they look similar. JSX is just another way of creating React elements, so you don't have to pull your hair out looking for the missing comma in a complex createElement call.

2『 JSX 做一张术语卡片。（2021-05-03）』

In this chapter, we're going to discuss how to use JSX to construct a React application.

### 5.1 React Elements as JSX

Facebook's React team released JSX when they released React to provide a concise syntax for creating complex DOM trees with attributes. They also hoped to make React more readable like HTML and XML. In JSX, an element's type is specified with a tag. The tag's attributes represent the properties. The element's children can be added between the opening and closing tags.

You can also add other JSX elements as children. If you have an unordered list, you can add child list item elements to it with JSX tags.

It looks very similar to HTML:

```html
<ul>
  <li> 1 lb Salmon</li>
  <li> 1 cup Pine Nuts</li>
  <li> 2 cups Butter Lettuce</li>
  <li> 1 Yellow Squash</li>
  <li> 1/2 cup Olive Oil</li>
  <li> 3 Cloves of Garlic</li>
</ul>
```

JSX works with components as well. Simply define the component using the class name. We pass an array of ingredients to the IngredientsList as a property with JSX, as shown in Figure 5-1.

Figure 5-1. Creating the IngredientsList with JSX

When we pass the array of ingredients to this component, we need to surround it with curly braces. This is called a JavaScript expression, and we must use these when passing JavaScript values to components as properties. Component properties will take two types: either a string or a JavaScript expression. JavaScript expressions can include arrays, objects, and even functions. In order to include them, you must surround them in curly braces.

#### 5.1.1 JSX Tips

JSX might look familiar, and most of the rules result in syntax that's similar to HTML. However, there are a few considerations you should understand when working with JSX.

1 NESTED COMPONENTS

JSX allows you to add components as children of other components. For example, inside the IngredientsList, we can render another component called Ingredient multiple times:

```html
<IngredientsList>
  <Ingredient />
  <Ingredient />
  <Ingredient />
</IngredientsList>
```

2 CLASSNAME

Since class is a reserved word in JavaScript, className is used to define the class attribute instead:

```html
<h1 className="fancy" > Baked Salmon</h1> 
```

3 JAVASCRIPT EXPRESSIONS

JavaScript expressions are wrapped in curly braces and indicate where variables will be evaluated and their resulting values returned. For example, if we want to display the value of the title property in an element, we can insert that value using a JavaScript expression. The variable will be evaluated and its value returned:

```html
<h1>{title}</h1>
```

Values of types other than string should also appear as JavaScript expressions:

```html
<input type="checkbox" defaultChecked={false} /> EVALUATION
```

The JavaScript that's added in between the curly braces will get evaluated. This means that operations such as concatenation or addition will occur. This also means that functions found in JavaScript expressions will be invoked:

```html
<h1> {"Hello" + title}</h1>
<h1> {title.toLowerCase().replace}</h1> 
```

#### 5.1.2 Mapping Arrays with JSX

JSX is JavaScript, so you can incorporate JSX directly inside of JavaScript functions. For example, you can map an array to JSX elements:

```html
<ul>
  {props.ingredients.map((ingredient, i) => (
    <li key="{i}">{ingredient}</li>
  ))}
</ul>
```

JSX looks clean and readable, but it can't be interpreted with a browser. All JSX must be converted into createElement calls. Luckily, there's an excellent tool for this task: Babel.

### 5.2 Babel

Many software languages require you to compile your source code. JavaScript is an interpreted language: the browser interprets the code as text, so there's no need to compile JavaScript. However, not all browsers support the latest JavaScript syntax, and no browser supports JSX syntax. Since we want to use the latest features of JavaScript along with JSX, we're going to need a way to convert our fancy source code into something that the browser can interpret. This process is called compiling, and it's what Babel is designed to do.

1-2『本书作者给了自己很多醍醐灌顶的知识点，看到上面的信息才算弄明白 Babel 干啥的。虽然 JS 是解释性语言，但不是所有的浏览器都支持 JS 的最新相关语法（ES6、JSX 等），所需需要 Babel 来「翻译」。Babel 做一张术语卡片。（2021-05-03）』—— 已完成

The first version of the project was called 6to5, and it was released in September 2014. 6to5 was a tool that could be used to convert ES6 syntax to ES5 syntax, which was more widely supported by web browsers. As the project grew, it aimed to be a platform to support all of the latest changes in ECMAScript. It also grew to support converting JSX into JavaScript. The project was renamed Babel in February 2015.

Babel is used in production at Facebook, Netflix, PayPal, Airbnb, and more. Previously, Facebook had created a JSX transformer that was their standard, but it was soon retired in favor of Babel.

There are many ways of working with Babel. The easiest way to get started is to include a link to the Babel CDN directly in your HTML, which will compile any code in script blocks that have a type of 'text/babel'. Babel will compile the source code on the client before running it. Although this may not be the best solution for production, it's a great way to get started with JSX:

```html
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
```

CONSOLE WARNING IN THE BROWSER WITH IN-BROWSER BABEL

When using the in-browser transformer, you'll see a warning that says to precompile scripts for production. Don't worry about that warning for the purposes of this and any other small demos. We'll upgrade to production-ready Babel later in the chapter.

### 5.3 Recipes as JSX

JSX provides us with a nice, clean way to express React elements in our code that makes sense to us and is immediately readable by developers. The drawback of JSX is that it's not readable by the browser. Before our code can be interpreted by the browser, it needs to be converted from JSX into JavaScript.

This data array contains two recipes, and this represents our application's current state:

```js
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
```

The data is expressed in an array of two JavaScript objects. Each object contains the name of the recipe, a list of the ingredients required, and a list of steps necessary to cook the recipe.

We can create a UI for these recipes with two components: a Menu component for listing the recipes and a Recipe component that describes the UI for each recipe. It's the Menu component that we'll render to the DOM. We'll pass our data to the Menu component as a property called recipes:

```js
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
  <Menu recipes={data} title="Delicious Recipes" />, 
  document.getElementById("root")
);
```

1『这里有个注意点。传递给下游组件的 props 里包含 2 个属性，一个是 recipes，其值是那个 json 数组，一个是 title，其值是个字符串。可以把 props 当作一个对象，所有后面的改进版，props 数据传递过去后可以用解构对象的语法 `{ recipes, title }` 来解构数据。感觉一下子弄清楚不少东西。（2021-05-03）』

The React elements within the Menu component are expressed as JSX. Everything is contained within an article element. A header element, an h1 element, and a div.recipes element are used to describe the DOM for our menu. The value for the title property will be displayed as text within the h1:

```js
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
```

Inside of the div.recipes element, we add a component for each recipe:

```js
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
```

In order to list the recipes within the div.recipes element, we use curly braces to add a JavaScript expression that will return an array of children. We can use the map function on the props.recipes array to return a component for each object within the array. As mentioned previously, each recipe contains a name, some ingredients, and cooking instructions (steps). We'll need to pass this data to each Recipe as props. Also remember that we should use the key property to uniquely identify each element.

You could also refactor this to use spread syntax. The JSX spread operator works like the object spread operator. It will add each field of the recipe object as a property of the Recipe component. The syntax here will supply all properties to the component:

```js
{
  props.recipes.map((recipe, i) => <Recipe key={i} {...recipe} />);
}
```

Remember that this shortcut will provide all the properties to the Recipe component. This could be a good thing but might also add too many properties to the component.

Another place we can make a syntax improvement to our Menu component is where we take in the props argument. We can use object destructuring to scope the variables to this function. This allows us to access the title and recipes variables directly, no longer having to prefix them with props:

```js
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
```

Now let's code the component for each individual recipe:

```js
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
```

Each recipe has a string for the name, an array of objects for ingredients, and an array of strings for the steps. Using object destructuring, we can tell this component to locally scope those fields by name so we can access them directly without having to use props.name, props.ingredients, or props.steps.

The first JavaScript expression we see is being used to set the id attribute for the root section element. It's converting the recipe's name to a lowercase string and globally replacing spaces with dashes.

The result is that "Baked Salmon" will be converted to "baked-salmon" (and likewise, if we had a recipe with the name "Boston Baked Beans", it would be converted to "boston-baked-beans") before it's used as the id attribute in our UI. The value for name is also being displayed in an h1 as a text node.

Inside of the unordered list, a JavaScript expression is mapping each ingredient to an li element that displays the name of the ingredient. Within our instructions section, we see the same pattern being used to return a paragraph element where each step is displayed. These map functions are returning arrays of child elements. The complete code for the application should look like this: 

```js
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
  <Menu recipes={data} title="Delicious Recipes" />, 
  document.getElementById("root")
);
  
```

When we run this code in the browser, React will construct a UI using our instructions with the recipe data as shown in Figure 5-2.

2『

太爽了，上面的代码在自己新建的 React 项目（learn-react）里跑通了。

最开始自己测试用的项目代码：

```js
class Game extends React.Component {
  testFun() {
    // console.log('dalong')
    codeFun()
  }

  render() {
    return (
      <div>
        <Button type="primary" onClick={this.testFun}>测试按钮</Button>
      </div>
    )
  }
}

ReactDOM.render(
  <Game />,
  document.getElementById('root')
)
```

融合后的代码：

```js
/* eslint-disable react/prop-types */
import React from 'react'
import ReactDOM from 'react-dom'
import './index.css'
import { Button } from 'antd'
import { codeFun } from './testCode'

const data = [
  {
    name: "Baked Salmon",
    ingredients: [
      { name: "Salmon", amount: 1, measurement: "l lb" },
      { name: "Pine Nuts", amount: 1, measurement: "cup" },
      { name: "Butter Lettuce", amount: 2, measurement: "cups" },
    ],
    steps: [
      "Preheat the oven to 350 degrees.",
      "Spread the olive oil around a glass baking dish.",
    ]
  },
  
  {
    name: "Fish Tacos",
    ingredients: [
      { name: "Whitefish", amount: 1, measurement: "l lb" },
      { name: "Cheese", amount: 1, measurement: "cup" },
    ],
    steps: [
      "Cook the fish on the grill until cooked through.",
      "Place the fish on the 3 tortillas.",
    ]
  }
]

// A function component for an individual Recipe
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
  )
}

function Menu({ recipes, title}) {
  const testFun = () => {
    // console.log('dalong')
    codeFun()
  }
  
  return (
    <>
      <Button type="primary" onClick={testFun}>测试按钮</Button>
      <article>
        <header>
          <h1>{title}</h1>
        </header>
        <div className="recipes">
          {recipes.map((recipe, i) => (
            <Recipe key={i} {...recipe}/>
          ))}
        </div>
      </article>
    </>
  )
}

ReactDOM.render(
  <Menu recipes={data} title="Delicious Recipes" />, 
  document.getElementById("root")
)
```

』

If you're using Google Chrome and have the React Developer Tools Extension installed, you can take a look at the present state of the component tree. To do this, open the developer tools and select the Components tab, as shown in Figure 5-3.

Here we can see the Menu and its child elements. The data array contains two objects for recipes, and we have two Recipe elements. Each Recipe element has properties for the recipe name, ingredients, and steps. The ingredients and steps are passed down to their own components as data.

The components are constructed based on the application's data being passed to the Menu component as a property. If we change the recipes array and rerender our Menu component, React will change this DOM as efficiently as possible.

Figure 5-2. Delicious Recipes output

Figure 5-3. Resulting virtual DOM in React Developer Tools 

### 5.4 React Fragments

In the previous section, we rendered the Menu component, a parent component that rendered the Recipe component. We want to take a moment to look at a small example of rendering two sibling components using a React fragment. Let's start by creating a new component called Cat that we'll render to the DOM at the root: 

```js
function Cat({ name }) {
  return <h1>The cat's name is {name}</h1>;
}
  
ReactDOM.render(
  <Cat name="Jungle" />, 
  document.getElementById("root")
); 
```

This will render the h1 as expected, but what might happen if we added a p tag to the Cat component at the same level as the h1?

```js
function Cat({ name }) {
  return (
    <h1>The cat's name is {name}</h1>
    <p>He's good.</p>
  );
}
```

Immediately, we'll see an error in the console that reads Adjacent JSX elements must be wrapped in an enclosing tag and recommends using a fragment. This is where fragments come into play! React will not render two or more adjacent or sibling elements as a component, so we used to have to wrap these in an enclosing tag like a div. This led to a lot of unnecessary tags being created, though, and a bunch of wrappers without much purpose. If we use a React fragment, we can mimic the behavior of a wrapper without actually creating a new tag. Start by wrapping the adjacent tags, the h1 and p, with a React.Fragment tag:

```js
function Cat({ name }) {
  return (
    <React.Fragment>
      <h1>The cat's name is {name}</h1>
      <p>He's good.</p>
    </React.Fragment>
  );
}
```

Adding this clears the warning. You also can use a fragment shorthand to make this look even cleaner:

```js
function Cat({ name }) {
  return (
    <>
      <h1>The cat's name is {name}</h1>
      <p>He's good.</p>
    </>
  );
}
```

1『大赞啊，上面的代码涨知识了，而且也解决了自己之前遇到的困惑。React Fragments 容纳多个组件，做一张信息数据卡片。（2021-05-03）』—— 已完成

If you look at the DOM, the fragment is not visible in the resulting tree:

```js
<div id="root" >
  <h1> The cat's name is Jungle</h1>
  <p> He's good</p>
</div>
```

Fragments are a relatively new feature of React and do away with the need for extra wrapper tags that can pollute the DOM.

### 5.5 Intro to webpack

Once we start working with React in real projects, there are a lot of questions to consider: How do we want to deal with JSX and ESNext transformation? How can we manage our dependencies? How can we optimize our images and CSS?

Many different tools have emerged to answer these questions, including Browserify, gulp, Grunt, Prepack, and more. Due to its features and widespread adoption by large companies, webpack has also emerged as one of the leading tools for bundling.

The React ecosystem has matured to include tools like create-react-app, Gatsby, and Code Sandbox. When you use these tools, a lot of the details about how the code gets compiled are abstracted away. For the remainder of this chapter, we are going to set up our own webpack build. This day in age, understanding that your JavaScript/React code is being compiled by something like webpack is vital, but knowing how to compile your JavaScript/React with something like webpack is not as important. We understand if you want to skip ahead.

Webpack is billed as a module bundler. A module bundler takes all of our different files (JavaScript, LESS, CSS, JSX, ESNext, and so on) and turns them into a single file. The two main benefits of bundling are modularity and network performance.

12『这里的信息让自己对 Webpack 理解比以前深了些，但感觉还是云里雾里，没吃透。先做一张术语卡片。（2021-05-03）』—— 已完成

Modularity will allow you to break down your source code into parts, or modules, that are easier to work with, especially in a team environment. Network performance is gained by only needing to load one dependency in the browser: the bundle. Each script tag makes an HTTP request, and there's a latency penalty for each HTTP request.

Bundling all the dependencies into a single file allows you to load everything with one HTTP request, thereby avoiding additional latency.

Aside from code compilation, webpack also can handle:

1 Code splitting: Splits up your code into different chunks that can be loaded when you need them. Sometimes these are called rollups or layers; the aim is to break up code as needed for different pages or devices.

2 Minification: Removes whitespace, line breaks, lengthy variable names, and unnecessary code to reduce the file size.

3 Feature Flagging: Sends code to one or more — but not all — environments when testing out features.

4 Hot Module Replacement (HMR): Watches for changes in source code. Changes only the updated modules immediately.

The Recipes app we built earlier in this chapter has some limitations that webpack will help us alleviate. Using a tool like webpack to statically build client JavaScript makes it possible for teams to work together on large-scale web applications. We can also gain the following benefits by incorporating the webpack module bundler: 

1 Modularity: Using the module pattern to export modules that will later be imported or required by another part of the application makes source code more approachable. It allows development teams to work together, by allowing them to create and work with separate files that will be statically combined into a single file before sending to production.

2 Composition: With modules, we can build small, simple, reusable React components that we can compose efficiently into applications. Smaller components are easier to comprehend, test, and reuse. They're also easier to replace down the line when enhancing applications.

3 Speed: Packaging all the application's modules and dependencies into a single client bundle will reduce the load time of an application because there's latency associated with each HTTP request. Packaging everything together in a single file means that the client will only need to make a single request. Minifying the code in the bundle will improve load time as well.

4 Consistency: Since webpack will compile JSX and JavaScript, we can start using tomorrow's JavaScript syntax today. Babel supports a wide range of ESNext syntax, which means we don't have to worry about whether the browser supports our code. It allows developers to consistently use cutting-edge JavaScript syntax.

#### 5.5.1 Creating the Project

To demonstrate how we might set up a React project from scratch, let's go ahead and create a new folder on our computer called recipes-app: 

```
mkdir recipes-app
cd recipes-app
```

For this project, we're going to go through the following steps: 1) Create the project. 2) Break down the recipe app into components that live in different files. 3) Set up a webpack build that incorporates Babel.

CREATE-REACT-APP: There's a tool called Create React App that can be used to autogenerate a React project with all of this preconfigured. We're going to take a closer look at what's happening behind the scenes before abstracting these steps away with a tool.

1 CREATE THE PROJECT

Next, we'll create the project and package.json file with npm, sending the -y flag to use all of the defaults. We'll also install webpack, webpack-cli, react, and react-dom:

```
npm init -y
npm install react react-dom serve
```

If we're using npm 5, we don't need to send the --save flag when installing. Next, we'll create the following directory structure to house the components:

```
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
```

FILE ORGANIZATION: There's no one way to organize the files in a React project. This is just one possible strategy.

2 BREAK COMPONENTS INTO MODULES

Currently, the Recipe component is doing quite a bit. We're displaying the name of the recipe, constructing an unordered list of ingredients, and displaying the instructions, with each step getting its own paragraph element. This component should be placed in the Recipe.js file. In any file where we're using JSX, we'll need to import React at the top:

```js
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
```

A more functional approach to the Recipe component would be to break it down into smaller, more focused function components and compose them together. We can start by pulling the instructions out into their own component and creating a module in a separate file we can use for any set of instructions.

In that new file called Instructions.js, create the following component:

```js
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
```

Here, we've created a new component called Instructions. We'll pass the title of the instructions and the steps to this component. This way, we can reuse this component for「Cooking Instructions,」「Baking Instructions,」「Prep Instructions,」or a「Pre-cook Checklist」 — anything that has steps.

Now think about the ingredients. In the Recipe component, we're only displaying the ingredient names, but each ingredient in the data for the recipe has an amount and measurement as well. We'll create a component called Ingredient for this:

```js
// ./src/components/Ingredient.js
import React from "react";
export default function Ingredient({ amount, measurement, name }) {
  return (
    <li>
      {amount} {measurement} {name}
    </li>
  );
}
```

Here, we assume each ingredient has an amount, a measurement, and a name. We destructure those values from our props object and display them each in independent classed span elements.

Using the Ingredient component, we can construct an IngredientsList component that can be used any time we need to display a list of ingredients:

```js
// ./src/components/IngredientsList.js
import React from "react";
import Ingredient from "./Ingredient"; 

export default function IngredientsList({ list }) {
  return (
    <ul className="ingredients">
    {list.map((ingredient, i) => (
      <Ingredient key={i} {...ingredient} />
    ))}
    </ul>
  );
}
```

In this file, we first import the Ingredient component because we're going to use it for each ingredient. The ingredients are passed to this component as an array in a property called list. Each ingredient in the list array will be mapped to the Ingredient component. The JSX spread operator is used to pass all the data to the Ingredient component as props.

Using spread operator:

```
<Ingredient {...ingredient} />
```

is another way of expressing:

```js
<Ingredient
  amount={ingredient.amount}
  measurement={ingredient.measurement}
  name={ingredient.name}
/>
```

So, given an ingredient with these fields:

```js
let ingredient = {
  amount: 1,
  measurement: "cup",
  name: "sugar"
};
```

We get:

```js
<Ingredient amount={1} measurement="cup" name="sugar" /> 
```

Now that we have components for ingredients and instructions, we can compose recipes using these components:

```js
// ./src/components/Recipe.js
import React from "react";
import IngredientsList from "./IngredientsList"; 
import Instructions from "./Instructions"; 

function Recipe({ name, ingredients, steps }) {
  return (
    <section id={name.toLowerCase().replace(/ /g, "-")}>
      <h1>{name}</h1>
      <IngredientsList list={ingredients} />
      <Instructions title="Cooking Instructions" steps={steps} />
    </section>
  );
}

export default Recipe;
```

First, we import the components we're going to use: IngredientsList and Instructions. Now we can use them to create the Recipe component. Instead of a bunch of complicated code building out the entire recipe in one place, we've expressed our recipe more declaratively by composing smaller components. Not only is the code nice and simple, but it also reads well. This shows us that a recipe should display the name of the recipe, a list of ingredients, and some cooking instructions. We've abstracted away what it means to display ingredients and instructions into smaller, simple components.

In a modular approach, the Menu component would look pretty similar. The key difference is that it would live in its own file, import the modules it needs to use, and export itself:

```js
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
```

We still need to use ReactDOM to render the Menu component. The main file for the project is index.js. This will be responsible for rendering the component to the DOM. Let's create this file:

```js
// ./src/index.js
import React from "react"; 
import { render } from "react-dom";
import Menu from "./components/Menu";
import data from "./data/recipes.json";

render(<Menu recipes={data} />, document.getElementById("root")); 
```

The first four statements import the necessary modules for our app to work. Instead of loading react and react-dom via the script tag, we import them so webpack can add them to our bundle. We also need the Menu component and a sample data array that has been moved to a separate module. It still contains two recipes: Baked Salmon and Fish Tacos.

All of our imported variables are local to the index.js file. When we render the Menu component, we pass the array of recipe data to this component as a property. The data is being pulled from the recipes.json file. This is the same data we used earlier in the chapter, but now it's following valid JSON formatting rules:

```json
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
```

1『

目前也用 js 文件导出数据模块。

```js
// ./src/data/recipes.js

const data = [
  {
    name: "Baked Salmon",
    ingredients: [
      { name: "Salmon", amount: 1, measurement: "l lb" },
      { name: "Pine Nuts", amount: 1, measurement: "cup" },
      { name: "Butter Lettuce", amount: 2, measurement: "cups" },
    ],
    steps: [
      "Preheat the oven to 350 degrees.",
      "Spread the olive oil around a glass baking dish.",
    ]
  },
  
  {
    name: "Fish Tacos",
    ingredients: [
      { name: "Whitefish", amount: 1, measurement: "l lb" },
      { name: "Cheese", amount: 1, measurement: "cup" },
    ],
    steps: [
      "Cook the fish on the grill until cooked through.",
      "Place the fish on the 3 tortillas.",
    ]
  }
]

export default data
```

』

Now that we've pulled our code apart into separate modules and files, let's create a build process with webpack that will put everything back together into a single file. You may be thinking,「Wait, we just did all of that work to break everything apart, and now we're going to use a tool to put it back together? Why on Earth…?」Splitting projects into separate files typically makes larger projects easier to manage because team members can work on separate components without overlap. It also means that files can be easier to test.

3 CREATING THE WEBPACK BUILD

In order to create a static build process with webpack, we'll need to install a few things. Everything we need can be installed with npm: 

```js
npm install --save-dev webpack webpack-cli 

yarn add --save-dev webpack webpack-cli 
```

Remember that we've already installed React and ReactDOM.

For this modular Recipes app to work, we're going to need to tell webpack how to bundle our source code into a single file. As of version 4.0.0, webpack does not require a configuration file to bundle a project. If we don't include a config file, webpack will run the defaults to package our code. Using a config file, though, means we'll be able to customize our setup. Plus, this shows us some of the magic of webpack instead of hiding it away. The default webpack configuration file is always webpack.config.js.

The starting file for our Recipes app is index.js. It imports React, ReactDOM, and the Menu.js file. This is what we want to run in the browser first. Wherever webpack finds an import statement, it will find the associated module in the filesystem and include it in the bundle. index.js imports Menu.js, Menu.js imports Recipe.js, Recipe.js imports Instructions.js and IngredientsList.js, and IngredientsList.js imports Ingredient.js. Webpack will follow this import tree and include all of these necessary modules in our bundle. Traversal through all these files creates what's called a dependency graph. A dependency is just something our app needs, like a component file, a library file like React, or an image. Picture each file we need as a circle on the graph, with webpack drawing all the lines between the circles to create the graph. That graph is the bundle.

2『这里的信息，补充进 webpack 术语卡片。（2021-05-03）』—— 已完成

IMPORT STATEMENTS: We're using import statements, which are not presently supported by most browsers or by Node.js. The reason import statements work is that Babel will convert them into `require('module/path');` statements in our final code. The require function is how CommonJS modules are typically loaded.

As webpack builds our bundle, we need to tell it to transform JSX to React elements. The webpack.config.js file is just another module that exports a JavaScript literal object that describes the actions webpack should take. The configuration file should be saved to the root folder of the project, right next to the index.js file:

```js
// ./webpack.config.js
var path = require("path")
module.exports = {
  entry: "./src/index.js",
  output: {
    path: path.join(__dirname, "dist", "assets"), filename: "bundle.js"
  }
}
```

First, we tell webpack that our client entry file is `./src/index.js`. It will automatically build the dependency graph based on import statements starting in that file. Next, we specify that we want to output a bundled JavaScript file to `./dist/bundle.js`. This is where webpack will place the final packaged JavaScript.

Next, let's install the necessary Babel dependencies. We'll need babel-loader and @babel/core:

```
npm install babel-loader @babel/core --save-dev

yarn add babel-loader @babel/core --save-dev
```

The next set of instructions for webpack consists of a list of loaders to run on specified modules. This will be added to the config file under the module field:

```js
module.exports = {
  entry: "./src/index.js",
  output: {
    path: path.join(__dirname, "dist", "assets"), filename: "bundle.js"
  },
  module: {
    rules: [{ test: /\.js$/, exclude: /node_modules/, loader: "babel-loader" }]
  }
};
```

The rules field is an array because there are many types of loaders you can incorporate with webpack. In this example, we're only incorporating the babel-loader. Each loader is a JavaScript object.

The test field is a regular expression that matches the file path of each module that the loader should operate on. In this case, we're running the babel-loader on all imported JavaScript files except those found in the node_modules folder.

At this point, we need to specify presets for running Babel. When we set a preset, we tell Babel which transforms to perform. In other words, we can say,「Hey Babel. If you see some ESNext syntax here, go ahead and transform that code into syntax we're sure the browser understands. If you see some JSX, transform that too.」Start by installing the presets:

```
npm install @babel/preset-env @babel/preset-react --save-dev

yarn add @babel/preset-env @babel/preset-react --save-dev
```

Then create one more file at the root of the project: .babelrc:

```json
{
  "presets" : ["@babel/preset-env", "@babel/preset-react"]
}
```

All right! We've created something pretty cool: a project that resembles a real React app! Let's go ahead and run webpack to make sure this works. Webpack is run statically. Typically, bundles are created before the app is deployed to the server. You can run it from the command line using npx:

```
npx webpack --mode development

yarn run webpack --mode development
```

1『

报错：

```
ERROR in ./src/index.css 3:5
Module parse failed: Unexpected token (3:5)
```

解决方法：[reactjs - .css Module parse failed - Stack Overflow](https://stackoverflow.com/questions/42530582/css-module-parse-failed)

```
npm install --save-dev style-loader css-loader

yarn add --save-dev style-loader css-loader
```

接着修改 webpack 的配置文件：

```js
// ./webpack.config.js
var path = require("path")
module.exports = {
  entry: "./src/index.js",
  output: {
    path: path.join(__dirname, "dist", "assets"), filename: "bundle.js"
  },
  module: {
    rules: [
      { test: /\.js$/, exclude: /node_modules/, loader: "babel-loader" },
      { test: /\.css$/, loader: "style-loader!css-loader" }
    ]
  },
}
```

搞了半天，才意识到目前在做的事情是用 webpack 把所有前端代码打包成一个静态文件，服务器上直接读这个静态文件即可。就是数据流前端开发后，在公司服务器上 `yarn build:prod` 或者阿里云上 `yarn build:stage` 在干的事情一样。真实恍然大悟的感觉。补充进 webpack 的术语卡片中。（2021-05-03）

』

Webpack will either succeed and create a bundle or fail and show you an error. Most errors have to do with broken import references. When debugging webpack errors, look closely at the filenames and file paths used in import statements. You can also add an npm script to your package.json file to create a shortcut:

```json
"scripts": {
  "build": "webpack --mode production"
},
```

Then you can run the shortcut to generate the bundle:

```
npm run build
```

#### 5.5.2 Loading the Bundle

We have a bundle, so now what? We exported the bundle to the dist folder. This folder contains the files we want to run on the web server. The dist folder is where the index.html file should be placed. This file needs to include a target div element where the React Menu component will be mounted. It also requires a single script tag that will load our bundled JavaScript:

```js
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
```

This is the home page for your app. It will load everything it needs from one file, one HTTP request: bundle.js. You'll need to deploy these files to your web server or build a web server application that will serve these files with something like Node.js or Ruby on Rails.

#### 5.5.3 Source Mapping

Bundling our code into a single file can cause some setbacks when it comes time to debug the application in the browser. We can eliminate this problem by providing a source map. A source map is a file that maps a bundle to the original source files. With webpack, all we have to do is add a couple lines to our webpack.config.js file.

```js
//webpack.config.js with source mapping
module.exports = {
  ...
  devtool: "#source-map" // Add this option for source mapping
};
```

Setting the devtool property to '#source-map' tells webpack that you want to use source mapping. The next time you run webpack, you'll see that two output files are generated and added to the dist folder: the original bundle.js and bundle.js.map.

The source map is going to let you debug using your original source files. In the Sources tab of your browser's developer tools, you should find a folder named webpack://. Inside of this folder, you'll see all the source files in your bundle, as shown in Figure 5-4.

Figure 5-4. Sources panel of Chrome Developer Tools

You can debug from these files using the browser step-through debugger. Clicking on any line number adds a breakpoint. Refreshing the browser will pause JavaScript processing when any breakpoints are reached in your source file. You can inspect scoped variables in the Scope panel or add variables to watch in the Watch panel.

#### 5.5.4 Create React App

A pretty amazing tool to have at your disposal as a React developer is Create React App, a command-line tool that autogenerates a React project. Create React App was inspired by the Ember CLI project, and it lets developers get started with React projects quickly without the manual configuration of webpack, Babel, ESLint, and associated tools.

To get started with Create React App, install the package globally: 

```
npm install -g create-react-app
```

Then, use the command and the name of the folder where you'd like the app to be created:

```
create-react-app my-project
```

NPX: You can also use npx to run Create React App without the need for a global install. Simply run npx create-react-app my-project.

This will create a React project in that directory with just three dependencies: React, ReactDOM, and react-scripts. react-scripts was also created by Facebook and is where the real magic happens. It installs Babel, ESLint, webpack, and more so that you don't have to configure them manually. Within the generated project folder, you'll also find a src folder containing an App.js file. Here, you can edit the root component and import other component files.

From within the my-react-project folder, you can run npm start. If you prefer, you can also run yarn start. This will start your application on port 3000.

You can run tests with npm test or yarn test. This runs all of the test files in the project in an interactive mode.

You can also run the npm run build command. Using yarn, run yarn build. This will create a production-ready bundle that has been transformed and minified.

1『搞了半天，自己最初就是用 `create-react-app my-project` 创建的项目，系统默认都已经配置好了，目前感觉没没必须自己配置。按本书一套走下来后，发现系统配置的 build、test、start 都用不了了，错误提示是 `Babel` 版本号跟系统之前配置的不不一致。即使把 node_modules 全删掉重新装系统默认的那个 Babel 版本还是解决不了问题。（2021-05-03）』

Create React App is a great tool for beginners and experienced React developers alike. As the tool evolves, more functionality will likely be added, so you can keep an eye on the changes on GitHub. Another way to get started with React without having to worry about setting up your own customized webpack build is to use CodeSandbox. CodeSandbox is an IDE that runs online at https://codesandbox.io.

In this chapter, we leveled up our React skills by learning about JSX. We created components. We broke those components into a project structure, and we learned more about Babel and webpack. Now we're ready to take our knowledge of components to the next level. It's time to talk about Hooks.