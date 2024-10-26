# Nemo-10Xmultiome
Quality Control and Integration of Clownfish POA Brain Tissue using 10X's Single Nucleus Multiome ATAC + Gene Expression Platform 


## Load packages

```{r setup, include=FALSE, tidy = 'formatR'}
# Required R package installation:
# These will install packages if they are not already installed
# Set the correct default repository
r = getOption("repos")
r["CRAN"] = "http://cran.rstudio.com"
options(repos = r)
if (!require("Seurat")) {
    install.packages("Seurat")
    library(Seurat)
}
if (!require("tidyverse")) {
    install.packages("tidyverse")
    library(tidyverse)
}
if (!require("plotly")) {
    install.packages("plotly")
    library(plotly)
}
if (!require("patchwork")) {
  install.packages("patchwork")
  library(patchwork)
}
if (!require("ggplot2")) {
  install.packages("ggplot2")
  library(ggplot2)
}
if (!require("knitr")) {
  install.packages("knitr")
  library(knitr)
}
if (!require("tibble")) {
    install.packages("tibble")
    library(tibble)
}
if (!require("dplyr")) {
    install.packages("dplyr")
    library(dplyr)
}
if (!require("tidyr")) {
  install.packages("tidyr")
  library(tidyr)
}
if (!require("ggridges")) {
    install.packages("ggridges")
    library(ggridges)
}
if (!require('gprofiler2')) {
    install.packages("gprofiler2")
    library(gprofiler2)
}
if (!require('rrvgo')) {
    if (!require("BiocManager", quietly = TRUE))
        install.packages("BiocManager")
    BiocManager::install("rrvgo")
    library(rrvgo)
 }
if (!require('viridis')) {
    install.packages("viridis")
    library(viridis)
}
if (!require('scran')) {
    if (!require("BiocManager", quietly = TRUE))
        install.packages("BiocManager")
    BiocManager::install("scran")
    library(scran)
 }
if (!require('stringr')) {
    install.packages("stringr")
    library(stringr)
}
if (!require('sctransform')) {
    install.packages("sctransform")
    library(sctransform)
}
if (!require('glmGamPoi')) {
    if (!require("BiocManager", quietly = TRUE))
        install.packages("BiocManager")
    BiocManager::install("glmGamPoi")
    library(glmGamPoi)
 }
if (!require('GenomicFeatures')) {
    if (!require("BiocManager", quietly = TRUE))
        install.packages("BiocManager")
    BiocManager::install("GenomicFeatures")
    library(GenomicFeatures)
 }
if (!require('GenomicRanges')) {
    if (!require("BiocManager", quietly = TRUE))
        install.packages("BiocManager")
    BiocManager::install("GenomicRanges")
    library(GenomicRanges)
 }
if (!require('rtracklayer')) {
    if (!require("BiocManager", quietly = TRUE))
        install.packages("BiocManager")
    BiocManager::install("rtracklayer")
    library(rtracklayer)
 }
if (!require('HDF5Array')) {
    if (!require("BiocManager", quietly = TRUE))
        install.packages("BiocManager")
    BiocManager::install("HDF5Array")
    library(HDF5Array)
 }
if (!require('Signac')) {
    install.packages("Signac")
    library(Signac)
}
if (!require('multtest')) {
    if (!require("BiocManager", quietly = TRUE))
        install.packages("BiocManager")
    BiocManager::install("multtest")
    library(multtest)
}
if (!require('mutoss')) {
  install.packages("mutoss")
  library(mutoss)
}
if (!require('metap')) {
  install.packages("metap")
  library(metap)
}
if (!require('MuData')) {
    if (!require("BiocManager", quietly = TRUE))
        install.packages("BiocManager")
    BiocManager::install("MuData")
    library(MuData)
 }
if (!require('qlcMatrix')) {
  install.packages("qlcMatrix")
  library(qlcMatrix)
}
if (!require('ggExtra')) {
  install.packages("ggExtra")
  library(ggExtra)
}
if (!require('biomartr')) {
    install.packages("biomartr")
    library(biomartr)
}
if (!require('Biostrings')) {
    if (!require("BiocManager", quietly = TRUE))
        install.packages("BiocManager")
    BiocManager::install("Biostrings")
    library(Biostrings)
 }
if (!require("igraph")) {
    install.packages("igraph")
    library(igraph)
}
if (!require("MAST")) {
    if (!requireNamespace("BiocManager", quietly=TRUE))
        install.packages("BiocManager")
    BiocManager::install("MAST")
    library(MAST)
}
if (!require('BiocNeighbors')) {
    if (!require("BiocManager", quietly = TRUE))
        install.packages("BiocManager")
   BiocManager::install("BiocNeighbors")
   library(BiocNeighbors)
}
if (!require("circlize")) {
    install.packages("circlize")
    library(circlize)
}
if (!require("ggrepel")) {
    install.packages("ggrepel")
    library(ggrepel)
}
if (!require("mosaic")) {
    install.packages("mosaic")
    library(mosaic)
}
if (!require("plotly")) {
    install.packages("plotly")
    library(plotly)
}
if (!require("SeuratWrappers")) {
    if (!require(remotes)) {
    install.packages("remotes")}
    remotes::install_github('satijalab/seurat-wrappers')
    library(SeuratWrappers)
}
if (!require("speckle")) {
    if (!require(remotes)) {
    install.packages("remotes")}
    remotes::install_github("Oshlack/speckle")
    library(speckle)
}
if (!require("wesanderson")) {
    install.packages("wesanderson")
    library(wesanderson)
}
if (!require("kableExtra")) {
    install.packages("kableExtra")
    library(kableExtra)
}
if (!require("RColorBrewer")) {
    install.packages("RColorBrewer")
    library(RColorBrewer)
}
if (!require("scCustomize")) {
    install.packages("scCustomize")
    library(scCustomize)
}
if (!require("presto")) {
    if (!require(remotes)) {
    install.packages("remotes")}
    remotes::install_github("immunogenomics/presto")
    library(presto)
}
if (!require('DropletUtils')) {
    if (!require("BiocManager", quietly = TRUE))
        install.packages("BiocManager")
   BiocManager::install("DropletUtils")
   library(DropletUtils)
}
if (!require('DropletTestFiles')) {
    if (!require("BiocManager", quietly = TRUE))
        install.packages("BiocManager")
   BiocManager::install("DropletTestFiles")
   library(DropletTestFiles)
}
if (!require("scclusteval")) {
     if (!require(devtools)) {
         install.packages("devtools")}
    devtools::install_github("crazyhottommy/scclusteval")
    library(scclusteval)
}
if (!require("DropletUtils")) {
    if (!require("BiocManager", quietly = TRUE))
        install.packages("BiocManager")
   BiocManager::install("DropletUtils")
   library(DropletUtils)
}
if (!require("EmptyDropsMultiome")) {
     if (!require(devtools)) {
         install.packages("devtools")}
    devtools::install_github("MarioniLab/emptyDrops_multiome", ref="main")
    library(EmptyDropsMultiome)
}
if (!require('hdf5r')) {
    if (!require("BiocManager", quietly = TRUE))
        install.packages("BiocManager")
    BiocManager::install("hdf5r")
    library(hdf5r)
}
if (!require("future")) {
    install.packages("future")
    library(future)
}
if (!require("parallel")) {
    install.packages("parallel")
    library(parallel)
}
if (!require("parallelly")) {
    install.packages("parallelly")
    library(parallelly)
}
if (!require("formatR")) {
    install.packages("formatR")
    library(formatR)
}


knitr::opts_chunk$set(root.dir = "/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/R_markdowns/", tidy.opts = list(width.cutoff = 60), tidy = TRUE)

```

```{r}

annotations <- readRDS('/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/clownfish_genome_files/clownfish_genome_annotations.rds')
clown_gene.table <- as.data.frame(annotations)

clown_fasta <- readRDS('/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/clownfish_genome_files/clownfish_fasta.rds')

clown_id_info <- read_csv('/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/clownfish_experiment_id_info.csv')

ambient_markers <- read_csv('/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/Katie/MZ_genome_files/M_zebra_UMD2a/ambient_markers_E.Caglayan2022.csv')

```

