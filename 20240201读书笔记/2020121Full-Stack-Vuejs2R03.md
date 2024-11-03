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

1『看来是作为子组件，往往通过 prop 获取父组件的数据。』

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

1『上面的修饰符 stop 是个关键知识点，类似于小程序里的冒泡和非冒泡机制。但目前还没能力碰到一个场景知道该用它。（2020-05-15）』

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

1『这里的 css 样式值得学习。』

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

1『组件通知 store 修改数据，是通过 \$store.commit() 方法发送信息给 mutations。而组件想从 store 那边获取数据的话，必须通过自己的 computed 属性，methods 属性是不行的，这样做的原因是为了 computed 不会保存备份，确保了 Flux 框架里「单一数据源」的原则。』

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

### 8.8 Making ListingSave a button

As it is, the ListingSave feature appears too small in the listing page header and will be easily overlooked by a user. Let's make it a proper button, similar to the View Photos button in the bottom left of the header. To do this, we'll modify ListingSave to allow parent components to send a prop button. This Boolean prop will indicate if the component should include a button element wrapped around the icon or not. The text for this button will be a computed property message which will change from Save to Saved depending on the value of isListingSaved.

resources/assets/components/ListingSave.vue:

We will now set the button prop to true within HeaderImage. Even though the value is not dynamic, we use a v-bind to ensure the value is interpreted as a JavaScript value, not a string.

resources/assets/components/HeaderImage.vue:

```js
<listing-save :id="id" :button="true"></listing-save>
```

### 8.9 Moving page state into the store

Now that the user can save any listings that they like, we will need a saved page where they can view those saved listings together. We will build this new page shortly, and it will look like this:

Implementing the saved page will require an enhancement to our app architecture, however. Let's do a quick recap of how data is retrieved from the server to understand why.

All the pages in our app require a route on the server to return a view. This view includes the data for the relevant page component inlined in the document head. Or, if we navigate to that page via in-app links, an API endpoint will instead supply that same data. We set up this mechanism in Chapter 7, Building A Multi-Page App With Vue Router.

1『简单阐述了在没使用 VueX 的情况下，多页面是如何跟后台服务器交互数据的。』

The saved page will require the same data as the home page (the listing summary data), as the saved page is really just a slight variation on the home page. It makes sense, then, to share data between the home page and saved page. In other words, if a user loads Vuebnb from the home page, then navigates to the saved page, or vice versa, it would be a waste to load the listing summary data more than once.

1『首页的数据跟收藏页面的数据时共有的，所以只需加载一次。』

Let's decouple our page state from our page components and move it into Vuex. That way it can be used by whichever page needs and it and avoid unnecessary reloading:

1『上图说明了将公共的数据剥离出来放进 Store 里。』

### 8.10 State and mutator methods

Let's add two new state properties to our Vuex store: listings and listing\_summaries. These will be arrays that store our listings and listing summaries respectively. When the page first loads, or when the route changes and the API is called, the loaded data will be put into these arrays rather than being assigned directly to the page components. The page components will instead retrieve this data from the store.

We'll also add a mutator method, addData, for populating these arrays. It will accept a payload object with two properties: route and data. route is the name of the route, for example, listing, home, and so on. data is the listing or listing summary data retrieved from the document head or the API.

resources/assets/js/store.js:

```js
export default new Vuex.Store({
    state: {
        saved: [],
        listing_summaries: [],
        listings: [],
    },
    mutations: {
        toggleSaved(state, id) {
            let index = state.saved.findIndex(saved => saved === id);
            if (index === -1) {
                state.saved.push(id);
            } else {
                state.saved.splice(index, 1);
            }
        },
        addData(state, {route, data}) {
            if (route === 'listing') {
                state.listings.push(data.listing);
            } else {
                state.listing_summaries = data.listings;
            }
        },
    },
});
```

1『现在看上面的代码实现，清爽很多了。（2020-05-15）』

### 8.11 Router

The logic for retrieving page state is in the mixin file route-mixin.js. This mixin adds a beforeRouteEnter hook to a page component which applies the page state to the component instance when it becomes available.

1『 mixin file 是上一章的一个知识点，这里又看到钩子「hook」这个极其重要的概念，官方文档前面综述里的那张生命周期图值得反复看。』

Now that we're storing page state in Vuex we will utilize a different approach. Firstly, we won't need a mixin anymore; we'll put this logic into router.js now. Secondly, we'll use a different navigation guard, beforeEach. This is not a component hook, but a hook that can be applied to the router itself, and it is triggered before every navigation. You can see in the following code block how I've implemented this in router.js. Note that before next() is called we commit the page state to the store.

1『上面的知识密度很大。2 点更新：1）废除 route-mixin.js，将其逻辑合并到 router.js 里。2）增加 beforeEach() 来切换页面的数据，这个方法不是组件的钩子，而是给路由 router 用的，它是在跳转到各页面之间被触发的。注意一点，before next() 方法是在，组件页面通过 commit() 方法通知组件修改 store 数据之前被调用的。』

resources/assets/js/router.js:

```js
import Vue from 'vue';
import axios from 'axios';
import store from './store';

import VueRouter from 'vue-router';
Vue.use(VueRouter);

import HomePage from '../components/HomePage.vue';
import ListingPage from '../components/ListingPage.vue';

let router = new VueRouter({
    mode: 'history',
    routes: [
        {
            path: '/',
            component: HomePage,
            name: 'home',
        },
        {
            path: '/listing/:listing',
            component: ListingPage,
            name: 'listing',
        },
        {
            path: '/saved',
            component: SavedPage,
            name: 'saved',
        },
    ],
    scrollBehavior(to, from, savedPosition) {
        return {x:0, y:0};
    },
});

router.beforeEach((to, from, next) => {
    let serverData = JSON.parse(window.vuebnb_server_data);
    if (!serverData.path || to.path !== serverData.path) {
        axios.get(`/api${to.path}`).then(({data}) => {
            store.commit('addData', {route: to.name, data});
            next();
        });
    } else {
        store.commit('addData', {route: to.name, data: serverData});
        next();
    }
});

export default router;
```

With that done, we can now delete the route mixin:

    $ rm resources/assets/js/route-mixin.js

### 8.12 Retrieving page state from Vuex

Now that we've moved page state into Vuex we'll need to modify our page components to retrieve it. Starting with ListingPage, the changes we must make are: 1) Remove local data properties. 2) Add a computed property listing. This will find the right listing data from the store based on the route. 3) Remove the mixin. 4) Change template variables so they're properties of listing: an example is {{ title }} , which will become {{ listing.title }}. Unfortunately, all variables are now properties of listing which makes our template slightly more verbose.

resources/assets/components/ListingPage.vue:

```html
<template>
    <div>
        <header-image v-if="listing.images[0]" 
        :image-url="listing.images[0]" 
        @header-clicked="openModal"
        :id="listing.id"></header-image>
        <div class="listing-container">
            <div class="heading">
                <h1>{{ listing.title }}</h1>
                <p>{{ listing.address }}</p>
            </div>
            <hr>
            <div class="about">
                <h3>About this listing</h3>
                <expandable-text>{{ listing.about }}</expandable-text>
            </div>
            <div class="lists">
                <feature-list title="Amenities" :items="listing.amenities">
                    <template slot-scope="amenity">
                        <i class="fa fa-lg" :class="amenity.icon"></i>
                        <span>{{ amenity.title }}</span>
                    </template>
                </feature-list>
                <feature-list title="Prices" :items="listing.prices">
                    <template slot-scope="price">
                        {{ price.title }}: <strong>{{ price.value }}</strong>
                    </template>
                </feature-list>
            </div>
        </div>
        <modal-window ref="imagemodal">
            <image-carousel :images="listing.images"></image-carousel> 
        </modal-window>
    </div>
</template>

<script>
    import { populateAmenitiesAndPrices } from '../js/helpers';
    import ImageCarousel from './ImageCarousel.vue';
    import ModalWindow from './ModalWindow.vue';
    import HeaderImage from './HeaderImage.vue';
    import FeatureList from './FeatureList.vue';
    import ExpandableText from './ExpandableText.vue';

    export default {
        data() {
            return {
                title: null,
                about: null,
                address: null,
                amenities: [],
                prices: [],
                images: [],
                id: null,
            }
        },
        components: { 
            ImageCarousel,
            ModalWindow,
            HeaderImage,
            FeatureList,
            ExpandableText,
        },
        computed: {
            listing() {
                let listing = this.$store.state.listings.find(
                    listing => listing.id == this.$route.params.listing
                );
                return populateAmenitiesAndPrices(listing);
            }
        },
        methods: {
            openModal() {
                this.$refs.imagemodal.modalOpen = true;
            },
        },
}
</script>
```

1『

上面 JS 代码里，主要修改的地方是 computed 和 methods 属性里。多次减到 find() 方法结合箭头函数的妙用，牢记。

```js
let listing = this.$store.state.listings.find(
    listing => listing.id == this.$route.params.listing
);
```

』

Changes to HomePage are much simpler; just remove the mixin and the local state, and replace it with a computed property, listing\_groups, which will retrieve all the listing summaries from the store.

resources/assets/components/HomePage.vue:

```html
<template>
    <div class="home-container">
        <listing-summary-group 
        v-for="(group, country) in listing_groups"
        :key="country"
        :listings="group"
        :country="country"
        class="listing-summary-group">
        </listing-summary-group>
    </div>
</template>

<script>
    import { groupByCountry } from '../js/helpers';
    import ListingSummaryGroup from './ListingSummaryGroup.vue';

    export default {
        computed: {
            listing_groups() {
                return groupByCountry(this.$store.state.listing_summaries);
            }
        },
        components: {
            ListingSummaryGroup,
        },
    }
</script>
```

After making these changes, reload the app and you should see no obvious change in behavior. However, inspecting the Vuex tab of Vue Devtools, you will see that page data is now in the store:

1『

修改后是没有报错，但首页里没有收藏的心形图标，最后定位到问题在 ListingSave.vue 文件里。

```html
<template>
    <div class="listing-save" @click.stop="toggleSaved()">
        <button v-if="button">
            <i :class="classes"></i>
            {{ message }}
        </button>
        <i v-else :class="classes"></i>
    </div>
</template>
```

button 里需要加上 \<i v-else :class="classes">\</i>。但具体的原理目前没弄明白。（2020-04-29）

』

### 8.13 Getters

Sometimes what we want to get from the store is not a direct value, but a derived value. For example, say we wanted to get only those listing summaries that were saved by the user. To do this, we can define a getter, which is like a computed property for the store:

```js
state: { 
    saved: [5, 10], 
    listing_summaries: [ ... ] 
}, 
getters: { 
    savedSummaries(state) { 
        return state.listing_summaries.filter( 
        item => state.saved.indexOf(item.id) > -1 
        ); 
    } 
}
```

Now, any component that needs the getter data can retrieve it from the store as follows:

```js
console.log(this.$store.state.getters.savedSummaries);

 /* 
 [ 
    5 => [ ... ], 
    10 => [ ... ] 
 ] 
 */
```

Generally, you define a getter when several components need the same derived value, to save repeating code. Let's create a getter which retrieves a specific listing. We've already created this functionality in ListingPage, but since we're going to need it in our router as well, we'll refactor it as a getter. One thing about getters is that they don't accept a payload argument like mutations do. If you want to pass a value to a getter, you need to return a function where the payload is an argument of that function.

resources/assets/js/router.js:

```js
getters: {
    getListing(state) {
        return id => state.listings.find(listing => id == listing.id);
    }
},
```

1『上面的方法应该是在 store.js 文件里定义的，作者有误。』

Let's now use this getter in our ListingPage to replace the previous logic.

resources/assets/components/ListingPage.vue:

```js
computed: {
    listing() {
        return populateAmenitiesAndPrices(
            this.$store.getters.getListing(this.$route.params.listing)
        );
    }
},
```

1『注意下，目前页面获取数据已经放到路由文件「router.js」里去了，而且是在跳转页面之前完成的。上面小节讲的是如何获取状态「retrieving page state from Vuex」。使用 getter 方法可以封装同样的操作。』

### 8.14 Checking if page state is in the store

We've successfully moved page state into the store. Now in the navigation guard, we will check to see if the data a page needs is already stored to avoid retrieving the same data twice:

Figure 8.15. Decision logic for getting page data

1『上面的逻辑图很重要，经常消化下。』

Let's implement this logic in the beforeEach hook in router.js. We'll add an if block at the start that will instantly resolve the hook if the data is already present. The if uses a ternary function with the following logic: 1) If the route name is listing, use the getListing getter to see if that particular listing is available (this getter returns undefined if it is not). 2) If the route name is not listing, check to see if the store has listing summaries available. Listing summaries are always retrieved all at once, so if there's at least one, you can assume they're all there.

resources/assets/js/router.js:

```js
router.beforeEach((to, from, next) => {
    let serverData = JSON.parse(window.vuebnb_server_data);
    if (
        to.name === 'listing'
          ? store.getters.getListing(to.params.listing)
          : store.state.listing_summaries.length > 0
    ) {
    next();
    } else if (!serverData.path || to.path !== serverData.path) {
        axios.get(`/api${to.path}`).then(({data}) => {
            store.commit('addData', {route: to.name, data});
            next();
        });
    } else {
        store.commit('addData', {route: to.name, data: serverData});
        next();
    }
});
```

With that done, if the in-app navigation is used to navigate from the home page to listing 1, then back to the home page, then back to listing 1, the app will retrieve listing 1 from the API just the once. It would have done it twice under the previous architecture!

### 8.15 Saved page

We will now add the saved page to Vuebnb. Let's begin by creating the component file:

    $ touch resources/assets/components/SavedPage.vue

Next, we'll create a new route with this component at the path /saved.

resources/assets/js/router.js:

```js
let router = new VueRouter({
    mode: 'history',
    routes: [
        {
            path: '/',
            component: HomePage,
            name: 'home',
        },
        {
            path: '/listing/:listing',
            component: ListingPage,
            name: 'listing',
        },
        {
            path: '/saved',
            component: SavedPage,
            name: 'saved',
        },
    ],
    scrollBehavior(to, from, savedPosition) {
        return {x:0, y:0};
    },
});
```

Let's also add some server-side routes to the Laravel project. As discussed above, the saved page uses exactly the same data as the home page. This means that we can just call the same controller methods used for the home page.

routes/web.php:

```php
Route::get('/saved', 'ListingController@get_home_web');
```

routes/api.php:

```php
Route::get('/saved', 'ListingController@get_home_api');
```

Now we will define the SavedPage component. Beginning with the script tag, we will import the ListingSummary component we created back in Chapter 6, Composing Widgets with Vue.js Components. We'll also create a computed property, listings, that will return the listing summaries from the store, filtered by whether or not they're saved.

resources/assets/components/SavedPage.vue:

```html
<script>
    import ListingSummary from './ListingSummary.vue';
    export default {
        computed: {
            listings() {
                return this.$store.state.listing_summaries.filter(
                    item => this.$store.state.saved.indexOf(item.id) > -1
                );
            },
        },
        components: {
            ListingSummary,
        }
    }
</script>
```

Next, we will add to the template tag of SavedPage. The main content includes a check for the length of the array returned by the listings computed property. If it is 0, no items have been saved yet. In this case, we display a message to inform the user. If there are listings saved, however, we'll iterate through them and display them with the ListingSummary component.

resources/assets/components/SavedPage.vue:

```html
<template>
    <div class="home-container" id="saved">
        <h2>Saved listings</h2>
        <div v-if="listings.length" class="listing-summaries">
            <listing-summary
            v-for="listing in listings"
            :listing="listing"
            :key="listing.id"></listing-summary>
        </div>
        <div v-else> No Saved listings.</div>
    </div>
</template>
```

Lastly, we'll add to the style tag. The main thing to note here is that we're utilizing the flex-wrap: wrap rule and justifying to the left. This ensures that our listing summaries will organize themselves in rows without gaps.

resources/assets/components/SavedPage.vue:

```css
<style>
    #saved .listing-summaries {
        display: flex;
        flex-wrap: wrap;
        justify-content: left;
        overflow: hidden;
    }

    #saved .listing-summaries .listing-summary {
        padding-bottom: 30px;
    }

    .listing-summaries > .listing-summary {
        margin-right: 15px;
    }
</style>
```

Let's also add the .saved-container CSS rules in our global CSS file. This ensures that our custom footer has access to these rules as well.

resources/assets/css/style.css:

```css
.saved-container {
    margin: 0 auto;
    padding: 0 25px;
}

@media (min-width: 1131px) {
    .saved-container {
        width: 1095px;
        padding-left: 40px;
        margin-bottom: -10px;
    }
}
```

The final task is to add some default saved listings to the store. I've chosen 1 and 15 at random, but you can add any you want. We'll remove these again in the next chapter when we use Laravel to persist saved listings to the database.

resources/assets/js/store.js:

```js
state: { 
    saved: [1, 15], 
    ... 
},
```

### 8.16 Toolbar links

The last thing we'll do in this chapter is to add a link to the saved page in the toolbar so that the saved page is accessible from any other page. To do this, we'll add an inline ul where links are enclosed within a child li (we'll add more links to the toolbar in Chapter 9, Adding a User Login and API Authentication with Passport).

resources/assets/components/App.vue:

```js
<template>
    <div>
        <div id="toolbar">
            <router-link :to="{name:'home'}">
                <img src="/images/logo.png" class="icon">
                <h1>vuebnb</h1>
            </router-link>
            <ul class="links">
                <li>
                    <router-link :to="{ name:'saved' }">Saved</router-link>
                </li>
            </ul>
        </div>
        <router-view></router-view>
        <custom-footer></custom-footer>
    </div>
</template>
```

To display this correctly, we'll have to add some extra CSS. Firstly, we'll modify the #toolbar declaration so that the toolbar uses flex for display. We'll also add some new rules below that for displaying the links.

## 0901. Adding a User Login and API Authentication with Passport

In the last chapter, we allowed the user to save their favorite Vuebnb listings. This feature was only implemented in the frontend app though, so if the user reloaded the page their selections would be lost. In this chapter, we'll create a user login system and persist saved items to the database so they can be retrieved after a page refresh.

Topics covered in this chapter: 1) Setting up a user login system utilizing Laravel's built-in authentication features. 2) Creating a login form with CSRF protection. 3) Using Vuex actions for asynchronous operations in the store. 4) A brief introduction to the OAuth protocol for API authentication. 5) Setting up Laravel Passport to allow authenticated AJAX requests.

### Summary

In this chapter, we learned about authentication in full-stack Vue/Laravel apps, including session-based authentication for web routes, and token-based authentication for API routes using Laravel Passport. We used this knowledge to set up a login system for Vuebnb, and to allow saved room listings to be persisted to the database. Along the way, we also learned how to utilize CSRF tokens for securing forms, and about Vuex actions for adding asynchronous code to the store.

In the next, and final, chapter, we will learn how to deploy a full-stack Vue and Laravel app to production by deploying Vuebnb to a free Heroku PHP server. We will also begin serving images and other static content from a free CDN.

### 9.1 User model

In order to save listing items to the database, we first need a user model, as we want each user to have their own unique list. Adding a user model means we'll also need an authentication system so that users can sign in and out. Fortunately, Laravel provides a full-featured user model and authentication system out-of-the-box. Let's now take a look at the user model boilerplate files to see what modifications will be needed to fit them for our purposes.

#### 9.1.1 Migration

Looking first at the database migration, the user table schema already includes ID, name, email, and password columns.

database/migrations/2014_10_12_000000_create_users_table.php:

This schema will be sufficient for our needs if we add an additional column for storing the saved listing IDs. Ideally, we'd store these in an array, but since relational databases don't have an array column type, we will instead store them as a serialized string, for example, [1, 5, 10] within a text column.

database/migrations/2014_10_12_000000_create_users_table.php:

```php
Schema::create('users', function (Blueprint $table) { 
    ... 
    $table->text('saved'); }
);
```

### 9.1.2 Model

Let's now take a look now at the User model class that Laravel provides.

app/User.php:

The default configuration is fine, but let's allow the saved attribute to be mass assignable by adding it to the \$fillable array. We'll also get our model to serialize and deserialize the saved text when we read it or write it. To do this we can add a \$casts attribute to the model and cast saved as an array.

app/User.php:

```php
class User extends Authenticatable { 
    ... 
    protected $fillable = [ 'name', 'email', 'password', 'saved' ]; 
    
    ... 
    protected $casts = [ 'saved' => 'array' ]; 
}
```

Now we can treat the saved attribute as an array, even though it's stored as a string in the database:

```php
echo gettype($user->saved()); 
// array
```

#### 9.1.3 Seeder

In a normal web app with a login system, you'd have a registration page so users can create their own accounts. To ensure this book doesn't get too long, we'll skip that feature and instead generate user accounts with a database seeder:

    $ php artisan make:seeder UsersTableSeeder

You can implement a registration page for Vuebnb yourself if you want. The Laravel documentation covers it quite thoroughly at https://laravel.com/docs/5.5/authentication.

3『 [Authentication - Laravel - The PHP Framework For Web Artisans](https://laravel.com/docs/6.x/authentication) 』

Let's create at least one account with a name, email, password, and an array of saved listings. Note that I've used the make method of the Hash facade to hash the password rather than storing it as plain-text. Laravel's default LoginController will automatically verify plain-text passwords against the hash during the login process.

database/seeds/UsersTableSeeder.php:

```
<?php

use Illuminate\Database\Seeder;
use Illuminate\Support\Facades\Hash;
use App\User;

class UsersTableSeeder extends Seeder
{
    /**
     * Run the database seeds.
     *
     * @return void
     */
    public function run()
    {
        User::create([
            'name' => 'dalong',
            'email' => 'test@gmail.com',
            'password' => Hash::make('test'),
            'saved' => [1, 5, 7, 9],
        ]);
    }
}
```

To run the seeder we need to call it from the main DatabaseSeeder class.

database/seeds/DatabaseSeeder.php:

```php
<?php

use Illuminate\Database\Seeder;

class DatabaseSeeder extends Seeder
{
    /**
     * Seed the application's database.
     *
     * @return void
     */
    public function run()
    {
        $this->call(UsersTableSeeder::class);
        $this->call(ListingsTableSeeder::class);
    }
}
```

Let's now rerun our migrations and seeder to install the user table and data with the following command:

    $ php artisan migrate:refresh --seed

To confirm that our user table and data were created correctly, we'll use Tinker to query the table. You should get an output similar to the following:

### 9.2 Login system

Now that we have our user model created, we can implement the rest of the login system. Again, Laravel includes this as an out-of-the-box feature, so there is only a small amount of configuration for us to do. Here's an overview of how the login system works: 1) The user provides their email and password in a login form. We'll create this form with Vue. 2) The form is submitted to the /login POST route. 3) The LoginController will then verify the user's credentials against the database. 4) If the login is successful, the user is redirected to the home page. A session cookie is attached to the response, which is then passed to all outgoing requests to verify the user. Here's a diagrammatic representation of the login system for further clarity:

1『上面的图很形象。』

#### 9.2.1 LoginPage component

We will need a login page for our app, so let's create a new page component:

    $ touch resources/assets/components/LoginPage.vue

We'll begin by defining the template markup, which includes a form with fields for email and password, and a submit button. The form uses the HTTP POST method and is sent to the /login path. I've wrapped the form elements in a div with the .form-controller class to help with styling.

resources/assets/components/LoginPage.vue:

```html
<template>
    <div id="login" class="login-container">
        <form action="/login" method="POST" role="form">
            <div class="form-control">
                <input type="email" id="email" name="email" 
                placeholder="Email Address" required autofocus>
            </div>
            <div class="form-control">
                <input type="password" id="password" name="password"
                placeholder="Password" required>
            </div>
            <div class="form-control">
                <button type="submit">Login in</button>
            </div>
        </form>
    </div>
</template>
```

We don't need any JavaScript functionality just yet, so let's add our CSS rules now.

resources/assets/components/LoginPage.vue:

```html
<style>
    #login form {
        padding-top: 40px;
    }

    @media (min-width: 744px) {
        #login form {
            padding-top: 80px;
        }
    }
    
    #login .form-control {
        margin-bottom: 1em;
    }

    #login input[type=email],
    #login input[type=password],
    #login button,
    #login label {
        width: 100%;
        font-size: 19px !important;
        line-height: 24px;
        color: #484848;
        font-weight: 300;
    }

    #login input {
        background-color: transparent;
        padding: 11px;
        border: 1px solid #dbdbdb;
        border-radius: 2px;
        box-sizing: border-box;
    }

    #login button {
        background-color: #4fc08d;
        color: #ffffff;
        cursor: pointer;
        border: #4fc08d;
        border-radius: 4px;
        padding-top: 12px;
        padding-bottom: 12px;
    }
</style>
```

We'll add a login-container class to our global CSS file so the footer for this page aligns correctly. We'll also add a CSS rule to ensure text inputs display correctly on iPhone. The login page will be the only place we'll have a text input, but let's add it as a global rule in case you decide to add other forms later.

resources/assets/css/style.css:

```css
.login-container {
    margin: 0 auto;
    padding: 0 12px;
}

@media (min-width: 374px) {
    .login-container {
        width: 350px;
    }
}

input[type-text] {
    -webkit-appearance: none;
}
```

Finally, let's add this new page component to our router. We'll first import the component then add it to our routes array in the router configuration.

Note that the login page does not require any data from the server like the other pages of Vuebnb do. This means that we can skip the data-fetching step by modifying the logic of the first if statement in the navigation guard. It should now resolve straightaway if the name of the route is login.

resources/assets/js/router.js:

```js
import LoginPage from '../components/LoginPage.vue';     // 修改的地方

let router = new VueRouter({
    mode: 'history',
    routes: [
        {
            path: '/',
            component: HomePage,
            name: 'home',
        },
        {
            path: '/listing/:listing',
            component: ListingPage,
            name: 'listing',
        },
        {
            path: '/saved',
            component: SavedPage,
            name: 'saved',
        },
        {
            path: '/login',
            component: LoginPage,
            name: 'login',
        },      // 修改的地方
    ],
    scrollBehavior(to, from, savedPosition) {
        return {x:0, y:0};
    },
});

router.beforeEach((to, from, next) => {
    let serverData = JSON.parse(window.vuebnb_server_data);
    if (
        to.name === 'listing'
          ? store.getters.getListing(to.params.listing)
          : store.state.listing_summaries.length > 0
          || to.name === 'login'    // 修改的地方
    ) {
    next();
    } else if (!serverData.path || to.path !== serverData.path) {
        axios.get(`/api${to.path}`).then(({data}) => {
            store.commit('addData', {route: to.name, data});
            next();
        });
    } else {
        store.commit('addData', {route: to.name, data: serverData});
        next();
    }
});

export default router;
```

### 9.2.2 Server routes

Now that we've added a login page at the /login route, we will need to create a matching server-side route. We will also need a route for the login form that posts to the same /login path. In fact, both of these routes are provided out-of-the-box by Laravel as part of its default login system. All we have to do to activate the routes is add the following line to the bottom of our web route file.

routes/web.php:

```php
... Auth::routes();
```

To see the effect of this code, we can use Artisan to show a list of the routes in our app:

    $ php artisan route:list

You'll see all the routes that we've manually created, plus a few that we didn't, for example, login, logout, and register. These are the routes used by Laravel's authentication system that we just activated. Looking at the GET/HEAD /login route, you'll see that it points to the LoginController controller. Let's take a look at that file.

App\Http\Controllers\Auth\LoginController.php:

```php
<?php

namespace App\Http\Controllers\Auth;

use App\Http\Controllers\Controller;
use App\Providers\RouteServiceProvider;
use Illuminate\Foundation\Auth\AuthenticatesUsers;

class LoginController extends Controller
{
    use AuthenticatesUsers;

    /**
     * Where to redirect users after login.
     *
     * @var string
     */
    protected $redirectTo = RouteServiceProvider::HOME;

    /**
     * Create a new controller instance.
     *
     * @return void
     */
    public function __construct()
    {
        $this->middleware('guest')->except('logout');
    }
}
```

This class uses an AuthenticatesUsers trait that defines the showLoginForm method that the /login route handler refers to. Let's overwrite that method so it simply returns our app view. Since this instance of the view doesn't need any data to be inlined in the head (the login form has no state), we will pass an empty array to the data template variable.

App\Http\Controllers\Auth\LoginController.php:

```php
class LoginController extends Controller { 
... 

public function showLoginForm() { 
    return view('app', ['data' => []]); 
} 
}
```

With that done, we can now see our complete login page by navigating the browser to /login:

1『右上角的抬头没实现，作者的是新的「Log in」，目前自己的还是原来的抬头「Saved」。』

### 9.3 CSRF protection

CSRF (cross-site request forgery) is a type of malicious exploit where an attacker gets a user to unknowingly perform an action on a server that they're currently logged in to. This action will change something on the server that is advantageous to the attacker, for example, transfer money, change the password to one the attacker knows, and so on.

For example, an attacker might hide a script in a web page or email and direct the user to it somehow. When it executes, this script could make a POST request to importantwebsite.com/updateEmailAndPassword. If the user is logged in to this site, the request may be successful.

One way to prevent this kind of attack is to embed a special token, essentially a random string, in any form that a user might submit. When the form is submitted, the token is checked against the user's session to make sure it matches. An attacker won't be able to forge this token in their script and should, therefore, be thwarted by this feature. In Laravel, CSRF token creation and verification is managed by the VerifyCsrfToken middleware that is added to the web routes by default:

To include the CSRF token in a form you can simply add {{ csrf_field() }} within the form tag. This will generate a hidden input field containing a valid CSRF token, for example:

```html
<input type="hidden" name="_token" value="3B08L3fj...">
```

This won't work in our scenario, though, as our form is not inside a Blade view but inside a single-file component that will not get processed by Blade. As an alternative, we can add the CSRF token to the head of the page and assign it to the window object.

resources/views/app.blade.php:

```html
<script type="text/javascript"> 
    window.vuebnb_server_data = "{!! addslashes(json_encode($data)) !!}" 
    window.csrf_token = "{{ csrf_token() }}" 
</script>
```

We can now retrieve this from within our Vue.js app and manually add it to the login form. Let's modify LoginPage to include a hidden input field in the form. We'll add some state to this component now, in which the token is included as a data property and bound to the hidden field.

resources/assets/js/components/LoginPage.vue:

```html
<template> 
    <div id="login" class="login-container"> 
        <form role="form" method="POST" action="/login"> 
            <input type="hidden" name="_token" :value="csrf_token"> 
            ... 
        </form> 
    </div> 
</template> 

 <script>
    export default {
        data() {
            return {
                csrf_token: window.csrf_token,
            }
        }
    }
</script>

<style>...</style>
```

1『意外的收获，组件里通过绑定「:value」直接能访问组件里的数据属性，待验证。（2020-05-02）回复：之前理解有误，「:value」只是绑定 token 的值到 input 组件的 value 属性上。上面的知识点帮了大忙，解决了开发数据流开发时，上传 CAD 文件环节遇到的问题。』

If we now try to log in to our app using the credentials of the user we created in the seeder, we'll get served this error page. Looking in the address bar, you'll see that the route we're on is /home, which is not a valid route within our app, hence the NotFoundHttpException:

1『确实啊，一直自动跳转到「http://localhost:8000/home」，浏览器里输入「http://localhost:8000/login」都不行，跳不到登录页面。联想到，化工 101 远程的后台登录界面遇到的问题，是不是跟这个的原理一样的，待确认。（2020-05-02）』

### 9.4 Post-login redirection

When a user logs in, Laravel will redirect them to a page defined by the \$redirectTo attribute in the login controller. Let's change this from /home to /.

app/Http/Auth/Controllers/LoginController.php:

```php
class LoginController extends Controller { 
    ... 
    protected $redirectTo = '/'; 
    ... 
}
```

1『

新版的不一样了。

```php
protected $redirectTo = RouteServiceProvider::HOME;
```

它是调用了 RouteServiceProvider 类里的 HOME 静态属性，尝试了下直接修改无效，比如：

```
protected $redirectTo = '/'
```

必须进 RouteServiceProvider 把 HOME 改掉才行。具体原理目前不清楚。（2020-05-02）

』

Let's also update the RedirectIfAuthenticated middleware class so that if a logged-in user attempts to view the login page, they're redirect to / (instead of the default /home value.)

app/Http/Middleware/RedirectIfAuthenticated.php:

```php
... if (Auth::guard($guard)->check()) { 
    return redirect('/'); 
}
```

1『按上面新版的改了 HOME 就不用管「RedirectIfAuthenticated.php」了，因为这个类里也是引用了 RouteServiceProvider 类里的 HOME 静态属性，哈哈。（2020-05-02） 』

With that done, our login process will now work correctly.

### 9.5 Adding authentication links to the toolbar

Let's now add login and logout links in the toolbar so Vuebnb users can easily access these features. The login link is simply a RouterLink pointing to the login route.

The logout link is a bit more interesting: we capture the click event from this link and trigger the submission of a hidden form. This form sends a POST request to the /logout server route, which logs the user out and redirects them back to the home page. Note that we must include the CSRF token as a hidden input for this to work.

resources/assets/components/App.vue:

```html
<template>
    <div>
        <div id="toolbar">
            <router-link :to="{name:'home'}">
                <img src="/images/logo.png" class="icon">
                <h1>vuebnb</h1>
            </router-link>
            <ul class="links">
                <li>
                    <router-link :to="{ name:'saved' }">Saved</router-link>
                </li>
                <li>
                    <router-link :to="{ name:'login' }">Log In</router-link>
                </li>
                <li>
                    <a @click="logout">Log Out</a>
                    <form action="/logout" style="display:hidden" method="POST"
                    id="logout">
                        <input type="hidden" name="_token" :value="csrf_token">
                    </form>
                </li>
            </ul>
        </div>
        <router-view></router-view>
        <custom-footer></custom-footer>
    </div>
</template>

<script>
import CustomFooter from './CustomFooter';
    export default {
        components: {
            CustomFooter,
        },
        data() {
            return {
                csrf_token: window.csrf_token,
            }
        },
        methods: {
            logout() {
            document.getElementById('logout').submit();
            }
        },
    }
</script>
```

### 9.6 Protecting the saved route

We can use our login system now to protect certain routes from guests, that is, unauthenticated users. Laravel provides the auth middleware, which can be applied to any route and will redirect a guest user to the login page if they attempt to access it. Let's apply this to our saved page route.

routes/web.php:

```php
Route::get('/saved', 'ListingController@get_home_web')->middleware('auth');
```

If you log out of the application and attempt to access this route from the navigation bar of your browser, you'll find it redirects you back to /login.

### 9.7 Passing authentication state to the frontend

We now have a complete mechanism for logging users in and out of Vuebnb. However, the frontend app is not yet aware of the user's authentication state. Let's remedy that now so we can add authentication-based features to the frontend.

#### 9.7.1 auth meta property

We'll begin by adding the authentication state to the meta information we pass through in the head of each page. We'll utilize the Auth facade check method, which returns true if the user is authenticated, and assign this to a new auth property.

app/Http/Controllers/ListingController.php:

```php
... 
use Illuminate\Support\Facades\Auth; 

class ListingController extends Controller { 
    ... 
    private function add_meta_data($collection, $request) { 
        return $collection->merge([ 
            'path' => $request->getPathInfo(), 
            'auth' => Auth::check() 
        ]); 
    } 
}
```

1『码了一遍后发现，登录不进去，在 vuex 里看 state 里的 auth 属性值一直是 false。后来发现代码写错位置了，写在了「LoginController.php」，应该是写在「ListingController.php」。说到底还是对整个项目的数据流向没有完全掌握。（2020-05-02）』

We'll also add an auth property to our Vuex store. We'll mutate it from the addData method which, as you'll recall from the previous chapter, is where we retrieve data from the document head or API. Since the API does not include meta data, we'll conditionally mutate the auth property to avoid accessing a potentially undefined object property.

resources/assets/js/store.js:

```js
export default new Vuex.Store({
    state: {
        saved: [5, 10],
        listing_summaries: [],
        listings: [],
        auth: false,
    },
    mutations: {
        toggleSaved(state, id) {
            let index = state.saved.findIndex(saved => saved === id);
            if (index === -1) {
                state.saved.push(id);
            } else {
                state.saved.splice(index, 1);
            }
        },
        addData(state, {route, data}) {
            if (data.auth) {
                state.auth = data.auth;
            } if (route === 'listing') {
                state.listings.push(data.listing);
            } else {
                state.listing_summaries = data.listings;
            }
        },
    },
    getters: {
        getListing(state) {
            return id => state.listings.find(listing => id == listing.id);
        }
    },
});
```

With that done, Vuex is now tracking the authentication state of the user. Be sure to test this out by logging in and out and noticing the value of auth in the Vuex tab of Vue Devtools:

Figure 9.6. Value of auth in Vue Devtools

