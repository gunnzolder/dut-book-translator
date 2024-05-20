
lexicon in each of these centroids provides a stable and topical representation of the subjects in each class. An example of the (weighted) word vectors for two classes corresponding to the labels “Business schools” and “Law schools” could be as follows:

1. **Business schools**: business (35), management (31), school (22), university (11), campus (15), presentation (12), student (17), market (11), ...

2. **Law schools**: law (22), university (11), school (13), examination (15), justice (17), campus (10), courts (15), prosecutor (22), student (15), ...

Typically, most of the noisy words have been truncated from the cluster digest. Similar words are represented in the same centroid, and words with multiple meanings can be represented in contextually different centroids. Therefore, this approach also indirectly addresses the issues of synonymy and polysemy, with the additional advantage that the $k$-nearest neighbor classification can be performed more efficiently with a smaller number of centroids. The dominant label from the top-$k$ matching centroids, based on cosine similarity, is reported. Such an approach can provide comparable or better accuracy than the vanilla $k$-nearest neighbor classifier in many cases.

### 13.5.1.3 Rocchio Classification

The Rocchio method can be viewed as a special case of the aforementioned description of the centroid-based classifier. In this case, all documents belonging to the same class are aggregated into a single centroid. For a given document, the class label of the closest centroid is reported. This approach is obviously extremely fast because it requires a small constant number of similarity computations that is dependent on the number of classes in the data. On the other hand, the drawback is that the accuracy depends on the assumption of class contiguity. The class-contiguity assumption, as stated in [377], is as follows:

“Documents in the same class form a contiguous region, and regions of different classes do not overlap.”

Thus, Rocchio’s method would not work very well if documents of the same class were separated into distinct clusters. In such cases, the centroid of a class of documents may not even lie in one of the clusters of that class. A bad case for Rocchio’s method is illustrated in Fig. 13.6, in which two classes and four clusters are depicted. Each class is associated with two distinct clusters. In this case, the centroids for each of the classes are approximately the same. Therefore, the Rocchio method would have difficulty in distinguishing between the classes. On the other hand, a $k$-nearest neighbor classifier for small values of $k$, or a centroid-based classifier would perform quite well in this case. As discussed in Chap. 11, an increase in the value of $k$ for a $k$-nearest neighbor classifier increases its bias. The Rocchio classifier can be viewed as a $k$-nearest neighbor classifier with a high value of $k$.

### 13.5.2 Bayes Classifiers

The Bayes classifier is described in Sect. 10.5.1 of Chap. 10. The particular classifier described was a binary (or Bernoulli) model in which the posterior probability of a document belonging to a particular class was computed using only the presence or the absence of a word. This special case corresponds to the fact that each feature (word) takes on the value of either 0 or 1 depending on whether or not it is present in the document. However, such an approach does not account for the frequencies of the words in the documents.
