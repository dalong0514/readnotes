§ 1. Abstract Lebesgue Integrals

Let x be a random variable and A a set of . Let us form, for a positive λ, the sum

If this series converges absolutely for every λ, then as , Sλ tends toward a definite limit, which is by definition the integral

In this abstract form the concept of an integral was introduced by Fréchet2; it is indispensable for the theory of probability. (The reader will see in the following paragraphs that the usual definition for the conditional mathematical expectation of the variable x under hypothesis A coincides with the definition of the integral (2) except for a constant factor.)

We shall give here a brief survey of the most important properties of the integrals of form (2). The reader will find their proofs in every textbook on real variables, although the proofs are usually carried out only in the case where is the Lebesgue measure of sets in Rn. The extension of these proofs to the general case does not entail any new mathematical problem; for the most part they remain word for word the same.

I. If a random variable x is integrable on A, then it is integrate on each subset A′ of A belonging to .

II. If x is integrable on A and A is decomposed into no more than a countable number of non-intersecting sets An of , then

III. If x is integrable, |x| is also integrable, and in that case

IV. If in each event ξ, the inequalities hold, then along with x, y is also integrable3, and in that case

V. If where m and M are two constants, then

VI. If x and y are integrable, and K and L are two real constants, then Kx + Ly is also integrable, and in this case

VII. If the series

converges, then the series

converges at each point of set A with the exception of a certain set B for which . If we set x = 0 everywhere except on A − B, then

VIII. If x and y are equivalent (P{x ≠ y} = 0), then for every set A of

IX. If (3) holds for every set A of , then x and y are equivalent.

From the foregoing definition of an integral we also obtain the following property, which is not found in the usual Lebesgue theory.

X. Let and be two probability functions defined on the same field , , and let x be integrable on A relative to and . Then

XI. Every bounded random variable is integrable.

§ 2. Absolute and Conditional Mathematical Expectations

Let x be a random variable. The integral

is called in the theory of probability the mathematical expectation of the variable x. From the properties III, IV, V, VI, VII, VIII, XI, it follows that

I. ;

II. if everywhere;

III. ;

IV. ;

V. , if the series converges;

VI. If x and y are equivalent then

VII. Every bounded random variable has a mathematical expectation.

From the definition of the integral, we have

The second line is nothing more than the usual definition of the Stieltjes integral

Formula (1) may therefore serve as a definition of the mathematical expectation .

Now let u be a function of the elementary event ξ, and x be a random variable defined as a single-valued function x = x(u) of u. Then

where is the probability function of u. It then follows from the definition of the integral that

and, therefore,

where E(u) denotes the set of all possible values of u.

In particular, when u itself is a random variable we have

When x(u) is continuous, the last integral in (3) is the ordinary Stieltjes integral. We must note, however, that the integral

can exist even when the mathematical expectation does not. For the existence of , it is necessary and sufficient that the integral

be finite4.

If u is a point (u1, u2,..., un) of the space Rn, then as a result of (2):

We have already seen that the conditional probability possesses all the properties of a probability function. The corresponding integral

we call the conditional mathematical expectation of the random variable x with respect to the event B. Since

we obtain from (5) the equation

We recall that in case A ⊂ B,

we thus obtain

From (6) and the equality

we obtain at last

and, in particular, we have the formula

§ 3. The Tchebycheff Inequality

Let f(x) be a non-negative function of a real argument x, which for never becomes smaller than b > 0. Then for any random variable x

provided the mathematical expectation exists. For,

from which (1) follows at once.

For example, for every positive c,

Now let f(x) be non-negative, even, and, for positive x, nondecreasing. Then for every random variable x and for any choice of the constant a > 0 the following inequality holds

In particular,

Especially important is the case f(x) = x2. We then obtain from (3) and (4)

where

is called the variance of the variable x. It is easy to calculate that

If f(x) is bounded:

then a lower bound for can be found. For

and therefore