```{r echo=TRUE, message=FALSE, warning=FALSE, fig.height = 6, fig.width = 10}

s1.data <- Read10X_h5('/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/cellranger_outs/cellranger_seurat_files/s1/raw_feature_bc_matrix.h5')
s1 <- CreateSeuratObject(s1.data$`Gene Expression`)
dim(s1)

s1$orig.ident <- 'Pool_1'

rna <- s1.data$`Gene Expression`
atac <- s1.data$Peaks
eD.out <- emptydrops_multiome(count_matrix_rna=rna, count_matrix_atac=atac, verbose = T)
print("the number of cells detected is: ")
print(sum(eD.out$FDR_multi<0.001 & ! is.na(eD.out$FDR_multi)))

eD.out_multi <- eD.out
eD.out_multi$identity <- "fail"
eD.out_multi$identity[eD.out_multi$FDR_multi <= 0.001 & !is.na(eD.out_multi$FDR_multi) ] <- "pass"
observations1c <- data.frame("log_atac" = log10(eD.out_multi$Total_chromatin+0.1),
                             "log_rna" = log10(eD.out_multi$Total_RNA+0.1),
                             "identity" = eD.out_multi$identity)
lines <- data.frame(name=c("higher", "k-means", "lower"),
                    slope=c(eD.out_multi@metadata$k_means_slope, eD.out_multi@metadata$k_means_slope, eD.out_multi@metadata$k_means_slope),
                    intercept = c(eD.out_multi@metadata$higher_intercept, eD.out_multi@metadata$k_means_intercept, eD.out_multi@metadata$lower_intercept),
                    type=c("dashed", "solid", "dotted"))
emptyDrops_multi <- ggplot(observations1c, aes(x = log_atac, y = log_rna, color = identity)) + 
  geom_point(size=0.1) + 
  theme(
    panel.border = element_blank(),
    panel.background = element_rect("white"),
    panel.grid.major = element_blank(),
    panel.grid.minor = element_blank(),
    axis.line = element_line(colour = "black"),
    axis.text=element_text(size=10),
    legend.title = element_blank(),
    axis.title=element_text(size=10)
  ) + 
  scale_color_manual(values=c("red", "deepskyblue2") )+
  ggplot2::ggtitle(subtitle = 'EmptyDropsMultiome', sprintf("Clownfish Multiome: Pool_1 - Proportion of True Nuclei Detected", sum(eD.out$FDR_multi<0.001 & ! is.na(eD.out$FDR_multi))))+
  guides(colour = guide_legend(override.aes = list(size=5)))
emptyDrops_multi <- emptyDrops_multi + geom_abline(data = lines, aes(intercept = intercept, slope = slope, linetype = name))
emptyDrops_multi
ggsave("/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/QC/qc_plots/Pool_1_EmptyDropsMultiome_clownfish.pdf",
       height = 5, width = 6)

eD.out_multi_passed <- eD.out_multi$Row.names[eD.out_multi$identity == "pass"]
barcodes <- data.frame(Standard = eD.out_multi_passed)
write.table(barcodes, 
            file='/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/deconvolution/EmptyDropsMultiome/eDM_filtered_barcodes/Pool1_Clownfish_eDM.barcodes_passed.tsv', 
            quote=FALSE, sep='\t', col.names = FALSE, row.names = FALSE)
s1_eD.out_multi_passed <- as.data.frame(eD.out_multi)
colnames(s1_eD.out_multi_passed)[1] <- 'Barcode'
write.table(s1_eD.out_multi_passed, 
            file='/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/deconvolution/EmptyDropsMultiome/EmptyDropsMultiome_output/Pool1_Clownfish_EmptyDropsMultiome_output.tsv', 
            quote=FALSE, sep='\t', row.names = FALSE)

s1_emptyDrops_multi <- emptyDrops_multi

clown.s1_demulti <- read_csv('/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/deconvolution/souporcell_demuxlet_selected/s1_barcodes_sampleIDs.csv')

s1_good.cells <- as.character(barcodes$Standard)
s1 <- subset(s1, cells = s1_good.cells)
dim(s1)
s1_good.cells <- clown.s1_demulti$barcode
s1 <- subset(s1, cells = s1_good.cells)
dim(s1)

clown.s1_demulti$individual <- clown.s1_demulti$Sample
clown.s1_demulti$individual <- as.factor(clown.s1_demulti$individual)
s1$individual <- colnames(s1)
s1$individual <- clown.s1_demulti$individual[match(s1$individual, clown.s1_demulti$barcode)]
table(s1$individual)
dim(s1)

#################


s1_fragment_file = '/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/cellranger_outs/cellranger_seurat_files/s1/atac_fragments.tsv.gz'

# create a chromatin assay in the Seurat object
s1_atac <- CreateChromatinAssay(counts = s1.data$Peaks, 
                                fragments = s1_fragment_file, 
                                annotation = annotations, sep = c(":", "-"))

# only keep those barcodes passes QC stored in RNA assay
s1_barcodes <- Cells(s1_atac)[which(Cells(s1_atac) %in% Cells(s1))]
s1_atac <- subset(s1_atac, cells = s1_barcodes)

# create the multi-omics assay data containing both RNA and ATAC
s1[['ATAC']] <- s1_atac


################


mito <- rownames(s1)[grep('^KEG47-', rownames(s1))]
s1[['pct.mt']] <- PercentageFeatureSet(s1, pattern = '^KEG47-')

ribogenes <- c(rownames(s1)[grep('^rpl', rownames(s1))], rownames(s1)[grep('^rps', rownames(s1))])
ribogenes <- rownames(s1)[rownames(s1) %in% ribogenes]
s1[['pct.rb']] <- PercentageFeatureSet(s1, features = ribogenes)

ribosomal_mito_genes <- c(rownames(s1)[grep('^mrpl', rownames(s1))], rownames(s1)[grep('^mrps', rownames(s1))])
ribosomal_mito_genes <- rownames(s1)[rownames(s1) %in% ribosomal_mito_genes]
s1[['pct.mt.rb']] <- PercentageFeatureSet(s1, features = ribosomal_mito_genes)

coding <- unique(clown_gene.table$gene_id[clown_gene.table$gene_biotype == 'protein_coding'])
coding <- coding[which(! coding %in% c(mito, ribosomal_mito_genes, ribogenes))]
cgenes <- rownames(s1)[rownames(s1) %in% coding]
s1[['pct.cd']] <- PercentageFeatureSet(s1, features = cgenes)

lncRNA <- clown_gene.table$gene_id[clown_gene.table$gene_biotype == 'lncRNA']
snRNA <- clown_gene.table$gene_id[clown_gene.table$gene_biotype == 'snRNA']
snoRNA <- clown_gene.table$gene_id[clown_gene.table$gene_biotype == 'snoRNA']
nuclear <- unique(c(lncRNA, snRNA, snoRNA))
nuclear <- rownames(s1)[rownames(s1) %in% nuclear]
s1[['pct.nuclear']] <- PercentageFeatureSet(s1, features = nuclear)

ambient_markers$Gene <- tolower(ambient_markers$Gene)
ambient_markers$clown_homolog <- annotations$gene_id[match(ambient_markers$Gene, annotations$human_greatest_homolog, incomparables = T)]
ambient <- ambient_markers %>% dplyr::filter(PValue < 1e-3)
known_ambient <- rownames(s1)[which(ambient$clown_homolog %in% rownames(s1))]
ambient <- unique(c(known_ambient))
s1[['pct.ambient']] <- PercentageFeatureSet(s1, features = ambient)

s1 <- Add_Cell_Complexity(object = s1)
s1 <- Add_Top_Gene_Pct_Seurat(seurat_object = s1, num_top_genes = 50)
s1$genes_per_umi <- s1$nFeature_RNA/s1$nCount_RNA
dim(s1)


####################################


table(s1$individual)

s1_median_stats <- Median_Stats(seurat_object = s1, group_by_var = "individual", median_var = c('pct.mt', 'pct.cd', 'nCount_RNA', 'nFeature_RNA', 'nCount_ATAC', 'nFeature_ATAC'))
s1_median_stats

p1 <- QC_Plots_Genes(seurat_object = s1, low_cutoff = 250, high_cutoff = 4000, colors_use = brewer.pal(name = "Set2", n= 4), y_axis_log = TRUE, plot_median = TRUE, alpha = 0.1, group.by = 'individual')
p2 <- QC_Plots_UMIs(seurat_object = s1, low_cutoff = 250, high_cutoff = 10000, colors_use = brewer.pal(name = "Set2", n= 4), y_axis_log = TRUE, plot_median = TRUE, alpha = 0.1, group.by = 'individual')
p3 <- QC_Plots_Mito(seurat_object = s1, high_cutoff = 20, mito_name = 'pct.mt', colors_use = brewer.pal(name = "Set2", n= 4), group.by = 'individual')
p4 <- QC_Plots_Complexity(seurat_object = s1, high_cutoff = 0.88, colors_use = brewer.pal(name = "Set2", n= 4), plot_median = TRUE, alpha = 0.1, group.by = 'individual')
wrap_plots(p1, p2, p3, p4, ncol = 4)

qc.metrics <- as_tibble(
  s1[[]],
  rownames="Cell.Barcode"
)
qc.metrics %>%
  ggplot(aes(pct.mt)) + 
  geom_histogram(binwidth = 1.0, fill="#C93312", colour="red4") +
  ggtitle("Clownfish Pool_1 QC Metrics: Distribution of Percent Mitochondria \n \n") +
  geom_vline(xintercept = 20, color = 'black', linetype = 'longdash', linewidth = 0.75) + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.mt) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=pct.mt)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_1 QC Metrics: % MT genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.cd) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=pct.cd)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_1 QC Metrics: % coding genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.nuclear) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=pct.nuclear)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_1 QC Metrics: % nuclear genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.ambient) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=percent_top50)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_1 QC Metrics: % Top 50 Expressing genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.ambient) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=log10GenesPerUMI)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_1 QC Metrics: % Top Expressing genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))

VlnPlot(s1, 
        features = c('nCount_RNA', 'nFeature_RNA','nCount_ATAC','nFeature_ATAC'), 
        group.by = "individual", 
        ncol = 2,
        log = T, 
        pt.size = 0.1, 
        alpha = 0.1) + NoLegend()

VlnPlot(s1, features = c('pct.mt', 'pct.rb', 'pct.mt.rb', 'pct.cd','pct.ambient', 'pct.nuclear'), 
        group.by = "individual", 
        ncol = 3,
        log = F, 
        pt.size = 0.1, 
        alpha = 0.1) + NoLegend()

VlnPlot(s1, features = c('log10GenesPerUMI', 'percent_top50'), 
        group.by = "individual", 
        ncol = 2,
        log = F, 
        pt.size = 0.1, 
        alpha = 0.1) + NoLegend()

FeatureScatter(s1, 
               feature1 = 'nCount_RNA', 
               feature2 = 'nFeature_RNA', 
               split.by = 'individual', 
               group.by = 'individual',
               shuffle = T, 
               log = T)
FeatureScatter(s1, 
               feature1 = 'nCount_ATAC', 
               feature2 = 'nFeature_ATAC', 
               split.by = 'individual',
               group.by = 'individual',
               shuffle = T, 
               log = T)

saveRDS(s1, '/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/QC/qc_gex.atac_outs/s1_clownfish_gex.atac_raw.rds')

```


