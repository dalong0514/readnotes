# 0101. Preliminaries

## 1.1 What Is This Book About?

This book is concerned with the nuts and bolts of manipulating, processing, cleaning, and crunching data in Python. My goal is to offer a guide to the parts of the Python programming language and its data-oriented library ecosystem and tools that will equip you to become an effective data analyst. While「data analysis」is in the title of the book, the focus is specifically on Python programming, libraries, and tools as opposed to data analysis methodology. This is the Python programming you need for data analysis.

### What Kinds of Data?

When I say「data,」what am I referring to exactly? The primary focus is on structured data, a deliberately vague term that encompasses many different common forms of data, such as: 

1 Tabular or spreadsheet-like data in which each column may be a different type (string, numeric, date, or otherwise). This includes most kinds of data commonly stored in relational databases or tab- or comma-delimited text files.

2 Multidimensional arrays (matrices).

3 Multiple tables of data interrelated by key columns (what would be primary or foreign keys for a SQL user).

4 Evenly or unevenly spaced time series.

This is by no means a complete list. Even though it may not always be obvious, a large percentage of datasets can be transformed into a structured form that is more suitable for analysis and modeling. If not, it may be possible to extract features from a dataset into a structured form. As an example, a collection of news articles could be processed into a word frequency table, which could then be used to perform sentiment analysis. Most users of spreadsheet programs like Microsoft Excel, perhaps the most widely used data analysis tool in the world, will not be strangers to these kinds of data.

结构化数据的概念。大部分数据集都能被转化为更加适合分析和建模的结构化形式，虽然有时这并不是很明显。如果不行的话，也可以将数据集的特征提取为某种结构化形式。数据分析的步骤：获取数据；准备数据；转换数据；建模和计算；展示数据。

本书讲的是利用 Python 进行数据控制、处理、整理、分析等方面的具体细节和基本要点。我的目标是介绍 Python 编程和用于数据处理的库和工具环境，掌握这些，可以让你成为一个数据分析专家。虽然本书的标题是「数据分析」，重点确实 Python 编程、库，以及用于数据分析的工具。这就是数据分析要用到的 Python 编程。

当书中出现「数据」时，究竟指的是什么呢？主要指的是结构化数据（structured data），这个故意含糊其辞的术语代指了所有通用格式的数据，例如：表格型数据，其中各列可能是不同的类型（字符串、数值、日期等）。比如保存在关系型数据库中或以制表符 / 逗号为分隔符的文本文件中的那些数据；多维数组（矩阵）；通过关键列（对于 SQL 用户而言，就是主键和外键）相互联系的多个表；间隔平均或不平均的时间序列。

这绝不是一个完整的列表。大部分数据集都能被转化为更加适合分析和建模的结构化形式，虽然有时这并不是很明显。如果不行的话，也可以将数据集的特征提取为某种结构化形式。例如，一组新闻文章可以被处理为一张词频表，而这张词频表就可以用于情感分析。

2『大部分数据集都能被转化为更加适合分析和建模的结构化形式，做一张术语卡片。』

## 1.2 Why Python for Data Analysis?

For many people, the Python programming language has strong appeal. Since its first appearance in 1991, Python has become one of the most popular interpreted programming languages, along with Perl, Ruby, and others. Python and Ruby have become especially popular since 2005 or so for building websites using their numerous web frameworks, like Rails (Ruby) and Django (Python). Such languages are often called scripting languages, as they can be used to quickly write small programs, or scripts to automate other tasks. I don’t like the term「scripting language,」as it carries a connotation that they cannot be used for building serious software. Among interpreted languages, for various historical and cultural reasons, Python has developed a large and active scientific computing and data analysis community. In the last 10 years, Python has gone from a bleeding-edge or「at your own risk」scientific computing language to one of the most important languages for data science, machine learning, and general software development in academia and industry.

For data analysis and interactive computing and data visualization, Python will inevitably draw comparisons with other open source and commercial programming languages and tools in wide use, such as R, MATLAB, SAS, Stata, and others. In recent years, Python’s improved support for libraries (such as pandas and scikit-learn) has made it a popular choice for data analysis tasks. Combined with Python’s overall strength for general-purpose software engineering, it is an excellent option as a primary language for building data applications.

### 1.2.1 Python as Glue

Part of Python’s success in scientific computing is the ease of integrating C, C++, and FORTRAN code. Most modern computing environments share a similar set of legacy FORTRAN and C libraries for doing linear algebra, optimization, integration, fast Fourier transforms, and other such algorithms. The same story has held true for many companies and national labs that have used Python to glue together decades’ worth of legacy software.

Many programs consist of small portions of code where most of the time is spent, with large amounts of「glue code」that doesn’t run often. In many cases, the execution time of the glue code is insignificant; effort is most fruitfully invested in optimizing the computational bottlenecks, sometimes by moving the code to a lower-level language like C.

