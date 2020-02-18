26Debugging and Logging

This chapter deals with debugging PHP scripts. If you have worked through some of the examples in the book or used PHP before, you will probably already have developed some debugging skills and techniques of your own. As your projects get more complex, debugging can become more difficult. Although your skills improve, the errors are more likely to involve multiple files or interactions between code written by multiple people.

Key topics covered in this chapter include

 ■ Programming syntax, runtime, and logic errors

 ■ Error messages

 ■ Error levels

 ■ Triggering your own errors

 ■ Handling errors gracefully

Programming ErrorsRegardless of which language you are using, there are three general types of program errors:

 ■ Syntax errors

 ■ Runtime errors

 ■ Logic errors

We look briefly at each before discussing some tactics for detecting, handling, avoiding, and solving errors.

Syntax ErrorsLanguages have a set of rules called the syntax, which statements must follow to be valid. This applies to both natural languages, such as English, and programming languages, such as PHP. If a statement does not follow the rules of a language, it is said to have a syntax error. Syntax 

544

Chapter 26  Debugging and Logging

errors also are often called parser errors when discussing interpreted languages, such as PHP, or compiler errors when discussing compiled languages, such as C or Java.

If you break the English language’s syntax rules, there is a pretty good chance that people will still know what you intended to say. This often is not the case with programming languages. If a script does not follow the rules of PHP’s syntax—if it contains syntax errors—the PHP parser will not be able to process some or all of it. People are good at inferring information from partial or conflicting data. Computers are not.

Among many other rules, the syntax of PHP requires that statements end with semicolons, that strings are enclosed in straight quotation marks, and that parameters passed to functions be separated with commas and enclosed in parentheses. If you break these rules, your PHP script is unlikely to work and likely to generate an error message the first time you try to execute it.

One of PHP’s great strengths is the useful error messages that it provides when things go wrong. A PHP error message usually tells you what went wrong, which file the error occurred in, and which line the error was found at.

An error message resembles the following:

Parse error: syntax error, unexpected '');' (T_ENCAPSED_AND_WHITESPACE), expecting ',' or ')' in /var/www/pmwd5e/chapter26/error.php on line 2

This error was produced by the following script:

<?php   $date = date(m.d.y');?>

You can see that we attempted to pass a string to the date() function but accidentally missed the opening quotation mark that would mark the beginning of the string.

Simple syntax errors such as this one are usually the easiest to find. Additionally, errors can be hard to find if they result from a combination of multiple files. They can also be difficult to find if they occur in a large file. Seeing parse error on line 1001 of a 1000-line file can be enough to spoil your day, but it should provide a subtle hint that you should try to write more modular code.

In general, though, syntax errors are the easiest type of error to find. If you make a syntax error and try to execute that block of code, PHP will give you a message telling you where to find your mistake.

Runtime ErrorsRuntime errors can be harder to detect and fix. A script either contains a syntax error or it does not. If the script contains a syntax error, the parser will detect it when that code is executed. Runtime errors are not caused solely by the contents of your script. They can rely on interactions between your scripts and other events or conditions.

The statement

require ('filename.php');

Programming Errors

545

is a perfectly valid PHP statement. It contains no syntax errors.

However, this statement might generate a runtime error. If you execute this statement and filename.php does not exist, or the user whom the script runs as is denied read permission, you will get an error resembling this one:

Fatal error: require(): Failed opening required 'filename.php' (include_path='.:/usr/local/php/lib/php') in /var/www/pmwd5e/chapter26/error.php on line 2

Although nothing is wrong with the code here, because it relies on a file that might or might not exist at different times when the code is run, it can generate a runtime error.

The following three statements are all valid PHP. Unfortunately, in combination, they attempt to do the impossible—divide by zero:

$i = 10;$j = 0;$k = $i/$j;

This code snippet generates the following warning:

Warning: Division by zero in /var/www/pmwd5e/chapter26/error.php on line 4

This warning makes it very easy to correct. Few people would try to write code that attempted to divide by zero on purpose, but neglecting to check user input often results in this type of error.

The following code sometimes generates the same error but might be much harder to isolate and correct because it happens only some of the time:

$i = 10;$k = $i/$_REQUEST['input'];

This is one of many different runtime errors that you might see while testing your code.

Common causes of runtime errors include the following:

 ■ Calls to functions that do not exist

 ■ Reading or writing files

 ■ Interaction with MySQL or other databases

 ■ Connections to network services

 ■ Failure to check input data

We briefly discuss each of these causes in the following sections.

Calls to Functions That Do Not ExistAccidentally calling functions that do not exist is easy. The built-in functions are often  inconsistently named. For example, strip_tags() has an underscore, whereas  stripslashes() does not. This sort of mixup is very easy to make.

546

Chapter 26  Debugging and Logging

It is also easy to call one of your own functions that does not exist in the current script but might exist elsewhere. If your code contains a call to a nonexistent function, such as

nonexistent_function();

or

mispeled_function();

you will see an error message similar to this:

Fatal error: Uncaught Error: Call to undefined function nonexistent_function() in /var/www/pmwd5e/chapter26/error.php:2 Stack trace: #0 {main} thrown in /var/www/pmwd5e/chapter26/error.php on line 2

Similarly, if you call a function that exists but call it with an incorrect number of parameters, you will receive a warning.

The function strstr() requires two strings: a haystack to search and a needle to find. If instead you call it using

strstr();

you will get the following warning:

Warning: strstr() expects at least 2 parameters, 0 given in /var/www/pmwd5e/chapter26/error.php on line 2

That same statement within the following script is equally wrong:

<?php  if($var == 4) {    strstr();  }?>

Except in the possibly rare case in which the variable $var has the value 4, the call to strstr() will not occur, and no warning will be issued. The PHP interpreter does not waste time parsing sections of your code that are not needed for the current execution of the script. You need to be sure that you test carefully!

Calling functions incorrectly is easy to do, but because the resulting error messages identify the exact line and function call that are causing the problem, they are equally easy to fix. They are difficult to find only if your testing process is poor and does not test all conditionally executed code. When you test, one of the goals is to execute every line of code at least once. Another goal is to test all the boundary conditions and classes of input.

Reading or Writing FilesAlthough anything can go wrong at some point during your program’s useful life, some problems are more likely than others. Because errors accessing files are likely enough to occur, you need to handle them gracefully. Hard drives fail or fill up, and human error results in directory permissions changing.

Programming Errors

547

Functions such as fopen() that are likely to fail occasionally generally have a return value to signal that an error occurred. For fopen(), a return value of false indicates failure.

For functions that provide failure notification, you need to carefully check the return value of every call and act on failures.

Interaction with MySQL or Other DatabasesConnecting to and using MySQL can generate many errors. The function mysqli_connect() alone can generate at least the following errors:

 ■ Warning: mysqli_connect() [function.mysqli-connect]: Can't connect to 

MySQL server on 'localhost' (10061)

 ■ Warning: mysqli_connect() [function.mysqli-connect]: Unknown MySQL 

Server Host 'hostname' (11001)

 ■ Warning: mysqli_connect() [function.mysqli-connect]: Access denied for 

user: 'username'@'localhost' (Using password: YES)

As you would probably expect, mysqli_connect() provides a return value of false when an error occurs. This means that you can easily trap and handle these types of common errors.

If you do not stop the regular execution of your script and handle these errors, your script will attempt to continue interacting with the database. Trying to run queries and get results without a valid MySQL connection results in your visitors seeing an unprofessional-looking screen full of error messages.

Many other commonly used MySQL-related PHP functions such as mysqli_query() also return false to indicate that an error occurred.

If an error occurs, you can access the text of the error message using the function mysqli_error(), or an error code using the function mysqli_errno(). If the last MySQL function did not generate an error, mysqli_error() returns an empty string and mysqli_errno() returns 0.

For example, assuming that you have connected to the server and selected a database for use, the code snippet

$result = mysqli_query($db, 'select * from does_not_exist');echo mysqli_errno($db);echo '<br />';echo mysqli_error($db);

might output

1146Table 'dbname.does_not_exist' doesn't exist

Note that the output of these functions refers to the last MySQL function executed (other than mysqli_error() or mysqli_errno()). If you want to know the result of a command, make sure to check it before running others.

548

Chapter 26  Debugging and Logging

Like file interaction failures, database interaction failures will occur. Even after completing development and testing of a service, you will occasionally find that the MySQL daemon (mysqld) has crashed or run out of available connections. If your database runs on another physical machine, you are relying on another set of hardware and software components that could fail—another network connection, network card, routers, and so on between your Web server and the database machine.

You need to remember to check whether your database requests succeed before attempting to use the result. There is no point in attempting to run a query after failing to connect to the database and no point in trying to extract and process the results after running a query that failed.

It is important to note at this point that there is a difference between a query failing and a query that merely fails to return any data or affect any rows.

A SQL query that contains SQL syntax errors or refers to databases, tables, or columns that do not exist will fail. The query

select * from does_not_exist;

will fail because the table name does not exist, and it will generate an error number and message retrievable with mysqli_errno() and mysqli_error().

A SQL query that is syntactically valid and refers only to databases, tables, and columns that exist generally does not fail. The query might, however, return no results if it is querying an empty table or searching for data that does not exist. Assuming that you have connected to a database successfully and have a table called t1 and a column called c1, the query

select * from t1 where c1 = 'not in database';

will succeed but not return any results.

Before you use the result of the query, you need to check for both failure and no results.

Connections to Network ServicesAlthough devices and other programs on your system will occasionally fail, they should fail rarely unless they are of poor quality. When using a network to connect to other machines and the software on those machines, you need to accept that some part of the system will fail often. To connect from one machine to another, you rely on numerous devices and services that are not under your control.

At the risk of our being repetitive, be sure you carefully check the return value of functions that attempt to interact with a network service.

A function call such as

$sp = fsockopen('localhost', 5000 );

will provide a warning if it fails in its attempt to connect to port 5000 on the machine localhost, but it will display the warning in the default format and not give your script the option to handle it gracefully.

Programming Errors

549

Rewriting the call as

$sp = @fsockopen ('localhost', 5000, &$errorno, &$errorstr );if(!$sp) {  echo "ERROR: ".$errorno.": ".$errorstr;}

suppresses the built-in error message, checks the return value to see whether an error occurred, and uses your own code to handle the error message. The code will display an error message that might help you solve the problem, as opposed to the previous example that would most certainly not. In this case, the code would produce the following output:

ERROR: 10035: A non-blocking socket operation could not be completed immediately.

Runtime errors are harder to eliminate than syntax errors because the parser cannot signal the error the first time the code is executed. Because runtime errors occur in response to a combination of events, they can be hard to detect and solve. The parser cannot automatically tell you that a particular line will generate an error. Your testing needs to provide one of the situations that create the error.

Handling runtime errors requires a certain amount of forethought—to check for different types of failure that might occur and then take appropriate action. Simulating each class of runtime error that might occur also takes careful testing.

We do not mean that you need to attempt to simulate every different error that might occur. MySQL, for example, can provide hundreds of different error numbers and messages. Instead, you should simulate an error in each function call that is likely to result in an error and an error of each type that is handled by a different block of code.

Failure to Check Input DataOften you make assumptions about the input data that will be entered by users. If this data does not fit your expectations, it might cause an error, either a runtime error or a logic error (detailed in the following section).

A classic example of a runtime error occurs when you are dealing with user input data and you forget to apply addslashes() to it. This means if you have a user with a name such as O’Grady (one that contains an apostrophe), you will get an error from the database function if you use the input in an INSERT statement inside single quotation marks.

We discuss errors because of assumptions about input data in more detail in the next section.

Logic ErrorsLogic errors can be the hardest type of error to find and eliminate. This type of error occurs when perfectly valid code does exactly what it is instructed to do, but that was not what the writer intended.

550

Chapter 26  Debugging and Logging

Logic errors can be caused by a simple typing error, such as

for ( $i = 0; $i < 10; $i++ );{  echo 'doing something<br />';}

This snippet of code is perfectly valid. It follows valid PHP syntax. It does not rely on any external services, so it is unlikely to fail at runtime. Unless you looked at it very carefully, it probably will not do what you think it will, or what the programmer intended it to do.

At a glance, it looks as if it will iterate through the for loop 10 times, echoing "doing  something" each time. The addition of an extraneous semicolon at the end of the first line means that the loop has no effect on the following lines. The for loop will iterate 10 times with no result, and then the echo statement will be executed once.

Because this snippet is a perfectly valid, but inefficient, way to write code to achieve this result, the parser will not complain. Computers are very good at some things, but they do not have any common sense or intelligence. A computer will do exactly as it is told. You need to make sure that what you tell it is exactly what you want.

Logic errors are not caused by any sort of failure of the code, but merely a failure of the programmer to write code that instructs the computer to do exactly what he or she wanted. As a result, errors cannot be detected automatically. You are not told that an error has occurred, and you are not given a line number where you can look for the problem. Logic errors are detected only by proper testing.

A logic error such as the previous trivial example is fairly easy to make, but also easy to correct because the first time your code runs, you will see output other than what you expected. Most logic errors are more insidious.

Troublesome logic errors usually result from developers’ assumptions being wrong. Chapter 25,「Using PHP and MySQL for Large Projects,」recommended using other developers to review code to suggest additional test cases and using people from the target audience rather than developers for testing. Assuming that people will enter only certain types of data is very easy to do and an error that is very easy to leave undetected if you do your own testing.

Let’s say that you have an Order Quantity text box on a commerce site. Have you assumed that people will enter only positive numbers? If a visitor enters –10, will your software refund his credit card with 10 times the price of the item?

Suppose that you have a box to enter a dollar amount. Do you allow people to enter the amount with or without a dollar sign? Do you allow people to enter numbers with thousands separated by commas? Some of these things can be checked at the client side (using, for example, JavaScript) to take a little load off your server.

If you are passing information to another page, has it occurred to you that some characters might have special significance in a URL, such as spaces in the string you are passing?

Variable Debugging Aid

551

An infinite number of logic errors are possible. There is no automated way to check for these errors. The only solution is, first, to try to eliminate assumptions that you have implicitly coded into the script and, second, test thoroughly with every type of valid and invalid input possible, ensuring that you get the anticipated result for all.

Variable Debugging AidAs projects become more complex, having some utility code to help you identify the cause of errors can be useful. A piece of code that you might find useful is contained in Listing 26.1. This code echoes the contents of variables passed to your page.

Listing 26.1 

 dump_variables.php—This Code Can Be Included in Pages to Dump the Contents of Variables for Debugging

<?phpsession_start();

  // these lines format the output as HTML comments  // and call dump_array repeatedly

  echo "\n<!-- BEGIN VARIABLE DUMP -->\n\n";

  echo "<!-- BEGIN GET VARS -->\n";  echo "<!-- ".dump_array($_GET)." -->\n";

  echo "<!-- BEGIN POST VARS -->\n";  echo "<!-- ".dump_array($_POST)." -->\n";

  echo "<!-- BEGIN SESSION VARS -->\n";  echo "<!-- ".dump_array($_SESSION)." -->\n";

  echo "<!-- BEGIN COOKIE VARS -->\n";  echo "<!-- ".dump_array($_COOKIE)." -->\n";

  echo "\n<!-- END VARIABLE DUMP -->\n";

// dump_array() takes one array as a parameter// It iterates through that array, creating a single// line string to represent the array as a set

function dump_array($array) {

  if(is_array($array)) {

552

Chapter 26  Debugging and Logging

    $size = count($array);    $string = "";    if($size) {

      $count = 0;      $string .= "{ ";      // add each element's key and value to the string      foreach($array as $var => $value) {

        $string .= $var." = ".$value;        if($count++ < ($size-1)) {          $string .= ", ";        }      }      $string .= " }";    }    return $string;  } else {    // if it is not an array, just return it    return $array;  }}?>

This code outputs four arrays of variables that a page receives. If a page was called with GET variables, POST variables, loads cookies, or has session variables, they will be output.

Here, we put the output within an HTML comment so that it is viewable but does not interfere with the way the browser renders visible page elements. This is a good way to generate  debugging information. Hiding the debug information in comments, as in Listing 26.1, allows you to leave in your debug code until the last minute. We used the dump_array() function as a wrapper to print_r(). The dump_array() function just escapes out any HTML end comment characters.

The exact output depends on the variables passed to the page, but when added to Listing 22.4, one of the authentication examples from Chapter 22,「Using Session Control in PHP,」it adds the following lines to the HTML generated by the script:

<!-- BEGIN VARIABLE DUMP -->

<!-- BEGIN GET VARS --><!-- Array() --><!-- BEGIN POST VARS --><!-- Array

Error Reporting Levels

553

(    [userid] => testuser    [password] => password) --><!-- BEGIN SESSION VARS --><!-- Array() --><!-- BEGIN COOKIE VARS --><!-- Array(    [PHPSESSID] => b2b5f56fad986dd73af33f470f3c1865) -->

<!-- END VARIABLE DUMP -->

You can see that it displays the POST variables sent from the login form on the previous page: userid and password. It also shows the session variable used to keep the user’s name in: valid_user. As discussed in Chapter 22, PHP uses a cookie to link session variables to  particular users. The script echoes the pseudo-random number, PHPSESSID, which is stored in that cookie to identify a particular user.

Error Reporting LevelsPHP allows you to set how fussy it should be with errors. You can modify what types of events generate messages. By default, PHP reports all errors other than notices.

The error reporting level is assigned using a set of predefined constants, shown in Table 26.1.

Table 26.1  Error Reporting Constants

Value

Name

Meaning

1

2

4

8

16

32

64

E_ERROR

E_WARNING

E_PARSE

E_NOTICE

E_CORE_ERROR

E_CORE_WARNING

Report fatal errors at runtime

Report nonfatal errors at runtime

Report parse errors

Report notices, notifications that something you have done might be an error

Report failures in the startup of the PHP engine

Report nonfatal failures during the startup of the PHP engine

E_COMPILE_ERROR

Report errors in compilation

554

Chapter 26  Debugging and Logging

Value

Name

Meaning

128

256

512

1024

2048

4096

8192

E_COMPILE_WARNING

Report nonfatal errors in compilation

E_USER_ERROR

E_USER_WARNING

E_USER_NOTICE

E_STRICT

Report user-triggered errors

Report user-triggered warnings

Report user-triggered notices

Reports use of deprecated and unrecommended  behavior; not included in E_ALL but very useful for code refactoring. Suggests changes for interoperability.

E_RECOVERABLE_ERROR

Reports catchable fatal errors.

E_DEPRECATED

16384

E_USER_DEPRECATED

32767

E_ALL

Reports warnings about code that will not work in future PHP releases.

Reports warnings generated by the PHP function  trigger_error().

Report all errors and warnings except those reported in E_Strict

Each constant represents a type of error that can be reported or ignored. If, for instance, you specify the error level as E_ERROR, only fatal errors will be reported. These constants can be combined using binary arithmetic, to produce different error levels.

The default error level—report all errors other than notices—is specified as follows:

E_ALL & ~E_NOTICE

This expression consists of two of the predefined constants combined using bitwise arithmetic operators. The ampersand (&) is the bitwise AND operator and the tilde (~) is the bitwise NOT operator. This expression can be read as E_ALL AND NOT E_NOTICE.

E_ALL itself is effectively a combination of all the other error types except for E_STRICT. It could be replaced by the other levels combined together using the bitwise OR operator (|):

E_ERROR | E_WARNING | E_PARSE | E_NOTICE | E_CORE_ERROR | E_CORE_WARNING |E_COMPILE_ERROR |E_COMPILE_WARNING | E_USER_ERROR | E_USER_WARNING |E_USER_NOTICE

Similarly, the default error reporting level could be specified by all error levels except E_NOTICE combined with OR:

E_ERROR | E_WARNING | E_PARSE | E_CORE_ERROR | E_CORE_WARNING | E_COMPILE_ERROR |E_COMPILE_WARNING | E_USER_ERROR | E_USER_WARNING | E_USER_NOTICE

Altering the Error Reporting SettingsYou can set the error reporting settings globally, in your php.ini file or on a per-script basis.

To alter the error reporting for all scripts, you can modify these lines in the default php.ini file:

Altering the Error Reporting Settings

555

error_reporting        = E_ALL & ~E_NOTICE & ~E_STRICT & ~E_DEPRECATEDdisplay_errors         = Ondisplay_startup_errors = Offlog_errors             = Offlog_errors_max_len     = 1024ignore_repeated_errors = Offignore_repeated_source = Offreport_memleaks        = Ontrack_errors           = Offhtml_errors            = Onerror_log              =

The default global settings are to

 ■ Report all errors except notices, strict compatibility, and deprecated notices.

 ■ Not display errors during startup sequence.

 ■ Not log error messages to disk, but if you do the maximum length would be 1024 bytes.

 ■ Not log repeated errors or source lines.

 ■ Report memory leaks.

 ■ Not track errors, storing the error in the variable $php_errormsg.

 ■ Output error messages as HTML to standard output.

 ■ Send all errors to stderr.

The most likely change you will make is to turn the error reporting level up to E_ALL | E_STRICT. This change results in many notices being reported, for incidents that might indicate an error, or might just result from the programmer taking advantage of PHP’s weakly typed nature and the fact that it automatically initializes variables to 0.

While debugging, you might find it useful to set the error_reporting level higher. If you are providing useful error messages of your own, the production code would be more  professional looking if you turn display_errors off and turn log_errors on, while leaving the error_reporting level high. You then can refer to detailed errors in the logs if problems are reported.

Turning track_errors on might help you to deal with errors in your own code, rather than letting PHP provide its default functionality. Although PHP provides useful error messages, its default behavior looks ugly when things go wrong.

By default, when a fatal error occurs, PHP outputs

<br><b>Error Type</b>: error message in <b>path/file.php</b>on line <b>lineNumber</b><br>

556

Chapter 26  Debugging and Logging

and stops executing the script. For nonfatal errors, the same text is output, but execution continues.

This HTML output makes the error stand out but looks poor. The style of the error message is unlikely to fit the rest of the site’s look. It might also result in some users seeing no output at all if the page’s content is displayed within a table and their browser is fussy about valid HTML. HTML that opens but does not close table elements, such as

<table><tr><td><br><b>Error Type</b>:  error message in <b>path/file.php</b>on line <b>lineNumber</b><br>

can be rendered as a blank screen by some browsers.

You do not have to keep PHP’s default error handling behavior or even use the same settings for all files. To change the error reporting level for the current script, you can call the function error_reporting().

Passing an error report constant, or a combination of them, sets the level in the same way that the similar directive in php.ini does. The function returns the previous error reporting level. A common way to use the function is like this:

// turn off error reporting$old_level = error_reporting(0);

// here, put code that will generate warnings

// turn error reporting back onerror_reporting($old_level);

This code snippet turns off error reporting, allowing you to execute some code that is likely to generate warnings that you do not want to see.

Turning off error reporting permanently is a bad idea because it makes finding your coding errors and fixing them more difficult.

Triggering Your Own ErrorsThe function trigger_error() can be used to trigger your own errors. Errors created in this way are handled in the same way as regular PHP errors.

The function requires an error message and can optionally be given an error type. The error type needs to be one of E_USER_ERROR, E_USER_WARNING, or E_USER_NOTICE. If you do not specify a type, the default is E_USER_NOTICE.

You use trigger_error() as follows:

trigger_error('This computer will self destruct in 15 seconds', E_USER_WARNING); 

Logging Errors Gracefully

557

Logging Errors GracefullyIf you come from a C++ or Java background, you are probably comfortable using exceptions. Exceptions allow functions to signal that an error has occurred and leave dealing with the error to an exception handler. Exceptions are an excellent way to handle errors in large projects. They were adequately covered in Chapter 7,「Error and Exception Handling,」so they will not be revisited here.

You have already seen how you can trigger your own errors. You can also provide your own error handlers to catch errors.

The function set_error_handler() lets you provide a function to be called when user-level errors, warnings, and notices occur. You call set_error_handler() with the name of the  function you want to use as your error handler.

Your error handling function must take two parameters: an error type and an error message. Based on these two variables, your function can decide how to handle the error. The error type must be one of the defined error-type constants. The error message is a descriptive string.

A call to set_error_handler() looks like this:

set_error_handler('my_error_handler');

Having told PHP to use a function called my_error_handler(), you must then provide a function with that name. This function must have the following prototype:

my_error_handler(int error_type, string error_msg                  [, string errfile [, int errline [, array errcontext]]]))

What it actually does, however, is up to you.

The parameters passed to your handler function are

 ■ The error type

 ■ The error message

 ■ The file the error occurred in

 ■ The line the error occurred on

 ■ The symbol table—that is, a set of all the variables and their values at the time the error 

occurred

Logical actions might include

 ■ Displaying the error message provided

 ■ Logging the information in a log file

 ■ Emailing the error to an address

 ■ Terminating the script with a call to exit

558

Chapter 26  Debugging and Logging

Listing 26.2 contains a script that declares an error handler, sets the error handler using set_error_handler(), and then generates some errors.

Listing 26.2 

 handle.php—This Script Declares a Custom Error Handler and Generates Different Errors

<?php// The error handler functionfunction myErrorHandler ($errno, $errstr, $errfile, $errline) {  echo "<p><strong>ERROR:</strong> ".$errstr."<br/>        Please try again, or contact us and tell us that the         error occurred in line ".$errline." of file ".$errfile."         so that we can investigate further.</p>";

  if (($errno == E_USER_ERROR) || ($errno == E_ERROR)) {    echo "<p>Fatal error. Program ending.</p>";    exit;  }

  echo "<hr/>";}

