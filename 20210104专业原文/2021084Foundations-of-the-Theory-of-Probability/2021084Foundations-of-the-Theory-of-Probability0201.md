# 0201. INFINITE PROBABILITY FIELDS

§ 1. Axiom of Continuity

We denote by , as is customary, the product of the sets Am (whether finite or infinite in number) and their sum by . Only in the case of disjoint sets Am is the form used instead of . Consequently,

In all future investigations, we shall assume that besides Axioms I-V, still another holds true:

VI. For a decreasing sequence of events

of , for which

the following equation holds:

In the future we shall designate by probability field only a field of probability as outlined in the first chapter, which also satisfies Axiom VI. The fields of probability as defined in the first chapter without Axiom VI might be called generalized fields of probability.

If the system of sets is finite, Axiom VI follows from Axioms I-V. For actually, in that case there exist only a finite number of different sets in the sequence (1). Let Ak be the smallest among them, then all set Ak+p coincide with Ak and we obtain then

All examples of finite fields of probability, in the first chapter, satisfy, therefore, Axiom VI. The system of Axioms I-VI then proves to be consistent and incomplete.

For infinite fields, on the other hand, the Axiom of Continuity, VI, proved to be independent of Axioms I-V. Since the new axiom is essential for infinite fields of probability only, it is almost impossible to elucidate its empirical meaning, as has been done, for example, in the case of Axioms I-V in § 2 of the first chapter. For, in describing any observable random process we can obtain only finite fields of probability. Infinite fields of probability occur only as idealized models of real random processes. We limit ourselves, arbitrarily, to only those models which satisfy Axiom VI. This limitation has been found expedient in researches of the most diverse sort.

GENERALIZED ADDITION THEOREM: If A1, A2, . . . , An, . . . and A belong to , then from

follows the equation

Proof: Let

Then, obviously

and, therefore, according to Axiom VI

On the other hand, by the addition theorem

From (6) and (7) we immediately obtain (5).

We have shown, then, that the probability is a completely additive set function on . Conversely, Axioms V and VI hold true for every completely additive set function defined on any field .* We can, therefore, define the concept of a field of probability in the following way: Let E be an arbitrary set, a field of subsets of E, containing E, and a non-negative completely additive set function defined on ; the field together with the set function forms a field of probability.

A COVERING THEOREM: If A, A1, A2, . . . , An, . . . belong to and

then

Proof:

§ 2. Borel Fields of Probability

The field is called a Borel field, if all countable of the sets An from belong to . Borel fields are also called completely additive systems of sets. From the formula

we can deduce that a Borel field contains also all the sums composed of a countable number of sets An belonging to it. From the formula

the same can be said for the product of sets.

A field of probability is a Borel field of probability if the corresponding field is a Borel field. Only in the case of Borel fields of probability do we obtain full freedom of action, without danger of the occurrence of events having no probability. We shall now prove that we may limit ourselves to the investigation of Borel fields of probability. This will follow from the so-called extension theorem, to which we shall now turn.

Given a field of probability . As is known1, there exists a smallest Borel field containing . And we have the

EXTENSION THEOREM: It is always possible to extend a nonnegative completely additive set function , defined in , to all sets of without losing either of its properties (non-negativeness and complete additivity) and this can be done in only one way.

The extended field forms with the extended set function a field of probability . This field of probability we shall call the Borel extension of the field

The proof of this theorem, which belongs to the theory of additive set functions and which sometimes appears in other forms, can be given as follows:

Let A be any subset of E; we shall denote by the lower limit of the sums

for all coverings

of the set A by a finite or countable number of sets An of . It is easy to prove that is then an outer measure in the Carathéodory sense2. In accordance with the Covering Theorem (§ 1), coincides with for all sets of . It can be further shown that all sets of are measurable in the Carathéodory sense. Since all measurable sets form a Borel field, all sets of are consequently measurable. The set function is, therefore, completely additive on , and on we may set

We have thus shown the existence of the extension. The uniqueness of this extension follows immediately from the minimal property of the field .

Remark: Even if the sets (events) A of can be interpreted as actual and (perhaps only approximately) observable events, it does not, of course, follow from this that the sets of the extended field reasonably admit of such an interpretation.

Thus there is the possibility that while a field of probability may be regarded as the image (idealized, however) of actual random events, the extended field of probability will still remain merely a mathematical structure.

