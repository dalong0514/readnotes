23Integrating JavaScript and PHP

In this chapter we explore using JavaScript to interact with PHP scripts residing on the server to perform actions that don’t require a full-page synchronous request by the browser.

Key topics covered in this chapter include

 ■ Introducing the jQuery framework

 ■ Using basic jQuery techniques and concepts

 ■ Integrating jQuery and PHP

 ■ Creating a chat application with jQuery and PHP

Understanding AJAXThe synchronous requests made by web browsers are commonly called AJAX requests, with「AJAX」being an acronym coined circa 2003 that stands for「Asynchronous JavaScript and XML.」Despite the origin of the term, you will find no discussion of XML in this chapter because in the modern sense, AJAX typically deals with either HTML or JavaScript Object Notation (JSON) data.

What makes AJAX an interesting and powerful technology to the web developer can be found in the first letter of the acronym: AJAX is an asynchronous request. This means in a practical sense that we can perform requests against our PHP server, triggered by JavaScript, without having to refresh the entire web page. This process allows for robust user experiences that make web applications behave much more like native applications to the user, and also allows for user interfaces to be developed in a modular way that cannot reasonably build in a purely request-based approach in which the page is loaded and reloaded all the time.

The concept of AJAX has existed in widespread form since 2003 when JavaScript language imple-mentations across browsers all began supporting asynchronous request abilities using a common 

494

Chapter 23  Integrating JavaScript and PHP 

XMLHttpRequest class (sometimes referred to as「XHR」). However, in the modern era of web development, some sort of cross-browser JavaScript framework is almost universally used instead of these lower-level APIs. For the purposes of this chapter we explore using AJAX  technologies to interact with our server backend through the popular JavaScript framework jQuery.

A Brief Introduction to jQueryjQuery is an extremely popular JavaScript framework in use today. JavaScript frameworks such as jQuery perform the important job of creating a unified API for programming in JavaScript regardless of the browser being used by the end user. Without such a framework, the peculiarities and differences of each individual browser and version of that browser would have to be accounted for every time you wrote any JavaScript in your application. Frameworks like jQuery address this problem for you, which allows you to focus on the logic of your application rather than on the wide array of browsers your users could possibly use.

The jQuery framework is not only powerful in its own right, but is amazingly extendable through an entire collection of high-quality plugins based on the framework. These plugins provide the most functionality a developer could need in applications. For the purposes of this chapter we focus on the jQuery Core functionality, and specifically the AJAX functionality it provides.

Using jQuery in Web ApplicationsGetting jQuery as a tool in your toolbox for building a web application is extremely easy. Since it is just a JavaScript library, you simply need to include the library using the HTML <script> tag. 

There are two basic approaches available to you when doing this: 

 ■ Download and install the jQuery library as part of your web application, then reference 

the relevant JavaScript file using a standard <script> tag.

 ■ Use the jQuery CDN to load JavaScript into your web application requiring no files to 

exist locally in your project. Your <script> tag will reference an external URL. 

For the sake of portability, we use the latter approach throughout this chapter. 

Thus, enabling jQuery support in your web application is simply a matter of including the jQuery library within an HTML document using a <script> tag as follows, which references the current version of jQuery at the time of writing:

<script src="//code.jquery.com/jquery-2.2.3.min.js "/>

