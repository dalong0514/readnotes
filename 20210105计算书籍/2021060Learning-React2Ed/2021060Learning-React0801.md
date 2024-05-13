# 0801. Incorporating Data

Data is the lifeblood of our applications. It flows like water, and it nourishes our components with value. The user interface components we've composed are vessels for data. We fill our applications with data from the internet. We collect, create, and send new data to the internet.

The value of our applications is not the components themselves — it's the data that flows through those components.

When we talk about data, it may sound a little like we're talking about water or food. The cloud is the abundantly endless source from which we send and receive data. It's the internet. It's the networks, services, systems, and databases where we manipulate and store zettabytes of data. The cloud hydrates our clients with the latest and freshest data from the source. We work with this data locally and even store it locally. But when our local data becomes out of sync with the source, it loses its freshness and is said to be stale.

These are the challenges we face as developers working with data. We need to keep our applications hydrated with fresh data from the cloud.

In this chapter, we're going to take a look at various techniques for loading and working with data from the source.

## 8.1 Requesting Data

In the movie Star Wars, the droid C-3P0 is a protocol droid. His specialty, of course, is communication. He speaks over six million languages. Surely, C-3P0 knows how to send an HTTP request, because the Hyper Text Transfer Protocol is one of the most popular ways to transmit data to and from the internet.

HTTP provides the backbone for our internet communication. Every time we load http://www.google.com into our browser, we're asking Google to send us a search form. The files necessary for us to search are transmitted to the browser over HTTP. When we interact with Google by searching for「cat photos,」we're asking Google to find us cat photos. Google responds with data, and images are transferred to our browser over HTTP.

In JavaScript, the most popular way to make an HTTP request is to use fetch. If we wanted to ask GitHub for information about Moon Highway, we could do so by sending a fetch request:

```js
fetch(`https://api.github.com/users/moonhighway`)
  .then(response => response.json())
  .then(console.log)
  .catch(console.error);
```

The fetch function returns a promise. Here, we're making an asynchronous request to a specific URL: https://api.github.com/users/moonhighway. It takes time for that request to traverse the internet and respond with information. When it does, that information is passed to a callback using the .then(callback) method. The GitHub API will respond with JSON data, but that data is contained in the body of the HTTP response, so we call response.json() to obtain that data and parse it as JSON.

Once obtained, we log that data to the console. If anything goes wrong, we'll pass the error to the console.error method. GitHub will respond to this request with a JSON object:

```json
{
  "login" : "MoonHighway",
  "id" : 5952087,
  "node_id" : "MDEyOk9yZ2FuaXphdGlvbjU5NTIwODc=",
  "avatar_url" : "https://avatars0.githubusercontent.com/u/5952087?v=4",
  "bio" : "Web Development classroom training materials.",
  ...
}
```

On GitHub, basic information about user accounts is made available by their API. Go ahead, try searching for yourself: 

```
https://api.github.com/users/<YOUR_GITHUB_USER_NAME> .
```

Another way of working with promises is to use async/await. Since fetch returns a promise, we can await a fetch request inside of an async function:

```js
async function requestGithubUser(githubLogin) {
  try {
  const response = await fetch(
  `https://api.github.com/users/${githubLogin}`
  );
  
  const userData = await response.json();
  console.log(userData);
  } catch (error) {
    console.error(error);
  }
}
```

This code achieves the exact same results as the previous fetch request that was made by chaining .then functions on to the request. When we await a promise, the next line of code will not be executed until the promise has resolved. This format gives us a nice way to work with promises in code. We'll be using both approaches for the remainder of this chapter.

### 8.1.1 Sending Data with a Request

A lot of requests require us to upload data with the request. For instance, we need to collect information about a user in order to create an account, or we may need new information about a user to update their account.

Typically, we use a POST request when we're creating data and a PUT request when we're modifying it. The second argument of the fetch function allows us to pass an object of options that fetch can use when creating our HTTP request:

```js
fetch("/create/user", {
  method: "POST",
  body: JSON.stringify({ username, password, bio })
});
```

This fetch is using the POST method to create a new user. The username, password, and user's bio are being passed as string content in the body of the request.

### 8.1.2 Uploading Files with fetch

Uploading files requires a different type of HTTP request: a multipart-formdata request. This type of request tells the server that a file or multiple files are located in the body of the request. To make this request in JavaScript, all we have to do is pass a FormData object in the body of our request:

```js
const formData = new FormData();
formData.append("username", "moontahoe"); 
formData.append("fullname", "Alex Banks"); 
forData.append("avatar", imgFile);
fetch("/create/user", {
  method: "POST",
  body: formData
});
```

This time, when we create a user, we're passing the username, fullname, and avatar image along with the request as a formData object. Although these values are hardcoded here, we could easily collect them from a form.

### 8.1.3 Authorized Requests

Sometimes, we need to be authorized to make requests. Authorization is typically required to obtain personal or sensitive data. Additionally, authorization is almost always required for users to take action on the server with POST, PUT, or DELETE requests.

Users typically identify themselves with each request by adding a unique token to the request that a service can use to identify the user. This token is usually added as the Authorization header. On GitHub, you can see your personal account information if you send a token along with your request:

```js
fetch(`https://api.github.com/users/${login}`, {
  method: "GET",
  headers: {
    Authorization: `Bearer ${token}`
  }
});
```

Tokens are typically obtained when a user signs into a service by providing their username and password. Tokens can also be obtained from third parties like GitHub or Facebook using with an open standard protocol called OAuth.

GitHub allows you to generate a Personal User token. You can generate one by logging in to GitHub and navigating to: Settings > Developer Settings > Personal Access Tokens. From here, you can create tokens with specific read/write rules and then use those tokens to obtain personal information from the GitHub API. If you generate a Personal Access Token and send it along with the fetch request, GitHub will provide additional private information about your account.

Fetching data from within a React component requires us to orchestrate the useState and useEffect hooks. The useState hook is used to store the response in state, and the useEffect hook is used to make the fetch request. For example, if we wanted to display information about a GitHub user in a component, we could use the following code: 

```js
import React, { useState, useEffect } from "react"; 

function GitHubUser({ login }) {
  const [data, setData] = useState();
  useEffect(() => {
    if (!login) return;
    fetch(`https://api.github.com/users/${login}`)
      .then(response => response.json())
      .then(setData)
      . catch(console.error);
  }, [login]);
  if (data) return <pre>{JSON.stringify(data, null, 2)}</pre>; 
  return null;
}
  
export default function App() {
  return <GitHubUser login="moonhighway" />;
}
```

In this code, our App renders a GitHubUser component and displays JSON data about moonhighway. On the first render, GitHubUser sets up a state variable for data using the useState hook. Then, because data is initially null, the component returns null. Returning null from a component tells React to render nothing. It doesn't cause an error; we'll just see a black screen.

After the component is rendered, the useEffect hook is invoked. This is where we make the fetch request. When we get a response, we obtain and parse the data in that response as JSON. Now we can pass that JSON object to the setData function, which causes our component to render once again, but this time it will have data. This useEffect hook will not be invoked again unless the value for login changes. When it does, we'll need to request more information about a different user from GitHub.

When there is data, we're rendering it as a JSON string in a preelement. The JSON.stringify method takes three arguments: the JSON data to convert to a string, a replacer function that can be used to replace properties of the JSON object, and the number of spaces to use when formatting the data. In this case, we sent null as the replacer because we don't want to replace anything. The 2 represents the number of spaces to be used when formatting the code. This will indent the JSON string two spaces. Using the pre element honors whitespace, so readable JSON is what is finally rendered.

### 8.1.4 Saving Data Locally

We can save data locally to the browser using the Web Storage API.

Data can be saved by either using the window.localStorage or window.sessionStorage objects. The sessionStorage API only saves data for the user's session. Closing the tabs or restarting the browser will clear any data saved to sessionStorage. On the other hand, localStorage will save data indefinitely until you remove it.

JSON data should be saved in browser storage as a string. This means converting an object into a JSON string before saving it and parsing that string into JSON while loading it. Some function to handle saving and loading JSON data to the browser could look like:

```js
const loadJSON = key =>
  key && JSON.parse(localStorage.getItem(key));
