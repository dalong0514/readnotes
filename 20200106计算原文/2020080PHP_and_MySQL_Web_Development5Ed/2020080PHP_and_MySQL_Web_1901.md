20Internationalization and Localization

In this chapter, we discuss the basics of internationalizing your web applications in preparation for localizing their contents. Creating internationalized web applications with PHP is simple, and the benefits to your international audience are numerous. Start by understanding how internationalization and localization are different, but related, concepts, and you’ll be prepared to capture a truly worldwide audience.

Key topics covered in this chapter include

 ■ Understanding and preparing for different character sets

 ■ Structuring your application to produce localized content

 ■ Using gettext() for internationalization and localization 

Localization Is More than TranslationA common misconception is that localizing a website, web application, or really anything, is just about translating the content for the target location. However, it is important to understand that neither internationalization nor localization is the same thing as content translation. In fact, you can have a website or web application full of content that is translated—such as all in German, all in Spanish, or all in Japanese—and yet it might not be considered an internationalized or even localized website or web application at all. It would just be a translated website or web application, and that’s it.

In order to create localized software (encompassing websites and web applications, as well as all other types), you must first internationalize it. The basic aspects of internationalized software include

 ■ Externalized strings, icons, and graphics

 ■ Modifiable display of formatting functions (dates, currency, numbers, and so on)

438

Chapter 20  Internationalization and Localization 

Only after you have constructed your software so that your strings are externalized—meaning when all strings used in functions, classes, and other places within your code are managed in one place and included or otherwise referred to as constant variables—and your formatting functions can change per locale, can you begin the process of localization. Content translation happens to be part of localization, or targeting your software for a particular locale.

A locale is a place where something is set, such as the place where people live and speak American English and spell the word「color」without a「u」—you might refer to that locale as「The United States of America.」But in the world of computing, a locale refers to a set of parameters that identifies a user’s language, geographic region, and any other preferences based on location that might be relevant to represent within a user interface.

Standard locale identifiers consist of both language and region indicators, such as en_US for「English language in the United States」and en_GB for「English language in Great Britain.」

You might ask yourself why the regional differentiation, but think about just the spelling  differences between American and British English, let alone the contextual differences you might want to apply to your software overall for users in the United States versus Great Britain. To use another example, suppose you maintain a website with text in German and targeted for use only by people in Germany—that would be the de_DE locale (「German language in Germany」). While Austrians who speak German may very well use that site perfectly fine as-is, unless you have also localized the site for the de_AT locate (「German language in Austria」) that website would never be quite right for those users.

Understanding Character SetsCharacter sets are usually referred to as single-byte or multibyte, referring to the number of bytes needed to define a relationship with a character used in a language. English, German, and French (among many others) are single-byte languages, as only 1 byte is necessary to represent a character such as the letter a or the number 9. Single-byte code sets have, at most, 256  characters, including the entire set of ASCII characters, accented characters, and other characters necessary for formatting.

Multibyte character sets have more than 256 characters, including all the single-byte characters as a subset. Multibyte languages include Traditional and Simplified Chinese, Japanese, Korean, Thai, Arabic, and Hebrew, among others. These languages require more than 1 byte to represent a character. A good example is the word Tokyo, the capital of Japan. In English, it is spelled with four different characters, using a total of 5 bytes. However, in Japanese, the word is represented by two syllables, tou and kyou, each of which uses 2 bytes, for a total of 4 bytes used.

To properly interpret and display the text of web pages in their intended language, it is up to you to tell the web browser which character set to use. This goal is achieved by sending the appropriate headers before all content.

The headers in question are the Content-type and Content-language headers, and these can also be set as HTML5 tag attributes. Because PHP provides you with the ability to create a 

Understanding Character Sets

439

dynamic environment, go ahead and cover all your bases by sending the appropriate headers before your text and also print the correct HTML5 attributes tags in your document.

The following is an example of the header() function outputting the proper character  information for an English site:

header("Content-Type: text/html;charset=ISO-8859-1");header("Content-Language: en");

The accompanying HTML5 tags for the above headers are

<html lang="en"><meta charset="ISO-8859-1">

