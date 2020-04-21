# 02. Storing and Retrieving Data

Now that you know how to access and manipulate data entered in an HTML form, you can look at ways of storing that information for later use. In most cases, including the example from the previous chapter, you’ll want to store this data and load it later. In this case, you need to write customer orders to storage so that they can be filled later.

In this chapter, you learn how to write the customer’s order from the previous example to a file and read it back. You also learn why this isn’t always a good solution. When you have large numbers of orders, you should use a database management system such as MySQL instead.

Key topics covered in this chapter include:

 ■ Saving data for later.

 ■ Opening a file.

 ■ Creating and writing to a file.

 ■ Closing a file.

 ■ Reading from a file.

 ■ Locking files.

 ■ Deleting files.

 ■ Using other useful file functions.

 ■ Doing it a better way: using database management systems.

## 01. Saving Data for Later

You can store data in two basic ways: in flat files or in a database. A flat file can have many formats, but in general, when we refer to a flat file, we mean a simple text file. For this chapter’s example, you will write customer orders to a text file, one order per line.

Writing orders this way is very simple, but also limiting, as you’ll see later in this chapter. If you’re dealing with information of any reasonable volume, you’ll probably want to use a database instead. However, flat files have their uses, and in some situations you need to know how to use them.

The processes of writing to and reading from files are similar in many programming languages. If you’ve done any C programming or Unix shell scripting, these procedures will seem familiar to you.

## 02. Storing and Retrieving Bob’s Orders

In this chapter, you use a slightly modified version of the order form you looked at in the preceding chapter. Begin with this form and the PHP code you wrote to process the order data. We’ve modified the form to include a quick way to obtain the customer’s shipping address. You can see this modified form in Figure 2.1.

Figure 2.1  This version of the order form gets the customer’s shipping address

The form field for the shipping address is called address. This gives you a variable you can access as \$\_REQUEST['address'] or \$\_POST['address'] or \$\_GET['address'], depending on the form submission method. (See Chapter 1,「PHP Crash Course,」for details.)

In this chapter, you write each order that comes in to the same file. Then you construct a web interface for Bob’s staff to view the orders that have been received.

## 03. Processing Files

Writing data to a file requires three steps: 1) Open the file. If the file doesn’t already exist, you need to create it. 2) Write the data to the file. 3) Close the file.

Similarly, reading data from a file takes three steps: 1) Open the file. If you cannot open the file (for example, if it doesn’t exist), you need to recognize this and exit gracefully. 2) Read data from the file. 3) Close the file.

When you want to read data from a file, you have many choices about how much of the file to read at a time. We’ll describe some common choices in detail. For now, we’ll start at the beginning by opening a file.

## 04. Opening a File

To open a file in PHP, you use the fopen() function. When you open the file, you need to specify how you intend to use it. This is known as the file mode.

### 1. Choosing File Modes

The operating system on the server needs to know what you want to do with a file that you are opening. It needs to know whether the file can be opened by another script while you have it open and whether you (or the script owner) have permission to use it in the requested way. Essentially, file modes give the operating system a mechanism to determine how to handle access requests from other people or scripts and a method to check that you have access and permission to a particular file.

You need to make three choices when opening a file: 1) You might want to open a file for reading only, for writing only, or for both reading and writing. 2) If writing to a file, you might want to overwrite any existing contents of a file or append new data to the end of the file. You also might like to terminate your program gracefully instead of overwriting a file if the file already exists. 3) If you are trying to write to a file on a system that differentiates between binary and text files, you might need to specify this fact. The fopen() function supports combinations of these three options.

### 2. Using fopen() to Open a File

Assume that you want to write a customer order to Bob’s order file. You can open this file for writing with the following:

```php
$fp = fopen("$document_root/../orders/orders.txt", 'w');
```

When fopen() is called, it expects two, three, or four parameters. Usually, you use two, as shown in this code line.

The first parameter should be the file you want to open. You can specify a path to this file, as in the preceding code; here, the orders.txt file is in the orders directory. We used the PHP built-in variable \$\_SERVER['DOCUMENT_ROOT'] but, as with the cumbersome full names for form variables, we assigned a shorter name.

