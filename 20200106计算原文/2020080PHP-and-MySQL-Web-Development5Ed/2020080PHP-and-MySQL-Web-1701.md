17Interacting with the File System and the Server

In Chapter 2,「Storing and Retrieving Data,」you saw how to read data from and write data to files on the web server. This chapter covers other PHP functions that enable you to interact with the file system on the web server.

Key topics covered in this chapter include

 ■ Uploading files with PHP

 ■ Using directory functions

 ■ Interacting with files on the server

 ■ Executing programs on the server

 ■ Using server environment variables

To discuss the uses of these functions, we look at an example. Consider a situation in which you would like to be able to upload images to be included in a website’s content (or maybe you want a friendlier interface than FTP or SCP for yourself). One approach is to upload the files directly through a form on your site, perhaps one that is locked down to administrator access only. Once those files are uploaded, you can then use them however you see fit. 

Before we dive into the file system functions, let’s briefly look at how file upload works.

Uploading FilesOne useful piece of PHP functionality is support for uploading files. Instead of files coming from the server to the browser using HTTP, they go in the opposite direction—that is, from the browser to the server. Usually, you implement this configuration with an HTML form interface. The one used in this example is shown in Figure 17.1.

380

Chapter 17  Interacting with the File System and the Server

Figure 17.1  The HTML form used for this file upload has different fields and field types from those of a normal HTML form

As you can see, the form has a box where the user can enter a filename or click the Browse button to browse files available to him or her locally. We look at how to implement this form shortly. 

After entering a filename, the user can click Send File, and the file will be uploaded to the server, where a PHP script is waiting for it.

Before we dive into the file uploading example, it is important to note that the php.ini file has five directives that control how PHP will work with file uploading. These directives, their default values, and descriptions are shown in Table 17.1.

Table 17.1  File Upload Configuration Settings in php.ini

Directive

file_uploads

upload_tmp_dir

Description

Controls whether HTTP file uploads are allowed. Values are On or Off.

Indicates the directory where uploaded files will temporarily be stored while they are waiting to be processed. If this value is not set, the system default will be used (such as /tmp)

Default Value

On

NULL

Uploading Files

381

upload_max_filesize Controls the maximum allowed size for uploaded 

2M

post_max_size

files. If a file is larger than this value, PHP will write a 0 byte placeholder file instead. You may use shorthand notation for size: K for kilobytes, M for megabytes, and G for gigabytes.

Controls the maximum size of POST data that PHP will accept. This value must be greater than the value for the upload_max_filesize directive, since it is the size for all of the post data, including any files to be uploaded. You may use shorthand  notation for this configuration setting just like with upload_max_filesize.

8M

HTML for File UploadTo implement file upload, you need to use some HTML syntax that exists specially for this purpose. The HTML for this form is shown in Listing 17.1.

Listing 17.1  upload.html—HTML Form for File Upload<!DOCTYPE html><html><head>   <title>Upload a File</title></head><body>  <h1>Upload a File</h1>  <form action="upload.php" method="post" enctype="multipart/form-data">  <input type="hidden" name="MAX_FILE_SIZE" value="1000000" />  <label for="the_file">Upload a file:</label>  <input type="file" name="the_file" id="the_file"/>  <input type="submit" value="Upload File"/>  </form></body></html> 

Note that this form uses POST; file uploads do not work with GET.

The extra features in this form are as follows:

 ■ In the <form> tag, you must set the attribute enctype="multipart/form-data" to let 

the server know that a file is coming along with the regular information.

382

Chapter 17  Interacting with the File System and the Server

 ■ If you do not have a server-side configuration setting to control the maximum uploaded file size, as shown in Table 17.1, you must have a form field that sets the maximum size file that can be uploaded. This is a hidden field and an example is shown here as<input type="hidden" name="MAX_FILE_SIZE" value=" 1000000">

 ■ The value is the maximum size (in bytes) of files you will allow people to upload. Here, we set this field to 1,000,000 bytes (roughly 1 megabyte). You may like to make it bigger or smaller for your application. If you use MAX_FILE_SIZE as a hidden form value, then it will override the server-side configuration if the MAX_FILE_SIZE is smaller than upload_max_filesize and post_max_size in your php.ini file.

 ■ You need an input of type file, shown here as

