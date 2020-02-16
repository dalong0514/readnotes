## 05. Handling JavaScript

### 1. 逻辑脉络

用自己的话总结主题，梳理逻辑脉络，也就是这本书整个地图里这一章所在的节点。

### 2. 摘录及评论

In this chapter we looked at some approaches to scrape websites that utilize JavaScript. We looked at the mainstream Selenium using a web browser to execute JavaScript and then went to the headless world, where you don’t need any window to execute JavaScript and this makes your scripts portable and easier to execute. Naturally, using another tool to get some extra rendering done takes time and provides overhead. If you don’t require JavaScript rendering, create your scripts without any add-ons like Splash or Selenium. You’ll benefit from the speed gain.

1『尽量通过其他途径规避抓取涉及 JS 的信息。』

This chapter is all about handling websites that utilize JavaScript to render information dynamically. You have seen in the previous chapters that a basic website scraper loads the web page’s contents and does its extraction on this source code. And if there’s JavaScript included, it’s not executed, and the dynamic information is missing from the page. This is bad, at least in those cases where you need that dynamic data. Another interesting part of scraping websites that use JavaScript is that you may need clicks or button presses to go to the right page/get the right content, because these actions call a chain of JavaScript functions.

Now I will give you options for how you can deal with these problems. Most of the time you will find Selenium as the solution, if you Google or search the Internet with other engines. However, there are other options present, and I will give you more insight. Perhaps those other options will fit your needs better.


