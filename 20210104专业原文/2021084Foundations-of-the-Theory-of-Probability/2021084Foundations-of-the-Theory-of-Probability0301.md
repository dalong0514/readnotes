# 0301. RANDOM VARIABLES

§ 1. Probability Functions

Given a mapping of the set E into a set E′ consisting of any type of elements, i.e., a single-valued function u(ξ) defined on E, whose values belong to E′. To each subset A′ of E′ we shall put into correspondence, as its pre-image in E, the set u−1 (A′) of all elements of E which map onto elements of A′. Let be the system of all subsets A′ of E′, whose pre-images belong to the field . will then also be a field. If happens to be a Borel field, the same will be true of . We now set

Since this set-function , defined on , satisfies with respect to the field all of our Axioms I - VI, it represents a probability function on . Before turning to the proof of all the facts just stated, we shall formulate the following definition.

DEFINITION. Given a single-valued function u(ξ) of a random event ξ. The function , defined by (1), is then called the probability function of u.

Remark 1: In studying fields of probability , we call the function simply the probability function, but is called the probability function of u. In the case u(ξ) = ξ, coincides with .

Remark 2: The event u−1(A′) consists of the fact that u(ξ) belongs to A′. Therefore, is the probability of u(ξ) ⊂ A′.

We still have to prove the above-mentioned properties of and . They follow, however, from a single fact, namely:

LEMMA. The sum, product, and difference of any pre-image sets u−1(A′) are the pre-images of the corresponding sums, products, and differences of the original sets A′.

The proof of this lemma is left for the reader.

Let A′ and B′ be two sets of . Their pre-images A and B belong then to . Since is a field, the sets AB, A + B, and A − B also belong to ; but these sets are the pre-images of the sets A′B′, A′ + B′, and A′ − B′, which thus belong to . This proves that is a field. In the same manner it can be shown that if is a Borel field, so is .

Furthermore, it is clear that

That is always non-negative, is self-evident. It remains only to be shown, therefore, that is completely additive (cf. the end of § 1, Chap. II).

Let us assume that the sets , and therefore their pre-images , are disjoint. It follows that

which proves the complete additivity of .

In conclusion let us also note the following. Let u1(ξ) be a function mapping E on E′, and u2(ξ′) be another function, mapping E′ on E″. The product function u2u1(ξ) maps E on E″. We shall now study the probability functions P(u1)(A′) and for the functions u1(ξ) and u(ξ) = u2u1(ξ). It is easy to show that these two probability functions are connected by the following relation:

§ 2. Definition of Random Variables and of Distribution Functions

DEFINITION. A real single-valued function x(ξ), defined on the basic set E, is called a random variable if for each choice of a real number a the set {x < a) of all ξ for which the inequality x < a holds true, belongs to the system of sets .

This function x(ξ) maps the basic set E into the set R1 of all real numbers. This function determines, as in § 1, a field of subsets of the set R1. We may formulate our definition of random variable in this manner: A real function x(ξ) is a random variable if and only if contains every interval of the form (−∞; a).

Since is a field, then along with the intervals (−∞; a) it contains all possible finite sums of half-open intervals [a; b). If our field of probability is a Borel field, then and are Borel fields; therefore, in this case contains all Borel sets of R1

The probability function of a random variable we shall denote in the future by . It is defined for all sets of the field . In particular, for the most important case, the Borel field of probability, is defined for all Borel sets of R1.

DEFINITION. The function

where −∞ and +∞ are allowable values of a, is called the distribution function of the random variable x.

From the definition it follows at once that

The probability of the realization of both inequalities , is obviously given by the formula

From this, we have, for a < b,

which means that F(x)(a) is a non-decreasing function. Now let a1 < a2 < ... < an < ... < b; then

Therefore, in accordance with the continuity axiom,

approaches zero as n → + ∞. From this it is clear that F(x)(a) is continuous on the left.

In an analogous way we can prove the formulae:

If the field of probability is a Borel field, the values of the probability function for all Borel sets A of R1 are uniquely determined by knowledge of the distribution function F(x)(a) (cf. § 3, III in Chap. II). Since our main interest lies in these values of , the distribution function plays a most significant role in all our future work.

If the distribution function F(x)(a) is differentiable, then we call its derivative with respect to a,

the probability density of x at the point a.

If also for each a, then we may express the probability function for each Borel set A in terms of f(x)(a) in the following manner:

In this case we call the distribution of x continuous. And in the general case, we write, analogously

All the concepts just introduced are capable of generalization for conditional probabilities. The set function

is the conditional probability function of x under hypothesis B. The non-decreasing function

is the corresponding distribution function, and, finally (in the case where is differentiable)

