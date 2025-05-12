# AE370 Group Project 2 – Diffusion–Reaction Simulation

A self-contained Jupyter notebook that models the 1-D vertical dispersion and decay of two atmospheric pollutants (HCFC-22 and HFC-152a) using the method of lines and an implicit trapezoidal time integrator.

---

## 1. Repository / File Structure

| File                               | Purpose                                                                                                       |
|------------------------------------|---------------------------------------------------------------------------------------------------------------|
| `project2_simulation.ipynb`        | Main notebook with nine executable cells (plus explanatory markdown) implementing the solver, visualisation, grid-refinement study, reach metric, figure export, and analytic validation. |
| `figure_HCFC22_dispersion.png`     | Auto-saved semi-log plot of HCFC-22 vertical profiles (import into LaTeX).                                    |
| `figure_HFC152a_dispersion.png`    | Same for HFC-152a.                                                                                             |
| `README.md`                        | *This* document.                                                                                               |

> **Tip** – If you are only submitting the notebook to Gradescope, the PNGs are saved automatically when you run Cell 8; place them in your LaTeX directory for the final report.

---

## 2. Prerequisites

* Python ≥ 3.9  
* `numpy`  
* `matplotlib` (for interactive and file plots)

All dependencies are part of Anaconda or can be installed with `pip install numpy matplotlib`.

---

## 3. Quick Start

1. **Clone / download** the repo or copy the notebook into your working directory.  
2. Launch JupyterLab or Jupyter Notebook.  
3. Open `project2_simulation.ipynb` and **run cells sequentially** (Ctrl + Enter or the “Run All” button).  
   * The first five cells reproduce the baseline results used in the paper.  
   * Cells 6-9 add reach analysis, Δx-convergence, figure export, and analytic validation.  
4. Two PNG figures are written to disk; check the notebook output for the exact filenames.

> **Runtime:** default grid `n = 200` and `t_final = 3 × 10⁶ s` finish in under 30 s on a standard laptop. Finer grids increase runtime roughly linearly with `n`.

---

## 4. Customising the Simulation

| Parameter            | Location | Description                                                         |
|----------------------|----------|---------------------------------------------------------------------|
| `n`                  | Cell 1 (and Cell 7 for grid sweep) | Number of spatial intervals (higher ⇒ finer grid). |
| `dt`, `t_final`      | Cell 3   | Time-step and final time for baseline runs.                         |
| `species` dict       | Cell 3   | Diffusivity `D` and decay constant `k` for each pollutant; add more by extending the dict. |
| `reach_threshold`    | Cell 6   | Concentration threshold (molecules / cm³) used to compute maximum height reach. |

All other constants (domain length, initial Gaussian pulse, boundary values) are defined at the top of Cell 1 for easy editing.

---

## 5. Validation & Quality Checks

* **Analytic Gaussian test (Cell 9)** – Sets `k = 0` and compares numerical and closed-form solutions; prints relative L² error.  
* **Grid-refinement study (Cell 7)** – Runs Δx = L / {50, 100, 200, 400} and reports L² error vs. finest grid.

These provide confidence that the spatial and temporal discretisations are implemented correctly.

---

## 6. Known limitations

* The notebook rewrites global variables (`n`, `x`, `dx`) inside the grid-refinement sweep; run baseline cells *after* Cell 7 if you intend to reuse the original grid.  
* No high-performance sparse solver used – for `n > 1000` consider `scipy.sparse.linalg.spsolve`.

---

## 7. Authors / Credits

*Adam Lutz, DongDong Wang, Pratham Puskur, Rushil Malik, Spyros Kalleas*  
AE370 – Spring 2025  
University of Illinois at Urbana-Champaign

Feel free to adapt or extend this notebook for related diffusion–reaction studies. If you do, please retain attribution.
