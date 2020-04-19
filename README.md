# ViralMSA
ViralMSA is a tool to perform reference-guided multiple sequence alignment of viral genomes. ViralMSA wraps around existing read mapping tools such as [Minimap2](https://doi.org/10.1093/bioinformatics/bty191) and [HISAT2](https://doi.org/10.1038/s41587-019-0201-4), and as such, it can natively improve as methods of read mapping evolve. Importantly, this approach scales linearly with the number of sequences and can be massively parallelized. However, insertions with respect to the reference genome will be thrown away. This is fair for many viral analyses (e.g. phylogenetic inference, as insertions with respect to the reference likely lack phylogenetic information), but it may not be appropriate for all contexts.

## Installation
ViralMSA is written in Python 3 and depends on [BioPython](https://biopython.org/). You can simply download [ViralMSA.py](ViralMSA.py) to your machine and make it executable.

ViralMSA also requires at least one of the following tools to perform the alignment:

* [Minimap2](https://github.com/lh3/minimap2) (used by default)
* [HISAT2](http://daehwankimlab.github.io/hisat2/)
* [bowtie2](http://bowtie-bio.sourceforge.net/bowtie2/index.shtml)

## Usage
ViralMSA can be used as follows:

```
usage: ViralMSA.py [-h] -s SEQUENCES -r REFERENCE -e EMAIL -o OUTPUT [-a ALIGNER] [-t THREADS] [--include_ref] [--viralmsa_dir VIRALMSA_DIR]

optional arguments:
  -h, --help                            show this help message and exit
  -s SEQUENCES, --sequences SEQUENCES   Input Sequences (FASTA format) (default: None)
  -r REFERENCE, --reference REFERENCE   Reference (default: None)
  -e EMAIL, --email EMAIL               Email Address (for Entrez) (default: None)
  -o OUTPUT, --output OUTPUT            Output Directory (default: None)
  -a ALIGNER, --aligner ALIGNER         Aligner (default: Minimap2)
  -t THREADS, --threads THREADS         Number of Threads (default: max)
  --include_ref                         Include reference sequence in output alignment (default: False)
  --viralmsa_dir VIRALMSA_DIR           ViralMSA Cache Directory (default: ~/.viralmsa)
```

For the reference, you can provide a GenBank accession number, such as the following:

```
ViralMSA.py -e email@address.com -s sequences.fas -o output -r MT072688
```

For specific viruses of interest, you can simply use their name, and we have provided what we believe would be a good choice of reference genome, such as the following:

```
ViralMSA.py -e email@address.com -s sequences.fas -o output -r SARS-CoV-2
```