is the conditional probability density of x at the point a under hypothesis B.

§ 3. Multi-dimensional Distribution Functions

Let now n random variables x1, x2,..., xn be given. The point x = (x1, x2, ..., xn) of the n-dimensional space Rn is a function of the elementary event ξ. Therefore, according to the general rules in §1, we have a field consisting of subsets of space Rn and a probability function defined on . This probability function is called the n-dimensional probability function of the random variables x1, x2, ... , xn.

As follows directly from the definition of a random variable, the field contains, for each choice of i and ai (i = 1, 2, ... , n), the set of all points in Rn for which xi < ai. Therefore also contains the intersection of the above sets, i.e. the set La1a2...an of all points of Rn for which all the inequalities xi < ai hold (i = 1, 2, ..., n)1.

If we now denote as the n-dimensional half-open interval

the set of all points in Rn, for which , then we see at once that each such interval belongs to the field since

The Borel extension of the system of all n-dimensional half-open intervals consists of all Borel sets in Rn. From this it follows that in the case of a Borel field of probability, the field contains all the Borel sets in the space Rn.

THEOREM: In the case of a Borel field of probability each Borel function x = f(x1, x2,..., xn) of a finite number of random variables x1, x2, ..., xn is also a random variable.

All we need to prove this is to point out that the set of all points (x1, x2, . . . , xn) in Rn for which x = f (x1, x2, ..., xn) < a, is a Borel set. In particular, all finite sums and products of random variables are also random variables.

DEFINITION: The function

is called the n-dimensional distribution function of the random variables x1, x2, . . . , xn.

As in the one-dimensional case, we prove that the n-dimensional distribution function F(x1, x2, . . . , xn) (a1, a2, . . . , an) is non-decreasing and continuous on the left in each variable. In analogy to equations (3) and (4) in § 2, we here have

The distribution function F(x1 x2 ... xn) gives directly the values of only for the special sets La1a2...an. If our field, however, is a Borel field, then2 is uniquely determined for all Borel sets in Rn by knowledge of the distribution function F(x1, x2, ..., xn).

If there exists the derivative

we call this derivative the n-dimensional probability density of the random variables x1, x2, ... , xn at the point a1, a2, ..., an. If also for every point (a1, a2, ..., an)

then the distribution of x1, x2, . . . , xn is called continuous. For every Borel set A ⊂ Rn, we have the equality

In closing this section we shall make one more remark about the relationships between the various probability functions and distribution functions.

Given the substitution

and let rs denote the transformation

of space Rn into itself. It is then obvious that

Now let x′ = pk(x) be the「projection」of the space Rn on the space Rk (k < n), so that the point (x1, x2, ... , xn) is mapped onto the point (x1, x2,..., xk). Then, as a result of Formula (2) in § 1,

For the corresponding distribution functions, we obtain from (10) and (11) the equations:

§ 4. Probabilities in Infinite-dimensional Spaces

In § 3 of the second chapter we have seen how to construct various fields of probability common in the theory of probability. We can imagine, however, interesting problems in which the elementary events are defined by means of an infinite number of coordinates. Let us take a set M of indices μ (indexing set) of arbitrary cardinality . The totality of all systems

of real numbers xμ, where μ runs through the entire set M, we shall call the space RM (in order to define an element ξ in space RM, we must put each element μ in set M in correspondence with a real number xμ or, equivalently, assign a real single-valued function xμ of the element μ, defined on M)3. If the set M consists of the first n natural numbers 1, 2,... , n, then RM is the ordinary n-dimensional space Rn. If we choose for the set M all real numbers R1, then the corresponding space RM = RR1 will consist of all real functions

of the real variable μ.

We now take the set RM (with an arbitrary set M) as the basic set E. Let ξ = {xμ) be an element in E; we shall denote by pμ1 μ2 ... μn(ξ) the point (xμ1, xμ2, ..., xμn) of the n-dimensional space Rn. A subset A of E we shall call a cylinder set if it can be represented in the form

where A′ is a subset of Rn. The class of all cylinder sets coincides, therefore, with the class of all sets which can be defined by relations of the form

In order to determine an arbitrary cylinder set pμ1 μ2 ... μn(A′) by such a relation, we need only take as f a function which equals 0 on A′, but outside of A′ equals unity.

A cylinder set is a Borel cylinder set if the corresponding set A′ is a Borel set. All Borel cylinder sets of the space RM form a field, which we shall henceforth denote by 4.

The Borel extension of the field we shall denote, as always, by . Sets in we shall call Borel sets of the space RM.

