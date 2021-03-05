---
title: "Brain decoding with the HCP tasks"
description: "new paper on brain decoding"
date: 2021-03-04T20:31:00-05:00
author: "Yu Zhang, Loic Tetrel, Bertrand Thirion, Pierre Bellec"
image: "tsne.jpeg"
draft: true
tags: ["paper"]
---
Can we decode many tasks simultaneously with fMRI? how many time points do we need? New paper out with @YuZhang2bic @BertrandThirion Spoiler: deep (graph) learning outperforms traditional machine learning with ~1M @HumanConnectome brain images

![tsne_motor](tsne.jpeg)

First let's talk about the dataset. We used task fMRI from @HumanConnectome
 with N~1k subjects, 7 task domains including 21 specific conditions we tried to decode, and about ~1k brain images per subject (across all conditions).

 The main model was a graph convolutional network (GCN), with 6 convolutional layers (32 filters per layer), and 2 fully connected layers. The graph: Glasser parccellation and a group functional connectome. Baselines: support vector classifiers (SVC) and random forest (RF).

 ![schematic of the graph convolutional netwokr](gcn.jpeg)

 Using a time window of 10 seconds, it is possible to decode the 21 conditions simultaneously with an average test accuracy of 90%. Here's the confusion matrix, looking very diagonally.

 ![confusion matrix for 10 s windows and 21 conditions](confusion.jpeg)

 Looking at single time points (~700 ms of data), it's still possible to decode accurately the condition (here foot movement). The accuracy increases over time following the onset of the condition. This likely reflects the characteristics of  the hemodynamic response.  

 ![decoding foot movement from single time points](foot.jpeg)

 And how much data do we need to train this GCN? a lot. Performance reaches a plateau for about 200 subjects, representing hundreds of thousands of time points.

 ![accuracy as a function of the number of subjects](n_subject.jpeg)

 The GCN outperformed all our baselines by at least 10% accuracy for 10s long data, and as much as 25% accuracy for SVC-linear. So at least for some tasks and a massive number of brain images, deep learning has the potential to shine

 Finally, @YuZhang2bic also looked at saliency maps to get a feel of what the GCN learned. Top contributing regions had good face validity. There is a number of additional control experiments in the paper.

 ![saliency maps for different annotations](saliency.jpeg)


 Huge thanks to @HumanConnectome for making this amazing data resource available, @CNeuromod
 @IVADO_Qc for funding, and @IUGM @UMontreal @Parietal_INRIA @ai_unique for being wonderful, supportive environments for neuroAI projects.
