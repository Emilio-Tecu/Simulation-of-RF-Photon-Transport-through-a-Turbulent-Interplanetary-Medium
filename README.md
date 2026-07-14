# RF Photon Transport Simulation and CNN-Based Technosignature Detection

We simulate the degradation of narrowband SETI signals through turbulent stellar plasma (Exo-IPM) using Monte Carlo methods. This Lorentzian broadening evades classical detectors. To solve this, we developed a 1D CNN that identifies these dispersed technosignatures with >97% accuracy under severe thermal noise.

---

## Code Features

This repository is divided into two intrinsically connected components:

1.  **Monte Carlo Exo-IPM Simulation**: Developed using exclusively standard Python scientific libraries for maximum portability. It features clean logic based on NumPy vector operations and statistical modeling of the net broadening through parametric fitting to Cauchy distributions using SciPy.
2.  **Deep Learning Classification**: Implementation of a 1D Convolutional Neural Network (CNN) using TensorFlow/Keras. Designed as a non-linear adaptive matched filter, it bypasses classical mathematical threshold failures to detect signals hidden in extreme thermal noise.

---

## Phase 1: Simulator Architecture (Physics & Monte Carlo)

The first script simulates the physical phenomenon through three consecutive phases:

1.  **Astrophysical Environment**: Generation of a controlled stellar census (75% M-dwarf stars and 25% Sun-like stars). 3D orbital elements are randomly sampled to geometrically project the impact parameter on the plane of the sky.
2.  **Microscopic Monte Carlo Propagation**: Trajectory simulation of photon packets per system. Each individual collision against plasma irregularities generates a micro-Doppler shift based on a Kolmogorov isotropic turbulence regime (Rayleigh sampling).
3.  **Poblational Analysis**: Processing of the final frequencies and calculation of the Survival Function to determine what percentage of the population exceeds the standard detection limits of classical SETI projects.

---

## Phase 2: Deep Learning Architecture (1D CNN)

To overcome the detection limitations exposed in Phase 1, the repository includes a Machine Learning pipeline:

1.  **Physics-Informed Synthetic Dataset**: We generate massive datasets (e.g., 50,000 to 100,000 spectra) by mapping the empirically derived Lorentzian broadening to theoretical Cauchy distributions and injecting dynamic Gaussian thermal noise (SNR from 0.5 to 5.0).
2.  **Morphological Feature Extraction**: The network utilizes sequential `Conv1D` and `MaxPooling1D` blocks. These filters are translation-invariant and learn to ignore high-frequency thermal noise, resonating exclusively with the smooth slopes and heavy tails of the dispersed signal.
3.  **Robust Regularization**: To prevent overfitting on static noise anomalies, the model implements L2 Regularization (Weight Decay), aggressive `Dropout(0.5)`, and Early Stopping mechanisms.
4.  **Binary Classification**: A flattened Dense layer ending in a Sigmoid activation outputs the final probability, classifying the spectrum as either pure spatial noise or a genuine, Exo-IPM broadened technosignature.

---

## Requirements and Installation

To run both the physical simulator and the neural network pipeline, you need Python 3.8+ and the following packages:

```bash
pip install numpy scipy matplotlib tqdm pandas scikit-learn tensorflow seaborn