Thus sets of are generally merely ideal events to which nothing corresponds in the outside world. However, if reasoning which utilizes the probabilities of such ideal events leads us to a determination of the probability of an actual event of , then, from an empirical point of view also, this determination will automatically fail to be contradictory.

§ 3. Examples of Infinite Fields of Probability

I. In § 1 of the first chapter, we have constructed various finite probability fields.

Let now E = {ξ1, ξ2, . . . , ξn, . . .} be a countable set, and let coincide with the aggregate of the subsets of E.

All possible probability fields with such an aggregate are obtained in the following manner:

We take a sequence of non-negative numbers pn, such that

and for each set A put

where the summation ∑′ extends to all the indices n for which ξn belongs to A. These fields of probability are obviously Borel fields.

II. In this example, we shall assume that E represents the real number axis. At first, let be formed of all possible finite sums of half-open intervals (taking into consideration not only the proper intervals, with finite a and b, but also the improper intervals [− ∞; a), [a; + ∞) and [−∞; + ∞)). is then a field. By means of the extension theorem, however, each field of probability on can be extended to a similar field on . The system of sets is, therefore, in our case nothing but the system of all Borel point sets on a line. Let us turn now to the following case.

III. Again suppose E to be the real number axis, while is composed of all Borel point sets of this line. In order to construct a field of probability with the given field , it is sufficient to define an arbitrary non-negative completely additive set-function on which satisfies the condition . As is well known,3 such a function is uniquely determined by its values

for the special intervals [− ∞; x). The function F(x) is called the distribution function of ξ. Further on (Chap. III, § 2) we shall shown that F(x) is non-decreasing, continuous on the left, and has the following limiting values:

Conversely, if a given function F(x) satisfies these conditions, then it always determines a non-negative completely additive set-function for which .4

IV. Let us now consider the basic set E as an n-dimensional Euclidian space Rn, i.e., the set of all ordered n-tuples ξ = { x1, x2, . . . , xn} of real numbers. Let consist, in this case, of all Borel point-sets5 of the space Rn. On the basis of reasoning analogous to that used in Example II, we need not investigate narrower systems of sets, for example the systems of n-dimensional intervals.

The role of probability function will be played here, as always, by any non-negative and completely additive set-function defined on and satisfying the condition . Such a set-function is determined uniquely if we assign its values

for the special set La1 a2 . . . an, where La1 a2 . . . an represents the aggregate of all ξ for which xi < ai (i = 1, 2, . . . , n).

For our function F(a1, a2, . . . , an) we may choose any function which for each variable is non-decreasing and continuous on the left, and which satisfies the following conditions:

F(a1, a2, . . . , an) is called the distribution function of the variables x1, x2, . . . , xn.

The investigation of fields of probability of the above type is sufficient for all classical problems in the theory of probability6. In particular, a probability function in Rn can be defined thus:

We take any non-negative point function f(x1, x2, . . . , xn) defined in Rn, such that

and set

f(x1, x2, . . . , xn) is, in this case, the probability density at the point (x1, x2, . . . , xn) (cf. Chap. III, § 2).

Another type of probability function in Rn is obtained in the following manner: Let {ξi} be a sequence of points of Rn, and let {pi} be a sequence of non-negative real numbers, such that ∑Pi = 1; we then set, as we did in Example I,

where the summation ∑′ extends over all indices i for which ξ belongs to A. The two types of probability functions in Rn mentioned here do not exhaust all possibilities, but are usually considered sufficient for applications of the theory of probability. Nevertheless, we can imagine problems of interest for applications outside of this classical region in which elementary events are defined by means of an infinite number of coordinates. The corresponding fields of probability we shall study more closely after introducing several concepts needed for this purpose. (Cf. Chap. III, § 3).

* See, for example, O. NIKODYM, Sur une généralisation des intégrales de M. J. Radon, Fund. Math. v. 15, 1930, p. 136.

1 HAUSDORFF, Mengenlehre, 1927, p. 85.

2 CARATHÉODORY, Vorlesungen über reelle Funktionen, pp.237-258. (New York, Chelsea Publishing Company).

3 Cf., for example, LEBESGUE, Leçons sur l’intégration, 1928, p. 152-156.

4 See the previous note.

5 For a definition of Borel sets in R see HAUSDORFF, Mengenlehre, 1927, pp. 177-181.

6 Cf., for example, R. v. MISES [1], pp. 13-19. Here the existence of probabilities for「all practically possible:」sets of an n-dimensional space is required.