```{r echo=TRUE, message=FALSE, warning=FALSE, fig.height = 6, fig.width = 10}

s2.data <- Read10X_h5('/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/cellranger_outs/cellranger_seurat_files/s2/raw_feature_bc_matrix.h5')
s2 <- CreateSeuratObject(s2.data$`Gene Expression`)
dim(s2)

s2$orig.ident <- 'Pool_2'

rna <- s2.data$`Gene Expression`
atac <- s2.data$Peaks
eD.out <- emptydrops_multiome(count_matrix_rna=rna, count_matrix_atac=atac, verbose = T)
print("the number of cells detected is: ")
print(sum(eD.out$FDR_multi<0.001 & ! is.na(eD.out$FDR_multi)))

eD.out_multi <- eD.out
eD.out_multi$identity <- "fail"
eD.out_multi$identity[eD.out_multi$FDR_multi <= 0.001 & !is.na(eD.out_multi$FDR_multi) ] <- "pass"
observations2c <- data.frame("log_atac" = log10(eD.out_multi$Total_chromatin+0.1),
                             "log_rna" = log10(eD.out_multi$Total_RNA+0.1),
                             "identity" = eD.out_multi$identity)
lines <- data.frame(name=c("higher", "k-means", "lower"),
                    slope=c(eD.out_multi@metadata$k_means_slope, eD.out_multi@metadata$k_means_slope, eD.out_multi@metadata$k_means_slope),
                    intercept = c(eD.out_multi@metadata$higher_intercept, eD.out_multi@metadata$k_means_intercept, eD.out_multi@metadata$lower_intercept),
                    type=c("dashed", "solid", "dotted"))
emptyDrops_multi <- ggplot(observations2c, aes(x = log_atac, y = log_rna, color = identity)) + 
  geom_point(size=0.1) + 
  theme(
    panel.border = element_blank(),
    panel.background = element_rect("white"),
    panel.grid.major = element_blank(),
    panel.grid.minor = element_blank(),
    axis.line = element_line(colour = "black"),
    axis.text=element_text(size=10),
    legend.title = element_blank(),
    axis.title=element_text(size=10)
  ) + 
  scale_color_manual(values=c("red", "deepskyblue2") )+
  ggplot2::ggtitle(subtitle = 'EmptyDropsMultiome', sprintf("Clownfish Multiome: Pool_2 - Proportion of True Nuclei Detected", sum(eD.out$FDR_multi<0.001 & ! is.na(eD.out$FDR_multi))))+
  guides(colour = guide_legend(override.aes = list(size=5)))
emptyDrops_multi <- emptyDrops_multi + geom_abline(data = lines, aes(intercept = intercept, slope = slope, linetype = name))
emptyDrops_multi
ggsave("/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/QC/qc_plots/Pool_2_EmptyDropsMultiome_clownfish.pdf",
       height = 5, width = 6)

eD.out_multi_passed <- eD.out_multi$Row.names[eD.out_multi$identity == "pass"]
barcodes <- data.frame(Standard = eD.out_multi_passed)
write.table(barcodes, 
            file='/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/deconvolution/EmptyDropsMultiome/eDM_filtered_barcodes/Pool2_Clownfish_eDM.barcodes_passed.tsv', 
            quote=FALSE, sep='\t', col.names = FALSE, row.names = FALSE)
s2_eD.out_multi_passed <- as.data.frame(eD.out_multi)
colnames(s2_eD.out_multi_passed)[1] <- 'Barcode'
write.table(s2_eD.out_multi_passed, 
            file='/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/deconvolution/EmptyDropsMultiome/EmptyDropsMultiome_output/Pool2_Clownfish_EmptyDropsMultiome_output.tsv', 
            quote=FALSE, sep='\t', row.names = FALSE)

s2_emptyDrops_multi <- emptyDrops_multi

clown.s2_demulti <- read_csv('/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/deconvolution/souporcell_demuxlet_selected/s2_barcodes_sampleIDs.csv')

s2_good.cells <- as.character(barcodes$Standard)
s2 <- subset(s2, cells = s2_good.cells)
dim(s2)
s2_good.cells <- clown.s2_demulti$barcode
s2 <- subset(s2, cells = s2_good.cells)
dim(s2)

clown.s2_demulti$individual <- clown.s2_demulti$Sample
clown.s2_demulti$individual <- as.factor(clown.s2_demulti$individual)
s2$individual <- colnames(s2)
s2$individual <- clown.s2_demulti$individual[match(s2$individual, clown.s2_demulti$barcode)]
table(s2$individual)
dim(s2)

#################


s2_fragment_file = '/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/cellranger_outs/cellranger_seurat_files/s2/atac_fragments.tsv.gz'

# create a chromatin assay in the Seurat object
s2_atac <- CreateChromatinAssay(counts = s2.data$Peaks, 
                                fragments = s2_fragment_file, 
                                annotation = annotations, sep = c(":", "-"))

# only keep those barcodes passes QC stored in RNA assay
s2_barcodes <- Cells(s2_atac)[which(Cells(s2_atac) %in% Cells(s2))]
s2_atac <- subset(s2_atac, cells = s2_barcodes)

# create the multi-omics assay data containing both RNA and ATAC
s2[['ATAC']] <- s2_atac


################


mito <- rownames(s2)[grep('^KEG47-', rownames(s2))]
s2[['pct.mt']] <- PercentageFeatureSet(s2, pattern = '^KEG47-')

ribogenes <- c(rownames(s2)[grep('^rpl', rownames(s2))], rownames(s2)[grep('^rps', rownames(s2))])
ribogenes <- rownames(s2)[rownames(s2) %in% ribogenes]
s2[['pct.rb']] <- PercentageFeatureSet(s2, features = ribogenes)

ribosomal_mito_genes <- c(rownames(s2)[grep('^mrpl', rownames(s2))], rownames(s2)[grep('^mrps', rownames(s2))])
ribosomal_mito_genes <- rownames(s2)[rownames(s2) %in% ribosomal_mito_genes]
s2[['pct.mt.rb']] <- PercentageFeatureSet(s2, features = ribosomal_mito_genes)

coding <- unique(clown_gene.table$gene_id[clown_gene.table$gene_biotype == 'protein_coding'])
coding <- coding[which(! coding %in% c(mito, ribosomal_mito_genes, ribogenes))]
cgenes <- rownames(s2)[rownames(s2) %in% coding]
s2[['pct.cd']] <- PercentageFeatureSet(s2, features = cgenes)

lncRNA <- clown_gene.table$gene_id[clown_gene.table$gene_biotype == 'lncRNA']
snRNA <- clown_gene.table$gene_id[clown_gene.table$gene_biotype == 'snRNA']
snoRNA <- clown_gene.table$gene_id[clown_gene.table$gene_biotype == 'snoRNA']
nuclear <- unique(c(lncRNA, snRNA, snoRNA))
nuclear <- rownames(s2)[rownames(s2) %in% nuclear]
s2[['pct.nuclear']] <- PercentageFeatureSet(s2, features = nuclear)

ambient_markers$Gene <- tolower(ambient_markers$Gene)
ambient_markers$clown_homolog <- annotations$gene_id[match(ambient_markers$Gene, annotations$human_greatest_homolog, incomparables = T)]
ambient <- ambient_markers %>% dplyr::filter(PValue < 1e-3)
known_ambient <- rownames(s2)[which(ambient$clown_homolog %in% rownames(s2))]
ambient <- unique(c(known_ambient))
s2[['pct.ambient']] <- PercentageFeatureSet(s2, features = ambient)

s2 <- Add_Cell_Complexity(object = s2)
s2 <- Add_Top_Gene_Pct_Seurat(seurat_object = s2, num_top_genes = 50)
s2$genes_per_umi <- s2$nFeature_RNA/s2$nCount_RNA
dim(s2)


####################################


table(s2$individual)

s2_median_stats <- Median_Stats(seurat_object = s2, group_by_var = "individual", median_var = c('pct.mt', 'pct.cd', 'nCount_RNA', 'nFeature_RNA', 'nCount_ATAC', 'nFeature_ATAC'))
s2_median_stats

p1 <- QC_Plots_Genes(seurat_object = s2, low_cutoff = 250, high_cutoff = 4000, colors_use = brewer.pal(name = "Set2", n= 4), y_axis_log = TRUE, plot_median = TRUE, alpha = 0.1, group.by = 'individual')
p2 <- QC_Plots_UMIs(seurat_object = s2, low_cutoff = 250, high_cutoff = 10000, colors_use = brewer.pal(name = "Set2", n= 4), y_axis_log = TRUE, plot_median = TRUE, alpha = 0.1, group.by = 'individual')
p3 <- QC_Plots_Mito(seurat_object = s2, high_cutoff = 20, mito_name = 'pct.mt', colors_use = brewer.pal(name = "Set2", n= 4), group.by = 'individual')
p4 <- QC_Plots_Complexity(seurat_object = s2, high_cutoff = 0.88, colors_use = brewer.pal(name = "Set2", n= 4), plot_median = TRUE, alpha = 0.1, group.by = 'individual')
wrap_plots(p1, p2, p3, p4, ncol = 4)

qc.metrics <- as_tibble(
  s2[[]],
  rownames="Cell.Barcode"
)
qc.metrics %>%
  ggplot(aes(pct.mt)) + 
  geom_histogram(binwidth = 1.0, fill="#C93312", colour="red4") +
  ggtitle("Clownfish Pool_2 QC Metrics: Distribution of Percent Mitochondria \n \n") +
  geom_vline(xintercept = 20, color = 'black', linetype = 'longdash', linewidth = 0.75) + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.mt) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=pct.mt)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_2 QC Metrics: % MT genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.cd) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=pct.cd)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_2 QC Metrics: % coding genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.nuclear) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=pct.nuclear)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_2 QC Metrics: % nuclear genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.ambient) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=percent_top50)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_2 QC Metrics: % Top 50 Expressing genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.ambient) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=log10GenesPerUMI)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_2 QC Metrics: % Top Expressing genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))

VlnPlot(s2, 
        features = c('nCount_RNA', 'nFeature_RNA','nCount_ATAC','nFeature_ATAC'), 
        group.by = "individual", 
        ncol = 2,
        log = T, 
        pt.size = 0.1, 
        alpha = 0.1) + NoLegend()

VlnPlot(s2, features = c('pct.mt', 'pct.rb', 'pct.mt.rb', 'pct.cd','pct.ambient', 'pct.nuclear'), 
        group.by = "individual", 
        ncol = 3,
        log = F, 
        pt.size = 0.1, 
        alpha = 0.1) + NoLegend()

VlnPlot(s2, features = c('log10GenesPerUMI', 'percent_top50'), 
        group.by = "individual", 
        ncol = 2,
        log = F, 
        pt.size = 0.1, 
        alpha = 0.1) + NoLegend()

FeatureScatter(s2, 
               feature1 = 'nCount_RNA', 
               feature2 = 'nFeature_RNA', 
               split.by = 'individual', 
               group.by = 'individual',
               shuffle = T, 
               log = T)
FeatureScatter(s2, 
               feature1 = 'nCount_ATAC', 
               feature2 = 'nFeature_ATAC', 
               split.by = 'individual',
               group.by = 'individual',
               shuffle = T, 
               log = T)

saveRDS(s2, '/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/QC/qc_gex.atac_outs/s2_clownfish_gex.atac_raw.rds')

```