Later on we shall give a method of constructing and operating with probability functions on , and consequently, by means of the Extension Theorem, on also. We obtain in this manner fields of probability sufficient for all purposes in the case that the set M is denumerable. We can therefore handle all questions touching upon a denumerable sequence of random variables. But if M is not denumerable, many simple and interesting subsets of RM remain outside of . For example, the set of all elements ξ for which xμ remains smaller than a fixed constant for all indices μ, does not belong to the system if the set M is non-denumerable.

It is therefore desirable to try whenever possible to put each problem in such a form that the space of all elementary events ξ has only a denumerable set of coordinates.

Let a probability function be defined on . We may then regard every coordinate xμ of the elementary event ξ as a random variable. In consequence, every finite group (xμ1, xμ2, ..., xμn) of these coordinates has an n-dimensional probability function and a corresponding distribution function Fμ1μ2...μn(a1, a2, ..., an). It is obvious that for every Borel cylinder set

the following equation holds:

where A′ is a Borel set of Rn. In this manner, the probability function is uniquely determined on the field of all cylinder sets by means of the values of all finite probability functions for all Borel sets of the corresponding spaces Rn. However, for Borel sets, the values of the probability functions are uniquely determined by means of the corresponding distribution functions. We have thus proved the following theorem:

The set of all finite-dimensional distribution functions Fμ1μ2...μn uniquely determines the probability function for all sets in . If is defined on , then (according to the extension theorem) it is uniquely determined on by the values of the distribution functions Fμ1μ2...μn.

We may now ask the following. Under what conditions does a system of distribution functions Fμ1μ2...μn given a priori define a field of probability on (and, consequently, on )?

We must first note that every distribution function Fμ1μ2...μn must satisfy the conditions given in § 3, III of the second chapter; indeed this is contained in the very concept of distribution function. Besides, as a result of formulas (13) and (14) in §2, we have also the following relations:

where k < n and is an arbitrary permutation. These necessary conditions prove also to be sufficient, as will appear from the following theorem.

FUNDAMENTAL THEOREM: Every system of distribution functions Fμ1μ2...μn, satisfying the conditions (2) and (3), defines a probability function on , which satisfies Axioms I - VI. This probability function can be extended (by the extension theorem) to also.

Proof. Given the distribution functions Fμ1μ2...μn, satisfying the general conditions of Chap. II, § 3, III and also conditions (2) and (3). Every distribution function Fμ1μ2...μn defines uniquely a corresponding probability function for all Borel sets of Rn (cf. § 3). We shall deal in the future only with Borel sets of Rn and with Borel cylinder sets in E.

For every cylinder set

we set

Since the same cylinder set A can be defined by various sets A′, we must first show that formula (4) yields always the same value for .

Let (xμ1, xμ2,..., xμn) be a finite system of random variables xμ. Proceeding from the probability function of these random variables, we can, in accordance with the rules in § 3, define the probability function of each subsystem (xμi1, xμi2, ..., xμik). From equations (2) and (3) it follows that this probability function defined according to § 3 is the same as the function given a priori. We shall now suppose that the cylinder set A is defined by means of

and simultaneously by means of

where all random variables xμi and xμj belong to the system (xμ1, xμ2, ..., xμn), which is obviously not an essential restriction. The conditions

and

are equivalent. Therefore

which proves our statement concerning the uniqueness of the definition of .

Let us now prove that the field of probability satisfies all the Axioms I - VI. Axiom I requires merely that be a field. This fact has already been proven above. Moreover, for an arbitrary μ:

which proves that Axioms II and IV apply in this case. Finally, from the definition of it follows at once that is nonnegative (Axiom III).

It is only slightly more complicated to prove that Axiom V is also satisfied. In order to do so, we investigate two cylinder sets

and

We shall assume that all variables xμi and xμj belong to one inclusive finite system (xμ1, xμ2, ...xμn). If the sets A and B do not intersect, the relations

and

are incompatible. Therefore

which concludes our proof.

Only Axiom VI remains. Let

be a decreasing sequence of cylinder sets satisfying the condition

We shall prove that the product of all sets An is not empty. We may assume, without essentially restricting the problem, that in the definition of the first n cylinder sets Ak, only the first n coordinates xμk in the sequence

occur, i.e.

For brevity we set

then, obviously

In each set Bn it is possible to find a closed bounded set Un such that

From this inequality we have for the set

the inequality

Let, morever,

From (5) it follows that

Since Wn ⊂ Vn ⊂ An, it follows that

If ε is sufficiently small, and Wn is not empty. We shall now choose in each set Wn a point ξ(n) with the coordinates . Every point ξ(n + p), p = 0, 1, 2, ... , belongs to the set Vn; therefore