This variable points at the base of the document tree on your web server. This code line uses .. to mean「the parent directory of the document root directory.」This directory is outside the document tree, for security reasons. In this case, we do not want this file to be web acces-sible except through the interface that we provide. This path is called a relative path because it describes a position in the file system relative to the document root. As with the short names given form variables, you need the following line at the start of your script to copy the contents of the long-style variable to the short-style name.

```php
$document_root = $_SERVER['DOCUMENT_ROOT'];
```

You could also specify an absolute path to the file. This is the path from the root directory (/ on a Unix system and typically C:\ on a Windows system). On our Unix server, this path could be something like /data/orders. If no path is specified, the file will be created or looked for in the same directory as the script itself. The directory used will vary if you are running PHP through some kind of CGI wrapper and depends on your server configuration.

In a Unix environment, you use forward slashes (/) in directory paths. If you are using a Windows platform, you can use forward (/) or backslashes (\). If you use backslashes, they must be escaped (marked as a special character) for fopen() to understand them properly. To escape a character, you simply add an additional backslash in front of it, as shown in the following:

```php
$fp = fopen("$document_root\\..\\orders\\orders.txt", 'w');
```

Very few people use backslashes in paths within PHP because it means the code will work only in Windows environments. If you use forward slashes, you can often move your code between Windows and Unix machines without alteration.

The second fopen() parameter is the file mode, which should be a string. This string speci-fies what you want to do with the file. In this case, we are passing 'w' to fopen(); this means「open the file for writing.」A summary of file modes is shown in Table 2.1.

Table 2.1  Summary of File Modes for fopen()

Mode Mode Name Meaning

r, Open the file for reading, beginning from the start of the file.

r+, Open the file for reading and writing, beginning from the start of the file.

w, Open the file for writing, beginning from the start of the file. If the file already exists, delete the existing contents. If it does not exist, try to  create it.

w+, Open the file for writing and reading, beginning from the start of the file. If the file already exists, delete the existing contents. If it does not exist, try to create it.

x, Open the file for writing, beginning from the start of the file. If the file already exists, it will not be opened, fopen() will return false, and PHP will generate a warning.

x+, Open the file for writing and reading, beginning from the start of the file. If the file already exists, it will not be opened, fopen() will return false, and PHP will generate a warning.

a, Open the file for appending (writing) only, starting from the end of the  existing contents, if any. If it does not exist, try to create it.

a+, Open the file for appending (writing) and reading, starting from the end of the existing contents, if any. If it does not exist, try to create it.

b, Used in conjunction with one of the other modes. You might want to use this mode if your file system differentiates between binary and text files. Windows systems differentiate; Unix systems do not. The PHP developers recommend you always use this option for maximum portability. It is the default mode.

t, Used in conjunction with one of the other modes. This mode is an option only in Windows systems. It is not recommended except before you have ported your code to work with the b option.

The right file mode to choose depends on how the system will be used. We used 'w' in this example which allows only one order to be stored in the file. Each time a new order is taken, it overwrites the previous order. This usage is probably not very sensible, so you would be better off specifying append mode (and binary mode, as recommended):

```php
$fp = fopen("$document_root/../orders/orders.txt", 'ab');
```

The third parameter of fopen() is optional. You can use it if you want to search the include\_path (set in your PHP configuration; see Appendix A,「Installing Apache, PHP, and MySQL」) for a file. If you want to do this, set this parameter to true. If you tell PHP to search the include\_path, you do not need to provide a directory name or path:

```php
$fp = fopen('orders.txt', 'ab', true);
```

The fourth parameter is also optional. The fopen() function allows filenames to be prefixed with a protocol (such as http://) and opened at a remote location. Some protocols allow for an extra parameter. We look at this use of the fopen() function in the next section of this chapter.

If fopen() opens the file successfully, a resource that is effectively a handle or pointer to the file is returned and should be stored in a variable—in this case, \$fp. You use this variable to access the file when you actually want to read from or write to it.

### 3. Opening Files Through FTP or HTTP

In addition to opening local files for reading and writing, you can open files via FTP, HTTP, and other protocols using fopen(). You can disable this capability by turning off the allow\_url\_fopen directive in the php.ini file. If you have trouble opening remote files with fopen(), check your php.ini file.

If the filename you use begins with ftp://, a passive mode FTP connection will be opened to the server you specify and a pointer to the start of the file will be returned. If the filename you use begins with http://, an HTTP connection will be opened to the server you specify and a pointer to the response will be returned. Remember that the domain names in your URL are not case sensitive, but the path and file-name might be.

### 4. Addressing Problems Opening Files

An error you might make is trying to open a file you don’t have permission to read from or write to. (This error occurs commonly on Unix-like operating systems, but you may also see it occasionally under Windows.) When you do, PHP gives you a warning similar to the one shown in Figure 2.2.

Figure 2.2  PHP specifically warns you when a file can’t be opened

If you receive this error, you need to make sure that the user under which the script runs has permission to access the file you are trying to use. Depending on how your server is set up, the script might be running as the web server user or as the owner of the directory where the script is located.

On most systems, the script runs as the web server user. If your script is on a Unix system in the ~/public_html/chapter02/ directory, for example, you could create a group-writable directory in which to store the order by typing the following:

```
mkdir path/to/orders
chgrp apache path/to/orders
chmod 775 path/to/orders
```

1『

由于用的是 laravel 框架，第 2 步不需要，进入根目录 public 后：

```
mkdir orders
chmod 775 orders
```

』

You could also choose to change ownership of the file to the web server user. Some people will choose to make the file world-writable as a shortcut here, but bear in mind that directories and files that anybody can write to are dangerous. In particular, directories that are accessible directly from the Web should not be writable. For this reason, our orders directory is outside the document tree. We discuss security more in Chapter 15「Building a Secure Web Application.」

Incorrect permission setting is probably the most common thing that can go wrong when opening a file, but it’s not the only thing. If you can’t open the file, you really need to know this so that you don’t try to read data from or write data to it.

If the call to fopen() fails, the function will return false. It will also cause PHP to emit a warning\_level error (E\_WARNING). You can deal with the error in a more user-friendly way by suppressing PHP’s error message and giving your own:

```php
@$fp = fopen("$document_root/../orders/orders.txt", 'ab');
if (!$fp){  
    echo "<p><strong> Your order could not be processed at this time.  "       
        .Please try again later.</strong></p></body></html>";  
    exit;
}
```

The @ symbol in front of the call to fopen() tells PHP to suppress any errors resulting from the function call. Usually, it’s a good idea to know when things go wrong, but in this case we’re going to deal with that problem elsewhere. You can also write this line as follows:

```php
$fp = @fopen("$document_root/../orders/orders.txt", 'a');
```

1『 @ 的用法，处理错误的时候用，可以「压制」任何函数调用时的错误。』

Using this method tends to make it less obvious that you are using the error suppression operator, so it may make your code harder to debug.

Note: In general, use of the error suppression operator is not considered good style, so consider it a shortcut for now. The method described here is a simplistic way of dealing with errors. We look at a more elegant method for error handling in Chapter 7「Error and Exception Handling.」But one thing at a time.

The if statement tests the variable \$fp to see whether a valid file pointer was returned from the fopen() call; if not, it prints an error message and ends script execution.

The output when using this approach is shown in Figure 2.3.

Figure 2.3  Using your own error messages instead of PHP’s is more user friendly

### 5. Writing to a File

Writing to a file in PHP is relatively simple. You can use either of the functions fwrite() (file write) or fputs() (file put string); fputs() is an alias to fwrite(). You call fwrite() in the following way:

```php
fwrite($fp, $outputstring);
```

This function call tells PHP to write the string stored in \$outputstring to the file pointed to by \$fp.

An alternative to fwrite() is the file\_put\_contents() function. It has the following prototype:

```php
int file_put_contents ( 
    string filename,                        
    mixed data                         
    [, int flags                         
    [, resource context]]
)
```

This function writes the string contained in data to the file named in filename without any need for an fopen() (or fclose()) function call. This function is the half of a matched pair, the other half being file_get_contents(), which we discuss shortly. You most commonly use the flags and context optional parameters when writing to remote files using, for example, HTTP or FTP. (We discuss these functions in Chapter 18,「Using Network and Protocol Functions.」)

Parameters for fwrite()The function fwrite() actually takes three parameters, but the third one is optional. The prototype for fwrite() is

int fwrite ( resource handle, string [, int length])

The third parameter, length, is the maximum number of bytes to write. If this parameter is supplied, fwrite() will write string to the file pointed to by handle until it reaches the end of string or has written length bytes, whichever comes first.

You can obtain the string length by using PHP’s built-in strlen() function, as follows:

fwrite($fp, $outputstring, strlen($outputstring));

You may want to use this third parameter when writing in binary mode because it helps avoid some cross-platform compatibility issues.

File FormatsWhen you are creating a data file like the one in the example, the format in which you store the data is completely up to you. (However, if you are planning to use the data file in another application, you may have to follow that application’s rules.)

Now construct a string that represents one record in the data file. You can do this as follows:

$outputstring = $date.'\t'.$tireqty.' tires \t'.$oilqty.' oil\t'                  .$sparkqty.' spark plugs\t\$'.$totalamount                  .'\t'. $address.'\n';

In this simple example, you store each order record on a separate line in the file. Writing one record per line gives you a simple record separator in the newline character. Because newlines are invisible, you can represent them with the control sequence "\n".

Throughout the book, we write the data fields in the same order every time and separate fields with a tab character. Again, because a tab character is invisible, it is represented by the control sequence "\t". You may choose any sensible delimiter that is easy to read back.

The separator or delimiter character should be something that will certainly not occur in the input, or you should process the input to remove or escape out any instances of the delimiter. For now, if you look at the full code listing, you’ll see that we have used a regular expression function (preg_replace()) to strip out potentially problematic characters. We will explain this fully when we look at processing input in Chapter 4,「String Manipulation and Regular Expressions.」

Using a special field separator allows you to split the data back into separate variables more easily when you read the data back. We cover this topic in Chapter 3,「Using Arrays,」and Chapter 4. Here, we treat each order as a single string.

After a few orders are processed, the contents of the file look something like the example shown in Listing 2.1.

Closing a File

63

Listing 2.1  orders.txt—Example of What the Orders File Might Contain18:55, 16th April 2013  4 tires  1 oil  6 spark plugs  $477.4 22 Short St, Smalltown18:56, 16th April 2013  1 tires  0 oil  0 spark plugs  $110   33 Main Rd, Oldtown18:57, 16th April 2013  0 tires  1 oil  4 spark plugs  $28.6  127 Acacia St, Springfield

Closing a FileAfter you’ve finished using a file, you need to close it. You should do this by using the fclose() function as follows:

fclose($fp);

This function returns true if the file was successfully closed or false if it wasn’t. This process is much less likely to go wrong than opening a file in the first place, so in this case we’ve chosen not to test it.

The complete listing for the final version of processorder.php is shown in Listing 2.2.

Listing 2.2  processorder.php—Final Version of the Order Processing Script<?php  // create short variable names  $tireqty = (int) $_POST['tireqty'];  $oilqty = (int) $_POST['oilqty'];  $sparkqty = (int) $_POST['sparkqty'];  $address = preg_replace('/\t|\R/',' ',$_POST['address']);  $document_root = $_SERVER['DOCUMENT_ROOT'];  $date = date('H:i, jS F Y');?><!DOCTYPE html><html>  <head>    <title>Bob's Auto Parts - Order Results</title>  </head>  <body>    <h1>Bob's Auto Parts</h1>    <h2>Order Results</h2>     <?php      echo "<p>Order processed at ".date('H:i, jS F Y')."</p>";      echo "<p>Your order is as follows: </p>";       $totalqty = 0;      $totalamount = 0.00;       define('TIREPRICE', 100);

64

Chapter 2  Storing and Retrieving Data

      define('OILPRICE', 10);      define('SPARKPRICE', 4);

      $totalqty = $tireqty + $oilqty + $sparkqty;      echo "<p>Items ordered: ".$totalqty."<br />";

      if ($totalqty == 0) {        echo "You did not order anything on the previous page!<br />";      } else {        if ($tireqty > 0) {          echo htmlspecialchars($tireqty).' tires<br />';        }        if ($oilqty > 0) {          echo htmlspecialchars($oilqty).' bottles of oil<br />';        }        if ($sparkqty > 0) {          echo htmlspecialchars($sparkqty).' spark plugs<br />';        }      }

      $totalamount = $tireqty * TIREPRICE                   + $oilqty * OILPRICE                   + $sparkqty * SPARKPRICE;

      echo "Subtotal: $".number_format($totalamount,2)."<br />";

      $taxrate = 0.10;  // local sales tax is 10%      $totalamount = $totalamount * (1 + $taxrate);      echo "Total including tax: $".number_format($totalamount,2)."</p>";

      echo "<p>Address to ship to is ".htmlspecialchars($address)."</p>";

      $outputstring = $date."\t".$tireqty." tires \t".$oilqty." oil\t"                      .$sparkqty." spark plugs\t\$".$totalamount                      ."\t". $address."\n";

       // open file for appending       @$fp = fopen("$document_root/../orders/orders.txt", 'ab');

       if (!$fp) {         echo "<p><strong> Your order could not be processed at this time.               Please try again later.</strong></p>";         exit;       }

       flock($fp, LOCK_EX);

Reading from a File

65

       fwrite($fp, $outputstring, strlen($outputstring));       flock($fp, LOCK_UN);       fclose($fp);

       echo "<p>Order written.</p>";    ?>  </body></html>

Reading from a FileRight now, Bob’s customers can leave their orders via the Web, but if Bob’s staff members want to look at the orders, they have to open the files themselves.

Let’s create a web interface to let Bob’s staff read the files easily. The code for this interface is shown in Listing 2.3.

Listing 2.3  vieworders.php—Staff Interface to the Orders File<?php  // create short variable name  $document_root = $_SERVER['DOCUMENT_ROOT'];?><!DOCTYPE html><html>  <head>    <title>Bob's Auto Parts - Order Results</title>  </head>  <body>    <h1>Bob's Auto Parts</h1>    <h2>Customer Orders</h2>    <?php      @$fp = fopen("$document_root/../orders/orders.txt", 'rb');      flock($fp, LOCK_SH); // lock file for reading

      if (!$fp) {        echo "<p><strong>No orders pending.<br />              Please try again later.</strong></p>";        exit;      }

      while (!feof($fp)) {         $order= fgets($fp);         echo htmlspecialchars($order)."<br />";      }

66

Chapter 2  Storing and Retrieving Data

      flock($fp, LOCK_UN); // release read lock      fclose($fp);     ?>  </body></html>

This script follows the sequence we described earlier: open the file, read from the file, close the file. The output from this script using the data file from Listing 2.1 is shown in Figure 2.4.

Figure 2.4  The vieworders.php script displays all the orders currently in the orders.txt file in the browser window

Let’s look at the functions in this script in detail.

Opening a File for Reading: fopen()Again, you open the file by using fopen(). In this case, you open the file for reading only, so you use the file mode 'rb':

$fp = fopen("$document_root/../orders/orders.txt", 'rb');

Knowing When to Stop: feof()In this example, you use a while loop to read from the file until the end of the file is reached. The while loop tests for the end of the file using the feof() function:

while (!feof($fp))

Reading from a File

67

The feof() function takes a file handle as its single parameter. It returns true if the file pointer is at the end of the file. Although the name might seem strange, you can remember it easily if you know that feof stands for File End Of File.

In this case (and generally when reading from a file), you read from the file until EOF is reached.

Reading a Line at a Time: fgets(), fgetss(), and fgetcsv()In this example, you use the fgets() function to read from the file:

$order= fgets($fp);

This function reads one line at a time from a file. In this case, it reads until it encounters a newline character (\n) or EOF.

You can use many different functions to read from files. The fgets() function, for example, is useful when you’re dealing with files that contain plain text that you want to deal with in chunks.

An interesting variation on fgets() is fgetss(), which has the following prototype:

string fgetss(resource fp[, int length[, string allowable_tags]]);

This function is similar to fgets() except that it strips out any PHP and HTML tags found in the string. If you want to leave in any particular tags, you can include them in the  allowable_tags string. You would use fgetss() for safety when reading a file written by somebody else or one containing user input. Allowing unrestricted HTML code in the file could mess up your carefully planned formatting. Allowing unrestricted PHP or JavaScript could give a malicious user an opportunity to create a security problem.

The function fgetcsv() is another variation on fgets(). It has the following prototype:

array fgetcsv ( resource fp, int length [, string delimiter              [, string enclosure              [, string escape]]])

This function breaks up lines of files when you have used a delimiting character, such as the tab character (as we suggested earlier) or a comma (as commonly used by spreadsheets and other applications). If you want to reconstruct the variables from the order separately rather than as a line of text, fgetcsv() allows you to do this simply. You call it in much the same way as you would call fgets(), but you pass it the delimiter you used to separate fields. For example,

$order = fgetcsv($fp, 0, "\t");

This code would retrieve a line from the file and break it up wherever a tab (\t) was encoun-tered. The results are returned in an array ($order in this code example). We cover arrays in more detail in Chapter 3.

68

Chapter 2  Storing and Retrieving Data

The length parameter should be greater than the length in characters of the longest line in the file you are trying to read, or 0 if you do not want to limit the line length.

The enclosure parameter specifies what each field in a line is surrounded by. If not specified, it defaults to " (a double quotation mark).

Reading the Whole File: readfile(), fpassthru(), file(), and file_get_contents()Instead of reading from a file a line at a time, you can read the whole file in one go. Here are four different ways you can do this.

The first uses readfile(). You can replace almost the entire script you wrote previously with one line:

readfile("$document_root/../orders/orders.txt");

A call to the readfile() function opens the file, echoes the content to standard output (the browser), and then closes the file. The prototype for readfile() is

int readfile(string filename, [bool use_include_path[, resource context]] );

The optional second parameter specifies whether PHP should look for the file in the include_path and operates the same way as in fopen(). The optional context parameter is used only when files are opened remotely via, for example, HTTP; we cover such usage in more detail in Chapter 18. The function returns the total number of bytes read from the file.

Second, you can use fpassthru(). To do so, you need to open the file using fopen() first. You can then pass the file pointer as an argument to fpassthru(), which dumps the contents of the file from the pointer’s position onward to standard output. It closes the file when it is finished.

You can use fpassthru() as follows:

$fp = fopen("$document_root/../orders/orders.txt", 'rb');fpassthru($fp);

The function fpassthru() returns true if the read is successful and false otherwise.

The third option for reading the whole file is using the file() function. This function is  identical to readfile() except that instead of echoing the file to standard output, it turns it into an array. We cover this function in more detail when we look at arrays in Chapter 3. Just for reference, you would call it using

$filearray = file("$document_root/../orders/orders.txt");

This line reads the entire file into the array called $filearray. Each line of the file is stored in a separate element of the array. Note that this function was not binary safe in older versions of PHP.

Using Other File Functions

69

The fourth option is to use the file_get_contents() function. This function is identical to readfile() except that it returns the content of the file as a string instead of outputting it to the browser. 

Reading a Character: fgetc()Another option for file processing is to read a single character at a time from a file. You can do this by using the fgetc() function. It takes a file pointer as its only parameter and returns the next character in the file. You can replace the while loop in the original script with one that uses fgetc(), as follows:

while (!feof($fp)){  $char = fgetc($fp);  if (!feof($fp))    echo ($char=="\n" ? "<br />": $char);  }}

This code reads a single character at a time from the file using fgetc() and stores it in $char, until the end of the file is reached. It then does a little processing to replace the text end-of-line characters (\n) with HTML line breaks (<br />). 

This is just to clean up the formatting. If you try to output the file with newlines between records, the whole file will be printed on a single line. (Try it and see.) Web browsers do not render whitespace, such as newlines, so you need to replace them with HTML linebreaks (<br />) instead. You can use the ternary operator to do this neatly.

A minor side effect of using fgetc() instead of fgets() is that fgetc() returns the EOF  character, whereas fgets() does not. You need to test feof() again after you’ve read the  character because you don’t want to echo the EOF to the browser.

Reading a file character by character is not generally sensible or efficient unless for some reason you actually want to process it character by character.

Reading an Arbitrary Length: fread()The final way you can read from a file is to use the fread() function to read an arbitrary number of bytes from the file. This function has the following prototype:

string fread(resource fp, int length);

It reads up to length bytes, to the end of the file or network packet, whichever comes first.

Using Other File FunctionsNumerous other file functions are useful from time to time. Some that we have found handy are described next.

70

Chapter 2  Storing and Retrieving Data

Checking Whether a File Is There: file_exists()If you want to check whether a file exists without actually opening it, you can use file_exists(), as follows:

if (file_exists("$document_root/../orders/orders.txt")) {     echo 'There are orders waiting to be processed.';} else {     echo 'There are currently no orders.';}

Determining How Big a File Is: filesize()You can check the size of a file by using the filesize() function:

echo filesize("$document_root/../orders/orders.txt");

It returns the size of a file in bytes and can be used in conjunction with fread() to read a whole file (or some fraction of the file) at a time. You can even replace the entire original script with the following:

$fp = fopen("$document_root/../orders/orders.txt", 'rb');echo nl2br(fread( $fp, filesize("$document_root/../orders/orders.txt")));fclose( $fp ); 

The nl2br() function converts the \n characters in the output to HTML line breaks (<br />).

Deleting a File: unlink()If you want to delete the order file after the orders have been processed, you can do so by using unlink(). (There is no function called delete.) For example,

unlink("$document_root/../orders/orders.txt");

This function returns false if the file could not be deleted. This situation typically occurs if the permissions on the file are insufficient or if the file does not exist.

Navigating Inside a File: rewind(), fseek(), and ftell()You can manipulate and discover the position of the file pointer inside a file by using rewind(), fseek(), and ftell().

The rewind() function resets the file pointer to the beginning of the file. The ftell()  function reports how far into the file the pointer is in bytes. For example, you can add the following lines to the bottom of the original script (before the fclose() command):

