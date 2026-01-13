# 01 – Quality control and read filtering

## Computing environment
Most analyses were performed using the high-performance computing cluster of the
Departamento de Química Biológica, Facultad de Ciencias Exactas y Naturales,
Universidad de Buenos Aires (UBA).

## ONT data
Raw reads from whole-transcriptome and amplicon ONT sequencing were stored in POD5
format. Basecalled reads were generated as compressed FASTQ files.

FASTQ files corresponding to each sample were processed within the directory
containing all compressed FASTQ files generated after basecalling and demultiplexing.

Example commands used:
```bash
gunzip *.fastq.gz
cat *.fastq > merged.fastq
```
Read quality was assessed using **NanoPlot**
(https://github.com/wdecoster/NanoPlot), a visualization tool for long-read
sequencing data.

Example command used:
```bash
NanoPlot --fastq merged.fastq --raw -o nanoplot_out
```
Read filtering was performed using **SeqKit**
(https://github.com/shenwei356/seqkit), a toolkit for FASTA/FASTQ file manipulation.

Reads were filtered by minimum length to remove short and low-information
sequences prior to downstream analyses.

Example command used:
```bash
seqkit seq merged.fastq --min-len <MIN_READ_LENGTH> > merged_filtered.fastq
```
The value of <MIN_READ_LENGTH> was selected based on the experimental design
and sequencing strategy.