#### 9.7.2 Responding to authenticated state

Now that we're tracking the authentication state of the user, we can get Vuebnb to respond to it. For one, let's make it so that a user can't save a listing unless they're logged in. To do this, we'll modify the behavior of the toggleSaved mutator method so that if the user is logged in they can save an item, but if not they are redirected to the login page via the push method of Vue Router. Note that we'll have to import our router module at the top of the file to access its features.

resources/assets/js/store.js:

```js
toggleSaved(state, id) {
    if (state.auth) {
        let index = state.saved.findIndex(saved => saved === id);
        if (index === -1) {
            state.saved.push(id);
        } else {
            state.saved.splice(index, 1);
        }
    } else {
        router.push('/login');
    }
},
```

We'll also make it so that either the login link or the logout link is shown in the toolbar, never both. This can be achieved by using v-if and v-else directives in the toolbar that depend on the \$store.state.auth value. It would also make sense to hide the saved page link unless the user is logged in, so let's do that as well.

resources/assets/components/App.vue:

```html
<ul class="links">
    <li v-if="$store.state.auth">
        <router-link :to="{ name:'saved' }">Saved</router-link>
    </li>
    <li v-if="$store.state.auth">
        <a @click="logout">Log Out</a>
        <form action="/logout" style="display:hidden" method="POST"
        id="logout">
            <input type="hidden" name="_token" :value="csrf_token">
        </form>
    </li>
    <li v-else>
        <router-link :to="{ name:'login' }">Log In</router-link>
    </li>
</ul>
```

This is how the toolbar will look now, depending on whether the user is logged in or out:

### 9.8 Retrieving saved items from the database

Let's now work on retrieving the saved items from the database and displaying them in the frontend. To begin with, we'll add a new saved property to the metadata we put in the document head. This will be an empty array if the user is logged out, or the array of saved listing IDs associated with that user, if they're logged in.

app/Http/Controllers/ListingController.php:

```php
private function add_meta_data($collection, $request) {
    return $collection->merge([
        'path' => $request->getPathInfo(),
        'auth' => Auth::check(),
        'saved' => Auth::check() ? Auth::user()->saved : [],
    ]);
}
```

Back in the frontend, we'll put the logic for retrieving the saved items in the beforeEach router navigation guard. The reason we put it here and not in the addData mutation is that we don't want to directly assign the data to the store state, but instead call the toggleSaved mutation for each of the listings. You can't commit a mutation from another mutation, so this must be done outside the store.

resources/assets/js/router.js:

```js
router.beforeEach((to, from, next) => {
    let serverData = JSON.parse(window.vuebnb_server_data);
    if (
        to.name === 'listing'
          ? store.getters.getListing(to.params.listing)
          : store.state.listing_summaries.length > 0
          || to.name === 'login'
    ) {
    next();
    } else if (!serverData.path || to.path !== serverData.path) {
        axios.get(`/api${to.path}`).then(({data}) => {
            store.commit('addData', {route: to.name, data});
            next();
        });
    } else {
        store.commit('addData', {route: to.name, data: serverData});
        serverData.saved.forEach(id => store.commit('toggleSaved', id));
        next();
    }
});
```

Let's also remove the placeholder listing IDs we added to saved in the previous chapter so the store is empty upon initialization.

resources/assets/js/store.js:

```js
state: {
    saved: [],
    listing_summaries: [],
    listings: [],
    auth: false,
},
```

With that done, we should find that the saved listings in the database now match those in the frontend if we check with Vue Devtools:

### 9.9 Persisting saved listings

The mechanism for persisting saved listings is as follows: when a listing is toggled in the frontend app, we trigger an AJAX request that POSTs the ID to a route on the backend. This route calls a controller that will update the model:

Figure 9.9. Persisting saved listings

Let's now implement this mechanism.

1『上面的逻辑图需仔细消化。因为这一节的代码还没实现。（2020-05-02）』

#### 9.9.1 Creating an API route

