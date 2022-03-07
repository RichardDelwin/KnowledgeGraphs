# [VILA: Improving Structured Content Extraction from Scientific PDFs Using Visual Layout Groups](https://arxiv.org/abs/2106.00676v3)

## Zejiang Shen, Kyle Lo, Lucy Lu Wang et al.

### 2021

## Abstract
Accurately extracting structured content from PDFs is a critical first step for NLP over scientific papers. Recent work has improved extraction accuracy by incorporating elementary layout information, e.g., each token's 2D position on the page, into language model pretraining. We introduce new methods that explicitly model VIsual LAyout (VILA) groups, i.e., text lines or text blocks, to further improve performance. In our I-VILA approach, we show that simply inserting special tokens denoting layout group boundaries into model inputs can lead to a 1.9% Macro F1 improvement in token classification. In the H-VILA approach, we show that hierarchical encoding of layout-groups can result in up-to 47% inference time reduction with less than 0.8% Macro F1 loss. Unlike prior layout-aware approaches, our methods do not require expensive additional pretraining, only fine-tuning, which we show can reduce training cost by up to 95%. Experiments are conducted on a newly curated evaluation suite, S2-VLUE, that unifies existing automatically-labeled datasets and includes a new dataset of manual annotations covering diverse papers from 19 scientific disciplines. Pre-trained weights, benchmark datasets, and source code are available at https://github.com/allenai/VILA.

## Key concepts
#finding/BERT; #portable_document_format; #claim/scientific_paper; #empirical_methods_in_natural_language_processing; #international_conference_on_document_analysis_and_recognition; #claim/R_CNN; #claim/semantic_scholar

## Key points
- Scientific papers are usually distributed in Portable Document Format (PDF) without extensive semantic markup
- I-VIsual LAyout (VILA) models achieve better token prediction consistency; the corresponding group category inconsistency is reduced by 32.1%, 21.7%, and 21.7% compared to baseline
- We report on the S2-VL dataset using two automated group detectors: the CERMINE PDF parser ([^Tkaczyk_et+al_2015_a]) and the Mask R-CNN vision model trained on the PubLayNet dataset ([^Zhong_et+al_2019_a])
- We introduce two new ways to integrate Visual Layout (VILA) structures into the NLP pipeline for structured content extraction from scientific paper PDFs
- We show that inserting special indicator tokens based on VILA (I-VILA) can lead to robust improvements in token classification accuracy and consistency
- We design a hierarchical transformer model based on VILA (H-VILA), which can reduce inference time by 46% with less than 0.8% Macro F1 reduction compared to previous SOTA methods

## Synopsis

### Introduction
- Scientific papers are usually distributed in Portable Document Format (PDF) without extensive semantic markup.
- Recent work demonstrates that document layout information can be used to enhance content extraction via large-scale, layout-aware pretraining (Xu et al, 2020, 2021; Li et al, 2021).
- These methods only consider individual tokens’ 2D positions and do not explicitly model high-level layout structures like the grouping of text into lines and blocks, limiting accuracy.
- Existing methods come with enormous computational costs: they rely on further pretraining an existing pretrained model like BERT ([^Devlin_et+al_2019_a]) on layout-enriched input, and achieving the best performance from the models requires more than a thousand (Xu et al, 2020) to several thousand (Xu et al, 2021) GPUhours
- This means swapping in a new pretrained text model or experimenting with new layout-aware architectures can be prohibitively expensive, incompatible with the goals of green AI (Schwartz et al, 2020)

### Objectives
- We aim to incorporate document layout features in the form of visual layout groupings, in novel ways that improve or match performance without the need for expensive pretraining

### Methods
- Following prior work ([^Tkaczyk_et+al_2015_a]</a>; Li et al, 2020), our task is to map each token ti in an input sequence T =
Input tokens are extracted via PDF-to-text tools, which output both the word ti and its 2D position on the page, a rectangular bounding box ai = (x0, y0, x1, y1) denoting the left, top, right, and bottom coordinate of the word.
- Scientific papers are organized into groups of tokens, which consist of consecutive pieces of text that can be segmented from other pieces based on spatial gaps.
- The group information can be extracted via visual layout detection models ([^Zhong_et+al_2019_a]; [^He_et+al_2017_a]) or rule-based PDF parsing ([^Tkaczyk_et+al_2015_a]</a>)

### Results
- Compared to the baseline LayoutLM model, inserting layout indicators results in +1.13%, +1.90%, and +1.29% Macro F1 improvements across the three benchmark datasets.
- I-VILA models achieve better token prediction consistency; the corresponding group category inconsistency is reduced by 32.1%, 21.7%, and 21.7% compared to baseline.
- As block-level models perform predictions directly at the text block level, the group category inconsistency is naturally zero.
- Compared to LayoutLM, H-VILA models with text lines brings a 46.59% reduction in inference time, without heavily pe-

