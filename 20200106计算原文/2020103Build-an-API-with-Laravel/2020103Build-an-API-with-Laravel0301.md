# 03 Planning

Now that we have the basics covered and have been through the JSON:API specification, it’s time to talk about planning.

For us, this is the most important part of a project. Whether it’s a small, medium or large project, it is always beneficial to do some planning ahead of time to identify possible problems and roadblocks you can steer around. For us, time equals money so we need to be as fast and efficient as possible.

The same goes for APIs. The more you can plan out ahead of time, the more it benefits you later, when you actually have to implement the API.

If you are making a public API, we especially recommend planning ahead and documenting your API as early as possible. In this way, you know everything about the data and what needs to be developed ahead of time, as well as getting a good grasp of where the more complex areas of your application lie.

The planning tools and methods we will be going through in this chapter are those that we use when planning out our projects. These are the methods and tools we have picked out over time, that fit most of our projects.

## 01. A different way of planning

If you have never written an API before, you need to think of your applications in a new way.

If you are used to building Laravel Applications in the more “old-fashioned” way, where Laravel primarily render all the HTML and returns this to the user’s browsers, thinking in APIs is completely different.

You can stop worrying about user interfaces and how the application should look and feel. You still have features, but it’s in the form of tasks that the backend should perform. The actual worries about UI / UX can be handed over to the frontend developers on the client side and you get to worry about data instead. That can still seem like a daunting task, but remember that the difficulty of projects vary, and in some cases, your backend doesn’t even have to be that smart. In some cases, its only purpose is to ensure that data is stored and retrieved from databases correctly and that’s it. It is quite a contrast to what we are used to, with applications that do all the work on the server.

In most of our newer projects, the client does most of the hard work. Through single page applications, which are Javascript powered web applications, we can build a much more intuitive user experience than ever before. It almost seems like you’re interacting with a real desktop application and not a web application. In fact, it is possible to build desktop application this way too, but it is beyond the scope of this book.

The HTML responsibilities have been removed from the backend so it can focus on tasks like saving/retrieving data, whether it’s from a database, external services or APIs, to sending emails, encoding audio or video and so on.

And of course, this has changed the way we plan our projects. We are still doing UI / UX but it is now separated from the planning and development of the backend. When planning our backend, we can focus on data and how

75 BUILD AN API WITH LARAVEL

these data need to be delivered, retrieved and related to each other. Instead of templates, views and actions, we are thinking in resources and relationships.

This makes it possible for us to plan our backend development with the API in mind, since this will be the new interface. By defining our resources and starting to document these, we are forced to think about our applications and the requirements of the backend. You see by documenting the API, we need to think about which data that needs to go into our application and also how we want the application to respond. This isn’t easy if you are doing everything from scratch, but remember that we have the JSON:API specification to lean on, so we know exactly how our request and response documents should be formed. We only need to think about the attributes of our documents.

With the documentation done in the planning phase, we not only have everything planned, we get the documentation out of the way. An even bigger plus is that it makes it possible for the frontend developers to mock our API and that makes it possible for the development to be done almost in parallel.

So let’s start thinking in these new ways and begin to plan out our API.

Requirement Specificaঞon

The first step in planning a project is to identify all the requirements for the project and put them in a requirement specification. This is especially important since it describes all the features that should be implemented and also how these features are expected to work. It’s a document that gives a consensus between the customer and the developer.

Through an interview of the customer, you should take notes of what they tell you about the project they would like you to develop. When interviewing, it’s important to consider how we as developers know all the terms in the business, but our customers might not — especially not someone like Anna from the hypothetical coffee shop of our case example. Because of this, it is

76 PLANNING

our responsibility to take good notes and talk to the customer in a language they understand, and afterward transform those notes into clear requirement specifications that both parties can understand and agree on. Of course, it’s also our responsibility to cover as much as possible, especially if the customer does not know a lot about software development. In that case, small sketches can be a huge help, particularly when trying to convey functionality between you and the customer, but also when you have to write the requirement specification later on.

It always pays off to be thorough and leave no stone unturned, so take good notes and be sure to write down all the important parts of the interview. If you are not that good at note taking, then ask if you can record the interview with an audio recorder. The customer is just as interested in a good product in the end as you are, and oftentimes they don’t mind being recorded.

When you have your notes after the interview, it’s time to write the actual requirement specification.

We recommend that you start out by identifying the main areas of the application you’re going to build and divide your specification into these areas. In terms of a bookstore these could be:

• Public store

• User Profile

• Administration

In a case like this, we would recommend starting out with something easy that you are familiar with to get the ball rolling. You should be familiar with how authorization and login work, so start out with that. In the areas above, there are two that need access restrictions and the authorization methods might not be the same. Start by making requirements for the authorization for one of them.

77 BUILD AN API WITH LARAVEL

Write each requirement in bullet form and make indented bullets if something needs to be explained further like this:

• The administrator should be able to enter an email address

• - The email should be of the bookstore’s own domain to be allowed as administrator

• - The email cannot also be used for a regular user profile.

• The administrator should be able to enter a password

• - Passwords should be over 6 characters

• - Passwords should contain at least one capital letter

• - Passwords should contain at least one number

• The administrator should be able to tick a “remember me” checkbox

• - When ticking the remember me checkbox, a cookie should be saved for easier logins in the future

• - A “remember me” cookie should only be valid for 48 hours

• The administrator should be able to click the login button to proceed

• The administrator should be able to see if he/she has entered the email or password incorrectly.

The language in each requirement should most often contain “should”, “must” or “cannot” to clearly signify that it is a requirement for the project.

In the example we gave, some of the requirements relate to the flow of a login, whereas others are business rules, like “The email cannot also be used for a regular user profile”. In some cases, there can be more requirements that describe business rules, rather than the flow. Here, we recommend writing a little scenario to accompany the requirements of the area you are describing. This would look something like:

The administrator has arrived to the login screen.

She types in her email in the email section and pushes the tab button on her keyboard to get down into the password space, where she types

78 PLANNING

in her password as well. Before clicking the login button, she ticks off the “remember me” checkbox so she doesn’t have to perform the same procedure, if she comes back within the next 48 hours.

Now both the requirements and the scenario describes the authorization precisely. We know what should be developed and the customer knows what to expect.

As you can see, a requirement specification describes the entire project, not just the API, but there’s a lot we can get from the requirement specification as well as the other developers working on the project.

Some of the logic described in the requirements can be on either the frontend or backend and in that case it might be something our API should support.

From a broader perspective, let’s start to focus more on our API. To do this we first want to introduce you to Postman, which we will be using throughout the most of this book.

Postman

Postman started out as a small in-browser application for Google Chrome in 2012. Later, the application expanded to native applications running on desktop machines, and now it’s an entire Saas platform.

We have used it for years, first as a tool to test out our own, but also especially, third-party APIs. Sure, you can do the same with CURL, but often a nice UI and the ability to remember both requests and responses beat that.

The expansion of the application has also included features like:

• Multiple Workspaces - which gives a great separation of projects with the ability to invite others to share the same workspace as well. A workspace

79 BUILD AN API WITH LARAVEL

embraces the following features mentioned in this list.

• Collections - Which is a grouping of requests, a feature we will be using while planning and developing our API.

• Mock Servers - Which is a feature that makes you mock out your API when all endpoints and responses have been planned out. A great feature for frontend developers, which makes it possible to interact with a mocked server, making it possible to work in parallel with the backend developers.

• Monitoring - Which is a way to schedule automated tests and thereby monitor how your API performs.

• API Documentation - Which makes it possible to create and publish documentation for your API using your collections.

It is especially the ability to test our APIs, the collections, and API documentation we are interested in and will be going through in this book. First, we will be looking at how to plan out our API by setting up a new workspace and identifying resources to determine our endpoints, the attributes of our resources, and later identifying relationships and adding these in as well.

Download & Installaঞon

To download the application for your platform, follow this link https://www.getpostman.com and click on the “Get Started” button. This will lead you to the download page, where you can click on the “Download” button to get the version for your platform. When it’s downloaded, install the application and when the installation is done, open the application.

When opening the application, you should be greeted with an interface that looks like the image above. It might prompt you to login and if so, create your account and log in. If you did not get a login, you’ll hit it as soon as we start working with Postman and you can then create your account.

If you are at the screen you see above, close the window by hitting the X in the corner.

Creaࢼng a new Workspace

After you have installed Postman, created your account and logged in, you should be seeing an interface like the one in the image above.

It’s time to create our workspace for the API we will be building. Click the “My Workspace” dropdown at the top of the window. In the dropdown, click “Create New” and you will see a form that needs to be filled out to create the Workspace.

Name the workspace “Build an API with Laravel” and leave the summary blank. Under “Type” choose “Personal” and click “Create this workspace”.

You should then be seeing an interface like the image above.

Great! We now have a workspace for our API, so let’s take a closer look at the Postman interface.

User Interface

On the image above, you can see the division of the two main areas of the Postman application.

• Is the side panel where we will create our collection of endpoints for our API.

• Is the main area where we will do our main work, like create requests, define the body of our requests, and later create examples for the documentation of our API.

At first, we will mostly work in the side panel and do some minor work in the main area. When we get deeper into planning our resources, we will do most of our work in the main area.

Just to quickly show you the features of the main area, let’s try to make a request to the following URL:

84 PLANNING

GET: reqres.in/api/users

In the top of the main area, you see a gray input with the placeholder text “Enter request URL” and then a selector to the left of this, that has all the HTTP verbs. Directly underneath, there are some tabs and then a small table, where you can fill out params.

This is the request area of the main area. Set the HTTP verb to GET and input the regres.in/api/users URL and hit the “Send” button.

Now you can see the response document from the server underneath the request area formatted nicely, so you can see every bit of data that are sent from the server. This is the response area. Here you can also look at the cookies and headers sent from the server.

If you feel like the request and response areas blend too much, you can switch

85 BUILD AN API WITH LARAVEL

to “Two-pane view” by clicking icon down in the bar in the bottom. This will make the request and response areas sit side-by-side instead, except for the actual endpoint and HTTP verb of the request. For clarity, we will be using this mode for the rest of this book, since it makes it easier

to see the difference, in which data that are being sent in a request, and which data that have been received in the response.

The reqres.in is a fake REST API you can use to test your frontend or programs like Postman against a live API. If you want to explore Postman’s capabilities more in depth, we recommend that you spend some time going through the various requests you can make to the API using Postman. We will, of course, return and go through more of the features when we start building our own API.

Before we move on though, take a look at the side panel. It should be on the “History” tab where you can see the latest requests you have made. Next, we will be looking at the “Collections” tab in the side panel.

Collecࢼons

Click on the “Collections” tab in the side panel. Here, you will be greeted by a message saying “You don’t have any collections”.

Click on “Create a collection” to create a collection. In the overlay that opens, name it “Build an API with Laravel - V1”. In a workspace like this, it is possible to have multiple collections where each collection will produce its own documentation. If we were to update our API in the future, it would be possible to produce new documentation to keep the two versions separate.

Leave everything else as it is, click the “Create” button, and you should get a new collection like in the image above.

Click the small arrow to the left of the folder icon and you will see a message telling you that your collection is empty, and you can add request and create folders to organize your request.

A request in Postman is a request to a single endpoint. This could, for example, be a request to the following endpoint to get alle books:

GET: /books

Another request could be for the following endpoint to get the book with an ID of 1

87 BUILD AN API WITH LARAVEL

GET: /books/1

Another could be to the following to create a book:

POST: /books

