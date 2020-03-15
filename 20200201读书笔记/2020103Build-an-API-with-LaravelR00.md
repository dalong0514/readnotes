## 记忆时间

## 卡片

### 0101. 反常识卡——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

#### 01. 常识

#### 02. 反常识

#### 03. 知识来源

比如提出者，如何演化成型的；书或专栏具体出现的地方。

#### 04. 例子

### 0201. 术语卡——CRUD

As mentioned earlier, HTTP verbs play a significant role in the intention of a request. The HTTP verb tells the server about how we, on the client side, intend to handle our data. How to handle data is often looked at from a CRUD perspective, which stands for: Create, Read, Update, Delete. As an example, imagine an application for a bookstore. The CRUD part here will be responsible for: Adding, Listing, Updating or Removing books from the bookstore.

### 0202. 术语卡——conventions

You see, it’s not the development of the API on the backend that takes time and causes pain. The pain is mostly felt when you have to work with the API on the frontend, or even worse when other people or companies are working with your API. Without strict conventions, you not only have to write documentation that shows what your API can do, but you also end up teaching how to use the API. This is where following a specification like the JSON:API specification shows its worth. How to use it is already documented and as long as you follow the specification, anybody who knows how to work with the JSON:API specification, knows how to work with your API. Of course, they won’t know what your API can do — you will still have to tell them that — but how to communicate with your server through your API, will never be a problem for them.

Even better, when following the conventions of the JSON:API specification, you have a strict protocol that never changes from application to application. This means that you can extract the whole client-server communication part of your frontend application and reuse it from application to application. You won’t have to write the same tedious boilerplate code over and over again, and you can focus on building the functionality of your frontend app instead. The JSON:API specification even lists available implementations, which includes implementations made for a lot of languages like Javascript as well as frameworks like VueJS and React.

### 0203. 术语卡——

### 0301. 人名卡——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

维基百科链接：有的话。

#### 01. 基本信息

用一句话描述你对这个大牛的印象。

#### 02. 贡献及著作

### 0401. 金句卡——anybody who knows how to work with the JSON:API specification, knows how to work with your API

## 模板

### 1. 逻辑脉络

用自己的话总结主题，梳理逻辑脉络，也就是这本书整个地图里这一章所在的节点。

### 2. 摘录及评论

## 总体

### Prerequisites

Therefore, you will have to have a basic understanding of Laravel to keep up. We certainly recommend that you have tried writing an application in the framework before reading, and that you know what we talk about when we mention: Client, Server, Request, Response, Routes, Controllers, Eloquent or Models, Migrations, Factories, Authentication, Authorization, and Validation.

We will also be using Laravel Collections heavily, so an understanding of these – especially the map, filter, each, flatten, flatMap, merge, pluck, sort, unique and values methods is necessary.

Also, we expect that you know the basics around PHP, especially the basics around PSR-4 namespacing, how to import classes from other namespaces and so forth. In many IDE’s and editors, all this functionality can be installed with a simple plugin or will already built into the IDE or editor.

## 01. Introduction

### 1. 逻辑脉络

api 如同餐馆里的菜单。REST 里的 HTTP verbs 继承于 HTTP method，也就是那些常规的 status codes。

### 2. 摘录及评论

We have looked at what an API is and how it can be seen as a menu at a restaurant, where users can see what you can order from the backend. We have taken a look at REST, how it builds on top of HTTP and thereby inherits all the abilities that HTTP already has. We have looked at HTTP verbs and how they play a significant role in the intention of a request. We have looked at the more common status codes and the ones we will cover in this book, how these are used to respond back to the client about how the request has been fulfilled or not. With this knowledge in mind, let’s dig a little deeper into APIs and how to plan your work before you sit down and write your API.

Welcome to Build an API with Laravel, where we, as the title reveals, will take a look at how to build an API using Laravel. First, we will be looking at an API from a more theoretical point of view. Don’t worry, we won’t bore you to death with small details, but rather give you a fundamental understanding, which we can build on from there. We will be looking at why we are using PHP and Laravel, and what makes it a great candidate for writing APIs. We will go through the JSON:API Specification and learn about the protocols and conventions, and how these can help us build a more consistent API that is easier for us to consume. We will look at how to plan an API, what to be aware of and what decisions you’ll have to make, depending on whether your API is public or private.

Next, we will be looking at authentication, where we take a closer look at Laravel Passport and OAuth 2, which Laravel Passport is built upon. Here, we will go over the different grant types and what they are used for, to give you a clearer image of what you should choose for your applications.

Then, we’ll get to the heart of the matter, where we will be writing the actual API. We will start out with a rather simple case to give you a better picture of how to apply the knowledge you’ll get from this book and to have a common ground to build on.

We will be looking at Test-driven Development, especially the parts that are relevant to API development, and through this use the great testing tools from Laravel to test our API and also get an excellent workflow on top of it. We won’t go into every detail about Test-driven Development, since it’s a huge topic in itself and that’s not what this book is about. We will, however, use Test-driven Development to show you how we can drive out our implementations, how we can refactor code to not having to repeat the same code over and over again, and get code that is easier to reuse.

Lastly, we will be looking at authorization and how you can authorize different parts of your API. We will end the book with a bonus chapter, where we will go over the client side of things and show you how you can consume your API using client implementations, which is a huge advantage to using a set of strict protocols which the JSON:API specification will give us.

We hope you will enjoy reading this book as much as we have enjoyed writing it. We find that knowing how to build APIs has helped us a lot during our projects, since you can separate the concerns between frontend and backend, and thereby adapt to changes or new platforms, which might consume your API much easier. Let’s get to it!

1『会写好的 api 太重要了，好的 api 它可以很好分割开前端和后端。』

### 01. What is an API?

To best describe what an API is, let’s imagine that our application or service is like a restaurant. The frontend of the application is where you sit at the table and eat, and the backend is the kitchen, where they prepare food for you. Here, an API plays the role of the menu, where you can pick what you want the kitchen to cook for you. In programming terms, an API makes it possible for a frontend developer to request a specific task or resource from the backend.

1『api 如同菜单这个隐喻真棒。进了餐馆顾客只需看菜单就可以知道后厨可以提供哪些服务了。』

