# [Identifying Meaningful Citations](http://ai2-website.s3.amazonaws.com/publications/ValenzuelaHaMeaningfulCitations.pdf)

## Marco Valenzuela, Vu Ha, Oren Etzioni

## Abstract
We introduce the novel task of identifying important citations in scholarly literature, i.e., citations that indicate that the cited work is used or extended in the new effort. We believe this task is a crucial component in algorithms that detect and follow research topics and in methods that measure the quality of publications. We model this task as a supervised classification problem at two levels of detail: a coarse one with classes (important vs. non-important), and a more detailed one with four importance classes. We annotate a dataset of approximately 450 citations with this information, and release it publicly. ==We propose a supervised classification approach that addresses this task with a battery of features that range from citation counts to where the citation appears in the body of the paper, and show that, our approach achieves a precision of 65% for a recall of 90%.

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
- Scientific papers are usually distributed in Portable Document Format (PDF) without extensive semantic markup.
- Recent work demonstrates that document layout information can be used to enhance content extraction via large-scale, layout-aware pretraining (Xu et al, 2020, 2021; Li et al, 2021).
- These methods only consider individual tokens’ 2D positions and do not explicitly model high-level layout structures like the grouping of text into lines and blocks, limiting accuracy.
- Existing methods come with enormous computational costs: they rely on further pretraining an existing pretrained model like BERT (Devlin et al, 2019) on layout-enriched input, and achieving the best performance from the models requires more than a thousand (Xu et al, 2020) to several thousand (Xu et al, 2021) GPUhours
- This means swapping in a new pretrained text model or experimenting with new layout-aware architectures can be prohibitively expensive, incompatible with the goals of green AI (Schwartz et al, 2020)


### Objectives
- We aim to incorporate document layout features in the form of visual layout groupings, in novel ways that improve or match performance without the need for expensive pretraining


### Methods
- Following prior work (Tkaczyk et al, 2015; Li et al, 2020), our task is to map each token ti in an input sequence T =
- Input tokens are extracted via PDF-to-text tools, which output both the word ti and its 2D position on the page, a rectangular bounding box ai = (x0, y0, x1, y1) denoting the left, top, right, and bottom coordinate of the word.
- Scientific papers are organized into groups of tokens, which consist of consecutive pieces of text that can be segmented from other pieces based on spatial gaps.
- The group information can be extracted via visual layout detection models (Zhong et al, 2019; He et al, 2017) or rule-based PDF parsing (Tkaczyk et al, 2015)


### Results
- Compared to the baseline LayoutLM model, inserting layout indicators results in +1.13%, +1.90%, and +1.29% Macro F1 improvements across the three benchmark datasets.
I-VILA models achieve better token prediction consistency; the corresponding group category inconsistency is reduced by 32.1%, 21.7%, and 21.7% compared to baseline.

- As block-level models perform predictions directly at the text block level, the group category inconsistency is naturally zero.
- Compared to LayoutLM, H-VILA models with text lines brings a 46.59% reduction in inference time, without heavily pe-


### Conclusion
- We introduce two new ways to integrate Visual Layout (VILA) structures into the NLP pipeline for structured content extraction from scientific paper PDFs. We show that inserting special indicator tokens based on VILA (I-VILA) can lead to robust improvements in token classification accuracy and consistency.
- We design a hierarchical transformer model based on VILA (H-VILA), which can reduce inference time by 46% with less than 0.8% Macro F1 reduction compared to previous SOTA methods.
- These VILA-based methods can be incorporated into different BERT variants with only fine-tuning, achieving comparable performance against existing work with only 5% of the training cost.
- We ablate the influence of different visual layout detectors on VILA-based models, and provide suggestions for practical use.
- We release a benchmark suite, along with a newly curated dataset S2-VL, to systematically evaluate the proposed methods

## Study subjects

### 20527 papers
- Our method performs well, obtaining a precision of 65% for a recall of 90%. ==To address this task, we used a collection of 20,527 papers from the ACL anthology1, together with their citation graph. 1http://www.aclweb.org/anthology/

### 50 papers
- In this work we focus solely on the precision of the set of extracted descriptions, which are responsible for the indirect citations.6. ==For this purpose, we selected a subset of 50 papers from the larger corpus of +20K papers. 12 of these papers appear as cited papers in our smaller, annotated citation corpus==. For these 50 papers, we collected all the descriptions automatically extracted by our approach

### 50 papers
- For this purpose, we selected a subset of 50 papers from the larger corpus of +20K papers. 12 of these papers appear as cited papers in our smaller, annotated citation corpus. ==For these 50 papers, we collected all the descriptions automatically extracted by our approach==. The descriptions in this set total 119

## Data analysis
- #method/post_hoc_analysis
- #method/yarowsky_algorithm

## Findings
- We propose a supervised classification approach that addresses this task with a battery of features that range from citation counts to where the citation appears in the body of the paper, and show that, our approach achieves a precision of 65% for a recall of 90%

## Counterpoint to earlier claims
- There has been considerable effort in the past decade on citation indexing systems ([^Giles_et+al_1998_a]; [^Lawrence_et+al_1999_a]; [^Councill_et+al_2006_a]) and on algorithms that analyze these citation graphs to, e.g., understand the flow of research topics in the literature, model the influence of specific papers in their field, or recommend citations for a given topic; see, inter alia, ([^Dietz_et+al_2007_a]; [^Gruber_et+al_2008_a]; [^Nallapati_et+al_2008_a]; [^Daume_2009_a]; [^Sun_et+al_2009_a]; [^Wong_et+al_2009_a]; [^Nallapati_et+al_2011_a]). However, by and large, these works assume that all citations are important, which we dispute in our work.

## Contributions
- To our knowledge, this paper is among the first to tackle the important task of identifying important citations, which, we believe, will ultimately improve many applications that focus on tracking scholarly citations, such as detecting and following research trends, or quantitatively measuring the quality and impact of publications.<br/><br/>In addition to introducing and formalizing this task, our contributions include a novel dataset of 465 citation tuples, which is publicly available8. We also describe a supervised classification approach for identifying meaningful citations, which uses a battery of features ranging from citation counts to where the citation appears in the body of the paper. Using the previously described dataset, we show that our approach performs well, obtaining a precision of 0.65 for a high recall of 0.9.

## Limitations
- A remaining limitation of our approach is that we currently use unigrams and bigrams, which might not to be sufficient to capture longer descriptions. We analyze this issue later in the paper.

## Future work
- We annotate a dataset of approximately 450 citations with citation importance information. The dataset is publicly available in the hope that it will foster further research on this topic.
- In this work, we mitigate the latter issue by counting sentences rather than individual indirect citations. In future work, we will explore more complex solutions, such as n-gram tiling ([^Dumais_et+al_2002_a]), which combine multiple incomplete n-grams to form a complete description.
- This work is far from complete. In future work we will improve the extraction of the paper description and, correspondingly, of the indirect citations, by implementing tiling algorithms that merge incomplete descriptions. We will continue to improve the features used to represent a citation. We will explore different ways of normalizing citation counts, e.g., by dividing by the total number of references and/or citations in the citing paper. We will evaluate new features like the rhetorical function of citations ([^Teufel_et+al_2006_a]).
