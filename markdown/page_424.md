
#### 12.2.2.2 Count-Min Sketch

While the bloom filter is effective for set-membership queries, it is not designed for methods that require *count-based* summaries. This is because the bloom filter tracks only binary values. The count-min sketch is designed for resolving such queries and is intuitively related to the bloom filter. A count-min sketch consists of a set of $w$ different *numeric arrays*, each of which has a length $m$. Thus, the space requirement of the count-min sketch is equal to $m \cdot w$ cells containing numeric values. The elements of each of the $w$ numeric arrays are indexed starting with 0, corresponding to an index range of $\{0 \ldots m-1\}$. The count-min sketch can also be viewed as a $w \times m$-dimensional array of cells.

Each of the $w$ numeric arrays corresponds to a hash function. The $i$th numeric array corresponds to the $i$th hash function $h_i(x)$. The hash functions have the following properties:

1. The $i$th hash function $h_i(x)$ maps a stream element to an integer in the range $[0 \ldots m-1]$. This mapping can also be viewed as one of the index values in the $i$th numeric array.

2. The $w$ hash functions $h_1(\cdot) \ldots h_w(\cdot)$ are fully independent of one another, but *pairwise independent* over different arguments. In other words, for any two values $x_1$ and $x_2$, $h_i(x_1)$ and $h_i(x_2)$ are independent.

The *pairwise independence* requirement is a weaker one than the full independence requirement. This is a convenient property of the count-min sketch because it is usually easier to construct pairwise independent hash functions rather than fully independent ones.

The procedure for updating the sketch is as follows. All $m \cdot w$ entries in the count-min sketch are initialized to 0. For each incoming stream element $x$, the functions $h_1(x) \ldots h_w(x)$ are applied to it. For the $i$th array, the element $h_i(x)$ is incremented by 1. Thus, if the count-min sketch $CM$ is visualized as a $2$-dimensional $w \times m$ numeric array, then the element $(i, h_i(x))$ is incremented^2 by 1. Note that the value of $h_i(x)$ maps to an integer in the range $[0, m-1]$. This is also the range of the indices of each numeric array. A pictorial illustration of the count-min sketch and the corresponding update process is provided in Fig. 12.4. The pseudocode for the overall update process is illustrated in Fig. 12.5. In the pseudocode, the stream is denoted by $S$, and the count-min sketch data structure is denoted by $CM$. The inputs to the algorithm are the stream $S$ and two parameters $(w, m)$ specifying the size of the $2$-dimensional array for the count-min sketch. A $2$-dimensional $w \times m$ array $CM$ is initialized with all values set to 0. For each incoming stream element, the counts of all the cells in the sketch that correspond to the element is associated with a nonnegative frequency, the count-min sketch can be updated with the frequency value. Only the simple case of unit updates is discussed here.

[illustration, page 403]
