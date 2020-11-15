# 03 Built-in services

scrapy.log has been deprecated alongside its functions in favor of explicit calls to the Python standard logging. Keep reading to learn more about the new logging system.

Scrapy uses Python’s builtin logging system [https://docs.python.org/3/library/logging.html] for event logging. We’ll provide some simple examples to get you started, but for more advanced use-cases it’s strongly suggested to read thoroughly its documentation.

Logging works out of the box, and can be configured to some extent with the Scrapy settings listed in Logging settings.

Scrapy calls scrapy.utils.log.configure_logging() to set some reasonable defaults and handle those settings in Logging settings when running commands, so it’s recommended to manually call it if you’re running Scrapy from scripts as described in Run Scrapy from a script.

Log levels

Python’s builtin logging defines 5 different levels to indicate the severity of a given log message. Here are the standard ones, listed in decreasing order:

logging.CRITICAL - for critical errors (highest severity)

logging.ERROR - for regular errors

logging.WARNING - for warning messages

logging.INFO - for informational messages

logging.DEBUG - for debugging messages (lowest severity)

How to log messages

Here’s a quick example of how to log a message using the logging.WARNING level:

import logging logging.warning("This is a warning")

There are shortcuts for issuing log messages on any of the standard 5 levels, and there’s also a general logging.log method which takes a given level as argument. If needed, the last example could be rewritten as:

import logging logging.log(logging.WARNING, "This is a warning")

On top of that, you can create different「loggers」to encapsulate messages. (For example, a common practice is to create different loggers for every module). These loggers can be configured independently, and they allow hierarchical constructions.

The previous examples use the root logger behind the scenes, which is a top level logger where all messages are propagated to (unless otherwise specified). Using logging helpers is merely a shortcut for getting the root logger explicitly, so this is also an equivalent of the last snippets:

import logging logger = logging.getLogger() logger.warning("This is a warning")

You can use a different logger just by getting its name with the logging.getLogger function:

import logging logger = logging.getLogger('mycustomlogger') logger.warning("This is a warning")

Finally, you can ensure having a custom logger for any module you’re working on by using the __name__ variable, which is populated with current module’s path:

import logging logger = logging.getLogger(__name__) logger.warning("This is a warning")

See also

Module logging, HowTo [https://docs.python.org/2/howto/logging.html]

Basic Logging Tutorial

Module logging, Loggers [https://docs.python.org/2/library/logging.html#logger-objects]

Further documentation on loggers

Logging from Spiders

Scrapy provides a logger within each Spider instance, which can be accessed and used like this:

import scrapy class MySpider(scrapy.Spider): name = 'myspider' start_urls = ['https://scrapinghub.com'] def parse(self, response): self.logger.info('Parse function called on %s', response.url)

That logger is created using the Spider’s name, but you can use any custom Python logger you want. For example:

import logging import scrapy logger = logging.getLogger('mycustomlogger') class MySpider(scrapy.Spider): name = 'myspider' start_urls = ['https://scrapinghub.com'] def parse(self, response): logger.info('Parse function called on %s', response.url)

Logging configuration

Loggers on their own don’t manage how messages sent through them are displayed. For this task, different「handlers」can be attached to any logger instance and they will redirect those messages to appropriate destinations, such as the standard output, files, emails, etc.

By default, Scrapy sets and configures a handler for the root logger, based on the settings below.

Logging settings

These settings can be used to configure the logging:

LOG_FILE

LOG_ENABLED

LOG_ENCODING

LOG_LEVEL

LOG_FORMAT

LOG_DATEFORMAT

LOG_STDOUT

LOG_SHORT_NAMES

The first couple of settings define a destination for log messages. If LOG_FILE is set, messages sent through the root logger will be redirected to a file named LOG_FILE with encoding LOG_ENCODING. If unset and LOG_ENABLED is True, log messages will be displayed on the standard error. Lastly, if LOG_ENABLED is False, there won’t be any visible log output.

LOG_LEVEL determines the minimum level of severity to display, those messages with lower severity will be filtered out. It ranges through the possible levels listed in Log levels.

LOG_FORMAT and LOG_DATEFORMAT specify formatting strings used as layouts for all messages. Those strings can contain any placeholders listed in logging’s logrecord attributes docs [https://docs.python.org/2/library/logging.html#logrecord-attributes] and datetime’s strftime and strptime directives [https://docs.python.org/2/library/datetime.html#strftime-and-strptime-behavior] respectively.

If LOG_SHORT_NAMES is set, then the logs will not display the scrapy component that prints the log. It is unset by default, hence logs contain the scrapy component responsible for that log output.

Command-line options

There are command-line arguments, available for all commands, that you can use to override some of the Scrapy settings regarding logging.

--logfile FILE

Overrides LOG_FILE

--loglevel/-L LEVEL

Overrides LOG_LEVEL

--nolog

Sets LOG_ENABLED to False

See also

Module logging.handlers [https://docs.python.org/2/library/logging.handlers.html]

Further documentation on available handlers

Custom Log Formats

A custom log format can be set for different actions by extending LogFormatter class and making LOG_FORMATTER point to your new class.

class scrapy.logformatter.LogFormatter

Class for generating log messages for different actions.

All methods must return a dictionary listing the parameters level, msg and args which are going to be used for constructing the log message when calling logging.log.

Dictionary keys for the method outputs:

level is the log level for that action, you can use those from the python logging library [https://docs.python.org/3/library/logging.html] : logging.DEBUG, logging.INFO, logging.WARNING, logging.ERROR and logging.CRITICAL.

msg should be a string that can contain different formatting placeholders. This string, formatted with the provided args, is going to be the long message for that action.

args should be a tuple or dict with the formatting placeholders for msg. The final log message is computed as msg % args.

Users can define their own LogFormatter class if they want to customize how each action is logged or if they want to omit it entirely. In order to omit logging an action the method must return None.

Here is an example on how to create a custom log formatter to lower the severity level of the log message when an item is dropped from the pipeline:

class PoliteLogFormatter(logformatter.LogFormatter): def dropped(self, item, exception, response, spider): return { 'level': logging.INFO, # lowering the level from logging.WARNING 'msg': u"Dropped: %(exception)s" + os.linesep + "%(item)s", 'args': { 'exception': exception, 'item': item, } }

crawled(request, response, spider)

Logs a message when the crawler finds a webpage.

dropped(item, exception, response, spider)

Logs a message when an item is dropped while it is passing through the item pipeline.

scraped(item, response, spider)

Logs a message when an item is scraped by a spider.

Advanced customization

Because Scrapy uses stdlib logging module, you can customize logging using all features of stdlib logging.

For example, let’s say you’re scraping a website which returns many HTTP 404 and 500 responses, and you want to hide all messages like this:

2016-12-16 22:00:06 [scrapy.spidermiddlewares.httperror] INFO: Ignoring response <500 http://quotes.toscrape.com/page/1-34/>: HTTP status code is not handled or not allowed

The first thing to note is a logger name - it is in brackets: [scrapy.spidermiddlewares.httperror]. If you get just [scrapy] then LOG_SHORT_NAMES is likely set to True; set it to False and re-run the crawl.

Next, we can see that the message has INFO level. To hide it we should set logging level for scrapy.spidermiddlewares.httperror higher than INFO; next level after INFO is WARNING. It could be done e.g. in the spider’s __init__ method:

import logging import scrapy class MySpider(scrapy.Spider): # ... def __init__(self, *args, **kwargs): logger = logging.getLogger('scrapy.spidermiddlewares.httperror') logger.setLevel(logging.WARNING) super().__init__(*args, **kwargs)

If you run this spider again then INFO messages from scrapy.spidermiddlewares.httperror logger will be gone.

scrapy.utils.log module

scrapy.utils.log.configure_logging(settings=None, install_root_handler=True)

Initialize logging defaults for Scrapy.

Parameters

settings (dict, Settings object or None) – settings used to create and configure a handler for the root logger (default: None).

install_root_handler (bool [https://docs.python.org/3/library/functions.html#bool]) – whether to install root logging handler (default: True)

This function does:

Route warnings and twisted logging through Python standard logging

Assign DEBUG and ERROR level to Scrapy and Twisted loggers respectively

Route stdout to log if LOG_STDOUT setting is True

When install_root_handler is True (default), this function also creates a handler for the root logger according to given settings (see Logging settings). You can override default options using settings argument. When settings is empty or None, defaults are used.

configure_logging is automatically called when using Scrapy commands or CrawlerProcess, but needs to be called explicitly when running custom scripts using CrawlerRunner. In that case, its usage is not required but it’s recommended.

If you plan on configuring the handlers yourself is still recommended you call this function, passing install_root_handler=False. Bear in mind there won’t be any log output set by default in that case.

To get you started on manually configuring logging’s output, you can use logging.basicConfig() [https://docs.python.org/2/library/logging.html#logging.basicConfig] to set a basic root handler. This is an example on how to redirect INFO or higher messages to a file:

import logging from scrapy.utils.log import configure_logging configure_logging(install_root_handler=False) logging.basicConfig( filename='log.txt', format='%(levelname)s: %(message)s', level=logging.INFO )

Refer to Run Scrapy from a script for more details about using Scrapy this way.

Stats Collection

Scrapy provides a convenient facility for collecting stats in the form of key/values, where values are often counters. The facility is called the Stats Collector, and can be accessed through the stats attribute of the Crawler API, as illustrated by the examples in the Common Stats Collector uses section below.

However, the Stats Collector is always available, so you can always import it in your module and use its API (to increment or set new stat keys), regardless of whether the stats collection is enabled or not. If it’s disabled, the API will still work but it won’t collect anything. This is aimed at simplifying the stats collector usage: you should spend no more than one line of code for collecting stats in your spider, Scrapy extension, or whatever code you’re using the Stats Collector from.

Another feature of the Stats Collector is that it’s very efficient (when enabled) and extremely efficient (almost unnoticeable) when disabled.

The Stats Collector keeps a stats table per open spider which is automatically opened when the spider is opened, and closed when the spider is closed.

Common Stats Collector uses

Access the stats collector through the stats attribute. Here is an example of an extension that access stats:

class ExtensionThatAccessStats(object): def __init__(self, stats): self.stats = stats @classmethod def from_crawler(cls, crawler): return cls(crawler.stats)

Set stat value:

stats.set_value('hostname', socket.gethostname())

Increment stat value:

stats.inc_value('custom_count')

Set stat value only if greater than previous:

stats.max_value('max_items_scraped', value)

Set stat value only if lower than previous:

stats.min_value('min_free_memory_percent', value)

Get stat value:

>>> stats.get_value('custom_count') 1

Get all stats:

>>> stats.get_stats() {'custom_count': 1, 'start_time': datetime.datetime(2009, 7, 14, 21, 47, 28, 977139)}

Available Stats Collectors

Besides the basic StatsCollector there are other Stats Collectors available in Scrapy which extend the basic Stats Collector. You can select which Stats Collector to use through the STATS_CLASS setting. The default Stats Collector used is the MemoryStatsCollector.

MemoryStatsCollector

class scrapy.statscollectors.MemoryStatsCollector

A simple stats collector that keeps the stats of the last scraping run (for each spider) in memory, after they’re closed. The stats can be accessed through the spider_stats attribute, which is a dict keyed by spider domain name.

This is the default Stats Collector used in Scrapy.

spider_stats

A dict of dicts (keyed by spider name) containing the stats of the last scraping run for each spider.

DummyStatsCollector

class scrapy.statscollectors.DummyStatsCollector

A Stats collector which does nothing but is very efficient (because it does nothing). This stats collector can be set via the STATS_CLASS setting, to disable stats collect in order to improve performance. However, the performance penalty of stats collection is usually marginal compared to other Scrapy workload like parsing pages.

Sending e-mail

Although Python makes sending e-mails relatively easy via the smtplib [https://docs.python.org/2/library/smtplib.html] library, Scrapy provides its own facility for sending e-mails which is very easy to use and it’s implemented using Twisted non-blocking IO [https://twistedmatrix.com/documents/current/core/howto/defer-intro.html], to avoid interfering with the non-blocking IO of the crawler. It also provides a simple API for sending attachments and it’s very easy to configure, with a few settings.

Quick example

There are two ways to instantiate the mail sender. You can instantiate it using the standard constructor:

from scrapy.mail import MailSender mailer = MailSender()

Or you can instantiate it passing a Scrapy settings object, which will respect the settings:

mailer = MailSender.from_settings(settings)

And here is how to use it to send an e-mail (without attachments):

mailer.send(to=["someone@example.com"], subject="Some subject", body="Some body", cc=["another@example.com"])

MailSender class reference

MailSender is the preferred class to use for sending emails from Scrapy, as it uses Twisted non-blocking IO [https://twistedmatrix.com/documents/current/core/howto/defer-intro.html], like the rest of the framework.

class scrapy.mail.MailSender(smtphost=None, mailfrom=None, smtpuser=None, smtppass=None, smtpport=None)

Parameters

smtphost (str [https://docs.python.org/3/library/stdtypes.html#str] or bytes [https://docs.python.org/3/library/stdtypes.html#bytes]) – the SMTP host to use for sending the emails. If omitted, the MAIL_HOST setting will be used.

mailfrom (str [https://docs.python.org/3/library/stdtypes.html#str]) – the address used to send emails (in the From: header). If omitted, the MAIL_FROM setting will be used.

smtpuser – the SMTP user. If omitted, the MAIL_USER setting will be used. If not given, no SMTP authentication will be performed.

smtppass (str [https://docs.python.org/3/library/stdtypes.html#str] or bytes [https://docs.python.org/3/library/stdtypes.html#bytes]) – the SMTP pass for authentication.

smtpport (int [https://docs.python.org/3/library/functions.html#int]) – the SMTP port to connect to

smtptls (boolean) – enforce using SMTP STARTTLS

smtpssl (boolean) – enforce using a secure SSL connection

classmethod from_settings(settings)

Instantiate using a Scrapy settings object, which will respect these Scrapy settings.

Parameters

settings (scrapy.settings.Settings object) – the e-mail recipients

send(to, subject, body, cc=None, attachs=(), mimetype='text/plain', charset=None)

Send email to the given recipients.

Parameters

to (str [https://docs.python.org/3/library/stdtypes.html#str] or list of str) – the e-mail recipients

subject (str [https://docs.python.org/3/library/stdtypes.html#str]) – the subject of the e-mail

cc (str [https://docs.python.org/3/library/stdtypes.html#str] or list of str) – the e-mails to CC

body (str [https://docs.python.org/3/library/stdtypes.html#str]) – the e-mail body

attachs (iterable) – an iterable of tuples (attach_name, mimetype, file_object) where attach_name is a string with the name that will appear on the e-mail’s attachment, mimetype is the mimetype of the attachment and file_object is a readable file object with the contents of the attachment

mimetype (str [https://docs.python.org/3/library/stdtypes.html#str]) – the MIME type of the e-mail

charset (str [https://docs.python.org/3/library/stdtypes.html#str]) – the character encoding to use for the e-mail contents

Mail settings

These settings define the default constructor values of the MailSender class, and can be used to configure e-mail notifications in your project without writing any code (for those extensions and code that uses MailSender).

MAIL_FROM

Default: 'scrapy@localhost'

Sender email to use (From: header) for sending emails.

MAIL_HOST

Default: 'localhost'

SMTP host to use for sending emails.

MAIL_PORT

Default: 25

SMTP port to use for sending emails.

MAIL_USER

Default: None

User to use for SMTP authentication. If disabled no SMTP authentication will be performed.

MAIL_PASS

Default: None

Password to use for SMTP authentication, along with MAIL_USER.

MAIL_TLS

Default: False

Enforce using STARTTLS. STARTTLS is a way to take an existing insecure connection, and upgrade it to a secure connection using SSL/TLS.

MAIL_SSL

Default: False

Enforce connecting using an SSL encrypted connection

Telnet Console

Scrapy comes with a built-in telnet console for inspecting and controlling a Scrapy running process. The telnet console is just a regular python shell running inside the Scrapy process, so you can do literally anything from it.

The telnet console is a built-in Scrapy extension which comes enabled by default, but you can also disable it if you want. For more information about the extension itself see Telnet console extension.

Warning

It is not secure to use telnet console via public networks, as telnet doesn’t provide any transport-layer security. Having username/password authentication doesn’t change that.

Intended usage is connecting to a running Scrapy spider locally (spider process and telnet client are on the same machine) or over a secure connection (VPN, SSH tunnel). Please avoid using telnet console over insecure connections, or disable it completely using TELNETCONSOLE_ENABLED option.

How to access the telnet console

The telnet console listens in the TCP port defined in the TELNETCONSOLE_PORT setting, which defaults to 6023. To access the console you need to type:

telnet localhost 6023 Trying localhost... Connected to localhost. Escape character is '^]'. Username: Password: >>>

By default Username is scrapy and Password is autogenerated. The autogenerated Password can be seen on scrapy logs like the example below:

2018-10-16 14:35:21 [scrapy.extensions.telnet] INFO: Telnet Password: 16f92501e8a59326

Default Username and Password can be overriden by the settings TELNETCONSOLE_USERNAME and TELNETCONSOLE_PASSWORD.

Warning

Username and password provide only a limited protection, as telnet is not using secure transport - by default traffic is not encrypted even if username and password are set.

You need the telnet program which comes installed by default in Windows, and most Linux distros.

Available variables in the telnet console

The telnet console is like a regular Python shell running inside the Scrapy process, so you can do anything from it including importing new modules, etc.

However, the telnet console comes with some default variables defined for convenience:

Shortcut

Description

crawler

the Scrapy Crawler (scrapy.crawler.Crawler object)

engine

Crawler.engine attribute

spider

the active spider

slot

the engine slot

extensions

the Extension Manager (Crawler.extensions attribute)

stats

the Stats Collector (Crawler.stats attribute)

settings

the Scrapy settings object (Crawler.settings attribute)

est

print a report of the engine status

prefs

for memory debugging (see Debugging memory leaks)

p

a shortcut to the pprint.pprint function

hpy

for memory debugging (see Debugging memory leaks)

Telnet console usage examples

Here are some example tasks you can do with the telnet console:

View engine status

You can use the est() method of the Scrapy engine to quickly show its state using the telnet console:

telnet localhost 6023 >>> est() Execution engine status time()-engine.start_time : 8.62972998619 engine.has_capacity() : False len(engine.downloader.active) : 16 engine.scraper.is_idle() : False engine.spider.name : followall engine.spider_is_idle(engine.spider) : False engine.slot.closing : False len(engine.slot.inprogress) : 16 len(engine.slot.scheduler.dqs or []) : 0 len(engine.slot.scheduler.mqs) : 92 len(engine.scraper.slot.queue) : 0 len(engine.scraper.slot.active) : 0 engine.scraper.slot.active_size : 0 engine.scraper.slot.itemproc_size : 0 engine.scraper.slot.needs_backout() : False

Pause, resume and stop the Scrapy engine

To pause:

telnet localhost 6023 >>> engine.pause() >>>

To resume:

telnet localhost 6023 >>> engine.unpause() >>>

To stop:

telnet localhost 6023 >>> engine.stop() Connection closed by foreign host.

Telnet Console signals

scrapy.extensions.telnet.update_telnet_vars(telnet_vars)

Sent just before the telnet console is opened. You can hook up to this signal to add, remove or update the variables that will be available in the telnet local namespace. In order to do that, you need to update the telnet_vars dict in your handler.

Parameters

telnet_vars (dict [https://docs.python.org/3/library/stdtypes.html#dict]) – the dict of telnet variables

Telnet settings

These are the settings that control the telnet console’s behaviour:

TELNETCONSOLE_PORT

Default: [6023, 6073]

The port range to use for the telnet console. If set to None or 0, a dynamically assigned port is used.

TELNETCONSOLE_HOST

Default: '127.0.0.1'

The interface the telnet console should listen on

TELNETCONSOLE_USERNAME

Default: 'scrapy'

The username used for the telnet console

TELNETCONSOLE_PASSWORD

Default: None

The password used for the telnet console, default behaviour is to have it autogenerated

Web Service

webservice has been moved into a separate project.

It is hosted at:

https://github.com/scrapy-plugins/scrapy-jsonrpc