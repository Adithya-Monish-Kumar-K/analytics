
# analytics

This repository contains visualizations and explanations for graphs generated in **Stage 2** of the Decodex project (CASE 01: STABILIS — In-Space Validation & Model Robustness Check).

## Stage 2 Graphs and Explanations

### 1. Performance Dashboard
![Performance Dashboard](stage2_outputs/fig_s2_performance.png)
**Explanation:**
This dashboard compares key behavioral metrics between the training (Stage 1) and validation (Stage 2) datasets. While per-transaction metrics like basket value remain stable (only -6.1% drift, KS p=0.13), cumulative per-user metrics such as ERPU and frequency drop sharply in validation due to the shorter observation window, not model failure. The validation set over-represents one-time buyers, but per-transaction economics are identical, confirming model generalization.

### 2. Ranking Quality (Leak-Free)
![Ranking Quality](stage2_outputs/fig_s2_ranking.png)
**Explanation:**
Validation users are ranked by their training ERPU. The top 10% by training scores capture 27.8% of validation revenue (2.78x lift over random). The basket value distributions are statistically identical (KS p=0.134), and user ERPU persistence is high (r = 0.712). This demonstrates genuine predictive signal and confirms the model's ranking utility is strong and generalizable.

### 3. Overfitting Diagnosis & Recalibration
![Calibration](stage2_outputs/fig_s2_calibration.png)
**Explanation:**
Feature stability is assessed by Spearman correlation with net revenue. Product diversity is the most robust predictor (ρ = +0.812 in validation, +0.893 in training). No overfitting is detected; all correlations remain directionally consistent. Instability in frequency and tenure is explained by the high proportion of one-time buyers in validation. Only the return rate is recalibrated (8.98% → 4.82%), resulting in a minor ERPU adjustment (−2.2%).

### 4. Overfitting Check
![Overfitting](stage2_outputs/fig_s2_overfitting.png)
**Explanation:**
This graph visualizes the concentration and persistence of high-value users. The drop in Gini and top-decile share in validation is expected due to the shorter observation window. The model does not overfit; performance drops are mechanically explained by the sample design, not by spurious relationships.

---

## Key Insights

- **Model Generalization:** The Stage 1 model generalizes well to the validation set. Per-transaction metrics are stable, and the ERPU decomposition formula holds with <1% error.
- **Ranking Quality:** The model correctly identifies high-value users in unseen data (top-decile lift = 2.78x in FINAL_STAGE2, 3.94x in STAGE2_SUBMISSION).
- **No Overfitting:** Feature correlations remain directionally consistent. Instability is explained by sample design, not overfitting.
- **Product Diversity:** The most robust predictor of revenue, making it the safest targeting variable for future stages.
- **Return Rate:** The only metric requiring recalibration, reflecting genuine behavioral improvement in the validation population.

---

For detailed analysis, see the Stage 2 submission files in `stage2_outputs/`.
