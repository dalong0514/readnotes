19Managing the Date and Time

In this chapter, we discuss checking and formatting the date and time and converting between date formats. These capabilities are especially important when you are converting between MySQL and PHP date formats, Unix and PHP date formats, and dates entered by the user in an HTML form.

Key topics covered in this chapter include

 ■ Getting the date and time in PHP

 ■ Converting between PHP and MySQL date formats

 ■ Calculating dates

 ■ Using the calendar functions

Getting the Date and Time from PHPWay back in Chapter 1,「PHP Crash Course,」we described using the date() function to get and format the date and time from PHP. Here, we discuss this function and some of PHP’s other date and time functions in a little more detail.

Understanding TimezonesSome will argue that the easiest way to deal with timezones in a web application is just not to deal with them at all, because of the inevitable heartbreak timezones bring to developers. However, ignoring timezones really isn’t the best way to go about working with dates and times in applications that will be used by people worldwide.  

Instead, you have the option of storing all of your dates and times in a single, standard timezone (such as UTC) and converting them as needed to your user’s own timezone, storing dates and times in your own timezone and converting them as needed to your user’s own timezone (this can get tricky when you don’t actually know where your servers are located, or 

424

Chapter 19  Managing the Date and Time 

they are located in a different timezone than you physically are), or storing dates and times in the user’s own timezone.  

In this chapter, you’ll learn about the date(), time(), and strtotime() functions in PHP, among others, and it is important to note that these functions all use the timezone specified by the date.timezone setting in php.ini. By default, the value of date.timezone is not set, so PHP uses the system default. We recommend you specifically set a value for date.timezone in your server’s php.ini, using one of the timezones in the allowed list at http://php.net/manual/en/timezones.php.

If you use a standard timezone such as UTC for all dates and times in your application, you have the added bonus of a built-in MySQL function called UTC_TIMESTAMP(), which you could use anywhere you want to insert or update a date in a table. However, even if you go the route of storing dates and times in a standard format but want to convert them on the fly based on user settings, you could also use the MySQL function called CONVERT_TZ() to do so.

Using the date() FunctionAs you might recall, the date() function takes two parameters, one of them optional. The first one is a format string, and the second, optional one is a Unix timestamp. If you don’t specify a timestamp, date() will default to the current date and time. It returns a formatted string  representing the appropriate date.

A typical call to the date() function could be

echo date('jS F Y');

This call produces a date in the format 17th February 2015. The format codes accepted by date() are listed in Table 19.1.

Table 19.1  Format Codes for PHP’s date() Function

Code Description

a

A

B

c

d

D

e

F

Morning or afternoon, represented as two lowercase characters, either am or pm.

Morning or afternoon, represented as two uppercase characters, either AM or PM.

Swatch Internet time, a universal time scheme representing the time of day between 000 and 999. More information is available at http://www.swatch.com/en/internet-time.

ISO 8601 date. A date is represented as YYYY-MM-DD. An uppercase T separates the date from the time. The time is represented as HH:MM:SS. Finally, the time zone is represented as an offset from Greenwich mean time (GMT)—for example, 2015-02-17T01:38:35+00:00.

Day of the month as a two-digit number with a leading zero. The range is from 01 to 31.

Day of the week in three-character abbreviated text format. The range is from Mon to Sun.

Timezone identifier, such as UTC or GMT.

Month of the year in full text format. The range is from January to December.

Getting the Date and Time from PHP

425

g

G

h

H

i

I

j

l

L

m

M

n

N

o

O

P

r

s

S

t

T

U

w

W

y

Y

z

Z

Hour of the day in 12-hour format without leading zeros. The range is from 1 to 12.

Hour of the day in 24-hour format without leading zeros. The range is from 0 to 23.

Hour of the day in 12-hour format with leading zeros. The range is from 01 to 12.

Hour of the day in 24-hour format with leading zeros. The range is from 00 to 23.

Minutes past the hour with leading zeros. The range is from 00 to 59.

Daylight savings time, represented as a Boolean value. This format code returns 1 if the date is in daylight savings and 0 if it is not.

Day of the month as a number without leading zeros. The range is from 1 to 31.

Day of the week in full-text format. The range is from Sunday to Saturday.