### Conclusion
- We introduce two new ways to integrate Visual Layout (VILA) structures into the NLP pipeline for structured content extraction from scientific paper PDFs. We show that inserting special indicator tokens based on VILA (I-VILA) can lead to robust improvements in token classification accuracy and consistency.
- We design a hierarchical transformer model based on VILA (H-VILA), which can reduce inference time by 46% with less than 0.8% - Macro F1 reduction compared to previous SOTA methods.
- These VILA-based methods can be incorporated into different BERT variants with only fine-tuning, achieving comparable performance against existing work with only 5% of the training cost.
- We ablate the influence of different visual layout detectors on VILA-based models, and provide suggestions for practical use.
- We release a benchmark suite, along with a newly curated dataset S2-VL, to systematically evaluate the proposed methods


## Study subjects

### 3 datasets
- To systematically evaluate the proposed methods, we develop the the Semantic Scholar Visual Layout-enhanced Scientific Text Understanding Evaluation (S2-VLUE) benchmark suite. S2VLUE consists of three datasets—two previously released resources which we augment with VILA information, and a new hand-curated dataset S2VL. Key statistics for S2-VLUE are provided in Table 1

### 3 constituent datasets
- Key statistics for S2-VLUE are provided in Table 1. Notably, the three constituent datasets differ with respect to their: 1) annotation method, 2) VILA generation method, and 3) paper domain coverage. We provide details below

### 87 papers
- The ground-truth VILA labels in S2-VL can be used to fine-tune visual layout detection models, and paper PDFs are also included, making PDF-based structure parsing feasible: this enables VILA annotations to be created by different means, which is helpful for benchmarking new VILA-based models. Moreover, S2-VL currently contains 1337 pages of 87 papers from 19 different disciplines, including e.g. Philosophy and Sociology which are not present in previous data sets. Overall, the datasets in S2-VLUE cover a wide range of academic disciplines with different layouts

## Findings
- In the H-VILA approach, we show that hierarchical encoding of layout-groups can result in up-to 47% inference time reduction with less than 0.8% Macro F1 loss
- Unlike prior layout-aware approaches, our methods do not require expensive additional pretraining, only fine-tuning, which we show can reduce training cost by up to 95%
- In this paper, we explore how to improve the accuracy and efficiency of structured content extraction from scientific documents by using VIsual LAyout (VILA) groups
- Given text lines or blocks generated by rule-based PDF parsers ([^Tkaczyk_et+al_2015_a]) or vision models ([^Zhong_et+al_2019_a]), we design two different methods to incorporate the VILA groups and the assumption into modeling: the I-VILA model adds layout indicator tokens to textual inputs to improve the accuracy of existing BERT-based language models, while the H-VILA model uses VILA structures to define a hierarchical model that models pages as collections of groups rather than of individual tokens, increasing inference efficiency
- The H-VILA model performs group-level predictions and can reduce model inference time by 47% with less than 0.8% loss in Macro F1
- The learning rate is linearly warmed up over 5% steps then linearly decayed
- As DocBank contains 4× examples, the number of DocBank models’ training epochs is reduced by 75%
- I-VILA models also achieve better token prediction consistency; the corresponding group category inconsistency is reduced by 32.1%, 21.7%, and 21.7% compared to baseline
- Compared to LayoutLM, H-VILA models with text lines brings a 46.59% reduction in inference time, without heavily penalizing the final prediction accuracies (-0.75%, +0.23%, +1.21% Macro F1)
- BERT+I-VILA achieves comparable accuracy to LayoutLM (0.00%, -0.89%, -1.05%), with only 5% of the training cost.11
- We design a hierarchical transformer model based on VILA (H-VILA), which can reduce inference time by 46% with less than 0.8% Macro F1 reduction compared to previous SOTA methods

##  Builds on previous research
- Following Zhong et al (2019) and [^Tkaczyk_et+al_2015_a]), our methods use the idea that a document page can be segmented into visual groups of tokens (either lines or blocks), and that the tokens within each group generally have the same semantic category, which we refer to as the group uniformity assumption (see Figure 1(b)). Given text lines or blocks generated by rule-based PDF parsers ([^Tkaczyk_et+al_2015_a]) or vision models ([^Zhong_et+al_2019_a]), we design two different methods to incorporate the VILA groups and the assumption into modeling: the I-VILA model adds layout indicator tokens to textual inputs to improve the accuracy of existing BERT-based language models, while the H-VILA model uses VILA structures to define a hierarchical model that models pages as collections of groups rather than of individual tokens, increasing inference efficiency
- The benchmark extends two existing resources ([^Tkaczyk_et+al_2015_a]; Li et al, 2020) and introduces a newly curated dataset, S2-VL, which contains high-quality human annotations for papers across 19 disciplines. Our contributions are as follows: 1. We introduce a new strategy for PDF content extraction that uses VILA structures to inject layout information into language models, and show that this improves accuracy without the expensive pretraining required by existing methods, and generalizes to different language models
- Our models then augment the base model to incorporate group structures, as detailed below. Following prior work ([^Tkaczyk_et+al_2015_a]; Li et al, 2020), our task is to map each token ti in an input sequence T = (t1, . . . , tn) to its semantic category ci (e.g. title, body text, reference, etc.)
- However, only a specific set of token tags is extracted from the main TEX file for each paper, leading to inaccurate and incomplete token labels, especially for papers employing LaTeX macro commands,5 and thus, incorrect visual groupings. Hence, we develop a Mask R-CNN-based vision layout detection model based on a collection of existing resources ([^Zhong_et+al_2019_a]; MFD, 2021; [^He_et+al_2017_a]; [^Shen_et+al_2021_a]) to fix these inaccuracies and generate trustworthy VILA annotations at both the text block and line level.6 As a result, this dataset can be used to evaluate VILA models under a different setting, since the VILA structures are generated independently from the token annotations
- 2. Sentence Breaks For I-VILA models, besides using VILA-based indicators, we also compare with indicators generated from sentence breaks detected by PySBD ([^Sadvilkar_2020_a])
- The results are shown in Table 6. We report on the S2-VL dataset using two automated group detectors: the CERMINE PDF parser ([^Tkaczyk_et+al_2015_a]) and the Mask R-CNN vision model trained on the PubLayNet dataset ([^Zhong_et+al_2019_a])