Since the sets Un are bounded we may (by the diagonal method) choose from the sequence {ξ(n)} a subsequence

for which the corresponding coordinates tend for any k to a definite limit xk. Let, finally, ξ be a point in set E with the coordinates

As the limit of the sequence , i = 1, 2, 3, ..., the point (x1, x2, ..., xk) belongs to the set Uk. Therefore, ξ belongs to

for any k and therefore to the product

§ 5. Equivalent Random Variables; Various Kinds of Convergence

Starting with this paragraph, we deal exclusively with Borel fields of probability. As we have already explained in § 2 of the second chapter, this does not constitute any essential restriction on our investigations.

Two random variables x and y are called equivalent, if the probability of the relation x ≠ y is equal to zero. It is obvious that two equivalent random variables have the same probability function:

Therefore, the distribution functions F(x) and F(y) are also identical. In many problems in the theory of probability we may substitute for any random variable any equivalent variable.

Now let

be a sequence of random variables. Let us study the set A of all elementary events ξ for which the sequence (1) converges. If we denote by the sets of ξ for which all the following inequalities hold

then we obtain at once

According to § 3, the set always belongs to the field . The relation (2) shows that A, too, belongs to . We may, therefore, speak of the probability of convergence of a sequence of random variables, for it always has a perfectly definite meaning.

Now let the probability of the convergence set A be equal to unity. We may then state that the sequence (1) converges with the probability one to a random variable x, where the random variable x is uniquely defined except for equivalence. To determine such a random variable we set

on A, and x = 0 outside of A. We have to show that x is a random variable, in other words, that the set A(a) of the elements ξ for which x < a, belongs to . But

in case , and

in the opposite case, from which our statement follows at once.

If the probability of convergence of the sequence (1) to x equals one, then we say that the sequence (1) converges almost surely to x. However, for the theory of probability, another conception of convergence is possibly more important.

DEFINITION. The sequence x1, x2, ... , xn, . . . of random variables converges in probability (converge en probabilité) to the random variable x, if for any ε > 0, the probability

tends toward zero as 5.

I. If the sequence (1) converges in probability to x and also to x′, then x and x′ are equivalent. In fact

since the last probabilities are as small as we please for a sufficiently large n it follows that

and we obtain at once that

II. If the sequence (1) almost surely converges to x, then it also converges to x in probability. Let A be the convergence set of the sequence (1); then

from which the convergence in probability follows.

III. For the convergence in probability of the sequence (1) the following condition is both necessary and sufficient: For any ξ > 0 there exists an n such that, for every p > 0, the following inequality holds:

Let F1(a), F2(a), . . . , Fn(a), . . . , F(a) be the distribution functions of the random variables x1 x2, . . . , xn, . . . , x. If the sequence xn converges in probability to x, the distribution function F(a) is uniquely determined by knowledge of the functions Fn(a). We have, in fact,

THEOREM: If the sequence x1, x2, . . . , xn, . . . converges in probability to x, the corresponding sequence of distribution functions Fn(a) converges at each point of continuity of F(a) to the distribution function F(a) of x.

That F(a) is really determined by the Fn(a) follows from the fact that F(a), being a monotone function, continuous on the left, is uniquely determined by its values at the points of continuity6. To prove the theorem we assume that F is continuous at the point a. Let a′ < a; then in case x < a′, it is necessary that |xn − x| > a − a′. Therefore

In an analogous manner, we can prove that from a″ > a there follows the relation

Since F(a′) and F(a″) converge to F(a) for and , it follows from (3) and (4) that

which proves our theorem.

1 The ar may also assume the infinite values ±∞.

2 Cf. § 3, IV in the Second Chapter.

3 Cf. HAUSDORFF, Mengenlehre, 1927, p. 23.

4 From the above it follows that Borel cylinder sets are Borel sets definable by relations of type (1). Now let A and B be two Borel cylinder sets defined by the relations

Then we can define the sets A + B, AB, and A − B respectively by the relations

where ω(x) = 0 for x ≠ 0 and ω(0) = 1 If f and g are Borel functions, so also are f · g, f2 + g2 and f2 + ω(g); therefore, A + B, AB and A − B are Borel cylinder sets. Thus we have shown that the system of sets is a field.

5 This concept is due to Bernoulli; its completely general treatment was introduced by E. E. Slutsky (see [1]).

6 In fact, it has at most only a countable set of discontinuities (see LEBESGUE, Leçons sur l’intégration, 1928, p. 50. Therefore, the points of continuity are everywhere dense, and the value of the function F(a) at a point of discontinuity is determined as the limit of its values at the points of continuity on its left.

Chapter IV

MATHEMATICAL EXPECTATIONS1

