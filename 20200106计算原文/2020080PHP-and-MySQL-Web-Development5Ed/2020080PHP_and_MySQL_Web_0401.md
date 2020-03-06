4String Manipulation and Regular Expressions

In this chapter, we discuss how you can use PHP’s string functions to format and manipulate text. We also discuss using string functions or regular expression functions to search (and replace) words, phrases, or other patterns within a string.

These functions are useful in many contexts. You often may want to clean up or reformat user input that is going to be stored in a database. Search functions are great when building search engine applications (among other things).

Key topics covered in this chapter include

 ■ Formatting strings

 ■ Joining and splitting strings

 ■ Comparing strings

 ■ Matching and replacing substrings with string functions

 ■ Using regular expressions

Creating a Sample Application: Smart Form MailIn this chapter, you will use string and regular expression functions in the context of a Smart Form Mail application. You’ll then add these scripts to the Bob’s Auto Parts site you’ve been building in preceding chapters.

This time, you’ll build a straightforward and commonly used customer feedback form for Bob’s customers to enter their complaints and compliments, as shown in Figure 4.1. However, this application has one improvement over many you will find on the Web. Instead of  emailing the form to a generic email address like feedback@example.com, you’ll attempt to put some  intelligence into the process by searching the input for key words and phrases and then sending the email to the appropriate employee at Bob’s company. For example, if the email 

102

Chapter 4  String Manipulation and Regular Expressions

contains the word advertising, you might send the feedback to the Marketing department. If the email is from Bob’s biggest client, it can go straight to Bob.

Figure 4.1  Bob’s feedback form asks customers for their name, email address, and comments.

Start with the bare bones script shown in Listing 4.1 and add to it as you read along.

Note that this script, while working, should not be deployed as-is, for reasons we’ll discuss in the next section. We’ll look at a refined version later in the chapter, which will be suitable for actual use.

Listing 4.1  processfeedback.php—Basic Script to Email Form Contents<?php

//create short variable names$name=$_POST['name'];$email=$_POST['email'];$feedback=$_POST['feedback'];

//set up some static information

Creating a Sample Application: Smart Form Mail

103

$toaddress = "feedback@example.com";

$subject = "Feedback from web site";

$mailcontent = "Customer name: ".filter_var($name)."\n".               "Customer email: ".$email."\n".               "Customer comments:\n".$feedback."\n";

$fromaddress = "From: webserver@example.com";

//invoke mail() function to send mailmail($toaddress, $subject, $mailcontent, $fromaddress);

?><!DOCTYPE html><html>  <head>    <title>Bob's Auto Parts - Feedback Submitted</title>  </head>  <body>

    <h1>Feedback submitted</h1>    <p>Your feedback has been sent.</p>

  </body></html>

Generally, you should check that users have filled out all the required form fields using, for example, isset(). We have omitted this function call from the script and other examples for the sake of brevity.

In this script, you can see that we have concatenated the form fields together and used PHP’s mail() function to email them to feedback@example.com. This is a sample email address. If you want to test the code in this chapter, substitute your own email address here. Because we haven’t yet used mail(), we need to discuss how it works.

Unsurprisingly, this function sends email. The prototype for mail() looks like this:

bool mail(string to, string subject, string message,          string [additional_headers [, string additional_parameters]]);

The first three parameters are compulsory and represent the address to send email to, the subject line, and the message contents, respectively. The fourth parameter can be used to send any additional valid email headers. Valid email headers are described in the document RFC822, which is available online if you want more details. (RFCs, or Requests for Comment, are the source of many Internet standards; we discuss them in Chapter 18,「Using Network and Protocol Functions.」) Here, the fourth parameter adds a From: address for the mail. You can also use it to add Reply-To: and Cc: fields, among others. If you want more than one 

104

Chapter 4  String Manipulation and Regular Expressions

additional header, just separate them by using newlines and carriage returns (\\n) within the string, as follows:

$additional_headers="From: webserver@example.com\r\n "                     ."Reply-To: bob@example.com";

The optional fifth parameter can be used to pass a parameter to whatever program you have configured to send mail.

To use the mail() function, set up your PHP installation to point at your mail-sending program. If the script doesn’t work for you in its current form, an installation issue might be at fault, check Appendix A,「Installing Apache, PHP, and MySQL.」

Throughout this chapter, you enhance this basic script by making use of PHP’s string handling and regular expression functions.

Formatting StringsYou often need to clean up user strings (typically from an HTML form interface) before you can use them. The following sections describe some of the functions you can use.

Trimming Strings: chop(), ltrim(), and trim()The first step in tidying up is to trim any excess whitespace from the string. Although this step is never compulsory, it can be useful if you are going to store the string in a file or database, or if you’re going to compare it to other strings.

PHP provides three useful functions for this purpose. In the beginning of the script when you give short names to the form input variables, you can use the trim() function to tidy up your input data as follows:

$name = trim($_POST['name']);$email = trim($_POST['email']);$feedback = trim($_POST['feedback']);

The trim() function strips whitespace from the start and end of a string and returns the  resulting string. The characters it strips by default are newlines and carriage returns (\n and \r), horizontal and vertical tabs (\t and \x0B), end-of-string characters (\0), and spaces. You can also pass it a second parameter containing a list of characters to strip instead of this default list. Depending on your particular purpose, you might like to use the ltrim() or rtrim()  functions instead. They are both similar to trim(), taking the string in question as a parameter and returning the formatted string. The difference between these three is that trim() removes whitespace from the start and end of a string, ltrim() removes whitespace from the start (or left) only, and rtrim() removes whitespace from the end (or right) only.

You may also use the alias chop() for rtrim(). Perl has a similar function but they behave slightly differently, so be cautious in your assumptions if you are coming to PHP from a Perl background.

Formatting Strings

105

Formatting Strings for OutputPHP includes a set of functions that you can use to reformat a string in different ways for different purposes.

Filtering Strings for OutputWhenever we take user-submitted data and output it somewhere, we need to plan it with the destination in mind. This is because most places we send output to consider some  characters and strings as special or control characters and strings, and we don’t want the output  destination to interpret user-submitted data as commands.

