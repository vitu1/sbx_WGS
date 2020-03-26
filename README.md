# sbx_SPARCQ (SPAdes, Read map coverage, CheckM, and QUAST)

## Introduction

SPARCQ is an extension for the sunbeam pipeline for de novo microbial genome assembly and quality assessment.

### Installation
1. Add packages in sbx_SPARCQ_env.yml to sunbeam environment.yml and install with your sunbeam's ./install.sh --update env
2. To install QUAST in sunbeam environment (if you cannot install it in step #1), use your environment's pip to install quast
```
/path/to/miniconda3/envs/sunbeam/bin/pip install quast
(If installed this way, may need to change quast to quast.py in sbx_SPARCQ.rules)
```
3. Add config.yml to sunbeam_config.yml
```
cat config.yml >> /path/to/sunbeam_config.yml
```
4. Recommended for cluster: add the memory specifications in cluster.json, especially for checkm_tree rule

## Options for config.yml
threads (SPAdes, BWA, samtools): # of threads to use for running programs

rank (CheckM, optional): one of {life,domain,phylum,class,order,family,genus,species}

taxon (CheckM, optional): choose the taxon for the specified 'rank'; inputting this option will tell CheckM to generate gene markers of the specified taxon to assess completeness of the assembled genome; the default option will be to run the lineage work flow (https://github.com/Ecogenomics/CheckM/wiki/Workflows)

ncbi_ref (QUAST, optional): file path of the downloaded NCBI fasta file (*.fna) of the genome of interest to align the assembled contigs to
```
ncbi-genome-download -F fasta,gff -t [Taxonomy ID] -o [file path for ncbi_ref] all
```

ref_sample (QUAST, optional): sample name of interest to align the assembled contigs to; default will be to run QUAST assessment without alignment

alnLen (Read mapping): filter the reads by this minimum length that maps to the assembled genome

percIdentity (Read mapping): filter reads that maps to the genome by this percentage (0 to 1)

window_size (Read mapping): define the window size to do sliding window coverage

sampling (read mapping): define minimum length of data to slide over

## Contributors
This extension was adapted from pipelines written by Scott Daniels, Jung-Jin Lee, Ceylan Tanes, and Louis Taylor. Read mapping rules were adapted from the sunbeam pipeline (https://github.com/sunbeam-labs/sunbeam/tree/stable/rules/mapping) and sbx_mapping_withFilter (https://github.com/ctanes/sbx_mapping_withFilter)