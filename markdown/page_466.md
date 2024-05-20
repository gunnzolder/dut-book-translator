
G_m and can be derived from the parameters estimated in the M-step using the Bayes rule as follows:

$$
P(G_m | X_i) = \frac{P(G_m) \cdot P(X_i | G_m)}{\sum_{r=1}^{k} P(G_r) \cdot P(X_i | G_r)}. \tag{13.16}
$$

Thus, the PLSA approach can also be viewed as a soft clustering method that provides assignment probabilities of documents to clusters. In addition, the quantity $P(w_j | G_m)$, which is estimated in the M-step, provides probabilistic information about the probabilistic affinity of different words to aspects (or topics). The terms with the highest probability values for a specific aspect $G_m$ can be viewed as a cluster digest for that topic.

As the PLSA approach also provides a multidimensional $n \times k$ coordinate representation $Q_k \sum_k$ of the documents, a different way of performing the clustering would be to represent the documents in this new space and use a k-means algorithm on the transformed corpus. Because the noise impact of synonymy and polysemy has been removed by PLSA, the k-means approach will generally be more effective on the reduced representation than on the original corpus.

### 13.4.3 Limitations of PLSA

Although the PLSA method is an intuitively sound model for probabilistic modeling, it does have a number of practical drawbacks. The number of parameters grows linearly with the number of documents. Therefore, such an approach can be slow and may overfit the training data because of the large number of estimated parameters. Furthermore, while PLSA provides a generative model of document–word pairs in the training data, it cannot easily assign probabilities to previously unseen documents. Most of the other EM mixture models discussed in this book, such as the probabilistic Bayes model, are much better at assigning probabilities to previously unseen documents. To address these issues, Latent Dirichlet Allocation (LDA) was defined. This model uses Dirichlet priors on the topics, and generalizes relatively easily to new documents. In this sense, LDA is a fully generative model. The bibliographic notes contain pointers to this model.

## 13.5 Specialized Classification Methods for Text

As in clustering, classification algorithms are affected by the nonnegative, sparse and high-dimensional nature of text data. An important effect of sparsity is that the presence of a word in a document is more informative than the absence of the word. This observation has implications for classification methods such as the Bernoulli model used for Bayes classification that treat the presence and absence of a word in a symmetric way.

Popular techniques in the text domain include instance-based methods, the Bayes classifier, and the SVM classifier. The Bayes classifier is very popular because Web text is often combined with other types of features such as URLs or side information. It is relatively easy to incorporate these features into the Bayes classifier. The sparse high-dimensional nature of text also necessitates the design of more refined multinomial Bayes models for the text domain. SVM classifiers are also extremely popular for text data because of their high accuracy. The major issue with the use of the SVM classifier is that the high-dimensional nature of text necessitates performance enhancements to such classifiers. In the following, some of these algorithms will be discussed.
