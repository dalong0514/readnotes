16Implementing Authentication Methods with PHP

In this chapter, we discuss how to implement various PHP and MySQL techniques for authenticating users.

Key topics covered in this chapter include

 ■ Identifying visitors

 ■ Implementing access control

 ■ Using basic authentication

 ■ Using basic authentication in PHP

 ■ Using Apache’s .htaccess basic authentication

Identifying VisitorsThe web is a fairly anonymous medium, but it is often useful to know who is visiting your site. With a little work, servers can find out quite a lot about the computers and networks that connect to them, however. A web browser usually identifies itself, telling the server what browser, browser version, and operating system a user is running. You can often determine what resolution and color depth visitors’ screens are set to and how large their web browser windows are by using JavaScript.

Each computer connected to the Internet has a unique IP address. From a visitor’s IP address, you might be able to deduce a little about him or her. You can find out who owns an IP and make a reasonable guess as to a visitor’s geographic location. Some addresses are more 

366

Chapter 16  Implementing Authentication Methods with PHP

useful than others. Generally, people with permanent Internet connections have a permanent IP address. Customers dialing into an ISP usually get only the temporary use of one of the ISP’s addresses. The next time you see that address, it might be used by a different computer, and the next time you see that visitor, he or she will likely be using a different IP address. Mobile devices add another level of complexity. The key thing is that IP addresses are not as useful for identifying people as they might seem at first glance.

Fortunately for web users, none of the information that their browsers give out identifies them personally. If you want to know a visitor’s name or other details, you will have to ask him or her.

Many websites provide compelling reasons to get users to provide their details. More and more websites provide content for free, but only to people willing to register an account and log in. Most e-commerce sites record their customers’ details when they make their first order. This means that a customer is not required to type his or her details every time.

Having asked for and received information from your visitor, you need a way to associate the information with the same user the next time he or she visits. If you are willing to make the assumption that only one person visits your site from a particular account on a particular machine and that each visitor uses only one machine, you could store a cookie on the user’s machine to identify the user.

This arrangement is certainly not true for all users. Many people share a computer, and many people use more than one computer or mobile device. At least some of the time, you need to ask a visitor who he or she is again. In addition to asking who a user is, you also need to ask the user to provide some level of proof that he or she is who the user claims to be.

Asking a user to prove his or her identity is called authentication. The most common method of authentication used on websites is asking visitors to provide a unique login name and a  password. Authentication is usually used to allow or disallow access to particular pages or resources, but can be optional, or used for other purposes such as personalization.

Implementing Access ControlSimple access control is not difficult to implement. The code shown in Listing 16.1 delivers one of three possible outputs. If the file is loaded without parameters, it will display an HTML form requesting a username and password. This type of form is shown in Figure 16.1.

Listing 16.1  secret.php—PHP and HTML to Provide a Simple Authentication Mechanism<!DOCTYPE html><html><head>   <title>Secret Page</title></head><body>

Implementing Access Control

367

