microPIPE on Zeus/Topaz @ Pawsey
===========

---

# Accessing tool/workflow

The workflow can be downloaded from the GitHub page https://github.com/BeatsonLab-MicrobialGenomics/micropipe using the command: 
```
git clone https://github.com/BeatsonLab-MicrobialGenomics/micropipe.git
```
Includes straightforward signing in to *HPC/HTC*

---

# Installation

* **[Nextflow](https://www.nextflow.io/)**  
A modified version of Nextflow, capable of submitting jobs to Zeus, Topaz and Magnus, has been installed as a system module and can be accessed with the command:
```
module load nextflow/20.07.1-multi
```
* **[Singularity](https://singularity.lbl.gov/install-linux)**  
Singularity has been installed as a system module and can be accessed with the command:
```
module load singularity/3.6.4 
```
* **Guppy** (3.6.1 was the latest working version)   
Due to the Oxford Nanopore Technologies terms and conditions, we are not allowed to redistribute the Guppy software either in its binary form or packaged form e.g. Docker or Singularity images. Therefore users will have to either install Guppy, provide a container image or start the pipeline from the basecalled fastq files.  See [Usage](https://github.com/BeatsonLab-MicrobialGenomics/micropipe#usage) section for instructions. 
---

# Quickstart tutorial

A tutorial is available on the GitHub page: https://github.com/BeatsonLab-MicrobialGenomics/micropipe#usage

**1. Prepare the Nextflow configuration file (nextflow.config)**  
Use the configuration file to run microPIPE at Pawsey Zeus [here](./nextflow.config).

**2. Prepare the samplesheet file (csv)**  
See instructions at the microPIPE [GitHub page](https://github.com/BeatsonLab-MicrobialGenomics/micropipe#usage), section 2. Prepare the samplesheet file. 

**3. Prepare the slurm script**  
The pipeline will be launched using a Slurm script submitted to Zeus. This script will load the required modules, define the input/output directories and files, and include the nextflow command line with optional parameters. 
```
#!/bin/bash

#SBATCH --job-name=micropipe
#SBATCH --nodes=1
#SBATCH --cpus-per-task=1
#SBATCH --output=s%A.micropipe_guppy3.6.1_gpu_12samples.out
#SBATCH --error=s%A.micropipe_guppy3.6.1_gpu_12samples.err
#SBATCH --time=24:00:00

module load nextflow/20.07.1-multi
module load singularity/3.6.4 

#directory containing the nextflow.config file and the main.nf script
dir=/scratch/director2172/vmurigneux/micropipe
cd ${dir}
datadir=${dir}/Illumina
out_dir=${dir}/results_3.6.1_gpu

#Run A, B or C depending on whether you are starting with ONT fast5 (A or B) or fastq files (C or D) 

#A) Workflow including basecalling, demultiplexing and assembly
fast5_dir=${dir}/fast5_pass
csv=${dir}/test_data/samples_all_basecalling.csv
nextflow main.nf --gpu true --basecalling  -profile zeus --slurm_account='director2172' --demultiplexing --samplesheet ${csv} --outdir ${out_dir} --fast5 ${fast5_dir} --datadir ${datadir}
#nextflow main.nf --gpu false --basecalling --guppy_num_callers 16 -profile zeus --slurm_account='director2172' --demultiplexing --samplesheet ${csv} --outdir ${out_dir} --fast5 ${fast5_dir} --datadir ${datadir}

#B) Workflow including basecalling and assembly (skip demultiplexing step)
#fast5_dir=${dir}/fast5_pass
#csv=${dir}/test_data/samples_1_basecalling_single_isolate.csv
#nextflow main.nf --basecalling --samplesheet ${csv} --outdir ${out_dir} --fast5 ${fast5_dir} --datadir ${datadir}

#C) Workflow including demultiplexing and assembly
#fastq_dir=${dir}/fastq
#csv=${dir}/test_data/samples_1_basecalling.csv
#nextflow main.nf --demultiplexing --samplesheet ${csv} --outdir ${out_dir} --fastq ${fastq_dir} --datadir ${datadir}

#D) Assembly workflow (skip basecalling and demultiplexing step)
#csv=${dir}/test_data/samples_1.csv
#nextflow main.nf --samplesheet ${csv} --outdir ${out_dir} --datadir ${datadir}

#to restart the pipeline if something failed, use the -resume flag after correcting the issue
#nextflow main.nf -resume --samplesheet ${csv} --outdir ${out_dir} --datadir ${datadir}
```

**4. Run the pipeline by submitting a job at Pawsey Zeus**
```
sbatch nextflow_batch_template.sh
```
---

# Optimisation required

```
Were any optimisations required that were specific to the HPC / HTC infrastructure used?
```

---

# Infrastructure usage and benchmarking

---

## Summary

## Exemplar 1: Assembly of 12 *E.coli* ST131 samples using GPU and CPU resources

* We used the *E.coli* data from the [microPIPE publication](https://bmcgenomics.biomedcentral.com/articles/10.1186/s12864-021-07767-z) available from the NCBI SRA [BioProject PRJNA679678](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA679678/) (Oxford Nanopore) and the [BioProject PRJEB2968](https://www.ncbi.nlm.nih.gov/bioproject/?term=PRJEB2968) (Illumina). 

* See Nextflow configuration file used [here](./nextflow.config) and slurm submission script [here](./nextflow_batch_template.sh). 
* See Nextflow [HTML execution report](./micropipe_ecoli_ST131_pawsey_guppy3.6.1_gpu.report.html), [trace report](./micropipe_ecoli_ST131_pawsey_guppy3.6.1_gpu.trace.txt) and [HTML processes execution timeline](./micropipe_ecoli_ST131_pawsey_guppy3.6.1_gpu.timeline.html). 

## Exemplar 2: Assembly of 12 *E.coli* ST131 samples using CPU resources 

* See Nextflow configuration file used [here]() and slurm submission script [here](). 

---

# Acknowledgements / citations / credits

- Marco de la Pierre (Pawsey Supercomputing Centre) [@marcodelapierre](https://github.com/marcodelapierre)
```
Any attribution information that is relevant to the workflow being documented, or the infrastructure being used.
```

---
