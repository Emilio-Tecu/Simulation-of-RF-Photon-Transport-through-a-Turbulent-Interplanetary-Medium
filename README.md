# Simulation of RF Photon Transport through a Turbulent Interplanetary Medium

This repository contains a stochastic simulator developed in Python to model the transport of radio signals (narrowband technosignatures at 1 GHz) through the Exoplanetary Interplanetary Medium (Exo-IPM).

The main objective of the code is to statistically quantify the spectral broadening (\Delta\nu_{sb}) induced by stellar plasma turbulence, comparing the impact on Sun-like systems versus M-dwarf stellar systems.

---

## Code Features

This section of the project (Monte Carlo Exo-IPM simulation) is developed using exclusively standard Python scientific libraries, which guarantees:
*   Maximum Portability: It does not require external compilers or complex optimization dependencies (such as Numba).
*   Readable Code: Clean logic based on NumPy vector operations and direct visualization via Matplotlib.
*   Statistical Fitting: Modeling and extraction of the net broadening through parametric fitting to Cauchy distributions using SciPy.

---

## Simulator Architecture (MPI)

The main script simulates the phenomenon through three consecutive phases:

1.  Astrophysical Environment: Generation of a controlled stellar census (75% M-dwarf stars and 25% Sun-like stars). 3D orbital elements are randomly sampled to geometrically project the impact parameter on the plane of the sky.
2.  Microscopic Monte Carlo Propagation: Trajectory simulation of photon packets per system. Each individual collision against plasma irregularities generates a micro-Doppler shift based on a Kolmogorov isotropic turbulence regime (Rayleigh sampling).
3.  Poblational Analysis: Processing of the final frequencies and calculation of the Survival Function S(>\Delta\nu_{sb}) to determine what percentage of the population exceeds the standard detection limits of SETI projects.

---

## Requirements and Installation

To run this simulator, you only need Python 3.8+ and the following basic packages:

```bash
pip install numpy scipy matplotlib tqdm
