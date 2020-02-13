# 01 Getting Started

Instead of installation instructions, which follow later for each library, we will dive right into deep water: this chapter introduces website scraping in general and the requirements we will implement throughout this book.

You may expect a thorough introduction into website scraping, but because you are reading this book I expect you already know what website scraping is and you want to learn how to do it with Python.

Therefore, I’ll just give you a glance at the topic and jump right into the depths of creating a script that scrapes websites!

## 01. Website Scraping

The need to scrape websites came with the popularity of the Internet, where you share your content and a lot of data. The first widely known scrapers were invented by search engine developers (like Google or AltaVista). These scrapers go through (almost) the whole Internet, scan every web page, extract information from it, and build an index that you can search.

Everyone can create a scraper. Few of us will try to implement such a big application, which could be new competition to Google or Bing. But we can narrow the scope to one or two web pages and extract information in a structured manner — and get the results exported to a database or structured file (JSON, CSV, XML, Excel sheets).

Nowadays, digital transformation is the new buzzword companies use and want to engage. One component of this transformation is providing data access points to everyone (or at least to other companies interested in that data) through APIs. With those APIs available, you do not need to invest time and other resources to create a website scraper.

Even though providing APIs is something scraper developers won’t benefit from, the process is slow, and many companies don’t bother creating those access points because they have a website and it is enough to maintain.

### 1. Projects for Website Scraping

There are a lot of use cases where you can leverage your knowledge of website scraping. Some might be common sense, while others are extreme cases. In this section you will find some use cases where you can leverage your knowledge.

The main reason to create a scraper is to extract information from a website. This information can be a list of products sold by a company, nutrition details of groceries, or NFL results from the last 15 years. Most of these projects are the groundwork for further data analysis: gathering all this data manually is a long and error-prone process.

Sometimes you encounter projects where you need to extract data from one website to load it into another—a migration. I recently had a project where my customer moved his website to WordPress and the old blog engine’s export functionality wasn’t meant to import it into WordPress. I created a scraper that extracted all the posts (around 35,000) with their images, did some formatting on the contents to use WordPress short codes, and then imported all those posts into the new website.

A weird project could be to download the whole Internet! Theoretically it is not impossible: you start at a website, download it, extract and follow all the links on this page, and download the new sites too. If the websites you scrape all have links to each other, you can browse (and download) the whole Internet. I don’t suggest you start this project because you won’t have enough disk space to contain the entire Internet, but the idea is interesting. Let me know how far you reached if you implement a scraper like this.

### 2. Websites Are the Bottleneck

One of the most difficult parts of gathering data through websites is that websites differ. I mean not only the data but the layout too. It is hard to create a good-fit-for-all scraper because every website has a different layout, uses different (or no) HTML IDs to identify fields, and so on.

And if this is not enough, many websites change their layout frequently. If this happens, your scraper is not working as it did previously. In these cases, the only option is to revisit your code and adapt it to the changes of the target website.

Unfortunately, you won’t learn secret tricks that will help you create a scraper that always works—if you want to write specialized data extractors. I will show some examples in this book that will always work if the HTML standard is in use.

### 3. Tools in This Book

In this book you will learn the basic tools you can use in Python to do your website scraping. You will soon realize how hard it is to create every single piece of a scraper from scratch.

But Python has a great community, and a lot of projects are available to help you focus on the important part of your scraper: data extraction.

I will introduce you to tools like the requests library, Beautiful Soup, and Scrapy.

The requests library is a lightweight wrapper over the tedious task of handling HTTP, and it emerged as the recommended way:

The Requests package is recommended for a higher level HTTP client interface.

— Python 3 documentation

Beautiful Soup is a content parser. It is not a tool for website scraping because it doesn’t navigate pages automatically and it is hard to scale. But it aids in parsing content, and gives you options to extract the required information from XML and HTML structures in a friendly manner.

