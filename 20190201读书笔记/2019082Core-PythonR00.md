# 2019082Core-PythonR00

原文出版时间：2012 年

## 记忆时间

## 卡片

### 0101. 反常识卡——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡——regular expression

a regular expression is a string that use special symbols and characters to indicate pattern repetition or to represent multiple characters so that they can “match” a set of strings with similar characteristics described by the pattern. In other words, they enable matching of multiple strings—a regex pattern that matched only one string would be rather boring and ineffective.

### 0202. 术语卡——pattern-matching

Throughout this chapter, you will find references to searching and matching. When we are strictly discussing regular expressions with respect to patterns in strings, we will say “matching,” referring to the term pattern-matching. In Python terminology, there are two main ways to accomplish pattern-matching: searching, that is, looking for a pattern match in any part of a string; and matching, that is, attempting to match a pattern to an entire string (starting from the beginning). Searches are accomplished by using the search() function or method, and matching is done with the match() function or method. In summary, we keep the term “matching” universal when referencing patterns, and we differentiate between “searching” and “matching” in terms of how Python accomplishes pattern-matching.

### 0203. 术语卡——贪婪匹配

In the previous table, we notice the question mark is used more than once (overloaded), meaning either matching 0 or 1 occurrences, or its other meaning: if it follows any matching using the close operators, it will direct the regular expression engine to match as few repetitions as possible.

What does “as few repetitions as possible” mean? When patternmatching is employed using the grouping operators, the regular expression engine will try to “absorb” as many characters as possible that match the pattern. This is known as being greedy. The question mark tells the engine to lay off and, if possible, take as few characters as possible in the current match, leaving the rest to match as many succeeding characters of the next pattern (if applicable). Toward the end of the chapter, we will show you a great example where non-greediness is required. For now, let’s continue to look at the closure operators:

### 0301. 人名卡——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

### 0401. 金句卡——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 任意卡——

最后还有一张任意卡，记录个人阅读感想。

## 书评

### 01

不得不说，这本书的翻译错误非常之多，多到我不可想象。各种错误都有，有时候一页上就有两个地方有错。不过这些错误大多都不影响阅读，不过肯定还有些我没发现的错误吧。我对这个翻译者的声望真的到仇恨了。但是话说回来，这的确是本好书，尤其是每一小节后面的核心笔记，讲解了一些有用的编程技巧和知识。而且知识点很细致，我学到了之前不知道的编程知识，并且网上搜一下，又获得了更细致的资料，越看越开心。

### 02

这本书确实不是给初学者的，我们有必要在乎一下书名里面的「核心」二字，虽然它也在介绍了基础性的东西，但作为入门教材的话，我最前面提到的那几本入门教材都比它合适。为什么呢？这本书对 Python 底层知识做了很多详细的介绍，这些介绍对需要进阶的 Python 用户是来说是十分必要和有用的，但是对于初学者来说这些知识反而会阻碍它们的 Python 的学习（因为他们确实还不需要知道那么多）。而且从编排来看，这本书整体并不是循序渐进的方式，作者在每章都试图对这章的内容从浅到深进行介绍，但是章与章之间是几乎平行的。这也是进阶类书籍的一个特点，而入门类的书籍一般整体上呈现循序渐进的特点。

看了豆瓣上的评论，有不少人觉得值得，但差评不少。前面有一篇书评《书是好书，遇见需时机》，深有感触，不对的时机就像前面提到的看《Python 灰帽子》，我不记得看了这本书到底给我了什么收获（或许真的没什么收获）。大部分时候不是书不好，只是没遇到对的读者，读者永远比书多，适合每个读者的书根本不存在。

### 06

总体看下来，觉得这书其实不错：几乎涵盖了 Python 所有主流的应用情景，如果是紧急项目很有可能通过此书来简单地快速开发；作者对代码和 API 讲解也容易弄懂。因为同样的应用场景我在 Java 下做过开发，很容易理解，不过真心不推荐初学者食用该书，概念性的东西作者一笔带过，把重点放在项目的开发（比如网络协议还没搞懂，上来直接就套接字编程），而且可惜的是因为涉及的方面过多因此都没有达到「入门」水准，广而不精。

## PREFACE

The changes brought about in version 3.x continue the trend of iterating and improving the language, taking a larger step toward removing some of its last major flaws, and representing a bigger jump in the continuing evolution of the language. Similarly, the structure of the book is also making a rather significant transition. Due to its size and scope, Core Python Programming as it has existed wouldn’t be able to handle all the new material introduced in this third edition.

Therefore, Prentice Hall and I have decided the best way of moving forward is to take that logical division represented by Parts I and II of the previous editions, representing the core language and advanced applications topics, respectively, and divide the book into two volumes at this juncture. You are holding in your hands (perhaps in eBook form) the second half of the third edition of Core Python Programming. The good news is that the first half is not required in order to make use of the rich amount of content in this volume. We only recommend that you have intermediate Python experience. If you’ve learned Python recently and are fairly comfortable with using it, or have existing Python skills and want to take it to the next level, then you’ve come to the right place!

As existing Core Python Programming readers already know, my primary focus is teaching you the core of the Python language in a comprehensive manner, much more than just its syntax (which you don’t really need a book to learn, right?). Knowing more about how Python works under the hood—including the relationship between data objects and memory management—will make you a much more effective Python programmer right out of the gate. This is what Part I, and now Core Python Language Fundamentals, is all about.

• Web-based e-mail examples (Chapter 3)

• Using Tile/Ttk (Chapter 5)

• Using MongoDB (Chapter 6)

• More significant Outlook and PowerPoint examples (Chapter 7)

• Web server gateway interface (WSGI) (Chapter 10)

• Using Twitter (Chapter 13)

• Using Google+ (Chapter 15)

In addition, we are proud to introduce three brand new chapters to the book: Chapter 11, “Web Frameworks: Django,” Chapter 12, “Cloud Computing: Google App Engine,” and Chapter 14, “Text Processing.” These represent new or ongoing areas of application development for which Python is used quite often. All existing chapters have been refreshed and updated to the latest versions of Python, possibly including new material. Take a look at the chapter guide that follows for more details on what to expect from every part of this volume.

### Chapter Guide

This book is divided into three parts. The first part, which takes up about two-thirds of the text, gives you treatment of the "core" members of an application development toolset  (with Python being the focus, of course). The second part concentrates on a variety of topics, all tied to Web programming. The book concludes with the supplemental section which provides experimental chapters that are under development and hopefully will grow into independent chapters in future editions.

All three parts provide a set of various advanced topics to show what you can build by using Python. We are certainly glad that we were at least able to provide you with a good introduction to many of the key areas of Python development including some of the topics mentioned previously Following is a more in-depth, chapter-by-chapter guide.

#### Part l: General Application Topics

Chapter 1 regular Expressions. Regular expressions are a powerful tool that you can use for pattern matching, extracting, and search-and-replace functionality.

Chapter 2 network Programming. So many applications today need to be network oriented. In this chapter, you learn to create clients and servers using TCP/IP and UDP/IP as well as get an introduction to Socketserver and Twisted.

Chapter 3 internet Client Programming. Most Internet protocols in use today were developed using sockets. In Chapter 3, we explore some of those higher-level libraries that are used to build clients of these Internet protocols. In particular, we focus on file transfer (FTP), the Usenet news protocol (NNTP), and a variety of e-mail protocols  (SMTP POP3, IMAP4).

Chapter 4 multithreaded Programming. Multithreaded programming is one way to improve the execution performance of many types of applications by introducing concurrency. This chapter ends the drought of written documentation on how to implement threads in Python by explaining the concepts and showing you how to correctly build a Python multithreaded application and what the best use Cases are.

Chapter 5 GUI Programming. Based on the Tk graphical toolkit, Tkinter (renamed to tkinter in Python 3) is Python's default GUI development library. We introduce Tkinter to you by showing you how to build simple GUI applications. One of the best ways to learn is to copy, and by building on top of some of these applications, you will be on your way in no time. We conclude the chapter by taking a brief look at other graphical libraries, such as Tix, Pmw, wxpython, PYGTK, and Ttk/Tile.

Chapter 6 database Programming. Python helps simplify database programming, as well. We first review basic concepts and then introduce you to the Python database application programmers interface (db-apt). We then show you how you can connect to a relational database and perform queries and operations by using Python. If you prefer a hands-off approach that uses the Structured Query Language  (SQL) and want to just work with objects without having to worry about the underlying database layer, we have object-relational managers (ORMS) just for that purpose. Finally, we introduce you to the world of non-relational databases, experimenting with Mongodb as our NOSQL example.

Chapter 7 programming Microsoft Office. Like it or not, we live in a world where we will likely have to interact with Microsoft Windows-based PCs. It might be intermittent or something we have to deal with on a daily basis, but regardless of how much exposure we face, the power of Python can be used to make our lives easier. In this chapter, we explore COM Client programming by using Python to control and communicate with Office applications, such as Word, Excel, Power-Point, and Outlook. Although experimental in the previous edition, we're glad we were able to add enough material to turn this into a standalone chapter.

Chapter 8 extending Python. We mentioned earlier how powerful it is to be able to reuse code and extend the language. In pure Python, these extensions are modules and packages, but you can also develop lower-level code in C/C++, C#, or Java. Those extensions then can interface with Python in a seamless fashion. Writing your extensions in a lower-level programming language gives you added performance and some security (because the source code does not have to be revealed). This chapter walks you step-by-step through the extension building process using C.

#### Part ll Web Development

Chapter 9 web Clients and Servers. Extending our discussion of client-server architecture in Chapter 2, we apply this concept to the Web. In this chapter, we not only look at clients, but also explore a variety of Web client tools, parsing Web content, and finally, we introduce you to customizing your own Web servers in Python.

Chapter 10 Web Programming: CGI and WSGI. The main job of Web servers is to take client requests and return results. But how do servers get that data? Because they’re really only good at returning results, they generally do not have the capabilities or logic necessary to do so; the heavy lifting is done elsewhere. CGI gives servers the ability to spawn another program to do this processing and has historically been the solution, but it doesn’t scale and is thus not really used in practice; however, its concepts still apply, regardless of what framework(s) you use, so we’ll spend most of the chapter learning CGI. You will also learn how WSGI helps application developers by providing them a common programming interface. In addition, you’ll see how WSGI helps framework developers who have to connect to Web servers on one side and application code on the other so that application developers can write code without having to worry about the execution platform.

Chapter 11 Web Frameworks: Django. Python features a host of Web frameworks with Django being one of the most popular. In this chapter, you get an introduction to this framework and learn how to write simple Web applications. With this knowledge, you can then explore other Web frameworks as you wish.

Chapter 12 cloud Computing: Google App Engine. Cloud computing is taking the industry by storm. While the world is most familiar with infrastructure services like Amazon’s AWS and online applications such as Gmail and Yahoo! Mail, platforms present a powerful alternative that take advantage of infrastructure without user involvement but give more flexibility than cloud software because you control the application and its code. In this chapter, you get a comprehensive introduction to the first platform service using Python, Google App Engine. With the knowledge gained here, you can then explore similar services in the same space.

Chapter 13 web Services. In this chapter we explore higher-level services on the Web (using HTTP). We look at an older service (Yahoo! Finance) and a newer one  (Twitter) You learn how to interact with both of these services by using Python as well as knowledge you've gained from earlier chapters.

#### Part Ill: Supplemental/Experimental

Chapter 14 text Processing. Our first supplemental chapter introduces you to text processing using Python. We first explore CSV, then JSON, and finally XML. In the last part of this chapter, we take our client/server knowledge from earlier in the book and combine it XML to look at how you can create online remote procedure calls (RPC) services by using XML-RPC.

Chapter 15 Miscellaneous. This chapter consists of bonus material that we will likely develop into full, individual chapters in the next edition. Topics covered here include Java/Jython and Google+.

## 01. Regular Expressions

### 1. 逻辑脉络

用自己的话总结主题，梳理逻辑脉络，也就是这本书整个地图里这一章所在的节点。

### 2. 摘录及评论

### 1.1 Introduction / Motivation

Manipulating text or data is a big thing. If you don’t believe me, look very carefully at what computers primarily do today. Word processing, “fillout-form” Web pages, streams of information coming from a database dump, stock quote information, news feeds—the list goes on and on. Because we might not know the exact text or data that we have programmed our machines to process, it becomes advantageous to be able to express it in patterns that a machine can recognize and take action upon.

If I were running an e-mail archiving company, and you, as one of my customers, requested all of the e-mail that you sent and received last February, for example, it would be nice if I could set a computer program to collate and forward that information to you. Another example request might be to look for a subject line like “ILOVEYOU,” indicating a virus-infected message, and remove those e-mail messages from your personal archive. So this begs the question of how we can program machines with the ability to look for patterns in text.

Regular expressions provide such an infrastructure for advanced text pattern matching, extraction, and/or search-and-replace functionality. To put it simply, a regular expression (a.k.a. a “regex” for short) is a string that use special symbols and characters to indicate pattern repetition or to represent multiple characters so that they can “match” a set of strings with similar characteristics described by the pattern (Figure 1-1). In other words, they enable matching of multiple strings—a regex pattern that matched only one string would be rather boring and ineffective, wouldn’t you say?

2『给出了正则的定义：a regular expression is a string that use special symbols and characters to indicate pattern repetition or to represent multiple characters so that they can “match” a set of strings with similar characteristics described by the pattern. In other words, they enable matching of multiple strings—a regex pattern that matched only one string would be rather boring and ineffective. 做一张术语卡片。』

Figure 1-1 You can use regular expressions, such as the one here, which recognizes valid Python identifiers. [A-Za-z]\w+ means the first character should be alphabetic, that is, either A–Z or a–z, followed by at least one (+) alphanumeric character (\w). In our filter, notice how many strings go into the filter, but the only ones to come out are the ones we asked for via the regex. One example that did not make it was “4xZ” because it starts with a number. 

Python supports regexes through the standard library re module. In this introductory subsection, we will give you a brief and concise introduction. Due to its brevity, only the most common aspects of regexes used in everyday Python programming will be covered. Your experience will, of course, vary. We highly recommend reading any of the official supporting documentation as well as external texts on this interesting subject. You will never look at strings in the same way again!

CORE NOTE: Searching vs. matching

Throughout this chapter, you will find references to searching and matching. When we are strictly discussing regular expressions with respect to patterns in strings, we will say “matching,” referring to the term pattern-matching. In Python terminology, there are two main ways to accomplish pattern-matching: searching, that is, looking for a pattern match in any part of a string; and matching, that is, attempting to match a pattern to an entire string (starting from the beginning). Searches are accomplished by using the search() function or method, and matching is done with the match() function or method. In summary, we keep the term “matching” universal when referencing patterns, and we differentiate between “searching” and “matching” in terms of how Python accomplishes pattern-matching.

1『在 Python 里正则的模式匹配其实包含 2 个内容：搜索和匹配。searching, that is, looking for a pattern match in any part of a string; and matching, that is, attempting to match a pattern to an entire string (starting from the beginning). Searches are accomplished by using the search() function or method, and matching is done with the match() function or method. 做一张术语卡片。』

As we mentioned earlier, regexes are strings containing text and special characters that describe a pattern with which to recognize multiple strings. We also briefly discussed a regular expression alphabet. For general text, the alphabet used for regular expressions is the set of all uppercase and lowercase letters plus numeric digits. Specialized alphabets are also possible; for instance, you can have one consisting of only the characters “0” and “1.” The set of all strings over this alphabet describes all binary strings, that is, “0,” “1,” “00,” “01,” “10,” “11,” “100,” etc.

Let’s look at the most basic of regular expressions now to show you that although regexes are sometimes considered an advanced topic, they can also be rather simplistic. Using the standard alphabet for general text, we present some simple regexes and the strings that their patterns describe. The following regular expressions are the most basic, “true vanilla,” as it were. They simply consist of a string pattern that matches only one string: the string defined by the regular expression. We now present the regexes followed by the strings that match them:

The first regular expression pattern from the above chart is “foo.” This pattern has no special symbols to match any other symbol other than those described, so the only string that matches this pattern is the string “foo.” The same thing applies to “Python” and “abc123.” The power of regular expressions comes in when special characters are used to define character sets, subgroup matching, and pattern repetition. It is these special symbols that allow a regex to match a set of strings rather than a single one.

1『正则的核心是 special charaters。special characters are used to define character sets, subgroup matching, and pattern repetition. It is these special symbols that allow a regex to match a set of strings rather than a single one. 』

### 1.2 Special Symbols and Characters

We will now introduce the most popular of the special characters and symbols, known as metacharacters, which give regular expressions their power and flexibility. You will find the most common of these symbols and characters in Table 1-1.

1『这里的表格内信息值得反复看。』

#### 1.2.1 Matching More Than One Regex Pattern with Alternation (|)

The pipe symbol (|) indicates an alternation operation. It is used to separate different regular expressions. For example, the following are some patterns that employ alternation, along with the strings they match:

With this one symbol, we have just increased the flexibility of our regular expressions, enabling the matching of more than just one string. Alternation is also sometimes called union or logical OR.

1『择一匹配符，能够增强正则表达式的灵活性，使得正则表达式能够匹配多个字符串而不仅仅只是一个字符串。择一匹配有时候也称作并（union）或者逻辑或（logical OR）。』

『 at | home 是 at、home；r2d2 | c3po 是 r2d2、c3po；bat | bet | bit 是 bat、bet、bit。』

#### 1.2.2 Matching Any Single Character (.)

The dot or period (.) symbol matches any single character except for \n. (Python regexes have a compilation flag [S or DOTALL], which can override this to include \ns.) Whether letter, number, whitespace (not including “\n”), printable, non-printable, or a symbol, the dot can match them all. Q: What if I want to match the dot or period character? A: To specify a dot character explicitly, you must escape its functionality with a backslash, as in “\.”.

