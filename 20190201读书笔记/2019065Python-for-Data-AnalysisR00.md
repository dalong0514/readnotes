## 记忆时间

## 卡片

### 0101. 新知卡

新知卡，是有什么理论模型、推断证据、故事或行动，挑战了你的既有认知。新知卡的信息结构是：已知 + 新知 + 例子。「已知」建议挑选大众或自己以前的观念或掌握的知识；「新知」建议挑选自己更新之后的新知。「例子」建议使用自己日常生活中碰到过的事情，这样更容易记忆。新知卡举例如下：

{
已知：通过熟人找工作更容易。

新知：社会学家马克·格兰诺维特的弱联系理论告诉我们，在大多数人寻找工作的过程中，弱联系的那些人起到的作用最大。

例子：读本科时，我的第一份实习工作是一个统计论坛上素未谋面的朋友介绍的。
}

请通过文档提炼一张新知卡，新知的主题是：「认识到人类的认知可以是科学研究而不光是哲学思辩的对象还不到 150 年」。尽可能多的列举文档中的例子，并将例子具体展开。开始前请先重新阐述任务。

#### 1.1 新知卡 —— XXXX

已知：在过去，人们普遍认为人类的认知是哲学思辩的对象，而非科学研究的领域。

新知：然而，近 150 年来，科学家们开始将人类的认知视为科学研究的对象。这一转变的起点可以追溯到 19 世纪末的心理学的诞生，特别是威廉·詹姆斯的开创性工作。

例子：

1、威廉·詹姆斯是心理学的奠基人之一，他的研究使我们开始将人类的认知视为科学研究的对象。他的著作《心理学原理》是第一本系统性地研究人类认知的科学著作，它开启了认知科学的新篇章。

2、在 20 世纪，认知科学的发展进一步推动了我们对人类认知的科学研究。例如，艾伦·图灵的工作，他提出了「图灵测试」，这是一个判断机器是否具有人类智能的测试，这个测试的提出，使我们开始思考人类认知的本质和可能性。

3、另一个例子是诺姆·乔姆斯基的生成语法理论，他的理论挑战了我们对人类语言认知的理解，使我们开始从科学的角度研究语言的本质（页码：9）。

参考：约翰·R.安德森.(2012).认知心理学及其启示.(裕林，程瑶，周海燕，译).人民邮电出版社 => 0101. 认知的科学

唯一编码：202305292046

打印备注：2023-05-29

### 0201. 术语卡

术语卡记录的是阅读中出现过的陌生术语或概念，有时候是学术词汇，有时候是作者发明的黑话。如果不是作者首创的术语，建议找到最原始的论文或者资料，查询谁首先提出了这个术语，分辨哪些是作者真正意义上的原创贡献，哪些是作者改善前人研究，哪些是作者故意曲解他人术语。一旦养成这种习惯，你的独立思考能力就会增强。术语卡常见的信息结构是：「标题 + 定义 + 解释 + 例子」。试举如下：

参考以下的示例为`广播`写一张术语卡。

示例如下：

```
标题：什么是执行意图？

定义：它是一种制订计划的方式。认知心理学家彼得·戈尔维策将「我要减肥十斤」这种制订计划的方式称为「目标意图」，将使用「如果...那么...」（if...then...）的句式来制订计划的方式称为「执行意图」。

解释：执行意图通过在大脑中提前规划执行计划的时间、地点，从而更易引发行动。

例子：你可以将「我要多运动」改写为「如果到了每天傍晚 5 点，那么我就去操场跑步」。前者是目标意图，后者是执行意图。
```

#### 2.1 术语卡 —— 广播

定义：广播是 NumPy 中的一种机制，允许不同形状的数组在算术运算中自动扩展以匹配对方的形状，而无需实际复制数据。这个概念最早由 Travis Oliphant 在 2006 年开发 NumPy 时引入。

解释：广播遵循一定的规则，主要包括：

1、如果两个数组的维度数不同，形状较小的数组会在左侧补 1。

2、如果两个数组在某维度上的大小不匹配，且其中一个数组在该维度上的大小为 1，则这个数组会被沿着这个维度重复。

3、如果两个数组在对应维度上的大小不一致，且都不为 1，则会引发错误。

广播通过避免不必要的内存使用和显式循环，提高了数组操作的效率和代码的简洁性。

例子：考虑一个形状为（3,4）的二维数组和一个形状为（4,）的一维数组相加:

```python
arr_2d = np.array([[1, 2, 3, 4],
                   [5, 6, 7, 8],
                   [9, 10, 11, 12]])
arr_1d = np.array([10, 20, 30, 40])

result = arr_2d + arr_1d
\# 结果:
\# array([[11, 22, 33, 44],
\#        [15, 26, 37, 48],
\#        [19, 30, 41, 52]])
```

在这个例子中，一维数组 arr_1d 被广播到二维数组 arr_2d 的每一行，实现了高效的元素级加法运算。


---

不同大小的数组之间的运算叫做广播（broadcasting），将在附录 A 中对其进行详细讨论。

广播是 NumPy 中一个非常强大和方便的特性，它允许在执行算术运算时自动处理不同形状的数组。简单来说，广播使得较小的数组能够被「扩展」以匹配较大数组的形状，而无需实际复制数据。这样可以高效地进行不同形状数组之间的运算。

让我们通过几个例子来理解广播：

1、标量和数组的运算。

这是最简单的广播形式：

```python
arr = np.array([1, 2, 3, 4])
arr * 2
\# 结果: array([2, 4, 6, 8])
```

这里，标量值 2 被「广播」到数组的每个元素上。实际上，它等同于 `[2，2，2，2]` 与 `arr` 相乘，但 NumPy 并不需要创建这个临时数组。

2、一维数组和二维数组的运算。

```python
arr_2d = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])
arr_1d = np.array([10, 20, 30])

arr_2d + arr_1d
\# 结果:
\# array([[11, 22, 33],
\#        [14, 25, 36],
\#        [17, 28, 39]])
```

在这个例子中，一维数组 `arr_1d` 被广播到二维数组 `arr_2d` 的每一行。

3、广播的规则。

广播遵循以下规则：

- 如果两个数组的维度数不同，形状较小的数组会在左侧补 1。
- 如果两个数组的形状在任何维度上不匹配，且其中一个数组在该维度上的大小为 1，则这个数组会被沿着这个维度重复。
- 如果两个数组在对应维度上的大小不一致，且都不为 1，则会引发错误。

让我们通过一个更复杂的例子来说明这些规则：

```python
arr_3d = np.zeros((3, 4, 5))  # 3x4x5的三维数组
arr_2d = np.ones((4, 5))      # 4x5的二维数组

result = arr_3d + arr_2d
```

在这个例子中:

1. `arr_2d` 的形状是（4，5），它会被视为（1，4，5）以匹配 `arr_3d` 的维度。

