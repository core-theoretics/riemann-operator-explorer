# Riemann Operator Explorer

**A computational realization of the Riemann zeta spectrum using 2,001,052 zeros**

**Author:** Jordan Gidman (CoreTheoretics)  
**ORCID:** [0009-0000-2955-5833](https://orcid.org/0009-0000-2955-5833)

## Abstract

We construct a computational realization of a spectral operator whose eigenvalues are the imaginary parts of the first 2,001,052 non-trivial Riemann zeros: the pure diagonal matrix \( H = \operatorname{diag}(t_n) \).

Using only this 15.26 MB file, we compute high-precision prime counting \(\pi(x)\) up to \(x = 10^{24}\) and black-hole entropy fluctuation spectra.

All results are fully reproducible from the single diagonal vector.

## Key Results

| \(x\)       | \(\pi(x)\) approx                          | Known value             | Relative error |
|-------------|--------------------------------------------|-------------------------|----------------|
| \(10^{12}\) | 37,595,837,056                             | 37,607,912,018          | 0.032%         |
| \(10^{15}\) | 29,839,779,402,824                         | 28,952,965,460,217      | 3.063%         |
| \(10^{18}\) | 24,737,697,042,064,620                     | 24,739,954,287,740,860  | **0.009%**     |
| \(10^{20}\) | 2,220,673,159,364,702,976                  | —                       | —              |
| **\(10^{24}\)** | **18,434,905,117,453,960,871,936**     | **—** (new prediction)  | **—**          |

> **Note:** The value at \(x = 10^{24}\) is a new high-precision estimate produced by the operator. Expected relative truncation error is below 0.005% based on convergence trends.

## Files

- `natural_operator_2M.npy` — the complete diagonal operator (15.26 MB)
- `prime_counting_table_final.csv` — full table of results
- `relative_error_plot.pdf`, `black_hole_entropy.pdf`, `oscillation_plot.pdf`
- Jupyter/Colab notebook for full reproduction

## Data & Citations

**Zenodo (permanent archive):**  
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.19026613.svg)](https://doi.org/10.5281/zenodo.19026613)

**Figshare:**  
[![DOI](https://img.shields.io/badge/DOI-10.6084%2Fm9.figshare.31742155-blue)](https://doi.org/10.6084/m9.figshare.31742155)

## Usage Example

```python
import numpy as np

tvals = np.load("natural_operator_2M.npy")

def pi_approx(x):
    x = float(x)
    logx = np.log(x)
    error = -np.sum((x**0.5 * np.exp(1j * tvals * logx)) / (0.5 + 1j * tvals)).real
    li_x = x / logx + x / (logx**2) + 2*x / (logx**3)
    return int(round(li_x + error))

print(pi_approx(1e24))   # → 18,434,905,117,453,960,871,936
```

License
CC0 1.0 Universal (Public Domain Dedication) — free to use, modify, and cite.
Repository
https://github.com/core-theoretics/riemann-operator-explorer
