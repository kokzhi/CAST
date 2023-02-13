# Sternberg Lab - CAST guide RNA tool 
This is a tool for guide RNA design and off-target protospacer search for RNA-guided CRISPR-transposon (CAST) experiments, particularly for the Type I-F VchCAST system. 
It utilizes the bowtie2 alignment algorithm for genome-wide off-target search.

## Installation
This library requires Python >= 3.8, and a working installation of bowtie2 in the user's path. 
See [here](http://bowtie-bio.sourceforge.net/bowtie2/manual.shtml#obtaining-bowtie-2) for information on installing bowtie2. Note that Windows machines will also need Perl installed and in their path to run bowtie2. 

Python dependencies can be installed with `pip install -r requirements.txt` run in this directory. 

Note: bowtie2 must be in the SYSTEM path, not just installed via conda. The script uses a new subprocess call to invoke bowtie, so bowtie needs to be available outside any virtual environments that it might be running in. 

## Usage
There are two primary functions: spacer generation, and spacer evaluation. 

See the examples folder for some sample parameters. They should be copied to the appropriate file to run, not run on their own. 

There are also advanced parameters in `src/advanced_parameters.py`, see comments there for more details. 

#### Spacer generation
This function will generate a number of spacers per given region of a specified reference genome. It can be set to target a set of genes by gene names, intergenic (non-coding) regions, as well as custom (user-specified) windows. 
The function can be called by modifying variables within the `spacer_gen.py` file and running it with Python. Potential spacer candidates are filtered according to user-specified parameters, as well as evaluated for genome-wide potential off-targets using bowtie2 sequence alignment. A csv will output in the specified directory containing valid spacers targeting the region with minimal off-target potential. 

Be aware that, depending on the given run parameters, each region can take 2-5 minutes on a typical personal computer, so it may not be practical to run this code against thousands of genes in one run. Additional parameters that can influence speed and results (most notably the number of allowed mismatches) can be set in `advanced_parameters.py`

#### Spacer evalution
This function utilizes bowtie2 sequence alignment to evaluate user-specified spacers for potential off-targets in the genome. The function can be called by modify the variables in `spacer_eval.py` and running with Python. A summary csv output file contains information on off-target potential for each provided spacer, and for each spacer a detailed text file with more information about these off-targets will also be generated. 