### 1.2.2 Solving the「Two-Language」Problem

In many organizations, it is common to research, prototype, and test new ideas using a more specialized computing language like SAS or R and then later port those ideas to be part of a larger production system written in, say, Java, C#, or C++. What people are increasingly finding is that Python is a suitable language not only for doing research and prototyping but also for building the production systems. Why maintain two development environments when one will suffice? I believe that more and more companies will go down this path, as there are often significant organizational benefits to having both researchers and software engineers using the same set of programming tools.

### 1.2.3 Why Not Python?

While Python is an excellent environment for building many kinds of analytical applications and general-purpose systems, there are a number of uses for which Python may be less suitable.

As Python is an interpreted programming language, in general most Python code will run substantially slower than code written in a compiled language like Java or C++. As programmer time is often more valuable than CPU time, many are happy to make this trade-off. However, in an application with very low latency or demanding resource utilization requirements (e.g., a high-frequency trading system), the time spent programming in a lower-level (but also lower-productivity) language like C++ to achieve the maximum possible performance might be time well spent.

Python can be a challenging language for building highly concurrent, multithreaded applications, particularly applications with many CPU-bound threads. The reason for this is that it has what is known as the global interpreter lock (GIL), a mechanism that prevents the interpreter from executing more than one Python instruction at a time. The technical reasons for why the GIL exists are beyond the scope of this book. While it is true that in many big data processing applications, a cluster of computers may be required to process a dataset in a reasonable amount of time, there are still situations where a single-process, multithreaded system is desirable.

This is not to say that Python cannot execute truly multithreaded, parallel code. Python C extensions that use native multithreading (in C or C++) can run code in parallel without being impacted by the GIL, so long as they do not need to regularly interact with Python objects.

为什么要使用 Python 进行数据分析。许许多多的人（包括我自己）都很容易爱上 Python 这门语言。自从 1991 年诞生以来，Python 现在已经成为最受欢迎的动态编程语言之一，其他还有 Perl、Ruby 等。由于拥有大量的 Web 框架（比如 Rails（Ruby）和 Django（Python）），自从 2005 年，非常流行使用 Python 和 Ruby 进行网站建设工作。这些语言常被称作脚本（scripting）语言，因为它们可以用于编写简短而粗糙的小程序（也就是脚本）。我个人并不喜欢「脚本语言」这个术语，因为它好像在说这些语言无法用于构建严谨的软件。在众多解释型语言中，由于各种历史和文化的原因，Python 发展出了一个巨大而活跃的科学计算（scientific computing）社区。在过去的 10 年，Python 从一个边缘或「自担风险」的科学计算语言，成为了数据科学、机器学习、学界和工业界软件开发最重要的语言之一。

在数据分析、交互式计算以及数据可视化方面，Python 将不可避免地与其他开源和商业的领域特定编程语言 / 工具进行对比，如 R、MATLAB、SAS、Stata 等。近年来，由于 Python 的库（例如 pandas 和 scikit-learn）不断改良，使其成为数据分析任务的一个优选方案。结合其在通用编程方面的强大实力，我们完全可以只使用 Python 这一种语言构建以数据为中心的应用。

Python 作为胶水语言。Python 能变为成功的科学计算工具的部分原因是，它能够轻松地集成 C、C++ 以及 Fortran 代码。大部分现代计算环境都利用了一些 Fortran 和 C 库来实现线性代数、优选、积分、快速傅里叶变换以及其他诸如此类的算法。许多企业和国家实验室也利用 Python 来「粘合」那些已经用了多年的遗留软件系统。大多数软件都是由两部分代码组成的：少量需要占用大部分执行时间的代码，以及大量不经常执行的「胶水代码」。大部分情况下，胶水代码的执行时间是微不足道的。开发人员的精力几乎都是花在优化计算瓶颈上面，有时更是直接转用更低级的语言（比如 C）。

解决「两种语言」问题。很多组织通常都会用一种类似于领域特定的计算语言（如 SAS 和 R）对新的想法进行研究、原型构建和测试，然后再将这些想法移植到某个更大的生产系统中去（可能是用 Java、C# 或 C++ 编写的）。人们逐渐意识到，Python 不仅适用于研究和原型构建，同时也适用于构建生产系统。为什么一种语言就够了，却要使用两个语言的开发环境呢？我相信越来越多的企业也会这样看，因为研究人员和工程技术人员使用同一种编程工具将会给企业带来非常显著的组织效益。

为什么不选 Python。虽然 Python 非常适合构建分析应用以及通用系统，但它对不少应用场景适用性较差。由于 Python 是一种解释型编程语言，因此大部分 Python 代码都要比用编译型语言（比如 Java 和 C++）编写的代码运行慢得多。由于程序员的时间通常都比 CPU 时间值钱，因此许多人也愿意在这里做一些权衡。但是，在那些要求延迟非常小或高资源利用率的应用中（例如高频交易系统），耗费时间使用诸如 C++ 这样更低级、更低生产率的语言进行编程也是值得的。