// Set the error handlerset_error_handler('myErrorHandler');

//trigger different levels of errortrigger_error('Trigger function called.', E_USER_NOTICE);fopen('nofile', 'r');trigger_error('This computer is beige.', E_USER_WARNING);include ('nofile');trigger_error('This computer will self destruct in 15 seconds.', E_USER_ERROR);?>

The output from this script is shown in Figure 26.1.

This custom error handler does not do any more than the default behavior. Because you write this code, you can make it do anything. You have a choice about what to tell your  visitors when something goes wrong and how to present that information so that it fits the rest of the site. More importantly, you have the flexibility to decide what happens. Should the script continue? Should a message be logged or displayed? Should tech support be alerted automatically?

Logging Errors Gracefully

559

Figure 26.1  You can give friendlier error messages than PHP if you use your own error handler

It is important to note that your error handler will not have the responsibility for dealing with all error types. Some errors, such as parse errors and fatal runtime errors, still trigger the default behavior. If this behavior concerns you, make sure that you check parameters carefully before passing them to a function that can generate fatal errors and trigger your own E_USER_ERROR level error if your parameters are going to cause failure.

Here’s a useful feature: If your error handler returns an explicit false value, PHP’s built-in error handler will be invoked. This way, you can handle the E_USER_* errors yourself and let the built-in handler deal with the regular errors.

560

Chapter 26  Debugging and Logging

Logging Errors to a Log FilePHP allows you to log your errors to a log file rather than relying on stderr and displaying errors on the web page itself. This has the benefit of making your web applications look cleaner and also more secure. PHP errors can provide information about the path, database schema, and other sensitive information. By logging errors to a file, you ensure that information remains secure. 

To enable logging, you need to change the php.ini file to modify the error log directive. For example, to send all your errors to /var/log/php-errors.log, write:

error_log = /var/log/php-errors.log

Then make sure that the display_errors directive is turned off so that no errors are sent to end users. 

display_errors = Off

Then restart your web server so that your changes take effect; once complete, you can view the log file at your convenience (hopefully without too many errors logged). 

NextIn Chapter 27,「Building User Authentication and Personalization,」you will learn how to get users to register at your website, and then, you can track what they’re interested in and show them appropriate content.

27Building User Authentication and Personalization

