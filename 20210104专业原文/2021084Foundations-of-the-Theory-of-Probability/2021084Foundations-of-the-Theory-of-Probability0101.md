# 0101. Elementary Theory of Probability

We define as elementary theory of probability that part of the theory in which we have to deal with probabilities of only a finite number of events. The theorems which we derive here can be applied also to the problems connected with an infinite number of random events. However, when the latter are studied, essentially new principles are used. Therefore the only axiom of the mathematical theory of probability which deals particularly with the case of an infinite number of random events is not introduced until the beginning of Chapter II (Axiom VI).

The theory of probability, as a mathematical discipline, can and should be developed from axioms in exactly the same way as Geometry and Algebra. This means that after we have defined the elements to be studied and their basic relations, and have stated the axioms by which these relations are to be governed, all further exposition must be based exclusively on these axioms, independent of the usual concrete meaning of these elements and their relations.

In accordance with the above, in § 1 the concept of a field of probabilities is defined as a system of sets which satisfies certain conditions. What the elements of this set represent is of no importance in the purely mathematical development of the theory of probability (cf. the introduction of basic geometric concepts in the Foundations of Geometry by Hilbert, or the definitions of groups, rings and fields in abstract algebra).

Every axiomatic (abstract) theory admits, as is well known, of an unlimited number of concrete interpretations besides those from which it was derived. Thus we find applications in fields of science which have no relation to the concepts of random event and of probability in the precise meaning of these words.

The postulational basis of the theory of probability can be established by different methods in respect to the selection of axioms as well as in the selection of basic concepts and relations. However, if our aim is to achieve the utmost simplicity both in the system of axioms and in the further development of the theory, then the postulational concepts of a random event and its probability seem the most suitable. There are other postulational systems of the theory of probability, particularly those in which the concept of probability is not treated as one of the basic concepts, but is itself expressed by means of other concepts.[1] However, in that case, the aim is different, namely, to tie up as closely as possible the mathematical theory with the empirical development of the theory of probability.

## 1.1 Axioms [2]

Let E be a collection of elements ξ, η, ζ, . . ., which we shall call elementary events, and a set of subsets of E; the elements of the set will be called random events.

I. δ is a field [3] of sets.

II. δ contains the set E.

III. To each set A in δ is assigned a non-negative real number. This number P(A) is called the probability of the event A.

IV. P(E) equals 1.

V. If A and B have no element in common, then `P(A+B) = P(A)+P(B).`

A system of sets, δ, together with a definite assignment of numbers P(A), satisfying Axioms I-V, is called a field of probability.

Our system of Axioms I-V is consistent. This is proved by the following example. Let E consist of the single element ξ and let δ consist of E and the null set 0. P(E) is then set equal to 1 and P(0) equals 0.

Our system of axioms is not, however, complete, for in various problems in the theory of probability different fields of probability have to be examined.

The Construction of Fields of Probability. The simplest fields of probability are constructed as follows. We take an arbitrary finite set E = {ξ1, ξ2, . . ., ξk} and an arbitrary set of non-negative numbers with the sum p1 + p2 + . . . + pk = 1. δ is taken as the set of all subsets in E, and we put

$$P\{ξ_{i1}, ξ_{i2}, . . ., ξ_{iλ}\} = p_{i1} + p_{i2} + ... + p_{iλ}$$

In such cases, p1, p2, . . ., pk are called the probabilities of the elementary events ξ1, ξ2, . . ., ξk or simply elementary probabilities. In this way are derived all possible finite fields of probability in which δ consists of the set of all subsets of E. (The field of probability is called finite if the set E is finite.) For further examples see Chap. II, § 3.

## 1.2 The Relation to Experimental Data [4]

We apply the theory of probability to the actual world of experiments in the following manner:

1 There is assumed a complex of conditions,, which allows of any number of repetitions.

2 We study a definite set of events which could take place as a result of the establishment of the conditions . In individual cases where the conditions are realized, the events occur, generally, in different ways. Let E be the set of all possible variants ξ1, ξ2, . . . of the outcome of the given events. Some of these variants might in general not occur. We include in set E all the variants which we regard a priori as possible.

3 If the variant of the events which has actually occurred upon realization of conditions belongs to the set A (defined in any way), then we say that the event A has taken place.





