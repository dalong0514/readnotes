## 记忆时间

## 卡片

### 0101. 反常识卡——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡—— DI

Laravel follows the MVC pattern of logic. But it has many more features that have enhanced the pattern’s features, elevating them to a new level. Laravel ships with a dependency injection (DI) mechanism by default (Figure 1-1). Figure 1-1. How DI works with an IoC container

If you are new to this important concept of software building and programming, don’t worry. I will discuss it in great detail later. For now, know that the DI mechanism is a way to add a class instance to another class instance using a class constructor.

The key concept of DI is that the abstraction (here, PaymentInterface) never worries about the details. The lower-level implementation modules (here, the PaymentGateway class) handle the details. In this case, it uses Stripe as a payment gateway. And the PaymentNotification class uses the abstraction to get those details. It also does not bother about what type of payment gateway has been used.

Now if the client changes the payment gateway from Stripe to PayPal, you don’t have to hard-code it into the class that uses the payment gateway. In the implementation, you will change it, and any class into which you inject the implementation will reflect the change.

Depending on many classes is necessary. Managing those dependencies is not easy. Using an IoC container, you can manage the class dependencies as I have shown in the previous code. The IoC container resolves the dependencies easily. In fact, the IoC container is a central piece of the Laravel framework. This container can build complex objects for you. Note dI is a form of IoC, which is why the container that manages this is called an IoC container.

### 0202. 术语卡——

### 0203. 术语卡——

### 0301. 人名卡——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

### 0401. 金句卡——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 任意卡——

最后还有一张任意卡，记录个人阅读感想。

## Introduction

the book explains routing, controllers, templates, and views in detail so that beginners can get started easily. It explains how a resourceful controller can become your great friend in keeping resources separated.

While introducing models, I also explain route model binding, model relations, and the relationship between models, databases, and Eloquent. I also explain how user input and dependency injection work together and how Elixir and pagination work. Understanding Eloquent relationships is important, so this book explains all types of relations, including one-to-one, one-to-many, many-to-many, has-many-through, and polymorphic.

While learning about Query Builder and Database Facade, you will also learn how you use fake database data for testing purposes. Handling user data and redirecting it plays a big role in Laravel, so this is explained along with web form fundamentals and validations.

Artisan and Tinker are two great features of Laravel 5.8; you will learn about them in detail. You will also learn how to use SQLite in a small or medium-sized application.

In this book, you will get a detailed overview of authentication, authorization, and middleware; in addition, you will learn how authorization can be managed through Blade templates, gates, and policies.

After a detailed discussion of Laravel container and facades, you will learn how a mail template works, how one user can send a notification to another, and so on. Events and broadcasting also play vital roles in building complicated applications. The same is true for APIs; they are explained with examples.

## 01 Introduction to Laravel

### 1. 逻辑脉络

用自己的话总结主题，梳理逻辑脉络，也就是这本书整个地图里这一章所在的节点。

### 2. 摘录及评论

### 01. Laravel’s Flexibility

Laravel is a highly flexible PHP framework, and it makes complicated tasks easier to do. Laravel provides powerful tools for making large, robust applications; however, to accomplish that, you need to understand a few key concepts such as how to use IoC containers or service containers to manage class dependencies. The expressive migration system is another concept that you will learn about in detail in Chapter 5.

Behind the scenes, Laravel uses many design patterns, and as you progress through this book, you will find that from the beginning Laravel helps you code in a loosely coupled environment. The framework focuses on designing classes to have a single responsibility, avoiding hard-coding in the higher-level modules, and allowing IoC containers to have abstractions that depend on the details. Higher-level modules do not depend on the lower-level modules, making coding a joyful experience. As you progress through the book, you will find plenty of examples supporting this general paradigm. Because of this flexibility, Laravel has become one of the most popular frameworks today.

If you are not convinced, I will also say that without the help of a framework like Laravel, you would need to write thousands of lines of code that would probably start out by routing HTTP requests. In Laravel, it is simple and straightforward to route an HTTP request. This is defined in the routes/web.php file, as shown here:

```
//code 1.1 
//Laravel Route Example 
Route::get('/', function () { return view('welcome'); });
```

This defines the URL for an application. While defining the URL, Laravel also helps you return a Blade template page that you can use to nicely format and design your data. You will learn about this in detail in Chapter 3.

In any other framework, you won’t know how complicated the requests will be and what your responses will be. So, you’ll need response libraries to assist you in your framework, which could easily be a humongous task to implement.

