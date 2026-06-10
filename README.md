# Modeling Wound Healing Without Migration and Proliferation

## Abstract

This repository consolidates three source documents on retinal pigment epithelium (RPE) wound healing and morphology in the context of age-related macular degeneration (AMD). The material describes a cell-based framework for studying how RPE tissue repairs itself without explicit migration or proliferation, and it compares simulated repair behavior against published and experimental observations. The central modeling question is whether local tissue rearrangement, cell fusion, cell expansion, and purse-string closure can explain the observed recovery of wounded RPE monolayers and the morphological differences associated with aging and disease.

## Background

AMD is presented in the source material as a major cause of vision loss in the aging population, with the RPE identified as a principal site of pathology. The papers and poster emphasize that RPE morphology, topology, and repair dynamics may encode information about both tissue health and disease progression. This makes the system a useful test case for combining mathematical modeling, image-based quantification, and mechanistic biological interpretation.

## Research Aim

The work collected here pursues three closely related goals:

1. Quantitatively characterize how RPE morphology changes with age and AMD status.
2. Build a predictive model of RPE morphogenesis and wound healing.
3. Compare simulated repair mechanisms with human and mouse RPE morphology to support future diagnostic and prognostic tools.

## Source Materials

The source PDFs are kept locally in `materials/` for reference, but the folder is excluded from version control so the documents are not pushed to GitHub:

- `RPEWoundHealingModeling.pdf`
- `ModelingMechanism.pdf`
- `Modeling-Wound-Healing-Without-Migration-and-Proliferation_Poster.pdf`

## Biological Context

The source documents frame RPE wound healing as a problem of epithelial repair under stress. In healthy tissue, RPE cells maintain a tightly packed monolayer with characteristic polygonal geometry. In aging and AMD, that geometry becomes more irregular, and wound repair may involve local stretching, fusion, rearrangement, or closure around apoptotic cells rather than cell migration and proliferation alone.

## Modeling Framework

The main paper describes the RPE as a 2D cellular system modeled with a Cellular Potts-style lattice framework. The lattice assigns an identifier to each site, with connected domains representing individual cells. Cell boundaries, area constraints, and intercellular coupling contribute to the free-energy landscape, and Monte Carlo updates drive tissue evolution toward lower-energy configurations.

The mechanism summary expands this framework using a 2D Q-Potts cellular model with two dominant contributions to energy:

- coupling energy between neighboring cells
- area elasticity energy

This setup is used to simulate normal young and old RPE, and to test several candidate repair mechanisms after tissue damage.

## Repair Mechanisms

The mechanism document organizes the model into three repair families.

### 1. Purse-string closure

Purse-string closure is modeled by killing a cell or a cluster of cells and allowing neighboring cells to enlarge so that they stretch over the void. The nearest neighbors absorb the space left behind by the dead cell, and larger clusters require a correspondingly broader neighborhood response.

### 2. Cell fusion

Cell fusion is represented by repeated merging events in which one cell adopts the identity of a neighbor. The source material describes several variants:

- random fusion between adjacent cells
- wound-induced fusion within a damage zone
- chain fusion spreading through tissue after the initial wound response

The model allows repeated fusion up to the observed upper bound on nuclei count in RPE cells.

### 3. Cell expansion

In the expansion scenario, one cell enlarges substantially while neighboring cells shrink in a graded fashion. The model caps the maximum expansion and marks heavily compressed neighbors as dead if their size reduction exceeds a threshold.

## Simulated Experiments

The source documents compare several classes of simulation experiments:

- random cell killing in young and old tissue
- clustered cell death in young and old tissue
- apoptosis in small and medium drusen regions
- repair patterns under purse-string closure, fusion, and expansion
- cluster-based killing to emulate AMD-like damaged tissue

The poster adds a more explicit Compucell3D-based wound-healing study, where two parameters are varied:

- volume constraint
- neighborhood radii for wound influence and repair response

For each parameter setting, five random-seed runs are repeated and five wound-healing rounds are performed per run. The healing rate is summarized using the mean and standard deviation across the resulting 25 simulations.

## Reported Findings

Across the poster and source papers, several consistent qualitative findings appear:

- Higher volume constraints produce faster and more stable healing.
- The first neighborhood radius controls wound size.
- The second neighborhood radius controls how many surrounding cells participate in closure.
- Purse-string closure, fusion, and expansion each produce distinct tissue-scale signatures that can be compared with experimental RPE morphology.

The main paper also highlights a comparison between human RPE and simulation output, together with statistical descriptors such as area distributions, neighbor-count distributions, Voronoi index, texture tensor analysis, spatial point statistics, and second-order correlations.

## Data Analysis Tools

The source material uses several morphology and topology measures to compare simulation and experiment:

- cell area distributions
- number-of-neighbor distributions
- Voronoi index
- texture tensor analysis
- cumulative nearest-neighbor distance distributions
- second-order correlation of cell counts
- Aboav-Weaire law and Lewis law
- Ripley’s K function
- machine-learning or deep-learning classification features

## Interpretation

Taken together, the documents suggest that RPE wound healing can be studied as a mechanistic competition between local cell rearrangement strategies. The model does not assume that every repair event requires migration or proliferation. Instead, it explores whether geometric relaxation, fusion, and constrained expansion are sufficient to recover a stable epithelial pattern after damage. That makes the project useful both as a hypothesis test and as a quantitative bridge between image analysis and disease interpretation.

## Repository Layout

The repository is intentionally minimal:

- `README.md` provides a research-style summary of the source material.
- `materials/` stores the three PDFs used to prepare the summary.
- `.gitignore` excludes common operating-system, editor, Python, and derived-artifact clutter.

## Notes on Attribution

The README is a paraphrased synthesis of the supplied PDFs, not a verbatim reproduction. Any future manuscript, presentation, or derivative document should cite the original authors and venue information from the source files.

## Next Steps

If you want to extend this repository, the most natural follow-up is to add the simulation code, parameter tables, or figure reproductions alongside the source PDFs so the README can link each experiment to a concrete implementation.