# ECG Arrhythmia Analysis — MIT-BIH Database

## Overview
Exploratory analysis of cardiac arrhythmias using the MIT-BIH Arrhythmia Database. 
This project processes and analyses 112,000+ annotated heartbeats from 48 patients, computing RR intervals, heart rate variability (HRV) metrics, and beat-type distributions 
to characterise different cardiac arrhythmias.
## Dataset
The MIT-BIH Arrhythmia Database contains 48 half-hour ECG recordings sampled at 360 Hz, with expert annotations for every heartbeat. 
To reproduce this analysis, download the database from PhysioNet and place it in a `data/` folder.
## Methods
1. **Data Loading:** Loaded all 48 patient records using the `wfdb` library, extracting ECG signals and beat annotations into a unified DataFrame.

2. **RR Interval Computation:** Calculated RR intervals (time between consecutive beats) in milliseconds, grouped by patient to avoid cross-patient contamination.

3. **Data Cleaning:** Removed physiologically impossible values 
   (`100ms ≤ RR interval ≤ 5000ms`), eliminating artefacts and non-beat annotations.

4. **Beat Analysis:** Computed BPM statistics (min, max, mean) and beat-type distributions per patient.

5. **HRV Analysis:** Calculated SDNN (standard deviation of RR intervals) per patient as a measure of heart rate variability.

6. **Visualisation:** Plotted RR interval distributions and HRV scatter plot to characterise different arrhythmia types.
## Key Findings
- **Paced beats (/)** show extremely narrow RR interval distribution, confirming the artificial and highly regular rhythm imposed by pacemakers.

- **Ventricular premature beats (V)** have a lower median RR interval (~500ms, ~120 bpm), arriving earlier than expected (premature ventricular contractions).

- **Right bundle branch block (R)** exhibits the highest variability, with many outliers above 2000ms, indicating conduction delays causing long pauses.

- **Left bundle branch block (L)** maintains a similar median to normal beats (~800ms) but with delayed conduction, confirming the block affects morphology more than rate.

- **Patient-level HRV (SDNN)** ranges from ~42ms (stable rhythm) to ~600ms (severe arrhythmia), with patients 232 and 201 showing the highest variability.
## Stack
Python · Pandas · NumPy · Matplotlib · Seaborn · wfdb
## Usage
1. Clone this repository
2. Install dependencies:
```bash
   pip install wfdb pandas numpy matplotlib seaborn
```
3. Download the [MIT-BIH Arrhythmia Database](https://physionet.org/content/mitdb/1.0.0/) 
   and place it in a `data/` folder inside the repo
4. Open and run `01_load_explore.ipynb` in Jupyter