
12.5. STREAMING OUTLIER DETECTION

1. The statistics of the newly inserted data points are computed such as its reachability distance and LOF score.

2. The LOF scores of the existing points in the window are updated along with their densities and reachability distances. In other words, the scores of many of the existing data points need to be updated because they are affected by the addition of a new data point. However, not all scores need to be updated because only the locality of the new data point is affected. Similarly, when data points are deleted, only the LOF scores in the locality of the deleted point are affected.

Because distance-based methods are well-known to be computationally expensive, many of the aforementioned methods are still quite expensive in the context of the data stream. Therefore, the complexity of the outlier detection process can be greatly improved by using an online clustering-based approach. The microclustering approach discussed earlier in this chapter automatically discovers outliers, together with clusters.

While clustering-based methods are generally not advisable when the number of data points are limited, this is not the case in streaming analysis. In the context of a data stream, a sufficient number of data points are typically available to maintain the clusters at a very high level of granularity. *In the context of a streaming clustering algorithm, the formation of new clusters is often associated with unsupervised novelties.* For example, the CluStream algorithm explicitly regulates the creation of new clusters in the data stream when an incoming data point does not lie within a specified statistical radius of the existing clusters in the data. Such data points may be considered outliers. In many cases, this is the beginning of a new trend, as more data points are added to the cluster at later stages of the algorithm. In some cases, such data points may correspond to novelties, and in other cases, they may correspond to trends that were seen a long time ago, but are no longer reflected in the current clusters. In either case, such data points are interesting outliers. However, it is not possible to distinguish between these different kinds of outliers unless one is willing to allow the number of clusters in the stream to increase over time.

## 12.5.2 Aggregate Change Points as Outliers

The sudden changes in aggregate local and global trends in the underlying data are often indicative of anomalous events in the data. Many methods also provide statistical ways of quantifying the level of the changes in the underlying data stream. One way of measuring concept drift is to use the concept of velocity density. The idea in velocity density estimation is to construct a density-based velocity profile of the data. This is analogous to the concepts of kernel density estimation in static data sets. The kernel density estimation $\hat{f}(X)$ for n data points and kernel function $K_{h}^{i}( \cdot )$ is defined as follows:

$$
f(X) = \frac{1}{n} \sum_{i=1}^{n} K_{h}^{i}(X - X_{i})
$$

The kernel function used is a Gaussian kernel with width $h$.

$$
K_{h}^{i}(X - X_{i}) \propto e^{ - \| X - X_{i} \|^{2} / (2h^{2})}
$$

The estimation error is defined by the kernel width $h$ that is chosen in a data-driven manner based on Silverman's approximation rule [471].

The velocity density computations are performed over a temporal window of size $h_{t}$. Intuitively, the value of $h_{t}$ defines the time horizon over which the evolution is measured.
