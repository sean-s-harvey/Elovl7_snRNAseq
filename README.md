# How does loss of endothelial-Elovl7 impact cortical gene expression?
Here you can find all jupyter notebooks used for analyzing our Elovl7 single-nucleus RNA-sequencing (snRNAseq) dataset. Specifically, we sequenced the transcriptomes of all cells captured within cortical isolates from Elovl7 conditional knockout (cKO) mice and litter-mate controls in the context of health, as well as two timepoints after injection with the systemic inflammatory stimulus lipopolysaccharide (LPS). Therefore, this allows us to compare how loss of Elovl7 impacts gene expression in the brain at the single-nucleus level, and allows us to determine how loss of Elovl7 affects neuroinflammatory responses. 

For droplet-based snRNAseq, libraries were prepared using the Chromium Next GEM Single Cell 3' HT v3.1 according to the manufacturer's protocol (10x Genomics), targeting 20,000 nuclei per sample. Final snRNAseq libraries were sequenced on Illumina NovaSeq X Plus at the UCSD IGM Genomics Center.

# snRNAseq quality control
Gene counts were obtained by aligning reads to the mm10 genome (refdata-gex-mm10-2020-A) using CellRanger software (v.7.2.0) (10x Genomics). Reads mapped to introns were counted to account for unspliced nuclear pre-mRNA. Ambient cell free mRNA contamination was estimated and removed using SoupX (v.1.6.2) with default settings. In the R packages Seurat (v.5.0.1), low-quality nuclei were removed from the dataset based on the following criteria: 1)<200 features, 2) homotypic doublets with >5000 features, 3) high ratio of mitochondrial RNAs (>5%) relative to endogenous RNA, and 4) cells were manually inspected using known cell-type specific markers and heterotypic doublets expressing more than one cell-type specific marker were removed.

# Analysis Pipeline
