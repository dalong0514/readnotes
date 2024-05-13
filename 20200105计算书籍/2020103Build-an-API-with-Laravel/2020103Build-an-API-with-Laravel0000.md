## 01 Why Laravel?

There are a lot of reasons why we chose to write this book around Laravel. The biggest reason is that we use the framework in almost all of our applications and solutions. At the time of writing, we have been using Laravel for almost six years and have written over a dozen applications, varying from small to rather large sizes.

Since our primary income comes from developing applications, we want the development time to be as short and cheap as possible. We don’t want to reinvent the wheel every time we start on a new project, we don’t want something that is extremely hard to deploy to a server, and we also want to make something that is not a nightmare to maintain later on. Laravel helps us deal with precisely those problems, which makes development a joy.

## 02. Prerequisites

This book is written with Laravel developers in mind. You do not have to be a super advanced and skilled developer to follow along, but bear in mind that this is not a book about the Laravel framework itself, but instead about how to write an API using Laravel.

Therefore, you will have to have a basic understanding of Laravel to keep up. We certainly recommend that you have tried writing an application in the framework before reading, and that you know what we talk about when we mention: Client, Server, Request, Response, Routes, Controllers, Eloquent or Models, Migrations, Factories, Authentication, Authorization, and Validation.

If most of these words are foreign to you, we recommend that you read up on Laravel before continuing.

We will also be using Laravel Collections heavily, so an understanding of these – especially the map, filter, each, flatten, flatMap, merge, pluck, sort, unique and values methods is necessary.

Also, we expect that you know the basics around PHP, especially the basics around PSR-4 namespacing, how to import classes from other namespaces and so forth. In many IDE’s and editors, all this functionality can be installed with a simple plugin or will already built into the IDE or editor.

## 03. The Github Repository

Throughout this book, we will not only be building an API, but also touching upon various concepts where we will need code examples. All of these can be found in our Github repository at this address:

[WackyStudio/build-an-api-with-laravel: Official Build an API with Laravel repository](https://github.com/WackyStudio/build-an-api-with-laravel)

For the code to the API we will be building, we have the entire application as well as every step of the process separated into small folders in our Github repository, which you can use if you need help or need to see how we have implemented a certain feature:

Each step will add onto the next one and only contain the files that have been added or changed following the structure of our main Laravel application, so you can easily follow along:

You don’t have to clone this repository from the beginning, but if you want to follow along in your code editor instead of the code examples in the book, you can do so with the following commands in your terminal. You will have to be in the desired folder on your local system where the repository should be cloned down to, before running any of the commands. When you are ready, type the following command and make sure you are in the right directory before cloning it:

git clone git@github.com:WackyStudio/build-an-api-with-laravel.git

If you are not using SSH you can clone through HTTPS like this:

git clone https://github.com/WackyStudio/build-an-api-with-laravel.git

If you are not familiar with git, you can also download a zip file with the contents by visiting the repository with the link given previously in this section.

