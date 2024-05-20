```
## 13.5.2.1 Multinomial Bayes Model

A more general approach is to use a multinomial Bayes model, in which the frequencies of the words are used explicitly. The Bernoulli model is helpful mostly for cases where the documents are short, and drawn over a lexicon of small size. In the general case of documents of longer sizes over a large lexicon, the multinomial model is more effective. Before discussing the multinomial model, the Bernoulli model (cf. Sect. 10.5.1 of Chap. 10) will be revisited in the context of text classification.

Let $C$ be the random variable representing the class variable of an unseen test instance, with $d$-dimensional feature values $X = (a_1, \ldots, a_d)$. For the Bernoulli model on text data, each value of $a_i$ is 1 or 0, depending on whether or not the $i$th word of the lexicon is present in the document $X$. The goal is to estimate the posterior probability $P(C = c|X = (a_1, \ldots, a_d))$. Let the random variables for the individual dimensions of $X$ be denoted by $X = (x_1, \ldots, x_d)$. Then, it is desired to estimate the conditional probability $P(C = c|x_1 = a_1, \ldots, x_d = a_d)$. Then, by using Bayes' theorem, the following equivalence can be inferred.

\[
P(C = c|x_1 = a_1, \ldots, x_d = a_d) = \frac{P(C = c)P(x_1 = a_1, \ldots, x_d = a_d|C = c)}{P(x_1 = a_1, \ldots, x_d = a_d)} \tag{13.17}
\]

\[
\propto P(C = c)P(x_1 = a_1, \ldots, x_d = a_d|C = c) \tag{13.18}
\]

\[
\approx P(C = c) \prod_{i=1}^{d} P(x_i = a_i|C = c). \tag{13.19}
\]

The last of the aforementioned relationships is based on the naive assumption of conditional independence. In the binary model discussed in Chap. 10, each attribute value $a_i$ takes on the value of 1 or 0 depending on the presence or the absence of a word. Thus, if the fraction of the documents in class $c$ containing word $i$ is denoted by $p(i, c)$, then the value of $P(x_i = a_i|C = c)$ is estimated as either $p(i, c)$ or $1 - p(i, c)$ depending upon whether $a_i$ is 1 or 0, respectively. Note that this approach explicitly penalizes nonoccurrence of words in documents. Larger lexicon sizes will result in many words that are absent in a document. Therefore, the Bernoulli model may be dominated by word absence rather than 
```
