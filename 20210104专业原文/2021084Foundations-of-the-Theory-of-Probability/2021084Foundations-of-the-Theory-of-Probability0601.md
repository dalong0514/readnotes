# 0601. INDEPENDENCE; THE LAW OF LARGE NUMBERS

§ 1. Independence

DEFINITION 1: Two functions, u and v of ξ, are mutually independent if for any two sets, A of , and B of , the following equation holds:

If the sets E(u) and E(v) consist of only a finite number of elements,

then our definition of independence of u and v is identical with the definition of independence of the partitions

as in § 5, Chap. I.

For the independence of u and v, the following condition is necessary and sufficient. For any choice of set A in the following equation holds almost certainly:

In the case , both equations (1) and (2) are satisfied, and therefore we need only prove their equivalence in the case . In this case (1) is equivalent to the relation

and therefore to the relation

On the other hand, it is obvious that equation (4) follows from (2). Conversely since is uniquely determined by (4) to within probability zero, then equation (2) follows from (4) almost certainly.

DEFINITION 2: Let M be a set of functions uμ(ξ) of ξ. These functions are called mutually independent in their totality if the following condition is satisfied. Let M′ and M″ be two nonintersecting subsets of M, and let A′ (or A″) be a set from defined by a relation among from uμ from M′ (or M″); then we have

The aggregate of all uμ of M′ (or of M″) can be regarded as coordinates of some function u′ (or u″). Definition 2 requires only the independence of u′ and u″ in the sense of Definition 1 for each choice of non-intersecting sets M′ and M″.

If u1, u2, . . . , un are mutually independent, then in all cases

provided the sets Ak belong to the corresponding (proved by induction). This equation is not in general, however, at all sufficient for the mutual independence of u1, u2, . . . , un.

Equation (5) is easily generalized for the case of a countably infinite product.

From the mutual independence of uμk in each finite group (uμ1, uμ2, . . . , uμk) it does not necessarily follow that all uμ are mutually independent.

Finally, it is easy to note that the mutual independence of the functions uμ is in reality a property of the corresponding partitions . Further, if are single-valued functions of the corresponding uμ, then from the mutual independence of uμ follows that of .

§ 2 Independent Random Variables

If x1, x2, . . . , xn are mutually independent random variables then from equation (2) of the foregoing paragraph follows, in particular, the formula

If in this case the field consists only of Borel sets of the space Rn, then condition (1) is also sufficient for the mutual independence of the variables x1, x2, . . . , xn.

Proof. Let x′ = (xi1, xi2, . . . , xik) and x″ = (xj1, xj2, . . . , xjm) be two non-intersecting subsystems of the variables x1, x2, . . . , xn. We must show, on the basis of formula (1), that for every two Borel sets A′ and A″ of Rk (or Rm) the following equation holds:

This follows at once from (1) for the sets of the form

It can be shown that this property of the sets A′ and A″ is preserved under formation of sums and differences, from which equation (2) follows for all Borel sets.

Now let x = {xμ} be an arbitrary (in general infinite) aggregate of random variables. If the field coincides with the field (M is the set of all μ), the aggregate of equations

is necessary and sufficient for the mutual independence of the variables xμ.

The necessity of this condition follows at once from formula (1) . We shall now prove that it is also sufficient. Let M′ and M″ be two non-intersecting subsets of the set M of all indices μ, and let A′ (or A″) be a set of defined by a relation among the xμ with indices μ from M′ (or M″). We must show that we then have

If A′ and A″ are cylinder sets then we are dealing with relations among a finite set of variables xμ, equation (4) represents in that case a simple consequence of previous results (Formula (2)). And since relation (4) holds for sums and differences of sets A′ (or A″) also, we have proved (4) for all sets of as well.

Now for every μ of a set M let there be given a priori a distribution function Fμ(a); in that case we can construct a field of probability such that certain random valuables xμ in that field (μ assuming all values in M) will be mutually independent, where xμ will have for its distribution function the Fμ(a) given a priori. In order to show this it is enough to take RM for the basic set E and for the field , and to define the distribution functions Fμ1 μ2 . . . μn(see Chap. III, § 4) by equation (3).

Let us also note that from the mutual independence of each finite group of variables xμ (equation (3)) there follows, as we have seen above, the mutual independence of all on . In more inclusive fields of probability this property may be lost.

To conclude this section, we shall give a few more criteria for the independence of two random variables.

If two random variables x and y are mutually independent and if and are finite then almost certainly

These formulas represent an immediate consequence of the second definition of conditional mathematical expectation (Formulas (10) and (11) of Chap. V, § 4). Therefore, in the case of independence both

are equal to zero (provided σ2(x) > 0 and σ2(y) > 0). The number f2 is called the correlation ratio of y with respect to x, and g2 the same for x with respect to y (Pearson).

From (5) it further follows that

To prove this we apply Formula (15) of § 4, Chap. V:

Therefore, in the case of independence

is also equal to zero; r, as is well known, is the correlation coefficient of x and y.

If two random variables x and y satisfy equation (6), then they are called uncorrelated. For the sum

where the x1, x2, . . . , xn are uncorrelated in pairs, we can easily compute that

In particular, equation (7) holds for the independent variables xk.

§ 3. The Law of Large Numbers

Random variables s of a sequence

are called stable, if there exists a numerical sequence

such that for any positive

converges to zero as . If all exist and if we may set

then the stability is normal.

If all sn are uniformly bounded, then from

we obtain the relation

and therefore

The stability of a bounded stable sequence is thus necessarily normal.

Let

According to the Tchebycheff inequality,

Therefore, the Markov Condition

is sufficient for normal stability.

