# 01 Introduction to Laravel

This book is intended for intermediate-level PHP developers. Advanced users may also find this book helpful to keep on hand as a quick reference. Either way, you should have a good grasp of object-oriented PHP7 programming knowledge to understand the examples.

## 01. Laravel’s Flexibility

Laravel is a highly flexible PHP framework, and it makes complicated tasks easier to do.

Laravel provides powerful tools for making large, robust applications; however, to accomplish that, you need to understand a few key concepts such as how to use IoC containers or service containers to manage class dependencies. The expressive migration system is another concept that you will learn about in detail in Chapter 5.

Behind the scenes, Laravel uses many design patterns, and as you progress through this book, you will find that from the beginning Laravel helps you code in a loosely coupled environment. The framework focuses on designing classes to have a single responsibility, avoiding hard-coding in the higher-level modules, and allowing IoC containers to have abstractions that depend on the details. Higher-level modules do not depend on the lower-level modules, making coding a joyful experience.

As you progress through the book, you will find plenty of examples supporting this general paradigm. Because of this flexibility, Laravel has become one of the most popular frameworks today.

If you are not convinced, I will also say that without the help of a framework like Laravel, you would need to write thousands of lines of code that would probably start out by routing HTTP requests. In Laravel, it is simple and straightforward to route an HTTP request. This is defined in the routes/web.php file, as shown here:

```
//code 1.1 
//Laravel Route Example 
Route::get('/', function () { return view('welcome'); });
```

This defines the URL for an application. While defining the URL, Laravel also helps you return a Blade template page that you can use to nicely format and design your data. You will learn about this in detail in Chapter 3.

In any other framework, you won’t know how complicated the requests will be and what your responses will be. So, you’ll need response libraries to assist you in your framework, which could easily be a humongous task to implement.

Laravel can handle your request/response lifecycle quite easily. The complexity of requests does not matter here. Laravel’s HTTP middleware consists of little HTTP layers that surround your application. So, every request must pass through these HTTP middleware layers before hitting your application. They can intercept and interrupt the HTTP request/response lifecycle, so you can stay calm about all the security matters that are most important. From the beginning, you have a well-guarded application interface when you install Laravel. You can think the first layer as the authentication layer, whereas the middleware tests whether the user is authenticated. If the user is not authenticated, the user is sent back to the login page. If the user passes the test, the user must face the second layer, which could consist of CSRF token validation. The process goes on like this, and the most common use cases of the Laravel middleware that protects your application are authentication, CSRF token validation, maintenance mode, and so on. When your application is in maintenance mode, a custom view is displayed for all requests.

For any experienced developer, it takes many months to build well-structured containers that can handle such complex requests and at the same time terminate the response lifecycle at the proper time.

Frameworks help you achieve this goal in a short period of time. Finding components is much easier; once you understand how routing works in Laravel, you can apply it quite easily for the rest of your working life.

In addition, Laravel’s installation process is simple. With the help of the Composer dependency manager, you can manage it quite easily. In Chapter 2, I will discuss it in detail.

As a developer, you are here to solve multiple problems, and a framework like Laravel, in most cases, addresses those problems in an elegant way. So, you don’t have to write tons of libraries and worry about version changes. The makers of Laravel have already thought about that.

Laravel’s author, Taylor Otwell, summarizes the flexible features of Laravel as follows (from a PHPWorld conference in 2014):

• Aim for simplicity

• Minimal configuration

• Terse, memorable, expressive syntax

• Powerful infrastructure for modern PHP

• Great for beginners and advanced developers

• Embraces the PHP community

## 02. How Laravel Works

Laravel follows the MVC pattern of logic. But it has many more features that have enhanced the pattern’s features, elevating them to a new level.

Laravel ships with a dependency injection (DI) mechanism by default (Figure 1-1).

![](./res/2020001.png)

Figure 1-1. How DI works with an IoC container

If you are new to this important concept of software building and programming, don’t worry. I will discuss it in great detail later. For now, know that the DI mechanism is a way to add a class instance to another class instance using a class constructor.

Let’s consider a real-life example. Take a look at the following code first; then I will explain how IoC and DI work together in Laravel:

```

```

With the previous code, you will get output like this:

We have received your payment, you have paid through Stripe.

The key concept of DI is that the abstraction (here, PaymentInterface) never worries about the details. The lower-level implementation modules (here, the PaymentGateway class) handle the details. In this case, it uses Stripe as a payment gateway. And the PaymentNotification class uses the abstraction to get those details. It also does not bother about what type of payment gateway has been used.

Now if the client changes the payment gateway from Stripe to PayPal, you don’t have to hard-code it into the class that uses the payment gateway. In the implementation, you will change it, and any class into which you inject the implementation will reflect the change.

Depending on many classes is necessary. Managing those dependencies is not easy.

Using an IoC container, you can manage the class dependencies as I have shown in the previous code. The IoC container resolves the dependencies easily. In fact, the IoC container is a central piece of the Laravel framework. This container can build complex objects for you.

Note dI is a form of IoC, which is why the container that manages this is called an IoC container.

