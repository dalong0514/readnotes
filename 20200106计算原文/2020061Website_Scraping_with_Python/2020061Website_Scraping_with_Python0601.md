# 06Website Scraping in the Cloud

Running website scraping locally is fine for do-once tasks and small amounts of data, where you can easily trigger the crawl manually.

However, if you want reoccurring tasks and automatic scheduling, you should think about other solutions such as deploying your spiders somewhere into the cloud or a bought server slot.

In this chapter we will look at the virtual network of servers, the cloud, and what options you have if you want to use website scraping in the cloud. I’ll focus on Scrapy because it is the tool for website scraping and there are services provided and matched for use with Scrapy.

Scrapy Cloud

The name tells you everything: Scrapy Cloud 1 is a cloud solution where you can deploy your Scrapy spiders. As the website states: “Think of it as a Heroku for web crawling.”

1 https://scrapinghub.com/scrapy-cloud

© Gábor László Hajba 2018 G. L. Hajba, Website Scraping with Python, https://doi.org/10.1007/978-1-4842-3925-4_6

193 Chapter 6

Website sCraping in the Cloud

Creating a Project

When you arrive at ScrapingHub, you will want to create a project because the page you get is empty, as shown in Figure 6-1.

Figure 6-1. My company’s empty ScrapingHub overview

Fortunately, it is intuitive: we must click the green button in the upper right corner.

We will use Scrapy spiders, so select this option, as shown in Figure 6-2.

Figure 6-2. Creating a new project

194 Chapter 6

Website sCraping in the Cloud

Now that the project is created, we must upload our spider to the cloud. There are two options: over the command line or cloning a GitHub repository, as you can see in Figure 6-3. We will go with the command line solution because I am a nerd, and because most of the time I use some internal Git system and not GitHub to store my code.

Figure 6-3. New project and upload options

If you decide to use the command line, you have two options: to deploy directly or a Docker image. I will stay with the simple deploy version for now.

Deploying Your Spider

Because I use the basic command line deployment, I go to the spider’s base folder (where the scrapy.cfg file is located) and execute the following commands:

pip install shub shub login shub deploy

195 Chapter 6

Website sCraping in the Cloud

After you run the shub deploy command the first time, you will see following message among others:

Saved to scrapinghub\sainsburys\scrapinghub.yml.

This file is important because you must edit this file if you deploy a Python 3 spider. And because I focused on Python 3, we will use this configuration. Let’s do this now and add the following line to your scrapinghub.yml:

stack: scrapy:1.5-py3 This tells ScrapingHub that you want to use Scrapy version 1.5 running in a Python 3 environment.

After this change, run shub deploy again to update the spider on the server. The deployment information is then something similar to what is shown in Figure 6-4.

Figure 6-4. Deployment info and history

Start and Wait

After deployment, in the upper left corner you will see that you have one spider, like in Figure 6-5. Clicking this link (or the Dashboard menu entry in the Spiders section) navigates you to your spiders.

196 Chapter 6

Website sCraping in the Cloud

Figure 6-5. Spiders in the project

Clicking the basic spider (for me the only spider deployed) will get you to the spider’s page, as shown in Figure 6-6. Here you can change some project specific settings, and you can run the spider.

Figure 6-6. Spider details

Running the Sainsbury’s spider takes some time. But you can do it and wait for its completion. After running the spiders, you will see all information about runs—even if you had errors while running your spiders, as shown in Figure 6-7.

Figure 6-7. Completed jobs

197 Chapter 6

Website sCraping in the Cloud

As you can see, you get information about loaded items, sent requests, and some statistics. If you click the job’s number, you will get some detailed statistics and you can look at the items extracted by the run, as shown in Figure 6-8.

Figure 6-8. Some basic statistics of the run

Accessing the Data

You can access the extracted information in some ways. The most common access is to download your results in some format, as you would export it while running Scrapy from your command line, as shown in Figure 6-9.

Figure 6-9. Export options

198 Chapter 6

