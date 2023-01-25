---
title: "Data Visualization"
teaching: 10
exercises: 60
questions:
- "How are phylogenetic trees viewed and compared?"
- "How can I visualize several layers of data?"
objectives:
- "Explore the resulting trees in conjunction with the meta data."
- "Make an estimation on the likelihood of transmission events"
keypoints:
- "Genetic information can confirm or contradict the meta data"
---

## Comparison of clustering results

We now grouped our isolates by the the information that we extracted from the sequencing reads.
We compared our isolates to a reference genome and clustered them on basis of the single nucleotide variations that they exhibit when compared to this reference.

![workflow](../fig/Workflow.png)

Now we will visualize this grouping in the context of the meta data. Make sure you have the SNP tree that you generated (or can be downloaded here [core_snps.newick](../files/core_snps.newick)) on your own computer. 

## Visualization of genetic information and metadata

Visualization is frequently used to aid the interpretation of complex datasets. Within microbial genomics, visualizing the relationships between multiple genomes as a tree provides a framework onto which associated data (geographical, temporal, phenotypic and epidemiological) are added to generate hypotheses and to explore the dynamics of the system under investigation.

Download the meta data [file](../files/meta.csv) to your computer. Open Chrome. Go to [microreact](https://microreact.org/). Click on 'Upload'. Upload the newick tree produced by SNP typing ([core_snps.newick](../files/core_snps.newick)) and the metadata file.

Explore the location, time and further meta data. Play around with the different visualization options with the help of the [documentation of microreact](https://docs.microreact.org/).

> ## Discussion
>
> 1. Which transmission events are likely based on the metadata alone?
> 2. Which transmission events are likely based on the SNP or pangenome data?
> 3. Draw a transmission tree where possible.
{: .discussion}


