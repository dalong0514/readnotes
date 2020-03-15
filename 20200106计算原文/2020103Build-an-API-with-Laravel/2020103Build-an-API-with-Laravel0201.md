# The JSON:API specification

Let’s have a look at the JSON:API specification — a specification for building APIs in JSON. A specification like this can help us build our API, following a set of rules that makes it easier for ourselves, and especially others, who will be consuming our API in the future.

We will be looking at the specification and how it fits into the features Laravel offers, and how it can be a great tool to master, and make it possible for you to actually plan out your API with more confidence.

Firstly, we will be looking at a case for this book to have something to work from: a common ground which makes it a bit easier to put things into perspective. This way we can give examples when looking at the JSON:API specification with context and in later chapters show you how we go from planning all the way to implementation.

Let’s have a look at the case.

## 01. The case

As mentioned earlier, we will be using a case to establish a common ground. It makes it easier for us to give examples in a context you understand, and lets us reuse this context for planning and later implementation. By having a case that simulates a real life example, it might be easier for you to understand the concepts we will present to you and apply them into your own projects in the future. We all learn differently, but it is our experience that having a case and a context makes it easier to see the concepts applied and learn how to apply them yourself.

So without further ado, let’s get into the case:

Anna’s Bookstore has existed since the early 90s where it opened as a small cornershop in the city. It isn’t a fancy place — the floor, bookshelves and furniture make it seem a bit like your grandma’s place, but it’s cosy, welcoming and the perfect combination of a bookstore and coffee shop, where you will feel right at home. Customers come back for Anna’s personality, which is reflected in every little thing in the store, and especially the selection of books. It’s not the selection of books you’ll find in every store; these are hand-picked by Anna herself. She’ll often offer customers a cup of coffee and discuss a book, or the work of an author, when there isn’t anything to do at the cash register. You can feel that both literature and people are her passion.

As the years go by, new stores start emerging and Anna gets a lot more competition, especially from modern bookstores, where people can find and buy books faster. This isn’t really Anna’s cup of tea, and to compete, she would have to change everything about her store. She’s beginning to think about closing the store, until a day when her nephew visits her. When they talk about the store, the nephew asks: “Why don’t you go online, so you can keep your store as it is and sell to people at home or in a hurry?”. Anna must admit that it is a good idea. Over the years, she has started to order books online herself and is quite pleased with the experience. The nephew then continues: “You don’t have to have a huge selection of the books, why not cater to a niche and sell a curated selection of books, like you do in your store now? You know people always praise you for having so many hidden gems.” Anna is convinced. This is something she can see herself in, she can still use her expertise, and people can still buy a bit of Anna’s personality in the selection of her books.

Other than being able to sell books and being able to keep stock of her books, Anna wants to be able to present these books through authors. Anna has a bunch of authors that she can vouch for, who always publish good work, a key part of her having so many hidden gems.

Sometimes, Anna finds books by reading comments that other people have left on the online bookstores. She loves the helpful tips people give in the comments and it reminds her of the discussions she has been a part of in her own bookstore. She would like something like this in her online bookstore as well.

There are a few things to take note of here. To some, the case might sound really simple and to others, it might seem daunting. But fear not, we won’t be building the entire solution for Anna. Instead, we will pick out parts of the online bookstore that makes sense in terms of an API, and not the entire purchase flow etc. Keep in mind that we have written this case to communicate the concepts about building an API, as easy as possible, and there is more than enough in the part about handling books and authors to do that.

Now that we know more about the case and what we need to build, we could go straight to the planning, but let’s hold that thought and take a closer look at the JSON:API specification, and learn a bit more about the protocols that will be the foundation of how we communicate with our API.

## 02. JSON:API specification

When developing software, there are a lot of decisions to make about how to design the software in the best way — from how to design your code to the application architecture, and all the way up to the visual representation of your application on screen. With APIs this isn’t any different. Up until 2013, where the first draft of the JSON:API specification was made, there weren’t any approaches to standardization of JSON API interactions.

Before adhering to the JSON:API, we at Wacky Studio even made our APIs in our own way, the way we thought was best. We drew inspiration from APIs of the services we used and made our decisions based on how they were implementing their APIs.

1『Wacky Studio 是作者他们的公司。』

That was a very bad idea because:

• They were also in a phase of learning how to write a good API for their services.

• None of them were following the same conventions.

• Most of them had an API design that meant you had to make a lot of requests for data.

The worst of it all was when we had to consume our own API on the frontend. Because of the lack of conventions, we had to constantly go back and forth to get the correct endpoints, to see what data each request should contain and to see what would be returned from the server.

And every time we started a new project, we ended up writing all the code for communication with the server, again and again, because of inconsistency.

