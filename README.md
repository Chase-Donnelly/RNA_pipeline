# RNA_pipeline
This is an overview of an RNAseq pipeline useing STAR and DESeq2 with my descriptions, starting with data coming from the sequencer.  There are verious other programs that can be used for RNAseq anaylsis, but this is the authors preference at the time of writting. Feel free to explore other pipelines based on the current concencuss and what fits your needs, not everyone may have access to a cluster.  

An example RNAseq pipeline flows as follows: Data from sequencer -> Quality assesment -> Obtain reference genome -> Alignment/count data -> Expression annalysis -> Annotation -> Visualiztion of anaylsis 

This is the main document that will have links to the code used in the pipeline. 

# Data from the sequencer. 
The data coming from the sequencer will likley be in the form of fastq files.  This pipeline uses paired end reads so there will be two files used R1 and R2. 

R1 and R2 can be explained like this; "Illumina paired-end sequencing is based on the idea that you have initial DNA fragments (longer than your actual read length) and you sequence both its ends. On the Illumina chip, both ends of each sequence are amplified prior to actual sequencing using bridging. This approach results in two reads per fragment, with the first read in forward orientation and the second read in reverse-complement orientation."

You will also need a metadata file to show what each of the samples is in your experiment

# Quality Checking and Trimming
The first step should always be to check the quality of the data for the experiment.  This is ussually done with FastQC, either from their GUI or via terminal(command line).  For the GUI you can just select the files you wish to run.  From terminal you for a server that has FastQC installed you can just type "fastqc filepath/filename -o outputfilepath/outputfilename"

The next code to be run will be from trimmomatic, this will "trim" your reads to a certain set of standards and remove illumina adapters from your data. Examples of this codes can be seen in the trimmomatic_example.pbs file. 

# Alignment with STAR 

There are a few possible allignment tools, but at the time STAR is a concessus pick for use in RNAseq experiments.  STAR is a fast and accuart aligmnent program but does require alot of memory to use (at least 30gb RAM), and so is best run on a dedicated server or very powerful machine (think 64gb of RAM). 

The first step with STAR is to create the needed genome index files.  This step is not resorce intensive and can be run on a local machine. The input files needed to generate the index files are the reference genome in fasta format, and the annotation (.GTF) file. An example of the STAR code is provided in the generate_index.pbs file. The output files should be kept in your genome directory for use with STAR for alignment. 

The next step is alignment, and example code for this can be found in the alignment.pbs file.

The STAR manual can be found by using the following link: https://physiology.med.cornell.edu/faculty/skrabanek/lab/angsd/lecture_notes/STARmanual.pdf

# Putting it all together

When working on a server all the previous steps can be combined into one larger code file to be used by your local cluster.  This means you can reduce the number of jobs that you are queing and henceforth be able to stay higher in prioty in the que. 