Leap year, represented as a Boolean value. This format code returns 1 if the date is in a leap year and 0 if it is not.

Month of the year as a two-digit number with leading zeros. The range is from 01 to 12.

Month of the year in three-character abbreviated text format. The range is from Jan to Dec.

Month of the year as a number without leading zeros. The range is from 1 to 12.

Day of the week as a single digit; ISO-8601 compliant. The range is from 1 (Monday) to 7 (Sunday).

ISO-8601 year number. This has the same value as Y, except that if the ISO week number (W) belongs to the previous or next year, the year is used instead. 

Difference between the current time zone and GMT in hours—for example, +1600.

Difference between the current time zone and GMT, with colon between hours and  minutes—for example, +05:00.

RFC822-formatted date and time—for example, Tue, 17 Feb 2015 01:41:42 +0000.

Seconds past the minute with leading zeros. The range is from 00 to 59.

Ordinal suffix for dates in two-character format. It can be st, nd, rd, or th, depending on the number it follows.

Total number of days in the date’s month. The range is from 28 to 31.

Time zone setting of the server in three-character format—for example, EST.

Total number of seconds from January 1, 1970 at 00:00:00, to the current time; also known as a Unix timestamp for this date.

Day of the week as a single digit. The range is from 0 (Sunday) to 6 (Saturday).

Week number in the year, with weeks beginning on a Monday; ISO-8601 compliant. 

Year in two-digit format—for example, 15.

Year in four-digit format—for example, 2015.

Day of the year as a number. The range is 0 to 365.

Offset for the current time zone in seconds. The range is -43200 to 43200.

426

Chapter 19  Managing the Date and Time 

Dealing with Unix TimestampsThe second parameter to the date() function is a Unix timestamp. In case you are  wondering exactly what this means, most Unix systems store the current time and date as a 32-bit integer containing the number of seconds since midnight, January 1, 1970, GMT, also known as the Unix Epoch. This concept can seem a bit esoteric if you are not familiar with it, but it’s a  standard and integers are easy for computers to deal with.

Unix timestamps are a compact way of storing dates and times, but it is worth noting that they do not suffer from the year 2000 (Y2K) problem that affects some other compact or abbreviated date formats. They do have similar problems, though, because they can represent only a limited span of time using a 32-bit integer. If your software needs to deal with events before 1902 or after 2038, you will be in trouble.

On some systems including Windows, the range is more limited. A timestamp cannot be nega-tive, so timestamps before 1970 cannot be used. To keep your code portable, you should bear this fact in mind.

You probably don’t need to worry about your software still being used in 2038. Timestamps do not have a fixed size; they are tied to the size of a C long, which is at least 32 bits. If your soft-ware still happens to be in use in 2038, it is exceedingly likely that your system will be using a larger type by that time.

Although this is a standard Unix convention, this format is still used by date() and a number of other PHP functions even if you are running PHP under Windows. The only difference is that, for Windows, the timestamp must be positive.

If you want to convert a date and time to a Unix timestamp, you can use the mktime()  function. It has the following prototype:

int mktime ([int hour[, int minute[, int second[, int month[,            int day[, int year]]]]]])

The parameters are fairly self-explanatory, but a trap to avoid with this function is that the parameters are in a fairly unintuitive order. The ordering doesn’t lend itself to leaving out the time. If you are not worried about the time, you can pass in 0s to the hour, minute, and second parameters. You can, however, leave out values from the right side of the parameter list. If you don’t provide parameters, they will be set to the current values. Hence, a call such as

$timestamp = mktime();

returns the Unix timestamp for the current date and time (although it will throw an E_STRICT notice if that is your error reporting setting). You could also get the same result by calling

$timestamp = time();

The time() function does not take any parameters and always returns the Unix timestamp for the current date and time.

Another option is the date() function, as already discussed. The format string "U" requests a timestamp. The following statement is equivalent to the two previous ones:

$timestamp = date("U");

Getting the Date and Time from PHP

427

You can pass in a two- or four-digit year to mktime(). Two-digit values from 0 to 69 are  interpreted as the years 2000 to 2069, and values from 70 to 99 are interpreted as 1970 to 1999.

