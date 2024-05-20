
the array. Consider the situation where n items have already been processed. Because each
segment contains w items, a total of $r = O(n/w) = O(n \cdot \epsilon)$ segments have been processed.
This implies that any particular item has been decremented at most $r = O(n \cdot \epsilon)$ times.
Therefore, if $\lfloor n \cdot \epsilon \rfloor$ were to be added to the counts of the items after processing n items, then
no count will be underestimated. Furthermore, this is a good overestimate on the frequency
that is proportional to the user-defined tolerance $\epsilon$. If the frequent items are reported with
the use of this overestimate, it may result in some false positives, but no false negatives.
Under some uniformity assumptions, it has been shown that the lossy counting algorithm
requires $O(1/\epsilon)$ space.

The approach can be generalized to the case of frequent patterns by batching multiple
segments, each of size $w = \lfloor 1/\epsilon \rfloor$. In this case, arrays containing counts of patterns (rather
than items) are maintained. However, patterns can obviously not be generated efficiently
from individual transactions. The idea here is to batch $\eta$ segments that are read into main
memory. The value of $\eta$ is decided on the basis of memory availability. When the $\eta$ segments
have been read in, the frequent patterns with (absolute) support of at least $\eta$ are determined
using any memory-based frequent pattern mining algorithm. First, all the old counts in the
array are decremented by $\eta$, and then the counts of the corresponding patterns from the
current segment are added to the array. Those itemsets with zero or negative supports are
removed from the array. Over the entire processing of the stream of length n, the count of
any itemset is decreased by at most $\lfloor \epsilon \cdot n \rfloor$. Therefore, by adding $\lfloor \epsilon \cdot n \rfloor$ to all array counts
at the end of the process, no counts would be underestimated. The overestimate is the same
as in the previous case. Thus, it is possible to report the frequent patterns with no false
negatives, and false positives that are regulated by user-defined tolerance $\epsilon$. Conceptually,
the main difference of this algorithm for frequent itemset counting from the aforementioned
algorithm for frequent item counting is that batching is used. The main goal of batching
is to reduce the number of frequent patterns generated at support level of $\eta$ during the
application of the frequent pattern mining algorithm. If batching is not used, then a large
number of irrelevant frequent patterns will be generated at an absolute support level of 1.
The main shortcoming of lossy counting is that it cannot adjust to concept drift. In this
sense, reservoir sampling has a number of advantages over the lossy counting algorithm.

# 12.4 Clustering Data Streams

The problem of clustering is especially significant in the data stream scenario because of its
ability to provide a compact synopsis of the data stream. A clustering of the data stream
can often be used as a heuristic substitute for reservoir sampling, especially if a fine-grained
clustering is used. For these reasons, stream clustering is often used as a precursor to other
applications such as streaming classification. In the following, a few representative stream
clustering algorithms will be discussed.

## 12.4.1 STREAM Algorithm

The STREAM algorithm is based on the k-medians clustering methodology. The core idea is
to break the stream into smaller memory-resident segments. Thus, the original data stream
$S$ is divided into segments $S_1 \ldots S_r$. Each segment contains at most $m$ data points. The
value of $m$ is fixed on the basis of a predefined memory budget.

Because each segment $S_i$ fits in main memory, a more complex clustering algorithm can
be applied to it, without worrying about the one-pass constraint. One can use a variety
