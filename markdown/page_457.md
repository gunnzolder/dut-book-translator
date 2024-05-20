
1. Select a cluster $G_m$, where $m \in \{1, \ldots, k\}$.

2. Generate the term distribution of $G_m$ based on a generative model. Examples of such models for text include the Bernoulli model or the multinomial model.

The observed data are then used to estimate the parameters of the Bernoulli or multinomial distributions in the generative process. This section will discuss the Bernoulli model.

The clustering is done in an iterative way with the EM algorithm, where cluster assignments of documents are determined from conditional word distributions in the E-step with the Bayes rule, and the conditional word distributions are inferred from cluster assignments in the M-step. For initialization, the documents are randomly assigned to clusters. The initial prior probabilities $P(G_m)$ and conditional feature distributions $P(w_j|G_m)$ are estimated from the statistical distribution of this random assignment. A Bayes classifier is used to estimate the posterior probability $P(G_m|X)$ in the E-step. The Bayes classifier commonly uses either a Bernoulli model or the multinomial model discussed later in this chapter. The posterior probability $P(G_m|X)$ of the Bayes classifier can be viewed as a soft assignment probability of document $X$ to the $m$th mixture component $G_m$. The conditional feature distribution $P(w_j|G_m)$ for word $w_j$ is estimated from these posterior probabilities in the M-step as follows:
$$
P(w_j|G_m) = \frac{\sum_X P(G_m|X) \cdot I(X, w_j)}{\sum_X P(G_m|X)} \tag{13.5}
$$

Here, $I(X, w_j)$ is an indicator variable that takes on the value of 1, if the word $w_j$ is present in $X$, and 0, otherwise. As in the Bayes classification method, the same Laplacian smoothing approach may be incorporated to reduce overfitting. The prior probabilities $P(G_m)$ for each cluster may also be estimated by computing the average assignment probability of all documents to $G_m$. This completes the description of the M-step of the EM algorithm. The next E-step uses these modified values of $P(w_j|G_m)$ and the prior probability to derive the posterior Bayes probability with a standard Bayes classifier. Therefore, the following two iterative steps are repeated to convergence:

1. (E-step) Estimate posterior probability of membership of documents to clusters using Bayes rule:
$$
P(G_m|X) \propto P(G_m) \prod_{w_j \in X} P(w_j|G_m) \prod_{w_j \notin X} (1 - P(w_j|G_m)) \tag{13.6}
$$

The aforementioned Bayes rule assumes a Bernoulli generative model. Note that Eq. 13.6 is identical to naive Bayes posterior probability estimation for classification. The multinomial model, which is discussed later in this chapter, may also be used. In such a case, the aforementioned posterior probability definition of Eq. 13.6 is replaced by the multinomial Bayes classifier.

2. (M-step) Estimate conditional distribution $P(w_j|G_m)$ of words (Eq. 13.5) and prior probabilities $P(G_m)$ of different clusters using the estimated probabilities in the E-step.

At the end of the process, the estimated value of $P(G_m|X)$ provides a cluster assignment probability and the estimated value of $P(w_j|G_m)$ provides the term distribution of each cluster. This can be viewed as a probabilistic variant of the notion of cluster digest discussed earlier. Therefore, the probabilistic method provides dual insights about cluster membership and the words relevant to each cluster.
