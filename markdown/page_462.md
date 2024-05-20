
An important assumption in PLSA is that the selected documents and words are conditionally independent after the latent topical component $G_m$ has been fixed. In other words, the following is assumed:

$$
P(X_i, w_j | G_m) = P(X_i | G_m) \cdot P(w_j | G_m) \tag{13.7}
$$

This implies that the joint probability $P(X_i, w_j)$ for selecting a document–word pair can be expressed in the following way:

$$
P(X_i, w_j) = \sum_{m=1}^k P(G_m) \cdot P(X_i, w_j | G_m) = \sum_{m=1}^k P(G_m) \cdot P(X_i | G_m) \cdot P(w_j | G_m) \tag{13.8}
$$

It is important to note that local independence between documents and words within a latent component does not imply global independence between the same pair over the entire corpus. The local independence assumption is useful in the derivation of EM algorithm. 

In PLSA, the posterior probability $P(G_m | X_i, w_j)$ of the latent component associated with a particular document-word pair is estimated. The EM algorithm starts by initializing $P(G_m)$, $P(X_i | G_m)$, and $P(w_j | G_m)$ to $1/k$, $1/n$, and $1/d$, respectively. Here, $k$, $n$, and $d$ denote the number of clusters, number of documents, and number of words, respectively. The algorithm iteratively executes the following E- and M-steps to convergence:

1. (E-step) Estimate posterior probability $P(G_m | X_i, w_j)$ in terms of $P(G_m)$, $P(X_i | G_m)$, and $P(w_j | G_m)$.

2. (M-step) Estimate $P(G_m)$, $P(X_i | G_m)$ and $P(w_j | G_m)$ in terms of the posterior probability $P(G_m | X_i, w_j)$, and observed data about word-document co-occurrence using log-likelihood maximization.

These steps are iteratively repeated to convergence. It now remains to discuss the details of the E-step and the M-step. First, the E-step is discussed. The posterior probability estimated in the E-step can be expanded using the Bayes rule:

$$
P(G_m | X_i, w_j) = \frac{P(G_m) \cdot P(X_i, w_j | G_m)}{P(X_i, w_j)} \tag{13.9}
$$

The numerator of the right-hand side of the aforementioned equation can be expanded using Eq. 13.7, and the denominator can be expanded using Eq. 13.8:

$$
P(G_m | X_i, w_j) = \frac{P(G_m) \cdot P(X_i | G_m) \cdot P(w_j | G_m)}{\sum_{r=1}^k P(G_r) \cdot P(X_i | G_r) \cdot P(w_j | G_r)} \tag{13.10}
$$

This shows that the E-step can be implemented in terms of the estimated values $P(G_m)$, $P(X_i | G_m)$, and $P(w_j | G_m)$.

It remains to show how these values can be estimated using the observed word-document co-occurrences in the M-step. The posterior probabilities $P(G_m | X_i, w_j)$ may be viewed as weights attached with word-document co-occurrence pairs for each aspect $G_m$. These weights can be leveraged to estimate the values $P(G_m)$, $P(X_i | G_m)$, and $P(w_j | G_m)$ for each aspect using maximization of the log-likelihood function. The details of the log-likelihood function and the differential calculus associated with the maximization process will not be discussed here. Rather, the final estimated values will be presented directly. Let $f(X_i, w_j)$ represent
