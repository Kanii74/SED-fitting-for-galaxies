# Spectral Energy Distribution (SED) Fitting of Galaxies using BAGPIPES

This repository contains the work carried out for **Assignment 3: Modelling Galaxy Spectra** as part of the **Galaxies course at the Indian Institute of Space Science and Technology (IIST)**.

The goal of this project was to **model the spectral energy distributions (SEDs) of galaxies from the GAMA survey** using photometric observations across multiple wavelength bands. The analysis was performed using the **BAGPIPES (Bayesian Analysis of Galaxies for Physical Inference and Parameter EStimation)** Python package.

---

# Scientific Background

Galaxies emit radiation across a wide range of wavelengths, from the ultraviolet to the far infrared.

The **Spectral Energy Distribution (SED)** represents the flux of a galaxy as a function of wavelength and provides insight into its physical properties such as:

* Star Formation Rate (SFR)
* Stellar Mass
* Redshift
* Age of the Stellar Population
* Star Formation History

By fitting theoretical models to observed photometric data, we can infer these properties and understand the evolutionary state of galaxies.

The galaxies analyzed in this assignment come from the **GAMA (Galaxy And Mass Assembly) survey**, which is a large spectroscopic and imaging survey of approximately **300,000 galaxies covering 290 square degrees of the sky**.

---

# Dataset Description

Two ASCII files containing photometric measurements were provided.

## 1. 21-band Photometric Dataset

File: `21_band.txt`

This file contains photometric observations for **two galaxies measured across 21 wavelength bands** from multiple astronomical surveys.

### Photometric Bands

**GALEX**

* FUV
* NUV

**SDSS**

* u
* g
* r
* i
* z

**VIKING**

* Z
* Y
* J
* H
* Ks

**WISE**

* W1
* W2
* W3
* W4

**Herschel PACS**

* 100 μm
* 160 μm

**Herschel SPIRE**

* 250 μm
* 350 μm
* 500 μm

The dataset contains **43 columns**, including:

* Galaxy identifier (**CATAID**)
* Flux measurements in each photometric band
* Associated flux uncertainties

All flux values are given in **Janskys (Jy)**.

---

## 2. 5-band Photometric Dataset

File: `5_band.txt`

This file contains photometric measurements for **two galaxies observed in the five SDSS photometric bands**:

* u
* g
* r
* i
* z

The dataset contains **11 columns**, including:

* Galaxy identifier (**CATAID**)
* Flux measurements
* Flux uncertainties

All flux values are given in **Janskys (Jy)**.

---

# Methodology

The following steps were performed to model the galaxy spectra.

## 1. Data Preparation

Photometric flux values and their uncertainties were extracted from the ASCII files and used as inputs for the BAGPIPES fitting routines.

Filter response curves for each photometric band were obtained from the **SVO Filter Profile Service**, which are required to accurately model photometric observations.

---

## 2. Installation of BAGPIPES

The **BAGPIPES** package was installed in a Python environment compatible with **Python 3.10.9**.

BAGPIPES enables:

* Generation of synthetic galaxy spectra
* Fitting models to photometric data
* Estimation of galaxy properties using Bayesian inference

---

## 3. Model Definition

A galaxy model was defined within BAGPIPES including parameters such as:

* Star Formation History
* Stellar Mass
* Redshift
* Age of Stellar Population
* Dust Attenuation
* Nebular Emission (when required)

These parameters define the **synthetic spectral energy distribution (SED)** which is compared with observed photometric data.

---

## 4. Model Fitting

BAGPIPES generates a **synthetic SED** and compares it with observed photometric flux values.

Using **Bayesian sampling**, the code produces **posterior probability distributions** for each model parameter.

The fitting procedure produces:

* Best-fit SED spectra
* Star formation history plots
* Estimates of galaxy properties

---

# Results

SED fitting was performed for **four galaxies**.

* Two galaxies were analyzed using **5-band SDSS photometry**
* Two galaxies were analyzed using **21-band multi-wavelength photometry**

---

# 5-Band SED Fitting

## Galaxy 130653

| Parameter           | Value        |
| ------------------- | ------------ |
| Star Formation Rate | 17.5 M☉ yr⁻¹ |
| Stellar Mass        | 10¹⁴ M☉      |
| Redshift            | 0.0035       |
| Age                 | 9.42 Gyr     |

The absence of strong emission lines suggests that this galaxy is dominated by older stellar populations.
This indicates that the galaxy is most likely an **elliptical galaxy**.

---

## Galaxy 220955

| Parameter           | Value         |
| ------------------- | ------------- |
| Star Formation Rate | 705.2 M☉ yr⁻¹ |
| Stellar Mass        | 10¹³ M☉       |
| Redshift            | 0.0015        |
| Age                 | 7.84 Gyr      |

The presence of strong emission lines suggests active star formation.
This indicates that the galaxy is most likely a **spiral galaxy**.

---

# 21-Band SED Fitting

## Galaxy 382567

This galaxy was analyzed using the **21-band photometric dataset**, which spans wavelengths from the ultraviolet to the far infrared.

The SED fit provides a detailed view of the spectral properties of the galaxy across the electromagnetic spectrum. However, the absence of clear spectral features makes morphological classification uncertain.

---

## Galaxy 229206

| Parameter           | Value       |
| ------------------- | ----------- |
| Star Formation Rate | 2.8 M☉ yr⁻¹ |
| Stellar Mass        | 10¹¹ M☉     |
| Redshift            | 0.155       |
| Age                 | 7.85 Gyr    |

The presence of emission features suggests **ongoing star formation**, indicating that the galaxy is likely a **spiral galaxy**.

---

# Comparison: 5-Band vs 21-Band Photometry

The analysis shows that **21-band photometry provides more accurate constraints** on galaxy parameters compared to 5-band photometry.

### Reasons

**1. Increased Data Points**

More photometric bands provide stronger constraints on the SED model and reduce parameter degeneracies.

**2. Broader Wavelength Coverage**

21-band photometry spans wavelengths from **ultraviolet to far infrared**, capturing spectral features not available in the limited SDSS bands.

**3. Improved Parameter Estimation**

The wider spectral coverage enables more reliable estimation of:

* Redshift
* Dust extinction
* Star formation history

---

# Repository Structure

```
SED-fitting-for-galaxies
│
├── 21_band.txt
├── 5_band.txt
├── Assignment 3 Galaxies (1).pdf
├── SED_FITTING.pdf
└── README.md
```

---

# Tools and Libraries

The analysis was performed using:

* Python
* BAGPIPES
* NumPy
* Matplotlib
* Astropy

---

# References

Carnall, A. C., et al. (2018)
**BAGPIPES: Bayesian Analysis of Galaxies for Physical Inference and Parameter Estimation**

Driver, S. P., et al. (2009)
**Galaxy And Mass Assembly (GAMA) Survey**

---

# Acknowledgements

This assignment was completed as part of the **Galaxies course at the Indian Institute of Space Science and Technology (IIST)**.

I would like to thank **Dr. Anand Narayana** for designing this assignment and providing valuable insight into **SED fitting and galaxy spectral modelling**.
