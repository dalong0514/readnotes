# Pre-Render A Vue.js App (With Node Or Laravel)

Anthony Gore | April 1st, 2017 | 6 min read

[Pre-Render A Vue.js App (With Node Or Laravel) - Vue.js Developers](https://vuejsdevelopers.com/2017/04/01/vue-js-prerendering-node-laravel/)

Server-side rendering is all the rage right now. But it's not without its downsides. Pre-rendering is an alternative approach that may even be better in some circumstances.

In this article we'll explore how pre-rendering works with Vue.js and look at two examples; one with a Node.js project, one with a Laravel project.

Server-side rendering
One of the downsides to Javascript-based apps is that the browser receives an essentially empty page from the server. The DOM cannot be built until the Javascript has been downloaded and run.

This means that the user has to wait a bit longer to see anything. It can also have an impact on SEO if crawlers can't see content of the page quickly.

Server-side rendering (SSR) overcomes this issue by rendering the app on the server so that the client receives the complete DOM content when the page is loaded, before Javascript is even run.

So instead of the browser receiving this from the server:

<head> ... </head>
<body>
<div id="app">
  <!--This is empty, Javascript will populate it later-->
</app>
</body>
With SSR it receives a page with complete content:

<head> ... </head>
<body>
<div id="app">
  <div class="container">
    <h1>Your Server-Side Rendered App</h1>
    <div class="component-1">
      <p>Hello World</p>
      <!--etc etc. This was all rendered on the server-->
</app>
</body>
Server-side rendering cons
Your app will need to be executable on the server, so you'll need to design your code to be "universal" i.e. it works in both the browser and a Node server.

Your app will run on each request to the server, adding aditional load and slowing responses. Caching can partially alleviate this.

You can only do SSR with Node.js. If your primary backend is Laravel, Django etc you'll have to run a Node server alongside the main backend to take care of SSR.

Pre-rendering
There's another way to tackle the empty page problem: pre-rendering. With this approach you run your app before deploying it, capture the page output and replace your HTML files with this captured output.

It's pretty much the same concept as SSR except it's done pre-deployment in your development environment, not a live server.

Pre-rendering is typically performed with a headless browser like PhantomJS and can be incorporated into a build flow with Webpack, Gulp etc.

Pre-rendering pros
No additional server load, therefore faster and cheaper than SSR
A simpler production setup and simpler app code, therefore less prone to error
Doesn't require a Node.js production server
Pre-rendering cons
Doesn't work well for pages that display changing data e.g. tables.
Doesn't work for pages that have user-specific content e.g. an account page with a user's personal details. However these kinds of pages are less critical for pre-rendering anyway; it's our main, frequently used pages that we want to serve up fast.
You'll need to pre-render every route in the app indiviually.
Comparison table
Client-rendering only	Server-side rendering	Pre-rendering
Production server	Any/none	Node.js only	Any/none
Additional server load?	No	Yes	No
Personalised user data?	N/A	Yes	No
Vue.js pre-rendering example
Let's do a simple example of pre-rendering a Vue.js app, once in a Node.js environment and once in a Laravel environment.

In these examples we'll use Webpack with the prerender-spa-plugin to perform the pre-render.

Vue and Node
Step 1: Project installation
We'll use vue-cli with the webpack-simple template.

$ vue init webpack-simple vue-node-pr-test
$ cd vue-node-pr-test
$ npm install
There are three additional modules we'll need, explanations to follow.

$ npm install --save-dev http-server html-webpack-plugin prerender-spa-plugin
Step 2: Include index.html in the Webpack build
The webpack-simple template doesn't include the index.html file in the Webpack build output. However when we pre-render the app we'll need to overwrite our index.html, so let's add it to the output so as not to destroy the original.

Use the html-webpack-plugin in our webpack.config.js file to include the file in the Webpack build:

var HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports.plugins.push(
  new HtmlWebpackPlugin({
    template: './index.html',
    inject: false
  }),
);
Now we change our Webpack publicPath since the index.html will now be in the same folder as the other static assets:

output: {
  path: path.resolve(__dirname, './dist'),
  filename: 'build.js',
  publicPath: '/', // was originally 'dist'
},
And we'll also need to change <script src="/dist/build.js"></script> in our index.html to <script src="/build.js"></script> due to the changed path.

Step 3: Test the Webpack production build
Now when we build:

$ npm run build
Our dist folder should look like this:

- dist
-- build.js
-- index.html
-- logo.png
And if we inspect dist/index.html it'll look like this:

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>vue-node-pr-test</title>
  </head>
  <body>
    <div id="app"></div>
    <script type="text/javascript" src="/build.js"></script>
  </body>
</html>
Now we can use http-server and serve the app from the dist folder. By default it will run at localhost:8080:

$ ./node_modules/.bin/http-server ./dist

Join Our Next Live Workshop Online!
"Making Vue.js Apps Enterprise Ready" - May 27th, 2020, 5-6pm PDT
Step 4: Pre-render app
Now that our index.html file is in the Webpack build we can update it with the pre-rendered HTML.

Firstly we need to add prerender-spa-plugin to our webpack config. Make sure it comes after html-webpack-plugin.

var PrerenderSpaPlugin = require('prerender-spa-plugin');

module.exports.plugins.push(
  new PrerenderSpaPlugin(
    path.join(__dirname, './dist'),
    [ '/' ]
  )
);
The first argument to PrerenderSpaPlugin is the location of our index.html file, the second is a list of routes in the app. For each you add you'll get a different output file! In this example we just have one route, though.

Now we build again:

$ npm run build
Our build will take longer than it did before because the pre-render plugin is doing it's thing:

It creates an instance of Phantom JS and runs the app
Takes a snapshot of the DOM
Outputs the snapshot to an HTML file in our build folder
It repeats this process for every route, so it can take quite a while to build the app if you have many pages.

After the build our dist/index.html should now include all the pre-rendered HTML:

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>prerender-test</title>
  <style type="text/css">#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px
  }

  h1, h2 {
    font-weight: 400
  }

  ul {
    list-style-type: none;
    padding: 0
  }

  li {
    display: inline-block;
    margin: 0 10px
  }

  a {
    color: #42b983
  }</style>
