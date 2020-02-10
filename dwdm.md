### To implement data preprocessing to perform the following operations on a raw dataset -

- Data cleaning: missing data, noisy data
- Redundancy and correlation analysis
- Tuple duplication
- Data value conflict detection and resolution
- Data reduction - attribute subset selection
- Histograms
- Sampling
- Data transformation and data discretization

What is the significance of correlation matrix?

Why normalization?


#### Mini Project

Identify tools for data preprocessing

How to apply these tools


# DWDM

## Unit 3

### What is data mining?

❯ Data Mining is Non-trivial extraction of implicit, previously unknown and potentially useful information from data.

❯ Data Mining is Exploration & analysis, by automatic or semi-automatic means, of large quantities of data in order to discover meaningful patterns.

Input Data -> Data Preprocessing -> Data Mining -> Data Postprocessing -> Information


### Methods

❯ Predictive Methods
  - Use some variables to predict unknown or future values of other variables.

❯ Descriptive Methods
  - Find human-interpretable patterns that describe the data.


#### Supervised Learning

❯ Prediction methods are commonly referred to as supervised learning.

❯ Supervised methods are thought to attempt the discovery of the relationships between input attributes and a target attribute.

❯ A training set is given and the objective is to form a description that can be used to predict unseen examples.

❯ Problems:

■ Classification
  - The domain of the target attribute is finite and categorical.
  - A classifier must assign a class to a unseen example.

■ Regression
  - The target attribute is formed by infinite values.
  - To fit a model to learn the output target attribute as a function of input attributes.

■ Time Series Analysis
  - Making predictions in time.

#### Unsupervised Learning

❯ There is no supervisor and only input data is available.

❯ The aim is to find regularities, irregularities, relationships, similarities and associations in the input.

❯ Problems:
■ Clustering

■ Association Rules

■ Pattern Mining
- It is adopted as a more general term than frequent pattern mining or association mining

■ Outlier Detection
- It is the process of finding data examples with behaviours that are very different from the expectation (outliers or anomalies)

#### Semi Supervised Learning

❯ Semi-supervised learning is a class of machine learning tasks and techniques that also make use of unlabeled data for training – typically a small amount of labeled data with a large amount of unlabeled data

❯ Semi-supervised learning falls between unsupervised learning (without any labeled training data) and supervised learning (with completely labeled training data).

#### Supervised vs Unsupervised

- Supervised learning (classification)
❯ Supervision: The training data (observations, measurements, etc.) are accompanied by labels indicating the class of the observations
❯ New data is classified based on the training set
- Unsupervised learning (clustering)
❯ The class labels of training data is unknown
❯ Given a set of measurements, observations, etc. have the aim of establishing the existence of classes or clusters in the data

### Market Basket Analysis

❯ Market Basket Analysis (Association Analysis) is a mathematical modeling technique based upon the theory that if you buy a certain group of items, you are likely to buy another group of items.

❯ It is used to analyze the customer purchasing behavior and helps in increasing the sales and maintain inventory by focusing on the point of sale transaction data.

❯ Given a dataset, the Apriori Algorithm trains and identifies product baskets and product association rules.

#### Why Association Rule Analysis is important?

- Discloses an intrinsic and important property of data sets
- Forms the foundation for many essential data mining tasks
❯ Association, correlation, and causality analysis
❯ Sequential, structural (e.g., sub-graph) patterns
❯ Pattern analysis in spatiotemporal, multimedia, timeseries, and stream data
❯ Classification: associative classification
❯ Cluster analysis: frequent pattern-based clustering
❯ Data warehousing: iceberg cube and cube-gradient
❯ Semantic data compression: fascicles
❯ Broad applications


### Introduction - Frequent Patterns

- Frequent pattern: a pattern (a set of items, subsequences, substructures, etc.) that occurs frequently in a data set
- First proposed by Agrawal, Imielinski, and Swami [AIS93] in the context of frequent item sets and association rule mining
- Motivation: Finding inherent regularities in data
❯ What products were often purchased together?— Pen and Pencil?!
❯ What are the subsequent purchases after buying a PC?
❯ What kinds of DNA are sensitive to this new drug?
- Applications
❯ Basket data analysis, cross-marketing, catalog design, sale campaign analysis, Web log (click stream) analysis, and DNA sequence analysis

