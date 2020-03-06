# 2020061Website-Scraping-with-PythonR02

Copyright © 2018

## 记忆时间

2020-03-08/

## 04. Using Scrapy

### 1. 逻辑脉络

如何用 scrapy 框架抓取一个没有 JS 的静态网页里指定的元素。

### 2. 摘录及评论

In this chapter you learned about Scrapy, the tool for website scraping. You implemented the scraper for the requirements of Chapter 2 with Scrapy. You have seen that you need to write much less than when you use a homemade spider where you have to handle requests — just to mention one example. You learned some advanced topics too like writing your own middleware, pipelines, and extensions, and what the result is if you turn some knobs on the configuration panel.

Now you are a full-fledged website scraper. You have the tools with which you can complete 75% of all scraping jobs. Feel free to stop reading here, but keep in mind that these 75% are decreasing with the emerging number of JavaScript-heavy websites that render data dynamically. The next chapter will cover an advanced topic I rarely use: handling web pages with JavaScript. There are different approaches, and we will go a bit deeper because I will show you options other than Selenium. If you are interested in the “Why?,” keep on reading!

In my opinion, this is the only viable tool available currently for Python, which can handle complex scraping tasks out of the box. You can cache web pages, and add parallelism as you wish; you only need to configure Scrapy properly and write the extraction code.

In this chapter you will learn how to get the most out of Scrapy for the majority of your website scraping projects. You will write the Sainsbury’s extractor, configure Scrapy to create a website-friendly spider, and you will learn how to apply custom exporting options to the extracted information. As opposed to the previous chapter, where I introduced Beautiful Soup at the beginning and you created the project to scrape the Sainsbury’s website afterward, now you will learn the basics of Scrapy through implementing the project scraper. Toward the end of this chapter I’ll add more information and insights into the tools that we didn’t use for the project, but I think it is useful to know if you write your own scrapers in the future.

Note The developers of Scrapy recommend installing the tool into a virtual environment. This is a good practice to have a clean version of your scraping tool; and this hinders you from updating a dependency of Scrapy to a noncompatible version, which will render your scraper nonworking.

Configuring the Project. Before you dive into the code of the main scraper you will implement with Scrapy, you should configure your project properly. Basic configuration is required to show you are a “good citizen,” and your spider is a well-raised tool too. The basic configuration I suggest you do every time is to add the user agent and see that the robots.txt file is honored.

Fortunately, the basic project skeleton of Scrapy comes with a configuration file where most of the settings are set properly or are commented out but tell you about the option and which values it accepts. You can find the configuration of the project in the settings.py file. If you take a look at it, you will see a lot of options added; most of them are commented out. The default values work perfectly fine for most scraping projects, but you can tune them if you think it gives you better performance or you need some more complexity added. The two properties I always use are: USER_AGENT and ROBOTSTXT_OBEY.

The names of these properties already tell you what they are good for. For the USER_AGENT, you see a default that consists of the bot’s name (sainsburys) and an example domain. I change it mostly to a Chrome agent. You can obtain one through the DevTools of Chrome: you open the Network tab, load a web page normally in your browser, click on the request in the Network tab, and copy the value of User Agent in the Headers tab of the request. This works even if you are offline.

1『这是目前知道的第二种获取客户端信息的办法，第一种是直接在 Chrome 里输入「http://httpbin.org/get?a=123&b=456」即可获得相关信息。User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.100 Safari/537.36。』

And to be a good citizen, leave the ROBOTSTXT_OBEY on True. With this, Scrapy takes care of handling the contents of the robots.txt file if one is present. I suggest you delete all commented-out settings. This will help you in reading the file later and you see all active configuration at once; you do not have to scroll through all the lines to see which is commented out. it is hard even in an iDe with good color coding.

Besides these properties, I suggest you add CONCURRENT_REQUESTS = 1. This reduces the speed of the spider, but while testing, you will run the code quite a lot and you don’t want to get banned from the website right at the beginning — or you don’t want the website’s servers to be done just because you (and 99,999 other readers) run the scraper simultaneously and the servers cannot handle the load. If you look at the commented code, you’ll find that the default value for this is 16. I’ll add a section where I will turn up the number of parallel requests and will do a flawed microbenchmark. To summarize: my final settings.py file looks like this. Now that the basic configuration is done, we can implement the spider that will do the work for us.

2『采纳了作者的意见，CONCURRENT_REQUESTS = 1。』

Terminology. While setting the configuration, you have had the option to learn some of Scrapy’s terminology, like middleweare or pipeline. They are the building blocks of this scraper, where you can implement your own code and extend the functionality if it is missing something you need.

Middleware. Middlewares are hooks into Scrapy; this means, you can extend the already available functionality. There are two types of middlewares in Scrapy: 1) Downloader middlewares. 2) Spider middlewares.

As their names already suggest, you can either extend the downloader (add your own cache, proxy the calls, modify requests prior sending, or ignore requests, just as a few examples), or the parser functionality (filter out some responses, handle spider exceptions, call different functions based on the response, etc.).

For basic scraping there’s no need to write your own middlewares, because you can get along well with the tools available — and as Scrapy is evolving, more custom code gets into the standard library. Middlewares need to be activated in the settings.py file.

```
DOWNLOADER_MIDDLEWARES = { 'yourproject.middlewares.CustomDownloader': 500 }
SPIDER_MIDDLEWARES = { 'yourproject.middlewares.SpiderMiddleware': 211 }
```

If you have your middlewares but they don’t seem to work, you might have forgotten to activate them. Another reason could be that they are executed at the wrong position: the number you provide as the value in the dictionary tells Scrapy about the order in which the middleware should be executed: 1) For downloader middlewares, the process_request method is called in increasing order. 2) For downloader middlewares, the process_response method is called in decreasing order. 3) For spider middlewares, the process_spider_input method is called in increasing order. 4) For spider middlewares, the process_spider_output method is called in decreasing order. Therefore, it can happen that you expect something in the request / response / input / output, but it was handled by a middleware with a lower / higher priority.

Pipeline. Pipelines handle the extracted data. This involves cleaning, formatting, and sometimes exporting the data. Even though Scrapy has built-in pipelines that export your data in a given format (CSV, JSON — more on these later in this chapter), sometimes you need to write your own pipeline to configure the result to meet your (your customers’) expectations. You will write more pipelines than middlewares while you’re working as a pro scraper. Nevertheless, it is not as bad as it might sound. In this chapter we will create a simple item pipeline to show you how it is done. Similar to middlewares, you have to activate your pipelines in the settings.py file.

    ITEM_PIPELINES = { 'yourproject.pipelines.MongoPipeline': 418 }

Extension. Extensions are singleton classes that get instantiated once at startup and contain custom code, which you can use to add some custom functionality that is not related to downloading or scraping like a middleware does. Such extensions can be used for logging, or monitoring memory consumption (these are already built-in extensions). Extensions can be loaded the same way as middlewares and pipelines in settings.py.

    EXTENSIONS = { 'scrapy.extensions.memusage.CoreStats': 500 }


2『经验证，这些配置都先别设，否者抓取不了数据，目前也不清楚问题出在哪里。』

Selectors. This is the most important term you will encounter while using Scrapy. Selectors are the code parts that select certain parts of the HTML. As you can see, selectors work similar to Beautiful Soup and lxml but they are the Scrapy version, and you can use XPath or CSS expressions. I prefer XPath expressions because I worked for years with XML and XML transformations. Selectors are objects in Scrapy, and because of this they can be constructed from a text.

```
from scrapy.selector import Selector

selector = Selector(text='<html><body><h1>Hello Selectors!</h1> </body></html>') 
print(selector.xpath('//h1/text()').extract()) 
# ['Hello Selectors!']
```

or from a response:

```
from scrapy.selector import Selector 

from scrapy.http import HtmlResponse

response = HtmlResponse(url='http://my.domain.com', body='<html><body><h1>Hello Selectors!</h1></body></html>', encoding='UTF-8') 
print(Selector(response=response).css('h1::text').extract()) 
# ['Hello Selectors!']
```

However, because selectors are the way to extract data, you can conveniently access them from your response using [response.xpath()] or [response.css()]. And this makes Scrapy a great tool in my opinion: you don’t have to bother creating selector objects, but use the available convenient method accesses. Follow the links if you want to read more about CSS selectors 2 or XPath expressions.3 

[Selectors Level 4](https://www.w3.org/TR/selectors/)

[xpath cover page - W3C](https://www.w3.org/TR/xpath/all/)

Implementing the Sainsbury Scraper. To start working on the extraction code, you will need a spider generated. As you have seen in the previous section, where you created and configured the base of the project, you can do it with the genspider command. Let’s do it right now. First change the directory to the one where you generated your bot, and then execute the following command:

    scrapy genspider sainsburys 'https://www.sainsburys.co.uk/shop/gb/groceries/meat-fish/'

When executing the preceding command, you get a strange message: Cannot create a spider with the same name as your project. Well, if we cannot get a spider with the same name, let’s give it a different name. My suggestion is a name that is easy to remember for you. I use mostly "basic" because it’s easy to write and I have a basic scraper to do the extraction for me. The project already has a unique name; and with basic I can always start my spiders, regardless of the project.

    scrapy genspider basic www.sainsburys.co.uk/shop/gb/groceries/meat-fish

The response now is different. Created spider 'basic' using template 'basic' in module: sainsburys.spiders.basic

With this command, Scrapy added a basic.py file to the project’s spiders folder. This file will be the base of your spider; here will you implement the extraction code. 

What’s This allowed_domains About? If you looked at the code thoroughly, you have seen there’s a list of allowed domains. This list is used to give the spider a bound. Without setting the allowed domains, you could write a script that goes through the Internet (following every link on the pages it scrapes). For most purposes, you want to keep your scraping in one domain. However, sometimes you have to deal with internal or subdomains. In those cases, you can extend this list manually to fix such “issues.” And here you should set the domain only. When you generated the spider, it added the whole URL to this list, but you need something like this. you can find the source code for an empty project with my default configuration among the sources for this chapter in the folder 01_empty_project.

    allowed_domains = ['www.sainsburys.co.uk']

Preparation. This section is brief. If you followed along, you have everything configured and there is no need for any other preparation. Just a quick checklist to see if you are ready to go: 1) You’ve read the requirements of Chapter 2. 2) You’ve created a Scrapy-project. 3) You’ve configured the project as described in this chapter. 4) You’ve created a spider.

