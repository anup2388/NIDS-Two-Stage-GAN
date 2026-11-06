# NIDS-Two-Stage-GAN
Network Intrusion Detection System using a Two-Stage GAN Architecture
# TSG-NIDS v5: Two-Stage GAN-Based Network Intrusion Detection System

## Overview

This repository contains the implementation of **TSG-NIDS v5**, a Two-Stage Network Intrusion Detection System designed to detect and classify network attacks, with particular emphasis on improving the detection of minority and rare attack classes.

The proposed framework combines a regularised LightGBM-based detection gate with a second-stage stacked ensemble classifier. It uses Conditional Generative Adversarial Networks (CTGAN) to generate synthetic samples for minority attack classes and incorporates benign hard-negative samples to improve classification reliability.

The implementation is developed for research and experimental evaluation, with a focus on multiclass intrusion detection and controlling false alarm rates.

## Proposed Architecture

The proposed TSG-NIDS framework consists of two major stages.

### Stage 1: LightGBM-Based Detection Gate

- Uses a regularised LightGBM classifier.
- Separates potentially malicious traffic from benign traffic.
- Uses selected network flow features.
- Determines a detection threshold using validation data.
- Reduces the number of flows passed to the second stage.

### Stage 2: GAN-Based Data Augmentation and Stacked Ensemble Classification

The second stage performs multiclass attack classification.

It incorporates:

- **Per-Class CTGAN:** Generates synthetic samples for minority attack classes.
- **SMOTE:** Used as a reference augmentation technique.
- **Benign Hard Negatives:** Includes challenging benign flows that receive high attack scores from the first-stage gate.
- **Stacked Ensemble:** Combines Random Forest, Extra Trees and LightGBM as base classifiers, with XGBoost as the meta-learner.

The final classifier identifies the specific attack category or classifies the traffic as benign.

## Datasets

The implementation supports the following datasets:

1. CIC-IDS2017
2. CSE-CIC-IDS2018

The datasets contain network traffic flow records with benign and multiple attack categories.

Dataset preprocessing includes:

- Removing duplicate records.
- Handling missing and infinite values.
- Removing repeated header rows.
- Removing identifier and non-predictive columns.
- Cleaning inconsistent attack labels.
- Feature selection using mutual information.
- Correlation-based feature reduction.

**Note:** The datasets are not included in this repository. Users must obtain the datasets from their respective sources and configure the data paths before execution.

## Methodology

The experimental framework includes:

1. Dataset preprocessing and cleaning.
2. Training, validation and testing data preparation.
3. Mutual-information-based feature selection.
4. LightGBM gate training.
5. Out-of-fold gate scoring.
6. Benign hard-negative selection.
7. Minority-class synthetic data generation using CTGAN.
8. Stage-2 stacked ensemble training.
9. Validation-based threshold selection.
10. Multiclass intrusion detection and performance evaluation.

The proposed generator is configured as per-class CTGAN. The experimental configuration is frozen, and test data is not used for model or threshold selection.

## Experimental Evaluation

The framework evaluates the models using multiple performance measures, including:

- Accuracy
- Precision
- Recall
- Macro-F1 Score
- Matthews Correlation Coefficient (MCC)
- ROC-AUC
- PR-AUC
- Confusion Matrix
- False Positive Rate (FPR)
- Training Time
- Inference Time

Additional experiments include:

- Comparison with single-stage classification models.
- Comparison of SMOTE and CTGAN augmentation.
- False-alarm budget analysis at 0.5%, 1% and 2%.
- Hard-negative sensitivity analysis.
- Ablation studies.
- Synthetic data quality evaluation.
- Statistical significance testing using McNemar's test and bootstrap analysis.

## Repository Structure

```text
TSG-NIDS/
│
├── README.md
│
├── notebooks/
│   └── nids_two_stage_gan_v5.ipynb
│
├── datasets/
│   └── (Dataset files - not included)
│
├── checkpoints/
│   └── (Saved model checkpoints)
│
├── results/
│   └── (Experimental results and figures)
│
└── requirements.txt
```

The directory structure is indicative. Actual experiment outputs are generated under the configured output directory.

## Requirements

The implementation uses Python and the following major libraries:

- NumPy
- Pandas
- Scikit-learn
- LightGBM
- XGBoost
- Imbalanced-learn
- CTGAN
- SDV
- SciPy
- Matplotlib
- Joblib
- KaggleHub
- PyArrow
- OpenPyXL
- Psutil

## Installation and Execution

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/TSG-NIDS.git
cd TSG-NIDS
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

Alternatively, run the dependency installation cell in the Jupyter Notebook.

### 3. Configure the dataset

The notebook supports CIC-IDS2017 and CSE-CIC-IDS2018.

For CIC-IDS2017, the dataset can be downloaded using KaggleHub or provided through a local dataset directory.

For CSE-CIC-IDS2018, configure the dataset CSV path using the `NIDS_DATA_PATH` environment variable.

### 4. Execute the notebook

Open:

```text
notebooks/nids_two_stage_gan_v5.ipynb
```

The notebook can be executed using Google Colab or a suitable Python environment.

Google Colab users can mount Google Drive to access datasets and save experimental outputs.

## Experimental Configuration

The implementation includes configurable parameters for:

- Dataset selection.
- Train, validation and test splits.
- Feature selection.
- CTGAN augmentation.
- SMOTE augmentation.
- Hard-negative selection.
- Classification thresholds.
- False-alarm budgets.
- Model training and inference timing.

For reproducible comparisons, experiments should use consistent hardware and runtime configurations.

## Research Contribution

The main contributions of the proposed framework are:

1. A two-stage intrusion detection architecture combining LightGBM-based traffic filtering and multiclass stacked ensemble classification.
2. Per-class CTGAN-based synthetic sample generation to address minority attack representation.
3. Integration of benign hard negatives to improve the second-stage classification process.
4. Validation-based threshold selection with false-alarm constraints.
5. Comprehensive evaluation involving baseline comparisons, ablation studies, synthetic data quality analysis and statistical significance testing.

## Disclaimer

This repository is intended for academic research and educational purposes. The experimental results depend on the dataset, preprocessing configuration, hardware and execution environment.

## Citation

If you use this implementation in your research, please cite the associated research publication once it is published.

**Project:** TSG-NIDS v5 – Two-Stage GAN-Based Network Intrusion Detection System.