<input type="file" name="the_file" id="the_file"/>

 ■ You can choose whatever name you like for the file, but you should keep it in mind 

because you will use this name to access your file from the receiving PHP script.

Writing the PHP to Deal with the FileWriting the PHP script to handle the uploaded file is reasonably straightforward.

When the file is uploaded, it briefly goes into the temporary directory that is specified in the upload_tmp_dir directive indicated in your php.ini file. As stated in Table 17.1, if this  directive is not set, it will default to the web server’s main temporary directory, such as /tmp. If you do not move, copy, or rename the file before your script finishes execution, it will be deleted when the script ends.

The data you need to handle in your PHP script is stored in the superglobal array $_FILES. The entries in $_FILES will be stored with the name of the <file> tag from your HTML form. Your form element is named the_file, so the array will have the following contents:

 ■ The value stored in $_FILES['the_file']['tmp_name'] is the temporary name and 

location where the file has been temporarily stored on the web server.

 ■ The value stored in $_FILES['the_file']['name'] is the original name of the 

uploaded file.

 ■ The value stored in $_FILES['the_file']['size'] is the size of the file in bytes.

 ■ The value stored in $_FILES['the_file']['type'] is the MIME type of the file—for 

example, text/plain or image/png.

 ■ The value stored in $_FILES['the_file']['error'] will give you any error codes 

associated with the file upload. 

Given that you know where the file is and what it’s called, you can now copy it to somewhere useful. At the end of your script’s execution, the temporary file will be deleted. Hence, you must move or rename the file if you want to keep it.

Uploading Files

383

In this example, you will be uploading PNG image files to a new directory called /uploads/. Note that you will need to create a folder called uploads in the document root of your web server. If this directory does not exist, the file upload will fail.

A script that performs this task is shown in Listing 17.2.

Listing 17.2  upload.php—PHP to Catch the Files from the HTML Form<!DOCTYPE html><html><head>  <title>Uploading...</title></head><body>   <h1>Uploading File...</h1>

<?php

  if ($_FILES['the_file']['error'] > 0)  {    echo 'Problem: ';    switch ($_FILES['the_file']['error'])    {      case 1:           echo 'File exceeded upload_max_filesize.';         break;      case 2:           echo 'File exceeded max_file_size.';         break;      case 3:           echo 'File only partially uploaded.';         break;      case 4:           echo 'No file uploaded.';         break;      case 6:           echo 'Cannot upload file: No temp directory specified.';         break;      case 7:           echo 'Upload failed: Cannot write to disk.';         break;      case 8:           echo 'A PHP extension blocked the file upload.';         break;    }    exit;  }

384

Chapter 17  Interacting with the File System and the Server

  // Does the file have the right MIME type?  if ($_FILES['the_file']['type'] != 'image/png')  {    echo 'Problem: file is not a PNG image.';    exit;  }

  // put the file where we'd like it  $uploaded_file = '/filesystem/path/to/uploads/'.$_FILES['the_file']['name'];

  if (is_uploaded_file($_FILES['the_file']['tmp_name']))  {     if (!move_uploaded_file($_FILES['the_file']['tmp_name'], $uploaded_file))     {        echo 'Problem: Could not move file to destination directory.';        exit;     }  }  else  {    echo 'Problem: Possible file upload attack. Filename: ';    echo $_FILES['the_file']['name'];    exit;  }

  echo 'File uploaded successfully.';

  // show what was uploaded  echo '<p>You uploaded the following image:<br/>';  echo '<img src="/uploads/'.$_FILES['the_file']['name'].'"/>';?></body></html>

Interestingly enough, most of this script is error checking. File upload involves potential security risks, and you need to mitigate these risks where possible. You need to validate the uploaded file as carefully as possible to make sure it is safe to show your visitors.

Uploading Files

385

Let’s go through the main parts of the script. You begin by checking the error code returned in $_FILES['userfile']['error']. A constant is also associated with each of the codes. The possible constants and values are as follows:

 ■ UPLOAD_ERROR_OK, value 0, means no error occurred.

 ■ UPLOAD_ERR_INI_SIZE, value 1, means that the size of the uploaded file exceeds the 

maximum value specified in your php.ini file with the upload_max_filesize directive.

 ■ UPLOAD_ERR_FORM_SIZE, value 2, means that the size of the uploaded file exceeds the 

