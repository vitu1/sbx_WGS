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

checkm_yml (optional): YAML file containing a sample:rank and sample:taxon dictionary for CheckM parameters (see example);
rank is one of {life,domain,phylum,class,order,family,genus,species};
taxon is the taxonomic classification for the specified 'rank'

taxid_yml (optional): YAML file containing a sample:TaxonID dictionary for reference genomes to be downloaded by ncbi-genome-download for comparison in QUAST

window_size (Read mapping): define the window size to do sliding window coverage

sampling (read mapping): define minimum length of data to slide over

## Contributors
This extension was adapted from pipelines written by Scott Daniel, Jung-Jin Lee, Ceylan Tanes, and Louis Taylor. Read mapping rules were adapted from the sunbeam pipeline (https://github.com/sunbeam-labs/sunbeam/tree/stable/rules/mapping) and sbx_mapping_withFilter (https://github.com/ctanes/sbx_mapping_withFilter)

