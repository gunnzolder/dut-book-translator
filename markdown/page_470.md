
In the multinomial model, the $L$ terms in a document are treated as samples from a 
multinomial distribution. The total number of terms in the document (or document length) 
is denoted by $L = \sum_{j=1}^{d} a_i$. In this case, the value of $a_i$ is assumed to be the raw frequency 
of the term in the document. The posterior class probabilities of a test document with 
the frequency vector $(a_1 \ldots a_d)$ are defined and estimated using the following generative 
approach:

1. Sample a class $c$ with a class-specific prior probability.

2. Sample $L$ terms with replacement from the term distribution of the chosen class $c$. 
   The term distribution is defined using a multinomial model. The sampling process 
   generates the frequency vector $(a_1 \ldots a_d)$. All training and test documents are assumed 
   to be observed samples of this generative process. Therefore, all model parameters of 
   the generative process are estimated from the training data.

3. Test instance classification: What is the posterior probability that the class $c$ is 
   selected in the first generative step, conditional on the observed word frequency 
   $(a_1 \ldots a_d)$ in the test document?

When the sequential ordering of the $L$ different samples are considered, the number of 
possible ways to sample the different terms to result in the representation $(a_1 \ldots a_d)$ is given 
by $\frac{L!}{\prod_{i:a_i>0} a_i!}$. The probability of each of these sequences is given by $\prod_{i:a_i>0} p(i, c)^{a_i}$, by using 
the naive independence assumption. In this case, $p(i, c)$ is estimated as the fractional number 
of occurrences of word $i$ in class $c$ including repetitions. Therefore, unlike the Bernoulli 
model, repeated presence of word $i$ in a document belonging to class $c$ will increase $p(i, c)$. 
If $n(i, c)$ is the number of occurrences of word $i$ in all documents belonging to class $c$, then 
$p(i, c) = \frac{n(i, c)}{\sum_i n(i, c)}$. Then, the class conditional feature distribution is estimated as follows:

$$
P(x_1 = a_1, \ldots , x_d = a_d | C = c) \approx \frac{L!}{\prod_{i:a_i > 0} a_i !} \prod_{i:a_i > 0} p(i, c)^{a_i}.
\tag{13.20}
$$

Using the Bayes rule, the multinomial Bayes model computes the posterior probability for 
a test document as follows:

$$
P(C = c | x_1 = a_1, \ldots , x_d = a_d) \propto P(C = c) \cdot P(x_1 = a_1, \ldots , x_d = a_d | C = c)
\tag{13.21}
$$

$$
\approx P(C = c) \cdot \frac{L!}{\prod_{i:a_i > 0} a_i !} \prod_{i:a_i > 0} p(i, c)^{a_i}
\tag{13.22}
$$

$$
\propto P(C = c) \cdot \prod_{i:a_i > 0} p(i, c)^{a_i}.
\tag{13.23}
$$

The constant factor $\frac{L!}{\prod_{i:a_i > 0} a_i !}$ has been removed from the last condition because it is the 
same across all classes. Note that in this case, the product on the right-hand side only uses 
those words $i$, for which $a_i$ is strictly larger than 0. Therefore, nonoccurrence of words is 
ignored. In this case, we have assumed that each $a_i$ is the raw frequency of a word, which is 
an integer. It is also possible to use the multinomial Bayes model with the tf-idf frequency of 
a word, in which the frequency $a_i$ might be fractional. However, the generative explanation 
becomes less intuitive in such a case.