Website sCraping in the Cloud

As you can see, you get some options and one will fit your project’s needs. An alternative option is to publish your dataset. This makes it available to people even without knowing how you gathered the data. Publishing comes in three flavors:

• Public: Everyone has access to the data, no need for ScrapingHub account, and search engines can index it.

• Protected: Only users with ScrapingHub account can access this data.

• Private: Oonly members of your ScrapingHub organization can access the data.

If you have confident information, then use private. ScrapingHub has some issues with publicly available datasets, and you cannot access them without a ScrapingHub account.

Anyhow, if you want to publish a dataset, you must provide a description and a logo to it to be publicly available. I agree with the description, but a logo is in my eyes too much. Sure, if you look at the catalog, 2 you will see why a logo is required, as shown in Figure 6-10.

Figure 6-10. The public dataset catalog

2 https://app.scrapinghub.com/datasets

199 Chapter 6

Website sCraping in the Cloud

From these datasets, you can download the items the same way you can through your job’s page. note, that you have to be logged in to see the available datasets.

API

ScrapingHub provides an API that you can use to access your data programmatically. Let’s examine this option too.

I suggest you use the scrapinghub Python library, because accessing the API directly (with curl for example) doesn’t work the way it is described in the documentation.

pip install scrapinghub[msgpack]

Now we’re ready to access our data from a simple Python code. I’ll use the interactive interpreter so you can follow along.

>>> from scrapinghub import ScrapinghubClient

>>> apikey = 'YOUR-API-KEY'

>>> client = ScrapinghubClient(apikey)

>>>

>>> client.projects.list() [310577]

The first step, after logging in, is to get the ID of our project. Because I have only one project, I get only one ID back. You’ll get back a different one, so replace accordingly.

>>> project = client.get_project(310577)

>>> [j['key'] for j in project.jobs.list()] ['310577/1/4']

200 Chapter 6

Website sCraping in the Cloud

Above we list all the jobs associated with the project. This job key is needed to access the data. If you have long-running jobs, you can use the state flag of the job’s metadata information:

>>> job = project.jobs.get('310577/1/4')

>>> job.metadata.get('state') 'finished'

Now that we have the job we’re interested in, let’s retrieve all the items.

>>> job.items.iter() <generator object mpdecode at 0x000001DAC5092D58>

>>> for item in job.items.iter(count=1):

... print(item) ...

