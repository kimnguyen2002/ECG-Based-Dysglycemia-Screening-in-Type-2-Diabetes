# ECG-Based Dysglycemia Screening in Type 2 Diabetes
## A Multi-Modal Machine-Learning Framework using MIMIC-III Waveform Data

This repository contains a comprehensive analytical pipeline for screening dysglycemia (hypo- and hyperglycemia) in Type 2 Diabetes Mellitus (T2DM) patients using non-invasive electrocardiogram (ECG) signals. The framework specifically leverages real-world clinical data from the MIMIC-III Matched Waveform Database to extract morphological and heart rate variability (HRV) features for high-accuracy physiological monitoring.

---

## 📊 Overview

Dysglycemia significantly impacts cardiac repolarization and autonomic nervous system regulation. This project implements an end-to-end machine learning workflow to:
1. **Process raw physiological signals** from intensive care environments.
2. **Extract clinically validated biomarkers** (25 morphological PQRST features).
3. **Analyze cardiac rhythms** via Pan-Tompkins R-peak detection and HRV quantification.
4. **Classify metabolic states** using a combination of traditional statistical models (One-Class SVM, XGBoost) and Deep Learning (ResNet).

---

## 📂 Data Acquisition

The framework is built around the **MIMIC-III Waveform Database Matched Subset** ([PhysioNet DOI: 10.13026/c2294b](http://doi.org/10.13026/c2294b)). To replicate this research or test the code, you can download the sample patient data (p000020) using the following command:

```bash
wget -r -N -c -np --domains physionet.org \
https://physionet.org/files/mimic3wdb-matched/1.0/p00/p000020/
```

> **Note:** Ensure your local path structure matches the `BASE_PATH` defined in the notebook (`data/physionet.org/...`).

---

## 🛠️ Pipeline Architecture

### 1. Signal Preprocessing
- **Filtering:** 4th-order zero-phase Butterworth bandpass filter (0.5 – 40 Hz) to remove baseline wander and muscle artifacts.
- **Artifact Removal:** Internal logic for outlier detection and interpolation.

### 2. Feature Engineering
- **R-Peak Detection:** Implementation of the Pan-Tompkins algorithm for precise QRS localization.
- **Morphological Analysis:** Automated extraction of 25 distinct features including PR intervals, QT dispersion, and T-wave amplitudes.
- **HRV Analysis:** Time-domain (SDNN, RMSSD) and Frequency-domain (LF, HF, VLF) metrics.

### 3. Machine Learning Framework
- **One-Class SVM:** Anomaly detection for out-of-range glucose levels based on the protocol by *Chiu et al. (2023)*.
- **XGBoost:** Gradient boosted decision trees for multi-modal feature classification.
- **Deep Learning:** ResNet architecture adapted for 1D time-series ECG classification.

---

## 🚀 Installation & Setup

### Prerequisites
- Python 3.8+
- Jupyter Notebook or JupyterLab

### Dependencies
Install the required Python packages using the provided `requirements.txt`:

```bash
pip install -r requirements.txt
```

### Libraries used:
- `wfdb`: Official PhysioNet waveform reader.
- `scipy.signal`: Digital signal processing.
- `xgboost` & `scikit-learn`: Supervised and unsupervised modeling.
- `matplotlib` & `seaborn`: High-resolution research visualizations.

---

## 📈 Visualizations

The notebook generates several figures illustrating the physiological state of the patient:
- **Multi-channel Overview:** Simultaneous visualization of ECG, Arterial Blood Pressure (ABP), and Pulmonary Artery Pressure (PAP).
- **R-Peak Detection Performance:** Accuracy check for the beat segmentation.
- **PQRST Mapping:** Visual validation of the 25 morphological fiducial points.
- **Model Interpretabilty:** Feature importance plots and ROC curves for dysglycemia detection.

---

## 📖 References

- **Chiu, C. C., et al. (2023).** *"Electrocardiogram-based dysglycemia screening using one-class support vector machine."* (Primary methodology reference).
- **MIMIC-III Waveform Database.** Johnson, A. E. W., et al. Scientific Data (2016).

---

## ⚖️ License
This project is intended for research and educational purposes. Data usage must comply with the [PhysioNet Credentialed Health Data License](https://physionet.org/about/license/).
