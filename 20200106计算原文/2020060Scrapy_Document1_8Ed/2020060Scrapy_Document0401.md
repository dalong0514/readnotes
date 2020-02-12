# 04 Solving speciﬁc problems

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