If you look at a menu, you might notice that it consists of a finite predetermined set of dishes: a collection of dishes that the kitchen knows how to cook and prepare for you. The same goes for an API, but instead of having dishes to choose from, you instead select between endpoints. Through endpoints, we can order our backend to prepare and send back some data for us. It could be a list of books for a bookstore or the latest comments for a blog post, depending on the service or application that serves a solution to a problem. Like a menu being divided into starters, main course and desserts, an API is divided into resources. We’ll be touching upon resources later — right now you just have to know that they exist.

1「又见 resource 资源的概念，api 被分为很多的资源。」

Much like a menu can have various designs, the same goes for APIs and the architecture behind. At the time of writing this book, there are many types of API architectures. Some architectures like SOAP are not used that much more, while others like GraphQL are new and exciting. Then there is the common technology like REST, which we are going to cover in this book.

1『api 也有很多框架，或者类似于模式，目前推荐 REST。』

### 02. What is REST?

REST stands for Representational State Transfer and is an architectural style used for communication between a server and a client. REST uses the HTTP or Hypertext Transfer Protocol, as a base for the communication. We already use HTTP for transferring HTML and other media from servers to our clients. This is, for instance, what happens when you visit a website, so by building on an already familiar technology, REST is easily adaptable.

REST sends data using either XML or JSON. Both of these languages are meant for transferring data, but also meant to be readable by humans, which also makes error tracking in REST a lot easier. REST is platform and language independent, as long as you adapt to HTTP, you adapt to REST. Already established features of HTTP, like SSL encryption, make it possible to transfer encrypted data across from server to client, so there are a lot of advantages we get for free.

A disadvantage is that REST is not stateful, meaning that the state is not carried along from one request to the other. Therefore, you always have to send some kind of context to the server for it to know what to deliver to you. This limitation stems from HTTP itself, so this is most likely something you are already familiar with.

Like HTTP, REST works through requests, where you “pull” data from the server. There is no way of “pushing” data through REST, although it is possible for the server to do server pushing, using the HTTP 2 standard, but even that is only initiated by a request.

Since REST relies so much on HTTP, there are some things we have to examine to understand REST and the way communication takes place. For instance, HTTP methods, also called verbs, play a significant role in the intention for a REST request, as much as the HTTP Status code plays a significant role in the answers. These are the HTTP building blocks that make up most of the base of REST communication. Let’s take a closer look at HTTP Verbs.

### 03. HTTP verbs

As mentioned earlier, HTTP verbs play a significant role in the intention of a request. The HTTP verb tells the server about how we, on the client side, intend to handle our data. How to handle data is often looked at from a CRUD perspective, which stands for: Create, Read, Update, Delete. As an example, imagine an application for a bookstore. The CRUD part here will be responsible for: Adding, Listing, Updating or Removing books from the bookstore.

2『CRUD，做一张术语卡片。』

GET. A request with a GET verb is for reading data. That’s the only thing this verb tells our server. The API endpoint will determine whether we are reading a collection of resources or just a single resource. We will go much further into detail about collections and resources later in this book, but for now, to put it into context, let’s revisit the bookstore. Here, the resource is a book and a collection could be a stack of books.

POST. A request with a POST verb is for creating a resource. In other words, we use POST whenever we want to transfer new data from the client to the server.

PUT and PATCH. Both the PUT and the PATCH request is for updating or modifying data, but the way they are intended is a bit different. PUT verbs are used when all data for a resource is completely replaced with the data given by the client. PATCH verbs are used for a partial update or modification, instead of replacing everything in the resource. Whether to use PUT or PATCH is all up to you and the needs of your application. The differences might be subtle, but they are there to make it clear to the client making the request, what is actually happening.

2XX as Success. The 2XX range are statuses that tell the client a request was successful. You would think that only one status was needed here, but in some cases where, for example, you create something, it would be nice to know if the resource has been created. Let’s take a look at a few of the statuses we’ll be using later.

200 OK. The 200 status code, which tells the client that the entire request was successful, is the most common. You might think that it’s sufficient to use this one status and then add more details about the request in the response payload, but remember that these statuses were created for HTTP and to solve a problem. Since REST is built upon HTTP, and HTTP uses its status codes to communicate how a request has been fulfilled, why reinvent the wheel? Better to use what is already a well-known standard. Which leads us to the next status.

201 Created. This status code tells the client that one or more resources have been created. As mentioned in the 200 status code, this status code makes it possible to only look at the 201 status, and we know, without having to look at the response payload, that the resource was created and we can move on much faster.

204 No Content. This status code tells the client that the request has been fulfilled, but also that there is no payload in the response. To give an example, this could be used when updating a resource. Here you don’t really need any data back since you are telling the backend what to update and therefore know what to expect.

3XX as Redirection. The 3XX range are all statuses that tell the client about redirections. Most applications are continually being updated, and it is not uncommon that endpoints are being updated or removed. Then what do you do if someone out there is using an old endpoint where a sudden change could break their entire site or application? Here, redirects play an important role.

301 Moved Permanently. The 301 status code tells the client that an endpoint has been moved and should give a new location in its payload for the client to save for future reference. A thing to note here is that the 301 status code makes it possible to change the HTTP verb for the request. This example is a little silly, but let’s imagine we have the following endpoint:

    POST: /v1/book

We know you wouldn’t use POST for this, but imagine that this endpoint returns a collection of books. With the 301 status code, you are allowed to change the HTTP verb when redirecting to the new endpoint, which then could be like this:

    GET: /v2/book

This is not something we recommend doing, unless you are using a wrong HTTP verb beforehand, where a change makes sense. Let’s take a look at a status code that allows you to redirect, but does not allow you to change the HTTP verb. A HTTP verb that can ensure the redirect is more consistent than in this example.

307 Temporary Redirect. The 307 status code is used for a temporary redirect. Here, the server should give a new location in its payload, for the client to redirect to. The client will not save any information about the redirect and will merely follow the location given by the server and gladly hit the old endpoint time after time, since the redirect is only temporary. A thing to note, as mentioned in the 301 status code, is that the 307 status code does not let you change the HTTP verb in the redirect. When redirecting the user, the endpoint to which you are redirected must match the HTTP verb from which you were redirected.