```{r echo=TRUE, message=FALSE, warning=FALSE, fig.height = 6, fig.width = 10}

s3.data <- Read10X_h5('/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/cellranger_outs/cellranger_seurat_files/s3/raw_feature_bc_matrix.h5')
s3 <- CreateSeuratObject(s3.data$`Gene Expression`)
dim(s3)

s3$orig.ident <- 'Pool_3'

rna <- s3.data$`Gene Expression`
atac <- s3.data$Peaks
eD.out <- emptydrops_multiome(count_matrix_rna=rna, count_matrix_atac=atac, verbose = T)
print("the number of cells detected is: ")
print(sum(eD.out$FDR_multi<0.001 & ! is.na(eD.out$FDR_multi)))

eD.out_multi <- eD.out
eD.out_multi$identity <- "fail"
eD.out_multi$identity[eD.out_multi$FDR_multi <= 0.001 & !is.na(eD.out_multi$FDR_multi) ] <- "pass"
observations3c <- data.frame("log_atac" = log10(eD.out_multi$Total_chromatin+0.1),
                             "log_rna" = log10(eD.out_multi$Total_RNA+0.1),
                             "identity" = eD.out_multi$identity)
lines <- data.frame(name=c("higher", "k-means", "lower"),
                    slope=c(eD.out_multi@metadata$k_means_slope, eD.out_multi@metadata$k_means_slope, eD.out_multi@metadata$k_means_slope),
                    intercept = c(eD.out_multi@metadata$higher_intercept, eD.out_multi@metadata$k_means_intercept, eD.out_multi@metadata$lower_intercept),
                    type=c("dashed", "solid", "dotted"))
emptyDrops_multi <- ggplot(observations3c, aes(x = log_atac, y = log_rna, color = identity)) + 
  geom_point(size=0.1) + 
  theme(
    panel.border = element_blank(),
    panel.background = element_rect("white"),
    panel.grid.major = element_blank(),
    panel.grid.minor = element_blank(),
    axis.line = element_line(colour = "black"),
    axis.text=element_text(size=10),
    legend.title = element_blank(),
    axis.title=element_text(size=10)
  ) + 
  scale_color_manual(values=c("red", "deepskyblue2") )+
  ggplot2::ggtitle(subtitle = 'EmptyDropsMultiome', sprintf("Clownfish Multiome: Pool_3 - Proportion of True Nuclei Detected", sum(eD.out$FDR_multi<0.001 & ! is.na(eD.out$FDR_multi))))+
  guides(colour = guide_legend(override.aes = list(size=5)))
emptyDrops_multi <- emptyDrops_multi + geom_abline(data = lines, aes(intercept = intercept, slope = slope, linetype = name))
emptyDrops_multi
ggsave("/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/QC/qc_plots/Pool_3_EmptyDropsMultiome_clownfish.pdf",
       height = 5, width = 6)

eD.out_multi_passed <- eD.out_multi$Row.names[eD.out_multi$identity == "pass"]
barcodes <- data.frame(Standard = eD.out_multi_passed)
write.table(barcodes, 
            file='/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/deconvolution/EmptyDropsMultiome/eDM_filtered_barcodes/Pool3_Clownfish_eDM.barcodes_passed.tsv', 
            quote=FALSE, sep='\t', col.names = FALSE, row.names = FALSE)
s3_eD.out_multi_passed <- as.data.frame(eD.out_multi)
colnames(s3_eD.out_multi_passed)[1] <- 'Barcode'
write.table(s3_eD.out_multi_passed, 
            file='/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/deconvolution/EmptyDropsMultiome/EmptyDropsMultiome_output/Pool3_Clownfish_EmptyDropsMultiome_output.tsv', 
            quote=FALSE, sep='\t', row.names = FALSE)

s3_emptyDrops_multi <- emptyDrops_multi

clown.s3_demulti <- read_csv('/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/deconvolution/souporcell_demuxlet_selected/s3_barcodes_sampleIDs.csv')

s3_good.cells <- as.character(barcodes$Standard)
s3 <- subset(s3, cells = s3_good.cells)
dim(s3)
s3_good.cells <- clown.s3_demulti$barcode
s3 <- subset(s3, cells = s3_good.cells)
dim(s3)

clown.s3_demulti$individual <- clown.s3_demulti$Sample
clown.s3_demulti$individual <- as.factor(clown.s3_demulti$individual)
s3$individual <- colnames(s3)
s3$individual <- clown.s3_demulti$individual[match(s3$individual, clown.s3_demulti$barcode)]
table(s3$individual)
dim(s3)

#################


s3_fragment_file = '/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/cellranger_outs/cellranger_seurat_files/s3/atac_fragments.tsv.gz'

# create a chromatin assay in the Seurat object
s3_atac <- CreateChromatinAssay(counts = s3.data$Peaks, 
                                fragments = s3_fragment_file, 
                                annotation = annotations, sep = c(":", "-"))

# only keep those barcodes passes QC stored in RNA assay
s3_barcodes <- Cells(s3_atac)[which(Cells(s3_atac) %in% Cells(s3))]
s3_atac <- subset(s3_atac, cells = s3_barcodes)

# create the multi-omics assay data containing both RNA and ATAC
s3[['ATAC']] <- s3_atac


################


mito <- rownames(s3)[grep('^KEG47-', rownames(s3))]
s3[['pct.mt']] <- PercentageFeatureSet(s3, pattern = '^KEG47-')

ribogenes <- c(rownames(s3)[grep('^rpl', rownames(s3))], rownames(s3)[grep('^rps', rownames(s3))])
ribogenes <- rownames(s3)[rownames(s3) %in% ribogenes]
s3[['pct.rb']] <- PercentageFeatureSet(s3, features = ribogenes)

ribosomal_mito_genes <- c(rownames(s3)[grep('^mrpl', rownames(s3))], rownames(s3)[grep('^mrps', rownames(s3))])
ribosomal_mito_genes <- rownames(s3)[rownames(s3) %in% ribosomal_mito_genes]
s3[['pct.mt.rb']] <- PercentageFeatureSet(s3, features = ribosomal_mito_genes)

coding <- unique(clown_gene.table$gene_id[clown_gene.table$gene_biotype == 'protein_coding'])
coding <- coding[which(! coding %in% c(mito, ribosomal_mito_genes, ribogenes))]
cgenes <- rownames(s3)[rownames(s3) %in% coding]
s3[['pct.cd']] <- PercentageFeatureSet(s3, features = cgenes)

lncRNA <- clown_gene.table$gene_id[clown_gene.table$gene_biotype == 'lncRNA']
snRNA <- clown_gene.table$gene_id[clown_gene.table$gene_biotype == 'snRNA']
snoRNA <- clown_gene.table$gene_id[clown_gene.table$gene_biotype == 'snoRNA']
nuclear <- unique(c(lncRNA, snRNA, snoRNA))
nuclear <- rownames(s3)[rownames(s3) %in% nuclear]
s3[['pct.nuclear']] <- PercentageFeatureSet(s3, features = nuclear)

ambient_markers$Gene <- tolower(ambient_markers$Gene)
ambient_markers$clown_homolog <- annotations$gene_id[match(ambient_markers$Gene, annotations$human_greatest_homolog, incomparables = T)]
ambient <- ambient_markers %>% dplyr::filter(PValue < 1e-3)
known_ambient <- rownames(s3)[which(ambient$clown_homolog %in% rownames(s3))]
ambient <- unique(c(known_ambient))
s3[['pct.ambient']] <- PercentageFeatureSet(s3, features = ambient)

s3 <- Add_Cell_Complexity(object = s3)
s3 <- Add_Top_Gene_Pct_Seurat(seurat_object = s3, num_top_genes = 50)
s3$genes_per_umi <- s3$nFeature_RNA/s3$nCount_RNA
dim(s3)


####################################


table(s3$individual)

s3_median_stats <- Median_Stats(seurat_object = s3, group_by_var = "individual", median_var = c('pct.mt', 'pct.cd', 'nCount_RNA', 'nFeature_RNA', 'nCount_ATAC', 'nFeature_ATAC'))
s3_median_stats

p1 <- QC_Plots_Genes(seurat_object = s3, low_cutoff = 250, high_cutoff = 4000, colors_use = brewer.pal(name = "Set2", n= 4), y_axis_log = TRUE, plot_median = TRUE, alpha = 0.1, group.by = 'individual')
p2 <- QC_Plots_UMIs(seurat_object = s3, low_cutoff = 250, high_cutoff = 10000, colors_use = brewer.pal(name = "Set2", n= 4), y_axis_log = TRUE, plot_median = TRUE, alpha = 0.1, group.by = 'individual')
p3 <- QC_Plots_Mito(seurat_object = s3, high_cutoff = 20, mito_name = 'pct.mt', colors_use = brewer.pal(name = "Set2", n= 4), group.by = 'individual')
p4 <- QC_Plots_Complexity(seurat_object = s3, high_cutoff = 0.88, colors_use = brewer.pal(name = "Set2", n= 4), plot_median = TRUE, alpha = 0.1, group.by = 'individual')
wrap_plots(p1, p2, p3, p4, ncol = 4)

qc.metrics <- as_tibble(
  s3[[]],
  rownames="Cell.Barcode"
)
qc.metrics %>%
  ggplot(aes(pct.mt)) + 
  geom_histogram(binwidth = 1.0, fill="#C93312", colour="red4") +
  ggtitle("Clownfish Pool_3 QC Metrics: Distribution of Percent Mitochondria \n \n") +
  geom_vline(xintercept = 20, color = 'black', linetype = 'longdash', linewidth = 0.75) + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.mt) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=pct.mt)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_3 QC Metrics: % MT genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.cd) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=pct.cd)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_3 QC Metrics: % coding genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.nuclear) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=pct.nuclear)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_3 QC Metrics: % nuclear genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.ambient) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=percent_top50)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_3 QC Metrics: % Top 50 Expressing genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.ambient) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=log10GenesPerUMI)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_3 QC Metrics: % Top Expressing genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))

VlnPlot(s3, 
        features = c('nCount_RNA', 'nFeature_RNA','nCount_ATAC','nFeature_ATAC'), 
        group.by = "individual", 
        ncol = 2,
        log = T, 
        pt.size = 0.1, 
        alpha = 0.1) + NoLegend()

VlnPlot(s3, features = c('pct.mt', 'pct.rb', 'pct.mt.rb', 'pct.cd','pct.ambient', 'pct.nuclear'), 
        group.by = "individual", 
        ncol = 3,
        log = F, 
        pt.size = 0.1, 
        alpha = 0.1) + NoLegend()

VlnPlot(s3, features = c('log10GenesPerUMI', 'percent_top50'), 
        group.by = "individual", 
        ncol = 2,
        log = F, 
        pt.size = 0.1, 
        alpha = 0.1) + NoLegend()

FeatureScatter(s3, 
               feature1 = 'nCount_RNA', 
               feature2 = 'nFeature_RNA', 
               split.by = 'individual', 
               group.by = 'individual',
               shuffle = T, 
               log = T)
FeatureScatter(s3, 
               feature1 = 'nCount_ATAC', 
               feature2 = 'nFeature_ATAC', 
               split.by = 'individual',
               group.by = 'individual',
               shuffle = T, 
               log = T)

saveRDS(s3, '/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/QC/qc_gex.atac_outs/s3_clownfish_gex.atac_raw.rds')

```



