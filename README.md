<div align="center">

# Crop Simulation

**A Monte Carlo simulation study of the Latin Square design for corn-yield experiments**

![R](https://img.shields.io/badge/R-276DC3?style=flat&logo=r&logoColor=white)
![Quarto](https://img.shields.io/badge/Quarto-75AADB?style=flat&logo=quarto&logoColor=white)
![tidyverse](https://img.shields.io/badge/tidyverse-1A162D?style=flat&logo=tidyverse&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat&logo=jupyter&logoColor=white)

</div>

## Overview

This is a computational statistics final project for STAT 415 that uses Monte Carlo
simulation to study a 3x3 Latin Square experimental design for evaluating corn yield.
Three fertilizer treatments (A, B, C) are arranged across a 3x3 grid so that each
treatment appears exactly once in every row and every column, allowing the design to
control for two sources of nuisance variation (row and column field effects) while
testing for a fertilizer effect. The study repeatedly simulates field data, fits an
ANOVA model, and examines the distribution of the resulting F-test p-values to assess
how the test behaves under different effect structures and error distributions.

## Features

- A configurable `simCorn()` data-generating function that builds a balanced 3x3 Latin
  Square with adjustable overall, fertilizer, row, and column effects.
- Pluggable error distributions, so the same design can be simulated with normal,
  gamma, or exponential noise (any R random-number generator can be passed in).
- Reproducible runs via optional seeding, with input validation on the seed argument.
- Monte Carlo loops that run 100 replications per scenario, fit an ANOVA model to each,
  and collect the fertilizer-effect p-value from every fit.
- Histograms of the p-value distributions used to visualize Type I error behavior under
  the null and statistical power under the alternative.
- Delivered as a reproducible Quarto report, a standalone R script, and a Jupyter
  presentation notebook.

## Tech stack

- **R** for the simulation, modeling (`lm`, `anova`), and plotting.
- **tidyverse** for data handling.
- **Quarto** (`final_project.qmd`) for the reproducible report, rendered to HTML, PDF,
  and GitHub-flavored Markdown.
- **Jupyter** (`Presentation.ipynb`) for the accompanying presentation.

## How it works

1. **Generate data.** `simCorn()` lays out the fixed Latin Square (fertilizer, row, and
   column factors) and computes a `Yield` response as the sum of the overall effect, the
   fertilizer effect, the row effect, the column effect, and a random error term drawn
   from the chosen distribution.
2. **Fit the model.** Each simulated dataset is fit with
   `lm(Yield ~ Fertilizer + Row + Column)`, and the ANOVA F-test p-value for the
   `Fertilizer` term is extracted.
3. **Replicate.** Each scenario repeats this 100 times and stores the p-values in a
   vector.
4. **Inspect the distribution.** Histograms of the p-values reveal the test's behavior:
   under a true null effect the p-values should be roughly uniform on (0, 1), while a
   genuine fertilizer effect pushes the distribution toward zero. Scenarios vary the
   effect sizes and swap normal errors for skewed (gamma/exponential) errors to probe
   the test's robustness.

## Getting started

**Prerequisites**

- [R](https://www.r-project.org/) (with the `tidyverse` package installed)
- [Quarto](https://quarto.org/) to render the report
- Optionally, Jupyter to open the presentation notebook

**Install the R dependency**

```r
install.packages("tidyverse")
```

**Run the simulation script**

```bash
Rscript stat415_final.R
```

**Render the Quarto report**

```bash
quarto render final_project.qmd
```

This produces `final_project.html`, `final_project.pdf`, and `final_project.md`.

**View the presentation**

Open `Presentation.ipynb` in Jupyter or any compatible notebook viewer.

## Author

**Devin Oommen** — [devinoommen.com](https://devinoommen.com) · Oommen & Company

## License

Released under the [MIT License](LICENSE).
