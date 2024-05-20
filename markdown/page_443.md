```
achieved with the original data set with high probability. The Hoeffding bound is used to 
estimate this probability, and therefore the intermediate steps of the approach are designed 
with this bound in mind. This is the reason that such trees are referred to as Hoeffding trees.

The Hoeffding tree can be constructed incrementally by growing the tree simultaneously 
with stream arrival. An important assumption is that the stream does not evolve, and 
therefore the currently arrived set of points can be viewed as a sample of the full stream. 
The higher levels of the tree are constructed at earlier stages of the stream, when enough 
tuples have been collected to quantify the accuracy of the corresponding split criteria. The 
lower level nodes are constructed later because statistics about lower level nodes can be 
collected only after the higher level nodes have been constructed. Thus, successive levels of 
the tree are constructed, as more examples stream in and the tree continues to grow. The 
key in the Hoeffding tree algorithm is to quantify the point at which statistically sufficient 
tuples have been collected in order to perform a split, so that the split is approximately the 
same as what would have been performed with knowledge of the full stream.

The same decision tree will be constructed on the current stream sample and the full 
stream, as long as the same splits are used at each stage. Therefore, the goal of the approach 
is to ensure that the splits on the sample are identical to the splits on the full stream. For ease 
in discussion, consider the case where each attribute^6 is binary. In this case, two algorithms 
will produce exactly the same tree, as long as the same split attribute is selected at each 
point. The split attribute is selected using a measure such as the Gini index. Consider a 
particular node in the tree constructed on the original data, and the same node constructed 
on the sampled data. What is the probability that the same attribute will be selected for 
the stream sample as for the full stream?

Consider the best and second-best attributes for a split, indexed by $i$ and $j$, respectively, 
in the sampled data. Let $G_i$ and $G_i'$ be the Gini index values of the split attribute $i$, as 
computed on the full stream, and the sampled data, respectively. Because the attribute $i$ 
was selected for a split in the sampled data, it is evident that $G_i' < G_j'$. The problem is that 
the sampling might cause an error. In other words, for the original data, it might be the 
case that $G_j < G_i$. Let the difference $G_j' - G_i'$ between $G_j'$ and $G_i'$ be $\epsilon > 0$. If the number 
of samples $n$ for evaluating the split is large enough, then it can be shown with the use of 
the Hoeffding bound that the undesirable case where $G_j < G_i$ will not occur with at least a 
user-defined probability $1 - \delta$. The required value of $n$ would be a function of $\epsilon$ and $\delta$. In the 
context of data streams with continuously accumulating samples, the key is to wait for a 
large enough sample size $n$ before performing the split. In the Hoeffding tree, the Hoeffding 
bound is used to determine the value of $n$ in terms of $\epsilon$ and $\delta$ as follows:

$$
n = \frac{R^2 \cdot \ln(1/\delta)}{2 \epsilon^2}
\tag{12.32}
$$

The value of $R$ denotes the range of the split criterion. For the Gini index, the value of $R$ is 
1, and for the entropy criterion, the value is $\log(k)$, where $k$ is the number of classes. Near 
ties in the split criterion correspond to small values of $\epsilon$. According to Eq. 12.32, such ties 
will lead to large sample size requirements, and therefore a larger waiting time until one 
can be sufficiently confident of performing a split with the available stream sample.

The Hoeffding tree approach determines whether the current difference in the Gini index 
between the best and second-best split attributes is at least $\sqrt{\frac{R^2 \cdot \ln(1/\delta)}{2n}}$ in order to initiate 
a split. This provides a guarantee on the quality of a split at a particular node. In cases,
```