Using the Shell. One function of Scrapy I like to utilize for preparation work is to use its shell, which gives us an environment to test and prepare code snippets for extraction. And because the shell behaves just like your spider code will, it is ideal for creating the building blocks of your application.

With a naive approach (or similar, like we did in the previous chapter), you’d write a part of your code and run the spider. If there’s an error, you’d fix the code and rerun the spider. This is OK if the website doesn’t limit access based on requests. If there’s a limit, you may end up exceeding it and your spider (and your computer, current IP, whole company network4 ) is banned from the website. And, as I have seen, Sainsbury’s runs behind CloudFlare — you better not send parallel requests to their website!

The Scrapy shell works differently: it downloads your target web page and you can create your extraction logic on this copy. If you need to move to another page, you let the shell download it and you are good to write the next chunk of code. Starting the shell is easy.

scrapy shell. You can pass along a \<url> parameter, which is your target URL. For this book we will use https://www.sainsburys.co.uk/shop/gb/groceries/meat-fish/:

    scrapy shell https://www.sainsburys.co.uk/shop/gb/groceries/meat-fish/

Alternatively, you can also fetch the URL when you open Scrapy’s shell without any, or with a different URL.

    >>> fetch('https://www.sainsburys.co.uk/shop/gb/groceries/meat-fish/')

Now the shell has downloaded the web page behind the URL. This means two things: now you have access to the Meat & Fish page’s content and can try your extractors; and second, you have to download every page you want to use in the shell. Even though the second point sounds bad, it is not: getting other pages is made easy in Scrapy and therefore in the shell too. In the shell you have access to a response object (just like in the parse method, which we will write later in this chapter), and with this response you can use the available selectors.

I don’t want to dig very deep into how to use the shell to prepare your scraper script. Therefore, we will do one example: we get the URLs to the next page. This will give you a good start and the feel of using the shell for further preparation.

As you may remember, the links that lead to the detailed pages can be found in an unordered list (\<ul class="categories departments">). The list’s elements (\<li>) have an anchor child (\<a>), and the value of the href attribute of these anchors is the URL we are looking for. To get the list of these URLs, you can write the following code using XPath:

    urls = response.xpath('//ul[@class="categories departments"]/li/a/@href').extract()

Using CSS selectors, this would look like this:

    urls = response.css('ul.categories.departments > li > a::attr(href)').extract()

And that is it. You have all the URLs that lead to either product listings of the category or to a site containing more subcategories, just like in the previous chapter. I suggest you dig a bit deeper into XPath and CSS selectors for now, to understand the extractor code that you will write starting with the next section.

1『找「翻页」的方法。』

def parse(self, response). Now we are good to go to write the code in the basic.py file. The parse method is the core of every spider. This method is called every time Scrapy downloads a URL, and most of the time you write your extraction code in this method. The response argument holds the response from calling the URL. It can contain the website’s content but sometimes you can get back error codes, for example, when the website is down or nonexistent.

You can write a whole scraper into the parse method, but I suggest organizing your code into methods (and actually, this is the suggested practice of many developers). This helps you in the future to understand what the code wants to achieve. Therefore, the parse function will be very sparse: it extracts only the URLs to the category pages (the same from the preparation with the shell), and initiates the download and parsing of those pages.

1『parse() 方法的说明，This method is called every time Scrapy downloads a URL.』

```
from scrapy import Request

# some code left out...

def parse(self, response):
    urls = response.xpath('//ul[@class="categories departments"]/li/a/@href').extract()
    for url in urls:
        yield Request(url, callback=self.parse_department_ pages)
```

The preceding code extracts the href attributes of every anchor element of the list of the desired class. The interesting part is how the scraping is continued: you yield a new Request object with the target URL as the first parameter and the callback function that should be called if the server returns an OK-ish response for the given URL. In this case it will be the parse_department_pages method of this same class. There’s an alternative way to get to the next page with writing less code.

```
def parse(self, response):

    urls = response.xpath('//ul[@class="categories departments"]/li/a')
    for url in urls:
        yield response.follow(url, callback=self.parse_ department_pages)
```

Here we use the syntactic sugar of Scrapy: under the hood the same code is executed, but you don’t have to bother with extracting the exact reference from the anchor tags. And sometimes you don’t get a fully qualified (absolute) URL in web page links but relative references, and you have to manually add the host (or use urljoin). By using response.follow you get this out of the box too. Therefore, I suggest you use this syntax, and I’ll use this in the book too!

1『建议用语法糖，response.follow(url, callback=self.parse_ department_pages)，当要使用相对文件地址时其优势就体现出来了；\<a> 指锚标签元素（anchor tags）。』

Currently, as of version 1.4.0, you have to provide a single URL or Linktype object to the follow method. I bet that someone will add a method that accepts a list (for example follow_all) too, because we like make things easier. With this, we are done with this section. Let’s move on and see how to get to the product pages. At the end of this section, your basic.py file should look like this:

2『

有几个正则规则要机会弄明白，作者每个源码里都有。

```
import re

# what is the meaning?
reviews_pattern = re.compile("Reviews \((\d+)\)")
item_code_pattern = re.compile("Item code: (\d+)"
```

』

Navigating Through Categories. Your first task is to navigate through the category pages of the Sainsbury’s website. You have seen in the previous chapter how complex it can get to find the page where the item details are. As you have seen in the previous chapter, each category’s link can lead either to the product listing or to a page containing subcategories and their links, which can lead to either the product listing page or a third page with sub-subcategories. Fortunately, there is no deeper layering.

In this section we will handle the case wherin your code in the previous section resulted in a sub- or sub-subcategory page and not the product detail. We sent requests with Scrapy in the previous section and told the tool to handle the responses with the parse_department_pages method. To implement this method, we have to take care of the three versions of the response: 1) We get a product listing page. 2) We get a sub-category page. 3) We get a sub-sub-category page.

If the response is a product listing, the idea is to forward the response to the next section’s method. However, we must take care of triggering the requests. The resulting block will look like this one:

```
product_grid = response.xpath('//ul[@class="productLister gridView"]')
if product_grid:
    for product in self.handle_product_listings(response):
        yield product
```

In the preceding code, we call the handle_product_listings method with the response object. We could provide the product grid too (or just the grid) because we have it already extracted but, as you will see later, we need the response to navigate between the pages of the product grid. Then we yield the result, which is the trigger for Scrapy to scrape these URLs too.

The next step is to get through the deeper layers of categories, which are represented by CSS classes like aisles (class="category aisles") and shelves (class="category shelves") — just like in your supermarket. The trick here is to check if the page’s source contains shelves and if not, then go for aisles. This is because a page containing shelves contains aisles too, and if you get the aisles links first you can end up in a neverending circle of getting the same pages over and over again if you don’t use caching. And getting the same pages means slower scraping (actually, never ending) and a lot of duplicate items in your scraping result.

```
pages = response.xpath('//ul[@class="categories shelf"]/li/a') 
if not pages:
    pages = response.xpath('//ul[@class="categories aisles"] /li/a') 
if not pages:
# here is something fishy 
    return
for url in pages:
    yield response.follow(url, callback=self.parse_department_ pages)
```

The preceding code follows the approach mentioned previously: it looks for shelves and if they are not found, it looks for aisles. If nothing is found, then we are at a page from which we cannot gather more information: we have extracted the links to the product listings or there are no links to aisles or shelves on the page. At the end of this section, your basic.py file should look something like this:

Navigating Through the Product Listings. Now your code leads at some point to a product listing page. In this section we will navigate through these pages if they have too many elements to display on one page, and we will request a download for the detailed item pages. We are currently in the handle_product_listings function. Let’s start with the item details.

```
urls = response.xpath('//ul[@class="productLister gridView"]//li[@class="gridItem"]//h3/a') 
for url in urls:
    yield response.follow(url, callback=self.parse_product_detail)
```

The preceding code extracts the URLs to the detailed pages, and these URLs are then returned to the parse_department_pages method where their scraping is triggered.

```
next_page = response.xpath('//ul[@class="pages"]/li [@class="next"]/a') 
if next_page:
    yield response.follow(next_page, callback=self.handle_ product_listings)
```

This code looks for the link to the next page. If one is found (on the website, it’s under the > symbol) then it is returned to the parse_ department_pages method. Note here the callback method: Because we know that we get another page of product listing, we can use the same method as a callback. After finishing this section, your basic.py file should look like this:

Extracting the Data. Now that your code can handle the complex navigation and find the item details page, it’s time to extract the required information from the website. We are currently in the parse_product_detail method. Now it is time to extract all the required information from the item page. Actually, this process is the same as you did in the previous chapter (if you coded along): you can use the queries; however, you can save some lines of code on validating every find or find_all call.

