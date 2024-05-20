
Thus, if $h_t$ is chosen to be large, then the velocity density estimation technique provides long term trends, whereas if $h_t$ is chosen to be small then the trends are relatively short term. This provides the user flexibility in analyzing the changes in the data over different time horizons. In addition, a spatial smoothing parameter $h_s$ is used that is analogous to the kernel width $h$ in conventional kernel density estimation.

Let $t$ be the current instant and $S$ be the set of data points that have arrived in the time window $(t - h_t, t)$. The rate of increase in density at spatial location $\mathbf{X}$ and time $t$ is estimated with two measures the forward time-slice density estimate and the reverse time-slice density estimate. Intuitively, the forward time-slice estimate measures the density function for all spatial locations at a given time $t$ based on the set of data points that have arrived in the past time window $(t - h_t, t)$. Similarly, the reverse time-slice estimate measures the density function at a given time $t$ based on the set of data points that will arrive in the future time window $(t, t + h_t)$. Obviously, this value cannot be computed until these points have actually arrived.

It is assumed that the $i$th data point in $S$ is denoted by $(\mathbf{X}_i, t_i)$, where $i$ varies from 1 to $|S|$. Then, the forward time-slice estimate $F_{(h_s, h_t)} (\mathbf{X}, t)$ of the set $S$ at the spatial location $\mathbf{X}$ and time $t$ is given by:

$$
F_{(h_s, h_t)} (\mathbf{X}, t) = C_f \cdot \sum_{i=1}^{|S|} K_{(h_s, h_t)} (\mathbf{X} - \mathbf{X}_i, t - t_i).
$$

Here $K_{(h_s, h_t)}(\cdot, \cdot)$ is a spatiotemporal kernel smoothing function, $h_s$ is the spatial kernel vector, and $h_t$ is temporal kernel width. The kernel function $K_{(h_s, h_t)} (\mathbf{X} - \mathbf{X}_i, t - t_i)$ is a smooth distribution that decreases with increasing value of $t - t_i$. The value of $C_f$ is a suitably chosen normalization constant, so that the entire density over the spatial plane is one unit. Thus, $C_f$ is defined as follows:

$$
\int_{\text{All } \mathbf{X}} F_{(h_s, h_t)} (\mathbf{X}, t) d\mathbf{X} = 1.
$$

The reverse time-slice density estimate is calculated differently from the forward time-slice density estimate. Assume that the set of points in the time interval $(t, t + h_t)$ is denoted by $U$. As before, the value of $C_r$ is chosen as a normalization constant. Correspondingly, the reverse time-slice density estimate $R_{(h_s, h_t)} (\mathbf{X}, t)$ is defined as follows:

$$
R_{(h_s, h_t)} (\mathbf{X}, t) = C_r \cdot \sum_{i=1}^{|U|} K_{(h_s, h_t)} (\mathbf{X} - \mathbf{X}_i, t_i - t).
$$

In this case, $t_i - t$ is used in the argument instead of $t - t_i$. Thus, the reverse time-slice density in the interval $(t, t + h_t)$ would be exactly the same as the forward time-slice density, if time were reversed, and the data stream arrived in reverse order, starting at $t + h_t$ and ending at $t$.

The velocity density $V_{(h_s, h_t)} (\mathbf{X}, T)$ at spatial location $\mathbf{X}$ and time $T$ is defined as follows:

$$
V_{(h_s, h_t)} (\mathbf{X}, T) = \frac{F_{(h_s, h_t)} (\mathbf{X}, T) - R_{(h_s, h_t)} (\mathbf{X}, T - h_t)}{h_t}.
$$

Note that the reverse time-slice density estimate is defined with a temporal argument of $(T - h_t)$, and therefore the future points with respect to $(T - h_t)$ are known at time $T$. A