For example, if echoing user input to a browser, we don’t want to execute any HTML or JavaScript that the user may have included. This is not only because it might break the  formatting, but also because it is a security vulnerability to allow the execution of arbitrary user-submitted code or commands. We’ll discuss this in a lot more detail in Part III of this book,「Web Application Security.」In that section, we’ll also cover the filter extension, which enables generic filtering per-destination.

Filtering Strings for Output to the Browser with htmlspecialchars()We used this function in previous chapters, but let’s recap here. The htmlspecialchars() function converts characters that have a special meaning in HTML to their HTML entity equivalent. For example, the character < is converted to the entity &lt;.

The prototype of this function is as follows:

string htmlspecialchars (string string [, int flags = ENT_COMPAT | ENT_HTML401 [, string encoding = 'UTF-8' [, bool double_encode = true ]]])

In general, this function converts characters to their HTML entity equivalents as shown in Table 4.1.

Table 4.1  HTML Entities Encoded by the htmlspecialchars() Function

Character

Translation

&

"

'

<

>

&amp;

&quot;

&apos;

&lt;

&gt;

The default encoding of quotes is to only encode double quotes. Single quotes will remain untranslated. This behavior is controlled by the flags parameter.

The first parameter is the string to be translated, and the function returns the translated string.

106

Chapter 4  String Manipulation and Regular Expressions

Note: If the input string is not valid in the specified encoding, the function will return the empty string without raising an error. This is intended to help avoid code injection issues.

The first optional parameter, flags, specifies how the translation should be done. You pass in a bitmask representing the possible values combined together. The default value, as you can see in the prototype above, is ENT_COMPAT | ENT_HTML401. The ENT_COMPAT constant indicates that double quotes should be encoded, and single quotes left as-is, while the ENT_HTML401 constant indicates that code should be treated as HTML 4.01.

The second optional parameter, encoding, specifies the encoding used for conversion. From PHP 5.4 on, the default is UTF-8. Prior to that, it was ISO-8859-1, commonly known as Latin-1. The list of supported encodings may be found in the PHP documentation.

The third optional parameter, double_encode, specifies whether to encode HTML entities. The default is to convert them (again).

The full set of possible values that may be combined in the flags parameter can be found in Table 4.2.

Table 4.2  Flags for the htmlspecialchars() Function

Flag

Meaning

ENT_COMPAT

Encode double quotes but not single quotes

ENT_NOQUOTES

Do not encode either single or double quotes

ENT_QUOTES

Encodes both single and double quotes

ENT_HTML401

Treat code as HTML 4.01

ENT_XML1

ENT_XHTML

ENT_HTML5

ENT_IGNORE

Treat code as XML1

Treat code as XHTML

Treat code as HTML5

Discard invalid code unit sequences instead of returning the empty string. Not recommended for security reasons.

ENT_SUBSTITUTE

Replace invalid code unit sequences with a Unicode Replacement Character.

ENT_DISALLOWED

Replace invalid code points with a Unicode Replacement Character.

Filtering Strings for Other Forms of OutputDepending on where you are outputting strings, the characters that may cause problems are different. We previously discussed the htmlspecialchars() function for output to the browser.

Formatting Strings

107

In the example in Listing 4.1, we are sending output to email. What do we need to take into account here? We don’t care if the email contains HTML, so using the htmlspecialchars() function is not appropriate here.

The main issue in email is that headers are separated by the character string \r\n (carriage return-line feed). We need to take care that user data we use in the email headers does not contain these characters, or we run the risk of a set of attacks, called header injection. (We discuss this in more detail in Part III.)

As with many string processing problems, there are multiple ways to approach this. One way is to use the str_replace() function, as follows:

$mailcontent = "Customer name: ".str_replace("\r\n", "", $name)."\n".               "Customer email: ".str_replace("\r\n", "",$email)."\n".               "Customer comments:\n".str_replace("\r\n", "",$feedback)."\n";

If you have more complicated matching or replacement rules, you can use the regular expression functions described later in this chapter. In a simple case like this where you want to entirely replace one string with another, you should always use the str_replace() function. We’ll discuss the str_replace() function in more detail later in this chapter.

Using HTML Formatting: The nl2br() FunctionThe nl2br() function takes a string as a parameter and replaces all the newlines in it with the HTML <br/> tag. This capability is useful for echoing a long string to the browser. For example, you can use this function to format the customer’s feedback to echo it back:

<p>Your feedback (shown below) has been sent.</p><p><?php echo nl2br(htmlspecialchars($feedback)); ?> </p>

Remember that HTML disregards plain whitespace, so if you don’t filter this output through nl2br(), it will appear on a single line (except for newlines forced by the browser window). The result is illustrated in Figure 4.2.

Notice that we first applied the htmlspecialchars() function and then the nl2br()  function. This is because if we did them in the opposite order, the <br/> tags inserted by the nl2br() function would be translated into HTML entities by the htmlspecialchars()  function and hence would have no effect.

108

Chapter 4  String Manipulation and Regular Expressions

Figure 4.2  Using PHP’s nl2br() function improves the display of long strings within HTML.

At this stage, we have an order processing script that formats user data for output to both email and HTML. The revised order processing script is found in Listing 4.2.

Listing 4.2  processfeedback_v2.php—Revised Script to Email Form Contents<?php

//create short variable names$name = trim($_POST['name']);$email = trim($_POST['email']);$feedback = trim($_POST['feedback']);

//set up some static information$toaddress = "feedback@example.com";

$subject = "Feedback from web site";

$mailcontent = "Customer name: ".str_replace("\r\n", "", $name)."\n".               "Customer email: ".str_replace("\r\n", "",$email)."\n".               "Customer comments:\n".str_replace("\r\n", "",$feedback)."\n";

$fromaddress = "From: webserver@example.com";

//invoke mail() function to send mailmail($toaddress, $subject, $mailcontent, $fromaddress);

Formatting Strings

109

