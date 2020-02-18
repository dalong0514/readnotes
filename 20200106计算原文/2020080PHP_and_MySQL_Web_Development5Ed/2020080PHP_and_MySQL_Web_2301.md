24Other Useful Features

Some useful PHP functions and features do not fit into any particular category. This chapter explains these features.

Key topics covered in this chapter include

 ■ Evaluating strings with eval()

 ■ Terminating execution with die and exit

 ■ Serializing variables and objects

 ■ Getting information about the PHP environment

 ■ Temporarily altering the runtime environment

 ■ Highlighting source code

 ■ Using PHP on the command line

Many of the examples you’ll see in this chapter are brief code snippets that you can use as the basis of larger code elements in your applications.

Evaluating Strings: eval()The function eval() evaluates a string as PHP code. For example,

eval("echo 'Hello World';");

takes the contents of the string and executes it. This line produces the same output as

echo 'Hello World';

At first glance, this function may not seem all that useful, but in fact  eval() can be useful in a variety of cases. For example, you might want to store blocks of code in a database, retrieve them, and then evaluate them at a later point. You also might want to generate code in a loop and then use eval() to execute it.

520

Chapter 24  Other Useful Features

But the most common use for eval() is as part of a templating system, which you’ll read a bit more about in Chapter 25,「Using PHP and MySQL for Large Projects.」With a templating system, you can load a mixture of HTML, PHP, and plain text from a database, then the templating system can apply formatting to this content and run it through eval() to execute any PHP code.

You can also use eval() to update or correct existing code. If you had a large collection of scripts that needed a predictable change, it would be possible (but inefficient) to write a script that loads an old script into a string, runs regexp to make changes, and then uses eval() to execute the modified script.

It is even conceivable that a very trusting person somewhere might want to allow PHP code to be entered in a browser and executed on his or her server, but we do not recommend this  practice for general use.

Terminating Execution: die() and exit()So far in this book, we have used the language construct exit to stop execution of a script at a certain point. As you probably recall, it appears on a line by itself, like this:

exit;

It does not return anything. You can alternatively use its alias, die().

For a slightly more useful termination to your script, you can pass a parameter to exit(). You can use this approach to output an error message or execute a function before terminating a script. This will be familiar to Perl programmers. For example,

exit('Script ending now...');

More commonly, exit() or die() is combined using or with a statement that might fail, such as opening a file or connecting to a database:

mysql_query($query) or die('Could not execute query.');

In the example above, the string「Could not execute query.」will be printed to the screen if the return value of the mysql_query($query) function is false. Additionally, instead of just printing an error message, you can run one last function before the script terminates:

function err_msg(){    return 'MySQL error was: '.mysql_error();}

mysql_query($query) or die(err_msg());

This approach can be useful as a way of giving the user a more specific reason why the script failed, or as a way of closing HTML elements or clearing a half-completed page from the output buffer.

Alternatively, you could create a function that emails yourself upon failure, so that you know whether a major error has occurred, or you could add errors to a log file or throw an exception.

Serializing Variables and Objects

521

Serializing Variables and ObjectsSerialization is the process of turning anything you can store in a PHP variable or object into a bytestream that can be stored in a database or passed along via a URL from page to page. Without this process, it is difficult to store or pass the entire contents of an array or object.

Serialization has decreased in usefulness since the introduction of session control. Serializing data is principally used for the types of things you would now use session control for. In fact, the session control functions serialize session variables to store them between HTTP requests.

However, you might still want to store a PHP array or object in a file or database. If you do, you need to know how to use these two functions: serialize() and unserialize().

You can call the serialize() function as follows:

$serial_object = serialize($my_object);

If you want to know what the serialization actually does, look at what is returned from serialize(). This line turns the contents of an object or array into a string.

For example, you can look at the output of running serialize() on a simple employee object, defined and instantiated thus:

class employee{  var $name;  var $employee_id;}

$this_emp = new employee;$this_emp->name = 'Fred';$this_emp->employee_id = 5324;

If you serialize this and echo it to the browser, the output is

