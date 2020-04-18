In the last chapter, we learned about Vue.js components and converted Vuebnb to a component-based architecture. Now that we've done this, we can easily add new pages to our app using Vue Router.

In this chapter, we'll create a home page for Vuebnb, including a gallery of clickable thumbnails that showcase the full set of mock listings.

Topics covered in this chapter:

An explanation of what router libraries are and why they are a critical part of single-page applications

An overview of Vue Router and its main features

Installation and basic configuration of Vue Router

Using the RouterLink and RouterView special components to manage page navigation

Setting up AJAX with Vue to retrieve data from the web service without a page refresh

Using route navigation guards to retrieve data before a new page is loaded

Single-page applications

Most websites are broken up into pages in order to make the information they contain easier to consume. Traditionally this is done with a server/client model, where each page must be loaded from the server with a different URL. To navigate to a new page, the browser must send a request to the URL of that page. The server will send the data back and the browser can unload the existing page and load the new one. For the average internet connection, this process will likely take a few seconds, during which the user must wait for the new page to load.

By using a powerful frontend framework and an AJAX utility, a different model is possible: the browser can load an initial web page, but navigating to new pages will not require the browser to unload the page and load a new one. Instead, any data required for new pages can be loaded asynchronously with AJAX. From a user's perspective, such a website would appear to have pages just like any other, but from a technical perspective, this site really only has one page. Hence the name, Single-Page Application (SPA).

The advantage of the Single-Page Application architecture is that it can create a more seamless experience for the user. Data for new pages must still be retrieved, and will therefore create some small disruption to the user's flow, but this disruption is minimized since the data retrieval can be done asynchronously and JavaScript can continue to run. Also, since SPA pages usually require less data due to the reuse of some page elements, page loading is quicker.

The disadvantage of the SPA architecture is that it makes the client app bulkier due to the added functionality, so gains from speeding up page changes may be negated by the fact that the user must download a large app on the first page load. Also, handling routes adds complexity to the app as multiple states must be managed, URLs must be handled, and a lot of default browser functionality must be recreated in the app.

Routers

If you are going with an SPA architecture and your app design includes multiple pages, you'll want to use a router. A router, in this context, is a library that will mimic browser navigation through JavaScript and various native APIs so that the user gets an experience similar to that of a traditional multi-page app. Routers will typically include functionality to:

Handle navigation actions from within the page

Match parts of the application to routes

Manage the address bar

Manage the browser history

Manage scroll bar behavior

Vue Router

Some frontend frameworks, such as Angular or Ember, include a router library out-of-the-box. The philosophy guiding these frameworks is that the developer is better served with a complete, integrated solution for their SPA.

Others frameworks/libraries, such as React and Vue.js, do not include a router. Instead, you must install a separate library.

In the case of Vue.js, an official router library is available called Vue Router. This library has been developed by the Vue.js core team, so it is optimized for usage with Vue.js and makes full use of fundamental Vue features such as components and reactivity.

With Vue Router, different pages of the application are represented by different components. When you set up Vue Router, you will pass in configuration to tell it which URLs map to which component. Then, when a link is clicked in the app, Vue Router will swap the active component so as to match the new URL, for example:

let routes = [ { path: '/', component: HomePage }, { path: '/about', component: AboutPage }, { path: '/contact', component: ContactPage } ];

Since rendering a component is an almost instantaneous process in normal circumstances, the transition between pages with Vue Router is as well. However, there are asynchronous hooks that can be invoked to give you the opportunity to load new data from the server, if your different pages require it.

Special components

When you install Vue Router, two components are registered globally for use throughout your app: RouterLink and RouterView.

RouterLink is generally used in place of a tags and gives your links access to the special features of Vue Router.

As explained, Vue Router will swap designated page components as a way of mimicking browser navigation. RouterView is the outlet in which this component swap takes place. Like a slot, you put it somewhere in your main page template. For example:

<div id="app"> <header></header> <router-view> // This is where different page components display </router-view> <footer></footer> </div>

Vuebnb routing

It was never a stated goal for Vuebnb to be a single-page application. Indeed, Vuebnb will deviate from pure SPA architecture as we'll see later in the book.

That said, incorporating Vue Router will be very beneficial to the user's experience of navigation in the app, so we'll add it to Vuebnb in this chapter.

Of course, if we're going to add a router, we'll need some extra pages! So far in the project, we've been working on the listing page of Vuebnb, but are yet to start work on the front page of the app. So in addition to installing Vue Router, we will start work on the Vuebnb home page, which displays thumbnails and links to all our mock listings:

Figure 7.1. Front page of Vuebnb

Installing Vue Router

Vue Router is an NPM package and can be installed on the command line:

$ npm i --save-dev vue-router

Let's put our router configuration into a new file, router.js:

$ touch resources/assets/js/router.js

To add Vue Router to our project, we must import the library and then use the Vue.use API method to make Vue compatible with Vue Router. This will give Vue a new configuration property, router, that we can use to connect a new router.

We then create an instance of Vue Router with new VueRouter().

resources/assets/js/router.js:

import Vue from 'vue'; import VueRouter from 'vue-router'; Vue.use(VueRouter); export default new VueRouter();

By exporting our router instance from this new file, we've made it into a module that can be imported in app.js. If we name the imported module router, object destructuring can be used to succinctly connect it to our main configuration object.

resources/assets/js/app.js:

import "core-js/fn/object/assign"; import Vue from 'vue'; import ListingPage from '../components/ListingPage.vue'; import router from './router' var app = new Vue({ el: '#app', render: h => h(ListingPage), router });

Creating routes

The most basic configuration for Vue Router is to provide a routes array, which maps URLs to the corresponding page components. This array will contain objects with at least two properties: path and component.

Note that by page components I'm simply referring to any components that we've designated to represent a page in our app. They are regular components in every other way.

For now, we're only going to have two routes in our app, one for our home page and one for our listing page. The HomePage component doesn't exist yet, so we'll keep its route commented out until we create it.