308 Permanent Redirect. The 308 status code is used for a permanent redirect, much like the 301 redirects. The only difference is that, like 307, it does not allow for the HTTP verb to change from the original endpoint to the endpoint redirected to.

4XX as Client errors. The 4XX range are all statuses that deal with client error, which could be a request that the client is not authenticated to do or even a request to a misspelled endpoint, which the server cannot fulfill.

400 Bad Request. The 400, much like the 200, is a broad status code. All it does is tell the client that the server could not or would not process the request. It does not specify any reasons, and the client would have to look at the payload for further information.

2『去查 payload 的概念。』

401 Unauthorized. The 401 status tells the client that the request could not be fulfilled due to lacking authentication credentials.

403 Forbidden. The 403 status tells the client that the request could not be fulfilled due to lacking authorization. For example, this status code could be sent back if one user tries to access or update another user’s data. The user might be authenticated to access the endpoint, but not have authorization to access the data.

3『

出现很多次的，endpoint 的概念。

http://www.ttdev.com/SimpleService 这个 webservice 全名就是所谓的 endpoint。注释：http://ttdev.com/ss 就是 namespace, 并无特别意义，只需要 global 唯一。namespace 不用于 endpoint，endpoint 是一个存在的 location，而namespace 就是一个表示 unique ID。可以任意移动 webservice 的位置，改变 Server，也就是说变更 endpoint；但是方法（operation）的 namespace 不可以改变。不同点在哪？ 最大不同就是 RPC 不能通过 Schema 来校验，而 document  类型是可以的。因此 document 类型 webservice 成为主流 。WS-I (web services interoperability organization) 组织规定只使用 document类型 web services。

An endpoint is the 'connection point' of a service, tool, or application accessed over a network. In the world of software, any software application that is running and "listening" for connections uses an endpoint as the "front door." When you want to connect to the application/service/tool to exchange data you connect to its endpoint.

Simply put, an endpoint is one end of a communication channel. When an API interacts with another system, the touchpoints of this communication are considered endpoints. For APIs, an endpoint can include a URL of a server or service. Each endpoint is the location from which APIs can access the resources they need to carry out their function.

APIs work using ‘requests’ and ‘responses.’ When an API requests information from a web application or web server, it will receive a response. The place that APIs send requests and where the resource lives, is called an endpoint.

1「目前的理解，endpoint 是 resource 的存放点，即前端里请求资源时填写的 api 地址。」

endpoint 在 RESTful 风格下通常看起来是这样：

```
/this-is-an-endpoint
/another/endpoint
/some/other/endpoint 
/login
/accounts
/cart/items
```

放在某个域名下：

```
https://example.com/this-is-an-endpoint
https://example.com/another/endpoint
https://example.com/some/other/endpoint
https://example.com/login
https://example.com/accounts
https://example.com/cart/items
```

http 或者 https 都可以，这里只是用 http 举例。HTTP method 不同，endpoint 看起来也不一样,  比如说：

```
GET /item/{id}
PUT /item/{id}
```

这是两个不同的 endpoints, 一个是用于 CRUD 的 R (Retrieving), 一个是用于 CRUD 的 U (updating)。

』

404 Not Found. The 404 status tells the client that the requested resource could not be found. This is a pretty common status that most people, even non-developers, have been met by.

405 Method Not Allowed. As we have explained earlier, HTTP methods are also called HTTP verbs in REST. The 405 status tells the client that the request has been made with an HTTP verb that is not allowed. This could, for instance, be a request made using a GET verb to an endpoint that only supports the POST verb. In this case, a 405 status should be sent to the client.

1『HTTP methods 对应于 REST 里的 HTTP verbs，因为 REST 不造轮子。』

3『资源层如同数据（数据结构），HTTP verbs 如同操作这些数据结构的算法。可以去看看「2020017郑晔的10倍程序员工作法R00」里有关 MVC 分层的思考。』

422 Unprocessable Entity. The official RFC4918 states that this status is to be used when the server understands the content of the request and the syntax of the request is correct, but was unable to process the request. An RFC stands for Request For Comments, which can be viewed as the rules for standardizing the internet. The number references the document in which the request has been documented. In Laravel, the 422 status code is used for validation errors when using REST and JSON. The JSON:API documentation says that this status is to be used when creating or updating a resource where an attribute is invalid. Based on all these examples, we can safely say that the 422 status code tells the client about invalid data sent in the request.

5XX as Server errors. The 5XX range are all statuses that deal with the server, where it is aware that an error has occurred or might otherwise be unable to handle the request.

500 Internal Server Error. This status is used as a generic error message given when it is not possible to provide a more specific status code.

501 Not Implemented. This status is used when the server does not know how to fulfill the request, but implies that it might be available in the future. This could be a new feature that is under development.

502 Bad Gateway. This status is used when the server is acting as a gateway and has received an invalid response. If you have ever used nginx, you have probably seen this status code. Since nginx sits as the man in the middle and intercepts all incoming requests and then proxies these forwards, if nginx receives an error from the party it tries to proxy to, it gives you a 502 status code.

503 Service Unavailable. This status code is used if the server is down for maintenance.

504 Gateway Timeout. This status is used when the server is acting as a gateway and did not receive a response within a given period. As with the 502 status code, this is something you see with nginx, where you configure a timeout limit, in which a request should be fulfilled or else a timeout will be sent back to the client. This is used to prevent the server from working forever on a job that might not be solvable. This could, for instance, be an error in PHP, where something loops forever. We don’t want our users to wait forever and they want their data, so let’s use a time limit and move on.

## 02. The JSON:API specification

### 1. 逻辑脉络

JSON:API specification 在 api 里最重要了，即以 JSON 数据结构编写 API 的规范（a specification for building APIs in JSON）。JSON:API specification 还有一个视角：endpoint 的命名约定。

### 2. 摘录及评论

We’re at the end of this chapter and we have covered quite a lot. Not only did we introduce the case of Anna’s Bookstore, which we will use as a common ground to easily put things into perspective in the rest of this book. We also covered naming conventions for API endpoints, the JSON:API specification, and especially all of the important rules that are specified. We looked at how to structure our data or documents for both requests and responses, how to structure our primary data of a document, both when handling single resources and collections of resources.