maximum value specified in the HTML form in the MAX_FILE_SIZE element.

 ■ UPLOAD_ERR_PARTIAL, value 3, means that the file was only partially uploaded.

 ■ UPLOAD_ERR_NO_FILE, value 4, means that no file was uploaded.

 ■ UPLOAD_ERR_NO_TMP_DIR, value 6, means that no temporary directory is specified in the 

php.ini.

 ■ UPLOAD_ERR_CANT_WRITE, value 7, means that writing the file to disk failed.

 ■ UPLOAD_ERR_EXTENSION, value 8, means that a PHP extension stopped the file upload 

process.

You also check the MIME type to ensure that only certain file types are uploaded. In this case, we want to upload image files only, and specifically PNG files. So, we test the MIME type by making sure that $_FILES['userfile']['type'] contains image/png. This is really only error checking, and not security checking. The MIME type is interpreted by the user’s browser from the file extension and information within the file, and then passed to your server. 

You then check that the file you are trying to open has actually been uploaded and is not a local file such as /etc/passwd. We will return to this at the end of this section.

If these checks work out, the code then copies the file into the /uploads/ directory, for easy access to display these uploaded files, as we do at the end of the script by printing an HTML <img/> tag containing the path to the uploaded file so that the user can see that the file uploaded successfully.

The results of one (successful) run of this script are shown in Figure 17.2.

386

Chapter 17  Interacting with the File System and the Server

Figure 17.2  After the file is uploaded, it is displayed as confirmation to the user that the upload was successful

To ensure that you are not vulnerable, this script uses the is_uploaded_file() and move_uploaded_file() functions to make sure that the file you are processing has actually been uploaded and is not a local file such as /etc/passwd. 

Please note that unless you write your upload handling script carefully, a malicious visitor could provide his or her own temporary filename and convince your script to handle that file as though it were the uploaded file. Because many file upload scripts echo the uploaded data back to the user or store it somewhere that it can be loaded, this could lead to people being able to access any file that the web server can read. This could include sensitive files such as /etc/passwd and PHP source code including your database passwords.

Uploading Files

387

NoteThe example form and script in Listings 17.1 and 17.2 handled just a single file upload, but you can easily modify the form and script to handle multiple files. Instead of a single file upload form field, use multiple form fields and change the name to reference the use of an array that will hold the names of the multiple uploaded files. For example,

<input type="file" name="the_files[]" id="the_files"/>

In your script, you would refer to the elements of the array using their array position, such as $_FILES['the_files']['name'][0], $_FILES['the_files']['name'][1], and so on.

Session Upload ProgressAs of version 5.4, PHP includes an option to track the progress of an upload. This option is especially useful for web applications that use AJAX to return real-time information to the user. In the traditional file upload model, such as the one you saw in the previous section, there is no way for you to inform the user about the status of his or her upload until the end of the upload process. When using the session upload progress functionality of PHP, you can receive information about the file upload as it is happening, and then display that information to the user in a useful way.

To use the session upload progress functionality in PHP, first ensure the directives listed in Table 17.2 are uncommented in the php.ini.

Table 17.2  Session Upload Progress Configuration Settings in php.ini

Directive

Description

Default Value

session.upload_progress.enabled 

Enabled session upload progress tracking within the $_SESSION superglobal variable. Values are On or Off.

On

On

upload_progress_

session.upload_progress.cleanup 

session.upload_progress. prefix

session.upload_progres s.name

session.upload_progress.freq

session.upload_progress.min_freq

Cleans up the session upload progress  information after the POST data has all been read and therefore the upload has completed. Values are On or Off.

The prefix is used as part of the session upload progress key in the $_SESSION superglobal, so as to ensure a unique identifier.

The name of the session upload progress key in the $_SESSION superglobal.

PHP_SESSION_UPLOAD_PROGRESS

Defines how often the session upload  progress information should be updated, in bytes or  percentages.

Defines the minimum delay between updates of the session upload progress information, in seconds.

1%

1

388

Chapter 17  Interacting with the File System and the Server

When these configuration options are set, the $_SESSION superglobal will contain information about your file uploads. If you were to print all the variables and their values contained in $_SESSION, as part of your file upload script, it might contain something like this: 

