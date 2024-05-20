
To make this decision, the cluster feature vector of $M_p$ is used to decide if this data
point falls within the maximum boundary of the microcluster $M_p$. If so, then the data point
$X_i$ is added to the microcluster $M_p$ by using the additivity property of microclusters. The
maximum boundary of the microcluster $M_p$ is defined as a factor of $t$ the root-mean-square
deviation of the data points in $M_p$ from the centroid. The value of $t$ is a user-defined
parameter, and it is typically set to 3.

If the data point does not lie within the maximum boundary of the nearest microcluster,
then a new microcluster must be created containing the data point $X_i$. However, to create
this new microcluster, the number of other microclusters must be reduced by 1 to free
memory availability. This can be achieved by either deleting an old microcluster or merging
two of the older clusters. This decision is made by examining the staleness of the different
clusters, and the number of points in them. The time-stamp statistics of the microclusters
are examined to determine whether one of them is “sufficiently” stale to merit removal. If
this is not the case, then a merging of the two microclusters is initiated.

How is staleness of a microcluster determined? The microclusters are used to approx-
imate the average time-stamp of the last $m$ data points of the cluster $M$. This value is
not known explicitly because the last $m$ data points are not explicitly retained in order
to minimize memory requirements. The mean $\mu$ and variance $\sigma^2$ of the time-stamps in the
microcluster can be used together with a normal distribution assumption of the distribution
of time stamps to estimate this value. Thus, if the cluster contains $m_0 > m$ data points, then
the $m/(2 \cdot m_0)$th percentile of the normal distribution with mean $\mu$ and variance $\sigma^2$ may
be used as the estimate. This value is referred to as the relevance stamp of cluster $M$. Note
that $\mu$ and $\sigma^2$ can be computed from the temporal components of the cluster feature vec-
tors. When the smallest such relevance stamp of any microcluster is below a user-defined
threshold $\delta$, it can be eliminated. In cases where no microclusters can be safely deleted,
the closest microclusters are merged. The merging operation can be effectively performed
because of the existence of the cluster feature vector. Distances between microclusters can
be easily computed using the cluster-feature vector. When two microclusters are merged,
their statistics are added together, because of the additivity property of microclusters.

## 12.4.2.3 Pyramidal Time Frame

The microclusters statistics are stored periodically to enable horizon-specific analysis of the
clusters. This maintenance is performed during the microclustering phase. In this approach,
the microcluster snapshots are stored at varying levels of granularity depending on the
recency of the snapshot. Snapshots are classified into different orders that can vary from 1
to $\log(T)$, where $T$ is the clock time elapsed since the beginning of the stream. The order
of a snapshot regulates the level of temporal granularity at which it is stored, according to
the following rules:

- Snapshots of the $i$th order are stored at time intervals of $\alpha^i$, where $\alpha$ is an integer
  and $\alpha \geq 1$. Specifically, each snapshot of the $i$th order is stored when the clock value
  is exactly divisible by $\alpha^i$.

- At any given time, only the last $\alpha^l + 1$ snapshots of order $i$ are stored.

The aforementioned definition allows for considerable redundancy in storage of snapshots.
For example, the clock time of 8 is divisible by $2^0, 2^1, 2^2$, and $2^3$ (where $\alpha = 2$). Therefore,
the state of the microclusters at a clock time of 8 simultaneously corresponds to order 0,
order 1, order 2, and order 3 snapshots. From an implementation point of view, a snapshot
needs to be maintained only once.
