
Definition 12.4.1 A microcluster for a set of $d$-dimensional points $X_{i1}, \ldots, X_{in}$, with time stamps $T_{i1}, \ldots, T_{in}$ is the $(2 \cdot d + 3)$ tuple $(CF^{2x}, CF^{1x}, CF^2 t, CF^1 t, n)$, wherein $CF^{2x}$ and $CF^{1x}$ each correspond to a vector of $d$ entries. The definition of each of these entries is as follows:

1. For each dimension, the sum of the squares of the data values is maintained in $CF^{2x}$. Thus, $CF^{2x}$ contains $d$ values. The $p$-th entry of $CF^{2x}$ is equal to $\sum_{j=1}^{n} (x_p^j)^2$.

2. For each dimension, the sum of the data values is maintained in $CF^{1x}$. Thus, $CF^{1x}$ contains $d$ values. The $p$-th entry of $CF^{1x}$ is equal to $\sum_{j=1}^{n} x_p^j$.

3. The sum of the squares of the time stamps $T_{i1}, \ldots, T_{in}$ is maintained in $CF^2 t$.

4. The sum of the time stamps $T_{i1}, \ldots, T_{in}$ is maintained in $CF^1 t$.

5. The number of data points is maintained in $n$.

An important property of microclusters is that they are additive. In other words, the microclusters can be updated by purely additive operations. Note that each of the $2 \cdot d + 3$ components of the microcluster can be expressed as a linearly separable sum over the constituent data points in the microcluster. This is an important property for enabling the efficient maintenance of the microclusters in the online streaming scenario. When a data point $X_i$ is added to a microcluster, the corresponding statistics of the data point $X_i$ need to be added to each of the $(2 \cdot d + 3)$ components. Similarly, the microclusters for the stream period $(t_1, t_2)$ can be obtained by subtracting the microclusters at time $t_1$ from those at time $t_2$. This property is important for enabling the computation of the higher-level microclusters over an arbitrary time horizon $(t_1, t_2)$ from the microclusters stored at different times.

### 12.4.2.2 Microclustering Algorithm

The data stream clustering algorithm can generate approximate clusters in any user-specified length of history from the current instant. This is achieved by storing the microclusters at particular moments in the stream that are referred to as snapshots. At the same time, the current snapshot of microclusters is always maintained by the algorithm. The additive property can be used to extract microclusters from any time horizon. The macroclustering phase is applied to this representation.

The input to the algorithm is the number of microclusters, denoted by $k$. The online phase of the algorithm works in an iterative fashion, by always maintaining a current set of microclusters. Whenever a new data point $X_i$ arrives, the microclusters are updated to reflect the changes. Each data point either needs to be absorbed by a microcluster, or it needs to be put in a cluster of its own. The first preference is to absorb the data point into a currently existing microcluster. The distance of the data point to the current microcluster centroids $M_1, \ldots, M_k$ is determined. The distance value of the data point $X_i$ to the centroid of the microcluster $M_j$ is denoted by $\text{dist}(M_j, X_i)$. Because the centroid of the microcluster can be derived from the cluster feature vector, this distance value can be computed easily. The closest centroid $M_p$ is determined. The data point $X_i$ is assigned to its closest cluster $M_p$, unless it is deemed that the data point does not "naturally" belong to that (or any other) microcluster. In such cases, the data point $X_i$ needs to be assigned a (new) microcluster of its own. Therefore, before assigning a data point to a microcluster, it first needs to be decided whether it naturally belongs to its closest microcluster centroid $M_p$.
