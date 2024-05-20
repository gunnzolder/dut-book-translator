
of edges across the partition represents the weight of the nonzero entries in Fig. 13.1b. Therefore, a $k$-way co-clustering problem can be converted to a $k$-way graph partitioning problem. The overall co-clustering approach may be described as follows:

1. Create a graph $G = (N_d \cup N_w, A)$ with nodes in $N_d$ representing documents, nodes in $N_w$ representing words, and edges in $A$ with weights representing nonzero entries in matrix $D$.

2. Use a $k$-way graph partitioning algorithm to partition the nodes in $N_d \cup N_w$ into $k$ groups.

3. Report row–column pairs $(R_i V_i)$ for $i \in \{1 \ldots k\}$. Here, $R_i$ represents the rows corresponding to nodes in $N_d$ for the $i$th cluster, and $V_i$ represents the columns corresponding to the nodes in $N_w$ for the $i$th cluster.

It remains to be explained, how the $k$-way graph partitioning may be performed. The problem of graph partitioning is addressed in Sect. 19.3 of Chap. 19. Any of these algorithms may be leveraged to determine the required graph partitions. Specialized methods for bipartite graph partitioning are also discussed in the bibliographic notes.

## 13.4 Topic Modeling

Topic modeling can be viewed as a probabilistic version of the latent semantic analysis (LSA) method, and the most basic version of the approach is referred to as Probabilistic Latent Semantic Analysis (PLSA). It provides an alternative method for performing dimensionality reduction and has several advantages over traditional LSA.

Probabilistic latent semantic analysis is an expectation maximization-based mixture modeling algorithm. However, the way in which the EM algorithm is used is different than the other examples of the EM algorithm in this book. This is because the underlying generative process is different, and is optimized to discovering the correlation structure of the words rather than the clustering structure of the documents. This is because the approach