echo 'Final position of the file pointer is '.(ftell($fp));echo '<br />';rewind($fp);echo 'After rewind, the position is '.(ftell($fp));echo '<br />';

The output in the browser should be similar to that shown in Figure 2.5.

Locking Files

71

Figure 2.5  After reading the orders, the file pointer points to the end of the file, an offset of 198 bytes. The call to rewind sets it back to position 0, the start of the file

You can use the function fseek() to set the file pointer to some point within the file. Its prototype is

int fseek ( resource fp, int offset [, int whence])

A call to fseek() sets the file pointer fp at a point starting from whence and moving offset bytes into the file. The optional whence parameter defaults to the value SEEK_SET, which is effectively the start of the file. The other possible values are SEEK_CUR (the current location of the file pointer) and SEEK_END (the end of the file).

The rewind() function is equivalent to calling the fseek() function with an offset of zero. For example, you can use fseek() to find the middle record in a file or to perform a binary search. If you reach the level of complexity in a data file where you need to do these kinds of things, your life will be much easier if you use a built-for-purpose database.

Locking FilesImagine a situation in which two customers are trying to order a product at the same time. (This situation is not uncommon, especially when your website starts to get any kind of traffic volume.) What if one customer calls fopen() and begins writing, and then the other customer calls fopen() and also begins writing? What will be the final contents of the file? Will it be the first order followed by the second order, or vice versa? Will it be one order or the other? 