Laravel can handle your request/response lifecycle quite easily. The complexity of requests does not matter here. Laravel’s HTTP middleware consists of little HTTP layers that surround your application. So, every request must pass through these HTTP middleware layers before hitting your application. They can intercept and interrupt the HTTP request/response lifecycle, so you can stay calm about all the security matters that are most important. 

From the beginning, you have a well-guarded application interface when you install Laravel. You can think the first layer as the authentication layer, whereas the middleware tests whether the user is authenticated. If the user is not authenticated, the user is sent back to the login page. If the user passes the test, the user must face the second layer, which could consist of CSRF token validation. The process goes on like this, and the most common use cases of the Laravel middleware that protects your application are authentication, CSRF token validation, maintenance mode, and so on. When your application is in maintenance mode, a custom view is displayed for all requests.

For any experienced developer, it takes many months to build well-structured containers that can handle such complex requests and at the same time terminate the response lifecycle at the proper time. Frameworks help you achieve this goal in a short period of time. Finding components is much easier; once you understand how routing works in Laravel, you can apply it quite easily for the rest of your working life.

1『要的框架真的可以省很多精力，而且研究框架设计者的思维也很价值。』

As a developer, you are here to solve multiple problems, and a framework like Laravel, in most cases, addresses those problems in an elegant way. So, you don’t have to write tons of libraries and worry about version changes. The makers of Laravel have already thought about that. Laravel’s author, Taylor Otwell, summarizes the flexible features of Laravel as follows (from a PHPWorld conference in 2014):

• Aim for simplicity.

• Minimal configuration.

• Terse, memorable, expressive syntax.

• Powerful infrastructure for modern PHP.

• Great for beginners and advanced developers.

• Embraces the PHP community.

### 02. How Laravel Works

Laravel follows the MVC pattern of logic. But it has many more features that have enhanced the pattern’s features, elevating them to a new level. Laravel ships with a dependency injection (DI) mechanism by default (Figure 1-1). Figure 1-1. How DI works with an IoC container

If you are new to this important concept of software building and programming, don’t worry. I will discuss it in great detail later. For now, know that the DI mechanism is a way to add a class instance to another class instance using a class constructor. Let’s consider a real-life example. Take a look at the following code first; then I will explain how IoC and DI work together in Laravel:

2『上面的代码敲一遍并且好好研究。』

With the previous code, you will get output like this: We have received your payment, you have paid through Stripe.

The key concept of DI is that the abstraction (here, PaymentInterface) never worries about the details. The lower-level implementation modules (here, the PaymentGateway class) handle the details. In this case, it uses Stripe as a payment gateway. And the PaymentNotification class uses the abstraction to get those details. It also does not bother about what type of payment gateway has been used.

Now if the client changes the payment gateway from Stripe to PayPal, you don’t have to hard-code it into the class that uses the payment gateway. In the implementation, you will change it, and any class into which you inject the implementation will reflect the change.

Depending on many classes is necessary. Managing those dependencies is not easy. Using an IoC container, you can manage the class dependencies as I have shown in the previous code. The IoC container resolves the dependencies easily. In fact, the IoC container is a central piece of the Laravel framework. This container can build complex objects for you. Note dI is a form of IoC, which is why the container that manages this is called an IoC container.

Laravel ships with more than a dozen service providers, and they manage the IoC container bindings for the core Laravel framework components. The system loops through all the providers since you don’t use them all the time. Suppose you are using a form to send data; HTMLServiceProvider helps you with that. As shown in Figure 1-2, the kernel sends the request through the middleware to the controller, which I’ll cover in the next section. Figure 1-2. How the route and middleware request and response cycle work together.

If you open the config/app.php file, you will find these lines of code: This code is not shown here in its entirety, but this gives you an idea how the Laravel kernel system loops through those providers.

the Silex microframework, once maintained by Symfony, is now deprecated (at the time of writing this book), yet I encourage you to download it. You can study the similarities and differences compared to Laravel.

#### 1. What Is the MVC Pattern?

How do you successfully implement user interfaces with Laravel and follow the separation of concerns principle? The Model-View-Controller (MVC) architecture is the answer. And Laravel helps you do this quite easily (Figure 1-3). The workflow is simple: the user action reaches the controller from the view. The controller notifies the model. Accordingly, the model updates the controller. After that, the controller again updates the user.

That is why it is commonly used and a popular choice. The separation of concerns principle usually separates the application logic from the presentation layers in Laravel. Quite naturally, your application will become more flexible, modular, and reusable.

Let’s imagine a social networking application where you want to view a user’s page. You may click a link that looks like this: https://example.com/home/index/username 

