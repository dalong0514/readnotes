15Building a Secure Web Application

In this chapter we continue the task of looking at application security, looking at the broader theme of securing our entire web application. Indeed, every single part of our web applications will need to be secured from possible misuse (accidental or intentional), and we will want to develop some strategies to developing our application that will help us stay secure.

Key topics covered in this chapter include

 ■ Strategies for dealing with security

 ■ Securing your code

 ■ Securing your web server and PHP

 ■ Database server security

 ■ Protecting the network

 ■ Disaster planning

Strategies for Dealing with SecurityOne of the greatest features of the Internet—the openness and accessibility of all machines to each other—also turns out to be one of the biggest headaches that you as a web application author have to face. With so many computers out there, the users of some are bound to have less than noble intentions. With all this danger swirling around us, it can be intimidating to think about exposing a web application dealing with potentially confidential information such as credit card numbers, bank account information, or health records to the global network. But business must go on, and we as the authors must look beyond simply securing the e-commerce portions of our application, and develop an approach to planning for and dealing with security. The key is to find one with the appropriate balance between the need to protect ourselves and the need to actually do business and have a working application.

342

Chapter 15  Building a Secure Web Application

Start with the Right MindsetSecurity is not a feature. When you are writing a web application and deciding the list of features that you want to include, security is not something that you casually include in the list and assign a developer to work on for a couple of days. It must be constantly part of the core design of the application, and it is a never-ending effort, even after the application is deployed and development has slowed, if not outright ceased.

By thinking of and planning for, right from the beginning, the various ways in which our system could be abused or through which attackers might try to compromise it, we can design our code to reduce the likelihood of these problems occurring. This also saves us having to try to retrofit everything later on when we finally do turn our attention to the problem (when we are almost certain to miss many more potential problems).

Balancing Security and UsabilityOne of the greatest concerns we have when designing a system is user passwords. Users will often choose passwords that are not particularly difficult to crack with software, especially when they use words readily available in dictionaries. We would like a way to reduce the risk of a user’s password being guessed and our system being compromised through this.

One possible solution is to require each user to go through four login dialogs, each with a separate password. We can also require that the user change these four passwords at least once a month and make sure the user never uses a password he or she has used in the past. We could require these passwords to be very long, and include many different character classes (uppercase, lowercase, punctuation, and numbers, for example). This would make our system much more secure, and crackers would have to spend significantly more time getting through the login process and into the compromised system.

Unfortunately, our system would be so secure that nobody would bother to use it—at some point they would decide that it was simply not worth it. This illustrates the point that just as it is important to worry about security, it is also important to worry about how this affects usability. An easy-to-use system with little security might prove attractive to users, but will also result in a higher probability of security-related problems and possible business interruptions. Similarly, a system with security that is so robust as to be borderline unusable will attract few users and also very negatively affect our business.

As web application designers, we must look for ways to improve our security without disproportionately affecting the usability of the system. As with all things related to the user interface, there are no hard and fast rules to follow, so instead we must rely on some personal judgment, usability testing, and focus groups to see how users react to our prototypes and designs.

Monitoring SecurityAfter we finish developing our web application and deploy it to production servers for people to begin using, our job is not complete. Part of security is monitoring the system as it operates, 

Securing Your Code

343

looking at logs and other files to see how the system is performing and being used. Only by keeping a close eye on the operation of the system (or by writing and running tools to do portions of this for us), can we see whether ongoing security problems exist and find areas where we might need to spend some time developing more secure solutions.

Security is, unfortunately, an ongoing battle and, in a certain hyperbolic sense, a battle that can never be won. Constant vigilance, improvements to our system, and rapid reaction to any problems are the price to be paid for a smoothly operating web application.

Our Basic ApproachTo give ourselves the most complete security solution possible for reasonable effort and time, we describe in this book a twofold approach to security. The first part falls along the lines of what we have discussed thus far: how to plan for securing our application and designing features into it that will help keep it safe. Were we compulsive labelers, we might call this a top-down approach.

In contrast, we might call the second part of our security approach a bottom-up approach. This is what we will cover in this chapter. In this phase we look at all the individual components in our application, such as the database server, the server itself, and the network on which it resides. We try to ensure that not only are our interactions with these components safe, but that the installation and configuration of these components is safe. Many products install with default configurations that leave us open to attack, and we would do well to learn about these holes and plug them.

Securing Your CodeMaking a good effort at securing your code requires you to think at a granular level, including inspecting each of the components individually and looking at how to improve their security. We begin in this section by investigating the things we can do to help keep our code safe. Although we cannot show you everything you might want to do to cover all possible security threats (entire tomes have been devoted to these subjects), we can at least give some general guidelines and point you in the right direction.

Filtering User InputOne of the most important things we can do in our web applications to make them more secure is to filter all user input. 

Application developers must filter all input that comes from external sources. This does not mean that we should design a system with the assumption that all our users are crooks. We still want them to feel welcome and indeed encourage them to use our web application. We just want to be sure that we are prepared at any point for misuse of our system.

If we do this filtering effectively, we can reduce the number of external threats substantially and massively improve the robustness of our system. Even if we are pretty sure that we trust 

344

Chapter 15  Building a Secure Web Application

the users, we cannot be certain that they do not have some type of spyware program or other such thing that is modifying or sending new requests to our server. So really, never trust the users.