Example: Let the complex of conditions be the tossing of a coin two times. The set of events mentioned in Paragraph 2) consists of the fact that at each toss either a head or tail may come up. From this it follows that only four different variants (elementary events) are possible, namely: HH, HT, TH, TT. If the「event A」connotes the occurrence of a repetition, then it will consist of a happening of either of the first or fourth of the four elementary events. In this manner, every event may be regarded as a set of elementary events.

4) Under certain conditions, which we shall not discuss here, we may assume that to an event A which may or may not occur under conditions, is assigned a real number which has the following characteristics:

(a) One can be practically certain that if the complex of conditions is repeated a large number of times, n, then if m be the number of occurrences of event A, the ratio m/n will differ very slightly from .

(b) If is very small, one can be practically certain that when conditions are realized only once, the event A would not occur at all.

The Empirical Deduction of the Axioms. In general, one may assume that the system of the observed events A, B, C, . . . to which are assigned definite probabilities, form a field containing as an element the set E (Axioms I, II, and the first part of III, postulating the existence of probabilities). It is clear that so that the second part of Axiom III is quite natural. For the event E, m is always equal to n, so that it is natural to postulate (Axiom IV). If, finally, A and B are non-intersecting (incompatible), then m = m1 + m2 where m, m1, m2 are respectively the number of experiments in which the events A + B, A, and B occur. From this it follows that

It therefore seems appropriate to postulate that (Axiom V).

Remark 1. If two separate statements are each practically reliable, then we may say that simultaneously they are both reliable, although the degree of reliability is somewhat lowered in the process. If, however, the number of such statements is very large, then from the practical reliability of each, one cannot deduce anything about the simultaneous correctness of all of them. Therefore from the principle stated in (a) it does not follow that in a very large number of series of n tests each, in each the ratio m/n will differ only slightly from .

Remark 2. To an impossible event (an empty set) corresponds, in accordance with our axioms, the probability 5, but the converse is not true: does not imply the impossibility of A. When, from principle (b) all we can assert is that when the conditions are realized but once, event A is practically impossible. It does not at all assert, however, that in a sufficiently long series of tests the event A will not occur. On the other hand, one can deduce from the principle (a) merely that when and n is very large, the ratio m/n will be very small (it might, for example, be equal to 1/n).

## 1.3 Notes on Terminology

We have defined the objects of our future study, random events, as sets. However, in the theory of probability many set-theoretic concepts are designated by other terms. We shall give here a brief list of such concepts.

Theory of Sets

Random Events

1. A and B do not intersect, i.e., AB = 0.

1. Events A and B are incompatible.

2. AB. . . N = 0.

2. Events A, B, . . ., N are incompatible.

3. AB . . . N = X.

3. Event X is defined as the simultaneous occurrence of events A, B, . . ., N.

4. .

4. Event X is defined as the occurrence of at least one of the events A, B, . . ., N.

5. The complementary set Ā.

5. The opposite event Ā consisting of the non-occurence of event A.

6. A = 0.

6. Event A is impossible.

7. A = E.

7. Event A must occur.

8. The system of the sets A1, A2, . . ., An forms a decomposition of the set E if A1 + A2 + . . . + An = E.

(This assumes that the sets Ai do not intersect, in pairs.)

8. Experiment consists of determining which of the events Al, A2, . . ., An occurs. We therefore call A1, A2, . . ., An the possible results of experiment .

9. B is a subset of A: B⊂A.

9. From the occurrence of event B follows the inevitable occurrence of A.

## 1.4 Immediate Corollaries of the Axioms; Conditional Probabilities; Theorem of Bayes

From A + Ā = E and the Axioms IV and V it follows that

Since Ē = 0, then, in particular,

If A, B, . . ., N are incompatible, then from Axiom V follows the formula (the Addition Theorem)

If, then the quotient

is defined to be the conditional probability of the event B under the condition A.

From (5) it follows immediately that

And by induction we obtain the general formula (the Multiplication Theorem)

The following theorems follow easily:

Comparing formulae (8) — (10) with axioms III — V, we find that the system of sets together with the set function (provided A is a fixed set), form a field of probability and therefore, all the above general theorems concerning hold true for the conditional probability (provided the event A is fixed).

It is also easy to see that

From (6) and the analogous formula

we obtain the important formula:

which contains, in essence, the Theorem of Bayes.

THE THEOREM ON TOTAL PROBABILITY: Let A1 + A2 + . . . + An = E (this assumes that the events A1, A2, . . ., An are mutually exclusive) and let X be arbitrary. Then