const saveJSON = (key, data) =>
  localStorage.setItem(key, JSON.stringify(data));
```

The loadJSON function loads an item from localStorage using the key. The localStorage.getItem function is used to load the data. If the item is there, it's then parsed into JSON before being returned. If it's not there, the loadJSON function will return null.

The saveJSON function will save some data to localStorage using a unique key identifier. The localStorage.setItem function can be used to save data to the browser. Before saving the data, we'll need to convert it to a JSON string.

Loading data from web storage, saving data to web storage, stringifying data, and parsing JSON strings are all synchronous tasks. Both the loadJSON and saveJSON functions are synchronous. So be careful — calling these functions too often with too much data can lead to performance issues. It's typically a good idea to throttle or debounce these functions for the sake of performance.

We could save the user's data that we received from our GitHub request. Then the next time that same user is requested, we could use the data saved to localStorage instead of sending another request to GitHub. We'll add the following code to the GitHubUser component: 

```js
const [data, setData] = useState(loadJSON(`user:${login}`)); 
useEffect(() => {
  if (!data) return;
  if (data.login === login) return;
  const { name, avatar_url, location } = data;
  saveJSON(`user:${login}`, {
  name,
  login,
  avatar_url,
  location
  });
}, [data]);
```

The loadJSON function is synchronous, so we can use it when we invoke useState to set the initial value for data. If there was user data saved to the browser under user:moonhighway, we'll initially set the data using that value. Otherwise, data will initially be null.

When data changes here after it has been loaded from GitHub, we'll invoke saveJSON to save only those user details that we need: name, login, avatar_url, and location. No need to save the rest of the user object when we're not using it. We also skip saving the data when that object is empty, !data. Also, if the current login and data.login are equal to each other, then we already have saved data for that user. We'll skip the step of saving that data again.

Here's a look at the entire GitHubUser component that uses localStorage to save data in the browser:

```js
import React, { useState, useEffect } from "react"; 

const loadJSON = key => key && JSON.parse(localStorage.getItem(key));
const saveJSON = (key, data) => localStorage.setItem(key, JSON.stringify(data));

function GitHubUser({ login }) {
  const [data, setData] = useState(
    loadJSON(`user:${login}`)
  );

  useEffect(() => {
    if (!data) return;
    if (data.login === login) return;
    const { name, avatar_url, location } = data;
    saveJSON(`user:${login}`, {
      name,
      login,
      avatar_url,
      location
    });
  }, [data]);

  useEffect(() => {
    if (!login) return;
    if (data && data.login === login) return; 
    fetch(`https://api.github.com/users/${login}`)
      .then(response => response.json())
      .then(setData)
      . catch(console.error);
  }, [login]);

  if (data) return <pre>{JSON.stringify(data, null, 2)}</pre>; 
  return null;

}
```

Notice the GitHubUser component now has two useEffect hooks.

The first hook is used to save the data to the browser. It's invoked whenever the value for data changes. The second hook is used to request more data from GitHub. The fetch request is not sent when there's already data saved locally for that user. This is handled by the second if statement in the second useEffect hook: if (data && data.login === login) return;. If there is data and the login for that data matches the login property, then there's no need to send an additional request to GitHub. We'll just use the local data.

The first time we run the application, if the login is set to moonhighway, the following object will be rendered to the page:

```json
{
  "login" : "MoonHighway",
  "id" : 5952087,
  "node_id" : "MDEyOk9yZ2FuaXphdGlvbjU5NTIwODc=",
  "avatar_url" : "https://avatars0.githubusercontent.com/u/5952087?v=4",
  "gravatar_id" : "",
  "url" : "https://api.github.com/users/MoonHighway",
  "html_url" : "https://github.com/MoonHighway",
  ...
}
```

This is the response from GitHub. We can tell because this object contains a lot of extra information about the user that we don't need. The first time we run this page we'll see this lengthy response. But the second time we run the page, the response is much shorter:

```json
{
  "name" : "Moon Highway",
  "login" : "moonhighway",
  "avatar_url" : "https://avatars0.githubusercontent.com/u/5952087?v=4",
  "location" : "Tahoe City, CA"
}
```

This time, the data we saved locally for moonhighway is being rendered to the browser. Since we only needed four fields of data, we only saved four fields of data. We'll always see this smaller offline object until we clear the storage:

```js
localStorage.clear();
```

Both sessionStorage and localStorage are essential weapons for web developers. We can work with this local data when we're offline, and they allow us to increase the performance of our applications by sending fewer network requests. However, we must know when to use them. Implementing offline storage adds complexity to our applications, and it can make them tough to work with in development.

Additionally, we don't need to work with web storage to cache data. If we're simply looking for a performance bump, we could try letting HTTP handle caching. Our browser will automatically cache content if we add Cache-Control: `max-age=<EXP_DATE>` to our headers. The `EXP_DATE` defines the expiration date for the content.

### 8.1.5 Handling Promise States

HTTP requests and promises both have three states: pending, success (fulfilled), and fail (rejected). A request is pending when we make the request and are waiting for a response. That response can only go one of two ways: success or fail. If a response is successful, it means we've successfully connected to the server and have received data. In the world of promises, a successful response means that the promise has been resolved. If something goes wrong during this process, we can say the HTTP request has failed or the promise has been rejected. In both cases, we'll receive an error explaining what happened.

We really need to handle all three of these states when we make HTTP requests. We can modify the GitHub user component to render more than just a successful response. We can add a「loading…」message when the request is pending, or we can render the error details if something goes wrong:

```js
function GitHubUser({ login }) {
  const [data, setData] = useState();
  const [error, setError] = useState();
  const [loading, setLoading] = useState(false); 
  
  useEffect(() => {
    if (!login) return;
    setLoading(true);
    fetch(`https://api.github.com/users/${login}`)
      .then(data => data.json())
      .then(setData)
      .then(() => setLoading(false))
      . catch(setError);
  }, [login]);
  
  if (loading) return <h1>loading...</h1>; 
  if (error) return <pre>{JSON.stringify(error, null, 2)}</pre>; 
  if (!data) return null;
  
  return (
    <div className="githubUser">
      <img
        src={data.avatar_url}
        alt={data.login}
        style={{ width: 200 }}
      />
      <div>
        <h1>{data.login}</h1>
        {data.name && <p>{data.name}</p>}
        {data.location && <p>{data.location}</p>}
      </div>
    </div>
  );
}
```

When this request is successful, Moon Highway's information is rendered for the user to see on the screen, as shown in Figure 8-1.

Figure 8-1. Sample output

If something goes wrong, we're simply displaying the error object as a JSON string. In production, we would do more with the error. Maybe we would track it, log it, or try to make another request. While in development, it's OK to render error details, which gives the developer instant feedback.

Finally, while the request is pending, we simply display a「loading…」message using an h1.

Sometimes an HTTP request can succeed with an error. This happens when the request was successful — successfully connected to a server and received a response — but the response body contains an error.

Sometimes servers pass additional errors as successful responses.

Handling all three of these states bloats our code a little bit, but it's essential to do so on every request. Requests take time and a lot could go wrong. Because all requests — and promises — have these three states, it makes it possible to handle all HTTP requests with a reusable hook, or a component, or even a React feature called Suspense. We'll cover each of these approaches, but first, we must introduce the concept of render props.

## 8.2 Render Props

Render props are exactly what they sound like: properties that are rendered. This can mean components that are sent as properties that are rendered when specific conditions are met, or it can mean function properties that return components that will be rendered. In the second case, when they're functions, data can be passed as arguments and used when rendering the returned component.

Render props are useful when maximizing reusability in asynchronous components. With this pattern, we can create components that abstract away complex mechanics or monotonous boilerplate that's necessary for application development.

Consider the task of displaying a list:

```ks
import React from "react";
const tahoe_peaks = [
  { name: "Freel Peak", elevation: 10891 },
  { name: "Monument Peak", elevation: 10067 },
  { name: "Pyramid Peak", elevation: 9983 },
  { name: "Mt. Tallac", elevation: 9735 }
];