『 f.o 匹配在字母“f”和“o”之间的任意一个字符；例如 fao、f9o、f#o 等；.. 是任意两个字符；.end 是匹配在字符串 end 之前的任意一个字符。』

#### 1.2.3 Matching from the Beginning or End of Strings or Word Boundaries (^, \$, \b, \B)

There are also symbols and related special characters to specify searching for patterns at the beginning and end of strings. To match a pattern starting from the beginning, you must use the carat symbol (^) or the special character \A (backslash-capital “A”). The latter is primarily for keyboards that do not have the carat symbol (for instance, an international keyboard). Similarly, the dollar sign (\$) or \Z will match a pattern from the end of a string.

Patterns that use these symbols differ from most of the others we describe in this chapter because they dictate location or position. In the previous Core Note, we noted that a distinction is made between matching (attempting matches of entire strings starting at the beginning) and searching (attempting matches from anywhere within a string). With that said, here are some examples of “edge-bound” regex search patterns:

『使用这些符号的模式与本章描述的其他大多数模式是不同的，因为这些模式指定了位置或方位。之前的「核心提示」记录了匹配（试图在字符串的开始位置进行匹配）和搜索（试 图从字符串的任何位置开始匹配）之间的差别。』

Again, if you want to match either (or both) of these characters verbatim, you must use an escaping backslash. For example, if you wanted to match any string that ended with a dollar sign, one possible regex solution would be the pattern 

    .*\$$

The special characters \b and \B pertain to word boundary matches. The difference between them is that \b will match a pattern to a word boundary, meaning that a pattern must be at the beginning of a word, whether there are any characters in front of it (word in the middle of a string) or not (word at the beginning of a line). And likewise, \B will match a pattern only if it appears starting in the middle of a word (i.e., not at a word boundary). Here are some examples:

『 ^From 是任何以 From 作为起始的字符串；/bin/tcsh\$ 是任何以/bin/tcsh 作为结尾的字符串；^Subject: hi\$ 是任何由单独的字符串 Subject: hi 构成的字符串。』

#### 1.2.4 Creating Character Classes ([])

Whereas the dot is good for allowing matches of any symbols, there might be occasions for which there are specific characters that you want to match. For this reason, the bracket symbols ([]) were invented. The regular expression will match any of the enclosed characters. Here are some examples:

『b[aeiu]t 是匹配 bat、bet、bit、but；[cr][23][dp][o2] 是匹配，一个包含四个字符的字符串，第一个字符是“c”或“r”，然后是“2”或“3”，后面 是“d”或“p”，最后要么是“o”要么是“2”。例如，c2do、r3p2、r2d2、c3po 等。』

1『感觉 [] 匹配模式好强大，它能匹配含有 [] 里任意字符的文本，只要把想筛选的所有可能的字符塞进 [] 里即可。但注意 [] 只能匹配单个字符，里面的字符全是「逻辑或」的关系。』

One side note regarding the regex [cr][23][dp][o2]—a more restrictive version of this regex would be required to allow only “r2d2” or “c3po” as valid strings. Because brackets merely imply logical OR functionality, it is not possible to use brackets to enforce such a requirement. The only solution is to use the pipe, as in r2d2|c3po.

For single-character regexes, though, the pipe and brackets are equivalent. For example, let’s start with the regular expression “ab,” which matches only the string with an “a” followed by a “b.” If we wanted either a one-letter string, for instance, either “a” or a “b,” we could use the regex [ab]. Because “a” and “b” are individual strings, we can also choose the regex a|b. However, if we wanted to match the string with the pattern “ab” followed by “cd,” we cannot use the brackets because they work only for single characters. In this case, the only solution is ab|cd, similar to the r2d2/c3po problem just mentioned.

3『对于单个字符的正则表达式，使用择一匹配和字符集是等效的。例如，我们以正则表达式 "ab" 作为开始，该正则表达式只匹配包含字母 "a" 且后面跟着字母 "b" 的字符串，如果我们想要匹配一个字母的字符串，例如，要么匹配 "a"，要么匹配 "b"，就可以使用正则表达式 [ab]，因为此时字母 "a" 和字母 "b" 是相互独立的字符串。我们也可以选择正则表达式 a|b。然而，如果我们想要匹配满足模式 "ab" 后面且跟着 "cd" 的字符串，我们就不能使用方括号，因为字符集的方法只适用于单字符的情况。这种情况下，唯一的方法就是使用 ab|cd，这与刚オ提到的 r2d2/c3po 问题是相同的。』

#### 1.2.5 Denoting Ranges (-) and Negation (^)

In addition to single characters, the brackets also support ranges of characters. A hyphen between a pair of symbols enclosed in brackets is used to indicate a range of characters; for example A–Z, a–z, or 0–9 for uppercase letters, lowercase letters, and numeric digits, respectively. This is a lexicographic range, so you are not restricted to using just alphanumeric characters. Additionally, if a caret (^) is the first character immediately inside the open left bracket, this symbolizes a directive not to match any of the characters in the given character set.

『 z.[0-9] 是字母“z”后面跟着任何一个字符，然后跟着一个数字；[r-u][env-y][us] 是字母“r”、“s”、“t”或者“u”后面跟着“e”、“n”、“v”、“w”、“x”或者“y”，然后跟着“u”或者“s”；[^aeiou] 是一个非元音字符（练习：为什么我们说“非元音”而不是“辅音”？）；[^\t\n] 是不匹配制表符或者 \n；[“-a] 是在一个 ASCII 系统中，所有字符都位于“”和“a”之间，即 34~97 之间。』

1『原来 [^XX] 是否定掉 [] 里的所有字符，之前的理解又偏误。（2020-03-30）』

#### 1.2.6 Multiple Occurrence/Repetition Using Closure Operators (*, +, ?, {})

We will now introduce the most common regex notations, namely, the special symbols \*, +, and ?, all of which can be used to match single, multiple, or no occurrences of string patterns. The asterisk or star operator (*) will match zero or more occurrences of the regex immediately to its left (in language and compiler theory, this operation is known as the Kleene Closure). The plus operator (+) will match one or more occurrences of a regex (known as Positive Closure), and the question mark operator (?) will match exactly 0 or 1 occurrences of a regex.

1『Kleene Closure、Positive Closure，又见名词「闭包」。』

There are also brace operators ({}) with either a single value or a comma-separated pair of values. These indicate a match of exactly N occurrences (for {N}) or a range of occurrences; for example, {M, N} will match from M to N occurrences. These symbols can also be escaped by using the backslash character; \\* matches the asterisk, etc.

In the previous table, we notice the question mark is used more than once (overloaded), meaning either matching 0 or 1 occurrences, or its other meaning: if it follows any matching using the close operators, it will direct the regular expression engine to match as few repetitions as possible.

1『

目前知道 ? 有 2 个用法：一是匹配 0 或者 1 次；二是作为贪婪匹配的标识，如果问号紧跟在任何使用闭合操作符的匹配后面，它将直接要求正则表达式引擎匹配尽可能少的次数；三是扩展表示法的时候是以 ? 开头的。之前网上看到的匹配 html 标签的正则就是采用了第 2 个用法：

    <div(([\s\S])*?)<\/div>

』

What does “as few repetitions as possible” mean? When patternmatching is employed using the grouping operators, the regular expression engine will try to “absorb” as many characters as possible that match the pattern. This is known as being greedy. The question mark tells the engine to lay off and, if possible, take as few characters as possible in the current match, leaving the rest to match as many succeeding characters of the next pattern (if applicable). Toward the end of the chapter, we will show you a great example where non-greediness is required. For now, let’s continue to look at the closure operators:

『当模式匹配使用分组操作符时，正则表达式引擎将试图「吸收」匹配该模式的尽可能多的字符。这通常被叫做贪婪匹配。问号要求正则表达式引擎去「偷懒」，如果可能，就在当前的正则表达式中尽可能少地匹配字符，留下尽可能多的字符给后面的模式（如果存在）。』

2『greedy，贪婪匹配的概念终于出来了。做一张术语卡片。』

1『注意，使用特殊字符匹配的是其前面的那个字母。[dn]ot? 是字母 d 或者 n，后面跟着一个 o，然后是最多一个 t，例如，do、no、dot、not；[0-9]{15,16} 是匹配 15 或者 16 个数字（例如信用卡号码）；\</?[^>]+> 是匹配全部有效的（和无效的）HTML 标签；[KQRBNP][a-h][1-8]-[a-h][1-8] 是在「长代数」标记法中，表示国际象棋合法的棋盘移动（仅移动，不包括吃子和将军）。 即 K、Q、R、B、N 或 P 等字母后面加上 a1～h8 之间的棋盘坐标。 前面的坐标表示从哪里开始走棋，后面的坐标代表走到哪个位置（棋格）上。』