</head>
<body>
<div id="app"><img src="/logo.png?82b9c7a5a3f405032b1db71a25f67021">
  <h1></h1>
  <h2>Essential Links</h2>
  <ul>
    <li><a href="https://vuejs.org" target="_blank">Core Docs</a></li>
    <li><a href="https://forum.vuejs.org" target="_blank">Forum</a></li>
    <li><a href="https://gitter.im/vuejs/vue" target="_blank">Gitter Chat</a></li>
    <li><a href="https://twitter.com/vuejs" target="_blank">Twitter</a></li>
  </ul>
  <h2>Ecosystem</h2>
  <ul>
    <li><a href="http://router.vuejs.org/" target="_blank">vue-router</a></li>
    <li><a href="http://vuex.vuejs.org/" target="_blank">vuex</a></li>
    <li><a href="http://vue-loader.vuejs.org/" target="_blank">vue-loader</a></li>
    <li><a href="https://github.com/vuejs/awesome-vue" target="_blank">awesome-vue</a></li>
  </ul>
</div>
<script type="text/javascript" src="/build.js"></script>

</body>
</html>
Vue and Laravel
If you skipped the Vue and Node example, I recommend you go back and read it first as it includes a more thorough explanation of any common steps.

Step 1: Project installation
Firstly we'll setup a new Laravel project.

$ laravel new vue-laravel-pr-test
$ cd vue-laravel-pr-test
$ npm install
We'll also add two more NPM modules we're going to need:

$ npm install --save-dev html-webpack-plugin prerender-spa-plugin
Step 2: Serve a plain HTML file
By default Laravel serves a Blade template file at the root URL. To keep the example simple we'll replace it with the following plain HTML file that we'll create at resources/views/index.html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>Laravel</title>
    <link rel="stylesheet" href="/css/app.css">
<body>
<div id="app">
  <example></example>
</div>
<script type="text/javascript" src="/js/app.js"></script>
</body>
</html>
Now we need to serve that file instead of the Blade template at the root route. Change routes/web.php to this:

Route::get('/', function () {
  return File::get(public_path() . '/index.html');
});
This is actually pointing to our build folder which we'll generate shortly.

Step 3: Add the HTML file to the build
Like in the Node example, we want to include our index.html in the Webpack build so we can overwrite it later with the pre-rendered HTML.

We'll need to do some Webpack configuration. I'm using Laravel 5.4 in this example, which uses Laravel Mix. Mix doesn't give you a local webpack configuration file because it uses it's own default file, so let's make one by coping from the laravel-mix module:

$ cp ./node_modules/laravel-mix/setup/webpack.config.js .
We'll also need to make our NPM production script point to this config file, so edit package.json and change the production script to this:

cross-env NODE_ENV=production node_modules/webpack/bin/webpack.js --progress --hide-modules --config=webpack.config.js
Now we add html-webpack-plugin to our webpack.config.js file. Add this to the bottom of the file above the Mix Finalizing section:

var HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports.plugins.push(
  new HtmlWebpackPlugin({
    template: Mix.Paths.root('resources/views/index.html'),
    inject: false
  });
);
Step 4: Test the Weback production build
Let's now build for production and serve:

$ npm run production
$ php artisan serve
You'll probably get an error in the browser when you run the app, though, because we never set a value for window.Laravel.csrfToken. For this simple example it's quicker just to comment it out, so change resources/assets/js/bootstap.js like this:

window.axios.defaults.headers.common = {
  'X-Requested-With': 'XMLHttpRequest'
  // 'X-CSRF-TOKEN': window.Laravel.csrfToken;
};
Step 5: Pre-render app
We now need to use prerender-spa-plugin in our webpack config to perform the pre-rendering. Make sure it comes after html-webpack-plugin.

var PrerenderSpaPlugin = require('prerender-spa-plugin');

module.exports.plugins.push(
  new PrerenderSpaPlugin(
    Mix.output().path,
    [ '/' ]
  )
);
Now we can do a production build:

$ npm run production
If you check the build folder, dist/index.html should now look like the following, complete with pre-render HTML:

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>Laravel</title>
    <link rel="stylesheet" href="/css/app.css">
</head>
<body>
<div id="app">
    <div class="container">
        <div class="row">
            <div class="col-md-8 col-md-offset-2">
                <div class="panel panel-default">
                    <div class="panel-heading">Example Component</div>
                    <div class="panel-body">
                        I'm an example component!
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
<script src="/js/app.js"></script>
</body>
</html>
Anthony Gore
About Anthony Gore
I'm Anthony Gore and I'm here to teach you Vue.js! Through my books, online courses, and social media, my aim is to turn you into a Vue.js expert.

I'm a Vue Community Partner, curator of the weekly Vue.js Developers Newsletter, and the creator of Vue.js Developers.

If you enjoyed this article, show your support by buying me a coffee, and if you'd like to support me ongoingly, you can make a pledge through Patreon.