We'll begin on the server side and add a route for the frontend to POST listing IDS to. We'll need to add the auth middleware so that only authenticated users can access this route (we'll discuss the meaning of :api shortly).

routes/api.php:

```php
...

Route::post('/user/toggle_saved', 'UserController@toggle_saved')->middleware('auth:api');
```

Since this is an API route, its full path will be /api/user/toggle\_saved. We haven't yet created the controller that this route calls, UserController, so let's do that now:

    $ php artisan make:controller UserController

In this new controller, we'll add the toggled\_saved handling method. Since this is an HTTP POST route, this method will have access to the form data. We'll make it so that the frontend AJAX call to this route includes an id field, which will be the listing ID we want to toggle. To access this field, we can use the Input facade, that is, Input::get('id');.

1『 laravel 6 开始，已经取消了 Input。搜索得到的信息「Input:: is replaced with Request::」。』

Since we're using the auth middleware on this route, we can retrieve the user model associated with the request by using the Auth::user() method. We can then either add or remove the ID from the user's saved listings, just as we do in the toggledSaved method in our Vuex store. Once the ID is toggled, we can then use the model's save method to persist the update to the database.

app/Http/Controllers/UserController.php:

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Illuminate\Support\Facades\Auth;

class UserController extends Controller
{
    public function toggle_saved() {
        $id = Request::get('id');
        $user = Auth::user();
        $saved = $user->saved;
        $key = array_search($id, $saved);
        if ($key === FALSE) {
            array_push($saved, $id);
        } else {
            array_splice($saved, $id);
        }
        $user->saved = $saved;
        $user->save();
        return response()->json();
    }
}
```

#### 9.9.2 Vuex actions

In Chapter 8, Managing Your Application State With Vuex, we discussed the key principles of the Flux pattern, including the principle that mutations must be synchronous to avoid race conditions that make our application data unpredictable.

1『核心知识点：Flux pattern 的原则是「mutations must be synchronous」。』

If you have a need to include asynchronous code in a mutator method, you should instead create an action. Actions are like mutations, but instead of mutating the state, they commit mutations. For example:

```js
var store = new Vuex.Store({ 
    state: { val: null }, 
    mutations: { 
        assignVal(state, payload) { 
            state.val = payload; 
        } 
    }, 
    actions: { 
        setTimeout(() => { 
            commit('assignVal', 10); 
        }, 1000) 
    } 
}); 

store.dispatch('assignVal', 10);
```

By abstracting asynchronous code into actions we can still centralize any state-altering logic in the store without tainting our application data through race conditions.

#### 9.9.3 AJAX request

Let's now use AJAX to make the request to /api/user/toggle\_saved when a listing is saved. We'll put this logic into a Vuex action so that the toggleSaved mutation is not committed until the AJAX call resolves. We'll import the Axios HTTP library into the store to facilitate this. Also, let's move the authentication check from the mutation to the action, as it makes sense to do this check before the AJAX call is initiated.

resources/assets/js/store.js:

```js
import axios from 'axios'; 

export default new Vuex.Store({
    state: {
        saved: [],
        listing_summaries: [],
        listings: [],
        auth: false,
    },
    mutations: {
        // 修改内容
        toggleSaved(state, id) {
            let index = state.saved.findIndex(saved => saved === id);
            if (index === -1) {
                state.saved.push(id);
            } else {
                state.saved.splice(index, 1);
            }
        },
        addData(state, {route, data}) {
            if (data.auth) {
                state.auth = data.auth;
            } if (route === 'listing') {
                state.listings.push(data.listing);
            } else {
                state.listing_summaries = data.listings;
            }
        },
    },
    // 修改内容
    actions: {
        toggleSaved({commit, state}, id) {
            if (state.auth) {
                axios.post('/api/user/toggle_saved', {id}).then(
                    () => commit('toggleSaved', id)
                );
            } else {
                router.push('/login');
            }
        },
    },
    getters: {
        getListing(state) {
            return id => state.listings.find(listing => id == listing.id);
        }
    },
});
```

We now need to call the toggledSaved action, not the mutation, from our ListingSave component. Calling an action is done in exactly the same way as a mutation, only the terminology changes from commit to dispatch.

resources/assets/components/ListingSave.vue:

```js
toggleSaved() { 
    this.$store.dispatch('toggleSaved', this.id); 
}
```

The code for this feature in the frontend is correct, but if we test it out and try and save an item we get a 401 Unauthenticated error from the server:

Figure 9.10. AJAX call results in a 401 Unauthenticated error

1『

我的报错是 405：

````
app.js:285 POST http://localhost:8000/api/user/toggle_saved 405 (Method Not Allowed)

app.js:699 Uncaught (in promise) Error: Request failed with status code 405
    at createError (app.js:699)
    at settle (app.js:960)
    at XMLHttpRequest.handleLoad (app.js:168)
```

』

### 9.10 API authentication

We added the auth middleware to our /api/user/toggle\_saved route to protect it from guest users. We also specified the api guard for this middleware, that is, auth:api. 

Guards define how users are authenticated and are configured in the following file.

config/auth.php:

```php
<?php 

return [ 
    ... 
    'guards' => [ 
        'web' => [ 
            'driver' => 'session', 
            'provider' => 'users', 
        ], 
    'api' => [ 
        'driver' => 'token', 
        'provider' => 'users', 
        ], 
    ], 
    ... 
];
```

Our web routes use the session driver which maintains authentication state using session cookies. The session driver ships with Laravel and works out-of-the-box. API routes, though, use the token guard by default. We have not yet implemented this driver, hence our AJAX calls are unauthorized.

We could use the session driver for API routes as well, but this is not recommended, as session authentication is not sufficient for AJAX requests. We're instead going to use the passport guard, which implements the OAuth protocol. You may see auth used as a shorthand for auth:web, as the web guard is the default.

#### 9.10.1 OAuth

OAuth is an authorization protocol that allows third-party applications to access a user's data on a server without exposing their password. Access to this protected data is given in exchange for a special token that is granted to the application once it, and the user, have identified themselves to the server. A typical use case for OAuth is social login, for example, when you utilize a Facebook or Google login for your own website.

One challenge of making secure AJAX requests is that you can't store any credentials in the frontend source code, as it's trivial for an attacker to find these. A simple implementation of OAuth, where the third-party application is actually your own frontend app, is a good solution to the issue. This is the approach we'll be taking now for Vuebnb.

While OAuth is a great solution for API authentication, it is also quite an in-depth topic that I can't fully cover in this book. I recommend you read this guide to get a better understanding: https://www.oauth.com/.

3『 [OAuth.com - OAuth 2.0 Simplified](https://www.oauth.com/) 』

#### 9.10.2 Laravel Passport

Laravel Passport is an implementation of OAuth that can easily be set up in a Laravel application. Let's install it now for use in Vuebnb. First, install Passport with Composer:

    $ composer require laravel/passport

Passport includes new database migrations that generate the tables needed to store OAuth tokens. Let's run the migration:

    $ php artisan migrate

The following command will install the encryption keys needed to generate secure tokens:

    $ php artisan passport:install

1『

跑完显示：

```
Encryption keys generated successfully.
Personal access client created successfully.
Client ID: 1
Client secret: VWJozkalVgeChffQwgB9UpjKUnxAxShcLxvEPHQH
Password grant client created successfully.
Client ID: 2
Client secret: yR1MrVUhgRpVYC51gc6XGgeQt7TkEoplV5sWKhil
```

』

After running this command, add the Laravel\Passport\HasApiTokens trait to the user model.

app/User.php:

```php
<?php 

...

use Laravel\Passport\HasApiTokens; 

class User extends Authenticatable { 
    use HasApiTokens, Notifiable; 
    ... 
}
```

Finally, in the config/auth.php configuration file, let's set the driver option of the API guard to passport. This ensures the auth middleware will use Passport as a guard for API routes.

config/auth.php:

```php
'guards' => [
    'web' => [
        'driver' => 'session',
        'provider' => 'users',
    ],

    'api' => [
        'driver' => 'passport',
        'provider' => 'users',
        'hash' => false,
    ],
],
```

#### 9.10.3 Attaching tokens

OAuth requires an access token to be sent to the frontend app when the user logs in. Passport includes a middleware that can handle this for you. Add the CreateFreshApiToken middleware to the web middleware group and the laravel\_token cookie will be attached to outgoing responses.

app/Http/Kernel.php:

```php
protected $middlewareGroups = [ 
    'web' => [ 
        ... 
        \Laravel\Passport\Http\Middleware\CreateFreshApiToken::class, 
    ], 
...
```

For outgoing requests, we need to add some headers to our AJAX calls. We can make it so Axios automatically attaches these by default. 'X-Requested-With': 'XMLHttpRequest' ensures that Laravel knows the request was from AJAX, while 'X-CSRF-TOKEN': window.csrf\_token attaches the CSRF token.

resources/assets/js/store.js:

```
... 
axios.defaults.headers.common = {
    'X-Requested-With': 'XMLHttpRequest', 
    'X-CSRF-TOKEN': window.csrf_token,
};

export default new Vuex.Store({ ... });
```

With that done, our API requests should now be properly authenticated. To test this, let's use Tinker to see which items we have saved for our first seeded user:

```
$ php artisan tinker 

>>> DB::table('users')->select('saved')->first(); # "saved": "[1,5,7,9]"
```

Make sure you're logged in as that user and load Vuebnb in the browser. Toggle a few of your saved listing selections and rerun the query above. You should find that the database is now persisting the saved listing IDs.

1『

还是没解决之前的问题，报错 405，目前没能力解决，设计到很多异步的算法，待解决。（2020-05-02）

先回滚到好的版本「git reset --hard 0fe0f773908f1e」->「HEAD is now at 0fe0f77 0909-Creating an API route」，后面有时间以此点开始试验解决该问题。

』

## 1001. Deploying a Full-Stack App to the Cloud

Now that the functionality of Vuebnb is complete, the final step is to deploy it to production. We'll use two free services, Heroku and KeyCDN, to share Vuebnb with the world. Topics covered in this chapter: 1) An introduction to the Heroku cloud platform service. 2) Deploying Vuebnb to Heroku as a free app. 3) How CDNs improve the performance of full-stack apps. 4) Integrating a free CDN with Laravel. 5) Building assets in production-mode for performance and security.

### Summary

In this chapter, we learned how to deploy a full-stack app to a Heroku cloud server. To do this, we used the Heroku CLI to set up a new Heroku app, and then deployed it using Heroku's Git server. We also created a CDN with KeyCDN, and used FTP to deploy our static assets to the CDN. Finally, we learned why it's important for performance and security to build our JavaScript assets in production-mode ahead of deployment.

### 10.1 Heroku

Heroku is a cloud platform service for web applications. It's immensely popular among developers due to the simplicity and affordability it offers for getting apps online. Heroku applications can be made in a variety of languages including PHP, JavaScript, and Ruby. In addition to a web server, Heroku offers a variety of add-ons, such as databases, email services, and application monitoring. Heroku apps can be deployed for free, though there are certain limitations, for example, the app will sleep after periods of inactivity, making it slow to respond. These limitations are lifted if you upgrade to a paid service. 

3『 [Heroku | Sign up](https://signup.heroku.com/) 』

1『后面的都是部署相关的知识，暂时留着，有需求的时候再看。』

### 10.2 Reading from the CDN

We now want Vuebnb to load any static assets from the CDN instead of the web server when in production. To do this, we're going to create our own Laravel helper method. Currently, we reference assets in our app using the asset helper. This helper returns a fully-qualified URL for that asset's location on the web server. For example, in our app view we link to the JavaScript bundle file like this:

```html
<script type="text/javascript" src="{{ asset('js/app.js') }}"></script>
```

Our new helper, which we'll call cdn, will instead return a URL that points to the asset's location on the CDN:

```html
<script type="text/javascript" src="{{ cdn('js/app.js') }}"></script>
```

#### 10.2.1 CDN helper

Let's begin by creating a file called helpers.php. This will declare a new cdn method which, for now, won't do anything but return the asset helper method.

app/helpers.php:

```php
<?php 

if (!function_exists('cdn')) { 
    function cdn($asset) { 
        return asset($asset); 
    } 
}
```

To ensure this helper is available to be used anywhere in our app, we can use Composer's autoload feature. This makes a class or file available to all other files without them having to manually include or require it.

composer.json:

```json
... 
"autoload": { 
"classmap": [ ... ], 
"psr-4": { ... }, 
"files": [ "app/helpers.php" ] 
}, 

...
```

Each time you modify Composer's autoload declaration you need to run dump-autoload:

```
$ composer dump-autoload
```

With that done, the cdn helper will be available for use within our app. Let's test it with Tinker:

```
$ php artisan tinker 
>>>> cdn('js/app.js') => "http://vuebnb.test/js/app.js"
```

#### 10.2.2 Setting the CDN URL

The cdn helper method will need to know the URL of the CDN. Let's set an CDN\_URL environment variable that will be assigned the zone URL for Vuebnb, minus the protocol prefix. While we're at it, let's add another variable, CDN\_BYPASS, that can be used to bypass the CDN in our local development environment where we won't need it.

.env:

```
... 
CDN_URL=vuebnb-9c0f.kxcdn.com 
CDN_BYPASS=0
```

Let's now register these new variables in the app configuration file.

config/app.php:

```
<?php 
return [ 

    ... 
    // CDN 
    'cdn' => [ 
        'url' => env('CDN_URL'), 
        'bypass' => env('CDN_BYPASS', false), 
    ], 
];
```

Now we can complete the logic of our cdn helper.

app/helpers.php:

```php
<?php 
use Illuminate\Support\Facades\Config; 

if (!function_exists('cdn')) { 
    function cdn($asset) { 
        if (Config::get('app.cdn.bypass') || !Config::get('app.cdn.url')) { 
            return asset($asset); 
            } else { 
                return "//" . Config::get('app.cdn.url') . '/' . $asset; 
        } 
    } 
}
```


If you still have Tinker open, exit and re-enter, and test the changes work as expected:

```
>>>> exit
$ php artisan tinker 
>>>> cdn('js/app.js') => "//vuebnb-9c0f.kxcdn.com/js/app.js"
```

#### 10.2.3 Using the CDN in Laravel

Let's now replace usages of the asset helper in our Laravel files with the cdn helper.

app/Http/Controllers/ListingController.php:

```php
<?php 
... 

class ListingController extends Controller { 
    private function get_listing($listing) { 
    ... 
    for($i = 1; $i <=4; $i++) { 
        $model['image_' . $i] = cdn('images/' . $listing->id . '/Image_' . $i . '.jpg'); 
    } 
    ... 
    } 

    ... 
    private function get_listing_summaries() { 
        ... 
        $collection->transform(function($listing) { 
            $listing->thumb = cdn( 'images/' . $listing->id . '/Image_1_thumb.jpg' ); 
            return $listing; 
        }); 
        ... 
    } 
    ... 
}
```

resources/views/app.blade.php:

```html
<html> 
    <head> 
        ... 
        <link rel="stylesheet" href="{{ cdn('css/style.css') }}" type="text/css"> 
        <link rel="stylesheet" href="{{ cdn('css/vue-style.css') }}" type="text/css"> ... 
    </head> 
    <body> 
        ... 
        <script src="{{ cdn('js/app.js') }}"></script> 
    </body> 
</html>
```

#### 10.2.4 Using the CDN in Vue

In our Vue app, we're loading some static assets as well. For example, in the toolbar we use the logo.

resources/assets/components/App.vue:

```html
<img class="icon" src="/images/logo.png">
```

As this is a relative URL it will, by default, point to the web server. If we make it an absolute URL instead, we'd have to hard-code the CDN URL, which is not ideal either.

Let's instead get Laravel to pass the CDN URL in the head of the document. We can do this by simply calling the cdn helper with an empty string.

resources/views/app.blade.php:

```html
<head> 
    ... 
    <script type="text/javascript"> 
        ...
        window.cdn_url = "{{ cdn('') }}"; 
    </script> 
</head>
```

We'll now use a computed property to construct the absolute URL using this global value.

resources/assets/components/App.vue:

```html
<template> 
    ... 
    <router-link :to="{ name: 'home' }"> 
        <img class="icon" :src="logoUrl"> 
        <h1>vuebnb</h1> 
    </router-link> 
    ... 
</template> 

<script> 
    export default { 
        computed: { 
            logoUrl() { 
                return `${window.cdn_url || ''}images/logo.png`; 
            } 
        }, 
        ... 
    } 
</script> 

<style>...</style>
```

We'll use the same concept in the footer where the grey logo is used.

resources/assets/components/CustomFooter.vue:

```html
<template> 
    ... 
    <img class="icon" :src="logoUrl"> 
    ... 
</template> 

<script> 
    export default { 
        computed: { 
            containerClass() { ... }, 
            logoUrl() { 
                return `${window.cdn_url || ''}images/logo_grey.png`; 
            } 
        }, 
    } 
</script>
```

### 10.3 Deploying to Heroku

With that done, commit any file changes to Git and push again to Heroku to trigger a new deploy. You'll also need to rebuild your frontend assets and transfer these to the CDN. Finally, set the CDN environment variables:

```
$ heroku config:set \ 
CDN_BYPASS=0 \ 
CDN_URL=vuebnb-9c0f.kxcdn.com
```

Finale. You have now completed the case-study project for this book, a sophisticated full-stack Vue.js and Laravel application. Congratulations!

## Next steps

You may have reached the end of the book, but your journey as a full-stack Vue developer has only just begun! What should you move on to next?

Firstly, there are still plenty more features you can add to Vuebnb. Designing and implementing these yourself will increase your skill and knowledge immensely. Here are a few ideas to get you started: 1) Complete the user authentication flow. Add a registration page and functionality for resetting passwords. 2) Add a user profile page. Here, users can upload an avatar that will display in the toolbar when they're logged in. 3) Create a form on the listing page that allows the room to be booked. Include a drop-down datepicker widget for selecting start and end dates. 4) Server render the app by running Vue from a JavaScript sandbox on the server. This way users get a complete page with visible content when they load the site.

Secondly, I invite you to check out Vue.js Developers, an online community for Vue.js enthusiasts that I founded. Here you can read articles on Vue.js, stay up-to-date with Vue.js news through our newsletter, and share tips and tricks with other developers in our Facebook group. Check it out at this URL: https://vuejsdevelopers.com.

3『[Latest posts - Vue.js Developers](https://vuejsdevelopers.com/) 』
