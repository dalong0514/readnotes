# 0101. Getting Started with Scientiﬁc Python

Python went mainstream years ago. It is now part of many undergraduate curricula in engineering and computer science. Great books and interactive on-line tutorials are easy to ﬁnd. In particular, Python is well-established in web programming with frameworks such as Django and CherryPy, and is the back-end platform for many high-trafﬁc sites.

Beyond web programming, there is an ever-expanding list of third-party extensions that reach across many scientiﬁc disciplines, from linear algebra to visualization to machine learning. For these applications, Python is the software glue that permits easy exchange of methods and data across core routines typically written in Fortran or C. Scientiﬁc Python has been fundamental for almost two decades in government, academia, and industry. For example, NASA’s Jet Propulsion Laboratory uses it for interfacing Fortran/C++ libraries for planning and visualization of spacecraft trajectories. The Lawrence Livermore National Laboratory uses scientiﬁc Python for a wide variety of computing tasks, some involving routine text processing, and others involving advanced visualization of vast data sets (e.g. VISIT [1]). Shell Research, Boeing, Industrial Light and Magic, Sony Entertainment, and Procter & Gamble use scientiﬁc Python on a daily basis for data processing and analysis. Python is thus well-established and continues to extend into many different ﬁelds.

Python is a language geared towards scientists and engineers who may not have formal software development training. It is used to prototype, design, simulate, and test without getting in the way because Python provides an inherently easy and incremental development cycle, interoperability with existing codes, access to a large base of reliable open source codes, and a hierarchical compartmentalized design philosophy. It is known that productivity is strongly inﬂuenced by the workﬂow of the user, (e.g., time spent running versus time spent programming) [2]. Therefore, Python can dramatically enhance user-productivity.

Python is an interpreted language. This means that Python codes run on a Python virtual machine that provides a layer of abstraction between the code and the platform it runs on, thus making codes portable across different platforms. For example, the same script that runs on a Windows laptop can also run on a Linux-based supercomputer or on a mobile phone. This makes programming easier because the virtual machine handles the low-level details of implementing the business logic of the script on the underlying platform.

Python is a dynamically typed language, which means that the interpreter itself ﬁgures out the representative types (e.g., ﬂoats, integers) interactively or at run-time. This is in contrast to a language like Fortran that have compilers that study the code from beginning to end, perform many compiler-level optimizations, link intimately with the existing libraries on a speciﬁc platform, and then create an executable that is henceforth liberated from the compiler. As you may guess, the compiler’s access to the details of the underlying platform means that it can utilize optimizations that exploit chip-speciﬁc features and cache memory. Because the virtual machine abstracts away these details, it means that the Python language does not have programmable access to these kinds of optimizations. So, where is the balance between the ease of programming the virtual machine and these key numerical optimizations that are crucial for scientiﬁc work?

The balance comes from Python’s native ability to bind to compiled Fortran and C libraries. This means that you can send intensive computations to compiled libraries directly from the interpreter. This approach has two primary advantages. First, it give you the fun of programming in Python, with its expressive syntax and lack of visual clutter. This is a particular boon to scientists who typically want to use software as a tool as opposed to developing software as a product. The second advantage is that you can mix-and-match different compiled libraries from diverse research areas that were not otherwise designed to work together. This works because Python makes it easy to allocate and ﬁll memory in the interpreter, pass it as input to compiled libraries, and then retrieve the output back at the interpreter.

Moreover, Python provides a multiplatform solution for scientiﬁc codes. As an open-source project, Python itself is available anywhere you can build it, even though it typically comes standard nowadays, as part of many operating systems. This means that once you have written your code in Python, you can just transfer the script to another platform and run it, as long as the compiled libraries are also available there. What if the compiled libraries are absent? Building and conﬁguring compiled libraries across multiple systems used to be a painstaking job, but as scientiﬁc Python has matured, a wide range of libraries have now become available across all of the major platforms (i.e., Windows, MacOS, Linux, Unix) as prepackaged distributions.

Finally, scientiﬁc Python facilitates maintainability of scientiﬁc codes because Python syntax is clean, free of semi-colon litter and other visual distractions that makes code hard to read and easy to obfuscate. Python has many built-in testing, documentation, and development tools that ease maintenance. Scientiﬁc codes are usually written by scientists unschooled in software development, so having solid software development tools built into the language itself is a particular boon.

## 1.1 Installation and Setup

The easiest way to get started is to download the freely available Anaconda distribution provided by Continuum Analytics (continuum.io), which is available for all of the major platforms. On Linux, even though most of the toolchain is available via the built-in Linux package manager, it is still better to install the Anaconda distribution because it provides its own powerful package manager (i.e., conda) that can keep track of changes in the software dependencies of the packages that it supports. Note that if you do not have administrator privileges, there is also a corresponding miniconda distribution that does not require these privileges.

Regardless of your platform, we recommend Python version 2.7. Python 2.7 is the last of the Python 2.x series and guarantees backwards compatibility with legacy codes. Python 3.x makes no such guarantees. Although all of the key components of scientiﬁc Python are available in version 3.x, the safest bet is to stick with version 2.7. Alternatively, one compromise is to write in a hybrid dialect of Python that is the intersection of elements of versions 2.7 and 3.x. The six module enables this transition by providing utility functions for 2.5 and newer codes. There is also a Python 2.7 to 3.x converter available as the 2to3 module but it may be hard to debug or maintain the so-converted code; nonetheless, this might be a good option for small, self-contained libraries that do not require further development or maintenance.