Without talking too much, let’s jump into the code. if you want, you can put down the book and implement the extraction logic. it is not hard, and you can use the information from the previous two chapters to go with. My solution looks like this (yours may differ):

And that is it. Extracting information on a product takes up to 30 lines of code (with my custom formatting settings). And this is just great! As you can see in the code, there are some interesting code blocks. For example, every xpath call returns a list, even if you know there has to be at most one result. And some of those lists are empty because the product doesn’t have ratings or unit information. As with Beautiful Soup, you must handle such cases with Scrapy too. After this section, your basic.py file should look something like this:

Where to Put the Data? OK: you have followed along, implemented the product extractor, and you have a lot of variables in your spider that contain the information for the project, but where to store them? With Scrapy, you have to store data in so-called items. These items are plain old Python classes and can be found in the items.py file. Besides this, these items behave as dictionaries: you declare them as Python classes and can fill them like dictionaries using a key-value assignment. If you have run your spider after the previous step, you might have seen entries in the console like this one:

    2018-02-11 11:06:03 [scrapy.extensions.logstats] INFO: Crawled 47 pages (at 47 pages/min), scraped 0 items (at 0 items/min)

Here you can see that there were no items scraped. We will fix this now. Let’s adapt the parse_product_detail method to put the data into an item. To do this, first of all we need an item, which is already there in the items.py file. This class is currently empty; we must add fields to it. Because I don’t like to write scrapy.Field() every time (even if it is just copy+paste), I like to do “static” imports (from scrapy import Item, Field). My solution looks like this; yours may differ, depending on how you named your fields.

As you can see, the problem with this approach will come in the code: for the nutrition table you get strings as keys and you have to map them to these field names. This makes things complicated. Besides this, there are over 70 different fields that you must map. I don’t think it useful to include such mapping code here. If you are interested, you can give it a try, but it is not a requirement of this book or website scraping in general.

1『这里作者留了一个难题待挑战。』

When we export the results to files later in this chapter, we will take a closer look at how fields containing dictionaries are exported by default and what we can do to get the same results as in Chapter 2. Now to add and use items, you have to adapt the parse_product_ detail method like this:

This involves defining the new item (add the import to the file: from sainsburys.items import SainsburysItem) and then use it like a dictionary. I used the variable names from the previous version as the Field names in my item definition, but it is up to you how to name your fields. You just must find the right mapping. Finally, you must yield the item, which makes Scrapy know there’s an item to handle. The current state of the spider can be found in the folder 02_basic_ spider among the sources of this chapter.

1『mapping 的概念很重要，很多地方看到这个概念。』

Why Items? Good question! Because items are dictionary-like objects; alternatively, you can use dictionaries to store your information. item = {} This doesn’t result in any difference in coding or handling results, although Scrapy’s items hold some extended information that some components use. For example, exporters look at which fields to export, serialization can be customized by Items metadata, and you can use them to find memory leaks. You will see later in this chapter that sometimes it is convenient to use a simple dictionary instead of an item. But for now, you should use items.

Running the Spider. Now it is time to start our spider, because we finished the extractor methods and added the items to export. To start the spider, execute:

    scrapy crawl basic

from your crawler-projects main folder (where the scrapy.cfg file is located). In my case, this is. Depending on your logging configuration, you either see something similar to this:

or a lot more information buzzing through your screen. This is because of the default logging level. If you don’t set it explicitly to INFO, you get all information Scrapy-developers thought useful. And one portion of this information is the item that was gathered. It is good to see on the console which items are processed, but for more than 3,000 entries this generates a lot of unwanted output. These first lines of the prcedimg output tell you what configuration runs Scrapy. Here you can see the middlewares, pipelines, extensions, and all the important stuff to analyze if you encounter strange results.

    2018-02-11 13:53:20 [scrapy.extensions.logstats] INFO: Crawled 220 pages (at 220 pages/min), scraped 205 items (at 205 items/min)

Over time, a new line like the preceding one pops up on the screen. This tells you the current progress: how many pages are scraped, how many items are extracted, and how fast the scraping is. These numbers vary on your settings: if you increase the concurrent requests and decrease the delay between requests, this will get faster (depending on the target website, of course). If you find such statistics annoying, you can disable them by adding the following to your spider’s settings.py:

    EXTENSIONS = { 'scrapy.extensions.logstats.LogStats': None }

When the scraping is done, you will see a similar summary to this:

    2018-02-11 14:13:01 [scrapy.core.engine] INFO: Closing spider (finished) 2018-02-11 14:13:01 [scrapy.statscollectors] INFO: Dumping Scrapy stats:

In these statistic dumps you can find the summary of the whole scraping process: requests, errors, different HTTP codes, number of items scraped, memory usage, and many other useful things. This can give you ideas about where to enable extensions (for example finding which outside domains were triggered or which page wasn’t found). Download finished in 20 minutes. This is way better than the run using my basic scraper from Chapter 3 (I let it run prior to this run and it took 4,009 seconds). And we didn’t have to write so much code.

Exporting the Results. Now you have the extracted data, you have the items representing the information, but the results are gone as soon as the spider finishes, and the Python process is gone from the memory of your computer. Fortunately, Scrapy offers you built-in solutions, but they are very basic (you can call them primitive). But there’s a way to plug in your custom solution and make the scraper behave. In this section we will first explore the built-in options and see if they’re really so primitive. Then we will take a look at how to shape the export to our needs — and yes, this requires writing some code.

Because Scrapy knows that scraping results in saving extracted information, it doesn’t require you to configure the exporter pipeline. You can tell Scrapy to export the scraped results easily via the command-line using the -o option. From this, Scrapy will figure out what type of file you want to save if you provide the right file-extension (.csv for CSV, .json for JSON), or you can add the -t option too and tell in what format you want the data in your specified output file (the value provided with -t has to be a valid feed exporter — more on those later).

The only problem I encountered with these default exporters is that they append the results to the file: if the file doesn’t exist, there’s no problem. However, if the file exists and has contents (for example from a previous run) then the new data is simply appended to the file, resulting in invalid content. Besides the JSON and CSV exporters I will discuss in the next section, you can export your items in XML, Pickle, or Marshal format. They are done with built-in item exporters and use already provided functionality.

1『我也发现了，如果输出的文件是存在的，输出的数据时累加进原来的文件，而不是覆盖掉。』

To CSV. The first approach is to export everything to CSV. As you can see in the previous paragraph, you simply have to run the spider with the -o option providing a CSV file.

    scrapy crawl basic -o sainsburys.csv

If the scraper is finished, you can open the sainsburys.csv file and look at its contents. Note For Windows users, you may encounter extra blank lines in your file. This is because of a currently open bug in Scrapy but the main reason is in the line-ending differences between the operating systems. There’s already a pull-request at github 5 when i’m writing this; it has been merged and i hope it’s available with the next released Scrapy version.

