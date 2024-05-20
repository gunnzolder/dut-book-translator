
Table 12.2: An example [39] of snapshots stored for $\alpha = 2$ and $l = 2$

| Order of Snapshots | Clock times (last five snapshots) |
|--------------------|-----------------------------------|
| 0                  | 55 54 53 52 51                    |
| 1                  | 54 52 50 48 46                    |
| 2                  | 52 48 44 40 36                    |
| 3                  | 48 40 32 24 16                    |
| 4                  | 48 32 16                          |
| 5                  | 32                                |

[illustration, page 416]

Figure 12.7: Recent snapshots are stored more frequently by pyramidal time frame

To illustrate the snapshots, an example will be used. Consider the case when the stream has been running starting at a clock time of 1, and a use of $\alpha = 2$ and $l = 2$. Therefore, $2^2 + 1 = 5$ snapshots of each order are stored. Then, at a clock time of 55, snapshots at the clock times illustrated in Table 12.2 are stored. While some snapshots are redundant in this case, they are not stored in a redundant way. The corresponding pattern of storage is illustrated in Fig. 12.7. It is evident that recent snapshots are stored more frequently in the pyramidal pattern of storage.

The following observations are true at any moment in time over the course of the data stream:

- The maximum order of any snapshot stored at $T$ time units since the beginning of the stream mining process is $\log_{\alpha}(T)$.
- The maximum number of snapshots maintained at $T$ time units since the beginning of the stream mining process is $(\alpha^l + 1) \cdot \log_{\alpha}(T)$.
- For any user-specified time horizon $h$, at least one stored snapshot can be found, which corresponds to a horizon of length within a factor $(1 + 1/\alpha^{l-1})$ units of the desired value $h$. This property is important because the microcluster statistics of time horizon $(t_c - h, t_c)$ can be constructed by subtracting the statistics at time $(t_c - h)$ from those at time $t_c$. Therefore, the microcluster within the approximate temporal locality of $(t_c - h)$ can be used instead. This enables the approximate clustering of data stream points within an arbitrary time horizon $(t_c - h, t_c)$ from the stored pyramidal pattern of microcluster statistics.

For larger values of $l$, the time horizon can be approximated as closely as desired. It is instructive to use an example to illustrate the combination of the effectiveness and compactness achieved by the pyramidal pattern of snapshot storage. For example, by choosing
