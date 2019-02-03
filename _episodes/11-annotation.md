---
title: "Annotation"
start: true
teaching: 10
exercises: 50
questions:
- "How are proteins predicted from a DNA sequence?"
objectives:
- "Search for open reading frames"
- "Predict a protein from an open reading frame"
- "Annotate a genome"
keypoints:
- "Genome annotation includes prediction of protein-coding genes, as well as other functional genome units"
- "It often starts by identifying open reading frames"
- "Predicted sequences are further analysed with BLAST"
- "Larger DNA sequences or genomes require automated prediction and annotation"
---

## Annotation

Now that we have assembled the data into contigs the next natural step to do is annotation of the data. The contigs we assembled contain different genomic features. The process of identifying and labelling those features is called genome annotation.

Genome annotation includes prediction of protein-coding genes, as well as other functional genome units such as structural RNAs, tRNAs, small RNAs, pseudogenes, control regions, direct and inverted repeats, insertion sequences, transposons and other mobile elements. It starts by identifying open reading frames (ORFs). Predicted sequences are further analysed to search for similarity to known elements, for example with BLAST.


Have a look at the 3000 characters of ERR029207.fasta

~~~
$ head -c 3000 ~/dc_workshop/results/assembly/ERR029207.fasta
~~~
{: .source}


Let's copy the first contig including the header by moving over it with the mouse and pressing the left mouse button to copy.

> ## Exercise: Annotate a gene
> Go to [ORFfinder](https://www.ncbi.nlm.nih.gov/orffinder/). Paste the sequence including the header into the query 
> field. Choose the genetic code (translation table) 11. Start the search by pressing 'submit'. 
> This will open the Open Reading Frame viewer.
> 
> Search for the longest ORF. If you have found it, click on 'Mark'. Submit the longest ORF to BLAST.
> 
> How will this ORF be annotated? Is it a gene or something else? What does the gene do? Fill your annotation into the
> [table](https://docs.google.com/spreadsheets/d/1xjiliy_USyMwiyzEgWhpn8_109F7Z3jPM_f7Jp-lOb8/edit?usp=sharing) under the header ERR029207_ORF.
> 
{: .challenge}


## Automated Annotation

Now we will annotate all genomes with an automated approach. Prokka is a pipeline script which coordinates a series of genome feature predictor tools and sequence similarity tools to annotate the genome sequence or contigs. 
A range of programs are available for these tasks but here we will use PROKKA, which is a pipeline comprising several open source bioinformatic tools and databases.

PROKKA automates the process of locating ORFs and RNA regions on contigs, translating ORFs to protein sequences, searching for protein homologs and producing standard output files. For gene finding and translation, PROKKA makes use of the program Prodigal. Homology searching (via BLAST and HMMER) is then performed using the translated protein sequences as queries against a set of public databases (CDD, PFAM, TIGRFAM) as well as custom databases that come with PROKKA.

First we need to make a new folder to contain our annotation results.

~~~
$ cd ~/dc_workshop/results
$ mkdir annotation
~~~
{: .bash}

Now we are all set to annotate our contigs with PROKKA. Again, this will run for a while.
The parameter --outdir tells PROKKA which output directory to write to. This needs to be a new directory. 
The parameter --prefix assigns the sample name as a prefix to all files. If we ommit this, all output files would have the same name.

~~~
$ for sample in ERR026473 ERR026474 ERR026478 ERR026481 ERR026482 ERR029206 ERR029207
>  do
>  prokka --outdir annotation/anno_"${sample}" --prefix $sample assembly/"${sample}".fasta
>  done
~~~
{: .bash}

Let's check the output:

~~~
$ cat annotation/anno_*/ERR*.txt
~~~
{: .bash}


> ## Discussion: How many coding regions did PROKKA find in the contigs??
>
> Find out how many coding regions there are in the *M. tuberculosis* isolates. Enter your solution in the
> [table](https://docs.google.com/spreadsheets/d/1xjiliy_USyMwiyzEgWhpn8_109F7Z3jPM_f7Jp-lOb8/edit?usp=sharing) under the head 'Number of CDS'
>
> Hint:
> ~~~
> $ grep "CDS" 
> ~~~
> prints matching lines for each input file.
> 
> > ## Solution
> >
> > 
> > ~~~
> > $ grep CDS annotation/anno_*/ERR*.txt
> >  
> > annotation/anno_ERR026473/ERR026473.txt:CDS: 4028
> > annotation/anno_ERR026474/ERR026474.txt:CDS: 4024
> > annotation/anno_ERR026478/ERR026478.txt:CDS: 4008
> > annotation/anno_ERR026481/ERR026481.txt:CDS: 4024
> > annotation/anno_ERR026482/ERR026482.txt:CDS: 4010
> > annotation/anno_ERR029206/ERR029206.txt:CDS: 4036
> > annotation/anno_ERR029207/ERR029207.txt:CDS: 4042
> > 
> > These *M. tuberculosis* genomes contain between 4008 and 4042 coding regions.
> > ~~~
> > {: .output}
> Is your solution the same or do you get other numbers of coding regions? What could be possible explanations 
> if the solution differs? 
> {: .solution}
{: .discussion}


> ## Discussion: How many big are the genomes??
>
>Repeat the same exercise as described above with the key word 'bases' to see how large the sum of all contigs is (and by >approximation the genome) and fill into the [table](https://docs.google.com/spreadsheets>/d/1xjiliy_USyMwiyzEgWhpn8_109F7Z3jPM_f7Jp-lOb8/edit?usp=sharing) under the head 'Genome size'
{: .discussion}

{% include links.md %}