Then we covered resource objects and which members we must include like id and type, but also learned how to name our member names for a more consistent structure when adding attributes to a resources object. We then moved on to relationships and how to define relationship links that make it possible to access both relationships themselves and related resources objects. We covered how to define resource identifier objects and how these could be used together with the includes top-level member, to contain related resources in a response in order to save HTTP requests.

Afterward, it was time to look at how to use our new knowledge about data structures to properly communicate between client and servers. We covered how to get resources, and how we could use request documents to fetch the exact resource or collections of resources needed. We looked at how we could sort and paginate resource collections, through both query parameters and a links top-level member. 

We then looked at how to create resources and how to structure our request documents, how we could create a relationship through request documents for resource creation, but also how relationship links could be used to create relationships, using relationship linkages instead of resource objects.

We covered how to update resources and relationships using the same principles when creating these, and how an update to a relationship would always remove the current relationship to a resource and then update with the newly given resource instead.

We then learned how to delete both resources and relationships. Finally, we concluded the chapter by looking at errors and how to convey these through error objects.

We now have a good set of conventions and a knowledge to use when we are building our APIs. We have rules that give us a more consistent way to not only structure data, but also how to communicate and what to communicate. Better yet, when implementing this specification, clients and consumers can use client implementations that will work right out of the box, and save them a lot of time when consuming your API, since these client implementations follow the same conventions and consistency. It’s now time to look at how to plan out an API. Even though we have a lot of knowledge about convention and rules to build a consistent API, we still need to plan out our project and documentation for our API.

Let’s have a look at the JSON:API specification — a specification for building APIs in JSON. A specification like this can help us build our API, following a set of rules that makes it easier for ourselves, and especially others, who will be consuming our API in the future. We will be looking at the specification and how it fits into the features Laravel offers, and how it can be a great tool to master, and make it possible for you to actually plan out your API with more confidence.

Firstly, we will be looking at a case for this book to have something to work from: a common ground which makes it a bit easier to put things into perspective. This way we can give examples when looking at the JSON:API specification with context and in later chapters show you how we go from planning all the way to implementation.

### 01. The case

By having a case that simulates a real life example, it might be easier for you to understand the concepts we will present to you and apply them into your own projects in the future. We all learn differently, but it is our experience that having a case and a context makes it easier to see the concepts applied and learn how to apply them yourself. So without further ado, let’s get into the case:

Anna’s Bookstore has existed since the early 90s where it opened as a small cornershop in the city. It isn’t a fancy place — the floor, bookshelves and furniture make it seem a bit like your grandma’s place, but it’s cosy, welcoming and the perfect combination of a bookstore and coffee shop, where you will feel right at home. Customers come back for Anna’s personality, which is reflected in every little thing in the store, and especially the selection of books. It’s not the selection of books you’ll find in every store; these are hand-picked by Anna herself. She’ll often offer customers a cup of coffee and discuss a book, or the work of an author, when there isn’t anything to do at the cash register. You can feel that both literature and people are her passion.

As the years go by, new stores start emerging and Anna gets a lot more competition, especially from modern bookstores, where people can find and buy books faster. This isn’t really Anna’s cup of tea, and to compete, she would have to change everything about her store. She’s beginning to think about closing the store, until a day when her nephew visits her. When they talk about the store, the nephew asks: “Why don’t you go online, so you can keep your store as it is and sell to people at home or in a hurry?”. Anna must admit that it is a good idea. Over the years, she has started to order books online herself and is quite pleased with the experience. The nephew then continues: “You don’t have to have a huge selection of the books, why not cater to a niche and sell a curated selection of books, like you do in your store now? You know people always praise you for having so many hidden gems.” Anna is convinced. This is something she can see herself in, she can still use her expertise, and people can still buy a bit of Anna’s personality in the selection of her books.

Other than being able to sell books and being able to keep stock of her books, Anna wants to be able to present these books through authors. Anna has a bunch of authors that she can vouch for, who always publish good work, a key part of her having so many hidden gems.

1『a key part of her having so many hidden gems. 是她的核心优势，可以理解为定制化、算法之类的。』

Sometimes, Anna finds books by reading comments that other people have left on the online bookstores. She loves the helpful tips people give in the comments and it reminds her of the discussions she has been a part of in her own bookstore. She would like something like this in her online bookstore as well.

There are a few things to take note of here. To some, the case might sound really simple and to others, it might seem daunting. But fear not, we won’t be building the entire solution for Anna. Instead, we will pick out parts of the online bookstore that makes sense in terms of an API, and not the entire purchase flow etc. Keep in mind that we have written this case to communicate the concepts about building an API, as easy as possible, and there is more than enough in the part about handling books and authors to do that.

Now that we know more about the case and what we need to build, we could go straight to the planning, but let’s hold that thought and take a closer look at the JSON:API specification, and learn a bit more about the protocols that will be the foundation of how we communicate with our API.

### 02. JSON:API specification

When developing software, there are a lot of decisions to make about how to design the software in the best way — from how to design your code to the application architecture, and all the way up to the visual representation of your application on screen. With APIs this isn’t any different. Up until 2013, where the first draft of the JSON:API specification was made, there weren’t any approaches to standardization of JSON API interactions.

Before adhering to the JSON:API, we at Wacky Studio even made our APIs in our own way, the way we thought was best. We drew inspiration from APIs of the services we used and made our decisions based on how they were implementing their APIs.

1『Wacky Studio 是作者他们的公司。』

That was a very bad idea because:

• They were also in a phase of learning how to write a good API for their services.

• None of them were following the same conventions.

• Most of them had an API design that meant you had to make a lot of requests for data.

The worst of it all was when we had to consume our own API on the frontend. Because of the lack of conventions, we had to constantly go back and forth to get the correct endpoints, to see what data each request should contain and to see what would be returned from the server. And every time we started a new project, we ended up writing all the code for communication with the server, again and again, because of inconsistency.

1『重视约定（conventions）是很重要的一条编程规则。anybody who knows how to work with the JSON:API specification, knows how to work with your API. 』