Hopefully, you see a pattern here and see that all requests are for the book resource. Instead of having these in the root of our collection, we can make folders and give these the name of a resource. This will group all requests for that resource and later get a nice separation of requests in our documentation.

Before we do that, let’s revisit how we identify resources.

Idenঞfying Resources

It might seem strange that we use Postman as much in our planning phase, but since it’s the platform in which we will create our documentation, you can get ahead by starting to document your findings in your planning phase right away. Nothing is written in stone, we can still make changes as we go, but instead of putting things on paper, why not put it into something useful that can save us time later on.

In chapter 2 when we covered naming conventions for endpoints, we talked about the convenience of thinking about our models in a Laravel application as resources.

If we take another look at the case presented in chapter two, we have been given the following objects of real life:

• Books

88 PLANNING

• Authors

• Comments on a single book

As Laravel developers, we would quickly identify that we need a model for each of these things and that’s absolutely right. But we are here to plan and here to think ahead and find roadblocks that we might have to steer around. If you ask us, that specification up there is only telling half of the story.

In an application like this, there must be someone who creates new books and updates books, or deletes the books that are no longer on sale and the same goes for authors. The persons we are referring to here are administrators. In order to service the bookstore, we need administrators to perform these tasks.

What about comments, who leaves those? The common thing here would be a registered bookstore user. They can leave comments on books and possibly in a future implementation, also leave ratings of these.

If we step back a little and actually look at the things we just discovered about administrators and users, we can see that we have a multi-tenant application on our hands.

A tenant is a group of users that share the same access levels in an application. Since we have administrators, who are allowed to administer books and authors, but also users that are allowed to comment on books, these are two different tenants and therefore it’s a multi-tenant application.

There is not a standardized way of making multi-tenant applications in Laravel, but a common pattern is to use a “Role” or “Type” attribute on the User model to differentiate the users and thereby only using one model for handling users and administrators. We will be using this strategy in our API, where we will be using a role attribute to not confuse anything with the already existing type member coming from the JSON:API Specification.

89 BUILD AN API WITH LARAVEL

Idenঞfying Aributes

When identifying attributes, you can rely on the same methods you use when thinking about columns in your database or attributes on your models in Laravel.

If a book is an object we are trying to model into our database, the columns convey more about the book. That could be things like:

• A title

• A summary

• Number of pages

• Publication year

Laravel can help you send all these data in the response of your API, but also filter those parts you do not want to give. In the end, you decide how much information you want to give. In terms of planning, we often use the columns we identify when planning our database.

This gives us the ability to start documenting a lot of our APIs early on and also provides the ability to start mocking the API so that the frontend development can begin early on as well.

Idenঞfying Relaঞonships

As important as it is to identify resources, it is just as important to identify relationships. These are not only to be defined in your API, but your models as well, and the type of the relationship defines the complexity.

It is also the first step where you really have to think about your data and how you are solving the given problems, as well as whether or not decisions you make have an impact when the end-users start working with the application.

90 PLANNING

Idenঞfying the right relaঞonship

Let’s examine the first and most obvious relationship between Books and Authors. Here a one-to-many relationship would be the easiest to implement. From a database perspective, the book could have a foreign key pointing to the author who has written the book, and from a Laravel Eloquent perspective, a book would belong to an author and so forth.

If you didn’t stop and think about it, a one-to-many relationship might be a constraint on the applications. Because of that decision, there can only be one author for each book in the bookstore, or at least only one author would get the credit.

This is a roadblock we want to identify early, so that we can steer around it. Here, it would be much better to have a many-to-many relationship since a book can be written by many authors, but an author can also have written many books. By identifying this early and not having to change this later when the code is already written, we have potentially saved hours.

In terms of an API, the relationship here would be the same. Since we do not have a one-to-one relationship, we know that the relationship will involve collections.

Idenঞfying the remaining relaঞonships

Let’s move on and identify the remaining relationships. Since we are already in the vain of books, why don’t we look at the relationship between books and comments next?

The relationship here is not that complex, a comment will only ever be for one book and a book can have many comments, so a one-to-many relationship is pretty easy to identify here. In terms of our API, it’s not a one-to-one relationship, which means that we will still work with collections. There’s

91 BUILD AN API WITH LARAVEL

one thing here that we might have to note and that is about the users and the relationship between a comment and a user. In the case where you request all comments for a book, it would be nice to also have the users for those comments. Remembering back to the Compound Documents section of chapter 2, this is a good candidate for data to be included in a response, since you would not have to have yet another request just to get the users that the comments belong to. But we are getting a little ahead of ourselves. Let’s take a look at the relationship between comments and users then.

Again, it’s not that complex. A comment can only really belong to one user so this must be a one-to-one relationship, and in terms of our API, we will be handling a single resource identifier object instead of collections.

Let’s see the relationships we have identified then:

• Books and Authors - A many-to-many relationship with endpoints:

• - Self

GET: /books/1/relationships/authors

• - Related

GET: /books/1/authors

And the inverse relationship from authors:

• - Self

GET: /authors/1/relationships/books

92 PLANNING

• - Related

GET: /authors/1/books

• Books and Comments - A one-to-many relationship with endpoints:

• - Self

GET: /books/1/relationships/comments

• - Related

GET: /books/1/comments

And the inverse relationship from comments:

• - Self

GET: /comments/1/relationships/books

• - Related

GET: /comments/1/books

• Comments and Users - A one-to-one relationship with endpoints:

• - Self

93 BUILD AN API WITH LARAVEL

GET: /comments/1/relationships/books

• - Related

GET: /comments/1/books

And the inverse relationship from users:

• - Self

GET: /users/1/relationships/comments

• - Related

GET: /users/1/comments

Now we have both identified our resources and relationships, and are ready to begin our documentation. Before we do though, and we promise this is the last thing, let’s just quickly take a look at IDs and UUIDs, since there’s a bit to consider here — again to avoid hitting those roadblocks later.