If instead of f(x) the random variable x itself is bounded,

then , and instead of (7), we have the formula

In the case f(x) = x2, we have from (8)

§ 4. Some Criteria for Convergence

Let

be a sequence of random variables and f(x) be a non-negative, even, and for positive x a monotonically increasing function5. Then the following theorems are true:

I. In order that the sequence (1) converge in probability the following condition is sufficient: For each ε > 0 there exists an n such that for every p > 0, the following inequality holds:

II. In order that the sequence (1) converge in probability to the random variable x, the following condition is sufficient:

III. If f(x) is bounded and continuous and f(0) = 0, then conditions I and II are also necessary.

IV. If f(x) is continuous, f(0) = 0, and the totality of all x1, x2, ..., xn, ..., x is bounded, then conditions I and II are also necessary.

From II and IV, we obtain in particular

V. In order that sequence (1) converge in probability to x, it is sufficient that

If also the totality of all x1, x2,..., xn, ..., x is bounded, then the condition is also necessary.

For proofs of I-IV see Slutsky [1] and Fréchet [1]. However, these theorems follow almost immediately from formulas (3) and (8) of the preceding section.

§ 5. Differentiation and Integration of Mathematical Expectations with Respect to a Parameter

Let us put each elementary event ξ into correspondence with a definite real function x(t) of a real variable t. We say that x(t) is a random function if for every fixed t, the variable x(t) is a random variable. The question now arises, under what conditions can the mathematical expectation sign be interchanged with the integration and differentiation signs. The two following theorems, though they do not exhaust the problem, can nevertheless give a satisfactory answer to this question in many simple cases.

THEOREM I: If the mathematical expectation is finite for any t, and x(t) is always differentiable for any t, while the derivative x′(t) of x(t) with respect to t is always less in absolute value than some constant M, then

THEOREM II: If x(t) always remains less, in absolute value, than some constant K and is integrable in the Riemann sense, then

provided is integrable in the Riemann sense.

Proof of Theorem I. Let us first note that x′(t) as the limit of the random variables

is also a random variable. Since x′(t) is bounded, the mathematical expectation exists (Property VII of mathematical expectation, in § 2). Let us choose a fixed t and denote by A the event

The probability tends to zero as for every ε > 0. Since

holds everywhere, and moreover in the case Ā

then

We may choose the arbitrarily, and is arbitrarily small for any sufficiently small h. Therefore

which was to be proved.

Proof of Theorem II. Let

Since Sn converges to , we can choose for any ε > 0 an N such that from there follows the inequality

If we set

then

Therefore, converges to , from which results the equation

Theorem II can easily be generalized for double and triple and higher order multiple integrals. We shall give an application of this theorem to one example in geometric probability. Let G be a measurable region of the plane whose shape depends on chance; in other words, let us assign to every elementary event ξ of a field of probability a definite measurable plane region G. We shall denote by J the area of the region G, and by the probability that the point (x, y) belongs to the region G. Then

To prove this it is sufficient to note that

where f(x, y) is the characteristic function of the region G (f(x, y) = 1 on G and f(x, y) = 0 outside of G)6.

1 As was stated in § 5 of the third chapter, we are considering in this, as well as in the following chapters, Borel fields of probability only.

2 FRÉCHET, Sur l’intégrale d’une functionnelle étendue à un ensemble abstrait, Bull. Soc. Math. France v. 43, 1915, p. 248.

3 It is assumed that y is a random variable, i.e., in the terminology of the general theory of integration, measurable with respect to .

4 Cf. V. GLIVENKO, Sur les valeurs probables de fonctions, Rend. Accad. Lincei v. 8, 1928, pp. 480-483.

5 Therefore f(x) > 0 if x ≠ 0.

6 Cf. A. KOLMOGOROV and M. LEONTOVICH, Zur Berechnung der mittleren Brownschen Fläche, Physik. Zeitschr. d. Sovietunion, v. 4, 1933.

