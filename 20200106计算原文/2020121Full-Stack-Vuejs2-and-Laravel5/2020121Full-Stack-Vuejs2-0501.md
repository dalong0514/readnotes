In this chapter, we'll migrate the Vuebnb frontend prototype into our main Laravel project, achieving the first full-stack iteration of Vuebnb. This fully-integrated environment will include a Webpack build step, allowing us to incorporate more sophisticated tools and techniques as we continue to build the frontend.

Topics covered in this chapter:

An introduction to Laravel's out-of-the-box frontend app

A high-level overview of Webpack

How to configure Laravel Mix to compile frontend assets

Migrating the Vuebnb prototype into the full-stack Laravel environment

Using ES2015 with Vue.js, including syntax and polyfills for older browsers

Switching hard-coded data in the frontend app to backend data

Laravel frontend

We think of Laravel as being a backend framework, but a fresh Laravel project includes boilerplate code and configuration for a frontend app as well.

The out-of-the-box frontend includes JavaScript and Sass asset files, as a well as a package.json file that specifies dependencies such as Vue.js, jQuery, and Bootstrap.

Let's take a look at this boilerplate code and configuration so we get an idea of how the Vuebnb frontend app will fit into our Laravel project when we begin the migration.

JavaScript

JavaScript assets are kept in the resources/assets/js folder. There are several .js files in this directory, as well as a sub-directory component, with a .vue file. This latter file will be explained in another chapter so we'll ignore it for now.

The main JavaScript file is app.js. You'll see the familiar Vue constructor in this file, but also some syntax that may not be as familiar. On the first line is a require function that is intended to import an adjacent file, bootstrap.js, which in turn loads other libraries including jQuery and Lodash.

require is not a standard JavaScript function and must be resolved somehow before this code can be used in a browser.

resources/assets/js/app.js:

require('./bootstrap'); window.Vue = require('vue'); Vue.component('example', require('./components/Example.vue')); const app = new Vue({ el: '#app' });

CSS

If you haven't heard of Sass before, it's a CSS extension that makes it easier to develop CSS. A default Laravel installation includes the resources/assets/sass directory, which includes two boilerplate Sass files.

The main Sass file is app.scss. Its job is to import other Sass files including the Bootstrap CSS framework.

resources/assets/sass/app.scss:

// Fonts @import url("https://fonts.googleapis.com/css?family=Raleway:300,400,600"); // Variables @import "variables"; // Bootstrap @import "~bootstrap-sass/assets/stylesheets/bootstrap";

Node modules

Another key aspect of the Laravel frontend is the package.json file in the root of the project directory. Similar to composer.json, this file is used for configuration and dependency management, only for Node modules rather than PHP.

One of the properties of package.json is devDependencies, which specifies the modules required in the development environment, including jQuery, Vue, and Lodash.

package.json:

{ ... "devDependencies": { "axios": "^0.17", "bootstrap-sass": "^3.3.7", "cross-env": "^5.1", "jquery": "^3.2", "laravel-mix": "^1.4", "lodash": "^4.17.4", "vue": "^2.5.3" } }

Views

To serve the frontend app with Laravel, it needs to be included in a view. The only out-of-the-box view provided is the welcome view, located at resources/views/welcome.blade.php, which is used as a boilerplate home page.

The welcome view does not actually include the frontend app and it's left to the user to install it themselves. We'll look at how to do this later in the chapter.

Asset compilation

The files in resources/assets include functions and syntax that can't be used directly in a browser. For example, the require method used in app.js, which is designed to import a JavaScript module, is not a native JavaScript method and is not part of the standard Web API:

Figure 5.1. require is not defined in the browser

A build tool is needed to take these asset files, resolve any non-standard functions and syntax, and output code that the browser can use. There are a number of popular build tools for frontend assets including Grunt, Gulp, and Webpack:

Figure 5.2. Asset compilation process

The reason we go to the effort of using this asset compilation process is so we can author our frontend app without the constraints of what a browser allows. We can introduce a variety of handy development tools and features that'll allow us to write our code and fix problems more easily.

Webpack

Webpack is the default build tool supplied with Laravel 5.5 and we'll be making use of it in the development of Vuebnb.

What makes Webpack different to other popular build tools, such as Gulp and Grunt, is that it's first and foremost a module bundler. Let's begin our overview of Webpack by getting an understanding of how the module bundling process works.

Dependencies

In a frontend application, we are likely to have dependencies for third-party JavaScript libraries or even other files in our own code base. For example, the Vuebnb prototype is dependent on Vue.js and the mock-listing data file:

Figure 5.3. Vuebnb prototype dependencies

There's no real way of managing these dependencies in a browser, other than to ensure any shared functions and variables have global scope and that scripts are loaded in the right order.

For example, since node_modules/vue/dist/vue.js defines a global Vue object and is loaded first, we're able to use the Vue object in our app.js script. If either of those conditions was not met, Vue would not be defined when app.js ran, resulting in an error:

<script src="node_modules/vue/dist/vue.js"></script> <script src="sample/data.js"></script> <script src="app.js"></script>

This system has a number of downsides:

Global variables introduce possibilities of naming collisions and accidental mutations

Script loading order is fragile and can be easily broken as the app grows

We can't utilize performance optimizations, such as loading scripts asynchronously

Modules

A solution to the dependency management problem is to use a module system, such as CommonJS or native ES modules. These systems allow JavaScript code to be modularized and imported into other files.

Here is a CommonJS example:

// moduleA.js module.exports = function(value) { return value * 2; } // moduleB.js var multiplyByTwo = require('./moduleA'); console.log(multiplyByTwo(2)); // Output: 4

And here is a Native ES modules example:

// moduleA.js export default function(value) { return value * 2; } // moduleB.js import multiplyByTwo from './moduleA';

console.log(multiplyByTwo(2));

// Output: 4

The problem is that CommonJS cannot be used in a browser (it was designed for server-side JavaScript) and native ES modules are only now getting browser support. If we want to use a module system in a project, we'll need a build tool: Webpack.

Bundling

The process of resolving modules into browser-friendly code is called bundling. Webpack begins the bundling process with the entry file as a starting point. In the Laravel frontend app, resources/assets/js/app.js is the entry file.

Webpack analyzes the entry file to find any dependencies. In the case of app.js, it will find three: bootstrap, vue, and Example.vue.

resources/assets/js/app.js:

require('./bootstrap'); window.Vue = require('vue'); Vue.component('example', require('./components/Example.vue')); ...

Webpack will resolve these dependencies and then analyze them to find any dependencies that they might have. This process continues until all dependencies of the project are found. The result is a graph of dependencies that, in a large project, might include hundreds of different modules.

Webpack uses this graph of dependencies as a blueprint for bundling all the code into a single browser-friendly file:

<script src="bundle.js"></script>

Loaders

Part of what makes Webpack so powerful is that during the bundling process it can transform a module with one or more Webpack loaders.

For example, Babel is a compiler that transforms next-generation JavaScript syntax such as ES2015 into standard ES5. The Webpack Babel loader is one of the most popular as it allows developers to write their code using modern features, but still provide support in older browsers.

For example, in the entry file, we see the ES2015 const declaration that isn't supported by IE10.

resources/assets/js/app.js:

const app = new Vue({ el: '#app' });

If the Babel loader is used, const will be transformed to var before it's added to the bundle.

public/js/app.js:

var app = new Vue({ el: '#app' });

Laravel Mix

One of the downsides of Webpack is that configuring it is arduous. To make thing easier, Laravel includes a module called Mix that takes the most commonly-used Webpack options and puts them behind a simple API.

The Mix configuration file can be found in the root of the project directory. Mix configuration involves chaining methods to the mix object that declare the basic build steps of your app. For example, the js method takes two arguments, the entry file and the output directory, and the Babel loader is applied by default. The sass method works in an equivalent way.

webpack.mix.js:

let mix = require('laravel-mix'); mix.js('resources/assets/js/app.js', 'public/js') .sass('resources/assets/sass/app.scss', 'public/css');

Running Webpack

Now that we have a high-level understanding of Webpack, let's run it and see how it bundles the default frontend asset files.

First, ensure you have all the development dependencies installed:

$ npm install

CLI

Webpack is typically runs from the command line, for example:

$ webpack [options]

Rather than figuring out the correct CLI option ourselves, we can use one of the Weback scripts predefined in package.json. For example, the development script will run Webpack with options suitable for creating a development build.

package.json:

"scripts": { ... "development": "cross-env NODE_ENV=development node_modules/webpack/bin/webpack.js --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js", ... }

First build

Let's now run the dev script (a shortcut for the development script):

$ npm run dev

After this runs, you should see an output in the Terminal similar to the following:

Figure 5.4. Webpack Terminal output

This output tells us a number of things, but most importantly that the build was successful and what files were created in the output including fonts, JavaScript, and CSS. Note that the output file path is relative not to the project root but to the public directory, so the js/apps.js file will be found at public/js/app.js.