『[[MRG+1] Fix for #3034, CSV export unnecessary blank lines problem on Windows by ReLLL · Pull Request #3039 · scrapy/scrapy](https://github.com/scrapy/scrapy/pull/3039)』

Because each line has a lot of content, I don’t want to list more here. But you can already see the interesting part: the nutrition column (in my example the second column). It has curly braces ({}) with the nutrition dictionary written out as text. This is not good; therefore, we will implement a custom item exporter to handle this case.

To JSON. Exporting to JSON works similar to CSV: you provide a JSON file as output.

    scrapy crawl basic -o sainsburys.json

The result is a JSON file containing entries like this one. Using JSON, the nutrition dictionary fits great into the exported result. The keys could use a bit of tidying, but for now the structure looks great. There’s a little flaw in there: those nasty Unicode characters. To fix this, add the following line to your settings.py file:

    FEED_EXPORT_ENCODING = 'utf-8'

1『可以设置编码格式。』

As an alternative to whole JSON files, you can use JSON-lines. This format exports every item as a single JSON object, which enables handling a large amount of data because you don’t have to load everything into memory and put it together into a megaobject to write to a file — or be read by your target platform. Scrapy has a built-in exporter for this result type too, and you can access it with the following command:

    scrapy crawl basic -o sainsburys.jl

If you look at your file system while running the spiders, you will see that JSON-lines files are written to the disk as soon as they’re processed by the item pipelines! You don’t have to wait till the scraping is done to get a valid file.

To Databases. Well, for databases there’s no out of the box solution; you cannot add an extra parameter to the command line to write your results into a database. If you want your data stored in a database, then you have to write your own solution. However, because storing in a database is a use-case I often encounter, I wanted to add it into this section and not in the next one when I write about bringing your own exporter.

We will take a look at two different types of databases: MongoDB and SQLite. They represent the approach to the majority of databases currently in use, although other cloud-based storage solutions are rising, but most of the clients are still using these types of databases.

First let’s go and create the item pipeline. The idea while using any database is that you need a connection to the target database and you must clean up after you are finished. The pipeline above does this. open_spider is called every time the spider is started, when the scrape starts. close_spider is called when the spider finishes its work and is dismissed. And these are the two methods where you have to open and close the connection to the database. process_item processes the item, and in this case this item is stored in the database.

But the most interesting method is the from_crawler. If present, it has to return a new instance of the pipeline. The crawler provided to the method should be used to access the crawler-specific settings. In the case of the example, we get the connection, database, and collection settingswhere the last two have default values and you don’t have to provide them. To have your pipeline working, you have to configure it in settings.py.

    ITEM_PIPELINES = { 'sainsburys.pipelines.MongoDBPipeline': 300 }

Then you need to provide the database configuration. You can do it either in the settings.py file (which makes the configuration hard-coded):

    MONGO_URI = 'localhost:27017'

or you can provide it through the command line when starting the spider:

    scrapy crawl basic -s MONGO_URI=localhost:27017

Because we’re using pymongo, we don’t even have to provide the database URI. In such cases, pymongo creates a default connection to localhost:27017. After running the spider, we can see the results in the database, as shown in Figure 4-2. you can find a spider using MongoDB to store the extracted information in the folder 03_mongodb among the sources for this chapter.

SQLite. Similar to the MongoDB solution, when using a SQLite database, you have to open and close the connection when the spider is started and finished, respectively. Because handling the nutrition table gets too complex (with the 70 fields, which could be reduced), I won’t implement this part of the export. if you’re interested and want to give it a try, don’t feel intimidated by my approach! First, I defined the table DDL and the insert statement.

As you can see, the class works almost the same as the MongoDB pipeline from the previous example. The interesting part comes when you insert it into the database. Because we have some nullable fields (and properties that don’t have to exist in the item), we have to ensure that we don’t encounter a Python error while saving. To test out the code, you have to add the pipeline to settings.py.

```
ITEM_PIPELINES = { 
    'sainsburys.pipelines.MongoDBPipeline': None 
    'sainsburys.pipelines.SQLitePipeline': 300 }
```

Now you can run the application.

    scrapy crawl basic -s SQLITE_LOCATION=sainsburys.db

Don’t forget to add the SQLite location with the -s settings flag. Without this you’ll get an exception. you can find a spider using sQLite to store the extracted information in the folder 04_sqlite among the sources for this chapter.

Bring Your Own Exporter. This section is the most interesting if you followed along and think the default exporting solution doesn’t fit your needs. Besides item pipelines (which we implemented for database connections), you can define your own feed exporters. These work like the built-in CSV, XML, and JSON exporters but adapted to your taste. In this section we will take a look at both approaches, even though you’ve already written two item pipelines for database storage.

You will now implement a CSV pipeline that will handle the nutritions field properly: instead of writing the whole dictionary as plain text, you will append the fields to the main content. This requires you to store the extracted items in a cache just like with Beautiful Soup, because you cannot know the possible fields you may encounter in all the items. Remember: The website has multiple different nutrition tables that have more or less the same fields.

Filtering Duplicates. You remember the SQLite pipeline. There we defined INSERT OR REPLACE INTO when we saved an item into the database. This is because there are duplicate items that can be found from different pages on the website. With SQLite you can easily overcome this problem, but with other exports you get too much data, and duplicates are never good. Sure, the postprocessing (your customer or data mining algorithm) can fix this, but why not you? Because Scrapy is highly extensible, you will create a duplicate filter based on the item code.

1『写入 SQLite 数据库的过程中可以方便的处理重复 items，还有其他的方法，即此处的主题。』

```
from scrapy.exceptions import DropItem

class DuplicateItemFilter:
    def __init__(self):
        self.item_codes_seen = set()

    def process_item(self, item, spider):
        if item['item_code'] in self.item_codes_seen:
            raise DropItem("Duplicate item found: %s" % item['item_code'])
        self.item_codes_seen.add(item['item_code']) return item
```


The preceding code stores seen item codes in an internal set, and if the item code was seen already then it discards the item. To enable this pipeline, add the following code to your settings.py file:

    ITEM_PIPELINES { 'sainsburys.pipelines.DuplicateItemFilter': 1 }

Setting a low value for the pipeline ensures that duplicates are filtered as soon as they arrive, saving a lot of work for other tasks. And you can use such filter pipeline items for every possible kind of filtering. If you don’t want an item to be present in the final export, then you can create a filter pipeline, add it to your settings.py, and it handles missing values.

Silently Dropping Items. If you add the item filter from the previous section and run your spider, you will see a lot of entries like this one:

One solution would be to raise the LOG_LEVEL to ERROR, but with this approach you end up skipping other warnings that can be useful in analyzing not expected behavior. The other solution would be to write your own log-formatter for dropped items.

```
from scrapy import logformatter
import logging

class SilentlyDroppedFormatter(logformatter.LogFormatter):
    def dropped(self, item, exception, response, spider):
        return {
            'level': logging.DEBUG,
            'msg': logformatter.DROPPEDMSG,
            'args': {
                'exception': exception,
                'item': item,
            }
        }

```

To use this formatter, you must enable it in the settings.py file.

    LOG_FORMATTER = 'sainsburys.formatter.SilentlyDroppedFormatter'

you can find a spider using the duplicate item filter in the folder 05_item_filter among the sources for this chapter.

1『上面的类「SilentlyDroppedFormatter」，需要新建一个文件「formatter.py」，放在爬虫文件夹下，跟「pipelines.py」平行的。』

Fixing the CSV File. Do you remember what problem the currently exported CSV files have? Yes, they write the nutrition information as plain text into one column of the CSV file. This is not ideal. Besides this, the order of the columns may vary between runs because they’re stored in a dictionary.6 You will implement an item pipeline that stores every item during the scraping process and exports only when the spider finishes.

6 In the current version of Python, the dictionaries are ordered by their key per default. This means every time you run your spider on the same 3.6 CPython implementation, the order of the columns will stay the same.

You can see that every processed item is converted to a new dictionary that contains all the fields of the original item, then nutritions and image_urls are removed, finally the original nutritions dictionary is added to this new item by combining the two dictionaries, and the result is stored in memory for later usage.

When the spider finishes, all the different field names are extracted from all the items and are used as the CSV header. The order still varies between Python installations. To fix the order (at least for the standard properties that are not nutrition information) you can define a base list of properties and then add the missing values — something like this:

As always, you can add this pipeline to your settings.py file.

    ITEM_PIPELINES = { 'sainsburys.pipelines.CsvItemPipeline': 800, }

However, using this approach, the CSV file will be written every time you run the spider, even if you export into a different format or don’t want any export. To solve this problem, let’s implement a feed exporter. you can find a spider using this CsV item pipeline in the folder 06_csv_pipeline among the sources for this chapter.

CSV Item Exporter. Feed exports are similar to item pipelines, but you can write them in a general fashion and use them on-demand, without changing the settings.py file. You already used feed exporters (an alternative name for item exporters) when you saved information to CSV, JSON, or JSON-lines files using the -o output file and Scrapy could derive the exporter to use, or you can provide the -t option and tell Scrapy which exporter you want to use. The following list contains the currently built-in feed exporters:

• csv: saves information as CSV.

• json: saves information as JSON.

• jsonlines: saves information as JSON-lines.

• xml: saves information as XML.

• pickle: saves information as Pickle data.

• marshal: saves information in Marshal format, which is similar to Pickle (specific to Python) but doesn’t have any machine architectural issues.

Because item exporters are similar to item pipelines, they process only one item at a time, we have to be tricky and save the items in memory just like for the CsvItemPipeline class. Basically, we will reuse the already written code and rename some methods. But item exporters have a problem: they don’t delete the file, they append to it. Fortunately, there is a solution: you can truncate the file to 0 bytes using the truncate() method. The extended constructor would look like this:

Here you provided mycsv as the name of the feed exporter. This means, later you can call the spider using the -t option and mycsv as argument.

    scrapy crawl basic -o mycsv.csv -t mycsv

you can find an example spider using the just-created feed exporter in the folder 07_csv_feed_exporter among the sources for this chapter.

1『新建一个文件「exporters.py」，放在爬虫文件夹下，跟「pipelines.py」平行的。』

Caching with Scrapy. Even though I think using caching is an advanced configuration option, I’ve added an extra section for this topic to cover. This is because it improves your execution time by multiple times, and once you cache the website locally you can tweak your scraper script as you wish without overloading the target server. If you want to configure caching, for example while developing your scripts, there are some options in Scrapy. Naturally, you can write your own cache just like you did in the previous chapter but before you invest time, sweat, and brain cells into coding your cache, let’s see what is present, what can we utilize.

Scrapy offers caching. The default configuration disables caching; this means, every page is downloaded every time you request it. But as you know, there are a lot of knobs you can turn, and you can enable caching with the HTTPCACHE_ENABLED = True setting.

There are three HTTP cache options you can utilize out of the box: 1) File system storage. 1) DBM storage. 3)LevelDB storage.

And as always, you can write your own solution too; however, I consider this scenario unlikely, because 90% of use-cases can be covered with the built-in solutions. My default caching configuration looks like this:

```
HTTPCACHE_ENABLED = True 
HTTPCACHE_EXPIRATION_SECS = 0 
HTTPCACHE_DIR = 'httpcache' 
HTTPCACHE_IGNORE_HTTP_CODES = []
```

With this you can enable caching, and when you run your spider it stores every request-response pair on your file system in the .scrapy/httpcache folder in your project’s directory, and from now on it uses this cache when you rerun your spider. This is ideal for tweaking your script: download a snapshot of the target website and use it for fine-tuning your item extraction. 

If you have any HTTP response codes that you don’t want cached, you can add them in the HTTPCACHE_IGNORE_HTTP_CODES list, for example:

    HTTPCACHE_IGNORE_HTTP_CODES = [503, 418]

Setting HTTPCACHE_EXPIRATION_SECS to 0 keeps files always in the cache. If you give it a positive value, older cached files are discarded. Note that this setting requires values in seconds! Let’s see what caching has to offer!

Storage Solutions. In this section we will look at the different storage solutions Scrapy has to offer for caching. Out of the box you have the following options available: 1) File System Storage. 2) DBM Storage. 3) LevelDB Storage.

