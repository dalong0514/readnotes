# 0303Gradient Descent For Linear Regression

In previous videos, we talked about the gradient descent algorithm and we talked about the linear regression model and the squared error cost function. In this video we're gonna put together gradient descent with our cost function, and that will give us an algorithm for linear regression or putting a straight line to our data.
Play video starting at ::20 and follow transcript0:20
So this was what we worked out in the previous videos. This gradient descent algorithm which you should be familiar and here's the linear regression model with our linear hypothesis and our squared error cost function. What we're going to do is apply gradient descent to minimize our squared error cost function. Now in order to apply gradient descent, in order to, you know, write this piece of code, the key term we need is this derivative term over here. So you need to figure out what is this partial derivative term and plugging in the definition of the cause function j. This turns out to be this.
Play video starting at :1:13 and follow transcript1:13
Sum from y equals 1 though m. Of this squared error cost function term. And all I did here was I just, you know plug in the definition of the cost function there.
Play video starting at :1:27 and follow transcript1:27
And simplifying a little bit more, this turns out to be equal to this. Sigma i equals one through m of theta zero plus theta one x i minus Yi squared. And all I did there was I took the definition for my hypothesis and plugged it in there. And turns out we need to figure out what is this partial derivative for two cases for J equals 0 and J equals 1. So we want to figure out what is this partial derivative for both the theta 0 case and the theta 1 case. And I'm just going to write out the answers. It turns out this first term is, simplifies to 1/M sum from over my training step of just that of X(i)- Y(i) and for this term partial derivative let's write the theta 1, it turns out I get this term. Minus Y(i) times X(i). Okay and computing these partial derivatives, so we're going from this equation. Right going from this equation to either of the equations down there. Computing those partial derivative terms requires some multivariate calculus. If you know calculus, feel free to work through the derivations yourself and check that if you take the derivatives, you actually get the answers that I got. But if you're less familiar with calculus, don't worry about it and it's fine to just take these equations that were worked out and you won't need to know calculus or anything like that, in order to do the homework so let's implement gradient descent and get back to work.
Play video starting at :3:14 and follow transcript3:14
So armed with these definitions or armed with what we worked out to be the derivatives which is really just the slope of the cost function j
Play video starting at :3:23 and follow transcript3:23
we can now plug them back in to our gradient descent algorithm. So here's gradient descent for linear regression which is gonna repeat until convergence, theta 0 and theta 1 get updated as you know this thing minus alpha times the derivative term.
Play video starting at :3:39 and follow transcript3:39
So this term here.
Play video starting at :3:43 and follow transcript3:43
So here's our linear regression algorithm.
Play video starting at :3:47 and follow transcript3:47
This first term here.
Play video starting at :3:52 and follow transcript3:52
That term is of course just the partial derivative with respect to theta zero, that we worked out on a previous slide. And this second term here, that term is just a partial derivative in respect to theta 1, that we worked out on the previous line. And just as a quick reminder, you must, when implementing gradient descent. There's actually this detail that you should be implementing it so the update theta 0 and theta 1 simultaneously.
Play video starting at :4:24 and follow transcript4:24
So. Let's see how gradient descent works. One of the issues we saw with gradient descent is that it can be susceptible to local optima. So when I first explained gradient descent I showed you this picture of it going downhill on the surface, and we saw how depending on where you initialize it, you can end up at different local optima. You will either wind up here or here. But, it turns out that that the cost function for linear regression is always going to be a bow shaped function like this. The technical term for this is that this is called a convex function.
Play video starting at :5:3 and follow transcript5:03
And I'm not gonna give the formal definition for what is a convex function, C, O, N, V, E, X. But informally a convex function means a bowl shaped function and so this function doesn't have any local optima except for the one global optimum. And does gradient descent on this type of cost function which you get whenever you're using linear regression it will always converge to the global optimum. Because there are no other local optimum, global optimum. So now let's see this algorithm in action.
Play video starting at :5:38 and follow transcript5:38
As usual, here are plots of the hypothesis function and of my cost function j. And so let's say I've initialized my parameters at this value. Let's say, usually you initialize your parameters at zero, zero. Theta zero and theta equals zero. But for the demonstration, in this physical infrontation I've initialized you know, theta zero at 900 and theta one at about -0.1 okay. And so this corresponds to h(x)=-900-0.1x, [the intercept should be +900] is this line, out here on the cost function. Now, if we take one step in gradient descent, we end up going from this point out here, over to the down and left, to that second point over there. And you notice that my line changed a little bit, and as I take another step of gradient descent, my line on the left will change.
Play video starting at :6:41 and follow transcript6:41
Right? And I've also moved to a new point on my cost function.
Play video starting at :6:47 and follow transcript6:47
And as I take further steps of gradient descent, I'm going down in cost. So my parameters and such are following this trajectory.
Play video starting at :6:57 and follow transcript6:57
And if you look on the left, this corresponds with hypotheses. That seem to be getting to be better and better fits to the data
Play video starting at :7:8 and follow transcript7:08
until eventually I've now wound up at the global minimum and this global minimum corresponds to this hypothesis, which gets me a good fit to the data.
Play video starting at :7:21 and follow transcript7:21
And so that's gradient descent, and we've just run it and gotten a good fit to my data set of housing prices. And you can now use it to predict, you know, if your friend has a house size 1250 square feet, you can now read off the value and tell them that I don't know maybe they could get $250,000 for their house. Finally just to give this another name it turns out that the algorithm that we just went over is sometimes called batch gradient descent. And it turns out in machine learning I don't know I feel like us machine learning people were not always great at giving names to algorithms. But the term batch gradient descent refers to the fact that in every step of gradient descent, we're looking at all of the training examples. So in gradient descent, when computing the derivatives, we're computing the sums [INAUDIBLE]. So ever step of gradient descent we end up computing something like this that sums over our m training examples and so the term batch gradient descent refers to the fact that we're looking at the entire batch of training examples. And again, it's really not a great name, but this is what machine learning people call it. And it turns out that there are sometimes other versions of gradient descent that are not batch versions, but they are instead. Do not look at the entire training set but look at small subsets of the training sets at a time. And we'll talk about those versions later in this course as well. But for now using the algorithm we just learned about or using batch gradient descent you now know how to implement gradient descent for linear regression.
Play video starting at :9:5 and follow transcript9:05
So that's linear regression with gradient descent. If you've seen advanced linear algebra before, so some of you may have taken a class in advanced linear algebra. You might know that there exists a solution for numerically solving for the minimum of the cost function j without needing to use an iterative algorithm like gradient descent. Later in this course we'll talk about that method as well that just solves for the minimum of the cost function j without needing these multiple steps of gradient descent. That other method is called the normal equations method. But in case you've heard of that method it turns out that gradient descent will scale better to larger data sets than that normal equation method. And now that we know about gradient descent we'll be able to use it in lots of different contexts and we'll use it in lots of different machine learning problems as well.
Play video starting at :9:55 and follow transcript9:55
So congrats on learning about your first machine learning algorithm. We'll later have exercises in which we'll ask you to implement gradient descent and hopefully see these algorithms right for yourselves. But before that I first want to tell you in the next set of videos. The first one to tell you about a generalization of the gradient descent algorithm that will make it much more powerful. And I guess I'll tell you about that in the next video.

## Reading

Gradient Descent For Linear Regression 
Note: [At 6:15 "h(x) = -900 - 0.1x" should be "h(x) = 900 - 0.1x"]

When specifically applied to the case of linear regression, a new form of the gradient descent equation can be derived. We can substitute our actual cost function and our actual hypothesis function and modify the equation to :

repeat until convergence: {θ0:=θ1:=}θ0−α1m∑i=1m(hθ(xi)−yi)θ1−α1m∑i=1m((hθ(xi)−yi)xi)
where m is the size of the training set, \theta_0θ 
0
​	
  a constant that will be changing simultaneously with \theta_1θ 
1
​	
  and x_{i}, y_{i}x 
i
​	
 ,y 
i
​	
 are values of the given training set (data).

Note that we have separated out the two cases for \theta_jθ 
j
​	
  into separate equations for \theta_0θ 
0
​	
  and \theta_1θ 
1
​	
 ; and that for \theta_1θ 
1
​	
  we are multiplying x_{i}x 
i
​	
  at the end due to the derivative. The following is a derivation of \frac {\partial}{\partial \theta_j}J(\theta) 
∂θ 
j
​	
 
∂
​	
 J(θ) for a single example : 


The point of all this is that if we start with a guess for our hypothesis and then repeatedly apply these gradient descent equations, our hypothesis will become more and more accurate.

So, this is simply gradient descent on the original cost function J. This method looks at every example in the entire training set on every step, and is called batch gradient descent. Note that, while gradient descent can be susceptible to local minima in general, the optimization problem we have posed here for linear regression has only one global, and no other local, optima; thus gradient descent always converges (assuming the learning rate α is not too large) to the global minimum. Indeed, J is a convex quadratic function. Here is an example of gradient descent as it is run to minimize a quadratic function.


The ellipses shown above are the contours of a quadratic function. Also shown is the trajectory taken by gradient descent, which was initialized at (48,30). The x’s in the figure (joined by straight lines) mark the successive values of θ that gradient descent went through as it converged to its minimum.