## Differs from previous work
- A MLP-based linear classifier is attached thereafter, and is trained to generate the group-level category probability pjc. Different from previous work ([^Yang_et+al_2020_a]), we restrict the choice of lg and lp to {1, 12} such that we can load pre-trained weights from BERT base models
- N Ls, it approximates as O(N 2/L2s). However, in our case, it is infeasible to adopt the Greedy Sentence Filling technique ([^Yang_et+al_2020_a]) as it mingles signals from different groups and obfuscates group structures

## Contributions
- In this paper, we introduce two new ways to integrate Visual Layout (VILA) structures into the NLP pipeline for structured content extraction from scientific paper PDFs. We show that inserting special indicator tokens based on VILA (I-VILA) can lead to robust improvements in token classification accuracy (up to +1.9% Macro F1) and consistency (up to -32% group category inconsistency). In addition, we design a hierarchical transformer model based on VILA (H-VILA), which can reduce inference time by 46% with less than 0.8% Macro F1 reduction compared to previous SOTA methods. These VILA-based methods can be easily incorporated into different BERT variants with only fine-tuning, achieving comparable performance against existing work with only 5% of the training cost. We ablate the influence of different visual layout detectors on VILA-based models, and provide suggestions for practical use. We release a benchmark suite, along with a newly curated dataset S2-VL, to systematically evaluate the proposed methods.

## Future work
- While we evaluate on scientific documents, related visual group structures exist in other kinds of documents, and adapting our techniques to those domains could offer improvements in corporate reports, historical archives, or legal documents, and this is an item of future work.

## Data and code
- The benchmark datasets, modeling code, and trained weights are available at https://github.com/allenai/VILA
- https://github.com/allenai/VILA
- https://github.com/kermitt2/pdfalto