对于高并发、多线程的应用程序而言（尤其是拥有许多计算密集型线程的应用程序），Python 并不是一种理想的编程语言。这是因为 Python 有一个叫做全局解释器锁（Global Interpreter Lock，GIL）的组件，这是一种防止解释器同时执行多条 Python 字节码指令的机制。有关「为什么会存在 GIL」的技术性原因超出了本书的范围。虽然很多大数据处理应用程序为了能在较短的时间内完成数据集的处理工作都需要运行在计算机集群上，但是仍然有一些情况需要用单进程多线程系统来解决。这并不是说 Python 不能执行真正的多线程并行代码。例如，Python 的 C 插件使用原生的 C 或 C++ 的多线程，可以并行运行而不被 GIL 影响，只要它们不频繁地与 Python 对象交互。

## 1.3 Essential Python Libraries

For those who are less familiar with the Python data ecosystem and the libraries used throughout the book, I will give a brief overview of some of them.

### 1.3.1 NumPy

NumPy, short for Numerical Python, has long been a cornerstone of numerical computing in Python. It provides the data structures, algorithms, and library glue needed for most scientific applications involving numerical data in Python. NumPy contains, among other things:

1 A fast and efficient multidimensional array object ndarray.

2 Functions for performing element-wise computations with arrays or mathematical operations between arrays.

3 Tools for reading and writing array-based datasets to disk.

4 Linear algebra operations, Fourier transform, and random number generation.

5 A mature C API to enable Python extensions and native C or C++ code to access NumPy’s data structures and computational facilities.

Beyond the fast array-processing capabilities that NumPy adds to Python, one of its primary uses in data analysis is as a container for data to be passed between algorithms and libraries. For numerical data, NumPy arrays are more efficient for storing and manipulating data than the other built-in Python data structures. Also, libraries written in a lower-level language, such as C or Fortran, can operate on the data stored in a NumPy array without copying data into some other memory representation. Thus, many numerical computing tools for Python either assume NumPy arrays as a primary data structure or else target seamless interoperability with NumPy.

NumPy（Numerical Python 的简称）是 Python 科学计算的基础包。本书大部分内容都基于 NumPy 以及构建于其上的库。它提供了以下功能（不限于此）：快速高效的多维数组对象 ndarray；用于对数组执行元素级计算以及直接对数组执行数学运算的函数；用于读写硬盘上基于数组的数据集的工具；线性代数运算、傅里叶变换，以及随机数生成；成熟的 C API，用于 Python 插件和原生 C、C++、Fortran 代码访问 NumPy 的数据结构和计算工具。

除了为 Python 提供快速的数组处理能力，NumPy 在数据分析方面还有另外一个主要作用，即作为在算法和库之间传递数据的容器。对于数值型数据，NumPy 数组在存储和处理数据时要比内置的 Python 数据结构高效得多。此外，由低级语言（比如 C 和 Fortran）编写的库可以直接操作 NumPy 数组中的数据，无需进行任何数据复制工作。因此，许多 Python 的数值计算工具要么使用 NumPy 数组作为主要的数据结构，要么可以与 NumPy 进行无缝交互操作。

### 1.3.2 pandas

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

pandas 提供了快速便捷处理结构化数据的大量数据结构和函数。自从 2010 年出现以来，它助使 Python 成为强大而高效的数据分析环境。本书用得最多的 pandas 对象是 DataFrame，它是一个面向列（column-oriented）的二维表结构，另一个是 Series，一个一维的标签化数组对象。pandas 兼具 NumPy 高性能的数组计算功能以及电子表格和关系型数据库（如 SQL）灵活的数据处理功能。它提供了复杂精细的索引功能，以便更为便捷地完成重塑、切片和切块、聚合以及选取数据子集等操作。因为数据操作、准备、清洗是数据分析最重要的技能，pandas 是本书的重点。

作为一点背景，我是在 2008 年初开始开发 pandas 的，那时我任职于 AQR Capital Management，一家量化投资管理公司，我有许多工作需求都不能用任何单一的工具解决：有标签轴的数据结构，支持自动或清晰的数据对齐。这可以防止由于数据不对齐，和处理来源不同的索引不同的数据，造成的错误；集成时间序列功能；相同的数据结构用于处理时间序列数据和非时间序列数据；保存元数据的算术运算和压缩；灵活处理缺失数据；合并和其它流行数据库（例如基于 SQL 的数据库）的关系操作。