Laravel ships with more than a dozen service providers, and they manage the IoC container bindings for the core Laravel framework components.

The system loops through all the providers since you don’t use them all the time. Suppose you are using a form to send data; HTMLServiceProvider helps you with that. As shown in Figure 1-2, the kernel sends the request through the middleware to the controller, which I’ll cover in the next section.

![](./res/2020002.png)

Figure 1-2. How the route and middleware request and response cycle work together

If you open the config/app.php file, you will find these lines of code:

This code is not shown here in its entirety, but this gives you an idea how the Laravel kernel system loops through those providers.

the Silex microframework, once maintained by Symfony, is now deprecated (at the time of writing this book), yet I encourage you to download it. You can study the similarities and differences compared to Laravel.

### 1. What Is the MVC Pattern?

How do you successfully implement user interfaces with Laravel and follow the separation of concerns principle? The Model-View-Controller (MVC) architecture is the answer. And Laravel helps you do this quite easily (Figure 1-3).

The workflow is simple: the user action reaches the controller from the view. The controller notifies the model. Accordingly, the model updates the controller. After that, the controller again updates the user.

![](./res/2020003.png)

Figure 1-3. How the MVC workflow works

That is why it is commonly used and a popular choice. The separation of concerns principle usually separates the application logic from the presentation layers in Laravel. Quite naturally, your application will become more flexible, modular, and reusable.

Let’s imagine a social networking application where you want to view a user’s page. You may click a link that looks like this:

https://example.com/home/index/username 

Here you can imagine that home is the controller, index is the method, and in the username section you can even pass an ID. This is pretty simple, and it takes you to the user’s page. How you can make your app work through an MVC model like this?

As you might guess, you will get the user’s data from a database. The model defines what data your application should contain. So, it is model’s job to interact with the database. Now, a user’s database will be constantly evolving; changes will take place, and the user will make updates. If the state of this data changes, the model will usually notify the view. If different logic is needed to control the view, the model notifies the controller. 

Keeping the social media app in mind, the model would specify what data a list item should contain, such as first name, last name, location, and so on.

The role of the controller is critical. It contains the programming logic that updates the model and sometimes the view in response to input from the users of the app. In other social media apps, almost the same thing happens. The app could have input forms to allow you to post or edit or delete the data. The actions require the model to be updated, so the input is sent to the controller, which then acts upon the model, and the model then sends the updated data to the view. Now, this view can be manipulated in a different manner; you can use your layout template engine. In some cases, the controller can handle these tasks independently without needing to update the model.

Compared to the functions of the model and the controller, the workflow of the view consists of simple tasks. It will define only how the list is presented to another user. It will also receive the data from the model to display.

Actually, you have seen this pattern before. The data model uses some kind of database, probably MySQL in the LAMP technology. In such cases, your controller’s code is written in PHP, and in your view part, you have used a combination of HTML and CSS.

### 2. How the MVC Pattern Works

Imagine a portal, where your user interacts with the user interface in some way, such as by clicking a link or submitting a form. Now, the controller takes charge and handles the user input event from the user interface. Consequently, the controller notifies the model of the user action. Usually, the state of model changes. Suppose the controller updates the status of the user. It interacts with the model, and the model has no direct knowledge of the view. The model passes data objects to the controller, and then your controller generates the content with that dynamic data.

Because of its simple iterations and the principle of separation of concerns, the MVC pattern is often found in web application.

Now, the MVC pattern can be interpreted in different ways: A section of people thinks that the actual processing part is handled by the model, and the controller handles only the input data. In such interpretations, the input-processing-output flow is represented by Controller-Model-View; here the controller interprets the mouse and keyboard inputs from the user.

Therefore, a controller is responsible for mapping end-user actions to application responses, whereas a model’s actions include activating business processes or changing the state of the model. The user’s interactions and model’s response decide how a controller will respond by selecting an appropriate view.

To summarize, an MVC pattern must have a minimum of three components, each of which performs its own responsibilities. Now many MVC frameworks add extra functionalities such as a data access object (DAO) to communicate with the relational database.

In normal circumstances, the data flow between each of these components carries out its designated tasks; however, it is up to you to decide how this data flow is to be implemented. With the MVC framework, you will learn that the data is pushed by the controller into the view. At the same time, the controller keeps manipulating the data in the model. Now the question is, who is doing the real processing? The model or controller? Does the controller play an intermediary role, and behind the scenes, the model actually pulls the strings? Or, is the controller the actual processing unit controlling the database manipulations and representation simultaneously?

It does not matter as long as the data flows and the pattern works. In the Laravel applications in this book, you will implement MVC in a way so that the controller will do processing jobs, controlling the model and the view simultaneously.

When using the MVC framework, you must keep a separate DAO, and the model will handle the DAO as appropriate. Therefore, all SQL statements can be generated and executed in only one place. Data validation and manipulation can be applied in one place: the model. The controller will handle the request/response lifecycle, taking the input from the user interface and updating model accordingly. When the controller gets the green signal from the model, it sends the response to the view. The view is aware of only one thing: the display.