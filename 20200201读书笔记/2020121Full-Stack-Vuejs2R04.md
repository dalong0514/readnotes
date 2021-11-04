## 附件01-Avoid-This-Common-Anti-Pattern.md

If you want your Vue.js single-page app to communicate with a Laravel backend, you will, quite reasonably, think of using AJAX. Indeed, Laravel comes with the Axios library loaded in by default. However, it's not advisable to use AJAX to retrieve application state on the initial page load, as it requires an extra round-trip to the server that will delay your Vue app from rendering.

1『不建议在首页获取数据信息。』

3『

[Pre-Render A Vue.js App (With Node Or Laravel) - Vue.js Developers](https://vuejsdevelopers.com/2017/04/01/vue-js-prerendering-node-laravel/)

[The Ultimate AJAX Guide For Vue.js Apps - Vue.js Developers](https://vuejsdevelopers.com/2017/08/28/vue-js-ajax-recipes/)

[Advanced Server-Side Rendering With Laravel & Vue: Multi-Page App - Vue.js Developers](https://vuejsdevelopers.com/2017/11/27/vue-js-laravel-server-side-rendering-router/)

』

I see many full-stack Vue/Laravel apps architected in this way. An alternative to this anti-pattern is to inject initial application state into the head of the HTML page so it's available to the app as soon as it's needed. AJAX can then be used more appropriately for subsequent data fetches.

Using this approach can get messy, though, if your app has different routes requiring different initial state. In this article, I'll demonstrate a design pattern that makes it very simple to implement this injection approach, and allows for a lot of flexibility even in multi-route apps.

As you'll shortly see, an example app I created is interactive 25% sooner when implementing this design pattern.

### 01. Passing Data To Vue From Laravel

Here's an example full-stack Vue/Laravel app I built for Oldtime Cars, a fictitious vintage car retailer. The app has a front page, which shows available cars, and a generic detail page, which shows the specifics of a particular model.

This app uses Vue Router to handle page navigation. Each page needs data from the backend (e.g. the name of the car model, the price etc), so a mechanism for sending it between Vue and Laravel is required. The standard design pattern is to setup API endpoints for each page in Laravel, then use Vue Router's beforeRouteEnter hook to asynchronously load the data via AJAX before the page transitions.

1『常规的数据请求过程：后台为每一个配一个 api，页面跳转前用 vue 的 beforeRouteEnter 钩子去异步请求数据。』

The problem with such an architecture is that it gives us this sub-optimal loading process for the initial page load:

Eliminating the AJAX request here would make the page interactive much sooner, especially on slow internet connections.

### 02. Injecting initial application state

If we inject the initial application state into the HTML page, Vue Router won't need to request it from the server, as it will already be available in the client. We can implement this by JSON-encoding the state server-side and assigning it to a global variable:

index.html

```html
<html>
...
<head>
  ...
  <script type="text/javascript">
   window.__INITIAL_STATE__ = '{ "cars": [ { "id": 1 "name": "Buick", ... }, { ... } ] }'
  </script>
</head>
<body>
  <div id="app"></div>
</body>
</html>
```

It is then trivial for the app to access and use the state:

```js
let initialState = JSON.parse(window.__INITIAL_STATE__);

new Vue({
  ...
})
```

This approach eliminates the need for an AJAX request, and reduces the initial app loading process to this:

I've supplied Lighthouse reports at the bottom of the article to show the improvement in load time.

Note: this approach won't be appropriate if the initial application state includes sensitive data. In that case, you could perhaps do a "hybrid" approach where only non-sensitive data is injected into the page and the sensitive data is retrieved by an authenticated API call.

### 03. Implementation in a multi-route app

This approach is good enough as-is in an app with only a single route, or if you're happy to inject the initial state of every page within each page requested. But Oldtime Cars has multiple routes, and it'd be much more efficient to only inject the initial state of the current page.

This means we have the following problems to address: 1) How can we determine what initial state to inject into the page request, since we don't know what page the user will initially land on? 2) When the user navigates to a different route from within the app, how will the app know whether or not it needs to load new state or just use the injected state?

#### 3.1 Navigation types

Vue Router is able to capture any route changes that occur from within the page and handle them without a page refresh. That means clicked links, or JavaScript commands that change the browser location. But route changes from the browser e.g. the URL bar, or links to the app from external pages, cannot be intercepted by Vue Router and will result in a fresh page load.

#### 3.2 Core concept of the design pattern

With that in mind, we need to ensure that each page has the required logic to get its data from either an injection into the page, or via AJAX, depending on whether the page is being loaded freshly from the server, or by Vue Router.

1『状态的切换其实就 2 种，一是 vue-router 控制的页面间路由的跳转，不涉及后台的路由。另外一个是后台路由的跳转。』

Implementing this is simpler than it sounds, and is best understood through demonstration, so let's go through the code of Oldtime Cars and I'll show you how I did it. You can see the complete code in this Github repo [ [anthonygore/oldtime-cars-vue-laravel](https://github.com/anthonygore/oldtime-cars-vue-laravel) ].

2『源码有空看下。』

### 04. Backend setup

#### 4.1 Routes

As the site has two pages, there are two different routes to serve: the home route, and the detail route. The design pattern requires that the routes be served either views, or as JSON payloads, so I've created both web and API routes for each:

routes/web.php

```php
<?php

Route::get('/', 'CarController@home_web');
Route::get('/detail/{id}', 'CarController@detail_web');

```

routes/api.php
```php
<?php

Route::get('/', 'CarController@home_api');
Route::get('/detail/{id}', 'CarController@detail_api');
```

1『老套路，2 手准备，返回页面视图以及返回纯数据对象。这是针对于在 laravel 里前后端一体化的场景，那么前后端分离该如何实现同时返回这两手呢？（2020-05-22）』

#### 4.2 Controller

I've abbreviated some of the code to save space, but the main idea is this: the web routes return a view with the initial application state injected into the head of the page (the template is shown below), while the API routes return exactly the same state, only as a payload.

(Also note that in addition to the state, the data includes a path. I'll need this value in the frontend, as you'll see shortly).

app/Http/Controllers/CarController.php

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class CarController extends Controller
{

  /* This function returns the data for each car, by id */
  public function get_cars($id) { ... }

  /* Returns a view */
  public function detail_web($id)
  {
      $state = array_merge([ 'path' => '/detail/' . $id], $this->get_cars($id));
      return view('app', ['state' => $state]);
  }

  /* Returns a JSON payload */
  public function detail_api($id)
  {
      $state = array_merge([ 'path' => '/detail/' . $id], $this->get_cars($id));
      return response()->json($state);
  }

  public function home_web() { ... }

  public function home_api() { ... }
}
```

#### 4.3 View

I'm using the same template for each page. Its only notable feature is that it will encode the state as JSON in the head:

resource/views/app.blade.php

```html
<!DOCTYPE html>
<html>
<head>
  <script type="text/javascript">
    window.__INITIAL_STATE__ = "{!! addslashes(json_encode($fields)) !!}";
  </script>
</head>
<body>
  <div id="app"...>
</body>
</html>
```

### 05. Frontend setup

#### 5.1 Router

The frontend of the app uses a standard Vue Router setup. I have a different component for each page i.e. Home.vue and Detail.vue. Note that the router is in history mode, because I want each route to treated separately.

1『如果想让每个 vue-router 被独立的处理，得使用 history 模式而非 hash 模式。』

resources/assets/js/app.js

```js
import Vue from 'vue';
import VueRouter from 'vue-router';

Vue.use(VueRouter);

import Home from './components/Home.vue';
import Detail from './components/Detail.vue';

const router = new VueRouter({
  mode: 'history',
  routes: [
    { path: '/', component: Home },
    { path: '/detail/:id', component: Detail }
  ]
});

const app = new Vue({
  el: '#app',
  router
});
```

#### 5.2 Page components

There's very little going on in the page components. The key logic is in a mixin which I'll show next.

Home.vue

```html
<template>
  <div>
    <h1>Oldtime Cars</h1>
    <div v-for="car in cars"...>
  </div>
</template>
<script>
  import mixin  from '../mixin';

  export default {
    mixins: [ mixin ],
    data() {
      return {
        cars: null
      }
    }
  };
</script>
```

#### 5.3 Mixin

1『有关 mixin 的知识点来了，其实就是一个封装方法，如果用 vue-state 管理状态的话可以不用它，哈哈。』

This mixin needs to be added to all the page components, in this case Home and Detail. Here's how it works:

1. Adds a beforeRouteEnter hook to each page component. When the app first loads, or whenever the route changes, this hook is called. It in turn calls the getData method.

2. The getData method loads the injected state and inspects the path property. From this, it determine if it can use the injected data, or if it needs to fetch new data. If the latter, it requests the appropriate API endpoint with the Axios HTTP client.

3. When the promise returned from getData resolves, the beforeRouteEnter hook will use whatever data is returned, and assign it to the data property of that component.

mixin.js

```js
import axios from 'axios';

let getData = function(to) {
  return new Promise((resolve, reject) => {
    let initialState = JSON.parse(window.__INITIAL_STATE__) || {};
    if (!initialState.path || to.path !== initialState.path) {
      axios.get(`/api${to.path}`).then(({ data }) => {
        resolve(data);
      })
    } else {
      resolve(initialState);
    }
  });
};

export default {
  beforeRouteEnter (to, from, next) {
    getData(to).then((data) => {
      next(vm => Object.assign(vm.$data, data))
    });
  }
};
```

1『上面的代码总算是吃透了，哈哈。（2020-05-22）』

By implementing this mixin, the page components have the required logic to get their initial state from either the data injected into the page, or via AJAX, depending on whether the page loaded from the server, or was navigated to from Vue Router.

## 附件02-Advanced-Server-Side-Rendering-With-Vue-Multi-Page-App.md

Anthony Gore | November 27th, 2017 | 3 min read

[Advanced Server-Side Rendering With Laravel & Vue: Multi-Page App - Vue.js Developers](https://vuejsdevelopers.com/2017/11/27/vue-js-laravel-server-side-rendering-router/)

A few weeks ago I wrote a tutorial on the new Vue server-side rendering capabilities for Laravel. That tutorial mostly focused on the set up of SSR in a Laravel environment and so I only had time to demonstrate a simple "Hello World" app with no significant features. Now I want to build on that previous tutorial and demonstrate how to server render a Vue app that includes multiple pages with Vue Router, since most of your Laravel projects will have more than one page.

You can get the completed code for this tutorial here on Github.

2『源码：[anthonygore/vue-js-laravel-multi-ssr: Source code for the article "Advanced Server-Side Rendering With Laravel & Vue: Multi-Page App"](https://github.com/anthonygore/vue-js-laravel-multi-ssr)，有空去实践下。』

### 01. Installation

This tutorial will extend the app I built in the previous article [[Server-Side Rendering With Laravel & Vue.js 2.5 - Vue.js Developers](https://vuejsdevelopers.com/2017/11/06/vue-js-laravel-server-side-rendering/)]. Make sure you're familiar with how it works and have a suitable development environment set up i.e. with the php-v8js extension installed.

If you don't have that code, clone it and set it up:

```
$ git clone https://github.com/anthonygore/vue-js-laravel-ssr
$ cd vue-js-laravel-ssr
$ cp .env.example .env
$ composer install
$ npm i
```

Then install Vue Router:

```
$ npm i --save-dev vue-router
```

3『 devDependencies 节点下的模块是我们在开发时需要用的，比如项目中使用的 gulp ，压缩 css、js 的模块。这些模块在我们的项目部署后是不需要的，所以我们可以使用 --save-dev 的形式安装。像 express 这些模块是项目运行必备的，应该安装在 dependencies 节点下，所以我们应该使用 --save 的形式安装。』

2『好好研究下 element-admin 的源码，哪些组件是安装在「dev」下的。』

### 02. Router module

We'll begin by creating a file for our router configuration that exports an instance of the router for use in the app. I've made up some sample routes with each displaying a component generated from the method pageComponent. This factory method returns a simple component that does nothing more than display the name of the page. This is all we need to prove SSR routing works.

resources/assets/js/router.js

```js
import Vue from 'vue'
import Router from 'vue-router'

Vue.use(Router);

function PageComponent(name) {
 return {
   render: h => h('h3', `Hello from the ${name} page`)
 };
}

export default new Router({
  mode: 'history',
  routes: [
    { path: '/', component: PageComponent('Home'), name: 'home' },
    { path: '/about', component: PageComponent('About'), name: 'about' },
    { path: '/contact', component: PageComponent('Contact'), name: 'contact' }
  ]
});
```

1『这里的路由器设置，跟 element-admin 里的一个套路。这里的 h3 没吃透，肯定跟本文开始展示的那个动画有关，待确认。（2020-05-22）』

In the main app file we'll now import the router module and add it to the app, just as you would in any Vue project. The app instance is then exported for use in the client and server entry files.

resources/assets/js/app.js

```js
import App from './components/App.vue';
import Vue from 'vue';
import router from './router'

export default new Vue({
  router,
  render: h => h(App)
});
```

### 03. Laravel routes

Note that our Vue Router instance is in history mode, so routes will fallback to the server when a sub-page is refreshed or loaded from the navigation bar. This means that any route that we created in the front-end app also needs to be created on the server side. They can all point to the same controller method get:

1『对 history 模式的理解又深了一点，用它的话，前端和后端的路由必须匹配。』

routes/web.php

```php
<?php

Route::get('/', 'AppController@get');
Route::get('/about', 'AppController@get');
Route::get('/contact', 'AppController@get');
```

### 04. Controller

Now we need to set up multi-page SSR in the controller. This is a modification of the logic in the base app, so make sure you're familiar with how that worked.

To SSR a multi-page app, we need to tell the Vue server app (as defined in entry-server.js) what the current URL being requested is. This will ensure that when the app loads in the sandbox, it's displaying the correct page component.

To do this we pass the URL i.e. \$request->path() through to the render method from the get method. We then store the URL in a global JavaScript variable url that will be accessible from the Vue server app when it runs in the sandbox.

app/Http/Controllers/AppController.php

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Illuminate\Support\Facades\File;
use Illuminate\Routing\Route;

class AppController extends Controller
{
  private function render($path) {
    $renderer_source = File::get(base_path('node_modules/vue-server-renderer/basic.js'));
    $app_source = File::get(public_path('js/entry-server.js'));

    $v8 = new \V8Js();

    ob_start();

    $js = 
<<<EOT
var process = { env: { VUE_ENV: "server", NODE_ENV: "production" } }; 
this.global = { process: process }; 
var url = "$path";
EOT;

    $v8->executeString($js);
    $v8->executeString($renderer_source);
    $v8->executeString($app_source);

    return ob_get_clean();
  }

  public function get(Request $request) {
    $ssr = $this->render($request->path());
    return view('app', ['ssr' => $ssr]);
  }
}
```

1『上面的逻辑感觉好复杂，没弄懂。（2020-05-22）』

### 05. Vue server app

The last major step is to modify the Vue server app so that we can programmatically set the URL rather than waiting for a user to do it. The logic for doing this is inside the Promise callback function. Here's what it does:

1. The router is set to the correct URL by pushing the global variable url.

2. When the router is ready, we see if any page components are being displayed as a result of this push, telling us the route is valid. If not, we throw a 404. If so, we return the app instance.

A Promise is used because the router loads asynchronously. Once this Promise resolves, we can use the server renderer method renderVueComponentToString to SSR the instance and finally use print to return the output back to our Laravel environment.

resources/assets/js/entry-server.js

```js
import app from './app'
import router from './router';

new Promise((resolve, reject) => {
  router.push(url);
  router.onReady(() => {
    const matchedComponents = router.getMatchedComponents();
    if (!matchedComponents.length) {
      return reject({ code: 404 });
    }
    resolve(app);
  }, reject);
})
  .then(app => {
    renderVueComponentToString(app, (err, res) => {
      print(res);
    });
  })
  .catch((err) => {
    print(err);
  });
```

### 06. App file

The SSR logic for the multi-page app is now complete. Let's create some router links in the page so we can test the app in a browser:

resources/asset/js/components/App.vue

```html
<template>
  <div id="app">
    <h1>{{ title }}</h1>
    <router-view></router-view>
    <router-link :to="{ name: 'about' }">About</router-link>
    <router-link :to="{ name: 'contact' }">Contact</router-link>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        title: 'Welcome To My Site'
      }
    }
  }
</script>
```

Loading the home page look like this:

The real test is visiting a route in the navigation bar so the server routes handle the request and hopefully SSR the app. To do so, visit http://localhost:9000/about and inspect the source markup. As you can see, it includes the rendered app at the correct URL:

## 附件03-Pre-Render-A-Vue.js-App.md

## 附件04-The-Ultimate-AJAX-Guide-For-Vue-Apps.md

If you ask two Vue.js developers "what's the best way to implement AJAX in a Vue app?", you'll get three different opinions. Vue is a UI library and therefore doesn't provide an official way of implementing AJAX. There are a number of different approaches that may be used effectively, each with its pros and cons that should be considered against your requirements. In this article, I'll first show you how to AJAX-enable a Vue app before getting into the most useful patterns for managing AJAX requests. I'll explain each pattern, give an example, and cover the pros and cons as well.

1『啥叫 pros 和 cons。回复：应该是优点和缺点的意思。（2020-05-25）』

### 01. What is AJAX?

AJAX (Asynchronous JavaScript and XML) is a way of communicating from a client-side application to a web server over HTTP. If you ever want to read or write data from a Vue.js app, you'll most likely consider AJAX. Of course, you'll need to work with a web server that has publicly accessible endpoints e.g. GET /items. AJAX will allow your Vue app to request that endpoint any time in its lifecycle.

### 02. AJAX-enabling a Vue app

AJAX can be implemented in any JavaScript app by using native web APIs including XMLHttpRequest or the more recent Fetch API. However, using these APIs directly will require tedious boilerplate, and in the case of Fetch, a polyfill for older browsers. So the recommended method amongst most web devs is to use an HTTP client library like Axios.

The easiest way to add an HTTP client to a Vue app is by using a Vue plugin. The best known are Vue Axios, which simply wraps the Axios library and Vue Resource. I'm a fan of Vue Axios, so let's see how to install that. Firstly, install Axios and Vue Axios from the command line:

```
$ npm i axios vue-axios --save
```

Now, import Axios and Vue Axios and install them on the Vue instance:

app.js

```js
import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'
 
Vue.use(VueAxios, axios)
```

With that done, the Axios will be accessible from anywhere in your Vue app from the instance property \$http:

SomeComponent.vue

```js
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
```

Here we're using the post method of Axios to POST data. If you want to see all the available methods of Axios take a look at the docs here.

### 03. Working with asynchronous code

AJAX calls are, by definition, asynchronous, so we must use asynchronous JavaScript code to handle requests. It's a good idea to get yourself comfortable with both the Promise API and with async/await syntax which, in 2020, is generally considered the easiest way to write async JS.

Most HTTP clients, and the Fetch API, will return a Promise from an AJAX request. Here we can see how Axios returns a Promise which we can get await for the result in an async method.

SomeComponent.vue

```js
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
```

### 04. Handling errors

Sometimes things go wrong. Maybe the user's connection drops or some knucklehead changes the API response format without telling you. You should ensure your application can handle such a situation by using try/catch:

SomeComponent.vue

```js
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
```

### 05. UX considerations

When AJAX calls are made across the internet there will be a delay between when the request is made, and when the request is resolved, with the length depending on both the internet connection speed and the latency of the web server.

It's good UX to let the user know what's going on by reflecting the AJAX state in the interface. One way to do this is to create a boolean flag isLoading that gets set to true before an AJAX call is initiated, then set to false when it completes. Thanks to Vue reactivity, this flag can be used in the template to conditionally show a "Loading" message or perhaps a spinner. In this example, I'm using two flags - isLoading and also isError to cover all bases.

SomeComponent.vue

```js
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
```

We can now make the template reflect the loading/error/ok state giving the user valuable feedback:

SomeComponent.vue

```html
<template>
  <div class="wrapper">
    <div v-if="isError">...</div>
    <div v-else-if="isLoading">...</div>
    <div v-else>...</div>
  </div>
</template>
```

### 06. Architectural patterns

Okay, so now you know how to make your Vue app AJAX-enabled. Where should you begin making AJAX calls in your app? For the rest of this article, I'm going to cover the most common patterns that you might want to use.

#### Pattern #1. From the root instance

With this pattern, you issue all your AJAX requests from the root instance and store all state there too. If any sub-components need data, it will come down as props. If sub-components need refreshed data, a custom event will be used to prompt the root instance to request it.

Example:

App.vue

```html
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
```

SomeComponent.vue

```html
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
```

Pros: 1) Keeps all your AJAX logic and data in one place. 2) Keeps your components "dumb" so they can focus on presentation.

Cons: A lot of props and custom events needed as your app expands.

#### Pattern #2. From components

With this architecture, components are responsible for managing their own AJAX requests and state independently. In practice, you'll probably want to create several "container" components that manage data for their local group of "presentational" components.

For example, filter-list might be a container component wrapping filter-input and filter-reset, which serve as presentational components. filter-list would contain the AJAX logic and would manage data for all the components in this group, communicating via props and events.

See Presentational and Container Components by Dan Abramov for a better description of this pattern. To make the implementation of this architecture easier, you can abstract any AJAX logic into a mixin, then use the mixin in a component to make it AJAX-enabled.

3『 [Presentational and Container Components - Dan Abramov - Medium](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0) 』

1『把交互的逻辑抽象为 mixin。』

app.js

```js
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
```

Pros: 1) Keeps components decoupled and reusable. 2) Gets the data when and where it's needed.