IDs and UUIDs

When planning out an API, you have to think about what kind of information you are giving away. The things we are talking about here are the IDs of your resources. Of course, it’s convenient to reuse the IDs given by the database, but is that really a good idea? It depends on the application behind, especially if it’s a multi-tenant application. If you take IDs from a database, these are most often primary keys in the form of integers that increment chronologically for

94 PLANNING

each row in that database. If you were building a multi-tenant application, one user could potentially try to access another user’s data, by editing the ID of the resource being accessed. And given the chronological order of IDs, there’s a good possibility that the data of the given ID exists in the database.

In this case, it would be a better idea to use a UUID.

A UUID or Universal Unique IDentifier is a 128-bit number we can use to identify entities in our applications. These entities could be users in your application: they could be books, they could be virtually any table in your database, but the key here is that they are used to identify information in our systems. UUIDs can be generated by anyone and does not require some kind of central registration authority to keep track of each UUID created. This does mean that there is a probability that a UUID could be duplicated, but the chance is very close to zero and would not happen in the same system at least, which makes UUID eligible to use for primary keys in relational databases, which we use for Laravel.

The fact that we get a 128-bit unique number has another advantage, namely that an UUID is near impossible to guess.

There are 5 different versions of the UUID standard where each version generates a UUID in different ways. As an example, the first version uses a date-time and the MAC address of the machine in which it is being generated to generate a unique ID.

The version we use the most is version 4, which does not use MAC addresses and the like, but generates a random number.

It doesn’t mean that you always have to use UUIDs. Sometimes, you also have to consider ease of use for your API, especially if it’s public. And if the IDs don’t present a security risk, you could keep the IDs from the database.

95 BUILD AN API WITH LARAVEL

Beginning our documentaঞon

We are finally ready to begin our documentation since we now know which resources and relationship we need in our application. Let’s start by documenting resources and endpoints, and afterward we’ll go more into detail with attributes and relationships.

Folders for Resources

Firstly, to have a nice segregation of resources in our collection and later our documentation, we want to create Folders for each resource. By clicking on the three dots, we get a menu in which you will click on “Add Folder”, as shown in the image below.

In the overlay, give the folder the name “Books” and click on the “Create” button.Repeat the same procedure for the rest of the resources which are:

96 PLANNING

• Authors

• Comments

• Users

When you’re done, you should have something that looks like the image above.

Resources Requests

In the next sections, we will be going through the entire documentation process for the Books resource only. But don’t worry, with the methods used here, you will be able to document the rest of the resource yourself, plus it will give you hands-on experience with both Postman and documenting your API.

To make a request in a resource folder, you need to click the three dots that appear when you hover over the folder name.

Select “Add Request” and name the first request: All Books and click “Save

97 BUILD AN API WITH LARAVEL

to Books”.

In the main window set the method to GET, enter the URL /books, and click the “Save” button next to the “Send” button.

Create another request and name it: Single Book and click “Save to Books”. Give it the method GET and URL of /books/1 and click the “Save” button next to the “Send” button.

Create yet another request and name it: Create Book and click “Save to Books”. Give it the method POST and URL of /books and click the “Save” button next to the “Send” button.

Create the last requests for:

• Update Book

• Delete Book

The Update Book needs a PATCH method and the Delete Book needs a DELETE method. Both have the same URL:

/books/1

98

You should have something that looks like the image above.

Now, just for the fun of it, let’s see how our documentation is taking form. If you look at the status line in the bottom, there are two buttons in the lower right named “Build”, which is active at the moment, and “Browse”. Click the “Browse” button and click the name of your workspace. You will now be presented with a somewhat raw version of our documentation, but this gives you an idea of what we are slowly building as we give Postman more information. Look how our folders provide a nice structure to the menu. We still need all of our attributes and also the responses that can be expected. Let’s look at the attributes next. Go back to Postman and click on the “Build” button.

Resource Aributes and Request Document

When thinking in attributes, do you then know when we need to document these? Right, it’s when creating and updating our resources. Let’s take a look at the Create Book request in Postman to set up our request document and

99 BUILD AN API WITH LARAVEL

add the attributes.

Remember that we are using Two Pane View in Postman, so the bottom part of our main area is divided into request on the left side and response on the right.

On the left side, there’s a menu with the tabs shown in the image above. Here, we will be working in the Body tab to be able to define our request document, so you should click on this.

Under the Body tab, you’ll see a bunch of choices for the format of our data. You should choose Raw, which makes us able to define our request document in the JSON format so that it adheres to the JSON:API specification. Right under the choices, there’s a dropdown list that currently is on Text. Fold this out and choose JSON (application/json). You’ll see a change in the header’s tabs with a 1 indicating that there’s one header defined in the request. We will return to that shortly.

You should be at the same point as shown in the image above. Now it’s time to define our request document.

First, we need to define the root of our request document and as the JSON:API specification states, we need to have a root object with a data member for our primary data of the document. Since we are documenting how to create a book, the primary data for our request document will be a resource object for a book. The important thing here is to define the type member as a string and then the attributes member as an object, which makes the entire request document look like this:

{

"data": {

"type": "books", "attributes": {

"title": "Example book",

"description": "This is an example of a book",

101 BUILD AN API WITH LARAVEL

"publication_year": "2019"

}

}

}

In Postman it should look like the image above.

We’re almost done defining the Create Book request. We just have to go back to that Headers tab and take a look at the value of the Content-Type header defined by Postman.

The value here is application/json but since we want to adhere to the JSON:API specification, we need to use the right Content-Type defined in the specification. This needs to be changed to application/vnd.api+json.

Before we move on, we might as well set the Accept header as well. Like the Content-Type, this should be application/vnd.api+json to tell the server that

102 PLANNING

we expect to receive the data in the same format.

Click the “Save” button next to the “Send” button again to save your changes.

