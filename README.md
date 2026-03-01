# NTT Data Merit Prize 2025–26 — Fake News Detection in Portuguese

**Finalist — NTT Data Merit Prize 2025–26**  
Machine Learning · Instituto Superior Técnico · Academic Year 2025/2026

---

## Overview

This project tackles the challenge of **detecting fake news in Portuguese** using classical machine learning models trained on a labeled dataset of Portuguese news articles. It was developed as part of the NTT Data Merit Prize competition for the Machine Learning course at [Instituto Superior Técnico (IST)](https://tecnico.ulisboa.pt/), Lisbon.

The work covers the full ML pipeline: feature extraction, hyperparameter tuning, model evaluation, interpretability analysis, and unsupervised clustering — achieving up to **92% accuracy** on lemmatized data.

**Authors:**
- Pedro Vicente — [ist1109852](mailto:pedro.costa.vicente@tecnico.ulisboa.pt)
- Ema Ferrão — [ist1109247](mailto:emassferrao@tecnico.ulisboa.pt)

---

## Repository Structure

```
NTT_Data_merit_challenge/
├── src/                    # Jupyter notebooks with all experiments
├── important_docs/         # Supporting documents and datasets
├── latex_formatting/       # LaTeX source for the report
├── report.pdf              # Final submitted report
└── README.md
```

---

## Methodology

### Feature Extraction

Text was vectorized using **TF-IDF** with the following configuration:
- Minimum document frequency: 10
- Maximum document frequency: 90%
- Vocabulary size: 5,000 features
- Portuguese stopword removal + lowercase normalization

A key finding from an ablation study: **retaining numeric tokens** (dates, statistics, quantities) consistently improved accuracy across all classifiers, as numbers act as discriminative stylistic markers distinguishing authentic journalism from fabricated content.

### Preprocessing Configurations Evaluated

| Configuration | Description |
|---|---|
| Not lemmatized, with duplicates | Raw text, original dataset |
| Lemmatized, with duplicates | Base-form words, original dataset |
| Lemmatized, without duplicates | Base-form words, deduplicated dataset |

### Models Trained

All models were tuned via **stratified 5-fold cross-validation** (seed=42) using F1-score as the optimization metric:

- Decision Tree
- Gaussian Naive Bayes
- Logistic Regression (L1 regularization)
- Logistic Regression (L2 regularization)
- Multi-Layer Perceptron (MLP)

---

## Results

### Best Configuration: Lemmatized, with duplicates

| Model | Accuracy | F1-Score |
|---|---|---|
| Decision Tree | 0.9640 | 0.9640 |
| Gaussian Naive Bayes | 0.8637 | 0.8637 |
| Logistic Regression L2 | 0.9108 | 0.9108 |
| Logistic Regression L1 | 0.9037 | 0.9037 |
| **MLP Classifier** | **0.9203** | **0.9203** |

### Most Realistic Configuration: Lemmatized, without duplicates

| Model | Accuracy | F1-Score |
|---|---|---|
| Decision Tree | 0.8058 | 0.8058 |
| Gaussian Naive Bayes | 0.8395 | 0.8397 |
| Logistic Regression L2 | 0.8820 | 0.8816 |
| Logistic Regression L1 | 0.8834 | 0.8831 |
| **MLP Classifier** | **0.8883** | **0.8880** |

> Duplicate-containing datasets inflate metrics through memorization. The **duplicate-free** results offer more realistic generalization estimates for production deployment.

### Best Model: MLP Classifier

The MLP achieved the highest accuracy across both configurations and obtained an **AUC of 0.96** on the ROC curve, demonstrating strong discriminative ability regardless of classification threshold.

---

## Model Interpretability

### Global — Logistic Regression Coefficients (L1)

The L1 model retained **2,116 non-zero features** out of 5,000, offering natural sparsity and interpretability. Fake-news marker coefficients reach magnitudes near −20, while real-news markers peak around +15 — indicating that fake news leaves stronger lexical fingerprints.

### Local — LIME Explanations

LIME was applied to four validation samples (IDs: 2921, 2437, 5557, 1697) for both the Logistic Regression and MLP models, providing instance-level justifications for each prediction. The MLP's non-linearity makes LIME especially valuable for transparency here.

### Global — Permutation Importance (MLP)

Permutation Importance was computed over 1,000 validation samples across 10 random permutations. Top discriminative features include: `detido`, `última`, `estados`, `inflação`, `segurança`, `esquerda`, `2021`, `directo`, and `feira`.

---

## Clustering Analysis

K-Means (K=5, max_iter=500, random_state=42) was applied to explore unsupervised structure, yielding five thematic clusters:

| Cluster | Theme | Key Terms |
|---|---|---|
| 0 | Health & Pandemic | saúde, vacina, covid, médico |
| 1 | Ukraine-Russia War | russo, ucrânia, guerra, putin |
| 2 | Miscellaneous | ter, ir, fazer, poder |
| 3 | Portuguese Domestic Politics | ministro, governo, costa, partido |
| 4 | Economic & Fiscal Policy | euro, milhão, preço, banco |

PCA visualization confirmed that clustering captures **topical similarity**, not veracity — fake and real articles remain intermixed across all clusters. This highlights the fundamental limitation of unsupervised approaches for fake news detection.

---

## Setup & Usage

### Requirements

```bash
pip install numpy pandas scikit-learn matplotlib seaborn lime jupyter
```

For Portuguese lemmatization:
```bash
pip install spacy
python -m spacy download pt_core_news_sm
```

### Running the Notebooks

```bash
git clone https://github.com/pedroMVicente/NTT_Data_merit_challenge.git
cd NTT_Data_merit_challenge
jupyter notebook src/
```

---

## Report

The full technical report (submitted for the competition) is available as [`report.pdf`](./report.pdf), formatted in the NeurIPS 2024 style.

---

## Competition

This project was submitted to the **NTT Data Merit Prize 2025–26**, a competition organized in the context of the Machine Learning course at Instituto Superior Técnico. The project was selected as a **finalist**.

---

## License

This repository is intended for academic and educational purposes.