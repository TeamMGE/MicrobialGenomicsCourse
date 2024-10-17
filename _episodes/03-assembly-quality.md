---
title: "Genome assembly quality"
teaching: 0
exercises: 30
questions:
- How can we interpret the genome assembly quality of fungal genome assemblies?
objectives:
- Compare genome assemblies in light of their quality.
- Assess the implications of different genome sequencing technologies and assembly approaches on genome assemblies.
keypoints:
- You can compare genome assemblies with quast.
- You can examine and critically reflect on the impact of genome sequencing technologies on fungal genome assemblies.
---

##  Genome assembly information
We will now analyse *Zymoseptoria* genomes assemblies in more detail. Take a look at the `QUAST` [manual](http://quast.sourceforge.net/quast) to understand how to prepare a suitable command to execute `QUAST` on the command line.

The genome assemblies of some _Z. tritici_ isolates downloaded from NCBI GenBank can be found **data/fungalgenomics_seidl/assemblies/** (state: 2020). It will be useful to make a symbolic link to the data folder in your own home directory (or any other folder your own). You can do this by using `ln -s [source folder] [target folder]` where *source folder* is the name/location of the data folder and *target folder* is the name of the link you wish to create.

QUAST can be run using `quast`. First run the command without arguments (i.e. options nor files) to get a list of basic options (run with `--help` for the expanded help).

~~~
$ quast --help
~~~
{: .bash}

We will now prepare and execute a QUAST analyses on one *Zymoseptoria* genome using the reference IPO323 genome and annotation as comparison. Please make sure the output goes to your local folder and specify the number of threads (max=2).

~~~
$ quast.py -o quast_output -g gene:data/IPO323.gff -r data/IPO323.fna data/ASM22370v2.fna -t 2 
~~~
{: .bash}



> ## Exercise
> 
> How many fungal genomes are deposited in the database today?
>
>> ## Solution
>> 
>> `cat assembly_summary.txt | grep -v "^#" | wc -l`
>> 
> {: .solution}
{: .challenge}


{% include links.md %}
