
Algorithm BloomQuery(Element: y, Bloom Filter: B)
begin
  Initialize BooleanFlag = 1;
  for i = 1 to w do
    BooleanFlag = BooleanFlag AND h_i(y);
  return BooleanFlag;
end

[Figure 12.3: Membership check using bloom filter, page 401]

Proof: Consider a particular bit corresponding to the bit array element h_r(y) for some fixed value of the index r ∈ {1...w}. Each element x ∈ S sets u different bits h_1(x)...h_u(x) to 1. The probability that none of these bits is the same as h_r(y) is given by (1 - 1/m)^u. Over n distinct stream elements, this probability is (1 - 1/m)^un. Therefore, the probability that the bit array index h_r(y) is set to 1, by at least one of the n spurious elements in S is given by Q = 1 - (1 - 1/m)^un. A false positive occurs, when all bit array indices h_r(y) (over varying values of r ∈ {1...w}) have been set to 1. The probability of this is F = Q^w. The result follows.

While the false-positive probability is expressed above in terms of the number of distinct stream elements, it is trivially true for the total number of stream elements (including repetitions), as an upper bound.

The expression in the aforementioned lemma can be simplified by observing that (1 - 1/m)^m ≈ e^(-1), where e is the base of the natural logarithm. Correspondingly, the expression can be rewritten as follows:
$$
F = (1 - e^{-u/m})^w.
$$
(12.19)

Values of u that are too small or too large lead to poor performance. The value of u needs be selected optimally in terms of m and n to minimize the number of false positives. The number of false positives is minimized, when u = m * ln(2)/n. Substituting this value in Eq. 12.19, it can be shown that the probability of false positives for optimal number of hash functions is:
$$
F = 2^{-m \cdot ln(2)/n}.
$$
(12.20)

The expression above can be written purely as an expression of m/n. Therefore, for a fixed value of the false-positive probability F, the length of the bloom filter needs to be proportional to the number of distinct elements n in the data stream. Furthermore, the constant of proportionality for a particular false-positive probability F can be shown to be
$$
\frac{m}{n} = \left(\frac{\ln(1/F)}{(\ln(2))^2}\right).
$$
While this may not seem like a significant compression, it needs to be pointed out that bloom filters use elementary bits to track the membership of arbitrary elements, such as strings. Furthermore, because of bitwise operations, which can be implemented very efficiently with low-level implementations, the overall approach is generally very efficient.

It does need to be kept in mind that the value of n is not known in advance for many applications. Therefore, one strategy is to use a cascade of bloom filters for geometrically increasing values of u, and to use a logical AND of the membership query result over different bloom filters. This is a practical approach that provides more stable performance over the life of the data stream.

The bloom filter is referred to as a "filter" because it is often used to make decisions on which elements to exclude from a data stream, when they meet the membership condition.