But because you can extend Scrapy easily, you can write your own storage solution (for example to use a custom database, like MongoDB). If you ask me, I am fine with a file system–based solution. However, if you’re running on-demand (for example in the cloud or in a container environment), you may favor a remote caching service, which is most likely based on a database.

File System Storage. If you enable HTTP caching, this is the default solution used. Even though it’s the default, you can add the following line to your settings.py file:

    HTTPCACHE_STORAGE = 'scrapy.extensions.httpcache. FilesystemCacheStorage'

Using this storage option, all requests and responses are downloaded and stored in a folder whose name is unique for this scraper and is 40 characters long. In these folders is all the information identifying the request and the response the middleware will need to identify pages that should be served from the cache.

DBM Storage. To activate the DBM 7 storage, just add (or replace if it exists).

    HTTPCACHE_STORAGE = 'scrapy.extensions.httpcache. DbmCacheStorage'

The default setting is to use the anydbm module, but you can change it using the HTTPCACHE_DBM_MODULE setting.

LevelDB Storage. You can also use LevelDB 8 (a fast key-value storage) for your cache, but it is not encouraged in the development phase of your project because it allows only a single process to access the database at the same time. This is OK if you just run your spider, but if you want to have the Scrapy shell open for your project and run the spider you will end up with an error. To use LevelDB you can change the HTTPCACHE_STORAGE to 'scrapy. extensions.httpcache.LeveldbCacheStorage' in the settings.py file and install LevelDB with the following command:

    pip install leveldb

8 [google/leveldb: LevelDB is a fast key-value storage library written at Google that provides an ordered mapping from string keys to string values.](https://github.com/google/leveldb)

Cache Policies. Scrapy comes with two default policies for caching: 1) Dummy policy. 2) RFC2616 policy.

Dummy Policy. The Dummy policy is the default setting. Here, every request and its response are stored, and when the same request is seen again, the stored response is returned. This is useful if you are testing your spider and want to replay runs at the same. Because this is the default policy, you don’t have to add anything to your project’s settings.py file.

RFC2616 Policy. This policy is aware of cache-control settings and is aimed at production use to avoid downloading unchanged pages, save bandwidth, and speed-up crawls. To enable this policy, add the following setting to your settings.py file:

    HTTPCACHE_POLICY = scrapy.extensions.httpcache.RFC2616Policy 

What does aware of cache-control settings mean? It means that the scraper works according to the RFC2616 caching specification. If you are lazy and don’t want to read the whole specification, here is a small excerpt of what Scrapy can do for you:

Downloading Images. Even though this is not a requirement for our project, you will encounter many tasks where you must download images besides data. Fortunately, Scrapy has a built-in solution for this problem too. For this section, let’s extend our requirements to gather images along with the items. These images will be saved on your file system besides your project files, but you can configure your spider to store the downloaded files at Amazon S3 or Google Cloud. Because Scrapy uses Pillow for image resizing and thumbnail generation, you must install it before you can start gathering images.

    pip install pillow

To get started, first add the following to your settings.py file:

    ITEM_PIPELINES = { 'scrapy.pipelines.images.ImagesPipeline': 5 }

And you have to tell Scrapy where to save the downloaded images. I use the images folder inside the project.

IMAGES_STORE = 'images'

The folder you provide to IMAGES_STORE must exist. The combination of those two settings activates the image pipeline, which downloads the files and stores them on your computer’s hard disk. To get items into this pipeline, you must add

```
image_urls = Field() 
images = Field()
```

to your Item. This is because the ImagesPipeline works using the image_urls field and adds the resulting images to the images field. In the case of the Sainsbury’s scraper, we must rename product_image to image_urls, add images in the SainsburysItem, and change the spider code to fill image_urls with a list instead of a URL.

```
item['image_urls'] = [response.urljoin(response.xpath('//div[@id="productImageHolder"]/img/@src').extract()[0])]
```

Now if you run your spider and save the results (for example using scrapy crawl basic -o images.jl), you will see the downloaded images in the images/full folder, similar to the one shown in Figure 4-3.

The values in the images.jl file are inserted into the item’s images field. A sample value looks like this:

```
"images": [
{ "url": "https://www.sainsburys.co.uk/wcsstore7.25.53/ ExtendedSitesCatalogAssetStore/images/catalog/product Images/23/5060084344723/5060084344723_L.jpeg", "path": "full/4ae5a3a0dfa0fac7f3728d76b788716e8a2bc9fb.jpg", "checksum": "132512348d379f8365ca02082a16adf1" }
]
```

This tells you not only how the file is named on your file system and where it’s downloaded from, but you get a checksum too to verify that the image on your file system is really the same that Scrapy downloaded. In the preceding example, the file can be found under images/full/4ae5a3a0dfa0fac7f3728d76b788716e8a2bc9fb.jpg and is shown in Figure 4-4.

Note you can find the sources for this section in the 08_image_pipeline folder among the sources for this chapter. scrapy uses its own algorithm to generate the file names. This means you can encounter different file names than me if you run the spider on your computer.

Using Beautiful Soup with Scrapy. Sometimes you already have an HTML extractor ready, created with Beautiful Soup, and you don’t want to convert it to Scrapy code. Or you have a team member who is a pro at Beautiful Soup and she creates the extraction code; you only have to take care of configuring Scrapy. In such cases you use the already existing code because you can integrate Beautiful Soup and Scrapy.

```
def parse_product_details_bs(self, response):
    item = SainsburysItem()
    
    from bs4 import BeautifulSoup 
    soup = BeautifulSoup(response.text, 'lxml') 
    h1 = soup.find('h1') 
    if h1:
        item['product_name'] = h1.text.strip()
```

In the preceding code you can see the integration of Beautiful Soup and Scrapy with a subset of the code from the previous chapter. I explicitly use lxml for speed while parsing but you can use any of the available parsers (and by the way, lxml is available out of the box when you install Scrapy). With this information, you can rewrite the spider to use the functionality written in Chapter 3. You can find a sample solution in the 09_beautifulsoup folder among the sources for this chapter.

Logging. Sometimes you prefer to see custom messages in the console while scraping. This is useful if you cut back the log level of Scrapy to INFO but you want to see a little more of the current process. Every spider comes with a logger, which you can access right in its methods. For example, logging the response’s URL would look like this:

    self.logger.info("URL: %s", response.url)

The logger uses the same log levels that you configured in settings.py. If you don’t see a log output on the console, you can turn up the logging (decrease the level to DEBUG). If it still doesn’t show up, then you can be sure that the code is not reached while running.

If you want to do standard logging and not use the logger in your spider (for example because you are in a different file where you don’t have access to a spider), you can either use Scrapy’s log module (which is deprecated so you shouldn’t use it) or Python’s built-in logger module. There are no considerations; logger works the same way as it would in a “standard” Python application.

(A Bit) Advanced Configuration. Because there are a lot of knobs you can turn on your Scrapy project, I add a section to get you started and try out some different combinations. This book has size limitations; therefore, I won’t list every setting you can toggle, but just the most used ones. For more settings, take a look at Scrapy’s documentation: https://doc.scrapy.org.

LOG_LEVEL. Working through this chapter gave you a lot of output while running the spider. However, you can restrict the information to a subset. As a default, Scrapy uses the DEBUG log-level for its output. It logs you every bit of information you can get from the code, and most of the time this is too much. However, you can restrict the log level in the settings.py file by adding the following line:

    LOG_LEVEL = 'INFO'

This sets the log level to log only information, and warning and error messages. This is because of how logging levels work. Each has a priority, and with the log level setting you tell the application to “log the items with this priority and above.”

You can use the following list as a reference to the log-level priority: 1) CRITICAL. 2) ERROR. 3) WARNING. 4) INFO. 5) DEBUG.

This list contains Scrapy’s log level settings. DEBUG is a good setting while developing, but in a running/live system I prefer INFO or sometimes WARNING as the log level. Depending on the developer, you get the right amount of information using this level.

CONCURRENT_REQUESTS. You have already seen this setting at the beginning of this chapter. As its name already tells you, you can limit the number of concurrent requests to one website. Depending on the website, it makes sense to turn this number up a bit or stay with the default value. This is because network operations (downloading the website’s code) take time, and while the thread waits the process/application is hanging idle. In such cases, even with the GIL present, Python can execute multiple threads parallel, and therefore while your code is waiting for one page to load you can download more.

However, you cannot turn the knob forever. Your computer has its limits too, and having 16 or 160 concurrent requests doesn’t make a difference. I suggest you start with 1 request while developing, then use the default setting of 16. This is good for you because you get the required data faster, and this is good for the targeted website too because it’s not overwhelmed by you.

Moreover, sometimes it happens that the target website has request monitoring enabled. This means, requests and their interval are monitored and evaluated, and if your IP exceeds a threshold you get banned for a time from the website — sometimes forever. Therefore, be responsible with your configuration.

DOWNLOAD_DELAY. Accompanying the concurrent requests, you can set the delay between two downloads too. The download delay tells the spider how many seconds it should wait between downloading another page from the same domain or IP address (if CONCURRENT_REQUESTS_PER_IP is set to a nonzero positive number). This configuration awaits seconds as value, but you can provide decimal values too.

    DOWNLOAD_DELAY = 0.125 # 125 milliseconds

This setting is used to not hit the target servers too hard with your requests. Sometimes this setting is useful to avoid detection and mock human-like behavior.

