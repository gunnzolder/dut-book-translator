
the median of $O(\ln(1/\delta))$ averages of different sets of $O(1/\epsilon^2)$ values of $Q_i \cdot R_i$. It is possible to bound the approximation within $1 \pm \epsilon$ with probability at least $1 - \delta$. This estimation can be performed using the count-min sketch as well, though with a different bound.

2. The Euclidean distance between the frequency counts of a pair of streams can be estimated as $Q_i^2 + R_i^2 - 2Q_i \cdot R_i$. The Euclidean distance can be viewed as a linear combination of three different dot products (including self-products) between the frequency counts of the two streams. Because each dot product is itself bounded using the “mean–median trick” discussed above, the approach can be used to determine similar quality bounds in this case as well.

3. Like the count-min sketch, the AMS sketch can be used to estimate frequency values. For the $j$th distinct stream element with frequency $f_j$, the product of the random variable $r_j$ and $Q_i$ provides an estimate of the frequency.

$$
E[f_j] = r_j \cdot Q_i \tag{12.29}
$$

The mean, median, or mean–median combination of these values over different sketch components $Q_i$ can be reported as a robust estimate. The AMS sketch can also be used to identify heavy hitters from the data stream.

Some of the queries resolved by the AMS and count-min sketch are similar, although others are different. The bounds provided by the two techniques are also different, although none of them is strictly better than the other in all scenarios. The count-min sketch does have the advantage of being intuitively easy to interpret because of its natural hash-table data structure. As a result, it can be more naturally integrated in data mining applications such as clustering and classification in a seamless way.

## 12.2.2.4 Flajolet–Martin Algorithm for Distinct Element Counting

Sketches are designed for determining stream statistics that are dominated by large aggregate signals of frequent items. However, they are not optimized for estimating stream statistics that are dominated by infrequently occurring items. Problems such as distinct element counting are more directly influenced by the much larger number of infrequent items in a data stream. Distinct element counting can be performed efficiently with the Flajolet–Martin algorithm.

The Flajolet–Martin algorithm uses a hash function $h(\cdot)$ to render a mapping from a given element $x$ in the data stream to an integer in the range $[0, 2^L - 1]$. The value of $L$ is selected to be large enough, so that $2^L$ is an upper bound on the number of distinct elements. Usually, the value $L$ is selected to be 64 for implementation convenience, and because the value of $2^{64}$ is large enough for most practical applications. Therefore, the binary representation of the integer $h(x)$ will have length $L$. The position of the rightmost 1 bit of the binary representation of the integer $h(x)$ is determined. Thus, the value of $R$ represents the number of trailing zeros in this binary representation. Let $R_{\max}$ be the maximum value of $R$ over all stream elements. The value of $R_{\max}$ can be maintained incrementally in the streaming scenario by applying the hash function to each incoming stream element, determining its rightmost bit, and then updating $R_{\max}$. The key idea in the Flajolet–Martin algorithm is that the dynamically maintained value of $R_{\max}$ is logarithmically related to the number of distinct elements encountered so far in the stream.
