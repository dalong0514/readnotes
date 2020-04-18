Now that the functionality of Vuebnb is complete, the final step is to deploy it to production. We'll use two free services, Heroku and KeyCDN, to share Vuebnb with the world.

Topics covered in this chapter:

An introduction to the Heroku cloud platform service

Deploying Vuebnb to Heroku as a free app

How CDNs improve the performance of full-stack apps

Integrating a free CDN with Laravel

Building assets in production-mode for performance and security

Heroku

Heroku is a cloud platform service for web applications. It's immensely popular among developers due to the simplicity and affordability it offers for getting apps online.

Heroku applications can be made in a variety of languages including PHP, JavaScript, and Ruby. In addition to a web server, Heroku offers a variety of add-ons, such as databases, email services, and application monitoring.

Heroku apps can be deployed for free, though there are certain limitations, for example, the app will sleep after periods of inactivity, making it slow to respond. These limitations are lifted if you upgrade to a paid service.

We will now deploy Vuebnb to the Heroku platform. The first step is to create an account by visiting the following URL: https://signup.heroku.com.

CLI

The most convenient way to use Heroku is from the command line. Visit the following URL and follow the steps for installation: https://devcenter.heroku.com/articles/heroku-cli.

Once you've installed the CLI, log in to Heroku from the Terminal. After verifying your credentials you'll be able to use the CLI to create and manage your Heroku apps:

$ heroku login # Enter your Heroku credentials: # Email: anthony@vuejsdevelopers.com # Password: ************ # Logged in as anthony@vuejsdevelopers.com

Creating an app

Let's now create a new Heroku app. New apps require a unique name, so replace vuebnbapp in the command below with your own choice. The name will be part of the app's URL, so make sure it's short and memorable:

$ heroku create vuebnbapp

Once the app is created you will be given the URL, for example: https://vuebnbapp.herokuapp.com/. Put it in the browser and you'll see this default message:

Figure 10.1. Heroku default message

New Heroku apps are assigned a free domain name, for example: appname.herokuapp.com, but you can also use your own custom domain. See the Heroku Dev Center for more information at https://devcenter.heroku.com.

Source code

To deploy code to your Heroku app you can use Heroku's Git server. When you created your app with the CLI, a new remote repository was automatically added to your Git project. Confirm this with the following command:

$ git remote -v heroku https://git.heroku.com/vuebnbapp.git (fetch) heroku https://git.heroku.com/vuebnbapp.git (push) origin git@github.com:fsvwd/vuebnb.git (fetch) origin git@github.com:fsvwd/vuebnb.git (push)

Once we've completed the configuration of our app we'll make our first push. Heroku will use this code to build the app.

Environment variables

Heroku apps have an ephemeral filesystem that only includes code from the most recent Git push. This means Vuebnb will not have its .env file present since this file is not committed to the source code.

Environment variables are instead set by Heroku CLI, with the heroku config command. Let's begin by setting the app key. Replace the following value with your own app key:

$ heroku config:set APP_KEY=base64:mDZ5lQnC2Hq+M6G2iesFzxRxpr+vKJSl+8bbGs=

Creating a database

We need a database for our production app. The ClearDB add-on for Heroku provides a MySQL cloud database that is easy to set up and connect.

This add-on is free for a limited number of transactions each month. However, you will need to verify your Heroku account before you can add a database, which means you'll need to supply credit card details, even if you use the free plan.

To verify your Heroku account, go to this URL: https://heroku.com/verify.

Once you've done that, create a new ClearDB database with this command:

$ heroku addons:create cleardb:ignite

Default string length

At the time of writing, ClearDB uses MySQL version 5.5, while our Homestead database is MySQL 5.7. The default string length in MySQL 5.5 is too short for Passport authorization keys, so we need to manually set the default string length in the app service provider before we run the database migrations in our production app.

app/Providers/AppServiceProvider.php:

<?php ... use Illuminate\Support\Facades\Schema; class AppServiceProvider extends ServiceProvider { ... public function boot() { Schema::defaultStringLength(191); } ... }

Configuration

When you installed the ClearDB add-on, a new environment variable, CLEARDB_DATABASE_URL, was automatically set. Let's read its value using the heroku config:get command:

$ heroku config:get CLEARDB_DATABASE_URL # mysql://b221344377ce82c:398z940v@us-cdbr-iron-east-03.cleardb.net/heroku_n0b30ea856af46f?reconnect=true

In a Laravel project, the database is connected by setting values for DB_HOST and DB_DATABASE. We can extract the values for these from the CLEARDB_DATABASE_URL variable, which is in the form:

mysql://[DB_USERNAME]:[DB_PASSWORD]@[DB_HOST]/[DB_DATABASE]?reconnect=true

Once you've extracted the values, set the applicable environment variables in the Heroku app:

$ heroku config:set \ DB_HOST=us-cdbr-iron-east-03.cleardb.net \ DB_DATABASE=heroku_n0b30ea856af46f \ DB_USERNAME=b221344377ce82c \ DB_PASSWORD=398z940v

Configuring a web server

Web server configuration for Heroku is done via a special file called Procfile (no file extension) that lives in the root of your project directory.

Let's now create that file:

$ touch Procfile

Each line of the Procfile is a declaration that tells Heroku how to run various pieces of your app. Let's create a Procfile for Vuebnb now and add this single declaration.

Procfile:

web: vendor/bin/heroku-php-apache2 public/

The part to the left of the colon is the process type. The web process type defines where HTTP requests are sent in the app. The part to the right is the command to run or start that process. We will route requests to an Apache server that points to the public directory of our app.

Passport keys

In Chapter 9, Adding a User Login and API Authentication with Passport, we created encryption keys for Passport with the php artisan passport:install command. These keys are stored in text files that can be found in the storage directory.

Encryption keys should not be under version control, as this would make them insecure. Instead, we need to regenerate these keys on each deploy. We can do this by adding a post-install script to our composer file.

composer.json:

"scripts": {

...

"post-install-cmd": [ "Illuminate\\Foundation\\ComposerScripts::postInstall", "php artisan optimize",

"php artisan passport:install" ],

}

Deployment

We've done all the necessary set up and configuration, so we're ready now to deploy Vuebnb. Make sure you commit any file changes to your Git repository and push to the master branch of the Heroku Git server:

$ git add --all $ git commit -m "Ready for deployment!" $ git push heroku master

During the push you'll see the output similar to the following:

Figure 10.2. Git output after a push to Heroku

Something wrong with your Heroku app that needs debugging? heroku logs --tail will show you the Terminal output from your Heroku app. You can also set the APP_DEBUG=true environment variable to debug Laravel. Remember to set it back to false when you've finished, though.

Migration and seed

Once the deploy completes, we will migrate our tables and seed the database. You can run Artisan and other app commands on the production app via Heroku CLI by preceding them with heroku run:

$ heroku run php artisan migrate --seed

Once the migration and seeding are complete, we can attempt to view the app via the browser. The page should be served but you'll see these mixed content errors:

Figure 10.3. Console errors

Fixing these errors won't help much, as the files referred to are not on the server anyway. Let's deal with that issue first.

Serving static assets

Since our static assets, that is, CSS, JavaScript and image files, are not in version control, they have not been deployed to our Heroku app server.

This is okay, though, as a better option is to serve them via a CDN. In this part of the chapter, we'll set up an account with KeyCDN and serve our static assets from there.

Content distribution networks

When a server receives an incoming HTTP request, it usually responds with one of two types of content: dynamic or static. Dynamic content includes web pages or AJAX responses containing data specific to that request, for example, a web page with user data inserted via Blade.

Static content includes images, JavaScript, and CSS files that do not change between requests. It's inefficient to use a web server for serving static content since it unnecessarily engages the server resources to simply return a file.

A Content Delivery Network (CDN) is a network of servers, usually in different locations around the world, that are optimized for delivering static assets more quickly and cheaply than your typical web server.

KeyCDN

There are many different CDN services available, but in this book we'll use KeyCDN as it offers an easy-to-use service with a free usage tier.

