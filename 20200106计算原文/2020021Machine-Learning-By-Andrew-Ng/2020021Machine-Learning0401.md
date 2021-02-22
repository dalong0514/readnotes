Linear Algebra Review

# 0401Matrices and Vectors

Let's get started with our linear algebra review.
Play video starting at ::2 and follow transcript0:02
In this video I want to tell you what are matrices and what are vectors.
Play video starting at ::9 and follow transcript0:09
A matrix is a rectangular array of numbers written between square brackets.
Play video starting at ::16 and follow transcript0:16
So, for example, here is a matrix on the right, a left square bracket.
Play video starting at ::22 and follow transcript0:22
And then, write in a bunch of numbers.
Play video starting at ::27 and follow transcript0:27
These could be features from a learning problem or it could be data from somewhere else, but
Play video starting at ::35 and follow transcript0:35
the specific values don't matter, and then I'm going to close it with another right bracket on the right. And so that's one matrix. And, here's another example of the matrix, let's write 3, 4, 5,6. So matrix is just another way for saying, is a 2D or a two dimensional array.
Play video starting at ::53 and follow transcript0:53
And the other piece of knowledge that we need is that the dimension of the matrix is going to be written as the number of row times the number of columns in the matrix. So, concretely, this example on the left, this has 1, 2, 3, 4 rows and has 2 columns,
Play video starting at :1:14 and follow transcript1:14
and so this example on the left is a 4 by 2 matrix - number of rows by number of columns. So, four rows, two columns. This one on the right, this matrix has two rows. That's the first row, that's the second row, and it has three columns.
Play video starting at :1:35 and follow transcript1:35
That's the first column, that's the second column, that's the third column So, this second matrix we say it is a 2 by 3 matrix.
Play video starting at :1:45 and follow transcript1:45
So we say that the dimension of this matrix is 2 by 3.
Play video starting at :1:50 and follow transcript1:50
Sometimes you also see this written out, in the case of left, you will see this written out as R4 by 2 or concretely what people will sometimes say this matrix is an element of the set R 4 by 2. So, this thing here, this just means the set of all matrices that of dimension 4 by 2 and this thing on the right, sometimes this is written out as a matrix that is an R 2 by 3. So if you ever see, 2 by 3. So if you ever see something like this are 4 by 2 or are 2 by 3, people are just referring to matrices of a specific dimension.
Play video starting at :2:26 and follow transcript2:26
Next, let's talk about how to refer to specific elements of the matrix. And by matrix elements, other than the matrix I just mean the entries, so the numbers inside the matrix.
Play video starting at :2:37 and follow transcript2:37
So, in the standard notation, if A is this matrix here, then A sub-strip IJ is going to refer to the i, j entry, meaning the entry in the matrix in the ith row and jth column.
Play video starting at :2:51 and follow transcript2:51
So for example a1-1 is going to refer to the entry in the 1st row and the 1st column, so that's the first row and the first column and so a1-1 is going to be equal to 1, 4, 0, 2. Another example, 8 1 2 is going to refer to the entry in the first row and the second column and so A 1 2 is going to be equal to one nine one.
Play video starting at :3:20 and follow transcript3:20
This come from a quick examples.
Play video starting at :3:22 and follow transcript3:22
Let's see, A, oh let's say A 3 2, is going to refer to the entry in the 3rd row, and second column,
Play video starting at :3:33 and follow transcript3:33
right, because that's 3 2 so that's equal to 1 4 3 7. And finally, 8 4 1 is going to refer to this one right, fourth row, first column is equal to 1 4 7 and if, hopefully you won't, but if you were to write and say well this A 4 3, well, that refers to the fourth row, and the third column that, you know, this matrix has no third column so this is undefined,
Play video starting at :4:6 and follow transcript4:06
you know, or you can think of this as an error. There's no such element as 8 4 3, so, you know, you shouldn't be referring to 8 4 3. So, the matrix gets you a way of letting you quickly organize, index and access lots of data. In case I seem to be tossing up a lot of concepts, a lot of new notations very rapidly, you don't need to memorize all of this, but on the course website where we have posted the lecture notes, we also have all of these definitions written down. So you can always refer back, you know, either to these slides, possible coursework, so audible lecture notes if you forget well, A41 was that? Which row, which column was that? Don't worry about memorizing everything now. You can always refer back to the written materials on the course website, and use that as a reference. So that's what a matrix is. Next, let's talk about what is a vector. A vector turns out to be a special case of a matrix. A vector is a matrix that has only 1 column so you have an N x 1 matrix, then that's a remember, right? N is the number of rows, and 1 here is the number of columns, so, so matrix with just one column is what we call a vector. So here's an example of a vector, with I guess I have N equals four elements here.
Play video starting at :5:23 and follow transcript5:23
so we also call this thing, another term for this is a four dmensional
Play video starting at :5:30 and follow transcript5:30
vector, just means that
Play video starting at :5:32 and follow transcript5:32
this is a vector with four elements, with four numbers in it. And, just as earlier for matrices you saw this notation R3 by 2 to refer to 2 by 3 matrices, for this vector we are going to refer to this as a vector in the set R4.
Play video starting at :5:49 and follow transcript5:49
So this R4 means a set of four-dimensional vectors.
Play video starting at :5:56 and follow transcript5:56
Next let's talk about how to refer to the elements of the vector.
Play video starting at :6:1 and follow transcript6:01
We are going to use the notation yi to refer to the ith element of the vector y. So if y is this vector, y subscript i is the ith element. So y1 is the first element,four sixty, y2 is equal to the second element,
Play video starting at :6:19 and follow transcript6:19
two thirty two -there's the first. There's the second. Y3 is equal to 315 and so on, and only y1 through y4 are defined consistency 4-dimensional vector.
Play video starting at :6:32 and follow transcript6:32
Also it turns out that there are actually 2 conventions for how to index into a vector and here they are. Sometimes, people will use one index and sometimes zero index factors. So this example on the left is a one in that specter where the element we write is y1, y2, y3, y4.
Play video starting at :6:53 and follow transcript6:53
And this example in the right is an example of a zero index factor where we start the indexing of the elements from zero.
Play video starting at :7:1 and follow transcript7:01
So the elements go from a zero up to y three. And this is a bit like the arrays of some primary languages
Play video starting at :7:9 and follow transcript7:09
where the arrays can either be indexed starting from one. The first element of an array is sometimes a Y1, this is sequence notation I guess, and sometimes it's zero index depending on what programming language you use. So it turns out that in most of math, the one index version is more common For a lot of machine learning applications, zero index
Play video starting at :7:33 and follow transcript7:33
vectors gives us a more convenient notation.
Play video starting at :7:36 and follow transcript7:36
So what you should usually do is, unless otherwised specified,
Play video starting at :7:40 and follow transcript7:40
you should assume we are using one index vectors. In fact, throughout the rest of these videos on linear algebra review, I will be using one index vectors.
Play video starting at :7:50 and follow transcript7:50
But just be aware that when we are talking about machine learning applications, sometimes I will explicitly say when we need to switch to, when we need to use the zero index
Play video starting at :7:59 and follow transcript7:59
vectors as well. Finally, by convention, usually when writing matrices and vectors, most people will use upper case to refer to matrices. So we're going to use capital letters like A, B, C, you know, X, to refer to matrices,
Play video starting at :8:16 and follow transcript8:16
and usually we'll use lowercase, like a, b, x, y,
Play video starting at :8:21 and follow transcript8:21
to refer to either numbers, or just raw numbers or scalars or to vectors. This isn't always true but this is the more common notation where we use lower case "Y" for referring to vector and we usually use upper case to refer to a matrix.
Play video starting at :8:37 and follow transcript8:37
So, you now know what are matrices and vectors. Next, we'll talk about some of the things you can do with them

## reading

Matrices and Vectors
Matrices are 2-dimensional arrays:

⎡⎣⎢⎢⎢adgjbehkcfil⎤⎦⎥⎥⎥
[ 
a
​	
  
b
​	
  
cd
​	
  
e
​	
  
fg
​	
  
h
​	
  
ij
​	
  
k
​	
  
l
​	
 ]
The above matrix has four rows and three columns, so it is a 4 x 3 matrix.

A vector is a matrix with one column and many rows: 

⎡⎣⎢⎢⎢wxyz⎤⎦⎥⎥⎥
[ 
wxyz
​	
 ]
So vectors are a subset of matrices. The above vector is a 4 x 1 matrix.

Notation and terms:

A_{ij}A 
ij
​	
  refers to the element in the ith row and jth column of matrix A.
A vector with 'n' rows is referred to as an 'n'-dimensional vector.
v_iv 
i
​	
  refers to the element in the ith row of the vector.
In general, all our vectors and matrices will be 1-indexed. Note that for some programming languages, the arrays are 0-indexed.
Matrices are usually denoted by uppercase names while vectors are lowercase.
"Scalar" means that an object is a single value, not a vector or matrix.
\mathbb{R}R refers to the set of scalar real numbers.
\mathbb{R^n}R 
n
  refers to the set of n-dimensional vectors of real numbers.
Run the cell below to get familiar with the commands in Octave/Matlab. Feel free to create matrices and vectors and try out different things.