resources/assets/js/router.js:

import ListingPage from '../components/ListingPage.vue';

export default new VueRouter({ mode: 'history', routes: [ // { path: '/', component: HomePage }, // doesn't exist yet! { path: '/listing/:listing', component: ListingPage } ] });

You'll notice that the path for our ListingPage component contains a dynamic segment :listing so that this route will match paths including /listing/1, listing/2 ... listing/whatever.

There are two modes for Vue Router: hash mode and history mode. Hash mode uses the URL hash to simulate a full URL so that the page won't be reloaded when the hash changes. History mode has real URLs and leverages the history.pushState API to change the URL without causing a page reload. The only downside to history mode is that URLs outside of the app, such as /some/weird/path, can't be handled by Vue and must be handled by the server. That's no problem for us, so we'll use history mode for Vuebnb.

App component

For our router to work, we need to declare a RouterView component somewhere in our page template. Otherwise, there's nowhere for the page components to render.

We'll slightly restructure our app to do this. As it is, the ListingPage component is the root component of the app, as it is at the top of the component hierarchy and loads all other components that we use.

Since we want the router to switch between ListingPage and HomePage based on the URL, we need another component to be above ListingPage in the hierarchy and handle this work. We'll call this new root component App:

Figure 7.2. The relationship between App, ListingPage, and HomePage

Let's create the App component file:

$ touch resources/assets/components/App.vue

The root instance of Vue should render this to the page when it loads, instead of ListingPage.

resources/assets/js/app.js:

import App from '../components/App.vue'; ... var app = new Vue({ el: '#app', render: h => h(App), router });

The following is the content of the App component. I've added the special RouterView component into the template, which is the outlet where either the HomePage or ListingPage component will render.

You'll also notice I've moved the toolbar from app.blade.php into the template of App. This is so the toolbar is in the domain of Vue; before it was outside of the mount point and therefore untouchable by Vue. I've done this so that later we can make the main logo a link to the home page using RouterLink, as this is a convention for most websites. I've moved any toolbar related CSS into the style element as well.

resources/assets/components/App.vue:

<template> <div> <div id="toolbar"> <img class="icon" src="/images/logo.png"> <h1>vuebnb</h1> </div> <router-view></router-view> </div> </template> <style> #toolbar { display: flex; align-items: center; border-bottom: 1px solid #e4e4e4; box-shadow: 0 1px 5px rgba(0, 0, 0, 0.1); } #toolbar .icon { height: 34px; padding: 16px 12px 16px 24px; display: inline-block; } #toolbar h1 { color: #4fc08d; display: inline-block; font-size: 28px; margin: 0; } </style>

With that done, if you now navigate the browser to a URL like /listing/1, you'll see everything looks the same as it did before. However, if you look at Vue Devtools, you'll see the component hierarchy has changed, reflecting the addition of the App component.

There's also an indicator, which tells us that the ListingPage component is the active page component for Vue Router:

Figure 7.3. /listing/1 with Vue Devtools open, showing the component hierarchy

Home page

Let's start work on our home page now. We'll first create a new component, HomePage:

$ touch resources/assets/components/HomePage.vue

For now, let's add placeholder markup to the component before we set it up properly.

resources/assets/components/HomePage.vue:

<template> <div>Vuebnb home page</div> </template>

Be sure to import this component in the router file, and uncomment the route where it's used.

resources/assets/js/router.js:

.... import HomePage from '../components/HomePage.vue'; import ListingPage from '../components/ListingPage.vue'; export default new VueRouter({ mode: 'history', routes: [ { path: '/', component: HomePage }, { path: '/listing/:listing', component: ListingPage } ] });

You might be tempted to test this new route out by putting the URL http://vuebnb.test/ into your browser address bar. You'll find, though, that it results in a 404 error. Remember, we still haven't created a route for this on our server. Although Vue is managing routes from within the app, any address bar navigation requests must be served from Laravel.

Let's now create a link to our home page in the toolbar by using the RouterLink component. This component is like an enhanced a tag. For example, if you give your routes a name property, you can simply use the to prop rather than having to supply an href. Vue will resolve this to the correct URL on render.

resources/assets/components/App.vue:

<div id="toolbar"> <router-link :to="{ name: 'home' }"> <img class="icon" src="/images/logo.png"> <h1>vuebnb</h1> </router-link> </div>

Let's also add name properties to our routes for this to work.

resources/assets/js/app.js:

routes: [ { path: '/', component: HomePage, name: 'home' }, { path: '/listing/:listing', component: ListingPage, name: 'listing' } ]

We'll also have to modify our CSS now since we now have another tag wrapped around our logo. Modify the toolbar CSS rules to match those that follow.

resources/assets/components/App.vue:

<template>...</template> <style> #toolbar { border-bottom: 1px solid #e4e4e4; box-shadow: 0 1px 5px rgba(0, 0, 0, 0.1); }

... #toolbar a { display: flex; align-items: center; text-decoration: none; } </style>

Let's now open a listing page, such as /listing/1. If you inspect the DOM, you'll see that our toolbar now has a new a tag inside it with a correctly resolved link back to the home page:

Figure 7.4. The toolbar is a link back to the home page via the RouterLink element

If you click that link, you'll be taken to the home page! Remember, the page hasn't actually changed; Vue router simply swapped ListingPage for HomePage within RouterView, and also updated the browser URL via the history.pushState API:

Figure 7.5. Home page with Vue Devtools showing component hierarchy

Home route

Let's now add a server-side route for the home page so that we can load our app from the root path. This new route will point to a get_home_web method in our ListingController class.

routes/web.php:

<?php

Route::get('/', 'ListingController@get_home_web'); Route::get('/listing/{listing}', 'ListingController@get_listing_web');

Going to the controller now, we'll make it so the get_home_web method returns the app view, just as it does for the listing web route. The app view includes a template variable model which we use to pass through the initial application state, as set up in Chapter 5, Integrating Laravel and Vue.js with Webpack. For now, just assign an empty array as a placeholder.

app/Http/Controllers/ListingController.php:

public function get_home_web() { return view('app', ['model' => []]); }

With that done, we can now navigate to http://vuebnb.test/ and it will work! When the Vue app is bootstrapped, Vue Router will check the URL value and, seeing that the path is /, will load the HomePage component inside the RouterView outlet for the first rendering of the app.

Viewing the source of this page, it's exactly the same page as we get when we load the listing route since it's the same view, that is, app.blade.php. The only difference is that the initial state is an empty array:

Figure 7.6. Page source of vuebnb.test with empty initial state

Initial state

Just like our listing page, our home page will need initial state. Looking at the finished product, we can see that the home page displays a summary of all our mock listings with a thumbnail image, a title, and short description:

Figure 7.7. Completed home page, focusing on listings

Refactoring

Before we inject the initial state into the home page, let's do a small refactoring of the code including renaming some variables and restructuring some methods. This will ensure that the code semantics reflect the changing requirements and keep our code readable and easy to understand.

Firstly, let's rename our template variable from $model to the more general $data.

resources/views/app.blade.php:

<script type="text/javascript"> window.vuebnb_server_data = "{!! addslashes(json_encode($data)) !!}" </script>

In our listing controller, we're now going to abstract any common logic from our listing route methods into a new helper method called get_listing. In this helper method, we will nest the Listing model inside a Laravel Collection under the listing key. Collection is an array-like wrapper for Eloquent models that offers a bunch of handy methods that we'll be putting to use shortly. get_listing will include logic from the add_image_urls helper method, which can now safely be deleted.

We'll also need to reflect the change to our template variable when we call the view method.

app/Http/Controllers/ListingController.php:

private function get_listing($listing) { $model = $listing->toArray(); for($i = 1; $i <=4; $i++) { $model['image_' . $i] = asset(

'images/' . $listing->id . '/Image_' . $i . '.jpg'

); } return collect(['listing' => $model]); } public function get_listing_api(Listing $listing) { $data = $this->get_listing($listing); return response()->json($data); } public function get_listing_web(Listing $listing) { $data = $this->get_listing($listing); return view('app', ['data' => $data]); }

public function get_home_web()

{

return view('app', ['data' => []]);

}

Finally, we'll need to update our ListingPage component to reflect the new name and structure of the server data we're injecting.

resources/assets/components/ListingPage.vue:

<script> let serverData = JSON.parse(window.vuebnb_server_data); let model = populateAmenitiesAndPrices(serverData.listing); ... </script>

Home page initial state

Using Eloquent ORM, it's trivial to retrieve all our listing entries using the method Listing::all. Multiple Model instances are returned by this method within a Collection object.

Note that we don't need all the fields on the model, for example, amenities, about, and so on are not used in the listing summaries that populate the home page. To ensure our data is as lean as possible, we can pass an array of fields to the Listing::all method that will tell the database to only include those fields explicitly mentioned.

app/Http/Controllers/ListingController.php:

public function get_home_web() { $collection = Listing::all([ 'id', 'address', 'title', 'price_per_night' ]); $data = collect(['listings' => $collection->toArray()]); return view('app', ['data' => $data]); } /* [ "listings" => [ 0 => [ "id" => 1, "address" => "...", "title" => "...", "price_per_night" => "..." ] 1 => [ ... ] ... 29 => [ ... ] ] ] */

Adding the thumbnail

Each mock listing has a thumbnail version of the first image, which can be used for the listing summary. The thumbnail is much smaller than the image we use for the header of the listing page and is ideal for the listing summaries on the home page. The URL for the thumbnail is public/images/{x}/Image_1_thumb.jpg where {x} is the ID of the listing.

Collection objects have a helper method, transform, that we can use to add the thumbnail image URL to each listing. transform accepts a callback closure function that is called once per item, allowing you to modify that item and return it to the collection without fuss.

app/Http/Controllers/ListingController.php:

public function get_home_web() { $collection = Listing::all([ 'id', 'address', 'title', 'price_per_night' ]); $collection->transform(function($listing) { $listing->thumb = asset( 'images/' . $listing->id . '/Image_1_thumb.jpg' ); return $listing; }); $data = collect(['listings' => $collection->toArray()]); return view('app', ['data' => $data]); } /* [ "listings" => [ 0 => [ "id" => 1, "address" => "...", "title" => "...", "price_per_night" => "...", "thumb" => "..." ] 1 => [ ... ] ... 29 => [ ... ] ] ] */

Receiving in the client

With the initial state now ready, let's add it to our HomePage component. Before we can use it though there's an additional aspect we need to consider: the listing summaries are grouped by country. Look again at Figure 7.7 to see how these groups are displayed.

After we've parsed our injected data, let's modify the object so the listings are grouped by country. We can easily create a function to do this, as every listing object has an address property in which the country is always explicitly named, for example, No. 51, Hanzhong Street, Wanhua District, Taipei City, Taiwan 108.

To save you having to write this function, I have supplied one in the helpers module called groupByCountry which can be imported at the top of the component configuration.

resources/assets/components/HomePage.vue:

... <script> import { groupByCountry } from '../js/helpers'; let serverData = JSON.parse(window.vuebnb_server_data); let listing_groups = groupByCountry(serverData.listings); export default { data() { return { listing_groups } } } </script>

We'll now see through Vue Devtools that HomePage has successfully loaded the listing summaries, grouped by country and ready for display:

Figure 7.8. Vue Devtools showing the state of the HomePage component

ListingSummary component

Now that the HomePage component has data available, we can work on displaying it.

To begin with, clear out the existing content of the component and replace it with a div. This div will feature a v-for directive to iterate through each of our listing groups. Since listing_groups is an object with key/value pairs, we'll give our v-for two aliases: group and country, which are the value and key of each object item respectively.

We will interpolate country inside a heading. group will be used in the next section.

resources/assets/components/HomePage.vue:

<template> <div> <div v-for="(group, country) in listing_groups"> <h1>Places in {{ country }}</h1> <div> Each listing will go here </div> </div> </div> </template>

<script>...</script>

This is what the home page will now look like:

Figure 7.9. Iterating the listing summary groups in the HomePage component

Since each listing summary will be of some complexity, we'll create a separate component, ListingSummary, for displaying them:

$ touch resources/assets/components/ListingSummary.vue

Let's declare ListingSummary within our HomePage template. We'll again use a v-for directive to iterate group, an array, creating a new instance of ListingSummary for each member. The data for each member will be bound to a single prop, listing.

resources/assets/components/HomePage.vue:

<template> <div> <div v-for="(group, country) in listing_groups"> <h1>Places in {{ country }}</h1> <div class="listing-summaries"> <listing-summary v-for="listing in group" :key="listing.id" :listing="listing" ></listing-summary> </div> </div> </div> </template> <script> import { groupByCountry } from '../js/helpers';

import ListingSummary from './ListingSummary.vue'; let serverData = JSON.parse(window.vuebnb_server_data); let listing_groups = groupByCountry(serverData.listings); export default { data() { return { listing_groups } }, components: { ListingSummary } } </script>

Let's create some simple content for the ListingSummary component, just to test our approach.

resources/assets/components/ListingSummary.vue:

<template> <div class="listing-summary"> {{ listing.address }} </div> </template> <script> export default { props: [ 'listing' ], } </script>

Refreshing our page, we'll now see this prototype of our listing summaries:

Figure 7.10. Prototype of ListingSummary component

Since this approach is working, let's now complete the structure of the ListingSummary component. To display the thumbnail, we bind it as a background image for a fixed width/height div. We'll also need some CSS rules to get this displaying nicely.

resources/assets/components/ListingSummary.vue:

<template> <div class="listing-summary"> <div class="wrapper"> <div class="thumbnail" :style="backgroundImageStyle"></div> <div class="info title"> <span>{{ listing.price_per_night }}</span> <span>{{ listing.title }}</span> </div> <div class="info address">{{ listing.address }}</div> </div> </div> </template> <script> export default { props: [ 'listing' ], computed: { backgroundImageStyle() { return { 'background-image': `url("${this.listing.thumb}")` } } } } </script> <style> .listing-summary { flex: 0 0 auto; } .listing-summary a { text-decoration: none; } .listing-summary .wrapper { max-width: 350px; display: block; } .listing-summary .thumbnail { width: 350px; height: 250px; background-size: cover; background-position: center; } .listing-summary .info { color: #484848; word-wrap: break-word; letter-spacing: 0.2px; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; } .listing-summary .info.title { padding-top: 5px; font-weight: 700; font-size: 16px; line-height: 24px; } .listing-summary .info.address { font-size: 14px; line-height: 18px; } </style>

After you add that code, your listing summaries will look like this:

Figure 7.11. Complete listing summaries being displayed

We gave each listing summary a fixed width/height so that we could display them in a neat grid. Currently, they're displaying in one tall column, so let's add some CSS flex rules to the HomePage component to get the summaries into rows.

We'll add a class listing-summary-group to the element that wraps the summaries. We'll also add a class home-container to the root div to constrain the width of the page and center the content.

resources/assets/components/HomePage.vue:

<template> <div class="home-container"> <div v-for="(group, country) in listing_groups" class="listing-summary-group" > ... </div> </div> </template> <script>...</script> <style> .home-container { margin: 0 auto; padding: 0 25px; } @media (min-width: 1131px) { .home-container { width: 1080px; } } .listing-summary-group { padding-bottom: 20px; } .listing-summaries { display: flex; flex-direction: row; justify-content: space-between; overflow: hidden; } .listing-summaries > .listing-summary { margin-right: 15px; }

.listing-summaries > .listing-summary:last-child {

margin-right: 0; } </style>

Finally, we'll need to add a rule to prevent the listings from forcing the edge of the document to exceed the viewport. Add this to the main CSS file.

resources/assets/css/style.css:

html, body { overflow-x: hidden; }

With that, we get a nice looking home page:

Figure 7.12. Listing summaries in rows

You'll notice that at full page width, we can only see three listings from each country group. The other seven are hidden by the CSS overflow: hidden rule. Soon, we'll be adding image slider functionality to each group to allow the user to browse through all the listings.

In-app navigation

If we use the address bar of the browser to navigate to the home page, http://vuebnb.test/, it works because Laravel is now serving a page at this route. But, if we navigate to the home page from the listing page, there's no longer any page content:

Figure 7.13. Empty home page after navigating from listing page

We currently don't have any links to the listing page from the home page, but if we did, we'd experience a similar issue.

The reason is that our page components currently get their initial state from the data we've injected into the head of the document. If we navigate to a different page using Vue Router, which doesn't invoke a page refresh, the next page component will have the wrong initial state merged in.

We need to improve our architecture so that when a page is navigated to we check if the model injected into the head matches the current page. To facilitate this, we'll add a path property to the model and check that it matches the active URL. If not, we'll use AJAX to get the right data from the web service:

Figure 7.14. How a page decides what data it needs

If you're interested in reading more about this design pattern, check out the article Avoid This Common Anti-Pattern In Full-Stack Vue/Laravel Apps at https://vuejsdevelopers.com/2017/08/06/vue-js-laravel-full-stack-ajax/.

Adding a path to the model

Let's go to the listing controller and add a path property to the data injected into the head of our view. To do this, we'll add a helper function called add_meta_data which will add the path, as well as some other meta properties in later chapters.

Note that the path of the current route can be determined by the Request object. This object can be declared as the last argument of any route-handling functions and is provided in each request by the service container.

app/Http/Controllers/ListingController.php:

...

private function add_meta_data($collection, $request) { return $collection->merge([ 'path' => $request->getPathInfo() ]); } public function get_listing_web(Listing $listing, Request $request) { $data = $this->get_listing($listing); $data = $this->add_meta_data($data, $request); return view('app', ['data' => $data]); } public function get_home_web(Request $request) { $collection = Listing::all([ 'id', 'address', 'title', 'price_per_night' ]); $collection->transform(function($listing) { $listing->thumb = asset( 'images/' . $listing->id . '/Image_1_thumb.jpg' ); return $listing; }); $data = collect(['listings' => $collection->toArray()]); $data = $this->add_meta_data($data, $request); return view('app', ['data' => $data]); } /* [ "listings" => [ ... ], "path" => "/" ] */

Route navigation guards

Similar to lifecycle hooks, navigation guards allow you to intercept Vue Router navigations at a particular point in their life cycle. These guards can be applied to a specific component, a specific route, or to all routes.

For example, afterEach is the navigation guard called after any route is navigated away from. You might use this hook to store analytics information, for example:

router.afterEach((to, from) => { storeAnalytics(userId, from.path); })

We can use the beforeRouteEnter navigation guard to fetch data from our web service if the data in the head is unsuitable. Consider the following pseudo-code for how we might implement this:

beforeRouteEnter(to, from, next) { if (to !== injectedData.path) { getDataWithAjax.then(data => { applyData(data) }) } else { applyData(injectedData) } next() }

next

An important feature of navigation guards is that they will halt navigation until the next function is called. This allows asynchronous code to be executed before the navigation is resolved:

beforeRouteEnter(to, from, next) { new Promise(...).then(() => { next(); }); }

You can pass false to the next function to prevent a navigation, or you can pass a different route to redirect it. If you don't pass anything, the navigation is considered confirmed.

The beforeRouteEnter guard is a special case. Firstly, this is undefined within it since it is called before the next page component has been created:

beforeRouteEnter(to, from, next) { console.log(this); // undefined }

However, the next function in beforeRouteEnter can accept a callback function as an argument, for example, next(component => { ... }); where component is the page component instance.

This callback is not triggered until the route is confirmed and the component instance has been created. Due to how JavaScript closures work, the callback will have access to the scope of the surrounding code where it was called:

beforeRouteEnter(to, from, next) { var data = { ... } next(component => { component.$data = data; }); }

HomePage component

Let's add beforeRouteEnter to the HomePage component. Firstly, move any logic for retrieving data from the document head into the hook. We then check the path property of the data to see if it matches the current route. If so, we call next and pass a callback function that applies the data to the component's instance. If not, we'll need to use AJAX to get the right data.

resources/assets/components/HomePage.vue:

export default { data() { return { listing_groups: [] }; }, components: { ListingSummary }, beforeRouteEnter(to, from, next) { let serverData = JSON.parse(window.vuebnb_server_data); if (to.path === serverData.path) { let listing_groups = groupByCountry(serverData.listings); next(component => component.listing_groups = listing_groups); } else { console.log('Need to get data with AJAX!') next(false); } } }

I've added listing_groups as a data property. Before, we were applying our data to the component instance as it was created. Now, we're applying the data after the component is created. To set up reactive data, Vue must know the names of the data properties, so we initialize with an empty value and update it when the data needed is available.

Home API endpoint

We'll now implement the AJAX functionality. Before we do, though, we need to add a home page endpoint to our web service.

Let's first add the home API route.

routes/api.php:

...

Route::get('/', 'ListingController@get_home_api');

Looking now at the ListingController class, we'll abstract the bulk of the logic from get_home_web into a new function, get_listing_summaries. We'll then use this function in the get_home_api method and return a JSON response.

app/Http/Controllers/ListingController.php:

private function get_listing_summaries() { $collection = Listing::all([ 'id', 'address', 'title', 'price_per_night' ]); $collection->transform(function($listing) { $listing->thumb = asset( 'images/' . $listing->id . '/Image_1_thumb.jpg' ); return $listing; }); return collect(['listings' => $collection->toArray()]); } public function get_home_web(Request $request) { $data = $this->get_listing_summaries(); $data = $this->add_meta_data($data, $request); return view('app', ['data' => $data]); } public function get_home_api() { $data = $this->get_listing_summaries(); return response()->json($data); }

Axios

To perform AJAX requests to the web service, we'll use the Axios HTTP client, which is included with Laravel's default frontend code. Axios has a very simple API allowing us to make requests to a GET URL like this:

axios.get('/my-url');

Axios is a Promise-based library, so in order to retrieve the response, you can simply chain a then callback:

axios.get('/my-url').then(response => { console.log(response.data); // Hello from my-url });

As the Axios NPM package is already installed, we can go ahead and import the HomePage component. We can then use it to perform the request to the home API endpoint, /api/. In the then callback, we apply the returned data to the component instance exactly as we did with the inlined model.

resources/assets/components/HomePage.vue:

...

import axios from 'axios'; export default { data() { ... }, components: { ... }, beforeRouteEnter (to, from, next) { let serverData = JSON.parse(window.vuebnb_server_data); if (to.path === serverData.path) { let listing_groups = groupByCountry(serverData.listings); next(component => component.listing_groups = listing_groups); } else { axios.get(`/api/`).then(({ data }) => { let listing_groups = groupByCountry(data.listings); next(component => component.listing_groups = listing_groups); }); } } }

And with that, we can now navigate to the home page in two ways, either via the address bar, or by going from a link from the listing page. Either way, we get the right data!

Mixins

If you have any functionality that is common between components, you can put it in a mixin to avoid rewriting the same functionality.

A Vue mixin is an object in the same form as a component configuration object. To use it in a component, declare within an array and assign it to the configuration property mixin. When this component is instantiated, any configuration options of the mixin will be merged with what you've declared on the component:

var mixin = { methods: { commonMethod() { console.log('common method'); } } }; Vue.component('a', { mixins: [ mixin ] }); Vue.component('b', { mixins: [ mixin ] methods: { otherMethod() { ... } } });

You might be wondering what happens if the component configuration has a method or other property that conflicts with the mixin. The answer is that mixins have a merging strategy that determines the priority of any conflicts. Generally, the component's specified configuration will take precedence. The details of the merging strategy are explained in the Vue.js documentation at http://vuejs.org.

Moving the solution to a mixin

Let's generalize the solution for getting the right data to the home page so that we can use it on the listing page as well. To do this, we'll move Axios and the beforeRouteEnter hook from the HomePage component into a mixin that can then be added to both page components:

$ touch resources/assets/js/route-mixin.js

At the same time, let's improve the code by removing the repetition of the next function call. To do this, we'll create a new method, getData, which will be responsible for figuring out where to get the right data for the page and also for getting it. Note that this method will be asynchronous since it may need to wait for AJAX to resolve, so it will return a Promise rather than an actual value. This Promise is then resolved within the navigation guard.

resources/assets/js/route-mixin.js:

import axios from 'axios'; function getData(to) { return new Promise((resolve) => { let serverData = JSON.parse(window.vuebnb_server_data); if (!serverData.path || to.path !== serverData.path) { axios.get(`/api${to.path}`).then(({ data }) => { resolve(data); }); } else { resolve(serverData); } }); } export default { beforeRouteEnter: (to, from, next) => { getData(to).then((data) => { next(component => component.assignData(data)); }); } };

We don't need a polyfill for Promise as that is already supplied in the Axios library.

assignData

You'll notice that within the next callback we call a method on the subject component called assignData, passing the data object as an argument. We'll need to implement the assignData method in any component that uses this mixin. We do it this way so that the component can process the data, if necessary, before it is applied to the component instance. For example, the ListingPage component must process the data via the populateAmenitiesAndPrices helper function.

resources/assets/components/ListingPage.vue:

... import routeMixin from '../js/route-mixin'; export default { mixins: [ routeMixin ], data() { return { title: null, about: null, address: null, amenities: [], prices: [], images: [] } }, components: { ... }, methods: { assignData({ listing }) { Object.assign(this.$data, populateAmenitiesAndPrices(listing)); }, openModal() { this.$refs.imagemodal.modalOpen = true; } } }

We'll also need to add assignData to the HomePage component.

resources/assets/components/HomePage.vue:

<script> import { groupByCountry } from '../js/helpers'; import ListingSummary from './ListingSummary.vue'; import axios from 'axios'; import routeMixin from '../js/route-mixin'; export default { mixins: [ routeMixin ], data() { ... }, methods: { assignData({ listings }) { this.listing_groups = groupByCountry(listings); }, }, components: { ... } } </script>

Linking to the listing page

The above should work but we can't test it since there are not yet any in-app links to the listing page!

Each of our ListingSummary instances represents a single listing, and should therefore be a clickable link to the page for that listing. Let's use the RouterLink component to achieve this. Note that the object we bind to the to prop includes the name of the route as well as a params object which includes a value for the dynamic segment of the route, the listing ID.

resources/assets/components/ListingSummary.vue:

<div class="listing-summary"> <router-link :to="{ name: 'listing', params: { listing: listing.id } }"> <div class="wrapper"> <div class="thumbnail" :style="backgroundImageStyle"></div> <div class="info title"> <span>{{ listing.price_per_night }}</span> <span>{{ listing.title }}</span> </div> <div class="info address">{{ listing.address }}</div> </div> </router-link> </div>

With that done, the listing summaries will now be links. Clicking from one to the listing page, we see this:

Figure 7.15. Successful AJAX call after navigating to listing page

We can see in Figure 7.15 that the AJAX call to the listing API was successful and returned the data we wanted. If we also look at the Vue Devtools tab, as well as the Dev Tools console, we can see the correct data in our component instance. The problem is that we now have an unhandled 404 error for the header image:

Figure 7.16. Dev Tools console showing error

The reason for this is that the component's first render occurs before the callback in the next hook is called. This means that the initialization values for the component data are used in the first render.

resources/assets/components/ListingPage.vue:

data() { return { title: null, about: null, address: null, amenities: [], prices: [], images: [] } },

In the HeaderImage declaration, we bind the first image like this: :image-url="images[0]". Since the array is initially empty, this will be an undefined value and results in the unhandled error.

The explanation is complex, but the fix is easy: just add a v-if to header-image, ensuring it won't render until valid data is available.

resources/assets/components/ListingPage.vue:

<header-image v-if="images[0]" :image-url="images[0]" @header-clicked="openModal" ></header-image>

Scroll behavior

Another aspect of website navigation that the browser automatically manages is scroll behavior. For example, if you scroll to the bottom of a page, then navigate to a new page, the scroll position is reset. But if you return to the previous page, the scroll position is remembered by the browser, and you're taken back to the bottom.

The browser can't do this when we've hijacked navigation with Vue Router. So, when you scroll to the bottom of the Vuebnb home page and click a listing in Cuba, let's say, the scroll position is unchanged when the listing page component is loaded. This feels really unnatural to the user, who would expect to be taken to the top of the new page:

Figure 7.17. Scroll position issue after navigating with Vue Router

Vue Router has a scrollbehavior method that allows you to adjust where the page is scrolled when you change routes by simply defining the x and y positions of the horizontal and vertical scroll bars. To keep it simple, and yet to still keep the UX natural, let's make it so we are always at the top of the page when a new page is loaded.

resources/assets/js/router.js:

export default new VueRouter({ mode: 'history', routes: [ ... ], scrollBehavior (to, from, savedPosition) { return { x: 0, y: 0 } } });

Adding a footer

To improve the design of Vuebnb, let's add a footer to the bottom of each page. We'll make it a reusable component, so let's begin by creating that:

$ touch resources/assets/components/CustomFooter.vue

Here is the markup. For now, it's just a stateless component.

resources/assets/js/CustomFooter.vue:

<template> <div id="footer"> <div class="hr"></div> <div class="container"> <p> <img class="icon" src="/images/logo_grey.png"> <span>

<strong>Vuebnb</strong>. A full-stack Vue.js and Laravel demo app

</span> </p> </div> </div> </template> <style> #footer { margin-bottom: 3em; } #footer .icon { height: 23px; display: inline-block; margin-bottom: -6px; } .hr { border-bottom: 1px solid #dbdbdb; margin: 3em 0; } #footer p { font-size</span>: 15px; color: #767676 !important;

display: flex; }

#footer p img {

padding-right: 6px;

} </style>

Let's add the footer to the App component, just below the RouterView where the pages are output.

resources/assets/js/App.vue:

<template> <div> <div id="toolbar">...</div> <router-view></router-view> <custom-footer></custom-footer> </div> </template> <script> import CustomFooter from './CustomFooter.vue'; export default { components: { CustomFooter } } </script> <style>...</style>

Here's how it looks on the listing page:

Figure 7.18. Custom footer on listing page

Now here's how it looks on the home page. It doesn't look as good because the text is not aligned left as you'd expect. This is because the container constraints used on this page are different to the .container class we've added to the footer:

Figure 7.19. Custom footer on home page

In fact, .container was specifically designed for the listing page, while .home-container was designed for the home page. To fix this, and to make things less confusing, let's firstly rename the .container class to .listing-container. You'll also need to update the ListingPage component to ensure it's using this new class name.

Secondly, let's move .home-container to the main CSS file as well, since we'll start to use it globally as well.

resources/assets/css/style.css:

.listing-container { margin: 0 auto; padding: 0 12px; } @media (min-width: 744px) { .listing-container { width: 696px; } } .home-container { margin: 0 auto; padding: 0 25px; } @media (min-width: 1131px) { .home-container { width: 1080px; } }

Now we have .home-container and .listing-container as two possible containers for our custom-footer component. Let's dynamically select the class depending on the route, so the footer is always correctly aligned.

The route object

The route object represents the state of the currently active route and can be accessed inside the root instance, or a component instance, as this.$route. This object contains parsed information of the current URL and the route records matched by the URL:

created() { console.log(this.$route.fullPath); // /listing/1 console.log(this.$route.params); // { listing: "1" } }

Dynamically selecting the container class

In order to select the correct container class in custom-footer, we can get the name of the current route from the route object, and use that in a template literal.

resources/assets/components/CustomFooter.vue:

<template> <div id="footer"> <div class="hr"></div> <div :class="containerClass"> <p>...</p> </div> </div> </template> <script> export default { computed: { containerClass() { // this.$route.name is either 'home' or 'listing' return `${this.$route.name}-container`; } } } </script> <style>...</style>

Now the footer will use .home-container when displayed on the home page:

Figure 7.20. Custom footer on home page with the correct container class

Listing summary image slider

On our home page, we need to make it so that a user can see more than just three of the possible 10 listings for each country. To do this, we will turn each listing summary group into an image slider.

Let's create a new component to house each listing summary group. We'll then add arrowheads to the sides of this component, allowing the user to easily step through its listings:

$ touch resources/assets/components/ListingSummaryGroup.vue

We'll now abstract the markup and logic for displaying listing summaries from HomePage into this new component. Each group will need to know the name of the country and the included listings, so we'll add this data as props.

resources/assets/components/ListingSummaryGroup.vue:

<template> <div class="listing-summary-group"> <h1>Places in {{ country }}</h1> <div class="listing-summaries"> <listing-summary v-for="listing in listings" :key="listing.id" :listing="listing" ></listing-summary> </div> </div> </template> <script> import ListingSummary from './ListingSummary.vue'; export default { props: [ 'country', 'listings' ], components: { ListingSummary } } </script> <style> .listing-summary-group { padding-bottom: 20px; } .listing-summaries { display: flex; flex-direction: row; justify-content: space-between; overflow: hidden; } .listing-summaries > .listing-summary { margin-right: 15px; } .listing-summaries > .listing-summary:last-child { margin-right: 0; } </style>

Back in the HomePage, we will declare the ListingSummaryGroup with a v-for, iterating over each country group.

resources/assets/components/HomePage.vue:

<template> <div class="home-container"> <listing-summary-group v-for="(group, country) in listing_groups" :key="country" :listings="group" :country="country" class="listing-summary-group" ></listing-summary-group> </div> </template> <script> import routeMixin from '../js/route-mixin'; import ListingSummaryGroup from './ListingSummaryGroup.vue'; import { groupByCountry } from '../js/helpers'; export default { mixins: [ routeMixin ], data() { return { listing_groups: [] }; }, methods: { assignData({ listings }) { this.listing_groups = groupByCountry(listings); } }, components: { ListingSummaryGroup } } </script>

Most developers will use the terms image carousel and image slider interchangeably. In this book, I make a slight distinction, a carousel contains a single image that gets completely switched out with another, while a slider shifts the position of images, with several visible at once.

Adding the slider

We'll now add the slider functionality to ListingSummaryGroup. To do this, we'll reuse the CarouselControl component we made back in Chapter 6, Composing Widgets with Vue.js Components. We'll want to display one on either side of the group, so let's put them into the template, remembering to declare the dir attribute. We'll also add some structural markup and CSS for displaying the controls.

resources/assets/components/ListingSummaryGroup.vue:

<template> <div class="listing-summary-group"> <h1>Places in {{ country }}</h1> <div class="listing-carousel"> <div class="controls"> <carousel-control dir="left"></carousel-control> <carousel-control dir="right"></carousel-control> </div> <div class="listing-summaries-wrapper"> <div class="listing-summaries"> <listing-summary v-for="listing in listings" :listing="listing" :key="listing.id" ></listing-summary> </div> </div> </div> </div> </template> <script> import ListingSummary from './ListingSummary.vue'; import CarouselControl from './CarouselControl.vue'; export default { props: [ 'country', 'listings' ], components: { ListingSummary, CarouselControl } } </script> <style> ... .listing-carousel { position: relative; } .listing-carousel .controls { display: flex; justify-content: space-between; position: absolute; top: calc(50% - 45px); left: -45px; width: calc(100% + 90px); } .listing-carousel .controls .carousel-control{ color: #c5c5c5; font-size: 1.5rem; cursor: pointer; } .listing-summaries-wrapper { overflow: hidden; } </style>

After adding this code, your home page will look like this:

Figure 7.21. Carousel controls on listing summary groups

Translate

In order to shift our listing summaries in response to the carousel controls being clicked, we will use a CSS transform called translate. This moves an affected element from its current position by an amount specified in pixels.

The total width of each listing summary is 365px (350px fixed width plus 15px margin). This means if we move our group to the left by 365px, it will give the effect of shifting the position of all images by one. You can see here I've added the translate as inline styling to test if it works. Note that we translate in a negative direction to get the group to move to the left:

Figure 7.22. Listing group shifted to the left by using translate

By binding inline style to the element with the listing-summary class, we can control the translate from JavaScript. Let's do this via a computed property so we can calculate the translate amount dynamically.

resources/assets/components/ListingSummaryGroup.vue:

<template> <div class="listing-summary-group"> <h1>Places in {{ country }}</h1> <div class="listing-carousel"> <div class="controls">...</div> <div class="listing-summaries" :style="style"> <listing-summary...>...</listing-summary> </div> </div> </div> </template> <script> export default { props: [ 'country', 'listings' ], computed: { style() { return { transform: `translateX(-365px)` } } }, components: { ... } } </script>

Now all of our summary groups will be shifted:

Figure 7.23. Shifted listing groups with translate controlled by JavaScript

The problem evident in Figure 7.23 is that we can only see three images at once and that they're overflowing out of the container into the other parts of the page.

To fix this, we'll move the CSS rule overflow: hidden from listing-summaries to listing-summaries-wrapper.

resources/assets/components/ListingSummaryGroup.vue:

... .listing-summaries-wrapper { overflow: hidden; } .listing-summaries { display: flex; flex-direction: row; justify-content: space-between; } ...

Carousel controls

We now need the carousel controls to change the value of the translate. To do so, let's add a data property, offset, to ListingSummaryGroup. This will track how many images we've shifted along, that is, it will start at zero, and go up to a maximum of seven (not 10 because we don't want to shift so far along that all of the images are off-screen).

We'll also add a method change, which will serve as an event handling function for the custom event that the carousel control components emit. This method accepts one argument, val, which will either be -1 or 1, depending on whether the left or right carousel control was triggered.

change will step the value of offset, which is then multiplied by the width of each listing (365px) to calculate the translate.

resources/assets/components/ListingSummaryGroup.vue:

...

const rowSize = 3; const listingSummaryWidth = 365; export default { props: [ 'country', 'listings' ], data() { return { offset: 0 } }, methods: { change(val) { let newVal = this.offset + parseInt(val); if (newVal >= 0 && newVal <= this.listings.length - rowSize) { this.offset = newVal; } } }, computed: { style() { return { transform: `translateX(${this.offset * -listingSummaryWidth}px)` } } }, components: { ... } }

Lastly, we must use a v-on directive in the template to register a listener for the change-image event of the CarouselControl components.

resources/assets/components/ListingSummaryGroup.vue:

<div class="controls"> <carousel-control dir="left" @change-image="change"></carousel-control>

<carousel-control dir="right" @change-image="change"></carousel-control> </div>

With that done, we have a working image slider for each listing group!

Finishing touches

There are two more small features to add to these image sliders to give Vuebnb users the best possible experience. Firstly, let's add a CSS transition to animate the translate change over a period of half a second and give a nice sliding effect.

resources/assets/components/ListingSummaryGroup.vue:

.listing-summaries { display: flex; flex-direction: row; justify-content: space-between; transition: transform 0.5s; }

Sadly you can't see the effects of this in a book, so you'll have to try it for yourself!

Finally, unlike our image carousel, these sliders are not continuous; they have a minimum and maximum value. Let's hide the appropriate arrow if that minimum or maximum is reached. For example, when the sliders load, the left arrow should be hidden because the user cannot decrement the offset further below zero.

To do this, we'll use style bindings to dynamically add a visibility: hidden CSS rule.

resources/assets/components/ListingSummaryGroup.vue:

<div class="controls"> <carousel-control dir="left" @change-image="change" :style="leftArrowStyle" ></carousel-control> <carousel-control dir="right" @change-image="change" :style="rightArrowStyle" ></carousel-control> </div>

And the computed properties.

resources/assets/components/ListingSummaryGroup.vue:

computed: { ... leftArrowStyle() { return { visibility: (this.offset > 0 ? 'visible' : 'hidden') } }, rightArrowStyle() { return { visibility: ( this.offset < (this.listings.length - rowSize) ? 'visible' : 'hidden' ) } } }

With that done, we can see the left arrow is hidden when the page loads, as expected:

Figure 7.24. Hidden left arrow on page load

Summary

In this chapter, we learned how router libraries work and why they are a crucial addition to SPAs. We then got familiar with the key features of Vue Router including the route object, navigation guards, and the RouterLink and RouterView special components.

Putting this knowledge into practice, we installed Vue Router and configured it for use in our app. We then built a home page for Vuebnb, including a gallery of listing summaries organized within image sliders.

Finally, we implemented an architecture for correctly matching pages with either available local data or new data retrieved from the web service via AJAX.

Now that we have a substantial number of components in our app, many of which communicate data between one another, it's time to investigate another key Vue.js tool: Vuex. Vuex is a Flux-based library that offers a superior way of managing application state.

Managing Your Application State with Vuex