```{r echo=TRUE, message=FALSE, warning=FALSE, fig.height = 6, fig.width = 10}

s4.data <- Read10X_h5('/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/cellranger_outs/cellranger_seurat_files/s4/raw_feature_bc_matrix.h5')
s4 <- CreateSeuratObject(s4.data$`Gene Expression`)
dim(s4)

s4$orig.ident <- 'Pool_4'

rna <- s4.data$`Gene Expression`
atac <- s4.data$Peaks
eD.out <- emptydrops_multiome(count_matrix_rna=rna, count_matrix_atac=atac, verbose = T)
print("the number of cells detected is: ")
print(sum(eD.out$FDR_multi<0.001 & ! is.na(eD.out$FDR_multi)))

eD.out_multi <- eD.out
eD.out_multi$identity <- "fail"
eD.out_multi$identity[eD.out_multi$FDR_multi <= 0.001 & !is.na(eD.out_multi$FDR_multi) ] <- "pass"
observations4c <- data.frame("log_atac" = log10(eD.out_multi$Total_chromatin+0.1),
                             "log_rna" = log10(eD.out_multi$Total_RNA+0.1),
                             "identity" = eD.out_multi$identity)
lines <- data.frame(name=c("higher", "k-means", "lower"),
                    slope=c(eD.out_multi@metadata$k_means_slope, eD.out_multi@metadata$k_means_slope, eD.out_multi@metadata$k_means_slope),
                    intercept = c(eD.out_multi@metadata$higher_intercept, eD.out_multi@metadata$k_means_intercept, eD.out_multi@metadata$lower_intercept),
                    type=c("dashed", "solid", "dotted"))
emptyDrops_multi <- ggplot(observations4c, aes(x = log_atac, y = log_rna, color = identity)) + 
  geom_point(size=0.1) + 
  theme(
    panel.border = element_blank(),
    panel.background = element_rect("white"),
    panel.grid.major = element_blank(),
    panel.grid.minor = element_blank(),
    axis.line = element_line(colour = "black"),
    axis.text=element_text(size=10),
    legend.title = element_blank(),
    axis.title=element_text(size=10)
  ) + 
  scale_color_manual(values=c("red", "deepskyblue2") )+
  ggplot2::ggtitle(subtitle = 'EmptyDropsMultiome', sprintf("Clownfish Multiome: Pool_4 - Proportion of True Nuclei Detected", sum(eD.out$FDR_multi<0.001 & ! is.na(eD.out$FDR_multi))))+
  guides(colour = guide_legend(override.aes = list(size=5)))
emptyDrops_multi <- emptyDrops_multi + geom_abline(data = lines, aes(intercept = intercept, slope = slope, linetype = name))
emptyDrops_multi
ggsave("/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/QC/qc_plots/Pool_4_EmptyDropsMultiome_clownfish.pdf",
       height = 5, width = 6)

eD.out_multi_passed <- eD.out_multi$Row.names[eD.out_multi$identity == "pass"]
barcodes <- data.frame(Standard = eD.out_multi_passed)
write.table(barcodes, 
            file='/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/deconvolution/EmptyDropsMultiome/eDM_filtered_barcodes/Pool4_Clownfish_eDM.barcodes_passed.tsv', 
            quote=FALSE, sep='\t', col.names = FALSE, row.names = FALSE)
s4_eD.out_multi_passed <- as.data.frame(eD.out_multi)
colnames(s4_eD.out_multi_passed)[1] <- 'Barcode'
write.table(s4_eD.out_multi_passed, 
            file='/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/deconvolution/EmptyDropsMultiome/EmptyDropsMultiome_output/Pool4_Clownfish_EmptyDropsMultiome_output.tsv', 
            quote=FALSE, sep='\t', row.names = FALSE)

s4_emptyDrops_multi <- emptyDrops_multi

clown.s4_demulti <- read_csv('/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/deconvolution/souporcell_demuxlet_selected/s4_barcodes_sampleIDs.csv')

s4_good.cells <- as.character(barcodes$Standard)
s4 <- subset(s4, cells = s4_good.cells)
dim(s4)
s4_good.cells <- clown.s4_demulti$barcode
s4 <- subset(s4, cells = s4_good.cells)
dim(s4)

clown.s4_demulti$individual <- clown.s4_demulti$Sample
clown.s4_demulti$individual <- as.factor(clown.s4_demulti$individual)
s4$individual <- colnames(s4)
s4$individual <- clown.s4_demulti$individual[match(s4$individual, clown.s4_demulti$barcode)]
table(s4$individual)
dim(s4)

#################


s4_fragment_file = '/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/cellranger_outs/cellranger_seurat_files/s4/atac_fragments.tsv.gz'

# create a chromatin assay in the Seurat object
s4_atac <- CreateChromatinAssay(counts = s4.data$Peaks, 
                                fragments = s4_fragment_file, 
                                annotation = annotations, sep = c(":", "-"))

# only keep those barcodes passes QC stored in RNA assay
s4_barcodes <- Cells(s4_atac)[which(Cells(s4_atac) %in% Cells(s4))]
s4_atac <- subset(s4_atac, cells = s4_barcodes)

# create the multi-omics assay data containing both RNA and ATAC
s4[['ATAC']] <- s4_atac


################


mito <- rownames(s4)[grep('^KEG47-', rownames(s4))]
s4[['pct.mt']] <- PercentageFeatureSet(s4, pattern = '^KEG47-')

ribogenes <- c(rownames(s4)[grep('^rpl', rownames(s4))], rownames(s4)[grep('^rps', rownames(s4))])
ribogenes <- rownames(s4)[rownames(s4) %in% ribogenes]
s4[['pct.rb']] <- PercentageFeatureSet(s4, features = ribogenes)

ribosomal_mito_genes <- c(rownames(s4)[grep('^mrpl', rownames(s4))], rownames(s4)[grep('^mrps', rownames(s4))])
ribosomal_mito_genes <- rownames(s4)[rownames(s4) %in% ribosomal_mito_genes]
s4[['pct.mt.rb']] <- PercentageFeatureSet(s4, features = ribosomal_mito_genes)

coding <- unique(clown_gene.table$gene_id[clown_gene.table$gene_biotype == 'protein_coding'])
coding <- coding[which(! coding %in% c(mito, ribosomal_mito_genes, ribogenes))]
cgenes <- rownames(s4)[rownames(s4) %in% coding]
s4[['pct.cd']] <- PercentageFeatureSet(s4, features = cgenes)

lncRNA <- clown_gene.table$gene_id[clown_gene.table$gene_biotype == 'lncRNA']
snRNA <- clown_gene.table$gene_id[clown_gene.table$gene_biotype == 'snRNA']
snoRNA <- clown_gene.table$gene_id[clown_gene.table$gene_biotype == 'snoRNA']
nuclear <- unique(c(lncRNA, snRNA, snoRNA))
nuclear <- rownames(s4)[rownames(s4) %in% nuclear]
s4[['pct.nuclear']] <- PercentageFeatureSet(s4, features = nuclear)

ambient_markers$Gene <- tolower(ambient_markers$Gene)
ambient_markers$clown_homolog <- annotations$gene_id[match(ambient_markers$Gene, annotations$human_greatest_homolog, incomparables = T)]
ambient <- ambient_markers %>% dplyr::filter(PValue < 1e-3)
known_ambient <- rownames(s4)[which(ambient$clown_homolog %in% rownames(s4))]
ambient <- unique(c(known_ambient))
s4[['pct.ambient']] <- PercentageFeatureSet(s4, features = ambient)

s4 <- Add_Cell_Complexity(object = s4)
s4 <- Add_Top_Gene_Pct_Seurat(seurat_object = s4, num_top_genes = 50)
s4$genes_per_umi <- s4$nFeature_RNA/s4$nCount_RNA
dim(s4)


####################################


table(s4$individual)

s4_median_stats <- Median_Stats(seurat_object = s4, group_by_var = "individual", median_var = c('pct.mt', 'pct.cd', 'nCount_RNA', 'nFeature_RNA', 'nCount_ATAC', 'nFeature_ATAC'))
s4_median_stats

p1 <- QC_Plots_Genes(seurat_object = s4, low_cutoff = 250, high_cutoff = 4000, colors_use = brewer.pal(name = "Set2", n= 4), y_axis_log = TRUE, plot_median = TRUE, alpha = 0.1, group.by = 'individual')
p2 <- QC_Plots_UMIs(seurat_object = s4, low_cutoff = 250, high_cutoff = 10000, colors_use = brewer.pal(name = "Set2", n= 4), y_axis_log = TRUE, plot_median = TRUE, alpha = 0.1, group.by = 'individual')
p3 <- QC_Plots_Mito(seurat_object = s4, high_cutoff = 20, mito_name = 'pct.mt', colors_use = brewer.pal(name = "Set2", n= 4), group.by = 'individual')
p4 <- QC_Plots_Complexity(seurat_object = s4, high_cutoff = 0.88, colors_use = brewer.pal(name = "Set2", n= 4), plot_median = TRUE, alpha = 0.1, group.by = 'individual')
wrap_plots(p1, p2, p3, p4, ncol = 4)

qc.metrics <- as_tibble(
  s4[[]],
  rownames="Cell.Barcode"
)
qc.metrics %>%
  ggplot(aes(pct.mt)) + 
  geom_histogram(binwidth = 1.0, fill="#C93312", colour="red4") +
  ggtitle("Clownfish Pool_4 QC Metrics: Distribution of Percent Mitochondria \n \n") +
  geom_vline(xintercept = 20, color = 'black', linetype = 'longdash', linewidth = 0.75) + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.mt) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=pct.mt)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_4 QC Metrics: % MT genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.cd) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=pct.cd)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_4 QC Metrics: % coding genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.nuclear) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=pct.nuclear)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_4 QC Metrics: % nuclear genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.ambient) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=percent_top50)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_4 QC Metrics: % Top 50 Expressing genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.ambient) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=log10GenesPerUMI)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_4 QC Metrics: % Top Expressing genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))

VlnPlot(s4, 
        features = c('nCount_RNA', 'nFeature_RNA','nCount_ATAC','nFeature_ATAC'), 
        group.by = "individual", 
        ncol = 2,
        log = T, 
        pt.size = 0.1, 
        alpha = 0.1) + NoLegend()

VlnPlot(s4, features = c('pct.mt', 'pct.rb', 'pct.mt.rb', 'pct.cd','pct.ambient', 'pct.nuclear'), 
        group.by = "individual", 
        ncol = 3,
        log = F, 
        pt.size = 0.1, 
        alpha = 0.1) + NoLegend()

VlnPlot(s4, features = c('log10GenesPerUMI', 'percent_top50'), 
        group.by = "individual", 
        ncol = 2,
        log = F, 
        pt.size = 0.1, 
        alpha = 0.1) + NoLegend()

FeatureScatter(s4, 
               feature1 = 'nCount_RNA', 
               feature2 = 'nFeature_RNA', 
               split.by = 'individual', 
               group.by = 'individual',
               shuffle = T, 
               log = T)
FeatureScatter(s4, 
               feature1 = 'nCount_ATAC', 
               feature2 = 'nFeature_ATAC', 
               split.by = 'individual',
               group.by = 'individual',
               shuffle = T, 
               log = T)

saveRDS(s4, '/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/QC/qc_gex.atac_outs/s4_clownfish_gex.atac_raw.rds')

```



