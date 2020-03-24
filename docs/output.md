
# nf-core/kmermaid: Output

This document describes the output produced by the pipeline.


## Pipeline overview
The pipeline is built using [Nextflow](https://www.nextflow.io/)
and processes data using the following steps:

* [FastQC](#fastqc) - read quality control
* [Sourmash sketch](#sourmash-sketch) - Compute a k-mer sketch of each sample
* [Sourmash compare](#sourmash-compare) - Compare all samples on k-mer sketches

## FastQC
[FastQC](http://www.bioinformatics.babraham.ac.uk/projects/fastqc/) gives general quality metrics about your reads. It provides information about the quality score distribution across your reads, the per base sequence content (%T/A/G/C). You get information about adapter contamination and other overrepresented sequences.

For further reading and documentation see the [FastQC help](http://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/).


**Output directory: `results/fastqc`**

* `sample_fastqc.html`
  * FastQC report, containing quality metrics for your untrimmed raw fastq files
* `zips/sample_fastqc.zip`
  * zip file containing the FastQC report, tab-delimited data file and plot images

## Sourmash Sketch

[Sourmash](https://sourmash.readthedocs.io/en/latest/) is a tool to compute MinHash sketches on nucleotide (DNA/RNA) and protein sequences. It allows for fast comparisons of sequences based on their nucleotide content.

**Output directory: `results/sourmash/sketches`**

For each sample and provided `molecule`, `ksize` and `log2_sketch_size`, a file is created:

* `sample_molecule-$molecule_ksize-$ksize_log2sketchsize-$log2_sketch_size.sig`

For example:

```
SRR4050379_molecule-dayhoff_ksize-3_log2sketchsize-2.sig
SRR4050379_molecule-dayhoff_ksize-3_log2sketchsize-4.sig
SRR4050379_molecule-dayhoff_ksize-9_log2sketchsize-2.sig
SRR4050379_molecule-dayhoff_ksize-9_log2sketchsize-4.sig
SRR4050379_molecule-dna_ksize-3_log2sketchsize-2.sig
SRR4050379_molecule-dna_ksize-3_log2sketchsize-4.sig
SRR4050379_molecule-dna_ksize-9_log2sketchsize-2.sig
SRR4050379_molecule-dna_ksize-9_log2sketchsize-4.sig
SRR4050379_molecule-protein_ksize-3_log2sketchsize-2.sig
SRR4050379_molecule-protein_ksize-3_log2sketchsize-4.sig
SRR4050379_molecule-protein_ksize-9_log2sketchsize-2.sig
SRR4050379_molecule-protein_ksize-9_log2sketchsize-4.sig
```

## Sourmash Compare

**Output directory: `results/sourmash`**

For each provided `molecule`, `ksize` and `log2_sketch_size`, a file is created containing a symmetric matrix of the similarity between all samples, written as a comma-separated variable file:

* `molecule-$molecule_ksize-$ksize_log2sketchsize-$log2_sketch_size.csv`

For example,

```
similarities_molecule-dna_ksize-3_log2sketchsize-2.csv
similarities_molecule-dna_ksize-3_log2sketchsize-4.csv
similarities_molecule-dna_ksize-9_log2sketchsize-2.csv
similarities_molecule-dna_ksize-9_log2sketchsize-4.csv
similarities_molecule-protein_ksize-3_log2sketchsize-2.csv
similarities_molecule-protein_ksize-3_log2sketchsize-4.csv
similarities_molecule-protein_ksize-9_log2sketchsize-2.csv
similarities_molecule-protein_ksize-9_log2sketchsize-4.csv
```