我想只用一种工具就实现所有功能，并使用通用软件开发语言。Python 是一个不错的候选语言，但是此时没有集成的数据结构和工具来实现。我一开始就是想把 pandas 设计为一款适用于金融和商业分析的工具，pandas 专注于深度时间序列功能和工具，适用于时间索引化的数据。

对于使用 R 语言进行统计计算的用户，肯定不会对 DataFrame 这个名字感到陌生，因为它源自于 R 的 data.frame 对象。但与 Python 不同，data frames 是构建于 R 和它的标准库。因此，pandas 的许多功能不属于 R 或它的扩展包。pandas 这个名字源于 panel data（面板数据，这是多维结构化数据集在计量经济学中的术语）以及 Python data analysis（Python 数据分析）。

### 1.3.3 matplotlib

matplotlib is the most popular Python library for producing plots and other two-dimensional data visualizations. It was originally created by John D. Hunter and is now maintained by a large team of developers. It is designed for creating plots suitable for publication. While there are other visualization libraries available to Python programmers, matplotlib is the most widely used and as such has generally good integration with the rest of the ecosystem. I think it is a safe choice as a default visualization tool.

matplotlib 是最流行的用于绘制图表和其它二维数据可视化的 Python 库。它最初由 John D.Hunter（JDH）创建，目前由一个庞大的开发人员团队维护。它非常适合创建出版物上用的图表。虽然还有其它的 Python 可视化库，matplotlib 却是使用最广泛的，并且它和其它生态工具配合也非常完美。我认为，可以使用它作为默认的可视化工具。

IPython 项目起初是 Fernando Pérez 在 2001 年的一个用以加强和 Python 交互的子项目。在随后的 16 年中，它成为了 Python 数据栈最重要的工具之一。虽然 IPython 本身没有提供计算和数据分析的工具，它却可以大大提高交互式计算和软件开发的生产率。IPython 鼓励「执行 - 探索」的工作流，区别于其它编程软件的「编辑 - 编译 - 运行」的工作流。它还可以方便地访问系统的 shell 和文件系统。因为大部分的数据分析代码包括探索、试错和重复，IPython 可以使工作更快。

### 1.3.4 IPython and Jupyter

The IPython project began in 2001 as Fernando Pérez’s side project to make a better interactive Python interpreter. In the subsequent 16 years it has become one of the most important tools in the modern Python data stack. While it does not provide any computational or data analytical tools by itself, IPython is designed from the ground up to maximize your productivity in both interactive computing and software development. It encourages an execute-explore workflow instead of the typical edit-compile-run workflow of many other programming languages. It also provides easy access to your operating system’s shell and filesystem. Since much of data analysis coding involves exploration, trial and error, and iteration, IPython can help you get the job done faster.

In 2014, Fernando and the IPython team announced the Jupyter project, a broader initiative to design language-agnostic interactive computing tools. The IPython web notebook became the Jupyter notebook, with support now for over 40 programming languages. The IPython system can now be used as a kernel (a programming language mode) for using Python with Jupyter.

IPython itself has become a component of the much broader Jupyter open source project, which provides a productive environment for interactive and exploratory computing. Its oldest and simplest「mode」is as an enhanced Python shell designed to accelerate the writing, testing, and debugging of Python code. You can also use the IPython system through the Jupyter Notebook, an interactive web-based code「notebook」offering support for dozens of programming languages. The IPython shell and Jupyter notebooks are especially useful for data exploration and visualization.

The Jupyter notebook system also allows you to author content in Markdown and HTML, providing you a means to create rich documents with code and text. Other programming languages have also implemented kernels for Jupyter to enable you to use languages other than Python in Jupyter.

For me personally, IPython is usually involved with the majority of my Python work, including running, debugging, and testing code. In the accompanying book materials, you will find Jupyter notebooks containing all the code examples from each chapter.

2014 年，Fernando 和 IPython 团队宣布了 Jupyter 项目，一个更宽泛的多语言交互计算工具的计划。IPython web notebook 变成了 Jupyter notebook，现在支持 40 种编程语言。IPython 现在可以作为 Jupyter 使用 Python 的内核（一种编程语言模式）。

IPython 变成了 Jupyter 庞大开源项目（一个交互和探索式计算的高效环境）中的一个组件。它最老也是最简单的模式，现在是一个用于编写、测试、调试 Python 代码的强化 shell。你还可以使用通过 Jupyter Notebook，一个支持多种语言的交互式网络代码「笔记本」，来使用 IPython。IPython shell 和 Jupyter notebooks 特别适合进行数据探索和可视化。

Jupyter notebooks 还可以编写 Markdown 和 HTML 内容，提供了一种创建代码和文本的富文本方法。其它编程语言也在 Jupyter 中植入了内核，好让在 Jupyter 中可以使用 Python 另外的语言。对我个人而言，我的大部分 Python 都要用到 IPython，包括运行、调试和测试代码。在本书的 GitHub 页面，你可以找到包含各章节所有代码实例的 Jupyter notebooks。