You will note that we did not specify a protocol (i.e., http://) when including the jQuery library. This was an intentional omission indicating to the browser that this resource should be loaded using the protocol defined by the parent document. Thus, if the page was loading using the https:// protocol this will be used to load the library as well. By taking this approach you can avoid potential security warnings raised by browsers attempting to load, for example, insecure resources during a secure request.

Using jQuery in Web Applications

495

Loading the base jQuery library is all that is needed to give the full power of the jQuery core to your web application! Next, let’s discuss some of the basic concepts and abilities of jQuery usage.

Basic jQuery Techniques and ConceptsWe will start our discussion of using jQuery by presenting some of the most fundamental concepts of the framework. For starters, by default jQuery exposes itself to the developer by creating a jQuery function namespace containing the full scope of functionality available of the core.

You use this jQuery namespace handle any time you want to do something using the jQuery library. That being said, having to type jQuery every time is a bit cumbersome, so by default the framework also creates a simple alias to the jQuery namespace using the $ symbol. We will use this alias throughout this chapter, as it is the most commonly used in practice in jQuery development. 

However, please note that if you use jQuery in conjunction with other JavaScript frameworks that also try to make use of the $ symbol as an alias for their framework, you can still use jQuery by setting it up to run in「no conflict」mode. This is done by calling the jQuery.noConflict() method that returns an instance you can assign to any variable or alias you choose:

var $newjQuery = jQuery.noConflict();

With that out of the way, let’s move on to the two fundamental concepts of jQuery development: selectors and events. 

Using jQuery SelectorsSelectors can be thought of as a type of query language that allows you to identify pieces of your HTML documents that, based on criteria, either perform manipulations on or attach logic to events triggered by them. This quasi-language is extremely powerful, allowing you to quickly reference HTML elements of a web page by various attributes of those elements. 

To better understand how selectors work, let’s start with a simple HTML document for discussion:

Listing 23.1  simple_form.html—A Simple Form to Reference for Work with Selectors<!DOCTYPE html><html><head>   <title>Sample Form</title></head><body>   <form id="myForm">    <label for="first_name">First Name</label><br/>    <input type="text" name="name[first]"            id="first_name" class="name"/><br/>

496

Chapter 23  Integrating JavaScript and PHP 

    <label for="last_name">Last Name</label><br/>    <input type="text" name="name[last]"            id="last_name" class="name"/><br/>    <button type="submit">Submit Form </button>    </form>

   <hr/>

   <div id="webConsole">      <h3>Web Console</h3>   </div>

    <script src="//code.jquery.com/jquery-2.2.3.min.js"></script></body></html>

Using the HTML in Listing 23.1 as an example, let’s look at a few different ways you can use jQuery to select various HTML elements. If you want to select a single specific element the best approach is to do so by the id attribute of the element:

var last_name = $('#last_name');

This introduces us to our first selector syntax, the # operation, which indicates the string that follows is the id attribute value of the target HTML element. If you want to select a group of elements, say both the first name and last name input fields, you can combine selectors together and separate each by a space:

var nameElements = $('#first_name #last_name');

This code would return into nameElements an array of two nodes that would be the HTML elements with the id attribute of first_name and last_name, respectively. 

Typically, when selecting multiple elements, you wouldn’t necessarily use the # operator to list out individually each element you wish to select. A more common use case would be to select a group of elements, regardless of their HTML element ID, that belong to the same class. You can do this using the class selector syntax:

var nameElements = $('.name');

Since both input elements in our example HTML document have been assigned the name class (using the class attribute of their respective HTML element), the proceeding two selector  examples in this case are equivalent. Selectors can also be based on HTML attributes that aren’t the id or class attributes as well as shown below:

var nameElements = $('input[type='text']');

This selector introduces a new syntax that allows you to search for HTML elements that have an arbitrary value for an arbitrary attribute. In this case, we are selecting all <input> HTML elements in the document that have a type attribute that equals text. Since in this case there are only two such elements, which also happen to share the class name and have 

Using jQuery in Web Applications

497

the id values of first_name and last_name, respectively, the three previous examples are  functionally equivalent for our example document, and return the same elements.

Unsurprisingly, you can also simply select by name elements based on the element type. For example, if you wanted to simply return the entire body of an HTML document you could use the following syntax:

var documentBody = $('body');

In addition to the ability to select specific elements based on attributes or element name, jQuery supports a number of pseudo-selectors that allow the developer to select elements in a more programmatic fashion. We will not be covering every pseudo-selector available (nor every specific selector syntax in general) in this chapter, but here are a few of the more useful and common syntaxes available:

var firstInput = $('input:first');

This code returns the first HTML <input> element found in the document. If you wanted to limit the search to the first <input> element found within our specific HTML form you could do this as well by combining two selectors:

var firstInput = $('#myForm input:first');

Another useful selector, especially working with HTML tables, can be seen in the selectors that allow you to select every other result of a given overall selector. For example, we know from previous examples that the following selector will return every <tr> tag in a given HTML document:

var tableRows = $('tr');

By adding the pseudo-selector :even or :odd, we can return every other table row into our selector, based on if by counting it was an「even」or「odd」row:

var oddRows = $('tr:odd');var evenRows = $('tr:even');

Selectors can also be used on fundamental JavaScript objects such as the document object available by default in an HTML page (representing the entire document). Simply pass the object into jQuery as you would a selector:

var jQueryDocSelector = $(document);

Finally, while not technically a「selector,」this same approach can be used to create brand new HTML elements in memory which can then be manipulated and added to the existing HTML document—essentially changing the contents on the page without refreshing the page. For example, say you wanted to create a new <p> HTML element. You could do so quickly as follows:

var newParagraph = $('<p>');

Using this technique, you could in theory construct entire segments of an HTML document, or even an entire HTML document:

var newParagraph = $('<p>This Is some <strong>Strong Text</strong></p>');

498

Chapter 23  Integrating JavaScript and PHP 

This is only the most basic of introductions to jQuery selectors but should be sufficient to introduce you to jQuery as you continue on to understand the AJAX-related examples of this chapter. Please consult the jQuery documentation on selectors for an in-depth understanding of the full syntax of selectors and their function: http://learn.jquery.com/using-jquery-core/selecting-elements/.

Acting on Selector SetsNow that you have an idea of how to search through an HTML document for specific elements, let’s discuss the various ways you can act on a selector. Fundamentally, jQuery selectors are plural in nature, meaning a selector with a single element is considered a set of one rather than a single element. Thus, you can perform actions on the whole set regardless of if it is one or one hundred individual elements in that set. 

Consider the jQuery val() method, which allows the developer to get or set the value  attribute of an input element:

var myInput = $('#first_name');console.log("The value of the input element with id #first_name is: ' + myInput.val());myInput.val('John');console.log("The value of #first_name has been changed to: ' + myInput.val());

In this example we are only selecting a single HTML element by the ID of that element, which in this case is first_name. However, because the selector always returns a set of elements the same method could have been used. To make this a little more practical, let’s introduce a second jQuery method called addClass(), which as its name implies, adds a new class to HTML elements:

var nameFields = $('.name');nameFields.addClass('form-control');

This example finds all HTML elements that have the existing class name, and applies a new class to them called form-control. 

In more complicated applications, where elements may or may not already exist, it becomes important to determine if a given selector actually returned any elements when executed. Since a set of zero is still technically a set (and thus would return a boolean true in JavaScript), you must use the length property of the set to determine if anything is actually in it:

var nameFields = $('.name'); if(nameFields.length > 0) {    console.log("We found some elements with the 'name' class");} else {    console.log("We found zero elements with the 'name' class");}

Using jQuery in Web Applications

499

Introduction to jQuery EventsEvents are a critical part of JavaScript, and by extension, of jQuery. Since JavaScript itself is an asynchronous programming language (meaning the logic of the program does not necessarily execute in the same order every time), events are critical to ensuring the meaning of your application is not lost when the order changes.

There are countless different events available to the jQuery developer representing all sorts of various circumstances. Some of these events are native to JavaScript itself, such as the click event broadcast every time a user clicks on something. Some other events are constructs of jQuery, such as the ready event that is fired when all the resources for a given HTML document have been properly loaded.

In the hierarchy of an HTML document, events bubble up from their source HTML element through the parent elements and eventually through the entire document, triggering actions for anything listening for them. Like many event systems, a given listener can halt the progres-sion of an event as well. Typically in jQuery, a selector is first used to identify the relevant HTML elements in question and then the on() method is used to listen for and consequently perform logic when that event is triggered. One of the simplest versions of this is listening for the ready event, triggered by jQuery upon full loading of the HTML document and its resources:

$(document).on('ready', function(event) {     // Code to execute when the document is ready});

Like most jQuery methods, the on() method can be used on any given selector. For example, if you wanted to respond every time a user clicked on a link you could attach a listener on all <a> tags with an href attribute and listen for the click event:

$('a').on('click', function(event) {    // Do something every time an <a> HTML element is clicked});

The on() method is a universal way to bind an event listener to a given event, but for both convenience and historic reasons, jQuery also provides a number of alias methods mapping directly to the event name. For example, $(document).on('ready', …) and $(document).ready(…) are identical in function.

Depending on the nature of your original selector, you may find yourself wanting to create a single event for a set of many HTML elements, but when fired act only on the specific element that triggered the event. You will note in the last two examples the closure provided to handle the event accepted a single parameter event. This event parameter is the event object created when the event fired, and contains within its target property the specific element that fired this specific event. Thus, if you wanted to act on a specific button when clicked you could do as follows:

$('button').on('click', function(event) {     var button = $(event.target);

     // Do something with the specific button that was clicked});

500

Chapter 23  Integrating JavaScript and PHP 

Likewise, especially for certain events like the click event of an <a> HTML element, the default listener of this event may take actions you don’t want to occur. For example, consider the following code:

$('a').on('click', function(event) {    var link = $(event.target).attr('href');    console.log("The link clicked had a URL of: " + link);});

Logically speaking, you could use this snippet of code to listen for a click event, extract the href attribute from the source of that click event using the attr() method, and then display the value of that attribute in the browser’s console. You would be right, however, if you think the code would not function as expected because there is a default behavior associated with clicking on this element (changing the browser’s location to the specified URL). This result is because although you correctly listened for the event, the event continued to bubble up through the HTML document, and the default behavior of the event in the browser was eventu-ally triggered. To prevent this outcome, you must prevent the event from continuing to bubble up through the document by using the preventDefault() method available in every event object. The following code includes this method call and would function correctly:

$('a').on('click', function(event) {    event.preventDefault();

    var link = $(event.target).attr('href');    console.log("The link clicked had a URL of: " + link);});

As previously stated in this chapter, there are many different events available to attach to and perform logic against—much too many to discuss in detail in this chapter. However, Table 23.1 provides a list of some of the most commonly used events available within the jQuery framework.

Table 23.1  Useful jQuery Events

Event

change

click

Type

Form Event

Mouse Event

Description

Triggered when a given form element changes value

Triggered when a given element is clicked

dblclick

Mouse Event

Triggered when a given element is double-clicked

error

JavaScript Event

Triggered when a JavaScript error occurs

focusin

Form Event

Triggered when a form element receives focus, prior to actually being focused

focus

focusout

hover

Form Event

Form Event

Triggered when a form element is focused

Triggered when a form element loses focus

Mouse Event

Triggered when the mouse floats over a given element

Using jQuery in Web Applications

501

keydown

Keyboard Event

Triggered when a key is pressed

keypress

Keyboard Event

Triggered when a key is pressed and released

keyup

ready

submit

Keyboard Event

Triggered when a key is released

Document Event

Triggered when the document object model is fully loaded

Form Event

Triggered when a given form is submitted

Pulling together all of the information presented so far in this chapter regarding selectors and events, let’s revisit a revamped version of the example document in Listing 23.1 to include the use of events to perform various actions. This new document is shown in Listing 23.2.

Listing 23.2  simple_form_v2.html—A Simple Form Example Now with jQuery in Use<!DOCTYPE html><html><head>   <title>Sample Form</title></head><body>   <form id="myForm">    <label for="first_name">First Name</label><br/>    <input type="text" name="name[first]"            id="first_name" class="name"/><br/>    <label for="last_name">Last Name</label><br/>    <input type="text" name="name[last]"            id="last_name" class="name"/><br/>    <button type="submit">Submit Form </button>    </form>

   <hr/>

   <div id="webConsole">      <h3>Web Console</h3>   </div>

    <script src="//code.jquery.com/jquery-2.2.3.min.js"></script>

    <script>       var webConsole = function(msg) {          var console = $('#webConsole');          var newMessage = $('<p>').text(msg);          console.append(newMessage);       }

       $(document).on('ready', function() {          $('#first_name').attr('placeholder', 'Johnny');

502

Chapter 23  Integrating JavaScript and PHP 

          $('#last_name').attr('placeholder', 'Appleseed');          });

       $('#myForm').on('submit', function(event) {          var first_name = $('#first_name').val();          var last_name = $('#last_name').val();

          webConsole("The form was submitted");          alert("Hello, " + first_name + " " + last_name + "!");        });

        $('.name').on('focusout', function(event) {          var nameField = $(event.target);          webConsole("Name field '" +                      nameField.attr('id') +                      "' was updated to '" +                      nameField.val() +                      "''");          });    </script>   

</body></html>

As you can see, we have made some significant additions to our original HTML by including a number of jQuery event handlers to breathe life into this once static document. The first thing we will discuss is the webConsole function we have defined as shown below:

var webConsole = function(msg) {    var console = $('#webConsole');            var newMessage = $('<p>').text(msg);

    console.append(newMessage);};

This function will be used at various points in the rest of our application to provide some real-time output of the script execution. We accomplish this by appending new paragraph (<p>) elements within an empty <div> element with the webConsole ID every time a new message is to be displayed. This is a great example of how to use jQuery to select, create, and then  manipulate a loaded HTML document using JavaScript.

Now that our helper function is out of the way, let’s get into the actual functionality of our simple jQuery app with the first piece of JavaScript that will be executed once the document is loaded:

$(document).on('ready', function() {    $('#first_name').attr('placeholder', 'Johnny');    $('#last_name').attr('placeholder', 'Appleseed');   });

Using jQuery in Web Applications

503

This will, upon loading of the HTML document, add new placeholder attributes to the input fields with the IDs of first_name and last_name, respectively. To the end user, this process happens fast enough that it is nearly indistinguishable from including those attributes statically within the HTML document.

Since all of the remaining code is in the form of event listeners, there is no logical progression to the next piece of code we will examine. Thus, let’s pick one at random and look at the code that handles the focusout event for our input elements:

$('.name').on('focusout', function(event) {    var nameField = $(event.target);    webConsole("Name field '" +                nameField.attr('id') +                "' was updated to '" +                nameField.val() +                "''"); });

Upon losing focus (presumably because the user entered some data into the <form> element), the focusout event will be triggered and our function called. The function then examines the element that triggered the event (by using the target property of the passed event object) and creates a message using the webConsole function previously explained. The result is a real-time updating of the web page every time the user changes the input of either form element. You can see some examples of these messages in Figure 23.1.

Figure 23.1  Performing actions in the jQuery-enabled form shows a log to the user

504

Chapter 23  Integrating JavaScript and PHP 

The final event we listen to in our jQuery script is the submit event, which is triggered when the form itself is submitted. Our selector specifies this listener should be limited to only the form whose ID is myForm and is as follows:

$('#myForm').on('submit', function(event) {    var first_name = $('#first_name').val();    var last_name = $('#last_name').val();

    webConsole("The form was submitted");    alert("Hello, " + first_name + " " + last_name + "!");});

Again, this event listener is simplistic for example purposes, and only extracts the final value of each input field before displaying it as an alert modal using the native JavaScript alert function. It then updates the HTML page itself to reflect that the form was submitted.

So wraps up our brief introduction to the fundamentals of jQuery. This is by no means whatsoever a comprehensive explanation of all the power of even the basic tools provided by jQuery, but it should provide sufficient understanding to proceed with the focus of this chapter: using jQuery to communicate with a backend PHP server using AJAX. 

Using jQuery and AJAX with PHPAlong with all of the powerful HTML document manipulation available to jQuery developers comes an entire suite of functionality dedicated to communicate asynchronously with backend web servers. This functionality is built into the implementation of JavaScript within the web browser, but using jQuery makes it easier because each browser tends to do things slightly differently and jQuery kindly abstracts those details away into a consistent API. The result is you can expect your logic to function similarly across the entirety of browser implementations, with few (and not really notable) exceptions.

To get started with AJAX and jQuery, we are going to build a simple web-based real-time chat application. This application will allow multiple users to concurrently chat with each other from their browsers, and receive these messages without having to refresh the browser window at all.

The AJAX-Enabled Chat Script/ServerTo handle the chat functionality on the server side, we need a simple PHP script that does two things: accept messages to send and return a list of messages that have not yet been seen by the user. Since we are building this as an AJAX application our PHP will function strictly using JavaScript Object Notation (JSON) for all output as well. Since a chat application needs some sort of persistent storage available to it, we will need to create a table in MySQL to handle it. 

As a precondition to creating the PHP script, create a table in MySQL using the following SQL CREATE queries to create a database called chat and a table in that database called chatlog:

Using jQuery and AJAX with PHP

505

CREATE DATABASE chat;USE chat;CREATE TABLE chatlog (     id INT(11) AUTO_INCREMENT PRIMARY KEY,      message TEXT,      sent_by VARCHAR(50),     date_created INT(11));

This rudimentary database table stores the basic metadata about the chat plus the message itself. The four columns are the uniquely identifying record ID, the message itself, the PHP session ID of the user who sent the message, and an integer field meant to hold the UNIX timestamp for when the message was submitted. The PHP session ID is important because we will use that value to determine if a chat message was sent by the user viewing the chat or another user entirely. 

The code in Listing 23.3 is the entirety of the script used to create and display a chat. We’ll step through the code directly after the listing.

Listing 23.3  chat.php—Backend PHP Script to Create and Display a Chat<?phpsession_start();ob_start();header("Content-type: application/json");

date_default_timezone_set('UTC');

//connect to database$db = mysqli_connect('localhost', 'your_user', 'your_password', 'chat');

if (mysqli_connect_errno()) {   echo '<p>Error: Could not connect to database.<br/>   Please try again later.</p>';   exit;}

try {

    $currentTime = time();    $session_id = session_id();

    $lastPoll = isset($_SESSION['last_poll']) ?                       $_SESSION['last_poll'] : $currentTime;

    $action = isset($_SERVER['REQUEST_METHOD']) &&               ($_SERVER['REQUEST_METHOD'] == 'POST') ?               'send' : 'poll';

506

Chapter 23  Integrating JavaScript and PHP 

    switch($action) {        case 'poll':

           $query = "SELECT * FROM chatlog WHERE                      date_created >= ?";

           $stmt = $db->prepare($query);           $stmt->bind_param('s', $lastPoll);             $stmt->execute();           $stmt->bind_result($id, $message, $session_id, $date_created);           $result = $stmt->get_result();

           $newChats = [];           while($chat = $result->fetch_assoc()) {

               if($session_id == $chat['sent_by']) {                  $chat['sent_by'] = 'self';               } else {                  $chat['sent_by'] = 'other';               }

               $newChats[] = $chat;            }

           $_SESSION['last_poll'] = $currentTime;

           print json_encode([               'success' => true,               'messages' => $newChats           ]);           exit;

        case 'send':

            $message = isset($_POST['message']) ? $_POST['message'] : '';            $message = strip_tags($message);

            $query = "INSERT INTO chatlog (message, sent_by, date_created)                      VALUES(?, ?, ?)";

            $stmt = $db->prepare($query);            $stmt->bind_param('ssi', $message, $session_id, $currentTime);            $stmt->execute(); 

            print json_encode(['success' => true]);            exit;    }

Using jQuery and AJAX with PHP

507

} catch(\Exception $e) {    print json_encode([        'success' => false,        'error' => $e->getMessage()    ]);

}

We start our simple chat server by enabling sessions and output buffing by calls to the session_start() and ob_start() functions. We then set a Content-Type response header with the value of application/json to ensure the requesting client knows we will be  returning a JSON document as a response. So that your chat timestamps are all lined up, you use date_default_timezone_set() to match the timezone for our server. 

With the basics out of the way, we then open a database connection to MySQL and check to see that the connection is good—if it is not, we exit immediately because a lack of a database at this stage means a pretty boring chat with no saved messages to display to any user.

However, with our database connection ready, we next figure out exactly how the script should respond to the request at hand. In our case, we are going to define the action we take by the nature of the request we receive from the user interface. For HTTP GET requests, we will retrieve a list of messages that have yet to be seen by the user and return them to the screen. For HTTP POST requests (form submissions), we will accept a new message to be broadcast to all the other users.

Regardless of the nature of the request, this script always returns a JSON object that has a key called success that will be either a Boolean true or false depending on the success of the operation. If false, we will also provide an error key with an error message. If we are handling an HTTP GET operation we will additionally return a messages key containing a list of messages the client should render.

Listing 23.2 is a simple PHP script that employs several concepts you have seen throughout this book to insert or retrieve information from a database. The key to this script, however, is in how it is executed. The intention is that this script will be executed at regular intervals by the user’s browser via AJAX to update the interface with any messages received. Concurrently, the browser interface will also provide the ability to send a message using AJAX back to the server to be broadcast to anyone else looking in on the chat as well. Let’s move on now by taking a look at the client side of our application and the AJAX methods that we will use.

The jQuery AJAX MethodsBefore we actually build the simple user interface for our chat application, let’s return to the discussion of using jQuery by introducing the various methods available to us for performing AJAX requests. Fundamentally, the AJAX methods you’ll learn about in the next sections are all simplified versions of a single API method—the $.ajax() method. 

508

Chapter 23  Integrating JavaScript and PHP 

The jQuery $.ajax() MethodFrom a prototype perspective, the $.ajax() method is rather simple:

$.ajax(string url, object settings);

The first parameter of the method is the URL against which you want to perform the asynchronous request, and the second parameter includes any settings for that request. The complexity of this method doesn’t reveal itself until you examine the numerous settings that are available to control basically every detail of that request and its response. Since all of these various settings are well-documented in the jQuery documentation for the method, we won’t discuss every single one of them here—feel free to peruse http://api.jquery.com/jQuery.ajax/ at a later date. Rather, we will introduce a few common use cases and how they are achieved using the $.ajax() method.

The first example performs a simple HTTP GET request. The success property is a function that is called upon success of the request, and is populated with the data retrieved during the request, the textual status of the request, and the jQuery request object itself. 

// Perform a HTTP GET request$.ajax('/example.php', {    'method' : 'GET',    'success' : function(data, textStatus, jqXHR) {        console.log(data);    }});

The next example performs a HTTP POST request that includes some data sent to the server. Upon success, just as was true with our earlier GET request, the function attached to the success property is called. However, in this case, we also have a function attached to the error property. This function is called in the event of an error (such as the server returning a HTTP 500 status), and its results can be used to inform the user interface:

// Perform an HTTP POST request with error handling$.ajax('/example.php', {    'method' : 'POST',    'data' : {        'myBoolean': true,        'myString' : 'This is some sample data.'    },    'success' : function(data, textStatus, jqXHR) {        console.log(data);    },    'error' : function(jqXHR, textStatus, errorThrown) {        console.log("An error occurred: " + errorThrown);    }});

If you would like to add headers to your HTTP request, such as to add authentication values, you can do so as well by using the headers setting and specifying the key / value pairs of the headers you wish to send, as below:

Using jQuery and AJAX with PHP

509

// Sending headers with a GET request$.ajax('/example.php', {     'method' : 'GET',     'headers' : {         'X-my-auth' : 'SomeAuthValue'     }    success: function(data, textStatus, jqXHR) {        console.log(data);    }});

In modern versions of jQuery, when specifically using the HTTP authentication protocol during an AJAX request, you no longer need to send HTTP authentication headers yourself before sending them in the request. Rather, you can simply use the username and password settings to specify the HTTP authentication credentials:

// Make a request using HTTP Auth$.ajax('/example.php', {    'method' : 'GET',    'username' : 'myusername',    'password' : 'mypassword',    'success' : function(data, textStatus, jqXHR) {        console.log(data);    }});

Depending on the complexity of your AJAX requests, and how closely you want to control the request itself, you may be able to use one of the various AJAX helper-methods instead of the complexity of the $.ajax() method and all of its settings. In the next section we’ll walk you through some simplified AJAX methods for making requests to a web server, before jumping in to complete your jQuery and PHP-driven chat application.

jQuery AJAX Helper MethodsIn many cases the flexibility and complexity provided by the $.ajax() method described above are a bit of an overkill for the needs of the developer. For this reason, jQuery provides several AJAX helper methods that encapsulate common use cases. The ease of use of these methods does come at a price, as they sometimes lack useful functionality like error handling that is built in to the $.ajax() method.

For example, the following is a considerably more straightforward way to perform a HTTP GET request for a resource on the server:

// Simplified GET requests$.get('/example.php', {      'queryParam' : 'paramValue'}, function(data, textStatus, jqXHR) {    console.log(data);});

510

Chapter 23  Integrating JavaScript and PHP 

Using the $.get() method, we simply pass the URL we are requesting, any query parameters (in the form of a generic JavaScript object), and the callback to use when the request returns successfully. If an error occurs while performing the request, the $.get() method silently fails. 

As one might expect, there is a corresponding $.post()method that functions in an identical fashion (except performing a HTTP POST request instead):

// Simplified POST requests$.post('/example.php', {     'postParam' : 'paramValue'}, function(data, textStatus, jqXHR) {    console.log(data););

There are two additional methods that can be useful under certain circumstances beyond the simple HTTP GET and HTTP POST. The first is the $.getScript() method, which dynamically loads a JavaScript document from the server and executes it in a single command:

$.getScript('/path/to/my.js', function() {      // my.js has been loaded and any functions / objects defined can now be used});

In a similar fashion, the $.getJSON() method performs an HTTP GET request to the specified URI, parses the return value as a JSON document, and then makes it available to the callback specified:

// Load a JSON document via HTTP GET$.getJSON('/example.php', {     'jsonParam' : 'paramValue'}, function(data, textStatus, jqXHR) {     console.log(data.status);});

With this brief introduction to jQuery and its AJAX functionality, let’s continue on and finish the web-based chat client based on these technologies.

The Chat Client/jQuery ApplicationWe have the backend script (chat.php from Listing 23.3) all ready, so now we need to build a jQuery-based front end to display a meaningful user interface to the end user—one that allows both input and retrieval of messages. For these purposes we will start by building a simple HTML interface using the Bootstrap CSS framework for its layout and a little customized CSS to render the popular「chat bubble」style of widget for each chat message we display (see Listing 23.4).

NoteFor the CSS styling used to render the fancy-looking chat bubbles we used a great online tool by designer John Clifford called "Bubbler," which can be found at http://ilikepixels.co.uk/drop/bubbler/.

 

 

Using jQuery and AJAX with PHP

511

Listing 23.4  chat.html—The Front End Chat Interface<!DOCTYPE html><html>    <head>        <title>AJAX Chat</title>        <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css">        <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap-theme.min.css">        <style>            .bubble-recv            {              position: relative;              width: 330px;              height: 75px;              padding: 10px;              background: #AEE5FF;              -webkit-border-radius: 10px;              -moz-border-radius: 10px;              border-radius: 10px;              border: #000000 solid 1px;              margin-bottom: 10px;            }

            .bubble-recv:after             {              content: '';              position: absolute;              border-style: solid;              border-width: 15px 15px 15px 0;              border-color: transparent #AEE5FF;              display: block;              width: 0;              z-index: 1;              left: -15px;              top: 12px;            }

            .bubble-recv:before             {              content: '';              position: absolute;              border-style: solid;              border-width: 15px 15px 15px 0;              border-color: transparent #000000;              display: block;              width: 0;              z-index: 0;

512

Chapter 23  Integrating JavaScript and PHP 

              left: -16px;              top: 12px;            }

            .bubble-sent            {              position: relative;              width: 330px;              height: 75px;              padding: 10px;              background: #00E500;              -webkit-border-radius: 10px;              -moz-border-radius: 10px;              border-radius: 10px;              border: #000000 solid 1px;              margin-bottom: 10px;            }

            .bubble-sent:after             {              content: '';              position: absolute;              border-style: solid;              border-width: 15px 0 15px 15px;              border-color: transparent #00E500;              display: block;              width: 0;              z-index: 1;              right: -15px;              top: 12px;            }

            .bubble-sent:before             {              content: '';              position: absolute;              border-style: solid;              border-width: 15px 0 15px 15px;              border-color: transparent #000000;              display: block;              width: 0;              z-index: 0;              right: -16px;              top: 12px;            }

            .spinner {              display: inline-block;

Using jQuery and AJAX with PHP

513

              opacity: 0;              width: 0;

              -webkit-transition: opacity 0.25s, width 0.25s;              -moz-transition: opacity 0.25s, width 0.25s;              -o-transition: opacity 0.25s, width 0.25s;              transition: opacity 0.25s, width 0.25s;            }

            .has-spinner.active {              cursor:progress;            }

            .has-spinner.active .spinner {              opacity: 1;              width: auto;             }

            .has-spinner.btn-mini.active .spinner {              width: 10px;            }

            .has-spinner.btn-small.active .spinner {              width: 13px;            }

            .has-spinner.btn.active .spinner {              width: 16px;            }

            .has-spinner.btn-large.active .spinner {              width: 19px;            }

            .panel-body {              padding-right: 35px;              padding-left: 35px;            }

        </style>    </head>    <body>    <h1 style="text-align:center">AJAX Chat</h1>    <div class="container">        <div class="panel panel-default">            <div class="panel-heading">                <h2 class="panel-title">Let's Chat</h2>            </div>            <div class="panel-body" id="chatPanel">

514

Chapter 23  Integrating JavaScript and PHP 

            </div>            <div class="panel-footer">                <div class="input-group">                    <input type="text" class="form-control" id="chatMessage" placeholder="Send a message here..."/>                    <span class="input-group-btn">                        <button id="sendMessageBtn" class="btn btn-primary has-spinner" type="button">                            <span class="spinner"><i class="icon-spin icon-refresh"></i></span>                            Send                        </button>                    </span>                </div>            </div>        </div>    </div>        <script src="//code.jquery.com/jquery-2.2.3.min.js"></script>    <script src="client.js"></script>    </body></html>

When rendered, you will be presented with a simple interface that will look something like Figure 23.2, depending on the conversation you have ongoing (note the first time you render it no chat messages will be displayed).

Figure 23.2  The AJAX chat in action

Using jQuery and AJAX with PHP

515

In order to take a static HTML document loaded by the browser and bring it to life, we need to implement client-side JavaScript logic to connect it to our backend PHP script and render our messages. This is all done within the client.js JavaScript file referenced in our HTML document. 

This JavaScript application is responsible for polling the PHP script at regular intervals to retrieve messages, then rendering each of those messages as a new chat bubble in the user  interface. Additionally, the script binds itself to the click event of the「Send」button and takes the typed message and sends it to the server to be rendered in the user interface.

In order to enable polling of our PHP script, we need to use something called a JavaScript timeout. The timeout is a feature of JavaScript that delays the execution of a function for a  pre-determined amount of time, and then executes the function when that time is up. In our script we have called this function pollServer, and it is defined as follows:

var pollServer = function() {    $.get('chat.php', function(result) {

        if(!result.success) {            console.log("Error polling server for new messages!");            return;        }

        $.each(result.messages, function(idx) {

            var chatBubble;

            if(this.sent_by == 'self') {                chatBubble = $('<div class="row bubble-sent pull-right">' +                                this.message +                                '</div><div class="clearfix"></div>');            } else {                chatBubble = $('<div class="row bubble-recv">' +                                this.message +                                '</div><div class="clearfix"></div>');            }

            $('#chatPanel').append(chatBubble);        });

        setTimeout(pollServer, 5000);    });}

Fundamentally the pollServer() function does two things: it performs an asynchronous HTTP GET request to the backend PHP script to request new messages, and then it calls the setTimeout() function to schedule the pollServer() function to be called again in 5 seconds. Throughout the execution of the pollServer() function, the HTTP GET request is 

516

Chapter 23  Integrating JavaScript and PHP 

triggered and completed, and the closure passed into the jQuery $.get() method is executed. This closure will examine the result, loop through each message, and add it to our web  interface using the proper CSS classes. 

The pollServer() function only needs to be called once to begin the cycle of polling for new chat messages, and this is best done once the HTML document is fully loaded. Thus, we attach a handler to the jQuery ready event to trigger the start of the polling process. Just to add a bit of flair to the user interface, we have also added a handler to the click event of all buttons on the page, which toggles the active class on and off when clicked.

$(document).on('ready', function() {    pollServer();

    $('button').click(function() {        $(this).toggleClass('active');    });});

Finally, we see the code responsible for sending a message to our backend PHP script. This code is part of the click handler for the send button on our HTML interface, which sends the message to the backend PHP script via HTTP POST for distribution to other polling clients.

$('#sendMessageBtn').on('click', function(event) {    event.preventDefault();

    var message = $('#chatMessage').val();

    $.post('chat.php', {        'message' : message    }, function(result) {

        $('#sendMessageBtn').toggleClass('active');

        if(!result.success) {            alert("There was an error sending your message");        } else {            console.log("Message sent!");            $('#chatMessage').val('');        }    });

});

Putting these relatively simple methods into a nice neat JavaScript file (in our case, called client.js) and then loading it from our page is all we need to make our chat application come to life. Although this chat application does not provide up-to-the-second updates (it is a 5 second update), this page allows you and your friends to chat with each other in real-time without ever having to reload the page.

Next

517

If you are following along on your own and use the Google Chrome browser, you can  simulate this easily as well simply by opening two browser windows (one in normal mode, one in incognito mode). As long as each connecting browser has a different PHP session ID assigned to it, you can have as many participants as you desire.

Further ReadingThis chapter’s introduction to AJAX approaches to web development has only scratched the surface of the possibilities available to you. While we have laid a solid foundation for you to build from, the subject of jQuery fills entire books on its own. That being said, with what you have been introduced to here, you should be well on your way to implementing these technologies into your own applications. 

If you are interested in studying them further, jQuery provides an extensive series of articles and tutorials on a variety of topics at its website: http://learn.jquery.com.

NextWe’re almost finished with this part of the book. Before we move on to the projects, we briefly discuss some of the useful odds and ends of PHP that we haven’t covered elsewhere.

This page intentionally left blank 