You see, it’s not the development of the API on the backend that takes time and causes pain. The pain is mostly felt when you have to work with the API on the frontend, or even worse when other people or companies are working with your API. Without strict conventions, you not only have to write documentation that shows what your API can do, but you also end up teaching how to use the API.

This is where following a specification like the JSON:API specification shows its worth. How to use it is already documented and as long as you follow the specification, anybody who knows how to work with the JSON:API specification, knows how to work with your API. Of course, they won’t know what your API can do — you will still have to tell them that — but how to communicate with your server through your API, will never be a problem for them.

Even better, when following the conventions of the JSON:API specification, you have a strict protocol that never changes from application to application. This means that you can extract the whole client-server communication part of your frontend application and reuse it from application to application. You won’t have to write the same tedious boilerplate code over and over again, and you can focus on building the functionality of your frontend app instead. The JSON:API specification even lists available implementations, which includes implementations made for a lot of languages like Javascript as well as frameworks like VueJS and React.

The JSON:API specification was drafted in 2013 and had the first final v1.0 ready in 2015, where it has been used ever since. At the time of writing, a new version is about to be released, but as stated in the specification, the new version will always be backward compatible, using a “never remove - only add” strategy. So you won’t end up like us, where your inspiration is suddenly drastically changed. When implementing the JSON:API specification, you are ensured that people will always be able to use it, no matter which version of the specification they have learned and/or are using.

As we see it, the JSON:API specification is a great approach to standardization of APIs and throughout this book, we will dive further into it and show you how to build an API in Laravel using it. Before we get ahead of ourselves, let’s commence by looking at the fundamentals of the specification.

### 1. Client / Server Responsibilities

When you adopt the JSON:API specification, the first thing you have to look at are the headers sent in your request and responses. As a client, you have to send your request with:

    Accept: application/vnd.api+json

And

    Content-Type: application/vnd.api+json

These headers tell the server that what you’re sending lives up to the protocol given in the JSON:API specification, and also that you expect to receive data in the response that adhere to that same protocol.

As a server, you have to deliver your response with:

    Content-Type: application/vnd.api+json

to tell the client that what you’re sending lives up to the protocol given in the JSON:API specification.

### 2. Endpoints

Though the specification provides a strict protocol for how requests and responses are structured, it only gives a few recommendations about how to form your endpoints. In this section, we will have a look at the recommendations from the JSON:API specification and give some of our recommendations as well.

It isn’t hard to define endpoints, since you are already used to it by the routes you have defined in your existing Laravel applications. The thing that can be hard is making sure that you are consistent.

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

### 4. Before we continue

In the upcoming sections, we will take a deeper look at the JSON:API specification. We will touch upon conventions that the JSON:API specification states as conventions that MUST be followed and conventions the specification states as conventions that MAY be followed. However, we recommend that you follow the conventions we have picked out, whether the specification states that they MUST or MAY be implemented. We will touch upon most of the conventions given in the specification, but there are a few that we haven’t had any use for and feel that they cover more edge cases.

### 5. Document structure

Let’s look at the document structure of the data for both JSON:API request and responses. The document describes how your JSON data should be formed, how members should be named, where these should be placed, and so forth.

#### 01. Top-level

Here, the JSON:API specification states that there must be a JSON object at the root of the document, representing the top-level. In the top-level of the document, there must be at least one of the following members:

• data - which is the most important member that contains the primary data of the document.

• errors - which is a member that contains all error objects.

• included - which is a member that contains all resource objects that are related to the primary data and/or related to each other. We will touch more on this when we get to the section about resource objects and relationships.

• jsonapi - which is a member that contains the server’s implementation of the JSON:API specification.

• meta - which is a member that contains all non-standard meta information.

Note that it is very important that the data and errors member never coexist in the same document. The data member should only be used in successful request and responses, where the errors member should only be used whenever there is an unsuccessful request or response. By separating these, you have a clear convention that states where to look for either data or the errors that might occur. Now that we know what the top-level structure should be, let’s take a look at what our primary data will be and also how to structure that.

#### 02. Primary data and Resource objects

In the section about naming conventions, we talked about how convenient it is to be thinking of our Laravel models as resources since these represent the rows of data in our database and data that we most likely will share across our APIs.

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

#### 03. Member names

The JSON:API has a clear naming convention when it comes to member names, where all member names must be treated as case sensitive by both client and servers. Other than that, there are some conditions that the member names must also follow:

1. Member names must contain at least one character.

2. Member names must contain only allowed characters.

3. Member names must start and end with globally allowed characters.

The globally allowed characters are:

• a-z

• A-Z

• 0-9

The characters that are allowed except for the beginning and end of a member name are:

• -

• _

As an example, it is ok with a member name like this:

```
{
    "member_name": "content" 
}
```

