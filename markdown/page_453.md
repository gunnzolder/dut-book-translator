
The Jaccard coefficient is rarely used for the text domain, but it is used very commonly for
sparse binary data as well as sets. Many forms of transaction and market basket data use the
Jaccard coefficient. It needs to be pointed out that the transaction and market basket data
share many similarities with text because of their sparse and nonnegative characteristics.
Most text mining techniques discussed in this chapter can also be applied to these domains
with minor modifications.

### 13.2.2 Specialized Preprocessing for Web Documents

Web documents require specialized preprocessing techniques because of some common prop-
erties of their structure, and the richness of the links inside them. Two major aspects of
Web document preprocessing include the removal of specific parts of the documents (e.g.,
tags) that are not useful, and the leveraging of the actual structure of the document. HTML
tags are generally removed by most preprocessing techniques.

HTML documents have numerous fields in them, such as the title, the metadata, and the
body of the document. Typically, analytical algorithms treat these fields with different levels
of importance, and therefore weigh them differently. For example, the title of a document is
considered more important than the body and is weighted more heavily. Another example
is the anchor text in Web documents. Anchor text contains a description of the Web page
pointed to by a link. Due to its descriptive nature, it is considered important, but it is
sometimes not relevant to the topic of the page itself. Therefore, it is often removed from
the text of the document. In some cases, where possible, anchor text could even be added to
the text of the document to which it points. This is because anchor text is often a summary
description of the document to which it points.

A Web page may often be organized into content blocks that are not related to the
primary subject matter of the page. A typical Web page will have many irrelevant blocks,
such as advertisements, disclaimers, or notices, that are not very helpful for mining. It has
been shown that the quality of mining results improve when only the text in the main block
is used. However, the (automated) determination of main blocks from web-scale collections
is itself a data mining problem of interest. While it is relatively easy to decompose the
Web page into blocks, it is sometimes difficult to identify the main block. Most automated
methods for determining main blocks rely on the fact that a particular site will typically
utilize a similar layout for the documents on the site. Therefore, if a collection of documents
is available from the site, two types of automated methods can be used:

1. **Block labeling as a classification problem**: The idea in this case is to create a new
    training data set that extracts visual rendering features for each block in the training
    data, using Web browsers such as Internet Explorer. Many browsers provide an API
    that can be used to extract the coordinates for each block. The main block is then
    manually labeled for some examples. This results in a training data set. The resulting
    training data set is used to build a classification model. This model is used to identify
    the main block in the remaining (unlabeled) documents of the site.

2. **Tree matching approach**: Most Web sites generate the documents using a fixed tem-
    plate. Therefore, if the template can be extracted, then the main block can be identified
    relatively easily. The first step is to extract tag trees from the HTML pages. These
    represent the frequent tree patterns in the Web site. The tree matching algorithm,
    discussed in the bibliographic section, can be used to determine such templates from
    these tag trees. After the templates have been found, it is determined, which block
    is the main one in the extracted template. Many of the peripheral blocks often have
    similar content in different pages and can therefore be eliminated.
