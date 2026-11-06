# Genomic Data Science Specialization — Johns Hopkins University

![Institution](https://img.shields.io/badge/Institution-Johns%20Hopkins%20University-blue)
![Platform](https://img.shields.io/badge/Platform-Coursera-0056D2)
![Language](https://img.shields.io/badge/Language-Python%20%7C%20R%20%7C%20Bash-green)
![Tools](https://img.shields.io/badge/Tools-samtools%20%7C%20bowtie2%20%7C%20cufflinks%20%7C%20Bioconductor-orange)

Coursework from the Johns Hopkins Genomic Data Science Specialization (Coursera),
kept as code. Five courses, one folder each, with the data files the exercises were
run against so the notebooks can be re-executed.

This is coursework: the exercises follow the instructors' protocols. What the
repository shows is sequence-side data handling end to end — FASTA and FASTQ
parsing, read alignment, variant calling, transcript assembly and differential
expression — run on real files rather than described.

Work in this repository was done in June–July 2022.

---

## What is here

| Folder | Course | Contents |
|---|---|---|
| [`1_Python/`](1_Python) | Python for Genomic Data Science | 3 notebooks, 2 FASTA files |
| [`2_Algorithms/`](2_Algorithms) | Algorithms for DNA Sequencing | 4 projects, 10 notebooks, 2 Python modules |
| [`3_Command_Line_Tools/`](3_Command_Line_Tools) | Command Line Tools for Genomic Data Science | 4 module projects with their full working data |
| [`4_Bioconductor/`](4_Bioconductor) | Bioconductor for Genomic Data Science | 4 module quizzes (R Markdown) |
| [`5_Statistics/`](5_Statistics) | Statistics for Genomic Data Science | 4 module quizzes (R Markdown), 2 figures |

---

## 1. Python for Genomic Data Science

FASTA parsing written from scratch, without Biopython.

- `1_FASTA_records_length.ipynb` — read a multi-record FASTA, count records, report sequence lengths
- `2_FASTA_ORF_analysis.ipynb` — find open reading frames across forward frames, by record
- `3_FASTA_repeat_counter.ipynb` — count repeated substrings of a given length across records

Data: `dna.example.fasta`, `dna2.fasta`

## 2. Algorithms for DNA Sequencing

Read alignment and assembly algorithms, implemented rather than called.

**Project 1 — exact matching**
- naive exact matching, and a variant tolerating up to 2 mismatches
- FASTQ quality analysis: per-cycle quality read from `ERR037900_1.first1000.fastq`
- Data: `lambda_virus.fa`

**Project 2 — approximate matching**
- Boyer-Moore with character-comparison and alignment counts, against the naive baseline
- index-assisted approximate matching with a k-mer index, plus a subsequence-index variant
- Helper modules: `bm_preproc.py` (bad character and good suffix tables), `kmer_index.py`
- Data: `chr1.GRCh38.excerpt.fasta` (human chromosome 1 excerpt)

**Project 3 — dynamic programming**
- edit distance for approximate best match
- all-pairs suffix/prefix overlap detection
- Data: `ERR266411_1.for_asm.fastq`

**Project 4 — assembly**
- shortest common superstring, then a greedy SCS implementation for a larger read set
- Data: `ads1_week4_reads.fq`

## 3. Command Line Tools for Genomic Data Science

The four module projects, each kept with the intermediate and output files the
pipeline produced. These are the folders to open to see the actual artefacts of a
sequencing workflow rather than a description of one.

**Module 1 — genome arithmetic.** BED and annotation operations over an apple
genome and three conditions (`apple.genome`, `apple.genes`, `apple.conditionA/B/C`),
with sorted outputs and an intersection.

**Module 2 — alignment inspection.** *Arabidopsis thaliana* strain wu_0:
`athal_wu_0_A.bam` sorted and indexed with samtools, a region extracted, overlaps
against `athal_wu_0_A_annot.gtf` written to `overlaps.bed`.

**Module 3 — variant calling.** `wu_0_A_wgs.fastq` aligned to `wu_0.v7.fas` with
bowtie2 (end-to-end and local), converted and sorted with samtools, piled up to
`wu_0.mpileup.bcf`, and called to `wu_0.vcf` / `wu_0.final.vcf`.

**Module 4 — RNA-seq differential expression.** *A. thaliana* shoot apical meristem
at day 8 against day 16. bowtie2 index build, tophat alignment (`Tophat/Day8`,
`Tophat/Day16`, with run logs), cufflinks assembly per sample, cuffmerge into
`merged_asm/`, cuffcompare against the reference annotation, and cuffdiff across the
two conditions — the `Cuffdiff/` folder holds the FPKM and read-group tracking
tables and the `*_exp.diff` results.

Software versions the exercises target: samtools 1.2, bowtie2 2.2.2, tophat 2.0.14,
cufflinks / cuffmerge / cuffcompare / cuffdiff 2.2.1.

## 4. Bioconductor for Genomic Data Science

Four module quizzes as R Markdown: `GenomicRanges` and interval operations,
`BSgenome` and sequence retrieval, annotation and expression containers, and
working with alignment and epigenomic data in Bioconductor.

## 5. Statistics for Genomic Data Science

Four module quizzes as R Markdown, covering exploratory analysis and
transformation, linear models and model fitting, multiple testing and correction,
and the reading of a published analysis. Two supporting figures are included.

---

## What this repository does not contain

**The Specialization capstone is not here.** An earlier version of this README
described a capstone NGS pipeline on the human reference (hg19/hg38). That pipeline
is not in these folders. The human data present is the chromosome 1 excerpt used by
the Algorithms course; the end-to-end alignment, variant calling and RNA-seq work is
on *Arabidopsis thaliana* and comes from the Command Line Tools course. This README
has been corrected to describe what is actually committed.

**No independent research question.** The exercises are the courses' own. For work
where I set the question, designed the controls and fixed the criteria before running
anything, see:

- [vhh-mpnn-selfconsistency](https://github.com/OHfromH2O/vhh-mpnn-selfconsistency)
  — do ProteinMPNN redesigns fold back to the backbone they came from?
- [pdl1-rfdiffusion-hotspots](https://github.com/OHfromH2O/pdl1-rfdiffusion-hotspots)
  — does naming the hotspots change what RFdiffusion produces?

---

## Stack

| | |
|---|---|
| Languages | Python (Jupyter), R (R Markdown), Bash |
| Libraries | Bioconductor, GenomicRanges, BSgenome |
| Command line | samtools, bcftools, bowtie2, tophat, cufflinks, cuffmerge, cuffcompare, cuffdiff, bedtools |
| Formats handled | FASTA, FASTQ, SAM/BAM, BED, GTF/GFF3, VCF/BCF, FPKM tracking tables |

## Layout

```
1_Python/                FASTA parsing notebooks + data
2_Algorithms/            Project1-4: notebooks, helper modules, reads
3_Command_Line_Tools/    Module1-4: quizzes + full pipeline working data
4_Bioconductor/          Module1-4 quizzes (.Rmd)
5_Statistics/            Module1-4 quizzes (.Rmd) + figures
```

Certificates for the individual courses are listed on my
[LinkedIn](https://www.linkedin.com/in/jeongho-choi/).
