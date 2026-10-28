# ICD-341-LABS-9-13
# ICD 341: Advanced Computational Methods — Lab Solutions (Labs 9–13)

**Institution:** Mulungushi University  
**School:** Natural and Applied Sciences  
**Department:** Mathematics and Statistics  
**Course Code:** ICD 341  


---

## 📌 Overview

This repository contains comprehensive Python implementations, test suites, and theoretical explanations for **ICD 341 Labs 9 through 13** (Lab 1 through Lab 5 in the assignment series). 

The laboratory series covers key computational and statistical concepts:
1. **Non-parametric and Parametric Bootstrapping** (Resampling & Validation)
2. **Bayesian Inference & MCMC** (Metropolis-Hastings, Beta-Binomial conjugacy, PyMC)
3. **Advanced Simulation Techniques** (Inverse Transform, Rejection Sampling, Particle Filtering, SBC)
4. **Software Engineering for Data Science** (Unit testing, custom Estimators/Transformers, `pyproject.toml`)
5. **High-Performance Computing & Scalability** (Vectorization, Numba JIT, Joblib parallelization, Dask arrays)

---

## 🗂️ Table of Contents

* [Lab Topics Breakdown](#-lab-topics-breakdown)
  * [Lab 1: Bootstrap & Resampling](#lab-1-bootstrap--resampling)
  * [Lab 2: Bayesian MCMC](#lab-2-bayesian-mcmc)
  * [Lab 3: Advanced Simulation](#lab-3-advanced-simulation)
  * [Lab 4: Testing, Estimators, Packaging](#lab-4-testing-estimators-packaging)
  * [Lab 5: Performance and Scalability](#lab-5-performance-and-scalability)
* [Installation & Setup](#-installation--setup)
* [Running Tests](#-running-tests)
* [Usage Examples](#-usage-examples)

---

## 🧪 Lab Topics Breakdown

### Lab 1: Bootstrap & Resampling
- **Percentile Bootstrap Interval (Mean & Median):** Non-parametric resampling of sample dataset `[3, 4, 5, 7, 8, 9]` over $10,000$ iterations to build $95\%$ confidence intervals.
- **Parametric Bootstrap:** Fitting $\mathcal{N}(\mu, \sigma^2)$ to observed data and sampling synthetic datasets from the estimated parametric model.
- **Data Leakage in Validation:** Analysis of improper feature scaling prior to cross-validation split and how standardizing full datasets inflates validation metrics.

### Lab 2: Bayesian MCMC
- **Random-Walk Metropolis-Hastings (MH):** Manual implementation of a random-walk MH sampler targeted at a standard normal distribution $\mathcal{N}(0, 1)$.
- **Conjugate Beta-Binomial Updating:** Analytical calculation of posterior parameter values $\text{Beta}(\alpha+s, \beta+f) = \text{Beta}(10, 6)$ given a $\text{Beta}(2, 2)$ prior and observing $8$ successes in $12$ trials.
- **Diagnostics:** Conceptual summary of Trace Plots, Autocorrelation Functions (ACF), Gelman-Rubin Diagnostic ($\hat{R}$), and Effective Sample Size (ESS).
- **PyMC Probabilistic Programming:** Implementation of a simple normal likelihood model using PyMC.

### Lab 3: Advanced Simulation
- **Inverse Transform Method:** Sampling from $x = -\frac{\ln(U)}{\lambda}$ to draw $5,000$ exponential samples ($\lambda = 3$).
- **Categorical Sampling:** Inverse CDF lookup and discrete probability sampling for categorical distribution $P(X) = [0.1, 0.6, 0.3]$.
- **Rejection Sampling:** Rejection algorithm generating random draws from a $\text{Beta}(2,2)$ density using a Uniform proposal envelope.
- **Particle Filtering:** Summary of Prediction, Weight Update, Normalization, and Resampling steps in Sequential Monte Carlo (SMC).
- **Simulation-Based Calibration (SBC):** Diagnosing model miscalibration, underdispersion/overdispersion, and parameter bias using SBC rank histograms.

### Lab 4: Testing, Estimators, Packaging
- **Unit Testing with `pytest`:** Edge-case validation for mathematical functions (handling empty inputs and standard cases).
- **Estimator Boundary Constraints:** Unit assertions verifying predictions stay strictly within $[0, 1]$.
- **Custom Scikit-Learn Transformer:** Building a `ColumnStdScaler` class inheriting from `BaseEstimator` and `TransformerMixin`.
- **Packaging:** Configuring a standard `pyproject.toml` file and demonstrating editable package installation (`pip install -e .`).

### Lab 5: Performance and Scalability
- **Vectorization:** Accelerating vectorized computations $x^2 + 2x + 1$ over $1,000,000$ elements using NumPy.
- **Numba Just-In-Time (JIT):** `@jit(nopython=True)` compilation for fast array summation.
- **Parallel Computing:** Multi-core parallel bootstrapping using `joblib.Parallel`.
- **Out-of-Core Processing with Dask:** Chunked lazy evaluation of large datasets via `dask.array`.
- **Benchmarking Best Practices:** Explanation of JIT overhead warm-ups and why first-call compilation must be omitted from runtime benchmarks.

---

## 🛠️ Installation & Setup

### Prerequisites
* Python 3.9+
* `pip` or `conda`

### Environment Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-username/icd341-labs.git
   cd icd341-labs
   ```

2. **Create and activate a virtual environment:**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies in editable mode:**
   ```bash
   pip install -e .
   ```

---

## ⚡ Running Tests

To run the unit tests built during Lab 4:

```bash
pytest tests/
```

---

## 💻 Usage Examples

### Running Bootstrap Analysis (Lab 1)
```python
import numpy as np
from icd341.bootstrap import percentile_ci

data = np.array([3, 4, 5, 7, 8, 9])
lower, upper = percentile_ci(data, stat_func=np.mean, n_bootstraps=10000)
print(f"95% CI for Mean: [{lower:.2f}, {upper:.2f}]")
```

### Fitting PyMC Normal Model (Lab 2)
```python
import pymc as pm
import numpy as np

data = np.random.normal(loc=5.0, scale=2.0, size=100)

with pm.Model() as model:
    mu = pm.Normal("mu", mu=0, sigma=10)
    sigma = pm.HalfNormal("sigma", sigma=5)
    y = pm.Normal("y", mu=mu, sigma=sigma, observed=data)
    trace = pm.sample(draws=1000, tune=1000)
```

---

## 📄 License

This project is submitted in partial fulfillment of the coursework requirements for ICD 341 at Mulungushi University.
