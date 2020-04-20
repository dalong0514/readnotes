# 0801. Managing Your Application State with Vuex

In the last chapter, you learned how Vue Router can be used to add virtual pages to a Vue.js single-page app. We will now add components to Vuebnb that share data across pages and therefore can't rely on transient local state. To do this, we will utilize Vuex, a Flux-inspired library for Vue.js that offers a robust means of managing global application state.

Topics covered in this chapter: 1) An introduction to the Flux application architecture and why it is useful for building user interfaces. 2) An overview of Vuex and its key features, including state and mutations. 3) How to install Vuex and set up a global store that can be accessed by Vue.js components. 4) How Vuex allows for superior debugging with Vue Devtools via mutation logging and time-travel debugging. 5) The creation of a save feature for Vuebnb listings and a saved listings page. 6) Moving page state into Vuex to minimize unnecessary data retrieval from the server.

## 01. Flux application architecture

Imagine you've developed a multi-user chat app. The interface has a user list, private chat windows, an inbox with chat history and a notification bar to inform users of unread messages.

Millions of users are chatting through your app on a daily basis. However, there are complaints about an annoying problem: the notification bar of the app will occasionally give false notifications; that is, a user will be notified of a new unread message, but when they check to see what it is, it's just a message they've already seen.

What I've described is a real scenario that Facebook developers had with their chat system a few years ago. The process of solving this inspired their developers to create an application architecture they named Flux. Flux forms the basis of Vuex, Redux and other similar libraries.

Facebook developers struggled with this zombie notification bug for some time. They eventually realized that its persistent nature was more than a simple bug; it pointed to an underlying flaw in the architecture of the app.

The flaw is most easily understood in the abstract: when you have multiple components in an application that share data, the complexity of their interconnections will increase to a point where the state of the data is no longer predictable or understandable. When bugs like the one described inevitably arise, the complexity of the app data makes them near impossible to resolve:

Figure 8.1. The complexity of communication between components increases with every extra component

Flux is not a library. You can't go to GitHub and download it. Flux is a set of guiding principles that describe a scalable frontend architecture that sufficiently mitigates this flaw. It is not just for a chat app, but for any complex UI with components which share state, like Vuebnb.

Let's now explore the guiding principles of Flux.

Principle #1 – Single source of truth

Components may have local data that only they need to know about. For example, the position of the scroll bar in the user list component is probably of no interest to other components:

Vue.component('user-list', { data() { scrollPos: ... } });

But any data that is to be shared between components, for example application data, needs to be kept in a single place, separate from the components that use it. This location is referred to as the store. Components must read application data from this location and not keep their own copy to prevent conflict or disagreement:

Figure 8.2. Centralized data simplifies application state

Principle #2 – Data is read-only

Components can freely read data from the store. But they cannot change data in the store, at least not directly.

Instead, they must inform the store of their intent to change the data and the store will be responsible for making those changes via a set of defined functions called mutator methods.

Why this approach? If we centralize the data-altering logic then we don't have to look far if there are inconsistencies in the state. We're minimizing the possibility that some random component (possibly in a third party module) has changed the data in an unexpected fashion:

Figure 8.3. State is read-only. Mutator methods are used to write to the store

Principle #3 – Mutations are synchronous

It's much easier to debug state inconsistencies in an app that implements the above two principles in its architecture. You could log commits and observe how the state changes in response (which automatically happens with Vue Devtools, as we'll see).

But this ability would be undermined if our mutations were applied asynchronously. We'd know the order our commits came in, but we would not know the order in which our components committed them. Synchronous mutations ensure state is not dependent on the sequence and timing of unpredictable events.

Vuex

Vuex (usually pronounced veweks) is the official Vue.js implementation of the Flux architecture. By enforcing the principles described previously, Vuex keeps your application data in a transparent and predictable state even when that data is being shared across many components.

Vuex includes a store with state and mutator methods, and will reactively update any components that are reading data from the store. It also allows for handy development features like hot module reloading (updating modules in a running application) and time-travel debugging (stepping back through mutations to trace bugs).