2. 然后，(1，4，5）的形状会被广播到（3，4，5），即在第一个维度上重复 3 次。

3. 最后，两个（3，4，5）形状的数组相加。

广播的优点：

1. 内存效率：不需要复制数据来创建大的临时数组。

2. 计算效率：避免了显式循环，利用了底层优化的向量化操作。

3. 代码简洁：使代码更加简洁和易读。

需要注意的是，虽然广播非常强大，但也要小心使用。在某些情况下，它可能会导致意外的结果，特别是当处理多维数组时。始终确保你理解数组的形状和广播的规则，以避免潜在的错误。

总的来说，广播是 NumPy 中一个非常有用的功能，它简化了数组操作，提高了代码的效率和可读性。掌握广播可以让你更有效地使用 NumPy 进行数值计算和数据处理。

#### 2.1 术语卡 —— 结构化数据

When I say「data,」what am I referring to exactly? The primary focus is on structured data, a deliberately vague term that encompasses many different common forms of data, such as: 

1 Tabular or spreadsheet-like data in which each column may be a different type (string, numeric, date, or otherwise). This includes most kinds of data commonly stored in relational databases or tab- or comma-delimited text files.

2 Multidimensional arrays (matrices).

3 Multiple tables of data interrelated by key columns (what would be primary or foreign keys for a SQL user).

4 Evenly or unevenly spaced time series.

This is by no means a complete list. Even though it may not always be obvious, a large percentage of datasets can be transformed into a structured form that is more suitable for analysis and modeling. If not, it may be possible to extract features from a dataset into a structured form. As an example, a collection of news articles could be processed into a word frequency table, which could then be used to perform sentiment analysis. Most users of spreadsheet programs like Microsoft Excel, perhaps the most widely used data analysis tool in the world, will not be strangers to these kinds of data.

当书中出现「数据」时，究竟指的是什么呢？主要指的是结构化数据（structured data），这个故意含糊其辞的术语代指了所有通用格式的数据，例如：表格型数据，其中各列可能是不同的类型（字符串、数值、日期等）。比如保存在关系型数据库中或以制表符 / 逗号为分隔符的文本文件中的那些数据；多维数组（矩阵）；通过关键列（对于 SQL 用户而言，就是主键和外键）相互联系的多个表；间隔平均或不平均的时间序列。

这绝不是一个完整的列表。大部分数据集都能被转化为更加适合分析和建模的结构化形式，虽然有时这并不是很明显。如果不行的话，也可以将数据集的特征提取为某种结构化形式。例如，一组新闻文章可以被处理为一张词频表，而这张词频表就可以用于情感分析。

### 0301. 人名卡

请为约翰·R.安德森（John R. Anderson）写一份 500-1000 字的小传。要求包括他的姓名全称、生卒年份、教育背景、工作经历、主要身份、家庭网络、社会关系、人生重要节点以及重要成果，着重介绍其重要成果和著作，请参考维基百科的信息，并给出链接。

#### 3.1 人名卡 —— Wes Mckinney

[wesm (Wes McKinney - GitHub)](https://github.com/wesm)

Wes Mckinney，本书作者，pandas 的创建者。

Director of https://ursalabs.org/. Creator of Python pandas. Co-creator Apache Arrow. @apache Member and Apache Parquet PMC.

---

小传：

约翰·R. 安德森（John Robert Anderson，1947-）是一位杰出的认知心理学家和人工智能研究员，他的研究对于理解人类认知过程产生了深远影响。安德森的理论和模型已经被广泛应用于教育、人机交互和认知心理疗法等领域。

约翰·R. 安德森于 1947 年 1 月 27 日出生在加拿大温哥华。他在 1968 年毕业于加拿大不列颠哥伦比亚大学，获得数学和物理的学士学位。1972 年，他在斯坦福大学获得心理学博士学位。毕业后，他加入卡内基梅隆大学（CMU）任教，并在那里度过了他的大部分职业生涯。

安德森是 CMU 认知心理学和人工智能研究的核心人物，他的贡献主要集中在认知建模和智能教育系统的设计与研究。他开发的「ACT-R」认知建模框架，为认知心理学家研究人类复杂认知行为提供了一种强大的工具。他还是 CMU "LearnLab" 的联合创始人，这是一个研究人类学习过程的实验室，它使用科技手段，如智能教学系统，以提高学习效率。

他的主要著作有《人类认知的适应性性质》（The Adaptive Character of Thought, 1990）、《认知的规则》（Rules of the Mind, 1993）等，这些著作在认知心理学界产生了广泛的影响。

安德森在生活中是一位爱好广泛的人，他喜欢徒步、攀岩和滑雪等户外活动。他与妻子 Lynne Reder 共同生活，Lynne 也是一位在 CMU 任职的心理学教授。

在科研领域，安德森的贡献得到了广泛认可，他是美国国家科学院的院士，获得过多项重要奖项，包括美国心理学会的「杰出科学贡献奖」。

约翰·R. 安德森以其深入的研究和实践，为我们理解和改善人类认知提供了宝贵的资源。他的工作已经超越了学术领域的边界，影响了教育政策的制定和技术产品的设计。他的 ACT-R 理论以及研究人类学习的 LearnLab 为人们理解复杂认知过程以及改进教育方法提供了极为宝贵的资源。

至于他的人生重要节点，除了他的教育背景和职业生涯之外，他在 2004 年获得了杰出贡献奖，以表彰他在心理学领域的杰出贡献，尤其是在认知科学领域。他的贡献在诸多方面都得到了认可，这包括他对人工智能的研究，尤其是他对认知建模的创新工作。

总的来说，约翰·R. 安德森是一位杰出的认知心理学家和人工智能研究员，他的研究和理论在认知科学、教育和人机交互等领域产生了深远影响。尽管他已经离开了教室和实验室，但他的贡献和影响力仍然深远，他的工作仍然是当前认知科学研究的重要参考。

约翰·R. 安德森与冯特、佛洛依德、巴甫洛夫以及赫伯特·西蒙并列被评为人类历史上「50 位最伟大的心理学思想家」之一，他是最年轻的一位。

参考：[John Robert Anderson (psychologist) - Wikipedia](https://en.wikipedia.org/wiki/John_Robert_Anderson_(psychologist))

唯一编码：202305292311

打印备注：2023-05-29

### 0401. 金句卡

最后根据他写的非常震撼的话语——产生一张金句卡。

#### 4.1 金句卡 —— XXXX

### 0501. 基础卡

基础卡是最为基础的卡片，用于记录一些基础性事实、观点、故事等。基础卡常见的信息结构是：「标题 + 内容 + 评论」。「标题」指的是对卡片内容简明扼要的概括，类似卡片助记词，帮助你更好地记忆；「内容」指的是卡片正文，你可将阅读心得写成内容 + 评论或心得或想法或收获。基础卡举例如下：

{
标题：读《听听那冷雨》

内容：惊蛰一过，春寒加剧。先是料料峭峭，继而雨季开始，时而淋淋漓漓，时而渐渐沥沥，天潮潮地湿湿，即连在梦里，也似乎把伞撑着。而就凭一把伞，躲过一阵潇潇的冷雨，也躲不过整个雨季。连思想也都是潮润的。每天回家，曲折穿过金门街到厦门街迷宫式的长巷短巷，雨里风里，走入靠靠令人更想入非非。想这样子的台北凄凄切切完全是黑白片的味道，想整个中国整部中国的历史无非是一张黑白片子，片头到片尾，一直是这样下着雨的。

评论：余光中散文名篇《听听那冷雨》堪称白话文范文，将中文之美用到了极致，开篇「料料峭峭」「淋淋漓满」「渐渐沥沥」「凄凄切切」，又「天潮潮」「地湿湿」「潮润润」，又「惊蛰一过」「泰寒加剧」「雨季开始」。从头读到尾，毫不采板。
}

请结合以下内容提炼一张标题为{金属和非金属的判断指标}的基础卡。开始前请先重新阐述任务。

#### 5.1 基础卡 —— 创建变量即创建了一个指向等号右边对象的引用

变量和参数传递。在 Python 中对一个变量（或者变量名）赋值时，你就创建了一个指向等号右边对象的引用。考虑一个整数列表；假设将 a 赋值给一个新变量 b，在某些语言中，会是数据 [1, 2, 3] 被拷贝的过程。但在 Python 中，a 和 b 实际上是指向了相同的对象，即原来的 [1, 2, 3]（在图 2-7 中示范）。你可以通过向 a 中添加一个元素，然后检查 b 来证明；理解 Python 引用语义中复制数据的时机、方法和原因的机制，对于利用 Python 处理大数据集尤其重要。

赋值也被称为绑定，这是因为我们将一个变量名绑定到了一个对象上。已被赋值的变量名有时也会被称为被绑定变量。当你将对象作为参数传给一个函数时，指向原始对象的新的本地变量就会被创建而无须复制。如果你将一个新的对象绑定到一个函数内部的变量上，这种变更不会在上级范围中产生影响。因此，更换可变参数的内部值是可以做到的。

#### 5.1 基础卡 —— pandas 的开发背景

pandas provides high-level data structures and functions designed to make working with structured or tabular data fast, easy, and expressive. Since its emergence in 2010, it has helped enable Python to be a powerful and productive data analysis environment. The primary objects in pandas that will be used in this book are the DataFrame, a tabular, column-oriented data structure with both row and column labels, and the Series, a one-dimensional labeled array object.

pandas blends the high-performance, array-computing ideas of NumPy with the flexible data manipulation capabilities of spreadsheets and relational databases (such as SQL). It provides sophisticated indexing functionality to make it easy to reshape, slice and dice, perform aggregations, and select subsets of data. Since data manipulation, preparation, and cleaning is such an important skill in data analysis, pandas is one of the primary focuses of this book.

As a bit of background, I started building pandas in early 2008 during my tenure at AQR Capital Management, a quantitative investment management firm. At the time, I had a distinct set of requirements that were not well addressed by any single tool at my disposal:

1 Data structures with labeled axes supporting automatic or explicit data alignment — this prevents common errors resulting from misaligned data and working with differently indexed data coming from different sources.

2 Integrated time series functionality.

3 The same data structures handle both time series data and non–time series data.

4 Arithmetic operations and reductions that preserve metadata.

5 Flexible handling of missing data.

Merge and other relational operations found in popular databases (SQL-based, for example).

I wanted to be able to do all of these things in one place, preferably in a language well suited to general-purpose software development. Python was a good candidate language for this, but at that time there was not an integrated set of data structures and tools providing this functionality. As a result of having been built initially to solve finance and business analytics problems, pandas features especially deep time series functionality and tools well suited for working with time-indexed data generated by business processes.

For users of the R language for statistical computing, the DataFrame name will be familiar, as the object was named after the similar R data.frame object. Unlike Python, data frames are built into the R programming language and its standard library. As a result, many features found in pandas are typically either part of the R core implementation or provided by add-on packages.

The pandas name itself is derived from panel data, an econometrics term for multidimensional structured datasets, and a play on the phrase Python data analysis itself.

Wes Mckinney 觉得没有一个单一的工具可以满足其日常工作需求，然后自己发明了一个。我是在 2008 年初开始开发 pandas 的，那时我任职于 AQR Capital Management，一家量化投资管理公司，我有许多工作需求都不能用任何单一的工具解决：1）有标签轴的数据结构，支持自动或清晰的数据对齐。这可以防止由于数据不对齐，和处理来源不同的索引不同的数据，造成的错误；2）集成时间序列功能；3）相同的数据结构用于处理时间序列数据和非时间序列数据；4）保存元数据的算术运算和压缩；5）灵活处理缺失数据；6）合并和其它流行数据库（例如基于 SQL 的数据库）的关系操作。我想只用一种工具就实现所有功能，并使用通用软件开发语言。Python 是一个不错的候选语言，但是此时没有集成的数据结构和工具来实现。我一开始就是想把 pandas 设计为一款适用于金融和商业分析的工具，pandas 专注于深度时间序列功能和工具，适用于时间索引化的数据。

对于使用 R 语言进行统计计算的用户，肯定不会对 DataFrame 这个名字感到陌生，因为它源自于 R 的 data.frame 对象。但与 Python 不同，data frames 是构建于 R 和它的标准库。因此，pandas 的许多功能不属于 R 或它的扩展包。pandas 这个名字源于 panel data（面板数据，这是多维结构化数据集在计量经济学中的术语）以及 Python data analysis（Python 数据分析）。

## Preface

### Section 1. New for the Second Edition

The first edition of this book was published in 2012, during a time when open source data analysis libraries for Python (such as pandas) were very new and developing rapidly. In this updated and expanded second edition, I have overhauled the chapters to account both for incompatible changes and deprecations as well as new features that have occurred in the last five years. I’ve also added fresh content to introduce tools that either did not exist in 2012 or had not matured enough to make the first cut. Finally, I have tried to avoid writing about new or cutting-edge open source projects that may not have had a chance to mature. I would like readers of this edition to find that the content is still almost as relevant in 2020 or 2021 as it is in 2017.

The major updates in this second edition include:

1 All code, including the Python tutorial, updated for Python 3.6 (the first edition used Python 2.7).

2 Updated Python installation instructions for the Anaconda Python Distribution and other needed Python packages.

3 Updates for the latest versions of the pandas library in 2017.

4 A new chapter on some more advanced pandas tools, and some other usage tips.

5 A brief introduction to using statsmodels and scikit-learn.

I also reorganized a significant portion of the content from the first edition to make the book more accessible to newcomers.

### Section 2. Conventions Used in This Book

The following typographical conventions are used in this book:

Italic —— Indicates new terms, URLs, email addresses, filenames, and file extensions.

Constant width —— Used for program listings, as well as within paragraphs to refer to program elements such as variable or function names, databases, data types, environment variables, statements, and keywords.

Constant width bold —— Shows commands or other text that should be typed literally by the user.

Constant width italic —— Shows text that should be replaced with user-supplied values or by values determined by context.

Tip —— This element signifies a tip or suggestion.

Note —— This element signifies a general note.

Caution —— This element indicates a warning or caution.

### Section 3. Using Code Examples

You can find data files and related material for each chapter is available in this book’s GitHub repository at [wesm/pydata-book: Materials and IPython notebooks for "Python for Data Analysis" by Wes McKinney](https://github.com/wesm/pydata-book).

1『这本书的仓库很赞，直接看每章的 jupyter notebook 源码，已下载作为书籍源码附件。（2020-11-25）』

时过境迁，从本书英文版第 1 版 2012 年出版至今，已经过去了 6 年。这 6 年中，Python 的主流版本从 2.7 升级到了 3.6。无论是否情愿，大部分 Pythoner 都不得不学会适应新版本；而 pandas 则从 0.1.0 版本送代到如今的 0.22.0 版本。版本号的持续増加意味着新技术、新特性的不断丰富。

本书英文版的副书名是「Data Wrangling with Pandas, Numpy, and Ipython」，其中 Wrangling 是一个很难直译的词汇，它的原意是争执、争论，但在书中它描述的是将数据进行规整、处理的意思。希望读者读完本书后，可以使用好 pandas、Numpy 和 python 这些工具，更好地完成数据处理、分析的学习和工作。