Autothrottling. Previously, you have seen how to set hard download delays and concurrent requests, to act like a good citizen. However, with this approach you can end up with many requests waiting for completion if the server is busy. Or if the server starts to send back error messages, those are returned faster than 200 OK responses, which generate more requests per second because errors are handled faster by Scrapy. However, in case of errors, the scraper should send fewer requests to help the server to recover itself from its (hopefully temporary) failure state.

A solution, and an alternative approach, is to use Scrapy’s autothrottling feature. This is not enabled by default; you must enable it with the following setting:

    AUTOTHROTTLE_ENABLED = True

What the algorithm behind this setting does is adjust the download delay based on the response times of the server. If the server is busy, it sends the responses later, and Scrapy adjusts the download delay to send requests less frequently. If the server has no difficulties, the download delay is reduced, and more requests are sent to the server. And most importantly: non-200-OK responses do not decrease the download delay. You can configure some settings for autothrottling too. For example, setting:

    AUTOTHROTTLE_START_DELAY = 15

You tell Scrapy to wait 15 seconds initially between two requests. Based on the server’s response time, Scrapy can reduce or extend this waiting time. If the latency is big, Scrapy raises this delay. However, you can give it a maximum where it won’t wait longer.

    AUTOTHROTTLE_MAX_DELAY = 25 

This setting tells Scrapy to wait at most 25 seconds until the next request. To have detailed information on all the requests and their responses, you can enable debugging for auto-throttling.

    AUTOTHROTTLE_DEBUG = True

COOKIES_ENABLED. You know cookies. They are settings stored in your browser and exchanged by every request with the server. They store information regarding your session, browsing preferences, or settings at the website. Sometimes they are required to prove you are using a browser. Sometimes you have to avoid a subset, because they tell the server you’re not using a browser. If you’re browsing in the European Union (EU), you get a notification about cookies by visiting almost every EU website. This is quite annoying, but a regulation to be aware of that websites store (let store) information about your browsing history.

As you may think, sometimes it is required to use cookies (for example websites that require login), but sometimes it’s better to avoid them. The default setting in Scrapy is to use cookies. This means that every time the target web server returns an HTTP parameter Set-Cookie its value is stored internally by Scrapy and is sent back to the server with every new request. You can disable this setting by adding the following configuration to your settings.py file:

    COOKIES_ENABLED = False

If you want to debug which cookies are exchanged between the server and your spider, you can add the following configuration:

    COOKIES_DEBUG = True

This will log every sent cookie (the Cookie header in your request) and received cookie (the Set-Cookie header in the response) to the console, or the logging framework you specified.

1『Cookie 还是用默认的激活，不然想豆瓣这种就抓取不了了。』

## 05. Handling JavaScript

### 1. 逻辑脉络

用自己的话总结主题，梳理逻辑脉络，也就是这本书整个地图里这一章所在的节点。

### 2. 摘录及评论

In this chapter we looked at some approaches to scrape websites that utilize JavaScript. We looked at the mainstream Selenium using a web browser to execute JavaScript and then went to the headless world, where you don’t need any window to execute JavaScript and this makes your scripts portable and easier to execute. Naturally, using another tool to get some extra rendering done takes time and provides overhead. If you don’t require JavaScript rendering, create your scripts without any add-ons like Splash or Selenium. You’ll benefit from the speed gain.

1『尽量通过其他途径规避抓取涉及 JS 的信息。』

This chapter is all about handling websites that utilize JavaScript to render information dynamically. You have seen in the previous chapters that a basic website scraper loads the web page’s contents and does its extraction on this source code. And if there’s JavaScript included, it’s not executed, and the dynamic information is missing from the page. This is bad, at least in those cases where you need that dynamic data. Another interesting part of scraping websites that use JavaScript is that you may need clicks or button presses to go to the right page/get the right content, because these actions call a chain of JavaScript functions.

Now I will give you options for how you can deal with these problems. Most of the time you will find Selenium as the solution, if you Google or search the Internet with other engines. However, there are other options present, and I will give you more insight. Perhaps those other options will fit your needs better.

### Reverse Engineering

This first option is for advanced developers — at least I feel advanced developers will do more reverse engineering. The idea here is to use the DevTools from Chrome (or similar functionality in other browsers), enable JavaScript, and monitor the XHR network flow to find out which data is requested from the server and rendered separately.

1『做反向求解的工作，挖掘出从服务器请求回来的数据。』

With the target endpoint (either a GET or a POST request) in your hands, you see which parameters to provide and how they affect the results. Let’s look at a simple example: at kayak.com you can search for flights and, therefore, airports too. In this simple example we will reverse engineer the destination search endpoint to extract some information, even if this information is not valuable. I’ll use Chrome for these examples. This is because I use Chrome for all my scraping tasks. It will work with Firefox too, if you know how to handle the developer tools.

First let’s go to kayak.com, open up the DevTools window, and locate the Network tab there, as shown in Figure 5-1. As you can see in the image, I already navigated to the XHR tab inside the Network tab because all AJAX and XHR calls are listed here. Now let’s click the field on the website labeled To? and type in a letter, for example S, and watch the values on the right side inside the XHR tab, as shown in Figure 5-2.

Now you get a list of some possible airports on the website, but two XHR requests too. We’re interested in the request starting with marvel:

www.kayak.com/mv/marvel?f=h&where=so&s=50&lc_cc=US&lc=en&v=v2&cv=5.

This is the request that returns the information about the airport. It has some parameters where I have no idea what they do and how the results are affected if changed, but here’s what I know: 1) where is the key you’re searching for. 2) s is the type of the search; 58 is for airports. 3) lc is the locale; you can change it and get different results — more on this later. 4) v is the version; there’s a small difference in the result format if you choose v1 instead of the default v2.

Based on this information, what can we get out of it? We get some airports, and some idea about how to reverse engineer JavaScript and when to decide to use a different tool. In this example, the JavaScript rendering is a simple HTTP GET call — nothing fancy, and I bet you already have an idea how to extract information delivered from these endpoints. Yes, using either the requests and Beautiful Soup libraries or Scrapy and some Request objects.

Back to the example: when you vary the lc value, for example, to de or es in the request, you get back different airports and the description of these airports in the locale you chose. This means JavaScript reverse engineering is not just about finding the right calls you want to use but also requires a bit of thinking.

Thoughts on Reverse Engineering. If you find yourself having a search that utilizes an HTTP endpoint to get the data, you can try to figure out how the search works. For example, instead of sending some values you expect to deliver results, try to add search expressions. Such expressions could be * to match all, .+ to evaluate regular expressions, or % if it has some kind of SQL query in the back.

You see, sometimes JavaScript reverse engineering pays off: you learned that those nasty XHR calls are simple requests and you can cover them from your scripts. However, sometimes JavaScript makes more complex things like rendering and loading data after the initial page is loaded. And you don’t want to reverse engineer this, believe me.

### Splash

Splash 1 is an open-source JavaScript rendering engine written in Python. It is lightweight and has a smooth integration with Scrapy. It is maintained, and new versions are released every few months, when need arises.

Splash is a nice Python-based website rendering tool that you can integrate easily with Scrapy. One drawback is that you must install it manually through a somewhat complicated process or using Docker. This makes porting it to the cloud complicated (see Chapter 6 for Cloud solutions), therefore you should use Splash only for a local scraper. However, locally it can give you a great benefit with its seamless integration with Scrapy for scraping websites using JavaScript to render content dynamically. Another drawback is the speed. When I used Splash on my local computer, it barely scraped 20 pages per minute. This is too slow for my taste, but sometimes I cannot get around it.

