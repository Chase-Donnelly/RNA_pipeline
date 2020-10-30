# RNA_pipeline
This is an overview of the pipeline used with descriptions starting with data coming from the sequencer. 

This is the main document that will have links to the code used in the pipeline. 

# Data from the sequencer. 
The data coming from the sequencer will likley be in the form of fastq files.  This pipeline uses paired end reads so there will be two files used R1 and R2. 

R1 and R2 can be explained like this; "Illumina paired-end sequencing is based on the idea that you have initial DNA fragments (longer than your actual read length) and you sequence both its ends. On the Illumina chip, both ends of each sequence are amplified prior to actual sequencing using bridging. This approach results in two reads per fragment, with the first read in forward orientation and the second read in reverse-complement orientation."

You will also need a metadata file to show what each of the samples is in your experiment

# Quality Checking and Trimming
The first step should always be to check the quality of the data for the experiment.  The first code to be run will be from trimmomatic, this will "trim" your reads to a certain set of standards and remove illumina adapters from your data. Examples of this codes can be seen in the trimmomatic_example.pbs file. 