Cons: 1) Not easy to communicate data with other components or groups of components. 2) Components can end up with too many responsibilities and duplicate functionality.

#### Pattern #3. From Vuex actions

With this architecture, you manage AJAX logic in your Vuex store. Note that you'll need to import Axios in your store file rather than using the Vue Axios plugin, as Vuex does not have access to the Vue instance.

store.js

```js
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
```

Now components can request new data by dispatching an action.

MyComponent.vue

```html
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
```

Pros: 1) Decouples your state and presentation logic. 2) All the pros of the root component architecture, without needing props and custom events.

Cons: Adds the overhead of Vuex.

#### Pattern #4. From route navigation guards

With this architecture, your app is split into pages, and all data required for a page and its sub-components is fetched when the route is changed. The main advantage of this approach is that it simplifies your UI. If components are independently getting their data, the page will re-render unpredictably as component data gets populated in an arbitrary order.

A neat way of implementing this is to create endpoints on your server for each page e.g. /about, /contact, etc, which match the route names in your app. Then you can implement a generic beforeRouteEnter hook that will merge all the data properties into the page component's data:

router.js

```js
import axios from 'axios';

...

router.beforeRouteEnter(async (to, from, next) => {
  const { data } = await axios.get(`/api${to.path}`);
  next(vm => Object.assign(vm.$data, data));
});
```

