
11. Suppose that $X$ is a random variable, which always lies in the range $[1, 64]$. Suppose that $Y$ is the geometric mean of a large number $n$ of independent and identical realizations of $X$. Establish a bound on $\log_2(Y)$. Assume that you know the expected value of $\log_2(X)$.

12. Let $Z$ be a random variable satisfying $E[Z] = 0$, and $Z \in [a, b]$.

(a) Show that $E[e^{t \cdot Z}] \le e^{t^2 \cdot (b-a)^2/8}$.

(b) Use the aforementioned result to complete the proof of the Hoeffding inequality.

13. Suppose that $n$ distinct items are loaded into a bloom filter of length $m$ with $w$ hash functions.

(a) Show that the probability of a bit taking on the value of 0 is equal to $(1 - 1/m)^{nw}$.

(b) Show that the probability in (a) is approximately equal to $e^{-nw/m}$.

(c) Show that the expected number of 0-bits $m_0$ in the bloom filter is related to $n$, $m$, and $w$ as follows:
$$
n \approx \frac{m \cdot \ln(m/m_0)}{w}
$$

14. Show the proof of the bound discussed in the chapter for the count-min sketch when items with negative counts are included in the sketch.

15. Let a single component of an AMS sketch be constructed for each of two streams with the same hash-function. Show that the expected value of the product of these components is equal to the dot product of the frequency vector of distinct items in the two streams.

16. Show that the variance of the square of an AMS sketch component is bounded above by twice the square of the second-order moment of the items in the data stream.

17. Show the correctness of AMS point query frequency estimation methodology discussed in the chapter. In other words, the expected value of the $r_i \cdot Q$ should be equal to the point query result.