3『[Splash - A javascript rendering service — Splash 3.4 documentation](https://splash.readthedocs.io/en/stable/)』

1『Splash 真要深入使用估计得结合 docker，又简单容器 docker，得去学。目前暂定先学「2020071The_Docker_Book」。』

Set-up. The basic and easiest usage of Splash is getting a Docker image from the developers and running it. This ensures that you have all the dependencies required by the project and can start using it. In this section we will use Docker. If this is done, you can get the image executing the following commands on your console:

```
docker pull scrapinghub/splash 
sudo docker run -p 5023:5023 -p 8050:8050 -p 8051:8051 scrapinghub/splash
```

Note On some machines, administrator rights are required to start Splash. For example, on my Windows 10 computer, I had to run the docker container from an administrator console. On Unix-like machines, you may need to run the container using sudo. Now Splash is running on localhost:8050, and it should look something like Figure 5-3.

1『经验证，Mac 上需要用 sudo 来跑，sudo docker run -p 5023:5023 -p 8050:8050 -p 8051:8051 scrapinghub/splash』

Now you can enter a URL at the top right corner and hit Render me! to get the website rendered. If you input http://sainsburys.co.uk you get a similar result to the one shown in Figure 5-4 (the image will vary). As you can see, you get a screenshot from the page you are scraping, and below it some statistics and timing of the requests rendering the website involved. At the bottom of the page you see the source code of the website, as shown in Figure 5-5. This source code is the one you get after the page is rendered. To verify this, you can open an interactive Python shell and get the website using requests.

```
>>> import requests
>>> r = requests.get('http://sainsburys.co.uk')
>>> r.text 
```

The preceding example result is just an excerpt. If you save this code into an HTML file and open it in a browser and do the same with the sources returned by Splash, you will see the same page. The difference is in the sources: Splash has more lines and contains expanded JavaScript functions.

1『比较 requests 抓取的和 Splash 里的，Splash 含有更多的信息，作者应该是这个意思。』

A Dynamic Example. To see how to get Splash working with dynamic websites (which utilize JavaScript a lot), let’s see a different example. For instance, http://www.protopage.com/ generates you a web page based on a prototype, which you can customize. If you visit the site, you must wait some seconds until the page gets rendered. If we want to scrape data from this site (there’s not much available either, but imagine it has a lot to offer) and we use a simple tool (the requests library, Scrapy) or Splash with the default settings, we only get the base page that tells us that the page is currently rendered. To have the rendered site rendered with Splash, I altered the script (which is written in Lua by the way) and turned up the wait time to three seconds.

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

Integration with Scrapy. The recommended way by Splash developers is to integrate this tool with Scrapy, and because we use Scrapy as our scraping tool, we will take a thorough look at how it can be accomplished. First, we need to install the Splash Python package using pip.

    pip install scrapy-splash

Now that this library is installed, we need to enable the middlewares that have been delivered with scrapy-splash. The prceding numbers are not fully empiric: the Splash middlewares must have a higher order than the HttpProxyMiddleware, which has a default value of 750. To be on the safe side (for example Scrapy changes the default value of this proxy middleware), we could alter the middleware configuration like this:

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

The second variable points to a cache storage solution, which is aware of Splash. If you’re using another custom cache storage, you must adapt it to work with Splash. This requires you to subclass the aforementioned storage class and replace all calls to scrapy.util.request.request_ fingerprint with scrapy_splash.splash_request_fingerprint to have those nasty changed fingerprints work out. The last change we must adapt is the usage of Requests: instead of using the default Scrapy Request we need to use SplashRequest. Now let’s adapt the Sainsbury’s spider to use Splash.

Adapting the basic Spider. In an ideal world, you would only need to alter the configuration as we did in the previous section, and all requests and responses would go over Splash because we don’t have any usages of Scrapy’s Request objects. Unfortunately, we need some more configuration in the code of the scraper too. If you don’t believe me, just start the scraper without having Splash running.

To get our scraper running through Splash, we need to adapt every request call to use a SplashRequest, and every time we initiate a new request (either when starting the scraper or yield-ing some response. follow calls). To get the first start right, we can add the following function to our script:

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

So, we’re good and we render the first page through Splash, but what about the other calls like navigating to the detail pages or the next page? To adapt these, I changed the XPath extraction code a bit. Until now, we used the response. follow approach where we could provide the selector containing the potential next URL we want to scrape. Using Splash, we need to extract these URLs and provide them as parameters to the SplashRequest constructor. I’ll use the parse method as an example. It looked like this at the end of Chapter 4:

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

One change I made besides the ones mentioned previously was to rename the spider to splash. Running the scraper stays the same.

    scrapy crawl splash -o splashburys.jl

After the scraper finishes, you will find records similar to the following excerpt in the splashburys.jl file.

What Happens When Splash Isn’t Running? Good question, but I bet you already have the answer. The scraper won’t do anything, and exits with an error message containing the following valuable information to identify this particular error cause.

### Selenium

Selenium is an alternative tool that website scraper developers use because it supports JavaScript rendering through a browser. We saw some solutions on how to integrate Selenium with Scrapy but skipped the built-in methods to extract information. Again, using an external tool like Selenium makes your scraping slower, even in headless mode.

If you search the Internet about website scraping, you will most often encounter articles and questions about Selenium. Originally, I wanted to leave Selenium out of this book because I don’t like its approach; it’s a bit clumsy for my taste. However, because of its popularity, I decided to add a section about this tool. Perhaps you will embed a Selenium-based solution to your Scrapy scripts (for example you already have a Selenium-scraper but want to extend it), and I want to help you with this task.

First we will look at Selenium and how to use it in a stand-alone fashion, then we will add it to a Scrapy spider.

Prerequisites. To have Selenium working on your computer, you must install it like most Python libraries through the Python Package Index.

    pip install selenium

To use Selenium for website scraping, you will need a web browser. This means you will see the configured web browser (let’s say Firefox or Chrome) open up, load the website, and then Selenium does its work and extracts the script you defined. To enable linking between Selenium and your browser, you must install a specific WebDriver.

For Chrome, visit [ChromeDriver - WebDriver for Chrome](https://sites.google.com/a/chromium.org/chromedriver/home). I downloaded version 2.38. For Firefox, you need to install GeckoDriver. It can be found at GitHub. I downloaded version 0.20.1. These drivers must be on the PATH when you’re running your Python script. I put all of them inside a folder, because in this case I have to add only this one folder and all my web drivers are available.

Note that these web drivers require a specific browser version. For example, if you already have Chrome installed and download the latest version of the web driver, you may encounter an exception like the one following if you miss updating your browser:

raise exception_class(message, screen, stacktrace) selenium.common.exceptions.SessionNotCreatedException: Message: session not created exception: Chrome version must be >= 65.0.3325.0

(Driver info: chromedriver=2.38.552522 (437e6fbedfa 8762dec75e2c5b3ddb86763dc9dcb),platform=Windows NT 10.0.16299 x86_64)

Basic Usage. Now to verify if everything is working fine, let’s write a simple script to open the Sainsbury’s website for us using Selenium.

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

1『

查到自己浏览器的版本是  80.0.3987.116，然后下载了驱动版本号为：ChromeDriver 80.0.3987.106。打开驱动进入其指定的端口：http://localhost:9515/，发现报错，估计上面代码用不了，试验了下果然。然后在 stackflow 找到了答案，要自己指定驱动的径路的：[selenium - ChromeDriver v80 doesn't work even though Chrome version is matched (Chrome v80) - Stack Overflow](https://stackoverflow.com/questions/60292349/chromedriver-v80-doesnt-work-even-though-chrome-version-is-matched-chrome-v80)

```
from selenium import webdriver
driver = webdriver.Chrome(executable_path='/Users/Daglas/scrapys/chromedriver')
driver.get('https://sainsburys.co.uk') 
```

』

OK, it’s nice to have the browser open automatically and navigate to the target website. But what about scraping information? Because we have a website in our reach (in the browser), we can parse the HTML — almost like we did in the previous chapters or use Selenium’s offering for data extraction from the HTML of the web page. I won’t go into detail on Selenium’s extractors because it would exceed the boundaries of this book, but let me tell you that by using Selenium you have access to a different set of extraction functions, which you can use on your browser instances.

Integration with Scrapy. Selenium can be integrated with Scrapy. The only thing you need is to configure Selenium properly (have the web drivers on the PATH and the browsers installed) and then the fun can begin. What I like to do is to disable the browser window for my scrapes. That’s because I get distracted every time I see a browser window if it navigates the pages automatically, and it would go crazy if you combine Scrapy with Selenium. Besides this, you will need a middleware that will intercept calls prior to sending them directly through Scrapy and will use Selenium instead of normal requests. A rudimentary middleware would look like this one:


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

The preceding code uses Firefox as the default browser and starts it in headless mode when the spider is opened. When the spider closes, the web driver is closed too. The interesting part is when the request happens: it is intercepted and routed through the browser and the response HTML code is wrapped into an HtmlResponse object. Now your spider gets the Selenium-loaded HTML code and you can use it for scraping.

scrapy-selenium. Recently, I have found a fresh project at GitHub called scrapy-selenium. 2 It is a convenient project to have you install and use it to combine the powers of Scrapy and Selenium. I think it is worth sharing this project with you.

2 [clemfromspace/scrapy-selenium: Scrapy middleware to handle javascript pages using selenium](https://github.com/clemfromspace/scrapy-selenium)

Note: Because this project is a private one, it may have issues. If you find something not working, feel free to raise an issue for this project and the developer will help you out to fix that problem. If not, shoot me an email and I’ll see if I can give you a solution or perhaps maintain the application myself and deliver newer versions. This project works just like the custom middleware we implemented in the previous section: it intercepts requests and downloads the pages using Selenium. Let’s start with the configuration.

1『有好的问题可以直接发邮件给作者。』

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

### Solutions for Beautiful Soup

Even though we focus on Scrapy, because in my opinion it’s currently the website scraping tool for Python, you can see that options that make Scrapy handle JavaScript can be added to “plain” Beautiful Soup scrapers. And this gives you options to stay with the tools you already know!

Until now, we looked at solutions where we can integrate JavaScript-based website scraping with Scrapy. But some projects are fine using Beautiful Soup and don’t need a full scraper environment.

Splash. Splash offers manual usage too. This means, you have an alternative option to get Splash to render a website and return the source code back to your code. And we can utilize this to have a simple scraper written with Beautiful Soup. The idea here is to send an HTTP request to Splash, providing the URL to render (and any configuration parameters) and get the result back, and then use Beautiful Soup on this result, which is a rendered HTML.

To stick with the previous example, we will convert the scraper form Chapter 3 into a tool that utilizes Splash to render the pages of Sainsbury’s. The idea here is to simply call Splash’s HTTP API to render the web page instead of getting the page through the requests library. This means our only change will be in the get_page function, where we forward the URL we want to scrape to Splash.


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

1『这里异常处理的方式很值得借鉴，返回的错误不知道嘛，那就用 pass 替代，然后返回 None。』

As you can see, we call the render.html endpoint of our Splash installation and provide the target URL as a simple GET parameter. If you’re more into POST requests, you can change the prceding function to look like this:

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

Selenium. Of course, we can integrate Selenium to our Beautiful Soup solutions too. It works the same way as it did with Scrapy. Again, I won’t use the built-in Selenium methods to extract information from the website. I use Selenium only to render the page and extract the information I require. To do this, I’ll add two helper functions to the scraper, which initialize and tear down Selenium at the required places.

1『作者一直强调的观点，不要用 Selenium 内置的方法直接抓取，而只是把它当做渲染工具，渲染返回的结果用其他手段来处理。』


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

## 06. Website Scraping in the Cloud

In this chapter we looked at options for how to run scrapers in the cloud. This is the solution if you don’t want to run your extractors every time manually, or you don’t want to have them run on your computer because they eat a lot of resources and your computer gets slow for a long time. We looked at Scraping Hub, which provides services specific for Scrapy and this makes it unique. Besides this, they’re the developers of Splash too and they have a solution for how you can run your Splash-based spiders in the cloud. As an alternative, we looked at PythonAnywhere, where you can upload Python scripts and execute them. This is not only useful for Scrapy but for scripts using Beautiful Soup too, and this moves your simple scrapers into the Cloud too.

Running website scraping locally is fine for do-once tasks and small amounts of data, where you can easily trigger the crawl manually. However, if you want reoccurring tasks and automatic scheduling, you should think about other solutions such as deploying your spiders somewhere into the cloud or a bought server slot. In this chapter we will look at the virtual network of servers, the cloud, and what options you have if you want to use website scraping in the cloud. I’ll focus on Scrapy because it is the tool for website scraping and there are services provided and matched for use with Scrapy.

###  Scrapy Cloud

ScrapingHub is the ideal solution in my eyes, if you have bigger Scrapy projects, because it offers an easy to use platform for setting up and evaluating your project. The presence of the Python library to access your scraped data (and interacting with your spiders too) makes it convenient both to automate data extraction and work with this data. The free plan gives you a lot, and help is there to get you started.

Creating a Project. When you arrive at ScrapingHub, you will want to create a project because the page you get is empty, as shown in Figure 6-1. Fortunately, it is intuitive: we must click the green button in the upper right corner. We will use Scrapy spiders, so select this option, as shown in Figure 6-2.

Now that the project is created, we must upload our spider to the cloud. There are two options: over the command line or cloning a GitHub repository, as you can see in Figure 6-3. We will go with the command line solution because I am a nerd, and because most of the time I use some internal Git system and not GitHub to store my code. If you decide to use the command line, you have two options: to deploy directly or a Docker image. I will stay with the simple deploy version for now.

1『又见 docker 镜像，docker 实在是重要。』

Deploying Your Spider. Because I use the basic command line deployment, I go to the spider’s base folder (where the scrapy.cfg file is located) and execute the following commands:

```
pip install shub 
shub login 
shub deploy
```

After you run the shub deploy command the first time, you will see following message among others:

    Saved to scrapinghub\sainsburys\scrapinghub.yml.

This file is important because you must edit this file if you deploy a Python 3 spider. And because I focused on Python 3, we will use this configuration. Let’s do this now and add the following line to your scrapinghub.yml:

    stack: scrapy:1.5-py3 

This tells ScrapingHub that you want to use Scrapy version 1.5 running in a Python 3 environment. After this change, run shub deploy again to update the spider on the server. The deployment information is then something similar to what is shown in Figure 6-4.

Start and Wait. After deployment, in the upper left corner you will see that you have one spider, like in Figure 6-5. Clicking this link (or the Dashboard menu entry in the Spiders section) navigates you to your spiders. Clicking the basic spider (for me the only spider deployed) will get you to the spider’s page, as shown in Figure 6-6. Here you can change some project specific settings, and you can run the spider.

Running the Sainsbury’s spider takes some time. But you can do it and wait for its completion. After running the spiders, you will see all information about runs — even if you had errors while running your spiders, as shown in Figure 6-7. As you can see, you get information about loaded items, sent requests, and some statistics. If you click the job’s number, you will get some detailed statistics and you can look at the items extracted by the run, as shown in Figure 6-8.

Accessing the Data. You can access the extracted information in some ways. The most common access is to download your results in some format, as you would export it while running Scrapy from your command line, as shown in Figure 6-9. 

As you can see, you get some options and one will fit your project’s needs. An alternative option is to publish your dataset. This makes it available to people even without knowing how you gathered the data. Publishing comes in three flavors: 1) Public: Everyone has access to the data, no need for ScrapingHub account, and search engines can index it. 2) Protected: Only users with ScrapingHub account can access this data. 3) Private: Oonly members of your ScrapingHub organization can access the data.

