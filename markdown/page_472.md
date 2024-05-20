
The optimization formulation (OP2) is different from (OP1) in that it has only one slack variable $\xi$ but $2^n$ constraints that represent the sum of every subset of constraints in (OP1). It can be shown that a one-to-one correspondence exists between the solutions of (OP1) and (OP2).

**Lemma 13.5.1** 
*A one-to-one correspondence exists between solutions of (OP1) and (OP2), with equal values of $W = W^*$ in both models, and $\xi^* = \frac{\sum_{i=1}^n \xi_i}{n}$.*

**Proof:** We will show that if the same value of $W$ is fixed for (OP1), and (OP2), then it will lead to the same objective function value. The first step is to derive the slack variables in terms of this value of $W$ for (OP1) and (OP2). For problem (OP1), it can be derived from the slack constraints that the optimal value of $\xi_i$ is achieved for $\xi_i = \max \{0, 1 - y_i W \cdot X_i \}$ in order to minimize the slack penalty. For the problem OP2, a similar result for $\xi$ can be obtained:

$$
\xi = \max_{u_1, \ldots, u_n} \left\{ \frac{\sum_{i=1}^n u_i}{n} - \frac{1}{n} \sum_{i=1}^n u_i y_i W \cdot X_i \right\}. \tag{13.24}
$$

Because this function is linearly separable in $u_i$, one can push the maximum inside the summation, and independently optimize for each $u_i$:

$$
\xi = \frac{1}{n} \sum_{i=1}^n \max_{u_i} u_i \left\{ \frac{1}{n} - \frac{1}{n} y_i W \cdot X_i \right\}. \tag{13.25}
$$

For optimality, the value of $u_i$ should be picked as 1 for only the positive values of $\left\{ \frac{1}{n} - \frac{1}{n} y_i W \cdot X_i \right\}$ and 0, otherwise. Therefore, one can show the following:

$$
\xi = \frac{1}{n} \sum_{i=1}^n \max \left\{ 0, \frac{1}{n} - \frac{1}{n} y_i W \cdot X_i \right\} \tag{13.26}
$$

$$
= \frac{1}{n} \sum_{i=1}^n \max \{0, 1 - y_i W \cdot X_i \} = \frac{\sum_{i=1}^n \xi_i}{n} \tag{13.27}
$$

This one-to-one correspondence between optimal values of $W$ in (OP1) and (OP2) implies that the two optimization problems are equivalent.

Thus, by determining the optimal solution to problem (OP2), it is possible to determine the optimal solution to (OP1) as well. Of course, it is not yet clear, why (OP2) is a better formulation than (OP1). After all, problem (OP2) contains an exponential number of constraints, and it seems to be intractable to even enumerate the constraints, let alone solve them.

Even so, the optimization formulation (OP2) does have some advantages over (OP1). First, a single slack variable measures the feasibility of all the constraints. This implies that all constraints can be expressed in terms of $(W, \xi)$. Therefore, if one were to solve the optimization problem with only a subset of the $2^n$ constraints and the remaining were satisfied to a precision of $\epsilon$ by $(W, \xi)$, then it is guaranteed that $(W, \xi + \epsilon)$ is feasible for the full set of constraints.

The key is to never use all the constraints explicitly. Rather, a small subset $\mathcal{WS}$ of the $2^n$ constraints is used as the working set. We start with an empty working set $\mathcal{WS}$. The corresponding optimization problem is solved, and the most violated constraint among the constraints not in $\mathcal{WS}$ is added to the working set. The vector $U$ for the most violated constraint is relatively easy to find. This is done by setting $u_i$ to 1, if $y_i W \cdot X_i < 1$, and 0 otherwise. Therefore, the iterative steps for adding to the working set $\mathcal{WS}$ are as follows:
