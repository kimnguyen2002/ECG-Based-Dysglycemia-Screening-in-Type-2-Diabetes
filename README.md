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

```bash
git clone https://github.com/kimnguyen2002/ECG-Based-Dysglycemia-Screening-in-Type-2-Diabetes.git
cd ECG-Based-Dysglycemia-Screening-in-Type-2-Diabetes
pip install -r requirements.txt
```

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

1.  **Chiu I-M, et al. (2023).** *"Utilization of Personalized Machine-Learning to Screen for Dysglycemia from Ambulatory ECG, toward Noninvasive Blood Glucose Monitoring."* **Biosensors**, 13, 23. [DOI: 10.3390/bios13010023](https://doi.org/10.3390/bios13010023)
2.  **González S, et al. (2024).** *"Multi-modal heart failure risk estimation based on short ECG and sampled long-term HRV."* **Information Fusion**, 107, 102337. [DOI: 10.1016/j.inffus.2024.102337](https://doi.org/10.1016/j.inffus.2024.102337)
3.  **Fu Q, et al. (2023).** *"Effect of SGLT-2 inhibitor dapagliflozin on left ventricular remodeling in patients with type 2 diabetes and HFrEF."* **BMC Cardiovascular Disorders**, 23:544. [DOI: 10.1186/s12872-023-03591-3](https://doi.org/10.1186/s12872-023-03591-3)
4.  **Isaksen JL, et al. (2024).** *"Electrocardiographic markers in patients with type 2 diabetes and the role of diabetes duration."* **Journal of Electrocardiology**, 84, 129–136. [DOI: 10.1016/j.jelectrocard.2024.04.003](https://doi.org/10.1016/j.jelectrocard.2024.04.003)
5.  **Mohsen F, et al. (2025).** *"ECG features improve multimodal deep learning prediction of incident T2DM in a Middle Eastern cohort."* **Scientific Reports**, 15, 27164. [DOI: 10.1038/s41598-025-12633-z](https://doi.org/10.1038/s41598-025-12633-z)
6.  **Savvopoulos S, et al. (2025).** *"AI-based integration of ECG biomarkers for assessing cardiac risk in type 2 diabetes mellitus with comorbid conditions for patient stratification."* **Frontiers in Medicine**, 12, 1646495. [DOI: 10.3389/fmed.2025.1646495](https://doi.org/10.3389/fmed.2025.1646495)
7.  **Johnson AEW, et al. (2016).** *"MIMIC-III, a freely accessible critical care database."* **Scientific Data**, 3, 160035. [DOI: 10.1038/sdata.2016.35](https://doi.org/10.1038/sdata.2016.35)
8.  **Moody GB, et al. (2000).** *"PhysioNet: A Research Resource for Studies of Complex Physiologic and Biomedical Signals."* **Circulation**, 101, e215–e220. [DOI: 10.1161/01.CIR.101.23.e215](https://doi.org/10.1161/01.CIR.101.23.e215)
9.  **Pan J, Tompkins WJ. (1985).** *"A Real-Time QRS Detection Algorithm."* **IEEE Transactions on Biomedical Engineering**, 32(3), 230–236. [DOI: 10.1109/TBME.1985.325532](https://doi.org/10.1109/TBME.1985.325532)
10. **Goldberger AL, et al. (2000).** *"PhysioBank, PhysioToolkit, and PhysioNet."* **Circulation**, 101(23), e215–e220. [PhysioNet DOI: 10.13026/c2294b](https://doi.org/10.13026/c2294b)

---

## ⚖️ License
This project is intended for research and educational purposes to simulate the working of ECG. Data usage must comply with the [PhysioNet Credentialed Health Data License](https://physionet.org/about/licenses/open-data-commons-attribution-license-v10/).
