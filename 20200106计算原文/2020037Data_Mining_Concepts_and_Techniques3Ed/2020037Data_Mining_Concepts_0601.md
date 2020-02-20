Basic Concepts and Methods

Imagine that you are a sales manager at AllElectronics, and you are talking to a customer who recently bought a PC and a digital camera from the store. What should you recommend to her next? Information about which products are frequently purchased by your customers following their purchases of a PC and a digital camera in sequence would be very helpful in making your recommendation. Frequent patterns and association rules are the knowledge that you want to mine in such a scenario.

Frequent patterns are patterns (e.g., itemsets, subsequences, or substructures) that appear frequently in a data set. For example, a set of items, such as milk and bread, that appear frequently together in a transaction data set is a frequent itemset. A subsequence, such as buying first a PC, then a digital camera, and then a memory card, if it occurs frequently in a shopping history database, is a (frequent) sequential pattern. A substructure can refer to different structural forms, such as subgraphs, subtrees, or sublattices, which may be combined with itemsets or subsequences. If a substructure occurs frequently, it is called a (frequent) structured pattern. Finding frequent patterns plays an essential role in mining associations, correlations, and many other interesting relationships among data. Moreover, it helps in data classification, clustering, and other data mining tasks. Thus, frequent pattern mining has become an important data mining task and a focused theme in data mining research.

In this chapter, we introduce the basic concepts of frequent patterns, associations, and correlations (Section 6.1) and study how they can be mined efficiently (Section 6.2). We also discuss how to judge whether the patterns found are interesting (Section 6.3). In Chapter 7, we extend our discussion to advanced methods of frequent pattern mining, which mine more complex forms of frequent patterns and consider user preferences or constraints to speed up the mining process.

6.1. Basic Concepts

Frequent pattern mining searches for recurring relationships in a given data set. This section introduces the basic concepts of frequent pattern mining for the discovery of interesting associations and correlations between itemsets in transactional and relational databases. We begin in Section 6.1.1 by presenting an example of market basket analysis, the earliest form of frequent pattern mining for association rules. The basic concepts of mining frequent patterns and associations are given in Section 6.1.2.

6.1.1. Market Basket Analysis: A Motivating Example

Frequent itemset mining leads to the discovery of associations and correlations among items in large transactional or relational data sets. With massive amounts of data continuously being collected and stored, many industries are becoming interested in mining such patterns from their databases. The discovery of interesting correlation relationships among huge amounts of business transaction records can help in many business decision-making processes such as catalog design, cross-marketing, and customer shopping behavior analysis.

A typical example of frequent itemset mining is market basket analysis. This process analyzes customer buying habits by finding associations between the different items that customers place in their「shopping baskets」(Figure 6.1). The discovery of these associations can help retailers develop marketing strategies by gaining insight into which items are frequently purchased together by customers. For instance, if customers are buying milk, how likely are they to also buy bread (and what kind of bread) on the same trip to the supermarket? This information can lead to increased sales by helping retailers do selective marketing and plan their shelf space.

Figure 6.1

Market basket analysis.

Let's look at an example of how market basket analysis can be useful.

Market basket analysis Suppose, as manager of an AllElectronics branch, you would like to learn more about the buying habits of your customers. Specifically, you wonder,「Which groups or sets of items are customers likely to purchase on a given trip to the store?」To answer your question, market basket analysis may be performed on the retail data of customer transactions at your store. You can then use the results to plan marketing or advertising strategies, or in the design of a new catalog. For instance, market basket analysis may help you design different store layouts. In one strategy, items that are frequently purchased together can be placed in proximity to further encourage the combined sale of such items. If customers who purchase computers also tend to buy antivirus software at the same time, then placing the hardware display close to the software display may help increase the sales of both items.

In an alternative strategy, placing hardware and software at opposite ends of the store may entice customers who purchase such items to pick up other items along the way. For instance, after deciding on an expensive computer, a customer may observe security systems for sale while heading toward the software display to purchase antivirus software, and may decide to purchase a home security system as well. Market basket analysis can also help retailers plan which items to put on sale at reduced prices. If customers tend to purchase computers and printers together, then having a sale on printers may encourage the sale of printers as well as computers.

If we think of the universe as the set of items available at the store, then each item has a Boolean variable representing the presence or absence of that item. Each basket can then be represented by a Boolean vector of values assigned to these variables. The Boolean vectors can be analyzed for buying patterns that reflect items that are frequently associated or purchased together. These patterns can be represented in the form of association rules. For example, the information that customers who purchase computers also tend to buy antivirus software at the same time is represented in the following association rule:(6.1)

Rule support and confidence are two measures of rule interestingness. They respectively reflect the usefulness and certainty of discovered rules. A support of 2% for Rule (6.1) means that 2% of all the transactions under analysis show that computer and antivirus software are purchased together. A confidence of 60% means that 60% of the customers who purchased a computer also bought the software. Typically, association rules are considered interesting if they satisfy both a minimum support threshold and a minimum confidence threshold. These thresholds can be a set by users or domain experts. Additional analysis can be performed to discover interesting statistical correlations between associated items.

6.1.2. Frequent Itemsets, Closed Itemsets, and Association Rules

Let be an itemset. Let D, the task-relevant data, be a set of database transactions where each transaction T is a nonempty itemset such that . Each transaction is associated with an identifier, called a TID. Let A be a set of items. A transaction T is said to contain A if . An association rule is an implication of the form , where , , , , and . The rule holds in the transaction set D with support s, where s is the percentage of transactions in D that contain (i.e., the union of sets A and B say, or, both A and B). This is taken to be the probability, . 1 The rule has confidence c in the transaction set D, where c is the percentage of transactions in D containing A that also contain B. This is taken to be the conditional probability, . That is,(6.2)

(6.3)

Rules that satisfy both a minimum support threshold (min_sup) and a minimum confidence threshold (min_conf) are called strong. By convention, we write support and confidence values so as to occur between 0% and 100%, rather than 0 to 1.0.

1Notice that the notation indicates the probability that a transaction contains the union of sets A and B (i.e., it contains every item in A and B). This should not be confused with , which indicates the probability that a transaction contains either A or B.

A set of items is referred to as an itemset. 2 An itemset that contains k items is a k-itemset. The set {computer, antivirus_software } is a 2-itemset. The occurrence frequency of an itemset is the number of transactions that contain the itemset. This is also known, simply, as the frequency, support count, or count of the itemset. Note that the itemset support defined in Eq. (6.2) is sometimes referred to as relative support, whereas the occurrence frequency is called the absolute support. If the relative support of an itemset I satisfies a prespecified minimum support threshold (i.e., the absolute support of I satisfies the corresponding minimum support count threshold), then I is a frequent itemset. 3 The set of frequent k-itemsets is commonly denoted by Lk. 4

2In the data mining research literature,「itemset」is more commonly used than「item set.」

3In early work, itemsets satisfying minimum support were referred to as large. This term, however, is somewhat confusing as it has connotations of the number of items in an itemset rather than the frequency of occurrence of the set. Hence, we use the more recent term frequent.

4Although the term frequent is preferred over large, for historic reasons frequent k-itemsets are still denoted as Lk.

From Eq. (6.3), we have(6.4)

Equation (6.4) shows that the confidence of rule can be easily derived from the support counts of A and . That is, once the support counts of A, B, and are found, it is straightforward to derive the corresponding association rules and and check whether they are strong. Thus, the problem of mining association rules can be reduced to that of mining frequent itemsets.

In general, association rule mining can be viewed as a two-step process:1. Find all frequent itemsets: By definition, each of these itemsets will occur at least as frequently as a predetermined minimum support count, min_sup.

2. Generate strong association rules from the frequent itemsets: By definition, these rules must satisfy minimum support and minimum confidence.

Additional interestingness measures can be applied for the discovery of correlation relationships between associated items, as will be discussed in Section 6.3. Because the second step is much less costly than the first, the overall performance of mining association rules is determined by the first step.

A major challenge in mining frequent itemsets from a large data set is the fact that such mining often generates a huge number of itemsets satisfying the minimum support (min_sup) threshold, especially when min_sup is set low. This is because if an itemset is frequent, each of its subsets is frequent as well. A long itemset will contain a combinatorial number of shorter, frequent sub-itemsets. For example, a frequent itemset of length 100, such as {}, contains frequent 1-itemsets: , , …, ; frequent 2-itemsets: , ,…,; and so on. The total number of frequent itemsets that it contains is thus(6.5)

This is too huge a number of itemsets for any computer to compute or store. To overcome this difficulty, we introduce the concepts of closed frequent itemset and maximal frequent itemset.

An itemset X is closed in a data set D if there exists no proper super-itemset Y5 such that Y has the same support count as X in D. An itemset X is a closed frequent itemset in set D if X is both closed and frequent in D. An itemset X is a maximal frequent itemset (or max-itemset) in a data set D if X is frequent, and there exists no super-itemset Y such that and Y is frequent in D.