Just a little caveat. If you go back to the Body tab, the content under Raw has changed back to the text. This is because Postman does not recognize the JSON:API specifications Content-Type and does not know that it is indeed JSON. We hope they will fix this in a future update, but for now we will have to live with it. If you need to make alterations, you can change it from text to application/json again, but be aware that the Content-Type in the header tab will change back to application/json as well, which means that you need to change this to application/vnd.api/json when you’re done.

If we look at our documentation now by clicking Browse in the status bar at the bottom, and clicking Build an API with Laravel afterward, we can see that our documentation now contains the attributes for our resource together with the correct request document. It even gives an example of how to implement this request. But wouldn’t it be great if we could get an example of how the response document would look as well? Then everybody would know which data are being returned. Postman has us covered here with the ability to make request/response examples. Let’s take a look at that next.

Request/Response Examples

As we mentioned, the way Postman handles documentation of responses is through examples. You find the ability to do this, right above the “Save” button in the top right corner.

Click on “Examples” and afterward click on the “Add Example” button.

The interface changes a bit as you can see in the image above.

The ability to make a request is now substituted with a name for the example, but we still have our request to the left and response to the right.

If you take a look at the request body, it is the same as we had before, but on the response side, we have some work to do.

First, we need to give a status code. Since it’s a request that creates a book, we need the appropriate status code. If you remember from the chapter about the JSON:API specification, when a resource is created, we respond with a 201 Created status code.

Next up is the body. As stated in the JSON:API specification, we need to return the newly created resource as the primary data of our response document.

Easy enough, we already have that in the requested document, so let’s copy it over. We need to do some editing though. Unless you expressly tell it not

104 PLANNING

to, Laravel includes a created_at and an updated_at attribute to its models. We love that Laravel does that: it has helped us countless times to have these timestamps, so let’s include these as well. Since the resource is created now, we will have to give it an ID as well. This should result in a response document that looks like this:

{

"data": {

"id": "1", "type": "books", "attributes": { "title": "Example book", "description": "This is an example of a book", "publication_year": "2019", "created_at": "2019-01-01", "updated_at": "2019-01-01"

}

}

}

In Postman it should look like the image below.

105 BUILD AN API WITH LARAVEL

Now, let’s take a look at the headers. If you click on the “Header”, you should see an empty list. Here, you should provide the Content-Type as well as the Location for the newly created resource.

By now you must know what the Content-Type should be, but the location is a bit more tricky. Since we don’t have a domain yet, let’s use the example.com domain to emphasize that this is just an example. The value of the Location header would then be:

GET: http://example.com/api/v1/books/1

We use the /api to signal that it’s an API you’re making requests to and the /v1 is our way of telling the version of the API.

106 PLANNING

If you have done it correctly, you should have the same as in the image above. Remember to hit the “Save Example” button.

If you go through “Browse” again to see the result in the documentation, you can see that the response has also been added.

Great. That was an example for the Create Book request, and now let’s make examples for the rest of them.

Examples for all endpoints

Back in Build mode, let’s begin with the Single Book request since we actually have everything needed for this endpoint.

107 BUILD AN API WITH LARAVEL

Single Book

Before clicking away from the Create Book example, copy the contents of the body of the response and then go to the Single Book request.

Before making the example, there is one thing we are missing. Can you guess what that is We need to define one header, namely the Accept header. Remember that the JSON:API specification states that we should include the Accept header with a value of application/vnd.api+json to tell the server that we expect the response to be in this format. Let’s add that to the request.

If done right, you should have what is shown in the image above. Remember to save the request, and now let’s make a new example for this request, using the dropdown above the “Save” button. We don’t have to do anything about the request — we can leave that as it is. We actually only have to fill out the status code, body, and header of the response. Set the status to 200 OK, since we are reading data this time, paste in the contents in the body, and set a header of

108 PLANNING

Content-Type with the value application/vnd.api+json.

If done correctly, when looking at the documentation, you should see that the endpoint is documented like in the image above.

Let’s take a look at All Books next, since we almost have everything for this.

All Books

Here, you should use the same procedure as with Single Book, adding the Accept header to the request and afterward making an example. In the example, the request can be left alone and in the response, the exact same status and header should be used.

Now, you are welcome to come up with the contents of the body yourself, as long as you remember that we are dealing with a collection of books as the primary data this time.

If you need some inspiration, here’s what we have inserted into our example:

{

"data": [

{ "id": "1",

109 BUILD AN API WITH LARAVEL

"type": "books", "attributes": {

"title": "Example book", "description": "This is an example of a book", "publication_year": "2019",

"created_at": "2019-01-01",

"updated_at": "2019-01-01"

}

}, {

"id": "2", "type": "books", "attributes": {

"title": "Example book two", "description": "This is yet another example of a

book", "publication_year": "2019",

"created_at": "2019-01-01",

"updated_at": "2019-01-01"

}

}

]

}

Now, take a look at your documentation using “Browse”. It should look like the image above.

110 PLANNING

Ok, let’s tackle the Update Book request next.

Update Book

We will be taking the same approach as when creating a book. To begin, we will build up the body of the request, then set the correct headers, and save the request. Thereafter, we will be making the example and building up the response.

So let’s start with the request body. Here, we only need to include the attributes we want to update, so for instance, if we only want to update the title, that’s all we need. Let’s do that, and the request document will look like this:

{

"data": {

"id": 1, "type": "books", "attributes": { "title": "Update book title" }

}

}

Remember that we need to include the id and type in the update request and then the attribute object containing the attributes we want to update.

Next, let’s tackle the header. You have most likely set the content to be JSON (application/json) so that it is easier to work with the content, but remember that Postman then sets the Content-Type header as well, so this will have to be corrected. We also need to add the Accept header as well. By now, you should be able to remember what the values must be, so let’s move on to the example, but before you click on example, be sure to copy the contents of the request body.

111 BUILD AN API WITH LARAVEL

Set the status to 200 OK and paste the contents of the request into the body. We need to include the last attributes, which you can find in the Single Book example if you can’t remember them. The reason why we are returning the resource object is that we are planning ahead. The JSON:API specification states that you need to return the resource object if it has an updated_at attribute that will be updated as well. Laravel does that, so we need to return the resource object. To show that the update of the updated_at attribute is happening as well, set the date to be the 2nd of January 2019.

Set the Content-Type header as well and we are done with this request.

If you have done it correctly, it will be like in the image above when looking at your documentation.

We are almost done. We only need the last Delete Book request, so let’s go through that now.

Delete Book

This one is probably the easiest one. We don’t need a request document, and we don’t need to do a detailed response example since you don’t have to respond with any response documents unless you have some meta-data you want to

112 PLANNING

include. In our planning, we don’t have that, so the only thing we need to do is to add the Accept header to the request and make an example where we include the status code 204 No Content. To make it show up in the documentation, go into the response body and make a new line.

That is all the request and examples for the Books resource. Now we just have to repeat the same tasks for the rest of the resources.

The remaining resources

Now it’s time for you to be a little on your own in Postman. For the next resources, you have to create all the requests and define the attributes, examples, and so forth. We are not going to force attributes on you — we want you to think about these yourself. If you still feel a little unsure or just need inspiration, here is a list of attributes we have defined for each resource in our planning phase:

• Authors

• - Name

• - Updated At (Comes from Laravel)

• - Created At (Comes from Laravel)

• Comments

• - Message

• - Updated At (Comes from Laravel)

• - Created At (Comes from Laravel)

• Users

• - Username

• - Name

• - Email

• - Updated At (Comes from Laravel)

• - Created At (Comes from Laravel)

We have kept it pretty simple here, and there are probably many more

113 BUILD AN API WITH LARAVEL

attributes that could be a part of each resource. If you have many more than us, that’s fine. Just don’t include so many that you introduce unnecessary complexity into your application.

If you still find yourself a bit lost, we have an export of our finished collection/documentation in our Github repository — just ignore the relationships and query parameters for now, as we will get into these next.

Documenࢼng Query Parameters

In the part about sorting resources and pagination in the chapter about the JSON:API specification, we learned that this is done through query parameters. It gives us the ability to sort books by their publication year by writing:

GET: /books?sort=publication_year

We need to document this as well. Since we are in the vein of books why don’t we, once again, take a look at our Books resource in Postman.

Sorࢼng

Here, the sorting only really makes sense in the All Books request, since we get a list of books that may need to be sorted.

Select the All Books request in the side-panel. In the main area, in the request part to the left, we see that we are already at the “Params” tab. The way we define query parameters is the same as headers. We have a table where we define the key and give a value. If we want, we can give a description as well. Set the key to sort, the value to attribute, and in the description you write: “Sort books by attributes”. Right next to the key, there’s a checkmark. Remove this, since we don’t want the query parameter to be a part of the endpoint in

114 PLANNING

the documentation, but only inform that it is possible. Save the request and take a look at the documentation.

Now there’s a Params section, informing about the Sort query parameter. An example is often the most efficient means of communicating information, so let’s make a new example that shows how the sort query parameters work.

In the example dropdown, click “Add Example” and name it “All Books Sorted”. In the Params tab, check the checkbox at the sort key and change the value to publication_year. Copy the contents in body from the All Books example and change the publication_year value to 2018 for the first book. Then add the correct status code and header and save.

Make another example, this time for sorting in descending order and name it “All Books Sorted Descending”. Perform the exact same steps as before, but this time the value of the query parameter needs to be -publication_year. After you have copied the contents of the response body and changed the publication_year, the two books need to switch places, so the book with id of value 2 is first in the array.

If you take a look at the documentation now, we have some examples that show both how to use the sort query parameter but also how it works with descending order. There is one last example we need, namely an example showing a comma separated list for sorting by multiple attributes.

115 BUILD AN API WITH LARAVEL

Add a new example and name it “All Books Sorted by Multiple Attributes” and repeat the steps from the previous example. This time for the query parameter write: -publication_year,title. And that’s it. Look at the documentation to see if everything is how it should be.

Paginaࢼon

Documenting pagination for our books takes the same approach as the sort query parameter. It only really makes sense in the All Books request and luckily we only need one example.

Before we can make that example, however, we first need to add pagination query parameter to our All Books request part so that it will show up in our documentation.

Under the sort parameter, add a new parameter with the key page, value 1 and description: “Current pagination page”. Uncheck the checkbox next to page and save the request.

You should see something like in the image above.

Let’s make an example for it. Create a new example and name it “All Books Paginated”. In this new example, check the checkbox next to page, change the value from 1 to 2, and add the following into the response body:

{

"data": [

{ "id": "3", "type": "books", "attributes": { "title": "Example book 3", "description": "This is an example of a book", "publication_year": "2019" }, "relationships": {} },

117 BUILD AN API WITH LARAVEL

{

"id": "4", "type": "books", "attributes": {

"title": "Example book 4",

"description": "This is an example of a book",

"publication_year": "2019" }, "relationships": {}

} ], "links": { "first": "/books?page=1", "last": "/books?page=5", "prev": "/books?page=1", "next": "/books?page=3" }

}

For brevity we have omitted the relationship, since they don’t have anything to do with what we are trying to convey here, namely the new links member with pagination links inside the object. Don’t forget the header and Content-Type and save the example.

Documenࢼng Relaࢼonships

By now, we have been working with our resources and which attributes these should have, as well as sorting and pagination by query parameters. We have even documented these findings. Now, it’s time to do the same with relationships. Here, we will edit the existing resources and add the various resource identifier objects and also, once again, have a look at the included top-level member of our response documents.

