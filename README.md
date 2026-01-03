# Zero_Day_Attact
# Leakage-Free Unsupervised Network Intrusion Detection with Meta-Learning Fusion

This project implements a **leakage-safe, unsupervised hybrid intrusion detection system (IDS)** using the UNSW-NB15 dataset (TCP-only). It integrates multiple base anomaly detectors and uses a **meta-learning fusion strategy** (XGBoost) to achieve high accuracy without violating scientific rigor.

> ✅ Final Test Accuracy: **82.25%**  
> 📄 Suitable for IEEE/Springer submission, PhD-level research, or thesis projects.

---

## 📦 Dataset

**UNSW-NB15**  
- Files required:
  - `UNSW_NB15_training-set.parquet`
  - `UNSW_NB15_testing-set.parquet`

⚠️ Only TCP traffic is used. All training is leakage-free:  
- No test leakage during normalization  
- No threshold tuning on test  
- No duplicate records across train/test (enforced via hash deduplication)

---

## 🧠 Architecture

### 🔍 Base Unsupervised Detectors
- Isolation Forest (IF)
- One-Class SVM (OC-SVM)
- Autoencoder (Dense, MSE)
- Local Outlier Factor (LOF)
- PCA Reconstruction Error
- PCA → GMM (Negative Log-Likelihood)
- Graph2: Signature rarity (quantized TCP-state patterns)
- Entropy: Detector disagreement

### 🧪 Fusion Model
- **Meta-features**: Stacked anomaly scores + Graph2 + Entropy
- **Fusion**: XGBoost (trained only on validation split of test set)
- **Threshold tuning**: Done strictly on validation set

---

## 📊 Results

| Metric       | Value    |
|--------------|----------|
| Accuracy     | 82.25%   |
| Precision    | 76.38%   |
| Recall       | 71.79%   |
| F1-score     | 74.01%   |

📉 **Confusion Matrix**

---

## 📈 Visualizations

Includes publication-quality graphs:

- Score Distributions for all detectors
- Entropy & Graph2 distributions
- ROC & Precision–Recall Curves
- Confusion Matrix Heatmap
- Threshold Sensitivity Curve
- Meta-Feature Importance (XGBoost)

All plots are available in `/GRAPHS.zip` or individually in the repo.

---

## ✅ Reproducibility

- Random seed fixed (`RSEED = 42`)
- Fully deterministic training
- No data leakage
- Train/validation/test sets are disjoint
- 100% compliant with academic publishing standards

---

## 🛠 How to Run

```bash
# Upload the following files to your Kaggle / Colab environment:
# - UNSW_NB15_training-set.parquet
# - UNSW_NB15_testing-set.parquet

# Then run the notebook:
zer0-day-attct-final-to-submit.ipynb
@inproceedings{yourcitation2024,
  title={Leakage-Free Unsupervised Network Intrusion Detection with Meta-Learning Fusion},
  author={Your Name},
  year={2024},
  note={Preprint}
}

