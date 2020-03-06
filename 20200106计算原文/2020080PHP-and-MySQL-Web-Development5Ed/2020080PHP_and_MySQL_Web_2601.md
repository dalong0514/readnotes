In this project, you get users to register at your website. After they’ve done that, you can track what they’re interested in and show them appropriate content. This behavior is called user personalization.

This particular project enables users to build a set of bookmarks on the web and suggests other links they might find interesting based on their past behavior. More generally, user personalization can be used in almost any web-based application to show users the content they want in the format in which they want it.

In this project, you start by looking at a set of requirements similar to those you might get from a client. You develop those requirements into a set of solution components, build a design to connect those components together, and then implement each of the components.

In this project, you implement the following functionality:

 ■ Logging in and authenticating users

 ■ Managing passwords

 ■ Recording user preferences

 ■ Personalizing content

 ■ Recommending content based on existing knowledge about a user

Solution ComponentsFor this project, your job is to build a prototype for an online bookmarking system, to be called PHPbookmark.

562

Chapter 27  Building User Authentication and Personalization

This system should enable users to log in and store their personal bookmarks and to get recommendations for other sites that they might like to visit based on their personal preferences.

These solution components fall into three main categories:

 ■ You need to be able to identify individual users. You should also have some way of 

authenticating them.

 ■ You need to be able to store bookmarks for an individual user. Users should be able to 

add and delete bookmarks.

 ■ You need to be able to recommend to users sites that might appeal to them, based on 

what you know about them already.

Now that you know the idea behind the project, you can begin designing the solution and its components. Let’s look at possible solutions to each of the three main requirements listed.

User Identification and PersonalizationSeveral alternatives can be used for user authentication, as you have seen elsewhere in this book. Because you want to tie users to some personalization information, you can store the users’ logins and passwords in a MySQL database and authenticate against it.

If you are going to let users log in with usernames and passwords, you will need the following components:

 ■ Users should be able to register their usernames and passwords. You need some 

restrictions on the length and format of each username and password. You should store passwords in an encrypted format for security reasons.

 ■ Users should be able to log in with the details they supplied in the registration process.

 ■ Users should be able to log out after they have finished using a site. This capability is not particularly important if people use the site from their home PC but is very important for security if they use the site from a shared PC such as at a library.

 ■ The site needs to be able to check whether a particular user is logged in, and then access 

data for the logged-in user.

 ■ Users should be able to change their passwords as an aid to security.

 ■ Users should be able to reset their passwords without needing personal assistance from 

you. A common way of doing this is to send a user’s password to him or her at an email address he or she has provided at registration. This means you need to store the user’s email address at registration. Because you store the passwords in an encrypted form and cannot decrypt the user’s original password, you actually need to generate a new password, set it, and mail the new password to the user.

For purposes of this project, you will write custom functions for all of these pieces of functionality. Most of them will be reusable, or reusable with minor modifications, in other projects.

Solution Overview

563

Storing BookmarksTo store a user’s bookmarks, you need to set up some relational tables in your MySQL database. You need the following functionality:

 ■ Users should be able to retrieve and view their bookmarks.

 ■ Users should be able to add new bookmarks. The site should check that these are valid 

URLs.

 ■ Users should be able to delete bookmarks.

Again, you will write functions for each of these pieces of functionality.

Recommending BookmarksYou could take a number of different approaches to recommending bookmarks to a user. You could recommend the most popular overall or the most popular within a topic. For this project, you will implement a「like minds」suggestion system that looks for users who have a  bookmark the same as your logged-in user and suggests their other bookmarks to your user. To avoid recommending any personal bookmarks, you will recommend only bookmarks stored by more than one other user.

You will again write a function to implement this functionality.

Solution OverviewAfter some doodling on napkins, we came up with a system flowchart you can use, as shown in Figure 27.1.

Figure 27.1  The possible paths through the PHPbookmark system

564

Chapter 27  Building User Authentication and Personalization

You can build a module for each box on this diagram; some will need one script and others, two. You can also set up function libraries for

 ■ User authentication.

 ■ Bookmark storage and retrieval.

 ■ Data validation.

 ■ Database connections.

 ■ Output to the browser. You can confine all the HTML production to this function library, 

ensuring that visual presentation is consistent throughout the site. (This is the function API approach to separating logic and content.)

You also need to build a back-end database for the system.

We describe the solution in some detail, but all the code for this application can be found in the book’s code files online. A summary of included files is shown in Table 27.1.

Table 27.1  Files in the PHPbookmark Application

Filename

bookmarks.sql

login.php

Description

SQL statements to create the PHPbookmark database

Front page with login form for the system

register_form.php

Form for users to register in the system

register_new.php

Script to process new registrations

forgot_form.php

Form for users to fill out if they’ve forgotten their passwords

forgot_passwd.php

Script to reset forgotten passwords

member.php

A user’s main page, with a view of all of the user’s current bookmarks

add_bm_form.php

Form for adding new bookmarks

add_bms.php

delete_bms.php

recommend.php

Script to actually add new bookmarks to the database

Script to delete selected bookmarks from a user’s list

Script to suggest recommendations to a user, based on users with similar interests

change_passwd_form.php

Form for members to fill out if they want to change their passwords

change_passwd.php

Script to change a user’s password in the database

logout.php

Script to log a user out of the application

bookmark_fns.php

A collection of includes for the application

data_valid_fns.php

Functions to validate user-input data

Implementing the Database

565

db_fns.php

Functions to connect to the database

user_auth_fns.php

Functions for user authentication

url_fns.php

output_fns.php

bookmark.gif

Functions for adding and deleting bookmarks and for making recommendations

Functions that format output as HTML

Logo for PHPbookmark

You begin by implementing the MySQL database for this application because it is required for virtually all the other functionality to work. Then you work through the code in the order it was written, starting from the front page, going through the user authentication, to bookmark storage and retrieval, and finally to recommendations. This order is fairly logical; it’s just a question of working out the dependencies and building first the things that will be required for later modules.

