Chapter 11. React Router

When the web started, most websites consisted of a series of pages that users could navigate through by requesting and opening separate files.

The location of the current file or resource was listed in the browser's location bar. The browser's forward and back buttons would work as expected. Bookmarking content deep within a website would allow users to save a reference to a specific file that could be reloaded at the user's request. On a page-based, or server-rendered, website, the browser's navigation and history features simply work as expected.

In a single-page app, all of these features become problematic.

Remember, in a single-page app, everything is happening on the same page. JavaScript is loading information and changing the UI. Features like browser history, bookmarks, and forward and back buttons will not work without a routing solution. Routing is the process of defining endpoints for your client's requests.

1 These endpoints work in

conjunction with the browser's location and history objects. They're used to identify requested content so that JavaScript can load and render the appropriate user interface.

Unlike Angular, Ember, or Backbone, React doesn't come with a standard router. Recognizing the importance of a routing solution, engineers Michael Jackson and Ryan Florence created one named simply React Router. The React Router has been adopted by the community as a popular routing solution for React apps.

2 It's used by

3

companies including Uber, Zendesk, PayPal, and Vimeo. 3

In this chapter, we'll introduce React Router and leverage its features to handle routing on the client.

Incorporating the Router

To demonstrate the capabilities of the React Router, we'll build a classic starter website complete with About, Events, Products, and Contact Us sections. Although this website will feel as though it has multiple pages, there's only one—it's an SPA, a single-page application (see Figure 11-1).

Figure 11-1. Simple website with link navigation

The sitemap for this website consists of a home page, a page for each

section, and an error page to handle 404 Not Found errors (see

Figure 11-2).

Figure 11-2. Sitemap with local links

The router will allow us to set up routes for each section of the website.

Each route is an endpoint that can be entered into the browser's location bar. When a route is requested, we can render the appropriate content.

To start, let's install React Router and React Router DOM. React Router DOM is used for regular React applications that use the DOM.

If you're writing an app for React Native, you'll use react-router-native. We're going to install these packages at their experimental versions because React Router 6 is not officially out at the time of this printing. Once released, you can use the packages without that designation.

npm install react-router@experimental react-router-dom@experimental

We'll also need a few placeholder components for each section or page in the sitemap. We can export these components from a single file called pages.js:

import React from "react";

export function Home() {

return (

<div>

<h1>[Company Website]</h1>

</div>

);

}

export function About() {

return (

<div>

<h1>[About]</h1>

</div>

);

}

export function Events() {

return (

<div>

<h1>[Events]</h1>

</div>

);

}

export function Products() {

return (

<div>

<h1>[Products]</h1>

</div>

);

}

export function Contact() {

return (

<div>

<h1>[Contact]</h1>

</div>

);

}

With these pages stubbed out, we need to adjust the index.js file.

Instead of rendering the App component, we'll render the Router component. The Router component passes information about the current location to any children that are nested inside of it. The Router component should be used once and placed near the root of our component tree:

import React from "react";

import { render } from "react-dom";

import App from "./App";

import { BrowserRouter as Router } from "react-router-dom"; render(

<Router>

<App />

</Router>,

document.getElementById("root")

);

Notice that we're importing BrowserRouter as Router. The next thing we need to do is set up our route configuration. We're going to place this in the App.js file. The wrapper component for any routes we want to render is called Routes. Inside of Routes, we'll use a Route component for each page we want to render. We also want to import all of the pages from the ./pages.js file:

import React from "react";

import { Routes, Route } from "react-router-dom";

import {

Home,

About,

Events,

Products,

Contact

} from "./pages";

function App() {

return (

<div>

<Routes>

<Route path="/" element={<Home />} />

<Route

path="/about"

element={<About />}

/>

<Route

path="/events"

element={<Events />}

/>

<Route

path="/products"

element={<Products />}

/>

<Route

path="/contact"

element={<Contact />}

/>

</Routes>

</div>

);

}

These routes tell the Router which component to render when the window's location changes. Each Route component has path and element properties. When the browser's location matches the path, the element will be displayed. When the location is /, the router will render the Home component. When the location is /products, the router will render the Products component.