Scrapy is a website scraping framework/library. It is much more powerful than Beautiful Soup, and it can be scaled. Therefore, you can create more complex scrapers easier with Scrapy. But on the other side, you have more options to configure. Fine-tuning Scrapy can be a problem, and you can mess up a lot if you do something wrong. But with great power comes great responsibility: you must use Scrapy with care.

Even though Scrapy is the Python library created for website scraping, sometimes I just prefer a combination of requests and Beautiful Soup because it is lightweight, and I can write my scraper in a short period—and I do not need scaling or parallel execution.

## 02. Preparation

When starting a website scraper, even if it is a small script, you must prepare yourself for the task. There are some legal and technical considerations for you right at the beginning.

In this section I will give you a short list of what you should do to be prepared for a website scraping job or task:

1. Do the website’s owners allow scraping? To find out, read the Terms & Conditions and the Privacy Policy of the website.

2. Can you scrape the parts you are interested in? See the robots.txt file for more information and use a tool that can handle this information.

3. What technology does the website use? There are free tools available that can help you with this task, but you can look at the website’s HTML code to find out.

4. What tools should I use? Depending on your task and the website’s structure, there are different paths you can choose from.

Now let’s see a detailed description for each item mentioned.

### 1. Terms and Robots

Scraping currently has barely any limitations; there are no laws defining what can be scraped and what cannot.

However, there are guidelines that define what you should respect. There is no enforcing; you can completely ignore these recommendations, but you shouldn’t.

Before you start any scraping task, look at the Terms & Conditions and Privacy Policy of the website you want to gather data from. If there is no limitation on scraping, then you should look at the robots.txt file for the given website(s).

When reading the terms and conditions of a website, you can search for following keywords to find restrictions:

• scraper/scraping

• crawler/crawling

• bot

• spider

• program

Most of the time these keywords can be found, and this makes your search easier. If you have no luck, you need to read through the whole legal content and it is not as easy—at least I think legal stuff is always dry to read.

in the european Union there’s a data protection right that has been live for some years but strictly enforced from 2018: Gdpr. Keep the private data of private persons out of your scraping—you can be held liable if some of it slips out into public because of your scraper.

### 2. robots.txt

Most websites provide a file called robots.txt, which is used to tell web crawlers what they can scrape and what they should not touch. Naturally, it is up to the developer to respect these recommendations, but I advise you to always obey the contents of the robots.txt file.

Let’s see one example of such a file:

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

