# Network Data Security Scanner

<a target="_blank" href="https://cookiecutter-data-science.drivendata.org/">
    <img src="https://img.shields.io/badge/CCDS-Project%20template-328F97?logo=cookiecutter" />
</a>

A machine learning-based intrusion detection system that detects and classifies network attacks with 98.59% accuracy using the CIC-UNSW-NB15 dataset. This project implements a LightGBM classifier capable of identifying 10 types of network threats including DoS attacks, exploits, backdoors, and worms.

## Overview

Traditional intrusion detection systems rely on static rules and signatures that cannot adapt to evolving attack patterns. This project leverages machine learning to dynamically detect malicious network activity by analyzing traffic metadata and behavior patterns across 30 key network features.

**Final Model Performance:**
- **Overall Accuracy:** 98.59%
- **Benign Traffic Detection:** 99%
- **Model Type:** LightGBM Classifier
- **Dataset:** CIC-UNSW-NB15 (100,000 samples from 447,915 original instances)

📊 **[View Final Notebook](notebooks/Model.ipynb)**

[Project Documentation](reports/Capstone_Final_Doc.pdf) | [Initial Proposal](docs/NetworkDataandCybersecurity.pdf)

## Key Findings

### Attack Types Detected
The model classifies network traffic into 10 categories:
- **Benign:** Normal network activity
- **Analysis:** Network scanning and reconnaissance (passive)
- **Backdoor:** Persistent unauthorized access mechanisms
- **DoS:** Denial of Service attacks (network flooding)
- **Exploits:** Hardware/firmware-specific vulnerability exploitation
- **Fuzzers:** Automated malformed packet attacks
- **Generic:** General unauthorized access attempts
- **Reconnaissance:** Active targeted network scans
- **Shellcode:** Remote code execution attempts
- **Worms:** Self-replicating malware propagation

### Model Comparison Results
Model selection was updated to account for class imbalance using **Macro-F1** and per-class recall, not accuracy alone.

| Finalist Model + Strategy | Macro-F1 (Imbalance Study) | Selection Note |
|-------|----------|----------|
| **Random Forest + RandomOverSampler** | **0.4720** | Best overall Macro-F1, but weaker minority-class behavior on at least one class (notably Worms) |
| **LightGBM + RandomOverSampler** | **0.4708** | Near-top Macro-F1 with stronger minority-class consistency and better speed/performance balance |

**Final model:** LightGBM (`random_oversample` + tuned parameters). It was chosen for more robust minority-class behavior while keeping strong overall performance and practical inference speed.

### Data Processing
- **Data Cleaning:** Aligned schema across source files, removed duplicates, handled infinities/missing values, and kept a consistent feature space across splits.
- **Categorical Encoding:** One-hot encoded `Protocol` and `Dst Port`, then aligned validation/holdout columns to the training schema.
- **Split Strategy:** Preserved predefined split workflow (`df1` train, `df2` validation, `df3` holdout).
- **Modeling Artifacts:** Saved sparse matrices and labels for reproducible modeling (`X_train.npz`, `X_val.npz`, `X_holdout.npz`, `X_feature_names.csv`, `y_train.csv`, `y_val.csv`, `y_holdout.csv`).
- **Scaling Note:** Included as a demonstration step only; final tree-based models were trained on unscaled features.

## Project Organization

```
├── Makefile           <- Makefile with convenience commands like `make data` or `make train`
├── README.md          <- The top-level README for developers using this project.
├── data
│   ├── external       <- Data from third party sources.
│   ├── interim        <- Intermediate data that has been transformed.
│   ├── processed      <- The final, canonical data sets for modeling.
│   └── raw            <- The original, immutable data dump.
│
├── docs               <- A default mkdocs project; see www.mkdocs.org for details
│
├── models             <- Trained and serialized models, model predictions, or model summaries
│
├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
│                         the creator's initials, and a short `-` delimited description, e.g.
│                         `1.0-jqp-initial-data-exploration`.
│
├── pyproject.toml     <- Project configuration file with package metadata for
│                         networkdatasecurityscanner and configuration for tools like black
│
├── references         <- Data dictionaries, manuals, and all other explanatory materials.
│
├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
│   └── figures        <- Generated graphics and figures to be used in reporting
│
├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
│                         generated with `pip freeze > requirements.txt`
│
├── setup.cfg          <- Configuration file for flake8
```

## Getting Started

### Prerequisites
```bash
pip install -r requirements.txt
```

## References

Dataset: [CIC-UNSW-NB15](https://www.unb.ca/cic/datasets/cic-unsw-nb15.html)

```
H. Mohammadian, A. H. Lashkari, A. Ghorbani. “Poisoning and Evasion: Deep Learning-Based NIDS under Adversarial Attacks,” 21st Annual International Conference on Privacy, Security and Trust (PST), 2024.
```

---