We always use the included member by default - remember that this is optional - and have often not supported the feature of the include query parameter. But we want to teach you all we know, so of course we will support it in this book.

118 PLANNING

Adding Relaࢼonships

When we identified our relationships, we made a list of these where we also identified the relationship links based on the conventions from the JSON:API specification.

These are:

• Books and Authors - A many-to-many relationship with endpoints:

• - Self

GET: /books/1/relationships/authors

• - Related

GET: /books/1/authors

And the inverse relationship from authors

• - Self

GET: /authors/1/relationships/books

• - Related

GET: /authors/1/books

• Books and Comments - A one-to-many relationship with endpoints:

• - Self

119 BUILD AN API WITH LARAVEL

GET: /books/1/relationships/comments

• - Related

GET: /books/1/comments

And the inverse relationship from comments

• - Self

GET: /comments/1/relationships/books

• - Related

GET: /comments/1/books

• Comments and Users - A one-to-one relationship with endpoints:

• - Self

GET: /comments/1/relationships/books

• - Related

GET: /comments/1/books

And the inverse relationship from users

120 PLANNING

• - Self

GET: /users/1/relationships/comments

• - Related

GET: /users/1/comments

Let’s use the Books resource again. Here, we need to update our requests in Postman, as well as add new examples, so our documentation reflects what you can include in the requests.

Why don’t we start with the Single Book request first. Returning to Postman, open up the example which right now should have the name Single Book as well. We will change that in a bit, but for now you should add the relationships member to the response body like this:

{

"data": {

"id": "1", "type": "books", "attributes": { "title": "Example book", "description": "This is an example of a book", "publication_year": "2019", "created_at": "2019-01-01", "updated_at": "2019-01-01"

}, "relationships": {

"authors": { "links": { "self": "/books/1/relationships/authors",

121 BUILD AN API WITH LARAVEL

"related": "/books/1/authors"

}, "data": [

{ "id": "1", "type": "authors" }, {

"id": "2",

"type": "authors" }

]

}, "comments": {

"links": { "self": "/books/1/relationships/comments", "related": "/books/1/comments" }, "data": [ { "id": "1", "type": "comments" }, { "id": "2", "type": "comments" }

]

}

}

}

}

Just to give an example for our documentation, we have included two related resources for both Authors and Comments. Save the example and let’s take a look at the documentation for our Books resource and the Single Book request.

The example is now too long to be shown in the documentation, but if you click to expand it, it should reflect the response document given in the example

122 PLANNING

above.

Now that we have the Single Book, we also have the recipe for the changes to All Books. We’ll let you do this on your own, but remember to change the relationships, especially for the comments, so two books don’t share the same comments. If you get stuck, remember that we do have a finished version of the collection/documentation in our Github repository.

For the Create Book and Update Book requests, we need to make examples that show how to make requests that not only creates or updates a resource, but also creates a relationship to another resource. Let’s start with Create Book.

We will only create a book with a relationship to authors. It doesn’t make sense to create a book with a relationship to a comment, since it requires that the comment on the book already exists. Create a new example and name it Create Book with Authors.

Now, to create relationships along with a resource, we need to include the relationship member in the request document. Just like in the response document, this need to be on level with the attributes member. We define the relationship by adding members for the various resources we want to create a relation to, in this case authors. We add a data member or resource linkage inside the authors object where we give resource identifier objects to the specific resources we want a relationship to.

It would look like this:

{

"data": {

"type": "books", "attributes": {

123 BUILD AN API WITH LARAVEL

"title": "Example book", "description": "This is an example of a book", "publication_year": "2019" }, "relationship": { "authors": { "data": [ { "id": "1", "type": "authors" }, { "id": "2", "type": "authors" }

]

}

}

} }

If you have the same as above, you can continue on to the response body. Take a copy of the request body and make the right adjustments, such as adding an id member for the book and adding the links member to each relationship, together with an object containing the self and related links.

That would look like this:

{

"data": {

"id": "1", "type": "books", "attributes": {

"title": "Example book",

"description": "This is an example of a book",

124 PLANNING

"publication_year": "2019", "created_at": "2019-01-01", "updated_at": "2019-01-01"

}, "relationships": {

"authors": { "links": { "self": "/books/1/relationships/authors", "related": "/books/1/authors" }, "data": [ { "id": "1", "type": "authors" }, { "id": "2", "type": "authors" }

]

}

}

}

}

Remember to add the correct status code and headers.

Next up, is the Update Book request. We can follow the same steps as above, but you don’t need to include all of the attributes, only the ones that need to be updated.

Create a new example and name it Update Book with Authors. Copy the request body from the Update Book example and add the relationship to authors with an array of resource identifier objects like this:

125 BUILD AN API WITH LARAVEL

{

"data": {

"id": "1", "type": "books", "attributes": { "title": "Updated title", }, "relationship": { "authors": { "data": [ { "id": "4", "type": "authors" } ]

}

}

} }

Here, we will remove all existing authors from the book and add the author with the id of 4. Just like the Create Book with Authors example, you can copy over the request body to the response body and fill out the relationship links.

It would look like this:

{

"data": {

"id": "1", "type": "books", "attributes": { "title": "Updated title", "description": "This is an example of a book", "publication_year": "2019", "created_at": "2019-01-01", "updated_at": "2019-01-02"

126 PLANNING

}, "relationships": {

"authors": { "links": { "self": "/books/1/relationships/authors", "related": "/books/1/authors" }, "data": [ { "id": "4", "type": "authors" } ]

}

}

}

}

Again, remember the correct status code and header.

Now that we have updated all of our resources to reflect the relationships, it is time to look at the included member and how it works with the include query parameter.

The Include Query Parameter