The preceding code block is from www.apress.com/robots.txt. As you can see, most content tells what is disallowed. For example, scrapers shouldn’t scrape [Springer DE - wissenschaftliche Zeitschriften, Bücher & Online Medien](https://www.apress.com/covers/).

Besides the Allow and Disallow entries, the User-agent can be interesting. Every scraper should have an identification, which is provided through the user agent parameter. Bigger bots, created by Google and Bing, have their unique identifier. And because they are scrapers that add your pages to the search results, you can define excludes for these bots to leave you alone. Later in this chapter, you will create a script which will examine and follow the guidelines of the robots.txt file with a custom user agent.

There can be other entries in a robots.txt file, but they are not standard. To find out more about those entries, visit https://en.wikipedia.org/wiki/Robots_exclusion_standard.

### 3. Technology of the Website

Another useful preparation step is to look at the technologies the targeted website uses.

There is a Python library called builtwith, which aims to detect the technologies a website utilizes. The problem with this library is that the last version 1.3.2 was released in 2015, and it is not compatible with Python 3. Therefore, you cannot use it as you do with libraries available from the PyPI.1 

However, in May 2017, Python 3 support has been added to the sources, but the new version was not released (yet, I’m writing this in November 2017). This doesn’t mean we cannot use the tool; we must manually install it.

First, download the sources from [richardpenman / builtwith / Downloads — Bitbucket](https://bitbucket.org/richardpenman/builtwith/downloads/). If you prefer, you can clone the repository with Mercurial to stay up to date if new changes occur. After downloading the sources, navigate to the folder where you downloaded the sources and execute the following command:

    pip install .

The command installs builtwith to your Python environment and you can use it.

Now if you open a Python CLI, you can look at your target site to see what technologies it uses.

```
>>> from builtwith import builtwith
>>> builtwith('http://www.apress.com') 
>>> {'javascript-frameworks': ['AngularJS', 'jQuery'], 'font-scripts': ['Font Awesome'], 'tag-managers': ['Google Tag Manager'], 'analytics': ['Optimizely']}
```

The preceding code block shows which technologies Apress uses for its website. You can learn from AngularJS that if you plan to write a scraper, you should be prepared to handle dynamic content that is rendered with JavaScript.

builtwith is not a magic tool, it is a website scraper that downloads the given URL; parses its contents; and based on its knowledge base, it tells you which technologies the website uses. This tool uses basic Python features, which means sometimes you cannot get information in the website you are interested in, but most of the time you get enough information.

### 4. Using Chrome Developer Tools

To walk through the website and identify the fields of the requirements, we will use Google Chrome’s built-in DevTools. If you do not know what this tool can do for you, here is a quick introduction.

The Chrome Developer Tools (DevTools for short), are a set of web authoring and debugging tools built into Google Chrome. The DevTools provide web developers deep access into the internals of the browser and their web application. Use the DevTools to efficiently track down layout issues, set JavaScript breakpoints, and get insights for code optimization.

As you can see, DevTools give you tools to see inside the workings of the browser. We don’t need anything special; we will use DevTools to see where the information resides.

In this section I will guide us with screenshots through the steps I usually do when I start (or just evaluate) a scraping project.

Set-up

First, you must prepare to get the information. Even though we know which website to scrape and what kind of data to extract, we need some preparation.

Basic website scrapers are simple tools that download the contents of the website into memory and then do extraction on this data. This means they are not capable of running dynamic content just like JavaScript, and therefore we have to make our browser similar to a simple scraper by disabling JavaScript rendering.

First, right-click with your mouse on the web page and from the menu select “Inspect,” as shown in Figure 1-1.

Figure 1-1. Starting Chrome’s DevTools

Alternatively, you can press CTRL+SHIFT+I in Windows or z+⇧+I on a Mac to open the DevTools window.

Then locate the settings button (the three vertically aligned dots, as shown in Figure 1-2.) and click it:

Figure 1-2. The Settings menu is located under the three dots

Alternatively, you can press F1 in Windows.

Now scroll down to the bottom of the Settings screen and make sure Disable JavaScript is checked, as shown in Figure 1-3.

Figure 1-3. Disabling JavaScript

Now reload the page, exit the Settings window, but stay in the inspector view because we will use the HTML element selector available here.

Note disabling JavaScript is necessary if you want to see how your scraper sees the website.

Later in this book, you will learn options how to scrape websites that utilize JavaScript to render dynamic content.

But to fully understand and enjoy those extra capabilities, you must learn the basics.

### 5. Tool Considerations

If you are reading this book, you will write your scrapers most likely with Python 3. However, you must decide on which tools to use.

In this book you will learn the tools of the trade and you can decide on your own what to use, but now I’ll share with you how I decide on an approach.

If you are dealing with a simple website—and by simple, I mean one that is not using JavaScript excessively for rendering—then you can choose between creating a crawler with Beautiful Soup + requests or use Scrapy. If you must deal with a lot of data and want to speed things up, use Scrapy. In the end, you will use Scrapy in 90% of your tasks, and you can integrate Beautiful Soup into Scrapy and use them together.

If the website uses JavaScript for rendering, you can either reverse engineer the AJAX/XHR calls and use your preferred tool, or you can reach out to a tool that renders websites for you. Such tools are Selenium and Portia. I will introduce you to these approaches in this book and you can decide which fits you best, which is easier for you to use.

## 03. Starting to Code

After this lengthy introduction, it is time to write some code. I guess you are keen to get your fingers “dirty” and create your first scrapers.

In this section we will write simple Python 3 scripts to get you started with scraping and to utilize some of the information you read previously in this chapter.

These miniscripts won’t be full-fledged applications, just small demos of what is awaiting you in this book.

### 1. Parsing robots.txt

Let’s create an application that parses the robots.txt file of the target website and acts based on the contents.

Python has a built-in module that is called robotparser, which enables us to read and understand the robots.txt file and ask the parser if we can scrape a given part of the target website.

We will use the previously shown robots.txt file from Apress.com. To follow along, open your Python editor of choice, create a file called robots.py, and add the following code:

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

Now let’s run the example application. If we have done everything right (and Apress didn’t change its robot guidelines), we should get back False and True, because we are not allowed to access the covers folder, but there is no restriction on the Python section.

> python robots.py False True

This code snippet is good if you write your own scraper and you don’t use Scrapy. Integrating the robotparser and checking every URL before accessing it helps you automate the task of honoring the website owners’ request what to access.

Previously, in this chapter, I mentioned that you can define user agent-specific restrictions in a robots.txt file. Because I have no access to the Apress website, I created a custom entry on my own homepage for this book and this entry looks like this:

```
User-Agent: bookbot 
Disallow: /category/software-development/java-softwaredevelopment/
```

Now to see how this works. For this, you must modify the previously written Python code (robots.py) or create a new one to provide a user agent when you call the is_allowed function because it already accepts a user agent as argument.

```
from urllib import robotparser

robot_parser = robotparser.RobotFileParser()

def prepare(robot_txt_url):
    robot_parser.set_url(robot_txt_url)
    robot_parser.read()

def is_allowed(target_url, user_agent='*'):
    return robot_parser.can_fetch(user_agent, target_url)

if __name__ == '__main__':
    prepare('http://hajba.hu/robots.txt')

    print(is_allowed('http://hajba.hu/category/softwaredevelopment/java-software-development/'), 'bookbot')
    print(is_allowed('http://hajba.hu/category/softwaredevelopment/java-software-development/'), 'my-agent')
    print(is_allowed('http://hajba.hu/category/softwaredevelopment/java-software-development/'), 'googlebot')
```

The preceding code will result in the following output:

False 

True 

True

Unfortunately, you cannot prevent malicious bots from scraping your website because in most cases they will ignore the settings in your robots.txt file.

### 2. Creating a Link Extractor

After this lengthy introduction, it is time to create our first scraper, which will extract links from a given page.

This example will be simple; we won’t use any specialized tools for website scraping, just libraries available with the standard Python 3 installation.

Let’s open a text editor (or the Python IDE of your choice). We will work in a file called link_extractor.py.

```
from urllib.request import urlopen
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
        print(link)
```

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

As you can see, when you run the modified code, this new method adds http://www.apress.com to every URL that is missing this prefix, for example http://www.apress.com/gp/python, but leaves others like https://twitter.com/apress intact.

The previous code example uses regular expressions to find all the anchor tags (<a>) in the HTML code of the website. Regular expressions are a hard topic to learn, and they are not easy to write. That’s why we won’t dive deeper into this topic and will use more high-level tools, like Beautiful Soup, in this book to extract our contents.

### 3. Extracting Images

In this section we will extract image sources from the website. We won’t download any images yet, just lay hands on the information about where these images are in the web.

Images are very similar to links from the previous section, but they are defined by the <img> tag and have a src attribute instead of an href.

With this information you can stop here and try to write the extractor on your own. Following, you’ll find my solution.

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

## Summary

In this chapter you’ve gotten a basic introduction to website scraping and how to prepare for a scraping job.

Besides the introduction, you created your first building blocks for scrapers that extracted information from a web page, like links and image sources.

As you may guess, Chapter 1 was just the beginning. There is a lot more coming up in the following chapters.

You will learn the requirements for which you must create a scraper, and you will write your first scrapers using tools like Beautiful Soup and Scrapy. Stay tuned and continue reading!
