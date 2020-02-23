# 2020061Website_Scraping_with_R01

Copyright © 2018

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

This book is split into six chapters:

1. Getting Started is to get you started with this book: you can learn what website scraping is and why it worth writing a book about this topic.

2. Enter the Requirements introduces the requirements we will use to implement website scrapers in the follow-up chapters.

3. Using Beautiful Soup introduces you to Beautiful Soup, an HTML content parser that you can use to write website scraper scripts. We will implement a scraper to gather the requirements of Chapter 2 using Beautiful Soup.

4. Using Scrapy introduces you to Scrapy, the (in my opinion) best website scraping toolbox available for the Python programming language. We will use Scrapy to implement a website scraper to gather the requirements of Chapter 2.

5. Handling JavaScript shows you options for how you can deal with websites that utilize JavaScript to load data dynamically and through this, give users a better experience. Unfortunately, this makes basic website scraping a torture but there are options that you can rely on.

6. Website Scraping in the Cloud moves your scrapers from running on your computer locally to remote computers in the Cloud. I'll show you free and paid providers where you can deploy your spiders and automate the scraping schedules.

You can read this book from cover to cover if you want to learn the different approaches of website scraping with Python. If you're interested only in a specific topic, like Scrapy for example, you can jump straight to Chapter 4, although I recommend reading Chapter 2 because it contains the description of the data gathering task we will implement in the vast part of the book.

2『本书的源码：[Apress/website-scraping-w-python: Source code for 'Website Scraping with Python' by Gabor Laszlo Hajba](https://github.com/Apress/website-scraping-w-python)，然后追源到出版社 Apress 的 GitHub 仓库：[Apress](https://github.com/Apress?utf8=%E2%9C%93&q=&type=&language=)，那么同理其他出版社在 GitHub 上应该也有源码仓库。已下载源码「2020061Website_Scraping_with_Python源码」。』

## 01. Getting Started

### 1. 逻辑脉络

网络爬虫的基本知识以及其准备工作。给了两个小案例，抓取网页里的子页地址以及地图地址。

### 2. 摘录及评论

In this chapter you've gotten a basic introduction to website scraping and how to prepare for a scraping job. Besides the introduction, you created your first building blocks for scrapers that extracted information from a web page, like links and image sources. 

we can narrow the scope to one or two web pages and extract information in a structured manner — and get the results exported to a database or structured file (JSON, CSV, XML, Excel sheets).

Nowadays, digital transformation is the new buzzword companies use and want to engage. One component of this transformation is providing data access points to everyone (or at least to other companies interested in that data) through APIs. With those APIs available, you do not need to invest time and other resources to create a website scraper. Even though providing APIs is something scraper developers won't benefit from, the process is slow, and many companies don't bother creating those access points because they have a website and it is enough to maintain.

Projects for Website Scraping. There are a lot of use cases where you can leverage your knowledge of website scraping. Some might be common sense, while others are extreme cases. In this section you will find some use cases where you can leverage your knowledge. The main reason to create a scraper is to extract information from a website. This information can be a list of products sold by a company, nutrition details of groceries, or NFL results from the last 15 years. Most of these projects are the groundwork for further data analysis: gathering all this data manually is a long and error-prone process.

Sometimes you encounter projects where you need to extract data from one website to load it into another — a migration. I recently had a project where my customer moved his website to WordPress and the old blog engine's export functionality wasn't meant to import it into WordPress. I created a scraper that extracted all the posts (around 35,000) with their images, did some formatting on the contents to use WordPress short codes, and then imported all those posts into the new website.

A weird project could be to download the whole Internet! Theoretically it is not impossible: you start at a website, download it, extract and follow all the links on this page, and download the new sites too. If the websites you scrape all have links to each other, you can browse (and download) the whole Internet. I don't suggest you start this project because you won't have enough disk space to contain the entire Internet, but the idea is interesting. Let me know how far you reached if you implement a scraper like this.

1『一个网页有很多连接，从几个网页出发甚至可以下载整个万维网上的数据，哈哈。』

Websites Are the Bottleneck. One of the most difficult parts of gathering data through websites is that websites differ. I mean not only the data but the layout too. It is hard to create a good-fit-for-all scraper because every website has a different layout, uses different (or no) HTML IDs to identify fields, and so on. And if this is not enough, many websites change their layout frequently. If this happens, your scraper is not working as it did previously. In these cases, the only option is to revisit your code and adapt it to the changes of the target website. Unfortunately, you won't learn secret tricks that will help you create a scraper that always works — if you want to write specialized data extractors. I will show some examples in this book that will always work if the HTML standard is in use.

1『网页都形式多样（layout），没法做一个通用的爬虫，爬虫得随网页的变化而调整。』

Tools in This Book. In this book you will learn the basic tools you can use in Python to do your website scraping. You will soon realize how hard it is to create every single piece of a scraper from scratch. But Python has a great community, and a lot of projects are available to help you focus on the important part of your scraper: data extraction. I will introduce you to tools like the requests library, Beautiful Soup, and Scrapy. The requests library is a lightweight wrapper over the tedious task of handling HTTP, and it emerged as the recommended way:

The Requests package is recommended for a higher level HTTP client interface. — Python 3 documentation

1『Requests package 即为更高层的客户接口。』

Beautiful Soup is a content parser. It is not a tool for website scraping because it doesn't navigate pages automatically and it is hard to scale. But it aids in parsing content, and gives you options to extract the required information from XML and HTML structures in a friendly manner.

Scrapy is a website scraping framework/library. It is much more powerful than Beautiful Soup, and it can be scaled. Therefore, you can create more complex scrapers easier with Scrapy. But on the other side, you have more options to configure. Fine-tuning Scrapy can be a problem, and you can mess up a lot if you do something wrong. But with great power comes great responsibility: you must use Scrapy with care. Even though Scrapy is the Python library created for website scraping, sometimes I just prefer a combination of requests and Beautiful Soup because it is lightweight, and I can write my scraper in a short period — and I do not need scaling or parallel execution.

1『BS 是内容解析器。相比于 Python 的 scraper 框架，作者更倾向于使用 requests 和 BS4 的组合工具，但对于复杂的抓取任务可以用 scraper 框架的同时结合 BS4。』

Preparation. When starting a website scraper, even if it is a small script, you must prepare yourself for the task. There are some legal and technical considerations for you right at the beginning. In this section I will give you a short list of what you should do to be prepared for a website scraping job or task: 1) Do the website's owners allow scraping? To find out, read the Terms & Conditions and the Privacy Policy of the website. 2) Can you scrape the parts you are interested in? See the robots.txt file for more information and use a tool that can handle this information. 3) What technology does the website use? There are free tools available that can help you with this task, but you can look at the website's HTML code to find out. 4) What tools should I use? Depending on your task and the website's structure, there are different paths you can choose from. Now let's see a detailed description for each item mentioned.

Terms and Robots. Scraping currently has barely any limitations; there are no laws defining what can be scraped and what cannot. However, there are guidelines that define what you should respect. There is no enforcing; you can completely ignore these recommendations, but you shouldn't. Before you start any scraping task, look at the Terms & Conditions and Privacy Policy of the website you want to gather data from. If there is no limitation on scraping, then you should look at the robots.txt file for the given website(s).

