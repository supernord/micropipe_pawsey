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
Due to the Oxford Nanopore Technologies terms and conditions, we are not allowed to redistribute the Guppy software either in its binary form or packaged form e.g. Docker or Singularity images. Therefore users will have to either install Guppy, provide a container image or start the pipeline from the basecalled fastq files.  See [Usage](#usage) section for instructions. 
---

# Quickstart tutorial

```
A tutorial to get a user started as quickly as practical.
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

## Exemplar 1: e.g. *Genus species* reference genome assembly

```
Any exemplar notes, or benchmarking, can be documented here.
```

## Exemplar 2: e.g. *Genus species* reference genome assembly

```
Any exemplar notes, or benchmarking, can be documented here.
```

---

# Acknowledgements / citations / credits

```
Any attribution information that is relevant to the workflow being documented, or the infrastructure being used.
```

---
