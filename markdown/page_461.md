```
can be viewed as a probabilistic variant of SVD and LSA, rather than a probabilistic variant
of clustering. Nevertheless, soft clusters can also be generated with the use of this method.
There are many other dimensionality reduction methods, such as nonnegative matrix fac-
torization, which are intimately related to clustering. PLSA is, in fact, a nonnegative matrix
factorization method with a maximum-likelihood objective function.

In most of the EM clustering algorithms of this book, a mixture component (cluster) is
selected, and then the data record is generated based on a particular form of the distribution
of that component. An example is the Bernoulli clustering model, which is discussed in
Sect. 13.3.2. In PLSA, the generative process^3 is inherently designed for dimensionality
reduction rather than clustering, and different parts of the same document can be generated
by different mixture components. It is assumed that there are k aspects (or latent topics)
denoted by $G_1 . . . G_k$. The generative process builds the document-term matrix as follows:

1. Select a latent component (aspect) $G_m$ with probability $P(G_m)$.

2. Generate the indices $(i, j)$ of a document–word pair $(X_i, w_j)$ with probabilities
$P(X_i|G_m)$ and $P(w_j|G_m)$, respectively. Increment the frequency of entry $(i, j)$ in the
document-term matrix by 1. The document and word indices are generated in a prob-
abilistically independent way.

All the parameters of this generative process, such as $P(G_m)$, $P(X_i|G_m)$, and $P(w_j|G_m)$,
need to be estimated from the observed frequencies in the $n \times d$ document-term matrix.

Although the aspects $G_1 . . . G_k$ are analogous to the clusters of Sect. 13.3.2, they are not
the same. Note that each iteration of the generative process of Sect. 13.3.2 creates the final
frequency vector of an entire row of the document-term matrix. In PLSA, even a single
matrix entry may have frequency contributions from various mixture components. Indeed,
even in deterministic latent semantic analysis, a document is expressed as a linear combina-
tion of different latent directions. Therefore, the interpretation of each mixture component
as a cluster is more direct in the method of Sect. 13.3.2. The generative differences between
these models are illustrated in Fig. 13.3. Nevertheless, PLSA can also be used for clus-
tering because of the highly interpretable and nonnegative nature of the underlying latent
factorization. The relationship with and applicability to clustering will be discussed later.
```
