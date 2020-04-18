# 0301 Setting Up a Laravel Development Environment

In the first two chapters of the book, we introduced Vue.js. You should now be pretty comfortable with its basic features. In this chapter, we'll get a Laravel development environment up and running as we prepare to build the Vuebnb backend.

Topics covered in this chapter:

A brief introduction to Laravel

Setting up the Homestead virtual development environment

Configuring Homestead to host Vuebnb

Laravel

Laravel is an open source MVC framework for PHP that is used to build robust web applications. Laravel is currently at version 5.5 and is among the most popular PHP frameworks, beloved for its elegant syntax and powerful features.

Laravel is suitable for creating a variety of web-based projects, such as the following:

Websites with user authentication, such as a customer portal or a social network

Web applications, such as an image cropper or a monitoring dashboard

Web services, such as RESTful APIs

In this book, I'm assuming a basic knowledge of Laravel. You should be comfortable with installing and setting up Laravel and be familiar with its core features, such as routing, views, and middleware.

If you're new to Laravel or think you might need to brush up a bit, you should take an hour or two to read through Laravel's excellent documentation before continuing with this book: https://laravel.com/docs/5.5/.

Laravel and Vue

Laravel may seem like a monolithic framework because it includes features for building almost any kind of web application. Under the hood, though, Laravel is a collection of many separate modules, some developed as part of the Laravel project and some from third-party authors. Part of what makes Laravel great is its careful curation and seamless connection of these constituent modules.

Since Laravel version 5.3, Vue.js has been the default frontend framework included in a Laravel installation. There's no official reason why Vue was chosen over other worthy options, such as React, but my guess is that it's because Vue and Laravel share the same philosophy: simplicity and an emphasis on the developer experience.

Whatever the reason, Vue and Laravel offer an immensely powerful and flexible full-stack framework for developing web applications.

Environment

We'll be using Laravel 5.5 for the backend of Vuebnb. This version of Laravel requires PHP 7, several PHP extensions, and the following software:

Composer

A web server, such as Apache or Nginx

A database, such as MySQL or MariaDB

A complete list of requirements for Laravel can be found in the installation guide: https://laravel.com/docs/5.5#installation.

Rather than manually installing the Laravel requirements on your computer, I strongly recommend you use the Homestead development environment, which has everything you need pre-installed.

Homestead

Laravel Homestead is a virtual web application environment which runs on Vagrant and VirtualBox and can be run on any Windows, Mac, or Linux system.

Using Homestead will save you the headache of setting up an development environment from scratch. It will also ensure you have an identical environment to the one I'm using, which will make it easier for you to follow along with this book.

If you don't have Homestead installed on your computer, follow the directions in the Laravel documentation: https://laravel.com/docs/5.5/homestead. Use the default configuration options.

Once you've installed Homestead and launched the Vagrant box with the vagrant up command, you're ready to continue.

Vuebnb

In Chapter 2, Prototyping Vuebnb, Your First Vue.js Project, we made a prototype of the frontend of Vuebnb. The prototype was created from a single HTML file that we loaded directly from the browser.

Now we'll start working on the full-stack Vuebnb project, of which the prototype will soon be a critical part. This main project will be a full Laravel installation with a web server and database.

Project code

If you haven't already, you'll need to download the code base to your computer by cloning it from GitHub. Instructions are given in the Code base section in Chapter 1, Hello Vue - An Introduction to Vue.js.

The vuebnb folder within the code base has the project code that we now want to work with. Change into this folder and list the content:

$ cd vuebnb $ ls -la

The folder contents should look like this:

Figure 3.1. vuebnb project files

Shared folders

The folders property of the Homestead.yaml file lists all of the folders you want to share between your computer and the Homestead environment.

Ensure the code base is shared with Homestead so that we can serve Vuebnb from Homestead's web server later in the chapter.

~/Homestead/Homestead.yaml:

folders: - map: /Users/anthonygore/Projects/Full-Stack-Vue.js-2-and-Laravel-5 to: /home/vagrant/projects

Terminal commands

All further Terminal commands in the book will be given relative to the project directory, that is, vuebnb, unless otherwise specified.

However, as the project directory is shared between your host computer and Homestead, Terminal commands can be run from either of these environments.

Homestead saves you from having to install any software on your host computer. But if you don't, many Terminal commands may not work, or may not work correctly, in the host environment. For example, if you don't have PHP installed on your host computer, you can't run Artisan commands from it:

$ php artisan --version -bash: php: command not found

If this is the case for you, you'll need to run these commands from within Homestead environment by connecting first via SSH:

$ cd ~/Homestead $ vagrant ssh

Change, then, to the project directory within the OS and the same Terminal command will now work:

$ cd ~/projects/vuebnb $ php artisan --version Laravel Framework 5.5.20

The only downside to running commands from Homestead is that they're slower due to the SSH connection. I'll leave it up to you to decide which you'd rather use.

Environment variables

A Laravel project requires certain environment variables to be set in a .env file. Create one now by copying the environment file sample:

$ cp .env.example .env

Generate an app key by running this command:

$ php artisan key:generate

I've preset most other relevant environment variables so you shouldn't have to change anything unless you've configured Homestead differently to me.

Composer install

To complete the installation process, we must run composer install to download all the required packages:

$ composer install

Database

We'll be using a relational database to persist data in our backend application. Homestead has MySQL running out of the box; you just have to provide configuration in the .env file to use it with Laravel. The default configuration will work without any further changes.

.env:

DB_CONNECTION=mysql DB_HOST=192.168.10.10 DB_PORT=3306 DB_DATABASE=vuebnb DB_USERNAME=homestead DB_PASSWORD=secret

Whatever name you choose for your database (that is, the value of DB_DATABASE), make sure it's added to the databases array in your Homestead.yaml file.

~/Homestead/Homestead.yaml:

databases: ... - vuebnb

Serving the project

The main Vuebnb project is now installed. Let's get the web server to serve it at the local development domain vuebnb.test.

In the Homestead configuration file, map vuebnb.test to the project's public folder.

~/Homestead/Homestead.yaml:

sites: ... - map: vuebnb.test to: /home/vagrant/vuebnb/public

Local DNS entry

We also need to update our computer's host file so it understands the mapping between vuebnb.test, and the IP of the web server. The web server is in the Homestead box, which has the IP 192.168.10.10 by default.

To configure this on a Mac, open your host file, /etc/hosts, in a text editor and add this entry:

192.168.10.10 vuebnb.test

The hosts file can normally be found at C:\Windows\System32\Drivers\etc\hosts on a Windows system.

Accessing the project

With all the configuration complete, we can now run vagrant provision from within the Homestead directory to complete the setup:

$ cd ~/Homestead $ vagrant provision

# The next command will return you to the project directory $ cd -

When the provisioning process completes, we should be able to see our site running when we navigate our browser to http://vuebnb.test:

Figure 3.2. Laravel welcome view

Now we're ready to start developing Vuebnb!

## Summary

In this brief chapter, we discussed the requirements for developing a Laravel project. We then installed and configured the Homestead virtual development environment to host our main project, Vuebnb.

In the next chapter, we will begin work on our main project by building a web service to supply data to the frontend of Vuebnb.

Building a Web Service with Laravel