### 1.3.5 SciPy

SciPy is a collection of packages addressing a number of different standard problem domains in scientific computing. Here is a sampling of the packages included:

scipy.integrate ——Numerical integration routines and differential equation solvers.

scipy.linalg —— Linear algebra routines and matrix decompositions extending beyond those provided in numpy.linalg.

scipy.optimize —— Function optimizers (minimizers) and root finding algorithms.

scipy.signal —— Signal processing tools.

scipy.sparse —— Sparse matrices and sparse linear system solvers.

scipy.special —— Wrapper around SPECFUN, a Fortran library implementing many common mathematical functions, such as the gamma function.

scipy.stats —— Standard continuous and discrete probability distributions (density functions, samplers, continuous distribution functions), various statistical tests, and more descriptive statistics.

Together NumPy and SciPy form a reasonably complete and mature computational foundation for many traditional scientific computing applications.

SciPy 是一组专门解决科学计算中各种标准问题域的包的集合，主要包括下面这些包：1）scipy.integrate，数值积分例程和微分方程求解器；2）scipy.linalg，扩展了由 numpy.linalg 提供的线性代数例程和矩阵分解功能；3）scipy.optimize，函数优化器（最小化器）以及根查找算法；4）scipy.signal，信号处理工具；5）scipy.sparse，稀疏矩阵和稀疏线性系统求解器；6）scipy.special，SPECFUN（这是一个实现了许多常用数学函数（如伽玛函数）的 Fortran 库）的包装器；7）scipy.stats，标准连续和离散概率分布（如密度函数、采样器、连续分布函数等）、各种统计检验方法，以及更好的描述统计法。NumPy 和 SciPy 结合使用，便形成了一个相当完备和成熟的计算平台，可以处理多种传统的科学计算问题。

### scikit-learn

Since the project’s inception in 2010, scikit-learn has become the premier general-purpose machine learning toolkit for Python programmers. In just seven years, it has had over 1,500 contributors from around the world. It includes submodules for such models as:

1 Classification: SVM, nearest neighbors, random forest, logistic regression, etc.

2 Regression: Lasso, ridge regression, etc.

3 Clustering: k-means, spectral clustering, etc.

4 Dimensionality reduction: PCA, feature selection, matrix factorization, etc.

5 Model selection: Grid search, cross-validation, metrics.

6 Preprocessing: Feature extraction, normalization.

Along with pandas, statsmodels, and IPython, scikit-learn has been critical for enabling Python to be a productive data science programming language. While I won’t be able to include a comprehensive guide to scikit-learn in this book, I will give a brief introduction to some of its models and how to use them with the other tools presented in the book.

2010 年诞生以来，scikit-learn 成为了 Python 的通用机器学习工具包。仅仅七年，就汇聚了全世界超过 1500 名贡献者。它的子模块包括：分类，SVM、近邻、随机森林、逻辑回归等等；回归，Lasso、岭回归等等；聚类，k - 均值、谱聚类等等；降维，PCA、特征选择、矩阵分解等等；选型，网格搜索、交叉验证、度量；预处理，特征提取、标准化。与 pandas、statsmodels 和 IPython 一起，scikit-learn 对于 Python 成为高效数据科学编程语言起到了关键作用。虽然本书不会详细讲解 scikit-learn，我会简要介绍它的一些模型，以及用其它工具如何使用这些模型。

### statsmodels

statsmodels is a statistical analysis package that was seeded by work from Stanford University statistics professor Jonathan Taylor, who implemented a number of regression analysis models popular in the R programming language. Skipper Seabold and Josef Perktold formally created the new statsmodels project in 2010 and since then have grown the project to a critical mass of engaged users and contributors. Nathaniel Smith developed the Patsy project, which provides a formula or model specification framework for statsmodels inspired by R’s formula system.

Compared with scikit-learn, statsmodels contains algorithms for classical (primarily frequentist) statistics and econometrics. This includes such submodules as:

1 Regression models: Linear regression, generalized linear models, robust linear models, linear mixed effects models, etc.

2 Analysis of variance (ANOVA)

3 Time series analysis: AR, ARMA, ARIMA, VAR, and other models

4 Nonparametric methods: Kernel density estimation, kernel regression

5 Visualization of statistical model results

statsmodels is more focused on statistical inference, providing uncertainty estimates and p-values for parameters. scikit-learn, by contrast, is more prediction-focused. As with scikit-learn, I will give a brief introduction to statsmodels and how to use it with NumPy and pandas.

