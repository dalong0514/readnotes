18Using Network and Protocol Functions

In this chapter, we look at the network-oriented functions in PHP that enable your scripts to interact with the rest of the Internet. A world of resources is available out there, and a wide variety of protocols is available for using them.

Key topics covered in this chapter include

 ■ Examining available protocols

 ■ Sending and reading email

 ■ Using data from other websites

 ■ Using network lookup functions

 ■ Using FTP

Examining Available ProtocolsProtocols are the rules of communication for a given situation. For example, you know the protocol when meeting another person: You say hello, shake hands, communicate for a while, and then say goodbye. Different situations require different protocols. Also, people from other cultures may expect different protocols, which may make interaction difficult. Computer networking protocols are similar.

Like human protocols, different computer protocols are used for different situations and applications. For instance, you use the Hypertext Transfer Protocol (HTTP) when you request and receive web pages—your computer requests a document (such as an HTML or PHP file) from a web server, and that server responds by sending the document to your computer. You probably also have used the File Transfer Protocol (FTP) for transferring files between machines on a network. Many others are available.

404

Chapter 18  Using Network and Protocol Functions 

Most protocols and other Internet standards are described in documents called Requests for Comments (RFCs). These protocols are defined by the Internet Engineering Task Force (IETF). The RFCs are widely available on the Internet. The base source is the RFC Editor at http://www.rfc-editor.org/.

If you have problems when working with a given protocol, the documents that define them are the authoritative sources and are often useful for troubleshooting your code. They are, however, very detailed and often run to hundreds of pages.

Some examples of well-known RFCs are RFC2616, which describes the HTTP/1.1 protocol, and RFC822, which describes the format of Internet email messages.

In this chapter, we look at aspects of PHP that use some of these protocols. Specifically, we discuss sending mail with SMTP, reading mail with POP3 and IMAP4, connecting to other web servers via HTTP, and transferring files with FTP.

Sending and Reading EmailThe main way to send mail in PHP is to use the simple mail() function. We discussed the use of this function in Chapter 4,「String Manipulation and Regular Expressions,」so we won’t visit it again here. This function uses the Simple Mail Transfer Protocol (SMTP) to send mail.

You can use a variety of freely available classes to add to the functionality of mail(). SMTP is only for sending mail. The Internet Message Access Protocol (IMAP4), described in RFC2060, and Post Office Protocol (POP3), described in RFC1939 or STD0053, are used to read mail from a mail server. These protocols cannot send mail.

IMAP4 is used to read and manipulate mail messages stored on a server and is more  sophisticated than POP3, which is generally used simply to download mail messages to a client and delete them from the server.

PHP includes over thirty functions that can be used with IMAP4, all of which are documented at http://php.net/manual/en/book.imap.php. 

Using Data from Other WebsitesOne of the great things you can do with the Web is use, modify, and embed existing services and information into your own pages. PHP makes this very easy as long as there is a consistently formed URL to access, even if it is not an official published API. Let’s look at an example to illustrate this use of accessing a URL and retrieving content from it for later use.

Imagine that the company you work for wants the company’s stock quote displayed on its home page. This information is available on some stock exchange site somewhere, but how do you get at it?

Using Data from Other Websites

405

Start by finding an original source URL for the information. When you know the URL, every time someone goes to your home page, you can open a connection to that URL, retrieve the page, and pull out the information you require.

As an example, we put together a script that retrieves and reformats a stock quote from the Yahoo! Finance website, which consistently provides a「Download Data」link on every stock quote page, which follows the same general URL format for all stock symbols. For the purpose of the example, we retrieved the current stock price of Google. (The information you want to include on your page might differ, but the principles are the same.)

Our example script consumes the data provided by another site and displays it on our site. The script is shown in Listing 18.1.

Listing 18.1 

 lookup.php—Script Retrieves a Stock Quote from the NASDAQ for the Stock with the Ticker Symbol Listed in $symbol

<!DOCTYPE html><html><head>   <title>Stock Quote From NASDAQ</title></head><body>