When reading the terms and conditions of a website, you can search for following keywords to find restrictions:

• scraper/scraping

• crawler/crawling

• bot

• spider

• program

Most of the time these keywords can be found, and this makes your search easier. If you have no luck, you need to read through the whole legal content and it is not as easy — at least I think legal stuff is always dry to read. in the european Union there's a data protection right that has been live for some years but strictly enforced from 2018: Gdpr. Keep the private data of private persons out of your scraping — you can be held liable if some of it slips out into public because of your scraper.

robots.txt. Most websites provide a file called robots.txt, which is used to tell web crawlers what they can scrape and what they should not touch. Naturally, it is up to the developer to respect these recommendations, but I advise you to always obey the contents of the robots.txt file. Let's see one example of such a file:

```
User-agent: * 
Disallow: /covers/ 
Disallow: /api/ 
Disallow: /*checkval 
Disallow: /*wicket:interface 
Disallow: ?print_view=true 
Disallow: /*/search 
Disallow: /*/product-search 
Allow: /*/product-search/discipline 
Disallow: /*/product-search/discipline?*facet-subj= 
Disallow: /*/product-search/discipline?*facet-pdate= 
Disallow: /*/product-search/discipline?*facet-type=category
```

The preceding code block is from www.apress.com/robots.txt. As you can see, most content tells what is disallowed. For example, scrapers shouldn't scrape www.apress.com/covers/. Besides the Allow and Disallow entries, the User-agent can be interesting. Every scraper should have an identification, which is provided through the user agent parameter. Bigger bots, created by Google and Bing, have their unique identifier. And because they are scrapers that add your pages to the search results, you can define excludes for these bots to leave you alone. Later in this chapter, you will create a script which will examine and follow the guidelines of the robots.txt file with a custom user agent. There can be other entries in a robots.txt file, but they are not standard. To find out more about those entries, visit https://en.wikipedia.org/wiki/Robots_exclusion_standard.

