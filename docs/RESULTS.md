# Results: Psilocybin, Ketamine, and Saline c-Fos Network Analysis

*Interpretation of pipeline output figures (Murgia et al. 2026 network methodology applied to the psilocybin/ketamine/saline c-Fos dataset). All values below were read directly off the figures; no underlying CSV/statistics tables were available, so region names are reported as truncated on the axis labels where the full label was not legible.*

---

## 1. Community structure differs sharply between saline and the two drugs (Fig. 1)

Whole-brain Pearson correlation matrices were partitioned into modules for each condition:

| Condition | Number of modules (*k*) | Modularity (*Q*) |
|---|---|---|
| Psilocybin | 2 | 0.081 |
| Ketamine | 2 | 0.083 |
| Saline | 8 | 0.059 |

Both drug conditions collapse onto a simple **two-module** partition with modestly higher modularity than saline, whereas saline resolves into **eight** smaller modules with lower modularity. Visually, the saline matrix (panel C) shows a fine-grained block-diagonal structure with several small, tightly-correlated sub-blocks, while psilocybin and ketamine (panels A–B) show two large, coarser blocks — i.e., drug administration appears to *coarsen* the correlational architecture into fewer, larger communities rather than preserving the saline-like fine parcellation.

## 2. Node centrality: no single metric or region survives correction, but broad group tendencies are visible (Fig. 2, Fig. 8)

Betweenness, closeness, and weighted degree were computed for every region under each condition (bootstrap SEM error bars; label color denotes the smallest raw *p*-value across pairwise comparisons, uncorrected).

- **Weighted degree** (panel C): Ketamine tends to show the highest values across most regions, saline is a close second, and psilocybin is consistently the lowest of the three.
- **Closeness** (panel B): the ordering shifts — saline is consistently highest, ketamine intermediate, psilocybin lowest.
- **Betweenness** (panel A): no consistent group ordering is apparent; bars overlap heavily and bootstrap SEMs are large relative to the between-group differences.

Critically, when these region-level betweenness differences are tested formally against a label-permutation null and corrected for multiple comparisons (Fig. 8, BH-FDR), **no single region reaches significance in any of the three pairwise comparisons** (Psilocybin vs. Saline, Ketamine vs. Saline, Psilocybin vs. Ketamine) — every point falls far below the −log10(0.05) ≈ 1.3 threshold. This confirms that the region-colored "raw *p* < 0.05" labels visible in Fig. 2 do not survive FDR correction, and that condition effects on centrality are **not localizable to individual regions** at this sample size.

## 3. Real networks resist targeted (strong-edge) attack far more than randomized nulls, in all conditions (Fig. 3)

Global efficiency (*E<sub>g</sub>*, normalized) was tracked while removing edges either strongest-first or weakest-first, benchmarked against a pooled randomized-network null (grey 95% CI band).

- **Strong links removed first** (panels A, C, E): in every pairwise comparison, the empirical curves (colored) sit *above* the null curve (dashed black) across nearly the entire removal range, with pointwise significance (green ticks) at most steps up to ~15,000 edges removed. This means the true correlational networks are **more resilient to loss of their strongest connections** than degree/weight-matched random networks — evidence of a non-random, redundant "rich" backbone in all three conditions.
- **Weak links removed first** (panels B, D, F): efficiency stays flat at 1.0 and indistinguishable from the null band throughout, as expected (removing weak edges first does not touch the connectivity that drives global efficiency).
- The two drug conditions and saline track each other very closely within each panel, i.e., **this "above-null resilience" property itself does not obviously differentiate psilocybin/ketamine from saline** — it is a shared feature of all three condition networks.

## 4. Sparse "backbone" topology: ketamine forms the most integrated giant component (Fig. 4)

Retaining only the strongest 2% of edges (559 edges) per condition and laying out the resulting backbone with a spring layout:

| Condition | Giant component (% of nodes) |
|---|---|
| Psilocybin | 53% |
| Ketamine | **67%** |
| Saline | 53% |

Ketamine's backbone is qualitatively more consolidated into one large connected cluster, while psilocybin's and saline's backbones fragment into a comparably sized giant component (53%) with more isolated/peripheral nodes. Each condition's backbone is organized around a small set of core hub regions (labeled clusters near the network center); the specific hub label sets differ visibly across conditions.

## 5. Top 5%-of-edges chord diagrams: predominantly positive correlations across all conditions (Fig. 5)