## Figures
![Figure 1. a) Real-world scientific documents often have intricate layout structures, so analyzing only flattened raw text forfeits valuable information, yielding sub-optimal results. (b) The complex structures can be broken down into groups (text blocks or lines) that are composed of tokens with the same semantic category](https://engine.scholarcy.com/images/VILA.pdf_njua4ka4_images_fe07yoww/img-000.png)
![Figure 2. Comparing inserting indicator tokens [BLK] based on VILA groups and sentence boundaries. Indicators representing VILA groups (e.g., text blocks in the left figure) are usually consistent with the token category changes (illustrated by the background color in (a)), while sentence boundary indicators fail to provide helpful hints (both "false positive"s and "false negative"s occur frequently in (b)). Best viewed in color](https://engine.scholarcy.com/images/VILA.pdf_njua4ka4_images_fe07yoww/img-002.png)
![Figure 3. Illustration of the H-VILA model. Texts from each visual layout group are encoded separatedly using the group encoder, and the generated representation are subsequently modeled by a page encoder. The semantic category are predicted at the group-level, which significantly improves efficiency](https://engine.scholarcy.com/images/VILA.pdf_njua4ka4_images_fe07yoww/img-004.png)
![Figure 4. Model predictions for the 10th page of our paper draft. We present the token category and text block bounding boxes (highlighted in red rectangles) based on the (a) ground-truth annotations and model predictions from both I-VILA and H-VILA models (the three results happen to be identical) and (b) model predictions from the LayoutLM model. When VILA is injected, the model achieves more consistent predictions for the example, as indicated by arrows (1) and (2) in the figure. Best view in color](https://engine.scholarcy.com/images/VILA.pdf_njua4ka4_images_fe07yoww/img-006.png)
![Figure 5. Illustration of models trained and evaluated with incorrect text block detections (only the top half of the page is shown). The blocks are created by vision predictions, which fails to capture the correct caption text structure (arrow 1). Because the I-VILA model can generate different token predictions within a group, it maintains high accuracy, whereas H-VILA assigns the same category for all tokens in the incorrect block, leading to lower accuracy](https://engine.scholarcy.com/images/VILA.pdf_njua4ka4_images_fe07yoww/img-008.png)

## Tables
| - |        GROTOAP2        |    DocBank    |       S2-VL       |              -               |
|---|------------------------|---------------|-------------------|------------------------------|
|   |Train / Dev / Test Pages|83k / 18k / 18k|398k / 50k / 50k   |1.3k1                         |
|   |Annotation Method       |Automatic      |Automatic          |Human Annotation              |
|   |Scientific Discipline   |Life Science   |Math / Physics / CS|19 Disciplines                |
|   |Visual Layout Group     |PDF parsing    |Vision model       |Gold Label / Detection methods|
|   |Number of Categories    |22             |12                 |15                            |
|   |Average Token Count2    |1203 (591)     |838 (503)          |790 (453)                     |
|   |Average Text Line Count |90 (51)        |60 (34)            |64 (54)                       |
|   |Average Text Block Count|12 (16)        |15 (8)             |22 (36)                       |
|   |1                       |               |                   |                              |
# Table 1: Details for the three datasets in the S2-VLUE benchmark.
| the PAWLS annotation tool (Neumann et al., 2021),  |                                     Hutter, 2019) is adopted with a 5 × 10−5 learning                                     |  -   |    -     |  -   |    -     |           -           |    -     |
|----------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|------|----------|------|----------|-----------------------|----------|
|annotators draw rectangular text blocks directly on |rate and (β1 , β2 ) = (0.9, 0.999). The learning                                                                           |      |          |      |          |                       |          |
|each PDF page, and specify the block-level seman-   |rate is linearly warmed up over 5% steps then                                                                              |      |          |      |          |                       |          |
|tic categories from 15 possible candidates.7 Tokens |linearly decayed. For all datasets (GROTOAP2,                                                                              |      |          |      |          |                       |          |
|within a group can therefore inherit the category   |DocBank, S2-VL), unless otherwise specified, we                                                                            |      |          |      |          |                       |          |
|from the parent text block. Inter-annotator agree-  |select the best fine-tuning batch size (40, 40 and                                                                         |      |          |      |          |                       |          |
|ment, in terms of token-level accuracy measured on  |12) and training epochs (24, 6,8 and 10) for all                                                                           |      |          |      |          |                       |          |
|a 12-paper subset, is high at 0.95. The ground-truth|models. As for S2-VL, given its smaller size, we                                                                           |      |          |      |          |                       |          |
|VILA labels in S2-VL can be used to fine-tune       |use 5-fold cross validation and report averaged                                                                            |      |          |      |          |                       |          |
|visual layout detection models, and paper PDFs are  |scores, and use 2 × 10−5 learning rate with 20                                                                             |      |          |      |          |                       |          |
|also included, making PDF-based structure pars-     |epochs. We split S2-VL based on papers rather                                                                              |      |          |      |          |                       |          |
|ing feasible: this enables VILA annotations to be   |than pages to avoid exposing paper templates of                                                                            |      |          |      |          |                       |          |
|created by different means, which is helpful for    |test samples in the training data. Mixed precision                                                                         |      |          |      |          |                       |          |
|benchmarking new VILA-based models. More-           |training (Micikevicius et al., 2018) is used to speed                                                                      |      |          |      |          |                       |          |
|over, S2-VL currently contains 1337 pages of 87     |up the training process.                                                                                                   |      |          |      |          |                       |          |
|papers from 19 different disciplines, including e.g.|For I-VILA models, we fine-tune several BERT-                                                                              |      |          |      |          |                       |          |
|Philosophy and Sociology which are not present in   |variants with VILA-enhanced text inputs, and the                                                                           |      |          |      |          |                       |          |
|previous data sets.                                 |models are initialized from pre-trained weights                                                                            |      |          |      |          |                       |          |
|                                                    |Macro F1                                                                                                                  |H(G) |Macro F1 |H(G) |Macro F1 |H(G)                  |          |
|                                                    |LayoutLMBASE (Xu et al., 2020)                                                                                             | 92.34|      0.78| 91.06|      2.64|82.69(6.04)            |4.19(0.25)|
|                                                    |LayoutLMBASE + Sentence Breaks                                                                                             | 91.83|      0.78| 91.44|      2.62|82.81(5.21)            |4.21(0.55)|
|                                                    |LayoutLMBASE + I-VILA(Text Line)                                                                                           | 92.37|      0.73| 92.79|      2.17|83.77(5.75)2 3.28(0.35)|          |
|                                                    |LayoutLMBASE + I-VILA(Text Block)                                                                                          | 93.38|      0.53|    92|      2.10|83.44(6.48)            |2.83(0.34)|
|                                                    |1 For S2-VL, we show averaged scores with standard deviation in parentheses across the 5-fold cross validation subsets.    |      |          |      |          |                       |          |
|                                                    |2 In this table, we report S2-VL results using VILA structures detected by visual layout models. When the ground-truth VILA|      |          |      |          |                       |          |
# Table 2: Performance of baseline and I-VILA models on the scientific document extraction task. I-VILA provides
|consistent accuracy improvements over the baseline LayoutLM model on all three benchmark datasets.|                                                                   -                                                                    |  -   |    -     |  -   |    -     |     -     |         -         |     -      |
|--------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|------|----------|------|----------|-----------|-------------------|------------|
|                                                                                                  |Macro F1                                                                                                                               |H(G) |Macro F1 |H(G) |Macro F1 |H(G)      |Inference Time (ms)|            |
|                                                                                                  |LayoutLMBASE                                                                                                                            |92.34 |0.78      |91.06 |2.64      |82.69(6.04)|4.19(0.25)         |52.56(0.25) |
|Simple Group Classifier                                                                           |92.65                                                                                                                                   |0.00  |87.01     |0.00  |-1        |-          |82.57(0.30)        |            |
|                                                                                                  |H-VILA(Text Line)                                                                                                                       |91.65 |0.32      |91.27 |1.07      |83.69(2.92)|1.70(0.68)         |28.07(0.37)2|
|                                                                                                  |H-VILA(Text Block)                                                                                                                      |92.37 |0.00      |87.78 |0.00      |82.09(5.89)|0.36(0.12)         |16.37(0.15) |
|                                                                                                 1|The simple group classifier fails to converge for one run. We do not report the results for fair comparison.                            |      |          |      |          |           |                   |            |
|                                                                                                 2|When reporting efficiency in other parts of the paper, we use this result because of its optimal combination of accuracy and efficiency.|      |          |      |          |           |                   |            |
# Table 3: Content extraction performance for H-VILA. The H-VILA models significantly reduce the inference time
|cost compared to LayoutLM, while achieving comparable accuracy on the three benchmark datasets.|    -     |   -    |      -       |       -       |
|-----------------------------------------------------------------------------------------------|----------|--------|--------------|---------------|
|                                                                                               |Base Model|Baseline|Text Line G(L)|Text Block G(B)|
|                                                                                               |DistilBERT|90.52   |91.14         |92.12          |
|                                                                                               |BERT      |90.78   |91.65         |92.31          |
|                                                                                               |RoBERTa   |91.64   |92.04         |92.52          |
|                                                                                               |LayoutLM  |92.34   |92.37         |93.38          |
# Table 4: Content extraction performance (Macro F1
|on the GROTOAP2 dataset) for I-VILA using different|              -               |  -   |  -  |  -   |     -     |           -           |        -        |        -        |
|---------------------------------------------------|------------------------------|------|-----|------|-----------|-----------------------|-----------------|-----------------|
|                                                   |F1                           |H(G) |F1  |H(G) |F1        |H(G)                  |Training Cost1   |                 |
|                                                   |BERTBASE (Devlin et al., 2019)|90.78 |1.58 |87.24 |3.50       |78.34(6.53)1 7.17(0.95)|40 hr fine-tuning|                 |
|                                                   |BERTBASE + I-VILA(Text Line)  |91.65 |1.13 |90.25 |2.56       |81.15(4.83)            |4.76(1.28)       |40 hr fine-tuning|
| BERTBASE + I-VILA(Text Block)                     |92.31                         |0.63  |89.49|2.25  |81.82(4.88)|3.65(0.26)             |40 hr fine-tuning|                 |
|                                                   |1.2k hr pretraining           |      |     |      |           |                       |                 |                 |
|                                                   |LayoutLMBASE (Xu et al., 2020)|92.34 |0.78 |91.06 |2.64       |82.69(6.04)            |4.19(0.25)       |                 |
|                                                   |+ 50 hr fine-tuning           |      |     |      |           |                       |                 |                 |
|                                                   |9.6k hr pretraining3          |      |     |      |           |                       |                 |                 |
|LayoutLMv2BASE (Xu et al., 2021)                   |-2                            |-     |93.33|1.93  |83.05(4.51)|3.34(0.82)             |                 |                 |
# Table 5: Comparison between I-VILA models and other layout-aware methods that require expensive pretraining.
|I-VILA achieves comparable accuracy with less than 5% of the training cost.|               -               |                          -                           |               -               |     -     |     -     |     -     |     -     |    -     |
|--------------------------------------------------------------------------:|-------------------------------|------------------------------------------------------|-------------------------------|-----------|-----------|-----------|-----------|----------|
|                                                                        7.0|Ablation Studies               |                                                     8|VILA in Practice: The Impact of|           |           |           |           |          |
|                                                                           |Layout Group Detectors         |                                                      |                               |           |           |           |           |          |
|                                                                        7.1|I-VILA is Effective Across BERT|Applying VILA methods in practice requires run-       |                               |           |           |           |           |          |
|                                                                           |Variants                       |ning a group layout detector as a critical first step.|                               |           |           |           |           |          |
|                                                                           |Experiment                     |Group Source                                          |Max Macro F1                   |H(G)       |Macro F1   |H(G)       |Macro F1   |H(G)      |
|                                                                           |Ground-Truth                   |100.00(0.00)                                          |0.00(0.00)                     |86.50(4.52)|1.86(0.29) |85.91(3.13)|0.35(0.19) |          |
|                                                                           |Varying GB                     |Vision Model                                          |99.31(0.23)                    |1.09(0.30) |83.44(6.48)|2.83(0.34) |82.09(5.89)|0.36(0.12)|
|                                                                           |PDF Parsing                    |96.91(1.09)                                           |2.06(0.86)                     |83.95(4.45)|3.93(0.93) |78.69(4.90)|0.02(0.01) |          |
|                                                                           |Vision Model                   |99.57(0.13)                                           |0.42(0.18)1                    |83.77(5.75)|1.20(0.16) |83.69(2.92)|0.20(0.12) |          |
|                                                                           |Varying GL                     |                                                      |                               |           |           |           |           |          |
|                                                                           |PDF Parsing                    |99.70(0.12)                                           |0.38(0.26)                     |82.97(5.56)|1.28(0.13) |82.61(4.10)|0.00(0.00) |          |
# Table 6: VILA model performance when using different layout group detectors for text blocks G(B) and lines G(L)
|      on the S2-VL dataset.      |    -     |      -       |     -     |    -    |   -    |  -   |   -    |   -    |
|---------------------------------|----------|--------------|-----------|---------|--------|------|--------|--------|
|                                 |Author    |Bib           |Body       |Conflict |        |      |        |        |
|                                 |Abstract  |Acknowledgment|Affiliation|Author   |        |      |        |        |
|                                 |Title     |Info          |Content    |Statement|        |      |        |        |
|BERTBASE                         |97.42     |95.83         |96.12      |96.91    |   96.09|    95|   98.80|   88.66|
|BERTBASE + I-VILA(Text Line)     |97.65     |95.89         |96.61      |97.17    |   96.48| 95.78|   98.93|   88.28|
|BERTBASE + I-VILA(Text Block)    |97.67     |96.46         |96.80      |97.23    |   97.73| 96.29|   98.99|   91.88|
|LayoutLMBASE                     |98.05     |96.29         |96.64      |97.49    |   96.51| 96.74|   99.06|   91.16|
|LayoutLMBASE + Sentence Breaks   |97.92     |96.32         |96.68      |96.74    |   95.42| 96.77|   99.11|   90.42|
|LayoutLMBASE + I-VILA(Text Line) |97.99     |96.41         |96.72      |97.29    |   95.98| 96.66|   99.11|   90.75|
|LayoutLMBASE + I-VILA(Text Block)|98.12     |96.81         |96.93      |96.96    |   97.52| 96.87|   99.14|   91.43|
|Simple Group Classifier          |96.10     |95.53         |97.10      |97.48    |   97.94| 96.68|   98.94|   93.25|
|H-VILA(Text Line)                |98.47     |95.88         |96.21      |97.46    |   95.26| 96.68|   99.16|   89.67|
|H-VILA(Text Block)               |98.01     |96.45         |96.14      |97.38    |   96.31| 96.33|   99.08|   91.67|
|# Tokens in Class                |395788    |88531         |90775      |26742    |    7083|223739| 7567934|   22289|
|contd.                           |Copyright |Correspondence|Dates      |Editor   |Equation|Figure|Glossary|Keywords|
|BERTBASE                         |97.34     |89.66         |94.56      |99.71    |   17.60| 94.05|   80.18|   93.42|
|BERTBASE + I-VILA(Text Line)     |97.38     |89.57         |94.60      |99.93    |      25| 94.84|   81.35|   94.34|
|BERTBASE + I-VILA(Text Block)    |97.85     |91.29         |94.99      |99.95    |   29.46| 95.52|   80.45|   95.40|
|LayoutLMBASE                     |97.63     |89.99         |94.80      |99.90    |   30.78| 95.52|   83.83|   94.95|
|LayoutLMBASE + Sentence Breaks   |97.62     |90.07         |94.73      |99.95    |   20.73| 95.83|   84.99|   93.88|
|LayoutLMBASE + I-VILA(Text Line) |97.47     |90.97         |95.20      |99.93    |   26.42| 95.67|   84.16|   94.82|
|LayoutLMBASE + I-VILA(Text Block)|97.66     |91.04         |95.13      |100.00   |   39.28| 95.74|      87|   96.23|
|Simple Group Classifier          |97.56     |92.11         |95.47      |100.00   |   33.17| 95.77|   80.35|   95.64|
|H-VILA(Text Line)                |97.78     |89.96         |94.98      |99.91    |   15.60| 95.63|   84.01|   93.69|
|H-VILA(Text Block)               |97.98     |90.37         |94.92      |100.00   |   30.64| 95.86|   78.29|   96.15|
|# Tokens in Class                |57419     |26653         |23702      |2937     |     761|581554|    2807|    7012|
|                                 |Page      |              |           |         |        |      |        |        |
|contd.                           |References|              |           |         |        |      |        |        |
# Table,Title,Type,Unknown,Macro F1
|                -                | Number |    -     |    -    |   -    |   -   |   -    |  -  |
|---------------------------------|-------:|---------:|--------:|-------:|------:|-------:|-----|
|BERTBASE                         |   98.32|     99.60|    94.11|   97.60|  87.62|   88.60|90.78|
|BERTBASE + I-VILA(Text Line)     |   98.82|     99.60|    94.53|   97.77|  93.70|   88.14|91.65|
|BERTBASE + I-VILA(Text Block)    |   98.92|     99.64|    94.31|   98.19|  93.09|   88.81|92.31|
|LayoutLMBASE                     |   98.94|     99.62|    95.30|   97.91|  91.24|   89.19|92.34|
|LayoutLMBASE + Sentence Breaks   |   98.90|     99.61|    95.63|   98.13|  91.68|   89.14|91.83|
|LayoutLMBASE + I-VILA(Text Line) |   99.05|     99.63|    95.61|   97.80|  94.59|   89.86|92.37|
|LayoutLMBASE + I-VILA(Text Block)|   99.05|     99.65|    95.73|   98.39|  95.17|   90.47|93.38|
|Simple Group Classifier          |   99.02|     99.61|    93.94|   98.18|  94.91|   89.60|92.65|
|H-VILA(Text Line)                |   98.96|     99.63|    96.02|   97.76|  93.61|   90.00|91.65|
|H-VILA(Text Block)               |   99.16|     99.68|    95.00|   98.36|  95.07|   89.23|92.37|
|# Tokens in Class                |46884.00|2340796.00|558103.00|22110.00|4543.00|54639.00|—    |
# Table,Title,Macro F1
|            BERTBASE             |  97.82  | 89.96  |  93.91  | 87.33 |  71.97  |  84.76  |  75.99  |   96.84   |  92.05   |  92.81  |  74.19  | 89.31  |87.24|
|---------------------------------|--------:|-------:|--------:|------:|--------:|--------:|--------:|----------:|---------:|--------:|--------:|-------:|-----|
|BERTBASE + I-VILA(Text Line)     |    97.99|   90.67|    95.74|  88.12|    88.85|    88.29|    80.20|      97.85|     92.68|    94.91|    77.39|   90.34|90.25|
|BERTBASE + I-VILA(Text Block)    |    98.15|   90.66|    96.56|  87.83|    79.49|    88.40|    80.72|      97.51|     92.62|    94.86|    76.91|   90.22|89.49|
|LayoutLMBASE                     |    98.63|   92.25|    96.88|  87.13|    76.56|    94.26|    89.67|      97.72|     93.16|    96.31|    77.38|   92.80|91.06|
|LayoutLMBASE + Sentence Breaks   |    98.48|   92.70|    96.93|  88.06|    77.65|    94.35|    90.46|      97.81|     92.61|    96.58|    78.84|   92.81|91.44|
|LayoutLMBASE + I-VILA(Text Line) |    98.57|   92.64|    97.35|  87.87|    90.78|    94.37|    90.77|      98.44|     92.87|    96.60|    80.43|   92.78|92.79|
|LayoutLMBASE + I-VILA(Text Block)|    98.68|   92.31|    97.44|  87.69|    83.41|    94.03|    90.56|      98.13|     93.27|    96.44|    79.51|   92.48|   92|
|LayoutLMv2BASE                   |    98.68|   93.04|    97.49|  89.55|    85.60|    95.30|    93.63|      98.46|     94.30|    96.48|    84.41|   93.10|93.34|
|Simple Group Classifier          |    93.85|   84.68|    96.55|  71.04|    80.63|    91.58|    83.84|      97.53|     92.54|    85.33|    73.85|   92.65|87.01|
|H-VILA(Text Line)                |    98.68|   90.95|    95.46|  80.99|    88.79|    93.84|    90.77|      98.36|     93.81|    95.27|    78.46|   89.81|91.27|
|H-VILA(Text Block)               |    98.57|   86.81|    95.76|  70.33|    80.29|    91.23|    79.82|      97.53|     92.97|    86.70|    79.84|   93.52|87.78|
|# Tokens in Class                |461898.00|81061.00|858862.00|3275.00|932150.00|158176.00|684786.00|20630188.00|1813594.00|154062.00|235801.00|26355.00|—    |
# Table 8: Prediction F1 breakdown for all models on the DocBank dataset.
|                -                | Abstract  |   Author   |Bibliography|  Caption  |  Equation  |   Figure   |   Footer   |  Footnote  |
|---------------------------------|-----------|------------|------------|-----------|------------|------------|------------|------------|
|BERTBASE                         |91.67(5.51)|71.38(18.79)|97.90(1.59) |94.64(1.38)|76.23(4.36) |60.14(24.13)|61.99(17.04)|62.91(7.23) |
|BERTBASE + I-VILA(Text Line)     |89.38(6.50)|65.93(15.48)|97.92(1.56) |96.66(1.39)|83.22(5.87) |72.11(13.35)|57.75(22.46)|72.78(12.45)|
|BERTBASE + I-VILA(Text Block)    |90.45(3.61)|64.97(16.11)|97.21(1.27) |96.82(0.94)|83.56(5.59) |70.57(11.56)|59.79(23.18)|80.17(10.48)|
|LayoutLMBASE                     |91.87(4.89)|69.39(11.30)|98.08(1.13) |92.98(7.35)|77.49(7.13) |74.46(18.48)|67.42(18.90)|77.22(17.59)|
|LayoutLMBASE + Sentence Breaks   |92.01(4.79)|69.22(11.02)|98.57(1.24) |95.74(1.36)|77.94(9.68) |67.80(25.61)|69.67(20.06)|78.57(16.45)|
|LayoutLMBASE + I-VILA(Text Line) |91.77(5.85)|69.81(7.86) |98.09(1.64) |94.06(2.91)|84.48(7.00) |71.57(21.49)|67.23(23.01)|77.10(15.64)|
|LayoutLMBASE + I-VILA(Text Block)|92.91(4.02)|70.42(13.38)|98.19(1.57) |97.19(1.16)|83.76(6.61) |68.38(26.11)|68.03(19.11)|76.77(17.64)|
|LayoutLMv2BASE                   |91.09(6.46)|63.42(17.55)|97.74(2.00) |96.73(1.39)|77.18(13.70)|83.71(11.53)|64.37(22.24)|70.20(12.43)|
|H-VILA(Text Line)                |93.90(5.16)|70.86(9.78) |97.71(1.26) |92.86(3.89)|81.38(7.79) |77.86(10.65)|65.95(23.44)|81.76(15.03)|
|H-VILA(Text Block)               |93.40(6.14)|67.03(19.43)|96.11(3.38) |92.76(6.47)|86.87(8.64) |79.64(11.21)|63.72(22.01)|83.66(9.88) |
|# Tokens in Class                |2854(432)  |543(118)    |15681(3704) |4046(2119) |2552(1872)  |1402(1316)  |480(205)    |2468(1254)  |
|contd.                           |Header     |Keywords    |List        |Paragraph  |Section     |            |            |            |
# Table,Title,Macro F1
|            BERTBASE             |76.47(8.51)|90.16(6.44) |51.00(16.90)|96.07(1.37)|79.72(3.46)|79.93(16.26)|84.81(8.52)|78.34(6.53)|
|---------------------------------|-----------|------------|------------|-----------|-----------|------------|-----------|-----------|
|BERTBASE + I-VILA(Text Line)     |81.53(7.94)|87.06(5.57) |58.64(8.10) |96.67(1.13)|87.21(3.25)|85.58(15.67)|84.80(5.84)|81.15(4.83)|
|BERTBASE + I-VILA(Text Block)    |83.99(8.74)|87.86(7.51) |62.01(13.25)|96.65(1.21)|86.71(3.23)|80.44(16.35)|86.14(5.23)|81.82(4.88)|
|LayoutLMBASE                     |88.21(5.81)|88.14(5.94) |58.21(15.15)|96.88(0.87)|88.14(2.73)|82.02(15.58)|89.90(8.17)|82.69(6.04)|
|LayoutLMBASE + Sentence Breaks   |88.08(5.71)|88.80(3.23) |60.61(11.80)|97.01(0.85)|88.05(2.79)|81.59(16.22)|88.52(5.92)|82.81(5.21)|
|LayoutLMBASE + I-VILA(Text Line) |87.14(6.49)|86.66(6.24) |65.82(10.92)|97.17(1.26)|89.79(2.48)|86.00(12.33)|89.89(7.47)|83.77(5.75)|
|LayoutLMBASE + I-VILA(Text Block)|88.39(6.20)|90.92(3.97) |59.06(17.99)|97.17(1.14)|88.67(3.57)|81.84(15.77)|89.95(6.32)|83.44(6.48)|
|LayoutLMv2BASE                   |86.95(6.84)|89.71(7.95) |68.36(10.05)|96.65(0.71)|89.48(4.13)|81.69(15.05)|88.46(6.00)|83.05(4.51)|
|H-VILA(Text Line)                |87.89(6.45)|86.34(5.02) |65.76(10.26)|96.90(0.75)|85.45(2.02)|85.19(7.55) |85.62(6.00)|83.69(2.92)|
|H-VILA(Text Block)               |86.49(6.08)|76.97(18.82)|55.82(16.99)|96.43(1.40)|86.72(4.55)|81.38(14.94)|84.39(9.10)|82.09(5.89)|
|# Tokens in Class                |1122(463)  |130(27)     |2274(593)   |95732(8226)|882(113)   |3887(2041)  |240(26)    |—          |