But it is not ok with a member name like this:

```
{
    "_member_name_": "content" 
}
```

The above example is pretty trivial. Who would do that, right? The important thing to remember here is to have a letter in the beginning and the end and you’re home safe. 

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

#### 04. Aributes

Now that we have a naming convention for our member names, we can continue to attributes. Attributes on a resource object are just like the attributes on your model in a Laravel Application. These are data like the title of a book, the name of an author, and so forth. The JSON:API specification specifies that on a resource object, the attributes member should be an object. Any member inside this object can be whatever data that represents the object, but must never be a relationship. For relationships, we use a dedicated member in the resource object, which we will look at shortly. To make an example, let’s look at a single book again:

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

Here, you see the definition of the attributes member as an object containing two members, namely title and publication_year. You also see how the naming convention of snake casing takes effect. As mentioned earlier, the attributes member can contain any information about the resource object, but cannot contain relationships or a member called relationships.

Another rule is that the attributes member can never contain an id or type member, since these are reserved on the root of the resource object. But how do we define relationships then? Let’s take a look at that next.

#### 05. Relationships

When it comes to data in an application, these are often related to one another. When building applications in Laravel, we are used to defining models as objects in real life and as such, these have different relations to one another:

A car belongs to a brand, a bus can have many passengers, a book can have many authors, and an author can have written many books.

Do you see how everything connects? Chances are that you have already written something like the sentences we just presented, since Laravel uses most of the wording in the relationships you define in models.

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

By declaring a relationship method on our model, we can fetch the brand of our car very easily, now that we have told Laravel about the relationship. But how do you tell about relationships in your APIs and how do you convey enough information, so that your consumers can easily get the data they want? Relationships in the JSON:API specification is defined as the relationships member.

Like the id, type and attributes members, it should be placed at the root of the resources object and be defined as an object like this:

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

```
{

"data": {
"id": "1", "type": "books", "attributes": { "title": "Build an API with Laravel", "publication_year": "2019" }, "relationships": { "comments": { "links": { "self": "http://example.com/books/1/relationships/comments ", "related": "http://example.com/books/1/comments" }, "data": [ { "id": "16", "type": "comments" }, { "id": "28", "type": "comments" }
]
}
}
} }
```

The way the data attribute contains resource identifier objects is just like the primary data’s data member, which holds either an object for a single resource or an array for a collection of resources.

Ok, that was a bunch of rules at once. Let’s recap on how to define a relationship. We make an object as the relationships member. Each member inside relationships defines each related resource. In the examples given above, the relationship is between books, authors and comments. All of those combined would look like this:

```
{

"data": {

"id": "1", "type": "books", "attributes": { "title": "Build an API with Laravel", "publication_year": "2019" }, "relationships": { "author": { "links": { "self": "http://example.com/books/1/relationships/authors ", "related": "http://example.com/books/1/authors" }, "data": { "id": "5", "type": "authors" } }, "comments": { "links": { "self": "http://example.com/books/1/relationships/comments ", "related": "http://example.com/books/1/comments" }, "data": [ { "id": "16", "type": "comments" }, { "id": "28", "type": "comments" }
]
}
}
} }
```

Inside each relationship, we have at least one of the members: 1) inks. 2) data. 3) meta.

In our case, we have both links and data, which we recommend that you do as well. The links members give us a consistent way of accessing either the relationship between the resources or the related resource object. The data members give us either a resource identifier object or a collection of resources.

We now know how to define relationships, we even know how to provide links for manipulating relationships and how to fetch related resources. If we want the comments for the book, we can simply make a request to the link given in the related member and a response containing all the resource objects will be returned.

1『这张完整的 json 数据结构好好研究琢磨。』

Right now, the data member of the relationships seems a bit redundant, since it only contains id and type member instead of an entire resource object, but let’s look further into this in the next section and it will make more sense.

### 6. Compound Documents

We have just looked at the relationships member and what kind of members this should contain. We left with some confusion about the data member inside the relationships object. To understand this part, we need to revisit the top-level of our document, more specifically the included member. We only touched upon this briefly in the section about Top-level, so let’s have a better look at this.

When building an API or an application for that matter, you have to make some thoughts about optimization and make sure your application performs as intended. One optimization could be to reduce the number of HTTP requests as much as possible. One way to do this is to use the included member. The reason for this is that it makes it possible for you to include the related resources of the fetched resource, which will then be the resources defined in the data member in the relationships object. Instead of having to make a new request for the related resources, they can just be included in the current response.

In this case, the resource objects sent in the included member will correspond to the resource identifier objects given in the relationships’ data member. Let’s build upon the previous examples to give a better idea of this:

```
{

"data": {

"id": "1", "type": "books", "attributes": { "title": "Build an API with Laravel", "publication_year": "2019" }, "relationships": { "author": { "links": { "self": "http://example.com/books/1/relationships/authors ", "related": "http://example.com/books/1/authors" }, "data": { "id": "5","type": "authors"

} }, "comments": { "links": { "self": "http://example.com/books/1/relationships/comments ", "related": "http://example.com/books/1/comments" }, "data": [ { "id": "16", "type": "comments" }, { "id": "28", "type": "comments" }

]

}

} }, "included": [ { "id": "5", "type": "authors", "attributes": { "name": "Wacky Studio" } }, { "id": "16", "type": "comments", "attributes": { "body": "Hello world" } }, { "id": "28", "type": "comments","attributes": { "body": "Foo bar" }

}

] }
```

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

### 7. Request and responses

It’s time to look at how we should make our request and responses according to the JSON:API specification. We know what to send and what we can expect to receive, but we don’t know how to request it or how these should be sent with a response yet. Of course, there are conventions and we will adhere to them. Let’s take a closer look.

#### 01. Requests

All requests to get data from our API must be done with a GET request. Remember the previous chapter in the section about REST and HTTP verbs, the GET request is for reading data and the same goes for the JSON:API specification. Nothing has changed here.

Some interesting conventions the JSON:API specification brings along for requests is the ability for sorting and pagination of collection data. These are only optional conventions, but we are mentioning them because we have had great use of these. There are more conventions, but these are outside of the scope of this book.

Now, let’s first take a closer look at sorting.

#### Sorting

Sorting data is a great feature to have in an API. Think about sorting just like ORDER BY in your database. You get the ability to sort your data based on member names in a more dynamic way, instead of being limited by the way the API developer may have thought was the best way to sort the data.

Sorting data is done via a query parameter. If you are unsure what a query parameter is, it is a convention in HTTP you use to send along parameters for a request, as a part of the URL like this:

    GET: http://example.com/cars?color=blue

Here, the parameter we are sending along is color with a value of blue. The query parameter used by the sort feature is the sort parameter.

The value of the parameter is the member name of the attribute you want to sort by. It would look something like this:

    GET: /books?sort=title

If you want to support multiple sort fields, these should be separated by a comma like this:

    GET: /books?sort=title, publication_date

When ordering a database query by a column name, we are able to tell if the ordering should be done in ascending order or descending order. The same thing goes for sorting a collection, according to the JSON:API specification. Here, a sorting is always done in ascending order unless you prefix a sort field with a minus, in which case it will be sorted in descending order. It would look something like this:

    GET: /authors?sort=-age

Here, you will get the oldest authors first, descending until the youngest author in the collection.

#### Pagination

Pagination is another feature that can have great benefits, especially if you have large sets of data that can be quite a strain on the system to query. You can paginate the results and do the queries in smaller chunks, letting the API consumer do the work of progressing through the pagination. The way pagination is done in the JSON:API specification is through a links object in the root of the response document. The links object must have the following members used for pagination links:

• first - which is the first page of data.

• last - which is the last page of data.

• prev - which is the previous page of data.

• next - which is the next page of data.

The links object in the document would look something like this:

```
{

"data": [ { "id": "4", "type": "books", "attributes": { "title": "Lorem Ipsum" } }, { "id": "5", "type": "books", "attributes": { "title": "Lorem Ipsum" } }, { "id": "6", "type": "books", "attributes": { "title": "Lorem Ipsum" } }, ], "links": { "first": "http://example.com/books?page=1", "last": "http://example.com/books?page=5", "prev": "http://example.com/books?page=1", "next": "http://example.com/books?page=3" } }
```

In the example, you can see a collection of books and in the bottom of the response document you see the links member with the four members of a pagination link object. Can you guess which page we are on? Correct! We are on page two! Had we been on the first page, the JSON:API specification actually requires us to omit or set a null value for the links that are unavailable, which in that case would be the prev link, since there is no previous page, when being on the first page. Just to demonstrate, here is an example of that scenario:

```
{

"data": [ { "id": "1", "type": "books", "attributes": { "title": "Lorem Ipsum" } }, { "id": "2", "type": "books", "attributes": { "title": "Lorem Ipsum" } }, { "id": "3", "type": "books", "attributes": { "title": "Lorem Ipsum" } }, ], "links": { "first": "http://example.com/books?page=1", "last": "http://example.com/books?page=5", "prev": null, "next": "http://example.com/books?page=2" } }
```

You see how a null value is provided for the prev member to indicate that it is unavailable.

The JSON:API specification does not have any conventions when it comes to query parameters signifying which page in the pagination we are currently on. However, they state that the page query parameter can be used for this and we will recommend that as well. The good thing about this is that it’s then possible to deep link into a page of data using the page query parameter. We will support this in our API as well.

Now, we know how to make a request for data and even how we can sort or paginate data provided in collections. It is time to look at responses and the conventions from the JSON:API specification we must follow.

#### 02. Responses

It’s time to look at the server side and which convention it must adhere to when sending responses to the client. Here, we will revisit HTTP verbs and status codes as well as look at conventions that must be followed to keep your API consistent. The first rule we will look at is making GET requests for data or fetching data, as the JSON:API specification calls it.

#### Response guarantees

Here, the server must always support getting resource data and or relationship data for all URLs that are provided in a response. The URLs we are talking about are the URLs provided in a relationship for a resource object. It is the links given in the links object of the relationship object, more specifically the self and related links. It should always be possible to get data through these links, otherwise we are breaking the conventions from the specification. Also, it would not make a lot of sense if links we provide from the API does not work. It would lead to a lot of frustration for the consumers of the API and that’s not what we want.

#### Resource Responses

When we make requests to a server for a specific resource or collection, it must always return a status code 200 OK.







Referring back to the former chapter, we talked about how the 200 status code is the most common, which tells the client that the entire request was successful. When making such a response, the server must also ensure to send the requested resource or resources in the response documents primary data. As covered in the section about Primary data and Resource objects, the server must ensure that the primary data for a response document is either a single resource or a collection of resources.

Here’s an example of a response document for a request for a single resource:

```
{

"data": {

"id": "1", "type": "books", "attributes": { "title": "Lorem ipsum" }

} }
```

Here’s an example of a response document for a request for a collection of resources:

```
{

"data": [

{ "id": "1",

"type": "books", "attributes": { "title": "Lorem ipsum" } }, { "id": "2", "type": "books", "attributes": { "title": "Lorem ipsum" }

}

] }
```

If the single resource cannot be found, the primary data would have to be null. Take a look at this example with a request to the following resource:

GET: /books/1

```
{

"data": null }
```

Here, the resource with an id of the value 1 does not exist. This, however, is only a response you should use if the request warrants a 200 OK response. The JSON:API specification unfortunately doesn’t give a concrete example of this. We’re using a 404 Not Found response for this scenario since it gives a clear message about the resource not being found.

If a collection of resources cannot be found, the primary data would still have to be an array, but an empty array though like this:

```
{

"data": [] }
```

Where a request for a single, not existing resource, should trigger an error since you are trying to access something that does not exist, a collection will always exist. A collection is allowed to be empty since this can be filled with resources later on when they are being created.

#### Relationship Responses

Relationship responses follow some of the same conventions as Resource responses. Remember though that there are two types of links in a relationship:

• self - Which is a link to the relationship itself

• related - Which is a link to the related resource

Here, the link for the related member would give a response document of a resource, since you are requesting the related resource or collection of resources, depending on the relationship.

For the self member, it’s a little different. Here, a request to the self link will respond with a response document, where the primary data would be the resource identifier object. Here is an example of a book resource with a relationship to an author. The relationship in this context is one-to-one, meaning that a book can only have one author.

{

"data": {

"id": "1", "type": "books", "attributes": {

"title": "Lorem ipsum" }, "relationships": { "author": { "links": { "self": "/books/1/relationships/authors", "related": "/books/1/authors" }, "data": { "id": "1", "type": "authors" }

}

}

} }

The URL for the self member is the following, and a request for this endpoint would return a response document with the primary data being the resource identifier object.

GET: /books/1/relationships/authors

So a request to the URL would be something like this:

{

"data": { "id": "1", "type": "authors" } }

Notice how the primary data has the same structure as the data of the relationship of the previous example? This is because a request to relationship endpoint returns resource identifier objects instead of resource objects.

For a one-to-many scenario, where a book can have many authors, the response document would contain the following:

{

"data": [

{ "id": "1", "type": "authors" }, {

"id": "2",

"type": "authors" }

] }

Even though two resources can have a defined relationship, it’s not always a guarantee that they have a relation at the moment. In this case, we follow the same conventions as with resources.

In the case of a one-to-one relation, a request to the self link would give a response document like this:

{

"data": null }

In the case of a one-to-many relation, a request to the self link would give a response document like this:

{

"data": [] }

And the pattern continues.

We know the conventions for requests and responses to get data for both resources and relationships. Now, it’s time to look at how to create or modify data.

### 8. Creating or modifying data

As an interface for your application, an API can give your consumers the ability to create or modify data too. APIs for services like Dropbox or Google give the consumer the ability to add data into their services. This can be data like files, documents and much more. Unless you are writing an API for a service that only provides readable data, like a weather service, you most likely would like a consistent way to add data to your application through your API.

Once more, we will be looking at HTTP verbs covered earlier in this book, as well as status codes required by the JSON:API specification.

Creating

As mentioned earlier in this book, we use the POST HTTP verb to post data to our APIs. This is not any different with the JSON:API specification. The thing that does matter is the request document sent to the server.

In this regard, we should follow the convention we’ve been through earlier about resource objects and relationships. A request to create a new book would

look something like this with a request to the following endpoint

POST: /books

{

"data": {

"type": "books", "attributes": { "title": "Build an API with Laravel", "summary": "Learn how to build an API using the Laravel Framework", "publication_year": "2019" }

} }

The primary data in this request document is a single resource object that describes the new book to be created. Note that in contrast to the response document, we do not include the id member. The JSON:API specification states that you can do that, but we recommend you don’t, unless you have a very specific scenario where it’s needed. It would be better to let the server and backend take care of this, especially if you are using incremental IDs, but even with UUIDs, it’s better to let the server take care of the generation of these. The way we see it, it is a concern that should not be placed on the client side.

When creating a resource, you can also define a relationship. Let’s see how that looks, using that same example from before with this request:

POST: /books

{

"data": { "type": "books", "attributes": { "title": "Build an API with Laravel", "summary": "Learn how to build an API using the Laravel Framework", "publication_year": "2019" } }, "relationships": { "authors": { "data": { "type": "authors", "id": "1" } }

} }

Above, you can see how we reuse the convention about relationships. We give a resource identifier object through the data member and the server will take care of the rest.

The example given here is of a one-to-one relationship but of course, you can also create a relationship in the case of a to-many relationship.

That would look like this, again with this request:

POST: /books

{

"data": { "type": "books", "attributes": { "title": "Build an API with Laravel", "summary": "Learn how to build an API using the Laravel Framework", "publication_year": "2019" } }, "relationships": { "authors": { "data": [ { "type": "authors", "id": "1" }, { "type": "authors", "id": "2" }, { "type": "authors", "id": "3" }

]

}

} }

As shown in the example, you give a collection of resource identifier objects in the data member instead.

Creaࢼng Relaࢼonships

If you recall the relationship links we covered earlier when talking about relationships between resource objects, the endpoint for such a relationship link could look like this:

GET: /books/1/relationships/authors

You can also create, modify or delete relationships by sending a request to these endpoints, where the only difference is that the primary data of your request document becomes the new resource identifier object instead.

As an example, we can create a new relationship between a book and an author like this with a request to the relationship endpoint:

POST: /books/1/relationships/authors

{

"data": { "type": "authors", "id": "1" }

}

As you can see, it is far less data we need to provide as the request document’s primary data. In fact, it’s only the resource identifier object we need to give. The rest of the information about which book and so forth is given in the endpoint.

The same concept works for to-many relationships with a request to the same endpoint:

The endpoint is reused since it’s still a relationship between a book and authors.

If a request to create a relationship that already exists occurs, the server should ignore the new request and keep the relationship as it was before.

Status Codes

When creating a resource, the server must respond with a 201 Created status code. Remember from the Status Codes section in the first chapter, how this status code is used to tell the client that one or more resources have been created. The JSON:API specification follows that same convention. The primary data of the response document must also contain the newly created resource objects as well as a Location header that provides the location of the new resource.

If a request to create a new resource is unsupported, the server should respond with a 403 Forbidden status code.

Now that we know how to create resources according to the JSON:API specification, how do we then modify these data? We will cover that in the next section.

Updaࢼng

As mentioned in the section about HTTP verbs, there are two methods for updating resources. PUT will replace all data in the resource whereas PATCH is only used for updating specific attributes.

The JSON:API specification specifies that the PATCH verb should be used to updating resources, even if all the attributes are updated. Though a request doesn’t have to include all the attributes of a resource, the server would have to interpret the missing attributes.

Let’s take a look at how to make a request to the update endpoint:

PATCH: /books/1

{

"data": {

"id": "1", "type": "books", "attributes": {

"title": "Hello world",

"summary": "This book is about hello world." }

} }

If you take a look at this example and the examples of how to create a book, do

60 THE JSON:API SPECIFICATION

we send the exact same attributes? No, we are missing the publication_year attribute in the resource object. The server would then have the responsibility to interpret this resource object, find the existing one, and update only the attributes given here.

When updating relationships, some of the same concepts repeat.

Just like with creation of resources, updating a relationship can be done through the relationships member on the root of the request document. Like with attributes, where the server has to interpret which attributes you wish to update, the same goes for the relationships given in the relationships object. Only the relationships mentioned are the ones getting updated. Let’s look at an example again with a request to the same endpoint:

PATCH: /books/1

{

"data": { "id": "1", "type": "books" }, "relationships": { "authors": { "data": { "type": "authors", "id": "2" } }

}

}

Here, the relationship to authors is being updated. In this case, it’s a one-to-

61 BUILD AN API WITH LARAVEL

one so the relationship to the author before is being changed to a new author with the id of 2. Just like when creating relationships, you give a resource identifier object and the server will take care of the rest.

And as with creating a resource, the way to update relationships with a tomany relation you give a collection of resource identifier objects, like this with a request to the same endpoint:

PATCH: /books/1

{

"data": { "id": "1", "type": "books" }, "relationships": { "authors": { "data": [ { "type": "authors", "id": "2" }, { "type": "authors", "id": "4" }, { "type": "authors", "id": "7" }

]

}

}

}

In the example above, we give an array of resource identifier objects that we want to update as the new related resource. It is important to note that in this case the relationship to any earlier resources will be removed and relations to the given resources will be made instead.

You can think of this kind of update as the sync method on Laravel Eloquent’s many-to-many relationships. Here, you give the sync method an array of IDs that you want to associate, and all the IDs not in that array that may already be associated, will be removed.

As mentioned in the creation of resources, relationship links can also be used to create, modify or delete relationship between resources. Here’s an example with a request to update the author of a book, using the following relationship endpoint:

PATCH: /books/1/relationships/authors

{

"data": { "type": "authors", "id": "1" } }

As with relationships defined through resource objects, updating a relationship through relationship links also replaces the relationship before. You could go and delete a relationship by making the following request to the same endpoint as before:

PATCH: /books/1/relationships/author

{

"data": null }

Now, the old relationship will be removed and since an empty relationship has been given, there is nothing new to save instead.

Again, the examples have been on a one-to-one relationship, but the concepts are the same for to-many relationships. A request to update authors as a many-to-many relationship would be like this, with a request to that same endpoint:

PATCH: /books/1/relationships/authors

And just like with the single resource object, where a request document with the primary data set as null clears a relationship, an empty array clears a to-many relationship like this:

{

"data": [] }

Status Codes

When updating a resource, the server must send back either a 200 OK status code or a 204 No Content status code in case of an update where nothing else than the attributes provided in the request document was updated.

In an attempt to update a resource that does not exist, the server should send back a response with a 404 Not Found status code to indicate that the resource is not found.

Deleࢼng

Things are moving fast. We now know how to both create and update resources and relationships. We only need to know about deletion, so we are almost done.

Just like requests for creating or modifying a resource, there is a dedicated HTTP verb for deletion of a resource. If you look back to the section about HTTP verbs, we discussed the DELETE verb and that it’s used to tell the server that we want to delete a resource. The JSON:API specification uses the same

HTTP verb for deletion of resources.

To delete a resource, you don’t need a request document since the HTTP verb says it all — at least when it comes to deletion of a resource. Here, it is enough to send a request to an endpoint for a specific resource. For example, imagine that we want to delete the book of ID 1. This can be done with a request like this:

DELETE: /books/1

The same goes for relationships. If you make a DELETE request to a relationship endpoint, the server must delete the relationship between the specified resources. Say, for instance, we want to remove an author from a book. We can just send a request to the endpoint like this:

DELETE: /books/1/relationships/authors

In case of a to-many relationship, you can specify which resources you no longer want to have a relation through a request document, where the primary data is a collection of resource identifier objects. Just like when we want to create or modify a relationship through relationship links. Say we have a book with five authors and we want to remove three of them. This can be done so with a request to the following endpoint:

Now. the relationship between the book and the three authors mentioned in the request document will be deleted, while the rest will remain.

This is actually all there is to requesting, creating, modifying and deleting data, which is enough for us to work with our server with conventions that ensure a consistent communication and data exchange. There is one thing we are missing though. What do we do when an error sneaks in and how do we respond to that?

Errors

It’s time to take a look at errors. Let’s face it, no matter how great of an application you build, errors will always be a part of it. Some are intentional, like validation rules that are not met, and some are not. In both cases, it’s crucial that they are handled in a consistent way, so both you and the consumer of your API know what went wrong.

To start this section, we will take a look back at the top-level of our response

document. If you recall, a document must contain at least one of the following members:

• data

• errors

• meta

A rule we covered earlier was that the data and error members must never coexist in the same document. So from now on, whenever we talk about errors, we will never include the data member in our response document.

The errors member, however, will be an array containing error objects that describe errors of the request made to the server like this:

{

"errors": [] }

We will take a look at error objects in a moment, but one thing we must cover is how the JSON:API specification states which error status codes should be used.

When an error occurs in your application, you as the developer can decide whether or not the application should continue to try to fulfill the request or if it should just fail and stop.

In the case of a fail and stop solution, you should use the appropriate status code. When we looked at how to get, create, modify or delete resources and relationships, we talked about the status codes that should be used.

