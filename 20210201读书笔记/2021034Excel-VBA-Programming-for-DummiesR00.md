by Michael Alexander and John Walkenbach

Excel® VBA Programming For Dummies®, 5th Edition

Copyright © 2019 by John Wiley & Sons, Inc., Hoboken, New Jersey

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

## Introduction

Greetings, prospective Excel programmer. . .

You no doubt have your reasons for picking up a book on VBA programming. Maybe you got a new job (congratulations). Maybe you're trying to automate some of the repetitive data crunching tasks you have to do. Maybe you're just a nerd at heart. Whatever the reason, thank you for choosing this book.

Inside, you find everything you need to get up and running with VBA fast. Even if you don't have the foggiest idea of what programming is all about, this book can help. Unlike most programming books, this one is filled with information designed to include just what you need to know to quickly ramp your VBA programming skillset.

### 01. About This Book

Go to any large bookstore (in-person or online), and you'll find many Excel books. A quick overview can help you decide whether this book is really right for you.

This book: 1) Is designed for intermediate to advanced Excel users who want to get up to speed with Visual Basic for Applications (VBA) programming. 2) Requires no previous programming experience. 3) Covers the most commonly used commands. 4) Is appropriate for Excel 2013, Excel 2016, or Excel 2019. 5) Just might make you crack a smile occasionally.

If you're using Excel 2003, you need a much older book (and a hug). If you're using Excel 2007 or 2010, this book might be okay, but some things have changed. You'd probably be better off with the previous edition.

Oh, yeah — this is not an introductory Excel book. If you're looking for a general-purpose Excel book, check out either of the following books, which are both published by Wiley:

Excel 2019 For Dummies, by Greg Harvey

Excel 2019 Bible, by Michael Alexander and Dick Kusleika

These books are also available in editions for earlier versions of Excel.

Notice that the title of this book isn't「 The Complete Guide to Excel VBA Programming For Dummies.」 This book doesn't cover all aspects of Excel programming — but then again, you probably don't want to know everything about this topic.

If you consume this book and find that you're hungry for a more comprehensive Excel programming book, you might try Microsoft Excel 2019 Power Programming with VBA, also published by Wiley. And yes, editions for older versions of Excel are also available.

### 02. Obligatory Typographical Conventions Section

All computer books have a section like this. (I think some federal law requires it.) Read it or skip it. Sometimes, I refer to key combinations — which means you hold down one key while you press another. For example, Ctrl+Z means you hold down the Ctrl key while you press Z.

For menu commands, I use a distinctive character to separate items on the Ribbon or menu. For example, you use the following command to create a named range in a worksheet:

Formulas => Defined Names => Define Name

Formulas is the tab at the top of the Ribbon, Defined Names is the Ribbon group, and Define Name is the actual command.

The Visual Basic Editor still uses old-fashioned menus and toolbars. So Tools => Options means choose the Tools menu and then choose the Options menu item.

Excel programming involves developing code — that is, the instructions Excel follows. All code in this book appears in a monospace font, like this:

```c
Range("A1:A12").Select
```

Some long lines of code don't fit between the margins in this book. In such cases, I use the standard VBA line-continuation character sequence: a space followed by an underscore character. Here's an example:

```c
Selection.PasteSpecial Paste:=xlValues, _
Operation:=xlNone, SkipBlanks:=False, _
Transpose:=False
```

When you enter this code, you can type it as written or place it on a single line (omitting the space and underscore combination).

### 03. Check Your Security Settings

It's a cruel world out there. It seems that some scam artist is always trying to take advantage of you or cause some type of problem. The world of computing is equally cruel. You probably know about computer viruses, which can cause some nasty things to happen to your system. But did you know that computer viruses can also reside in an Excel file? It's true. In fact, it's relatively easy to write a computer virus by using VBA. An unknowing user can open an Excel file and spread the virus to other Excel workbooks and to other systems.

Over the years, Microsoft has become increasingly concerned about security issues. This is a good thing, but it also means that Excel users need to understand how things work. You can check Excel's security settings by choosing File => Options => Trust Center => Trust Center Settings. There is a plethora of options in there, and people have been known to open that dialog box and never be heard from again.

If you click the Macro Settings tab (on the left side of the Trust Center dialog box), your options are as follows:

1 Disable all macros without notification. Macros will not work, regardless of what you do.

