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

## 附件02-Advanced-Server-Side-Rendering-With-Vue- Multi-Page-App.md

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
