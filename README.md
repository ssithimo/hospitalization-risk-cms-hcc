# 🏥 Hospitalization Risk Prediction Using CMS-HCC Scores

**Notebook:** `Hospitalization-Risk.ipynb`  
**Language:** Python  
**Tech Stack:** `Pandas`, `NumPy`, `Scikit-learn`, `XGBoost`, `SHAP`, `Matplotlib`, `Seaborn`

---

## 📘 Objective
This project builds a predictive model to identify patients at risk of hospitalization using **CMS-HCC (Hierarchical Condition Category)** risk adjustment scores and simulated patient data.  
The CMS-HCC model quantifies patient comorbidities through condition-specific weights that represent their expected impact on healthcare costs. This framework mirrors how insurers and healthcare organizations use risk adjustment to forecast expenses, design interventions, and allocate care resources.

---

## 🧩 Project Workflow

### 1. Data Simulation
- Simulated 500 adult patients (ages 18–90) with demographic features, prior-year costs, and 1–3 ICD-10 conditions.  
- Five ICD-10 codes were mapped to CMS-HCC categories with assigned weights to compute patient-level risk scores.  
- Hospitalization was determined using a **probabilistic rule**:
  - Patients over 60 → 40% chance of hospitalization  
  - Patients 60 or younger → 20% chance  

This simplified simulation helps illustrate risk modeling concepts but limits real-world variability.

---

### 2. CMS-HCC Mapping & Risk Scoring
- Built a mapping function linking ICD-10 codes to HCC categories and hierarchical groups.  
- Aggregated HCC weights to calculate a **composite risk score** per patient, with an age adjustment (+0.15 for age > 60).  
- Emulates how the CMS-HCC system assigns higher scores to patients with multiple or severe chronic conditions.

---

### 3. Modeling
Prepared features (`age`, `gender`, `risk_score`) and target (`hospitalization`), encoding categorical variables as needed.  
Compared multiple classification models:

- **Logistic Regression** (baseline, class-weighted, and threshold-tuned)  
- **Random Forest**  
- **XGBoost (Gradient Boosting Machine)**  

Evaluation metrics: **ROC-AUC**, **precision**, **recall**, **F1**, and **F2** scores to assess trade-offs between false positives and false negatives.

---

### 4. Model Results & Interpretation

- Threshold tuning substantially improved recall (capturing 78% of positive cases) but reduced precision to 0.22, indicating a high false-positive rate.  
- Models performed slightly below random, suggesting limited predictive signal in the synthetic data.

---

### 5. SHAP Feature Importance
Used **SHAP values** to explain the logistic regression model’s predictions and quantify each feature’s contribution to hospitalization risk.  
Key predictors included **age** and **CMS-HCC risk score**, aligning with clinical expectations about hospitalization likelihood.

---

### 6. Conclusion
Despite efforts to fine-tune class weights and thresholds, all models struggled to accurately predict hospitalizations. The tuned logistic regression achieved higher recall but at the cost of inflated false positives, which in a real-world insurance setting could lead to artificially inflated cost projections under risk adjustment  

---

### 🚀 Key Takeaways
- **CMS-HCC scores** provide a standardized way to quantify patient comorbidity and risk burden.  
- **Threshold tuning** can improve recall but should be balanced against cost implications of false positives.  
- **Synthetic data realism** is critical — deterministic simulation patterns limit model generalization.  
- Future work should explore richer features (chronic conditions, utilization, demographics) and non-linear models with better calibration.