Pros: Makes the UI more predictable.

Cons: 1) Slower overall, as the page can't render until all the data is ready. 2) Not much help if you don't use routes.

#### Pattern #5. From a service module

"Separation of concerns" is the idea that classes/modules/files should have just one job. This principle ensures your code is easy to read and maintain. To abide by that principle, we should try to keep AJAX logic out of our components (which are for presentation) and out of Vuex (which is for state).

A good way to achieve this is by abstracting AJAX into a separate module. In this case, we probably wouldn't need the vue-axios plugin anymore, and can instead use Axios directly.

```js
services/http.js

import "axios" from "axios";

export default {
  async getPost(id) {
    const { data } = await axios.get(`/posts/${id}`);
    return data;
  }
  ...
}
```

Now you can call this from anywhere in the Vue app - components, Vuex, or whatever floats your boat.

Post.vue

```js
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
```

Tip: you might even want to add your HTTP service to the Vue instance so it can be accessed from anywhere within the app e.g. this.$http.getPost();

1『 element-admin 作者用的就是这种方案，单独抽象出 api。』

#### Pattern #6. Server-render initial page state instead of using AJAX

Let's say your first page load includes server data as part of the state e.g. \<p>Hello {{ name }}!\</p>. It's not advisable to use AJAX to retrieve application state on the initial page load, as it requires an extra round-trip to the server that will delay your app from rendering. Instead, inject initial application state into an inline script in the head of the HTML page so it’s available to the app as a global variable as soon as it’s needed.

```html
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
```

AJAX can then be used for subsequent data fetches. If you're interested in learning more about this architecture, check out my article Avoid This Common Anti-Pattern In Full-Stack Vue/Laravel Apps.