5Y is a proper super-itemset of X if X is a proper sub-itemset of Y, that is, if . In other words, every item of X is contained in Y but there is at least one item of Y that is not in X.

Let be the set of closed frequent itemsets for a data set D satisfying a minimum support threshold, . Let be the set of maximal frequent itemsets for D satisfying . Suppose that we have the support count of each itemset in and . Notice that and its count information can be used to derive the whole set of frequent itemsets. Thus, we say that contains complete information regarding its corresponding frequent itemsets. On the other hand, registers only the support of the maximal itemsets. It usually does not contain the complete support information regarding its corresponding frequent itemsets. We illustrate these concepts with Example 6.2.

Closed and maximal frequent itemsets Suppose that a transaction database has only two transactions: {; }. Let the minimum support count threshold be . We find two closed frequent itemsets and their support counts, that is, {{; {}. There is only one maximal frequent itemset: {{}. Notice that we cannot include {} as a maximal frequent itemset because it has a frequent superset, {}. Compare this to the preceding where we determined that there are frequent itemsets, which are too many to be enumerated!

The set of closed frequent itemsets contains complete information regarding the frequent itemsets. For example, from , we can derive, say, (1) {} since {} is a sub-itemset of the itemset {}; and (2) {} since {} is not a sub-itemset of the previous itemset but of the itemset {}. However, from the maximal frequent itemset, we can only assert that both itemsets ({} and {}) are frequent, but we cannot assert their actual support counts.

6.2. Frequent Itemset Mining Methods

In this section, you will learn methods for mining the simplest form of frequent patterns such as those discussed for market basket analysis in Section 6.1.1. We begin by presenting Apriori, the basic algorithm for finding frequent itemsets (Section 6.2.1). In Section 6.2.2, we look at how to generate strong association rules from frequent itemsets. Section 6.2.3 describes several variations to the Apriori algorithm for improved efficiency and scalability. Section 6.2.4 presents pattern-growth methods for mining frequent itemsets that confine the subsequent search space to only the data sets containing the current frequent itemsets. Section 6.2.5 presents methods for mining frequent itemsets that take advantage of the vertical data format.

6.2.1. Apriori Algorithm: Finding Frequent Itemsets by Confined Candidate Generation

Apriori is a seminal algorithm proposed by R. Agrawal and R. Srikant in 1994 for mining frequent itemsets for Boolean association rules [AS94b]. The name of the algorithm is based on the fact that the algorithm uses prior knowledge of frequent itemset properties, as we shall see later. Apriori employs an iterative approach known as a level-wise search, where k-itemsets are used to explore (k + 1)-itemsets. First, the set of frequent 1-itemsets is found by scanning the database to accumulate the count for each item, and collecting those items that satisfy minimum support. The resulting set is denoted by L1. Next, L1 is used to find L2, the set of frequent 2-itemsets, which is used to find L3, and so on, until no more frequent k-itemsets can be found. The finding of each Lk requires one full scan of the database.

To improve the efficiency of the level-wise generation of frequent itemsets, an important property called the Apriori property is used to reduce the search space.

Apriori property: All nonempty subsets of a frequent itemset must also be frequent.

The Apriori property is based on the following observation. By definition, if an itemset I does not satisfy the minimum support threshold, min_sup, then I is not frequent, that is, . If an item A is added to the itemset I, then the resulting itemset (i.e., ) cannot occur more frequently than I. Therefore, is not frequent either, that is, .

This property belongs to a special category of properties called antimonotonicity in the sense that if a set cannot pass a test, all of its supersets will fail the same test as well. It is called antimonotonicity because the property is monotonic in the context of failing a test. 6

6The Apriori property has many applications. For example, it can also be used to prune search during data cube computation (Chapter 5).

「How is the Apriori property used in the algorithm?」To understand this, let us look at how Lk − 1 is used to find Lk for . A two-step process is followed, consisting of join and prune actions.

1. The join step: To find Lk, a set of candidate k-itemsets is generated by joining Lk − 1 with itself. This set of candidates is denoted Ck. Let l1 and l2 be itemsets in Lk − 1. The notation refers to the j th item in li (e.g., refers to the second to the last item in l1). For efficient implementation, Apriori assumes that items within a transaction or itemset are sorted in lexicographic order. For the (k − 1)-itemset, li, this means that the items are sorted such that . The join, , is performed, where members of Lk − 1 are joinable if their first items are in common. That is, members l1 and l2 of Lk − 1 are joined if (. The condition simply ensures that no duplicates are generated. The resulting itemset formed by joining l1 and l2 is .

2. The prune step: Ck is a superset of Lk, that is, its members may or may not be frequent, but all of the frequent k-itemsets are included in Ck. A database scan to determine the count of each candidate in Ck would result in the determination of Lk (i.e., all candidates having a count no less than the minimum support count are frequent by definition, and therefore belong to Lk). Ck, however, can be huge, and so this could involve heavy computation. To reduce the size of Ck, the Apriori property is used as follows. Any (k − 1)-itemset that is not frequent cannot be a subset of a frequent k-itemset. Hence, if any (k − 1)-subset of a candidate k-itemset is not in Lk − 1, then the candidate cannot be frequent either and so can be removed from Ck. This subset testing can be done quickly by maintaining a hash tree of all frequent itemsets.

Apriori Let's look at a concrete example, based on the AllElectronics transaction database, D, of Table 6.1. There are nine transactions in this database, that is, . We use Figure 6.2 to illustrate the Apriori algorithm for finding frequent itemsets in D.

Figure 6.2

Generation of the candidate itemsets and frequent itemsets, where the minimum support count is 2.

Table 6.1

Transactional Data for an AllElectronics Branch

TIDList of item_IDs

T100 I1, I2, I5

T200 I2, I4

T300 I2, I3

T400 I1, I2, I4

T500 I1, I3

T600 I2, I3

T700 I1, I3

T800 I1, I2, I3, I5

T900 I1, I2, I3

1. In the first iteration of the algorithm, each item is a member of the set of candidate 1-itemsets, C1. The algorithm simply scans all of the transactions to count the number of occurrences of each item.

2. Suppose that the minimum support count required is 2, that is, . (Here, we are referring to absolute support because we are using a support count. The corresponding relative support is %.) The set of frequent 1-itemsets, L1, can then be determined. It consists of the candidate 1-itemsets satisfying minimum support. In our example, all of the candidates in C1 satisfy minimum support.

3. To discover the set of frequent 2-itemsets, L2, the algorithm uses the join to generate a candidate set of 2-itemsets, C2. 7C2 consists of 2-itemsets. Note that no candidates are removed from C2 during the prune step because each subset of the candidates is also frequent.

7 is equivalent to , since the definition of requires the two joining itemsets to share k − 1 = 0 items.

4. Next, the transactions in D are scanned and the support count of each candidate itemset in C2 is accumulated, as shown in the middle table of the second row in Figure 6.2.

5. The set of frequent 2-itemsets, L2, is then determined, consisting of those candidate 2-itemsets in C2 having minimum support.

6. The generation of the set of the candidate 3-itemsets, C3, is detailed in Figure 6.3. From the join step, we first get {{I1, I2, I3}, {I1, I2, I5}, {I1, I3, I5}, {I2, I3, I4}, {I2, I3, I5}, {I2, I4, I5}}. Based on the Apriori property that all subsets of a frequent itemset must also be frequent, we can determine that the four latter candidates cannot possibly be frequent. We therefore remove them from C3, thereby saving the effort of unnecessarily obtaining their counts during the subsequent scan of D to determine L3. Note that when given a candidate k-itemset, we only need to check if its (k − 1)-subsets are frequent since the Apriori algorithm uses a level-wise search strategy. The resulting pruned version of C3 is shown in the first table of the bottom row of Figure 6.2.

Figure 6.3

Generation and pruning of candidate 3-itemsets, C3, from L2 using the Apriori property.

7. The transactions in D are scanned to determine L3, consisting of those candidate 3-itemsets in C3 having minimum support (Figure 6.2).

8. The algorithm uses to generate a candidate set of 4-itemsets, C4. Although the join results in {{I1, I2, I3, I5}}, itemset {I1, I2, I3, I5} is pruned because its subset {I2, I3, I5} is not frequent. Thus, , and the algorithm terminates, having found all of the frequent itemsets.

Figure 6.4 shows pseudocode for the Apriori algorithm and its related procedures. Step 1 of Apriori finds the frequent 1-itemsets, L1. In steps 2 through 10, Lk − 1 is used to generate candidates Ck to find Lk for . The apriori_gen procedure generates the candidates and then uses the Apriori property to eliminate those having a subset that is not frequent (step 3). This procedure is described later. Once all of the candidates have been generated, the database is scanned (step 4). For each transaction, a subset function is used to find all subsets of the transaction that are candidates (step 5), and the count for each of these candidates is accumulated (steps 6 and 7). Finally, all the candidates satisfying the minimum support (step 9) form the set of frequent itemsets, L (step 11). A procedure can then be called to generate association rules from the frequent itemsets. Such a procedure is described in Section 6.2.2.

Figure 6.4

Apriori algorithm for discovering frequent itemsets for mining Boolean association rules.

The apriori_gen procedure performs two kinds of actions, namely, join and prune, as described before. In the join component, Lk − 1 is joined with Lk − 1 to generate potential candidates (steps 1–4). The prune component (steps 5–7) employs the Apriori property to remove candidates that have a subset that is not frequent. The test for infrequent subsets is shown in procedure has_infrequent_subset.

6.2.2. Generating Association Rules from Frequent Itemsets

Once the frequent itemsets from transactions in a database D have been found, it is straightforward to generate strong association rules from them (where strong association rules satisfy both minimum support and minimum confidence). This can be done using Eq. (6.4) for confidence, which we show again here for completeness:

The conditional probability is expressed in terms of itemset support count, where is the number of transactions containing the itemsets , and is the number of transactions containing the itemset A. Based on this equation, association rules can be generated as follows:■ For each frequent itemset l, generate all nonempty subsets of l.

■ For every nonempty subset s of l, output the rule「」if min_conf, where min_conf is the minimum confidence threshold.

Because the rules are generated from frequent itemsets, each one automatically satisfies the minimum support. Frequent itemsets can be stored ahead of time in hash tables along with their counts so that they can be accessed quickly.

Generating association rules Let's try an example based on the transactional data for AllElectronics shown before in Table 6.1. The data contain frequent itemset {I1, I2, I5}. What are the association rules that can be generated from X? The nonempty subsets of X are {I1, I2}, {I1, I5}, {I2, I5}, {I1}, {I2}, and {I5}. The resulting association rules are as shown below, each listed with its confidence: {I1, I2}⇒I5,confidence = 2/4 = 50%

{I1, I5}⇒I2,confidence = 2/2 = 100%

{I2, I5}⇒I1,confidence = 2/2 = 100%

I1⇒{I2, I5},confidence = 2/6 = 33%

I2⇒{I1, I5},confidence = 2/7 = 29%

I5⇒{I1, I2},confidence = 2/2 = 100%

If the minimum confidence threshold is, say, 70%, then only the second, third, and last rules are output, because these are the only ones generated that are strong. Note that, unlike conventional classification rules, association rules can contain more than one conjunct in the right side of the rule.

6.2.3. Improving the Efficiency of Apriori

「How can we further improve the efficiency of Apriori-based mining?」Many variations of the Apriori algorithm have been proposed that focus on improving the efficiency of the original algorithm. Several of these variations are summarized as follows: Hash-based technique (hashing itemsets into corresponding buckets): A hash-based technique can be used to reduce the size of the candidate k-itemsets, Ck, for . For example, when scanning each transaction in the database to generate the frequent 1-itemsets, L1, we can generate all the 2-itemsets for each transaction, hash (i.e., map) them into the different buckets of a hash table structure, and increase the corresponding bucket counts (Figure 6.5). A 2-itemset with a corresponding bucket count in the hash table that is below the support threshold cannot be frequent and thus should be removed from the candidate set. Such a hash-based technique may substantially reduce the number of candidate k-itemsets examined (especially when ).

Transaction reduction (reducing the number of transactions scanned in future iterations): A transaction that does not contain any frequent k-itemsets cannot contain any frequent ()-itemsets. Therefore, such a transaction can be marked or removed from further consideration because subsequent database scans for j-itemsets, where , will not need to consider such a transaction.

Partitioning (partitioning the data to find candidate itemsets): A partitioning technique can be used that requires just two database scans to mine the frequent itemsets (Figure 6.6). It consists of two phases. In phase I, the algorithm divides the transactions of D into n nonoverlapping partitions. If the minimum relative support threshold for transactions in D is , then the minimum support count for a partition is × the number of transactions in that partition. For each partition, all the local frequent itemsets (i.e., the itemsets frequent within the partition) are found.

Figure 6.5

Hash table, H2, for candidate 2-itemsets. This hash table was generated by scanning Table 6.1's transactions while determining L1. If the minimum support count is, say, 3, then the itemsets in buckets 0, 1, 3, and 4 cannot be frequent and so they should not be included in C2.

Figure 6.6

Mining by partitioning the data.

A local frequent itemset may or may not be frequent with respect to the entire database, D. However, any itemset that is potentially frequent with respect to D must occur as a frequent itemset in at least one of the partitions. 8 Therefore, all local frequent itemsets are candidate itemsets with respect to D. The collection of frequent itemsets from all partitions forms the global candidate itemsets with respect to D. In phase II, a second scan of D is conducted in which the actual support of each candidate is assessed to determine the global frequent itemsets. Partition size and the number of partitions are set so that each partition can fit into main memory and therefore be read only once in each phase.

8The proof of this property is left as an exercise (see Exercise 6.3d).

Sampling (mining on a subset of the given data): The basic idea of the sampling approach is to pick a random sample S of the given data D, and then search for frequent itemsets in S instead of D. In this way, we trade off some degree of accuracy against efficiency. The S sample size is such that the search for frequent itemsets in S can be done in main memory, and so only one scan of the transactions in S is required overall. Because we are searching for frequent itemsets in S rather than in D, it is possible that we will miss some of the global frequent itemsets.

To reduce this possibility, we use a lower support threshold than minimum support to find the frequent itemsets local to S (denoted Ls). The rest of the database is then used to compute the actual frequencies of each itemset in Ls. A mechanism is used to determine whether all the global frequent itemsets are included in Ls. If Ls actually contains all the frequent itemsets in D, then only one scan of D is required. Otherwise, a second pass can be done to find the frequent itemsets that were missed in the first pass. The sampling approach is especially beneficial when efficiency is of utmost importance such as in computationally intensive applications that must be run frequently.

Dynamic itemset counting (adding candidate itemsets at different points during a scan): A dynamic itemset counting technique was proposed in which the database is partitioned into blocks marked by start points. In this variation, new candidate itemsets can be added at any start point, unlike in Apriori, which determines new candidate itemsets only immediately before each complete database scan. The technique uses the count-so-far as the lower bound of the actual count. If the count-so-far passes the minimum support, the itemset is added into the frequent itemset collection and can be used to generate longer candidates. This leads to fewer database scans than with Apriori for finding all the frequent itemsets.

Other variations are discussed in the next chapter.

6.2.4. A Pattern-Growth Approach for Mining Frequent Itemsets

As we have seen, in many cases the Apriori candidate generate-and-test method significantly reduces the size of candidate sets, leading to good performance gain. However, it can suffer from two nontrivial costs:■ It may still need to generate a huge number of candidate sets. For example, if there are 104 frequent 1-itemsets, the Apriori algorithm will need to generate more than 107 candidate 2-itemsets.

■ It may need to repeatedly scan the whole database and check a large set of candidates by pattern matching. It is costly to go over each transaction in the database to determine the support of the candidate itemsets.

「Can we design a method that mines the complete set of frequent itemsets without such a costly candidate generation process?」An interesting method in this attempt is called frequent pattern growth, or simply FP-growth, which adopts a divide-and-conquer strategy as follows. First, it compresses the database representing frequent items into a frequent pattern tree, or FP-tree, which retains the itemset association information. It then divides the compressed database into a set of conditional databases (a special kind of projected database), each associated with one frequent item or「pattern fragment,」and mines each database separately. For each「pattern fragment,」only its associated data sets need to be examined. Therefore, this approach may substantially reduce the size of the data sets to be searched, along with the「growth」of patterns being examined. You will see how it works in Example 6.5.

FP-growth (finding frequent itemsets without candidate generation) We reexamine the mining of transaction database, D, of Table 6.1 in Example 6.3 using the frequent pattern growth approach.

The first scan of the database is the same as Apriori, which derives the set of frequent items (1-itemsets) and their support counts (frequencies). Let the minimum support count be 2. The set of frequent items is sorted in the order of descending support count. This resulting set or list is denoted by L. Thus, we have L = {{I2: 7}, {I1: 6}, {I3: 6}, {I4: 2}, {I5: 2}}.

An FP-tree is then constructed as follows. First, create the root of the tree, labeled with「null.」Scan database D a second time. The items in each transaction are processed in L order (i.e., sorted according to descending support count), and a branch is created for each transaction. For example, the scan of the first transaction,「T100: I1, I2, I5,」which contains three items (I2, I1, I5 in L order), leads to the construction of the first branch of the tree with three nodes, 〈I2: 1〉, 〈I1: 1〉, and 〈I5: 1〉, where I2 is linked as a child to the root, I1 is linked to I2, and I5 is linked to I1. The second transaction, T200, contains the items I2 and I4 in L order, which would result in a branch where I2 is linked to the root and I4 is linked to I2. However, this branch would share a common prefix, I2, with the existing path for T100. Therefore, we instead increment the count of the I2 node by 1, and create a new node, 〈I4: 1〉, which is linked as a child to 〈I2: 2〉. In general, when considering the branch to be added for a transaction, the count of each node along a common prefix is incremented by 1, and nodes for the items following the prefix are created and linked accordingly.

To facilitate tree traversal, an item header table is built so that each item points to its occurrences in the tree via a chain of node-links. The tree obtained after scanning all the transactions is shown in Figure 6.7 with the associated node-links. In this way, the problem of mining frequent patterns in databases is transformed into that of mining the FP-tree.

Figure 6.7

An FP-tree registers compressed, frequent pattern information.

The FP-tree is mined as follows. Start from each frequent length-1 pattern (as an initial suffix pattern), construct its conditional pattern base (a「sub-database,」which consists of the set of prefix paths in the FP-tree co-occurring with the suffix pattern), then construct its (conditional) FP-tree, and perform mining recursively on the tree. The pattern growth is achieved by the concatenation of the suffix pattern with the frequent patterns generated from a conditional FP-tree.

Mining of the FP-tree is summarized in Table 6.2 and detailed as follows. We first consider I5, which is the last item in L, rather than the first. The reason for starting at the end of the list will become apparent as we explain the FP-tree mining process. I5 occurs in two FP-tree branches of Figure 6.7. (The occurrences of I5 can easily be found by following its chain of node-links.) The paths formed by these branches are 〈I2, I1, I5: 1〉 and 〈I2, I1, I3, I5: 1〉. Therefore, considering I5 as a suffix, its corresponding two prefix paths are 〈I2, I1: 1〉 and 〈I2, I1, I3: 1〉, which form its conditional pattern base. Using this conditional pattern base as a transaction database, we build an I5-conditional FP-tree, which contains only a single path, 〈I2: 2, I1: 2〉; I3 is not included because its support count of 1 is less than the minimum support count. The single path generates all the combinations of frequent patterns: {I2, I5: 2}, {I1, I5: 2}, {I2, I1, I5: 2}.

Table 6.2

Mining the FP-Tree by Creating Conditional (Sub-)Pattern Bases

ItemConditional Pattern BaseConditional FP-treeFrequent Patterns Generated

I5 {{I2, I1: 1}, {I2, I1, I3: 1}} 〈I2: 2, I1: 2〉 {I2, I5: 2}, {I1, I5: 2}, {I2, I1, I5: 2}

I4 {{I2, I1: 1}, {I2: 1}} 〈I2: 2〉 {I2, I4: 2}

I3 {{I2, I1: 2}, {I2: 2}, {I1: 2}} 〈I2: 4, I1: 2〉, 〈I1: 2〉 {I2, I3: 4}, {I1, I3: 4}, {I2, I1, I3: 2}

I1 {{I2: 4}} 〈I2: 4〉 {I2, I1: 4}

For I4, its two prefix paths form the conditional pattern base, {{I2 I1: 1}, {I2: 1}}, which generates a single-node conditional FP-tree, 〈I2: 2〉, and derives one frequent pattern, {I2, I4: 2}.

Similar to the preceding analysis, I3's conditional pattern base is {{I2, I1: 2}, {I2: 2}, {I1: 2}}. Its conditional FP-tree has two branches, 〈I2: 4, I1: 2〉 and 〈I1: 2〉, as shown in Figure 6.8, which generates the set of patterns {{I2, I3: 4}, {I1, I3: 4}, {I2, I1, I3: 2}}. Finally, I1's conditional pattern base is {{I2: 4}}, with an FP-tree that contains only one node, 〈I2: 4〉, which generates one frequent pattern, {I2, I1: 4}. This mining process is summarized in Figure 6.9.

Figure 6.8

The conditional FP-tree associated with the conditional node I3.

Figure 6.9

FP-growth algorithm for discovering frequent itemsets without candidate generation.

The FP-growth method transforms the problem of finding long frequent patterns into searching for shorter ones in much smaller conditional databases recursively and then concatenating the suffix. It uses the least frequent items as a suffix, offering good selectivity. The method substantially reduces the search costs.

When the database is large, it is sometimes unrealistic to construct a main memory-based FP-tree. An interesting alternative is to first partition the database into a set of projected databases, and then construct an FP-tree and mine it in each projected database. This process can be recursively applied to any projected database if its FP-tree still cannot fit in main memory.

A study of the FP-growth method performance shows that it is efficient and scalable for mining both long and short frequent patterns, and is about an order of magnitude faster than the Apriori algorithm.

6.2.5. Mining Frequent Itemsets Using the Vertical Data Format

Both the Apriori and FP-growth methods mine frequent patterns from a set of transactions in TID-itemset format (i.e., ), where TID is a transaction ID and itemset is the set of items bought in transaction TID. This is known as the horizontal data format. Alternatively, data can be presented in item-TID_set format (i.e., , where item is an item name, and TID_set is the set of transaction identifiers containing the item. This is known as the vertical data format.

In this subsection, we look at how frequent itemsets can also be mined efficiently using vertical data format, which is the essence of the Eclat (Equivalence Class Transformation) algorithm.

Mining frequent itemsets using the vertical data format Consider the horizontal data format of the transaction database, D, of Table 6.1 in Example 6.3. This can be transformed into the vertical data format shown in Table 6.3 by scanning the data set once.

Table 6.3

The Vertical Data Format of the Transaction Data Set D of Table 6.1

itemsetTID_set

I1 {T100, T400, T500, T700, T800, T900}

I2 {T100, T200, T300, T400, T600, T800, T900}

I3 {T300, T500, T600, T700, T800, T900}

I4 {T200, T400}

I5 {T100, T800}

Mining can be performed on this data set by intersecting the TID_sets of every pair of frequent single items. The minimum support count is 2. Because every single item is frequent in Table 6.3, there are 10 intersections performed in total, which lead to eight nonempty 2-itemsets, as shown in Table 6.4. Notice that because the itemsets {I1, I4} and {I3, I5} each contain only one transaction, they do not belong to the set of frequent 2-itemsets.

Table 6.4

2-Itemsets in Vertical Data Format

itemsetTID_set

{I1, I2} {T100, T400, T800, T900}

{I1, I3} {T500, T700, T800, T900}

{I1, I4} {T400}

{I1, I5} {T100, T800}

{I2, I3} {T300, T600, T800, T900}

{I2, I4} {T200, T400}

{I2, I5} {T100, T800}

{I3, I5} {T800}

Based on the Apriori property, a given 3-itemset is a candidate 3-itemset only if every one of its 2-itemset subsets is frequent. The candidate generation process here will generate only two 3-itemsets: {I1, I2, I3} and {I1, I2, I5}. By intersecting the TID_sets of any two corresponding 2-itemsets of these candidate 3-itemsets, it derives Table 6.5, where there are only two frequent 3-itemsets: {I1, I2, I3: 2} and {I1, I2, I5: 2}.

Table 6.5

3-Itemsets in Vertical Data Format

itemsetTID_set

{I1, I2, I3} {T800, T900}

{I1, I2, I5} {T100, T800}

Example 6.6 illustrates the process of mining frequent itemsets by exploring the vertical data format. First, we transform the horizontally formatted data into the vertical format by scanning the data set once. The support count of an itemset is simply the length of the TID_set of the itemset. Starting with , the frequent k-itemsets can be used to construct the candidate (k + 1)-itemsets based on the Apriori property. The computation is done by intersection of the TID_sets of the frequent k-itemsets to compute the TID_sets of the corresponding (k + 1)-itemsets. This process repeats, with k incremented by 1 each time, until no frequent itemsets or candidate itemsets can be found.

Besides taking advantage of the Apriori property in the generation of candidate (k + 1)-itemset from frequent k-itemsets, another merit of this method is that there is no need to scan the database to find the support of (k + 1)-itemsets (for ). This is because the TID_set of each k-itemset carries the complete information required for counting such support. However, the TID_sets can be quite long, taking substantial memory space as well as computation time for intersecting the long sets.

To further reduce the cost of registering long TID_sets, as well as the subsequent costs of intersections, we can use a technique called diffset, which keeps track of only the differences of the TID_sets of a (k + 1)-itemset and a corresponding k-itemset. For instance, in Example 6.6 we have {I1} = {T100, T400, T500, T700, T800, T900} and {I1, I2} = {T100, T400, T800, T900}. The diffset between the two is diffset ({I1, I2}, {I1}) = {T500, T700}. Thus, rather than recording the four TIDs that make up the intersection of {I1} and {I2}, we can instead use diffset to record just two TIDs, indicating the difference between {I1} and {I1, I2}. Experiments show that in certain situations, such as when the data set contains many dense and long patterns, this technique can substantially reduce the total cost of vertical format mining of frequent itemsets.

6.2.6. Mining Closed and Max Patterns

In Section 6.1.2 we saw how frequent itemset mining may generate a huge number of frequent itemsets, especially when the min_sup threshold is set low or when there exist long patterns in the data set. Example 6.2 showed that closed frequent itemsets9 can substantially reduce the number of patterns generated in frequent itemset mining while preserving the complete information regarding the set of frequent itemsets. That is, from the set of closed frequent itemsets, we can easily derive the set of frequent itemsets and their support. Thus, in practice, it is more desirable to mine the set of closed frequent itemsets rather than the set of all frequent itemsets in most cases.

9Remember that X is a closed frequent itemset in a data set S if there exists no proper super-itemset Y such that Y has the same support count as X in S, and X satisfies minimum support.

「How can we mine closed frequent itemsets?」A na ve approach would be to first mine the complete set of frequent itemsets and then remove every frequent itemset that is a proper subset of, and carries the same support as, an existing frequent itemset. However, this is quite costly. As shown in Example 6.2, this method would have to first derive frequent itemsets to obtain a length-100 frequent itemset, all before it could begin to eliminate redundant itemsets. This is prohibitively expensive. In fact, there exist only a very small number of closed frequent itemsets in Example 6.2's data set.

A recommended methodology is to search for closed frequent itemsets directly during the mining process. This requires us to prune the search space as soon as we can identify the case of closed itemsets during mining. Pruning strategies include the following: Item merging: If every transaction containing a frequent itemset X also contains an itemset Y but not any proper superset of Y, then forms a frequent closed itemset and there is no need to search for any itemset containing X but no Y.

For example, in Table 6.2 of Example 6.5, the projected conditional database for prefix itemset {I5:2} is {{I2, I1}, {I2, I1, I3}}, from which we can see that each of its transactions contains itemset {I2, I1} but no proper superset of {I2, I1}. Itemset {I2, I1} can be merged with {I5} to form the closed itemset, {I5, I2, I1: 2}, and we do not need to mine for closed itemsets that contain I5 but not {I2, I1}.

Sub-itemset pruning: If a frequent itemset X is a proper subset of an already found frequent closed itemset Y and support_count(X) = support_count(Y), then X and all of X's descendants in the set enumeration tree cannot be frequent closed itemsets and thus can be pruned.

Similar to Example 6.2, suppose a transaction database has only two transactions: {, }, and the minimum support count is min_sup = 2. The projection on the first item, , derives the frequent itemset, {}, based on the itemset merging optimization. Because support ({}) = support ({}) = 2, and {} is a proper subset of {}, there is no need to examine and its projected database. Similar pruning can be done for as well. Thus, the mining of closed frequent itemsets in this data set terminates after mining 's projected database.

Item skipping: In the depth-first mining of closed itemsets, at each level, there will be a prefix itemset X associated with a header table and a projected database. If a local frequent item p has the same support in several header tables at different levels, we can safely prune p from the header tables at higher levels.

Consider, for example, the previous transaction database having only two transactions: {, }, where . Because in 's projected database has the same support as in the global header table, can be pruned from the global header table. Similar pruning can be done for . There is no need to mine anything more after mining 's projected database.

Besides pruning the search space in the closed itemset mining process, another important optimization is to perform efficient checking of each newly derived frequent itemset to see whether it is closed. This is because the mining process cannot ensure that every generated frequent itemset is closed.

When a new frequent itemset is derived, it is necessary to perform two kinds of closure checking: (1) superset checking, which checks if this new frequent itemset is a superset of some already found closed itemsets with the same support, and (2) subset checking, which checks whether the newly found itemset is a subset of an already found closed itemset with the same support.

If we adopt the item merging pruning method under a divide-and-conquer framework, then the superset checking is actually built-in and there is no need to explicitly perform superset checking. This is because if a frequent itemset is found later than itemset X, and carries the same support as X, it must be in X's projected database and must have been generated during itemset merging.

To assist in subset checking, a compressed pattern-tree can be constructed to maintain the set of closed itemsets mined so far. The pattern-tree is similar in structure to the FP-tree except that all the closed itemsets found are stored explicitly in the corresponding tree branches. For efficient subset checking, we can use the following property: If the current itemset can be subsumed by another already found closed itemset , then (1) and have the same support, (2) the length of is smaller than that of , and (3) all of the items in are contained in .

Based on this property, a two-level hash index structure can be built for fast accessing of the pattern-tree: The first level uses the identifier of the last item in as a hash key (since this identifier must be within the branch of ), and the second level uses the support of as a hash key (since and have the same support). This will substantially speed up the subset checking process.

This discussion illustrates methods for efficient mining of closed frequent itemsets.「Can we extend these methods for efficient mining of maximal frequent itemsets?」Because maximal frequent itemsets share many similarities with closed frequent itemsets, many of the optimization techniques developed here can be extended to mining maximal frequent itemsets. However, we leave this method as an exercise for interested readers.

6.3. Which Patterns Are Interesting?—Pattern Evaluation Methods

Most association rule mining algorithms employ a support–confidence framework. Although minimum support and confidence thresholds help weed out or exclude the exploration of a good number of uninteresting rules, many of the rules generated are still not interesting to the users. Unfortunately, this is especially true when mining at low support thresholds or mining for long patterns. This has been a major bottleneck for successful application of association rule mining.

In this section, we first look at how even strong association rules can be uninteresting and misleading (Section 6.3.1). We then discuss how the support–confidence framework can be supplemented with additional interestingness measures based on correlation analysis (Section 6.3.2). Section 6.3.3 presents additional pattern evaluation measures. It then provides an overall comparison of all the measures discussed here. By the end, you will learn which pattern evaluation measures are most effective for the discovery of only interesting rules.

6.3.1. Strong Rules Are Not Necessarily Interesting

Whether or not a rule is interesting can be assessed either subjectively or objectively. Ultimately, only the user can judge if a given rule is interesting, and this judgment, being subjective, may differ from one user to another. However, objective interestingness measures, based on the statistics「behind」the data, can be used as one step toward the goal of weeding out uninteresting rules that would otherwise be presented to the user.

「How can we tell which strong association rules are really interesting?」Let's examine the following example.

A misleading「strong」association rule Suppose we are interested in analyzing transactions at AllElectronics with respect to the purchase of computer games and videos. Let game refer to the transactions containing computer games, and video refer to those containing videos. Of the 10,000 transactions analyzed, the data show that 6000 of the customer transactions included computer games, while 7500 included videos, and 4000 included both computer games and videos. Suppose that a data mining program for discovering association rules is run on the data, using a minimum support of, say, 30% and a minimum confidence of 60%. The following association rule is discovered:(6.6)

Rule (6.6) is a strong association rule and would therefore be reported, since its support value of and confidence value of satisfy the minimum support and minimum confidence thresholds, respectively. However, Rule (6.6) is misleading because the probability of purchasing videos is 75%, which is even larger than 66%. In fact, computer games and videos are negatively associated because the purchase of one of these items actually decreases the likelihood of purchasing the other. Without fully understanding this phenomenon, we could easily make unwise business decisions based on Rule (6.6).

Example 6.7 also illustrates that the confidence of a rule can be deceiving. It does not measure the real strength (or lack of strength) of the correlation and implication between A and B. Hence, alternatives to the support–confidence framework can be useful in mining interesting data relationships.

6.3.2. From Association Analysis to Correlation Analysis

As we have seen so far, the support and confidence measures are insufficient at filtering out uninteresting association rules. To tackle this weakness, a correlation measure can be used to augment the support–confidence framework for association rules. This leads to correlation rules of the form(6.7)

That is, a correlation rule is measured not only by its support and confidence but also by the correlation between itemsets A and B. There are many different correlation measures from which to choose. In this subsection, we study several correlation measures to determine which would be good for mining large data sets.

Lift is a simple correlation measure that is given as follows. The occurrence of itemset A is independent of the occurrence of itemset B if ; otherwise, itemsets A and B are dependent and correlated as events. This definition can easily be extended to more than two itemsets. The lift between the occurrence of A and B can be measured by computing(6.8)

If the resulting value of Eq. (6.8) is less than 1, then the occurrence of A is negatively correlated with the occurrence of B, meaning that the occurrence of one likely leads to the absence of the other one. If the resulting value is greater than 1, then A and B are positively correlated, meaning that the occurrence of one implies the occurrence of the other. If the resulting value is equal to 1, then A and B are independent and there is no correlation between them.

Equation (6.8) is equivalent to , or , which is also referred to as the lift of the association (or correlation) rule . In other words, it assesses the degree to which the occurrence of one「lifts」the occurrence of the other. For example, if A corresponds to the sale of computer games and B corresponds to the sale of videos, then given the current market conditions, the sale of games is said to increase or「lift」the likelihood of the sale of videos by a factor of the value returned by Eq. (6.8).

Let's go back to the computer game and video data of Example 6.7.

Correlation analysis using lift To help filter out misleading「strong」associations of the form from the data of Example 6.7, we need to study how the two itemsets, A and B, are correlated. Let refer to the transactions of Example 6.7 that do not contain computer games, and refer to those that do not contain videos. The transactions can be summarized in a contingency table, as shown in Table 6.6.

Table 6.6

2 × 2 Contingency Table Summarizing the Transactions with Respect to Game and Video Purchases

game

video 4000 3500 7500

2000 500 2500

6000 4000 10,000

From the table, we can see that the probability of purchasing a computer game is , the probability of purchasing a video is , and the probability of purchasing both is . By Eq. (6.8), the lift of Rule (6.6) is . Because this value is less than 1, there is a negative correlation between the occurrence of {game} and {video}. The numerator is the likelihood of a customer purchasing both, while the denominator is what the likelihood would have been if the two purchases were completely independent. Such a negative correlation cannot be identified by a support–confidence framework.

The second correlation measure that we study is the measure, which was introduced in Chapter 3 (Eq. 3.1). To compute the value, we take the squared difference between the observed and expected value for a slot (A and B pair) in the contingency table, divided by the expected value. This amount is summed for all slots of the contingency table. Let's perform a analysis of Example 6.8.

Correlation analysis using χ2 To compute the correlation using analysis for nominal data, we need the observed value and expected value (displayed in parenthesis) for each slot of the contingency table, as shown in Table 6.7. From the table, we can compute the value as follows:

Because the value is greater than 1, and the observed value of the slot (game, video) = 4000, which is less than the expected value of 4500, buying game and buying video are negatively correlated. This is consistent with the conclusion derived from the analysis of the lift measure in Example 6.8.

Table 6.7

Table 6.6 Contingency Table, Now with the Expected Values

game

video 4000 (4500) 3500 (3000) 7500

2000 (1500) 500 (1000) 2500

6000 4000 10,000

6.3.3. A Comparison of Pattern Evaluation Measures

The above discussion shows that instead of using the simple support–confidence framework to evaluate frequent patterns, other measures, such as lift and , often disclose more intrinsic pattern relationships. How effective are these measures? Should we also consider other alternatives?

Researchers have studied many pattern evaluation measures even before the start of in-depth research on scalable methods for mining frequent patterns. Recently, several other pattern evaluation measures have attracted interest. In this subsection, we present four such measures: all_confidence, max_confidence, Kulczynski, and cosine. We'll then compare their effectiveness with respect to one another and with respect to the lift and measures.

Given two itemsets, A and B, the all_confidence measure of A and B is defined as(6.9)

where max {sup (A), sup (B)} is the maximum support of the itemsets A and B. Thus, is also the minimum confidence of the two association rules related to A and B, namely,「」and「.」

Given two itemsets, A and B, the max_confidence measure of A and B is defined as(6.10)

The max_conf measure is the maximum confidence of the two association rules,「」and「.」

Given two itemsets, A and B, the Kulczynski measure of A and B (abbreviated as Kulc) is defined as(6.11)

It was proposed in 1927 by Polish mathematician S. Kulczynski. It can be viewed as an average of two confidence measures. That is, it is the average of two conditional probabilities: the probability of itemset B given itemset A, and the probability of itemset A given itemset B.

Finally, given two itemsets, A and B, the cosine measure of A and B is defined as(6.12)

The cosine measure can be viewed as a harmonized lift measure: The two formulae are similar except that for cosine, the square root is taken on the product of the probabilities of A and B. This is an important difference, however, because by taking the square root, the cosine value is only influenced by the supports of A, B, and , and not by the total number of transactions.

Each of these four measures defined has the following property: Its value is only influenced by the supports of A, B, and , or more exactly, by the conditional probabilities of and , but not by the total number of transactions. Another common property is that each measure ranges from 0 to 1, and the higher the value, the closer the relationship between A and B.

Now, together with lift and , we have introduced in total six pattern evaluation measures. You may wonder,「Which is the best in assessing the discovered pattern relationships?」To answer this question, we examine their performance on some typical data sets.

Comparison of six pattern evaluation measures on typical data sets The relationships between the purchases of two items, milk and coffee, can be examined by summarizing their purchase history in Table 6.8, a 2 × 2 contingency table, where an entry such as mc represents the number of transactions containing both milk and coffee.

Table 6.8

2 × 2 Contingency Table for Two Items

milk

coffee mc c

m Σ

Table 6.9 shows a set of transactional data sets with their corresponding contingency tables and the associated values for each of the six evaluation measures. Let's first examine the first four data sets, D1 through D4. From the table, we see that m and c are positively associated in D1 and D2, negatively associated in D3, and neutral in D4. For D1 and D2, m and c are positively associated because mc (10,000) is considerably greater than (1000) and (1000). Intuitively, for people who bought milk (), it is very likely that they also bought coffee (), and vice versa.

Table 6.9

Comparison of Six Pattern Evaluation Measures Using Contingency Tables for a Variety of Data Sets

Data

Setmcliftall_conf.max_conf.Kulc.cosine

D1 10,000 1000 1000 100,000 90557 9.26 0.91 0.91 0.91 0.91

D2 10,000 1000 1000 100 0 1 0.91 0.91 0.91 0.91

D3 100 1000 1000 100,000 670 8.44 0.09 0.09 0.09 0.09

D4 1000 1000 1000 100,000 24740 25.75 0.5 0.5 0.5 0.5

D5 1000 100 10,000 100,000 8173 9.18 0.09 0.91 0.5 0.29

D6 1000 10 100,000 100,000 965 1.97 0.01 0.99 0.5 0.10

The results of the four newly introduced measures show that m and c are strongly positively associated in both data sets by producing a measure value of 0.91. However, lift and generate dramatically different measure values for D1 and D2 due to their sensitivity to . In fact, in many real-world scenarios, is usually huge and unstable. For example, in a market basket database, the total number of transactions could fluctuate on a daily basis and overwhelmingly exceed the number of transactions containing any particular itemset. Therefore, a good interestingness measure should not be affected by transactions that do not contain the itemsets of interest; otherwise, it would generate unstable results, as illustrated in D1 and D2.

Similarly, in D3, the four new measures correctly show that m and c are strongly negatively associated because the m to c ratio equals the mc to m ratio, that is, . However, lift and both contradict this in an incorrect way: Their values for D2 are between those for D1 and D3.

For data set D4, both lift and indicate a highly positive association between m and c, whereas the others indicate a「neutral」association because the ratio of mc to equals the ratio of mc to , which is 1. This means that if a customer buys coffee (or milk), the probability that he or she will also purchase milk (or coffee) is exactly 50%.

「Why are lift and so poor at distinguishing pattern association relationships in the previous transactional data sets?」To answer this, we have to consider the null- transactions. A null-transaction is a transaction that does not contain any of the itemsets being examined. In our example, represents the number of null-transactions. Lift and have difficulty distinguishing interesting pattern association relationships because they are both strongly influenced by . Typically, the number of null-transactions can outweigh the number of individual purchases because, for example, many people may buy neither milk nor coffee. On the other hand, the other four measures are good indicators of interesting pattern associations because their definitions remove the influence of (i.e., they are not influenced by the number of null-transactions).

This discussion shows that it is highly desirable to have a measure that has a value that is independent of the number of null-transactions. A measure is null-invariant if its value is free from the influence of null-transactions. Null-invariance is an important property for measuring association patterns in large transaction databases. Among the six discussed measures in this subsection, only lift and are not null-invariant measures.

「Among the all_confidence, max_confidence, Kulczynski, and cosine measures, which is best at indicating interesting pattern relationships?」

To answer this question, we introduce the imbalance ratio (IR), which assesses the imbalance of two itemsets, A and B, in rule implications. It is defined as(6.13)

where the numerator is the absolute value of the difference between the support of the itemsets A and B, and the denominator is the number of transactions containing A or B. If the two directional implications between A and B are the same, then will be zero. Otherwise, the larger the difference between the two, the larger the imbalance ratio. This ratio is independent of the number of null-transactions and independent of the total number of transactions.

Let's continue examining the remaining data sets in Example 6.10.

Comparing null-invariant measures in pattern evaluation Although the four measures introduced in this section are null-invariant, they may present dramatically different values on some subtly different data sets. Let's examine data sets D5 and D6, shown earlier in Table 6.9, where the two events m and c have unbalanced conditional probabilities. That is, the ratio of mc to c is greater than 0.9. This means that knowing that c occurs should strongly suggest that m occurs also. The ratio of mc to m is less than 0.1, indicating that m implies that c is quite unlikely to occur. The all_confidence and cosine measures view both cases as negatively associated and the Kulc measure views both as neutral. The max_confidence measure claims strong positive associations for these cases. The measures give very diverse results!

「Which measure intuitively reflects the true relationship between the purchase of milk and coffee?」Due to the「balanced」skewness of the data, it is difficult to argue whether the two data sets have positive or negative association. From one point of view, only % of milk-related transactions contain coffee in D5 and this percentage is % in D6, both indicating a negative association. On the other hand, % of transactions in D5 (i.e., ) and 9% in D6 (i.e., ) containing coffee contain milk as well, which indicates a positive association between milk and coffee. These draw very different conclusions.

For such「balanced」skewness, it could be fair to treat it as neutral, as Kulc does, and in the meantime indicate its skewness using the imbalance ratio (IR). According to Eq. (6.13), for D4 we have , a perfectly balanced case; for D5, , a rather imbalanced case; whereas for D6, , a very skewed case. Therefore, the two measures, Kulc and , work together, presenting a clear picture for all three data sets, D4 through D6.

In summary, the use of only support and confidence measures to mine associations may generate a large number of rules, many of which can be uninteresting to users. Instead, we can augment the support–confidence framework with a pattern interestingness measure, which helps focus the mining toward rules with strong pattern relationships. The added measure substantially reduces the number of rules generated and leads to the discovery of more meaningful rules. Besides those introduced in this section, many other interestingness measures have been studied in the literature. Unfortunately, most of them do not have the null-invariance property. Because large data sets typically have many null-transactions, it is important to consider the null-invariance property when selecting appropriate interestingness measures for pattern evaluation. Among the four null-invariant measures studied here, namely all_confidence, max_confidence, Kulc, and cosine, we recommend using Kulc in conjunction with the imbalance ratio.

6.4. Summary

■ The discovery of frequent patterns, associations, and correlation relationships among huge amounts of data is useful in selective marketing, decision analysis, and business management. A popular area of application is market basket analysis, which studies customers' buying habits by searching for itemsets that are frequently purchased together (or in sequence).

■ Association rule mining consists of first finding frequent itemsets (sets of items, such as A and B, satisfying a minimum support threshold, or percentage of the task-relevant tuples), from which strong association rules in the form of are generated. These rules also satisfy a minimum confidence threshold (a prespecified probability of satisfying B under the condition that A is satisfied). Associations can be further analyzed to uncover correlation rules, which convey statistical correlations between itemsets A and B.

■ Many efficient and scalable algorithms have been developed for frequent itemset mining, from which association and correlation rules can be derived. These algorithms can be classified into three categories: (1) Apriori-like algorithms, (2) frequent pattern growth –based algorithms such as FP-growth, and (3) algorithms that use the vertical data format.

■ The Apriori algorithm is a seminal algorithm for mining frequent itemsets for Boolean association rules. It explores the level-wise mining Apriori property that all nonempty subsets of a frequent itemset must also be frequent. At the k th iteration (for ), it forms frequent k-itemset candidates based on the frequent (k − 1)-itemsets, and scans the database once to find the complete set of frequent k-itemsets, Lk.

Variations involving hashing and transaction reduction can be used to make the procedure more efficient. Other variations include partitioning the data (mining on each partition and then combining the results) and sampling the data (mining on a data subset). These variations can reduce the number of data scans required to as little as two or even one.

■ Frequent pattern growth is a method of mining frequent itemsets without candidate generation. It constructs a highly compact data structure (an FP-tree) to compress the original transaction database. Rather than employing the generate-and-test strategy of Apriori-like methods, it focuses on frequent pattern (fragment) growth, which avoids costly candidate generation, resulting in greater efficiency.

■ Mining frequent itemsets using the vertical data format (Eclat) is a method that transforms a given data set of transactions in the horizontal data format of TID-itemset into the vertical data format of item-TID_set. It mines the transformed data set by TID_set intersections based on the Apriori property and additional optimization techniques such as diffset.

■ Not all strong association rules are interesting. Therefore, the support–confidence framework should be augmented with a pattern evaluation measure, which promotes the mining of interesting rules. A measure is null-invariant if its value is free from the influence of null-transactions (i.e., the transactions that do not contain any of the itemsets being examined). Among many pattern evaluation measures, we examined lift, , all_confidence, max_confidence, Kulczynski, and cosine, and showed that only the latter four are null-invariant. We suggest using the Kulczynski measure, together with the imbalance ratio, to present pattern relationships among itemsets.

6.5. Exercises

6.1 Suppose you have the set of all frequent closed itemsets on a data set D, as well as the support count for each frequent closed itemset. Describe an algorithm to determine whether a given itemset X is frequent or not, and the support of X if it is frequent.

6.2 An itemset X is called a generator on a data set D if there does not exist a proper sub-itemset such that . A generator X is a frequent generator if passes the minimum support threshold. Let be the set of all frequent generators on a data set D.

(a) Can you determine whether an itemset A is frequent and the support of A, if it is frequent, using only and the support counts of all frequent generators? If yes, present your algorithm. Otherwise, what other information is needed? Can you give an algorithm assuming the information needed is available?

(b) What is the relationship between closed itemsets and generators?

6.3 The Apriori algorithm makes use of prior knowledge of subset support properties.

(a) Prove that all nonempty subsets of a frequent itemset must also be frequent.

(b) Prove that the support of any nonempty subset of itemset s must be at least as great as the support of s.

(c) Given frequent itemset l and subset s of l, prove that the confidence of the rule「」cannot be more than the confidence of「,」where is a subset of s.

(d) A partitioning variation of Apriori subdivides the transactions of a database D into n nonoverlapping partitions. Prove that any itemset that is frequent in D must be frequent in at least one partition of D.

6.4 Let c be a candidate itemset in Ck generated by the Apriori algorithm. How many length-(k − 1) subsets do we need to check in the prune step? Per your previous answer, can you give an improved version of procedure has_infrequent_subset in Figure 6.4?

6.5 Section 6.2.2 describes a method for generating association rules from frequent itemsets. Propose a more efficient method. Explain why it is more efficient than the one proposed there. (Hint: Consider incorporating the properties of (b) and (c) into your design.)

6.6 A database has five transactions. Let % and %.

TIDitems_bought

T100 {M, O, N, K, E, Y}

T200 {D, O, N, K, E, Y }

T300 {M, A, K, E}

T400 {M, U, C, K, Y}

T500 {C, O, O, K, I, E}

(a) Find all frequent itemsets using Apriori and FP-growth, respectively. Compare the efficiency of the two mining processes.

(b) List all the strong association rules (with support s and confidence c) matching the following metarule, where X is a variable representing customers, and denotes variables representing items (e.g.,「A,」「B,」):

6.7 (Implementation project) Using a programming language that you are familiar with, such as C++ or Java, implement three frequent itemset mining algorithms introduced in this chapter: (1) Apriori [AS94b], (2) FP-growth [HPY00] and (3) Eclat [Zak00] (mining using the vertical data format). Compare the performance of each algorithm with various kinds of large data sets. Write a report to analyze the situations (e.g., data size, data distribution, minimal support threshold setting, and pattern density) where one algorithm may perform better than the others, and state why.

6.8 A database has four transactions. Let % and %.

cust_IDTIDitems_bought (in the form of brand-item_category)

01 T100 {King's-Crab, Sunset-Milk, Dairyland-Cheese, Best-Bread}

02 T200 {Best-Cheese, Dairyland-Milk, Goldenfarm-Apple, Tasty-Pie, Wonder-Bread}

01 T300 {Westcoast-Apple, Dairyland-Milk, Wonder-Bread, Tasty-Pie}

03 T400 {Wonder-Bread, Sunset-Milk, Dairyland-Cheese}

(a) At the granularity of item_category (e.g., could be「Milk」), for the rule template,

list the frequent k-itemset for the largest k, and all the strong association rules (with their support s and confidence c) containing the frequent k-itemset for the largest k.

(b) At the granularity of brand-item_category (e.g., could be「Sunset-Milk」), for the rule template,

list the frequent k-itemset for the largest k (but do not print any rules).

6.9 Suppose that a large store has a transactional database that is distributed among four locations. Transactions in each component database have the same format, namely , where Tj is a transaction identifier, and ik () is the identifier of an item purchased in the transaction. Propose an efficient algorithm to mine global association rules. You may present your algorithm in the form of an outline. Your algorithm should not require shipping all the data to one site and should not cause excessive network communication overhead.

6.10 Suppose that frequent itemsets are saved for a large transactional database, . Discuss how to efficiently mine the (global) association rules under the same minimum support threshold, if a set of new transactions, denoted as , is (incrementally) added in?

6.11 Most frequent pattern mining algorithms consider only distinct items in a transaction. However, multiple occurrences of an item in the same shopping basket, such as four cakes and three jugs of milk, can be important in transactional data analysis. How can one mine frequent itemsets efficiently considering multiple occurrences of items? Propose modifications to the well-known algorithms, such as Apriori and FP-growth, to adapt to such a situation.

6.12 (Implementation project) Many techniques have been proposed to further improve the performance of frequent itemset mining algorithms. Taking FP-tree–based frequent pattern growth algorithms (e.g., FP-growth) as an example, implement one of the following optimization techniques. Compare the performance of your new implementation with the unoptimized version.

(a) The frequent pattern mining method of Section 6.2.4 uses an FP-tree to generate conditional pattern bases using a bottom-up projection technique (i.e., project onto the prefix path of an item p). However, one can develop a top-down projection technique, that is, project onto the suffix path of an item p in the generation of a conditional pattern base. Design and implement such a top-down FP-tree mining method. Compare its performance with the bottom-up projection method.

(b) Nodes and pointers are used uniformly in an FP-tree in the FP-growth algorithm design. However, such a structure may consume a lot of space when the data are sparse. One possible alternative design is to explore array- and pointer-based hybrid implementation, where a node may store multiple items when it contains no splitting point to multiple sub-branches. Develop such an implementation and compare it with the original one.

(c) It is time and space consuming to generate numerous conditional pattern bases during pattern-growth mining. An interesting alternative is to push right the branches that have been mined for a particular item p, that is, to push them to the remaining branch(es) of the FP-tree. This is done so that fewer conditional pattern bases have to be generated and additional sharing can be explored when mining the remaining FP-tree branches. Design and implement such a method and conduct a performance study on it.

6.13 Give a short example to show that items in a strong association rule actually may be negatively correlated.

6.14 The following contingency table summarizes supermarket transaction data, where hot dogs refers to the transactions containing hot dogs, refers to the transactions that do not contain hot dogs, hamburgers refers to the transactions containing hamburgers, and refers to the transactions that do not contain hamburgers.

hot dogs

hamburgers 2000 500 2500

1000 1500 2500

3000 2000 5000

(a) Suppose that the association rule「hot dogs ⇒hamburgers」is mined. Given a minimum support threshold of 25% and a minimum confidence threshold of 50%, is this association rule strong?

(b) Based on the given data, is the purchase of hot dogs independent of the purchase of hamburgers? If not, what kind of correlation relationship exists between the two?

(c) Compare the use of the all_confidence, max_confidence, Kulczynski, and cosine measures with lift and correlation on the given data.

6.15 (Implementation project) The DBLP data set (www.informatik.uni-trier.de/~ley/db/) consists of over one million entries of research papers published in computer science conferences and journals. Among these entries, there are a good number of authors that have coauthor relationships.

(a) Propose a method to efficiently mine a set of coauthor relationships that are closely correlated (e.g., often coauthoring papers together).

(b) Based on the mining results and the pattern evaluation measures discussed in this chapter, discuss which measure may convincingly uncover close collaboration patterns better than others.

(c) Based on the study in (a), develop a method that can roughly predict advisor and advisee relationships and the approximate period for such advisory supervision.

6.6. Bibliographic Notes

Association rule mining was first proposed by Agrawal, Imielinski, and Swami [AIS93]. The Apriori algorithm discussed in Section 6.2.1 for frequent itemset mining was presented in Agrawal and Srikant [AS94b]. A variation of the algorithm using a similar pruning heuristic was developed independently by Mannila, Tiovonen, and Verkamo [MTV94]. A joint publication combining these works later appeared in Agrawal, Mannila, Srikant et al. [AMS+96]. A method for generating association rules from frequent itemsets is described in Agrawal and Srikant [AS94a].

References for the variations of Apriori described in Section 6.2.3 include the following. The use of hash tables to improve association mining efficiency was studied by Park, Chen, and Yu [PCY95a]. The partitioning technique was proposed by Savasere, Omiecinski, and Navathe [SON95]. The sampling approach is discussed in Toivonen [Toi96]. A dynamic itemset counting approach is given in Brin, Motwani, Ullman, and Tsur [BMUT97]. An efficient incremental updating of mined association rules was proposed by Cheung, Han, Ng, and Wong [CHNW96]. Parallel and distributed association data mining under the Apriori framework was studied by Park, Chen, and Yu [PCY95b]; Agrawal and Shafer [AS96]; and Cheung, Han, Ng, et al. [CHN+96]. Another parallel association mining method, which explores itemset clustering using a vertical database layout, was proposed in Zaki, Parthasarathy, Ogihara, and Li [ZPOL97].

Other scalable frequent itemset mining methods have been proposed as alternatives to the Apriori-based approach. FP-growth, a pattern-growth approach for mining frequent itemsets without candidate generation, was proposed by Han, Pei, and Yin [HPY00] (Section 6.2.4). An exploration of hyper structure mining of frequent patterns, called H-Mine, was proposed by Pei, Han, Lu, et al. [PHL+01]. A method that integrates top-down and bottom-up traversal of FP-trees in pattern-growth mining was proposed by Liu, Pan, Wang, and Han [LPWH02]. An array-based implementation of prefix-tree structure for efficient pattern growth mining was proposed by Grahne and Zhu [GZ03b]. Eclat, an approach for mining frequent itemsets by exploring the vertical data format, was proposed by Zaki [Zak00]. A depth-first generation of frequent itemsets by a tree projection technique was proposed by Agarwal, Aggarwal, and Prasad [AAP01]. An integration of association mining with relational database systems was studied by Sarawagi, Thomas, and Agrawal [STA98].

The mining of frequent closed itemsets was proposed in Pasquier, Bastide, Taouil, and Lakhal [PBTL99], where an Apriori-based algorithm called A-Close for such mining was presented. CLOSET, an efficient closed itemset mining algorithm based on the frequent pattern growth method, was proposed by Pei, Han, and Mao [PHM00]. CHARM by Zaki and Hsiao [ZH02] developed a compact vertical TID list structure called diffset, which records only the difference in the TID list of a candidate pattern from its prefix pattern. A fast hash-based approach is also used in CHARM to prune nonclosed patterns. CLOSET+ by Wang, Han, and Pei [WHP03] integrates previously proposed effective strategies as well as newly developed techniques such as hybrid tree-projection and item skipping. AFOPT, a method that explores a right push operation on FP-trees during the mining process, was proposed by Liu, Lu, Lou, and Yu [LLLY03]. Grahne and Zhu [GZ03b] proposed a prefix-tree–based algorithm integrated with array representation, called FPClose, for mining closed itemsets using a pattern-growth approach.

Pan, Cong, Tung, et al. [PCT+03] proposed CARPENTER, a method for finding closed patterns in long biological data sets, which integrates the advantages of vertical data formats and pattern growth methods. Mining max-patterns was first studied by Bayardo [Bay98], where MaxMiner, an Apriori-based, level-wise, breadth-first search method, was proposed to find max-itemset by performing superset frequency pruning and subset infrequency pruning for search space reduction. Another efficient method, MAFIA, developed by Burdick, Calimlim, and Gehrke [BCG01], uses vertical bitmaps to compress TID lists, thus improving the counting efficiency. A FIMI (Frequent Itemset Mining Implementation) workshop dedicated to implementation methods for frequent itemset mining was reported by Goethals and Zaki [GZ03a].

The problem of mining interesting rules has been studied by many researchers. The statistical independence of rules in data mining was studied by Piatetski-Shapiro [P-S91]. The interestingness problem of strong association rules is discussed in Chen, Han, and Yu [CHY96]; Brin, Motwani, and Silverstein [BMS97]; and Aggarwal and Yu [AY99], which cover several interestingness measures, including lift. An efficient method for generalizing associations to correlations is given in Brin, Motwani, and Silverstein [BMS97]. Other alternatives to the support–confidence framework for assessing the interestingness of association rules are proposed in Brin, Motwani, Ullman, and Tsur [BMUT97] and Ahmed, El-Makky, and Taha [AEMT00].

A method for mining strong gradient relationships among itemsets was proposed by Imielinski, Khachiyan, and Abdulghani [IKA02]. Silverstein, Brin, Motwani, and Ullman [SBMU98] studied the problem of mining causal structures over transaction databases. Some comparative studies of different interestingness measures were done by Hilderman and Hamilton [HH01]. The notion of null transaction invariance was introduced, together with a comparative analysis of interestingness measures, by Tan, Kumar, and Srivastava [TKS02]. The use of all_confidence as a correlation measure for generating interesting association rules was studied by Omiecinski [Omi03] and by Lee, Kim, Cai, and Han [LKCH03]. Wu, Chen, and Han [WCH10] introduced the Kulczynski measure for associative patterns and performed a comparative analysis of a set of measures for pattern evaluation.

