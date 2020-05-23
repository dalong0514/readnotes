# The Ultimate AJAX Guide For Vue.js Apps

Anthony Gore | August 28th, 2017 (Updated January 20th, 2020) | 8 min read

[The Ultimate AJAX Guide For Vue.js Apps - Vue.js Developers](https://vuejsdevelopers.com/2017/08/28/vue-js-ajax-recipes/)

If you ask two Vue.js developers "what's the best way to implement AJAX in a Vue app?", you'll get three different opinions.

Vue is a UI library and therefore doesn't provide an official way of implementing AJAX. There are a number of different approaches that may be used effectively, each with its pros and cons that should be considered against your requirements.

In this article, I'll first show you how to AJAX-enable a Vue app before getting into the most useful patterns for managing AJAX requests. I'll explain each pattern, give an example, and cover the pros and cons as well.

Table of contents:

What is AJAX?
AJAX-enabling a Vue app
Working with asynchronous code
Handling errors
UX considerations
Architectural patterns
Pattern #1. From the root instance
Pattern #2. From components
Pattern #3. From Vuex actions
Pattern #4. From route navigation guards
Pattern #5. From a service module
Pattern #6. Server-render initial page state instead of using AJAX
What is AJAX?
AJAX (Asynchronous JavaScript and XML) is a way of communicating from a client-side application to a web server over HTTP. If you ever want to read or write data from a Vue.js app, you'll most likely consider AJAX.

Of course, you'll need to work with a web server that has publicly accessible endpoints e.g. GET /items. AJAX will allow your Vue app to request that endpoint any time in its lifecycle.

AJAX-enabling a Vue app
AJAX can be implemented in any JavaScript app by using native web APIs including XMLHttpRequest or the more recent Fetch API.

However, using these APIs directly will require tedious boilerplate, and in the case of Fetch, a polyfill for older browsers. So the recommended method amongst most web devs is to use an HTTP client library like Axios.

The easiest way to add an HTTP client to a Vue app is by using a Vue plugin. The best known are Vue Axios, which simply wraps the Axios library and Vue Resource.

I'm a fan of Vue Axios, so let's see how to install that. Firstly, install Axios and Vue Axios from the command line:

$ npm i axios vue-axios --save
Now, import Axios and Vue Axios and install them on the Vue instance:

app.js

import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'
 
Vue.use(VueAxios, axios)
With that done, the Axios will be accessible from anywhere in your Vue app from the instance property $http:

SomeComponent.vue

export default {
  ...
  methods: {
    myMethod () {
      this.$http.post(
        '/api/items', 
        { name: "my item" }
      );
    }
  }
}
Here we're using the post method of Axios to POST data. If you want to see all the available methods of Axios take a look at the docs here.

Working with asynchronous code
AJAX calls are, by definition, asynchronous, so we must use asynchronous JavaScript code to handle requests. It's a good idea to get yourself comfortable with both the Promise API and with async/await syntax which, in 2020, is generally considered the easiest way to write async JS.

Most HTTP clients, and the Fetch API, will return a Promise from an AJAX request. Here we can see how Axios returns a Promise which we can get await for the result in an async method.

SomeComponent.vue

export default {
  ...
  methods: {
    async myMethod () {
      const { data } = await this.$http.patch(
        '/api/items/1', 
        { name: "something" }
      );
      console.log(data);
      // example response: { id: 1, name: "something" }
    }
  }
}
Handling errors
Sometimes things go wrong. Maybe the user's connection drops or some knucklehead changes the API response format without telling you.

You should ensure your application can handle such a situation by using try/catch:

SomeComponent.vue

export default {
  ...
  methods: {
    async myMethod () {
      try {
        const { data } = await this.$http.patch(
          '/api/items/1', 
          { name: "something" }
        );
        // do stuff
      } catch (err) {
        // uh oh, didn't work, time for plan B
      }
    }
  }
}
UX considerations
When AJAX calls are made across the internet there will be a delay between when the request is made, and when the request is resolved, with the length depending on both the internet connection speed and the latency of the web server.

It's good UX to let the user know what's going on by reflecting the AJAX state in the interface. One way to do this is to create a boolean flag isLoading that gets set to true before an AJAX call is initiated, then set to false when it completes.

Thanks to Vue reactivity, this flag can be used in the template to conditionally show a "Loading" message or perhaps a spinner.

In this example, I'm using two flags - isLoading and also isError to cover all bases.

SomeComponent.vue

export default {
  data: () => ({
    ...
    isLoading: false,
    isError: false
  }),
  methods: {
    async myMethod () {
      try {
        this.isLoading = true;
        const { data } = await this.$http.patch(
          '/api/items/1', 
          { name: "something" }
        );
      } catch (err) {
        this.isError = true;
      } finally {
        this.isLoading = false;
      }
    }
  }
}
We can now make the template reflect the loading/error/ok state giving the user valuable feedback:

SomeComponent.vue

<template>
  <div class="wrapper">
    <div v-if="isError">...</div>
    <div v-else-if="isLoading">...</div>
    <div v-else>...</div>
  </div>
</template>
Architectural patterns
Okay, so now you know how to make your Vue app AJAX-enabled. Where should you begin making AJAX calls in your app?

For the rest of this article, I'm going to cover the most common patterns that you might want to use.

Pattern #1. From the root instance
With this pattern, you issue all your AJAX requests from the root instance and store all state there too. If any sub-components need data, it will come down as props. If sub-components need refreshed data, a custom event will be used to prompt the root instance to request it.

Example:

App.vue

<template>
  <some-component :message="message" @refresh-message="refreshMessage" />
</template>
<script>
import SomeComponent from "@/components/SomeComponent";
export default {
  data: {
    message: ''
  },
  methods: {
    async refreshMessage(resource) {
      const response = await this.$http.get('/message');
      this.message = response.data.message;
    }
  },
  components: {
    SomeComponent
  }
};
</script>
SomeComponent.vue

<template>
  <div>{{ message }}</div>
</template>
<script>
export default {
  props: [ 'message' ]
  methods: {
    refreshMessage() {
      this.$emit('refresh-message');
    }
  }
};
</script>
Pros

Keeps all your AJAX logic and data in one place.
Keeps your components "dumb" so they can focus on presentation.
Cons

A lot of props and custom events needed as your app expands.
Pattern #2. From components
With this architecture, components are responsible for managing their own AJAX requests and state independently. In practice, you'll probably want to create several "container" components that manage data for their local group of "presentational" components.

For example, filter-list might be a container component wrapping filter-input and filter-reset, which serve as presentational components. filter-list would contain the AJAX logic and would manage data for all the components in this group, communicating via props and events.

See Presentational and Container Components by Dan Abramov for a better description of this pattern.

To make the implementation of this architecture easier, you can abstract any AJAX logic into a mixin, then use the mixin in a component to make it AJAX-enabled.

app.js

let mixin = {
  methods: {
    refreshMessage() {
      ...
    }
  }
}

Vue.component('container-comp', {
  // No meaningful template, I just manage data for my children
  template: '<div><presentation-comp :mydata="mydata"></presentation-comp></div>', 
  mixins: [ myMixin ],
  data() {
    return { ... }
  },

})

Vue.component('presentation-comp', {
  template: '<div>I just show stuff like {{ mydata }}</div>',
  props: [ 'mydata' ]
})
Pros

Keeps components decoupled and reusable.
Gets the data when and where it's needed.
Cons

Not easy to communicate data with other components or groups of components.
Components can end up with too many responsibilities and duplicate functionality.

Join Our Next Live Workshop Online!
"Making Vue.js Apps Enterprise Ready" - May 27th, 2020, 5-6pm PDT
Pattern #3. From Vuex actions
With this architecture, you manage AJAX logic in your Vuex store. Note that you'll need to import Axios in your store file rather than using the Vue Axios plugin, as Vuex does not have access to the Vue instance.

store.js

import axios from "axios";

store = new Vuex.Store({
  state: {
    message: ''
  },
  mutations: {
    updateMessage(state, payload) {
      state.message = payload
    }
  },
  actions: {
    async refreshMessage(context) {
      const response = await axios.get('...');
      context.commit('updateMessage', response.data.message);
    }
  }
});

export default store;
Now components can request new data by dispatching an action.

MyComponent.vue

<template>
  <div>{{ message }}</div>
</template>
<script>
export default {
  template: '',
  methods: {
    refreshMessage() {
      this.$store.dispatch('refeshMessage');
    }
  },
  computed: {
    message: { return this.$store.state.message; }
  }
}
</script>
Pros

Decouples your state and presentation logic
All the pros of the root component architecture, without needing props and custom events.
Cons

Adds the overhead of Vuex.
Pattern #4. From route navigation guards
With this architecture, your app is split into pages, and all data required for a page and its sub-components is fetched when the route is changed.

The main advantage of this approach is that it simplifies your UI. If components are independently getting their data, the page will re-render unpredictably as component data gets populated in an arbitrary order.

A neat way of implementing this is to create endpoints on your server for each page e.g. /about, /contact, etc, which match the route names in your app. Then you can implement a generic beforeRouteEnter hook that will merge all the data properties into the page component's data:

router.js

import axios from 'axios';

...

router.beforeRouteEnter(async (to, from, next) => {
  const { data } = await axios.get(`/api${to.path}`);
  next(vm => Object.assign(vm.$data, data));
});
Pros

Makes the UI more predictable.
Cons

Slower overall, as the page can't render until all the data is ready.
Not much help if you don't use routes.
Pattern #5. From a service module
"Separation of concerns" is the idea that classes/modules/files should have just one job. This principle ensures your code is easy to read and maintain.

To abide by that principle, we should try to keep AJAX logic out of our components (which are for presentation) and out of Vuex (which is for state).

A good way to achieve this is by abstracting AJAX into a separate module. In this case, we probably wouldn't need the vue-axios plugin anymore, and can instead use Axios directly.

services/http.js

import "axios" from "axios";

export default {
  async getPost(id) {
    const { data } = await axios.get(`/posts/${id}`);
    return data;
  }
  ...
}
Now you can call this from anywhere in the Vue app - components, Vuex, or whatever floats your boat.

Post.vue

import http from "@/services/http";
export default {
  props: {
    id: String
  },
  data: () => ({
    post: null
  }),
  async created () {
    this.post = await http.getPost(this.id);
  }
}
Tip: you might even want to add your HTTP service to the Vue instance so it can be accessed from anywhere within the app e.g. this.$http.getPost();

Pattern #6. Server-render initial page state instead of using AJAX
Let's say your first page load includes server data as part of the state e.g. <p>Hello {{ name }}!</p>.

It's not advisable to use AJAX to retrieve application state on the initial page load, as it requires an extra round-trip to the server that will delay your app from rendering.

Instead, inject initial application state into an inline script in the head of the HTML page so it’s available to the app as a global variable as soon as it’s needed.

<html>
...
<head>
  ...
  <script type="text/javascript">
    window.__INITIAL_STATE__ = '{ "data": [ ... ] }';
  </script>
</head>
<body>
  <div id="app"></div>
</body>
</html>
AJAX can then be used for subsequent data fetches.

If you're interested in learning more about this architecture, check out my article Avoid This Common Anti-Pattern In Full-Stack Vue/Laravel Apps.

Anthony Gore
About Anthony Gore
I'm Anthony Gore and I'm here to teach you Vue.js! Through my books, online courses, and social media, my aim is to turn you into a Vue.js expert.

I'm a Vue Community Partner, curator of the weekly Vue.js Developers Newsletter, and the creator of Vue.js Developers.

If you enjoyed this article, show your support by buying me a coffee, and if you'd like to support me ongoingly, you can make a pledge through Patreon.

Follow Anthony Gore on Twitter