Here are some other examples to illustrate the use of mktime():

$time = mktime(12, 0, 0);

gives noon on today’s date.

$time = mktime(0,0,0,1,1);

gives the 1st of January in the current year. Note that 0 (rather than 24) is used in the hour parameter to specify midnight.

You can also use mktime() for simple date arithmetic. For example,

$time = mktime(12,0,0,$mon,$day+30,$year);

adds 30 days to the date specified in the components, even though ($day+30) will usually be bigger than the number of days in that month.

To eliminate some problems with daylight savings time, use hour 12 rather than hour 0. If you add (24 * 60 * 60) to midnight on a 25-hour day, you’ll stay on the same day. Add the same number to midday, and it’ll give 11am but will at least be the right day.

Using the getdate() FunctionAnother date-determining function you might find useful is getdate(). This function has the following prototype:

array getdate ([int timestamp])

It takes an optional timestamp as a parameter and returns an array representing the parts of that date and time, as shown in Table 19.2.

Table 19.2  Array Key-Value Pairs from getdate() Function

Key

seconds

minutes

hours

mday

wday

mon

year

yday

Value

Seconds, numeric

Minutes, numeric

Hours, numeric

Day of the month, numeric

Day of the week, numeric

Month, numeric

Year, numeric

Day of the year, numeric

weekday

Day of the week, full-text format

428

Chapter 19  Managing the Date and Time 

Key

month

0

Value

Month, full-text format

Timestamp, numeric

After you have these parts of the date and time in an array, you can easily process them into any required format. The 0 element in the array (the timestamp) might seem useless, but if you call getdate() without a parameter,  it will give you the current timestamp.

Using the getdate() function, the code

<?php$today = getdate();print_r($today);?>

produces something similar to the following output:

Array(    [seconds] => 43    [minutes] => 7    [hours] => 2    [mday] => 17    [wday] => 2    [mon] => 2    [year] => 2015    [yday] => 47    [weekday] => Tuesday    [month] => February    [0] => 1424138863)

You can use the elements of the resulting array to display to your users, or use them further on in a script.

Validating Dates with checkdate()You can use the checkdate() function to check whether a date is valid. This capability is especially useful for checking dates constructed from user input. The checkdate() function has the following prototype:

int checkdate (int month, int day, int year)

It checks whether the year is a valid integer between 0 and 32,767, whether the month is an integer between 1 and 12, and whether the day given exists in that particular month. The function also takes leap years into consideration when working out whether a day is valid.

Getting the Date and Time from PHP

429

For example,

checkdate(2, 29, 2008)

returns true, whereas

checkdate(2, 29, 2007)

does not.

Formatting TimestampsYou can format a timestamp according to the system’s locale (the web server’s local settings) using the strftime() function. This function has the following prototype:

string strftime ( string $format [, int $timestamp] )

The $format parameter is the formatting code that defines how the timestamp will be displayed. The $timestamp parameter is the timestamp that you pass to the function. This parameter is optional. If no timestamp is passed as a parameter, the local system timestamp (at the time the script is run) is used. For instance, the following code

<?php echo strftime('%A<br />'); echo strftime('%x<br />'); echo strftime('%c<br />'); echo strftime('%Y<br />');?>

displays the current system timestamp in four different formats. This code will produce output similar to the following:

Tuesday02/17/15Tue Feb 17 02:10:19 20152015

The complete list of formatting codes for strftime() is listed in Table 19.3.

Table 19.3  Formatting Codes for strftime()

Code

%a

%A

Description

Day of week (abbreviated). The range is Sun through Sat.

Day of week. The range is Sunday through Saturday.

%b or %h

Month (abbreviated). The range is Jan through Dec.

%B

%c

Month. The range is January through December.

Date and time in standard format. For example: Tue Feb 17 02:13:04 2015.

430

Chapter 19  Managing the Date and Time 

Code

Description

%C

%d

%D

%e

%F

%g

%G

%H

%I

%j

%k

%l

%m

%M

%n

%p

%P

%r

%R

%s

%S

%t

%T

%u

%U

%V

%w

Century, in two-digit format, determined by dividing the year by 100 and  truncating to an integer. For example: 20. 

Day of month from 01 to 31.