For all three conditions, the strongest 5% of pairwise correlations (by |*r*|) are overwhelmingly **positive** (red arcs), with a smaller number of negative (blue) long-range arcs, several of which involve thalamic and hypothalamic regions crossing to isocortical/cerebellar regions. Qualitatively, the ketamine chord diagram appears the densest and most homogeneously red, with comparatively fewer prominent negative arcs, while psilocybin and saline show more visually salient negative (blue) long-range connections crossing the circle.

## 6. Community partitions do not align across conditions (Fig. 6)

Pairwise Adjusted Rand Index (ARI) between the community partitions of Fig. 1:

| | Psilocybin (k=2) | Ketamine (k=2) | Saline (k=8) |
|---|---|---|---|
| Psilocybin | 1.000 | −0.003 | 0.008 |
| Ketamine | −0.003 | 1.000 | −0.001 |
| Saline | 0.008 | −0.001 | 1.000 |

All off-diagonal ARI values are indistinguishable from zero, indicating that module membership is **essentially uncorrelated across conditions** — i.e., condition-specific partitions do not simply "coarsen" or "split" a shared underlying modular scaffold. The figure's own caption notes this should be interpreted cautiously given the mismatched cluster counts (*k* = 2, 2, 8), which mechanically pulls ARI toward zero.

## 7. Whole-network similarity (Mantel test): drug conditions are more similar to each other than either is to saline (Fig. 7)

Node-permutation Mantel tests comparing whole correlation matrices:

| Comparison | Observed Mantel *r* | *p* | *q* (FDR) |
|---|---|---|---|
| Psilocybin vs. Saline | 0.093 | 0.011 | 0.011 |
| Ketamine vs. Saline | 0.137 | 0.001 | 0.001 |
| Psilocybin vs. Ketamine | **0.156** | 0.000 | 0.001 |

All three comparisons exceed their respective permutation nulls, so all condition pairs share more network structure than expected by chance. However, the effect size gradient is informative: **Psilocybin vs. Ketamine shows the strongest whole-network similarity**, followed by Ketamine vs. Saline, with **Psilocybin vs. Saline the weakest (though still significant) relationship** — consistent with psilocybin producing the network state most divergent from the saline baseline, while ketamine sits topologically "closer" to saline than psilocybin does.

## 8. Virtual lesion analysis: distinct, condition-specific critical hubs, with drug conditions showing larger peak impact (Fig. 9)

Regions were removed one at a time and the resulting drop in global efficiency (ΔE<sub>g</sub>) recorded. Top-15 most critical regions per condition:

- **Psilocybin** (peak ΔE<sub>g</sub> ≈ 1.17): tuberomammillary nucleus, interfascicular nucleus, spinal nucleus, primary somatosensory cortex, inferior colliculus, lateral visual area, (additional) primary somatosensory subregion, anterior amygdalar area, paraventricular nucleus, anterior olfactory nucleus, agranular insular cortex, fiber tracts, superior olivary complex, visceral area, induseum griseum.
- **Ketamine** (peak ΔE<sub>g</sub> ≈ 1.08): anterior hypothalamic nucleus, dorsal cochlear nucleus, fiber tracts, anteromedial nucleus, lateral visual area, parasubthalamic nucleus, accessory supraoptic group, tuberomammillary nucleus, interfascicular nucleus, dorsal peduncular area, central lateral nucleus, primary somatosensory cortex, entorhinal area, induseum griseum, perirhinal area.
- **Saline** (peak ΔE<sub>g</sub> ≈ 0.98): piriform-amygdalar area, locus ceruleus, fiber tracts, ventral tegmental area, paraventricular nucleus, cortical amygdalar area, pontine reticular nucleus, dorsal motor nucleus, tuberomammillary nucleus, paramedian lobule, dorsal premammillary nucleus, prelimbic area, ventral premammillary nucleus, rhomboid nucleus, "nucleus of the..." (label truncated).

Two points stand out:

1. **Peak lesion impact scales with condition**: Psilocybin > Ketamine > Saline (≈1.17 vs. ≈1.08 vs. ≈0.98), meaning the single most critical node produces a proportionally larger efficiency collapse under the drug conditions — especially psilocybin — than under saline, despite psilocybin's networks generally showing *lower* weighted degree/closeness in Fig. 2. This suggests psychedelic/dissociative states may concentrate functional dependence onto fewer, more indispensable hub regions even while overall connectivity strength is not elevated.
2. **No region in any condition is a strict backbone articulation point** (the legend's red category is unused in all three panels) — i.e., these are high-impact hubs in the weighted, continuous sense, not single points of failure in the sparse binary backbone graph.
3. Several regions recur across two or more conditions' top-15 lists — most notably the **tuberomammillary nucleus**, **fiber tracts**, **paraventricular nucleus**, and **induseum griseum/entorhinal-perirhinal** areas — pointing to a conserved neuromodulatory/hypothalamic-limbic hub set that remains functionally important regardless of condition, layered with condition-specific hubs (e.g., locus ceruleus/VTA unique to saline; anterior hypothalamic/parasubthalamic unique to ketamine).

## 9. Lesion-impact concordance: psilocybin and ketamine share the most similar hub architecture (Fig. 10)

Spearman correlation of regional lesion-impact rankings between conditions:

| Comparison | Spearman ρ | *p* | *q* (FDR) |
|---|---|---|---|
| Psilocybin vs. Saline | 0.111 | 0.080 | 0.080 (n.s.) |
| Ketamine vs. Saline | 0.176 | 0.007 | 0.010 |
| Psilocybin vs. Ketamine | **0.274** | 0.000 | 0.001 |

This mirrors the whole-network Mantel result (Section 7): **which regions are most functionally critical is most concordant between the two drug conditions**, moderately concordant between ketamine and saline, and **not statistically distinguishable from chance between psilocybin and saline**. Psilocybin therefore produces the hub architecture most distinct from the saline baseline, while ketamine's hub structure is intermediate — sharing significant, if partial, structure with both.

---

## Synthesis

Taken together, the twelve analyses converge on a consistent picture:

- **No condition effect is localizable to individual regions after multiple-comparison correction** (Fig. 8: betweenness volcano; Fig. 6: near-zero ARI). Region-level, single-metric statistics are underpowered or the effects are too distributed to survive FDR at the region level.
- **Condition effects are nonetheless robust and significant at the whole-network / distributed level.** All three networks are significantly more resistant to targeted (strong-edge) attack than randomized nulls (Fig. 3), and whole-network topology (Mantel, Fig. 7) and hub-criticality profiles (lesion concordance, Fig. 10) both show a consistent ordering: **Psilocybin–Ketamine > Ketamine–Saline > Psilocybin–Saline**, with the Psilocybin–Saline relationship the weakest of the three (borderline non-significant for lesion concordance). This places **psilocybin as the condition most topologically divergent from saline**, with **ketamine occupying an intermediate position**.
- **Ketamine's networks are the most integrated/consolidated**: fewer, larger modules with the highest modularity among the three (Fig. 1), the largest giant component in the sparse backbone (67% vs. 53%/53%, Fig. 4), and generally the highest weighted degree across regions (Fig. 2C).
- **Psilocybin's networks show a distinct signature**: generally lower weighted degree and closeness than saline/ketamine (Fig. 2), yet the *single* most functionally critical region produces the largest efficiency collapse of any condition when lesioned (Fig. 9) — suggesting a shift toward reliance on a smaller set of indispensable hubs (largely hypothalamic/limbic: tuberomammillary nucleus, paraventricular nucleus, anterior amygdalar/olfactory and agranular insular areas) rather than a uniformly "hyperconnected" network.
- A recurring hub set — **tuberomammillary nucleus, fiber tracts, paraventricular nucleus, and entorhinal/perirhinal/induseum griseum areas** — appears among the top-critical regions in at least two of the three conditions, suggesting these nodes anchor global efficiency largely independent of pharmacological state, on top of which each condition adds its own distinctive critical regions.

## Caveats

- All quantitative values were transcribed directly from rendered figure axes/annotations; no source data tables were provided, so exact per-region numeric values (e.g., individual weighted-degree or betweenness values) could not be extracted, only qualitative/ordinal group tendencies.
- Several axis region labels in Figs. 2 and 9 are truncated by the plotting layout; truncated names are reported as they appear (e.g., "primary somato...", "nucleus of the...").
- The Fig. 6 ARI comparison is confounded by unequal cluster counts (*k* = 2, 2, 8) across conditions, which mechanically biases ARI toward zero; a near-zero ARI is therefore suggestive but not conclusive evidence of unrelated modular organization.
- Fig. 2's per-region color-coded "significant" labels reflect **uncorrected** pairwise *p*-values (as stated in the panel title) and should be read alongside the FDR-corrected null result in Fig. 8, which found no surviving region.