If are uniformly bounded:

then from the inequality (9) in § 3, Chap. IV,

Therefore, in this case the Markov condition (3) is also necessary for the stability of the sn.

If

and the variables xn are uncorrelated in pairs, we have

Therefore, in this case, the following condition is sufficient for the normal stability of the arithmetical means sn:

(Theorem of Tchebycheff). In particular, condition (4) is fulfilled if all variables xn are uniformly bounded.

This theorem can be generalized for the case of weakly correlated variables xn. If we assume that the coefficient of correlation rmn1 of xm and xn satisfies the inequality

and that

then a sufficient condition for normal stability of the arithmetic means s is2

In the case of independent summands xn we can state a necessary and sufficient condition for the stability of the arithmetic means sn. For every xn there exists a constant mn (the median of xn) which satisfies the following conditions:

We set

Then the relations

are necessary and sufficient for the stability of variables sn3.

We may here assume the constants dn to be equal to the so that in the case where

(and only in this case) the stability is normal.

A further generalization of Tchebycheff’s theorem is obtained if we assume that the sn depend in some way upon the results of any n trials,

so that after each definite outcome of all these n trials sn assumes a definite value. The general idea of all these theorems known as the law of large numbers, consists in the fact that if the dependence of variables sn upon each separate trial is very small for a large n, then the variables sn are stable. If we regard

as a reasonable measure of the dependence of variables sn upon the trial , then the above-mentioned general idea of the law of large numbers can be made concrete by the following considerations4.

Let

Then

We can easily compute also that the random variables znk (k = 1, 2, . . . , n) are uncorrelated. For let i < k; then5

and therefore

We thus have

Therefore, the condition

is sufficient for the normal stability of the variables sn.

§ 4. Notes on the Concept of Mathematical Expectation

We have defined the mathematical expectation of a random variable x as

where the integral on the right is understood as

The idea suggests itself to consider the expression

as a generalized mathematical expectation. We lose in this case, of course, several simple properties of mathematical expectation. For example, in this case the formula

is not always true. In this form the generalization is hardly admissible. We may add however that, with some restrictive supplementary conditions, definition (2) becomes entirely natural and useful.

We can discuss the problem as follows. Let

be a sequence of mutually independent variables, having the same distribution function F(x)(a) = F(xn)(a), (n = 1, 2, . . .) as x. Let further

We now ask whether there exists a constant such that for every

The answer is: If such a constant exists, it is expressed by Formula (2). The necessary and sufficient condition that Formula (3) hold consists in the existence of limit (2) and the relation

To prove this we apply the theorem that condition (4) is necessary and sufficient for the stability of the arithmetic means sn, where, in the case of stability, we may set6

If there exists a mathematical expectation in the former sense (Formula (1)), then condition (4) is always fulfilled7. Since in this case , the condition (3) actually does define a generalization of the concept of mathematical expectation. For the generalized mathematical expectation, Properties I - VII (Chap. IV, § 2) still hold; in general, however, the existence of does not follow from the existence of .

To prove that the new concept of mathematical expectation is really more general than the previous one, it is sufficient to give the following example. Set the probability density f(x)(a) equal to

where the constant C is determined by

It is easy to compute that in this case condition (4) is fulfilled. Formula (2) gives the value

but the integral

diverges.

§ 5. Strong Law of Large Numbers; Convergence of Series

The random variables sn of the sequence

are strongly stable if there exists a sequence of numbers

such that the random variables

almost certainly tend to zero as n → +∞. From strong stability follows, obviously, ordinary stability. If we can choose

then the strong stability is normal.

In the Tchebycheff case,

where the variables xn are mutually independent. A sufficient8 condition for the normal strong stability of the arithmetic means sn is the convergence of the series

This condition is the best in the sense that for any series of constants bn such that

we can build a series of mutually independent random variables xn such that

and the corresponding arithmetic means sn will not be strongly stable.

If all xn have the same distribution function F(x)(a), then the existence of the mathematical expectation

is necessary and sufficient for the strong stability of sn; the stability in this case is always normal9.

Again, let

be mutually independent random variables. Then the probability of convergence of the series

is equal either to one or to zero. In particular, this probability equals one when both series

converge. Let us further assume

Then in order that series (1) converge with the probability one, it is necessary and sufficient10 that the following series converge simultaneously:

1 It is obvious that rnn = 1 always.

2 Cf. A. KHINTCHINE, Sur la loi forte des grandes nombres. C. R. de l’acad. sci. Paris v. 186, 1928, p. 285.

3 Cf. A. KOLMOGOROV. Über die Summen durch den Zufall bestimmter unabhängiger Grössen, Math. Ann. v. 99, 1928, pp. 309-319 (corrections and notes to this study, v. 102, 1929 pp. 484-488, Theorem VIII and a supplement on p. 318).

4 Cf. A. KOLMOGOROV. Sur la loi des grandes nombres. Rend. Accad. Lincei v. 9, 1929 pp. 470-474.

5 Application of Formula (15) in § 4, Chap. V.

6 Cf. A. KOLMOGOROV, Bemerkungen zu meiner Arbeit,「Über die Summen zufälliger Grössen.」Math. Ann. v. 102, 1929, pp. 484-488, Theorem XII.

7 Ibid, Theorem XIII.

8 Cf. A. KOLMOGOROV, Sur la loi forte des grandes nombres , C. R. Acad. Sci. Paris v. 191, 1930, pp. 910-911.

9 The proof of this statement has not yet been published.

10 Cf. A. KHINTCHINE and A. KOLMOGOROV, On the Convergence of Series, Rec. Math. Soc. Moscow, v. 32, 1925, p. 668-677.