Date in abbreviated format (mm/dd/yy). For example: 02/17/15.

Day of month as a two-character string (from '1' to '31').

An alias for "%Y-%m-%d", which is a common format for database dat-estamps. Produces a date such as 2015-02-17.

Year according to the week number, two digits; ISO-8601 compliant.

Year according to the week number, four digits; ISO-8601 compliant.

Hour, from 00 to 23.

Hour, from 1 to 12.

Day of year, from 001 to 366.

Hour as a two-character string (from '1' to '23').

Hour as a two-character string (from '1' to '12').

Month, from 01 to 12.

Minute, from 00 to 59.

A newline character (\n).

Upper-case AM or PM. 

Lower-case am or pm.

Time using AM/PM. notation, such as 02:22:45 AM.

Time using 24-hour notation, such as 02:22.

The Unix Epoch Time timestamp, the same as calling time(). For example: 1424140235.

Seconds, from 00 to 59.

A tab character (\t).

Time in hh:ss:mm format, such as 02:23:57.

Day of week, from 1 (Monday) to 7 (Sunday); ISO-8601 compliant.

Week number of the year (with the first Sunday of the year being the first day of the first week).

Week number (with the first week in the year with at least four days counting as week number 1); ISO-8601 compliant.

Day of week, from 0 (Sunday) to 6 (Saturday).

Converting Between PHP and MySQL Date Formats

431

%W

%x

%X

%y

%Y

%z

%Z

Week number (with the first Monday of the year being the first day of the first week).

Date in standard format (without the time), such as 02/17/15.

Time in standard format (without the date), such as 02:26:21.

Year, in two digits, such as 15.

Year, in four digits, such as 2015.The timezone offset, such as -0500.The timezone abbreviation, such as EST.

It is important to note that whenever it says standard format in Table 19.3, the formatting code gets replaced by the associated value according to the web server’s locale settings. The strftime() function is very useful for displaying dates and times in a variety of different ways to make your pages more user friendly.

Converting Between PHP and MySQL Date FormatsDates and times in MySQL are handled in ISO 8601 format. Times work relatively intuitively, but ISO 8601 requires you to enter dates with the year first. For example, you could enter February 17, 2015, either as 2015-02-17 or as 15-02-17. Dates retrieved from MySQL are also in this format by default.

Depending on your intended audience, you might not find this function very user friendly. To communicate between PHP and MySQL, then, you usually need to perform some date conversion. This operation can be performed at either end.

When putting dates into MySQL from PHP, you can easily put them into the correct format by using the date() function, as shown previously. One minor caution if you are creating them from your own code is that you should store the day and month with leading zeros to avoid confusing MySQL. You can use a two-digit year, but using a four-digit year is usually a good idea. If you want to convert dates or times in MySQL, two useful functions are DATE_FORMAT() and UNIX_TIMESTAMP().

The DATE_FORMAT() function works similarly to the PHP function but uses different formatting codes. The most common thing you want to do is format a date in American format (MM-DD-YYYY) rather than in the ISO format (YYYY-MM-DD) native to MySQL. You can do this by writing your query as follows:

SELECT DATE_FORMAT(date_column, '%m %d %Y')FROM tablename;

432

Chapter 19  Managing the Date and Time 

The format code %m represents the month as a two-digit number; %d, the day as a two-digit number; and %Y, the year as a four-digit number. A summary of the more useful MySQL format codes for this purpose is shown in Table 19.4.

Table 19.4  Format Codes for MySQL’s DATE_FORMAT() Function

Code

%M

%W

%D

%Y

%y

%a

%d

%e

%m

%c

%b

%j

%H

%k

Description

Month, full text

Weekday name, full text

Day of month, numeric, with text suffix (for example, 1st)

Year, numeric, four digits

Year, numeric, two digits

Weekday name, three characters

Day of month, numeric, leading zeros

Day of month, numeric, no leading zeros

Month, numeric, leading zeros

Month, numeric, no leading zeros

Month, text, three characters

Day of year, numeric

Hour, 24-hour clock, leading zeros

Hour, 24-hour clock, no leading zeros

%h or %I

Hour, 12-hour clock, leading zeros

%l

%i

%r

%T

