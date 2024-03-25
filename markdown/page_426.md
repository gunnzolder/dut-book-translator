```
Proof: The expected number of spurious items hashed to the cells belonging to item y is about $3 \cdot n_f/m$, if all spurious items are hashed uniformly at random to the different cells. This result uses pairwise independence of hash functions because it relies on the fact that the mapping of y to a cell does not affect the distribution of another spurious item in its cells. The probability of the number of spurious items exceeding $n_f \cdot \varepsilon/m$ in any of the w cells belonging to y is given by at most $e^{-1}$ by the Markov inequality. For $E(y)$ to exceed the upper bound of Eq. 12.23, this violation needs to be repeated for all the w cells to which y is mapped. The probability of a violation of Eq. 12.23 is therefore $e^{-w}$. The result follows.

In many cases, it is desirable to directly control the error level $\varepsilon$ and the error probability $\delta$. By setting $m = e/\varepsilon$ and $w = ln(1/\delta)$, it is possible to bond the error with a user-defined tolerance $n_f \cdot \varepsilon$ and probability at least $1 - \delta$. Two natural generalizations of the point query can be implemented as follows:

1. If the stream elements have arbitrary positive frequencies associated with them, the only change required is to the update operation, where the counts are incremented by the relevant frequency. The frequency bound is identical to Eq. 12.23, with $n_f$ representing the sum of the frequencies of the stream items.

2. If the stream elements have either positive or negative frequencies associated with them, then a further change is required to the query procedure. In this case, the median of the counts is reported. The corresponding error bound of Eq. 12.23 now needs to be modified. With a probability of at least $1 - e^{-w/4}$, the estimated frequency $E(y)$ of item y lies in the following ranges:

$$
G(y) - \frac{3n_f \cdot \varepsilon}{m} \leq E(y) \leq G(y) + \frac{3n_f \cdot \varepsilon}{m}.
$$

In this case, $n_f$ represents the sum of the absolute frequencies of the incoming items in the data stream. The bounds in this case are much weaker than those for nonnegative elements.

A useful application is to determine the dot product of the frequency counts of the discrete attribute values in two data streams. This has a useful application in estimating the join size on massive-domain attribute in two data streams. The dot product between the frequency counts of the items in a pair of nonnegative data streams can be estimated by first constructing a count-min sketch representation for each of the two data streams in a separate $w \times m$ count-min data structure. The same hash functions are used for both sketches. The dot product of their corresponding count-min arrays for each hash function is computed. The minimum value of the dot product over the w different arrays is reported as the estimation. As in the previous case, this is an overestimate, and an upper bound on the estimate may be obtained with a probability of at least $1 - e^{-w}$. The corresponding error tolerance for the upper bound is $n_{f1} \cdot n_{f2} \cdot \varepsilon/m$, where $n_{f1}$ and $n_{f2}$ are the aggregate frequencies of the items in each of the two streams. Other useful queries with the use of the count-min sketch include the determination of quantiles and frequent elements. Frequent elements are also referred to as heavy hitters. The bibliographic notes contain pointers to various queries and applications that can be addressed with the use of the count-min sketch.
```