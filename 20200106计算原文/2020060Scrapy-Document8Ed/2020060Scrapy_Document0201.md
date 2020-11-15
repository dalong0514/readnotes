# 02 Basic concepts

Command line tool

New in version 0.10.

Scrapy is controlled through the scrapy command-line tool, to be referred here as the「Scrapy tool」to differentiate it from the sub-commands, which we just call「commands」or「Scrapy commands」.

The Scrapy tool provides several commands, for multiple purposes, and each one accepts a different set of arguments and options.

(The scrapy deploy command has been removed in 1.0 in favor of the standalone scrapyd-deploy. See Deploying your project [https://scrapyd.readthedocs.io/en/latest/deploy.html].)

Configuration settings

Scrapy will look for configuration parameters in ini-style scrapy.cfg files in standard locations:

/etc/scrapy.cfg or c:\scrapy\scrapy.cfg (system-wide),

~/.config/scrapy.cfg ($XDG_CONFIG_HOME) and ~/.scrapy.cfg ($HOME) for global (user-wide) settings, and

scrapy.cfg inside a scrapy project’s root (see next section).

Settings from these files are merged in the listed order of preference: user-defined values have higher priority than system-wide defaults and project-wide settings will override all others, when defined.

Scrapy also understands, and can be configured through, a number of environment variables. Currently these are:

SCRAPY_SETTINGS_MODULE (see Designating the settings)

SCRAPY_PROJECT (see Sharing the root directory between projects)

SCRAPY_PYTHON_SHELL (see Scrapy shell)

Default structure of Scrapy projects

Before delving into the command-line tool and its sub-commands, let’s first understand the directory structure of a Scrapy project.

Though it can be modified, all Scrapy projects have the same file structure by default, similar to this:

scrapy.cfg myproject/ __init__.py items.py middlewares.py pipelines.py settings.py spiders/ __init__.py spider1.py spider2.py ...

The directory where the scrapy.cfg file resides is known as the project root directory. That file contains the name of the python module that defines the project settings. Here is an example:

[settings] default = myproject.settings

Sharing the root directory between projects

A project root directory, the one that contains the scrapy.cfg, may be shared by multiple Scrapy projects, each with its own settings module.

In that case, you must define one or more aliases for those settings modules under [settings] in your scrapy.cfg file:

[settings] default = myproject1.settings project1 = myproject1.settings project2 = myproject2.settings

By default, the scrapy command-line tool will use the default settings. Use the SCRAPY_PROJECT environment variable to specify a different project for scrapy to use:

$ scrapy settings --get BOT_NAME Project 1 Bot $ export SCRAPY_PROJECT=project2 $ scrapy settings --get BOT_NAME Project 2 Bot

Using the scrapy tool

You can start by running the Scrapy tool with no arguments and it will print some usage help and the available commands:

Scrapy X.Y - no active project Usage: scrapy <command> [options] [args] Available commands: crawl Run a spider fetch Fetch a URL using the Scrapy downloader [...]

The first line will print the currently active project if you’re inside a Scrapy project. In this example it was run from outside a project. If run from inside a project it would have printed something like this:

Scrapy X.Y - project: myproject Usage: scrapy <command> [options] [args] [...]

Creating projects

The first thing you typically do with the scrapy tool is create your Scrapy project:

scrapy startproject myproject [project_dir]

That will create a Scrapy project under the project_dir directory. If project_dir wasn’t specified, project_dir will be the same as myproject.

Next, you go inside the new project directory:

cd project_dir

And you’re ready to use the scrapy command to manage and control your project from there.

Controlling projects

You use the scrapy tool from inside your projects to control and manage them.

For example, to create a new spider:

scrapy genspider mydomain mydomain.com

Some Scrapy commands (like crawl) must be run from inside a Scrapy project. See the commands reference below for more information on which commands must be run from inside projects, and which not.

Also keep in mind that some commands may have slightly different behaviours when running them from inside projects. For example, the fetch command will use spider-overridden behaviours (such as the user_agent attribute to override the user-agent) if the url being fetched is associated with some specific spider. This is intentional, as the fetch command is meant to be used to check how spiders are downloading pages.

Available tool commands

This section contains a list of the available built-in commands with a description and some usage examples. Remember, you can always get more info about each command by running:

scrapy <command> -h

And you can see all available commands with:

scrapy -h

There are two kinds of commands, those that only work from inside a Scrapy project (Project-specific commands) and those that also work without an active Scrapy project (Global commands), though they may behave slightly different when running from inside a project (as they would use the project overridden settings).

Global commands:

startproject

genspider

settings

runspider

shell

fetch

view

version

Project-only commands:

crawl

check

list

edit

parse

bench

startproject

Syntax: scrapy startproject <project_name> [project_dir]

Requires project: no

Creates a new Scrapy project named project_name, under the project_dir directory. If project_dir wasn’t specified, project_dir will be the same as project_name.

Usage example:

$ scrapy startproject myproject

genspider

Syntax: scrapy genspider [-t template] <name> <domain>

Requires project: no

Create a new spider in the current folder or in the current project’s spiders folder, if called from inside a project. The <name> parameter is set as the spider’s name, while <domain> is used to generate the allowed_domains and start_urls spider’s attributes.

Usage example:

$ scrapy genspider -l Available templates: basic crawl csvfeed xmlfeed $ scrapy genspider example example.com Created spider 'example' using template 'basic' $ scrapy genspider -t crawl scrapyorg scrapy.org Created spider 'scrapyorg' using template 'crawl'

This is just a convenience shortcut command for creating spiders based on pre-defined templates, but certainly not the only way to create spiders. You can just create the spider source code files yourself, instead of using this command.

crawl

Syntax: scrapy crawl <spider>

Requires project: yes

Start crawling using a spider.

Usage examples:

$ scrapy crawl myspider [ ... myspider starts crawling ... ]

check

Syntax: scrapy check [-l] <spider>

Requires project: yes

Run contract checks.

Usage examples:

$ scrapy check -l first_spider * parse * parse_item second_spider * parse * parse_item $ scrapy check [FAILED] first_spider:parse_item >>> 'RetailPricex' field is missing [FAILED] first_spider:parse >>> Returned 92 requests, expected 0..4

list

Syntax: scrapy list

Requires project: yes

List all available spiders in the current project. The output is one spider per line.

Usage example:

$ scrapy list spider1 spider2

edit

Syntax: scrapy edit <spider>

Requires project: yes

Edit the given spider using the editor defined in the EDITOR environment variable or (if unset) the EDITOR setting.

This command is provided only as a convenience shortcut for the most common case, the developer is of course free to choose any tool or IDE to write and debug spiders.

Usage example:

$ scrapy edit spider1

fetch

Syntax: scrapy fetch <url>

Requires project: no

Downloads the given URL using the Scrapy downloader and writes the contents to standard output.

The interesting thing about this command is that it fetches the page how the spider would download it. For example, if the spider has a USER_AGENT attribute which overrides the User Agent, it will use that one.

So this command can be used to「see」how your spider would fetch a certain page.

If used outside a project, no particular per-spider behaviour would be applied and it will just use the default Scrapy downloader settings.

Supported options:

--spider=SPIDER: bypass spider autodetection and force use of specific spider

--headers: print the response’s HTTP headers instead of the response’s body

--no-redirect: do not follow HTTP 3xx redirects (default is to follow them)

Usage examples:

$ scrapy fetch --nolog http://www.example.com/some/page.html [ ... html content here ... ] $ scrapy fetch --nolog --headers http://www.example.com/ {'Accept-Ranges': ['bytes'], 'Age': ['1263 '], 'Connection': ['close '], 'Content-Length': ['596'], 'Content-Type': ['text/html; charset=UTF-8'], 'Date': ['Wed, 18 Aug 2010 23:59:46 GMT'], 'Etag': ['"573c1-254-48c9c87349680"'], 'Last-Modified': ['Fri, 30 Jul 2010 15:30:18 GMT'], 'Server': ['Apache/2.2.3 (CentOS)']}

view

Syntax: scrapy view <url>

Requires project: no

Opens the given URL in a browser, as your Scrapy spider would「see」it. Sometimes spiders see pages differently from regular users, so this can be used to check what the spider「sees」and confirm it’s what you expect.

Supported options:

--spider=SPIDER: bypass spider autodetection and force use of specific spider

--no-redirect: do not follow HTTP 3xx redirects (default is to follow them)

Usage example:

$ scrapy view http://www.example.com/some/page.html [ ... browser starts ... ]

shell

Syntax: scrapy shell [url]

Requires project: no

Starts the Scrapy shell for the given URL (if given) or empty if no URL is given. Also supports UNIX-style local file paths, either relative with ./ or ../ prefixes or absolute file paths. See Scrapy shell for more info.

Supported options:

--spider=SPIDER: bypass spider autodetection and force use of specific spider

-c code: evaluate the code in the shell, print the result and exit

--no-redirect: do not follow HTTP 3xx redirects (default is to follow them); this only affects the URL you may pass as argument on the command line; once you are inside the shell, fetch(url) will still follow HTTP redirects by default.

Usage example:

$ scrapy shell http://www.example.com/some/page.html [ ... scrapy shell starts ... ] $ scrapy shell --nolog http://www.example.com/ -c '(response.status, response.url)' (200, 'http://www.example.com/') # shell follows HTTP redirects by default $ scrapy shell --nolog http://httpbin.org/redirect-to?url=http%3A%2F%2Fexample.com%2F -c '(response.status, response.url)' (200, 'http://example.com/') # you can disable this with --no-redirect # (only for the URL passed as command line argument) $ scrapy shell --no-redirect --nolog http://httpbin.org/redirect-to?url=http%3A%2F%2Fexample.com%2F -c '(response.status, response.url)' (302, 'http://httpbin.org/redirect-to?url=http%3A%2F%2Fexample.com%2F')

parse

Syntax: scrapy parse <url> [options]

Requires project: yes

Fetches the given URL and parses it with the spider that handles it, using the method passed with the --callback option, or parse if not given.

Supported options:

--spider=SPIDER: bypass spider autodetection and force use of specific spider

--a NAME=VALUE: set spider argument (may be repeated)

--callback or -c: spider method to use as callback for parsing the response

--meta or -m: additional request meta that will be passed to the callback request. This must be a valid json string. Example: –meta=’{「foo」:「bar」}’

--cbkwargs: additional keyword arguments that will be passed to the callback. This must be a valid json string. Example: –cbkwargs=’{「foo」:「bar」}’

--pipelines: process items through pipelines

--rules or -r: use CrawlSpider rules to discover the callback (i.e. spider method) to use for parsing the response

--noitems: don’t show scraped items

--nolinks: don’t show extracted links

--nocolour: avoid using pygments to colorize the output

--depth or -d: depth level for which the requests should be followed recursively (default: 1)

--verbose or -v: display information for each depth level

Usage example:

$ scrapy parse http://www.example.com/ -c parse_item [ ... scrapy log lines crawling example.com spider ... ] >>> STATUS DEPTH LEVEL 1 <<< # Scraped Items ------------------------------------------------------------ [{'name': 'Example item', 'category': 'Furniture', 'length': '12 cm'}] # Requests ----------------------------------------------------------------- []

settings

Syntax: scrapy settings [options]

Requires project: no

Get the value of a Scrapy setting.

If used inside a project it’ll show the project setting value, otherwise it’ll show the default Scrapy value for that setting.

Example usage:

$ scrapy settings --get BOT_NAME scrapybot $ scrapy settings --get DOWNLOAD_DELAY 0

runspider

Syntax: scrapy runspider <spider_file.py>

Requires project: no

Run a spider self-contained in a Python file, without having to create a project.

Example usage:

$ scrapy runspider myspider.py [ ... spider starts crawling ... ]

version

Syntax: scrapy version [-v]

Requires project: no

Prints the Scrapy version. If used with -v it also prints Python, Twisted and Platform info, which is useful for bug reports.

bench

New in version 0.17.

Syntax: scrapy bench

Requires project: no

Run a quick benchmark test. Benchmarking.

Custom project commands

You can also add your custom project commands by using the COMMANDS_MODULE setting. See the Scrapy commands in scrapy/commands [https://github.com/scrapy/scrapy/tree/master/scrapy/commands] for examples on how to implement your commands.

COMMANDS_MODULE

Default: '' (empty string)

A module to use for looking up custom Scrapy commands. This is used to add custom commands for your Scrapy project.

Example:

COMMANDS_MODULE = 'mybot.commands'

Register commands via setup.py entry points

Note

This is an experimental feature, use with caution.

You can also add Scrapy commands from an external library by adding a scrapy.commands section in the entry points of the library setup.py file.

The following example adds my_command command:

from setuptools import setup, find_packages setup(name='scrapy-mymodule', entry_points={ 'scrapy.commands': [ 'my_command=my_scrapy_module.commands:MyCommand', ], }, )

Spiders

Spiders are classes which define how a certain site (or a group of sites) will be scraped, including how to perform the crawl (i.e. follow links) and how to extract structured data from their pages (i.e. scraping items). In other words, Spiders are the place where you define the custom behaviour for crawling and parsing pages for a particular site (or, in some cases, a group of sites).

For spiders, the scraping cycle goes through something like this:

You start by generating the initial Requests to crawl the first URLs, and specify a callback function to be called with the response downloaded from those requests.

The first requests to perform are obtained by calling the start_requests() method which (by default) generates Request for the URLs specified in the start_urls and the parse method as callback function for the Requests.

In the callback function, you parse the response (web page) and return either dicts with extracted data, Item objects, Request objects, or an iterable of these objects. Those Requests will also contain a callback (maybe the same) and will then be downloaded by Scrapy and then their response handled by the specified callback.

In callback functions, you parse the page contents, typically using Selectors (but you can also use BeautifulSoup, lxml or whatever mechanism you prefer) and generate items with the parsed data.

Finally, the items returned from the spider will be typically persisted to a database (in some Item Pipeline) or written to a file using Feed exports.

Even though this cycle applies (more or less) to any kind of spider, there are different kinds of default spiders bundled into Scrapy for different purposes. We will talk about those types here.

scrapy.Spider

class scrapy.spiders.Spider

This is the simplest spider, and the one from which every other spider must inherit (including spiders that come bundled with Scrapy, as well as spiders that you write yourself). It doesn’t provide any special functionality. It just provides a default start_requests() implementation which sends requests from the start_urls spider attribute and calls the spider’s method parse for each of the resulting responses.

name

A string which defines the name for this spider. The spider name is how the spider is located (and instantiated) by Scrapy, so it must be unique. However, nothing prevents you from instantiating more than one instance of the same spider. This is the most important spider attribute and it’s required.

If the spider scrapes a single domain, a common practice is to name the spider after the domain, with or without the TLD [https://en.wikipedia.org/wiki/Top-level_domain]. So, for example, a spider that crawls mywebsite.com would often be called mywebsite.

Note

In Python 2 this must be ASCII only.

allowed_domains

An optional list of strings containing domains that this spider is allowed to crawl. Requests for URLs not belonging to the domain names specified in this list (or their subdomains) won’t be followed if OffsiteMiddleware is enabled.

Let’s say your target url is https://www.example.com/1.html, then add 'example.com' to the list.

start_urls

A list of URLs where the spider will begin to crawl from, when no particular URLs are specified. So, the first pages downloaded will be those listed here. The subsequent Request will be generated successively from data contained in the start URLs.

custom_settings

A dictionary of settings that will be overridden from the project wide configuration when running this spider. It must be defined as a class attribute since the settings are updated before instantiation.

For a list of available built-in settings see: Built-in settings reference.

crawler

This attribute is set by the from_crawler() class method after initializating the class, and links to the Crawler object to which this spider instance is bound.

Crawlers encapsulate a lot of components in the project for their single entry access (such as extensions, middlewares, signals managers, etc). See Crawler API to know more about them.

settings

Configuration for running this spider. This is a Settings instance, see the Settings topic for a detailed introduction on this subject.

logger

Python logger created with the Spider’s name. You can use it to send log messages through it as described on Logging from Spiders.

from_crawler(crawler, *args, **kwargs)

This is the class method used by Scrapy to create your spiders.

You probably won’t need to override this directly because the default implementation acts as a proxy to the __init__() method, calling it with the given arguments args and named arguments kwargs.

Nonetheless, this method sets the crawler and settings attributes in the new instance so they can be accessed later inside the spider’s code.

Parameters

crawler (Crawler instance) – crawler to which the spider will be bound

args (list [https://docs.python.org/3/library/stdtypes.html#list]) – arguments passed to the __init__() method

kwargs (dict [https://docs.python.org/3/library/stdtypes.html#dict]) – keyword arguments passed to the __init__() method

start_requests()

This method must return an iterable with the first Requests to crawl for this spider. It is called by Scrapy when the spider is opened for scraping. Scrapy calls it only once, so it is safe to implement start_requests() as a generator.

The default implementation generates Request(url, dont_filter=True) for each url in start_urls.

If you want to change the Requests used to start scraping a domain, this is the method to override. For example, if you need to start by logging in using a POST request, you could do:

class MySpider(scrapy.Spider): name = 'myspider' def start_requests(self): return [scrapy.FormRequest("http://www.example.com/login", formdata={'user': 'john', 'pass': 'secret'}, callback=self.logged_in)] def logged_in(self, response): # here you would extract links to follow and return Requests for # each of them, with another callback pass

parse(response)

This is the default callback used by Scrapy to process downloaded responses, when their requests don’t specify a callback.

The parse method is in charge of processing the response and returning scraped data and/or more URLs to follow. Other Requests callbacks have the same requirements as the Spider class.

This method, as well as any other Request callback, must return an iterable of Request and/or dicts or Item objects.

Parameters

response (Response) – the response to parse

log(message[, level, component])

Wrapper that sends a log message through the Spider’s logger, kept for backward compatibility. For more information see Logging from Spiders.

closed(reason)

Called when the spider closes. This method provides a shortcut to signals.connect() for the spider_closed signal.

Let’s see an example:

import scrapy class MySpider(scrapy.Spider): name = 'example.com' allowed_domains = ['example.com'] start_urls = [ 'http://www.example.com/1.html', 'http://www.example.com/2.html', 'http://www.example.com/3.html', ] def parse(self, response): self.logger.info('A response from %s just arrived!', response.url)

Return multiple Requests and items from a single callback:

import scrapy class MySpider(scrapy.Spider): name = 'example.com' allowed_domains = ['example.com'] start_urls = [ 'http://www.example.com/1.html', 'http://www.example.com/2.html', 'http://www.example.com/3.html', ] def parse(self, response): for h3 in response.xpath('//h3').getall(): yield {"title": h3} for href in response.xpath('//a/@href').getall(): yield scrapy.Request(response.urljoin(href), self.parse)

Instead of start_urls you can use start_requests() directly; to give data more structure you can use Items:

import scrapy from myproject.items import MyItem class MySpider(scrapy.Spider): name = 'example.com' allowed_domains = ['example.com'] def start_requests(self): yield scrapy.Request('http://www.example.com/1.html', self.parse) yield scrapy.Request('http://www.example.com/2.html', self.parse) yield scrapy.Request('http://www.example.com/3.html', self.parse) def parse(self, response): for h3 in response.xpath('//h3').getall(): yield MyItem(title=h3) for href in response.xpath('//a/@href').getall(): yield scrapy.Request(response.urljoin(href), self.parse)

Spider arguments

Spiders can receive arguments that modify their behaviour. Some common uses for spider arguments are to define the start URLs or to restrict the crawl to certain sections of the site, but they can be used to configure any functionality of the spider.

Spider arguments are passed through the crawl command using the -a option. For example:

scrapy crawl myspider -a category=electronics

Spiders can access arguments in their __init__ methods:

import scrapy class MySpider(scrapy.Spider): name = 'myspider' def __init__(self, category=None, *args, **kwargs): super(MySpider, self).__init__(*args, **kwargs) self.start_urls = ['http://www.example.com/categories/%s' % category] # ...

The default __init__ method will take any spider arguments and copy them to the spider as attributes. The above example can also be written as follows:

import scrapy class MySpider(scrapy.Spider): name = 'myspider' def start_requests(self): yield scrapy.Request('http://www.example.com/categories/%s' % self.category)

Keep in mind that spider arguments are only strings. The spider will not do any parsing on its own. If you were to set the start_urls attribute from the command line, you would have to parse it on your own into a list using something like ast.literal_eval [https://docs.python.org/library/ast.html#ast.literal_eval] or json.loads [https://docs.python.org/library/json.html#json.loads] and then set it as an attribute. Otherwise, you would cause iteration over a start_urls string (a very common python pitfall) resulting in each character being seen as a separate url.

A valid use case is to set the http auth credentials used by HttpAuthMiddleware or the user agent used by UserAgentMiddleware:

scrapy crawl myspider -a http_user=myuser -a http_pass=mypassword -a user_agent=mybot

Spider arguments can also be passed through the Scrapyd schedule.json API. See Scrapyd documentation [https://scrapyd.readthedocs.io/en/latest/].

Generic Spiders

Scrapy comes with some useful generic spiders that you can use to subclass your spiders from. Their aim is to provide convenient functionality for a few common scraping cases, like following all links on a site based on certain rules, crawling from Sitemaps [https://www.sitemaps.org/index.html], or parsing an XML/CSV feed.

For the examples used in the following spiders, we’ll assume you have a project with a TestItem declared in a myproject.items module:

import scrapy class TestItem(scrapy.Item): id = scrapy.Field() name = scrapy.Field() description = scrapy.Field()

CrawlSpider

class scrapy.spiders.CrawlSpider

This is the most commonly used spider for crawling regular websites, as it provides a convenient mechanism for following links by defining a set of rules. It may not be the best suited for your particular web sites or project, but it’s generic enough for several cases, so you can start from it and override it as needed for more custom functionality, or just implement your own spider.

Apart from the attributes inherited from Spider (that you must specify), this class supports a new attribute:

rules

Which is a list of one (or more) Rule objects. Each Rule defines a certain behaviour for crawling the site. Rules objects are described below. If multiple rules match the same link, the first one will be used, according to the order they’re defined in this attribute.

This spider also exposes an overrideable method:

parse_start_url(response)

This method is called for the start_urls responses. It allows to parse the initial responses and must return either an Item object, a Request object, or an iterable containing any of them.

Crawling rules

class scrapy.spiders.Rule(link_extractor=None, callback=None, cb_kwargs=None, follow=None, process_links=None, process_request=None)

link_extractor is a Link Extractor object which defines how links will be extracted from each crawled page. Each produced link will be used to generate a Request object, which will contain the link’s text in its meta dictionary (under the link_text key). If omitted, a default link extractor created with no arguments will be used, resulting in all links being extracted.

callback is a callable or a string (in which case a method from the spider object with that name will be used) to be called for each link extracted with the specified link extractor. This callback receives a Response as its first argument and must return either a single instance or an iterable of Item, dict and/or Request objects (or any subclass of them). As mentioned above, the received Response object will contain the text of the link that produced the Request in its meta dictionary (under the link_text key)

Warning

When writing crawl spider rules, avoid using parse as callback, since the CrawlSpider uses the parse method itself to implement its logic. So if you override the parse method, the crawl spider will no longer work.

cb_kwargs is a dict containing the keyword arguments to be passed to the callback function.

follow is a boolean which specifies if links should be followed from each response extracted with this rule. If callback is None follow defaults to True, otherwise it defaults to False.

process_links is a callable, or a string (in which case a method from the spider object with that name will be used) which will be called for each list of links extracted from each response using the specified link_extractor. This is mainly used for filtering purposes.

process_request is a callable (or a string, in which case a method from the spider object with that name will be used) which will be called for every Request extracted by this rule. This callable should take said request as first argument and the Response from which the request originated as second argument. It must return a Request object or None (to filter out the request).

CrawlSpider example

Let’s now take a look at an example CrawlSpider with rules:

import scrapy from scrapy.spiders import CrawlSpider, Rule from scrapy.linkextractors import LinkExtractor class MySpider(CrawlSpider): name = 'example.com' allowed_domains = ['example.com'] start_urls = ['http://www.example.com'] rules = ( # Extract links matching 'category.php' (but not matching 'subsection.php') # and follow links from them (since no callback means follow=True by default). Rule(LinkExtractor(allow=('category\.php', ), deny=('subsection\.php', ))), # Extract links matching 'item.php' and parse them with the spider's method parse_item Rule(LinkExtractor(allow=('item\.php', )), callback='parse_item'), ) def parse_item(self, response): self.logger.info('Hi, this is an item page! %s', response.url) item = scrapy.Item() item['id'] = response.xpath('//td[@id="item_id"]/text()').re(r'ID: (\d+)') item['name'] = response.xpath('//td[@id="item_name"]/text()').get() item['description'] = response.xpath('//td[@id="item_description"]/text()').get() item['link_text'] = response.meta['link_text'] return item

This spider would start crawling example.com’s home page, collecting category links, and item links, parsing the latter with the parse_item method. For each item response, some data will be extracted from the HTML using XPath, and an Item will be filled with it.

XMLFeedSpider

class scrapy.spiders.XMLFeedSpider

XMLFeedSpider is designed for parsing XML feeds by iterating through them by a certain node name. The iterator can be chosen from: iternodes, xml, and html. It’s recommended to use the iternodes iterator for performance reasons, since the xml and html iterators generate the whole DOM at once in order to parse it. However, using html as the iterator may be useful when parsing XML with bad markup.

To set the iterator and the tag name, you must define the following class attributes:

iterator

A string which defines the iterator to use. It can be either:

'iternodes' - a fast iterator based on regular expressions

'html' - an iterator which uses Selector. Keep in mind this uses DOM parsing and must load all DOM in memory which could be a problem for big feeds

'xml' - an iterator which uses Selector. Keep in mind this uses DOM parsing and must load all DOM in memory which could be a problem for big feeds

It defaults to: 'iternodes'.

itertag

A string with the name of the node (or element) to iterate in. Example:

itertag = 'product'

namespaces

A list of (prefix, uri) tuples which define the namespaces available in that document that will be processed with this spider. The prefix and uri will be used to automatically register namespaces using the register_namespace() method.

You can then specify nodes with namespaces in the itertag attribute.

Example:

class YourSpider(XMLFeedSpider): namespaces = [('n', 'http://www.sitemaps.org/schemas/sitemap/0.9')] itertag = 'n:url' # ...

Apart from these new attributes, this spider has the following overrideable methods too:

adapt_response(response)

A method that receives the response as soon as it arrives from the spider middleware, before the spider starts parsing it. It can be used to modify the response body before parsing it. This method receives a response and also returns a response (it could be the same or another one).

parse_node(response, selector)

This method is called for the nodes matching the provided tag name (itertag). Receives the response and an Selector for each node. Overriding this method is mandatory. Otherwise, you spider won’t work. This method must return either a Item object, a Request object, or an iterable containing any of them.

process_results(response, results)

This method is called for each result (item or request) returned by the spider, and it’s intended to perform any last time processing required before returning the results to the framework core, for example setting the item IDs. It receives a list of results and the response which originated those results. It must return a list of results (Items or Requests).

XMLFeedSpider example

These spiders are pretty easy to use, let’s have a look at one example:

from scrapy.spiders import XMLFeedSpider from myproject.items import TestItem class MySpider(XMLFeedSpider): name = 'example.com' allowed_domains = ['example.com'] start_urls = ['http://www.example.com/feed.xml'] iterator = 'iternodes' # This is actually unnecessary, since it's the default value itertag = 'item' def parse_node(self, response, node): self.logger.info('Hi, this is a <%s> node!: %s', self.itertag, ''.join(node.getall())) item = TestItem() item['id'] = node.xpath('@id').get() item['name'] = node.xpath('name').get() item['description'] = node.xpath('description').get() return item

Basically what we did up there was to create a spider that downloads a feed from the given start_urls, and then iterates through each of its item tags, prints them out, and stores some random data in an Item.

CSVFeedSpider

class scrapy.spiders.CSVFeedSpider

This spider is very similar to the XMLFeedSpider, except that it iterates over rows, instead of nodes. The method that gets called in each iteration is parse_row().

delimiter

A string with the separator character for each field in the CSV file Defaults to ',' (comma).

quotechar

A string with the enclosure character for each field in the CSV file Defaults to '"' (quotation mark).

headers

A list of the column names in the CSV file.

parse_row(response, row)

Receives a response and a dict (representing each row) with a key for each provided (or detected) header of the CSV file. This spider also gives the opportunity to override adapt_response and process_results methods for pre- and post-processing purposes.

CSVFeedSpider example

Let’s see an example similar to the previous one, but using a CSVFeedSpider:

from scrapy.spiders import CSVFeedSpider from myproject.items import TestItem class MySpider(CSVFeedSpider): name = 'example.com' allowed_domains = ['example.com'] start_urls = ['http://www.example.com/feed.csv'] delimiter = ';' quotechar = "'" headers = ['id', 'name', 'description'] def parse_row(self, response, row): self.logger.info('Hi, this is a row!: %r', row) item = TestItem() item['id'] = row['id'] item['name'] = row['name'] item['description'] = row['description'] return item

SitemapSpider

class scrapy.spiders.SitemapSpider

SitemapSpider allows you to crawl a site by discovering the URLs using Sitemaps [https://www.sitemaps.org/index.html].

It supports nested sitemaps and discovering sitemap urls from robots.txt [http://www.robotstxt.org/].

sitemap_urls

A list of urls pointing to the sitemaps whose urls you want to crawl.

You can also point to a robots.txt [http://www.robotstxt.org/] and it will be parsed to extract sitemap urls from it.

sitemap_rules

A list of tuples (regex, callback) where:

regex is a regular expression to match urls extracted from sitemaps. regex can be either a str or a compiled regex object.

callback is the callback to use for processing the urls that match the regular expression. callback can be a string (indicating the name of a spider method) or a callable.

For example:

sitemap_rules = [('/product/', 'parse_product')]

Rules are applied in order, and only the first one that matches will be used.

If you omit this attribute, all urls found in sitemaps will be processed with the parse callback.

sitemap_follow

A list of regexes of sitemap that should be followed. This is only for sites that use Sitemap index files [https://www.sitemaps.org/protocol.html#index] that point to other sitemap files.

By default, all sitemaps are followed.

sitemap_alternate_links

Specifies if alternate links for one url should be followed. These are links for the same website in another language passed within the same url block.

For example:

<url> <loc>http://example.com/</loc> <xhtml:link rel="alternate" hreflang="de" href="http://example.com/de"/> </url>

With sitemap_alternate_links set, this would retrieve both URLs. With sitemap_alternate_links disabled, only http://example.com/ would be retrieved.

Default is sitemap_alternate_links disabled.

sitemap_filter(entries)

This is a filter function that could be overridden to select sitemap entries based on their attributes.

For example:

<url> <loc>http://example.com/</loc> <lastmod>2005-01-01</lastmod> </url>

We can define a sitemap_filter function to filter entries by date:

from datetime import datetime from scrapy.spiders import SitemapSpider class FilteredSitemapSpider(SitemapSpider): name = 'filtered_sitemap_spider' allowed_domains = ['example.com'] sitemap_urls = ['http://example.com/sitemap.xml'] def sitemap_filter(self, entries): for entry in entries: date_time = datetime.strptime(entry['lastmod'], '%Y-%m-%d') if date_time.year >= 2005: yield entry

This would retrieve only entries modified on 2005 and the following years.

Entries are dict objects extracted from the sitemap document. Usually, the key is the tag name and the value is the text inside it.

It’s important to notice that:

as the loc attribute is required, entries without this tag are discarded

alternate links are stored in a list with the key alternate (see sitemap_alternate_links)

namespaces are removed, so lxml tags named as {namespace}tagname become only tagname

If you omit this method, all entries found in sitemaps will be processed, observing other attributes and their settings.

SitemapSpider examples

Simplest example: process all urls discovered through sitemaps using the parse callback:

from scrapy.spiders import SitemapSpider class MySpider(SitemapSpider): sitemap_urls = ['http://www.example.com/sitemap.xml'] def parse(self, response): pass # ... scrape item here ...

Process some urls with certain callback and other urls with a different callback:

from scrapy.spiders import SitemapSpider class MySpider(SitemapSpider): sitemap_urls = ['http://www.example.com/sitemap.xml'] sitemap_rules = [ ('/product/', 'parse_product'), ('/category/', 'parse_category'), ] def parse_product(self, response): pass # ... scrape product ... def parse_category(self, response): pass # ... scrape category ...

Follow sitemaps defined in the robots.txt [http://www.robotstxt.org/] file and only follow sitemaps whose url contains /sitemap_shop:

from scrapy.spiders import SitemapSpider class MySpider(SitemapSpider): sitemap_urls = ['http://www.example.com/robots.txt'] sitemap_rules = [ ('/shop/', 'parse_shop'), ] sitemap_follow = ['/sitemap_shops'] def parse_shop(self, response): pass # ... scrape shop here ...

Combine SitemapSpider with other sources of urls:

from scrapy.spiders import SitemapSpider class MySpider(SitemapSpider): sitemap_urls = ['http://www.example.com/robots.txt'] sitemap_rules = [ ('/shop/', 'parse_shop'), ] other_urls = ['http://www.example.com/about'] def start_requests(self): requests = list(super(MySpider, self).start_requests()) requests += [scrapy.Request(x, self.parse_other) for x in self.other_urls] return requests def parse_shop(self, response): pass # ... scrape shop here ... def parse_other(self, response): pass # ... scrape other here ...

Selectors

When you’re scraping web pages, the most common task you need to perform is to extract data from the HTML source. There are several libraries available to achieve this, such as:

BeautifulSoup [https://www.crummy.com/software/BeautifulSoup/] is a very popular web scraping library among Python programmers which constructs a Python object based on the structure of the HTML code and also deals with bad markup reasonably well, but it has one drawback: it’s slow.

lxml [http://lxml.de/] is an XML parsing library (which also parses HTML) with a pythonic API based on ElementTree [https://docs.python.org/2/library/xml.etree.elementtree.html]. (lxml is not part of the Python standard library.)

Scrapy comes with its own mechanism for extracting data. They’re called selectors because they「select」certain parts of the HTML document specified either by XPath [https://www.w3.org/TR/xpath] or CSS [https://www.w3.org/TR/selectors] expressions.

XPath [https://www.w3.org/TR/xpath] is a language for selecting nodes in XML documents, which can also be used with HTML. CSS [https://www.w3.org/TR/selectors] is a language for applying styles to HTML documents. It defines selectors to associate those styles with specific HTML elements.

Note

Scrapy Selectors is a thin wrapper around parsel [https://parsel.readthedocs.io/] library; the purpose of this wrapper is to provide better integration with Scrapy Response objects.

parsel [https://parsel.readthedocs.io/] is a stand-alone web scraping library which can be used without Scrapy. It uses lxml [http://lxml.de/] library under the hood, and implements an easy API on top of lxml API. It means Scrapy selectors are very similar in speed and parsing accuracy to lxml.

Using selectors

Constructing selectors

Response objects expose a Selector instance on .selector attribute:

>>> response.selector.xpath('//span/text()').get() 'good'

Querying responses using XPath and CSS is so common that responses include two more shortcuts: response.xpath() and response.css():

>>> response.xpath('//span/text()').get() 'good' >>> response.css('span::text').get() 'good'

Scrapy selectors are instances of Selector class constructed by passing either TextResponse object or markup as an unicode string (in text argument). Usually there is no need to construct Scrapy selectors manually: response object is available in Spider callbacks, so in most cases it is more convenient to use response.css() and response.xpath() shortcuts. By using response.selector or one of these shortcuts you can also ensure the response body is parsed only once.

But if required, it is possible to use Selector directly. Constructing from text:

>>> from scrapy.selector import Selector >>> body = '<html><body><span>good</span></body></html>' >>> Selector(text=body).xpath('//span/text()').get() 'good'

Constructing from response - HtmlResponse is one of TextResponse subclasses:

>>> from scrapy.selector import Selector >>> from scrapy.http import HtmlResponse >>> response = HtmlResponse(url='http://example.com', body=body) >>> Selector(response=response).xpath('//span/text()').get() 'good'

Selector automatically chooses the best parsing rules (XML vs HTML) based on input type.

Using selectors

To explain how to use the selectors we’ll use the Scrapy shell (which provides interactive testing) and an example page located in the Scrapy documentation server:

https://docs.scrapy.org/en/latest/_static/selectors-sample1.html

For the sake of completeness, here’s its full HTML code:

<html> <head> <base href='http://example.com/' /> <title>Example website</title> </head> <body> <div id='images'> <a href='image1.html'>Name: My image 1 <br /><img src='image1_thumb.jpg' /></a> <a href='image2.html'>Name: My image 2 <br /><img src='image2_thumb.jpg' /></a> <a href='image3.html'>Name: My image 3 <br /><img src='image3_thumb.jpg' /></a> <a href='image4.html'>Name: My image 4 <br /><img src='image4_thumb.jpg' /></a> <a href='image5.html'>Name: My image 5 <br /><img src='image5_thumb.jpg' /></a> </div> </body> </html>

First, let’s open the shell:

scrapy shell https://docs.scrapy.org/en/latest/_static/selectors-sample1.html

Then, after the shell loads, you’ll have the response available as response shell variable, and its attached selector in response.selector attribute.

Since we’re dealing with HTML, the selector will automatically use an HTML parser.

So, by looking at the HTML code of that page, let’s construct an XPath for selecting the text inside the title tag:

>>> response.xpath('//title/text()') [<Selector xpath='//title/text()' data='Example website'>]

To actually extract the textual data, you must call the selector .get() or .getall() methods, as follows:

>>> response.xpath('//title/text()').getall() ['Example website'] >>> response.xpath('//title/text()').get() 'Example website'

.get() always returns a single result; if there are several matches, content of a first match is returned; if there are no matches, None is returned. .getall() returns a list with all results.

Notice that CSS selectors can select text or attribute nodes using CSS3 pseudo-elements:

>>> response.css('title::text').get() 'Example website'

As you can see, .xpath() and .css() methods return a SelectorList instance, which is a list of new selectors. This API can be used for quickly selecting nested data:

>>> response.css('img').xpath('@src').getall() ['image1_thumb.jpg', 'image2_thumb.jpg', 'image3_thumb.jpg', 'image4_thumb.jpg', 'image5_thumb.jpg']

If you want to extract only the first matched element, you can call the selector .get() (or its alias .extract_first() commonly used in previous Scrapy versions):

>>> response.xpath('//div[@id="images"]/a/text()').get() 'Name: My image 1 '

It returns None if no element was found:

>>> response.xpath('//div[@id="not-exists"]/text()').get() is None True

A default return value can be provided as an argument, to be used instead of None:

>>> response.xpath('//div[@id="not-exists"]/text()').get(default='not-found') 'not-found'

Instead of using e.g. '@src' XPath it is possible to query for attributes using .attrib property of a Selector:

>>> [img.attrib['src'] for img in response.css('img')] ['image1_thumb.jpg', 'image2_thumb.jpg', 'image3_thumb.jpg', 'image4_thumb.jpg', 'image5_thumb.jpg']

As a shortcut, .attrib is also available on SelectorList directly; it returns attributes for the first matching element:

>>> response.css('img').attrib['src'] 'image1_thumb.jpg'

This is most useful when only a single result is expected, e.g. when selecting by id, or selecting unique elements on a web page:

>>> response.css('base').attrib['href'] 'http://example.com/'

Now we’re going to get the base URL and some image links:

>>> response.xpath('//base/@href').get() 'http://example.com/' >>> response.css('base::attr(href)').get() 'http://example.com/' >>> response.css('base').attrib['href'] 'http://example.com/' >>> response.xpath('//a[contains(@href, "image")]/@href').getall() ['image1.html', 'image2.html', 'image3.html', 'image4.html', 'image5.html'] >>> response.css('a[href*=image]::attr(href)').getall() ['image1.html', 'image2.html', 'image3.html', 'image4.html', 'image5.html'] >>> response.xpath('//a[contains(@href, "image")]/img/@src').getall() ['image1_thumb.jpg', 'image2_thumb.jpg', 'image3_thumb.jpg', 'image4_thumb.jpg', 'image5_thumb.jpg'] >>> response.css('a[href*=image] img::attr(src)').getall() ['image1_thumb.jpg', 'image2_thumb.jpg', 'image3_thumb.jpg', 'image4_thumb.jpg', 'image5_thumb.jpg']

Extensions to CSS Selectors

Per W3C standards, CSS selectors [https://www.w3.org/TR/css3-selectors/#selectors] do not support selecting text nodes or attribute values. But selecting these is so essential in a web scraping context that Scrapy (parsel) implements a couple of non-standard pseudo-elements:

to select text nodes, use ::text

to select attribute values, use ::attr(name) where name is the name of the attribute that you want the value of

Warning

These pseudo-elements are Scrapy-/Parsel-specific. They will most probably not work with other libraries like lxml [http://lxml.de/] or PyQuery [https://pypi.python.org/pypi/pyquery].

Examples:

title::text selects children text nodes of a descendant <title> element:

>>> response.css('title::text').get() 'Example website'

*::text selects all descendant text nodes of the current selector context:

>>> response.css('#images *::text').getall() ['\n ', 'Name: My image 1 ', '\n ', 'Name: My image 2 ', '\n ', 'Name: My image 3 ', '\n ', 'Name: My image 4 ', '\n ', 'Name: My image 5 ', '\n ']

foo::text returns no results if foo element exists, but contains no text (i.e. text is empty):

>>> response.css('img::text').getall() []

This means .css('foo::text').get() could return None even if an element exists. Use default='' if you always want a string:

>>> response.css('img::text').get() >>> response.css('img::text').get(default='') ''

a::attr(href) selects the href attribute value of descendant links:

>>> response.css('a::attr(href)').getall() ['image1.html', 'image2.html', 'image3.html', 'image4.html', 'image5.html']

Note

See also: Selecting element attributes.

Note

You cannot chain these pseudo-elements. But in practice it would not make much sense: text nodes do not have attributes, and attribute values are string values already and do not have children nodes.

Nesting selectors

The selection methods (.xpath() or .css()) return a list of selectors of the same type, so you can call the selection methods for those selectors too. Here’s an example:

>>> links = response.xpath('//a[contains(@href, "image")]') >>> links.getall() ['<a href="image1.html">Name: My image 1 <br><img src="image1_thumb.jpg"></a>', '<a href="image2.html">Name: My image 2 <br><img src="image2_thumb.jpg"></a>', '<a href="image3.html">Name: My image 3 <br><img src="image3_thumb.jpg"></a>', '<a href="image4.html">Name: My image 4 <br><img src="image4_thumb.jpg"></a>', '<a href="image5.html">Name: My image 5 <br><img src="image5_thumb.jpg"></a>'] >>> for index, link in enumerate(links): ... args = (index, link.xpath('@href').get(), link.xpath('img/@src').get()) ... print('Link number %d points to url %r and image %r' % args) Link number 0 points to url 'image1.html' and image 'image1_thumb.jpg' Link number 1 points to url 'image2.html' and image 'image2_thumb.jpg' Link number 2 points to url 'image3.html' and image 'image3_thumb.jpg' Link number 3 points to url 'image4.html' and image 'image4_thumb.jpg' Link number 4 points to url 'image5.html' and image 'image5_thumb.jpg'

Selecting element attributes

There are several ways to get a value of an attribute. First, one can use XPath syntax:

>>> response.xpath("//a/@href").getall() ['image1.html', 'image2.html', 'image3.html', 'image4.html', 'image5.html']

XPath syntax has a few advantages: it is a standard XPath feature, and @attributes can be used in other parts of an XPath expression - e.g. it is possible to filter by attribute value.

Scrapy also provides an extension to CSS selectors (::attr(...)) which allows to get attribute values:

>>> response.css('a::attr(href)').getall() ['image1.html', 'image2.html', 'image3.html', 'image4.html', 'image5.html']

In addition to that, there is a .attrib property of Selector. You can use it if you prefer to lookup attributes in Python code, without using XPaths or CSS extensions:

>>> [a.attrib['href'] for a in response.css('a')] ['image1.html', 'image2.html', 'image3.html', 'image4.html', 'image5.html']

This property is also available on SelectorList; it returns a dictionary with attributes of a first matching element. It is convenient to use when a selector is expected to give a single result (e.g. when selecting by element ID, or when selecting an unique element on a page):

>>> response.css('base').attrib {'href': 'http://example.com/'} >>> response.css('base').attrib['href'] 'http://example.com/'

.attrib property of an empty SelectorList is empty:

>>> response.css('foo').attrib {}

Using selectors with regular expressions

Selector also has a .re() method for extracting data using regular expressions. However, unlike using .xpath() or .css() methods, .re() returns a list of unicode strings. So you can’t construct nested .re() calls.

Here’s an example used to extract image names from the HTML code above:

>>> response.xpath('//a[contains(@href, "image")]/text()').re(r'Name:\s*(.*)') ['My image 1', 'My image 2', 'My image 3', 'My image 4', 'My image 5']

There’s an additional helper reciprocating .get() (and its alias .extract_first()) for .re(), named .re_first(). Use it to extract just the first matching string:

>>> response.xpath('//a[contains(@href, "image")]/text()').re_first(r'Name:\s*(.*)') 'My image 1'

extract() and extract_first()

If you’re a long-time Scrapy user, you’re probably familiar with .extract() and .extract_first() selector methods. Many blog posts and tutorials are using them as well. These methods are still supported by Scrapy, there are no plans to deprecate them.

However, Scrapy usage docs are now written using .get() and .getall() methods. We feel that these new methods result in a more concise and readable code.

The following examples show how these methods map to each other.

SelectorList.get() is the same as SelectorList.extract_first():

>>> response.css('a::attr(href)').get() 'image1.html' >>> response.css('a::attr(href)').extract_first() 'image1.html'

SelectorList.getall() is the same as SelectorList.extract():

>>> response.css('a::attr(href)').getall() ['image1.html', 'image2.html', 'image3.html', 'image4.html', 'image5.html'] >>> response.css('a::attr(href)').extract() ['image1.html', 'image2.html', 'image3.html', 'image4.html', 'image5.html']

Selector.get() is the same as Selector.extract():

>>> response.css('a::attr(href)')[0].get() 'image1.html' >>> response.css('a::attr(href)')[0].extract() 'image1.html'

For consistency, there is also Selector.getall(), which returns a list:

>>> response.css('a::attr(href)')[0].getall() ['image1.html']

So, the main difference is that output of .get() and .getall() methods is more predictable: .get() always returns a single result, .getall() always returns a list of all extracted results. With .extract() method it was not always obvious if a result is a list or not; to get a single result either .extract() or .extract_first() should be called.

Working with XPaths

Here are some tips which may help you to use XPath with Scrapy selectors effectively. If you are not much familiar with XPath yet, you may want to take a look first at this XPath tutorial [http://www.zvon.org/comp/r/tut-XPath_1.html].

Note

Some of the tips are based on this post from ScrapingHub’s blog [https://blog.scrapinghub.com/2014/07/17/xpath-tips-from-the-web-scraping-trenches/].

Working with relative XPaths

Keep in mind that if you are nesting selectors and use an XPath that starts with /, that XPath will be absolute to the document and not relative to the Selector you’re calling it from.

For example, suppose you want to extract all <p> elements inside <div> elements. First, you would get all <div> elements:

>>> divs = response.xpath('//div')

At first, you may be tempted to use the following approach, which is wrong, as it actually extracts all <p> elements from the document, not only those inside <div> elements:

>>> for p in divs.xpath('//p'): # this is wrong - gets all <p> from the whole document ... print(p.get())

This is the proper way to do it (note the dot prefixing the .//p XPath):

>>> for p in divs.xpath('.//p'): # extracts all <p> inside ... print(p.get())

Another common case would be to extract all direct <p> children:

>>> for p in divs.xpath('p'): ... print(p.get())

For more details about relative XPaths see the Location Paths [https://www.w3.org/TR/xpath#location-paths] section in the XPath specification.

When querying by class, consider using CSS

Because an element can contain multiple CSS classes, the XPath way to select elements by class is the rather verbose:

*[contains(concat(' ', normalize-space(@class), ' '), ' someclass ')]

If you use @class='someclass' you may end up missing elements that have other classes, and if you just use contains(@class, 'someclass') to make up for that you may end up with more elements that you want, if they have a different class name that shares the string someclass.

As it turns out, Scrapy selectors allow you to chain selectors, so most of the time you can just select by class using CSS and then switch to XPath when needed:

>>> from scrapy import Selector >>> sel = Selector(text='<div class="hero shout"><time datetime="2014-07-23 19:00">Special date</time></div>') >>> sel.css('.shout').xpath('./time/@datetime').getall() ['2014-07-23 19:00']

This is cleaner than using the verbose XPath trick shown above. Just remember to use the . in the XPath expressions that will follow.

Beware of the difference between //node[1] and (//node)[1]

//node[1] selects all the nodes occurring first under their respective parents.

(//node)[1] selects all the nodes in the document, and then gets only the first of them.

Example:

>>> from scrapy import Selector >>> sel = Selector(text=""" ....: <ul class="list"> ....: <li>1</li> ....: <li>2</li> ....: <li>3</li> ....: </ul> ....: <ul class="list"> ....: <li>4</li> ....: <li>5</li> ....: <li>6</li> ....: </ul>""") >>> xp = lambda x: sel.xpath(x).getall()

This gets all first <li> elements under whatever it is its parent:

>>> xp("//li[1]") ['<li>1</li>', '<li>4</li>']

And this gets the first <li> element in the whole document:

>>> xp("(//li)[1]") ['<li>1</li>']

This gets all first <li> elements under an <ul> parent:

>>> xp("//ul/li[1]") ['<li>1</li>', '<li>4</li>']

And this gets the first <li> element under an <ul> parent in the whole document:

>>> xp("(//ul/li)[1]") ['<li>1</li>']

Using text nodes in a condition

When you need to use the text content as argument to an XPath string function [https://www.w3.org/TR/xpath/#section-String-Functions], avoid using .//text() and use just . instead.

This is because the expression .//text() yields a collection of text elements – a node-set. And when a node-set is converted to a string, which happens when it is passed as argument to a string function like contains() or starts-with(), it results in the text for the first element only.

Example:

>>> from scrapy import Selector >>> sel = Selector(text='<a href="#">Click here to go to the <strong>Next Page</strong></a>')

Converting a node-set to string:

>>> sel.xpath('//a//text()').getall() # take a peek at the node-set ['Click here to go to the ', 'Next Page'] >>> sel.xpath("string(//a[1]//text())").getall() # convert it to string ['Click here to go to the ']

A node converted to a string, however, puts together the text of itself plus of all its descendants:

>>> sel.xpath("//a[1]").getall() # select the first node ['<a href="#">Click here to go to the <strong>Next Page</strong></a>'] >>> sel.xpath("string(//a[1])").getall() # convert it to string ['Click here to go to the Next Page']

So, using the .//text() node-set won’t select anything in this case:

>>> sel.xpath("//a[contains(.//text(), 'Next Page')]").getall() []

But using the . to mean the node, works:

>>> sel.xpath("//a[contains(., 'Next Page')]").getall() ['<a href="#">Click here to go to the <strong>Next Page</strong></a>']

Variables in XPath expressions

XPath allows you to reference variables in your XPath expressions, using the $somevariable syntax. This is somewhat similar to parameterized queries or prepared statements in the SQL world where you replace some arguments in your queries with placeholders like ?, which are then substituted with values passed with the query.

Here’s an example to match an element based on its「id」attribute value, without hard-coding it (that was shown previously):

>>> # `$val` used in the expression, a `val` argument needs to be passed >>> response.xpath('//div[@id=$val]/a/text()', val='images').get() 'Name: My image 1 '

Here’s another example, to find the「id」attribute of a <div> tag containing five <a> children (here we pass the value 5 as an integer):

>>> response.xpath('//div[count(a)=$cnt]/@id', cnt=5).get() 'images'

All variable references must have a binding value when calling .xpath() (otherwise you’ll get a ValueError: XPath error: exception). This is done by passing as many named arguments as necessary.

parsel [https://parsel.readthedocs.io/], the library powering Scrapy selectors, has more details and examples on XPath variables [https://parsel.readthedocs.io/en/latest/usage.html#variables-in-xpath-expressions].

Removing namespaces

When dealing with scraping projects, it is often quite convenient to get rid of namespaces altogether and just work with element names, to write more simple/convenient XPaths. You can use the Selector.remove_namespaces() method for that.

Let’s show an example that illustrates this with the Python Insider blog atom feed.

First, we open the shell with the url we want to scrape:

$ scrapy shell https://feeds.feedburner.com/PythonInsider

This is how the file starts:

<?xml version="1.0" encoding="UTF-8"?> <?xml-stylesheet ... <feed xmlns="http://www.w3.org/2005/Atom" xmlns:openSearch="http://a9.com/-/spec/opensearchrss/1.0/" xmlns:blogger="http://schemas.google.com/blogger/2008" xmlns:georss="http://www.georss.org/georss" xmlns:gd="http://schemas.google.com/g/2005" xmlns:thr="http://purl.org/syndication/thread/1.0" xmlns:feedburner="http://rssnamespace.org/feedburner/ext/1.0"> ...

You can see several namespace declarations including a default「http://www.w3.org/2005/Atom」and another one using the「gd:」prefix for「http://schemas.google.com/g/2005」.

Once in the shell we can try selecting all <link> objects and see that it doesn’t work (because the Atom XML namespace is obfuscating those nodes):

>>> response.xpath("//link") []

But once we call the Selector.remove_namespaces() method, all nodes can be accessed directly by their names:

>>> response.selector.remove_namespaces() >>> response.xpath("//link") [<Selector xpath='//link' data='<link rel="alternate" type="text/html" h'>, <Selector xpath='//link' data='<link rel="next" type="application/atom+'>, ...

If you wonder why the namespace removal procedure isn’t always called by default instead of having to call it manually, this is because of two reasons, which, in order of relevance, are:

Removing namespaces requires to iterate and modify all nodes in the document, which is a reasonably expensive operation to perform by default for all documents crawled by Scrapy

There could be some cases where using namespaces is actually required, in case some element names clash between namespaces. These cases are very rare though.

Using EXSLT extensions

Being built atop lxml [http://lxml.de/], Scrapy selectors support some EXSLT [http://exslt.org/] extensions and come with these pre-registered namespaces to use in XPath expressions:

prefix

namespace

usage

re

http://exslt.org/regular-expressions

regular expressions

set

http://exslt.org/sets

set manipulation

Regular expressions

The test() function, for example, can prove quite useful when XPath’s starts-with() or contains() are not sufficient.

Example selecting links in list item with a「class」attribute ending with a digit:

>>> from scrapy import Selector >>> doc = u""" ... <div> ... <ul> ... <li class="item-0"><a href="link1.html">first item</a></li> ... <li class="item-1"><a href="link2.html">second item</a></li> ... <li class="item-inactive"><a href="link3.html">third item</a></li> ... <li class="item-1"><a href="link4.html">fourth item</a></li> ... <li class="item-0"><a href="link5.html">fifth item</a></li> ... </ul> ... </div> ... """ >>> sel = Selector(text=doc, type="html") >>> sel.xpath('//li//@href').getall() ['link1.html', 'link2.html', 'link3.html', 'link4.html', 'link5.html'] >>> sel.xpath('//li[re:test(@class, "item-\d$")]//@href').getall() ['link1.html', 'link2.html', 'link4.html', 'link5.html'] >>>

Warning

C library libxslt doesn’t natively support EXSLT regular expressions so lxml [http://lxml.de/]’s implementation uses hooks to Python’s re module. Thus, using regexp functions in your XPath expressions may add a small performance penalty.

Set operations

These can be handy for excluding parts of a document tree before extracting text elements for example.

Example extracting microdata (sample content taken from http://schema.org/Product) with groups of itemscopes and corresponding itemprops:

>>> doc = u""" ... <div itemscope itemtype="http://schema.org/Product"> ... <span itemprop="name">Kenmore White 17" Microwave</span> ... <img src="kenmore-microwave-17in.jpg" alt='Kenmore 17" Microwave' /> ... <div itemprop="aggregateRating" ... itemscope itemtype="http://schema.org/AggregateRating"> ... Rated <span itemprop="ratingValue">3.5</span>/5 ... based on <span itemprop="reviewCount">11</span> customer reviews ... </div> ... ... <div itemprop="offers" itemscope itemtype="http://schema.org/Offer"> ... <span itemprop="price">$55.00</span> ... <link itemprop="availability" href="http://schema.org/InStock" />In stock ... </div> ... ... Product description: ... <span itemprop="description">0.7 cubic feet countertop microwave. ... Has six preset cooking categories and convenience features like ... Add-A-Minute and Child Lock.</span> ... ... Customer reviews: ... ... <div itemprop="review" itemscope itemtype="http://schema.org/Review"> ... <span itemprop="name">Not a happy camper</span> - ... by <span itemprop="author">Ellie</span>, ... <meta itemprop="datePublished" content="2011-04-01">April 1, 2011 ... <div itemprop="reviewRating" itemscope itemtype="http://schema.org/Rating"> ... <meta itemprop="worstRating" content = "1"> ... <span itemprop="ratingValue">1</span>/ ... <span itemprop="bestRating">5</span>stars ... </div> ... <span itemprop="description">The lamp burned out and now I have to replace ... it. </span> ... </div> ... ... <div itemprop="review" itemscope itemtype="http://schema.org/Review"> ... <span itemprop="name">Value purchase</span> - ... by <span itemprop="author">Lucas</span>, ... <meta itemprop="datePublished" content="2011-03-25">March 25, 2011 ... <div itemprop="reviewRating" itemscope itemtype="http://schema.org/Rating"> ... <meta itemprop="worstRating" content = "1"/> ... <span itemprop="ratingValue">4</span>/ ... <span itemprop="bestRating">5</span>stars ... </div> ... <span itemprop="description">Great microwave for the price. It is small and ... fits in my apartment.</span> ... </div> ... ... ... </div> ... """ >>> sel = Selector(text=doc, type="html") >>> for scope in sel.xpath('//div[@itemscope]'): ... print("current scope:", scope.xpath('@itemtype').getall()) ... props = scope.xpath(''' ... set:difference(./descendant::*/@itemprop, ... .//*[@itemscope]/*/@itemprop)''') ... print(" properties: %s" % (props.getall())) ... print("") current scope: ['http://schema.org/Product'] properties: ['name', 'aggregateRating', 'offers', 'description', 'review', 'review'] current scope: ['http://schema.org/AggregateRating'] properties: ['ratingValue', 'reviewCount'] current scope: ['http://schema.org/Offer'] properties: ['price', 'availability'] current scope: ['http://schema.org/Review'] properties: ['name', 'author', 'datePublished', 'reviewRating', 'description'] current scope: ['http://schema.org/Rating'] properties: ['worstRating', 'ratingValue', 'bestRating'] current scope: ['http://schema.org/Review'] properties: ['name', 'author', 'datePublished', 'reviewRating', 'description'] current scope: ['http://schema.org/Rating'] properties: ['worstRating', 'ratingValue', 'bestRating'] >>>

Here we first iterate over itemscope elements, and for each one, we look for all itemprops elements and exclude those that are themselves inside another itemscope.

Other XPath extensions

Scrapy selectors also provide a sorely missed XPath extension function has-class that returns True for nodes that have all of the specified HTML classes.

For the following HTML:

<p class="foo bar-baz">First</p> <p class="foo">Second</p> <p class="bar">Third</p> <p>Fourth</p>

You can use it like this:

>>> response.xpath('//p[has-class("foo")]') [<Selector xpath='//p[has-class("foo")]' data='<p class="foo bar-baz">First</p>'>, <Selector xpath='//p[has-class("foo")]' data='<p class="foo">Second</p>'>] >>> response.xpath('//p[has-class("foo", "bar-baz")]') [<Selector xpath='//p[has-class("foo", "bar-baz")]' data='<p class="foo bar-baz">First</p>'>] >>> response.xpath('//p[has-class("foo", "bar")]') []

So XPath //p[has-class("foo", "bar-baz")] is roughly equivalent to CSS p.foo.bar-baz. Please note, that it is slower in most of the cases, because it’s a pure-Python function that’s invoked for every node in question whereas the CSS lookup is translated into XPath and thus runs more efficiently, so performance-wise its uses are limited to situations that are not easily described with CSS selectors.

Parsel also simplifies adding your own XPath extensions.

parsel.xpathfuncs.set_xpathfunc(fname, func)

Register a custom extension function to use in XPath expressions.

The function func registered under fname identifier will be called for every matching node, being passed a context parameter as well as any parameters passed from the corresponding XPath expression.

If func is None, the extension function will be removed.

See more in lxml documentation [http://lxml.de/extensions.html#xpath-extension-functions].

Built-in Selectors reference

Selector objects

class scrapy.selector.Selector(response=None, text=None, type=None, root=None, **kwargs)

An instance of Selector is a wrapper over response to select certain parts of its content.

response is an HtmlResponse or an XmlResponse object that will be used for selecting and extracting data.

text is a unicode string or utf-8 encoded text for cases when a response isn’t available. Using text and response together is undefined behavior.

type defines the selector type, it can be "html", "xml" or None (default).

If type is None, the selector automatically chooses the best type based on response type (see below), or defaults to "html" in case it is used together with text.

If type is None and a response is passed, the selector type is inferred from the response type as follows:

"html" for HtmlResponse type

"xml" for XmlResponse type

"html" for anything else

Otherwise, if type is set, the selector type will be forced and no detection will occur.

xpath(query, namespaces=None, **kwargs)

Find nodes matching the xpath query and return the result as a SelectorList instance with all elements flattened. List elements implement Selector interface too.

query is a string containing the XPATH query to apply.

namespaces is an optional prefix: namespace-uri mapping (dict) for additional prefixes to those registered with register_namespace(prefix, uri). Contrary to register_namespace(), these prefixes are not saved for future calls.

Any additional named arguments can be used to pass values for XPath variables in the XPath expression, e.g.:

selector.xpath('//a[href=$url]', url="http://www.example.com")

Note

For convenience, this method can be called as response.xpath()

css(query)

Apply the given CSS selector and return a SelectorList instance.

query is a string containing the CSS selector to apply.

In the background, CSS queries are translated into XPath queries using cssselect [https://pypi.python.org/pypi/cssselect/] library and run .xpath() method.

Note

For convenience, this method can be called as response.css()

get()

Serialize and return the matched nodes in a single unicode string. Percent encoded content is unquoted.

See also: extract() and extract_first()

attrib

Return the attributes dictionary for underlying element.

See also: Selecting element attributes.

re(regex, replace_entities=True)

Apply the given regex and return a list of unicode strings with the matches.

regex can be either a compiled regular expression or a string which will be compiled to a regular expression using re.compile(regex).

By default, character entity references are replaced by their corresponding character (except for &amp; and &lt;). Passing replace_entities as False switches off these replacements.

re_first(regex, default=None, replace_entities=True)

Apply the given regex and return the first unicode string which matches. If there is no match, return the default value (None if the argument is not provided).

By default, character entity references are replaced by their corresponding character (except for &amp; and &lt;). Passing replace_entities as False switches off these replacements.

register_namespace(prefix, uri)

Register the given namespace to be used in this Selector. Without registering namespaces you can’t select or extract data from non-standard namespaces. See Selector examples on XML response.

remove_namespaces()

Remove all namespaces, allowing to traverse the document using namespace-less xpaths. See Removing namespaces.

__bool__()

Return True if there is any real content selected or False otherwise. In other words, the boolean value of a Selector is given by the contents it selects.

getall()

Serialize and return the matched node in a 1-element list of unicode strings.

This method is added to Selector for consistency; it is more useful with SelectorList. See also: extract() and extract_first()

SelectorList objects

class scrapy.selector.SelectorList

The SelectorList class is a subclass of the builtin list class, which provides a few additional methods.

xpath(xpath, namespaces=None, **kwargs)

Call the .xpath() method for each element in this list and return their results flattened as another SelectorList.

query is the same argument as the one in Selector.xpath()

namespaces is an optional prefix: namespace-uri mapping (dict) for additional prefixes to those registered with register_namespace(prefix, uri). Contrary to register_namespace(), these prefixes are not saved for future calls.

Any additional named arguments can be used to pass values for XPath variables in the XPath expression, e.g.:

selector.xpath('//a[href=$url]', url="http://www.example.com")

css(query)

Call the .css() method for each element in this list and return their results flattened as another SelectorList.

query is the same argument as the one in Selector.css()

getall()

Call the .get() method for each element is this list and return their results flattened, as a list of unicode strings.

See also: extract() and extract_first()

get(default=None)

Return the result of .get() for the first element in this list. If the list is empty, return the default value.

See also: extract() and extract_first()

re(regex, replace_entities=True)

Call the .re() method for each element in this list and return their results flattened, as a list of unicode strings.

By default, character entity references are replaced by their corresponding character (except for &amp; and &lt;. Passing replace_entities as False switches off these replacements.

re_first(regex, default=None, replace_entities=True)

Call the .re() method for the first element in this list and return the result in an unicode string. If the list is empty or the regex doesn’t match anything, return the default value (None if the argument is not provided).

By default, character entity references are replaced by their corresponding character (except for &amp; and &lt;. Passing replace_entities as False switches off these replacements.

attrib

Return the attributes dictionary for the first element. If the list is empty, return an empty dict.

See also: Selecting element attributes.

Examples

Selector examples on HTML response

Here are some Selector examples to illustrate several concepts. In all cases, we assume there is already a Selector instantiated with a HtmlResponse object like this:

sel = Selector(html_response)

Select all <h1> elements from an HTML response body, returning a list of Selector objects (ie. a SelectorList object):

sel.xpath("//h1")

Extract the text of all <h1> elements from an HTML response body, returning a list of unicode strings:

sel.xpath("//h1").getall() # this includes the h1 tag sel.xpath("//h1/text()").getall() # this excludes the h1 tag

Iterate over all <p> tags and print their class attribute:

for node in sel.xpath("//p"): print(node.attrib['class'])

Selector examples on XML response

Here are some examples to illustrate concepts for Selector objects instantiated with an XmlResponse object:

sel = Selector(xml_response)

Select all <product> elements from an XML response body, returning a list of Selector objects (ie. a SelectorList object):

sel.xpath("//product")

Extract all prices from a Google Base XML feed [https://support.google.com/merchants/answer/160589?hl=en&ref_topic=2473799] which requires registering a namespace:

sel.register_namespace("g", "http://base.google.com/ns/1.0") sel.xpath("//g:price").getall()

Items

The main goal in scraping is to extract structured data from unstructured sources, typically, web pages. Scrapy spiders can return the extracted data as Python dicts. While convenient and familiar, Python dicts lack structure: it is easy to make a typo in a field name or return inconsistent data, especially in a larger project with many spiders.

To define common output data format Scrapy provides the Item class. Item objects are simple containers used to collect the scraped data. They provide a dictionary-like [https://docs.python.org/2/library/stdtypes.html#dict] API with a convenient syntax for declaring their available fields.

Various Scrapy components use extra information provided by Items: exporters look at declared fields to figure out columns to export, serialization can be customized using Item fields metadata, trackref tracks Item instances to help find memory leaks (see Debugging memory leaks with trackref), etc.

Declaring Items

Items are declared using a simple class definition syntax and Field objects. Here is an example:

import scrapy class Product(scrapy.Item): name = scrapy.Field() price = scrapy.Field() stock = scrapy.Field() tags = scrapy.Field() last_updated = scrapy.Field(serializer=str)

Note

Those familiar with Django [https://www.djangoproject.com/] will notice that Scrapy Items are declared similar to Django Models [https://docs.djangoproject.com/en/dev/topics/db/models/], except that Scrapy Items are much simpler as there is no concept of different field types.

Item Fields

Field objects are used to specify metadata for each field. For example, the serializer function for the last_updated field illustrated in the example above.

You can specify any kind of metadata for each field. There is no restriction on the values accepted by Field objects. For this same reason, there is no reference list of all available metadata keys. Each key defined in Field objects could be used by a different component, and only those components know about it. You can also define and use any other Field key in your project too, for your own needs. The main goal of Field objects is to provide a way to define all field metadata in one place. Typically, those components whose behaviour depends on each field use certain field keys to configure that behaviour. You must refer to their documentation to see which metadata keys are used by each component.

It’s important to note that the Field objects used to declare the item do not stay assigned as class attributes. Instead, they can be accessed through the Item.fields attribute.

Working with Items

Here are some examples of common tasks performed with items, using the Product item declared above. You will notice the API is very similar to the dict API [https://docs.python.org/2/library/stdtypes.html#dict].

Creating items

>>> product = Product(name='Desktop PC', price=1000) >>> print(product) Product(name='Desktop PC', price=1000)

Getting field values

>>> product['name'] Desktop PC >>> product.get('name') Desktop PC >>> product['price'] 1000 >>> product['last_updated'] Traceback (most recent call last): ... KeyError: 'last_updated' >>> product.get('last_updated', 'not set') not set >>> product['lala'] # getting unknown field Traceback (most recent call last): ... KeyError: 'lala' >>> product.get('lala', 'unknown field') 'unknown field' >>> 'name' in product # is name field populated? True >>> 'last_updated' in product # is last_updated populated? False >>> 'last_updated' in product.fields # is last_updated a declared field? True >>> 'lala' in product.fields # is lala a declared field? False

Setting field values

>>> product['last_updated'] = 'today' >>> product['last_updated'] today >>> product['lala'] = 'test' # setting unknown field Traceback (most recent call last): ... KeyError: 'Product does not support field: lala'

Accessing all populated values

To access all populated values, just use the typical dict API [https://docs.python.org/2/library/stdtypes.html#dict]:

>>> product.keys() ['price', 'name'] >>> product.items() [('price', 1000), ('name', 'Desktop PC')]

Copying items

To copy an item, you must first decide whether you want a shallow copy or a deep copy.

If your item contains mutable [https://docs.python.org/glossary.html#term-mutable] values like lists or dictionaries, a shallow copy will keep references to the same mutable values across all different copies.

For example, if you have an item with a list of tags, and you create a shallow copy of that item, both the original item and the copy have the same list of tags. Adding a tag to the list of one of the items will add the tag to the other item as well.

If that is not the desired behavior, use a deep copy instead.

See the documentation of the copy module [https://docs.python.org/library/copy.html] for more information.

To create a shallow copy of an item, you can either call copy() on an existing item (product2 = product.copy()) or instantiate your item class from an existing item (product2 = Product(product)).

To create a deep copy, call deepcopy() instead (product2 = product.deepcopy()).

Other common tasks

Creating dicts from items:

>>> dict(product) # create a dict from all populated values {'price': 1000, 'name': 'Desktop PC'}

Creating items from dicts:

>>> Product({'name': 'Laptop PC', 'price': 1500}) Product(price=1500, name='Laptop PC') >>> Product({'name': 'Laptop PC', 'lala': 1500}) # warning: unknown field in dict Traceback (most recent call last): ... KeyError: 'Product does not support field: lala'

Extending Items

You can extend Items (to add more fields or to change some metadata for some fields) by declaring a subclass of your original Item.

For example:

class DiscountedProduct(Product): discount_percent = scrapy.Field(serializer=str) discount_expiration_date = scrapy.Field()

You can also extend field metadata by using the previous field metadata and appending more values, or changing existing values, like this:

class SpecificProduct(Product): name = scrapy.Field(Product.fields['name'], serializer=my_serializer)

That adds (or replaces) the serializer metadata key for the name field, keeping all the previously existing metadata values.

Item objects

class scrapy.item.Item([arg])

Return a new Item optionally initialized from the given argument.

Items replicate the standard dict API [https://docs.python.org/2/library/stdtypes.html#dict], including its constructor, and also provide the following additional API members:

copy()

deepcopy()

Return a deep copy [https://docs.python.org/library/copy.html#copy.deepcopy] of this item.

fields

A dictionary containing all declared fields for this Item, not only those populated. The keys are the field names and the values are the Field objects used in the Item declaration.

Field objects

class scrapy.item.Field([arg])

The Field class is just an alias to the built-in dict [https://docs.python.org/2/library/stdtypes.html#dict] class and doesn’t provide any extra functionality or attributes. In other words, Field objects are plain-old Python dicts. A separate class is used to support the item declaration syntax based on class attributes.

Other classes related to Item

class scrapy.item.BaseItem

Base class for all scraped items.

In Scrapy, an object is considered an item if it is an instance of either BaseItem or dict [https://docs.python.org/3/library/stdtypes.html#dict]. For example, when the output of a spider callback is evaluated, only instances of BaseItem or dict [https://docs.python.org/3/library/stdtypes.html#dict] are passed to item pipelines.

If you need instances of a custom class to be considered items by Scrapy, you must inherit from either BaseItem or dict [https://docs.python.org/3/library/stdtypes.html#dict].

Unlike instances of dict [https://docs.python.org/3/library/stdtypes.html#dict], instances of BaseItem may be tracked to debug memory leaks.

class scrapy.item.ItemMeta

Metaclass [https://realpython.com/python-metaclasses] of Item that handles field definitions.

Item Loaders

Item Loaders provide a convenient mechanism for populating scraped Items. Even though Items can be populated using their own dictionary-like API, Item Loaders provide a much more convenient API for populating them from a scraping process, by automating some common tasks like parsing the raw extracted data before assigning it.

In other words, Items provide the container of scraped data, while Item Loaders provide the mechanism for populating that container.

Item Loaders are designed to provide a flexible, efficient and easy mechanism for extending and overriding different field parsing rules, either by spider, or by source format (HTML, XML, etc) without becoming a nightmare to maintain.

Using Item Loaders to populate items

To use an Item Loader, you must first instantiate it. You can either instantiate it with a dict-like object (e.g. Item or dict) or without one, in which case an Item is automatically instantiated in the Item Loader constructor using the Item class specified in the ItemLoader.default_item_class attribute.

Then, you start collecting values into the Item Loader, typically using Selectors. You can add more than one value to the same item field; the Item Loader will know how to「join」those values later using a proper processing function.

Note

Collected data is internally stored as lists, allowing to add several values to the same field. If an item argument is passed when creating a loader, each of the item’s values will be stored as-is if it’s already an iterable, or wrapped with a list if it’s a single value.

Here is a typical Item Loader usage in a Spider, using the Product item declared in the Items chapter:

from scrapy.loader import ItemLoader from myproject.items import Product def parse(self, response): l = ItemLoader(item=Product(), response=response) l.add_xpath('name', '//div[@class="product_name"]') l.add_xpath('name', '//div[@class="product_title"]') l.add_xpath('price', '//p[@id="price"]') l.add_css('stock', 'p#stock]') l.add_value('last_updated', 'today') # you can also use literal values return l.load_item()

By quickly looking at that code, we can see the name field is being extracted from two different XPath locations in the page:

//div[@class="product_name"]

//div[@class="product_title"]

In other words, data is being collected by extracting it from two XPath locations, using the add_xpath() method. This is the data that will be assigned to the name field later.

Afterwards, similar calls are used for price and stock fields (the latter using a CSS selector with the add_css() method), and finally the last_update field is populated directly with a literal value (today) using a different method: add_value().

Finally, when all data is collected, the ItemLoader.load_item() method is called which actually returns the item populated with the data previously extracted and collected with the add_xpath(), add_css(), and add_value() calls.

Input and Output processors

An Item Loader contains one input processor and one output processor for each (item) field. The input processor processes the extracted data as soon as it’s received (through the add_xpath(), add_css() or add_value() methods) and the result of the input processor is collected and kept inside the ItemLoader. After collecting all data, the ItemLoader.load_item() method is called to populate and get the populated Item object. That’s when the output processor is called with the data previously collected (and processed using the input processor). The result of the output processor is the final value that gets assigned to the item.

Let’s see an example to illustrate how the input and output processors are called for a particular field (the same applies for any other field):

l = ItemLoader(Product(), some_selector) l.add_xpath('name', xpath1) # (1) l.add_xpath('name', xpath2) # (2) l.add_css('name', css) # (3) l.add_value('name', 'test') # (4) return l.load_item() # (5)

So what happens is:

Data from xpath1 is extracted, and passed through the input processor of the name field. The result of the input processor is collected and kept in the Item Loader (but not yet assigned to the item).

Data from xpath2 is extracted, and passed through the same input processor used in (1). The result of the input processor is appended to the data collected in (1) (if any).

This case is similar to the previous ones, except that the data is extracted from the css CSS selector, and passed through the same input processor used in (1) and (2). The result of the input processor is appended to the data collected in (1) and (2) (if any).

This case is also similar to the previous ones, except that the value to be collected is assigned directly, instead of being extracted from a XPath expression or a CSS selector. However, the value is still passed through the input processors. In this case, since the value is not iterable it is converted to an iterable of a single element before passing it to the input processor, because input processor always receive iterables.

The data collected in steps (1), (2), (3) and (4) is passed through the output processor of the name field. The result of the output processor is the value assigned to the name field in the item.

It’s worth noticing that processors are just callable objects, which are called with the data to be parsed, and return a parsed value. So you can use any function as input or output processor. The only requirement is that they must accept one (and only one) positional argument, which will be an iterable.

Note

Both input and output processors must receive an iterable as their first argument. The output of those functions can be anything. The result of input processors will be appended to an internal list (in the Loader) containing the collected values (for that field). The result of the output processors is the value that will be finally assigned to the item.

If you want to use a plain function as a processor, make sure it receives self as the first argument:

def lowercase_processor(self, values): for v in values: yield v.lower() class MyItemLoader(ItemLoader): name_in = lowercase_processor

This is because whenever a function is assigned as a class variable, it becomes a method and would be passed the instance as the the first argument when being called. See this answer on stackoverflow [https://stackoverflow.com/a/35322635] for more details.

The other thing you need to keep in mind is that the values returned by input processors are collected internally (in lists) and then passed to output processors to populate the fields.

Last, but not least, Scrapy comes with some commonly used processors built-in for convenience.

Declaring Item Loaders

Item Loaders are declared like Items, by using a class definition syntax. Here is an example:

from scrapy.loader import ItemLoader from scrapy.loader.processors import TakeFirst, MapCompose, Join class ProductLoader(ItemLoader): default_output_processor = TakeFirst() name_in = MapCompose(unicode.title) name_out = Join() price_in = MapCompose(unicode.strip) # ...

As you can see, input processors are declared using the _in suffix while output processors are declared using the _out suffix. And you can also declare a default input/output processors using the ItemLoader.default_input_processor and ItemLoader.default_output_processor attributes.

Declaring Input and Output Processors

As seen in the previous section, input and output processors can be declared in the Item Loader definition, and it’s very common to declare input processors this way. However, there is one more place where you can specify the input and output processors to use: in the Item Field metadata. Here is an example:

import scrapy from scrapy.loader.processors import Join, MapCompose, TakeFirst from w3lib.html import remove_tags def filter_price(value): if value.isdigit(): return value class Product(scrapy.Item): name = scrapy.Field( input_processor=MapCompose(remove_tags), output_processor=Join(), ) price = scrapy.Field( input_processor=MapCompose(remove_tags, filter_price), output_processor=TakeFirst(), )

>>> from scrapy.loader import ItemLoader >>> il = ItemLoader(item=Product()) >>> il.add_value('name', [u'Welcome to my', u'<strong>website</strong>']) >>> il.add_value('price', [u'&euro;', u'<span>1000</span>']) >>> il.load_item() {'name': u'Welcome to my website', 'price': u'1000'}

The precedence order, for both input and output processors, is as follows:

Item Loader field-specific attributes: field_in and field_out (most precedence)

Field metadata (input_processor and output_processor key)

Item Loader defaults: ItemLoader.default_input_processor() and ItemLoader.default_output_processor() (least precedence)

See also: Reusing and extending Item Loaders.

Item Loader Context

The Item Loader Context is a dict of arbitrary key/values which is shared among all input and output processors in the Item Loader. It can be passed when declaring, instantiating or using Item Loader. They are used to modify the behaviour of the input/output processors.

For example, suppose you have a function parse_length which receives a text value and extracts a length from it:

def parse_length(text, loader_context): unit = loader_context.get('unit', 'm') # ... length parsing code goes here ... return parsed_length

By accepting a loader_context argument the function is explicitly telling the Item Loader that it’s able to receive an Item Loader context, so the Item Loader passes the currently active context when calling it, and the processor function (parse_length in this case) can thus use them.

There are several ways to modify Item Loader context values:

By modifying the currently active Item Loader context (context attribute):

loader = ItemLoader(product) loader.context['unit'] = 'cm'

On Item Loader instantiation (the keyword arguments of Item Loader constructor are stored in the Item Loader context):

loader = ItemLoader(product, unit='cm')

On Item Loader declaration, for those input/output processors that support instantiating them with an Item Loader context. MapCompose is one of them:

class ProductLoader(ItemLoader): length_out = MapCompose(parse_length, unit='cm')

ItemLoader objects

class scrapy.loader.ItemLoader([item, selector, response, ]**kwargs)

Return a new Item Loader for populating the given Item. If no item is given, one is instantiated automatically using the class in default_item_class.

When instantiated with a selector or a response parameters the ItemLoader class provides convenient mechanisms for extracting data from web pages using selectors.

Parameters

item (Item object) – The item instance to populate using subsequent calls to add_xpath(), add_css(), or add_value().

selector (Selector object) – The selector to extract data from, when using the add_xpath() (resp. add_css()) or replace_xpath() (resp. replace_css()) method.

response (Response object) – The response used to construct the selector using the default_selector_class, unless the selector argument is given, in which case this argument is ignored.

The item, selector, response and the remaining keyword arguments are assigned to the Loader context (accessible through the context attribute).

ItemLoader instances have the following methods:

get_value(value, *processors, **kwargs)

Process the given value by the given processors and keyword arguments.

Available keyword arguments:

Parameters

re (str [https://docs.python.org/3/library/stdtypes.html#str] or compiled regex) – a regular expression to use for extracting data from the given value using extract_regex() method, applied before processors

Examples:

>>> from scrapy.loader.processors import TakeFirst >>> loader.get_value(u'name: foo', TakeFirst(), unicode.upper, re='name: (.+)') 'FOO`

add_value(field_name, value, *processors, **kwargs)

Process and then add the given value for the given field.

The value is first passed through get_value() by giving the processors and kwargs, and then passed through the field input processor and its result appended to the data collected for that field. If the field already contains collected data, the new data is added.

The given field_name can be None, in which case values for multiple fields may be added. And the processed value should be a dict with field_name mapped to values.

Examples:

loader.add_value('name', u'Color TV') loader.add_value('colours', [u'white', u'blue']) loader.add_value('length', u'100') loader.add_value('name', u'name: foo', TakeFirst(), re='name: (.+)') loader.add_value(None, {'name': u'foo', 'sex': u'male'})

replace_value(field_name, value, *processors, **kwargs)

Similar to add_value() but replaces the collected data with the new value instead of adding it.

get_xpath(xpath, *processors, **kwargs)

Similar to ItemLoader.get_value() but receives an XPath instead of a value, which is used to extract a list of unicode strings from the selector associated with this ItemLoader.

Parameters

xpath (str [https://docs.python.org/3/library/stdtypes.html#str]) – the XPath to extract data from

re (str [https://docs.python.org/3/library/stdtypes.html#str] or compiled regex) – a regular expression to use for extracting data from the selected XPath region

Examples:

# HTML snippet: <p class="product-name">Color TV</p> loader.get_xpath('//p[@class="product-name"]') # HTML snippet: <p id="price">the price is $1200</p> loader.get_xpath('//p[@id="price"]', TakeFirst(), re='the price is (.*)')

add_xpath(field_name, xpath, *processors, **kwargs)

Similar to ItemLoader.add_value() but receives an XPath instead of a value, which is used to extract a list of unicode strings from the selector associated with this ItemLoader.

See get_xpath() for kwargs.

Parameters

xpath (str [https://docs.python.org/3/library/stdtypes.html#str]) – the XPath to extract data from

Examples:

# HTML snippet: <p class="product-name">Color TV</p> loader.add_xpath('name', '//p[@class="product-name"]') # HTML snippet: <p id="price">the price is $1200</p> loader.add_xpath('price', '//p[@id="price"]', re='the price is (.*)')

replace_xpath(field_name, xpath, *processors, **kwargs)

Similar to add_xpath() but replaces collected data instead of adding it.

get_css(css, *processors, **kwargs)

Similar to ItemLoader.get_value() but receives a CSS selector instead of a value, which is used to extract a list of unicode strings from the selector associated with this ItemLoader.

Parameters

css (str [https://docs.python.org/3/library/stdtypes.html#str]) – the CSS selector to extract data from

re (str [https://docs.python.org/3/library/stdtypes.html#str] or compiled regex) – a regular expression to use for extracting data from the selected CSS region

Examples:

# HTML snippet: <p class="product-name">Color TV</p> loader.get_css('p.product-name') # HTML snippet: <p id="price">the price is $1200</p> loader.get_css('p#price', TakeFirst(), re='the price is (.*)')

add_css(field_name, css, *processors, **kwargs)

Similar to ItemLoader.add_value() but receives a CSS selector instead of a value, which is used to extract a list of unicode strings from the selector associated with this ItemLoader.

See get_css() for kwargs.

Parameters

css (str [https://docs.python.org/3/library/stdtypes.html#str]) – the CSS selector to extract data from

Examples:

# HTML snippet: <p class="product-name">Color TV</p> loader.add_css('name', 'p.product-name') # HTML snippet: <p id="price">the price is $1200</p> loader.add_css('price', 'p#price', re='the price is (.*)')

replace_css(field_name, css, *processors, **kwargs)

Similar to add_css() but replaces collected data instead of adding it.

load_item()

Populate the item with the data collected so far, and return it. The data collected is first passed through the output processors to get the final value to assign to each item field.

nested_xpath(xpath)

Create a nested loader with an xpath selector. The supplied selector is applied relative to selector associated with this ItemLoader. The nested loader shares the Item with the parent ItemLoader so calls to add_xpath(), add_value(), replace_value(), etc. will behave as expected.

nested_css(css)

Create a nested loader with a css selector. The supplied selector is applied relative to selector associated with this ItemLoader. The nested loader shares the Item with the parent ItemLoader so calls to add_xpath(), add_value(), replace_value(), etc. will behave as expected.

get_collected_values(field_name)

Return the collected values for the given field.

get_output_value(field_name)

Return the collected values parsed using the output processor, for the given field. This method doesn’t populate or modify the item at all.

get_input_processor(field_name)

Return the input processor for the given field.

get_output_processor(field_name)

Return the output processor for the given field.

ItemLoader instances have the following attributes:

item

The Item object being parsed by this Item Loader.

context

The currently active Context of this Item Loader.

default_item_class

An Item class (or factory), used to instantiate items when not given in the constructor.

default_input_processor

The default input processor to use for those fields which don’t specify one.

default_output_processor

The default output processor to use for those fields which don’t specify one.

default_selector_class

The class used to construct the selector of this ItemLoader, if only a response is given in the constructor. If a selector is given in the constructor this attribute is ignored. This attribute is sometimes overridden in subclasses.

selector

The Selector object to extract data from. It’s either the selector given in the constructor or one created from the response given in the constructor using the default_selector_class. This attribute is meant to be read-only.

Nested Loaders

When parsing related values from a subsection of a document, it can be useful to create nested loaders. Imagine you’re extracting details from a footer of a page that looks something like:

Example:

<footer> <a class="social" href="https://facebook.com/whatever">Like Us</a> <a class="social" href="https://twitter.com/whatever">Follow Us</a> <a class="email" href="mailto:whatever@example.com">Email Us</a> </footer>

Without nested loaders, you need to specify the full xpath (or css) for each value that you wish to extract.

Example:

loader = ItemLoader(item=Item()) # load stuff not in the footer loader.add_xpath('social', '//footer/a[@class = "social"]/@href') loader.add_xpath('email', '//footer/a[@class = "email"]/@href') loader.load_item()

Instead, you can create a nested loader with the footer selector and add values relative to the footer. The functionality is the same but you avoid repeating the footer selector.

Example:

loader = ItemLoader(item=Item()) # load stuff not in the footer footer_loader = loader.nested_xpath('//footer') footer_loader.add_xpath('social', 'a[@class = "social"]/@href') footer_loader.add_xpath('email', 'a[@class = "email"]/@href') # no need to call footer_loader.load_item() loader.load_item()

You can nest loaders arbitrarily and they work with either xpath or css selectors. As a general guideline, use nested loaders when they make your code simpler but do not go overboard with nesting or your parser can become difficult to read.

Reusing and extending Item Loaders

As your project grows bigger and acquires more and more spiders, maintenance becomes a fundamental problem, especially when you have to deal with many different parsing rules for each spider, having a lot of exceptions, but also wanting to reuse the common processors.

Item Loaders are designed to ease the maintenance burden of parsing rules, without losing flexibility and, at the same time, providing a convenient mechanism for extending and overriding them. For this reason Item Loaders support traditional Python class inheritance for dealing with differences of specific spiders (or groups of spiders).

Suppose, for example, that some particular site encloses their product names in three dashes (e.g. ---Plasma TV---) and you don’t want to end up scraping those dashes in the final product names.

Here’s how you can remove those dashes by reusing and extending the default Product Item Loader (ProductLoader):

from scrapy.loader.processors import MapCompose from myproject.ItemLoaders import ProductLoader def strip_dashes(x): return x.strip('-') class SiteSpecificLoader(ProductLoader): name_in = MapCompose(strip_dashes, ProductLoader.name_in)

Another case where extending Item Loaders can be very helpful is when you have multiple source formats, for example XML and HTML. In the XML version you may want to remove CDATA occurrences. Here’s an example of how to do it:

from scrapy.loader.processors import MapCompose from myproject.ItemLoaders import ProductLoader from myproject.utils.xml import remove_cdata class XmlProductLoader(ProductLoader): name_in = MapCompose(remove_cdata, ProductLoader.name_in)

And that’s how you typically extend input processors.

As for output processors, it is more common to declare them in the field metadata, as they usually depend only on the field and not on each specific site parsing rule (as input processors do). See also: Declaring Input and Output Processors.

There are many other possible ways to extend, inherit and override your Item Loaders, and different Item Loaders hierarchies may fit better for different projects. Scrapy only provides the mechanism; it doesn’t impose any specific organization of your Loaders collection - that’s up to you and your project’s needs.

Available built-in processors

Even though you can use any callable function as input and output processors, Scrapy provides some commonly used processors, which are described below. Some of them, like the MapCompose (which is typically used as input processor) compose the output of several functions executed in order, to produce the final parsed value.

Here is a list of all built-in processors:

class scrapy.loader.processors.Identity

The simplest processor, which doesn’t do anything. It returns the original values unchanged. It doesn’t receive any constructor arguments, nor does it accept Loader contexts.

Example:

>>> from scrapy.loader.processors import Identity >>> proc = Identity() >>> proc(['one', 'two', 'three']) ['one', 'two', 'three']

class scrapy.loader.processors.TakeFirst

Returns the first non-null/non-empty value from the values received, so it’s typically used as an output processor to single-valued fields. It doesn’t receive any constructor arguments, nor does it accept Loader contexts.

Example:

>>> from scrapy.loader.processors import TakeFirst >>> proc = TakeFirst() >>> proc(['', 'one', 'two', 'three']) 'one'

class scrapy.loader.processors.Join(separator=u' ')

Returns the values joined with the separator given in the constructor, which defaults to u' '. It doesn’t accept Loader contexts.

When using the default separator, this processor is equivalent to the function: u' '.join

Examples:

>>> from scrapy.loader.processors import Join >>> proc = Join() >>> proc(['one', 'two', 'three']) 'one two three' >>> proc = Join('<br>') >>> proc(['one', 'two', 'three']) 'one<br>two<br>three'

class scrapy.loader.processors.Compose(*functions, **default_loader_context)

A processor which is constructed from the composition of the given functions. This means that each input value of this processor is passed to the first function, and the result of that function is passed to the second function, and so on, until the last function returns the output value of this processor.

By default, stop process on None value. This behaviour can be changed by passing keyword argument stop_on_none=False.

Example:

>>> from scrapy.loader.processors import Compose >>> proc = Compose(lambda v: v[0], str.upper) >>> proc(['hello', 'world']) 'HELLO'

Each function can optionally receive a loader_context parameter. For those which do, this processor will pass the currently active Loader context through that parameter.

The keyword arguments passed in the constructor are used as the default Loader context values passed to each function call. However, the final Loader context values passed to functions are overridden with the currently active Loader context accessible through the ItemLoader.context() attribute.

class scrapy.loader.processors.MapCompose(*functions, **default_loader_context)

A processor which is constructed from the composition of the given functions, similar to the Compose processor. The difference with this processor is the way internal results are passed among functions, which is as follows:

The input value of this processor is iterated and the first function is applied to each element. The results of these function calls (one for each element) are concatenated to construct a new iterable, which is then used to apply the second function, and so on, until the last function is applied to each value of the list of values collected so far. The output values of the last function are concatenated together to produce the output of this processor.

Each particular function can return a value or a list of values, which is flattened with the list of values returned by the same function applied to the other input values. The functions can also return None in which case the output of that function is ignored for further processing over the chain.

This processor provides a convenient way to compose functions that only work with single values (instead of iterables). For this reason the MapCompose processor is typically used as input processor, since data is often extracted using the extract() method of selectors, which returns a list of unicode strings.

The example below should clarify how it works:

>>> def filter_world(x): ... return None if x == 'world' else x ... >>> from scrapy.loader.processors import MapCompose >>> proc = MapCompose(filter_world, str.upper) >>> proc(['hello', 'world', 'this', 'is', 'scrapy']) ['HELLO, 'THIS', 'IS', 'SCRAPY']

As with the Compose processor, functions can receive Loader contexts, and constructor keyword arguments are used as default context values. See Compose processor for more info.

class scrapy.loader.processors.SelectJmes(json_path)

Queries the value using the json path provided to the constructor and returns the output. Requires jmespath (https://github.com/jmespath/jmespath.py) to run. This processor takes only one input at a time.

Example:

>>> from scrapy.loader.processors import SelectJmes, Compose, MapCompose >>> proc = SelectJmes("foo") #for direct use on lists and dictionaries >>> proc({'foo': 'bar'}) 'bar' >>> proc({'foo': {'bar': 'baz'}}) {'bar': 'baz'}

Working with Json:

>>> import json >>> proc_single_json_str = Compose(json.loads, SelectJmes("foo")) >>> proc_single_json_str('{"foo": "bar"}') 'bar' >>> proc_json_list = Compose(json.loads, MapCompose(SelectJmes('foo'))) >>> proc_json_list('[{"foo":"bar"}, {"baz":"tar"}]') ['bar']

Scrapy shell

The Scrapy shell is an interactive shell where you can try and debug your scraping code very quickly, without having to run the spider. It’s meant to be used for testing data extraction code, but you can actually use it for testing any kind of code as it is also a regular Python shell.

The shell is used for testing XPath or CSS expressions and see how they work and what data they extract from the web pages you’re trying to scrape. It allows you to interactively test your expressions while you’re writing your spider, without having to run the spider to test every change.

Once you get familiarized with the Scrapy shell, you’ll see that it’s an invaluable tool for developing and debugging your spiders.

Configuring the shell

If you have IPython [https://ipython.org/] installed, the Scrapy shell will use it (instead of the standard Python console). The IPython [https://ipython.org/] console is much more powerful and provides smart auto-completion and colorized output, among other things.

We highly recommend you install IPython [https://ipython.org/], specially if you’re working on Unix systems (where IPython [https://ipython.org/] excels). See the IPython installation guide [https://ipython.org/install.html] for more info.

Scrapy also has support for bpython [https://www.bpython-interpreter.org/], and will try to use it where IPython [https://ipython.org/] is unavailable.

Through scrapy’s settings you can configure it to use any one of ipython, bpython or the standard python shell, regardless of which are installed. This is done by setting the SCRAPY_PYTHON_SHELL environment variable; or by defining it in your scrapy.cfg:

[settings] shell = bpython

Launch the shell

To launch the Scrapy shell you can use the shell command like this:

scrapy shell <url>

Where the <url> is the URL you want to scrape.

shell also works for local files. This can be handy if you want to play around with a local copy of a web page. shell understands the following syntaxes for local files:

# UNIX-style scrapy shell ./path/to/file.html scrapy shell ../other/path/to/file.html scrapy shell /absolute/path/to/file.html # File URI scrapy shell file:///absolute/path/to/file.html

Note

When using relative file paths, be explicit and prepend them with ./ (or ../ when relevant). scrapy shell index.html will not work as one might expect (and this is by design, not a bug).

Because shell favors HTTP URLs over File URIs, and index.html being syntactically similar to example.com, shell will treat index.html as a domain name and trigger a DNS lookup error:

$ scrapy shell index.html [ ... scrapy shell starts ... ] [ ... traceback ... ] twisted.internet.error.DNSLookupError: DNS lookup failed: address 'index.html' not found: [Errno -5] No address associated with hostname.

shell will not test beforehand if a file called index.html exists in the current directory. Again, be explicit.

Using the shell

The Scrapy shell is just a regular Python console (or IPython [https://ipython.org/] console if you have it available) which provides some additional shortcut functions for convenience.

Available Shortcuts

shelp() - print a help with the list of available objects and shortcuts

fetch(url[, redirect=True]) - fetch a new response from the given URL and update all related objects accordingly. You can optionaly ask for HTTP 3xx redirections to not be followed by passing redirect=False

fetch(request) - fetch a new response from the given request and update all related objects accordingly.

view(response) - open the given response in your local web browser, for inspection. This will add a <base> tag [https://developer.mozilla.org/en-US/docs/Web/HTML/Element/base] to the response body in order for external links (such as images and style sheets) to display properly. Note, however, that this will create a temporary file in your computer, which won’t be removed automatically.

Available Scrapy objects

The Scrapy shell automatically creates some convenient objects from the downloaded page, like the Response object and the Selector objects (for both HTML and XML content).

Those objects are:

crawler - the current Crawler object.

spider - the Spider which is known to handle the URL, or a Spider object if there is no spider found for the current URL

request - a Request object of the last fetched page. You can modify this request using replace() or fetch a new request (without leaving the shell) using the fetch shortcut.

response - a Response object containing the last fetched page

settings - the current Scrapy settings

Example of shell session

Here’s an example of a typical shell session where we start by scraping the https://scrapy.org page, and then proceed to scrape the https://reddit.com page. Finally, we modify the (Reddit) request method to POST and re-fetch it getting an error. We end the session by typing Ctrl-D (in Unix systems) or Ctrl-Z in Windows.

Keep in mind that the data extracted here may not be the same when you try it, as those pages are not static and could have changed by the time you test this. The only purpose of this example is to get you familiarized with how the Scrapy shell works.

First, we launch the shell:

scrapy shell 'https://scrapy.org' --nolog

Then, the shell fetches the URL (using the Scrapy downloader) and prints the list of available objects and useful shortcuts (you’ll notice that these lines all start with the [s] prefix):

[s] Available Scrapy objects: [s] scrapy scrapy module (contains scrapy.Request, scrapy.Selector, etc) [s] crawler <scrapy.crawler.Crawler object at 0x7f07395dd690> [s] item {} [s] request <GET https://scrapy.org> [s] response <200 https://scrapy.org/> [s] settings <scrapy.settings.Settings object at 0x7f07395dd710> [s] spider <DefaultSpider 'default' at 0x7f0735891690> [s] Useful shortcuts: [s] fetch(url[, redirect=True]) Fetch URL and update local objects (by default, redirects are followed) [s] fetch(req) Fetch a scrapy.Request and update local objects [s] shelp() Shell help (print this help) [s] view(response) View response in a browser >>>

After that, we can start playing with the objects:

>>> response.xpath('//title/text()').get() 'Scrapy | A Fast and Powerful Scraping and Web Crawling Framework' >>> fetch("https://reddit.com") >>> response.xpath('//title/text()').get() 'reddit: the front page of the internet' >>> request = request.replace(method="POST") >>> fetch(request) >>> response.status 404 >>> from pprint import pprint >>> pprint(response.headers) {'Accept-Ranges': ['bytes'], 'Cache-Control': ['max-age=0, must-revalidate'], 'Content-Type': ['text/html; charset=UTF-8'], 'Date': ['Thu, 08 Dec 2016 16:21:19 GMT'], 'Server': ['snooserv'], 'Set-Cookie': ['loid=KqNLou0V9SKMX4qb4n; Domain=reddit.com; Max-Age=63071999; Path=/; expires=Sat, 08-Dec-2018 16:21:19 GMT; secure', 'loidcreated=2016-12-08T16%3A21%3A19.445Z; Domain=reddit.com; Max-Age=63071999; Path=/; expires=Sat, 08-Dec-2018 16:21:19 GMT; secure', 'loid=vi0ZVe4NkxNWdlH7r7; Domain=reddit.com; Max-Age=63071999; Path=/; expires=Sat, 08-Dec-2018 16:21:19 GMT; secure', 'loidcreated=2016-12-08T16%3A21%3A19.459Z; Domain=reddit.com; Max-Age=63071999; Path=/; expires=Sat, 08-Dec-2018 16:21:19 GMT; secure'], 'Vary': ['accept-encoding'], 'Via': ['1.1 varnish'], 'X-Cache': ['MISS'], 'X-Cache-Hits': ['0'], 'X-Content-Type-Options': ['nosniff'], 'X-Frame-Options': ['SAMEORIGIN'], 'X-Moose': ['majestic'], 'X-Served-By': ['cache-cdg8730-CDG'], 'X-Timer': ['S1481214079.394283,VS0,VE159'], 'X-Ua-Compatible': ['IE=edge'], 'X-Xss-Protection': ['1; mode=block']} >>>

Invoking the shell from spiders to inspect responses

Sometimes you want to inspect the responses that are being processed in a certain point of your spider, if only to check that response you expect is getting there.

This can be achieved by using the scrapy.shell.inspect_response function.

Here’s an example of how you would call it from your spider:

import scrapy class MySpider(scrapy.Spider): name = "myspider" start_urls = [ "http://example.com", "http://example.org", "http://example.net", ] def parse(self, response): # We want to inspect one specific response. if ".org" in response.url: from scrapy.shell import inspect_response inspect_response(response, self) # Rest of parsing code.

When you run the spider, you will get something similar to this:

2014-01-23 17:48:31-0400 [scrapy.core.engine] DEBUG: Crawled (200) <GET http://example.com> (referer: None) 2014-01-23 17:48:31-0400 [scrapy.core.engine] DEBUG: Crawled (200) <GET http://example.org> (referer: None) [s] Available Scrapy objects: [s] crawler <scrapy.crawler.Crawler object at 0x1e16b50> ... >>> response.url 'http://example.org'

Then, you can check if the extraction code is working:

>>> response.xpath('//h1[@class="fn"]') []

Nope, it doesn’t. So you can open the response in your web browser and see if it’s the response you were expecting:

>>> view(response) True

Finally you hit Ctrl-D (or Ctrl-Z in Windows) to exit the shell and resume the crawling:

>>> ^D 2014-01-23 17:50:03-0400 [scrapy.core.engine] DEBUG: Crawled (200) <GET http://example.net> (referer: None) ...

Note that you can’t use the fetch shortcut here since the Scrapy engine is blocked by the shell. However, after you leave the shell, the spider will continue crawling where it stopped, as shown above.

Item Pipeline

After an item has been scraped by a spider, it is sent to the Item Pipeline which processes it through several components that are executed sequentially.

Each item pipeline component (sometimes referred as just「Item Pipeline」) is a Python class that implements a simple method. They receive an item and perform an action over it, also deciding if the item should continue through the pipeline or be dropped and no longer processed.

Typical uses of item pipelines are:

cleansing HTML data

validating scraped data (checking that the items contain certain fields)

checking for duplicates (and dropping them)

storing the scraped item in a database

Writing your own item pipeline

Each item pipeline component is a Python class that must implement the following method:

process_item(self, item, spider)

This method is called for every item pipeline component. process_item() must either: return a dict with data, return an Item (or any descendant class) object, return a Twisted Deferred [https://twistedmatrix.com/documents/current/core/howto/defer.html] or raise DropItem exception. Dropped items are no longer processed by further pipeline components.

Parameters

item (Item object or a dict) – the item scraped

spider (Spider object) – the spider which scraped the item

Additionally, they may also implement the following methods:

open_spider(self, spider)

This method is called when the spider is opened.

Parameters

spider (Spider object) – the spider which was opened

close_spider(self, spider)

This method is called when the spider is closed.

Parameters

spider (Spider object) – the spider which was closed

from_crawler(cls, crawler)

If present, this classmethod is called to create a pipeline instance from a Crawler. It must return a new instance of the pipeline. Crawler object provides access to all Scrapy core components like settings and signals; it is a way for pipeline to access them and hook its functionality into Scrapy.

Parameters

crawler (Crawler object) – crawler that uses this pipeline

Item pipeline example

Price validation and dropping items with no prices

Let’s take a look at the following hypothetical pipeline that adjusts the price attribute for those items that do not include VAT (price_excludes_vat attribute), and drops those items which don’t contain a price:

from scrapy.exceptions import DropItem class PricePipeline(object): vat_factor = 1.15 def process_item(self, item, spider): if item.get('price'): if item.get('price_excludes_vat'): item['price'] = item['price'] * self.vat_factor return item else: raise DropItem("Missing price in %s" % item)

Write items to a JSON file

The following pipeline stores all scraped items (from all spiders) into a single items.jl file, containing one item per line serialized in JSON format:

import json class JsonWriterPipeline(object): def open_spider(self, spider): self.file = open('items.jl', 'w') def close_spider(self, spider): self.file.close() def process_item(self, item, spider): line = json.dumps(dict(item)) + "\n" self.file.write(line) return item

Note

The purpose of JsonWriterPipeline is just to introduce how to write item pipelines. If you really want to store all scraped items into a JSON file you should use the Feed exports.

Write items to MongoDB

In this example we’ll write items to MongoDB [https://www.mongodb.org/] using pymongo [https://api.mongodb.org/python/current/]. MongoDB address and database name are specified in Scrapy settings; MongoDB collection is named after item class.

The main point of this example is to show how to use from_crawler() method and how to clean up the resources properly.:

import pymongo class MongoPipeline(object): collection_name = 'scrapy_items' def __init__(self, mongo_uri, mongo_db): self.mongo_uri = mongo_uri self.mongo_db = mongo_db @classmethod def from_crawler(cls, crawler): return cls( mongo_uri=crawler.settings.get('MONGO_URI'), mongo_db=crawler.settings.get('MONGO_DATABASE', 'items') ) def open_spider(self, spider): self.client = pymongo.MongoClient(self.mongo_uri) self.db = self.client[self.mongo_db] def close_spider(self, spider): self.client.close() def process_item(self, item, spider): self.db[self.collection_name].insert_one(dict(item)) return item

Take screenshot of item

This example demonstrates how to return Deferred [https://twistedmatrix.com/documents/current/core/howto/defer.html] from process_item() method. It uses Splash [https://splash.readthedocs.io/en/stable/] to render screenshot of item url. Pipeline makes request to locally running instance of Splash [https://splash.readthedocs.io/en/stable/]. After request is downloaded and Deferred callback fires, it saves item to a file and adds filename to an item.

import scrapy import hashlib from urllib.parse import quote class ScreenshotPipeline(object): """Pipeline that uses Splash to render screenshot of every Scrapy item.""" SPLASH_URL = "http://localhost:8050/render.png?url={}" def process_item(self, item, spider): encoded_item_url = quote(item["url"]) screenshot_url = self.SPLASH_URL.format(encoded_item_url) request = scrapy.Request(screenshot_url) dfd = spider.crawler.engine.download(request, spider) dfd.addBoth(self.return_item, item) return dfd def return_item(self, response, item): if response.status != 200: # Error happened, return item. return item # Save screenshot to file, filename will be hash of url. url = item["url"] url_hash = hashlib.md5(url.encode("utf8")).hexdigest() filename = "{}.png".format(url_hash) with open(filename, "wb") as f: f.write(response.body) # Store filename in item. item["screenshot_filename"] = filename return item

Duplicates filter

A filter that looks for duplicate items, and drops those items that were already processed. Let’s say that our items have a unique id, but our spider returns multiples items with the same id:

from scrapy.exceptions import DropItem class DuplicatesPipeline(object): def __init__(self): self.ids_seen = set() def process_item(self, item, spider): if item['id'] in self.ids_seen: raise DropItem("Duplicate item found: %s" % item) else: self.ids_seen.add(item['id']) return item

Activating an Item Pipeline component

To activate an Item Pipeline component you must add its class to the ITEM_PIPELINES setting, like in the following example:

ITEM_PIPELINES = { 'myproject.pipelines.PricePipeline': 300, 'myproject.pipelines.JsonWriterPipeline': 800, }

The integer values you assign to classes in this setting determine the order in which they run: items go through from lower valued to higher valued classes. It’s customary to define these numbers in the 0-1000 range.

Feed exports

New in version 0.10.

One of the most frequently required features when implementing scrapers is being able to store the scraped data properly and, quite often, that means generating an「export file」with the scraped data (commonly called「export feed」) to be consumed by other systems.

Scrapy provides this functionality out of the box with the Feed Exports, which allows you to generate a feed with the scraped items, using multiple serialization formats and storage backends.

Serialization formats

For serializing the scraped data, the feed exports use the Item exporters. These formats are supported out of the box:

JSON

JSON lines

CSV

XML

But you can also extend the supported format through the FEED_EXPORTERS setting.

JSON

FEED_FORMAT: json

Exporter used: JsonItemExporter

See this warning if you’re using JSON with large feeds.

JSON lines

FEED_FORMAT: jsonlines

Exporter used: JsonLinesItemExporter

CSV

FEED_FORMAT: csv

Exporter used: CsvItemExporter

To specify columns to export and their order use FEED_EXPORT_FIELDS. Other feed exporters can also use this option, but it is important for CSV because unlike many other export formats CSV uses a fixed header.

XML

FEED_FORMAT: xml

Exporter used: XmlItemExporter

Pickle

FEED_FORMAT: pickle

Exporter used: PickleItemExporter

Marshal

FEED_FORMAT: marshal

Exporter used: MarshalItemExporter

Storages

When using the feed exports you define where to store the feed using a URI [https://en.wikipedia.org/wiki/Uniform_Resource_Identifier] (through the FEED_URI setting). The feed exports supports multiple storage backend types which are defined by the URI scheme.

The storages backends supported out of the box are:

Local filesystem

FTP

S3 (requires botocore [https://github.com/boto/botocore] or boto [https://github.com/boto/boto])

Standard output

Some storage backends may be unavailable if the required external libraries are not available. For example, the S3 backend is only available if the botocore [https://github.com/boto/botocore] or boto [https://github.com/boto/boto] library is installed (Scrapy supports boto [https://github.com/boto/boto] only on Python 2).

Storage URI parameters

The storage URI can also contain parameters that get replaced when the feed is being created. These parameters are:

%(time)s - gets replaced by a timestamp when the feed is being created

%(name)s - gets replaced by the spider name

Any other named parameter gets replaced by the spider attribute of the same name. For example, %(site_id)s would get replaced by the spider.site_id attribute the moment the feed is being created.

Here are some examples to illustrate:

Store in FTP using one directory per spider:

ftp://user:password@ftp.example.com/scraping/feeds/%(name)s/%(time)s.json

Store in S3 using one directory per spider:

s3://mybucket/scraping/feeds/%(name)s/%(time)s.json

Storage backends

Local filesystem

The feeds are stored in the local filesystem.

URI scheme: file

Example URI: file:///tmp/export.csv

Required external libraries: none

Note that for the local filesystem storage (only) you can omit the scheme if you specify an absolute path like /tmp/export.csv. This only works on Unix systems though.

FTP

The feeds are stored in a FTP server.

URI scheme: ftp

Example URI: ftp://user:pass@ftp.example.com/path/to/export.csv

Required external libraries: none

FTP supports two different connection modes: active or passive [https://stackoverflow.com/a/1699163]. Scrapy uses the passive connection mode by default. To use the active connection mode instead, set the FEED_STORAGE_FTP_ACTIVE setting to True.

S3

The feeds are stored on Amazon S3 [https://aws.amazon.com/s3/].

URI scheme: s3

Example URIs:

s3://mybucket/path/to/export.csv

s3://aws_key:aws_secret@mybucket/path/to/export.csv

Required external libraries: botocore [https://github.com/boto/botocore] (Python 2 and Python 3) or boto [https://github.com/boto/boto] (Python 2 only)

The AWS credentials can be passed as user/password in the URI, or they can be passed through the following settings:

AWS_ACCESS_KEY_ID

AWS_SECRET_ACCESS_KEY

You can also define a custom ACL for exported feeds using this setting:

FEED_STORAGE_S3_ACL

Standard output

The feeds are written to the standard output of the Scrapy process.

URI scheme: stdout

Example URI: stdout:

Required external libraries: none

Settings

These are the settings used for configuring the feed exports:

FEED_URI (mandatory)

FEED_FORMAT

FEED_STORAGES

FEED_STORAGE_FTP_ACTIVE

FEED_STORAGE_S3_ACL

FEED_EXPORTERS

FEED_STORE_EMPTY

FEED_EXPORT_ENCODING

FEED_EXPORT_FIELDS

FEED_EXPORT_INDENT

FEED_URI

Default: None

The URI of the export feed. See Storage backends for supported URI schemes.

This setting is required for enabling the feed exports.

FEED_FORMAT

The serialization format to be used for the feed. See Serialization formats for possible values.

FEED_EXPORT_ENCODING

Default: None

The encoding to be used for the feed.

If unset or set to None (default) it uses UTF-8 for everything except JSON output, which uses safe numeric encoding (\uXXXX sequences) for historic reasons.

Use utf-8 if you want UTF-8 for JSON too.

FEED_EXPORT_FIELDS

Default: None

A list of fields to export, optional. Example: FEED_EXPORT_FIELDS = ["foo", "bar", "baz"].

Use FEED_EXPORT_FIELDS option to define fields to export and their order.

When FEED_EXPORT_FIELDS is empty or None (default), Scrapy uses fields defined in dicts or Item subclasses a spider is yielding.

If an exporter requires a fixed set of fields (this is the case for CSV export format) and FEED_EXPORT_FIELDS is empty or None, then Scrapy tries to infer field names from the exported data - currently it uses field names from the first item.

FEED_EXPORT_INDENT

Default: 0

Amount of spaces used to indent the output on each level. If FEED_EXPORT_INDENT is a non-negative integer, then array elements and object members will be pretty-printed with that indent level. An indent level of 0 (the default), or negative, will put each item on a new line. None selects the most compact representation.

Currently implemented only by JsonItemExporter and XmlItemExporter, i.e. when you are exporting to .json or .xml.

FEED_STORE_EMPTY

Default: False

Whether to export empty feeds (ie. feeds with no items).

FEED_STORAGES

Default: {}

A dict containing additional feed storage backends supported by your project. The keys are URI schemes and the values are paths to storage classes.

FEED_STORAGE_FTP_ACTIVE

Default: False

Whether to use the active connection mode when exporting feeds to an FTP server (True) or use the passive connection mode instead (False, default).

For information about FTP connection modes, see What is the difference between active and passive FTP? [https://stackoverflow.com/a/1699163].

FEED_STORAGE_S3_ACL

Default: '' (empty string)

A string containing a custom ACL for feeds exported to Amazon S3 by your project.

For a complete list of available values, access the Canned ACL [https://docs.aws.amazon.com/AmazonS3/latest/dev/acl-overview.html#canned-acl] section on Amazon S3 docs.

FEED_STORAGES_BASE

Default:

{ '': 'scrapy.extensions.feedexport.FileFeedStorage', 'file': 'scrapy.extensions.feedexport.FileFeedStorage', 'stdout': 'scrapy.extensions.feedexport.StdoutFeedStorage', 's3': 'scrapy.extensions.feedexport.S3FeedStorage', 'ftp': 'scrapy.extensions.feedexport.FTPFeedStorage', }

A dict containing the built-in feed storage backends supported by Scrapy. You can disable any of these backends by assigning None to their URI scheme in FEED_STORAGES. E.g., to disable the built-in FTP storage backend (without replacement), place this in your settings.py:

FEED_STORAGES = { 'ftp': None, }

FEED_EXPORTERS

Default: {}

A dict containing additional exporters supported by your project. The keys are serialization formats and the values are paths to Item exporter classes.

FEED_EXPORTERS_BASE

Default:

{ 'json': 'scrapy.exporters.JsonItemExporter', 'jsonlines': 'scrapy.exporters.JsonLinesItemExporter', 'jl': 'scrapy.exporters.JsonLinesItemExporter', 'csv': 'scrapy.exporters.CsvItemExporter', 'xml': 'scrapy.exporters.XmlItemExporter', 'marshal': 'scrapy.exporters.MarshalItemExporter', 'pickle': 'scrapy.exporters.PickleItemExporter', }

A dict containing the built-in feed exporters supported by Scrapy. You can disable any of these exporters by assigning None to their serialization format in FEED_EXPORTERS. E.g., to disable the built-in CSV exporter (without replacement), place this in your settings.py:

FEED_EXPORTERS = { 'csv': None, }

Requests and Responses

Scrapy uses Request and Response objects for crawling web sites.

Typically, Request objects are generated in the spiders and pass across the system until they reach the Downloader, which executes the request and returns a Response object which travels back to the spider that issued the request.

Both Request and Response classes have subclasses which add functionality not required in the base classes. These are described below in Request subclasses and Response subclasses.

Request objects

class scrapy.http.Request(url, callback=None, method='GET', headers=None, body=None, cookies=None, meta=None, encoding='utf-8', priority=0, dont_filter=False, errback=None, flags=None, cb_kwargs=None)

A Request object represents an HTTP request, which is usually generated in the Spider and executed by the Downloader, and thus generating a Response.

Parameters

url (string) – the URL of this request

callback (callable) – the function that will be called with the response of this request (once its downloaded) as its first parameter. For more information see Passing additional data to callback functions below. If a Request doesn’t specify a callback, the spider’s parse() method will be used. Note that if exceptions are raised during processing, errback is called instead.

method (string) – the HTTP method of this request. Defaults to 'GET'.

meta (dict [https://docs.python.org/3/library/stdtypes.html#dict]) – the initial values for the Request.meta attribute. If given, the dict passed in this parameter will be shallow copied.

body (str [https://docs.python.org/3/library/stdtypes.html#str] or unicode) – the request body. If a unicode is passed, then it’s encoded to str using the encoding passed (which defaults to utf-8). If body is not given, an empty string is stored. Regardless of the type of this argument, the final value stored will be a str (never unicode or None).

headers (dict [https://docs.python.org/3/library/stdtypes.html#dict]) – the headers of this request. The dict values can be strings (for single valued headers) or lists (for multi-valued headers). If None is passed as value, the HTTP header will not be sent at all.

cookies (dict [https://docs.python.org/3/library/stdtypes.html#dict] or list [https://docs.python.org/3/library/stdtypes.html#list]) –

the request cookies. These can be sent in two forms.

Using a dict:

request_with_cookies = Request(url="http://www.example.com", cookies={'currency': 'USD', 'country': 'UY'})

Using a list of dicts:

request_with_cookies = Request(url="http://www.example.com", cookies=[{'name': 'currency', 'value': 'USD', 'domain': 'example.com', 'path': '/currency'}])

The latter form allows for customizing the domain and path attributes of the cookie. This is only useful if the cookies are saved for later requests.

When some site returns cookies (in a response) those are stored in the cookies for that domain and will be sent again in future requests. That’s the typical behaviour of any regular web browser.

To create a request that does not send stored cookies and does not store received cookies, set the dont_merge_cookies key to True in request.meta.

Example of a request that sends manually-defined cookies and ignores cookie storage:

Request( url="http://www.example.com", cookies={'currency': 'USD', 'country': 'UY'}, meta={'dont_merge_cookies': True}, )

For more info see CookiesMiddleware.

encoding (string) – the encoding of this request (defaults to 'utf-8'). This encoding will be used to percent-encode the URL and to convert the body to str (if given as unicode).

priority (int [https://docs.python.org/3/library/functions.html#int]) – the priority of this request (defaults to 0). The priority is used by the scheduler to define the order used to process requests. Requests with a higher priority value will execute earlier. Negative values are allowed in order to indicate relatively low-priority.

dont_filter (boolean) – indicates that this request should not be filtered by the scheduler. This is used when you want to perform an identical request multiple times, to ignore the duplicates filter. Use it with care, or you will get into crawling loops. Default to False.

errback (callable) – a function that will be called if any exception was raised while processing the request. This includes pages that failed with 404 HTTP errors and such. It receives a Twisted Failure [https://twistedmatrix.com/documents/current/api/twisted.python.failure.Failure.html] instance as first parameter. For more information, see Using errbacks to catch exceptions in request processing below.

flags (list [https://docs.python.org/3/library/stdtypes.html#list]) – Flags sent to the request, can be used for logging or similar purposes.

cb_kwargs (dict [https://docs.python.org/3/library/stdtypes.html#dict]) – A dict with arbitrary data that will be passed as keyword arguments to the Request’s callback.

url

A string containing the URL of this request. Keep in mind that this attribute contains the escaped URL, so it can differ from the URL passed in the constructor.

This attribute is read-only. To change the URL of a Request use replace().

method

A string representing the HTTP method in the request. This is guaranteed to be uppercase. Example: "GET", "POST", "PUT", etc

headers

A dictionary-like object which contains the request headers.

body

A str that contains the request body.

This attribute is read-only. To change the body of a Request use replace().

meta

A dict that contains arbitrary metadata for this request. This dict is empty for new Requests, and is usually populated by different Scrapy components (extensions, middlewares, etc). So the data contained in this dict depends on the extensions you have enabled.

See Request.meta special keys for a list of special meta keys recognized by Scrapy.

This dict is shallow copied [https://docs.python.org/2/library/copy.html] when the request is cloned using the copy() or replace() methods, and can also be accessed, in your spider, from the response.meta attribute.

cb_kwargs

A dictionary that contains arbitrary metadata for this request. Its contents will be passed to the Request’s callback as keyword arguments. It is empty for new Requests, which means by default callbacks only get a Response object as argument.

This dict is shallow copied [https://docs.python.org/2/library/copy.html] when the request is cloned using the copy() or replace() methods, and can also be accessed, in your spider, from the response.cb_kwargs attribute.

copy()

Return a new Request which is a copy of this Request. See also: Passing additional data to callback functions.

replace([url, method, headers, body, cookies, meta, flags, encoding, priority, dont_filter, callback, errback, cb_kwargs])

Return a Request object with the same members, except for those members given new values by whichever keyword arguments are specified. The Request.cb_kwargs and Request.meta attributes are shallow copied by default (unless new values are given as arguments). See also Passing additional data to callback functions.

classmethod from_curl(curl_command, ignore_unknown_options=True, **kwargs)

Create a Request object from a string containing a cURL [https://curl.haxx.se/] command. It populates the HTTP method, the URL, the headers, the cookies and the body. It accepts the same arguments as the Request class, taking preference and overriding the values of the same arguments contained in the cURL command.

Unrecognized options are ignored by default. To raise an error when finding unknown options call this method by passing ignore_unknown_options=False.

Caution

Using from_curl() from Request subclasses, such as JSONRequest, or XmlRpcRequest, as well as having downloader middlewares and spider middlewares enabled, such as DefaultHeadersMiddleware, UserAgentMiddleware, or HttpCompressionMiddleware, may modify the Request object.

Passing additional data to callback functions

The callback of a request is a function that will be called when the response of that request is downloaded. The callback function will be called with the downloaded Response object as its first argument.

Example:

def parse_page1(self, response): return scrapy.Request("http://www.example.com/some_page.html", callback=self.parse_page2) def parse_page2(self, response): # this would log http://www.example.com/some_page.html self.logger.info("Visited %s", response.url)

In some cases you may be interested in passing arguments to those callback functions so you can receive the arguments later, in the second callback. The following example shows how to achieve this by using the Request.cb_kwargs attribute:

def parse(self, response): request = scrapy.Request('http://www.example.com/index.html', callback=self.parse_page2, cb_kwargs=dict(main_url=response.url)) request.cb_kwargs['foo'] = 'bar' # add more arguments for the callback yield request def parse_page2(self, response, main_url, foo): yield dict( main_url=main_url, other_url=response.url, foo=foo, )

Caution

Request.cb_kwargs was introduced in version 1.7. Prior to that, using Request.meta was recommended for passing information around callbacks. After 1.7, Request.cb_kwargs became the preferred way for handling user information, leaving Request.meta for communication with components like middlewares and extensions.

Using errbacks to catch exceptions in request processing

The errback of a request is a function that will be called when an exception is raise while processing it.

It receives a Twisted Failure [https://twistedmatrix.com/documents/current/api/twisted.python.failure.Failure.html] instance as first parameter and can be used to track connection establishment timeouts, DNS errors etc.

Here’s an example spider logging all errors and catching some specific errors if needed:

import scrapy from scrapy.spidermiddlewares.httperror import HttpError from twisted.internet.error import DNSLookupError from twisted.internet.error import TimeoutError, TCPTimedOutError class ErrbackSpider(scrapy.Spider): name = "errback_example" start_urls = [ "http://www.httpbin.org/", # HTTP 200 expected "http://www.httpbin.org/status/404", # Not found error "http://www.httpbin.org/status/500", # server issue "http://www.httpbin.org:12345/", # non-responding host, timeout expected "http://www.httphttpbinbin.org/", # DNS error expected ] def start_requests(self): for u in self.start_urls: yield scrapy.Request(u, callback=self.parse_httpbin, errback=self.errback_httpbin, dont_filter=True) def parse_httpbin(self, response): self.logger.info('Got successful response from {}'.format(response.url)) # do something useful here... def errback_httpbin(self, failure): # log all failures self.logger.error(repr(failure)) # in case you want to do something special for some errors, # you may need the failure's type: if failure.check(HttpError): # these exceptions come from HttpError spider middleware # you can get the non-200 response response = failure.value.response self.logger.error('HttpError on %s', response.url) elif failure.check(DNSLookupError): # this is the original request request = failure.request self.logger.error('DNSLookupError on %s', request.url) elif failure.check(TimeoutError, TCPTimedOutError): request = failure.request self.logger.error('TimeoutError on %s', request.url)

Request.meta special keys

The Request.meta attribute can contain any arbitrary data, but there are some special keys recognized by Scrapy and its built-in extensions.

Those are:

dont_redirect

dont_retry

handle_httpstatus_list

handle_httpstatus_all

dont_merge_cookies

cookiejar

dont_cache

redirect_reasons

redirect_urls

bindaddress

dont_obey_robotstxt

download_timeout

download_maxsize

download_latency

download_fail_on_dataloss

proxy

ftp_user (See FTP_USER for more info)

ftp_password (See FTP_PASSWORD for more info)

referrer_policy

max_retry_times

bindaddress

The IP of the outgoing IP address to use for the performing the request.

download_timeout

The amount of time (in secs) that the downloader will wait before timing out. See also: DOWNLOAD_TIMEOUT.

download_latency

The amount of time spent to fetch the response, since the request has been started, i.e. HTTP message sent over the network. This meta key only becomes available when the response has been downloaded. While most other meta keys are used to control Scrapy behavior, this one is supposed to be read-only.

download_fail_on_dataloss

Whether or not to fail on broken responses. See: DOWNLOAD_FAIL_ON_DATALOSS.

max_retry_times

The meta key is used set retry times per request. When initialized, the max_retry_times meta key takes higher precedence over the RETRY_TIMES setting.

Request subclasses

Here is the list of built-in Request subclasses. You can also subclass it to implement your own custom functionality.

FormRequest objects

The FormRequest class extends the base Request with functionality for dealing with HTML forms. It uses lxml.html forms [http://lxml.de/lxmlhtml.html#forms] to pre-populate form fields with form data from Response objects.

class scrapy.http.FormRequest(url[, formdata, ...])

The FormRequest class adds a new keyword parameter to the constructor. The remaining arguments are the same as for the Request class and are not documented here.

Parameters

formdata (dict [https://docs.python.org/3/library/stdtypes.html#dict] or iterable of tuples) – is a dictionary (or iterable of (key, value) tuples) containing HTML Form data which will be url-encoded and assigned to the body of the request.

The FormRequest objects support the following class method in addition to the standard Request methods:

classmethod from_response(response[, formname=None, formid=None, formnumber=0, formdata=None, formxpath=None, formcss=None, clickdata=None, dont_click=False, ...])

Returns a new FormRequest object with its form field values pre-populated with those found in the HTML <form> element contained in the given response. For an example see Using FormRequest.from_response() to simulate a user login.

The policy is to automatically simulate a click, by default, on any form control that looks clickable, like a <input type="submit">. Even though this is quite convenient, and often the desired behaviour, sometimes it can cause problems which could be hard to debug. For example, when working with forms that are filled and/or submitted using javascript, the default from_response() behaviour may not be the most appropriate. To disable this behaviour you can set the dont_click argument to True. Also, if you want to change the control clicked (instead of disabling it) you can also use the clickdata argument.

Caution

Using this method with select elements which have leading or trailing whitespace in the option values will not work due to a bug in lxml [https://bugs.launchpad.net/lxml/+bug/1665241], which should be fixed in lxml 3.8 and above.

Parameters

response (Response object) – the response containing a HTML form which will be used to pre-populate the form fields

formname (string) – if given, the form with name attribute set to this value will be used.

formid (string) – if given, the form with id attribute set to this value will be used.

formxpath (string) – if given, the first form that matches the xpath will be used.

formcss (string) – if given, the first form that matches the css selector will be used.

formnumber (integer) – the number of form to use, when the response contains multiple forms. The first one (and also the default) is 0.

formdata (dict [https://docs.python.org/3/library/stdtypes.html#dict]) – fields to override in the form data. If a field was already present in the response <form> element, its value is overridden by the one passed in this parameter. If a value passed in this parameter is None, the field will not be included in the request, even if it was present in the response <form> element.

clickdata (dict [https://docs.python.org/3/library/stdtypes.html#dict]) – attributes to lookup the control clicked. If it’s not given, the form data will be submitted simulating a click on the first clickable element. In addition to html attributes, the control can be identified by its zero-based index relative to other submittable inputs inside the form, via the nr attribute.

dont_click (boolean) – If True, the form data will be submitted without clicking in any element.

The other parameters of this class method are passed directly to the FormRequest constructor.

New in version 0.10.3: The formname parameter.

New in version 0.17: The formxpath parameter.

New in version 1.1.0: The formcss parameter.

New in version 1.1.0: The formid parameter.

Request usage examples

Using FormRequest to send data via HTTP POST

If you want to simulate a HTML Form POST in your spider and send a couple of key-value fields, you can return a FormRequest object (from your spider) like this:

return [FormRequest(url="http://www.example.com/post/action", formdata={'name': 'John Doe', 'age': '27'}, callback=self.after_post)]

Using FormRequest.from_response() to simulate a user login

It is usual for web sites to provide pre-populated form fields through <input type="hidden"> elements, such as session related data or authentication tokens (for login pages). When scraping, you’ll want these fields to be automatically pre-populated and only override a couple of them, such as the user name and password. You can use the FormRequest.from_response() method for this job. Here’s an example spider which uses it:

import scrapy def authentication_failed(response): # TODO: Check the contents of the response and return True if it failed # or False if it succeeded. pass class LoginSpider(scrapy.Spider): name = 'example.com' start_urls = ['http://www.example.com/users/login.php'] def parse(self, response): return scrapy.FormRequest.from_response( response, formdata={'username': 'john', 'password': 'secret'}, callback=self.after_login ) def after_login(self, response): if authentication_failed(response): self.logger.error("Login failed") return # continue scraping with authenticated session...

JsonRequest

The JsonRequest class extends the base Request class with functionality for dealing with JSON requests.

class scrapy.http.JsonRequest(url[, ... data, dumps_kwargs])

The JsonRequest class adds two new keyword parameters to the constructor. The remaining arguments are the same as for the Request class and are not documented here.

Using the JsonRequest will set the Content-Type header to application/json and Accept header to application/json, text/javascript, */*; q=0.01

Parameters

data (JSON serializable object) – is any JSON serializable object that needs to be JSON encoded and assigned to body. if Request.body argument is provided this parameter will be ignored. if Request.body argument is not provided and data argument is provided Request.method will be set to 'POST' automatically.

dumps_kwargs (dict [https://docs.python.org/3/library/stdtypes.html#dict]) – Parameters that will be passed to underlying json.dumps [https://docs.python.org/3/library/json.html#json.dumps] method which is used to serialize data into JSON format.

JsonRequest usage example

Sending a JSON POST request with a JSON payload:

data = { 'name1': 'value1', 'name2': 'value2', } yield JsonRequest(url='http://www.example.com/post/action', data=data)

Response objects

class scrapy.http.Response(url, status=200, headers=None, body=b'', flags=None, request=None)

A Response object represents an HTTP response, which is usually downloaded (by the Downloader) and fed to the Spiders for processing.

Parameters

url (string) – the URL of this response

status (integer) – the HTTP status of the response. Defaults to 200.

headers (dict [https://docs.python.org/3/library/stdtypes.html#dict]) – the headers of this response. The dict values can be strings (for single valued headers) or lists (for multi-valued headers).

body (bytes [https://docs.python.org/3/library/stdtypes.html#bytes]) – the response body. To access the decoded text as str (unicode in Python 2) you can use response.text from an encoding-aware Response subclass, such as TextResponse.

flags (list [https://docs.python.org/3/library/stdtypes.html#list]) – is a list containing the initial values for the Response.flags attribute. If given, the list will be shallow copied.

request (Request object) – the initial value of the Response.request attribute. This represents the Request that generated this response.

url

A string containing the URL of the response.

This attribute is read-only. To change the URL of a Response use replace().

status

An integer representing the HTTP status of the response. Example: 200, 404.

headers

A dictionary-like object which contains the response headers. Values can be accessed using get() to return the first header value with the specified name or getlist() to return all header values with the specified name. For example, this call will give you all cookies in the headers:

response.headers.getlist('Set-Cookie')

body

The body of this Response. Keep in mind that Response.body is always a bytes object. If you want the unicode version use TextResponse.text (only available in TextResponse and subclasses).

This attribute is read-only. To change the body of a Response use replace().

request

The Request object that generated this response. This attribute is assigned in the Scrapy engine, after the response and the request have passed through all Downloader Middlewares. In particular, this means that:

HTTP redirections will cause the original request (to the URL before redirection) to be assigned to the redirected response (with the final URL after redirection).

Response.request.url doesn’t always equal Response.url

This attribute is only available in the spider code, and in the Spider Middlewares, but not in Downloader Middlewares (although you have the Request available there by other means) and handlers of the response_downloaded signal.

meta

A shortcut to the Request.meta attribute of the Response.request object (ie. self.request.meta).

Unlike the Response.request attribute, the Response.meta attribute is propagated along redirects and retries, so you will get the original Request.meta sent from your spider.

See also

Request.meta attribute

flags

A list that contains flags for this response. Flags are labels used for tagging Responses. For example: 'cached', 'redirected’, etc. And they’re shown on the string representation of the Response (__str__ method) which is used by the engine for logging.

copy()

Returns a new Response which is a copy of this Response.

replace([url, status, headers, body, request, flags, cls])

Returns a Response object with the same members, except for those members given new values by whichever keyword arguments are specified. The attribute Response.meta is copied by default.

urljoin(url)

Constructs an absolute url by combining the Response’s url with a possible relative url.

This is a wrapper over urlparse.urljoin [https://docs.python.org/2/library/urlparse.html#urlparse.urljoin], it’s merely an alias for making this call:

urlparse.urljoin(response.url, url)

follow(url, callback=None, method='GET', headers=None, body=None, cookies=None, meta=None, encoding='utf-8', priority=0, dont_filter=False, errback=None, cb_kwargs=None)

Return a Request instance to follow a link url. It accepts the same arguments as Request.__init__ method, but url can be a relative URL or a scrapy.link.Link object, not only an absolute URL.

TextResponse provides a follow() method which supports selectors in addition to absolute/relative URLs and Link objects.

Response subclasses

Here is the list of available built-in Response subclasses. You can also subclass the Response class to implement your own functionality.

TextResponse objects

class scrapy.http.TextResponse(url[, encoding[, ...]])

TextResponse objects adds encoding capabilities to the base Response class, which is meant to be used only for binary data, such as images, sounds or any media file.

TextResponse objects support a new constructor argument, in addition to the base Response objects. The remaining functionality is the same as for the Response class and is not documented here.

Parameters

encoding (string) – is a string which contains the encoding to use for this response. If you create a TextResponse object with a unicode body, it will be encoded using this encoding (remember the body attribute is always a string). If encoding is None (default value), the encoding will be looked up in the response headers and body instead.

TextResponse objects support the following attributes in addition to the standard Response ones:

text

Response body, as unicode.

The same as response.body.decode(response.encoding), but the result is cached after the first call, so you can access response.text multiple times without extra overhead.

Note

unicode(response.body) is not a correct way to convert response body to unicode: you would be using the system default encoding (typically ascii) instead of the response encoding.

encoding

A string with the encoding of this response. The encoding is resolved by trying the following mechanisms, in order:

the encoding passed in the constructor encoding argument

the encoding declared in the Content-Type HTTP header. If this encoding is not valid (ie. unknown), it is ignored and the next resolution mechanism is tried.

the encoding declared in the response body. The TextResponse class doesn’t provide any special functionality for this. However, the HtmlResponse and XmlResponse classes do.

the encoding inferred by looking at the response body. This is the more fragile method but also the last one tried.

selector

A Selector instance using the response as target. The selector is lazily instantiated on first access.

TextResponse objects support the following methods in addition to the standard Response ones:

xpath(query)

A shortcut to TextResponse.selector.xpath(query):

response.xpath('//p')

css(query)

A shortcut to TextResponse.selector.css(query):

response.css('p')

follow(url, callback=None, method='GET', headers=None, body=None, cookies=None, meta=None, encoding=None, priority=0, dont_filter=False, errback=None, cb_kwargs=None)

Return a Request instance to follow a link url. It accepts the same arguments as Request.__init__ method, but url can be not only an absolute URL, but also

a relative URL;

a scrapy.link.Link object (e.g. a link extractor result);

an attribute Selector (not SelectorList) - e.g. response.css('a::attr(href)')[0] or response.xpath('//img/@src')[0].

a Selector for <a> or <link> element, e.g. response.css('a.my_link')[0].

See A shortcut for creating Requests for usage examples.

body_as_unicode()

The same as text, but available as a method. This method is kept for backward compatibility; please prefer response.text.

HtmlResponse objects

class scrapy.http.HtmlResponse(url[, ...])

The HtmlResponse class is a subclass of TextResponse which adds encoding auto-discovering support by looking into the HTML meta http-equiv [https://www.w3schools.com/TAGS/att_meta_http_equiv.asp] attribute. See TextResponse.encoding.

XmlResponse objects

class scrapy.http.XmlResponse(url[, ...])

The XmlResponse class is a subclass of TextResponse which adds encoding auto-discovering support by looking into the XML declaration line. See TextResponse.encoding.

Link Extractors

Link extractors are objects whose only purpose is to extract links from web pages (scrapy.http.Response objects) which will be eventually followed.

There is scrapy.linkextractors.LinkExtractor available in Scrapy, but you can create your own custom Link Extractors to suit your needs by implementing a simple interface.

The only public method that every link extractor has is extract_links, which receives a Response object and returns a list of scrapy.link.Link objects. Link extractors are meant to be instantiated once and their extract_links method called several times with different responses to extract links to follow.

Link extractors are used in the CrawlSpider class (available in Scrapy), through a set of rules, but you can also use it in your spiders, even if you don’t subclass from CrawlSpider, as its purpose is very simple: to extract links.

Built-in link extractors reference

Link extractors classes bundled with Scrapy are provided in the scrapy.linkextractors module.

The default link extractor is LinkExtractor, which is the same as LxmlLinkExtractor:

from scrapy.linkextractors import LinkExtractor

There used to be other link extractor classes in previous Scrapy versions, but they are deprecated now.

LxmlLinkExtractor

class scrapy.linkextractors.lxmlhtml.LxmlLinkExtractor(allow=(), deny=(), allow_domains=(), deny_domains=(), deny_extensions=None, restrict_xpaths=(), restrict_css=(), tags=('a', 'area'), attrs=('href', ), canonicalize=False, unique=True, process_value=None, strip=True)

LxmlLinkExtractor is the recommended link extractor with handy filtering options. It is implemented using lxml’s robust HTMLParser.

Parameters

allow (a regular expression (or list of)) – a single regular expression (or list of regular expressions) that the (absolute) urls must match in order to be extracted. If not given (or empty), it will match all links.

deny (a regular expression (or list of)) – a single regular expression (or list of regular expressions) that the (absolute) urls must match in order to be excluded (ie. not extracted). It has precedence over the allow parameter. If not given (or empty) it won’t exclude any links.

allow_domains (str [https://docs.python.org/3/library/stdtypes.html#str] or list [https://docs.python.org/3/library/stdtypes.html#list]) – a single value or a list of string containing domains which will be considered for extracting the links

deny_domains (str [https://docs.python.org/3/library/stdtypes.html#str] or list [https://docs.python.org/3/library/stdtypes.html#list]) – a single value or a list of strings containing domains which won’t be considered for extracting the links

deny_extensions (list [https://docs.python.org/3/library/stdtypes.html#list]) – a single value or list of strings containing extensions that should be ignored when extracting links. If not given, it will default to the IGNORED_EXTENSIONS list defined in the scrapy.linkextractors [https://github.com/scrapy/scrapy/blob/master/scrapy/linkextractors/__init__.py] package.

restrict_xpaths (str [https://docs.python.org/3/library/stdtypes.html#str] or list [https://docs.python.org/3/library/stdtypes.html#list]) – is an XPath (or list of XPath’s) which defines regions inside the response where links should be extracted from. If given, only the text selected by those XPath will be scanned for links. See examples below.

restrict_css (str [https://docs.python.org/3/library/stdtypes.html#str] or list [https://docs.python.org/3/library/stdtypes.html#list]) – a CSS selector (or list of selectors) which defines regions inside the response where links should be extracted from. Has the same behaviour as restrict_xpaths.

restrict_text (a regular expression (or list of)) – a single regular expression (or list of regular expressions) that the link’s text must match in order to be extracted. If not given (or empty), it will match all links. If a list of regular expressions is given, the link will be extracted if it matches at least one.

tags (str [https://docs.python.org/3/library/stdtypes.html#str] or list [https://docs.python.org/3/library/stdtypes.html#list]) – a tag or a list of tags to consider when extracting links. Defaults to ('a', 'area').

attrs (list [https://docs.python.org/3/library/stdtypes.html#list]) – an attribute or list of attributes which should be considered when looking for links to extract (only for those tags specified in the tags parameter). Defaults to ('href',)

canonicalize (boolean) – canonicalize each extracted url (using w3lib.url.canonicalize_url). Defaults to False. Note that canonicalize_url is meant for duplicate checking; it can change the URL visible at server side, so the response can be different for requests with canonicalized and raw URLs. If you’re using LinkExtractor to follow links it is more robust to keep the default canonicalize=False.

unique (boolean) – whether duplicate filtering should be applied to extracted links.

process_value (callable) –

a function which receives each value extracted from the tag and attributes scanned and can modify the value and return a new one, or return None to ignore the link altogether. If not given, process_value defaults to lambda x: x.

For example, to extract links from this code:

<a href="javascript:goToPage('../other/page.html'); return false">Link text</a>

You can use the following function in process_value:

def process_value(value): m = re.search("javascript:goToPage\('(.*?)'", value) if m: return m.group(1)

strip (boolean) – whether to strip whitespaces from extracted attributes. According to HTML5 standard, leading and trailing whitespaces must be stripped from href attributes of <a>, <area> and many other elements, src attribute of <img>, <iframe> elements, etc., so LinkExtractor strips space chars by default. Set strip=False to turn it off (e.g. if you’re extracting urls from elements or attributes which allow leading/trailing whitespaces).

Settings

The Scrapy settings allows you to customize the behaviour of all Scrapy components, including the core, extensions, pipelines and spiders themselves.

The infrastructure of the settings provides a global namespace of key-value mappings that the code can use to pull configuration values from. The settings can be populated through different mechanisms, which are described below.

The settings are also the mechanism for selecting the currently active Scrapy project (in case you have many).

For a list of available built-in settings see: Built-in settings reference.

Designating the settings

When you use Scrapy, you have to tell it which settings you’re using. You can do this by using an environment variable, SCRAPY_SETTINGS_MODULE.

The value of SCRAPY_SETTINGS_MODULE should be in Python path syntax, e.g. myproject.settings. Note that the settings module should be on the Python import search path [https://docs.python.org/2/tutorial/modules.html#the-module-search-path].

Populating the settings

Settings can be populated using different mechanisms, each of which having a different precedence. Here is the list of them in decreasing order of precedence:

Command line options (most precedence)

Settings per-spider

Project settings module

Default settings per-command

Default global settings (less precedence)

The population of these settings sources is taken care of internally, but a manual handling is possible using API calls. See the Settings API topic for reference.

These mechanisms are described in more detail below.

1. Command line options

Arguments provided by the command line are the ones that take most precedence, overriding any other options. You can explicitly override one (or more) settings using the -s (or --set) command line option.

Example:

scrapy crawl myspider -s LOG_FILE=scrapy.log

2. Settings per-spider

Spiders (See the Spiders chapter for reference) can define their own settings that will take precedence and override the project ones. They can do so by setting their custom_settings attribute:

class MySpider(scrapy.Spider): name = 'myspider' custom_settings = { 'SOME_SETTING': 'some value', }

3. Project settings module

The project settings module is the standard configuration file for your Scrapy project, it’s where most of your custom settings will be populated. For a standard Scrapy project, this means you’ll be adding or changing the settings in the settings.py file created for your project.

4. Default settings per-command

Each Scrapy tool command can have its own default settings, which override the global default settings. Those custom command settings are specified in the default_settings attribute of the command class.

5. Default global settings

The global defaults are located in the scrapy.settings.default_settings module and documented in the Built-in settings reference section.

How to access settings

In a spider, the settings are available through self.settings:

class MySpider(scrapy.Spider): name = 'myspider' start_urls = ['http://example.com'] def parse(self, response): print("Existing settings: %s" % self.settings.attributes.keys())

Note

The settings attribute is set in the base Spider class after the spider is initialized. If you want to use the settings before the initialization (e.g., in your spider’s __init__() method), you’ll need to override the from_crawler() method.

Settings can be accessed through the scrapy.crawler.Crawler.settings attribute of the Crawler that is passed to from_crawler method in extensions, middlewares and item pipelines:

class MyExtension(object): def __init__(self, log_is_enabled=False): if log_is_enabled: print("log is enabled!") @classmethod def from_crawler(cls, crawler): settings = crawler.settings return cls(settings.getbool('LOG_ENABLED'))

The settings object can be used like a dict (e.g., settings['LOG_ENABLED']), but it’s usually preferred to extract the setting in the format you need it to avoid type errors, using one of the methods provided by the Settings API.

Rationale for setting names

Setting names are usually prefixed with the component that they configure. For example, proper setting names for a fictional robots.txt extension would be ROBOTSTXT_ENABLED, ROBOTSTXT_OBEY, ROBOTSTXT_CACHEDIR, etc.

Built-in settings reference

Here’s a list of all available Scrapy settings, in alphabetical order, along with their default values and the scope where they apply.

The scope, where available, shows where the setting is being used, if it’s tied to any particular component. In that case the module of that component will be shown, typically an extension, middleware or pipeline. It also means that the component must be enabled in order for the setting to have any effect.

AWS_ACCESS_KEY_ID

Default: None

The AWS access key used by code that requires access to Amazon Web services [https://aws.amazon.com/], such as the S3 feed storage backend.

AWS_SECRET_ACCESS_KEY

Default: None

The AWS secret key used by code that requires access to Amazon Web services [https://aws.amazon.com/], such as the S3 feed storage backend.

AWS_ENDPOINT_URL

Default: None

Endpoint URL used for S3-like storage, for example Minio or s3.scality. Only supported with botocore library.

AWS_USE_SSL

Default: None

Use this option if you want to disable SSL connection for communication with S3 or S3-like storage. By default SSL will be used. Only supported with botocore library.

AWS_VERIFY

Default: None

Verify SSL connection between Scrapy and S3 or S3-like storage. By default SSL verification will occur. Only supported with botocore library.

AWS_REGION_NAME

Default: None

The name of the region associated with the AWS client. Only supported with botocore library.

BOT_NAME

Default: 'scrapybot'

The name of the bot implemented by this Scrapy project (also known as the project name). This name will be used for the logging too.

It’s automatically populated with your project name when you create your project with the startproject command.

CONCURRENT_ITEMS

Default: 100

Maximum number of concurrent items (per response) to process in parallel in the Item Processor (also known as the Item Pipeline).

CONCURRENT_REQUESTS

Default: 16

The maximum number of concurrent (ie. simultaneous) requests that will be performed by the Scrapy downloader.

CONCURRENT_REQUESTS_PER_DOMAIN

Default: 8

The maximum number of concurrent (ie. simultaneous) requests that will be performed to any single domain.

See also: AutoThrottle extension and its AUTOTHROTTLE_TARGET_CONCURRENCY option.

CONCURRENT_REQUESTS_PER_IP

Default: 0

The maximum number of concurrent (ie. simultaneous) requests that will be performed to any single IP. If non-zero, the CONCURRENT_REQUESTS_PER_DOMAIN setting is ignored, and this one is used instead. In other words, concurrency limits will be applied per IP, not per domain.

This setting also affects DOWNLOAD_DELAY and AutoThrottle extension: if CONCURRENT_REQUESTS_PER_IP is non-zero, download delay is enforced per IP, not per domain.

DEFAULT_ITEM_CLASS

Default: 'scrapy.item.Item'

The default class that will be used for instantiating items in the the Scrapy shell.

DEFAULT_REQUEST_HEADERS

Default:

{ 'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8', 'Accept-Language': 'en', }

The default headers used for Scrapy HTTP Requests. They’re populated in the DefaultHeadersMiddleware.

DEPTH_LIMIT

Default: 0

Scope: scrapy.spidermiddlewares.depth.DepthMiddleware

The maximum depth that will be allowed to crawl for any site. If zero, no limit will be imposed.

DEPTH_PRIORITY

Default: 0

Scope: scrapy.spidermiddlewares.depth.DepthMiddleware

An integer that is used to adjust the priority of a Request based on its depth.

The priority of a request is adjusted as follows:

request.priority = request.priority - ( depth * DEPTH_PRIORITY )

As depth increases, positive values of DEPTH_PRIORITY decrease request priority (BFO), while negative values increase request priority (DFO). See also Does Scrapy crawl in breadth-first or depth-first order?.

Note

This setting adjusts priority in the opposite way compared to other priority settings REDIRECT_PRIORITY_ADJUST and RETRY_PRIORITY_ADJUST.

DEPTH_STATS_VERBOSE

Default: False

Scope: scrapy.spidermiddlewares.depth.DepthMiddleware

Whether to collect verbose depth stats. If this is enabled, the number of requests for each depth is collected in the stats.

DNSCACHE_ENABLED

Default: True

Whether to enable DNS in-memory cache.

DNSCACHE_SIZE

Default: 10000

DNS in-memory cache size.

DNS_TIMEOUT

Default: 60

Timeout for processing of DNS queries in seconds. Float is supported.

DOWNLOADER

Default: 'scrapy.core.downloader.Downloader'

The downloader to use for crawling.

DOWNLOADER_HTTPCLIENTFACTORY

Default: 'scrapy.core.downloader.webclient.ScrapyHTTPClientFactory'

Defines a Twisted protocol.ClientFactory class to use for HTTP/1.0 connections (for HTTP10DownloadHandler).

Note

HTTP/1.0 is rarely used nowadays so you can safely ignore this setting, unless you use Twisted<11.1, or if you really want to use HTTP/1.0 and override DOWNLOAD_HANDLERS_BASE for http(s) scheme accordingly, i.e. to 'scrapy.core.downloader.handlers.http.HTTP10DownloadHandler'.

DOWNLOADER_CLIENTCONTEXTFACTORY

Default: 'scrapy.core.downloader.contextfactory.ScrapyClientContextFactory'

Represents the classpath to the ContextFactory to use.

Here,「ContextFactory」is a Twisted term for SSL/TLS contexts, defining the TLS/SSL protocol version to use, whether to do certificate verification, or even enable client-side authentication (and various other things).

Note

Scrapy default context factory does NOT perform remote server certificate verification. This is usually fine for web scraping.

If you do need remote server certificate verification enabled, Scrapy also has another context factory class that you can set, 'scrapy.core.downloader.contextfactory.BrowserLikeContextFactory', which uses the platform’s certificates to validate remote endpoints. This is only available if you use Twisted>=14.0.

If you do use a custom ContextFactory, make sure its __init__ method accepts a method parameter (this is the OpenSSL.SSL method mapping DOWNLOADER_CLIENT_TLS_METHOD), a tls_verbose_logging parameter (bool) and a tls_ciphers parameter (see DOWNLOADER_CLIENT_TLS_CIPHERS).

DOWNLOADER_CLIENT_TLS_CIPHERS

Default: 'DEFAULT'

Use this setting to customize the TLS/SSL ciphers used by the default HTTP/1.1 downloader.

The setting should contain a string in the OpenSSL cipher list format [https://www.openssl.org/docs/manmaster/man1/ciphers.html#CIPHER-LIST-FORMAT], these ciphers will be used as client ciphers. Changing this setting may be necessary to access certain HTTPS websites: for example, you may need to use 'DEFAULT:!DH' for a website with weak DH parameters or enable a specific cipher that is not included in DEFAULT if a website requires it.

DOWNLOADER_CLIENT_TLS_METHOD

Default: 'TLS'

Use this setting to customize the TLS/SSL method used by the default HTTP/1.1 downloader.

This setting must be one of these string values:

'TLS': maps to OpenSSL’s TLS_method() (a.k.a SSLv23_method()), which allows protocol negotiation, starting from the highest supported by the platform; default, recommended

'TLSv1.0': this value forces HTTPS connections to use TLS version 1.0 ; set this if you want the behavior of Scrapy<1.1

'TLSv1.1': forces TLS version 1.1

'TLSv1.2': forces TLS version 1.2

'SSLv3': forces SSL version 3 (not recommended)

Note

We recommend that you use PyOpenSSL>=0.13 and Twisted>=0.13 or above (Twisted>=14.0 if you can).

DOWNLOADER_CLIENT_TLS_VERBOSE_LOGGING

Default: False

Setting this to True will enable DEBUG level messages about TLS connection parameters after establishing HTTPS connections. The kind of information logged depends on the versions of OpenSSL and pyOpenSSL.

This setting is only used for the default DOWNLOADER_CLIENTCONTEXTFACTORY.

DOWNLOADER_MIDDLEWARES

Default:: {}

A dict containing the downloader middlewares enabled in your project, and their orders. For more info see Activating a downloader middleware.

DOWNLOADER_MIDDLEWARES_BASE

Default:

{ 'scrapy.downloadermiddlewares.robotstxt.RobotsTxtMiddleware': 100, 'scrapy.downloadermiddlewares.httpauth.HttpAuthMiddleware': 300, 'scrapy.downloadermiddlewares.downloadtimeout.DownloadTimeoutMiddleware': 350, 'scrapy.downloadermiddlewares.defaultheaders.DefaultHeadersMiddleware': 400, 'scrapy.downloadermiddlewares.useragent.UserAgentMiddleware': 500, 'scrapy.downloadermiddlewares.retry.RetryMiddleware': 550, 'scrapy.downloadermiddlewares.ajaxcrawl.AjaxCrawlMiddleware': 560, 'scrapy.downloadermiddlewares.redirect.MetaRefreshMiddleware': 580, 'scrapy.downloadermiddlewares.httpcompression.HttpCompressionMiddleware': 590, 'scrapy.downloadermiddlewares.redirect.RedirectMiddleware': 600, 'scrapy.downloadermiddlewares.cookies.CookiesMiddleware': 700, 'scrapy.downloadermiddlewares.httpproxy.HttpProxyMiddleware': 750, 'scrapy.downloadermiddlewares.stats.DownloaderStats': 850, 'scrapy.downloadermiddlewares.httpcache.HttpCacheMiddleware': 900, }

A dict containing the downloader middlewares enabled by default in Scrapy. Low orders are closer to the engine, high orders are closer to the downloader. You should never modify this setting in your project, modify DOWNLOADER_MIDDLEWARES instead. For more info see Activating a downloader middleware.

DOWNLOADER_STATS

Default: True

Whether to enable downloader stats collection.

DOWNLOAD_DELAY

Default: 0

The amount of time (in secs) that the downloader should wait before downloading consecutive pages from the same website. This can be used to throttle the crawling speed to avoid hitting servers too hard. Decimal numbers are supported. Example:

DOWNLOAD_DELAY = 0.25 # 250 ms of delay

This setting is also affected by the RANDOMIZE_DOWNLOAD_DELAY setting (which is enabled by default). By default, Scrapy doesn’t wait a fixed amount of time between requests, but uses a random interval between 0.5 * DOWNLOAD_DELAY and 1.5 * DOWNLOAD_DELAY.

When CONCURRENT_REQUESTS_PER_IP is non-zero, delays are enforced per ip address instead of per domain.

You can also change this setting per spider by setting download_delay spider attribute.

DOWNLOAD_HANDLERS

Default: {}

A dict containing the request downloader handlers enabled in your project. See DOWNLOAD_HANDLERS_BASE for example format.

DOWNLOAD_HANDLERS_BASE

Default:

{ 'file': 'scrapy.core.downloader.handlers.file.FileDownloadHandler', 'http': 'scrapy.core.downloader.handlers.http.HTTPDownloadHandler', 'https': 'scrapy.core.downloader.handlers.http.HTTPDownloadHandler', 's3': 'scrapy.core.downloader.handlers.s3.S3DownloadHandler', 'ftp': 'scrapy.core.downloader.handlers.ftp.FTPDownloadHandler', }

A dict containing the request download handlers enabled by default in Scrapy. You should never modify this setting in your project, modify DOWNLOAD_HANDLERS instead.

You can disable any of these download handlers by assigning None to their URI scheme in DOWNLOAD_HANDLERS. E.g., to disable the built-in FTP handler (without replacement), place this in your settings.py:

DOWNLOAD_HANDLERS = { 'ftp': None, }

DOWNLOAD_TIMEOUT

Default: 180

The amount of time (in secs) that the downloader will wait before timing out.

Note

This timeout can be set per spider using download_timeout spider attribute and per-request using download_timeout Request.meta key.

DOWNLOAD_MAXSIZE

Default: 1073741824 (1024MB)

The maximum response size (in bytes) that downloader will download.

If you want to disable it set to 0.

Note

This size can be set per spider using download_maxsize spider attribute and per-request using download_maxsize Request.meta key.

This feature needs Twisted >= 11.1.

DOWNLOAD_WARNSIZE

Default: 33554432 (32MB)

The response size (in bytes) that downloader will start to warn.

If you want to disable it set to 0.

Note

This size can be set per spider using download_warnsize spider attribute and per-request using download_warnsize Request.meta key.

This feature needs Twisted >= 11.1.

DOWNLOAD_FAIL_ON_DATALOSS

Default: True

Whether or not to fail on broken responses, that is, declared Content-Length does not match content sent by the server or chunked response was not properly finish. If True, these responses raise a ResponseFailed([_DataLoss]) error. If False, these responses are passed through and the flag dataloss is added to the response, i.e.: 'dataloss' in response.flags is True.

Optionally, this can be set per-request basis by using the download_fail_on_dataloss Request.meta key to False.

Note

A broken response, or data loss error, may happen under several circumstances, from server misconfiguration to network errors to data corruption. It is up to the user to decide if it makes sense to process broken responses considering they may contain partial or incomplete content. If RETRY_ENABLED is True and this setting is set to True, the ResponseFailed([_DataLoss]) failure will be retried as usual.

DUPEFILTER_CLASS

Default: 'scrapy.dupefilters.RFPDupeFilter'

The class used to detect and filter duplicate requests.

The default (RFPDupeFilter) filters based on request fingerprint using the scrapy.utils.request.request_fingerprint function. In order to change the way duplicates are checked you could subclass RFPDupeFilter and override its request_fingerprint method. This method should accept scrapy Request object and return its fingerprint (a string).

You can disable filtering of duplicate requests by setting DUPEFILTER_CLASS to 'scrapy.dupefilters.BaseDupeFilter'. Be very careful about this however, because you can get into crawling loops. It’s usually a better idea to set the dont_filter parameter to True on the specific Request that should not be filtered.

DUPEFILTER_DEBUG

Default: False

By default, RFPDupeFilter only logs the first duplicate request. Setting DUPEFILTER_DEBUG to True will make it log all duplicate requests.

EDITOR

Default: vi (on Unix systems) or the IDLE editor (on Windows)

The editor to use for editing spiders with the edit command. Additionally, if the EDITOR environment variable is set, the edit command will prefer it over the default setting.

EXTENSIONS

Default:: {}

A dict containing the extensions enabled in your project, and their orders.

EXTENSIONS_BASE

Default:

{ 'scrapy.extensions.corestats.CoreStats': 0, 'scrapy.extensions.telnet.TelnetConsole': 0, 'scrapy.extensions.memusage.MemoryUsage': 0, 'scrapy.extensions.memdebug.MemoryDebugger': 0, 'scrapy.extensions.closespider.CloseSpider': 0, 'scrapy.extensions.feedexport.FeedExporter': 0, 'scrapy.extensions.logstats.LogStats': 0, 'scrapy.extensions.spiderstate.SpiderState': 0, 'scrapy.extensions.throttle.AutoThrottle': 0, }

A dict containing the extensions available by default in Scrapy, and their orders. This setting contains all stable built-in extensions. Keep in mind that some of them need to be enabled through a setting.

For more information See the extensions user guide and the list of available extensions.

FEED_TEMPDIR

The Feed Temp dir allows you to set a custom folder to save crawler temporary files before uploading with FTP feed storage and Amazon S3.

FTP_PASSIVE_MODE

Default: True

Whether or not to use passive mode when initiating FTP transfers.

FTP_PASSWORD

Default: "guest"

The password to use for FTP connections when there is no "ftp_password" in Request meta.

Note

Paraphrasing RFC 1635 [https://tools.ietf.org/html/rfc1635], although it is common to use either the password「guest」or one’s e-mail address for anonymous FTP, some FTP servers explicitly ask for the user’s e-mail address and will not allow login with the「guest」password.

FTP_USER

Default: "anonymous"

The username to use for FTP connections when there is no "ftp_user" in Request meta.

ITEM_PIPELINES

Default: {}

A dict containing the item pipelines to use, and their orders. Order values are arbitrary, but it is customary to define them in the 0-1000 range. Lower orders process before higher orders.

Example:

ITEM_PIPELINES = { 'mybot.pipelines.validate.ValidateMyItem': 300, 'mybot.pipelines.validate.StoreMyItem': 800, }

ITEM_PIPELINES_BASE

Default: {}

A dict containing the pipelines enabled by default in Scrapy. You should never modify this setting in your project, modify ITEM_PIPELINES instead.

LOG_ENABLED

Default: True

Whether to enable logging.

LOG_ENCODING

Default: 'utf-8'

The encoding to use for logging.

LOG_FILE

Default: None

File name to use for logging output. If None, standard error will be used.

LOG_FORMAT

Default: '%(asctime)s [%(name)s] %(levelname)s: %(message)s'

String for formatting log messsages. Refer to the Python logging documentation [https://docs.python.org/2/library/logging.html#logrecord-attributes] for the whole list of available placeholders.

LOG_DATEFORMAT

Default: '%Y-%m-%d %H:%M:%S'

String for formatting date/time, expansion of the %(asctime)s placeholder in LOG_FORMAT. Refer to the Python datetime documentation [https://docs.python.org/2/library/datetime.html#strftime-and-strptime-behavior] for the whole list of available directives.

LOG_FORMATTER

Default: scrapy.logformatter.LogFormatter

The class to use for formatting log messages for different actions.

LOG_LEVEL

Default: 'DEBUG'

Minimum level to log. Available levels are: CRITICAL, ERROR, WARNING, INFO, DEBUG. For more info see Logging.

LOG_STDOUT

Default: False

If True, all standard output (and error) of your process will be redirected to the log. For example if you print('hello') it will appear in the Scrapy log.

LOG_SHORT_NAMES

Default: False

If True, the logs will just contain the root path. If it is set to False then it displays the component responsible for the log output

LOGSTATS_INTERVAL

Default: 60.0

The interval (in seconds) between each logging printout of the stats by LogStats.

MEMDEBUG_ENABLED

Default: False

Whether to enable memory debugging.

MEMDEBUG_NOTIFY

Default: []

When memory debugging is enabled a memory report will be sent to the specified addresses if this setting is not empty, otherwise the report will be written to the log.

Example:

MEMDEBUG_NOTIFY = ['user@example.com']

MEMUSAGE_ENABLED

Default: True

Scope: scrapy.extensions.memusage

Whether to enable the memory usage extension. This extension keeps track of a peak memory used by the process (it writes it to stats). It can also optionally shutdown the Scrapy process when it exceeds a memory limit (see MEMUSAGE_LIMIT_MB), and notify by email when that happened (see MEMUSAGE_NOTIFY_MAIL).

See Memory usage extension.

MEMUSAGE_LIMIT_MB

Default: 0

Scope: scrapy.extensions.memusage

The maximum amount of memory to allow (in megabytes) before shutting down Scrapy (if MEMUSAGE_ENABLED is True). If zero, no check will be performed.

See Memory usage extension.

MEMUSAGE_CHECK_INTERVAL_SECONDS

New in version 1.1.

Default: 60.0

Scope: scrapy.extensions.memusage

The Memory usage extension checks the current memory usage, versus the limits set by MEMUSAGE_LIMIT_MB and MEMUSAGE_WARNING_MB, at fixed time intervals.

This sets the length of these intervals, in seconds.

See Memory usage extension.

MEMUSAGE_NOTIFY_MAIL

Default: False

Scope: scrapy.extensions.memusage

A list of emails to notify if the memory limit has been reached.

Example:

MEMUSAGE_NOTIFY_MAIL = ['user@example.com']

See Memory usage extension.

MEMUSAGE_WARNING_MB

Default: 0

Scope: scrapy.extensions.memusage

The maximum amount of memory to allow (in megabytes) before sending a warning email notifying about it. If zero, no warning will be produced.

NEWSPIDER_MODULE

Default: ''

Module where to create new spiders using the genspider command.

Example:

NEWSPIDER_MODULE = 'mybot.spiders_dev'

RANDOMIZE_DOWNLOAD_DELAY

Default: True

If enabled, Scrapy will wait a random amount of time (between 0.5 * DOWNLOAD_DELAY and 1.5 * DOWNLOAD_DELAY) while fetching requests from the same website.

This randomization decreases the chance of the crawler being detected (and subsequently blocked) by sites which analyze requests looking for statistically significant similarities in the time between their requests.

The randomization policy is the same used by wget [https://www.gnu.org/software/wget/manual/wget.html] --random-wait option.

If DOWNLOAD_DELAY is zero (default) this option has no effect.

REACTOR_THREADPOOL_MAXSIZE

Default: 10

The maximum limit for Twisted Reactor thread pool size. This is common multi-purpose thread pool used by various Scrapy components. Threaded DNS Resolver, BlockingFeedStorage, S3FilesStore just to name a few. Increase this value if you’re experiencing problems with insufficient blocking IO.

REDIRECT_MAX_TIMES

Default: 20

Defines the maximum times a request can be redirected. After this maximum the request’s response is returned as is. We used Firefox default value for the same task.

REDIRECT_PRIORITY_ADJUST

Default: +2

Scope: scrapy.downloadermiddlewares.redirect.RedirectMiddleware

Adjust redirect request priority relative to original request:

a positive priority adjust (default) means higher priority.

a negative priority adjust means lower priority.

RETRY_PRIORITY_ADJUST

Default: -1

Scope: scrapy.downloadermiddlewares.retry.RetryMiddleware

Adjust retry request priority relative to original request:

a positive priority adjust means higher priority.

a negative priority adjust (default) means lower priority.

ROBOTSTXT_OBEY

Default: False

Scope: scrapy.downloadermiddlewares.robotstxt

If enabled, Scrapy will respect robots.txt policies. For more information see RobotsTxtMiddleware.

Note

While the default value is False for historical reasons, this option is enabled by default in settings.py file generated by scrapy startproject command.

ROBOTSTXT_PARSER

Default: 'scrapy.robotstxt.ProtegoRobotParser'

The parser backend to use for parsing robots.txt files. For more information see RobotsTxtMiddleware.

ROBOTSTXT_USER_AGENT

Default: None

The user agent string to use for matching in the robots.txt file. If None, the User-Agent header you are sending with the request or the USER_AGENT setting (in that order) will be used for determining the user agent to use in the robots.txt file.

SCHEDULER

Default: 'scrapy.core.scheduler.Scheduler'

The scheduler to use for crawling.

SCHEDULER_DEBUG

Default: False

Setting to True will log debug information about the requests scheduler. This currently logs (only once) if the requests cannot be serialized to disk. Stats counter (scheduler/unserializable) tracks the number of times this happens.

Example entry in logs:

1956-01-31 00:00:00+0800 [scrapy.core.scheduler] ERROR: Unable to serialize request: <GET http://example.com> - reason: cannot serialize <Request at 0x9a7c7ec> (type Request)> - no more unserializable requests will be logged (see 'scheduler/unserializable' stats counter)

SCHEDULER_DISK_QUEUE

Default: 'scrapy.squeues.PickleLifoDiskQueue'

Type of disk queue that will be used by scheduler. Other available types are scrapy.squeues.PickleFifoDiskQueue, scrapy.squeues.MarshalFifoDiskQueue, scrapy.squeues.MarshalLifoDiskQueue.

SCHEDULER_MEMORY_QUEUE

Default: 'scrapy.squeues.LifoMemoryQueue'

Type of in-memory queue used by scheduler. Other available type is: scrapy.squeues.FifoMemoryQueue.

SCHEDULER_PRIORITY_QUEUE

Default: 'scrapy.pqueues.ScrapyPriorityQueue'

Type of priority queue used by the scheduler. Another available type is scrapy.pqueues.DownloaderAwarePriorityQueue. scrapy.pqueues.DownloaderAwarePriorityQueue works better than scrapy.pqueues.ScrapyPriorityQueue when you crawl many different domains in parallel. But currently scrapy.pqueues.DownloaderAwarePriorityQueue does not work together with CONCURRENT_REQUESTS_PER_IP.

SPIDER_CONTRACTS

Default:: {}

A dict containing the spider contracts enabled in your project, used for testing spiders. For more info see Spiders Contracts.

SPIDER_CONTRACTS_BASE

Default:

{ 'scrapy.contracts.default.UrlContract' : 1, 'scrapy.contracts.default.ReturnsContract': 2, 'scrapy.contracts.default.ScrapesContract': 3, }

A dict containing the scrapy contracts enabled by default in Scrapy. You should never modify this setting in your project, modify SPIDER_CONTRACTS instead. For more info see Spiders Contracts.

You can disable any of these contracts by assigning None to their class path in SPIDER_CONTRACTS. E.g., to disable the built-in ScrapesContract, place this in your settings.py:

SPIDER_CONTRACTS = { 'scrapy.contracts.default.ScrapesContract': None, }

SPIDER_LOADER_CLASS

Default: 'scrapy.spiderloader.SpiderLoader'

The class that will be used for loading spiders, which must implement the SpiderLoader API.

SPIDER_LOADER_WARN_ONLY

New in version 1.3.3.

Default: False

By default, when scrapy tries to import spider classes from SPIDER_MODULES, it will fail loudly if there is any ImportError exception. But you can choose to silence this exception and turn it into a simple warning by setting SPIDER_LOADER_WARN_ONLY = True.

Note

Some scrapy commands run with this setting to True already (i.e. they will only issue a warning and will not fail) since they do not actually need to load spider classes to work: scrapy runspider, scrapy settings, scrapy startproject, scrapy version.

SPIDER_MIDDLEWARES

Default:: {}

A dict containing the spider middlewares enabled in your project, and their orders. For more info see Activating a spider middleware.

SPIDER_MIDDLEWARES_BASE

Default:

{ 'scrapy.spidermiddlewares.httperror.HttpErrorMiddleware': 50, 'scrapy.spidermiddlewares.offsite.OffsiteMiddleware': 500, 'scrapy.spidermiddlewares.referer.RefererMiddleware': 700, 'scrapy.spidermiddlewares.urllength.UrlLengthMiddleware': 800, 'scrapy.spidermiddlewares.depth.DepthMiddleware': 900, }

A dict containing the spider middlewares enabled by default in Scrapy, and their orders. Low orders are closer to the engine, high orders are closer to the spider. For more info see Activating a spider middleware.

SPIDER_MODULES

Default: []

A list of modules where Scrapy will look for spiders.

Example:

SPIDER_MODULES = ['mybot.spiders_prod', 'mybot.spiders_dev']

STATS_CLASS

Default: 'scrapy.statscollectors.MemoryStatsCollector'

The class to use for collecting stats, who must implement the Stats Collector API.

STATS_DUMP

Default: True

Dump the Scrapy stats (to the Scrapy log) once the spider finishes.

For more info see: Stats Collection.

STATSMAILER_RCPTS

Default: [] (empty list)

Send Scrapy stats after spiders finish scraping. See StatsMailer for more info.

TELNETCONSOLE_ENABLED

Default: True

A boolean which specifies if the telnet console will be enabled (provided its extension is also enabled).

TELNETCONSOLE_PORT

Default: [6023, 6073]

The port range to use for the telnet console. If set to None or 0, a dynamically assigned port is used. For more info see Telnet Console.

TEMPLATES_DIR

Default: templates dir inside scrapy module

The directory where to look for templates when creating new projects with startproject command and new spiders with genspider command.

The project name must not conflict with the name of custom files or directories in the project subdirectory.

URLLENGTH_LIMIT

Default: 2083

Scope: spidermiddlewares.urllength

The maximum URL length to allow for crawled URLs. For more information about the default value for this setting see: https://boutell.com/newfaq/misc/urllength.html

USER_AGENT

Default: "Scrapy/VERSION (+https://scrapy.org)"

The default User-Agent to use when crawling, unless overridden. This user agent is also used by RobotsTxtMiddleware if ROBOTSTXT_USER_AGENT setting is None and there is no overridding User-Agent header specified for the request.

Settings documented elsewhere:

The following settings are documented elsewhere, please check each specific case to see how to enable and use them.

AJAXCRAWL_ENABLED

AUTOTHROTTLE_DEBUG

AUTOTHROTTLE_ENABLED

AUTOTHROTTLE_MAX_DELAY

AUTOTHROTTLE_START_DELAY

AUTOTHROTTLE_TARGET_CONCURRENCY

CLOSESPIDER_ERRORCOUNT

CLOSESPIDER_ITEMCOUNT

CLOSESPIDER_PAGECOUNT

CLOSESPIDER_TIMEOUT

COMMANDS_MODULE

COMPRESSION_ENABLED

COOKIES_DEBUG

COOKIES_ENABLED

FEED_EXPORTERS

FEED_EXPORTERS_BASE

FEED_EXPORT_ENCODING

FEED_EXPORT_FIELDS

FEED_EXPORT_INDENT

FEED_FORMAT

FEED_STORAGES

FEED_STORAGES_BASE

FEED_STORAGE_FTP_ACTIVE

FEED_STORAGE_S3_ACL

FEED_STORE_EMPTY

FEED_URI

FILES_EXPIRES

FILES_RESULT_FIELD

FILES_STORE

FILES_STORE_GCS_ACL

FILES_STORE_S3_ACL

FILES_URLS_FIELD

GCS_PROJECT_ID

HTTPCACHE_ALWAYS_STORE

HTTPCACHE_DBM_MODULE

HTTPCACHE_DIR

HTTPCACHE_ENABLED

HTTPCACHE_EXPIRATION_SECS

HTTPCACHE_GZIP

HTTPCACHE_IGNORE_HTTP_CODES

HTTPCACHE_IGNORE_MISSING

HTTPCACHE_IGNORE_RESPONSE_CACHE_CONTROLS

HTTPCACHE_IGNORE_SCHEMES

HTTPCACHE_POLICY

HTTPCACHE_STORAGE

HTTPERROR_ALLOWED_CODES

HTTPERROR_ALLOW_ALL

HTTPPROXY_AUTH_ENCODING

HTTPPROXY_ENABLED

IMAGES_EXPIRES

IMAGES_MIN_HEIGHT

IMAGES_MIN_WIDTH

IMAGES_RESULT_FIELD

IMAGES_STORE

IMAGES_STORE_GCS_ACL

IMAGES_STORE_S3_ACL

IMAGES_THUMBS

IMAGES_URLS_FIELD

MAIL_FROM

MAIL_HOST

MAIL_PASS

MAIL_PORT

MAIL_SSL

MAIL_TLS

MAIL_USER

MEDIA_ALLOW_REDIRECTS

METAREFRESH_ENABLED

METAREFRESH_IGNORE_TAGS

METAREFRESH_MAXDELAY

REDIRECT_ENABLED

REDIRECT_MAX_TIMES

REFERER_ENABLED

REFERRER_POLICY

RETRY_ENABLED

RETRY_HTTP_CODES

RETRY_TIMES

TELNETCONSOLE_HOST

TELNETCONSOLE_PASSWORD

TELNETCONSOLE_PORT

TELNETCONSOLE_USERNAME

Exceptions

Built-in Exceptions reference

Here’s a list of all exceptions included in Scrapy and their usage.

DropItem

exception scrapy.exceptions.DropItem

The exception that must be raised by item pipeline stages to stop processing an Item. For more information see Item Pipeline.

CloseSpider

exception scrapy.exceptions.CloseSpider(reason='cancelled')

This exception can be raised from a spider callback to request the spider to be closed/stopped. Supported arguments:

Parameters

reason (str [https://docs.python.org/3/library/stdtypes.html#str]) – the reason for closing

For example:

def parse_page(self, response): if 'Bandwidth exceeded' in response.body: raise CloseSpider('bandwidth_exceeded')

DontCloseSpider

exception scrapy.exceptions.DontCloseSpider

This exception can be raised in a spider_idle signal handler to prevent the spider from being closed.

IgnoreRequest

exception scrapy.exceptions.IgnoreRequest

This exception can be raised by the Scheduler or any downloader middleware to indicate that the request should be ignored.

NotConfigured

exception scrapy.exceptions.NotConfigured

This exception can be raised by some components to indicate that they will remain disabled. Those components include:

Extensions

Item pipelines

Downloader middlewares

Spider middlewares

The exception must be raised in the component’s __init__ method.

NotSupported

exception scrapy.exceptions.NotSupported

This exception is raised to indicate an unsupported feature.

Logging

Note