Hour, 12-hour clock, no leading zeros

Minutes, numeric, leading zeros

Time, 12-hour (hh:mm:ss [AM|PM])

Time, 24-hour (hh:mm:ss)

%S or %s

Seconds, numeric, leading zeros

%p

%w

AM or PM

Day of the week, numeric, from 0 (Sunday) to 6 (Saturday)

You can see the most current and complete list of format codes for MySQL’s DATE_FORMAT() function at http://dev.mysql.com/doc/refman/5.6/en/date-and-time-functions.html#function_date-format.

The UNIX_TIMESTAMP() function works similarly but converts a column into a Unix  timestamp. For example,

Calculating Dates in PHP

433

SELECT UNIX_TIMESTAMP(date_column)FROM tablename;

returns the date formatted as a Unix timestamp. You can then do as you want with it in PHP.

You can easily perform date calculations and comparisons with the Unix timestamp. Bear in mind, however, that a timestamp can usually represent dates only between 1902 and 2038, whereas the MySQL date type has a much wider range.

As a rule of thumb, use a Unix timestamp for date calculations and the standard date format when you are just storing or showing dates.

Calculating Dates in PHPA simple way to work out the length of time between two dates in PHP is to use the difference between Unix timestamps. We use this approach in the script shown in Listing 19.1.

Listing 19.1  calc_age.php—Working Out a Person’s Age Based on Birthdate<?php// set date for calculation$day = 18;$month = 9;$year = 1972;

// remember you need bday as day month and year$bdayunix = mktime (0, 0, 0, $month, $day, $year); // get ts for then$nowunix = time(); // get unix ts for today$ageunix = $nowunix - $bdayunix; // work out the difference$age = floor($ageunix / (365 * 24 * 60 * 60)); // convert from seconds to years

echo 'Current age is '.$age.'.';?>

This script sets the date for calculating the age. In a real application, it is likely that this infor-mation might come from an HTML form. The script begins by calling mktime() to work out the timestamp for the birthday and for the current time:

$bdayunix = mktime (0, 0, 0, $month, $day, $year);$nowunix = time(); // get unix ts for today

Now that these dates are in the same format, you can simply subtract them:

$ageunix = $nowunix - $bdayunix;

Now, the slightly tricky part: converting this time period back to a more human-friendly unit of measure. This is not a timestamp but instead the age of the person measured in seconds. You can convert it back to years by dividing by the number of seconds in a year. You then round it 

434

Chapter 19  Managing the Date and Time 

down by using the floor() function because a person is not said to be, for example, 20, until the end of his twentieth year:

$age = floor($ageunix / (365 * 24 * 60 * 60)); // convert from seconds to years

Note, however, that this approach is somewhat flawed because it is limited by the range of Unix timestamps (generally 32-bit integers). Birthdates are not an ideal application for timestamps. This example works on all platforms only for people born from 1970 onward. Windows cannot manage timestamps prior to 1970. Even then, this calculation is not always accurate because it does not allow for leap years and might fail if midnight on the person’s birthday is the daylight savings switchover time in the local time zone.

Calculating Dates in MySQLPHP has a few date manipulation functions built in, specifically date_add(), date_sub(), and date_diff(). Obviously, you can write your own, but ensuring that you correctly account for leap years and daylight savings time can be tricky, so best to go with what is already available. 

Another date calculation option that may not seem immediately obvious is using MySQL. MySQL provides an extensive range of date manipulation functions that work for times outside the reliable range of Unix timestamps. You need to connect to a MySQL server to run your query, but you do not have to select any data from the database.

For example, the following query adds one day to the date February 28, 1700, and returns the resulting date:

select adddate('1700-02-28', interval 1 day)

The year 1700 is not a leap year, so the result is 1700-03-01.

You can find an extensive syntax for describing and modifying dates and times described in the MySQL manual; it is located at http://dev.mysql.com/doc/refman/5.6/en/date-and-time-functions.html

Unfortunately, there is not a simple way to get the number of years between two dates, so the birthday example in Listing 19.1 is still a little flaky. You can get a person’s age in days very easily, and Listing 19.2 converts that age to years imprecisely.

Listing 19.2 

 mysql_calc_age.php—Using MySQL to Work Out a Person’s Age Based on Birthdate

