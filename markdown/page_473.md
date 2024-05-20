
1. Determine optimal solution $(W, \xi)$ for objective function of (OP2) using only constraints in the working set $\text{WS}$.

2. Determine most violated constraint among the $2^n$ constraints of (OP2) by setting $u_1$ to 1 if $y_i W \cdot X_i < 1$, and 0 otherwise.

3. Add the most violated constraint to $\text{WS}$.

The termination criterion is the case when the most violated constraint is violated by no more than $\epsilon$. This provides an approximate solution to the problem, depending on the desired precision level $\epsilon$.

This algorithm has several desirable properties. It can be shown that the time required to solve the problem for a constant size working set $\text{WS}$ is $O(n \cdot s)$, where $n$ is the number of training examples, and $s$ is the number of nonzero attributes per example. This is important for the text domain, where the number of non-zero attributes is small. Furthermore, the algorithm usually terminates in a small constant number of iterations. Therefore, the working set $\text{WS}$ never exceeds a constant size, and the entire algorithm terminates in $O(n \cdot s)$ time.

# 13.6 Novelty and First Story Detection

The problem of first story detection is a popular one in the context of temporal text stream mining applications. The goal is to determine novelties from the underlying text stream based on the history of previous text documents in the stream. This problem is particularly important in the context of streams of news documents, where a first story on a new topic needs to be reported as soon as possible.

A simple approach is to compute the maximum similarity of the current document with all previous documents, and report the documents with very low maximum similarity values as novelties. Alternatively, the inverse of the maximum similarity value could be continuously reported as a streaming novelty score or alarm level. The major problem with this approach is that the stream size continuously increases with time, and one has to compute similarity with all previous documents. One possibility is to use reservoir sampling to maintain a constant sample of documents. The inverse of the maximum similarity of the document to any incoming document is reported as the novelty score. The major drawback of this approach is that similarity between individual pairs of documents is often not a stable representation of the aggregate trends. Text documents are sparse, and pairwise similarity often does not capture the impact of synonymy and polysemy.

## 13.6.1 Micro-clustering Method

The micro-clustering method can be used to maintain online clusters of the text documents. The idea is that micro-clustering simultaneously determines the clusters and novelties from the underlying text stream. The basic micro-clustering method is described in Sect. 12.4 of Chap. 12. The approach maintains $k$ different cluster centroids, or cluster digests. For an incoming document, its similarity to all the centroids is computed. If this similarity is larger than a user-defined threshold, then the document is added to the cluster. The frequencies of the words in the corresponding centroid are updated, by adding the frequency of the word in the document to it. For each document, only the $r$ most frequent words in the centroid are retained. The typical value of $r$ varies between 200 and 400. On the other hand, when the incoming document is not sufficiently similar to one of the centroids, then it is reported