72

Chapter 2  Storing and Retrieving Data

Or will it be something less useful, such as the two orders interleaved somehow? The answer depends on your operating system but is often impossible to know.

To avoid problems like this, you can use file locking. You use this feature in PHP by using the flock() function. This function should be called after a file has been opened but before any data is read from or written to the file.

The prototype for flock() is

bool flock (resource fp, int operation [, int &wouldblock])

You need to pass it a pointer to an open file and a constant representing the kind of lock you require. It returns true if the lock was successfully acquired and false if it was not. The optional third parameter will contain the value true if acquiring the lock would cause the current process to block (that is, have to wait).

The possible values for operation are shown in Table 2.2.

Table 2.2  flock() Operation Values

Value of Operation

Meaning

LOCK_SH 

LOCK_EX

LOCK_UN

LOCK_NB

Reading lock. The file can be shared with other readers.

Writing lock. This operation is exclusive; the file cannot be shared.

The existing lock is released.

Blocking is prevented while you are trying to acquire a lock. (Not  supported on Windows.)

If you are going to use flock(), you need to add it to all the scripts that use the file; otherwise, it is worthless.

Note that flock() does not work with NFS or other networked file systems. It also does not work with antique file systems that do not support locking, such as FAT. On some operating systems, it is implemented at the process level and does not work correctly if you are using a multithreaded server API. 