2 Disable all macros with notification. When you open a workbook with macros, you see the Message Bar open with an option you can click to enable macros, or (if the Visual Basic Editor window is open) you get a message asking if you want to enable macros.

3 Disable all macros except digitally signed macros. Only macros with a digital signature are allowed to run (but even for those signatures you haven't marked as trusted, you still get the security warning).

4 Enable all macros. All macros run with no warnings. This option is not recommended because potentially dangerous code can be executed.

Consider this scenario: You spend a week writing a killer VBA program that will revolutionize your company. You test it thoroughly and then send it to your boss. He calls you into his office and claims that your macro doesn't do anything at all.

What's going on? Chances are, your boss's security setting doesn't allow macros to run. Or maybe he chose to go along with Microsoft's default suggestion and disable the macros when he opened the file.

Bottom line? Just because an Excel workbook contains a macro no guarantee that the macro will ever be executed. It all depends on the security setting and whether the user chooses to enable or disable macros for that file.

To work with this book, you need to enable macros for the files you work with. My advice is to use the second security level. Then, when you open a file that you've created, you can simply enable the macros. If you open a file from someone you don't know, you should disable the macros and check the VBA code to ensure that it doesn't contain anything destructive or malicious. Usually, it's pretty easy to identify suspicious VBA code.

Another option is to designate a trusted folder. Choose File => Options => Trust Center => Trust Center Settings. Select the Trusted Locations option and then designate a particular folder as a trusted location. Store your trusted workbooks there, and Excel won't bug you about enabling macros. For example, if you download the sample files for this book, you can put them in a trusted location.

### 04. Foolish Assumptions

People who write books usually have a target reader in mind. The following points more or less describe the hypothetical target reader for this book:

1 You have access to a PC at work — and probably at home. And those computers are connected to the Internet.

2 You're running Excel 2013, Excel 2016, or Excel 2019.

3 You've been using computers for several years.

4 You use Excel frequently in your work, and you consider yourself to be more knowledgeable about Excel than the average bear.

5 You need to make Excel do some things that you currently can't make it do.

6 You have little or no programming experience.

7 You understand that the Help system in Excel can actually be useful. Face it — this book doesn't cover everything. If you get on good speaking terms with the Help system, you'll be able to fill in some of the missing pieces.

8 You need to accomplish some work, and you have a low tolerance for thick, boring computer books.

### 05. Icons Used in This Book

Don't skip information marked with this icon. It identifies a shortcut that can save you lots of time (and maybe even allow you to leave the office at a reasonable hour). This icon is also used to let you know that the code being discussed is available on the web. Download it to eliminate lots of typing.

This icon tells you when you need to store information in the deep recesses of your brain for later use.

This icon flags material that you might consider technical. You may find it interesting, but you can safely skip it if you're in a hurry.

Read anything marked with this icon. Otherwise, you may lose your data, blow up your computer, cause a nuclear meltdown — or maybe even ruin your whole day.

### 06. Sample Files Online

This book has its very own website where you can download the example files. To get these files, point your web browser to:

[Excel VBA Programming For Dummies, 5th Edition - dummies](https://www.dummies.com/programming/vba/excel-vba-programming-for-dummies-5th-edition/)

Please note that this URL is case-sensitive and uses all lowercase letters. If you don't type it exactly, it won't work.

2『已下载书籍的示例代码作为本书的附件「2021034Excel-VBA-Programming-for-Dummies附件」。（2021-03-21）』

Having the sample files will save you a lot of typing. Better yet, you can play around with them and experiment with various changes. In fact, experimentation is the best way to master VBA.

### 07. Where to Go from Here

This book contains everything you need to learn VBA programming at a mid-advanced level. The book starts off with the basics of recording macros and builds, chapter by chapter.

If you're completely new to Excel macros, start with Part 1 to get a refresher on the fundamentals of recording macros. If you have experience recording macros, but want to better understand the VBA behind them, go to Part 2. There, you gain a concise understanding of how VBA works, along with the basic foundation you need to implement your own code.

Finally, if you're familiar with programming concepts and just want to get a quick runthrough of some of the more advanced techniques like creating your custom functions and add-ins, feel free to jump to Part 4. There's also the cheat sheet filled with handy shortcuts. Go to dummies.com and search for「Excel VBA programming cheat sheet」to find it.