At this point, we can run the app and physically type the routes into the browser's location bar to watch the content change. For example, type http://localhost:3000/about into the location bar and watch the About component render.

It's probably not realistic to expect our users to navigate the website by typing routes into the location bar. The react-router-dom provides a Link component that we can use to create browser links.

Let's modify the home page to contain a navigation menu with a link for each route:

import { Link } from "react-router-dom"; export function Home() {

return (

<div>

<h1>[Company Website]</h1>

<nav>

<Link to="about">About</Link>

<Link to="events">Events</Link>

<Link to="products">Products</Link>

<Link to="contact">Contact Us</Link>

</nav>

</div>

);

}

Now users can access every internal page from the home page by clicking on a link. The browser's back button will take them back to the home page.

Router Properties

The React Router passes properties to the components it renders. For instance, we can obtain the current location via a property. Let's use the current location to help us create a 404 Not Found component.

First, we'll create the component:

export function Whoops404() {

return (

<div>

<h1>Resource not found</h1>

</div>

);

}

Then we'll add this to our route configuration in App.js. If we visit a route that doesn't exist, like highway, we want to display the Whoops404 component. We'll use the * as the path value and the component as the element:

function App() {

return (

<div>

<Routes>

<Route path="/" element={<Home />} />

<Route

path="/about"

element={<About />}

/>

<Route

path="/events"

element={<Events />}

/>

<Route

path="/products"

element={<Products />}

/>

<Route

path="/contact"

element={<Contact />}

/>

<Route path="*" element={<Whoops404 />} />

</Routes>

</div>

);

}

Now if we visit localhost:3000/highway, we'll see the 404 page component render. We also could display the value of the route that we've visited by using the location value. Since we're living in a world with React Hooks, there's a hook for that. In the Whoops404

component, create a variable called location that returns the value of the current location (i.e., properties about which page you're navigated to). Then use the value of location.pathname to display the route that's being visited:

export function Whoops404() {

let location = useLocation();

console.log(location);

return (

<div>

<h1>

Resource not found at {location.pathname}

</h1>

</div>

);

}

If you log the location, you can explore that object further.

This section introduced the basics of implementing and working with the React Router. Router is used once and wraps all components that will use routing. All Route components need to be wrapped with a Routes component, which selects the component to render based on the window's present location. Link components can be used to

facilitate navigation. These basics can get you pretty far, but they just scratch the surface of the router's capabilities.

Nesting Routes

Route components are used with content that should be displayed only when specific URLs are matched. This feature allows us to organize our web apps into eloquent hierarchies that promote content reuse.

Sometimes, as users navigate our apps, we want some of the UI to stay in place. In the past, solutions such as page templates and master pages have helped web developers reuse UI elements.

Let's consider the simple starter website. We might want to create subpages for the About page that will display additional content. When the user selects the About section, they should be defaulted to the Company page under that section. The outline looks like this: Home Page

About the Company

Company (default)

History

Services

Location

Events

Products

Contact Us

404 Error Page

The new routes that we need to create will reflect this hierarchy: http://localhost:3000/

http://localhost:3000/about

http://localhost:3000/about

http://localhost:3000/about/history

http://localhost:3000/about/services

http://localhost:3000/about/location

http://localhost:3000/events

http://localhost:3000/products

http://localhost:3000/contact

http://localhost:3000/hot-potato

We also need to remember to stub placeholder components for our new sections: Company, Services, History, and Location. As an example, here's some text for the Services component that you can reuse for the other two:

export function Services() {

<section>

<h2>Our Services</h2>

<p>

Lorem ipsum dolor sit amet, consectetur

adipiscing elit. Integer nec odio. Praesent

libero. Sed cursus ante dapibus diam. Sed

nisi. Nulla quis sem at nibh elementum

imperdiet. Duis sagittis ipsum. Praesent

mauris. Fusce nec tellus sed augue semper

porta. Mauris massa. Vestibulum lacinia arcu

eget nulla. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per

inceptos himenaeos. Curabitur sodales ligula

in libero.

</p>

</section>;

}

With those components created, we can configure the router starting with the App.js file. If you want to create a page hierarchy with the routes, all you need to do is nest the Route components inside of each other:

import {

Home,

About,

Events,

Products,

Contact,

Whoops404,

Services,

History,

Location

} from "./pages";

function App() {

return (

<div>

<Routes>

<Route path="/" element={<Home />} />

<Route path="about" element={<About />}>

<Route

path="services"

element={<Services />}

/>

<Route

path="history"

element={<History />}

/>

<Route

path="location"

element={<Location />}

/>

</Route>

<Route

path="events"

element={<Events />}

/>

<Route

path="products"

element={<Products />}

/>

<Route

path="contact"

element={<Contact />}

/>

<Route path="*" element={<Whoops404 />} />

</Routes>

</div>

);

}

Once you've wrapped the nested routes with the About Route component, you can visit these pages. If you open

http://localhost:3000/about/history, you'll just see the content from the About page, but the History component doesn't display. In order to get that to display, we'll use another feature of React Router DOM: the Outlet component. Outlet will let us render these nested components.

We'll just place it anywhere we want to render child content.

In the About component in pages.js, we'll add this under the <h1>: import {

Link,

useLocation,

Outlet

} from "react-router-dom";

export function About() {

return (

<div>

<h1>[About]</h1>

<Outlet />

</div>

);

}

Now this About component will be reused across the entire section and will display the nested components. The location will tell the app which subsection to render. For example, when the location is http://localhost:3000/about/history, the History component will be rendered inside of the About component.

Using Redirects

Sometimes you want to redirect users from one route to another. For instance, we can make sure that if users try to access content via http://localhost:3000/services, they get redirected to the correct route: http://localhost:3000/about/services.

Let's modify our application to include redirects to ensure that our users can access the correct content:

import {

Routes,

Route,

Redirect

} from "react-router-dom";

function App() {

return (

<div>

<Routes>

<Route path="/" element={<Home />} />

// Other Routes

<Redirect

from="services"

to="about/services"

/>

</Routes>

</div>

);

}

The Redirect component allows us to redirect the user to a specific route.

When routes are changed in a production application, users will still try to access old content via old routes. This typically happens because of bookmarks. The Redirect component provides us with a way to load the appropriate content for users, even if they're accessing our site via an old bookmark.

Throughout this section, we've created a route configuration using the Route component. If you love this structure, feel free to ignore this next section, but we wanted to make sure that you knew how to create a route configuration a different way. It's also possible to use the hook useRoutes to configure your application's routing.

If we wanted to refactor our application to use useRoutes, we'd make the adjustments in the App component (or anywhere where the routes are set up). Let's refactor it:

import { useRoutes } from "react-router-dom"; function App() {

let element = useRoutes([

{ path: "/", element: <Home /> },

{

path: "about",

element: <About />,

children: [

{

path: "services",

element: <Services />

},

{ path: "history", element: <History /> },

{

path: "location",

element: <Location />

}

]

},

{ path: "events", element: <Events /> },

{ path: "products", element: <Products /> },

{ path: "contact", element: <Contact /> },

{ path: "*", element: <Whoops404 /> },

{

path: "services",

redirectTo: "about/services"

}

]);

return element;

}

The official docs call the config element, but you can choose to call it whatever you like. It's also totally optional to use this syntax. Route is a wrapper around useRoutes, so you're actually using this either way.

Choose whichever syntax and style works best for you!

Routing Parameters

Another useful feature of the React Router is the ability to set up

routing parameters. Routing parameters are variables that obtain their values from the URL. They're extremely useful in data-driven web applications for filtering content or managing display preferences.

Let's revisit the color organizer and improve it by adding the ability to select and display one color at a time using React Router. When a user selects a color by clicking on it, the app should render that color and display its title and hex value.

Using the router, we can obtain the color ID via the URL. For example, this is the URL we'll use to display the color「lawn」because the ID for lawn is being passed within the URL:

http://localhost:3000/58d9caee-6ea6-4d7b-9984-65b145031979