To use it with the order example, you can alter processorder.php as follows:

    @ $fp = fopen("$document_root/../orders/orders.txt", 'ab');

    flock($fp, LOCK_EX);

    if (!$fp) {      echo "<p><strong> Your order could not be processed at this time.            Please try again later.</strong></p></body></html>";      exit;    }

    fwrite($fp, $outputstring, strlen($outputstring));

A Better Way: Databases

73

    flock($fp, LOCK_UN);    fclose($fp);

You should also add locks to vieworders.php:

   @$fp = fopen("$document_root/../orders/orders.txt", 'rb');   flock($fp, LOCK_SH); // lock file for reading   // read from file   flock($fp, LOCK_UN); // release read lock   fclose($fp);

The code is now more robust but still not perfect. What if two scripts tried to acquire a lock at the same time? This would result in a race condition, in which the processes compete for locks but it is uncertain which will succeed. Such a condition could cause more problems. You can do better by using a database.

A Better Way: DatabasesSo far, all the examples we have looked at use flat files. In Part II of this book, we look at how to use MySQL, a relational database management system (RDBMS), instead. You might ask,「Why would I bother?」

Problems with Using Flat FilesThere are a number of problems in working with flat files:

 ■ When a file grows large, working with it can be very slow.

 ■ Searching for a particular record or group of records in a flat file is difficult. If the records 

are in order, you can use some kind of binary search in conjunction with a fixed-width record to search on a key field. If you want to find patterns of information (for example, you want to find all the customers who live in Sometown), you would have to read in each record and check it individually.

 ■ Dealing with concurrent access can become problematic. You have seen how to lock files, but locking can cause the race condition we discussed earlier. It can also cause a bottleneck. With enough traffic on a site, a large group of users may be waiting for the file to be unlocked before they can place their order. If the wait is too long, people will go elsewhere to buy.

 ■ All the file processing you have seen so far deals with a file using sequential processing; that is, you start from the beginning of the file and read through to the end. Inserting records into or deleting records from the middle of the file (random access) can be difficult because you end up reading the whole file into memory, making the changes, and writing the whole file out again. With a large data file, having to go through all these steps becomes a significant overhead.

 ■ Beyond the limits offered by file permissions, there is no easy way of enforcing different levels of access to data.

How RDBMSs Solve These ProblemsRelational database management systems address all these issues:

 ■ RDBMSs can provide much faster access to data than flat files. And MySQL, the database 

system we use in this book, has some of the fastest benchmarks of any RDBMS.

 ■ RDBMSs can be easily queried to extract sets of data that fit certain criteria.

 ■ RDBMSs have built-in mechanisms for dealing with concurrent access so that you, as a 

programmer, don’t have to worry about it.

 ■ RDBMSs provide random access to your data.

 ■ RDBMSs have built-in privilege systems. MySQL has particular strengths in this area.

Probably the main reason for using an RDBMS is that all (or at least most) of the functionality that you want in a data storage system has already been implemented. Sure, you could write your own library of PHP functions, but why reinvent the wheel?

In Part II of this book,「Using MySQL,」we discuss how relational databases work generally, and specifically how you can set up and use MySQL to create database-backed websites.

If you are building a simple system and don’t feel you need a full-featured database but want to avoid the locking and other issues associated with using a flat file, you may want to consider using PHP’s SQLite extension. This extension provides essentially an SQL interface to a flat file. In this book, we focus on using MySQL, but if you would like more information about SQLite, you can find it at http://sqlite.org/ and http://www.php.net/sqlite.

Further ReadingFor more information on interacting with the file system, you can go straight to Chapter 17,「Interacting with the File System and the Server.」In that part of the book, we talk about how to change permissions, ownership, and names of files; how to work with directories; and how to interact with the file system environment.

You may also want to read through the file system section of the PHP online manual at http://www.php.net/filesystem.

## Next

In the next chapter, you learn what arrays are and how they can be used for processing data in your PHP scripts.