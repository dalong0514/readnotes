AInstalling Apache, PHP, and MySQL

Apache, PHP, and MySQL are available for many combinations of operating systems and web servers. In this appendix, we explain how to set up Apache, PHP, and MySQL on a UNIX platform from (almost) scratch, and offer pointers for installing these technologies on Windows and Mac OS X.

Key topics covered in this appendix include

 ■ Running PHP as a CGI interpreter or as a module

 ■ Installing Apache, SSL, PHP, and MySQL under UNIX

 ■ Installing Apache, PHP, and MySQL using all-in-one installation packages

 ■ Installing PEAR

 ■ Considering other web server configurations

NoteDetailed information for adding PHP to Microsoft Internet Information Server or other web servers is not included in this appendix. We recommend using the Apache web server when possible. However, pointers to other web server configurations can be found at the end of this appendix.

 

 

Our goal in this appendix is to provide you with an installation guide for a web server that will enable you to host multiple websites. Some sites that you create will require Secure Sockets Layer (SSL) for e-commerce solutions, and most sites are driven via scripts to connect to a  database (DB) server to extract and process data. Therefore, we include instructions for the common setup of PHP, MySQL, and Apache with SSL on a UNIX machine.

Many PHP users never need to install PHP on a machine, which is why this material is in an appendix rather than Chapter 1,「PHP Crash Course.」The easiest way to get access to a reliable server with a fast connection to the Internet and PHP already installed is to simply sign up for 

600

Appendix A  Installing Apache, PHP, and MySQL

an account at one of the thousands of hosting services or hosting service resellers around the globe. If this is the route you take, be sure your hosting provider is using up-to-date versions of Apache, PHP, and MySQL, otherwise you will be susceptible to security issues that you cannot control (not to mention you will not be able to use the latest and greatest features within the technologies).

Depending on why you are installing PHP on a machine, you might make different decisions. For example, if you have a machine permanently connected to the network that you intend to use as a live server, then performance will be important to you. If you are building a  development server where you can build and test your code, then having a similar configuration to the live server will be the most important consideration.

NoteThe PHP interpreter can be run as either a module or as a separate common gateway interface (CGI) binary. Generally, the module version is used for performance reasons. However, the CGI version is sometimes used for servers where a module version is not available or because it enables Apache users to run different PHP-enabled pages under different user IDs.In this appendix, we primarily cover the module option as the method to run PHP .

Installing Apache, PHP, and MySQL Under UNIXDepending on your needs and your level of experience with UNIX systems, you might choose to do a binary install or compile the programs directly from their source. Both approaches have their advantages.

A binary install will take an expert minutes and a beginner not much longer, but it will result in a system that is probably a minor version or two behind the current releases and one that is configured with somebody else’s choices of options. If you have read the subsequent release changelogs and know what you’re missing, or if the build options used by the maintainer of the binary distribution meet your needs, then by all means perform a binary installation.

Although a source install will take additional time to download, install, and configure, and such an approach may be intimidating the first few times you do it, it does give you complete control over the configuration of the technologies. When performing a source installation, you may choose exactly what to install, which version to use, and have complete control over the configuration directives that can be set.

Binary InstallationMost Linux distributions include a preconfigured Apache Web Server with PHP built in. The details of what is provided out of the box depend on your chosen distribution and version.

Installing Apache, PHP, and MySQL Under UNIX

601

One disadvantage of binary installs is that you rarely get the latest version of a program. Depending on how important the last few bug fix releases are, getting an older version might not be a problem for you. However, we recommend that if you intend to use the preconfigured binary installations of PHP, MySQL, Apache, and any ancillary libraries, then before you begin using them be sure to update the packages using your distribution’s typical update method (e.g., using apt-get, yum, or other package managers).

The biggest issue with binary installations is that you do not get to choose what options are compiled into your programs. The most flexible and reliable path to take is to compile all the programs you need from their sources. This path will take a little more time than installing packages using a package manager, so we understand you might choose to use binary packages when available, and in fact if you just want a basic configuration, it is likely that the official pre-packaged binaries for your system will meet your needs.

Source InstallationTo install Apache, PHP, and MySQL from source under a UNIX environment, the first step is to decide which extra modules you will load under the trio. Because some of the examples covered in this book show the use of a secure server for web transactions, you should install an SSL-enabled server.

For purposes of this book, the PHP configuration is more or less the default setup but also covers ways to enable the gd2 library under PHP.

The gd2 library is just one of the many libraries available for PHP. We included this installation step so that you can get an idea of what may be required to build from source and enable extra libraries within PHP. Compiling most UNIX programs follows a similar process, but as you can see as we move through this section, there are times when it is just easier to install precompiled packages anyway.

You usually need to recompile PHP after installing a new library, so if you know what you need in advance, you can install all required libraries on your machine and then begin to compile the PHP module.

Here, we describe installation from source on a Ubuntu server, but the description is generic enough to apply to other UNIX servers as well.

