# ÄKTA Chromatography Analysis Notebook

## Overview

This notebook provides a lightweight analysis workflow for visualizing and interpreting chromatographic data generated from **ÄKTA FPLC systems**. It is designed for rapid inspection of purification runs (e.g., Ni-NTA affinity chromatography) directly from exported CSV files. The workflow supports automated plotting and peak detection, enabling fast evaluation of protein purification quality.

The notebook is optimized for use in **Google Colab with Google Drive storage**, but can be adapted for local execution.

---

## Features

* Import and preprocess ÄKTA chromatography data
* Compatible with multiple ÄKTA export formats (e.g., small vs. large systems)
* Automated plotting of chromatograms
* Peak detection using `scipy.signal.find_peaks`
* Minimal dependencies and easy customization

---

## Requirements

### Python Packages

* `pandas`
* `matplotlib`
* `scipy`

Install locally via:

```bash
pip install pandas matplotlib scipy
```

---

## Directory Structure

The notebook assumes chromatographic CSV files are stored in a dedicated directory:

```
Äkta_daten/
├── 20251119_sample_run.csv
├── 20251029_sample_run.csv
└── ...
```

In the default configuration, this folder is located on **Google Drive**.

---

## Usage

### 1. Mount Google Drive (Colab)

```python
from google.colab import drive
drive.mount('/content/drive')
```

Set the working directory:

```python
directory = '/content/drive/MyDrive/Äkta_daten'
os.chdir(directory)
```

---

### 2. Load Chromatography Data

The notebook expects a helper function (e.g., `load()`) that reads exported ÄKTA CSV files and standardizes column names.

Example:

```python
name = '20251119_Cdkal_CDel1-62_NDel496_4L_LB_1NiNTA_GB'
akta_type = 'large'

data = load(name, akta_type=akta_type)
```

**Parameters**

* `name` — filename without extension
* `akta_type` — distinguishes between file formats (e.g., `small`, `large`)

---

### 3. Plot Chromatograms

The central plotting function:

```python
plot(name, input_data, akta_type, **kwargs)
```

#### Functionality

* Generates chromatograms for absorbance traces (e.g., A280)
* Supports customization via keyword arguments
* Enables peak detection using SciPy

---

## Typical Workflow

1. Export chromatographic data from ÄKTA as CSV
2. Upload files to Google Drive
3. Run notebook cells sequentially
4. Load dataset using `load()`
5. Generate plots with `plot()`
6. Interpret elution profiles and peaks

---

## Applications

This notebook is particularly useful for:

* His-tag purification (Ni-NTA)
* Protein construct screening
* Domain truncation comparisons
* Monitoring purification reproducibility
* Rapid QC during protein production

---

## Customization

### Adapting to Local Execution

Replace the Google Drive mounting section with:

```python
directory = os.getcwd()
os.chdir(directory)
```

---

### Adding New Plot Features

Potential extensions:

* Multi-trace overlays
* Fraction annotations
* Conductivity or gradient overlays
* Automated peak integration
* Export-ready publication plots

---

## Notes

* Ensure CSV files match expected ÄKTA export formatting.
* The notebook currently contains duplicated imports and Colab mounting cells, which can be safely consolidated.
* Consider refactoring into:

  * `load.py`
  * `plotting.py`
  * Notebook for visualization only