#### 1.2.7 Special Characters Representing Character Sets

We also mentioned that there are special characters that can represent character sets. Rather than using a range of “0–9,” you can simply use \d to indicate the match of any decimal digit. Another special character, \w, can be used to denote the entire alphanumeric character class, serving as a shortcut for [A-Za-z0-9_], and \s can be used for whitespace characters. Uppercase versions of these strings symbolize non-matches; for example, \D matches any non-decimal digit (same as [^0-9]), etc. Using these shortcuts, we will present a few more complex examples:

1『这几个特殊字符大写表示不匹配，之前忽略了这个重要信息点，比如 re.sub('[/S]', '', string) 表示剔除 string 字符串里所有非空格字符的内容，空格字符其实不仅仅包含空格，换行符、制表符也是。』

『 \w+-\d+ 是一个由字母数字组成的字符串和一串由一个连字符分隔的数字；[A-Za-z]\w* 是第一个字符是字母，其余字符（如果存在）可以是字母或者数字（几乎等价于 Python 中的有 效标识符［参见练习］；\d{3}-\d{3}-\d{4} 是美国电话号码的格式，前面是区号前缀，例如 800-555-1212；\w+@\w+\.com 是以 XXX@YYY.com 格式表示的简单电子邮件地址。）』

#### 1.2.8 Designating Groups with Parentheses (())

Now, we have achieved the goal of matching a string and discarding nonmatches, but in some cases, we might also be more interested in the data that we did match. Not only do we want to know whether the entire string matched our criteria, but also whether we can extract any specific strings or substrings that were part of a successful match. The answer is yes. To accomplish this, surround any regex with a pair of parentheses. 

『有些时候我们可能会对之前匹配成功的数据更感兴趣。我们不仅想要知道整个字符串是否匹配我们的标准而且想要知道能否提取任何已经成功匹配的特定字符串或者子字符串。』

A pair of parentheses () can accomplish either (or both) of the following when used with regular expressions: 1) Grouping regular expressions. 2) Matching subgroups.

1『 () 可以实现的 2 个功能：一是对正则表达式进行分组，二是匹配子组。』

One good example of why you would want to group regular expressions is when you have two different regexes with which you want to compare a string. Another reason is to group a regex in order to use a repetition operator on the entire regex (as opposed to an individual character or character class).

One side effect of using parentheses is that the substring that matched the pattern is saved for future use. These subgroups can be recalled for the same match or search, or extracted for post-processing. You will see some examples of pulling out subgroups at the end of Section 1.3.9.

Why are matches of subgroups important? The main reason is that there are times when you want to extract the patterns you match, in addition to making a match. For example, what if we decided to match the pattern \w+-\d+ but wanted save the alphabetic first part and the numeric second part individually? We might want to do this because with any successful match, we might want to see just what those strings were that matched our regex patterns.

If we add parentheses to both subpatterns such as (\w+)-(\d+), then we can access each of the matched subgroups individually. Subgrouping is preferred because the alternative is to write code to determine we have a match, then execute another separate routine (which we also had to create) to parse the entire match just to extract both parts. Why not let Python do it; it’s a supported feature of the re module, so why reinvent the wheel?

