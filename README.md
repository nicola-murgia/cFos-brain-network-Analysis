# cFos Brain Network Analysis

Network analysis of c-Fos expression data comparing **psilocybin**, **ketamine**, and **saline** conditions. Whole-brain correlation matrices are analyzed for community structure, node centrality, backbone topology, communication efficiency, and virtual lesion impact.

## Overview

This repository contains the complete output of a GPU-accelerated network analysis pipeline applied to c-Fos expression data across three pharmacological conditions (n=4 animals per group, 237 brain regions). The analysis reveals that psilocybin produces the most topologically divergent network state from saline, while ketamine occupies an intermediate position.

## Key Findings

- **Community structure**: Both drug conditions collapse to 2 large modules; saline resolves into 8 smaller modules
- **Whole-network similarity**: Psilocybin–Ketamine > Ketamine–Saline > Psilocybin–Saline (Mantel test)
- **Backbone topology**: Ketamine forms the most integrated giant component (67% vs 53%)
- **Virtual lesion**: Psilocybin shows the highest peak lesion impact, suggesting concentrated hub dependence
- **No single region survives FDR correction** for centrality differences — effects are distributed, not localizable

## Repository Structure

```
├── data/                          # Raw analysis outputs (CSV)
│   ├── backbone_edges.csv         # Sparse backbone edge list
│   ├── centrality_results.csv     # Node centrality metrics
│   ├── centrality_bootstrap_ci.csv
│   ├── cluster_summary.csv        # Community detection results
│   ├── corr_KET.csv               # Ketamine correlation matrix
│   ├── corr_PSI.csv               # Psilocybin correlation matrix
│   ├── corr_SAL.csv               # Saline correlation matrix
│   ├── disruption_results.csv     # Network disruption curves
│   ├── efficiency_curves.csv      # Global efficiency curves
│   ├── efficiency_bootstrap_ci.csv
│   ├── lesion_concordance.csv     # Lesion-impact concordance tests
│   ├── lesion_impact.csv          # Virtual lesion results
│   ├── mantel_results.csv         # Whole-network Mantel tests
│   ├── permutation_results.csv    # Region-level permutation tests
│   ├── region_categories.csv      # Anatomical category assignments
│   ├── region_list.csv            # Region name index
│   └── region_stats.csv           # Per-region statistics
├── figures/                       # Publication-quality figures (SVG)
│   ├── fig1_correlation_matrices.svg
│   ├── fig2_centrality_allregions.svg
│   ├── fig3_disruption_curves.svg
│   ├── fig4_backbone_spring.svg
│   ├── fig5_chord_KET.svg
│   ├── fig5_chord_PSI.svg
│   ├── fig5_chord_SAL.svg
│   ├── fig6_cluster_overlap.svg
│   ├── fig7_mantel_summary.svg
│   ├── fig8_region_volcano_betweenness.svg
│   ├── fig9_lesion_impact.svg
│   └── fig10_lesion_concordance.svg
├── scripts/
│   └── GPU_Brain_Network_pipeline.ipynb   # Complete analysis pipeline
├── docs/
│   ├── REPORT.md                  # Executive summary report
│   └── RESULTS.md                 # Detailed results interpretation
├── LICENSE                        # MIT License
└── README.md                      # This file
```

## Pipeline

The analysis was performed using a custom GPU-accelerated pipeline (CuPy on NVIDIA RTX 3090 Ti) implementing:

1. **Correlation matrices** — Pearson r across all region pairs per condition
2. **Community detection** — Voronoi partitioning with modularity selection
3. **Centrality metrics** — Betweenness, closeness, weighted degree (with bootstrap CIs)
4. **Backbone extraction** — Top 2% strongest edges, spring-layout visualization
5. **Network disruption** — Sequential edge removal vs randomized null models
6. **Mantel tests** — Whole-network similarity between conditions
7. **Virtual lesion analysis** — Single-region removal impact on global efficiency
8. **Permutation tests** — Region-level statistics with BH-FDR correction

## Usage

The Jupyter notebook in `scripts/` contains the full reproducible pipeline. To run:

```bash
jupyter notebook scripts/GPU_Brain_Network_pipeline.ipynb
```

Requirements: Python 3.11+, CuPy (GPU), NetworkX, pandas, numpy, scipy, matplotlib

## Data

All data are derived from c-Fos expression experiments. Correlation matrices represent inter-regional co-expression patterns across 237 brain regions from the Allen Brain Atlas ontology.

## License

This project is licensed under the MIT License — see [LICENSE](LICENSE) for details.

## Citation

If you use this work, please cite:

```
Murgia et al., 2026. Network analysis of c-Fos expression reveals divergent 
topological signatures of psilocybin and ketamine.
```

## Contact

Nicola Murgia — [GitHub](https://github.com/nicola-murgia)
