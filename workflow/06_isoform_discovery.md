# 06 – Isoform discovery

Isoform discovery and characterization were performed using long-read ONT
transcriptome data in order to identify known and novel transcript isoforms of
therapeutic target genes.

Two complementary tools were used: **FLAIR** and **IsoQuant**.

---

## Isoform discovery using FLAIR

Isoform analysis was performed using **FLAIR**
(https://github.com/BrooksLabUCSC/flair), a tool designed for full-length
alternative isoform analysis of long-read RNA sequencing data.

Genome-aligned ONT reads in BAM format were converted to BED12 format prior to
isoform correction and collapsing.

Example command used for BAM to BED12 conversion:
```bash
bam2Bed12 genome_alignment.sorted.bam > genome_alignment.bed