Technology of the Website. Another useful preparation step is to look at the technologies the targeted website uses. There is a Python library called builtwith, which aims to detect the technologies a website utilizes. The problem with this library is that the last version 1.3.2 was released in 2015, and it is not compatible with Python 3. Therefore, you cannot use it as you do with libraries available from the PyPI. However, in May 2017, Python 3 support has been added to the sources, but the new version was not released (yet, I'm writing this in November 2017). This doesn't mean we cannot use the tool; we must manually install it.

First, download the sources from [richardpenman / builtwith / Downloads — Bitbucket](https://bitbucket.org/richardpenman/builtwith/downloads/). If you prefer, you can clone the repository with Mercurial to stay up to date if new changes occur. After downloading the sources, navigate to the folder where you downloaded the sources and execute the following command:

    pip install .

The command installs builtwith to your Python environment and you can use it. Now if you open a Python CLI, you can look at your target site to see what technologies it uses.

1『下载后解压，放在 scrapers 文件里里的，进入「/Users/Daglas/scrapys/richardpenman-builtwith」后命令安装。』

3『作者的个人仓库：[Bitbucket](https://bitbucket.org/%7B48b76067-f0dc-4ada-b5ba-2352e4fe0953%7D/)。』

```
>>> from builtwith import builtwith
>>> builtwith('http://www.apress.com') 
>>> {'javascript-frameworks': ['AngularJS', 'jQuery'], 'font-scripts': ['Font Awesome'], 'tag-managers': ['Google Tag Manager'], 'analytics': ['Optimizely']}
```

The preceding code block shows which technologies Apress uses for its website. You can learn from AngularJS that if you plan to write a scraper, you should be prepared to handle dynamic content that is rendered with JavaScript. builtwith is not a magic tool, it is a website scraper that downloads the given URL; parses its contents; and based on its knowledge base, it tells you which technologies the website uses. This tool uses basic Python features, which means sometimes you cannot get information in the website you are interested in, but most of the time you get enough information.

1『builtwith 获取这个网站采用的哪些技术，你要深度爬这个网的话就得去研究这些技术。』

Using Chrome Developer Tools. To walk through the website and identify the fields of the requirements, we will use Google Chrome's built-in DevTools. If you do not know what this tool can do for you, here is a quick introduction. The Chrome Developer Tools (DevTools for short), are a set of web authoring and debugging tools built into Google Chrome. The DevTools provide web developers deep access into the internals of the browser and their web application. Use the DevTools to efficiently track down layout issues, set JavaScript breakpoints, and get insights for code optimization.

As you can see, DevTools give you tools to see inside the workings of the browser. We don't need anything special; we will use DevTools to see where the information resides. In this section I will guide us with screenshots through the steps I usually do when I start (or just evaluate) a scraping project.

First, you must prepare to get the information. Even though we know which website to scrape and what kind of data to extract, we need some preparation. Basic website scrapers are simple tools that download the contents of the website into memory and then do extraction on this data. This means they are not capable of running dynamic content just like JavaScript, and therefore we have to make our browser similar to a simple scraper by disabling JavaScript rendering.

First, right-click with your mouse on the web page and from the menu select "Inspect," as shown in Figure 1-1. Alternatively, you can press CTRL+SHIFT+I in Windows or z+⇧+I on a Mac to open the DevTools window. Then locate the settings button (the three vertically aligned dots, as shown in Figure 1-2.) and click it. Alternatively, you can press F1 in Windows. Now scroll down to the bottom of the Settings screen and make sure Disable JavaScript is checked, as shown in Figure 1-3.

1『在 Chrome 开发者工具里一定要在设置里，将「Debugger」里的「Disable JavaScript」打勾。』

Now reload the page, exit the Settings window, but stay in the inspector view because we will use the HTML element selector available here. Note disabling JavaScript is necessary if you want to see how your scraper sees the website. Later in this book, you will learn options how to scrape websites that utilize JavaScript to render dynamic content. But to fully understand and enjoy those extra capabilities, you must learn the basics.

Tool Considerations. If you are reading this book, you will write your scrapers most likely with Python 3. However, you must decide on which tools to use. In this book you will learn the tools of the trade and you can decide on your own what to use, but now I'll share with you how I decide on an approach.

If you are dealing with a simple website — and by simple, I mean one that is not using JavaScript excessively for rendering — then you can choose between creating a crawler with Beautiful Soup + requests or use Scrapy. If you must deal with a lot of data and want to speed things up, use Scrapy. In the end, you will use Scrapy in 90% of your tasks, and you can integrate Beautiful Soup into Scrapy and use them together.

If the website uses JavaScript for rendering, you can either reverse engineer the AJAX/XHR calls and use your preferred tool, or you can reach out to a tool that renders websites for you. Such tools are Selenium and Portia. I will introduce you to these approaches in this book and you can decide which fits you best, which is easier for you to use.

1『上面的这段是动态抓取的原理介绍，多读几遍。』

Starting to Code. After this lengthy introduction, it is time to write some code. I guess you are keen to get your fingers "dirty" and create your first scrapers. In this section we will write simple Python 3 scripts to get you started with scraping and to utilize some of the information you read previously in this chapter. These miniscripts won't be full-fledged applications, just small demos of what is awaiting you in this book.

Parsing robots.txt. Let's create an application that parses the robots.txt file of the target website and acts based on the contents. Python has a built-in module that is called robotparser, which enables us to read and understand the robots.txt file and ask the parser if we can scrape a given part of the target website. We will use the previously shown robots.txt file from Apress.com. To follow along, open your Python editor of choice, create a file called robots.py, and add the following code:

```
from urllib import robotparser

robot_parser = robotparser.RobotFileParser()

def prepare(robot_txt_url):
    robot_parser.set_url(robot_txt_url)
    robot_parser.read()

def is_allowed(target_url, user_agent='*'):
    return robot_parser.can_fetch(user_agent, target_url)

if __name__ == '__main__':
    prepare('http://www.apress.com/robots.txt')

    print(is_allowed('http://www.apress.com/covers/'))
    print(is_allowed('http://www.apress.com/gp/python'))
```

We should get back False and True, because we are not allowed to access the covers folder, but there is no restriction on the Python section. This code snippet is good if you write your own scraper and you don't use Scrapy. Integrating the robotparser and checking every URL before accessing it helps you automate the task of honoring the website owners' request what to access.

Previously, in this chapter, I mentioned that you can define user agent-specific restrictions in a robots.txt file. Because I have no access to the Apress website, I created a custom entry on my own homepage for this book and this entry looks like this:

```
User-Agent: bookbot 
Disallow: /category/software-development/java-softwaredevelopment/
```

Now to see how this works. For this, you must modify the previously written Python code (robots.py) or create a new one to provide a user agent when you call the is_allowed function because it already accepts a user agent as argument.

```
if __name__ == '__main__':
    prepare('http://hajba.hu/robots.txt')

    print(is_allowed('http://hajba.hu/category/softwaredevelopment/java-software-development/'), 'bookbot')
    print(is_allowed('http://hajba.hu/category/softwaredevelopment/java-software-development/'), 'my-agent')
    print(is_allowed('http://hajba.hu/category/softwaredevelopment/java-software-development/'), 'googlebot')
```

Unfortunately, you cannot prevent malicious bots from scraping your website because in most cases they will ignore the settings in your robots.txt file.

Creating a Link Extractor. After this lengthy introduction, it is time to create our first scraper, which will extract links from a given page. This example will be simple; we won't use any specialized tools for website scraping, just libraries available with the standard Python 3 installation. Let's open a text editor (or the Python IDE of your choice). We will work in a file called link_extractor.py.

The preceding code block extracts all the links, which you can find at the Apress homepage (on the first page only). If you run the code with the Python command link_extractor.py, you will see a lot of URLs that start with a slash (/) without any domain information. This is because those are internal links on the apress.com website. To fix this, we could manually look for such entries in the links set, or use a tool already present in the Python standard library: urljoin.

```
from urllib.request import urlopen, urljoin
import re

def download_page(url):
    return urlopen(url).read().decode('utf-8')

def extract_links(page):
    link_regex = re.compile('<a[^>]+href=["\'](.*?)["\']', re.IGNORECASE)
    return link_regex.findall(page)

if __name__ == '__main__':
    target_url = 'http://www.apress.com'
    apress = download_page(target_url)
    links = extract_links(apress)

    for link in links:
        print(urljoin(target_url, link))
```

As you can see, when you run the modified code, this new method adds http://www.apress.com to every URL that is missing this prefix, for example http://www.apress.com/gp/python, but leaves others like https://twitter.com/apress intact. The previous code example uses regular expressions to find all the anchor tags (\<a>) in the HTML code of the website. Regular expressions are a hard topic to learn, and they are not easy to write. That's why we won't dive deeper into this topic and will use more high-level tools, like Beautiful Soup, in this book to extract our contents.

Extracting Images. In this section we will extract image sources from the website. We won't download any images yet, just lay hands on the information about where these images are in the web. Images are very similar to links from the previous section, but they are defined by the \<img> tag and have a src attribute instead of an href. With this information you can stop here and try to write the extractor on your own. Following, you'll find my solution.

```
from urllib.request import urlopen, urljoin
import re

def download_page(url):
    return urlopen(url).read().decode('utf-8')

def extract_links(page):
    link_regex = re.compile('<img[^>]+src=["\'](.*?)["\']', re.IGNORECASE)
    return link_regex.findall(page)

if __name__ == '__main__':
    target_url = 'http://www.apress.com'
    apress = download_page(target_url)
    image_locations = extract_links(apress)

    for src in image_locations:
        print(urljoin(target_url, src))
```

If you take a close look, I modified just some variable names and the regular expression. I could have used the link extractor from the previous section and changed only the expression.

## 02. Enter the Requirements

### 1. 逻辑脉络

you've met the requirements, analyzed the website to scrape, and identified where in the HTML code the fields of interest lay. And you implemented a simple scraper, mostly with basic Python tools, which navigates through the website.

### 2. 摘录及评论

This chapter prepared you for the remaining parts of the book: you've met the requirements, analyzed the website to scrape, and identified where in the HTML code the fields of interest lay. And you implemented a simple scraper, mostly with basic Python tools, which navigates through the website. In the next chapter you will learn Beautiful Soup, a simple extractor library that helps you to forget regular expressions, and adds more features to traverse and extract HTML-trees like a boss.

After the introductory chapter, it is time to get you started with a real scraping project. In this chapter you will learn what data you must extract throughout the next two chapters, using Beautiful Soup and Scrapy. Don't worry; the requirements are simple. We will extract information from the following website: [Sainsbury's](https://www.sainsburys.co.uk/). Sainsbury's is an online shop with a lot of goods provided. This makes a great source for a website scraping project. I'll guide you to find your way to the requirements, and you'll learn how I approach a scraping project.

The Requirements. If you look at the website, you can see this is a simple web page with a lot of information. Let me show you which parts we will extract. One idea would be to extract something from the Halloween-themed site (see Figure 2-1. for their themed landing page). However, this is not an option because you cannot try this yourself; Halloween is over when you read this — at least for 2017, and I cannot guarantee that the future sales will be the same. Therefore, you will extract information on groceries. To be more specific, you will gather nutrition details from the "Meat & fish" department. For every entry, which has nutrition details, you extract the following information:

This looks like a lot, but do not worry! You will learn how to extract this information from all the products of this department with an automated script. And if you are keen and motivated, you can extend this knowledge and extract all the nutrition information for all the products.

Preparation. As I mentioned in the previous chapter, before you start your scraper development, you should look at the website's terms and conditions, and the robots.txt file to see if you can extract the information you need. When writing this part (November 2017), there was no entry on scraper restrictions in the terms and conditions of the website. This means, you can create a bot to extract information. The next step is to look at the robots.txt file, found at [https://www.sainsburys.co.uk/robots.txt](https://www.sainsburys.co.uk/robots.txt).

In the code block you can see what is allowed and what is not, and this robots.txt is quite restrictive and has only Disallow entries but this is for all bots. What can we find out from this text? For example, you shouldn't create bots that order automatically through this website. But this is unimportant for us because we only need to gather information — no purchasing. This robots.txt file has no limitations on our purposes; we are free to continue our preparation and scraping. What would limit our purposes? Good question. an entry in the robots.txt referencing the "meat & fish" department could limit our scraping intent. a sample entry would look like this:

```
User-agent: * 
Disallow: /shop/gb/groceries/meat-fish/ 
Disallow: /shop/gb/groceries/
```

But this won't allow search engines to look up the goods sainsbury's is selling, and that would be a big profit loss.

Navigating Through "Meat & fishFish". As mentioned at the beginning of this chapter, we will extract data from the "Meat & fish" department. The URL of this part of the website is www.sainsburys.co.uk/shop/gb/groceries/meat-fish. Let's open the URL in our Chrome browser, disable JavaScript, and reload the browser window as described in the previous chapter. Remember, disabling JavaScript enables you to see the website's HTML code as a basic scraper will see it.

For our purposes, the navigation menu on the left side is interesting. It contains the links to the pages where we will find products to extract. Let's use the selection tool (or hit CTRL-SHIFT-C) and select the box containing these links, as shown in Figure 2-3. 

1『选取元素的快捷键「commad+shiht+C」。』

Now we can see in the DevTools that every link is in a list element (\<li> tag) of an unordered list (\<ul>), with class categories departments. Note down this information because we will use it later.

Links, which have a little arrow pointing to the right (>), tell us they are just a grouping category and we will find another navigation menu beneath them if we click them. Let's examine the Roast dinner option, as shown in Figure 2-4. Here we can see that the page has no products but another list with links to detailed sites. If we look at the HTML structure in DevTools, we can see that these links are again elements of an unordered list. This unordered list has the class categories aisles.

Now we can go further into the Beef category, and here we have products listed (after a big filter box), as shown in Figure 2-5. Here we need to examine two things: one is the list of products; the other is the navigation. If the category contains more products than 36 (this is the default count to show on the website), the items will be split into multiple pages. Because we want to extract information on all products, we must navigate through all those pages. If we select the navigation, we can see it is again an unordered list of the class pages, as shown in Figure 2-6.

From those list elements, we are interested in the one with the rightpointing arrow symbol, which has the class next. This tells us if we have a next page we must navigate to or not. Now let's find the link to the detail page of the products. All the products are in an unordered list (again). This list has the class productLister gridView, as shown in Figure 2-7.

Every product is in a list element with the class gridItem. If we open up the details of one of those products we can see where the navigation link is: located in some divs and an h3. We note that the last div has the class productNameAndPromotions, as shown in Figure 2-8. Now we reached the level of the products, and we can step further and concentrate on the real task: identifying the required information.

Selecting the Required Information. We will discover the elements where our required information resides, based on the product shown in Figure 2-9. Now that we have the product, let's identify the required information. As previously, we can use the select tool, locate the required text, and read the properties from the HTML code. 

The name of the product is inside a header (h1), which is inside a div with the class productTitleDescriptionContainer. The price and the unit are in a div of the class pricing. The price itself is in a paragraph (p) of the class pricePerUnit; the unit is in a span of the class pricePerUnitUnit. 

Extracting the rating is tricky because here we only see the stars for the rating, but we want the numeric rating itself. Let's look at the image's HTML definition, as shown in Figure 2-10. We can see the location of the image is inside a label of class numberOfReviews and it has an attribute, alt, which contains the decimal value of the averages of the reviews. After the image, there is the text containing the number of the reviews. The item code is inside a paragraph of class itemCode.

The nutrition information, as shown in Figrue 2-11, is inside a table of class nutritionTable. Every row (tr) of this table contains one entry of our required data: the header (th) of the row has the name and the first column (td) contains the value. The only exception is the energy information, because two rows contain the values but only the first one the header. As you will see, we will solve this problem too with some specific code.

The country of origin, as shown in Figure 2-12, is inside a paragraph of a div of class productText. This field is not unique: every description is in a productText div. This will make the extraction a bit complicated, but there is a solution for this too. Even though we must extract many fields, we identified them easily in the website. Now it is time to extract the data and learn the tools of the trade!

Outlining the Application. After the requirements are defined and we've found each entry to extract, it is time to plan the applications structure and behavior.

If you think a bit about how to approach this project, you will start with big-bang, "Let's hammer the code" thinking. But you will realize later that you can break down the whole script into smaller steps. One example can be the following: 1) Download the starting page, in this case the "Meat & fish" department, and extract the links to the product pages. 2) Download the product pages and extract the links to the detailed products. 3) Extract the information we are interested in from the already downloaded product pages. 4) Export the extracted information.