<?php// set date for calculation$day = 18;$month = 9;$year = 1972;

// format birthday as an ISO 8601 date$bdayISO = date("c", mktime (0, 0, 0, $month, $day, $year));

Using Microseconds

435

// use mysql query to calculate an age in days$db = mysqli_connect('localhost', 'user', 'pass');$res = mysqli_query($db, "select datediff(now(), '$bdayISO')");$age = mysqli_fetch_array($res);

// convert age in days to age in years (approximately)echo 'Current age is '.floor($age[0]/365.25).'.';?>

After formatting the birthday as an ISO timestamp, you pass the following query to MySQL:

select datediff(now(), '1972-09-18T00:00:00+10:00')

The MySQL function now() always returns the current date and time. The MySQL function datediff() subtracts one date from another and returns the difference in days.

It is worth noting that you are not selecting data from a table or even choosing a database to use for this script, but you do need to log in to the MySQL server with a valid username and password.

Because no specific built-in function is available for such calculations, a SQL query to  calculate the exact number of years is fairly complex. Here, we took a shortcut and divided the age in days by 365.25 to give the age in years. This calculation can be one year out if run exactly on somebody’s birthday, depending on how many leap years there have been in that person’s lifetime.

Using MicrosecondsFor some applications, measuring time in seconds is not precise enough to be useful. If you want to measure very short periods, such as the time taken to run some or all of a PHP script, you need to use the function microtime().

Although an optional parameter, we recommend you pass true to microtime(). When this optional parameter is provided, microtime() will return the time as a floating point value that is ready for whatever use you have in mind. The value is the same one returned by mktime(), time(), or date() but has a fractional component.

The statement

echo number_format(microtime(true), 5, '.', '');

produces something like 1424141373.59059.

On older versions, you cannot request the result as a float. It is provided as a string. A call to microtime() without a parameter returns a string of this form " 0.88679500 1424141403". The first number is the fractional part, and the second number is the number of whole seconds elapsed since January 1, 1970.

Dealing with numbers rather than strings is more useful, so it is easiest to call microtime() with the parameter true.

436

Chapter 19  Managing the Date and Time 

Using the Calendar FunctionsPHP has a set of functions that enable you to convert between different calendar systems. The main calendars you will work with are the Gregorian, Julian, and Julian Day Count.

Most Western countries currently use the Gregorian calendar. The Gregorian date October 15, 1582, is equivalent to October 5, 1582, in the Julian calendar. Prior to that date, the Julian calendar was commonly used. Different countries converted to the Gregorian calendar at different times and some not until early in the twentieth century.

Although you may have heard of these two calendars, you might not have heard of the Julian Day Count (JD). It is similar in many ways to a Unix timestamp. It is a count of the number of days since a date around 4000 BC. In itself, it is not particularly useful, but it is useful for converting between formats. To convert from one format to another, you first convert to a Julian Day Count and then to the desired output calendar.

To use these functions under Unix, you first need to compile the calendar extension into PHP with --enable-calendar. These functions are built into the standard Windows install.

To give you a taste for these functions, consider the prototypes for the functions you would use to convert from the Gregorian calendar to the Julian calendar:

int gregoriantojd (int month, int day, int year)string jdtojulian(int julianday)

To convert a date, you would need to call both of these functions:

$jd = gregoriantojd (9, 18, 1582);echo jdtojulian($jd);

This call echoes the Julian date in a MM/DD/YYYY format.

Variations of these functions exist for converting between the Gregorian, Julian, French, and Jewish calendars and Unix timestamps.

Further ReadingIf you would like to read more about date and time functions in PHP and MySQL, you can consult the relevant sections of the manuals at http://php.net/manual/en/book.datetime.php and http://dev.mysql.com/doc/refman/5.6/en/date-and-time-functions.html.

If you are converting between calendars, try the manual page for PHP’s calendar functions: http://php.net/manual/en/book.calendar.php.

NextWe mentioned locales a bit during our discussion of dates and times, and understanding locales is part of understanding the internationalization of web applications. In Chapter 20,「Internationalization and Localization,」we discuss how localization is far more than just translation, and how to prepare your applications for localization. 

