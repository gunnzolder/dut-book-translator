
## 13.2.1 Document Normalization and Similarity Computation

The problem of document normalization is closely related to that of similarity computation. While the issue of text similarity is discussed in Chap. 3, it is also discussed here for completeness. Two primary types of normalization are applied to documents:

1. **Inverse document frequency:** Higher frequency words tend to contribute noise to data mining operations such as similarity computation. The removal of stop words is motivated by this aspect. The concept of inverse document frequency generalizes this principle in a softer way, where words with higher frequency are weighted less.

2. **Frequency damping:** The repeated presence of a word in a document will typically bias the similarity computation significantly. To provide greater stability to the similarity computation, a damping function is applied to word frequencies so that the frequencies of different words become more similar to one another. It should be pointed out that frequency damping is optional, and the effects vary with the application at hand. Some applications, such as clustering, have shown comparable or better performance without damping. This is particularly true if the underlying data sets are relatively clean and have few spam documents.

In the following, these different types of normalization will be discussed. The inverse document frequency $id_i$ of the $i$th term is a decreasing function of the number of documents $n_i$ in which it occurs:

$$
id_i = \log(n/n_i). \tag{13.1}
$$

Here, the number of documents in the collection is denoted by $n$. Other ways of computing the inverse document frequency are possible, though the impact on the similarity function is usually limited.

Next, the concept of frequency damping is discussed. This normalization ensures that the excessive presence of a single word does not throw off the similarity computation. Consider a document with word-frequency vector $X = (x_1 \ldots x_d)$, where $d$ is the size of the lexicon. A damping function $f(\cdot)$, such as the square root or the logarithm, is optionally applied to the frequencies before similarity computation:

$$
f(x_i) = \sqrt{x_i}
$$

$$
f(x_i) = \log(x_i).
$$

Frequency damping is optional and is often omitted. This is equivalent to setting $f(x_i)$ to $x_i$. The normalized frequency $h(x_i)$ for the $i$th word may be defined as follows:

$$
h(x_i) = f(x_i) id_i. \tag{13.2}
$$

This model is popularly referred to as the tf-idf model, where tf represents the term frequency and idf represents the inverse document frequency.

The normalized representation of the document is used for data mining algorithms. A popularly used measure is the cosine measure. The cosine measure between two documents with raw frequencies $X = (x_1 \ldots x_d)$ and $\mathbf{Y} = (y_1 \ldots y_d)$ is defined using their normalized representations:

$$
\cos(X, Y) = \frac{\sum_{i=1}^{d} h(x_i) h(y_i)}{\sqrt{\sum_{i=1}^{d} h(x_i)^2} \sqrt{\sum_{i=1}^{d} h(y_i)^2}} \tag{13.3}
$$

Another measure that is less commonly used for text is the Jaccard coefficient $J(X, Y)$:

$$
J(X, Y) = \frac{\sum_{i=1}^{d} h(x_i) h(y_i)}{\sum_{i=1}^{d} h(x_i)^2 + \sum_{i=1}^{d} h(y_i)^2 - \sum_{i=1}^{d} h(x_i) h(y_i)} \tag{13.4}
$$