If you choose to let your application continue trying to fulfill the request, there may be multiple errors that can happen in that single request. In that case, a

68 THE JSON:API SPECIFICATION

more general status code should be used.

• In the case of a 4XX category, error use a 400 Bad Request status code

• In the case of a 5XX category, error use a 500 Internal Server Error status code

Error Objects

Error objects are used to further specify what went wrong when trying to fulfill the request. The JSON:API specification does not have a strict protocol for how this object should be constructed, but a couple of optional members you can include. We have concluded that the following are useful to have in an error document and would recommend that you use these.

• title - which should contain a short human-readable summary of the problem.

• detail - which should contain a human-readable explanation of the problem.

• source - which should contain an object containing references to the source of the error.

The source member is a bit special here, since the JSON:API specification recommends that you use an object containing a JSON pointer member. A JSON pointer is a string syntax that can point to another value in a JSON document.

If you have the following JSON document:

{

"foo": "bar", "baz": [10,20] }

A JSON pointer described like this, /foo would then point to the value bar, where a JSON pointer like this, /baz/0 would point to the value 10 and a JSON pointer like this, /baz/1 would point to 20.

You can think of JSON pointer like the dot notations Laravel provides when you, for instance, are accessing values in your config. Here, you are able to write like this:

<?php

// Get the application name from config

$name = config('app.name');

This will give you the application name defined in the app.php config file. Instead of a dot notation for separating children, a slash notation is used in JSON pointers.

Now that we know about JSON pointers, let’s look at how an error object could look like:

{

"errors": [

{ "title": "Validation error", "source": { "pointer": "/data/attributes/name" }, "detail": "The name field is required."

}

] }

In this example, we are getting a validation error in our application like the title

70 THE JSON:API SPECIFICATION

member describes. The source object contains a JSON pointer to an attribute in the response document sent to the server. Here, it’s the name attribute that might be empty, based on the description given in the detail member.

How would it look if we had more than one error? Right out of the box, Laravel won’t continue to process a request, whenever an error occurs. It will just throw an exception and stop the execution. When handling validation though, it is possible that more than one field would fail and here you would get multiple errors returned. That would look something like this:

{

"errors": [

{ "title": "Validation error", "source": { "pointer": "/data/attributes/name" }, "detail": "The name field is required."

}, { "title": "Validation error", "source": { "pointer": "/data/attributes/email" }, "detail": "The email must be a valid email address." }, { "title": "Validation error", "source": { "pointer": "/data/attributes/age" }, "detail": "The :attribute must be a number."

}

] }

As you can see, there’s an error for each field that did not pass the validation. Although the JSON:API specification states that you should give a more general status code when having multiple errors, in this case, it’s ok to give a 422 Unprocessable Entity status code.

## Summary

We’re at the end of this chapter and we have covered quite a lot. Not only did we introduce the case of Anna’s Bookstore, which we will use as a common ground to easily put things into perspective in the rest of this book. We also covered naming conventions for API endpoints, the JSON:API specification, and especially all of the important rules that are specified.

We looked at how to structure our data or documents for both requests and responses, how to structure our primary data of a document, both when handling single resources and collections of resources.

Then we covered resource objects and which members we must include like id and type, but also learned how to name our member names for a more consistent structure when adding attributes to a resources object.

We then moved on to relationships and how to define relationship links that make it possible to access both relationships themselves and related resources objects. We covered how to define resource identifier objects and how these could be used together with the includes top-level member, to contain related resources in a response in order to save HTTP requests.

Afterward, it was time to look at how to use our new knowledge about data structures to properly communicate between client and servers. We covered how to get resources, and how we could use request documents to fetch the exact resource or collections of resources needed. We looked at how we could sort and paginate resource collections, through both query parameters and a links top-level member.

We then looked at how to create resources and how to structure our request documents, how we could create a relationship through request documents for resource creation, but also how relationship links could be used to create relationships, using relationship linkages instead of resource objects.

We covered how to update resources and relationships using the same principles when creating these, and how an update to a relationship would always remove the current relationship to a resource and then update with the newly given resource instead.

We then learned how to delete both resources and relationships.

Finally, we concluded the chapter by looking at errors and how to convey these through error objects.

We now have a good set of conventions and a knowledge to use when we are building our APIs. We have rules that give us a more consistent way to not only structure data, but also how to communicate and what to communicate. Better yet, when implementing this specification, clients and consumers can use client implementations that will work right out of the box, and save them a lot of time when consuming your API, since these client implementations follow the same conventions and consistency.

It’s now time to look at how to plan out an API. Even though we have a lot of knowledge about convention and rules to build a consistent API, we still need to plan out our project and documentation for our API.

Let’s take a look at that in the next chapter.