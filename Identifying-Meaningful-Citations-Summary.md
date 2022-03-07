# [Identifying Meaningful Citations](http://ai2-website.s3.amazonaws.com/publications/ValenzuelaHaMeaningfulCitations.pdf)

## Marco Valenzuela, Vu Ha, Oren Etzioni

### 2014

## Abstract

We introduce the novel task of identifying important citations in scholarly literature, i.e., citations that indicate that the cited work is used or extended in the new effort. We believe this task is a crucial component in algorithms that detect and follow research topics and in methods that measure the quality of publications. We model this task as a supervised classification problem at two levels of detail: a coarse one with classes (important vs. non-important), and a more detailed one with four importance classes. We annotate a dataset of approximately 450 citations with this information, and release it publicly. We propose a supervised classification approach that addresses this task with a battery of features that range from citation counts to where the citation appears in the body of the paper, and show that, our approach achieves a precision of 65% for a recall of 90%.

## Key concepts

#support_vector_machines; #search_engine; #citation_indexing

## Key points

- Tracking citations is an important component of analyzing scholarly big data
- We propose a supervised classification approach that separates important from incidental citations using a battery of features, ranging from citation counts to where the citation appears in the body of the paper
- This paper is among the first to tackle the important task of identifying important citations, which, we believe, will improve many applications that focus on tracking scholarly citations, such as detecting and following research trends, or quantitatively measuring the quality and impact of publications
- We describe a supervised classification approach for identifying meaningful citations, which uses a battery of features ranging from citation counts to where the citation appears in the body of the paper
- Using the previously described dataset, we show that our approach performs well, obtaining a precision of 0.65 for a high recall of 0.9

## Synopsis

### Introduction

In this work we argue that not all citations are equal.
While some indicate that the cited work is used or, more importantly, extended in the new publication, some are less important, e.g., they discuss the cited work in the context of related work that does not directly impact the new effort.
We further argue that because current citation tracking algorithms do not distinguish between important vs incidental citations, all of the above applications are negatively affected

### Methods

- 0.6 svm random forest baseline models on a different citation, by training on all remaining ones.
- For this experiment, we used only the binary coarse labels, i.e., important vs incidental, and employed the standard precision, recall, and F1 scores as evaluation measures, considering the important citations as the positive class.
- To obtain the P/R curve, we used various thresholds on the classifier confidence.
- Both classifiers are compared against a baseline that randomly assigns the “important” label using a probability p, which varies from 0 to 1.
- The red dot in the figure corresponds to a value of p equal to the the prior distribution of the “important” label in the entire corpus (i.e., 14.6%)

### Findings

- We propose a supervised classification approach that addresses this task with a battery of features that range from citation counts to where the citation appears in the body of the paper, and show that, our approach achieves a precision of 65% for a recall of 90%

### Discussion

- One of the strengths of this work is its immediate applicability to a real-world problem.
- We have incorporated our citation classifier into a scientific literature search engine, such that users can immediately identify the most important followup work for a given cited paper.
- The example highlights that of the ten papers that cite the paper “The infinite HMM for unsupervised PoS tagging” only two are considered important and are shown first.
- In future work we will improve the extraction of the paper description and, correspondingly, of the indirect citations, by implementing tiling algorithms that merge incomplete descriptions.
- We will continue to improve the features used to represent a citation.
- We will explore different ways of normalizing citation counts, e.g., by dividing by the total number of references and/or citations in the citing paper.
- We will evaluate new features like the rhetorical function of citations ([^teufel_et+al_2006_a])

### Conclusion

- This paper is among the first to tackle the important task of identifying important citations, which, we believe, will improve many applications that focus on tracking scholarly citations, such as detecting and following research trends, or quantitatively measuring the quality and impact of publications.
- In addition to introducing and formalizing this task, our contributions include a novel dataset of 465 citation tuples, which is publicly available.
- We describe a supervised classification approach for identifying meaningful citations, which uses a battery of features ranging from citation counts to where the citation appears in the body of the paper.
- Using the previously described dataset, we show that our approach performs well, obtaining a precision of 0.65 for a high recall of 0.9

## Study subjects

### 20527 papers

- Our method performs well, obtaining a precision of 65% for a recall of 90%. To address this task, we used a collection of 20,527 papers from the ACL anthology1, together with their citation graph. 1http://www.aclweb.org/anthology/

### 50 papers

- For this purpose, we selected a subset of 50 papers from the larger corpus of +20K papers. 12 of these papers appear as cited papers in our smaller, annotated citation corpus. For these 50 papers, we collected all the descriptions automatically extracted by our approach. The descriptions in this set total 119

## Data analysis

- #method/post_hoc_analysis
- #method/yarowsky_algorithm

## Findings

- We propose a supervised classification approach that addresses this task with a battery of features that range from citation counts to where the citation appears in the body of the paper, and show that, our approach achieves a precision of 65% for a recall of 90%

## Counterpoint to earlier claims

- There has been considerable effort in the past decade on citation indexing systems ([^giles_et+al_1998_a]; [^lawrence_et+al_1999_a]; [^councill_et+al_2006_a]) and on algorithms that analyze these citation graphs to, e.g., understand the flow of research topics in the literature, model the influence of specific papers in their field, or recommend citations for a given topic; see, inter alia, ([^dietz_et+al_2007_a]; [^gruber_et+al_2008_a]; [^nallapati_et+al_2008_a]; [^daume_2009_a]; [^sun_et+al_2009_a]; [^wong_et+al_2009_a]; [^nallapati_et+al_2011_a]). However, by and large, these works assume that all citations are important, which we dispute in our work

## Contributions

- To our knowledge, this paper is among the first to tackle the important task of identifying important citations, which, we believe, will ultimately improve many applications that focus on tracking scholarly citations, such as detecting and following research trends, or quantitatively measuring the quality and impact of publications.<br/><br/>In addition to introducing and formalizing this task, our contributions include a novel dataset of 465 citation tuples, which is publicly available8. We also describe a supervised classification approach for identifying meaningful citations, which uses a battery of features ranging from citation counts to where the citation appears in the body of the paper. Using the previously described dataset, we show that our approach performs well, obtaining a precision of 0.65 for a high recall of 0.9.

## Limitations

- A remaining limitation of our approach is that we currently use unigrams and bigrams, which might not to be sufficient to capture longer descriptions. We analyze this issue later in the paper.

## Future work

- We annotate a dataset of approximately 450 citations with citation importance information. The dataset is publicly available in the hope that it will foster further research on this topic.
- In this work, we mitigate the latter issue by counting sentences rather than individual indirect citations. In future work, we will explore more complex solutions, such as n-gram tiling ([^dumais_et+al_2002_a]), which combine multiple incomplete n-grams to form a complete description.
- This work is far from complete. In future work we will improve the extraction of the paper description and, correspondingly, of the indirect citations, by implementing tiling algorithms that merge incomplete descriptions. We will continue to improve the features used to represent a citation. We will explore different ways of normalizing citation counts, e.g., by dividing by the total number of references and/or citations in the citing paper. We will evaluate new features like the rhetorical function of citations ([^teufel_et+al_2006_a]).
