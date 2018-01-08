---
title: "Sequence assembly"
teaching: 45
exercises: 30
questions:
- "How can the information in the sequencing reads be reduced?"
- "What are the different methods for assembly?"
objectives:
- "Understand differences between assembly methods"
- "Assemble the short reads"
- "Interpret an assembly QC plot"
---

Sequence assembly means the alignment and merging of reads in order to reconstruct the original sequence.
There are a few ways to keep cloud processes running in the background. Many times when we refer to a background process we are talking about what is described at this tutorial - running a command and returning to shell prompt. Here we describe a program that will allow us to run our entire shell and keep that process running even if we disconnect.

## Starting and attaching to screen sessions

### Starting a new session

A ‘session’ can be thought of as a window for screen, you might open an terminal to do one thing on the a computer and then open a new terminal to work on another task at the command line. You can start a session and give it a descriptive name:

~~~
screen -S session_name
~~~
{: .source}

This creates a session with the name ‘session_name’

As you work, this session will stay active until you close this session. Even if you disconnect from your machine, the jobs you start in this session will run till completion.


## Sequence assembly

We will talk about sequence assembly in a separate [lecture](../data/lectureAssembly.pdf)

The assembler we will run is SPAdes. SPAdes generates a final assembly from multiple kmers. A list of kmers is automatically selected by SPAdes using the maximum read length of the input data, and each individual kmer contributes to the final assembly. To run SPAdes we will use the spades.py command with the --careful option to minimize the number of mismatches in the contigs, -o for the output folder, -1 for the path to the forward reads, -2 for the path to the reverse reads, and -s for the path to the singles reads. If desired, a list of kmers can be specified with the -k flag which will override automatic kmer selection.


## Assembly (over night)

Because assembly of each genome might take a couple of hours, we will run all assemblies in a loop overnight. It is important to run them within the screen session or else the process will be terminated if we disconnect from the machine. 

We can start the loop with the assemblies

~~~
for sample in ERR026473 ERR026474 ERR026478 ERR026481 ERR026482 ERR029206 ERR029207
  do
  spades.py -1 --careful "$sample"_R1_sub.fastq -2 "$sample"_R2_sub.fastq -o ../results/assembly/"$sample"
  done
~~~
{: .source}

**Detach session (process keeps running in background)**

You can detach from a session by pressing `control + a` followed by `d` (for detach) on your keyboard. 

You can now safely log out from your machine. The assembly will run over night.

If you reconnect the next day to your machine, you will also have to reconnect to your session to see how it went.

**Seeing active sessions**

If you disconnect from your session, or from your ssh into a machine, you will need to reconnect to an existing `screen` session. You can see a list of existing sessions:

~~~
$ screen -ls
~~~
{: .bash}

**Reconnecting to a session**

To reconnect to an existing session:

~~~
$ screen -r session_name
~~~
{: .bash}

The `-r` option = 'resume  a detached screen session'

**Kill a session**
To end a session, type `exit` after reconnecting to the session:

~~~
$ screen -r session_name
$ exit
~~~
{: .bash}



> ## Challenge: How many contigs where generated by SPAdes??
>
> Find out how many contigs there are in the *M. tuberculosis* isolates. Enter your solution in the
> [table](https://docs.google.com/spreadsheets/d/1xjiliy_USyMwiyzEgWhpn8_109F7Z3jPM_f7Jp-lOb8/edit?usp=sharing)
>
> Hint:
> ~~~
> grep -c
> ~~~
> prints a count of matching lines for each input file.
> 
> > ## Solution
> >
> > 
> > ~~~
> > [1] grep -c '>' *.fna
> > ..
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}


{% include links.md %}