### Introduction - Assocation Rule Mining

❯ Given a set of transactions, find rules that will predict the occurrence of an item based on the occurrences of other items in the transaction

|---|---|
|ID|Items|
|100|Bread, Milk|
|200|Bread, Diaper, Beer, Eggs|
|300|Milk, Diaper, Beer, Coke|
|400|Bread, Milk, Diaper, Beer|
|500|Bread, Milk, Diaper, Coke|

- Example of Association Rules
❯ {Diaper} → {Beer},
❯ {Milk, Bread} → {Eggs,Coke},
❯ {Beer, Bread} → {Milk},
Implication means co-occurrence, not causality


#### Definitions and Terminologies

❯ Transaction → A set of items (Itemset).
❯ Confidence → The measure of uncertainty or trust worthiness associated with each discovered pattern.
❯ Support → The measure of how often the collection of items in an association occur together as percentage of all transactions
❯ Frequent Itemset → If an itemset satisfies minimum support, then it is a frequent itemset.
❯ Strong Association Rules → Rules that satisfy both a minimum support threshold and a minimum confidence threshold
❯ In Association Rule Mining, we first find all frequent itemsets and then generate strong association rules from the frequent itemsets

#### Definition with example

❯ Itemset → A collection of one or more items
❯ Example → {Milk, Bread, Diaper}
❯ k-itemset → An itemset that contains k items
❯ Support count (σ)
❯ Frequency of occurrence of an itemset
  E.g. σ({Milk, Bread,Diaper}) = 2
❯ Support: Fraction of transactions that contain an itemset
  E.g. s({Milk, Bread, Diaper}) = 2/5
❯ Frequent Itemset: An itemset whose support is greater than or equal to a minimum support threshold

#### Definition - Association Rule

❯ Association Rule: An implication expression of the form X → Y, where X and Y are itemsets
❯ Example: {Milk, Diaper} → {Beer}
❯ Rule Evaluation Metrics
- Support (s) = union(X, Y).count / n
Fraction of transactions that contain both X and Y
❯ Confidence (c) = union(X, Y).count / X.count
- Measures how often items in Y appear in transactions that contain X

#### Association Rule Mining Task

❯ Given a set of transactions T, the goal of association rule mining is to find all rules having
- support ≥ minsup threshold
- confidence ≥ minconf threshold
❯ Brute-force approach
- List all possible association rules
- Compute the support and confidence for each rule
- Prune rules that fail the minsup and minconf thresholds

Revisited Terms
❯ Support: The rule holds with support sup in T (the transaction data set) if sup% of transactions contain X U Y.
- sup = Pr(X U Y).
❯ Confidence: The rule holds in T with confidence conf if conf % of tranactions that contain X also contain Y.
- conf = Pr(Y | X)
❯ An association rule is a pattern that states when X occurs, Y occurs with certain probability.

#### Mining Assocation Rules

❯ Two-step approach →
❯ Frequent Itemset Generation
- Generate all itemsets whose support ≥ minsup
❯ Rule Generation
- Generate high confidence rules from each frequent itemset, where each rule is a binary partitioning of a frequent itemset
❯ Frequent itemset generation is computationally expensive

#### Frequent Itemset Generation

- Brute-force approach:
❯ Each itemset in the lattice is a candidate frequent itemset
❯ Count the support of each candidate by scanning the database
- Match each transaction against every candidate
❯ Expensive

##### Frequent Itemset Generation Strategies

To Reduce the number of candidates (M)
Complete search: M=2<sup>d</sup>
- Use pruning techniques

#### Reducing Number of Candidates

Apriori principle:
❯ An itemset is frequent, then all of its subsets must also be frequent
❯ Apriori principle holds due to the following property of the support measure:
❯ Support of an itemset never exceeds the support of its subsets
❯ This is known as the anti-monotone property of support

