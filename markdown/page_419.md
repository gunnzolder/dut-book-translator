
Table 12.1: Comparison of different methods used to bound tail probabilities

| Result       | Scenario                                    | Strength |
|--------------|---------------------------------------------|----------|
| Chebyshev    | Any random variable                         | Weak     |
| Markov       | Nonnegative random variable                 | Weak     |
| Hoeffding    | Sum of independent bounded random variables | Strong   |
| Chernoff     | Sum of independent Bernoulli variables      | Strong   |

This inequality holds for any nonnegative value of t. Therefore, to find the tightest bound, the value of t that minimizes the right-hand side of the above equation needs to be determined. The optimal value of t = t* can be shown to be:

$$
t^* = \frac{40}{\sum_{i=1}^n (u_i - l_i)^2} .
$$

(12.17)

By substituting the value of t = t* in Eq. 12.16, the desired result may be obtained. The lower-tail bound may be derived by applying the aforementioned steps to $P(E[X] - X > \theta)$ rather than $P(X - E[X] > \theta)$. 

Thus, the different inequalities may apply to scenarios of different generality, and they may also have different levels of strength. These different scenarios are illustrated in Table 12.1.

## 12.2.2 Synopsis Structures for the Massive-Domain Scenario

As discussed in the introduction, many streaming applications contain discrete attributes, whose domain is drawn on a large number of distinct values. A classical example would be the value of the IP address in a network stream, or the e-mail address in an e-mail stream. Such scenarios are more common in data streams, simply because the massive number of data items in the stream are often associated with discrete identifiers of different types. E-mail addresses and IP addresses are examples of such identifiers. The streaming objects are often associated with pairs of identifiers. For example, each element of an e-mail stream may have both a sender and recipient. In some applications, it may be desirable to store statistics using pairwise identifiers, and therefore the pairwise combination is treated as a single integrated attribute. The domain of possible values can be rather large. For example, for an e-mail application with over a hundred million different senders and receivers, the number of possible pairwise combinations is $10^{16}$. In such cases, even storing simple summary statistics such as set membership, frequent item counts, and distinct element counts becomes more challenging from the perspective of space constraints.

If the number of distinct elements were small, one might simply use an array, and update the counts in these arrays in order to create an effective summary. Such a summary could address all the aforementioned queries. However, such an approach would not be practical in the massive-domain scenario because an array with $10^{16}$ elements would require more than 10 petabytes. Furthermore, for many queries, such as set membership and distinct element counting, a reservoir sample would not work well. This is because the vast majority of the stream may contain infrequent elements, and the reservoir will disproportionately overrepresent the frequent elements for queries that are agnostic to the absolute frequency. Set membership and distinct-element counting are examples of such queries.

It is often difficult to create a single synopsis structure that can address all queries. Therefore, different synopsis structures are designed for different classes of queries. In the
