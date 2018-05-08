# BIOC3301 Soil Microbiome Project

  This repository contains all files used in the analysis of the soil microbiome of Gordon Square Gardens and of an organic farm (Lupatini et al. (2016)). The aim of this project was to determine the suitability of London soil for urban agriculture with regards to its microbiome. 

  All bioinformatic analyses were carried out in Cartesius, the Dutch supercomputer (SURFsara), except for LEfSe and initial PICRUSt analysis, which were performed in the Huttenhower lab Galaxy web server. As such, all files in this repository are in the **P**ortable **B**atch **S**ystem format which specifies the commands and cluster resources required for each job. All jobs were run with 24 cores, and most could be completed under 1h walltime (an exception to this was chimera identification).

  Core diversity analysis was run with the core_div_analysis.pbs script in order to obtain an overview of the sample diversities and compositions.

## Raw Sequence Processing
  1. Join paired end reads (joining_paired_ends.pbs)
  2. Demultiplex and quality filtering (split_libraries_q25.pbs)
  3. Merge park and farm datasets and maps (merge_OTU_maps.pbs and merge_OTU_tables.pbs)
  4. Identify chimeras using usearch (identify_chimeras_usearch.pbs)
  5. Filter chimeras (filter_chimeras.pbs)
  6. Pick closed reference OTUs against SILVA database (pick_closed_ref_otus.pbs)
  7. Filter singletons from OTU table (filter_singletons.pbs)
  8. Filter outliers (filter_outliers.pbs)
  
## Diversity Analysis
  1. Rarefy OTU tables at different levels (multiple_rarefactions.pbs)
  2. Compute alpha diversity at each rarefaction level (alpha_diversity.pbs)
  3. Collate alpha diversity tables (collate_alpha.pbs)

## Taxonomic Composition
  1. Pick representative sequences (pick_rep_set.pbs)
  2. Align representative sequences (align_rep_seqs_pynast.pbs)
  3. Produce phylogenetic tree (make_tree.pbs)
  4. Summarize taxa through plots (summarize_taxa.pbs)

## Functional Metagenomics Profiling
  1. Pick OTUs with Greengenes (pick_closed_ref_otus.pbs)
  2. Followed PICRUSt pipeline on the Huttenhower lab Galaxy web server to obtain OTU table with assigned functions.
  3. Carried out beta diversity analysis on rarefied (single_rarefaction.pbs) functional OTU table and taxonomy OTU table in 
     QIIME. The resulting distance matrices were transposed for Procrustes analysis with transform_coordinate_matrices.pbs.
  4. EMPeror was used to produce three dimensional PCoA plots (make_emperor)
