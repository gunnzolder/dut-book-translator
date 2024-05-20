
each time series is treated as a unit, whereas temporal correlations are much weaker for 
multidimensional data. This chapter will address only multidimensional streaming outlier 
detection, whereas time-series methods will be addressed in Chap. 14.

The multidimensional stream scenario is similar to static multidimensional outlier anal-
ysis. The only difference is the addition of a temporal component to the analysis, though 
this temporal component is much weaker than in the case of time series data. In the context 
of multidimensional data streams, efficiency is an important concern because the outliers 
need to be discovered quickly. There are two kinds of outliers that may arise in the context 
of multidimensional data streams.

1. One is based on the outlier detection of individual records. For example, a first news 
   story on a specific topic represents an outlier of this type. Such an outlier is also 
   referred to as a novelty.

2. The second is based on changes in the aggregate trends of the multidimensional data. 
   For example, an unusual event such as a terrorist attack may lead to a burst of 
   news stories on a specific topic. This represents an aggregated outlier based on a 
   specific time window. The second kind of change point almost always begins with an 
   individual outlier of the first type. However, an individual outlier of the first type 
   may not always develop into an aggregate change point. This is closely related to the 
   concept of concept drift. While concept drift is generally gentle, an abrupt change 
   may be viewed as an outlier instant in time rather than an outlier data point.

Both kinds of outliers (or change points) will be discussed in this section.

## 12.5.1 Individual Data Points as Outliers

The problem of detecting individual data points as outliers is closely related to the problem 
of unsupervised novelty detection, especially when the entire history of the data stream is 
used. This problem is studied extensively in the text domain in the context of the problem 
of first story detection. Such novelties are often trend setters and may eventually become a 
part of the normal data. However, when an individual record is declared an outlier in the 
context of a window of data points, it may not necessarily be a novelty. In this context, 
proximity-based algorithms are particularly easy to generalize to the incremental scenario 
by almost direct applications of the corresponding algorithms to the window of data points.

Distance-based algorithms can be easily generalized to the streaming scenario. The orig-
inal distance-based definition of outliers is modified in the following way:

*The outlier score of a data point is defined in terms of its k-nearest neighbor distance 
to data points in a time window of length $W$.*

Note that this is a relatively straightforward modification of the original distance-based 
definition. When the entire window of data points can be maintained in main memory, it 
is fairly easy to determine the outliers by computing the score of every data point in the 
window. However, incremental maintenance of the scores of data points is more challenging 
because of the addition and removal of data points from the window. Furthermore, some 
algorithms such as LOF require the re-computation of statistics such as reachability dis-
tances. The LOF algorithm has been extended to the incremental scenario. Two steps are 
performed in the process:
