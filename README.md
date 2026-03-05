# SED Fitting for Galaxies using BAGPIPES

This repository contains work carried out as part of an **Astrophysics laboratory assignment at the Indian Institute of Space Science and Technology (IIST)**.

The objective of this project is to perform **Spectral Energy Distribution (SED) fitting** for galaxies using **multi-band photometric observations** and the **BAGPIPES (Bayesian Analysis of Galaxies for Physical Inference and Parameter EStimation)** Python package.

The analysis explores how galaxy physical properties such as **stellar mass, star formation history, and redshift** can be inferred from broadband photometric data.

---

# Scientific Background

A galaxy emits radiation across a wide range of wavelengths. The **Spectral Energy Distribution (SED)** describes how the flux emitted by a galaxy varies with wavelength.

$$
F_\lambda(\lambda)
$$

where

* $F_\lambda$ is the flux density
* $\lambda$ is the wavelength

However, observations rarely measure the full spectrum. Instead, flux is measured through **photometric filters**, each covering a specific wavelength range.

The measured flux in a photometric band is therefore

$$
F_{\text{band}} =
\frac{\int F_\lambda(\lambda),T(\lambda),d\lambda}
{\int T(\lambda),d\lambda}
$$

where

* $T(\lambda)$ is the **filter transmission function**
* $F_\lambda(\lambda)$ is the **intrinsic galaxy spectrum**

SED fitting attempts to determine the **physical parameters of a galaxy** by comparing observed photometric fluxes with synthetic galaxy spectra generated from stellar population models.

---

# BAGPIPES

This project uses the **BAGPIPES** package.

Carnall et al. (2018)
**BAGPIPES: Bayesian Analysis of Galaxies for Physical Inference and Parameter EStimation**

BAGPIPES performs **Bayesian inference** to determine galaxy parameters by sampling the posterior probability distribution.

$$
P(\theta \mid D) \propto P(D \mid \theta)P(\theta)
$$

where

* $D$ represents the observed photometric data
* $\theta$ represents the model parameters
* $P(D|\theta)$ is the likelihood
* $P(\theta)$ is the prior

The Bayesian evidence of a model is

$$
Z = \int P(D|\theta),P(\theta),d\theta
$$

and the logarithm of this quantity

$$
\ln Z
$$

is commonly used for **model comparison**.

---

# Dataset

The repository contains two photometric catalogs.

## 5-band Photometry

`5_band.txt`

This catalog contains galaxy flux measurements in **five photometric bands**.

These bands correspond to the **Sloan Digital Sky Survey (SDSS)** filters:

* u
* g
* r
* i
* z

Each row contains:

```
Galaxy_ID   flux_1   error_1   flux_2   error_2   ...   flux_5   error_5
```

---

## 21-band Photometry

`21_band.txt`

This catalog contains flux measurements across **21 photometric filters** spanning ultraviolet to far-infrared wavelengths.

The filters correspond to instruments from multiple astronomical surveys.

| Survey   | Filters        |
| -------- | -------------- |
| GALEX    | FUV, NUV       |
| SDSS     | u, g, r, i, z  |
| VISTA    | Z, Y, J, H, Ks |
| WISE     | W1, W2, W3, W4 |
| Herschel | PACS, SPIRE    |

Using a larger number of bands provides **better sampling of the SED**, allowing tighter constraints on galaxy parameters.

---

# Filter Transmission Curves

The `filters/` directory contains the **transmission curves of the photometric filters**.

Each `.dat` file contains two columns:

```
wavelength   transmission
```

These curves describe the fraction of incoming light transmitted by the filter as a function of wavelength.

During SED fitting, BAGPIPES computes the predicted flux in a photometric band by integrating the model spectrum over the filter transmission curve.

---

# Filter Lists

Two filter list files define which filters correspond to each dataset.

### 5-band filter list

`filter_list_5_band.txt`

Contains the SDSS filters used for the 5-band catalog.

### 21-band filter list

`filter_list_21_band.txt`

Contains the full set of filters spanning UV to far-infrared wavelengths.

---

# Repository Structure

```
SED-fitting-for-galaxies
│
├── data
│   ├── 5_band.txt
│   └── 21_band.txt
│
├── filters
│   ├── GALEX_GALEX.FUV.dat
│   ├── SLOAN_SDSS.g.dat
│   ├── Paranal_VISTA.J.dat
│   └── WISE_WISE.W1.dat
│
├── filter_lists
│   ├── filter_list_5_band.txt
│   └── filter_list_21_band.txt
│
├── notebooks
│   ├── 01_photometry_loader.ipynb
│   ├── 02_sed_fitting_5band.ipynb
│   └── 03_sed_fitting_21band_lnZ_analysis.ipynb
│
├── Assignment_3_Galaxies.pdf
├── SED_FITTING.pdf
└── README.md
```

---

# Analysis Workflow

The workflow used in this project is:

1. Load galaxy photometric data.
2. Define the filter transmission curves.
3. Construct a BAGPIPES galaxy object.
4. Define a star formation history model.
5. Perform Bayesian SED fitting.
6. Estimate galaxy physical parameters.

Key parameters explored include

* Stellar mass $M_\ast$
* Star formation duration $\tau$
* Redshift $z$
* Star formation rate (SFR)

---

# Star Formation History Model

The star formation history (SFH) is modeled using an **exponentially declining model**.

$$
\text{SFR}(t) \propto e^{-t/\tau}
$$

where

* $\tau$ is the **star formation timescale**
* $t$ is the **age of the stellar population**

This model is commonly referred to as a **$\tau$-model**.

---

# Key Outputs

The SED fitting procedure estimates several physical properties of galaxies:

* Stellar mass
* Star formation rate
* Galaxy age
* Dust attenuation
* Metallicity

These parameters are inferred from the **posterior distributions generated by BAGPIPES**.

---

# Comparison of 5-band and 21-band Fitting

The analysis compares SED fits obtained using:

* **Limited photometric coverage (5 bands)**
* **Extended photometric coverage (21 bands)**

Increasing the number of photometric bands improves constraints on galaxy parameters because the SED is sampled over a wider wavelength range.

---

# Requirements

Python packages required:

```
numpy
matplotlib
bagpipes
astropy
```

Install BAGPIPES using

```
pip install bagpipes
```

---

# References

Carnall et al. (2018)
*Inferring the star formation histories of massive galaxies with BAGPIPES*

BAGPIPES Documentation:
https://bagpipes.readthedocs.io