And these steps could identify functions of the application we are developing. Step 1 has a bit more to offer: if you remember the analysis with DevTools you have seen, some links are just a grouping category and you must extract the detail page links from this grouping category.

Navigating the Website. Before we jump into learning the first tools you will use to scrape website data, I want to show you how to navigate websites — and this will be another building block for scrapers. Websites consist of pages and links between those pages. If you remember your mathematic studies, you will realize a website can be depicted as a graph, as shown in Figure 2-13. Because a website is a graph, you can use graph algorithms to navigate through the pages and links: Breadth First Search (BFS) and Depth First Search (DFS).

Using BFS, you go one level of the graph and gather all the URLs you need for the next level. For example, you start at the "Meat & fish" department page and extract all URLs to the next required level, like "Top sellers" or "Roast dinner." Then you have all these URLs and go to the Top sellers and extract all URLs that lead to the detailed product pages. After this is done, you go to the "Roast dinner" page and extract all product details from there too, and so on. At the end you will have the URLs to all product pages, where you can go and extract the required information.

Using DFS, you go straight to the first product through "Meat & fish," "Top sellers," and extract the information from its site. Then you go to the next product on the "Top sellers" page and extract the information from there. If you have all the products from "Top sellers" then you move to "Roast dinner" and extract all products from there.

1『两个抓取算法：BFS 和 DFS。』

If you ask me, both algorithms are good, and they deliver the same result. I could write two scripts and compare them to see which one is faster, but this comparison would be biased and flawed.1 Therefore, you will implement a script that will navigate a website, and you can change the algorithm behind it to use BFS or DFS. If you are interested in the Why? for both algorithms, I suggest you consider Magnus Hetland's book: Python Algorithms.2 