In this chapter, we will add a save feature to our Vuebnb listings so that a user can keep track of the listings that they like best. Unlike other data in our app so far, the saved state must persist across pages; for example, when a user changes from one page to another, the app must remember which items the user has already saved. We will use Vuex to achieve this:

Figure 8.4. Saved state is available to all page components

Installing Vuex

Vuex is an NPM package that can be installed from the command line:

$ npm i --save-dev vuex

We will put our Vuex configuration into a new module file store.js:

$ touch resources/assets/js/store.js

We need to import Vuex in this file and, like Vue Router, install it with Vue.use. This gives special properties to Vue that make it compatible with Vuex, such as allowing components to access the store via this.$store.

resources/assets/js/store.js:

import Vue from 'vue'; import Vuex from 'vuex'; Vue.use(Vuex); export default new Vuex.Store();

We will then import the store module in our main app file, and add it to our Vue instance.

resources/assets/js/app.js:

... import router from './router';

import store from './store'; var app = new Vue({ el: '#app', render: h => h(App), router, store });

Save feature

As mentioned, we'll be adding a save feature to our Vuebnb listings. The UI of this feature is a small, clickable icon that is overlaid on the top right of a listing summary's thumbnail image. It acts similarly to a checkbox, allowing the user to toggle the saved status of any particular listing:

Figure 8.5. The save feature shown on listing summaries

The save feature will also be added as a button in the header image on the listing page:

Figure 8.6. The save feature shown on the listing page

ListingSave component

Let's begin by creating the new component:

$ touch resources/assets/components/ListingSave.vue

The template of this component will include a Font Awesome heart icon. It will also include a click handler which will be used to toggle the saved state. Since this component will always be a child of a listing or listing summary, it will receive a listing ID as a prop. This prop will be used shortly to save the state in Vuex.

resources/assets/components/ListingSave.vue:

<template> <div class="listing-save" @click.stop="toggleSaved()"> <i class="fa fa-lg fa-heart-o"></i> </div> </template> <script> export default { props: [ 'id' ], methods: { toggleSaved() { // Implement this } } } </script> <style> .listing-save { position: absolute; top: 20px; right: 20px; cursor: pointer; } .listing-save .fa-heart-o { color: #ffffff; } </style>

Note that the click handler has a stop modifier. This modifier prevents the click event from bubbling up to ancestor elements, especially any anchor tags which might trigger a page change!

We'll now add ListingSave to the ListingSummary component. Remember to pass the listing's ID as a prop. While we're at it, let's add a position: relative to the .listing-summary class rules so that ListingSave can be positioned absolutely against it.

resources/assets/components/ListingSummary.vue:

<template> <div class="listing-summary"> <router-link :to="{ name: 'listing', params: {listing: listing.id}}"> ... </router-link> <listing-save :id="listing.id"></listing-save> </div> </template> <script> import ListingSave from './ListingSave.vue'; export default { ... components: { ListingSave } } </script> <style> .listing-summary { ... position: relative; } ... @media (max-width: 400px) { .listing-summary .listing-save { left: 15px; right: auto; } } </style>

With that done, we will now see the ListingSave heart icon rendered on each summary:

Figure 8.7. The ListingSave component within ListingSummary components

Saved state

The ListingSave component does not have any local data; we will instead keep any saved listings in our Vuex store. To do this, we will create an array in the store called saved. Each time the user toggles the saved state of a listing its ID will be either added or removed from this array.

To begin, let's add a state property to our Vuex store. This object will hold any data we want to be globally available to the components of our app. We will add the saved property to this object and assign it an empty array.

resources/assets/js/store.js:

...

export default new Vuex.Store({ state: { saved: [] } });

Mutator method

We created the stub for a toggleSaved method in our ListingSave component. This method should add or remove the listing's ID from the saved state in the store. Components can access the store as this.$store. More specifically, the saved array can be accessed at this.$store.state.saved.

resources/assets/components/ListingSave.vue:

methods: { toggleSaved() { console.log(this.$store.state.saved); /* Currently an empty array. [] */ } }

Remember that in the Flux architecture state is read-only. That means we cannot directly modify saved from a component. Instead, we must create a mutator method in the store which does the modification for us.

Let's create a mutations property in our store configuration, and add a function property toggleSaved. Vuex mutator methods receive two arguments: the store state and a payload. This payload can be anything you want to pass from the component to the mutator. For the current case, we will send the listing ID.

The logic for toggleSaved is to check if the listing ID is already in the saved array and if so, remove it, or if not, add it.

resources/assets/js/store.js:

export default new Vuex.Store({ state: { saved: [] }, mutations: { toggleSaved(state, id) { let index = state.saved.findIndex(saved => saved === id); if (index === -1) { state.saved.push(id); } else { state.saved.splice(index, 1); } } } });

We now need to commit this mutation from ListingSave. Commit is Flux jargon that is synonymous with call or trigger. A commit looks like a custom event with the first argument being the name of the mutator method and the second being the payload.

resources/assets/components/ListingSave.vue:

export default { props: [ 'id' ], methods: { toggleSaved() { this.$store.commit('toggleSaved', this.id); } } }

The main point of using mutator methods in the store architecture is that state is changed consistently. But there is an additional benefit: we can easily log these changes for debugging. If you check the Vuex tab in Vue Devtools after clicking one of the save buttons, you will see an entry for that mutation:

Figure 8.8: Mutation log

Each entry in the log can tell you the state after the change was committed, as well as the particulars of the mutation.

If you double-click a logged mutation, Vue Devtools will revert the state of the app to what it was directly after that change. This is called time-travel debugging and can be useful for fine-grained debugging.

Changing the icon to reflect the state

Our ListingSave component's icon will appear differently, depending on whether or not the listing is saved; it will be opaque if the listing is saved, and transparent if it is not. Since the component doesn't store its state locally, we need to retrieve state from the store to implement this feature.

Vuex store state should generally be retrieved via a computed property. This ensures that the component is not keeping its own copy, which would violate the single source of truth principle, and that the component is re-rendered when the state is mutated by this component or another. Reactivity works with Vuex state, too!

Let's create a computed property isListingSaved, which will return a Boolean value reflecting whether or not this particular listing has been saved.

resources/assets/components/ListingSave.vue:

export default { props: [ 'id' ], methods: { toggleSaved() { this.$store.commit('toggleSaved', this.id); } }, computed: { isListingSaved() { return this.$store.state.saved.find(saved => saved === this.id); } } }

We can now use this computed property to change the icon. Currently we're using the Font Awesome icon fa-heart-o. This should represent the unsaved state. When the listing is saved we should instead use the icon fa-heart. We can implement this with a dynamic class binding.

resources/assets/components/ListingSave.vue:

<template> <div class="listing-save" @click.stop="toggleSaved()"> <i :class="classes"></i> </div> </template> <script> export default { props: [ 'id' ], methods: { ... }, computed: { isListingSaved() { ...}, classes() { let saved = this.isListingSaved; return { 'fa': true, 'fa-lg': true, 'fa-heart': saved, 'fa-heart-o': !saved } } } } </script> <style> ... .listing-save .fa-heart { color: #ff5a5f; } </style>

Now the user can visually identify which listings have been saved and which haven't. Thanks to reactive Vuex data, the icon will instantly be updated when a change to the saved state is made from anywhere in the app:

Figure 8.9. The ListingSave icon will change depending on the state

Adding to ListingPage

We also want the save feature to appear on the listing page. It will go inside the HeaderImage component alongside the View Photos button so that, like with the listing summaries, the button is overlaid on the listing's main image.

resources/assets/components/HeaderImage.vue:

<template> <div class="header"> <div

class="header-img"

:style="headerImageStyle"

@click="$emit('header-clicked')"

> <listing-save :id="id"></listing-save> <button class="view-photos">View Photos</button> </div> </div> </template> <script> import ListingSave from './ListingSave.vue'; export default { computed: { ... }, props: ['image-url', 'id'], components: { ListingSave } } </script> <style>...</style>

Note that HeaderImage does not have the listing ID in its scope, so we'll have to pass this down as a prop from ListingPage. id is not currently a data property of ListingPage either, but, if we declare it, it will simply work.

This is because the ID is already a property of the initial state/AJAX data the component receives, therefore id will automatically be populated by the Object.assign when the component is loaded by the router.

resources/assets/components/ListingPage.vue:

<template> <div> <header-image v-if="images[0]" :image-url="images[0]" @header-clicked="openModal" :id="id" ></header-image> ... </div> </template> <script> ... export default { data() { ... id: null }, methods: { assignData({ listing }) { Object.assign(this.$data, populateAmenitiesAndPrices(listing)); }, ... }, ... } </script>

<style>...</style>

With that done, the save feature will now appear on the listing page:

Figure 8.10. The listing save feature on the listing page

If you save a listing via the listing page, then return to the home page, the equivalent listing summary will be saved. This is because our Vuex state is global and will persist across page changes (though not page refreshes...yet).

Making ListingSave a button

As it is, the ListingSave feature appears too small in the listing page header and will be easily overlooked by a user. Let's make it a proper button, similar to the View Photos button in the bottom left of the header.

To do this, we'll modify ListingSave to allow parent components to send a prop button. This Boolean prop will indicate if the component should include a button element wrapped around the icon or not.

The text for this button will be a computed property message which will change from Save to Saved depending on the value of isListingSaved.

resources/assets/components/ListingSave.vue:

<template> <div class="listing-save" @click.stop="toggleSaved()"> <button v-if="button"> <i :class="classes"></i> {{ message }} </button> <i v-else :class="classes"></i> </div> </template> <script> export default { props: [ 'id', 'button' ], methods: { ... }, computed: { isListingSaved() { ... }, classes() { ... }, message() { return this.isListingSaved ? 'Saved' : 'Save'; } } } </script> <style> ... .listing-save i { padding-right: 4px; } .listing-save button .fa-heart-o { color: #808080; } </style>

We will now set the button prop to true within HeaderImage. Even though the value is not dynamic, we use a v-bind to ensure the value is interpreted as a JavaScript value, not a string.

resources/assets/components/HeaderImage.vue:

<listing-save :id="id" :button="true"></listing-save>

With that, the ListingSave will appear as a button on our listing pages:

Figure 8.11. The listing save feature appears as a button on the listing page

Moving page state into the store

Now that the user can save any listings that they like, we will need a saved page where they can view those saved listings together. We will build this new page shortly, and it will look like this:

Figure 8.12: Saved page

Implementing the saved page will require an enhancement to our app architecture, however. Let's do a quick recap of how data is retrieved from the server to understand why.

All the pages in our app require a route on the server to return a view. This view includes the data for the relevant page component inlined in the document head. Or, if we navigate to that page via in-app links, an API endpoint will instead supply that same data. We set up this mechanism in Chapter 7, Building A Multi-Page App With Vue Router.

The saved page will require the same data as the home page (the listing summary data), as the saved page is really just a slight variation on the home page. It makes sense, then, to share data between the home page and saved page. In other words, if a user loads Vuebnb from the home page, then navigates to the saved page, or vice versa, it would be a waste to load the listing summary data more than once.

Let's decouple our page state from our page components and move it into Vuex. That way it can be used by whichever page needs and it and avoid unnecessary reloading:

Figure 8.13. Page state in store

State and mutator methods

Let's add two new state properties to our Vuex store: listings and listing_summaries. These will be arrays that store our listings and listing summaries respectively. When the page first loads, or when the route changes and the API is called, the loaded data will be put into these arrays rather than being assigned directly to the page components. The page components will instead retrieve this data from the store.

We'll also add a mutator method, addData, for populating these arrays. It will accept a payload object with two properties: route and data. route is the name of the route, for example, listing, home, and so on. data is the listing or listing summary data retrieved from the document head or the API.

resources/assets/js/store.js:

import Vue from 'vue'; import Vuex from 'vuex'; Vue.use(Vuex); export default new Vuex.Store({ state: { saved: [], listing_summaries: [], listings: [] }, mutations: { toggleSaved(state, id) { ... }, addData(state, { route, data }) { if (route === 'listing') { state.listings.push(data.listing); } else { state.listing_summaries = data.listings; } } } });

Router

The logic for retrieving page state is in the mixin file route-mixin.js. This mixin adds a beforeRouteEnter hook to a page component which applies the page state to the component instance when it becomes available.

Now that we're storing page state in Vuex we will utilize a different approach. Firstly, we won't need a mixin anymore; we'll put this logic into router.js now. Secondly, we'll use a different navigation guard, beforeEach. This is not a component hook, but a hook that can be applied to the router itself, and it is triggered before every navigation.

You can see in the following code block how I've implemented this in router.js. Note that before next() is called we commit the page state to the store.

resources/assets/js/router.js:

...

import axios from 'axios'; import store from './store'; let router = new VueRouter({ ... }); router.beforeEach((to, from, next) => { let serverData = JSON.parse(window.vuebnb_server_data); if (!serverData.path || to.path !== serverData.path) { axios.get(`/api${to.path}`).then(({data}) => { store.commit('addData', {route: to.name, data}); next(); }); } else { store.commit('addData', {route: to.name, data: serverData}); next(); } }); export default router;

With that done, we can now delete the route mixin:

$ rm resources/assets/js/route-mixin.js

Retrieving page state from Vuex

Now that we've moved page state into Vuex we'll need to modify our page components to retrieve it. Starting with ListingPage, the changes we must make are:

Remove local data properties.

Add a computed property listing. This will find the right listing data from the store based on the route.

Remove the mixin.

Change template variables so they're properties of listing: an example is {{ title }} , which will become {{ listing.title }}. Unfortunately, all variables are now properties of listing which makes our template slightly more verbose.

resources/assets/components/ListingPage.vue:

<template> <div> <header-image v-if="listing.images[0]" :image-url="listing.images[0]" @header-clicked="openModal" :id="listing.id" ></header-image> <div class="listing-container"> <div class="heading"> <h1>{{ listing.title }}</h1> <p>{{ listing.address }}</p> </div> <hr> <div class="about"> <h3>About this listing</h3> <expandable-text>{{ listing.about }}</expandable-text> </div> <div class="lists"> <feature-list title="Amenities" :items="listing.amenities"> ... </feature-list> <feature-list title="Prices" :items="listing.prices"> ... </feature-list> </div> </div> <modal-window ref="imagemodal"> <image-carousel :images="listing.images"></image-carousel> </modal-window> </div> </template> <script> ... export default { components: { ... }, computed: { listing() { let listing = this.$store.state.listings.find( listing => listing.id == this.$route.params.listing ); return populateAmenitiesAndPrices(listing); } }, methods: { ... } } </script>

Changes to HomePage are much simpler; just remove the mixin and the local state, and replace it with a computed property, listing_groups, which will retrieve all the listing summaries from the store.

resources/assets/components/HomePage.vue:

export default { computed: { listing_groups() { return groupByCountry(this.$store.state.listing_summaries); } }, components: { ... } }

After making these changes, reload the app and you should see no obvious change in behavior. However, inspecting the Vuex tab of Vue Devtools, you will see that page data is now in the store:

Figure 8.14. Page state is now in the Vuex store

Getters

Sometimes what we want to get from the store is not a direct value, but a derived value. For example, say we wanted to get only those listing summaries that were saved by the user. To do this, we can define a getter, which is like a computed property for the store:

state: { saved: [5, 10], listing_summaries: [ ... ] }, getters: { savedSummaries(state) { return state.listing_summaries.filter( item => state.saved.indexOf(item.id) > -1 ); } }

Now, any component that needs the getter data can retrieve it from the store as follows:

console.log(this.$store.state.getters.savedSummaries); /* [ 5 => [ ... ], 10 => [ ... ] ] */

Generally, you define a getter when several components need the same derived value, to save repeating code. Let's create a getter which retrieves a specific listing. We've already created this functionality in ListingPage, but since we're going to need it in our router as well, we'll refactor it as a getter.

One thing about getters is that they don't accept a payload argument like mutations do. If you want to pass a value to a getter, you need to return a function where the payload is an argument of that function.

resources/assets/js/router.js:

getters: { getListing(state) { return id => state.listings.find(listing => id == listing.id); } }

Let's now use this getter in our ListingPage to replace the previous logic.

resources/assets/components/ListingPage.vue:

computed: {

listing() { return populateAmenitiesAndPrices( this.$store.getters.getListing(this.$route.params.listing) ); }

}

Checking if page state is in the store

We've successfully moved page state into the store. Now in the navigation guard, we will check to see if the data a page needs is already stored to avoid retrieving the same data twice:

Figure 8.15. Decision logic for getting page data

Let's implement this logic in the beforeEach hook in router.js. We'll add an if block at the start that will instantly resolve the hook if the data is already present. The if uses a ternary function with the following logic:

If the route name is listing, use the getListing getter to see if that particular listing is available (this getter returns undefined if it is not)

If the route name is not listing, check to see if the store has listing summaries available. Listing summaries are always retrieved all at once, so if there's at least one, you can assume they're all there

resources/assets/js/router.js:

router.beforeEach((to, from, next) => { let serverData = JSON.parse(window.vuebnb_server_data); if ( to.name === 'listing' ? store.getters.getListing(to.params.listing) : store.state.listing_summaries.length > 0 ) { next(); } else if (!serverData.path || to.path !== serverData.path) { axios.get(`/api${to.path}`).then(({data}) => { store.commit('addData', {route: to.name, data}); next(); }); } else { store.commit('addData', {route: to.name, data: serverData}); next(); } });

With that done, if the in-app navigation is used to navigate from the home page to listing 1, then back to the home page, then back to listing 1, the app will retrieve listing 1 from the API just the once. It would have done it twice under the previous architecture!

Saved page

We will now add the saved page to Vuebnb. Let's begin by creating the component file:

$ touch resources/assets/components/SavedPage.vue

Next, we'll create a new route with this component at the path /saved.

resources/assets/js/router.js:

... import SavedPage from '../components/SavedPage.vue'; let router = new VueRouter({ ... routes: [ ... { path: '/saved', component: SavedPage, name: 'saved' } ] });

Let's also add some server-side routes to the Laravel project. As discussed above, the saved page uses exactly the same data as the home page. This means that we can just call the same controller methods used for the home page.

routes/web.php:

Route::get('/saved', 'ListingController@get_home_web');

routes/api.php:

Route::get('/saved', 'ListingController@get_home_api');

Now we will define the SavedPage component. Beginning with the script tag, we will import the ListingSummary component we created back in Chapter 6, Composing Widgets with Vue.js Components. We'll also create a computed property, listings, that will return the listing summaries from the store, filtered by whether or not they're saved.

resources/assets/components/SavedPage.vue:

<template></template> <script> import ListingSummary from './ListingSummary.vue'; export default { computed: { listings() { return this.$store.state.listing_summaries.filter( item => this.$store.state.saved.indexOf(item.id) > -1 ); } }, components: { ListingSummary } } </script> <style></style>

Next, we will add to the template tag of SavedPage. The main content includes a check for the length of the array returned by the listings computed property. If it is 0, no items have been saved yet. In this case, we display a message to inform the user. If there are listings saved, however, we'll iterate through them and display them with the ListingSummary component.

resources/assets/components/SavedPage.vue:

<template> <div id="saved" class="home-container"> <h2>Saved listings</h2> <div v-if="listings.length" class="listing-summaries"> <listing-summary v-for="listing in listings" :listing="listing" :key="listing.id" ></listing-summary> </div> <div v-else>No saved listings.</div> </div> </template> <script>...</script> <style>...</style>

Lastly, we'll add to the style tag. The main thing to note here is that we're utilizing the flex-wrap: wrap rule and justifying to the left. This ensures that our listing summaries will organize themselves in rows without gaps.

resources/assets/components/SavedPage.vue:

<template>...</template> <script>...</script> <style> #saved .listing-summaries { display: flex; flex-wrap: wrap; justify-content: left; overflow: hidden; } #saved .listing-summaries .listing-summary { padding-bottom: 30px; } .listing-summaries > .listing-summary { margin-right: 15px; } </style>

Let's also add the .saved-container CSS rules in our global CSS file. This ensures that our custom footer has access to these rules as well.

resources/assets/css/style.css:

.saved-container { margin: 0 auto; padding: 0 25px; } @media (min-width: 1131px) { .saved-container { width: 1095px; padding-left: 40px; margin-bottom: -10px; } }

The final task is to add some default saved listings to the store. I've chosen 1 and 15 at random, but you can add any you want. We'll remove these again in the next chapter when we use Laravel to persist saved listings to the database.

resources/assets/js/store.js:

state: { saved: [1, 15], ... },

With that done, here's what our saved page looks like:

Figure 8.16. Saved page

If we remove all our saved listings, this is what we see:

Figure 8.17. Saved page without listings

Toolbar links

The last thing we'll do in this chapter is to add a link to the saved page in the toolbar so that the saved page is accessible from any other page. To do this, we'll add an inline ul where links are enclosed within a child li (we'll add more links to the toolbar in Chapter 9, Adding a User Login and API Authentication with Passport).

resources/assets/components/App.vue:

<div id="toolbar"> <router-link :to="{ name: 'home' }"> <img class="icon" src="/images/logo.png"> <h1>vuebnb</h1> </router-link> <ul class="links"> <li> <router-link :to="{ name: 'saved' }">Saved</router-link> </li> </ul> </div>

To display this correctly, we'll have to add some extra CSS. Firstly, we'll modify the #toolbar declaration so that the toolbar uses flex for display. We'll also add some new rules below that for displaying the links.

resources/assets/components/App.vue:

<style> #toolbar { display: flex; justify-content: space-between; border-bottom: 1px solid #e4e4e4; box-shadow: 0 1px 5px rgba(0, 0, 0, 0.1); } ... #toolbar ul { display: flex; align-items: center; list-style: none; padding: 0 24px 0 0; margin: 0; } @media (max-width: 373px) { #toolbar ul { padding-right: 12px; } } #toolbar ul li { padding: 10px 10px 0 10px; } #toolbar ul li a { text-decoration: none; line-height: 1; color: inherit; font-size: 13px; padding-bottom: 8px; letter-spacing: 0.5px;

cursor: pointer; } #toolbar ul li a:hover { border-bottom: 2px solid #484848; padding-bottom: 6px; } </style>

We now have a link to the saved page in the toolbar:

Figure 8.18: Saved link in toolbar

## Summary

In this chapter, we learned about Vuex, Vue's official state management library, which is based on the Flux architecture. We installed Vuex in Vuebnb and set up a store where global state could be written and retrieved. We then learned the main features of Vuex including state, mutator methods and getters, and how we can debug Vuex using Vue Devtools. We used this knowledge to implement a listing save component, which we then added to our main pages. Lastly, we married Vuex and Vue Router to allow page state to be more efficiently stored and retrieved when the route changes.

In the next chapter, we'll cover one of the trickiest topics of full-stack apps - authentication. We'll add a user profile to Vuebnb so a user can persist their saved items to the database. We'll also continue to add to our knowledge of Vuex by utilizing some of its more advanced features.