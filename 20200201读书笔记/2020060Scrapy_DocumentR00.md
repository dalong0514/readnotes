## 记忆时间

## 卡片

### 0101. 反常识卡——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

#### 01. 常识

#### 02. 反常识

#### 03. 知识来源

比如提出者，如何演化成型的；书或专栏具体出现的地方。

#### 04. 例子

### 0201. 术语卡——

根据反常识，再补充三个证据——就产生三张术语卡。

例子。

### 0202. 术语卡——

### 0203. 术语卡——

### 0301. 人名卡——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

维基百科链接：有的话。

#### 01. 出生日期

用一句话描述你对这个大牛的印象。

#### 02. 贡献及经历

#### 03. 论文及书籍

#### 04. 演讲汇总

找一个他的 TED 演讲，有的话。

### 0401. 金句卡——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 行动卡——

行动卡是能够指导自己的行动的卡。

### 0601. 任意卡——

最后还有一张任意卡，记录个人阅读感想。

## 模板

### 1. 逻辑脉络

用自己的话总结主题，梳理逻辑脉络，也就是这本书整个地图里这一章所在的节点。

### 2. 摘录及评论

1『自己的观点』

2『行动指南』

3『与其他知识的连接』

## 总体

Scrapy is a fast high-level web crawling [https://en.wikipedia.org/wiki/Web_crawler] and web scraping [https://en.wikipedia.org/wiki/Web_scraping] framework, used to crawl websites and extract structured data from their pages. It can be used for a wide range of purposes, from data mining to monitoring and automated testing.

Getting help. Having trouble? We’d like to help!

1. Try the FAQ – it’s got answers to some common questions.

2. Looking for specific information? Try the Index or Module Index.

3. Ask or search questions in StackOverflow using the scrapy tag ([Highest Voted 'scrapy' Questions - Stack Overflow](https://stackoverflow.com/tags/scrapy)).

4. Ask or search questions in the Scrapy subreddit [https://www.reddit.com/r/scrapy/].

5. Search for questions on the archives of the scrapy-users mailing list [https://groups.google.com/forum/#!forum/scrapy-users].

6. Ask a question in the #scrapy IRC channel,

7. Report bugs with Scrapy in our issue tracker [https://github.com/scrapy/scrapy/issues].

## 01. First steps

The best way to learn is with examples, and Scrapy is no exception. For this reason, there is an example Scrapy project named quotesbot [https://github.com/scrapy/quotesbot], that you can use to play and learn more about Scrapy. It contains two spiders for http://quotes.toscrape.com, one using CSS selectors and another one using XPath expressions.([scrapy/quotesbot: This is a sample Scrapy project for educational purposes](https://github.com/scrapy/quotesbot))

2『已下载 forked「2020007quotesbot」。』

### Scrapy at a glance

Scrapy is an application framework for crawling web sites and extracting structured data which can be used for a wide range of useful applications, like data mining, information processing or historical archival.

Even though Scrapy was originally designed for web scraping, it can also be used to extract data using APIs (such as Amazon Associates Web Services [https://affiliate-program.amazon.com/gp/advertising/api/detail/main.html]) or as a general purpose web crawler.

Walk-through of an example spider. In order to show you what Scrapy brings to the table, we’ll walk you through an example of a Scrapy Spider using the simplest way to run a spider. Here’s the code for a spider that scrapes famous quotes from website http://quotes.toscrape.com, following the pagination:

```
import scrapy

class QuotesSpider(scrapy.Spider):
    name = 'quotes' 
    start_urls = [ 'http://quotes.toscrape.com/tag/humor/', ]

def parse(self, response):
    for quote in response.css('div.quote'):
        yield { 'text': quote.css('span.text::text').get(), 
        'author': quote.xpath('span/small/text()').get(), }

    next_page = response.css('li.next a::attr("href")').get() 
    if next_page is not None:
        yield response.follow(next_page, self.parse)
```

Put this in a text file, name it to something like quotes_spider.py and run the spider using the runspider command:

    scrapy runspider quotes_spider.py -o quotes.json

When this finishes you will have in the quotes.json file a list of the quotes in JSON format, containing text and author, looking like this (reformatted here for better readability):

What just happened? When you ran the command scrapy runspider quotes_spider.py, Scrapy looked for a Spider definition inside it and ran it through its crawler engine. The crawl started by making requests to the URLs defined in the start_urls attribute (in this case, only the URL for quotes in humor category) and called the default callback method parse, passing the response object as an argument. In the parse callback, we loop through the quote elements using a CSS Selector, yield a Python dict with the extracted quote text and author, look for a link to the next page and schedule another request using the same parse method as callback.

1『这个例子用的是 CSS Selector，之前学习的是用 XPath Selector。』

Here you notice one of the main advantages about Scrapy: requests are scheduled and processed asynchronously. This means that Scrapy doesn’t need to wait for a request to be finished and processed, it can send another request or do other things in the meantime. This also means that other requests can keep going even if some request fails or an error happens while handling it.

1『asynchronously 异步处理。』

While this enables you to do very fast crawls (sending multiple concurrent requests at the same time, in a fault-tolerant way). Scrapy also gives you control over the politeness of the crawl through a few settings. You can do things like setting a download delay between each request, limiting amount of concurrent requests per domain or per IP, and even using an auto-throttling extension that tries to figure out these automatically.

Note: This is using feed exports to generate the JSON file, you can easily change the export format (XML or CSV, for example) or the storage backend (FTP or Amazon S3 [https://aws.amazon.com/s3/], for example). You can also write an item pipeline to store the items in a database.

What else? You’ve seen how to extract and store items from a website using Scrapy, but this is just the surface. Scrapy provides a lot of powerful features for making scraping easy and efficient, such as: 1) Built-in support for selecting and extracting data from HTML/XML sources using extended CSS selectors and XPath expressions, with helper methods to extract using regular expressions. 2) An interactive shell console (IPython aware) for trying out the CSS and XPath expressions to scrape data, very useful when writing or debugging your spiders. 3) Built-in support for generating feed exports in multiple formats (JSON, CSV, XML) and storing them in multiple backends (FTP, S3, local filesystem).

4) Robust encoding support and auto-detection, for dealing with foreign, non-standard and broken encoding declarations. 5) Strong extensibility support, allowing you to plug in your own functionality using signals and a well-defined API (middlewares, extensions, and pipelines). 6) Wide range of built-in extensions and middlewares for handling: cookies and session handling; HTTP features like compression, authentication, caching; user-agent spoofing; robots.txt; crawl depth restriction; and more.

7) A Telnet console for hooking into a Python console running inside your Scrapy process, to introspect and debug your crawler. 8) Plus other goodies like reusable spiders to crawl sites from Sitemaps [https://www.sitemaps.org/index.html] and XML/CSV feeds, a media pipeline for automatically downloading images (or any other media) associated with the scraped items, a caching DNS resolver, and much more!

1『原来还有通用模板的，Sitemaps 和 automatically downloading images。』

We strongly recommend that you install Scrapy in a dedicated virtualenv, to avoid conflicting with your system packages.

Python virtualenvs can be created to use Python 2 by default, or Python 3 by default. If you want to install scrapy with Python 3, install scrapy within a Python 3 virtualenv. And if you want to install scrapy with Python 2, install scrapy within a Python 2 virtualenv.

2『意思是创建虚拟环境的时候可以指定 Python 2 或 3，待试验一下确认。』

    sudo apt-get install python3 python3-dev

### Scrapy Tutorial

We are going to scrape quotes.toscrape.com [http://quotes.toscrape.com/], a website that lists quotes from famous authors. This tutorial will walk you through these tasks: 1) Creating a new Scrapy project. 2) Writing a spider to crawl a site and extract data. 3) Exporting the scraped data using the command line. 4) Changing spider to recursively follow links. 4) Using spider arguments.

[Automate the Boring Stuff with Python](https://automatetheboringstuff.com/)

[How to Think Like a Computer Scientist — How to Think Like a Computer Scientist: Learning with Python 3](http://openbookproject.net/thinkcs/python/english3e/)

[Learn Python the Hard Way](https://learnpythonthehardway.org/python3/)

Our first Spider. Spiders are classes that you define and that Scrapy uses to scrape information from a website (or a group of websites). They must subclass Spider and define the initial requests to make, optionally how to follow links in the pages, and how to parse the downloaded page content to extract data.
























