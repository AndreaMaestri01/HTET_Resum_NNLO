# Numerical database for HTET with NNLO corrections

This repository contains the numerical data used in the analysis of Hamiltonian Truncation Effective Theory (HTET) for the two–dimensional $\lambda\phi^4$ theory on a circle, including local, resummed, and non–local corrections up to next–to–next–to–local order (NNLO).

The data correspond to the results discussed in Sections II–V of the accompanying paper:

- Andrea Maestri, Simone Rodini, Barbara Pasquini, **Higher-Order Structure of Hamiltonian Truncation Effective Theory** (2026).

---

## 1. Directory structure

The database is organized as
```text
Data/
 ├── config1/
 ├── config2/
 │    ⋮
 └── config9/
database.yaml
```

Each `configX/` directory corresponds to a specific choice of physical parameters $(\lambda, m, R)$, defined in `database.yaml`. 

---

## 2. Physical parameters (`database.yaml`)

The file `database.yaml` defines the mapping between configuration labels and physical parameters:
- `Lambda_frac_4pi`: the dimensionless coupling $\lambda / (4\pi)$,
- `M`: the mass parameter $m$,
- `2piR`: the spatial circumference $L = 2\pi R$.

Example:
```yaml
config1:
  Lambda_frac_4pi: 5.0
  M: 1.0
  2piR: 10.0
```

All results within `Data/config1/` are obtained for this specific choice of parameters.

---

## 3. File naming convention

Inside each `configX/` directory, files follow the naming scheme
```text
Eigen_Emax<N>_<TYPE>.txt
```

### 3.1 Truncation scale

- `Emax<N>` denotes the truncation scale $E_{\max} = N$ applied to the free Hamiltonian spectrum.

Each value of `N` corresponds to an independent diagonalization of the truncated Hamiltonian.

---

### 3.2 Approximation type (`TYPE`)

The suffix `<TYPE>` specifies the truncation/improvement scheme used:

| Suffix        | Meaning |
|---------------|---------|
| `Raw`         | Bare Hamiltonian truncation $H_{\text{raw}} = PHP$, no HTET corrections |
| `Imp`         | Leading local HTET corrections (LO), i.e. $O(E_{\max}^{-2})$ |
| `Imp_Cont`    | Same as `Imp`, but matching coefficients evaluated in infinite volume |
| `NLO`         | HTET including next-to-local corrections $O(E_{\max}^{-3})$ |
| `NLO_Cont`    | NLO with infinite-volume matching coefficients |
| `NNLO_Cont`   | HTET including NNLO non-local corrections $O(E_{\max}^{-4})$ |
| `Resum`       | Resummed local corrections to mass and coupling |

---

## 4. File content

Each `Eigen_Emax<N>_<TYPE>.txt` file contains the low-energy spectrum obtained by diagonalizing the (truncated/effective) Hamiltonian $H$ at fixed $E_{\max}$.

Specifically, each `.txt` file stores the **ordered list of eigenvalues**:
$$
E_0,\; E_1,\; E_2,\; \dots
$$
with $E_0$ the ground-state energy and $E_n$ the $n$-th excited level.

These eigenvalues can be used to construct gaps such as
$$
\Delta E_1(E_{\max}) = E_1(E_{\max}) - E_0(E_{\max}),
$$
and, more generally, $\Delta E_n = E_n - E_0$.

No further post-processing is applied to the data stored in these files.

---

## 5. Typical usage

A typical analysis workflow is:
1. Select a configuration `configX` corresponding to fixed $(\lambda, m, R)$.
2. For a given approximation scheme (`Raw`, `Imp/LO`, `NLO`, `NNLO`, `Resum`), load the files at different `Emax`.
3. Study the convergence of spectral quantities as a function of $E_{\max}$.
4. Compare different HTET prescriptions at fixed parameters.

---

## 6. Relation to the paper

- Local and resummed corrections: Sec. III.
- NLO and NNLO non-local operator insertions: Sec. IV (operator classification and scaling in $1/E_{\max}$).
- Numerical convergence studies: Sec. V.
