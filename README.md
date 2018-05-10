# Cas9-Guide-Designer
Software used to design single-guide RNA sequences for CRISPR/Cas9 genome editing

This software written in R aims to provide important feature information when designing guide RNA sequences for Cas9 genome editing using a simple user-friendly graphical interface. The user provides a target DNA sequence for editing, a genome to check for off-targets in, and a genome annotation file (.gtf) that is used for annotating off-target matches. The tool will output two separate data tables. The first table contains all information on the generated sgRNA sequences themselves (sgRNA Sequence, PAM, Direction, Start, End, GC Content, Presence of Homopolymers, Effciency Score (Doench 2014), and Genomic Matches). The second table contains all information about off-target sequences (Original sgRNA Sequence, Chromosome, Start, End, Number of Mismatches, Direction, Matched Sequence, Gene ID, Gene Name, Sequence Type, and Exon Number).

# Required files:
StandaloneFindsgRNAfunction_Doench2014.R - The main script that contains all the code needed to design sgRNA. This is the only R file users familiar with R will need.

Doench_Model_Weights_Singleonly.csv and Doench_Model_Weights_Doubleonly.csv - Two data tables used to assist with efficiency scoring. These must be put in the working directory when using the sgRNA_design function.

# Optional files:
RunShiny.R - A script that contains code for the graphical user interface. This UI requires installation of several addition packages and is currently only functional for the human and yeast genomes.

FindsgRNAfunction_Doench2014.R - A script designed to be used with the user optional Shiny user interface

Saccharomyces_cerevisiae.R64-1-1.92.gtf.gz - an example of a gene annotation file (.gtf) that needs to be used with the the sgRNA_design function

# Installation instructions
Simply clone or download all the Cas9-Guide-Designer files.
The necessary R packages are: ... *here list all the required packages*

If packages need to be installed input the following code in R:
install.packages("stringr", repos='http://cran.us.r-project.org')
source("https://bioconductor.org/biocLite.R")
biocLite("Biostrings")
biocLite("BSgenome")

# Instructions for StandaloneFindsgRNAfunction_Doench2014.R
The working directory must be set to a folder that contains this script, a .gtf file from a species of your choice, and the files: "Doench_Model_Weights_Singleonly.csv" and "Doench_Model_Weights_Doubleonly.csv"

Example: setwd("C://Users//User//Desktop//Folder")

Your organism's genome must be obtained from BSgenome
To obtain a list of available genomes type:

available.genomes()

When a genome has been selected use the following code:

biocLite("your.genenome")

Example: biocLite("BSgenome.Hsapiens.UCSC.hg19")

Finally, a genome annotation file (.gtf) must be obtained for your organism and placed in the working directory

These can be found at: https://useast.ensembl.org/info/data/ftp/index.html

Simply source this file and run the sgRNA_desgin function with the target sequence, genome, and gtf as arguments.

Example:

source("StandaloneFindsgRNAfunction_Doench2014.R")

alldata <- sgRNA_design("ATTCGAGGAGACTATAGAGCAGGATTAGGACAGAGACCATGTGACAGAA", Scerevisiae, "Saccharomyces_cerevisiae.R64-1-1.92.gtf.gz")


Important Note: When designing sgRNA for large genomes (billions of base pairs), use short query DNA sequences (under 250 bp). Depending on your hardware checking for off-targets can be quite computationally intensive and may take several hours if not limited to smaller query sequences.

# Instructions for Graphical User Interface using rShiny: FindsgRNAfunction_Doench2014.R 
