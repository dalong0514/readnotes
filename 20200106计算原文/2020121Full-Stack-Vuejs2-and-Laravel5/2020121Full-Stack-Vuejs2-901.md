# 0901. Adding a User Login and API Authentication with Passport

In the last chapter, we allowed the user to save their favorite Vuebnb listings. This feature was only implemented in the frontend app though, so if the user reloaded the page their selections would be lost.

In this chapter, we'll create a user login system and persist saved items to the database so they can be retrieved after a page refresh.

Topics covered in this chapter:

Setting up a user login system utilizing Laravel's built-in authentication features

Creating a login form with CSRF protection

Using Vuex actions for asynchronous operations in the store

A brief introduction to the OAuth protocol for API authentication

Setting up Laravel Passport to allow authenticated AJAX requests

User model

In order to save listing items to the database, we first need a user model, as we want each user to have their own unique list. Adding a user model means we'll also need an authentication system so that users can sign in and out. Fortunately, Laravel provides a full-featured user model and authentication system out-of-the-box.

Let's now take a look at the user model boilerplate files to see what modifications will be needed to fit them for our purposes.

Migration

Looking first at the database migration, the user table schema already includes ID, name, email, and password columns.

database/migrations/2014_10_12_000000_create_users_table.php:

<?php use Illuminate\Support\Facades\Schema; use Illuminate\Database\Schema\Blueprint; use Illuminate\Database\Migrations\Migration; class CreateUsersTable extends Migration { public function up() { Schema::create('users', function (Blueprint $table) { $table->increments('id'); $table->string('name'); $table->string('email')->unique(); $table->string('password'); $table->rememberToken(); $table->timestamps(); }); } public function down() { Schema::dropIfExists('users'); } }

This schema will be sufficient for our needs if we add an additional column for storing the saved listing IDs. Ideally, we'd store these in an array, but since relational databases don't have an array column type, we will instead store them as a serialized string, for example, [1, 5, 10] within a text column.

database/migrations/2014_10_12_000000_create_users_table.php:

Schema::create('users', function (Blueprint $table) { ... $table->text('saved'); });

Model

Let's now take a look now at the User model class that Laravel provides.

app/User.php:

<?php namespace App; use Illuminate\Notifications\Notifiable; use Illuminate\Foundation\Auth\User as Authenticatable; class User extends Authenticatable { use Notifiable; protected $fillable = [ 'name', 'email', 'password', ]; protected $hidden = [ 'password', 'remember_token', ]; }

The default configuration is fine, but let's allow the saved attribute to be mass assignable by adding it to the $fillable array.

We'll also get our model to serialize and deserialize the saved text when we read it or write it. To do this we can add a $casts attribute to the model and cast saved as an array.

app/User.php:

class User extends Authenticatable { ... protected $fillable = [ 'name', 'email', 'password', 'saved' ]; ... protected $casts = [ 'saved' => 'array' ]; }

Now we can treat the saved attribute as an array, even though it's stored as a string in the database:

echo gettype($user->saved()); // array

Seeder

In a normal web app with a login system, you'd have a registration page so users can create their own accounts. To ensure this book doesn't get too long, we'll skip that feature and instead generate user accounts with a database seeder:

$ php artisan make:seeder UsersTableSeeder

You can implement a registration page for Vuebnb yourself if you want. The Laravel documentation covers it quite thoroughly at https://laravel.com/docs/5.5/authentication.

Let's create at least one account with a name, email, password, and an array of saved listings. Note that I've used the make method of the Hash facade to hash the password rather than storing it as plain-text. Laravel's default LoginController will automatically verify plain-text passwords against the hash during the login process.

database/seeds/UsersTableSeeder.php:

<?php use Illuminate\Database\Seeder; use App\User; use Illuminate\Support\Facades\Hash; class UsersTableSeeder extends Seeder { public function run() { User::create([ 'name' => 'Jane Doe', 'email' => 'test@gmail.com', 'password' => Hash::make('test'), 'saved' => [1,5,7,9] ]); } }

To run the seeder we need to call it from the main DatabaseSeeder class.

database/seeds/DatabaseSeeder.php:

<?php use Illuminate\Database\Seeder; class DatabaseSeeder extends Seeder { public function run() { $this->call(ListingsTableSeeder::class); $this->call(UsersTableSeeder::class); } }

Let's now rerun our migrations and seeder to install the user table and data with the following command:

$ php artisan migrate:refresh --seed

To confirm that our user table and data were created correctly, we'll use Tinker to query the table. You should get an output similar to the following:

$ php artisan tinker >>> DB::table('users')->get(); /* { "id": 1, "name": "Jane Doe", "email": "test@gmail.com", "password": "...", "remember_token": null, "created_at": "2017-10-27 02:30:31", "updated_at": "2017-10-27 02:30:31", "saved": "[1,5,7,9]" } */

Login system

Now that we have our user model created, we can implement the rest of the login system. Again, Laravel includes this as an out-of-the-box feature, so there is only a small amount of configuration for us to do.

Here's an overview of how the login system works:

The user provides their email and password in a login form. We'll create this form with Vue

The form is submitted to the /login POST route

The LoginController will then verify the user's credentials against the database

If the login is successful, the user is redirected to the home page. A session cookie is attached to the response, which is then passed to all outgoing requests to verify the user

Here's a diagrammatic representation of the login system for further clarity:

Figure 9.1. Login flow

LoginPage component

We will need a login page for our app, so let's create a new page component:

$ touch resources/assets/components/LoginPage.vue

We'll begin by defining the template markup, which includes a form with fields for email and password, and a submit button. The form uses the HTTP POST method and is sent to the /login path. I've wrapped the form elements in a div with the .form-controller class to help with styling.

resources/assets/components/LoginPage.vue:

<template> <div id="login" class="login-container"> <form role="form" method="POST" action="/login"> <div class="form-control"> <input id="email" type="email" name="email" placeholder="Email Address" required autofocus> </div> <div class="form-control"> <input id="password" type="password" name="password" placeholder="Password" required> </div> <div class="form-control"> <button type="submit">Log in</button> </div> </form> </div> </template>

We don't need any JavaScript functionality just yet, so let's add our CSS rules now.

resources/assets/components/LoginPage.vue:

<template>...</template> <style> #login form { padding-top: 40px; } @media (min-width: 744px) { #login form { padding-top: 80px; } } #login .form-control { margin-bottom: 1em; } #login input[type=email], #login input[type=password], #login button, #login label { width: 100%; font-size: 19px !important; line-height: 24px; color: #484848; font-weight: 300; } #login input { background-color: transparent; padding: 11px; border: 1px solid #dbdbdb; border-radius: 2px; box-sizing:border-box } #login button { background-color: #4fc08d; color: #ffffff; cursor: pointer; border: #4fc08d; border-radius: 4px; padding-top: 12px; padding-bottom: 12px; } </style>

We'll add a login-container class to our global CSS file so the footer for this page aligns correctly. We'll also add a CSS rule to ensure text inputs display correctly on iPhone. The login page will be the only place we'll have a text input, but let's add it as a global rule in case you decide to add other forms later.

resources/assets/css/style.css:

... .login-container { margin: 0 auto; padding: 0 12px; } @media (min-width: 374px) { .login-container { width: 350px; } }

input[type=text] { -webkit-appearance: none; }

Finally, let's add this new page component to our router. We'll first import the component then add it to our routes array in the router configuration.

Note that the login page does not require any data from the server like the other pages of Vuebnb do. This means that we can skip the data-fetching step by modifying the logic of the first if statement in the navigation guard. It should now resolve straightaway if the name of the route is login.

resources/assets/js/router.js:

... import LoginPage from '../components/LoginPage.vue'; let router = new VueRouter({ ... routes: [ ... { path: '/login', component: LoginPage, name: 'login' } ], ... }); router.beforeEach((to, from, next) => { ... if ( to.name === 'listing' ? store.getters.getListing(to.params.listing) : store.state.listing_summaries.length > 0 || to.name === 'login' ) { next(); } ... }); export default router;

Server routes

Now that we've added a login page at the /login route, we will need to create a matching server-side route. We will also need a route for the login form that posts to the same /login path.

In fact, both of these routes are provided out-of-the-box by Laravel as part of its default login system. All we have to do to activate the routes is add the following line to the bottom of our web route file.

routes/web.php:

... Auth::routes();

To see the effect of this code, we can use Artisan to show a list of the routes in our app:

$ php artisan route:list

Output:

Figure 9.2. Terminal output showing routes list

You'll see all the routes that we've manually created, plus a few that we didn't, for example, login, logout, and register. These are the routes used by Laravel's authentication system that we just activated.

Looking at the GET/HEAD /login route, you'll see that it points to the LoginController controller. Let's take a look at that file.

App\Http\Controllers\Auth\LoginController.php:

<?php namespace App\Http\Controllers\Auth; use App\Http\Controllers\Controller; use Illuminate\Foundation\Auth\AuthenticatesUsers; class LoginController extends Controller { use AuthenticatesUsers; protected $redirectTo = '/home'; public function __construct() { $this->middleware('guest')->except('logout'); } }

This class uses an AuthenticatesUsers trait that defines the showLoginForm method that the /login route handler refers to. Let's overwrite that method so it simply returns our app view. Since this instance of the view doesn't need any data to be inlined in the head (the login form has no state), we will pass an empty array to the data template variable.

App\Http\Controllers\Auth\LoginController.php:

class LoginController extends Controller { ... public function showLoginForm() { return view('app', ['data' => []]); } }

With that done, we can now see our complete login page by navigating the browser to /login:

Figure 9.3. Login page

CSRF protection

CSRF (cross-site request forgery) is a type of malicious exploit where an attacker gets a user to unknowingly perform an action on a server that they're currently logged in to. This action will change something on the server that is advantageous to the attacker, for example, transfer money, change the password to one the attacker knows, and so on.

For example, an attacker might hide a script in a web page or email and direct the user to it somehow. When it executes, this script could make a POST request to importantwebsite.com/updateEmailAndPassword. If the user is logged in to this site, the request may be successful.

One way to prevent this kind of attack is to embed a special token, essentially a random string, in any form that a user might submit. When the form is submitted, the token is checked against the user's session to make sure it matches. An attacker won't be able to forge this token in their script and should, therefore, be thwarted by this feature.

In Laravel, CSRF token creation and verification is managed by the VerifyCsrfToken middleware that is added to the web routes by default:

Figure 9.4. CSRF prevention process

To include the CSRF token in a form you can simply add {{ csrf_field() }} within the form tag. This will generate a hidden input field containing a valid CSRF token, for example:

<input type="hidden" name="_token" value="3B08L3fj...">

This won't work in our scenario, though, as our form is not inside a Blade view but inside a single-file component that will not get processed by Blade. As an alternative, we can add the CSRF token to the head of the page and assign it to the window object.

resources/views/app.blade.php:

<script type="text/javascript"> window.vuebnb_server_data = "{!! addslashes(json_encode($data)) !!}" window.csrf_token = "{{ csrf_token() }}" </script>

We can now retrieve this from within our Vue.js app and manually add it to the login form. Let's modify LoginPage to include a hidden input field in the form. We'll add some state to this component now, in which the token is included as a data property and bound to the hidden field.

resources/assets/js/components/LoginPage.vue:

<template> <div id="login" class="login-container"> <form role="form" method="POST" action="/login"> <input type="hidden" name="_token" :value="csrf_token"> ... </form> </div> </template> <script> export default { data() { return { csrf_token: window.csrf_token } } } </script> <style>...</style>

If we now try to log in to our app using the credentials of the user we created in the seeder, we'll get served this error page. Looking in the address bar, you'll see that the route we're on is /home, which is not a valid route within our app, hence the NotFoundHttpException:

Figure 9.5. Invalid route

Post-login redirection

When a user logs in, Laravel will redirect them to a page defined by the $redirectTo attribute in the login controller. Let's change this from /home to /.

app/Http/Auth/Controllers/LoginController.php:

class LoginController extends Controller { ... protected $redirectTo = '/'; ... }

Let's also update the RedirectIfAuthenticated middleware class so that if a logged-in user attempts to view the login page, they're redirect to / (instead of the default /home value.)

app/Http/Middleware/RedirectIfAuthenticated.php:

... if (Auth::guard($guard)->check()) { return redirect('/'); }

With that done, our login process will now work correctly.

Adding authentication links to the toolbar

Let's now add login and logout links in the toolbar so Vuebnb users can easily access these features.

The login link is simply a RouterLink pointing to the login route.

The logout link is a bit more interesting: we capture the click event from this link and trigger the submission of a hidden form. This form sends a POST request to the /logout server route, which logs the user out and redirects them back to the home page. Note that we must include the CSRF token as a hidden input for this to work.

resources/assets/components/App.vue:

<template> ... <ul class="links"> <li> <router-link :to="{ name: 'saved' }"> Saved </router-link> </li> <li> <router-link :to="{ name: 'login' }"> Log In </router-link> </li> <li> <a @click="logout">Log Out</a> <form

style="display: hidden"

action="/logout"

method="POST"

id="logout"

> <input type="hidden" name="_token" :value="csrf_token"/> </form> </li> </ul> ... </template> <script> ... export default { components: { ... }, data() { return { csrf_token: window.csrf_token } }, methods: { logout() { document.getElementById('logout').submit(); } } } </script>

Protecting the saved route

We can use our login system now to protect certain routes from guests, that is, unauthenticated users. Laravel provides the auth middleware, which can be applied to any route and will redirect a guest user to the login page if they attempt to access it. Let's apply this to our saved page route.

routes/web.php:

Route::get('/saved', 'ListingController@get_home_web')->middleware('auth');

If you log out of the application and attempt to access this route from the navigation bar of your browser, you'll find it redirects you back to /login.

Passing authentication state to the frontend

We now have a complete mechanism for logging users in and out of Vuebnb. However, the frontend app is not yet aware of the user's authentication state. Let's remedy that now so we can add authentication-based features to the frontend.

auth meta property

We'll begin by adding the authentication state to the meta information we pass through in the head of each page. We'll utilize the Auth facade check method, which returns true if the user is authenticated, and assign this to a new auth property.

app/Http/Controllers/ListingController.php:

... use Illuminate\Support\Facades\Auth; class ListingController extends Controller { ... private function add_meta_data($collection, $request) { return $collection->merge([ 'path' => $request->getPathInfo(), 'auth' => Auth::check() ]); } }

We'll also add an auth property to our Vuex store. We'll mutate it from the addData method which, as you'll recall from the previous chapter, is where we retrieve data from the document head or API. Since the API does not include meta data, we'll conditionally mutate the auth property to avoid accessing a potentially undefined object property.

resources/assets/js/store.js:

... export default new Vuex.Store({ state: { ... auth: false }, mutations: { ... addData(state, { route, data }) { if (data.auth) { state.auth = data.auth; } if (route === 'listing') { state.listings.push(data.listing); } else { state.listing_summaries = data.listings; } } }, getters: { ... } });

With that done, Vuex is now tracking the authentication state of the user. Be sure to test this out by logging in and out and noticing the value of auth in the Vuex tab of Vue Devtools:

Figure 9.6. Value of auth in Vue Devtools

