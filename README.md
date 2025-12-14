# Fieldwork-data-preprocessing

# Spectral Data Preprocessing Pipeline (ASD Field Spectroscopy)

This repository contains a set of R scripts designed to **automate the preprocessing of field spectrometer data** collected using ASD (Analytical Spectral Devices) instruments. The pipeline is optimized for **large field campaigns** where spectral data are organized in nested directory structures (e.g., by year, site, plot, or sampling date).

The scripts support **recursive directory processing**, **standardized spectral filtering**, and **reproducible data organization**, making them suitable for vegetation stress, forest health, and calibration/validation workflows.

---

## Repository Structure and Scripts

The preprocessing workflow is implemented as **three sequential R scripts**, each responsible for a specific stage of the spectral data pipeline.

---

### 1. ASD Spectral Data Consolidator  
**Script:** `asd_spectral_data_consolidator_recursive.R`

This script ingests raw ASD binary files (`*.asd`) and converts them into consolidated CSV files.

**Key functions:**
- Recursively scans all subfolders under a user-defined input directory.
- Identifies folders containing ASD files.
- Reads ASD spectra using the `spectrolab` package.
- Consolidates all spectra within a folder into a single CSV file.
- Preserves the original directory hierarchy in the output location.

**Input:**  
- Raw ASD files (`*.asd`) organized in nested folders.

**Output:**  
- One CSV file per folder containing wavelength-resolved reflectance spectra.

---

### 2. Spectral CSV Preprocessor (Clipping + Savitzky–Golay Filtering)  
**Script:** `recursive_spectral_csv_preprocessor.R`

This script performs spectral normalization and noise reduction on the consolidated CSV files.

**Key functions:**
- Recursively processes all spectral CSV files.
- Clips reflectance values to the physically valid range \([0, 1]\).
- Applies Savitzky–Golay smoothing independently to each spectrum.
- Writes filtered CSV files to a mirrored directory structure.
- Appends `_filtered` to output filenames.

**Input:**  
- Spectral CSV files produced by Script 1.

**Output:**  
- Filtered spectral CSV files suitable for analysis and modeling.

---

### 3. [Add Script Name Here – e.g., Spectral Quality Control or Aggregation]
**Script:** `script_name_here.R`

This script provides an additional processing step in the spectral workflow (e.g., quality control, wavelength selection, resampling, or feature extraction).

**Key functions:**
- [Brief description of what this script does]
- [Key transformations or outputs]

**Input:**  
- Filtered spectral CSV files.

**Output:**  
- Analysis-ready spectral datasets.

---

## Typical Workflow

```text
Raw ASD (*.asd)
   ↓
[1] ASD Spectral Data Consolidator
   ↓
Consolidated spectral CSVs
   ↓
[2] Spectral CSV Preprocessor (Clipping + Filtering)
   ↓
Filtered spectral CSVs
   ↓
[3] Downstream analysis / QC / modeling