### Advantages Disadvantages of FP Growth

- Advantages Of FP Growth Algorithm
❯ This algorithm needs to scan the database only twice when compared to Apriori which scans the transactions for each iteration.
❯ The pairing of items is not done in this algorithm and this makes it faster.
❯ The database is stored in a compact version in memory.
❯ It is efficient and scalable for mining both long and short frequent patterns.
- Disadvantages Of FP-Growth Algorithm
❯ FP Tree is more cumbersome and difficult to build than Apriori.
❯ It may be expensive.
❯ When the database is large, the algorithm may not fit in the shared memory

|---|---|
|FP Growth|Apriori|
|Generates pattern by constructing FP tree|Generates pattern by pairing items in singleton/pairs/triplets|
|No candidate generation|This uses candidate generation|
|Faster process, runtime increases linearly with increase in itemsets|Comparitively slower, runtime increases exponentially|
|Compact version of database is saved|Candidate combinations are saved in memory|


### Visual Data Mining

- Visualization:
❯ Use of computer graphics to create visual images which aid in the understanding of complex, often massive representations of data
- Visual Data Mining:
❯ The process of discovering implicit but useful knowledge from large data sets using visualization techniques

### Purpose of Visualization

❯ Gain insight into an information space by mapping data onto graphical primitives
❯ Provide qualitative overview of large data sets
❯ Search for patterns, trends, structure, irregularities, relationships among data
❯ Help find interesting regions and suitable parameters for further quantitative analysis
❯ Provide a visual proof of computer representations derived

❯ Integration of visualization and data mining
- Data visualization
- Data mining result visualization
- Data mining process visualization
- Interactive visual data mining
❯ Data visualization
- Data in a database or data warehouse can be viewed
- At different levels of abstraction
- As different combinations of attributes or dimensions
❯ Data can be presented in various visual forms

### Classification of Visualization techniques

❯ Geometric Techniques:
- Scatterplots, Landscapes, Projection Pursuit, Prosection Views, Hyperslice, Parallel Coordinates...
❯ Icon-based Techniques:
- Chernoff Faces, Stick Figures, Shape-Coding, Color Icons, TileBars,...
❯ Pixel-oriented Techniques:
- Recursive Pattern Technique, Circle Segments Technique, Spiral- & AxesTechniques,...
❯ Hierarchical Techniques:
- Dimensional Stacking, Worlds-within-Worlds,Treemap, Cone Trees, InfoCube,...
❯ Graph-Based Techniques:
- Basic Graphs (Straight-Line, Polyline, Curved-Line,...)
- Specific Graphs (e.g., DAG, Symmetric, Cluster,...)
- Systems (e.g., Tom Sawyer, Hy+, SeeNet, Narcissus,...)
❯ Hybrid Techniques: arbitrary combinations from above

### Data Visualization Techniques

❯ Scatterplot Matrices, Landscapes
❯ Icon-based, Treemaps

#### Scatterplot Matrices

❯ A scatterplot matrix shows a grid of scatterplots where each attribute is plotted against all other attributes
❯ It can be read by column or row, and each plot appears twice, allowing you to consider the spatial relationships from two perspectives.

#### Box and Whisker Plots

❯ It summarize the distribution of a given attribute by showing a box for the 25th and 75th percentile
❯ A line in the box for the 50th percentile (median) and a dot for the mean.
❯ The whiskers show 1.5*the height of the box (called the Inter Quartile Range) which indicate the expected range of the data and any data beyond those whiskers is assumed to be an outlier and marked with a dot.

#### Landscapes

❯ Visualization of the data as perspective landscape
❯ The data needs to be transformed into a (possibly artificial) 2D spatial representation which preserves the characteristics of the data

#### Tree Maps to visualize complex hierarchies

❯ Tree maps are visualizations for hierarchical data.
❯ They are made of a series of nested rectangles of sizes proportional to the corresponding data value.
❯ A large rectangle represents a branch of a data tree, and it is subdivided into smaller rectangles that represent the size of each node within that branch.

