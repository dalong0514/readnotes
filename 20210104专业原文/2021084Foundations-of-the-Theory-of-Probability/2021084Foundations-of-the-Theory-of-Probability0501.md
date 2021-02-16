# 0501. CONDITIONAL PROBABILITIES AND MATHEMATICAL EXPECTATIONS

§ 1. Conditional Probabilities

In § 6, Chapter I, we defined the conditional probability, , of the event B with respect to trial . It was there assumed that allows of only a finite number of different possible results. We can, however, define also for the case of an with an infinite set of possible results, i.e. the case in which the set E is partitioned into an infinite number of non-intersecting subsets. In particular, we obtain such a partitioning if we consider an arbitrary function u of ξ and define as elements of the partition the sets u = constant. The conditional probability we also denote by . Any partitioning of the set E can be defined as the partitioning which is「induced」by a function u of ξ, if one assigns to every ξ, as u(ξ), that set of the partitioning of E which contains ξ.

Two functions u and u′ of ξ determine the same partitioning of the set E if and only if there exists a one-to-one correspondence u′ = f(u) between their domains and such that u′(ξ) is identical with fu(ξ). The reader can easily show that the random variables and , defined below, are in this case the same. They are thus determined, in fact, by the partition itself.

To define we may use the following equation:

It is easy to prove that if the set E(u) of all possible values of u is finite, equation (1) holds true for any choice of A (when is defined as in § 6, Chap. I). In the general case (in which is not yet defined) we shall prove that there always exists one and only one random variable (except for the matter of equivalence) which is defined as a function of u and which satisfies equation (1) for every choice of A from such that . The function of u thus determined to within equivalence, we call the conditional probability of B with respect to u (or, for a given u). The value of when u = a we shall designate by .

The proof of the existence and uniqueness of . If we multiply (1) by , we obtain, on the left,

and, on the right,

leading to the formula

and conversely (1) follows from (2). In the case , in which case (1) is meaningless, equation (2) becomes trivially true. Condition (2) is thus equivalent to (1). In accordance with Property IX of the integral (§ 1, Chap. IV) the random variable x is uniquely defined (except for equivalence) by means of the values of the integral

