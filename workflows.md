microPIPE: a pipeline for high-quality bacterial genome construction using ONT and Illumina sequencing
================

  - [Description](#description)
  - [Diagram](#diagram)
  - [User guide](#user-guide)
      - [Quick start guide](#quick-start-guide)
      - [Infrastructure usage and
        recommendations](#infrastructure-usage-and-recommendations)
      - [Compute resource usage across tested
        infrastructures](#compute-resource-usage-across-tested-infrastructures)
  - [Benchmarking](#benchmarking)
  - [Workflow summaries](#workflow-summaries)
      - [Metadata](#metadata)
      - [Component tools](#component-tools)
      - [Required (minimum)
        inputs/parameters](#required-minimum-inputsparameters)
      - [Third party tools /dependencies](#third-party-tools-dependencies)
  - [Additional notes](#additional-notes)
  - [Help / FAQ / Troubleshooting](#help-faq-troubleshooting)
  - [3rd party Tutorials](#rd-party-tutorials)
  - [Licence(s)](#licences)
  - [Acknowledgements / citations /credits](#acknowledgements-citations-credits)

# Description

microPIPE was developed to automate high-quality complete bacterial genome assembly using Oxford Nanopore Sequencing in combination with Illumina sequencing. 

To build microPIPE we evaluated the performance of several tools at each step of bacterial genome assembly, including basecalling, assembly, and polishing. Results at each step were validated using the high-quality ST131 *Escherichia coli* strain EC958 (GenBank: HG941718.1). After appraisal of each step, we selected the best combination of tools to achieve the most consistent and best quality bacterial genome assemblies.

Micropipe has been written in Nextflow and uses Singularity containers. It can use both GPU and CPU resources. 

For more information please see our publication here: https://doi.org/10.1186/s12864-021-07767-z.

-----

# Diagram

 <p align="center">
 <img src="https://github.com/BeatsonLab-MicrobialGenomics/micropipe/blob/main/docs/Fig_workflow.png" alt="Workflow" width="400"/>
 </p>

-----

# User guide

## Quick start guide

Infrastructure specific guide for [Zeus @ Pawsey Supercomputing Centre provided here](https://github.com/vmurigneu/micropipe_pawsey/blob/master/docs/infrastructure_optimisation_zeus.md#quickstart-tutorial).

## Infrastructure usage and recommendations

### General recommendations for using microPIPE

When using microPIPE to run the Oxford Nanopore data basecalling and demultiplexing, it is recommended to use the GPU resources. As a result, the basecalling step will be performed using the high accuracy model (instead of the fast model) and the workflow will complete faster than with only the CPU resources. 

* The table below summarised the basecalling run time depending on the resources used. 

|Resources (Cluster)|Basecalling model|Guppy Configuration file|Run time|
|-------|:-----:|:-----:|:-----:|
|GPU (Topaz)| high-accuracy | dna_r9.4.1_450bps_hac.cfg | 10h 17m 17s |    
|CPU (Zeus)| fast | dna_r9.4.1_450bps_fast.cfg | 3d 19h 21m 31s |    
 
To use GPU resources for basecalling and demultiplexing, use the `--gpu` flag in the main nextflow command:  
```
nextflow main.nf --gpu true --basecalling --demultiplexing --samplesheet /path/to/samples.csv --fast5 /path/to/fast5/directory/ --datadir /path/to/datadir/ --outdir /path/to/outdir/
```

-----

## Compute resource usage across tested infrastructures

    Table with high level compute resource usage information for standalone runs or testing of specific versions on specific computational infrastructures.

| Title | Version | Sample description | Wall time | Cores | Peak RAM in GB (requested) | Drive (GB) | HPC-HTC | If HPC-HTC is other, specify | Scheduler | Year-Month |
| ----- | ------- | ------------------ | --------- | ----- | -------------------------- | ---------- | ------- | ---------------------------- | --------- | ---------- |
|       |         |                    |           |       |                            |            |         |                              |           |            |

-----

# Benchmarking

## Summary

### Exemplar 1: Assembly of 12 *E.coli* ST131 samples using GPU and CPU resources

You can collect usage metrics from your Canu run using the NCI Gadi optimised workflow using scripts available on the Sydney Informatics Hub, University of Sydney GitHub repository.
* We used the *E.coli* data from the [microPIPE publication](https://bmcgenomics.biomedcentral.com/articles/10.1186/s12864-021-07767-z) available from the NCBI SRA [BioProject PRJNA679678](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA679678/) (Oxford Nanopore) and the [BioProject PRJEB2968](https://www.ncbi.nlm.nih.gov/bioproject/?term=PRJEB2968) (Illumina). 

* See Nextflow configuration file used [here](./nextflow.config) and slurm submission script [here](./nextflow_batch_template.sh). 
* See Nextflow [HTML execution report](./micropipe_ecoli_ST131_pawsey_guppy3.6.1_gpu.report.html), [trace report](./micropipe_ecoli_ST131_pawsey_guppy3.6.1_gpu.trace.txt) and [HTML processes execution timeline](./micropipe_ecoli_ST131_pawsey_guppy3.6.1_gpu.timeline.html). 

* The table below summarised the assembly results for each strain. 

|Strain|Chromosome/plasmid|Size (bps)|Circularised?|
|-------|:-----:|:-----:|:-----:|
|S24EC| Chromosome <br> Plasmid A | 5078304 <br> 114708 | Yes <br> Yes |    
|S34EC| Chromosome <br> Plasmid A <br> Plasmid B | 5050427 <br> 153321 <br> 108135 | Yes <br> Yes <br> Yes |    
|S37EC| Chromosome <br> Plasmid A <br> Plasmid B | 4981928 <br> 157642 <br> 61072 | Yes <br> Yes <br> Yes |    
|S39EC| Chromosome <br> Plasmid A <br> Plasmid B <br> Plasmid C <br> Plasmid D <br> Plasmid E <br> Plasmid F | 5054402 <br> 141007 <br> 94979 <br> 68049 <br> 62085 <br> 2070 <br> 1846 | Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes |    
|S65EC| Chromosome <br> Plasmid A | 5205011 <br> 147412 | Yes <br> Yes |    
|S96EC| Chromosome <br> Plasmid A <br> Plasmid B <br> Plasmid C <br> Plasmid D | 5069496 <br> 164355 <br> 115965 <br> 14479 <br> 4184 | Yes <br> Yes <br> Yes <br> Yes <br> Yes |  
|S97EC| Chromosome <br> Plasmid A <br> Plasmid B <br> Plasmid C <br> Plasmid D | 5178868 <br> 166099 <br> 96788 <br> 4092 <br> 3209 | Yes <br> Yes <br> Yes <br> Yes <br> Yes |  
|S112EC| Chromosome <br> Plasmid A <br> Plasmid B <br> Plasmid C <br> Plasmid D | 5020013 <br> 161028 <br> 68847 <br> 5338 <br> 4136 | Yes <br> Yes <br> Yes <br> Yes <br> Yes |  
|S116EC| Chromosome <br> Plasmid A <br> Plasmid B <br> Plasmid C <br> Plasmid D | 4989207 <br> 66792 <br> 5263 <br> 4257 <br> 4104 | Yes <br> Yes <br> Yes <br> Yes <br> Yes |  
|S129EC| Chromosome <br> Plasmid A <br> Plasmid B <br> Plasmid C <br> Plasmid D <br> Plasmid E <br> Plasmid F <br> Plasmid G | 5193964 <br> 163681 <br> 93505 <br> 33344 <br> 4087 <br> 2401 <br> 2121 <br> 1571 | Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes |  
|EC958| Chromosome <br> Plasmid A <br> Plasmid B <br> Plasmid C | 5126816 <br> 136157 <br> 4145 <br> 1830 | Yes <br> Yes <br> Yes <br> Yes |    
|HVM2044| Chromosome <br> Plasmid A <br> Plasmid B <br> Plasmid C | 5003288 <br> 142959 <br> 18716 <br> 18345 | Yes <br> Yes <br> Yes <br> Yes |    


### Exemplar 2: Assembly of 12 *E.coli* ST131 samples using CPU resources 

* See Nextflow configuration file used [here](./nextflow.config) and slurm submission script [here](./nextflow_batch_template.sh). 

* See Nextflow [HTML execution report](./micropipe_ecoli_ST131_pawsey_guppy3.6.1_cpu.report.html), [trace report](./micropipe_ecoli_ST131_pawsey_guppy3.6.1_cpu.trace.txt) and [HTML processes execution timeline](./micropipe_ecoli_ST131_pawsey_guppy3.6.1_cpu.timeline.html). 

-----

# Workflow summaries

## Metadata

| metadata field   | workflow\_name / workflow\_version |
| ---------------- | :--------------------------------: |
| Version          |         v0.9          |
| Maturity         |               stable               |
| Creators         |        Valentine Murigneux, Leah W Roberts,  Brian M Forde, Minh-Duy Phan, Nguyen Thi Khanh Nhu, Adam D Irwin, Patrick N A Harris, David L Paterson, Mark A Schembri, David M Whiley, Scott A Beatson          |
| Source           |                 https://github.com/BeatsonLab-MicrobialGenomics/micropipe                 |
| License          |                 https://github.com/BeatsonLab-MicrobialGenomics/micropipe/blob/main/LICENSE                 |
| Workflow manager |              NextFlow              |
| Container        |                Singularity                |
| Install method   |               Manual               |
| GitHub           |                 https://github.com/BeatsonLab-MicrobialGenomics/micropipe                 |
| bio.tools        |                 NA                 |
| BioContainers    |                 NA                 |
| bioconda         |                 NA                 |

-----

## Component tools

| Workflow element | Workflow element version | Workflow title |
| ---------------- | :----------------------: | :------------: |
| Guppy           |   See workflow version   | microPIPE |
| qcat           |   See workflow version   | microPIPE |
| pycoQC           |   See workflow version   | microPIPE |
| Porechop           |   See workflow version   | microPIPE |
| Japsa           |   See workflow version   | microPIPE |
| Flye           |   See workflow version   | microPIPE |
| Racon           |   See workflow version   | microPIPE |
| Medaka           |   See workflow version   | microPIPE |
| NextPolish           |   See workflow version   | microPIPE |

-----

## Required (minimum) inputs/parameters

    The minimum inputs required for the workflow to run.

-----

## Third party tools / dependencies

* [Nextflow](https://www.nextflow.io/) >= 20.10.0

Nextflow can be used on any POSIX compatible system (Linux, OS X, etc). It requires Bash 3.2 (or later) and Java 8 (or later, up to 15) to be installed.

To install Nextflow, run the command:

`wget -qO- https://get.nextflow.io | bash` or `curl -s https://get.nextflow.io | bash`

It will create the nextflow main executable file in the current directory. Optionally, move the nextflow file to a directory accessible by your $PATH variable. 

* [Singularity](https://singularity.lbl.gov/install-linux) >= 2.3 (microPIPE has been tested with version 3.4.1, 3.5.0 and 3.6.3)

* Guppy (4.4.1 was the latest working version)
 
Due to the Oxford Nanopore Technologies terms and conditions, we are not allowed to redistribute the Guppy software either in its binary form or packaged form e.g. Docker or Singularity images. Therefore users will have to either install Guppy, provide a container image or start the pipeline from the basecalled fastq files. 

-----

# Additional notes

-----

# Help / FAQ / Troubleshooting

-----

# 3rd party Tutorials

-----

# Licence(s)
 https://github.com/BeatsonLab-MicrobialGenomics/micropipe/blob/main/LICENSE  
 
-----

# Acknowledgements / citations / credits

## Citations

- Murigneux, V., Roberts, L.W., Forde, B.M. et al. MicroPIPE: validating an end-to-end workflow for high-quality complete bacterial genome construction. BMC Genomics 22, 474 (2021). [https://doi.org/10.1186/s12864-021-07767-z](https://doi.org/10.1186/s12864-021-07767-z)
- Murigneux, V. (2021). microPIPE: a pipeline for high-quality bacterial genome construction using ONT and Illumina sequencing. WorkflowHub. [https://doi.org/10.48546/WORKFLOWHUB.WORKFLOW.140.1](https://doi.org/10.48546/WORKFLOWHUB.WORKFLOW.140.1)

# Acknowledgements

This work is supported by the Australian BioCommons via funding from Bioplatforms Australia, the Australian Research Data Commons (https://doi.org/10.47486/PL105) and the Queensland Government RICF programme. Bioplatforms Australia and the Australian Research Data Commons are funded by the National Collaborative Research Infrastructure Strategy (NCRIS).

-----

