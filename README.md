# How does loss of endothelial-Elovl7 impact cortical gene expression?
Here you can find all jupyter notebooks used for analyzing our Elovl7 single-nucleus RNA-sequencing (snRNAseq) dataset. Specifically, we sequenced the transcriptomes of all cells captured within cortical isolates from endothelial-specific Elovl7 conditional knockout (cKO) mice and litter-mate controls in the context of health, as well as two timepoints after injection with the systemic inflammatory stimulus lipopolysaccharide (LPS). Therefore, this allows us to compare how loss of Elovl7 impacts gene expression in the brain at the single-nucleus level, and allows us to determine how loss of Elovl7 affects neuroinflammatory responses across distinct cell types in the mouse cortex. 

For droplet-based snRNAseq, libraries were prepared using the Chromium Next GEM Single Cell 3' HT v3.1 according to the manufacturer's protocol (10x Genomics), targeting 20,000 nuclei per sample. Final snRNAseq libraries were sequenced on Illumina NovaSeq X Plus at the UCSD IGM Genomics Center.

![Screenshot 2025-01-15 at 12 54 01 PM](https://github.com/user-attachments/assets/90ffae58-6908-428c-8827-0290985700a5)
# snRNAseq quality control
Gene counts were obtained by aligning reads to the mm10 genome (refdata-gex-mm10-2020-A) using CellRanger software (v.7.2.0) (10x Genomics). Reads mapped to introns were counted to account for unspliced nuclear pre-mRNA. Ambient cell free mRNA contamination was estimated and removed using SoupX (v.1.6.2) with default settings. In the R packages Seurat (v.5.0.1), low-quality nuclei were removed from the dataset based on the following criteria: 1)<200 features, 2) homotypic doublets with >5000 features, 3) high ratio of mitochondrial RNAs (>5%) relative to endogenous RNA, and 4) cells were manually inspected using known cell-type specific markers and heterotypic doublets expressing more than one cell-type specific marker were removed.

# Analysis Pipeline
After quality control, indivdual sample datasets were initially consolidated into one dataset using the merge() function in Seurat. SCTransform (v.0.4.1) was used for normalization, and data were projected into principal component (PC) space using PC analysis (RunPCA()). Integration was performed with the IntegrateLayers() function utilizing the RPCA Integration method. The first 30 PCs were used as inputs into Seurat's FindNeighbors(), FindClusters() with resolution of 2.0, and RunUMAP() functions.

Positive differential expression of each cluster against all other clusters was determined with the FindAllMarkers() function. Cell-types were annotated using previously published marker genes. 

![annotated_UMAP_052824](https://github.com/user-attachments/assets/9a2e9dfb-0a9c-4667-9051-7a47866f7c42)

# Differential Expression Analysis
Differential expression analysis between groups was performed by providing log-normalized counts data to the MAST algorithm, which leverages a hurdle model that combines tests for both discrete and continuous aspects of gene expression, and accounts for variation in the cellular detection rate, or the proportion of genes expressed in a single cell. Differentially expressed genes (DEGs) were assigned when the absolute value of the fold-change was greater than 20%, and p-value with Bonferroni's correction was <0.01. For heatmaps, the average expression value of each gene across all cells within a sample was determined via the AverageExpression() function in Seurat. Heatmaps were generated with the pheatmap (v.1.0.12) package in R. 

Example: astrocyte DEGs
![astrocyte_barplot_DEGs_240915](https://github.com/user-attachments/assets/02a884ed-9517-4a66-824e-d9669eb81fc2)

Example: Persistently up-regulated LPS-response genes in Elovl7 cKO astrocytes
![AcuPersD6cKO_Heatmap_2409013](https://github.com/user-attachments/assets/4c4348f5-cd69-487e-b996-85a47ca968ba)
