# 01 Linear Equations in Linear Algebra

INTRODUCTORY EXAMPLE

Linear Models in Economics and Engineering

It was late summer in 1949. Harvard Professor Wassily Leontief was carefully feeding the last of his punched cards into the university’s Mark II computer. The cards contained information about the U.S. economy and represented a summary of more than 250,000 pieces of information produced by the U.S. Bureau of Labor Statistics after two years of intensive work. Leontief had divided the U.S. economy into 500 “sectors,” such as the coal industry, the automotive industry, communications, and so on. For each sector, he had written a linear equation that described how the sector distributed its output to the other sectors of the economy. Because the Mark II, one of the largest computers of its day, could not handle the resulting system of 500 equations in 500 unknowns, Leontief had distilled the problem into a system of 42 equations in 42 unknowns.

Programming the Mark II computer for Leontief’s 42 equations had required several months of effort, and he was anxious to see how long the computer would take to solve the problem. The Mark II hummed and blinked for 56 hours before ﬁnally producing a solution. We will discuss the nature of this solution in Sections 1.6 and 2.6.

Leontief, who was awarded the 1973 Nobel Prize in Economic Science, opened the door to a new era in mathematical modeling in economics. His efforts at Harvard in 1949 marked one of the ﬁrst signiﬁcant uses of computers to analyze what was then a largescale mathematical model. Since that time, researchers in many other ﬁelds have employed computers to analyze mathematical models. Because of the massive amounts of data involved, the models are usually linear; that is, they are described by systems of linear equations.

The importance of linear algebra for applications has risen in direct proportion to the increase in computing power, with each new generation of hardware and software triggering a demand for even greater capabilities. Computer science is thus intricately linked with linear algebra through the explosive growth of parallel processing and large-scale computations.

Scientists and engineers now work on problems far more complex than even dreamed possible a few decades ago. Today, linear algebra has more potential value for students in many scientiﬁc and business ﬁelds than any other undergraduate mathematics subject! The material in this text provides the foundation for further work in many interesting areas. Here are a few possibilities; others will be described later.

 Oil exploration. When a ship searches for offshore oil deposits, its computers solve thousands of separate systems of linear equations every day.

The seismic data for the equations are obtained from underwater shock waves created by explosions from air guns. The waves bounce off subsurface rocks and are measured by geophones attached to mile-long cables behind the ship.

Linear programming. Many important management decisions today are made on the basis of linear programming models that use hundreds of variables. The airline industry, for instance, employs linear programs that schedule ﬂight crews, monitor the locations of aircraft, or plan the varied schedules of support services such as maintenance and terminal operations.

Electrical networks. Engineers use simulation software to design electrical circuits and microchips involving millions of transistors. Such software relies on linear algebra techniques and systems of linear equations.

Systems of linear equations lie at the heart of linear algebra, and this chapter uses them to introduce some of the central concepts of linear algebra in a simple and concrete setting. Sections 1.1 and 1.2 present a systematic method for solving systems of linear equations. This algorithm will be used for computations throughout the text. Sections 1.3 and 1.4 show how a system of linear equations is equivalent to a vector equation and to a matrix equation. This equivalence will reduce problems involving linear combinations of vectors to questions about systems of linear equations. The fundamental concepts of spanning, linear independence, and linear transformations, studied in the second half of the chapter, will play an essential role throughout the text as we explore the beauty and power of linear algebra.

## 1.1 SYSTEMS OF LINEAR EQUATIONS

A linear equation in the variables x ; : : : ; x n is an equation that can be written in the form a 1 x 1 1 C a x 2 C    C a n x n D b (1)

where b and the coefﬁcients a ; : : : ;2 1 a n are real or complex numbers, usually known in advance. The subscript n may be any positive integer. In textbook examples and exercises, n is normally between 2 and 5. In real-life problems, n might be 50 or 5000, or even larger.

The equations  4x 1 5 x 2 C 2 D x 1 and x 2 D 2 p6 x 1 C x3 