for all sets of . Since is a random variable determined on the probability field (, , it follows that formula (2) uniquely determines this variable except for equivalence.

We must still prove the existence of . We shall apply here the following theorem of Nikodym1:

Let be a Borel field, a non-negative completely additive set function defined on (in the terminology of the probability theory, a random variable on ), and let Q(A) be another completely additive set function defined on , such that from Q(A) ≠ 0 follows the inequality . Then there exists a function f(ξ) (in the terminology of the theory of probability, a random variable) which is measurable with respect to , and which satisfies, for each set A of , the equation

In order to apply this theorem to our case, we need to prove 1° that

is a completely additive function on , 2°. that from Q(A) ≠ 0 follows the inequality .

Firstly, 2° follows from

For the proof of 1° we set

then

and

Since is completely additive, it follows that

which was to be proved.

From the equation (1) follows an important formula (if we set A = E(u)):

Now we shall prove the following two fundamental properties of conditional probability.

THEOREM I. It is almost sure that

THEOREM II. If B is decomposed into at most a countable number of sets Bn:

then the following equality holds almost surely:

These two properties of correspond to the two characteristic properties of the probability function : that always, and that is completely additive. These allow us to carry over many other basic properties of the absolute probability to the conditional probability . However, we must not forget that is, for a fixed set B, a random variable determined uniquely only to within equivalence.

Proof of Theorem I. If we assume — contrary to the assertion to be proved — that on a set M ⊂ E(u) with , the inequality ,, holds true, then according to formula (1)

which is obviously impossible. In the same way we prove that almost surely .

Proof of Theorem II. From the convergence of the series

it follows from Property V of mathematical expectation (Chap. IV, § 2) that the series

almost surely converges. Since the series

converges for every choice of the set A such that , then from Property V of mathematical expectation just referred to it follows that for each A of the above kind we have the relation

and from this, equation (5) immediately follows.

To close this section we shall point out two particular cases. If, first, u(ξ) = c (a constant), then almost surely. If, however, we set u(ξ) = ξ, then we obtain at once that is almost surely equal to one on A and is almost surely equal to zero on Ā. is thus revealed to be the characteristic function of set A.

§ 2. Explanation of a Borel Paradox

Let us choose for our basic set E the set of all points on a spherical surface. Our will be the aggregate of all Borel sets of the spherical surface. And finally, our is to be proportional to the measure of set A. Let us now choose two diametrically opposite points for our poles, so that each meridian circle will be uniquely defined by the longitude . Since ψ varies from 0 only to π,  —  in other words, we are considering complete meridian circles (and not merely semicircles)  —  the latitude Θ must vary from  — π to +π (and not from to ). Borel set the following problem: Required to determine「the conditional probability distribution」of latitude Θ, , for a given longitude ψ.

It is easy to calculate that

The probability distribution of Θ for a given ψ is not uniform.

If we assume that the conditional probability distribution of Θ「with the hypothesis that ξ lies on the given meridian circle」must be uniform, then we have arrived at a contradiction.

This shows that the concept of a conditional probability with regard to an isolated given hypothesis whose probability equals 0 is inadmissible. For we can obtain a probability distribution for Θ on the meridian circle only if we regard this circle as an element of the decomposition of the entire spherical surface into meridian circles with the given poles.

§ 3. Conditional Probabilities with Respect to a Random Variable

If x is a random variable and as a function of x is measurable in the Borel sense, then can be defined in an elementary way. For we can rewrite formula (2) in § 1, to look as follows:

In this case we obtain from (1) at once that

In accordance with a theorem of Lebesgue2 it follows from (2) that

which is always true except for a set H of points a for which .

was defined in § 1 except on a set G, which is such that . If we now regard formula (3) as the definition of (setting when the limit in the right hand side of (3) fails to exist), then this new variable satisfies all requirements of § 1.

If, besides, the probability densities f(x)(a) and exist and if f(x)(a) > 0, then formula (3) becomes

Moreover, from formula (3) it follows that the existence of a limit in (3) and of a probability density f(x)(a) results in the existence of . In that case

If , then from (4) we have

In case f(x)(a) = 0, then according to (5) and therefore (6) also holds. If, besides, the distribution of x is continuous, we have

From (6) and (7) we obtain

This equation gives us the so-called Bayes Theorem for continuous distributions. The assumptions under which this theorem is proved are these: is measurable in the Borel sense and at the point a is defined by formula (3), the distribution of x is continuous, and at the point a there exists a probability density f(x)(a).

§ 4. Conditional Mathematical Expectations

Let u be an arbitrary function of ξ, and y a random variable. The random variable , representable as a function of u and satisfying, for any set A of with , the condition

is called (if it exists) the conditional mathematical expectation of the variable y for known value of u.

If we multiply (1) by , we obtain

Conversely from (2) follows formula (1). In case , in which case (1) is meaningless, (2) becomes trivial. In the same manner as in the case of conditional probability (§ 1) we can prove that is determined uniquely — except for equivalence — by (2).

The value of for u = a we shall denote by . Let us also note that , as well as , depends only upon the partition and may be designated by .

The existence of is implied in the definition of (if we set A = E(u), then .

We shall now prove that the existence of is also sufficient for the existence of . For this we only need to prove that by the theorem of Nikodym (§ 1), the set function

is completely additive on and absolutely continuous with respect to . The first property is proved verbatim as in the case of conditional probability (§ 1). The second property — absolute continuity — is contained in the fact that from Q(A) ≠ 0 the inequality must follow. If we assume that , it is clear that

and our second requirement is thus fulfilled.

If in equation (1) we set A = E(u), we obtain the formula

We can show further that almost surely

where a and b are two arbitrary constants. (The proof is left to the reader.)

If u and v are two functions of the elementary event ξ, then the couple (u, v) can always be regarded as a function of ξ. The following important equation then holds:

For, is defined by the relation

Therefore we must show that satisfies the equation

From the definition of it follows that

From the definition of it follows, moreover, that

Equation (6) results from equations (7) and (8) and thus proves our statement.

If we set equal to one on B and to zero outside of B, then

In this case, from formula (5) we obtain the formula

The conditional mathematical expectation may also be defined directly by means of the corresponding conditional probabilities. To do this we consider the following sums:

If exists, the series (10) almost certainly* converges. For we have from formula (3), of § 1,

and the convergence of the series

is the necessary condition for the existence of (see Chap. IV, § 1). From this convergence it follows that the series (10) converges almost certainly (see Chap. IV, § 2, V). We can further show, exactly as in the theory of the Lebesgue integral, that from the convergence of (10) for some λ, its convergence for every λ follows, and that in the case where series (10) converges, Sλ(u) tends to a definite limit as 3. We can then define

To prove that the conditional expectation defined by relation (11) satisfies the requirements set forth above, we need only convince ourselves that , as determined by (11), satisfies equation (1). We prove this fact thus:

The interchange of the mathematical expectation sign with the limit sign is admissible in this computation, since Sλ(u) converges uniformly to as (a simple result of Property V of mathematical expectation in § 2). The interchange of the mathematical expectation sign and the summation sign is also admissible since the series

converges (an immediate result of Property V of mathematical expectation).

Instead of (11) we may write

We must not forget here, however, that (12) is not an integral in the sense of § 1, Chap. IV, so that (12) is only a symbolic expression.

If x is a random variable then we call the function of x and a

the conditional distribution function of y for known x.

Fx(y)(a) is almost certainly defined for every a. If a < b then almost certainly

From (11) and (10) it follows4 that almost certainly

This fact can be expressed symbolically by the formula

By means of the new definition of mathematical expectation [(10) and (11)] it is easy to prove that, for a real function of u,

1 O. NIKODYM, Sur une généralisation des intégrales de M. J. Ra don, Fund. Math. v. 15, 1930 p. 168 (Theorem III).

2 Lebesgue, l. c., 1928, pp. 301-302.

* We use almost certainly interchangeably with almost surely.

3 In this case we consider only a Countable sequence of values of λ; then all probabilities are almost certainly defined for all these values of λ.

4 Cf. footnote 3.