Here you can imagine that home is the controller, index is the method, and in the username section you can even pass an ID. This is pretty simple, and it takes you to the user’s page. How you can make your app work through an MVC model like this?

As you might guess, you will get the user’s data from a database. The model defines what data your application should contain. So, it is model’s job to interact with the database. Now, a user’s database will be constantly evolving; changes will take place, and the user will make updates. If the state of this data changes, the model will usually notify the view. If different logic is needed to control the view, the model notifies the controller. Keeping the social media app in mind, the model would specify what data a list item should contain, such as first name, last name, location, and so on.

The role of the controller is critical. It contains the programming logic that updates the model and sometimes the view in response to input from the users of the app. In other social media apps, almost the same thing happens. The app could have input forms to allow you to post or edit or delete the data. The actions require the model to be updated, so the input is sent to the controller, which then acts upon the model, and the model then sends the updated data to the view. Now, this view can be manipulated in a different manner; you can use your layout template engine. In some cases, the controller can handle these tasks independently without needing to update the model.

Compared to the functions of the model and the controller, the workflow of the view consists of simple tasks. It will define only how the list is presented to another user. It will also receive the data from the model to display. Actually, you have seen this pattern before. The data model uses some kind of database, probably MySQL in the LAMP technology. In such cases, your controller’s code is written in PHP, and in your view part, you have used a combination of HTML and CSS.

#### 2. How the MVC Pattern Works

Imagine a portal, where your user interacts with the user interface in some way, such as by clicking a link or submitting a form. Now, the controller takes charge and handles the user input event from the user interface. Consequently, the controller notifies the model of the user action. Usually, the state of model changes. Suppose the controller updates the status of the user. It interacts with the model, and the model has no direct knowledge of the view. The model passes data objects to the controller, and then your controller generates the content with that dynamic data.

Because of its simple iterations and the principle of separation of concerns, the MVC pattern is often found in web application. Now, the MVC pattern can be interpreted in different ways: A section of people thinks that the actual processing part is handled by the model, and the controller handles only the input data. In such interpretations, the input-processing-output flow is represented by Controller-Model-View; here the controller interprets the mouse and keyboard inputs from the user.

Therefore, a controller is responsible for mapping end-user actions to application responses, whereas a model’s actions include activating business processes or changing the state of the model. The user’s interactions and model’s response decide how a controller will respond by selecting an appropriate view.

To summarize, an MVC pattern must have a minimum of three components, each of which performs its own responsibilities. Now many MVC frameworks add extra functionalities such as a data access object (DAO) to communicate with the relational database.

In normal circumstances, the data flow between each of these components carries out its designated tasks; however, it is up to you to decide how this data flow is to be implemented. With the MVC framework, you will learn that the data is pushed by the controller into the view. At the same time, the controller keeps manipulating the data in the model. Now the question is, who is doing the real processing? The model or controller? Does the controller play an intermediary role, and behind the scenes, the model actually pulls the strings? Or, is the controller the actual processing unit controlling the database manipulations and representation simultaneously?

1『controller 是个中转站。controller 最核心，它担任 processing 工作，一方面控制 model，同时也要控制 view。但数据的验证和操作是在 model 里进行。』

It does not matter as long as the data flows and the pattern works. In the Laravel applications in this book, you will implement MVC in a way so that the controller will do processing jobs, controlling the model and the view simultaneously.

When using the MVC framework, you must keep a separate DAO, and the model will handle the DAO as appropriate. Therefore, all SQL statements can be generated and executed in only one place. Data validation and manipulation can be applied in one place: the model. The controller will handle the request/response lifecycle, taking the input from the user interface and updating model accordingly. When the controller gets the green signal from the model, it sends the response to the view. The view is aware of only one thing: the display.

## 12. Working with APIs

What allows a third party to easily interact with a Laravel application’s data? The answer is an API. Usually the API is based on JSON and REST or is REST-like. You can easily work with JSON in your Laravel application, which gives Laravel a big advantage over other PHP frameworks. Without an API you cannot interact with any third-party software that is written in a different language and that works on different platforms. So, writing APIs is a common task that Laravel developers do in their jobs. Another advantage of Laravel is that its resource controllers are already structured around REST verbs and patterns. This makes Laravel developers’ lives much easier.

### 01. What Is REST?

Representational State Transfer (REST) is an architectural style for building APIs. There are some heated arguments over the definition of REST in the computer world. Please do not get overwhelmed by the definition or get caught in the crossfire. With Laravel, when I talk about REST-like APIs, I generally mean they have a few common characteristics; for example, they are structured around resources, and the APIs can be represented by simple URIs.

The URI http://localhost:8000/articles is a representation of all articles. The URI http:://localhost:8000/article/2 represents the second article. The representation of second article goes on just like normal URI representation.

The stateless condition of APIs makes a big difference. Between requests, there is no persistent session authentication, which means that each request needs to authenticate itself. Finally, the major advantage is it can return JSON, which the server understands. That is the reason why a third party can easily interact with a Laravel application. The main purpose of building an API is to enable another application to communicate with your application without any issues. The server knows XML and JSON; however, JSON is the most popular choice now. So, when you return your data in JSON, the ease of communication increases.

### 02. Creating an API

To create an API, you need controllers and models as usual. But, at the same time, you need to transform your models and model collections into JSON. For that, you want Laravel’s resource classes. They allow you to transform data into JSON. You can imagine your resource classes as a transformation layer that sits between your Eloquent models and the JSON responses.

1『用 laravel 的资源类把数据表单转化为 json 格式的数据，资源类是 models 和 json 数据库之间的转换层。』

Let’s start from scratch. The first step is to create a fresh Laravel project. Let’s say you want to create an Article API. So, you need a model, database table, and controller.

```
php artisan make:controller ArticleController --resource
```

Next, you need an Article model and a database table, as shown here:

```
php artisan make:model Article -m
```

The database table should have two fields, title and body, as shown here:

Before building an API, you should fill the Article table with some fake data with the help of a database seeder. To do this, you need to create ArticlesTableSeeder and ArticleFactory, as shown here:

```
//code 12.5 
$ php artisan make:seeder ArticlesTable
Seeder Seeder created successfully.

//code 12.6 
$ php artisan make:factory ArticleFactory 
Factory created successfully
```

Let’s change the code of both ArticlesTableSeeder and ArticleFactory, as shown here:

```
<?php

use App\Article;
use Illuminate\Database\Seeder;

class ArticlesTableSeeder extends Seeder
{
    /**
     * Run the database seeds.
     *
     * @return void
     */
    public function run()
    {
        factory(Article::class, 30)->create();
    }
}
```

This will create 30 articles. Next, you need to prepare your factory class to fill up the articles table, as shown here:

```
<?php

/** @var \Illuminate\Database\Eloquent\Factory $factory */

use App\Model;
use Faker\Generator as Faker;

$factory->define(Model::class, function (Faker $faker) {
    return [
        'title' => $faker->text(50),
        'body' => $faker->text(300)
    ];
});
```

The title property will have a maximum of 50 characters, and for the body you will be content with 300 characters for demonstration purposes. Let’s fill the database table, as shown here:

```
$ php artisan db:seed 
Seeding: ArticlesTableSeeder 
Database seeding completed successfully.
```

After the completion of database seeding, you will generate the resource class. To do that, you will use the make:resource Artisan command.

```
//code 12.10 
$ php artisan make:resource Article 
Resource created successfully.
```

These resources are created to transform the individual models. You may want to generate resources that are responsible for transforming collections of models. This allows you to include links and other meta information in your response.

To create a resource collection, either you can use the --collection flag or you can include the word Collection in the resource name. The word Collection will indicate to Laravel that it should create a collection resource. Collection resources extend the Illuminate\Http\Resources\Json\ResourceCollection class. The relevant artisan command will look like this:

```
//code 12.13 
$ php artisan make:resource Article --collection 
$ php artisan make:resource ArticleCollection
```

1『就用第二条命令。』

Later in this chapter I will discuss collections and show how they work. So, you have created a resource called Article. You can find it in the app/Http/ Resources directory of your application. Resources extend the Illuminate\Http\ Resources\Json\JsonResource class.


```
<?php

namespace App\Http\Resources;

use Illuminate\Http\Resources\Json\JsonResource;

class Article extends JsonResource
{
    /**
     * Transform the resource into an array.
     *
     * @param  \Illuminate\Http\Request  $request
     * @return array
     */
    public function toArray($request)
    {
        return parent::toArray($request);
    }
}
```

As you can see in the previous code, every resource class defines a toArray method, which returns the array of attributes that should be converted to JSON when sending the response. Laravel takes care of that in the background.

You are not ready yet. You need to register your API routes in the routes/api.php file, like this:

```
use Illuminate\Http\Request;
use Illuminate\Routing\Route;

Route::middleware('auth:api')->get('/user', function (Request $request) {
    return $request->user();
});

// list articles
Route::get('articles', 'ArticleController@index');
// list single article
Route::get('article/{id}', 'ArticleController@show');
// create new article
Route::post('article', 'ArticleController@store');
// update articles
Route::put('article', 'ArticleController@store');
// delete articles
Route::delete('article/{id}', 'ArticleController@destory');
```

