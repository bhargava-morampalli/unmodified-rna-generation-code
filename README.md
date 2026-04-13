# Native vs. IVT RNA Coverage Analysis

Repository for reproducing all figures from the paper:
**Transcriptome-wide generation of unmodified RNA controls for nanopore epitranscriptome profiling via T7-coupled strand switching**

---

## Overview

Four Jupyter notebooks compare genome-wide coverage patterns between Native RNA and In Vitro Transcribed (IVT) RNA sequencing data from *E. coli* K-12, validating that IVT RNA faithfully reproduces native RNA coverage across the genome.

| Notebook | Figures Generated |
|---|---|
| `figs-2-3-4.ipynb` | Fig. 2, Fig. 3, Fig. 4 |
| `fig5_native_vs_ivt_correlation.ipynb` | Fig. 5 |
| `supp_fig_S1_technical_reprod.ipynb` | Supp. Fig. S1 |
| `supp_fig_S2_stratified_correlations.ipynb` | Supp. Fig. S2 |

---

## Input Files

### Coverage Files

Tab-separated files produced by `samtools depth`, with three columns (chrom, position, depth), one file per sample replicate:

| Directory | Files |
|---|---|
| `coverages/native/` | `k12_native_full_bc1.txt`, `k12_native_full_bc2.txt`, `k12_native_full_bc3.txt` |
| `coverages/ivt/` | `k12_ivt_full_bc1.txt`, `k12_ivt_full_bc2.txt`, `k12_ivt_full_bc3.txt` |

### rRNA Coordinates File

**`rrna_coordinates.csv`** — Required only by `supp_fig_S2_stratified_correlations.ipynb`. Contains 22 rRNA genes across 7 operons in *E. coli* K-12 (NC_000913.3), with columns: gene name, start position, end position.

### Expected Directory Structure

```
unmodified-rna-generation-code/
├── figs-2-3-4.ipynb
├── fig5_native_vs_ivt_correlation.ipynb
├── supp_fig_S1_technical_reprod.ipynb
├── supp_fig_S2_stratified_correlations.ipynb
├── rrna_coordinates.csv
├── coverages/
│   ├── native/
│   │   ├── k12_native_full_bc1.txt
│   │   ├── k12_native_full_bc2.txt
│   │   └── k12_native_full_bc3.txt
│   └── ivt/
│       ├── k12_ivt_full_bc1.txt
│       ├── k12_ivt_full_bc2.txt
│       └── k12_ivt_full_bc3.txt
├── output/
│   ├── figs-pngs/        ← auto-created by figs-2-3-4 notebook
│   └── figs-svgs/        ← auto-created by figs-2-3-4 notebook
├── suppfig_s1/           ← auto-created by supp_fig_S1 notebook
└── suppfig_s2/           ← auto-created by supp_fig_S2 notebook
```

> **Tip:** If your coverage files live elsewhere, update the path variables at the top of each notebook.

---

## Requirements

### Python Packages

```
numpy
pandas
matplotlib
seaborn
scipy
```

### Environment

- Python 3.10+
- Jupyter Notebook or JupyterLab

### Installation

```bash
pip install -r requirements.txt
```

---

## Usage

Run the notebooks in the following order:

1. **`figs-2-3-4.ipynb`** — genome-wide coverage visualizations comparing Native and IVT RNA at per-base, 100 bp, and 1 kb resolutions
2. **`fig5_native_vs_ivt_correlation.ipynb`** — correlation analysis validating that IVT RNA faithfully reproduces native RNA coverage patterns
3. **`supp_fig_S1_technical_reprod.ipynb`** — pairwise correlation analysis across biological replicates within each condition
4. **`supp_fig_S2_stratified_correlations.ipynb`** — stratified correlations separating rRNA regions from the rest of the genome

Each notebook automatically creates its output folder and saves figures in high-resolution PNG and PDF/SVG formats.

---

## Outputs

| Output Folder | Contents |
|---|---|
| `output/figs-pngs/`, `output/figs-svgs/` | Fig. 2, 3, 4 — coverage plots (PNG 600 dpi, SVG) |
| `output/` | Fig. 5 — Native vs. IVT correlation plots (PNG, PDF) |
| `suppfig_s1/` | Supp. Fig. S1 — replicate reproducibility plots (PNG, PDF) + CSV summary table |
| `suppfig_s2/` | Supp. Fig. S2 — stratified correlation plots (PNG, PDF) + CSV summary table |