#### Data Mining Result Visualization

- Presentation of the results or knowledge obtained from data mining in visual forms
- Examples
❯ Scatter plots and boxplots (obtained from descriptive data mining)
❯ Decision trees
❯ Association rules
❯ Clusters
❯ Outliers
❯ Generalized rules
❯ Text mining

#### Text Mining

❯ According to Oracle, 90% of the world's data is in an unstructured format
❯ Just 10% is properly structured
❯ Makes it easier to analyze documents, query data, etc.
❯ Can discover new/important information from huge chunks of text
❯ Lots of new information is available on the internet, increasing second by second
❯ Users want instant access to new/useful information
❯ Some issues - language barriers, etc
❯ Searching and extracting information from the internet can be done by applying Natural Language Processing
❯ NLP can be used for preprocessing of data
❯ Normal data mining can be used when have structured data
❯ Text Mining = <i>Statistical NLP</i> (structured data) + <i>Data Mining</i> (pattern discovery)

Steps involved

❯ Preprocessing
- Syntactic/semantic analysis
❯ Transformation
❯ Feature Selection
- Counting, statistics
❯ Data Mining
- Classification (supervised), clustering (unsupervised)
❯ Evaluation
❯ Application

❯ NLP has difficulties - document may not provide context
❯ Humans need context to interpret anything correctly

- Supervised learning (classification)
❯ The training data is labeled indicating the class
❯ New data is classified based on the training set
❯ Correct classification: The known label of test sample is identical with the class result from the classification model
- Unsupervised learning (clustering)
❯ The class labels of training data are unknown
❯ Establish the existence of classes or clusters in the data
❯ Good clustering method: high intra-cluster similarity and low intercluster similarity


|---|---|
|Data Mining|Text Mining|
|Process directly|Linguistic/Natural Language Processing|
|Identify casual relationship|Discover heretofore unknown information|
|Structured data|Semi-structured and unstructured textual data|
|Structured numeric transaction data residing in data warehouse|Application deal with diverse and eclectic collections of systems and formats|

#### Challenges in Text Mining

❯ Information is in unstructured textual form
❯ Not readily accessible to be used by computers
❯ Dealing with huge collections of documents


### Web Mining

❯ Getting information from various sources on the internet
❯ Virtually unlimited data with a lot of duplication
❯ Huge, easily accessible, wide and diverse coverage, all types of information, semi structured (HTML), linked (documents hyperlink to each other), lots of redundant information
❯ Pages can be noisy - advertisments, copyright notices, navigation controls etc., besides the main content.
❯ Service providers - need user information
❯ Dynamic pages - lots of information keeps changing, not everything is a static page
❯ The web is basically a virtual society
❯ Web content mining
- Mining content from the web - i.e. extracting useful information from various webpages
❯ Web structure mining
- Hyperlink level, getting structure of website
- Categorizing webpages
- Information about the page, check hyperlinks to see what the author endorses
- Schema discovery in semi-structured environment
❯ Web usage mining - Statistics about users and how they use the web
- Discovering the users usage patterns
- Prediction of their behaviour on different webpages


## Unit 4

### Classification vs Prediction

- Classification
❯ Predicts categorical class labels (discrete or nominal)
❯ Classifies data (constructs a model) based on the training set and the values (class labels) in a classifying attribute and uses it in classifying new data
- Prediction
❯ Models continuous-valued functions, i.e. predicts unknown or missing values
- Typical applications
❯ Credit approval
❯ Target marketing
❯ Medical diagnosis
❯ Fraud detection

#### Classification Process

- Model construction: describing a set of predetermined classes
❯ Each tuple/sample is assumed to belong to a predefined class, as determined by the class label attribute
❯ The set of tuples used for model construction is training set
❯ The model is represented as classification rules, decision trees, or mathematical formulae
- Model usage: for classifying future or unknown objects
❯ Estimate accuracy of the model
  • The known label of test sample is compared with the classified result from the model
  • Accuracy rate is the percentage of test set samples that are correctly classified by the model
  • Test set is independent of training set, otherwise over-fitting will occur