JavaScript

Inspecting the output JavaScript file, public/js/app.js, we see a whole lot of code in there - around 42,000 lines! That's because jQuery, Lodash, Vue, and the other JavaScript dependencies have all been bundled into this one file. It's also because we've used a development build that does not include minification or uglification.

If you search through the file, you'll see that the code from our entry file, app.js, has been transpiled to ES5 as expected:

Figure 5.5. Bundle file public/js/app.js

CSS

We also have a CSS bundle file, public/css/app.css. If you inspect this file you will find the imported Bootstrap CSS framework has been included and the Sass syntax has been compiled to plain CSS.

Fonts

You might think it's strange that there are fonts in the output, since Mix did not include any explicit font configuration. These fonts are dependencies of the Bootstrap CSS framework and Mix, by default, will output them individually rather than in a font bundle.

Migrating Vuebnb

Now that we're familiar with the default Laravel frontend app code and configuration, we're ready to migrate the Vuebnb prototype into the main project. This migration will allow us to have all our source code in one place, plus we can utilize this more sophisticated development environment for building the remainder of Vuebnb.

The migration will involve:

Removing any unnecessary modules and files

Moving the prototype files into the Laravel project structure

Modifications to the prototype files to adapt them to the new environment

Figure 5.6. Vuebnb prototype migration

Removing unnecessary dependencies and files

Let's begin by removing the Node dependencies we no longer need. We'll keep axis as it'll be used in a later chapter, and cross-env because it ensures our NPM scripts can be run in a variety of environments. We'll get rid of the rest:

$ npm uninstall bootstrap-sass jquery lodash --save-dev

This command will leave your dev dependencies looking like this.

package.json:

"devDependencies": { "axios": "^0.17", "cross-env": "^5.1", "laravel-mix": "^1.4", "vue": "^2.5.3" }

Next, we'll remove the files we don't need. This includes several of the JavaScript assets, all of the Sass plus the welcome view:

$ rm -rf \ resources/assets/js/app.js \ resources/assets/js/bootstrap.js \ resources/assets/js/components/* \ resources/assets/sass \ resources/views/welcome.blade.php

Since we're removing all the Sass files, we'll also need to remove the sass method in the Mix configuration.

webpack.mix.js:

let mix = require('laravel-mix'); mix .js('resources/assets/js/app.js', 'public/js') ;

Now our frontend app is free from clutter and we can move the prototype files into their new home.

HTML

Let's now copy the contents of index.html from the prototype project we completed in Chapter 2, Prototyping Vuebnb, Your First Vue.js Project, into a new file, app.blade.php. This will allow the template to be used as a Laravel view:

$ cp ../vuebnb-prototype/index.html ./resources/views/app.blade.php

We'll also update the home web route to point to this new view instead of welcome.

routes/web.php:

<?php Route::get('/', function () { return view('app'); });

Syntax clash

Using the prototype template file as a view will cause a small issue as Vue and Blade share a common syntax. For example, look at the heading section where Vue.js interpolates the title and address of a listing.

resources/views/app.blade.php:

<div class="heading"> <h1>{{ title }}</h1> <p>{{ address }}</p> </div>

When Blade processes this, it will think the double curly brackets are its own syntax and will generate a PHP error as neither title nor address are defined functions.

There is a simple solution: escape these double curly brackets to let Blade know to ignore them. This can be done by placing an @ symbol as a prefix.

resources/views/app.blade.php:

<div class="heading"> <h1>@{{ title }}</h1> <p>@{{ address }}</p> </div>

Once you've done that for each set of double curly brackets in the file, load the home route in the browser to test the new view. Without the JavaScript or CSS it doesn't look great, but at least we can confirm it works:

Figure 5.7. Home route

JavaScript

Let's now move the prototype's main script file, app.js, into the Laravel project:

$ cp ../vuebnb-prototype/app.js ./resources/assets/js/

Given the current Mix settings, this will now be the entry file of the JavaScript bundle. This means JavaScript dependencies at the bottom of the view can be replaced with the bundle, that is.

resources/views/app.blade.php:

<script src="node_modules/vue/dist/vue.js"></script> <script src="sample/data.js"></script> <script src="app.js"></script>

Can be replaced with,

resources/views/app.blade.php:

<script src="{{ asset('js/app.js') }}"></script>

Mock data dependency

Let's copy the mock data dependency into the project as well:

$ cp ../vuebnb-prototype/sample/data.js ./resources/assets/js/

Currently, this file declares a global variable sample that is then picked up in the entry file. Let's make this file a module by replacing the variable declaration with an ES2015 export default.

resources/assets/js/data.js:

export default { ... }

We can now import this module at the top of our entry file. Note that Webpack can guess the file extension in an import statement so you can omit the .js from data.js.

resources/assets/js/app.js:

import sample from './data'; var app = new Vue({ ... });

While Laravel has opted to use CommonJS syntax for including modules, that is require, we will use native ES module syntax, that is import. This is because ES modules are making their way into the JavaScript standard, and it's more consistent with the syntax used by Vue.

Displaying modules with Webpack

Let's run a Webpack build to make sure the JavaScript migration is working so far:

$ npm run dev

If all is well, you'll see the JavaScript bundle file being output:

Figure 5.8. Webpack Terminal output

It'd be nice to know that the mock data dependency was added without having to manually inspect the bundle to find the code. We can do this by telling Webpack to print the modules it has processed in the Terminal output.

In the development script in our package.json, a --hide-modules flag has been set, as some developers prefer a succinct output message. Let's remove it for now and instead add the --display-modules flag, so the script looks like this:

"scripts": { ... "development": "cross-env NODE_ENV=development node_modules/webpack/bin/webpack.js --progress --display-modules --config=node_modules/laravel-mix/setup/webpack.config.js", ... }

Now run the build again, and we get this more verbose terminal output:

Figure 5.9. Webpack Terminal output with the display-modules flag

This assures us that both our app.js and data.js files are included in the bundle.

Vue.js dependency

Let's now import Vue.js as a dependency of our entry file.

resources/assets/js/app.js:

import Vue from 'vue'; import sample from './data'; var app = new Vue({ ... });

Running the build again, we'll now see Vue.js in the list of modules in the Terminal output, plus some dependencies that it has introduced:

Figure 5.10. Webpack Terminal output showing Vue.js

You may be wondering how import Vue from 'vue' resolves, as it doesn't seem to be a proper file reference. Webpack will, by default, check the node_modules folder in the project for any dependencies, saving you from having to put import Vue from 'node_modules/vue';.

But how, then, does it know the entry file of this package? Looking at the Webpack Terminal output in the preceding screenshot, you can see that it has included node_modules/vue/dist/vue.common.js. It knows to use this file because, when Webpack is adding node modules as dependencies, it checks their package.json file and looks for the main property, which in the case of Vue is.

node_modules/vue/package.json:

{ ... "main": "dist/vue.runtime.common.js", ... }

However, Laravel Mix overrides this to force a different Vue build.

node_modules/laravel-mix/setup/webpack.config.js:

alias: { 'vue$': 'vue/dist/vue.common.js' }

In short, import Vue from 'vue' is effectively the same as import Vue from 'node_modules/vue/dist/vue.common.js'.

We'll explain the different Vue builds in Chapter 6, Composing Widgets with Vue.js Components.

With that done, our JavaScript has been successfully migrated. Loading the home route again, we can better make out the listing page of Vuebnb with the JavaScript now included:

Figure 5.11. Home route with JavaScript migrated

CSS

To migrate CSS, we'll copy style.css from the prototype into the Laravel project. The default Laravel frontend app used Sass rather than CSS, so we'll need to make a directory for CSS assets first:

$ mkdir ./resources/assets/css $ cp ../vuebnb-prototype/style.css ./resources/assets/css/

Let's then make a new declaration in our Mix config to get a CSS bundle using the styles method.

webpack.mix.js:

mix .js('resources/assets/js/app.js', 'public/js') .styles('resources/assets/css/style.css', 'public/css/style.css') ;

We'll now link to the CSS bundle in our view by updating the link's href.

resources/views/app.blade.php:

<link rel="stylesheet" href="{{ asset('css/style.css') }}" type="text/css">

Font styles

We also have the Open Sans and Font Awesome style sheets to include. First, install the font packages with NPM:

$ npm i --save-dev font-awesome open-sans-all

We'll modify our Mix configuration to bundle our app CSS, Open Sans, and Font Awesome CSS together. We can do this by passing an array to the first argument of the styles method.

webpack.mix.js:

mix .js('resources/assets/js/app.js', 'public/js') .styles([ 'node_modules/open-sans-all/css/open-sans.css', 'node_modules/font-awesome/css/font-awesome.css', 'resources/assets/css/style.css'

], 'public/css/style.css') ;

Mix will append statistics about the CSS bundle into the Terminal output:

Figure 5.12. Webpack Terminal output with CSS

Remember to remove the links to the font style sheets from the view as these will now be in the CSS bundle.

Fonts

Open Sans and Font Awesome need both a CSS style sheet, and the relevant font files. Like CSS, Webpack can bundle fonts as modules, but we currently don't need to take advantage of this. Instead, we'll use the copy method, which tells Mix to copy the fonts from their home directory into the public folder where they can be accessed by the frontend app.

webpack.mix.js:

mix .js('resources/assets/js/app.js', 'public/js') .styles([ 'node_modules/open-sans-all/css/open-sans.css', 'node_modules/font-awesome/css/font-awesome.css', 'resources/assets/css/style.css' ], 'public/css/style.css') .copy('node_modules/open-sans-all/fonts', 'public/fonts') .copy('node_modules/font-awesome/fonts', 'public/fonts') ;

After building again, you'll now see a public/fonts folder in the project structure.

Images

We'll now migrate the images, including the logo for the toolbar, and the mock data header image:

$ cp ../vuebnb-prototype/logo.png ./resources/assets/images/ $ cp ../vuebnb-prototype/sample/header.jpg ./resources/assets/images/

Let's chain on another copy method to include these in the public/images directory.

webpack.mix.js:

mix .js('resources/assets/js/app.js', 'public/js') .styles([ 'node_modules/open-sans-all/css/open-sans.css', 'node_modules/font-awesome/css/font-awesome.css', 'resources/assets/css/style.css' ], 'public/css/style.css') .copy('node_modules/open-sans-all/fonts', 'public/fonts') .copy('node_modules/font-awesome/fonts', 'public/fonts') .copy('resources/assets/images', 'public/images') ;

We also need to ensure the view is pointing to the correct file location for the images. In the toolbar.

resources/views/app.blade.php:

<div id="toolbar"> <img class="icon" src="{{ asset('images/logo.png') }}"> <h1>vuebnb</h1> </div>

And in the modal.

resources/views/app.blade.php:

<div class="modal-content"> <img src="{{ asset('images/header.jpg') }}"/> </div>

Don't forget that the headerImageStyle data property in the entry file also needs to be updated.

resources/assets/js/app.js:

headerImageStyle: { 'background-image': 'url(/images/header.jpg)' },

While not exactly an image, we'll also migrate the favicon. This can be put straight into the public folder:

$ cp ../vuebnb-prototype/favicon.ico ./public

After building again, we'll now have the Vuebnb client app prototype fully migrated:

Figure 5.13. Vuebnb client app prototype served from Laravel

Development tools

We can utilize some handy development tools to improve our frontend workflow, including:

Watch mode

BrowserSync

Watch mode

So far, we've been running builds of our app manually using npm run dev every time we make a change. Webpack also has a watch mode where it automatically runs a build when a dependency changes. Thanks to the design of Webpack, it is able to efficiently complete these automatic builds by only rebuilding modules that have changed.

To use watch mode, run the watch script included in package.json:

$ npm run watch

To test that it works, add this at the bottom of resources/assets/js/app.js:

console.log("Testing watch");

If watch mode is running correctly, saving this file will trigger a build, and you'll see updated build statistics in the Terminal. If you then refresh the page you'll see the Testing watch message in the console.

To turn off watch mode, press Ctrl + C in the Terminal. It can then be restarted at any time. Don't forget to remove the console.log once you're satisfied watch mode is working.

I'll assume you're using watch for the rest of the book, so I won't remind you to build your project after changes anymore!

BrowserSync

Another useful development tool is BrowserSync. Similar to watch mode, BrowserSync monitors your files for changes, and when one occurs inserts the change into the browser. This saves you from having to do a manual browser refresh after every build.

To use BrowserSync, you'll need to have the Yarn package manager installed. If you're running terminal commands from within the Vagrant Box, you're all set, as Yarn is pre-installed with Homestead. Otherwise, follow the installation instructions for Yarn here: https://yarnpkg.com/en/docs/install.

BrowserSync has been integrated with Mix and can be used by chaining a call to the browserSync method in your Mix configuration. Pass an options object with the app's URL as a proxy property, for example, browserSync({ proxy: http://vuebnb.test }).

We have the app's URL stored as an environment variable in the .env file, so let's get it from there rather than hard-coding into our Mix file. First, install the NPM dotenv module, which reads a .env file into a Node project:

$ npm i dotenv --save-devpm

Require the dotenv module at the top of the Mix configuration file and use the config method to load .env. Any environment variables will then be available as properties of the process.env object.

We can now pass an options object to the browserSync method with process.env.APP_URL assigned to proxy. I also like to use the open: false option as well, which prevents BrowserSync from automatically opening a tab.

webpack.mix.js:

require('dotenv').config(); let mix = require('laravel-mix'); mix ... .browserSync({ proxy: process.env.APP_URL, open: false }) ;

BrowserSync runs on its own port, 3000 by default. When you run npm run watch again, open a new tab at localhost:3000. After you make changes to your code you'll find they are automatically reflected in this BrowserSync tab!

Note that if you run BrowserSync inside your Homestead box you can access it at vuebnb.test:3000.

Even though the BrowserSync server runs on a different port to the web server, I will continue to refer to URLs in the app without specifying the port to avoid any confusion, for example, vuebnb.test rather than localhost:3000 or vuebnb.test:3000.

ES2015

The js Mix method applies the Babel plugin to Webpack, ensuring that any ES2015 code is transpiled down to browser-friendly ES5 before it's added to the bundle file.

We wrote the Vuebnb frontend app prototype using only ES5 syntax, as we ran it directly in the browser without any build step. But now we can take advantage of ES2015 syntax, which includes a lot of handy features.

For example, we can use a shorthand for assigning a function to an object property.

resources/assets/js/app.js:

escapeKeyListener: function(evt) { ... }

Can be changed to this:

escapeKeyListener(evt) { ... }

There are several instances of this in app.js that we can change. There aren't any other opportunities for using ES2015 syntax in our code yet, though in the coming chapters we'll see more.

Polyfills

The ES2015 proposal includes new syntax, but also new APIs, such as Promise, and additions to existing APIs, such as Array and Object.

The Webpack Babel plugin can transpile ES2015 syntax, but new API methods require polyfilling. A polyfill is a script that is run in the browser to cover an API or API method that may be missing.

For example, Object.assign is a new API method that is not supported in Internet Explorer 11. If we want to use it in our frontend app, we have to check at the top of our script whether the API method exists, and if not, we define it manually with a polyfill:

if (typeof Object.assign != 'function') { // Polyfill to define Object.assign }

Speaking of which, Object.assign is a handy way of merging objects and would be useful in our frontend app. Let's use it in our code, then add a polyfill to ensure the code will run in older browsers.

Look at the data object in our entry file, resources/assets/js/app.js. We are manually assigning each property of the sample object to the data object, giving it the same property name. To save having to repeat ourselves, we can instead use Object.assign and simply merge the two objects. In practice, this doesn't do anything different, it's just more succinct code.

resources/assets/js/app.js:

data: Object.assign(sample, { headerImageStyle: { 'background-image': 'url(/images/header.jpg)' }, contracted: true, modalOpen: false }),

To polyfill Object.assign we must install a new core-js dependency, which is a library of polyfills for most new JavaScript APIs. We'll use some other core-js polyfills later in the project:

$ npm i --save-dev core-js

At the top of app.js, add this line to include the Object.assign polyfill:

import "core-js/fn/object/assign";

After this builds, refresh your page to see whether it works. Most likely you will not notice any difference unless you can test this on an older browser, such as Internet Explorer, but now you have the assurance that this code will run almost anywhere.

Mock data

We've now completely migrated the Vuebnb prototype into our Laravel project, plus we've added a build step. Everything in the frontend app is working as it was in Chapter 2, Prototyping Vuebnb, Your First Vue.js Project.

However, we still have mock data hard-coded into the frontend app. In this last part of the chapter, we're going to remove that hard-coded data and replace it with data from the backend.

Routes

Currently, the home route, that is, /, loads our frontend app. But what we've built for our frontend app so far is not meant to be a home page! We'll be building that in future chapters.

What we've built is the listing page, which should be at a route like /listing/5, where 5 is the ID of the mock data listing being used.

Page Route

Home page /

Listing page /listing/{listing}

Let's modify the route to reflect this.

routes/web.php:

<?php

use App\Listing; Route::get('/listing/{listing}', function ($id) { return view('app'); });

Just like in our api/listing/{listing} route, the dynamic segment is meant to match the ID for one of our mock data listings. If you recall from the previous chapter, we created 30 mock data listings with an ID range of 1 to 30.

If we now type hint the Listing model in the closure function's profile, Laravel's service container will pass in a model with an ID that matches that dynamic route segment.

routes/web.php:

Route::get('/listing/{listing}', function (Listing $listing) { // echo $listing->id // will equal 5 for route /listing/5 return view('app'); });

One cool in-built feature is, if the dynamic segment does not match a model, for example /listing/50 or /listing/somestring, Laravel will abort the route and return a 404.

Architecture

Given that we can retrieve the correct listing model in the route handler, and that, thanks to the Blade templating system, we can dynamically insert content into our app view, an obvious architecture emerges: we can inject the model into the head of the page. That way, when the Vue app loads, it will have immediate access to the model:

Figure 5.14. Inline listing model into the head of the page

Injecting data

Getting the mock-listing data into the client app will take several steps. We'll begin by converting the model to an array. The view helper can then be used to make the model available within the template at runtime.

routes/web.php:

Route::get('/listing/{listing}', function (Listing $listing) { $model = $listing->toArray(); return view('app', [ 'model' => $model ]); });

Now, in the Blade template, we'll create a script in the head of the document. By using double curly brackets, we can interpolate the model directly into the script.

resources/views/app.blade.php:

<head> ... <script type="text/javascript"> console.log({{ $model[ 'id' ] }}); </script> </head>

If we now go to the /listing/5 route, we will see the following in our page source:

<script type="text/javascript"> console.log(5); </script>

And you will see the following in our console:

Figure 5.15. Console output after injecting model ID

JSON

We'll now encode the entire model as JSON within the view. The JSON format is good because it can be stored as a string and can be parsed by both PHP and JavaScript.

In our inline script, let's format the model as a JSON string and assign to a model variable.

resources/views/app.blade.php:

<script type="text/javascript"> var model = "{!! addslashes(json_encode($model)) !!}"; console.log(model); </script>

Notice we also had to wrap json_encode in another global function, addslashes. This function will add backslashes before any character that needs to be escaped. It's necessary to do this because the JavaScript JSON parser doesn't know which quotes in the string are part of the JavaScript syntax, and which are part of the JSON object.

We also had to use a different kind of Blade syntax for interpolation. A feature of Blade is that statements within double curly brackets {{ }} are automatically sent through PHP's htmlspecialchars function to prevent XSS attacks. This will, unfortunately, invalidate our JSON object. The solution is to use the alternative {!! !!} syntax, which does not validate the contents. This is safe to do in this scenario because we're sure we're not using any user-supplied content.

Now if we refresh the page, we'll see the JSON object as a string in the console:

Figure 5.16. Model as a JSON string in the console

If we change the log command to console.log(JSON.parse(model));, we see our model not as a string, but as a JavaScript object:

Figure 5.17. Model as an object in the console

We've now successfully gotten our model from the backend into the frontend app!

Sharing data between scripts

We have another issue to overcome now. The inline script in the head of the document, which is where our model object is, is a different script to the one where we have our client application, which is where it's needed.

As we've discussed in the previous section, multiple scripts and global variables are generally not preferred as they make the app fragile. But in this scenario, they're a necessity. The safest way to share an object or function between two scripts is to make it a property of the global window object. That way, it's very obvious from your code that you're intentionally using a global variable:

// scriptA.js window.myvar = 'Hello World'; // scriptB.js console.log(window.myvar); // Hello World

If you add additional scripts to your project, particularly third-party ones, they might also add to the window object, and there's a possibility of a naming collision. To avoid this the best we can, we'll make sure we use a very specific property name.

resources/views/app.blade.php:

<script type="text/javascript"> window.vuebnb_listing_model = "{!! addslashes(json_encode($model)) !!}" </script>

Now, over in the entry file of the frontend app, we can work with this window property in our script.

resources/assets/js/app.js:

let model = JSON.parse(window.vuebnb_listing_model); var app = new Vue({ ... });

Replacing the hard-coded model

We now have access to our listing model in the entry file, so let's switch it with our hard-coded model in the data property assignment.

resources/assets/js/app.js:

let model = JSON.parse(window.vuebnb_listing_model); var app = new Vue({ el: '#app' data: Object.assign(model, { ... }) ... });

With that done, we can now remove the import sample from './data'; statement from the top of app.js. We can also delete the sample data files as they won't be used any further in the project:

$ rm resources/assets/js/data.js resources/assets/images/header.jpg

Amenities and prices

If you refresh the page now, it will load, but the script will have some errors. The problem is that the amenities and prices data are structured differently in the frontend app to how they are in the backend. This is because the model initially came from our database, which stores scalar values. In JavaScript, we can use richer objects which allow us to nest data, making it much easier to work with and manipulate.

Here is how the model object currently looks. Notice that the amenities and prices are scalar values:

Figure 5.18. How the listing model currently looks

This is how we need it to look, with the amenities and prices as arrays:

Figure 5.19. How the listing model should look

To fix this problem, we'll need to transform the model before we pass it to Vue. To save you having to think too much about this, I've put the transformation function into a file, resources/assets/js/helpers.js. This file is a JavaScript module that we can import into our entry file and use by simply passing the model object into the function.

resources/assets/js/app.js:

import Vue from 'vue'; import { populateAmenitiesAndPrices } from './helpers'; let model = JSON.parse(window.vuebnb_listing_model); model = populateAmenitiesAndPrices(model)</span>;

Once we've added this and refreshed the page, we should see the new model data in the text parts of the page (although still with the hard-coded images):

Figure 5.20. New model data in page with hard-coded images

Image URLs

The last thing to do is replace the hard-coded images' URLs in the frontend app. These URLs are not currently a part of the model, so need to be manually added to the model before we inject it into the template.

We've already done a very similar job back in Chapter 4, Building a Web Service With Laravel, for the API listing route.

app/Http/Controllers/ListingController.php:

public function get_listing_api(Listing $listing) { $model = $listing->toArray(); for($i = 1; $i <=4; $i++) { $model['image_' . $i] = asset( 'images/' . $listing->id . '/Image_' . $i . '.jpg' ); } return response()->json($model); }

In fact, our web route will end up with identical code to this API route, only instead of returning JSON, it will return a view.

Let's share the common logic. Begin by moving the route closure function into a new get_listing_web method in the listing controller.

app/Http/Controllers/ListingController.php:

<?php namespace App\Http\Controllers; use Illuminate\Http\Request; use App\Listing; class ListingController extends Controller { public function get_listing_api(Listing $listing) { ... } public function get_listing_web(Listing $listing) { $model = $listing->toArray(); return view('app', ['model' => $model]); } }

Then adjust the route to call this new controller method.

routes/web.php:

<?php Route::get('/listing/{listing}', 'ListingController@get_listing_web');

Let's now update the controller so both the web and API routes get the images' URLs added to their model. We'll first create a new add_image_urls method, which abstracts the logic that was used in get_listing_api. Now both of the route-handling methods will call this new method.

app/Http/Controllers/ListingController.php:

<?php namespace App\Http\Controllers; use Illuminate\Http\Request; use App\Listing; class ListingController extends Controller { private function add_image_urls($model, $id) { for($i = 1; $i <=4; $i++) { $model['image_' . $i] = asset( 'images/' . $id . '/Image_' . $i . '.jpg' ); } return $model; } public function get_listing_api(Listing $listing) { $model = $listing->toArray(); $model = $this->add_image_urls($model, $listing->id); return response()->json($model); } public function get_listing_web(Listing $listing) { $model = $listing->toArray(); $model = $this->add_image_urls($model, $listing->id);

return view('app', ['model' => $model]); } }

With that done, if we refresh the app and open Vue Devtools, we should see that we have the image URLs as an images data property:

Figure 5.21. Images are now a data property as shown in Vue Devtools

Replacing the hard-coded image URLs

The final step is to use these image URLs from the backend instead of the hard-coded URL. Remembering that images is an array of URLs, we'll use the first image as a default, that is, images[0].

First, we'll update the entry file,

resources/assets/js/app.js:

headerImageStyle: { 'background-image': `url(${model.images[0]})` }

Then the view for the modal image.

resources/views/app.blade.php:

<div class="modal-content"> <img v-bind:src="images[0]"/> </div>

With that done, after a rebuild and page refresh, you'll see the content of mock data listing #5 in the page:

Figure 5.22. Listing page with mock data

To verify, and to admire our work, let's try another route, for example, /listing/10:

Figure 5.23. Listing page with mock data

Summary

In this chapter, we got familiar with the files and configuration of Laravel's default frontend app. We then migrated the Vuebnb client app prototype into our Laravel project, achieving the first full-stack iteration of Vuebnb.

We also learned about Webpack, seeing how it addresses the JavaScript dependency management problem by bundling modules into a browser-friendly build file. We set up Webpack in our project via Laravel Mix, which offers a simple API for common build scenarios.

We then investigated tools for making our frontend development process easier, including Webpack watch mode and BrowserSync.

Finally, we saw how to get data from the backend into the frontend app by injecting it into the document head.

In Chapter 6, Composing Widgets with Vue.js Components, we will be introduced to one of the most important and powerful tools for building user interfaces with Vue.js: components. We will build an image carousel for Vuebnb, and use knowledge of components to refactor the Vuebnb client app into a flexible component-based architecture.

Composing Widgets with Vue.js Components

