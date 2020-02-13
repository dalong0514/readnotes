# 02 Enter the Requirements

After the introductory chapter, it is time to get you started with a real scraping project.

In this chapter you will learn what data you must extract throughout the next two chapters, using Beautiful Soup and Scrapy.

Don’t worry; the requirements are simple. We will extract information from the following website: [Sainsbury’s](https://www.sainsburys.co.uk/).

Sainsbury’s is an online shop with a lot of goods provided. This makes a great source for a website scraping project.

I’ll guide you to find your way to the requirements, and you’ll learn how I approach a scraping project.

Figure 2-1. The landing page of Sainsbury's at Halloween 2017

## 01. The Requirements

If you look at the website, you can see this is a simple web page with a lot of information. Let me show you which parts we will extract.

One idea would be to extract something from the Halloween-themed site (see Figure 2-1. for their themed landing page). However, this is not an option because you cannot try this yourself; Halloween is over when you read this—at least for 2017, and I cannot guarantee that the future sales will be the same.

Therefore, you will extract information on groceries. To be more specific, you will gather nutrition details from the “Meat & fish” department.

For every entry, which has nutrition details, you extract the following information:

• Name of the product

• URL of the product

• Item code

• Nutrition details per 100g:

• Energy in kilocalories

• Energy in kilojoules

• Fat

• Saturates

• Carbohydrates

• Total sugars

• Starch

• Fibre

• Protein

• Salt

enter the requirements

• Country of origin

• Price per unit

• Unit

• Number of reviews

• Average rating

This looks like a lot, but do not worry! You will learn how to extract this information from all the products of this department with an automated script. And if you are keen and motivated, you can extend this knowledge and extract all the nutrition information for all the products.

## 02. Preparation

As I mentioned in the previous chapter, before you start your scraper development, you should look at the website’s terms and conditions, and the robots.txt file to see if you can extract the information you need.

When writing this part (November 2017), there was no entry on scraper restrictions in the terms and conditions of the website. This means, you can create a bot to extract information.

The next step is to look at the robots.txt file, found at http://sainsburys.co.uk/robots.txt.

# __PUBLIC_IP_ADDR__ Domain name.

- Internet facing IP Address or

User-agent: * Disallow: /webapp/wcs/stores/servlet/OrderItemAdd Disallow: /webapp/wcs/stores/servlet/OrderItemDisplay Disallow: /webapp/wcs/stores/servlet/OrderCalculate Disallow: /webapp/wcs/stores/servlet/QuickOrderCmd Disallow: /webapp/wcs/stores/servlet/InterestItemDisplay

21 Chapter 2

enter the requirements

Disallow: /webapp/wcs/stores/servlet/ProductDisplayLargeImageView Disallow: /webapp/wcs/stores/servlet/QuickRegistrationFormView Disallow: /webapp/wcs/stores/servlet/UserRegistrationAdd Disallow: /webapp/wcs/stores/servlet/ PostCodeCheckBeforeAddToTrolleyView Disallow: /webapp/wcs/stores/servlet/Logon Disallow: /webapp/wcs/stores/servlet/ RecipesTextSearchDisplayView Disallow: /webapp/wcs/stores/servlet/PostcodeCheckView Disallow: /webapp/wcs/stores/servlet/ShoppingListDisplay Disallow: /webapp/wcs/stores/servlet/gb/groceries/get-ideas/ advertising Disallow: /webapp/wcs/stores/servlet/gb/groceries/get-ideas/ development Disallow: /webapp/wcs/stores/servlet/gb/groceries/get-ideas/ dormant Disallow: /shop/gb/groceries/get-ideas/dormant/ Disallow: /shop/gb/groceries/get-ideas/advertising/ Disallow: /shop/gb/groceries/get-ideas/development

Sitemap: http://www.sainsburys.co.uk/sitemap.xml

In the code block you can see what is allowed and what is not, and this robots.txt is quite restrictive and has only Disallow entries but this is for all bots.

What can we find out from this text? For example, you shouldn’t create bots that order automatically through this website. But this is unimportant for us because we only need to gather information—no purchasing. This robots.txt file has no limitations on our purposes; we are free to continue our preparation and scraping.

22 Chapter 2

enter the requirements

What would limit our purposes? Good question. an entry in the robots.txt referencing the “meat & fish” department could limit our scraping intent. a sample entry would look like this:

User-agent: * Disallow: /shop/gb/groceries/meat-fish/ Disallow: /shop/gb/groceries/

But this won’t allow search engines to look up the goods sainsbury’s is selling, and that would be a big profit loss.

Navigating Through “Meat & fishFish”

As mentioned at the beginning of this chapter, we will extract data from the “Meat & fish” department. The URL of this part of the website is www.sainsburys.co.uk/shop/gb/groceries/meat-fish.

Let’s open the URL in our Chrome browser, disable JavaScript, and reload the browser window as described in the previous chapter. Remember, disabling JavaScript enables you to see the website’s HTML code as a basic scraper will see it.

While I am writing this, the website of the department looks like Figure 2-2.

enter the requirements

Figure 2-2. The “Meat & fish” department’s page inspected with Chrome’s DevTools

For our purposes, the navigation menu on the left side is interesting. It contains the links to the pages where we will find products to extract. Let’s use the selection tool (or hit CTRL-SHIFT-C) and select the box containing these links, as shown in Figure 2-3.

Figure 2-3. Selecting the navigation bar on the left

Now we can see in the DevTools that every link is in a list element (<li> tag) of an unordered list (<ul>), with class categories departments. Note down this information because we will use it later.

enter the requirements

Links, which have a little arrow pointing to the right (>), tell us they are just a grouping category and we will find another navigation menu beneath them if we click them. Let’s examine the Roast dinner option, as shown in Figure 2-4.

Figure 2-4. The “Roast dinner” submenu

Here we can see that the page has no products but another list with links to detailed sites. If we look at the HTML structure in DevTools, we can see that these links are again elements of an unordered list. This unordered list has the class categories aisles.

Now we can go further into the Beef category, and here we have products listed (after a big filter box), as shown in Figure 2-5.

enter the requirements

Figure 2-5. Products in the “Beef” category

Here we need to examine two things: one is the list of products; the other is the navigation.

If the category contains more products than 36 (this is the default count to show on the website), the items will be split into multiple pages. Because we want to extract information on all products, we must navigate through all those pages. If we select the navigation, we can see it is again an unordered list of the class pages, as shown in Figure 2-6.

26 Chapter 2

enter the requirements

Figure 2-6. Unordered list with the class “pages”

From those list elements, we are interested in the one with the rightpointing arrow symbol, which has the class next. This tells us if we have a next page we must navigate to or not.

Now let’s find the link to the detail page of the products. All the products are in an unordered list (again). This list has the class productLister gridView, as shown in Figure 2-7.

Figure 2-7. Selecting the product list from the DevTools

Every product is in a list element with the class gridItem. If we open up the details of one of those products we can see where the navigation link is: located in some divs and an h3. We note that the last div has the class productNameAndPromotions, as shown in Figure 2-8.

27 Chapter 2

enter the requirements

Figure 2-8. Selecting the product’s name

Now we reached the level of the products, and we can step further and concentrate on the real task: identifying the required information.

Selecting the Required Information

We will discover the elements where our required information resides, based on the product shown in Figure 2-9.

Figure 2-9. The detailed product page we will use for the example

28 Chapter 2

enter the requirements

Now that we have the product, let’s identify the required information. As previously, we can use the select tool, locate the required text, and read the properties from the HTML code.

The name of the product is inside a header (h1), which is inside a div with the class productTitleDescriptionContainer.

The price and the unit are in a div of the class pricing. The price itself is in a paragraph (p) of the class pricePerUnit; the unit is in a span of the class pricePerUnitUnit.

Extracting the rating is tricky because here we only see the stars for the rating, but we want the numeric rating itself. Let’s look at the image’s HTML definition, as shown in Figure 2-10.

Figure 2-10. The image’s HTML code

We can see the location of the image is inside a label of class numberOfReviews and it has an attribute, alt, which contains the decimal value of the averages of the reviews. After the image, there is the text containing the number of the reviews.

The item code is inside a paragraph of class itemCode.

29 Chapter 2

enter the requirements

The nutrition information, as shown in Figrue 2-11, is inside a table of class nutritionTable. Every row (tr) of this table contains one entry of our required data: the header (th) of the row has the name and the first column (td) contains the value. The only exception is the energy information, because two rows contain the values but only the first one the header. As you will see, we will solve this problem too with some specific code.

Figure 2-11. The nutrition table

The country of origin, as shown in Figure 2-12, is inside a paragraph of a div of class productText. This field is not unique: every description is in a productText div. This will make the extraction a bit complicated, but there is a solution for this too.

30 Chapter 2

enter the requirements

Figure 2-12. Selecting the “Country of Origin” in Chrome’s DevTools

Even though we must extract many fields, we identified them easily in the website. Now it is time to extract the data and learn the tools of the trade!

Outlining the Application

After the requirements are defined and we’ve found each entry to extract, it is time to plan the applications structure and behavior.

If you think a bit about how to approach this project, you will start with big-bang, “Let’s hammer the code” thinking. But you will realize later that you can break down the whole script into smaller steps. One example can be the following:

1. Download the starting page, in this case the “Meat & fish” department, and extract the links to the product pages.

2. Download the product pages and extract the links to the detailed products.

3. Extract the information we are interested in from the already downloaded product pages.

4. Export the extracted information.

And these steps could identify functions of the application we are developing.

31 Chapter 2

enter the requirements

Step 1 has a bit more to offer: if you remember the analysis with DevTools you have seen, some links are just a grouping category and you must extract the detail page links from this grouping category.

## 04. Navigating the Website

Before we jump into learning the first tools you will use to scrape website data, I want to show you how to navigate websites—and this will be another building block for scrapers.

Websites consist of pages and links between those pages. If you remember your mathematic studies, you will realize a website can be depicted as a graph, as shown in Figure 2-13.

Figure 2-13. The navigation path

Because a website is a graph, you can use graph algorithms to navigate through the pages and links: Breadth First Search (BFS) and Depth First Search (DFS).

32 Chapter 2

enter the requirements

Using BFS, you go one level of the graph and gather all the URLs you need for the next level. For example, you start at the “Meat & fish” department page and extract all URLs to the next required level, like “Top sellers” or “Roast dinner.” Then you have all these URLs and go to the Top sellers and extract all URLs that lead to the detailed product pages. After this is done, you go to the “Roast dinner” page and extract all product details from there too, and so on. At the end you will have the URLs to all product pages, where you can go and extract the required information.

Using DFS, you go straight to the first product through “Meat & fish,” “Top sellers,” and extract the information from its site. Then you go to the next product on the “Top sellers” page and extract the information from there. If you have all the products from “Top sellers” then you move to “Roast dinner” and extract all products from there.

If you ask me, both algorithms are good, and they deliver the same result. I could write two scripts and compare them to see which one is faster, but this comparison would be biased and flawed.1 

Therefore, you will implement a script that will navigate a website, and you can change the algorithm behind it to use BFS or DFS.

If you are interested in the Why? for both algorithms, I suggest you consider Magnus Hetland’s book: Python Algorithms.2 

Creating the Navigation

Implementing the navigation is simple if you look at the algorithms, because this is the only trick: implement the pseudo code.

OK, I was a bit lazy, because you need to implement the link extraction too, which can be a bit complex, but you already have a building block from Chapter 1 and you are free to use it.

1 Read more on this topic here: www.ibm.com/developerworks/library/

j-jtp02225/index.html 2 www.apress.com/gp/book/9781484200568

33 Chapter 2

enter the requirements

def extract_links(page):

if not page:

return []

link_regex = re.compile('<a[^>]+href=["\'](.*?)["\']',

re.IGNORECASE) return [urljoin(page, link) for link in link_regex. findall(page)]

def get_links(page_url):

host = urlparse(page_url)[1] page = download_page(page_url) links = extract_links(page) return [link for link in links if urlparse(link)[1] == host]

The two functions shown extract the page, and the links still point to the Sainsbury’s website.

Note if you don’t filter out external urLs, your script may never end. this is only useful if you want to navigate the whole WWW to see how far you can reach from one website.

The extract_links function takes care of an empty or None page. urljoin wouldn’t bleat about this but re.findall would throw an exception and you don’t want that to happen.

The get_links function returns all the links of the web page that point to the same host. To find out which host to use, you can utilize the urlparse function, 3 which returns a tuple. The second parameter of this tuple is the host extracted from the URL.

3 https://docs.python.org/3/library/urllib.parse.html

34 Chapter 2

enter the requirements

Those were the basics; now come the two search algorithms:

def depth_first_search(start_url):

from collections import deque visited = set() queue = deque() queue.append(start_url) while queue:

url = queue.popleft() if url in visited:

continue visited.add(url) for link in get_links(url):

queue.appendleft(link) print(url)

def breadth_first_search(start_url):

from collections import deque visited = set() queue = deque() queue.append(start_url) while queue:

url = queue.popleft() if url in visited:

continue visited.add(url) queue.extend(get_links(url)) print(url)

If you look at the two functions just shown, you will see only one difference in their code (hint: it’s highlighted): how you put them into the queue, which is a stack.

35 Chapter 2

enter the requirements

The requests Library

To implement the script successfully, you must learn a bit about the requests library.

I really like the extendedness of the Python core library, but sometimes you need libraries developed by members of the community. And the requests library is one of those.

With basic Python urlopen you can create simple requests and corresponding data, but it is complex to use. The requests library adds a friendly layer above this complexity and makes network programming easy: it takes care of redirects, and can handle sessions and cookies for you. The Python documentation recommends it as the tool to use.

Again, I won’t give you a detailed introduction into this library, just the necessary information to get you going. If you need more information, look at the project’s website.4 

Installation

You, as a “Pythonista,” already know how to install a library. But for the sake of completeness I include it here.

pip install requests

Now you are set up to continue this book.

Getting Pages

Requesting pages is easy with the requests library: requests.get(url).

This returns a response object that contains basic information, like status code and content. The content is most often the body of the website you requested, but if you requested some binary data (like images or sound files) or JSON, then you get that back. For this book, we will focus on HTML content.

4 Requests: HTTP for Humans: http://docs.python-requests.org/en/master/

36 Chapter 2

enter the requirements

You can get the HTML content from the response by calling its text parameter:

import requests r = requests.get('http://www.hajba.hu') if r.status_code == 200:

print(r.text[:250]) else:

print(r.status_code)

The preceding code block requests my website’s front page, and if the server returns the status code 200, which means OK, it prints the first 250 characters of the content. If the server returns a different status, that code is printed.

You can see an example of a successful result as follows:

<!DOCTYPE html>

<html lang="en-US">

<head>

<meta property="og:type" content="website" />

<meta property="og:url" content="http://hajba.hu/2017/10/26/ red-hat-forum-osterreich-2017/" />

<meta name="twitter:card" content="summary_large_image" />

With this we are through the basics of the requests library. As I introduce more concepts of the library later in this book, I will tell you more about it.

Now it is time to skip the default urllib calls of Python 3 and change to requests.

Switching to requests

Now it is time to finish the script and use the requests library for downloading the pages.

37 Chapter 2

enter the requirements

By now you know already how to accomplish this, but here is the code anyway.

def download_page(url):

try:

return requests.get(url).text except:

print('error in the url', url)

I surrounded the requesting method call with a try-except block because it can happen that the content has some encoding issues and we get an exception back that kills the whole application; and we don’t want this because the website is big and starting over would require too much resources.5 

Putting the Code Together

Now if you put everything together and run both functions with 'https:// www.sainsburys.co.uk/shop/gb/groceries/meat-fish/' as starting_url, then you should get a similar result to this one.

starting navigation with BFS https://www.sainsburys.co.uk/shop/gb/groceries/meat-fish/ http://www.sainsburys.co.uk https://www.sainsburys.co.uk/shop/gb/groceries https://www.sainsburys.co.uk/shop/gb/groceries/favourites https://www.sainsburys.co.uk/shop/gb/groceries/great-offers

starting navigation with DFS https://www.sainsburys.co.uk/shop/gb/groceries/meat-fish/

5 I’ll share a writing secret with you: I encountered six exceptions caused by

encoding problems when I created the code for this chapter, and one was in the “Meat & fish” department.

enter the requirements

http://www.sainsburys.co.uk/accessibility http://www.sainsburys.co.uk/shop/gb/groceries http://www.sainsburys.co.uk/terms http://www.sainsburys.co.uk/cookies

If your result is slightly different, then the website’s structure changed in the meantime.

As you can see from the printed URLs, the current solution is rudimentary: the code navigates the whole website instead of focusing only on the “Meat & fish” department and nutrition details.

One option would be to extend the filter to return only relevant links, but I don’t like regular expressions because they are hard to read. Instead let’s go ahead to the next chapter.

## Summary

This chapter prepared you for the remaining parts of the book: you’ve met the requirements, analyzed the website to scrape, and identified where in the HTML code the fields of interest lay. And you implemented a simple scraper, mostly with basic Python tools, which navigates through the website.

In the next chapter you will learn Beautiful Soup, a simple extractor library that helps you to forget regular expressions, and adds more features to traverse and extract HTML-trees like a boss.