A Japanese site uses a different character set and different language code:

header("Content-Type: text/html;charset=UTF-8");header("Content-Language: ja");

The accompanying HTML5 tags for these headers are

<html lang="ja"><meta charset="UTF-8">

It is important to set your headers appropriately because, for example, if you have a set of pages that include Japanese text and you do not send the correct headers regarding language and character set, those pages will render incorrectly in web browsers whose primary language is not Japanese. In other words, because no character set information was included, the browser would assume that it is supposed to render the text using its own default character set. 

Similarly, if your Japanese pages use the UTF-8 character set and your browser is set for ISO-8859-1, your browser will try to render the Japanese text using the single-byte ISO-8859-1 character set. It will fail miserably in this unless headers alert it to use UTF-8 and you have the appropriate libraries and language packs installed on your operating system to display the text as it was meant to be viewed.

Security Implications of Character SetsThroughout the PHP Manual—and especially in the sections that concentrate on interact-ing with databases such as MySQL—you may see cautions about the security implications of character sets. This is not to say that character sets themselves are inherently insecure. Instead, these are cautions to ensure that developers understand a little bit about the character sets in use and how security issues may arise if basic precautions are not taken when working with strings that contain these characters—for example, in SQL statements.

A classic example of character set–related security issues is the encoding mismatch between the server, PHP, and MySQL, and especially with multibyte languages. Let’s say that PHP thinks it is sending pure ASCII text to MySQL, and the database’s default character set is Big5. In this situation, when you use a function such as mysql_real_escape_string() (or its object-oriented counterpart) to escape strings before sending them to the database, PHP will miss the trailing character of the double-byte character set because it simply didn’t know to look for it. 

440

Chapter 20  Internationalization and Localization 

This miscommunication will cause the encoded character to essentially become gibberish, which is bad enough if you intended to display it in a user interface. However, an even worse outcome is when someone takes advantage of this mismatch by injecting SQL into what is now an open string making its way to your database for possible execution. 

Using Multibyte String Functions in PHPHaving mentioned multibyte character encoding schemes previously in this chapter, we would be remiss not to point out that PHP includes a set of built-in functions specifically to handle the manipulation of multibyte strings. If you attempt to manipulate multibyte strings with a non-multibyte-aware string function, that function very likely will not parse the string correctly—this should make sense if you think about it, as a function specifically looking for single byte characters shouldn’t know what to do (or should do something messy) when faced with multibyte strings. 

In order to use the multibyte string functions in PHP, they must be enabled during the configuration process by using --enable-mbstring when configuring and building PHP. Windows users will need to enable the php_mbstring.dll extension in php.ini. After this is  configured, you can use any of the more than 40 mbstring-related functions for handling multibtye input in PHP. 

You can read about these multibyte string–related functions in great detail in the PHP Manual at http://www.php.net/mbstring. As a general rule when working with multibyte strings, just look for a similarly named function as its single-byte equivalent (e.g., mb_stripos() versus just strpos() to find the first occurrence of a string within another string).

Creating a Basic Localizable Page StructureNow that you’ve learned some foundational information about internationalization, localization, and character sets, take a look at creating a basic localizable page structure for a website. The pieces shown here enable a user to select a target language and then receive a welcome message in the appropriate language.

The goal of this section is simply to provide a basic example of externalizing strings—which is one of the characteristics of internationalization—and presenting localized text based on user preferences. The workflow of this set of scripts is such that a user happens upon your English-based website but is also presented with an option to browse within the locale of the user’s choice (only English or Japanese in this example). 

Three elements are involved in this process:

 ■ Creating and using a master file for sending locale-specific header information

 ■ Creating and using a master file for displaying the information based on the selected 

locale

 ■ Using the script itself

Creating a Basic Localizable Page Structure

441

Listing 20.1 shows the contents of the master file used for sending locale-specific header information.

Listing 20.1  define_lang.php—Language Definition File<?phpif ((!isset($_SESSION['lang'])) || (!isset($_GET['lang']))) {    $_SESSION['lang'] = "en";    $currLang = "en";} else {    $currLang = $_GET['lang'];    $_SESSION['lang'] = $currLang;}

