
## 12.9 Exercises

1. Let $X$ be a random variable in $[0, 1]$ with mean of $0.5$. Show that $P(X > 0.9) \leq 5/9$.

2. Suppose the standard deviation of a random variable $X$ is $r$ times its mean. Here, $r$ can be any constant. Show how to combine the Chebychev inequality and Chernoff bound to show that repeated i.i.d. samples can be used to create a well-bounded estimate of $X$. In other words, we would like to create another random variable $Z$ (using the multiple i.i.d. samples) with the same expected value of $X$, such that for small $\delta$, we would like to show that:

$$
P(|Z - E[Z]| > \alpha \cdot E[Z]) \leq \delta
$$

(Hint: This is the "mean-median trick" discussed in the chapter.)

3. Discuss scenarios in which both the Hoeffding inequality and the Chernoff bound can be used. Which one applies more generally?

4. Suppose that you have a reservoir of size $k = 1000$, and you have a sample of a stream containing an exactly equal distribution of two classes. Use the upper-tail Chernoff bound to determine the probability that the reservoir contains more than 600 samples of one of the two classes. Can the lower tail be used?

5. (Difficult) Work out the full proof of the biased reservoir sampling algorithm.

6. (Difficult) Work out the proof of correctness of the dot-product estimate obtained with the use of the count-min sketch.

7. Discuss the generality of different synopsis construction methods to various stream mining problems. Why is it difficult to apply these methods to outlier analysis?

8. Implement the CluStream algorithm.

9. Extend the implementation of the previous exercise to the problem of classification with the microclustering method.

10. Implement the Flajolet–Martin algorithm for distinct element counting.
