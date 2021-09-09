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
    
    Table with embedded registry links.

-----

# Diagram

 <p align="center">
 <img src="https://github.com/BeatsonLab-MicrobialGenomics/micropipe/blob/main/docs/Fig_workflow.png" alt="Workflow" width="400"/>
 </p>


-----

# User guide

## Quick start guide

    General guide for deployment across multiple infrastructures (distinct from specific infrastructure quick start guide) 

## Infrastructure usage and recommendations

    + link to installation instructions for each infrastructure 
    + recommendations
    
    Documentation for a specific infrastructure should go into a infrastructure documentation template
    https://github.com/AustralianBioCommons/doc_guidelines/blob/master/infrastructure_optimisation.md

-----

## Compute resource usage across tested infrastructures

    Table with high level compute resource usage information for standalone runs or testing of specific versions on specific computational infrastructures.

| Title | Version | Sample description | Wall time | Cores | Peak RAM in GB (requested) | Drive (GB) | HPC-HTC | If HPC-HTC is other, specify | Scheduler | Year-Month |
| ----- | ------- | ------------------ | --------- | ----- | -------------------------- | ---------- | ------- | ---------------------------- | --------- | ---------- |
|       |         |                    |           |       |                            |            |         |                              |           |            |

-----

# Benchmarking

    Benchmarking for a specific infrastructure should go here: if this document is complicated it should go into a benchmarking template, or be provided elsewhere (e.g. Zenodo). 

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

can be found

-----

# 3rd party Tutorials

-----

# Licence(s)
 https://github.com/BeatsonLab-MicrobialGenomics/micropipe/blob/main/LICENSE  
 
-----

# Acknowledgements / citations / credits

    Any attribution information that is relevant to the workflow being documented.

-----