<?php//choose stock to look at$symbol = 'GOOG';echo '<h1>Stock Quote for '.$symbol.'</h1>';

$url = 'http://download.finance.yahoo.com/d/quotes.csv' .    '?s='.$symbol.'&e=.csv&f=sl1d1t1c1ohgv';

if (!($contents = file_get_contents($url))) {    die('Failed to open '.$url);}

// extract relevant datalist($symbol, $quote, $date, $time) = explode(',', $contents);$date = trim($date, '"');$time = trim($time, '"');

echo '<p>'.$symbol.' was last sold at: $'.$quote.'</p>';echo '<p>Quote current as of '.$date.' at '.$time.'</p>';

// acknowledge sourceecho '<p>This information retrieved from <br /><a href="'.$url.'">'.$url.'</a>.</p>';

?></body></html>

406

Chapter 18  Using Network and Protocol Functions 

The output from one sample run of Listing 18.1 is shown in Figure 18.1.

Figure 18.1  The lookup.php script uses a regular expression to pull out the stock quote from information retrieved from the stock exchange

The script itself is reasonably straightforward; in fact, it doesn’t use any functions you haven’t seen before, just new applications of those functions.

You might recall that when we discussed reading from files in Chapter 2,「Storing and Retrieving Data,」we mentioned that you could use the file functions to read from an URL. That’s what we have done in this case. The call to file_get_contents():

