markdown
Algorithm BloomConstruct(Stream: $S$, Size: $m$, Num. Hash Functions: $w$)
begin
  Initialize all elements in a bit array $B$ of size $m$ to 0;
  repeat
    Receive next stream element $x \in S$;
    for $i = 1$ to $w$ do
      Update $h_i(x)$th element in bit array $B$ to 1;
    until end of stream $S$;
  return $B$;
end

[Figure 12.2: Update of bloom filter, page 400]

are not possible with the bloom filter. On the other hand, if all the entries $h_1(y) \ldots h_w(y)$ in the bit array have a value of 1, then it is reported that $y$ has occurred in the data stream. This can be checked efficiently by applying an “AND” logical operator to all the bit entries corresponding to the indices $h_1(y) \ldots h_w(y)$ in the bit array. The overall procedure of membership checks is illustrated in Fig. 12.3. The binary result for the decision problem for checking membership is tracked by the variable $BooleanFlag$. This binary flag is reported at the end of the procedure.

The bloom filter approach can lead to false positives, but not false negatives. A false positive occurs, if all the w different bloom filter array elements $h_i(y)$ for $i = 1 \ldots w$ have been set to 1 by some spurious element other than $y$. This is a direct result of collisions. As the number of elements in the data stream increases, all elements in the bloom filter are eventually set to 1. In such a case, all set-membership queries will yield a positive response. This is, of course, not a useful application of the bloom filter. Therefore, it is instructive to bound the false positive probability in terms of the size of the filter and the number of distinct elements in the data stream.

Lemma 12.2.2 Consider a bloom filter $B$ with $m$ elements, and $w$ different hash functions. Let $n$ be the number of distinct elements in the stream $S$ so far. Consider an element $y$, which has not appeared in the stream so far. Then, the probability $F$ that an element $y$ is reported as a false positive is given by the following:

$$
F = \left[ 1 - \left( 1 - \frac{1}{m} \right)^{wn} \right]^w
$$

(12.18)