❯ If the accuracy is acceptable, use the model to classify data tuples whose class labels are not known

#### Bayesian Classification

❯ Statistical classfier - probabistic predictions - predicts class member probabilities
❯ Based on Bayes' theorem
❯ Has comparable performance with decision tree and selected neural network classifiers
❯ Each training example can increment/decrement the probability that a hypothesis is correct - prior knowledge can be combined with observed data
❯ Even when the methods are computationally intractable, they can provide a standard of optimal decision making against which other methods can be measured

#### Naive Bayes Classification

- Advantages
❯ Easy to implement
❯ Good results obtained in most cases
- Disadvantages
❯ Assumption - class conditional independence, therefore loss of accuracy


### Decision Tree Classification

❯ Decision tree may be n-ary, n ≥ 2.
❯ There is a special node called root node.
❯ Internal nodes are test attribute/decision attribute.
❯ Leaf nodes are class labels.
❯ Edges of a node represent the outcome for a value of the test node.
❯ In a path, a node with same label is never repeated.
❯ Decision tree is not unique, as different ordering of internal nodes can give different decision tree.

#### Decision Tree Algorithm

- Basic algorithm (a greedy algorithm)
❯ Tree is constructed in a top-down recursive divide-and-conquer manner
❯ At start, all the training examples are at the root
❯ Attributes are categorical (if continuous-valued, they are discretized in advance)
❯ Examples are partitioned recursively based on selected attributes
❯ Test attributes are selected on the basis of a heuristic or statistical measure (e.g., information gain)
- Conditions for stopping partitioning
❯ All samples for a given node belong to the same class
❯ There are no remaining attributes for further partitioning – majority voting is employed for classifying the leaf
❯ There are no samples left

### Summary - Classification Algorithm

- Classification is a form of data analysis that extracts models describing important data classes
- Effective and scalable methods have been developed for
❯ Decision Tree Induction
❯ Naive Bayesian classification
❯ Rule based classification
❯ and many other classification models


### Clustering

❯ Organizing data into classes such that there is
- high intra-class similarity
- low inter-class similarity
❯ Finding the class labels and the number of classes directly from the data (in contrast to classification).
❯ More informally, finding natural groupings among objects.
❯ Also called unsupervised learning, sometimes called classification by statisticians and sorting by psychologists and segmentation by people in marketing

❯ Finding groups of objects such that the objects in a group will be similar (or related) to one another and different from (or unrelated to) the objects in other groups
❯ Intra-cluster - minimum distance
❯ Inter-cluster - maximum distance

#### Types of clustering

❯ Hierarchical clustering (BIRCH)
- A set of nested clusters organized as a hierarchical tree
❯ Partitional Clustering (k-means,k-mediods)
- A division data objects into non-overlapping (distinct) subsets (i.e., clusters) such that each data object is in exactly one subset
❯ Density based (DBSCAN)
- Based on density functions
❯ Grid based (STING)
- Based on nultiple-level granularity structure
❯ Model based (SOM)
- Hypothesize a model for each of the clusters and find the best fit of the data to the given model


#### 2 Types

❯ Partitional algorithms - Construct various partitions and then evaluate them by some criterion (we will see an example called BIRCH)
❯ Hierarchical algorithms - Create a hierarchical decomposition of the set of objects using some criterion

#### Clustering algorithms

- Partitional
❯ K-means
❯ K-mediods
- Hierarchial
❯ Agglomerative
❯ Divisive

Since we cannot test all possible trees we will have to heuristic search of all possible trees. We could do this -
❯ Bottom-Up (agglomerative)
- Starting with each item in its own cluster, find the best pair to merge into a new cluster. Repeat until all clusters are fused together.
❯ Top-Down (divisive)
- Starting with all the data in a single cluster, consider every possible way to divide the cluster into two. Choose the best division and recursively operate on both sides.

❯ We begin with a distance matrix
❯ Agglomerative
- Starting with each item in its own cluster, find the best pair to merge into a new cluster, repeat until all are fused

#### Desirable Properties of Clustering

