# 05 – Molecular subtype classification

Molecular subtype classification of pediatric B-cell acute lymphoblastic leukemia
(B-ALL) samples was performed using transcriptome-wide expression profiles.

Two complementary approaches were applied:
- **ALLCatchR**, a gene-expression–based classifier.
- **nanopore-wts-classification**, a long-read–specific whole-transcriptome
  classification pipeline.

---

## Classification using ALLCatchR

Subtype classification was performed using **ALLCatchR**
(https://github.com/ThomasBeder/ALLCatchR).

Transcript-level quantifications obtained with Salmon were collapsed to gene-level
counts prior to classification. This step was performed in R using the
**tximport** package (https://github.com/thelovelab/tximport).

Example R workflow:
```r
library(tximport)
library(ALLCatchR)

txi <- tximport(files, type = "salmon", txOut = FALSE)

allcatch(
  Counts.file = "gene_counts.csv",
  ID_class = "ensembl_ID",
  sep = ","
)
