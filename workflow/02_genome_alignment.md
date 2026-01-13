# 02 – Alignment to the reference genome

ONT reads (whole-transcriptome and amplicon sequencing) were aligned to the human
reference genome (Homo sapiens, GRCh38.dna_sm.primary_assembly.fa https://www.ensembl.org/Homo_sapiens/Info/Index).

Genome alignment was performed using **minimap2**
(https://github.com/lh3/minimap2), a versatile aligner for long-read and spliced
nucleotide sequences.

Spliced alignment parameters were used to account for exon–exon junctions in
cDNA-derived reads.

Example command used:
```bash
minimap2 -ax splice GRCh38.dna_sm.primary_assembly.fa merged_filtered.fastq > alignment.sam
```

SAM files were converted to BAM format, sorted and indexed using samtools
(https://github.com/samtools/samtools
).

Example commands used:
```bash
samtools view -Sb alignment.sam > alignment.bam
samtools sort alignment.bam -o alignment.sorted.bam
samtools index alignment.sorted.bam
```
Basic alignment statistics were obtained using samtools:
```bash
samtools flagstat alignment.sam
```
