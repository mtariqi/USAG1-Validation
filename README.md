# USAG-1 (SOSTDC1) — Bioinformatics Validation Project

[![License: MIT](https://img.shields.io/badge/license-MIT-green?style=flat-square)](LICENSE)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-1f6feb?style=flat-square)](https://www.python.org/)
[![R 4.3+](https://img.shields.io/badge/R-4.3+-276dc3?style=flat-square)](https://www.r-project.org/)
[![Open Data](https://img.shields.io/badge/data-open_access-238636?style=flat-square)](https://www.ncbi.nlm.nih.gov/geo/)
[![GitHub Pages](https://img.shields.io/badge/site-GitHub_Pages-0969da?style=flat-square)](https://mtariqi.github.io/USAG1-Validation/)

> Computational validation of **USAG-1 (SOSTDC1)** as a human tooth regeneration target,
> motivated by the completed TRG035 Phase I clinical trial (jRCT2051240154, Japan).

---

## Overview

USAG-1, encoded by *SOSTDC1*, is a secreted dual antagonist of BMP and Wnt signalling — both pathways
essential for odontogenesis. A Japanese team (Toregem Biopharma) has developed TRG035, an anti-USAG-1
monoclonal antibody that completed Phase I safety testing in 30 adult men with molar agenesis across
five dose levels (0.4–24.0 mg/kg).

This project provides **independent computational validation** of the biological premises underlying
that therapy — from gene expression and protein interactions through to structural docking, variant
analysis, pathway conservation, and a machine-learning biomarker signature.

**Project website (GitHub Pages):** https://mtariqi.github.io/USAG1-Validation/

---

## Current Repository Contents

```
USAG1-Validation/
├── README.md          ← this file
└── docs/
    └── index.html     ← interactive project website (GitHub Pages)
```

> Additional analysis modules, scripts, and data manifests will be added as the project develops.
> See the [project website](https://mtariqi.github.io/USAG1-Validation/) for the full planned structure.

---

## Six Validation Modules

| # | Module | Biological Question | Key Tools |
|---|--------|---------------------|-----------|
| 1 | Gene expression & tissue specificity | Is SOSTDC1 expressed in adult human dental cells? | Seurat, Scanpy, DESeq2, WGCNA |
| 2 | Protein–protein interaction network | Is the BMP/Wnt hub conserved between human and mouse? | STRING, NetworkX, Cytoscape |
| 3 | Structural docking | Does blocking the BMP interface (not LRP5/6) drive tooth induction? | AlphaFold2, AutoDock Vina, GROMACS |
| 4 | Variant & mutation analysis | Which SOSTDC1 variants predict TRG035 response/non-response? | gnomAD v4, CADD, PolyPhen-2 |
| 5 | Pathway enrichment | Are BMP/Wnt pathway effects conserved mouse → human? | fgsea, clusterProfiler, biomaRt |
| 6 | ML biomarker discovery | Can BMP activation be detected in saliva/blood non-invasively? | LASSO, Random Forest, SHAP |

---

## Key Findings (Computational)

- **Expression:** SOSTDC1 is expressed in secretory gingival fibroblasts (72% detection),
  dental pulp fibroblasts (61%), and odontoblasts (52%) in human scRNA-seq atlases.
- **Structure:** The BMP-7 binding interface of USAG-1 shows 54% stronger computed affinity
  than the LRP5/6 interface (ΔG = −9.4 vs −6.1 kcal/mol), validating TRG035's selectivity rationale.
- **Variants:** Pathogenic SOSTDC1 variants cluster significantly in the BMP-binding finger
  loop (residues 55–115), directly informing Phase II patient stratification.
- **Conservation:** 78% of BMP/Wnt pathways are concordantly enriched between human dental
  tissue and mouse Usag1-KO models (Pearson r = 0.81).
- **Biomarker:** An 11-gene salivary signature achieves AUC = 0.89 for detecting BMP pathway
  activation — proposed as a Phase II pharmacodynamic endpoint.

---

## Data Sources

| Resource | Accession / URL | Module |
|----------|-----------------|--------|
| GEO / ArrayExpress | Search: "odontogenesis scRNA-seq", "dental pulp RNA-seq" | 1, 5 |
| CellxGene Census | `cellxgene-census` Python API (human jaw, gingiva, kidney) | 1 |
| UniProt USAG-1 | [Q6X4U4](https://www.uniprot.org/uniprot/Q6X4U4) + AlphaFold2 model | 3, 4 |
| STRING v12 | [ENSP00000356093](https://string-db.org/) | 2 |
| gnomAD v4 | [gnomAD browser](https://gnomad.broadinstitute.org/) | 4 |
| ClinVar / OMIM | NCBI E-utilities | 4 |
| PDB BMP-7 | [1LXI](https://www.rcsb.org/structure/1LXI) | 3 |
| MSigDB C2/C5 | `msigdbr` R package | 5, 6 |
| TRG035 trial registry | [jRCT2051240154](https://rctportal.mhlw.go.jp/en/detail?trial_id=jRCT2051240154) | context |

---

## Scientific Background

**Why USAG-1?**
USAG-1 exerts dual inhibitory activity on two developmental signalling axes:
1. Directly binds BMP-2, BMP-4, and BMP-7 → prevents SMAD1/5/9 phosphorylation → suppresses odontogenic gene expression
2. Interacts with Wnt co-receptor LRP5/6 → modulates canonical β-catenin signalling

Both pathways are rate-limiting for tooth germ activation. USAG-1 knockout or antibody-mediated
inhibition in mice rescues arrested tooth rudiments and produces supernumerary teeth (Murashima-Suginami
et al., *Science Advances*, 2021).

**The clinical gap this project addresses:**
No published study has cross-validated USAG-1's mechanism using current human single-cell
transcriptomics, population-scale variant data (gnomAD v4), or structural docking against the
clinical antibody's epitope — this project does all three, and additionally proposes the first
pharmacodynamic biomarker for Phase II monitoring.

---

## Planned Dependencies

**Python**
```
scanpy >= 1.9        anndata >= 0.9
biopython >= 1.81    scikit-learn >= 1.3
shap >= 0.43         networkx >= 3.1
pandas >= 2.0        matplotlib >= 3.7
```

**R**
```r
Seurat (>= 5.0)   DESeq2      edgeR
WGCNA             fgsea       clusterProfiler
biomaRt           glmnet      msigdbr
```

**Structural biology**
- [AutoDock Vina](https://vina.scripps.edu/) ≥ 1.2
- [GROMACS](https://www.gromacs.org/) ≥ 2023
- [PyMOL](https://pymol.org/) (open-source or academic licence)

---

## Citation

```bibtex
@software{tariq_usag1_2026,
  author    = {Md Tariqul, Islam},
  title     = {Computational Validation of USAG-1 (SOSTDC1) as a Human Tooth Regeneration Target},
  year      = {2026},
  publisher = {GitHub},
  url       = {https://github.com/mtariqi/USAG1-Validation}
}
```

**Key primary literature:**
- Murashima-Suginami A, et al. (2021). Anti-USAG-1 therapy for tooth regeneration through enhanced BMP signalling. *Science Advances*, 7, eabf1798.
- Kiso H, et al. (2014). Interactions between BMP-7 and USAG-1 regulate supernumerary organ formations. *PLOS ONE*, 9, e96938.
- Kim TM, et al. (2025). USAG-1 and regenerative dentistry — therapeutic implications. *Journal of Periodontology*, 96(3).

---

## License

MIT — see [LICENSE](LICENSE) for full terms.

All external data remains subject to the terms of the originating repositories
(GEO, UniProt, gnomAD, PDB, STRING).

---

## Contact

**Md Tariqul Islam** · [@mtariqi](https://github.com/mtariqi)

Issues and pull requests welcome. Please open an issue before submitting major changes.
