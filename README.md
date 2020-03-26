#Introduction

SPARCQ (SPAdes, Read map coverage, CheckM, and QUAST) is an extension for the sunbeam pipeline for de novo microbial genome assembly and quality assessment.

#Installation
1. Add packages in sbx_SPARCQ_env.yml to sunbeam environment.yml and install with your sunbeam's ./install.sh --update env
2. To install QUAST in sunbeam environment (if you cannot install it in step #1), use your environment's pip to install quast
  - ex. /home/tuv/miniconda3/envs/sunbeam/bin/pip install quast
  - change rule quast to use quast.py
3. Recommended for cluster: specify the memory usage in cluster.json, especially with checkm_tree

#Config
threads (SPAdes, BWA, samtools): # of threads to use for running programs
rank (CheckM): one of {life,domain,phylum,class,order,family,genus,species}
taxon (CheckM): choose the taxon for the specified 'rank'; inputting this option will tell CheckM to generate gene markers of the specified taxon to assess completeness of the assembled genome; the default option will be to run the lineage work flow (https://github.com/Ecogenomics/CheckM/wiki/Workflows)
ncbi_ref (QUAST): file path to the downloaded NCBI fasta file (*.fna) of the genome of interest to align the assembled contigs to
  -ncbi-genome-download -F fasta,gff -t [Taxonomy ID] -o [file path for ncbi_ref] all
ref_sample (QUAST): sample name of interest to align the assembled contigs to; default will be to use the first sample as a reference
alnLen (Read mapping): filter the reads by this minimum length that maps to the assembled genome
percIdentity (Read mapping): filter reads that maps to the genome by this percentage (0 to 1)
window_size (Read mapping): define the window size to do sliding window coverage
sampling (read mapping): define minimum length of data to slide over

#Contributors
1. This extension was adapted from pipelines written by Scott Daniels, Ceylan Tanes, Jung-Jin Lee, and Louis Taylor. Mapping rules were adapted from the sunbeam pipeline (https://github.com/sunbeam-labs/sunbeam/tree/stable/rules/mapping) and sbx_mapping_withFilter (https://github.com/ctanes/sbx_mapping_withFilter)