You see, it’s not the development of the API on the backend that takes time and causes pain. The pain is mostly felt when you have to work with the API on the frontend, or even worse when other people or companies are working with your API. Without strict conventions, you not only have to write documentation that shows what your API can do, but you also end up teaching how to use the API. This is where following a specification like the JSON:API specification shows its worth. How to use it is already documented and as long as you follow the specification, anybody who knows how to work with the JSON:API specification, knows how to work with your API. Of course, they won’t know what your API can do — you will still have to tell them that — but how to communicate with your server through your API, will never be a problem for them.

Even better, when following the conventions of the JSON:API specification, you have a strict protocol that never changes from application to application. This means that you can extract the whole client-server communication part of your frontend application and reuse it from application to application. You won’t have to write the same tedious boilerplate code over and over again, and you can focus on building the functionality of your frontend app instead. The JSON:API specification even lists available implementations, which includes implementations made for a lot of languages like Javascript as well as frameworks like VueJS and React.

The JSON:API specification was drafted in 2013 and had the first final v1.0 ready in 2015, where it has been used ever since. At the time of writing, a new version is about to be released, but as stated in the specification, the new version will always be backward compatible, using a “never remove - only add” strategy. So you won’t end up like us, where your inspiration is suddenly drastically changed. When implementing the JSON:API specification, you are ensured that people will always be able to use it, no matter which version of the specification they have learned and/or are using.

1『never remove - only add.』

As we see it, the JSON:API specification is a great approach to standardization of APIs and throughout this book, we will dive further into it and show you how to build an API in Laravel using it. Before we get ahead of ourselves, let’s commence by looking at the fundamentals of the specification.

#### 1. Client / Server Responsibilities

When you adopt the JSON:API specification, the first thing you have to look at are the headers sent in your request and responses. As a client, you have to send your request with:

    Accept: application/vnd.api+json

And

    Content-Type: application/vnd.api+json

These headers tell the server that what you’re sending lives up to the protocol given in the JSON:API specification, and also that you expect to receive data in the response that adhere to that same protocol.

As a server, you have to deliver your response with:

    Content-Type: application/vnd.api+json

to tell the client that what you’re sending lives up to the protocol given in the JSON:API specification.

#### 2. Endpoints

Though the specification provides a strict protocol for how requests and responses are structured, it only gives a few recommendations about how to form your endpoints. In this section, we will have a look at the recommendations from the JSON:API specification and give some of our recommendations as well. It isn’t hard to define endpoints, since you are already used to it by the routes you have defined in your existing Laravel applications. The thing that can be hard is making sure that you are consistent.

### 3. Naming conventions

In Laravel, we are used to working with models through the Eloquent ORM. Models define the tables in our database that hold the data for our entire application. Our API should give the client the data being requested and these data are most likely to be fetched from our database. Therefore, it is also very convenient to be thinking of our models as resources.

We are used to naming our tables after what they represent in the real world and often with nouns. As an example, the data for the users of our application will most likely be stored in a users table with a User model. The books of our bookstore will be placed in a books table with a Book model. The resource in this example would be “books”.

The naming convention may confuse since you are used to working with model names in a singular naming convention, but the table names are made in a plural naming convention. When it comes to resource naming, there have been a lot of discussions whether to use singular or plural names. The JSON:API specification doesn’t provide a clear answer here, but gives the following example of a plural naming when having URL for a collection of resources.

    GET: /photos

Later on, they do give an example where they use singular naming, but here it seems like it is done when there is a one-to-one relationship between resources. We have been down both roads and have felt both the upsides and downsides to plural and singular naming conventions and especially with a combination of both. We started out with a singular naming convention because it made a lot of sense, since it’s so close to how you work with models in Laravel. If we want to get a book we write:

```
<?php

$book = Book::first(); 
// or 
$book = Book::find(1);
```

Here, our endpoint would reflect this as:

    GET: /book/1

And it makes sense — if you want a single book, you write it out in singular. But what about the situation when you want a collection of books? Because of the conventions in the Laravel framework where model names are using a singular naming convention, it is not unusual to get a collection of Books when you write the following:

```
<?php

$books = Book::all();
```

For us, when it came to reflecting this in endpoints, we had a little trouble. It felt wrong getting a collection of books by:

    GET: /book

Because of this, we came up with a solution that borrowed a bit more of how Laravel’s Eloquent ORM work, with an endpoint like this:

    GET: /book/all

It isn’t pretty and it would force our consumers to always remember the all when wanting to fetch collections of resource, which we also occasionally forgot, whenever we had been away from the project in some time. The next API we wrote, we wanted to change that ugly reference to all and write something that made more sense. We opted to change the resource naming for requests for collections to plural. In this way, we would write the following to get a collection of books:

    GET: /books

And we could then write the following to get a single book:

    GET: /book/1

1『这里应该是作者的笔误，GET: /books/1。』

We thought this was a great and consistent way, until we stumbled upon words with irregular plurals. As a trivial example, let’s look at the word leaf. It has one spelling in singular, but the plural spelling leaves is different. Somebody whose first language isn’t English, could end up writing leafs and get an error. This could lead to confusion since you write the following to get a single leaf:

    GET: /leaf/1

To get a collection of leaves, you write the following:

    GET: /leaves

There is suddenly an introduction of inconsistency and that is not what we want. We want to have predictable behavior and one word only for a resource. The way we do it now, and the way we would recommend, is to use plural only. This might sound strange and like we would hit the same obstacles, but that is not the case. Let’s look back at the conventions by Laravel’s Eloquent ORM.

Model names are in singular, but tables names are in plural. Models are in singular, because you are only interacting with a single model at a time, since a single model corresponds to a single row in the database. Here, the singular naming convention fits perfectly. If you have multiple models, these are placed in collections. It’s not an instance of a Model you get. No, here you’ll get an instance of a Collection, which contains an array of many models.

A database table will contain one or more rows. It is suddenly a collection of data for the thing it represents, therefore the plural naming convention of Laravel makes sense for these. If we want a certain row in that table, we use a Primary Key, most often with the name id, to access that single row.

1『解释了在 laravel 里为啥 Models 的名称用的是单数，而数据库里的表单（table）却用的是复数。』

We like to take that same approach to our endpoint naming convention. We use a plural naming convention, like our table names, because we expect a collection of resources. We won’t be able to avoid irregular plurals, but by sticking to plural only, our consumers only need to remember one name and don’t have to care if that name is an irregular plural. They just have to remember the name leaves and that’s it. A request to the following will give us a resource collection of all books:

    GET: /books