❯ Scalability (in terms of both time and space)
❯ Ability to deal with different data types
❯ Minimal requirements for domain knowledge to determine input parameters
❯ Able to deal with noise and outliers
❯ Insensitive to order of input records
❯ Incorporation of user-specified constraints
❯ Interpretability and usability


### K-Means Clustering

❯ The k-means algorithm is an algorithm to cluster n objects based on attributes into k partitions, where k < n.
❯ It assumes that the object attributes form a vector space.
❯ An algorithm for partitioning (or clustering) N data points into K disjoint subsets S<sub>j</sub> containing data points so as to minimize the sum-of-squares criterion
❯ Simply speaking k-means clustering is an algorithm to classify or to group the objects based on attributes/features into K number of group.
❯ K is positive integer number.
❯ The grouping is done by minimizing the sum of squares of distances between data and the corresponding cluster centroid.

#### Working

Number of clusters K → Centroid → Distance of objects to centroid → Grouping based on minimum distance → no object move group (if false then back to centroid) → End

#### Classical Partitioning Method- K mean
❯ First, it randomly selects K of the objects, each of which initially means represents cluster mean or center.
❯ For each of the remaining objects, an object is assigned to the cluster to which it is most similar, based on the distance between the object and the cluster mean.
❯ It then computes the new mean for each cluster.
❯ This process iterates until the criterion function converges.
❯ Basically, for each object in each cluster, the distance from the objects to its cluster center is squared, and the distances are summed.
❯ This criterion tries to make the resulting k clusters as compact and separate as possible.

#### Working of K-Means clustering

Begin with a decision on the value of k = number of clusters
❯ Arbitrarily assign k objects from D as the initial cluster centers
❯ Each object is distributed to a cluster based on the cluster center to which it is the nearest.
❯ Next, the cluster centers are updated i.e. mean value of each cluster is recalculated based on the current objects in the cluster
❯ Using the new cluster centers, the objects are redistributed to the clusters based on which cluster center is the nearest.
❯ This process iterates
❯ Eventually, no redistribution of the objects in any occurs, and so the process terminates
❯ Resulting clusters are returned by the clustering process.

#### Applications of K-Means clustering

❯ It is relatively efficient and fast. It computes result at O(tkn), where n is number of objects or points, k is number of clusters and t is number of iterations.
❯ K-means clustering can be applied to machine learning or data mining
❯ Used on acoustic data in speech understanding to convert waveforms into one of k categories (known as Vector Quantization or Image Segmentation).
❯ Also used for choosing color palettes on old fashioned graphical display devices and Image Quantization.

#### Weaknessses

❯ When the data is less, initial grouping will determine the cluster significantly.
❯ The number of clusters, K, must be determined before hand.
Its disadvantage is that it does not yield the same result with each run, since the resulting clusters depend on the initial random assignments.
❯ We never know the real cluster, using the same data, because if it is inputted in a different order it may produce a different cluster if the data is less.
❯ It is sensitive to initial condition. Different initial condition may produce different result of cluster. The algorithm may be trapped in the local optimum.

#### Advantages and Disadvantages

##### Advantages

❯ K-means is relatively scalable and efficient in processing large data sets
❯ The computational complexity of the algorithm is O(nkt)
❯ n: the total number of objects
❯ k: the number of clusters
❯ t: the number of iterations
❯ Normally: k<<n and t<<n

##### Disadvantages

❯ Can be applied only when the mean of a cluster is defined
❯ Users need to specify K
❯ K-means is not suitable for discovering clusters with non convex shapes or clusters of varying sizes
❯ It is sensitive to noise and outlier data points

### K-Medoids

❯ The iterative process of replacing representative objects by no representative objects continues as long as the quality of the clustering is improved 
❯ For each representative Object O
- For each non-representative object R, swap O and R
❯ Choose the configuration with the lowest cost
❯ Cost function is the difference in absolute error-value if a current representative object is replaced by a non-representative object

#### Method

