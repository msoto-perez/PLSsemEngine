# PLSsemEngine: A Transparent PLS-SEM Engine in Base R 📊

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20703909.svg)](https://doi.org/10.5281/zenodo.20703909)

**Version:** 1.3.0 (2026-06-15)

**PLSsemEngine** provides a transparent, modular, and reproducible implementation of Partial Least Squares Structural Equation Modeling (PLS-SEM), specifically designed for **composite-based Mode A estimation** of reflective models.

---

## 🌟 Purpose and Philosophy

The software prioritizes:

* **Algorithmic Transparency:** Implementation via pure base R matrix operations to ensure long-term stability.
* **Methodological Bridges:** Native integration with `lavaan` for CB-SEM/CFA cross-validation.
* **Explicit Analytical Control:** No hidden heuristics or automatic re-specifications; interpretive support is optional and researcher-led.
* **Modular Architecture:** Clear separation between estimation, inference, and prediction components.

---

## ⚙️ Computational Workflow

The engine follows a standardized and inspectable PLS-SEM pipeline:

1. **Data Standardization:** Handles mean-centered and standardized scales.
2. **Iterative Mode A Estimation:** Factorial weighting scheme by default.
3. **Measurement Evaluation:** Loadings, CR, AVE, HTMT, and **HTMT2**.
4. **Structural Estimation:** Path coefficients via OLS on latent scores with $f^2$ effect sizes.
5. **Inference:** Non-parametric percentile bootstrap for structural significance.
6. **Prediction:** Strict k-fold cross-validation following the `PLSpredict` protocol.
7. **Model Fit:** Assessment via SRMR, $d_{ULS}$, and $d_G$.

> **Note:** Deterministic sign alignment is implemented to ensure stability across resamples and eliminate sign indeterminacy.

---

## 🚀 What's New in V1.3.0 (Response to Reviewers)

* **Methodological Bridge:** Added `export_lavaan_syntax()` to translate PLS specifications for `lavaan`.
* **Interpretive Layer:** Added `interpret_model()` for diagnostic guidance based on established literature without forcing mechanical decisions.
* **Advanced Metrics:** Implemented **HTMT2** for congeneric models and global fit indices (SRMR, $d_{ULS}$, $d_G$).
* **Professional Packaging:** The software is now a fully versioned R package installable via `devtools`.
* **Inferential Prediction:** Added `cvpat()` implementing the Cross-Validated Predictive Ability Test (Liengaard et al., 2021; Sharma et al., 2023) for inferential testing of predictive superiority over a naive benchmark.

---

## 🛠️ Minimal Example

```r
# Install and load the engine
# devtools::install_github("msoto-perez/PLSsemEngine")
library(PLSsemEngine)

# 1. Generate data
set.seed(123)
data <- data.frame(
  SQ1=rnorm(100), SQ2=rnorm(100), SQ3=rnorm(100),
  CS1=rnorm(100), CS2=rnorm(100), CS3=rnorm(100),
  CL1=rnorm(100), CL2=rnorm(100), CL3=rnorm(100)
)

# 2. Define Models using Native R structures
mm <- list(
  Quality = c("SQ1", "SQ2", "SQ3"),
  Satisfaction = c("CS1", "CS2", "CS3"),
  Loyalty = c("CL1", "CL2", "CL3")
)

sm <- list(
  Satisfaction ~ Quality,
  Loyalty ~ Satisfaction + Quality
)

# 3. Run Analysis
model <- pls_sem(data=data, measurement_model=mm, structural_model=sm)

# 4. Methodological Bridge & Interpretation
export_lavaan_syntax(mm, sm)
interpret_model(model)

# 5. View Results
print(model$tables$table4)  # Structural Paths
```

📖 Citation
If you use this software, please cite:

Manuscript:
Soto-Perez, M. (2026). A transparent PLSsemEngine for composite-based Mode A estimation of reflective models in R. SoftwareX. (Under review) .

Software Archive:
Soto-Perez, M. (2026). PLSsemEngine (Version 1.3.0). Zenodo. https://doi.org/10.5281/zenodo.20703909

✉️ Contact
Dr. M. Soto-Perez Email: msoto@up.edu.mx 

Universidad Panamericana, Mexico.

