# Murgia pipeline v2 - summary report

Backend: GPU (cupy) (NVIDIA GeForce RTX 3090 Ti (23.5 GB, 1.9 GB free))
Animals: {'KET': 4, 'PSI': 4, 'SAL': 4}  |  Regions analysed: 237

## Group correlation structure
- Psilocybin (n=4): mean|r|=0.584, r range [-1.000, 1.000]
- Ketamine (n=4): mean|r|=0.647, r range [-0.999, 1.000]
- Saline (n=4): mean|r|=0.609, r range [-1.000, 1.000]

## Clustering (Voronoi, modularity-selected)
- Psilocybin: k=2 clusters, Q=0.0807 (gamma=0.50)
- Ketamine: k=2 clusters, Q=0.0829 (gamma=0.68)
- Saline: k=8 clusters, Q=0.0588 (gamma=2.82)
  ! cluster counts differ substantially across groups - any ARI-based comparison between them is confounded by this alone.

## Communication efficiency (baseline, intact network)
- Psilocybin: E_g=37.2383, E_l=37.1824  (MAX_ABS_R=0.9999)
- Ketamine: E_g=55.6928, E_l=55.6121  (MAX_ABS_R=0.9999)
- Saline: E_g=48.1304, E_l=48.0627  (MAX_ABS_R=0.9999)

## Backbone extraction
- Psilocybin: 2% of edges kept (559), giant component 52.7%
- Ketamine: 2% of edges kept (559), giant component 67.1%
- Saline: 2% of edges kept (559), giant component 52.7%

## Whole-matrix permutation test (n_perm=5000)
- PSI_vs_SAL: delta=0.5465, p=0.6479, q=0.9622
- KET_vs_SAL: delta=0.4747, p=0.9622, q=0.9622
- PSI_vs_KET: delta=0.5217, p=0.7814, q=0.9622

## Mantel test - whole-network similarity (n_perm=5000)
- PSI_vs_SAL: r=0.0927, p=0.0112, q=0.0112
- KET_vs_SAL: r=0.1366, p=0.0008, q=0.0012
- PSI_vs_KET: r=0.1564, p=0.0004, q=0.0012

## Region-level permutation test (wdeg/closeness n_perm=10000, betweenness n_perm=5000; BH-FDR < 0.05)
- PSI_vs_SAL / wdeg: 0 region(s) significant
- PSI_vs_SAL / closeness: 0 region(s) significant
- PSI_vs_SAL / betweenness: 0 region(s) significant
- KET_vs_SAL / wdeg: 0 region(s) significant
- KET_vs_SAL / closeness: 0 region(s) significant
- KET_vs_SAL / betweenness: 0 region(s) significant
- PSI_vs_KET / wdeg: 0 region(s) significant
- PSI_vs_KET / closeness: 0 region(s) significant
- PSI_vs_KET / betweenness: 0 region(s) significant

## Virtual lesion analysis - most functionally critical region per group
- Psilocybin: region index 0 (delta_Eg=1.1682); 28 backbone articulation point(s) total - see lesion_impact.csv for region names and the full ranking
- Ketamine: region index 18 (delta_Eg=1.0817); 22 backbone articulation point(s) total - see lesion_impact.csv for region names and the full ranking
- Saline: region index 167 (delta_Eg=0.9794); 19 backbone articulation point(s) total - see lesion_impact.csv for region names and the full ranking

## Lesion-impact concordance across conditions (n_perm=5000)
- PSI_vs_SAL: rho=0.1113, p=0.0804, q=0.0804
- KET_vs_SAL: rho=0.1760, p=0.0070, q=0.0105  (same regions critical in both)
- PSI_vs_KET: rho=0.2738, p=0.0002, q=0.0006  (same regions critical in both)

## Anatomical categories (Allen ontology major divisions)
- Isocortex: 37 region(s)
- Medulla: 37 region(s)
- Hypothalamus: 36 region(s)
- Thalamus: 26 region(s)
- Midbrain: 25 region(s)
- Cerebellum: 17 region(s)
- Pons: 15 region(s)
- Striatum: 12 region(s)
- Hippocampal formation: 12 region(s)
- Olfactory areas: 11 region(s)
- Pallidum: 5 region(s)
- Cortical subplate: 3 region(s)
- fiber tracts: 1 region(s)

## Disruption null model (randomized-network, n_null=100)
- PSI_vs_SAL: 15 edge-count steps, 0-16780 of 27966 edges (see disruption_results.csv for the pointwise p-values)
- KET_vs_SAL: 15 edge-count steps, 0-16780 of 27966 edges (see disruption_results.csv for the pointwise p-values)
- PSI_vs_KET: 15 edge-count steps, 0-16780 of 27966 edges (see disruption_results.csv for the pointwise p-values)

## Caveats to keep in view when reading these numbers
- n=4 animals/group minimum - this is a descriptive/exploratory analysis, not a powered study.
- Weighted degree and closeness saturate on this near-complete graph; see the z-scored versions (Figures 2, 5) rather than raw values.
- Efficiency-curve bootstrap CIs (if enabled) resample only 4 distinct animals per group - the band is coarse, not a publication-grade CI.
- Virtual lesion impact (delta_Eg) is a single-region removal from the point-estimate network, not animal-resampled - treat the region ranking as descriptive; only the concordance test between groups is significance-tested.