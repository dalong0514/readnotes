Versioning and API Stability

Understand Scrapy versioning and API stability.

Scrapy at a glance

Scrapy is an application framework for crawling web sites and extracting structured data which can be used for a wide range of useful applications, like data mining, information processing or historical archival.

Even though Scrapy was originally designed for web scraping [https://en.wikipedia.org/wiki/Web_scraping], it can also be used to extract data using APIs (such as Amazon Associates Web Services [https://affiliate-program.amazon.com/gp/advertising/api/detail/main.html]) or as a general purpose web crawler.

Walk-through of an example spider

In order to show you what Scrapy brings to the table, we’ll walk you through an example of a Scrapy Spider using the simplest way to run a spider.

Here’s the code for a spider that scrapes famous quotes from website http://quotes.toscrape.com, following the pagination:

import scrapy class QuotesSpider(scrapy.Spider): name = 'quotes' start_urls = [ 'http://quotes.toscrape.com/tag/humor/', ] def parse(self, response): for quote in response.css('div.quote'): yield { 'text': quote.css('span.text::text').get(), 'author': quote.xpath('span/small/text()').get(), } next_page = response.css('li.next a::attr("href")').get() if next_page is not None: yield response.follow(next_page, self.parse)

Put this in a text file, name it to something like quotes_spider.py and run the spider using the runspider command:

scrapy runspider quotes_spider.py -o quotes.json

When this finishes you will have in the quotes.json file a list of the quotes in JSON format, containing text and author, looking like this (reformatted here for better readability):

[{ "author": "Jane Austen", "text": "\u201cThe person, be it gentleman or lady, who has not pleasure in a good novel, must be intolerably stupid.\u201d" }, { "author": "Groucho Marx", "text": "\u201cOutside of a dog, a book is man's best friend. Inside of a dog it's too dark to read.\u201d" }, { "author": "Steve Martin", "text": "\u201cA day without sunshine is like, you know, night.\u201d" }, ...]

What just happened?

When you ran the command scrapy runspider quotes_spider.py, Scrapy looked for a Spider definition inside it and ran it through its crawler engine.

The crawl started by making requests to the URLs defined in the start_urls attribute (in this case, only the URL for quotes in humor category) and called the default callback method parse, passing the response object as an argument. In the parse callback, we loop through the quote elements using a CSS Selector, yield a Python dict with the extracted quote text and author, look for a link to the next page and schedule another request using the same parse method as callback.

Here you notice one of the main advantages about Scrapy: requests are scheduled and processed asynchronously. This means that Scrapy doesn’t need to wait for a request to be finished and processed, it can send another request or do other things in the meantime. This also means that other requests can keep going even if some request fails or an error happens while handling it.

While this enables you to do very fast crawls (sending multiple concurrent requests at the same time, in a fault-tolerant way) Scrapy also gives you control over the politeness of the crawl through a few settings. You can do things like setting a download delay between each request, limiting amount of concurrent requests per domain or per IP, and even using an auto-throttling extension that tries to figure out these automatically.

Note

This is using feed exports to generate the JSON file, you can easily change the export format (XML or CSV, for example) or the storage backend (FTP or Amazon S3 [https://aws.amazon.com/s3/], for example). You can also write an item pipeline to store the items in a database.

What else?

You’ve seen how to extract and store items from a website using Scrapy, but this is just the surface. Scrapy provides a lot of powerful features for making scraping easy and efficient, such as:

Built-in support for selecting and extracting data from HTML/XML sources using extended CSS selectors and XPath expressions, with helper methods to extract using regular expressions.

An interactive shell console (IPython aware) for trying out the CSS and XPath expressions to scrape data, very useful when writing or debugging your spiders.

Built-in support for generating feed exports in multiple formats (JSON, CSV, XML) and storing them in multiple backends (FTP, S3, local filesystem)

Robust encoding support and auto-detection, for dealing with foreign, non-standard and broken encoding declarations.

Strong extensibility support, allowing you to plug in your own functionality using signals and a well-defined API (middlewares, extensions, and pipelines).

Wide range of built-in extensions and middlewares for handling:

cookies and session handling

HTTP features like compression, authentication, caching

user-agent spoofing

robots.txt

crawl depth restriction

and more

A Telnet console for hooking into a Python console running inside your Scrapy process, to introspect and debug your crawler

Plus other goodies like reusable spiders to crawl sites from Sitemaps [https://www.sitemaps.org/index.html] and XML/CSV feeds, a media pipeline for automatically downloading images (or any other media) associated with the scraped items, a caching DNS resolver, and much more!

What’s next?

The next steps for you are to install Scrapy, follow through the tutorial to learn how to create a full-blown Scrapy project and join the community [https://scrapy.org/community/]. Thanks for your interest!

Installation guide

Installing Scrapy

Scrapy runs on Python 2.7 and Python 3.5 or above under CPython (default Python implementation) and PyPy (starting with PyPy 5.9).

If you’re using Anaconda [https://docs.anaconda.com/anaconda/] or Miniconda [https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html], you can install the package from the conda-forge [https://conda-forge.org/] channel, which has up-to-date packages for Linux, Windows and OS X.

To install Scrapy using conda, run:

conda install -c conda-forge scrapy

Alternatively, if you’re already familiar with installation of Python packages, you can install Scrapy and its dependencies from PyPI with:

pip install Scrapy

Note that sometimes this may require solving compilation issues for some Scrapy dependencies depending on your operating system, so be sure to check the Platform specific installation notes.

We strongly recommend that you install Scrapy in a dedicated virtualenv, to avoid conflicting with your system packages.

For more detailed and platform specifics instructions, as well as troubleshooting information, read on.

Things that are good to know

Scrapy is written in pure Python and depends on a few key Python packages (among others):

lxml [http://lxml.de/], an efficient XML and HTML parser

parsel [https://pypi.python.org/pypi/parsel], an HTML/XML data extraction library written on top of lxml,

w3lib [https://pypi.python.org/pypi/w3lib], a multi-purpose helper for dealing with URLs and web page encodings

twisted [https://twistedmatrix.com/], an asynchronous networking framework

cryptography [https://cryptography.io/] and pyOpenSSL [https://pypi.python.org/pypi/pyOpenSSL], to deal with various network-level security needs

The minimal versions which Scrapy is tested against are:

Twisted 14.0

lxml 3.4

pyOpenSSL 0.14

Scrapy may work with older versions of these packages but it is not guaranteed it will continue working because it’s not being tested against them.

Some of these packages themselves depends on non-Python packages that might require additional installation steps depending on your platform. Please check platform-specific guides below.

In case of any trouble related to these dependencies, please refer to their respective installation instructions:

lxml installation [http://lxml.de/installation.html]

cryptography installation [https://cryptography.io/en/latest/installation/]

Using a virtual environment (recommended)

TL;DR: We recommend installing Scrapy inside a virtual environment on all platforms.

Python packages can be installed either globally (a.k.a system wide), or in user-space. We do not recommend installing scrapy system wide.

Instead, we recommend that you install scrapy within a so-called「virtual environment」(virtualenv [https://virtualenv.pypa.io]). Virtualenvs allow you to not conflict with already-installed Python system packages (which could break some of your system tools and scripts), and still install packages normally with pip (without sudo and the likes).

To get started with virtual environments, see virtualenv installation instructions [https://virtualenv.pypa.io/en/stable/installation/]. To install it globally (having it globally installed actually helps here), it should be a matter of running:

$ [sudo] pip install virtualenv

Check this user guide [https://virtualenv.pypa.io/en/stable/userguide/] on how to create your virtualenv.

Note

If you use Linux or OS X, virtualenvwrapper [https://virtualenvwrapper.readthedocs.io/en/latest/install.html] is a handy tool to create virtualenvs.

Once you have created a virtualenv, you can install scrapy inside it with pip, just like any other Python package. (See platform-specific guides below for non-Python dependencies that you may need to install beforehand).

Python virtualenvs can be created to use Python 2 by default, or Python 3 by default.

If you want to install scrapy with Python 3, install scrapy within a Python 3 virtualenv.

And if you want to install scrapy with Python 2, install scrapy within a Python 2 virtualenv.

Platform specific installation notes

Windows

Though it’s possible to install Scrapy on Windows using pip, we recommend you to install Anaconda [https://docs.anaconda.com/anaconda/] or Miniconda [https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html] and use the package from the conda-forge [https://conda-forge.org/] channel, which will avoid most installation issues.

Once you’ve installed Anaconda [https://docs.anaconda.com/anaconda/] or Miniconda [https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html], install Scrapy with:

conda install -c conda-forge scrapy

Ubuntu 14.04 or above

Scrapy is currently tested with recent-enough versions of lxml, twisted and pyOpenSSL, and is compatible with recent Ubuntu distributions. But it should support older versions of Ubuntu too, like Ubuntu 14.04, albeit with potential issues with TLS connections.

Don’t use the python-scrapy package provided by Ubuntu, they are typically too old and slow to catch up with latest Scrapy.

To install scrapy on Ubuntu (or Ubuntu-based) systems, you need to install these dependencies:

sudo apt-get install python-dev python-pip libxml2-dev libxslt1-dev zlib1g-dev libffi-dev libssl-dev

python-dev, zlib1g-dev, libxml2-dev and libxslt1-dev are required for lxml

libssl-dev and libffi-dev are required for cryptography

If you want to install scrapy on Python 3, you’ll also need Python 3 development headers:

sudo apt-get install python3 python3-dev

Inside a virtualenv, you can install Scrapy with pip after that:

pip install scrapy

Note

The same non-Python dependencies can be used to install Scrapy in Debian Jessie (8.0) and above.

Mac OS X

Building Scrapy’s dependencies requires the presence of a C compiler and development headers. On OS X this is typically provided by Apple’s Xcode development tools. To install the Xcode command line tools open a terminal window and run:

xcode-select --install

There’s a known issue [https://github.com/pypa/pip/issues/2468] that prevents pip from updating system packages. This has to be addressed to successfully install Scrapy and its dependencies. Here are some proposed solutions:

(Recommended) Don’t use system python, install a new, updated version that doesn’t conflict with the rest of your system. Here’s how to do it using the homebrew [https://brew.sh/] package manager:

Install homebrew [https://brew.sh/] following the instructions in https://brew.sh/

Update your PATH variable to state that homebrew packages should be used before system packages (Change .bashrc to .zshrc accordantly if you’re using zsh [https://www.zsh.org/] as default shell):

echo "export PATH=/usr/local/bin:/usr/local/sbin:$PATH" >> ~/.bashrc

Reload .bashrc to ensure the changes have taken place:

source ~/.bashrc

Install python:

brew install python

Latest versions of python have pip bundled with them so you won’t need to install it separately. If this is not the case, upgrade python:

brew update; brew upgrade python

(Optional) Install Scrapy inside an isolated python environment.

This method is a workaround for the above OS X issue, but it’s an overall good practice for managing dependencies and can complement the first method.

virtualenv [https://virtualenv.pypa.io] is a tool you can use to create virtual environments in python. We recommended reading a tutorial like http://docs.python-guide.org/en/latest/dev/virtualenvs/ to get started.

After any of these workarounds you should be able to install Scrapy:

pip install Scrapy

PyPy

We recommend using the latest PyPy version. The version tested is 5.9.0. For PyPy3, only Linux installation was tested.

Most scrapy dependencides now have binary wheels for CPython, but not for PyPy. This means that these dependecies will be built during installation. On OS X, you are likely to face an issue with building Cryptography dependency, solution to this problem is described here [https://github.com/pyca/cryptography/issues/2692#issuecomment-272773481], that is to brew install openssl and then export the flags that this command recommends (only needed when installing scrapy). Installing on Linux has no special issues besides installing build dependencies. Installing scrapy with PyPy on Windows is not tested.

You can check that scrapy is installed correctly by running scrapy bench. If this command gives errors such as TypeError: ... got 2 unexpected keyword arguments, this means that setuptools was unable to pick up one PyPy-specific dependency. To fix this issue, run pip install 'PyPyDispatcher>=2.1.0'.

Troubleshooting

AttributeError: ‘module’ object has no attribute ‘OP_NO_TLSv1_1’

After you install or upgrade Scrapy, Twisted or pyOpenSSL, you may get an exception with the following traceback:

[…] File "[…]/site-packages/twisted/protocols/tls.py", line 63, in <module> from twisted.internet._sslverify import _setAcceptableProtocols File "[…]/site-packages/twisted/internet/_sslverify.py", line 38, in <module> TLSVersion.TLSv1_1: SSL.OP_NO_TLSv1_1, AttributeError: 'module' object has no attribute 'OP_NO_TLSv1_1'

The reason you get this exception is that your system or virtual environment has a version of pyOpenSSL that your version of Twisted does not support.

To install a version of pyOpenSSL that your version of Twisted supports, reinstall Twisted with the tls extra option:

pip install twisted[tls]

For details, see Issue #2473 [https://github.com/scrapy/scrapy/issues/2473].

Scrapy Tutorial

In this tutorial, we’ll assume that Scrapy is already installed on your system. If that’s not the case, see Installation guide.

We are going to scrape quotes.toscrape.com [http://quotes.toscrape.com/], a website that lists quotes from famous authors.

This tutorial will walk you through these tasks:

Creating a new Scrapy project

Writing a spider to crawl a site and extract data

Exporting the scraped data using the command line

Changing spider to recursively follow links

Using spider arguments

Scrapy is written in Python [https://www.python.org/]. If you’re new to the language you might want to start by getting an idea of what the language is like, to get the most out of Scrapy.

If you’re already familiar with other languages, and want to learn Python quickly, the Python Tutorial [https://docs.python.org/3/tutorial] is a good resource.

If you’re new to programming and want to start with Python, the following books may be useful to you:

Automate the Boring Stuff With Python [https://automatetheboringstuff.com/]

How To Think Like a Computer Scientist [http://openbookproject.net/thinkcs/python/english3e/]

Learn Python 3 The Hard Way [https://learnpythonthehardway.org/python3/]

You can also take a look at this list of Python resources for non-programmers [https://wiki.python.org/moin/BeginnersGuide/NonProgrammers], as well as the suggested resources in the learnpython-subreddit [https://www.reddit.com/r/learnpython/wiki/index#wiki_new_to_python.3F].

Creating a project

Before you start scraping, you will have to set up a new Scrapy project. Enter a directory where you’d like to store your code and run:

scrapy startproject tutorial

This will create a tutorial directory with the following contents:

tutorial/ scrapy.cfg # deploy configuration file tutorial/ # project's Python module, you'll import your code from here __init__.py items.py # project items definition file middlewares.py # project middlewares file pipelines.py # project pipelines file settings.py # project settings file spiders/ # a directory where you'll later put your spiders __init__.py

Our first Spider

Spiders are classes that you define and that Scrapy uses to scrape information from a website (or a group of websites). They must subclass Spider and define the initial requests to make, optionally how to follow links in the pages, and how to parse the downloaded page content to extract data.

This is the code for our first Spider. Save it in a file named quotes_spider.py under the tutorial/spiders directory in your project:

import scrapy class QuotesSpider(scrapy.Spider): name = "quotes" def start_requests(self): urls = [ 'http://quotes.toscrape.com/page/1/', 'http://quotes.toscrape.com/page/2/', ] for url in urls: yield scrapy.Request(url=url, callback=self.parse) def parse(self, response): page = response.url.split("/")[-2] filename = 'quotes-%s.html' % page with open(filename, 'wb') as f: f.write(response.body) self.log('Saved file %s' % filename)

As you can see, our Spider subclasses scrapy.Spider and defines some attributes and methods:

name: identifies the Spider. It must be unique within a project, that is, you can’t set the same name for different Spiders.

start_requests(): must return an iterable of Requests (you can return a list of requests or write a generator function) which the Spider will begin to crawl from. Subsequent requests will be generated successively from these initial requests.

parse(): a method that will be called to handle the response downloaded for each of the requests made. The response parameter is an instance of TextResponse that holds the page content and has further helpful methods to handle it.

The parse() method usually parses the response, extracting the scraped data as dicts and also finding new URLs to follow and creating new requests (Request) from them.

How to run our spider

To put our spider to work, go to the project’s top level directory and run:

scrapy crawl quotes

This command runs the spider with name quotes that we’ve just added, that will send some requests for the quotes.toscrape.com domain. You will get an output similar to this:

... (omitted for brevity) 2016-12-16 21:24:05 [scrapy.core.engine] INFO: Spider opened 2016-12-16 21:24:05 [scrapy.extensions.logstats] INFO: Crawled 0 pages (at 0 pages/min), scraped 0 items (at 0 items/min) 2016-12-16 21:24:05 [scrapy.extensions.telnet] DEBUG: Telnet console listening on 127.0.0.1:6023 2016-12-16 21:24:05 [scrapy.core.engine] DEBUG: Crawled (404) <GET http://quotes.toscrape.com/robots.txt> (referer: None) 2016-12-16 21:24:05 [scrapy.core.engine] DEBUG: Crawled (200) <GET http://quotes.toscrape.com/page/1/> (referer: None) 2016-12-16 21:24:05 [scrapy.core.engine] DEBUG: Crawled (200) <GET http://quotes.toscrape.com/page/2/> (referer: None) 2016-12-16 21:24:05 [quotes] DEBUG: Saved file quotes-1.html 2016-12-16 21:24:05 [quotes] DEBUG: Saved file quotes-2.html 2016-12-16 21:24:05 [scrapy.core.engine] INFO: Closing spider (finished) ...

Now, check the files in the current directory. You should notice that two new files have been created: quotes-1.html and quotes-2.html, with the content for the respective URLs, as our parse method instructs.

Note

If you are wondering why we haven’t parsed the HTML yet, hold on, we will cover that soon.

What just happened under the hood?

Scrapy schedules the scrapy.Request objects returned by the start_requests method of the Spider. Upon receiving a response for each one, it instantiates Response objects and calls the callback method associated with the request (in this case, the parse method) passing the response as argument.

A shortcut to the start_requests method

Instead of implementing a start_requests() method that generates scrapy.Request objects from URLs, you can just define a start_urls class attribute with a list of URLs. This list will then be used by the default implementation of start_requests() to create the initial requests for your spider:

import scrapy class QuotesSpider(scrapy.Spider): name = "quotes" start_urls = [ 'http://quotes.toscrape.com/page/1/', 'http://quotes.toscrape.com/page/2/', ] def parse(self, response): page = response.url.split("/")[-2] filename = 'quotes-%s.html' % page with open(filename, 'wb') as f: f.write(response.body)

The parse() method will be called to handle each of the requests for those URLs, even though we haven’t explicitly told Scrapy to do so. This happens because parse() is Scrapy’s default callback method, which is called for requests without an explicitly assigned callback.

Extracting data

The best way to learn how to extract data with Scrapy is trying selectors using the Scrapy shell. Run:

scrapy shell 'http://quotes.toscrape.com/page/1/'

Note

Remember to always enclose urls in quotes when running Scrapy shell from command-line, otherwise urls containing arguments (ie. & character) will not work.

On Windows, use double quotes instead:

scrapy shell "http://quotes.toscrape.com/page/1/"

You will see something like:

[ ... Scrapy log here ... ] 2016-09-19 12:09:27 [scrapy.core.engine] DEBUG: Crawled (200) <GET http://quotes.toscrape.com/page/1/> (referer: None) [s] Available Scrapy objects: [s] scrapy scrapy module (contains scrapy.Request, scrapy.Selector, etc) [s] crawler <scrapy.crawler.Crawler object at 0x7fa91d888c90> [s] item {} [s] request <GET http://quotes.toscrape.com/page/1/> [s] response <200 http://quotes.toscrape.com/page/1/> [s] settings <scrapy.settings.Settings object at 0x7fa91d888c10> [s] spider <DefaultSpider 'default' at 0x7fa91c8af990> [s] Useful shortcuts: [s] shelp() Shell help (print this help) [s] fetch(req_or_url) Fetch request (or URL) and update local objects [s] view(response) View response in a browser >>>

Using the shell, you can try selecting elements using CSS [https://www.w3.org/TR/selectors] with the response object:

>>> response.css('title') [<Selector xpath='descendant-or-self::title' data='<title>Quotes to Scrape</title>'>]

The result of running response.css('title') is a list-like object called SelectorList, which represents a list of Selector objects that wrap around XML/HTML elements and allow you to run further queries to fine-grain the selection or extract the data.

To extract the text from the title above, you can do:

>>> response.css('title::text').getall() ['Quotes to Scrape']

There are two things to note here: one is that we’ve added ::text to the CSS query, to mean we want to select only the text elements directly inside <title> element. If we don’t specify ::text, we’d get the full title element, including its tags:

>>> response.css('title').getall() ['<title>Quotes to Scrape</title>']

The other thing is that the result of calling .getall() is a list: it is possible that a selector returns more than one result, so we extract them all. When you know you just want the first result, as in this case, you can do:

>>> response.css('title::text').get() 'Quotes to Scrape'

As an alternative, you could’ve written:

>>> response.css('title::text')[0].get() 'Quotes to Scrape'

However, using .get() directly on a SelectorList instance avoids an IndexError and returns None when it doesn’t find any element matching the selection.

There’s a lesson here: for most scraping code, you want it to be resilient to errors due to things not being found on a page, so that even if some parts fail to be scraped, you can at least get some data.

Besides the getall() and get() methods, you can also use the re() method to extract using regular expressions [https://docs.python.org/3/library/re.html]:

>>> response.css('title::text').re(r'Quotes.*') ['Quotes to Scrape'] >>> response.css('title::text').re(r'Q\w+') ['Quotes'] >>> response.css('title::text').re(r'(\w+) to (\w+)') ['Quotes', 'Scrape']

In order to find the proper CSS selectors to use, you might find useful opening the response page from the shell in your web browser using view(response). You can use your browser’s developer tools to inspect the HTML and come up with a selector (see Using your browser’s Developer Tools for scraping).

Selector Gadget [http://selectorgadget.com/] is also a nice tool to quickly find CSS selector for visually selected elements, which works in many browsers.

XPath: a brief intro

Besides CSS [https://www.w3.org/TR/selectors], Scrapy selectors also support using XPath [https://www.w3.org/TR/xpath] expressions:

>>> response.xpath('//title') [<Selector xpath='//title' data='<title>Quotes to Scrape</title>'>] >>> response.xpath('//title/text()').get() 'Quotes to Scrape'

XPath expressions are very powerful, and are the foundation of Scrapy Selectors. In fact, CSS selectors are converted to XPath under-the-hood. You can see that if you read closely the text representation of the selector objects in the shell.

While perhaps not as popular as CSS selectors, XPath expressions offer more power because besides navigating the structure, it can also look at the content. Using XPath, you’re able to select things like: select the link that contains the text「Next Page」. This makes XPath very fitting to the task of scraping, and we encourage you to learn XPath even if you already know how to construct CSS selectors, it will make scraping much easier.

We won’t cover much of XPath here, but you can read more about using XPath with Scrapy Selectors here. To learn more about XPath, we recommend this tutorial to learn XPath through examples [http://zvon.org/comp/r/tut-XPath_1.html], and this tutorial to learn「how to think in XPath」[http://plasmasturm.org/log/xpath101/].

Extracting quotes and authors

Now that you know a bit about selection and extraction, let’s complete our spider by writing the code to extract the quotes from the web page.

Each quote in http://quotes.toscrape.com is represented by HTML elements that look like this:

<div class="quote"> <span class="text">「The world as we have created it is a process of our thinking. It cannot be changed without changing our thinking.」</span> <span> by <small class="author">Albert Einstein</small> <a href="/author/Albert-Einstein">(about)</a> </span> <div class="tags"> Tags: <a class="tag" href="/tag/change/page/1/">change</a> <a class="tag" href="/tag/deep-thoughts/page/1/">deep-thoughts</a> <a class="tag" href="/tag/thinking/page/1/">thinking</a> <a class="tag" href="/tag/world/page/1/">world</a> </div> </div>

Let’s open up scrapy shell and play a bit to find out how to extract the data we want:

$ scrapy shell 'http://quotes.toscrape.com'

We get a list of selectors for the quote HTML elements with:

>>> response.css("div.quote")

Each of the selectors returned by the query above allows us to run further queries over their sub-elements. Let’s assign the first selector to a variable, so that we can run our CSS selectors directly on a particular quote:

>>> quote = response.css("div.quote")[0]

Now, let’s extract text, author and the tags from that quote using the quote object we just created:

>>> text = quote.css("span.text::text").get() >>> text '「The world as we have created it is a process of our thinking. It cannot be changed without changing our thinking.」' >>> author = quote.css("small.author::text").get() >>> author 'Albert Einstein'

Given that the tags are a list of strings, we can use the .getall() method to get all of them:

>>> tags = quote.css("div.tags a.tag::text").getall() >>> tags ['change', 'deep-thoughts', 'thinking', 'world']

Having figured out how to extract each bit, we can now iterate over all the quotes elements and put them together into a Python dictionary:

>>> for quote in response.css("div.quote"): ... text = quote.css("span.text::text").get() ... author = quote.css("small.author::text").get() ... tags = quote.css("div.tags a.tag::text").getall() ... print(dict(text=text, author=author, tags=tags)) {'tags': ['change', 'deep-thoughts', 'thinking', 'world'], 'author': 'Albert Einstein', 'text': '「The world as we have created it is a process of our thinking. It cannot be changed without changing our thinking.」'} {'tags': ['abilities', 'choices'], 'author': 'J.K. Rowling', 'text': '「It is our choices, Harry, that show what we truly are, far more than our abilities.」'} ... a few more of these, omitted for brevity >>>

Extracting data in our spider

Let’s get back to our spider. Until now, it doesn’t extract any data in particular, just saves the whole HTML page to a local file. Let’s integrate the extraction logic above into our spider.

A Scrapy spider typically generates many dictionaries containing the data extracted from the page. To do that, we use the yield Python keyword in the callback, as you can see below:

import scrapy class QuotesSpider(scrapy.Spider): name = "quotes" start_urls = [ 'http://quotes.toscrape.com/page/1/', 'http://quotes.toscrape.com/page/2/', ] def parse(self, response): for quote in response.css('div.quote'): yield { 'text': quote.css('span.text::text').get(), 'author': quote.css('small.author::text').get(), 'tags': quote.css('div.tags a.tag::text').getall(), }

If you run this spider, it will output the extracted data with the log:

2016-09-19 18:57:19 [scrapy.core.scraper] DEBUG: Scraped from <200 http://quotes.toscrape.com/page/1/> {'tags': ['life', 'love'], 'author': 'André Gide', 'text': '「It is better to be hated for what you are than to be loved for what you are not.」'} 2016-09-19 18:57:19 [scrapy.core.scraper] DEBUG: Scraped from <200 http://quotes.toscrape.com/page/1/> {'tags': ['edison', 'failure', 'inspirational', 'paraphrased'], 'author': 'Thomas A. Edison', 'text': "「I have not failed. I've just found 10,000 ways that won't work.」"}

Storing the scraped data

The simplest way to store the scraped data is by using Feed exports, with the following command:

scrapy crawl quotes -o quotes.json

That will generate an quotes.json file containing all scraped items, serialized in JSON [https://en.wikipedia.org/wiki/JSON].

For historic reasons, Scrapy appends to a given file instead of overwriting its contents. If you run this command twice without removing the file before the second time, you’ll end up with a broken JSON file.

You can also use other formats, like JSON Lines [http://jsonlines.org]:

scrapy crawl quotes -o quotes.jl

The JSON Lines [http://jsonlines.org] format is useful because it’s stream-like, you can easily append new records to it. It doesn’t have the same problem of JSON when you run twice. Also, as each record is a separate line, you can process big files without having to fit everything in memory, there are tools like JQ [https://stedolan.github.io/jq] to help doing that at the command-line.

In small projects (like the one in this tutorial), that should be enough. However, if you want to perform more complex things with the scraped items, you can write an Item Pipeline. A placeholder file for Item Pipelines has been set up for you when the project is created, in tutorial/pipelines.py. Though you don’t need to implement any item pipelines if you just want to store the scraped items.

Following links

Let’s say, instead of just scraping the stuff from the first two pages from http://quotes.toscrape.com, you want quotes from all the pages in the website.

Now that you know how to extract data from pages, let’s see how to follow links from them.

First thing is to extract the link to the page we want to follow. Examining our page, we can see there is a link to the next page with the following markup:

<ul class="pager"> <li class="next"> <a href="/page/2/">Next <span aria-hidden="true">&rarr;</span></a> </li> </ul>

We can try extracting it in the shell:

>>> response.css('li.next a').get() '<a href="/page/2/">Next <span aria-hidden="true">→</span></a>'

This gets the anchor element, but we want the attribute href. For that, Scrapy supports a CSS extension that lets you select the attribute contents, like this:

>>> response.css('li.next a::attr(href)').get() '/page/2/'

There is also an attrib property available (see Selecting element attributes for more):

>>> response.css('li.next a').attrib['href'] '/page/2'

Let’s see now our spider modified to recursively follow the link to the next page, extracting data from it:

import scrapy class QuotesSpider(scrapy.Spider): name = "quotes" start_urls = [ 'http://quotes.toscrape.com/page/1/', ] def parse(self, response): for quote in response.css('div.quote'): yield { 'text': quote.css('span.text::text').get(), 'author': quote.css('small.author::text').get(), 'tags': quote.css('div.tags a.tag::text').getall(), } next_page = response.css('li.next a::attr(href)').get() if next_page is not None: next_page = response.urljoin(next_page) yield scrapy.Request(next_page, callback=self.parse)

Now, after extracting the data, the parse() method looks for the link to the next page, builds a full absolute URL using the urljoin() method (since the links can be relative) and yields a new request to the next page, registering itself as callback to handle the data extraction for the next page and to keep the crawling going through all the pages.

What you see here is Scrapy’s mechanism of following links: when you yield a Request in a callback method, Scrapy will schedule that request to be sent and register a callback method to be executed when that request finishes.

Using this, you can build complex crawlers that follow links according to rules you define, and extract different kinds of data depending on the page it’s visiting.

In our example, it creates a sort of loop, following all the links to the next page until it doesn’t find one – handy for crawling blogs, forums and other sites with pagination.

A shortcut for creating Requests

As a shortcut for creating Request objects you can use response.follow:

import scrapy class QuotesSpider(scrapy.Spider): name = "quotes" start_urls = [ 'http://quotes.toscrape.com/page/1/', ] def parse(self, response): for quote in response.css('div.quote'): yield { 'text': quote.css('span.text::text').get(), 'author': quote.css('span small::text').get(), 'tags': quote.css('div.tags a.tag::text').getall(), } next_page = response.css('li.next a::attr(href)').get() if next_page is not None: yield response.follow(next_page, callback=self.parse)

Unlike scrapy.Request, response.follow supports relative URLs directly - no need to call urljoin. Note that response.follow just returns a Request instance; you still have to yield this Request.

You can also pass a selector to response.follow instead of a string; this selector should extract necessary attributes:

for href in response.css('li.next a::attr(href)'): yield response.follow(href, callback=self.parse)

For <a> elements there is a shortcut: response.follow uses their href attribute automatically. So the code can be shortened further:

for a in response.css('li.next a'): yield response.follow(a, callback=self.parse)

Note

response.follow(response.css('li.next a')) is not valid because response.css returns a list-like object with selectors for all results, not a single selector. A for loop like in the example above, or response.follow(response.css('li.next a')[0]) is fine.

More examples and patterns

Here is another spider that illustrates callbacks and following links, this time for scraping author information:

import scrapy class AuthorSpider(scrapy.Spider): name = 'author' start_urls = ['http://quotes.toscrape.com/'] def parse(self, response): # follow links to author pages for href in response.css('.author + a::attr(href)'): yield response.follow(href, self.parse_author) # follow pagination links for href in response.css('li.next a::attr(href)'): yield response.follow(href, self.parse) def parse_author(self, response): def extract_with_css(query): return response.css(query).get(default='').strip() yield { 'name': extract_with_css('h3.author-title::text'), 'birthdate': extract_with_css('.author-born-date::text'), 'bio': extract_with_css('.author-description::text'), }

This spider will start from the main page, it will follow all the links to the authors pages calling the parse_author callback for each of them, and also the pagination links with the parse callback as we saw before.

Here we’re passing callbacks to response.follow as positional arguments to make the code shorter; it also works for scrapy.Request.

The parse_author callback defines a helper function to extract and cleanup the data from a CSS query and yields the Python dict with the author data.

Another interesting thing this spider demonstrates is that, even if there are many quotes from the same author, we don’t need to worry about visiting the same author page multiple times. By default, Scrapy filters out duplicated requests to URLs already visited, avoiding the problem of hitting servers too much because of a programming mistake. This can be configured by the setting DUPEFILTER_CLASS.

Hopefully by now you have a good understanding of how to use the mechanism of following links and callbacks with Scrapy.

As yet another example spider that leverages the mechanism of following links, check out the CrawlSpider class for a generic spider that implements a small rules engine that you can use to write your crawlers on top of it.

Also, a common pattern is to build an item with data from more than one page, using a trick to pass additional data to the callbacks.

Using spider arguments

You can provide command line arguments to your spiders by using the -a option when running them:

scrapy crawl quotes -o quotes-humor.json -a tag=humor

These arguments are passed to the Spider’s __init__ method and become spider attributes by default.

In this example, the value provided for the tag argument will be available via self.tag. You can use this to make your spider fetch only quotes with a specific tag, building the URL based on the argument:

import scrapy class QuotesSpider(scrapy.Spider): name = "quotes" def start_requests(self): url = 'http://quotes.toscrape.com/' tag = getattr(self, 'tag', None) if tag is not None: url = url + 'tag/' + tag yield scrapy.Request(url, self.parse) def parse(self, response): for quote in response.css('div.quote'): yield { 'text': quote.css('span.text::text').get(), 'author': quote.css('small.author::text').get(), } next_page = response.css('li.next a::attr(href)').get() if next_page is not None: yield response.follow(next_page, self.parse)

If you pass the tag=humor argument to this spider, you’ll notice that it will only visit URLs from the humor tag, such as http://quotes.toscrape.com/tag/humor.

You can learn more about handling spider arguments here.

Next steps

This tutorial covered only the basics of Scrapy, but there’s a lot of other features not mentioned here. Check the What else? section in Scrapy at a glance chapter for a quick overview of the most important ones.

You can continue from the section Basic concepts to know more about the command-line tool, spiders, selectors and other things the tutorial hasn’t covered like modeling the scraped data. If you prefer to play with an example project, check the Examples section.

Examples

The best way to learn is with examples, and Scrapy is no exception. For this reason, there is an example Scrapy project named quotesbot [https://github.com/scrapy/quotesbot], that you can use to play and learn more about Scrapy. It contains two spiders for http://quotes.toscrape.com, one using CSS selectors and another one using XPath expressions.

The quotesbot [https://github.com/scrapy/quotesbot] project is available at: https://github.com/scrapy/quotesbot. You can find more information about it in the project’s README.

If you’re familiar with git, you can checkout the code. Otherwise you can download the project as a zip file by clicking here [https://github.com/scrapy/quotesbot/archive/master.zip].

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

scrapy.log has been deprecated alongside its functions in favor of explicit calls to the Python standard logging. Keep reading to learn more about the new logging system.

Scrapy uses Python’s builtin logging system [https://docs.python.org/3/library/logging.html] for event logging. We’ll provide some simple examples to get you started, but for more advanced use-cases it’s strongly suggested to read thoroughly its documentation.

Logging works out of the box, and can be configured to some extent with the Scrapy settings listed in Logging settings.

Scrapy calls scrapy.utils.log.configure_logging() to set some reasonable defaults and handle those settings in Logging settings when running commands, so it’s recommended to manually call it if you’re running Scrapy from scripts as described in Run Scrapy from a script.

Log levels

Python’s builtin logging defines 5 different levels to indicate the severity of a given log message. Here are the standard ones, listed in decreasing order:

logging.CRITICAL - for critical errors (highest severity)

logging.ERROR - for regular errors

logging.WARNING - for warning messages

logging.INFO - for informational messages

logging.DEBUG - for debugging messages (lowest severity)

How to log messages

Here’s a quick example of how to log a message using the logging.WARNING level:

import logging logging.warning("This is a warning")

There are shortcuts for issuing log messages on any of the standard 5 levels, and there’s also a general logging.log method which takes a given level as argument. If needed, the last example could be rewritten as:

import logging logging.log(logging.WARNING, "This is a warning")

On top of that, you can create different「loggers」to encapsulate messages. (For example, a common practice is to create different loggers for every module). These loggers can be configured independently, and they allow hierarchical constructions.

The previous examples use the root logger behind the scenes, which is a top level logger where all messages are propagated to (unless otherwise specified). Using logging helpers is merely a shortcut for getting the root logger explicitly, so this is also an equivalent of the last snippets:

import logging logger = logging.getLogger() logger.warning("This is a warning")

You can use a different logger just by getting its name with the logging.getLogger function:

import logging logger = logging.getLogger('mycustomlogger') logger.warning("This is a warning")

Finally, you can ensure having a custom logger for any module you’re working on by using the __name__ variable, which is populated with current module’s path:

import logging logger = logging.getLogger(__name__) logger.warning("This is a warning")

See also

Module logging, HowTo [https://docs.python.org/2/howto/logging.html]

Basic Logging Tutorial

Module logging, Loggers [https://docs.python.org/2/library/logging.html#logger-objects]

Further documentation on loggers

Logging from Spiders

Scrapy provides a logger within each Spider instance, which can be accessed and used like this:

import scrapy class MySpider(scrapy.Spider): name = 'myspider' start_urls = ['https://scrapinghub.com'] def parse(self, response): self.logger.info('Parse function called on %s', response.url)

That logger is created using the Spider’s name, but you can use any custom Python logger you want. For example:

import logging import scrapy logger = logging.getLogger('mycustomlogger') class MySpider(scrapy.Spider): name = 'myspider' start_urls = ['https://scrapinghub.com'] def parse(self, response): logger.info('Parse function called on %s', response.url)

Logging configuration

Loggers on their own don’t manage how messages sent through them are displayed. For this task, different「handlers」can be attached to any logger instance and they will redirect those messages to appropriate destinations, such as the standard output, files, emails, etc.

By default, Scrapy sets and configures a handler for the root logger, based on the settings below.

Logging settings

These settings can be used to configure the logging:

LOG_FILE

LOG_ENABLED

LOG_ENCODING

LOG_LEVEL

LOG_FORMAT

LOG_DATEFORMAT

LOG_STDOUT

LOG_SHORT_NAMES

The first couple of settings define a destination for log messages. If LOG_FILE is set, messages sent through the root logger will be redirected to a file named LOG_FILE with encoding LOG_ENCODING. If unset and LOG_ENABLED is True, log messages will be displayed on the standard error. Lastly, if LOG_ENABLED is False, there won’t be any visible log output.

LOG_LEVEL determines the minimum level of severity to display, those messages with lower severity will be filtered out. It ranges through the possible levels listed in Log levels.

LOG_FORMAT and LOG_DATEFORMAT specify formatting strings used as layouts for all messages. Those strings can contain any placeholders listed in logging’s logrecord attributes docs [https://docs.python.org/2/library/logging.html#logrecord-attributes] and datetime’s strftime and strptime directives [https://docs.python.org/2/library/datetime.html#strftime-and-strptime-behavior] respectively.

If LOG_SHORT_NAMES is set, then the logs will not display the scrapy component that prints the log. It is unset by default, hence logs contain the scrapy component responsible for that log output.

Command-line options

There are command-line arguments, available for all commands, that you can use to override some of the Scrapy settings regarding logging.

--logfile FILE

Overrides LOG_FILE

--loglevel/-L LEVEL

Overrides LOG_LEVEL

--nolog

Sets LOG_ENABLED to False

See also

Module logging.handlers [https://docs.python.org/2/library/logging.handlers.html]

Further documentation on available handlers

Custom Log Formats

A custom log format can be set for different actions by extending LogFormatter class and making LOG_FORMATTER point to your new class.

class scrapy.logformatter.LogFormatter

Class for generating log messages for different actions.

All methods must return a dictionary listing the parameters level, msg and args which are going to be used for constructing the log message when calling logging.log.

Dictionary keys for the method outputs:

level is the log level for that action, you can use those from the python logging library [https://docs.python.org/3/library/logging.html] : logging.DEBUG, logging.INFO, logging.WARNING, logging.ERROR and logging.CRITICAL.

msg should be a string that can contain different formatting placeholders. This string, formatted with the provided args, is going to be the long message for that action.

args should be a tuple or dict with the formatting placeholders for msg. The final log message is computed as msg % args.

Users can define their own LogFormatter class if they want to customize how each action is logged or if they want to omit it entirely. In order to omit logging an action the method must return None.

Here is an example on how to create a custom log formatter to lower the severity level of the log message when an item is dropped from the pipeline:

class PoliteLogFormatter(logformatter.LogFormatter): def dropped(self, item, exception, response, spider): return { 'level': logging.INFO, # lowering the level from logging.WARNING 'msg': u"Dropped: %(exception)s" + os.linesep + "%(item)s", 'args': { 'exception': exception, 'item': item, } }

crawled(request, response, spider)

Logs a message when the crawler finds a webpage.

dropped(item, exception, response, spider)

Logs a message when an item is dropped while it is passing through the item pipeline.

scraped(item, response, spider)

Logs a message when an item is scraped by a spider.

Advanced customization

Because Scrapy uses stdlib logging module, you can customize logging using all features of stdlib logging.

For example, let’s say you’re scraping a website which returns many HTTP 404 and 500 responses, and you want to hide all messages like this:

2016-12-16 22:00:06 [scrapy.spidermiddlewares.httperror] INFO: Ignoring response <500 http://quotes.toscrape.com/page/1-34/>: HTTP status code is not handled or not allowed

The first thing to note is a logger name - it is in brackets: [scrapy.spidermiddlewares.httperror]. If you get just [scrapy] then LOG_SHORT_NAMES is likely set to True; set it to False and re-run the crawl.

Next, we can see that the message has INFO level. To hide it we should set logging level for scrapy.spidermiddlewares.httperror higher than INFO; next level after INFO is WARNING. It could be done e.g. in the spider’s __init__ method:

import logging import scrapy class MySpider(scrapy.Spider): # ... def __init__(self, *args, **kwargs): logger = logging.getLogger('scrapy.spidermiddlewares.httperror') logger.setLevel(logging.WARNING) super().__init__(*args, **kwargs)

If you run this spider again then INFO messages from scrapy.spidermiddlewares.httperror logger will be gone.

scrapy.utils.log module

scrapy.utils.log.configure_logging(settings=None, install_root_handler=True)

Initialize logging defaults for Scrapy.

Parameters

settings (dict, Settings object or None) – settings used to create and configure a handler for the root logger (default: None).

install_root_handler (bool [https://docs.python.org/3/library/functions.html#bool]) – whether to install root logging handler (default: True)

This function does:

Route warnings and twisted logging through Python standard logging

Assign DEBUG and ERROR level to Scrapy and Twisted loggers respectively

Route stdout to log if LOG_STDOUT setting is True

When install_root_handler is True (default), this function also creates a handler for the root logger according to given settings (see Logging settings). You can override default options using settings argument. When settings is empty or None, defaults are used.

configure_logging is automatically called when using Scrapy commands or CrawlerProcess, but needs to be called explicitly when running custom scripts using CrawlerRunner. In that case, its usage is not required but it’s recommended.

If you plan on configuring the handlers yourself is still recommended you call this function, passing install_root_handler=False. Bear in mind there won’t be any log output set by default in that case.

To get you started on manually configuring logging’s output, you can use logging.basicConfig() [https://docs.python.org/2/library/logging.html#logging.basicConfig] to set a basic root handler. This is an example on how to redirect INFO or higher messages to a file:

import logging from scrapy.utils.log import configure_logging configure_logging(install_root_handler=False) logging.basicConfig( filename='log.txt', format='%(levelname)s: %(message)s', level=logging.INFO )

Refer to Run Scrapy from a script for more details about using Scrapy this way.

Stats Collection

Scrapy provides a convenient facility for collecting stats in the form of key/values, where values are often counters. The facility is called the Stats Collector, and can be accessed through the stats attribute of the Crawler API, as illustrated by the examples in the Common Stats Collector uses section below.

However, the Stats Collector is always available, so you can always import it in your module and use its API (to increment or set new stat keys), regardless of whether the stats collection is enabled or not. If it’s disabled, the API will still work but it won’t collect anything. This is aimed at simplifying the stats collector usage: you should spend no more than one line of code for collecting stats in your spider, Scrapy extension, or whatever code you’re using the Stats Collector from.

Another feature of the Stats Collector is that it’s very efficient (when enabled) and extremely efficient (almost unnoticeable) when disabled.

The Stats Collector keeps a stats table per open spider which is automatically opened when the spider is opened, and closed when the spider is closed.

Common Stats Collector uses

Access the stats collector through the stats attribute. Here is an example of an extension that access stats:

class ExtensionThatAccessStats(object): def __init__(self, stats): self.stats = stats @classmethod def from_crawler(cls, crawler): return cls(crawler.stats)

Set stat value:

stats.set_value('hostname', socket.gethostname())

Increment stat value:

stats.inc_value('custom_count')

Set stat value only if greater than previous:

stats.max_value('max_items_scraped', value)

Set stat value only if lower than previous:

stats.min_value('min_free_memory_percent', value)

Get stat value:

>>> stats.get_value('custom_count') 1

Get all stats:

>>> stats.get_stats() {'custom_count': 1, 'start_time': datetime.datetime(2009, 7, 14, 21, 47, 28, 977139)}

Available Stats Collectors

Besides the basic StatsCollector there are other Stats Collectors available in Scrapy which extend the basic Stats Collector. You can select which Stats Collector to use through the STATS_CLASS setting. The default Stats Collector used is the MemoryStatsCollector.

MemoryStatsCollector

class scrapy.statscollectors.MemoryStatsCollector

A simple stats collector that keeps the stats of the last scraping run (for each spider) in memory, after they’re closed. The stats can be accessed through the spider_stats attribute, which is a dict keyed by spider domain name.

This is the default Stats Collector used in Scrapy.

spider_stats

A dict of dicts (keyed by spider name) containing the stats of the last scraping run for each spider.

DummyStatsCollector

class scrapy.statscollectors.DummyStatsCollector

A Stats collector which does nothing but is very efficient (because it does nothing). This stats collector can be set via the STATS_CLASS setting, to disable stats collect in order to improve performance. However, the performance penalty of stats collection is usually marginal compared to other Scrapy workload like parsing pages.

Sending e-mail

Although Python makes sending e-mails relatively easy via the smtplib [https://docs.python.org/2/library/smtplib.html] library, Scrapy provides its own facility for sending e-mails which is very easy to use and it’s implemented using Twisted non-blocking IO [https://twistedmatrix.com/documents/current/core/howto/defer-intro.html], to avoid interfering with the non-blocking IO of the crawler. It also provides a simple API for sending attachments and it’s very easy to configure, with a few settings.

Quick example

There are two ways to instantiate the mail sender. You can instantiate it using the standard constructor:

from scrapy.mail import MailSender mailer = MailSender()

Or you can instantiate it passing a Scrapy settings object, which will respect the settings:

mailer = MailSender.from_settings(settings)

And here is how to use it to send an e-mail (without attachments):

mailer.send(to=["someone@example.com"], subject="Some subject", body="Some body", cc=["another@example.com"])

MailSender class reference

MailSender is the preferred class to use for sending emails from Scrapy, as it uses Twisted non-blocking IO [https://twistedmatrix.com/documents/current/core/howto/defer-intro.html], like the rest of the framework.

class scrapy.mail.MailSender(smtphost=None, mailfrom=None, smtpuser=None, smtppass=None, smtpport=None)

Parameters

smtphost (str [https://docs.python.org/3/library/stdtypes.html#str] or bytes [https://docs.python.org/3/library/stdtypes.html#bytes]) – the SMTP host to use for sending the emails. If omitted, the MAIL_HOST setting will be used.

mailfrom (str [https://docs.python.org/3/library/stdtypes.html#str]) – the address used to send emails (in the From: header). If omitted, the MAIL_FROM setting will be used.

smtpuser – the SMTP user. If omitted, the MAIL_USER setting will be used. If not given, no SMTP authentication will be performed.

smtppass (str [https://docs.python.org/3/library/stdtypes.html#str] or bytes [https://docs.python.org/3/library/stdtypes.html#bytes]) – the SMTP pass for authentication.

smtpport (int [https://docs.python.org/3/library/functions.html#int]) – the SMTP port to connect to

smtptls (boolean) – enforce using SMTP STARTTLS

smtpssl (boolean) – enforce using a secure SSL connection

classmethod from_settings(settings)

Instantiate using a Scrapy settings object, which will respect these Scrapy settings.

Parameters

settings (scrapy.settings.Settings object) – the e-mail recipients

send(to, subject, body, cc=None, attachs=(), mimetype='text/plain', charset=None)

Send email to the given recipients.

Parameters

to (str [https://docs.python.org/3/library/stdtypes.html#str] or list of str) – the e-mail recipients

subject (str [https://docs.python.org/3/library/stdtypes.html#str]) – the subject of the e-mail

cc (str [https://docs.python.org/3/library/stdtypes.html#str] or list of str) – the e-mails to CC

body (str [https://docs.python.org/3/library/stdtypes.html#str]) – the e-mail body

attachs (iterable) – an iterable of tuples (attach_name, mimetype, file_object) where attach_name is a string with the name that will appear on the e-mail’s attachment, mimetype is the mimetype of the attachment and file_object is a readable file object with the contents of the attachment

mimetype (str [https://docs.python.org/3/library/stdtypes.html#str]) – the MIME type of the e-mail

charset (str [https://docs.python.org/3/library/stdtypes.html#str]) – the character encoding to use for the e-mail contents

Mail settings

These settings define the default constructor values of the MailSender class, and can be used to configure e-mail notifications in your project without writing any code (for those extensions and code that uses MailSender).

MAIL_FROM

Default: 'scrapy@localhost'

Sender email to use (From: header) for sending emails.

MAIL_HOST

Default: 'localhost'

SMTP host to use for sending emails.

MAIL_PORT

Default: 25

SMTP port to use for sending emails.

MAIL_USER

Default: None

User to use for SMTP authentication. If disabled no SMTP authentication will be performed.

MAIL_PASS

Default: None

Password to use for SMTP authentication, along with MAIL_USER.

MAIL_TLS

Default: False

Enforce using STARTTLS. STARTTLS is a way to take an existing insecure connection, and upgrade it to a secure connection using SSL/TLS.

MAIL_SSL

Default: False

Enforce connecting using an SSL encrypted connection

Telnet Console

Scrapy comes with a built-in telnet console for inspecting and controlling a Scrapy running process. The telnet console is just a regular python shell running inside the Scrapy process, so you can do literally anything from it.

The telnet console is a built-in Scrapy extension which comes enabled by default, but you can also disable it if you want. For more information about the extension itself see Telnet console extension.

Warning

It is not secure to use telnet console via public networks, as telnet doesn’t provide any transport-layer security. Having username/password authentication doesn’t change that.

Intended usage is connecting to a running Scrapy spider locally (spider process and telnet client are on the same machine) or over a secure connection (VPN, SSH tunnel). Please avoid using telnet console over insecure connections, or disable it completely using TELNETCONSOLE_ENABLED option.

How to access the telnet console

The telnet console listens in the TCP port defined in the TELNETCONSOLE_PORT setting, which defaults to 6023. To access the console you need to type:

telnet localhost 6023 Trying localhost... Connected to localhost. Escape character is '^]'. Username: Password: >>>

By default Username is scrapy and Password is autogenerated. The autogenerated Password can be seen on scrapy logs like the example below:

2018-10-16 14:35:21 [scrapy.extensions.telnet] INFO: Telnet Password: 16f92501e8a59326

Default Username and Password can be overriden by the settings TELNETCONSOLE_USERNAME and TELNETCONSOLE_PASSWORD.

Warning

Username and password provide only a limited protection, as telnet is not using secure transport - by default traffic is not encrypted even if username and password are set.

You need the telnet program which comes installed by default in Windows, and most Linux distros.

Available variables in the telnet console

The telnet console is like a regular Python shell running inside the Scrapy process, so you can do anything from it including importing new modules, etc.

However, the telnet console comes with some default variables defined for convenience:

Shortcut

Description

crawler

the Scrapy Crawler (scrapy.crawler.Crawler object)

engine

Crawler.engine attribute

spider

the active spider

slot

the engine slot

extensions

the Extension Manager (Crawler.extensions attribute)

stats

the Stats Collector (Crawler.stats attribute)

settings

the Scrapy settings object (Crawler.settings attribute)

est

print a report of the engine status

prefs

for memory debugging (see Debugging memory leaks)

p

a shortcut to the pprint.pprint function

hpy

for memory debugging (see Debugging memory leaks)

Telnet console usage examples

Here are some example tasks you can do with the telnet console:

View engine status

You can use the est() method of the Scrapy engine to quickly show its state using the telnet console:

telnet localhost 6023 >>> est() Execution engine status time()-engine.start_time : 8.62972998619 engine.has_capacity() : False len(engine.downloader.active) : 16 engine.scraper.is_idle() : False engine.spider.name : followall engine.spider_is_idle(engine.spider) : False engine.slot.closing : False len(engine.slot.inprogress) : 16 len(engine.slot.scheduler.dqs or []) : 0 len(engine.slot.scheduler.mqs) : 92 len(engine.scraper.slot.queue) : 0 len(engine.scraper.slot.active) : 0 engine.scraper.slot.active_size : 0 engine.scraper.slot.itemproc_size : 0 engine.scraper.slot.needs_backout() : False

Pause, resume and stop the Scrapy engine

To pause:

telnet localhost 6023 >>> engine.pause() >>>

To resume:

telnet localhost 6023 >>> engine.unpause() >>>

To stop:

telnet localhost 6023 >>> engine.stop() Connection closed by foreign host.

Telnet Console signals

scrapy.extensions.telnet.update_telnet_vars(telnet_vars)

Sent just before the telnet console is opened. You can hook up to this signal to add, remove or update the variables that will be available in the telnet local namespace. In order to do that, you need to update the telnet_vars dict in your handler.

Parameters

telnet_vars (dict [https://docs.python.org/3/library/stdtypes.html#dict]) – the dict of telnet variables

Telnet settings

These are the settings that control the telnet console’s behaviour:

TELNETCONSOLE_PORT

Default: [6023, 6073]

The port range to use for the telnet console. If set to None or 0, a dynamically assigned port is used.

TELNETCONSOLE_HOST

Default: '127.0.0.1'

The interface the telnet console should listen on

TELNETCONSOLE_USERNAME

Default: 'scrapy'

The username used for the telnet console

TELNETCONSOLE_PASSWORD

Default: None

The password used for the telnet console, default behaviour is to have it autogenerated

Web Service

webservice has been moved into a separate project.

It is hosted at:

https://github.com/scrapy-plugins/scrapy-jsonrpc

Frequently Asked Questions

How does Scrapy compare to BeautifulSoup or lxml?

BeautifulSoup [https://www.crummy.com/software/BeautifulSoup/] and lxml [http://lxml.de/] are libraries for parsing HTML and XML. Scrapy is an application framework for writing web spiders that crawl web sites and extract data from them.

Scrapy provides a built-in mechanism for extracting data (called selectors) but you can easily use BeautifulSoup [https://www.crummy.com/software/BeautifulSoup/] (or lxml [http://lxml.de/]) instead, if you feel more comfortable working with them. After all, they’re just parsing libraries which can be imported and used from any Python code.

In other words, comparing BeautifulSoup [https://www.crummy.com/software/BeautifulSoup/] (or lxml [http://lxml.de/]) to Scrapy is like comparing jinja2 [http://jinja.pocoo.org/] to Django [https://www.djangoproject.com/].

Can I use Scrapy with BeautifulSoup?

Yes, you can. As mentioned above, BeautifulSoup [https://www.crummy.com/software/BeautifulSoup/] can be used for parsing HTML responses in Scrapy callbacks. You just have to feed the response’s body into a BeautifulSoup object and extract whatever data you need from it.

Here’s an example spider using BeautifulSoup API, with lxml as the HTML parser:

from bs4 import BeautifulSoup import scrapy class ExampleSpider(scrapy.Spider): name = "example" allowed_domains = ["example.com"] start_urls = ( 'http://www.example.com/', ) def parse(self, response): # use lxml to get decent HTML parsing speed soup = BeautifulSoup(response.text, 'lxml') yield { "url": response.url, "title": soup.h1.string }

Note

BeautifulSoup supports several HTML/XML parsers. See BeautifulSoup’s official documentation [https://www.crummy.com/software/BeautifulSoup/bs4/doc/#specifying-the-parser-to-use] on which ones are available.

What Python versions does Scrapy support?

Scrapy is supported under Python 2.7 and Python 3.5+ under CPython (default Python implementation) and PyPy (starting with PyPy 5.9). Python 2.6 support was dropped starting at Scrapy 0.20. Python 3 support was added in Scrapy 1.1. PyPy support was added in Scrapy 1.4, PyPy3 support was added in Scrapy 1.5.

Note

For Python 3 support on Windows, it is recommended to use Anaconda/Miniconda as outlined in the installation guide.

Did Scrapy「steal」X from Django?

Probably, but we don’t like that word. We think Django [https://www.djangoproject.com/] is a great open source project and an example to follow, so we’ve used it as an inspiration for Scrapy.

We believe that, if something is already done well, there’s no need to reinvent it. This concept, besides being one of the foundations for open source and free software, not only applies to software but also to documentation, procedures, policies, etc. So, instead of going through each problem ourselves, we choose to copy ideas from those projects that have already solved them properly, and focus on the real problems we need to solve.

We’d be proud if Scrapy serves as an inspiration for other projects. Feel free to steal from us!

Does Scrapy work with HTTP proxies?

Yes. Support for HTTP proxies is provided (since Scrapy 0.8) through the HTTP Proxy downloader middleware. See HttpProxyMiddleware.

How can I scrape an item with attributes in different pages?

See Passing additional data to callback functions.

Scrapy crashes with: ImportError: No module named win32api

You need to install pywin32 [https://sourceforge.net/projects/pywin32/] because of this Twisted bug [https://twistedmatrix.com/trac/ticket/3707].

How can I simulate a user login in my spider?

See Using FormRequest.from_response() to simulate a user login.

Does Scrapy crawl in breadth-first or depth-first order?

By default, Scrapy uses a LIFO [https://en.wikipedia.org/wiki/Stack_(abstract_data_type)] queue for storing pending requests, which basically means that it crawls in DFO order [https://en.wikipedia.org/wiki/Depth-first_search]. This order is more convenient in most cases.

If you do want to crawl in true BFO order [https://en.wikipedia.org/wiki/Breadth-first_search], you can do it by setting the following settings:

DEPTH_PRIORITY = 1 SCHEDULER_DISK_QUEUE = 'scrapy.squeues.PickleFifoDiskQueue' SCHEDULER_MEMORY_QUEUE = 'scrapy.squeues.FifoMemoryQueue'

While pending requests are below the configured values of CONCURRENT_REQUESTS, CONCURRENT_REQUESTS_PER_DOMAIN or CONCURRENT_REQUESTS_PER_DOMAIN, those requests are sent concurrently. As a result, the first few requests of a crawl rarely follow the desired order. Lowering those settings to 1 enforces the desired order, but it significantly slows down the crawl as a whole.

My Scrapy crawler has memory leaks. What can I do?

See Debugging memory leaks.

Also, Python has a builtin memory leak issue which is described in Leaks without leaks.

How can I make Scrapy consume less memory?

See previous question.

Can I use Basic HTTP Authentication in my spiders?

Yes, see HttpAuthMiddleware.

Why does Scrapy download pages in English instead of my native language?

Try changing the default Accept-Language [https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.4] request header by overriding the DEFAULT_REQUEST_HEADERS setting.

Where can I find some example Scrapy projects?

See Examples.

Can I run a spider without creating a project?

Yes. You can use the runspider command. For example, if you have a spider written in a my_spider.py file you can run it with:

scrapy runspider my_spider.py

See runspider command for more info.

I get「Filtered offsite request」messages. How can I fix them?

Those messages (logged with DEBUG level) don’t necessarily mean there is a problem, so you may not need to fix them.

Those messages are thrown by the Offsite Spider Middleware, which is a spider middleware (enabled by default) whose purpose is to filter out requests to domains outside the ones covered by the spider.

For more info see: OffsiteMiddleware.

What is the recommended way to deploy a Scrapy crawler in production?

See Deploying Spiders.

Can I use JSON for large exports?

It’ll depend on how large your output is. See this warning in JsonItemExporter documentation.

Can I return (Twisted) deferreds from signal handlers?

Some signals support returning deferreds from their handlers, others don’t. See the Built-in signals reference to know which ones.

What does the response status code 999 means?

999 is a custom response status code used by Yahoo sites to throttle requests. Try slowing down the crawling speed by using a download delay of 2 (or higher) in your spider:

class MySpider(CrawlSpider): name = 'myspider' download_delay = 2 # [ ... rest of the spider code ... ]

Or by setting a global download delay in your project with the DOWNLOAD_DELAY setting.

Can I call pdb.set_trace() from my spiders to debug them?

Yes, but you can also use the Scrapy shell which allows you to quickly analyze (and even modify) the response being processed by your spider, which is, quite often, more useful than plain old pdb.set_trace().

For more info see Invoking the shell from spiders to inspect responses.

Simplest way to dump all my scraped items into a JSON/CSV/XML file?

To dump into a JSON file:

scrapy crawl myspider -o items.json

To dump into a CSV file:

scrapy crawl myspider -o items.csv

To dump into a XML file:

scrapy crawl myspider -o items.xml

For more information see Feed exports

What’s this huge cryptic __VIEWSTATE parameter used in some forms?

The __VIEWSTATE parameter is used in sites built with ASP.NET/VB.NET. For more info on how it works see this page [http://search.cpan.org/~ecarroll/HTML-TreeBuilderX-ASP_NET-0.09/lib/HTML/TreeBuilderX/ASP_NET.pm]. Also, here’s an example spider [https://github.com/AmbientLighter/rpn-fas/blob/master/fas/spiders/rnp.py] which scrapes one of these sites.

What’s the best way to parse big XML/CSV data feeds?

Parsing big feeds with XPath selectors can be problematic since they need to build the DOM of the entire feed in memory, and this can be quite slow and consume a lot of memory.

In order to avoid parsing all the entire feed at once in memory, you can use the functions xmliter and csviter from scrapy.utils.iterators module. In fact, this is what the feed spiders (see Spiders) use under the cover.

Does Scrapy manage cookies automatically?

Yes, Scrapy receives and keeps track of cookies sent by servers, and sends them back on subsequent requests, like any regular web browser does.

For more info see Requests and Responses and CookiesMiddleware.

How can I see the cookies being sent and received from Scrapy?

Enable the COOKIES_DEBUG setting.

How can I instruct a spider to stop itself?

Raise the CloseSpider exception from a callback. For more info see: CloseSpider.

How can I prevent my Scrapy bot from getting banned?

See Avoiding getting banned.

Should I use spider arguments or settings to configure my spider?

Both spider arguments and settings can be used to configure your spider. There is no strict rule that mandates to use one or the other, but settings are more suited for parameters that, once set, don’t change much, while spider arguments are meant to change more often, even on each spider run and sometimes are required for the spider to run at all (for example, to set the start url of a spider).

To illustrate with an example, assuming you have a spider that needs to log into a site to scrape data, and you only want to scrape data from a certain section of the site (which varies each time). In that case, the credentials to log in would be settings, while the url of the section to scrape would be a spider argument.

I’m scraping a XML document and my XPath selector doesn’t return any items

You may need to remove namespaces. See Removing namespaces.

How to split an item into multiple items in an item pipeline?

Item pipelines cannot yield multiple items per input item. Create a spider middleware instead, and use its process_spider_output() method for this puspose. For example:

from copy import deepcopy from scrapy.item import BaseItem class MultiplyItemsMiddleware: def process_spider_output(self, response, result, spider): for item in result: if isinstance(item, (BaseItem, dict)): for _ in range(item['multiply_by']): yield deepcopy(item)

Debugging Spiders

This document explains the most common techniques for debugging spiders. Consider the following scrapy spider below:

import scrapy from myproject.items import MyItem class MySpider(scrapy.Spider): name = 'myspider' start_urls = ( 'http://example.com/page1', 'http://example.com/page2', ) def parse(self, response): # <processing code not shown> # collect `item_urls` for item_url in item_urls: yield scrapy.Request(item_url, self.parse_item) def parse_item(self, response): # <processing code not shown> item = MyItem() # populate `item` fields # and extract item_details_url yield scrapy.Request(item_details_url, self.parse_details, cb_kwargs={'item': item}) def parse_details(self, response, item): # populate more `item` fields return item

Basically this is a simple spider which parses two pages of items (the start_urls). Items also have a details page with additional information, so we use the cb_kwargs functionality of Request to pass a partially populated item.

Parse Command

The most basic way of checking the output of your spider is to use the parse command. It allows to check the behaviour of different parts of the spider at the method level. It has the advantage of being flexible and simple to use, but does not allow debugging code inside a method.

In order to see the item scraped from a specific url:

$ scrapy parse --spider=myspider -c parse_item -d 2 <item_url> [ ... scrapy log lines crawling example.com spider ... ] >>> STATUS DEPTH LEVEL 2 <<< # Scraped Items ------------------------------------------------------------ [{'url': <item_url>}] # Requests ----------------------------------------------------------------- []

Using the --verbose or -v option we can see the status at each depth level:

$ scrapy parse --spider=myspider -c parse_item -d 2 -v <item_url> [ ... scrapy log lines crawling example.com spider ... ] >>> DEPTH LEVEL: 1 <<< # Scraped Items ------------------------------------------------------------ [] # Requests ----------------------------------------------------------------- [<GET item_details_url>] >>> DEPTH LEVEL: 2 <<< # Scraped Items ------------------------------------------------------------ [{'url': <item_url>}] # Requests ----------------------------------------------------------------- []

Checking items scraped from a single start_url, can also be easily achieved using:

$ scrapy parse --spider=myspider -d 3 'http://example.com/page1'

Scrapy Shell

While the parse command is very useful for checking behaviour of a spider, it is of little help to check what happens inside a callback, besides showing the response received and the output. How to debug the situation when parse_details sometimes receives no item?

Fortunately, the shell is your bread and butter in this case (see Invoking the shell from spiders to inspect responses):

from scrapy.shell import inspect_response def parse_details(self, response, item=None): if item: # populate more `item` fields return item else: inspect_response(response, self)

See also: Invoking the shell from spiders to inspect responses.

Open in browser

Sometimes you just want to see how a certain response looks in a browser, you can use the open_in_browser function for that. Here is an example of how you would use it:

from scrapy.utils.response import open_in_browser def parse_details(self, response): if "item name" not in response.body: open_in_browser(response)

open_in_browser will open a browser with the response received by Scrapy at that point, adjusting the base tag [https://www.w3schools.com/tags/tag_base.asp] so that images and styles are displayed properly.

Logging

Logging is another useful option for getting information about your spider run. Although not as convenient, it comes with the advantage that the logs will be available in all future runs should they be necessary again:

def parse_details(self, response, item=None): if item: # populate more `item` fields return item else: self.logger.warning('No item received for %s', response.url)

For more information, check the Logging section.

Spiders Contracts

New in version 0.15.

Testing spiders can get particularly annoying and while nothing prevents you from writing unit tests the task gets cumbersome quickly. Scrapy offers an integrated way of testing your spiders by the means of contracts.

This allows you to test each callback of your spider by hardcoding a sample url and check various constraints for how the callback processes the response. Each contract is prefixed with an @ and included in the docstring. See the following example:

def parse(self, response): """ This function parses a sample response. Some contracts are mingled with this docstring. @url http://www.amazon.com/s?field-keywords=selfish+gene @returns items 1 16 @returns requests 0 0 @scrapes Title Author Year Price """

This callback is tested using three built-in contracts:

class scrapy.contracts.default.UrlContract

This contract (@url) sets the sample URL used when checking other contract conditions for this spider. This contract is mandatory. All callbacks lacking this contract are ignored when running the checks:

@url url

class scrapy.contracts.default.CallbackKeywordArgumentsContract

This contract (@cb_kwargs) sets the cb_kwargs attribute for the sample request. It must be a valid JSON dictionary.

@cb_kwargs {"arg1": "value1", "arg2": "value2", ...}

class scrapy.contracts.default.ReturnsContract

This contract (@returns) sets lower and upper bounds for the items and requests returned by the spider. The upper bound is optional:

@returns item(s)|request(s) [min [max]]

class scrapy.contracts.default.ScrapesContract

This contract (@scrapes) checks that all the items returned by the callback have the specified fields:

@scrapes field_1 field_2 ...

Use the check command to run the contract checks.

Custom Contracts

If you find you need more power than the built-in scrapy contracts you can create and load your own contracts in the project by using the SPIDER_CONTRACTS setting:

SPIDER_CONTRACTS = { 'myproject.contracts.ResponseCheck': 10, 'myproject.contracts.ItemValidate': 10, }

Each contract must inherit from Contract and can override three methods:

class scrapy.contracts.Contract(method, *args)

Parameters

method (function) – callback function to which the contract is associated

args (list [https://docs.python.org/3/library/stdtypes.html#list]) – list of arguments passed into the docstring (whitespace separated)

adjust_request_args(args)

This receives a dict as an argument containing default arguments for request object. Request is used by default, but this can be changed with the request_cls attribute. If multiple contracts in chain have this attribute defined, the last one is used.

Must return the same or a modified version of it.

pre_process(response)

This allows hooking in various checks on the response received from the sample request, before it’s being passed to the callback.

post_process(output)

This allows processing the output of the callback. Iterators are converted listified before being passed to this hook.

Raise ContractFail from pre_process or post_process if expectations are not met:

class scrapy.exceptions.ContractFail

Error raised in case of a failing contract

Here is a demo contract which checks the presence of a custom header in the response received:

from scrapy.contracts import Contract from scrapy.exceptions import ContractFail class HasHeaderContract(Contract): """ Demo contract which checks the presence of a custom header @has_header X-CustomHeader """ name = 'has_header' def pre_process(self, response): for header in self.args: if header not in response.headers: raise ContractFail('X-CustomHeader not present')

Detecting check runs

When scrapy check is running, the SCRAPY_CHECK environment variable is set to the true string. You can use os.environ [https://docs.python.org/3/library/os.html#os.environ] to perform any change to your spiders or your settings when scrapy check is used:

import os import scrapy class ExampleSpider(scrapy.Spider): name = 'example' def __init__(self): if os.environ.get('SCRAPY_CHECK'): pass # Do some scraper adjustments when a check is running

Common Practices

This section documents common practices when using Scrapy. These are things that cover many topics and don’t often fall into any other specific section.

Run Scrapy from a script

You can use the API to run Scrapy from a script, instead of the typical way of running Scrapy via scrapy crawl.

Remember that Scrapy is built on top of the Twisted asynchronous networking library, so you need to run it inside the Twisted reactor.

The first utility you can use to run your spiders is scrapy.crawler.CrawlerProcess. This class will start a Twisted reactor for you, configuring the logging and setting shutdown handlers. This class is the one used by all Scrapy commands.

Here’s an example showing how to run a single spider with it.

import scrapy from scrapy.crawler import CrawlerProcess class MySpider(scrapy.Spider): # Your spider definition ... process = CrawlerProcess(settings={ 'FEED_FORMAT': 'json', 'FEED_URI': 'items.json' }) process.crawl(MySpider) process.start() # the script will block here until the crawling is finished

Define settings within dictionary in CrawlerProcess. Make sure to check CrawlerProcess documentation to get acquainted with its usage details.

If you are inside a Scrapy project there are some additional helpers you can use to import those components within the project. You can automatically import your spiders passing their name to CrawlerProcess, and use get_project_settings to get a Settings instance with your project settings.

What follows is a working example of how to do that, using the testspiders [https://github.com/scrapinghub/testspiders] project as example.

from scrapy.crawler import CrawlerProcess from scrapy.utils.project import get_project_settings process = CrawlerProcess(get_project_settings()) # 'followall' is the name of one of the spiders of the project. process.crawl('followall', domain='scrapinghub.com') process.start() # the script will block here until the crawling is finished

There’s another Scrapy utility that provides more control over the crawling process: scrapy.crawler.CrawlerRunner. This class is a thin wrapper that encapsulates some simple helpers to run multiple crawlers, but it won’t start or interfere with existing reactors in any way.

Using this class the reactor should be explicitly run after scheduling your spiders. It’s recommended you use CrawlerRunner instead of CrawlerProcess if your application is already using Twisted and you want to run Scrapy in the same reactor.

Note that you will also have to shutdown the Twisted reactor yourself after the spider is finished. This can be achieved by adding callbacks to the deferred returned by the CrawlerRunner.crawl method.

Here’s an example of its usage, along with a callback to manually stop the reactor after MySpider has finished running.

from twisted.internet import reactor import scrapy from scrapy.crawler import CrawlerRunner from scrapy.utils.log import configure_logging class MySpider(scrapy.Spider): # Your spider definition ... configure_logging({'LOG_FORMAT': '%(levelname)s: %(message)s'}) runner = CrawlerRunner() d = runner.crawl(MySpider) d.addBoth(lambda _: reactor.stop()) reactor.run() # the script will block here until the crawling is finished

See also

Twisted Reactor Overview [https://twistedmatrix.com/documents/current/core/howto/reactor-basics.html].

Running multiple spiders in the same process

By default, Scrapy runs a single spider per process when you run scrapy crawl. However, Scrapy supports running multiple spiders per process using the internal API.

Here is an example that runs multiple spiders simultaneously:

import scrapy from scrapy.crawler import CrawlerProcess class MySpider1(scrapy.Spider): # Your first spider definition ... class MySpider2(scrapy.Spider): # Your second spider definition ... process = CrawlerProcess() process.crawl(MySpider1) process.crawl(MySpider2) process.start() # the script will block here until all crawling jobs are finished

Same example using CrawlerRunner:

import scrapy from twisted.internet import reactor from scrapy.crawler import CrawlerRunner from scrapy.utils.log import configure_logging class MySpider1(scrapy.Spider): # Your first spider definition ... class MySpider2(scrapy.Spider): # Your second spider definition ... configure_logging() runner = CrawlerRunner() runner.crawl(MySpider1) runner.crawl(MySpider2) d = runner.join() d.addBoth(lambda _: reactor.stop()) reactor.run() # the script will block here until all crawling jobs are finished

Same example but running the spiders sequentially by chaining the deferreds:

from twisted.internet import reactor, defer from scrapy.crawler import CrawlerRunner from scrapy.utils.log import configure_logging class MySpider1(scrapy.Spider): # Your first spider definition ... class MySpider2(scrapy.Spider): # Your second spider definition ... configure_logging() runner = CrawlerRunner() @defer.inlineCallbacks def crawl(): yield runner.crawl(MySpider1) yield runner.crawl(MySpider2) reactor.stop() crawl() reactor.run() # the script will block here until the last crawl call is finished

See also

Run Scrapy from a script.

Distributed crawls

Scrapy doesn’t provide any built-in facility for running crawls in a distribute (multi-server) manner. However, there are some ways to distribute crawls, which vary depending on how you plan to distribute them.

If you have many spiders, the obvious way to distribute the load is to setup many Scrapyd instances and distribute spider runs among those.

If you instead want to run a single (big) spider through many machines, what you usually do is partition the urls to crawl and send them to each separate spider. Here is a concrete example:

First, you prepare the list of urls to crawl and put them into separate files/urls:

http://somedomain.com/urls-to-crawl/spider1/part1.list http://somedomain.com/urls-to-crawl/spider1/part2.list http://somedomain.com/urls-to-crawl/spider1/part3.list

Then you fire a spider run on 3 different Scrapyd servers. The spider would receive a (spider) argument part with the number of the partition to crawl:

curl http://scrapy1.mycompany.com:6800/schedule.json -d project=myproject -d spider=spider1 -d part=1 curl http://scrapy2.mycompany.com:6800/schedule.json -d project=myproject -d spider=spider1 -d part=2 curl http://scrapy3.mycompany.com:6800/schedule.json -d project=myproject -d spider=spider1 -d part=3

Avoiding getting banned

Some websites implement certain measures to prevent bots from crawling them, with varying degrees of sophistication. Getting around those measures can be difficult and tricky, and may sometimes require special infrastructure. Please consider contacting commercial support [https://scrapy.org/support/] if in doubt.

Here are some tips to keep in mind when dealing with these kinds of sites:

rotate your user agent from a pool of well-known ones from browsers (google around to get a list of them)

disable cookies (see COOKIES_ENABLED) as some sites may use cookies to spot bot behaviour

use download delays (2 or higher). See DOWNLOAD_DELAY setting.

if possible, use Google cache [http://www.googleguide.com/cached_pages.html] to fetch pages, instead of hitting the sites directly

use a pool of rotating IPs. For example, the free Tor project [https://www.torproject.org/] or paid services like ProxyMesh [https://proxymesh.com/]. An open source alternative is scrapoxy [https://scrapoxy.io/], a super proxy that you can attach your own proxies to.

use a highly distributed downloader that circumvents bans internally, so you can just focus on parsing clean pages. One example of such downloaders is Crawlera [https://scrapinghub.com/crawlera]

If you are still unable to prevent your bot getting banned, consider contacting commercial support [https://scrapy.org/support/].

Broad Crawls

Scrapy defaults are optimized for crawling specific sites. These sites are often handled by a single Scrapy spider, although this is not necessary or required (for example, there are generic spiders that handle any given site thrown at them).

In addition to this「focused crawl」, there is another common type of crawling which covers a large (potentially unlimited) number of domains, and is only limited by time or other arbitrary constraint, rather than stopping when the domain was crawled to completion or when there are no more requests to perform. These are called「broad crawls」and is the typical crawlers employed by search engines.

These are some common properties often found in broad crawls:

they crawl many domains (often, unbounded) instead of a specific set of sites

they don’t necessarily crawl domains to completion, because it would be impractical (or impossible) to do so, and instead limit the crawl by time or number of pages crawled

they are simpler in logic (as opposed to very complex spiders with many extraction rules) because data is often post-processed in a separate stage

they crawl many domains concurrently, which allows them to achieve faster crawl speeds by not being limited by any particular site constraint (each site is crawled slowly to respect politeness, but many sites are crawled in parallel)

As said above, Scrapy default settings are optimized for focused crawls, not broad crawls. However, due to its asynchronous architecture, Scrapy is very well suited for performing fast broad crawls. This page summarizes some things you need to keep in mind when using Scrapy for doing broad crawls, along with concrete suggestions of Scrapy settings to tune in order to achieve an efficient broad crawl.

Use the right SCHEDULER_PRIORITY_QUEUE

Scrapy’s default scheduler priority queue is 'scrapy.pqueues.ScrapyPriorityQueue'. It works best during single-domain crawl. It does not work well with crawling many different domains in parallel

To apply the recommended priority queue use:

SCHEDULER_PRIORITY_QUEUE = 'scrapy.pqueues.DownloaderAwarePriorityQueue'

Increase concurrency

Concurrency is the number of requests that are processed in parallel. There is a global limit (CONCURRENT_REQUESTS) and an additional limit that can be set either per domain (CONCURRENT_REQUESTS_PER_DOMAIN) or per IP (CONCURRENT_REQUESTS_PER_IP).

Note

The scheduler priority queue recommended for broad crawls does not support CONCURRENT_REQUESTS_PER_IP.

The default global concurrency limit in Scrapy is not suitable for crawling many different domains in parallel, so you will want to increase it. How much to increase it will depend on how much CPU and memory you crawler will have available.

A good starting point is 100:

CONCURRENT_REQUESTS = 100

But the best way to find out is by doing some trials and identifying at what concurrency your Scrapy process gets CPU bounded. For optimum performance, you should pick a concurrency where CPU usage is at 80-90%.

Increasing concurrency also increases memory usage. If memory usage is a concern, you might need to lower your global concurrency limit accordingly.

Increase Twisted IO thread pool maximum size

Currently Scrapy does DNS resolution in a blocking way with usage of thread pool. With higher concurrency levels the crawling could be slow or even fail hitting DNS resolver timeouts. Possible solution to increase the number of threads handling DNS queries. The DNS queue will be processed faster speeding up establishing of connection and crawling overall.

To increase maximum thread pool size use:

REACTOR_THREADPOOL_MAXSIZE = 20

Setup your own DNS

If you have multiple crawling processes and single central DNS, it can act like DoS attack on the DNS server resulting to slow down of entire network or even blocking your machines. To avoid this setup your own DNS server with local cache and upstream to some large DNS like OpenDNS or Verizon.

Reduce log level

When doing broad crawls you are often only interested in the crawl rates you get and any errors found. These stats are reported by Scrapy when using the INFO log level. In order to save CPU (and log storage requirements) you should not use DEBUG log level when preforming large broad crawls in production. Using DEBUG level when developing your (broad) crawler may be fine though.

To set the log level use:

LOG_LEVEL = 'INFO'

Disable cookies

Disable cookies unless you really need. Cookies are often not needed when doing broad crawls (search engine crawlers ignore them), and they improve performance by saving some CPU cycles and reducing the memory footprint of your Scrapy crawler.

To disable cookies use:

COOKIES_ENABLED = False

Disable retries

Retrying failed HTTP requests can slow down the crawls substantially, specially when sites causes are very slow (or fail) to respond, thus causing a timeout error which gets retried many times, unnecessarily, preventing crawler capacity to be reused for other domains.

To disable retries use:

RETRY_ENABLED = False

Reduce download timeout

Unless you are crawling from a very slow connection (which shouldn’t be the case for broad crawls) reduce the download timeout so that stuck requests are discarded quickly and free up capacity to process the next ones.

To reduce the download timeout use:

DOWNLOAD_TIMEOUT = 15

Disable redirects

Consider disabling redirects, unless you are interested in following them. When doing broad crawls it’s common to save redirects and resolve them when revisiting the site at a later crawl. This also help to keep the number of request constant per crawl batch, otherwise redirect loops may cause the crawler to dedicate too many resources on any specific domain.

To disable redirects use:

REDIRECT_ENABLED = False

Enable crawling of「Ajax Crawlable Pages」

Some pages (up to 1%, based on empirical data from year 2013) declare themselves as ajax crawlable [https://developers.google.com/webmasters/ajax-crawling/docs/getting-started]. This means they provide plain HTML version of content that is usually available only via AJAX. Pages can indicate it in two ways:

by using #! in URL - this is the default way;

by using a special meta tag - this way is used on「main」,「index」website pages.

Scrapy handles (1) automatically; to handle (2) enable AjaxCrawlMiddleware:

AJAXCRAWL_ENABLED = True

When doing broad crawls it’s common to crawl a lot of「index」web pages; AjaxCrawlMiddleware helps to crawl them correctly. It is turned OFF by default because it has some performance overhead, and enabling it for focused crawls doesn’t make much sense.

Crawl in BFO order

Scrapy crawls in DFO order by default.

In broad crawls, however, page crawling tends to be faster than page processing. As a result, unprocessed early requests stay in memory until the final depth is reached, which can significantly increase memory usage.

Crawl in BFO order instead to save memory.

Be mindful of memory leaks

If your broad crawl shows a high memory usage, in addition to crawling in BFO order and lowering concurrency you should debug your memory leaks.

Using your browser’s Developer Tools for scraping

Here is a general guide on how to use your browser’s Developer Tools to ease the scraping process. Today almost all browsers come with built in Developer Tools [https://en.wikipedia.org/wiki/Web_development_tools] and although we will use Firefox in this guide, the concepts are applicable to any other browser.

In this guide we’ll introduce the basic tools to use from a browser’s Developer Tools by scraping quotes.toscrape.com [http://quotes.toscrape.com].

Caveats with inspecting the live browser DOM

Since Developer Tools operate on a live browser DOM, what you’ll actually see when inspecting the page source is not the original HTML, but a modified one after applying some browser clean up and executing Javascript code. Firefox, in particular, is known for adding <tbody> elements to tables. Scrapy, on the other hand, does not modify the original page HTML, so you won’t be able to extract any data if you use <tbody> in your XPath expressions.

Therefore, you should keep in mind the following things:

Disable Javascript while inspecting the DOM looking for XPaths to be used in Scrapy (in the Developer Tools settings click Disable JavaScript)

Never use full XPath paths, use relative and clever ones based on attributes (such as id, class, width, etc) or any identifying features like contains(@href, 'image').

Never include <tbody> elements in your XPath expressions unless you really know what you’re doing

Inspecting a website

By far the most handy feature of the Developer Tools is the Inspector feature, which allows you to inspect the underlying HTML code of any webpage. To demonstrate the Inspector, let’s look at the quotes.toscrape.com [http://quotes.toscrape.com]-site.

On the site we have a total of ten quotes from various authors with specific tags, as well as the Top Ten Tags. Let’s say we want to extract all the quotes on this page, without any meta-information about authors, tags, etc.

Instead of viewing the whole source code for the page, we can simply right click on a quote and select Inspect Element (Q), which opens up the Inspector. In it you should see something like this:

The interesting part for us is this:

<div class="quote" itemscope="" itemtype="http://schema.org/CreativeWork"> <span class="text" itemprop="text">(...)</span> <span>(...)</span> <div class="tags">(...)</div> </div>

If you hover over the first div directly above the span tag highlighted in the screenshot, you’ll see that the corresponding section of the webpage gets highlighted as well. So now we have a section, but we can’t find our quote text anywhere.

The advantage of the Inspector is that it automatically expands and collapses sections and tags of a webpage, which greatly improves readability. You can expand and collapse a tag by clicking on the arrow in front of it or by double clicking directly on the tag. If we expand the span tag with the class= "text" we will see the quote-text we clicked on. The Inspector lets you copy XPaths to selected elements. Let’s try it out: Right-click on the span tag, select Copy > XPath and paste it in the scrapy shell like so:

$ scrapy shell "http://quotes.toscrape.com/" (...) >>> response.xpath('/html/body/div/div[2]/div[1]/div[1]/span[1]/text()').getall() ['"The world as we have created it is a process of our thinking. It cannot be changed without changing our thinking.」]

Adding text() at the end we are able to extract the first quote with this basic selector. But this XPath is not really that clever. All it does is go down a desired path in the source code starting from html. So let’s see if we can refine our XPath a bit:

If we check the Inspector again we’ll see that directly beneath our expanded div tag we have nine identical div tags, each with the same attributes as our first. If we expand any of them, we’ll see the same structure as with our first quote: Two span tags and one div tag. We can expand each span tag with the class="text" inside our div tags and see each quote:

<div class="quote" itemscope="" itemtype="http://schema.org/CreativeWork"> <span class="text" itemprop="text">「The world as we have created it is a process of our thinking. It cannot be changed without changing our thinking.」</span> <span>(...)</span> <div class="tags">(...)</div> </div>

With this knowledge we can refine our XPath: Instead of a path to follow, we’ll simply select all span tags with the class="text" by using the has-class-extension [https://parsel.readthedocs.io/en/latest/usage.html#other-xpath-extensions]:

>>> response.xpath('//span[has-class("text")]/text()').getall() ['"The world as we have created it is a process of our thinking. It cannot be changed without changing our thinking.」, '「It is our choices, Harry, that show what we truly are, far more than our abilities.」', '「There are only two ways to live your life. One is as though nothing is a miracle. The other is as though everything is a miracle.」', (...)]

And with one simple, cleverer XPath we are able to extract all quotes from the page. We could have constructed a loop over our first XPath to increase the number of the last div, but this would have been unnecessarily complex and by simply constructing an XPath with has-class("text") we were able to extract all quotes in one line.

The Inspector has a lot of other helpful features, such as searching in the source code or directly scrolling to an element you selected. Let’s demonstrate a use case:

Say you want to find the Next button on the page. Type Next into the search bar on the top right of the Inspector. You should get two results. The first is a li tag with the class="text", the second the text of an a tag. Right click on the a tag and select Scroll into View. If you hover over the tag, you’ll see the button highlighted. From here we could easily create a Link Extractor to follow the pagination. On a simple site such as this, there may not be the need to find an element visually but the Scroll into View function can be quite useful on complex sites.

Note that the search bar can also be used to search for and test CSS selectors. For example, you could search for span.text to find all quote texts. Instead of a full text search, this searches for exactly the span tag with the class="text" in the page.

The Network-tool

While scraping you may come across dynamic webpages where some parts of the page are loaded dynamically through multiple requests. While this can be quite tricky, the Network-tool in the Developer Tools greatly facilitates this task. To demonstrate the Network-tool, let’s take a look at the page quotes.toscrape.com/scroll [http://quotes.toscrape.com/scroll].

The page is quite similar to the basic quotes.toscrape.com [http://quotes.toscrape.com]-page, but instead of the above-mentioned Next button, the page automatically loads new quotes when you scroll to the bottom. We could go ahead and try out different XPaths directly, but instead we’ll check another quite useful command from the scrapy shell:

$ scrapy shell "quotes.toscrape.com/scroll" (...) >>> view(response)

A browser window should open with the webpage but with one crucial difference: Instead of the quotes we just see a greenish bar with the word Loading....

The view(response) command let’s us view the response our shell or later our spider receives from the server. Here we see that some basic template is loaded which includes the title, the login-button and the footer, but the quotes are missing. This tells us that the quotes are being loaded from a different request than quotes.toscrape/scroll.

If you click on the Network tab, you will probably only see two entries. The first thing we do is enable persistent logs by clicking on Persist Logs. If this option is disabled, the log is automatically cleared each time you navigate to a different page. Enabling this option is a good default, since it gives us control on when to clear the logs.

If we reload the page now, you’ll see the log get populated with six new requests.

Here we see every request that has been made when reloading the page and can inspect each request and its response. So let’s find out where our quotes are coming from:

First click on the request with the name scroll. On the right you can now inspect the request. In Headers you’ll find details about the request headers, such as the URL, the method, the IP-address, and so on. We’ll ignore the other tabs and click directly on Response.

What you should see in the Preview pane is the rendered HTML-code, that is exactly what we saw when we called view(response) in the shell. Accordingly the type of the request in the log is html. The other requests have types like css or js, but what interests us is the one request called quotes?page=1 with the type json.

If we click on this request, we see that the request URL is http://quotes.toscrape.com/api/quotes?page=1 and the response is a JSON-object that contains our quotes. We can also right-click on the request and open Open in new tab to get a better overview.

With this response we can now easily parse the JSON-object and also request each page to get every quote on the site:

import scrapy import json class QuoteSpider(scrapy.Spider): name = 'quote' allowed_domains = ['quotes.toscrape.com'] page = 1 start_urls = ['http://quotes.toscrape.com/api/quotes?page=1'] def parse(self, response): data = json.loads(response.text) for quote in data["quotes"]: yield {"quote": quote["text"]} if data["has_next"]: self.page += 1 url = "http://quotes.toscrape.com/api/quotes?page={}".format(self.page) yield scrapy.Request(url=url, callback=self.parse)

This spider starts at the first page of the quotes-API. With each response, we parse the response.text and assign it to data. This lets us operate on the JSON-object like on a Python dictionary. We iterate through the quotes and print out the quote["text"]. If the handy has_next element is true (try loading quotes.toscrape.com/api/quotes?page=10 [http://quotes.toscrape.com/api/quotes?page=10] in your browser or a page-number greater than 10), we increment the page attribute and yield a new request, inserting the incremented page-number into our url.

In more complex websites, it could be difficult to easily reproduce the requests, as we could need to add headers or cookies to make it work. In those cases you can export the requests in cURL [https://curl.haxx.se/] format, by right-clicking on each of them in the network tool and using the from_curl() method to generate an equivalent request:

from scrapy import Request request = Request.from_curl( "curl 'http://quotes.toscrape.com/api/quotes?page=1' -H 'User-Agent: Mozil" "la/5.0 (X11; Linux x86_64; rv:67.0) Gecko/20100101 Firefox/67.0' -H 'Acce" "pt: */*' -H 'Accept-Language: ca,en-US;q=0.7,en;q=0.3' --compressed -H 'X" "-Requested-With: XMLHttpRequest' -H 'Proxy-Authorization: Basic QFRLLTAzM" "zEwZTAxLTk5MWUtNDFiNC1iZWRmLTJjNGI4M2ZiNDBmNDpAVEstMDMzMTBlMDEtOTkxZS00MW" "I0LWJlZGYtMmM0YjgzZmI0MGY0' -H 'Connection: keep-alive' -H 'Referer: http" "://quotes.toscrape.com/scroll' -H 'Cache-Control: max-age=0'")

Alternatively, if you want to know the arguments needed to recreate that request you can use the scrapy.utils.curl.curl_to_request_kwargs() function to get a dictionary with the equivalent arguments.

As you can see, with a few inspections in the Network-tool we were able to easily replicate the dynamic requests of the scrolling functionality of the page. Crawling dynamic pages can be quite daunting and pages can be very complex, but it (mostly) boils down to identifying the correct request and replicating it in your spider.

Selecting dynamically-loaded content

Some webpages show the desired data when you load them in a web browser. However, when you download them using Scrapy, you cannot reach the desired data using selectors.

When this happens, the recommended approach is to find the data source and extract the data from it.

If you fail to do that, and you can nonetheless access the desired data through the DOM from your web browser, see Pre-rendering JavaScript.

Finding the data source

To extract the desired data, you must first find its source location.

If the data is in a non-text-based format, such as an image or a PDF document, use the network tool of your web browser to find the corresponding request, and reproduce it.

If your web browser lets you select the desired data as text, the data may be defined in embedded JavaScript code, or loaded from an external resource in a text-based format.

In that case, you can use a tool like wgrep [https://github.com/stav/wgrep] to find the URL of that resource.

If the data turns out to come from the original URL itself, you must inspect the source code of the webpage to determine where the data is located.

If the data comes from a different URL, you will need to reproduce the corresponding request.

Inspecting the source code of a webpage

Sometimes you need to inspect the source code of a webpage (not the DOM) to determine where some desired data is located.

Use Scrapy’s fetch command to download the webpage contents as seen by Scrapy:

scrapy fetch --nolog https://example.com > response.html

If the desired data is in embedded JavaScript code within a <script/> element, see Parsing JavaScript code.

If you cannot find the desired data, first make sure it’s not just Scrapy: download the webpage with an HTTP client like curl [https://curl.haxx.se/] or wget [https://www.gnu.org/software/wget/] and see if the information can be found in the response they get.

If they get a response with the desired data, modify your Scrapy Request to match that of the other HTTP client. For example, try using the same user-agent string (USER_AGENT) or the same headers.

If they also get a response without the desired data, you’ll need to take steps to make your request more similar to that of the web browser. See Reproducing requests.

Reproducing requests

Sometimes we need to reproduce a request the way our web browser performs it.

Use the network tool of your web browser to see how your web browser performs the desired request, and try to reproduce that request with Scrapy.

It might be enough to yield a Request with the same HTTP method and URL. However, you may also need to reproduce the body, headers and form parameters (see FormRequest) of that request.

As all major browsers allow to export the requests in cURL [https://curl.haxx.se/] format, Scrapy incorporates the method from_curl() to generate an equivalent Request from a cURL command. To get more information visit request from curl inside the network tool section.

Once you get the expected response, you can extract the desired data from it.

You can reproduce any request with Scrapy. However, some times reproducing all necessary requests may not seem efficient in developer time. If that is your case, and crawling speed is not a major concern for you, you can alternatively consider JavaScript pre-rendering.

If you get the expected response sometimes, but not always, the issue is probably not your request, but the target server. The target server might be buggy, overloaded, or banning some of your requests.

Handling different response formats

Once you have a response with the desired data, how you extract the desired data from it depends on the type of response:

If the response is HTML or XML, use selectors as usual.

If the response is JSON, use json.loads [https://docs.python.org/library/json.html#json.loads] to load the desired data from response.text:

data = json.loads(response.text)

If the desired data is inside HTML or XML code embedded within JSON data, you can load that HTML or XML code into a Selector and then use it as usual:

selector = Selector(data['html'])

If the response is JavaScript, or HTML with a <script/> element containing the desired data, see Parsing JavaScript code.

If the response is CSS, use a regular expression [https://docs.python.org/library/re.html] to extract the desired data from response.text.

If the response is an image or another format based on images (e.g. PDF), read the response as bytes from response.body and use an OCR solution to extract the desired data as text.

For example, you can use pytesseract [https://github.com/madmaze/pytesseract]. To read a table from a PDF, tabula-py [https://github.com/chezou/tabula-py] may be a better choice.

If the response is SVG, or HTML with embedded SVG containing the desired data, you may be able to extract the desired data using selectors, since SVG is based on XML.

Otherwise, you might need to convert the SVG code into a raster image, and handle that raster image.

Parsing JavaScript code

If the desired data is hardcoded in JavaScript, you first need to get the JavaScript code:

If the JavaScript code is in a JavaScript file, simply read response.text.

If the JavaScript code is within a <script/> element of an HTML page, use selectors to extract the text within that <script/> element.

Once you have a string with the JavaScript code, you can extract the desired data from it:

You might be able to use a regular expression [https://docs.python.org/library/re.html] to extract the desired data in JSON format, which you can then parse with json.loads [https://docs.python.org/library/json.html#json.loads].

For example, if the JavaScript code contains a separate line like var data = {"field": "value"}; you can extract that data as follows:

>>> pattern = r'\bvar\s+data\s*=\s*(\{.*?\})\s*;\s*\n' >>> json_data = response.css('script::text').re_first(pattern) >>> json.loads(json_data) {'field': 'value'}

Otherwise, use js2xml [https://github.com/scrapinghub/js2xml] to convert the JavaScript code into an XML document that you can parse using selectors.

For example, if the JavaScript code contains var data = {field: "value"}; you can extract that data as follows:

>>> import js2xml >>> import lxml.etree >>> from parsel import Selector >>> javascript = response.css('script::text').get() >>> xml = lxml.etree.tostring(js2xml.parse(javascript), encoding='unicode') >>> selector = Selector(text=xml) >>> selector.css('var[name="data"]').get() '<var name="data"><object><property name="field"><string>value</string></property></object></var>'

Pre-rendering JavaScript

On webpages that fetch data from additional requests, reproducing those requests that contain the desired data is the preferred approach. The effort is often worth the result: structured, complete data with minimum parsing time and network transfer.

However, sometimes it can be really hard to reproduce certain requests. Or you may need something that no request can give you, such as a screenshot of a webpage as seen in a web browser.

In these cases use the Splash [https://github.com/scrapinghub/splash] JavaScript-rendering service, along with scrapy-splash [https://github.com/scrapy-plugins/scrapy-splash] for seamless integration.

Splash returns as HTML the DOM of a webpage, so that you can parse it with selectors. It provides great flexibility through configuration [https://splash.readthedocs.io/en/stable/api.html] or scripting [https://splash.readthedocs.io/en/stable/scripting-tutorial.html].

If you need something beyond what Splash offers, such as interacting with the DOM on-the-fly from Python code instead of using a previously-written script, or handling multiple web browser windows, you might need to use a headless browser instead.

Using a headless browser

A headless browser [https://en.wikipedia.org/wiki/Headless_browser] is a special web browser that provides an API for automation.

The easiest way to use a headless browser with Scrapy is to use Selenium [https://www.seleniumhq.org/], along with scrapy-selenium [https://github.com/clemfromspace/scrapy-selenium] for seamless integration.

Debugging memory leaks

In Scrapy, objects such as Requests, Responses and Items have a finite lifetime: they are created, used for a while, and finally destroyed.

From all those objects, the Request is probably the one with the longest lifetime, as it stays waiting in the Scheduler queue until it’s time to process it. For more info see Architecture overview.

As these Scrapy objects have a (rather long) lifetime, there is always the risk of accumulating them in memory without releasing them properly and thus causing what is known as a「memory leak」.

To help debugging memory leaks, Scrapy provides a built-in mechanism for tracking objects references called trackref, and you can also use a third-party library called Guppy for more advanced memory debugging (see below for more info). Both mechanisms must be used from the Telnet Console.

Common causes of memory leaks

It happens quite often (sometimes by accident, sometimes on purpose) that the Scrapy developer passes objects referenced in Requests (for example, using the cb_kwargs or meta attributes or the request callback function) and that effectively bounds the lifetime of those referenced objects to the lifetime of the Request. This is, by far, the most common cause of memory leaks in Scrapy projects, and a quite difficult one to debug for newcomers.

In big projects, the spiders are typically written by different people and some of those spiders could be「leaking」and thus affecting the rest of the other (well-written) spiders when they get to run concurrently, which, in turn, affects the whole crawling process.

The leak could also come from a custom middleware, pipeline or extension that you have written, if you are not releasing the (previously allocated) resources properly. For example, allocating resources on spider_opened but not releasing them on spider_closed may cause problems if you’re running multiple spiders per process.

Too Many Requests?

By default Scrapy keeps the request queue in memory; it includes Request objects and all objects referenced in Request attributes (e.g. in cb_kwargs and meta). While not necessarily a leak, this can take a lot of memory. Enabling persistent job queue could help keeping memory usage in control.

Debugging memory leaks with trackref

trackref is a module provided by Scrapy to debug the most common cases of memory leaks. It basically tracks the references to all live Requests, Responses, Item and Selector objects.

You can enter the telnet console and inspect how many objects (of the classes mentioned above) are currently alive using the prefs() function which is an alias to the print_live_refs() function:

telnet localhost 6023 >>> prefs() Live References ExampleSpider 1 oldest: 15s ago HtmlResponse 10 oldest: 1s ago Selector 2 oldest: 0s ago FormRequest 878 oldest: 7s ago

As you can see, that report also shows the「age」of the oldest object in each class. If you’re running multiple spiders per process chances are you can figure out which spider is leaking by looking at the oldest request or response. You can get the oldest object of each class using the get_oldest() function (from the telnet console).

Which objects are tracked?

The objects tracked by trackrefs are all from these classes (and all its subclasses):

scrapy.http.Request

scrapy.http.Response

scrapy.item.Item

scrapy.selector.Selector

scrapy.spiders.Spider

A real example

Let’s see a concrete example of a hypothetical case of memory leaks. Suppose we have some spider with a line similar to this one:

return Request("http://www.somenastyspider.com/product.php?pid=%d" % product_id, callback=self.parse, cb_kwargs={'referer': response})

That line is passing a response reference inside a request which effectively ties the response lifetime to the requests’ one, and that would definitely cause memory leaks.

Let’s see how we can discover the cause (without knowing it a-priori, of course) by using the trackref tool.

After the crawler is running for a few minutes and we notice its memory usage has grown a lot, we can enter its telnet console and check the live references:

>>> prefs() Live References SomenastySpider 1 oldest: 15s ago HtmlResponse 3890 oldest: 265s ago Selector 2 oldest: 0s ago Request 3878 oldest: 250s ago

The fact that there are so many live responses (and that they’re so old) is definitely suspicious, as responses should have a relatively short lifetime compared to Requests. The number of responses is similar to the number of requests, so it looks like they are tied in a some way. We can now go and check the code of the spider to discover the nasty line that is generating the leaks (passing response references inside requests).

Sometimes extra information about live objects can be helpful. Let’s check the oldest response:

>>> from scrapy.utils.trackref import get_oldest >>> r = get_oldest('HtmlResponse') >>> r.url 'http://www.somenastyspider.com/product.php?pid=123'

If you want to iterate over all objects, instead of getting the oldest one, you can use the scrapy.utils.trackref.iter_all() function:

>>> from scrapy.utils.trackref import iter_all >>> [r.url for r in iter_all('HtmlResponse')] ['http://www.somenastyspider.com/product.php?pid=123', 'http://www.somenastyspider.com/product.php?pid=584', ...

Too many spiders?

If your project has too many spiders executed in parallel, the output of prefs() can be difficult to read. For this reason, that function has a ignore argument which can be used to ignore a particular class (and all its subclases). For example, this won’t show any live references to spiders:

>>> from scrapy.spiders import Spider >>> prefs(ignore=Spider)

scrapy.utils.trackref module

Here are the functions available in the trackref module.

class scrapy.utils.trackref.object_ref

Inherit from this class (instead of object) if you want to track live instances with the trackref module.

scrapy.utils.trackref.print_live_refs(class_name, ignore=NoneType)

Print a report of live references, grouped by class name.

Parameters

ignore (class or classes tuple) – if given, all objects from the specified class (or tuple of classes) will be ignored.

scrapy.utils.trackref.get_oldest(class_name)

Return the oldest object alive with the given class name, or None if none is found. Use print_live_refs() first to get a list of all tracked live objects per class name.

scrapy.utils.trackref.iter_all(class_name)

Return an iterator over all objects alive with the given class name, or None if none is found. Use print_live_refs() first to get a list of all tracked live objects per class name.

Debugging memory leaks with Guppy

trackref provides a very convenient mechanism for tracking down memory leaks, but it only keeps track of the objects that are more likely to cause memory leaks (Requests, Responses, Items, and Selectors). However, there are other cases where the memory leaks could come from other (more or less obscure) objects. If this is your case, and you can’t find your leaks using trackref, you still have another resource: the Guppy library [https://pypi.python.org/pypi/guppy]. If you’re using Python3, see Debugging memory leaks with muppy.

If you use pip, you can install Guppy with the following command:

pip install guppy

The telnet console also comes with a built-in shortcut (hpy) for accessing Guppy heap objects. Here’s an example to view all Python objects available in the heap using Guppy:

>>> x = hpy.heap() >>> x.bytype Partition of a set of 297033 objects. Total size = 52587824 bytes. Index Count % Size % Cumulative % Type 0 22307 8 16423880 31 16423880 31 dict 1 122285 41 12441544 24 28865424 55 str 2 68346 23 5966696 11 34832120 66 tuple 3 227 0 5836528 11 40668648 77 unicode 4 2461 1 2222272 4 42890920 82 type 5 16870 6 2024400 4 44915320 85 function 6 13949 5 1673880 3 46589200 89 types.CodeType 7 13422 5 1653104 3 48242304 92 list 8 3735 1 1173680 2 49415984 94 _sre.SRE_Pattern 9 1209 0 456936 1 49872920 95 scrapy.http.headers.Headers <1676 more rows. Type e.g. '_.more' to view.>

You can see that most space is used by dicts. Then, if you want to see from which attribute those dicts are referenced, you could do:

>>> x.bytype[0].byvia Partition of a set of 22307 objects. Total size = 16423880 bytes. Index Count % Size % Cumulative % Referred Via: 0 10982 49 9416336 57 9416336 57 '.__dict__' 1 1820 8 2681504 16 12097840 74 '.__dict__', '.func_globals' 2 3097 14 1122904 7 13220744 80 3 990 4 277200 2 13497944 82 "['cookies']" 4 987 4 276360 2 13774304 84 "['cache']" 5 985 4 275800 2 14050104 86 "['meta']" 6 897 4 251160 2 14301264 87 '[2]' 7 1 0 196888 1 14498152 88 "['moduleDict']", "['modules']" 8 672 3 188160 1 14686312 89 "['cb_kwargs']" 9 27 0 155016 1 14841328 90 '[1]' <333 more rows. Type e.g. '_.more' to view.>

As you can see, the Guppy module is very powerful but also requires some deep knowledge about Python internals. For more info about Guppy, refer to the Guppy documentation [http://guppy-pe.sourceforge.net/].

Debugging memory leaks with muppy

If you’re using Python 3, you can use muppy from Pympler [https://pypi.org/project/Pympler/].

If you use pip, you can install muppy with the following command:

pip install Pympler

Here’s an example to view all Python objects available in the heap using muppy:

>>> from pympler import muppy >>> all_objects = muppy.get_objects() >>> len(all_objects) 28667 >>> from pympler import summary >>> suml = summary.summarize(all_objects) >>> summary.print_(suml) types | # objects | total size ==================================== | =========== | ============ <class 'str | 9822 | 1.10 MB <class 'dict | 1658 | 856.62 KB <class 'type | 436 | 443.60 KB <class 'code | 2974 | 419.56 KB <class '_io.BufferedWriter | 2 | 256.34 KB <class 'set | 420 | 159.88 KB <class '_io.BufferedReader | 1 | 128.17 KB <class 'wrapper_descriptor | 1130 | 88.28 KB <class 'tuple | 1304 | 86.57 KB <class 'weakref | 1013 | 79.14 KB <class 'builtin_function_or_method | 958 | 67.36 KB <class 'method_descriptor | 865 | 60.82 KB <class 'abc.ABCMeta | 62 | 59.96 KB <class 'list | 446 | 58.52 KB <class 'int | 1425 | 43.20 KB

For more info about muppy, refer to the muppy documentation [https://pythonhosted.org/Pympler/muppy.html].

Leaks without leaks

Sometimes, you may notice that the memory usage of your Scrapy process will only increase, but never decrease. Unfortunately, this could happen even though neither Scrapy nor your project are leaking memory. This is due to a (not so well) known problem of Python, which may not return released memory to the operating system in some cases. For more information on this issue see:

Python Memory Management [http://www.evanjones.ca/python-memory.html]

Python Memory Management Part 2 [http://www.evanjones.ca/python-memory-part2.html]

Python Memory Management Part 3 [http://www.evanjones.ca/python-memory-part3.html]

The improvements proposed by Evan Jones, which are detailed in this paper [http://www.evanjones.ca/memoryallocator/], got merged in Python 2.5, but this only reduces the problem, it doesn’t fix it completely. To quote the paper:

Unfortunately, this patch can only free an arena if there are no more objects allocated in it anymore. This means that fragmentation is a large issue. An application could have many megabytes of free memory, scattered throughout all the arenas, but it will be unable to free any of it. This is a problem experienced by all memory allocators. The only way to solve it is to move to a compacting garbage collector, which is able to move objects in memory. This would require significant changes to the Python interpreter.

To keep memory consumption reasonable you can split the job into several smaller jobs or enable persistent job queue and stop/start spider from time to time.

Downloading and processing files and images

Scrapy provides reusable item pipelines for downloading files attached to a particular item (for example, when you scrape products and also want to download their images locally). These pipelines share a bit of functionality and structure (we refer to them as media pipelines), but typically you’ll either use the Files Pipeline or the Images Pipeline.

Both pipelines implement these features:

Avoid re-downloading media that was downloaded recently

Specifying where to store the media (filesystem directory, Amazon S3 bucket, Google Cloud Storage bucket)

The Images Pipeline has a few extra functions for processing images:

Convert all downloaded images to a common format (JPG) and mode (RGB)

Thumbnail generation

Check images width/height to make sure they meet a minimum constraint

The pipelines also keep an internal queue of those media URLs which are currently being scheduled for download, and connect those responses that arrive containing the same media to that queue. This avoids downloading the same media more than once when it’s shared by several items.

Using the Files Pipeline

The typical workflow, when using the FilesPipeline goes like this:

In a Spider, you scrape an item and put the URLs of the desired into a file_urls field.

The item is returned from the spider and goes to the item pipeline.

When the item reaches the FilesPipeline, the URLs in the file_urls field are scheduled for download using the standard Scrapy scheduler and downloader (which means the scheduler and downloader middlewares are reused), but with a higher priority, processing them before other pages are scraped. The item remains「locked」at that particular pipeline stage until the files have finish downloading (or fail for some reason).

When the files are downloaded, another field (files) will be populated with the results. This field will contain a list of dicts with information about the downloaded files, such as the downloaded path, the original scraped url (taken from the file_urls field) , and the file checksum. The files in the list of the files field will retain the same order of the original file_urls field. If some file failed downloading, an error will be logged and the file won’t be present in the files field.

Using the Images Pipeline

Using the ImagesPipeline is a lot like using the FilesPipeline, except the default field names used are different: you use image_urls for the image URLs of an item and it will populate an images field for the information about the downloaded images.

The advantage of using the ImagesPipeline for image files is that you can configure some extra functions like generating thumbnails and filtering the images based on their size.

The Images Pipeline uses Pillow [https://github.com/python-pillow/Pillow] for thumbnailing and normalizing images to JPEG/RGB format, so you need to install this library in order to use it. Python Imaging Library [http://www.pythonware.com/products/pil/] (PIL) should also work in most cases, but it is known to cause troubles in some setups, so we recommend to use Pillow [https://github.com/python-pillow/Pillow] instead of PIL.

Enabling your Media Pipeline

To enable your media pipeline you must first add it to your project ITEM_PIPELINES setting.

For Images Pipeline, use:

ITEM_PIPELINES = {'scrapy.pipelines.images.ImagesPipeline': 1}

For Files Pipeline, use:

ITEM_PIPELINES = {'scrapy.pipelines.files.FilesPipeline': 1}

Note

You can also use both the Files and Images Pipeline at the same time.

Then, configure the target storage setting to a valid value that will be used for storing the downloaded images. Otherwise the pipeline will remain disabled, even if you include it in the ITEM_PIPELINES setting.

For the Files Pipeline, set the FILES_STORE setting:

FILES_STORE = '/path/to/valid/dir'

For the Images Pipeline, set the IMAGES_STORE setting:

IMAGES_STORE = '/path/to/valid/dir'

Supported Storage

File system is currently the only officially supported storage, but there are also support for storing files in Amazon S3 [https://aws.amazon.com/s3/] and Google Cloud Storage [https://cloud.google.com/storage/].

File system storage

The files are stored using a SHA1 hash [https://en.wikipedia.org/wiki/SHA_hash_functions] of their URLs for the file names.

For example, the following image URL:

http://www.example.com/image.jpg

Whose SHA1 hash is:

3afec3b4765f8f0a07b78f98c07b83f013567a0a

Will be downloaded and stored in the following file:

<IMAGES_STORE>/full/3afec3b4765f8f0a07b78f98c07b83f013567a0a.jpg

Where:

<IMAGES_STORE> is the directory defined in IMAGES_STORE setting for the Images Pipeline.

full is a sub-directory to separate full images from thumbnails (if used). For more info see Thumbnail generation for images.

Amazon S3 storage

FILES_STORE and IMAGES_STORE can represent an Amazon S3 bucket. Scrapy will automatically upload the files to the bucket.

For example, this is a valid IMAGES_STORE value:

IMAGES_STORE = 's3://bucket/images'

You can modify the Access Control List (ACL) policy used for the stored files, which is defined by the FILES_STORE_S3_ACL and IMAGES_STORE_S3_ACL settings. By default, the ACL is set to private. To make the files publicly available use the public-read policy:

IMAGES_STORE_S3_ACL = 'public-read'

For more information, see canned ACLs [https://docs.aws.amazon.com/AmazonS3/latest/dev/acl-overview.html#canned-acl] in the Amazon S3 Developer Guide.

Because Scrapy uses boto / botocore internally you can also use other S3-like storages. Storages like self-hosted Minio [https://github.com/minio/minio] or s3.scality [https://s3.scality.com/]. All you need to do is set endpoint option in you Scrapy settings:

AWS_ENDPOINT_URL = 'http://minio.example.com:9000'

For self-hosting you also might feel the need not to use SSL and not to verify SSL connection:

AWS_USE_SSL = False # or True (None by default) AWS_VERIFY = False # or True (None by default)

Google Cloud Storage

FILES_STORE and IMAGES_STORE can represent a Google Cloud Storage bucket. Scrapy will automatically upload the files to the bucket. (requires google-cloud-storage [https://cloud.google.com/storage/docs/reference/libraries#client-libraries-install-python] )

For example, these are valid IMAGES_STORE and GCS_PROJECT_ID settings:

IMAGES_STORE = 'gs://bucket/images/' GCS_PROJECT_ID = 'project_id'

For information about authentication, see this documentation [https://cloud.google.com/docs/authentication/production].

You can modify the Access Control List (ACL) policy used for the stored files, which is defined by the FILES_STORE_GCS_ACL and IMAGES_STORE_GCS_ACL settings. By default, the ACL is set to '' (empty string) which means that Cloud Storage applies the bucket’s default object ACL to the object. To make the files publicly available use the publicRead policy:

IMAGES_STORE_GCS_ACL = 'publicRead'

For more information, see Predefined ACLs [https://cloud.google.com/storage/docs/access-control/lists#predefined-acl] in the Google Cloud Platform Developer Guide.

Usage example

In order to use a media pipeline first, enable it.

Then, if a spider returns a dict with the URLs key (file_urls or image_urls, for the Files or Images Pipeline respectively), the pipeline will put the results under respective key (files or images).

If you prefer to use Item, then define a custom item with the necessary fields, like in this example for Images Pipeline:

import scrapy class MyItem(scrapy.Item): # ... other item fields ... image_urls = scrapy.Field() images = scrapy.Field()

If you want to use another field name for the URLs key or for the results key, it is also possible to override it.

For the Files Pipeline, set FILES_URLS_FIELD and/or FILES_RESULT_FIELD settings:

FILES_URLS_FIELD = 'field_name_for_your_files_urls' FILES_RESULT_FIELD = 'field_name_for_your_processed_files'

For the Images Pipeline, set IMAGES_URLS_FIELD and/or IMAGES_RESULT_FIELD settings:

IMAGES_URLS_FIELD = 'field_name_for_your_images_urls' IMAGES_RESULT_FIELD = 'field_name_for_your_processed_images'

If you need something more complex and want to override the custom pipeline behaviour, see Extending the Media Pipelines.

If you have multiple image pipelines inheriting from ImagePipeline and you want to have different settings in different pipelines you can set setting keys preceded with uppercase name of your pipeline class. E.g. if your pipeline is called MyPipeline and you want to have custom IMAGES_URLS_FIELD you define setting MYPIPELINE_IMAGES_URLS_FIELD and your custom settings will be used.

Additional features

File expiration

The Image Pipeline avoids downloading files that were downloaded recently. To adjust this retention delay use the FILES_EXPIRES setting (or IMAGES_EXPIRES, in case of Images Pipeline), which specifies the delay in number of days:

# 120 days of delay for files expiration FILES_EXPIRES = 120 # 30 days of delay for images expiration IMAGES_EXPIRES = 30

The default value for both settings is 90 days.

If you have pipeline that subclasses FilesPipeline and you’d like to have different setting for it you can set setting keys preceded by uppercase class name. E.g. given pipeline class called MyPipeline you can set setting key:

MYPIPELINE_FILES_EXPIRES = 180

and pipeline class MyPipeline will have expiration time set to 180.

Thumbnail generation for images

The Images Pipeline can automatically create thumbnails of the downloaded images.

In order to use this feature, you must set IMAGES_THUMBS to a dictionary where the keys are the thumbnail names and the values are their dimensions.

For example:

IMAGES_THUMBS = { 'small': (50, 50), 'big': (270, 270), }

When you use this feature, the Images Pipeline will create thumbnails of the each specified size with this format:

<IMAGES_STORE>/thumbs/<size_name>/<image_id>.jpg

Where:

<size_name> is the one specified in the IMAGES_THUMBS dictionary keys (small, big, etc)

<image_id> is the SHA1 hash [https://en.wikipedia.org/wiki/SHA_hash_functions] of the image url

Example of image files stored using small and big thumbnail names:

<IMAGES_STORE>/full/63bbfea82b8880ed33cdb762aa11fab722a90a24.jpg <IMAGES_STORE>/thumbs/small/63bbfea82b8880ed33cdb762aa11fab722a90a24.jpg <IMAGES_STORE>/thumbs/big/63bbfea82b8880ed33cdb762aa11fab722a90a24.jpg

The first one is the full image, as downloaded from the site.

Filtering out small images

When using the Images Pipeline, you can drop images which are too small, by specifying the minimum allowed size in the IMAGES_MIN_HEIGHT and IMAGES_MIN_WIDTH settings.

For example:

IMAGES_MIN_HEIGHT = 110 IMAGES_MIN_WIDTH = 110

Note

The size constraints don’t affect thumbnail generation at all.

It is possible to set just one size constraint or both. When setting both of them, only images that satisfy both minimum sizes will be saved. For the above example, images of sizes (105 x 105) or (105 x 200) or (200 x 105) will all be dropped because at least one dimension is shorter than the constraint.

By default, there are no size constraints, so all images are processed.

Allowing redirections

By default media pipelines ignore redirects, i.e. an HTTP redirection to a media file URL request will mean the media download is considered failed.

To handle media redirections, set this setting to True:

MEDIA_ALLOW_REDIRECTS = True

Extending the Media Pipelines

See here the methods that you can override in your custom Files Pipeline:

class scrapy.pipelines.files.FilesPipeline

file_path(request, response, info)

This method is called once per downloaded item. It returns the download path of the file originating from the specified response.

In addition to response, this method receives the original request and info.

You can override this method to customize the download path of each file.

For example, if file URLs end like regular paths (e.g. https://example.com/a/b/c/foo.png), you can use the following approach to download all files into the files folder with their original filenames (e.g. files/foo.png):

import os from urllib.parse import urlparse from scrapy.pipelines.files import FilesPipeline class MyFilesPipeline(FilesPipeline): def file_path(self, request, response, info): return 'files/' + os.path.basename(urlparse(request.url).path)

By default the file_path() method returns full/<request URL hash>.<extension>.

get_media_requests(item, info)

As seen on the workflow, the pipeline will get the URLs of the images to download from the item. In order to do this, you can override the get_media_requests() method and return a Request for each file URL:

def get_media_requests(self, item, info): for file_url in item['file_urls']: yield scrapy.Request(file_url)

Those requests will be processed by the pipeline and, when they have finished downloading, the results will be sent to the item_completed() method, as a list of 2-element tuples. Each tuple will contain (success, file_info_or_error) where:

success is a boolean which is True if the image was downloaded successfully or False if it failed for some reason

file_info_or_error is a dict containing the following keys (if success is True) or a Twisted Failure [https://twistedmatrix.com/documents/current/api/twisted.python.failure.Failure.html] if there was a problem.

url - the url where the file was downloaded from. This is the url of the request returned from the get_media_requests() method.

path - the path (relative to FILES_STORE) where the file was stored

checksum - a MD5 hash [https://en.wikipedia.org/wiki/MD5] of the image contents

The list of tuples received by item_completed() is guaranteed to retain the same order of the requests returned from the get_media_requests() method.

Here’s a typical value of the results argument:

[(True, {'checksum': '2b00042f7481c7b056c4b410d28f33cf', 'path': 'full/0a79c461a4062ac383dc4fade7bc09f1384a3910.jpg', 'url': 'http://www.example.com/files/product1.pdf'}), (False, Failure(...))]

By default the get_media_requests() method returns None which means there are no files to download for the item.

item_completed(results, item, info)

The FilesPipeline.item_completed() method called when all file requests for a single item have completed (either finished downloading, or failed for some reason).

The item_completed() method must return the output that will be sent to subsequent item pipeline stages, so you must return (or drop) the item, as you would in any pipeline.

Here is an example of the item_completed() method where we store the downloaded file paths (passed in results) in the file_paths item field, and we drop the item if it doesn’t contain any files:

from scrapy.exceptions import DropItem def item_completed(self, results, item, info): file_paths = [x['path'] for ok, x in results if ok] if not file_paths: raise DropItem("Item contains no files") item['file_paths'] = file_paths return item

By default, the item_completed() method returns the item.

See here the methods that you can override in your custom Images Pipeline:

class scrapy.pipelines.images.ImagesPipeline

The ImagesPipeline is an extension of the FilesPipeline, customizing the field names and adding custom behavior for images.

file_path(request, response, info)

This method is called once per downloaded item. It returns the download path of the file originating from the specified response.

In addition to response, this method receives the original request and info.

You can override this method to customize the download path of each file.

For example, if file URLs end like regular paths (e.g. https://example.com/a/b/c/foo.png), you can use the following approach to download all files into the files folder with their original filenames (e.g. files/foo.png):

import os from urllib.parse import urlparse from scrapy.pipelines.images import ImagesPipeline class MyImagesPipeline(ImagesPipeline): def file_path(self, request, response, info): return 'files/' + os.path.basename(urlparse(request.url).path)

By default the file_path() method returns full/<request URL hash>.<extension>.

get_media_requests(item, info)

Works the same way as FilesPipeline.get_media_requests() method, but using a different field name for image urls.

Must return a Request for each image URL.

item_completed(results, item, info)

The ImagesPipeline.item_completed() method is called when all image requests for a single item have completed (either finished downloading, or failed for some reason).

Works the same way as FilesPipeline.item_completed() method, but using a different field names for storing image downloading results.

By default, the item_completed() method returns the item.

Custom Images pipeline example

Here is a full example of the Images Pipeline whose methods are examplified above:

import scrapy from scrapy.pipelines.images import ImagesPipeline from scrapy.exceptions import DropItem class MyImagesPipeline(ImagesPipeline): def get_media_requests(self, item, info): for image_url in item['image_urls']: yield scrapy.Request(image_url) def item_completed(self, results, item, info): image_paths = [x['path'] for ok, x in results if ok] if not image_paths: raise DropItem("Item contains no images") item['image_paths'] = image_paths return item

Deploying Spiders

This section describes the different options you have for deploying your Scrapy spiders to run them on a regular basis. Running Scrapy spiders in your local machine is very convenient for the (early) development stage, but not so much when you need to execute long-running spiders or move spiders to run in production continuously. This is where the solutions for deploying Scrapy spiders come in.

Popular choices for deploying Scrapy spiders are:

Scrapyd (open source)

Scrapy Cloud (cloud-based)

Deploying to a Scrapyd Server

Scrapyd [https://github.com/scrapy/scrapyd] is an open source application to run Scrapy spiders. It provides a server with HTTP API, capable of running and monitoring Scrapy spiders.

To deploy spiders to Scrapyd, you can use the scrapyd-deploy tool provided by the scrapyd-client [https://github.com/scrapy/scrapyd-client] package. Please refer to the scrapyd-deploy documentation [https://scrapyd.readthedocs.io/en/latest/deploy.html] for more information.

Scrapyd is maintained by some of the Scrapy developers.

Deploying to Scrapy Cloud

Scrapy Cloud [https://scrapinghub.com/scrapy-cloud] is a hosted, cloud-based service by Scrapinghub [https://scrapinghub.com/], the company behind Scrapy.

Scrapy Cloud removes the need to setup and monitor servers and provides a nice UI to manage spiders and review scraped items, logs and stats.

To deploy spiders to Scrapy Cloud you can use the shub [https://doc.scrapinghub.com/shub.html] command line tool. Please refer to the Scrapy Cloud documentation [https://doc.scrapinghub.com/scrapy-cloud.html] for more information.

Scrapy Cloud is compatible with Scrapyd and one can switch between them as needed - the configuration is read from the scrapy.cfg file just like scrapyd-deploy.

AutoThrottle extension

This is an extension for automatically throttling crawling speed based on load of both the Scrapy server and the website you are crawling.

Design goals

be nicer to sites instead of using default download delay of zero

automatically adjust scrapy to the optimum crawling speed, so the user doesn’t have to tune the download delays to find the optimum one. The user only needs to specify the maximum concurrent requests it allows, and the extension does the rest.

How it works

AutoThrottle extension adjusts download delays dynamically to make spider send AUTOTHROTTLE_TARGET_CONCURRENCY concurrent requests on average to each remote website.

It uses download latency to compute the delays. The main idea is the following: if a server needs latency seconds to respond, a client should send a request each latency/N seconds to have N requests processed in parallel.

Instead of adjusting the delays one can just set a small fixed download delay and impose hard limits on concurrency using CONCURRENT_REQUESTS_PER_DOMAIN or CONCURRENT_REQUESTS_PER_IP options. It will provide a similar effect, but there are some important differences:

because the download delay is small there will be occasional bursts of requests;

often non-200 (error) responses can be returned faster than regular responses, so with a small download delay and a hard concurrency limit crawler will be sending requests to server faster when server starts to return errors. But this is an opposite of what crawler should do - in case of errors it makes more sense to slow down: these errors may be caused by the high request rate.

AutoThrottle doesn’t have these issues.

Throttling algorithm

AutoThrottle algorithm adjusts download delays based on the following rules:

spiders always start with a download delay of AUTOTHROTTLE_START_DELAY;

when a response is received, the target download delay is calculated as latency / N where latency is a latency of the response, and N is AUTOTHROTTLE_TARGET_CONCURRENCY.

download delay for next requests is set to the average of previous download delay and the target download delay;

latencies of non-200 responses are not allowed to decrease the delay;

download delay can’t become less than DOWNLOAD_DELAY or greater than AUTOTHROTTLE_MAX_DELAY

Note

The AutoThrottle extension honours the standard Scrapy settings for concurrency and delay. This means that it will respect CONCURRENT_REQUESTS_PER_DOMAIN and CONCURRENT_REQUESTS_PER_IP options and never set a download delay lower than DOWNLOAD_DELAY.

In Scrapy, the download latency is measured as the time elapsed between establishing the TCP connection and receiving the HTTP headers.

Note that these latencies are very hard to measure accurately in a cooperative multitasking environment because Scrapy may be busy processing a spider callback, for example, and unable to attend downloads. However, these latencies should still give a reasonable estimate of how busy Scrapy (and ultimately, the server) is, and this extension builds on that premise.

Settings

The settings used to control the AutoThrottle extension are:

AUTOTHROTTLE_ENABLED

AUTOTHROTTLE_START_DELAY

AUTOTHROTTLE_MAX_DELAY

AUTOTHROTTLE_TARGET_CONCURRENCY

AUTOTHROTTLE_DEBUG

CONCURRENT_REQUESTS_PER_DOMAIN

CONCURRENT_REQUESTS_PER_IP

DOWNLOAD_DELAY

For more information see How it works.

AUTOTHROTTLE_ENABLED

Default: False

Enables the AutoThrottle extension.

AUTOTHROTTLE_START_DELAY

Default: 5.0

The initial download delay (in seconds).

AUTOTHROTTLE_MAX_DELAY

Default: 60.0

The maximum download delay (in seconds) to be set in case of high latencies.

AUTOTHROTTLE_TARGET_CONCURRENCY

New in version 1.1.

Default: 1.0

Average number of requests Scrapy should be sending in parallel to remote websites.

By default, AutoThrottle adjusts the delay to send a single concurrent request to each of the remote websites. Set this option to a higher value (e.g. 2.0) to increase the throughput and the load on remote servers. A lower AUTOTHROTTLE_TARGET_CONCURRENCY value (e.g. 0.5) makes the crawler more conservative and polite.

Note that CONCURRENT_REQUESTS_PER_DOMAIN and CONCURRENT_REQUESTS_PER_IP options are still respected when AutoThrottle extension is enabled. This means that if AUTOTHROTTLE_TARGET_CONCURRENCY is set to a value higher than CONCURRENT_REQUESTS_PER_DOMAIN or CONCURRENT_REQUESTS_PER_IP, the crawler won’t reach this number of concurrent requests.

At every given time point Scrapy can be sending more or less concurrent requests than AUTOTHROTTLE_TARGET_CONCURRENCY; it is a suggested value the crawler tries to approach, not a hard limit.

AUTOTHROTTLE_DEBUG

Default: False

Enable AutoThrottle debug mode which will display stats on every response received, so you can see how the throttling parameters are being adjusted in real time.

Benchmarking

New in version 0.17.

Scrapy comes with a simple benchmarking suite that spawns a local HTTP server and crawls it at the maximum possible speed. The goal of this benchmarking is to get an idea of how Scrapy performs in your hardware, in order to have a common baseline for comparisons. It uses a simple spider that does nothing and just follows links.

To run it use:

scrapy bench

You should see an output like this:

2016-12-16 21:18:48 [scrapy.utils.log] INFO: Scrapy 1.2.2 started (bot: quotesbot) 2016-12-16 21:18:48 [scrapy.utils.log] INFO: Overridden settings: {'CLOSESPIDER_TIMEOUT': 10, 'ROBOTSTXT_OBEY': True, 'SPIDER_MODULES': ['quotesbot.spiders'], 'LOGSTATS_INTERVAL': 1, 'BOT_NAME': 'quotesbot', 'LOG_LEVEL': 'INFO', 'NEWSPIDER_MODULE': 'quotesbot.spiders'} 2016-12-16 21:18:49 [scrapy.middleware] INFO: Enabled extensions: ['scrapy.extensions.closespider.CloseSpider', 'scrapy.extensions.logstats.LogStats', 'scrapy.extensions.telnet.TelnetConsole', 'scrapy.extensions.corestats.CoreStats'] 2016-12-16 21:18:49 [scrapy.middleware] INFO: Enabled downloader middlewares: ['scrapy.downloadermiddlewares.robotstxt.RobotsTxtMiddleware', 'scrapy.downloadermiddlewares.httpauth.HttpAuthMiddleware', 'scrapy.downloadermiddlewares.downloadtimeout.DownloadTimeoutMiddleware', 'scrapy.downloadermiddlewares.defaultheaders.DefaultHeadersMiddleware', 'scrapy.downloadermiddlewares.useragent.UserAgentMiddleware', 'scrapy.downloadermiddlewares.retry.RetryMiddleware', 'scrapy.downloadermiddlewares.redirect.MetaRefreshMiddleware', 'scrapy.downloadermiddlewares.httpcompression.HttpCompressionMiddleware', 'scrapy.downloadermiddlewares.redirect.RedirectMiddleware', 'scrapy.downloadermiddlewares.cookies.CookiesMiddleware', 'scrapy.downloadermiddlewares.stats.DownloaderStats'] 2016-12-16 21:18:49 [scrapy.middleware] INFO: Enabled spider middlewares: ['scrapy.spidermiddlewares.httperror.HttpErrorMiddleware', 'scrapy.spidermiddlewares.offsite.OffsiteMiddleware', 'scrapy.spidermiddlewares.referer.RefererMiddleware', 'scrapy.spidermiddlewares.urllength.UrlLengthMiddleware', 'scrapy.spidermiddlewares.depth.DepthMiddleware'] 2016-12-16 21:18:49 [scrapy.middleware] INFO: Enabled item pipelines: [] 2016-12-16 21:18:49 [scrapy.core.engine] INFO: Spider opened 2016-12-16 21:18:49 [scrapy.extensions.logstats] INFO: Crawled 0 pages (at 0 pages/min), scraped 0 items (at 0 items/min) 2016-12-16 21:18:50 [scrapy.extensions.logstats] INFO: Crawled 70 pages (at 4200 pages/min), scraped 0 items (at 0 items/min) 2016-12-16 21:18:51 [scrapy.extensions.logstats] INFO: Crawled 134 pages (at 3840 pages/min), scraped 0 items (at 0 items/min) 2016-12-16 21:18:52 [scrapy.extensions.logstats] INFO: Crawled 198 pages (at 3840 pages/min), scraped 0 items (at 0 items/min) 2016-12-16 21:18:53 [scrapy.extensions.logstats] INFO: Crawled 254 pages (at 3360 pages/min), scraped 0 items (at 0 items/min) 2016-12-16 21:18:54 [scrapy.extensions.logstats] INFO: Crawled 302 pages (at 2880 pages/min), scraped 0 items (at 0 items/min) 2016-12-16 21:18:55 [scrapy.extensions.logstats] INFO: Crawled 358 pages (at 3360 pages/min), scraped 0 items (at 0 items/min) 2016-12-16 21:18:56 [scrapy.extensions.logstats] INFO: Crawled 406 pages (at 2880 pages/min), scraped 0 items (at 0 items/min) 2016-12-16 21:18:57 [scrapy.extensions.logstats] INFO: Crawled 438 pages (at 1920 pages/min), scraped 0 items (at 0 items/min) 2016-12-16 21:18:58 [scrapy.extensions.logstats] INFO: Crawled 470 pages (at 1920 pages/min), scraped 0 items (at 0 items/min) 2016-12-16 21:18:59 [scrapy.core.engine] INFO: Closing spider (closespider_timeout) 2016-12-16 21:18:59 [scrapy.extensions.logstats] INFO: Crawled 518 pages (at 2880 pages/min), scraped 0 items (at 0 items/min) 2016-12-16 21:19:00 [scrapy.statscollectors] INFO: Dumping Scrapy stats: {'downloader/request_bytes': 229995, 'downloader/request_count': 534, 'downloader/request_method_count/GET': 534, 'downloader/response_bytes': 1565504, 'downloader/response_count': 534, 'downloader/response_status_count/200': 534, 'finish_reason': 'closespider_timeout', 'finish_time': datetime.datetime(2016, 12, 16, 16, 19, 0, 647725), 'log_count/INFO': 17, 'request_depth_max': 19, 'response_received_count': 534, 'scheduler/dequeued': 533, 'scheduler/dequeued/memory': 533, 'scheduler/enqueued': 10661, 'scheduler/enqueued/memory': 10661, 'start_time': datetime.datetime(2016, 12, 16, 16, 18, 49, 799869)} 2016-12-16 21:19:00 [scrapy.core.engine] INFO: Spider closed (closespider_timeout)

That tells you that Scrapy is able to crawl about 3000 pages per minute in the hardware where you run it. Note that this is a very simple spider intended to follow links, any custom spider you write will probably do more stuff which results in slower crawl rates. How slower depends on how much your spider does and how well it’s written.

In the future, more cases will be added to the benchmarking suite to cover other common scenarios.

Jobs: pausing and resuming crawls

Sometimes, for big sites, it’s desirable to pause crawls and be able to resume them later.

Scrapy supports this functionality out of the box by providing the following facilities:

a scheduler that persists scheduled requests on disk

a duplicates filter that persists visited requests on disk

an extension that keeps some spider state (key/value pairs) persistent between batches

Job directory

To enable persistence support you just need to define a job directory through the JOBDIR setting. This directory will be for storing all required data to keep the state of a single job (ie. a spider run). It’s important to note that this directory must not be shared by different spiders, or even different jobs/runs of the same spider, as it’s meant to be used for storing the state of a single job.

How to use it

To start a spider with persistence support enabled, run it like this:

scrapy crawl somespider -s JOBDIR=crawls/somespider-1

Then, you can stop the spider safely at any time (by pressing Ctrl-C or sending a signal), and resume it later by issuing the same command:

scrapy crawl somespider -s JOBDIR=crawls/somespider-1

Keeping persistent state between batches

Sometimes you’ll want to keep some persistent spider state between pause/resume batches. You can use the spider.state attribute for that, which should be a dict. There’s a built-in extension that takes care of serializing, storing and loading that attribute from the job directory, when the spider starts and stops.

Here’s an example of a callback that uses the spider state (other spider code is omitted for brevity):

def parse_item(self, response): # parse item here self.state['items_count'] = self.state.get('items_count', 0) + 1

Persistence gotchas

There are a few things to keep in mind if you want to be able to use the Scrapy persistence support:

Cookies expiration

Cookies may expire. So, if you don’t resume your spider quickly the requests scheduled may no longer work. This won’t be an issue if you spider doesn’t rely on cookies.

Request serialization

Requests must be serializable by the pickle module, in order for persistence to work, so you should make sure that your requests are serializable.

The most common issue here is to use lambda functions on request callbacks that can’t be persisted.

So, for example, this won’t work:

def some_callback(self, response): somearg = 'test' return scrapy.Request('http://www.example.com', callback=lambda r: self.other_callback(r, somearg)) def other_callback(self, response, somearg): print("the argument passed is: %s" % somearg)

But this will:

def some_callback(self, response): somearg = 'test' return scrapy.Request('http://www.example.com', callback=self.other_callback, cb_kwargs={'somearg': somearg}) def other_callback(self, response, somearg): print("the argument passed is: %s" % somearg)

If you wish to log the requests that couldn’t be serialized, you can set the SCHEDULER_DEBUG setting to True in the project’s settings page. It is False by default.

Architecture overview

This document describes the architecture of Scrapy and how its components interact.

Overview

The following diagram shows an overview of the Scrapy architecture with its components and an outline of the data flow that takes place inside the system (shown by the red arrows). A brief description of the components is included below with links for more detailed information about them. The data flow is also described below.

Data flow

The data flow in Scrapy is controlled by the execution engine, and goes like this:

The Engine gets the initial Requests to crawl from the Spider.

The Engine schedules the Requests in the Scheduler and asks for the next Requests to crawl.

The Scheduler returns the next Requests to the Engine.

The Engine sends the Requests to the Downloader, passing through the Downloader Middlewares (see process_request()).

Once the page finishes downloading the Downloader generates a Response (with that page) and sends it to the Engine, passing through the Downloader Middlewares (see process_response()).

The Engine receives the Response from the Downloader and sends it to the Spider for processing, passing through the Spider Middleware (see process_spider_input()).

The Spider processes the Response and returns scraped items and new Requests (to follow) to the Engine, passing through the Spider Middleware (see process_spider_output()).

The Engine sends processed items to Item Pipelines, then send processed Requests to the Scheduler and asks for possible next Requests to crawl.

The process repeats (from step 1) until there are no more requests from the Scheduler.

Components

Scrapy Engine

The engine is responsible for controlling the data flow between all components of the system, and triggering events when certain actions occur. See the Data Flow section above for more details.

Scheduler

The Scheduler receives requests from the engine and enqueues them for feeding them later (also to the engine) when the engine requests them.

Downloader

The Downloader is responsible for fetching web pages and feeding them to the engine which, in turn, feeds them to the spiders.

Spiders

Spiders are custom classes written by Scrapy users to parse responses and extract items (aka scraped items) from them or additional requests to follow. For more information see Spiders.

Item Pipeline

The Item Pipeline is responsible for processing the items once they have been extracted (or scraped) by the spiders. Typical tasks include cleansing, validation and persistence (like storing the item in a database). For more information see Item Pipeline.

Downloader middlewares

Downloader middlewares are specific hooks that sit between the Engine and the Downloader and process requests when they pass from the Engine to the Downloader, and responses that pass from Downloader to the Engine.

Use a Downloader middleware if you need to do one of the following:

process a request just before it is sent to the Downloader (i.e. right before Scrapy sends the request to the website);

change received response before passing it to a spider;

send a new Request instead of passing received response to a spider;

pass response to a spider without fetching a web page;

silently drop some requests.

For more information see Downloader Middleware.

Spider middlewares

Spider middlewares are specific hooks that sit between the Engine and the Spiders and are able to process spider input (responses) and output (items and requests).

Use a Spider middleware if you need to

post-process output of spider callbacks - change/add/remove requests or items;

post-process start_requests;

handle spider exceptions;

call errback instead of callback for some of the requests based on response content.

For more information see Spider Middleware.

Event-driven networking

Scrapy is written with Twisted [https://twistedmatrix.com/trac/], a popular event-driven networking framework for Python. Thus, it’s implemented using a non-blocking (aka asynchronous) code for concurrency.

For more information about asynchronous programming and Twisted see these links:

Introduction to Deferreds in Twisted [https://twistedmatrix.com/documents/current/core/howto/defer-intro.html]

Twisted - hello, asynchronous programming [http://jessenoller.com/blog/2009/02/11/twisted-hello-asynchronous-programming/]

Twisted Introduction - Krondo [http://krondo.com/an-introduction-to-asynchronous-programming-and-twisted/]

Downloader Middleware

The downloader middleware is a framework of hooks into Scrapy’s request/response processing. It’s a light, low-level system for globally altering Scrapy’s requests and responses.

Activating a downloader middleware

To activate a downloader middleware component, add it to the DOWNLOADER_MIDDLEWARES setting, which is a dict whose keys are the middleware class paths and their values are the middleware orders.

Here’s an example:

DOWNLOADER_MIDDLEWARES = { 'myproject.middlewares.CustomDownloaderMiddleware': 543, }

The DOWNLOADER_MIDDLEWARES setting is merged with the DOWNLOADER_MIDDLEWARES_BASE setting defined in Scrapy (and not meant to be overridden) and then sorted by order to get the final sorted list of enabled middlewares: the first middleware is the one closer to the engine and the last is the one closer to the downloader. In other words, the process_request() method of each middleware will be invoked in increasing middleware order (100, 200, 300, …) and the process_response() method of each middleware will be invoked in decreasing order.

To decide which order to assign to your middleware see the DOWNLOADER_MIDDLEWARES_BASE setting and pick a value according to where you want to insert the middleware. The order does matter because each middleware performs a different action and your middleware could depend on some previous (or subsequent) middleware being applied.

If you want to disable a built-in middleware (the ones defined in DOWNLOADER_MIDDLEWARES_BASE and enabled by default) you must define it in your project’s DOWNLOADER_MIDDLEWARES setting and assign None as its value. For example, if you want to disable the user-agent middleware:

DOWNLOADER_MIDDLEWARES = { 'myproject.middlewares.CustomDownloaderMiddleware': 543, 'scrapy.downloadermiddlewares.useragent.UserAgentMiddleware': None, }

Finally, keep in mind that some middlewares may need to be enabled through a particular setting. See each middleware documentation for more info.

Writing your own downloader middleware

Each downloader middleware is a Python class that defines one or more of the methods defined below.

The main entry point is the from_crawler class method, which receives a Crawler instance. The Crawler object gives you access, for example, to the settings.

class scrapy.downloadermiddlewares.DownloaderMiddleware

Note

Any of the downloader middleware methods may also return a deferred.

process_request(request, spider)

This method is called for each request that goes through the download middleware.

process_request() should either: return None, return a Response object, return a Request object, or raise IgnoreRequest.

If it returns None, Scrapy will continue processing this request, executing all other middlewares until, finally, the appropriate downloader handler is called the request performed (and its response downloaded).

If it returns a Response object, Scrapy won’t bother calling any other process_request() or process_exception() methods, or the appropriate download function; it’ll return that response. The process_response() methods of installed middleware is always called on every response.

If it returns a Request object, Scrapy will stop calling process_request methods and reschedule the returned request. Once the newly returned request is performed, the appropriate middleware chain will be called on the downloaded response.

If it raises an IgnoreRequest exception, the process_exception() methods of installed downloader middleware will be called. If none of them handle the exception, the errback function of the request (Request.errback) is called. If no code handles the raised exception, it is ignored and not logged (unlike other exceptions).

Parameters

request (Request object) – the request being processed

spider (Spider object) – the spider for which this request is intended

process_response(request, response, spider)

process_response() should either: return a Response object, return a Request object or raise a IgnoreRequest exception.

If it returns a Response (it could be the same given response, or a brand-new one), that response will continue to be processed with the process_response() of the next middleware in the chain.

If it returns a Request object, the middleware chain is halted and the returned request is rescheduled to be downloaded in the future. This is the same behavior as if a request is returned from process_request().

If it raises an IgnoreRequest exception, the errback function of the request (Request.errback) is called. If no code handles the raised exception, it is ignored and not logged (unlike other exceptions).

Parameters

request (is a Request object) – the request that originated the response

response (Response object) – the response being processed

spider (Spider object) – the spider for which this response is intended

process_exception(request, exception, spider)

Scrapy calls process_exception() when a download handler or a process_request() (from a downloader middleware) raises an exception (including an IgnoreRequest exception)

process_exception() should return: either None, a Response object, or a Request object.

If it returns None, Scrapy will continue processing this exception, executing any other process_exception() methods of installed middleware, until no middleware is left and the default exception handling kicks in.

If it returns a Response object, the process_response() method chain of installed middleware is started, and Scrapy won’t bother calling any other process_exception() methods of middleware.

If it returns a Request object, the returned request is rescheduled to be downloaded in the future. This stops the execution of process_exception() methods of the middleware the same as returning a response would.

Parameters

request (is a Request object) – the request that generated the exception

exception (an Exception object) – the raised exception

spider (Spider object) – the spider for which this request is intended

from_crawler(cls, crawler)

If present, this classmethod is called to create a middleware instance from a Crawler. It must return a new instance of the middleware. Crawler object provides access to all Scrapy core components like settings and signals; it is a way for middleware to access them and hook its functionality into Scrapy.

Parameters

crawler (Crawler object) – crawler that uses this middleware

Built-in downloader middleware reference

This page describes all downloader middleware components that come with Scrapy. For information on how to use them and how to write your own downloader middleware, see the downloader middleware usage guide.

For a list of the components enabled by default (and their orders) see the DOWNLOADER_MIDDLEWARES_BASE setting.

CookiesMiddleware

class scrapy.downloadermiddlewares.cookies.CookiesMiddleware

This middleware enables working with sites that require cookies, such as those that use sessions. It keeps track of cookies sent by web servers, and send them back on subsequent requests (from that spider), just like web browsers do.

The following settings can be used to configure the cookie middleware:

COOKIES_ENABLED

COOKIES_DEBUG

Multiple cookie sessions per spider

New in version 0.15.

There is support for keeping multiple cookie sessions per spider by using the cookiejar Request meta key. By default it uses a single cookie jar (session), but you can pass an identifier to use different ones.

For example:

for i, url in enumerate(urls): yield scrapy.Request(url, meta={'cookiejar': i}, callback=self.parse_page)

Keep in mind that the cookiejar meta key is not「sticky」. You need to keep passing it along on subsequent requests. For example:

def parse_page(self, response): # do some processing return scrapy.Request("http://www.example.com/otherpage", meta={'cookiejar': response.meta['cookiejar']}, callback=self.parse_other_page)

COOKIES_ENABLED

Default: True

Whether to enable the cookies middleware. If disabled, no cookies will be sent to web servers.

Notice that despite the value of COOKIES_ENABLED setting if Request.meta['dont_merge_cookies'] evaluates to True the request cookies will not be sent to the web server and received cookies in Response will not be merged with the existing cookies.

For more detailed information see the cookies parameter in Request.

COOKIES_DEBUG

Default: False

If enabled, Scrapy will log all cookies sent in requests (ie. Cookie header) and all cookies received in responses (ie. Set-Cookie header).

Here’s an example of a log with COOKIES_DEBUG enabled:

2011-04-06 14:35:10-0300 [scrapy.core.engine] INFO: Spider opened 2011-04-06 14:35:10-0300 [scrapy.downloadermiddlewares.cookies] DEBUG: Sending cookies to: <GET http://www.diningcity.com/netherlands/index.html> Cookie: clientlanguage_nl=en_EN 2011-04-06 14:35:14-0300 [scrapy.downloadermiddlewares.cookies] DEBUG: Received cookies from: <200 http://www.diningcity.com/netherlands/index.html> Set-Cookie: JSESSIONID=B~FA4DC0C496C8762AE4F1A620EAB34F38; Path=/ Set-Cookie: ip_isocode=US Set-Cookie: clientlanguage_nl=en_EN; Expires=Thu, 07-Apr-2011 21:21:34 GMT; Path=/ 2011-04-06 14:49:50-0300 [scrapy.core.engine] DEBUG: Crawled (200) <GET http://www.diningcity.com/netherlands/index.html> (referer: None) [...]

DefaultHeadersMiddleware

class scrapy.downloadermiddlewares.defaultheaders.DefaultHeadersMiddleware

This middleware sets all default requests headers specified in the DEFAULT_REQUEST_HEADERS setting.

DownloadTimeoutMiddleware

class scrapy.downloadermiddlewares.downloadtimeout.DownloadTimeoutMiddleware

This middleware sets the download timeout for requests specified in the DOWNLOAD_TIMEOUT setting or download_timeout spider attribute.

Note

You can also set download timeout per-request using download_timeout Request.meta key; this is supported even when DownloadTimeoutMiddleware is disabled.

HttpAuthMiddleware

class scrapy.downloadermiddlewares.httpauth.HttpAuthMiddleware

This middleware authenticates all requests generated from certain spiders using Basic access authentication [https://en.wikipedia.org/wiki/Basic_access_authentication] (aka. HTTP auth).

To enable HTTP authentication from certain spiders, set the http_user and http_pass attributes of those spiders.

Example:

from scrapy.spiders import CrawlSpider class SomeIntranetSiteSpider(CrawlSpider): http_user = 'someuser' http_pass = 'somepass' name = 'intranet.example.com' # .. rest of the spider code omitted ...

HttpCacheMiddleware

class scrapy.downloadermiddlewares.httpcache.HttpCacheMiddleware

This middleware provides low-level cache to all HTTP requests and responses. It has to be combined with a cache storage backend as well as a cache policy.

Scrapy ships with three HTTP cache storage backends:

Filesystem storage backend (default)

DBM storage backend

You can change the HTTP cache storage backend with the HTTPCACHE_STORAGE setting. Or you can also implement your own storage backend.

Scrapy ships with two HTTP cache policies:

RFC2616 policy

Dummy policy (default)

You can change the HTTP cache policy with the HTTPCACHE_POLICY setting. Or you can also implement your own policy.

You can also avoid caching a response on every policy using dont_cache meta key equals True.

Dummy policy (default)

class scrapy.extensions.httpcache.DummyPolicy

This policy has no awareness of any HTTP Cache-Control directives. Every request and its corresponding response are cached. When the same request is seen again, the response is returned without transferring anything from the Internet.

The Dummy policy is useful for testing spiders faster (without having to wait for downloads every time) and for trying your spider offline, when an Internet connection is not available. The goal is to be able to「replay」a spider run exactly as it ran before.

RFC2616 policy

class scrapy.extensions.httpcache.RFC2616Policy

This policy provides a RFC2616 compliant HTTP cache, i.e. with HTTP Cache-Control awareness, aimed at production and used in continuous runs to avoid downloading unmodified data (to save bandwidth and speed up crawls).

What is implemented:

Do not attempt to store responses/requests with no-store cache-control directive set

Do not serve responses from cache if no-cache cache-control directive is set even for fresh responses

Compute freshness lifetime from max-age cache-control directive

Compute freshness lifetime from Expires response header

Compute freshness lifetime from Last-Modified response header (heuristic used by Firefox)

Compute current age from Age response header

Compute current age from Date header

Revalidate stale responses based on Last-Modified response header

Revalidate stale responses based on ETag response header

Set Date header for any received response missing it

Support max-stale cache-control directive in requests

This allows spiders to be configured with the full RFC2616 cache policy, but avoid revalidation on a request-by-request basis, while remaining conformant with the HTTP spec.

Example:

Add Cache-Control: max-stale=600 to Request headers to accept responses that have exceeded their expiration time by no more than 600 seconds.

See also: RFC2616, 14.9.3

What is missing:

Pragma: no-cache support https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9.1

Vary header support https://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html#sec13.6

Invalidation after updates or deletes https://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html#sec13.10

… probably others ..

Filesystem storage backend (default)

class scrapy.extensions.httpcache.FilesystemCacheStorage

File system storage backend is available for the HTTP cache middleware.

Each request/response pair is stored in a different directory containing the following files:

request_body - the plain request body

request_headers - the request headers (in raw HTTP format)

response_body - the plain response body

response_headers - the request headers (in raw HTTP format)

meta - some metadata of this cache resource in Python repr() format (grep-friendly format)

pickled_meta - the same metadata in meta but pickled for more efficient deserialization

The directory name is made from the request fingerprint (see scrapy.utils.request.fingerprint), and one level of subdirectories is used to avoid creating too many files into the same directory (which is inefficient in many file systems). An example directory could be:

/path/to/cache/dir/example.com/72/72811f648e718090f041317756c03adb0ada46c7

DBM storage backend

class scrapy.extensions.httpcache.DbmCacheStorage

New in version 0.13.

A DBM [https://en.wikipedia.org/wiki/Dbm] storage backend is also available for the HTTP cache middleware.

By default, it uses the anydbm [https://docs.python.org/2/library/anydbm.html] module, but you can change it with the HTTPCACHE_DBM_MODULE setting.

Writing your own storage backend

You can implement a cache storage backend by creating a Python class that defines the methods described below.

class scrapy.extensions.httpcache.CacheStorage

open_spider(spider)

This method gets called after a spider has been opened for crawling. It handles the open_spider signal.

Parameters

spider (Spider object) – the spider which has been opened

close_spider(spider)

This method gets called after a spider has been closed. It handles the close_spider signal.

Parameters

spider (Spider object) – the spider which has been closed

retrieve_response(spider, request)

Return response if present in cache, or None otherwise.

Parameters

spider (Spider object) – the spider which generated the request

request (Request object) – the request to find cached response for

store_response(spider, request, response)

Store the given response in the cache.

Parameters

spider (Spider object) – the spider for which the response is intended

request (Request object) – the corresponding request the spider generated

response (Response object) – the response to store in the cache

In order to use your storage backend, set:

HTTPCACHE_STORAGE to the Python import path of your custom storage class.

HTTPCache middleware settings

The HttpCacheMiddleware can be configured through the following settings:

HTTPCACHE_ENABLED

New in version 0.11.

Default: False

Whether the HTTP cache will be enabled.

Changed in version 0.11: Before 0.11, HTTPCACHE_DIR was used to enable cache.

HTTPCACHE_EXPIRATION_SECS

Default: 0

Expiration time for cached requests, in seconds.

Cached requests older than this time will be re-downloaded. If zero, cached requests will never expire.

Changed in version 0.11: Before 0.11, zero meant cached requests always expire.

HTTPCACHE_DIR

Default: 'httpcache'

The directory to use for storing the (low-level) HTTP cache. If empty, the HTTP cache will be disabled. If a relative path is given, is taken relative to the project data dir. For more info see: Default structure of Scrapy projects.

HTTPCACHE_IGNORE_HTTP_CODES

New in version 0.10.

Default: []

Don’t cache response with these HTTP codes.

HTTPCACHE_IGNORE_MISSING

Default: False

If enabled, requests not found in the cache will be ignored instead of downloaded.

HTTPCACHE_IGNORE_SCHEMES

New in version 0.10.

Default: ['file']

Don’t cache responses with these URI schemes.

HTTPCACHE_STORAGE

Default: 'scrapy.extensions.httpcache.FilesystemCacheStorage'

The class which implements the cache storage backend.

HTTPCACHE_DBM_MODULE

New in version 0.13.

Default: 'anydbm'

The database module to use in the DBM storage backend. This setting is specific to the DBM backend.

HTTPCACHE_POLICY

New in version 0.18.

Default: 'scrapy.extensions.httpcache.DummyPolicy'

The class which implements the cache policy.

HTTPCACHE_GZIP

New in version 1.0.

Default: False

If enabled, will compress all cached data with gzip. This setting is specific to the Filesystem backend.

HTTPCACHE_ALWAYS_STORE

New in version 1.1.

Default: False

If enabled, will cache pages unconditionally.

A spider may wish to have all responses available in the cache, for future use with Cache-Control: max-stale, for instance. The DummyPolicy caches all responses but never revalidates them, and sometimes a more nuanced policy is desirable.

This setting still respects Cache-Control: no-store directives in responses. If you don’t want that, filter no-store out of the Cache-Control headers in responses you feedto the cache middleware.

HTTPCACHE_IGNORE_RESPONSE_CACHE_CONTROLS

New in version 1.1.

Default: []

List of Cache-Control directives in responses to be ignored.

Sites often set「no-store」,「no-cache」,「must-revalidate」, etc., but get upset at the traffic a spider can generate if it respects those directives. This allows to selectively ignore Cache-Control directives that are known to be unimportant for the sites being crawled.

We assume that the spider will not issue Cache-Control directives in requests unless it actually needs them, so directives in requests are not filtered.

HttpCompressionMiddleware

class scrapy.downloadermiddlewares.httpcompression.HttpCompressionMiddleware

This middleware allows compressed (gzip, deflate) traffic to be sent/received from web sites.

This middleware also supports decoding brotli-compressed [https://www.ietf.org/rfc/rfc7932.txt] responses, provided brotlipy [https://pypi.python.org/pypi/brotlipy] is installed.

HttpCompressionMiddleware Settings

COMPRESSION_ENABLED

Default: True

Whether the Compression middleware will be enabled.

HttpProxyMiddleware

New in version 0.8.

class scrapy.downloadermiddlewares.httpproxy.HttpProxyMiddleware

This middleware sets the HTTP proxy to use for requests, by setting the proxy meta value for Request objects.

Like the Python standard library modules urllib [https://docs.python.org/2/library/urllib.html] and urllib2 [https://docs.python.org/2/library/urllib2.html], it obeys the following environment variables:

http_proxy

https_proxy

no_proxy

You can also set the meta key proxy per-request, to a value like http://some_proxy_server:port or http://username:password@some_proxy_server:port. Keep in mind this value will take precedence over http_proxy/https_proxy environment variables, and it will also ignore no_proxy environment variable.

RedirectMiddleware

class scrapy.downloadermiddlewares.redirect.RedirectMiddleware

This middleware handles redirection of requests based on response status.

The urls which the request goes through (while being redirected) can be found in the redirect_urls Request.meta key.

The reason behind each redirect in redirect_urls can be found in the redirect_reasons Request.meta key. For example: [301, 302, 307, 'meta refresh'].

The format of a reason depends on the middleware that handled the corresponding redirect. For example, RedirectMiddleware indicates the triggering response status code as an integer, while MetaRefreshMiddleware always uses the 'meta refresh' string as reason.

The RedirectMiddleware can be configured through the following settings (see the settings documentation for more info):

REDIRECT_ENABLED

REDIRECT_MAX_TIMES

If Request.meta has dont_redirect key set to True, the request will be ignored by this middleware.

If you want to handle some redirect status codes in your spider, you can specify these in the handle_httpstatus_list spider attribute.

For example, if you want the redirect middleware to ignore 301 and 302 responses (and pass them through to your spider) you can do this:

class MySpider(CrawlSpider): handle_httpstatus_list = [301, 302]

The handle_httpstatus_list key of Request.meta can also be used to specify which response codes to allow on a per-request basis. You can also set the meta key handle_httpstatus_all to True if you want to allow any response code for a request.

RedirectMiddleware settings

REDIRECT_ENABLED

New in version 0.13.

Default: True

Whether the Redirect middleware will be enabled.

REDIRECT_MAX_TIMES

Default: 20

The maximum number of redirections that will be followed for a single request.

MetaRefreshMiddleware

class scrapy.downloadermiddlewares.redirect.MetaRefreshMiddleware

This middleware handles redirection of requests based on meta-refresh html tag.

The MetaRefreshMiddleware can be configured through the following settings (see the settings documentation for more info):

METAREFRESH_ENABLED

METAREFRESH_IGNORE_TAGS

METAREFRESH_MAXDELAY

This middleware obey REDIRECT_MAX_TIMES setting, dont_redirect, redirect_urls and redirect_reasons request meta keys as described for RedirectMiddleware

MetaRefreshMiddleware settings

METAREFRESH_ENABLED

New in version 0.17.

Default: True

Whether the Meta Refresh middleware will be enabled.

METAREFRESH_IGNORE_TAGS

Default: ['script', 'noscript']

Meta tags within these tags are ignored.

METAREFRESH_MAXDELAY

Default: 100

The maximum meta-refresh delay (in seconds) to follow the redirection. Some sites use meta-refresh for redirecting to a session expired page, so we restrict automatic redirection to the maximum delay.

RetryMiddleware

class scrapy.downloadermiddlewares.retry.RetryMiddleware

A middleware to retry failed requests that are potentially caused by temporary problems such as a connection timeout or HTTP 500 error.

Failed pages are collected on the scraping process and rescheduled at the end, once the spider has finished crawling all regular (non failed) pages.

The RetryMiddleware can be configured through the following settings (see the settings documentation for more info):

RETRY_ENABLED

RETRY_TIMES

RETRY_HTTP_CODES

If Request.meta has dont_retry key set to True, the request will be ignored by this middleware.

RetryMiddleware Settings

RETRY_ENABLED

New in version 0.13.

Default: True

Whether the Retry middleware will be enabled.

RETRY_TIMES

Default: 2

Maximum number of times to retry, in addition to the first download.

Maximum number of retries can also be specified per-request using max_retry_times attribute of Request.meta. When initialized, the max_retry_times meta key takes higher precedence over the RETRY_TIMES setting.

RETRY_HTTP_CODES

Default: [500, 502, 503, 504, 522, 524, 408, 429]

Which HTTP response codes to retry. Other errors (DNS lookup issues, connections lost, etc) are always retried.

In some cases you may want to add 400 to RETRY_HTTP_CODES because it is a common code used to indicate server overload. It is not included by default because HTTP specs say so.

RobotsTxtMiddleware

class scrapy.downloadermiddlewares.robotstxt.RobotsTxtMiddleware

This middleware filters out requests forbidden by the robots.txt exclusion standard.

To make sure Scrapy respects robots.txt make sure the middleware is enabled and the ROBOTSTXT_OBEY setting is enabled.

The ROBOTSTXT_USER_AGENT setting can be used to specify the user agent string to use for matching in the robots.txt [http://www.robotstxt.org/] file. If it is None, the User-Agent header you are sending with the request or the USER_AGENT setting (in that order) will be used for determining the user agent to use in the robots.txt [http://www.robotstxt.org/] file.

This middleware has to be combined with a robots.txt [http://www.robotstxt.org/] parser.

Scrapy ships with support for the following robots.txt [http://www.robotstxt.org/] parsers:

Protego (default)

RobotFileParser

Reppy

Robotexclusionrulesparser

You can change the robots.txt [http://www.robotstxt.org/] parser with the ROBOTSTXT_PARSER setting. Or you can also implement support for a new parser.

If Request.meta has dont_obey_robotstxt key set to True the request will be ignored by this middleware even if ROBOTSTXT_OBEY is enabled.

Parsers vary in several aspects:

Language of implementation

Supported specification

Support for wildcard matching

Usage of length based rule [https://developers.google.com/search/reference/robots_txt#order-of-precedence-for-group-member-lines]: in particular for Allow and Disallow directives, where the most specific rule based on the length of the path trumps the less specific (shorter) rule

Performance comparison of different parsers is available at the following link [https://anubhavp28.github.io/gsoc-weekly-checkin-12/].

Protego parser

Based on Protego [https://github.com/scrapy/protego]:

implemented in Python

is compliant with Google’s Robots.txt Specification [https://developers.google.com/search/reference/robots_txt]

supports wildcard matching

uses the length based rule

Scrapy uses this parser by default.

RobotFileParser

Based on RobotFileParser [https://docs.python.org/3.7/library/urllib.robotparser.html]:

is Python’s built-in robots.txt [http://www.robotstxt.org/] parser

is compliant with Martijn Koster’s 1996 draft specification [http://www.robotstxt.org/norobots-rfc.txt]

lacks support for wildcard matching

doesn’t use the length based rule

It is faster than Protego and backward-compatible with versions of Scrapy before 1.8.0.

In order to use this parser, set:

ROBOTSTXT_PARSER to scrapy.robotstxt.PythonRobotParser

Reppy parser

Based on Reppy [https://github.com/seomoz/reppy/]:

is a Python wrapper around Robots Exclusion Protocol Parser for C++ [https://github.com/seomoz/rep-cpp]

is compliant with Martijn Koster’s 1996 draft specification [http://www.robotstxt.org/norobots-rfc.txt]

supports wildcard matching

uses the length based rule

Native implementation, provides better speed than Protego.

In order to use this parser:

Install Reppy [https://github.com/seomoz/reppy/] by running pip install reppy

Set ROBOTSTXT_PARSER setting to scrapy.robotstxt.ReppyRobotParser

Robotexclusionrulesparser

Based on Robotexclusionrulesparser [http://nikitathespider.com/python/rerp/]:

implemented in Python

is compliant with Martijn Koster’s 1996 draft specification [http://www.robotstxt.org/norobots-rfc.txt]

supports wildcard matching

doesn’t use the length based rule

In order to use this parser:

Install Robotexclusionrulesparser [http://nikitathespider.com/python/rerp/] by running pip install robotexclusionrulesparser

Set ROBOTSTXT_PARSER setting to scrapy.robotstxt.RerpRobotParser

Implementing support for a new parser

You can implement support for a new robots.txt [http://www.robotstxt.org/] parser by subclassing the abstract base class RobotParser and implementing the methods described below.

class scrapy.robotstxt.RobotParser

allowed(url, user_agent)

Return True if user_agent is allowed to crawl url, otherwise return False.

Parameters

url (string) – Absolute URL

user_agent (string) – User agent

classmethod from_crawler(crawler, robotstxt_body)

Parse the content of a robots.txt [http://www.robotstxt.org/] file as bytes. This must be a class method. It must return a new instance of the parser backend.

Parameters

crawler (Crawler instance) – crawler which made the request

robotstxt_body (bytes [https://docs.python.org/3/library/stdtypes.html#bytes]) – content of a robots.txt [http://www.robotstxt.org/] file.

DownloaderStats

class scrapy.downloadermiddlewares.stats.DownloaderStats

Middleware that stores stats of all requests, responses and exceptions that pass through it.

To use this middleware you must enable the DOWNLOADER_STATS setting.

UserAgentMiddleware

class scrapy.downloadermiddlewares.useragent.UserAgentMiddleware

Middleware that allows spiders to override the default user agent.

In order for a spider to override the default user agent, its user_agent attribute must be set.

AjaxCrawlMiddleware

class scrapy.downloadermiddlewares.ajaxcrawl.AjaxCrawlMiddleware

Middleware that finds ‘AJAX crawlable’ page variants based on meta-fragment html tag. See https://developers.google.com/webmasters/ajax-crawling/docs/getting-started for more info.

Note

Scrapy finds ‘AJAX crawlable’ pages for URLs like 'http://example.com/!#foo=bar' even without this middleware. AjaxCrawlMiddleware is necessary when URL doesn’t contain '!#'. This is often a case for ‘index’ or ‘main’ website pages.

AjaxCrawlMiddleware Settings

AJAXCRAWL_ENABLED

New in version 0.21.

Default: False

Whether the AjaxCrawlMiddleware will be enabled. You may want to enable it for broad crawls.

HttpProxyMiddleware settings

HTTPPROXY_ENABLED

Default: True

Whether or not to enable the HttpProxyMiddleware.

HTTPPROXY_AUTH_ENCODING

Default: "latin-1"

The default encoding for proxy authentication on HttpProxyMiddleware.

Spider Middleware

The spider middleware is a framework of hooks into Scrapy’s spider processing mechanism where you can plug custom functionality to process the responses that are sent to Spiders for processing and to process the requests and items that are generated from spiders.

Activating a spider middleware

To activate a spider middleware component, add it to the SPIDER_MIDDLEWARES setting, which is a dict whose keys are the middleware class path and their values are the middleware orders.

Here’s an example:

SPIDER_MIDDLEWARES = { 'myproject.middlewares.CustomSpiderMiddleware': 543, }

The SPIDER_MIDDLEWARES setting is merged with the SPIDER_MIDDLEWARES_BASE setting defined in Scrapy (and not meant to be overridden) and then sorted by order to get the final sorted list of enabled middlewares: the first middleware is the one closer to the engine and the last is the one closer to the spider. In other words, the process_spider_input() method of each middleware will be invoked in increasing middleware order (100, 200, 300, …), and the process_spider_output() method of each middleware will be invoked in decreasing order.

To decide which order to assign to your middleware see the SPIDER_MIDDLEWARES_BASE setting and pick a value according to where you want to insert the middleware. The order does matter because each middleware performs a different action and your middleware could depend on some previous (or subsequent) middleware being applied.

If you want to disable a builtin middleware (the ones defined in SPIDER_MIDDLEWARES_BASE, and enabled by default) you must define it in your project SPIDER_MIDDLEWARES setting and assign None as its value. For example, if you want to disable the off-site middleware:

SPIDER_MIDDLEWARES = { 'myproject.middlewares.CustomSpiderMiddleware': 543, 'scrapy.spidermiddlewares.offsite.OffsiteMiddleware': None, }

Finally, keep in mind that some middlewares may need to be enabled through a particular setting. See each middleware documentation for more info.

Writing your own spider middleware

Each spider middleware is a Python class that defines one or more of the methods defined below.

The main entry point is the from_crawler class method, which receives a Crawler instance. The Crawler object gives you access, for example, to the settings.

class scrapy.spidermiddlewares.SpiderMiddleware

process_spider_input(response, spider)

This method is called for each response that goes through the spider middleware and into the spider, for processing.

process_spider_input() should return None or raise an exception.

If it returns None, Scrapy will continue processing this response, executing all other middlewares until, finally, the response is handed to the spider for processing.

If it raises an exception, Scrapy won’t bother calling any other spider middleware process_spider_input() and will call the request errback if there is one, otherwise it will start the process_spider_exception() chain. The output of the errback is chained back in the other direction for process_spider_output() to process it, or process_spider_exception() if it raised an exception.

Parameters

response (Response object) – the response being processed

spider (Spider object) – the spider for which this response is intended

process_spider_output(response, result, spider)

This method is called with the results returned from the Spider, after it has processed the response.

process_spider_output() must return an iterable of Request, dict or Item objects.

Parameters

response (Response object) – the response which generated this output from the spider

result (an iterable of Request, dict or Item objects) – the result returned by the spider

spider (Spider object) – the spider whose result is being processed

process_spider_exception(response, exception, spider)

This method is called when a spider or process_spider_output() method (from a previous spider middleware) raises an exception.

process_spider_exception() should return either None or an iterable of Request, dict or Item objects.

If it returns None, Scrapy will continue processing this exception, executing any other process_spider_exception() in the following middleware components, until no middleware components are left and the exception reaches the engine (where it’s logged and discarded).

If it returns an iterable the process_spider_output() pipeline kicks in, starting from the next spider middleware, and no other process_spider_exception() will be called.

Parameters

response (Response object) – the response being processed when the exception was raised

exception (Exception [https://docs.python.org/2/library/exceptions.html#exceptions.Exception] object) – the exception raised

spider (Spider object) – the spider which raised the exception

process_start_requests(start_requests, spider)

New in version 0.15.

This method is called with the start requests of the spider, and works similarly to the process_spider_output() method, except that it doesn’t have a response associated and must return only requests (not items).

It receives an iterable (in the start_requests parameter) and must return another iterable of Request objects.

Note

When implementing this method in your spider middleware, you should always return an iterable (that follows the input one) and not consume all start_requests iterator because it can be very large (or even unbounded) and cause a memory overflow. The Scrapy engine is designed to pull start requests while it has capacity to process them, so the start requests iterator can be effectively endless where there is some other condition for stopping the spider (like a time limit or item/page count).

Parameters

start_requests (an iterable of Request) – the start requests

spider (Spider object) – the spider to whom the start requests belong

from_crawler(cls, crawler)

If present, this classmethod is called to create a middleware instance from a Crawler. It must return a new instance of the middleware. Crawler object provides access to all Scrapy core components like settings and signals; it is a way for middleware to access them and hook its functionality into Scrapy.

Parameters

crawler (Crawler object) – crawler that uses this middleware

Built-in spider middleware reference

This page describes all spider middleware components that come with Scrapy. For information on how to use them and how to write your own spider middleware, see the spider middleware usage guide.

For a list of the components enabled by default (and their orders) see the SPIDER_MIDDLEWARES_BASE setting.

DepthMiddleware

class scrapy.spidermiddlewares.depth.DepthMiddleware

DepthMiddleware is used for tracking the depth of each Request inside the site being scraped. It works by setting request.meta['depth'] = 0 whenever there is no value previously set (usually just the first Request) and incrementing it by 1 otherwise.

It can be used to limit the maximum depth to scrape, control Request priority based on their depth, and things like that.

The DepthMiddleware can be configured through the following settings (see the settings documentation for more info):

DEPTH_LIMIT - The maximum depth that will be allowed to crawl for any site. If zero, no limit will be imposed.

DEPTH_STATS_VERBOSE - Whether to collect the number of requests for each depth.

DEPTH_PRIORITY - Whether to prioritize the requests based on their depth.

HttpErrorMiddleware

class scrapy.spidermiddlewares.httperror.HttpErrorMiddleware

Filter out unsuccessful (erroneous) HTTP responses so that spiders don’t have to deal with them, which (most of the time) imposes an overhead, consumes more resources, and makes the spider logic more complex.

According to the HTTP standard [https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html], successful responses are those whose status codes are in the 200-300 range.

If you still want to process response codes outside that range, you can specify which response codes the spider is able to handle using the handle_httpstatus_list spider attribute or HTTPERROR_ALLOWED_CODES setting.

For example, if you want your spider to handle 404 responses you can do this:

class MySpider(CrawlSpider): handle_httpstatus_list = [404]

The handle_httpstatus_list key of Request.meta can also be used to specify which response codes to allow on a per-request basis. You can also set the meta key handle_httpstatus_all to True if you want to allow any response code for a request.

Keep in mind, however, that it’s usually a bad idea to handle non-200 responses, unless you really know what you’re doing.

For more information see: HTTP Status Code Definitions [https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html].

HttpErrorMiddleware settings

HTTPERROR_ALLOWED_CODES

Default: []

Pass all responses with non-200 status codes contained in this list.

HTTPERROR_ALLOW_ALL

Default: False

Pass all responses, regardless of its status code.

OffsiteMiddleware

class scrapy.spidermiddlewares.offsite.OffsiteMiddleware

Filters out Requests for URLs outside the domains covered by the spider.

This middleware filters out every request whose host names aren’t in the spider’s allowed_domains attribute. All subdomains of any domain in the list are also allowed. E.g. the rule www.example.org will also allow bob.www.example.org but not www2.example.com nor example.com.

When your spider returns a request for a domain not belonging to those covered by the spider, this middleware will log a debug message similar to this one:

DEBUG: Filtered offsite request to 'www.othersite.com': <GET http://www.othersite.com/some/page.html>

To avoid filling the log with too much noise, it will only print one of these messages for each new domain filtered. So, for example, if another request for www.othersite.com is filtered, no log message will be printed. But if a request for someothersite.com is filtered, a message will be printed (but only for the first request filtered).

If the spider doesn’t define an allowed_domains attribute, or the attribute is empty, the offsite middleware will allow all requests.

If the request has the dont_filter attribute set, the offsite middleware will allow the request even if its domain is not listed in allowed domains.

RefererMiddleware

class scrapy.spidermiddlewares.referer.RefererMiddleware

Populates Request Referer header, based on the URL of the Response which generated it.

RefererMiddleware settings

REFERER_ENABLED

New in version 0.15.

Default: True

Whether to enable referer middleware.

REFERRER_POLICY

New in version 1.4.

Default: 'scrapy.spidermiddlewares.referer.DefaultReferrerPolicy'

Referrer Policy [https://www.w3.org/TR/referrer-policy] to apply when populating Request「Referer」header.

Note

You can also set the Referrer Policy per request, using the special "referrer_policy" Request.meta key, with the same acceptable values as for the REFERRER_POLICY setting.

Acceptable values for REFERRER_POLICY

either a path to a scrapy.spidermiddlewares.referer.ReferrerPolicy subclass — a custom policy or one of the built-in ones (see classes below),

or one of the standard W3C-defined string values,

or the special "scrapy-default".

String value

Class name (as a string)

"scrapy-default" (default)

scrapy.spidermiddlewares.referer.DefaultReferrerPolicy

「no-referrer」

scrapy.spidermiddlewares.referer.NoReferrerPolicy

「no-referrer-when-downgrade」

scrapy.spidermiddlewares.referer.NoReferrerWhenDowngradePolicy

「same-origin」

scrapy.spidermiddlewares.referer.SameOriginPolicy

「origin」

scrapy.spidermiddlewares.referer.OriginPolicy

「strict-origin」

scrapy.spidermiddlewares.referer.StrictOriginPolicy

「origin-when-cross-origin」

scrapy.spidermiddlewares.referer.OriginWhenCrossOriginPolicy

「strict-origin-when-cross-origin」

scrapy.spidermiddlewares.referer.StrictOriginWhenCrossOriginPolicy

「unsafe-url」

scrapy.spidermiddlewares.referer.UnsafeUrlPolicy

class scrapy.spidermiddlewares.referer.DefaultReferrerPolicy

A variant of「no-referrer-when-downgrade」, with the addition that「Referer」is not sent if the parent request was using file:// or s3:// scheme.

Warning

Scrapy’s default referrer policy — just like「no-referrer-when-downgrade」[https://www.w3.org/TR/referrer-policy/#referrer-policy-no-referrer-when-downgrade], the W3C-recommended value for browsers — will send a non-empty「Referer」header from any http(s):// to any https:// URL, even if the domain is different.

「same-origin」[https://www.w3.org/TR/referrer-policy/#referrer-policy-same-origin] may be a better choice if you want to remove referrer information for cross-domain requests.

class scrapy.spidermiddlewares.referer.NoReferrerPolicy

https://www.w3.org/TR/referrer-policy/#referrer-policy-no-referrer

The simplest policy is「no-referrer」, which specifies that no referrer information is to be sent along with requests made from a particular request client to any origin. The header will be omitted entirely.

class scrapy.spidermiddlewares.referer.NoReferrerWhenDowngradePolicy

https://www.w3.org/TR/referrer-policy/#referrer-policy-no-referrer-when-downgrade

The「no-referrer-when-downgrade」policy sends a full URL along with requests from a TLS-protected environment settings object to a potentially trustworthy URL, and requests from clients which are not TLS-protected to any origin.

Requests from TLS-protected clients to non-potentially trustworthy URLs, on the other hand, will contain no referrer information. A Referer HTTP header will not be sent.

This is a user agent’s default behavior, if no policy is otherwise specified.

Note

「no-referrer-when-downgrade」policy is the W3C-recommended default, and is used by major web browsers.

However, it is NOT Scrapy’s default referrer policy (see DefaultReferrerPolicy).

class scrapy.spidermiddlewares.referer.SameOriginPolicy

https://www.w3.org/TR/referrer-policy/#referrer-policy-same-origin

The「same-origin」policy specifies that a full URL, stripped for use as a referrer, is sent as referrer information when making same-origin requests from a particular request client.

Cross-origin requests, on the other hand, will contain no referrer information. A Referer HTTP header will not be sent.

class scrapy.spidermiddlewares.referer.OriginPolicy

https://www.w3.org/TR/referrer-policy/#referrer-policy-origin

The「origin」policy specifies that only the ASCII serialization of the origin of the request client is sent as referrer information when making both same-origin requests and cross-origin requests from a particular request client.

class scrapy.spidermiddlewares.referer.StrictOriginPolicy

https://www.w3.org/TR/referrer-policy/#referrer-policy-strict-origin

The「strict-origin」policy sends the ASCII serialization of the origin of the request client when making requests: - from a TLS-protected environment settings object to a potentially trustworthy URL, and - from non-TLS-protected environment settings objects to any origin.

Requests from TLS-protected request clients to non- potentially trustworthy URLs, on the other hand, will contain no referrer information. A Referer HTTP header will not be sent.

class scrapy.spidermiddlewares.referer.OriginWhenCrossOriginPolicy

https://www.w3.org/TR/referrer-policy/#referrer-policy-origin-when-cross-origin

The「origin-when-cross-origin」policy specifies that a full URL, stripped for use as a referrer, is sent as referrer information when making same-origin requests from a particular request client, and only the ASCII serialization of the origin of the request client is sent as referrer information when making cross-origin requests from a particular request client.

class scrapy.spidermiddlewares.referer.StrictOriginWhenCrossOriginPolicy

https://www.w3.org/TR/referrer-policy/#referrer-policy-strict-origin-when-cross-origin

The「strict-origin-when-cross-origin」policy specifies that a full URL, stripped for use as a referrer, is sent as referrer information when making same-origin requests from a particular request client, and only the ASCII serialization of the origin of the request client when making cross-origin requests:

from a TLS-protected environment settings object to a potentially trustworthy URL, and

from non-TLS-protected environment settings objects to any origin.

Requests from TLS-protected clients to non- potentially trustworthy URLs, on the other hand, will contain no referrer information. A Referer HTTP header will not be sent.

class scrapy.spidermiddlewares.referer.UnsafeUrlPolicy

https://www.w3.org/TR/referrer-policy/#referrer-policy-unsafe-url

The「unsafe-url」policy specifies that a full URL, stripped for use as a referrer, is sent along with both cross-origin requests and same-origin requests made from a particular request client.

Note: The policy’s name doesn’t lie; it is unsafe. This policy will leak origins and paths from TLS-protected resources to insecure origins. Carefully consider the impact of setting such a policy for potentially sensitive documents.

Warning

「unsafe-url」policy is NOT recommended.

UrlLengthMiddleware

class scrapy.spidermiddlewares.urllength.UrlLengthMiddleware

Filters out requests with URLs longer than URLLENGTH_LIMIT

The UrlLengthMiddleware can be configured through the following settings (see the settings documentation for more info):

URLLENGTH_LIMIT - The maximum URL length to allow for crawled URLs.

Extensions

The extensions framework provides a mechanism for inserting your own custom functionality into Scrapy.

Extensions are just regular classes that are instantiated at Scrapy startup, when extensions are initialized.

Extension settings

Extensions use the Scrapy settings to manage their settings, just like any other Scrapy code.

It is customary for extensions to prefix their settings with their own name, to avoid collision with existing (and future) extensions. For example, a hypothetic extension to handle Google Sitemaps [https://en.wikipedia.org/wiki/Sitemaps] would use settings like GOOGLESITEMAP_ENABLED, GOOGLESITEMAP_DEPTH, and so on.

Loading & activating extensions

Extensions are loaded and activated at startup by instantiating a single instance of the extension class. Therefore, all the extension initialization code must be performed in the class constructor (__init__ method).

To make an extension available, add it to the EXTENSIONS setting in your Scrapy settings. In EXTENSIONS, each extension is represented by a string: the full Python path to the extension’s class name. For example:

EXTENSIONS = { 'scrapy.extensions.corestats.CoreStats': 500, 'scrapy.extensions.telnet.TelnetConsole': 500, }

As you can see, the EXTENSIONS setting is a dict where the keys are the extension paths, and their values are the orders, which define the extension loading order. The EXTENSIONS setting is merged with the EXTENSIONS_BASE setting defined in Scrapy (and not meant to be overridden) and then sorted by order to get the final sorted list of enabled extensions.

As extensions typically do not depend on each other, their loading order is irrelevant in most cases. This is why the EXTENSIONS_BASE setting defines all extensions with the same order (0). However, this feature can be exploited if you need to add an extension which depends on other extensions already loaded.

Available, enabled and disabled extensions

Not all available extensions will be enabled. Some of them usually depend on a particular setting. For example, the HTTP Cache extension is available by default but disabled unless the HTTPCACHE_ENABLED setting is set.

Disabling an extension

In order to disable an extension that comes enabled by default (ie. those included in the EXTENSIONS_BASE setting) you must set its order to None. For example:

EXTENSIONS = { 'scrapy.extensions.corestats.CoreStats': None, }

Writing your own extension

Each extension is a Python class. The main entry point for a Scrapy extension (this also includes middlewares and pipelines) is the from_crawler class method which receives a Crawler instance. Through the Crawler object you can access settings, signals, stats, and also control the crawling behaviour.

Typically, extensions connect to signals and perform tasks triggered by them.

Finally, if the from_crawler method raises the NotConfigured exception, the extension will be disabled. Otherwise, the extension will be enabled.

Sample extension

Here we will implement a simple extension to illustrate the concepts described in the previous section. This extension will log a message every time:

a spider is opened

a spider is closed

a specific number of items are scraped

The extension will be enabled through the MYEXT_ENABLED setting and the number of items will be specified through the MYEXT_ITEMCOUNT setting.

Here is the code of such extension:

import logging from scrapy import signals from scrapy.exceptions import NotConfigured logger = logging.getLogger(__name__) class SpiderOpenCloseLogging(object): def __init__(self, item_count): self.item_count = item_count self.items_scraped = 0 @classmethod def from_crawler(cls, crawler): # first check if the extension should be enabled and raise # NotConfigured otherwise if not crawler.settings.getbool('MYEXT_ENABLED'): raise NotConfigured # get the number of items from settings item_count = crawler.settings.getint('MYEXT_ITEMCOUNT', 1000) # instantiate the extension object ext = cls(item_count) # connect the extension object to signals crawler.signals.connect(ext.spider_opened, signal=signals.spider_opened) crawler.signals.connect(ext.spider_closed, signal=signals.spider_closed) crawler.signals.connect(ext.item_scraped, signal=signals.item_scraped) # return the extension object return ext def spider_opened(self, spider): logger.info("opened spider %s", spider.name) def spider_closed(self, spider): logger.info("closed spider %s", spider.name) def item_scraped(self, item, spider): self.items_scraped += 1 if self.items_scraped % self.item_count == 0: logger.info("scraped %d items", self.items_scraped)

Built-in extensions reference

General purpose extensions

Log Stats extension

class scrapy.extensions.logstats.LogStats

Log basic stats like crawled pages and scraped items.

Core Stats extension

class scrapy.extensions.corestats.CoreStats

Enable the collection of core statistics, provided the stats collection is enabled (see Stats Collection).

Telnet console extension

class scrapy.extensions.telnet.TelnetConsole

Provides a telnet console for getting into a Python interpreter inside the currently running Scrapy process, which can be very useful for debugging.

The telnet console must be enabled by the TELNETCONSOLE_ENABLED setting, and the server will listen in the port specified in TELNETCONSOLE_PORT.

Memory usage extension

class scrapy.extensions.memusage.MemoryUsage

Note

This extension does not work in Windows.

Monitors the memory used by the Scrapy process that runs the spider and:

sends a notification e-mail when it exceeds a certain value

closes the spider when it exceeds a certain value

The notification e-mails can be triggered when a certain warning value is reached (MEMUSAGE_WARNING_MB) and when the maximum value is reached (MEMUSAGE_LIMIT_MB) which will also cause the spider to be closed and the Scrapy process to be terminated.

This extension is enabled by the MEMUSAGE_ENABLED setting and can be configured with the following settings:

MEMUSAGE_LIMIT_MB

MEMUSAGE_WARNING_MB

MEMUSAGE_NOTIFY_MAIL

MEMUSAGE_CHECK_INTERVAL_SECONDS

Memory debugger extension

class scrapy.extensions.memdebug.MemoryDebugger

An extension for debugging memory usage. It collects information about:

objects uncollected by the Python garbage collector

objects left alive that shouldn’t. For more info, see Debugging memory leaks with trackref

To enable this extension, turn on the MEMDEBUG_ENABLED setting. The info will be stored in the stats.

Close spider extension

class scrapy.extensions.closespider.CloseSpider

Closes a spider automatically when some conditions are met, using a specific closing reason for each condition.

The conditions for closing a spider can be configured through the following settings:

CLOSESPIDER_TIMEOUT

CLOSESPIDER_ITEMCOUNT

CLOSESPIDER_PAGECOUNT

CLOSESPIDER_ERRORCOUNT

CLOSESPIDER_TIMEOUT

Default: 0

An integer which specifies a number of seconds. If the spider remains open for more than that number of second, it will be automatically closed with the reason closespider_timeout. If zero (or non set), spiders won’t be closed by timeout.

CLOSESPIDER_ITEMCOUNT

Default: 0

An integer which specifies a number of items. If the spider scrapes more than that amount and those items are passed by the item pipeline, the spider will be closed with the reason closespider_itemcount. Requests which are currently in the downloader queue (up to CONCURRENT_REQUESTS requests) are still processed. If zero (or non set), spiders won’t be closed by number of passed items.

CLOSESPIDER_PAGECOUNT

New in version 0.11.

Default: 0

An integer which specifies the maximum number of responses to crawl. If the spider crawls more than that, the spider will be closed with the reason closespider_pagecount. If zero (or non set), spiders won’t be closed by number of crawled responses.

CLOSESPIDER_ERRORCOUNT

New in version 0.11.

Default: 0

An integer which specifies the maximum number of errors to receive before closing the spider. If the spider generates more than that number of errors, it will be closed with the reason closespider_errorcount. If zero (or non set), spiders won’t be closed by number of errors.

StatsMailer extension

class scrapy.extensions.statsmailer.StatsMailer

This simple extension can be used to send a notification e-mail every time a domain has finished scraping, including the Scrapy stats collected. The email will be sent to all recipients specified in the STATSMAILER_RCPTS setting.

Debugging extensions

Stack trace dump extension

class scrapy.extensions.debug.StackTraceDump

Dumps information about the running process when a SIGQUIT [https://en.wikipedia.org/wiki/SIGQUIT] or SIGUSR2 [https://en.wikipedia.org/wiki/SIGUSR1_and_SIGUSR2] signal is received. The information dumped is the following:

engine status (using scrapy.utils.engine.get_engine_status())

live references (see Debugging memory leaks with trackref)

stack trace of all threads

After the stack trace and engine status is dumped, the Scrapy process continues running normally.

This extension only works on POSIX-compliant platforms (ie. not Windows), because the SIGQUIT [https://en.wikipedia.org/wiki/SIGQUIT] and SIGUSR2 [https://en.wikipedia.org/wiki/SIGUSR1_and_SIGUSR2] signals are not available on Windows.

There are at least two ways to send Scrapy the SIGQUIT [https://en.wikipedia.org/wiki/SIGQUIT] signal:

By pressing Ctrl-while a Scrapy process is running (Linux only?)

By running this command (assuming <pid> is the process id of the Scrapy process):

kill -QUIT <pid>

Debugger extension

class scrapy.extensions.debug.Debugger

Invokes a Python debugger [https://docs.python.org/2/library/pdb.html] inside a running Scrapy process when a SIGUSR2 [https://en.wikipedia.org/wiki/SIGUSR1_and_SIGUSR2] signal is received. After the debugger is exited, the Scrapy process continues running normally.

For more info see Debugging in Python [https://pythonconquerstheuniverse.wordpress.com/2009/09/10/debugging-in-python/].

This extension only works on POSIX-compliant platforms (ie. not Windows).

Core API

New in version 0.15.

This section documents the Scrapy core API, and it’s intended for developers of extensions and middlewares.

Crawler API

The main entry point to Scrapy API is the Crawler object, passed to extensions through the from_crawler class method. This object provides access to all Scrapy core components, and it’s the only way for extensions to access them and hook their functionality into Scrapy.

The Extension Manager is responsible for loading and keeping track of installed extensions and it’s configured through the EXTENSIONS setting which contains a dictionary of all available extensions and their order similar to how you configure the downloader middlewares.

class scrapy.crawler.Crawler(spidercls, settings)

The Crawler object must be instantiated with a scrapy.spiders.Spider subclass and a scrapy.settings.Settings object.

settings

The settings manager of this crawler.

This is used by extensions & middlewares to access the Scrapy settings of this crawler.

For an introduction on Scrapy settings see Settings.

For the API see Settings class.

signals

The signals manager of this crawler.

This is used by extensions & middlewares to hook themselves into Scrapy functionality.

For an introduction on signals see Signals.

For the API see SignalManager class.

stats

The stats collector of this crawler.

This is used from extensions & middlewares to record stats of their behaviour, or access stats collected by other extensions.

For an introduction on stats collection see Stats Collection.

For the API see StatsCollector class.

extensions

The extension manager that keeps track of enabled extensions.

Most extensions won’t need to access this attribute.

For an introduction on extensions and a list of available extensions on Scrapy see Extensions.

engine

The execution engine, which coordinates the core crawling logic between the scheduler, downloader and spiders.

Some extension may want to access the Scrapy engine, to inspect or modify the downloader and scheduler behaviour, although this is an advanced use and this API is not yet stable.

spider

Spider currently being crawled. This is an instance of the spider class provided while constructing the crawler, and it is created after the arguments given in the crawl() method.

crawl(*args, **kwargs)

Starts the crawler by instantiating its spider class with the given args and kwargs arguments, while setting the execution engine in motion.

Returns a deferred that is fired when the crawl is finished.

stop()

Starts a graceful stop of the crawler and returns a deferred that is fired when the crawler is stopped.

class scrapy.crawler.CrawlerRunner(settings=None)

This is a convenient helper class that keeps track of, manages and runs crawlers inside an already setup Twisted reactor [https://twistedmatrix.com/documents/current/core/howto/reactor-basics.html].

The CrawlerRunner object must be instantiated with a Settings object.

This class shouldn’t be needed (since Scrapy is responsible of using it accordingly) unless writing scripts that manually handle the crawling process. See Run Scrapy from a script for an example.

crawl(crawler_or_spidercls, *args, **kwargs)

Run a crawler with the provided arguments.

It will call the given Crawler’s crawl() method, while keeping track of it so it can be stopped later.

If crawler_or_spidercls isn’t a Crawler instance, this method will try to create one using this parameter as the spider class given to it.

Returns a deferred that is fired when the crawling is finished.

Parameters

crawler_or_spidercls (Crawler instance, Spider subclass or string) – already created crawler, or a spider class or spider’s name inside the project to create it

args (list [https://docs.python.org/3/library/stdtypes.html#list]) – arguments to initialize the spider

kwargs (dict [https://docs.python.org/3/library/stdtypes.html#dict]) – keyword arguments to initialize the spider

crawlers

Set of crawlers started by crawl() and managed by this class.

create_crawler(crawler_or_spidercls)

Return a Crawler object.

If crawler_or_spidercls is a Crawler, it is returned as-is.

If crawler_or_spidercls is a Spider subclass, a new Crawler is constructed for it.

If crawler_or_spidercls is a string, this function finds a spider with this name in a Scrapy project (using spider loader), then creates a Crawler instance for it.

join()

Returns a deferred that is fired when all managed crawlers have completed their executions.

stop()

Stops simultaneously all the crawling jobs taking place.

Returns a deferred that is fired when they all have ended.

class scrapy.crawler.CrawlerProcess(settings=None, install_root_handler=True)

Bases: scrapy.crawler.CrawlerRunner

A class to run multiple scrapy crawlers in a process simultaneously.

This class extends CrawlerRunner by adding support for starting a Twisted reactor [https://twistedmatrix.com/documents/current/core/howto/reactor-basics.html] and handling shutdown signals, like the keyboard interrupt command Ctrl-C. It also configures top-level logging.

This utility should be a better fit than CrawlerRunner if you aren’t running another Twisted reactor [https://twistedmatrix.com/documents/current/core/howto/reactor-basics.html] within your application.

The CrawlerProcess object must be instantiated with a Settings object.

Parameters

install_root_handler – whether to install root logging handler (default: True)

This class shouldn’t be needed (since Scrapy is responsible of using it accordingly) unless writing scripts that manually handle the crawling process. See Run Scrapy from a script for an example.

crawl(crawler_or_spidercls, *args, **kwargs)

Run a crawler with the provided arguments.

It will call the given Crawler’s crawl() method, while keeping track of it so it can be stopped later.

If crawler_or_spidercls isn’t a Crawler instance, this method will try to create one using this parameter as the spider class given to it.

Returns a deferred that is fired when the crawling is finished.

Parameters

crawler_or_spidercls (Crawler instance, Spider subclass or string) – already created crawler, or a spider class or spider’s name inside the project to create it

args (list [https://docs.python.org/3/library/stdtypes.html#list]) – arguments to initialize the spider

kwargs (dict [https://docs.python.org/3/library/stdtypes.html#dict]) – keyword arguments to initialize the spider

crawlers

Set of crawlers started by crawl() and managed by this class.

create_crawler(crawler_or_spidercls)

Return a Crawler object.

If crawler_or_spidercls is a Crawler, it is returned as-is.

If crawler_or_spidercls is a Spider subclass, a new Crawler is constructed for it.

If crawler_or_spidercls is a string, this function finds a spider with this name in a Scrapy project (using spider loader), then creates a Crawler instance for it.

join()

Returns a deferred that is fired when all managed crawlers have completed their executions.

start(stop_after_crawl=True)

This method starts a Twisted reactor [https://twistedmatrix.com/documents/current/core/howto/reactor-basics.html], adjusts its pool size to REACTOR_THREADPOOL_MAXSIZE, and installs a DNS cache based on DNSCACHE_ENABLED and DNSCACHE_SIZE.

If stop_after_crawl is True, the reactor will be stopped after all crawlers have finished, using join().

Parameters

stop_after_crawl (boolean) – stop or not the reactor when all crawlers have finished

stop()

Stops simultaneously all the crawling jobs taking place.

Returns a deferred that is fired when they all have ended.

Settings API

scrapy.settings.SETTINGS_PRIORITIES

Dictionary that sets the key name and priority level of the default settings priorities used in Scrapy.

Each item defines a settings entry point, giving it a code name for identification and an integer priority. Greater priorities take more precedence over lesser ones when setting and retrieving values in the Settings class.

SETTINGS_PRIORITIES = { 'default': 0, 'command': 10, 'project': 20, 'spider': 30, 'cmdline': 40, }

For a detailed explanation on each settings sources, see: Settings.

scrapy.settings.get_settings_priority(priority)

Small helper function that looks up a given string priority in the SETTINGS_PRIORITIES dictionary and returns its numerical value, or directly returns a given numerical priority.

class scrapy.settings.Settings(values=None, priority='project')

Bases: scrapy.settings.BaseSettings

This object stores Scrapy settings for the configuration of internal components, and can be used for any further customization.

It is a direct subclass and supports all methods of BaseSettings. Additionally, after instantiation of this class, the new object will have the global default settings described on Built-in settings reference already populated.

class scrapy.settings.BaseSettings(values=None, priority='project')

Instances of this class behave like dictionaries, but store priorities along with their (key, value) pairs, and can be frozen (i.e. marked immutable).

Key-value entries can be passed on initialization with the values argument, and they would take the priority level (unless values is already an instance of BaseSettings, in which case the existing priority levels will be kept). If the priority argument is a string, the priority name will be looked up in SETTINGS_PRIORITIES. Otherwise, a specific integer should be provided.

Once the object is created, new settings can be loaded or updated with the set() method, and can be accessed with the square bracket notation of dictionaries, or with the get() method of the instance and its value conversion variants. When requesting a stored key, the value with the highest priority will be retrieved.

copy()

Make a deep copy of current settings.

This method returns a new instance of the Settings class, populated with the same values and their priorities.

Modifications to the new object won’t be reflected on the original settings.

copy_to_dict()

Make a copy of current settings and convert to a dict.

This method returns a new dict populated with the same values and their priorities as the current settings.

Modifications to the returned dict won’t be reflected on the original settings.

This method can be useful for example for printing settings in Scrapy shell.

freeze()

Disable further changes to the current settings.

After calling this method, the present state of the settings will become immutable. Trying to change values through the set() method and its variants won’t be possible and will be alerted.

frozencopy()

Return an immutable copy of the current settings.

Alias for a freeze() call in the object returned by copy().

get(name, default=None)

Get a setting value without affecting its original type.

Parameters

name (string) – the setting name

default (any) – the value to return if no setting is found

getbool(name, default=False)

Get a setting value as a boolean.

1, '1', True` and 'True' return True, while 0, '0', False, 'False' and None return False.

For example, settings populated through environment variables set to '0' will return False when using this method.

Parameters

name (string) – the setting name

default (any) – the value to return if no setting is found

getdict(name, default=None)

Get a setting value as a dictionary. If the setting original type is a dictionary, a copy of it will be returned. If it is a string it will be evaluated as a JSON dictionary. In the case that it is a BaseSettings instance itself, it will be converted to a dictionary, containing all its current settings values as they would be returned by get(), and losing all information about priority and mutability.

Parameters

name (string) – the setting name

default (any) – the value to return if no setting is found

getfloat(name, default=0.0)

Get a setting value as a float.

Parameters

name (string) – the setting name

default (any) – the value to return if no setting is found

getint(name, default=0)

Get a setting value as an int.

Parameters

name (string) – the setting name

default (any) – the value to return if no setting is found

getlist(name, default=None)

Get a setting value as a list. If the setting original type is a list, a copy of it will be returned. If it’s a string it will be split by「,」.

For example, settings populated through environment variables set to 'one,two' will return a list [‘one’, ‘two’] when using this method.

Parameters

name (string) – the setting name

default (any) – the value to return if no setting is found

getpriority(name)

Return the current numerical priority value of a setting, or None if the given name does not exist.

Parameters

name (string) – the setting name

getwithbase(name)

Get a composition of a dictionary-like setting and its _BASE counterpart.

Parameters

name (string) – name of the dictionary-like setting

maxpriority()

Return the numerical value of the highest priority present throughout all settings, or the numerical value for default from SETTINGS_PRIORITIES if there are no settings stored.

set(name, value, priority='project')

Store a key/value attribute with a given priority.

Settings should be populated before configuring the Crawler object (through the configure() method), otherwise they won’t have any effect.

Parameters

name (string) – the setting name

value (any) – the value to associate with the setting

priority (string or int [https://docs.python.org/3/library/functions.html#int]) – the priority of the setting. Should be a key of SETTINGS_PRIORITIES or an integer

setmodule(module, priority='project')

Store settings from a module with a given priority.

This is a helper function that calls set() for every globally declared uppercase variable of module with the provided priority.

Parameters

module (module object or string) – the module or the path of the module

priority (string or int [https://docs.python.org/3/library/functions.html#int]) – the priority of the settings. Should be a key of SETTINGS_PRIORITIES or an integer

update(values, priority='project')

Store key/value pairs with a given priority.

This is a helper function that calls set() for every item of values with the provided priority.

If values is a string, it is assumed to be JSON-encoded and parsed into a dict with json.loads() first. If it is a BaseSettings instance, the per-key priorities will be used and the priority parameter ignored. This allows inserting/updating settings with different priorities with a single command.

Parameters

values (dict or string or BaseSettings) – the settings names and values

priority (string or int [https://docs.python.org/3/library/functions.html#int]) – the priority of the settings. Should be a key of SETTINGS_PRIORITIES or an integer

SpiderLoader API

class scrapy.spiderloader.SpiderLoader

This class is in charge of retrieving and handling the spider classes defined across the project.

Custom spider loaders can be employed by specifying their path in the SPIDER_LOADER_CLASS project setting. They must fully implement the scrapy.interfaces.ISpiderLoader interface to guarantee an errorless execution.

from_settings(settings)

This class method is used by Scrapy to create an instance of the class. It’s called with the current project settings, and it loads the spiders found recursively in the modules of the SPIDER_MODULES setting.

Parameters

settings (Settings instance) – project settings

load(spider_name)

Get the Spider class with the given name. It’ll look into the previously loaded spiders for a spider class with name spider_name and will raise a KeyError if not found.

Parameters

spider_name (str [https://docs.python.org/3/library/stdtypes.html#str]) – spider class name

list()

Get the names of the available spiders in the project.

find_by_request(request)

List the spiders’ names that can handle the given request. Will try to match the request’s url against the domains of the spiders.

Parameters

request (Request instance) – queried request

Signals API

class scrapy.signalmanager.SignalManager(sender=_Anonymous)

connect(receiver, signal, **kwargs)

Connect a receiver function to a signal.

The signal can be any object, although Scrapy comes with some predefined signals that are documented in the Signals section.

Parameters

receiver (callable) – the function to be connected

signal (object [https://docs.python.org/3/library/functions.html#object]) – the signal to connect to

disconnect(receiver, signal, **kwargs)

Disconnect a receiver function from a signal. This has the opposite effect of the connect() method, and the arguments are the same.

disconnect_all(signal, **kwargs)

Disconnect all receivers from the given signal.

Parameters

signal (object [https://docs.python.org/3/library/functions.html#object]) – the signal to disconnect from

send_catch_log(signal, **kwargs)

Send a signal, catch exceptions and log them.

The keyword arguments are passed to the signal handlers (connected through the connect() method).

send_catch_log_deferred(signal, **kwargs)

Like send_catch_log() but supports returning deferreds [https://twistedmatrix.com/documents/current/core/howto/defer.html] from signal handlers.

Returns a Deferred that gets fired once all signal handlers deferreds were fired. Send a signal, catch exceptions and log them.

The keyword arguments are passed to the signal handlers (connected through the connect() method).

Stats Collector API

There are several Stats Collectors available under the scrapy.statscollectors module and they all implement the Stats Collector API defined by the StatsCollector class (which they all inherit from).

class scrapy.statscollectors.StatsCollector

get_value(key, default=None)

Return the value for the given stats key or default if it doesn’t exist.

get_stats()

Get all stats from the currently running spider as a dict.

set_value(key, value)

Set the given value for the given stats key.

set_stats(stats)

Override the current stats with the dict passed in stats argument.

inc_value(key, count=1, start=0)

Increment the value of the given stats key, by the given count, assuming the start value given (when it’s not set).

max_value(key, value)

Set the given value for the given key only if current value for the same key is lower than value. If there is no current value for the given key, the value is always set.

min_value(key, value)

Set the given value for the given key only if current value for the same key is greater than value. If there is no current value for the given key, the value is always set.

clear_stats()

Clear all stats.

The following methods are not part of the stats collection api but instead used when implementing custom stats collectors:

open_spider(spider)

Open the given spider for stats collection.

close_spider(spider)

Close the given spider. After this is called, no more specific stats can be accessed or collected.

Signals

Scrapy uses signals extensively to notify when certain events occur. You can catch some of those signals in your Scrapy project (using an extension, for example) to perform additional tasks or extend Scrapy to add functionality not provided out of the box.

Even though signals provide several arguments, the handlers that catch them don’t need to accept all of them - the signal dispatching mechanism will only deliver the arguments that the handler receives.

You can connect to signals (or send your own) through the Signals API.

Here is a simple example showing how you can catch signals and perform some action:

from scrapy import signals from scrapy import Spider class DmozSpider(Spider): name = "dmoz" allowed_domains = ["dmoz.org"] start_urls = [ "http://www.dmoz.org/Computers/Programming/Languages/Python/Books/", "http://www.dmoz.org/Computers/Programming/Languages/Python/Resources/", ] @classmethod def from_crawler(cls, crawler, *args, **kwargs): spider = super(DmozSpider, cls).from_crawler(crawler, *args, **kwargs) crawler.signals.connect(spider.spider_closed, signal=signals.spider_closed) return spider def spider_closed(self, spider): spider.logger.info('Spider closed: %s', spider.name) def parse(self, response): pass

Deferred signal handlers

Some signals support returning Twisted deferreds [https://twistedmatrix.com/documents/current/core/howto/defer.html] from their handlers, see the Built-in signals reference below to know which ones.

Built-in signals reference

Here’s the list of Scrapy built-in signals and their meaning.

engine_started

scrapy.signals.engine_started()

Sent when the Scrapy engine has started crawling.

This signal supports returning deferreds from their handlers.

Note

This signal may be fired after the spider_opened signal, depending on how the spider was started. So don’t rely on this signal getting fired before spider_opened.

engine_stopped

scrapy.signals.engine_stopped()

Sent when the Scrapy engine is stopped (for example, when a crawling process has finished).

This signal supports returning deferreds from their handlers.

item_scraped

scrapy.signals.item_scraped(item, response, spider)

Sent when an item has been scraped, after it has passed all the Item Pipeline stages (without being dropped).

This signal supports returning deferreds from their handlers.

Parameters

item (dict or Item object) – the item scraped

spider (Spider object) – the spider which scraped the item

response (Response object) – the response from where the item was scraped

item_dropped

scrapy.signals.item_dropped(item, response, exception, spider)

Sent after an item has been dropped from the Item Pipeline when some stage raised a DropItem exception.

This signal supports returning deferreds from their handlers.

Parameters

item (dict or Item object) – the item dropped from the Item Pipeline

spider (Spider object) – the spider which scraped the item

response (Response object) – the response from where the item was dropped

exception (DropItem exception) – the exception (which must be a DropItem subclass) which caused the item to be dropped

item_error

scrapy.signals.item_error(item, response, spider, failure)

Sent when a Item Pipeline generates an error (ie. raises an exception), except DropItem exception.

This signal supports returning deferreds from their handlers.

Parameters

item (dict or Item object) – the item dropped from the Item Pipeline

response (Response object) – the response being processed when the exception was raised

spider (Spider object) – the spider which raised the exception

failure (Failure [https://twistedmatrix.com/documents/current/api/twisted.python.failure.Failure.html] object) – the exception raised as a Twisted Failure [https://twistedmatrix.com/documents/current/api/twisted.python.failure.Failure.html] object

spider_closed

scrapy.signals.spider_closed(spider, reason)

Sent after a spider has been closed. This can be used to release per-spider resources reserved on spider_opened.

This signal supports returning deferreds from their handlers.

Parameters

spider (Spider object) – the spider which has been closed

reason (str [https://docs.python.org/3/library/stdtypes.html#str]) – a string which describes the reason why the spider was closed. If it was closed because the spider has completed scraping, the reason is 'finished'. Otherwise, if the spider was manually closed by calling the close_spider engine method, then the reason is the one passed in the reason argument of that method (which defaults to 'cancelled'). If the engine was shutdown (for example, by hitting Ctrl-C to stop it) the reason will be 'shutdown'.

spider_opened

scrapy.signals.spider_opened(spider)

Sent after a spider has been opened for crawling. This is typically used to reserve per-spider resources, but can be used for any task that needs to be performed when a spider is opened.

This signal supports returning deferreds from their handlers.

Parameters

spider (Spider object) – the spider which has been opened

spider_idle

scrapy.signals.spider_idle(spider)

Sent when a spider has gone idle, which means the spider has no further:

requests waiting to be downloaded

requests scheduled

items being processed in the item pipeline

If the idle state persists after all handlers of this signal have finished, the engine starts closing the spider. After the spider has finished closing, the spider_closed signal is sent.

You may raise a DontCloseSpider exception to prevent the spider from being closed.

This signal does not support returning deferreds from their handlers.

Parameters

spider (Spider object) – the spider which has gone idle

Note

Scheduling some requests in your spider_idle handler does not guarantee that it can prevent the spider from being closed, although it sometimes can. That’s because the spider may still remain idle if all the scheduled requests are rejected by the scheduler (e.g. filtered due to duplication).

spider_error

scrapy.signals.spider_error(failure, response, spider)

Sent when a spider callback generates an error (ie. raises an exception).

This signal does not support returning deferreds from their handlers.

Parameters

failure (Failure [https://twistedmatrix.com/documents/current/api/twisted.python.failure.Failure.html] object) – the exception raised as a Twisted Failure [https://twistedmatrix.com/documents/current/api/twisted.python.failure.Failure.html] object

response (Response object) – the response being processed when the exception was raised

spider (Spider object) – the spider which raised the exception

request_scheduled

scrapy.signals.request_scheduled(request, spider)

Sent when the engine schedules a Request, to be downloaded later.

The signal does not support returning deferreds from their handlers.

Parameters

request (Request object) – the request that reached the scheduler

spider (Spider object) – the spider that yielded the request

request_dropped

scrapy.signals.request_dropped(request, spider)

Sent when a Request, scheduled by the engine to be downloaded later, is rejected by the scheduler.

The signal does not support returning deferreds from their handlers.

Parameters

request (Request object) – the request that reached the scheduler

spider (Spider object) – the spider that yielded the request

request_reached_downloader

scrapy.signals.request_reached_downloader(request, spider)

Sent when a Request reached downloader.

The signal does not support returning deferreds from their handlers.

Parameters

request (Request object) – the request that reached downloader

spider (Spider object) – the spider that yielded the request

response_received

scrapy.signals.response_received(response, request, spider)

Sent when the engine receives a new Response from the downloader.

This signal does not support returning deferreds from their handlers.

Parameters

response (Response object) – the response received

request (Request object) – the request that generated the response

spider (Spider object) – the spider for which the response is intended

response_downloaded

scrapy.signals.response_downloaded(response, request, spider)

Sent by the downloader right after a HTTPResponse is downloaded.

This signal does not support returning deferreds from their handlers.

Parameters

response (Response object) – the response downloaded

request (Request object) – the request that generated the response

spider (Spider object) – the spider for which the response is intended

Item Exporters

Once you have scraped your items, you often want to persist or export those items, to use the data in some other application. That is, after all, the whole purpose of the scraping process.

For this purpose Scrapy provides a collection of Item Exporters for different output formats, such as XML, CSV or JSON.

Using Item Exporters

If you are in a hurry, and just want to use an Item Exporter to output scraped data see the Feed exports. Otherwise, if you want to know how Item Exporters work or need more custom functionality (not covered by the default exports), continue reading below.

In order to use an Item Exporter, you must instantiate it with its required args. Each Item Exporter requires different arguments, so check each exporter documentation to be sure, in Built-in Item Exporters reference. After you have instantiated your exporter, you have to:

1. call the method start_exporting() in order to signal the beginning of the exporting process

2. call the export_item() method for each item you want to export

3. and finally call the finish_exporting() to signal the end of the exporting process

Here you can see an Item Pipeline which uses multiple Item Exporters to group scraped items to different files according to the value of one of their fields:

from scrapy.exporters import XmlItemExporter class PerYearXmlExportPipeline(object): """Distribute items across multiple XML files according to their 'year' field""" def open_spider(self, spider): self.year_to_exporter = {} def close_spider(self, spider): for exporter in self.year_to_exporter.values(): exporter.finish_exporting() def _exporter_for_item(self, item): year = item['year'] if year not in self.year_to_exporter: f = open('{}.xml'.format(year), 'wb') exporter = XmlItemExporter(f) exporter.start_exporting() self.year_to_exporter[year] = exporter return self.year_to_exporter[year] def process_item(self, item, spider): exporter = self._exporter_for_item(item) exporter.export_item(item) return item

Serialization of item fields

By default, the field values are passed unmodified to the underlying serialization library, and the decision of how to serialize them is delegated to each particular serialization library.

However, you can customize how each field value is serialized before it is passed to the serialization library.

There are two ways to customize how a field will be serialized, which are described next.

1. Declaring a serializer in the field

If you use Item you can declare a serializer in the field metadata. The serializer must be a callable which receives a value and returns its serialized form.

Example:

import scrapy def serialize_price(value): return '$ %s' % str(value) class Product(scrapy.Item): name = scrapy.Field() price = scrapy.Field(serializer=serialize_price)

2. Overriding the serialize_field() method

You can also override the serialize_field() method to customize how your field value will be exported.

Make sure you call the base class serialize_field() method after your custom code.

Example:

from scrapy.exporter import XmlItemExporter class ProductXmlExporter(XmlItemExporter): def serialize_field(self, field, name, value): if field == 'price': return '$ %s' % str(value) return super(Product, self).serialize_field(field, name, value)

Built-in Item Exporters reference

Here is a list of the Item Exporters bundled with Scrapy. Some of them contain output examples, which assume you’re exporting these two items:

Item(name='Color TV', price='1200') Item(name='DVD player', price='200')

BaseItemExporter

class scrapy.exporters.BaseItemExporter(fields_to_export=None, export_empty_fields=False, encoding='utf-8', indent=0)

This is the (abstract) base class for all Item Exporters. It provides support for common features used by all (concrete) Item Exporters, such as defining what fields to export, whether to export empty fields, or which encoding to use.

These features can be configured through the constructor arguments which populate their respective instance attributes: fields_to_export, export_empty_fields, encoding, indent.

export_item(item)

Exports the given item. This method must be implemented in subclasses.

serialize_field(field, name, value)

Return the serialized value for the given field. You can override this method (in your custom Item Exporters) if you want to control how a particular field or value will be serialized/exported.

By default, this method looks for a serializer declared in the item field and returns the result of applying that serializer to the value. If no serializer is found, it returns the value unchanged except for unicode values which are encoded to str using the encoding declared in the encoding attribute.

Parameters

field (Field object or an empty dict) – the field being serialized. If a raw dict is being exported (not Item) field value is an empty dict.

name (str [https://docs.python.org/3/library/stdtypes.html#str]) – the name of the field being serialized

value – the value being serialized

start_exporting()

Signal the beginning of the exporting process. Some exporters may use this to generate some required header (for example, the XmlItemExporter). You must call this method before exporting any items.

finish_exporting()

Signal the end of the exporting process. Some exporters may use this to generate some required footer (for example, the XmlItemExporter). You must always call this method after you have no more items to export.

fields_to_export

A list with the name of the fields that will be exported, or None if you want to export all fields. Defaults to None.

Some exporters (like CsvItemExporter) respect the order of the fields defined in this attribute.

Some exporters may require fields_to_export list in order to export the data properly when spiders return dicts (not Item instances).

export_empty_fields

Whether to include empty/unpopulated item fields in the exported data. Defaults to False. Some exporters (like CsvItemExporter) ignore this attribute and always export all empty fields.

This option is ignored for dict items.

encoding

The encoding that will be used to encode unicode values. This only affects unicode values (which are always serialized to str using this encoding). Other value types are passed unchanged to the specific serialization library.

indent

Amount of spaces used to indent the output on each level. Defaults to 0.

indent=None selects the most compact representation, all items in the same line with no indentation

indent<=0 each item on its own line, no indentation

indent>0 each item on its own line, indented with the provided numeric value

PythonItemExporter

class scrapy.exporters.PythonItemExporter(**kwargs)

This is a base class for item exporters that extends BaseItemExporter with support for nested items.

It serializes items to built-in Python types, so that any serialization library (e.g. json [https://docs.python.org/3/library/json.html#module-json] or msgpack [https://pypi.org/project/msgpack/]) can be used on top of it.

XmlItemExporter

class scrapy.exporters.XmlItemExporter(file, item_element='item', root_element='items', **kwargs)

Exports Items in XML format to the specified file object.

Parameters

file – the file-like object to use for exporting the data. Its write method should accept bytes (a disk file opened in binary mode, a io.BytesIO object, etc)

root_element (str [https://docs.python.org/3/library/stdtypes.html#str]) – The name of root element in the exported XML.

item_element (str [https://docs.python.org/3/library/stdtypes.html#str]) – The name of each item element in the exported XML.

The additional keyword arguments of this constructor are passed to the BaseItemExporter constructor.

A typical output of this exporter would be:

<?xml version="1.0" encoding="utf-8"?> <items> <item> <name>Color TV</name> <price>1200</price> </item> <item> <name>DVD player</name> <price>200</price> </item> </items>

Unless overridden in the serialize_field() method, multi-valued fields are exported by serializing each value inside a <value> element. This is for convenience, as multi-valued fields are very common.

For example, the item:

Item(name=['John', 'Doe'], age='23')

Would be serialized as:

<?xml version="1.0" encoding="utf-8"?> <items> <item> <name> <value>John</value> <value>Doe</value> </name> <age>23</age> </item> </items>

CsvItemExporter

class scrapy.exporters.CsvItemExporter(file, include_headers_line=True, join_multivalued=', ', **kwargs)

Exports Items in CSV format to the given file-like object. If the fields_to_export attribute is set, it will be used to define the CSV columns and their order. The export_empty_fields attribute has no effect on this exporter.

Parameters

file – the file-like object to use for exporting the data. Its write method should accept bytes (a disk file opened in binary mode, a io.BytesIO object, etc)

include_headers_line (str [https://docs.python.org/3/library/stdtypes.html#str]) – If enabled, makes the exporter output a header line with the field names taken from BaseItemExporter.fields_to_export or the first exported item fields.

join_multivalued – The char (or chars) that will be used for joining multi-valued fields, if found.

The additional keyword arguments of this constructor are passed to the BaseItemExporter constructor, and the leftover arguments to the csv.writer [https://docs.python.org/2/library/csv.html#csv.writer] constructor, so you can use any csv.writer constructor argument to customize this exporter.

A typical output of this exporter would be:

product,price Color TV,1200 DVD player,200

PickleItemExporter

class scrapy.exporters.PickleItemExporter(file, protocol=0, **kwargs)

Exports Items in pickle format to the given file-like object.

Parameters

file – the file-like object to use for exporting the data. Its write method should accept bytes (a disk file opened in binary mode, a io.BytesIO object, etc)

protocol (int [https://docs.python.org/3/library/functions.html#int]) – The pickle protocol to use.

For more information, refer to the pickle module documentation [https://docs.python.org/2/library/pickle.html].

The additional keyword arguments of this constructor are passed to the BaseItemExporter constructor.

Pickle isn’t a human readable format, so no output examples are provided.

PprintItemExporter

class scrapy.exporters.PprintItemExporter(file, **kwargs)

Exports Items in pretty print format to the specified file object.

Parameters

file – the file-like object to use for exporting the data. Its write method should accept bytes (a disk file opened in binary mode, a io.BytesIO object, etc)

The additional keyword arguments of this constructor are passed to the BaseItemExporter constructor.

A typical output of this exporter would be:

{'name': 'Color TV', 'price': '1200'} {'name': 'DVD player', 'price': '200'}

Longer lines (when present) are pretty-formatted.

JsonItemExporter

class scrapy.exporters.JsonItemExporter(file, **kwargs)

Exports Items in JSON format to the specified file-like object, writing all objects as a list of objects. The additional constructor arguments are passed to the BaseItemExporter constructor, and the leftover arguments to the JSONEncoder [https://docs.python.org/2/library/json.html#json.JSONEncoder] constructor, so you can use any JSONEncoder [https://docs.python.org/2/library/json.html#json.JSONEncoder] constructor argument to customize this exporter.

Parameters

file – the file-like object to use for exporting the data. Its write method should accept bytes (a disk file opened in binary mode, a io.BytesIO object, etc)

A typical output of this exporter would be:

[{"name": "Color TV", "price": "1200"}, {"name": "DVD player", "price": "200"}]

Warning

JSON is very simple and flexible serialization format, but it doesn’t scale well for large amounts of data since incremental (aka. stream-mode) parsing is not well supported (if at all) among JSON parsers (on any language), and most of them just parse the entire object in memory. If you want the power and simplicity of JSON with a more stream-friendly format, consider using JsonLinesItemExporter instead, or splitting the output in multiple chunks.

JsonLinesItemExporter

class scrapy.exporters.JsonLinesItemExporter(file, **kwargs)

Exports Items in JSON format to the specified file-like object, writing one JSON-encoded item per line. The additional constructor arguments are passed to the BaseItemExporter constructor, and the leftover arguments to the JSONEncoder [https://docs.python.org/2/library/json.html#json.JSONEncoder] constructor, so you can use any JSONEncoder [https://docs.python.org/2/library/json.html#json.JSONEncoder] constructor argument to customize this exporter.

Parameters

file – the file-like object to use for exporting the data. Its write method should accept bytes (a disk file opened in binary mode, a io.BytesIO object, etc)

A typical output of this exporter would be:

{"name": "Color TV", "price": "1200"} {"name": "DVD player", "price": "200"}

Unlike the one produced by JsonItemExporter, the format produced by this exporter is well suited for serializing large amounts of data.

MarshalItemExporter

class scrapy.exporters.MarshalItemExporter(file, **kwargs)

Exports items in a Python-specific binary format (see marshal [https://docs.python.org/3/library/marshal.html#module-marshal]).

Parameters

file – The file-like object to use for exporting the data. Its write method should accept bytes [https://docs.python.org/3/library/stdtypes.html#bytes] (a disk file opened in binary mode, a BytesIO [https://docs.python.org/3/library/io.html#io.BytesIO] object, etc)

Release notes

Note

Scrapy 1.x will be the last series supporting Python 2. Scrapy 2.0, planned for Q4 2019 or Q1 2020, will support Python 3 only.

Scrapy 1.8.0 (2019-10-28)

Highlights:

Dropped Python 3.4 support and updated minimum requirements; made Python 3.8 support official

New Request.from_curl class method

New ROBOTSTXT_PARSER and ROBOTSTXT_USER_AGENT settings

New DOWNLOADER_CLIENT_TLS_CIPHERS and DOWNLOADER_CLIENT_TLS_VERBOSE_LOGGING settings

Backward-incompatible changes

Python 3.4 is no longer supported, and some of the minimum requirements of Scrapy have also changed:

cssselect [https://github.com/scrapy/cssselect/] 0.9.1

cryptography [https://cryptography.io/en/latest/] 2.0

lxml [http://lxml.de/] 3.5.0

pyOpenSSL [https://www.pyopenssl.org/en/stable/] 16.2.0

queuelib [https://github.com/scrapy/queuelib] 1.4.2

service_identity [https://service-identity.readthedocs.io/en/stable/] 16.0.0

six [https://six.readthedocs.io/] 1.10.0

Twisted [https://twistedmatrix.com/trac/] 17.9.0 (16.0.0 with Python 2)

zope.interface [https://zopeinterface.readthedocs.io/en/latest/] 4.1.3

(issue 3892 [https://github.com/scrapy/scrapy/issues/3892])

JSONRequest is now called JsonRequest for consistency with similar classes (issue 3929 [https://github.com/scrapy/scrapy/issues/3929], issue 3982 [https://github.com/scrapy/scrapy/issues/3982])

If you are using a custom context factory (DOWNLOADER_CLIENTCONTEXTFACTORY), its __init__ method must accept two new parameters: tls_verbose_logging and tls_ciphers (issue 2111 [https://github.com/scrapy/scrapy/issues/2111], issue 3392 [https://github.com/scrapy/scrapy/issues/3392], issue 3442 [https://github.com/scrapy/scrapy/issues/3442], issue 3450 [https://github.com/scrapy/scrapy/issues/3450])

ItemLoader now turns the values of its input item into lists:

>>> item = MyItem() >>> item['field'] = 'value1' >>> loader = ItemLoader(item=item) >>> item['field'] ['value1']

This is needed to allow adding values to existing fields (loader.add_value('field', 'value2')).

(issue 3804 [https://github.com/scrapy/scrapy/issues/3804], issue 3819 [https://github.com/scrapy/scrapy/issues/3819], issue 3897 [https://github.com/scrapy/scrapy/issues/3897], issue 3976 [https://github.com/scrapy/scrapy/issues/3976], issue 3998 [https://github.com/scrapy/scrapy/issues/3998], issue 4036 [https://github.com/scrapy/scrapy/issues/4036])

See also Deprecation removals below.

New features

A new Request.from_curl class method allows creating a request from a cURL command (issue 2985 [https://github.com/scrapy/scrapy/issues/2985], issue 3862 [https://github.com/scrapy/scrapy/issues/3862])

A new ROBOTSTXT_PARSER setting allows choosing which robots.txt [http://www.robotstxt.org/] parser to use. It includes built-in support for RobotFileParser, Protego (default), Reppy, and Robotexclusionrulesparser, and allows you to implement support for additional parsers (issue 754 [https://github.com/scrapy/scrapy/issues/754], issue 2669 [https://github.com/scrapy/scrapy/issues/2669], issue 3796 [https://github.com/scrapy/scrapy/issues/3796], issue 3935 [https://github.com/scrapy/scrapy/issues/3935], issue 3969 [https://github.com/scrapy/scrapy/issues/3969], issue 4006 [https://github.com/scrapy/scrapy/issues/4006])

A new ROBOTSTXT_USER_AGENT setting allows defining a separate user agent string to use for robots.txt [http://www.robotstxt.org/] parsing (issue 3931 [https://github.com/scrapy/scrapy/issues/3931], issue 3966 [https://github.com/scrapy/scrapy/issues/3966])

Rule no longer requires a LinkExtractor parameter (issue 781 [https://github.com/scrapy/scrapy/issues/781], issue 4016 [https://github.com/scrapy/scrapy/issues/4016])

Use the new DOWNLOADER_CLIENT_TLS_CIPHERS setting to customize the TLS/SSL ciphers used by the default HTTP/1.1 downloader (issue 3392 [https://github.com/scrapy/scrapy/issues/3392], issue 3442 [https://github.com/scrapy/scrapy/issues/3442])

Set the new DOWNLOADER_CLIENT_TLS_VERBOSE_LOGGING setting to True to enable debug-level messages about TLS connection parameters after establishing HTTPS connections (issue 2111 [https://github.com/scrapy/scrapy/issues/2111], issue 3450 [https://github.com/scrapy/scrapy/issues/3450])

Callbacks that receive keyword arguments (see Request.cb_kwargs) can now be tested using the new @cb_kwargs spider contract (issue 3985 [https://github.com/scrapy/scrapy/issues/3985], issue 3988 [https://github.com/scrapy/scrapy/issues/3988])

When a @scrapes spider contract fails, all missing fields are now reported (issue 766 [https://github.com/scrapy/scrapy/issues/766], issue 3939 [https://github.com/scrapy/scrapy/issues/3939])

Custom log formats can now drop messages by having the corresponding methods of the configured LOG_FORMATTER return None (issue 3984 [https://github.com/scrapy/scrapy/issues/3984], issue 3987 [https://github.com/scrapy/scrapy/issues/3987])

A much improved completion definition is now available for Zsh [https://www.zsh.org/] (issue 4069 [https://github.com/scrapy/scrapy/issues/4069])

Bug fixes

ItemLoader.load_item() no longer makes later calls to ItemLoader.get_output_value() or ItemLoader.load_item() return empty data (issue 3804 [https://github.com/scrapy/scrapy/issues/3804], issue 3819 [https://github.com/scrapy/scrapy/issues/3819], issue 3897 [https://github.com/scrapy/scrapy/issues/3897], issue 3976 [https://github.com/scrapy/scrapy/issues/3976], issue 3998 [https://github.com/scrapy/scrapy/issues/3998], issue 4036 [https://github.com/scrapy/scrapy/issues/4036])

Fixed DummyStatsCollector raising a TypeError [https://docs.python.org/3/library/exceptions.html#TypeError] exception (issue 4007 [https://github.com/scrapy/scrapy/issues/4007], issue 4052 [https://github.com/scrapy/scrapy/issues/4052])

FilesPipeline.file_path and ImagesPipeline.file_path no longer choose file extensions that are not registered with IANA [https://www.iana.org/assignments/media-types/media-types.xhtml] (issue 1287 [https://github.com/scrapy/scrapy/issues/1287], issue 3953 [https://github.com/scrapy/scrapy/issues/3953], issue 3954 [https://github.com/scrapy/scrapy/issues/3954])

When using botocore [https://github.com/boto/botocore] to persist files in S3, all botocore-supported headers are properly mapped now (issue 3904 [https://github.com/scrapy/scrapy/issues/3904], issue 3905 [https://github.com/scrapy/scrapy/issues/3905])

FTP passwords in FEED_URI containing percent-escaped characters are now properly decoded (issue 3941 [https://github.com/scrapy/scrapy/issues/3941])

A memory-handling and error-handling issue in scrapy.utils.ssl.get_temp_key_info() has been fixed (issue 3920 [https://github.com/scrapy/scrapy/issues/3920])

Documentation

The documentation now covers how to define and configure a custom log format (issue 3616 [https://github.com/scrapy/scrapy/issues/3616], issue 3660 [https://github.com/scrapy/scrapy/issues/3660])

API documentation added for MarshalItemExporter and PythonItemExporter (issue 3973 [https://github.com/scrapy/scrapy/issues/3973])

API documentation added for BaseItem and ItemMeta (issue 3999 [https://github.com/scrapy/scrapy/issues/3999])

Minor documentation fixes (issue 2998 [https://github.com/scrapy/scrapy/issues/2998], issue 3398 [https://github.com/scrapy/scrapy/issues/3398], issue 3597 [https://github.com/scrapy/scrapy/issues/3597], issue 3894 [https://github.com/scrapy/scrapy/issues/3894], issue 3934 [https://github.com/scrapy/scrapy/issues/3934], issue 3978 [https://github.com/scrapy/scrapy/issues/3978], issue 3993 [https://github.com/scrapy/scrapy/issues/3993], issue 4022 [https://github.com/scrapy/scrapy/issues/4022], issue 4028 [https://github.com/scrapy/scrapy/issues/4028], issue 4033 [https://github.com/scrapy/scrapy/issues/4033], issue 4046 [https://github.com/scrapy/scrapy/issues/4046], issue 4050 [https://github.com/scrapy/scrapy/issues/4050], issue 4055 [https://github.com/scrapy/scrapy/issues/4055], issue 4056 [https://github.com/scrapy/scrapy/issues/4056], issue 4061 [https://github.com/scrapy/scrapy/issues/4061], issue 4072 [https://github.com/scrapy/scrapy/issues/4072], issue 4071 [https://github.com/scrapy/scrapy/issues/4071], issue 4079 [https://github.com/scrapy/scrapy/issues/4079], issue 4081 [https://github.com/scrapy/scrapy/issues/4081], issue 4089 [https://github.com/scrapy/scrapy/issues/4089], issue 4093 [https://github.com/scrapy/scrapy/issues/4093])

Deprecation removals

scrapy.xlib has been removed (issue 4015 [https://github.com/scrapy/scrapy/issues/4015])

Deprecations

The LevelDB [https://github.com/google/leveldb] storage backend (scrapy.extensions.httpcache.LeveldbCacheStorage) of HttpCacheMiddleware is deprecated (issue 4085 [https://github.com/scrapy/scrapy/issues/4085], issue 4092 [https://github.com/scrapy/scrapy/issues/4092])

Use of the undocumented SCRAPY_PICKLED_SETTINGS_TO_OVERRIDE environment variable is deprecated (issue 3910 [https://github.com/scrapy/scrapy/issues/3910])

scrapy.item.DictItem is deprecated, use Item instead (issue 3999 [https://github.com/scrapy/scrapy/issues/3999])

Other changes

Minimum versions of optional Scrapy requirements that are covered by continuous integration tests have been updated:

botocore [https://github.com/boto/botocore] 1.3.23

Pillow [https://python-pillow.org/] 3.4.2

Lower versions of these optional requirements may work, but it is not guaranteed (issue 3892 [https://github.com/scrapy/scrapy/issues/3892])

GitHub templates for bug reports and feature requests (issue 3126 [https://github.com/scrapy/scrapy/issues/3126], issue 3471 [https://github.com/scrapy/scrapy/issues/3471], issue 3749 [https://github.com/scrapy/scrapy/issues/3749], issue 3754 [https://github.com/scrapy/scrapy/issues/3754])

Continuous integration fixes (issue 3923 [https://github.com/scrapy/scrapy/issues/3923])

Code cleanup (issue 3391 [https://github.com/scrapy/scrapy/issues/3391], issue 3907 [https://github.com/scrapy/scrapy/issues/3907], issue 3946 [https://github.com/scrapy/scrapy/issues/3946], issue 3950 [https://github.com/scrapy/scrapy/issues/3950], issue 4023 [https://github.com/scrapy/scrapy/issues/4023], issue 4031 [https://github.com/scrapy/scrapy/issues/4031])

Scrapy 1.7.4 (2019-10-21)

Revert the fix for issue 3804 [https://github.com/scrapy/scrapy/issues/3804] (issue 3819 [https://github.com/scrapy/scrapy/issues/3819]), which has a few undesired side effects (issue 3897 [https://github.com/scrapy/scrapy/issues/3897], issue 3976 [https://github.com/scrapy/scrapy/issues/3976]).

As a result, when an item loader is initialized with an item, ItemLoader.load_item() once again makes later calls to ItemLoader.get_output_value() or ItemLoader.load_item() return empty data.

Scrapy 1.7.3 (2019-08-01)

Enforce lxml 4.3.5 or lower for Python 3.4 (issue 3912 [https://github.com/scrapy/scrapy/issues/3912], issue 3918 [https://github.com/scrapy/scrapy/issues/3918]).

Scrapy 1.7.2 (2019-07-23)

Fix Python 2 support (issue 3889 [https://github.com/scrapy/scrapy/issues/3889], issue 3893 [https://github.com/scrapy/scrapy/issues/3893], issue 3896 [https://github.com/scrapy/scrapy/issues/3896]).

Scrapy 1.7.1 (2019-07-18)

Re-packaging of Scrapy 1.7.0, which was missing some changes in PyPI.

Scrapy 1.7.0 (2019-07-18)

Note

Make sure you install Scrapy 1.7.1. The Scrapy 1.7.0 package in PyPI is the result of an erroneous commit tagging and does not include all the changes described below.

Highlights:

Improvements for crawls targeting multiple domains

A cleaner way to pass arguments to callbacks

A new class for JSON requests

Improvements for rule-based spiders

New features for feed exports

Backward-incompatible changes

429 is now part of the RETRY_HTTP_CODES setting by default

This change is backward incompatible. If you don’t want to retry 429, you must override RETRY_HTTP_CODES accordingly.

Crawler, CrawlerRunner.crawl and CrawlerRunner.create_crawler no longer accept a Spider subclass instance, they only accept a Spider subclass now.

Spider subclass instances were never meant to work, and they were not working as one would expect: instead of using the passed Spider subclass instance, their from_crawler method was called to generate a new instance.

Non-default values for the SCHEDULER_PRIORITY_QUEUE setting may stop working. Scheduler priority queue classes now need to handle Request objects instead of arbitrary Python data structures.

See also Deprecation removals below.

New features

A new scheduler priority queue, scrapy.pqueues.DownloaderAwarePriorityQueue, may be enabled for a significant scheduling improvement on crawls targetting multiple web domains, at the cost of no CONCURRENT_REQUESTS_PER_IP support (issue 3520 [https://github.com/scrapy/scrapy/issues/3520])

A new Request.cb_kwargs attribute provides a cleaner way to pass keyword arguments to callback methods (issue 1138 [https://github.com/scrapy/scrapy/issues/1138], issue 3563 [https://github.com/scrapy/scrapy/issues/3563])

A new JSONRequest class offers a more convenient way to build JSON requests (issue 3504 [https://github.com/scrapy/scrapy/issues/3504], issue 3505 [https://github.com/scrapy/scrapy/issues/3505])

A process_request callback passed to the Rule constructor now receives the Response object that originated the request as its second argument (issue 3682 [https://github.com/scrapy/scrapy/issues/3682])

A new restrict_text parameter for the LinkExtractor constructor allows filtering links by linking text (issue 3622 [https://github.com/scrapy/scrapy/issues/3622], issue 3635 [https://github.com/scrapy/scrapy/issues/3635])

A new FEED_STORAGE_S3_ACL setting allows defining a custom ACL for feeds exported to Amazon S3 (issue 3607 [https://github.com/scrapy/scrapy/issues/3607])

A new FEED_STORAGE_FTP_ACTIVE setting allows using FTP’s active connection mode for feeds exported to FTP servers (issue 3829 [https://github.com/scrapy/scrapy/issues/3829])

A new METAREFRESH_IGNORE_TAGS setting allows overriding which HTML tags are ignored when searching a response for HTML meta tags that trigger a redirect (issue 1422 [https://github.com/scrapy/scrapy/issues/1422], issue 3768 [https://github.com/scrapy/scrapy/issues/3768])

A new redirect_reasons request meta key exposes the reason (status code, meta refresh) behind every followed redirect (issue 3581 [https://github.com/scrapy/scrapy/issues/3581], issue 3687 [https://github.com/scrapy/scrapy/issues/3687])

The SCRAPY_CHECK variable is now set to the true string during runs of the check command, which allows detecting contract check runs from code (issue 3704 [https://github.com/scrapy/scrapy/issues/3704], issue 3739 [https://github.com/scrapy/scrapy/issues/3739])

A new Item.deepcopy() method makes it easier to deep-copy items (issue 1493 [https://github.com/scrapy/scrapy/issues/1493], issue 3671 [https://github.com/scrapy/scrapy/issues/3671])

CoreStats also logs elapsed_time_seconds now (issue 3638 [https://github.com/scrapy/scrapy/issues/3638])

Exceptions from ItemLoader input and output processors are now more verbose (issue 3836 [https://github.com/scrapy/scrapy/issues/3836], issue 3840 [https://github.com/scrapy/scrapy/issues/3840])

Crawler, CrawlerRunner.crawl and CrawlerRunner.create_crawler now fail gracefully if they receive a Spider subclass instance instead of the subclass itself (issue 2283 [https://github.com/scrapy/scrapy/issues/2283], issue 3610 [https://github.com/scrapy/scrapy/issues/3610], issue 3872 [https://github.com/scrapy/scrapy/issues/3872])

Bug fixes

process_spider_exception() is now also invoked for generators (issue 220 [https://github.com/scrapy/scrapy/issues/220], issue 2061 [https://github.com/scrapy/scrapy/issues/2061])

System exceptions like KeyboardInterrupt [https://docs.python.org/library/exceptions.html#KeyboardInterrupt] are no longer caught (issue 3726 [https://github.com/scrapy/scrapy/issues/3726])

ItemLoader.load_item() no longer makes later calls to ItemLoader.get_output_value() or ItemLoader.load_item() return empty data (issue 3804 [https://github.com/scrapy/scrapy/issues/3804], issue 3819 [https://github.com/scrapy/scrapy/issues/3819])

The images pipeline (ImagesPipeline) no longer ignores these Amazon S3 settings: AWS_ENDPOINT_URL, AWS_REGION_NAME, AWS_USE_SSL, AWS_VERIFY (issue 3625 [https://github.com/scrapy/scrapy/issues/3625])

Fixed a memory leak in scrapy.pipelines.media.MediaPipeline affecting, for example, non-200 responses and exceptions from custom middlewares (issue 3813 [https://github.com/scrapy/scrapy/issues/3813])

Requests with private callbacks are now correctly unserialized from disk (issue 3790 [https://github.com/scrapy/scrapy/issues/3790])

FormRequest.from_response() now handles invalid methods like major web browsers (issue 3777 [https://github.com/scrapy/scrapy/issues/3777], issue 3794 [https://github.com/scrapy/scrapy/issues/3794])

Documentation

A new topic, Selecting dynamically-loaded content, covers recommended approaches to read dynamically-loaded data (issue 3703 [https://github.com/scrapy/scrapy/issues/3703])

Broad Crawls now features information about memory usage (issue 1264 [https://github.com/scrapy/scrapy/issues/1264], issue 3866 [https://github.com/scrapy/scrapy/issues/3866])

The documentation of Rule now covers how to access the text of a link when using CrawlSpider (issue 3711 [https://github.com/scrapy/scrapy/issues/3711], issue 3712 [https://github.com/scrapy/scrapy/issues/3712])

A new section, Writing your own storage backend, covers writing a custom cache storage backend for HttpCacheMiddleware (issue 3683 [https://github.com/scrapy/scrapy/issues/3683], issue 3692 [https://github.com/scrapy/scrapy/issues/3692])

A new FAQ entry, How to split an item into multiple items in an item pipeline?, explains what to do when you want to split an item into multiple items from an item pipeline (issue 2240 [https://github.com/scrapy/scrapy/issues/2240], issue 3672 [https://github.com/scrapy/scrapy/issues/3672])

Updated the FAQ entry about crawl order to explain why the first few requests rarely follow the desired order (issue 1739 [https://github.com/scrapy/scrapy/issues/1739], issue 3621 [https://github.com/scrapy/scrapy/issues/3621])

The LOGSTATS_INTERVAL setting (issue 3730 [https://github.com/scrapy/scrapy/issues/3730]), the FilesPipeline.file_path and ImagesPipeline.file_path methods (issue 2253 [https://github.com/scrapy/scrapy/issues/2253], issue 3609 [https://github.com/scrapy/scrapy/issues/3609]) and the Crawler.stop() method (issue 3842 [https://github.com/scrapy/scrapy/issues/3842]) are now documented

Some parts of the documentation that were confusing or misleading are now clearer (issue 1347 [https://github.com/scrapy/scrapy/issues/1347], issue 1789 [https://github.com/scrapy/scrapy/issues/1789], issue 2289 [https://github.com/scrapy/scrapy/issues/2289], issue 3069 [https://github.com/scrapy/scrapy/issues/3069], issue 3615 [https://github.com/scrapy/scrapy/issues/3615], issue 3626 [https://github.com/scrapy/scrapy/issues/3626], issue 3668 [https://github.com/scrapy/scrapy/issues/3668], issue 3670 [https://github.com/scrapy/scrapy/issues/3670], issue 3673 [https://github.com/scrapy/scrapy/issues/3673], issue 3728 [https://github.com/scrapy/scrapy/issues/3728], issue 3762 [https://github.com/scrapy/scrapy/issues/3762], issue 3861 [https://github.com/scrapy/scrapy/issues/3861], issue 3882 [https://github.com/scrapy/scrapy/issues/3882])

Minor documentation fixes (issue 3648 [https://github.com/scrapy/scrapy/issues/3648], issue 3649 [https://github.com/scrapy/scrapy/issues/3649], issue 3662 [https://github.com/scrapy/scrapy/issues/3662], issue 3674 [https://github.com/scrapy/scrapy/issues/3674], issue 3676 [https://github.com/scrapy/scrapy/issues/3676], issue 3694 [https://github.com/scrapy/scrapy/issues/3694], issue 3724 [https://github.com/scrapy/scrapy/issues/3724], issue 3764 [https://github.com/scrapy/scrapy/issues/3764], issue 3767 [https://github.com/scrapy/scrapy/issues/3767], issue 3791 [https://github.com/scrapy/scrapy/issues/3791], issue 3797 [https://github.com/scrapy/scrapy/issues/3797], issue 3806 [https://github.com/scrapy/scrapy/issues/3806], issue 3812 [https://github.com/scrapy/scrapy/issues/3812])

Deprecation removals

The following deprecated APIs have been removed (issue 3578 [https://github.com/scrapy/scrapy/issues/3578]):

scrapy.conf (use Crawler.settings)

From scrapy.core.downloader.handlers:

http.HttpDownloadHandler (use http10.HTTP10DownloadHandler)

scrapy.loader.ItemLoader._get_values (use _get_xpathvalues)

scrapy.loader.XPathItemLoader (use ItemLoader)

scrapy.log (see Logging)

From scrapy.pipelines:

files.FilesPipeline.file_key (use file_path)

images.ImagesPipeline.file_key (use file_path)

images.ImagesPipeline.image_key (use file_path)

images.ImagesPipeline.thumb_key (use thumb_path)

From both scrapy.selector and scrapy.selector.lxmlsel:

HtmlXPathSelector (use Selector)

XmlXPathSelector (use Selector)

XPathSelector (use Selector)

XPathSelectorList (use Selector)

From scrapy.selector.csstranslator:

ScrapyGenericTranslator (use parsel.csstranslator.GenericTranslator [https://parsel.readthedocs.io/en/latest/parsel.html#parsel.csstranslator.GenericTranslator])

ScrapyHTMLTranslator (use parsel.csstranslator.HTMLTranslator [https://parsel.readthedocs.io/en/latest/parsel.html#parsel.csstranslator.HTMLTranslator])

ScrapyXPathExpr (use parsel.csstranslator.XPathExpr [https://parsel.readthedocs.io/en/latest/parsel.html#parsel.csstranslator.XPathExpr])

From Selector:

_root (both the constructor argument and the object property, use root)

extract_unquoted (use getall)

select (use xpath)

From SelectorList:

extract_unquoted (use getall)

select (use xpath)

x (use xpath)

scrapy.spiders.BaseSpider (use Spider)

From Spider (and subclasses):

DOWNLOAD_DELAY (use download_delay)

set_crawler (use from_crawler())

scrapy.spiders.spiders (use SpiderLoader)

scrapy.telnet (use scrapy.extensions.telnet)

From scrapy.utils.python:

str_to_unicode (use to_unicode)

unicode_to_str (use to_bytes)

scrapy.utils.response.body_or_str

The following deprecated settings have also been removed (issue 3578 [https://github.com/scrapy/scrapy/issues/3578]):

SPIDER_MANAGER_CLASS (use SPIDER_LOADER_CLASS)

Deprecations

The queuelib.PriorityQueue value for the SCHEDULER_PRIORITY_QUEUE setting is deprecated. Use scrapy.pqueues.ScrapyPriorityQueue instead.

process_request callbacks passed to Rule that do not accept two arguments are deprecated.

The following modules are deprecated:

scrapy.utils.http (use w3lib.http [https://w3lib.readthedocs.io/en/latest/w3lib.html#module-w3lib.http])

scrapy.utils.markup (use w3lib.html [https://w3lib.readthedocs.io/en/latest/w3lib.html#module-w3lib.html])

scrapy.utils.multipart (use urllib3 [https://urllib3.readthedocs.io/en/latest/index.html])

The scrapy.utils.datatypes.MergeDict class is deprecated for Python 3 code bases. Use ChainMap [https://docs.python.org/3/library/collections.html#collections.ChainMap] instead. (issue 3878 [https://github.com/scrapy/scrapy/issues/3878])

The scrapy.utils.gz.is_gzipped function is deprecated. Use scrapy.utils.gz.gzip_magic_number instead.

Other changes

It is now possible to run all tests from the same tox [https://pypi.python.org/pypi/tox] environment in parallel; the documentation now covers this and other ways to run tests (issue 3707 [https://github.com/scrapy/scrapy/issues/3707])

It is now possible to generate an API documentation coverage report (issue 3806 [https://github.com/scrapy/scrapy/issues/3806], issue 3810 [https://github.com/scrapy/scrapy/issues/3810], issue 3860 [https://github.com/scrapy/scrapy/issues/3860])

The documentation policies now require docstrings [https://docs.python.org/glossary.html#term-docstring] (issue 3701 [https://github.com/scrapy/scrapy/issues/3701]) that follow PEP 257 [https://www.python.org/dev/peps/pep-0257/] (issue 3748 [https://github.com/scrapy/scrapy/issues/3748])

Internal fixes and cleanup (issue 3629 [https://github.com/scrapy/scrapy/issues/3629], issue 3643 [https://github.com/scrapy/scrapy/issues/3643], issue 3684 [https://github.com/scrapy/scrapy/issues/3684], issue 3698 [https://github.com/scrapy/scrapy/issues/3698], issue 3734 [https://github.com/scrapy/scrapy/issues/3734], issue 3735 [https://github.com/scrapy/scrapy/issues/3735], issue 3736 [https://github.com/scrapy/scrapy/issues/3736], issue 3737 [https://github.com/scrapy/scrapy/issues/3737], issue 3809 [https://github.com/scrapy/scrapy/issues/3809], issue 3821 [https://github.com/scrapy/scrapy/issues/3821], issue 3825 [https://github.com/scrapy/scrapy/issues/3825], issue 3827 [https://github.com/scrapy/scrapy/issues/3827], issue 3833 [https://github.com/scrapy/scrapy/issues/3833], issue 3857 [https://github.com/scrapy/scrapy/issues/3857], issue 3877 [https://github.com/scrapy/scrapy/issues/3877])

Scrapy 1.6.0 (2019-01-30)

Highlights:

better Windows support;

Python 3.7 compatibility;

big documentation improvements, including a switch from .extract_first() + .extract() API to .get() + .getall() API;

feed exports, FilePipeline and MediaPipeline improvements;

better extensibility: item_error and request_reached_downloader signals; from_crawler support for feed exporters, feed storages and dupefilters.

scrapy.contracts fixes and new features;

telnet console security improvements, first released as a backport in Scrapy 1.5.2 (2019-01-22);

clean-up of the deprecated code;

various bug fixes, small new features and usability improvements across the codebase.

Selector API changes

While these are not changes in Scrapy itself, but rather in the parsel [https://github.com/scrapy/parsel] library which Scrapy uses for xpath/css selectors, these changes are worth mentioning here. Scrapy now depends on parsel >= 1.5, and Scrapy documentation is updated to follow recent parsel API conventions.

Most visible change is that .get() and .getall() selector methods are now preferred over .extract_first() and .extract(). We feel that these new methods result in a more concise and readable code. See extract() and extract_first() for more details.

Note

There are currently no plans to deprecate .extract() and .extract_first() methods.

Another useful new feature is the introduction of Selector.attrib and SelectorList.attrib properties, which make it easier to get attributes of HTML elements. See Selecting element attributes.

CSS selectors are cached in parsel >= 1.5, which makes them faster when the same CSS path is used many times. This is very common in case of Scrapy spiders: callbacks are usually called several times, on different pages.

If you’re using custom Selector or SelectorList subclasses, a backward incompatible change in parsel may affect your code. See parsel changelog [https://parsel.readthedocs.io/en/latest/history.html] for a detailed description, as well as for the full list of improvements.

Telnet console

Backward incompatible: Scrapy’s telnet console now requires username and password. See Telnet Console for more details. This change fixes a security issue; see Scrapy 1.5.2 (2019-01-22) release notes for details.

New extensibility features

from_crawler support is added to feed exporters and feed storages. This, among other things, allows to access Scrapy settings from custom feed storages and exporters (issue 1605 [https://github.com/scrapy/scrapy/issues/1605], issue 3348 [https://github.com/scrapy/scrapy/issues/3348]).

from_crawler support is added to dupefilters (issue 2956 [https://github.com/scrapy/scrapy/issues/2956]); this allows to access e.g. settings or a spider from a dupefilter.

item_error is fired when an error happens in a pipeline (issue 3256 [https://github.com/scrapy/scrapy/issues/3256]);

request_reached_downloader is fired when Downloader gets a new Request; this signal can be useful e.g. for custom Schedulers (issue 3393 [https://github.com/scrapy/scrapy/issues/3393]).

new SitemapSpider sitemap_filter() method which allows to select sitemap entries based on their attributes in SitemapSpider subclasses (issue 3512 [https://github.com/scrapy/scrapy/issues/3512]).

Lazy loading of Downloader Handlers is now optional; this enables better initialization error handling in custom Downloader Handlers (issue 3394 [https://github.com/scrapy/scrapy/issues/3394]).

New FilePipeline and MediaPipeline features

Expose more options for S3FilesStore: AWS_ENDPOINT_URL, AWS_USE_SSL, AWS_VERIFY, AWS_REGION_NAME. For example, this allows to use alternative or self-hosted AWS-compatible providers (issue 2609 [https://github.com/scrapy/scrapy/issues/2609], issue 3548 [https://github.com/scrapy/scrapy/issues/3548]).

ACL support for Google Cloud Storage: FILES_STORE_GCS_ACL and IMAGES_STORE_GCS_ACL (issue 3199 [https://github.com/scrapy/scrapy/issues/3199]).

scrapy.contracts improvements

Exceptions in contracts code are handled better (issue 3377 [https://github.com/scrapy/scrapy/issues/3377]);

dont_filter=True is used for contract requests, which allows to test different callbacks with the same URL (issue 3381 [https://github.com/scrapy/scrapy/issues/3381]);

request_cls attribute in Contract subclasses allow to use different Request classes in contracts, for example FormRequest (issue 3383 [https://github.com/scrapy/scrapy/issues/3383]).

Fixed errback handling in contracts, e.g. for cases where a contract is executed for URL which returns non-200 response (issue 3371 [https://github.com/scrapy/scrapy/issues/3371]).

Usability improvements

more stats for RobotsTxtMiddleware (issue 3100 [https://github.com/scrapy/scrapy/issues/3100])

INFO log level is used to show telnet host/port (issue 3115 [https://github.com/scrapy/scrapy/issues/3115])

a message is added to IgnoreRequest in RobotsTxtMiddleware (issue 3113 [https://github.com/scrapy/scrapy/issues/3113])

better validation of url argument in Response.follow (issue 3131 [https://github.com/scrapy/scrapy/issues/3131])

non-zero exit code is returned from Scrapy commands when error happens on spider inititalization (issue 3226 [https://github.com/scrapy/scrapy/issues/3226])

Link extraction improvements:「ftp」is added to scheme list (issue 3152 [https://github.com/scrapy/scrapy/issues/3152]);「flv」is added to common video extensions (issue 3165 [https://github.com/scrapy/scrapy/issues/3165])

better error message when an exporter is disabled (issue 3358 [https://github.com/scrapy/scrapy/issues/3358]);

scrapy shell --help mentions syntax required for local files (./file.html) - issue 3496 [https://github.com/scrapy/scrapy/issues/3496].

Referer header value is added to RFPDupeFilter log messages (issue 3588 [https://github.com/scrapy/scrapy/issues/3588])

Bug fixes

fixed issue with extra blank lines in .csv exports under Windows (issue 3039 [https://github.com/scrapy/scrapy/issues/3039]);

proper handling of pickling errors in Python 3 when serializing objects for disk queues (issue 3082 [https://github.com/scrapy/scrapy/issues/3082])

flags are now preserved when copying Requests (issue 3342 [https://github.com/scrapy/scrapy/issues/3342]);

FormRequest.from_response clickdata shouldn’t ignore elements with input[type=image] (issue 3153 [https://github.com/scrapy/scrapy/issues/3153]).

FormRequest.from_response should preserve duplicate keys (issue 3247 [https://github.com/scrapy/scrapy/issues/3247])

Documentation improvements

Docs are re-written to suggest .get/.getall API instead of .extract/.extract_first. Also, Selectors docs are updated and re-structured to match latest parsel docs; they now contain more topics, such as Selecting element attributes or Extensions to CSS Selectors (issue 3390 [https://github.com/scrapy/scrapy/issues/3390]).

Using your browser’s Developer Tools for scraping is a new tutorial which replaces old Firefox and Firebug tutorials (issue 3400 [https://github.com/scrapy/scrapy/issues/3400]).

SCRAPY_PROJECT environment variable is documented (issue 3518 [https://github.com/scrapy/scrapy/issues/3518]);

troubleshooting section is added to install instructions (issue 3517 [https://github.com/scrapy/scrapy/issues/3517]);

improved links to beginner resources in the tutorial (issue 3367 [https://github.com/scrapy/scrapy/issues/3367], issue 3468 [https://github.com/scrapy/scrapy/issues/3468]);

fixed RETRY_HTTP_CODES default values in docs (issue 3335 [https://github.com/scrapy/scrapy/issues/3335]);

remove unused DEPTH_STATS option from docs (issue 3245 [https://github.com/scrapy/scrapy/issues/3245]);

other cleanups (issue 3347 [https://github.com/scrapy/scrapy/issues/3347], issue 3350 [https://github.com/scrapy/scrapy/issues/3350], issue 3445 [https://github.com/scrapy/scrapy/issues/3445], issue 3544 [https://github.com/scrapy/scrapy/issues/3544], issue 3605 [https://github.com/scrapy/scrapy/issues/3605]).

Deprecation removals

Compatibility shims for pre-1.0 Scrapy module names are removed (issue 3318 [https://github.com/scrapy/scrapy/issues/3318]):

scrapy.command

scrapy.contrib (with all submodules)

scrapy.contrib_exp (with all submodules)

scrapy.dupefilter

scrapy.linkextractor

scrapy.project

scrapy.spider

scrapy.spidermanager

scrapy.squeue

scrapy.stats

scrapy.statscol

scrapy.utils.decorator

See Module Relocations for more information, or use suggestions from Scrapy 1.5.x deprecation warnings to update your code.

Other deprecation removals:

Deprecated scrapy.interfaces.ISpiderManager is removed; please use scrapy.interfaces.ISpiderLoader.

Deprecated CrawlerSettings class is removed (issue 3327 [https://github.com/scrapy/scrapy/issues/3327]).

Deprecated Settings.overrides and Settings.defaults attributes are removed (issue 3327 [https://github.com/scrapy/scrapy/issues/3327], issue 3359 [https://github.com/scrapy/scrapy/issues/3359]).

Other improvements, cleanups

All Scrapy tests now pass on Windows; Scrapy testing suite is executed in a Windows environment on CI (issue 3315 [https://github.com/scrapy/scrapy/issues/3315]).

Python 3.7 support (issue 3326 [https://github.com/scrapy/scrapy/issues/3326], issue 3150 [https://github.com/scrapy/scrapy/issues/3150], issue 3547 [https://github.com/scrapy/scrapy/issues/3547]).

Testing and CI fixes (issue 3526 [https://github.com/scrapy/scrapy/issues/3526], issue 3538 [https://github.com/scrapy/scrapy/issues/3538], issue 3308 [https://github.com/scrapy/scrapy/issues/3308], issue 3311 [https://github.com/scrapy/scrapy/issues/3311], issue 3309 [https://github.com/scrapy/scrapy/issues/3309], issue 3305 [https://github.com/scrapy/scrapy/issues/3305], issue 3210 [https://github.com/scrapy/scrapy/issues/3210], issue 3299 [https://github.com/scrapy/scrapy/issues/3299])

scrapy.http.cookies.CookieJar.clear accepts「domain」,「path」and「name」optional arguments (issue 3231 [https://github.com/scrapy/scrapy/issues/3231]).

additional files are included to sdist (issue 3495 [https://github.com/scrapy/scrapy/issues/3495]);

code style fixes (issue 3405 [https://github.com/scrapy/scrapy/issues/3405], issue 3304 [https://github.com/scrapy/scrapy/issues/3304]);

unneeded .strip() call is removed (issue 3519 [https://github.com/scrapy/scrapy/issues/3519]);

collections.deque is used to store MiddlewareManager methods instead of a list (issue 3476 [https://github.com/scrapy/scrapy/issues/3476])

Scrapy 1.5.2 (2019-01-22)

Security bugfix: Telnet console extension can be easily exploited by rogue websites POSTing content to http://localhost:6023, we haven’t found a way to exploit it from Scrapy, but it is very easy to trick a browser to do so and elevates the risk for local development environment.

The fix is backward incompatible, it enables telnet user-password authentication by default with a random generated password. If you can’t upgrade right away, please consider setting TELNETCONSOLE_PORT out of its default value.

See telnet console documentation for more info

Backport CI build failure under GCE environment due to boto import error.

Scrapy 1.5.1 (2018-07-12)

This is a maintenance release with important bug fixes, but no new features:

O(N^2) gzip decompression issue which affected Python 3 and PyPy is fixed (issue 3281 [https://github.com/scrapy/scrapy/issues/3281]);

skipping of TLS validation errors is improved (issue 3166 [https://github.com/scrapy/scrapy/issues/3166]);

Ctrl-C handling is fixed in Python 3.5+ (issue 3096 [https://github.com/scrapy/scrapy/issues/3096]);

testing fixes (issue 3092 [https://github.com/scrapy/scrapy/issues/3092], issue 3263 [https://github.com/scrapy/scrapy/issues/3263]);

documentation improvements (issue 3058 [https://github.com/scrapy/scrapy/issues/3058], issue 3059 [https://github.com/scrapy/scrapy/issues/3059], issue 3089 [https://github.com/scrapy/scrapy/issues/3089], issue 3123 [https://github.com/scrapy/scrapy/issues/3123], issue 3127 [https://github.com/scrapy/scrapy/issues/3127], issue 3189 [https://github.com/scrapy/scrapy/issues/3189], issue 3224 [https://github.com/scrapy/scrapy/issues/3224], issue 3280 [https://github.com/scrapy/scrapy/issues/3280], issue 3279 [https://github.com/scrapy/scrapy/issues/3279], issue 3201 [https://github.com/scrapy/scrapy/issues/3201], issue 3260 [https://github.com/scrapy/scrapy/issues/3260], issue 3284 [https://github.com/scrapy/scrapy/issues/3284], issue 3298 [https://github.com/scrapy/scrapy/issues/3298], issue 3294 [https://github.com/scrapy/scrapy/issues/3294]).

Scrapy 1.5.0 (2017-12-29)

This release brings small new features and improvements across the codebase. Some highlights:

Google Cloud Storage is supported in FilesPipeline and ImagesPipeline.

Crawling with proxy servers becomes more efficient, as connections to proxies can be reused now.

Warnings, exception and logging messages are improved to make debugging easier.

scrapy parse command now allows to set custom request meta via --meta argument.

Compatibility with Python 3.6, PyPy and PyPy3 is improved; PyPy and PyPy3 are now supported officially, by running tests on CI.

Better default handling of HTTP 308, 522 and 524 status codes.

Documentation is improved, as usual.

Backward Incompatible Changes

Scrapy 1.5 drops support for Python 3.3.

Default Scrapy User-Agent now uses https link to scrapy.org (issue 2983 [https://github.com/scrapy/scrapy/issues/2983]). This is technically backward-incompatible; override USER_AGENT if you relied on old value.

Logging of settings overridden by custom_settings is fixed; this is technically backward-incompatible because the logger changes from [scrapy.utils.log] to [scrapy.crawler]. If you’re parsing Scrapy logs, please update your log parsers (issue 1343 [https://github.com/scrapy/scrapy/issues/1343]).

LinkExtractor now ignores m4v extension by default, this is change in behavior.

522 and 524 status codes are added to RETRY_HTTP_CODES (issue 2851 [https://github.com/scrapy/scrapy/issues/2851])

New features

Support <link> tags in Response.follow (issue 2785 [https://github.com/scrapy/scrapy/issues/2785])

Support for ptpython REPL (issue 2654 [https://github.com/scrapy/scrapy/issues/2654])

Google Cloud Storage support for FilesPipeline and ImagesPipeline (issue 2923 [https://github.com/scrapy/scrapy/issues/2923]).

New --meta option of the「scrapy parse」command allows to pass additional request.meta (issue 2883 [https://github.com/scrapy/scrapy/issues/2883])

Populate spider variable when using shell.inspect_response (issue 2812 [https://github.com/scrapy/scrapy/issues/2812])

Handle HTTP 308 Permanent Redirect (issue 2844 [https://github.com/scrapy/scrapy/issues/2844])

Add 522 and 524 to RETRY_HTTP_CODES (issue 2851 [https://github.com/scrapy/scrapy/issues/2851])

Log versions information at startup (issue 2857 [https://github.com/scrapy/scrapy/issues/2857])

scrapy.mail.MailSender now works in Python 3 (it requires Twisted 17.9.0)

Connections to proxy servers are reused (issue 2743 [https://github.com/scrapy/scrapy/issues/2743])

Add template for a downloader middleware (issue 2755 [https://github.com/scrapy/scrapy/issues/2755])

Explicit message for NotImplementedError when parse callback not defined (issue 2831 [https://github.com/scrapy/scrapy/issues/2831])

CrawlerProcess got an option to disable installation of root log handler (issue 2921 [https://github.com/scrapy/scrapy/issues/2921])

LinkExtractor now ignores m4v extension by default

Better log messages for responses over DOWNLOAD_WARNSIZE and DOWNLOAD_MAXSIZE limits (issue 2927 [https://github.com/scrapy/scrapy/issues/2927])

Show warning when a URL is put to Spider.allowed_domains instead of a domain (issue 2250 [https://github.com/scrapy/scrapy/issues/2250]).

Bug fixes

Fix logging of settings overridden by custom_settings; this is technically backward-incompatible because the logger changes from [scrapy.utils.log] to [scrapy.crawler], so please update your log parsers if needed (issue 1343 [https://github.com/scrapy/scrapy/issues/1343])

Default Scrapy User-Agent now uses https link to scrapy.org (issue 2983 [https://github.com/scrapy/scrapy/issues/2983]). This is technically backward-incompatible; override USER_AGENT if you relied on old value.

Fix PyPy and PyPy3 test failures, support them officially (issue 2793 [https://github.com/scrapy/scrapy/issues/2793], issue 2935 [https://github.com/scrapy/scrapy/issues/2935], issue 2990 [https://github.com/scrapy/scrapy/issues/2990], issue 3050 [https://github.com/scrapy/scrapy/issues/3050], issue 2213 [https://github.com/scrapy/scrapy/issues/2213], issue 3048 [https://github.com/scrapy/scrapy/issues/3048])

Fix DNS resolver when DNSCACHE_ENABLED=False (issue 2811 [https://github.com/scrapy/scrapy/issues/2811])

Add cryptography for Debian Jessie tox test env (issue 2848 [https://github.com/scrapy/scrapy/issues/2848])

Add verification to check if Request callback is callable (issue 2766 [https://github.com/scrapy/scrapy/issues/2766])

Port extras/qpsclient.py to Python 3 (issue 2849 [https://github.com/scrapy/scrapy/issues/2849])

Use getfullargspec under the scenes for Python 3 to stop DeprecationWarning (issue 2862 [https://github.com/scrapy/scrapy/issues/2862])

Update deprecated test aliases (issue 2876 [https://github.com/scrapy/scrapy/issues/2876])

Fix SitemapSpider support for alternate links (issue 2853 [https://github.com/scrapy/scrapy/issues/2853])

Docs

Added missing bullet point for the AUTOTHROTTLE_TARGET_CONCURRENCY setting. (issue 2756 [https://github.com/scrapy/scrapy/issues/2756])

Update Contributing docs, document new support channels (issue 2762 [https://github.com/scrapy/scrapy/issues/2762], issue:3038)

Include references to Scrapy subreddit in the docs

Fix broken links; use https:// for external links (issue 2978 [https://github.com/scrapy/scrapy/issues/2978], issue 2982 [https://github.com/scrapy/scrapy/issues/2982], issue 2958 [https://github.com/scrapy/scrapy/issues/2958])

Document CloseSpider extension better (issue 2759 [https://github.com/scrapy/scrapy/issues/2759])

Use pymongo.collection.Collection.insert_one() in MongoDB example (issue 2781 [https://github.com/scrapy/scrapy/issues/2781])

Spelling mistake and typos (issue 2828 [https://github.com/scrapy/scrapy/issues/2828], issue 2837 [https://github.com/scrapy/scrapy/issues/2837], issue 2884 [https://github.com/scrapy/scrapy/issues/2884], issue 2924 [https://github.com/scrapy/scrapy/issues/2924])

Clarify CSVFeedSpider.headers documentation (issue 2826 [https://github.com/scrapy/scrapy/issues/2826])

Document DontCloseSpider exception and clarify spider_idle (issue 2791 [https://github.com/scrapy/scrapy/issues/2791])

Update「Releases」section in README (issue 2764 [https://github.com/scrapy/scrapy/issues/2764])

Fix rst syntax in DOWNLOAD_FAIL_ON_DATALOSS docs (issue 2763 [https://github.com/scrapy/scrapy/issues/2763])

Small fix in description of startproject arguments (issue 2866 [https://github.com/scrapy/scrapy/issues/2866])

Clarify data types in Response.body docs (issue 2922 [https://github.com/scrapy/scrapy/issues/2922])

Add a note about request.meta['depth'] to DepthMiddleware docs (issue 2374 [https://github.com/scrapy/scrapy/issues/2374])

Add a note about request.meta['dont_merge_cookies'] to CookiesMiddleware docs (issue 2999 [https://github.com/scrapy/scrapy/issues/2999])

Up-to-date example of project structure (issue 2964 [https://github.com/scrapy/scrapy/issues/2964], issue 2976 [https://github.com/scrapy/scrapy/issues/2976])

A better example of ItemExporters usage (issue 2989 [https://github.com/scrapy/scrapy/issues/2989])

Document from_crawler methods for spider and downloader middlewares (issue 3019 [https://github.com/scrapy/scrapy/issues/3019])

Scrapy 1.4.0 (2017-05-18)

Scrapy 1.4 does not bring that many breathtaking new features but quite a few handy improvements nonetheless.

Scrapy now supports anonymous FTP sessions with customizable user and password via the new FTP_USER and FTP_PASSWORD settings. And if you’re using Twisted version 17.1.0 or above, FTP is now available with Python 3.

There’s a new response.follow method for creating requests; it is now a recommended way to create Requests in Scrapy spiders. This method makes it easier to write correct spiders; response.follow has several advantages over creating scrapy.Request objects directly:

it handles relative URLs;

it works properly with non-ascii URLs on non-UTF8 pages;

in addition to absolute and relative URLs it supports Selectors; for <a> elements it can also extract their href values.

For example, instead of this:

for href in response.css('li.page a::attr(href)').extract(): url = response.urljoin(href) yield scrapy.Request(url, self.parse, encoding=response.encoding)

One can now write this:

for a in response.css('li.page a'): yield response.follow(a, self.parse)

Link extractors are also improved. They work similarly to what a regular modern browser would do: leading and trailing whitespace are removed from attributes (think href=" http://example.com") when building Link objects. This whitespace-stripping also happens for action attributes with FormRequest.

Please also note that link extractors do not canonicalize URLs by default anymore. This was puzzling users every now and then, and it’s not what browsers do in fact, so we removed that extra transformation on extracted links.

For those of you wanting more control on the Referer: header that Scrapy sends when following links, you can set your own Referrer Policy. Prior to Scrapy 1.4, the default RefererMiddleware would simply and blindly set it to the URL of the response that generated the HTTP request (which could leak information on your URL seeds). By default, Scrapy now behaves much like your regular browser does. And this policy is fully customizable with W3C standard values (or with something really custom of your own if you wish). See REFERRER_POLICY for details.

To make Scrapy spiders easier to debug, Scrapy logs more stats by default in 1.4: memory usage stats, detailed retry stats, detailed HTTP error code stats. A similar change is that HTTP cache path is also visible in logs now.

Last but not least, Scrapy now has the option to make JSON and XML items more human-readable, with newlines between items and even custom indenting offset, using the new FEED_EXPORT_INDENT setting.

Enjoy! (Or read on for the rest of changes in this release.)

Deprecations and Backward Incompatible Changes

Default to canonicalize=False in scrapy.linkextractors.LinkExtractor (issue 2537 [https://github.com/scrapy/scrapy/issues/2537], fixes issue 1941 [https://github.com/scrapy/scrapy/issues/1941] and issue 1982 [https://github.com/scrapy/scrapy/issues/1982]): warning, this is technically backward-incompatible

Enable memusage extension by default (issue 2539 [https://github.com/scrapy/scrapy/issues/2539], fixes issue 2187 [https://github.com/scrapy/scrapy/issues/2187]); this is technically backward-incompatible so please check if you have any non-default MEMUSAGE_*** options set.

EDITOR environment variable now takes precedence over EDITOR option defined in settings.py (issue 1829 [https://github.com/scrapy/scrapy/issues/1829]); Scrapy default settings no longer depend on environment variables. This is technically a backward incompatible change.

Spider.make_requests_from_url is deprecated (issue 1728 [https://github.com/scrapy/scrapy/issues/1728], fixes issue 1495 [https://github.com/scrapy/scrapy/issues/1495]).

New Features

Accept proxy credentials in proxy request meta key (issue 2526 [https://github.com/scrapy/scrapy/issues/2526])

Support brotli [https://github.com/google/brotli]-compressed content; requires optional brotlipy [https://github.com/python-hyper/brotlipy/] (issue 2535 [https://github.com/scrapy/scrapy/issues/2535])

New response.follow shortcut for creating requests (issue 1940 [https://github.com/scrapy/scrapy/issues/1940])

Added flags argument and attribute to Request objects (issue 2047 [https://github.com/scrapy/scrapy/issues/2047])

Support Anonymous FTP (issue 2342 [https://github.com/scrapy/scrapy/issues/2342])

Added retry/count, retry/max_reached and retry/reason_count/<reason> stats to RetryMiddleware (issue 2543 [https://github.com/scrapy/scrapy/issues/2543])

Added httperror/response_ignored_count and httperror/response_ignored_status_count/<status> stats to HttpErrorMiddleware (issue 2566 [https://github.com/scrapy/scrapy/issues/2566])

Customizable Referrer policy in RefererMiddleware (issue 2306 [https://github.com/scrapy/scrapy/issues/2306])

New data: URI download handler (issue 2334 [https://github.com/scrapy/scrapy/issues/2334], fixes issue 2156 [https://github.com/scrapy/scrapy/issues/2156])

Log cache directory when HTTP Cache is used (issue 2611 [https://github.com/scrapy/scrapy/issues/2611], fixes issue 2604 [https://github.com/scrapy/scrapy/issues/2604])

Warn users when project contains duplicate spider names (fixes issue 2181 [https://github.com/scrapy/scrapy/issues/2181])

scrapy.utils.datatypes.CaselessDict now accepts Mapping instances and not only dicts (issue 2646 [https://github.com/scrapy/scrapy/issues/2646])

Media downloads, with FilesPipeline or ImagesPipeline, can now optionally handle HTTP redirects using the new MEDIA_ALLOW_REDIRECTS setting (issue 2616 [https://github.com/scrapy/scrapy/issues/2616], fixes issue 2004 [https://github.com/scrapy/scrapy/issues/2004])

Accept non-complete responses from websites using a new DOWNLOAD_FAIL_ON_DATALOSS setting (issue 2590 [https://github.com/scrapy/scrapy/issues/2590], fixes issue 2586 [https://github.com/scrapy/scrapy/issues/2586])

Optional pretty-printing of JSON and XML items via FEED_EXPORT_INDENT setting (issue 2456 [https://github.com/scrapy/scrapy/issues/2456], fixes issue 1327 [https://github.com/scrapy/scrapy/issues/1327])

Allow dropping fields in FormRequest.from_response formdata when None value is passed (issue 667 [https://github.com/scrapy/scrapy/issues/667])

Per-request retry times with the new max_retry_times meta key (issue 2642 [https://github.com/scrapy/scrapy/issues/2642])

python -m scrapy as a more explicit alternative to scrapy command (issue 2740 [https://github.com/scrapy/scrapy/issues/2740])

Bug fixes

LinkExtractor now strips leading and trailing whitespaces from attributes (issue 2547 [https://github.com/scrapy/scrapy/issues/2547], fixes issue 1614 [https://github.com/scrapy/scrapy/issues/1614])

Properly handle whitespaces in action attribute in FormRequest (issue 2548 [https://github.com/scrapy/scrapy/issues/2548])

Buffer CONNECT response bytes from proxy until all HTTP headers are received (issue 2495 [https://github.com/scrapy/scrapy/issues/2495], fixes issue 2491 [https://github.com/scrapy/scrapy/issues/2491])

FTP downloader now works on Python 3, provided you use Twisted>=17.1 (issue 2599 [https://github.com/scrapy/scrapy/issues/2599])

Use body to choose response type after decompressing content (issue 2393 [https://github.com/scrapy/scrapy/issues/2393], fixes issue 2145 [https://github.com/scrapy/scrapy/issues/2145])

Always decompress Content-Encoding: gzip at HttpCompressionMiddleware stage (issue 2391 [https://github.com/scrapy/scrapy/issues/2391])

Respect custom log level in Spider.custom_settings (issue 2581 [https://github.com/scrapy/scrapy/issues/2581], fixes issue 1612 [https://github.com/scrapy/scrapy/issues/1612])

‘make htmlview’ fix for macOS (issue 2661 [https://github.com/scrapy/scrapy/issues/2661])

Remove「commands」from the command list (issue 2695 [https://github.com/scrapy/scrapy/issues/2695])

Fix duplicate Content-Length header for POST requests with empty body (issue 2677 [https://github.com/scrapy/scrapy/issues/2677])

Properly cancel large downloads, i.e. above DOWNLOAD_MAXSIZE (issue 1616 [https://github.com/scrapy/scrapy/issues/1616])

ImagesPipeline: fixed processing of transparent PNG images with palette (issue 2675 [https://github.com/scrapy/scrapy/issues/2675])

Cleanups & Refactoring

Tests: remove temp files and folders (issue 2570 [https://github.com/scrapy/scrapy/issues/2570]), fixed ProjectUtilsTest on OS X (issue 2569 [https://github.com/scrapy/scrapy/issues/2569]), use portable pypy for Linux on Travis CI (issue 2710 [https://github.com/scrapy/scrapy/issues/2710])

Separate building request from _requests_to_follow in CrawlSpider (issue 2562 [https://github.com/scrapy/scrapy/issues/2562])

Remove「Python 3 progress」badge (issue 2567 [https://github.com/scrapy/scrapy/issues/2567])

Add a couple more lines to .gitignore (issue 2557 [https://github.com/scrapy/scrapy/issues/2557])

Remove bumpversion prerelease configuration (issue 2159 [https://github.com/scrapy/scrapy/issues/2159])

Add codecov.yml file (issue 2750 [https://github.com/scrapy/scrapy/issues/2750])

Set context factory implementation based on Twisted version (issue 2577 [https://github.com/scrapy/scrapy/issues/2577], fixes issue 2560 [https://github.com/scrapy/scrapy/issues/2560])

Add omitted self arguments in default project middleware template (issue 2595 [https://github.com/scrapy/scrapy/issues/2595])

Remove redundant slot.add_request() call in ExecutionEngine (issue 2617 [https://github.com/scrapy/scrapy/issues/2617])

Catch more specific os.error exception in scrapy.pipelines.files.FSFilesStore (issue 2644 [https://github.com/scrapy/scrapy/issues/2644])

Change「localhost」test server certificate (issue 2720 [https://github.com/scrapy/scrapy/issues/2720])

Remove unused MEMUSAGE_REPORT setting (issue 2576 [https://github.com/scrapy/scrapy/issues/2576])

Documentation

Binary mode is required for exporters (issue 2564 [https://github.com/scrapy/scrapy/issues/2564], fixes issue 2553 [https://github.com/scrapy/scrapy/issues/2553])

Mention issue with FormRequest.from_response due to bug in lxml (issue 2572 [https://github.com/scrapy/scrapy/issues/2572])

Use single quotes uniformly in templates (issue 2596 [https://github.com/scrapy/scrapy/issues/2596])

Document ftp_user and ftp_password meta keys (issue 2587 [https://github.com/scrapy/scrapy/issues/2587])

Removed section on deprecated contrib/ (issue 2636 [https://github.com/scrapy/scrapy/issues/2636])

Recommend Anaconda when installing Scrapy on Windows (issue 2477 [https://github.com/scrapy/scrapy/issues/2477], fixes issue 2475 [https://github.com/scrapy/scrapy/issues/2475])

FAQ: rewrite note on Python 3 support on Windows (issue 2690 [https://github.com/scrapy/scrapy/issues/2690])

Rearrange selector sections (issue 2705 [https://github.com/scrapy/scrapy/issues/2705])

Remove __nonzero__ from SelectorList docs (issue 2683 [https://github.com/scrapy/scrapy/issues/2683])

Mention how to disable request filtering in documentation of DUPEFILTER_CLASS setting (issue 2714 [https://github.com/scrapy/scrapy/issues/2714])

Add sphinx_rtd_theme to docs setup readme (issue 2668 [https://github.com/scrapy/scrapy/issues/2668])

Open file in text mode in JSON item writer example (issue 2729 [https://github.com/scrapy/scrapy/issues/2729])

Clarify allowed_domains example (issue 2670 [https://github.com/scrapy/scrapy/issues/2670])

Scrapy 1.3.3 (2017-03-10)

Bug fixes

Make SpiderLoader raise ImportError again by default for missing dependencies and wrong SPIDER_MODULES. These exceptions were silenced as warnings since 1.3.0. A new setting is introduced to toggle between warning or exception if needed ; see SPIDER_LOADER_WARN_ONLY for details.

Scrapy 1.3.2 (2017-02-13)

Bug fixes

Preserve request class when converting to/from dicts (utils.reqser) (issue 2510 [https://github.com/scrapy/scrapy/issues/2510]).

Use consistent selectors for author field in tutorial (issue 2551 [https://github.com/scrapy/scrapy/issues/2551]).

Fix TLS compatibility in Twisted 17+ (issue 2558 [https://github.com/scrapy/scrapy/issues/2558])

Scrapy 1.3.1 (2017-02-08)

New features

Support 'True' and 'False' string values for boolean settings (issue 2519 [https://github.com/scrapy/scrapy/issues/2519]); you can now do something like scrapy crawl myspider -s REDIRECT_ENABLED=False.

Support kwargs with response.xpath() to use XPath variables and ad-hoc namespaces declarations ; this requires at least Parsel v1.1 (issue 2457 [https://github.com/scrapy/scrapy/issues/2457]).

Add support for Python 3.6 (issue 2485 [https://github.com/scrapy/scrapy/issues/2485]).

Run tests on PyPy (warning: some tests still fail, so PyPy is not supported yet).

Bug fixes

Enforce DNS_TIMEOUT setting (issue 2496 [https://github.com/scrapy/scrapy/issues/2496]).

Fix view command ; it was a regression in v1.3.0 (issue 2503 [https://github.com/scrapy/scrapy/issues/2503]).

Fix tests regarding *_EXPIRES settings with Files/Images pipelines (issue 2460 [https://github.com/scrapy/scrapy/issues/2460]).

Fix name of generated pipeline class when using basic project template (issue 2466 [https://github.com/scrapy/scrapy/issues/2466]).

Fix compatiblity with Twisted 17+ (issue 2496 [https://github.com/scrapy/scrapy/issues/2496], issue 2528 [https://github.com/scrapy/scrapy/issues/2528]).

Fix scrapy.Item inheritance on Python 3.6 (issue 2511 [https://github.com/scrapy/scrapy/issues/2511]).

Enforce numeric values for components order in SPIDER_MIDDLEWARES, DOWNLOADER_MIDDLEWARES, EXTENIONS and SPIDER_CONTRACTS (issue 2420 [https://github.com/scrapy/scrapy/issues/2420]).

Documentation

Reword Code of Coduct section and upgrade to Contributor Covenant v1.4 (issue 2469 [https://github.com/scrapy/scrapy/issues/2469]).

Clarify that passing spider arguments converts them to spider attributes (issue 2483 [https://github.com/scrapy/scrapy/issues/2483]).

Document formid argument on FormRequest.from_response() (issue 2497 [https://github.com/scrapy/scrapy/issues/2497]).

Add .rst extension to README files (issue 2507 [https://github.com/scrapy/scrapy/issues/2507]).

Mention LevelDB cache storage backend (issue 2525 [https://github.com/scrapy/scrapy/issues/2525]).

Use yield in sample callback code (issue 2533 [https://github.com/scrapy/scrapy/issues/2533]).

Add note about HTML entities decoding with .re()/.re_first() (issue 1704 [https://github.com/scrapy/scrapy/issues/1704]).

Typos (issue 2512 [https://github.com/scrapy/scrapy/issues/2512], issue 2534 [https://github.com/scrapy/scrapy/issues/2534], issue 2531 [https://github.com/scrapy/scrapy/issues/2531]).

Cleanups

Remove reduntant check in MetaRefreshMiddleware (issue 2542 [https://github.com/scrapy/scrapy/issues/2542]).

Faster checks in LinkExtractor for allow/deny patterns (issue 2538 [https://github.com/scrapy/scrapy/issues/2538]).

Remove dead code supporting old Twisted versions (issue 2544 [https://github.com/scrapy/scrapy/issues/2544]).

Scrapy 1.3.0 (2016-12-21)

This release comes rather soon after 1.2.2 for one main reason: it was found out that releases since 0.18 up to 1.2.2 (included) use some backported code from Twisted (scrapy.xlib.tx.*), even if newer Twisted modules are available. Scrapy now uses twisted.web.client and twisted.internet.endpoints directly. (See also cleanups below.)

As it is a major change, we wanted to get the bug fix out quickly while not breaking any projects using the 1.2 series.

New Features

MailSender now accepts single strings as values for to and cc arguments (issue 2272 [https://github.com/scrapy/scrapy/issues/2272])

scrapy fetch url, scrapy shell url and fetch(url) inside scrapy shell now follow HTTP redirections by default (issue 2290 [https://github.com/scrapy/scrapy/issues/2290]); See fetch and shell for details.

HttpErrorMiddleware now logs errors with INFO level instead of DEBUG; this is technically backward incompatible so please check your log parsers.

By default, logger names now use a long-form path, e.g. [scrapy.extensions.logstats], instead of the shorter「top-level」variant of prior releases (e.g. [scrapy]); this is backward incompatible if you have log parsers expecting the short logger name part. You can switch back to short logger names using LOG_SHORT_NAMES set to True.

Dependencies & Cleanups

Scrapy now requires Twisted >= 13.1 which is the case for many Linux distributions already.

As a consequence, we got rid of scrapy.xlib.tx.* modules, which copied some of Twisted code for users stuck with an「old」Twisted version

ChunkedTransferMiddleware is deprecated and removed from the default downloader middlewares.

Scrapy 1.2.3 (2017-03-03)

Packaging fix: disallow unsupported Twisted versions in setup.py

Scrapy 1.2.2 (2016-12-06)

Bug fixes

Fix a cryptic traceback when a pipeline fails on open_spider() (issue 2011 [https://github.com/scrapy/scrapy/issues/2011])

Fix embedded IPython shell variables (fixing issue 396 [https://github.com/scrapy/scrapy/issues/396] that re-appeared in 1.2.0, fixed in issue 2418 [https://github.com/scrapy/scrapy/issues/2418])

A couple of patches when dealing with robots.txt:

handle (non-standard) relative sitemap URLs (issue 2390 [https://github.com/scrapy/scrapy/issues/2390])

handle non-ASCII URLs and User-Agents in Python 2 (issue 2373 [https://github.com/scrapy/scrapy/issues/2373])

Documentation

Document "download_latency" key in Request’s meta dict (issue 2033 [https://github.com/scrapy/scrapy/issues/2033])

Remove page on (deprecated & unsupported) Ubuntu packages from ToC (issue 2335 [https://github.com/scrapy/scrapy/issues/2335])

A few fixed typos (issue 2346 [https://github.com/scrapy/scrapy/issues/2346], issue 2369 [https://github.com/scrapy/scrapy/issues/2369], issue 2369 [https://github.com/scrapy/scrapy/issues/2369], issue 2380 [https://github.com/scrapy/scrapy/issues/2380]) and clarifications (issue 2354 [https://github.com/scrapy/scrapy/issues/2354], issue 2325 [https://github.com/scrapy/scrapy/issues/2325], issue 2414 [https://github.com/scrapy/scrapy/issues/2414])

Other changes

Advertize conda-forge [https://anaconda.org/conda-forge/scrapy] as Scrapy’s official conda channel (issue 2387 [https://github.com/scrapy/scrapy/issues/2387])

More helpful error messages when trying to use .css() or .xpath() on non-Text Responses (issue 2264 [https://github.com/scrapy/scrapy/issues/2264])

startproject command now generates a sample middlewares.py file (issue 2335 [https://github.com/scrapy/scrapy/issues/2335])

Add more dependencies’ version info in scrapy version verbose output (issue 2404 [https://github.com/scrapy/scrapy/issues/2404])

Remove all *.pyc files from source distribution (issue 2386 [https://github.com/scrapy/scrapy/issues/2386])

Scrapy 1.2.1 (2016-10-21)

Bug fixes

Include OpenSSL’s more permissive default ciphers when establishing TLS/SSL connections (issue 2314 [https://github.com/scrapy/scrapy/issues/2314]).

Fix「Location」HTTP header decoding on non-ASCII URL redirects (issue 2321 [https://github.com/scrapy/scrapy/issues/2321]).

Documentation

Fix JsonWriterPipeline example (issue 2302 [https://github.com/scrapy/scrapy/issues/2302]).

Various notes: issue 2330 [https://github.com/scrapy/scrapy/issues/2330] on spider names, issue 2329 [https://github.com/scrapy/scrapy/issues/2329] on middleware methods processing order, issue 2327 [https://github.com/scrapy/scrapy/issues/2327] on getting multi-valued HTTP headers as lists.

Other changes

Removed www. from start_urls in built-in spider templates (issue 2299 [https://github.com/scrapy/scrapy/issues/2299]).

Scrapy 1.2.0 (2016-10-03)

New Features

New FEED_EXPORT_ENCODING setting to customize the encoding used when writing items to a file. This can be used to turn off \uXXXX escapes in JSON output. This is also useful for those wanting something else than UTF-8 for XML or CSV output (issue 2034 [https://github.com/scrapy/scrapy/issues/2034]).

startproject command now supports an optional destination directory to override the default one based on the project name (issue 2005 [https://github.com/scrapy/scrapy/issues/2005]).

New SCHEDULER_DEBUG setting to log requests serialization failures (issue 1610 [https://github.com/scrapy/scrapy/issues/1610]).

JSON encoder now supports serialization of set instances (issue 2058 [https://github.com/scrapy/scrapy/issues/2058]).

Interpret application/json-amazonui-streaming as TextResponse (issue 1503 [https://github.com/scrapy/scrapy/issues/1503]).

scrapy is imported by default when using shell tools (shell, inspect_response) (issue 2248 [https://github.com/scrapy/scrapy/issues/2248]).

Bug fixes

DefaultRequestHeaders middleware now runs before UserAgent middleware (issue 2088 [https://github.com/scrapy/scrapy/issues/2088]). Warning: this is technically backward incompatible, though we consider this a bug fix.

HTTP cache extension and plugins that use the .scrapy data directory now work outside projects (issue 1581 [https://github.com/scrapy/scrapy/issues/1581]). Warning: this is technically backward incompatible, though we consider this a bug fix.

Selector does not allow passing both response and text anymore (issue 2153 [https://github.com/scrapy/scrapy/issues/2153]).

Fixed logging of wrong callback name with scrapy parse (issue 2169 [https://github.com/scrapy/scrapy/issues/2169]).

Fix for an odd gzip decompression bug (issue 1606 [https://github.com/scrapy/scrapy/issues/1606]).

Fix for selected callbacks when using CrawlSpider with scrapy parse (issue 2225 [https://github.com/scrapy/scrapy/issues/2225]).

Fix for invalid JSON and XML files when spider yields no items (issue 872 [https://github.com/scrapy/scrapy/issues/872]).

Implement flush() fpr StreamLogger avoiding a warning in logs (issue 2125 [https://github.com/scrapy/scrapy/issues/2125]).

Refactoring

canonicalize_url has been moved to w3lib.url [https://w3lib.readthedocs.io/en/latest/w3lib.html#w3lib.url.canonicalize_url] (issue 2168 [https://github.com/scrapy/scrapy/issues/2168]).

Tests & Requirements

Scrapy’s new requirements baseline is Debian 8「Jessie」. It was previously Ubuntu 12.04 Precise. What this means in practice is that we run continuous integration tests with these (main) packages versions at a minimum: Twisted 14.0, pyOpenSSL 0.14, lxml 3.4.

Scrapy may very well work with older versions of these packages (the code base still has switches for older Twisted versions for example) but it is not guaranteed (because it’s not tested anymore).

Documentation

Grammar fixes: issue 2128 [https://github.com/scrapy/scrapy/issues/2128], issue 1566 [https://github.com/scrapy/scrapy/issues/1566].

Download stats badge removed from README (issue 2160 [https://github.com/scrapy/scrapy/issues/2160]).

New scrapy architecture diagram (issue 2165 [https://github.com/scrapy/scrapy/issues/2165]).

Updated Response parameters documentation (issue 2197 [https://github.com/scrapy/scrapy/issues/2197]).

Reworded misleading RANDOMIZE_DOWNLOAD_DELAY description (issue 2190 [https://github.com/scrapy/scrapy/issues/2190]).

Add StackOverflow as a support channel (issue 2257 [https://github.com/scrapy/scrapy/issues/2257]).

Scrapy 1.1.4 (2017-03-03)

Packaging fix: disallow unsupported Twisted versions in setup.py

Scrapy 1.1.3 (2016-09-22)

Bug fixes

Class attributes for subclasses of ImagesPipeline and FilesPipeline work as they did before 1.1.1 (issue 2243 [https://github.com/scrapy/scrapy/issues/2243], fixes issue 2198 [https://github.com/scrapy/scrapy/issues/2198])

Documentation

Overview and tutorial rewritten to use http://toscrape.com websites (issue 2236 [https://github.com/scrapy/scrapy/issues/2236], issue 2249 [https://github.com/scrapy/scrapy/issues/2249], issue 2252 [https://github.com/scrapy/scrapy/issues/2252]).

Scrapy 1.1.2 (2016-08-18)

Bug fixes

Introduce a missing IMAGES_STORE_S3_ACL setting to override the default ACL policy in ImagesPipeline when uploading images to S3 (note that default ACL policy is「private」– instead of「public-read」– since Scrapy 1.1.0)

IMAGES_EXPIRES default value set back to 90 (the regression was introduced in 1.1.1)

Scrapy 1.1.1 (2016-07-13)

Bug fixes

Add「Host」header in CONNECT requests to HTTPS proxies (issue 2069 [https://github.com/scrapy/scrapy/issues/2069])

Use response body when choosing response class (issue 2001 [https://github.com/scrapy/scrapy/issues/2001], fixes issue 2000 [https://github.com/scrapy/scrapy/issues/2000])

Do not fail on canonicalizing URLs with wrong netlocs (issue 2038 [https://github.com/scrapy/scrapy/issues/2038], fixes issue 2010 [https://github.com/scrapy/scrapy/issues/2010])

a few fixes for HttpCompressionMiddleware (and SitemapSpider):

Do not decode HEAD responses (issue 2008 [https://github.com/scrapy/scrapy/issues/2008], fixes issue 1899 [https://github.com/scrapy/scrapy/issues/1899])

Handle charset parameter in gzip Content-Type header (issue 2050 [https://github.com/scrapy/scrapy/issues/2050], fixes issue 2049 [https://github.com/scrapy/scrapy/issues/2049])

Do not decompress gzip octet-stream responses (issue 2065 [https://github.com/scrapy/scrapy/issues/2065], fixes issue 2063 [https://github.com/scrapy/scrapy/issues/2063])

Catch (and ignore with a warning) exception when verifying certificate against IP-address hosts (issue 2094 [https://github.com/scrapy/scrapy/issues/2094], fixes issue 2092 [https://github.com/scrapy/scrapy/issues/2092])

Make FilesPipeline and ImagesPipeline backward compatible again regarding the use of legacy class attributes for customization (issue 1989 [https://github.com/scrapy/scrapy/issues/1989], fixes issue 1985 [https://github.com/scrapy/scrapy/issues/1985])

New features

Enable genspider command outside project folder (issue 2052 [https://github.com/scrapy/scrapy/issues/2052])

Retry HTTPS CONNECT TunnelError by default (issue 1974 [https://github.com/scrapy/scrapy/issues/1974])

Documentation

FEED_TEMPDIR setting at lexicographical position (commit 9b3c72c [https://github.com/scrapy/scrapy/commit/9b3c72c])

Use idiomatic .extract_first() in overview (issue 1994 [https://github.com/scrapy/scrapy/issues/1994])

Update years in copyright notice (commit c2c8036 [https://github.com/scrapy/scrapy/commit/c2c8036])

Add information and example on errbacks (issue 1995 [https://github.com/scrapy/scrapy/issues/1995])

Use「url」variable in downloader middleware example (issue 2015 [https://github.com/scrapy/scrapy/issues/2015])

Grammar fixes (issue 2054 [https://github.com/scrapy/scrapy/issues/2054], issue 2120 [https://github.com/scrapy/scrapy/issues/2120])

New FAQ entry on using BeautifulSoup in spider callbacks (issue 2048 [https://github.com/scrapy/scrapy/issues/2048])

Add notes about scrapy not working on Windows with Python 3 (issue 2060 [https://github.com/scrapy/scrapy/issues/2060])

Encourage complete titles in pull requests (issue 2026 [https://github.com/scrapy/scrapy/issues/2026])

Tests

Upgrade py.test requirement on Travis CI and Pin pytest-cov to 2.2.1 (issue 2095 [https://github.com/scrapy/scrapy/issues/2095])

Scrapy 1.1.0 (2016-05-11)

This 1.1 release brings a lot of interesting features and bug fixes:

Scrapy 1.1 has beta Python 3 support (requires Twisted >= 15.5). See Beta Python 3 Support for more details and some limitations.

Hot new features:

Item loaders now support nested loaders (issue 1467 [https://github.com/scrapy/scrapy/issues/1467]).

FormRequest.from_response improvements (issue 1382 [https://github.com/scrapy/scrapy/issues/1382], issue 1137 [https://github.com/scrapy/scrapy/issues/1137]).

Added setting AUTOTHROTTLE_TARGET_CONCURRENCY and improved AutoThrottle docs (issue 1324 [https://github.com/scrapy/scrapy/issues/1324]).

Added response.text to get body as unicode (issue 1730 [https://github.com/scrapy/scrapy/issues/1730]).

Anonymous S3 connections (issue 1358 [https://github.com/scrapy/scrapy/issues/1358]).

Deferreds in downloader middlewares (issue 1473 [https://github.com/scrapy/scrapy/issues/1473]). This enables better robots.txt handling (issue 1471 [https://github.com/scrapy/scrapy/issues/1471]).

HTTP caching now follows RFC2616 more closely, added settings HTTPCACHE_ALWAYS_STORE and HTTPCACHE_IGNORE_RESPONSE_CACHE_CONTROLS (issue 1151 [https://github.com/scrapy/scrapy/issues/1151]).

Selectors were extracted to the parsel [https://github.com/scrapy/parsel] library (issue 1409 [https://github.com/scrapy/scrapy/issues/1409]). This means you can use Scrapy Selectors without Scrapy and also upgrade the selectors engine without needing to upgrade Scrapy.

HTTPS downloader now does TLS protocol negotiation by default, instead of forcing TLS 1.0. You can also set the SSL/TLS method using the new DOWNLOADER_CLIENT_TLS_METHOD.

These bug fixes may require your attention:

Don’t retry bad requests (HTTP 400) by default (issue 1289 [https://github.com/scrapy/scrapy/issues/1289]). If you need the old behavior, add 400 to RETRY_HTTP_CODES.

Fix shell files argument handling (issue 1710 [https://github.com/scrapy/scrapy/issues/1710], issue 1550 [https://github.com/scrapy/scrapy/issues/1550]). If you try scrapy shell index.html it will try to load the URL http://index.html, use scrapy shell ./index.html to load a local file.

Robots.txt compliance is now enabled by default for newly-created projects (issue 1724 [https://github.com/scrapy/scrapy/issues/1724]). Scrapy will also wait for robots.txt to be downloaded before proceeding with the crawl (issue 1735 [https://github.com/scrapy/scrapy/issues/1735]). If you want to disable this behavior, update ROBOTSTXT_OBEY in settings.py file after creating a new project.

Exporters now work on unicode, instead of bytes by default (issue 1080 [https://github.com/scrapy/scrapy/issues/1080]). If you use PythonItemExporter, you may want to update your code to disable binary mode which is now deprecated.

Accept XML node names containing dots as valid (issue 1533 [https://github.com/scrapy/scrapy/issues/1533]).

When uploading files or images to S3 (with FilesPipeline or ImagesPipeline), the default ACL policy is now「private」instead of「public」Warning: backward incompatible!. You can use FILES_STORE_S3_ACL to change it.

We’ve reimplemented canonicalize_url() for more correct output, especially for URLs with non-ASCII characters (issue 1947 [https://github.com/scrapy/scrapy/issues/1947]). This could change link extractors output compared to previous scrapy versions. This may also invalidate some cache entries you could still have from pre-1.1 runs. Warning: backward incompatible!.

Keep reading for more details on other improvements and bug fixes.

Beta Python 3 Support

We have been hard at work to make Scrapy run on Python 3 [https://github.com/scrapy/scrapy/wiki/Python-3-Porting]. As a result, now you can run spiders on Python 3.3, 3.4 and 3.5 (Twisted >= 15.5 required). Some features are still missing (and some may never be ported).

Almost all builtin extensions/middlewares are expected to work. However, we are aware of some limitations in Python 3:

Scrapy does not work on Windows with Python 3

Sending emails is not supported

FTP download handler is not supported

Telnet console is not supported

Additional New Features and Enhancements

Scrapy now has a Code of Conduct [https://github.com/scrapy/scrapy/blob/master/CODE_OF_CONDUCT.md] (issue 1681 [https://github.com/scrapy/scrapy/issues/1681]).

Command line tool now has completion for zsh (issue 934 [https://github.com/scrapy/scrapy/issues/934]).

Improvements to scrapy shell:

Support for bpython and configure preferred Python shell via SCRAPY_PYTHON_SHELL (issue 1100 [https://github.com/scrapy/scrapy/issues/1100], issue 1444 [https://github.com/scrapy/scrapy/issues/1444]).

Support URLs without scheme (issue 1498 [https://github.com/scrapy/scrapy/issues/1498]) Warning: backward incompatible!

Bring back support for relative file path (issue 1710 [https://github.com/scrapy/scrapy/issues/1710], issue 1550 [https://github.com/scrapy/scrapy/issues/1550]).

Added MEMUSAGE_CHECK_INTERVAL_SECONDS setting to change default check interval (issue 1282 [https://github.com/scrapy/scrapy/issues/1282]).

Download handlers are now lazy-loaded on first request using their scheme (issue 1390 [https://github.com/scrapy/scrapy/issues/1390], issue 1421 [https://github.com/scrapy/scrapy/issues/1421]).

HTTPS download handlers do not force TLS 1.0 anymore; instead, OpenSSL’s SSLv23_method()/TLS_method() is used allowing to try negotiating with the remote hosts the highest TLS protocol version it can (issue 1794 [https://github.com/scrapy/scrapy/issues/1794], issue 1629 [https://github.com/scrapy/scrapy/issues/1629]).

RedirectMiddleware now skips the status codes from handle_httpstatus_list on spider attribute or in Request’s meta key (issue 1334 [https://github.com/scrapy/scrapy/issues/1334], issue 1364 [https://github.com/scrapy/scrapy/issues/1364], issue 1447 [https://github.com/scrapy/scrapy/issues/1447]).

Form submission:

now works with <button> elements too (issue 1469 [https://github.com/scrapy/scrapy/issues/1469]).

an empty string is now used for submit buttons without a value (issue 1472 [https://github.com/scrapy/scrapy/issues/1472])

Dict-like settings now have per-key priorities (issue 1135 [https://github.com/scrapy/scrapy/issues/1135], issue 1149 [https://github.com/scrapy/scrapy/issues/1149] and issue 1586 [https://github.com/scrapy/scrapy/issues/1586]).

Sending non-ASCII emails (issue 1662 [https://github.com/scrapy/scrapy/issues/1662])

CloseSpider and SpiderState extensions now get disabled if no relevant setting is set (issue 1723 [https://github.com/scrapy/scrapy/issues/1723], issue 1725 [https://github.com/scrapy/scrapy/issues/1725]).

Added method ExecutionEngine.close (issue 1423 [https://github.com/scrapy/scrapy/issues/1423]).

Added method CrawlerRunner.create_crawler (issue 1528 [https://github.com/scrapy/scrapy/issues/1528]).

Scheduler priority queue can now be customized via SCHEDULER_PRIORITY_QUEUE (issue 1822 [https://github.com/scrapy/scrapy/issues/1822]).

.pps links are now ignored by default in link extractors (issue 1835 [https://github.com/scrapy/scrapy/issues/1835]).

temporary data folder for FTP and S3 feed storages can be customized using a new FEED_TEMPDIR setting (issue 1847 [https://github.com/scrapy/scrapy/issues/1847]).

FilesPipeline and ImagesPipeline settings are now instance attributes instead of class attributes, enabling spider-specific behaviors (issue 1891 [https://github.com/scrapy/scrapy/issues/1891]).

JsonItemExporter now formats opening and closing square brackets on their own line (first and last lines of output file) (issue 1950 [https://github.com/scrapy/scrapy/issues/1950]).

If available, botocore is used for S3FeedStorage, S3DownloadHandler and S3FilesStore (issue 1761 [https://github.com/scrapy/scrapy/issues/1761], issue 1883 [https://github.com/scrapy/scrapy/issues/1883]).

Tons of documentation updates and related fixes (issue 1291 [https://github.com/scrapy/scrapy/issues/1291], issue 1302 [https://github.com/scrapy/scrapy/issues/1302], issue 1335 [https://github.com/scrapy/scrapy/issues/1335], issue 1683 [https://github.com/scrapy/scrapy/issues/1683], issue 1660 [https://github.com/scrapy/scrapy/issues/1660], issue 1642 [https://github.com/scrapy/scrapy/issues/1642], issue 1721 [https://github.com/scrapy/scrapy/issues/1721], issue 1727 [https://github.com/scrapy/scrapy/issues/1727], issue 1879 [https://github.com/scrapy/scrapy/issues/1879]).

Other refactoring, optimizations and cleanup (issue 1476 [https://github.com/scrapy/scrapy/issues/1476], issue 1481 [https://github.com/scrapy/scrapy/issues/1481], issue 1477 [https://github.com/scrapy/scrapy/issues/1477], issue 1315 [https://github.com/scrapy/scrapy/issues/1315], issue 1290 [https://github.com/scrapy/scrapy/issues/1290], issue 1750 [https://github.com/scrapy/scrapy/issues/1750], issue 1881 [https://github.com/scrapy/scrapy/issues/1881]).

Deprecations and Removals

Added to_bytes and to_unicode, deprecated str_to_unicode and unicode_to_str functions (issue 778 [https://github.com/scrapy/scrapy/issues/778]).

binary_is_text is introduced, to replace use of isbinarytext (but with inverse return value) (issue 1851 [https://github.com/scrapy/scrapy/issues/1851])

The optional_features set has been removed (issue 1359 [https://github.com/scrapy/scrapy/issues/1359]).

The --lsprof command line option has been removed (issue 1689 [https://github.com/scrapy/scrapy/issues/1689]). Warning: backward incompatible, but doesn’t break user code.

The following datatypes were deprecated (issue 1720 [https://github.com/scrapy/scrapy/issues/1720]):

scrapy.utils.datatypes.MultiValueDictKeyError

scrapy.utils.datatypes.MultiValueDict

scrapy.utils.datatypes.SiteNode

The previously bundled scrapy.xlib.pydispatch library was deprecated and replaced by pydispatcher [https://pypi.python.org/pypi/PyDispatcher].

Relocations

telnetconsole was relocated to extensions/ (issue 1524 [https://github.com/scrapy/scrapy/issues/1524]).

Note: telnet is not enabled on Python 3 (https://github.com/scrapy/scrapy/pull/1524#issuecomment-146985595)

Bugfixes

Scrapy does not retry requests that got a HTTP 400 Bad Request response anymore (issue 1289 [https://github.com/scrapy/scrapy/issues/1289]). Warning: backward incompatible!

Support empty password for http_proxy config (issue 1274 [https://github.com/scrapy/scrapy/issues/1274]).

Interpret application/x-json as TextResponse (issue 1333 [https://github.com/scrapy/scrapy/issues/1333]).

Support link rel attribute with multiple values (issue 1201 [https://github.com/scrapy/scrapy/issues/1201]).

Fixed scrapy.http.FormRequest.from_response when there is a <base> tag (issue 1564 [https://github.com/scrapy/scrapy/issues/1564]).

Fixed TEMPLATES_DIR handling (issue 1575 [https://github.com/scrapy/scrapy/issues/1575]).

Various FormRequest fixes (issue 1595 [https://github.com/scrapy/scrapy/issues/1595], issue 1596 [https://github.com/scrapy/scrapy/issues/1596], issue 1597 [https://github.com/scrapy/scrapy/issues/1597]).

Makes _monkeypatches more robust (issue 1634 [https://github.com/scrapy/scrapy/issues/1634]).

Fixed bug on XMLItemExporter with non-string fields in items (issue 1738 [https://github.com/scrapy/scrapy/issues/1738]).

Fixed startproject command in OS X (issue 1635 [https://github.com/scrapy/scrapy/issues/1635]).

Fixed PythonItemExporter and CSVExporter for non-string item types (issue 1737 [https://github.com/scrapy/scrapy/issues/1737]).

Various logging related fixes (issue 1294 [https://github.com/scrapy/scrapy/issues/1294], issue 1419 [https://github.com/scrapy/scrapy/issues/1419], issue 1263 [https://github.com/scrapy/scrapy/issues/1263], issue 1624 [https://github.com/scrapy/scrapy/issues/1624], issue 1654 [https://github.com/scrapy/scrapy/issues/1654], issue 1722 [https://github.com/scrapy/scrapy/issues/1722], issue 1726 [https://github.com/scrapy/scrapy/issues/1726] and issue 1303 [https://github.com/scrapy/scrapy/issues/1303]).

Fixed bug in utils.template.render_templatefile() (issue 1212 [https://github.com/scrapy/scrapy/issues/1212]).

sitemaps extraction from robots.txt is now case-insensitive (issue 1902 [https://github.com/scrapy/scrapy/issues/1902]).

HTTPS+CONNECT tunnels could get mixed up when using multiple proxies to same remote host (issue 1912 [https://github.com/scrapy/scrapy/issues/1912]).

Scrapy 1.0.7 (2017-03-03)

Packaging fix: disallow unsupported Twisted versions in setup.py

Scrapy 1.0.6 (2016-05-04)

FIX: RetryMiddleware is now robust to non-standard HTTP status codes (issue 1857 [https://github.com/scrapy/scrapy/issues/1857])

FIX: Filestorage HTTP cache was checking wrong modified time (issue 1875 [https://github.com/scrapy/scrapy/issues/1875])

DOC: Support for Sphinx 1.4+ (issue 1893 [https://github.com/scrapy/scrapy/issues/1893])

DOC: Consistency in selectors examples (issue 1869 [https://github.com/scrapy/scrapy/issues/1869])

Scrapy 1.0.5 (2016-02-04)

FIX: [Backport] Ignore bogus links in LinkExtractors (fixes issue 907 [https://github.com/scrapy/scrapy/issues/907], commit 108195e [https://github.com/scrapy/scrapy/commit/108195e])

TST: Changed buildbot makefile to use ‘pytest’ (commit 1f3d90a [https://github.com/scrapy/scrapy/commit/1f3d90a])

DOC: Fixed typos in tutorial and media-pipeline (commit 808a9ea [https://github.com/scrapy/scrapy/commit/808a9ea] and commit 803bd87 [https://github.com/scrapy/scrapy/commit/803bd87])

DOC: Add AjaxCrawlMiddleware to DOWNLOADER_MIDDLEWARES_BASE in settings docs (commit aa94121 [https://github.com/scrapy/scrapy/commit/aa94121])

Scrapy 1.0.4 (2015-12-30)

Ignoring xlib/tx folder, depending on Twisted version. (commit 7dfa979 [https://github.com/scrapy/scrapy/commit/7dfa979])

Run on new travis-ci infra (commit 6e42f0b [https://github.com/scrapy/scrapy/commit/6e42f0b])

Spelling fixes (commit 823a1cc [https://github.com/scrapy/scrapy/commit/823a1cc])

escape nodename in xmliter regex (commit da3c155 [https://github.com/scrapy/scrapy/commit/da3c155])

test xml nodename with dots (commit 4418fc3 [https://github.com/scrapy/scrapy/commit/4418fc3])

TST don’t use broken Pillow version in tests (commit a55078c [https://github.com/scrapy/scrapy/commit/a55078c])

disable log on version command. closes #1426 (commit 86fc330 [https://github.com/scrapy/scrapy/commit/86fc330])

disable log on startproject command (commit db4c9fe [https://github.com/scrapy/scrapy/commit/db4c9fe])

Add PyPI download stats badge (commit df2b944 [https://github.com/scrapy/scrapy/commit/df2b944])

don’t run tests twice on Travis if a PR is made from a scrapy/scrapy branch (commit a83ab41 [https://github.com/scrapy/scrapy/commit/a83ab41])

Add Python 3 porting status badge to the README (commit 73ac80d [https://github.com/scrapy/scrapy/commit/73ac80d])

fixed RFPDupeFilter persistence (commit 97d080e [https://github.com/scrapy/scrapy/commit/97d080e])

TST a test to show that dupefilter persistence is not working (commit 97f2fb3 [https://github.com/scrapy/scrapy/commit/97f2fb3])

explicit close file on file:// scheme handler (commit d9b4850 [https://github.com/scrapy/scrapy/commit/d9b4850])

Disable dupefilter in shell (commit c0d0734 [https://github.com/scrapy/scrapy/commit/c0d0734])

DOC: Add captions to toctrees which appear in sidebar (commit aa239ad [https://github.com/scrapy/scrapy/commit/aa239ad])

DOC Removed pywin32 from install instructions as it’s already declared as dependency. (commit 10eb400 [https://github.com/scrapy/scrapy/commit/10eb400])

Added installation notes about using Conda for Windows and other OSes. (commit 1c3600a [https://github.com/scrapy/scrapy/commit/1c3600a])

Fixed minor grammar issues. (commit 7f4ddd5 [https://github.com/scrapy/scrapy/commit/7f4ddd5])

fixed a typo in the documentation. (commit b71f677 [https://github.com/scrapy/scrapy/commit/b71f677])

Version 1 now exists (commit 5456c0e [https://github.com/scrapy/scrapy/commit/5456c0e])

fix another invalid xpath error (commit 0a1366e [https://github.com/scrapy/scrapy/commit/0a1366e])

fix ValueError: Invalid XPath: //div/[id=」not-exists」]/text() on selectors.rst (commit ca8d60f [https://github.com/scrapy/scrapy/commit/ca8d60f])

Typos corrections (commit 7067117 [https://github.com/scrapy/scrapy/commit/7067117])

fix typos in downloader-middleware.rst and exceptions.rst, middlware -> middleware (commit 32f115c [https://github.com/scrapy/scrapy/commit/32f115c])

Add note to ubuntu install section about debian compatibility (commit 23fda69 [https://github.com/scrapy/scrapy/commit/23fda69])

Replace alternative OSX install workaround with virtualenv (commit 98b63ee [https://github.com/scrapy/scrapy/commit/98b63ee])

Reference Homebrew’s homepage for installation instructions (commit 1925db1 [https://github.com/scrapy/scrapy/commit/1925db1])

Add oldest supported tox version to contributing docs (commit 5d10d6d [https://github.com/scrapy/scrapy/commit/5d10d6d])

Note in install docs about pip being already included in python>=2.7.9 (commit 85c980e [https://github.com/scrapy/scrapy/commit/85c980e])

Add non-python dependencies to Ubuntu install section in the docs (commit fbd010d [https://github.com/scrapy/scrapy/commit/fbd010d])

Add OS X installation section to docs (commit d8f4cba [https://github.com/scrapy/scrapy/commit/d8f4cba])

DOC(ENH): specify path to rtd theme explicitly (commit de73b1a [https://github.com/scrapy/scrapy/commit/de73b1a])

minor: scrapy.Spider docs grammar (commit 1ddcc7b [https://github.com/scrapy/scrapy/commit/1ddcc7b])

Make common practices sample code match the comments (commit 1b85bcf [https://github.com/scrapy/scrapy/commit/1b85bcf])

nextcall repetitive calls (heartbeats). (commit 55f7104 [https://github.com/scrapy/scrapy/commit/55f7104])

Backport fix compatibility with Twisted 15.4.0 (commit b262411 [https://github.com/scrapy/scrapy/commit/b262411])

pin pytest to 2.7.3 (commit a6535c2 [https://github.com/scrapy/scrapy/commit/a6535c2])

Merge pull request #1512 from mgedmin/patch-1 (commit 8876111 [https://github.com/scrapy/scrapy/commit/8876111])

Merge pull request #1513 from mgedmin/patch-2 (commit 5d4daf8 [https://github.com/scrapy/scrapy/commit/5d4daf8])

Typo (commit f8d0682 [https://github.com/scrapy/scrapy/commit/f8d0682])

Fix list formatting (commit 5f83a93 [https://github.com/scrapy/scrapy/commit/5f83a93])

fix scrapy squeue tests after recent changes to queuelib (commit 3365c01 [https://github.com/scrapy/scrapy/commit/3365c01])

Merge pull request #1475 from rweindl/patch-1 (commit 2d688cd [https://github.com/scrapy/scrapy/commit/2d688cd])

Update tutorial.rst (commit fbc1f25 [https://github.com/scrapy/scrapy/commit/fbc1f25])

Merge pull request #1449 from rhoekman/patch-1 (commit 7d6538c [https://github.com/scrapy/scrapy/commit/7d6538c])

Small grammatical change (commit 8752294 [https://github.com/scrapy/scrapy/commit/8752294])

Add openssl version to version command (commit 13c45ac [https://github.com/scrapy/scrapy/commit/13c45ac])

Scrapy 1.0.3 (2015-08-11)

add service_identity to scrapy install_requires (commit cbc2501 [https://github.com/scrapy/scrapy/commit/cbc2501])

Workaround for travis#296 (commit 66af9cd [https://github.com/scrapy/scrapy/commit/66af9cd])

Scrapy 1.0.2 (2015-08-06)

Twisted 15.3.0 does not raises PicklingError serializing lambda functions (commit b04dd7d [https://github.com/scrapy/scrapy/commit/b04dd7d])

Minor method name fix (commit 6f85c7f [https://github.com/scrapy/scrapy/commit/6f85c7f])

minor: scrapy.Spider grammar and clarity (commit 9c9d2e0 [https://github.com/scrapy/scrapy/commit/9c9d2e0])

Put a blurb about support channels in CONTRIBUTING (commit c63882b [https://github.com/scrapy/scrapy/commit/c63882b])

Fixed typos (commit a9ae7b0 [https://github.com/scrapy/scrapy/commit/a9ae7b0])

Fix doc reference. (commit 7c8a4fe [https://github.com/scrapy/scrapy/commit/7c8a4fe])

Scrapy 1.0.1 (2015-07-01)

Unquote request path before passing to FTPClient, it already escape paths (commit cc00ad2 [https://github.com/scrapy/scrapy/commit/cc00ad2])

include tests/ to source distribution in MANIFEST.in (commit eca227e [https://github.com/scrapy/scrapy/commit/eca227e])

DOC Fix SelectJmes documentation (commit b8567bc [https://github.com/scrapy/scrapy/commit/b8567bc])

DOC Bring Ubuntu and Archlinux outside of Windows subsection (commit 392233f [https://github.com/scrapy/scrapy/commit/392233f])

DOC remove version suffix from ubuntu package (commit 5303c66 [https://github.com/scrapy/scrapy/commit/5303c66])

DOC Update release date for 1.0 (commit c89fa29 [https://github.com/scrapy/scrapy/commit/c89fa29])

Scrapy 1.0.0 (2015-06-19)

You will find a lot of new features and bugfixes in this major release. Make sure to check our updated overview to get a glance of some of the changes, along with our brushed tutorial.

Support for returning dictionaries in spiders

Declaring and returning Scrapy Items is no longer necessary to collect the scraped data from your spider, you can now return explicit dictionaries instead.

Classic version

class MyItem(scrapy.Item): url = scrapy.Field() class MySpider(scrapy.Spider): def parse(self, response): return MyItem(url=response.url)

New version

class MySpider(scrapy.Spider): def parse(self, response): return {'url': response.url}

Per-spider settings (GSoC 2014)

Last Google Summer of Code project accomplished an important redesign of the mechanism used for populating settings, introducing explicit priorities to override any given setting. As an extension of that goal, we included a new level of priority for settings that act exclusively for a single spider, allowing them to redefine project settings.

Start using it by defining a custom_settings class variable in your spider:

class MySpider(scrapy.Spider): custom_settings = { "DOWNLOAD_DELAY": 5.0, "RETRY_ENABLED": False, }

Read more about settings population: Settings

Python Logging

Scrapy 1.0 has moved away from Twisted logging to support Python built in’s as default logging system. We’re maintaining backward compatibility for most of the old custom interface to call logging functions, but you’ll get warnings to switch to the Python logging API entirely.

Old version

from scrapy import log log.msg('MESSAGE', log.INFO)

New version

import logging logging.info('MESSAGE')

Logging with spiders remains the same, but on top of the log() method you’ll have access to a custom logger created for the spider to issue log events:

class MySpider(scrapy.Spider): def parse(self, response): self.logger.info('Response received')

Read more in the logging documentation: Logging

Crawler API refactoring (GSoC 2014)

Another milestone for last Google Summer of Code was a refactoring of the internal API, seeking a simpler and easier usage. Check new core interface in: Core API

A common situation where you will face these changes is while running Scrapy from scripts. Here’s a quick example of how to run a Spider manually with the new API:

from scrapy.crawler import CrawlerProcess process = CrawlerProcess({ 'USER_AGENT': 'Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1)' }) process.crawl(MySpider) process.start()

Bear in mind this feature is still under development and its API may change until it reaches a stable status.

See more examples for scripts running Scrapy: Common Practices

Module Relocations

There’s been a large rearrangement of modules trying to improve the general structure of Scrapy. Main changes were separating various subpackages into new projects and dissolving both scrapy.contrib and scrapy.contrib_exp into top level packages. Backward compatibility was kept among internal relocations, while importing deprecated modules expect warnings indicating their new place.

Full list of relocations

Outsourced packages

Note

These extensions went through some minor changes, e.g. some setting names were changed. Please check the documentation in each new repository to get familiar with the new usage.

Old location

New location

scrapy.commands.deploy

scrapyd-client (See other alternatives here: Deploying Spiders)

scrapy.contrib.djangoitem

scrapy-djangoitem

scrapy.webservice

scrapy-jsonrpc

scrapy.contrib_exp and scrapy.contrib dissolutions

Old location

New location

scrapy.contrib_exp.downloadermiddleware.decompression

scrapy.downloadermiddlewares.decompression

scrapy.contrib_exp.iterators

scrapy.utils.iterators

scrapy.contrib.downloadermiddleware

scrapy.downloadermiddlewares

scrapy.contrib.exporter

scrapy.exporters

scrapy.contrib.linkextractors

scrapy.linkextractors

scrapy.contrib.loader

scrapy.loader

scrapy.contrib.loader.processor

scrapy.loader.processors

scrapy.contrib.pipeline

scrapy.pipelines

scrapy.contrib.spidermiddleware

scrapy.spidermiddlewares

scrapy.contrib.spiders

scrapy.spiders

scrapy.contrib.closespider

scrapy.contrib.corestats

scrapy.contrib.debug

scrapy.contrib.feedexport

scrapy.contrib.httpcache

scrapy.contrib.logstats

scrapy.contrib.memdebug

scrapy.contrib.memusage

scrapy.contrib.spiderstate

scrapy.contrib.statsmailer

scrapy.contrib.throttle

scrapy.extensions.*

Plural renames and Modules unification

Old location

New location

scrapy.command

scrapy.commands

scrapy.dupefilter

scrapy.dupefilters

scrapy.linkextractor

scrapy.linkextractors

scrapy.spider

scrapy.spiders

scrapy.squeue

scrapy.squeues

scrapy.statscol

scrapy.statscollectors

scrapy.utils.decorator

scrapy.utils.decorators

Class renames

Old location

New location

scrapy.spidermanager.SpiderManager

scrapy.spiderloader.SpiderLoader

Settings renames

Old location

New location

SPIDER_MANAGER_CLASS

SPIDER_LOADER_CLASS

Changelog

New Features and Enhancements

Python logging (issue 1060 [https://github.com/scrapy/scrapy/issues/1060], issue 1235 [https://github.com/scrapy/scrapy/issues/1235], issue 1236 [https://github.com/scrapy/scrapy/issues/1236], issue 1240 [https://github.com/scrapy/scrapy/issues/1240], issue 1259 [https://github.com/scrapy/scrapy/issues/1259], issue 1278 [https://github.com/scrapy/scrapy/issues/1278], issue 1286 [https://github.com/scrapy/scrapy/issues/1286])

FEED_EXPORT_FIELDS option (issue 1159 [https://github.com/scrapy/scrapy/issues/1159], issue 1224 [https://github.com/scrapy/scrapy/issues/1224])

Dns cache size and timeout options (issue 1132 [https://github.com/scrapy/scrapy/issues/1132])

support namespace prefix in xmliter_lxml (issue 963 [https://github.com/scrapy/scrapy/issues/963])

Reactor threadpool max size setting (issue 1123 [https://github.com/scrapy/scrapy/issues/1123])

Allow spiders to return dicts. (issue 1081 [https://github.com/scrapy/scrapy/issues/1081])

Add Response.urljoin() helper (issue 1086 [https://github.com/scrapy/scrapy/issues/1086])

look in ~/.config/scrapy.cfg for user config (issue 1098 [https://github.com/scrapy/scrapy/issues/1098])

handle TLS SNI (issue 1101 [https://github.com/scrapy/scrapy/issues/1101])

Selectorlist extract first (issue 624 [https://github.com/scrapy/scrapy/issues/624], issue 1145 [https://github.com/scrapy/scrapy/issues/1145])

Added JmesSelect (issue 1016 [https://github.com/scrapy/scrapy/issues/1016])

add gzip compression to filesystem http cache backend (issue 1020 [https://github.com/scrapy/scrapy/issues/1020])

CSS support in link extractors (issue 983 [https://github.com/scrapy/scrapy/issues/983])

httpcache dont_cache meta #19 #689 (issue 821 [https://github.com/scrapy/scrapy/issues/821])

add signal to be sent when request is dropped by the scheduler (issue 961 [https://github.com/scrapy/scrapy/issues/961])

avoid download large response (issue 946 [https://github.com/scrapy/scrapy/issues/946])

Allow to specify the quotechar in CSVFeedSpider (issue 882 [https://github.com/scrapy/scrapy/issues/882])

Add referer to「Spider error processing」log message (issue 795 [https://github.com/scrapy/scrapy/issues/795])

process robots.txt once (issue 896 [https://github.com/scrapy/scrapy/issues/896])

GSoC Per-spider settings (issue 854 [https://github.com/scrapy/scrapy/issues/854])

Add project name validation (issue 817 [https://github.com/scrapy/scrapy/issues/817])

GSoC API cleanup (issue 816 [https://github.com/scrapy/scrapy/issues/816], issue 1128 [https://github.com/scrapy/scrapy/issues/1128], issue 1147 [https://github.com/scrapy/scrapy/issues/1147], issue 1148 [https://github.com/scrapy/scrapy/issues/1148], issue 1156 [https://github.com/scrapy/scrapy/issues/1156], issue 1185 [https://github.com/scrapy/scrapy/issues/1185], issue 1187 [https://github.com/scrapy/scrapy/issues/1187], issue 1258 [https://github.com/scrapy/scrapy/issues/1258], issue 1268 [https://github.com/scrapy/scrapy/issues/1268], issue 1276 [https://github.com/scrapy/scrapy/issues/1276], issue 1285 [https://github.com/scrapy/scrapy/issues/1285], issue 1284 [https://github.com/scrapy/scrapy/issues/1284])

Be more responsive with IO operations (issue 1074 [https://github.com/scrapy/scrapy/issues/1074] and issue 1075 [https://github.com/scrapy/scrapy/issues/1075])

Do leveldb compaction for httpcache on closing (issue 1297 [https://github.com/scrapy/scrapy/issues/1297])

Deprecations and Removals

Deprecate htmlparser link extractor (issue 1205 [https://github.com/scrapy/scrapy/issues/1205])

remove deprecated code from FeedExporter (issue 1155 [https://github.com/scrapy/scrapy/issues/1155])

a leftover for.15 compatibility (issue 925 [https://github.com/scrapy/scrapy/issues/925])

drop support for CONCURRENT_REQUESTS_PER_SPIDER (issue 895 [https://github.com/scrapy/scrapy/issues/895])

Drop old engine code (issue 911 [https://github.com/scrapy/scrapy/issues/911])

Deprecate SgmlLinkExtractor (issue 777 [https://github.com/scrapy/scrapy/issues/777])

Relocations

Move exporters/__init__.py to exporters.py (issue 1242 [https://github.com/scrapy/scrapy/issues/1242])

Move base classes to their packages (issue 1218 [https://github.com/scrapy/scrapy/issues/1218], issue 1233 [https://github.com/scrapy/scrapy/issues/1233])

Module relocation (issue 1181 [https://github.com/scrapy/scrapy/issues/1181], issue 1210 [https://github.com/scrapy/scrapy/issues/1210])

rename SpiderManager to SpiderLoader (issue 1166 [https://github.com/scrapy/scrapy/issues/1166])

Remove djangoitem (issue 1177 [https://github.com/scrapy/scrapy/issues/1177])

remove scrapy deploy command (issue 1102 [https://github.com/scrapy/scrapy/issues/1102])

dissolve contrib_exp (issue 1134 [https://github.com/scrapy/scrapy/issues/1134])

Deleted bin folder from root, fixes #913 (issue 914 [https://github.com/scrapy/scrapy/issues/914])

Remove jsonrpc based webservice (issue 859 [https://github.com/scrapy/scrapy/issues/859])

Move Test cases under project root dir (issue 827 [https://github.com/scrapy/scrapy/issues/827], issue 841 [https://github.com/scrapy/scrapy/issues/841])

Fix backward incompatibility for relocated paths in settings (issue 1267 [https://github.com/scrapy/scrapy/issues/1267])

Documentation

CrawlerProcess documentation (issue 1190 [https://github.com/scrapy/scrapy/issues/1190])

Favoring web scraping over screen scraping in the descriptions (issue 1188 [https://github.com/scrapy/scrapy/issues/1188])

Some improvements for Scrapy tutorial (issue 1180 [https://github.com/scrapy/scrapy/issues/1180])

Documenting Files Pipeline together with Images Pipeline (issue 1150 [https://github.com/scrapy/scrapy/issues/1150])

deployment docs tweaks (issue 1164 [https://github.com/scrapy/scrapy/issues/1164])

Added deployment section covering scrapyd-deploy and shub (issue 1124 [https://github.com/scrapy/scrapy/issues/1124])

Adding more settings to project template (issue 1073 [https://github.com/scrapy/scrapy/issues/1073])

some improvements to overview page (issue 1106 [https://github.com/scrapy/scrapy/issues/1106])

Updated link in docs/topics/architecture.rst (issue 647 [https://github.com/scrapy/scrapy/issues/647])

DOC reorder topics (issue 1022 [https://github.com/scrapy/scrapy/issues/1022])

updating list of Request.meta special keys (issue 1071 [https://github.com/scrapy/scrapy/issues/1071])

DOC document download_timeout (issue 898 [https://github.com/scrapy/scrapy/issues/898])

DOC simplify extension docs (issue 893 [https://github.com/scrapy/scrapy/issues/893])

Leaks docs (issue 894 [https://github.com/scrapy/scrapy/issues/894])

DOC document from_crawler method for item pipelines (issue 904 [https://github.com/scrapy/scrapy/issues/904])

Spider_error doesn’t support deferreds (issue 1292 [https://github.com/scrapy/scrapy/issues/1292])

Corrections & Sphinx related fixes (issue 1220 [https://github.com/scrapy/scrapy/issues/1220], issue 1219 [https://github.com/scrapy/scrapy/issues/1219], issue 1196 [https://github.com/scrapy/scrapy/issues/1196], issue 1172 [https://github.com/scrapy/scrapy/issues/1172], issue 1171 [https://github.com/scrapy/scrapy/issues/1171], issue 1169 [https://github.com/scrapy/scrapy/issues/1169], issue 1160 [https://github.com/scrapy/scrapy/issues/1160], issue 1154 [https://github.com/scrapy/scrapy/issues/1154], issue 1127 [https://github.com/scrapy/scrapy/issues/1127], issue 1112 [https://github.com/scrapy/scrapy/issues/1112], issue 1105 [https://github.com/scrapy/scrapy/issues/1105], issue 1041 [https://github.com/scrapy/scrapy/issues/1041], issue 1082 [https://github.com/scrapy/scrapy/issues/1082], issue 1033 [https://github.com/scrapy/scrapy/issues/1033], issue 944 [https://github.com/scrapy/scrapy/issues/944], issue 866 [https://github.com/scrapy/scrapy/issues/866], issue 864 [https://github.com/scrapy/scrapy/issues/864], issue 796 [https://github.com/scrapy/scrapy/issues/796], issue 1260 [https://github.com/scrapy/scrapy/issues/1260], issue 1271 [https://github.com/scrapy/scrapy/issues/1271], issue 1293 [https://github.com/scrapy/scrapy/issues/1293], issue 1298 [https://github.com/scrapy/scrapy/issues/1298])

Bugfixes

Item multi inheritance fix (issue 353 [https://github.com/scrapy/scrapy/issues/353], issue 1228 [https://github.com/scrapy/scrapy/issues/1228])

ItemLoader.load_item: iterate over copy of fields (issue 722 [https://github.com/scrapy/scrapy/issues/722])

Fix Unhandled error in Deferred (RobotsTxtMiddleware) (issue 1131 [https://github.com/scrapy/scrapy/issues/1131], issue 1197 [https://github.com/scrapy/scrapy/issues/1197])

Force to read DOWNLOAD_TIMEOUT as int (issue 954 [https://github.com/scrapy/scrapy/issues/954])

scrapy.utils.misc.load_object should print full traceback (issue 902 [https://github.com/scrapy/scrapy/issues/902])

Fix bug for「.local」host name (issue 878 [https://github.com/scrapy/scrapy/issues/878])

Fix for Enabled extensions, middlewares, pipelines info not printed anymore (issue 879 [https://github.com/scrapy/scrapy/issues/879])

fix dont_merge_cookies bad behaviour when set to false on meta (issue 846 [https://github.com/scrapy/scrapy/issues/846])

Python 3 In Progress Support

disable scrapy.telnet if twisted.conch is not available (issue 1161 [https://github.com/scrapy/scrapy/issues/1161])

fix Python 3 syntax errors in ajaxcrawl.py (issue 1162 [https://github.com/scrapy/scrapy/issues/1162])

more python3 compatibility changes for urllib (issue 1121 [https://github.com/scrapy/scrapy/issues/1121])

assertItemsEqual was renamed to assertCountEqual in Python 3. (issue 1070 [https://github.com/scrapy/scrapy/issues/1070])

Import unittest.mock if available. (issue 1066 [https://github.com/scrapy/scrapy/issues/1066])

updated deprecated cgi.parse_qsl to use six’s parse_qsl (issue 909 [https://github.com/scrapy/scrapy/issues/909])

Prevent Python 3 port regressions (issue 830 [https://github.com/scrapy/scrapy/issues/830])

PY3: use MutableMapping for python 3 (issue 810 [https://github.com/scrapy/scrapy/issues/810])

PY3: use six.BytesIO and six.moves.cStringIO (issue 803 [https://github.com/scrapy/scrapy/issues/803])

PY3: fix xmlrpclib and email imports (issue 801 [https://github.com/scrapy/scrapy/issues/801])

PY3: use six for robotparser and urlparse (issue 800 [https://github.com/scrapy/scrapy/issues/800])

PY3: use six.iterkeys, six.iteritems, and tempfile (issue 799 [https://github.com/scrapy/scrapy/issues/799])

PY3: fix has_key and use six.moves.configparser (issue 798 [https://github.com/scrapy/scrapy/issues/798])

PY3: use six.moves.cPickle (issue 797 [https://github.com/scrapy/scrapy/issues/797])

PY3 make it possible to run some tests in Python3 (issue 776 [https://github.com/scrapy/scrapy/issues/776])

Tests

remove unnecessary lines from py3-ignores (issue 1243 [https://github.com/scrapy/scrapy/issues/1243])

Fix remaining warnings from pytest while collecting tests (issue 1206 [https://github.com/scrapy/scrapy/issues/1206])

Add docs build to travis (issue 1234 [https://github.com/scrapy/scrapy/issues/1234])

TST don’t collect tests from deprecated modules. (issue 1165 [https://github.com/scrapy/scrapy/issues/1165])

install service_identity package in tests to prevent warnings (issue 1168 [https://github.com/scrapy/scrapy/issues/1168])

Fix deprecated settings API in tests (issue 1152 [https://github.com/scrapy/scrapy/issues/1152])

Add test for webclient with POST method and no body given (issue 1089 [https://github.com/scrapy/scrapy/issues/1089])

py3-ignores.txt supports comments (issue 1044 [https://github.com/scrapy/scrapy/issues/1044])

modernize some of the asserts (issue 835 [https://github.com/scrapy/scrapy/issues/835])

selector.__repr__ test (issue 779 [https://github.com/scrapy/scrapy/issues/779])

Code refactoring

CSVFeedSpider cleanup: use iterate_spider_output (issue 1079 [https://github.com/scrapy/scrapy/issues/1079])

remove unnecessary check from scrapy.utils.spider.iter_spider_output (issue 1078 [https://github.com/scrapy/scrapy/issues/1078])

Pydispatch pep8 (issue 992 [https://github.com/scrapy/scrapy/issues/992])

Removed unused ‘load=False’ parameter from walk_modules() (issue 871 [https://github.com/scrapy/scrapy/issues/871])

For consistency, use job_dir helper in SpiderState extension. (issue 805 [https://github.com/scrapy/scrapy/issues/805])

rename「sflo」local variables to less cryptic「log_observer」(issue 775 [https://github.com/scrapy/scrapy/issues/775])

Scrapy 0.24.6 (2015-04-20)

encode invalid xpath with unicode_escape under PY2 (commit 07cb3e5 [https://github.com/scrapy/scrapy/commit/07cb3e5])

fix IPython shell scope issue and load IPython user config (commit 2c8e573 [https://github.com/scrapy/scrapy/commit/2c8e573])

Fix small typo in the docs (commit d694019 [https://github.com/scrapy/scrapy/commit/d694019])

Fix small typo (commit f92fa83 [https://github.com/scrapy/scrapy/commit/f92fa83])

Converted sel.xpath() calls to response.xpath() in Extracting the data (commit c2c6d15 [https://github.com/scrapy/scrapy/commit/c2c6d15])

Scrapy 0.24.5 (2015-02-25)

Support new _getEndpoint Agent signatures on Twisted 15.0.0 (commit 540b9bc [https://github.com/scrapy/scrapy/commit/540b9bc])

DOC a couple more references are fixed (commit b4c454b [https://github.com/scrapy/scrapy/commit/b4c454b])

DOC fix a reference (commit e3c1260 [https://github.com/scrapy/scrapy/commit/e3c1260])

t.i.b.ThreadedResolver is now a new-style class (commit 9e13f42 [https://github.com/scrapy/scrapy/commit/9e13f42])

S3DownloadHandler: fix auth for requests with quoted paths/query params (commit cdb9a0b [https://github.com/scrapy/scrapy/commit/cdb9a0b])

fixed the variable types in mailsender documentation (commit bb3a848 [https://github.com/scrapy/scrapy/commit/bb3a848])

Reset items_scraped instead of item_count (commit edb07a4 [https://github.com/scrapy/scrapy/commit/edb07a4])

Tentative attention message about what document to read for contributions (commit 7ee6f7a [https://github.com/scrapy/scrapy/commit/7ee6f7a])

mitmproxy 0.10.1 needs netlib 0.10.1 too (commit 874fcdd [https://github.com/scrapy/scrapy/commit/874fcdd])

pin mitmproxy 0.10.1 as >0.11 does not work with tests (commit c6b21f0 [https://github.com/scrapy/scrapy/commit/c6b21f0])

Test the parse command locally instead of against an external url (commit c3a6628 [https://github.com/scrapy/scrapy/commit/c3a6628])

Patches Twisted issue while closing the connection pool on HTTPDownloadHandler (commit d0bf957 [https://github.com/scrapy/scrapy/commit/d0bf957])

Updates documentation on dynamic item classes. (commit eeb589a [https://github.com/scrapy/scrapy/commit/eeb589a])

Merge pull request #943 from Lazar-T/patch-3 (commit 5fdab02 [https://github.com/scrapy/scrapy/commit/5fdab02])

typo (commit b0ae199 [https://github.com/scrapy/scrapy/commit/b0ae199])

pywin32 is required by Twisted. closes #937 (commit 5cb0cfb [https://github.com/scrapy/scrapy/commit/5cb0cfb])

Update install.rst (commit 781286b [https://github.com/scrapy/scrapy/commit/781286b])

Merge pull request #928 from Lazar-T/patch-1 (commit b415d04 [https://github.com/scrapy/scrapy/commit/b415d04])

comma instead of fullstop (commit 627b9ba [https://github.com/scrapy/scrapy/commit/627b9ba])

Merge pull request #885 from jsma/patch-1 (commit de909ad [https://github.com/scrapy/scrapy/commit/de909ad])

Update request-response.rst (commit 3f3263d [https://github.com/scrapy/scrapy/commit/3f3263d])

SgmlLinkExtractor - fix for parsing <area> tag with Unicode present (commit 49b40f0 [https://github.com/scrapy/scrapy/commit/49b40f0])

Scrapy 0.24.4 (2014-08-09)

pem file is used by mockserver and required by scrapy bench (commit 5eddc68 [https://github.com/scrapy/scrapy/commit/5eddc68])

scrapy bench needs scrapy.tests* (commit d6cb999 [https://github.com/scrapy/scrapy/commit/d6cb999])

Scrapy 0.24.3 (2014-08-09)

no need to waste travis-ci time on py3 for 0.24 (commit 8e080c1 [https://github.com/scrapy/scrapy/commit/8e080c1])

Update installation docs (commit 1d0c096 [https://github.com/scrapy/scrapy/commit/1d0c096])

There is a trove classifier for Scrapy framework! (commit 4c701d7 [https://github.com/scrapy/scrapy/commit/4c701d7])

update other places where w3lib version is mentioned (commit d109c13 [https://github.com/scrapy/scrapy/commit/d109c13])

Update w3lib requirement to 1.8.0 (commit 39d2ce5 [https://github.com/scrapy/scrapy/commit/39d2ce5])

Use w3lib.html.replace_entities() (remove_entities() is deprecated) (commit 180d3ad [https://github.com/scrapy/scrapy/commit/180d3ad])

set zip_safe=False (commit a51ee8b [https://github.com/scrapy/scrapy/commit/a51ee8b])

do not ship tests package (commit ee3b371 [https://github.com/scrapy/scrapy/commit/ee3b371])

scrapy.bat is not needed anymore (commit c3861cf [https://github.com/scrapy/scrapy/commit/c3861cf])

Modernize setup.py (commit 362e322 [https://github.com/scrapy/scrapy/commit/362e322])

headers can not handle non-string values (commit 94a5c65 [https://github.com/scrapy/scrapy/commit/94a5c65])

fix ftp test cases (commit a274a7f [https://github.com/scrapy/scrapy/commit/a274a7f])

The sum up of travis-ci builds are taking like 50min to complete (commit ae1e2cc [https://github.com/scrapy/scrapy/commit/ae1e2cc])

Update shell.rst typo (commit e49c96a [https://github.com/scrapy/scrapy/commit/e49c96a])

removes weird indentation in the shell results (commit 1ca489d [https://github.com/scrapy/scrapy/commit/1ca489d])

improved explanations, clarified blog post as source, added link for XPath string functions in the spec (commit 65c8f05 [https://github.com/scrapy/scrapy/commit/65c8f05])

renamed UserTimeoutError and ServerTimeouterror #583 (commit 037f6ab [https://github.com/scrapy/scrapy/commit/037f6ab])

adding some xpath tips to selectors docs (commit 2d103e0 [https://github.com/scrapy/scrapy/commit/2d103e0])

fix tests to account for https://github.com/scrapy/w3lib/pull/23 (commit f8d366a [https://github.com/scrapy/scrapy/commit/f8d366a])

get_func_args maximum recursion fix #728 (commit 81344ea [https://github.com/scrapy/scrapy/commit/81344ea])

Updated input/ouput processor example according to #560. (commit f7c4ea8 [https://github.com/scrapy/scrapy/commit/f7c4ea8])

Fixed Python syntax in tutorial. (commit db59ed9 [https://github.com/scrapy/scrapy/commit/db59ed9])

Add test case for tunneling proxy (commit f090260 [https://github.com/scrapy/scrapy/commit/f090260])

Bugfix for leaking Proxy-Authorization header to remote host when using tunneling (commit d8793af [https://github.com/scrapy/scrapy/commit/d8793af])

Extract links from XHTML documents with MIME-Type「application/xml」(commit ed1f376 [https://github.com/scrapy/scrapy/commit/ed1f376])

Merge pull request #793 from roysc/patch-1 (commit 91a1106 [https://github.com/scrapy/scrapy/commit/91a1106])

Fix typo in commands.rst (commit 743e1e2 [https://github.com/scrapy/scrapy/commit/743e1e2])

better testcase for settings.overrides.setdefault (commit e22daaf [https://github.com/scrapy/scrapy/commit/e22daaf])

Using CRLF as line marker according to http 1.1 definition (commit 5ec430b [https://github.com/scrapy/scrapy/commit/5ec430b])

Scrapy 0.24.2 (2014-07-08)

Use a mutable mapping to proxy deprecated settings.overrides and settings.defaults attribute (commit e5e8133 [https://github.com/scrapy/scrapy/commit/e5e8133])

there is not support for python3 yet (commit 3cd6146 [https://github.com/scrapy/scrapy/commit/3cd6146])

Update python compatible version set to debian packages (commit fa5d76b [https://github.com/scrapy/scrapy/commit/fa5d76b])

DOC fix formatting in release notes (commit c6a9e20 [https://github.com/scrapy/scrapy/commit/c6a9e20])

Scrapy 0.24.1 (2014-06-27)

Fix deprecated CrawlerSettings and increase backward compatibility with .defaults attribute (commit 8e3f20a [https://github.com/scrapy/scrapy/commit/8e3f20a])

Scrapy 0.24.0 (2014-06-26)

Enhancements

Improve Scrapy top-level namespace (issue 494 [https://github.com/scrapy/scrapy/issues/494], issue 684 [https://github.com/scrapy/scrapy/issues/684])

Add selector shortcuts to responses (issue 554 [https://github.com/scrapy/scrapy/issues/554], issue 690 [https://github.com/scrapy/scrapy/issues/690])

Add new lxml based LinkExtractor to replace unmantained SgmlLinkExtractor (issue 559 [https://github.com/scrapy/scrapy/issues/559], issue 761 [https://github.com/scrapy/scrapy/issues/761], issue 763 [https://github.com/scrapy/scrapy/issues/763])

Cleanup settings API - part of per-spider settings GSoC project (issue 737 [https://github.com/scrapy/scrapy/issues/737])

Add UTF8 encoding header to templates (issue 688 [https://github.com/scrapy/scrapy/issues/688], issue 762 [https://github.com/scrapy/scrapy/issues/762])

Telnet console now binds to 127.0.0.1 by default (issue 699 [https://github.com/scrapy/scrapy/issues/699])

Update debian/ubuntu install instructions (issue 509 [https://github.com/scrapy/scrapy/issues/509], issue 549 [https://github.com/scrapy/scrapy/issues/549])

Disable smart strings in lxml XPath evaluations (issue 535 [https://github.com/scrapy/scrapy/issues/535])

Restore filesystem based cache as default for http cache middleware (issue 541 [https://github.com/scrapy/scrapy/issues/541], issue 500 [https://github.com/scrapy/scrapy/issues/500], issue 571 [https://github.com/scrapy/scrapy/issues/571])

Expose current crawler in Scrapy shell (issue 557 [https://github.com/scrapy/scrapy/issues/557])

Improve testsuite comparing CSV and XML exporters (issue 570 [https://github.com/scrapy/scrapy/issues/570])

New offsite/filtered and offsite/domains stats (issue 566 [https://github.com/scrapy/scrapy/issues/566])

Support process_links as generator in CrawlSpider (issue 555 [https://github.com/scrapy/scrapy/issues/555])

Verbose logging and new stats counters for DupeFilter (issue 553 [https://github.com/scrapy/scrapy/issues/553])

Add a mimetype parameter to MailSender.send() (issue 602 [https://github.com/scrapy/scrapy/issues/602])

Generalize file pipeline log messages (issue 622 [https://github.com/scrapy/scrapy/issues/622])

Replace unencodeable codepoints with html entities in SGMLLinkExtractor (issue 565 [https://github.com/scrapy/scrapy/issues/565])

Converted SEP documents to rst format (issue 629 [https://github.com/scrapy/scrapy/issues/629], issue 630 [https://github.com/scrapy/scrapy/issues/630], issue 638 [https://github.com/scrapy/scrapy/issues/638], issue 632 [https://github.com/scrapy/scrapy/issues/632], issue 636 [https://github.com/scrapy/scrapy/issues/636], issue 640 [https://github.com/scrapy/scrapy/issues/640], issue 635 [https://github.com/scrapy/scrapy/issues/635], issue 634 [https://github.com/scrapy/scrapy/issues/634], issue 639 [https://github.com/scrapy/scrapy/issues/639], issue 637 [https://github.com/scrapy/scrapy/issues/637], issue 631 [https://github.com/scrapy/scrapy/issues/631], issue 633 [https://github.com/scrapy/scrapy/issues/633], issue 641 [https://github.com/scrapy/scrapy/issues/641], issue 642 [https://github.com/scrapy/scrapy/issues/642])

Tests and docs for clickdata’s nr index in FormRequest (issue 646 [https://github.com/scrapy/scrapy/issues/646], issue 645 [https://github.com/scrapy/scrapy/issues/645])

Allow to disable a downloader handler just like any other component (issue 650 [https://github.com/scrapy/scrapy/issues/650])

Log when a request is discarded after too many redirections (issue 654 [https://github.com/scrapy/scrapy/issues/654])

Log error responses if they are not handled by spider callbacks (issue 612 [https://github.com/scrapy/scrapy/issues/612], issue 656 [https://github.com/scrapy/scrapy/issues/656])

Add content-type check to http compression mw (issue 193 [https://github.com/scrapy/scrapy/issues/193], issue 660 [https://github.com/scrapy/scrapy/issues/660])

Run pypy tests using latest pypi from ppa (issue 674 [https://github.com/scrapy/scrapy/issues/674])

Run test suite using pytest instead of trial (issue 679 [https://github.com/scrapy/scrapy/issues/679])

Build docs and check for dead links in tox environment (issue 687 [https://github.com/scrapy/scrapy/issues/687])

Make scrapy.version_info a tuple of integers (issue 681 [https://github.com/scrapy/scrapy/issues/681], issue 692 [https://github.com/scrapy/scrapy/issues/692])

Infer exporter’s output format from filename extensions (issue 546 [https://github.com/scrapy/scrapy/issues/546], issue 659 [https://github.com/scrapy/scrapy/issues/659], issue 760 [https://github.com/scrapy/scrapy/issues/760])

Support case-insensitive domains in url_is_from_any_domain() (issue 693 [https://github.com/scrapy/scrapy/issues/693])

Remove pep8 warnings in project and spider templates (issue 698 [https://github.com/scrapy/scrapy/issues/698])

Tests and docs for request_fingerprint function (issue 597 [https://github.com/scrapy/scrapy/issues/597])

Update SEP-19 for GSoC project per-spider settings (issue 705 [https://github.com/scrapy/scrapy/issues/705])

Set exit code to non-zero when contracts fails (issue 727 [https://github.com/scrapy/scrapy/issues/727])

Add a setting to control what class is instanciated as Downloader component (issue 738 [https://github.com/scrapy/scrapy/issues/738])

Pass response in item_dropped signal (issue 724 [https://github.com/scrapy/scrapy/issues/724])

Improve scrapy check contracts command (issue 733 [https://github.com/scrapy/scrapy/issues/733], issue 752 [https://github.com/scrapy/scrapy/issues/752])

Document spider.closed() shortcut (issue 719 [https://github.com/scrapy/scrapy/issues/719])

Document request_scheduled signal (issue 746 [https://github.com/scrapy/scrapy/issues/746])

Add a note about reporting security issues (issue 697 [https://github.com/scrapy/scrapy/issues/697])

Add LevelDB http cache storage backend (issue 626 [https://github.com/scrapy/scrapy/issues/626], issue 500 [https://github.com/scrapy/scrapy/issues/500])

Sort spider list output of scrapy list command (issue 742 [https://github.com/scrapy/scrapy/issues/742])

Multiple documentation enhancemens and fixes (issue 575 [https://github.com/scrapy/scrapy/issues/575], issue 587 [https://github.com/scrapy/scrapy/issues/587], issue 590 [https://github.com/scrapy/scrapy/issues/590], issue 596 [https://github.com/scrapy/scrapy/issues/596], issue 610 [https://github.com/scrapy/scrapy/issues/610], issue 617 [https://github.com/scrapy/scrapy/issues/617], issue 618 [https://github.com/scrapy/scrapy/issues/618], issue 627 [https://github.com/scrapy/scrapy/issues/627], issue 613 [https://github.com/scrapy/scrapy/issues/613], issue 643 [https://github.com/scrapy/scrapy/issues/643], issue 654 [https://github.com/scrapy/scrapy/issues/654], issue 675 [https://github.com/scrapy/scrapy/issues/675], issue 663 [https://github.com/scrapy/scrapy/issues/663], issue 711 [https://github.com/scrapy/scrapy/issues/711], issue 714 [https://github.com/scrapy/scrapy/issues/714])

Bugfixes

Encode unicode URL value when creating Links in RegexLinkExtractor (issue 561 [https://github.com/scrapy/scrapy/issues/561])

Ignore None values in ItemLoader processors (issue 556 [https://github.com/scrapy/scrapy/issues/556])

Fix link text when there is an inner tag in SGMLLinkExtractor and HtmlParserLinkExtractor (issue 485 [https://github.com/scrapy/scrapy/issues/485], issue 574 [https://github.com/scrapy/scrapy/issues/574])

Fix wrong checks on subclassing of deprecated classes (issue 581 [https://github.com/scrapy/scrapy/issues/581], issue 584 [https://github.com/scrapy/scrapy/issues/584])

Handle errors caused by inspect.stack() failures (issue 582 [https://github.com/scrapy/scrapy/issues/582])

Fix a reference to unexistent engine attribute (issue 593 [https://github.com/scrapy/scrapy/issues/593], issue 594 [https://github.com/scrapy/scrapy/issues/594])

Fix dynamic itemclass example usage of type() (issue 603 [https://github.com/scrapy/scrapy/issues/603])

Use lucasdemarchi/codespell to fix typos (issue 628 [https://github.com/scrapy/scrapy/issues/628])

Fix default value of attrs argument in SgmlLinkExtractor to be tuple (issue 661 [https://github.com/scrapy/scrapy/issues/661])

Fix XXE flaw in sitemap reader (issue 676 [https://github.com/scrapy/scrapy/issues/676])

Fix engine to support filtered start requests (issue 707 [https://github.com/scrapy/scrapy/issues/707])

Fix offsite middleware case on urls with no hostnames (issue 745 [https://github.com/scrapy/scrapy/issues/745])

Testsuite doesn’t require PIL anymore (issue 585 [https://github.com/scrapy/scrapy/issues/585])

Scrapy 0.22.2 (released 2014-02-14)

fix a reference to unexistent engine.slots. closes #593 (commit 13c099a [https://github.com/scrapy/scrapy/commit/13c099a])

downloaderMW doc typo (spiderMW doc copy remnant) (commit 8ae11bf [https://github.com/scrapy/scrapy/commit/8ae11bf])

Correct typos (commit 1346037 [https://github.com/scrapy/scrapy/commit/1346037])

Scrapy 0.22.1 (released 2014-02-08)

localhost666 can resolve under certain circumstances (commit 2ec2279 [https://github.com/scrapy/scrapy/commit/2ec2279])

test inspect.stack failure (commit cc3eda3 [https://github.com/scrapy/scrapy/commit/cc3eda3])

Handle cases when inspect.stack() fails (commit 8cb44f9 [https://github.com/scrapy/scrapy/commit/8cb44f9])

Fix wrong checks on subclassing of deprecated classes. closes #581 (commit 46d98d6 [https://github.com/scrapy/scrapy/commit/46d98d6])

Docs: 4-space indent for final spider example (commit 13846de [https://github.com/scrapy/scrapy/commit/13846de])

Fix HtmlParserLinkExtractor and tests after #485 merge (commit 368a946 [https://github.com/scrapy/scrapy/commit/368a946])

BaseSgmlLinkExtractor: Fixed the missing space when the link has an inner tag (commit b566388 [https://github.com/scrapy/scrapy/commit/b566388])

BaseSgmlLinkExtractor: Added unit test of a link with an inner tag (commit c1cb418 [https://github.com/scrapy/scrapy/commit/c1cb418])

BaseSgmlLinkExtractor: Fixed unknown_endtag() so that it only set current_link=None when the end tag match the opening tag (commit 7e4d627 [https://github.com/scrapy/scrapy/commit/7e4d627])

Fix tests for Travis-CI build (commit 76c7e20 [https://github.com/scrapy/scrapy/commit/76c7e20])

replace unencodeable codepoints with html entities. fixes #562 and #285 (commit 5f87b17 [https://github.com/scrapy/scrapy/commit/5f87b17])

RegexLinkExtractor: encode URL unicode value when creating Links (commit d0ee545 [https://github.com/scrapy/scrapy/commit/d0ee545])

Updated the tutorial crawl output with latest output. (commit 8da65de [https://github.com/scrapy/scrapy/commit/8da65de])

Updated shell docs with the crawler reference and fixed the actual shell output. (commit 875b9ab [https://github.com/scrapy/scrapy/commit/875b9ab])

PEP8 minor edits. (commit f89efaf [https://github.com/scrapy/scrapy/commit/f89efaf])

Expose current crawler in the scrapy shell. (commit 5349cec [https://github.com/scrapy/scrapy/commit/5349cec])

Unused re import and PEP8 minor edits. (commit 387f414 [https://github.com/scrapy/scrapy/commit/387f414])

Ignore None’s values when using the ItemLoader. (commit 0632546 [https://github.com/scrapy/scrapy/commit/0632546])

DOC Fixed HTTPCACHE_STORAGE typo in the default value which is now Filesystem instead Dbm. (commit cde9a8c [https://github.com/scrapy/scrapy/commit/cde9a8c])

show ubuntu setup instructions as literal code (commit fb5c9c5 [https://github.com/scrapy/scrapy/commit/fb5c9c5])

Update Ubuntu installation instructions (commit 70fb105 [https://github.com/scrapy/scrapy/commit/70fb105])

Merge pull request #550 from stray-leone/patch-1 (commit 6f70b6a [https://github.com/scrapy/scrapy/commit/6f70b6a])

modify the version of scrapy ubuntu package (commit 725900d [https://github.com/scrapy/scrapy/commit/725900d])

fix 0.22.0 release date (commit af0219a [https://github.com/scrapy/scrapy/commit/af0219a])

fix typos in news.rst and remove (not released yet) header (commit b7f58f4 [https://github.com/scrapy/scrapy/commit/b7f58f4])

Scrapy 0.22.0 (released 2014-01-17)

Enhancements

[Backward incompatible] Switched HTTPCacheMiddleware backend to filesystem (issue 541 [https://github.com/scrapy/scrapy/issues/541]) To restore old backend set HTTPCACHE_STORAGE to scrapy.contrib.httpcache.DbmCacheStorage

Proxy https:// urls using CONNECT method (issue 392 [https://github.com/scrapy/scrapy/issues/392], issue 397 [https://github.com/scrapy/scrapy/issues/397])

Add a middleware to crawl ajax crawleable pages as defined by google (issue 343 [https://github.com/scrapy/scrapy/issues/343])

Rename scrapy.spider.BaseSpider to scrapy.spider.Spider (issue 510 [https://github.com/scrapy/scrapy/issues/510], issue 519 [https://github.com/scrapy/scrapy/issues/519])

Selectors register EXSLT namespaces by default (issue 472 [https://github.com/scrapy/scrapy/issues/472])

Unify item loaders similar to selectors renaming (issue 461 [https://github.com/scrapy/scrapy/issues/461])

Make RFPDupeFilter class easily subclassable (issue 533 [https://github.com/scrapy/scrapy/issues/533])

Improve test coverage and forthcoming Python 3 support (issue 525 [https://github.com/scrapy/scrapy/issues/525])

Promote startup info on settings and middleware to INFO level (issue 520 [https://github.com/scrapy/scrapy/issues/520])

Support partials in get_func_args util (issue 506 [https://github.com/scrapy/scrapy/issues/506], issue:504)

Allow running indiviual tests via tox (issue 503 [https://github.com/scrapy/scrapy/issues/503])

Update extensions ignored by link extractors (issue 498 [https://github.com/scrapy/scrapy/issues/498])

Add middleware methods to get files/images/thumbs paths (issue 490 [https://github.com/scrapy/scrapy/issues/490])

Improve offsite middleware tests (issue 478 [https://github.com/scrapy/scrapy/issues/478])

Add a way to skip default Referer header set by RefererMiddleware (issue 475 [https://github.com/scrapy/scrapy/issues/475])

Do not send x-gzip in default Accept-Encoding header (issue 469 [https://github.com/scrapy/scrapy/issues/469])

Support defining http error handling using settings (issue 466 [https://github.com/scrapy/scrapy/issues/466])

Use modern python idioms wherever you find legacies (issue 497 [https://github.com/scrapy/scrapy/issues/497])

Improve and correct documentation (issue 527 [https://github.com/scrapy/scrapy/issues/527], issue 524 [https://github.com/scrapy/scrapy/issues/524], issue 521 [https://github.com/scrapy/scrapy/issues/521], issue 517 [https://github.com/scrapy/scrapy/issues/517], issue 512 [https://github.com/scrapy/scrapy/issues/512], issue 505 [https://github.com/scrapy/scrapy/issues/505], issue 502 [https://github.com/scrapy/scrapy/issues/502], issue 489 [https://github.com/scrapy/scrapy/issues/489], issue 465 [https://github.com/scrapy/scrapy/issues/465], issue 460 [https://github.com/scrapy/scrapy/issues/460], issue 425 [https://github.com/scrapy/scrapy/issues/425], issue 536 [https://github.com/scrapy/scrapy/issues/536])

Fixes

Update Selector class imports in CrawlSpider template (issue 484 [https://github.com/scrapy/scrapy/issues/484])

Fix unexistent reference to engine.slots (issue 464 [https://github.com/scrapy/scrapy/issues/464])

Do not try to call body_as_unicode() on a non-TextResponse instance (issue 462 [https://github.com/scrapy/scrapy/issues/462])

Warn when subclassing XPathItemLoader, previously it only warned on instantiation. (issue 523 [https://github.com/scrapy/scrapy/issues/523])

Warn when subclassing XPathSelector, previously it only warned on instantiation. (issue 537 [https://github.com/scrapy/scrapy/issues/537])

Multiple fixes to memory stats (issue 531 [https://github.com/scrapy/scrapy/issues/531], issue 530 [https://github.com/scrapy/scrapy/issues/530], issue 529 [https://github.com/scrapy/scrapy/issues/529])

Fix overriding url in FormRequest.from_response() (issue 507 [https://github.com/scrapy/scrapy/issues/507])

Fix tests runner under pip 1.5 (issue 513 [https://github.com/scrapy/scrapy/issues/513])

Fix logging error when spider name is unicode (issue 479 [https://github.com/scrapy/scrapy/issues/479])

Scrapy 0.20.2 (released 2013-12-09)

Update CrawlSpider Template with Selector changes (commit 6d1457d [https://github.com/scrapy/scrapy/commit/6d1457d])

fix method name in tutorial. closes GH-480 (commit b4fc359 [https://github.com/scrapy/scrapy/commit/b4fc359]

Scrapy 0.20.1 (released 2013-11-28)

include_package_data is required to build wheels from published sources (commit 5ba1ad5 [https://github.com/scrapy/scrapy/commit/5ba1ad5])

process_parallel was leaking the failures on its internal deferreds. closes #458 (commit 419a780 [https://github.com/scrapy/scrapy/commit/419a780])

Scrapy 0.20.0 (released 2013-11-08)

Enhancements

New Selector’s API including CSS selectors (issue 395 [https://github.com/scrapy/scrapy/issues/395] and issue 426 [https://github.com/scrapy/scrapy/issues/426]),

Request/Response url/body attributes are now immutable (modifying them had been deprecated for a long time)

ITEM_PIPELINES is now defined as a dict (instead of a list)

Sitemap spider can fetch alternate URLs (issue 360 [https://github.com/scrapy/scrapy/issues/360])

Selector.remove_namespaces() now remove namespaces from element’s attributes. (issue 416 [https://github.com/scrapy/scrapy/issues/416])

Paved the road for Python 3.3+ (issue 435 [https://github.com/scrapy/scrapy/issues/435], issue 436 [https://github.com/scrapy/scrapy/issues/436], issue 431 [https://github.com/scrapy/scrapy/issues/431], issue 452 [https://github.com/scrapy/scrapy/issues/452])

New item exporter using native python types with nesting support (issue 366 [https://github.com/scrapy/scrapy/issues/366])

Tune HTTP1.1 pool size so it matches concurrency defined by settings (commit b43b5f575 [https://github.com/scrapy/scrapy/commit/b43b5f575])

scrapy.mail.MailSender now can connect over TLS or upgrade using STARTTLS (issue 327 [https://github.com/scrapy/scrapy/issues/327])

New FilesPipeline with functionality factored out from ImagesPipeline (issue 370 [https://github.com/scrapy/scrapy/issues/370], issue 409 [https://github.com/scrapy/scrapy/issues/409])

Recommend Pillow instead of PIL for image handling (issue 317 [https://github.com/scrapy/scrapy/issues/317])

Added debian packages for Ubuntu quantal and raring (commit 86230c0 [https://github.com/scrapy/scrapy/commit/86230c0])

Mock server (used for tests) can listen for HTTPS requests (issue 410 [https://github.com/scrapy/scrapy/issues/410])

Remove multi spider support from multiple core components (issue 422 [https://github.com/scrapy/scrapy/issues/422], issue 421 [https://github.com/scrapy/scrapy/issues/421], issue 420 [https://github.com/scrapy/scrapy/issues/420], issue 419 [https://github.com/scrapy/scrapy/issues/419], issue 423 [https://github.com/scrapy/scrapy/issues/423], issue 418 [https://github.com/scrapy/scrapy/issues/418])

Travis-CI now tests Scrapy changes against development versions of w3lib and queuelib python packages.

Add pypy 2.1 to continuous integration tests (commit ecfa7431 [https://github.com/scrapy/scrapy/commit/ecfa7431])

Pylinted, pep8 and removed old-style exceptions from source (issue 430 [https://github.com/scrapy/scrapy/issues/430], issue 432 [https://github.com/scrapy/scrapy/issues/432])

Use importlib for parametric imports (issue 445 [https://github.com/scrapy/scrapy/issues/445])

Handle a regression introduced in Python 2.7.5 that affects XmlItemExporter (issue 372 [https://github.com/scrapy/scrapy/issues/372])

Bugfix crawling shutdown on SIGINT (issue 450 [https://github.com/scrapy/scrapy/issues/450])

Do not submit reset type inputs in FormRequest.from_response (commit b326b87 [https://github.com/scrapy/scrapy/commit/b326b87])

Do not silence download errors when request errback raises an exception (commit 684cfc0 [https://github.com/scrapy/scrapy/commit/684cfc0])

Bugfixes

Fix tests under Django 1.6 (commit b6bed44c [https://github.com/scrapy/scrapy/commit/b6bed44c])

Lot of bugfixes to retry middleware under disconnections using HTTP 1.1 download handler

Fix inconsistencies among Twisted releases (issue 406 [https://github.com/scrapy/scrapy/issues/406])

Fix scrapy shell bugs (issue 418 [https://github.com/scrapy/scrapy/issues/418], issue 407 [https://github.com/scrapy/scrapy/issues/407])

Fix invalid variable name in setup.py (issue 429 [https://github.com/scrapy/scrapy/issues/429])

Fix tutorial references (issue 387 [https://github.com/scrapy/scrapy/issues/387])

Improve request-response docs (issue 391 [https://github.com/scrapy/scrapy/issues/391])

Improve best practices docs (issue 399 [https://github.com/scrapy/scrapy/issues/399], issue 400 [https://github.com/scrapy/scrapy/issues/400], issue 401 [https://github.com/scrapy/scrapy/issues/401], issue 402 [https://github.com/scrapy/scrapy/issues/402])

Improve django integration docs (issue 404 [https://github.com/scrapy/scrapy/issues/404])

Document bindaddress request meta (commit 37c24e01d7 [https://github.com/scrapy/scrapy/commit/37c24e01d7])

Improve Request class documentation (issue 226 [https://github.com/scrapy/scrapy/issues/226])

Other

Dropped Python 2.6 support (issue 448 [https://github.com/scrapy/scrapy/issues/448])

Add cssselect [https://github.com/scrapy/cssselect/] python package as install dependency

Drop libxml2 and multi selector’s backend support, lxml [http://lxml.de/] is required from now on.

Minimum Twisted version increased to 10.0.0, dropped Twisted 8.0 support.

Running test suite now requires mock python library (issue 390 [https://github.com/scrapy/scrapy/issues/390])

Thanks

Thanks to everyone who contribute to this release!

List of contributors sorted by number of commits:

69 Daniel Graña <dangra@...> 37 Pablo Hoffman <pablo@...> 13 Mikhail Korobov <kmike84@...> 9 Alex Cepoi <alex.cepoi@...> 9 alexanderlukanin13 <alexander.lukanin.13@...> 8 Rolando Espinoza La fuente <darkrho@...> 8 Lukasz Biedrycki <lukasz.biedrycki@...> 6 Nicolas Ramirez <nramirez.uy@...> 3 Paul Tremberth <paul.tremberth@...> 2 Martin Olveyra <molveyra@...> 2 Stefan <misc@...> 2 Rolando Espinoza <darkrho@...> 2 Loren Davie <loren@...> 2 irgmedeiros <irgmedeiros@...> 1 Stefan Koch <taikano@...> 1 Stefan <cct@...> 1 scraperdragon <dragon@...> 1 Kumara Tharmalingam <ktharmal@...> 1 Francesco Piccinno <stack.box@...> 1 Marcos Campal <duendex@...> 1 Dragon Dave <dragon@...> 1 Capi Etheriel <barraponto@...> 1 cacovsky <amarquesferraz@...> 1 Berend Iwema <berend@...>

Scrapy 0.18.4 (released 2013-10-10)

IPython refuses to update the namespace. fix #396 (commit 3d32c4f [https://github.com/scrapy/scrapy/commit/3d32c4f])

Fix AlreadyCalledError replacing a request in shell command. closes #407 (commit b1d8919 [https://github.com/scrapy/scrapy/commit/b1d8919])

Fix start_requests laziness and early hangs (commit 89faf52 [https://github.com/scrapy/scrapy/commit/89faf52])

Scrapy 0.18.3 (released 2013-10-03)

fix regression on lazy evaluation of start requests (commit 12693a5 [https://github.com/scrapy/scrapy/commit/12693a5])

forms: do not submit reset inputs (commit e429f63 [https://github.com/scrapy/scrapy/commit/e429f63])

increase unittest timeouts to decrease travis false positive failures (commit 912202e [https://github.com/scrapy/scrapy/commit/912202e])

backport master fixes to json exporter (commit cfc2d46 [https://github.com/scrapy/scrapy/commit/cfc2d46])

Fix permission and set umask before generating sdist tarball (commit 06149e0 [https://github.com/scrapy/scrapy/commit/06149e0])

Scrapy 0.18.2 (released 2013-09-03)

Backport scrapy check command fixes and backward compatible multi crawler process(issue 339 [https://github.com/scrapy/scrapy/issues/339])

Scrapy 0.18.1 (released 2013-08-27)

remove extra import added by cherry picked changes (commit d20304e [https://github.com/scrapy/scrapy/commit/d20304e])

fix crawling tests under twisted pre 11.0.0 (commit 1994f38 [https://github.com/scrapy/scrapy/commit/1994f38])

py26 can not format zero length fields {} (commit abf756f [https://github.com/scrapy/scrapy/commit/abf756f])

test PotentiaDataLoss errors on unbound responses (commit b15470d [https://github.com/scrapy/scrapy/commit/b15470d])

Treat responses without content-length or Transfer-Encoding as good responses (commit c4bf324 [https://github.com/scrapy/scrapy/commit/c4bf324])

do no include ResponseFailed if http11 handler is not enabled (commit 6cbe684 [https://github.com/scrapy/scrapy/commit/6cbe684])

New HTTP client wraps connection losts in ResponseFailed exception. fix #373 (commit 1a20bba [https://github.com/scrapy/scrapy/commit/1a20bba])

limit travis-ci build matrix (commit 3b01bb8 [https://github.com/scrapy/scrapy/commit/3b01bb8])

Merge pull request #375 from peterarenot/patch-1 (commit fa766d7 [https://github.com/scrapy/scrapy/commit/fa766d7])

Fixed so it refers to the correct folder (commit 3283809 [https://github.com/scrapy/scrapy/commit/3283809])

added quantal & raring to support ubuntu releases (commit 1411923 [https://github.com/scrapy/scrapy/commit/1411923])

fix retry middleware which didn’t retry certain connection errors after the upgrade to http1 client, closes GH-373 (commit bb35ed0 [https://github.com/scrapy/scrapy/commit/bb35ed0])

fix XmlItemExporter in Python 2.7.4 and 2.7.5 (commit de3e451 [https://github.com/scrapy/scrapy/commit/de3e451])

minor updates to 0.18 release notes (commit c45e5f1 [https://github.com/scrapy/scrapy/commit/c45e5f1])

fix contributters list format (commit 0b60031 [https://github.com/scrapy/scrapy/commit/0b60031])

Scrapy 0.18.0 (released 2013-08-09)

Lot of improvements to testsuite run using Tox, including a way to test on pypi

Handle GET parameters for AJAX crawleable urls (commit 3fe2a32 [https://github.com/scrapy/scrapy/commit/3fe2a32])

Use lxml recover option to parse sitemaps (issue 347 [https://github.com/scrapy/scrapy/issues/347])

Bugfix cookie merging by hostname and not by netloc (issue 352 [https://github.com/scrapy/scrapy/issues/352])

Support disabling HttpCompressionMiddleware using a flag setting (issue 359 [https://github.com/scrapy/scrapy/issues/359])

Support xml namespaces using iternodes parser in XMLFeedSpider (issue 12 [https://github.com/scrapy/scrapy/issues/12])

Support dont_cache request meta flag (issue 19 [https://github.com/scrapy/scrapy/issues/19])

Bugfix scrapy.utils.gz.gunzip broken by changes in python 2.7.4 (commit 4dc76e [https://github.com/scrapy/scrapy/commit/4dc76e])

Bugfix url encoding on SgmlLinkExtractor (issue 24 [https://github.com/scrapy/scrapy/issues/24])

Bugfix TakeFirst processor shouldn’t discard zero (0) value (issue 59 [https://github.com/scrapy/scrapy/issues/59])

Support nested items in xml exporter (issue 66 [https://github.com/scrapy/scrapy/issues/66])

Improve cookies handling performance (issue 77 [https://github.com/scrapy/scrapy/issues/77])

Log dupe filtered requests once (issue 105 [https://github.com/scrapy/scrapy/issues/105])

Split redirection middleware into status and meta based middlewares (issue 78 [https://github.com/scrapy/scrapy/issues/78])

Use HTTP1.1 as default downloader handler (issue 109 [https://github.com/scrapy/scrapy/issues/109] and issue 318 [https://github.com/scrapy/scrapy/issues/318])

Support xpath form selection on FormRequest.from_response (issue 185 [https://github.com/scrapy/scrapy/issues/185])

Bugfix unicode decoding error on SgmlLinkExtractor (issue 199 [https://github.com/scrapy/scrapy/issues/199])

Bugfix signal dispatching on pypi interpreter (issue 205 [https://github.com/scrapy/scrapy/issues/205])

Improve request delay and concurrency handling (issue 206 [https://github.com/scrapy/scrapy/issues/206])

Add RFC2616 cache policy to HttpCacheMiddleware (issue 212 [https://github.com/scrapy/scrapy/issues/212])

Allow customization of messages logged by engine (issue 214 [https://github.com/scrapy/scrapy/issues/214])

Multiples improvements to DjangoItem (issue 217 [https://github.com/scrapy/scrapy/issues/217], issue 218 [https://github.com/scrapy/scrapy/issues/218], issue 221 [https://github.com/scrapy/scrapy/issues/221])

Extend Scrapy commands using setuptools entry points (issue 260 [https://github.com/scrapy/scrapy/issues/260])

Allow spider allowed_domains value to be set/tuple (issue 261 [https://github.com/scrapy/scrapy/issues/261])

Support settings.getdict (issue 269 [https://github.com/scrapy/scrapy/issues/269])

Simplify internal scrapy.core.scraper slot handling (issue 271 [https://github.com/scrapy/scrapy/issues/271])

Added Item.copy (issue 290 [https://github.com/scrapy/scrapy/issues/290])

Collect idle downloader slots (issue 297 [https://github.com/scrapy/scrapy/issues/297])

Add ftp:// scheme downloader handler (issue 329 [https://github.com/scrapy/scrapy/issues/329])

Added downloader benchmark webserver and spider tools Benchmarking

Moved persistent (on disk) queues to a separate project (queuelib [https://github.com/scrapy/queuelib]) which scrapy now depends on

Add scrapy commands using external libraries (issue 260 [https://github.com/scrapy/scrapy/issues/260])

Added --pdb option to scrapy command line tool

Added XPathSelector.remove_namespaces which allows to remove all namespaces from XML documents for convenience (to work with namespace-less XPaths). Documented in Selectors.

Several improvements to spider contracts

New default middleware named MetaRefreshMiddldeware that handles meta-refresh html tag redirections,

MetaRefreshMiddldeware and RedirectMiddleware have different priorities to address #62

added from_crawler method to spiders

added system tests with mock server

more improvements to Mac OS compatibility (thanks Alex Cepoi)

several more cleanups to singletons and multi-spider support (thanks Nicolas Ramirez)

support custom download slots

added –spider option to「shell」command.

log overridden settings when scrapy starts

Thanks to everyone who contribute to this release. Here is a list of contributors sorted by number of commits:

130 Pablo Hoffman <pablo@...> 97 Daniel Graña <dangra@...> 20 Nicolás Ramírez <nramirez.uy@...> 13 Mikhail Korobov <kmike84@...> 12 Pedro Faustino <pedrobandim@...> 11 Steven Almeroth <sroth77@...> 5 Rolando Espinoza La fuente <darkrho@...> 4 Michal Danilak <mimino.coder@...> 4 Alex Cepoi <alex.cepoi@...> 4 Alexandr N Zamaraev (aka tonal) <tonal@...> 3 paul <paul.tremberth@...> 3 Martin Olveyra <molveyra@...> 3 Jordi Llonch <llonchj@...> 3 arijitchakraborty <myself.arijit@...> 2 Shane Evans <shane.evans@...> 2 joehillen <joehillen@...> 2 Hart <HartSimha@...> 2 Dan <ellisd23@...> 1 Zuhao Wan <wanzuhao@...> 1 whodatninja <blake@...> 1 vkrest <v.krestiannykov@...> 1 tpeng <pengtaoo@...> 1 Tom Mortimer-Jones <tom@...> 1 Rocio Aramberri <roschegel@...> 1 Pedro <pedro@...> 1 notsobad <wangxiaohugg@...> 1 Natan L <kuyanatan.nlao@...> 1 Mark Grey <mark.grey@...> 1 Luan <luanpab@...> 1 Libor Nenadál <libor.nenadal@...> 1 Juan M Uys <opyate@...> 1 Jonas Brunsgaard <jonas.brunsgaard@...> 1 Ilya Baryshev <baryshev@...> 1 Hasnain Lakhani <m.hasnain.lakhani@...> 1 Emanuel Schorsch <emschorsch@...> 1 Chris Tilden <chris.tilden@...> 1 Capi Etheriel <barraponto@...> 1 cacovsky <amarquesferraz@...> 1 Berend Iwema <berend@...>

Scrapy 0.16.5 (released 2013-05-30)

obey request method when scrapy deploy is redirected to a new endpoint (commit 8c4fcee [https://github.com/scrapy/scrapy/commit/8c4fcee])

fix inaccurate downloader middleware documentation. refs #280 (commit 40667cb [https://github.com/scrapy/scrapy/commit/40667cb])

doc: remove links to diveintopython.org, which is no longer available. closes #246 (commit bd58bfa [https://github.com/scrapy/scrapy/commit/bd58bfa])

Find form nodes in invalid html5 documents (commit e3d6945 [https://github.com/scrapy/scrapy/commit/e3d6945])

Fix typo labeling attrs type bool instead of list (commit a274276 [https://github.com/scrapy/scrapy/commit/a274276])

Scrapy 0.16.4 (released 2013-01-23)

fixes spelling errors in documentation (commit 6d2b3aa [https://github.com/scrapy/scrapy/commit/6d2b3aa])

add doc about disabling an extension. refs #132 (commit c90de33 [https://github.com/scrapy/scrapy/commit/c90de33])

Fixed error message formatting. log.err() doesn’t support cool formatting and when error occurred, the message was:「ERROR: Error processing %(item)s」(commit c16150c [https://github.com/scrapy/scrapy/commit/c16150c])

lint and improve images pipeline error logging (commit 56b45fc [https://github.com/scrapy/scrapy/commit/56b45fc])

fixed doc typos (commit 243be84 [https://github.com/scrapy/scrapy/commit/243be84])

add documentation topics: Broad Crawls & Common Practies (commit 1fbb715 [https://github.com/scrapy/scrapy/commit/1fbb715])

fix bug in scrapy parse command when spider is not specified explicitly. closes #209 (commit c72e682 [https://github.com/scrapy/scrapy/commit/c72e682])

Update docs/topics/commands.rst (commit 28eac7a [https://github.com/scrapy/scrapy/commit/28eac7a])

Scrapy 0.16.3 (released 2012-12-07)

Remove concurrency limitation when using download delays and still ensure inter-request delays are enforced (commit 487b9b5 [https://github.com/scrapy/scrapy/commit/487b9b5])

add error details when image pipeline fails (commit 8232569 [https://github.com/scrapy/scrapy/commit/8232569])

improve mac os compatibility (commit 8dcf8aa [https://github.com/scrapy/scrapy/commit/8dcf8aa])

setup.py: use README.rst to populate long_description (commit 7b5310d [https://github.com/scrapy/scrapy/commit/7b5310d])

doc: removed obsolete references to ClientForm (commit 80f9bb6 [https://github.com/scrapy/scrapy/commit/80f9bb6])

correct docs for default storage backend (commit 2aa491b [https://github.com/scrapy/scrapy/commit/2aa491b])

doc: removed broken proxyhub link from FAQ (commit bdf61c4 [https://github.com/scrapy/scrapy/commit/bdf61c4])

Fixed docs typo in SpiderOpenCloseLogging example (commit 7184094 [https://github.com/scrapy/scrapy/commit/7184094])

Scrapy 0.16.2 (released 2012-11-09)

scrapy contracts: python2.6 compat (commit a4a9199 [https://github.com/scrapy/scrapy/commit/a4a9199])

scrapy contracts verbose option (commit ec41673 [https://github.com/scrapy/scrapy/commit/ec41673])

proper unittest-like output for scrapy contracts (commit 86635e4 [https://github.com/scrapy/scrapy/commit/86635e4])

added open_in_browser to debugging doc (commit c9b690d [https://github.com/scrapy/scrapy/commit/c9b690d])

removed reference to global scrapy stats from settings doc (commit dd55067 [https://github.com/scrapy/scrapy/commit/dd55067])

Fix SpiderState bug in Windows platforms (commit 58998f4 [https://github.com/scrapy/scrapy/commit/58998f4])

Scrapy 0.16.1 (released 2012-10-26)

fixed LogStats extension, which got broken after a wrong merge before the 0.16 release (commit 8c780fd [https://github.com/scrapy/scrapy/commit/8c780fd])

better backward compatibility for scrapy.conf.settings (commit 3403089 [https://github.com/scrapy/scrapy/commit/3403089])

extended documentation on how to access crawler stats from extensions (commit c4da0b5 [https://github.com/scrapy/scrapy/commit/c4da0b5])

removed .hgtags (no longer needed now that scrapy uses git) (commit d52c188 [https://github.com/scrapy/scrapy/commit/d52c188])

fix dashes under rst headers (commit fa4f7f9 [https://github.com/scrapy/scrapy/commit/fa4f7f9])

set release date for 0.16.0 in news (commit e292246 [https://github.com/scrapy/scrapy/commit/e292246])

Scrapy 0.16.0 (released 2012-10-18)

Scrapy changes:

added Spiders Contracts, a mechanism for testing spiders in a formal/reproducible way

added options -o and -t to the runspider command

documented AutoThrottle extension and added to extensions installed by default. You still need to enable it with AUTOTHROTTLE_ENABLED

major Stats Collection refactoring: removed separation of global/per-spider stats, removed stats-related signals (stats_spider_opened, etc). Stats are much simpler now, backward compatibility is kept on the Stats Collector API and signals.

added process_start_requests() method to spider middlewares

dropped Signals singleton. Signals should now be accesed through the Crawler.signals attribute. See the signals documentation for more info.

dropped Signals singleton. Signals should now be accesed through the Crawler.signals attribute. See the signals documentation for more info.

dropped Stats Collector singleton. Stats can now be accessed through the Crawler.stats attribute. See the stats collection documentation for more info.

documented Core API

lxml is now the default selectors backend instead of libxml2

ported FormRequest.from_response() to use lxml [http://lxml.de/] instead of ClientForm [http://wwwsearch.sourceforge.net/old/ClientForm/]

removed modules: scrapy.xlib.BeautifulSoup and scrapy.xlib.ClientForm

SitemapSpider: added support for sitemap urls ending in .xml and .xml.gz, even if they advertise a wrong content type (commit 10ed28b [https://github.com/scrapy/scrapy/commit/10ed28b])

StackTraceDump extension: also dump trackref live references (commit fe2ce93 [https://github.com/scrapy/scrapy/commit/fe2ce93])

nested items now fully supported in JSON and JSONLines exporters

added cookiejar Request meta key to support multiple cookie sessions per spider

decoupled encoding detection code to w3lib.encoding [https://github.com/scrapy/w3lib/blob/master/w3lib/encoding.py], and ported Scrapy code to use that module

dropped support for Python 2.5. See https://blog.scrapinghub.com/2012/02/27/scrapy-0-15-dropping-support-for-python-2-5/

dropped support for Twisted 2.5

added REFERER_ENABLED setting, to control referer middleware

changed default user agent to: Scrapy/VERSION (+http://scrapy.org)

removed (undocumented) HTMLImageLinkExtractor class from scrapy.contrib.linkextractors.image

removed per-spider settings (to be replaced by instantiating multiple crawler objects)

USER_AGENT spider attribute will no longer work, use user_agent attribute instead

DOWNLOAD_TIMEOUT spider attribute will no longer work, use download_timeout attribute instead

removed ENCODING_ALIASES setting, as encoding auto-detection has been moved to the w3lib [https://github.com/scrapy/w3lib] library

promoted DjangoItem to main contrib

LogFormatter method now return dicts(instead of strings) to support lazy formatting (issue 164 [https://github.com/scrapy/scrapy/issues/164], commit dcef7b0 [https://github.com/scrapy/scrapy/commit/dcef7b0])

downloader handlers (DOWNLOAD_HANDLERS setting) now receive settings as the first argument of the constructor

replaced memory usage acounting with (more portable) resource [https://docs.python.org/2/library/resource.html] module, removed scrapy.utils.memory module

removed signal: scrapy.mail.mail_sent

removed TRACK_REFS setting, now trackrefs is always enabled

DBM is now the default storage backend for HTTP cache middleware

number of log messages (per level) are now tracked through Scrapy stats (stat name: log_count/LEVEL)

number received responses are now tracked through Scrapy stats (stat name: response_received_count)

removed scrapy.log.started attribute

Scrapy 0.14.4

added precise to supported ubuntu distros (commit b7e46df [https://github.com/scrapy/scrapy/commit/b7e46df])

fixed bug in json-rpc webservice reported in https://groups.google.com/forum/#!topic/scrapy-users/qgVBmFybNAQ/discussion. also removed no longer supported ‘run’ command from extras/scrapy-ws.py (commit 340fbdb [https://github.com/scrapy/scrapy/commit/340fbdb])

meta tag attributes for content-type http equiv can be in any order. #123 (commit 0cb68af [https://github.com/scrapy/scrapy/commit/0cb68af])

replace「import Image」by more standard「from PIL import Image」. closes #88 (commit 4d17048 [https://github.com/scrapy/scrapy/commit/4d17048])

return trial status as bin/runtests.sh exit value. #118 (commit b7b2e7f [https://github.com/scrapy/scrapy/commit/b7b2e7f])

Scrapy 0.14.3

forgot to include pydispatch license. #118 (commit fd85f9c [https://github.com/scrapy/scrapy/commit/fd85f9c])

include egg files used by testsuite in source distribution. #118 (commit c897793 [https://github.com/scrapy/scrapy/commit/c897793])

update docstring in project template to avoid confusion with genspider command, which may be considered as an advanced feature. refs #107 (commit 2548dcc [https://github.com/scrapy/scrapy/commit/2548dcc])

added note to docs/topics/firebug.rst about google directory being shut down (commit 668e352 [https://github.com/scrapy/scrapy/commit/668e352])

dont discard slot when empty, just save in another dict in order to recycle if needed again. (commit 8e9f607 [https://github.com/scrapy/scrapy/commit/8e9f607])

do not fail handling unicode xpaths in libxml2 backed selectors (commit b830e95 [https://github.com/scrapy/scrapy/commit/b830e95])

fixed minor mistake in Request objects documentation (commit bf3c9ee [https://github.com/scrapy/scrapy/commit/bf3c9ee])

fixed minor defect in link extractors documentation (commit ba14f38 [https://github.com/scrapy/scrapy/commit/ba14f38])

removed some obsolete remaining code related to sqlite support in scrapy (commit 0665175 [https://github.com/scrapy/scrapy/commit/0665175])

Scrapy 0.14.2

move buffer pointing to start of file before computing checksum. refs #92 (commit 6a5bef2 [https://github.com/scrapy/scrapy/commit/6a5bef2])

Compute image checksum before persisting images. closes #92 (commit 9817df1 [https://github.com/scrapy/scrapy/commit/9817df1])

remove leaking references in cached failures (commit 673a120 [https://github.com/scrapy/scrapy/commit/673a120])

fixed bug in MemoryUsage extension: get_engine_status() takes exactly 1 argument (0 given) (commit 11133e9 [https://github.com/scrapy/scrapy/commit/11133e9])

fixed struct.error on http compression middleware. closes #87 (commit 1423140 [https://github.com/scrapy/scrapy/commit/1423140])

ajax crawling wasn’t expanding for unicode urls (commit 0de3fb4 [https://github.com/scrapy/scrapy/commit/0de3fb4])

Catch start_requests iterator errors. refs #83 (commit 454a21d [https://github.com/scrapy/scrapy/commit/454a21d])

Speed-up libxml2 XPathSelector (commit 2fbd662 [https://github.com/scrapy/scrapy/commit/2fbd662])

updated versioning doc according to recent changes (commit 0a070f5 [https://github.com/scrapy/scrapy/commit/0a070f5])

scrapyd: fixed documentation link (commit 2b4e4c3 [https://github.com/scrapy/scrapy/commit/2b4e4c3])

extras/makedeb.py: no longer obtaining version from git (commit caffe0e [https://github.com/scrapy/scrapy/commit/caffe0e])

Scrapy 0.14.1

extras/makedeb.py: no longer obtaining version from git (commit caffe0e [https://github.com/scrapy/scrapy/commit/caffe0e])

bumped version to 0.14.1 (commit 6cb9e1c [https://github.com/scrapy/scrapy/commit/6cb9e1c])

fixed reference to tutorial directory (commit 4b86bd6 [https://github.com/scrapy/scrapy/commit/4b86bd6])

doc: removed duplicated callback argument from Request.replace() (commit 1aeccdd [https://github.com/scrapy/scrapy/commit/1aeccdd])

fixed formatting of scrapyd doc (commit 8bf19e6 [https://github.com/scrapy/scrapy/commit/8bf19e6])

Dump stacks for all running threads and fix engine status dumped by StackTraceDump extension (commit 14a8e6e [https://github.com/scrapy/scrapy/commit/14a8e6e])

added comment about why we disable ssl on boto images upload (commit 5223575 [https://github.com/scrapy/scrapy/commit/5223575])

SSL handshaking hangs when doing too many parallel connections to S3 (commit 63d583d [https://github.com/scrapy/scrapy/commit/63d583d])

change tutorial to follow changes on dmoz site (commit bcb3198 [https://github.com/scrapy/scrapy/commit/bcb3198])

Avoid _disconnectedDeferred AttributeError exception in Twisted>=11.1.0 (commit 98f3f87 [https://github.com/scrapy/scrapy/commit/98f3f87])

allow spider to set autothrottle max concurrency (commit 175a4b5 [https://github.com/scrapy/scrapy/commit/175a4b5])

Scrapy 0.14

New features and settings

Support for AJAX crawleable urls [https://developers.google.com/webmasters/ajax-crawling/docs/getting-started?csw=1]

New persistent scheduler that stores requests on disk, allowing to suspend and resume crawls (r2737 [http://hg.scrapy.org/scrapy/changeset/2737])

added -o option to scrapy crawl, a shortcut for dumping scraped items into a file (or standard output using -)

Added support for passing custom settings to Scrapyd schedule.json api (r2779 [http://hg.scrapy.org/scrapy/changeset/2779], r2783 [http://hg.scrapy.org/scrapy/changeset/2783])

New ChunkedTransferMiddleware (enabled by default) to support chunked transfer encoding [https://en.wikipedia.org/wiki/Chunked_transfer_encoding] (r2769 [http://hg.scrapy.org/scrapy/changeset/2769])

Add boto 2.0 support for S3 downloader handler (r2763 [http://hg.scrapy.org/scrapy/changeset/2763])

Added marshal [https://docs.python.org/2/library/marshal.html] to formats supported by feed exports (r2744 [http://hg.scrapy.org/scrapy/changeset/2744])

In request errbacks, offending requests are now received in failure.request attribute (r2738 [http://hg.scrapy.org/scrapy/changeset/2738])

Big downloader refactoring to support per domain/ip concurrency limits (r2732 [http://hg.scrapy.org/scrapy/changeset/2732])

CONCURRENT_REQUESTS_PER_SPIDER setting has been deprecated and replaced by:

CONCURRENT_REQUESTS, CONCURRENT_REQUESTS_PER_DOMAIN, CONCURRENT_REQUESTS_PER_IP

check the documentation for more details

Added builtin caching DNS resolver (r2728 [http://hg.scrapy.org/scrapy/changeset/2728])

Moved Amazon AWS-related components/extensions (SQS spider queue, SimpleDB stats collector) to a separate project: [scaws](https://github.com/scrapinghub/scaws) (r2706 [http://hg.scrapy.org/scrapy/changeset/2706], r2714 [http://hg.scrapy.org/scrapy/changeset/2714])

Moved spider queues to scrapyd: scrapy.spiderqueue -> scrapyd.spiderqueue (r2708 [http://hg.scrapy.org/scrapy/changeset/2708])

Moved sqlite utils to scrapyd: scrapy.utils.sqlite -> scrapyd.sqlite (r2781 [http://hg.scrapy.org/scrapy/changeset/2781])

Real support for returning iterators on start_requests() method. The iterator is now consumed during the crawl when the spider is getting idle (r2704 [http://hg.scrapy.org/scrapy/changeset/2704])

Added REDIRECT_ENABLED setting to quickly enable/disable the redirect middleware (r2697 [http://hg.scrapy.org/scrapy/changeset/2697])

Added RETRY_ENABLED setting to quickly enable/disable the retry middleware (r2694 [http://hg.scrapy.org/scrapy/changeset/2694])

Added CloseSpider exception to manually close spiders (r2691 [http://hg.scrapy.org/scrapy/changeset/2691])

Improved encoding detection by adding support for HTML5 meta charset declaration (r2690 [http://hg.scrapy.org/scrapy/changeset/2690])

Refactored close spider behavior to wait for all downloads to finish and be processed by spiders, before closing the spider (r2688 [http://hg.scrapy.org/scrapy/changeset/2688])

Added SitemapSpider (see documentation in Spiders page) (r2658 [http://hg.scrapy.org/scrapy/changeset/2658])

Added LogStats extension for periodically logging basic stats (like crawled pages and scraped items) (r2657 [http://hg.scrapy.org/scrapy/changeset/2657])

Make handling of gzipped responses more robust (#319, r2643 [http://hg.scrapy.org/scrapy/changeset/2643]). Now Scrapy will try and decompress as much as possible from a gzipped response, instead of failing with an IOError.

Simplified !MemoryDebugger extension to use stats for dumping memory debugging info (r2639 [http://hg.scrapy.org/scrapy/changeset/2639])

Added new command to edit spiders: scrapy edit (r2636 [http://hg.scrapy.org/scrapy/changeset/2636]) and -e flag to genspider command that uses it (r2653 [http://hg.scrapy.org/scrapy/changeset/2653])

Changed default representation of items to pretty-printed dicts. (r2631 [http://hg.scrapy.org/scrapy/changeset/2631]). This improves default logging by making log more readable in the default case, for both Scraped and Dropped lines.

Added spider_error signal (r2628 [http://hg.scrapy.org/scrapy/changeset/2628])

Added COOKIES_ENABLED setting (r2625 [http://hg.scrapy.org/scrapy/changeset/2625])

Stats are now dumped to Scrapy log (default value of STATS_DUMP setting has been changed to True). This is to make Scrapy users more aware of Scrapy stats and the data that is collected there.

Added support for dynamically adjusting download delay and maximum concurrent requests (r2599 [http://hg.scrapy.org/scrapy/changeset/2599])

Added new DBM HTTP cache storage backend (r2576 [http://hg.scrapy.org/scrapy/changeset/2576])

Added listjobs.json API to Scrapyd (r2571 [http://hg.scrapy.org/scrapy/changeset/2571])

CsvItemExporter: added join_multivalued parameter (r2578 [http://hg.scrapy.org/scrapy/changeset/2578])

Added namespace support to xmliter_lxml (r2552 [http://hg.scrapy.org/scrapy/changeset/2552])

Improved cookies middleware by making COOKIES_DEBUG nicer and documenting it (r2579 [http://hg.scrapy.org/scrapy/changeset/2579])

Several improvements to Scrapyd and Link extractors

Code rearranged and removed

Merged item passed and item scraped concepts, as they have often proved confusing in the past. This means: (r2630 [http://hg.scrapy.org/scrapy/changeset/2630])

original item_scraped signal was removed

original item_passed signal was renamed to item_scraped

old log lines Scraped Item... were removed

old log lines Passed Item... were renamed to Scraped Item... lines and downgraded to DEBUG level

Reduced Scrapy codebase by striping part of Scrapy code into two new libraries:

w3lib [https://github.com/scrapy/w3lib] (several functions from scrapy.utils.{http,markup,multipart,response,url}, done in r2584 [http://hg.scrapy.org/scrapy/changeset/2584])

scrapely [https://github.com/scrapy/scrapely] (was scrapy.contrib.ibl, done in r2586 [http://hg.scrapy.org/scrapy/changeset/2586])

Removed unused function: scrapy.utils.request.request_info() (r2577 [http://hg.scrapy.org/scrapy/changeset/2577])

Removed googledir project from examples/googledir. There’s now a new example project called dirbot available on GitHub: https://github.com/scrapy/dirbot

Removed support for default field values in Scrapy items (r2616 [http://hg.scrapy.org/scrapy/changeset/2616])

Removed experimental crawlspider v2 (r2632 [http://hg.scrapy.org/scrapy/changeset/2632])

Removed scheduler middleware to simplify architecture. Duplicates filter is now done in the scheduler itself, using the same dupe fltering class as before (DUPEFILTER_CLASS setting) (r2640 [http://hg.scrapy.org/scrapy/changeset/2640])

Removed support for passing urls to scrapy crawl command (use scrapy parse instead) (r2704 [http://hg.scrapy.org/scrapy/changeset/2704])

Removed deprecated Execution Queue (r2704 [http://hg.scrapy.org/scrapy/changeset/2704])

Removed (undocumented) spider context extension (from scrapy.contrib.spidercontext) (r2780 [http://hg.scrapy.org/scrapy/changeset/2780])

removed CONCURRENT_SPIDERS setting (use scrapyd maxproc instead) (r2789 [http://hg.scrapy.org/scrapy/changeset/2789])

Renamed attributes of core components: downloader.sites -> downloader.slots, scraper.sites -> scraper.slots (r2717 [http://hg.scrapy.org/scrapy/changeset/2717], r2718 [http://hg.scrapy.org/scrapy/changeset/2718])

Renamed setting CLOSESPIDER_ITEMPASSED to CLOSESPIDER_ITEMCOUNT (r2655 [http://hg.scrapy.org/scrapy/changeset/2655]). Backward compatibility kept.

Scrapy 0.12

The numbers like #NNN reference tickets in the old issue tracker (Trac) which is no longer available.

New features and improvements

Passed item is now sent in the item argument of the item_passed (#273)

Added verbose option to scrapy version command, useful for bug reports (#298)

HTTP cache now stored by default in the project data dir (#279)

Added project data storage directory (#276, #277)

Documented file structure of Scrapy projects (see command-line tool doc)

New lxml backend for XPath selectors (#147)

Per-spider settings (#245)

Support exit codes to signal errors in Scrapy commands (#248)

Added -c argument to scrapy shell command

Made libxml2 optional (#260)

New deploy command (#261)

Added CLOSESPIDER_PAGECOUNT setting (#253)

Added CLOSESPIDER_ERRORCOUNT setting (#254)

Scrapyd changes

Scrapyd now uses one process per spider

It stores one log file per spider run, and rotate them keeping the lastest 5 logs per spider (by default)

A minimal web ui was added, available at http://localhost:6800 by default

There is now a scrapy server command to start a Scrapyd server of the current project

Changes to settings

added HTTPCACHE_ENABLED setting (False by default) to enable HTTP cache middleware

changed HTTPCACHE_EXPIRATION_SECS semantics: now zero means「never expire」.

Deprecated/obsoleted functionality

Deprecated runserver command in favor of server command which starts a Scrapyd server. See also: Scrapyd changes

Deprecated queue command in favor of using Scrapyd schedule.json API. See also: Scrapyd changes

Removed the !LxmlItemLoader (experimental contrib which never graduated to main contrib)

Scrapy 0.10

The numbers like #NNN reference tickets in the old issue tracker (Trac) which is no longer available.

New features and improvements

New Scrapy service called scrapyd for deploying Scrapy crawlers in production (#218) (documentation available)

Simplified Images pipeline usage which doesn’t require subclassing your own images pipeline now (#217)

Scrapy shell now shows the Scrapy log by default (#206)

Refactored execution queue in a common base code and pluggable backends called「spider queues」(#220)

New persistent spider queue (based on SQLite) (#198), available by default, which allows to start Scrapy in server mode and then schedule spiders to run.

Added documentation for Scrapy command-line tool and all its available sub-commands. (documentation available)

Feed exporters with pluggable backends (#197) (documentation available)

Deferred signals (#193)

Added two new methods to item pipeline open_spider(), close_spider() with deferred support (#195)

Support for overriding default request headers per spider (#181)

Replaced default Spider Manager with one with similar functionality but not depending on Twisted Plugins (#186)

Splitted Debian package into two packages - the library and the service (#187)

Scrapy log refactoring (#188)

New extension for keeping persistent spider contexts among different runs (#203)

Added dont_redirect request.meta key for avoiding redirects (#233)

Added dont_retry request.meta key for avoiding retries (#234)

Command-line tool changes

New scrapy command which replaces the old scrapy-ctl.py (#199) - there is only one global scrapy command now, instead of one scrapy-ctl.py per project - Added scrapy.bat script for running more conveniently from Windows

Added bash completion to command-line tool (#210)

Renamed command start to runserver (#209)

API changes

url and body attributes of Request objects are now read-only (#230)

Request.copy() and Request.replace() now also copies their callback and errback attributes (#231)

Removed UrlFilterMiddleware from scrapy.contrib (already disabled by default)

Offsite middelware doesn’t filter out any request coming from a spider that doesn’t have a allowed_domains attribute (#225)

Removed Spider Manager load() method. Now spiders are loaded in the constructor itself.

Changes to Scrapy Manager (now called「Crawler」):

scrapy.core.manager.ScrapyManager class renamed to scrapy.crawler.Crawler

scrapy.core.manager.scrapymanager singleton moved to scrapy.project.crawler

Moved module: scrapy.contrib.spidermanager to scrapy.spidermanager

Spider Manager singleton moved from scrapy.spider.spiders to the spiders` attribute of ``scrapy.project.crawler singleton.

moved Stats Collector classes: (#204)

scrapy.stats.collector.StatsCollector to scrapy.statscol.StatsCollector

scrapy.stats.collector.SimpledbStatsCollector to scrapy.contrib.statscol.SimpledbStatsCollector

default per-command settings are now specified in the default_settings attribute of command object class (#201)

changed arguments of Item pipeline process_item() method from (spider, item) to (item, spider)

backward compatibility kept (with deprecation warning)

moved scrapy.core.signals module to scrapy.signals

backward compatibility kept (with deprecation warning)

moved scrapy.core.exceptions module to scrapy.exceptions

backward compatibility kept (with deprecation warning)

added handles_request() class method to BaseSpider

dropped scrapy.log.exc() function (use scrapy.log.err() instead)

dropped component argument of scrapy.log.msg() function

dropped scrapy.log.log_level attribute

Added from_settings() class methods to Spider Manager, and Item Pipeline Manager

Changes to settings

Added HTTPCACHE_IGNORE_SCHEMES setting to ignore certain schemes on !HttpCacheMiddleware (#225)

Added SPIDER_QUEUE_CLASS setting which defines the spider queue to use (#220)

Added KEEP_ALIVE setting (#220)

Removed SERVICE_QUEUE setting (#220)

Removed COMMANDS_SETTINGS_MODULE setting (#201)

Renamed REQUEST_HANDLERS to DOWNLOAD_HANDLERS and make download handlers classes (instead of functions)

Scrapy 0.9

The numbers like #NNN reference tickets in the old issue tracker (Trac) which is no longer available.

New features and improvements

Added SMTP-AUTH support to scrapy.mail

New settings added: MAIL_USER, MAIL_PASS (r2065 [http://hg.scrapy.org/scrapy/changeset/2065] | #149)

Added new scrapy-ctl view command - To view URL in the browser, as seen by Scrapy (r2039 [http://hg.scrapy.org/scrapy/changeset/2039])

Added web service for controlling Scrapy process (this also deprecates the web console. (r2053 [http://hg.scrapy.org/scrapy/changeset/2053] | #167)

Support for running Scrapy as a service, for production systems (r1988 [http://hg.scrapy.org/scrapy/changeset/1988], r2054 [http://hg.scrapy.org/scrapy/changeset/2054], r2055 [http://hg.scrapy.org/scrapy/changeset/2055], r2056 [http://hg.scrapy.org/scrapy/changeset/2056], r2057 [http://hg.scrapy.org/scrapy/changeset/2057] | #168)

Added wrapper induction library (documentation only available in source code for now). (r2011 [http://hg.scrapy.org/scrapy/changeset/2011])

Simplified and improved response encoding support (r1961 [http://hg.scrapy.org/scrapy/changeset/1961], r1969 [http://hg.scrapy.org/scrapy/changeset/1969])

Added LOG_ENCODING setting (r1956 [http://hg.scrapy.org/scrapy/changeset/1956], documentation available)

Added RANDOMIZE_DOWNLOAD_DELAY setting (enabled by default) (r1923 [http://hg.scrapy.org/scrapy/changeset/1923], doc available)

MailSender is no longer IO-blocking (r1955 [http://hg.scrapy.org/scrapy/changeset/1955] | #146)

Linkextractors and new Crawlspider now handle relative base tag urls (r1960 [http://hg.scrapy.org/scrapy/changeset/1960] | #148)

Several improvements to Item Loaders and processors (r2022 [http://hg.scrapy.org/scrapy/changeset/2022], r2023 [http://hg.scrapy.org/scrapy/changeset/2023], r2024 [http://hg.scrapy.org/scrapy/changeset/2024], r2025 [http://hg.scrapy.org/scrapy/changeset/2025], r2026 [http://hg.scrapy.org/scrapy/changeset/2026], r2027 [http://hg.scrapy.org/scrapy/changeset/2027], r2028 [http://hg.scrapy.org/scrapy/changeset/2028], r2029 [http://hg.scrapy.org/scrapy/changeset/2029], r2030 [http://hg.scrapy.org/scrapy/changeset/2030])

Added support for adding variables to telnet console (r2047 [http://hg.scrapy.org/scrapy/changeset/2047] | #165)

Support for requests without callbacks (r2050 [http://hg.scrapy.org/scrapy/changeset/2050] | #166)

API changes

Change Spider.domain_name to Spider.name (SEP-012, r1975 [http://hg.scrapy.org/scrapy/changeset/1975])

Response.encoding is now the detected encoding (r1961 [http://hg.scrapy.org/scrapy/changeset/1961])

HttpErrorMiddleware now returns None or raises an exception (r2006 [http://hg.scrapy.org/scrapy/changeset/2006] | #157)

scrapy.command modules relocation (r2035 [http://hg.scrapy.org/scrapy/changeset/2035], r2036 [http://hg.scrapy.org/scrapy/changeset/2036], r2037 [http://hg.scrapy.org/scrapy/changeset/2037])

Added ExecutionQueue for feeding spiders to scrape (r2034 [http://hg.scrapy.org/scrapy/changeset/2034])

Removed ExecutionEngine singleton (r2039 [http://hg.scrapy.org/scrapy/changeset/2039])

Ported S3ImagesStore (images pipeline) to use boto and threads (r2033 [http://hg.scrapy.org/scrapy/changeset/2033])

Moved module: scrapy.management.telnet to scrapy.telnet (r2047 [http://hg.scrapy.org/scrapy/changeset/2047])

Changes to default settings

Changed default SCHEDULER_ORDER to DFO (r1939 [http://hg.scrapy.org/scrapy/changeset/1939])

Scrapy 0.8

The numbers like #NNN reference tickets in the old issue tracker (Trac) which is no longer available.

New features

Added DEFAULT_RESPONSE_ENCODING setting (r1809 [http://hg.scrapy.org/scrapy/changeset/1809])

Added dont_click argument to FormRequest.from_response() method (r1813 [http://hg.scrapy.org/scrapy/changeset/1813], r1816 [http://hg.scrapy.org/scrapy/changeset/1816])

Added clickdata argument to FormRequest.from_response() method (r1802 [http://hg.scrapy.org/scrapy/changeset/1802], r1803 [http://hg.scrapy.org/scrapy/changeset/1803])

Added support for HTTP proxies (HttpProxyMiddleware) (r1781 [http://hg.scrapy.org/scrapy/changeset/1781], r1785 [http://hg.scrapy.org/scrapy/changeset/1785])

Offsite spider middleware now logs messages when filtering out requests (r1841 [http://hg.scrapy.org/scrapy/changeset/1841])

Backward-incompatible changes

Changed scrapy.utils.response.get_meta_refresh() signature (r1804 [http://hg.scrapy.org/scrapy/changeset/1804])

Removed deprecated scrapy.item.ScrapedItem class - use scrapy.item.Item instead (r1838 [http://hg.scrapy.org/scrapy/changeset/1838])

Removed deprecated scrapy.xpath module - use scrapy.selector instead. (r1836 [http://hg.scrapy.org/scrapy/changeset/1836])

Removed deprecated core.signals.domain_open signal - use core.signals.domain_opened instead (r1822 [http://hg.scrapy.org/scrapy/changeset/1822])

log.msg() now receives a spider argument (r1822 [http://hg.scrapy.org/scrapy/changeset/1822])

Old domain argument has been deprecated and will be removed in 0.9. For spiders, you should always use the spider argument and pass spider references. If you really want to pass a string, use the component argument instead.

Changed core signals domain_opened, domain_closed, domain_idle

Changed Item pipeline to use spiders instead of domains

The domain argument of process_item() item pipeline method was changed to spider, the new signature is: process_item(spider, item) (r1827 [http://hg.scrapy.org/scrapy/changeset/1827] | #105)

To quickly port your code (to work with Scrapy 0.8) just use spider.domain_name where you previously used domain.

Changed Stats API to use spiders instead of domains (r1849 [http://hg.scrapy.org/scrapy/changeset/1849] | #113)

StatsCollector was changed to receive spider references (instead of domains) in its methods (set_value, inc_value, etc).

added StatsCollector.iter_spider_stats() method

removed StatsCollector.list_domains() method

Also, Stats signals were renamed and now pass around spider references (instead of domains). Here’s a summary of the changes:

To quickly port your code (to work with Scrapy 0.8) just use spider.domain_name where you previously used domain. spider_stats contains exactly the same data as domain_stats.

CloseDomain extension moved to scrapy.contrib.closespider.CloseSpider (r1833 [http://hg.scrapy.org/scrapy/changeset/1833])

Its settings were also renamed:

CLOSEDOMAIN_TIMEOUT to CLOSESPIDER_TIMEOUT

CLOSEDOMAIN_ITEMCOUNT to CLOSESPIDER_ITEMCOUNT

Removed deprecated SCRAPYSETTINGS_MODULE environment variable - use SCRAPY_SETTINGS_MODULE instead (r1840 [http://hg.scrapy.org/scrapy/changeset/1840])

Renamed setting: REQUESTS_PER_DOMAIN to CONCURRENT_REQUESTS_PER_SPIDER (r1830 [http://hg.scrapy.org/scrapy/changeset/1830], r1844 [http://hg.scrapy.org/scrapy/changeset/1844])

Renamed setting: CONCURRENT_DOMAINS to CONCURRENT_SPIDERS (r1830 [http://hg.scrapy.org/scrapy/changeset/1830])

Refactored HTTP Cache middleware

HTTP Cache middleware has been heavilty refactored, retaining the same functionality except for the domain sectorization which was removed. (r1843 [http://hg.scrapy.org/scrapy/changeset/1843] )

Renamed exception: DontCloseDomain to DontCloseSpider (r1859 [http://hg.scrapy.org/scrapy/changeset/1859] | #120)

Renamed extension: DelayedCloseDomain to SpiderCloseDelay (r1861 [http://hg.scrapy.org/scrapy/changeset/1861] | #121)

Removed obsolete scrapy.utils.markup.remove_escape_chars function - use scrapy.utils.markup.replace_escape_chars instead (r1865 [http://hg.scrapy.org/scrapy/changeset/1865])

Scrapy 0.7

First release of Scrapy.

Contributing to Scrapy

Important

Double check that you are reading the most recent version of this document at https://docs.scrapy.org/en/master/contributing.html

There are many ways to contribute to Scrapy. Here are some of them:

Blog about Scrapy. Tell the world how you’re using Scrapy. This will help newcomers with more examples and will help the Scrapy project to increase its visibility.

Report bugs and request features in the issue tracker [https://github.com/scrapy/scrapy/issues], trying to follow the guidelines detailed in Reporting bugs below.

Submit patches for new functionalities and/or bug fixes. Please read Writing patches and Submitting patches below for details on how to write and submit a patch.

Join the Scrapy subreddit [https://reddit.com/r/scrapy] and share your ideas on how to improve Scrapy. We’re always open to suggestions.

Answer Scrapy questions at Stack Overflow [https://stackoverflow.com/questions/tagged/scrapy].

Reporting bugs

Note

Please report security issues only to scrapy-security@googlegroups.com. This is a private list only open to trusted Scrapy developers, and its archives are not public.

Well-written bug reports are very helpful, so keep in mind the following guidelines when you’re going to report a new bug.

check the FAQ first to see if your issue is addressed in a well-known question

if you have a general question about scrapy usage, please ask it at Stack Overflow [https://stackoverflow.com/questions/tagged/scrapy] (use「scrapy」tag).

check the open issues [https://github.com/scrapy/scrapy/issues] to see if the issue has already been reported. If it has, don’t dismiss the report, but check the ticket history and comments. If you have additional useful information, please leave a comment, or consider sending a pull request with a fix.

search the scrapy-users [https://groups.google.com/forum/#!forum/scrapy-users] list and Scrapy subreddit [https://reddit.com/r/scrapy] to see if it has been discussed there, or if you’re not sure if what you’re seeing is a bug. You can also ask in the #scrapy IRC channel.

write complete, reproducible, specific bug reports. The smaller the test case, the better. Remember that other developers won’t have your project to reproduce the bug, so please include all relevant files required to reproduce it. See for example StackOverflow’s guide on creating a Minimal, Complete, and Verifiable example [https://stackoverflow.com/help/mcve] exhibiting the issue.

the most awesome way to provide a complete reproducible example is to send a pull request which adds a failing test case to the Scrapy testing suite (see Submitting patches). This is helpful even if you don’t have an intention to fix the issue yourselves.

include the output of scrapy version -v so developers working on your bug know exactly which version and platform it occurred on, which is often very helpful for reproducing it, or knowing if it was already fixed.

Writing patches

The better a patch is written, the higher the chances that it’ll get accepted and the sooner it will be merged.

Well-written patches should:

contain the minimum amount of code required for the specific change. Small patches are easier to review and merge. So, if you’re doing more than one change (or bug fix), please consider submitting one patch per change. Do not collapse multiple changes into a single patch. For big changes consider using a patch queue.

pass all unit-tests. See Running tests below.

include one (or more) test cases that check the bug fixed or the new functionality added. See Writing tests below.

if you’re adding or changing a public (documented) API, please include the documentation changes in the same patch. See Documentation policies below.

if you’re adding a private API, please add a regular expression to the coverage_ignore_pyobjects variable of docs/conf.py to exclude the new private API from documentation coverage checks.

To see if your private API is skipped properly, generate a documentation coverage report as follows:

tox -e docs-coverage

Submitting patches

The best way to submit a patch is to issue a pull request [https://help.github.com/en/articles/creating-a-pull-request] on GitHub, optionally creating a new issue first.

Remember to explain what was fixed or the new functionality (what it is, why it’s needed, etc). The more info you include, the easier will be for core developers to understand and accept your patch.

You can also discuss the new functionality (or bug fix) before creating the patch, but it’s always good to have a patch ready to illustrate your arguments and show that you have put some additional thought into the subject. A good starting point is to send a pull request on GitHub. It can be simple enough to illustrate your idea, and leave documentation/tests for later, after the idea has been validated and proven useful. Alternatively, you can start a conversation in the Scrapy subreddit [https://reddit.com/r/scrapy] to discuss your idea first.

Sometimes there is an existing pull request for the problem you’d like to solve, which is stalled for some reason. Often the pull request is in a right direction, but changes are requested by Scrapy maintainers, and the original pull request author hasn’t had time to address them. In this case consider picking up this pull request: open a new pull request with all commits from the original pull request, as well as additional changes to address the raised issues. Doing so helps a lot; it is not considered rude as soon as the original author is acknowledged by keeping his/her commits.

You can pull an existing pull request to a local branch by running git fetch upstream pull/$PR_NUMBER/head:$BRANCH_NAME_TO_CREATE (replace ‘upstream’ with a remote name for scrapy repository, $PR_NUMBER with an ID of the pull request, and $BRANCH_NAME_TO_CREATE with a name of the branch you want to create locally). See also: https://help.github.com/articles/checking-out-pull-requests-locally/#modifying-an-inactive-pull-request-locally.

When writing GitHub pull requests, try to keep titles short but descriptive. E.g. For bug #411:「Scrapy hangs if an exception raises in start_requests」prefer「Fix hanging when exception occurs in start_requests (#411)」instead of「Fix for #411」. Complete titles make it easy to skim through the issue tracker.

Finally, try to keep aesthetic changes (PEP 8 [https://www.python.org/dev/peps/pep-0008] compliance, unused imports removal, etc) in separate commits from functional changes. This will make pull requests easier to review and more likely to get merged.

Coding style

Please follow these coding conventions when writing code for inclusion in Scrapy:

Unless otherwise specified, follow PEP 8 [https://www.python.org/dev/peps/pep-0008].

It’s OK to use lines longer than 80 chars if it improves the code readability.

Don’t put your name in the code you contribute; git provides enough metadata to identify author of the code. See https://help.github.com/articles/setting-your-username-in-git/ for setup instructions.

Documentation policies

For reference documentation of API members (classes, methods, etc.) use docstrings and make sure that the Sphinx documentation uses the autodoc [http://www.sphinx-doc.org/en/stable/ext/autodoc.html] extension to pull the docstrings. API reference documentation should follow docstring conventions (PEP 257 [https://www.python.org/dev/peps/pep-0257/]) and be IDE-friendly: short, to the point, and it may provide short examples.

Other types of documentation, such as tutorials or topics, should be covered in files within the docs/ directory. This includes documentation that is specific to an API member, but goes beyond API reference documentation.

In any case, if something is covered in a docstring, use the autodoc [http://www.sphinx-doc.org/en/stable/ext/autodoc.html] extension to pull the docstring into the documentation instead of duplicating the docstring in files within the docs/ directory.

Tests

Tests are implemented using the Twisted unit-testing framework [https://twistedmatrix.com/documents/current/core/development/policy/test-standard.html], running tests requires tox [https://pypi.python.org/pypi/tox].

Running tests

Make sure you have a recent enough tox [https://pypi.python.org/pypi/tox] installation:

tox --version

If your version is older than 1.7.0, please update it first:

pip install -U tox

To run all tests go to the root directory of Scrapy source code and run:

tox

To run a specific test (say tests/test_loader.py) use:

tox -- tests/test_loader.py

To run the tests on a specific tox [https://pypi.python.org/pypi/tox] environment, use -e <name> with an environment name from tox.ini. For example, to run the tests with Python 3.6 use:

tox -e py36

You can also specify a comma-separated list of environmets, and use tox’s parallel mode [https://tox.readthedocs.io/en/latest/example/basic.html#parallel-mode] to run the tests on multiple environments in parallel:

tox -e py27,py36 -p auto

To pass command-line options to pytest [https://docs.pytest.org/en/latest/usage.html], add them after -- in your call to tox [https://pypi.python.org/pypi/tox]. Using -- overrides the default positional arguments defined in tox.ini, so you must include those default positional arguments (scrapy tests) after -- as well:

tox -- scrapy tests -x # stop after first failure

You can also use the pytest-xdist [https://docs.pytest.org/en/3.0.0/xdist.html] plugin. For example, to run all tests on the Python 3.6 tox [https://pypi.python.org/pypi/tox] environment using all your CPU cores:

tox -e py36 -- scrapy tests -n auto

To see coverage report install coverage [https://pypi.python.org/pypi/coverage] (pip install coverage) and run:

coverage report

see output of coverage --help for more options like html or xml report.

Writing tests

All functionality (including new features and bug fixes) must include a test case to check that it works as expected, so please include tests for your patches if you want them to get accepted sooner.

Scrapy uses unit-tests, which are located in the tests/ [https://github.com/scrapy/scrapy/tree/master/tests] directory. Their module name typically resembles the full path of the module they’re testing. For example, the item loaders code is in:

scrapy.loader

And their unit-tests are in:

tests/test_loader.py

Versioning and API Stability

Versioning

There are 3 numbers in a Scrapy version: A.B.C

A is the major version. This will rarely change and will signify very large changes.

B is the release number. This will include many changes including features and things that possibly break backward compatibility, although we strive to keep theses cases at a minimum.

C is the bugfix release number.

Backward-incompatibilities are explicitly mentioned in the release notes, and may require special attention before upgrading.

Development releases do not follow 3-numbers version and are generally released as dev suffixed versions, e.g. 1.3dev.

Note

With Scrapy 0.* series, Scrapy used odd-numbered versions for development releases [https://en.wikipedia.org/wiki/Software_versioning#Odd-numbered_versions_for_development_releases]. This is not the case anymore from Scrapy 1.0 onwards.

Starting with Scrapy 1.0, all releases should be considered production-ready.

For example:

1.1.1 is the first bugfix release of the 1.1 series (safe to use in production)

API Stability

API stability was one of the major goals for the 1.0 release.

Methods or functions that start with a single dash (_) are private and should never be relied as stable.

Also, keep in mind that stable doesn’t mean complete: stable APIs could grow new methods or functionality but the existing methods should keep working the same way.

Python Module Index

s

s

scrapy

scrapy.contracts

scrapy.contracts.default

scrapy.crawler The Scrapy crawler

scrapy.downloadermiddlewares

scrapy.downloadermiddlewares.ajaxcrawl

scrapy.downloadermiddlewares.cookies Cookies Downloader Middleware

scrapy.downloadermiddlewares.defaultheaders Default Headers Downloader Middleware

scrapy.downloadermiddlewares.downloadtimeout Download timeout middleware

scrapy.downloadermiddlewares.httpauth HTTP Auth downloader middleware

scrapy.downloadermiddlewares.httpcache HTTP Cache downloader middleware

scrapy.downloadermiddlewares.httpcompression Http Compression Middleware

scrapy.downloadermiddlewares.httpproxy Http Proxy Middleware

scrapy.downloadermiddlewares.redirect Redirection Middleware

scrapy.downloadermiddlewares.retry Retry Middleware

scrapy.downloadermiddlewares.robotstxt robots.txt middleware

scrapy.downloadermiddlewares.stats Downloader Stats Middleware

scrapy.downloadermiddlewares.useragent User Agent Middleware

scrapy.exceptions Scrapy exceptions

scrapy.exporters Item Exporters

scrapy.extensions.closespider Close spider extension

scrapy.extensions.corestats Core stats collection

scrapy.extensions.debug Extensions for debugging Scrapy

scrapy.extensions.httpcache

scrapy.extensions.logstats Basic stats logging

scrapy.extensions.memdebug Memory debugger extension

scrapy.extensions.memusage Memory usage extension

scrapy.extensions.statsmailer StatsMailer extension

scrapy.extensions.telnet Telnet console

scrapy.http Request and Response classes

scrapy.item Item and Field classes

scrapy.linkextractors Link extractors classes

scrapy.linkextractors.lxmlhtml lxml's HTMLParser-based link extractors

scrapy.loader Item Loader class

scrapy.loader.processors A collection of processors to use with Item Loaders

scrapy.mail Email sending facility

scrapy.pipelines.files Files Pipeline

scrapy.pipelines.images Images Pipeline

scrapy.robotstxt robots.txt parser interface and implementations

scrapy.selector Selector class

scrapy.settings Settings manager

scrapy.signalmanager The signal manager

scrapy.signals Signals definitions

scrapy.spiderloader The spider loader

scrapy.spidermiddlewares

scrapy.spidermiddlewares.depth Depth Spider Middleware

scrapy.spidermiddlewares.httperror HTTP Error Spider Middleware

scrapy.spidermiddlewares.offsite Offsite Spider Middleware

scrapy.spidermiddlewares.referer Referer Spider Middleware

scrapy.spidermiddlewares.urllength URL Length Spider Middleware

scrapy.spiders Spiders base class, spider manager and spider middleware

scrapy.statscollectors Stats Collectors

scrapy.utils.log Logging utils

scrapy.utils.trackref Track references of live objects

Index

_ | A | B | C | D | E | F | G | H | I | J | L | M | N | O | P | Q | R | S | T | U | V | X

_

__bool__() (scrapy.selector.Selector method)

A

adapt_response() (scrapy.spiders.XMLFeedSpider method)

add_css() (scrapy.loader.ItemLoader method)

add_value() (scrapy.loader.ItemLoader method)

add_xpath() (scrapy.loader.ItemLoader method)

adjust_request_args() (scrapy.contracts.Contract method)

AJAXCRAWL_ENABLED setting

AjaxCrawlMiddleware (class in scrapy.downloadermiddlewares.ajaxcrawl)

allowed() (scrapy.robotstxt.RobotParser method)

allowed_domains (scrapy.spiders.Spider attribute)

attrib (scrapy.selector.Selector attribute) (scrapy.selector.SelectorList attribute)

AUTOTHROTTLE_DEBUG setting

AUTOTHROTTLE_ENABLED setting

AUTOTHROTTLE_MAX_DELAY setting

AUTOTHROTTLE_START_DELAY setting

AUTOTHROTTLE_TARGET_CONCURRENCY setting

AWS_ACCESS_KEY_ID setting

AWS_ENDPOINT_URL setting

AWS_REGION_NAME setting

AWS_SECRET_ACCESS_KEY setting

AWS_USE_SSL setting

AWS_VERIFY setting

B

BaseItem (class in scrapy.item)

BaseItemExporter (class in scrapy.exporters)

BaseSettings (class in scrapy.settings)

bench command

bindaddress reqmeta

body (scrapy.http.Request attribute) (scrapy.http.Response attribute)

body_as_unicode() (scrapy.http.TextResponse method)

BOT_NAME setting

C

CacheStorage (class in scrapy.extensions.httpcache)

CallbackKeywordArgumentsContract (class in scrapy.contracts.default)

cb_kwargs (scrapy.http.Request attribute)

check command

clear_stats() (scrapy.statscollectors.StatsCollector method)

close_spider() (scrapy.extensions.httpcache.CacheStorage method)

(scrapy.statscollectors.StatsCollector method)

closed() (scrapy.spiders.Spider method)

CloseSpider (class in scrapy.extensions.closespider)

CLOSESPIDER_ERRORCOUNT setting

CLOSESPIDER_ITEMCOUNT setting

CLOSESPIDER_PAGECOUNT setting

CLOSESPIDER_TIMEOUT setting

command bench

check

crawl

edit

fetch

genspider

list

parse

runspider

settings

shell

startproject

version

view

COMMANDS_MODULE setting

Compose (class in scrapy.loader.processors)

COMPRESSION_ENABLED setting

CONCURRENT_ITEMS setting

CONCURRENT_REQUESTS setting

CONCURRENT_REQUESTS_PER_DOMAIN setting

CONCURRENT_REQUESTS_PER_IP setting

configure_logging() (in module scrapy.utils.log)

connect() (scrapy.signalmanager.SignalManager method)

context (scrapy.loader.ItemLoader attribute)

Contract (class in scrapy.contracts)

ContractFail (class in scrapy.exceptions)

cookiejar reqmeta

COOKIES_DEBUG setting

COOKIES_ENABLED setting

CookiesMiddleware (class in scrapy.downloadermiddlewares.cookies)

copy() (scrapy.http.Request method) (scrapy.http.Response method)

(scrapy.item.Item method)

(scrapy.settings.BaseSettings method)

copy_to_dict() (scrapy.settings.BaseSettings method)

CoreStats (class in scrapy.extensions.corestats)

crawl command

crawl() (scrapy.crawler.Crawler method) (scrapy.crawler.CrawlerProcess method)

(scrapy.crawler.CrawlerRunner method)

crawled() (scrapy.logformatter.LogFormatter method)

Crawler (class in scrapy.crawler)

crawler (scrapy.spiders.Spider attribute)

CrawlerProcess (class in scrapy.crawler)

CrawlerRunner (class in scrapy.crawler)

crawlers (scrapy.crawler.CrawlerProcess attribute) (scrapy.crawler.CrawlerRunner attribute)

CrawlSpider (class in scrapy.spiders)

create_crawler() (scrapy.crawler.CrawlerProcess method) (scrapy.crawler.CrawlerRunner method)

css() (scrapy.http.TextResponse method) (scrapy.selector.Selector method)

(scrapy.selector.SelectorList method)

CSVFeedSpider (class in scrapy.spiders)

CsvItemExporter (class in scrapy.exporters)

custom_settings (scrapy.spiders.Spider attribute)

D

DbmCacheStorage (class in scrapy.extensions.httpcache)

Debugger (class in scrapy.extensions.debug)

deepcopy() (scrapy.item.Item method)

default_input_processor (scrapy.loader.ItemLoader attribute)

DEFAULT_ITEM_CLASS setting

default_item_class (scrapy.loader.ItemLoader attribute)

default_output_processor (scrapy.loader.ItemLoader attribute)

DEFAULT_REQUEST_HEADERS setting

default_selector_class (scrapy.loader.ItemLoader attribute)

DefaultHeadersMiddleware (class in scrapy.downloadermiddlewares.defaultheaders)

DefaultReferrerPolicy (class in scrapy.spidermiddlewares.referer)

delimiter (scrapy.spiders.CSVFeedSpider attribute)

DEPTH_LIMIT setting

DEPTH_PRIORITY setting

DEPTH_STATS_VERBOSE setting

DepthMiddleware (class in scrapy.spidermiddlewares.depth)

disconnect() (scrapy.signalmanager.SignalManager method)

disconnect_all() (scrapy.signalmanager.SignalManager method)

DNS_TIMEOUT setting

DNSCACHE_ENABLED setting

DNSCACHE_SIZE setting

dont_cache reqmeta

dont_merge_cookies reqmeta

dont_obey_robotstxt reqmeta

dont_redirect reqmeta

dont_retry reqmeta

DontCloseSpider

DOWNLOAD_DELAY setting

DOWNLOAD_FAIL_ON_DATALOSS setting

download_fail_on_dataloss reqmeta

DOWNLOAD_HANDLERS setting

DOWNLOAD_HANDLERS_BASE setting

download_latency reqmeta

DOWNLOAD_MAXSIZE setting

download_maxsize reqmeta

DOWNLOAD_TIMEOUT setting

download_timeout reqmeta

DOWNLOAD_WARNSIZE setting

DOWNLOADER setting

DOWNLOADER_CLIENT_TLS_CIPHERS setting

DOWNLOADER_CLIENT_TLS_METHOD setting

DOWNLOADER_CLIENT_TLS_VERBOSE_LOGGING setting

DOWNLOADER_CLIENTCONTEXTFACTORY setting

DOWNLOADER_HTTPCLIENTFACTORY setting

DOWNLOADER_MIDDLEWARES setting

DOWNLOADER_MIDDLEWARES_BASE setting

DOWNLOADER_STATS setting

DownloaderMiddleware (class in scrapy.downloadermiddlewares)

DownloaderStats (class in scrapy.downloadermiddlewares.stats)

DownloadTimeoutMiddleware (class in scrapy.downloadermiddlewares.downloadtimeout)

DropItem

dropped() (scrapy.logformatter.LogFormatter method)

DummyPolicy (class in scrapy.extensions.httpcache)

DummyStatsCollector (class in scrapy.statscollectors)

DUPEFILTER_CLASS setting

DUPEFILTER_DEBUG setting

E

edit command

EDITOR setting

encoding (scrapy.exporters.BaseItemExporter attribute) (scrapy.http.TextResponse attribute)

engine (scrapy.crawler.Crawler attribute)

engine_started signal

engine_started() (in module scrapy.signals)

engine_stopped signal

engine_stopped() (in module scrapy.signals)

export_empty_fields (scrapy.exporters.BaseItemExporter attribute)

export_item() (scrapy.exporters.BaseItemExporter method)

EXTENSIONS setting

extensions (scrapy.crawler.Crawler attribute)

EXTENSIONS_BASE setting

F

FEED_EXPORT_ENCODING setting

FEED_EXPORT_FIELDS setting

FEED_EXPORT_INDENT setting

FEED_EXPORTERS setting

FEED_EXPORTERS_BASE setting

FEED_FORMAT setting

FEED_STORAGE_FTP_ACTIVE setting

FEED_STORAGE_S3_ACL setting

FEED_STORAGES setting

FEED_STORAGES_BASE setting

FEED_STORE_EMPTY setting

FEED_TEMPDIR setting

FEED_URI setting

fetch command

Field (class in scrapy.item)

fields (scrapy.item.Item attribute)

fields_to_export (scrapy.exporters.BaseItemExporter attribute)

file_path() (scrapy.pipelines.files.FilesPipeline method) (scrapy.pipelines.images.ImagesPipeline method)

FILES_EXPIRES setting

FILES_RESULT_FIELD setting

FILES_STORE setting

FILES_STORE_GCS_ACL setting

FILES_STORE_S3_ACL setting

FILES_URLS_FIELD setting

FilesPipeline (class in scrapy.pipelines.files)

FilesystemCacheStorage (class in scrapy.extensions.httpcache)

find_by_request() (scrapy.spiderloader.SpiderLoader method)

finish_exporting() (scrapy.exporters.BaseItemExporter method)

flags (scrapy.http.Response attribute)

follow() (scrapy.http.Response method) (scrapy.http.TextResponse method)

FormRequest (class in scrapy.http)

freeze() (scrapy.settings.BaseSettings method)

from_crawler() (scrapy.downloadermiddlewares.DownloaderMiddleware method)

(scrapy.robotstxt.RobotParser class method)

(scrapy.spidermiddlewares.SpiderMiddleware method)

(scrapy.spiders.Spider method)

from_curl() (scrapy.http.Request class method)

from_response() (scrapy.http.FormRequest class method)

from_settings() (scrapy.mail.MailSender class method) (scrapy.spiderloader.SpiderLoader method)

frozencopy() (scrapy.settings.BaseSettings method)

FTP_PASSIVE_MODE setting

FTP_PASSWORD setting

ftp_password reqmeta

FTP_USER setting

ftp_user reqmeta

G

GCS_PROJECT_ID setting

genspider command

get() (scrapy.selector.Selector method) (scrapy.selector.SelectorList method)

(scrapy.settings.BaseSettings method)

get_collected_values() (scrapy.loader.ItemLoader method)

get_css() (scrapy.loader.ItemLoader method)

get_input_processor() (scrapy.loader.ItemLoader method)

get_media_requests() (scrapy.pipelines.files.FilesPipeline method) (scrapy.pipelines.images.ImagesPipeline method)

get_oldest() (in module scrapy.utils.trackref)

get_output_processor() (scrapy.loader.ItemLoader method)

get_output_value() (scrapy.loader.ItemLoader method)

get_settings_priority() (in module scrapy.settings)

get_stats() (scrapy.statscollectors.StatsCollector method)

get_value() (scrapy.loader.ItemLoader method) (scrapy.statscollectors.StatsCollector method)

get_xpath() (scrapy.loader.ItemLoader method)

getall() (scrapy.selector.Selector method) (scrapy.selector.SelectorList method)

getbool() (scrapy.settings.BaseSettings method)

getdict() (scrapy.settings.BaseSettings method)

getfloat() (scrapy.settings.BaseSettings method)

getint() (scrapy.settings.BaseSettings method)

getlist() (scrapy.settings.BaseSettings method)

getpriority() (scrapy.settings.BaseSettings method)

getwithbase() (scrapy.settings.BaseSettings method)

H

handle_httpstatus_all reqmeta

handle_httpstatus_list reqmeta

headers (scrapy.http.Request attribute) (scrapy.http.Response attribute)

(scrapy.spiders.CSVFeedSpider attribute)

HtmlResponse (class in scrapy.http)

HttpAuthMiddleware (class in scrapy.downloadermiddlewares.httpauth)

HTTPCACHE_ALWAYS_STORE setting

HTTPCACHE_DBM_MODULE setting

HTTPCACHE_DIR setting

HTTPCACHE_ENABLED setting

HTTPCACHE_EXPIRATION_SECS setting

HTTPCACHE_GZIP setting

HTTPCACHE_IGNORE_HTTP_CODES setting

HTTPCACHE_IGNORE_MISSING setting

HTTPCACHE_IGNORE_RESPONSE_CACHE_CONTROLS setting

HTTPCACHE_IGNORE_SCHEMES setting

HTTPCACHE_POLICY setting

HTTPCACHE_STORAGE setting

HttpCacheMiddleware (class in scrapy.downloadermiddlewares.httpcache)

HttpCompressionMiddleware (class in scrapy.downloadermiddlewares.httpcompression)

HTTPERROR_ALLOW_ALL setting

HTTPERROR_ALLOWED_CODES setting

HttpErrorMiddleware (class in scrapy.spidermiddlewares.httperror)

HTTPPROXY_AUTH_ENCODING setting

HTTPPROXY_ENABLED setting

HttpProxyMiddleware (class in scrapy.downloadermiddlewares.httpproxy)

I

Identity (class in scrapy.loader.processors)

IgnoreRequest

IMAGES_EXPIRES setting

IMAGES_MIN_HEIGHT setting

IMAGES_MIN_WIDTH setting

IMAGES_RESULT_FIELD setting

IMAGES_STORE setting

IMAGES_STORE_GCS_ACL setting

IMAGES_STORE_S3_ACL setting

IMAGES_THUMBS setting

IMAGES_URLS_FIELD setting

ImagesPipeline (class in scrapy.pipelines.images)

inc_value() (scrapy.statscollectors.StatsCollector method)

indent (scrapy.exporters.BaseItemExporter attribute)

Item (class in scrapy.item)

item (scrapy.loader.ItemLoader attribute)

item_completed() (scrapy.pipelines.files.FilesPipeline method) (scrapy.pipelines.images.ImagesPipeline method)

item_dropped signal

item_dropped() (in module scrapy.signals)

item_error signal

item_error() (in module scrapy.signals)

ITEM_PIPELINES setting

ITEM_PIPELINES_BASE setting

item_scraped signal

item_scraped() (in module scrapy.signals)

ItemLoader (class in scrapy.loader)

ItemMeta (class in scrapy.item)

iter_all() (in module scrapy.utils.trackref)

iterator (scrapy.spiders.XMLFeedSpider attribute)

itertag (scrapy.spiders.XMLFeedSpider attribute)

J

Join (class in scrapy.loader.processors)

join() (scrapy.crawler.CrawlerProcess method) (scrapy.crawler.CrawlerRunner method)

JsonItemExporter (class in scrapy.exporters)

JsonLinesItemExporter (class in scrapy.exporters)

JsonRequest (class in scrapy.http)

L

list command

list() (scrapy.spiderloader.SpiderLoader method)

load() (scrapy.spiderloader.SpiderLoader method)

load_item() (scrapy.loader.ItemLoader method)

log() (scrapy.spiders.Spider method)

LOG_DATEFORMAT setting

LOG_ENABLED setting

LOG_ENCODING setting

LOG_FILE setting

LOG_FORMAT setting

LOG_FORMATTER setting

LOG_LEVEL setting

LOG_SHORT_NAMES setting

LOG_STDOUT setting

LogFormatter (class in scrapy.logformatter)

logger (scrapy.spiders.Spider attribute)

LogStats (class in scrapy.extensions.logstats)

LOGSTATS_INTERVAL setting

LxmlLinkExtractor (class in scrapy.linkextractors.lxmlhtml)

M

MAIL_FROM setting

MAIL_HOST setting

MAIL_PASS setting

MAIL_PORT setting

MAIL_SSL setting

MAIL_TLS setting

MAIL_USER setting

MailSender (class in scrapy.mail)

MapCompose (class in scrapy.loader.processors)

MarshalItemExporter (class in scrapy.exporters)

max_retry_times reqmeta

max_value() (scrapy.statscollectors.StatsCollector method)

maxpriority() (scrapy.settings.BaseSettings method)

MEDIA_ALLOW_REDIRECTS setting

MEMDEBUG_ENABLED setting

MEMDEBUG_NOTIFY setting

MemoryDebugger (class in scrapy.extensions.memdebug)

MemoryStatsCollector (class in scrapy.statscollectors)

MemoryUsage (class in scrapy.extensions.memusage)

MEMUSAGE_CHECK_INTERVAL_SECONDS setting

MEMUSAGE_ENABLED setting

MEMUSAGE_LIMIT_MB setting

MEMUSAGE_NOTIFY_MAIL setting

MEMUSAGE_WARNING_MB setting

meta (scrapy.http.Request attribute) (scrapy.http.Response attribute)

METAREFRESH_ENABLED setting

METAREFRESH_IGNORE_TAGS setting

METAREFRESH_MAXDELAY setting

MetaRefreshMiddleware (class in scrapy.downloadermiddlewares.redirect)

method (scrapy.http.Request attribute)

min_value() (scrapy.statscollectors.StatsCollector method)

N

name (scrapy.spiders.Spider attribute)

namespaces (scrapy.spiders.XMLFeedSpider attribute)

nested_css() (scrapy.loader.ItemLoader method)

nested_xpath() (scrapy.loader.ItemLoader method)

NEWSPIDER_MODULE setting

NoReferrerPolicy (class in scrapy.spidermiddlewares.referer)

NoReferrerWhenDowngradePolicy (class in scrapy.spidermiddlewares.referer)

NotConfigured

NotSupported

O

object_ref (class in scrapy.utils.trackref)

OffsiteMiddleware (class in scrapy.spidermiddlewares.offsite)

open_spider() (scrapy.extensions.httpcache.CacheStorage method)

(scrapy.statscollectors.StatsCollector method)

OriginPolicy (class in scrapy.spidermiddlewares.referer)

OriginWhenCrossOriginPolicy (class in scrapy.spidermiddlewares.referer)

P

parse command

parse() (scrapy.spiders.Spider method)

parse_node() (scrapy.spiders.XMLFeedSpider method)

parse_row() (scrapy.spiders.CSVFeedSpider method)

parse_start_url() (scrapy.spiders.CrawlSpider method)

PickleItemExporter (class in scrapy.exporters)

post_process() (scrapy.contracts.Contract method)

PprintItemExporter (class in scrapy.exporters)

pre_process() (scrapy.contracts.Contract method)

print_live_refs() (in module scrapy.utils.trackref)

process_exception() (scrapy.downloadermiddlewares.DownloaderMiddleware method)

process_item()

process_request() (scrapy.downloadermiddlewares.DownloaderMiddleware method)

process_response() (scrapy.downloadermiddlewares.DownloaderMiddleware method)

process_results() (scrapy.spiders.XMLFeedSpider method)

process_spider_exception() (scrapy.spidermiddlewares.SpiderMiddleware method)

process_spider_input() (scrapy.spidermiddlewares.SpiderMiddleware method)

process_spider_output() (scrapy.spidermiddlewares.SpiderMiddleware method)

process_start_requests() (scrapy.spidermiddlewares.SpiderMiddleware method)

proxy reqmeta

Python Enhancement Proposals PEP 8, [1]

PythonItemExporter (class in scrapy.exporters)

Q

quotechar (scrapy.spiders.CSVFeedSpider attribute)

R

RANDOMIZE_DOWNLOAD_DELAY setting

re() (scrapy.selector.Selector method) (scrapy.selector.SelectorList method)

re_first() (scrapy.selector.Selector method) (scrapy.selector.SelectorList method)

REACTOR_THREADPOOL_MAXSIZE setting

REDIRECT_ENABLED setting

REDIRECT_MAX_TIMES setting, [1]

REDIRECT_PRIORITY_ADJUST setting

redirect_reasons reqmeta

redirect_urls reqmeta

RedirectMiddleware (class in scrapy.downloadermiddlewares.redirect)

REFERER_ENABLED setting

RefererMiddleware (class in scrapy.spidermiddlewares.referer)

REFERRER_POLICY setting

referrer_policy reqmeta

register_namespace() (scrapy.selector.Selector method)

remove_namespaces() (scrapy.selector.Selector method)

replace() (scrapy.http.Request method) (scrapy.http.Response method)

replace_css() (scrapy.loader.ItemLoader method)

replace_value() (scrapy.loader.ItemLoader method)

replace_xpath() (scrapy.loader.ItemLoader method)

reqmeta bindaddress

cookiejar

dont_cache

dont_merge_cookies

dont_obey_robotstxt

dont_redirect

dont_retry

download_fail_on_dataloss

download_latency

download_maxsize

download_timeout

ftp_password

ftp_user

handle_httpstatus_all

handle_httpstatus_list

max_retry_times

proxy

redirect_reasons

redirect_urls

referrer_policy

Request (class in scrapy.http)

request (scrapy.http.Response attribute)

request_dropped signal

request_dropped() (in module scrapy.signals)

request_reached_downloader signal

request_reached_downloader() (in module scrapy.signals)

request_scheduled signal

request_scheduled() (in module scrapy.signals)

Response (class in scrapy.http)

response_downloaded signal

response_downloaded() (in module scrapy.signals)

response_received signal

response_received() (in module scrapy.signals)

retrieve_response() (scrapy.extensions.httpcache.CacheStorage method)

RETRY_ENABLED setting

RETRY_HTTP_CODES setting

RETRY_PRIORITY_ADJUST setting

RETRY_TIMES setting

RetryMiddleware (class in scrapy.downloadermiddlewares.retry)

ReturnsContract (class in scrapy.contracts.default)

RFC2616Policy (class in scrapy.extensions.httpcache)

RobotParser (class in scrapy.robotstxt)

ROBOTSTXT_OBEY setting

ROBOTSTXT_PARSER setting

ROBOTSTXT_USER_AGENT setting

RobotsTxtMiddleware (class in scrapy.downloadermiddlewares.robotstxt)

Rule (class in scrapy.spiders)

rules (scrapy.spiders.CrawlSpider attribute)

runspider command

S

SameOriginPolicy (class in scrapy.spidermiddlewares.referer)

SCHEDULER setting

SCHEDULER_DEBUG setting

SCHEDULER_DISK_QUEUE setting

SCHEDULER_MEMORY_QUEUE setting

SCHEDULER_PRIORITY_QUEUE setting

scraped() (scrapy.logformatter.LogFormatter method)

ScrapesContract (class in scrapy.contracts.default)

scrapy.contracts (module)

scrapy.contracts.default (module)

scrapy.crawler (module)

scrapy.downloadermiddlewares (module)

scrapy.downloadermiddlewares.ajaxcrawl (module)

scrapy.downloadermiddlewares.cookies (module)

scrapy.downloadermiddlewares.defaultheaders (module)

scrapy.downloadermiddlewares.downloadtimeout (module)

scrapy.downloadermiddlewares.httpauth (module)

scrapy.downloadermiddlewares.httpcache (module)

scrapy.downloadermiddlewares.httpcompression (module)

scrapy.downloadermiddlewares.httpproxy (module)

scrapy.downloadermiddlewares.redirect (module)

scrapy.downloadermiddlewares.retry (module)

scrapy.downloadermiddlewares.robotstxt (module)

scrapy.downloadermiddlewares.stats (module)

scrapy.downloadermiddlewares.useragent (module)

scrapy.exceptions (module)

scrapy.exporters (module)

scrapy.extensions.closespider (module)

scrapy.extensions.corestats (module)

scrapy.extensions.debug (module)

scrapy.extensions.httpcache (module)

scrapy.extensions.logstats (module)

scrapy.extensions.memdebug (module)

scrapy.extensions.memusage (module)

scrapy.extensions.statsmailer (module)

scrapy.extensions.telnet (module)

scrapy.http (module)

scrapy.item (module)

scrapy.linkextractors (module)

scrapy.linkextractors.lxmlhtml (module)

scrapy.loader (module)

scrapy.loader.processors (module)

scrapy.mail (module)

scrapy.pipelines.files (module)

scrapy.pipelines.images (module)

scrapy.robotstxt (module)

scrapy.selector (module)

scrapy.settings (module)

scrapy.signalmanager (module)

scrapy.signals (module)

scrapy.spiderloader (module)

scrapy.spidermiddlewares (module)

scrapy.spidermiddlewares.depth (module)

scrapy.spidermiddlewares.httperror (module)

scrapy.spidermiddlewares.offsite (module)

scrapy.spidermiddlewares.referer (module)

scrapy.spidermiddlewares.urllength (module)

scrapy.spiders (module)

scrapy.statscollectors (module)

scrapy.utils.log (module)

scrapy.utils.trackref (module)

SelectJmes (class in scrapy.loader.processors)

Selector (class in scrapy.selector)

selector (scrapy.http.TextResponse attribute) (scrapy.loader.ItemLoader attribute)

SelectorList (class in scrapy.selector)

send() (scrapy.mail.MailSender method)

send_catch_log() (scrapy.signalmanager.SignalManager method)

send_catch_log_deferred() (scrapy.signalmanager.SignalManager method)

serialize_field() (scrapy.exporters.BaseItemExporter method)

set() (scrapy.settings.BaseSettings method)

set_stats() (scrapy.statscollectors.StatsCollector method)

set_value() (scrapy.statscollectors.StatsCollector method)

set_xpathfunc() (in module parsel.xpathfuncs)

setmodule() (scrapy.settings.BaseSettings method)

setting AJAXCRAWL_ENABLED

AUTOTHROTTLE_DEBUG

AUTOTHROTTLE_ENABLED

AUTOTHROTTLE_MAX_DELAY

AUTOTHROTTLE_START_DELAY

AUTOTHROTTLE_TARGET_CONCURRENCY

AWS_ACCESS_KEY_ID

AWS_ENDPOINT_URL

AWS_REGION_NAME

AWS_SECRET_ACCESS_KEY

AWS_USE_SSL

AWS_VERIFY

BOT_NAME

CLOSESPIDER_ERRORCOUNT

CLOSESPIDER_ITEMCOUNT

CLOSESPIDER_PAGECOUNT

CLOSESPIDER_TIMEOUT

COMMANDS_MODULE

COMPRESSION_ENABLED

CONCURRENT_ITEMS

CONCURRENT_REQUESTS

CONCURRENT_REQUESTS_PER_DOMAIN

CONCURRENT_REQUESTS_PER_IP

COOKIES_DEBUG

COOKIES_ENABLED

DEFAULT_ITEM_CLASS

DEFAULT_REQUEST_HEADERS

DEPTH_LIMIT

DEPTH_PRIORITY

DEPTH_STATS_VERBOSE

DNSCACHE_ENABLED

DNSCACHE_SIZE

DNS_TIMEOUT

DOWNLOADER

DOWNLOADER_CLIENTCONTEXTFACTORY

DOWNLOADER_CLIENT_TLS_CIPHERS

DOWNLOADER_CLIENT_TLS_METHOD

DOWNLOADER_CLIENT_TLS_VERBOSE_LOGGING

DOWNLOADER_HTTPCLIENTFACTORY

DOWNLOADER_MIDDLEWARES

DOWNLOADER_MIDDLEWARES_BASE

DOWNLOADER_STATS

DOWNLOAD_DELAY

DOWNLOAD_FAIL_ON_DATALOSS

DOWNLOAD_HANDLERS

DOWNLOAD_HANDLERS_BASE

DOWNLOAD_MAXSIZE

DOWNLOAD_TIMEOUT

DOWNLOAD_WARNSIZE

DUPEFILTER_CLASS

DUPEFILTER_DEBUG

EDITOR

EXTENSIONS

EXTENSIONS_BASE

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

FEED_TEMPDIR

FEED_URI

FILES_EXPIRES

FILES_RESULT_FIELD

FILES_STORE

FILES_STORE_GCS_ACL

FILES_STORE_S3_ACL

FILES_URLS_FIELD

FTP_PASSIVE_MODE

FTP_PASSWORD

FTP_USER

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

ITEM_PIPELINES

ITEM_PIPELINES_BASE

LOGSTATS_INTERVAL

LOG_DATEFORMAT

LOG_ENABLED

LOG_ENCODING

LOG_FILE

LOG_FORMAT

LOG_FORMATTER

LOG_LEVEL

LOG_SHORT_NAMES

LOG_STDOUT

MAIL_FROM

MAIL_HOST

MAIL_PASS

MAIL_PORT

MAIL_SSL

MAIL_TLS

MAIL_USER

MEDIA_ALLOW_REDIRECTS

MEMDEBUG_ENABLED

MEMDEBUG_NOTIFY

MEMUSAGE_CHECK_INTERVAL_SECONDS

MEMUSAGE_ENABLED

MEMUSAGE_LIMIT_MB

MEMUSAGE_NOTIFY_MAIL

MEMUSAGE_WARNING_MB

METAREFRESH_ENABLED

METAREFRESH_IGNORE_TAGS

METAREFRESH_MAXDELAY

NEWSPIDER_MODULE

RANDOMIZE_DOWNLOAD_DELAY

REACTOR_THREADPOOL_MAXSIZE

REDIRECT_ENABLED

REDIRECT_MAX_TIMES, [1]

REDIRECT_PRIORITY_ADJUST

REFERER_ENABLED

REFERRER_POLICY

RETRY_ENABLED

RETRY_HTTP_CODES

RETRY_PRIORITY_ADJUST

RETRY_TIMES

ROBOTSTXT_OBEY

ROBOTSTXT_PARSER

ROBOTSTXT_USER_AGENT

SCHEDULER

SCHEDULER_DEBUG

SCHEDULER_DISK_QUEUE

SCHEDULER_MEMORY_QUEUE

SCHEDULER_PRIORITY_QUEUE

SPIDER_CONTRACTS

SPIDER_CONTRACTS_BASE

SPIDER_LOADER_CLASS

SPIDER_LOADER_WARN_ONLY

SPIDER_MIDDLEWARES

SPIDER_MIDDLEWARES_BASE

SPIDER_MODULES

STATSMAILER_RCPTS

STATS_CLASS

STATS_DUMP

TELNETCONSOLE_ENABLED

TELNETCONSOLE_HOST

TELNETCONSOLE_PASSWORD

TELNETCONSOLE_PORT, [1]

TELNETCONSOLE_USERNAME

TEMPLATES_DIR

URLLENGTH_LIMIT

USER_AGENT

settings command

Settings (class in scrapy.settings)

settings (scrapy.crawler.Crawler attribute) (scrapy.spiders.Spider attribute)

SETTINGS_PRIORITIES (in module scrapy.settings)

shell command

signal engine_started

engine_stopped

item_dropped

item_error

item_scraped

request_dropped

request_reached_downloader

request_scheduled

response_downloaded

response_received

spider_closed

spider_error

spider_idle

spider_opened

update_telnet_vars

SignalManager (class in scrapy.signalmanager)

signals (scrapy.crawler.Crawler attribute)

sitemap_alternate_links (scrapy.spiders.SitemapSpider attribute)

sitemap_filter() (scrapy.spiders.SitemapSpider method)

sitemap_follow (scrapy.spiders.SitemapSpider attribute)

sitemap_rules (scrapy.spiders.SitemapSpider attribute)

sitemap_urls (scrapy.spiders.SitemapSpider attribute)

SitemapSpider (class in scrapy.spiders)

Spider (class in scrapy.spiders)

spider (scrapy.crawler.Crawler attribute)

spider_closed signal

spider_closed() (in module scrapy.signals)

SPIDER_CONTRACTS setting

SPIDER_CONTRACTS_BASE setting

spider_error signal

spider_error() (in module scrapy.signals)

spider_idle signal

spider_idle() (in module scrapy.signals)

SPIDER_LOADER_CLASS setting

SPIDER_LOADER_WARN_ONLY setting

SPIDER_MIDDLEWARES setting

SPIDER_MIDDLEWARES_BASE setting

SPIDER_MODULES setting

spider_opened signal

spider_opened() (in module scrapy.signals)

spider_stats (scrapy.statscollectors.MemoryStatsCollector attribute)

SpiderLoader (class in scrapy.spiderloader)

SpiderMiddleware (class in scrapy.spidermiddlewares)

StackTraceDump (class in scrapy.extensions.debug)

start() (scrapy.crawler.CrawlerProcess method)

start_exporting() (scrapy.exporters.BaseItemExporter method)

start_requests() (scrapy.spiders.Spider method)

start_urls (scrapy.spiders.Spider attribute)

startproject command

stats (scrapy.crawler.Crawler attribute)

STATS_CLASS setting

STATS_DUMP setting

StatsCollector (class in scrapy.statscollectors)

StatsMailer (class in scrapy.extensions.statsmailer)

STATSMAILER_RCPTS setting

status (scrapy.http.Response attribute)

stop() (scrapy.crawler.Crawler method) (scrapy.crawler.CrawlerProcess method)

(scrapy.crawler.CrawlerRunner method)

store_response() (scrapy.extensions.httpcache.CacheStorage method)

StrictOriginPolicy (class in scrapy.spidermiddlewares.referer)

StrictOriginWhenCrossOriginPolicy (class in scrapy.spidermiddlewares.referer)

T

TakeFirst (class in scrapy.loader.processors)

TelnetConsole (class in scrapy.extensions.telnet)

TELNETCONSOLE_ENABLED setting

TELNETCONSOLE_HOST setting

TELNETCONSOLE_PASSWORD setting

TELNETCONSOLE_PORT setting, [1]

TELNETCONSOLE_USERNAME setting

TEMPLATES_DIR setting

text (scrapy.http.TextResponse attribute)

TextResponse (class in scrapy.http)

U

UnsafeUrlPolicy (class in scrapy.spidermiddlewares.referer)

update() (scrapy.settings.BaseSettings method)

update_telnet_vars signal

update_telnet_vars() (in module scrapy.extensions.telnet)

url (scrapy.http.Request attribute) (scrapy.http.Response attribute)

UrlContract (class in scrapy.contracts.default)

urljoin() (scrapy.http.Response method)

URLLENGTH_LIMIT setting

UrlLengthMiddleware (class in scrapy.spidermiddlewares.urllength)

USER_AGENT setting

UserAgentMiddleware (class in scrapy.downloadermiddlewares.useragent)

V

version command

view command

X

XMLFeedSpider (class in scrapy.spiders)

XmlItemExporter (class in scrapy.exporters)

XmlResponse (class in scrapy.http)

xpath() (scrapy.http.TextResponse method) (scrapy.selector.Selector method)

(scrapy.selector.SelectorList method)

Scrapy documentation quick start guide

This file provides a quick guide on how to compile the Scrapy documentation.

Setup the environment

To compile the documentation you need Sphinx Python library. To install it and all its dependencies run the following command from this dir

pip install -r requirements.txt

Compile the documentation

To compile the documentation (to classic HTML output) run the following command from this dir:

make html

Documentation will be generated (in HTML format) inside the build/html dir.

View the documentation

To view the documentation run the following command:

make htmlview

This command will fire up your default browser and open the main page of your (previously generated) HTML documentation.

Start over

To cleanup all generated documentation files and start from scratch run:

make clean

Keep in mind that this command won’t touch any documentation source files.

Recreating documentation on the fly

There is a way to recreate the doc automatically when you make changes, you need to install watchdog (pip install watchdog) and then use:

make watch

DjangoItem

DjangoItem has been moved into a separate project.

It is hosted at:

https://github.com/scrapy-plugins/scrapy-djangoitem

Scrapyd

Scrapyd has been moved into a separate project.

Its documentation is now hosted at:

https://scrapyd.readthedocs.io/en/latest/

