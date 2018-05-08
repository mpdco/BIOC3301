# BIOC3301 Soil Microbiome Project

  This repository contains all files used in the analysis of the soil microbiome of Gordon Square Gardens and of an organic farm (Lupatini et al. (2016)). The aim of this project was to determine the suitability of London soil for urban agriculture with regards to its microbiome. 

  All bioinformatic analyses were carried out in Cartesius, the Dutch supercomputer (SURFsara), except for LEfSe and initial PICRUSt analysis, which were performed in the Huttenhower lab Galaxy web server. As such, all files in this repository are in the **P**ortable **B**atch **S**ystem (PBS) format which specifies the commands and cluster resources required for each job. All jobs were run with 24 cores, and most could be completed under 1h walltime (an exception to this was chimera identification).

  Core diversity analysis was run with the core_div_analysis.pbs script in order to obtain an overview of the sample diversities and compositions.
  

## Raw Sequence Processing
  1. Join paired end reads (1_joining_paired_ends.pbs)
  2. Demultiplex and quality filtering (2_demultiplex.pbs)
  3. Merge park and farm datasets and maps (using BASH command line and 3_merge_OTU_maps.pbs)
  4. Identify chimeras using usearch against the SILVA database, v132 (4_identify_chimeras_usearch.pbs)
  5. Filter chimeras (5_filter_chimeras.pbs)
  6. Pick closed reference OTUs against SILVA database (6_pick_closed_ref_otus.pbs)
  7. Filter singletons from OTU table (7_filter_singletons.pbs)
  8. Filter outliers (8_filter_outliers.pbs)
  
## Diversity Analysis
  1. Rarefy OTU tables at different levels (9_multi_rarefactions.pbs)
  2. Compute alpha diversity at each rarefaction level (10_alpha_diversity.pbs)
  3. Collate alpha diversity tables (11_collate_alpha.pbs)

## Taxonomic Composition
  1. Pick representative sequences (12_pick_rep_set.pbs)
  2. Align representative sequences (13_align_rep_seqs_pynast.pbs) and filter alignment for highly variable regions (filter_alignment.pbs)
  3. Produce phylogenetic tree (14_make_tree.pbs)
  4. Summarize taxa through plots (15_summarize_taxa.pbs)

## Functional Metagenomics Profiling
  1. Pick OTUs with Greengenes (6_pick_closed_ref_otus.pbs)
  2. Followed PICRUSt pipeline on the Huttenhower lab Galaxy web server to obtain OTU table with assigned functions (https://huttenhower.sph.harvard.edu/galaxy/)
  3. Carried out beta diversity analysis (17_beta_diversity.pbs) on rarefied (16_single_rarefaction.pbs) functional OTU table and taxonomy OTU table in QIIME. The resulting distance matrices were transposed for Procrustes analysis with 18_transform_coordinate_matrices.pbs.
  4. EMPeror was used to produce three dimensional PCoA plots (19_make_emperor)
