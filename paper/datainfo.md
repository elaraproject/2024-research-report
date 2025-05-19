---
title: "Data and source code"
---

All data and source code associated with this research are dedicated to the public domain and are completely free and open-source. Source files for the simulations can be found within Project Elara's [`elara-labs`](https://github.com/elaraproject/elara-labs) repository:

- FreeFEM finite-element simulation files used for the final report can be found within `freefem/release/report-1`
- `findiff` finite-difference simulation files used for the final report can be found in `notebooks/archived/helmholz-fdm-updated-8-31-2024.ipynb`

To be able to run the simulations locally, first clone the repository:

```bash
git clone https://github.com/elaraproject/elara-labs
cd elara-labs
```

Then, install FreeFEM according to their [official installation instructions](https://doc.freefem.org/introduction/installation.html), and ensure you have a fairly recent Python installation (Python 3.10+). Then, simply run:

```bash
pip install notebook matplotlib numpy findiff scipy scikit-learn
```

For running the finite-element simulations, **from the root of the repository**, `cd` into the finite-element scripts directory and run with FreeFEM via the commandline:

```bash
cd freefem/release/report-1
FreeFem++ solve-Efield.edp # for the primary simulation
FreeFem++ solve-Efield-validation.edp # for the validation simulation
```

For the finite-difference simulations, **from the root of the repository**, `cd` into the notebook directory and start Jupyter notebook for interactive programming with the given notebook:

```bash
cd notebooks/archived
jupyter notebook
```
