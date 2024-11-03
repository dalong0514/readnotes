## 记忆时间

## 目录

7、用 pandas 进行数据的清洗。处理缺失数据，删除或者填充的方法；数据转换，移除重复数据、利用函数或映射进行数据转换、替换值、重命名轴索引、离散化和分箱、检测和过滤异常值、排列和随机采样、计算指标/虚拟变量；字符串操作，大部分文本运算都直接做成了字符串对象的内置方法，对于更为复杂的模式匹配和文本操作，则可能需要用到正则表达式，pandas 对此进行了加强，它使你能够对整组数据应用字符串表达式和正则表达式，而且能处理烦人的缺失数据。

8、数据的规整，包括聚合、合并和重塑。层次化索引，在一个轴上拥有多个（两个以上）索引级别，方便用低维度形式处理高维度数据；联合与合并数据集，pandas.merge 根据一个或多个键将行进行连接，pandas.concat 使对象在轴向上进行黏合或「堆叠」，combine_first 实例方法允许将重叠的数据拼接在一起，以使用一个对象中的值填充另一个对象中的缺失值；数据的重塑或透视，使用多层索引进行重塑，2 个基础操作，stack 将数据的列「旋转」为行，unstack 将数据的行「旋转」为列。

9、一些基本的数据可视化操作，使用 pandas，matplotlib 和 seaborn。只是入门级的知识，深入的话去看有关可视化的书籍。图片和子图。颜色、标记和线型，刻度、标签和图例，注解以及在 Subplot 上绘图，将图表保存到文件。使用 pandas 和 seaborn 绘图，包括折线图、柱状图、直方图和密度图、散布图或点图、分面网格（facet grid）和类型数据。

13、模型开发的通常工作流是使用 pandas 进行数据加载和清洗，然后切换到建模库进行建模。用 Patsy 创建模型描述：用 Patsy 公式进行数据转换，分类数据和 Patsy；statsmodels 介绍：估计线性模型，估计时间序列过程；scikit-learn 介绍。

附录 A：深入 NumPy 库的数组计算，包括 ndarray 更内部的细节（数据指针、dtype、shape 和跨度信息），和更高级的数组操作（数组重塑、C 顺序和 Fortran 顺序、数组的合并和拆分、花式索引的等价函数）和算法。

## 0701. 数据清洗和准备

在数据分析和建模的过程中，相当多的时间要用在数据准备上：加载、清理、转换以及重塑。这些工作会占到分析师时间的 80% 或更多。有时，存储在文件和数据库中的数据的格式不适合某个特定的任务。许多研究者都选择使用通用编程语言（如 Python、Perl、R 或 Java）或 UNIX 文本处理工具（如 sed 或 awk）对数据格式进行专门处理。幸运的是，pandas 和内置的 Python 标准库提供了一组高级的、灵活的、快速的工具，可以让你轻松地将数据规变为想要的格式。

如果你发现了一种本书或 pandas 库中没有的数据操作方式，请尽管在邮件列表或 GitHub 网站上提出。实际上，pandas 的许多设计和实现都是由真实应用的需求所驱动的。在本章中，我会讨论处理缺失数据、重复数据、字符串操作和其它分析数据转换的工具。下一章，我会关注于用多种方法合并、重塑数据集。

2『去研究下「邮件列表」，很多地方看到这个概念。』

在许多数据分析工作中，缺失数据是经常发生的。pandas 的目标之一就是尽量轻松地处理缺失数据。例如，pandas 对象的所有描述性统计默认都不包括缺失数据。缺失数据在 pandas 中呈现的方式有些不完美，但对于大多数用户可以保证功能正常。对于数值数据，pandas 使用浮点值 NaN（Not a Number）表示缺失数据。我们称其为哨兵值，可以方便的检测出来；在 pandas 中，我们采用了 R 语言中的惯用法，即将缺失值表示为 NA，它表示不可用 not available。在统计应用中，NA 数据可能是不存在的数据或者虽然存在，但是没有观察到（例如，数据采集中发生了问题）。当进行数据清洗以进行分析时，最好直接对缺失数据进行分析，以判断数据采集的问题或缺失数据可能导致的偏差。Python 内置的 None 值在对象数组中也可以作为 NA；pandas 项目中还在不断优化内部细节以更好处理缺失数据，像用户 API 功能，例如 pandas.isnull，去除了许多恼人的细节。表 7-1 列出了一些关于缺失数据处理的函数。

1『哨兵值 NaN 可以用 np.nan 来赋值，而检测哨兵值用 Series 对象里的 isnull() 函数。』

过滤掉缺失数据的办法有很多种。你可以通过 pandas.isnull 或布尔索引的手工方法，但 dropna 可能会更实用一些。对于一个 Series，dropna 返回一个仅含非空数据和索引值的 Series，data.dropna() ；这等价于 data[data.notnull()]；而对于 DataFrame 对象，事情就有点复杂了。你可能希望丢弃全 NA 或含有 NA 的行或列。dropna 默认丢弃任何含有缺失值的行。传入 how='all' 将只丢弃全为 NA 的那些行。用这种方式丢弃列，只需传入 axis=1 即可；另一个滤除 DataFrame 行的问题涉及时间序列数据。假设你只想留下一部分观测数据，可以用 thresh 参数实现此目的。

1『以上都是说的如何删除缺失值。』

填充缺失数据。你可能不想滤除缺失数据（有可能会丢弃跟它有关的其他数据），而是希望通过其他方式填补那些「空洞」。对于大多数情况而言，fillna 方法是最主要的函数。通过一个常数调用 fillna 就会将缺失值替换为那个常数值；若是通过一个字典调用 fillna，就可以实现对不同的列填充不同的值；fillna 返回的是一个新的对象，但你也可以修改已经存在的对象；对 reindexing 有效的那些插值方法也可用于 fillna；使用 fillna 你可以完成很多带有一点创造性的工作。例如，你可以将 Series 的平均值或中位数用于填充缺失值；表 7-2 列出了 fillna 的参考。

1『frame.fillna(0)，缺失值全部填充为 0；frame.fillna({1:0.5, 2:0})，将第 2 列的缺失值转换为 0.5，将第 3 列的缺失值转换为 0；_ = frame.fillna(0, inplace=True) 修改现有的对象；data.fillna(data.mean()) ，用 data 的平均值填充缺失值。』

数据转换。本章到目前为止介绍的都是数据的重排。另一类重要操作则是过滤、清理以及其他的转换工作。

移除重复数据。DataFrame 中出现重复行有多种原因。下面就是一个例子；DataFrame 的 duplicated 方法返回一个布尔型 Series，表示各行是否是重复行（前面出现过的行）；还有一个与此相关的 drop_duplicates 方法，它会返回一个 DataFrame，重复的数组会标为 False；这两个方法默认会判断全部列，你也可以指定部分列进行重复项判断。假设我们还有一列值，且只希望根据 k1 列过滤重复项。

1『data.drop_duplicates(['k1'])，对列名为 k1 的列进行过滤重复项操作；duplicated 和 drop_duplicates 默认保留的是第一个出现的值组合。传入 keep='last' 则保留最后一个。』

3『设备表的清洗过程中可以用到，因为后面要做 groupby 整合，开始的时候进行了向前填充处理：specdata.loc[:,'posnum'] = specdata['posnum'].fillna(method='ffill')，这时候通过删掉重复行达到保留第一行设备信息的目的：specdata.drop_duplicates(['posnum'], inplace=True)。还有种办法是在填充之前，删掉位号那列是空值的所有行：data = data[data['posnum'].notnull()]。』

利用函数或映射进行数据转换。对于许多数据集，你可能希望根据数组、Series 或 DataFrame 列中的值来实现转换工作。我们来看看下面这组有关肉类的数据；假设你想要添加一列表示该肉类食物来源的动物类型。我们先编写一个不同肉类到动物的映射；Series 的 map 方法可以接受一个函数或含有映射关系的字典型对象，但是这里有一个小问题，即有些肉类的首字母大写了，而另一些则没有。因此，我们还需要使用 Series 的 str.lower 方法，将各个值转换为小写；我们也可以传入一个能够完成全部这些工作的函数；使用 map 是一种实现元素级转换以及其他数据清理工作的便捷方式。

1『添加一列表示该肉类食物来源的动物类型，即传递一个映射数据进去，感觉就是在不同的关系型数据表里，根据主键值进行数据的传递。』

```py
In [55]: lowercased = data['food'].str.lower() 
In [56]: lowercased 
In [57]: data['animal'] = lowercased.map(meat_to_animal) 
In [58]: data 
```

1『这个太 NB 了，基本思路：1）DataFrame 的特定列变小写同时转化成了一个 Series对象；对这个 Series 对象使用 map() 函数，同时传入的是一个字典型对象，这时会形成一个新的 Series 对象；3）把这个新的 Series 对象作为新增的一列数据添加进原来的 DataFrame 对象里，data['animal'] = lowercased.map(meat_to_animal) 。另外更牛的是上面的 2 个过程可以仅仅通过 lambda 匿名函数与 map() 函数的结合体，即一行代码完成：data['food'].map(lambda x: meat_to_animal[x.lower()])￼。』

替换值。利用 fillna 方法填充缺失数据可以看做值替换的一种特殊情况。前面已经看到，map 可用于修改对象的数据子集，而 replace 则提供了一种实现该功能的更简单、更灵活的方式。我们来看看下面这个 Series；-999 这个值可能是一个表示缺失数据的标记值。要将其替换为 pandas 能够理解的 NA 值，我们可以利用 replace 来产生一个新的 Series（除非传入 inplace=True）；如果你希望一次性替换多个值，可以传入一个由待替换值组成的列表以及一个替换值；要让每个值有不同的替换值，可以传递一个替换列表；传入的参数也可以是字典；笔记：data.replace 方法与 data.str.replace 不同，后者做的是字符串的元素级替换。我们会在后面学习 Series 的字符串方法。

1『data.replace(-999, np.nan)』

```py
In [62]: data.replace(-999, np.nan) 
In [63]: data.replace([-999, -1000], np.nan)
In [64]: data.replace([-999, -1000], [np.nan, 0])
In [65]: data.replace({-999: np.nan, -1000: 0})
```

重命名轴索引。跟 Series 中的值一样，轴标签也可以通过函数或映射进行转换，从而得到一个新的不同标签的对象。轴还可以被就地修改，而无需新建一个数据结构。接下来看看下面这个简单的例子；跟 Series 一样，轴索引也有一个 map 方法；你可以将其赋值给 index，这样就可以对 DataFrame 进行就地修改；如果想要创建数据集的转换版（而不是修改原始数据），比较实用的方法是 rename；特别说明一下，rename 可以结合字典型对象实现对部分轴标签的更新；rename 可以实现复制 DataFrame 并对其索引和列标签进行赋值。如果希望就地修改某个数据集，传入 inplace=True 即可。

```py
In [67]: transform = lambda x: x[:4].upper() 
In [68]: data.index.map(transform) 
In [69]: data.index = data.index.map(transform) 
In [70]: data 
In [71]: data.rename(index=str.title, columns=str.upper) 
In [72]: data.rename(index={'OHIO': 'INDIANA'}, columns={'three': 'peekaboo'})
In [73]: data.rename(index={'OHIO': 'INDIANA'}, inplace=True) 
```

离散化和分箱。连续值经常需要离散化，或者分离成「箱子」进行分析。假设你有某项研究中一组人群的数据，你想将他们进行分组，放入离散的年龄框中；接下来将这些数据划分为「18 到 25」、「26 到 35」、「35 到 60」以及「60 以上」几个组。要实现该功能，你需要使用 pandas 的 cut 函数；pandas 返回的对象是一个特殊的 Categorical 对象。你看到的输出描述了由 pandas.cut 计算出的箱。你可以将它当作一个表示箱名的字符串数组，它在内部包含一个categories（类别）数组，它指定了不同的类别名称以及 codes 属性中的 ages（年龄）数据标签。

1『分箱操作，输入源是一些列离散的数据点，传入一个由「锚点」组成的列表来分割这个数据源，从而形成一个个箱体，每个箱体里装的是用相邻 2 个锚点做上下限的离散数据。两个主要的参数是 cut() 和 qcut()，作者说这两个离散化函数对于分位数和分组分析特别有用，主要用于聚合和分组操作，但目前还没有 get 到应用点，以后留意。』

请注意，pd.value_counts(cats) 是对 pandas.cut 的结果中的箱数量的计数。与区间的数学符号一致，小括号表示边是开放的，中括号表示它是封闭的（包括边）。你可以通过传递 right=False 来改变哪一边是封闭的；你也可以通过向 labels 选项传递一个列表或数组来传入自定义的箱名；如果你传给 cut 整数个的箱来代替显式的箱边，pandas 将根据数据中的最小值和最大值计算出等长的箱。请考虑一些均匀分布的数据被切成四份的情况，precision=2 的选项将十进制精度限制在两位。qcut 是一个与分箱密切相关的函数，它基于样本分位数进行分箱。取决于数据的分布，使用 cut 通常不会使每个箱具有相同数据量的数据点。由于 qcut 使用样本的分位数，你可以通过 qcut 获得等长的箱；与 cut 类似，你可以传入自定义的分位数（0 和 1 之间的数据，包括边）；后续章节中，在讨论聚合和分组操作时，我们将会继续讨论 cut 和 qcut，因为这些离散化函数对于分位数和分组分析特别有用。

2『分箱操作应该可以应用于分割脚本里，实现如何把字符串列表分割为特定的一组组。实现代码用来替换掉原来的分割函数。』

```py
In [75]: ages = [20, 22, 25, 27, 21, 23, 37, 31, 61, 45, 41, 32]
In [76]: bins = [18, 25, 35, 60, 100] 
In [77]: cats = pd.cut(ages, bins) 
In [78]: cats 

In [79]: cats.codes 
In [80]: cats.categories 
In [81]: pd.value_counts(cats) 

In [82]: pd.cut(ages, [18, 26, 36, 61, 100], right=False) 
In [83]: group_names = ['Youth', 'YoungAdult', 'MiddleAged', 'Senior'] 
In [84]: pd.cut(ages, bins, labels=group_names) 

In [85]: data = np.random.rand(20) 
In [86]: pd.cut(data, 4, precision=2) 
In [87]: data = np.random.randn(1000) # Normally distributed 
In [88]: cats = pd.qcut(data, 4) # Cut into quartiles 
In [91]: pd.qcut(data, [0, 0.1, 0.5, 0.9, 1.]) 
```

检测和过滤异常值。过滤或变换异常值（outlier）在很大程度上就是运用数组运算。来看一个含有正态分布数据的 DataFrame；假设你想要找出某列中绝对值大小超过 3 的值；要选出全部含有「超过 3 或 -3 的值」的行，你可以在布尔型 DataFrame 中使用 any 方法；根据这些条件，就可以对值进行设置。下面的代码可以将值限制在区间 -3 到 3 以内；根据数据的值是正还是负，np.sign(data) 可以生成 1 和 -1。

```py
In [92]: data = pd.DataFrame(np.random.randn(1000, 4)) 
In [93]: data.describe() 
In [94]: col = data[2] 
In [95]: col[np.abs(col) > 3] 

In [96]: data[(np.abs(data) > 3).any(1)] 
In [97]: data[np.abs(data) > 3] = np.sign(data) * 3 
In [98]: data.describe() 
In [99]: np.sign(data).head() 
```

排列和随机采样。利用 numpy.random.permutation 函数可以轻松实现对 Series 或 DataFrame 的列的排列工作（permuting，随机重排序）。通过需要排列的轴的长度调用 permutation，可产生一个表示新顺序的整数数组；整数数组可以用在基于 iloc 的索引或等价的 take 函数中；要选出一个不含有替代值的随机子集，你可以使用 Series 和 DataFrame 的 sample 方法；要生成一个带有替代值的样本（允许有重复选择），将 replace=True 传入 sample 方法；


```py
In [100]: df = pd.DataFrame(np.arange(5 * 4).reshape((5, 4))) 
In [101]: sampler = np.random.permutation(5) 
In [102]: sampler 
Out[102]: array([3, 1, 4, 2, 0])

In [104]: df.take(sampler) 
In [105]: df.sample(n=3) 
In [106]: choices = pd.Series([5, 7, -1, 6, 4]) 
In [107]: draws = choices.sample(n=10, replace=True) 
```

计算指标/虚拟变量。将分类变量转换为「虚拟」或「指标」矩阵是另一种用于统计建模或机器学习的转换操作。如果 DataFrame 中的一列有 k 个不同的值，则可以衍生一个 k 列的值为 1 和 0 的矩阵或 DataFrame。pandas 有一个 get_dummies 函数用于实现该功能，尽管你自行实现也不难。让我们回顾一下之前的一个示例 DataFrame；在某些情况下，你可能想在指标 DataFrame 的列上加入前缀，然后与其他数据合并。在 get_dummies 方法中有一个前缀参数用于实现该功能；如果 DataFrame 中的一行属于多个类别，则情况略为复杂。

让我们看看 MovieLens 的 1M 数据集，在第 14 章中有更为详细的介绍；为每个电影流派添加指标变量需要进行一些数据处理。首先，我们从数据集中提取出所有不同的流派的列表。使用全 0 的 DataFrame 是构建指标 DataFrame 的一种方式；现在，遍历每一部电影，将 dummies 每一行的条目设置为 1。为了实现该功能，我们使用 dummies.columns 来计算每一个流派的列指标；之后，使用 .loc 根据这些指标来设置值；之后，和前面一样，你可以将结果与 movies 进行联合。

笔记：对于更大的数据，上面这种使用多成员构建指标变量并不是特别快速。更好的方法是写一个直接将数据写为 NumPy 数组的底层函数，然后将结果封装进 DataFrame。

将 get_dummies 与 cut 等离散化函数结合使用是统计应用的一个有用方法；我们使用 numpy.random.seed 来设置随机种子以确保示例的确定性。我们将在本书后面的内容中再次讨论 pandas.get_dummies。

字符串操作。Python 能够成为流行的数据处理语言，部分原因是其简单易用的字符串和文本处理功能。大部分文本运算都直接做成了字符串对象的内置方法。对于更为复杂的模式匹配和文本操作，则可能需要用到正则表达式。pandas 对此进行了加强，它使你能够对整组数据应用字符串表达式和正则表达式，而且能处理烦人的缺失数据。

字符串对象方法。对于许多字符串处理和脚本应用，内置的字符串方法已经能够满足要求了。例如，以逗号分隔的字符串可以用 split 拆分成数段；split 常常与 strip 一起使用，以去除空白符（包括换行符）；利用加法，可以将这些子字符串以双冒号分隔符的形式连接起来；但这种方式并不是很实用。一种更快更符合 Python 风格的方式是，向字符串 "::" 的 join 方法传入一个列表或元组；其它方法关注的是子串定位。检测子串的最佳方式是利用 Python 的 in 关键字，还可以使用 index 和 find；注意 find 和 index 的区别：如果找不到字符串，index 将会引发一个异常（而不是返回－1）；与此相关，count 可以返回指定子串的出现次数；replace 用于将指定模式替换为另一个模式。通过传入空字符串，它也常常用于删除模式；表 7-3 列出了 Python 内置的字符串方法。这些运算大部分都能使用正则表达式实现。casefold 将字符转换为小写，并将任何特定区域的变量字符组合转换成一个通用的可比较形式。

```py
In [134]: val = 'a,b, guido' 
In [135]: val.split(',') 
Out[135]: ['a', 'b', ' guido']

In [136]: pieces = [x.strip() for x in val.split(',')] 
In [137]: pieces 
Out[137]: ['a', 'b', 'guido']

In [140]: '::'.join(pieces) 
Out[140]: 'a::b::guido'

In [141]: 'guido' in val 
Out[141]: True 
In [142]: val.index(',') 
Out[142]: 1 
In [143]: val.find(':') 
Out[143]: -1
In [144]: val.index(':') 
--------------------------------------------------------------------------- 
ValueError: substring not found

In [145]: val.count(',') 
Out[145]: 2
In [146]: val.replace(',', '::') 
Out[146]: 'a::b:: guido' 
In [147]: val.replace(',', '') 
Out[147]: 'ab guido'
```

正则表达式。正则表达式提供了一种灵活的在文本中搜索或匹配（通常比前者复杂）字符串模式的方式。正则表达式，常称作 regex，是根据正则表达式语言编写的字符串。Python 内置的 re 模块负责对字符串应用正则表达式。re 模块的函数可以分为三个大类：模式匹配、替换以及拆分。当然，它们之间是相辅相成的。一个 regex 描述了需要在文本中定位的一个模式，它可以用于许多目的。我们先来看一个简单的例子：假设我想要拆分一个字符串，分隔符为数量不定的一组空白符（制表符、空格、换行符等）。描述一个或多个空白符的 regex 是 \s+。

1『re 模块的三大类：模式匹配、替换和拆分。』

调用 re.split ('\s+',text) 时，正则表达式会先被编译，然后再在 text 上调用其 split 方法。你可以用 re.compile 自己编译 regex 以得到一个可重用的 regex 对象；如果你想获得的是一个所有匹配正则表达式的模式的列表，你可以使用 findall 方法；如果打算对许多字符串应用同一条正则表达式，强烈建议通过 re.compile 创建 regex 对象。这样将可以节省大量的 CPU 时间；如果想避免正则表达式中不需要的转义（\），则可以使用原始字符串字面量如 r'C:\x'（也可以编写其等价式 'C:\\x'）。

match 和 search 跟 findall 功能类似。findall 返回的是字符串中所有的匹配项，而 search 则只返回第一个匹配项。match 更加严格，它只匹配字符串的首部。来看一个小例子，假设我们有一段文本以及一条能够识别大部分电子邮件地址的正则表达式；对 text 使用 findall 将得到一组电子邮件地址；search 返回的是文本中第一个电子邮件地址（以特殊的匹配项对象形式返回）。对于上面那个 regex，匹配项对象只能告诉我们模式在原字符串中的起始和结束位置；regex.match 则将返回 None，因为它只匹配出现在字符串开头的模式。

相关的，sub 方法可以将匹配到的模式替换为指定字符串，并返回所得到的新字符串；假设你不仅想要找出电子邮件地址，还想将各个地址分成 3 个部分：用户名、域名以及域后缀。要实现此功能，只需将待分段的模式的各部分用圆括号包起来即可；由这种修改过的正则表达式所产生的匹配项对象，可以通过其 groups 方法返回一个由模式各段组成的元组；对于带有分组功能的模式，findall 会返回一个元组列表；sub 还能通过诸如 \1、\2 之类的特殊符号访问各匹配项中的分组。符号 \1 对应第一个匹配的组，\2 对应第二个匹配的组，以此类推；Python 中还有许多的正则表达式，但大部分都超出了本书的范围。表 7-4 是一个简要概括。

```py
In [148]: import re 
In [149]: text = "foo bar\t baz \tqux" 
In [150]: re.split('\s+', text) 
Out[150]: ['foo', 'bar', 'baz', 'qux']
In [151]: regex = re.compile('\s+') 
In [152]: regex.split(text) 
Out[152]: ['foo', 'bar', 'baz', 'qux']

In [153]: regex.findall(text) 
Out[153]: [' ', '\t ', ' \t']

text = """Dave dave@google.com Steve steve@gmail.com Rob rob@gmail.com Ryan ryan@yahoo.com """ 
pattern = r'[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}' 
#  re.IGNORECASE 使用正则表达式不区分大小写
regex = re.compile(pattern, flags=re.IGNORECASE)

In [155]: regex.findall(text) 
Out[155]: ['dave@google.com', 'steve@gmail.com', 'rob@gmail.com', 'ryan@yahoo.com']

In [156]: m = regex.search(text) 
In [157]: m 
Out[157]: <_sre.SRE_Match object; span=(5, 20), match='dave@google.com'> 
In [158]: text[m.start():m.end()] 
Out[158]: 'dave@google.com'

In [159]: print(regex.match(text)) 
None

In [161]: pattern = r'([A-Z0-9._%+-]+)@([A-Z0-9.-]+)\.([A-Z]{2,4})' 
In [162]: regex = re.compile(pattern, flags=re.IGNORECASE)

In [163]: m = regex.match('wesm@bright.net') 
In [164]: m.groups() 
Out[164]: ('wesm', 'bright', 'net')

In [165]: regex.findall(text) 
Out[165]: [('dave', 'google', 'com'), ('steve', 'gmail', 'com'), ('rob', 'gmail', 'com'), ('ryan', 'yahoo', 'com')]

In [166]: print(regex.sub(r'Username: \1, Domain: \2, Suffix: \3', text)) 
```

pandas 的矢量化字符串函数。清理待分析的散乱数据时，常常需要做一些字符串规整化工作。更为复杂的情况是，含有字符串的列有时还含有缺失数据；通过 data.map，所有字符串和正则表达式方法都能被应用于（传入 lambda 表达式或其他函数）各个值，但是如果存在 NA（null）就会报错。为了解决这个问题，Series 有一些能够跳过 NA 值的面向数组方法，进行字符串操作。通过 Series 的 str 属性即可访问这些方法。例如，我们可以通过 str.contains 检查各个电子邮件地址是否含有 "gmail"；也可以使用正则表达式，还可以加上任意 re 选项（如 IGNORECASE）；有两个办法可以实现矢量化的元素获取操作：要么使用 str.get，要么在 str 属性上使用索引；要访问嵌入列表中的元素，我们可以传递索引到这两个函数中；你可以利用这种方法对字符串进行截取；表 7-5 介绍了更多的 pandas 字符串方法。

```py
In [171]: data.str.contains('gmail') 
In [172]: pattern 
Out[172]: '([A-Z0-9._%+-]+)@([A-Z0-9.-]+)\\.([A-Z]{2,4})' 
In [173]: data.str.findall(pattern, flags=re.IGNORECASE) 

In [174]: matches = data.str.match(pattern, flags=re.IGNORECASE) 
In [175]: matches 
In [176]: matches.str.get(1) 
In [177]: matches.str[0] 
In [178]: data.str[:5] 
```

## 0801. 数据规整：聚合、合并和重塑

在许多应用中，数据可能分散在许多文件或数据库中，存储的形式也不利于分析。本章关注可以聚合、合并、重塑数据的方法。首先，我会介绍 pandas 的层次化索引，它广泛用于以上操作。然后，我深入介绍了一些特殊的数据操作。在第 14 章，你可以看到这些工具的多种应用。

层次化索引（hierarchical indexing）是 pandas 的一项重要功能，它使你能在一个轴上拥有多个（两个以上）索引级别。抽象点说，它使你能以低维度形式处理高维度数据。我们先来看一个简单的例子：创建一个 Series，并用一个由列表或数组组成的列表作为索引；看到的结果是经过美化的带有 MultiIndex 索引的 Series 的格式。索引之间的「间隔」表示「直接使用上面的标签」；对于一个层次化索引的对象，可以使用所谓的部分索引，使用它选取数据子集的操作更简单；有时甚至还可以在「内层」中进行选取。

层次化索引在数据重塑和基于分组的操作（如透视表生成）中扮演着重要的角色。例如，可以通过 unstack 方法将这段数据重新安排到一个 DataFrame 中；unstack 的逆运算是 stack；对于一个 DataFrame，每条轴都可以有分层索引；各层都可以有名字（可以是字符串，也可以是别的 Python 对象）。如果指定了名称，它们就会显示在控制台输出中；注意：小心区分索引名 state、color 与行标签；有了部分列索引，因此可以轻松选取列分组；可以单独创建 MultiIndex 然后复用。上面那个 DataFrame 中的（带有分级名称）列可以这样创建。

重排与分级排序。有时，你需要重新排列轴上的层级顺序，或者按照特定层级的值对数据进行排序。swaplevel 接收两个层级序号或层级名称，返回一个进行了层级变更的新对象（但是数据是不变的）；另一方面，sort_index 只能在单一层级上对数据进行排序。在进行层级变换时，使用 sort_index 以使得结果按照层级进行字典排序也很常见；如果索引按照字典顺序从最外层开始排序，那么数据选择性能会更好 —— 调用 sort_index(level=0) 或 sort_index 可以得到这样的结果。

按层级进行汇总统计。DataFrame 和 Series 中很多描述性和汇总性统计有一个 level 选项，通过 level 选项你可以指定你想要在某个特定的轴上进行聚合。考虑上述示例中的 DataFrame，我们可以按照层级在行或列上像下面这样进行聚合；上面的例子使用了 pandas 的 groupby 机制，这个机制的细节将会在本书后续章节讨论。

使用 DataFrame 的列进行索引。通常我们不会使用 DataFrame 中一个或多个列作为行索引；反而你可能想要将行索引移动到 DataFrame 的列中。下面是一个示例 DataFrame；DataFrame 的 set_index 函数会生成一个新的 DataFrame，新的 DataFrame 使用一个或多个列作为索引；默认情况下这些列会从 DataFrame 中移除，你也可以将它们留在 DataFrame 中；另一方面，reset_index 是 set_index 的反操作，分层索引的索引层级会被移动到列中。

联合与合并数据集。包含在 pandas 对象的数据可以通过多种方式联合在一起：pandas.merge 根据一个或多个键将行进行连接。对于 SQL 或其他关系型数据库的用户来说，这种方式比较熟悉，它实现的是数据库的连接操作；pandas.concat 使对象在轴向上进行黏合或「堆叠」；combine_first 实例方法允许将重叠的数据拼接在一起，以使用一个对象中的值填充另一个对象中的缺失值。

数据集的合并（merge）或连接（join）运算是通过一个或多个键将行链接起来的。这些运算是关系型数据库（基于 SQL）的核心。pandas 的 merge 函数是对数据应用这些算法的主要切入点。以一个简单的例子开始；这是一种多对一的合并。df1 中的数据有多个被标记为 a 和 b 的行，而 df2 中 key 列的每个值则仅对应一行。对这些对象调用 merge 即可得到；请注意，我并没有指定在哪一列上进行连接。如果连接的键信息没有指定，merge 会自动将重叠列名作为连接的键。但是，显式地指定连接键才是好的实现。可能你已经注意到了，结果里面 c 和 d 以及与之相关的数据消失了。默认情况下，merge 做的是「内连接」；结果中的键是交集。其他方式还有 "left"、"right" 以及 "outer"。外连接求取的是键的并集，组合了左连接和右连接的效果。表 8-1 对这些选项进行了总结。

```py
In [39]: pd.merge(df1, df2) 
In [40]: pd.merge(df1, df2, on='key') 
In [44]: pd.merge(df1, df2, how='outer') 
```

多对多的合并有些不直观。看下面的例子；多对多连接产生的是行的笛卡尔积。由于左边的 DataFrame 有 3 个 "b" 行，右边的有 2 个，所以最终结果中就有 6 个 "b" 行。连接方式只影响出现在结果中的不同的键的值；要根据多个键进行合并，传入一个由列名组成的列表即可；结果中会出现哪些键组合取决于所选的合并方式，你可以这样来理解：多个键形成一系列元组，并将其当做单个连接键（当然，实际上并不是这么回事）。注意：在进行列－列连接时，DataFrame 对象中的索引会被丢弃。

对于合并运算需要考虑的最后一个问题是对重复列名的处理。虽然你可以手工处理列名重叠的问题（查看前面介绍的重命名轴标签），但 merge 有一个更实用的 suffixes 选项，用于指定附加到左右两个 DataFrame 对象的重叠列名上的字符串；indicator 添加特殊的列 _merge，它可以指明每个行的来源，它的值有 left_only、right_only 或 both，根据每行的合并数据的来源。merge 的参数请参见表 8-2。

根据索引合并。在某些情况下，DataFrame 中用于合并的键是它的索引。在这种情况下，你可以传递 left_index=True 或 right_index=True（或者都传）来表示索引需要用来作为合并的键；由于默认的 merge 方法是求取连接键的交集，因此你可以通过外连接的方式得到它们的并集；在多层索引数据的情况下，事情会更复杂，在索引上连接是一个隐式的多键合并；这种情况下，你必须以列表的方式指明合并所需多个列（请注意使用 how='outer’ 处理重复的索引值）；使用两边的索引进行合并也是可以的。

DataFrame 有一个方便的 join 实例方法，用于按照索引合并。该方法也可以用于合并多个索引相同或相似但没有重叠列的 DataFrame 对象。在之前的例子中，我们可以这样写；由于一些历史原因（例如，一些非常早期版本的 pandas）, DataFrame 的 join 方法进行连接键上的左连接，完全保留左边 DataFrame 的行索引。它还支持在调用 DataFrame 的某一列上连接传递的 DataFrame 的索引；最后，对于一些简单索引-索引合并，你可以向 join 方法传入一个 DataFrame 列表，这个方法可以替代下一节中将要介绍的使用更为通用的 concat 函数的方法。

另一种数据组合操作可互换地称为拼接、绑定或堆叠。NumPy 的 concatenate 函数可以在 NumPy 数组上实现该功能；在 Series 和 DataFrame 等 pandas 对象的上下文中，使用标记的轴可以进一步泛化数组连接。尤其是你还有许多需要考虑的事情：如果对象在其他轴上的索引不同，我们是否应该将不同的元素组合在这些轴上，还是只使用共享的值（交集）？连接的数据块是否需要在结果对象中被识别？「连接轴」是否包含需要保存的数据？在许多情况下，DataFrame 中的默认整数标签在连接期间最好丢弃。pandas 的 concat 函数提供了一种一致性的方式来解决以上问题。我将给出一些例子来表明它的工作机制。假设我们有三个索引不存在重叠的 Series。

对这些对象调用 concat 可以将值和索引粘合在一起；默认情况下，concat 是在 axis=0 上工作的，最终产生一个新的 Series。如果传入 axis=1，则结果就会变成一个 DataFrame（axis=1 是列）；这种情况下，另外的轴上没有重叠，从索引的有序并集（外连接）上就可以看出来。传入 join='inner' 即可得到它们的交集；在这个例子中，f 和 g 标签消失了，是因为使用的是 join='inner' 选项。你可以通过 join_axes 指定要在其它轴上使用的索引。

不过有个问题，参与连接的片段在结果中区分不开。假设你想要在连接轴上创建一个层次化索引。使用 keys 参数即可达到这个目的；如果沿着 axis=1 对 Series 进行合并，则 keys 就会成为 DataFrame 的列头；同样的逻辑也适用于 DataFrame 对象。如果传入的不是列表而是一个字典，则字典的键就会被当做 keys 选项的值。

```py
In [82]: s1 = pd.Series([0, 1], index=['a', 'b']) 
In [83]: s2 = pd.Series([2, 3, 4], index=['c', 'd', 'e']) 
In [84]: s3 = pd.Series([5, 6], index=['f', 'g'])
In [85]: pd.concat([s1, s2, s3]) 

In [86]: pd.concat([s1, s2, s3], axis=1) 
In [87]: s4 = pd.concat([s1, s3]) 
```

此外还有两个用于管理层次化索引创建方式的参数（参见表 8-3）。举个例子，我们可以用 names 参数命名创建的轴级别；最后一个关于 DataFrame 的问题是，DataFrame 的行索引不包含任何相关数据；在这种情况下，传入 ignore_index=True 即可。

合并重叠数据。还有一种数据组合问题不能用简单的合并（merge）或连接（concatenation）运算来处理。比如说，你可能有索引全部或部分重叠的两个数据集。举个有启发性的例子，我们使用 NumPy 的 where 函数，它表示一种等价于面向数组的 if-else；Series 有一个 combine_first 方法，实现的也是一样的功能，还带有 pandas 的数据对齐；对于 DataFrame，combine_first 自然也会在列上做同样的事情，因此你可以将其看做：用传递对象中的数据为调用对象的缺失数据「打补丁」。

重塑和透视。重排列表格型数据有多种基础操作。这些操作被称为重塑或透视。

使用多层索引进行重塑。多层索引在 DataFrame 中提供了一种一致性方式用于重排列数据。以下是两个基础操作：stack，将数据的列「旋转」为行；unstack，将数据的行「旋转」为列。

对该数据使用 stack 方法即可将列转换为行，得到一个 Series；对于一个层次化索引的 Series，你可以用 unstack 将其重排为一个 DataFrame；默认情况下，unstack 操作的是最内层（stack 也是如此）。传入分层级别的编号或名称即可对其它级别进行 unstack 操作；如果不是所有的级别值都能在各分组中找到的话，则 unstack 操作可能会引入缺失数据；stack 默认会滤除缺失数据，因此该运算是可逆的；在对 DataFrame 进行 unstack 操作时，作为旋转轴的级别将会成为结果中的最低级别；当调用 stack，我们可以指明轴的名字。

将「长格式」旋转为「宽格式」。多个时间序列数据通常是以所谓的「长格式」（long）或「堆叠格式」（stacked）存储在数据库和 CSV 中的。我们先加载一些示例数据，做一些时间序列规整和数据清洗；我们将在第 11 章中更深入地讲解 PeriodIndex。简单地说，PeriodIndex 将 year 和 quarter 等列进行联合并生成了一种时间间隔类型：现在，ldata 看起来如下。

这种数据即所谓的多时间序列的长格式，或称为具有两个或更多个键的其他观测数据（这里，我们的键是 date 和 item）。表中的每一行表示一个时间点上的单个观测值。数据通常以这种方式存储在关系型数据库中，比如 MySQL，因为固定模式（列名称和数据类型）允许 item 列中不同值的数量随着数据被添加到表中而改变。在之前的例子中，date 和 item 通常是主键（使用关系型数据库的说法），提供了关系完整性和更简单的连接。在某些情况下，处理这种格式的数据更为困难，你可能更倾向于获取一个按 date 列时间戳索引的且每个不同的 item 独立一列的 DataFrame。DataFrame 的 pivot 方法就是进行这种转换的。

传递的前两个值是分别用作行和列索引的列，然后是可选的数值列以填充 DataFrame。假设你有两个数值列，你想同时进行重塑；如果遗漏最后一个参数，你会得到一个含有多层列的 DataFrame；请注意，pivot 方法等价于使用 set_index 创建分层索引，然后调用 unstack。

将「宽格式」旋转为「长格式」。旋转 DataFrame 的逆运算是 pandas.melt。它不是将一列转换到多个新的 DataFrame，而是合并多个列成为一个，产生一个比输入长的 DataFrame。看一个例子；key 列可能是分组指标，其它的列是数据值。当使用 pandas.melt，我们必须指明哪些列是分组指标。下面使用 key 作为唯一的分组指标；使用 pivot，可以重塑回原来的样子；因为 pivot 的结果从列创建了一个索引，用作行标签，我们可以使用 reset_index 将数据移回列；你还可以指定列的子集，作为值的列；pandas.melt 也可以不用分组指标。

## 0901. 绘图和可视化

与其它开源库类似，Python 创建图形的方式非常多（根本罗列不完）。自从 2010 年，许多开发工作都集中在创建交互式图形以便在 Web 上发布。利用工具如 [Boken](https://docs.bokeh.org/en/latest/) 和 [Plotly](https://github.com/plotly/plotly.py)，现在可以创建动态交互图形，用于网页浏览器。对于创建用于打印或网页的静态图形，我建议默认使用 matplotlib 和附加的库，比如 pandas 和 seaborn。对于其它数据可视化要求，学习其它的可用工具可能是有用的。我鼓励你探索绘图的生态系统，因为它将持续发展。

信息可视化（也叫绘图）是数据分析中最重要的工作之一。它可能是探索过程的一部分，例如，帮助我们找出异常值、必要的数据转换、得出有关模型的 idea 等。另外，做一个可交互的数据可视化也许是工作的最终目标。Python 有许多库进行静态或动态的数据可视化，但我这里重要关注于 matplotlib和基于它的库。

matplotlib 是一个用于创建出版质量图表的桌面绘图包（主要是 2D 方面）。该项目是由 John Hunter 于 2002 年启动的，其目的是为 Python 构建一个 MATLAB 式的绘图接口。matplotlib 和 IPython 社区进行合作，简化了从 IPython shell（包括现在的 Jupyter notebook）进行交互式绘图。matplotlib 支持各种操作系统上许多不同的 GUI 后端，而且还能将图片导出为各种常见的矢量（vector）和光栅（raster）图：PDF、SVG、JPG、PNG、BMP、GIF 等。除了几张，本书中的大部分图都是用它生成的。随着时间的发展，matplotlib 衍生出了多个数据可视化的工具集，它们使用 matplotlib 作为底层。其中之一是 [seaborn: statistical data visualization — seaborn 0.10.0 documentation](http://seaborn.pydata.org/)，本章后面会学习它。学习本章代码案例的最简单方法是在 Jupyter notebook 进行交互式绘图。在 Jupyter notebook 中执行下面的语句：

    %matplotlib notebook

1『上面在 Jupyter notebook 里的操作还没头绪。』

虽然 seaborn 这样的库和 pandas 的内置绘图函数能够处理许多普通的绘图任务，但如果需要自定义一些高级功能的话就必须学习 matplotlib API。matplotlib 的示例库和文档是学习高级特性的最好资源。

图片与子图。matplotlib 所绘制的图位于图片（Figure）对象中。你可以使用 plt.figure 生成一个新的图片；如果用的是 IPython，这时会弹出一个空窗口，但在 Jupyter 中，必须再输入更多命令才能看到。plt.figure 有一些选项，特别是 figsize，它用于确保当图片保存到磁盘时具有一定的大小和纵横比。不能通过空 Figure 绘图。必须用 add_subplot 创建一个或多个子图（subplot）才行；这条代码的意思是：图像应该是 2×2 的（即最多 4 张图），且当前选中的是 4 个 subplot 中的第一个（编号从 1 开始）。如果再把后面两个 subplot 也创建出来，最终得到的图像如图 9-2 所示；

```py
In [16]: fig = plt.figure()
In [17]: ax1 = fig.add_subplot(2, 2, 1)
In [18]: ax2 = fig.add_subplot(2, 2, 2) 
In [19]: ax3 = fig.add_subplot(2, 2, 3)
```

注意：使用 Jupyter notebook 时有个细节需要注意，在每个单元格运行后，图表被重置，因此对于更复杂的图表，你必须将所有的绘图命令放在单个的 notebook 单元格中。我们将上面的代码在同一个单元格中运行；如果这时执行一条绘图命令（如 plt.plot ([1.5, 3.5, -2, 1.6])），matplotlib 就会在最后一个用过的 subplot（如果没有则创建一个）上进行绘制，隐藏创建 figure 和 subplot 的过程。因此，如果我们执行下列命令，你就会得到如图 9-3 所示的结果；'k--' 是一个线型选项，用于告诉 matplotlib 绘制黑色虚线图。上面那些由 fig.add_subplot 所返回的对象是 AxesSubplot 对象，直接调用它们的实例方法就可以在其它空着的格子里面画图了，如图 9-4 所示；你可以在 matplotlib 的文档中找到各种图表类型。

```py
In [20]: plt.plot(np.random.randn(50).cumsum(), 'k--')
In [21]: _ = ax1.hist(np.random.randn(100), bins=20, color='k', alpha=0.3) 
In [22]: ax2.scatter(np.arange(30), np.arange(30) + 3 * np.random.randn(30))
```

使用子图网格创建图片是非常常见的任务，所以 matplotlib 包含了一个便捷方法 plt.subplots，它创建一个新的图片，然后返回包含了已生成子图对象的 NumPy 数组；这是非常有用的，因为数组 axes 可以像二维数组那样方便地进行索引，例如， axes[0, 1]。你也可以通过使用 sharex 和 sharey 来表明子图分别拥有相同的 x 轴或 y 轴。当你在相同的比例下进行数据对比时，sharex 和 sharey 会非常有用；此外， matplotlib 还可以独立地缩放图像的界限。表 9-1 对此方法有更多介绍。

```py
In [24]: fig, axes = plt.subplots(2, 3) 
In [25]: axes 
```

调整子图周围的间距。默认情况下，matplotlib 会在子图的外部和子图之间留出一定的间距。这个间距都是相对于图的高度和宽度来指定的，所以如果你通过编程或手动使用 GUI 窗口来调整图的大小，那么图就会自动调整。你可以使用图对象上的 subplots_adjust 方法更改间距，也可以用作顶层函数；wspace 和 hspace 用于控制宽度和高度的百分比，可以用作 subplot 之间的间距。下面是一个简单的例子，其中我将间距收缩到了 0（如图 9-5 所示）；你可能会注意到轴标签是存在重叠的。matplotlib并不检查标签是否重叠，因此在类似情况下你需要通过显式指定刻度位置和刻度标签的方法来修复轴标签。

```py
subplots_adjust(left=None, bottom=None, right=None, top=None, wspace=None, hspace=None)

fig, axes = plt.subplots(2, 2, sharex=True, sharey=True) 
for i in range(2): 
    for j in range(2): 
        axes[i, j].hist(np.random.randn(500), bins=50, color='k', alpha=0.5) 
plt.subplots_adjust(wspace=0, hspace=0)
```

颜色、标记和线类型。matplotlib 的主函数 plot 接收带有 x 和 y 轴的数组以及一些可选的字符串缩写参数来指明颜色和线类型。例如，要用绿色破折号绘制 x 对 y 的线，你需要执行；这种在一个字符串中指定颜色和线型的方式非常方便。在实际中，如果你是用代码绘图，你可能不想通过处理字符串来获得想要的格式。通过下面这种更为明确的方式也能得到同样的效果；常用的颜色可以使用颜色缩写，你也可以指定颜色码（例如，'#CECECE'）。你可以通过查看 plot 的文档字符串查看所有线型的合集（在 IPython 和 Jupyter 中使用 plot?）。

```py
ax.plot(x, y, 'g--')
ax.plot(x, y, linestyle='--', color='g')

In [30]: from numpy.random import randn 
In [31]: plt.plot(randn(30).cumsum(), 'ko--')
```

线图可以使用标记强调数据点。因为 matplotlib 可以创建连续线图，在点之间进行插值，因此有时可能不太容易看出真实数据点的位置。标记也可以放到格式字符串中，但标记类型和线型必须放在颜色后面（见图 9-6）；还可以将其写成更为明确的形式。

```py
In [30]: from numpy.random import randn 
In [31]: plt.plot(randn(30).cumsum(), 'ko--')

plot(randn(30).cumsum(), color='k', linestyle='dashed', marker='o')
```

对于折线图，你会注意到后续的点默认是线性内插的。可以通过 drawstyle 选项修改（见图 9-7）；你可能注意到运行上面代码时有输出 <matplotlib.lines.Line2D at ...>。matplotlib 会返回引用了新添加的子组件的对象。大多数时候，你可以放心地忽略这些输出。这里，因为我们传递了 label 参数到 plot，我们可以创建一个 plot 图例，指明每条使用 plt.legend 的线。笔记：你必须调用 plt.legend（或使用 ax.legend，如果引用了轴的话）来创建图例，无论你绘图时是否传递 label 标签选项。

```py
In [33]: data = np.random.randn(30).cumsum() 
In [34]: plt.plot(data, 'k--', label='Default') 
Out[34]: [<matplotlib.lines.Line2D at 0x7fb624d86160>] 
In [35]: plt.plot(data, 'k-', drawstyle='steps-post', label='steps-post') 
Out[35]: [<matplotlib.lines.Line2D at 0x7fb624d869e8>] 
In [36]: plt.legend(loc='best')
```

刻度、标签和图例。对于大多数的图表装饰项，其主要实现方式有二：使用过程型的 pyplot 接口（例如，matplotlib.pyplot）以及更为面向对象的原生 matplotlib API。pyplot 接口的设计目的就是交互式使用，含有诸如 xlim、xticks 和 xticklabels 之类的方法。它们分别控制图表的范围、刻度位置、刻度标签等。其使用方式有以下两种：调用时不带参数，则返回当前的参数值（例如，plt.xlim () 返回当前的 X 轴绘图范围）；调用时带参数，则设置参数值（例如，plt.xlim ([0,10]) 会将 X 轴的范围设置为 0 到 10）。所有这些方法都是对当前或最近创建的 AxesSubplot 起作用的。它们各自对应 subplot 对象上的两个方法，以 xlim 为例，就是 ax.get_xlim 和 ax.set_xlim。我更喜欢使用 subplot 的实例方法（因为我喜欢明确的事情，而且在处理多个 subplot 时这样也更清楚一些）。当然你完全可以选择自己觉得方便的那个。

设置标题、轴标签、刻度以及刻度标签。为了说明自定义轴，我将创建一个简单的图像并绘制一段随机漫步（如图 9-8 所示）；要改变 x 轴刻度，最简单的办法是使用 set_xticks 和 set_xticklabels。前者告诉 matplotlib 要将刻度放在数据范围中的哪些位置，默认情况下，这些位置也就是刻度标签。但我们可以通过 set_xticklabels 将任何其他的值用作标签；rotation 选项设定 x 刻度标签倾斜 30 度。最后，再用 set_xlabel 为 X 轴设置一个名称，并用 set_title 设置一个标题（见图 9-9 的结果）。

```py
In [37]: fig = plt.figure() 
In [38]: ax = fig.add_subplot(1, 1, 1) 
In [39]: ax.plot(np.random.randn(1000).cumsum())

In [40]: ticks = ax.set_xticks([0, 250, 500, 750, 1000]) 
In [41]: labels = ax.set_xticklabels(['one', 'two', 'three', 'four', 'five'], rotation=30, fontsize='small')

In [42]: ax.set_title('My first matplotlib plot') 
Out[42]: <matplotlib.text.Text at 0x7fb624d055f8> 
In [43]: ax.set_xlabel('Stages')
```

Y 轴的修改方式与此类似，只需将上述代码中的 x 替换为 y 即可。轴的类有集合（set）方法，可以批量设定绘图选项。前面的例子，也可以写为：

```py
props = { 
    'title': 'My first matplotlib plot', 
    'xlabel': 'Stages' 
} 
ax.set(**props)
```

图例（legend）是另一种用于标识图表元素的重要工具。添加图例的方式有多种。最简单的是在添加 subplot 的时候传入 label 参数；在此之后，你可以调用 ax.legend () 或 plt.legend () 来自动创建图例（结果见图 9-10）；legend 方法有几个其它的 loc 位置参数选项。请查看文档字符串（使用 ax.legend?）。loc 告诉 matplotlib 要将图例放在哪。如果你不是吹毛求疵的话，"best" 是不错的选择，因为它会选择最不碍事的位置。要从图例中去除一个或多个元素，不传入 label 或传入 label='nolegend' 即可。

```py
In [44]: from numpy.random import randn 
In [45]: fig = plt.figure(); ax = fig.add_subplot(1, 1, 1) 
In [46]: ax.plot(randn(1000).cumsum(), 'k', label='one') 
Out[46]: [<matplotlib.lines.Line2D at 0x7fb624bdf860>] 
In [47]: ax.plot(randn(1000).cumsum(), 'k--', label='two') 
Out[47]: [<matplotlib.lines.Line2D at 0x7fb624be90f0>] 
In [48]: ax.plot(randn(1000).cumsum(), 'k.', label='three') 
Out[48]: [<matplotlib.lines.Line2D at 0x7fb624be9160>]

In [49]: ax.legend(loc='best')
```

注释与子图加工。除了标准的绘图类型，你可能还会想在图表上绘制自己的注释，而且注释中可能会包含文本、箭头以及其他图形。你可以使用 text、arrow 和 annote 方法来添加注释和文本。text 在图表上给定的坐标（x, y），根据可选的定制样式绘制文本；注解中可以既含有文本也含有箭头。例如，我们根据最近的标准普尔 500 指数价格（来自 Yahoo!Finance）绘制一张曲线图，并标出 2008 年到 2009 年金融危机期间的一些重要日期。你可以在 Jupyter notebook 的一个小窗中试验这段代码（图 9-11 是结果）；这张图中有几个重要的点要强调：ax.annotate 方法可以在指定的 x 和 y 坐标轴绘制标签。我们使用 set_xlim 和 set_ylim 人工设定起始和结束边界，而不使用 matplotlib 的默认方法。最后，用 ax.set_title 添加图标标题。更多有关注解的示例，请访问 matplotlib 的在线示例库。

```py
ax.text(x, y, 'Hello world!', family='monospace', fontsize=10)

from datetime import datetime 
fig = plt.figure() 
ax = fig.add_subplot(1, 1, 1) 
data = pd.read_csv('examples/spx.csv', index_col=0, parse_dates=True) 
spx = data['SPX'] 
spx.plot(ax=ax, style='k-') 
crisis_data = [ 
    (datetime(2007, 10, 11), 'Peak of bull market'), 
    (datetime(2008, 3, 12), 'Bear Stearns Fails'), 
    (datetime(2008, 9, 15), 'Lehman Bankruptcy') 
] 
for date, label in crisis_data: 
    ax.annotate(label, xy=(date, spx.asof(date) + 75), 
    xytext=(date, spx.asof(date) + 225), 
    arrowprops=dict(facecolor='black', headwidth=4, width=2, headlength=4), 
    horizontalalignment='left', 
    verticalalignment='top') # Zoom in on 2007-2010 
ax.set_xlim(['1/1/2007', '1/1/2011']) 
ax.set_ylim([600, 1800]) 
ax.set_title('Important dates in the 2008-2009 financial crisis')
```

图形的绘制要麻烦一些。matplotlib 有一些表示常见图形的对象。这些对象被称为块（patch）。其中有些（如 Rectangle 和 Circle），可以在 matplotlib.pyplot 中找到，但完整集合位于 matplotlib.patches。要在图表中添加一个图形，你需要创建一个块对象 shp，然后通过 ax.add_patch (shp) 将其添加到 subplot 中（如图 9-12 所示）；如果查看许多常见图表对象的具体实现代码，你就会发现它们其实就是由块 patch 组装而成的。

```py
fig = plt.figure() 
ax = fig.add_subplot(1, 1, 1) 
rect = plt.Rectangle((0.2, 0.75), 0.4, 0.15, color='k', alpha=0.3) 
circ = plt.Circle((0.7, 0.2), 0.15, color='b', alpha=0.3) 
pgon = plt.Polygon([[0.15, 0.15], [0.35, 0.4], [0.2, 0.6]], color='g', alpha=0.5) 
ax.add_patch(rect) 
ax.add_patch(circ) 
ax.add_patch(pgon)
```

将图表保存到文件。利用 plt.savefig 可以将当前图表保存到文件。该方法相当于 Figure 对象的实例方法 savefig。例如，要将图表保存为 SVG 文件，你只需输入；文件类型是通过文件扩展名推断出来的。因此，如果你使用的是 .pdf，就会得到一个 PDF 文件。我在发布图片时最常用到两个重要的选项是 dpi（控制「每英寸点数」分辨率）和 bbox_inches（可以剪除当前图表周围的空白部分）。要得到一张带有最小白边且分辨率为 400DPI 的 PNG 图片，你可以；savefig 并非一定要写入磁盘，也可以写入任何文件型的对象，比如 BytesIO；表 9-2 列出了 savefig 的其它选项。

```py
plt.savefig('figpath.svg')

plt.savefig('figpath.png', dpi=400, bbox_inches='tight')

from io import BytesIO 
buffer = BytesIO() 
plt.savefig(buffer) 
plot_data = buffer.getvalue()
```

matplotlib 配置。matplotlib 自带一些配色方案，以及为生成出版质量的图片而设定的默认配置信息。幸运的是，几乎所有默认行为都能通过一组全局参数进行自定义，它们可以管理图像大小、subplot 边距、配色方案、字体大小、网格类型等。一种 Python 编程方式配置系统的方法是使用 rc 方法。例如，要将全局的图像默认大小设置为 10×10，你可以执行；rc 的第一个参数是希望自定义的对象，如 'figure'、'axes'、'xtick'、'ytick'、'grid'、'legend' 等。其后可以跟上一系列的关键字参数。一个简单的办法是将这些选项写成一个字典。

```py
plt.rc('figure', figsize=(10, 10))

font_options = {'family' : 'monospace', 
                            'weight' : 'bold', 
                            'size' : 'small'} 
plt.rc('font', **font_options)
```

要了解全部的自定义选项，请查阅 matplotlib 的配置文件 matplotlibrc（位于 matplotlib/mpl-data 目录中）。如果对该文件进行了自定义，并将其放在你自己的 .matplotlibrc 目录中，则每次使用 matplotlib 时就会加载该文件。下一节，我们会看到，seaborn 包有若干内置的绘图主题或类型，它们使用了 matplotlib 的内部配置。

1『/Users/Daglas/miniconda3/pkgs/matplotlib-3.1.1-py37h54f8f79_0/lib/python3.7/site-packages/matplotlib/mpl-data/matplotlibrc』

matplotlib 实际上是一种比较低级的工具。你可以从其基本组件中组装一个图表：数据展示（即图表类型：线型图、柱状图、盒形图、散布图、等值线图等）、图例、标题、刻度标签以及其他注解型信息。在 pandas 中，我们有多列数据，还有行和列标签。pandas 自身就有内置的方法，用于简化从 DataFrame 和 Series 绘制图形。另一个库 seaborn，由 Michael Waskom 创建的静态图形库。Seaborn 简化了许多常见可视类型的创建。

提示：引入 seaborn 会修改 matplotlib 默认的颜色方案和绘图类型，以提高可读性和美观度。即使你不使用 seaborn API，你可能也会引入 seaborn，作为提高美观度和绘制常见 matplotlib 图形的简化方法。

折线图。Series 和 DataFrame 都有一个 plot 属性，用于绘制基本的图形。默认情况下，plot() 绘制的是折线图（见图9-13）；Series 对象的索引传入 matplotlib 作为绘图的 x 轴，你可以通过传入 use_index=False 来禁用这个功能。x 轴的刻度和范围可以通过 xticks 和 xlim 选项进行调整，相应地 y 轴使用 yticks 和 ylim 进行调整。表 9-3 是 plot 的全部选项列表。

本节我会介绍这些选项中的一些，其余你可以自行探索。大部分 pandas 的绘图方法，接收可选的 ax 参数，该参数可以是一个 matplotlib 子图对象。这使你可以更为灵活地在网格布局中放置子图。DataFrame 的 plot 方法在同一个子图中将每一列绘制为不同的折线，并自动生成图例（见图 9-14）；plot 属性包含了不同绘图类型的方法族。例如，df.plot() 等价于 df.plot.line()。我们之后将会探索这些方法中的一部分。plot 的其他关键字参数会传递到相应的 matplotlib 绘图函数，因此你可以通过了解更多的 matplotlib 的 API 信息来进一步定制这些图表。DataFrame 拥有多个选项，允许灵活地处理列。例如，是否将各列绘制到同一个子图中，或为各列生成独立的子图。参考表 9-4 了解更多选项。

```py
In [60]: s = pd.Series(np.random.randn(10).cumsum(), index=np.arange(0, 100, 10)) 
In [61]: s.plot()

In [62]: df = pd.DataFrame(np.random.randn(10, 4).cumsum(0),  columns=['A', 'B', 'C', 'D'], index=np.arange(0, 100, 10)) 
In [63]: df.plot()
```

柱状图。plot.bar () 和 plot.barh () 分别绘制水平和垂直的柱状图。这时，Series 和 DataFrame 的索引将会被用作 X（bar）或 Y（barh）刻度（如图 9-15 所示）；color='k' 和 alpha=0.7 设定了图形的颜色为黑色，并使用部分的填充透明度。对于 DataFrame，柱状图会将每一行的值分为一组，并排显示，如图 9-16 所示；注意，DataFrame 各列的名称 "Genus" 被用作了图例的标题。设置 stacked=True 即可为 DataFrame 生成堆积柱状图，这样每行的值就会被堆积在一起（如图 9-17 所示）。

```py
In [64]: fig, axes = plt.subplots(2, 1) 
In [65]: data = pd.Series(np.random.rand(16), index=list('abcdefghijklmnop')) 
In [66]: data.plot.bar(ax=axes[0], color='k', alpha=0.7) 
Out[66]: <matplotlib.axes._subplots.AxesSubplot at 0x7fb62493d470> 
In [67]: data.plot.barh(ax=axes[1], color='k', alpha=0.7)

In [69]: df = pd.DataFrame(np.random.rand(6, 4), index=['one', 'two', 'three', 'four', 'five', 'six'], columns=pd.Index(['A', 'B', 'C', 'D'], name='Genus')) 
In [70]: df 
In [71]: df.plot.bar()

In [73]: df.plot.barh(stacked=True, alpha=0.5)
```

笔记：柱状图有一个非常不错的用法：利用 value_counts 图形化显示 Series 中各值的出现频率，比如 s.value_counts ().plot.bar ()。

再以本书前面用过的那个有关小费的数据集为例，假设我们想要做一张堆积柱状图以展示每天各种聚会规模的数据点的百分比。我用 read_csv 将数据加载进来，然后根据日期和聚会规模创建一张交叉表；然后进行规格化，使得各行的和为 1，并生成图表（如图 9-18 所示）；于是，通过该数据集就可以看出，聚会规模在周末会变大。

```py
In [75]: tips = pd.read_csv('examples/tips.csv') 
In [76]: party_counts = pd.crosstab(tips['day'], tips['size']) 
In [77]: party_counts 
# Not many 1- and 6-person parties 
In [78]: party_counts = party_counts.loc[:, 2:5]

# Normalize to sum to 1 
In [79]: party_pcts = party_counts.div(party_counts.sum(1), axis=0) 
In [80]: party_pcts 
In [81]: party_pcts.plot.bar()
```

对于在绘制一个图形之前，需要进行合计的数据，使用 seaborn 可以减少工作量。用 seaborn 来看每天的小费比例（图 9-19 是结果）；seaborn 的绘制函数使用 data 参数，它可能是 pandas 的 DataFrame。其它的参数是关于列的名字。因为一天的每个值有多次观察，柱状图的值是 tip_pct 的平均值。绘制在柱状图上的黑线代表 95% 置信区间（可以通过可选参数配置）。seaborn.barplot 有颜色选项，使我们能够通过一个额外的值设置（见图 9-20）；注意，seaborn 已经自动修改了图形的美观度：默认调色板，图形背景和网格线的颜色。你可以用 seaborn.set 在不同的图形外观之间切换。

```py
In [83]: import seaborn as sns 
In [84]: tips['tip_pct'] = tips['tip'] / (tips['total_bill'] - tips['tip'])
In [85]: tips.head() 
In [86]: sns.barplot(x='tip_pct', y='day', data=tips, orient='h')

In [88]: sns.barplot(x='tip_pct', y='day', hue='time', data=tips, orient='h')

In [90]: sns.set(style="whitegrid")
```

直方图和密度图。直方图（histogram）是一种可以对值频率进行离散化显示的柱状图。数据点被拆分到离散的、间隔均匀的面元中，绘制的是各面元中数据点的数量。再以前面那个小费数据为例，通过在 Series 使用 plot.hist 方法，我们可以生成一张「小费占消费总额百分比」的直方图（如图 9-21 所示）；与此相关的一种图表类型是密度图，它是通过计算「可能会产生观测数据的连续概率分布的估计」而产生的。一般的过程是将该分布近似为一组核（即诸如正态分布之类的较为简单的分布）。因此，密度图也被称作 KDE（Kernel Density Estimate，核密度估计）图。使用 plot.kde 和标准混合正态分布估计即可生成一张密度图（见图 9-22）；seaborn 的 distplot 方法绘制直方图和密度图更加简单，还可以同时画出直方图和连续密度估计图。作为例子，考虑一个双峰分布，由两个不同的标准正态分布组成（见图 9-23）。

```py
In [92]: tips['tip_pct'].plot.hist(bins=50)

In [94]: tips['tip_pct'].plot.density()

In [96]: comp1 = np.random.normal(0, 1, size=200) 
In [97]: comp2 = np.random.normal(10, 2, size=200) 
In [98]: values = pd.Series(np.concatenate([comp1, comp2])) 
In [99]: sns.distplot(values, bins=100, color='k')
```

散布图或点图。点图或散布图是观察两个一维数据序列之间的关系的有效手段。在下面这个例子中，我加载了来自 statsmodels 项目的 macrodata 数据集，选择了几个变量，然后计算对数差；然后可以使用 seaborn 的 regplot 方法，它可以做一个散布图，并加上一条线性回归的线（见图 9-24）；在探索式数据分析工作中，同时观察一组变量的散布图是很有意义的，这也被称为散布图矩阵（scatter plot matrix）。纯手工创建这样的图表很费工夫，所以 seaborn 提供了一个便捷的 pairplot 函数，它支持在对角线上放置每个变量的直方图或密度估计（见图 9-25）。

```py
In [100]: macro = pd.read_csv('examples/macrodata.csv') 
In [101]: data = macro[['cpi', 'm1', 'tbilrate', 'unemp']] 
In [102]: trans_data = np.log(data).diff().dropna() 
In [103]: trans_data[-5:] 

In [105]: sns.regplot('m1', 'unemp', data=trans_data) 
Out[105]: <matplotlib.axes._subplots.AxesSubplot at 0x7fb613720be0> 
In [106]: plt.title('Changes in log %s versus log %s' % ('m1', 'unemp'))

In [107]: sns.pairplot(trans_data, diag_kind='kde', plot_kws={'alpha': 0.2})
```

你可能注意到了 plot_kws 参数。它可以让我们传递配置选项到非对角线元素上的图形使用。对于更详细的配置选项，可以查阅 seaborn.pairplot 文档字符串。

分面网格（facet grid）和类型数据。要是数据集有额外的分组维度呢？有多个分类变量的数据可视化的一种方法是使用小面网格。seaborn 有一个有用的内置函数 factorplot，可以简化制作多种分面图（见图 9-26）；除了在分面中用不同的颜色按时间分组，我们还可以通过给每个时间值添加一行来扩展分面网格；factorplot 支持其它的绘图类型，你可能会用到。例如，盒图（它可以显示中位数，四分位数，和异常值）就是一个有用的可视化类型（见图 9-28）；使用更通用的 seaborn.FacetGrid 类，你可以创建自己的分面网格。请查阅 seaborn 的文档。

```py
In [108]: sns.factorplot(x='day', y='tip_pct', hue='time', col='smoker', kind='bar', data=tips[tips.tip_pct < 1])
In [109]: sns.factorplot(x='day', y='tip_pct', row='time', col='smoker', kind='bar', data=tips[tips.tip_pct < 1])
In [110]: sns.factorplot(x='tip_pct', y='day', kind='box', data=tips[tips.tip_pct < 0.5])
```

## 1301. Python 建模库介绍

只是介绍了一些 Python 建模库的表面内容，现在有越来越多的框架用于各种统计和机器学习，它们都是用 Python 或 Python 用户界面实现的。这本书的重点是数据规整，有其它的书是关注建模和数据科学工具的。其中优秀的有：Andreas Mueller and Sarah Guido (O’Reilly) 的 《Introduction to Machine Learning with Python》、Jake VanderPlas (O’Reilly) 的 《Python Data Science Handbook》、Joel Grus (O’Reilly) 的 《Data Science from Scratch: First Principles》、Sebastian Raschka (Packt Publishing) 的《Python Machine Learning》、Aurélien Géron (O’Reilly) 的《Hands-On Machine Learning with Scikit-Learn and TensorFlow》 。虽然书是学习的好资源，但是随着底层开源软件的发展，书的内容会过时。最好是不断熟悉各种统计和机器学习框架的文档，学习最新的功能和 API。

2『已下载书籍：「2019110Python机器学习基础教程/2019110Introduction_to_Machine_Learning_with_Python」、「2020043Python深度学习/2020043Deep_Learning_with_Python」、「2019004Python数据科学手册/2019004Python_Data_Science_Handbook」、「2020029数据科学入门1Ed/2020029Data_Science_from_Scratch2Ed」、「2020045Python机器学习1Ed/2020045Python_Machine_Learning3Ed」、「2020046机器学习实战1Ed/2020046Hands-On_Machine_Learning2Ed」、「2020039Python_Data_Analytics_With_PaNp」、「2020040Numerical_Python」、「2020041Data_Analysis_From_Scratch_With_Python」、「2020042Matplotlib_Cookbook」。外加之前下载的书籍「2020024Python_Data_Analysis_Cookbook2016」、「2020025Python_Data_Analysis2014」、「2020026NumPy_Cookbook2Ed2015」、「2020027NumPy_ Beginners_Guide3Ed2015」、「2020028Keeping_up_with_the_Quants」、「2020034Small_Data」、「2020035Pentaho_Kettle_Solutions」、「2020036Data_Mining_for_Business_Analytics_Python」、「2020037Data_Mining_Concepts_and_Techniques3Ed」。』

1『以上全是数据分析方面的书籍，其中 2020024-2020027 都是 Ivan Idris 写的书。』

因为数据分析师和科学家总是在数据规整和准备上花费大量时间，这本书的重点在于掌握这些功能。开发模型选用什么库取决于应用本身。许多统计问题可以用简单方法解决，比如普通的最小二乘回归，其它问题可能需要复杂的机器学习方法。幸运的是，Python 已经成为了运用这些分析方法的语言之一，因此读完此书，你可以探索许多工具。

本章中，我会回顾一些 pandas 的特点，在你胶着于 pandas 数据规整和模型拟合和评分时，它们可能派上用场。然后我会简短介绍两个流行的建模工具，statsmodels 和 scikit-learn。这二者每个都值得再写一本书，我就不做全面的介绍，而是建议你学习两个项目的线上文档和其它基于 Python 的数据科学、统计和机器学习的书籍。

模型开发的通常工作流是使用 pandas 进行数据加载和清洗，然后切换到建模库进行建模。开发模型的重要一环是机器学习中的「特征工程」。它可以描述从原始数据集中提取信息的任何数据转换或分析，这些数据集可能在建模中有用。本书中学习的数据聚合和 GroupBy 工具常用于特征工程中。优秀的特征工程超出了本书的范围，我会尽量直白地介绍一些用于数据操作和建模切换的方法。pandas 与其它分析库通常是靠 NumPy 的数组联系起来的。将 DataFrame 转换为 NumPy 数组，可以使用 .values 属性；要转换回 DataFrame，可以传递一个二维 ndarray，可带有列名。

1『frame.columns 是获得数据对象的列名称；frame.values 是将 DataFrame 数据结构中的数据转化为 NumPy 数组。』

```py
In [13]: data 
In [14]: data.columns 
Out[14]: Index(['x0', 'x1', 'y'], dtype='object') 
In [15]: data.values 
Out[15]: array([[ 1. , 0.01, -1.5 ], [ 2. , -0.01, 0. ], [ 3. , 0.25, 3.6 ], [ 4. , -4.1 , 1.3 ], [ 5. , 0. , -2. ]])
In [16]: df2 = pd.DataFrame(data.values, columns=['one', 'two', 'three']) 
In [17]: df2 
```

最好当数据是均匀的时候使用 .values 属性。例如，全是数值类型。如果数据是不均匀的，结果会是 Python 对象的 ndarray；对于一些模型，你可能只想使用列的子集。我建议你使用 loc，用 values 作索引；一些库原生支持 pandas，会自动完成工作：从 DataFrame 转换到 NumPy，将模型的参数名添加到输出表的列或 Series。其它情况，你可以手工进行「元数据管理」；在第 12 章，我们学习了 pandas 的 Categorical 类型和 pandas.get_dummies 函数。假设数据集中有一个非数值列。如果我们想替换 category 列为虚变量，我们可以创建虚变量，删除 category 列，然后添加到结果。用虚变量拟合某些统计模型会有一些细微差别。当你不只有数字列时，使用 Patsy（下一节的主题）可能更简单，更不容易出错。

```py
In [18]: df3 = data.copy() 
In [19]: df3['strings'] = ['a', 'b', 'c', 'd', 'e'] 
In [20]: df3 
In [21]: df3.values 
Out[21]: array([[1, 0.01, -1.5, 'a'], [2, -0.01, 0.0, 'b'], [3, 0.25, 3.6, 'c'], [4, -4.1, 1.3, 'd'], [5, 0.0, -2.0, 'e']], dtype=object)

In [22]: model_cols = ['x0', 'x1'] 
In [23]: data.loc[:, model_cols].values 

In [26]: dummies = pd.get_dummies(data.category, prefix='category') 
In [27]: data_with_dummies = data.drop('category', axis=1).join(dummies) 
In [28]: data_with_dummies 
```

Patsy 是 Python 的一个库，使用简短的字符串「公式语法」描述统计模型（尤其是线性模型），可能是受到了 R 和 S 统计编程语言的公式语法的启发。Patsy 适合描述 statsmodels 的线性模型，因此我会关注于它的主要特点，让你尽快掌握。Patsy 的公式是一个特殊的字符串语法，如下所示：

    y~x0 + x1

语法 a+b 并不代表 a 加 b，而是指为模型而创建的设计矩阵中的名词列。patsy.dmatrices 函数在数据集上（可以是一个 DataFrame 或数组的字典）使用了一个公式字符串，并为一个线性模型产生了设计矩阵；这些 Patsy 的 DesignMatrix 实例是 NumPy 的 ndarray，带有附加元数据；你可能想 Intercept 是哪里来的。这是线性模型（比如普通最小二乘胡桂）的惯例用法。添加 +0 到模型可以不显示 intercept；Patsy 对象可以直接传递到算法（比如 numpy.linalg.lstsq）中，它执行普通最小二乘回归；模型的元数据保留在 design_info 属性中，因此你可以重新附加列名到拟合系数，以获得一个 Series，例如。

```py
In [29]: data = pd.DataFrame({ ....: 'x0': [1, 2, 3, 4, 5], ....: 'x1': [0.01, -0.01, 0.25, -4.1, 0.], ....: 'y': [-1.5, 0., 3.6, 1.3, -2.]}) 
In [30]: data 
In [31]: import patsy 
In [32]: y, X = patsy.dmatrices('y ~ x0 + x1', data)

In [33]: y 
Out[33]: DesignMatrix with shape (5, 1) 
Intercept 
In [34]: X 
Out[34]: DesignMatrix with shape (5, 3) 
Intercept 

In [35]: np.asarray(y) 
Out[35]: array([[-1.5], [ 0. ], [ 3.6], [ 1.3], [-2. ]]) 
In [36]: np.asarray(X) 
Out[36]: array([[ 1. , 1. , 0.01], [ 1. , 2. , -0.01], [ 1. , 3. , 0.25], [ 1. , 4. , -4.1 ], [ 1. , 5. , 0. ]])

In [37]: patsy.dmatrices('y ~ x0 + x1 + 0', data)[1] 
Out[37]: DesignMatrix with shape (5, 2) 

In [38]: coef, resid, _, _ = np.linalg.lstsq(X, y)

In [39]: coef 
Out[39]: array([[ 0.3129], [-0.0791], [-0.2655]]) 
In [40]: coef = pd.Series(coef.squeeze(), index=X.design_info.column_names) 
In [41]: coef 
Out[41]: Intercept 0.312910 x0 -0.079106 x1 -0.265464 dtype: float64
```

用 Patsy 公式进行数据转换。可以将 Python 代码与 patsy 公式结合。在评估公式时，库将尝试查找在封闭作用域内使用的函数；常见的变量转换包括标准化（平均值为 0，方差为 1）和中心化（减去平均值）。Patsy 有内置的函数进行这样的工作；作为建模的一步，你可能拟合模型到一个数据集，然后用另一个数据集评估模型。另一个数据集可能是剩余的部分或是新数据。当执行中心化和标准化转变，用新数据进行预测要格外小心。因为你必须使用平均值或标准差转换新数据集，这也称作状态转换。patsy.build_design_matrices 函数可以应用于转换新数据，使用原始样本数据集的保存信息。因为 Patsy 中的加号不是加法的意义，当你按照名称将数据集的列相加时，你必须用特殊 I 函数将它们封装起来。

```py
In [42]: y, X = patsy.dmatrices('y ~ x0 + np.log(np.abs(x1) + 1)', data) 
In [43]: X 
Out[43]: DesignMatrix with shape (5, 3) 

In [44]: y, X = patsy.dmatrices('y ~ standardize(x0) + center(x1)', data) 
In [45]: X 
Out[45]: DesignMatrix with shape (5, 3) 

In [46]: new_data = pd.DataFrame({ 
....: 'x0': [6, 7, 8, 9], .
...: 'x1': [3.1, -0.5, 0, 2.3], 
....: 'y': [1, 2, 3, 4]}) 
In [47]: new_X = patsy.build_design_matrices([X.design_info], new_data) 
In [48]: new_X 
Out[48]: [DesignMatrix with shape (4, 3) 

In [49]: y, X = patsy.dmatrices('y ~ I(x0 + x1)', data) 
In [50]: X 
Out[50]: DesignMatrix with shape (5, 2) I
```

Patsy 的 patsy.builtins 模块还有一些其它的内置转换。请查看线上文档。分类数据有一类特殊的转换，我将在之后介绍。

分类数据与 Patsy。有多种方式可以将非数字类型数据转换以用于模型的设计矩阵。一个完整的解决方案是超出了本书的范围的，最好是能够学习一门统计学课程。当你在 Patsy 公式中使用非数字名词列时，它们将会被默认转换为虚拟变量。如果有拦截，其中一个级别将被排除以避免共线性；如果你从模型中忽略截距，每个分类值得列都会包括在设计矩阵的模型中；使用 C 函数，数值列可以截取为分类量；当你在模型中使用多个分类名，事情就会变复杂，因为会包括 key1:key2 形式的相交部分，它可以用在方差（ANOVA）模型分析中。Patsy 提供转换分类数据的其它方法，包括以特定顺序转换。请参阅线上文档。

statsmodels 介绍。statsmodels 是 Python 进行拟合多种统计模型、进行统计试验和数据探索可视化的库。Statsmodels 包含许多经典的统计方法，但没有贝叶斯方法和机器学习模型。statsmodels 包含的模型有：线性模型，广义线性模型和健壮线性模型；线性混合效应模型；方差（ANOVA）方法分析；时间序列过程和状态空间模型；广义的矩量法。下面会使用一些基本的 statsmodels 工具，探索 Patsy 公式和 pandasDataFrame 对象如何使用模型接口。

3『[Introduction — statsmodels](http://www.statsmodels.org/stable/index.html)』

估计线性模型。statsmodels 有多种线性回归模型，包括从基本（比如普通最小二乘）到复杂（比如迭代加权最小二乘法）的。statsmodels 的线性模型有两种不同的接口：基于数组，和基于公式。它们可以通过 API 模块引入；为了展示它们的使用方法，我们从一些随机数据生成一个线性模型：

```py
import statsmodels.api as sm 
import statsmodels.formula.api as smf

def dnorm(mean, variance, size=1): 
    if isinstance(size, int): 
        size = size, 
    return mean + np.sqrt(variance) * np.random.randn(*size) 
# For reproducibility 
np.random.seed(12345) 
N = 100 
X = np.c_[dnorm(0, 0.4, size=N), 
                dnorm(0, 0.6, size=N), 
                dnorm(0, 0.2, size=N)] 
eps = dnorm(0, 0.1, size=N) 
beta = [0.1, 0.3, 0.5] 
y = np.dot(X, beta) + eps
```

这里，我使用了「真实」模型和可知参数 beta。此时，dnorm 可用来生成正太分布数据，带有特定均值和方差。现在有；像之前 Patsy 看到的，线性模型通常要拟合一个截距。sm.add_constant 函数可以添加一个截距的列到现存的矩阵；sm.OLS 类可以拟合一个普通最小二乘回归；这个模型的 fit 方法返回了一个回归结果对象，它包含估计的模型参数和其它内容；对结果使用 summary 方法可以打印模型的详细诊断结果。

```py
In [66]: X[:5] 
Out[66]: 
array([[-0.1295, -1.2128, 0.5042], 
            [ 0.3029, -0.4357, -0.2542], 
            [-0.3285, -0.0253, 0.1384], 
            [-0.3515, -0.7196, -0.2582], 
            [ 1.2433, -0.3738, -0.5226]]) 
In [67]: y[:5] 
Out[67]: array([ 0.4279, -0.6735, -0.0909, -0.4895,-0.1289])

In [68]: X_model = sm.add_constant(X) 
In [69]: X_model[:5] 
Out[69]: 

In [70]: model = sm.OLS(y, X)

In [71]: results = model.fit() 
In [72]: results.params 
Out[72]: array([ 0.1783, 0.223 , 0.501 ])
```

这里的参数名为原始的名字 x1, x2 等等。假设所有的模型参数都在一个 DataFrame 中；现在，我们使用 statsmodels 的公式 API 和 Patsy 的公式字符串；观察下 statsmodels 是如何返回 Series 结果的，附带有 DataFrame 的列名。当使用公式和 pandas 对象时，我们不需要使用 add_constant。给出一个样本外数据，你可以根据估计的模型参数计算预测值；statsmodels 的线性模型结果还有其它的分析、诊断和可视化工具。除了普通最小二乘模型，还有其它的线性模型。

```py
In [74]: data = pd.DataFrame(X, columns=['col0', 'col1', 'col2']) 
In [75]: data['y'] = y 
In [76]: data[:5] 
Out[76]: 

In [77]: results = smf.ols('y ~ col0 + col1 + col2', data=data).fit() 
In [78]: results.params 
Out[78]: 
Intercept
In [79]: results.tvalues 
Out[79]: 
Intercept

In [80]: results.predict(data[:5]) 
```

估计时间序列过程。statsmodels 的另一模型类是进行时间序列分析，包括自回归过程、卡尔曼滤波和其它态空间模型，和多元自回归模型。用自回归结构和噪声来模拟一些时间序列数据。这个数据有 AR (2) 结构（两个延迟），参数是 0.8 和 - 0.4。当你和 AR 模型，你可能不知道滞后项的个数，因此可以用较多的滞后量来拟合这个模型；结果中的估计参数首先是截距，其次是前两个参数的估计值；更多的细节以及如何解释结果超出了本书的范围，可以通过 statsmodels 文档学习更多。

```py
init_x = 4 
import random 
values = [init_x, init_x] 
N = 1000 
b0 = 0.8 
b1 = -0.4 
noise = dnorm(0, 0.1, N) 
for i in range(N): 
    new_x = values[-1] * b0 + values[-2] * b1 + noise[i] 
    values.append(new_x)

In [82]: MAXLAGS = 5 
In [83]: model = sm.tsa.AR(values) 
In [84]: results = model.fit(MAXLAGS)

In [85]: results.params 
Out[85]: array([-0.0062, 0.7845, -0.4085, -0.0136, 0.015 , 0.0143])
```

scikit-learn 介绍。scikit-learn 是使用最广泛且最受信任的通用 Python 机器学习库。它包含广泛的标准监督的和无监督的机器学习方法，包括用于模型选择和评估、数据转换、数据加载和模型持久化的工具。这些模型可用于分类、聚类、预测和其他常见任务。有很多优秀的在线和印刷资源可用于学习机器学习，以及如何应用 scikit-learn 和 TensorFlow 等库来解决实际问题。在本节中，我将简要介绍一下 scikit-learn API 风格。在写这篇文章的时候，scikit-learn 并没有深度地和 pandas 集成，尽管还有一些附加的第三方包仍在开发中。不过，在模型拟合之前，pandas 对于「按摩」数据集非常有用。作为一个例子，我使用 Kaggle 比赛中关于泰坦尼克号上生还乘客的经典数据集，其中泰坦尼克号于 1912 年沉没。我们使用 pandas 载入测试和训练数据集：

3『

[scikit-learn: machine learning in Python — scikit-learn 0.22.1 documentation](https://scikit-learn.org/stable/)

[Titanic: Machine Learning from Disaster | Kaggle](https://www.kaggle.com/c/titanic)

』

statsmodels 和 scikit-learn 通常不能接收缺失数据，因此我们要查看列是否包含缺失值；在像这样的统计和机器学习的例子中，一个典型的任务是根据数据中的特征来预测乘客是否能幸存下来。将模型拟合到训练数据集上，然后在样本外测试数据集上进行评估。

我想用 Age 作为预测，但它缺少数据。有很多方法可以进行缺失数据插补（imputation），但我会做一个简单的插补，并使用训练数据集的中间值填充两个表中的空值；现在我们需要明确我们的模型。我添加了一列I sFemale 作为 ’Sex’ 列的编码版本；然后我们决定一些模型变量并创建 NumPy 数组；我没有声称这是一个好的模型，也没有说这些功能是正确设计的。我们使用 scikit-learn 的 LogisticRegression 模型创建一个模型实例；与 statsmodels 类似，我们可以使用模型的 fit 方法在训练数据上拟合模型；现在，我们可以使用 model.predict 为测试数据集形成预测。如果你拥有测试数据集的真实值，则可以计算精度百分比或其他一些错误指标。

实际上，模型训练中经常存在许多附加的复杂层次。许多模型具有可以调整的参数，并且存在可用于参数调整的交叉验证等技术以避免过度拟合训练数据。这通常可以在新数据上产生更好的预测性能或稳健性。交叉验证通过分割训练数据来模拟样本外预测。基于像均方误差之类的模型准确度分数，可以对模型参数执行网格搜索。一些模型，如逻辑回归，具有内置交叉验证的估计类。例如，LogisticRegressionCV 类可以与一个参数一起使用，该参数表示网格搜索在模型正则化参数 C 上的细致度。

要手动进行交叉验证，可以使用 cross_val_score 帮助函数，该函数处理数据拆分过程。例如，为了用我们的模型与训练数据的四个非重叠分割进行交叉验证，我们可以这样做；默认评分指标是依赖于模型的，但可以选择明确的评分函数。经过交叉验证的模型需要更长时间的训练，但通常可以产生更好的模型性能。

## 附录 A——NumPy 高级应用

NumPy 的 ndarray 提供了一种将同质数据块（可以是连续或跨越）解释为多维数组对象的方式。正如你之前所看到的那样，数据类型（dtype）决定了数据的解释方式，比如浮点数、整数、布尔值等。ndarray 如此强大的部分原因是所有数组对象都是数据块的一个跨度视图（strided view）。你可能想知道数组视图 arr[::2,::-1] 不复制任何数据的原因是什么。简单地说，ndarray 不只是一块内存和一个 dtype，它还有跨度信息，这使得数组能以各种步幅（step size）在内存中移动。更准确地讲，ndarray 内部由以下内容组成：一个指向数据（内存或内存映射文件中的一块数据）的指针；数据类型或 dtype，描述在数组中的固定大小值的格子；一个表示数组形状（shape）的元组；一个跨度元组（stride），其中的整数指的是为了前进到当前维度下一个元素需要「跨过」的字节数。

例如，一个 10×5 的数组，其形状为 (10,5)；一个典型的（C 顺序，稍后将详细讲解）3×4×5 的 float64（8 个字节）数组，其跨度为 (160,40,8) —— 知道跨度是非常有用的，通常，跨度在一个轴上越大，沿这个轴进行计算的开销就越大；虽然 NumPy 用户很少会对数组的跨度信息感兴趣，但它们却是构建非复制式数组视图的重要因素。跨度甚至可以是负数，这样会使数组在内存中后向移动，比如在切片 obj[::-1] 或 obj[:,::-1] 中就是这样的。

```py
In [10]: np.ones((10, 5)).shape
Out[10]: (10, 5)

In [11]: np.ones((3, 4, 5), dtype=np.float64).strides 
Out[11]: (160, 40, 8)
```

NumPy 数据类型体系。你可能偶尔需要检查数组中所包含的是否是整数、浮点数、字符串或 Python 对象。因为浮点数的种类很多（从 float16 到 float128），判断 dtype 是否属于某个大类的工作非常繁琐。幸运的是，dtype 都有一个超类（比如 np.integer 和 np.floating），它们可以跟 np.issubdtype 函数结合使用；调用 dtype 的 mro 方法即可查看其所有的父类。

```py
In [12]: ints = np.ones(10, dtype=np.uint16) 
In [13]: floats = np.ones(10, dtype=np.float32) 
In [14]: np.issubdtype(ints.dtype, np.integer) 
Out[14]: True 
In [15]: np.issubdtype(floats.dtype, np.floating) 
Out[15]: True

In [16]: np.float64.mro() 
Out[16]: [numpy.float64, numpy.floating, numpy.inexact, numpy.number, numpy.generic, float, object]

In [17]: np.issubdtype(ints.dtype, np.number) 
Out[17]: True
```

高级数组操作。除花式（神奇）索引、切片、布尔条件取子集等操作之外，数组的操作方式还有很多。虽然 pandas 中的高级函数可以处理数据分析工作中的许多重型任务，但有时你还是需要编写一些在现有库中找不到的数据算法。

数组重塑。多数情况下，你可以无需复制任何数据，就将数组从一个形状转换为另一个形状。只需向数组的实例方法 reshape 传入一个表示新形状的元组即可实现该目的。例如，假设有一个一维数组，我们希望将其重新排列为一个矩阵（结果见图 A-3）；图 A-3 按 C 顺序（按行）和按 Fortran 顺序（按列）进行重塑；多维数组也能被重塑；作为参数的形状的其中一维可以是 -1，它表示该维度的大小由数据本身推断而来；与 reshape 将一维数组转换为多维数组的运算过程相反的运算通常称为扁平化（flattening）或散开（raveling）；如果结果中的值与原始数组相同，ravel 不会产生源数据的副本。flatten 方法的行为类似于 ravel，只不过它总是返回数据的副本。

```py
In [18]: arr = np.arange(8) 
In [19]: arr 
Out[19]: array([0, 1, 2, 3, 4, 5, 6, 7]) 
In [20]: arr.reshape((4, 2)) 
Out[20]: array([[0, 1], [2, 3], [4, 5], [6, 7]])

In [21]: arr.reshape((4, 2)).reshape((2, 4)) 
Out[21]: array([[0, 1, 2, 3], [4, 5, 6, 7]])

In [22]: arr = np.arange(15) 
In [23]: arr.reshape((5, -1)) 
Out[23]: array([[ 0, 1, 2], [ 3, 4, 5], [ 6, 7, 8], [ 9, 10, 11], [12, 13, 14]])

In [27]: arr = np.arange(15).reshape((5, 3)) 
In [28]: arr 
Out[28]: array([[ 0, 1, 2], [ 3, 4, 5], [ 6, 7, 8], [ 9, 10, 11], [12, 13, 14]]) 
In [29]: arr.ravel() 
Out[29]: array([ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14])
```

C 顺序和 Fortran 顺序。NumPy 允许你更为灵活地控制数据在内存中的布局。默认情况下，NumPy 数组是按行优先顺序创建的。在空间方面，这就意味着，对于一个二维数组，每行中的数据项是被存放在相邻内存位置上的。另一种顺序是列优先顺序，它意味着每列中的数据项是被存放在相邻内存位置上的。由于一些历史原因，行和列优先顺序又分别称为 C 和 Fortran 顺序。在 FORTRAN 77 中，矩阵全都是列优先的；像 reshape 和 reval 这样的函数，都可以接受一个表示数组数据存放顺序的 order 参数。一般可以是 'C' 或 'F'（还有 'A' 和 'K' 等不常用的选项，具体请参考 NumPy 的文档）。图 A-3 对此进行了说明；图 A-3 按 C（行优先）或 Fortran（列优先）顺序进行重塑；二维或更高维数组的重塑过程比较令人费解（见图 A-3）。C 和 Fortran 顺序的关键区别就是维度的行进顺序：C / 行优先顺序：先经过更高的维度（例如，轴 1 会先于轴 0 被处理）。Fortran / 列优先顺序：后经过更高的维度（例如，轴 0 会先于轴 1 被处理）。

```py
In [31]: arr = np.arange(12).reshape((3, 4)) 
In [32]: arr 
Out[32]: array([[ 0, 1, 2, 3], [ 4, 5, 6, 7], [ 8, 9, 10, 11]]) 
In [33]: arr.ravel() 
Out[33]: array([ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]) 
In [34]: arr.ravel('F') 
Out[34]: array([ 0, 4, 8, 1, 5, 9, 2, 6, 10, 3, 7, 11])
```

数组的合并和拆分。numpy.concatenate 可以按指定轴将一个由数组组成的序列（如元组、列表等）连接到一起；对于常见的连接操作，NumPy 提供了一些比较方便的方法（如 vstack 和 hstack）。因此，上面的运算还可以表达为：

```py
In [35]: arr1 = np.array([[1, 2, 3], [4, 5, 6]]) 
In [36]: arr2 = np.array([[7, 8, 9], [10, 11, 12]]) 
In [37]: np.concatenate([arr1, arr2], axis=0) 
Out[37]: array([[ 1, 2, 3], [ 4, 5, 6], [ 7, 8, 9], [10, 11, 12]]) 
In [38]: np.concatenate([arr1, arr2], axis=1) 
Out[38]: array([[ 1, 2, 3, 7, 8, 9], [ 4, 5, 6, 10, 11, 12]])

In [39]: np.vstack((arr1, arr2)) 
Out[39]: array([[ 1, 2, 3], [ 4, 5, 6], [ 7, 8, 9], [10, 11, 12]]) 
In [40]: np.hstack((arr1, arr2)) 
Out[40]: array([[ 1, 2, 3, 7, 8, 9], [ 4, 5, 6, 10, 11, 12]])
```

与此相反，split 用于将一个数组沿指定轴拆分为多个数组；传入到 np.split 的值 [1,3] 指示在哪个索引处分割数组。表 A-1 中列出了所有关于数组连接和拆分的函数，其中有些是专门为了方便常见的连接运算而提供的。

```py
In [41]: arr = np.random.randn(5, 2) 
In [42]: arr 
Out[42]: array([[-0.2047, 0.4789], [-0.5194, -0.5557], [ 1.9658, 1.3934], [ 0.0929, 0.2817], [ 0.769 , 1.2464]]) 
In [43]: first, second, third = np.split(arr, [1, 3]) 
In [44]: first 
Out[44]: array([[-0.2047, 0.4789]]) 
In [45]: second 
Out[45]: array([[-0.5194, -0.5557], [ 1.9658, 1.3934]]) 
In [46]: third 
Out[46]: array([[ 0.0929, 0.2817], [ 0.769 , 1.2464]])
```

NumPy 命名空间中有两个特殊的对象 —— r_ 和 c_，它们可以使数组的堆叠操作更为简洁；它还可以将切片转换成数组；r_ 和 c_ 的具体功能请参考其文档。

元素的重复操作：tile 和 repeat。对数组进行重复以产生更大数组的工具主要是 repeat 和 tile 这两个函数。repeat 会将数组中的各个元素重复一定次数，从而产生一个更大的数组；跟其他流行的数组编程语言（如 MATLAB）不同，NumPy 中很少需要对数组进行重复（replicate）。这主要是因为广播（broadcasting，我们将在下一节中讲解该技术）能更好地满足该需求。默认情况下，如果传入的是一个整数，则各元素就都会重复那么多次。如果传入的是一组整数，则各元素就可以重复不同的次数；对于多维数组，还可以让它们的元素沿指定轴重复；注意，如果没有设置轴向，则数组会被扁平化，这可能不会是你想要的结果。同样，在对多维进行重复时，也可以传入一组整数，这样就会使各切片重复不同的次数。

```py
In [53]: arr = np.arange(3) 
In [54]: arr 
Out[54]: array([0, 1, 2]) 
In [55]: arr.repeat(3) 
Out[55]: array([0, 0, 0, 1, 1, 1, 2, 2, 2])

In [56]: arr.repeat([2, 3, 4]) 
Out[56]: array([0, 0, 1, 1, 1, 2, 2, 2, 2])

In [57]: arr = np.random.randn(2, 2) 
In [58]: arr 
Out[58]: array([[-2.0016, -0.3718], [ 1.669 , -0.4386]]) 
In [59]: arr.repeat(2, axis=0) 
Out[59]: array([[-2.0016, -0.3718], [-2.0016, -0.3718], [ 1.669 , -0.4386], [ 1.669 , -0.4386]])
```

tile 的功能是沿指定轴向堆叠数组的副本。你可以形象地将其想象成「铺瓷砖」；第二个参数是瓷砖的数量。对于标量，瓷砖是水平铺设的，而不是垂直铺设。它可以是一个表示「铺设」布局的元组。

花式（神奇）索引的等价函数：take 和 put。在第 4 章中我们讲过，获取和设置数组子集的一个办法是通过整数数组使用花式索引；ndarray 还有其它方法用于获取单个轴向上的选区；要在其它轴上使用 take，只需传入 axis 关键字即可；put 不接受 axis 参数，它只会在数组的扁平化版本（一维，C 顺序）上进行索引。因此，在需要用其他轴向的索引设置元素时，最好还是使用花式索引。

```py
In [67]: arr = np.arange(10) * 100 
In [68]: inds = [7, 1, 2, 6] 
In [69]: arr[inds] 
Out[69]: array([700, 100, 200, 600])

In [70]: arr.take(inds) 
Out[70]: array([700, 100, 200, 600]) 
In [71]: arr.put(inds, 42) 
In [72]: arr
Out[72]: array([ 0, 42, 42, 300, 400, 500, 42, 42,800, 900]) 
In [73]: arr.put(inds, [40, 41, 42, 43]) 
In [74]: arr 
Out[74]: array([ 0, 41, 42, 300, 400, 500, 43, 40, 800, 900])

In [75]: inds = [2, 0, 2, 1] 
In [76]: arr = np.random.randn(2, 4) 
In [77]: arr 
Out[77]: array([[-0.5397, 0.477 , 3.2489, -1.0212], [-0.5771, 0.1241, 0.3026, 0.5238]]) 
In [78]: arr.take(inds, axis=1) 
Out[78]: array([[ 3.2489, -0.5397, 3.2489, 0.477 ], [ 0.3026, -0.5771, 0.3026, 0.1241]])
```

广播（broadcasting）指的是不同形状的数组之间的算术运算的执行方式。它是一种非常强大的功能，但也容易令人误解，即使是经验丰富的老手也是如此。将标量值跟数组合并时就会发生最简单的广播；这里我们说：在这个乘法运算中，标量值 4 被广播到了其他所有的元素上。

```py
In [79]: arr = np.arange(5) 
In [80]: arr 
Out[80]: array([0, 1, 2, 3, 4]) 
In [81]: arr * 4 
Out[81]: array([ 0, 4, 8, 12, 16])
```

例如，我们可以通过减去列均值来降低数组中的每一列的数值。在这种情况下，它非常简单；图 A-4 形象地展示了该过程。对行进行减均值的广播需要更小心。幸运的是，只要遵循规则，就可以在数组的任何维度上对潜在较低维度值进行广播（例如从二维数组的每一列中减去行均值）。于是我们有（广播的规则）：如果对于每个结尾维度（即从尾部开始的），轴长度都匹配或者长度都是 1，两个二维数组就是可以兼容广播的。之后，广播会在丢失的或长度为 1 的轴上进行。

1『换个说法是，只要遵循一定的规则，低维度的值是可以被广播到数组的任意维度的（比如对二维数组各列减去行平均值）。』

```py
In [82]: arr = np.random.randn(4, 3) 
In [83]: arr.mean(0) 
Out[83]: array([-0.3928, -0.3824, -0.8768]) 
In [84]: demeaned = arr - arr.mean(0) 
In [85]: demeaned 
Out[85]: array([[ 0.3937, 1.7263, 0.1633], [-0.4384, -1.9878, -0.9839], [-0.468 , 0.9426, -0.3891], [ 0.5126, -0.6811, 1.2097]]) 
In [86]: demeaned.mean(0) 
Out[86]: array([-0., 0., -0.])
```

虽然我是一名经验丰富的 NumPy 老手，但经常还是得停下来画张图并想想广播的原则。再来看一下最后那个例子，假设你希望对各行减去那个平均值。由于 arr.mean (0) 的长度为 3，所以它可以在 0 轴向上进行广播：因为 arr 的后缘维度是 3，所以它们是兼容的。根据该原则，要在 1 轴向上做减法（即各行减去行平均值），较小的那个数组的形状必须是 (4,1)：

```py
In [87]: arr 
Out[87]: array([[ 0.0009, 1.3438, -0.7135], [-0.8312, -2.3702, -1.8608], [-0.8608, 0.5601, -1.2659], [ 0.1198, -1.0635, 0.3329]]) 
In [88]: row_means = arr.mean(1) 
In [89]: row_means.shape Out[89]: (4,) 
In [90]: row_means.reshape((4, 1)) 
Out[90]: array([[ 0.2104], [-1.6874], [-0.5222], [-0.2036]]) 
In [91]: demeaned = arr - row_means.reshape((4, 1)) 
In [92]: demeaned.mean(1) 
Out[92]: array([ 0., -0., 0., 0.])
```

图 A-5 说明了该运算的过程。图 A-6 展示了另外一种情况，这次是在一个三维数组上沿 0 轴向加上一个二维数组。

沿其它轴向广播。高维度数组的广播似乎更难以理解，而实际上它也是遵循广播原则的。如果不然，你就会得到下面这样一个错误；人们经常需要通过算术运算过程将较低维度的数组在除 0 轴以外的其他轴向上广播。根据广播的原则，较小数组的「广播维」必须为 1。在上面那个行距平化的例子中，这就意味着要将行平均值的形状变成 (4,1) 而不是 (4,)；对于三维的情况，在三维中的任何一维上广播其实也就是将数据重塑为兼容的形状而已。

图 A-7 说明了要在三维数组各维度上广播的形状需求。于是就有了一个非常普遍的问题（尤其是在通用算法中），即专门为了广播而添加一个长度为 1 的新轴。虽然 reshape 是一个办法，但插入轴需要构造一个表示新形状的元组。这是一个很郁闷的过程。因此，NumPy 数组提供了一种通过索引机制插入轴的特殊语法。下面这段代码通过特殊的 np.newaxis 属性以及「全」切片来插入新轴；因此，如果我们有一个三维数组，并希望对轴 2 进行距平化，那么只需要编写下面这样的代码就可以了；因此，如果我们有一个三维数组，并希望对轴 2 进行距平化，那么只需要编写下面这样的代码就可以了。有些读者可能会想，在对指定轴进行距平化时，有没有一种既通用又不牺牲性能的方法呢？实际上是有的，但需要一些索引方面的技巧。

通过广播设置数组的值。算术运算所遵循的广播原则同样也适用于通过索引机制设置数组值的操作。对于最简单的情况，我们可以这样做；但是，假设我们想要用一个一维数组来设置目标数组的各列，只要保证形状兼容就可以了。

```py
In [107]: arr = np.zeros((4, 3)) 
In [108]: arr[:] = 5 In [109]: arr 
Out[109]: array([[ 5., 5., 5.], [ 5., 5., 5.], [ 5., 5., 5.], [ 5., 5., 5.]])

In [110]: col = np.array([1.28, -0.42, 0.44, 1.6]) 
In [111]: arr[:] = col[:, np.newaxis] 
In [112]: arr 
Out[112]: array([[ 1.28, 1.28, 1.28], [-0.42, -0.42, -0.42], [ 0.44, 0.44, 0.44], [ 1.6 , 1.6 , 1.6 ]]) 
In [113]: arr[:2] = [[-1.37], [0.509]] 
In [114]: arr 
Out[114]: array([[-1.37 , -1.37 , -1.37 ], [ 0.509, 0.509, 0.509], [ 0.44 , 0.44 , 0.44 ], [ 1.6 , 1.6 , 1.6 ]])
```