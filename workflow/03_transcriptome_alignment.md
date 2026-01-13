# 03 – Alignment to the reference transcriptome

Filtered ONT reads were aligned to the human reference transcriptome
(Homo sapiens, GRCh38), using the Ensembl cDNA reference file
(Homo_sapiens.GRCh38.cdna.all.fa) and its corresponding annotation.

Transcriptome alignment was performed using **minimap2**
(https://github.com/lh3/minimap2) with parameters optimized for Oxford Nanopore
cDNA reads.

Example command used:
```bash
minimap2 -ax map-ont Homo_sapiens.GRCh38.cdna.all.fa merged_filtered.fastq > alignment.sam
```
SAM files were converted to BAM format using samtools for downstream analyses:
```bash
samtools view -Sb alignment.sam > alignment.bam
```
Basic alignment statistics were obtained using samtools:
```bash
samtools flagstat alignment.bam
```
### Generation of PAF files

In addition to BAM files, alignments in PAF (Pairwise Alignment Format) were
generated for tools requiring this format in subsequent quantification steps.