You see the URI, method, and action parts of your routes. If you want a full list, you can issue this artisan command in your terminal:

    $ php artisan route:list

1『上面的命令经常用，要牢记。』

Now you can see the full route list (Figure 12-1).

1『

报错：

```
 ErrorException  : Non-static method Illuminate\Routing\Route::middleware() should not be called statically
```

把「use Illuminate\Routing\Route;」注释掉即可，但本质原因目前不理解。（2020-03-14）

』

After starting the local server, you can open Postman to get the response (Figure 12-2). Postman is a tool that can send requests to an API and show you the response. In other words, it is a fancy version of cURL. You can get the same output in your regular web browser also. The URL is http:// localhost:8000/api/articles. See Figure 12-3.


1『

无法显示，查找原因后发现「ArticleFactory.php」有误，之前没按书里的修改。

```
use App\Model;
use Faker\Generator as Faker;

$factory->define(Model::class, function (Faker $faker) {
    return [
        'title' => $faker->text(50),
        'body' => $faker->text(300)
    ];
});
```

```
use Faker\Generator as Faker;

$factory->define(App\Article::class, function (Faker $faker) {
    return [
        'title' => $faker->text(50),
        'body' => $faker->text(300)
    ];
});

```

api 在软件 postman 和浏览器里还是显示不出来。此问题待解决。（2020-03-14）

』

Let’s take a look at the ArticleController index method, as shown here:

For demonstration purposes, I have shown only two methods here: index and show. Since I have used the paginate() method, each page shows you 15 articles. Figure 12-4 shows the second page.

The URL is http://localhost:8000/api/articles?page=2.

Now you may not want to give your application user every output. You may want to omit created\_at and updated\_at. Laravel allows you to customize the JSON output. In that case, you can return the selected records like this:

```
//code 12.17
//app/Http/Resources/Article.php
<?php

namespace App\Http\Resources;

use Illuminate\Http\Resources\Json\JsonResource;

class Article extends JsonResource
{
    /**
     * Transform the resource into an array.
     *
     * @param  \Illuminate\Http\Request  $request
     * @return array
     */
    public function toArray($request)
    {  
        return [
            'id' => $this->id,
            'title' => $this->title,
            'body' => $this->body
        ];
    }
}
```

So, you are returning only id, title, and body and giving a customized look (Figure 12-5).

You can use the show method to have one article display at a time, as shown in Figure 12-6.

Notice that for the customized version, you access the model properties directly from the \$this variable.

How does this work?

This is because a resource class is able to automatically proxy properties and methods, and it accesses the underlying model. Once the resource is defined, it may be returned from a route or controller, as in the ArticleController show method in the example.

```
//code 12.18
public function show($id)
    {
        //get article
        $article = Article::findOrFail($id);
        
        //returning single article as a resource
        return new ArticleResource($article);
    }
```

Here you are returning a single article as a resource. Suppose, in case of the User resource, you return a new UserResource like this:

```
//code 12.19
use App\User;
    use App\Http\Resources\User as UserResource;
    Route::get('/user', function () {
        return new UserResource(User::find(1));
    });
```

In the customized version, you can add some more elements with the help of the with method in app/Http/Resources/Article.php.

The changed code looks like this:


The JSON response changes to the screen shown in Figure 12-7 in Postman.

Next, you will see how API collection works. Let’s first create a UserCollection class.

```
//code 12.21
$ php artisan make:resource UserCollection
Resource collection created successfully.
```

I have added a few dummy users to the application. In the resource UserCollection, when you have this line of code:

```
//code 12.22
//app/Http/Resources/UserCollection.php
public function toArray($request)
    {
        return parent::toArray($request);
    }
```

you get this JSON response output:

Once the resource collection class has been generated, you can easily define any metadata that should be included with the response. To do that, you need to change the code of UserCollection in this way:

```
//code 12.23
//app/Http/Resources/UserCollection.php
    public function toArray($request)
        {
            return [
                'data' => $this->collection,
                'links' => [
                    'author_url' => 'https://sanjib.site',
                ],
            ];
        }
```

Now you have added extra metadata, and in the output it has been included at the bottom of your JSON response.

In your browser display, it also has been included at the bottom (Figure 12-9). To get all those new UserCollection JSON responses, you can register your route in this way:

```
//code 12.24
//routes/api.php
use App\User;
use App\Http\Resources\UserCollection;

Route::get('/users', function () {
      return new UserCollection(User::all());
});
```
















