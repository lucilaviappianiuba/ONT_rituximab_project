# 04 – Transcript-level quantification

Transcript-level quantification of ONT long-read RNA-seq data was performed using
multiple tools in order to compare abundance estimates obtained with different
quantification strategies.

The following tools were used: **Salmon**, **Oarfish** and **Minnow**.

---

## Quantification of ONT data using Salmon

**Salmon** (https://github.com/COMBINE-lab/salmon) was applied in alignment-based
mode, using transcriptome alignments in BAM format as input.

For this step, the BAM file used as input corresponds to the **unsorted BAM**
generated directly after SAM-to-BAM conversion and prior to any sorting step.

Example command used:
```bash
salmon quant -t Homo_sapiens.GRCh38.cdna.all.fa -l U \
  -a alignment.bam \
  --noErrorModel --noLengthCorrection \
  -o salmon_output
```

Quantification results were stored in quant.sf files, reporting transcript-level
abundances in TPM and estimated counts.

## Quantification of ONT data using Oarfish

Transcript quantification from ONT reads was also performed using Oarfish
(https://github.com/COMBINE-lab/oarfish
), a long-read RNA-seq quantification tool.

Example command used:
```bash
oarfish --seq-tech ont-cdna \
  --alignments alignment.bam \
  --output oarfish_output \
  --model-coverage \
  --filter-group no-filters
```