?><!DOCTYPE html><html>  <head>    <title>Bob's Auto Parts - Feedback Submitted</title>  </head>  <body>

    <h1>Feedback submitted</h1>    <p>Your feedback (shown below) has been sent.</p>    <p><?php echo nl2br(htmlspecialchars($feedback)); ?> </p>  </body></html>

There are many other string processing functions you may find useful. We’ll examine these in the remainder of this section.

Formatting a String for PrintingSo far, you have used the echo language construct to print strings to the browser. PHP also supports a print() construct, which does the same thing as echo, but returns a value, which is always equal to 1.

Both of these techniques print a string「as is.」You can apply some more sophisticated  formatting using the functions printf() and sprintf(). They work basically the same way, except that printf() outputs a formatted string and sprintf() returns a formatted string.

If you have previously programmed in C, you will find that these functions are conceptually similar to the C versions. Be careful, though, because the syntax is not exactly the same. If you haven’t, they take getting used to but are useful and powerful.

The prototypes for these functions are

string sprintf (string format [, mixed args...])int printf (string format [, mixed args...])

The first parameter passed to both of these functions is a format string that describes the basic shape of the output with format codes instead of variables. The other parameters are variables that will be substituted in to the format string.

For example, using echo, you can use the variables you want to print inline, like this:

echo "Total amount of order is $total.";

To get the same effect with printf(), you would use

printf ("Total amount of order is %s.", $total);

The %s in the format string is called a conversion specification. This one means「replace with a string.」In this case, it is replaced with $total interpreted as a string. If the value stored in $total was 12.4, both of these approaches would print it as 12.4.

110

Chapter 4  String Manipulation and Regular Expressions

The advantage of printf() is that you can use a more useful conversion specification to specify that $total is actually a floating-point number and that it should have two decimal places after the decimal point, as follows:

printf ("Total amount of order is %.2f", $total);

Given this formatting, and 12.4 stored in $total, this statement will print as 12.40.

You can have multiple conversion specifications in the format string. If you have n conversion specifications, you will usually have n arguments after the format string. Each conversion speci-fication will be replaced by a reformatted argument in the order they are listed. For example,

printf ("Total amount of order is %.2f (with shipping %.2f) ",           $total, $total_shipping);

Here, the first conversion specification uses the variable $total, and the second uses the  variable $total_shipping.

Each conversion specification follows the same format, which is

