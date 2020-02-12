# 05 Extending Scrapy

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