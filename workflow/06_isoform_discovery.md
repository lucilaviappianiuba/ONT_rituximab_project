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
```

### Isoform correction

The FLAIR correct module was applied to refine splice junctions using the
reference annotation and genome sequence.

Example command used:
```bash
flair correct -q genome_alignment.bed \
  --gtf Homo_sapiens.GRCh38.113.gtf \
  -g Homo_sapiens.GRCh38.dna_sm.primary_assembly.fa \
  --ss_window 30
```
### Isoform collapsing

Corrected reads were collapsed into isoform models using the collapse module.

Example command used:
```bash
flair collapse -g Homo_sapiens.GRCh38.dna_sm.primary_assembly.fa \
  -q flair_all_corrected.bed \
  -r reads.fastq \
  --gtf Homo_sapiens.GRCh38.113.gtf
```
### Isoform quantification

Isoform abundance was estimated using the quantify module.

Example command used:
```bash
flair quantify --isoforms flair.collapse.isoforms.fa \
  --reads_manifest reads_manifest.tsv \
  --isoform_bed flair.collapse.isoforms.bed
```
A more stringent configuration was also applied to restrict isoform detection to
high-confidence splice events:

```bash
flair quantify --isoforms flair.collapse.isoforms.fa \
  --reads_manifest reads_manifest.tsv \
  --isoform_bed flair.collapse.isoforms.bed \
  --stringent --check_splice
```

## Isoform discovery using IsoQuant

Isoform discovery was additionally performed using IsoQuant
(https://github.com/ablab/IsoQuant
), which reconstructs transcript isoforms from
long-read RNA sequencing data.

Two strategies were applied: a permissive configuration to maximize sensitivity
and a more conservative configuration to prioritize high-confidence isoforms.

Example command used (permissive mode):
```bash
isoquant.py \
  --reference <GENOME_FASTA> \
  --genedb <GTF_FILE> \
  --complete_genedb \
  --bam <GENOME_ALIGNED_BAM> \
  --data_type nanopore \
  --report_novel_unspliced true \
  --stranded none \
  --splice_correction_strategy all \
  --matching_strategy loose \
  --model_construction_strategy sensitive_ont \
  --output isoquant_output
```

Example command used (conservative mode):
```bash
isoquant.py \
  --reference <GENOME_FASTA> \
  --genedb <GTF_FILE> \
  --complete_genedb \
  --bam <GENOME_ALIGNED_BAM> \
  --data_type nanopore \
  --report_novel_unspliced true \
  --stranded none \
  --splice_correction_strategy default_ont \
  --matching_strategy default \
  --model_construction_strategy default_ont \
  --output isoquant_output
```

