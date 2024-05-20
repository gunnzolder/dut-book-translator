
of different $k$-medians style algorithms for this purpose. In $k$-medians algorithms, a set 
$\mathcal{Y}$ of $k$ representatives from each chunk $S_i$ is selected, and each point in $S_i$ is assigned to 
its closest representative. The goal is to select the representatives to minimize the sum of 
squared distances (SSQ) of the assigned data points to these representatives. For a set of 
$m$ data points $X_1 \ldots X_m$ in segment $S$, and a set of $k$ representatives $\mathcal{Y} = Y_1 \ldots Y_k$, the 
objective function is defined as follows:
$$
\text{Objective}(S, \mathcal{Y}) = \sum_{X_i \in S, X_i \overset{\leftarrow}{Y_j}} \text{dist}(X_i, Y_j). \tag{12.31}
$$
The assignment operator is denoted by $\overset{\leftarrow}{Y_j}$ above. The squared distance between a data 
point and its assigned cluster center is denoted by $\text{dist}(X_i, \overline{Y_j})$, where the data record $X_i$ is 
assigned to the representative $\overline{Y_j}$. In principle, any partitioning algorithm, such as $k$-means 
or $k$-medoids, can be applied to the segment $S_i$ in order to determine the representatives 
$\overline{Y_1} \ldots \overline{Y_k}$. For the purpose of discussion, this algorithm will be treated as a black box.

After the first segment $S_1$ has been processed, we now have a set of $k$ medians that are 
stored away. The number of points assigned to each representative is stored as a “weight” 
for that representative. Such representatives are considered level-1 representatives. The next 
segment $S_2$ is independently processed to find its $k$ optimal median representatives. Thus, 
at the end of processing the second segment, one will have $2 \cdot k$ such representatives. Thus, 
the memory requirement for storing the representatives also increases with time, and after 
processing $r$ segments, one will have a total of $r \cdot k$ representatives. When the number 
of representatives exceeds $m$, a second level of clustering is applied to these set of $r \cdot k$ 
points, except that the stored weights on the representatives are also used in the clustering 
process. The resulting representatives are stored as level-2 representatives. In general, when 
the number of representatives of level-$p$ reaches $m$, they are converted to $k$ level-$(p + 1)$ 
representatives. Thus, the process will result in increasing the number of representatives of 
all levels, though the number of representatives at higher levels will increase exponentially 
slower than those at the lower levels. At the end of processing the entire data stream (or 
when a specific need for the clustering result arises), all remaining representatives of different 
levels are clustered together in one final application of the $k$-medians subroutine.

The specific choice of the algorithm used for the $k$-medians problem is critical in ensuring 
a high-quality clustering. The other factor that affects the quality of the final output is the 
effect of the problem decomposition into chunks followed by hierarchical clustering. How 
does such a problem decomposition affect the final quality of the output? It has been shown 
in the STREAM paper [240], that the final quality of the output cannot be arbitrarily 
worse than the particular subroutine that is used at the intermediate stage for $k$-medians 
clustering.

#### Lemma 12.4.1
Let the subroutine used for $k$-medians clustering in the STREAM algorithm 
have an approximation factor of $c$. Then, the STREAM algorithm will have an approxima-
tion factor of no worse than $5 \cdot c$.

A variety of solutions are possible for the $k$-medians problem. In principle, virtually any 
approximation algorithm can be used as a black box. A particularly effective solution is 
based on the problem of facility location. The reader is referred to the bibliographic notes 
for pointers to the relevant approach.
