# 04 Using Scrapy

After a lengthy introduction to Beautiful Soup and custom scrapers, it’s time to look at Scrapy: the website scraping tool for Python.

In my opinion, this is the only viable tool available currently for Python, which can handle complex scraping tasks out of the box. You can cache web pages, and add parallelism as you wish; you only need to configure Scrapy properly and write the extraction code.

In this chapter you will learn how to get the most out of Scrapy for the majority of your website scraping projects. You will write the Sainsbury’s extractor, configure Scrapy to create a website-friendly spider, and you will learn how to apply custom exporting options to the extracted information.

As opposed to the previous chapter, where I introduced Beautiful Soup at the beginning and you created the project to scrape the Sainsbury’s website afterward, now you will learn the basics of Scrapy through implementing the project scraper. Toward the end of this chapter I’ll add more information and insights into the tools that we didn’t use for the project, but I think it is useful to know if you write your own scrapers in the future.

Ready? Why not!

## 01. Installing Scrapy

Your first task is to install Scrapy to your Python environment.

To install Scrapy, simply execute

    pip install scrapy

And that’s it. With this command you installed all requirements too, so you’re ready to create scraper projects.

Note The developers of Scrapy recommend installing the tool into a virtual environment. This is a good practice to have a clean version of your scraping tool; and this hinders you from updating a dependency of Scrapy to a noncompatible version, which will render your scraper nonworking.

If you have a hard time installing Scrapy, just read their instructions.1 

## 02. Creating the Project

To get started with Scrapy, you have to create a project. This helps you to keep order in your files and focus on only one problem. To create a new project, simply execute the following command:

    scrapy startproject sainsburys

This call results in something like this:

New Scrapy project 'sainsburys', using template directory 'c:\\python\\scrapy\\lib\\site-packages\\scrapy\\templates\\ project', created in:

C:\scraping_book\chapter_4\sainsburys

You can start your first spider with

cd sainsburys scrapy genspider example example.com

Depending on the OS you use and the location where you have your projects, the preceding text can vary. However, what matters is the information about how you can create your first spider.

But before you create your first spider, let’s look at the file structure created, as shown in Figure 4-1.

Figure 4-1. The project structure

The structure should be similar; if not, perhaps something changed in the new version of Scrapy you are using.

## 03. Configuring the Project

Before you dive into the code of the main scraper you will implement with Scrapy, you should configure your project properly. Basic configuration is required to show you are a “good citizen,” and your spider is a well-raised tool too.

The basic configuration I suggest you do every time is to add the user agent and see that the robots.txt file is honored.

Fortunately, the basic project skeleton of Scrapy comes with a configuration file where most of the settings are set properly or are commented out but tell you about the option and which values it accepts. You can find the configuration of the project in the settings.py file.

If you take a look at it, you will see a lot of options added; most of them are commented out. The default values work perfectly fine for most scraping projects, but you can tune them if you think it gives you better performance or you need some more complexity added.

The two properties I always use are

• USER_AGENT

• ROBOTSTXT_OBEY

The names of these properties already tell you what they are good for. For the USER_AGENT, you see a default that consists of the bot’s name (sainsburys) and an example domain. I change it mostly to a Chrome agent. You can obtain one through the DevTools of Chrome: you open the Network tab, load a web page normally in your browser, click on the request in the Network tab, and copy the value of User Agent in the Headers tab of the request. This works even if you are offline.

And to be a good citizen, leave the ROBOTSTXT_OBEY on True. With this, Scrapy takes care of handling the contents of the robots.txt file if one is present.

i suggest you delete all commented-out settings. This will help you in reading the file later and you see all active configuration at once; you do not have to scroll through all the lines to see which is commented out. it is hard even in an iDe with good color coding.

Besides these properties, I suggest you add CONCURRENT_REQUESTS = 1. This reduces the speed of the spider, but while testing, you will run the code quite a lot and you don’t want to get banned from the website right at the beginning—or you don’t want the website’s servers to be done just because you (and 99,999 other readers) run the scraper simultaneously and the servers cannot handle the load. If you look at the commented code, you’ll find that the default value for this is 16. I’ll add a section where I will turn up the number of parallel requests and will do a flawed microbenchmark.

To summarize: my final settings.py file looks like this:

```
# -*- coding: utf -8 -*

BOT_NAME = 'sainsburys' 
SPIDER_MODULES = ['sainsburys.spiders'] 
NEWSPIDER_MODULE = 'sainsburys.spiders' 
USER_AGENT = 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36' \ '(KHTML, like Gecko) Chrome/63.0.3239.84 Safari/537.36' 

ROBOTSTXT_OBEY = True 
CONCURRENT_REQUESTS = 1

```

Now that the basic configuration is done, we can implement the spider that will do the work for us.

## 04. Terminology

While setting the configuration, you have had the option to learn some of Scrapy’s terminology, like middleweare or pipeline. They are the building blocks of this scraper, where you can implement your own code and extend the functionality if it is missing something you need.

### 1. Middleware

Middlewares are hooks into Scrapy; this means, you can extend the already available functionality. There are two types of middlewares in Scrapy:

• Downloader middlewares

• Spider middlewares

As their names already suggest, you can either extend the downloader (add your own cache, proxy the calls, modify requests prior sending, or ignore requests, just as a few examples), or the parser functionality (filter out some responses, handle spider exceptions, call different functions based on the response, etc.).

For basic scraping there’s no need to write your own middlewares, because you can get along well with the tools available—and as Scrapy is evolving, more custom code gets into the standard library.

Middlewares need to be activated in the settings.py file.

```
DOWNLOADER_MIDDLEWARES = { 'yourproject.middlewares.CustomDownloader': 500 }

SPIDER_MIDDLEWARES = { 'yourproject.middlewares.SpiderMiddleware': 211 }
```

If you have your middlewares but they don’t seem to work, you might have forgotten to activate them. Another reason could be that they are executed at the wrong position: the number you provide as the value in the dictionary tells Scrapy about the order in which the middleware should be executed:

• For downloader middlewares, the process_request method is called in increasing order.

• For downloader middlewares, the process_response method is called in decreasing order.

• For spider middlewares, the process_spider_input method is called in increasing order.

• For spider middlewares, the process_spider_output method is called in decreasing order.

Therefore, it can happen that you expect something in the request / response / input / output, but it was handled by a middleware with a lower / higher priority.

### 2. Pipeline

Pipelines handle the extracted data. This involves cleaning, formatting, and sometimes exporting the data. Even though Scrapy has built-in pipelines that export your data in a given format (CSV, JSON—more on these later in this chapter), sometimes you need to write your own pipeline to configure the result to meet your (your customers’) expectations.

You will write more pipelines than middlewares while you’re working as a pro scraper. Nevertheless, it is not as bad as it might sound. In this chapter we will create a simple item pipeline to show you how it is done.

Similar to middlewares, you have to activate your pipelines in the settings.py file.

    ITEM_PIPELINES = { 'yourproject.pipelines.MongoPipeline': 418 }

### 3. Extension

Extensions are singleton classes that get instantiated once at startup and contain custom code, which you can use to add some custom functionality that is not related to downloading or scraping like a middleware does. Such extensions can be used for logging, or monitoring memory consumption (these are already built-in extensions).

Extensions can be loaded the same way as middlewares and pipelines in settings.py.

    EXTENSIONS = { 'scrapy.extensions.memusage.CoreStats': 500 }

### 4. Selectors

This is the most important term you will encounter while using Scrapy. Selectors are the code parts that select certain parts of the HTML. As you can see, selectors work similar to Beautiful Soup and lxml but they are the Scrapy version, and you can use XPath or CSS expressions.

I prefer XPath expressions because I worked for years with XML and XML transformations; therefore, I know XPath expression well. You are free to use any approach, but I will stick to XPath.

Selectors are objects in Scrapy, and because of this they can be constructed from a text.

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

However, because selectors are the way to extract data, you can conveniently access them from your response using

response.xpath()

or

response.css()

And this makes Scrapy a great tool in my opinion: you don’t have to bother creating selector objects, but use the available convenient method accesses.

Follow the links if you want to read more about CSS selectors 2 or XPath expressions.3 

