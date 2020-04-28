# 2020121Full-Stack-Vuejs2-R03

## 记忆时间

## 0801. Managing Your Application State with Vuex

In the last chapter, you learned how Vue Router can be used to add virtual pages to a Vue.js single-page app. We will now add components to Vuebnb that share data across pages and therefore can't rely on transient local state. To do this, we will utilize Vuex, a Flux-inspired library for Vue.js that offers a robust means of managing global application state.

Topics covered in this chapter: 1) An introduction to the Flux application architecture and why it is useful for building user interfaces. 2) An overview of Vuex and its key features, including state and mutations. 3) How to install Vuex and set up a global store that can be accessed by Vue.js components. 4) How Vuex allows for superior debugging with Vue Devtools via mutation logging and time-travel debugging. 5) The creation of a save feature for Vuebnb listings and a saved listings page. 6) Moving page state into Vuex to minimize unnecessary data retrieval from the server.

### Summary

In this chapter, we learned about Vuex, Vue's official state management library, which is based on the Flux architecture. We installed Vuex in Vuebnb and set up a store where global state could be written and retrieved. We then learned the main features of Vuex including state, mutator methods and getters, and how we can debug Vuex using Vue Devtools. We used this knowledge to implement a listing save component, which we then added to our main pages. Lastly, we married Vuex and Vue Router to allow page state to be more efficiently stored and retrieved when the route changes.

In the next chapter, we'll cover one of the trickiest topics of full-stack apps - authentication. We'll add a user profile to Vuebnb so a user can persist their saved items to the database. We'll also continue to add to our knowledge of Vuex by utilizing some of its more advanced features.

### 8.1 Flux application architecture

Imagine you've developed a multi-user chat app. The interface has a user list, private chat windows, an inbox with chat history and a notification bar to inform users of unread messages.

Millions of users are chatting through your app on a daily basis. However, there are complaints about an annoying problem: the notification bar of the app will occasionally give false notifications; that is, a user will be notified of a new unread message, but when they check to see what it is, it's just a message they've already seen.

What I've described is a real scenario that Facebook developers had with their chat system a few years ago. The process of solving this inspired their developers to create an application architecture they named Flux. Flux forms the basis of Vuex, Redux and other similar libraries.

Facebook developers struggled with this zombie notification bug for some time. They eventually realized that its persistent nature was more than a simple bug; it pointed to an underlying flaw in the architecture of the app.

The flaw is most easily understood in the abstract: when you have multiple components in an application that share data, the complexity of their interconnections will increase to a point where the state of the data is no longer predictable or understandable. When bugs like the one described inevitably arise, the complexity of the app data makes them near impossible to resolve:

Figure 8.1. The complexity of communication between components increases with every extra component

Flux is not a library. You can't go to GitHub and download it. Flux is a set of guiding principles that describe a scalable frontend architecture that sufficiently mitigates this flaw. It is not just for a chat app, but for any complex UI with components which share state, like Vuebnb. Let's now explore the guiding principles of Flux.

#### Principle #1 – Single source of truth

Components may have local data that only they need to know about. For example, the position of the scroll bar in the user list component is probably of no interest to other components:

```js
Vue.component('user-list', { 
    data() { 
        scrollPos: ... 
    } 
});
```

But any data that is to be shared between components, for example application data, needs to be kept in a single place, separate from the components that use it. This location is referred to as the store. Components must read application data from this location and not keep their own copy to prevent conflict or disagreement:

1『 Single source of truth 指的就是中心数据文件。』

Figure 8.2. Centralized data simplifies application state

#### Principle #2 – Data is read-only

Components can freely read data from the store. But they cannot change data in the store, at least not directly. Instead, they must inform the store of their intent to change the data and the store will be responsible for making those changes via a set of defined functions called mutator methods.