switch($currLang) {    case "en":        define("CHARSET","ISO-8859-1");        define("LANGCODE", "en");     break;

    case "ja":        define("CHARSET","UTF-8");        define("LANGCODE", "ja");     break;

     default:        define("CHARSET","ISO-8859-1");        define("LANGCODE", "en");     break;}

header("Content-Type: text/html;charset=".CHARSET);header("Content-Language: ".LANGCODE);?>

In Listing 20.1 you can see that if no session value exists, the English locale settings are used. If your site were a Japanese site by default, you would change this file to use the Japanese locale by default. This script is meant to be used with the next script that you’ll see (in Listing 20.2), which contains an input-selection mechanism, by setting the value of $currLang to the result of this input in line 6 of Listing 20.1.

The switch statement beginning on line 10 contains a few case statements designed to assign the appropriate values to the constant variables CHARSET and LANGCODE. Lines 27–28 actually use these variables for the first time when dynamically creating and sending the headers for Content-type and Content-language.

442

Chapter 20  Internationalization and Localization 

Listing 20.2  lang_strings.php—String Definition File<?phpfunction defineStrings() {   switch($_SESSION['lang']) {         case "en":            define("WELCOME_TXT","Welcome!");            define("CHOOSE_TXT","Choose Language");         break;

case "ja":            define ("WELCOME_TXT","ようこそ！");            define ("CHOOSE_TXT","言語を選択");         break;

         default:            define("WELCOME_TXT","Welcome!");            define("CHOOSE_TXT","Choose Language");         break;   }}?>

Within the cases of the switch statement you can see two constants are defined for each language. The constants are CHARSET and LANGCODE, which correspond to the character set and language code for each locale. The display script in Listing 20.3 uses these constants to create the proper META tags for character set and language code.

Listing 20.2 creates the function that will be used in Listing 20.3 to pass localized strings to the browser. Like Listing 20.1, this code uses a switch statement to define the strings used for two constants—in this instance WELCOME_TXT and CHOOSE_TXT—which will be displayed in the script shown in Listing 20.3.

The last piece of the puzzle is the display script itself, shown in Listing 20.3. This script simply starts a session so that it can read the session value saved for the user’s language selection (set via clicking the link shown on the page), then fills in the blanks with the constants defined for that selected language.

Listing 20.3  lang_selector.php—Select and Display Language<?phpsession_start();include 'define_lang.php';include 'lang_strings.php';defineStrings();?>

Creating a Basic Localizable Page Structure

443

<!DOCTYPE html><html lang="<?php echo LANGCODE; ?>"><title><?php echo WELCOME_TXT; ?></title><meta charset="<?php echo CHARSET; ?>" /><body>   <h1><?php echo WELCOME_TXT; ?></h1>   <h2><?php echo CHOOSE_TXT; ?></h2>   <ul>      <li><a href="<?php echo $_SERVER['PHP_SELF']."?lang=en"; ?>">en</a></li>      <li><a href="<?php echo $_SERVER['PHP_SELF']."?lang=ja"; ?>">ja</a></li>    </ul></body></html>

When visiting the language selector page (lang_selector.php) for the first time, it should look something like Figure 20.1, since no selection has been made and thus the default English text is shown.

Figure 20.1  Showing the Default English Text

However, once another locale has been selected—such as Japanese in this example—the display changes to show the localized strings as in Figure 20.2.

444

Chapter 20  Internationalization and Localization 

Figure 20.2  Japanese Text Is Shown When Selecting the Japanese Locale

Using gettext() in an Internationalized ApplicationThe previous section walked you through a basic approach to internationalizing and  localizing a set of web pages. A more advanced approach—such as one for a large site with a lot of content or user interaction—would be to use the built-in PHP function called gettext(), which provides an API layer to the GNU gettext package. 

While the use of the built-in PHP function gettext() is, obviously, specific to PHP, many other programming languages have support for GNU gettext built into them. Conceptually understanding what GNU gettext does is important to the overall understanding of  internationalization and localization, no matter what programming language you use. At its core, GNU gettext looks for a specifically referenced string, indicated for you in a specific locale, and swaps that string in the appropriate place—this is much like the process we used to change the strings associated with constants in Listing 20.2, but at a larger scale.