O:8:"employee":2:{s:4:"name";s:4:"Fred";s:11:"employee_id";i:5324;}

You can easily see the relationship between the original object data here and the serialized data.

Because the serialized data is just text, you can write it to a database or whatever you like. Please use mysqli_real_escape_string() on any text data before writing it to a database to escape any special characters. You can see the need for this by noting the quotation marks in the previous serialized string.

To get the object back, call unserialize():

$new_object = unserialize($serial_object);

Another point to note when serializing classes or using them as session variables: PHP needs to know the structure of a class before it can reinstantiate the class. Therefore, you need to include the class definition file before calling session_start() or unserialize().

522

Chapter 24  Other Useful Features

Getting Information About the PHP EnvironmentA number of functions can be used to find out information about how PHP is configured, which can be very useful when trying to track down configuration issues or just to verify that a required configuration or extension is included in your PHP installation.

Finding Out What Extensions Are LoadedYou can easily see what function sets are available and what functions are available in each of those sets by using the get_loaded_extensions() and get_extension_funcs() functions.

The get_loaded_extensions() function returns an array of all the function sets currently available to PHP. Given the name of a particular function set or extension, get_extension_funcs() returns an array of the functions in that set.

The script in Listing 24.1 lists all the extension functions available to your PHP installation by using these two functions (also refer Figure 24.1).

Listing 24.1 

 list_functions.php—Lists the Extensions Available to PHP and the Functions for Each Extension

<?phpecho 'Function sets supported in this install are: <br />';$extensions = get_loaded_extensions();foreach ($extensions as $each_ext){  echo $each_ext.'<br />';  echo '<ul>';  $ext_funcs = get_extension_funcs($each_ext);  foreach($ext_funcs as $func)  {    echo '<li>'.$func.'</li>';  }  echo '</ul>';}?>

Getting Information About the PHP Environment

523

Figure 24.1  The list_functions.php script shows all the built-in PHP functions available in this installation

Note that the get_loaded_extensions() function doesn’t take any parameters, and the get_extension_funcs() function takes the name of the extension as its only parameter.

This information can be helpful if you are trying to tell whether you have successfully installed an extension or if you are trying to write portable code that generates useful diagnostic messages when installing.

Identifying the Script OwnerYou can find out the user who owns the script being run with a call to the get_current_user() function, as follows:

echo get_current_user();

This information can sometimes be useful for solving permissions issues.

Finding Out When the Script Was ModifiedAdding a last modification date to each page in a site is a fairly popular thing to do.

524

Chapter 24  Other Useful Features

You can check the last modification date of a script with the getlastmod() (note the lack of underscores in the function name) function, as follows:

echo date('g:i a, j M Y',getlastmod());

The function getlastmod() returns a Unix timestamp, which you can feed to date(), as done here, to produce a human-readable date.

Temporarily Altering the Runtime EnvironmentYou can view the directives set in the php.ini file or change them for the life of a single script. This capability can be particularly useful, for example, in conjunction with the max_execution_time directive if you know your script will take some time to run.

You can access and change the directives using the twin functions ini_get() and ini_set(). Listing 24.2 shows a simple script that uses these functions.

Listing 24.2  iniset.php—Resets Variables from the php.ini File<?php$old_max_execution_time = ini_set('max_execution_time', 120);echo 'old timeout is '.$old_max_execution_time.'<br />'; $max_execution_time = ini_get('max_execution_time');echo 'new timeout is '.$max_execution_time.'<br />';?>

The ini_set() function takes two parameters. The first is the name of the configuration  directive from php.ini that you would like to change, and the second is the value you would like to change it to. It returns the previous value of the directive.

In this case, you reset the value from the default 30-second (or whatever is set in your php.ini file) maximum time for a script to run to 120 seconds.

The ini_get() function simply checks the value of a particular configuration directive. The directive name should be passed to it as a string. Here, it just checks that the value really did change.

Not all INI options can be set this way. Each option has a level at which it can be set. The possible levels are

 ■ PHP_INI_USER—You can change these values in your scripts with ini_set().

 ■ PHP_INI_PERDIR—You can change these values in php.ini or in .htaccess or 

httpd.conf files if using Apache. The fact that you can change them in .htaccess files means that you can change these values on a per-directory basis—hence the name.

Highlighting Source Code

525

 ■ PHP_INI_SYSTEM—You can change these values in the php.ini or httpd.conf files.

 ■ PHP_INI_ALL—You can change these values in any of the preceding ways—that is, in a 

script, in an .htaccess file, or in your httpd.conf or php.ini files.

The full set of ini options and the levels at which they can be set is in the PHP manual at http://php.net/manual/en/ini.list.php.

Highlighting Source CodePHP comes with a built-in syntax highlighter, similar to many IDEs. In particular, it is useful for sharing code with others or presenting it for discussion on a web page.

The functions show_source() and highlight_file() are the same. (The show_source() function is actually an alias for highlight_file().) Both of these functions accept a filename as the parameter. (This file should be a PHP file; otherwise, you won’t get a very meaningful result.) Consider this example:

show_source('list_functions.php');

The file is echoed to the browser with the text highlighted in various colors depending on whether it is a string, a comment, a keyword, or HTML. The output is printed on a background color. Content that doesn’t fit into any of these categories is printed in a default color.

The highlight_string() function works similarly, but it takes a string as parameter and prints it to the browser in a syntax-highlighted format.

You can set the colors for syntax highlighting in your php.ini file. The section you want to change looks like this:

; Colors for Syntax Highlighting modehighlight.string    =    #DD0000highlight.comment   =    #FF9900highlight.keyword   =    #007700highlight.bg        =    #FFFFFFhighlight.default   =    #0000BBhighlight.html      =    #000000

The colors are in standard HTML RGB format.

Although you won’t be able to see the colors in the printed version of this book, you will in the electronic version of this book, and so Figure 24.2 shows the output of the show_source() function on the script in Listing 24.1.

526

Chapter 24  Other Useful Features

Figure 24.2  The show_source() function highlights PHP code in customizable colors

Using PHP on the Command LineYou can usefully write or download many small programs and run them on the command line. If you are on a Unix system, these programs are usually written in a shell scripting language or Perl. If you are on a Windows system, they are usually written as a batch file.

You probably first came to PHP for a web project, but the same text processing facilities that make it a strong web language make it a strong command-line utility program.

There are three ways to execute a PHP script at the command line: from a file, through a pipe, or directly on the command line.

To execute a PHP script in a file, make sure that the PHP executable (php or php.exe depending on your operating system) is in your path and call it with the name of script as an argument. Here’s an example:

php myscript.php

The file myscript.php is just a normal PHP file, so it contains any normal PHP syntax within PHP tags.

To pass code through a pipe, you can run any program that generates a valid PHP script as output and pipe that to the php executable. The following example uses the program echo to give a one-line program:

echo '<?php for($i=1; $i<10; $i++) echo $i; ?>' | php

Again, the PHP code here is enclosed in PHP tags (<?php and ?>). Also note that this is the command-line program echo, not the PHP language construct.

Next

527

A one-line program of this nature would be easier to pass directly from the command line, as in this example:

php -r 'for($i=1; $i<10; $i++) echo $i;'

The situation is slightly different here. The PHP code passed in this string is not enclosed in PHP tags. If you do enclose the string in PHP tags, you will get a syntax error.

The useful PHP programs that you can write for command-line use are unlimited. You can write installers for your PHP applications. You can knock together a quick script to reformat a text file before importing it to your database. You can even make a script do any repetitive tasks that you might need to do at the command line; a good candidate would be a script to copy all your PHP files, images, and MySQL table structures from your staging web server to your production one.

NextPart V,「Building Practical PHP and MySQL Projects,」covers a number of relatively complicated practical projects using PHP and MySQL. These projects provide useful examples for similar tasks you might have and demonstrate the use of PHP and MySQL on larger projects.

Chapter 25 addresses some of the issues you face when coding larger projects using PHP. They include software engineering principles such as design, documentation, and change management.

This page intentionally left blank 