%[+]['padding_character][-][width][.precision]type

All conversion specifications start with a % symbol. If you actually want to print a % symbol, you need to use %%.The + sign is optional. By default, only numbers that are negative show a sign (in this case -). If you specify a sign here then positive values will be prefixed with the + sign and negative values will be prefixed with the - sign.

The padding_character is optional. It is used to pad your variable to the width you have specified. An example would be to add leading zeros to a number like a counter. The default padding character is a space. If you are specifying a space or zero, you do not need to prefix it with the apostrophe ('). For any other padding character, you need to prefix it with an apostrophe.

The - symbol is optional. It specifies that the data in the field will be left-justified rather than right-justified, which is the default.

The width specifier tells printf() how much room (in characters) to leave for the variable to be substituted in here.

The precision specifier should begin with a decimal point. It should contain the number of places after the decimal point you would like displayed.

The final part of the specification is a type code. A summary of these codes is shown in Table 4.3.

Table 4.3  Conversion Specification Type Codes

Type

Meaning

%

b

A literal % character.

Interpret as an integer and print as a binary number.

Formatting Strings

111

c

d

e

E

f

F

g

G

o

s

u

x

X

Interpret as an integer and print as a character.

Interpret as an integer and print as a decimal number.

Interpret as a double and print in scientific notation. Precision is the number of digits after the decimal point.

Same as e but a capital E will be printed.

Interpret as a float and print as a locale-aware floating-point number.

Interpret as a float and print as a non-locale-aware floating-point number.

This is the shorter output, given a choice of e or f as the specification type.

This is the shorter output, given a choice of E or F as the specification type.

Interpret as an integer and print as an octal number.

Interpret as a string and print as a string.

Interpret as an integer and print as an unsigned decimal.

Interpret as an integer and print as a hexadecimal number with lowercase letters for the digits a–f.

Interpret as an integer and print as a hexadecimal number with uppercase letters for the digits A–F.

When using the printf() function with conversion type codes, you can use argument numbering. That means that the arguments don’t need to be in the same order as the  conversion specifications. For example,

printf ("Total amount of order is %2\$.2f (with shipping %1\$.2f) ",           $total_shipping, $total);

Just add the argument position in the list directly after the % sign, followed by an escaped $ symbol; in this example, 2\$ means「replace with the second argument in the list.」This method can also be used to repeat arguments.

Two alternative versions of these functions are called vprintf() and vsprintf(). These  variants accept two parameters: the format string and an array of the arguments rather than a variable number of parameters.

Changing the Case of a StringYou can also reformat the case of a string. This capability is not particularly useful for the sample application, but we’ll look at some brief examples.

If you start with the subject string, $subject, which you are using for email, you can change its case by using several functions. The effect of these functions is summarized in Table 4.4. The first column shows the function name, the second describes its effect, the third shows how it would be applied to the string $subject, and the last column shows what value would be returned from the function.

112

Chapter 4  String Manipulation and Regular Expressions

Table 4.4  String Case Functions and Their Effects

Function

Description

Use

Value

strtoupper()

Turns string to  uppercase

strtolower()

Turns string to  lowercase

ucfirst()

ucwords()

Capitalizes first Feedback from  character of string if it’s alphabetic

Capitalizes first Feedback From  character of each word in the string that begins with an  alphabetic character

$subject

Feedback from web site

strtoupper($subject)

strtolower($subject)

FEEDBACK FROM WEB SITE

feedback from web site

ucfirst($subject) web site

ucwords($subject) Web Site

Joining and Splitting Strings with String FunctionsOften, you may want to look at parts of a string individually. For example, you might want to look at words in a sentence (say, for spellchecking) or split a domain name or email address into its component parts. PHP provides several string functions (and regular expression functions) that allow you to do this.

In this example, Bob wants any customer feedback from bigcustomer.com to go directly to him, so you can split the email address the customer typed into parts to find out whether he or she works for Bob’s big customer.

Using explode(), implode(), and join()The first function you could use for this purpose, explode(), has the following prototype:

array explode(string separator, string input [, int limit]);

This function takes a string input and splits it into pieces on a specified separator string. The pieces are returned in an array. You can limit the number of pieces with the optional limit parameter.

To get the domain name from the customer’s email address in the script, you can use the following code:

$email_array = explode('@', $email);

This call to explode() splits the customer’s email address into two parts: the username, which is stored in $email_array[0], and the domain name, which is stored in $email_array[1]. 

Joining and Splitting Strings with String Functions

113

Now you can test the domain name to determine the customer’s origin and then send the feedback to the appropriate person:

if ($email_array[1] == "bigcustomer.com") {  $toaddress = "bob@example.com";} else {  $toaddress = "feedback@example.com";}

If the domain is capitalized or mixed case, however, this approach will not work. You could avoid this problem by first converting the domain to all uppercase or all lowercase and then checking for a match, as follows:

if (strtolower($email_array[1]) == "bigcustomer.com") {  $toaddress = "bob@example.com";} else {  $toaddress = "feedback@example.com";}

You can reverse the effects of explode() by using either implode() or join(), which are  identical. For example,

$new_email = implode('@', $email_array);

This statement takes the array elements from $email_array and joins them with the string passed in the first parameter. The function call is similar to explode(), but the effect is the opposite.

Using strtok()Unlike explode(), which breaks a string into all its pieces at one time, strtok() gets pieces (called tokens) from a string one at a time. strtok() is a useful alternative to using explode() for processing words from a string one at a time.

The prototype for strtok() is

string strtok(string input, string separator);

The separator can be either a character or a string of characters, but the input string is split on each of the characters in the separator string rather than on the whole separator string (as explode does).

Calling strtok() is not quite as simple as it seems in the prototype. To get the first token from a string, you call strtok() with the string you want tokenized and a separator. To get the subsequent tokens from the string, you just pass a single parameter—the separator. The  function keeps its own internal pointer to its place in the string. If you want to reset the pointer, you can pass the string into it again.

114

Chapter 4  String Manipulation and Regular Expressions

strtok() is typically used as follows:

$token = strtok($feedback, " ");while ($token != "") {  echo $token."<br />";  $token = strtok(" ");

}

As usual, it’s a good idea to check that the customer actually typed some feedback in the form, using, for example, the empty() function. We have omitted these checks for brevity.

The preceding code prints each token from the customer’s feedback on a separate line and loops until there are no more tokens. 

Using substr()The substr() function enables you to access a substring between given start and end points of a string. It’s not appropriate for the example used here but can be useful when you need to get at parts of fixed format strings.

The substr() function has the following prototype:

string substr(string string, int start[, int length] );

This function returns a substring copied from within string.

The following examples use this test string:

$test = 'Your customer service is excellent';

If you call it with a positive number for start (only), you will get the string from the start position to the end of the string. For example,

substr($test, 1);

returns our customer service is excellent. Note that the string position starts from 0, as with arrays.

If you call substr() with a negative start (only), you will get the string from the end of the string minus start characters to the end of the string. For example,

substr($test, -9);

returns excellent.

The length parameter can be used to specify either a number of characters to return (if it is positive) or the end character of the return sequence (if it is negative). For example,

substr($test, 0, 4);

returns the first four characters of the string—namely, Your. The code

substr($test, 5, -13);

returns the characters between the fourth character and the thirteenth-to-last character—that is, customer service. The first character is location 0. So location 5 is the sixth character.

Comparing Strings

115

Comparing StringsSo far, we’ve just shown you how to use the operator == to compare two strings for  equality. You can do some slightly more sophisticated comparisons using PHP. We’ve divided these comparisons into two categories for you: partial matches and others. We deal with the others first and then get into partial matching, which we need to further develop the Smart Form example.

Performing String Ordering: strcmp(), strcasecmp(), and strnatcmp()The strcmp(), strcasecmp(), and strnatcmp() functions can be used to order strings. This capability is useful when you are sorting data.

The prototype for strcmp() is

int strcmp(string str1, string str2);

The function expects to receive two strings, which it compares. If they are equal, it will return 0. If str1 comes after (or is greater than) str2 in lexicographic order, strcmp() will return a number greater than zero. If str1 is less than str2, strcmp() will return a number less than zero. This function is case sensitive.

Note that this is quite unintuitive in some ways, because testing for true/false as the return value will not give the results you expect. If the strings match, the function returns 0, and if you write code like this:

if(strcmp($a,$b)) {   …}

you will find that the if clause will be executed when the strings do not match.

The function strcasecmp() is identical except that it is not case sensitive.

The function strnatcmp() and its non-case sensitive twin, strnatcasecmp() compare strings according to a「natural ordering,」which is more the way a human would do it. For example, strcmp() would order the string 2 as greater than the string 12 because it is  lexicographically greater. strnatcmp() would order them the other way around. You can read more about natural ordering at http://www.naturalordersort.org/.

Testing String Length with strlen()You can check the length of a string by using the strlen() function. If you pass it a string, this function will return its length. For example, the result of this code is 5: 

echo strlen("hello");

116

Chapter 4  String Manipulation and Regular Expressions

You can use the strlen() function for validating input data. Consider the email address on the sample form, stored in $email. One basic way of validating an email address stored in $email is to check its length. By our reasoning, the minimum length of an email address is six characters—for example, a@a.to if you have a country code with no second-level domains, a one-letter server name, and a one-letter email address. Therefore, an error could be produced if the address is not at least this length:

if (strlen($email) < 6){    echo 'That email address is not valid';   exit;  // force termination of execution } 

Clearly, this approach is a very simplistic way of validating this information. We look at better ways in the next section.

Matching and Replacing Substrings with String FunctionsChecking whether a particular substring is present in a larger string is a common operation. This partial matching is usually more useful than testing for complete equality in strings.

In the Smart Form example, you want to look for certain key phrases in the customer  feedback and send the mail to the appropriate department. If you want to send emails discussing Bob’s shops to the retail manager, for example, you want to know whether the word shop or  derivatives thereof appear in the message.

Given the functions you have already looked at, you could use explode() or strtok() to retrieve the individual words in the message and then compare them using the == operator or strcmp().

You could also do the same thing, however, with a single function call to one of the  string-matching or regular expression-matching functions. They search for a pattern inside a string. Next, we look at each of these sets of functions.

Finding Strings in Strings: strstr(), strchr(), strrchr(), and stristr()To find a string within another string, you can use any of the functions strstr(), strchr(), strrchr(), or stristr().

The function strstr(), which is the most generic, can be used to find a string or  character match within a longer string. In PHP, the strchr() function is the same as strstr(), although its name implies that it is used to find a character in a string, similar to the C version of this function. In PHP, either of these functions can be used to find a string inside a string, including finding a string containing only a single character.

Matching and Replacing Substrings with String Functions 

117

The prototype for strstr() is as follows:

string strstr(string haystack, string needle[, bool before_needle=false]);

You pass the function a haystack to be searched and a needle to be found. If an exact match of the needle is found, the function returns the haystack from the needle onward;  otherwise, it returns false. If the needle occurs more than once, the returned string will start from the first occurrence of needle. If the before_needle parameter is set to true, the function will return the portion of the string prior to the needle.

For example, in the Smart Form application, you can decide where to send the email as follows:

$toaddress = 'feedback@example.com';  // the default value   // Change the $toaddress if the criteria are met  if (strstr($feedback, 'shop')) {      $toaddress = 'retail@example.com';        } else if (strstr($feedback, 'delivery')) {      $toaddress = 'fulfillment@example.com';  } else if (strstr($feedback, 'bill')) {   $toaddress = 'accounts@example.com';  }

This code checks for certain keywords in the feedback and sends the mail to the appropriate person. If, for example, the customer feedback reads「I still haven’t received delivery of my last order,」the string「delivery」will be detected and the feedback will be sent to fulfillment@example.com.

There are two variants on strstr(). The first variant is stristr(), which is nearly identical but is not case sensitive. This variation is useful for this application because the customer might type "delivery", "Delivery", "DELIVERY", or some other mixed-case variation.

The second variant is strrchr(), which is similar, but returns the haystack from the last occurrence of the needle onward. It also searches for only a single character (the first character of the string passed in needle), which is something of a gotcha.

Finding the Position of a Substring: strpos() and strrpos()The functions strpos() and strrpos() operate in a similar fashion to strstr(), except, instead of returning a substring, they return the numerical position of a needle within a haystack. The PHP manual recommends using strpos() instead of strstr() to check for the presence of a string within a string because it runs faster.

The strpos() function has the following prototype:

int strpos(string haystack, string needle[, int offset=0]);

The integer returned represents the position of the first occurrence of the needle within the haystack. The first character is in position 0 as usual.

118

Chapter 4  String Manipulation and Regular Expressions

For example, the following code echoes the value 4 to the browser:

$test = "Hello world";echo strpos($test, "o");

This code passes in only a single character as the needle, but it can be a string of any length.

The optional offset parameter specifies a point within the haystack to start searching. For example,

echo strpos($test, "o", 5);

This code echoes the value 7 to the browser because PHP has started looking for the character o at position 5 and therefore does not see the one at position 4.

The strrpos() function is almost identical but returns the position of the last occurrence of the needle in the haystack. 

In any of these cases, if the needle is not in the string, strpos() or strrpos() will return false. This result can be problematic because false in a weakly typed language such as PHP is in many contexts equivalent to 0—that is, the first location in a string.

You can avoid this problem by using the === operator to test return values:

$result = strpos($test, "H");    if ($result === false) {           echo "Not found";             } else {                          echo "Found at position ".$result;  } 

Replacing Substrings: str_replace() and substr_replace()Find-and-replace functionality can be extremely useful with strings. You can use find-and-replace for personalizing documents generated by PHP—for example, by replacing <name> with a person’s name and <address> with his or her address. You can also use it for censoring particular terms, such as in a discussion forum application, or even in the Smart Form applica-tion. Again, you can use string functions or regular expression functions for this purpose.

The most commonly used string function for replacement is str_replace(), as we discussed earlier in this chapter. It has the following prototype:

mixed str_replace(mixed needle, mixed new_needle, mixed haystack[, int &count]));

This function replaces all the instances of needle in haystack with new_needle and returns the new version of haystack. The optional fourth parameter, count, contains the number of replacements made. 

Introducing Regular Expressions

119

NoteYou can pass all parameters as arrays, and the str_replace() function works remarkably  intelligently. You can pass an array of words to be replaced, an array of words to replace them with (respectively), and an array of strings to apply these rules to. The function then returns an array of revised strings.

For example, because people can use the Smart Form to complain, they might use some  colorful words. As a programmer, you can easily prevent Bob’s various departments from being abused in that way if you have an array $offcolor that contains a number of offensive words. Here is an example using str_replace() with an array:

$feedback = str_replace($offcolor, '%!@*', $feedback);

The function substr_replace() finds and replaces a particular substring of a string based on its position. It has the following prototype:

string substr_replace(mixed string, mixed replacement,                       mixed start[, mixed length] );

This function replaces part of the string string with the string replacement. Which part is replaced depends on the values of the start and optional length parameters.

The start value represents an offset into the string where replacement should begin. If it is zero or positive, it is an offset from the beginning of the string; if it is negative, it is an offset from the end of the string. For example, this line of code replaces the last character in $test with「X」:

$test = substr_replace($test, 'X', -1);

The length value is optional and represents the point at which PHP will stop replacing. If you don’t supply this value, the string will be replaced from start to the end of the string.

If length is zero, the replacement string will actually be inserted into the string without  overwriting the existing string. A positive length represents the number of characters that you want replaced with the new string; a negative length represents the point at which you would like to stop replacing characters, counted from the end of the string.

Similar to the str_replace() function, you can also use substr_replace() by passing in a set of arrays.

Introducing Regular ExpressionsPHP has historically supported two styles of regular expression syntax: POSIX and Perl. Both types are compiled into PHP by default, but since PHP version 5.3 the POSIX style has been deprecated.

So far, all the pattern matching you’ve done has used the string functions. You have been limited to exact matches or to exact substring matches. If you want to do more complex pattern matching, you should use regular expressions. Regular expressions are difficult to grasp at first but can be extremely useful.

120

Chapter 4  String Manipulation and Regular Expressions

The BasicsA regular expression is a way of describing a pattern in a piece of text. The exact (or literal) matches you’ve seen so far are a form of regular expression. For example, earlier you searched for regular expression terms such as "shop" and "delivery".

Matching regular expressions in PHP is more like a strstr() match than an equal  comparison because you are matching a string somewhere within another string. (It can be anywhere within that string unless you specify otherwise.) For example, the string "shop" matches the regular expression "shop". It also matches the regular expressions "h", "ho", and so on.

You can use special characters to indicate a meta-meaning in addition to matching characters exactly. For example, with special characters you can indicate that a pattern must occur at the start or end of a string, that part of a pattern can be repeated, or that characters in a pattern must be of a particular type. You can also match on literal occurrences of special characters. 

DelimitersWith PCRE regular expressions, each expression must be contained within a pair of delimiters. You may choose any character that is not a letter, a number, a backslash, or whitespace. The delimiter at the start and end of the string must match.

The most commonly used delimiter is the forward slash (/). So, for example, if we wanted to write a regular expression to match the word「shop,」we could write

/shop/

If you need to match a literal / inside the regular expression, you will need to escape it with the \ (backslash) character. For example,

/http:\/\//

If your pattern contains many instances of your chosen delimiter, you might consider choosing a different delimiter. In the previous example, we might choose the # symbol instead, giving us the following expression:

#http://#

You may sometimes wish to add a pattern modifier after the closing delimiter. For example,

/shop/i

would match the word「shop」in a case-insensitive fashion. This is by far the most commonly used modifier. You may find others in the PHP manual.

Character Classes and TypesUsing character sets immediately gives regular expressions more power than exact matching expressions. Character sets can be used to match any character of a particular type; they’re really a kind of wildcard.

Introducing Regular Expressions

121

First, you can use the . character as a wildcard for any other single character except a newline (\n). For example, the regular expression

/.at/

matches the strings "cat", "sat", and "mat", among others. This kind of wildcard matching is often used for filename matching in operating systems.

With regular expressions, however, you can be more specific about the type of character you would like to match and can actually specify a set that a character must belong to. In the preceding example, the regular expression matches "cat" and "mat" but also matches "#at". If you want to limit this to a character between a and z, you can specify it as follows:

/[a-z]at/

Anything enclosed in the square brackets ([ and ]) is a character class—a set of characters to which a matched character must belong. Note that the expression in the square brackets matches only a single character.

You can list a set; for example,

/[aeiou]/

means any vowel.

You can also describe a range, as you just did using the special hyphen character, or a set of ranges, as follows:

/[a-zA-Z]/

This set of ranges stands for any alphabetic character in upper- or lowercase.

You can also use sets to specify that a character cannot be a member of a set. For example,

/[^a-z]/

matches any character that is not between a and z. The caret symbol (^, sometimes called circumflex) means not when it is placed inside the square brackets. It has another meaning when used outside square brackets, which we look at shortly.

In addition to listing out sets and ranges, you can use a number of predefined character classes in a regular expression. These classes are shown in Table 4.5.

Table 4.5  Character Classes for Use in PCRE-Style Regular Expressions

Class

[[:alnum:]]

[[:alpha:]]

[[:ascii:]]

[[:lower:]]

[[:upper:]]

Matches

Alphanumeric characters

Alphabetic characters

ASCII characters

Lowercase letters

Uppercase letters

122

Chapter 4  String Manipulation and Regular Expressions

Class

[[:word:]]

[[:digit:]]

Matches

「Word」characters (letters, digits, or the underscore)

Decimal digits

[[:xdigit:]]

Hexadecimal digits

[[:punct:]]

[[:blank:]]

[[:space:]]

[[:cntrl:]]

[[:print:]]

[[:graph:]]

Punctuation

Tabs and spaces

Whitespace characters

Control characters

All printable characters

All printable characters except for space

Note that the enclosing square brackets delimit the class, and the inner square brackets are part of the class name. For example,

/[[:alpha]1-5]/

describes a class that may contain an alphabetical character, or any of the digits from 1 to 5.

RepetitionOften, you may want to specify that there might be multiple occurrences of a particular string or class of character. You can represent this using three special characters in your regular expression. The ∗ symbol means that the pattern can be repeated zero or more times, and the + symbol means that the pattern can be repeated one or more times. The ? symbol means that the pattern should appear either once or not at all. The symbol should appear directly after the part of the expression that it applies to. For example,

/[[:alnum:]]+/

means「at least one alphanumeric character.」

SubexpressionsBeing able to split an expression into subexpressions is often useful so that you can, for example, represent「at least one of these strings followed by exactly one of those.」You can split expressions using parentheses, exactly the same way as you would in an arithmetic  expression. For example,

/(very )*large/

matches "large", "very large", "very very large", and so on.

Introducing Regular Expressions

123

Counted SubexpressionsYou can specify how many times something can be repeated by using a numerical  expression in curly braces ({}). You can show an exact number of repetitions ({3} means exactly three  repetitions), a range of repetitions ({2,4} means from two to four repetitions), or an  open-ended range of repetitions ({2,} means at least two repetitions).

For example,

/(very ){1,3}/

matches "very ", "very very ", and "very very very ".

Anchoring to the Beginning or End of a StringAs we've discussed, the pattern /[a-z]/ will match any string containing a lowercase  alphabetic character. It does not matter whether the string is one character long or contains a single matching character in a longer string.

You also can specify whether a particular subexpression should appear at the start, the end, or both. This capability is useful when you want to make sure that only your search term and nothing else appears in the string.

The caret symbol (^) is used at the start of a regular expression to show that it must appear at the beginning of a searched string, and $ is used at the end of a regular expression to show that it must appear at the end.

For example, the following matches bob at the start of a string:

/^bob/

This pattern matches com at the end of a string:

/com$/

Finally, this pattern matches a string containing only a single character between a and z:

/^[a-z]$/

BranchingYou can represent a choice in a regular expression with a vertical pipe. For example, if you want to match com, edu, or net, you can use the following expression:

/com|edu|net/

Matching Literal Special CharactersIf you want to match one of the special characters mentioned in the preceding sections, such as ., {, or $, you must put a backslash (\) in front of it. If you want to represent a backslash, you must replace it with two backslashes (\\).

124

Chapter 4  String Manipulation and Regular Expressions

Be careful to put your regular expression patterns in single-quoted strings in PHP. Using regular expressions in double-quoted PHP strings adds unnecessary complications. PHP also uses the backslash to escape special characters—such as a backslash. If you want to match a backslash in your pattern, you need to use two to indicate that it is a literal backslash, not an escape code.

Similarly, if you want a literal backslash in a double-quoted PHP string, you need to use two for the same reason. The somewhat confusing, cumulative result of these rules is that a double-quoted PHP string that represents a regular expression containing a literal backslash needs four backslashes. The PHP interpreter will parse the four backslashes as two, then the regular expression interpreter will parse the two as one.

The dollar sign is also a special character in double-quoted PHP strings and regular expressions. To get a literal $ matched in a pattern, you would need "\\\$". Because this string is in double quotation marks, PHP will parse it as \$, which the regular expression interpreter can then match against a dollar sign.

Reviewing Meta CharactersA summary of all the special characters—called meta characters—is shown in Tables 4.6 and 4.7. Table 4.6 shows the meaning of special characters outside square brackets, and Table 4.7 shows their meaning when used inside square brackets.

Table 4.6 

 Summary of Meta Characters Used in PCRE Regular Expressions Outside Square Brackets

Character

\

^

$

.

|

(

)

*

+

{

}

?

Meaning

Escape character

Match at start of string

Match at end of string

Match any character except newline (\n)

Start of alternative branch (read as OR)

Start subpattern

End subpattern

Repeat zero or more times

Repeat one or more times

Start min/max quantifier

End min/max quantifier

Mark a subpattern as optional

Introducing Regular Expressions

125

Table 4.7 

 Summary of Meta Characters Used in PCRE Regular Expressions Inside Square Brackets

Character

\

^

-

Meaning

Escape character

NOT, only if used in initial position

Used to specify character ranges

Escape SequencesEscape sequences are parts of a pattern that begin with the backslash character (\). These fall into several categories.

First, backslash may be used to escape one of the meta characters, as discussed in the previous two sections.

Second, backslash is used as the start of a set of character sequences used to represent non-printing characters. We’ve already seen several of these in other contexts, such as \n (newline), \r (carriage return), and \t (tab). A couple of other useful ones are \cx to represent Control-x (where x is any character) and \e to represent escape.

Third, backslash is used as the start of a set of generic character types. The possible types are listed in Table 4.8.

Table 4.8  Generic Character Types in PCRE Regular Expressions

Character Type

\d

\D

\h

\H

\s

\S

\v

\V

\w

\W

Meaning

A decimal digit

Anything but a decimal digit

Horizontal whitespace

Anything but horizontal whitespace

Whitespace

Anything but whitespace

Vertical whitespace

Anything but whitespace

「Word」characters 

Anything but "word" characters

126

Chapter 4  String Manipulation and Regular Expressions

A「word」character is generally speaking any letter, digit, or underscore. However, if you are using locale-specific matching, this will include letters in the appropriate locales; for example, accented letters.

There are two other uses of the backslash. One is to begin a back reference, and the other is to begin an assertion. We will cover these uses in the next two sections.

BackreferencesBackreferences are traditionally where non-Perl programmers throw up their hands. However, they are not actually that complex.

A backreference in a pattern is indicated by a backslash followed by a digit (and possibly more than one, depending on the context). It is used for matching the same subexpression appearing in more than one place in a string, without explicitly specifying the value.

For example, take the following pattern:

/^([a-z]+) \1 black sheep/

The \1 here is a backreference to the previously matched subexpression—that is, ([a-z]+), which is one or more alphabetical characters.

Given this pattern, the string

baa baa black sheep

will match, but the string

blah baa black sheep

will not. This is because the backreference effectively says「find the term that matched the previous subexpression, and match the exact same thing again」.

If multiple subexpressions have previously been encountered, they are effectively numbered in order starting at 1, if you wish to use them in backreferences.

AssertionsAn assertion is used to test some characters in a string being matched, without itself matching any characters. This may be a little hard to understand without some examples. Table 4.9 lists possible assertions that begin with a backslash.

Table 4.9  Backslashed Assertions in PCRE Regular Expressions

Assertion

\b

\B

\A

Meaning

Word boundary

Not a word boundary

Start of subject

Introducing Regular Expressions

127

\z 

\Z 

\G 

End of subject

End of subject or newline at end

First matching position in subject

Word boundaries are places where word characters (defined in the previous section) and non-word characters are placed next to one another.

The start and end assertions are similar to the caret (^) and dollar ($) meta characters, except that some configuration options change the behavior of ^ and $, but \A, \z, and \Z are unaffected.

The first matching position assertion (\G) is similar to the start assertion but is used when you begin matching at an offset, which is possible with some of the regular expression functions. For example, if you have an offset of 5, and the first thing you find at position 5 is a match, the \G assertion will be satisfied, but \A may not be, depending on what is found at position 1.

Putting It All Together for the Smart FormThere are at least two possible uses of regular expressions in the Smart Form application. The first use is to detect particular terms in the customer feedback. You can be slightly smarter about this by using regular expressions. Using a string function, you would have to perform three different searches if you wanted to match on "shop", "customer service", or "retail". With a regular expression, you can match all three:

/shop|customer service|retail/

The second use is to validate customer email addresses in the application by encoding the standardized format of an email address in a regular expression. The format includes some alphanumeric or punctuation characters, followed by an @ symbol, followed by a string of alphanumeric and hyphen characters, followed by a dot, followed by more alphanumeric and hyphen characters and possibly more dots, up until the end of the string, which encodes as follows:

/^[a-zA-Z0-9_\-.]+@[a-zA-Z0-9\-]+\.[a-zA-Z0-9\-.]+$/

The subexpression ^[a-zA-Z0-9_\-.]+ means「start the string with at least one letter, number, underscore, hyphen, or dot, or some combination of those.」Note that when a dot is used at the beginning or end of a character class, it loses its special wildcard meaning and becomes just a literal dot.

The @ symbol matches a literal @.

The subexpression [a-zA-Z0-9\-]+ matches the first part of the hostname including  alphanumeric characters and hyphens. Note that you slash out the hyphen because it’s a special character inside square brackets.

The \. combination matches a literal dot (.). We are using a dot outside character classes, so we need to escape it to match only a literal dot.

128

Chapter 4  String Manipulation and Regular Expressions

The subexpression [a-zA-Z0-9\-\.]+$ matches the rest of a domain name, including letters, numbers, hyphens, and more dots if required, up until the end of the string.

A bit of analysis shows that you can easily produce invalid email addresses that will still match this regular expression. It is almost impossible to catch them all, but this will improve the situation a little. You can refine this expression in many ways. You can, for example, list valid top-level domains (TLDs). Be careful when making things more restrictive, though, because a validation function that rejects 1% of valid data is far more annoying than one that allows through 10% of invalid data.

Now that you have read about regular expressions, you’re ready to look at the PHP functions that use them.

Finding Substrings with Regular ExpressionsFinding substrings is the main application of the regular expressions you just developed. 

There are a number of PCRE regular expression functions in PHP. The simplest, preg_match(), is the one we will use in this example. It has the following prototype:

int preg_match(string pattern, string subject[, array matches[, int flags=0[, int offset=0]]])

This function searches the subject string, looking for matches to the regular expression in pattern. If a match is found for the expression, the full match will be stored in $matches[0], and each of the subsequent array elements will store a match for each matched subexpression.

The only possible value to pass to flags is the constant PREG_OFFSET_CAPTURE. If this is set, the matches array will take a different form. Each element in the array will consist of an array of matched subexpressions, and the offset within the subject string where they were found.

The offset parameter can be used to start searching the subject string from the specified offset.

The preg_match() function returns 1 if a match was found, 0 if a match was not found, and FALSE if an error occurred. This means you need to use identity (===) to test what is returned, to avoid confusion between 0 and FALSE.

You can adapt the Smart Form example to use regular expressions by adding the following code to the order processing script:

if (preg_match('/^[a-zA-Z0-9_\-\.]+@[a-zA-Z0-9\-]+\.[a-zA-Z0-9\-\.]+$/',                        $email) === 0) {                                                    echo "<p>That is not a valid email address.</p>".                                    "<p>Please return to the previous page and try again.</p>";                exit;                                                                       }                                                                               $toaddress = 'feedback@example.com';  // the default value                      if (preg_match('/shop|customer service|retail/', $feedback)) {                      $toaddress = 'retail@example.com';                                          

Splitting Strings with Regular Expressions

129

} else if (preg_match('/deliver|fulfill/', $feedback)) {                            $toaddress = 'fulfillment@example.com';                                     } else if (preg_match('/bill|account/', $feedback)) {                               $toaddress = 'accounts@example.com';                                        }                                                                               if (preg_match('/bigcustomer\.com/', $email)) {                                     $toaddress = 'bob@example.com';                                             }       

Replacing Substrings with Regular ExpressionsYou can also use regular expressions to find and replace substrings in the same way as you used str_replace(), using the function preg_replace(). This function has the following prototype:

mixed preg_replace(string pattern, string replacement, string subject[, int limit=-1[, int &count]])

This function searches for the regular expression pattern in the subject string and replaces it with the string replacement.

The limit parameter specifies the maximum number of replacements to make. The default is -1, meaning no limit.

The count parameter, if supplied, will be filled with the total number of replacements made.

Splitting Strings with Regular ExpressionsAnother useful regular expression function is preg_split(), which has the following prototype:

array preg_split(string pattern, string subject[, int limit=-1[, int flags=0]]);

This function splits the string subject into substrings on the regular expression pattern and returns the substrings in an array. The limit parameter limits the number of items that can go into the array. (The default value, −1, means no limit.)

The flags parameter accepts the following constants, which can be combined via bitwise OR (|):

 ■ PREG_SPLIT_NO_EMPTY, means that only non-empty pieces will be returned.

 ■ PREG_SPLIT_DELIM_CAPTURE means that the delimiters will be returned as pieces.

 ■ PREG_SPLIT_OFFSET_CAPTURE means that the location of each piece in the original 

string will be returned in the same way that the preg_match() function does it.

130

Chapter 4  String Manipulation and Regular Expressions

This function can be useful for splitting up email addresses, domain names, or dates. For example,

$address = 'username@example.com';                                              $arr = preg_split ('/\.|@/', $address);                                         while (list($key, $value) = each ($arr)) {                                        echo '<br />'.$value;                                                         }

This example splits the =email address into its three components and prints each on a separate line:

usernameexamplecom

NoteIn general, the regular expression functions run less efficiently than the string functions with similar functionality. If your task is simple enough to use a string expression, do so. This may not be true for tasks that can be performed with a single regular expression but multiple string functions.

Further ReadingPHP has many string functions. We covered the more useful ones in this chapter, but if you have a particular need (such as translating characters into Cyrillic), check the PHP manual online to see whether PHP has the function for you.

The amount of material available on regular expressions is enormous. You can start with the man page for regexp if you are using Unix.

Regular expressions take a while to sink in; the more examples you look at and run, the more confident you will be using them.

NextIn the next chapter, we discuss several ways you can use PHP to save programming time and effort and prevent redundancy by reusing pre-existing code.