If you have confident information, then use private. ScrapingHub has some issues with publicly available datasets, and you cannot access them without a ScrapingHub account. Anyhow, if you want to publish a dataset, you must provide a description and a logo to it to be publicly available. I agree with the description, but a logo is in my eyes too much. Sure, if you look at the catalog, 2 you will see why a logo is required, as shown in Figure 6-10.

2 [Datasets · Scrapinghub](https://app.scrapinghub.com/datasets)

From these datasets, you can download the items the same way you can through your job’s page. note, that you have to be logged in to see the available datasets.

API. ScrapingHub provides an API that you can use to access your data programmatically. Let’s examine this option too. I suggest you use the scrapinghub Python library, because accessing the API directly (with curl for example) doesn’t work the way it is described in the documentation.

    pip install scrapinghub[msgpack]

Now we’re ready to access our data from a simple Python code. I’ll use the interactive interpreter so you can follow along.

```
>>> from scrapinghub import ScrapinghubClient
>>> apikey = 'YOUR-API-KEY'
>>> client = ScrapinghubClient(apikey)
>>>
>>> client.projects.list() [310577]
```

The first step, after logging in, is to get the ID of our project. Because I have only one project, I get only one ID back. You’ll get back a different one, so replace accordingly.

```
>>> project = client.get_project(310577)
>>> [j['key'] for j in project.jobs.list()] ['310577/1/4']
```

Above we list all the jobs associated with the project. This job key is needed to access the data. If you have long-running jobs, you can use the state flag of the job’s metadata information:

```
>>> job = project.jobs.get('310577/1/4')
>>> job.metadata.get('state') 
 'finished'
```

Now that we have the job we’re interested in, let’s retrieve all the items.


```
>>> job.items.iter() <generator object mpdecode at 0x000001DAC5092D58>
>>> for item in job.items.iter(count=1):
... print(item) ...

```
As you can see in the preceding code, you can get a generator over the items associated with the job; I printed out the first result of the list. If you’re interested in how many items have been extracted, you can use the metadata of the job again.

    >>> job.metadata.get('scrapystats')['item_scraped_count'] 923

As you can see, the API is very useful to split up data extraction from websites and process them automatically with scripts later.

Limitations. Free accounts have some limitations. Let’s look at them, even if you can go along very well with these limits. 1) First, there is a limitation of one concurrent crawl, which means you can only run one spider at a time. For starting out, this is not a problem because you will rarely want to run spiders in parallel. If the number of your customers is growing, then you can encounter occasions when you need parallel runs to gather data faster. 2) The second limitation, which can be annoying if you have jobs that should be run frequently, is no periodic jobs. You can configure them, but they won’t run until you subscribe to a paid plan, which start currently at \$9 per month. 3) The third big limitation is data storage. Your scraped results are stored only for seven days. After that time, your crawl result is history. You can extend this period to 120 days if you subscribe to a paid plan. But you can overcome this problem if you have automatic data processing (through the API), or if you store your data in a database.

### PythonAnywhere

Python Anywhere offers you cloud hosting and scheduling for free; however, it has limitations on the outgoing connections for the free plan. And this makes it only valuable for practicing. On the other side, if you pay $5 a month, you get an upgraded account where you don’t have to limit your scrapings to the whitelist.4 

OK, there are other options besides ScrapingHub, of course. One is PythonAnywhere, 3 a platform solution that enables you to run Python in the cloud. It has a free “beginner” account, which has limitations on outbound internet access, CPU, and memory usage, but it will fit our purposes. In this section we will create a simple scraper written in Scrapy, and we will upload it to the cloud.

### What About Beautiful Soup?

PythonAnywhere is a cloud platform for Python. This means you can not only run Scrapy spiders there but Beautiful Soup scrapers too. And this is what we will look at in a nutshell. The approach is the same as previously: we will extract the same sights but using Beautiful Soup. Fortunately, the requests and beautifulsoup4 libraries are already installed on the host computer, so you do not need to install anything.

The first step is to write and upload the script. Actually, I have already written the code, but this doesn’t mean you cannot do it for yourself. As always: my code examples are just one solution and there are many paths that lead to the final goal.


```
import requests
from bs4 import BeautifulSoup

bs_parser = 'html.parser'


def get_page(url):
    try:
        r = requests.get(url)
        if r.status_code == 200:
            return BeautifulSoup(r.content, bs_parser)
    except Exception as e:
        pass
    return None


def get_sights():
    soup = get_page('https://www.berlin.de/en/attractions-and-sights/')
    if not soup:
        return

    for sight in soup.select('div[class*="teaser"]'):
        h3 = sight.find('h3')
        if not h3:
            continue
        a = h3.find('a')
        if not a:
            continue
        name = a.text
        if not name:
            continue

        description = ''
        div = sight.find('div', class_='inner')
        if div:
            p = div.find('p')
            if p:
                description = p.text
        if not description:
            continue
        yield (name, description)


if __name__ == '__main__':
    with open('berlin_sights.jl', 'w') as outfile:
        for sight in get_sights():
            outfile.write('{' + '"name": "{}", "description": "{}"'.format(sight[0], sight[1]) + '}\n')

```

2『上面是附件里的源码，最后的主函数与书里的稍微有些不同，以后可以深度研究。』

After uploading, we can run the script. Running the script works as it would in a normal terminal window.

    python3 berlin.py

After the process finishes, you can access the results in the berlin_ sights.jl file. The first entry looks like this: