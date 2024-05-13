		 11. Advanced Cluster Analysis

You learned the fundamentals of cluster analysis in Chapter 10. In this chapter, we discuss advanced topics of cluster analysis. Specifically, we investigate four major perspectives:■ Probabilistic model-based clustering: Section 11.1 introduces a general framework and a method for deriving clusters where each object is assigned a probability of belonging to a cluster. Probabilistic model-based clustering is widely used in many data mining applications such as text mining.

■ Clustering high-dimensional data: When the dimensionality is high, conventional distance measures can be dominated by noise. Section 11.2 introduces fundamental methods for cluster analysis on high-dimensional data.

■ Clustering graph and network data: Graph and network data are increasingly popular in applications such as online social networks, the World Wide Web, and digital libraries. In Section 11.3, you will study the key issues in clustering graph and network data, including similarity measurement and clustering methods.

■ Clustering with constraints: In our discussion so far, we do not assume any constraints in clustering. In some applications, however, various constraints may exist. These constraints may rise from background knowledge or spatial distribution of the objects. You will learn how to conduct cluster analysis with different kinds of constraints in Section 11.4.

By the end of this chapter, you will have a good grasp of the issues and techniques regarding advanced cluster analysis.

11.1. Probabilistic Model-Based Clustering

In all the cluster analysis methods we have discussed so far, each data object can be assigned to only one of a number of clusters. This cluster assignment rule is required in some applications such as assigning customers to marketing managers. However, in other applications, this rigid requirement may not be desirable. In this section, we demonstrate the need for fuzzy or flexible cluster assignment in some applications, and introduce a general method to compute probabilistic clusters and assignments.

「In what situations may a data object belong to more than one cluster?」Consider Example 11.1.

Clustering product reviews AllElectronics has an online store, where customers not only purchase online, but also create reviews of products. Not every product receives reviews; instead, some products may have many reviews, while many others have none or only a few. Moreover, a review may involve multiple products. Thus, as the review editor of AllElectronics, your task is to cluster the reviews.

Ideally, a cluster is about a topic, for example, a group of products, services, or issues that are highly related. Assigning a review to one cluster exclusively would not work well for your task. Suppose there is a cluster for「cameras and camcorders」and another for「computers.」What if a review talks about the compatibility between a camcorder and a computer? The review relates to both clusters; however, it does not exclusively belong to either cluster.

You would like to use a clustering method that allows a review to belong to more than one cluster if the review indeed involves more than one topic. To reflect the strength that a review belongs to a cluster, you want the assignment of a review to a cluster to carry a weight representing the partial membership.

The scenario where an object may belong to multiple clusters occurs often in many applications. This is illustrated in Example 11.2.

Clustering to study user search intent The AllElectronics online store records all customer browsing and purchasing behavior in a log. An important data mining task is to use the log data to categorize and understand user search intent. For example, consider a user session (a short period in which a user interacts with the online store). Is the user searching for a product, making comparisons among different products, or looking for customer support information? Clustering analysis helps here because it is difficult to predefine user behavior patterns thoroughly. A cluster that contains similar user browsing trajectories may represent similar user behavior.

However, not every session belongs to only one cluster. For example, suppose user sessions involving the purchase of digital cameras form one cluster, and user sessions that compare laptop computers form another cluster. What if a user in one session makes an order for a digital camera, and at the same time compares several laptop computers? Such a session should belong to both clusters to some extent.

In this section, we systematically study the theme of clustering that allows an object to belong to more than one cluster. We start with the notion of fuzzy clusters in Section 11.1.1. We then generalize the concept to probabilistic model-based clusters in Section 11.1.2. In Section 11.1.3, we introduce the expectation-maximization algorithm, a general framework for mining such clusters.

11.1.1. Fuzzy Clusters

Given a set of objects, , a fuzzy set S is a subset of X that allows each object in X to have a membership degree between 0 and 1. Formally, a fuzzy set, S, can be modeled as a function, .

Fuzzy set The more digital camera units that are sold, the more popular the camera is. In AllElectronics, we can use the following formula to compute the degree of popularity of a digital camera, o, given the sales of o:(11.1)

Function pop() defines a fuzzy set of popular digital cameras. For example, suppose the sales of digital cameras at AllElectronics are as shown in Table 11.1. The fuzzy set of popular digital cameras is , where the degrees of membership are written in parentheses.

Table 11.1

Set of Digital Cameras and Their Sales at AllElectronics

CameraSales (units)

A 50

B 1320

C 860

D 270

We can apply the fuzzy set idea on clusters. That is, given a set of objects, a cluster is a fuzzy set of objects. Such a cluster is called a fuzzy cluster. Consequently, a clustering contains multiple fuzzy clusters.

Formally, given a set of objects, o1, …, on, a fuzzy clustering of kfuzzy clusters, C1, …, Ck, can be represented using a partition matrix, , where wij is the membership degree of oi in fuzzy cluster Cj. The partition matrix should satisfy the following three requirements:■ For each object, oi, and cluster, Cj, . This requirement enforces that a fuzzy cluster is a fuzzy set.

■ For each object, oi, . This requirement ensures that every object participates in the clustering equivalently.

■ For each cluster, Cj, . This requirement ensures that for every cluster, there is at least one object for which the membership value is nonzero.

Fuzzy clusters Suppose the AllElectronics online store has six reviews. The keywords contained in these reviews are listed in Table 11.2.

We can group the reviews into two fuzzy clusters, C1 and C2. C1 is for「digital camera」and「lens," and C2 is for「computer.」The partition matrix is

Here, we use the keywords「digital camera」and「lens」as the features of cluster C1, and「computer」as the feature of cluster C2. For review, Ri, and cluster, Cj, wij is defined as

In this fuzzy clustering, review R4 belongs to clusters C1 and C2 with membership degrees and , respectively.

Table 11.2

Set of Reviews and the Keywords Used

Review_IDKeywords

R1 digital camera, lens

R2 digital camera

R3 lens

R4 digital camera, lens, computer

R5 computer, CPU

R6 computer, computer game

「How can we evaluate how well a fuzzy clustering describes a data set?」Consider a set of objects, , and a fuzzy clustering of k clusters, . Let be the partition matrix. Let be the centers of clusters , respectively. Here, a center can be defined either as the mean or the medoid, or in other ways specific to the application.

As discussed in Chapter 10, the distance or similarity between an object and the center of the cluster to which the object is assigned can be used to measure how well the object belongs to the cluster. This idea can be extended to fuzzy clustering. For any object, oi, and cluster, Cj, if , then measures how well oi is represented by cj, and thus belongs to cluster Cj. Because an object can participate in more than one cluster, the sum of distances to the corresponding cluster centers weighted by the degrees of membership captures how well the object fits the clustering.

Formally, for an object oi, the sum of the squared error (SSE) is given by(11.2)

where the parameter controls the influence of the degrees of membership. The larger the value of p, the larger the influence of the degrees of membership. Orthogonally, the SSE for a cluster, Cj, is(11.3)

Finally, the SSE of the clustering is defined as(11.4)

The SSE can be used to measure how well a fuzzy clustering fits a data set.

Fuzzy clustering is also called soft clustering because it allows an object to belong to more than one cluster. It is easy to see that traditional (rigid) clustering, which enforces each object to belong to only one cluster exclusively, is a special case of fuzzy clustering. We defer the discussion of how to compute fuzzy clustering to Section 11.1.3.

11.1.2. Probabilistic Model-Based Clusters

「Fuzzy clusters (Section 11.1.1) provide the flexibility of allowing an object to participate in multiple clusters. Is there a general framework to specify clusterings where objects may participate in multiple clusters in a probabilistic way?」In this section, we introduce the general notion of probabilistic model-based clusters to answer this question.

As discussed in Chapter 10, we conduct cluster analysis on a data set because we assume that the objects in the data set in fact belong to different inherent categories. Recall that clustering tendency analysis (Section 10.6.1) can be used to examine whether a data set contains objects that may lead to meaningful clusters. Here, the inherent categories hidden in the data are latent, which means they cannot be directly observed. Instead, we have to infer them using the data observed. For example, the topics hidden in a set of reviews in the AllElectronics online store are latent because one cannot read the topics directly. However, the topics can be inferred from the reviews because each review is about one or multiple topics.

Therefore, the goal of cluster analysis is to find hidden categories. A data set that is the subject of cluster analysis can be regarded as a sample of the possible instances of the hidden categories, but without any category labels. The clusters derived from cluster analysis are inferred using the data set, and are designed to approach the hidden categories.

Statistically, we can assume that a hidden category is a distribution over the data space, which can be mathematically represented using a probability density function (or distribution function). We call such a hidden category a probabilistic cluster. For a probabilistic cluster, C, its probability density function, f, and a point, o, in the data space, f(o) is the relative likelihood that an instance of C appears at o.

Probabilistic clusters Suppose the digital cameras sold by AllElectronics can be divided into two categories: C1, a consumer line (e.g., point-and-shoot cameras), and C2, a professional line (e.g., single-lens reflex cameras). Their respective probability density functions, f1 and f2, are shown in Figure 11.1 with respect to the attribute price.

For a price value of, say, $1000, f1 (1000) is the relative likelihood that the price of a consumer-line camera is $1000. Similarly, f2 (1000) is the relative likelihood that the price of a professional-line camera is $1000.

The probability density functions, f1 and f2, cannot be observed directly. Instead, AllElectronics can only infer these distributions by analyzing the prices of the digital cameras it sells. Moreover, a camera often does not come with a well-determined category (e.g.,「consumer line」or「professional line」). Instead, such categories are typically based on user background knowledge and can vary. For example, a camera in the prosumer segment may be regarded at the high end of the consumer line by some customers, and the low end of the professional line by others.

As an analyst at AllElectronics, you can consider each category as a probabilistic cluster, and conduct cluster analysis on the price of cameras to approach these categories.

Figure 11.1

The probability density functions of two probabilistic clusters.

Suppose we want to find k probabilistic clusters, , through cluster analysis. For a data set, D, of n objects, we can regard D as a finite sample of the possible instances of the clusters. Conceptually, we can assume that D is formed as follows. Each cluster, Cj, is associated with a probability, ωj, that some instance is sampled from the cluster. It is often assumed that are given as part of the problem setting, and that , which ensures that all objects are generated by the k clusters. Here, parameter ωj captures background knowledge about the relative population of cluster Cj.

We then run the following two steps to generate an object in D. The steps are executed n times in total to generate n objects, , in D.

1. Choose a cluster, Cj, according to probabilities .

2. Choose an instance of Cj according to its probability density function, fj.

The data generation process here is the basic assumption in mixture models. Formally, a mixture model assumes that a set of observed objects is a mixture of instances from multiple probabilistic clusters. Conceptually, each observed object is generated independently by two steps: first choosing a probabilistic cluster according to the probabilities of the clusters, and then choosing a sample according to the probability density function of the chosen cluster.

Given data set, D, and k, the number of clusters required, the task of probabilistic model-based cluster analysis is to infer a set of k probabilistic clusters that is most likely to generate D using this data generation process. An important question remaining is how we can measure the likelihood that a set of k probabilistic clusters and their probabilities will generate an observed data set.

Consider a set, C, of k probabilistic clusters, , with probability density functions , respectively, and their probabilities, . For an object, o, the probability that o is generated by cluster Cj is given by . Therefore, the probability that o is generated by the set C of clusters is(11.5)

Since the objects are assumed to have been generated independently, for a data set, , of n objects, we have(11.6)

Now, it is clear that the task of probabilistic model-based cluster analysis on a data set, D, is to find a set C of k probabilistic clusters such that is maximized. Maximizing is often intractable because, in general, the probability density function of a cluster can take an arbitrarily complicated form. To make probabilistic model-based clusters computationally feasible, we often compromise by assuming that the probability density functions are parameterized distributions.

Formally, let be the n observed objects, and be the parameters of the k distributions, denoted by and , respectively. Then, for any object, , Eq. (11.5) can be rewritten as(11.7)

where is the probability that oi is generated from the j th distribution using parameter Θj. Consequently, Eq. (11.6) can be rewritten as(11.8)

Using the parameterized probability distribution models, the task of probabilistic model-based cluster analysis is to infer a set of parameters, Θ, that maximizes Eq. (11.8).

Univariate Gaussian mixture model Let's use univariate Gaussian distributions as an example. That is, we assume that the probability density function of each cluster follows a 1-D Gaussian distribution. Suppose there are k clusters. The two parameters for the probability density function of each cluster are center, μj, and standard deviation, σj. We denote the parameters as and . Let the data set be , where oi is a real number. For any point, , we have(11.9)

Assuming that each cluster has the same probability, that is , and plugging Eq. (11.9) into Eq. (11.7), we have(11.10)

Applying Eq. (11.8), we have(11.11)

The task of probabilistic model-based cluster analysis using a univariate Gaussian mixture model is to infer Θ such that Eq. (11.11) is maximized.

11.1.3. Expectation-Maximization Algorithm

「How can we compute fuzzy clusterings and probabilistic model-based clusterings?」In this section, we introduce a principled approach. Let's start with a review of the k-means clustering problem and the k-means algorithm studied in Chapter 10.

It can easily be shown that k-means clustering is a special case of fuzzy clustering (Exercise 11.1). The k-means algorithm iterates until the clustering cannot be improved. Each iteration consists of two steps: The expectation step (E-step): Given the current cluster centers, each object is assigned to the cluster with a center that is closest to the object. Here, an object is expected to belong to the closest cluster.

The maximization step (M-step): Given the cluster assignment, for each cluster, the algorithm adjusts the center so that the sum of the distances from the objects assigned to this cluster and the new center is minimized. That is, the similarity of objects assigned to a cluster is maximized.

We can generalize this two-step method to tackle fuzzy clustering and probabilistic model-based clustering. In general, an expectation-maximization (EM) algorithm is a framework that approaches maximum likelihood or maximum a posteriori estimates of parameters in statistical models. In the context of fuzzy or probabilistic model-based clustering, an EM algorithm starts with an initial set of parameters and iterates until the clustering cannot be improved, that is, until the clustering converges or the change is sufficiently small (less than a preset threshold). Each iteration also consists of two steps:■ The expectation step assigns objects to clusters according to the current fuzzy clustering or parameters of probabilistic clusters.

■ The maximization step finds the new clustering or parameters that maximize the SSE in fuzzy clustering (Eq. 11.4) or the expected likelihood in probabilistic model-based clustering.

Fuzzy clustering using the EM algorithm Consider the six points in Figure 11.2, where the coordinates of the points are also shown. Let's compute two fuzzy clusters using the EM algorithm.

Figure 11.2

Data set for fuzzy clustering.

We randomly select two points, say and , as the initial centers of the two clusters. The first iteration conducts the expectation step and the maximization step as follows.

In the E-step, for each point we calculate its membership degree in each cluster. For any point, o, we assign o to c1 and c2 with membership weights

respectively, where is the Euclidean distance. The rationale is that, if o is close to c1 and is small, the membership degree of o with respect to c1 should be high. We also normalize the membership degrees so that the sum of degrees for an object is equal to 1.

For point a, we have and . That is, a exclusively belongs to c1. For point b, we have and . For point c, we have and . The degrees of membership of the other points are shown in the partition matrix in Table 11.3.

Table 11.3

Intermediate Results from the First Three Iterations of Example 11.7's EM Algorithm

IterationE-StepM-Step

1

2

3

In the M-step, we recalculate the centroids according to the partition matrix, minimizing the SSE given in Eq. (11.4). The new centroid should be adjusted to(11.12)

where .

In this example,

and

We repeat the iterations, where each iteration contains an E-step and an M-step. Table 11.3 shows the results from the first three iterations. The algorithm stops when the cluster centers converge or the change is small enough.

「How can we apply the EM algorithm to compute probabilistic model-based clustering?」Let's use a univariate Gaussian mixture model (Example 11.6) to illustrate.

Using the EM algorithm for mixture models Given a set of objects, , we want to mine a set of parameters, , such that in Eq. (11.11) is maximized, where are the mean and standard deviation, respectively, of the j th univariate Gaussian distribution, .

We can apply the EM algorithm. We assign random values to parameters Θ as the initial values. We then iteratively conduct the E-step and the M-step as follows until the parameters converge or the change is sufficiently small.

In the E-step, for each object, , we calculate the probability that oi belongs to each distribution, that is,(11.13)

In the M-step, we adjust the parameters Θ so that the expected likelihood in Eq. (11.11) is maximized. This can be achieved by setting(11.14)

and(11.15)

In many applications, probabilistic model-based clustering has been shown to be effective because it is more general than partitioning methods and fuzzy clustering methods. A distinct advantage is that appropriate statistical models can be used to capture latent clusters. The EM algorithm is commonly used to handle many learning problems in data mining and statistics due to its simplicity. Note that, in general, the EM algorithm may not converge to the optimal solution. It may instead converge to a local maximum. Many heuristics have been explored to avoid this. For example, we could run the EM process multiple times using different random initial values. Furthermore, the EM algorithm can be very costly if the number of distributions is large or the data set contains very few observed data points.

11.2. Clustering High-Dimensional Data

The clustering methods we have studied so far work well when the dimensionality is not high, that is, having less than 10 attributes. There are, however, important applications of high dimensionality.「How can we conduct cluster analysis on high-dimensional data?」

In this section, we study approaches to clustering high-dimensional data. Section 11.2.1 starts with an overview of the major challenges and the approaches used. Methods for high-dimensional data clustering can be divided into two categories: subspace clustering methods (Section 11.2.2) and dimensionality reduction methods (Section 11.2.3).

11.2.1. Clustering High-Dimensional Data: Problems, Challenges, and Major Methodologies

Before we present any specific methods for clustering high-dimensional data, let's first demonstrate the needs of cluster analysis on high-dimensional data using examples. We examine the challenges that call for new methods. We then categorize the major methods according to whether they search for clusters in subspaces of the original space, or whether they create a new lower-dimensionality space and search for clusters there.

In some applications, a data object may be described by 10 or more attributes. Such objects are referred to as a high-dimensional data space.

High-dimensional data and clustering AllElectronics keeps track of the products purchased by every customer. As a customer-relationship manager, you want to cluster customers into groups according to what they purchased from AllElectronics.

The customer purchase data are of very high dimensionality. AllElectronics carries tens of thousands of products. Therefore, a customer's purchase profile, which is a vector of the products carried by the company, has tens of thousands of dimensions.

「Are the traditional distance measures, which are frequently used in low-dimensional cluster analysis, also effective on high-dimensional data?」Consider the customers in Table 11.4, where 10 products, P1, …, P10, are used in demonstration. If a customer purchases a product, a 1 is set at the corresponding bit; otherwise, a 0 appears. Let's calculate the Euclidean distances (Eq. 2.16) among Ada, Bob, and Cathy. It is easy to see that

According to Euclidean distance, the three customers are equivalently similar (or dissimilar) to each other. However, a close look tells us that Ada should be more similar to Cathy than to Bob because Ada and Cathy share one common purchased item, P1.

Table 11.4

Customer Purchase Data

CustomerP1P2P3P4P5P6P7P8P9P10

Ada 1 0 0 0 0 0 0 0 0 0

Bob 0 0 0 0 0 0 0 0 0 1

Cathy 1 0 0 0 1 0 0 0 0 1

As shown in Example 11.9, the traditional distance measures can be ineffective on high-dimensional data. Such distance measures may be dominated by the noise in many dimensions. Therefore, clusters in the full, high-dimensional space can be unreliable, and finding such clusters may not be meaningful.

「Then what kinds of clusters are meaningful on high-dimensional data?」For cluster analysis of high-dimensional data, we still want to group similar objects together. However, the data space is often too big and too messy. An additional challenge is that we need to find not only clusters, but, for each cluster, a set of attributes that manifest the cluster. In other words, a cluster on high-dimensional data often is defined using a small set of attributes instead of the full data space. Essentially, clustering high-dimensional data should return groups of objects as clusters (as conventional cluster analysis does), in addition to, for each cluster, the set of attributes that characterize the cluster. For example, in Table 11.4, to characterize the similarity between Ada and Cathy, P1 may be returned as the attribute because Ada and Cathy both purchased P1.

Clustering high-dimensional data is the search for clusters and the space in which they exist. Thus, there are two major kinds of methods:■ Subspace clustering approaches search for clusters existing in subspaces of the given high-dimensional data space, where a subspace is defined using a subset of attributes in the full space. Subspace clustering approaches are discussed in Section 11.2.2.

■ Dimensionality reduction approaches try to construct a much lower-dimensional space and search for clusters in such a space. Often, a method may construct new dimensions by combining some dimensions from the original data. Dimensionality reduction methods are the topic of Section 11.2.4.

In general, clustering high-dimensional data raises several new challenges in addition to those of conventional clustering:■ A major issue is how to create appropriate models for clusters in high-dimensional data. Unlike conventional clusters in low-dimensional spaces, clusters hidden in high-dimensional data are often significantly smaller. For example, when clustering customer-purchase data, we would not expect many users to have similar purchase patterns. Searching for such small but meaningful clusters is like finding needles in a haystack. As shown before, the conventional distance measures can be ineffective. Instead, we often have to consider various more sophisticated techniques that can model correlations and consistency among objects in subspaces.

■ There are typically an exponential number of possible subspaces or dimensionality reduction options, and thus the optimal solutions are often computationally prohibitive. For example, if the original data space has 1000 dimensions, and we want to find clusters of dimensionality 10, then there are possible subspaces.

11.2.2. Subspace Clustering Methods

「How can we find subspace clusters from high-dimensional data?」Many methods have been proposed. They generally can be categorized into three major groups: subspace search methods, correlation-based clustering methods, and biclustering methods.

Subspace Search Methods

A subspace search method searches various subspaces for clusters. Here, a cluster is a subset of objects that are similar to each other in a subspace. The similarity is often captured by conventional measures such as distance or density. For example, the CLIQUE algorithm introduced in Section 10.5.2 is a subspace clustering method. It enumerates subspaces and the clusters in those subspaces in a dimensionality-increasing order, and applies antimonotonicity to prune subspaces in which no cluster may exist.

A major challenge that subspace search methods face is how to search a series of subspaces effectively and efficiently. Generally there are two kinds of strategies:■ Bottom-up approaches start from low-dimensional subspaces and search higher-dimensional subspaces only when there may be clusters in those higher-dimensional subspaces. Various pruning techniques are explored to reduce the number of higher-dimensional subspaces that need to be searched. CLIQUE is an example of a bottom-up approach.

■ Top-down approaches start from the full space and search smaller and smaller subspaces recursively. Top-down approaches are effective only if the locality assumption holds, which require that the subspace of a cluster can be determined by the local neighborhood.

PROCLUS, a top-down subspace approach PROCLUS is a k-medoid-like method that first generates k potential cluster centers for a high-dimensional data set using a sample of the data set. It then refines the subspace clusters iteratively. In each iteration, for each of the current k-medoids, PROCLUS considers the local neighborhood of the medoid in the whole data set, and identifies a subspace for the cluster by minimizing the standard deviation of the distances of the points in the neighborhood to the medoid on each dimension. Once all the subspaces for the medoids are determined, each point in the data set is assigned to the closest medoid according to the corresponding subspace. Clusters and possible outliers are identified. In the next iteration, new medoids replace existing ones if doing so improves the clustering quality.

Correlation-Based Clustering Methods

While subspace search methods search for clusters with a similarity that is measured using conventional metrics like distance or density, correlation-based approaches can further discover clusters that are defined by advanced correlation models.

A correlation-based approach using PCA As an example, a PCA-based approach first applies PCA (Principal Components Analysis; see Chapter 3) to derive a set of new, uncorrelated dimensions, and then mine clusters in the new space or its subspaces. In addition to PCA, other space transformations may be used, such as the Hough transform or fractal dimensions.

For additional details on subspace search methods and correlation-based clustering methods, please refer to the bibliographic notes (Section 11.7).

Biclustering Methods

In some applications, we want to cluster both objects and attributes simultaneously. The resulting clusters are known as biclusters and meet four requirements: (1) only a small set of objects participate in a cluster; (2) a cluster only involves a small number of attributes; (3) an object may participate in multiple clusters, or does not participate in any cluster; and (4) an attribute may be involved in multiple clusters, or is not involved in any cluster. Section 11.2.3 discusses biclustering in detail.

11.2.3. Biclustering

In the cluster analysis discussed so far, we cluster objects according to their attribute values. Objects and attributes are not treated in the same way. However, in some applications, objects and attributes are defined in a symmetric way, where data analysis involves searching data matrices for submatrices that show unique patterns as clusters. This kind of clustering technique belongs to the category of biclustering.

This section first introduces two motivating application examples of biclustering–gene expression and recommender systems. You will then learn about the different types of biclusters. Last, we present biclustering methods.

Application Examples

Biclustering techniques were first proposed to address the needs for analyzing gene expression data. A gene is a unit of the passing-on of traits from a living organism to its offspring. Typically, a gene resides on a segment of DNA. Genes are critical for all living things because they specify all proteins and functional RNA chains. They hold the information to build and maintain a living organism's cells and pass genetic traits to offspring. Synthesis of a functional gene product, either RNA or protein, relies on the process of gene expression. A genotype is the genetic makeup of a cell, an organism, or an individual. Phenotypes are observable characteristics of an organism. Gene expression is the most fundamental level in genetics in that genotypes cause phenotypes.

Using DNA chips (also known as DNA microarrays ) and other biological engineering techniques, we can measure the expression level of a large number (possibly all) of an organism's genes, in a number of different experimental conditions. Such conditions may correspond to different time points in an experiment or samples from different organs. Roughly speaking, the gene expression data or DNA microarray data are conceptually a gene-sample/condition matrix, where each row corresponds to one gene, and each column corresponds to one sample or condition. Each element in the matrix is a real number and records the expression level of a gene under a specific condition. Figure 11.3 shows an illustration.

Figure 11.3

Microarrary data matrix.

From the clustering viewpoint, an interesting issue is that a gene expression data matrix can be analyzed in two dimensions—the gene dimension and the sample/ condition dimension.

■ When analyzing in the gene dimension, we treat each gene as an object and treat the samples/conditions as attributes. By mining in the gene dimension, we may find patterns shared by multiple genes, or cluster genes into groups. For example, we may find a group of genes that express themselves similarly, which is highly interesting in bioinformatics, such as in finding pathways.

■ When analyzing in the sample/condition dimension, we treat each sample/condition as an object and treat the genes as attributes. In this way, we may find patterns of samples/conditions, or cluster samples/conditions into groups. For example, we may find the differences in gene expression by comparing a group of tumor samples and nontumor samples.

Gene expression Gene expression matrices are popular in bioinformatics research and development. For example, an important task is to classify a new gene using the expression data of the gene and that of other genes in known classes. Symmetrically, we may classify a new sample (e.g., a new patient) using the expression data of the sample and that of samples in known classes (e.g., tumor and nontumor). Such tasks are invaluable in understanding the mechanisms of diseases and in clinical treatment.

As can be seen, many gene expression data mining problems are highly related to cluster analysis. However, a challenge here is that, instead of clustering in one dimension (e.g., gene or sample/condition), in many cases we need to cluster in two dimensions simultaneously (e.g., both gene and sample/condition). Moreover, unlike the clustering models we have discussed so far, a cluster in a gene expression data matrix is a submatrix and usually has the following characteristics:■ Only a small set of genes participate in the cluster.

■ The cluster involves only a small subset of samples/conditions.

■ A gene may participate in multiple clusters, or may not participate in any cluster.

■ A sample/condition may be involved in multiple clusters, or may not be involved in any cluster.

To find clusters in gene-sample/condition matrices, we need new clustering techniques that meet the following requirements for biclustering:■ A cluster of genes is defined using only a subset of samples/conditions.

■ A cluster of samples/conditions is defined using only a subset of genes.

■ The clusters are neither exclusive (e.g., where one gene can participate in multiple clusters) nor exhaustive (e.g., where a gene may not participate in any cluster).

Biclustering is useful not only in bioinformatics, but also in other applications as well. Consider recommender systems as an example.

Using biclustering for a recommender system AllElectronics collects data from customers' evaluations of products and uses the data to recommend products to customers. The data can be modeled as a customer-product matrix, where each row represents a customer, and each column represents a product. Each element in the matrix represents a customer's evaluation of a product, which may be a score (e.g., like, like somewhat, not like) or purchase behavior (e.g., buy or not). Figure 11.4 illustrates the structure.

The customer-product matrix can be analyzed in two dimensions: the customer dimension and the product dimension. Treating each customer as an object and products as attributes, AllElectronics can find customer groups that have similar preferences or purchase patterns. Using products as objects and customers as attributes, AllElectronics can mine product groups that are similar in customer interest.

Moreover, AllElectronics can mine clusters in both customers and products simultaneously. Such a cluster contains a subset of customers and involves a subset of products. For example, AllElectronics is highly interested in finding a group of customers who all like the same group of products. Such a cluster is a submatrix in the customer-product matrix, where all elements have a high value. Using such a cluster, AllElectronics can make recommendations in two directions. First, the company can recommend products to new customers who are similar to the customers in the cluster. Second, the company can recommend to customers new products that are similar to those involved in the cluster.

Figure 11.4

Customer-product matrix.

As with biclusters in a gene expression data matrix, the biclusters in a customer-product matrix usually have the following characteristics:■ Only a small set of customers participate in a cluster.

■ A cluster involves only a small subset of products.

■ A customer can participate in multiple clusters, or may not participate in any cluster.

■ A product may be involved in multiple clusters, or may not be involved in any cluster.

Biclustering can be applied to customer-product matrices to mine clusters satisfying these requirements.

11.2.3. Types of Biclusters

「How can we model biclusters and mine them?」Let's start with some basic notation. For the sake of simplicity, we will use「genes」and「conditions」to refer to the two dimensions in our discussion. Our discussion can easily be extended to other applications. For example, we can simply replace「genes」and「conditions」by「customers」and「products」to tackle the customer-product biclustering problem.

Let be a set of genes and be a set of conditions. Let be a gene expression data matrix, that is, a gene-condition matrix, where and . A submatrix I × J is defined by a subset of genes and a subset of conditions. For example, in the matrix shown in Figure 11.5, is a submatrix.

Figure 11.5

Gene-condition matrix, a submatrix, and a bicluster.

A bicluster is a submatrix where genes and conditions follow consistent patterns. We can define different types of biclusters based on such patterns.

■ As the simplest case, a submatrix I × J is a bicluster with constant values if for any and , , where c is a constant. For example, the submatrix in Figure 11.5 is a bicluster with constant values.

■ A bicluster is interesting if each row has a constant value, though different rows may have different values. A bicluster with constant values on rows is a submatrix I × J such that for any and , , where αi is the adjustment for row i. For example, Figure 11.6 shows a bicluster with constant values on rows.

Symmetrically, a bicluster with constant values on columns is a submatrix I × J such that for any and , , where βj is the adjustment for column j.

■ More generally, a bicluster is interesting if the rows change in a synchronized way with respect to the columns and vice versa. Mathematically, a bicluster with coherent values (also known as a pattern-based cluster ) is a submatrix I × J such that for any and , , where αi and βj are the adjustment for row i and column j, respectively. For example, Figure 11.7 shows a bicluster with coherent values.

It can be shown that I × J is a bicluster with coherent values if and only if for any and , then . Moreover, instead of using addition, we can define a bicluster with coherent values using multiplication, that is, . Clearly, biclusters with constant values on rows or columns are special cases of biclusters with coherent values.

■ In some applications, we may only be interested in the up- or down-regulated changes across genes or conditions without constraining the exact values. A bicluster with coherent evolutions on rows is a submatrix I × J such that for any and , . For example, Figure 11.8 shows a bicluster with coherent evolutions on rows. Symmetrically, we can define biclusters with coherent evolutions on columns.

Figure 11.6

Bicluster with constant values on rows.

Figure 11.7

Bicluster with coherent values.

Figure 11.8

Bicluster with coherent evolutions on rows.

Next, we study how to mine biclusters.

Biclustering Methods

The previous specification of the types of biclusters only considers ideal cases. In real data sets, such perfect biclusters rarely exist. When they do exist, they are usually very small. Instead, random noise can affect the readings of eij and thus prevent a bicluster in nature from appearing in a perfect shape.

There are two major types of methods for discovering biclusters in data that may come with noise. Optimization-based methods conduct an iterative search. At each iteration, the submatrix with the highest significance score is identified as a bicluster. The process terminates when a user-specified condition is met. Due to cost concerns in computation, greedy search is often employed to find local optimal biclusters. Enumeration methods use a tolerance threshold to specify the degree of noise allowed in the biclusters to be mined, and then tries to enumerate all submatrices of biclusters that satisfy the requirements. We use the δ-Cluster and MaPle algorithms as examples to illustrate these ideas.

Optimization Using the δ-Cluster Algorithm

For a submatrix, I × J, the mean of the i th row is(11.16)

Symmetrically, the mean of the j th column is(11.17)

The mean of all elements in the submatrix is(11.18)

The quality of the submatrix as a bicluster can be measured by the mean-squared residue value as(11.19)

Submatrix I × J is a δ-bicluster if , where is a threshold. When , I × J is a perfect bicluster with coherent values. By setting , a user can specify the tolerance of average noise per element against a perfect bicluster, because in Eq. (11.19) the residue on each element is(11.20)

A maximal δ-bicluster is a δ-bicluster I × J such that there does not exist another δ-bicluster , and , , and at least one inequality holds. Finding the maximal δ-bicluster of the largest size is computationally costly. Therefore, we can use a heuristic greedy search method to obtain a local optimal cluster. The algorithm works in two phases.

■ In the deletion phase, we start from the whole matrix. While the mean-squared residue of the matrix is over δ, we iteratively remove rows and columns. At each iteration, for each row i, we compute the mean-squared residue as(11.21)

Moreover, for each column j, we compute the mean-squared residue as(11.22)

We remove the row or column of the largest mean-squared residue. At the end of this phase, we obtain a submatrix I × J that is a δ-bicluster. However, the submatrix may not be maximal.

■ In the addition phase, we iteratively expand the δ-bicluster I × J obtained in the deletion phase as long as the δ-bicluster requirement is maintained. At each iteration, we consider rows and columns that are not involved in the current bicluster I × J by calculating their mean-squared residues. A row or column of the smallest mean-squared residue is added into the current δ-bicluster.

This greedy algorithm can find one δ-bicluster only. To find multiple biclusters that do not have heavy overlaps, we can run the algorithm multiple times. After each execution where a δ-bicluster is output, we can replace the elements in the output bicluster by random numbers. Although the greedy algorithm may find neither the optimal biclusters nor all biclusters, it is very fast even on large matrices.

Enumerating All Biclusters Using MaPle

As mentioned, a submatrix I × J is a bicluster with coherent values if and only if for any and , . For any submatrix of I × J, we can define a p-score as(11.23)

A submatrix I × J is a δ-pCluster (for p attern-based cluster ) if the p-score of every submatrix of I × J is at most δ, where is a threshold specifying a user's tolerance of noise against a perfect bicluster. Here, the p-score controls the noise on every element in a bicluster, while the mean-squared residue captures the average noise.

An interesting property of δ-pCluster is that if I × J is a δ-pCluster, then every x × y (x, y ≥ 2) submatrix of I × J is also a δ-pCluster. This monotonicity enables us to obtain a succinct representation of nonredundant δ-pClusters. A δ-pCluster is maximal if no more rows or columns can be added into the cluster while maintaining the δ-pCluster property. To avoid redundancy, instead of finding all δ-pClusters, we only need to compute all maximal δ-pClusters.

MaPle is an algorithm that enumerates all maximal δ-pClusters. It systematically enumerates every combination of conditions using a set enumeration tree and a depth-first search. This enumeration framework is the same as the pattern-growth methods for frequent pattern mining (Chapter 6). Consider gene expression data. For each condition combination, J, MaPle finds the maximal subsets of genes, I, such that I × J is a δ-pCluster. If I × J is not a submatrix of another δ-pCluster, then I × J is a maximal δ-pCluster.

There may be a huge number of condition combinations. MaPle prunes many unfruitful combinations using the monotonicity of δ-pClusters. For a condition combination, J, if there does not exist a set of genes, I, such that I × J is a δ-pCluster, then we do not need to consider any superset of J. Moreover, we should consider I × J as a candidate of a δ-pCluster only if for every -subset J′ of J, is a δ-pCluster. MaPle also employs several pruning techniques to speed up the search while retaining the completeness of returning all maximal δ-pClusters. For example, when examining a current δ-pCluster, I × J, MaPle collects all the genes and conditions that may be added to expand the cluster. If these candidate genes and conditions together with I and J form a submatrix of a δ-pCluster that has already been found, then the search of I × J and any superset of J can be pruned. Interested readers may refer to the bibliographic notes for additional information on the MaPle algorithm (Section 11.7).

An interesting observation here is that the search for maximal δ-pClusters in MaPle is somewhat similar to mining frequent closed itemsets. Consequently, MaPle borrows the depth-first search framework and ideas from the pruning techniques of pattern-growth methods for frequent pattern mining. This is an example where frequent pattern mining and cluster analysis may share similar techniques and ideas.

An advantage of MaPle and the other algorithms that enumerate all biclusters is that they guarantee the completeness of the results and do not miss any overlapping biclusters. However, a challenge for such enumeration algorithms is that they may become very time consuming if a matrix becomes very large, such as a customer-purchase matrix of hundreds of thousands of customers and millions of products.

11.2.4. Dimensionality Reduction Methods and Spectral Clustering

Subspace clustering methods try to find clusters in subspaces of the original data space. In some situations, it is more effective to construct a new space instead of using subspaces of the original data. This is the motivation behind dimensionality reduction methods for clustering high-dimensional data.

Clustering in a derived space Consider the three clusters of points in Figure 11.9. It is not possible to cluster these points in any subspace of the original space, X × Y, because all three clusters would end up being projected onto overlapping areas in the x and y axes. What if, instead, we construct a new dimension, (shown as a dashed line in the figure)? By projecting the points onto this new dimension, the three clusters become apparent.

Figure 11.9

Clustering in a derived space may be more effective.

Although Example 11.14 involves only two dimensions, the idea of constructing a new space (so that any clustering structure that is hidden in the data becomes well manifested) can be extended to high-dimensional data. Preferably, the newly constructed space should have low dimensionality.

There are many dimensionality reduction methods. A straightforward approach is to apply feature selection and extraction methods to the data set such as those discussed in Chapter 3. However, such methods may not be able to detect the clustering structure. Therefore, methods that combine feature extraction and clustering are preferred. In this section, we introduce spectral clustering, a group of methods that are effective in high-dimensional data applications.

Figure 11.10 shows the general framework for spectral clustering approaches. The Ng-Jordan-Weiss algorithm is a spectral clustering method. Let's have a look at each step of the framework. In doing so, we also note special conditions that apply to the Ng-Jordan-Weiss algorithm as an example.

Figure 11.10

The framework of spectral clustering approaches.

Source: Adapted from Slide 8 at http://videolectures.net/micued08_azran_mcl/.

Given a set of objects, , the distance between each pair of objects, , and the desired number k of clusters, a spectral clustering approach works as follows.

Using the distance measure, calculate an affinity matrix, W, such that

where σ is a scaling parameter that controls how fast the affinity Wij decreases as increases. In the Ng-Jordan-Weiss algorithm, Wii is set to 0.

Using the affinity matrix W, derive a matrix . The way in which this is done can vary. The Ng-Jordan-Weiss algorithm defines a matrix, D, as a diagonal matrix such that Dii is the sum of the i th row of W, that is,(11.24)

A is then set to(11.25)

Find the k leading eigenvectors of A. Recall that the eigenvectors of a square matrix are the nonzero vectors that remain proportional to the original vector after being multiplied by the matrix. Mathematically, a vector v is an eigenvector of matrix A if , where λ is called the corresponding eigenvalue. This step derives k new dimensions from A, which are based on the affinity matrix W. Typically, k should be much smaller than the dimensionality of the original data.

The Ng-Jordan-Weiss algorithm computes the k eigenvectors with the largest eigenvalues of A.

Using the k leading eigenvectors, project the original data into the new space defined by the k leading eigenvectors, and run a clustering algorithm such as k-means to find k clusters.

The Ng-Jordan-Weiss algorithm stacks the k largest eigenvectors in columns to form a matrix . The algorithm forms a matrix Y by renormalizing each row in X to have unit length, that is,(11.26)

The algorithm then treats each row in Y as a point in the k-dimensional space , and runs k-means (or any other algorithm serving the partitioning purpose) to cluster the points into k clusters.

Assign the original data points to clusters according to how the transformed points are assigned in the clusters obtained in step 4.

In the Ng-Jordan-Weiss algorithm, the original object oi is assigned to the j th cluster if and only if matrix Y's row i is assigned to the j th cluster as a result of step 4.

In spectral clustering methods, the dimensionality of the new space is set to the desired number of clusters. This setting expects that each new dimension should be able to manifest a cluster.

The Ng-Jordan-Weiss algorithm Consider the set of points in Figure 11.11. The data set, the affinity matrix, the three largest eigenvectors, and the normalized vectors are shown. Note that with the three new dimensions (formed by the three largest eigenvectors), the clusters are easily detected.

Figure 11.11

The new dimensions and the clustering results of the Ng-Jordan-Weiss algorithm.

Source: Adapted from Slide 9 at http://videolectures.net/micued08_azran_mcl/.

Spectral clustering is effective in high-dimensional applications such as image processing. Theoretically, it works well when certain conditions apply. Scalability, however, is a challenge. Computing eigenvectors on a large matrix is costly. Spectral clustering can be combined with other clustering methods, such as biclustering. Additional information on other dimensionality reduction clustering methods, such as kernel PCA, can be found in the bibliographic notes (Section 11.7).

11.3. Clustering Graph and Network Data

Cluster analysis on graph and network data extracts valuable knowledge and information. Such data are increasingly popular in many applications. We discuss applications and challenges of clustering graph and network data in Section 11.3.1. Similarity measures for this form of clustering are given in Section 11.3.2. You will learn about graph clustering methods in Section 11.3.3.

In general, the terms graph and network can be used interchangeably. In the rest of this section, we mainly use the term graph.

11.3.1. Applications and Challenges

As a customer relationship manager at AllElectronics, you notice that a lot of data relating to customers and their purchase behavior can be preferably modeled using graphs.

Bipartite graph The customer purchase behavior at AllElectronics can be represented in a bipartite graph. In a bipartite graph, vertices can be divided into two disjoint sets so that each edge connects a vertex in one set to a vertex in the other set. For the AllElectronics customer purchase data, one set of vertices represents customers, with one customer per vertex. The other set represents products, with one product per vertex. An edge connects a customer to a product, representing the purchase of the product by the customer. Figure 11.12 shows an illustration.

「What kind of knowledge can we obtain by a cluster analysis of the customer-product bipartite graph?」By clustering the customers such that those customers buying similar sets of products are placed into one group, a customer relationship manager can make product recommendations. For example, suppose Ada belongs to a customer cluster in which most of the customers purchased a digital camera in the last 12 months, but Ada has yet to purchase one. As manager, you decide to recommend a digital camera to her.

Alternatively, we can cluster products such that those products purchased by similar sets of customers are grouped together. This clustering information can also be used for product recommendations. For example, if a digital camera and a high-speed flash memory card belong to the same product cluster, then when a customer purchases a digital camera, we can recommend the high-speed flash memory card.

Figure 11.12

Bipartite graph representing customer-purchase data.

Bipartite graphs are widely used in many applications. Consider another example.

Web search engines In web search engines, search logs are archived to record user queries and the corresponding click-through information. (The click-through information tells us on which pages, given as a result of a search, the user clicked.) The query and click-through information can be represented using a bipartite graph, where the two sets of vertices correspond to queries and web pages, respectively. An edge links a query to a web page if a user clicks the web page when asking the query. Valuable information can be obtained by cluster analyses on the query–web page bipartite graph. For instance, we may identify queries posed in different languages, but that mean the same thing, if the click-through information for each query is similar.

As another example, all the web pages on the Web form a directed graph, also known as the web graph, where each web page is a vertex, and each hyperlink is an edge pointing from a source page to a destination page. Cluster analysis on the web graph can disclose communities, find hubs and authoritative web pages, and detect web spams.

In addition to bipartite graphs, cluster analysis can also be applied to other types of graphs, including general graphs, as elaborated Example 11.18.

Social network A social network is a social structure. It can be represented as a graph, where the vertices are individuals or organizations, and the links are interdependencies between the vertices, representing friendship, common interests, or collaborative activities. AllElectronics' customers form a social network, where each customer is a vertex, and an edge links two customers if they know each other.

As customer relationship manager, you are interested in finding useful information that can be derived from AllElectronics' social network through cluster analysis. You obtain clusters from the network, where customers in a cluster know each other or have friends in common. Customers within a cluster may influence one another regarding purchase decision making. Moreover, communication channels can be designed to inform the「heads」of clusters (i.e., the「best」connected people in the clusters), so that promotional information can be spread out quickly. Thus, you may use customer clustering to promote sales at AllElectronics.

As another example, the authors of scientific publications form a social network, where the authors are vertices and two authors are connected by an edge if they coauthored a publication. The network is, in general, a weighted graph because an edge between two authors can carry a weight representing the strength of the collaboration such as how many publications the two authors (as the end vertices) coauthored. Clustering the coauthor network provides insight as to communities of authors and patterns of collaboration.

「Are there any challenges specific to cluster analysis on graph and network data?」In most of the clustering methods discussed so far, objects are represented using a set of attributes. A unique feature of graph and network data is that only objects (as vertices) and relationships between them (as edges) are given. No dimensions or attributes are explicitly defined. To conduct cluster analysis on graph and network data, there are two major new challenges.

■「How can we measure the similarity between two objects on a graph accordingly?」Typically, we cannot use conventional distance measures, such as Euclidean distance. Instead, we need to develop new measures to quantify the similarity. Such measures often are not metric, and thus raise new challenges regarding the development of efficient clustering methods. Similarity measures for graphs are discussed in Section 11.3.2.

■「How can we design clustering models and methods that are effective on graph and network data?」Graph and network data are often complicated, carrying topological structures that are more sophisticated than traditional cluster analysis applications. Many graph data sets are large, such as the web graph containing at least tens of billions of web pages in the publicly indexable Web. Graphs can also be sparse where, on average, a vertex is connected to only a small number of other vertices in the graph. To discover accurate and useful knowledge hidden deep in the data, a good clustering method has to accommodate these factors. Clustering methods for graph and network data are introduced in Section 11.3.3.

11.3.2. Similarity Measures

「How can we measure the similarity or distance between two vertices in a graph?」In our discussion, we examine two types of measures: geodesic distance and distance based on random walk.

Geodesic Distance

A simple measure of the distance between two vertices in a graph is the shortest path between the vertices. Formally, the geodesic distance between two vertices is the length in terms of the number of edges of the shortest path between the vertices. For two vertices that are not connected in a graph, the geodesic distance is defined as infinite.

Using geodesic distance, we can define several other useful measurements for graph analysis and clustering. Given a graph , where V is the set of vertices and E is the set of edges, we define the following:■ For a vertext , the eccentricity of v, denoted , is the largest geodesic distance between v and any other vertex . The eccentricity of v captures how far away v is from its remotest vertex in the graph.

■ The radius of graph G is the minimum eccentricity of all vertices. That is,(11.27)

The radius captures the distance between the「most central point」and the「farthest border」of the graph.

■ The diameter of graph G is the maximum eccentricity of all vertices. That is,(11.28)

The diameter represents the largest distance between any pair of vertices.

■ A peripheral vertex is a vertex that achieves the diameter.

Measurements based on geodesic distance Consider graph G in Figure 11.13. The eccentricity of a is 2, that is, , , and . Thus, the radius of G is 2, and the diameter is 3. Note that it is not necessary that . Vertices c, d, and e are peripheral vertices.

Figure 11.13

A graph, G, where vertices c, d, and e are peripheral.

SimRank: Similarity Based on Random Walk and Structural Context

For some applications, geodesic distance may be inappropriate in measuring the similarity between vertices in a graph. Here we introduce SimRank, a similarity measure based on random walk and on the structural context of the graph. In mathematics, a random walk is a trajectory that consists of taking successive random steps.

Similarity between people in a social network Let's consider measuring the similarity between two vertices in the AllElectronics customer social network of Example 11.18. Here, similarity can be explained as the closeness between two participants in the network, that is, how close two people are in terms of the relationship represented by the social network.

「How well can the geodesic distance measure similarity and closeness in such a network?」Suppose Ada and Bob are two customers in the network, and the network is undirected. The geodesic distance (i.e., the length of the shortest path between Ada and Bob) is the shortest path that a message can be passed from Ada to Bob and vice versa. However, this information is not useful for AllElectronics' customer relationship management because the company typically does not want to send a specific message from one customer to another. Therefore, geodesic distance does not suit the application.

「What does similarity mean in a social network?」We consider two ways to define similarity:■ Two customers are considered similar to one another if they have similar neighbors in the social network. This heuristic is intuitive because, in practice, two people receiving recommendations from a good number of common friends often make similar decisions. This kind of similarity is based on the local structure (i.e., the neighborhoods ) of the vertices, and thus is called structural context–based similarity.

■ Suppose AllElectronics sends promotional information to both Ada and Bob in the social network. Ada and Bob may randomly forward such information to their friends (or neighbors ) in the network. The closeness between Ada and Bob can then be measured by the likelihood that other customers simultaneously receive the promotional information that was originally sent to Ada and Bob. This kind of similarity is based on the random walk reachability over the network, and thus is referred to as similarity based on random walk.

Let's have a closer look at what is meant by similarity based on structural context, and similarity based on random walk.

The intuition behind similarity based on structural context is that two vertices in a graph are similar if they are connected to similar vertices. To measure such similarity, we need to define the notion of individual neighborhood. In a directed graph , where V is the set of vertices and is the set of edges, for a vertex , the individual in-neighborhood of v is defined as(11.29)

Symmetrically, we define the individual out-neighborhood of v as(11.30)

Following the intuition illustrated in Example 11.20, we define SimRank, a structural-context similarity, with a value that is between 0 and 1 for any pair of vertices. For any vertex, , the similarity between the vertex and itself is because the neighborhoods are identical. For vertices such that , we can define(11.31)

where C is a constant between 0 and 1. A vertex may not have any in-neighbors. Thus, we define Eq. (11.31) to be 0 when either I(u) or I(v) is ∅. Parameter C specifies the rate of decay as similarity is propagated across edges.

「How can we compute SimRank?」A straightforward method iteratively evaluates Eq. (11.31) until a fixed point is reached. Let be the SimRank score calculated at the i th round. To begin, we set(11.32)

We use Eq. (11.31) to compute from si as(11.33)

It can be shown that . Additional methods for approximating SimRank are given in the bibliographic notes (Section 11.7).

Now, let's consider similarity based on random walk. A directed graph is strongly connected if, for any two nodes u and v, there is a path from u to v and another path from v to u. In a strongly connected graph, , for any two vertices, , we can define the expected distance from u to v as(11.34)

where is a path starting from u and ending at v that may contain cycles but does not reach v until the end. For a traveling tour, , its length is . The probability of the tour is defined as(11.35)

To measure the probability that a vertex w receives a message that originated simultaneously from u and v, we extend the expected distance to the notion of expected meeting distance, that is,(11.36)

where is a pair of tours and of the same length. Using a constant C between 0 and 1, we define the expected meeting probability as(11.37)

which is a similarity measure based on random walk. Here, the parameter C specifies the probability of continuing the walk at each step of the trajectory.

It has been shown that for any two vertices, u and v. That is, SimRank is based on both structural context and random walk.

11.3.3. Graph Clustering Methods

Let's consider how to conduct clustering on a graph. We first describe the intuition behind graph clustering. We then discuss two general categories of graph clustering methods.

To find clusters in a graph, imagine cutting the graph into pieces, each piece being a cluster, such that the vertices within a cluster are well connected and the vertices in different clusters are connected in a much weaker way. Formally, for a graph, , a cut, , is a partitioning of the set of vertices V in G, that is, and . The cut set of a cut is the set of edges, . The size of the cut is the number of edges in the cut set. For weighted graphs, the size of a cut is the sum of the weights of the edges in the cut set.

「What kinds of cuts are good for deriving clusters in graphs?」In graph theory and some network applications, a minimum cut is of importance. A cut is minimum if the cut's size is not greater than any other cut's size. There are polynomial time algorithms to compute minimum cuts of graphs. Can we use these algorithms in graph clustering?

Cuts and clusters Consider graph G in Figure 11.14. The graph has two clusters: and , and one outlier vertex, l.

Consider cut . Only one edge, namely, (e, l), crosses the two partitions created by C1. Therefore, the cut set of C1 is and the size of C1 is 1. (Note that the size of any cut in a connected graph cannot be smaller than 1.) As a minimum cut, C1 does not lead to a good clustering because it only separates the outlier vertex, l, from the rest of the graph.

Figure 11.14

A graph G and two cuts.

Cut leads to a much better clustering than C1.

The edges in the cut set of C2 are those connecting the two「natural clusters」in the graph. Specifically, for edges (d, h) and (e, k) that are in the cut set, most of the edges connecting d, h, e, and k belong to one cluster.

Example 11.21 indicates that using a minimum cut is unlikely to lead to a good clustering. We are better off choosing a cut where, for each vertex u that is involved in an edge in the cut set, most of the edges connecting to u belong to one cluster. Formally, let be the degree of u, that is, the number of edges connecting to u. The sparsity of a cut is defined as(11.38)

A cut is sparsest if its sparsity is not greater than the sparsity of any other cut. There may be more than one sparsest cut.

In Example 11.21 and Figure 11.14, C2 is a sparsest cut. Using sparsity as the objective function, a sparsest cut tries to minimize the number of edges crossing the partitions and balance the partitions in size.

Consider a clustering on a graph that partitions the graph into k clusters. The modularity of a clustering assesses the quality of the clustering and is defined as(11.39)

where li is the number of edges between vertices in the i th cluster, and di is the sum of the degrees of the vertices in the i th cluster. The modularity of a clustering of a graph is the difference between the fraction of all edges that fall into individual clusters and the fraction that would do so if the graph vertices were randomly connected. The optimal clustering of graphs maximizes the modularity.

Theoretically, many graph clustering problems can be regarded as finding good cuts, such as the sparsest cuts, on the graph. In practice, however, a number of challenges exist:■ High computational cost: Many graph cut problems are computationally expensive. The sparsest cut problem, for example, is NP-hard. Therefore, finding the optimal solutions on large graphs is often impossible. A good trade-off between efficiency/scalability and quality has to be achieved.

■ Sophisticated graphs: Graphs can be more sophisticated than the ones described here, involving weights and/or cycles.

■ High dimensionality: A graph can have many vertices. In a similarity matrix, a vertex is represented as a vector (a row in the matrix) with a dimensionality that is the number of vertices in the graph. Therefore, graph clustering methods must handle high dimensionality.

■ Sparsity: A large graph is often sparse, meaning each vertex on average connects to only a small number of other vertices. A similarity matrix from a large sparse graph can also be sparse.

There are two kinds of methods for clustering graph data, which address these challenges. One uses clustering methods for high-dimensional data, while the other is designed specifically for clustering graphs.

The first group of methods is based on generic clustering methods for high-dimensional data. They extract a similarity matrix from a graph using a similarity measure such as those discussed in Section 11.3.2. A generic clustering method can then be applied on the similarity matrix to discover clusters. Clustering methods for high-dimensional data are typically employed. For example, in many scenarios, once a similarity matrix is obtained, spectral clustering methods (Section 11.2.4) can be applied. Spectral clustering can approximate optimal graph cut solutions. For additional information, please refer to the bibliographic notes (Section 11.7).

The second group of methods is specific to graphs. They search the graph to find well-connected components as clusters. Let's look at a method called SCAN (Structural Clustering Algorithm for Networks) as an example.

Given an undirected graph, , for a vertex, , the neighborhood of u is . Using the idea of structural-context similarity, SCAN measures the similarity between two vertices, , by the normalized common neighborhood size, that is,(11.40)

The larger the value computed, the more similar the two vertices. SCAN uses a similarity threshold ε to define the cluster membership. For a vertex, , the ε-neighborhood of u is defined as . The ε-neighborhood of u contains all neighbors of u with a structural-context similarity to u that is at least ε.

In SCAN, a core vertex is a vertex inside of a cluster. That is, is a core vertex if , where μ is a popularity threshold. SCAN grows clusters from core vertices. If a vertex v is in the ε-neighborhood of a core u, then v is assigned to the same cluster as u. This process of growing clusters continues until no cluster can be further grown. The process is similar to the density-based clustering method, DBSCAN (Chapter 10).

Formally, a vertex v can be directly reached from a core u if . Transitively, a vertex v can be reached from a core u if there exist vertices such that w1 can be reached from u, wi can be reached from for , and v can be reached from wn. Moreover, two vertices, , which may or may not be cores, are said to be connected if there exists a core w such that both u and v can be reached from w. All vertices in a cluster are connected. A cluster is a maximum set of vertices such that every pair in the set is connected.

Some vertices may not belong to any cluster. Such a vertex u is a hub if the neighborhood of u contains vertices from more than one cluster. If a vertex does not belong to any cluster, and is not a hub, it is an outlier.

The SCAN algorithm is shown in Figure 11.15. The search framework closely resembles the cluster-finding process in DBSCAN. SCAN finds a cut of the graph, where each cluster is a set of vertices that are connected based on the transitive similarity in a structural context.

Figure 11.15

SCAN algorithm for cluster analysis on graph data.

An advantage of SCAN is that its time complexity is linear with respect to the number of edges. In very large and sparse graphs, the number of edges is in the same scale of the number of vertices. Therefore, SCAN is expected to have good scalability on clustering large graphs.

11.4. Clustering with Constraints

Users often have background knowledge that they want to integrate into cluster analysis. There may also be application-specific requirements. Such information can be modeled as clustering constraints. We approach the topic of clustering with constraints in two steps. Section 11.4.1 categorizes the types of constraints for clustering graph data. Methods for clustering with constraints are introduced in Section 11.4.2.

11.4.1. Categorization of Constraints

This section studies how to categorize the constraints used in cluster analysis. Specifically, we can categorize constraints according to the subjects on which they are set, or on how strongly the constraints are to be enforced.

As discussed in Chapter 10, cluster analysis involves three essential aspects: objects as instances of clusters, clusters as groups of objects, and the similarity among objects. Therefore, the first method we discuss categorizes constraints according to what they are applied to. We thus have three types: constraints on instances, constraints on clusters, and constraints on similarity measurement.

Constraints on instances: A constraint on instances specifies how a pair or a set of instances should be grouped in the cluster analysis. Two common types of constraints from this category include:■ Must-link constraints. If a must-link constraint is specified on two objects x and y, then x and y should be grouped into one cluster in the output of the cluster analysis. These must-link constraints are transitive. That is, if and , then .

■ Cannot-link constraints. Cannot-link constraints are the opposite of must-link constraints. If a cannot-link constraint is specified on two objects, x and y, then in the output of the cluster analysis, x and y should belong to different clusters. Cannot-link constraints can be entailed. That is, if , , and , then .

A constraint on instances can be defined using specific instances. Alternatively, it can also be defined using instance variables or attributes of instances. For example, a constraint,

uses the distance between objects to specify a must-link constraint.

Constraints on clusters: A constraint on clusters specifies a requirement on the clusters, possibly using attributes of the clusters. For example, a constraint may specify the minimum number of objects in a cluster, the maximum diameter of a cluster, or the shape of a cluster (e.g., a convex). The number of clusters specified for partitioning clustering methods can be regarded as a constraint on clusters.

Constraints on similarity measurement: Often, a similarity measure, such as Euclidean distance, is used to measure the similarity between objects in a cluster analysis. In some applications, exceptions apply. A constraint on similarity measurement specifies a requirement that the similarity calculation must respect. For example, to cluster people as moving objects in a plaza, while Euclidean distance is used to give the walking distance between two points, a constraint on similarity measurement is that the trajectory implementing the shortest distance cannot cross a wall.

There can be more than one way to express a constraint, depending on the category.

For example, we can specify a constraint on clusters as

The requirement can also be expressed using a constraint on instances as(11.41)

Constraints on instances, clusters, and similarity measurement AllElectronics clusters its customers so that each group of customers can be assigned to a customer relationship manager. Suppose we want to specify that all customers at the same address are to be placed in the same group, which would allow more comprehensive service to families. This can be expressed using a must-link constraint on instances:

AllElectronics has eight customer relationship managers. To ensure that they each have a similar workload, we place a constraint on clusters such that there should be eight clusters, and each cluster should have at least 10% of the customers and no more than 15% of the customers. We can calculate the spatial distance between two customers using the driving distance between the two. However, if two customers live in different countries, we have to use the flight distance instead. This is a constraint on similarity measurement.

Another way to categorize clustering constraints considers how firmly the constraints have to be respected. A constraint is hard if a clustering that violates the constraint is unacceptable. A constraint is soft if a clustering that violates the constraint is not preferable but acceptable when no better solution can be found. Soft constraints are also called preferences.

Hard and soft constraints For AllElectronics, Constraintfamily in Example 11.22 is a hard constraint because splitting a family into different clusters could prevent the company from providing comprehensive services to the family, leading to poor customer satisfaction. The constraint on the number of clusters (which corresponds to the number of customer relationship managers in the company) is also hard. Example 11.22 also has a constraint to balance the size of clusters. While satisfying this constraint is strongly preferred, the company is flexible in that it is willing to assign a senior and more capable customer relationship manager to oversee a larger cluster. Therefore, the constraint is soft.

Ideally, for a specific data set and a set of constraints, all clusterings satisfy the constraints. However, it is possible that there may be no clustering of the data set that satisfies all the constraints. Trivially, if two constraints in the set conflict, then no clustering can satisfy them at the same time.

Conflicting constraints Consider these constraints:

If a data set has two objects, x, y, such that , then no clustering can satisfy both constraints simultaneously.

Consider these two constraints:

The second constraint is redundant given the first. Moreover, for a data set where the distance between any two objects is at least 5, every possible clustering of the objects satisfies the constraints.

「How can we measure the quality and the usefulness of a set of constraints?」In general, we consider either their informativeness, or their coherence. The informativeness is the amount of information carried by the constraints that is beyond the clustering model. Given a data set, D, a clustering method, , and a set of constraints, , the informativeness of with respect to on D can be measured by the fraction of constraints in that are unsatisfied by the clustering computed by on D. The higher the informativeness, the more specific the requirements and background knowledge that the constraints carry. The coherence of a set of constraints is the degree of agreement among the constraints themselves, which can be measured by the redundancy among the constraints.

11.4.2. Methods for Clustering with Constraints

Although we can categorize clustering constraints, applications may have very different constraints of specific forms. Consequently, various techniques are needed to handle specific constraints. In this section, we discuss the general principles of handling hard and soft constraints.

Handling Hard Constraints

A general strategy for handling hard constraints is to strictly respect the constraints in the cluster assignment process. To illustrate this idea, we will use partitioning clustering as an example.

Given a data set and a set of constraints on instances (i.e., must-link or cannot-link constraints), how can we extend the k-means method to satisfy such constraints? The COP-k-means algorithm works as follows:1. Generate superinstances for must-link constraints. Compute the transitive closure of the must-link constraints. Here, all must-link constraints are treated as an equivalence relation. The closure gives one or multiple subsets of objects where all objects in a subset must be assigned to one cluster. To represent such a subset, we replace all those objects in the subset by the mean. The superinstance also carries a weight, which is the number of objects it represents.

After this step, the must-link constraints are always satisfied.

2. Conduct modified k-means clustering. Recall that, in k-means, an object is assigned to the closest center. What if a nearest-center assignment violates a cannot-link constraint? To respect cannot-link constraints, we modify the center assignment process in k-means to a nearest feasible center assignment. That is, when the objects are assigned to centers in sequence, at each step we make sure the assignments so far do not violate any cannot-link constraints. An object is assigned to the nearest center so that the assignment respects all cannot-link constraints.

Because COP-k-means ensures that no constraints are violated at every step, it does not require any backtracking. It is a greedy algorithm for generating a clustering that satisfies all constraints, provided that no conflicts exist among the constraints.

Handling Soft Constraints

Clustering with soft constraints is an optimization problem. When a clustering violates a soft constraint, a penalty is imposed on the clustering. Therefore, the optimization goal of the clustering contains two parts: optimizing the clustering quality and minimizing the constraint violation penalty. The overall objective function is a combination of the clustering quality score and the penalty score.

To illustrate, we again use partitioning clustering as an example. Given a data set and a set of soft constraints on instances, the CVQE (Constrained Vector Quantization Error) algorithm conducts k-means clustering while enforcing constraint violation penalties. The objective function used in CVQE is the sum of the distance used in k-means, adjusted by the constraint violation penalties, which are calculated as follows.

■ Penalty of a must-link violation. If there is a must-link constraint on objects x and y, but they are assigned to two different centers, c1 and c2, respectively, then the constraint is violated. As a result, , the distance between c1 and c2, is added to the objective function as the penalty.

■ Penalty of a cannot-link violation. If there is a cannot-link constraint on objects x and y, but they are assigned to a common center, c, then the constraint is violated. The distance, , between c and c′ is added to the objective function as the penalty.

Speeding up Constrained Clustering

Constraints, such as on similarity measurements, can lead to heavy costs in clustering.

Consider the following clustering with obstacles problem: To cluster people as moving objects in a plaza, Euclidean distance is used to measure the walking distance between two points. However, a constraint on similarity measurement is that the trajectory implementing the shortest distance cannot cross a wall (Section 11.4.1). Because obstacles may occur between objects, the distance between two objects may have to be derived by geometric computations (e.g., involving triangulation). The computational cost is high if a large number of objects and obstacles are involved.