Why this approach? If we centralize the data-altering logic then we don't have to look far if there are inconsistencies in the state. We're minimizing the possibility that some random component (possibly in a third party module) has changed the data in an unexpected fashion:

Figure 8.3. State is read-only. Mutator methods are used to write to the store

#### Principle #3 – Mutations are synchronous

It's much easier to debug state inconsistencies in an app that implements the above two principles in its architecture. You could log commits and observe how the state changes in response (which automatically happens with Vue Devtools, as we'll see).

But this ability would be undermined if our mutations were applied asynchronously. We'd know the order our commits came in, but we would not know the order in which our components committed them. Synchronous mutations ensure state is not dependent on the sequence and timing of unpredictable events.

### 8.2 Vuex

Vuex (usually pronounced veweks) is the official Vue.js implementation of the Flux architecture. By enforcing the principles described previously, Vuex keeps your application data in a transparent and predictable state even when that data is being shared across many components.

Vuex includes a store with state and mutator methods, and will reactively update any components that are reading data from the store. It also allows for handy development features like hot module reloading (updating modules in a running application) and time-travel debugging (stepping back through mutations to trace bugs).

In this chapter, we will add a save feature to our Vuebnb listings so that a user can keep track of the listings that they like best. Unlike other data in our app so far, the saved state must persist across pages; for example, when a user changes from one page to another, the app must remember which items the user has already saved. We will use Vuex to achieve this:

Figure 8.4. Saved state is available to all page components

#### 8.2.1 Installing Vuex

Vuex is an NPM package that can be installed from the command line:

    $ npm i --save-dev vuex

1『改用「yarn add vuex --dev」。』

We will put our Vuex configuration into a new module file store.js:

    $ touch resources/assets/js/store.js

We need to import Vuex in this file and, like Vue Router, install it with Vue.use. This gives special properties to Vue that make it compatible with Vuex, such as allowing components to access the store via this.\$store.

resources/assets/js/store.js:

```js
import Vue from 'vue';
import Vuex from 'vuex';
Vue.use(Vuex);

export default new Vuex.Store();
```

We will then import the store module in our main app file, and add it to our Vue instance.

resources/assets/js/app.js:

```js
// import "core-js/fn/object/assign";
// window.Vue = require('vue');
import Vue from 'vue';
import ListingPage from '../components/ListingPage.vue';
import App from '../components/App.vue';
import router from './router';
import store from './store';

// Vue 实例
var vm = new Vue({
    el: "#app",
    render: h => h(App),
    // components: {ListingPage},
    router,
    store,
});
```

### 8.3 Save feature

As mentioned, we'll be adding a save feature to our Vuebnb listings. The UI of this feature is a small, clickable icon that is overlaid on the top right of a listing summary's thumbnail image. It acts similarly to a checkbox, allowing the user to toggle the saved status of any particular listing:

The save feature will also be added as a button in the header image on the listing page:

#### 8.3.1 ListingSave component

Let's begin by creating the new component:

    $ touch resources/assets/components/ListingSave.vue

The template of this component will include a Font Awesome heart icon. It will also include a click handler which will be used to toggle the saved state. Since this component will always be a child of a listing or listing summary, it will receive a listing ID as a prop. This prop will be used shortly to save the state in Vuex.

resources/assets/components/ListingSave.vue:

```html
<template>
    <div class="listing-save" @click.stop="toggleSaved()">
        <i class="fa fa-lg fa-heart-o"></i>
    </div>
</template>

<script>
    export default {
        props: ['id'],
        methods: {
            toggleSaved() {
                //
            }
        }
    }
</script>

<style>
    .listing-save {
        position: absolute;
        top: 20px;
        right: 20px;
        cursor: pointer;
    }
    .listing-save .fa-heart-o {
        color: #ffffff;
    }
</style>
```

Note that the click handler has a stop modifier. This modifier prevents the click event from bubbling up to ancestor elements, especially any anchor tags which might trigger a page change!

