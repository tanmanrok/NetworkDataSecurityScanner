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

📊 **[View Final Notebook](notebooks/Final.ipynb)**

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
| Model | Accuracy |
|-------|----------|
| **LightGBM** | **98.59%** ✓ |
| XGBoost | 98.56% |
| Random Forest | 98.49% |
| Gradient Boosting | 98.29% |
| Logistic Regression | 96.64% |

LightGBM was selected as the final model due to superior balanced predictions across all threat categories, particularly for benign traffic classification (99% accuracy).

### Data Processing
- **Feature Engineering:** Reduced from 83 to 30 most impactful features based on correlation analysis
- **Sampling Strategy:** Stratified sampling maintaining original attack distribution
- **Key Insight:** No single parameter strongly predicts attacks; multiple features required for accurate detection

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