{'url': 'https://www.sainsburys.co.uk/shop/ProductDisplay ?storeId=10151&productId=1219376&urlRequestType=Base&cate goryId=275324&catalogId=10100&langId=44', 'product_name': "Sainsbury's British Pork Mince 20% Fat 500g", 'product_ image': 'https://www.sainsburys.co.uk/wcsstore7.27.110/ ExtendedSitesCatalogAssetStore/images/catalog/productI mages/93/0000000327893/0000000327893_L.jpeg', 'image_ urls': ['https://www.sainsburys.co.uk/wcsstore7.27.110/ ExtendedSitesCatalogAssetStore/images/catalog/productImages /93/0000000327893/0000000327893_L.jpeg'], 'price_per_unit': '£1.65', 'rating': '0.0', 'product_reviews': '0', 'item_ code': '7916164', 'nutritions': {'Energy kJ': '1104', 'Energy kcal': '265', 'Fat': '18.9g', 'of which saturates': '6.5g', '- mono-unsaturates': '8.0g', '- polyunsaturates': '3.5g', 'Carbohydrate': '1.0g', 'of which sugars': '<0.5g', 'Fibre': '0.6g', 'Protein': '22.5g', 'Salt': '0.50g'}, 'product_origin': ", '_type': 'SainsburysItem'}

201 Chapter 6

Website sCraping in the Cloud

As you can see in the preceding code, you can get a generator over the items associated with the job; I printed out the first result of the list. If you’re interested in how many items have been extracted, you can use the metadata of the job again.

>>> job.metadata.get('scrapystats')['item_scraped_count'] 923

As you can see, the API is very useful to split up data extraction from websites and process them automatically with scripts later.

Limitations

Free accounts have some limitations. Let’s look at them, even if you can go along very well with these limits.

First, there is a limitation of one concurrent crawl, which means you can only run one spider at a time. For starting out, this is not a problem because you will rarely want to run spiders in parallel. If the number of your customers is growing, then you can encounter occasions when you need parallel runs to gather data faster.

The second limitation, which can be annoying if you have jobs that should be run frequently, is no periodic jobs. You can configure them, but they won’t run until you subscribe to a paid plan, which start currently at $9 per month.

The third big limitation is data storage. Your scraped results are stored only for seven days. After that time, your crawl result is history. You can extend this period to 120 days if you subscribe to a paid plan. But you can overcome this problem if you have automatic data processing (through the API), or if you store your data in a database.

202 Chapter 6

Website sCraping in the Cloud

Summary

ScrapingHub is the ideal solution in my eyes, if you have bigger Scrapy projects, because it offers an easy to use platform for setting up and evaluating your project. The presence of the Python library to access your scraped data (and interacting with your spiders too) makes it convenient both to automate data extraction and work with this data. The free plan gives you a lot, and help is there to get you started.

PythonAnywhere

OK, there are other options besides ScrapingHub, of course. One is PythonAnywhere, 3 a platform solution that enables you to run Python in the cloud. It has a free “beginner” account, which has limitations on outbound internet access, CPU, and memory usage, but it will fit our purposes.

In this section we will create a simple scraper written in Scrapy, and we will upload it to the cloud.

The Example Script

We will use a different Scrapy script, because the free account has limitations on websites that you can reach from your scripts and Sainsbury’s is not listed.

Therefore, I picked a website and created a simple scraper that will extract the name and the description of the sights and attractions in Berlin.

3 https://www.pythonanywhere.com/

203 Chapter 6

Website sCraping in the Cloud

PythonAnywhere Configuration

Now it’s time to configure our PythonAnywhere account and get the script in the cloud. I’ll give you a step-by-step description here for the current version of the PythonAnywhere solution—as it is on the 3rd April 2018.

Install Scrapy with the following command:

pip install --user scrapy

the --user flag is required because you are not allowed to modify the global python package installations, and you cannot ad Scrapy to it either.

Now we have everything set up for our scraper. To verify this, you can execute the following command:

~ $ scrapy version Scrapy 1.5.0

Well, installing scrapy and all its dependencies consumes the daily assigned Cpu capacity. if you want to continue with this chapter’s examples, you can, but it can get slow on a free pythonanywhere account.

Uploading the Script

There are some ways to get your scripts up to PythonAnywhere:

• cloning from Github / BitBucket

• uploading as a ZIP file (actually, you can upload it file-by-file, but ZIP is more convenient)

• SFTP and Rsync for paying accounts

204 Chapter 6

Website sCraping in the Cloud

I used the ZIP approach: compressed the Scrapy project; uploaded it from the “Files” menu in PythonAnywhere; and then uncompressed it using the unzip command, as shown in Figures 6-11 and 6-12.

Figure 6-11. The berlin.zip file is uploaded into my home folder

Figure 6-12. Unzipping the package

Now the folder is available under the Files section of the dashboard, as shown in Figure 6-13.

205 Chapter 6

Website sCraping in the Cloud

Figure 6-13. The files containing the berlin folder

Running the Script

Now we can run the script from our Bash console the same way as locally, as shown in Figure 6-14. And because we have a file system, we can export the results as files too. For example, to get the sights and attractions in a JSON-lines file, we can execute the following command:

scrapy crawl sights -o sights.jl

Figure 6-14. Running the spider

206 Chapter 6

Website sCraping in the Cloud

When the script finishes, like in Figure 6-15, a new file is written into the project’s folder. If there’s already a file, Scrapy will append the new information to it instead of recreating the file from scratch. Remember this!

Figure 6-15. Spider finished and the first three lines of the file

You can access the file through the Files page. Here you can download the file, but it is possible to edit it in your browser, as shown in Figure 6-16.

Figure 6-16. Download the exported file

This Works Just Manually…

For now, we only ran the script manually. But this is not the way we sought when we deployed the scraper in the cloud.

207 Chapter 6

Website sCraping in the Cloud

The solution is to add a scheduler, which automatically starts the scraper at a defined time.

Remember if you are using a scheduler, make sure you remove the already present export file, because scrapy doesn’t overwrite it. if you’re using a custom item exporter, then you may already rewrite the contents of the file.

One option is to set up a Task right at Python Anywhere. Here you must configure what command to execute. And because we know our command, we can add it right to the scheduler, as shown in Figure 6-17.

Figure 6-17. Creating the task using a three-piece script

After the scheduled time up, you have access to the task log that contains the console output, and perhaps some errors, as shown in Figure 6-18.

208 Chapter 6

Website sCraping in the Cloud

Figure 6-18. Accessing the log for a task

The second approach is the extended version of the previous one: we create a script that executes the command sequence defined earlier, and we point the scheduler to this script.

The first step is to create a script that changes to the project’s folder and executes the spider (make sure, you’re pointing to your home folder!).

#!/bin/bash cd /home/GHajba/berlin rm sights.jl scrapy crawl sights -o sights.jl

The preceding script is the same we provided previously to the task, but we placed every command on its own line and this makes it readable.

I created the file right in my browser using PythonAnywhere’s editor, as shown in Figure 6-19.

Figure 6-19. Creating a new file

209 Chapter 6

Website sCraping in the Cloud

Caveat if you’re using a Windows computer, the file editor will add Windows line-endings to your file. to fix this issue (and be able to run the script in a bash shell) execute the following command from the console: sed -i -e 's/\r$//' berlin_scheduler.sh

Because a free account has limitations on the number of scheduled tasks (you can have only one), we will drop the previously created one and create a new one that will execute only the previously created berlin_ scheduler.sh, as shown in Figure 6-20.

Figure 6-20. Creating the new scheduler

After the task is available, you have access to the task log, which contains the same information as previously.

Storing Data in a Database?

It would be a viable option to store the extracted results in a database. Because we’re in the cloud and using PythonAnywhere for now, it would be ideal to have cloud storage—for example, mLab, which is a cloud-based MongoDB.

The problem is that a free account allows only HTTP and HTTPS connections to servers. This means, even though you set-up a Mongo database with mLab, you cannot create a connection to store the data.

210 Chapter 6

Website sCraping in the Cloud

However, Python Anywhere offers MySQL for free users. This means, you can have storage for your extracted information, and you don’t have to store everything in a file.

Let’s look at how to configure MySQL and store the extracted data in the database.

First, let’s create a database. You can do this on the Databases. I named mine berlinsights, as shown in Figure 6-21.

Figure 6-21. Creating a new database is easy

Now we must configure our Scrapy project to be able to connect to the database and write information to the given table.

We will use a simple item pipeline that will insert the sights into the database.

And we need the database table. I created it through the database console using the following script:

create table berlinsights( name varchar(1024) not null, description varchar(4096));

211 Chapter 6

Website sCraping in the Cloud

Figure 6-22. Creating the table using the console

As you can see in Figure 6-22: make sure, you’re using the right database! If you’re not sure which database you’re running on, type status and it will tell you which database you’re on.

If you forget your database password, you can simply set a new one at the database dashboard.

Now we can create our middleware. We will use the pymysql library.

# -*- coding: utf-8 -*-

import pymysql.cursors

insert_template = """INSERT INTO berlinsights (name, description) VALUES (%s, %s)"""

class BerlinMySQLPipeline(object):

def process_item(self, item, spider):

connection = pymysql.connect(host='GHajba.mysql. pythonanywhere-services.com', user='GHajba', password='YourDbPassHere', db='GHajba$berlinsights', charset='utf8mb4',

212 Chapter 6

Website sCraping in the Cloud

cursorclass=pymysql.cursors. DictCursor)

try:

with connection.cursor() as cursor:

cursor.execute(insert_template, (item['name'], item['description'])) connection.commit() finally:

connection.close()

return item

The prceding example uses my database, so make sure you’re filling in your data! And because this MySQL database is a PythonAnywhere service, you can test your connection only when you’ve deployed your scraper.

Again, this script doesn’t validate if an entry is already in the database. If you run it twice, you will get every entry duplicated. Feel free to adapt the script to filter or update already present entries.

After running the spider, we can verify that information is in the database, as shown in Figure 6-23.

Figure 6-23. Verifying the data in the console

If didn’t installed pymysql already, you can do it with the following command:

pip install --user pymysq

213 Chapter 6

Website sCraping in the Cloud

Summary

Python Anywhere offers you cloud hosting and scheduling for free; however, it has limitations on the outgoing connections for the free plan. And this makes it only valuable for practicing. On the other side, if you pay $5 a month, you get an upgraded account where you don’t have to limit your scrapings to the whitelist.4 

What About Beautiful Soup?

PythonAnywhere is a cloud platform for Python. This means you can not only run Scrapy spiders there but Beautiful Soup scrapers too. And this is what we will look at in a nutshell.

The approach is the same as previously: we will extract the same sights but using Beautiful Soup.

Fortunately, the requests and beautifulsoup4 libraries are already installed on the host computer, so you do not need to install anything.

The first step is to write and upload the script. Actually, I have already written the code, but this doesn’t mean you cannot do it for yourself. As always: my code examples are just one solution and there are many paths that lead to the final goal.

import requests from bs4 import BeautifulSoup

bs_parser = 'html.parser'

def get_page(url):

try:

r = requests.get(url) if r.status_code == 200:

4 https://www.pythonanywhere.com/whitelist/

214 Chapter 6

Website sCraping in the Cloud

return BeautifulSoup(r.content, bs_parser) except Exception as e:

pass return None

def get_sights():

soup = get_page('https://www.berlin.de/en/attractions-andsights/') if not soup:

return

for sight in soup.select('div[class*="teaser"]'):

h3 = sight.find('h3') if not h3:

continue a = h3.find('a') if not a:

continue name = a.text if not name:

continue

description = "

div = sight.find('div', class_='inner')

if div:

p = div.find('p') if p:

description = p.text if not description:

continue yield (name, description)

215 Chapter 6

Website sCraping in the Cloud

if __name__ == '__main__':

with open('berlin_sights.jl', 'w') as outfile:

for sight in get_sights():

outfile.write('{' + '"name": "{}", "description": "{}"'.format(sight[0], sight[1]) + '}\n')

After uploading, we can run the script. Running the script works as it would in a normal terminal window.

python3 berlin.py

After the process finishes, you can access the results in the berlin_ sights.jl file. The first entry looks like this:

{"name": "Academy of Arts", "description": "The Academy of Arts is the oldest and most prestigious cultural institution in Germany. Its tasks are to promote contemporary artistic positions and to safeguard cultural heritage. more »"}

Scheduling a script works the same way it did for Scrapy scripts, so I won’t go into detail. Think of PythonAnywhere as your remote Python terminal if you’re using Beautiful Soup.

## Summary

In this chapter we looked at options for how to run scrapers in the cloud. This is the solution if you don’t want to run your extractors every time manually, or you don’t want to have them run on your computer because they eat a lot of resources and your computer gets slow for a long time.

We looked at Scraping Hub, which provides services specific for Scrapy and this makes it unique. Besides this, they’re the developers of Splash too and they have a solution for how you can run your Splash-based spiders in the cloud.

As an alternative, we looked at PythonAnywhere, where you can upload Python scripts and execute them. This is not only useful for Scrapy but for scripts using Beautiful Soup too, and this moves your simple scrapers into the Cloud too.
