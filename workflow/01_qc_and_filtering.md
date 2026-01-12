# 01 – Quality control and read filtering

## Computing environment
Most analyses were performed using the high-performance computing cluster of the
Departamento de Química Biológica, Facultad de Ciencias Exactas y Naturales,
Universidad de Buenos Aires (UBA).

## ONT data
Raw reads from whole-transcriptome and amplicon ONT sequencing were stored in POD5
format. Basecalled reads were generated as compressed FASTQ files.

FASTQ files were decompressed and merged per sample.

Example commands used:
```bash
gunzip *.fastq.gz
cat *.fastq > merged.fastq

