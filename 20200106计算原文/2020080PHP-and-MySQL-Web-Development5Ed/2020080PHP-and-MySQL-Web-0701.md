# 07. Error and Exception Handling

In this chapter, we explain the concept of exception handling and the way it is  implemented in PHP. Exceptions provide a unified mechanism for handling errors in an extensible, maintainable, and object-oriented way.

Key topics covered in this chapter include

 ■ Exception handling concepts

 ■ Exception control structures: try...throw...catch

 ■ The Exception class

 ■ User-defined exceptions

 ■ Exceptions in Bob’s Auto Parts

 ■ Exceptions and PHP’s other error handling mechanisms

Exception Handling ConceptsThe basic idea of exception handling is that code is executed inside what is called a try block. That’s a section of code that looks like this:

try{  // code goes here}

If something goes wrong inside the try block, you can do what is called throwing an exception. Some languages, such as Java, throw exceptions automatically for you in certain cases. In PHP, exceptions must be thrown manually. You throw an exception as follows:

throw new Exception($message, $code);

200

Chapter 7  Error and Exception Handling

The keyword throw triggers the exception handling mechanism. It is a language construct rather than a function, but you need to pass it a value. It expects to receive an object. In the simplest case, you can instantiate the built-in Exception class, as done in this example.

The constructor for this class takes up to three parameters: a message, a code, and a previous exception. The first two are intended to represent an error message and an error code number. The third can be used to pass in the previously thrown exception when you are dealing with a chain of exceptions. All of these parameters are optional.

Underneath your try block, you need at least one catch block. A catch block looks like this:

catch (typehint exception){  // handle exception}

You can have more than one catch block associated with a single try block. Using more than one would make sense if each catch block is waiting to catch a different type of exception. For example, if you want to catch exceptions of the Exception class, your catch block might look like this:

catch (Exception $e){  // handle exception}

The object passed into (and caught by) the catch block is the one passed to (and thrown by) the throw statement that raised the exception. The exception can be of any type, but it is good form to use either instances of the Exception class or instances of your own user-defined exceptions that inherit from the Exception class. (You will see how to define your own  exceptions later in the chapter.)

When an exception is raised, PHP looks for a matching catch block. If you have more than one catch block, the objects passed in to each should be of different types so that PHP can work out which catch block to fall through to.

Finally, beneath all of your catch blocks, you may choose to have a finally block. This block of code will always be executed after the try and catch blocks, regardless of whether an exception is thrown or caught. A finally block after a try block and a catch block looks like this:

try {                                                                // do something, maybe throw some exceptions                     } catch (Exception $e) {                                             // handle exception                                              } finally {                                                          echo 'Always runs!';                                             }  

One other point to note is that you can raise further exceptions within a catch block.

To make this discussion a bit clearer, let’s look at an example. A simple exception handling example is shown in Listing 7.1.

The Exception Class

201

Listing 7.1  basic_exception.php—Throwing and Catching an Exception<?php

try  {  throw new Exception("A terrible error has occurred", 42);}catch (Exception $e) {  echo "Exception ". $e->getCode(). ": ". $e->getMessage()."<br />".  " in ". $e->getFile(). " on line ". $e->getLine(). "<br />";}

?>

In Listing 7.1, you can see that we used a number of methods of the Exception class, which we discuss shortly. The result of running this code is shown in Figure 7.1.

Figure 7.1  This catch block reports the exception error message and notes where it occurred

In the sample code, you can see that we raise an exception of class Exception. This built-in class has methods you can use in the catch block to report a useful error message.

The Exception ClassPHP has a built-in class called Exception. The constructor takes three optional parameters, as we discussed previously: an error message, an error code, and a previous exception.

In addition to the constructor, this class comes with the following built-in methods:

 ■ getCode()—Returns the code as passed to the constructor

 ■ getMessage()—Returns the message as passed to the constructor

202

Chapter 7  Error and Exception Handling

 ■ getFile()—Returns the full path to the code file where the exception was raised

 ■ getLine()—Returns the line number in the code file where the exception was raised

 ■ getTrace()—Returns an array containing a backtrace where the exception was raised

 ■ getTraceAsString()—Returns the same information as getTrace, formatted as a string

 ■ getPrevious()—Returns the previous exception (from the third parameter to the 

constructor)

 ■ __toString()—Allows you to simply echo an Exception object, giving all the 

information from the above methods

You can see that we used the first four of these methods in Listing 7.1. You could obtain the same information (plus the backtrace) by executing

echo $e;

A backtrace shows which functions were executing at the time the exception was raised.

User-Defined ExceptionsInstead of instantiating and passing an instance of the base Exception class, you can pass any other object you like. In most cases, you will extend the Exception class to create your own exception classes.

You can pass any other object with your throw clause. You may occasionally want to do this if you are having problems with one particular object and want to pass it through for debugging purposes.

Most of the time, however, you will extend the base Exception class. The PHP manual provides code that shows the skeleton of the Exception class. This code, taken from http://php.net/manual/en/language.exceptions.extending.php, is reproduced in Listing 7.2. Note that this is not the actual code but represents what you can expect to inherit.

Listing 7.2  Exception class—This Is What You Can Expect to Inherit<?phpclass Exception{    protected $message = 'Unknown exception';   // exception message    private   $string;                          // __toString cache    protected $code = 0;                        // user defined exception code    protected $file;                            // source filename of exception    protected $line;                            // source line of exception    private   $trace;                           // backtrace    private   $previous;                        //  previous exception if nested 

exception

 

User-Defined Exceptions

203

    public function __construct($message = null, $code = 0, Exception $previous = null);

    final private function __clone();           // Inhibits cloning of exceptions.

    final public  function getMessage();        // message of exception    final public  function getCode();           // code of exception    final public  function getFile();           // source filename    final public  function getLine();           // source line    final public  function getTrace();          // an array of the backtrace()    final public  function getPrevious();       // previous exception    final public  function getTraceAsString();  // formatted string of trace

    /* Overrideable */    public function __toString();               // formatted string for display}?> 

The main reason we are looking at this class definition is to note that most of the public methods are final: That means you cannot override them. You can create your own subclass Exceptions, but you cannot change the behavior of the basic methods. Note that you can override the __toString() function, so you can change ssthe way the exception is displayed.  You can also add your own methods.

An example of a user-defined Exception class is shown in Listing 7.3.

Listing 7.3   user_defined_exception.php—An Example of a User-Defined 

Exception Class

<?php

class myException extends Exception{  function __toString()   {       return "<strong>Exception ".$this->getCode()       ."</strong>: ".$this->getMessage()."<br />"       ."in ".$this->getFile()." on line ".$this->getLine()."<br/>";   }}

try{  throw new myException("A terrible error has occurred", 42);}

204

Chapter 7  Error and Exception Handling

catch (myException $m){   echo $m;}

?>

In this code, you declare a new exception class, called myException, that extends the basic Exception class. The difference between this class and the Exception class is that you override the __toString() method to provide a「pretty」way of printing the exception. The output from executing this code is shown in Figure 7.2. As you can see, it’s similar to the previous example.

Figure 7.2  The myException class provides exceptions with「pretty printing」

This example is fairly simple. In the next section, we look at ways to create different exceptions to deal with different categories of error.

Exceptions in Bob’s Auto PartsChapter 2,「Storing and Retrieving Data,」described how you could store Bob’s order data in a flat file. You know that file I/O (in fact, any kind of I/O) is one area in programs where errors often occur. This makes it a good place to apply exception handling.

Looking back at the original code, you can see that three things are likely to go wrong with writing to the file: the file cannot be opened, a lock cannot be obtained, or the file cannot be written to. We created an exception class for each of these possibilities. The code for these exceptions is shown in Listing 7.4.

Exceptions in Bob’s Auto Parts

205

Listing 7.4  file_exceptions.php—File I/O-Related Exceptions<?php

class fileOpenException extends Exception{  function __toString()  {       return "fileOpenException ". $this->getCode()              . ": ". $this->getMessage()."<br />"." in "              . $this->getFile(). " on line ". $this->getLine()              . "<br />";   }}

class fileWriteException extends Exception{  function __toString()  {       return "fileWriteException ". $this->getCode()              . ": ". $this->getMessage()."<br />"." in "              . $this->getFile(). " on line ". $this->getLine()              . "<br />";   }}

class fileLockException extends Exception{  function __toString()  {       return "fileLockException ". $this->getCode()              . ": ". $this->getMessage()."<br />"." in "              . $this->getFile(). " on line ". $this->getLine()              . "<br />";   }}?>

These Exception subclasses do not do anything particularly interesting. In fact, for the purpose of this application, you could leave them as empty subclasses or use the provided Exception class. We have, however, provided a __toString() method for each of the subclasses that explains what type of exception has occurred.

We rewrote the processorder.php file from Chapter 2 to incorporate the use of exceptions. The new version is shown in Listing 7.5.

206

Chapter 7  Error and Exception Handling

Listing 7.5   processorder.php—Bob’s Order-Processing Script with Exception 

Handling Included

<?php  require_once("file_exceptions.php");

  // create short variable names  $tireqty = (int) $_POST['tireqty'];                                 $oilqty = (int) $_POST['oilqty'];                                   $sparkqty = (int) $_POST['sparkqty'];                               $address = preg_replace('/\t|\R/',' ',$_POST['address']);           $document_root = $_SERVER['DOCUMENT_ROOT'];                         $date = date('H:i, jS F Y'); ?><!DOCTYPE html><html>  <head>    <title>Bob's Auto Parts - Order Results</title>  </head>  <body>    <h1>Bob's Auto Parts</h1>    <h2>Order Results</h2>     <?php      echo "<p>Order processed at ".date('H:i, jS F Y')."</p>";      echo "<p>Your order is as follows: </p>";

      $totalqty = 0;      $totalamount = 0.00;

      define('TIREPRICE', 100);      define('OILPRICE', 10);      define('SPARKPRICE', 4);

      $totalqty = $tireqty + $oilqty + $sparkqty;      echo "<p>Items ordered: ".$totalqty."<br />";

      if ($totalqty == 0) {        echo "You did not order anything on the previous page!<br />";      } else {        if ($tireqty > 0) {          echo htmlspecialchars($tireqty).' tires<br />';        }        if ($oilqty > 0) {          echo htmlspecialchars($oilqty).' bottles of oil<br />';        }        if ($sparkqty > 0) {          echo htmlspecialchars($sparkqty).' spark plugs<br />';        }      }

Exceptions in Bob’s Auto Parts

207

      $totalamount = $tireqty * TIREPRICE                   + $oilqty * OILPRICE                   + $sparkqty * SPARKPRICE;

      echo "Subtotal: $".number_format($totalamount,2)."<br />";

      $taxrate = 0.10;  // local sales tax is 10%      $totalamount = $totalamount * (1 + $taxrate);      echo "Total including tax: $".number_format($totalamount,2)."</p>";

      echo "<p>Address to ship to is ".htmlspecialchars($address)."</p>";

      $outputstring = $date."\t".$tireqty." tires \t".$oilqty." oil\t"                      .$sparkqty." spark plugs\t\$".$totalamount                      ."\t". $address."\n";

      // open file for appending      try      {        if (!($fp = @fopen("$document_root/../orders/orders.txt", 'ab'))) {            throw new fileOpenException();        }

        if (!flock($fp, LOCK_EX)) {           throw new fileLockException();        }

        if (!fwrite($fp, $outputstring, strlen($outputstring))) {           throw new fileWriteException();        }

        flock($fp, LOCK_UN);        fclose($fp);        echo "<p>Order written.</p>";      }      catch (fileOpenException $foe)      {         echo "<p><strong>Orders file could not be opened.<br/>               Please contact our webmaster for help.</strong></p>";      }      catch (Exception $e)      {         echo "<p><strong>Your order could not be processed at this time.<br/>               Please try again later.</strong></p>";      }    ?>  </body></html>

208

Chapter 7  Error and Exception Handling

You can see that the file I/O section of the script is wrapped in a try block. It is generally considered good coding practice to have small try blocks and catch the relevant exceptions at the end of each. This makes your exception handling code easier to write and maintain because you can see what you are dealing with.

If you cannot open the file, you throw a fileOpenException; if you cannot lock the file, you throw a fileLockException; and if you cannot write to the file, you throw a fileWriteException.

Look at the catch blocks. To illustrate a point, we have included only two: one to handle fileOpenExceptions and one to handle Exceptions. Because the other exceptions inherit from Exception, they will be caught by the second catch block. The catch blocks are matched on the same basis as the instanceof operator. This is a good reason for extending your own exception classes from a single class.

One important warning: If you raise an exception for which you have not written a matching catch block, PHP will report a fatal error.

Exceptions and PHP’s Other Error Handling MechanismsIn addition to the exception handling mechanism discussed in this chapter, PHP has complex error handling support, which we consider in Chapter 26,「Debugging and Logging.」Note that the process of raising and handling exceptions does not interfere or prevent this error handling mechanism from operating.

In Listing 7.5, notice how the call to fopen() is still prefaced with the @ error  suppression  operator. If it fails, PHP will issue a warning that may or may not be reported or logged  depending on the error reporting settings in php.ini. These settings are discussed at length in Chapter 26, but you need to know that this warning will still be issued regardless of whether you raise an exception.

Further ReadingBasic information about exception handling is plentiful. Oracle has a good tutorial about what exceptions are and why you might want to use them (written from a Java perspective, of course) at http://docs.oracle.com/javase/tutorial/essential/exceptions/handling.html.

NextThe next part of the book deals with MySQL. We explain how to create and populate a MySQL database and then link what you’ve learned to PHP so that you can access your database from the web.