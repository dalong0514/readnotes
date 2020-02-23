# 05 Handling JavaScript

This chapter is all about handling websites that utilize JavaScript to render information dynamically.

You have seen in the previous chapters that a basic website scraper loads the web page’s contents and does its extraction on this source code. And if there’s JavaScript included, it’s not executed, and the dynamic information is missing from the page.

This is bad, at least in those cases where you need that dynamic data.

Another interesting part of scraping websites that use JavaScript is that you may need clicks or button presses to go to the right page / get the right content, because these actions call a chain of JavaScript functions.

Now I will give you options for how you can deal with these problems. Most of the time you will find Selenium as the solution, if you Google or search the Internet with other engines. However, there are other options present, and I will give you more insight. Perhaps those other options will fit your needs better.

## 01. Reverse Engineering

This first option is for advanced developers—at least I feel advanced developers will do more reverse engineering.

The idea here is to use the DevTools from Chrome (or similar functionality in other browsers), enable JavaScript, and monitor the XHR network flow to find out which data is requested from the server and rendered separately.

With the target endpoint (either a GET or a POST request) in your hands, you see which parameters to provide and how they affect the results.

Let’s look at a simple example: at kayak.com you can search for flights and, therefore, airports too. In this simple example we will reverse engineer the destination search endpoint to extract some information, even if this information is not valuable.

I’ll use Chrome for these examples. This is because I use Chrome for all my scraping tasks. It will work with Firefox too, if you know how to handle the developer tools.

First let’s go to kayak.com, open up the DevTools window, and locate the Network tab there, as shown in Figure 5-1.

Figure 5-1. Kayak.com with DevTools open

As you can see in the image, I already navigated to the XHR tab inside the Network tab because all AJAX and XHR calls are listed here.

Now let’s click the field on the website labeled To? and type in a letter, for example S, and watch the values on the right side inside the XHR tab, as shown in Figure 5-2.

Figure 5-2. A small list of airports

Now you get a list of some possible airports on the website, but two XHR requests too. We’re interested in the request starting with marvel:

www.kayak.com/mv/marvel?f=h&where=so&s=50&lc_cc=US&lc=en&v=v2&cv=5.

This is the request that returns the information about the airport. It has some parameters where I have no idea what they do and how the results are affected if changed, but here’s what I know:

• where is the key you’re searching for

• s is the type of the search; 58 is for airports

• lc is the locale; you can change it and get different results—more on this later

• v is the version; there’s a small difference in the result format if you choose v1 instead of the default v2

Based on this information, what can we get out of it? We get some airports, and some idea about how to reverse engineer JavaScript and when to decide to use a different tool.

In this example, the JavaScript rendering is a simple HTTP GET call—nothing fancy, and I bet you already have an idea how to extract information delivered from these endpoints. Yes, using either the requests and Beautiful Soup libraries or Scrapy and some Request objects.

Back to the example: when you vary the lc value, for example, to de or es in the request, you get back different airports and the description of these airports in the locale you chose. This means JavaScript reverse engineering is not just about finding the right calls you want to use but also requires a bit of thinking.

### Thoughts on Reverse Engineering

If you find yourself having a search that utilizes an HTTP endpoint to get the data, you can try to figure out how the search works. For example, instead of sending some values you expect to deliver results, try to add search expressions. Such expressions could be * to match all, .+ to evaluate regular expressions, or % if it has some kind of SQL query in the back.

### Summary

You see, sometimes JavaScript reverse engineering pays off: you learned that those nasty XHR calls are simple requests and you can cover them from your scripts. However, sometimes JavaScript makes more complex things like rendering and loading data after the initial page is loaded. And you don’t want to reverse engineer this, believe me.

## 02. Splash

Splash 1 is an open-source JavaScript rendering engine written in Python. It is lightweight and has a smooth integration with Scrapy.

It is maintained, and new versions are released every few months, when need arises.