Proof:

using (4) we have

and according to (6) we have at the same time

THE THEOREM OF BAYES: Let A1 + A2 + . . . + An = E and X be arbitrary, then,

A1, A2, . . ., An are often called「hypotheses」and formula (14) is considered as the probability of the hypothesis Ai after the occurrence of event X. [ then denotes the a priori probability of Ai.]

Proof: From (12) we have

To obtain the formula (14) it only remains to substitute for the probability its value derived from (13) by applying the theorem on total probability.

## 1.5 Independence

The concept of mutual independence of two or more experiments holds, in a certain sense, a central position in the theory of probability. Indeed, as we have already seen, the theory of probability can be regarded from the mathematical point of view as a special application of the general theory of additive set functions. One naturally asks, how did it happen that the theory of probability developed into a large individual science possessing its own methods?

In order to answer this question, we must point out the specialization undergone by general problems in the theory of additive set functions when they are proposed in the theory of probability.

The fact that our additive set function is non-negative and satisfies the condition, does not in itself cause new difficulties. Random variables (see Chap. III) from a mathematical point of view represent merely functions measurable with respect to, while their mathematical expectations are abstract Lebesgue integrals. (This analogy was explained fully for the first time in the work of Fréchet6.) The mere introduction of the above concepts, therefore, would not be sufficient to produce a basis for the development of a large new theory.

Historically, the independence of experiments and random variables represents the very mathematical concept that has given the theory of probability its peculiar stamp. The classical work or LaPlace, Poisson, Tchebychev, Markov, Liapounov, Mises, and Bernstein is actually dedicated to the fundamental investigation of series of independent random variables. Though the latest dissertations (Markov, Bernstein and others) frequently fail to assume complete independence, they nevertheless reveal the necessity of introducing analogous, weaker, conditions, in order to obtain sufficiently significant results (see in this chapter § 6, Markov chains).

We thus see, in the concept of independence, at least the germ of the peculiar type of problem in probability theory. In this book, however, we shall not stress that fact, for here we are interested mainly in the logical foundation for the specialized investigations of the theory of probability.

In consequence, one of the most important problems in the philosophy of the natural sciences is — in addition to the well-known one regarding the essence of the concept of probability itself — to make precise the premises which would make it possible to regard any given real events as independent. This question, however, is beyond the scope of this book.

Let us turn to the definition of independence. Given n experiments, that is, n decompositions

of the basic set E. It is then possible to assign r = r1r2. . . rn probabilities (in the general case)

which are entirely arbitrary except for the single condition7 that

DEFINITION I. n experiments are called mutually independent, if for any q1, q2, . . ., qn the following equation holds true:

Among the r equations in (2), there are only r−r1−r2− . . . −rn + n − 1 independent equations8.

THEOREM I. If n experiments are mutually independent, then any m of them (m < n),, are also independent9.

In the case of independence we then have the equations:

(all ik must be different.)

DEFINITION II. n events A1, A2, . . ., An are mutually independent, if the decompositions (trials)

are independent.

In this case r1 = r2 = . . . = rn = 2, r = 2n; therefore, of the 2n equations in (2) only 2n − n − 1 are independent. The necessary and sufficient conditions for the independence of the events A1, A2, . . . ., An are the following 2n − n − 1 equations10:

All of these equations are mutually independent.

In the case n = 2 we obtain from (4) only one condition (22 − 2 − 1 = 1) for the independence of two events A1 and A2:

The system of equations (2) reduces itself, in this case, to three equations, besides (5):

which obviously follow from (5).11

It need hardly be remarked that from the independence of the events A1, A2, . . ., An in pairs, i.e. from the relations

it does not at all follow that when n > 2 these events are independent12. (For that we need the existence of all equations (4).)

In introducing the concept of independence, no use was made of conditional probability. Our aim has been to explain as clearly as possible, in a purely mathematical manner, the meaning of this concept. Its applications, however, generally depend upon the properties of certain conditional probabilities.

If we assume that all probabilities are positive, then from the equations (3) it follows13 that

From the fact that formulas (6) hold, and from the Multiplication Theorem (formula (7), § 4), follow the formulas (2). We obtain, therefore,

THEOREM II: A necessary and sufficient condition for independence of experiments in the case of positive probabilities is that the conditional probability of the results Aq(i) of experiments under the hypothesis that several other tests have had definite results is equal to the absolute probability .