1『上面的修饰符 stop 是个关键知识点，类似于小程序里的冒泡和非冒泡机制。』

We'll now add ListingSave to the ListingSummary component. Remember to pass the listing's ID as a prop. While we're at it, let's add a position: relative to the .listing-summary class rules so that ListingSave can be positioned absolutely against it.

resources/assets/components/ListingSummary.vue:

```html
<template>
    <div class="listing-summary">
        <router-link :to="{name:'listing', params:{listing:listing.id}}">
            <div class="wrapper">
                <div class="thumbnail" :style="backgroundImageStyle"></div>
                <div class="info title">
                    <span>{{ listing.price_per_night }}</span>
                    <span>{{ listing.title }}</span>
                </div>
                <div class="info address">{{ listing.address }}</div>
            </div>
        </router-link>
        <listing-save :id="listing.id"></listing-save>
    </div>
</template>

<script>
    import ListingSave from './ListingSave';
    export default {
        props: ['listing'],
        computed: {
            backgroundImageStyle() {
                return {
                    'background-image': `url("${this.listing.thumb}")`
                }
            }
        },
        components: {
            ListingSave,
        }
    }
</script>

<style>
    .listing-summary {
        flex: 0 0 auto;
        position: relative;
    }

    @media (max-width: 400px) {
        .listing-summary .listing-save {
            left: 15px;
            right: auto;
        }
    }
...
</style>
```

With that done, we will now see the ListingSave heart icon rendered on each summary:

Figure 8.7. The ListingSave component within ListingSummary components

### 8.4 Saved state

The ListingSave component does not have any local data; we will instead keep any saved listings in our Vuex store. To do this, we will create an array in the store called saved. Each time the user toggles the saved state of a listing its ID will be either added or removed from this array. To begin, let's add a state property to our Vuex store. This object will hold any data we want to be globally available to the components of our app. We will add the saved property to this object and assign it an empty array.

1『数据中心啊，太赞了。』

resources/assets/js/store.js:

```js
...

export default new Vuex.Store({ 
    state: { 
        saved: [] 
    } 
});
```

### 8.5 Mutator method

We created the stub for a toggleSaved method in our ListingSave component. This method should add or remove the listing's ID from the saved state in the store. Components can access the store as this.\$store. More specifically, the saved array can be accessed at this.\$store.state.saved.

resources/assets/components/ListingSave.vue:

```js
methods: { 
    toggleSaved() { 
    console.log(this.$store.state.saved); /* Currently an empty array. [] */ 
    } 
}
```

Remember that in the Flux architecture state is read-only. That means we cannot directly modify saved from a component. Instead, we must create a mutator method in the store which does the modification for us.

Let's create a mutations property in our store configuration, and add a function property toggleSaved. Vuex mutator methods receive two arguments: the store state and a payload. This payload can be anything you want to pass from the component to the mutator. For the current case, we will send the listing ID. The logic for toggleSaved is to check if the listing ID is already in the saved array and if so, remove it, or if not, add it.

resources/assets/js/store.js:

```js
export default new Vuex.Store({
    state: {
        saved: [],
    },
    mutations: {
        toggleSaved(state, id) {
            let index = state.saved.findIndex(saved => saved === id);
            if (index === -1) {
                state.saved.push(id);
            } else {
                state.saved.splice(index, 1);
            }
        }
    },
});
```

We now need to commit this mutation from ListingSave. Commit is Flux jargon that is synonymous with call or trigger. A commit looks like a custom event with the first argument being the name of the mutator method and the second being the payload.

resources/assets/components/ListingSave.vue:

```js
<script>
    export default {
        props: ['id'],
        methods: {
            toggleSaved() {
                this.$store.commit('toggleSaved', this.id);
            }
        }
    }
</script>
```

The main point of using mutator methods in the store architecture is that state is changed consistently. But there is an additional benefit: we can easily log these changes for debugging. If you check the Vuex tab in Vue Devtools after clicking one of the save buttons, you will see an entry for that mutation:

Figure 8.8: Mutation log

Each entry in the log can tell you the state after the change was committed, as well as the particulars of the mutation. If you double-click a logged mutation, Vue Devtools will revert the state of the app to what it was directly after that change. This is called time-travel debugging and can be useful for fine-grained debugging.

1『再点一下，数组里的该 id 会删掉，为实现取消收藏做准备啊。』

### 8.6 Changing the icon to reflect the state

Our ListingSave component's icon will appear differently, depending on whether or not the listing is saved; it will be opaque if the listing is saved, and transparent if it is not. Since the component doesn't store its state locally, we need to retrieve state from the store to implement this feature.

Vuex store state should generally be retrieved via a computed property. This ensures that the component is not keeping its own copy, which would violate the single source of truth principle, and that the component is re-rendered when the state is mutated by this component or another. Reactivity works with Vuex state, too! Let's create a computed property isListingSaved, which will return a Boolean value reflecting whether or not this particular listing has been saved.

resources/assets/components/ListingSave.vue:

We can now use this computed property to change the icon. Currently we're using the Font Awesome icon fa-heart-o. This should represent the unsaved state. When the listing is saved we should instead use the icon fa-heart. We can implement this with a dynamic class binding.

resources/assets/components/ListingSave.vue:

```js
<template>
    <div class="listing-save" @click.stop="toggleSaved()">
        <i :class="classes"></i>
    </div>
</template>

<script>
    export default {
        props: ['id'],
        methods: {
            toggleSaved() {
                this.$store.commit('toggleSaved', this.id);
            }
        },
        computed: {
            isListingSaved() {
                return this.$store.state.saved.find(saved => saved === this.id);
            },
            classes() {
                let saved = this.isListingSaved;
                return {
                    'fa': true,
                    'fa-lg': true,
                    'fa-heart': saved,
                    'fa-heart-o': !saved,

                }
            }
        },
    }
</script>

<style>
    .listing-save {
        position: absolute;
        top: 20px;
        right: 20px;
        cursor: pointer;
    }
    .listing-save .fa-heart-o {
        color: #ffffff;
    }

    .listing-save .fa-heart {
        color: #ff5a5f;
    }
</style>
```

1『发现心形不见了，又没报错，找了半天发现自己「classes」没用指令绑定，少了绑定指令简写的冒号。』

### 8.7 Adding to ListingPage

We also want the save feature to appear on the listing page. It will go inside the HeaderImage component alongside the View Photos button so that, like with the listing summaries, the button is overlaid on the listing's main image.

resources/assets/components/HeaderImage.vue:

```js
<template>
    <div class="header">
        <div class="header-img" :style="headerImageStyle" 
            @click="$emit('header-clicked')">
            <listing-save :id="id"></listing-save>
            <button class="view-photos">View Photos</button>
        </div>
    </div>
</template>

<script>
    import ListingSave from './ListingSave';
    export default {
        computed: {
            headerImageStyle() {
                return {
                    "background-image": `url(${this.imageUrl})`}
            },
        },
        props: ['image-url', 'id'],
        components: {
            ListingSave,
        }
    }
</script>
```

Note that HeaderImage does not have the listing ID in its scope, so we'll have to pass this down as a prop from ListingPage. id is not currently a data property of ListingPage either, but, if we declare it, it will simply work. This is because the ID is already a property of the initial state/AJAX data the component receives, therefore id will automatically be populated by the Object.assign when the component is loaded by the router.

resources/assets/components/ListingPage.vue:

```html
<header-image v-if="images[0]" 
:image-url="images[0]" 
@header-clicked="openModal"
:id="id"></header-image>
```

If you save a listing via the listing page, then return to the home page, the equivalent listing summary will be saved. This is because our Vuex state is global and will persist across page changes (though not page refreshes...yet).





