
Algorithm CountMinConstruct(Stream: $S$, Width: $w$, Height: $m$)
begin
    Initialize all entries of $w \times m$ array $CM$ to 0;
    repeat
        Receive next stream element $x \in S$;
        for $i = 1$ to $w$ do
            Increment $(i, h_i(x))$th element in $CM$ by 1;
    until end of stream $S$;
    return $CM$;
end

Algorithm CountMinQuery(Element: $y$, Count-min Sketch: $CM$)
begin
    Initialize $Estimate = \infty$;
    for $i = 1$ to $w$ do
        $Estimate = \min(Estimate, V_i(y))$;
    { $V_i(y)$ is the count of the $(i, h_i(y))$th element in $CM$ }
    return $Estimate$;
end

[Figure 12.5: Update of count-min sketch, page 404]

[Figure 12.6: Frequency queries for count-min sketch, page 404]

cells $(i, h_i(x))$ are updated for $i \in \{1 \ldots w\}$. In the pseudocode description, the resulting sketch $CM$ is returned after processing all the stream elements. In practice, the count-min sketch can be used at any time during the progression of the stream $S$. As in the case of the bloom filter, it is possible for multiple stream elements to map to the same cell in the count-min sketch. Therefore, different stream elements will increment the same cell, and the resulting cell counts are always overestimates of one or more stream element counts.

The count-min sketch can be used for many different queries. The simplest query is to determine the frequency of an element $y$. The first step is to compute the hash functions $h_1(y) \ldots h_w(y)$. For the each numeric array in $CM$, the value $V_i(y)$ of the $(i, h_i(y))$th array element is retrieved. The value $V_i(y)$ is an overestimate of the true frequency of $y$ because of potential collisions. Therefore, the tightest possible estimate may be obtained by using the minimum value $min(V_i(y))$ over the different hash functions. The overall procedure for frequency estimation is illustrated in Fig. 12.6.

The count-min sketch causes an overestimation of frequency values because of collisions of nonnegative frequency counts of distinct stream items. It is therefore helpful to determine an upper bound on the estimation quality.

Lemma 12.2.3 Let $E(y)$ be the estimate of the frequency of the item $y$, using a count-min sketch of size $w \times m$. Let $n_f$ be the total frequencies of all items received so far, and $G(y)$ be true frequency of item $y$. Then, with probability at least $1 - e^{-w}$, the upper bound on the estimate $E(y)$ is as follows:
$$
E(y) \leq G(y) + \frac{n_f \cdot e}{m}.
$$
Here, $e$ represents the base of the natural logarithm. (12.23)