On the basis of formulas (4) we can prove in an analogous manner the following theorem:

THEOREM III. If all probabilities are positive, then a necessary and sufficient condition for mutual independence of the events A1, A2, . . ., An is the satisfaction of the equations

for any pairwise different i1, i2, . . ., ik, i.

In the case n = 2 the conditions (7) reduce to two equations:

It is easy to see that the first equation in (8) alone is a necessary and sufficient condition for the independence of A1 and A2 provided .

## 1.6 Conditional Probabilities as Random Variables, Markov Chains

Let be a decomposition of the fundamental set E:

and x a real function of the elementary event ξ, which for every set Aq is equal to a corresponding constant aq. x is then called a random variable, and the sum

is called the mathematical expectation of the variable x. The theory of random variables will be developed in Chaps. III and IV. We shall not limit ourselves there merely to those random variables which can assume only a finite number of different values.

A random variable which for every set Aq assumes the value, we shall call the conditional probability of the event B after the given experiment and shall designate it by . Two experiments and are independent if, and only if,

Given any decompositions (experiments), we we shall represent by

the decomposition of set E into the products

Experiments are mutually independent when and only when

k and q being arbitrary14.

DEFINITION: The sequence forms a Markov chain if for arbitrary n and q

Thus, Markov chains form a natural generalization of sequences of mutually independent experiments. If we set

then the basic formula of the theory of Markov chains will assume the form:

If we denote the matrix by p(m, n), (1) can be written as15:




1 For example, R. von Mises [1] and [2] and S. Bernstein [1].

2 The reader who wishes from the outset to give a concrete meaning to the following axioms, is referred to § 2.

3 Cf. HAUSDORFF, Mengenlehre, 1927, p. 78. A system of sets is called a field if the sum, product, and difference of two sets of the system also belong to the same system. Every non-empty field contains the null set 0. Using Hausdorff’s notation, we designate the product of A and B by AB; the sum by A + B in the case where AB = 0; and in the general case by A + B; the difference of A and B by A−B. The set E−A, which is the complement of A, will be denoted by Ā. We shall assume that the reader is familiar with the fundamental rules of operations of sets and their sums, products, and differences. All subsets of will be designated by Latin capitals.

4 The reader who is interested in the purely mathematical development of the theory only, need not read this section, since the work following it is based only upon the axioms in § 1 and makes no use of the present discussion. Here we limit ourselves to a simple explanation of how the axioms of the theory of probability arose and disregard the deep philosophical dissertations on the concept of probability in the experimental world. In establishing the premises necessary for the applicability of the theory of probability to the world of actual events, the author has used, in large measure, the work of R. v. Mises, [1] pp. 21-27.

5 Cf. § 4, Formula (3).

6 See Fréchet [1] and [2].

7 One may construct a field of probability with arbitrary probabilities subject only to the above-mentioned conditions, as follows: E is composed of r elements ξq1 q2 . . . qn. Let the corresponding elementary probabilities be pq1q2 . . . qn, and finally let be the set of all ξq1, q2 . . . qn for which qi = q.

8 Actually, in the case of independence, one may choose arbitrarily only r1 + r2 + . . . + rn probabilities so as to comply with the n conditions

Therefore, in the general case, we have r−1 degrees of freedom, but in the case of independence only r1 + r2 + . . . + rn−n.

9 To prove this it is sufficient to show that from the mutual independence of n decompositions follows the mutual independence of the first n−1. Let us assume that the equations (2) hold. Then

10 See S. N. Bernstein [1] pp. 47-57. However, the reader can easily prove this himself (using mathematical induction).

11, etc.

12 This can be shown by the following: simple example (S. N. Bernstein): Let set E be composed of four elements ξ1, ξ2, ξ3, ξ4; the corresponding elementary probabilities p1, p2, p3, p4 are each assumed to be ¼ and

It is easy to compute that

13 To prove it, one must keep in mind the definition of conditional probability (formula (5), § 4) and substitute for the probabilities of products the products of probabilities according to formula (3).

14 The necessity of these conditions follows from Theorem II, § 5; that they are also sufficient follows immediately from the Multiplication Theorem (Formula (7) of § 4).

15 For further development of the theory of Markov chains, see R. v. Mises [1], § 16, and B. HOSTINSKY, Méthodes générales du calcul des probabilités,「Mém. Sci. Math.」V. 52, Paris 1931.
