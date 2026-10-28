# ICD 341 Labs 9-13

**Mulungushi University**
School of Natural and Applied Sciences
Department of Mathematics and Statistics

**Due:** 30th October 2026, 23:59

## Overview

This repository contains solutions to ICD 341 Labs 9-13, a practical series in computational statistics using Python. The labs cover resampling, Bayesian inference, simulation, software engineering practice, and performance tuning.

## Contents

| Lab | Topic | Main techniques |
|---|---|---|
| 1 | Bootstrap and resampling | Nonparametric and parametric bootstrap, percentile intervals, data leakage |
| 2 | Bayesian MCMC | Random-walk Metropolis-Hastings, Beta-Bernoulli model, trace plots, ACF, R-hat, ESS, PyMC |
| 3 | Advanced simulation | Inverse transform, categorical sampling, rejection sampling, particle filter, SBC |
| 4 | Testing, estimators, packaging | Unit tests, scikit-learn transformer, `pyproject.toml`, editable install |
| 5 | Performance and scalability | NumPy vectorisation, Numba, joblib, Dask |

## Requirements

- Python 3.9 or later
- numpy, scipy, matplotlib
- scikit-learn
- joblib
- numba
- dask[array]
- pymc and arviz
- pytest

Install everything with:

```bash
pip install numpy scipy matplotlib scikit-learn joblib numba "dask[array]" pymc arviz pytest
```

A virtual environment is recommended:

```bash
python -m venv .venv
source .venv/bin/activate      # Windows: .venv\Scripts\activate
```

## Running the labs

1. Open the lab file or notebook in Jupyter, VS Code, or Google Colab.
2. Run the cells in order. Each lab sets its own random seed (341) so results are reproducible.
3. For the tests in Lab 4, run `pytest` from the project root.

## Summary of results

- **Bootstrap mean** of [3, 4, 5, 7, 8, 9]: 6.0, with a 95% percentile interval of about (4.33, 7.67).
- **Beta posterior** for 8 successes in 12 trials with a Beta(2,2) prior: Beta(10, 6), mean 0.625. MCMC agrees (about 0.623).
- **Convergence:** R-hat of about 1.0005 across four chains.
- **Rejection sampling** for Beta(2,2): acceptance rate about 0.667 (1/1.5).
- **Vectorisation:** about 28 times faster than a Python loop for one million values.

## Notes

- The Numba, Dask, and PyMC sections need those libraries installed.
- Numba's first call includes compilation time. Benchmarks should use a warm-up call and time later calls only.
- The joblib bootstrap uses `SeedSequence.spawn` so that each worker has an independent random stream.
- On small jobs, parallel code can be slower than serial code because of start-up overhead.

## Suggested project layout

```
mypkg/
├── pyproject.toml
├── README.md
├── src/
│   └── mypkg/
│       ├── __init__.py
│       └── stats.py
└── tests/
    └── test_stats.py
```

## Author

Name: _your name_
Student number: _your student number_