Configuring Your System to Use gettext()Configuring PHP to use gettext() and related functions requires the installation of GNU gettext, a configuration change in PHP, and an adherence to a certain directory setup within your web server document root. 

If you are using a Linux or Mac OS X server for development or production, you may very well already have GNU gettext installed. Users of Windows systems as development or production servers very likely do not. To install GNU gettext for any system, please visit the「Downloading gettext」section of http://www.gnu.org/software/gettext/ and download the appropriate file for your system. Once GNU gettext is installed, you can configure PHP to recognize and use it.

Using gettext() in an Internationalized Application 

445

To enable gettext() and related functions in PHP, after you have installed GNU gettext on your server, requires reconfiguring and recompiling PHP on a Linux or Mac OS X system, and enabling a pre-built extension on a Windows system. When configuring PHP for compiling on Linux or Mac OS X, add the following configuration flag:

--with-gettext

After adding this compilation flag, continue compiling and installing PHP as usual. Remember to restart Apache after the new build the PHP module has been installed. 

On Windows, edit your php.ini file to enable the php_gettext.dll by removing the  semicolon from the line that looks like this:

;extension=php_gettext.dll

Restart the Apache web server after you have made this change and saved the file. With the appropriate changes made to your system as indicated above, you should now see a section in the results of the phpinfo() function that indicate that GNU gettext support is enabled.

With GNU gettext support enabled, the next change to make is simply to create directories for your locale-specific content within the document root of your web server. First, you will need to create a directory in the document root that will contain all the locale directories (for all the locales you want to support).

Next, within this parent directory, the locale directories should be named according to the two-letter lowercase abbreviation of the language according to the ISO-639-1  specification (e.g., 「en」,「ja」,「de」), followed by an underscore, followed by a two-letter uppercase country code according to the ISO-3166-1 (e.g.,「US」,「JP」,「DE」). Within the locale-specific  directory should be a directory called LC_MESSAGES.

So, to handle three locales in your site using GNU gettext and the PHP gettext() function, your directory structure might look something like this:

/htdocs   /locale      /de_DE         /LC_MESSAGES      /en_US         /LC_MESSAGES      /ja_JP         /LC_MESSAGES

Next, you’ll learn what sorts of files go into these directories—they’re not PHP files, but rather files that contain the translated strings to be used throughout the localized web site.

Creating Translation FilesThe translation files stored in the filesystem as above and used by GNU gettext are a specific type of file called a Portable Object file, or PO file. These files are plain text, but have the  extension *.po. While the use of a specific editor is not required to create PO files—they are just plain text after all—many people find the use of an editor or content management tool 

446

Chapter 20  Internationalization and Localization 

greatly reduces the overhead needed to maintain such files (which includes collaborating with translators and other content writers).

