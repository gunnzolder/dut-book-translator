
where there are near ties in split quality (very small values of $\epsilon$), the algorithm will need
to wait for a larger value of $n$ until the aforementioned split condition is satisfied. It can
be shown that the probability that the Hoeffding tree makes the same classification on the
instance as a tree constructed with infinite data is given by at least $1 - \delta / p$, where $p$ is the
probability that the instance will be assigned to a particular leaf. The memory requirements
are modest because only the counts of the different discrete values of the attributes (over
different classes) need to be maintained at various nodes to make split decisions.
The major theoretical implication of the Hoeffding tree algorithm is that one does not
need all the data to grow exactly the same tree as what would be constructed by a poten-
tially infinite data stream. Rather, the total number of required tuples is limited once the
probabilistic certainty level $\delta$ is fixed. The major bottleneck of the approach is that the
construction of some of nodes is delayed because of near ties during tree construction. Most
of the time is spent in breaking near ties. In the Hoeffding tree algorithm, once a decision
is made about a split (and it is a poor one), it cannot be reversed. The incremental process
of Hoeffding tree construction is illustrated in Fig. 12.8. It is noteworthy that test instance
classification can be performed at any point during stream progression, but the size of the
tree increases over time together with classification accuracy.

The VFDT approach improves over the Hoeffding tree algorithm by breaking ties more
aggressively and through the deactivation of less promising leaf nodes. It also has a number
of optimizations to improve accuracy, such as the dropping of poor splitting attributes, and
batching intermediate computations over multiple data points. However, it is not designed to
handle concept drift. The CVFDT approach was subsequently designed to address concept
drift. CVFDT incorporates two main ideas to address the additional challenges of drift:

1. A sliding window of training items is used to limit the impact of historical behavior.

2. Alternate subtrees at each internal node $i$ are constructed to account for the fact
that the best split attribute may no longer remain the top choice because of stream
evolution.

Because of the sliding window approach, a difference from the previous method is in the
update of the attribute frequency statistics at the nodes, as the sliding window moves
forward. For the incoming items, their statistics are added to the attribute value frequencies
in the current window, and the expiring items at the other end of the window are removed
from the statistics as well. Therefore, when these statistics are updated, some nodes may no
longer meet the Hoeffding bound. Such nodes are replaced. CVFDT associates each internal
node $i$ with a list of alternate subtrees corresponding to splits on different attributes. These