if (!($contents = file_get_contents($url))) {

returns the entire text of the file located at that URL, stored in $contents.

The file functions can do a lot in PHP. The example here simply loads a file via HTTP, but you could interact with other servers via HTTPS, FTP, or other protocols in exactly the same way. For some tasks, you might need to take a more specialized approach. For example, some FTP functionality is available in the specific FTP functions, and not available via fopen() and other file functions. Additionally, for some HTTP or HTTPS tasks, you may need to use the cURL library. With cURL, you can log in to a website and mimic a user’s progress through a few pages.

Using Data from Other Websites

407

Returning to the discussion of the script, now that you  obtained the text of the file from file_get_contents(), you can then use  the list() function to find the part of the content that you want:

list($symbol, $quote, $date, $time) = explode(',', $contents);$date = trim($date, '"');$time = trim($time, '"');

You can use the list() function to place comma-delimited content into specific variables precisely because the file you have accessed is consistently formatted. That is to say, when opening the file at the URL specified in the script, you assume it will always contain the stock symbol, the last stock purchase price, and the date and time of that purchase in that specific order. If the file structure changes, your script will also have to change, so always pay careful attention to the resources you are consuming via automated scripts, especially if they are not part of a well-documented and maintained public API.

Once you have the values in the variables indicated above, you can simply print them to the screen.

echo '<p>'.$symbol.' was last sold at: $'.$quote.'</p>';echo '<p>Quote current as of '.$date.' at '.$time.'</p>';

That’s it!

You can use this content-retrieval approach for a variety of purposes. Another good example is retrieving local weather information and embedding it in your page.

The best use of this approach is to combine information from different sources to add some value to the user. You can see one good example of this approach in Philip Greenspun’s infamous script that produces the Bill Gates Wealth Clock at http://philip.greenspun.com/WealthClock.

This page takes information from two sources. It obtains the current US population from the US Census Bureau’s site. It also looks up the current value of a Microsoft share and combines these two pieces of information, adds a healthy dose of the author’s opinion, and produces new information—an estimate of Bill Gates’ current worth.

One side note: If you’re using an outside information source such as this for a commercial purpose, it’s a good idea to check with the source or take legal advice first. You might need to consider intellectual property issues in some cases.

If you’re building a script like this lookup script, you might want to pass through some data. For example, if you’re connecting to an outside URL, you might like to pass some parameters that would normally be typed in by the user. If you’re doing this, it’s a good idea to use the urlencode() function. This function takes a string and converts it to the proper format for an URL; for example, transforming spaces into plus signs. You can call it like this:

$encodedparameter = urlencode($parameter);

408

Chapter 18  Using Network and Protocol Functions 

One problem with this overall approach is that the site you’re getting the information from may change its data format, which will stop your script from working. As mentioned above, always pay close attention to the data sources you might rely on in your scripts.

Using Network Lookup FunctionsPHP offers a set of「lookup」functions that can be used to check information about hostnames, IP addresses, and mail exchanges. For example, if you were setting up a directory site such as DMOZ (http://www.dmoz.org), when new URLs were submitted you might like to automatically check that the host of an URL and the contact information for that site are valid. This way, you can save some overhead further down the track when a reviewer comes to look at a site and finds that it doesn’t exist or that the email address isn’t valid.

Listing 18.2 shows the HTML for a submission form for a directory like this.

Listing 18.2  directory_submit.html—HTML for the Submission Form<!DOCTYPE html><html><head>   <title>Submit Site</title></head><body>   <h1>Submit Site</h1>   <form action="directory_submit.php" method="post">   <label for="url">Enter the URL:</label>   <input type="text" name="url" id="url" size="30" value="http://" /><br />   <label for="email">Enter the Email Contact:</label>   <input type="text" name="email" id="email" size="30" /><br />   <input type="submit" value="Submit Site"/>   </form></body></html>

This is a simple form; the rendered version is shown in Figure 18.2.

Using Network Lookup Functions

409

Figure 18.2  Directory submissions typically require your URL and some contact details so  directory administrators can notify you when your site is added to the directory

When the submit button is clicked, you want to first check that the URL is hosted on a real machine, and, second, that the host part of the email address is also on a real machine. We wrote a script to check these things, and the output is shown in Figure 18.3.

Figure 18.3  This version of the script displays the results of checking the hostnames for the URL and email address; a production version might not display these results, but it is interesting to see the information returned from the checks

The script that performs these checks uses two functions from the PHP network functions suite: gethostbyname() and getmxrr(). The full script is shown in Listing 18.3.

410

Chapter 18  Using Network and Protocol Functions 

Listing 18.3  directory_submit.php—Script to Verify URL and Email Address<!DOCTYPE html><html><head>   <title>Site Submission Results</title></head><body>   <h1>Site Submission Results</h1>

<?php

// Extract form fields$url = $_POST['url'];$email = $_POST['email'];

// Check the URL$url = parse_url($url);$host = $url['host'];

if (!($ip = gethostbyname($host))){  echo 'Host for URL does not have valid IP address.';  exit;} 

echo 'Host ('.$host.') is at IP '.$ip.'<br/>';

// Check the email address$email = explode('@', $email);$emailhost = $email[1];

if (!getmxrr($emailhost, $mxhostsarr)){  echo 'Email address is not at valid host.';  exit;}

echo 'Email is delivered via: <br/><ul>';

foreach ($mxhostsarr as $mx) {  echo '<li>'.$mx.'</li>';}echo '</ul>';

Using Network Lookup Functions

411

// If reached here, all okecho '<p>All submitted details are ok.</p>';echo '<p>Thank you for submitting your site.       It will be visited by one of our staff members soon.</p>';// In real case, add to db of waiting sites...?></body></html>

Let’s go through the interesting parts of this script.

First, you take the URL from the $_POST superglobal and apply the parse_url() function to it. This function returns an associative array of the different parts of an URL. The available pieces of information are the scheme, user, pass, host, port, path, query, and fragment. Typically, you don’t need all these pieces, but here’s an example of how they make up an URL.

Consider the following example URL construction: http://nobody:secret@example.com:80/script.php?variable=value#anchor.

The values of each of the parts of the array are

 ■ scheme: http

 ■ user: nobody

 ■ pass: secret

 ■ host: example.com

 ■ port: 80

 ■ path: /script.php

 ■ query: variable=value

 ■ fragment: anchor

In the directory_submit.php script, you want only the host information, so you pull it out of the array as follows:

$url = parse_url($url);$host = $url['host'];

After you’ve done this, you can get the IP address of that host, if it is in the domain name service (DNS). You can do this by using the gethostbyname() function, which returns the IP if there is one or false if not:

$ip = gethostbyname($host);

You can also go the other way by using the gethostbyaddr() function, which takes an IP as a parameter and returns the hostname. If you call these functions in succession, you might well end up with a different hostname from the one you began with. This can mean that a site is using a virtual hosting service where one physical machine and IP address host more than one domain name.

412

Chapter 18  Using Network and Protocol Functions 

If the URL is valid, you then go on to check the email address. First, you split it into username and hostname with a call to explode():

$email = explode('@', $email);$emailhost = $email[1];

When you have the host part of the address, you can check to see whether there is a place for that mail to go by using the getmxrr() function:

getmxrr($emailhost, $mxhostsarr);

This function returns the set of Mail Exchange (MX) records for an address in the array you supply at $mxhostsarr.

An MX record is stored at the DNS and is looked up like a hostname. The machine listed in the MX record isn’t necessarily the machine where the email will eventually end up. Instead, it’s a machine that knows where to route that email. (There can be more than one; hence, this  function returns an array rather than a hostname string.) If you don’t have an MX record in the DNS, there’s nowhere for the mail to go.

If all these checks are okay, you can put this form data in a database for later review by a staff member. We don’t perform that functionality in this script, but you can see in the comment at the end of the script just where that information might go.

In addition to the functions you just used, you can use the more generic function checkdnsrr(), which takes a hostname and simply returns true if any record of it appears in the DNS. The output of this function would not give you anything to directly display to the user, as with the getmxrr() function used in the script, but would be simple to use for quick checks of validity. 

Backing Up or Mirroring a FileFile Transfer Protocol, or FTP, is used to transfer files between hosts on a network. Using PHP, you can use fopen() and the various file functions with FTP as you can with HTTP connec-tions, to connect to and transfer files to and from an FTP server. However, a set of FTP-specific functions also comes with the standard PHP install.

These functions are not built into the standard install by default. To use them under Unix, you need to run the PHP configure program with the --enable-ftp option and then rerun make. If you are using the standard Windows install, FTP functions are enabled automatically.

For more details on configuring PHP, see Appendix A,「Installing Apache, PHP, and MySQL.」

Using FTP to Back Up or Mirror a FileThe FTP functions are useful for moving and copying files from and to other hosts. One common use you might make of this capability is to back up your website or mirror files at another location. Let’s look at a simple example using the FTP functions to mirror a file. This script is shown in Listing 18.4.

Backing Up or Mirroring a File

413

Listing 18.4 

 ftp_mirror.php—Script to Download New Versions of a File from an FTP Server

<!DOCTYPE html><html><head>   <title>Mirror Update</title></head><body>   <h1>Mirror Update</h1>

<?php// set up variables - change these to suit application$host = 'apache.cs.utah.edu';$user = 'anonymous';$password = 'me@example.com';$remotefile = '/apache.org/httpd/httpd-2.4.16.tar.gz';$localfile = '/path/to/files/httpd-2.4.16.tar.gz';

// connect to host$conn = ftp_connect($host);

if (!$conn){  echo 'Error: Could not connect to '.$host;  exit;}

echo 'Connected to '.$host.'<br />';

// log in to host$result = @ftp_login($conn, $user, $pass);if (!$result){  echo 'Error: Could not log in as '.$user;  ftp_quit($conn);  exit;}

echo 'Logged in as '.$user.'<br />';

// Turn on passive modeftp_pasv($conn, true); 

// Check file times to see if an update is requiredecho 'Checking file time...<br />';if (file_exists($localfile)){

414

Chapter 18  Using Network and Protocol Functions 

  $localtime = filemtime($localfile);  echo 'Local file last updated ';  echo date('G:i j-M-Y', $localtime);  echo '<br />';}else{  $localtime = 0;}

$remotetime = ftp_mdtm($conn, $remotefile);if (!($remotetime >= 0)){   // This doesn't mean the file's not there, server may not support mod time   echo 'Can\'t access remote file time.<br />';   $remotetime = $localtime+1;  // make sure of an update}else{  echo 'Remote file last updated ';  echo date('G:i j-M-Y', $remotetime);  echo '<br />';}

if (!($remotetime > $localtime)){   echo 'Local copy is up to date.<br />';   exit;}

// download fileecho 'Getting file from server...<br />';$fp = fopen($localfile, 'wb');

if (!$success = ftp_fget($conn, $fp, $remotefile, FTP_BINARY)){  echo 'Error: Could not download file.';  ftp_quit($conn);  exit;}

fclose($fp);echo 'File downloaded successfully.';

Backing Up or Mirroring a File

415

// close connection to hostftp_close($conn);

?></body></html>

The output from running this script on one occasion is shown in Figure 18.4.

Figure 18.4  The FTP mirroring script checks whether the local version of a file is up to date and downloads a new version if not

The ftp_mirror.php script is quite generic. You can see that it begins by setting up some variables:

$host = 'apache.cs.utah.edu';$user = 'anonymous';$password = 'me@example.com';$remotefile = '/apache.org/httpd/httpd-2.4.16.tar.gz';$localfile = '/path/to/files/httpd-2.4.16.tar.gz';

The $host variable should contain the name of the FTP server you want to connect to, and the $user and $password correspond to the username and password you would like to log in with.

Many FTP sites support what is called anonymous login—that is, a freely available username that anybody can use to connect. No password is required, but it is a common courtesy to supply your email address as a password so that the system’s administrators can see where their users are coming from. We followed this convention here.

416

Chapter 18  Using Network and Protocol Functions 

The $remotefile variable contains the path to the file you would like to download. In this case, you are downloading and mirroring a local copy of the Apache web server for Unix.

The $localfile variable contains the path to the location where you are going to store the downloaded file on your machine. No matter what directory you place your downloaded file into, be sure the permissions are set up so that PHP can write a file into it. Regardless of your operating system, you will need to create this directory for the script to work, if the directory does not already exist. Additionally, if your operating system has strong permissions, you will need to make sure that they allow your script to write. You should be able to change these  variables to adapt this script for your purposes.

The basic steps you follow in this script are the same as if you wanted to manually transfer the file via FTP from a command-line interface:

1.  Connect to the remote FTP server.

2.  Log in (either as a user or anonymous).

3.  Check whether the remote file has been updated.

4.  If it has, download it.

5.  Close the FTP connection.

Let’s consider each of these steps in turn.

Connecting to the Remote FTP ServerThe first step is equivalent to typing

ftp hostname

at a command prompt on either a Windows or Unix platform. You accomplish this step in PHP with the following code:

$conn = ftp_connect($host);if (!$conn){  echo 'Error: Could not connect to '.$host;  exit;}echo 'Connected to '.$host.'<br />';

The function call here is to ftp_connect(). This function takes a hostname as a parameter and returns either a handle to a connection or false if a connection could not be established. The function can also take the port number on the host to connect to as an optional second parameter. We did not use this parameter here; if you don’t specify a port number, it will default to port 21, which is the default for FTP.

Backing Up or Mirroring a File

417

Logging In to the FTP ServerThe next step is to log in as a particular user with a particular password. You can achieve this by using the ftp_login() function:

$result = @ftp_login($conn, $user, $pass);if (!$result){  echo 'Error: Could not log in as '.$user;  ftp_quit($conn);  exit;}echo 'Logged in as '.$user.'<br />';

The function takes three parameters: an FTP connection (obtained from ftp_connect()), a username, and a password. It returns true if the user can be logged in and false if she can’t. 

Notice that we put an @ symbol at the start of the line to suppress errors. We did this because, if the user cannot be logged in, a PHP warning appears in the browser window. You can catch the error as we have done here by testing $result and supplying your own, more user-friendly error message.

Notice that if the login attempt fails, you actually close the FTP connection by using ftp_quit(). We discuss this function more later.

Before moving on to working with the remote filesystem, note the use of the ftp_pasv() function, in the line:

ftp_pasv($conn, true);

In this case, we are ensuring that passive mode is true, which means that all data connections will be initiated by the client (the script) rather than by the remote FTP server. If you do not turn on passive mode, you may find that your script will not succeed past the point of login.

Checking File Update TimesGiven that the point of this script is to update a local copy of a file, checking whether the file needs updating first is sensible because you don’t want to have to download the file again, particularly a large one, if it’s up to date. This way, you can avoid unnecessary network traffic. Let’s look at the code that checks file update times.

File times are the reason that you use the FTP functions rather than a much simpler call to a file function. The file functions can easily read and, in some cases, write files over network interfaces, but most of the status functions such as filemtime() do not work remotely. 

To begin deciding whether you need to download a file, you check that you have a local copy of the file by using the file_exists() function. If you don’t, obviously you need to download the file. If it does exist, you get the last modified time of the file by using the filemtime() function and store it in the $localtime variable. If it doesn’t exist, you set the $localtime variable to 0 so that it will be「older」than any possible remote file modification time:

echo 'Checking file time...<br />';if (file_exists($localfile)){

418

Chapter 18  Using Network and Protocol Functions 

  $localtime = filemtime($localfile);  echo 'Local file last updated ';  echo date('G:i j-M-Y', $localtime);  echo '<br />';}else{  $localtime = 0;} 

For reference, you can get a refresh on the file_exists() and filemtime() functions in Chapters 2 and 17,「Interacting with the File System and the Server,」respectively.

After you have sorted out the local time, you need to get the modification time of the remote file. You can get this time by using the ftp_mdtm() function:

$remotetime = ftp_mdtm($conn, $remotefile);

This function takes two parameters—the FTP connection handle and the path to the remote file—and returns either the Unix timestamp of the time the file was last modified or –1 if there is an error of some kind. Not all FTP servers support this feature, so you might not get a useful result from the function. In this case, you can choose to artificially set the $remotetime vari-able to be「newer」than the $localtime variable by adding 1 to it. This way, you ensure that an attempt is made to download the file:

if (!($remotetime >= 0)){  // This doesn't mean the file's not there, server may not support mod time  echo 'Can\'t access remote file time.<br />';  $remotetime=$localtime+1;  // make sure of an update}else{  echo 'Remote file last updated ';  echo date('G:i j-M-Y', $remotetime);  echo '<br />';}

When you have both times, you can compare them to see whether you need to download the file:

if (!($remotetime > $localtime)){  echo 'Local copy is up to date.<br />';  exit;}

Backing Up or Mirroring a File

419

Downloading the FileAt this stage, you try to download the file from the server:

echo 'Getting file from server...<br />';$fp = fopen ($localfile, 'wb');if (!$success = ftp_fget($conn, $fp, $remotefile, FTP_BINARY)){  echo 'Error: Could not download file.';  fclose($fp);  ftp_quit($conn);  exit;}fclose($fp);echo 'File downloaded successfully.';

You open a local file by using fopen(), as you learned previously. After you have done this, you call the function ftp_fget(), which attempts to download the file and store it in a local file. This function takes four parameters. The first three are straightforward: the FTP connection, the local file handle, and the path to the remote file. The fourth parameter is the FTP mode.

The two modes for an FTP transfer are ASCII and binary. The ASCII mode is used for transferring text files (that is, files that consist solely of ASCII characters), and the binary mode is used for transferring everything else. Binary mode transfers a file unmodified, whereas ASCII mode translates carriage returns and line feeds into the appropriate characters for your system (\n for Unix, \r\n for Windows, and \r for Macintosh).

PHP’s FTP library comes with two predefined constants, FTP_ASCII and FTP_BINARY, which represent these two modes. You need to decide which mode fits your file type and pass the corresponding constant to ftp_fget() as the fourth parameter. In this case, you are transferring a gzipped file, so you use the FTP_BINARY mode.

The ftp_fget() function returns true if all goes well or false if an error is encountered. You store the result in $success and let the user know how it went.

After the download has been attempted, you close the local file by using the fclose() function.

As an alternative to ftp_fget(), you could use ftp_get(), which has the following prototype:

int ftp_get (int ftp_connection, string localfile_path,        string remotefile_path, int mode)

This function works in much the same way as ftp_fget() but does not require the local file to be open. You pass it the system filename of the local file you would like to write to rather than a file handle.

Note that there is no equivalent to the FTP command mget, which can be used to download multiple files at a time. You must instead make multiple calls to ftp_fget() or ftp_get().

420

Chapter 18  Using Network and Protocol Functions 

Closing the ConnectionAfter you have finished with the FTP connection, you should close it using the ftp_quit() function:

ftp_quit($conn);

You should pass this function the handle for the FTP connection.

Uploading FilesIf you want to go the other way—that is, copy files from your server to a remote machine—you can use two functions that are basically the opposite of ftp_fget() and ftp_get(). These functions are called ftp_fput() and ftp_put(). They have the following prototypes:

int ftp_fput (int ftp_connection, string remotefile_path, int fp, int mode)int ftp_put (int ftp_connection, string remotefile_path,               string localfile_path, int mode)

The parameters are the same as for the _get equivalents.

Avoiding TimeoutsOne problem you might face when transferring files via FTP is exceeding the maximum execu-tion time. You will know when this happens because PHP gives you an error message. This error is especially likely to occur if your server is running over a slow or congested network, or if you are downloading a large file, such as a movie clip.

The default value of the maximum execution time for all PHP scripts is defined in the php.ini file. By default, it’s set to 30 seconds. This is designed to catch scripts that are running out of control. However, when you are transferring files via FTP, if your link to the rest of the world is slow or if the file is large, the file transfer could well take longer than this.

Fortunately, you can modify the maximum execution time for a particular script by using the set_time_limit() function. Calling this function resets the maximum number of seconds the script is allowed to run, starting from the time the function is called. For example, if you call

set_time_limit(90);

the script will be able to run for another 90 seconds from the time the function is called.

Using Other FTP FunctionsA number of other FTP functions are useful in PHP. The function ftp_size() can tell you the size of a file on a remote server. It has the following prototype:

int ftp_size(int ftp_connection, string remotefile_path)This function returns the size of the remote file in bytes or −1 if an error occurs. It is not supported by all FTP servers.

Next

421

One handy use of ftp_size() is to work out the maximum execution time to set for a  particular transfer. Given the file size and speed of your connection, you can take a guess as to how long the transfer ought to take and use the set_time_limit() function accordingly.

You can get and display a list of files in a directory on a remote FTP server by using the  following code:

$listing = ftp_nlist($conn, dirname($remotefile));foreach ($listing as $filename){  echo $filename.'<br />'";}

This code uses the ftp_nlist() function to get a list of names of files in a particular directory.

In terms of other FTP functions, almost anything that you can do from an FTP command line, you can do with the FTP functions, with the exception of mget (multiple get).  For mget, you could use ftp_nlist() to get a list of files and then fetch them as needed. 

For a complete list of PHP functions corresponding to each FTP command, please see the PHP online manual at http://php.net/manual/en/book.ftp.php.

Further ReadingWe covered a lot of ground in this chapter, and as you might expect, a lot of material is out there on these topics. For information on the individual protocols and how they work, you can consult the RFCs at http://www.rfc-editor.org/.

You might also find some of the protocol information at the World Wide Web Consortium interesting; go to http://www.w3.org/Protocols/.

You can also try consulting a book on TCP/IP such as Computer Networks by Andrew Tanenbaum.

NextWe are now ready to move on to Chapter 19,「Managing the Date and Time,」and look at PHP’s libraries of date and calendar functions. There, you see how to convert from user-entered formats to PHP formats to MySQL formats, and back again.

This page intentionally left blank 