If we want a single book, we fetch it, by giving an id to the books collection, like this:

    GET: /books/1

This also matches the way the JSON:API specification wants us to treat collections of resources, namely as arrays keyed by a resource ID. There is also a naming convention when it comes to relations between resources. These are a part of the protocols given by the JSON:API specification, which we will look further into in the upcoming sections.

#### 4. Before we continue

In the upcoming sections, we will take a deeper look at the JSON:API specification. We will touch upon conventions that the JSON:API specification states as conventions that MUST be followed and conventions the specification states as conventions that MAY be followed. However, we recommend that you follow the conventions we have picked out, whether the specification states that they MUST or MAY be implemented. We will touch upon most of the conventions given in the specification, but there are a few that we haven’t had any use for and feel that they cover more edge cases.

#### 5. Document structure

Let’s look at the document structure of the data for both JSON:API request and responses. The document describes how your JSON data should be formed, how members should be named, where these should be placed, and so forth.

Top-level. Here, the JSON:API specification states that there must be a JSON object at the root of the document, representing the top-level. In the top-level of the document, there must be at least one of the following members:

• data - which is the most important member that contains the primary data of the document.

• errors - which is a member that contains all error objects.

• included - which is a member that contains all resource objects that are related to the primary data and/or related to each other. We will touch more on this when we get to the section about resource objects and relationships.

• jsonapi - which is a member that contains the server’s implementation of the JSON:API specification.

• meta - which is a member that contains all non-standard meta information.

Note that it is very important that the data and errors member never coexist in the same document. The data member should only be used in successful request and responses, where the errors member should only be used whenever there is an unsuccessful request or response. By separating these, you have a clear convention that states where to look for either data or the errors that might occur. Now that we know what the top-level structure should be, let’s take a look at what our primary data will be and also how to structure that.

Primary data and Resource objects. In the section about naming conventions, we talked about how convenient it is to be thinking of our Laravel models as resources since these represent the rows of data in our database and data that we most likely will share across our APIs.

In this section, we will be looking at how to structure these resources according to the JSON:API specification. Resources or resources objects, as they are called in the JSON:API specification, will be placed in the data member and therefore serve as the primary data in the JSON:API.

We know that Laravel Models can be returned in a response, where Laravel will handle the whole conversion of the Model data into JSON, without you having to lift a finger. That’s great and a very convenient feature — we have certainly used it a lot in our earlier API days. But the problem is that the data returned is not consistent.

1『请求返回的数据保持一致性很重要，比如都是 json 格式的。』

There is no strict document layout so you know where to look for the data you need. Instead, everything is just exposed in the top-level of the returned document. One endpoint exposes a new resource with members different than the next one and you’ll quickly have to look at the documentation to find out where to look for the data. Moreover, you actually can’t see what type of model you are receiving, so you’ll have to rely on the naming of the endpoints to tell that part of the story.

As a solution to the aforementioned problem, the JSON:API specification tells us to structure our resource object in this way:

```
{
    "id": 1, 
    "type": "books", 
    "attributes": { 
    }, 
    "relationships": { 
    } 
}
```

In the example, you can see a clear structure. In the root of the resource object you’ll find:

• id - which is the id of the resource as a string.

• type - which is the type of the resource as a string.

• attributes - which contains all of the attributes of our resource.

• relationships - which contains all of the relationships of our resource.

This structure mitigates the problem of not knowing where to look for your data, not knowing the type of the resource, and it gives us a predictable and consistent way of accessing the data of a resource. It is ok for the attributes and relationship members to be empty. In fact, these can be removed if not used. But, as an absolute minimum, you should always have the id and type members in your resource objects, and the value of both should always be a string.

1『resource 对象的结构里面，id 和 type 必不可少。』

Ok, so we know how to structure our resource objects, but as we talked about in the naming convention section, there is a difference between requesting a collection of resources versus requesting a single resource. The difference here is not that big, but it is important to be aware of it.

1『请求单个资源和多个资源是有区别的，虽然差不不大，但要有概念。』

When requesting a single resource like this:

    GET: /books/1

the data member of the returned document should be structured like this: (note that we are omitting the attributes and relationships for the sake of simplicity)

```
{
    "data": { 
        "id": "1", 
        "type": "books" 
    } 
}
```

Here, the data member is the resource object itself. When requesting a collection of resources like this :

    GET: /books

the data member of the returned document should be structured like this: (note that we are omitting the attributes and relationships once again)

```
{
    "data": [ 
        { 
        "id": "1", 
        "type": "books" 
        }
     ] 
 }
```

Here, the data member is an array containing the requested resource objects. As you can see here, it should be an array even if there is only one resource in the collection. If there weren’t any resources in the collection, an empty array should be returned. We got the basics down and it’s time to look at those attributes and relationships we have omitted in the examples. Here, we open up for the ability to create our own member names, therefore it is important to look at the naming convention for these as well to ensure consistency.

Member names. The JSON:API has a clear naming convention when it comes to member names, where all member names must be treated as case sensitive by both client and servers. Other than that, there are some conditions that the member names must also follow: 1) Member names must contain at least one character. 2) Member names must contain only allowed characters. 3) Member names must start and end with globally allowed characters.

We strongly recommend that you keep all your member names in lowercase and stick to a convention when picking characters like spaces, like these examples:

Using underscores as space, also known as snake case:

```
{
    "member_name": "content" 
}
```

Using hyphens as space, also known as kebab case:

```
{
    "member-name": "content" 
}
```

Using a capital letter on the next word to indicate a space, also known as camel case:

```
{
    "memberName": "content" 
}
```

We have adopted the camel case as a naming convention when coding in PHP, but in our APIs, it’s a bit of a different story. Here, we use snake casing, mostly because that’s a convention we have used from the start, when looking at other companies’ APIs. At the time of writing, both Google, Dropbox, and Facebook use snake cases in their APIs. Also, when calling the toJson() method on your model, Laravel converts your model attributes spaces into snake case. Our recommendation is to use snake cases, especially because we will be using these in this book, but also since it comes for free with Laravel. The choice, however, is entirely yours — just make sure you are consistent and don’t suddenly change in the middle of working with this book or in your own APIs.

