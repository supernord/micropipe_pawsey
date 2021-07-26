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

* See Nextflow configuration file used here and slurm submission script here. 
* See Nextflow [HTML execution report](), [trace report]() and [HTML processes execution timeline](). 

## Exemplar 2: Assembly of 12 *E.coli* ST131 samples using CPU resources 

* See Nextflow configuration file used [here]() and slurm submission script [here](). 

---

# Acknowledgements / citations / credits

- Marco de la Pierre (Pawsey Supercomputing Centre) [@marcodelapierre](https://github.com/marcodelapierre)
```
Any attribution information that is relevant to the workflow being documented, or the infrastructure being used.
```

---
