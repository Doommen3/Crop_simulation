# Crop Simulation Project

Monte Carlo simulation and ANOVA analysis of fertilizer effects in a 3x3 Latin square field design, built in R and documented with Quarto.

## Project Highlights
- Built a reusable simulation function (`simCorn`) for blocked agricultural experiments.
- Executed 7 simulation scenarios (100 runs each) to stress-test inference behavior under different assumptions.
- Fit and evaluated repeated linear models (`lm`) with ANOVA extraction of fertilizer p-values.
- Produced publication-ready outputs in Markdown, HTML, and PDF with reproducible workflows.

## Why This Project Matters
This project demonstrates end-to-end statistical engineering: model design, simulation, inference, visualization, and technical communication. It mirrors the type of workflow used in experimentation, analytics, and applied data science roles.

## Problem Statement
Given a 3x3 field layout where yield is affected by fertilizer, row, and column effects, how does the inferred fertilizer significance behave when we change:
- treatment and blocking effect configurations
- random seed
- error distribution (normal vs exponential)

## Technical Approach
1. Define a configurable simulation engine (`simCorn`) with parameters for overall effect, fertilizer effect, row effect, column effect, seed, and error distribution.
2. Generate synthetic field outcomes for a Latin square design with factors:
`Fertilizer`, `Row`, `Column`.
3. Fit a linear model on each simulated dataset:
`Yield ~ Fertilizer + Row + Column`.
4. Extract the fertilizer p-value from ANOVA.
5. Repeat across 100 iterations per scenario.
6. Compare p-value distributions with histograms across all scenarios.

## Scenario Coverage
Seven scenarios are implemented in `stat415_final.R`, spanning:
- baseline/no-treatment-effect setup
- multiple structured fertilizer-row-column effect settings
- normal-error and exponential-error assumptions

## Deliverables
- Reusable R simulation code in `/Users/devin/crop_simulation/Crop_simulation/stat415_final.R`
- Quarto analysis source in `/Users/devin/crop_simulation/Crop_simulation/final_project.qmd`
- Rendered report formats:
`/Users/devin/crop_simulation/Crop_simulation/final_project.md`,
`/Users/devin/crop_simulation/Crop_simulation/final_project.html`,
`/Users/devin/crop_simulation/Crop_simulation/final_project.pdf`
- Generated figures in `/Users/devin/crop_simulation/Crop_simulation/final_project_files`

## Skills Demonstrated
- Statistical simulation and experimental design modeling
- ANOVA-based inference and repeated model evaluation
- Reproducible research practices (`set.seed`, scripted workflows)
- Data visualization for distributional diagnostics
- Technical documentation and report publishing (Quarto)
- Clean analytical structuring from function design to communication

## Tech Stack
- R
- tidyverse
- base R modeling functions (`lm`, `anova`, `hist`)
- Quarto

## How To Run
```bash
cd /Users/devin/crop_simulation/Crop_simulation
Rscript stat415_final.R
quarto render final_project.qmd
```

## Repository Structure
- `/Users/devin/crop_simulation/Crop_simulation/stat415_final.R` - simulation and analysis script
- `/Users/devin/crop_simulation/Crop_simulation/final_project.qmd` - Quarto source
- `/Users/devin/crop_simulation/Crop_simulation/final_project.md` - rendered Markdown report
- `/Users/devin/crop_simulation/Crop_simulation/final_project.html` - rendered HTML report
- `/Users/devin/crop_simulation/Crop_simulation/final_project.pdf` - rendered PDF report
- `/Users/devin/crop_simulation/Crop_simulation/final_project_files` - figure and Quarto asset directory

## Summary
This repository showcases a complete statistical simulation pipeline with strong reproducibility and communication practices, making it a strong portfolio example for data science, analytics, and quantitative research roles.
