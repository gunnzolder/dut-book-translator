
probabilistic interpretability. By examining the probability values in each column of $P_k$, one
can immediately infer the topical words of the corresponding aspect. This is not possible
in LSA, where the entries in the corresponding matrix $P_k$ do not have clear probabilistic
significance and may even be negative. One advantage of LSA is that the transformation can
be interpreted in terms of the rotation of an orthonormal axis system. In LSA, the columns
of $P_k$ are a set of orthonormal vectors representing this rotated basis. This is not the case
in PLSA. Orthogonality of the basis system in LSA enables straightforward projection of
out-of-sample documents (i.e., documents not included in $D$) onto the new rotated axis
system.
Interestingly, as in SVD/LSA, the latent properties of the transpose of the document
matrix are revealed by PLSA. Each row of $P_k \sum_k$ can be viewed as the transformed coordi-
nates of the vertical or inverted list representation (rows of the transpose) of the document
matrix $D$ in the basis space defined by columns of $Q_k$. These complementary properties
are illustrated in Fig. 13.4. PLSA can also be viewed as a kind of nonnegative matrix
factorization method (cf. Sect. 6.8 of Chap. 6) in which matrix elements are interpreted
as probabilities and the maximum-likelihood estimate of a generative model is maximized
rather than minimizing the Frobenius norm of the error matrix.
An example of an approximately optimal PLSA matrix factorization of a toy $6 \times 6$ exam-
ple, with 6 documents and 6 words, is illustrated in Fig. 13.5. This example is the same
(see Fig. 6.22) as the one used for nonnegative matrix factorization (NMF) in Chap. 6.
Note that the factorizations in the two cases are very similar except that all basis vectors