Responding to authenticated state

Now that we're tracking the authentication state of the user, we can get Vuebnb to respond to it. For one, let's make it so that a user can't save a listing unless they're logged in. To do this, we'll modify the behavior of the toggleSaved mutator method so that if the user is logged in they can save an item, but if not they are redirected to the login page via the push method of Vue Router.

Note that we'll have to import our router module at the top of the file to access its features.

resources/assets/js/store.js:

... import router from './router'; export default new Vuex.Store({ ... mutations: { toggleSaved(state, id) { if (state.auth) { let index = state.saved.findIndex(saved => saved === id); if (index === -1) { state.saved.push(id); } else { state.saved.splice(index, 1); } } else { router.push('/login'); } }, ... }, ... });

We'll also make it so that either the login link or the logout link is shown in the toolbar, never both. This can be achieved by using v-if and v-else directives in the toolbar that depend on the $store.state.auth value.

It would also make sense to hide the saved page link unless the user is logged in, so let's do that as well.

resources/assets/components/App.vue:

<ul class="links"> <li v-if="$store.state.auth"> <router-link :to="{ name: 'saved' }"> Saved </router-link> </li> <li v-if="$store.state.auth"> <a @click="logout">Log Out</a> <form

style="display: hidden"

action="/logout"

method="POST"

id="logout"

> <input type="hidden" name="_token" :value="csrf_token"/> </form> </li> <li v-else> <router-link :to="{ name: 'login' }"> Log In </router-link> </li> </ul>

This is how the toolbar will look now, depending on whether the user is logged in or out:

Figure 9.8. Comparison of the logged in and logged out state in toolbar

Retrieving saved items from the database

Let's now work on retrieving the saved items from the database and displaying them in the frontend. To begin with, we'll add a new saved property to the metadata we put in the document head. This will be an empty array if the user is logged out, or the array of saved listing IDs associated with that user, if they're logged in.

app/Http/Controllers/ListingController.php:

private function add_meta_data($collection, $request) { return $collection->merge([ 'path' => $request->getPathInfo(), 'auth' => Auth::check(), 'saved' => Auth::check() ? Auth::user()->saved : [] ]); }

Back in the frontend, we'll put the logic for retrieving the saved items in the beforeEach router navigation guard. The reason we put it here and not in the addData mutation is that we don't want to directly assign the data to the store state, but instead call the toggleSaved mutation for each of the listings. You can't commit a mutation from another mutation, so this must be done outside the store.

resources/assets/js/router.js:

router.beforeEach((to, from, next) => { let serverData = JSON.parse(window.vuebnb_server_data); if ( ... ) { ... } else if ( ... ) { ... } else { store.commit('addData', {route: to.name, data: serverData}); serverData.saved.forEach(id => store.commit('toggleSaved', id)); next(); } });

Let's also remove the placeholder listing IDs we added to saved in the previous chapter so the store is empty upon initialization.

resources/assets/js/store.js:

state: { saved: [], listing_summaries: [], listings: [], auth: false }

With that done, we should find that the saved listings in the database now match those in the frontend if we check with Vue Devtools:

$ php artisan tinker >>> DB::table('users')->select('saved')->first(); # "saved": "[1,5,7,9]"

Figure 9.8. Vuex tab of Vue Devtools shows saved listings match database

Persisting saved listings

The mechanism for persisting saved listings is as follows: when a listing is toggled in the frontend app, we trigger an AJAX request that POSTs the ID to a route on the backend. This route calls a controller that will update the model:

Figure 9.9. Persisting saved listings

Let's now implement this mechanism.

Creating an API route