1 [Splash - A javascript rendering service — Splash 3.4 documentation](https://splash.readthedocs.io/en/stable/)

### 1. Set-up

The basic and easiest usage of Splash is getting a Docker image from the developers and running it. This ensures that you have all the dependencies required by the project and can start using it. In this section we will use Docker.

To get started, install Docker if you don’t have it already. You can find more information on installing Docker here: https://docs.docker.com/manuals/.

If this is done, you can get the image executing the following commands on your console:

```
docker pull scrapinghub/splash 

docker run -p 5023:5023 -p 8050:8050 -p 8051:8051 scrapinghub/splash
```

Note On some machines, administrator rights are required to start Splash. For example, on my Windows 10 computer, I had to run the docker container from an administrator console. On Unix-like machines, you may need to run the container using sudo.

Now Splash is running on localhost:8050, and it should look something like Figure 5-3.

Figure 5-3. Splash welcome screen

Now you can enter a URL at the top right corner and hit Render me! to get the website rendered. If you input http://sainsburys.co.uk you get a similar result to the one shown in Figure 5-4 (the image will vary).

Figure 5-4. Splash rendered Sainsbury’s

As you can see, you get a screenshot from the page you are scraping, and below it some statistics and timing of the requests rendering the website involved. At the bottom of the page you see the source code of the website, as shown in Figure 5-5.

Figure 5-5. Splash with sources

This source code is the one you get after the page is rendered. To verify this, you can open an interactive Python shell and get the website using requests.

```
>>> import requests

>>> r = requests.get('http://sainsburys.co.uk')

>>> r.text 
>>> 
>>> '<!DOCTYPE html><html class="no-js" lang="en"><head><meta charset="utf-8"><title>Sainsbury\'s</title><meta name="description" content="Shop online at Sainsbury\'s for everything from groceries and clothing to homewares, electricals and more. We also offer a great range of financial services. Live well for less."><meta name="viewport"

content="width=device-width,initial-scale=1"><meta name="google-site-verification" content="soOzMsGig7xqxpwJQWd8qJ kfOQQvL0j-ZS9fI9eSDiE"><link rel="shortcut icon" href="favicon.

ico"><meta http-equiv="X-UA-Compatible" content="IE=edge,

chrome=IE8"><script type="text/javascript" src="//service. maxymiser.net/cdn/sainsburyscoUK/js/mmcore.js"></script> <!--[if lt IE 9]>\n <script src="https://cdn.polyfill.io/ v1/polyfill.min.js"></script>\n <link rel="stylesheet" href="homepage/css/main_ie8.css?v=65f0de0508c75d5aac750158 0ddf4e0a">\n <![endif]--><!--[if gte IE 9]>\n <link rel="stylesheet" href="homepage/css/main.css?v=2fadbf3f7bf0aa 1b5e3613ec61ebabf7">\n <![endif]--><link rel="stylesheet" href="homepage/css/main.css?v=2fadbf3f7bf0aa1b5e3613ec61eba bf7"><!--[if !IE]><!--><!--<![endif]--></head><body><script type="text/javascript">(function(a,b,c,d) ....
```

The preceding example result is just an excerpt. If you save this code into an HTML file and open it in a browser and do the same with the sources returned by Splash, you will see the same page. The difference is in the sources: Splash has more lines and contains expanded JavaScript functions.

### 2. A Dynamic Example

To see how to get Splash working with dynamic websites (which utilize JavaScript a lot), let’s see a different example. For instance, http://www. protopage.com/ generates you a web page based on a prototype, which you can customize. If you visit the site, you must wait some seconds until the page gets rendered.

If we want to scrape data from this site (there’s not much available either, but imagine it has a lot to offer) and we use a simple tool (the requests library, Scrapy) or Splash with the default settings, we only get the base page that tells us that the page is currently rendered.

To have the rendered site rendered with Splash, I altered the script (which is written in Lua by the way) and turned up the wait time to three seconds.

```
function main(splash, args) 
    assert(splash:go(args.url)) 
    assert(splash:wait(3)) 
    return { 
        html = splash:html(), 
        png = splash:png(), 
        har = splash:har(), 
    } 
end
```

Depending on the network speed and load on the target website, three seconds can be too short. Feel free to experiment with different values for your target websites to have the page rendered. Now all this is good, but how to use Splash to scrape websites?

### 3. Integration with Scrapy

The recommended way by Splash developers is to integrate this tool with Scrapy, and because we use Scrapy as our scraping tool, we will take a thorough look at how it can be accomplished.

First, we need to install the Splash Python package using pip.

    pip install scrapy-splash

Now that this library is installed, we need to enable the middlewares that have been delivered with scrapy-splash.

```
DOWNLOADER_MIDDLEWARES = { 
'scrapy_splash.SplashCookiesMiddleware': 720, 
'scrapy_splash.SplashMiddleware': 725, 
'scrapy.downloadermiddlewares.httpcompression.Http CompressionMiddleware': 810, }
```

The prceding numbers are not fully empiric: the Splash middlewares must have a higher order than the HttpProxyMiddleware, which has a default value of 750. To be on the safe side (for example Scrapy changes the default value of this proxy middleware), we could alter the middleware configuration like this:

```
DOWNLOADER_MIDDLEWARES = { 
'scrapy_splash.SplashCookiesMiddleware': 720, 
'scrapy_splash.SplashMiddleware': 725, 
'scrapy.downloadermiddlewares.httpproxy.HttpProxyMiddleware': 750, 
'scrapy.downloadermiddlewares.httpcompression. HttpCompressionMiddleware': 810, }
```

Then we must add the spider middleware to save disk space and network traffic. This is optional; if you don’t do this, duplicate Splash arguments are stored on your disk and sent to your Splash server (this will be interesting in the Cloud — see next chapter for more on that topic).

```
SPIDER_MIDDLEWARES = { 'scrapy_splash.SplashDeduplicateArgsMiddleware': 100, }
```

Now we can define some variables required for Splash to work. One of these is the SPLASH_URL, which (obviously) tells the middleware where your Splash instance is available for rendering.

    SPLASH_URL = 'http://localhost:8050/'

The next two variables come because Scrapy doesn’t provide a way to override request fingerprints, and this makes routing those requests and responses between your script and Splash a bit complicated. However, the developers of Splash came up with a solution and you can use their configuration.

```
DUPEFILTER_CLASS = 'scrapy_splash.SplashAwareDupeFilter' 
HTTPCACHE_STORAGE = 'scrapy_splash.SplashAwareFSCacheStorage'
```

The second variable points to a cache storage solution, which is aware of Splash. If you’re using another custom cache storage, you must adapt it to work with Splash. This requires you to subclass the aforementioned storage class and replace all calls to scrapy.util.request.request_ fingerprint with scrapy_splash.splash_request_fingerprint to have those nasty changed fingerprints work out.

The last change we must adapt is the usage of Requests: instead of using the default Scrapy Request we need to use SplashRequest.

Now let’s adapt the Sainsbury’s spider to use Splash.

### 4. Adapting the basic Spider

In an ideal world, you would only need to alter the configuration as we did in the previous section, and all requests and responses would go over Splash because we don’t have any usages of Scrapy’s Request objects.

Unfortunately, we need some more configuration in the code of the scraper too. If you don’t believe me, just start the scraper without having Splash running.

To get our scraper running through Splash, we need to adapt every request call to use a SplashRequest, and every time we initiate a new request (either when starting the scraper or yield-ing some response. follow calls).

To get the first start right, we can add the following function to our script:

```
from scrapy_splash import SplashRequest

def start_requests(self):
    for url in self.start_urls:
        yield SplashRequest(url, callback=self.parse)
```

This is the bare minimum to get the spider operating through Splash. The parameters speak for themselves: URL is the target URL, and callback defines the method to use. There are some options to configure how Splash should behave, for example, waiting some time to get the website rendered. Say, if we want to wait one second for loading the page, we can alter the calls of SplashRequests like this:

```
yield SplashRequest(url, callback=self.parse, args={'wait':1.0})
```

So, we’re good and we render the first page through Splash, but what about the other calls like navigating to the detail pages or the next page?

To adapt these, I changed the XPath extraction code a bit. Until now, we used the response.follow approach where we could provide the selector containing the potential next URL we want to scrape.

Using Splash, we need to extract these URLs and provide them as parameters to the SplashRequest constructor. I’ll use the parse method as an example. It looked like this at the end of Chapter 4:

```
def parse(self, response):
    urls = response.xpath('//ul[@class="categories departments"]/li/a')
    for url in urls:
        yield response.follow(url, callback=self.parse_ department_pages) 
```

Now it looks like this:

```    
    def parse(self, response):
        urls = response.xpath('//ul[@class="categories departments"]/li/a/@href').extract()
    for url in urls:
        if url.startswith('http'):
            yield SplashRequest(url, callback=self.parse_ department_pages)
```

I added the filter for url.startswith('http') to avoid potential errors that may happen if the url doesn’t contain an absolute URL. In some cases, you need to join the URL together with the base URL of the response to get the target domain (because url is a relative URL to the domain). Following is an example again with the parse method.

```
def parse(self, response):
    urls = response.xpath('//ul[@class="categories departments"]/li/a/@href').extract()
for url in urls:
    yield SplashRequest(response.urljoin(url), callback=self.parse_department_pages)
```

One change I made besides the ones mentioned previously was to rename the spider to splash.

Running the scraper stays the same.

scrapy crawl splash -o splashburys.jl

After the scraper finishes, you will find records similar to the following excerpt in the splashburys.jl file.

```
{"url": "https://www.sainsburys.co.uk/shop/ProductDisplay ?storeId=10151&productId=1153156&urlRequestType=Base&cate goryId=312365&catalogId=10216&langId=44", "product_name": "Sainsbury's Venison Steak, Taste the Difference 250g", "product_image": "https://www.sainsburys.co.uk/wcsstore7.25.53/ ExtendedSitesCatalogAssetStore/images/catalog/productImages /90/0000001442090/0000001442090_L.jpeg", "price_per_unit": "£7.50", "rating": "3.0", "product_reviews": "2", "item_code": "6450995", "nutritions": {"Energy ": "583kJ/", "Fat ": "2.6g", "of which saturates ": "0.9g", "mono-unsaturates ": "1.0g", "polyunsaturates ": "0.6g", "Carbohydrate ": "<0.5g", "of which sugars ": "<0.5g", "Fibre ": "<0.5g", "Protein ": "28.2g", "Sodium ": "0.05g", "Salt ": "0.13g"}, "product_origin": ""} {"url": "https://www.sainsburys.co.uk/shop/gb/groceries/ special-offers-314361-44/sainsburys-salmon-with-lemon-butter-taste-the-difference-145g", "product_name": "Sainsbury's Lightly Smoked Salmon with Wild Garlic Butter, Taste the Difference 145g", "product_image": "https://www.sainsburys. co.uk/wcsstore7.25.53/ExtendedSitesCatalogAssetStore/images/ catalog/productImages/27/0000000301527/0000000301527_L.jpeg", "price_per_unit": "£3.00", "rating": "2.3333", "product_ reviews": "3", "item_code": "7880107", "nutritions": {"Energy": "990kJ", "Energy kcal": "238kcal", "Fat": "16.9g", "Saturates": "4.6g", "Mono-unsaturates": "7.5g", "Polyunsaturates": "3.8g", "Carbohydrate": "1.6g", "Sugars": "1.2g", "Fibre": "0.6g", "Protein": "19.6g", "Salt": "0.63g"}, "product_origin": "Packed in United Kingdom Farmed in Scotland Produced from Farmed Scottish ( UK) Atlantic Salmon ( Salmo salar)"}
```

And that is it: we converted the Sainsbury’s scraper to use Splash.

### 5. What Happens When Splash Isn’t Running?

Good question, but I bet you already have the answer. The scraper won’t do anything, and exits with an error message containing the following valuable information to identify this particular error cause.

```
2018-04-27 16:07:19 [scrapy.core.scraper] 
ERROR: Error downloading <GET https://www.sainsburys.co.uk/shop/gb/ groceries/meat-fish/ via http://localhost:8050/render.html>: Connection was refused by other side: 10061:
```

### Summary

Splash is a nice Python-based website rendering tool that you can integrate easily with Scrapy.

One drawback is that you must install it manually through a somewhat complicated process or using Docker. This makes porting it to the cloud complicated (see Chapter 6 for Cloud solutions), therefore you should use Splash only for a local scraper. However, locally it can give you a great benefit with its seamless integration with Scrapy for scraping websites using JavaScript to render content dynamically.

Another drawback is the speed. When I used Splash on my local computer, it barely scraped 20 pages per minute. This is too slow for my taste, but sometimes I cannot get around it.

## 03. Selenium

If you search the Internet about website scraping, you will most often encounter articles and questions about Selenium. Originally, I wanted to leave Selenium out of this book because I don’t like its approach; it’s a bit clumsy for my taste. However, because of its popularity, I decided to add a section about this tool. Perhaps you will embed a Selenium-based solution to your Scrapy scripts (for example you already have a Selenium-scraper but want to extend it), and I want to help you with this task.

First we will look at Selenium and how to use it in a stand-alone fashion, then we will add it to a Scrapy spider.

### 1. Prerequisites

To have Selenium working on your computer, you must install it like most Python libraries through the Python Package Index.

    pip install selenium

To use Selenium for website scraping, you will need a web browser. This means you will see the configured web browser (let’s say Firefox or Chrome) open up, load the website, and then Selenium does its work and extracts the script you defined.

To enable linking between Selenium and your browser, you must install a specific WebDriver.

For Chrome, visit [ChromeDriver - WebDriver for Chrome](https://sites.google.com/a/chromium.org/chromedriver/home). 

I downloaded version 2.38.

For Firefox, you need to install GeckoDriver. It can be found at GitHub. I downloaded version 0.20.1.

These drivers must be on the PATH when you’re running your Python script. I put all of them inside a folder, because in this case I have to add only this one folder and all my web drivers are available.

Note that these web drivers require a specific browser version. For example, if you already have Chrome installed and download the latest version of the web driver, you may encounter an exception like the one following if you miss updating your browser:

raise exception_class(message, screen, stacktrace) selenium.common.exceptions.SessionNotCreatedException: Message: session not created exception: Chrome version must be >= 65.0.3325.0

(Driver info: chromedriver=2.38.552522 (437e6fbedfa 8762dec75e2c5b3ddb86763dc9dcb),platform=Windows NT 10.0.16299 x86_64)

### 2. Basic Usage

Now to verify if everything is working fine, let’s write a simple script to open the Sainsbury’s website for us using Selenium.

```
from selenium.webdriver import Chrome, Firefox

chrome = Chrome() 
firefox = Firefox()
chrome.open()   # this opens a Chrome window 
firefox.open()  # this opens a Firefox window

# navigates to the target website in Chrome 
chrome.get('https://sainsburys.co.uk') 

# navigates to the target website in Firefox
firefox.get('https://sainsburys.co.uk') 

```

OK, it’s nice to have the browser open automatically and navigate to the target website. But what about scraping information? Because we have a website in our reach (in the browser), we can parse the HTML — almost like we did in the previous chapters or use Selenium’s offering for data extraction from the HTML of the web page.

I won’t go into detail on Selenium’s extractors because it would exceed the boundaries of this book, but let me tell you that by using Selenium you have access to a different set of extraction functions, which you can use on your browser instances.

### 3. Integration with Scrapy

Selenium can be integrated with Scrapy. The only thing you need is to configure Selenium properly (have the web drivers on the PATH and the browsers installed) and then the fun can begin.

What I like to do is to disable the browser window for my scrapes. That’s because I get distracted every time I see a browser window if it navigates the pages automatically, and it would go crazy if you combine Scrapy with Selenium.

Besides this, you will need a middleware that will intercept calls prior to sending them directly through Scrapy and will use Selenium instead of normal requests.

A rudimentary middleware would look like this one:

```
# -*- coding: utf-8 -*-

from scrapy import signals
from scrapy.http import HtmlResponse
from scrapy.utils.python import to_bytes
from selenium import webdriver
from selenium.webdriver.firefox.options import Options

class SeleniumDownloaderMiddleware:

    def __init__(self):
        self.driver = None

    @classmethod
    def from_crawler(cls, crawler):
        middleware = cls()
        crawler.signals.connect(middleware.spider_opened, signals.spider_opened)
        crawler.signals.connect(middleware.spider_closed, signals.spider_closed)
        return middleware

    def process_request(self, request, spider):
        self.driver.get(request.url)
        body = to_bytes(self.driver.page_source)
        return HtmlResponse(self.driver.current_url, body=body, encoding='utf-8', request=request)

    def spider_opened(self, spider):
        options = Options()
        options.set_headless()
        self.driver = webdriver.Firefox(options=options)

    def spider_closed(self, spider):
        if self.driver:
            self.driver.close()
            self.driver.quit()
            self.driver = None
```

The preceding code uses Firefox as the default browser and starts it in headless mode when the spider is opened. When the spider closes, the web driver is closed too.

The interesting part is when the request happens: it is intercepted and routed through the browser and the response HTML code is wrapped into an HtmlResponse object. Now your spider gets the Selenium-loaded HTML code and you can use it for scraping.

#### scrapy-selenium

Recently, I have found a fresh project at GitHub called scrapy-selenium. 2 It is a convenient project to have you install and use it to combine the powers of Scrapy and Selenium. I think it is worth sharing this project with you.

Note Because this project is a private one, it may have issues. If you find something not working, feel free to raise an issue for this project and the developer will help you out to fix that problem. If not, shoot me an email and I’ll see if I can give you a solution or perhaps maintain the application myself and deliver newer versions.

This project works just like the custom middleware we implemented in the previous section: it intercepts requests and downloads the pages using Selenium.

Let’s start with the configuration.

```
from shutil import which

SELENIUM_DRIVER_NAME = 'firefox' 
SELENIUM_DRIVER_EXECUTABLE_PATH = which('geckodriver') 
SELENIUM_DRIVER_ARGUMENTS = ['-headless']
```

Alternatively, you can use Chrome instead of Firefox, but in this case take care of the --headless argument: it requires two dashes.

```
from shutil import which

SELENIUM_DRIVER_NAME = 'firefox'
SELENIUM_DRIVER_EXECUTABLE_PATH = which('geckodriver')
SELENIUM_DRIVER_ARGUMENTS = ['--headless']

DOWNLOADER_MIDDLEWARES = {
    'scrapy_selenium.SeleniumMiddleware': 800
}

```

For the spider, I reused the code of the Splash section but changed the used Request implementation to the scrapy-selenium one:

    from scrapy_selenium import SeleniumRequest

and I had to adapt the constructor calls to contain the URL as a named parameter.

```
def start_requests(self):
    for url in self.start_urls:
        yield SeleniumRequest(url=url, callback=self.parse)
```

Be sure you change all these calls. If you miss one, you’ll get an error like this:

```
yield SeleniumRequest(url, callback=self.parse) File "c:\dev\__py_venv\scrapy\lib\site-packages\scrapy_ selenium\http.py", line 29, in __init__ super().__init__(*args, **kwargs) TypeError: __init__() missing 1 required positional argument: 'url'
```

2 [clemfromspace/scrapy-selenium: Scrapy middleware to handle javascript pages using selenium](https://github.com/clemfromspace/scrapy-selenium)

### Summary

Selenium is an alternative tool that website scraper developers use because it supports JavaScript rendering through a browser. We saw some solutions on how to integrate Selenium with Scrapy but skipped the built-in methods to extract information.

Again, using an external tool like Selenium makes your scraping slower, even in headless mode.

## 04. Solutions for Beautiful Soup

Until now, we looked at solutions where we can integrate JavaScript-based website scraping with Scrapy. But some projects are fine using Beautiful Soup and don’t need a full scraper environment.

### 1. Splash

Splash offers manual usage too. This means, you have an alternative option to get Splash to render a website and return the source code back to your code. And we can utilize this to have a simple scraper written with Beautiful Soup.

The idea here is to send an HTTP request to Splash, providing the URL to render (and any configuration parameters) and get the result back, and then use Beautiful Soup on this result, which is a rendered HTML.

To stick with the previous example, we will convert the scraper form Chapter 3 into a tool that utilizes Splash to render the pages of Sainsbury’s.

The idea here is to simply call Splash’s HTTP API to render the web page instead of getting the page through the requests library. This means our only change will be in the get_page function, where we forward the URL we want to scrape to Splash.

```
def get_page(url):
    try:
        r = requests.get('http://localhost:8050/render. html?url=' + url) 
        if r.status_code == 200:
            return BeautifulSoup(r.content, bs_parser) 
    except Exception as e:
        pass 
    return None
```

As you can see, we call the render.html endpoint of our Splash installation and provide the target URL as a simple GET parameter.

If you’re more into POST requests, you can change the prceding function to look like this:

```
def get_page(url):

    try:
        r = requests.post('http://localhost:8050/render.html', data='{'url': '+ url + '}')
        if r.status_code == 200:
            return BeautifulSoup(r.content, bs_parser) 
    except Exception as e:
        pass 
    return None
```

### 2. Selenium

Of course, we can integrate Selenium to our Beautiful Soup solutions too. It works the same way as it did with Scrapy.

Again, I won’t use the built-in Selenium methods to extract information from the website. I use Selenium only to render the page and extract the information I require.

To do this, I’ll add two helper functions to the scraper, which initialize and tear down Selenium at the required places.

```
def initialize():
    global selenium 
    if not selenium:
        selenium = Firefox()

def tear_down():
    global selenium 
    if selenium:
        selenium.quit()
        selenium = None
```

To be on the safe side, I’ll add a call to initialize() every time we want to download a page; however, I’ll call tear_down() only when the script finishes.

```
def get_page(url):
    initialize()
    try:
        selenium.get(url) 
        return BeautifulSoup(selenium.page_source, bs_parser) 
    except Exception as e:
        pass 
    return None
```

### Summary

Even though we focus on Scrapy, because in my opinion it’s currently the website scraping tool for Python, you can see that options that make Scrapy handle JavaScript can be added to “plain” Beautiful Soup scrapers. And this gives you options to stay with the tools you already know!

## Summary

In this chapter we looked at some approaches to scrape websites that utilize JavaScript. We looked at the mainstream Selenium using a web browser to execute JavaScript and then went to the headless world, where you don’t need any window to execute JavaScript and this makes your scripts portable and easier to execute.

Naturally, using another tool to get some extra rendering done takes time and provides overhead. If you don’t require JavaScript rendering, create your scripts without any add-ons like Splash or Selenium. You’ll benefit from the speed gain.

Now we are ready to see how we can deploy our spiders to the Cloud!