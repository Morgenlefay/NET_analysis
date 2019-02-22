# Nudler lab NET-seq analysis pipeline

This package provides scripts and `jupyter` notebooks to analyze `NET (Nascent
Elongating Transcript)-Seq` data.

## Installation

Dependencies: `pandas`, `jupyter`, `seaborn`

To install using `pip` and `venv`:

- create virtual environment:

        $ python3 -m venv /path/to/venv

- activate it and update `pip`:

        $ /path/to/venv/bin/activate
        (venv-name) $ pip install -U pip

- clone the repo:

        (venv-name) $ git clone https://github.com/NudlerLab/NET_analysis.git

- navigate to `NET_analysis` directory and run install script (this will install
    all dependencies):
    
        (venv-name) $ cd NET_analysis
        (venv-name) NET_analysis $ pip install -e .


data files are at: `brick1/netseq_tutorial`

right now, this project takes a demultiplexed zipped fastq file as input.
The example file name is: `wt-mmc.fastq.gz`
the first notebook named `code_Nudler_git_NET_get_map_files_from_fastq`. 
make sure you change the file path to fit the location of files on your station before you start. This notebook  will trim the reads of this file for 20-mer or less in length. 
i think it should make bowtie run faster.
the output file from this notebook is named `clean_Trimmed_wt-mmc.fastq.gz` and this file is used as input for bowtie 1. 
the output from bowtie in this case is not a binary file but rather a text-based map file. why? I dont know!
The map file is then used as input for the second notebook named `code_Nudler_Git_NET_collect_3end_RNA`.
This notebook will first collect the first nucleotide from each read. this nucletodei corresponds to the reverse complement of the 3' of the nascent RNA.

the second and last function of this notebook will then call for positinos where we are calling pauses.


Still much to do after wards but hey, the last time i was going over these codes was over 3 years ago...
So what next?

to be discussed in today's session!
 

### TODO:

- put everything to dataframe
- limit analysis to genes and take into account expression level
- simulation (FDR!)
- complete example notebook (make data location configurable)
- put the code into package
- add more more explanation of what it does and how
- explore how this can be adapted to eukaryotes

### OUTPUT

- Table 1: a table with two cols: (position, raw count signal) for each strand, normalized by total number of reads (RPM).
- Table 2:  Same as Table 1 but this time instead of row count signal, Table 2 should list only positions where the count signal is strong/significant enough to be defined as a pause.
- Fasta output for Weblogo: based on data from Table 2, extract from the genome-seq a 40nt window around the pause site.
- Table 3:  Same as Table 2 but with an additional 'gene' col
- Table 4:  Aggregation table with the mean/median pause number/1kb for each gene.
- Table 5: Meta-analysis of raw count signal around a point of interest (terminators, TSS etc.)

### Dependencies

- cutadapt
- bowtie2
- bedtools
- pandas
- jupyter
- seaborn