Let's sign up for an account by visiting this link and following the instructions: https://app.keycdn.com/signup.

Once you have created and confirmed a new KeyCDN account, add a new zone by visiting the following link. Zones are simply collections of assets; you'd probably have a different zone for each website you're managing with KeyCDN. Call your new zone vuebnb and make sure it's a Push zone type, which will allow us to add files with FTP: https://app.keycdn.com/zones/add.

Uploading files with FTP

We will now push our static assets to the CDN with FTP. You could use an FTP utility such as Filezilla to do this, but I've included a Node script with the project, scripts/ftp.js, that allows you to do it with a simple command.

The script requires a few NPM packages, so install those first:

$ npm i --save-dev dotenv ftp recursive-readdir

Environment variables

In order to connect to your KeyCDN account, the FTP script requires a few environment variables to be set. Let's create a new file called .env.node to keep this configuration separate from the main Laravel project:

$ touch .env.node

The URL used for FTP-ing to KeyCDN is ftp.keycdn.com. The username and password will be the same as those you created an account with, so be sure to replace those in the values in the following code. The remote directory will be the same as the name of the zone you created.

.env.node:

FTP_HOST=ftp.keycdn.com FTP_USER=anthonygore FTP_PWD=********* FTP_REMOTE_DIR=vuebnb FTP_SKIP_IMAGES=0

Skipping images

The files we need to transfer to the CDN are in the public/css, public/js, public/fonts, and public/images directories. The FTP script has been configured to recursively copy these.

If you set the FTP_SKIP_IMAGES environment variable to true, however, the script will ignore any files in public/images. You'll want to do this after you've run the script the first time, as the images don't change and take quite a while to transfer.

.env.node:

FTP_SKIP_IMAGES=1

You can see how this takes effect in scripts/ftp.js:

let folders = [ 'css', 'js', 'fonts' ]; if (process.env.FTP_SKIP_IMAGES == 0) { folders.push('images'); }

NPM scripts

To make it easy to use the FTP script, add the following script definitions to your package.json file.

package.json:

"ftp-deploy-with-images": "cross-env node ./ftp.js", "ftp-deploy": "cross-env FTP_SKIP_IMAGES=1 node ./ftp.js"

Production build

Before you run the FTP script, be sure to first build your app for production with the npm run prod command. This runs a Webpack build with the NODE_ENV=production environment variable set.

A production build ensures your assets are optimized for a production environment. For example, when Vue.js is bundled in production mode, it will not include warnings and tips, and will disable Vue Devtools. You can see how this is achieved from this snippet of the vue.runtime.common.js module.

node_modules/vue/dist/vue.runtime.common.js:

/** * Show production mode tip message on boot? */ productionTip: process.env.NODE_ENV !== 'production', /** * Whether to enable devtools */ devtools: process.env.NODE_ENV !== 'production',

Webpack will also run certain production-only plugins during a production build to ensure your bundle files are as small and secure as possible.

Running the FTP script

The first time you run the FTP script you will need to copy all the files, including images. This will take some time, probably 20 to 30 minutes depending on your Internet connection speed:

$ npm run prod && npm run ftp-deploy-with-images

Once the transfer completes, uploaded files will be available at the zone URL, for example, http://vuebnb-9c0f.kxcdn.com. The path to a file will be relative to the public folder, for example, public/css/vue-style.css will be available at [ZONE_URL]/css/vue-style.css.

Test a few files to ensure the transfer was successful:

>

Figure 10.4. Testing CDN files

Subsequent transfers can skip the images by using this command:

$ npm run prod && npm run ftp-deploy

Reading from the CDN

We now want Vuebnb to load any static assets from the CDN instead of the web server when in production. To do this, we're going to create our own Laravel helper method.

Currently, we reference assets in our app using the asset helper. This helper returns a fully-qualified URL for that asset's location on the web server. For example, in our app view we link to the JavaScript bundle file like this:

<script type="text/javascript" src="{{ asset('js/app.js') }}"></script>

Our new helper, which we'll call cdn, will instead return a URL that points to the asset's location on the CDN:

<script type="text/javascript" src="{{ cdn('js/app.js') }}"></script>

CDN helper

Let's begin by creating a file called helpers.php. This will declare a new cdn method which, for now, won't do anything but return the asset helper method.

app/helpers.php:

<?php if (!function_exists('cdn')) { function cdn($asset) { return asset($asset); } }

To ensure this helper is available to be used anywhere in our app, we can use Composer's autoload feature. This makes a class or file available to all other files without them having to manually include or require it.

composer.json:

... "autoload": { "classmap": [ ... ], "psr-4": { ... }, "files": [ "app/helpers.php" ] }, ...

Each time you modify Composer's autoload declaration you need to run dump-autoload:

$ composer dump-autoload

With that done, the cdn helper will be available for use within our app. Let's test it with Tinker:

$ php artisan tinker >>>> cdn('js/app.js') => "http://vuebnb.test/js/app.js"

Setting the CDN URL

The cdn helper method will need to know the URL of the CDN. Let's set an CDN_URL environment variable that will be assigned the zone URL for Vuebnb, minus the protocol prefix.

While we're at it, let's add another variable, CDN_BYPASS, that can be used to bypass the CDN in our local development environment where we won't need it.

.env:

... CDN_URL=vuebnb-9c0f.kxcdn.com CDN_BYPASS=0

Let's now register these new variables in the app configuration file.

config/app.php:

<?php return [ ... // CDN 'cdn' => [ 'url' => env('CDN_URL'), 'bypass' => env('CDN_BYPASS', false), ], ];

Now we can complete the logic of our cdn helper.

app/helpers.php:

<?php use Illuminate\Support\Facades\Config; if (!function_exists('cdn')) { function cdn($asset) { if (Config::get('app.cdn.bypass') || !Config::get('app.cdn.url')) { return asset($asset); } else { return "//" . Config::get('app.cdn.url') . '/' . $asset; } } }

If you still have Tinker open, exit and re-enter, and test the changes work as expected:

>>>> exit

$ php artisan tinker >>>> cdn('js/app.js') => "//vuebnb-9c0f.kxcdn.com/js/app.js"

Using the CDN in Laravel

Let's now replace usages of the asset helper in our Laravel files with the cdn helper.

app/Http/Controllers/ListingController.php:

<?php ... class ListingController extends Controller { private function get_listing($listing) { ... for($i = 1; $i <=4; $i++) { $model['image_' . $i] = cdn(

'images/' . $listing->id . '/Image_' . $i . '.jpg'

); } ... } ... private function get_listing_summaries() { ... $collection->transform(function($listing) { $listing->thumb = cdn( 'images/' . $listing->id . '/Image_1_thumb.jpg' ); return $listing; }); ... } ... }

resources/views/app.blade.php:

<html> <head> ... <link rel="stylesheet" href="{{ cdn('css/style.css') }}" type="text/css"> <link rel="stylesheet" href="{{ cdn('css/vue-style.css') }}" type="text/css"> ... </head> <body> ... <script src="{{ cdn('js/app.js') }}"></script> </body> </html>

Using the CDN in Vue

In our Vue app, we're loading some static assets as well. For example, in the toolbar we use the logo.

resources/assets/components/App.vue:

<img class="icon" src="/images/logo.png">

As this is a relative URL it will, by default, point to the web server. If we make it an absolute URL instead, we'd have to hard-code the CDN URL, which is not ideal either.

Let's instead get Laravel to pass the CDN URL in the head of the document. We can do this by simply calling the cdn helper with an empty string.

resources/views/app.blade.php:

<head> ... <script type="text/javascript"> ...

window.cdn_url = "{{ cdn('') }}"; </script> </head>

We'll now use a computed property to construct the absolute URL using this global value.

resources/assets/components/App.vue:

<template> ... <router-link :to="{ name: 'home' }"> <img class="icon" :src="logoUrl"> <h1>vuebnb</h1> </router-link> ... </template> <script> export default { computed: { logoUrl() { return `${window.cdn_url || ''}images/logo.png`; } }, ... } </script> <style>...</style>

We'll use the same concept in the footer where the grey logo is used.

resources/assets/components/CustomFooter.vue:

<template> ... <img class="icon" :src="logoUrl"> ... </template> <script> export default { computed: { containerClass() { ... }, logoUrl() { return `${window.cdn_url || ''}images/logo_grey.png`; } }, } </script>

Deploying to Heroku

With that done, commit any file changes to Git and push again to Heroku to trigger a new deploy. You'll also need to rebuild your frontend assets and transfer these to the CDN.

Finally, set the CDN environment variables:

$ heroku config:set \ CDN_BYPASS=0 \ CDN_URL=vuebnb-9c0f.kxcdn.com

Finale

You have now completed the case-study project for this book, a sophisticated full-stack Vue.js and Laravel application. Congratulations!

Be sure to show Vuebnb off to your friends and colleagues, as they'll no doubt be impressed with your new skills. I'd also appreciate if you tweeted me the link to your project so I can admire your work too. My Twitter handle is @anthonygore.

Recap

We've come a long way in this book, let's recap some of what we've achieved:

In Chapter 1, Hello Vue – An Introduction to Vue.js, we were introduced to Vue.js

In Chapter 2, Prototyping Vuebnb, Your First Vue.js Project, we learned the basics of Vue.js including installation, data binding, directives, and lifecycle hooks. We built a prototype of the listing page of Vuebnb including the image modal

In Chapter 3, Setting Up a Laravel Development Environment, we installed the main Vuebnb project and set up the Homestead development environment

In Chapter 4, Building a Web Service with Laravel, we created a Laravel web service to supply data for Vuebnb

In Chapter 5, Integrating Laravel and Vue.js with Webpack, we migrated the prototype into the main project and used Laravel Mix to compile our assets into bundle files

In Chapter 6, Composing Widgets with Vue.js Components, we learned about components. We used this knowledge to add an image carousel to the modal on the listing page and refactored the frontend to incorporate single-file components

In Chapter 7, Building a Multi-Page App With Vue Router, we added Vue Router to the project, allowing us to add a home page with the listing summary sliders

In Chapter 8, Managing Your Application State With Vuex, we introduced the Flux architecture and added Vuex to our app. We then created a save feature and moved page state into Vuex

In Chapter 9, Adding a User Login and API Authentication With Passport, we added a user login to the project. We sent the user's saved listings back to the database with an authenticated AJAX call

In Chapter 10, Deploying a Full-Stack App to the Cloud, we deployed the app to a Heroku cloud server and transferred static assets to a CDN

Next steps

You may have reached the end of the book, but your journey as a full-stack Vue developer has only just begun! What should you move on to next?

Firstly, there are still plenty more features you can add to Vuebnb. Designing and implementing these yourself will increase your skill and knowledge immensely. Here are a few ideas to get you started:

Complete the user authentication flow. Add a registration page and functionality for resetting passwords

Add a user profile page. Here, users can upload an avatar that will display in the toolbar when they're logged in

Create a form on the listing page that allows the room to be booked. Include a drop-down datepicker widget for selecting start and end dates

Server render the app by running Vue from a JavaScript sandbox on the server. This way users get a complete page with visible content when they load the site

Secondly, I invite you to check out Vue.js Developers, an online community for Vue.js enthusiasts that I founded. Here you can read articles on Vue.js, stay up-to-date with Vue.js news through our newsletter, and share tips and tricks with other developers in our Facebook group.

Check it out at this URL: https://vuejsdevelopers.com.

Summary

In this chapter, we learned how to deploy a full-stack app to a Heroku cloud server. To do this, we used the Heroku CLI to set up a new Heroku app, and then deployed it using Heroku's Git server.

We also created a CDN with KeyCDN, and used FTP to deploy our static assets to the CDN.

Finally, we learned why it's important for performance and security to build our JavaScript assets in production-mode ahead of deployment.

This is the final chapter of the book. Thank you for reading and good luck on your web development journey!