are both linear because they can be rearranged algebraically as in equation (1): p 3x 1 5 x 2 D 2 and 2x 1 C x 2 x3 D 2 6

The equations

4x

1 5

x 2 D x 1 x 2

and

p x 2 D 2 x 1 6

p are not linear because of the presence of x 1 x 2 in the ﬁrst equation and x 1 in the second.

A system of linear equations (or a linear system) is a collection of one or more linear equations involving the same variables—say, x 1 ; : : : ; x n . An example is

A solution of the system is a list .s 1 ; s 2 ; : : : ; s n / of numbers that makes each equation a true statement when the values s 1 ; : : : ; s n are substituted for x 1 ; : : : ; x n , respectively. For instance, .5; 6:5; 3/ is a solution of system (2) because, when these values are substituted in (2) for x 1 ; x 2 ; x 3 , respectively, the equations simplify to 8 D 8 and7 D7. 
The set of all possible solutions is called the solution set of the linear system. Two linear systems are called equivalent if they have the same solution set. That is, each solution of the ﬁrst system is a solution of the second system, and each solution of the second system is a solution of the ﬁrst. 
Finding the solution set of a system of two linear equations in two variables is easy because it amounts to ﬁnding the intersection of two lines. A typical problem is 
x 12 x 2 D1x 1 C 3x 2 D 3 
The graphs of these equations are lines, which we denote by ` 1 and ` 2 . A pair of numbers .x ; x 2 / satisﬁes both equations in the system if and only if the point .x 1 ; x 2 / lies on both `1 1 and ` 2 . In the system above, the solution is the single point .3; 2/, as you can easily verify. See Figure 1. 
x2 
2

2
1
3
x1 
FIGURE 1 Exactly one solution. 
Of course, two lines need not intersect in a single point—they could be parallel, or they could coincide and hence “intersect” at every point on the line. Figure 2 shows the graphs that correspond to the following systems: 
(a) x 12 x 2 D1x 1 C 2x 2 D 3 
(b) x 12 x 2 D1x 1 C 2x 2 D 1 
x2 
(a) 
x2 
2

1
3
2

1
3
x1 
x1 
2 
(b) 
FIGURE 2 (a) No solution. (b) Inﬁnitely many solutions. 
Figures 1 and 2 illustrate the following general fact about linear systems, to be veriﬁed in Section 1.2. 

A system of linear equations has

1. no solution, or

2. exactly one solution, or

3. inﬁnitely many solutions.

A system of linear equations is said to be consistent if it has either one solution or inﬁnitely many solutions; a system is inconsistent if it has no solution.

Matrix Notation

The essential information of a linear system can be recorded compactly in a rectangular array called a matrix. Given the system

x 1 2 x 2 C x 3 D 0

2x 2 8 x 3 D 8

x 3 D 10

1 5

(3)

5x

with the coefﬁcients of each variable aligned in columns, the matrix 2 3 1 2 1 4 0 2 8 5 5 0 5

is called the coefﬁcient matrix (or matrix of coefﬁcients) of the system (3), and 2 3 1 2 1 0 4 0 2 8 8 5 5 0 5 10

(4)

is called the augmented matrix of the system. (The second row here contains a zero because the second equation could be written as 0  x 1 C 2x 2 8 x 3 D 8.) An augmented matrix of a system consists of the coefﬁcient matrix with an added column containing the constants from the right sides of the equations.

The size of a matrix tells how many rows and columns it has. The augmented matrix (4) above has 3 rows and 4 columns and is called a 3  4 (read “3 by 4”) matrix. If m and n are positive integers, an m  n matrix is a rectangular array of numbers with m rows and n columns. (The number of rows always comes ﬁrst.) Matrix notation will simplify the calculations in the examples that follow.

Solving a Linear System

This section and the next describe an algorithm, or a systematic procedure, for solving linear systems. The basic strategy is to replace one system with an equivalent system (i.e., one with the same solution set) that is easier to solve.

Roughly speaking, use the x 1 term in the ﬁrst equation of a system to eliminate the x 1 terms in the other equations. Then use the x 2 term in the second equation to eliminate the x 2 terms in the other equations, and so on, until you ﬁnally obtain a very simple equivalent system of equations.

Three basic operations are used to simplify a linear system: Replace one equation by the sum of itself and a multiple of another equation, interchange two equations, and multiply all the terms in an equation by a nonzero constant. After the ﬁrst example, you will see why these three operations do not change the solution set of the system. 1.1 Systems of Linear Equations

5

EXAMPLE 1

Solve system (3).

SOLUTION The elimination procedure is shown here with and without matrix notation, and the results are placed side by side for comparison:

2 3 x 1 2 x 2 C x D 0 1 2 1 0 2x 2 8 x D 8 4 0 2 8 8 5 5 0 5 10 5x 1 5 x 3 3 3 D 10

Keep x 1 in the ﬁrst equation and eliminate it from the other equations. To do so, add 5 times equation 1 to equation 3. After some practice, this type of calculation is usually performed mentally: 5

 Œequation 1 C Œequation 3

x 1 C 10x 2 5 x 3 3 3 D 0 5x 1 5 x D 10

Œnew equation 3 5

10x

2 1

0x D 10

The result of this calculation is written in place of the original third equation: 2 3 x 1 2 x 2 C x 3 D 0 1 2 1 0 2x 2 8 x 3 D 8 4 0 2 8 8 5 0 10 10 10 10x 2 1 0x 3 D 10

Now, multiply equation 2 by 2 1 in order to obtain 1 as the coefﬁcient for x 2 . (This calculation will simplify the arithmetic in the next step.)

2 3 x 1 2 x 2 C x 3 D 0 1 2 1 0 x 2 4 x 3 D 4 4 0 1 4 4 5 0 10 10 10 10x 2 1 0x 3 D 10

Use the x 2 in equation 2 to eliminate the 10x 2 in equation 3. The “mental’’ computation is 1

0  Œequation 2 0x 2 C 40x 3 D 40

C Œequation 3 10x Œnew equation 3 1

2 1

0x 3 D

10

30x 3 D 30

The result of this calculation is written in place of the previous third equation (row): 2 3 x 1 2 x 2 C x 3 D 0 1 2 1 0 x 2 4 x 3 D 4 4 0 1 4 4 5 30x 3 D 30 0 0 30 30

Now, multiply equation 3 by 30 1 in order to obtain 1 as the coefﬁcient for x 3 . (This calculation will simplify the arithmetic in the next step.)

2 3 x 1 2 x 2 C x 3 D 0 1 2 1 0 x 2 4 x 3 D 4 4 0 1 4 4 5 0 0 1 1 x 3 D 1

The new system has a triangular form (the intuitive term triangular will be replaced by a precise term in the next section):

x 1 2 x 2 C x 3 D 0 x 2 4 x 3 D 4 x 3 D 1

2 3 1 2 1 0 4 0 1 4 4 5 0 0 1 1 6

CHAPTER 1

Linear Equations in Linear Algebra

Eventually, you want to eliminate the 2x term from equation 1, but it is more efﬁcient to use the x 3 in equation 3 ﬁrst, to eliminate the 4x and Cx 3 terms in equations 2 and 1. The two “mental” calculations are

x3 

4x D 4  Œequation 3 D 1 x 2 4 x 3 3 D 4 C Œequation 1 x 1 2 x 2 2 C x 3 3 D 0 x 2 D 0 1Œnew equation 1 xx 1 2 x D 1 It is convenient to combine the results of these two operations:

4  Œequation 3 C Œequation 2 Œnew equation 2

(1, 0, 1)

2 3 x 1 2 x D 1 1 2 0 1 x 2 2 D 0 4 0 3 1 0 0 5 x 3 D 1 0 0 1 1

x1 

x2 

Now, having cleaned out the column above the x in equation 3, move back to the x 2 in equation 2 and use it to eliminate the 2x above it. Because of the previous work with x 3 , there is now no arithmetic involving x 3 2 terms. Add 2 times equation 2 to equation 1 and obtain the system:

Each of the original equations determines a plane in three-dimensional space. The point .1; 0; 1/ lies in all three planes.

2 3 x 1 D 1 1 0 0 1 4 5 x 2 D 0 0 1 0 0 x D 1 0 0 1 1

3

The work is essentially done. It shows that the only solution of the original system is .1; 0; 1/. However, since there are so many calculations involved, it is a good practice to check the work. To verify that .1; 0; 1/ is a solution, substitute these values into the left side of the original system, and compute:

1.1/ 2.0/ C 1. 1/ D 1 0 1 D 0

2.0/ 8. 1/ D 0 C 8 D 8

5.1/ 5. 1/ D 5 C 5 D 10

The results agree with the right side of the original system, so .1; 0; 1/ is a solution of the system.

Example 1 illustrates how operations on equations in a linear system correspond to operations on the appropriate rows of the augmented matrix. The three basic operations listed earlier correspond to the following operations on the augmented matrix.

ELEMENTARY ROW OPERATIONS 1. (Replacement) Replace one row by the sum of itself and a multiple of another row. 1

2. (Interchange) Interchange two rows.

3. (Scaling) Multiply all entries in a row by a nonzero constant.

Row operations can be applied to any matrix, not merely to one that arises as the augmented matrix of a linear system. Two matrices are called row equivalent if there is a sequence of elementary row operations that transforms one matrix into the other.

It is important to note that row operations are reversible. If two rows are interchanged, they can be returned to their original positions by another interchange. If a

1

A common paraphrase of row replacement is “Add to one row a multiple of another row.” 1.1 Systems of Linear Equations

7

row is scaled by a nonzero constant c , then multiplying the new row by 1=c produces the original row. Finally, consider a replacement operation involving two rows—say, rows 1 and 2—and suppose that c times row 1 is added to row 2 to produce a new row 2. To “reverse” this operation, add c times row 1 to (new) row 2 and obtain the original row 2. See Exercises 29–32 at the end of this section.

At the moment, we are interested in row operations on the augmented matrix of a system of linear equations. Suppose a system is changed to a new one via row operations. By considering each type of row operation, you can see that any solution of the original system remains a solution of the new system. Conversely, since the original system can be produced via row operations on the new system, each solution of the new system is also a solution of the original system. This discussion justiﬁes the following statement.

If the augmented matrices of two linear systems are row equivalent, then the two systems have the same solution set.

Though Example 1 is lengthy, you will ﬁnd that after some practice, the calculations go quickly. Row operations in the text and exercises will usually be extremely easy to perform, allowing you to focus on the underlying concepts. Still, you must learn to perform row operations accurately because they will be used throughout the text.

The rest of this section shows how to use row operations to determine the size of a solution set, without completely solving the linear system.

Existence and Uniqueness Questions

Section 1.2 will show why a solution set for a linear system contains either no solutions, one solution, or inﬁnitely many solutions. Answers to the following two questions will determine the nature of the solution set for a linear system.

To determine which possibility is true for a particular system, we ask two questions.

TWO FUNDAMENTAL QUESTIONS ABOUT A LINEAR SYSTEM 1. Is the system consistent; that is, does at least one solution exist?

2. If a solution exists, is it the only one; that is, is the solution unique?

These two questions will appear throughout the text, in many different guises. This section and the next will show how to answer these questions via row operations on the augmented matrix.

EXAMPLE 2

Determine if the following system is consistent:

x

1 2

x2 C x3 D 0

2x

2 8

x3 D 8

5x

1 5

x 3 D 10

SOLUTION This is the system from Example 1. Suppose that we have performed the row operations necessary to obtain the triangular form 2 3 1 2 1 0 4 0 1 4 4 5 0 0 1 1

x 1 2 x 2 C x 3 D 0 x 2 4 x 3 D 4 x 3 D 1 8

CHAPTER 1

x1 

Linear Equations in Linear Algebra

At this point, we know x 3 . Were we to substitute the value of x 3 into equation 2, we could compute x 2 and hence could determine x 1 from equation 1. So a solution exists; the system is consistent. (In fact, x 2 is uniquely determined by equation 2 since x 3 has only one possible value, and x 1 is therefore uniquely determined by equation 1. So the solution is unique.)

EXAMPLE 3

Determine if the following system is consistent:

x 2 4 x 3 D 8

2x 1 3 x 2 C 2x 3 D 1

4x 1 8 x 2 C 12x 3 D 1

(5)

SOLUTION The augmented matrix is

2 4

0 1 4 2 3 2 4 8 12

8 1 1

3 5

To obtain an x 1 in the ﬁrst equation, interchange rows 1 and 2:

2 4

2 3 2 0 1 4 4 8 12

1 8 1

3 5

To eliminate the 4x 1 term in the third equation, add 2 times row 1 to row 3:

2 4

2 3 2 1 0 1 4 8 0 2 8 1

3 5

(6)

Next, use the x 2 term in the second equation to eliminate the 2x term from the third equation. Add 2 times row 2 to row 3:

x3 

2 4

2 3 2 0 1 4 0 0 0

1 8 15

3 5

(7)

The augmented matrix is now in triangular form. To interpret it correctly, go back to equation notation:

x2 

2x 1 3 x 2 C 2x 3 D 1 x 2 4 x 3 D 8 0 D 15

(8)

The system is inconsistent because there is no point that lies on all three planes.

The equation 0 D 15 is a short form of 0x 1 C 0x 2 C 0x 3 D 15. This system in triangular form obviously has a built-in contradiction. There are no values of x 1 ; x 2 ; x 3 that satisfy (8) because the equation 0 D 15 is never true. Since (8) and (5) have the same solution set, the original system is inconsistent (i.e., has no solution).

Pay close attention to the augmented matrix in (7). Its last row is typical of an inconsistent system in triangular form. 1.1 Systems of Linear Equations

9

NU M E R I C AL NOTE

In real-world problems, systems of linear equations are solved by a computer. For a square coefﬁcient matrix, computer programs nearly always use the elimination algorithm given here and in Section 1.2, modiﬁed slightly for improved accuracy.

The vast majority of linear algebra problems in business and industry are solved with programs that use ﬂoating point arithmetic. Numbers are represented as decimals ˙:d 1    d p  10 r , where r is an integer and the number p of digits to the right of the decimal point is usually between 8 and 16. Arithmetic with such numbers typically is inexact, because the result must be rounded (or truncated) to the number of digits stored. “Roundoff error” is also introduced when a number such as 1=3 is entered into the computer, since its decimal representation must be approximated by a ﬁnite number of digits. Fortunately, inaccuracies in ﬂoating point arithmetic seldom cause problems. The numerical notes in this book will occasionally warn of issues that you may need to consider later in your career.

PRACTICE PROBLEMS

Throughout the text, practice problems should be attempted before working the exercises. Solutions appear after each exercise set.

1. State in words the next elementary row operation that should be performed on the system in order to solve it. [More than one answer is possible in (a).]

a. x 1 C 4x 2 2 x 3 C 8x 4 D 12 x 2 7 x 3 C 2x 4 D 4 5x 3 x4 D 7 x 3 C 3x 4 D 5

b. x 1 3 x 2 C 5x 3 2 x 4 D

0

D 4 D 3 x 4 D 1 2. The augmented matrix of a linear system has been transformed by row operations into the form below. Determine if the system is consistent.

x 2 C 8x3 

2x3 

2 3 1 5 2 6 4 0 4 7 2 5 0 0 5 0

3. Is .3; 4; 2/ a solution of the following system?

5x 1 x2 C 2x 3 D 7 2 x 1 C 6x 2 C 9x 3 D 0 7 x 1 C 5x 2 3 x 3 D 7

4. For what values of h and k is the following system consistent?

2x 1 x2 D h 6 x 1 C 3x 2 D k 10

CHAPTER 1

Linear Equations in Linear Algebra

## 1.2 ROW REDUCTION AND ECHELON FORMS