2『参考 1 的链接：[Java theory and practice: Anatomy of a flawed microbenchmark](https://www.ibm.com/developerworks/library/j-jtp02225/index.html)；参考 2，已下载书籍「2020065Python_Algorithms」。』

Creating the Navigation. Implementing the navigation is simple if you look at the algorithms, because this is the only trick: implement the pseudo code. OK, I was a bit lazy, because you need to implement the link extraction too, which can be a bit complex, but you already have a building block from Chapter 1 and you are free to use it.

```
def extract_links(page):
    if not page:
        return []
    link_regex = re.compile('<a[^>]+href=["\'](.*?)["\']', re.IGNORECASE)
    return [urljoin(page,link) for link in link_regex.findall(page)]

def get_links(page_url):
    host = urlparse(page_url)[1]
    page = download_page(page_url)
    links = extract_links(page)
    return [link for link in links if urlparse(link)[1] == host]
```

The two functions shown extract the page, and the links still point to the Sainsbury's website. Note if you don't filter out external urLs, your script may never end. this is only useful if you want to navigate the whole WWW to see how far you can reach from one website.

The extract_links function takes care of an empty or None page. urljoin wouldn't bleat about this but re.findall would throw an exception and you don't want that to happen. The get_links function returns all the links of the web page that point to the same host. To find out which host to use, you can utilize the urlparse function, 3 which returns a tuple. The second parameter of this tuple is the host extracted from the URL. Those were the basics; now come the two search algorithms. If you look at the two functions just shown, you will see only one difference in their code (hint: it's highlighted): how you put them into the queue, which is a stack.

```
def depth_first_search(start_url):
    from collections import deque
    visited = set()
    queue = deque()
    queue.append(start_url)
    while queue:
        url = queue.popleft()
        if url in visited:
            continue
        visited.add(url)
        for link in get_links(url):
            queue.appendleft(link)
        print(url)

def breadth_first_search(start_url):
    from collections import deque
    visited = set()
    queue = deque()
    queue.append(start_url)
    while queue:
        url = queue.popleft()
        if url in visited:
            continue
        visited.add(url)
        queue.extend(get_links(url))
        print(url)
```

The requests Library. To implement the script successfully, you must learn a bit about the requests library. I really like the extendedness of the Python core library, but sometimes you need libraries developed by members of the community. And the requests library is one of those.

With basic Python urlopen you can create simple requests and corresponding data, but it is complex to use. The requests library adds a friendly layer above this complexity and makes network programming easy: it takes care of redirects, and can handle sessions and cookies for you. The Python documentation recommends it as the tool to use. Again, I won't give you a detailed introduction into this library, just the necessary information to get you going. If you need more information, look at the project's website.4 

Getting Pages. Requesting pages is easy with the requests library: requests.get(url). This returns a response object that contains basic information, like status code and content. The content is most often the body of the website you requested, but if you requested some binary data (like images or sound files) or JSON, then you get that back. For this book, we will focus on HTML content. You can get the HTML content from the response by calling its text parameter:

```
import requests

r = requests.get('http://wwww.baidu.com')
if r.status_code == 200:
    print(r.text[:250])
else:
    print(r.status_code
```

The preceding code block requests my website's front page, and if the server returns the status code 200, which means OK, it prints the first 250 characters of the content. If the server returns a different status, that code is printed. 

With this we are through the basics of the requests library. As I introduce more concepts of the library later in this book, I will tell you more about it. Now it is time to skip the default urllib calls of Python 3 and change to requests.

Switching to requests. Now it is time to finish the script and use the requests library for downloading the pages. By now you know already how to accomplish this, but here is the code anyway.

```
def download_page(url):
    try:
        return requests.get(url).text
    except:
        print('error in the url', url)
```

I surrounded the requesting method call with a try-except block because it can happen that the content has some encoding issues and we get an exception back that kills the whole application; and we don't want this because the website is big and starting over would require too much resources.5 

Putting the Code Together. Now if you put everything together and run both functions with 'https://www.sainsburys.co.uk/shop/gb/groceries/meat-fish' as starting_url, then you should get a similar result to this one. As you can see from the printed URLs, the current solution is rudimentary: the code navigates the whole website instead of focusing only on the “Meat & fish” department and nutrition details. One option would be to extend the filter to return only relevant links, but I don't like regular expressions because they are hard to read. Instead let's go ahead to the next chapter.

## 03. Using Beautiful Soup

### 1. 逻辑脉络

how to use Beautiful Soup and requests together, and you created your first full scraper application.

### 2. 摘录及评论

In this chapter you learned a lot, such as how to use Beautiful Soup and requests together, and you created your first full scraper application, which gathers the requirements from Chapter 2. The scraper exported the gathered results into different stores, like CSV, JSON, and databases. But every rose has its thorn: you learned about bottlenecks of this simpler solution, and applied some techniques to make it perform better. And with this you’ve learned how complex it can be to write your own scraper.

And even with such a lengthy chapter, there are some points still untouched, for example, honoring the robots.txt file. You can extend the code from this chapter to honor the robots.txt file of the website; you have the building blocks to do so. In the next chapter you will learn Scrapy, the website scraping tool for Python, which leverages these optimizations from your shoulders. The only things you must do are create the extractor code and configure Scrapy properly.

In this chapter, you will learn how to use Beautiful Soup, a lightweight Python library, to extract and navigate HTML content easily and forget overly complex regular expressions and text parsing. Before I let you jump right into coding, I will tell you some things about this tool to familiarize yourself with it. Feel free to jump to the next section if you are not in the mood for reading dry introductory text or basic tutorials; and if you don’t understand something in my later approach or the code, come back here.

I find Beautiful Soup easy to use, and it is a perfect tool for handling HTML DOM elements: you can navigate, search, and even modify a document with this tool. It has a superb user experience, as you will see in the first section of this chapter.

Simple Examples. After a lengthy introduction, it is time to start coding now, with simple examples to familiarize yourself with Beautiful Soup and try out some basic features without creating a complex scraper. These examples will show the building blocks of Beautiful Soup and how to use them if needed. You won’t scrape an existing site, but instead will use HTML text prepared for each use case.

3『

[python - Difference between BeautifulSoup and Scrapy crawler? - Stack Overflow](https://stackoverflow.com/questions/19687421/difference-between-beautifulsoup-and-scrapy-crawler)

Scrapy is a Web-spider or web scraper framework, You give Scrapy a root URL to start crawling, then you can specify constraints on how many (number of) URLs you want to crawl and fetch, etc. It is a complete framework for web-scraping or crawling.

While BeautifulSoup is a parsing library which also does a pretty good job of fetching contents from URL and allows you to parse certain parts of them without any hassle. It only fetches the contents of the URL that you give and then stops. It does not crawl unless you manually put it inside an infinite loop with certain criteria.

In simple words, with Beautiful Soup you can build something similar to Scrapy. Beautiful Soup is a library while Scrapy is a complete framework.

』

Parsing HTML Text. The very basic usage of Beautiful Soup, which you will see in every tutorial, is parsing and extracting information from an HTML string. This is the basic step, because when you download a website, you send its content to Beautiful Soup to parse, but there is nothing to see if you pass a variable to the parser. You will work most of the time with the following multiline string:

To create a parse tree with Beautiful Soup, just write the following code. The second argument to the function call defines which parser to use. If you don’t provide any parser, you will get an error message like this:

    soup = BeautifulSoup(example_html, 'html.parser')

1『jupyter-notenook 进 Jupyter 里练习。』

This warning is well defined and tells you everything you need to know. Because you can use different parsers with Beautiful Soup (see later in this chapter), you cannot assume it will always use the same parser; if a better one is installed, it will use that. Moreover, this can lead to unexpected behavior, for example, your script slows down. Now you can use the soup variable to navigate through the HTML.

Parsing Remote HTML. Beautiful Soup is not an HTTP client, so you cannot send URLs to it to do extraction. You can try it out.

    soup = BeautifulSoup('http://hajba.hu', 'html.parser')

The preceding code results in a warning message like this one: UserWarning: "http://hajba.hu" looks like a URL. Beautiful Soup is not an HTTP client. You should probably use an HTTP client like requests to get the document behind the URL, and feed that document to Beautiful Soup. To convert remote HTML pages into a soup, you should use the requests library.

    soup = BeautifulSoup(requests.get('http://hajba.hu').text, 'html.parser')

Parsing a File. The third option to parse content is to read a file. You don’t have to read the whole file; it is enough for Beautiful Soup if you provide an open file handle to its constructor and it does the rest.

```
with open('example.html') as infile:
    soup = BeautifulSoup(infile , 'html.parser')
```

Difference Between find and find_all. You will use two methods excessively with Beautiful Soup: find and find_all. The difference between these two lies in their function and return type: find returns only one — if multiple nodes match the criteria, the first is returned; None, if nothing is found. find_all returns all results matching the provided arguments as a list; this list can be empty.

This means, every time you search for a tag with a certain id, you can use find because you can assume that an id is used only once in a page. Alternatively, if you are looking for the first occurrence of a tag, then you can use find too. If you are unsure, use find_all and iterate through the results.

Extracting All Links. The core function of a scraper is to extract links from the website that lead to other pages or other websites. Links are in anchor tags (\<a>), and where they point to is in the href attribute of these anchors. To find all anchor tags that have an href attribute, you can use following code:

```
links = soup.find_all('a', href=True) 
for link in links:
    print(link['href'])
```

Running this code against the previously introduced HTML, you get the following result. The find_all method call includes the href=True argument. This tells Beautiful Soup to return only those anchor tags that have an href attribute. This gives you the freedom to access this attribute on resulting links without checking their existence. To verify this, try running the preceding code, but remove the href=True argument from the function call. It results in an exception because the empty anchor doesn’t have an href attribute. You can add any attribute to the find_all method, and you can search for tags where the attribute is not present too.

Extracting All Images. The second biggest use case for scrapers is to extract images from websites and download them or just store their information, like where they are located, their display size, alternative text, and much more. Like the link extractor, here you can use the find_all method of the soup, and specify filter tags.

    images = soup.find_all('img', src=True) 

Looking for a present src attribute helps to find images that have something to display. Naturally, sometimes the source attribute is added through JavaScript, and you must do some reverse engineering — but this is not the subject of this chapter.

Finding Tags Through Their Attributes. Sometimes you must find tags based on their attributes. For example, we identified HTML blocks for the requirements in the previous chapter through their class attribute. The previous sections have shown you how to find tags where an attribute is present. Now it’s time to find tags whose attributes have certain values. Two use cases dominate this topic: searching by id or class attributes.

```
soup.find('p', id='first') 
soup.find_all('p', class_='paragraph')
```

You can use any attribute in the find and find_all methods. The only exception is class because it is a keyword in Python. However, as you can see, you can use class_ instead. This means you can search for images, where the source is clouds.jpg.

    soup.find('img', src='clouds.jpg')

You can use regular expressions too to find tags that are of a specific type, and their attributes qualify them through some condition. For example, all image tags that display GIF files.

    soup.find('img', src=re.compile('\.gif$'))

Moreover, the text of a tag is one of its attributes too. This means you can search for tags that contain a specific text (or just a fragment of a text).

```
soup.find_all('p', text='paragraph') 
soup.find_all('p', text=re.compile('paragraph'))
```

The difference between the two preceding examples is their result. Because in the example HTML there is no paragraph that contains only the text “paragraph”, an empty list is returned. The second method call returns a list of paragraph tags that contain the word “paragraph.”

Finding Multiple Tags Based on Property. Previously, you have seen how to find one kind of tag (\<p>, \<img>) based on its properties. However, Beautiful Soup offers you other options too: for example, you can find multiple tags that share the same criteria. Look at the next example:

```
for tag in soup.find_all(re.compile('h')):
    print(tag.name)
```

Here, you search for all tags that start with an h. The result would be something like this.

    html head hr h1 h2 hr

Another example would be to find all tags that contain the text “paragraph.”

    soup.find_all(True, text=re.compile('paragraph'))

Here you use the True keyword to match all tags. If you don’t provide an attribute to narrow the search, you will get back a list of all tags in the HTML document.

Changing Content. I rarely use this function of Beautiful Soup, but valid use cases exist. Therefore I think you should learn about how to change the contents of a soup. Moreover, because I don’t use this function a lot, this section is skinny and won’t go into deep details.

Adding Tags and Attributes. Adding tags to the HTML is easy, though it is seldom used. If you add a tag, you must take care where and how you do it. You can use two methods: insert and append. Both work on a tag of the soup. insert requires a position where to insert the new tag, and the new tag itself. append requires only the new tag to append the new tag to the parent tag’s end on which the method is called. Because the soup itself is a tag, you can use these methods on it too, but you must take care. For example, try out the following code:

```
h2 = soup.new_tag('h2') 
h2.string = 'This is a second-level header' 
soup.insert(0, h2)
```

Here you want to insert the new tag, h2, into the soup at first place. This results in the following code (I omitted most of the HTML):

    <h2>This is a second-level header</h2><html>

Alternatively, you can change the 0 to a 1, to insert the new tag at the second position. In this case, your tag is inserted at the end of the HTML, after the \</html> tag.

    soup.insert(1, h2)

This results in

    </html><h2>This is a second-level header</h2>

For the two methods just shown, there are convenience methods too: insert_before, insert_after. The append method appends the new tag at the end of the tag. This means it behaves like the insert_after method.

    soup.append(soup.new_tag('p'))

The preceding code results in the following:

    </html><p></p>

The only difference is that the insert_after method is not implemented on soup objects, just on tags. Anyway, with these methods you must pay attention where you insert or append new tags into the document. Adding attributes to the tags is easy. Because tags behave like dictionaries, you can add new attributes the way you add keys and values to dictionaries.

    soup.head['style'] = 'bold'

Even though the preceding code doesn’t affect the rendered output, it added the new attribute to the head tag.

    <head style="bold">

Changing Tags and Attributes. Sometimes you don’t want to add new tags but want to change existing content. For example, you want to change the contents of paragraphs to be bold.

```
for p in soup.find_all('p', text=True):
    p.string.wrap(soup.new_tag('b'))
```

If you would like to change the contents of a tag that contains some formatting (like bold or italic tags), but you want to retain the contents, you can use the unwrap function.

```
soup = BeautifulSoup('<p> This is a <b>new</b> paragraph!</p>') 
p = soup.p.b.unwrap() 
print(soup.p)
```

Another example would be to change the id or the class of a tag. This works the same way as with adding new attributes: you can get the tag from the soup, and change the dictionary values.

```
for t in soup.findAll(True, id=True):
    t['class'] = 'withid' 
    print(t)
```

The preceding example changes (or adds) the class withid to all tags that have an id attribute.

Deleting Tags and Attributes. If you want to delete a tag, you can use either extract() or decompose() on the tag. extract() removes the tag from the tree and returns it, so you can use it in the future or add it to the HTML content at a different position. decompose() deletes the selected tag permanently. No return values, no later usage; it is gone forever.

```
print(soup.title.extract()) 
print(soup.head)
```

Running the preceding code example with the example HTML of this section results in the following lines:

```
<title>Your Title Here</title> 
<head>
</head>
```

Alternatively, you can change extract() to decompose().

```
print(soup.title.decompose()) 
print(soup.head)
```

Here, the result changes only in the first line where you don’t get back anything.

```
None <head>

</head>
```

Deletion doesn’t only work for tags; you can remove attributes of tags too. Imagine, you have tags that have an attribute called display, and you want to remove this display attribute from each tag. You can do it the following way:

```
for tag in soup.find_all(True, display=True):
    del tag['display']
```

If you now count the occurrences of tags having a display attribute, you will get 0.

    print(len(soup.find_all(True, display=True)))

Finding Comments. Sometimes you need to find comments in HTML code to reverse-engineer JavaScript calls, because sometimes the content of a website is delivered in a comment and JavaScript renders it properly. The preceding code finds and prints contents of all comments. To make it work, you need to import Comments from the bs4 package too.

```
for comment in soup.find_all(text=lambda text:isinstance (text, Comment)):
    print(comment)
```

Converting a Soup to HTML Text. This is one of the easiest parts for Beautiful Soup because as you may know from your Python studies, everything is an object in Python, and objects have a method \__str__ that returns the string representation of this object. Instead of writing something like soup.__str__() every time, this method is called every time you convert the object to a string — for example when you print it to the console: print(soup).

However, this results in the same string representation as you provided in the HTML content. Moreover, you know, you can do better and provide a formatted string. That’s why Beautiful Soup has the prettify method. Per default, this method prints the pretty formatted version of the selected tag-tree. Yes, this means you can prettify your whole soup or just a selected subset of the HTML content.

    print(soup.find('p').prettify())

This call results in (soup was created using the HTML from the beginning of this section)

```
<p> 
This is a new paragraph! 
</p>
```

Extracting the Required Information. Now it is time to prepare your fingers and keyboard because you are about to create your first dedicated scraper, which will extract the required information, introduced in Chapter 2, from the Sainsbury’s website.

Identifying, Extracting, and Calling the Target URLs. The first step in creating the scraper is to identify the links that lead us to product pages. In Chapter 2 we used Chrome’s DevTools to find the corresponding links and their locations. Those links are in an unordered list (\<ul>), which has the class categories departments. You can extract them from the page with following code:


```
links = []
ul = soup.find('ul', class_='categories departments')
if ul:
    for li in ul.find_all('li'):
        a = li.find('a',href=True)
        if a:
            links.append(a['href'])
```

You now have the links that lead to pages listing products, each showing 36 at most. However, some of these links lead to other groupings, which can lead to a third layer of grouping before you reach the product pages, just as you can see in Figure 3-1.

The navigation goes from “Chicken & turkey” to “Sauces, marinades & Yorkshire puddings,” which leads to the third layer of links. Therefore, your script should be able to navigate such chains too and get to the product listings.

```
product_pages = []
visited = set()
queue = deque()
queue.extend(department_links)
while queue:
    link = queue.popleft()
    if link in visited:
        continue
    visited.add(link)
    soup = get_page(link)
    ul = soup.find('ul', class_='produtlister gridView')
    if ul:
        product_pages.append(link)
    else:
        ul = soup.find('ul', class_='categories aisles')
        if not ul:
            continue
        for li in ul.find_all('li'):
            a = li.find('a', href=True)
            if a:
                queue.append(a['href'])
```

The preceding code uses the simple Breadth First Search (BFS) from the previous chapter to navigate through all the URLs until it finds the product lists. You can change the algorithm to Depth First Search(DFS); this results in a logically cleaner solution because if your code finds a URL that points to a navigation layer, it digs deeper until it finds all the pages.

The code looks first for shelves (categories shelf), which are the last layer of navigation prior to extracting categories aisles. This is because if it would extract aisles first and because all those URLs are already visited, the shelves and their content will be missing.

1『网站最新的布局里没有「categories shelf」层了，所以调整了作者的代码。』

Navigating the Product Pages. In Chapter 2 you have seen that products can be listed on multiple pages. To gather information about every product, you need to navigate between these pages. If you are lazy like me, you might come up with the idea to use the filter and set the product count to 108 per page, just like in Figure 3-2. Even though this is a good idea, it can happen that a category holds at least 109 products — and in this case, you need to navigate your script.

```
product_pages = []
visited = set()
queue = deque()
queue.extend(department_links)
while queue:
    link = queue.popleft()
    if link in visited:
        continue
    visited.add(link)
    soup = get_page(link)
    ul = soup.find('ul', class_='produtlister gridView')
    if ul:
        product_pages.append(link)
    else:
        ul = soup.find('ul', class_='categories aisles')
        if not ul:
            continue
        for li in ul.find_all('li'):
            a = li.find('a', href=True)
            if a:
                queue.append(a['href'])
```

The preceding code block navigates through all the product lists and adds the URLs of the product sites to the list of products. I used a BFS again, and a DFS would be OK too. The interesting thing is the handling of the next pages: you don’t search for the numbering of the navigation but consecutively for the link pointing to the next page. This is useful for bigger sites, where you have umpteen-thousand pages. They won’t be listed on the first site.1 

1 Unless you are lucky. Once I encountered a site where all the links to the remaining pages were there in the HTML code but had been hidden with some JS-magic.

Extracting the Information. You arrived at the product page. Now it is time to extract all the information required. Because you already identified and noted the locations in Chapter 2, it will be a simple task to wire everything together. Depending on your preferences, you can use dictionaries, named tuples, or classes to store information on a product. Here, you will create code using dictionaries and classes.

Using Dictionaries. The first solution you create will store the extracted information of products in dictionaries. The keys in the dictionary will be the fields’ names (which will be later used as a header in a CSV [Comma Separated Value], for example), the value the extracted information. Because each product you extract has a URL, you can initialize the dictionary for a product as follows:

    product = {'url': url}

I could list here how to extract all the information required, but I will only list the tricky parts. The other building blocks you should figure out yourself, as an exercise. You can take a break, put down the book and try to implement the extractor. if you struggle with nutrition information or product origin, you will find help below. if you are lazy, you can go ahead and find my whole solution later in this section or look at the source code provided for this book.

For me, the most interesting and lazy part is the extraction of the nutrition information table. It is a lazy solution because I used the table row headings as keys in the dictionary to store the values. They match the requirements, and therefore there is no need to add custom code that reads the table headers and decides which value to use.

```
table = soup.find('table', class_='nutritionTable') 
if table:
    rows = table.findAll('tr') 
    for tr in rows[1:]:
        th = tr.find('th', class_='rowHeader')
        td = tr.find('td') 
        if not th:
            product['Energy kcal'] = td.text 
        else:
            product[th.text] = td.text
```

Extracting the product’s origin was the most complicated part, at least in my eyes. Here you needed to find a header (\<h3>) that contains a specific text and then its sibling. This sibling holds all the text but in a sheer format, which you need to make readable.

```
product_origin_header = soup.find('h3', class_='productDataItemHeader', text='Country of Origin')
if product_origin_header:
    product_text = product_origin_header.find_next_sibling ('div', class_='productText') 
    if product_text:
        origin_info = [] 
        for p in product_text.find_all('p'):
            origin_info.append(p.text.strip()) 
    product['Country of Origin'] = '; '.join (origin_info)
```

After implementing a solution, I hope you’ve got something similar to the following code:

As you can see in the preceding code, this is the biggest part of the scraper. But hey! You finished your very first scraper, which extracts meaningful information from a real website. What you have probably noticed is the caution implemented in the code: every HTML tag is verified. If it does not exist, no processing happens; it would be a disaster and the application would crash. The regular expressions to extract item codes and review counts is again a lazy way. Even though I am not a regex guru, I can create some simple patterns and use them for my purposes.

```
reviews_pattern = re.compile("Reviews \((\d+)\)") 
item_code_pattern = re.compile("Item code: (\d+)")
```

Using Classes. You can implement the class-based solution similarly to the dictionarybased one. The only difference is in the planning phase: while using a dictionary you don’t have to plan much ahead, but with classes, you need to define the class model. For my solution, I used a simple, pragmatic approach and created two classes: one holds the basic information; the second is a key-value pair for nutrition details. I don’t plan to go deep into OOP 2 concepts. If you want to learn more, you can refer to different Python books. As you already know, filling these objects is different too. There are different options for how to solve such a problem, 3 but I used a lazy version where I access and set every field directly.

『3 For example, the Builder or Factory patterns, a constructor with all arguments.』

Unforeseen Changes. While implementing the source code yourself, you may have found some problems and needed to react. One of such changes could be the nutrition table. Even though we scrape one website, the rendering is not the same for all pages. Sometimes they display different elements or different styles. Moreover, sometimes the nutrition table contains different values than in the requirements, just like in Figures 3-3 and 3-4.

What to do in such cases? Well, first, mention to your customer (if you have any) that you’ve found tables that contain nutrition information but in different details and format. Then think out a solution that is good for the outcome, and you don’t have to create extra errands in your code to let it happen.

In my case, I went with the easiest solution and exported all I could from those tables. This means my results have fields that are not in the requirements and some can be missing, like Total sugars. Moreover, because the sublist of fats and carbohydrates has awkward dashes before each entry, or there are rows that contain only the text “of which,” I adjusted the preceding code a bit to handle these cases.

```
table = soup.find('table', class_='nutritionTable') 
if table:
    rows = table.findAll('tr') 
    for tr in rows[1:]:
        th = tr.find('th', class_='rowHeader')
        td = tr.find('td') 
        if not td:
            continue 
        if not th:
            product['Energy kcal'] = td.text 
        else:
            product[th.text.replace('-', ").strip()] = td.text
```

The exceptional case of Energy and Energy kcal (if not th) in the preceding code is fixed automatically in tables, which provide labels for every row. such changes are inevitable. even though you get requirements and prepare your scraping process, exceptions in the pages can occur. therefore, always be prepared and write code that can handle the unexpected, and you don’t have to redo all the work. You can read more about how i deal with such thing later in this chapter.

1『代码里一定要考虑出现异常情况时的处理措施，异常情况是避免不了的，至少要保证能抓取的数据先出来。』

Exporting the Data. Now that all information is gathered, we want to store it somewhere because keeping it in memory does not have much use for our customer. In this section, you will see basic approaches to how you can save your information into a CSV or JSON file, or into a relational database, which will be SQLite. Each subsection will create code for the following export objects: classes and dictionaries.

To CSV. A good old friend to store data is CSV. Python provides built-in functionality to export your information into this file type. Because you implemented two solutions in the previous section, you will now create exports for both. But don’t worry; you will keep both solutions simple. The common part is the csv module of Python. It is integrated and has everything you need.

Quick Glance at the csv Module. Here you get a quick introduction into the csv module of the Python standard library. If you need more information or reference, you can read it online.4 I will focus on writing CSV files in this section; here I present the basics to give you a smooth landing on the examples where you write the exported information into CSV files.

for the code examples, i assume you did import csv. Writing CSV files is easy: if you know how to write files, you are almost done. You must open a file-handle and create a CSV writer.

```
with open('result.csv', 'w') as outfile: 
    spamwriter = csv.writer(outfile)
```

The preceding code example is the simplest example I can come up with. However, there are a lot more options to configure, which sometimes will be important for you.

1. dialect: With the dialect parameter, you can specify formatting attributes grouped together to represent a common formatting. Such dialects are excel (the default dialect), excel_tab, or unix_dialect. You can define your own dialects too.

2. delimiter: If you do/don’t specify a dialect, you can customize the delimiter through this argument. This can be needed if you must use some special character for delimiting purposes because comma and escaping don’t do the trick, or your specifications are restrictive.

3. quotechar: As its name already mentions, you can override the default quoting. Sometimes your texts contain quote characters and escaping results in unwanted representations in MS Excel.

4. quoting: Quoting occurs automatically if the writer encounters the delimiter inside a field’s value. You can override the default behavior, and you can completely disable quoting (although I don’t encourage you to do this).

5. lineterminator: This setting enables you to change the character at the line’s ending. It defaults to '\r\n' but in Windows you don’t want this, just '\n'.

Most of the time, you are good to go without changing any of these settings (and relying on the Excel configuration). However, I encourage you to take some time and try out different settings. If something is wrong with your dataset and the export configuration, you’ll get an exception from the csv module—and this is bad if your script already scraped all the information and dies at the export.

Line Endings. If you’re working in a Windows environment like I do most of the time, it is a recommended practice to set the line ending for your writer. If not, you will get unwanted results.

```
with open('result.csv', 'w') as outfile: 
    spamwriter = csv.writer(outfile) 
    spamwriter.writerow([1,2,3,4,5]) 
    spamwriter.writerow([6,7,8,9,10])
```

The preceding code results in the CSV file in Figure 3-5. To fix this, set the lineterminator argument to the writer’s creation.

```
with open('result.csv', 'w') as outfile:
    spamwriter = csv.writer(outfile, lineterminator='\n') 
    spamwriter.writerow([1,2,3,4,5]) 
    spamwriter.writerow([6,7,8,9,10])
```

Headers. What are CSV files without a header? Useful for those who know what to expect in which order, but if the order or number of columns changes, you can expect nothing good. Writing the header works the same as writing a row: you must do it manually.

```
with open('result.csv', 'w') as outfile:
    spamwriter = csv.writer(outfile, lineterminator='\n') 
    spamwriter.writerow(['average', 'mean', 'median', 'max', 'sum']) 
    spamwriter.writerow([1,2,3,4,5]) 
    spamwriter.writerow([6,7,8,9,10])
```