[Selectors Level 4](https://www.w3.org/TR/selectors/)

[xpath cover page - W3C](https://www.w3.org/TR/xpath/all/)

## 05. Implementing the Sainsbury Scraper

To start working on the extraction code, you will need a spider generated. As you have seen in the previous section, where you created and configured the base of the project, you can do it with the genspider command. Let’s do it right now. First change the directory to the one where you generated your bot, and then execute the following command:

scrapy genspider sainsburys 'https://www.sainsburys.co.uk/shop/ gb/groceries/meat-fish/'

When executing the preceding command, you get a strange message:

Cannot create a spider with the same name as your project

Well, if we cannot get a spider with the same name, let’s give it a different name. My suggestion is a name that is easy to remember for you. I use mostly "basic" because it’s easy to write and I have a basic scraper to do the extraction for me. The project already has a unique name; and with basic I can always start my spiders, regardless of the project.

scrapy genspider basic https://www.sainsburys.co.uk/shop/gb/ groceries/meat-fish

The response now is different.

Created spider 'basic' using template 'basic' in module:

sainsburys.spiders.basic

With this command, Scrapy added a basic.py file to the project’s spiders folder. This file will be the base of your spider; here will you implement the extraction code.

The code looks normal, but if you look thoroughly, you will see that the start_urls variable looks a bit weird.

start_urls = ['http://https://www.sainsburys.co.uk/shop/gb/ groceries/meat-fish/']

It has an extra http://. This is because of the URL we provided for the scraper generation. Scrapy is meant to scrape a domain; therefore, you should provide a domain for the spider creation. However, in the particular case of the example, we will scrape only a subset of the whole domain (“Meat & fish”). There are two options:

• You create the spider using only the domain 'www.sainsburys.co.uk' and add the remaining part of the URL later to the start_urls (or change the entry completely).

• you simply remove the extra 'http://' from the start_urls entry.

### 1. What’s This allowed_domains About?

If you looked at the code thoroughly, you have seen there’s a list of allowed domains. This list is used to give the spider a bound. Without setting the allowed domains, you could write a script that goes through the Internet (following every link on the pages it scrapes). For most purposes, you want to keep your scraping in one domain. However, sometimes you have to deal with internal or subdomains. In those cases, you can extend this list manually to fix such “issues.”

And here you should set the domain only. When you generated the spider, it added the whole URL to this list, but you need something like this:

allowed_domains = ['www.sainsburys.co.uk']

you can find the source code for an empty project with my default configuration among the sources for this chapter in the folder 01_empty_project.

### 2. Preparation

This section is brief. If you followed along, you have everything configured and there is no need for any other preparation.

Just a quick checklist to see if you are ready to go:

• You’ve read the requirements of Chapter 2.

• You’ve created a Scrapy-project.

• You’ve configured the project as described in this chapter.

• You’ve created a spider.

If anything is missing, take the time to fix it; then you are good to follow along.

#### Using the Shell

One function of Scrapy I like to utilize for preparation work is to use its shell, which gives us an environment to test and prepare code snippets for extraction. And because the shell behaves just like your spider code will, it is ideal for creating the building blocks of your application.

With a naive approach (or similar, like we did in the previous chapter), you’d write a part of your code and run the spider. If there’s an error, you’d fix the code and rerun the spider. This is OK if the website doesn’t limit access based on requests. If there’s a limit, you may end up exceeding it and your spider (and your computer, current IP, whole company network4 ) is banned from the website. And, as I have seen, Sainsbury’s runs behind CloudFlare—you better not send parallel requests to their website!

4 Once our client was banned from StackOverflow (SO) for too many requests in a minute. Around 100 software developers have had a hard time without SO.

The Scrapy shell works differently: it downloads your target web page and you can create your extraction logic on this copy. If you need to move to another page, you let the shell download it and you are good to write the next chunk of code.

Starting the shell is easy.

scrapy shell

You can pass along a \<url> parameter, which is your target URL.

For this book we will use https://www.sainsburys.co.uk/shop/gb/ groceries/meat-fish/:

scrapy shell https://www.sainsburys.co.uk/shop/gb/groceries/ meat-fish/

Alternatively, you can also fetch the URL when you open Scrapy’s shell without any, or with a different URL.

    >>> fetch('https://www.sainsburys.co.uk/shop/gb/groceries/ meat-fish/')

Now the shell has downloaded the web page behind the URL. This means two things: now you have access to the Meat & Fish page’s content and can try your extractors; and second, you have to download every page you want to use in the shell. Even though the second point sounds bad, it is not: getting other pages is made easy in Scrapy and therefore in the shell too.

In the shell you have access to a response object (just like in the parse method, which we will write later in this chapter), and with this response you can use the available selectors.

I don’t want to dig very deep into how to use the shell to prepare your scraper script. Therefore, we will do one example: we get the URLs to the next page. This will give you a good start and the feel of using the shell for further preparation.

As you may remember, the links that lead to the detailed pages can be found in an unordered list (\<ul class="categories departments">). The list’s elements (\<li>) have an anchor child (\<a>), and the value of the href attribute of these anchors is the URL we are looking for.

To get the list of these URLs, you can write the following code using XPath:

    urls = response.xpath('//ul[@class="categories departments"]/ li/a/@href').extract()

Using CSS selectors, this would look like this:

    urls = response.css('ul.categories.departments > li > a::attr(href)').extract()

And that is it. You have all the URLs that lead to either product listings of the category or to a site containing more subcategories, just like in the previous chapter.

I suggest you dig a bit deeper into XPath and CSS selectors for now, to understand the extractor code that you will write starting with the next section.

### 3. def parse(self, response)

Now we are good to go to write the code in the basic.py file.

The parse method is the core of every spider. This method is called every time Scrapy downloads a URL, and most of the time you write your extraction code in this method.

The response argument holds the response from calling the URL. It can contain the website’s content but sometimes you can get back error codes, for example, when the website is down or nonexistent.

You can write a whole scraper into the parse method, but I suggest organizing your code into methods (and actually, this is the suggested practice of many developers). This helps you in the future to understand what the code wants to achieve.

Therefore, the parse function will be very sparse: it extracts only the URLs to the category pages (the same from the preparation with the shell), and initiates the download and parsing of those pages.

```
from scrapy import Request

# some code left out...

def parse(self, response):

urls = response.xpath('//ul[@class="categories departments"]/li/a/@href').extract()

for url in urls:

yield Request(url, callback=self.parse_department_ pages)
```

The preceding code extracts the href attributes of every anchor element of the list of the desired class. The interesting part is how the scraping is continued: you yield a new Request object with the target URL as the first parameter and the callback function that should be called if the server returns an OK-ish response for the given URL. In this case it will be the parse_department_pages method of this same class.

There’s an alternative way to get to the next page with writing less code.

```
def parse(self, response):

urls = response.xpath('//ul[@class="categories departments"]/li/a')

for url in urls:

yield response.follow(url, callback=self.parse_ department_pages)
```

Here we use the syntactic sugar of Scrapy: under the hood the same code is executed, but you don’t have to bother with extracting the exact reference from the anchor tags. And sometimes you don’t get a fully

qualified (absolute) URL in web page links but relative references, and you have to manually add the host (or use urljoin). By using response.follow you get this out of the box too. Therefore, I suggest you use this syntax, and I’ll use this in the book too!

Currently, as of version 1.4.0, you have to provide a single URL or Linktype object to the follow method. I bet that someone will add a method that accepts a list (for example follow_all) too, because we like make things easier.

With this, we are done with this section. Let’s move on and see how to get to the product pages.

At the end of this section, your basic.py file should look like this:

```
# -*- coding: utf-8 -*import scrapy

class BasicSpider(scrapy.Spider):

name = 'basic' allowed_domains = ['www.sainsburys.co.uk'] start_urls = ['https://www.sainsburys.co.uk/shop/gb/ groceries/meat-fish/']

def parse(self, response):

urls = response.xpath('//ul[@class="categories departments"]/li/a')

for url in urls:

yield response.follow(url, callback=self.parse_ department_pages)
```

### 4. Navigating Through Categories

Your first task is to navigate through the category pages of the Sainsbury’s website. You have seen in the previous chapter how complex it can get to find the page where the item details are.

As you have seen in the previous chapter, each category’s link can lead either to the product listing or to a page containing subcategories and their links, which can lead to either the product listing page or a third page with sub-subcategories. Fortunately, there is no deeper layering.

In this section we will handle the case wherin your code in the previous section resulted in a sub- or sub-subcategory page and not the product detail.

We sent requests with Scrapy in the previous section and told the tool to handle the responses with the parse_department_pages method.

To implement this method, we have to take care of the three versions of the response:

• We get a product listing page.

• We get a sub-category page.

• We get a sub-sub-category page.

If the response is a product listing, the idea is to forward the response to the next section’s method. However, we must take care of triggering the requests. The resulting block will look like this one:

product_grid = response.xpath('//ul[@class="productLister gridView"]')

if product_grid:

for product in self.handle_product_listings(response):

yield product

In the preceding code, we call the handle_product_listings method with the response object. We could provide the product grid too (or just the grid) because we have it already extracted but, as you will see later, we need the response to navigate between the pages of the product grid.

Then we yield the result, which is the trigger for Scrapy to scrape these URLs too.

The next step is to get through the deeper layers of categories, which are represented by CSS classes like aisles (class="category aisles") and shelves (class="category shelves")—just like in your supermarket.

The trick here is to check if the page’s source contains shelves and if not, then go for aisles. This is because a page containing shelves contains aisles too, and if you get the aisles links first you can end up in a neverending circle of getting the same pages over and over again if you don’t use caching. And getting the same pages means slower scraping (actually, never ending) and a lot of duplicate items in your scraping result.

pages = response.xpath('//ul[@class="categories shelf"]/li/a') if not pages:

pages = response.xpath('//ul[@class="categories aisles"] /li/a') if not pages:

# here is something fishy return

for url in pages:

yield response.follow(url, callback=self.parse_department_ pages)

The preceding code follows the approach mentioned previously: it looks for shelves and if they are not found, it looks for aisles. If nothing is found, then we are at a page from which we cannot gather more information: we have extracted the links to the product listings or there are no links to aisles or shelves on the page.

At the end of this section, your basic.py file should look something like this:

# -*- coding: utf-8 -*import scrapy

class BasicSpider(scrapy.Spider):

name = 'basic' allowed_domains = ['www.sainsburys.co.uk'] start_urls = ['https://www.sainsburys.co.uk/shop/gb/ groceries/meat-fish/']

def parse(self, response):

urls = response.xpath('//ul[@class="categories departments"]/li/a')

for url in urls:

yield response.follow(url, callback=self.parse_ department_pages)

def parse_department_pages(self, response):

product_grid = response.xpath('//ul[@class="product Lister gridView"]') if product_grid:

for product in self.handle_product_listings

(response):

yield product

pages = response.xpath('//ul[@class="categories shelf"]/li/a') if not pages:

pages = response.xpath('//ul[@class="categories

aisles"]/li/a') if not pages:

# here is something fishy

return

for url in pages:

yield response.follow(url, callback=self.parse_ department_pages)

Navigating Through the Product Listings

Now your code leads at some point to a product listing page. In this section we will navigate through these pages if they have too many elements to display on one page, and we will request a download for the detailed item pages.

We are currently in the handle_product_listings function. Let’s start with the item details.

urls = response.xpath('//ul[@class="productLister gridView"] //li[@class="gridItem"]//h3/a') for url in urls:

yield response.follow(url, callback=self.parse_product_detail)

The preceding code extracts the URLs to the detailed pages, and these URLs are then returned to the parse_department_pages method where their scraping is triggered.

next_page = response.xpath('//ul[@class="pages"]/li [@class="next"]/a') if next_page:

yield response.follow(next_page, callback=self.handle_ product_listings)

This code looks for the link to the next page. If one is found (on the website, it’s under the > symbol) then it is returned to the parse_ department_pages method. Note here the callback method: Because we know that we get another page of product listing, we can use the same method as a callback.

After finishing this section, your basic.py file should look like this:

# -*- coding: utf-8 -*import scrapy

class BasicSpider(scrapy.Spider):

name = 'basic' allowed_domains = ['www.sainsburys.co.uk'] start_urls = ['https://www.sainsburys.co.uk/shop/gb/ groceries/meat-fish/']

def parse(self, response):

urls = response.xpath('//ul[@class="categories departments"]/li/a')

for url in urls:

yield response.follow(url, callback=self.parse_ department_pages)

def parse_department_pages(self, response):

product_grid = response.xpath('//ul[@ class="productLister gridView"]') if product_grid:

for product in self.handle_product_ listings(response):

yield product

pages = response.xpath('//ul[@class="categories shelf"]/li/a') if not pages:

pages = response.xpath('//ul[@class="categories

aisles"]/li/a') if not pages:

# here is something fishy

return

for url in pages:

yield response.follow(url, callback=self.parse_ department_pages)

117 ChapTer 4

Using sCrapy

def handle_product_listings(self, response):

urls = response.xpath('//ul[@class="productLister

gridView"]//li[@class="gridItem"]//h3/a')

for url in urls:

yield response.follow(url, callback=self.parse_ product_detail)

next_page = response.xpath('//ul[@class="pages"]/li [@class="next"]/a') if next_page:

yield response.follow(next_page, callback=self. handle_product_listings)

### 5. Extracting the Data

Now that your code can handle the complex navigation and find the item details page, it’s time to extract the required information from the website.

We are currently in the parse_product_detail method.

Now it is time to extract all the required information from the item page. Actually, this process is the same as you did in the previous chapter (if you coded along): you can use the queries; however, you can save some lines of code on validating every find or find_all call.

Without talking too much, let’s jump into the code.

if you want, you can put down the book and implement the extraction logic. it is not hard, and you can use the information from the previous two chapters to go with.

My solution looks like this (yours may differ):

def parse_product_detail(self, response):

product_name = response.xpath('//h1/text()').extract()[0]. strip()

product_image = response.urljoin(response.xpath('//div [@id="productImageHolder"]/img/@src').extract()[0])

price_per_unit = response.xpath('//div[@

class="pricing"]/p[@class="pricePerUnit"]/text()').

extract()[0].strip() units = response.xpath('//div[@class="pricing"]/span [@class="pricePerUnitUnit"]').extract() if units:

unit = units[0].strip()

ratings = response.xpath('//label[@class="number OfReviews"]/img/@alt').extract() if ratings:

rating = ratings[0] reviews = response.xpath('//label[@class="number OfReviews"]').extract() if reviews:

reviews = reviews_pattern.findall(reviews[0])

if reviews:

product_reviews = reviews[0]

item_code = item_code_pattern.findall(response.xpath('//p [@class="itemCode"]/text()').extract()[0].strip())[0]

nutritions = {} for row in response.xpath('//table[@class="nutrition Table"]/tr'):

th = row.xpath('./th/text()').extract() if not th:

th = ['Energy kcal']

td = row.xpath('./td[1]/text()').extract()[0] nutritions[th[0]] = td

119 ChapTer 4

Using sCrapy

product_origin = ' '.join(response.xpath(

'.//h3[@class="productDataItemHeader" and text()= "Country of Origin"]/following-sibling::div[1]/p/ text()').extract())

And that is it. Extracting information on a product takes up to 30 lines of code (with my custom formatting settings). And this is just great!

As you can see in the code, there are some interesting code blocks. For example, every xpath call returns a list, even if you know there has to be at most one result. And some of those lists are empty because the product doesn’t have ratings or unit information. As with Beautiful Soup, you must handle such cases with Scrapy too.

After this section, your basic.py file should look something like this:

# -*- coding: utf-8 -*import scrapy

reviews_pattern = re.compile("Reviews \((\d+)\)") item_code_pattern = re.compile("Item code: (\d+)")

class BasicSpider(scrapy.Spider):

name = 'basic' allowed_domains = ['www.sainsburys.co.uk'] start_urls = ['https://www.sainsburys.co.uk/shop/gb/ groceries/meat-fish/']

def parse(self, response):

urls = response.xpath('//ul[@class="categories departments"]/li/a')

for url in urls:

yield response.follow(url, callback=self.parse_ department_pages)

120 ChapTer 4

Using sCrapy

def parse_department_pages(self, response):

product_grid = response.xpath('//ul[@class="product Lister gridView"]') if product_grid:

for product in self.handle_product_listings

(response):

yield product

pages = response.xpath('//ul[@class="categories shelf"]/li/a') if not pages:

pages = response.xpath('//ul[@class="categories

aisles"]/li/a') if not pages:

# here is something fishy

return

for url in pages:

yield response.follow(url, callback=self.parse_ department_pages)

def handle_product_listings(self, response):

urls = response.xpath('//ul[@class="productLister

gridView"]//li[@class="gridItem"]//h3/a')

for url in urls:

yield response.follow(url, callback=self.parse_ product_detail)

next_page = response.xpath('//ul[@class="pages"]/li[ @class="next"]/a') if next_page:

yield response.follow(next_page, callback=self. handle_product_listings)

121 ChapTer 4

Using sCrapy

def parse_product_detail(self, response):

product_name = response.xpath('//h1/text()').extract() [0].strip() product_image = response.urljoin(response.xpath('// div[@id="productImageHolder"]/img/@src').extract()[0])

price_per_unit = response.xpath('//div[@

class="pricing"]/p[@class="pricePerUnit"]/text()').

extract()[0].strip() units = response.xpath('//div[@class="pricing"]/span [@class="pricePerUnitUnit"]').extract() if units:

unit = units[0].strip()

ratings = response.xpath('//label[@class="number OfReviews"]/img/@alt').extract() if ratings:

rating = ratings[0] reviews = response.xpath('//label[@class="number OfReviews"]').extract() if reviews:

reviews = reviews_pattern.findall(reviews[0])

if reviews:

product_reviews = reviews[0]

item_code = item_code_pattern.findall(response.

xpath('//p[@class="itemCode"]/text()').extract()[0].

strip())[0]

nutritions = {} for row in response.xpath('//table[@class="nutrition Table"]/tr'):

th = row.xpath('./th/text()').extract()

122 ChapTer 4

Using sCrapy

if not th:

th = ['Energy kcal']

td = row.xpath('./td[1]/text()').extract()[0] nutritions[th[0]] = td

product_origin = ' '.join(response.xpath(

'.//h3[@class="productDataItemHeader" and text()="Country of Origin"]/followingsibling::div[1]/p/text()').extract())

Where to Put the Data?

OK: you have followed along, implemented the product extractor, and you have a lot of variables in your spider that contain the information for the project, but where to store them?

With Scrapy, you have to store data in so-called items. These items are plain old Python classes and can be found in the items.py file. Besides this, these items behave as dictionaries: you declare them as Python classes and can fill them like dictionaries using a key-value assignment.

If you have run your spider after the previous step, you might have seen entries in the console like this one:

2018-02-11 11:06:03 [scrapy.extensions.logstats] INFO: Crawled 47 pages (at 47 pages/min), scraped 0 items (at 0 items/min)

Here you can see that there were no items scraped. We will fix this now. Let’s adapt the parse_product_detail method to put the data into an item. To do this, first of all we need an item, which is already there in the items.py file.

class SainsburysItem(scrapy.Item):

# define the fields for your item here like: # name = scrapy.Field() pass

123 ChapTer 4

Using sCrapy

This class is currently empty; we must add fields to it. Because I don’t like to write scrapy.Field() every time (even if it is just copy+paste), I like to do “static” imports (from scrapy import Item, Field).

My solution looks like this; yours may differ, depending on how you named your fields.

class SainsburysItem(Item):

url = Field() product_name = Field() product_image = Field() price_per_unit = Field() unit = Field() rating = Field() product_reviews = Field() item_code = Field() nutritions = Field() product_origin = Field()

The only thing I changed is the nutritions field: I didn’t add all the possible fields to the item definition. This makes writing the file easier and exporting to JSON (see later) more convenient.

A flat (a.k.a. all fields included) class would look like this:

class FlatSainsburysItem(Item): url = Field() product_name = Field() product_image = Field() price_per_unit = Field() unit = Field() rating = Field() product_reviews = Field() item_code = Field() product_origin = Field()

124 ChapTer 4

Using sCrapy

energy = Field() energy_kj = Field() kcal = Field() fibre_g = Field() carbohydrates_g = Field() of_which_sugars = Field() ...

As you can see, the problem with this approach will come in the code: for the nutrition table you get strings as keys and you have to map them to these field names. This makes things complicated. Besides this, there are over 70 different fields that you must map.

I don’t think it useful to include such mapping code here. If you are interested, you can give it a try, but it is not a requirement of this book or website scraping in general.

When we export the results to files later in this chapter, we will take a closer look at how fields containing dictionaries are exported by default and what we can do to get the same results as in Chapter 2.

Now to add and use items, you have to adapt the parse_product_ detail method like this:

def parse_product_detail(self, response):

item = SainsburysItem() item['url'] = response.url item['product_name'] = response.xpath('//h1/text()'). extract()[0].strip() item['product_image'] = response.urljoin(

response.xpath('//div[@id="productImageHolder"]/img/

@src').extract()[0])

item['price_per_unit'] = response.xpath('//div[@class=

"pricing"]/p[@class="pricePerUnit"]/text()').extract()

[0].strip() units = response.xpath('//div[@class="pricing"]/span [@class="pricePerUnitUnit"]').extract()

125 ChapTer 4

Using sCrapy

if units:

item['unit'] = units[0].strip()

ratings = response.xpath('//label[@class="number OfReviews"]/img/@alt').extract() if ratings:

item['rating'] = ratings[0] reviews = response.xpath('//label[@class="number OfReviews"]').extract() if reviews:

reviews = reviews_pattern.findall(reviews[0])

if reviews:

item['product_reviews'] = reviews[0]

item['item_code'] = \

item_code_pattern.findall(response.xpath('//p[@class= "itemCode"]/text()').extract()[0].strip())[0]

nutritions = {} for row in response.xpath('//table[@class="nutrition Table"]/tr'):

th = row.xpath('./th/text()').extract() if not th:

th = ['Energy kcal']

td = row.xpath('./td[1]/text()').extract()[0] nutritions[th[0]] = td item['nutritions'] = nutritions

item['product_origin'] = ' '.join(response.xpath(

'.//h3[@class="productDataItemHeader" and text()="Country of Origin"]/followingsibling::div[1]/p/text()').extract())

yield item

126 ChapTer 4

Using sCrapy

This involves defining the new item (add the import to the file: from sainsburys.items import SainsburysItem) and then use it like a dictionary. I used the variable names from the previous version as the Field names in my item definition, but it is up to you how to name your fields. You just must find the right mapping.

Finally, you must yield the item, which makes Scrapy know there’s an item to handle.

The current state of the spider can be found in the folder 02_basic_ spider among the sources of this chapter.

Why Items?

Good question! Because items are dictionary-like objects; alternatively, you can use dictionaries to store your information.

item = {} This doesn’t result in any difference in coding or handling results, although Scrapy’s items hold some extended information that some components use. For example, exporters look at which fields to export, serialization can be customized by Items metadata, and you can use them to find memory leaks.

You will see later in this chapter that sometimes it is convenient to use a simple dictionary instead of an item. But for now, you should use items.

Running the Spider

Now it is time to start our spider, because we finished the extractor methods and added the items to export.

To start the spider, execute

scrapy crawl basic

127 ChapTer 4

Using sCrapy

from your crawler-projects main folder (where the scrapy.cfg file is located). In my case, this is

C:\wswp\chapter_4\sainsburys

Depending on your logging configuration, you either see something similar to this:

018-02-11 13:52:20 [scrapy.utils.log] INFO: Scrapy 1.5.0 started (bot: sainsburys) 2018-02-11 13:52:20 [scrapy.utils.log] INFO: Versions: lxml

4.1.1.0, libxml2 2.9.5, cssselect 1.0.3, parsel 1.4.0, w3lib

1.19.0, Twisted 17.9.0, Python 3.6.3 (v3.6.3:2c5fed8, Oct 3 2017, 18:11:49) [MSC v.1900 64 bit (AMD64)], pyOpenSSL 17.5.0 (OpenSSL 1.1.0g 2 Nov 2017), cryptography 2.1.4, Platform Windows-10-10.0.16299-SP0 2018-02-11 13:52:20 [scrapy.crawler] INFO: Overridden settings: {'BOT_NAME': 'sainsburys', 'CONCURRENT_REQUESTS': 1, 'LOG_ LEVEL': 'INFO', 'NEWSPIDER_MODULE': 'sainsburys.spiders', 'ROBOTSTXT_OBEY': True, 'SPIDER_MODULES': ['sainsburys. spiders'], 'USER_AGENT': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/63.0.3239.84 Safari/537.36'} 2018-02-11 13:52:20 [scrapy.middleware] INFO: Enabled extensions:

['scrapy.extensions.corestats.CoreStats', 'scrapy.extensions.telnet.TelnetConsole', 'scrapy.extensions.logstats.LogStats'] 2018-02-11 13:52:20 [scrapy.middleware] INFO: Enabled downloader middlewares: ['scrapy.downloadermiddlewares.robotstxt.RobotsTxtMiddleware', 'scrapy.downloadermiddlewares.httpauth.HttpAuthMiddleware',

128 ChapTer 4

Using sCrapy

'scrapy.downloadermiddlewares.downloadtimeout. DownloadTimeoutMiddleware', 'scrapy.downloadermiddlewares.defaultheaders. DefaultHeadersMiddleware', 'scrapy.downloadermiddlewares.useragent.UserAgentMiddleware', 'scrapy.downloadermiddlewares.retry.RetryMiddleware', 'scrapy.downloadermiddlewares.redirect.MetaRefreshMiddleware', 'scrapy.downloadermiddlewares.httpcompression. HttpCompressionMiddleware', 'scrapy.downloadermiddlewares.redirect.RedirectMiddleware', 'scrapy.downloadermiddlewares.cookies.CookiesMiddleware', 'scrapy.downloadermiddlewares.httpproxy.HttpProxyMiddleware', 'scrapy.downloadermiddlewares.stats.DownloaderStats'] 2018-02-11 13:52:20 [scrapy.middleware] INFO: Enabled spider middlewares: ['scrapy.spidermiddlewares.httperror.HttpErrorMiddleware', 'scrapy.spidermiddlewares.offsite.OffsiteMiddleware', 'scrapy.spidermiddlewares.referer.RefererMiddleware', 'scrapy.spidermiddlewares.urllength.UrlLengthMiddleware', 'scrapy.spidermiddlewares.depth.DepthMiddleware'] 2018-02-11 13:52:20 [scrapy.middleware] INFO: Enabled item pipelines:

[] 2018-02-11 13:52:20 [scrapy.core.engine] INFO: Spider opened 2018-02-11 13:52:20 [scrapy.extensions.logstats] INFO: Crawled 0 pages (at 0 pages/min), scraped 0 items (at 0 items/min) 2018-02-11 13:53:20 [scrapy.extensions.logstats] INFO: Crawled 220 pages (at 220 pages/min), scraped 205 items (at 205 items/min) 2018-02-11 13:54:20 [scrapy.extensions.logstats] INFO: Crawled 442 pages (at 222 pages/min), scraped 416 items (at 211 items/min)

129 ChapTer 4

Using sCrapy

2018-02-11 13:55:20 [scrapy.extensions.logstats] INFO: Crawled 666 pages (at 224 pages/min), scraped 630 items (at 214 items/min) 2018-02-11 13:56:20 [scrapy.extensions.logstats] INFO: Crawled 883 pages (at 217 pages/min), scraped 834 items (at 204 items/min) ...

2018-02-11 14:12:20 [scrapy.extensions.logstats] INFO: Crawled 4525 pages (at 257 pages/min), scraped 4329 items (at 246 items/min) 2018-02-11 14:13:01 [scrapy.core.engine] INFO: Closing spider (finished) 2018-02-11 14:13:01 [scrapy.statscollectors] INFO: Dumping Scrapy stats:

{'downloader/request_bytes': 11644228,

'downloader/request_count': 4720, 'downloader/request_method_count/GET': 4720, 'downloader/response_bytes': 72337636, 'downloader/response_count': 4720, 'downloader/response_status_count/200': 4718, 'downloader/response_status_count/302': 1, 'downloader/response_status_count/404': 1, 'finish_reason': 'finished', 'finish_time': datetime.datetime(2018, 2, 11, 13, 13, 1, 337489), 'item_scraped_count': 4515, 'log_count/INFO': 27, 'offsite/domains': 1, 'offsite/filtered': 416, 'request_depth_max': 13, 'response_received_count': 4719, 'scheduler/dequeued': 4719, 'scheduler/dequeued/memory': 4719,

130 ChapTer 4

Using sCrapy

'scheduler/enqueued': 4719, 'scheduler/enqueued/memory': 4719, 'start_time': datetime.datetime(2018, 2, 11, 12, 52, 20, 860026)} 2018-02-11 14:13:01 [scrapy.core.engine] INFO: Spider closed (finished)

or a lot more information buzzing through your screen. This is because of the default logging level. If you don’t set it explicitly to INFO, you get all information Scrapy-developers thought useful. And one portion of this information is the item that was gathered. It is good to see on the console which items are processed, but for more than 3,000 entries this generates a lot of unwanted output.

These first lines of the prcedimg output tell you what configuration runs Scrapy. Here you can see the middlewares, pipelines, extensions, and all the important stuff to analyze if you encounter strange results.

2018-02-11 13:53:20 [scrapy.extensions.logstats] INFO: Crawled 220 pages (at 220 pages/min), scraped 205 items (at 205 items/min)

Over time, a new line like the preceding one pops up on the screen. This tells you the current progress: how many pages are scraped, how many items are extracted, and how fast the scraping is. These numbers vary on your settings: if you increase the concurrent requests and decrease the delay between requests, this will get faster (depending on the target website, of course). If you find such statistics annoying, you can disable them by adding the following to your spider’s settings.py:

EXTENSIONS = { 'scrapy.extensions.logstats.LogStats': None }

131 ChapTer 4

Using sCrapy

When the scraping is done, you will see a similar summary to this:

2018-02-11 14:13:01 [scrapy.core.engine] INFO: Closing spider (finished) 2018-02-11 14:13:01 [scrapy.statscollectors] INFO: Dumping Scrapy stats:

{'downloader/request_bytes': 11644228, 'downloader/request_count': 4720, 'downloader/request_method_count/GET': 4720, 'downloader/response_bytes': 72337636, 'downloader/response_count': 4720, 'downloader/response_status_count/200': 4718, 'downloader/response_status_count/302': 1, 'downloader/response_status_count/404': 1, 'finish_reason': 'finished', 'finish_time': datetime.datetime(2018, 2, 11, 13, 13, 1, 337489), 'item_scraped_count': 4515, 'log_count/INFO': 27, 'offsite/domains': 1, 'offsite/filtered': 416, 'request_depth_max': 13, 'response_received_count': 4719, 'scheduler/dequeued': 4719, 'scheduler/dequeued/memory': 4719, 'scheduler/enqueued': 4719, 'scheduler/enqueued/memory': 4719, 'start_time': datetime.datetime(2018, 2, 11, 12, 52, 20, 860026)} 2018-02-11 14:13:01 [scrapy.core.engine] INFO: Spider closed (finished)

In these statistic dumps you can find the summary of the whole scraping process: requests, errors, different HTTP codes, number of items scraped, memory usage, and many other useful things. This can give you

132 ChapTer 4

Using sCrapy

ideas about where to enable extensions (for example finding which outside domains were triggered or which page wasn’t found).

Download finished in 20 minutes. This is way better than the run using my basic scraper from Chapter 3 (I let it run prior to this run and it took 4,009 seconds). And we didn’t have to write so much code.

Exporting the Results

Now you have the extracted data, you have the items representing the information, but the results are gone as soon as the spider finishes, and the Python process is gone from the memory of your computer.

Fortunately, Scrapy offers you built-in solutions, but they are very basic (you can call them primitive). But there’s a way to plug in your custom solution and make the scraper behave.

In this section we will first explore the built-in options and see if they’re really so primitive. Then we will take a look at how to shape the export to our needs—and yes, this requires writing some code.

Because Scrapy knows that scraping results in saving extracted information, it doesn’t require you to configure the exporter pipeline. You can tell Scrapy to export the scraped results easily via the command-line using the -o option. From this, Scrapy will figure out what type of file you want to save if you provide the right file-extension (.csv for CSV, .json for JSON), or you can add the -t option too and tell in what format you want the data in your specified output file (the value provided with -t has to be a valid feed exporter—more on those later).

The only problem I encountered with these default exporters is that they append the results to the file: if the file doesn’t exist, there’s no problem. However, if the file exists and has contents (for example from a previous run) then the new data is simply appended to the file, resulting in invalid content.

Besides the JSON and CSV exporters I will discuss in the next section, you can export your items in XML, Pickle, or Marshal format. They are done with built-in item exporters and use already provided functionality.

133 ChapTer 4

To CSV

Using sCrapy

The first approach is to export everything to CSV. As you can see in the previous paragraph, you simply have to run the spider with the -o option providing a CSV file.

scrapy crawl basic -o sainsburys.csv

If the scraper is finished, you can open the sainsburys.csv file and look at its contents.

item_code,nutritions,price_per_unit,product_image,product_ name,product_origin,product_reviews,rating,unit,url 7906825,"{'Energy ': '762kJ/', 'Fat ': '9.8g', 'Saturates': '3.5g', 'Carbohydrates': '6.6g', 'Sugars': '3.5g', 'Protein ': '16g', 'Salt ': '1.71g'}",£3.00,https://www.sainsburys. co.uk/wcsstore7.25.53/ExtendedSitesCatalogAssetStore/images/ catalog/productImages/23/5060084344723/5060084344723_L. jpeg,Black Farmer Reduced Fat Sausages 400g,,0,0.0,,https:// www.sainsburys.co.uk/shop/ProductDisplay?storeId=10151&product Id=1200360&urlRequestType=Base&categoryId=352852&catalogId=1019 4&langId=44

Note For Windows users, you may encounter extra blank lines in your file. This is because of a currently open bug in Scrapy but the main reason is in the line-ending differences between the operating systems. There’s already a pull-request at github 5 when i’m writing this; it has been merged and i hope it’s available with the next released Scrapy version.

5 https://github.com/scrapy/scrapy/pull/3039

134 ChapTer 4

Using sCrapy

Because each line has a lot of content, I don’t want to list more here. But you can already see the interesting part: the nutrition column (in my example the second column). It has curly braces ({}) with the nutrition dictionary written out as text. This is not good; therefore, we will implement a custom item exporter to handle this case.

To JSON

Exporting to JSON works similar to CSV: you provide a JSON file as output.

scrapy crawl basic -o sainsburys.json

The result is a JSON file containing entries like this one:

{

"url": "https://www.sainsburys.co.uk/shop/ProductDisplay?store Id=10151&productId=1200360&urlRequestType=Base&categoryId=352 852&catalogId=10123&langId=44", "product_name": "Black Farmer Reduced Fat Sausages 400g", "product_image": "https://www.sainsburys.co.uk/ wcsstore7.25.53/ExtendedSitesCatalogAssetStore/images/ catalog/productImages/23/5060084344723/5060084344723_L.jpeg", "price_per_unit": "\u00a33.00", "rating": "0.0", "product_reviews": "0", "item_code": "7906825", "nutritions": {

"Energy ": "762kJ/", "Fat ": "9.8g", "Saturates": "3.5g", "Carbohydrates": "6.6g", "Sugars": "3.5g", "Protein ": "16g",

135 ChapTer 4

Using sCrapy

"Salt ": "1.71g" }, "product_origin": ""

}

Using JSON, the nutrition dictionary fits great into the exported result. The keys could use a bit of tidying, but for now the structure looks great.

There’s a little flaw in there: those nasty Unicode characters. To fix this, add the following line to your settings.py file:

FEED_EXPORT_ENCODING = 'utf-8'

After running the scraper again, the same entry looks like this:

{

"url": "https://www.sainsburys.co.uk/shop/ProductDisplay?store Id=10151&productId=1200360&urlRequestType=Base&categoryId=276 041&catalogId=10172&langId=44", "product_name": "Black Farmer Reduced Fat Sausages 400g", "product_image": "https://www.sainsburys.co.uk/ wcsstore7.25.53/ExtendedSitesCatalogAssetStore/images/ catalog/productImages/23/5060084344723/5060084344723_L.jpeg", "price_per_unit": "£3.00", "rating": "0.0", "product_reviews": "0", "item_code": "7906825", "nutritions": {

"Energy ": "762kJ/", "Fat ": "9.8g", "Saturates": "3.5g", "Carbohydrates": "6.6g", "Sugars": "3.5g",

136 ChapTer 4

Using sCrapy

"Protein ": "16g", "Salt ": "1.71g" }, "product_origin": ""

}

As an alternative to whole JSON files, you can use JSON-lines. This format exports every item as a single JSON object, which enables handling a large amount of data because you don’t have to load everything into memory and put it together into a megaobject to write to a file—or be read by your target platform.

Scrapy has a built-in exporter for this result type too, and you can access it with the following command:

scrapy crawl basic -o sainsburys.jl

If you look at your file system while running the spiders, you will see that JSON-lines files are written to the disk as soon as they’re processed by the item pipelines! You don’t have to wait till the scraping is done to get a valid file.

To Databases

Well, for databases there’s no out of the box solution; you cannot add an extra parameter to the command line to write your results into a database.

If you want your data stored in a database, then you have to write your own solution. However, because storing in a database is a use-case I often encounter, I wanted to add it into this section and not in the next one when I write about bringing your own exporter.

We will take a look at two different types of databases: MongoDB and SQLite. They represent the approach to the majority of databases currently in use, although other cloud-based storage solutions are rising, but most of the clients are still using these types of databases.

137 ChapTer 4

Using sCrapy

MongoDB

First let’s go and create the item pipeline.

import pymongo

class MongoDBPipeline(object):

def __init__(self, mongo_uri, mongo_db, collection_name):

self.mongo_uri = mongo_uri self.mongo_db = mongo_db self.collection_name = collection_name

@classmethod def from_crawler(cls, crawler):

return cls( mongo_uri=crawler.settings.get('MONGO_URI'), mongo_db=crawler.settings.get('MONGO_DATABASE', 'items'), collection_name=crawler.settings.get('MONGO_ COLLECTION', 'sainsburys') )

def open_spider(self, spider):

self.client = pymongo.MongoClient(self.mongo_uri) self.db = self.client[self.mongo_db]

def close_spider(self, spider):

self.client.close()

def process_item(self, item, spider):

self.db[self.collection_name].insert_one(dict(item)) return item

138 ChapTer 4

Using sCrapy

The idea while using any database is that you need a connection to the target database and you must clean up after you are finished. The pipeline above does this.

open_spider is called every time the spider is started, when the scrape starts. close_spider is called when the spider finishes its work and is dismissed. And these are the two methods where you have to open and close the connection to the database.

process_item processes the item, and in this case this item is stored in the database.

But the most interesting method is the from_crawler. If present, it has to return a new instance of the pipeline. The crawler provided to the method should be used to access the crawler-specific settings. In the case of the example, we get the connection, database, and collection settingswhere the last two have default values and you don’t have to provide them.

To have your pipeline working, you have to configure it in settings.py.

ITEM_PIPELINES = { 'sainsburys.pipelines.MongoDBPipeline': 300 }

Then you need to provide the database configuration. You can do it either in the settings.py file (which makes the configuration hard-coded):

MONGO_URI = 'localhost:27017'

or you can provide it through the command line when starting the spider:

scrapy crawl basic -s MONGO_URI=localhost:27017

Because we’re using pymongo, we don’t even have to provide the database URI. In such cases, pymongo creates a default connection to localhost:27017.

139 ChapTer 4

Using sCrapy

After running the spider, we can see the results in the database, as shown in Figure 4-2.

Figure 4-2. The same item as previously—now in MongoDB

you can find a spider using MongoDB to store the extracted information in the folder 03_mongodb among the sources for this chapter.

SQLite

Similar to the MongoDB solution, when using a SQLite database, you have to open and close the connection when the spider is started and finished, respectively.

Because handling the nutrition table gets too complex (with the 70 fields, which could be reduced), i won’t implement this part of the export. if you’re interested and want to give it a try, don’t feel intimidated by my approach!

140 ChapTer 4

Using sCrapy

First, I defined the table DDL and the insert statement.

sqlite_ddl = """ CREATE TABLE IF NOT EXISTS {} (

item_code INTEGER PRIMARY KEY, product_name TEXT NOT NULL, url TEXT NOT NULL, product_image TEXT, product_origin TEXT, price_per_unit TEXT, unit TEXT, product_reviews INTEGER, rating REAL

) """

sqlite_insert = """ INSERT OR REPLACE INTO {} values (?, ?, ?, ?, ?, ?, ?, ?, ?) """

Then I’ve written the code.

class SQLitePipeline:

def __init__(self, database_location, table_name): self.database_location = database_location self.table_name = table_name self.db = None

@classmethod def from_crawler(cls, crawler):

return cls( database_location=crawler.settings.get('SQLITE_ LOCATION'),

141 ChapTer 4

Using sCrapy

table_name=crawler.settings.get('SQLITE_TABLE', 'sainsburys'),

)

def open_spider(self, spider):

self.db = sqlite3.connect(self.database_location) self.db.execute(sqlite_ddl.format(self.table_name))

def close_spider(self, spider): if self.db: self.db.close()

def process_item(self, item, spider):

if type(item) == SainsburysItem:

self.db.execute(sqlite_insert.format(self.table_ name), ( item['item_code'], item['product_name'], item['url'], item['product_ image'], item['product_origin'], item['price_per_unit'], item['unit'] if hasattr(item, 'unit') else None, int(item['product_reviews']) if hasattr(item, 'product_ reviews') else None, float(item['rating']) if hasattr(item, 'rating') else None

) )

self.db.commit()

142 ChapTer 4

Using sCrapy

As you can see, the class works almost the same as the MongoDB pipeline from the previous example. The interesting part comes when you insert it into the database. Because we have some nullable fields (and properties that don’t have to exist in the item), we have to ensure that we don’t encounter a Python error while saving.

To test out the code, you have to add the pipeline to settings.py.

ITEM_PIPELINES = { 'sainsburys.pipelines.MongoDBPipeline': None 'sainsburys.pipelines.SQLitePipeline': 300 }

Now you can run the application.

scrapy crawl basic -s SQLITE_LOCATION=sainsburys.db

Don’t forget to add the SQLite location with the -s settings flag. Without this you’ll get an exception.

you can find a spider using sQLite to store the extracted information in the folder 04_sqlite among the sources for this chapter.

Bring Your Own Exporter

This section is the most interesting if you followed along and think the default exporting solution doesn’t fit your needs.

Besides item pipelines (which we implemented for database connections), you can define your own feed exporters. These work like the built-in CSV, XML, and JSON exporters but adapted to your taste. In this section we will take a look at both approaches, even though you’ve already written two item pipelines for database storage.

143 ChapTer 4

Using sCrapy

You will now implement a CSV pipeline that will handle the nutritions field properly: instead of writing the whole dictionary as plain text, you will append the fields to the main content.

This requires you to store the extracted items in a cache just like with Beautiful Soup, because you cannot know the possible fields you may encounter in all the items. Remember: The website has multiple different nutrition tables that have more or less the same fields.

Filtering Duplicates

You remember the SQLite pipeline. There we defined INSERT OR REPLACE INTO when we saved an item into the database. This is because there are duplicate items that can be found from different pages on the website.

With SQLite you can easily overcome this problem, but with other exports you get too much data, and duplicates are never good. Sure, the postprocessing (your customer or data mining algorithm) can fix this, but why not you?

Because Scrapy is highly extensible, you will create a duplicate filter based on the item code.

from scrapy.exceptions import DropItem

class DuplicateItemFilter:

def __init__(self):

self.item_codes_seen = set()

def process_item(self, item, spider):

if item['item_code'] in self.item_codes_seen:

raise DropItem("Duplicate item found: %s" % item['item_code'])

self.item_codes_seen.add(item['item_code']) return item

144 ChapTer 4

Using sCrapy

The preceding code stores seen item codes in an internal set, and if the item code was seen already then it discards the item.

To enable this pipeline, add the following code to your settings.py file:

ITEM_PIPELINES { 'sainsburys.pipelines.DuplicateItemFilter': 1 }

Setting a low value for the pipeline ensures that duplicates are filtered as soon as they arrive, saving a lot of work for other tasks.

And you can use such filter pipeline items for every possible kind of filtering. If you don’t want an item to be present in the final export, then you can create a filter pipeline, add it to your settings.py, and it handles missing values.

Silently Dropping Items

If you add the item filter from the previous section and run your spider, you will see a lot of entries like this one:

2018-02-13 09:48:42 [scrapy.core.scraper] WARNING: Dropped: Duplicate item found: 7887890 {'image_urls': ['https://www.sainsburys.co.uk/wcsstore7.25.53/ ExtendedSitesCatalogAssetStore/images/catalog/productImages/74/ 0000000306874/0000000306874_L.jpeg'],

'item_code': '7887890', 'nutritions': {'Carbohydrate': '13.7g', 'Energy': '664kJ', 'Energy kcal': '158kcal', 'Fat': '6.0g', 'Fibre': '2.6g', 'Mono-unsaturates': '3.5g', 'Polyunsaturates': '1.5g',

145 ChapTer 4

Using sCrapy

'Protein': '11.1g', 'Salt': '0.91g', 'Saturates': '0.5g', 'Starch': '10.5g', 'Sugars': '3.2g'}, 'price_per_unit': '£2.50', 'product_image': 'https://www.sainsburys.co.uk/ wcsstore7.25.53/ExtendedSitesCatalogAssetStore/images/ catalog/productImages/74/0000000306874/0000000306874_L.jpeg', 'product_name': "Sainsbury's Mediterranean Tuna Fishcakes, Taste the " 'Difference 300g', 'product_origin': 'Produced in United Kingdom Produced using Yellowfin tuna ' 'caught by hooks and lines in the Western Indian Ocean, ' 'Eastern Indian Ocean, Western Central Pacific Ocean and ' 'Eastern Central Pacific Ocean', 'product_reviews': '4', 'rating': '2.0', 'url': 'https://www.sainsburys.co.uk/shop/gb/groceries/allfish-seafood/sainsburys-mediterranean-tuna-fishcakes--tastethe-difference-300g'}

One solution would be to raise the LOG_LEVEL to ERROR, but with this approach you end up skipping other warnings that can be useful in analyzing not expected behavior.

The other solution would be to write your own log-formatter for dropped items.

from scrapy import logformatter import logging

146 ChapTer 4

Using sCrapy

class SilentlyDroppedFormatter(logformatter.LogFormatter):

def dropped(self, item, exception, response, spider):

return { 'level': logging.DEBUG, 'msg': logformatter.DROPPEDMSG, 'args': { 'exception': exception, 'item': item, }

}

To use this formatter, you must enable it in the settings.py file.

LOG_FORMATTER = 'sainsburys.formatter.SilentlyDroppedFormatter'

you can find a spider using the duplicate item filter in the folder 05_item_filter among the sources for this chapter.

Fixing the CSV File

Do you remember what problem the currently exported CSV files have? Yes, they write the nutrition information as plain text into one column of the CSV file. This is not ideal.

Besides this, the order of the columns may vary between runs because they’re stored in a dictionary.6 

You will implement an item pipeline that stores every item during the scraping process and exports only when the spider finishes.

6 In the current version of Python, the dictionaries are ordered by their key per

default. This means every time you run your spider on the same 3.6 CPython implementation, the order of the columns will stay the same.

147 ChapTer 4

Using sCrapy

class CsvItemPipeline:

def __init__(self, csv_filename):

self.items = [] self.csv_filename = csv_filename

@classmethod def from_crawler(cls, crawler):

return cls( csv_filename=crawler.settings.get('CSV_FILENAME', 'sainsburys.csv'), )

def open_spider(self, spider):

pass

def close_spider(self, spider):

import csv with open(self.csv_filename, 'w', encoding='utf-8') as outfile:

spamwriter = csv.DictWriter(outfile, fieldnames=self. get_fieldnames(), lineterminator='\n') spamwriter.writeheader() for item in self.items:

spamwriter.writerow(item)

def process_item(self, item, spider):

if type(item) == SainsburysItem:

new_item = dict(item) new_item.pop('nutritions') new_item.pop('image_urls') self.items.append({**new_item, **item['nutritions']}) return item

148 ChapTer 4

Using sCrapy

def get_fieldnames(self):

field_names = set() for product in self.items:

field_names.update(product.keys()) return field_names

You can see that every processed item is converted to a new dictionary that contains all the fields of the original item, then nutritions and image_urls are removed, finally the original nutritions dictionary is added to this new item by combining the two dictionaries, and the result is stored in memory for later usage.

When the spider finishes, all the different field names are extracted from all the items and are used as the CSV header. The order still varies between Python installations. To fix the order (at least for the standard properties that are not nutrition information) you can define a base list of properties and then add the missing values—something like this:

class CsvItemPipeline:

fieldnames_standard = ['item_code', 'product_name',

'url', 'price_per_unit', 'unit', 'rating', 'product_ reviews','product_origin', 'product_image']

def get_fieldnames(self):

field_names = set() for product in self.items:

for key in product.keys():

if key not in self.fieldnames_standard: field_names.add(key) return self.fieldnames_standard + list(field_names)

As always, you can add this pipeline to your settings.py file.

ITEM_PIPELINES = { 'sainsburys.pipelines.CsvItemPipeline': 800, }

149 ChapTer 4

Using sCrapy

However, using this approach, the CSV file will be written every time you run the spider, even if you export into a different format or don’t want any export.

To solve this problem, let’s implement a feed exporter.

you can find a spider using this CsV item pipeline in the folder 06_csv_pipeline among the sources for this chapter.

CSV Item Exporter

Feed exports are similar to item pipelines, but you can write them in a general fashion and use them on-demand, without changing the settings.py file.

You already used feed exporters (an alternative name for item exporters) when you saved information to CSV, JSON, or JSON-lines files using the -o output file and Scrapy could derive the exporter to use, or you can provide the -t option and tell Scrapy which exporter you want to use. The following list contains the currently built-in feed exporters:

• csv: saves information as CSV

• json: saves information as JSON

• jsonlines: saves information as JSON-lines

• xml: saves information as XML

• pickle: saves information as Pickle data

• marshal: saves information in Marshal format, which is similar to Pickle (specific to Python) but doesn’t have any machine architectural issues

Because item exporters are similar to item pipelines, they process only one item at a time, we have to be tricky and save the items in memory just

150 ChapTer 4

Using sCrapy

like for the CsvItemPipeline class. Basically, we will reuse the already written code and rename some methods.

from scrapy.exporters import BaseItemExporter import io import csv

class CsvItemExporter(BaseItemExporter):

fieldnames_standard = ['item_code', 'product_name', 'url',

'price_per_unit', 'unit', 'rating', 'product_reviews', 'product_origin', 'product_image']

def __init__(self, file, **kwargs):

self._configure(kwargs) if not self.encoding:

self.encoding = 'utf-8'

self.file = io.TextIOWrapper(file, line_buffering=False, write_through=True, encoding=self.encoding) self.items = []

def finish_exporting(self):

spamwriter = csv.DictWriter(self.file, fieldnames=self.__get_fieldnames(), lineterminator='\n') spamwriter.writeheader() for item in self.items:

spamwriter.writerow(item)

def export_item(self, item):

new_item = dict(item) new_item.pop('nutritions')

151 ChapTer 4

Using sCrapy

new_item.pop('image_urls') self.items.append({**new_item, **item['nutritions']})

def __get_fieldnames(self):

field_names = set() for product in self.items:

for key in product.keys():

if key not in self.fieldnames_standard: field_names.add(key) return self.fieldnames_standard + list(field_names)

But item exporters have a problem: they don’t delete the file, they append to it. Fortunately, there is a solution: you can truncate the file to 0 bytes using the truncate() method. The extended constructor would look like this:

def __init__(self, file, **kwargs):

self._configure(kwargs) if not self.encoding:

self.encoding = 'utf-8'

self.file = io.TextIOWrapper(file, line_buffering=False, write_through=True, encoding=self.encoding) self.file.truncate(0) self.items = []

And again, we must add the item exporter to the settings.py to let Scrapy know that there’s another option you can use.

FEED_EXPORTERS = { 'mycsv': 'sainsburys.exporters.CsvItemExporter' }

152 ChapTer 4

Using sCrapy

Here you provided mycsv as the name of the feed exporter. This means, later you can call the spider using the -t option and mycsv as argument.

scrapy crawl basic -o mycsv.csv -t mycsv

you can find an example spider using the just-created feed exporter in the folder 07_csv_feed_exporter among the sources for this chapter.

Caching with Scrapy

Even though I think using caching is an advanced configuration option, I’ve added an extra section for this topic to cover. This is because it improves your execution time by multiple times, and once you cache the website locally you can tweak your scraper script as you wish without overloading the target server.

If you want to configure caching, for example while developing your scripts, there are some options in Scrapy. Naturally, you can write your own cache just like you did in the previous chapter but before you invest time, sweat, and brain cells into coding your cache, let’s see what is present, what can we utilize.

Scrapy offers caching. The default configuration disables caching; this means, every page is downloaded every time you request it. But as you know, there are a lot of knobs you can turn, and you can enable caching with the HTTPCACHE_ENABLED = True setting.

There are three HTTP cache options you can utilize out of the box:

• File system storage

• DBM storage

• LevelDB storage

153 ChapTer 4

Using sCrapy

And as always, you can write your own solution too; however, I consider this scenario unlikely, because 90% of use-cases can be covered with the built-in solutions.

My default caching configuration looks like this:

HTTPCACHE_ENABLED = True HTTPCACHE_EXPIRATION_SECS = 0 HTTPCACHE_DIR = 'httpcache' HTTPCACHE_IGNORE_HTTP_CODES = []

With this you can enable caching, and when you run your spider it stores every request-response pair on your file system in the .scrapy/ httpcache folder in your project’s directory, and from now on it uses this cache when you rerun your spider. This is ideal for tweaking your script: download a snapshot of the target website and use it for fine-tuning your item extraction.

If you have any HTTP response codes that you don’t want cached, you can add them in the HTTPCACHE_IGNORE_HTTP_CODES list, for example:

HTTPCACHE_IGNORE_HTTP_CODES = [503, 418]

Setting HTTPCACHE_EXPIRATION_SECS to 0 keeps files always in the cache. If you give it a positive value, older cached files are discarded. Note that this setting requires values in seconds!

Let’s see what caching has to offer!

Storage Solutions

In this section we will look at the different storage solutions Scrapy has to offer for caching. Out of the box you have the following options available:

• File System Storage

• DBM Storage

• LevelDB Storage

154 ChapTer 4

Using sCrapy

But because you can extend Scrapy easily, you can write your own storage solution (for example to use a custom database, like MongoDB).

If you ask me, I am fine with a file system–based solution. However, if you’re running on-demand (for example in the cloud or in a container environment), you may favor a remote caching service, which is most likely based on a database.

File System Storage

If you enable HTTP caching, this is the default solution used. Even though it’s the default, you can add the following line to your settings.py file:

HTTPCACHE_STORAGE = 'scrapy.extensions.httpcache. FilesystemCacheStorage'

Using this storage option, all requests and responses are downloaded and stored in a folder whose name is unique for this scraper and is 40 characters long. In these folders is all the information identifying the request and the response the middleware will need to identify pages that should be served from the cache.

DBM Storage

To activate the DBM7 storage, just add (or replace if it exists).

HTTPCACHE_STORAGE = 'scrapy.extensions.httpcache. DbmCacheStorage'

The default setting is to use the anydbm module, but you can change it using the HTTPCACHE_DBM_MODULE setting.

7 https://en.wikipedia.org/wiki/Dbm

155 ChapTer 4

Using sCrapy

LevelDB Storage

You can also use LevelDB 8 (a fast key-value storage) for your cache, but it is not encouraged in the development phase of your project because it allows only a single process to access the database at the same time. This is OK if you just run your spider, but if you want to have the Scrapy shell open for your project and run the spider you will end up with an error.

To use LevelDB you can change the HTTPCACHE_STORAGE to 'scrapy. extensions.httpcache.LeveldbCacheStorage' in the settings.py file and install LevelDB with the following command:

pip install leveldb

Cache Policies

Scrapy comes with two default policies for caching:

• Dummy policy

• RFC2616 policy

Dummy Policy

The Dummy policy is the default setting. Here, every request and its response are stored, and when the same request is seen again, the stored response is returned. This is useful if you are testing your spider and want to replay runs at the same.

Because this is the default policy, you don’t have to add anything to your project’s settings.py file.

8 https://github.com/google/leveldb

156 ChapTer 4

Using sCrapy

RFC2616 Policy

This policy is aware of cache-control settings and is aimed at production use to avoid downloading unchanged pages, save bandwidth, and speed-up crawls.

To enable this policy, add the following setting to your settings.py file:

HTTPCACHE_POLICY = scrapy.extensions.httpcache.RFC2616Policy What does aware of cache-control settings mean? It means that the scraper works according to the RFC2616 caching specification. If you are lazy and don’t want to read the whole specification, here is a small excerpt of what Scrapy can do for you:

• If the website provides a no-store response, Scrapy won’t try to store requests or responses.

• If the no-cache directive is set, Scrapy won’t return the response from the cache, even it is downloaded recently.

• It computes the current age from the Age or the Date headers.

• It computes the freshness lifetime from the max-age directive, the Expires, and the Last-Modified response headers.

However, when writing this book, some RFC2616 compliance requirements are not met, such as:

• Pragma: no-cache support

• Vary header support

• Invalidation after updates or deletes

157 ChapTer 4

Using sCrapy

Downloading Images

Even though this is not a requirement for our project, you will encounter many tasks where you must download images besides data. Fortunately, Scrapy has a built-in solution for this problem too.

For this section, let’s extend our requirements to gather images along with the items. These images will be saved on your file system besides your project files, but you can configure your spider to store the downloaded files at Amazon S3 or Google Cloud.

Because Scrapy uses Pillow for image resizing and thumbnail generation, you must install it before you can start gathering images.

pip install pillow

To get started, first add the following to your settings.py file:

ITEM_PIPELINES = { 'scrapy.pipelines.images.ImagesPipeline': 5 }

And you have to tell Scrapy where to save the downloaded images. I use the images folder inside the project.

IMAGES_STORE = 'images'

The folder you provide to IMAGES_STORE must exist.

The combination of those two settings activates the image pipeline, which downloads the files and stores them on your computer’s hard disk.

To get items into this pipeline, you must add

image_urls = Field() images = Field()

to your Item. This is because the ImagesPipeline works using the image_urls field and adds the resulting images to the images field.

158 ChapTer 4

Using sCrapy

In the case of the Sainsbury’s scraper, we must rename product_image to image_urls, add images in the SainsburysItem, and change the spider code to fill image_urls with a list instead of a URL.

item['image_urls'] = [response.urljoin(

response.xpath('//div[@id="productImageHolder"]/img/@src').

extract()[0])]

Now if you run your spider and save the results (for example using scrapy crawl basic -o images.jl), you will see the downloaded images in the images/full folder, similar to the one shown in Figure 4-3.

Figure 4-3. Images downloaded when Scrapy ran

159 ChapTer 4

Using sCrapy

The values in the images.jl file are inserted into the item’s images field. A sample value looks like this:

"images": [

{ "url": "https://www.sainsburys.co.uk/wcsstore7.25.53/ ExtendedSitesCatalogAssetStore/images/catalog/product Images/23/5060084344723/5060084344723_L.jpeg", "path": "full/4ae5a3a0dfa0fac7f3728d76b788716e8a2bc9fb.jpg", "checksum": "132512348d379f8365ca02082a16adf1" }

]

This tells you not only how the file is named on your file system and where it’s downloaded from, but you get a checksum too to verify that the image on your file system is really the same that Scrapy downloaded.

In the preceding example, the file can be found under images/full /4ae5a3a0dfa0fac7f3728d76b788716e8a2bc9fb.jpg and is shown in Figure 4-4.

Note you can find the sources for this section in the 08_image_pipeline folder among the sources for this chapter.

Figure 4-4. An example of a downloaded image

160 ChapTer 4

Using sCrapy

scrapy uses its own algorithm to generate the file names. This means you can encounter different file names than me if you run the spider on your computer.

Using Beautiful Soup with Scrapy

Sometimes you already have an HTML extractor ready, created with Beautiful Soup, and you don’t want to convert it to Scrapy code. Or you have a team member who is a pro at Beautiful Soup and she creates the extraction code; you only have to take care of configuring Scrapy.

In such cases you use the already existing code because you can integrate Beautiful Soup and Scrapy.

def parse_product_details_bs(self, response):

item = SainsburysItem()

from bs4 import BeautifulSoup soup = BeautifulSoup(response.text, 'lxml') h1 = soup.find('h1') if h1:

item['product_name'] = h1.text.strip()

In the preceding code you can see the integration of Beautiful Soup and Scrapy with a subset of the code from the previous chapter. I explicitly use lxml for speed while parsing but you can use any of the available parsers (and by the way, lxml is available out of the box when you install Scrapy).

With this information, you can rewrite the spider to use the functionality written in Chapter 3. You can find a sample solution in the 09_beautifulsoup folder among the sources for this chapter.

161 ChapTer 4

Using sCrapy

Logging

Sometimes you prefer to see custom messages in the console while scraping. This is useful if you cut back the log level of Scrapy to INFO but you want to see a little more of the current process.

Every spider comes with a logger, which you can access right in its methods. For example, logging the response’s URL would look like this:

self.logger.info("URL: %s", response.url)

The logger uses the same log levels that you configured in settings.py. If you don’t see a log output on the console, you can turn up the logging (decrease the level to DEBUG). If it still doesn’t show up, then you can be sure that the code is not reached while running.

If you want to do standard logging and not use the logger in your spider (for example because you are in a different file where you don’t have access to a spider), you can either use Scrapy’s log module (which is deprecated so you shouldn’t use it) or Python’s built-in logger module. There are no considerations; logger works the same way as it would in a “standard” Python application.

(A Bit) Advanced Configuration

Because there are a lot of knobs you can turn on your Scrapy project, I add a section to get you started and try out some different combinations.

This book has size limitations; therefore, I won’t list every setting you can toggle, but just the most used ones. For more settings, take a look at Scrapy’s documentation: https://doc.scrapy.org.

162 ChapTer 4

Using sCrapy

LOG_LEVEL

Working through this chapter gave you a lot of output while running the spider. However, you can restrict the information to a subset.

As a default, Scrapy uses the DEBUG log-level for its output. It logs you every bit of information you can get from the code, and most of the time this is too much.

However, you can restrict the log level in the settings.py file by adding the following line:

LOG_LEVEL = 'INFO'

This sets the log level to log only information, and warning and error messages. This is because of how logging levels work. Each has a priority, and with the log level setting you tell the application to “log the items with this priority and above.”

You can use the following list as a reference to the log-level priority:

1. CRITICAL

2. ERROR

3. WARNING

4. INFO

5. DEBUG

This list contains Scrapy’s log level settings. DEBUG is a good setting while developing, but in a running/live system I prefer INFO or sometimes WARNING as the log level. Depending on the developer, you get the right amount of information using this level.

163 ChapTer 4

Using sCrapy

CONCURRENT_REQUESTS

You have already seen this setting at the beginning of this chapter. As its name already tells you, you can limit the number of concurrent requests to one website.

Depending on the website, it makes sense to turn this number up a bit or stay with the default value. This is because network operations (downloading the website’s code) take time, and while the thread waits the process/application is hanging idle. In such cases, even with the GIL present, Python can execute multiple threads parallel, and therefore while your code is waiting for one page to load you can download more.

However, you cannot turn the knob forever. Your computer has its limits too, and having 16 or 160 concurrent requests doesn’t make a difference. I suggest you start with 1 request while developing, then use the default setting of 16. This is good for you because you get the required data faster, and this is good for the targeted website too because it’s not overwhelmed by you.

Moreover, sometimes it happens that the target website has request monitoring enabled. This means, requests and their interval are monitored and evaluated, and if your IP exceeds a threshold you get banned for a time from the website—sometimes forever. Therefore, be responsible with your configuration.

DOWNLOAD_DELAY

Accompanying the concurrent requests, you can set the delay between two downloads too. The download delay tells the spider how many seconds it should wait between downloading another page from the same domain or IP address (if CONCURRENT_REQUESTS_PER_IP is set to a nonzero positive number).

This configuration awaits seconds as value, but you can provide decimal values too.

DOWNLOAD_DELAY = 0.125 # 125 milliseconds

164 ChapTer 4

Using sCrapy

This setting is used to not hit the target servers too hard with your requests. Sometimes this setting is useful to avoid detection and mock human-like behavior.

Autothrottling

Previously, you have seen how to set hard download delays and concurrent requests, to act like a good citizen. However, with this approach you can end up with many requests waiting for completion if the server is busy. Or if the server starts to send back error messages, those are returned faster than 200 OK responses, which generate more requests per second because errors are handled faster by Scrapy. However, in case of errors, the scraper should send fewer requests to help the server to recover itself from its (hopefully temporary) failure state.

A solution, and an alternative approach, is to use Scrapy’s autothrottling feature. This is not enabled by default; you must enable it with the following setting:

AUTOTHROTTLE_ENABLED = True

What the algorithm behind this setting does is adjust the download delay based on the response times of the server. If the server is busy, it sends the responses later, and Scrapy adjusts the download delay to send requests less frequently. If the server has no difficulties, the download delay is reduced, and more requests are sent to the server. And most importantly: non-200-OK responses do not decrease the download delay.

You can configure some settings for autothrottling too. For example, setting

AUTOTHROTTLE_START_DELAY = 15

165 ChapTer 4

Using sCrapy

You tell Scrapy to wait 15 seconds initially between two requests. Based on the server’s response time, Scrapy can reduce or extend this waiting time. If the latency is big, Scrapy raises this delay. However, you can give it a maximum where it won’t wait longer.

AUTOTHROTTLE_MAX_DELAY = 25 This setting tells Scrapy to wait at most 25 seconds until the next request. To have detailed information on all the requests and their responses, you can enable debugging for auto-throttling.

AUTOTHROTTLE_DEBUG = True

COOKIES_ENABLED

You know cookies. They are settings stored in your browser and exchanged by every request with the server. They store information regarding your session, browsing preferences, or settings at the website. Sometimes they are required to prove you are using a browser. Sometimes you have to avoid a subset, because they tell the server you’re not using a browser. If you’re browsing in the European Union (EU), you get a notification about cookies by visiting almost every EU website. This is quite annoying, but a regulation to be aware of that websites store (let store) information about your browsing history.

As you may think, sometimes it is required to use cookies (for example websites that require login), but sometimes it’s better to avoid them.

The default setting in Scrapy is to use cookies. This means that every time the target web server returns an HTTP parameter Set-Cookie its value is stored internally by Scrapy and is sent back to the server with every new request.

You can disable this setting by adding the following configuration to your settings.py file:

COOKIES_ENABLED = False

166 ChapTer 4

Using sCrapy

If you want to debug which cookies are exchanged between the server and your spider, you can add the following configuration:

COOKIES_DEBUG = True

This will log every sent cookie (the Cookie header in your request) and received cookie (the Set-Cookie header in the response) to the console, or the logging framework you specified.

Summary

In this chapter you learned about Scrapy, the tool for website scraping. You implemented the scraper for the requirements of Chapter 2 with Scrapy. You have seen that you need to write much less than when you use a homemade spider where you have to handle requests—just to mention one example.

You learned some advanced topics too like writing your own middleware, pipelines, and extensions, and what the result is if you turn some knobs on the configuration panel.

Now you are a full-fledged website scraper. You have the tools with which you can complete 75% of all scraping jobs. Feel free to stop reading here, but keep in mind that these 75% are decreasing with the emerging number of JavaScript-heavy websites that render data dynamically.

The next chapter will cover an advanced topic I rarely use: handling web pages with JavaScript. There are different approaches, and we will go a bit deeper because I will show you options other than Selenium. If you are interested in the “Why?,” keep on reading!