export default function App() {
  return (
    <ul>
      {tahoe_peaks.map((peak, i) => (
        <li key={i}>
          {peak.name} - {peak.elevation.toLocaleString()}ft
        </li>
      ))}
    </ul>
  );
}
```

In this example, the four tallest peaks in Tahoe are rendered into an unordered list. This code makes sense, but mapping over an array to render each item individually does introduce some code complexity.

Mapping over an array of items is also a pretty common task. We may find ourselves frequently repeating this pattern. We could create a List component that we can reuse as a solution whenever we need to render an unordered list.

In JavaScript, arrays either contain values or they're empty. When a list is empty, we need to display a message to our users. However, that message may change upon implementation. No worries — we can pass a component to render when the list is empty:











function List({ data = [], renderEmpty }) {

if (!data.length) return renderEmpty;

return <p>{data.length} items</p>;

}

export default function App() {

return <List renderEmpty={<p>This list is empty</p>} />;

}

The List component expects two properties: data and renderEmpty.

The first argument, data, represents the array of items that are to be mapped over. Its default value is an empty array. The second argument, renderEmpty, is a component that will be rendered if the list is empty.

So when data.length is 0, the List component renders whatever was passed as the renderEmpty property by returning that property.

In this case, users would see the following message: This list is empty.

renderEmpty is a render prop because it contains a component to render when a particular condition has been met — in this case, when the list is empty or the data property has not been provided.

We can send this component an actual array of data:

export default function App() {

return (

<List

data={tahoe_peaks}

renderEmpty={<p>This list is empty</p>}

/>

);

}

Doing so at this point only renders the number of items found within the array: 4 items.

We can also tell our List component what to render for each item

found within the array. For example, we can send a renderItem property:

export default function App() {

return (

<List

data={tahoe_peaks}

renderEmpty={<p>This list is empty</p>}

renderItem={item => (

<>

{item.name} - {item.elevation.toLocaleString()}ft

</>

)}

/>

);

}

This time, the render prop is a function. The data (the item itself) is passed to this function as an argument so that it can be used when what to render for each Tahoe Peak is decided. In this case, we render a React fragment that displays the item's name and elevation. If the array is tahoe_peaks, we expect the renderItem property to be invoked four times: once for each of the peaks in the array.

This approach allows us to abstract away the mechanics of mapping over arrays. Now the List component will handle the mapping; we just have to tell it what to render:

function List({ data = [], renderItem, renderEmpty }) {

return !data.length ? (

renderEmpty

) : (

<ul>

{data.map((item, i) => (

<li key={i}>{renderItem(item)}</li>

))}

</ul>

);

}

When the data array is not empty, the List component renders an unordered list, <ul>. It maps over each item within the array using the

.map method and renders a list item, <li>, for every value within the array. The List component makes sure each list item receives a unique key. Within each <li> element, the renderItem property is invoked and the item itself is passed to that function property as an argument.

The result is an unordered list that displays the name and elevation of each of Tahoe's tallest peaks.

The good news is we have a reusable List component that we can use whenever we need to render an unordered list. The bad news is our component is a bit bare bones. There are better components we can use to handle this task.

Virtualized Lists

If it's our job to develop a reusable component for rendering lists, there are many different use cases to consider and solutions to implement.

One of the most important things to consider is what happens when the list is very large. Many of the data points we work with in production can feel infinite. A Google search yields pages and pages of results.

Searching for a place to stay in Tahoe on Airbnb results in a list of houses and apartments that seems to never end. Production applications typically have a lot of data that needs to be rendered, but we can't render it all at once.

There's a limit to what the browser can render. Rendering takes time, processing power, and memory, all three of which have eventual limitations. This should be taken into consideration when developing a reusable list component. When the data array is very large, what should we do?

Even though our search for a place to stay may have yielded one thousand results, we cannot possibly look at all those results at the same time — there's not enough screen space for all the images, names, and prices. We might only be able to see about five results at a time.

When scrolling, we can see more results, but we have to scroll down pretty far to see a thousand results. Rendering a thousand results in a scrollable layer is asking a lot of the phone.

Instead of rendering 1,000 results at a time, what if we only rendered 11? Remember that the user can only see about five results on one screen. So we render the five items the user can see and render six items off screen both above and below the visible window of items.

Rendering items above and below the visible window will allow the user to scroll in both directions. We can see that in Figure 8-2.

Figure 8-2. Windowing with off-screen content As the user scrolls, we can unmount the results that have already been viewed as well as render new results off screen, ready for the user to reveal via the scroll. This resulting solution means that the browser will only render 11 elements at a time while the data for the rest of the elements is there waiting to be rendered. This technique is called windowing or virtualization. It allows us to scroll very large, sometimes infinite lists of data without crashing our browser.

There's a lot to consider when building a virtualized list component.

Thankfully, we don't have to start from scratch; the community has already developed many virtualized list components for us to use. The most popular of these for the browser are react-window and react-virtualized. Virtualized lists are so important that React Native even ships with one: the FlatList. Most of us will not have to build virtualized list components, but we do need to know how to use them.

To implement a virtualized list, we're going to need a lot of data — in this case, fake data:

npm i faker

Installing faker will allow us to create a large array of fake data. For this example, we'll use fake users. We'll create five thousand fake users at random:

import faker from "faker";

const bigList = [...Array(5000)].map(() => ({

name: faker.name.findName(),

email: faker.internet.email(),

avatar: faker.internet.avatar()

}));

The bigList variable was created by mapping over an array of five thousand empty values and replacing those empty values with information about a fake user. The name, email, and avatar for each user are generated at random using functions supplied by faker.

If we use the List component we created in the last section, it will render all five thousand users at the same time:

export default function App() {

const renderItem = item => (

<div style={{ display: "flex" }}>

<img src={item.avatar} alt={item.name} width={50} />

<p>

{item.name} - {item.email}

</p>

</div>

);

return <List data={bigList} renderItem={renderItem} />;

}

This code creates a div element for each user. Within that div, an img element is rendered for that user's photo, and the user name and email are rendered with a paragraph element, as shown in Figure 8-3.

Figure 8-3. Performance results

The combination of React and modern browsers is already pretty amazing. We're most likely able to render all five thousand users, but it takes a while. In this example, it took 52ms to be exact. As the number of users in our list goes up, so does this time, until we eventually reach a tipping point.

Let's render the same fake user list using react-window:

npm i react-window

react-window is a library that has several components we can use to render virtualized lists. In this example, we'll use the FixSizeList component from react-window:

import React from "react";

import { FixedSizeList } from "react-window"; import faker from "faker";

const bigList = [...Array(5000)].map(() => ({

name: faker.name.findName(),

email: faker.internet.email(),

avatar: faker.internet.avatar()

}));

export default function App() {

const renderRow = ({ index, style }) => (

<div style={{ ...style, ...{ display: "flex" } }}>

<img

src={bigList[index].avatar}

alt={bigList[index].name}

width={50}

/>

<p>

{bigList[index].name} - {bigList[index].email}

</p>

</div>

);

return (

<FixedSizeList

height={window.innerHeight}

width={window.innerWidth - 20}

itemCount={bigList.length}

itemSize={50}

>

{renderRow}

</FixedSizeList>

);

}

FixedSizeList is slightly different from our List component. It requires the total number of items in the list along with the number of pixels each row requires as the itemSize property. Another big difference in this syntax is that the render prop is being passed to FixedSizeList as the children property. This render props pattern is used quite frequently.

So, let's see what happens when five thousand fake users are rendered with the FixSizeList component (see Figure 8-4).

This time, not all of the users are being rendered at once. Only those rows that the user can see or easily scroll to are being rendered. Notice that it only takes 2.6ms for this initial render.

As you scroll down to reveal more users, the FixedSizeList is hard at work rendering more users off screen as well as removing users that have scrolled off screen. This component automatically handles scrolling in both directions. This component may render quite frequently, but the renders are fast. It also doesn't matter how many users are in our array: the FixedSizeList can handle it.

Figure 8-4. 2.6ms for this render

Creating a Fetch Hook

We know that a request is either pending, successful, or failed. We can reuse the logic that's necessary for making a fetch request by creating a custom hook. We'll call this hook useFetch, and we can use it in components across our application whenever we need to make a fetch request:

import React, { useState, useEffect } from "react";

export function useFetch(uri) {

const [data, setData] = useState();

const [error, setError] = useState();

const [loading, setLoading] = useState(true); useEffect(() => {

if (!uri) return;

fetch(uri)

.then(data => data.json())

.then(setData)

.then(() => setLoading(false))

. catch(setError);

}, [uri]);

return {

loading,

data,

error

};

}

This custom hook was created by composing the useState and useEffect hooks. The three states of a fetch request are represented in this hook: pending, success, and error. When the request is pending, the hook will return true for loading. When the request is successful and data is retrieved, it will be passed to the component from this hook. If something goes wrong, then this hook will return the error.

All three of these states are managed inside of the useEffect hook.

This hook is invoked every time the value for uri changes. If there's no uri, the fetch request is not made. When there's a uri, the fetch request begins. If the request is successful, we pass the resulting JSON

to the setData function, changing the state value for data. After that, we then change the state value for loading to false because the request

was successful (i.e., it's no longer pending). Finally, if anything goes wrong, we catch it and pass it to setError, which changes the state value for error.

Now we can use this hook to make fetch requests within our components. Anytime the values for loading, data, or error change, this hook causes the GitHubUser component to rerender with those new values:

function GitHubUser({ login }) {

const { loading, data, error } = useFetch(

`https://api.github.com/users/${login}`

);

if (loading) return <h1>loading...</h1>; if (error)

return <pre>{JSON.stringify(error, null, 2)}</pre>; return (

<div className="githubUser">

<img

src={data.avatar_url}

alt={data.login}

style={{ width: 200 }}

/>

<div>

<h1>{data.login}</h1>

{data.name && <p>{data.name}</p>}

{data.location && <p>{data.location}</p>}

</div>

</div>

);

}

Although the component now has less logic, it still handles all three states. Assuming we have a SearchForm component ready to collect

search strings from the user, we can add the GitHubUser component to our main App component:

import React, { useState } from "react"; import GitHubUser from "./GitHubUser";

import SearchForm from "./SearchForm";

export default function App() {

const [login, setLogin] = useState("moontahoe"); return (

<>

<SearchForm value={login} onSearch={setLogin} />

<GitHubUser login={login} />

</>

);

}

The main App component stores the username of the GitHub user in state. The only way to change this value is to use the search form to search for a new user. Whenever the value of login changes, the value sent to useFetch changes because it depends on the login property: https://api.github.com/users/${login}. This changes the uri within our hook and triggers a fetch request for the new user login. We've created a custom hook and used it to successfully create a small application that can be used to look up and display GitHub user details. We'll continue to use this hook as we iterate on this application.

Creating a Fetch Component

Hooks typically allow us to reuse functionality across components.

There are times when we find ourselves repeating the exact same pattern when it comes to rendering within our components. For example, the loading spinner we choose to render may be the exact

same spinner we want to render across our entire application whenever a fetch request is pending. The way we handle errors with our fetch requests may also be consistent across our application.

Instead of replicating the exact same code in multiple components across our application, we can create one component to render consistent loading spinners and consistently handle all of our errors across our entire domain. Let's create a Fetch component: function Fetch({

uri,

renderSuccess,

loadingFallback = <p>loading...</p>,

renderError = error => (

<pre>{JSON.stringify(error, null, 2)}</pre>

)

}) {

const { loading, data, error } = useFetch(uri);

if (loading) return loadingFallback;

if (error) return renderError(error);

if (data) return renderSuccess({ data });

}

The custom hook, useFetch, is one layer of abstraction: it abstracts away the mechanics of making a fetch request. The Fetch component is an additional layer of abstraction: it abstracts away the mechanics of handling what to render. When the request is loading, the Fetch component will render whatever was passed to the optional loadingFallback property. When it's successful, the JSON response data is passed to the renderSuccess property. If there's an error, it's rendered using the optional renderError property. The

loadingFallback and renderError properties provide an optional

layer of customization. However, when they're not supplied, they fall back to their default values.

With the Fetch component in our arsenal, we can really simplify the logic in our GitHubUser component:

import React from "react";

import Fetch from "./Fetch";

export default function GitHubUser({ login }) {

return (

<Fetch

uri={`https://api.github.com/users/${login}`}

renderSuccess={UserDetails}

/>

);

}

function UserDetails({ data }) {

return (

<div className="githubUser">

<img

src={data.avatar_url}

alt={data.login}

style={{ width: 200 }}

/>

<div>

<h1>{data.login}</h1>

{data.name && <p>{data.name}</p>}

{data.location && <p>{data.location}</p>}

</div>

</div>

);

}

The GitHubUser component receives a login for a user to look up on GitHub. We use that login to construct the uri property we send to the fetch component. If successful, the UserDetails component is

rendered. When the Fetch component is loading, the default

「loading…」message will be displayed. If something goes wrong, the error details are automatically displayed.

We can provide custom values for these properties. Here's an example of how we can alternatively use our flexible component:

<Fetch

uri={`https://api.github.com/users/${login}`}

loadingFallback={<LoadingSpinner />}

renderError={error => {

// handle error

return <p>Something went wrong... {error.message}</p>;

}}

renderSuccess={({ data }) => (

<>

<h1>Todo: Render UI for data</h1>

<pre>{JSON.stringify(data, null, 2)}</pre>

</>

)}

/>

This time, the Fetch component will render our custom loading spinner. If something goes wrong, we hide the error details. When the request is successful, we've chosen to alternatively render the raw data along with a TODO message for ourselves.

Be careful: extra layers of abstraction, whether through hooks or components, can add complexity to our code. It's our job to reduce complexity wherever we can. However, in this case, we've reduced complexity by abstracting away reusable logic into a component and a hook.

Handling Multiple Requests

Once we start making requests for data from the internet, we won't be able to stop. More often than not, we need to make several HTTP

requests to obtain all the data required to hydrate our application. For example, we're currently asking GitHub to provide information about a user's account. We'll also need to obtain information about that user's repositories. Both of these data points are obtained by making separate HTTP requests.

GitHub users typically have many repositories. Information about a user's repositories is passed as an array of objects. We're going to create a special custom hook called useIterator that will allow us to iterate through any array of objects:

export const useIterator = (

items = [],

initialIndex = 0

) => {

const [i, setIndex] = useState(initialIndex);

const prev = () => {

if (i === 0) return setIndex(items.length - 1); setIndex(i - 1);

};

const next = () => {

if (i === items.length - 1) return setIndex(0); setIndex(i + 1);

};

return [items[i], prev, next];

};

This hook will allow us to cycle through any array. Because it returns items inside of an array, we can take advantage of array destructuring

to give these values names that make sense: const [letter, previous, next] = useIterator([

"a",

"b",

"c"

]);

In this case, the initial letter is「b.」If the user invokes next, the component will rerender, but this time, the value for letter will be

「b.」Invoke next two more times, and the value for letter will once again be「a」because this iterator circles back around to the first item in the array instead of letting the index go out of bounds.

The useIterator hook takes in an array of items and an initial index.

The key value to this iterator hook is the index, i, which was created with the useState hook. i is used to identify the current item in the array. This hook returns the current item, item[i], as well as functions for iterating through that array: prev and next. Both the prev and next functions either decrement or increment the value of i by invoking setIndex. This action causes the hook to rerender with a new index.

Memozing Values

The useIterator hook is pretty cool. But we can do even better by memoizing the value for item as well as the function for prev and next:

import React, { useCallback, useMemo } from "react"; export const useIterator = (

items = [],

initialValue = 0

) => {

const [i, setIndex] = useState(initialValue);

const prev = useCallback(() => {

if (i === 0) return setIndex(items.length - 1); setIndex(i - 1);

}, [i]);

const next = useCallback(() => {

if (i === items.length - 1) return setIndex(0); setIndex(i + 1);

}, [i]);

const item = useMemo(() => items[i], [i]);

return [item || items[0], prev, next];

};

Here, both prev and next are created with the useCallback hook.

This ensures that the function for prev will always be the same until the value for i changes. Likewise, the item value will always point to the same item object unless the value for i changes.

Memoizing these values does not give us huge performance gains, or at least not enough to justify the code complexity. However, when a consumer uses the useIterator component, the memoized values will always point to the exact same object and function. This makes it easier on our consumers when they need to compare these values or use them in their own dependency arrays.

Now, we're going to create a repository menu component. Within this component, we'll use the useIterator hook to allow the users to cycle through their list of repositories:

< learning-react >

If they click the Next button, they'll see the name of the next repository. Likewise, if they click the Previous button, they'll see the name of the previous repository. RepoMenu is the component we'll create to provide this feature:

import React from "react";

import { useIterator } from "../hooks";

export function RepoMenu({

repositories,

onSelect = f => f

}) {

const [{ name }, previous, next] = useIterator(

repositories

);

useEffect(() => {

if (!name) return;

onSelect(name);

}, [name]);

return (

<div style={{ display: "flex" }}>

<button onClick={previous}>&lt;</button>

<p>{name}</p>

<button onClick={next}>&gt;</button>

</div>

);

}

RepoMenu receives a list of repositories as a prop. It then destructures the name from the current repository object and the previous and next functions from useIterator. &lt; is an entity for

「Less Than,」and a less than sign,「<」, is displayed. The same is true

for &gt;, greater than. These are indicators for previous and next, and when the user clicks on either of these indicators, the component is rerendered with a new repository name. If the name changes, then the user has selected a different repository, so we invoke the onSelect function and pass the name of the new repository to that function as an argument.

Remember, array destructuring allows us to name the items whatever we want. Even though we named those functions prev and next within the hook, here, when we use the hook, we can change their names to previous and next.

Now we can create the UserRepositories component. This

component should request a list of a GitHub user's repositories first, and once received, pass that list to the RepoMenu component: import React from "react";

import Fetch from "./Fetch";

import RepoMenu from "./RepoMenu";

export default function UserRepositories({

login,

selectedRepo,

onSelect = f => f

}) {

return (

<Fetch

uri={`https://api.github.com/users/${login}/repos`}

renderSuccess={({ data }) => (

<RepoMenu

repositories={data}

selectedRepo={selectedRepo}

onSelect={onSelect}

/>

)}

/>

);

}

The UserRepositories component requires a login to use in order to make the fetch request for a list of repositories. That login is used to create the URI and pass it to the Fetch component. Once the fetch has successfully resolved, we'll render the RepoMenu along with the list of repositories that was returned from the Fetch component as data.

When the user selects a different repository, we simply pass the name of that new repository along to the parent object:

function UserDetails({ data }) {

return (

<div className="githubUser">

<img src={data.avatar_url} alt={data.login} style={{ width: 200 }}

/>

<div>

<h1>{data.login}</h1>

{data.name && <p>{data.name}</p>}

{data.location && <p>{data.location}</p>}

</div>

<UserRepositories

login={data.login}

onSelect={repoName => console.log(`${repoName} selected`)}

/>

</div>

);

Now we need to add our new component to the UserDetails

component. When the UserDetails component is rendered, we'll also render that user's repository list. Assuming the login value is eveporcello, the rendered output for the above component would look something like Figure 8-5.

Figure 8-5. Repository output

In order to get information about Eve's account along with her list of repositories, we need to send two separate HTTP requests. A majority of our lives as React developers will be spent like this: making multiple requests for information and composing all of the information received into beautiful user interface applications. Making two requests for information is just the beginning. In the next section, we'll continue to make more requests of GitHub so we can see the README.md for the selected repository.

Waterfall Requests

In the last section, we made two HTTP requests. The first request was for a user's details, then once we had those details, we made a second

request for that user's repositories. These requests happen one at a time, one after the other.

The first request is made when we initially fetch the user's details:

<Fetch

uri={`https://api.github.com/users/${login}`}

renderSuccess={UserDetails}

/>

Once we have that user's details, the UserDetails component is rendered. It in turn renders UserRepositories, which then sends a fetch request for that user's repositories:

<Fetch

uri={`https://api.github.com/users/${login}/repos`}

renderSuccess={({ data }) => (

<RepoMenu repositories={data} onSelect={onSelect} />

)}

/>

We call these requests waterfall requests because they happen one right after the other — they're dependent on each other. If something goes wrong with the user details request, the request for that user's repositories is never made.

Let's add some more layers (water?) to this waterfall. First, we request the user's info, then their repository list, then, once we have their repository list, we make a request for the first repository's README.md file. As the user cycles through the list of repositories, we'll make additional requests for the associated README to each repository.

Repository README files are written using Markdown, which is a text format that can be easily rendered as HTML with the

ReactMarkdown component. First, let's install react-markdown: npm i react-markdown

Requesting the contents of a repository's README file also requires a waterfall of requests. First, we have to make a data request to the repository's README route:

https://api.github.com/repos/${login}/${repo}/readme. GitHub will respond to this route with the details about a repository's README

file but not the contents of that file. It does provide us with a download_url that we can use to request the contents of the README

file. But to get the Markdown content, we'll have to make an additional request. Both of these requests can be made within a single async function:

const loadReadme = async (login, repo) => {

const uri = `https://api.github.com/repos/${login}/${repo}/readmè; const { download_url } = await fetch(uri).then(res => res.json()

);

const markdown = await fetch(download_url).then(res => res.text()

);

console.log(`Markdown for ${repo}\n\n${markdown}`);

};

In order to find a repository README, we need the repository owner's login and the name of the repository. Those values are used to construct a unique URL:

https://api.github.com/repos/moonhighway/learning-react/readme.

When this request is successful, we destructure the download_url from its response. Now we can use this value to download the contents of the README; all we have to do is fetch the download_url. We'll parse this text as text — res.text() — rather than JSON because the body of the response is Markdown text.

Once we have the Markdown, let's render it by wrapping the loadReadme function inside of a React component:

import React, {

useState,

useEffect,

useCallback

} from "react";

import ReactMarkdown from "react-markdown"; export default function RepositoryReadme({ repo, login }) {

const [loading, setLoading] = useState(false); const [error, setError] = useState();

const [markdown, setMarkdown] = useState(""); const loadReadme = useCallback(async (login, repo) => {

setLoading(true);

const uri = `https://api.github.com/repos/${login}/${repo}/readmè; const { download_url } = await fetch(uri).then(res => res.json()

);

const markdown = await fetch(download_url).then(res => res.text()

);

setMarkdown(markdown);

setLoading(false);

}, []);

