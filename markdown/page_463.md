
the observed frequency of the occurrence of word $w_j$ in document $X_i$ in the corpus. Then, the estimations in the M-step are as follows:

$$
P(X_i|g_m) \propto \sum_{w_j} f(X_i, w_j) \cdot P(g_m|X_i, w_j) \quad \forall i \in \{1 \ldots n\}, m \in \{1 \ldots k\} \tag{13.11}
$$

$$
P(w_j|g_m) \propto \sum_{X_i} f(X_i, w_j) \cdot P(g_m|X_i, w_j) \quad \forall j \in \{1 \ldots d\}, m \in \{1 \ldots k\} \tag{13.12}
$$

$$
P(g_m) \propto \sum_{X_i} \sum_{w_j} f(X_i, w_j) \cdot P(g_m|X_i, w_j) \quad \forall m \in \{1 \ldots k\}. \tag{13.13}
$$

Each of these estimations may be scaled to a probability by ensuring that they sum to 1 over all the outcomes for that random variable. This scaling corresponds to the constant of proportionality associated with the “$\propto$” notation in the aforementioned equations. Furthermore, these estimations can be used to decompose the original document-term matrix into a product of three matrices, which is very similar to SVD/LSA. This relationship will be explored in the next section.

## 13.4.1 Use in Dimensionality Reduction and Comparison with Latent Semantic Analysis

The three key sets of parameters estimated in the M-step are $P(X_i|g_m)$, $P(w_j|g_m)$, and $P(g_m)$, respectively. These sets of parameters provide an SVD-like matrix factorization of the $n \times d$ document-term matrix $D$. Assume that the document-term matrix $D$ is scaled by a constant to sum to an aggregate probability value of 1. Therefore, the $(i, j)$th entry of $D$ can be viewed as an observed instantiation of the probabilistic quantity $P(X_i, w_j)$. Let $Q_k$ be the $n \times k$ matrix, for which the $(i, m)$th entry is $P(X_i|g_m)$, let $\Sigma_k$ be the $k \times k$ diagonal matrix for which the $m$th diagonal entry is $P(g_m)$, and let $P_k$ be the $d \times k$ matrix for which the $(j, m)$th entry is $P(w_j|g_m)$. Then, the $(i, j)$th entry $P(X_i, w_j)$ of the matrix $D$ can be expressed in terms of the entries of the aforementioned matrices according to Eq. 13.8, which is replicated here:

$$
P(X_i, w_j) = \sum_{m=1}^{k} P(g_m) \cdot P(X_i|g_m) \cdot P(w_j|g_m). \tag{13.14}
$$

This LHS of the equation is equal to the $(i, j)$th entry of $D$, whereas the RHS of the equation is the $(i, j)$th entry of the matrix product $Q_k \Sigma_k P_k^T$. Depending on the number of components $k$, the LHS can only approximate the matrix $D$, which is denoted by $D_k$. By stacking up the $n \times d$ conditions of Eq. 13.14, the following matrix condition is obtained:

$$
D_k = Q_k \Sigma_k P_k^T. \tag{13.15}
$$

It is instructive to note that the matrix decomposition in Eq. 13.15 is similar to that in SVD/LSA (cf. Eq. 2.12 of Chap. 2). Therefore, as in LSA, $D_k$ is an approximation of the document-term matrix $D$, and the transformed representation in $k$-dimensional space is given by $Q_k \Sigma_k$. However, the transformed representations will be different in PLSA and LSA. This is because different objective functions are optimized in the two cases. LSA minimizes the mean-squared error of the approximation, whereas PLSA maximizes the log-likelihood fit to a probabilistic generative model. One advantage of PLSA is that the entries of $Q_k$ and $P_k$ and the transformed coordinate values are nonnegative and have clear