The include query parameter is actually an optional feature, according to the JSON:API specification. As we mentioned earlier, we usually don’t support this feature, but make use of the included member of our response document where all the relationship are queried and included in the response especially since it’s so easy with Laravel. But, of course, this puts a toll on performance and you could speed up requests by omitting this and letting the consumer decide for themselves. Also, we want to teach you everything we know that’s why we have chosen to go through this as well.

127 BUILD AN API WITH LARAVEL

In terms of documentation, this feature is not that complex since it’s a query parameter like the sort query parameter. But in contrast to the sort query parameter, the include parameter can be used when fetching all resources and a single resource. So let’s document that in Postman now and again, let’s use the Books resource and start in the Single Book request.

Just like when we created the sort query parameter, we need to make a parameter in the request, uncheck it, and afterwards copy it over to new examples where it needs to be checked. Add a new parameter with the key include, value resource and description: “Related resources to be included in the request” and save the request.

Create a new example and name it “Single Book including Comments”. Check the checkbox at the parameter and change the value to comments.

Copy the response body from the first Single Book example and add the included member containing the resource objects of all the comments, which should look like this:

{

"data": {

"id": "1", "type": "books", "attributes": { "title": "Example book", "description": "This is an example of a book", "publication_year": "2019", "created_at": "2019-01-01", "updated_at": "2019-01-01" }, "relationships": { "authors": { "links": { "self": "/books/1/relationships/authors",

128 PLANNING

"related": "/books/1/authors" }, "data": [ { "id": "1", "type": "authors" }, { "id": "2", "type": "authors" }

] }, "comments": { "links": { "self": "/books/1/relationships/comments", "related": "/books/1/comments" }, "data": [ { "id": "1", "type": "comments" }, { "id": "2", "type": "comments" }

]

}

} }, "included": [ { "id": "1", "type": "comments", "attributes": { "message": "Hello world" }, "relationships": { "users": {

129 BUILD AN API WITH LARAVEL

"data": { "id": "1", "type": "users" }

} }, "links": { "self": "/comments/1" } }, { "id": "2", "type": "comments", "attributes": { "message": "Foo bar" }, "relationships": { "users": { "data": { "id": "2", "type": "users" } } }, "links": { "self": "/comments/2" }

}

] }

Remember to add the correct header and Content-Type.

Let’s also make an example for related resources, which in this case is the user that creates each of the comments.

Create a new example and name it “Single Book including Comments and commenting User”. Check the parameter and change the value to com-

130 PLANNING

ments.users. Copy the contents of the response body from the previous example and add the two users’ resource objects to the included array of resource objects, like this:

{

"data": {

"id": "1", "type": "books", "attributes": { "title": "Example book", "description": "This is an example of a book", "publication_year": "2019", "created_at": "2019-01-01", "updated_at": "2019-01-01" }, "relationships": { "authors": { "links": { "self": "/books/1/relationships/authors", "related": "/books/1/authors" }, "data": [ { "id": "1", "type": "authors" }, { "id": "2", "type": "authors" }

] }, "comments": { "links": { "self": "/books/1/relationships/comments", "related": "/books/1/comments" }, "data": [

131 BUILD AN API WITH LARAVEL

{

"id": "1", "type": "comments" }, { "id": "2", "type": "comments" }

]

}

} }, "included": [ { "id": "1", "type": "comments", "attributes": { "message": "Hello world" }, "relationships": { "users": { "data": { "id": "1", "type": "users" } } }, "links": { "self": "/comments/1" } }, { "id": "2", "type": "comments", "attributes": { "message": "Foo bar" }, "relationships": { "users": { "data": {

132 PLANNING

"id": "2", "type": "users"

}

} }, "links": { "self": "/comments/2" } }, { "id": "1", "type": "users", "attributes": { "username": "johndoe", "name": "John Doe", "email": "john@example.com", "created_at": "2019-01-01", "updated_at": "2019-01-01" }, "relationships": { "comments": { "data": { "id": "1", "type": "comments" } } }, "links": { "self": "/users/1" } }, { "id": "2", "type": "users", "attributes": { "username": "janedoe", "name": "Jane Doe", "email": "jane@example.com", "created_at": "2019-01-01", "updated_at": "2019-01-01"

133 BUILD AN API WITH LARAVEL

}, "relationships": { "comments": { "data": { "id": "2", "type": "comments" } } }, "links": { "self": "/users/2" }

}

] }

Phew, that was quite an amount of data for a book like this! Don’t forget the headers and Content-Type.

We need one more example though: one showing a comma separated list of related resources.

Make yet another example and name it “Single Book including Authors and Comments”. Check the checkmark at the parameter and change the value to authors,comments.

Copy the contents of the resource body from the last example and change out the users to authors. This time you should try to edit the data yourself — if you have forgotten what the author’s resource object looks like, you can copy it from your Author resources Single Author example. Don’t forget the header and Content-Type.

## Summary

In this chapter we have been through a lot. First, we started the planning of our project. When developing an API, we no longer have to think about UI/UX and can focus more on our data.

We began our planning phase by identifying our resources and the relationships between these resources. We saw how we can conveniently think of our resources like a mapping of our models and database table.

We learned about Postman and how we can use it to document our API and how it can help us think about our resource attributes and relationships. By documenting our API early, we forced ourselves to work with the JSON:API specification and our applications data.

Sometimes, it’s tedious work, plotting all of these examples into Postman, but if you have been taking some notes, you already have a good idea of where the more complex parts of the implementation lie and where the easiest parts are.

We learned a bit more about the included top-level member of our response documents, and how we can leverage the include query parameter to tell our API which related resources we want included in the response.

We hope that you finished your documentation and explored Postman a little more. A big win, which we also touched upon in this chapter, is that when the documentation is done, a mock server can be set up for the frontend people or other consumers of our API, which can relieve the pressure on our shoulders as backend developers.

Next up, we will begin building our API. We won’t be leaving Postman yet, but we will finally start to do some coding, and isn’t that why we are all here anyway? Great! Let’s get on with it!