We recommend checking out tools such as Poedit (https://poedit.net/) or POEditor (https://poeditor.com/) for producing and maintaining the files of localized content, but for now we will simply show you simple PO file examples typed in plain text. You need one PO file for each locale, each called messages.po.

PO files begin with some identifying header information, then continue on to include message identifiers and message strings. An example PO file is shown in Listing 20.4, which sets up two strings for use in the en_US locale.

Listing 20.4  messages.po—PO file for en_US locale# required empty msgid & msgstrmsgid ""msgstr ""

"Project-Id-Version: 0.1\n""POT-Creation-Date: 2016-04-05 14:00+0500\n""Last-Translator: Jane Doe <jane@doe.com>\n""Content-Type: text/plain; charset=UTF-8\n""Language: en_US\n"

# welcome messagemsgid "WELCOME_TEXT"msgstr "Welcome!"

# instruction to choose languagemsgid "CHOOSE_LANGUAGE"msgstr "Choose Language"

The format of the file begins with an empty message identifier (msgid) and empty message string (msgstr), followed by some identifying information about the file and its creators: this file is versioned as 0.1, was created on April 4, 2016, by Jane Doe, and is in the UTF-8 character set for intended use in the en_US locale.

After this header information you find the messages and their translations. In this example, there are two messages identified by their keys: WELCOME_TEXT and CHOOSE_LANGUAGE. These message keys are similar to the constants used in the simple version of localization shown earlier in this chapter, but are named differently so as not to confuse the two examples. After each message key comes the message string to use in place of that key. Comments are used to introduce each set of message key and string, and you will notice one line of whitespace between each pair.

Sounds simple, and it is, but there is also a hidden complexity to creating and maintaining these PO files: the long list of options that are available to use, such as those listed in the  specification at http://www.gnu.org/software/gettext/manual/gettext.html#PO-Files.

Using gettext() in an Internationalized Application 

447

Reading the specification is recommended, but so is using a PO files editor because there’s one more step that such a piece of software takes care of for you: converting the PO files to MO files. MO files are Machine Object files, or files that contain the binary object data ultimately read by GNU gettext. Although easy for humans to read and maintain, PO files are not used directly by GNU gettext, and instead the MO file is used.

With GNU gettext and its related tools installed on your system, you can convert PO files to MO files using a utility program. On Linux, the command used for this example was simply:

msgfmt messages.po -o messages.mo

This command created a MO file called messages.mo from a plaintext PO file called messages.po. Now we’re ready to use PHP around all of this work.

Implementing Localized Content in PHP Using gettext()After all of the explanation above regarding how to install and use GNU gettext, the  implementation in PHP might seem like a bit of a let-down. The basic steps to the  implementation are as follows:

 ■ Use putenv() to set the LC_ALL environment variable for the locale.

 ■ Use setlocale() to set a value for LC_ALL.

 ■ Use bindtextdomain() to set the location of the translation catalog for the given 

domain (domain in this case means a name identifying the file that stores your message strings, not a domain like www.mydomain.com).

 ■ Use textdomain() to set the default domain to use with gettext(). 

 ■ Use gettext("some msgid") or _("some msgid") to invoke the GNU gettext 

translation for that message identifier. 

If you put the pieces together you might end up with something like Listing 20.5:

Listing 20.5  use_gettext.php—Reading MO Files with PHP<?php$locale="en_US";putenv("LC_ALL=".$locale);setlocale(LC_ALL, $locale);

$domain='messages';bindtextdomain($domain, "./locale");textdomain($domain);?><!DOCTYPE html><html><title><?php echo gettext("WELCOME_TEXT"); ?></title><body>

448

Chapter 20  Internationalization and Localization 

   <h1><?php echo gettext("WELCOME_TEXT"); ?></h1>   <h2><?php echo gettext("CHOOSE_LANGUAGE"); ?></h2>   <ul>   <li><a href="<?php echo $_SERVER['PHP_SELF']."?lang=en_US";?>">en_US</a></li>   <li><a href="<?php echo $_SERVER['PHP_SELF']."?lang =ja_JP";?>">ja_JP</a></li>    </ul></body></html>

Once you have a handle on the basics of application internationalization and localization, if you are going to develop an application used by speakers of many different languages, I recom-mend looking into a GNU gettext-based localization framework and crowdsourced translation services to handle the creation of your PO files (unless you have a plethora of native language speakers at your disposal or a lot of money to spend on translation services).

Further ReadingInternationalization and localization is a huge topic, and we only covered the most basic of the concepts in this brief chapter. For example, we didn’t talk about localizing numbers, dates, and currency using PHP, but all of these things are possible using built-in functionality such as the strftime() function for locale-aware time display, or by extending functionality to create helper classes and functions to suit your needs. You can also take a look at PHP  frameworks that handle all of this for you, to either evaluate their usefulness to your project or to see how those developers build the underlying functionality. Rich examples can be found in Zend Framework (http://framework.zend.com/manual/current/en/modules/zend.i18n.translating.html) and Symfony (http://symfony.com/doc/current/book/translation.html). 

NextOne of the many useful things you can do with PHP is to create images on the fly. Chapter 21,「Generating Images,」discusses how to use the image library functions to achieve some interesting and useful effects.

