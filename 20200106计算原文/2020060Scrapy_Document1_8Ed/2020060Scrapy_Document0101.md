# 01 First steps

## 01. Scrapy at a glance

Scrapy is an application framework for crawling web sites and extracting structured data which can be used for a wide range of useful applications, like data mining, information processing or historical archival.

Even though Scrapy was originally designed for web scraping, it can also be used to extract data using APIs (such as Amazon Associates Web Services [https://affiliate-program.amazon.com/gp/advertising/api/detail/main.html]) or as a general purpose web crawler.

### 1. Walk-through of an example spider

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

## 02. Installation guide

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

## Examples

The best way to learn is with examples, and Scrapy is no exception. For this reason, there is an example Scrapy project named quotesbot [https://github.com/scrapy/quotesbot], that you can use to play and learn more about Scrapy. It contains two spiders for http://quotes.toscrape.com, one using CSS selectors and another one using XPath expressions.

The quotesbot [https://github.com/scrapy/quotesbot] project is available at: https://github.com/scrapy/quotesbot. You can find more information about it in the project’s README.

If you’re familiar with git, you can checkout the code. Otherwise you can download the project as a zip file by clicking here [https://github.com/scrapy/quotesbot/archive/master.zip].