statsmodels 是一个统计分析包，起源于斯坦福大学统计学教授 Jonathan Taylor，他设计了多种流行于 R 语言的回归分析模型。Skipper Seabold 和 Josef Perktold 在 2010 年正式创建了 statsmodels 项目，随后汇聚了大量的使用者和贡献者。受到 R 的公式系统的启发，Nathaniel Smith 发展出了 Patsy 项目，它提供了 statsmodels 的公式或模型的规范框架。与 scikit-learn 比较，statsmodels 包含经典统计学和经济计量学的算法。包括如下子模块：回归模型，线性回归，广义线性模型，健壮线性模型，线性混合效应模型等等；方差分析（ANOVA）；时间序列分析，AR，ARMA，ARIMA，VAR 和其它模型；非参数方法，核密度估计，核回归；统计模型结果可视化。statsmodels 更关注与统计推断，提供不确定估计和参数 p - 值。相反的，scikit-learn 注重预测。同 scikit-learn 一样，我也只是简要介绍 statsmodels，以及如何用 NumPy 和 pandas 使用它。

## 1.4 Installation and Setup

Since everyone uses Python for different applications, there is no single solution for setting up Python and required add-on packages. Many readers will not have a complete Python development environment suitable for following along with this book, so here I will give detailed instructions to get set up on each operating system. I recommend using the free Anaconda distribution. At the time of this writing, Anaconda is offered in both Python 2.7 and 3.6 forms, though this might change at some point in the future. This book uses Python 3.6, and I encourage you to use Python 3.6 or higher.

### 1.4.1 Windows

To get started on Windows, download the Anaconda installer. I recommend following the installation instructions for Windows available on the Anaconda download page, which may have changed between the time this book was published and when you are reading this.

Now, let’s verify that things are configured correctly. To open the Command Prompt application (also known as cmd.exe), right-click the Start menu and select Command Prompt. Try starting the Python interpreter by typing python. You should see a message that matches the version of Anaconda you installed:

```
C:\Users\wesm>python 
Python 3.5.2 |Anaconda 4.1.1 (64-bit)| (default, Jul 5 2016, 11:41:13) 
[MSC v.1900 64 bit (AMD64)] on win32 >>>
```

To exit the shell, press Ctrl-D (on Linux or macOS), Ctrl-Z (on Windows), or type the command exit() and press Enter.

### 1.4.2 Apple (OS X, macOS)

Download the OS X Anaconda installer, which should be named something like `Anaconda3-4.1.0-MacOSX-x86_64.pkg`. Double-click the .pkg file to run the installer. When the installer runs, it automatically appends the Anaconda executable path to your .bash_profile file. This is located at `/Users/$USER/.bash_profile`.

To verify everything is working, try launching IPython in the system shell (open the Terminal application to get a command prompt):

```
$ ipython
```

To exit the shell, press Ctrl-D or type exit() and press Enter.

### 1.4.3 GNU/Linux

Linux details will vary a bit depending on your Linux flavor, but here I give details for such distributions as Debian, Ubuntu, CentOS, and Fedora. Setup is similar to OS X with the exception of how Anaconda is installed. The installer is a shell script that must be executed in the terminal. Depending on whether you have a 32-bit or 64-bit system, you will either need to install the x86 (32-bit) or x86_64 (64-bit) installer. You will then have a file named something similar to Anaconda3-4.1.0-Linux-x86_64.sh. To install it, execute this script with bash:

```
$ bash Anaconda3-4.1.0-Linux-x86_64.sh
```

Note: Some Linux distributions have versions of all the required Python packages in their package managers and can be installed using a tool like apt. The setup described here uses Anaconda, as it’s both easily reproducible across distributions and simpler to upgrade packages to their latest versions.

After accepting the license, you will be presented with a choice of where to put the Anaconda files. I recommend installing the files in the default location in your home directory — for example, `/home/$USER/anaconda` (with your username, naturally).

The Anaconda installer may ask if you wish to prepend its bin/ directory to your `$PATH` variable. If you have any problems after installation, you can do this yourself by modifying your .bashrc (or .zshrc, if you are using the zsh shell) with something akin to:

```
export PATH=/home/$USER/anaconda/bin:$PATH
```

After doing this you can either start a new terminal process or execute your .bashrc again with source ~/.bashrc.

### 1.4.4 Installing or Updating Python Packages

At some point while reading, you may wish to install additional Python packages that are not included in the Anaconda distribution. In general, these can be installed with the following command:

```
conda install package_name
```

If this does not work, you may also be able to install the package using the pip package management tool:

```
pip install package_name
```

You can update packages by using the conda update command:

```
conda update package_name
```

pip also supports upgrades using the --upgrade flag:

```
pip install --upgrade package_name
```

You will have several opportunities to try out these commands throughout the book.

Caution: While you can use both conda and pip to install packages, you should not attempt to update conda packages with pip, as doing so can lead to environment problems. When using Anaconda or Miniconda, it’s best to first try updating with conda.

### 1.4.5 Python 2 and Python 3

The first version of the Python 3.x line of interpreters was released at the end of 2008. It included a number of changes that made some previously written Python 2.x code incompatible. Because 17 years had passed since the very first release of Python in 1991, creating a「breaking」release of Python 3 was viewed to be for the greater good given the lessons learned during that time.

In 2012, much of the scientific and data analysis community was still using Python 2.x because many packages had not been made fully Python 3 compatible. Thus, the first edition of this book used Python 2.7. Now, users are free to choose between Python 2.x and 3.x and in general have full library support with either flavor.

However, Python 2.x will reach its development end of life in 2020 (including critical security patches), and so it is no longer a good idea to start new projects in Python 2.7. Therefore, this book uses Python 3.6, a widely deployed, well-supported stable release. We have begun to call Python 2.x「Legacy Python」and Python 3.x simply「Python.」I encourage you to do the same.

This book uses Python 3.6 as its basis. Your version of Python may be newer than 3.6, but the code examples should be forward compatible. Some code examples may work differently or not at all in Python 2.7.

### 1.4.6 Integrated Development Environments (IDEs) and Text Editors

When asked about my standard development environment, I almost always say「IPython plus a text editor.」I typically write a program and iteratively test and debug each piece of it in IPython or Jupyter notebooks. It is also useful to be able to play around with data interactively and visually verify that a particular set of data manipulations is doing the right thing. Libraries like pandas and NumPy are designed to be easy to use in the shell.

When building software, however, some users may prefer to use a more richly featured IDE rather than a comparatively primitive text editor like Emacs or Vim. Here are some that you can explore:

1 PyDev (free), an IDE built on the Eclipse platform

2 PyCharm from JetBrains (subscription-based for commercial users, free for open source developers)

3 Python Tools for Visual Studio (for Windows users)

4 Spyder (free), an IDE currently shipped with Anaconda

5 Komodo IDE (commercial)

Due to the popularity of Python, most text editors, like Atom and Sublime Text 2, have excellent Python support.

注意：当你使用 conda 和 pip 二者安装包时，千万不要用 pip 升级 conda 的包，这样会导致环境发生问题。当使用 Anaconda 或 Miniconda 时，最好首先使用 conda 进行升级。

1『 conda list 后，发现里面的包全跟 pip list 里的包混了，看不出来哪些事用 conda 安装的。想到的折中的办法，用 conda search 去筛选。』

## 1.5 Community and Conferences

Outside of an internet search, the various scientific and data-related Python mailing lists are generally helpful and responsive to questions. Some to take a look at include:

1 pydata: A Google Group list for questions related to Python for data analysis and pandas.

2 pystatsmodels: For statsmodels or pandas-related questions.

3 Mailing list for scikit-learn (scikit-learn@python.org) and machine learning in Python, generally.

4 numpy-discussion: For NumPy-related questions.

5 scipy-user: For general SciPy or scientific Python questions.

I deliberately did not post URLs for these in case they change. They can be easily located via an internet search. Each year many conferences are held all over the world for Python programmers. If you would like to connect with other Python programmers who share your interests, I encourage you to explore attending one, if possible. Many conferences have financial support available for those who cannot afford admission or travel to the conference. Here are some to consider:

1 PyCon and EuroPython: The two main general Python conferences in North America and Europe, respectively

2 SciPy and EuroSciPy: Scientific-computing-oriented conferences in North America and Europe, respectively

3 PyData: A worldwide series of regional conferences targeted at data science and data analysis use cases