[upload_progress_testing] => Array    (        [start_time] => 1424047703        [content_length] => 43837        [bytes_processed] => 43837        [done] => 1        [files] => Array            (                [0] => Array                    (                        [field_name] => the_file                        [name] => B9l2dX8IAAAs-gT.png                        [tmp_name] => /tmp/phpUVj0Bz                        [error] => 0                        [done] => 1                        [start_time] => 1424047703                        [bytes_processed] => 43413                    )            )    ))

This output shows that a POST request was started at timestamp 1424047703 (that’s Mon, 16 Feb 2015 00:48:23 GMT) with a content length of 43837 bytes. The total number of bytes processed was 43837 and the value of done is 1 (true) which means the $_SESSION variables were printed after the POST was completed. If the value of done was 0, that would have meant the POST was not yet completed.

An additional array of files exists, and in this case the array of uploaded files contains only one set of keys and values representing only one uploaded file. In this case, the file from the input field with the name the_file, with an original name of B9l2dX8IAAAs-gT.png, was uploaded to a temporary file location as /tmp/phpUVj0Bz at timestamp 1424047703. The file was uploaded with no errors and has a value of done that is 1 (true) with a total number of bytes processed of 43413.

The values for bytes_processed and content_length come into play if you were to create and display a client-side progress bar to your user to enable watching the progress of the upload move toward completion. Because session upload progress is based on a user’s session, once that session is started with one script (the upload script), it can be accessed by another script, such as one that simply reads the value of bytes_processed and content_length within the current session for a particular uploaded file or files. If the script that reads session data is being constantly polled asynchronously, as with an AJAX request, then you can perform a simple mathematical function to return the percentage completed of the upload (number of bytes processed divided by the total content length, times 100). 

Uploading Files

389

Avoiding Common Upload ProblemsKeep the following points in mind when performing file uploads:

 ■ The previous example of a file upload script contains no user authentication whatsoever, 

but you should ensure that file uploads happen only from users authenticated within your system and authorized to do so. You shouldn’t allow just anybody to upload files to your site.

 ■ However, if you are allowing untrusted or unauthenticated users to upload files, it’s a good idea to be paranoid about the contents of the files. The last thing you want is a malicious script being uploaded and run on your system. You should be careful, not just of the type and contents of the file as we are here, but of the filename itself. It’s a good idea to rename uploaded files to something you know to be「safe,」so that if someone does upload a file with the expectations of doing something nefarious with it later, they will be unable to do so as their original file name is no longer valid.

 ■ To mitigate the risk of users「directory surfing」on your server, you can use the 

basename() function to modify the names of incoming files. This function will strip off any directory paths that are passed in as part of the filename, which is a common attack that is used to place a file in a different directory on your server. An example of this function is as follows:<?php   $path = "/home/httpd/html/index.php";   $file1 = basename($path);    $file2 = basename($path, ".php");   print $file1 . "<br/>"; // the value of $file1 is "index.php"   print $file2 . "<br/>"; // the value of $file2 is "index"?>

 ■ If you are using a Windows-based machine, be sure to use \\ or / instead of \ in file 

paths as per usual.

 ■ Using the user-provided filename as we did in the script shown earlier in this chapter can cause a variety of problems. The most obvious one is that you run the risk of accidentally overwriting existing files if somebody uploads a file with a name that has already been used. A less obvious risk is that different operating systems and even different local language settings allow different sets of legal characters in filenames. A file being uploaded may have a filename that has illegal characters for your system.

 ■ If you are having problems getting your file upload to work, check out your php.ini 

file. You may need to have the upload_tmp_dir directive set to point to some directory that you have access to. You might also need to adjust the memory_limit directive if you want to upload large files; this determines the maximum file size in bytes that you can upload. Apache also has some configurable timeouts and transaction size limits that might need attention if you are having difficulties with large uploads.

390

Chapter 17  Interacting with the File System and the Server

Using Directory FunctionsAfter the users have uploaded some files, it will be useful for them to be able to see what’s been uploaded and manipulate the content files. PHP has a set of directory and file system functions that are useful for this purpose.

Reading from DirectoriesFirst, let’s implement a script to allow directory browsing of the uploaded content. Browsing directories is actually straightforward in PHP. Listing 17.3 shows a simple script that can be used for this purpose.

