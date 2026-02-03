# Repeat Analysis Pipeline

This repository contains scripts and instructions used for **de novo repeat identification, annotation, activity analysis, base composition analysis, and functional motif discovery**, as described in **"Compositional dynamics and genomic distribution of transposable elements in the great tit (Parus Major)" (Eswaran et al., 2026)**.

The analysis uses tools such as **RepeatModeler2**, **RepeatMasker2**, **seqtk**, and **HOMER**.

---

## Repository Contents

- `RepeatAnalysis.md` – Main script collection with all steps and bash commands.
- Scripts for de novo repeat library generation, repeat annotation, activity analysis, and motif search.
- Example input and output files (if included).

---

## Requirements

- Python (tested with 3.12.3, other versions may also work)
- Bioinformatics software:
  - [RepeatModeler2]  
  - [RepeatMasker2]
  - [seqtk](https://github.com/lh3/seqtk)  
  - [HOMER](http://homer.ucsd.edu/homer/)  
- Standard Unix utilities (`bash`, `grep`, `wc`, `perl`)  

> Note: Adjust paths in scripts according to your local environment.

---