useEffect(() => {

if (!repo || !login) return; loadReadme(login, repo). catch(setError);

}, [repo]);

if (error)

return <pre>{JSON.stringify(error, null, 2)}</pre>; if (loading) return <p>Loading...</p>; return <ReactMarkdown source={markdown} />;

}

First, we add the loadReadme function to the component using the useCallback hook to memoize the function when the component initially renders. This function now changes the loading state to true before the fetch request and changes it back to false after the request.

When the Markdown is received, it's saved in state using the setMarkdown function.

Next, we need to actually call loadReadme, so we add a useEffect hook to load the README file after the component initially renders. If for some reason the properties for repo and login are not present, the README will not be loaded. The dependency array in this hook contains [repo]. This is because we want to load another README if the value for repo changes. If anything goes wrong while loading the README, it will be caught and sent to the setError function.

Notice we have to handle the same three render states that we do for every fetch request: pending, success, and fail. Finally, when we have a successful response, the Markdown itself is rendered using the ReactMarkdown component.

All there is left to do is render the RepositoryReadme component

inside of the RepoMenu component. As the user cycles through repositories using the RepoMenu component, the README for each repository will also be loaded and displayed:

export function RepoMenu({ repositories, login }) {

const [{ name }, previous, next] = useIterator(

repositories

);

return (

<>

<div style={{ display: "flex" }}>

<button onClick={previous}>&lt;</button>

<p>{name}</p>

<button onClick={next}>&gt;</button>

</div>

<RepositoryReadme login={login} repo={name} />

</>

);

}

Now our application is really making multiple requests; initially, it makes four requests: one for the user's details, then one for that user's repository list, then one for information about the selected repository's README, and finally one more request for the text contents of the README. These are all waterfall requests because they happen one after another.

Additionally, as the user interacts with the application, more requests are made. Two waterfall requests are made to obtain the README file every time the user changes the current repository. All four initial waterfall requests are made every time the user searches for a different GitHub account.

Throttling the Network Speed

All of these requests are visible from the Network tab under your developer tools. From this tab, you can see every request, and you can throttle your network speed to see how these requests unfold on slow networks. If you want to see how the waterfall requests happen one after another you can slow down your network speed and see the loading messages as they're rendered.

The Network tab is available under the developer tools of most major browsers. To throttle the network speed in Google Chrome, select the arrow next to the word「Online,」as demonstrated in Figure 8-6.

Figure 8-6. Changing the speed of the network request This will open a menu where you can choose various speeds, as you can see in Figure 8-7.

Figure 8-7. Selecting the speed of the network request Selecting「Fast 3G」or「Slow 3G」will significantly throttle your network requests.

Additionally, the Network tab displays a timeline for all of the HTTP

requests. You can filter this timeline to only view「XHR」requests.

This means it will only show the request made using fetch (Figure 8-

8).

Figure 8-8. The waterfall of a request

Here, we see that four requests were made one after the other. Notice that the loading graphic is titled「Waterfall.」This shows that each request is made after the other is complete.

Parallel Requests

Sometimes, it's possible to make an application faster by sending all requests at once. Instead of having each request occur one after another in a waterfall, we can send our requests in parallel, or at the same time.

The reason our application is currently making a waterfall of request is that the components are rendered inside of one another. GitHubUser eventually renders UserRepositories, which eventually renders RepositoryReadme. Requests are not made until each component has been rendered.

Making these requests in parallel is going to require a different approach. First, we'll need to remove the <RepositoryReadme /> from the RepoMenu's render function. This is a good move. The RepoMenu should only focus on the logistics of creating a menu of repositories that the user can cycle through. The RepositoryReadme

component should be handed in a different component.

Next, we'll need to remove <RepoMenu /> from the renderSuccess property of UserRepositories. Likewise, <UserRepositories /> needs to be removed from the UserDetails component.

Instead of nesting these components inside of one another, we'll place them all on the same level next to one another, all within the App component:

import React, { useState } from "react"; import SearchForm from "./SearchForm";

import GitHubUser from "./GitHubUser";

import UserRepositories from "./UserRepositories"; import RepositoryReadme from "./RepositoryReadme"; export default function App() {

const [login, setLogin] = useState("moonhighway"); const [repo, setRepo] = useState("learning-react"); return (

<>

<SearchForm value={login} onSearch={setLogin} />

<GitHubUser login={login} />

<UserRepositories

login={login}

repo={repo}

onSelect={setRepo}

/>

<RepositoryReadme login={login} repo={repo} />

</>

);

}

The GitHubUser, UserRepositories, and RepositoryReadme

components all send HTTP requests to GitHub for data. Rending them side-by-side on the same level will cause all of these requests to

happen at the same time, in parallel.

Each component requires specific information in order to make the request. We need a login to obtain a GitHub user. We need a login to obtain a list of user repositories. The RepositoryReadme requires both a login and a repo to work properly. To make sure all of the components have what they need to make their requests, we initialize the app to display the details for the user「moonhighway」and the repository「learning-react.」

If the user searches for another GitHubUser with the SearchForm, the value for login will change, which will trigger the useEffect hooks within our components, causing them to make additional requests for data. If the user cycles through the list of repositories, then the onSelect property for UserRepositories will be invoked, which causes the repo value to change. Changing the repo value will trigger the useEffect hook inside of the RepositoryReadme component, and a new README will be requested.

The RepoMenu component always starts with the first repository, no matter what. We have to see if there's a selectedRepo property. If there is, we need to use it to find the initial index for the repository to be displayed:

export function RepoMenu({ repositories, selected, onSelect = f => f }) {

const [{ name }, previous, next] = useIterator(

repositories,

selected ? repositories.findIndex(repo => repo.name === selected) : null

);

...

}

The second argument for the useIterator hook is the initial index to start with. If there's a selected property, then we'll search for the index of the selected repository by name. This is required to make sure the repository menu displays the correct repository initially. We also need to pass this selected property to this component from UserRepositories:

<Fetch

uri={`https://api.github.com/users/${login}/repos`}

renderSuccess={({ data }) => (

<RepoMenu

repositories={data}

selected={repo}

onSelect={onSelect}

/>

)}

/>

Now that the repo property is being passed down to the RepoMenu, the menu should select the initial repository, which in our case is

「learning-react.」

If you take a look at the Network tab, you'll notice we've made three requests in parallel, as shown in Figure 8-9.

Figure 8-9. Creating a parallel request

So each component made its request at the same time. The RepoReadme component still has to make a waterfall request to obtain the contents of the README file. This is OK. It's hard to make every request right when your app initially renders. Parallel and waterfall requests can work in conjunction with each other.

Waiting for Values

We currently initialize the values for login and repo to

「moonhighway」and「learning-react.」We may not always be able to guess which data to render first. When that's the case, we simply don't render the component until the data it requires is present: export default function App() {

const [login, setLogin] = useState();

const [repo, setRepo] = useState();

return (

<>

<SearchForm value={login} onSearch={setLogin} />

{login && <GitHubUser login={login} />}

{login && (

<UserRepositories

login={login}

repo={repo}

onSelect={setRepo}

/>

)}

{login && repo && (

<RepositoryReadme login={login} repo={repo} />

)}

</>

);

}

In this scenario, none of the components are rendered until their

required props have values. Initially, the only component rendered is the SearchForm. Searching for a user will change the value for login, causing the UserRepositories component to render. When this component looks up the repositories, it will select the first repository in the list, causing setRepo to be invoked. Finally, we have a login and a repo, so the RepositoryReadme component will be rendered.

Canceling Requests

Thinking about our application a little bit more, we realize that the user could empty the search field and search for no user at all. In this case, we would also want to make sure that the value for repo is also empty.

Let's add a handleSearch method that makes sure the repo value changes when there's no value for login:

export default function App() {

const [login, setLogin] = useState("moonhighway"); const [repo, setRepo] = useState("learning-react"); const handleSearch = login => {

if (login) return setLogin(login);

setLogin("");

setRepo("");

};

if (!login)

return (

<SearchForm value={login} onSearch={handleSearch} />

);

return (

<>

<SearchForm value={login} onSearch={handleSearch} />

<GitHubUser login={login} />

<UserRepositories

login={login}

repo={repo}

onSelect={setRepo}

/>

<RepositoryReadme login={login} repo={repo} />

</>

);

}

We've added a handleSearch method. Now, when the user clears the search field and searches for an empty string, the repo value is also set to an empty string. If for some reason there's not a login, we only render one component: the SearchForm. When we have a value for login, we'll render all four components.

Now, technically our app has two screens. One screen only displays a search form. The other screen only shows when the search form contains a value, in which case, it shows all four components. We've set ourselves up to mount or unmount components based on user interactivity. Let's say we were looking at the details for

「moonhighway.」If the user empties the search field, then the GitHubUser, UserRepositories, and RepositoryReadme

components are unmounted and will no longer be displayed. But what if these components were in the middle of loading data when they were unmounted?

You can try it out:

1. Throttle the network to「Slow 3G」to have enough time to cause problems

2. Change the value of the search field from「moonhighway」to

「eveporcello」

3. While the data is loading, search for an empty string,「」

These steps will cause the GitHubUser, UserRepositories, and RepositoryReadme to become unmounted while they're in the middle of making fetch requests. Eventually, when there's a response to the fetch request, these components are no longer mounted. Attempting to change state values in an unmounted component will cause the error shown in Figure 8-10.

Figure 8-10. Mounted error

Whenever our users load data over a slow network, these errors can occur. But we can protect ourselves. First, we can create a hook that will tell us whether or not the current component is mounted: export function useMountedRef() {

const mounted = useRef(false);

useEffect(() => {

mounted.current = true;

return () => (mounted.current = false);

});

return mounted;

}

The useMountedRef hook uses a ref. When the component unmounts, state is wiped clean, but refs are still available. The above useEffect doesn't have a dependency array; it's invoked every time a component renders and ensures that the value for the ref is true. Whenever the

component unmounts, the function returned from useEffect is invoked, which changes the value of the ref to false.

Now we can use this hook inside of the RepoReadme component. This will allow us to make sure the component is mounted before applying any state updates:

const mounted = useMountedRef();