We'll begin on the server side and add a route for the frontend to POST listing IDS to. We'll need to add the auth middleware so that only authenticated users can access this route (we'll discuss the meaning of :api shortly).

routes/api.php:

...

Route::post('/user/toggle_saved', 'UserController@toggle_saved')

->middleware('auth:api')

;

Since this is an API route, its full path will be /api/user/toggle_saved. We haven't yet created the controller that this route calls, UserController, so let's do that now:

$ php artisan make:controller UserController

In this new controller, we'll add the toggled_saved handling method. Since this is an HTTP POST route, this method will have access to the form data. We'll make it so that the frontend AJAX call to this route includes an id field, which will be the listing ID we want to toggle. To access this field, we can use the Input facade, that is, Input::get('id');.

Since we're using the auth middleware on this route, we can retrieve the user model associated with the request by using the Auth::user() method. We can then either add or remove the ID from the user's saved listings, just as we do in the toggledSaved method in our Vuex store.

Once the ID is toggled, we can then use the model's save method to persist the update to the database.

app/Http/Controllers/UserController.php:

<?php ... use Illuminate\Support\Facades\Auth; use Illuminate\Support\Facades\Input; class UserController extends Controller { public function toggle_saved() { $id = Input::get('id'); $user = Auth::user(); $saved = $user->saved; $key = array_search($id, $saved); if ($key === FALSE) { array_push($saved, $id); } else { array_splice($saved, $key, 1); } $user->saved = $saved; $user->save(); return response()->json(); } }

Vuex actions

In Chapter 8, Managing Your Application State With Vuex, we discussed the key principles of the Flux pattern, including the principle that mutations must be synchronous to avoid race conditions that make our application data unpredictable.

If you have a need to include asynchronous code in a mutator method, you should instead create an action. Actions are like mutations, but instead of mutating the state, they commit mutations. For example:

var store = new Vuex.Store({ state: { val: null }, mutations: { assignVal(state, payload) { state.val = payload; } }, actions: { setTimeout(() => { commit('assignVal', 10); }, 1000) } }); store.dispatch('assignVal', 10);

By abstracting asynchronous code into actions we can still centralize any state-altering logic in the store without tainting our application data through race conditions.

AJAX request

Let's now use AJAX to make the request to /api/user/toggle_saved when a listing is saved. We'll put this logic into a Vuex action so that the toggleSaved mutation is not committed until the AJAX call resolves. We'll import the Axios HTTP library into the store to facilitate this.

Also, let's move the authentication check from the mutation to the action, as it makes sense to do this check before the AJAX call is initiated.

resources/assets/js/store.js:

import axios from 'axios'; export default new Vuex.Store({ ... mutations: { toggleSaved(state, id) { let index = state.saved.findIndex(saved => saved === id); if (index === -1) { state.saved.push(id); } else { state.saved.splice(index, 1); } }, ... }, ... actions: { toggleSaved({ commit, state }, id) { if (state.auth) { axios.post('/api/user/toggle_saved', { id }).then( () => commit('toggleSaved', id) ); } else { router.push('/login'); } } } });

We now need to call the toggledSaved action, not the mutation, from our ListingSave component. Calling an action is done in exactly the same way as a mutation, only the terminology changes from commit to dispatch.

resources/assets/components/ListingSave.vue:

toggleSaved() { this.$store.dispatch('toggleSaved', this.id); }

The code for this feature in the frontend is correct, but if we test it out and try and save an item we get a 401 Unauthenticated error from the server:

Figure 9.10. AJAX call results in a 401 Unauthenticated error

API authentication

We added the auth middleware to our /api/user/toggle_saved route to protect it from guest users. We also specified the api guard for this middleware, that is, auth:api.

Guards define how users are authenticated and are configured in the following file.

config/auth.php:

<?php return [ ... 'guards' => [ 'web' => [ 'driver' => 'session', 'provider' => 'users', ], 'api' => [ 'driver' => 'token', 'provider' => 'users', ], ], ... ];

Our web routes use the session driver which maintains authentication state using session cookies. The session driver ships with Laravel and works out-of-the-box. API routes, though, use the token guard by default. We have not yet implemented this driver, hence our AJAX calls are unauthorized.

We could use the session driver for API routes as well, but this is not recommended, as session authentication is not sufficient for AJAX requests. We're instead going to use the passport guard, which implements the OAuth protocol.

You may see auth used as a shorthand for auth:web, as the web guard is the default.

OAuth

OAuth is an authorization protocol that allows third-party applications to access a user's data on a server without exposing their password. Access to this protected data is given in exchange for a special token that is granted to the application once it, and the user, have identified themselves to the server. A typical use case for OAuth is social login, for example, when you utilize a Facebook or Google login for your own website.

One challenge of making secure AJAX requests is that you can't store any credentials in the frontend source code, as it's trivial for an attacker to find these. A simple implementation of OAuth, where the third-party application is actually your own frontend app, is a good solution to the issue. This is the approach we'll be taking now for Vuebnb.

While OAuth is a great solution for API authentication, it is also quite an in-depth topic that I can't fully cover in this book. I recommend you read this guide to get a better understanding: https://www.oauth.com/.

Laravel Passport

Laravel Passport is an implementation of OAuth that can easily be set up in a Laravel application. Let's install it now for use in Vuebnb.

First, install Passport with Composer:

$ composer require laravel/passport

Passport includes new database migrations that generate the tables needed to store OAuth tokens. Let's run the migration:

$ php artisan migrate

The following command will install the encryption keys needed to generate secure tokens:

$ php artisan passport:install

After running this command, add the Laravel\Passport\HasApiTokens trait to the user model.

app/User.php:

<?php ...

use Laravel\Passport\HasApiTokens; class User extends Authenticatable { use HasApiTokens, Notifiable; ... }

Finally, in the config/auth.php configuration file, let's set the driver option of the API guard to passport. This ensures the auth middleware will use Passport as a guard for API routes.

config/auth.php:

'guards' => [ 'web' => [ 'driver' => 'session', 'provider' => 'users', ], 'api' => [ 'driver' => 'passport', 'provider' => 'users', ], ],

Attaching tokens

OAuth requires an access token to be sent to the frontend app when the user logs in. Passport includes a middleware that can handle this for you. Add the CreateFreshApiToken middleware to the web middleware group and the laravel_token cookie will be attached to outgoing responses.

app/Http/Kernel.php:

protected $middlewareGroups = [ 'web' => [ ... \Laravel\Passport\Http\Middleware\CreateFreshApiToken::class, ], ...

For outgoing requests, we need to add some headers to our AJAX calls. We can make it so Axios automatically attaches these by default. 'X-Requested-With': 'XMLHttpRequest' ensures that Laravel knows the request was from AJAX, while 'X-CSRF-TOKEN': window.csrf_token attaches the CSRF token.

resources/assets/js/store.js:

... axios.defaults.headers.common = { 'X-Requested-With': 'XMLHttpRequest', 'X-CSRF-TOKEN': window.csrf_token }; export default new Vuex.Store({ ... });

With that done, our API requests should now be properly authenticated. To test this, let's use Tinker to see which items we have saved for our first seeded user:

$ php artisan tinker >>> DB::table('users')->select('saved')->first(); # "saved": "[1,5,7,9]"

Make sure you're logged in as that user and load Vuebnb in the browser. Toggle a few of your saved listing selections and rerun the query above. You should find that the database is now persisting the saved listing IDs.

## Summary

In this chapter, we learned about authentication in full-stack Vue/Laravel apps, including session-based authentication for web routes, and token-based authentication for API routes using Laravel Passport. We used this knowledge to set up a login system for Vuebnb, and to allow saved room listings to be persisted to the database. Along the way, we also learned how to utilize CSRF tokens for securing forms, and about Vuex actions for adding asynchronous code to the store.

In the next, and final, chapter, we will learn how to deploy a full-stack Vue and Laravel app to production by deploying Vuebnb to a free Heroku PHP server. We will also begin serving images and other static content from a free CDN.