<?php  if ((!isset($_POST['name'])) || (!isset($_POST['password']))) {  // visitor needs to enter a name and password?>    <h1>Please Log In</h1>    <p>This page is secret.</p>    <form method="post" action="secret.php">    <p><label for="name">Username:</label>     <input type="text" name="name" id="name" size="15" /></p>    <p><label for="password">Password:</label>     <input type="password" name="password" id="password" size="15" /></p>    <button type="submit" name="submit">Log In</button>        </form><?php  } else if(($_POST['name']=='user') && ($_POST['password']=='pass')) {    // visitor's name and password combination are correct    echo '<h1>Here it is!</h1>          <p>I bet you are glad you can see this secret page.</p>';  } else {    // visitor's name and password combination are not correct    echo '<h1>Go Away!</h1>          <p>You are not authorized to use this resource.</p>';  }?></body></html>

Figure 16.1  This HTML form requests that visitors enter a username and password for access

368

Chapter 16  Implementing Authentication Methods with PHP

If the supplied credentials are not correct, it will display an error message. A sample error message is shown in Figure 16.2.

Figure 16.2  When users enter incorrect details, you need to give them an error message. On a real site, you might want to give a somewhat friendlier message

If these parameters are present and correct, it will display the secret content. The sample test content is shown in Figure 16.3.

Figure 16.3  When provided with correct details, the script displays content

Implementing Access Control

369

The code to create the functionality shown in Figures 16.1–16.3 is shown in Listing 16.1.

The code from Listing 16.1 provides a simple authentication mechanism to allow authorized users to see a page, but it has some significant problems:

 ■ Has one username and password hard-coded into the script

 ■ Stores the password as plain text

 ■ Protects only one page

 ■ Transmits the password as plain text

These issues can all be addressed with varying degrees of effort and success.

Storing PasswordsThere are many better places to store usernames and passwords than inside the script. Inside the script, modifying the data is difficult. It is possible, but a bad idea, to write a script to modify itself. Doing so would mean having a script on your server that is executed on your server but that can be written or modified by others. Storing the data in another file on the server lets you more easily write a program to add and remove users and to alter passwords.

Inside a script or another data file, you are limited to the number of users you can have without seriously affecting the speed of the script. If you are considering storing and  searching through a large number of items in a file, you should use a database instead, as previously discussed. As a rule of thumb, if you want to store and search through a list of more than a handful of items, they should be in a database rather than a flat file.

Using a database to store usernames and passwords would not make the script much more complex but would allow you to authenticate many different users quickly. It would also allow you to easily write a script to add new users, delete users, and allow users to change their passwords. When storing passwords in a database, however, be sure not to store plain text passwords. Instead, it is common to store hashes of passwords (created using the built-in PHP md5() function, for example, and comparing the hashed value of the user’s form input to the hashed value stored in the database table. Using this approach, you can still authenticate a user who is attempting to gain access to your protected resource, but you are not storing any actual passwords. 

Securing PasswordsRegardless of whether you store your data in a database or a file, storing the passwords as plain text is an unnecessary risk. A one-way hashing algorithm can provide better security with very little extra effort.

370

Chapter 16  Implementing Authentication Methods with PHP

In older versions of PHP, it was typical practice to explicitly use one of the provided one-way hash functions. The oldest and least secure is the Unix Crypt algorithm, provided by the function crypt(). Then there’s the Message Digest 5 (MD5) algorithm, implemented in the function md5(). More recently people have used Secure Hashing Algorithm functions such as sha1() and sha256(), among others.

The problem with explicitly specifying a hash function is that as time passes, hashing  algorithms become insecure. How does this happen? Security researchers find a way to break the hash. This becomes easier as computing power increases, too.

As of PHP 5.5, and still present in PHP 7, a function called password_hash()applies a strong one-way hashing function to a string. The prototype for this function is

string password_hash ( string $password , integer $algo [, array $options ] )

Because the algorithm to use is a variable, this enables you to change the hashing algorithm by changing configuration instead of code, and by changing it in a single place.

One other nice thing here is that there is a constant called PASSWORD_DEFAULT, which you can pass in as the name of the hashing algorithm. PHP will update the value of this over versions to keep it pointed at a secure algorithm. The default algorithm is CRYPT_BLOWFISH, which you can also specify explicitly by passing in PASSWORD_BCRYPT as the $algo parameter. 

With PASSWORD_BCRYPT, it will also generate a salt for you. A salt, in this context, is a randomly generated piece of data added to the password before hashing. It makes it more  difficult for someone to guess a password.

Given the string $password and the PASSWORD_BCRYPT function, this function will return a 60-character hash. Strings returned by password_hash() contain all the information necessary to reproduce the hash. This includes the algorithm used and the salt.

This string cannot be decrypted and turned back into the original string even by its creator, so it might not seem very useful at first glance. The property that makes such hashing functions useful is that the output is deterministic. Given the same string, it will return the same result every time it is run.

Rather than having PHP code like

if (($name == 'username') &&     ($password == 'password')) {  // OK passwords match}

you can have code like

if (password_verify($password, $hash)) {  // OK passwords match}

You do not need to know what the password looked like before you used the hashing function on it. You need to know only if the hash of the password typed in is the same as the hash of the password that has been set previously.

Implementing Access Control

371

As already mentioned, hard-coding acceptable usernames and passwords into a script is a bad idea. You should use a separate file or a database to store them.

Keep in mind that the hash functions generally return data of a fixed size. In the case of PASSWORD_BCRYPT, it is 60 characters when represented as a string. Future algorithms may generate longer hashes, so you should make sure that your database column has space for such future expansion—255 characters is a reasonable length for now.

Protecting Multiple PagesMaking a script like the ones in the previous section protect more than one page is a little harder. Because HTTP is stateless, there is no automatic link or association between subsequent requests from the same person. This makes it harder to have data, such as authentication information that a user has entered, carry across from page to page.

The easiest way to protect multiple pages is to use the access control mechanisms provided by your web server. We look at these mechanisms shortly.

To create this functionality yourself, you could include parts of the script shown in Listing 16.1 in every page that you want to protect. Using auto_prepend_file and auto_append_file, you can automatically prepend and append the code required to every file in particular  directories. The use of these directives was discussed in Chapter 5,「Reusing Code and Writing Functions.」

If you use this approach, what happens when your visitors go to multiple pages within your site? Requiring them to re-enter their names and passwords for every page they want to view would not be acceptable.

You could append the details the users entered to every hyperlink on the page. Because they might have spaces or other characters that are not allowed in URLs, you could use the function urlencode() to safely encode these characters.

This approach still has a few problems, though. Because the data would be included in web pages sent to the users and the URLs they visit, the protected pages they visit will be visible to anybody who uses the same computer and steps back through cached pages or looks at the browser’s history list. Because you are sending the password back and forth to the browser with every page requested or delivered, this sensitive information is being transmitted more often than necessary.

There are two good ways to tackle these problems: HTTP basic authentication and sessions. Basic authentication overcomes the caching problem, but the browser still sends the  password to the server with every request. Session control overcomes both of these problems. We look at HTTP basic authentication now and examine session control in Chapter 22,「Using Session Control in PHP,」and in more detail in Chapter 27,「Building User Authentication and Personalization.」

372

Chapter 16  Implementing Authentication Methods with PHP

Using Basic AuthenticationFortunately, authenticating users is a common task, so authentication facilities are built into HTTP. Scripts or web servers can request authentication from a web browser. The web browser is then responsible for displaying a dialog box or similar device to obtain required information from the user.

Although the web server requests new authentication details for every user request, the web browser does not need to request the user’s details for every page. The browser generally stores these details for as long as the user has a browser window open and automatically resends them to the web server as required without user interaction.

This feature of HTTP is called basic authentication. You can trigger basic authentication using PHP or using mechanisms built into your web server. We look first at the PHP method and then the Apache method.

When you combine basic authentication with SSL and digital certificates, all parts of a web transaction can be protected by strong security.

Basic authentication protects a named realm and requires users to provide a valid username and password. Realms are named so that more than one realm can be on the same server. Different files or directories on the same server can be part of different realms, each protected by a  different set of names and passwords. Named realms also let you group multiple directories on the one host or virtual host as a realm and protect them all with one password.

Using Basic Authentication in PHPPHP scripts are generally cross-platform, but using basic authentication relies on environment variables set by the server. The code in Listing 16.2 has been tested against the Apache web server.

Listing 16.2  basic_auth.php—PHP Can Trigger HTTP Basic Authentication<?phpif ((!isset($_SERVER['PHP_AUTH_USER'])) &&    (!isset($_SERVER['PHP_AUTH_PW'])) &&    (substr($_SERVER['HTTP_AUTHORIZATION'], 0, 6) == 'Basic ')   ) {

  list($_SERVER['PHP_AUTH_USER'], $_SERVER['PHP_AUTH_PW']) =    explode(':', base64_decode(substr($_SERVER['HTTP_AUTHORIZATION'], 6)));}

// Replace this if statement with a database query or similarif (($_SERVER['PHP_AUTH_USER'] != 'user') ||   ($_SERVER['PHP_AUTH_PW'] != 'pass')) {

   // visitor has not yet given details, or their   // name and password combination are not correct

Using Basic Authentication in PHP

373

  header('WWW-Authenticate: Basic realm="Realm-Name"');  header('HTTP/1.0 401 Unauthorized');} else {?><!DOCTYPE html><html><head>   <title>Secret Page</title></head><body><?php

echo '<h1>Here it is!</h1>      <p>I bet you are glad you can see this secret page.</p>';}?></body></html>

The code in Listing 16.2 acts similarly to the previous listing in this chapter: if the user has not yet provided authentication information, it will be requested. If the user provides a matching name-password pair, he or she is presented with the contents of the page.

In this case, the user will see an interface somewhat different from the previous listings. This script does not provide an HTML form for login information. The user’s browser presents him or her with a dialog box. Some people see this as an improvement; others would prefer to have complete control over the visual aspects of the interface. A sample dialog box, in this instance provided from Firefox, is shown in Figure 16.4.

Figure 16.4  The user’s browser is responsible for the appearance of the dialog box when using HTTP authentication

374

Chapter 16  Implementing Authentication Methods with PHP

Using Basic Authentication with Apache’s .htaccess FilesYou can achieve similar results to the script in Listing 16.2 without writing a PHP script.

The Apache web server contains a number of different authentication modules that can be used to decide the validity of data entered by a user. To use HTTP Basic authentication, you’ll need mod_auth_basic, plus an authentication module corresponding to the password storage  mechanism you plan to use. In this section, we’ll look at how to store passwords in a file, and in the next section, we’ll look at how to store them in a database.

To get the same output as the preceding script, you need to create two separate HTML files: one for the content and one for the rejection page. We skipped some HTML elements in the  previous examples but really should include <html> and <body> tags when generating HTML.

Listing 16.3, named content.html, contains the content that authorized users see. Listing 16.4, called rejection.html, contains the rejection page. Having a page to show in case of errors is optional, but it is a nice, professional touch if you put something useful on it. Given that this page will be shown when a user attempts to enter a protected area but is rejected, useful content might include instructions on how to register for a password, or how to get a password reset and emailed if it has been forgotten.

Listing 16.3  content.html—Sample Content<!DOCTYPE html><html><head>   <title>Secret Page</title></head><body>   <h1>Here it is!</h1>   <p>I bet you are glad you can see this secret page.</p></body></html>

Listing 16.4  rejection.html—Sample 401 Error Page<!DOCTYPE html> <html><head>   <title>Rejected Page</title></head><body>   <h1>Go Away!</h1>   <p>You are not authorized to view this resource.</p></body></html> 

Using Basic Authentication with Apache’s .htaccess Files 

375

There is nothing new in these files. The interesting file for this example is Listing 16.5. This file needs to be called .htaccess and will control accesses to files and any subdirectories in its directory.

Listing 16.5 

 htaccess—An .htaccess File Can Set Many Apache Configuration Settings, Including Activating Authentication

AuthUserFile /var/www/.htpass                                  AuthType Basic                                                  AuthName "Authorization Needed"                                 AuthBasicProvider file                                          Require valid-user                                              ErrorDocument 401 /var/www/pmwd53/chapter16/rejection.html 

Listing 16.5 is an .htaccess file to turn on basic authentication in a directory. Many settings can be made in an .htaccess file, but the six lines in this example all relate to authentication.

The line

AuthUserFile /var/www/.htpass       

tells Apache where to find the file that contains authorized users’ passwords. This file is often named .htpass, but you can give it any name you prefer. It is not important what you call this file, but it is important where you store it. It should not be stored within the web tree— somewhere that people can download it via the web server. The sample .htpass file is shown in Listing 16.6.

Because a number of different authentication methods are supported, you need to specify which authentication method you are using. Here, you use Basic authentication, as specified by this directive:

AuthType Basic

Like the PHP example, to use HTTP Basic authentication, you need to name the realm as follows:

AuthName "Authorization Needed"

You can choose any realm name you prefer, but bear in mind that the name will be shown to your visitors. We named ours "Authorization Needed".

You need to specify what authentication provider is being used. In this case, we’re using a file, and specify it as follows:

AuthBasicProvider file  

You also need to specify who is allowed access. You could specify particular users, particular groups, or as we have done, simply allow any authenticated user access. The line

Require valid-user

specifies that any valid user is to be allowed access.

376

Chapter 16  Implementing Authentication Methods with PHP

The line

ErrorDocument 401 /var/www/pmwd5e/chapter16/rejection.html

tells Apache what document to display for visitors who fail to authenticate (HTTP error number 401). You can use other ErrorDocument directives to provide your own pages for other HTTP errors such as 404. The syntax is

ErrorDocument error_number URL

Listing 16.6 

 htpass—The Password File Stores Usernames and Each User’s Encrypted Password

user1:$apr1$2dTEuqf0$ok6jSPLkWoswioQyqTwdv.user2:$apr1$9aA0xUxC$pphrV4GqGahOwGI5qTerE1user3:$apr1$c2xbFr5F$dOLbi4NG8Ton0bOmRBw/11user4:$apr1$vjxonbG2$PPZyfInUnu2vDcpiO.lPZ0

Each line in the .htpass file contains a username, a colon, and that user’s hashed password.

The exact contents of your .htpass file will vary. To create it, you use a small program called htpasswd that comes in the Apache distribution.

The htpasswd program supports a large number of options. Commonly, it’s used as follows:

htpasswd -b[c] passwordfile username password

Using the -c switch tells htpasswd to create the file. You must use this for the first user you add. Be careful not to use it for other users because, if the file exists, htpasswd will delete it and create a new one.

The b switch tells the program to expect the password as a parameter rather than prompt for it. This feature is useful if you want to call htpasswd noninteractively as part of a batch process, but you should not use it if you are calling htpasswd from the command line because  passwords will be retained in history.

The following commands created the file shown in Listing 16.6:

htpasswd -bc /var/www/.htpass user1 pass1htpasswd -b /var/www/.htpass user2 pass2htpasswd -b /var/www/.htpass user4 pass3htpasswd -b /var/www/.htpass user4 pass4

Note that htpasswd may not be in your path: If it is not, you may need to supply the full path to it. On many systems, you will find it in the /usr/local/apache/bin directory.

This sort of authentication is easy to set up, but there are a few problems with using an .htaccess file this way.

Users and passwords are stored in a text file. Each time a browser requests a file that is protected by the .htaccess file, the server must parse the .htaccess file and then parse the password file, attempting to match the username and password. Instead of using an .htaccess file, 

Next

377

you could specify the same things in your httpd.conf file—the main configuration file for the web server. An .htaccess file is parsed every time a file is requested. The httpd.conf file is parsed only when the server is initially started. This approach is faster, but means that if you want to make changes, you need to stop and restart the server.

Regardless of where you store the server directives, the password file still needs to be searched for every request. This means that, like other techniques we have looked at that use a flat file, this would not be appropriate for hundreds or thousands of users.

For many simple websites, mod_auth_basic against a file is ideal. It is fast and relatively easy to implement, and it allows you to use any convenient mechanism to add database entries for new users. You can also use it with a database, but for more flexibility and the ability to apply fine-grained control to parts of pages, you can implement your own authentication using PHP and MySQL.

Creating Your Own Custom AuthenticationIn this chapter, you looked at creating your own authentication methods including some flaws and compromises and using built-in authentication methods, which are less flexible than writing your own code. Later in the book, after you learn about session control, you will be able to write your own custom authentication with fewer compromises than in this chapter.

In Chapter 22, we develop a simple user authentication system that avoids some of the problems we faced here by using sessions to track variables between pages.

In Chapter 27, we apply this approach to a real-world project and see how it can be used to implement a fine-grained authentication system.

Further ReadingThe details of HTTP authentication are specified by RFC 2617, which is available at http://www.rfc-editor.org/rfc/rfc2617.txt

The documentation for mod_auth_basic, which controls basic authentication in Apache, can be found at https://httpd.apache.org/docs/2.4/mod/mod_auth_basic.html.

NextThe next section of this book covers some more advanced PHP techniques, including working with the file system, using session control, implementing localization, and other useful features.

This page intentionally left blank 