You may have encountered other Python variants on the web, such as IronPython (Python implemented in C#) and Jython (Python implemented in Java). In this text, we focus on the C-implementation of Python (i.e., known as CPython), which is, by far, the most popular implementation. These other Python variants permit specialized, native interaction with libraries in C# or Java (respectively), which is still possible (but clunky) using the CPython. Even more Python variants exist that implement the low-level machinery of Python differently for various reasons, beyond interacting with native libraries in other languages. Most notable of these is Pypy that implements a just-in-time compiler (JIT) and other powerful optimizations that can substantially speed up pure Python codes. The downside of Pypy is that its coverage of some popular scientiﬁc modules (e.g., Matplotlib, Scipy) is limited or non-existent which means that you cannot use those modules in code meant for Pypy.

You may later want to use a Python module that is not maintained by Anaconda’s conda manager. Because Anaconda comes with the pip package manager, which is the main one used outside of scientiﬁc Python, you can simply do

Terminal> pip install package_name

and pipwillrunouttothewebanddownloadthepackageyouwantanditsdependencies and install them in the existing Anaconda directory tree. This works beautifully in the case where the package in question is pure-Python, without any system-speciﬁc dependencies. Otherwise, this can be a real nightmare, especially on Windows, which lacks freely available Fortran compilers. If the module in question is a C-library, one way to cope is to install the freely available Visual Studio Community Edition, which usually has enough to compile many C-codes. This platform dependency is the problem that conda was designed to solve by making the binary dependencies of the various platforms available instead of attempting to compile them. On a Windows system, if you installed Anaconda and registered it as the default Python installation (it asks during the install process), then you can use the high-quality Python wheel ﬁles on Christoph Gohlke’s laboratory site at the University of California, Irvine where he kindly makes a long list of scientiﬁc modules available. 1 Failing this, you can try the binstar.org site, which is a community-powered repository of modules that conda is capable of installing, but which are not formally supported by Anaconda. Note that binstar allows you to share scientiﬁc Python conﬁgurations with your remote colleagues using authentication so that you can be sure that you are downloading and running code from users you trust.

Again, if you are on Windows, and none of the above works, then you may want to consider installing a full virtual machine solution, as provided by VMWare’s PlayerorOracle’sVirtualBox(bothfreelyavailableunderliberalterms).Using either of these, you can set up a Linux machine running on top of Windows, which should cure these problems entirely! The great part of this approach is that you can share directories between the virtual machine and the Windows system so that you don’t have to maintain duplicate data ﬁles. Anaconda Linux images are also available on the cloud by IAAS providers like Amazon Web Services and Microsoft Azure. Note that for the vast majority of users, especially newcomers to Python, the Anaconda distribution should be more than enough on any platform. It is just worthhighlightingtheWindows-speciﬁcissuesandassociatedworkaroundsearlyon. Note that there are other well-maintained scientiﬁc Python Windows installers like WinPython and PythonXY. These provide the spyder integrated development environment, which is very Matlab-like environment for transitioning Matlab users.

1 Wheel ﬁles are a Python distribution format that you download and install using pip as in pip install file.whl. Christoph names ﬁles according to Python version (e.g., cp27 means Python 2.7) and chipset (e.g., amd32 vs. Intel win32).

## 1.2 Numpy

As we touched upon earlier, to use a compiled scientiﬁc library, the memory allocated in the Python interpreter must somehow reach this library as input. Furthermore, the output from these libraries must likewise return to the Python interpreter. This two-way exchange of memory is essentially the core function of the Numpy (numerical arrays in Python) module. Numpy is the de-facto standard for numerical arrays in Python. It arose as an effort by Travis Oliphant and others to unify the numerical arrays in Python. In this section, we provide an overview and some tips for using Numpy effectively, but for much more detail, Travis’ book [3] is a great place to start and is available for free online.

Numpy provides speciﬁcation of byte-sized arrays in Python. For example, below we create an array of three numbers, each of four-bytes long (32 bits at 8 bits per byte) as shown by the itemsize property. The ﬁrst line imports Numpy as np, which is the recommended convention. The next line creates an array of 32 bit ﬂoating point numbers. The itemize property shows the number of bytes per item.

>>> import numpy as np # recommended convention

>>> x = np.array([1,2,3],dtype=np.float32)

>>> x

array([ 1., 2., 3.], dtype=float32)

>>> x.itemsize 4

In addition to providing uniform containers for numbers, Numpy provides a comprehensive set of unary functions (i.e., ufuncs) that process arrays element-wise without additional looping semantics. Below, we show how to compute the element-wise sine using Numpy,

>>> np.sin(np.array([1,2,3],dtype=np.float32) ) array([ 0.84147096, 0.90929741, 0.14112 ], dtype=float32)

This computes the sine of the input array [1,2,3], using Numpy’s unary function, np.sin. There is another sine function in the built-in math module, but the Numpy version is faster because it does not require explicit looping (i.e., using a for loop) over each of the elements in the array. That looping happens in the compiled np.sin function itself. Otherwise, we would have to do looping explicitly as in the following:

>>> from math import sin

>>> [sin(i) for i in [1,2,3]] # list comprehension

[0.8414709848078965, 0.9092974268256817, 0.1411200080598672]

Numpy uses common-sense casting rules to resolve the output types. For example, if the inputs had been an integer-type, the output would still have been a ﬂoating point type. In this example, we provided a Numpy array as input to the sine function. We could have also used a plain Python list instead and Numpy would have built the intermediate Numpy array (e.g., np.sin([1,1,1])). The Numpy documentation provides a comprehensive (and very long) list of available ufuncs.

Numpy arrays come in many dimensions. For example, the following shows a two-dimensional 2 × 3 array constructed from two conforming Python lists.

>>> x=np.array([ [1,2,3],[4,5,6] ])

>>> x.shape (2, 3)

Note that Numpy is limited to 32 dimensions unless you build it for more. 2 Numpy arrays follow the usual Python slicing rules in multiple dimensions as shown below where the : colon character selects all elements along a particular axis.

>>> x=np.array([ [1,2,3],[4,5,6] ])

>>> x[:,0] # 0th column array([1, 4])

>>> x[:,1] # 1st column array([2, 5])

2 See arrayobject.h in the Numpy source code.

>>> x[0,:] # 0th row array([1, 2, 3])

>>> x[1,:] # 1st row array([4, 5, 6])

You can also select sub-sections of arrays by using slicing as shown below.

>>> x=np.array([ [1,2,3],[4,5,6] ])

>>> x

array([[1, 2, 3], [4, 5, 6]])

>>> x[:,1:] # all rows, 1st thru last column array([[2, 3], [5, 6]])

>>> x[:,::2] # all rows, every other column array([[1, 3], [4, 6]])

>>> x[:,::-1] # reverse order of columns array([[3, 2, 1], [6, 5, 4]])

1.2.1 Numpy Arrays and Memory

Some interpreted languages implicitly allocate memory. For example, in Matlab, you can extend a matrix by simply tacking on another dimension as in the following Matlab session:

>> x=ones(3,3) x = 1 1 1 1 1 1 1 1 1

>> x(:,4)=ones(3,1) % tack on extra dimension x = 1 1 1 1 1 1 1 1 1 1 1 1

>> size(x) ans = 3 4

This works because Matlab arrays use pass-by-value semantics so that slice operations actually copy parts of the array as needed. By contrast, Numpy uses pass-byreference semantics so that slice operations are views into the array without implicit copying. This is particularly helpful with large arrays that already strain available memory. In Numpy terminology, slicing creates views (no copying) and advanced indexing creates copies. Let’s start with advanced indexing.

If the indexing object (i.e., the item between the brackets) is a non-tuple sequence object, another Numpy array (of type integer or boolean), or a tuple with at least one sequence object or Numpy array, then indexing creates copies. For the above example,toaccomplishthesamearrayextensioninNumpy,youhavetodosomething like the following

>>> x = np.ones((3,3))

>>> x

array([[ 1., 1., 1.],

[ 1., 1., 1.], [ 1., 1., 1.]])

>>> x[:,[0,1,2,2]] # notice duplicated last dimension array([[ 1., 1., 1., 1.], [ 1., 1., 1., 1.], [ 1., 1., 1., 1.]])

>>> y=x[:,[0,1,2,2]] # same as above, but do assign it to y

Because of advanced indexing, the variable y has its own memory because the relevant parts of x were copied. To prove it, we assign a new element to x and see that y is not updated.

>>> x[0,0]=999 # change element in x

>>> x # changed array([[ 999., 1., 1.], [ 1., 1., 1.], [ 1., 1., 1.]])

>>> y # not changed! array([[ 1., 1., 1., 1.], [ 1., 1., 1., 1.], [ 1., 1., 1., 1.]])

However, if we start over and construct y by slicing (which makes it a view) as shown below, then the change we made does affect y because a view is just a window into the same memory.

>>> x = np.ones((3,3))

>>> y = x[:2,:2] # view of upper left piece

>>> x[0,0] = 999 # change value

>>> x

array([[ 999., 1., 1.], # see the change?

[ 1., 1., 1.], [ 1., 1., 1.]])

>>> y

array([[ 999., 1.], # changed y also!

[ 1., 1.]])

Note that if you want to explicitly force a copy without any indexing tricks, you can do y=x.copy(). The code below works through another example of advanced indexing versus slicing.

>>> x = np.arange(5) # create array

>>> x

array([0, 1, 2, 3, 4])

>>> y=x[[0,1,2]] # index by integer list to force copy

>>> y

array([0, 1, 2])

>>> z=x[:3] # slice creates view

>>> z # note y and z have same entries array([0, 1, 2])

>>> x[0]=999 # change element of x

>>> x

array([999, 1, 2, 3, 4])

>>> y # note y is unaffected, array([0, 1, 2])

>>> z # but z is (it’s a view). array([999, 1, 2])

In this example, y is a copy, not a view, because it was created using advanced indexing whereas z was created using slicing. Thus, even though y and z have the same entries, only z is affected by changes to x. Note that the flags.ownsdata property of Numpy arrays can help sort this out until you get used to it.

Manipulating memory using views is particularly powerful for signal and image processing algorithms that require overlapping fragments of memory. The following is an example of how to use advanced Numpy to create overlapping blocks that do not actually consume additional memory,

>>> from numpy.lib.stride_tricks import as_strided

>>> x = arange(16)

>>> y=as_strided(x,(7,4),(8,4)) # overlapped entries

>>> y array([[ 0, 1, 2, 3], [ 2, 3, 4, 5], [ 4, 5, 6, 7], [ 6, 7, 8, 9], [ 8, 9, 10, 11], [10, 11, 12, 13], [12, 13, 14, 15]])

The above code creates a range of integers and then overlaps the entries to create a 7 × 4 Numpy array. The ﬁnal argument in the as_strided function are the strides, which are the steps in bytes to move in the row and column dimensions, respectively. Thus, the resulting array steps four bytes in the column dimension and eight bytes in the row dimension. Because the integer elements in the Numpy array are four bytes, this is equivalent to moving by one element in the column dimension and by two elements in the row dimension. The second row in the Numpy array starts at eight bytes (two elements) from the ﬁrst entry (i.e., 2) and then proceeds by four bytes (by one element) in the column dimension (i.e., 2,3,4,5). The important part is that memory is re-used in the resulting 7 × 4 Numpy array. The code below demonstrates this by reassigning elements in the original x array. The changes show up in the y array because they point at the same allocated memory.

>>> x[::2]=99 # assign every other value

>>> x

array([99, 1, 99, 3, 99, 5, 99, 7, 99, 9, 99, 11, 99, 13, 99, 15])

>>> y # the changes appear because y is a view array([[99, 1, 99, 3], [99, 3, 99, 5], [99, 5, 99, 7], [99, 7, 99, 9], [99, 9, 99, 11], [99, 11, 99, 13], [99, 13, 99, 15]])

Bear in mind that as_strided does not check that you stay within memory block bounds. So, if the size of the target matrix is not ﬁlled by the available data, the remaining elements will come from whatever bytes are at that memory location. In other words, there is no default ﬁlling by zeros or other strategy that defends memory block bounds. One defense is to explicitly control the dimensions as in the following code, >>> n = 8 # number of elements

>>> x = arange(n) # create array

>>> k = 5 # desired number of rows

>>> y = as_strided(x,(k,n-k+1),(x.itemsize,)*2)

>>> y array([[0, 1, 2, 3], [1, 2, 3, 4], [2, 3, 4, 5], [3, 4, 5, 6], [4, 5, 6, 7]])

1.2.2 Numpy Matrices

Matrices in Numpy are similar to Numpy arrays but they can only have two dimensions.Theyimplementrow-columnmatrixmultiplicationasopposedtoelement-wise multiplication. If you have two matrices you want to multiply, you can either create them directly or convert them from Numpy arrays. For example, the following shows how to create two matrices and multiply them.

>>> import numpy as np

>>> A=np.matrix([[1,2,3],[4,5,6],[7,8,9]])

>>> x=np.matrix([[1],[0],[0]])

>>> A*x

matrix([[1],

[4],

[7]])

This can also be done using arrays as shown below,

>>> A=np.array([[1,2,3],[4,5,6],[7,8,9]])

>>> x=np.array([[1],[0],[0]])

>>> A.dot(x) array([[1],

[4],

[7]])

Numpy arrays support elementwise multiplication, not row-column multiplication. You must use Numpy matrices for this kind of multiplication unless use the inner product np.dot, which also works in multiple dimensions (see np.tensordot for more general dot products).

It is unnecessary to cast everything to matrices for multiplication. In the next example, everything until last line is a Numpy array and thereafter we cast the array as a matrix with np.matrix which then uses row-column multiplication. Note that it is unnecessary to cast the x variable as a matrix because the left-to-right order of the evaluation takes care of that automatically. If we need to use A as a matrix elsewhere in the code then we should bind it to another variable instead of re-casting it every time. If you ﬁnd yourself casting back and forth for large arrays, passing the copy=False ﬂag to matrix avoids the expense of making a copy.

>>> A=np.ones((3,3))

>>> type(A) # array not matrix <type ’numpy.ndarray’>

>>> x=np.ones((3,1)) # array not matrix

>>> A*x
array([[ 1., 1., 1.], [ 1., 1., 1.], [ 1., 1., 1.]]) >>> np.matrix(A)*x # row-column multiplication matrix([[ 3.], [ 3.], [ 3.]])

1.2.3 Numpy Broadcasting

Numpy broadcasting is a powerful way to make implicit multidimensional grids for expressions. It is probably the single most powerful feature of Numpy and the most difﬁcult to grasp. Proceeding by example, consider the vertices of a two-dimensional unit square as shown below,

>>> X,Y=np.meshgrid(np.arange(2),np.arange(2))

>>> X

array([[0, 1], [0, 1]])

>>> Y

array([[0, 0], [1, 1]])

Numpy’s meshgrid creates two-dimensional grids. The X and Y arrays have corresponding entries match the coordinates of the vertices of the unit square (e.g., (0, 0), (0, 1), (1, 0), (1, 1)). To add the x and y-coordinates, we could use X and Y as in X+Y shown below, The output is the sum of the vertex coordinates of the unit square.

>>> X+Y array([[0, 1], [1, 2]])

Because the two arrays have compatible shapes, they can be added together elementwise. It turns out we can skip a step here and not bother with meshgrid to implicitly obtain the vertex coordinates by using broadcasting as shown below

>>> x = np.array([0,1])

>>> y = np.array([0,1])

>>> x

array([0, 1])

>>> y

array([0, 1])

>>> x + y[:,None] # add broadcast dimension array([[0, 1], [1, 2]])

>>> X+Y

array([[0, 1], [1, 2]])

On line 7 the None Python singleton tells Numpy to make copies of y along this dimension to create a conformable calculation. Note that np.newaxis can be used instead of None to be more explicit. The following lines show that we obtain the same output as when we used the X+Y Numpy arrays. Note that without broadcasting x+y=array([0, 2]) which is not what we are trying to compute. Let’s continue with a more complicated example where we have differing array shapes.

>>> x = np.array([0,1])

>>> y = np.array([0,1,2])

>>> X,Y = np.meshgrid(x,y)

>>> X

array([[0, 1], # duplicate by row [0, 1], [0, 1]])

>>> Y

array([[0, 0], # duplicate by column [1, 1], [2, 2]])

>>> X+Y

array([[0, 1],

[1, 2], [2, 3]])

>>> x+y[:,None] # same as with meshgrid array([[0, 1], [1, 2], [2, 3]])

In this example, the array shapes are different, so the addition of x and y is not possible without Numpy broadcasting. The last line shows that broadcasting generates the same output as using the compatible array generated by meshgrid. This shows that broadcasting works with different array shapes. For the sake of comparison, on line 3, meshgrid creates two conformable arrays, X and Y. On the last line, x+y[:,None] produces the same output as X+Y without the meshgrid. We can also put the None dimension on the x array as x[:,None]+y which would give the transpose of the result.

Broadcasting works in multiple dimensions also. The output shown has shape (4,3,2). On the last line, the x+y[:,None] produces a two-dimensional array which is then broadcast against z[:,None,None], which duplicates itself along the two added dimensions to accommodate the two-dimensional result on its left (i.e., x + y[:,None]). The caveat about broadcasting is that it can potentially create large, memory-consuming, intermediate arrays. There are methods for controlling this by re-using previously allocated memory but that is beyond our scope here. Formulas in physics that evaluate functions on the vertices of high dimensional grids are great use-cases for broadcasting.

>>> x = np.array([0,1])

>>> y = np.array([0,1,2])

>>> z = np.array([0,1,2,3])

>>> x+y[:,None]+z[:,None,None] array([[[0, 1], [1, 2], [2, 3]], [[1, 2], [2, 3], [3, 4]], [[2, 3], [3, 4], [4, 5]], [[3, 4], [4, 5], [5, 6]]])

1.2.4 Numpy Masked Arrays

Numpy provides a powerful method to temporarily hide array elements without changing the shape of the array itself,

>>> from numpy import ma # import masked arrays

>>> x = np.arange(10)

>>> y = ma.masked_array(x, x<5)

>>> print y

[-- -- -- -- -- 5 6 7 8 9]

>>> print y.shape (10,)

Note that the elements in the array for which the logical condition (x < 5) is true are masked, but the size of the array remains the same. This is particularly useful in plotting categorical data, where you may only want those values that correspond to a given category for part of the plot. Another common use is for image processing, wherein parts of the image may need to be excluded from subsequent processing. Note that creating a masked array does not force an implicit copy operation unless copy=True argument is used. For example, changing an element in x does change the corresponding element in y, even though y is a masked array,

>>> x[-1] = 99 # change this

>>> print x

>>> print y # masked array changed! [ 0 1 2 3 4 5 6 7 8 99] [-- -- -- -- -- 5 6 7 8 99]

1.2.5 Numpy Optimizations and Prospectus

The scientiﬁc Python community continues to push the frontier of scientiﬁc computing. Several important extensions to Numpy are under active development. First, Numba is a compiler that generates optimized machine code from pure Python code using the LLVM compiler infrastructure. LLVM started as a research project at the University of Illinois to provide a target-independent compilation strategy for arbitrary programming languages and is now a well-established technology. The combination of LLVM and Python via Numba means that accelerating a block of Python code can be as easy as putting a @numba.jit decorator above the function deﬁnition, but this doesn’t work for all situations. Numba can target general graphics processing units (GPGPUs) also.

Blaze is considered the next generation of Numpy and generalizes the semantics of Numpy for very large data sets that exist on a variety of backend ﬁlesystems. This means that Blaze is designed to handle out-of-core (i.e., too big to ﬁt in a single workstation’s RAM) data manipulations and computations using the familiar operations from Numpy. Further, Blaze offers tight integration with Pandas (see Sect.1.6) dataframes. Roughly speaking, Blaze understands how to unpack Python expressions and translate them for a variety of distributed backend data services upon which the computing will actually happen (i.e., using blaze.compute).

This means that Blaze separates the expression of the computation from the particular implementation on a given backend.

Building on his amazing work on PyTables, Francesc Alted has been working on the bcolz module which is a compressed columnar data container. Also motivated by out-of-core data and computing, bcolz tries to relieve the stress of the memory subsystem by compressing data in memory and then interleaving computations on the compressed data in an intelligent way. This approach takes advantage of emerging architectures that have more cores and wider vector units.

1.3 Matplotlib

Matplotlib is the primary visualization tool for scientiﬁc graphics in Python. Like all great open-source projects, it originated to satisfy a personal need. At the time of its inception, John Hunter primarily used Matlab for scientiﬁc visualization, but as he began to integrate data from disparate sources using Python, he realized he needed a Python solution for visualization, so he single-handedly wrote Matplotlib. Since those early years, Matplotlib has displaced the other competing methods for two-dimensional scientiﬁc visualization and today is a very actively maintained project, even without John Hunter, who sadly passed away in 2012.

John had a few basic requirements for Matplotlib:

• Plots should look publication quality with beautiful text.

A • Plots should output Postscript for inclusion within L T E X documents and publication quality printing.

• Plots should be embeddable in a Graphical User Interface (GUI) for application development.

• The code should be mostly Python to allow for users to become developers.

• Plots should be easy to make with just a few lines of code for simple graphs.

Each of these requirements has been completely satisﬁed and Matplotlib’s capabilities have grown far beyond these requirements. In the beginning, to ease the transition from Matlab to Python, many of the Matplotlib functions were closely named after the corresponding Matlab commands. The community has moved away from this style and, even though you will still ﬁnd the old Matlab-esque style used in the on-line Matplotlib documentation.

The following shows the quickest way to draw a plot using Matplotlib and the plain Python interpreter. Later, we’ll see how to do this even faster using IPython. The ﬁrst line imports the requisite module as plt which is the recommended convention. The next line plots a sequence of numbers generated using Python’s range function. Notetheoutputlistcontainsa Line2Dobject.Thisisanartist inMatplotlibparlance. Finally, the plt.show() function draws the plot in a GUI ﬁgure window.

Fig. 1.1 The Matplotlib ﬁgure window. The icons on the bottom allow some limited plot-editing tools

>>> import matplotlib.pyplot as plt

>>> plt.plot(range(10))

[<matplotlib.lines.Line2D object at 0x00CB9770>]

>>> plt.show() # unnecessary in IPython (discussed later)

If you try this in your own plain Python interpreter (and you should), you will see that you cannot type in anything further in the interpreter until the ﬁgure window (i.e., something like Fig.1.1) is closed. This is because the plt.show() function preoccupies the interpreter with the controls in the GUI and blocks further interaction. As we discuss below, IPython provides ways to get around this blocking so you can simultaneously interact with the interpreter and the ﬁgure window.3 

As shown in Fig.1.1, the plot function returns a list containing the Line2D object. More complicated plots yield larger lists ﬁlled with artists. The suggestion is that artists draw on the canvas contained in the Matplotlib ﬁgure. The ﬁnal line is the plt.show function that provokes the embedded artists to render on the Matplotlib canvas. The reason this is a separate function is that plots may have dozens of complicated artists and rendering may be a time-consuming task to only

3 You can also do this in the plain Python interpreter by doing import matplotlib; matplotlib.interactive(True).

be undertaken at the end, when all the artists have been mustered. Matplotlib supports plotting images, contours, and many others that we cover in detail in the following chapters.

Even though this is the quickest way to draw a plot in Matplotlib, it is not recommended because there are no handles to the intermediate products of the plot such as the plot’s axis. While this is okay for a simple plot like this, later on we will see how to construct complicated plots using the recommended method. There is a close working relationship between Numpy and Matplotlib and you can load Matplotlib’s plotting functions and Numpy’s functions simultaneously using pylab as from matplotlib.pylab import *. Although importing everything this way as a standard practice is not recommended because of namespace pollution.

One of the best ways to get started with Matplotlib is to browse the extensive online gallery of plots on the main Matplotlib site. Each plot comes with corresponding source code that you can use as a starting point for your own plots. In Sect.1.4, we discuss special magic commands that make this particularly easy. The annual John Hunter: Excellence in Plotting Contest provides fantastic, compelling examples of scientiﬁc visualizations that are possible using Matplotlib.

1.3.1 Alternatives to Matplotlib

Even though Matplotlib is unbeatable for script-based plotting, there are some alternatives for specialized scientiﬁc graphics that may be of interest.

Chaco is part of the Enthought Tool-Suite (ETS) and implements many realtime data visualization concepts and corresponding widgets. It is available on all of the major platforms and is also actively maintained and well-documented. Chaco is geared towards GUI application development, rather than script-based data visualization. It depends on the Traits package, which is also available in ETS and in the Enthought Canopy. If you don’t want to use Canopy, then you have to build Chaco and its dependencies separately. On Linux, this should be straight-forward, but potentially a nightmare on Windows if not for Christoph Gohlke’s installers or Anaconda’s conda package manager.

If you require real-time data display and tools for volumetric data rendering and complicated 3D meshes with isosurfaces, then PyQtGraph is an option. PyQtGraph is a pure-Python graphics and GUI library that depends on Python bindings for the Qt GUI library (i.e., PySide or PyQt4) and Numpy. This means that the PyQtGraph relies on these other libraries (especially Qt’s GraphicsView framework) for the heavy-duty numbercrunching and rendering. This package is actively maintained, but is still pretty new, with good (but not comprehensive) documentation. You also need to grasp a few Qt-GUI development concepts to use this effectively. Mayavi is another Enthought-supported 3D visualization package that sits on VTK (open-source C++ library for 3D visualization). Like Chaco, it is a toolkit for scientiﬁc GUI development as opposed to script-based plotting. To use it effectively, you need to already know (or be willing to learn) about graphics pipelines. This package is actively supported and well-documented.

An alternative that comes from the R community is ggplot which is a Python port of the ggplot2 package that is fundamental to statistical graphics in R. From the Python standpoint, the main advantage of ggplot is the tight integration with the Pandas dataframe, which makes it easy to draw beautifully formatted statistical graphs. The downside of this package is that it applies un-Pythonic semantics based on the Grammer of Graphics [4], which is nonetheless a well-thought-out method for articulating complicated graphs. Of course, because there are two-way bridges between Python and R via the R2Py module (among others), it is workable to send Numpy arrays to R for native ggplot2 rendering and then retrieve the so-computed graphic back into Python. This is a workﬂow that is lubricated by the IPython Notebook via the rmagic extension. Thus, it is quite possible to get the best of both worlds via the IPython Notebook and this kind of multi-language workﬂow is quite common in data analysis communities.

1.3.2 Extensions to Matplotlib

Initially, to encourage adoption of Matplotlib from Matlab, many of the graphical sensibilities were adopted from Matlab to preserve the look and feel for transitioning users. Modern sensibilities and prettier default plots are possible because Matplotlib provides the ability to drill down and tweak just about every element on the canvas. However, this can be tedious to do and several alternatives offer relief. For statistical plots, the ﬁrst place to look is the seaborn module that includes a vast array of beautifully formatted plots including violin plots, kernel density plots, and bivariate histograms. The seaborn gallery includes samples of available plots and the corresponding code that generates them. Note that importing seaborn hijacks the default settings for all plots, so you have to coordinate this if you only want to use seaborn for some (not all) of your visualizations in a given session. Note that you can ﬁnd the defaults for Matplotlib in the matplotlib.rcParams dictionary.

The prettyplotlib module, like seaborn, provides an intelligent default color palate based on Cynthia Brewer’s work on color perception (c.f. colorbrewer2.org). Unfortunately, this work is no longer supported by the author, but still provides a great set of plotting tools and designs for building beautiful data visualizations.

1.4 IPython

IPython [5] originated as a way to enhance Python’s basic interpreter for smooth interactive scientiﬁc development. In the early days, the most important enhancement was tab-completion for dynamic introspection of workspace variables. For example, you can start IPython at the commandline by typing ipython and then you should see something like the following in your terminal:

Python 2.7.11 |Continuum Analytics, Inc.| (default, Dec 7 2015, 14:00 Type "copyright", "credits" or "license" for more information.

IPython 4.0.0 -- An enhanced Interactive Python.

? -> Introduction and overview of IPython’s features.

help -> Python’s own help system.

object? -> Details about ’object’, use ’object??’ for extra details.

In [1]:

Next, creating a string as shown and hitting the TAB key after the dot character initiates the introspection, showing all the functions and attributes of the string object in x.

In [1]: x = ’this is a string’

In [2]: x.<TAB> x.capitalize x.format x.center x.index x.count x.isalnum x.decode x.isalpha x.encode x.isdigit x.endswith x.islower x.expandtabs x.isspace x.find x.istitle

x.isupper x.join x.ljust x.lower x.lstrip x.partition x.replace x.rfind

x.rindex x.strip x.rjust x.swapcase x.rpartition x.title x.rsplit x.translate x.rstrip x.upper x.split x.zfill x.splitlines x.startswith

To get help about any of these, you simply add the ? character at the end as shown below,

In [2]: x.center?

Type: builtin_function_or_method String Form:<built-in method center of str object at 0x03193390> Docstring:

S.center(width[, fillchar]) -> string

Return S centered in a string of length width. Padding is done using the specified fill character (default is a space)

and IPython provides the built-in help documentation. Note that you can also get this documentationwith help(x.center)whichworksintheplainPythoninterpreter as well.

The combination of dynamic tab-based introspection and quick interactive help accelerates development because you can keep your eyes and ﬁngers in one place as you work. This was the original IPython experience, but IPython has since grown into a complete framework for delivering a rich scientiﬁc computing workﬂow that retains and enhances these fundamental features.

1.4.1 IPython Notebook

As you may have noticed investigating Python on the web, most Python users are web-developers, not scientiﬁc programmers, meaning that the Python stack is very well developed for web technologies. The genius of the IPython development team was to leverage these technologies for scientiﬁc computing by embedding IPython in modern web-browsers. In fact, this strategy has been so successful that IPython has moved into other languages beyond Python such as Julia and R as the Jupyter project.4 

You can start the IPython Notebook with the following commandline: ’jupyter notebook’. After starting the notebook, you should see something like the following in the terminal,

[W 10:26:55.332 NotebookApp] ipywidgets package not installed. Widgets [I 10:26:55.348 NotebookApp] Serving notebooks from local directory: D:\ [I 10:26:55.351 NotebookApp] 0 active kernels [I 10:26:55.351 NotebookApp] The IPython Notebook is running at: http:// [I 10:26:55.351 NotebookApp] Use Control-C to stop this server and shut

The ﬁrst line reveals where IPython looks for default settings. The next line shows where it looks for documents in the IPython Notebook format. The third line shows that the IPython Notebook started a web-server on the local machine (i.e., 127.0.0.1) on port number 8888. This is the address your browser needs to connect to the IPython session although your default browser should have opened automatically to this address. The port number and other conﬁguration options are available either on the commandline or in the proﬁle ﬁle shown in the ﬁrst line. If you are on a Windows platform and you do not get this far, then the Window’s ﬁrewall is probably blocking the port. For additonal conﬁguration help, see the main IPython site (www.ipython.org) or e-mail the very responsive IPython mailing list (ipython-dev@scipy.org).

When IPython starts, it initiates many small Python processes that use the blazing-fast ZeroMQ message passing framework for interprocess-communication, along with the web-sockets protocol for back-and-forth communication with the browser. To start IPython and get around your default browser, you can use the additonal —no-browser ﬂag and then manually type in the local host address http://127.0.0.1:8888 into your favorite browser to get started. Once all that is settled, you should see something like the following Fig.1.2.

You can create a new document by clicking the New Notebook button shown in Fig.1.2.Then,youshouldseesomethinglikeFig.1.3.TostartusingtheIPythonNotebook, you just start typing code in the shaded textbox and then hit SHIFT+ENTER to execute the code in that IPython cell. Figure1.4 shows the dynamic introspection in the pulldown menu when you type the TAB key after the x.. Context-based help is also available as before by using the ? sufﬁx which opens a help panel at the bottom of the browser window. There are many amazing features including the ability to

4 Because we are primarily focused on Python in this text we will continue to refer to IPython and the IPython Notebook instead of to the more general Jupyter project. At the time of this writing, the re-factorization of IPython into Jupyter has not been completed.

share notebooks between different users and to run IPython Notebooks in the Amazon cloud, but these features go beyond our scope here. Check the ipython.org website or peek at the mailing list for the lastest work on these fronts.

The IPython Notebook supports high-quality mathematical typesetting using A MathJaX,whichisaJavaScriptimplementationofmostofL T E X,aswellasvideoand other rich content. The concept of consolidating mathematical algorithm descriptions and the code that implements those algorithms into a shareable document is more important than all of these amazing features. There is no understating the importance of this in practice because the algorithm documentation (if it exists) is usually in one format and completely separate from the code that implements it. This common practice leads to un-synchronized documentation and code that renders one or the other useless. The IPython Notebook solves this problem by putting everything into a living shareable document based upon open standards and freely available software. IPython Notebooks can even be saved as static HTML documents for those without Python!

Finally, IPython provides a large set of magic commands for creating macros, proﬁling, debugging, and viewing codes. A full list of these can be found by typing in %lsmagic in IPython. Help on any of these is available using the ? character sufﬁx. Some frequently used commands include the %cd command that changes the current working directory, the %ls command that lists the ﬁles in the current directory, and the %hist command that shows the history of previous commands (including optional searching). The most important of these for new users is probably the %loadpy command that can load scripts from the local disk or from the web. Using this to explore the Matplotlib gallery is a great way to experiment with and re-use the plots there.

1.5 Scipy

Scipy was the ﬁrst consolidated module for a wide range of compiled libraries, all based on Numpy arrays. Scipy includes numerous special functions (e.g., Airy, Bessel, elliptical) as well as powerful numerical quadrature routines via the QUADPACK Fortran library (see scipy.integrate), where you will also ﬁnd other quadrature methods. Note that some of the same functions appear in multiple places within Scipy itself as well as in Numpy. Additionally, Scipy provides access to the ODEPACK library for solving differential equations. Lots of statistical functions, including random number generators, and a wide variety of probability distributions are included in the scipy.stats module. Interfaces to the Fortran MINPACK optimization library are provided via scipy.optimize. These include methods for root-ﬁnding, minimization and maximization problems, with and without higher-order derivatives. Methods for interpolation are provided in the scipy.interpolate module via the FITPACK Fortran package. Note that some of the modules are so big that you do not get all of them with import scipy because that would take too long to load. You may have to load some of these packages individually as import scipy.interpolate, for example.

As we discussed, the Scipy module is already packed with an extensive list of scientiﬁc codes. For that reason, the scikits modules were originally established as a way to stage candidates that could eventually make it into the already stuffed Scipy module, but it turns out that many of these modules became so successful on their own that they will never be integrated into Scipy proper. Some examples include sklearn for machine learning and scikit-image for image processing.

1.6 Pandas

Pandas [6] is a powerful module that is optimized on top of Numpy and provides a set of data structures particularly suited to time-series and spreadsheet-style data analysis (think of pivot tables in Excel). If you are familiar with the R statistical package, then you can think of Pandas as providing a Numpy-powered dataframe for Python.

1.6.1 Series

There are two primary data structures in Pandas. The ﬁrst is the Series object which combines an index and corresponding data values.

>>> import pandas as pd # recommended convention

>>> x=pd.Series(index = range(5),data=[1,3,9,11,12])

>>> x 0 1 2 3 4

1

3

9

11

12

The main thing to keep in mind with Pandas is that these data structures were originally designed to work with time-series data. In that case, the index in the data structures corresponds to a sequence of ordered time-stamps. In the general case, the index must be a sort-able array-like entity. For example,

>>> x=pd.Series(index = [’a’,’b’,’d’,’z’,’z’],data=[1,3,9,11,12])

>>> x

Note the duplicated z entries in the index. We can get at the entries in the Series in a number of ways. First, we can used the dot notation to select as in the following:

>>> x.a 1

>>> x.z z 11 z 12

We can also use the indexed-position of the entries with iloc as in the following:

>>> x.iloc[:3] a 1 b 3 d 9

which uses the same slicing syntax as Numpy arrays. You can also slice across the index, even if it is not numeric with loc as in the following:

>>> x.loc[’a’:’d’] a 1 b 3 d 9

which you can get directly from the usual slicing notation:

>>> x[’a’:’d’] a 1 b 3 d 9

Note that, unlike Python, slicing this way includes the endpoints. While that is very interesting, the main power of Pandas comes from its power to aggregate and group data. In the following, we build a more interesting Series object,

>>> x = pd.Series(range(5),[1,2,11,9,10])

1

2

11

9

10

0

1

2

3

4

and then group it in the following:

>>> grp=x.groupby(lambda i:i%2) # odd or even

>>> grp.get_group(0) # even group 2 1 10 4

>>> grp.get_group(1) # odd group 1 0 11 2 9 3

The ﬁrst line groups the elements of the Series object by whether or not the index is even or odd. The lambda function returns 0 or 1 depending on whether or not the corresponding index is even or odd, respectively. The next line shows the 0 (even) group and then the one after shows the 1 (odd) group. Now, that we have separate groups, we can perform a wide-variety of summarizations on the group. You can think of these as reducing each group into a single value. For example, in the following, we get the maximum value of each group:

>>> grp.max() # max in each group 0 4 1 3

Note that the operation above returns another Series object with an index corresponding to the [0,1] elements.

1.6.2 Dataframe

The Pandas DataFrame is an encapsulation of the Series that extends to twodimensions. One way to create a DataFrame is with dictionaries as in the following:

>>> df = pd.DataFrame({’col1’: [1,3,11,2], ’col2’: [9,23,0,2]}) col1 col2 0 1 9 1 3 23 2 11 0 3 2 2

Note that the keys in the input dictionary are now the column-headings (labels) of the DataFrame, with each corresponding column matching the list of corresponding values from the dictionary. Like the Series object, the DataFrame also has in index, which is the [0,1,2,3] column on the far-left. We can extract elements from each column using the iloc method as discussed earlier as shown below:

>>> df.iloc[:2,:2] # get section col1 col2 0 1 9 1 3 23

or by directly slicing or by using the dot notation as shown below:

>>> df[’col1’] # indexing 0 1 1 3 2 11 3 2

>>> df.col1 # use dot notation 0 1 1 3 2 11 3 2

Subsequent operations on the DataFrame preserve its column-wise structure as in the following:

>>> df.sum() col1 17 col2 34

where each column was totaled. Grouping and aggregating with the dataframe is even more powerful than with Series. Let’s construct the following dataframe, In the above dataframe, note that the col1 column has only two entries. We can group the data using this column as in the following:

>>> grp=df.groupby(’col1’)

>>> grp.get_group(0) col1 col2 2 0 3 3 0 4

>>> grp.get_group(1) col1 col2 0 1 1 1 1 2

Note that each group corresponds to entries for which col1 was either of its two values. Now that we have grouped on col1, as with the Series object, we can also functionally summarize each of the groups as in the following:

>>> grp.sum() col2 col1 0 7 1 3

where the sum is applied across each of the Dataframes present in each group. Note that the index of the output above is each of the values in the original col1.

The Dataframe can compute new columns based on existing columns using the eval method as shown below:

>>> df[’sum_col’]=df.eval(’col1+col2’)

>>> df col1 col2 sum_col 0 1 1 2 1 1 2 3 2 0 3 3 3 0 4 4

Note that you can assign the output to a new column to the Dataframe as shown.5  We can group by multiple columns as shown below:

>>> grp=df.groupby([’sum_col’,’col1’])

Doing the sum operation on each group gives the following:

>>> res=grp.sum()

>>> res col2 sum_col col1 2 1 1 3 0 3 1 2 4 0 4

5 Note this kind of on-the-ﬂy memory extension is not possible in regular Numpy. For example, x = np.array([1,2]); x[3]=3 generates an error.

This output is much more complicated than anything we have seen so far, so let’s carefully walk through it. Below the headers, the ﬁrst row 2 1 1 indicates that for sum_col=2 and for all values of col1 (namely, just the value 1), the value of col2 is 1. For the next row, the same pattern applies except that for sum_col=3, there are now two values for col1, namely 0 and 1, which each have their corresponding two values for the sum operation in col2. This layered display is one way to look at the result. Note that the layers above are not uniform. Alternatively, we can unstack this result to obtain the following tabular view of the previous result:

>>> res.unstack() col2 col1 0 1 sum_col 2 NaN 1 3 3 2 4 4 NaN

The NaN values indicate positions in the table where there is no entry. For example, for the pair (sum_col=2,col2=0), there is no corresponding value in the Dataframe, as you may verify by looking at the penultimate code block. There is also no entry corresponding to the (sum_col=4,col2=1) pair. Thus, this shows that the original presentation in the penultimate code block is the same as this one, just without the above-mentioned missing entries indicated by NaN.

We have barely scratched the surface of what Pandas is capable of and we have completely ignored its powerful features for managing dates and times. The text by Mckinney [6] is a very complete and happily readable introduction to Pandas. The online documentation and tutorials at the main Pandas site are also great for diving deeper into Pandas.

1.7 Sympy

Sympy [7] is the main computer algebra module in Python. It is a pure-Python package with no platform-dependencies. With the help of multiple Google Summer of Code sponsorships, it has grown into a powerful computer algebra system with many collateral projects that make it faster and integrate it tighter with Numpy and IPython (among others). Sympy’s on-line tutorial is excellent and allows interacting with its embedded code samples in the browser by running the code on the Google App Engine behind the scenes. This provides an excellent way to interact and experiment with Sympy.

If you ﬁnd Sympy too slow or need algorithms that it does not implement, then SAGE is your next stop. The SAGE project is a consolidation of over 70 of the best open source packages for computer algebra and related computation. Although Sympy and SAGE share code freely between them, SAGE is a specialized build of the Python kernel to facilitate deep integration with the underlying libraries. Thus, it is not a pure-Python solution for computer algebra (i.e., not as portable) and it is a proper superset of Python with its own extended syntax. The choice between SAGE and Sympy really depends on whether or not you intend primarily work in SAGE or just need occasional computer algebra support in your existing Python code.

An important new development regarding SAGE is the freely available SAGE Cloud (https://cloud.sagemath.com/), sponsored by University of Washington that allows you to use SAGE entirely in the browser with no additional setup. Both SAGE and Sympy offer tight integration with the IPython Notebook for mathematical typesetting in the browser using MathJaX.

To get started with Sympy, you must import the module as usual,

>>> import sympy as S # might take awhile

which may take a bit because it is a big package. The next step is to create a Sympy variable as in the following:

>>> x = S.symbols(’x’)

Now we can manipulate this using Sympy functions and Python logic as shown below:

>>> p=sum(x**i for i in range(3)) # 2nd order polynomial

>>> p

x**2 + x + 1

Now, we can ﬁnd the roots of this polynomial using Sympy functions,

>>> S.solve(p) # solves p == 0 [-1/2 - sqrt(3)*I/2, -1/2 + sqrt(3)*I/2]

There is also a sympy.roots function that provides the same output but as a dictionary.

>>> S.roots(p) {-1/2 - sqrt(3)*I/2: 1, -1/2 + sqrt(3)*I/2: 1}

We can also have more than one symbolic element in any expression as in the following:

>>> from sympy.abc import a,b,c

>>> p = a* x**2 + b*x + c

# quick way to get common symbols

>>> S.solve(p,x) # specific solving for x-variable

[(-b + sqrt(-4*a*c + b**2))/(2*a), -(b + sqrt(-4*a*c + b**2))/(2*a)]

which is the usual quadratic formula for roots. Sympy also provides many mathematical functions designed to work with Sympy variables. For example,

>>> S.exp(S.I*a) #using Sympy exponential

We can expand this using expand_complex to obtain the following:

>>> S.expand_complex(S.exp(S.I*a)) I*exp(-im(a))*sin(re(a)) + exp(-im(a))*cos(re(a))

which gives us Euler’s formula for the complex exponential. Note that Sympy does not know whether or not a is itself a complex number. We can ﬁx this by making that fact part of the construction of a as in the following:

>>> a = S.symbols(’a’,real=True)

>>> S.expand_complex(S.exp(S.I*a)) I*sin(a) + cos(a)

Note the much simpler output this time because we have forced the additional condition on a.

A powerful way to use Sympy is to construct complicated expressions that you can later evaluate using Numpy via the lambdify method. For example,

>>> y = S.tan(x) * x + x**2

>>> yf= S.lambdify(x,y,’numpy’)

>>> y.subs(x,.1) # evaluated using Sympy

0.0200334672085451

>>> yf(.1) # evaluated using Numpy

0.0200334672085451

After creating the Numpy function with lambdify, you can use Numpy arrays as input as shown:

>>> yf(np.arange(3)) # input is Numpy array array([ 0. , 2.55740772, -0.37007973])

>>> [ y.subs(x,i).evalf() for i in range(3) ] # need extra work for Sympy [0, 2.55740772465490, -0.370079726523038]

We can get the same output using Sympy, but that requires the extra programming logic shown to do the vectorizing that Numpy performs natively.

Once again, we have merely scratched the surface of what Sympy is capable of and the on-line interactive tutorial is the best place to learn more. Sympy also allows A automatic mathematical typesetting within the IPython Notebook using L T E X so the so-constructed notebooks look almost publication-ready (see sympy.latex) and can be made so with the ipython nbconvert command. This makes it easier to jump the cognitive gap between the Python code and the symbology of traditional mathematics.

1.8 Interfacing with Compiled Libraries

As we have discussed, Python for scientiﬁc computing really consists of gluing together different scientiﬁc libraries written in a compiled language like C or Fortran. Ultimately, you may want to use libraries not available with existing Python bindings. There are many, many options for doing this. The most direct way is to use the built-in ctypes module which provides tools for providing input/output pointers to the library’s functions just as if you were calling them from a compiled language. This means that you have to know the function signatures in the library exactly—how many bytes for each input and how many bytes for the output. You are responsible for building the inputs exactly the way the library expects and collecting the resulting outputs. Even though this seems tedious, Python bindings for vast libraries have been built this way.

If you want an easier way, then SWIG is an automatic wrapper generating tool that can provide bindings to a long list of languages, not just Python; so if you need bindings for multiple languages, then this is your best and only option. Using SWIG consists of writing an interface ﬁle so that the compiled Python dynamically linked library (Python PYD) can be readily imported into the Python interpreter. Huge and complex libraries like Trilinos (Sandia National Labs) have been interfaced to Python using SWIG, so it is a well-tested option. SWIG also supports Numpy arrays.

However, the SWIG model assumes that you want to continue developing primarily in C/Fortran and you are hooking into Python for usability or other reasons. On the other hand, if you start developing algorithms in Python and then want to speed them up, then Cython is an excellent option because it provides a mixed language that allows you to have both C-language and Python code intermixed. Like SWIG, you have to write additional ﬁles in this hybrid Python/C dialect to have Cython generate the C-code that you will ultimately compile. The best part of Cython is the proﬁler that can generate an HTML report showing where the code is slow and could beneﬁt from translation to Cython. The IPython Notebook integrates nicely with Cython via its %cython magic command. This means you can write Cython code in a cell in IPython Notebook and the notebook will handle all of the tedious details like setting up the intermediate ﬁles to actually compile the Cython extension. Cython also supports Numpy arrays.

Cython and SWIG are just two of the ways to create Python bindings for your favorite compiled libraries. Other notable (but less popular) options include FWrap, f2py, CFFI, and weave. It is also possible to use Python’s own API directly, but this is a difﬁcult undertaking that is hard to justify given the existence of so many well-developed alternatives.

1.9 Integrated Development Environments

For those who prefer Integrated Development Environments (IDEs), there is a lot to choose from. The most comprehensive is Enthought Canopy, which includes a rich, syntax-highlighted editor, integrated help, debugger, and even integrated training. If you are already familiar with Eclipse from other projects, or do mixedlanguage programming, then there is a Python plugin called PyDev that contains all usual features from Eclipse with a Python debugger. Wingware provides an affordable professional-level IDE with multi-project management support and unusually clairvoyant code-completion that works even in debug-mode. Another favorite is PyCharm, which also supports multiple languages and is particularly popular among Python web-developers because it provides powerful templates for popular web frameworks like Django. NinjaIDE is relatively new, but has quickly developed a strong following among Python newcomers because of its beautiful interface and easy-to-get-started framework. If you are a VIM user, then the Jedi plugin provides excellent code-completion that works well with pylint, which provides static code analysis (i.e., identiﬁes missing modules and typos). Naturally, emacs has many related plugins for developing in Python. Note that are many other options, but I have tried to emphasize those most suitable for Python beginners.

1.10 Quick Guide to Performance and Parallel Programming

There are many options available to improve the performance of your Python codes. The ﬁrst thing to determine is what is limiting your computation. It could be CPU speed (unlikely), memory limitations (out-of-core computing), or it could be data transfer speed (waiting on data to arrive for processing). If your code is pure-Python, then you can try running it with Pypy, which is is an alternative Python implementation that employs a just-in-time compiler. If your code does not experience a massive speed-up with Pypy, then there is probably something external to the code that is slowing it down (e.g., disk access or network access). If Pypy doesn’t make any sense because you are using many compiled modules that Pypy does not support, then there are many diagnostic tools available.

Python has its own built-in proﬁler cProfile you can invoke from the command line as in the following

>>> python -m cProfile -o program.prof my_program.py

The output of the proﬁler is saved to the program.prof ﬁle. This ﬁle can be visualized in runsnakerun to get a nice graphical picture of where the code is spending the most time. The task manager on your operating system can also provide clues as your program runs to see how it is consuming resources. The line_profiler by Robert Kern provides an excellent way to see how the code is spending its time by annotating each line of the code by its timings. In combination with runsnakerun, this narrows down problems to the line-level from the function-level.

The most common situation is that your program is waiting on data from disk or from some busy network resource. This is a common situation in web programming and there are lots of well-established tools to deal with this. Python has a multiprocessing module that is part of the standard library. This makes it easy to spawn child worker processes that can break off and individually process small parts of a big job. However, it is still your responsibility as the programmer to ﬁgure out how to distribute the data for your algorithm. Using this module means that the individual processes are to be managed by the operating system, which will be in charge of balancing the load.

The basic template for using multiprocessing is the following:

# filename multiprocessing_demo.py import multiprocessing import time def worker(k):

’worker function’ print ’am starting process %d’ % (k) time.sleep(10) # wait ten seconds print ’am done waiting!’

return

if __name__ == ’__main__’:

for i in range(10):

p = multiprocessing.Process(target=worker, args=(i,)) p.start()

Then, you run this program at the terminal as in the following,

Terminal> python multiprocessing_demo.py

It is crucially important that you run the program from the terminal this way. It is not possible to do this interactively from within IPython, say. If you look at the process manager on the operating system, you should see a number of new Python processes loitering for ten seconds. You should also see the output of the print statements above. Naturally, in a real application, you would be assigning some meaningful work for each of the workers and ﬁguring out how to send partially ﬁnished pieces between individual workers. Doing this is complex and easy to get wrong, so Python 3.2 has the helpful concurrent.futures module that has thankfully been back-ported to Python 2.7 and is available on pypi.

# filename: concurrent_demo.py import futures import time

def worker(k):

’worker function’ print ’am starting process %d’ % (k) time.sleep(10) # wait ten seconds print ’am done waiting!’

return

def main():

with futures.ProcessPoolExecutor(max_workers=3) as executor:

list(executor.map(worker,range(10)))

if __name__ == ’__main__’:

main()

Terminal> python concurrent_demo.py

You should see something like the following in the terminal. Note that we explicitly restricted the number of processes to three.

am starting process 0 am starting process 1 am starting process 2 am done waiting!

am done waiting!

...

The futures module is built on top of multiprocessing and makes it easier to use for this kind of simple task. Note that there are also versions of both that use threads instead of processes while maintaining the same usage pattern. The main difference between threads and processes is that processes have their own compartmentalized resources. The C-language Python (i.e., CPython) implementation uses a Global Interpreter Lock (GIL) that prevents threads from locking up on internal data structures. This is a course-grained locking mechanism where one thread may individually run faster because it does not have to keep track of all the bookkeeping involved in running multiple threads simultaneously. The downside is that you cannot run multiple threads simultaneously to speed up certain tasks.

There is no corresponding locking problem with processes but these are somewhat slower to start up because each process has to create its own private workspace for data structures that may be transferred between them. However, each process can certainly run independently and simultaneously once all that is set up. Note that certain alternative implementations of Python like IronPython use a ﬁner-grain threading design rather than a GIL approach. As a ﬁnal comment, on modern systems with multiple cores, it could be that multiple threads actually slow things down because the operating system may have to switch threads between different cores. This creates additional overheads in the thread switching mechanism that ultimately slow things down.

IPython itself has a parallel programming framework built into it that is powerful and easy-to-use. The ﬁrst step is to ﬁre up separate IPython engines at the terminal as in the following,

Terminal> ipcluster start --n=4

Then, in an IPython window, you can get the client,

In [1]: from IPython.parallel import Client ...: rc = Client()

The client has a connection to each of the processes we started before using ipcluster. To use all of the engines, we assign the DirectView object from the client as in the following,

In [2]: dview = rc[:]

Now, we can apply functions for each of the engines. For example, we can get the process identiﬁers using the os.getpid function,

In [3]: import os In [4]: dview.apply_sync(os.getpid) Out[4]: [6824, 4752, 8836, 3124]

Once the engines are up and running, data can be distributed to them using scatter,

In [5]: dview.scatter(’a’,range(10)) Out[5]: <AsyncResult: finished> In [6]: dview.execute(’print a’).display_outputs() [stdout:0] [0, 1, 2] [stdout:1] [3, 4, 5] [stdout:2] [6, 7] [stdout:3] [8, 9]

Note that the execute method evaluates the given string in each engine. Now that the data have been sprinkled among the active engines, we can do further computing on them,

In [7]: dview.execute(’b=sum(a)’) Out[7]: <AsyncResult: finished> In [8]: dview.execute(’print b’).display_outputs() [stdout:0] 3 [stdout:1] 12 [stdout:2] 13 [stdout:3] 17

In this example, we added up the individual a sub-lists available on each of the engines. We can gather up the individual results into a single list as in the following,

In [9]: dview.gather(’b’).r Out[9]: [3, 12, 13, 17]

This is one of the simplest mechanisms for distributing work to the individual engines and collecting the results. Unlike the other methods we discussed, you can do this iteratively, which makes it easy to experiment with how you want to distribute and compute with the data. The IPython documentation has many more examples of parallel programming styles that include running the engines on cloud resources, supercomputer clusters, and across disparate networked computing resources. Although there are many other specialized parallel programming packages, IPython provides the best trade-off for generality against complexity across all of the major platforms.

1.11 Other Resources

The Python community is ﬁlled with super-smart and amazingly helpful people. One of the best places to get help with scientiﬁc Python is the www.stackoverflow. com site which hosts a competitive Q&A forum that is particularly welcoming for Python newbies. Several of the key Python developers regularly participate there and the quality of the answers is very high. The mailing lists for any of the key tools (e.g., Numpy, IPython, Matplotlib) are also great for keeping up with the newest developments. Anything written by Hans Petter Langtangen [8] is excellent, especially if you have a physics background. The Scientiﬁc Python conference held annually in Austin is also a great place to see your favorite developers in person, ask questions, and participate in the many interesting sub-groups organized around niche topics. The PyData workshop is a semi-annual meeting focused on Python for large-scale data-intensive processing. The PyVideo site provides links to videos of talks and tutorials related to Python from around the world. A great article that summarizes best practices in Python for science is [9].

References

1. H. Childs, E.S. Brugger, K.S. Bonnell, J.S. Meredith, M. Miller, B.J. Whitlock, N. Max, A contract-based system for large data visualization. IEEE Vis. 2005, 190–198 (2005)

2. MIT Graduate Class Experimental Data. Interactive supercomputings star-p platform: Parallel MATLAB and MPI homework classroom study on high level language productivity (HPEC, 2006)

3. T.E. Oliphant, A Guide to NumPy (Trelgol Publishing, 2006)

4. L. Wilkinson, D. Wills, D. Rope, A. Norton, R. Dubbs, The Grammar of Graphics. Statistics and Computing (Springer, 2006)

5. F. Perez, B.E. Granger et al., IPython Software Package for Interactive Scientiﬁc Computing.

http://ipython.org/

6. W. McKinney, Python for Data Analysis: Data Wrangling with Pandas, NumPy, and IPython (O’Reilly, 2012)

7. O. Certik et al., SymPy: Python Library for Symbolic Mathematics. http://sympy.org/

8. H.P. Langtangen, Texts in Computational Science and Engineering, in Python Scripting for Computational Science, vol. 3, 3rd edn. (Springer, 2009)

9. D.A. Aruliah, C.T. Brown, N.P.C. Hong, M. Davis, R.T. Guy, S.H.D. Haddock, K. Huff, I.

Mitchell, M.D. Plumbley, B. Waugh, E.P. White, G. Wilson, P. Wilson, Best practices for scientiﬁc computing. CoRR, (2012). arXiv:abs/1210.0530