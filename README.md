# Crop Simulation Project: Fertilizer Effects in a 3x3 Field Design

## Project Overview
This project builds and tests a simulation framework for corn yield experiments using R. The core idea is to generate synthetic yield data for a blocked 3x3 field layout, then evaluate fertilizer effects with ANOVA across repeated simulation runs.

The work combines:
- custom data simulation (`simCorn`)
- linear modeling (`lm`)
- ANOVA-based hypothesis testing
- repeated Monte Carlo scenarios
- visualization of p-value distributions
- reproducible reporting through Quarto

## What the Project Accomplished
1. Created a reusable simulation function for a 3x3 experimental layout with fertilizer, row, and column effects.
2. Ran multiple simulation scenarios with different assumptions (normal vs exponential error, different effect vectors, different random seeds).
3. Fit the same ANOVA model repeatedly (`Yield ~ Fertilizer + Row + Column`) to evaluate fertilizer significance behavior.
4. Generated histogram-based diagnostics for p-values from each scenario.
5. Produced rendered outputs in Markdown, HTML, and PDF formats.

## Step-by-Step Walkthrough

### 1. Load dependencies
The script loads `tidyverse`:

- file: `stat415_final.R`
- line: `library(tidyverse)`

### 2. Define the simulation engine (`simCorn`)
`simCorn(...)` is the core function. It:
1. validates the seed input
2. creates error terms from a user-selected distribution (`dist`)
3. builds a fixed 9-plot field structure with factors:
   - `Fertilizer` (A/B/C)
   - `Row` (1/2/3)
   - `Column` (1/2/3)
4. computes yield as:

`Yield = overallEffect + fertilizerEffect + rowEffect + colEffect + error`

5. returns a data frame with one row per plot.

This makes it easy to swap assumptions while keeping the same experimental structure.

### 3. Run basic function checks
The project first runs simple examples of `simCorn`:
- default normal-error simulation
- gamma-error simulation with custom shape
- parameterized simulation with explicit overall, fertilizer, row, and column effects

These examples confirm that the function is flexible and reproducible.

### 4. Build repeated simulation scenarios
The main analysis creates seven p-value vectors (`p_vector_1` to `p_vector_7`), each with 100 simulated experiments.

For each iteration in each scenario:
1. generate synthetic data with `simCorn`
2. fit a linear model: `lm(Yield ~ Fertilizer + Row + Column, data=y)`
3. extract the fertilizer ANOVA p-value (`anova(fitCorn)$"Pr(>F)"[1]`)
4. store that p-value in the scenario vector

### 5. Compare scenarios using p-value histograms
Each scenario is visualized with `hist(...)` on p-values (common breaks from 0 to 1). This provides a quick view of whether p-values are broadly uniform or concentrated near 0.

### 6. Render results
The Quarto document (`final_project.qmd`) renders to:
- `final_project.md`
- `final_project.html`
- `final_project.pdf`

The plotted figures are stored under `final_project_files/figure-*`.

## Scenario Map (As Implemented)

| Scenario | Error distribution | Effect settings used in code | Notes |
|---|---|---|---|
| `p_vector_1` | Normal (`rnorm`) | baseline (`overallEffect=10`, other effects default) | Reference/null-like case |
| `p_vector_2` | Normal | fertilizer `c(1,2,3)`, row `c(0,0,1)`, col `c(0,0,1)` | Added treatment + mild blocking effects |
| `p_vector_3` | Normal | fertilizer `c(1,2,3)`, row `c(1,0,1)`, col `c(0,1,1)` | Stronger structure effects |
| `p_vector_4` | Normal | same parameterization as `p_vector_3` | Seed variation check |
| `p_vector_5` | Exponential (`rexp`) | fertilizer `c(1,2,3)`, row `c(0,0,1)`, col `c(0,0,1)` | Non-normal error case |
| `p_vector_6` | Exponential | fertilizer `c(1,2,3)`, row `c(1,0,1)`, col `c(0,1,1)` | Non-normal + structured effects |
| `p_vector_7` | Exponential | fertilizer `c(1,2,3)`, row `c(0,1,0)`, col `c(0,1,0)` | Loop stores into `p_vector_5` instead of `p_vector_7` |

## Skills Demonstrated
This project puts the following skills on display:

1. **Simulation design in R**
   - building a configurable generator function with distribution injection (`dist`) and variadic args (`...`)
2. **Experimental design thinking**
   - modeling row/column blocking with treatment factors
3. **Monte Carlo workflow**
   - repeated sampling and repeated model fitting across scenarios
4. **Statistical modeling**
   - linear models and ANOVA-based p-value extraction
5. **Reproducibility practices**
   - explicit use of `set.seed(...)` across scenarios
6. **Exploratory visualization**
   - distributional diagnostics through p-value histograms
7. **Technical reporting**
   - literate programming via Quarto and multi-format outputs (MD/HTML/PDF)

## Important Notes on Current Code Behavior
This repository preserves original work. The following points document how the current code behaves:

1. In scenario 7, p-values are assigned to `p_vector_5` rather than `p_vector_7` inside the loop.
2. Effect vectors (`fertilizerEffect`, `rowEffect`, `colEffect`) are added positionally and recycled by R; they are not mapped by factor level labels.

These notes are for interpretation clarity only; no source code was changed.

## How to Run
From the project directory:

```bash
cd /Users/devin/crop_simulation/Crop_simulation
```

Run the R script:

```bash
Rscript stat415_final.R
```

Render the Quarto report:

```bash
quarto render final_project.qmd
```

## Project Structure
- `stat415_final.R`: primary R script with simulation, loops, models, and plots.
- `final_project.qmd`: Quarto source document for the report.
- `final_project.md`: rendered Markdown report.
- `final_project.html`: rendered HTML report.
- `final_project.pdf`: rendered PDF report.
- `final_project_files/`: figure assets and Quarto library files.

## Summary
The project successfully demonstrates a full simulation-to-inference workflow for a blocked fertilizer experiment in R, including function engineering, repeated ANOVA evaluation, visual diagnostics, and publishable reporting artifacts.