const loadReadme = useCallback(async (login, repo) => {

setLoading(true);

const uri = `https://api.github.com/repos/${login}/${repo}/readmè; const { download_url } = await fetch(uri).then(res => res.json()

);

const markdown = await fetch(download_url).then(res => res.text()

);

if (mounted.current) {

setMarkdown(markdown);

setLoading(false);

}

}, []);

Now we have a ref that tells us whether or not the component is mounted. It will take time for both of these requests to finish. When they do, we check to make sure the component is still mounted before calling setMarkdown or setLoading.

Let's add the same logic to our useFetch hook:

const mounted = useMountedRef();

useEffect(() => {

if (!uri) return;

if (!mounted.current) return; setLoading(true);

fetch(uri)

.then(data => {

if (!mounted.current) throw new Error("component is not mounted"); return data;

})

.then(data => data.json())

.then(setData)

.then(() => setLoading(false))

. catch(error => {

if (!mounted.current) return;

setError(error);

});

The useFetch hook is used to make the rest of the fetch requests in our app. In this hook, we compose the fetch request using thenables, chainable .then() functions, instead of async/await. When the fetch is complete, we check to see if the component is mounted in the first

.then callback. If the component is mounted, the data is returned and the rest of the .then functions are invoked. When the component is not mounted, the first .then function throws an error, preventing the rest of the .then functions from executing. Instead, the .catch function is invoked and the new error is passed to that function. The .catch function will check to see if the component is mounted before it tries to invoke setError.

We've successfully canceled our requests. We didn't stop the HTTP

request itself from occurring, but we did protect the state calls we make after the request is resolved. It's always a good idea to test your app under slow network conditions. These bugs will be revealed and eliminated.

Introducing GraphQL

Just like React, GraphQL was designed at Facebook. And, just like React is a declarative solution for composing user interfaces, GraphQL

is a declarative solution for communicating with APIs. When we make parallel data requests, we're attempting to get all the data we need immediately at the same time. GraphQL was designed to do just that.

In order to get data from a GraphQL API, we still need to make an HTTP request to a specific URI. However, we also need to send a query along with the request. A GraphQL query is a declarative description of the data we're requesting. The service will parse this description and will package all the data we're asking for into a single response.

GitHub GraphQL API

In order to use GraphQL in your React application, the backend service you're communicating with needs to be built following GraphQL

specifications. Fortunately, GitHub also exposes a GraphQL API. Most GraphQL services provide a way to explore the GraphQL API. At GitHub, this is called the GraphQL Explorer. In order to use the Explorer, you must sign in with your GitHub account.

The left panel of the Explorer is where we draft our GraphQL query.

Inside of this panel, we could add a query to obtain information about a single GitHub user:

query {

user(login: "moontahoe") {

id

login

name

location

avatarUrl

}

}

This is a GraphQL query. We're asking for information about the GitHub user「moontahoe.」Instead of getting all of the public information available about moontahoe, we only get the data we want: id, login, avatarUrl, name, and location. When we press the Play button on this page, we send this query as an HTTP POST request to https://api.github.com/graphql. All GitHub GraphQL queries are sent to this URI. GitHub will parse this query and return only the data we asked for:

{

"data" : {

"user" : {

"id" : "MDQ6VXNlcjU5NTIwODI=",

"login" : "MoonTahoe",

"name" : "Alex Banks",

"location" : "Tahoe City, CA",

"avatarUrl" : "https://github.com/moontahoe.png"

}

}

}

We can formalize this GraphQL query into a reusable operation named findRepos. Every time we want to find information about a user and their repositories, we could do so by sending a login variable to this query:

query findRepos($login: String!) {

user(login: $login) {

login

name

location

avatar_url: avatarUrl

repositories(first: 100) {

totalCount

nodes {

name

}

}

}

}

Now we've created a formal findRepos query that we can reuse simply by chaining the value of the $login variable. We set this variable using the Query Variables panel shown in Figure 8-11.

Figure 8-11. GitHub GraphQL Explorer

In addition to obtaining details about a user, we're also asking for that user's first hundred repositories. We're asking for the number of repositories returned by the query, the totalCount, along with the

name of each repository. GraphQL only returns the data we ask for. In this case, we'll only get the name for each repository, nothing else.

There's one more change that we made to this query: we used an alias for the avatarUrl. The GraphQL field to obtain a user's avatar is called avatarUrl, but we want that variable to be named avatar_url.

The alias tells GitHub to rename that field in the data response.

GraphQL is a huge topic. We wrote a whole book about it: Learning

GraphQL. We're only scratching the surface here, but GraphQL is

increasingly becoming more of a requirement for any developer. In order to be a successful developer in the 21st century, it's important to understand the fundamentals of GraphQL.

Making a GraphQL Request

A GraphQL request is an HTTP request that contains a query in the body of the request. You can use fetch to make a GraphQL request.

There are also a number of libraries and frameworks that can handle the details of making these types of requests for you. In this next section, we'll see how we can hydrate our applications with GraphQL

data using a library called graphql-request.

NOTE

GraphQL is not restricted to HTTP. It's a specification of how data requests should be made over a network. It can technically work with any network protocol. Additionally, GraphQL is language-agnostic.

First, let's install graphql-request:

npm i graphql-request

GitHub's GraphQL API requires identification to send requests from client applications. In order to complete this next sample, you must obtain a personal access token from GitHub, and this token must be sent with every request.

To obtain a personal access token for GraphQL requests, navigate to Settings > Developer Settings > Personal Access Tokens. On this form, you can create an access token that has specific rights. The token must have the following read access in order to make GraphQL requests: user

public_repo

repo

repo_deployment

repo:status

read:repo_hook

read:org

read:public_key

read:gpg_key

We can use graphql-request to make GraphQL requests from

JavaScript:

import { GraphQLClient } from "graphql-request";

const query = `

query findRepos($login:String!) {

user(login:$login) {

login

name

location

avatar_url: avatarUrl

repositories(first:100) {

totalCount

nodes {

name

}

}

}

}

`;

const client = new GraphQLClient(

"https://api.github.com/graphql",

{

headers: {

Authorization: `Bearer <PERSONAL_ACCESS_TOKEN>`

}

}

);

client

.request(query, { login: "moontahoe" })

.then(results => JSON.stringify(results, null, 2))

.then(console.log)

. catch(console.error);

We send this request using the GraphQLClient constructor from graphql-request. When we create the client, we use the URI for GitHub's GraphQL API: https://api.github.com/graphql. We also send some additional headers that contain our personal access token. This token identifies us and is required by GitHub when using their GraphQL API. We can now use the client to make our GraphQL

requests.

In order to make a GraphQL request, we'll need a query. The query is simply a string that contains the GraphQL query from above. We send the query to the request function along with any variables that the query may require. In this case, the query requires a variable named $login, so we send an object that contains a value for $login in the login field.

Here, we're simply converting the resulting JSON to a string and logging it to the console:

{

"user" : {

"id" : "MDQ6VXNlcjU5NTIwODI=",

"login" : "MoonTahoe",

"name" : "Alex Banks",

"location" : "Tahoe City, CA",

"avatar_url" : "https://avatars0.githubusercontent.com/u/5952082?v=4",

"repositories" : {

"totalCount" : 52,

"nodes" : [

{

"name" : "snowtooth"

},

{

"name" : "Memory"

},

{

"name" : "snowtooth-status"

},

...

]

}

}

}

Just like fetch, client.request returns a promise. Getting this data inside of your React component will feel very similar to fetching data from a route:

export default function App() {

const [login, setLogin] = useState("moontahoe"); const [userData, setUserData] = useState();

useEffect(() => {

client

.request(query, { login })

.then(({ user }) => user)

.then(setUserData)

. catch(console.error);

}, [client, query, login]);

if (!userData) return <p>loading...</p>; return (

<>

<SearchForm value={login} onSearch={setLogin} />

<UserDetails {...userData} />

<p>{userData.repositories.totalCount} - repos</p>

<List

data={userData.repositories.nodes}

renderItem={repo => <span>{repo.name}</span>}

/>

</>

);

}

We make the client.request inside of a useEffect hook. If the client, query, or login changes, the useEffect hook will make another request. Then we'll render the resulting JSON with React, as shown in Figure 8-12.

Figure 8-12. GraphQL app

This example doesn't put care into handling loading and error states, but we can apply everything we learned in the rest of this chapter to GraphQL. React doesn't really care how we get the data. As long as we understand how to work with asynchronous objects like promises within our components, we'll be ready for anything.

Loading data from the internet is an asynchronous task. When we

request data, it takes some time for it to be delivered, and stuff can go wrong. Handling the pending, success, and fail states of a promise within a React component is an orchestration of stateful hooks with the useEffect hook.

We spent much of this chapter covering promises, fetch, and HTTP.

This is because HTTP is still the most popular way to request data from the internet, and promises fit nicely with HTTP requests. Sometimes, you may work with a different protocol like WebSockets. No worries: this is accomplished by working with stateful hooks and useEffect.

Here's a brief example of how we can incorporate socket.io into a custom useChatRoom hook:

const reducer = (messages, incomingMessage) => [

messages,

...incomingMessage

];

export function useChatRoom(socket, messages = []) {

const [status, setStatus] = useState(null); const [messages, appendMessage] = useReducer(

reducer,

messages

);

const send = message => socket.emit("message", message); useEffect(() => {

socket.on("connection", () => setStatus("connected")); socket.on("disconnecting", () =>

setStatus("disconnected")

);

socket.on("message", setStatus);

return () => {

socket.removeAllListeners("connect"); socket.removeAllListeners("disconnect");

socket.removeAllListeners("message");

};

}, []);

return {

status,

messages,

send

};

}

This hook provides an array of chat messages, the websocket connection status, and a function that can be used to broadcast new messages to the socket. All of these values are affected by listeners that are defined in the useEffect hook. When the socket raises connection or disconnecting events, the value for status changes.

When new messages are received, they're appended to the array of messages via the useReducer hook.

In this chapter, we've discussed some techniques for handling asynchronous data in applications. This is a hugely important topic, and in the next chapter, we'll show how Suspense might lead to future changes in this area.