4 International and regional PyCon conferences (see http://pycon.org for a complete listing)

除了在网上搜索，各式各样的科学和数据相关的 Python 邮件列表是非常有帮助的，很容易获得回答。包括：1）pydata，一个 Google 群组列表，用以回答 Python 数据分析和 pandas 的问题；2）pystatsmodels，statsmodels 或 pandas 相关的问题；3）scikit-learn 和 Python 机器学习邮件列表，scikit-learn@python.org；4）numpy-discussion，和 NumPy 相关的问题；5）scipy-user，SciPy 和科学计算的问题。因为这些邮件列表的 URLs 可以很容易搜索到，但因为可能发生变化，所以没有给出。

每年，世界各地会举办许多 Python 开发者大会。如果你想结识其他有相同兴趣的人，如果可能的话，我建议你去参加一个。许多会议会对无力支付入场费和差旅费的人提供财力帮助。下面是一些会议：1）PyCon 和 EuroPython，北美和欧洲的两大 Python 会议；2）SciPy 和 EuroSciPy，北美和欧洲两大面向科学计算的会议；3）PyData，世界范围内，一些列的地区性会议，专注数据科学和数据分析；4）国际和地区的 PyCon 会议（http://pycon.org 有完整列表） 。

## 1.6 Navigating This Book

If you have never programmed in Python before, you will want to spend some time in Chapters 2 and 3, where I have placed a condensed tutorial on Python language features and the IPython shell and Jupyter notebooks. These things are prerequisite knowledge for the remainder of the book. If you have Python experience already, you may instead choose to skim or skip these chapters.

Next, I give a short introduction to the key features of NumPy, leaving more advanced NumPy use for Appendix A. Then, I introduce pandas and devote the rest of the book to data analysis topics applying pandas, NumPy, and matplotlib (for visualization). I have structured the material in the most incremental way possible, though there is occasionally some minor cross-over between chapters, with a few isolated cases where concepts are used that haven’t necessarily been introduced yet.

While readers may have many different end goals for their work, the tasks required generally fall into a number of different broad groups:

Interacting with the outside world —— Reading and writing with a variety of file formats and data stores.

Preparation —— Cleaning, munging, combining, normalizing, reshaping, slicing and dicing, and transforming data for analysis.

Transformation —— Applying mathematical and statistical operations to groups of datasets to derive new datasets (e.g., aggregating a large table by group variables).

Modeling and computation —— Connecting your data to statistical models, machine learning algorithms, or other computational tools.

Presentation —— Creating interactive or static graphical visualizations or textual summaries.

接下来，简单地介绍了 NumPy 的关键特性，附录 A 中是更高级的 NumPy 功能。然后，我介绍了 pandas，本书剩余的内容全部是使用 pandas、NumPy 和 matplotlib 处理数据分析的问题。我已经尽量让全书的结构循序渐进，但偶尔会有章节之间的交叉，有时用到的概念还没有介绍过。

尽管读者各自的工作任务不同，大体可以分为几类：1）与外部世界交互，阅读编写多种文件格式和数据商店；2）数据准备，清洗、修改、结合、标准化、重塑、切片、切割、转换数据，以进行分析；3）转换数据，对旧的数据集进行数学和统计操作，生成新的数据集（例如，通过各组变量聚类成大的表）；4）建模和计算，将数据绑定统计模型、机器学习算法、或其他计算工具；5）展示，创建交互式和静态的图表可视化和文本总结。

1『数据分析的一般步骤：获取数据；准备数据；转换数据；建模和计算；展示数据。』

### 1.6.1 Code Examples

Most of the code examples in the book are shown with input and output as it would appear executed in the IPython shell or in Jupyter notebooks:

```
In [5]: CODE EXAMPLE 
Out[5]: OUTPUT
```

When you see a code example like this, the intent is for you to type in the example code in the In block in your coding environment and execute it by pressing the Enter key (or Shift-Enter in Jupyter). You should see output similar to what is shown in the Out block.

### 1.6.2 Data for Examples

Datasets for the examples in each chapter are hosted in a GitHub repository. You can download this data either by using the Git version control system on the command line or by downloading a zip file of the repository from the website. If you run into problems, navigate to my website for up-to-date instructions about obtaining the book materials.

I have made every effort to ensure that it contains everything necessary to reproduce the examples, but I may have made some mistakes or omissions. If so, please send me an email: book@wesmckinney.com. The best way to report errors in the book is on the errata page on the O’Reilly website.

### 1.6.3 Import Conventions

The Python community has adopted a number of naming conventions for commonly used modules:

```py
import numpy as np 
import matplotlib.pyplot as plt 
import pandas as pd 
import seaborn as sns
 import statsmodels as sm
```

This means that when you see np.arange, this is a reference to the arange function in NumPy. This is done because it’s considered bad practice in Python software development to import everything (from numpy import *) from a large package like NumPy.

也就是说，当你看到 np.arange 时，就应该想到它引用的是 NumPy 中的 arange 函数。这样做的原因是：在 Python 软件开发过程中，不建议直接引入类似 NumPy 这种大型库的全部内容（from numpy import *）。

### 1.6.4 Jargon

I’ll use some terms common both to programming and data science that you may not be familiar with. Thus, here are some brief definitions:

Munge/munging/wrangling —— Describes the overall process of manipulating unstructured and/or messy data into a structured or clean form. The word has snuck its way into the jargon of many modern-day data hackers.「Munge」rhymes with「grunge.」

Pseudocode —— A description of an algorithm or process that takes a code-like form while likely not being actual valid source code.

Syntactic sugar —— Programming syntax that does not add new features, but makes something more convenient or easier to type.

一些有关编程和数据科学方面的常用术语：1）数据规整（Munge/Munging/Wrangling），指的是将非结构化和（或）散乱数据处理为结构化或整洁形式的整个过程。这几个词已经悄悄成为当今数据黑客们的行话了。Munge 这个词跟 Lunge 押韵；2）伪码（Pseudocode），算法或过程的「代码式」描述，而这些代码本身并不是实际有效的源代码；3）语法糖（Syntactic sugar），这是一种编程语法，它并不会带来新的特性，但却能使代码更易读、更易写。