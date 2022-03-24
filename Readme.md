# 300K-RNA

Git repo for amalgamating splicing events from various public (and non-public) RNASeq datasets. Developed in R version 3.6

| Data source | URL                                   | Notes                                                        | Where to place the file?            |
| ----------- | ------------------------------------- | ------------------------------------------------------------ | ----------------------------------- |
| SRA (Recount3)  | http://snaptron.cs.jhu.edu/data/srav3h/junctions.bgz | Filtered to chromosomes 1-22, X, Y (filename junctions_1to22XY_srav3_filt.tsv) <br /> | src / sra |
| GTEx v8     | http://snaptron.cs.jhu.edu/data/gtexv2/junctions.bgz                              | Filtered to chromosomes 1-22, X, Y (filename junctions_1to22XY_gtexv2_filt.tsv) | src / gtex /    |


# Instructions
1. `sj_processing.Rmd` merges GTEx and SRA splice junctions and filters to those of interest, in preparation for creating 300K-RNA.   splice-junctions are processed seperately for ensembl and refseq transcripts:   
input:  
  gtex splice-junctions: `src/gtex/junctions_1to22XY_gtexv2_filt.tsv.gz`
  sra splice-junctions: `src/sra/junctions_1to22XY_srav3_filt.tsv.gz` 
  annotation files: `ref/ensembl_introns_exons.tsv.gz`, `ref/refseq_introns_exons.tsv.gz`  
output:  
  ensembl:`src/junctions_merged_processed_ensembl.tsv.gz`  
  refseq: `src/junctions_merged_processed_refseq.tsv.gz`  
    
3. `generate_300krna.Rmd` processes splice-junctions and infers which mis-splicing events they correspond to for each annotated donor & acceptor:  
input:   
  splice-junctions: `src/junctions_merged_processed_ensembl.tsv.gz`, `junctions_merged_processed_refseq.tsv.gz`  
  annotation files: `ref/ensembl_introns_exons.tsv.gz`, `ref/refseq_introns_exons.tsv.gz`  
output:   
  ensembl: `output/300KRNA_ensembl.tsv.gz`  
  refseq: `output/300KRNA_refseq.tsv.gz`  
  
Output is being used by [SpliceVault](https://kidsneuro.shinyapps.io/splicevault/)  