Implementing the DatabaseThe PHPbookmark database requires only a fairly simple schema. You need to store users and their email addresses and passwords. You also need to store the URL of a bookmark. One user can have many bookmarks, and many users can register the same bookmark. You therefore need two tables, user and bookmark, as shown in Figure 27.2.

Figure 27.2  Database schema for the PHPbookmark system

The user table stores each user’s username (which is the primary key), password, and email address. The bookmark table stores username and bookmark (bm_URL) pairs. The username in this table refers to a username from the user table.

The SQL to create this database, and to create a user for connecting to the database from the web, is shown in Listing 27.1. You should edit this file if you plan to use it on your system. Be sure to change the user’s password to something more secure!

566

Chapter 27  Building User Authentication and Personalization

Listing 27.1  bookmarks.sql—SQL File to Set Up the Bookmark Databasecreate database bookmarks;use bookmarks;

create table user  (  username varchar(16) not null primary key,  passwd char(40) not null,  email varchar(100) not null);

create table bookmark (  username varchar(16) not null,  bm_URL varchar(255) not null,  index (username),  index (bm_URL),  primary key(username, bm_URL));

grant select, insert, update, deleteon bookmarks.*to bm_user@localhost identified by 'password';

You can set up this database on your system by running this set of commands as the root MySQL user. You can do this with the following command on your system’s command line:

mysql -u youruser -p < bookmarks.sql

You are then prompted to type in your password.

With the database set up, you’re ready to go on and implement the basic site.

Implementing the Basic SiteThe first page you’ll build is called login.php because it provides users with the opportunity to log in to the system. The code for this first page is shown in Listing 27.2.

Listing 27.2  login.php—Front Page of the PHPbookmark System<?php require_once('bookmark_fns.php'); do_html_header('');

 display_site_info();  display_login_form();

 do_html_footer();?>

Implementing the Basic Site

567

This code looks very simple because it mostly calls functions from the function API that you will construct for this application. We look at the details of these functions shortly. Just looking at this file, you can see that it includes a file (containing the functions) and then calls some functions to render an HTML header, display some content, and render an HTML footer.

The output from this script is shown in Figure 27.3.

Figure 27.3  The front page of the PHPbookmark system is produced by the HTML rendering functions in login.php

The functions for the system are all included in the file bookmark_fns.php, shown in Listing 27.3.

Listing 27.3 

 bookmark_fns.php—Include File of Functions for the Bookmark Application

<?php  // We can include this file in all our files  // this way, every file will contain all our functions and exceptions  require_once('data_valid_fns.php');   require_once('db_fns.php');  require_once('user_auth_fns.php');  require_once('output_fns.php');  require_once('url_fns.php');?>

568

Chapter 27  Building User Authentication and Personalization

As you can see, this file is just a container for the five other include files you will use in this application. We structured the project like this because the functions fall into logical groups. Some of these groups might be useful for other projects, so we put each function group into a different file so you will know where to find it when you want it again. We constructed the bookmark_fns.php file because you will use most of the five function files in most of the scripts. Including this one file in each script is easier than having five require statements in each script.

In this particular case, you use functions from the file output_fns.php. They are all  straightforward functions that output fairly plain HTML. This file includes the four functions used in login.php—that is, do_html_header(), display_site_info(), display_login_form(), and do_html_footer(), among others.

Although we will not go through all these functions in detail, let’s look at one as an example. The code for do_html_header() is shown in Listing 27.4.

Listing 27.4 

 do_html_header()Function from output_fns.php—This Function Outputs the Standard Header That Will Appear on Each Page in the Application

function do_html_header($title) {  // print an HTML header?><!doctype html>  <html>  <head>    <meta charset="utf-8">    <title><?php echo $title;?></title>    <style>      body { font-family: Arial, Helvetica, sans-serif; font-size: 13px }      li, td { font-family: Arial, Helvetica, sans-serif; font-size: 13px }      hr { color: #3333cc;}      a { color: #000 }      div.formblock         { background: #ccc; width: 300px; padding: 6px; border: 1px solid #000;}    </style>  </head>  <body>  <div>    <img src="bookmark.gif" alt="PHPbookmark logo" height="55" width="57" style="float: left; padding-right: 6px;" />      <h1>PHPbookmark</h1>  </div>  <hr /><?php  if($title) {    do_html_heading($title);  }}

Implementing User Authentication

569

As you can see, the only logic in the do_html_header() function is to start the HTML  document and add the appropriate title and heading to the page. The other functions used in login.php are similar. The function display_site_info() adds some general text about the site, display_login_form() displays the gray form shown in Figure 27.3, and do_html_footer() adds a standard HTML footer to the page.

The advantages to isolating or removing HTML from your main logic stream are discussed in Chapter 25,「Using PHP and MySQL for Large Projects.」We use the function API approach here.

Looking at Figure 27.3, you can see that this page has three options: A user can register, log in if he or she has already registered, or reset the user’s password if he or she has forgotten it. To implement these modules, we move on to the next section, user authentication.

Implementing User AuthenticationThere are four main elements to the user authentication module: registering users, logging in and logging out, changing passwords, and resetting passwords. In the following sections, we look at each of these elements in turn.

Registering UsersTo register a user, you need to get the user’s details via a form and enter the user in the database.

When a user clicks on the Not a member? link on the login.php page, the user is taken to a registration form produced by register_form.php. This script is shown in Listing 27.5.

Listing 27.5 

 register_form.php—This Form Gives Users the Opportunity to Register with PHPbookmark

<?php require_once('bookmark_fns.php'); do_html_header('User Registration');

 display_registration_form();

 do_html_footer();?>

Again, you can see that this page is fairly simple and just calls functions from the output library in output_fns.php. The output of this script is shown in Figure 27.4.

The gray form on this page is output by the function display_registration_form(), contained in output_fns.php. When the user clicks on the Register button, the user is taken to the script register_new.php, shown in Listing 27.6.

570

Chapter 27  Building User Authentication and Personalization

Figure 27.4  The registration form retrieves the details needed for the database. This form requires users to type their passwords twice, in case they make a mistake

Listing 27.6 

 register_new.php—This Script Validates the New User’s Data and Puts It in the Database

<?php  // include function files for this application  require_once('bookmark_fns.php');

  //create short variable names  $email=$_POST['email'];  $username=$_POST['username'];  $passwd=$_POST['passwd'];  $passwd2=$_POST['passwd2'];  // start session which may be needed later  // start it now because it must go before headers  session_start();  try   {    // check forms filled in    if (!filled_out($_POST)) {      throw new Exception('You have not filled the form out correctly –           please go back and try again.');    }

Implementing User Authentication

571

    // email address not valid    if (!valid_email($email)) {      throw new Exception('That is not a valid email address.           Please go back and try again.');    }

    // passwords not the same    if ($passwd != $passwd2) {      throw new Exception('The passwords you entered do not match –           please go back and try again.');    }

    // check password length is ok    // ok if username truncates, but passwords will get    // munged if they are too long.    if ((strlen($passwd) < 6) || (strlen($passwd) > 16)) {      throw new Exception('Your password must be between 6 and 16 characters.          Please go back and try again.');    }

    // attempt to register    // this function can also throw an exception    register($username, $email, $passwd);    // register session variable    $_SESSION['valid_user'] = $username;

    // provide link to members page    do_html_header('Registration successful');    echo 'Your registration was successful.  Go to the members page to start           setting up your bookmarks!';    do_html_url('member.php', 'Go to members page');

   // end page   do_html_footer();  }  catch (Exception $e) {     do_html_header('Problem:');     echo $e->getMessage();     do_html_footer();     exit;  }?>

This is the first script with any complexity to it that we have looked at in this application. It begins by including the application’s function files and starting a session. (When the user is registered, you create his username as a session variable, as you did in Chapter 22,「Using Session Control in PHP.」)

572

Chapter 27  Building User Authentication and Personalization

The body of the script takes place in a try block because you check a number of conditions. If any of them fail, execution will fall through to the catch block, which we look at shortly.

Next, you validate the input data from the user. Here, you must test for the following conditions:

 ■ Check that the form is filled out. You test this with a call to the function filled_out(), 

as follows:if (!filled_out($_POST))

We wrote this function ourselves. It is in the function library in the ﬁ le data_valid_fns.php. We look at this function shortly.

 ■ Check that the email address supplied is valid. You test this as follows:

if (valid_email($email))

Again, this is a function we wrote; it’s in the data_valid_fns.php library.

 ■ Check that the two passwords the user has suggested are the same, as follows:

if ($passwd != $passwd2)

 ■ Check that the username and password are the appropriate length, as follows:

if ((strlen($passwd) < 6)

and

if ((strlen($passwd) > 16)

In the example, the password should be at least six characters long to make it harder to guess, and the username should be fewer than 17 characters so that it will ﬁ t in the data-base ﬁ eld that has been deﬁ ned to hold the username. Note that the maximum length of the password is not restricted in this way because it is stored as an SHA1 hash, which will always be 40 characters long no matter the length of the password.

The data validation functions used here, filled_out() and valid_email(), are shown in Listings 27.7 and 27.8, respectively. These functions serve as an extra protection for  validating form input on the server side, and go beyond any client-side validation handled by the browser. If you are collecting important information in a web form, you should always validate both on the client side and the server side.

Listing 27.7 

 filled_out() Function from data_valid_fns.php—This Function Checks That the Form Has Been Filled Out

function filled_out($form_vars) {  // test that each variable has a value  foreach ($form_vars as $key => $value) {     if ((!isset($key)) || ($value == '')) {        return false;     }  }  return true;}

Implementing User Authentication

573

Listing 27.8 

 valid_email() Function from data_valid_fns.php—This Function Checks Whether an Email Address Is Valid

function valid_email($address) {  // check an email address is possibly valid  if (preg_match('/^[a-zA-Z0-9_\.\-]+@[a-zA-Z0-9\-]+\.[a-zA-Z0-9\-\.]+$/', $address)) {    return true;  } else {    return false;  }}

The function filled_out() expects to be passed an array of variables; in general, this is the $_POST or $_GET array. It checks whether the form fields are all filled out, and returns true if they are and false if they are not.

The valid_email() function uses a slightly more complex regular expression than the one developed in Chapter 4,「String Manipulation and Regular Expressions,」for validating email addresses. It returns true if an address appears valid and false if it does not.

After you’ve validated the input data, you can actually try to register the user. If you look back at Listing 27.6, you can see that you do this as follows:

    register($username, $email, $passwd);    // register session variable    $_SESSION['valid_user'] = $username;

    // provide link to members page    do_html_header('Registration successful');    echo 'Your registration was successful. Go to the members page to start           setting up your bookmarks!';    do_html_url('member.php', 'Go to members page');

   // end page   do_html_footer();

As you can see, you call the register() function with the username, email address, and  password that were entered. If this call succeeds, you register the username as a session  variable and provide the user with a link to the main members’ page. (If it fails, this  function will throw an exception that will be caught in the catch block.) The output is shown in Figure 27.5.

574

Chapter 27  Building User Authentication and Personalization

Figure 27.5  Registration was successful; the user can now go to the members’ page

The register() function is in the included library called user_auth_fns.php. This function is shown in Listing 27.9.

Listing 27.9 

 register()Function from user_auth_fns.php—This Function Attempts to Put the New User’s Information in the Database

function register($username, $email, $password) {// register new person with db// return true or error message

  // connect to db  $conn = db_connect();

  // check if username is unique  $result = $conn->query("select * from user where username='".$username."'");  if (!$result) {    throw new Exception('Could not execute query');  }

  if ($result->num_rows>0) {    throw new Exception('That username is taken - go back and choose another one.');  }

Implementing User Authentication

575

  // if ok, put in db  $result = $conn->query("insert into user values                         ('".$username."', sha1('".$password."'), '".$email."')");  if (!$result) {    throw new Exception('Could not register you in database - please try again later.');  }

  return true;}

There is nothing particularly new in this function; it connects to the database you set up earlier. If the username selected is taken or the database cannot be updated, it will throw an exception. Otherwise, it will update the database and return true.

Note that you are performing the actual database connection with a function called db_connect(), which we wrote. This function simply provides a single location that contains the username and password to connect to the database. That way, if you change the database password, you need to change only one file in the application. The db_connect() function is shown in Listing 27.10.

Listing 27.10 

 db_connect()Function from db_fns.php—This Function Connects to the MySQL Database

<?php

function db_connect() {   $result = new mysqli('localhost', 'bm_user', 'password', 'bookmarks');   if (!$result) {     throw new Exception('Could not connect to database server');   } else {     return $result;   }}

?>

When users are registered, they can log in and out using the regular login and logout pages. You build them next.

Logging InIf users type their details into the form at login.php (see Figure 27.3) and submit it, they will be taken to the script called member.php. This script logs them in if they have come from this 

576

Chapter 27  Building User Authentication and Personalization

form. It also displays any relevant bookmarks to users who are logged in. It is the center of the rest of the application. This script is shown in Listing 27.11.

Listing 27.11  member.php—This Script Is the Main Hub of the Application<?php

// include function files for this applicationrequire_once('bookmark_fns.php');session_start();

//create short variable namesif (!isset($_POST['username']))  {  //if not isset -> set with dummy value   $_POST['username'] = " "; }$username = $_POST['username'];if (!isset($_POST['passwd']))  {  //if not isset -> set with dummy value   $_POST['passwd'] = " "; }$passwd = $_POST['passwd'];

if ($username && $passwd) {// they have just tried logging in  try  {    login($username, $passwd);    // if they are in the database register the user id    $_SESSION['valid_user'] = $username;  }  catch(Exception $e)  {    // unsuccessful login    do_html_header('Problem:');    echo 'You could not be logged in.<br>          You must be logged in to view this page.';    do_html_url('login.php', 'Login');    do_html_footer();    exit;  }}

do_html_header('Home');check_valid_user();// get the bookmarks this user has savedif ($url_array = get_user_urls($_SESSION['valid_user'])) {  display_user_urls($url_array);}

Implementing User Authentication

577

// give menu of optionsdisplay_user_menu();

do_html_footer();?>

You might recognize the logic in the member.php script: It reuses some of the ideas from Chapter 22.

First, you check whether the user has come from the front page—that is, whether the user has just filled in the login form—and try to log the user in as follows:

if ($username && $passwd) {// they have just tried logging in  try  {    login($username, $passwd);    // if they are in the database register the user id    $_SESSION['valid_user'] = $username;  }

You try to log the user in by using a function called login(). It is defined in the user_auth_fns.php library, and we look at the code for it shortly.

If the user is logged in successfully, you register the user’s session as you did before, storing the username in the session variable valid_user.

If all goes well, you then show the user the members’ page:

do_html_header('Home');check_valid_user();// get the bookmarks this user has savedif ($url_array = get_user_urls($_SESSION['valid_user'])) {  display_user_urls($url_array);}

// give menu of optionsdisplay_user_menu();

do_html_footer();

This page is again formed using the output functions. Notice that the page uses several other new functions: check_valid_user() from user_auth_fns.php, get_user_urls() from url_fns.php, and display_user_urls() from output_fns.php. The check_valid_user() function checks that the current user has a registered session. This is aimed at users who have not just logged in, but are mid-session. The get_user_urls() function gets a user’s bookmarks from the database, and display_user_urls() outputs the bookmarks to the browser in a table. We look at check_valid_user() in a moment and at the other two in the section on bookmark storage and retrieval.

578

Chapter 27  Building User Authentication and Personalization

The member.php script ends the page by displaying a menu with the display_user_menu() function. Some sample output as displayed by member.php is shown in Figure 27.6.

Figure 27.6  The member.php script checks that a user is logged in, retrieves and displays the user’s bookmarks, and gives the user a menu of options

Let’s look at the login() and check_valid_user() functions a little more closely now. The login() function is shown in Listing 27.12.

Listing 27.12 

 login()Function from user_auth_fns.php—This Function Checks a User’s Details Against the Database

function login($username, $password) {// check username and password with db// if yes, return true// else throw exception

  // connect to db  $conn = db_connect();

  // check if username is unique  $result = $conn->query("select * from user                         where username='".$username."'                         and passwd = sha1('".$password."')");

Implementing User Authentication

579

  if (!$result) {     throw new Exception('Could not log you in.');  }

  if ($result->num_rows>0) {     return true;  } else {     throw new Exception('Could not log you in.');  }}

As you can see, the login() function connects to the database and checks that there is a user with the username and password combination supplied. It returns true if there is or throws an exception if there is not or if the user’s credentials could not be checked.

The check_valid_user() function does not connect to the database again, but instead just checks that the user has a registered session—that is, that the user has already logged in. This function is shown in Listing 27.13.

Listing 27.13 

 check_valid_user()Function from user_auth_fns.php—This Function Checks That the User Has a Valid Session

function check_valid_user() {// see if somebody is logged in and notify them if not  if (isset($_SESSION['valid_user']))  {      echo "Logged in as ".$_SESSION['valid_user'].".<br>";  } else {     // they are not logged in     do_html_heading('Problem:');     echo 'You are not logged in.<br>';     do_html_url('login.php', 'Login');     do_html_footer();     exit;  }}

If the user is not logged in, the function will tell the user that he or she has to be logged in to see this page, and give the user a link to the login page.

Logging OutYou might have noticed the link marked Logout on the menu in Figure 27.6. This is a link to the logout.php script; the code for this script is shown in Listing 27.14.

580

Chapter 27  Building User Authentication and Personalization

Listing 27.14  logout.php—This Script Ends a User Session<?php

// include function files for this applicationrequire_once('bookmark_fns.php');session_start();$old_user = $_SESSION['valid_user'];

// store  to test if they *were* logged inunset($_SESSION['valid_user']);$result_dest = session_destroy();

// start output htmldo_html_header('Logging Out');

if (!empty($old_user)) {  if ($result_dest)  {    // if they were logged in and are now logged out    echo 'Logged out.<br>';    do_html_url('login.php', 'Login');  } else {   // they were logged in and could not be logged out    echo 'Could not log you out.<br>';  }} else {  // if they weren't logged in but came to this page somehow  echo 'You were not logged in, and so have not been logged out.<br>';  do_html_url('login.php', 'Login');}

do_html_footer();

?>

Again, you might find that this code looks familiar. That’s because it is based on the code you wrote in Chapter 22.

Changing PasswordsIf a user follows the Change Password menu option, the user will be presented with the form shown in Figure 27.7.

Implementing User Authentication

581

Figure 27.7  The change_passwd_form.php script supplies a form where users can change their passwords

This form is generated by the script change_passwd_form.php. This simple script just uses the functions from the output library, so we did not include the source for it here.

When this form is submitted, it triggers the change_passwd.php script, which is shown in Listing 27.15.

Listing 27.15  change_passwd_form.php—This Script Changes a User Password<?php require_once('bookmark_fns.php'); session_start(); do_html_header('Change password'); check_valid_user();

 display_password_form();

 display_user_menu();  do_html_footer();?>

582

Chapter 27  Building User Authentication and Personalization

This script checks that the user is logged in (using check_valid_user()), that the user filled out the password form (using filled_out()), and that the new passwords are the same and the right length. None of this is new. If all that goes well, the script will call the change_password() function as follows:

change_password($_SESSION['valid_user'], $old_passwd, $new_passwd);echo 'Password changed.';

This function is from the user_auth_fns.php library, and the code for it is shown in Listing 27.16.

Listing 27.16 

 change_password()Function from user_auth_fns.php—This Function Updates a User Password in the Database

function change_password($username, $old_password, $new_password) {// change password for username/old_password to new_password// return true or false

  // if the old password is right  // change their password to new_password and return true  // else throw an exception  login($username, $old_password);  $conn = db_connect();  $result = $conn->query("update user                          set passwd = sha1('".$new_password."')                          where username = '".$username."'");  if (!$result) {    throw new Exception('Password could not be changed.');  } else {    return true;  // changed successfully  }}

This function checks that the old password supplied was correct, using the login() function that you have already looked at. If it’s correct, the function will connect to the database and update the password to the new value.

Resetting Forgotten PasswordsIn addition to changing passwords, you need to deal with the common situation in which a user has forgotten his or her password. On the front page, login.php, you provide a link, marked Forgotten your password?, for users in this situation. This link takes users to the script called forgot_form.php, which uses the output functions to display a form, as shown in Figure 27.8.

Implementing User Authentication

583

Figure 27.8  The forgot_form.php script supplies a form in which users can ask to have their passwords reset and sent to them

The forgot_form.php script is very simple—just using the output functions—so we did not include it here. When the form is submitted, it calls the forgot_passwd.php script, which is more interesting. This script is shown in Listing 27.17.

Listing 27.17 

 forgot_passwd.php—This Script Resets a User’s Password to a Random Value and Emails the User the New One

<?php  require_once("bookmark_fns.php");  do_html_header("Resetting password");

  // creating short variable name  $username = $_POST['username'];

  try {    $password = reset_password($username);    notify_password($username, $password);    echo 'Your new password has been emailed to you.<br>';  }

584

Chapter 27  Building User Authentication and Personalization

  catch (Exception $e) {    echo 'Your password could not be reset - please try again later.';  }  do_html_url('login.php', 'Login');  do_html_footer();?>

As you can see, this script uses two main functions to do its job: reset_password() and notify_password(). Let’s look at each of these in turn.

The reset_password() function generates a random password for the user and puts it into the database. The code for this function is shown in Listing 27.18.

Listing 27.18 

 reset_password()Function from user_auth_fns.php—This Function Resets a User’s Password to a Random Value and Emails the User the New One

function reset_password($username) {// set password for username to a random value// return the new password or false on failure // get a random dictionary word b/w 6 and 13 chars in length  $new_password = get_random_word(6, 13);

  if($new_password == false) {    // give a default password    $new_password = "changeMe!";  }

  // add a number between 0 and 999 to it  // to make it a slightly better password  $rand_number = rand(0, 999);  $new_password .= $rand_number;

  // set user's password to this in database or return false  $conn = db_connect();  $result = $conn->query("update user                          set passwd = sha1('".$new_password."')                          where username = '".$username."'");  if (!$result) {    throw new Exception('Could not change password.');  // not changed  } else {    return $new_password;  // changed successfully  }}

Implementing User Authentication

585

The reset_password() function generates its random password by getting a random word from a dictionary, using the get_random_word() function and suffixing it with a random number between 0 and 999. If the dictionary word is missing, it sets the default password to changeMe! with the random number suffix. The get_random_word() function, shown in Listing 27.19, is also in the user_auth_fns.php library.

If you want your script to be more secure, you should throw an exception rather than setting a default starting word as follows:

  if($new_password == false) {    throw new Exception('Could not set new password.');  }

Listing 27.19 

 get_random_word()Function from user_auth_fns.php—This Function Gets a Random Word from the Dictionary for Use in Generating Passwords

function get_random_word($min_length, $max_length) {// grab a random word from dictionary between the two lengths// and return it

   // generate a random word  $word = '';  // remember to change this path to suit your system  $dictionary = '/usr/dict/words';  // the ispell dictionary  $fp = @fopen($dictionary, 'r');  if(!$fp) {    return false;  }  $size = filesize($dictionary);

  // go to a random location in dictionary  $rand_location = rand(0, $size);  fseek($fp, $rand_location);

  // get the next whole word of the right length in the file  while ((strlen($word) < $min_length) || (strlen($word)>$max_length) || (strstr($word, "'"))) {     if (feof($fp)) {        fseek($fp, 0);        // if at end, go to start     }     $word = fgets($fp, 80);  // skip first word as it could be partial     $word = fgets($fp, 80);  // the potential password  }  $word = trim($word); // trim the trailing \n from fgets  return $word;}

586

Chapter 27  Building User Authentication and Personalization

To work, the get_random_word() function needs a dictionary. If you are using a Unix system, the spell checker ispell comes with a dictionary of words, typically located at /usr/dict/words, as it is here, or at /usr/share/dict/words. If you don’t find it in one of these places, on most systems you can find yours by typing

# locate dict/words

If you are using some other system or do not want to install ispell, don’t worry! You can download word lists as used by ispell from http://wordlist.sourceforge.net/. Just change the location of your word list in the get_random_word() function.

This site also has dictionaries in many other languages, so if you would like a random, say, Norwegian or Esperanto word, you can download one of those dictionaries instead. These files are formatted with each word on a separate line, separated by newlines.

To get a random word from this file, you pick a random location between 0 and the filesize, and read from the file there. If you read from the random location to the next newline, you will most likely get only a partial word, so you skip the line you open the file to and take the next word as your word by calling fgets() twice.

The function has two clever bits. The first is that if you reach the end of the file while looking for a word, you go back to the beginning:

if (feof($fp)) {   fseek($fp, 0);        // if at end, go to start}

The second is that you can seek for a word of a particular length: You check each word that you pull from the dictionary, and, if it is not between $min_length and $max_length, you keep searching. At the same time, you also dump words with apostrophes (single quotation marks) in them. You could escape them out when using the word, but just getting the next word is easier.

Back in reset_password(), after you have generated a new password, you update the  database to reflect this and return the new password to the main script. This is then passed on to notify_password(), which emails it to the user. The notify_password() function is shown in Listing 27.20.

Listing 27.20 

 notify_password()Function from user_auth_fns.php—This Function Emails a Reset Password to a User

function notify_password($username, $password) {// notify the user that their password has been changed

    $conn = db_connect();    $result = $conn->query("select email from user                            where username='".$username."'");    if (!$result) {      throw new Exception('Could not find email address.');    } else if ($result->num_rows == 0) {

Implementing Bookmark Storage and Retrieval

587

      throw new Exception('Could not find email address.');      // username not in db    } else {      $row = $result->fetch_object();      $email = $row->email;      $from = "From: support@phpbookmark \r\n";      $mesg = "Your PHPBookmark password has been changed to ".$password."\r\n".              "Please change it next time you log in.\r\n";

      if (mail($email, 'PHPBookmark login information', $mesg, $from)) {        return true;      } else {        throw new Exception('Could not send email.');      }    }}

In the notify_password() function, given a username and new password, you simply look up the email address for that user in the database and use PHP’s mail() function to send it to the user.

It would be more secure to give users a truly random password—made from any combination of upper and lowercase letters, numbers, and punctuation—rather than the random word and number. However, a password like zigzag487 will be easier for users to read and type than a truly random one. It is often confusing for users to work out whether a character in a random string is 0 or O (zero or capital O), or 1 or l (one or a lowercase L).

On our system, the dictionary file contains about 45,000 words. If a cracker knew how we were creating passwords and knew a user’s name, he would still have to try 22,500,000 passwords on average to guess one. This level of security seems adequate for this type of application even if our users disregard our emailed advice to change their password, since no real personal data is being stored. 

However, a better approach to allowing users to reset their passwords would be to send users a link to a password reset page, in which the query string contained a one-time use token that expires after a certain amount of time (24 hours, 72 hours, and so on). This one-time use token would be the「key」that authorizes a user to change his or her password, without having to use a generated password that had been sent in plain text via email.

Implementing Bookmark Storage and RetrievalWith the user account–related functionality behind you, let’s move on and look at how users’ bookmarks are stored, retrieved, and deleted.

588

Chapter 27  Building User Authentication and Personalization

Adding BookmarksUsers can add bookmarks by clicking on the Add BM link in the user menu. This action takes them to the form shown in Figure 27.9.

Figure 27.9  The add_bm_form.php script supplies a form where users can add bookmarks to their bookmark pages

Again, because the add_bm_form.php script is simple and uses just the output functions, we did not include it here. When the form is submitted, it calls the add_bms.php script, which is shown in Listing 27.21.

Listing 27.21  add_bms.php—This Script Adds New Bookmarks to a User’s Personal Page<?php require_once('bookmark_fns.php'); session_start();

  //create short variable name  $new_url = $_POST['new_url'];

  do_html_header('Adding bookmarks');

  try {

Implementing Bookmark Storage and Retrieval

589

    check_valid_user();    if (!filled_out($_POST)) {      throw new Exception('Form not completely filled out.');    }    // check URL format    if (strstr($new_url, 'http://') === false) {       $new_url = 'http://'.$new_url;    }

    // check URL is valid    if (!(@fopen($new_url, 'r'))) {      throw new Exception('Not a valid URL.');    }

    // try to add bm    add_bm($new_url);    echo 'Bookmark added.';

    // get the bookmarks this user has saved    if ($url_array = get_user_urls($_SESSION['valid_user'])) {      display_user_urls($url_array);    }  }  catch (Exception $e) {    echo $e->getMessage();  }  display_user_menu();  do_html_footer();?>

Again, this script follows the pattern of validation, database entry, and output.

To validate, you first check whether the user has filled out the form using filled_out(). You then perform two URL checks. First, using strstr(), you see whether the URL begins with http://. If it doesn’t, you add this to the start of the URL. After you’ve done this, you can actually check that the URL really exists. As you might recall from Chapter 18,「Using Network and Protocol Functions,」you can use fopen() to open a URL that starts with http://. If you can open this file, you can assume the URL is valid and call the function add_bm() to add it to the database.

This function and the others relating to bookmarks are all in the function library url_fns.php. You can see the code for the add_bm() function in Listing 27.22.

590

Chapter 27  Building User Authentication and Personalization

Listing 27.22 

 add_bm()Function from url_fns.php—This Function Adds New Bookmarks to the Database

function add_bm($new_url) {  // Add new bookmark to the database

  echo "Attempting to add ".htmlspecialchars($new_url)."<br />";  $valid_user = $_SESSION['valid_user'];

  $conn = db_connect();

  // check not a repeat bookmark  $result = $conn->query("select * from bookmark                         where username='$valid_user'                         and bm_URL='".$new_url."'");  if ($result && ($result->num_rows>0)) {    throw new Exception('Bookmark already exists.');  }

  // insert the new bookmark  if (!$conn->query("insert into bookmark values     ('".$valid_user."', '".$new_url."')")) {    throw new Exception('Bookmark could not be inserted.');  }

  return true;} 

The add_bm()function is fairly simple. It checks that a user does not already have this  bookmark listed in the database. (Although it is unlikely that users would enter a bookmark twice, it is possible and even likely that they might refresh the page.) If the bookmark is new, it is entered into the database.

Looking back at add_bm.php, you can see that the last thing it does is call get_user_urls() and display_user_urls(), the same as member.php. We look at these functions next.

Displaying BookmarksThe member.php script and add_bm() function use the functions get_user_urls() and display_user_urls(). These functions get a user’s bookmarks from the database and display them, respectively. The get_user_urls() function is in the url_fns.php library, and the display_user_urls() function is in the output_fns.php library.

The get_user_urls() function is shown in Listing 27.23.

Implementing Bookmark Storage and Retrieval

591

Listing 27.23 

 get_user_urls()Function from url_fns.php—This Function Retrieves a User’s Bookmarks from the Database

function get_user_urls($username) {  //extract from the database all the URLs this user has stored

  $conn = db_connect();  $result = $conn->query("select bm_URL                          from bookmark                          where username = '".$username."'");  if (!$result) {    return false;  }

  //create an array of the URLs  $url_array = array();  for ($count = 1; $row = $result->fetch_row(); ++$count) {    $url_array[$count] = $row[0];  }  return $url_array;

}

Let’s briefly step through the get_user_urls() function. It takes a username as a parameter and retrieves the bookmarks for that user from the database. It returns an array of these URLs or false if the bookmarks could not be retrieved.

The array from get_user_urls() can be passed to display_user_urls(). This is again a simple HTML output function to print the user’s URLs in a nice table format, so we didn’t include it here. Refer to Figure 27.6 to see what the output looks like. The function actually puts the URLs into a form. Next to each URL is a check box that enables the user to mark  bookmarks for deletion. We look at this capability next.

Deleting BookmarksWhen a user marks some bookmarks for deletion and clicks on the Delete BM link on the menu, the form containing the URLs is submitted. Each one of the check boxes is produced by the following code in the display_user_urls() function:

echo "<tr bgcolor=\"".$color."\"><td>      <a href=\"".$url."\">".htmlspecialchars($url)."</a></td>      <td><input type=\"checkbox\" name=\"del_me[]\"           value=\"".$url."\"></td>      </tr>";

The name of each input is del_me[]. This means that, in the PHP script activated by this form, you have access to an array called $del_me that contains all the bookmarks to be deleted.

592

Chapter 27  Building User Authentication and Personalization

Clicking on the Delete BM option activates the delete_bms.php script, which is shown in Listing 27.24.

Listing 27.24  delete_bms.php—This Script Deletes Bookmarks from the Database<?php  require_once('bookmark_fns.php');  session_start();

  //create short variable names  $del_me = $_POST['del_me'];  $valid_user = $_SESSION['valid_user'];

  do_html_header('Deleting bookmarks');  check_valid_user();

  if (!filled_out($_POST)) {    echo '<p>You have not chosen any bookmarks to delete.<br>          Please try again.</p>';    display_user_menu();    do_html_footer();    exit;  } else {    if (count($del_me) > 0) {      foreach($del_me as $url) {        if (delete_bm($valid_user, $url)) {          echo 'Deleted '.htmlspecialchars($url).'.<br>';        } else {          echo 'Could not delete '.htmlspecialchars($url).'.<br>';        }      }    } else {      echo 'No bookmarks selected for deletion';    }  }

  // get the bookmarks this user has saved  if ($url_array = get_user_urls($valid_user)) {    display_user_urls($url_array);  }

  display_user_menu();  do_html_footer();?>

Implementing Bookmark Storage and Retrieval

593

You begin this script by performing the usual validations. When you know that the user has selected some bookmarks for deletion, you delete them in the following loop:

foreach($del_me as $url) {  if (delete_bm($valid_user, $url)) {    echo 'Deleted '.htmlspecialchars($url).'.<br>';  } else {    echo 'Could not delete '.htmlspecialchars($url).'.<br>';  }}

As you can see, the delete_bm() function does the actual work of deleting the bookmark from the database. This function is shown in Listing 27.25.

Listing 27.25 

 delete_bm()Function in url_fns.php—This Function Deletes a Single Bookmark from a User's List

function delete_bm($user, $url) {  // delete one URL from the database  $conn = db_connect();

  // delete the bookmark  if (!$conn->query("delete from bookmark where                    username='".$user."'                     and bm_url='".$url."'")) {     throw new Exception('Bookmark could not be deleted');  }  return true;}

As you can see, delete_bm() is also a pretty simple function. It attempts to delete the bookmark for a particular user from the database. Note that you want to remove a particular username-bookmark pair in this case. Other users might still have this URL bookmarked.

Some sample output from running the deletion script on the system is shown in Figure 27.10.

594

Chapter 27  Building User Authentication and Personalization

Figure 27.10  The deletion script notifies the user of deleted bookmarks and then displays the remaining bookmarks

As in the add_bms.php script, after the changes to the database have been made, you display the new bookmark list using get_user_urls() and display_user_urls().

Implementing RecommendationsFinally, you’re ready for the link recommender script, recommend.php. There are many  different ways you could approach recommendations. You should perform what we call a「like minds」recommendation. That is, look for other users who have at least one bookmark the same as your given user. The other bookmarks of those other users might appeal to your given user as well.

The easiest way to implement this as an SQL query is to use subqueries. The first subquery looks like this:

select distinct(b2.username)from bookmark b1, bookmark b2where b1.username='".$valid_user."'and b1.username != b2.usernameand b1.bm_URL = b2.bm_URL)

Implementing Recommendations

595

This query uses aliases to join the database table bookmark to itself—a strange but sometimes useful concept. Imagine that you actually have two bookmark tables, one called b1 and one called b2. In b1, you look at the current user and his bookmarks. In the other table, you look at the bookmarks of all the other users. You are looking for other users (b2.username) who have an URL the same as the current user (b1.bm_URL = b2.bm_URL) and are not the current user (b1.username != b2.username).

This query gives you a list of like-minded people to your current user. Armed with this list, you can search for their other bookmarks with the outer query:

select bm_URLfrom bookmarkwhere username in            (select distinct(b2.username)            from bookmark b1, bookmark b2            where b1.username='".$valid_user."'            and b1.username != b2.username            and b1.bm_URL = b2.bm_URL)

You add a second subquery to filter out the current user’s bookmarks; if the user already has a bookmark, there’s no point in recommending it. Finally, you add some filtering with the $popularity variable. You don’t want to recommend any URLs that are too personal, so you suggest only URLs that a certain number of other users in the list of like-minded users have bookmarked. The final query looks like this:

select bm_URLfrom bookmarkwhere username in         (select distinct(b2.username)         from bookmark b1, bookmark b2         where b1.username='".$valid_user."'         and b1.username != b2.username         and b1.bm_URL = b2.bm_URL)and bm_URL not in         (select bm_URL         from bookmark         where username='".$valid_user."')group by bm_urlhaving count(bm_url)>".$popularity;

If you were anticipating many users using your system, you could adjust $popularity upward to suggest only URLs that have been bookmarked by a large number of users. URLs bookmarked by many people might be higher quality and certainly have more general appeal than an average web page.

The full script for making recommendations is shown in Listings 27.26 and 27.27. The main script for making recommendations is called recommend.php (see Listing 27.26). It calls the recommender function recommend_urls() from url_fns.php (see Listing 27.27).

596

Chapter 27  Building User Authentication and Personalization

Listing 27.26 

 recommend.php—This Script Suggests Some Bookmarks That a User Might Like

<?php  require_once('bookmark_fns.php');  session_start();  do_html_header('Recommending URLs');  try   {    check_valid_user();    $urls = recommend_urls($_SESSION['valid_user']);    display_recommended_urls($urls);  }  catch(Exception $e)   {    echo $e->getMessage();  }  display_user_menu();  do_html_footer();?>

Listing 27.27 

 recommend_urls()Function from url_fns.php—This Function Works Out the Actual Recommendations

function recommend_urls($valid_user, $popularity = 1) {  // We will provide semi intelligent recommendations to people  // If they have an URL in common with other users, they may like  // other URLs that these people like  $conn = db_connect();   // find other matching users  // with an url the same as you  // as a simple way of excluding people's private pages, and  // increasing the chance of recommending appealing URLs, we  // specify a minimum popularity level  // if $popularity = 1, then more than one person must have  // an URL before we will recommend it   $query = "select bm_URL            from bookmark            where username in              (select distinct(b2.username)               from bookmark b1, bookmark b2               where b1.username='".$valid_user."'               and b1.username != b2.username               and b1.bm_URL = b2.bm_URL)            and bm_URL not in               (select bm_URL                from bookmark                where username='".$valid_user."')

Implementing Recommendations

597

            group by bm_url            having count(bm_url)>".$popularity;

  if (!($result = $conn->query($query))) {     throw new Exception('Could not find any bookmarks to recommend.');  }

  if ($result->num_rows==0) {     throw new Exception('Could not find any bookmarks to recommend.');  }

  $urls = array();  // build an array of the relevant urls  for ($count=0; $row = $result->fetch_object(); $count++) {     $urls[$count] = $row->bm_URL;  }

  return $urls;}

Some sample output from recommend.php is shown in Figure 27.11.

Figure 27.11  The recommend.php script has recommended that this user might like espn.com. At least two other users in the database who both like espn.com have this site bookmarked

598

Chapter 27  Building User Authentication and Personalization

Considering Possible ExtensionsIn the preceding sections, we described the basic functionality of the PHPbookmark  application. There are many possible extensions. For example, you might consider adding

 ■ A grouping of bookmarks by topic

 ■ An「Add this to my bookmarks」link for recommendations

 ■ Recommendations based on the most popular URLs in the database or on a particular 

topic

 ■ An administrative interface to set up and administer users and topics

 ■ Ways to make recommended bookmarks more intelligent or faster

 ■ Additional error checking of user input

Experiment! It’s the best way to learn.

