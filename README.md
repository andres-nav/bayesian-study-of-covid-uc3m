# Bayesian Study of COVID-19 Dataset

Bayesian logistic regression analysis comparing frequentist and Bayesian approaches for COVID-19 classification using Mexican patient data.

## Dataset

**Source:** [Kaggle - COVID-19 Dataset (Mexico)](https://www.kaggle.com/datasets/meirnizri/covid19-dataset)  
**Size:** 1,048,576 patients, 21 features  
**Target:** Binary COVID-19 classification (positive/negative diagnosis)

## Methodology

1. **Beta-Bernoulli Conjugate Prior Analysis**
   - Analytical posterior distribution for COVID probability
   - Improper Beta(0,0) prior → Beta(k, n-k) posterior
   - Predicted probability: 0.362 (close to ML estimate of 0.38)

2. **Frequentist GLM Baseline**
   - Logistic regression with all features
   - Accuracy: ~65.8%
   - Identified significant variables via p-values

3. **Bayesian Logistic Regression**
   - MCMCpack implementation
   - Full posterior distributions for all coefficients
   - Credible intervals for parameter uncertainty

4. **Bayesian Lasso Variable Selection**
   - monomvn package for sparse variable selection
   - Selected features: SEX, PATIENT_TYPE, PNEUMONIA, AGE, CARDIOVASCULAR
   - Probability of non-zero coefficients visualized

5. **Final OpenBUGS Model**
   - Logistic model with selected predictors
   - Posterior analysis via credible intervals
   - Age-stratified predictions (20, 50, 80 years)

## Key Findings

**Significant Predictors:**
- **Age:** Strong positive effect (older → higher COVID probability)
- **Patient Type:** Hospitalized patients have significantly higher COVID probability
- **Pneumonia:** Strong indicator of COVID-19 presence

**Inconclusive Predictors:**
- **Sex:** Wide credible intervals, minimal effect
- **Cardiovascular:** Large uncertainty, not reliable

**Bayesian Advantage:** Posterior distributions enable better significance assessment through credible intervals, revealing that some variables with low frequentist p-values have high uncertainty and should not be trusted.

## Tech Stack

- **R** (R Markdown)
- **MCMCpack** — Bayesian logistic regression
- **monomvn** — Bayesian Lasso
- **R2OpenBUGS** — Final model implementation
- **caret** — Frequentist baseline

## How to Run

```r
# Install dependencies
install.packages(c("MCMCpack", "monomvn", "R2OpenBUGS", "caret", "ggplot2", "GGally"))

# Render the analysis
rmarkdown::render("code.Rmd")
```

**Note:** Requires OpenBUGS installed separately for the final model section.

## Files

- `code.Rmd` — Complete analysis workflow
- `data.csv` — COVID-19 dataset
- `code.html` / `code.pdf` — Rendered outputs

## Conclusion

Bayesian methods provide richer inference than frequentist approaches by quantifying parameter uncertainty through posterior distributions. This enables more informed decisions about predictor significance, especially when credible intervals are wide despite low p-values.