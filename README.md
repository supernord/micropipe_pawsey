microPIPE
==============

This repository contains structured documentation for [microPIPE](https://github.com/BeatsonLab-MicrobialGenomics/micropipe), including links to existing repositories and community resources, as well as a description of the optimisations achieved on the following compute systems:

- [Pawsey Supercomputing Centre](https://pawsey.org.au/) (Perth, Western Australia)
     - [Zeus/Topaz](./infrastructure_optimisation.md)

---

# General recommendations for using microPIPE

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
---
```
###################################################################################
### Delete this section when the first version of the documentation is complete ###
###################################################################################

You can make use of this template repository as a base template for a new GitHub repository.

General information about the guidelines

- This **template** repository contains a set of guidelines for documenting bioinformatics tools and workflows. 
- The initial version uploaded to GitHub was informed by current documentation practices and structures used in the GitHub community.
- These guidelines will be further developed as needed to meet the requirements of the Australian BioCommons community.
```

---