```{r echo=TRUE, message=FALSE, warning=FALSE, fig.height = 6, fig.width = 10}

s5.data <- Read10X_h5('/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/cellranger_outs/cellranger_seurat_files/s5/raw_feature_bc_matrix.h5')
s5 <- CreateSeuratObject(s5.data$`Gene Expression`)
dim(s5)

s5$orig.ident <- 'Pool_5'

rna <- s5.data$`Gene Expression`
atac <- s5.data$Peaks
eD.out <- emptydrops_multiome(count_matrix_rna=rna, count_matrix_atac=atac, verbose = T)
print("the number of cells detected is: ")
print(sum(eD.out$FDR_multi<0.001 & ! is.na(eD.out$FDR_multi)))

eD.out_multi <- eD.out
eD.out_multi$identity <- "fail"
eD.out_multi$identity[eD.out_multi$FDR_multi <= 0.001 & !is.na(eD.out_multi$FDR_multi) ] <- "pass"
observations5c <- data.frame("log_atac" = log10(eD.out_multi$Total_chromatin+0.1),
                             "log_rna" = log10(eD.out_multi$Total_RNA+0.1),
                             "identity" = eD.out_multi$identity)
lines <- data.frame(name=c("higher", "k-means", "lower"),
                    slope=c(eD.out_multi@metadata$k_means_slope, eD.out_multi@metadata$k_means_slope, eD.out_multi@metadata$k_means_slope),
                    intercept = c(eD.out_multi@metadata$higher_intercept, eD.out_multi@metadata$k_means_intercept, eD.out_multi@metadata$lower_intercept),
                    type=c("dashed", "solid", "dotted"))
emptyDrops_multi <- ggplot(observations5c, aes(x = log_atac, y = log_rna, color = identity)) + 
  geom_point(size=0.1) + 
  theme(
    panel.border = element_blank(),
    panel.background = element_rect("white"),
    panel.grid.major = element_blank(),
    panel.grid.minor = element_blank(),
    axis.line = element_line(colour = "black"),
    axis.text=element_text(size=10),
    legend.title = element_blank(),
    axis.title=element_text(size=10)
  ) + 
  scale_color_manual(values=c("red", "deepskyblue2") )+
  ggplot2::ggtitle(subtitle = 'EmptyDropsMultiome', sprintf("Clownfish Multiome: Pool_5 - Proportion of True Nuclei Detected", sum(eD.out$FDR_multi<0.001 & ! is.na(eD.out$FDR_multi))))+
  guides(colour = guide_legend(override.aes = list(size=5)))
emptyDrops_multi <- emptyDrops_multi + geom_abline(data = lines, aes(intercept = intercept, slope = slope, linetype = name))
emptyDrops_multi
ggsave("/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/QC/qc_plots/Pool_5_EmptyDropsMultiome_clownfish.pdf",
       height = 5, width = 6)

eD.out_multi_passed <- eD.out_multi$Row.names[eD.out_multi$identity == "pass"]
barcodes <- data.frame(Standard = eD.out_multi_passed)
write.table(barcodes, 
            file='/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/deconvolution/EmptyDropsMultiome/eDM_filtered_barcodes/Pool5_Clownfish_eDM.barcodes_passed.tsv', 
            quote=FALSE, sep='\t', col.names = FALSE, row.names = FALSE)
s5_eD.out_multi_passed <- as.data.frame(eD.out_multi)
colnames(s5_eD.out_multi_passed)[1] <- 'Barcode'
write.table(s5_eD.out_multi_passed, 
            file='/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/deconvolution/EmptyDropsMultiome/EmptyDropsMultiome_output/Pool5_Clownfish_EmptyDropsMultiome_output.tsv', 
            quote=FALSE, sep='\t', row.names = FALSE)

s5_emptyDrops_multi <- emptyDrops_multi

clown.s5_demulti <- read_csv('/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/deconvolution/souporcell_demuxlet_selected/s5_barcodes_sampleIDs.csv')

s5_good.cells <- as.character(barcodes$Standard)
s5 <- subset(s5, cells = s5_good.cells)
dim(s5)
s5_good.cells <- clown.s5_demulti$barcode
s5 <- subset(s5, cells = s5_good.cells)
dim(s5)

clown.s5_demulti$individual <- clown.s5_demulti$Sample
clown.s5_demulti$individual <- as.factor(clown.s5_demulti$individual)
s5$individual <- colnames(s5)
s5$individual <- clown.s5_demulti$individual[match(s5$individual, clown.s5_demulti$barcode)]
table(s5$individual)
dim(s5)

#################


s5_fragment_file = '/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/cellranger_outs/cellranger_seurat_files/s5/atac_fragments.tsv.gz'

# create a chromatin assay in the Seurat object
s5_atac <- CreateChromatinAssay(counts = s5.data$Peaks, 
                                fragments = s5_fragment_file, 
                                annotation = annotations, sep = c(":", "-"))

# only keep those barcodes passes QC stored in RNA assay
s5_barcodes <- Cells(s5_atac)[which(Cells(s5_atac) %in% Cells(s5))]
s5_atac <- subset(s5_atac, cells = s5_barcodes)

# create the multi-omics assay data containing both RNA and ATAC
s5[['ATAC']] <- s5_atac


################


mito <- rownames(s5)[grep('^KEG47-', rownames(s5))]
s5[['pct.mt']] <- PercentageFeatureSet(s5, pattern = '^KEG47-')

ribogenes <- c(rownames(s5)[grep('^rpl', rownames(s5))], rownames(s5)[grep('^rps', rownames(s5))])
ribogenes <- rownames(s5)[rownames(s5) %in% ribogenes]
s5[['pct.rb']] <- PercentageFeatureSet(s5, features = ribogenes)

ribosomal_mito_genes <- c(rownames(s5)[grep('^mrpl', rownames(s5))], rownames(s5)[grep('^mrps', rownames(s5))])
ribosomal_mito_genes <- rownames(s5)[rownames(s5) %in% ribosomal_mito_genes]
s5[['pct.mt.rb']] <- PercentageFeatureSet(s5, features = ribosomal_mito_genes)

coding <- unique(clown_gene.table$gene_id[clown_gene.table$gene_biotype == 'protein_coding'])
coding <- coding[which(! coding %in% c(mito, ribosomal_mito_genes, ribogenes))]
cgenes <- rownames(s5)[rownames(s5) %in% coding]
s5[['pct.cd']] <- PercentageFeatureSet(s5, features = cgenes)

lncRNA <- clown_gene.table$gene_id[clown_gene.table$gene_biotype == 'lncRNA']
snRNA <- clown_gene.table$gene_id[clown_gene.table$gene_biotype == 'snRNA']
snoRNA <- clown_gene.table$gene_id[clown_gene.table$gene_biotype == 'snoRNA']
nuclear <- unique(c(lncRNA, snRNA, snoRNA))
nuclear <- rownames(s5)[rownames(s5) %in% nuclear]
s5[['pct.nuclear']] <- PercentageFeatureSet(s5, features = nuclear)

ambient_markers$Gene <- tolower(ambient_markers$Gene)
ambient_markers$clown_homolog <- annotations$gene_id[match(ambient_markers$Gene, annotations$human_greatest_homolog, incomparables = T)]
ambient <- ambient_markers %>% dplyr::filter(PValue < 1e-3)
known_ambient <- rownames(s5)[which(ambient$clown_homolog %in% rownames(s5))]
ambient <- unique(c(known_ambient))
s5[['pct.ambient']] <- PercentageFeatureSet(s5, features = ambient)

s5 <- Add_Cell_Complexity(object = s5)
s5 <- Add_Top_Gene_Pct_Seurat(seurat_object = s5, num_top_genes = 50)
s5$genes_per_umi <- s5$nFeature_RNA/s5$nCount_RNA
dim(s5)


####################################


table(s5$individual)

s5_median_stats <- Median_Stats(seurat_object = s5, group_by_var = "individual", median_var = c('pct.mt', 'pct.cd', 'nCount_RNA', 'nFeature_RNA', 'nCount_ATAC', 'nFeature_ATAC'))
s5_median_stats

p1 <- QC_Plots_Genes(seurat_object = s5, low_cutoff = 250, high_cutoff = 4000, colors_use = brewer.pal(name = "Set2", n= 4), y_axis_log = TRUE, plot_median = TRUE, alpha = 0.1, group.by = 'individual')
p2 <- QC_Plots_UMIs(seurat_object = s5, low_cutoff = 250, high_cutoff = 10000, colors_use = brewer.pal(name = "Set2", n= 4), y_axis_log = TRUE, plot_median = TRUE, alpha = 0.1, group.by = 'individual')
p3 <- QC_Plots_Mito(seurat_object = s5, high_cutoff = 20, mito_name = 'pct.mt', colors_use = brewer.pal(name = "Set2", n= 4), group.by = 'individual')
p4 <- QC_Plots_Complexity(seurat_object = s5, high_cutoff = 0.88, colors_use = brewer.pal(name = "Set2", n= 4), plot_median = TRUE, alpha = 0.1, group.by = 'individual')
wrap_plots(p1, p2, p3, p4, ncol = 4)

qc.metrics <- as_tibble(
  s5[[]],
  rownames="Cell.Barcode"
)
qc.metrics %>%
  ggplot(aes(pct.mt)) + 
  geom_histogram(binwidth = 1.0, fill="#C93312", colour="red4") +
  ggtitle("Clownfish Pool_5 QC Metrics: Distribution of Percent Mitochondria \n \n") +
  geom_vline(xintercept = 20, color = 'black', linetype = 'longdash', linewidth = 0.75) + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.mt) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=pct.mt)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_5 QC Metrics: % MT genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.cd) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=pct.cd)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_5 QC Metrics: % coding genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.nuclear) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=pct.nuclear)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_5 QC Metrics: % nuclear genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.ambient) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=percent_top50)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_5 QC Metrics: % Top 50 Expressing genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.ambient) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=log10GenesPerUMI)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_5 QC Metrics: % Top Expressing genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))

VlnPlot(s5, 
        features = c('nCount_RNA', 'nFeature_RNA','nCount_ATAC','nFeature_ATAC'), 
        group.by = "individual", 
        ncol = 2,
        log = T, 
        pt.size = 0.1, 
        alpha = 0.1) + NoLegend()

VlnPlot(s5, features = c('pct.mt', 'pct.rb', 'pct.mt.rb', 'pct.cd','pct.ambient', 'pct.nuclear'), 
        group.by = "individual", 
        ncol = 3,
        log = F, 
        pt.size = 0.1, 
        alpha = 0.1) + NoLegend()

VlnPlot(s5, features = c('log10GenesPerUMI', 'percent_top50'), 
        group.by = "individual", 
        ncol = 2,
        log = F, 
        pt.size = 0.1, 
        alpha = 0.1) + NoLegend()

FeatureScatter(s5, 
               feature1 = 'nCount_RNA', 
               feature2 = 'nFeature_RNA', 
               split.by = 'individual', 
               group.by = 'individual',
               shuffle = T, 
               log = T)
FeatureScatter(s5, 
               feature1 = 'nCount_ATAC', 
               feature2 = 'nFeature_ATAC', 
               split.by = 'individual',
               group.by = 'individual',
               shuffle = T, 
               log = T)

saveRDS(s5, '/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/QC/qc_gex.atac_outs/s5_clownfish_gex.atac_raw.rds')

```



