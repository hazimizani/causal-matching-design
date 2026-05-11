# Matching as Design

Recovering a causal effect from observational data by constructing a matched quasi-experiment.

## What this project does

Uses the **LaLonde** dataset (NSW job training program, with non-experimental CPS controls) to estimate the Average Treatment Effect (ATE) of training on 1978 earnings. Because LaLonde's experimental benchmark (~$1,794) is known, the analysis is a stress test of whether matching can recover the true effect from observational data alone.

The pipeline:

1. **Covariate selection and balance diagnostics** — standardized mean differences (SMDs), variance ratios, and density overlap before any adjustment.
2. **Propensity score estimation** — logistic regression of treatment on pre-treatment covariates.
3. **Matching** — nearest-neighbor 1:1 propensity score matching, with and without a caliper, and full matching as a robustness check.
4. **Post-matching balance** — SMDs, Love plots, and propensity score overlap to verify the matched sample resembles a randomized experiment.
5. **ATE estimation** — difference in means on `re78` over the matched sample, compared against the experimental benchmark.

## Files

| Path | Purpose |
|---|---|
| `analysis.Rmd` | R Markdown notebook — full reproducible analysis (load data, estimate PS, match, diagnose balance, estimate ATE). |
| `report.tex` | LaTeX writeup with methodology, results, and discussion. |
| `images/` | Pre-rendered figures used in the report (Love plots, density plots, PS overlap). |

## Requirements

- R (≥ 4.0)
- Packages: `MatchIt`, `dplyr`, `cobalt` (for some diagnostics), `ggplot2`

```r
install.packages(c("MatchIt", "dplyr", "cobalt", "ggplot2"))
```

The LaLonde data ships with `MatchIt` (`data("lalonde")`), so no external download is needed.

## Reproducing the analysis

```bash
# Render the notebook
Rscript -e 'rmarkdown::render("analysis.Rmd")'

# Compile the report
pdflatex report.tex
```

## Key references

- LaLonde, R. (1986). *Evaluating the Econometric Evaluations of Training Programs with Experimental Data.* American Economic Review.
- Rosenbaum, P. R., & Rubin, D. B. (1983). *The Central Role of the Propensity Score in Observational Studies for Causal Effects.* Biometrika.
- Stuart, E. A. (2010). *Matching Methods for Causal Inference: A Review and a Look Forward.* Statistical Science.

## Author

Hazim bin Mohd Izani.