To start, let's set up the router in the index.js file. We'll import the Router and wrap the App component:

import { BrowserRouter as Router } from "react-router-dom"; render(

<Router>

<App />

</Router>,

document.getElementById("root")

);

Wrapping the App passes all of the router's properties to the component and any other components nested inside of it. From there, we can set up the route configuration. We'll use the Routes and Route components instead of useRoutes, but remember that this is always an option if you prefer that syntax. Start by importing Routes and Route:

import { Routes, Route } from "react-router-dom"; Then add to the App. This application will have two routes: the ColorList and the ColorDetails. We haven't built ColorDetails yet, but let's import it:

import { ColorDetails } from "./ColorDetails"; export default function App() {

return (

<ColorProvider>

<AddColorForm />

<Routes>

<Route

path="/"

element={<ColorList />}

/>

<Route

path=":id"

element={<ColorDetails />}

/>

</Routes>

</ColorProvider>

);

}

The ColorDetails component will display dynamically based on the id of the color. Let's create the ColorDetails component in a new file called ColorDetails.js. To start, it'll be a placeholder: import React from "react";

export function ColorDetails() {

return (

<div>

<h1>Details</h1>

</div>

);

}

How do we know if this is working? The easiest way to check is to open the React Developer tools and find the id of one of the colors that is being rendered. If you don't have a color yet, then add one and take a look at its id. Once you have the id, you can append that to the localhost:3000 URL. For example, localhost:3000/00fdb4c5-c5bd-4087-a48f-4ff7a9d90af8.

Now, you should see the ColorDetails page appear. Now we know that the router and our routes are working, but we want this to be more dynamic. On the ColorDetails page, we want to display the correct color based on the id that's found in the URL. To do that, we'll use the useParams hook:

import { useParams } from "react-router-dom"; export function ColorDetails() {

let params = useParams();

console.log(params);

return (

<div>

<h1>Details</h1>

</div>

);

}

If we log params, we'll see that this is an object that contains any parameters that are available on the router. We'll destructure this object to grab the id, then we can use that id to find the correct color in the colors array. Let's use our useColors hook to make this happen: import { useColors } from "./";

export function ColorDetails() {

let { id } = useParams(); // destructure id

let { colors } = useColors();

let foundColor = colors.find(

color => color.id === id

);

console.log(foundColor);

return (

<div>

<h1>Details</h1>

</div>

);

}

Logging foundColor shows us that we've found the correct color.

Now all we need to do is display the data about that color in the component:

export function ColorDetails() {

let { id } = useParams();

let { colors } = useColors();

let foundColor = colors.find(

color => color.id === id

);

return (

<div>

<div

style={{

backgroundColor: foundColor.color,

height: 100,

width: 100

}}

></div>

<h1>{foundColor.title}</h1>

<h1>{foundColor.color}</h1>

</div>

);

}

Another feature we want to add to the color organizer is the ability to navigate to the ColorDetails page by clicking on the color in the list.

Let's add this functionality to the Color component. We're going to use another router hook called useNavigate to open the details page when we click on the component. We'll import it first from react-router-dom:

import { useNavigate } from "react-router-dom"; Then we'll call useNavigate, which will return a function we can use to navigate to another page:

let navigate = useNavigate();

Now in the section, we'll add an onClick handler to navigate to the route based on the color id:

let navigate = useNavigate();

return (

<section

className="color"

onClick={() => navigate(`/${id}`)}

>

// Color component

</section>

);

Now, when we click on the section, we'll be routed to the correct page.

Routing parameters are an ideal tool to obtain data that affects the

presentation of your user interface. However, they should only be used when you want users to capture these details in a URL. For example, in the case of the color organizer, users can send other users links to specific colors or all the colors sorted by a specific field. Users can also bookmark those links to return specific data.

In this chapter, we reviewed the basic usage of the React Router. In the next chapter, we'll learn how to use routing on the server.

Express.js documentation,「Basic routing」.

1

The project has been starred over 20,000 times on GitHub.

2

See「Sites Using React Router」.

3

Chapter 12. React and the

