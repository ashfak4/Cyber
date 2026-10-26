# ML Network Intrusion Detector

**IBM SkillsBuild Cyber Security Bootcamp 2026 — BharatCares**
Author: Ashfaq

## Project Description
A Scikit-learn machine learning model that classifies network connections as **Normal** or one of three attack types, using connection-level features from the KDD / NSL-KDD family of intrusion datasets:

- **DoS** – denial of service (e.g. SYN flood)
- **Probe** – scanning / reconnaissance (e.g. port scan)
- **R2L** – remote-to-local attacks (e.g. FTP password guessing)

Three models (Logistic Regression, Decision Tree, Random Forest) are compared inside a preprocessing pipeline. The best model is saved and used to detect new connections.

## Dataset
- **Default:** a reproducible *synthetic* dataset of 6,000 connections generated inside the notebook using real KDD feature names (includes stealthy attacks and 2% label noise). No download needed.
- **Real data (optional, recommended):** [NSL-KDD – Canadian Institute for Cybersecurity](https://www.unb.ca/cic/datasets/nsl.html).
  Map attack names to `Normal / DoS / Probe / R2L`, keep the feature columns listed in the notebook plus a `label` column, and save as `network_traffic.csv` in the project folder. It is loaded automatically.

## Technologies Used
Python 3.9+, Jupyter Notebook, pandas, NumPy, scikit-learn, matplotlib, seaborn, joblib

## Project Structure
```
Ashfaq_NetworkIntrusionDetector.ipynb   # complete code
requirements.txt                          # dependencies
Ashfaq_ProjectReport.docx               # full project report
README.md                                 # this file
```

## Setup & Run
```bash
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook Ashfaq_NetworkIntrusionDetector.ipynb
```
Choose **Kernel → Restart & Run All**. The trained model is saved as `intrusion_model.joblib`.

## Method Summary
1. Load / generate the labelled traffic dataset
2. Exploratory analysis of traffic classes and features
3. Preprocess (one-hot encoding + scaling) in a scikit-learn Pipeline
4. Train and cross-validate three classifiers (80/20 stratified split)
5. Evaluate: accuracy, macro F1, attack detection rate, false alarm rate, confusion matrix
6. Save the best model and classify sample connections (normal, SYN flood, port scan, password guessing)

## Key Results (synthetic dataset)
| Model | Accuracy | Macro F1 | Attack Detection Rate | False Alarm Rate |
|---|---|---|---|---|
| Logistic Regression | 0.9483 | 0.9410 | 0.8962 | 0.0000 |
| Decision Tree | 0.9367 | 0.9264 | 0.8998 | 0.0169 |
| **Random Forest** | **0.9500** | **0.9436** | 0.8998 | 0.0000 |

Missed attacks are mostly the deliberately stealthy ones that mimic normal traffic. Re-run with NSL-KDD for realistic figures.

## Limitations & Future Work
Synthetic default data; cannot detect unseen attack types. Future work: train on NSL-KDD / CIC-IDS2017, add Isolation Forest for anomaly detection, and feed live Zeek/Suricata logs.

## License
For educational use as part of the IBM SkillsBuild Cyber Security Bootcamp 2026.
