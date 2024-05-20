
referred to as a string. Therefore, many sequence-mining methods discussed in Chap. 15 are 
theoretically applicable to text. However, such sequence mining methods are rarely used in 
the text domain. This is partially because sequence mining methods are most effective when 
the length of the sequences and the number of possible tokens are both relatively modest. 
On the other hand, documents can often be long sequences drawn on a lexicon of several 
hundred thousand words.

In practice, text is usually represented as multidimensional data in the form of frequency-
annotated bag-of-words. Words are also referred to as terms. Although such a representation 
loses the ordering information among the words, it also enables the use of much larger classes 
of multidimensional techniques. Typically, a preprocessing approach is applied in which the 
very common words are removed, and the variations of the same word are consolidated. The 
processed documents are then represented as an unordered set of words, where normalized 
frequencies are associated with the individual words. The resulting representation is also 
referred to as the vector space representation of text. The vector space representation of a 
document is a multidimensional vector that contains a frequency associated with each word 
(dimension) in the document. The overall dimensionality of this data set is equal to the 
number of distinct words in the lexicon. The words from the lexicon that are not present in 
the document are assigned a frequency of 0. Therefore, text is not very different from the 
multidimensional data type that has been studied in the preceding chapters.

Due to the multidimensional nature of the text, the techniques studied in the afore-
mentioned chapters can also be applied to the text domain with a modest number of mod-
ifications. What are these modifications, and why are they needed? To understand these 
modifications, one needs to understand a number of specific characteristics that are unique 
to text data:

1. Number of “zero” attributes: Although the base dimensionality of text data may be 
   of the order of several hundred thousand words, a single document may contain only 
   a few hundred words. If each word in the lexicon is viewed as an attribute, and the 
   document word frequency is viewed as the attribute value, most attribute values are 
   0. This phenomenon is referred to as high-dimensional sparsity. There may also be a 
   wide variation in the number of nonzero values across different documents. This has 
   numerous implications for many fundamental aspects of text mining, such as distance 
   computation. For example, while it is possible, in theory, to use the Euclidean function 
   for measuring distances, the results are usually not very effective from a practical 
   perspective. This is because Euclidean distances are extremely sensitive to the varying 
   document lengths (the number of nonzero attributes). The Euclidean distance function 
   cannot compute the distance between two short documents in a comparable way to 
   that between two long documents because the latter will usually be larger.

2. Nonnegativity: The frequencies of words take on nonnegative values. When combined 
   with high-dimensional sparsity, the nonnegativity property enables the use of special-
   ized methods for document analysis. In general, all data mining algorithms must be 
   cognizant of the fact that the presence of a word in a document is statistically more 
   significant than its absence. Unlike traditional multidimensional techniques, incorpo-
   rating the global statistical characteristics of the data set in pairwise distance compu-
   tation is crucial for good distance function design.

3. Side information: In some domains, such as the Web, additional side information is 
   available. Examples include hyperlinks or other metadata associated with the doc-
   ument. These additional attributes can be leveraged to enhance the mining process 
   further.
