# 🎵 Subscription Retention Analysis & Churn Prediction (KKBox)

This project explores **subscription retention and churn prediction** using the KKBox dataset.  
It demonstrates an **end-to-end data science workflow**: data preparation, feature engineering, exploratory analysis, predictive modeling, model interpretability, causal inference, and **experimentation design (A/B testing with CUPED)**.  

The goal is to **identify at-risk users**, evaluate potential interventions, and provide **actionable insights** for improving customer retention strategies.

---

## Project Workflow
1. **Data Understanding** – Explore users, transactions, and activity logs.  
2. **Data Preparation** – Clean and engineer features for churn modeling.  
3. **Exploratory Data Analysis (EDA)** – Identify patterns linked with churn.  
4. **Predictive Modeling** – Train and evaluate models (Logistic Regression, XGBoost).  
5. **Model Explainability** – Use SHAP values to interpret predictions.  
6. **Causal Insights** – Explore retention drivers (auto-renew vs engagement).  
7. **Experimentation (A/B Testing)** – Simulate retention interventions with:  
   - Randomization (deterministic hashing)  
   - SRM (Sample Ratio Mismatch) check  
   - Covariate balance checks  
   - Outcome difference (renewal rates, lift, confidence interval)  
   - CUPED adjustment for variance reduction  
8. **Conclusions & Recommendations** – Translate results into business insights.  

---

## Dataset
- **Source**: [KKBox Churn Prediction Challenge (Kaggle)](https://www.kaggle.com/c/kkbox-churn-prediction-challenge)  
- **Key Tables**:  
  - `train.csv` – Labels (churned or not).  
  - `members.csv` – Demographics (gender, registration date, etc.).  
  - `transactions.csv` – Subscription payments, renewals, cancellations.  
  - `user_logs.csv` – Daily listening activity (play counts, listening time).  

---

## Key Insights (EDA)
- Users with **shorter plans (<1 month)** churn more often.  
- **Auto-renewal** is predictive of churn, but works mainly as a proxy for engagement.  
- **Long inactivity gaps** are the strongest churn signal.  
- High engagement (listens, unique songs per day) correlates with retention.  

---

## Modeling
- **Baseline:** Logistic Regression → poor performance (AUC ≈ 0.42).  
- **Best Model:** XGBoost → strong performance (AUC ≈ 0.98, AP ≈ 0.79).  

**Top Features (XGBoost & SHAP):**  
- `last_gap_days`  
- `cancel_rate`  
- `auto_renew_rate`  
- `n_txns`  
- `avg_list_price`, `total_amount_paid`  

---

## Explainability (SHAP)
- **Auto-renewal** strongly decreases predicted churn risk.  
- **Long inactivity gaps** strongly increase churn risk.  
- SHAP plots highlight both **global churn drivers** and **individual-level explanations**.  

---

## Causal Insights
- **Question:** *Does auto-renewal itself reduce churn, or is it just a proxy for user behavior?*  
- **Local Effect (IPW):** Auto-renew associated with ~26 pp lower churn in overlap region.  
- **Mediation Analysis:** Engagement drives retention; auto-renew is not a causal lever.  
- **Conclusion:** Engagement is the true causal driver → actionable lever for retention.  

---

## Experimentation (A/B Testing Simulation)
To demonstrate experimentation skills, we simulate a **retention coupon experiment**:  

- **Randomization:** Deterministic hashing at user level (`msno`).  
- **SRM check:** No sample ratio mismatch (50/50 split confirmed).  
- **Covariate balance:** Groups balanced on pre-period features (`last_gap_days`, `cancel_rate`, `n_txns`, etc.).  
- **Outcome difference:** Renewal rate lift ≈ +0.01 pp (95% CI crosses 0 → inconclusive).  
- **CUPED adjustment:** Used `last_gap_days` as covariate, reduced variance by ~8%.  
- **Interpretation:** No significant treatment effect (as expected, since no actual coupon applied). CUPED demonstrated variance reduction in practice.  

---

## Business Recommendations
- Focus on **increasing engagement** (shorter listening gaps, frequent plays, personalized playlists).  
- Use churn prediction to **flag at-risk users early** and target them with interventions.  
- **Experimentation** should validate interventions (e.g., coupons, trials) with proper randomization, guardrails, and variance reduction.  
- Auto-renew is predictive but not causal; retention must be driven through **behavioral levers**.  

---

## 📂 Repository Structure
```
kkbox-churn-prediction/
│
├── 01_data_preparation.ipynb
├── 02_exploratory_data_analysis.ipynb
├── 03_churn_prediction_modeling.ipynb
├── 04_causal_insights.ipynb
├── 05_ab_testing_retention.ipynb
└── README.md
```

