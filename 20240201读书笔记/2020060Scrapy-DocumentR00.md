## 记忆时间

## 卡片

### 0101. 主题卡 ——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡 ——

根据反常识，再补充三个证据——就产生三张术语卡。

### 0202. 术语卡 ——

### 0203. 术语卡 ——

### 0301. 人名卡 ——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

### 0401. 金句卡 ——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 行动卡 ——

行动卡是能够指导自己的行动的卡。

### 0601. 数据信息卡 ——

### 0701. 任意卡 ——

最后还有一张任意卡，记录个人阅读感想。

## 总体

Scrapy is a fast high-level web crawling [https://en.wikipedia.org/wiki/Web_crawler] and web scraping [https://en.wikipedia.org/wiki/Web_scraping] framework, used to crawl websites and extract structured data from their pages. It can be used for a wide range of purposes, from data mining to monitoring and automated testing.

Getting help. Having trouble? We’d like to help!

1 Try the FAQ – it’s got answers to some common questions.

2 Looking for specific information? Try the Index or Module Index.

3 Ask or search questions in StackOverflow using the scrapy tag ([Highest Voted 'scrapy' Questions - Stack Overflow](https://stackoverflow.com/tags/scrapy)).

4 Ask or search questions in the Scrapy subreddit [https://www.reddit.com/r/scrapy/].

5 Search for questions on the archives of the scrapy-users mailing list [https://groups.google.com/forum/#!forum/scrapy-users].

6 Ask a question in the #scrapy IRC channel,

7 Report bugs with Scrapy in our issue tracker [https://github.com/scrapy/scrapy/issues].

当您运行 scrapy runspider somefile.py 命令时，Scrapy 尝试从该文件中查找 Spider 的定义，并且在爬取引擎中运行它。Scrapy 首先读取定义在 start_urls 属性中的 URL (在本示例中，就是 StackOverflow 的 top question 页面的 URL)，创建请求，并且将接收到的 response 作为参数调用默认的回调函数 parse ，来启动爬取。在回调函数 parse 中，我们使用 CSS Selector 来提取链接。接着，我们产生 (yield) 更多的请求，注册 parse_question 作为这些请求完成时的回调函数。

这里，您可以注意到 Scrapy 的一个最主要的优势：请求（request）是被异步调度和处理的 。这意味着，Scrapy 并不需要等待一个请求（request）完成及处理，在此同时，也发送其他请求或者做些其他事情。这也意味着，当有些请求失败或者处理过程中出现错误时，其他的请求也能继续处理。

在允许您可以以非常快的速度进行爬取时（以容忍错误的方式同时发送多个 request），Scrapy 也通过一些设置来允许您控制其爬取的方式。例如，您可以为两个 request 之间设置下载延迟，限制单域名（domain）或单个 IP 的并发请求量，甚至可以使用自动限制插件来自动处理这些问题。最终，parse_question 回调函数从每个页面中爬取到问题（question）的数据并产生了一个 dict，Scrapy 收集并按照终端（command line）的要求将这些结果写入到了 JSON 文件中。

注解：这里使用了 feed exports 来创建了 JSON 文件，您可以很容易的改变导出的格式（比如 XML 或 CSV）或者存储后端（例如 FTP 或者 Amazon S3）。您也可以编写 item pipeline 来将 item 存储到数据库中。

您已经了解了如何通过 Scrapy 提取存储网页中的信息，但这仅仅只是冰山一角。Scrapy 提供了很多强大的特性来使得爬取更为简单高效，例如：1）对 HTML，XML 源数据「选择及提取」的内置支持，提供了 CSS 选择器（selector）以及 XPath 表达式进行处理，以及一些帮助函数 (helper method) 来使用正则表达式来提取数据。2）提供交互式 shell 终端，为您测试 CSS 及 XPath 表达式，编写和调试爬虫提供了极大的方便。3）通过 feed 导出提供了多格式 (JSON、CSV、XML)，多存储后端 (FTP、S3、本地文件系统) 的内置支持。4）提供了一系列在 spider 之间共享的可复用的过滤器 (即 Item Loaders)，对智能处理爬取数据提供了内置支持。5）针对非英语语系中不标准或者错误的编码声明，提供了自动检测以及健壮的编码支持。6）高扩展性。您可以通过使用 signals，设计好的 API (中间件，extensions, pipelines) 来定制实现您的功能。7）内置的中间件及扩展为下列功能提供了支持: * cookies and session 处理 * HTTP 压缩 * HTTP 认证 * HTTP 缓存 * user-agent 模拟 * robots.txt * 爬取深度限制 * 其他。8）内置 Telnet 终端 ，通过在 Scrapy 进程中钩入 Python 终端，使您可以查看并且调试爬虫。9）以及其他一些特性，例如可重用的，从 Sitemaps 及 XML/CSV feeds 中爬取网站的爬虫、 可以 自动下载 爬取到的数据中的图片 (或者其他资源) 的 media pipeline、 带缓存的 DNS 解析器，以及更多的特性。

## 0101. First steps

The best way to learn is with examples, and Scrapy is no exception. For this reason, there is an example Scrapy project named quotesbot [https://github.com/scrapy/quotesbot], that you can use to play and learn more about Scrapy. It contains two spiders for http://quotes.toscrape.com, one using CSS selectors and another one using XPath expressions.([scrapy/quotesbot: This is a sample Scrapy project for educational purposes](https://github.com/scrapy/quotesbot))

2『已下载 forked「2020007quotesbot」。』

### Scrapy at a glance

Scrapy is an application framework for crawling web sites and extracting structured data which can be used for a wide range of useful applications, like data mining, information processing or historical archival.

Even though Scrapy was originally designed for web scraping, it can also be used to extract data using APIs (such as Amazon Associates Web Services [https://affiliate-program.amazon.com/gp/advertising/api/detail/main.html]) or as a general purpose web crawler.

Walk-through of an example spider. In order to show you what Scrapy brings to the table, we’ll walk you through an example of a Scrapy Spider using the simplest way to run a spider. Here’s the code for a spider that scrapes famous quotes from website http://quotes.toscrape.com, following the pagination:

```py
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

## 0101. Scrapy入门教程.md

下列任务：1）创建一个 Scrapy 项目；2）定义提取的 Item；3）编写爬取网站的 spider 并提取 Item；4）编写 Item Pipeline 来存储提取到的 Item (即数据)。

在开始爬取之前，您必须创建一个新的 Scrapy 项目。进入您打算存储代码的目录中，运行下列命令：scrapy startproject tutorial。该命令将会创建包含下列内容的 tutorial 目录。

定义 Item。Item 是保存爬取到的数据的容器；其使用方法和 python 字典类似。虽然您也可以在 Scrapy 中直接使用 dict，但是 Item 提供了额外保护机制来避免拼写错误导致的未定义字段错误。They can also be used with Item Loaders, a mechanism with helpers to conveniently populate Items. 类似在 ORM 中做的一样，您可以通过创建一个 scrapy.Item 类，并且定义类型为 scrapy.Field 的类属性来定义一个 Item。首先根据需要从 dmoz.org 获取到的数据对 item 进行建模。我们需要从 dmoz 中获取名字，url，以及网站的描述。对此，在 item 中定义相应的字段。编辑 tutorial 目录中的 items.py 文件：

```py
import scrapy

class DmozItem(scrapy.Item):
    title = scrapy.Field()
    link = scrapy.Field()
    desc = scrapy.Field()
```

一开始这看起来可能有点复杂，但是通过定义 item，您可以很方便的使用 Scrapy 的其他方法。而这些方法需要知道您的 item 的定义。

Spider 是用户编写用于从单个网站 (或者一些网站) 爬取数据的类。其包含了一个用于下载的初始 URL，如何跟进网页中的链接以及如何分析页面中的内容，提取生成 item 的方法。为了创建一个 Spider，您必须继承 scrapy.Spider 类，且定义一些属性：1）name：用于区别 Spider。该名字必须是唯一的，您不可以为不同的 Spider 设定相同的名字。2）start_urls：包含了 Spider 在启动时进行爬取的 url 列表。因此，第一个被获取到的页面将是其中之一。后续的 URL 则从初始的 URL 获取到的数据中提取。3）parse () 是 spider 的一个方法。被调用时，每个初始 URL 完成下载后生成的 Response 对象将会作为唯一的参数传递给该函数。该方法负责解析返回的数据 (response data)，提取数据 (生成 item) 以及生成需要进一步处理的 URL 的 Request 对象。

以下为我们的第一个 Spider 代码，保存在 tutorial/spiders 目录下的 dmoz_spider.py 文件中：

```py
import scrapy

class DmozSpider(scrapy.Spider):
    name = "dmoz"
    allowed_domains = ["dmoz.org"]
    start_urls = [
        "http://www.dmoz.org/Computers/Programming/Languages/Python/Books/",
        "http://www.dmoz.org/Computers/Programming/Languages/Python/Resources/"
    ]

    def parse(self, response):
        filename = response.url.split("/")[-2] + '.html'
        with open(filename, 'wb') as f:
            f.write(response.body)
```

爬取。进入项目的根目录，执行下列命令启动 spider：scrapy crawl dmoz。该命令启动了我们刚刚添加的 dmoz spider，向 dmoz.org 发送一些请求。您将会得到类似的输出；注解：最后你可以看到有一行 log 包含定义在 start_urls 的初始 URL，并且与 spider 中是一一对应的。在 log 中可以看到其没有指向其他页面 (referer: None)。现在，查看当前目录，您将会注意到有两个包含 url 所对应的内容的文件被创建了：Book , Resources，正如我们的 parse 方法里做的一样。

1『启动命令里的对象 dmoz，是在类 Spider 里定义的 name 属性。』

Scrapy 为 Spider 的 start_urls 属性中的每个 URL 创建了 scrapy.Request 对象，并将 parse 方法作为回调函数 (callback) 赋值给了 Request。Request 对象经过调度，执行生成 scrapy.http.Response 对象并送回给 spider 的 parse () 方法。

Selectors 选择器简介。从网页中提取数据有很多方法。Scrapy 使用了一种基于 XPath 和 CSS 表达式机制：Scrapy Selectors 。关于 selector 和其他提取机制的信息请参考[Selector 文档](https://scrapy-chs.readthedocs.io/zh_CN/1.0/topics/selectors.html#topics-selectors)。

这里给出 XPath 表达式的例子及对应的含义：1）/html/head/title：选择 HTML 文档中 <head> 标签内的 <title> 元素。2）/html/head/title/text ()：选择上面提到的 <title> 元素的文字。3）//td：选择所有的 <td> 元素。4）//div [@class="mine"]：选择所有具有 class="mine" 属性的 div 元素。

上边仅仅是几个简单的 XPath 例子，XPath 实际上要比这远远强大的多。如果您想了解的更多，我们推荐通过这些例子来学习 XPath, 以及这篇教程学习：[A very brief primer to thinking in XPath // plasmasturm.org](http://plasmasturm.org/log/xpath101/)。注解：CSS vs XPath，您可以仅仅使用 CSS Selector 来从网页中提取数据。不过，XPath 提供了更强大的功能。其不仅仅能指明数据所在的路径，还能查看数据。比如，您可以这么进行选择：包含文字 ‘Next Page’ 的链接 。正因为如此，即使您已经了解如何使用 CSS selector，我们仍推荐您使用 XPath。

为了配合 CSS 与 XPath，Scrapy 除了提供了 Selector 之外，还提供了方法来避免每次从 response 中提取数据时生成 selector 的麻烦。Selector 有四个基本的方法（点击相应的方法可以看到详细的 API 文档）：1）xpath ()：传入 xpath 表达式，返回该表达式所对应的所有节点的 selector list 列表。2）css ()：传入 CSS 表达式，返回该表达式所对应的所有节点的 selector list 列表。3）extract ()：序列化该节点为 unicode 字符串并返回 list。4）re ()：根据传入的正则表达式对数据进行提取，返回 unicode 字符串 list 列表。

在 Shell 中尝试 Selector 选择器。为了介绍 Selector 的使用方法，接下来我们将要使用内置的 Scrapy shell 。Scrapy Shell 需要您预装好 IPython（一个扩展的 Python 终端）。您需要进入项目的根目录，执行下列命令来启动 shell：

    scrapy shell "http://www.dmoz.org/Computers/Programming/Languages/Python/Books/"

注解：当您在终端运行 Scrapy 时，请一定记得给 url 地址加上引号，否则包含参数的 url (例如 & 字符) 会导致 Scrapy 运行失败。shell 的输出类似。当 shell 载入后，您将得到一个包含 response 数据的本地 response 变量。输入 response.body 将输出 response 的包体，输出 response.headers 可以看到 response 的包头。

\#TODO... 更为重要的是，response 拥有一个 selector 属性，该属性是以该特定 response 初始化的类 Selector 的对象。您可以通过使用 response.selector.xpath () 或 response.selector.css () 来对 response 进行查询。此外，scrapy 也对 response.selector.xpath () 及 response.selector.css () 提供了一些快捷方式，例如 response.xpath () 或 response.css () 。

同时，shell 根据 response 提前初始化了变量 sel 。该 selector 根据 response 的类型自动选择最合适的分析规则 (XML vs HTML)。让我们来试试:

```py
In [1]: response.xpath('//title')
Out[1]: [<Selector xpath='//title' data=u'<title>Open Directory - Computers: Progr'>]

In [2]: response.xpath('//title').extract()
Out[2]: [u'<title>Open Directory - Computers: Programming: Languages: Python: Books</title>']

In [3]: response.xpath('//title/text()')
Out[3]: [<Selector xpath='//title/text()' data=u'Open Directory - Computers: Programming:'>]

In [4]: response.xpath('//title/text()').extract()
Out[4]: [u'Open Directory - Computers: Programming: Languages: Python: Books']

In [5]: response.xpath('//title/text()').re('(\w+):')
Out[5]: [u'Computers', u'Programming', u'Languages', u'Python']
```

提取数据。我们来尝试从这些页面中提取些有用的数据。您可以在终端中输入 response.body 来观察 HTML 源码并确定合适的 XPath 表达式。不过，这任务非常无聊且不易。您可以考虑使用 Firefox 的 Firebug 扩展来使得工作更为轻松。详情请参考[「使用 Firebug 进行爬取」](https://scrapy-chs.readthedocs.io/zh_CN/1.0/topics/firebug.html#topics-firebug)和[「借助 Firefox 来爬取」](https://scrapy-chs.readthedocs.io/zh_CN/1.0/topics/firefox.html#topics-firefox) 。

在查看了网页的源码后，您会发现网站的信息是被包含在第二个 `<ul>` 元素中。我们可以通过这段代码选择该页面中网站列表里所有 `<li>` 元素：

    response.xpath('//ul/li')

网站的描述：

    response.xpath('//ul/li/text()').extract()

网站的标题：

    response.xpath('//ul/li/a/text()').extract()

以及网站的链接：

    response.xpath('//ul/li/a/@href').extract()

之前提到过，每个 .xpath () 调用返回 selector 组成的 list，因此我们可以拼接更多的 .xpath () 来进一步获取某个节点。我们将在下边使用这样的特性：

```py
for sel in response.xpath('//ul/li'):
    title = sel.xpath('a/text()').extract()
    link = sel.xpath('a/@href').extract()
    desc = sel.xpath('text()').extract()
    print title, link, desc
```

注解：关于嵌套 selctor 的更多详细信息，请参考嵌套选择器 (selectors) 以及选择器 (Selectors) 文档中的使用相对 XPaths 部分。在我们的 spider 中加入这段代码：

```py
import scrapy

class DmozSpider(scrapy.Spider):
    name = "dmoz"
    allowed_domains = ["dmoz.org"]
    start_urls = [
        "http://www.dmoz.org/Computers/Programming/Languages/Python/Books/",
        "http://www.dmoz.org/Computers/Programming/Languages/Python/Resources/"
    ]

    def parse(self, response):
        for sel in response.xpath('//ul/li'):
            title = sel.xpath('a/text()').extract()
            link = sel.xpath('a/@href').extract()
            desc = sel.xpath('text()').extract()
            print title, link, desc
```

现在尝试再次爬取 dmoz.org，您将看到爬取到的网站信息被成功输出：

    scrapy crawl dmoz

使用 item。Item 对象是自定义的 python 字典。您可以使用标准的字典语法来获取到其每个字段的值。(字段即是我们之前用 Field 赋值的属性）：

```py
>>> item = DmozItem()
>>> item['title'] = 'Example title'
>>> item['title']
'Example title'
```

为了将爬取的数据返回，我们最终的代码将是：

```py
import scrapy

from tutorial.items import DmozItem

class DmozSpider(scrapy.Spider):
    name = "dmoz"
    allowed_domains = ["dmoz.org"]
    start_urls = [
        "http://www.dmoz.org/Computers/Programming/Languages/Python/Books/",
        "http://www.dmoz.org/Computers/Programming/Languages/Python/Resources/"
    ]

    def parse(self, response):
        for sel in response.xpath('//ul/li'):
            item = DmozItem()
            item['title'] = sel.xpath('a/text()').extract()
            item['link'] = sel.xpath('a/@href').extract()
            item['desc'] = sel.xpath('text()').extract()
            yield item
```

注解：您可以在 dirbot 项目中找到一个具有完整功能的 spider。该项目可以通过 [scrapy/dirbot: Scrapy project to scrape public web directories](https://github.com/scrapy/dirbot) 找到。现在对 dmoz.org 进行爬取将会产生 DmozItem 对象。

追踪链接（Following links）。接下来，不仅仅满足于爬取 Books 及 Resources 页面，您想要获取获取所有 Python directory 的内容。既然已经能从页面上爬取数据了，为什么不提取您感兴趣的页面的链接，追踪他们，读取这些链接的数据呢？下面是实现这个功能的改进版 spider：

```py
import scrapy

from tutorial.items import DmozItem

class DmozSpider(scrapy.Spider):
    name = "dmoz"
    allowed_domains = ["dmoz.org"]
    start_urls = [
        "http://www.dmoz.org/Computers/Programming/Languages/Python/",
    ]

    def parse(self, response):
        for href in response.css("ul.directory.dir-col > li > a::attr('href')"):
            url = response.urljoin(response.url, href.extract())
            yield scrapy.Request(url, callback=self.parse_dir_contents)

    def parse_dir_contents(self, response):
        for sel in response.xpath('//ul/li'):
            item = DmozItem()
            item['title'] = sel.xpath('a/text()').extract()
            item['link'] = sel.xpath('a/@href').extract()
            item['desc'] = sel.xpath('text()').extract()
            yield item
```

现在，parse () 仅仅从页面中提取我们感兴趣的链接，使用 response.urljoin 方法构造一个绝对路径的 URL (页面上的链接都是相对路径的)，产生 (yield) 一个请求，该请求使用 parse_dir_contents () 方法作为回调函数，用于最终产生我们想要的数据。这里展现的即是 Scrpay 的追踪链接的机制：当您在回调函数中 yield 一个 Request 后，Scrpay 将会调度，发送该请求，并且在该请求完成时，调用所注册的回调函数。

基于此方法，您可以根据您所定义的跟进链接的规则，创建复杂的 crawler，并且，根据所访问的页面，提取不同的数据。一种常见的方法是，回调函数负责提取一些 item，查找能跟进的页面的链接，并且使用相同的回调函数 yield 一个 Request：

```py
def parse_articles_follow_next_page(self, response):
    for article in response.xpath("//article"):
        item = ArticleItem()

        ... extract article data here

        yield item

    next_page = response.css("ul.navigation > li.next-page > a::attr('href')")
    if next_page:
        url = response.urljoin(next_page[0].extract())
        yield scrapy.Request(url, self.parse_articles_follow_next_page)
```

上述代码将创建一个循环，跟进所有下一页的链接，直到找不到为止 —— 对于爬取博客、论坛以及其他做了分页的网站十分有效。另一种常见的需求是从多个页面构建 item 的数据，这可以使用[在回调函数中传递信息的技巧](https://scrapy-chs.readthedocs.io/zh_CN/1.0/topics/request-response.html#topics-request-response-ref-request-callback-arguments)。

注解：上述代码仅仅作为阐述 scrapy 机制的样例 spider，想了解如何实现一个拥有小型的规则引擎 (rule engine) 的通用 spider 来构建您的 crawler，请查看 [Generic Spiders](https://scrapy-chs.readthedocs.io/zh_CN/1.0/topics/spiders.html#scrapy.spiders.CrawlSpider)。

保存爬取到的数据。最简单存储爬取的数据的方式是使用 Feed exports：

    scrapy crawl dmoz -o items.json

该命令将采用 JSON 格式对爬取的数据进行序列化，生成 items.json 文件。在类似本篇教程里这样小规模的项目中，这种存储方式已经足够。如果需要对爬取到的 item 做更多更为复杂的操作，您可以编写 [Item Pipeline](https://scrapy-chs.readthedocs.io/zh_CN/1.0/topics/item-pipeline.html#topics-item-pipeline)。类似于我们在创建项目时对 Item 做的，用于您编写自己的 tutorial/pipelines.py 也被创建。不过如果您仅仅想要保存 item，您不需要实现任何的 pipeline。

学习的最好方法就是参考例子，Scrapy 也不例外。Scrapy 提供了一个叫做 dirbot 的样例项目供您把玩学习。其包含了在教程中介绍的 dmoz spider。您可以通过 [scrapy/dirbot: Scrapy project to scrape public web directories](https://github.com/scrapy/dirbot) 找到 dirbot 。项目中包含了 README文 件，对项目内容进行了详细的介绍。如果您熟悉 git，可以 checkout 代码，或者点击 Downloads 来下载项目的 tarball 或者 zip 的压缩包。Snipplr 上的 scrapy 标签是用来分享 spider，middeware，extension 或者 script 代码片段。

1『上面的 dirbot 项目已经不维护了，新的项目是：[scrapy/quotesbot: This is a sample Scrapy project for educational purposes](https://github.com/scrapy/quotesbot)。』