Given the importance of filtering the input we get from external customers, we should take a look at the ways in which we might do this.

Double-Checking Expected ValuesAt times we will present the user with a range of possible values from which to choose, for things such as shipping (ground, express, overnight), state or province, and so on. Now, imagine if we were to have the following simple form, as shown in Listing 15.1:

Listing 15.1  simple_form.html—Just a Simple Form<!DOCTYPE html><html><head>   <title>What be ye laddie?</title></head><body><h1>What be ye laddie?</h1>

<form action="submit_form.php" method="post">

<p><input type="radio" name="gender" id="gender_m" value="male" />   <label for="gender_m">male</label><br/>

<input type="radio" name="gender" id="gender_f" value="female" />   <label for="gender_f">female</label><br/>

<input type="radio" name="gender" id="gender_o" value="other" />   <label for="gender_o">other</label><br/></p>

<button type="submit" name="submit">Submit Form</button></form>

</body></html>

This form could look as shown in Figure 15.1. Given this form, we might assume that whenever we query the value of $_POST['gender'] in submit_form.php, we are going to get one of the values 'male', 'female', or 'other'—and we would be completely wrong.

Securing Your Code

345

Figure 15.1  A Trivial Little Form

As we mentioned previously, the web operates using HTTP, a simple text protocol. The preceding form submission would be sent to our server as a text message with a structure similar to the following:

POST /submit_form.php HTTP/1.1Host: www.yourdomain.comUser-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:40.0) Gecko/20100101 Firefox/40.0Content-Type: application/x-www-form-urlencodedContent-Length: 11gender=male

However, there is absolutely nothing stopping somebody from connecting to our web server and sending whatever values they want. Thus, somebody can send us the following:

POST /submit_form.php HTTP/1.1Host: www.yourdomain.comUser-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:40.0) Gecko/20100101 Firefox/40.0Content-Type: application/x-www-form-urlencodedContent-Length: 22gender=I+like+cookies.

If we were to then write the following code:

<?phpecho "<h1>      The user's gender is: ".$_POST['gender']. ".      </h1>";?>

346

Chapter 15  Building a Secure Web Application

We might find ourselves somewhat confused later on. A much better strategy is to actually verify that the incoming value is actually one of the expected/permitted values, as shown in Listing 15.2: 

Listing 15.2  submit_form.php—Verifying Form Input<?php                                                                           switch ($_POST['gender']) {                                                        case 'male':                                                                    case 'female':                                                                  case 'other':                                                                

      echo "<h1>Congratulations!<br/>                                          You are: ".$_POST['gender']. ".</h1>";                                   break;                                                                       

   default:                                                                     

      echo "<h1><span style=\"color:  red;\">WARNING:</span><br/>                                    Invalid input value specified.</h1>";                         break;                                                                       }                                                                               ?>

There is a little bit more code involved here—setting up the list of valid input—but we can at least be sure we are getting correct values, and this becomes a lot more important when we start handling data values more financially sensitive than a user’s selected gender. As a rule, we cannot ever assume that a value from a form will be within a set of expected values—we must check first. 

Filtering Even Basic ValuesHTML form elements have no types associated with them and most simply pass strings (which may, in turn, represent things such as dates, times, or numbers) to the server. Thus, even if you have a numeric field, you cannot assume or trust that it was truly entered as such. Even in environments where particularly powerful client-side code can try to make sure that the value entered is of a particular type, there is no guarantee that the values will not be sent to the server directly, as we saw in the previous section.

An easy way to make sure that a value is of the expected type is to cast or convert it to that type and then use that value, as follows:

  $number_of_nights = (int)$_POST['num_nights'];  if ($number_of_nights == 0)  {    echo "ERROR: Invalid number of nights for the room!";    exit;  }

Securing Your Code

347

If we have the user input a date in some localized format, such as mm/dd/yy for users in the United States, we can then write some code to make sure it is a real date using the PHP  function called checkdate(). This function takes a month, day, and year value (two-digit years), and indicates whether they, combined, form a valid date:

  $mmddyy = explode('/', $_POST['departure_date']);             if (count($mmddyy) != 3)                                        {                                                                 echo "ERROR: Invalid Date specified!";                          exit;                                                         }                                                             

  // handle years like 02 or 95                                   if ((int)$mmddyy[2] < 100)                                      {                                                                 if ((int)$mmddyy[2] > 50) {                                         $mmddyy[2] = (int)$mmddyy[2] + 1900;                          } else if ((int)$mmddyy[2] >= 0) {                                    $mmddyy[2] = (int)$mmddyy[2] + 2000;                          }                                                                // else it's < 0 and checkdate will catch it                  }                                                             

  if (!checkdate($mmddyy[0], $mmddyy[1], $mmddyy[2]))             {                                                                 echo "ERROR: Invalid Date specified!";                          exit;                                                         }    

By taking the time to filter and validate the input, not only can we help ourselves out for natural error-checking that we should be doing in the first place (such as verifying whether a departure date for a plane ticket is a valid date), but we can also help improve the security of our system. 

Making Strings Safe for SQLOne other case where we want to process our strings to make them safe is to prevent SQL injection attacks, which were mentioned when first looking at using MySQL in PHP. In these attacks, the malicious user tries to take advantage of poorly protected code and user permissions to execute extra SQL code that we do not necessarily want them to. If we are not careful, a username of

  kitty_cat; DELETE FROM users;