Start by gathering the required files for the installation. You need these items:

 ■ Apache (http://httpd.apache.org/)—The web server

 ■ OpenSSL (http://www.openssl.org/)—Open source toolkit that implements the Secure 

Sockets Layer

 ■ MySQL (http://www.mysql.com/)—The relational database

602

Appendix A  Installing Apache, PHP, and MySQL

 ■ PHP (http://www.php.net/)—The server-side scripting language

 ■ JPEG (http://www.ijg.org/)—The JPEG library, needed for gd2

 ■ PNG (http://www.libpng.org/pub/png/libpng.html)—The PNG library, needed for gd2

 ■ zlib (http://www.zlib.net/)—The zlib library, needed for the PNG library, above

 ■ IMAP (ftp://ftp.cac.washington.edu/imap/)—The IMAP C client, needed for IMAP

If you want to use the mail() function, you will need to have an MTA (mail transfer agent) installed, although we do not go through this here.

We assume that you have root access to the server and the following tools installed on your system:

 ■ gzip or gunzip

 ■ gcc and GNU make

When you are ready to begin the PHP, Apache, and MySQL installation processes, you should start by downloading all file sources to a temporary directory. In our case, we chose /usr/src for the temporary directory. You should download them as the root user to avoid permissions problems.

Installing MySQLIn this section, we show you how to do a binary install of MySQL. Installing the official distributed binary version of MySQL for your system is actually the recommended process, given the few build configuration options you could possibly need, combined with the number of steps in the build process that have proven finicky throughout the years. Although it’s completely possible to download and build MySQL from source, and in fact the instructions are quite good, you’ll get up and running quicker and with no difference in functionality if you just install the binaries for your particular system.

In this example, we are using the apt repository for Ubuntu 14.04, but you can navigate to the proper binary repository for your system at http://www.mysql.com/downloads/. This type of install automatically places files in various locations and handles system configuration options.

We downloaded the release package mysql-apt-config_0.3.2-1ubuntu14.04_all.deb and then installed it using

# sudo dpkg -i mysql-apt-config_0.3.2-1ubuntu14.04_all.deb

Installing Apache, PHP, and MySQL Under UNIX

603

At this point you will be asked which components you wish to install, as shown in Figure A.1.

Figure A.1  Configuration options for MySQL

Select「Server」and continue, then select the server version in the next step. Select「Apply」to apply the changes, then「Ok」to set the configuration. At this point your system is prepared to use apt to install precisely the application you wish to use, so issue the update command like so:

# sudo apt-get update

When this process finishes, finally install the MySQL server:

# sudo apt-get install mysql-server

You may be asked to install additional necessary libraries, and if so select Y to continue. 

Next in the installation process, you should next see a request to set the MySQL root password, as shown in Figure A.2.

604

Appendix A  Installing Apache, PHP, and MySQL

Figure A.2  Prompted for a MySQL root password

After setting the password, you will be asked to confirm it, and the installation process will continue.

When you install MySQL, it automatically creates three databases. One is the mysql table, which controls users, hosts, and DB permissions in the actual server. The others are  information_schema and performance_schema, which store additional metadata about the MySQL server. You can check your database via the command line like this:

# mysql -u root –pEnter password:mysql> show databases;+--------------------+| Database           |+--------------------+| information_schema || mysql              || performance_schema |+--------------------+3 rows in set (0.00 sec)

Type quit or \q to quit the MySQL client.

The default MySQL configuration allows any user access to the system without providing a username or password. This is obviously undesirable, which is why the installation process takes you through the step of setting a password for the root user

Installing Apache, PHP, and MySQL Under UNIX

605

The final compulsory piece of MySQL housekeeping is deleting any anonymous accounts that may be part of the distributed database. Opening a command prompt and typing the following lines accomplish that task:

# mysql -u root –pEnter password:mysql> use mysqlmysql> delete from user where User='';mysql> quit

You then need to type

# mysqladmin -u root -p reload

for these changes to take effect. (You should be prompted for your password.)

At this point you have a working secured installation of MySQL that you can use with PHP.

Installing PHP and ApachePlease note that in the examples below, the word VERSION is used as a placeholder for the recent version of the software available to you. The installation process does not differ from version to version. When running the commands listed, substitute VERSION with the specific version number of the software you have downloaded. 

Before installing PHP, let’s get a vanilla version of Apache configured and installed so that the PHP install process can find everything related to Apache. Don’t worry, we will come back to the topic of fully configuring and installing Apache later in this section. First, ensure you are in the directory that contains the source-code distribution. 

# cd /usr/src# sudo gunzip httpd-VERSION.tar.gz –# sudo tar –xvf httpd-VERSION.tar# cd httpd-VERSION# sudo ./configure --prefix=/usr/local/apache2 –-enable-so

The second configuration flag is present to make sure that mod_so will be compiled into Apache. This module, named for the UNIX shared object (*.so) format, enables the use of dynamic modules such as PHP with Apache.

Let’s continue the build process by issuing the following commands:

# sudo make# sudo make install

At this point, a basic version of Apache is configured on your system. To continue preparing to build PHP, you will need to build the additional libraries that PHP and Apache will use in our example (JPEG, PNG, zlib, OpenSSL, and IMAP) so that the PHP build configuration properly points to those libraries.

606

Appendix A  Installing Apache, PHP, and MySQL

To install the JPEG library, follow these steps:

# cd /usr/src# sudo gunzip jpegsrc.VERSION.tar.gz# sudo tar –xvf jpegsrc.VERSION.tar.gz# cd jpeg-VERSION# sudo ./configure# sudo make# sudo make install

After the final step, unless there were error messages along the way, the JPEG library should be installed in /usr/local/lib. If there were error messages during the process, follow the instructions in the error message or refer to the JPEG library documentation.

Repeat the gunzip, tar, configure, make, and make install process for the PNG and zlib library source files, and note the installation directories for each.

For installing the IMAP C-client library, you can download and build the source files in much the same way, but there are some idiosyncrasies involved that may result in differences from system to system. We recommend you follow the most recent guidelines published in the PHP manual at http://php.net/manual/en/imap.requirements.php. 

You might also find it considerably simpler to install the precompiled package for your UNIX server type, as we do here on Ubuntu 14.04:

# sudo  sudo apt-get install libc-client-dev

With all of the libraries prepared for use, let’s switch back to setting up PHP. Extract the source files and change to its directory:

# cd /usr/src# sudo gunzip  php-VERSION.tar.gz # sudo tar –xvf php-VERSION.tar# cd php-VERSIONMany options are available with PHP’s configure command. Use ./configure --help to determine what you want to add. In this case, let’s add support for MySQL, Apache, and gd2.

Note that the following is all one command. You can put it all on one line or, as shown here, use the continuation character, the backslash (\). This character allows you to type one command across multiple lines to improve readability:

# ./configure  --prefix=/usr/local/php               --with-mysqli=mysqlnd \               --with-apxs2=/usr/local/apache2/bin/apxs \               --with-jpeg-dir=/usr/local/lib \               --with-png-dir=/usr/local/lib \               --with-zlib-dir=/usr/local/lib \               --with-imap=/usr/lib \               --with-kerberos \                --with-imap-ssl \               --with-gd

The first configuration flag sets the location of the installation directory for PHP, in this case /usr/local/php. The second flag ensures that PHP is built with the native driver for MySQL. 

Installing Apache, PHP, and MySQL Under UNIX

607

The third flag tells PHP the location of apxs2 (the Apache Extension tool), which is used to build Apache modules, of which PHP will be one. The need to configure the location of apxs2 within the PHP build process is so that the appropriate Apache module version of PHP can be built, resulting in the need to pre-configure and install at least a basic version of Apache before building PHP.

The next set of configuration flags point the PHP configuration tool to the location of the libraries you installed previously (JPEG, PNG, zlip, and IMAP). The --with-kerberos and –with-imap-ssl flags are additional flags related to the use of the IMAP library; depending on the precompiled package you use on your system, you may not need these flags or you may need additional flags. The configuration process will tell you what flags are missing.

Once the configuration has completed, you will see a message something like this:

Generating filesconfigure: creating ./config.statuscreating main/internal_functions.ccreating main/internal_functions_cli.c+--------------------------------------------------------------------+| License:                                                           || This software is subject to the PHP License, available in this     || distribution in the file LICENSE.  By continuing this installation || process, you are bound by the terms of this license agreement.     || If you do not agree with the terms of this license, you must abort || the installation process at this point.                            |+--------------------------------------------------------------------+

Thank you for using PHP.

config.status: creating php7.specconfig.status: creating main/build-defs.hconfig.status: creating scripts/phpizeconfig.status: creating scripts/man1/phpize.1config.status: creating scripts/php-configconfig.status: creating scripts/man1/php-config.1config.status: creating sapi/cli/php.1config.status: creating sapi/cgi/php-cgi.1config.status: creating ext/phar/phar.1config.status: creating ext/phar/phar.phar.1config.status: creating main/php_config.hconfig.status: main/php_config.h is unchangedconfig.status: executing default commands

At this point your system is prepared to make and install the binaries; issue the make and make install commands to build the binaries according to your specifications:

# make# make install

608

Appendix A  Installing Apache, PHP, and MySQL

After the final step, unless there were error messages along the way, the PHP binary will have been built and installed, and the PHP Apache module will have been built and installed and put in the proper directory within the Apache directory structure. The last bit of configuration you might want to do is to ensure that the php.ini file is located in a stable and usual place:

# sudo cp php.ini-development /usr/local/php/lib/php.ini

or

# sudo cp php.ini-production /usr/local/php/lib/php.ini

The two versions of php.ini in the suggested commands have different options set. The first, php.ini-development, is intended for development machines. For instance, it has display_errors set to On. This makes development easier, but it is not really appropriate on a production machine. When we refer to a php.ini setting’s default value in this book, we mean its setting in this version of php.ini. The second version, php.ini-production, is intended for production machines.

You can edit the php.ini file to set PHP options. There are numerous options that you might choose to set, but a few in particular are worth noting. You might need to set the value of sendmail_path if you want to send email from scripts.

With PHP all set, it’s time to briefly return to the Apache source files and reconfigure and recompile in a more appropriate way for development work (beyond the basics we configured earlier). In addition to the configuration option --enable-so, which enabled the use of shared objects such as PHP, let’s use  --enable-ssl to enables the use of the mod_ssl module. Additionally, we set the base directory for OpenSSL, which we configured and installed earlier in this section.

# cd /usr/local/httpd-VERSION# sudo SSL_BASE=../openssl-VERSION \       ./configure \       --prefix=/usr/local/apache2 \       --enable-so \       --enable-ssl# sudo make# sudo make install

If everything goes well, you will be returned to the command prompt without error messages and can make the final configuration modifications to your installation. If the installation process encounters any errors, visit the Apache HTTP Server 2.4 documentation for help working through any anomalies: http://httpd.apache.org/docs/2.4/. 

Basic Apache Configuration ModificationsThe file used for most of the Apache configuration is called httpd.conf. If you have followed the previous instructions, your httpd.conf file will be located in the /usr/local/apache2/conf directory. To ensure that your server will startup and use PHP and SSL, you’ll need to make a few modifications:

Installing Apache, PHP, and MySQL Under UNIX

609

 ■ Find the line that begins with #ServerName and make it simply say ServerName 

yourservername.com

 ■ Find the block of lines that begin with AddType and add the following to ensure that 

files with the PHP extension are appropriately routed through the PHP module for processing:

AddType application/x-httpd-php .phpAddType application/x-httpd-php-source .phps

Now you are ready to start the Apache server to see whether it works with PHP. First, let’s start the server without the SSL support and see whether it comes up at all. In the next sections we’ll check for PHP support and also SSL support  to see whether everything is working.

You can use configtest to check whether the configuration is set up properly:

# cd /usr/local/apache2/bin# sudo ./apachectl configtestSyntax OK# sudo ./apachectl start./apachectl start: httpd started

If it worked correctly, you will see something similar to Figure A.3 when you connect to the server with a web browser.

NoteYou can connect to the server by using a domain name or the actual IP address of the computer. Check both cases to ensure that everything is working properly.

Figure A.3  The default test page provided by Apache 

610

Appendix A  Installing Apache, PHP, and MySQL

Is PHP Support Working?Now that you’re sure the Apache web server works on its own, you can test its PHP support. Create a file named test.php in the document root path, which should be /usr/local/apache/htdocs if you followed the installation instructions above. Note that you can change this directory path in the httpd.conf file.

The file should contain just the following line of code:

<?php phpinfo(); ?>

The output screen should look like Figure A.4.

Figure A.4  The function phpinfo() provides useful configuration information

Is SSL Working?At this stage, SSL should not be working on your machine, because we have not created the SSL certificates and keys that go along with it. Apache is configured and ready to go, but the underlying certificates that secure your data are not yet present.

Installing Apache, PHP, and MySQL Under UNIX

611

You can create self-signed certificates for development purposes using OpenSSL; if you are going to use your site in production, you should use legitimately signed SSL certificates from a Certificate Authority. For example, Let’s Encrypt is a free, automated, and open certificate authority (CA), run for the public’s benefit by the Internet Security Research Group (ISRG). Learn more at https://letsencrypt.org/.

To create a self-signed certificate, issue the following command to create a certificate and key and place both in a location that Apache expects:

# sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \      -keyout /usr/local/apache2/conf/server.key \     -out /usr/local/apache2/conf/server.crt

The certificate and key creation script will ask some information such as country, state, company name, and domain name; you can make dummy information or use real information, as you’d like. After the script finishes, you will have a dummy self-signed certificate good for 365 days, placed in /usr/local/apache2/conf along with its matching key.

The Apache SSL module has its own configuration file, located at /usr/local/apache2/conf/extra/httpd-ssl.conf. You can leave it untouched at this stage and just restart Apache for all changes to take effect, or you can continue on to modify the configuration as you wish. For documentation on the possible Apache httpd-ssl.conf modifications, please see http://httpd.apache.org/docs/2.4/mod/mod_ssl.html.

In Apache 2.4, all you need to do to enable SSL at the server level is uncomment the rule for the httpd-ssl.conf file in httpd.conf. Instead of this in httpd.conf,

# Include conf/extra/httpd-ssl.conf

the line should read:

Include conf/extra/httpd-ssl.conf

Once configuration changes have been made, simply restart the server:

# sudo /usr/local/apache2/bin/apachectl restart

Test to see whether it works by connecting to the server with a web browser and selecting the https protocol, like this:

https://yourserver.yourdomain.com

Try your server’s IP address also, like this:

https://xxx.xxx.xxx.xxx

or

http://xxx.xxx.xxx.xxx:443

If the configuration and self-signed certificates are all working, the server will send the certifi-cate to the browser to establish a secure connection. Given this is a self-signed certificate, the browser will also show you a warning before allowing you to proceed, as shown in Figure A.5. If it were a certificate from a certification authority your browser already trusts, the browser would not prompt you.

612

Appendix A  Installing Apache, PHP, and MySQL

Figure A.5  When using a self-signed certificate, your browser will prompt you to add an exception to ensure you trust it

Installing Apache, PHP, and MySQL for Windows and Mac OS X Using All-in-One Installation PackagesIf you have the appropriate development tools, you can install PHP, Apache, and MySQL from source on both Windows and Mac OS X systems. You can also manually install PHP, Apache, and MySQL packages individually, as described in the installation pages of the PHP manual at http://php.net/manual/en/install.php. However, for getting up and running quickly in a development environment, you can use a third-party installation package that offers an all-in-one installation solution.

Installing PEAR

613

A popular and well-maintained third-party installation package for Apache, MySQL, and PHP is XAMPP—the「X」indicates it is cross-platform, and in fact you can download for free an XAMPP package for Linux, Windows, or Mac OS X at https://www.apachefriends.org/download.html:

There are two other solid third-party installation packages for Apache, MySQL, and PHP that are specific to operating systems:

 ■ WAMP—Installation of Apache, MySQL, and PHP on Windows. See http://www

.wampserver.com/ for more information.

 ■ MAMP—Installation of Apache, MySQL, and PHP on Mac. See http://www.mamp.info/ 

for more information.

To set up PHP, Apache, and MySQL on your Windows or Mac OS X system, follow the instructions of the third-party installation package of your choice. It is very likely that you will encounter a one-click install process, or a simple wizard-based installation process that will lead you carefully through the steps for installation and configuration.

Testing Your WorkOnce you have finished using your third-party configuration and installation package, start your web server and test to ensure that PHP is working as intended. Create a test.php file and add the following line to it:

<?php phpinfo(); ?>

Make sure the file is in the document root directory (for example, on Windows this is typically C:\Program File\Apache Software Foundation\Apache2.4\htdocs); then open it in your browser, as follows:

http://localhost/test.php

or

http://your-ip-address-here/test.php

If you see a page similar to the one shown in Figure A.4, you know that PHP is working with Apache.

Installing PEARPEAR, the PHP Extension and Application Repository (PEAR), is a distribution system for reusable PHP components contributed by the PHP developer community. There are currently over 200 packages available for PHP 5+, all of which provide extended functionality to the base PHP installation.

To use PEAR, you must first ensure you have the PEAR package installer. This package installer will already exist and be available for use subsequent to a UNIX-based PHP installation, but to install the PEAR package installer on Windows, go to the command line and type :c:\php\go-pear.

614

Appendix A  Installing Apache, PHP, and MySQL

The go-pear script asks you a few straightforward questions about where you would like the package installer and the standard PEAR classes installed, then downloads and installs them for you. At this stage, you should have an installed version of the PEAR package installer and the basic PEAR libraries. You can then simply install packages by typing

pear install package

where package is the name of the package you want to install.

To get a list of available packages, type

pear list-all

To see what you have installed currently, try

pear list

If you want to check for newer versions of any installed packages, use

pear upgrade pkgname

If the preceding procedure does not work for you for whatever reason, we suggest you try downloading PEAR packages directly. To do this, go to http://pear.php.net/packages.php. From this location you can navigate through the various packages available until you find the one you need, at which time you can download and manually place the files in the PHP PEAR directory on your system.

Installing PHP with Other Web ServersAlthough using PHP with the Apache web server is almost a default configuration given how long the two technologies have been working together successfully (well over 15 years at this point), you can certainly set up PHP with several other web servers. For example, a configuration that has been rising in popularity recently is PHP with Nginx (http://nginx.org).  For detailed instructions regarding the installation of PHP on an Nginx server, please see the PHP manual at http://php.net/manual/en/install.unix.nginx.php.

Additional web server configuration instructions for UNIX systems are also available in the PHP manual at http://php.net/manual/en/install.unix.php.

Index

Symbols

[] (array element operator), 35- - (decrement operator), 30–31== (equal operator), 31–32$_POST array, 20$.ajax( ) method, 508–509$.get( ) method, 510$.getJSON( ) method, 510$.getscript( ) method, 510$.post( ) method, 510$this pointer, 164\ (backslash), escape sequences, 

125–126

^ (caret symbol), 121, (comma operator), 33@ (error suppression operator), 34`` (execution operator), 34–35/ (forward slash), 56, 120% (percent) symbol, printing, 110& (reference operator), 31; (semicolon), 16, 222–223( ) (parentheses), order of precedence, 

37–38

?: (ternary operator), 34| (vertical pipe), 123

616

absolute path

A

absolute path, 56abstract classes, 188access control implementing, 366–369access modifiers, 165, 166

visibility, controlling, 169–170

accessing

array contents, 77–79array elements, 79

with each( ) construct, 80–81with foreach loop, 80

form variables, 20–22

assignment operators, 20htmlspecialchars( ) function, 21–22

PHP, 12

accessor functions, 166–168, 178ACID (atomicity, consistency, isolation, 

and durability), 317–318

add_bms.php, 588–589addClass( ) method, 498adding

dynamic content, 18–19locks to files, 71–73

addition operator, 28address field (Bob’s Auto Parts order form), 

54

administrator privileges (MySQL), 229advantages of reusing code

consistency, 132cost, 132reliability, 132

aggregating SQL data, 259–261AJAX (Asynchronous JavaScript and XML), 

493–494

$.ajax( ) method, 508–509asynchronous requests, 493helper methods, 509–510

$.get( ), 510$.getscript( ), 510$.post( ), 510

real-time chat application, building 

chat server, 504–507

aliases

for namespaces, 198for tables, 257–258

ALTER TABLE command (SQL), 265–268altering

error reporting settings, 554–556tables after creation, 265–268

alternative control structure syntax, 51anchoring regular expressions to beginning 

or end of string, 123

anonymous functions, 155–157Apache

HTTP Server

.htaccess files, 374–377configuring, 356

installing

on UNIX, 600–602on Windows and Mac, 612–613

applying

functions to arrray elements, 97–98localization to web pages, 440–445

language selector page, 442–444

software engineering to web 

development, 530

templates to web pages, 134–139text to buttons, 461–464arbitrary lengths, reading, 69ARCHIVE table type, 316arguments, 39arithmetic operators, 28–29array elements, 76

accessing, 79

auto_append_file directive

617

with each( ) construct, 80–81with foreach loop, 80

applying functions to, 97–98counting, 98–99indices, 76

array key-value pairs for getdate( ) function, 

427–428

array operators, 35, 81–82array_count( ) function, 98–99array_multisort( ) function, 87–88array_pop( ) function, 92array_push( ) function, 92array_reverse( ) function, 92array_walk( ) function, 97–98arrays, 24, 75–76

$_POST, 20accessing contents, 77–78, 78–79bounding box contents, 463converting to scalar variables, 

99–100

initializing, 79loading from files, 92–96multidimensional arrays, 75, 82–85

sorting, 87–90three-dimensional arrays, 84–85two-dimensional arrays, 82–84

navigating, 96–97numerically indexed arrays, 76–77reordering, 90–91

with shuffle( ) function, 90–91

reversing, 92sorting, 85–87

with asort( ) function, 86–87with ksort( ) function, 86–87reverse sorting, 83with sort( ) function, 85–86

superglobal, 20, 27

asort( ) function, 86–87assertions, 126–127assigning values to variables, 24assignment operators, 20

combined assignment operators, 30values returned from, 29

associativity, 37–38asynchronous requests, 493atomic column values, 216–217attackers, 339attributes, 160, 162, 164–165, 177

access modifiers, 165, 166accessor functions, 166–168overriding, 170–172preventing, 172

authentication, 333

access control, 366–369basic authentication, 372–377

in PHP, 372–373

custom authentication, creating, 377identifying visitors, 365–366passwords

hash functions, 370–371storing, 369

PHPbookmark project, 569–587

changing passwords, 580–582logging in, 576–579logging out, 580registering users, 569–575resetting forgotten passwords, 

582–587

in session control, 483–491authmain.php, 483–489logout.php, 490–491members_only.php, 489

authmain.php, 483–489auto_append_file directive, 139–140

618

_autoload( ) function

_autoload( ) function, 189AUTO_INCREMENT keyword (MySQL), 234auto_prepend_file directive, 139–140autocommit mode (MySQL), 318automatically generated images, 456available extensions, identifying, 522–523avoiding FTP timeouts, 420

bookmark_fns.php, 567–568bookmarks (PHPbookmark project), 561

adding, 588–590deleting, 591–594displaying, 590–591

Book-O-Rama bookstore application, 

213–214

inserting information into database, 

B

backing up

files, 412–420MySQL databases, 310–311

backreferences, 126backtraces, 202balancing security with usability, 342bar chart, drawing, 465–474basename( ) function, 397basic authentication, 372–377

.htaccess files, 374–377in PHP, 372–373

basic values, filtering, 346–347basic_auth.php, 372–373Bill Gates Wealth Clock, 407bitwise operators, 33blank canvas, creating, 452–453BLOBs (binary large objects), 244blocks, declaring, 42Bob’s Auto Parts site

exception handling, 204–208order form

address field, 54creating, 12–14fields, naming, 14processing, 14totals, calculating, 36–37

282–285

results.php, 273–275schema, 221search form, 272–273

Boolean values, 24bottom-up approach to security, 343bounding box, 462–463branching, 123breaking up code, 535–536browsedir2.php, 392browsedir.php, 390browsers

cookies, 476, 477

session ID, storing, 477–478setting from PHP, 476–477

outputting images to, 455session control, 475

authentication, 483–491configuring, 482–483

sessions

creating, 480–482registering variables, 

478–479

starting, 478

browsing php.ini file, 355–356Bubbler, 510built-in functions, 144buttons

Smart Form Mail application, creating, 

applying text, 461–464

101–104

creating, 457–465

chat application

classes

619

base canvas, setting up, 460–461

outputting to browser, 465positioning text on, 464text, writing on, 464–465

C

calculating

dates

in MySQL, 434–435in PHP, 433–434

totals on order forms, 36–37

calendar functions, 436_call method, 188–189callable type, 24calling

class operations, 165functions, 19, 141–142

recursive functions, 154–155undefined functions, 142–143

canvas images

creating, 452–453printing text on, 453–454Cartesian product, 254–255case of strings, changing, 111–112case sensitivity, of identifiers, 239catch blocks, 200CHAR type columns, 235character class, 121–122character sets, 120–121, 438–440

multi-byte, 438security implications, 439–440single-byte, 438

characters. See also special characters, 

123–124

reading, 69

charts, drawing from stored MySQL data, 

465–474

chat server, building, 504–507user interface, building, 510–517

chat.php, 504–507checkdate( ) function, 428–429checking

for existence of files, 70length of strings, 115–116

choosing

development environment, 537–538file mode, 55keys, 217

chop( ) function, 104classes, 161

$this pointer, 164abstract classes, 188attributes, 162, 164–165, 177converting to strings, 194designing, 176–177Exception class, 201–202inheritance, 161–162, 168–169

late static bindings, 186–187multiple inheritance, 172–173preventing, 172

instantiating, 163–164namespaces, 195–197

global namespaces, 197–198importing, 198subnamespaces, 197

naming, 177ObjectIterator, 192operations, 162–163

calling, 165

polymorphism, 161structure of, 162–163traits, 174–176writing code for, 177–184

620

classes

accessor functions, 178metatags, 177

click event, 500Clifford, John, 510cloning objects, 187–188closedir( ) function, 391closing files, 63–65closures, 155–157code

breaking up, 535–536checking out, 537for classes, writing, 177–184

operations, 181commenting, 534debugging, 352–353indenting, 42, 534–535maintainability, 532optimizing, 540–541organizing, 350–351reusing, 133–134

advantages of, 131–132functions, 140–157in large web projects, 531–532require( ) statement, 134–139traits, 174–176

securing, 343

command execution, 353–354escaping output, 348–350filtering input data, 343–348

source code, highlighting, 525–526standards, 532

defining naming conventions, 

532–534

testing, 541–542

code blocks, 42columns, 211, 235–237

atomic column values, 216–217

data types, 240–246

date and time types, 243–244numeric types, 241–242string types, 244–246

displaying, 302indexes, creating, 238MySQL

CHAR type, 235VARCHAR type, 235–236

primary key, 211

columns_priv table, 296–298combined assignment operators, 30command line

executing scripts on, 526–527running PHP on, 526–527

commands

executing, 353–354MySQL

CREATE INDEX, 238CREATE TABLE, 232–233CREATE USER, 226DESCRIBE, 304EXPLAIN, 304–309GRANT, 226–227, 230–231REVOKE, 230, 230–231SHOW, 301–304show tables, 237use, 232mysql, 223SQL

ALTER TABLE, 265–268DELETE, 268INSERT, 248–249ORDER BY clause, 259SELECT, 250–251, 252–253UPDATE, 265

comments, 17–18comparing

conditionals, 45–46constants and variables, 26SQL and MySQL, 248strings, 115

comparison operators, 31–32

equal operator, 31–32for WHERE clause, 252–253

concatenating strings, 22conditionals, 41

code blocks, 42comparing, 45–46else statements, 42–43elseif statements, 43–44if statements, 41–42switch statement, 44–45

configuring

Apache HTTP Server, 356MySQL users, 225–232PHP image support, 449–450session control, 482–483

authentication, 483–491

connecting

to MySQL, 277–278to network services, interaction 

failures, 548–549

ODBC, 286constants, 26

error reporting levels, 553–554per-class constants, 185and variables, 26

constructors, 163consuming data from other websites, 

404–408

control structures

CREATE TABLE command

621

alternative syntax, 51conditionals, 41

code blocks, 42comparing, 45–46else statements, 42–43elseif statements, 43–44if statements, 41–42switch statement, 44–45

declare structure, 51–52repetition structures, 46–50

do.while loops, 50foreach loops, 49–50for loops, 49–50while loops, 47–48

stopping, 50for stored procedures, 323–327

declare handlers, 325controlling visibility, 169–170conversion specification, 109

type codes, 110–111

converting

arrays to scalar variables, 99–100classes to strings, 194dates and times to Unix timestamp, 426Gregorian to Julian calendar, 436between PHP and MySQL date 

formats, 431–433

cookies, 476, 477session ID, 476setting from PHP, 476–477

correlated subqueries, 264count( ) function, 93, 98–99counted subexpressions, 123counting array elements, 98–99crackers, 339CREATE INDEX command, 238CREATE TABLE command, 232–233

622

CREATE USER command

CREATE USER command, 226creating

Bob’s Auto Parts order form, 12–14buttons

base canvas, setting up, 460–461outputting to browser, 465text, applying, 461–464text, positioning, 464

column indexes, 238directories, 394files, 398HTML elements, 497–498images, 451–455

make_button.php, 458–460

MySQL tables, 232–234MySQL users, 224sessions, 480–482

cross joins, 258crypt( ) function, 370CSV table type, 316current( ) function, 96–97cursors, 323, 325custom authentication, creating, 377customer feedback form (Bob’s Auto 

Parts site), creating, 101–104

customer order formaddress field, 54creating, 12–14fields, naming, 14processing, 14totals, calculating, 36–37

D

data hiding, 160data storage, RDBMSs, 74data types, 24–25

for MySQL columns, 240–246

date and time types, 243–244

numeric types, 241–242string types, 244–246

scalar values, 26type casting, 25type strength, 25

databases. See also RDBMSs (relational 

database management systems)

advantages of, 209designing, 213–220dropping, 268–269MySQL, 209

backing up, 310–311chat server, building, 504–507DATE_FORMAT( ) function, 431–432dates, calculating, 434–435displaying, 302inserting data, 282–285interaction failures, 547–548restoring, 311security, 299–301UNIX_TIMESTAMP( ) function, 

432–433

users, setting up, 225–232

null values, 217–218ODBC, 286optimizing, 309–310

design optimization, 309table optimization, 310

PHPbookmark project, implementing, 

565–566

querying, 278RDBMSs, 74replication, 311–313

initial data transfer, performing, 

313

master, setting up, 312–313slaves, setting up, 313

schemas, 212

DMZs (demilitarized zones)

623

security, 357–359transactions, 317–319update anomalies, 215web database architecture, 218–220, 272

Date, C.J., 220date and time type columns, 243–244date( ) function, 18, 19–20, 424–427

format codes, 424–425Unix timestamps, 426–427

DATE_FORMAT( ) function, 431–432dates

calculating

in MySQL, 434–435in PHP, 433–434

calendar functions, 436converting between PHP and MySQL 

formats, 431–433

Gregorian dates, 436Julian dates, 436validating with checkdate( ) function, 

428–429

db table, 295–296DDL (Data Definition Language), 248debugging, 352–353variables, 551–553declare handlers, 325declare structure, 51–52declaring

blocks, 42constants, 26functions, 144

decrement operators, 30–31define( ) function, 26defining naming conventions for large 

projects, 532–534

DELETE command (SQL), 268delete_bms.php, 592–593

deleting

bookmarks, 591–594files, 70, 398records from database, 268

deletion anomalies, 215delimiters, 120denial of service, 335–337, 361descenders, 463DESCRIBE command, 304designing

classes, 176–177RDBMSs, 213–220

destroying

image identifiers, 455sessions, 479destructors, 163die( ) function, 520–522directories

creating, 394reading from, 390–393retrieving information, 394submission form, 408

directory structure for large projects, 536directory_submit.php, 409–412disaster planning, 362–364disconnecting from MySQL database, 281disgruntled employees, threats 

posed by, 339

displaying

bookmarks, 590–591columns, 302databases, 302MySQL privileges, 302tables, 237

division operator, 28DML (Data Manipulation Language), 248DMZs (demilitarized zones), 360–361

624

documentation

documentation

function libraries, 536PHP manual, 531project documentation, 538

dot notation, 255double-quoted strings, interpolation, 22do.while loops, 50drawing bar charts, 465–474dropping

databases, 268–269tables, 268

DSN (data source name), 288dump_array( ) function, 552–553dump_variables.php, 551–553dynamic content, adding, 18–19

E

each( ) construct, accessing array contents, 

80–81

each( ) function, 80echo statement, 22else statements, 42–43elseif statements, 43–44email, sending and reading, 404embedding PHP in HTML, 14–19

comments, 17–18statements, 16tags, 16whitespace, 17

empty( ) function, 40encapsulation, 160end( ) function, 96–97environment variables, 401–402equal operator, 31–32equi-joins, 258error handling, 208

error reporting levels, 553–554logging errors, 560

graceful error logging, 557–559

logic errors, 549–551opening files, 58–61programming errors, 543–551runtime errors, 544–549

causes of, 545–549syntax errors, 543–544triggering your own errors, 556

error messages for undefined functions, 

142–143

error reporting levels, 553–554error reporting settings, altering, 554–556error suppression operator, 34, 60escape sequences, 125–126escapeshellcmd( ) function, 354escaping

from HTML, 16output, 348–350

eval( ) function, 519–520evaluating

SELECT queries, 304–309strings, 519–520

event handling

jQuery, 499–504

click event, 500focusout event, 503on( ) method, 499–500ready event, 499submit event, 504

triggers, 327–329

Exception class, 201–202exception handling, 199–201, 557

in Bob’s Auto Parts site, 204–208catch blocks, 200Exception class, 201–202

files

625

finally blocks, 200throw keyword, 200try blocks, 199user-defined exceptions, 202–204

executing commands, 353–354execution directives, 51–52execution operator, 34–35existence of files, checking for, 70exit( ) function, 520–522EXPLAIN command, 304–309explode( ) function, 95–96

splitting strings with, 112–113

extensions

loaded extensions, identifying, 522–523PDO data access abstraction extension, 

286–289

php_gd2.dll extension, registering, 450

extract( ) function, 99–100

Ffclose( ) function, 63–65feedback form (Bob’s Auto Parts site), 

creating, 101–104

feof( ) function, 66–67fgetc( ) function, 69fgetcsv( ) function, 67–68fgets( ) function, 67–68fgetts( ) function, 67–68fields, naming, 14file formats, 62–63file( ) function, 68–69, 93file mode, 55

choosing, 55fopen( ) function, 57

file systems

absolute path, 56file information, retrieving, 395–397

relative path, 56security, 352

file_exists( ) function, 70file_get_contents( ) function, 68–69file_put_contents( ) function, 61fileatime( ) function, 397filedetails.php, 395–396fileowner( ) function, 397fileperms( ) function, 397files

.htaccess files, 374–377backing up, 412–420characters, reading, 69closing, 63–65creating, 398deleting, 70, 398existence of, checking for, 70flat files, 53–54

problems with, 73

image files

creating, 451–455GIFs, 451JPEGs, 450PNGs, 450–451

loading arrays from, 92–96locking, 71–73logging errors to, 560moving, 398navigating inside, 70–71opening, 55

error handling, 58–61with fopen( ) function, 56–58through FTP or HTTP, 58

in PHPbookmark application, 564–565processing, 55properties, changing, 397–398reading from, 55, 65–66, 67–68, 68–69

626

files

as cause for runtime errors, 546–547line-by-line, 67–68

fonts, TrueType, 457fopen( ) function, 55, 66

require( ) statement, 132–134size of, determining, 70uploading, 379–389, 420HTML form, 381–382php.ini settings, 380–381tracking upload progress, 387–388troubleshooting, 389writing the file handling script, 

382–387

writing to, 55, 61

filesize( ) function, 70, 397filtering

input data, 276, 343–348basic values, 346–347double-checking expected values, 

344–346

strings, 347–348

strings, 105–107

for output to browser, 105–106for output to email, 106–107

final keyword, 172finally blocks, 200finding

non-matching rows, 256–257strings within strings, 116–117substrings with regular expressions, 

128–129firewalls, 360flat files, 53–54

problems with, 73

float data type, 25floating-point types, 242floatval( ) function, 41flock( ) function, 71–73focusout event, 503

file mode, 57opening files with, 56–58parameters, 56

foreach loops, 49–50, 190

accessing array elements, 80

FOREIGN KEY keyword (MySQL), 235foreign keys, 212, 319

Book-O-Rama bookstore application, 

221

forgot_passwd.php, 583–584format codes, date( ) function, 424–425formattingstrings

changing case of, 111–112conversion specification, 109for printing, 109–111

timestamps, 429–431

forms

Book-O-Rama bookstore application

HTML form, 282–285search form, 272–273

customer order form

creating, 12–14fields, naming, 14processing, 14

Smart Form Mail application

creating, 101–104regular expressions, 127–128

submission form, 408variables, accessing, 20–22

fpassthru( ) function, 68–69fputs( ) function, 61fread( ) function, 69front end interface, building for chat 

application, 504–507

functions

627

fseek( ) function, 70–71ftell( ) function, 70–71FTP

avoiding timeouts, 420backing up files with, 412–420files, opening, 58

ftp_mirror.php, 413–416ftp_nlist( ) function, 421ftp_size( ) function, 420full joins, 254–255func_num_args( ) function, 148functions, 140

_autoload( ), 189_get( ), 166–168_set( ), 166–168accessor functions, 166–168, 178aggregate functions (MySQL), 259–261applying to array elements, 97–98arguments, 39array_count( ), 98–99array_multisort( ), 87–88array_pop( ), 92array_push( ), 92array_reverse( ), 92array_walk( ), 97–98asort( ), 86–87backtraces, 202basename( ), 397built-in, 144calling, 19, 141–142case functions, 112case sensitivity, 143checkdate( ), 428–429chop( ), 104closedir( ), 391closures, 155–157count( ), 93, 98–99

crypt( ), 370current( ), 96–97date( ), 18, 19–20, 424–427format codes, 424–425DATE_FORMAT( ), 431–432define( ), 26die( ), 520–522dump_array( ), 552–553each( ), 80empty( ), 40end( ), 96–97escapeshellcmd( ), 354eval( ), 519–520exit( ), 520–522explode( ), 95–96

splitting strings with, 112–113

extract( ), 99–100fclose( ), 63–65feof( ), 66–67fgetc( ), 69fgetcsv( ), 67–68fgets( ), 67–68fgetts( ), 67–68file( ), 68–69, 93file_exists( ), 70file_get_contents( ), 68–69file_put_contents( ), 61fileatime( ), 397fileowner( ), 397fileperms( ), 397filesize( ), 70, 397floatval( ), 41flock( ), 71–73fopen( ), 55, 66

file mode, 57opening files with, 56–58parameters, 56

628

functions

fpassthru( ), 68–69fputs( ), 61fread( ), 69fseek( ), 70–71ftell( ), 70–71ftp_nlist( ), 421ftp_size( ), 420func_num_args( ), 148fwrite( ), 61

parameters, 62

get_loaded_extensions( ), 523getdate( ), 427–428

array key-value pairs, 427–428

getenv( ), 401–402getlastmod( ), 524gettext( ), 444–448gettype( ), 39header( ), 455highlight_string( ), 525htmlspecialchars( ), 21–22, 105–106imagecolorallocate( ), 453imagecreatetruecolor( ), 452–453imagecreatfrompng( ), 461imagefill( ), 453–454imagefilledrectangle( ), 472imageline( ), 472imagestring( ), 454imagettftext( ), 462implode( ), 113ini_get( ), 524–525ini_set( ), 524intval( ), 41isset( ), 40, 152join( ), 113krsort( ), 83ksort( ), 86–87libraries, 536

lookup functions, 408–412ltrim( ), 104mail( ), 104, 404microtime( ), 435mkdir( ), 394mktime( ), 426–427multibyte string functions, 440mysqli( ), 547namespaces, 195–197

global namespaces, 197–198importing, 198subnamespaces, 197

naming, 145–146next( ), 96–97nl2br( ), 70, 107–109nonexistent, as cause for runtime errors, 

545–546

number_format( ), 37in ObjectIterator class, 192opendir( ), 391overloading, 145parameters, 146–148

passing, 141passing by reference, 150–151

passthru( ), 399phpinfo( ), 26, 141pollServer( ), 515–516pos( ), 96–97preg_match( ), 128–129preg_split( ), 129–130prev( ), 96–97printf( ), 109–111program execution, 398–401prototype, 141–142putenv( ), 401–402range( ), 77readdir( ), 391

readfile( ), 68–69recursive, 154–155reset( ), 96–97return keyword, 152–153returning values from, 153rewind( ), 70–71rmdir( ), 394rsort( ), 83scope, 148–150serialize( ), 521session_start( ), 478set_error_handler( ), 557–558setcookie( ), 476settype( ), 39show_source( ), 525shuffle( ), 90–91sizeof( ), 98–99sort( ), 76, 85–86sprintf( ), 109str_replace( ), 107, 118–119strcasecmp( ), 115strchr( ), 117strcmp( ), 115strftime( ), 429–431stristr( ), 117strnatcmp( ), 115strpos( ), 117–118strstr( ), 116–117strtok( ), 113–114strtolower( ), 112strtoupper( ), 112structure of, 144–145strval( ), 41substr( ), 114system( ), 399trigger_error( ), 556trim( ), 104

GIF (Graphics Interchange Format) files

629

uasort( ), 89ucfirst( ), 112ucwords( ), 112uksort( ), 89umask( ), 394undefined functions, calling, 142–143UNIX_TIMESTAMP( ), 432–433unlink( ), 70unserialize( ), 521urlencode( ), 407user-defined, 144usort( ), 88–89variable functions, 146variable handling functions, 39–40vprintf( ), 111vsprintf( ), 111

fwrite( ) function, 61

parameters, 62

GGD2 image library, 449generating

bar charts from stored MySQL data, 

465–474

charts from stored MySQL data, 

465–474

generators, 192–193_get( ) function, 166–168get_loaded_extensions( ) function, 523getdate( ) function, 427–428

array key-value pairs, 427–428

getenv( ) function, 401–402getlastmod( ) function, 524gettext( ) function, 444–448, 446gettype( ) function, 39GIF (Graphics Interchange Format) 

files, 451

630

Git

Git, 537global keyword, 150global namespaces, 197–198GNU gettext

installing, 444–445translation files, 445–447

graceful error logging, 557–559GRANT command, 226–227, 230–231grant tables, 291–299

columns_priv table, 296–298connection verification, 298db table, 295–296procs_priv table, 296–298request verification, 298tables_priv table, 296–298user table, 293–295Greenspun, Philip, 407Gregorian dates, 436grouping SQL data, 259–261

H

handle.php, 558handles, 161hash functions, 370–371header( ) function, 455headers, 438–439

locale-specific, 441–442helper methods, 509–510

$.get( ), 510$.getJSON( ), 510$.getscript( ), 510$.post( ), 510

heredoc syntax, 23highlight_string( ) function, 525highlighting source code, 525–526hosting providers, 599–600

HTML

Book-O-Rama form, 282–285elements

creating, 497–498selecting with jQuery selectors, 

496–497escaping, 16file upload form, 381–382PHP, embedding, 14–19, 16

comments, 17–18statements, 16whitespace, 17

reusing, applying templates to web 

pages, 134–139

submission form, 408

htmlspecialchars( ) function, 21–22, 

105–106

HTTP files, opening, 58

I

identifiers, 23–24, 239–240

case sensitivity, 239rules, 239

identifying script owner, 523IETF (Internet Engineering Task Force), 404if statements, 41–42image identifiers, destroying, 455imagecolorallocate( ) function, 453imagecreatetruecolor( ) function, 

452–453

imagecreatfrompng( ) function, 461imagefill( ) function, 453–454imagefilledrectangle( ) function, 472imageline( ) function, 472ImageMagick image library, 449images

automatically generated, 456

interfaces

631

bar chart, drawing from stored SQL 

data, 465–474

buttons

creating, 457–465outputting to browser, 465positioning text on, 464text, applying, 461–464writing text on, 464–465

canvas images

creating, 452–453printing text on, 453–454

creating, 451–455

make_button.php, 458–460

GIFs, 451JPEGs, 450libraries, 449outputting to browser, 455php_gd2.dll extension, registering, 450PNGs, 450–451simplegraph.php, 451–452support in PHP, configuring, 449–450

imagestring( ) function, 454imagettftext( ) function, 462IMAP4 (Internet Message Access protocol), 

404

implode( ) function, 113importing namespaces, 198increment operators, 30–31indenting code, 42indexes, creating, 310indices, 76

numerically indexed arrays, 76–77

inheritance, 161–162, 168–169late static bindings, 186–187multiple inheritance, 172–173overriding, 170–172preventing, 172

ini_get( ) function, 524–525ini_set( ) function, 524initializing arrays, 79

numerically indexed arrays, 76–77

inner joins, 258InnoDB table type, 316

transactions, 318–319

input data, filtering, 343–348

basic values, 346–347double-checking expected values, 

344–346

strings, 347–348

INSERT command (SQL), 248–249inserting data into SQL database, 248–250, 

282–285

insertion anomalies, 215installing

Apache

on UNIX, 600–602on Windows and Mac, 612–613

GNU gettext, 444–445MySQL on UNIX, 602–605PEAR, 613–614PHP

with other web servers, 614on UNIX, 605–609on Windows and Mac, 612–613

instanceof operator, 35, 185–186instantiating classes, 163–164integers, 25integral data types, 241interacting with the environment, 401–402interfaces, 173–174

Book-O-Rama HTML form, 282–285Iterator, 190–191PDO data access abstraction extension, 

286–289

632

internationalization

internationalization, 437–438

applying to web pages, 440–445

language selector page, 442–444locale-specific headers, 441–442

gettext( ) function, 444–448

GNU gettext, installing, 444–445translation files, 445–447

interpolation, 22intval( ) function, 41isset( ) function, 40, 152iteration, 46–50, 190–192

accessing array contents, 78–79do.while loops, 50foreach loops, 49–50for loops, 49–50while loops, 47–48

Iterator interface, 190–191

$.getJSON( ), 510$.getscript( ), 510$.post( ), 510events, 499–504

click event, 500focusout, 503on( ) method, 499–500ready event, 499submit, 504namespace, 495pseudo-selectors, 497selectors, 495–498acting on, 498syntax, 496–497

selectors (jQuery), creating HTML 

elements, 497–498

val( ) method, 498in web applications, 494–495

J

Julian dates, 436

JavaScript. See also AJAX; jQuery

AJAX, 493–494join( ) function, 113joining strings, 113joins

cross joins, 258equi-joins, 258full joins, 254–255inner joins, 258joining more than two tables, 255–256left joins, 256–257

JPEG (Joint Photographic Experts Group) 

files, 450

jQuery, 494–504

$.ajax( ) method, 508–509addClass( ) method, 498AJAX helper methods, 509–510

$.get( ), 510

K

keys, 76, 211–212

Book-O-Rama bookstore application, 

221

choosing, 217foreign keys, 212, 319success, 507

keywords

clone, 187–188final, 172global, 150MySQL

AUTO_INCREMENT, 234FOREIGN KEY, 235NOT NULL, 234PRIMARY KEY, 234–235

return, 152–153

login.php

633

static, 185throw, 200trait, 174–176yield, 192–193

krsort( ) function, 83ksort( ) function, 86–87

L

languages

headers, 438–439multi-byte, 438single-byte, 438

large web application projects, 529

choosing a development environment, 

537–538

coding standards, 532

breaking up code, 535–536commenting your code, 534defining naming conventions, 

532–534

indenting, 534–535directory structure, 536documenting, 538function libraries, 536optimizing code, 540–541prototyping, 538–539reusing code, 531–532separating logic from content, 539–540testing code, 541–542version control, 536–537writing maintainable code, 532

late static bindings, 186–187left joins, 256–257length of strings, checking, 115–116libraries

function libraries, 536image libraries, 449jQuery library, loading, 494–495

LIMIT clause (SELECT command), 261–262line-by-line reading from files, 67–68linking tables, 218list( ) construct, 81list_functions.php, 522–523literals, 23LOAD DATA INFILE statement, 315loaded extensions, identifying, 522–523loading

arrays from files, 92–96files with require( ) statement, 132–134jQuery library, 494–495

local variables, 323locales, 438localization, 437–438

applying to web pages, 440–445

language selector page, 442–444

character sets, 438–440

multi-byte, 438security implications, 439–440single-byte, 438

gettext( ) function, 444–448

GNU gettext, installing, 444–445translation files, 445–447

headers, 438–439

locale-specific, 441–442

locales, 438multibyte string functions, 440

locking files, 71–73logging errors

graceful error logging, 557–559to log file, 560

logging in to MySQL, 223–224logic, separating from content, 539–540logic errors, 549–551logical operators, 32–33login.php, 566–567

634

logout.php

logout.php, 490–491lookup functions, 408–412lookup.php, 405for loops, 49–50loops

accessing array contents, 78–79do.while loops, 50foreach loops, 49–50, 190for loops, 49–50while loops, 47–48

ltrim( ) function, 104

M

Mac OS, installation packages, 612–613mail( ) function, 104, 404maintainability of code, 532make_button.php, 458–460many-to-many relationships, 213master, setting up for replication, 312–313matching

special characters, 123–124substrings with string functions, 116

max_execution_time directive, 524member.php, 576–577members_only.php, 489MEMORY table type, 316Mercurial, 537MERGE table type, 316meta characters, 124–125metatags, 177on( ) method, 499–500methods

$.ajax( ), 508–509AJAX helper methods, 509–510

$.get( ), 510$.getJSON( ), 510

$.getscript( ), 510$.post( ), 510

in Exception class, 201–202jQuery

on( ), 499–500addClass( ), 498val( ), 498

overloading, 188–189static, 185

microseconds, 435microtime( ) function, 435mirroring files, 412–420mkdir( ) function, 394mktime( ) function, 426–427modification anomalies, 215modification date of scripts, obtaining, 

523–524

modulus operator, 28monitoring security, 342–343moving files, 398multibyte string functions, 440multidimensional arrays, 75, 82–85

sorting, 87–90

with array_multisort( ) function, 

87–88

reverse sorting, 89–90user-defined sorts, 88–89

three-dimensional arrays, 84–85two-dimensional arrays, 82–84

multiline comments, 17multiple inheritance, 172–173multiplication operator, 28MyISAM storage engine, 316MySQL, 209, 221–222. See also MySQL 

monitor

aggregating data, 259–261autocommit mode, 318

MySQL

635

chat server, building, 504–507columns

data types, 240–246date and time types, 243–244indexes, creating, 238numeric types, 241–242string types, 244–246

commands

AUTO_INCREMENT keyword, 234CREATE USER, 226DESCRIBE, 304EXPLAIN, 304–309FOREIGN KEY keyword, 235GRANT, 226–227, 230–231mysql, 223NOT NULL keyword, 234PRIMARY KEY keyword, 234–235REVOKE, 230–231SHOW, 301–304SHOW command, 303–304

databases

backing up, 310–311creating, 224restoring, 311selecting, 232

date format, converting to PHP, 

431–433

DATE_FORMAT( ) function, 431–432dates, calculating, 434–435drawing charts from stored data, 

465–474

identifiers, 239–240

case sensitivity, 239rules, 239

installing

on UNIX, 602–605on Windows and Mac, 612–613

joins

cross joins, 258equi-joins, 258full joins, 254–255inner joins, 258joining more than two tables, 

255–256

left joins, 256–257

logging in, 223–224optimizing databases, 309–310

design optimization, 309table optimization, 310

privileges, 291–299

columns_priv table, 296–298db table, 295–296displaying, 302procs_priv table, 296–298tables_priv table, 296–298updating, 299user table, 293–295

querying from the Web, 275–281

disconnecting from database, 281filtering input data, 276prepared statements, 279–280retrieving the results, 280–281selecting the database, 278setting up connection, 277–278

runtime errors, 547–548security, 299–301

passwords, 300web issues, 301

stored procedures, 320–327

control structures, 323–327cursors, 323, 325declare handlers, 325example of, 320–323local variables, 323

636 MySQL

tables

aliases, 257–258altering after creation, 265–268columns, 235–237creating, 232–234dropping, 268viewing, 237–238

UNIX_TIMESTAMP( ) function, 432–433user privileges, 300–301users, 225–232

creating, 224principle of least privilege, 225privileges, 225–231, 227–230web access, 231–232

mysql command, 223MySQL monitor, 222–223mysqli( ) function, 547mysqli library, 277

prepared statements, 279–280

Nnamespaces, 195–197

aliasing, 198global namespaces, 197–198importing, 198jQuery, 495subnamespaces, 197

naming

classes, 177fields, 14functions, 145–146tables, 257–258

navigating

within arrays, 96–97inside files, 70–71

network security, 360–361

denial of service attacks, 361

DMZ, 360–361firewalls, 360

network services, interaction failures, 

548–549

next( ) function, 96–97Nginx servers, 614nl2br( ) function, 70, 107–109nonexistent functions, as cause for runtime 

errors, 545–546

non-matching rows, finding, 256–257NOT NULL keyword (MySQL), 234NOT operator, 32–33NULL type, 24null values, 217–218number_format( ) function, 37numeric type columns, 241–242

floating-point types, 242integral data types, 241

numerically indexed arrays, 76–77

OObjectIterator class, 192objects, 24, 160, 161

classes, 161cloning, 187–188instantiating a class, 163–164interfaces, 160, 173–174serializing, 521

ODBC (Open Database Connectivity), 286one-to-many relationships, 213one-to-one relationships, 213one-way hash functions, 370OO (object-oriented) development, 159

_autoload( ) function, 189accessor functions, 166–168attributes, 160

overriding, 170–172

operators

637

classes, 161

abstract classes, 188attributes, 162, 164–165, 177constructors, 163converting to strings, 194designing, 176–177destructors, 163Exception class, 201–202instantiating, 163–164ObjectIterator, 192operations, 162–163structure of, 162–163writing code for, 177–184

encapsulation, 160generators, 192–193inheritance, 161–162, 168–169

multiple inheritance, 172–173preventing, 172

instanceof operator, 185–186interfaces, 173–174

Iterator, 190–191

iteration, 190–192late static bindings, 186–187namespaces, 195–197

global namespaces, 197–198importing, 198subnamespaces, 197

objects, 160, 161

cloning, 187–188serializing, 521

operations, 160calling, 165

per-class constants, 185polymorphism, 161reflection API, 194–195static methods, 185traits, 174–176type hinting, 185–186

opendir( ) function, 391opening files, 55

error handling, 58–61with fopen( ) function, 56–58through FTP or HTTP, 58

operands, 28operating system, securing, 361–362operations, 160, 162–163, 181

calling, 165constructors, 163destructors, 163overriding, 170–172preventing, 172

AND operator, 32–33OR operator, 32–33operators, 28

arithmetic operators, 28–29array operators, 35, 81–82assignment operators, 20, 29–31

combined assignment operators, 30values returned from, 29

associativity, 37–38bitwise operators, 33comparison operators, 31–32

equal operator, 31–32

decrement operators, 30–31error suppression operator, 34, 60execution operator, 34–35increment operators, 30–31instanceof, 185–186logical operators, 32–33precedence, 37–38reference operator, 31string concatenation operator, 22string operators, 29for subqueries, 263ternary operator, 34type operator, 35

638

optimizing

optimizing

code, 540–541databases, 309–310

design optimization, 309table optimization, 310

options for session configuration, 482–483ORDER BY clause, 259order forms

address field, 54creating, 12–14fields, naming, 14processing, 14storing and retrieving orders, 54strings, 115totals, calculating, 36–37

organizing code, 350–351outputting

buttons to browser, 465images, 455

overloading methods, 188–189overriding, 170–172preventing, 172

owner of scripts, identifying, 523

Pparameters, 146–148

extract( ) function, 100fopen( ) function, 56fwrite( ) function, 62htmlspecialchars( ) function, 105–106passing, 141

parser errors, 543–544passing by reference, 150–151passing by value, 150–151passing parameters, 141passthru( ) function, 399

passwords, 369–371

hash functions, 370–371MySQL, 300storing, 369

pattern matching, delimiters, 120PEAR (PHP Extension and Application 

Repository), installing, 613–614

per-class constants, 185performance, optimizing databases

design optimization, 309table optimization, 310

permissions, 59PHP

accessing, 12basic authentication, 372–373dates, calculating, 433–434embedding in HTML, 14–19

comments, 17–18tags, 16whitespace, 17

English language manual, 531environment information, 

 obtaining, 522

installing

with other web servers, 614on UNIX, 605–609on Windows and Mac, 612–613

statements, 16tags

short style, 16XML style, 16PHP interpreter, 600php_gd2.dll extension, registering, 450PHPbookmark project, 561add_bms.php, 588–589basic site, implementing, 566–569bookmark_fns.php, 567–568

privileges (MySQL)

639

bookmarks

adding, 588–590deleting, 591–594displaying, 590–591

database, implementing, 565–566delete_bms.php, 592–593files, 564–565forgot_passwd.php, 583–584implementing recommendations, 

594–597

login.php, 566–567member.php, 576–577recommend.php, 595–597register_form.php, 569–570register_new.php, 570–572solution components, 561–565user authentication, 569–587

changing passwords, 580–582logging in, 576–579logging out, 580registering users, 569–575resetting forgotten passwords, 

582–587

phpinfo( ) function, 26, 141php.ini file

browsing, 355–356date.timezone setting, 424file upload settings, 380–381session upload progress configuration 

settings, 387

planning web application projects, 

530–531

PNG (Portable Network Graphics) files, 

450–451

PO (Portable Object) files, 445–446Poedit, 446pollServer( ) function, 515–516polymorphism, 161

POP (Post Office Protocol), 404pos( ) function, 96–97position of substrings, identifying, 117–118positioning text on buttons, 464POSIX-style regular expressions, 119precedence, 37–38preg_match( ) function, 128–129preg_split( ) function, 129–130prepared statements, 279–280Pressman, Roger, 542prev( ) function, 96–97preventing inheritance, 172primary key, 211PRIMARY KEY keyword (MySQL), 234–235primary keys, Book-O-Rama bookstore 

application, 221

principle of least privilege, 225printf( ) function, 109–111printing

echo statement, 22formatting strings for, 109–111percent symbol, 110text on canvas images, 453–454

private access modifier, 166

visibility, controlling, 169–170

privileges (MySQL), 225–231, 227–230, 

291–299, 300–301

administrator privileges, 229columns_priv table, 296–298CREATE USER command, 226db table, 295–296displaying, 302GRANT command, 226–227principle of least privilege, 225procs_priv table, 296–298revoking, 230special privileges, 230

640

privileges (MySQL)

tables_priv table, 296–298updating, 299user privileges, 228user table, 293–295

processfeedback_v2.php, 108–109processing

customer order form, 14files, 55

processorder.php, 14–19

creating, 14dynamic content, adding, 18–19with exception handling, 205–208form variables, accessing, 20–22functions, calling, 19

procs_priv table, 296–298progex.php, 400–401program execution functions, 398–401programming errors, 543–551

logic errors, 549–551runtime errors, 544–549

causes of, 545–549syntax errors, 543–544

properties of files, changing, 397–398protected access modifier, 166protecting multiple web pages, 371protocols, 403–404prototype, 141–142prototyping web applications, 538–539pseudo-selectors, 497public access modifier, 166

visibility, controlling, 169–170

putenv( ) function, 401–402

Q

querying databases

SELECT queries, evaluating, 304–309subqueries, 262–263

correlated subqueries, 264operators, 263row subqueries, 264as temporary table, 264

from the Web, 275–281

disconnecting from database, 281filtering input data, 276prepared statements, 279–280retrieving the results, 280–281selecting the database, 278setting up connection, 277–278

R

range( ) function, 77RDBMSs (relational database management 

systems), 74

atomic column values, 216–217columns, 211design principles, 213–220keys, 211–212

choosing, 217

MySQL

databases, creating, 224databases, selecting, 232logging in, 223–224mysql command, 223privileges, 225–231tables, creating, 232–234users, creating, 224

null values, 217–218relationships, 213rows, 211schemas, 212tables, 210, 218update anomalies, 215values, 211

readdir( ) function, 391readfile( ) function, 68–69

results.php

641

reading

arbitrary lengths, 69characters, 69email, 404from files, 55, 65–66, 67–68, 68–69

as cause for runtime errors, 546–547line-by-line, 67–68

form directories, 390–393

ready event, 499real-time chat application, chat server, 

building, 504–507

recommend.php, 595–597records

deleting, 268storing, 62updating, 265

recursive functions, 154–155reducing web application security risks

access to sensitive data, 332–333denial of service, 336–337loss of data, 334–335malicious code injection, 337

reference operator, 31reflection API, 194–195register_form.php, 569–570register_new.php, 570–572registering

php_gd2.dll extension, 450session variables, 478–479regular expressions, 119–130

anchoring to beginning or end 

of string, 123

assertions, 126–127backreferences, 126branching, 123character class, 121–122character sets, 120–121counted subexpressions, 123

delimiters, 120escape sequences, 125–126meta characters, 124–125POSIX, 119repetition, 122in Smart Form Mail application, 

127–128

special characters, matching, 123–124strings, splitting, 129–130substrings, finding, 128–129substrings, replacing, 129

relationships, 213relative path, 56reordering arrays, 90–91

with shuffle( ) function, 90–91

repetition in regular expressions, 122repetition structures, 46–50

accessing array contents, 78–79do.while loops, 50foreach loops, 49–50for loops, 49–50while loops, 47–48

replacing substrings

with regular expressions, 129with string functions, 116

replication, 311–313

initial data transfer, performing, 313master, setting up, 312–313slaves, setting up, 313

repudiation, 338–339require( ) statement, 132–134

adding templates to web pages, 134–139

reset( ) function, 96–97resource type, 24restoring MySQL databases, 311results.php, 273–275

querying from the Web, filtering input 

data, 276

642

retrieving data from SQL databases

retrieving data from SQL databases, 

require( ) statement, 132–134

250–259

criteria, specifying, 251–253joining more than two tables, 255–256from multiple tables, 253–258

finding rows that don’t match, 

256–257

full joins, 254–255ORDER BY clause, 259SELECT command, 250–251

return keyword, 152–153returning values from functions, 153reusing code

advantages of, 131–132

consistency, 132cost, 132reliability, 132

functions, 140

built-in functions, 144calling, 141–142case sensitivity, 143closures, 155–157naming, 145–146parameters, 146–148parameters, passing, 141prototype, 141–142recursive functions, 154–155return keyword, 152–153returning values from, 153scope, 148–150structure of, 144–145undefined functions, calling, 

142–143

user-defined, 144variable functions, 146

in large web projects, 531–532maintainability, 532

applying templates to web pages, 

134–139

traits, 174–176

reverse sorting functions, 83, 89–90reversing arrays, 92REVOKE command, 230, 230–231rewind( ) function, 70–71RFCs (Requests for Comments), 404rmdir( ) function, 394row subqueries, 264rows, 211

inserting into SQL database, 248–250non-matching rows, finding, 256–257

rsort( ) function, 83rules

for identifiers, 239of variable scope, 27

running PHP on command line, 526–527runtime environment, temporarily 

modifying, 524–525

runtime errors, 544–549

causes of, 545–549

calls to nonexistent functions, 

545–546

connections to network services, 

548–549

failure to check input data, 549interaction with MySQL, 547–548reading or writing files, 546–547

S

SaaS version control systems, 537scalar values, 26scalar variables, creating from arrays, 

99–100

scandir.php, 393schemas, 212

security

643

scope, 27, 148–150<script> tag, 494–495scripts

add_bms.php, 588–589adding locks to, 71–73authmain.php, 483–489basic_auth.php, 372–373bookmark_fns.php, 567–568browsedir2.php, 392browsedir.php, 390chat.php, 504–507delete_bms.php, 592–593directory_submit.php, 409–412dump_variables.php, 551–553executing on command line, 526–527filedetails.php, 395–396forgot_passwd.php, 583–584ftp_mirror.php, 413–416functions, calling, 19handle.php, 558list_functions.php, 522–523login.php, 566–567logout.php, 490–491lookup.php, 405make_button.php, 458–460member.php, 576–577members_only.php, 489modification date, obtaining, 523–524owner, identifying, 523processfeedback_v2.php, 108–109processfeedback.php, 101–104processorder.php

creating, 14dynamic content, adding, 18–19with exception handling, 205–208

progex.php, 400–401recommend.php, 595–597

register_form.php, 569–570register_new.php, 570–572results.php, 273–275scandir.php, 393secret.php, 369show poll.php, 468–474simplegraph.php, 451–452stopping, 50terminating, 520–522upload.php, 382–387vieworders.php, 65–66

search form (Book-0-Rama bookstore 

application), 272–273

secret.php, 367–369security

application security threats

access to sensitive data, 331–333actors, 339–340compromised server, 338denial of service, 335–337loss of data, 334–335malicious code injection, 337modification of data, 334repudiation, 338–339

attackers, 339authentication

access control, 366–369basic authentication, 372–377custom authentication, 

 creating, 377

passwords, 369–371PHPbookmark project, 569–587in session control, 483–491visitors, identifying, 365–366

character sets, 439–440code, securing, 343

bugs, 352–353escaping output, 348–350

644

security

filtering user input, 343–348organizing code, 350–351

crackers, 339database servers, securing, 357–359disaster planning, 362–364file systems, 352MySQL, 299–301

passwords, 300user privileges, 300–301web issues, 301

networks, securing, 360–361

denial of service attacks, 361DMZ, 360–361firewalls, 360

operating system, securing, 361–362permissions, 59strategies for handling, 341–343

balancing security and usability, 

342

monitoring, 342–343starting with the right mindset, 342

twofold approach to, 343web pages, protecting, 371web servers, securing, 354–357

browsing php.ini file, 355–356shared hosting of web applications, 

356–357

updating software, 354–355SELECT command (SQL), 250–251

evaluating, 304–309LIMIT clause, 261–262ORDER BY clause, 259WHERE clause, 252–253

comparison operators, 252–253

selecting

HTML elements with selectors, 496–497MySQL database, 232

SQL databases from the web, 278table types, 316

selectors (jQuery), 495–498

acting on, 498HTML elements, creating, 497–498pseudo-selectors, 497syntax, 496–497sending email, 404serialization, 521serialize( ) function, 521session control, 475

authentication, 483–491

authmain.php, 483–489logout.php, 490–491members_only.php, 489

configuring, 482–483cookies, 476, 477

setting from PHP, 476–477

session ID, storing, 477–478sessions

creating, 480–482destroying, 479registering variables, 478–479starting, 478

session ID, 476

storing, 477–478

session variables, 476, 479

unsetting, 479

session_start( ) function, 478set_error_handler( ) function, 557–558_set( ) function, 166–168setcookie( ) function, 476settype( ) function, 39SGML (Standard Generalized Markup 

Language), 16

shared hosting of web applications, security 

issues, 356–357

SSL (Secure Sockets Layer), troubleshooting

645

short style PHP tags, 16SHOW command (MySQL), 301–304

syntax, 303–304

show poll.php, 468–474show tables command, 237show_source( ) function, 525shuffle( ) function, 90–91simple tables, 218simplegraph.php, 451–452single-byte languages, 438single-line comments, 18size of files, determining, 70sizeof( ) function, 98–99slaves, setting up for replication, 313Smart Form Mail application

creating, 101–104regular expressions, 127–128

SMTP (Simple Mail Transfer Protocol), 404software, updating, 354–355Software Engineering: A Practitioner’s 

Approach, 542

software engineering, applying to web 

development, 530

solution components for PHPbookmark 

project, 561–565

sort( ) function, 76, 85–86sorting arrays, 85–87

with asort( ) function, 86–87with ksort( ) function, 86–87multidimensional arrays, 87–90reverse sorting, 83with sort( ) function, 85–86

source code, highlighting, 525–526special characters

meta characters, 124–125pattern matching, 123–124special privileges (MySQL), 230

splitting strings

explode( ) function, 112–113with regular expressions, 129–130with strtok( ) function, 113–114with substr( ) function, 114

sprintf( ) function, 109SQL (Structured Query Language), 

247–248. See also MySQL

aggregating data, 259–261INSERT command, 248–249inserting data, 248–250joins

cross joins, 258equi-joins, 258full joins, 254–255inner joins, 258joining more than two tables, 

255–256

left joins, 256–257

querying from the Web, 275–281

disconnecting from database, 281filtering input data, 276prepared statements, 279–280retrieving the results, 280–281selecting the database, 278setting up connection, 277–278

retrieving data, 250–259

from multiple tables, 251–253SELECT command, 250–251with specific criteria, 251–253

subqueries, 262–263

correlated subqueries, 264operators, 263row subqueries, 264as temporary table, 264

SSL (Secure Sockets Layer), troubleshooting, 610–612

646

stand-alone functions, _autoload( )

stand-alone functions, _autoload( ), 189starting sessions, 478statements, 16. See also commands

in RDBMSs, 74records, 62session ID, 477–478

echo, 22else, 42–43elseif, 43–44if, 41–42LOAD DATA INFILE, 315prepared statements, 279–280require( ), 132–134

applying templates to web pages, 

134–139

semicolons, 16switch, 44–45

static keyword, 185status of variables, testing, 40–41stopping scripts, 50, 520–522storage engines, 316–317

ARCHIVE, 316CSV, 316InnoDB, 316

foreign keys, 319transactions, 318–319

MEMORY, 316MERGE, 316MyISAM, 316

stored procedures, 320–327

control structures, 323–327

declare handlers, 325

cursors, 323, 325example of, 320–323local variables, 323

storing

dates and times, Unix timestamps, 

426–427orders, 54passwords, 300, 369

str_replace( ) function, 107, 118–119strategies for handling security, 341–343

balancing with usability, 342monitoring, 342–343starting with the right mindset, 342

strcasecmp( ) function, 115strchr( ) function, 117strcmp( ) function, 115strftime( ) function, 429–431string operators, 29string type columns, 244–246strings. See also regular expressions

changing case of, 111–112checking length of, 115–116comparing, 115concatenating, 22creating from classes, 194evaluating, 519–520filtering for output, 105–107, 347–348

to browser, 105–106to email, 106–107

finding within strings, 116–117formatting

conversion specification, 109for printing, 109–111

heredoc syntax, 23interpolation, 22joining, 113multibyte string functions, 440ordering, 115regular expressions, anchoring to 

 beginning or end of, 123

splitting

explode( ) function, 112–113

tables

647

with regular expressions, 129–130with strtok( ) function, 113–114with substr( ) function, 114

substrings

find-and-replace operations, 

118–119

finding position of, 117–118replacing with string functions, 116

trimming, 104

stristr( ) function, 117strlen( ) function, 115–116strnatcmp( ) function, 115strpos( ) function, 117–118strstr( ) function, 116–117strtok( ) function, 113–114strtolower( ) function, 112strtoupper( ) function, 112structure

of classes, 162–163of functions, 144–145

strval( ) function, 41subclasses, 161–162

inheritance, 168–169

submit event, 504subnamespaces, 197subqueries, 262–263

correlated subqueries, 264operators, 263row subqueries, 264as temporary table, 264

substr( ) function, 114substr_replace( ) function, 118–119substrings

find-and-replace operations, 118–119finding position of, 117–118finding with regular expressions, 

128–129

replacing

with regular expressions, 129with string functions, 116

subtraction operator, 28Subversion, 537success key, 507superclasses, 161–162superglobal arrays, 20, 27support for images in PHP, setting up, 

449–450

switch statement, 44–45syntax

heredoc, 23jQuery selectors, 496–497semicolons, 16SHOW command, 303–304

syntax errors, 543–544system( ) function, 399

T

table types

ARCHIVE, 316CSV, 316InnoDB, 316

foreign keys, 319transactions, 318–319

MEMORY, 316MERGE, 316MyISAM, 316selecting, 316tables, 210, 218

aliases, 257–258altering after creation, 265–268columns, 235–237

CHAR type, 235VARCHAR type, 235–236

creating, 232–234

648

tables

displaying, 302dropping, 268grant tables, 292–293

columns_priv table, 296–298connection verification, 298db table, 295–296procs_priv table, 296–298request verification, 298tables_priv table, 296–298user table, 293–295

joining

full joins, 254–255left joins, 256–257

linking tables, 218optimizing, 310records

deleting, 268updating, 265relationships, 213retrieving data

criteria, specifying, 251–253from multiple tables, 251–253rows, inserting into SQL database, 

248–250

simple tables, 218subqueries as temporary table, 264triggers, 327–329viewing, 237–238

tables_priv table, 296–298tags

JavaScript, <script> 494–495PHP, 16

short style, 16XML style, 16

templates, applying to web pages, 134–139temporarily modifying runtime environment, 

524–525

terminating scripts, 520–522

ternary operator, 34testing

code, 541–542PHP support, 610variable status, 40–41

text

applying to buttons, 461–464bounding box, 462–463descenders, 463positioning on buttons, 464regular expressions

anchoring to beginning or end of 

string, 123

assertions, 126–127backreferences, 126branching, 123character class, 121–122character sets, 120–121counted subexpressions, 123delimiters, 120escape sequences, 125–126meta characters, 124–125repetition, 122in Smart Form Mail application, 

127–128

special characters, matching, 

123–124

strings, splitting, 129–130substrings, finding, 128–129

writing on buttons, 464–465

threats to web application security

access to sensitive data, 331–333actors, 339–340compromised server, 338denial of service, 335–337malicious code injection, 337modification of data, 334repudiation, 338–339

user-defined exceptions

649

three-dimensional arrays, 84–85throw keyword, 200time, microseconds, 435timestamps, formatting, 429–431timezones, 423–424top-down approach to security, 343totals, calculating on order forms, 36–37tracking file upload progress, 387–388traits, 174–176transactions, 317–319

using InnoDB, 318–319translation files, 445–447trigger_error( ) function, 556triggering your own errors, 556triggers, 327–329trim( ) function, 104trimming strings, 104troubleshooting. See also error handling; 

exception handling

with EXPLAIN command, 308–309file upload, 389opening files, 58–61SSL, 610–612

TrueType fonts, 457try blocks, 199two-dimensional arrays, 82–84twofold approach to security, 343two-table joins, 254–255type casting, 25type codes for conversion specification, 

110–111

type hinting, 185–186type operator, 35type strength, 25

U

uasort( ) function, 89ucfirst( ) function, 112

ucwords( ) function, 112uksort( ) function, 89umask( ) function, 394unary operator, 28–29undefined functions, calling, 142–143UNIX

Apache, installing, 600–602MySQL, installing, 602–605PHP, installing, 605–609

Unix Epoch, 426Unix timestamps, 426–427

converting date and time to, 426

UNIX_TIMESTAMP( ) function, 432–433unlink( ) function, 70unserialize( ) function, 521unsetting session variables, 479update anomalies, 215UPDATE command (SQL), 265updating

privileges, 299records, 265software, 354–355

uploading files, 379–389, 420

HTML form, 381–382php.ini settings, 380–381tracking upload progress, 387–388troubleshooting, 389writing the file handling script, 

382–387

upload.php, 382–387urlencode( ) function, 407usability, balancing with security, 342use command, 232user interface for chat application, building, 

504–507

user personalization, 561user table, 293–295user-defined exceptions, 202–204

650

user-defined functions

user-defined functions, 144

parameters, 147

user-defined sorts, 88–89users

authentication, identifying visitors, 

365–366

MySQL, 225–232

creating, 224, 225–227principle of least privilege, 225privileges, 227–230, 300–301privileges (MySQL), 291–299web access, 231–232

usort( ) function, 88–89

V

val( ) method, 498validating dates with checkdate( ) function, 

428–429values, 211

atomic column values, 216–217basic values, filtering, 346–347null values, 217–218

VARCHAR type columns, 235–236variable functions, 146variable handling functions, 39–40variable variables, 25–26variables, 23

accessing, 20–22arrays, 75–76

accessing contents, 77–78converting to scalar variables, 

99–100

initializing, 79loading from files, 92–96multidimensional arrays, 75navigating, 96–97numerically indexed arrays, 76–77

reordering, 90–91reversing, 92sorting, 85–87three-dimensional arrays, 84–85two-dimensional arrays, 82–84

assigning values to, 24assignment operators, 20and constants, 26data types, 24–25

scalar values, 26type casting, 25type strength, 25debugging, 551–553environment variables, 401–402handles, 161identifiers, 23–24interpolation, 22local variables, 323scope, 27, 148–150serializing, 521session variables, 476, 479

registering, 478–479unsetting, 479

status, testing, 40–41version control, 536–537viewing tables, 237–238vieworders.php script, 65–66visibility, controlling, 169–170visitors, identifying, 365–366vprintf( ) function, 111vsprintf( ) function, 111

W

web access, configuring for MySQL users, 

231–232

web application development

applying to software engineering, 530

websites

651

chat application

chat server, building, 504–507user interface, building, 510–517internationalized software, 437–438jQuery, 494–495large projects

breaking up code, 535–536choosing a development  environment, 537–538

coding standards, 532commenting your code, 534defining naming conventions, 

532–534

directory structure, 536documenting, 538function libraries, 536indenting code, 534–535optimizing code, 540–541planning, 530–531prototyping, 538–539separating logic from content, 

539–540

testing code, 541–542version control, 536–537writing maintainable code, 532

localization, 437–438

character sets, 438–440locales, 438

operating system, securing, 361–362reusing code, 531–532security

code, securing, 343–352database servers, securing, 

357–359

disaster planning, 362–364executing commands, 353–354file system considerations, 352network security, 360–361

strategies for handling, 341–343web servers, 354–357

threats

access to sensitive data, 331–333compromised server, 338denial of service, 335–337loss of data, 334–335malicious code injection, 337modification of data, 334repudiation, 338–339

web database architecture, 218–220, 272web pages

internationalization

language selector page, 442–444locale-specific headers, 441–442

localizing, 440–445protecting, 371templates, applying with require( ) 

statement, 134–139

web servers, 218–219

Apache HTTP Server

.htaccess files, 374–377configuring, 356

Nginx, 614security, 354–357

browsing php.ini file, 355–356shared hosting of web applications, 

356–357

updating software, 354–355

websites

Bill Gates Wealth Clock, 407consuming date from other sites, 

404–408

cookies, 476, 477

session ID, storing, 477–478setting from PHP, 476–477

session control, 475visitors, identifying, 365–366

652 WHERE clause (SELECT command)

WHERE clause (SELECT command), 

252–253

comparison operators, 252–253

while loops, 47–48whitespace, 17Windows operating system, installation 

packages, 612–613

writing

code for classes, 177–184

accessor functions, 178attributes, 177metatags, 177operations, 181

file upload script, 382–387to files, 55, 61

as cause for runtime errors, 546–547

text on buttons, 464–465

X

XML, AJAX, 493–494XML style PHP tags, 16XOR operator, 32–33

Y-Zyield keyword, 192–193

This page intentionally left blank 

Accessing the Free Web EditionYour purchase of this book in any format, print or electronic, includes access to the corresponding Web Edition, which provides several special features to help you learn:

 ■ The complete text of the book online

 ■ Interactive quizzes and exercises to test your understanding of the material

 ■ Bonus chapters not included in the print or e-book editions

 ■ Updates and corrections as they become available

The Web Edition can be viewed on all types of computers and mobile devices with any modern web browser that supports HTML5.

To get access to the Web Edition of PHP and MySQL Web Development, Fifth Edition, all you need to do is register this book:

1.  Go to www.informit.com/register

2.  Sign in or create a new account

3.  Enter ISBN: 9780321833891

4.  Answer the questions as proof of purchase

The Web Edition will appear under the Digital Purchases tab on your Account page. Click the Launch link to access the product.