1『snake casing 是用下划线的形式命名。』

Aributes. Now that we have a naming convention for our member names, we can continue to attributes. Attributes on a resource object are just like the attributes on your model in a Laravel Application. These are data like the title of a book, the name of an author, and so forth. The JSON:API specification specifies that on a resource object, the attributes member should be an object. Any member inside this object can be whatever data that represents the object, but must never be a relationship. For relationships, we use a dedicated member in the resource object, which we will look at shortly. To make an example, let’s look at a single book again:

```
{
    "data": {
        "id": "1", 
        "type": "books", 
        "attributes": {
            "title": "Build an API with Laravel",
            "publication_year": "2019" }
    } 
}
```

Here, you see the definition of the attributes member as an object containing two members, namely title and publication_year. You also see how the naming convention of snake casing takes effect. As mentioned earlier, the attributes member can contain any information about the resource object, but cannot contain relationships or a member called relationships. Another rule is that the attributes member can never contain an id or type member, since these are reserved on the root of the resource object. But how do we define relationships then?

Relationships. When it comes to data in an application, these are often related to one another. When building applications in Laravel, we are used to defining models as objects in real life and as such, these have different relations to one another:

A car belongs to a brand, a bus can have many passengers, a book can have many authors, and an author can have written many books. Do you see how everything connects? Chances are that you have already written something like the sentences we just presented, since Laravel uses most of the wording in the relationships you define in models.

```
<?php

namespace App;
use Illuminate\Database\Eloquent\Model;

class Car extends Model {
    
    /** 
    * Get the brand of the car 
    */ 
    public function brand() 
    { 
        return $this->belongsTo('App\Brand'); 
    }

}
```

By declaring a relationship method on our model, we can fetch the brand of our car very easily, now that we have told Laravel about the relationship. But how do you tell about relationships in your APIs and how do you convey enough information, so that your consumers can easily get the data they want? Relationships in the JSON:API specification is defined as the relationships member. Like the id, type and attributes members, it should be placed at the root of the resources object and be defined as an object like this:


```
{
    "data": {
        "id": "1", 
        "type": "books", 
        "attributes": {
        "title": "Build an API with Laravel",
        "publication_year": "2019" }, 
        "relationships": { }
    } 
}
```

Unlike the attributes member, where you are in charge of the members, the relationships have a more strict set of rules. A relationship member must contain at least one of the following members:

• links

• -self

• -related

• data

• meta

Let’s take a look at the links member. This member contains two types of links. The link for the self member is a link for the relationship itself. With this link, it is possible to manipulate the relationship between two resources without having to delete one of them. A good example here would be tagging. If a book contains one or more tags, this link can be used to remove the tag from the book without having to delete the tag or the book.

1『只需要移除标签的连接即可，避免直接删除标签和书本身。』

The link for the related member is a link for the relation between resources. When making a request to this link, the related resources will be queried and returned as primary data. This is very much like calling a relationship method on your Laravel models, where Laravel will make a query for the related models of that model for you.

The data member is something we have seen before, yet this one is a little different. It’s called the resource linkage and instead of holding resource objects, it holds resource identifier objects. In contrast to resource objects, which hold id, type, attributes and relationships members, resource identifier objects only contain the id and type members of the related resource object.

The meta member is a meta object that can contain non-standard metadata about the relationship. We haven’t had the need for this yet and thus won’t include it in the examples. Now that we’re talking about it, let’s take a look at the relationship between a book and an author:

```
{
    "data": {
        "id": "1", 
        "type": "books", 
        "attributes": { "title": "Build an API with Laravel", "publication_year": "2019" }, 
        "relationships": { 
            "authors": { "links": { "self": "http://example.com/books/1/relationships/authors ", "related": "http://example.com/books/1/authors" }, 
            "data": { "id": "5", "type": "authors" }
            }
        }
    } 
}
```

If you take a look at the JSON example, you can see the author member inside the relationships object. In this example, we have the links that make it possible to easily fetch the related resource, which in this case is the author of the book. In the example above, we have a single author, as in a one-to-one relationship. In the case of a one-to-many or many-to-many relationship, an array should be used instead, just like this:

The way the data attribute contains resource identifier objects is just like the primary data’s data member, which holds either an object for a single resource or an array for a collection of resources. Ok, that was a bunch of rules at once. Let’s recap on how to define a relationship. We make an object as the relationships member. Each member inside relationships defines each related resource. In the examples given above, the relationship is between books, authors and comments. All of those combined would look like this:

Inside each relationship, we have at least one of the members: 1) inks. 2) data. 3) meta. In our case, we have both links and data, which we recommend that you do as well. The links members give us a consistent way of accessing either the relationship between the resources or the related resource object. The data members give us either a resource identifier object or a collection of resources.

We now know how to define relationships, we even know how to provide links for manipulating relationships and how to fetch related resources. If we want the comments for the book, we can simply make a request to the link given in the related member and a response containing all the resource objects will be returned.

1『这张完整的 json 数据结构好好研究琢磨。』

Right now, the data member of the relationships seems a bit redundant, since it only contains id and type member instead of an entire resource object, but let’s look further into this in the next section and it will make more sense.

#### 6. Compound Documents

We have just looked at the relationships member and what kind of members this should contain. We left with some confusion about the data member inside the relationships object. To understand this part, we need to revisit the top-level of our document, more specifically the included member. We only touched upon this briefly in the section about Top-level, so let’s have a better look at this.

When building an API or an application for that matter, you have to make some thoughts about optimization and make sure your application performs as intended. One optimization could be to reduce the number of HTTP requests as much as possible. One way to do this is to use the included member. The reason for this is that it makes it possible for you to include the related resources of the fetched resource, which will then be the resources defined in the data member in the relationships object. Instead of having to make a new request for the related resources, they can just be included in the current response.

In this case, the resource objects sent in the included member will correspond to the resource identifier objects given in the relationships’ data member. Let’s build upon the previous examples to give a better idea of this:

In the example, you can see how the included member, includes all of the resource objects, for the resource identifier objects given in the data member. Here, it’s important to note that the included member will always be an array that contains all of the related resource objects mixed together in a flat array. The included member can be included by default, or by an include query parameter like this:

    GET: /books/1?include=comments