『为何想要对正则表达式进行分组：一是当有两个不同的正则表达式而且想用它们来比较同一个字符串时。二是对正则表达式进行分组可以在整个正则表达式中使用重复操作符（而不是一个单独的字符或者字符集）。使用圆括号进行分组的一个作用就是，匹配模式的子字符串可以保存起来供后续使用。这些子组能够被同一次的匹配或者搜索重复调用，或者提取出来用于后续处理。为什么匹配子组这么重要呢？主要原因是在很多时候除了进行匹配操作以外，我们还想要提取所匹配的模式。例如，如果决定匹配模式 w+-d+，但是想要分别保存第一部分的字母和第二部分的数字，该如何实现？我们可能想要这样做的原因是，对于任何成功的匹配，我们可能想要看到这些匹配正则表达式模式的字符串究竟是什么？如果为两个子模式都加上圆括号，例如（w+)-(d+），然后就能够分别访问每一个匹配子组。我们更倾向于使用子组，这是因为择一匹配通过编写代码来判断是否匹配，然后执行另一个单独的程序（该程序也需要另行创建）来解析整个匹配仅仅用于提取两个部 分。为什么不让 Python 自己实现呢？这是 re 模块支持的一个特性。』

『 \d+(\.\d*)? 是表示简单浮点数的字符串，也就是说，任何十进制数字，后面可以接一个小数点和零个或 者多个十进制数字，例如“0.004”、“2”、“75.”等。』

『 (Mr?s?\.)?[A-Z][a-z]*[A-Za-z-]+ 是名字和姓氏，以及对名字的限制（如果有，首字母必须大写，后续字母小写），全名前可以有可选的“Mr.”、“Mrs.”、“Ms.”或者“M.”作为称谓，以及灵活可选的姓氏，可以有多个单词、横线以及大写字母。』

#### 1.2.9 Extension Notations

One final aspect of regular expressions we have not touched upon yet include the extension notations that begin with the question mark symbol (? . . .). We are not going to spend a lot of time on these as they are generally used more to provide flags, perform look-ahead (or look-behind), or check conditionally before determining a match. Also, although parentheses are used with these notations, only (?P\<name>) represents a grouping for matches. All others do not create a group. However, you should still know what they are because they might be “the right tool for the job.”

1『在扩展表示法了 () 表示的分组失效了，除了 (?P\<name>) 这种形式。』

『 (?:\w+\.)* 以句点作为结尾的字符串，例如“google.”、“twitter.”、“facebook.”，但是这些匹配不会保存下来供后续的使用和数据检索；(?#comment) 此处并不做匹配，只是作为注释；(?=.com) 如果一个字符串后面跟着“.com”才做匹配操作，并不使用任何目标字符串；(?!.net) 如果一个字符串后面不是跟着“.net”才做匹配操作；(?<=800-) 如果字符串之前为“800-”才做匹配，假定为电话号码，同样，并不使用任何输入字符串；(?<!192\.168\.) 如果一个字符串之前不是“192.168.” 才做匹配操作，假定用于过滤掉一组 C 类 IP 地址；(?(1)y|x) 如果一个匹配组 1(\1) 存在，就与 y 匹配；否则，就与 x 匹配。』

### 1.3 Regexes and Python

Now that we know all about regular expressions, we can examine how Python currently supports regular expressions through the re module, which was introduced way back in ancient history (Python 1.5), replacing the deprecated regex and regsub modules—both modules were removed from Python in version 2.5, and importing either module from that release on triggers an ImportError exception. The re module supports the more powerful and regular Perl-style (Perl 5) regexes, allows multiple threads to share the same compiled regex objects, and supports named subgroups.

『 re 模块支持更强大而且更通用的 Perl 风格（Perl 5 风格）的正则表达式，该模块允许多个线程共享同一个已编译的正则表达式对象，也支持命名子组。』

#### 1.3.1 The re Module: Core Functions and Methods

The chart in Table 1-2 lists the more popular functions and methods from the re module. Many of these functions are also available as methods of compiled regular expression objects (regex objects and regex match objects. In this subsection, we will look at the two main functions/methods, match() and search(), as well as the compile() function. We will introduce several more in the next section.

1『上面的表里有用的函数很多，多看看。函数基本的传参是正则匹配模式、要匹配的字符串以及参数 flags（默认为 0），匹配成功的话返回的是匹配对象，失败的话返回 None。』

CORE NOTE: Regex compilation (to compile or not to compile?)

In the Execution Environment chapter of Core Python Programming or the forthcoming Core Python Language Fundamentals, we describe how Python code is eventually compiled into bytecode, which is then executed by the interpreter. In particular, we specified that calling eval() or exec (in version 2.x or exec() in version 3.x) with a code object rather than a string provides a performance improvement due to the fact that the compilation process does not have to be performed repeatedly. In other words, using precompiled code objects is faster than using strings because the interpreter will have to compile it into a code object (anyway) each time before execution.

The same concept applies to regexes—regular expression patterns must be compiled into regex objects before any pattern matching can occur. For regexes, which are compared many times during the course of execution, we highly recommend using precompilation because, again, regexes have to be compiled anyway, so doing it ahead of time is prudent for performance reasons. re.compile() provides this functionality.

The module functions do cache the compiled objects, though, so it’s not as if every search() and match() with the same regex pattern requires compilation. Still, you save the cache lookups and do not have to make function calls with the same string, over and over. The number of compiled regex objects that are cached might vary between releases, and is undocumented. The purge() function can be used to clear this cache.

### 1.3.2 Compiling Regexes with compile()

Almost all of the re module functions we will be describing shortly are available as methods for regex objects. Remember, even though we recommend it, precompilation is not required. If you compile, you will use methods; if you don’t, you will just use functions. The good news is that either way, the names are the same, whether a function or a method. (This is the reason why there are module functions and methods that are identical; for example, search(), match(), etc., in case you were wondering.) Because it saves one small step for most of our examples, we will use strings, instead. We will throw in a few with compilation, though, just so you know how it is done.

Optional flags may be given as arguments for specialized compilation. These flags allow for case-insensitive matching, using system locale settings for matching alphanumeric characters, etc. Please see the entries in Table 1-2 and the official documentation for more information on these flags (re.IGNORECASE, re.MULTILINE, re.DOTALL, re.VERBOSE, etc.). They can be combined by using the bitwise OR operator (|).

These flags are also available as a parameter to most re module functions. If you want to use these flags with the methods, they must already be integrated into the compiled regex objects, or you need to use the (?F) notation directly embedded in the regex itself, where F is one or more of i (for re.I/IGNORECASE), m (for re.M/MULTILINE), s (for re.S/DOTALL), etc. If more than one is desired, you place them together rather than using the bitwise OR operation; for example, (?im) for both re.IGNORECASE plus re.MULTILINE.

『如果需要编译，就使用编译过的方法；如果不需要编译，就使用函数。幸运的是，不管使用函数还是方法，它们的名字都是相同的（也许你曾对此感到好奇，这就是模块函数和方法的名字相同的原因，例如，search()、match() 等）。因为这在大多数示例中省去一个小步骤，所以我们将使用字符串替代。我们仍将会遇到几个预编译代码的对象，这样就可以知道它的过程是怎么回事。对于一些特别的正则表达式编译，可选的标记可能以参数的形式给出，这些标记允许不区分大小写的匹配，使用系统的本地化设置来匹配字母数字，等等。请参考表 1-2 中的条目以及在正式的官方文档中查询关于这些标记（re.IGNORECASE、re.MULTILINE、re.DOTALL、 re.VERBOSE 等）的更多信息。它们可以通过按位或操作符（|）合并。这些标记也可以作为参数适用于大多数 re 模块函数。如果想要在方法中使用这些标记，它们必须已经集成到已编译的正则表达式对象之中，或者需要使用直接嵌入到正则表达式本身的（?F）标记，其中 F 是一个或者多个 i（用于 re.I/IGNORECASE）、m（用于 re.M/MULTILINE）、s（用于 re.S/DOTALL）等。如果想要同时使用多个，就把它们放在一起而不是使用按位或操作， 例如，（?im）可以用于同时表示 re.IGNORECASE 和 re.MULTILINE。』

### 1.3.3 Match Objects and the group() and groups() Methods

When dealing with regular expressions, there is another object type in addition to the regex object: the match object. These are the objects returned on successful calls to match() or search(). Match objects have two primary methods, group() and groups(). group() either returns the entire match, or a specific subgroup, if requested. groups() simply returns a tuple consisting of only/all the subgroups. If there are no subgroups requested, then groups() returns an empty tuple while group() still returns the entire match.

1『除了正则对象外，匹配成功返回的匹配对象也很重要，其有 2 个主要的函数，group() 和 groups()。』

Python regexes also allow for named matches, which are beyond the scope of this introductory section. We refer you to the complete re module documentation for a complete listing of the more advanced details we have omitted here.

#### 1.3.4 Matching Strings with match()

match() is the first re module function and regex object (regex object) method we will look at. The match() function attempts to match the pattern to the string, starting at the beginning. If the match is successful, a match object is returned; if it is unsuccessful, None is returned. The group() method of a match object can be used to show the successful match. Here is an example of how to use match() [and group()]:

```py
>>> m = re.match('foo', 'foo')  # pattern matches string 
>>> if m is not None:   # show match if successful
... m.group() ...
'foo'
```

Here is an example of a failed match for which None is returned:

```py
>>> m = re.match('foo', 'bar')# pattern does not match string
>>> if m is not None: 
    m.group() # (1-line version of if clause) ...
```

The preceding match fails, thus None is assigned to m, and no action is taken due to the way we constructed our if statement. For the remaining examples, we will try to leave out the if check for brevity, if possible, but in practice, it is a good idea to have it there to prevent AttributeError exceptions. (None is returned on failures, which does not have a group() attribute [method].) A match will still succeed even if the string is longer than the pattern, as long as the pattern matches from the beginning of the string. For example, the pattern “foo” will find a match in the string “food on the table” because it matches the pattern from the beginning:

```py
>>> m = re.match('foo', 'food on the table') # match succeeds
>>> m.group() 'foo'
```

1『 match() 的原则必须是从字符串的首部开始匹配，所以匹配模式可以用「'/w*'」。注意一点，可以去匹配比正则模式更长的字符串。』

As you can see, although the string is longer than the pattern, a successful match was made from the beginning of the string. The substring “foo” represents the match, which was extracted from the larger string. We can even sometimes bypass saving the result altogether, taking advantage of Python’s object-oriented nature:

```py
>>> re.match('foo', 'food on the table').group() 
'foo'
```

Note from a few paragraphs above that an AttributeError will be generated on a non-match.

#### 1.3.5 Looking for a Pattern within a String with search() (Searching versus Matching)

The chances are greater that the pattern you seek is somewhere in the middle of a string, rather than at the beginning. This is where search() comes in handy. It works exactly in the same way as match, except that it searches for the first occurrence of the given regex pattern anywhere with its string argument. Again, a match object is returned on success; None is returned otherwise. We will now illustrate the difference between match() and search(). Let’s try a longer string match attempt. This time, let’s try to match our string “foo” to “seafood”:

```py
>>> m = re.match('foo', 'seafood')  # no match
>>> if m is not None: m.group() 
...
>>>
```

As you can see, there is no match here. match() attempts to match the pattern to the string from the beginning; that is, the “f” in the pattern is matched against the “s” in the string, which fails immediately. However, the string “foo” does appear (elsewhere) in “seafood,” so how do we get Python to say “yes”? The answer is by using the search() function. Rather than attempting a match, search() looks for the first occurrence of the pattern within the string. search() evaluates a string strictly from left to right.

```py
>>> m = re.search('foo', 'seafood')     # use search() instead
>>> if m is not None: m.group() 
...
'foo' # search succeeds where match failed
>>>
```

Furthermore, both match() and search() take the optional flags parameter described earlier in Section 1.3.2. Lastly, we want to note that the equivalent regex object methods optionally take pos and endpos arguments to specify the search boundaries of the target string.

We will be using the match() and search() regex object methods and the group() and groups() match object methods for the remainder of this subsection, exhibiting a broad range of examples of how to use regular expressions with Python. We will be using almost all of the special characters and symbols that are part of the regular expression syntax.

『等价的正则表达式对象方法使用可选的 pos 和 endpos 参数来指定目标字符串的搜索范围。本节后面将使用 match() 和 search() 正则表达式对象方法以及 group() 和 groups() 匹配对象方法，通过展示大量的实例来说明 Python 中正则表达式的使用方法。我们将使用正则表达式语法中几乎全部的特殊字符和符号。』

#### 1.3.6 Matching More than One String (|)

In Section 1.2, we used the pipe character in the regex bat|bet|bit. Here is how we would use that regex with Python:

```py
>>> bt = 'bat|bet|bit'              # regex pattern: bat, bet, bit
>>> m = re.match(bt, 'bat')     # 'bat' is a match
>>> if m is not None: m.group() ...

'bat'

>>> m = re.match(bt, 'blt')     # no match for 'blt'
>>> if m is not None: m.group() ...

>>> m = re.match(bt, 'He bit me!') # does not match string
>>> if m is not None: m.group() ...

>>> m = re.search(bt, 'He bit me!') # found 'bit' via search
>>> if m is not None: m.group() ...
'bit'
```

#### 1.3.7 Matching Any Single Character (.)

In the following examples, we show that a dot cannot match a \n or a noncharacter; that is, the empty string:

```py
>>> anyend = '.end'
>>> m = re.match(anyend, 'bend')    # dot matches 'b'
>>> if m is not None: m.group() ...
'bend'

>>> m = re.match(anyend, 'end')     # no char to match
>>> if m is not None: m.group() ...

>>> m = re.match(anyend, '\nend')   # any char except \n
>>> if m is not None: m.group() ...

>>> m = re.search('.end', 'The end.')   # matches ' ' in search
>>> if m is not None: m.group() ...
' end'
```

The following is an example of searching for a real dot (decimal point) in a regular expression, wherein we escape its functionality by using a backslash:

#### 1.3.8 Creating Character Classes ([])

Earlier, we had a long discussion about [cr][23][dp][o2] and how it differs from r2d2|c3po” In the following examples, we will show that r2d2|c3po is more restrictive than [cr][23][dp][o2]:

#### 1.3.9 Repetition, Special Characters, and Grouping

The most common aspects of regexes involve the use of special characters, multiple occurrences of regex patterns, and using parentheses to group and extract submatch patterns. One particular regex we looked at related to simple e-mail addresses (\w+@\w+\.com). Perhaps we want to match more e-mail addresses than this regex allows. To support an additional host-name that precedes the domain, for example, www.xxx.com as opposed to accepting only xxx.com as the entire domain, we have to modify our existing regex. 

To indicate that the hostname is optional, we create a pattern that matches the hostname (followed by a dot), use the ? operator, indicating zero or one copy of this pattern, and insert the optional regex into our previous regex as follows: \w+@(\w+\.)?\w+\.com. As you can see from the following examples, either one or two names are now accepted before the .com:

1『使用 ？操作符来表示该模式出现零次或者一次，直觉上这个用处超级大。』

```py
>>> patt = '\w+@(\w+\.)?\w+\.com'

>>> re.match(patt, 'nobody@xxx.com').group() 
'nobody@xxx.com'

>>> re.match(patt, 'nobody@www.xxx.com').group() 
'nobody@www.xxx.com'
```

Furthermore, we can even extend our example to allow any number of intermediate subdomain names with the following pattern. Take special note of our slight change from using ? to \*. : \w+@(\w+\.)*\w+\.com:

```py
>>> patt = '\w+@(\w+\.)*\w+\.com'

>>> re.match(patt, 'nobody@www.xxx.yyy.zzz.com').group() 
'nobody@www.xxx.yyy.zzz.com'
```

However, we must add the disclaimer that using solely alphanumeric characters does not match all the possible characters that might make up e-mail addresses. The preceding regex patterns would not match a domain such as xxx-yyy.com or other domains with \W characters. 

Earlier, we discussed the merits of using parentheses to match and save subgroups for further processing rather than coding a separate routine to manually parse a string after a regex match had been determined. In particular, we discussed a simple regex pattern of an alphanumeric string and a number separated by a hyphen, \w+-\d+, and how adding subgrouping to form a new regex, (\w+)-(\d+), would do the job. Here is how the original regex works:

```py
>>> m = re.match('\w\w\w-\d\d\d', 'abc-123')
>>> if m is not None: m.group()
'abc-123'

>>> m = re.match('\w\w\w-\d\d\d', 'abc-xyz')
>>> if m is not None: m.group()
...
>>>
```

In the preceding code, we created a regex to recognize three alphanumeric characters followed by three digits. Testing this regex on abc-123, we obtained positive results, whereas abc-xyz fails. We will now modify our regex as discussed before to be able to extract the alphanumeric string and number. Note how we can now use the group() method to access individual subgroups or the groups() method to obtain a tuple of all the subgroups matched:

```py
>>> m = re.match('(\w\w\w)-(\d\d\d)', 'abc-123')
>>> m.group() # entire match 'abc-123'
>>> m.group(1) # subgroup 1 'abc'
>>> m.group(2) # subgroup 2 '123'
>>> m.groups() # all subgroups ('abc', '123')
```

As you can see, group() is used in the normal way to show the entire match, but it can also be used to grab individual subgroup matches. We can also use the groups() method to obtain a tuple of all the substring matches. Here is a simpler example that shows different group permutations, which will hopefully make things even more clear:

1『这个例子充分展示了正则模式里使用分组 () 去匹配的优势。』

```py
>>> m = re.match('ab', 'ab')
>>> m.group() 
'ab'
>>> m.groups()
()
>>>

>>> m = re.match('(ab)', 'ab')
>>> m.group() 
'ab'
>>> m.group(1) 
'ab'
>>> m.groups() 
('ab',)
>>>

>>> m = re.match('(a)(b)', 'ab')
>>> m.group() 
'ab'
>>> m.group(1) 
'a'
>>> m.group(2) 
'b'
>>> m.groups() 
('a', 'b')
>>>

# 下面的匹配不是很明白
>>> m = re.match('(a(b))', 'ab')
>>> m.group() 
'ab'
>>> m.group(1) 
'ab'
>>> m.group(2) 
'b'
>>> m.groups() 
('ab', 'b')
```

#### 1.3.10 Matching from the Beginning and End of Strings and on Word Boundaries

The following examples highlight the positional regex operators. These apply more for searching than matching because match() always starts at the beginning of a string.

```py
>>> m = re.search('^The', 'The end.')   # match
>>> if m is not None: m.group() 
...
'The'

>>> m = re.search('^The', 'end. The')   # not at beginning
>>> if m is not None: m.group() 
...

>>> m = re.search(r'\bthe', 'bite the dog') # at a boundary
>>> if m is not None: m.group() 
...
'the'

>>> m = re.search(r'\bthe', 'bitethe dog') # no boundary
>>> if m is not None: m.group() 
...

>>> m = re.search(r'\Bthe', 'bitethe dog') # no boundary
>>> if m is not None: m.group() 
...
'the'
```

1『 \b 只能匹配单独的单词（有边界），而 /B 可以匹配嵌入到字符串里面的单词。』

You will notice the appearance of raw strings here. You might want to take a look at the Core Note, “Using Python raw strings,” toward the end of this chapter for clarification on why they are here. In general, it is a good idea to use raw strings with regular expressions.

1『r'\bthe' 指原始字符串（ raw strings），传参的正则表达式用原始字符串。』

There are four other re module functions and regex object methods that we think you should be aware of: findall(), sub(), subn(), and split().

#### 1.3.11 Finding Every Occurrence with findall() and finditer()

findall() looks for all non-overlapping occurrences of a regex pattern in a string. It is similar to search() in that it performs a string search, but it differs from match() and search() in that findall() always returns a list. The list will be empty if no occurrences are found, but if successful, the list will consist of all matches found (grouped in left-to-right order of occurrence).

```py
>>> re.findall('car', 'car')
['car']

>>> re.findall('car', 'scary')
['car'] 

>>> re.findall('car', 'carry the barcardi to the car')
['car', 'car', 'car']
```

Subgroup searches result in a more complex list returned, and that makes sense, because subgroups are a mechanism with which you can extract specific patterns from within your single regular expression, such as matching an area code that is part of a complete telephone number, or a login name that is part of an entire e-mail address.

For a single successful match, each subgroup match is a single element of the resulting list returned by findall(); for multiple successful matches, each subgroup match is a single element in a tuple, and such tuples (one for each successful match) are the elements of the resulting list. This part might sound confusing at first, but if you try different examples, it will help to clarify things.

『子组在一个更复杂的返回列表中搜索结果，而且这样做是有意义的，因为子组是允许从单个正则表达式中抽取特定模式的一种机制，例如匹配一个完整电话号码中的一部分（例如区号），或者完整电子邮件地址的一部分（例如登录名称）。对于一个成功的匹配，每个子组匹配是由 findall() 返回的结果列表中的单一元素；对于多个成功的匹配，每个子组匹配是返回的一个元组中的单一元素，而且每个元组（每个元组都对应一个成功的匹配）是结果列表中的元素。这部分内容可能第一次听起来令人迷惑，但是如果你尝试练习过一些不同的示例，就将澄清很多知识点。』

The finditer() function, which was added back in Python 2.2, is a similar, more memory-friendly alternative to findall(). The main difference between it and its cousin, other than the return of an iterator versus a list (obviously), is that rather than returning matching strings, finditer() iterates over match objects. The following are the differences between the two with different groups in a single string:

『finditer() 函数是在 Python 2.2 版本中添加回来的，这是一个与 findall() 函数类似但是更节省内存的变体。两者之间以及和其他变体函数之间的差异（很明显不同于返回的是一个迭代器还是列表）在于，和返回的匹配字符串相比，finditer() 在匹配对象中迭代。如下是在单个字符串中两个不同分组之间的差别。』

```py
>>> s = 'This and that.'
>>> re.findall(r'(th\w+) and (th\w+)', s, re.I) 
[('This', 'that')]

>>> re.finditer(r'(th\w+) and (th\w+)', s, re.I).next().groups() 
('This', 'that')

>>> re.finditer(r'(th\w+) and (th\w+)', s, re.I).next().group(1) 
'This'

>>> re.finditer(r'(th\w+) and (th\w+)', s, re.I).next().group(2) 
'that'

>>> [g.groups() for g in re.finditer(r'(th\w+) and (th\w+)', s, re.I)]
 [('This', 'that')]
```

In the example that follows, we have multiple matches of a single group in a single string:

```py
>>> re.findall(r'(th\w+)', s, re.I) 
['This', 'that']

>>> it = re.finditer(r'(th\w+)', s, re.I)

>>> g = it.next()
>>> g.groups() 
('This',)

>>> g.group(1) 
'This'

>>> g = it.next()
>>> g.groups() 
('that',)

>>> g.group(1) 
'that'

>>> [g.group(1) for g in re.finditer(r'(th\w+)', s, re.I)] 
['This', 'that']
```

Note all the additional work that we had to do using finditer() to get its output to match that of findall(). Finally, like match() and search(), the method versions of findall() and finditer() support the optional pos and endpos parameters that control the search boundaries of the target string, as described earlier in this chapter.

#### 1.3.12 Searching and Replacing with sub() and subn()

There are two functions/methods for search-and-replace functionality: sub() and subn(). They are almost identical and replace all matched occurrences of the regex pattern in a string with some sort of replacement. The replacement is usually a string, but it can also be a function that returns a replacement string. subn() is exactly the same as sub(), but it also returns the total number of substitutions made—both the newly substituted string and the substitution count are returned as a 2-tuple.

『用来替换的部分通常是一个字符串，但它也可能是一个函数，该函数返回一个用来替换的字符串。subn() 和 sub() 一样，但 subn() 还返回一个表示替换的总数，替换后的字符串和表示替换总数的数字一起作为一个拥有两个元素的元组返回。』

```py
>>> re.sub('X', 'Mr. Smith', 'attn: X\n\nDear X,\n')
'attn: Mr. Smith\012\012Dear Mr. Smith,\012' 
>>>

>>> re.subn('X', 'Mr. Smith', 'attn: X\n\nDear X,\n')
('attn: Mr. Smith\012\012Dear Mr. Smith,\012', 2) 
>>>

>>> print re.sub('X', 'Mr. Smith', 'attn: X\n\nDear X,\n')
attn: Mr. Smith
Dear Mr. Smith,

>>> re.sub('[ae]', 'X', 'abcdef')
'XbcdXf'

>>> re.subn('[ae]', 'X’, 'abcdef')
('XbcdXf', 2)
```

As we saw in an earlier section, in addition to being able to pull out the matching group number using the match object’s group() method, you can use \N, where N is the group number to use in the replacement string. Below, we’re just converting the American style of date presentation, MM/ DD/YY{,YY} to the format used by all other countries, DD/MM/YY{,YY}:

```py
>>> re.sub(r'(\d{1,2})/(\d{1,2})/(\d{2}|\d{4})', r'\2/\1/\3', '2/20/91') # Yes, Python is... '20/2/91'

>>> re.sub(r'(\d{1,2})/(\d{1,2})/(\d{2}|\d{4})', r'\2/\1/\3', '2/20/1991') # ... 20+ years old! '20/2/1991'
```

#### 1.3.13 Splitting (on Delimiting Pattern) with split() 

The re module and regex object method split() work similarly to its string counterpart, but rather than splitting on a fixed string, they split a string based on a regex pattern, adding some significant power to string splitting capabilities. If you do not want the string split for every occurrence of the pattern, you can specify the maximum number of splits by setting a value (other than zero) to the max argument. 

If the delimiter given is not a regular expression that uses special symbols to match multiple patterns, then re.split() works in exactly the same manner as str.split(), as illustrated in the example that follows (which splits on a single colon): 

基于正则表达式的模式分隔字符串，为字符串分隔功能添加些额外的威力。如果你不想为每次模式的出现都分割字符串，就可以通过为 max 参数设定个值（非零）来指定最大分割数。如果给定分隔符不是使用特殊符号来匹配多重模式的正则表达式，那么 re.split 与 str.split 的工作方式相同，如下所示（基于单引号分割）。


```py
>>> re.split(':', 'str1:str2:str3') 
['str1', 'str2', 'str3'] 
```

That’s a simple example. What if we have a more complex example, such as a simple parser for a Web site like Google or Yahoo! Maps? Users can enter city and state, or city plus ZIP code, or all three? This requires more powerful processing than just a plain ’ol string split: 

```py
>>> import re 
>>> DATA = ( 'Mountain View, CA 94040', 'Sunnyvale, CA', 'Los Altos, 94023', 'Cupertino 95014', 'Palo Alto CA',  ) 
>>> for datum in DATA: 
... print re.split(', |(?= (?:\d{5} | [A-Z]{2})) ', datum) 
... 
['Mountain View', 'CA', '94040'] ['Sunnyvale', 'CA'] ['Los Altos', '94023'] ['Cupertino', '95014'] ['Palo Alto', 'CA'] 
```

The preceding regex has a simple component, split on comma-space (“, “). The harder part is the last regex, which previews some of the extension notations that you’ll learn in the next subsection. In plain English, this is what it says: also split on a single space if that space is immediately followed by five digits (ZIP code) or two capital letters (US state abbreviation). This allows us to keep together city names that have spaces in them. 

Naturally, this is just a simplistic regex that could be a starting point for an application that parses location information. It doesn’t process (or fails) lowercase states or their full spellings, street addresses, country codes, ZIP+4 (nine-digit ZIP codes), latitude-longitude, multiple spaces, etc. It’s just meant as a simple demonstration of re.split() doing something str.split() can’t do. 
As we just demonstrated, you benefit from much more power with a regular expression split; however, remember to always use the best tool for the job. If a string split is good enough, there’s no need to bring in the additional complexity and performance impact of regexes. 

1『扩展表示法里，「?=XX」表示要匹配的字符紧跟在 XX 后面，比如「?=.com」如果一个字符串后面跟着“.com”才做匹配操作，并不使用任何目标字符串；「?:」是表示返回的匹配对象不会保存下来供后续的使用和数据检索，比如「?= (?:\d{5} | [A-Z]{2})」表示，如果空格紧跟在五个数字（ZIP 编码）或者两个大写字母（美国联邦州缩 写）之后，就用 split 语句分割该空格。前面的解释是书里的，但这个空格是哪冒出来的呢？目前不理解。（2020-03-30）』

『上述正则表达式拥有一个简单的组件：使用 split 语句基于逗号分割字符串。更难的部分是最后的正则表达式，可以通过该正则表达式预览一些将在下一小节中介绍的扩展符号。在普通的英文中，通常这样说：如果空格紧跟在五个数字（ZIP 编码）或者两个大写字母（美国联邦州缩写）之后，就用 pli 语句分割该空格。这就允许我们在城市名中放置空格。通常情况下，这仅仅只是一个简单的正则表达式，可以在用来解析位置信息的应用中作为起点。该正则表达式并不能处理小写的州名或者州名的全拼、街道地址、州编码、ZIP+4  (9 位 ZIP 编码）、经纬度、多个空格等内容（或者在处理时会失败）。这仅仅意味着使用 re.split() 能够实现 str.split() 不能实现的一个简单的演示实例。我们刚刚已经证实，读者将从正则表达式 split 语句的强大能力中获益。然而，记得一定在编码过程中选择更合适的工具。如果对字符串使用 split 方法已经足够好，就不需要引入额外复杂并且影响性能的正则表达式。』

1『正则的 split() 比原生字符串的更强大，原生无法解决或者解决起来很麻烦的考虑用正则分割。』

#### 1.3.14 Extension Notations (?...) 

There are a variety of extension notations supported by Python regular expressions. Let’s take a look at some of them now and provide some usage examples. 

With the (?iLmsux) set of options, users can specify one or more flags directly into a regular expression rather than via compile() or other re module functions. Below are several examples that use re.I/IGNORECASE, with the last mixing in re.M/MULTILINE: 

『通过使用 (?iLmsux) 系列选项，用户可以直接在正则表达式里面指定一个或者多个标记，而不是通过 compile() 或者其他 re 模块函数。下面为一些使用 re.I/IGNORECASE 的示例， 最后一个示例在 re.M/MULTILINE 实现多行混合。』

```py
>>> re.findall(r'(?i)yes', 'yes? Yes. YES!!') 
['yes', 'Yes', 'YES'] 

>>> re.findall(r'(?i)th\w+', 'The quickest way is through this tunnel.') 
['The', 'through', 'this'] 

>>> re.findall(r'(?im)(^th[\w ]+)', """ 
... This line is the first, 
... another line, 
... that line, it's the best 
... """) 
['This line is the first', 'that line'] 
```

1『「?i」表示不区分大小写。』

For the previous examples, the case-insensitivity should be fairly straightforward. In the last example, by using “multiline” we can perform the search across multiple lines of the target string rather than treating the entire string as a single entity. Notice that the instances of “the” are skipped because they do not appear at the beginning of their respective lines. 

The next pair demonstrates the use of re.S/DOTALL. This flag indicates that the dot (.) can be used to represent \n characters (whereas normally it represents all characters except \n): 

```py
>>> re.findall(r'th.+', ''' 
... The first line 
... the second line 
... the third line 
... ''') 
['the second line', 'the third line'] 

>>> re.findall(r'(?s)th.+', ''' 
... The first line 
... the second line 
... the third line ... ''')
 ['the second line\nthe third line\n'] 
```

The re.X/VERBOSE flag is quite interesting; it lets users create more human-readable regular expressions by suppressing whitespace characters within regexes (except those in character classes or those that are backslash-escaped). Furthermore, hash/comment/octothorpe symbols (#) can also be used to start a comment, also as long as they’re not within a character class backslash-escaped: 

『Re. X/VERBOSE 标记非常有趣；该标记允许用户通过抑制在正则表达式中使用空白符（除了在字符类中或者在反斜线转义中）来创建更易读的正则表达式。此外，散列、注释和井号也可以用于一个注释的起始，只要它们不在一个用反斜线转义的字符类中。』

```py
>>> re.search(r'''(?x) 
... \((\d{3})\) # area code 
... [ ] # space 
... (\d{3}) # prefix 
... - # dash .
.. (\d{4}) # endpoint number 
... ''', '(800) 555-1212').groups() 
('800', '555', '1212') 
```

The (?: ...) notation should be fairly popular; with it, you can group parts of a regex, but it does not save them for future retrieval or use. This comes in handy when you don’t want superfluous matches that are saved and never used: 

『(?:…)符号将更流行；通过使用该符号，可以对部分正则表达式进行分组，但是并不会保存该分组用于后续的检索或者应用。当不想保存今后永远不会使用的多余匹配时，这个符号就非常有用。』

```py
>>> re.findall(r'http://(?:\w+\.)*(\w+\.com)', 
... 'http://google.com http://www.google.com http:// code.google.com') 
['google.com', 'google.com', 'google.com'] 

>>> re.search(r'\((?P<areacode>\d{3})\) (?P<prefix>\d{3})-(?:\d{4})', 
... '(800) 555-1212').groupdict() 
{'areacode': '800', 'prefix': '555'} 
```

You can use the (?P\<name>) and (?P=name) notations together. The former saves matches by using a name identifier rather than using increasing numbers, starting at one and going through N, which are then retrieved later by using \1, \2, ... \N. You can retrieve them in a similar manner using \g<name>: 

```py
>>> re.sub(r'\((?P<areacode>\d{3})\) (?P<prefix>\d{3})-(?:\d{4})', 
... 
'(\g<areacode>) 
\g<prefix>-xxxx', 
'(800) 
555-1212') 
'(800) 555-xxxx' 
```

Using the latter, you can reuse patterns in the same regex without specifying the same pattern again later on in the (same) regex, such as in this example, which presumably lets you validate normalization of phone numbers. Here are the ugly and compressed versions followed by a good use of (?x) to make things (slightly) more readable: 

```py
>>> bool(re.match(r'\((?P<areacode>\d{3})\) (?P<prefix>\d{3})-(?P<number>\d{4}) (?P=areacode)-(?P=prefix)-(?P=number) 1(?P=areacode)(?P=prefix)(?P=number)', 
... '(800) 555-1212 800-555-1212 18005551212')) 
True 

>>> bool(re.match(r'''(?x) ... 
... 
# match (800) 555-1212, save areacode, prefix, no. 
... 
\((? P<areacode>\d{3})\)[ ](? P=prefix)-(? P<prefix>\d{3})-(? P=number) P<number>\d{4}) 
... 
... # space 
... [ ] 
... 
... 
# match 800-555-1212 ... 
(? P=areacode)-(? P=prefix)-(?P=number)
... 
... 
# space 
... [ ] 
... 
... 
# match 18005551212 
... 
1(? P=areacode)(? P=prefix)(? P=number) 
... 
... ''', '(800) 555-1212 800-555-1212 18005551212')) 
True 
```

You use the (?=...) and (?!...) notations to perform a lookahead in the target string without actually consuming those characters. The first is the positive lookahead assertion, while the latter is the negative. In the examples that follow, we are only interested in the first names of the persons who have a last name of “van Rossum,” and the next example let’s us ignore e-mail addresses that begin with “noreply” or “postmaster.” 

The third snippet is another demonstration of the difference between findall() and finditer(); we use the latter to build a list of e-mail addresses (in a more memory-friendly way by skipping the creation of the intermediary list that would be thrown away) using the same login names but on a different domain. 

『读者可以使用 (?=...) 和 (?!…)符号在目标字符串中实现一个前视匹配，而不必实际上使用这些字符串。前者是正向前视断言，后者是负向前视断言。在后面的示例中，我们仅仅对姓氏为 “van Rossum” 的人的名字感兴趣，下一个示例中，让我们忽略以 “noreply” 或者 “postmaster” 开头的 e-mail 地址。第三个代码片段用于演示 findall() 和 finditer() 的区别；我们使用后者来构建一个使用相同登录名但不同域名的 e-mail 地址列表（在一个更易于记忆的方法中，通过忽略创建用完即丢弃的中间列表）。』

```py
>>> re.findall(r'\w+(?= van Rossum)', ... ''' ... Guido van Rossum ... Tim Peters ... Alex Martelli ... Just van Rossum ... Raymond Hettinger ... ''') ['Guido', 'Just']

>>> re.findall(r'(?m)^\s+(?!noreply|postmaster)(\w+)',''' ... sales@phptr.com ... postmaster@phptr.com ... eng@phptr.com .. noreply@phptr.com ... admin@phptr.com ''') 
['sales', 'eng', 'admin'] 
>>> ['%s@aw.com' % e.group(1) for e in \ re.finditer(r'(?m)^\s+(?!noreply|postmaster)(\w+)', ''' ... sales@phptr.com ... postmaster@phptr.com ... eng@phptr.com ... noreply@phptr.com ... admin@phptr.com ... ''')] 
['sales@aw.com', 'eng@aw.com', 'admin@aw.com']
```

The last examples demonstrate the use of conditional regular expression matching. Suppose that we have another specialized alphabet consisting only of the characters ‘x’ and ‘y,’ where we only want to restrict the string in such a way that two-letter strings must consist of one character followed by the other. In other words, you can’t have both letters be the same; either it’s an ‘x’ followed by a ‘y’ or vice versa: 

```py
>>> bool(re.search(r'(?:(x)|y)(?(1)y|x)', 'xy')) 
True 
>>> bool(re.search(r'(?:(x)|y)(?(1)y|x)', 'xx')) 
False 
```

『展示了使用条件正则表达式匹配。假定我们拥有另一个特殊字符，它仅仅包含字母“x”和“y”， 我们此时仅仅想要这样限定字符串：两字母的字符串必须由一 个字母跟着另一个字母。换句话说， 你不能同时拥有两个相同的字母；要么由“x”跟着 “y”， 要么相反。』

### 1.3.15 Miscellaneous 

There can be confusion between regular expression special characters and special ASCII symbols. We can use \n to represent a NEWLINE character, but we can use \d meaning a regular expression match of a single numeric digit. 
Problems can occur if there is a symbol used by both ASCII and regular expressions, so in the following Core Note, we recommend the use of Python raw strings to prevent any problems. One more caution: the \w and \W alphanumeric character sets are affected by the re.L/LOCALE and Unicode (re.U/UNICODE) flags. 

1『使用 Python 的原始字符串来避免与 ASCII 的特殊字符产生冲突。』

CORE NOTE: Using Python raw strings

You might have seen the use of raw strings in some of the previous examples. Regular expressions were a strong motivation for the advent of raw strings. The reason lies in the conflicts between ASCII characters and regular expression special characters. As a special symbol, \b represents the ASCII character for backspace, but \b is also a regular expression special symbol, meaning “match” on a word boundary. For the regex compiler to see the two characters \b as your string and not a (single) backspace, you need to escape the backslash in the string by using another backslash, resulting in \\b. 

This can get messy, especially if you have a lot of special characters in your string, adding to the confusion. We were introduced to raw strings in the Sequences chapter of Core Python Programming or Core Python Language Fundamentals, and they can be (and are often) used to help keep regexes looking somewhat manageable. In fact, many Python programmers swear by these and only use raw strings when defining regular expressions. 

Here are some examples of differentiating between the backspace \b and the regular expression \b, with and without raw strings: 

『读者可能在之前的一些示例中见过原始字符串的使用。正则表达式对于探索原始字符串有着强大的动力，原因就在于 ASCII 字符和正则表达式的特殊字符之间存在冲突。作为一个特殊符号，\b 表示 ASCII 字符的退格符，但是 \b 同时也是一个正则表达式的特殊符号， 表示匹配一个单词的边界。对于正则表达式编译器而言，若它把两个 \b 视为字符串内容而不是单个退格符，就需要在字符串中再使用一个反斜线转义反斜线，就像这样：\\b。

这样显得略微杂乱，特别是如果在字符串中拥有很多特殊字符，就会让人感到更加困 惑。我们在 Core Python Programming 或者 Core Python Language Fundamentals 的 Sequence 章节中介绍了原始字符串，而且该原始字符串可以用于（且经常用于）帮助保持正则表达式查找某些可托管的东西。事实上，很多 Python 程序员总是抱怨这个方法，仅仅用原始字符串来定义正则表达式。如下所示的一些示例用于说明退格符 \b 和正则表达式 \b 之间的差异，它们有的使用、 有的不使用原始字符串。』

```py
>>> m = re.match('\bblow', 'blow') # backspace, no match 
>>> if m: m.group() 
... 
>>> m = re.match('\\bblow', 'blow') # escaped \, now it works 
>>> if m: m.group() 
... 
'blow' 

>>> m = re.match(r'\bblow', 'blow') # use raw string instead 
>>> if m: m.group() ... 
'blow' 
```

You might have recalled that we had no trouble using \d in our regular expressions without using raw strings. That is because there is no ASCII equivalent special character, so the regular expression compiler knew that you meant a decimal digit. 