❯ Minimize the sensitivity of k-means to outliers
❯ Pick actual objects to represent clusters instead of mean values
❯ Each remaining object is clustered with the representative object (Medoid) to which is the most similar
❯ The algorithm minimizes the sum of the dissimilarities between each object and its corresponding reference point


#### Input
❯ K: the number of clusters
❯ D: a data set containing n objects
❯ Output: A set of k clusters
❯ Method:
1. Arbitrary choose k objects from D as representative objects (seeds)
2. Repeat (3) Assign each remaining object to the cluster with the nearest representative object
3. For each representative object Oj
4. Randomly select a non representative object Orandom
5. Compute the total cost S of swapping representative object Oj with Orandom (7) if S<0 then replace Oj with Orandom (8) Until no change 


K-Medoids Properties(k-medoids vs.Kmeans)
❯ The complexity of each iteration is O(k(n-k)2)
❯ For large values of n and k, such computation
becomes very costly
❯ Advantages
- K-Medoids method is more robust than k-Means in the presence of noise and outliers
❯ Disadvantages
- K-Medoids is more costly that the k-Means method
- Like k-means, k-medoids requires the user to specify k
- It does not scale well for large data sets

### Conclusion of Clustering
- K-means algorithm is useful for undirected knowledge discovery and is relatively simple.
- K-means has found wide spread usage in lot of fields, ranging from
❯ Unsupervised learning of neural network
❯ Pattern recognitions
❯ Classification analysis
❯ Artificial intelligence
❯ Image processing
❯ Machine vision
❯ and many others.


### Confusion Matrix

❯ Given m classes, an entry, CMi,j in a confusion matrix indicates # of tuples in class i that were labeled by the classifier as class j
❯ May have extra rows/columns to provide totals

#### Classifier Evaluation Metrics: Accuracy, Error Rate, Sensitivity and Specificity
- Classifier Accuracy, or recognition rate: percentage of test set tuples that are correctly classified
❯ Accuracy = (TP + TN)/All
- Error rate: 1 – accuracy, or
❯ Error rate = (FP + FN)/All
- Class Imbalance Problem:
❯ One class may be rare, e.g. fraud, or HIV-positive
❯ Significant majority of the negative class and minority of the positive class
❯ Sensitivity: True Positive recognition rate
  • Sensitivity = TP/P
❯ Specificity: True Negative recognition rate
  • Specificity = TN/N

#### Classifier Evaluation Metrics: Precision and Recall, and F-measures
❯ Precision: exactness – what % of tuples that the classifier labeled as positive are actually positive
❯ Recall: completeness – what % of positive tuples did the classifier label as positive?
❯ Perfect score is 1.0
❯ Inverse relationship between precision & recall
❯ F measure (F1 or F-score): harmonic mean of precision and recall,
❯ Fß: weighted measure of precision and recall
- assigns ß times as much weight to recall as to precision

### What is clustering

Clustering is the classification of objects into different groups, or more precisely, the partitioning of a data set into subsets (clusters), so that the data
in each subset (ideally) share some common trait often according to some defined distance measure

#### Types of Clustering
1. Hierarchical algorithms: these find successive clusters using previously established clusters.
❯ Agglomerative ("bottom-up"): Agglomerative algorithms begin with each element as a separate cluster and merge them into successively larger clusters.
❯ Divisive ("top-down"): Divisive algorithms begin with the whole set and proceed to divide it into successively smaller clusters.
2. Partitional clustering: Partitional algorithms determine all clusters at once. They include:
- K-means and derivatives
- Fuzzy c-means clustering
- QT clustering algorithm

#### Common Distance measures:

Distance measure will determine how the similarity of two elements is calculated and it will influence the shape of the clusters.
They include:
1. The Euclidean distance (also called 2-norm distance) is given by:

d(x,y) = √(<sup>P</sup>∑<sub>i=1</sub> |x<sub>i</sub>-y<sub>i</sub>|<sup>2</sup>)

2. The Manhattan distance (also called taxicab norm or 1-norm)
is given by:

d(x,y) = <sup>P</sup>∑<sub>i=1</sub> |x<sub>i</sub>-y<sub>i</sub>|