Here, there will not be anything included before the query parameters are in the URL and if the relationship does not exist, a 400 Bad Request should be used. If you choose to support using the include query parameter, there are a few more things you should implement.

First, it should be possible to specify which relationships that should be included in the response using a comma separated list:

    GET: /books/1?include=authors,comments

It should be possible to request resources related to other resources using a dot-separated path for each relationship name. In our example, a book has a relationship with authors and comments, but each comment also has an author, in the form of a user who created the comment. If we wanted to include the users for each comment, it should be possible to do this by adding the related resource like this:

1『请求时，请求的资源如果跟另一个资源相关联，可以用逗号分隔开这两个资源。』

    GET: /books/1?include=authors,comments.users

Again, if it isn’t possible to fetch the related resource, you should return with a 400 Bad Request. Whether you want to use the include query param is all up to you, and the same goes for the included member in your response documents, but if you choose to do so, you must have the data members in the relationships object, for each of your relationships. If not, you can omit the data member, but you then have to have the links member, so that the related resources can be requested through the related link.

Now, let’s take a step back and think about what we have been through. We now know how to structure the document for our data. We know that we must have a top-level object and that we must have a data member representing our primary data, and that the data member can be either an object or array, whether it’s a single resource or a collection we have requested. We know that a resource is represented in our document as a resource object that must contain an id and type member, both with a string datatype.

We know that we can use an attributes member to give information about our resource object, which in this case would be the attributes of your Laravel models. We know how to use the proper member name convention in our attributes object and how it’s important to stick to a naming convention strategy as snake case to keep consistency. 

We know how to represent a relationship between our resources through a relationship object. We know how to define a relationship as yet another object, which contains a links member with links to the relationship itself or the related resources and a data member holding resource identifier objects for use in the included top-level member. We know how to use the included top-level member to save HTTP request by sending related resources in the response.

That was quite a lot and we are almost done with the JSON:API specification. Before we move on though, we just have to look at how we make requests and responses using this new document structure and also how we handle errors.

#### 7. Request and responses

It’s time to look at how we should make our request and responses according to the JSON:API specification. We know what to send and what we can expect to receive, but we don’t know how to request it or how these should be sent with a response yet. Of course, there are conventions and we will adhere to them. Let’s take a closer look.

Requests. All requests to get data from our API must be done with a GET request. Remember the previous chapter in the section about REST and HTTP verbs, the GET request is for reading data and the same goes for the JSON:API specification. Nothing has changed here.

Some interesting conventions the JSON:API specification brings along for requests is the ability for sorting and pagination of collection data. These are only optional conventions, but we are mentioning them because we have had great use of these. There are more conventions, but these are outside of the scope of this book. Now, let’s first take a closer look at sorting.

1『GET 请求还可以额外添加两个功能：sorting 和 pagination。』

Sorting. Sorting data is a great feature to have in an API. Think about sorting just like ORDER BY in your database. You get the ability to sort your data based on member names in a more dynamic way, instead of being limited by the way the API developer may have thought was the best way to sort the data. Sorting data is done via a query parameter. If you are unsure what a query parameter is, it is a convention in HTTP you use to send along parameters for a request, as a part of the URL like this:

1『问号 ? 是查询参数，问号后面的座位一个参数传递进查询的 url 里，比如作为条件的一个参数。』

    GET: http://example.com/cars?color=blue

Here, the parameter we are sending along is color with a value of blue. The query parameter used by the sort feature is the sort parameter. The value of the parameter is the member name of the attribute you want to sort by. It would look something like this:

    GET: /books?sort=title

If you want to support multiple sort fields, these should be separated by a comma like this:

    GET: /books?sort=title, publication_date

When ordering a database query by a column name, we are able to tell if the ordering should be done in ascending order or descending order. The same thing goes for sorting a collection, according to the JSON:API specification. Here, a sorting is always done in ascending order unless you prefix a sort field with a minus, in which case it will be sorted in descending order. It would look something like this:

    GET: /authors?sort=-age

Here, you will get the oldest authors first, descending until the youngest author in the collection.

Pagination

Pagination is another feature that can have great benefits, especially if you have large sets of data that can be quite a strain on the system to query. You can paginate the results and do the queries in smaller chunks, letting the API consumer do the work of progressing through the pagination. The way pagination is done in the JSON:API specification is through a links object in the root of the response document. The links object must have the following members used for pagination links:

• first - which is the first page of data.

• last - which is the last page of data.

• prev - which is the previous page of data.

• next - which is the next page of data.

The links object in the document would look something like this:

In the example, you can see a collection of books and in the bottom of the response document you see the links member with the four members of a pagination link object. Can you guess which page we are on? Correct! We are on page two! Had we been on the first page, the JSON:API specification actually requires us to omit or set a null value for the links that are unavailable, which in that case would be the prev link, since there is no previous page, when being on the first page. Just to demonstrate, here is an example of that scenario:

You see how a null value is provided for the prev member to indicate that it is unavailable. The JSON:API specification does not have any conventions when it comes to query parameters signifying which page in the pagination we are currently on. However, they state that the page query parameter can be used for this and we will recommend that as well. The good thing about this is that it’s then possible to deep link into a page of data using the page query parameter. We will support this in our API as well.

Now, we know how to make a request for data and even how we can sort or paginate data provided in collections. It is time to look at responses and the conventions from the JSON:API specification we must follow.

Responses. It’s time to look at the server side and which convention it must adhere to when sending responses to the client. Here, we will revisit HTTP verbs and status codes as well as look at conventions that must be followed to keep your API consistent. The first rule we will look at is making GET requests for data or fetching data, as the JSON:API specification calls it.

Response guarantees. Here, the server must always support getting resource data and or relationship data for all URLs that are provided in a response. The URLs we are talking about are the URLs provided in a relationship for a resource object. It is the links given in the links object of the relationship object, more specifically the self and related links. It should always be possible to get data through these links, otherwise we are breaking the conventions from the specification. Also, it would not make a lot of sense if links we provide from the API does not work. It would lead to a lot of frustration for the consumers of the API and that’s not what we want.





