could become quite a problem for us.

You can use two primary methods in parallel to prevent this sort of security breach:

 ■ Use parameterized queries wherever possible. These queries separate SQL from data. The case where this won’t help you is for column and table names, as these cannot be passed 

348

Chapter 15  Building a Secure Web Application

via parameterized query. However, because you have a priori knowledge of your schema, you can whitelist appropriate values.

 ■ Make sure that all input conforms to what you expect it to be. If our usernames are 

supposed to be up to 50 characters long and include only letters and numbers, we can be sure that "; DELETE FROM users" at the end of it is probably something we would not want to permit. Writing the PHP code to make sure input conforms to the appropriate possible values before we even send it to the database server means we can print out a much more meaningful error than the database would give us (were it checking such things), and reduce our risks.

The mysqli extension has the added security advantage of allowing only a single query to execute with the mysqli_query or mysqli::query methods. To execute multiple queries, you have to use the mysqli_multi_query or mysqli::multi_query methods, which help us prevent the execution of additional potentially harmful statements or queries. 

Escaping OutputOf nearly equal importance to filtering our input is what we’ll call escaping our output. After we have user values in our system, it is critical that we be sure that these cannot do any damage or cause any unintended consequences. We do this by using a couple of key functions to ensure that values cannot be mistaken by the client web browser for anything other than display text.

Many web applications take the input a user has specified and display it on a page. Pages where users can comment on a published article or message board systems are perfect examples of where this might occur. In these situations, we need to be careful that users do not inject  malicious HTML markup into the text.

One of the easiest ways to do this is to use the htmlspecialchars() function or the  htmlentities() function. These functions take certain characters they see in the input string and convert them to HTML entities. In short, an HTML entity is a special character sequence, begun with the ampersand character (&), used to indicate some special character that cannot easily be represented in HTML code. After the ampersand character comes the entity name and then a terminating semicolon (;). Optionally, an entity can be an ASCII key code specified by # and a decimal number, such as &#47; for the forward slash character (/).

For example, because all markup elements in HTML are demarcated by < and > characters, it could prove difficult to enter them in a string for output to the final content (because the browser will default to assuming they delineate markup elements). To get around this, we use the entities &lt; and &gt;. Similarly, if we want to include the ampersand character in our HTML, we can use the entity &amp;. Single and double quotes are represented by &#39; and &quot;, respectively. Entities are converted into output by the HTML client (web browser) and are thus not considered part of the markup.

The difference between the htmlspecialchars() function and the  htmlentities()  function is as follows: The former defaults to only replacing &, <, and >, with optional switches for single and double quotes. The latter replaces anything that can be represented by 

Securing Your Code

349

a named entity with that named entity. Examples of such entities are the copyright symbol ©,  represented by &copy;, and the Euro currency symbol €, represented by &euro;. It will not convert characters to numeric entities, however.

Both functions take as their second parameter a value that specifies how to handle quotes and invalid code sequences, and both functions also take as an optional third parameter the character set in which the input string is encoded (which is vital for us, because we want this function to be safe on our UTF-8 strings). The five most common values for the second parameter are the following:

 ■ ENT_COMPAT (the default value)—Double quotes are converted to &quot; but single 

quotes are left untouched.

 ■ ENT_QUOTES—Both single and double quotes are converted, to &#39; and &quot;, 

respectively.

 ■ ENT_NOQUOTES—Neither single nor double quotes are converted by this function.

 ■ ENT_IGNORE—Invalid code sequences are silently disregarded.

 ■ ENT_SUBSTITUTE—Invalid code sequences are replaced with a Unicode Replacement 

Character instead of returning an empty string.

 ■ ENT_DISALLOWED—Invalid code sequences are replaced with a Unicode Replacement 

Character instead of leaving them as is. 

Consider the following code snippets: 

$input_str = "<p align=\"center\">The user gave us \"15000?\".</p>              <script type=\"text/javascript\">              // malicious JavaScript code goes here.              </script>";

If we run it through the following PHP script (we run the nl2br function on the output string strictly to ensure that it is formatted nicely in the browser),

<?php

  $str = htmlspecialchars($input_str, ENT_NOQUOTES, "UTF-8");  echo nl2br($str);

  $str = htmlentities($input_str, ENT_QUOTES, "UTF-8");  echo nl2br($str);

?>

We would see the following text output when viewing source in the browser:

&lt;p align="center"&gt;The user gave us "15000?".&lt;/p&gt;<br /><br />&lt;script type="text/javascript"&gt;<br />// malicious JavaScript code goes here.<br />

350

Chapter 15  Building a Secure Web Application

&lt;/script&gt;&lt;p align=&quot;center&quot;&gt;The user gave us &quot;15000&euro;&quot;.&lt;/p&gt;<br /><br />&lt;script type=&quot;text/javascript&quot;&gt;<br />// malicious JavaScript code goes here.<br />&lt;/script&gt;

And it would look as follows in the browser:

<p align="center">The user gave us "15000?".</p>

<script type="text/javascript">// malicious JavaScript code goes here.</script><p align="center">The user gave us "15000?".</p>

<script type="text/javascript">// malicious JavaScript code goes here.</script>

Note that the htmlentities() function replaced the symbol for the Euro currency symbol (€) with an entity (&euro;), whereas the htmlspecialchars() function left it alone.

For those situations where we would like to permit users to enter some HTML, such as a message board where people might like to use characters to control font, color, and style (bold or italicized), we will have to actually pick our way through the strings to find those and not strip them out. 

Code OrganizationA good guideline is that any file not intended to be directly accessible to the user from the Internet should be in the document tree of the website. For example, if the document root for our message board website is /home/httpd/messageboard/www, you should place include files in a location such as /home/httpd/messageboard/lib. Then, in your code, when you want to include those files, you can write:

  require_once('../lib/user_object.php);

There are a couple of reasons to do this.

First, consider what happens when a malicious user makes a request for a file that is not a .php or .html file. Many web servers will default to dumping the contents of that file to the output stream if improperly configured. If you were to keep some_library.inc in the public  document tree, and the user were to request it, the user might see a full dump of your code in the web browser. This may let the user see data or server paths and potentially find exploits that you might have missed.

To fix this, we should be sure that the web server is configured to only allow the request of .php and .html files and that requests for other types of files (such as *.inc, *.mo, *.txt and so on) should return an error from the server.

Securing Your Code

351

Second, even if your files all end in .php, some designed-to-be-included files may have  unintended consequences if loaded out of context. Consider a library of administrative code. You may check for authorization in the usual context, but if a file is loaded alone, the  authorization might be subverted.

Similarly, any other files, such as password files, text files, configuration files, or special  directories must be kept out of the public document tree. Even if you think you have your web server configured properly, you might have missed something, or if, in the future, your web application is moved to a new server that is not properly configured, you might be exposed to exploitation.

If you have allow_url_fopen enabled in your php.ini—and be aware it is enabled by default—then you could theoretically include or require files from remote servers. This is a possible point of security failure in your application, and you should avoid execution of files from separate machines, especially those over which you do not have full control. You should likewise not use user input when choosing which files to include or require, as bad input here could also cause problems. 

What Goes in Your CodeMany of the code snippets you have looked at so far for accessing databases have included in the code the database name, username, and user password in plain text, as follows:

  $conn = new mysqli("localhost", "bob", "secret", "somedb");

Although this is convenient, it is slightly insecure in that if crackers were to get their hands on this file, they would have immediate access to our database with the full permissions that the user bob has.

Better would be to put the username and password in a file that is not in the document tree of the web application, and include it in your script, as follows:

<?php  // this is dbconnect.php  $db_server = 'localhost';  $db_user_name = 'bob';  $db_password  = 'secret';  $db_name = 'somedb';?>

The above file could then be called as:

<?php  include('../code/dbconnect.php');

  $conn = @new mysqli($db_server, $db_user_name, $db_password,                      $db_name);  // etc?>

352

Chapter 15  Building a Secure Web Application

You should think about doing the same thing for other similarly sensitive data for which you might want an additional layer of protection. 

File System ConsiderationsPHP was designed with the capability to work with the local file system in mind. There are two concerns:

 ■ Are any files you write to the disk going to be visible by others?

 ■ If you expose this functionality to others, are they going to be able to access files we 

might not want them to access, such as /etc/passwd?

You have to be careful to not write files with wide open security permissions, or place them in a location where other users in a shared hosting environment could get access to them.

Additionally, you should be extremely careful when you let users enter the name of a file they would like to see. If you had a directory in your document root with a bunch of files you were granting users access to, and they input the name of the file they wanted to view, you could get into trouble if they navigated upward through the directory structure, to something like the following (using Windows filesystem references, for example):

  ..\..\..\php\php.ini

This would let them learn about our PHP installation and see whether any obvious weaknesses exist to exploit. Again, the fix to this problem is easy: if you accept user input, make sure you filter it aggressively. For the preceding example, removing any instances of ..\ would certainly help prevent this problem, as would any attempt at an absolute path such as c:\mysql\my.ini. or /etc/my.cnf.

Code Stability and BugsWe mentioned this briefly before, but your web application is neither likely to perform well nor be terribly secure if the code has not been properly tested, reviewed, or is full of bugs. All of us as programmers are fallible, as is the code we write. 

When a user connects to a website, enters a word in the search box (for example,「defenestration」), and clicks Search, the user is not going to have great confidence in the robustness or security of it if the next thing the user sees is

 This should never happen.  BUG BUG BUG !!!!

If we plan from the beginning for the stability of our application, we can effectively reduce the likelihood of problems due to human error. Ways in which we can do this are as follows:

 ■ Complete a thorough design phase of our product, possibly with prototypes. The more people we have reviewing what we plan to do, the more likely we are to spot problems even before we begin. This is also a great time to do usability testing on our interface.

 ■ Allocate QA/testing resources to our project. So many projects skimp on this, or hire 

perhaps one test engineer for a project with 50 developers. Developers do not typically make 

Securing Your Code

353

good testers! They are very good at making sure their code works with the correct input, but they are less proficient at finding other problems. Some major software companies have a ratio of developers to test engineers of nearly 1:1, and although it may not be likely that our bosses would pay for that many testers, some testing resources will be critical to the success of the application.

 ■ Have your developers use test automation. This might not help us find all the bugs that a tester would, but this will definitely help the product from regressing—a phenomenon in which problems or bugs that were fixed some time ago are reintroduced because of other code changes. Developers should not be allowed to commit recent changes to the project or deploy code unless tests pass.

 ■ Monitor the application as it runs after it is deployed. By browsing regularly through the logs, looking at user/customer comments, you should be able to see if any major problems or possible security holes are cropping up. If so, you can act to address them before they become more serious. 

Executing CommandsWe briefly mentioned a feature previously called the execution operator. This is basically a language operator via which you can execute arbitrary commands in a command shell (some flavor of sh under UNIX-like operating systems or cmd.exe under Windows) by enclosing the command in backticks (`)—notice that they are different from regular single quotes ('). The key is typically located in the upper-left of English-language keyboards and can be quite challenging to find on other keyboard layouts.

Backticks return a string value with the text output of the program executed. The shell_exec function is identical to the backtick operator.

If we had a text file with a list of names and phone numbers in it, we might use the grep command to find a list of names that contain「Smith.」grep is a UNIX-like command that takes a string pattern to look for and list of files in which to find it. It returns specific lines in those files that match the pattern.

  grep [args] pattern files-to-search...

There are Windows versions of grep, and Windows does in fact ship with a program called findstr.exe, which can be used similarly. To find people named「Smith,」we could execute the following:

<?php  // -i means ignore case  $users = `grep –i smith /home/httpd/www/phonenums.txt`;

  // split the output lines into an array  // note that the \n should be \r\n on Windows!  $lines = split($users, "\n");

354

Chapter 15  Building a Secure Web Application

  foreach ($lines as $line)  {    // names and phone nums are separated by , char    $namenum = split($lines, ',');    echo "Name: {$namenum[0]}, Phone #: {$namenum[1]}<br/>\n";  }?>

If you ever allow user input to the command placed in backticks, you are opening yourselves to all sorts of security problems and will need to filter the input heavily to ensure the safety of your system. The escapeshellcmd() function can be used to escape the whole command, and escapeshellarg() can be used to escape a single argument. To be certain, however, you might want to restrict the possible input even more via whitelisting.

Even worse, given that we normally want to run our web server and PHP in a context with lower permissions (we will see more about this in following sections), we might find ourselves wanting to grant it more permissions to execute some of these commands, which could further compromise our security. Use of this operator in a production environment is something to be approached with a great amount of caution. In general, it is not recommended. You can disable use of shell_exec and backticks in your configuration file, or by running PHP in safe mode.

The exec and system functions are similar to the execution quotes operator, except that they execute the command directly instead of executing it within a shell environment and do not always return the full set of output that the execution quotes return. They do share many of the same security concerns, and thus also come with the same warnings. 

Securing Your Web Server and PHPIn addition to worrying about code security, the installation and configuration of our web server with PHP is a large security concern. Much software that we install on our computers and servers comes with configuration files and default feature sets designed to show off the power and usefulness of the software. It assumes that we will work on disabling those portions that are not needed and/or that are less secure than may be needed. Tragically, many people do not think to do this, or do not take the time to do it properly.

As part of our approach to dealing with security holistically, we want to be sure that our web servers and PHP are indeed properly configured. Although we cannot give a full presentation of how to secure every web server or extension in PHP you might use, we can at least provide some key points to investigate and point you in the correct direction for more advice and suggestions.

Keep Software Up-to-DateOne of the easiest ways to help the security of your system is to ensure that you are always running the latest and most secure version of the software you are using. For PHP, this means going to the website (http://www.php.net) and looking for security advisories and new releases, and browsing through the list of new features to see if any are indeed security-related bug fixes.

Securing Your Web Server and PHP

355

Setting Up the New VersionConfiguration and installation of some of these software programs can be time consuming and require a good number of steps. Especially on the UNIX distributions where you install from source, there can be a number of other pieces of software you have to install first, and then a good number of command-line switches required to get all the right modules and extensions enabled.

This is important: Make yourself an installation script you follow whenever you install a newer version of the software. That way you can be sure you do not forget something important, which will only cause troubles later on. Automation is your friend. 

Deploying the New VersionInstallations should never be done directly on the production server for the first time. You should always have a staging server to which you can install the software and your web application and make sure everything still works as expected. Especially for a language such as PHP, where some of the default settings change between versions, you will absolutely want to run through your test suite before you can be sure that the new version of the software does not adversely affect your application.

After you have verified that the new version of the software works well with your web application, you can deploy it to production servers. Here you should be absolutely sure that the process is automated so that you can follow an exact sequence of steps to replicate the correct server environment. Final testing should be done in the production environment to make sure that everything has gone as expected (see Figure 15.2). 

Figure 15.2  The process of upgrading server software

Browse the php.ini fileIf you have not yet spent much time browsing through php.ini, now is a good time to load it into a text editor and look through its contents. Most of the entries in the files have comments above them describing their use. They are also organized by feature area/extension name; all mbstring configuration options have names starting with mbstring, whereas those pertaining to sessions (Chapter 22,「Using Session Control in PHP」) have session prefixed.

There are a large number of configuration options for modules that you probably won’t ever use, and if those modules are disabled, we don’t have to worry about the options—they will be ignored. For those modules we do use, however, it is important to look through the  documentation in the PHP online manual (http://www.php.net/manual) to see what options that extension offers and what the possible values are.

356

Chapter 15  Building a Secure Web Application

It is highly recommended to keep the php.ini file in your version control or configuration management system—or at the very least manually track what changes we have made so that when we install new versions, we can be sure the correct settings are still there.

Web Server ConfigurationAfter we are comfortable with the way we have configured the PHP language engine, we look next at the web server. Each server tends to have its own security configuration process, and we list those for Apache HTTP Server, which is the most widely used HTTP server.

Apache HTTP ServerThe httpd server tends to come with a reasonably secure default installation, but there are a few things we will want to double-check before running it in a production environment. The configuration options all go in a file called httpd.conf, the location of which depends on your operating system. There is a good list of places to look at the following URL: http://wiki.apache.org/httpd/DistrosDefaultLayout.

You should definitely make sure that you have read the appropriate security sections in the online documentation for the server (http://httpd.apache.org/docs-project) and followed the advice there.

In general, you should also:

 ■ Make sure that httpd runs as a user without superuser privileges (such as nobody or 

httpd on UNIX). This is controlled by the User and Group settings in httpd.conf. On Linux, httpd will start as root and then change to the user specified in httpd.conf.

 ■ Make sure that the file permissions on the Apache installation directory are set correctly. 

On UNIX, this involves making sure that all the directories except for the document root (which defaults to using the htdocs/ subdirectory) are only writable by root. The document root should be readable by the Apache user, and readable and writable by developers or deployment scripts.

 ■ Hide files that you do not want seen by including appropriate directives in httpd.conf. 

For example, to exclude .inc files from being seen, you could add the following:

  <Files ~ "\.inc$">    Order allow, deny    Deny from all  </Files>

(Of course, as mentioned previously, you should move these files out of the document root for the specified website outright, but if there is some reason you can’t, this is a less-secure plan B.)

Shared Hosting of Web ApplicationsThere is one group of users for whom the problem of security on virtual servers is a bit more problematic—those users running their web applications on a shared PHP/MySQL hosting service. 

Database Server Security

357

On these servers, you likely will not have access to php.ini, and you will not be able to set all the options you would like. In extreme cases, some services will not even allow you to create directories outside of your document root directory, depriving us of a safe place to put our include files. Fortunately, most of these companies want to remain in business, and having an insecure design is not a good way to keep customers.

To be certain, you can and should do a number of things as you look into a service and deploy your web applications there:

 ■ Before you select a shared hosting service, look through their support listings. Better services will have complete online documentation that shows you exactly how your private space is configured. You can get a feel for what restrictions and support you will have by browsing through these.

 ■ Look for hosting services that give you entire directory trees, not just a document root. Although some will state that the root directory of your private space is the document root, others will give you a complete directory hierarchy, such as one in which public_html is where you place your content and executable PHP scripts. 

 ■ Try to find out what values they have used in php.ini. Although many will probably 

not print these on a web page or email you the file, you can ask their support personnel questions such as whether safe mode is turned on, and which functions and classes are disabled. You can also use the ini_get function to see setting values. Sites not using safe mode or without any functions at all disabled will worry us more than those with some reasonable sounding configuration. 

 ■ Look at what versions of the various pieces of software they are running. Are they the 

most recent ones?

 ■ Look for services that offer trial periods, money-back guarantees, or some other way of 

seeing firsthand how your web applications will run before committing to using them for a longer period of time. 

 ■ Although some developers still prefer a shared hosting environment because they don’t want to have to deal with system administration tasks, seriously consider using one of the many excellent cloud providers such as Amazon AWS, or platform as a service (PaaS) providers such as Heroku. Performing your own operations in such an environment is significantly simplified over having to manage actual machines, and there are many excellent tutorials available online. These services make keeping up with newer versions of software very simple.

Database Server SecurityIn addition to keeping all of our software up to date, we can do a few things to keep our databases more secure as well. Again, although a complete treatment of security would require a full book for each of the database servers against which we might write our web applications, we will give some general strategies here to which we should all pay attention.

358

Chapter 15  Building a Secure Web Application

Users and the Permissions SystemSpend the time to get to know the authentication and permissions system of the database server that you have chosen to use. A surprising number of database attacks succeed simply because people have not taken the time to make sure this system is secure.

Make sure that all accounts have passwords. One of the first things you do with any  database server is make sure that the database superuser (root) has a password. It’s better to avoid dictionary words in passwords. Even passwords such as 44horseA are much less secure than passwords like FI93!!xl2@. For those worried about the ease with which passwords can be memorized, consider using the first letter of all the words in a particular sentence, with some pattern of capitalization, such as IwTbOtIwTwOt, from「It was the best of times, it was the worst of times」(A Tale of Two Cities, by Charles Dickens). Alternatively, you can use a  passphrase, such as a sentence of reasonable length.

Many databases (including older versions of MySQL) will be installed with an anonymous user with more privileges than you would probably like. While investigating and becoming comfortable with the permissions system, make sure that any default accounts do exactly what you want them to do, and remove those that do not. 

Make sure that only the superuser account has access to the permissions tables and administra-tive databases. Other accounts should have only permissions to access or modify strictly those databases or tables they need.

To test it out, try the following, and verify that an error occurs:

 ■ Connect without specifying a username and password.

 ■ Connect as root without specifying a password.

 ■ Give an incorrect password for root.

 ■ Connect as a user and try to access a table for which the user should not have 

permission.

 ■ Connect as a user and try to access system databases or permissions tables.

Until you have tried each of these, you cannot be sure that your system’s authentication system is adequately protected. 

Sending Data to the ServerAs we have said repeatedly throughout this book (and will continue to do so), never send unfiltered data to the server. 

However, as we have seen elsewhere, we should do more than just rely on this for protection, and validate each field from an input form. If we have a username field, we probably want to be sure that it doesn’t contain kilobytes of data as well as characters we do not want to see in user names. By doing this validation in code, we can provide better error messages and can reduce some of the security risk to our databases. Similarly, for numeric and date/time data, we can verify the relative sanity of values before passing them to the server.

Database Server Security

359

We should always use prepared statements on those servers where available, which will do much of the escaping for us and make sure that everything is in quotes where necessary.

Again, there are tests we can do to make sure that our database is handling our data correctly:

 ■ Try entering values in forms such as '; DELETE FROM HarmlessTable', and so on.

 ■ For fields such as numbers or dates, try entering garbage values such as '55#$888ABC' 

and make sure that you get an error back.

 ■ Try to enter data that is beyond whatever size limits you have specified and verify that an 

error occurs.

Connecting to the ServerThere are a few ways we can keep our database servers secure by controlling connections to them. One of the easiest is to restrict from where people are allowed to connect. Many of the permissions systems used in the various database management systems allow you to specify not only a username and password for a user, but also from which machines they are allowed to connect. If the database server and web server/PHP engine are on the same machine, it most certainly makes sense to allow only connections from ‘localhost’, or the IP address used by that machine. If our web server is always on one computer, there is absolutely nothing wrong with allowing users to connect to the database only from that machine.

Databases support the capability to connect to them via encrypted connections (usually using a protocol known as Secure Sockets Layer, or SSL). If you ever have to connect with a database server over the open Internet, you absolutely want to use an encrypted connection if available. If not, consider using a product that does tunneling, in which a secure connection is made from one machine to another, and TCP/IP ports (such as port 80 for HTTP or 25 for SMTP) are routed over this secure connection to the other computer, which sees the traffic as local.

Running the ServerWhen running the database server, we can take a number of actions to help keep it safe. First and foremost, we should never run it as the superuser (root on UNIX, administrator on Windows). In fact, MySQL refuses to run as the superuser unless you force it to (which, again, is discouraged).

After you have set up your database software, most programs will then have you go and change the ownership and permissions on the database directories and files to keep them away from prying eyes. Make sure that this is done, and that the database files are not still owned by the superuser (in which case the nonsuperuser database server process might not even be able to write to its own database files).

Finally, when working with the permissions and authentication system, create users with the absolute minimum set of permissions. Remember the principle of least privilege. Instead of creating users with a broad set because「they might need it some day,」create them with the least number possible, and add permissions only when they are absolutely needed. 

360

Chapter 15  Building a Secure Web Application

Protecting the NetworkThere are a few ways in which we can protect the network in which our web application resides. Although the exact details of these are beyond the scope of this book, they are reasonably easy to learn about and will protect more than just your web applications.

FirewallsJust as we need to filter all the input that comes into our web application written in PHP, we also need to filter all the traffic that comes at our network, whether it be into our corporate offices or a data center in which we are hosting our servers and applications.

You do this via a firewall, which can be software running on a known operating system such as FreeBSD, Linux, or Microsoft Windows, or it can be a dedicated appliance you purchase from a networking equipment vendor. A firewall’s job is to filter out unwanted traffic and block access to those parts of our network that we want left alone.

The TCP/IP protocol, on which the Internet is based, operates on ports, with different ports being dedicated to different types of traffic (for example, HTTP is port 80). A large number of ports are used strictly for internal network traffic and have little use for interaction with the outside world. If we prohibit traffic from entering or leaving our network on these ports, we reduce the risk that our computers or servers (and therefore our web applications) will be compromised.

Use a DMZAs we mentioned earlier in this chapter, our servers and web applications are not only at risk of attack from external customers, but also from internal malicious users. Although these latter attackers will be fewer and farther between, they often have the potential to do more damage via having intimate knowledge of how the company works.

One of the ways to mitigate this risk is to implement what is known as a demilitarized zone, or DMZ. In this, we isolate the servers running our web applications (and other servers, such as corporate email servers) from both the external Internet and internal corporate networks, as shown in Figure 15.3.

Figure 15.3  Setting up a demilitarized zone (DMZ)

Computer and Operating System Security

361

DMZs have two major advantages:

 ■ They protect our servers and web applications from internal attacks as well as external 

attacks.

 ■ They protect our internal networks even further by putting more layers of firewalls and 

security between our corporate network and the Internet.

The design, installation, and maintenance of a DMZ are something that should be  coordinated with the network administrators for the location where you will be hosting your web application. 

Prepare for DoS and DDoS AttacksOne of the more frightening attacks seen today is the denial of service (DoS) attack, which we mentioned in Chapter 14, Web Application Security Risks. Network DOS attacks and the even more alarming distributed denial of service (DDoS) attacks use hijacked computers, worms, or other devices to exploit weaknesses in software installations, or even those inherent within the design of protocols such as TCP/IP themselves to swamp a computer and prevent it from replying to any connection requests from legitimate clients.

Unfortunately, this type of attack is very difficult to prevent and respond to. Some network appliance vendors sell equipment to help mitigate the risks and effects of DoS attacks, but there are no comprehensive solutions against them yet.

Your network administrator, at the very least, should do some research to understand the nature of the problem and the risks that your particular network and installations face. This, in combination with discussions with your hosting provider will help prepare you for the eventuality when such an attack does occur. Even if the attack is not directed specifically at your servers, they may end up being victims nonetheless. 

Computer and Operating System SecurityThe last thing we will worry about protecting is the server on which the web application runs. There are a few key ways in which you can and should do this.

Keep the Operating System Up to DateOne of the easier ways to keep your computer safe is to keep the operating system software up to date as much as possible. As soon as you choose a particular operating system for your production environment, you should set into motion a plan for performing upgrades and applying security patches to that operating system. You should also have somebody periodically go and check certain sources looking for new alerts, patches, or updates.

Where exactly you find out about vulnerabilities depends exactly on the operating system software you are using. This can be done from the vendor who supports the operating system, 

362

Chapter 15  Building a Secure Web Application

for example Red Hat or Canonical for Linux or Microsoft for Windows. For operating systems that are more community driven such as FreeBSD or Gentoo Linux, you typically go to the website representing their organized communities and see what latest security fixes they are recommending.

Like all software updates, you should have a staging environment in which you can test the application of these patches and verify their successful installation before performing the operation on any production servers. This lets you verify that nothing has broken in your web application before the problem gets to your live servers.

Being smart with the operating system and security fixes is definitely worth your while: If there is a security fix in the FireWire subsystem of a particular operating system, and your server has no FireWire hardware anywhere inside, it is probably a waste of time to go through the whole deployment process for that fix. 

Run Only What Is NecessaryOne of the problems many physical servers have is that they come with large amounts of software running, such as mail servers, FTP servers, the capability to work with Microsoft file system shares (via the SMB protocol), and others. To run our web applications, we need the web server software (such as Apache HTTP Server), PHP and any related libraries, the database server software, and often not much else.

If you are not using any of those other pieces of software, shut them off and disable them for good. That way, you do not have to worry about them being safe. If in doubt, do some research—it is highly likely that somebody on the Internet has already asked (and received an answer to) what a particular service does and whether it is necessary.

Physically Secure the ServerWe mentioned previously that one of our security threats is somebody coming into our building, unplugging the server computer, and simply walking off with it. This is, tragically, not a joke. With the average server not being a terribly cheap piece of hardware, the motivations for stealing server computers are not limited to corporate espionage and intellectual theft. Some people might just want to steal the computer for resale.

Thus, it is critical that servers used to run your web applications are kept in a secure environment, with only authorized people given access to it and specific processes in place for granting and revoking access to different people.

Disaster PlanningIf you ever want to see a truly blank look, ask your average IT manager what would happen to their servers, or indeed their entire data center, if the building in which it was hosted burned down or was instantly destroyed in a massive earthquake. An alarming percentage of them will have no answer at all. 

Disaster Planning

363

If a website or service is hosted in the cloud, this problem may present as having the application running entirely in a single region. On the database side, it often looks like a failure to run backups.

Disaster (recovery) planning is a critical and frequently overlooked part of running a service, whether it is a web application or anything else (including the day-to-day operations of your business). It is usually a collection of documents or procedures that have been rehearsed for dealing with the questions that arise when one of the following happens (among many):

 ■ Parts of or our entire data center is destroyed in some catastrophic event, such as an 

earthquake.

 ■ Our development team goes out for lunch and all are hit by a bus and seriously injured 

(or killed). 

 ■ Our corporate headquarters burns down.

 ■ A network attacker or disgruntled (or merely incompetent) employee manages to destroy 

all the data on the servers for our web applications.

Although many people do not like to even talk about disasters and attacks for various reasons, the hard reality is that such things actually do occur—fortunately, only rarely. Businesses, however, usually cannot afford the downtime that an event of such magnitude would cause if they were completely unprepared. A business that does millions of dollars a day in business would be devastated if its web applications were shut down for over a week while people not 100% familiar with the setup worked to get the systems up and running again.

By preparing for these events, anticipating them with clear plans of action, and by rehearsing some of the more critical portions of these, a little financial investment up front can save the business from potentially disastrous losses later on when a real problem does strike.

Some of the things we might do to help with disaster planning and recovery include the following:

 ■ Make sure that all data is backed up daily and stored off-site or in another region, so that 

even if our data center is destroyed, we still have the data elsewhere.

 ■ Have documentation, also off-site, on how to re-create the server environments and set 

up the web application. Rehearse this re-creation at least once.

 ■ Have a full copy of all source code necessary for our web application, also in multiple 

locations. This might be an external source code repository stored on GitHub or similar, as well as in the production environment.

 ■ For larger teams, prohibit all members of the team from traveling in one vehicle, such as 

a car or airplane, so that if there is an accident, we will be affected less. This is actually required by some business insurance policies.

364

Chapter 15  Building a Secure Web Application

 ■ Have automated tools running to make sure that server operation is normal, and have an on-call roster so you know who will be responsible for solving problems outside business hours.

 ■ Make arrangements with a hardware provider to have new hardware immediately 

available in the case that your data center is destroyed, or keep spares on hand. It would be most frustrating to have to wait 4 to 6 weeks for new servers. 

NextIn Chapter 16,「Implementing Authentication Methods with PHP,」we move beyond security to take a closer look at authentication—allowing users to prove their identity. We look at a few different methods, including using PHP and MySQL to authenticate site visitors.