```{r echo=TRUE, message=FALSE, warning=FALSE, fig.height = 6, fig.width = 10}

s6.data <- Read10X_h5('/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/cellranger_outs/cellranger_seurat_files/s6/raw_feature_bc_matrix.h5')
s6 <- CreateSeuratObject(s6.data$`Gene Expression`)
dim(s6)

s6$orig.ident <- 'Pool_6'

rna <- s6.data$`Gene Expression`
atac <- s6.data$Peaks
eD.out <- emptydrops_multiome(count_matrix_rna=rna, count_matrix_atac=atac, verbose = T)
print("the number of cells detected is: ")
print(sum(eD.out$FDR_multi<0.001 & ! is.na(eD.out$FDR_multi)))

eD.out_multi <- eD.out
eD.out_multi$identity <- "fail"
eD.out_multi$identity[eD.out_multi$FDR_multi <= 0.001 & !is.na(eD.out_multi$FDR_multi) ] <- "pass"
observations6c <- data.frame("log_atac" = log10(eD.out_multi$Total_chromatin+0.1),
                             "log_rna" = log10(eD.out_multi$Total_RNA+0.1),
                             "identity" = eD.out_multi$identity)
lines <- data.frame(name=c("higher", "k-means", "lower"),
                    slope=c(eD.out_multi@metadata$k_means_slope, eD.out_multi@metadata$k_means_slope, eD.out_multi@metadata$k_means_slope),
                    intercept = c(eD.out_multi@metadata$higher_intercept, eD.out_multi@metadata$k_means_intercept, eD.out_multi@metadata$lower_intercept),
                    type=c("dashed", "solid", "dotted"))
emptyDrops_multi <- ggplot(observations6c, aes(x = log_atac, y = log_rna, color = identity)) + 
  geom_point(size=0.1) + 
  theme(
    panel.border = element_blank(),
    panel.background = element_rect("white"),
    panel.grid.major = element_blank(),
    panel.grid.minor = element_blank(),
    axis.line = element_line(colour = "black"),
    axis.text=element_text(size=10),
    legend.title = element_blank(),
    axis.title=element_text(size=10)
  ) + 
  scale_color_manual(values=c("red", "deepskyblue2") )+
  ggplot2::ggtitle(subtitle = 'EmptyDropsMultiome', sprintf("Clownfish Multiome: Pool_6 - Proportion of True Nuclei Detected", sum(eD.out$FDR_multi<0.001 & ! is.na(eD.out$FDR_multi))))+
  guides(colour = guide_legend(override.aes = list(size=5)))
emptyDrops_multi <- emptyDrops_multi + geom_abline(data = lines, aes(intercept = intercept, slope = slope, linetype = name))
emptyDrops_multi
ggsave("/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/QC/qc_plots/Pool_6_EmptyDropsMultiome_clownfish.pdf",
       height = 5, width = 6)

eD.out_multi_passed <- eD.out_multi$Row.names[eD.out_multi$identity == "pass"]
barcodes <- data.frame(Standard = eD.out_multi_passed)
write.table(barcodes, 
            file='/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/deconvolution/EmptyDropsMultiome/eDM_filtered_barcodes/Pool6_Clownfish_eDM.barcodes_passed.tsv', 
            quote=FALSE, sep='\t', col.names = FALSE, row.names = FALSE)
s6_eD.out_multi_passed <- as.data.frame(eD.out_multi)
colnames(s6_eD.out_multi_passed)[1] <- 'Barcode'
write.table(s6_eD.out_multi_passed, 
            file='/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/deconvolution/EmptyDropsMultiome/EmptyDropsMultiome_output/Pool6_Clownfish_EmptyDropsMultiome_output.tsv', 
            quote=FALSE, sep='\t', row.names = FALSE)

s6_emptyDrops_multi <- emptyDrops_multi

clown.s6_demulti <- read_csv('/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/deconvolution/souporcell_demuxlet_selected/s6_barcodes_sampleIDs.csv')

s6_good.cells <- as.character(barcodes$Standard)
s6 <- subset(s6, cells = s6_good.cells)
dim(s6)
s6_good.cells <- clown.s6_demulti$barcode
s6 <- subset(s6, cells = s6_good.cells)
dim(s6)

clown.s6_demulti$individual <- clown.s6_demulti$Sample
clown.s6_demulti$individual <- as.factor(clown.s6_demulti$individual)
s6$individual <- colnames(s6)
s6$individual <- clown.s6_demulti$individual[match(s6$individual, clown.s6_demulti$barcode)]
table(s6$individual)
dim(s6)

#################


s6_fragment_file = '/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/cellranger_outs/cellranger_seurat_files/s6/atac_fragments.tsv.gz'

# create a chromatin assay in the Seurat object
s6_atac <- CreateChromatinAssay(counts = s6.data$Peaks, 
                                fragments = s6_fragment_file, 
                                annotation = annotations, sep = c(":", "-"))

# only keep those barcodes passes QC stored in RNA assay
s6_barcodes <- Cells(s6_atac)[which(Cells(s6_atac) %in% Cells(s6))]
s6_atac <- subset(s6_atac, cells = s6_barcodes)

# create the multi-omics assay data containing both RNA and ATAC
s6[['ATAC']] <- s6_atac


################


mito <- rownames(s6)[grep('^KEG47-', rownames(s6))]
s6[['pct.mt']] <- PercentageFeatureSet(s6, pattern = '^KEG47-')

ribogenes <- c(rownames(s6)[grep('^rpl', rownames(s6))], rownames(s6)[grep('^rps', rownames(s6))])
ribogenes <- rownames(s6)[rownames(s6) %in% ribogenes]
s6[['pct.rb']] <- PercentageFeatureSet(s6, features = ribogenes)

ribosomal_mito_genes <- c(rownames(s6)[grep('^mrpl', rownames(s6))], rownames(s6)[grep('^mrps', rownames(s6))])
ribosomal_mito_genes <- rownames(s6)[rownames(s6) %in% ribosomal_mito_genes]
s6[['pct.mt.rb']] <- PercentageFeatureSet(s6, features = ribosomal_mito_genes)

coding <- unique(clown_gene.table$gene_id[clown_gene.table$gene_biotype == 'protein_coding'])
coding <- coding[which(! coding %in% c(mito, ribosomal_mito_genes, ribogenes))]
cgenes <- rownames(s6)[rownames(s6) %in% coding]
s6[['pct.cd']] <- PercentageFeatureSet(s6, features = cgenes)

lncRNA <- clown_gene.table$gene_id[clown_gene.table$gene_biotype == 'lncRNA']
snRNA <- clown_gene.table$gene_id[clown_gene.table$gene_biotype == 'snRNA']
snoRNA <- clown_gene.table$gene_id[clown_gene.table$gene_biotype == 'snoRNA']
nuclear <- unique(c(lncRNA, snRNA, snoRNA))
nuclear <- rownames(s6)[rownames(s6) %in% nuclear]
s6[['pct.nuclear']] <- PercentageFeatureSet(s6, features = nuclear)

ambient_markers$Gene <- tolower(ambient_markers$Gene)
ambient_markers$clown_homolog <- annotations$gene_id[match(ambient_markers$Gene, annotations$human_greatest_homolog, incomparables = T)]
ambient <- ambient_markers %>% dplyr::filter(PValue < 1e-3)
known_ambient <- rownames(s6)[which(ambient$clown_homolog %in% rownames(s6))]
ambient <- unique(c(known_ambient))
s6[['pct.ambient']] <- PercentageFeatureSet(s6, features = ambient)

s6 <- Add_Cell_Complexity(object = s6)
s6 <- Add_Top_Gene_Pct_Seurat(seurat_object = s6, num_top_genes = 50)
s6$genes_per_umi <- s6$nFeature_RNA/s6$nCount_RNA
dim(s6)


####################################


table(s6$individual)

s6_median_stats <- Median_Stats(seurat_object = s6, group_by_var = "individual", median_var = c('pct.mt', 'pct.cd', 'nCount_RNA', 'nFeature_RNA', 'nCount_ATAC', 'nFeature_ATAC'))
s6_median_stats

p1 <- QC_Plots_Genes(seurat_object = s6, low_cutoff = 250, high_cutoff = 4000, colors_use = brewer.pal(name = "Set2", n= 4), y_axis_log = TRUE, plot_median = TRUE, alpha = 0.1, group.by = 'individual')
p2 <- QC_Plots_UMIs(seurat_object = s6, low_cutoff = 250, high_cutoff = 10000, colors_use = brewer.pal(name = "Set2", n= 4), y_axis_log = TRUE, plot_median = TRUE, alpha = 0.1, group.by = 'individual')
p3 <- QC_Plots_Mito(seurat_object = s6, high_cutoff = 20, mito_name = 'pct.mt', colors_use = brewer.pal(name = "Set2", n= 4), group.by = 'individual')
p4 <- QC_Plots_Complexity(seurat_object = s6, high_cutoff = 0.88, colors_use = brewer.pal(name = "Set2", n= 4), plot_median = TRUE, alpha = 0.1, group.by = 'individual')
wrap_plots(p1, p2, p3, p4, ncol = 4)

qc.metrics <- as_tibble(
  s6[[]],
  rownames="Cell.Barcode"
)
qc.metrics %>%
  ggplot(aes(pct.mt)) + 
  geom_histogram(binwidth = 1.0, fill="#C93312", colour="red4") +
  ggtitle("Clownfish Pool_6 QC Metrics: Distribution of Percent Mitochondria \n \n") +
  geom_vline(xintercept = 20, color = 'black', linetype = 'longdash', linewidth = 0.75) + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.mt) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=pct.mt)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_6 QC Metrics: % MT genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.cd) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=pct.cd)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_6 QC Metrics: % coding genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.nuclear) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=pct.nuclear)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_6 QC Metrics: % nuclear genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.ambient) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=percent_top50)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_6 QC Metrics: % Top 50 Expressing genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))
qc.metrics %>%
  arrange(pct.ambient) %>%
  ggplot(aes(nCount_RNA,nFeature_RNA,colour=log10GenesPerUMI)) + 
  geom_point(size=0.7) + 
  scale_color_gradientn(colors=wes_palette("Zissou1", 100, type = "continuous")) +
  ggtitle("Clownfish Pool_6 QC Metrics: % Top Expressing genes highlighted \n \n") +
  geom_hline(yintercept = 200, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_hline(yintercept = 20000, color = 'red', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 200, color = 'blue', linewidth = .5, linetype = 'longdash') +
  geom_vline(xintercept = 20000, color = 'blue', linewidth = .5, linetype = 'longdash') +
  stat_smooth(method="lm", color = 'black') +
  scale_x_log10() + scale_y_log10() + theme_classic() + theme(plot.title = element_text(hjust=0.5, face="bold", size = 15, vjust = -2))

VlnPlot(s6, 
        features = c('nCount_RNA', 'nFeature_RNA','nCount_ATAC','nFeature_ATAC'), 
        group.by = "individual", 
        ncol = 2,
        log = T, 
        pt.size = 0.1, 
        alpha = 0.1) + NoLegend()

VlnPlot(s6, features = c('pct.mt', 'pct.rb', 'pct.mt.rb', 'pct.cd','pct.ambient', 'pct.nuclear'), 
        group.by = "individual", 
        ncol = 3,
        log = F, 
        pt.size = 0.1, 
        alpha = 0.1) + NoLegend()

VlnPlot(s6, features = c('log10GenesPerUMI', 'percent_top50'), 
        group.by = "individual", 
        ncol = 2,
        log = F, 
        pt.size = 0.1, 
        alpha = 0.1) + NoLegend()

FeatureScatter(s6, 
               feature1 = 'nCount_RNA', 
               feature2 = 'nFeature_RNA', 
               split.by = 'individual', 
               group.by = 'individual',
               shuffle = T, 
               log = T)
FeatureScatter(s6, 
               feature1 = 'nCount_ATAC', 
               feature2 = 'nFeature_ATAC', 
               split.by = 'individual',
               group.by = 'individual',
               shuffle = T, 
               log = T)

saveRDS(s6, '/Users/kathrynleatherbury/GaTech Dropbox/CoS/BioSci/BioSci-Streelman/MultiomeProjects/clownfish/QC/qc_gex.atac_outs/s6_clownfish_gex.atac_raw.rds')

```



