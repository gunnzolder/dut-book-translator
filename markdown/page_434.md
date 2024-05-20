
A major limitation of the STREAM algorithm is that it is not particularly sensitive
to evolution in the underlying data stream. In many cases, the patterns in the underlying
stream may evolve and change significantly. Therefore, it is critical for the clustering process
to be able to adapt to such changes and provide insights over different time horizons. In this
sense, the CluStream algorithm is able to provide significantly better insights at different
levels of temporal granularity.

## 12.4.2 CluStream Algorithm

The concept drift in an evolving data stream changes the clusters significantly over time.
The clusters over the past day are very different from the clusters over the past month. In
many data mining applications, analysts may wish to have the flexibility to determine the
clusters based on one or more time horizons, which are unknown at the beginning of the
stream clustering process. Because stream data naturally imposes a one-pass constraint on
the design of the algorithms, it is difficult to compute clusters over different time horizons
using conventional algorithms. A direct extension of the STREAM algorithm to such a
case would require the simultaneous maintenance of the intermediate results of clustering
algorithms over all possible time horizons. The computational burden of such an approach
increases with progression of the data stream and can rapidly become a bottleneck for online
implementation.

A natural approach to address this issue is to apply the clustering process with a two-
stage methodology, including an online microclustering stage, and an offline macroclustering
stage. The online microclustering stage processes the stream in real time to continuously
maintain summarized but detailed cluster statistics of the stream. These are referred to
as microclusters. The offline macroclustering stage further summarizes these detailed clus-
ters to provide the user with a more concise understanding of the clusters over different
time horizons and levels of temporal granularity. This is achieved by retaining sufficiently
detailed statistics in the microclusters, so that it is possible to re-cluster these detailed
representations over user-specified time horizons.

### 12.4.2.1 Microcluster Definition

It is assumed that the multidimensional records in the data stream are denoted by
$X_1 . . . X_k . . .$, arriving at time stamps $T_1 . . . T_k . . .$. Each $X_i$ is a multidimensional record
containing $d$ dimensions that are denoted by $X_i = (x_i^1 . . . x_i^d)$. The microclusters capture
summary statistics of the data stream to facilitate clustering and analysis over different
time horizons. These summary statistics are defined by the following structures:

1. **Microclusters**: The microclusters are defined as a temporal extension of the cluster
feature vector used in the BIRCH algorithm of Chap. 7. This concept can be viewed
as a temporally optimized representation of the CF-vector specifically designed for the
streaming scenario. To achieve this goal, the microclusters contain temporal statistics
in addition to the feature statistics.

2. **Pyramidal Time Frame**: The microclusters are stored at snapshots in time that follow
a pyramidal pattern. This pattern provides an effective trade-off between the storage
requirements and the ability to recall summary statistics from different time horizons.
This is important for enabling the ability to re-cluster the data over different time
horizons.

Microclusters are defined as follows.
