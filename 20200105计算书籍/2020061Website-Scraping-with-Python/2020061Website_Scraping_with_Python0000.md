## About the Author

Gábor László Hajba is a Senior Consultant at EBCONT enterprise technologies, who specializes in Java, Python, and Crystal. He is responsible for designing and developing customer needs in the enterprise software world. He has also held roles as an Advanced Software Engineer with Zühlke Engineering, and as a freelance developer with Porsche Informatik. He considers himself a workaholic, (hard)core and well-grounded developer, pragmatic minded, and freak of portable apps and functional code.

He currently resides in Sopron, Hungary with his loving wife, Ágnes.

## About the Technical Reviewer

Chaim Krause is an expert computer programmer with over thirty years of experience to prove it. He has worked as a lead tech support engineer for ISPs as early as 1995, as a senior developer support engineer with Borland for Delphi, and has worked in Silicon Valley for over a decade in various roles, including technical support engineer and developer support engineer. He is currently a military simulation specialist for the US Army’s Command and General Staff College, working on projects such as developing serious games for use in training exercises.

He has also authored several video training courses on Linux topics and has been a technical reviewer for over twenty books, including iOS Code Testing, Android Apps for Absolute Beginners (4ed), and XML Essentials for C# and .NET Development (all Apress). It seems only natural then that he would be an avid gamer and have his own electronics lab and server room in his basement. He currently resides in Leavenworth, Kansas with his loving partner, Ivana, and a menagerie of four-legged companions: their two dogs, Dasher and Minnie, and their three cats, Pudems, Talyn, and Alaska.

## Introduction

Welcome to our journey together exploring website scraping solutions using the Python programming language!

As the title already tells you, this book is about website scraping with Python. I distilled my knowledge into this book to give you a useful manual if you want to start data gathering from websites.

Website scraping is (in my opinion) an emerging topic.

I expect you have Python programming knowledge. This means I won’t clarify every code block I write or constructs I use. But because of this, you’re allowed to differ: every programmer has his/her own unique coding style, and your coding results can be different than mine.

This book is split into six chapters:

1. Getting Started is to get you started with this book: you can learn what website scraping is and why it worth writing a book about this topic.

2. Enter the Requirements introduces the requirements we will use to implement website scrapers in the follow-up chapters.

3. Using Beautiful Soup introduces you to Beautiful Soup, an HTML content parser that you can use to write website scraper scripts. We will implement a scraper to gather the requirements of Chapter 2 using Beautiful Soup.

4. Using Scrapy introduces you to Scrapy, the (in my opinion) best website scraping toolbox available for the Python programming language. We will use Scrapy to implement a website scraper to gather the requirements of Chapter 2.

5. Handling JavaScript shows you options for how you can deal with websites that utilize JavaScript to load data dynamically and through this, give users a better experience. Unfortunately, this makes basic website scraping a torture but there are options that you can rely on.

6. Website Scraping in the Cloud moves your scrapers from running on your computer locally to remote computers in the Cloud. I’ll show you free and paid providers where you can deploy your spiders and automate the scraping schedules.

You can read this book from cover to cover if you want to learn the different approaches of website scraping with Python. If you’re interested only in a specific topic, like Scrapy for example, you can jump straight to Chapter 4, although I recommend reading Chapter 2 because it contains the description of the data gathering task we will implement in the vast part of the book.