The clustering with obstacles problem can be represented using a graphical notation. First, a point, p, is visible from another point, q, in the region R if the straight line joining p and q does not intersect any obstacles. A visibility graph is the graph, , such that each vertex of the obstacles has a corresponding node in V and two nodes, v_1 and v_2, in V are joined by an edge in E if and only if the corresponding vertices they represent are visible to each other. Let be a visibility graph created from VG by adding two additional points, p and q, in V′. E′ contains an edge joining two points in V′ if the two points are mutually visible. The shortest path between two points, p and q, will be a subpath of , as shown in Figure 11.16(a). We see that it begins with an edge from p to either v_1, v_2, or v_3, goes through a path in VG, and then ends with an edge from either v_4 or v_5 to q.

Figure 11.16

Clustering with obstacle objects (o1 and o2): (a) a visibility graph and (b) triangulation of regions with microclusters.

Source: Adapted from Tung, Hou, and Han [THH01].

To reduce the cost of distance computation between any two pairs of objects or points, several preprocessing and optimization techniques can be used. One method groups points that are close together into microclusters. This can be done by first triangulating the region R into triangles, and then grouping nearby points in the same triangle into microclusters, using a method similar to BIRCH or DBSCAN, as shown in Figure 11.16(b). By processing microclusters rather than individual points, the overall computation is reduced. After that, precomputation can be performed to build two kinds of join indices based on the computation of the shortest paths: (1) VV indices, for any pair of obstacle vertices, and (2) MV indices, for any pair of microcluster and obstacle vertex. Use of the indices helps further optimize the overall performance.

Using such precomputation and optimization strategies, the distance between any two points (at the granularity level of a microcluster) can be computed efficiently. Thus, the clustering process can be performed in a manner similar to a typical efficient k-medoids algorithm, such as CLARANS, and achieve good clustering quality for large data sets.

Summary

■ In conventional cluster analysis, an object is assigned to one cluster exclusively. However, in some applications, there is a need to assign an object to one or more clusters in a fuzzy or probabilistic way. Fuzzy clustering and probabilistic model-based clustering allow an object to belong to one or more clusters. A partition matrix records the membership degree of objects belonging to clusters.

■ Probabilistic model-based clustering assumes that a cluster is a parameterized distribution. Using the data to be clustered as the observed samples, we can estimate the parameters of the clusters.

■ A mixture model assumes that a set of observed objects is a mixture of instances from multiple probabilistic clusters. Conceptually, each observed object is generated independently by first choosing a probabilistic cluster according to the probabilities of the clusters, and then choosing a sample according to the probability density function of the chosen cluster.

■ An expectation-maximization algorithm is a framework for approaching maximum likelihood or maximum a posteriori estimates of parameters in statistical models. Expectation-maximization algorithms can be used to compute fuzzy clustering and probabilistic model-based clustering.

■ High-dimensional data pose several challenges for cluster analysis, including how to model high-dimensional clusters and how to search for such clusters.

■ There are two major categories of clustering methods for high-dimensional data: subspace clustering methods and dimensionality reduction methods. Subspace clustering methods search for clusters in subspaces of the original space. Examples include subspace search methods, correlation-based clustering methods, and biclustering methods. Dimensionality reduction methods create a new space of lower dimensionality and search for clusters there.

■ Biclustering methods cluster objects and attributes simultaneously. Types of biclusters include biclusters with constant values, constant values on rows/columns, coherent values, and coherent evolutions on rows/columns. Two major types of biclustering methods are optimization-based methods and enumeration methods.

■ Spectral clustering is a dimensionality reduction method. The general idea is to construct new dimensions using an affinity matrix.

■ Clustering graph and network data has many applications such as social network analysis. Challenges include how to measure the similarity between objects in a graph, and how to design clustering models and methods for graph and network data.

■ Geodesic distance is the number of edges between two vertices on a graph. It can be used to measure similarity. Alternatively, similarity in graphs, such as social networks, can be measured using structural context and random walk. SimRank is a similarity measure that is based on both structural context and random walk.

■ Graph clustering can be modeled as computing graph cuts. A sparsest cut may lead to a good clustering, while modularity can be used to measure the clustering quality.

■ SCAN is a graph clustering algorithm that searches graphs to identify well-connected components as clusters.

■ Constraints can be used to express application-specific requirements or background knowledge for cluster analysis. Constraints for clustering can be categorized as constraints on instances, on clusters, or on similarity measurement. Constraints on instances includemust-linkandcannot-linkconstraints. A constraint can be hard or soft.

■ Hard constraints for clustering can be enforced by strictly respecting the constraints in the cluster assignment process. Clustering with soft constraints can be considered an optimization problem. Heuristics can be used to speed up constrained clustering.

11.6. Exercises

11.1 Traditional clustering methods are rigid in that they require each object to belong exclusively to only one cluster. Explain why this is a special case of fuzzy clustering. You may use k-means as an example.

11.2 AllElectronics carries 1000 products, P1, …, P1000. Consider customers Ada, Bob, and Cathy such that Ada and Bob purchase three products in common, , and P3. For the other 997 products, Ada and Bob independently purchase seven of them randomly. Cathy purchases 10 products, randomly selected from the 1000 products. In Euclidean distance, what is the probability that ? What if Jaccard similarity (Chapter 2) is used? What can you learn from this example?

11.3 Show that I × J is a bicluster with coherent values if and only if, for any and , .

11.4 Compare the MaPle algorithm (Section 11.2.3) with the frequent closed itemset mining algorithm, CLOSET (Pei, Han, and Mao [PHM00]). What are the major similarities and differences?

11.5 SimRank is a similarity measure for clustering graph and network data.

(a) Prove for SimRank computation.

(b) Show for SimRank.

11.6 In a large sparse graph where on average each node has a low degree, is the similarity matrix using SimRank still sparse? If so, in what sense? If not, why? Deliberate on your answer.

11.7 Compare the SCAN algorithm (Section 11.3.3) with DBSCAN (Section 10.4.1). What are their similarities and differences?

11.8 Consider partitioning clustering and the following constraint on clusters: The number of objects in each cluster must be between and , where n is the total number of objects in the data set, k is the number of clusters desired, and δ in [0, 1) is a parameter. Can you extend the k-means method to handle this constraint? Discuss situations where the constraint is hard and soft.

11.7. Bibliographic Notes

Höppner Klawonn, Kruse, and Runkler [HKKR99] provide a thorough discussion of fuzzy clustering. The fuzzy c-means algorithm (on which Example 11.7 is based) was proposed by Bezdek [Bez81]. Fraley and Raftery [FR02] give a comprehensive overview of model-based cluster analysis and probabilistic models. McLachlan and Basford [MB88] present a systematic introduction to mixture models and applications in cluster analysis.

Dempster, Laird, and Rubin [DLR77] are recognized as the first to introduce the EM algorithm and give it its name. However, the idea of the EM algorithm had been「proposed many times in special circumstances」before, as admitted in Dempster, Laird, and Rubin [DLR77]. Wu [Wu83] gives the correct analysis of the EM algorithm.

Mixture models and EM algorithms are used extensively in many data mining applications. Introductions to model-based clustering, mixture models, and EM algorithms can be found in recent textbooks on machine learning and statistical learning—for example, Bishop [Bis06], Marsland [Mar09] and Alpaydin [Alp11].

The increase of dimensionality has severe effects on distance functions, as indicated by Beyer et al. [BGRS99]. It also has had a dramatic impact on various techniques for classification, clustering, and semisupervised learning (Radovanović, Nanopoulos, and Ivanović[RNI09]).

Kriegel, Kröger, and Zimek [KKZ09] present a comprehensive survey on methods for clustering high-dimensional data. The CLIQUE algorithm was developed by Agrawal, Gehrke, Gunopulos, and Raghavan [AGGR98]. The PROCLUS algorithm was proposed by Aggawal, Procopiuc, Wolf, et al. [APW+99].

The technique of biclustering was initially proposed by Hartigan [Har72]. The term biclustering was coined by Mirkin [Mir98]. Cheng and Church [CC00] introduced biclustering into gene expression data analysis. There are many studies on biclustering models and methods. The notion of δ-pCluster was introduced by Wang, Wang, Yang, and Yu [WWYY02]. For informative surveys, see Madeira and Oliveira [MO04] and Tanay, Sharan, and Shamir [TSS04]. In this chapter, we introduced the δ-cluster algorithm by Cheng and Church [CC00] and MaPle by Pei, Zhang, Cho, et al. [PZC+03] as examples of optimization-based methods and enumeration methods for biclustering, respectively.

Donath and Hoffman [DH73] and Fiedler [Fie73] pioneered spectral clustering. In this chapter, we use an algorithm proposed by Ng, Jordan, and Weiss [NJW01] as an example. For a thorough tutorial on spectral clustering, see Luxburg [Lux07].

Clustering graph and network data is an important and fast-growing topic. Schaeffer [Sch07] provides a survey. The SimRank measure of similarity was developed by Jeh and Widom [JW02a]. Xu et al. [XYFS07] proposed the SCAN algorithm. Arora, Rao, and Vazirani [ARV09] discuss the sparsest cuts and approximation algorithms.

Clustering with constraints has been extensively studied. Davidson, Wagstaff, and Basu [DWB06] proposed the measures of informativeness and coherence. The COP-k-means algorithm is given by Wagstaff et al. [WCRS01]. The CVQE algorithm was proposed by Davidson and Ravi [DR05]. Tung, Han, Lakshmanan, and Ng [THLN01] presented a framework for constraint-based clustering based on user-specified constraints. An efficient method for constraint-based spatial clustering in the existence of physical obstacle constraints was proposed by Tung, Hou, and Han [THH01].

