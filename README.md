# About scPagwas

**scPagwas** employs a polygenic regression model to prioritize a set of
trait-relevant genes and uncover trait-relevant cell subpopulations by
incorporating pathway activity transformed single-cell RNA sequencing
(scRNA-seq) data with genome-wide association studies (GWAS) summary
data.

<img src="./man/figures/Figure1.png" width="100%" style="display: block; margin: auto;" />

We are preparing to release an upgraded version of scPagwas, named scPagwas2, which introduces enhanced methods for calculating genetically associated genes. By incorporating extensive random calculations, this version offers improved result stability. Additionally, we have addressed issues with synchronizing results across single-cell data and cell-type data. Please note that scPagwas2 requires the use of the scPagwas_main2 function to replace the original scPagwas_main.

To accommodate the substantial memory demands of single-cell data calculations in R, we have developed a Python version, scPagwas_py (https://github.com/dengchunyu/scPagwas_py)[https://github.com/mayunlong89/scPagwas_py], fully synchronized with scPagwas2.0. We will continue to provide updates to further enhance computational efficiency.

Please cite this article in press as: Ma et al.,Polygenic regression
uncovers trait-relevant cellular contexts through pathway activation
transformation of single-cell RNA sequencing data,Cell Genomics
(2023),<https://doi.org/10.1016/j.xgen.2023.100383>

Code for reproducing the analysis from the paper is available
[here](https://github.com/dengchunyu/scPagwas_reproduce), or
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.8137370.svg)](https://doi.org/10.5281/zenodo.8137370)

For further usage on the scPagwas package, you can visit the
[website](https://dengchunyu.github.io/about/). A vignette for using
also can be accessed using browseVignettes(“scPagwas”)

Some important data can be download from
[here](https://drive.google.com/drive/folders/1z7uQtzjnieJhYLhLmgmIz2jk6a6hes4l?usp=drive_link)

## Installation

You can install the released version of scPagwas from
[github](https://github.com/sulab-wmu/scPagwas) with:

``` r
#install some dependence packages
install.packages("Seurat")
install.packages("ggpubr")
if (!require("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
BiocManager::install("GenomicRanges")
BiocManager::install("IRanges")

devtools::install_github("sulab-wmu/scPagwas")
```

In many cases, installing packages using `devtools::install_github` may
fail.

``` r
library(devtools)
install_git("https://github.com/sulab-wmu/scPagwas.git", ref = "main")
```

Or, download the package file from
[here](https://api.github.com/repos/sulab-wmu/scPagwas/tarball/HEAD)
Then install it locally.

``` r
devtools::install_local("sulab-wmu-scPagwas-****.tar.gz")
```

## Usage

quick-start example:

``` r
library(scPagwas)
system.time(
 #1.start to run the wrapper functions for example.
 Pagwas_data<-scPagwas_main(Pagwas = NULL,
                     gwas_data =system.file("extdata", "GWAS_summ_example.txt", package = "scPagwas"), # The GWAS Summary statistics files 
                     Single_data =system.file("extdata", "scRNAexample.rds", package = "scPagwas"),# scRNA-seq data in seruat format with "RNA" assays and normalized.
                     output.prefix="test", # the prefix name for output files
                     output.dirs="scPagwastest_output",# the directory file's name for output
                     block_annotation = block_annotation_hg37,# gene position in chromosome is provided by package. default is hg38, block_annotation_hg37 is hg37.
                     assay="RNA", # the assays for scRNA-seq data to use.
                     Pathway_list=Genes_by_pathway_kegg,# pathway list is provided by package, including gene symbols.
                     n.cores=1,
                     iters_singlecell = 10,
                     chrom_ld = chrom_ld,# The LD data is provided by package.
                     singlecell=T, # Whether to run the singlecell process.
                     celltype=T# Whether to run the celltype process.
)
)
```

# All COVID-19-related projects in our group:
1) Meta-analysis of large-scale GWAS data to uncover novel loci for COVID-19. see [Ma et al. Human Molecular Genetics, 2021](https://academic.oup.com/hmg/article/30/13/1247/6265026), and see related [Github codes](https://github.com/mayunlong89/Host_genetics_for_COVID-19).
2) COVID-19 Quarantine Reveals That Behavioral Changes Have an Effect on Myopia Progression. see [Xu, Ma et al. Ophthalmology, 2021](https://www.sciencedirect.com/science/article/pii/S0161642021002578), see related [Github codes](https://github.com/mayunlong89/MIES).
3) Identification of genetics-influenced immune cell sub-populations relevant to severe COVID-19. see [Ma et al. Genome Medicine, 2022](https://link.springer.com/article/10.1186/s13073-022-01021-1), and see related [Github codes](https://github.com/mayunlong89/COVID19_scRNA).
4) Development of novel polygenic regression method scPagwas for integrating scRNA-seq data with GWAS on complex diseases. see [Ma et al. Cell Genomics, 2023](https://www.cell.com/cell-genomics/fulltext/S2666-979X(23)00180-5), and see related [Github codes](https://github.com/mayunlong89/scPagwas_main).
5) Repurposing cell type-specific durg targets for severe COVID-19 based on human organoids scRNA-seq atlas. see [Ma et al. Cell Proliferation, 2024](https://onlinelibrary.wiley.com/doi/full/10.1111/cpr.13558), and see related [Github codes](https://github.com/mayunlong89/scHuman_organoids_COVID19).