Listing 17.3  browsedir.php—A Directory Listing of the Uploaded Files<!DOCTYPE html><html><head>   <title>Browse Directories</title></head><body>   <h1>Browsing</h1>

<?php  $current_dir = '/path/to/uploads/';  $dir = opendir($current_dir);

  echo '<p>Upload directory is '.$current_dir.'</p>';  echo '<p>Directory Listing:</p><ul>';

  while(false !== ($file = readdir($dir)))  {    //strip out the two entries of . and ..    if($file != "." && $file != "..")       {         echo '<li>'.$file.'</li>';       }  }  echo '</ul>';  closedir($dir);?>

</body></html>

This script makes use of the opendir(), closedir(), and readdir() functions.

Using Directory Functions

391

The function opendir() opens a directory for reading. Its use is similar to the use of fopen() for reading from files. Instead of passing it a filename, you should pass it a directory name:

$dir = opendir($current_dir);

The function returns a directory handle, again in much the same way as fopen() returns a file handle.

When the directory is open, you can read a filename from it by calling readdir($dir), as shown in the example. This function returns false when there are no more files to be read. Note that it will also return false if it reads a file called "0"; in order to guard against this, we explicitly test to make sure the return value is not equal to false:

while(false !== ($file = readdir($dir)))

When you are finished reading from a directory, you call closedir($dir) to finish. This is again similar to calling fclose() for a file.

Sample output of the directory browsing script is shown in Figure 17.3.

Figure 17.3  The directory listing shows all the files in the chosen directory

Typically the . (the current directory) and .. (one level up) directories would also display in the list in Figure 17.3. However, we stripped these directories out with the following line of code:

if ($file != "." && $file != "..")

If you delete this line of code, the . and .. directories will be added to the list of files that are displayed.

392

Chapter 17  Interacting with the File System and the Server

If you are making directory browsing available via this mechanism, it is sensible to limit the directories that can be browsed so that a user cannot browse directory listings in areas not normally available to him or her.

An associated and sometimes useful function is rewinddir($dir), which resets the reading of filenames to the beginning of the directory.

As an alternative to these functions, you can use the dir class provided by PHP. It has the  properties handle and path, and the methods read(), close(), and rewind(), which perform identically to the nonclass alternatives.

In Listing 17.4 we rewrite the above example using the dir class.

Listing 17.4  browsedir2.php—Using the dir Class to Display the Directory Listing<!DOCTYPE html><html><head>   <title>Browse Directories</title></head><body>   <h1>Browsing</h1>

<?php  $dir = dir("/path/to/uploads/");

  echo '<p>Handle is '.$dir->handle.'</p>';  echo '<p>Upload directory is '.$dir->path.'</p>';  echo '<p>Directory Listing:</p><ul>';

  while(false !== ($file = $dir->read()))    //strip out the two entries of . and ..    if($file != "." && $file != "..")       {         echo '<li>'.$file.'</li>';       }

  echo '</ul>';  $dir->close();?>

</body></html>

The filenames in the above example aren’t sorted in any particular order, so if you require a sorted list, you can use a function called scandir(). This function can be used to store the filenames in an array and sort them in alphabetical order, either ascending or descending, as in Listing 17.5.

Listing 17.5 

 scandir.php—Uses the scandir() Function to Sort the Filenames Alphabetically

Using Directory Functions

393

<!DOCTYPE html><html><head>   <title>Browse Directories</title></head><body>   <h1>Browsing</h1>

<?php$dir = '/path/to/uploads/';$files1 = scandir($dir);$files2 = scandir($dir, 1);

echo '<p>Upload directory is '.$dir.'</p>';echo '<p>Directory Listing in alphabetical order, ascending:</p><ul>';

foreach($files1 as $file){   if ($file != "." && $file != "..")   {     echo '<li>'.$file.'</li>';   }}

echo '</ul>';

echo '<p>Upload directory is '.$dir.'</p>';echo '<p>Directory Listing in alphabetical, descending:</p><ul>';

foreach($files2 as $file){   if ($file != "." && $file != "..")   {     echo '<li>'.$file.'</li>';   }}

echo '</ul>';

?></body></html>

394

Chapter 17  Interacting with the File System and the Server

Getting Information About the Current DirectoryYou can obtain some additional information about the filesystem, given a path to a file. For example, the dirname($path) and basename($path) functions return the directory part of the path and filename part of the path, respectively. This information could be useful for the directory browser, particularly if you begin to build up a complex directory structure of content based on meaningful directory names and filenames.

You could also add to your directory listing an indication of how much space is left for uploads by using the disk_free_space($path) function. If you pass this function a path to a  directory, it will return the number of bytes free on the disk (Windows) or the file system (Unix) on which the directory is located.

Creating and Deleting DirectoriesIn addition to passively reading information about directories, you can use the PHP functions mkdir() and rmdir() to create and delete directories. You can create or delete directories only in paths that the user the script runs as has access to.

Using mkdir() is more complicated than you might think. It takes two parameters: the path to the desired directory (including the new directory name) and the permissions you would like that directory to have. Here’s an example:

mkdir("/tmp/testing", 0777);

However, the permissions you list are not necessarily the permissions you are going to get. The inverse of the current umask will be combined with this value using AND to get the actual permissions. For example, if the umask is 022, you will get permissions of 0755.

You might like to reset the umask before creating a directory to counter this effect, by entering

$oldumask = umask(0);mkdir("/tmp/testing", 0777);umask($oldumask);

This code uses the umask() function, which can be used to check and change the current umask. It changes the current umask to whatever it is passed and returns the old umask, or, if called without parameters, it just returns the current umask.

Note that the umask() function has no effect on Windows systems.

The rmdir() function deletes a directory, as follows:

rmdir("/tmp/testing");

or

rmdir("c:\\tmp\\testing");

The directory you are trying to delete must be empty.

Interacting with the File System

395

Interacting with the File SystemIn addition to viewing and getting information about directories, you can interact with and get information about files on the web server. You previously looked at writing to and reading from files. A large number of other functions related to the filesystem are available, which you can read about in more detail at http://php.net/manual/en/book.filesystem.php.

Getting File InformationAs an example of the types of information you can get about each file, let’s first alter the part of the directory browsing script that reads files as follows, to link to another script you’ll create momentarily. Instead of simply printing the file name within a bulleted list, print the file name as a link within a bulleted list:

echo '<li><a href="filedetails.php?file='.$file.'">'.$file.'</a></li>';

You can then create the script filedetails.php to provide further information about a file. The contents of this file are shown in Listing 17.6.

One warning about the script that follows in Listing 17.6: Some of the functions used here are not supported under Windows, including posix_getpwuid(), fileowner(), and  filegroup(), or are not supported reliably.

Listing 17.6  filedetails.php—File Status Functions and Their Results<!DOCTYPE html><html><head>  <title>File Details</title></head><body><?php

  if (!isset($_GET['file']))   {     echo "You have not specified a file name.";  }   else {     $uploads_dir = '/path/to/uploads/';

     // strip off directory information for security     $the_file = basename($_GET['file']);  

     $safe_file = $uploads_dir.$the_file;

     echo '<h1>Details of File: '.$the_file.'</h1>';

     echo '<h2>File Data</h2>';     echo 'File Last Accessed: '.date('j F Y H:i', fileatime($safe_file)).'<br/>';     echo 'File Last Modified: '.date('j F Y H:i', filemtime($safe_file)).'<br/>';

396

Chapter 17  Interacting with the File System and the Server

     $user = posix_getpwuid(fileowner($safe_file));     echo 'File Owner: '.$user['name'].'<br/>';

     $group = posix_getgrgid(filegroup($safe_file));     echo 'File Group: '.$group['name'].'<br/>';

     echo 'File Permissions: '.decoct(fileperms($safe_file)).'<br/>';     echo 'File Type: '.filetype($safe_file).'<br/>';     echo 'File Size: '.filesize($safe_file).' bytes<br>';

     echo '<h2>File Tests</h2>';     echo 'is_dir: '.(is_dir($safe_file)? 'true' : 'false').'<br/>';     echo 'is_executable: '.(is_executable($safe_file)? 'true' : 'false').'<br/>';     echo 'is_file: '.(is_file($safe_file)? 'true' : 'false').'<br/>';     echo 'is_link: '.(is_link($safe_file)? 'true' : 'false').'<br/>';     echo 'is_readable: '.(is_readable($safe_file)? 'true' : 'false').'<br/>';     echo 'is_writable: '.(is_writable($safe_file)? 'true' : 'false').'<br/>';  }?></body></html>

The results of one sample run of Listing 17.6 are shown in Figure 17.4.

Figure 17.4  The File Details view shows file system information about a file. Note that  permissions are shown in an octal format

Interacting with the File System

397

Let’s examine what each of the functions used in Listing 17.6 does. As mentioned previously, the basename() function gets the name of the file without the directory. (You can also use the dirname() function to get the directory name without the filename.)

The fileatime() and filemtime() functions return the timestamp of the time the file was last accessed and last modified, respectively. We reformatted the timestamp here using the date() function make it more human readable. These functions return the same value on some operating systems (as in the example) depending on what information the system stores.

The fileowner() and filegroup() functions return the user ID (uid) and group ID (gid) of the file. These IDs can be converted to names using the functions posix_getpwuid() and posix_getgrgid(), respectively, which makes them a bit easier to read. These functions take the uid or gid as a parameter and return an associative array of information about the user or group, including the name of the user or group, as we have used in this script.

The fileperms() function returns the permissions on the file. We reformatted them as an octal number using the decoct() function to put them into a format more familiar to Unix users.

The filetype() function returns some information about the type of file being examined. The possible results are fifo, char, dir, block, link, file, and unknown.

The filesize() function returns the size of the file in bytes.

The second set of functions—is_dir(), is_executable(), is_file(), is_link(), is_readable(), and is_writable()—all test the named attribute of a file and return true or false.

Alternatively, you could use the function stat() to gather a lot of the same information. When passed a file, this function returns an array containing similar data to these functions. The lstat() function is similar, but for use with symbolic links.

All the file status functions are quite expensive to run in terms of time. Their results are  therefore cached. If you want to check some file information before and after a change, you need to call

clearstatcache();

to clear the previous results. If you want to use the previous script before and after changing some of the file data, you should begin by calling this function to make sure the data produced is up to date.

Changing File PropertiesIn addition to viewing file properties, you can alter them as well, if the web server user has the proper filesystem permissions.

Each of the chgrp(file, group), chmod(file, permissions), and chown(file, user) functions behaves similarly to its Unix equivalent. None of these functions will work in Windows-based systems, although chown() will execute and always return true.

398

Chapter 17  Interacting with the File System and the Server

The chgrp() function changes the group of a file. It can be used to change the group only to groups of which the user is a member unless the user is root.

The chmod() function changes the permissions on a file. The permissions you pass to it are in the usual Unix chmod form. You should prefix them with a 0 (a zero) to show that they are in octal, as in this example:

chmod('somefile.txt', 0777);

The chown() function changes the owner of a file. It can be used only if the script is running as root, which should never happen, unless you are specifically running the script from the command line to perform an administrative task.

Creating, Deleting, and Moving FilesYou can use the file system functions to create, move, and delete files, if the web server user has the proper filesystem permissions.

First, and most simply, you can create a file, or change the time it was last modified, using the touch() function. This function works similarly to the Unix command touch. The function has the following prototype:

bool touch (string file, [int time [, int atime]])

If the file already exists, its modification time will be changed either to the current time or the time given in the second parameter if it is specified. If you want to specify this time, you should give it in timestamp format. If the file doesn’t exist, it will be created. The access time of the file will also change, by default to the current system time or alternatively to the timestamp you specify in the optional atime parameter.

You can delete files using the unlink() function. (Note that this function is not called delete()—there is no delete().) You use it like this:

unlink($filename);

You can copy and move files with the copy() and rename() functions, as follows:

copy($source_path, $destination_path);rename($oldfile, $newfile); 

The rename() function serves double duty as a function to move files from place to place because PHP doesn’t have a move function beyond the specific move_uploaded_file() func-tion. Whether you can move files from file system to file system and whether files are over-written when rename() is used are operating system dependent, so check the effects on your server. Also, be careful about the path you use to the filename. If  relative, this will be relative to the location of the script, not the original file.

Using Program Execution FunctionsLet’s move away from the file system functions now and look at the functions available for running commands on the server.

Using Program Execution Functions

399

These functions are useful when you want to provide a web-based front end to an existing command-line–based system. You can use four main techniques to execute a command on the web server. They are all relatively similar, but there are some minor differences:

 ■ exec()—The exec() function has the following prototype:

string exec (string command [, array &result [, int &return_value]])

You pass in the command that you would like executed, as in this example:

exec("ls -la");

The exec() function has no direct output. It returns the last line of the result of the  command.

If you pass in a variable as result, you will get back an array of strings representing each line of the output. If you pass in a variable as return_value, you will get the return code.

 ■ passthru()—The passthru() function has the following prototype:

void passthru (string command [, int return_value])

The passthru() function directly echoes its output through to the browser. (This functionality is useful if the output is binary—for example, some kind of image data.) It returns nothing.

The parameters work the same way as exec()’s parameters do.

 ■ system()—The system() function has the following prototype:

string system (string command [, int return_value])

The system() function echoes the output of the command to the browser. It tries to ﬂ ush the output after each line (assuming you are running PHP as a server module), which distinguishes it from passthru(). It returns the last line of the output (upon success) or false (upon failure).

The parameters work the same way as in the other functions listed above.

 ■ Backticks—We mentioned backticks briefly in Chapter 1,「PHP Crash Course.」They are 

actually execution operators.

They have no direct output. The result of executing the command is returned as a string, which can then be echoed or whatever you like.

If you have more complicated needs, you can also use popen(), proc_open(), and proc_close() functions, which fork external processes and pipe data to and from them.

The script shown in Listing 17.7 illustrates how to use each of the four techniques in an  equivalent fashion.

400

Chapter 17  Interacting with the File System and the Server

Listing 17.7  progex.php—File Status Functions and Their Results<?php

chdir('/path/to/uploads/');

// exec versionecho '<h1>Using exec()</h1>';echo '<pre>';

// unixexec('ls -la', $result);

// windows// exec('dir', $result);

foreach ($result as $line){   echo $line.PHP_EOL;}

echo '</pre>';echo '<hr />';

// passthru versionecho '<h1>Using passthru()</h1>';echo '<pre>';

// unixpassthru('ls -la') ;

// windows// passthru('dir');

echo '</pre>';echo '<hr />';

// system versionecho '<h1>Using system()</h1>';echo '<pre>';

// unix$result = system('ls -la');

// windows// $result = system('dir');

Interacting with the Environment: getenv() and putenv()

401

echo '</pre>';echo '<hr />';

// backticks versionecho '<h1>Using Backticks</h1>';echo '<pre>';

// unix$result = `ls -al`;

// windows // $result = `dir`;

echo $result;echo '</pre>';

?>

You could use one of these approaches as an alternative to the directory-browsing script you saw earlier. Note that one of the side effects of using external functions is amply demonstrated by this code: Your code is much less portable, as it uses Unix commands, and the Windows commands shown (but commented out) may not produce the effects you want.

If you plan to include user-submitted data as part of the command you’re going to execute, you should always run it through the escapeshellcmd() function first. This way, you stop users from maliciously (or otherwise) executing commands on your system. You can call it like this:

system(escapeshellcmd($command));

You should also use the escapeshellarg() function to escape any arguments you plan to pass to your shell command.

Interacting with the Environment: getenv() and putenv()Before we leave this discussion, let’s look at how to use environment variables from within PHP. Two functions serve this purpose: getenv(), which enables you to retrieve  environment  variables, and putenv(), which enables you to set environment variables. Note that the  environment we are talking about here is the environment in which PHP runs on the server.

You can get a list of all PHP’s environment variables by running phpinfo(). Some are more useful than others; for example,

getenv("HTTP_REFERER");

returns the URL of the page from which the user came to the current page.

402

Chapter 17  Interacting with the File System and the Server

If you are a system administrator and would like to limit which environment variables programmers can set, you can use the safe_mode_allowed_env_vars directive in php.ini. When PHP runs in safe mode, users can set only environment variables whose prefixes are listed in this directive.

You can also set environment variables as required with putenv(), as in this example:

$home = "/home/nobody";putenv (" HOME=$home ");

NoteIf you would like more information about what some of the environment variables represent, you can look at the CGI specification at http://www.ietf.org/rfc/rfc3875.

Further ReadingMost of the file system functions in PHP map to underlying operating system functions of the same name. Try reading the man pages for more information if you’re using Unix.

NextIn Chapter 18,「Using Network and Protocol Functions,」you learn to use PHP’s network and protocol functions to interact with systems other than your own web server. This again expands the horizons of what you can do with your scripts.

