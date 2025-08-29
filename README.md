# 🎵 Subscription Retention Analysis & Churn Prediction (KKBox)

This project explores **subscription retention and churn prediction** using the KKBox dataset.  
It demonstrates the **end-to-end data science workflow**: data preparation, feature engineering, exploratory analysis, predictive modeling, model interpretability, and causal inference.  

The goal is to **identify at-risk users** and provide **actionable insights** for improving customer retention strategies.

---

## 📌 Project Workflow
1. **Data Understanding** – Explore users, transactions, and activity logs.  
2. **Data Preparation** – Clean and engineer features for churn modeling.  
3. **Exploratory Data Analysis (EDA)** – Identify patterns linked with churn.  
4. **Predictive Modeling** – Train and evaluate models (Logistic Regression, XGBoost).  
5. **Model Explainability** – Use SHAP values to interpret predictions.  
6. **Causal Insights & Simulation** – Explore retention drivers and simulate interventions.  
7. **Conclusions & Recommendations** – Translate results into business insights.  

---

## 📊 Dataset
- **Source**: [KKBox Churn Prediction Challenge (Kaggle)](https://www.kaggle.com/c/kkbox-churn-prediction-challenge)  
- **Key Tables**:  
  - `train.csv` – Labels (churned or not).  
  - `members.csv` – Demographic details (gender, registration date, etc.).  
  - `transactions.csv` – Subscription payments, renewals, cancellations.  
  - `user_logs.csv` – Daily listening activity (play counts, listening time).  

---

## 🔍 Key Insights (EDA)
- Users with **shorter plans (<1 month)** churn more often.  
- **Auto-renewal** strongly reduces churn.  
- **Long inactivity gaps** are highly predictive of churn.  
- High engagement (listens, unique songs per day) is correlated with retention.  

---

## 🤖 Modeling
- **Baseline:** Logistic Regression → poor performance (AUC ≈ 0.42).  
- **Best Model:** XGBoost → strong performance (AUC ≈ 0.98, AP ≈ 0.79).  

📈 **Feature Importance (XGBoost):**
- `auto_renew_rate`  
- `last_gap_days`  
- `cancel_rate`  
- `n_txns` (number of transactions)  
- `avg_list_price`, `total_amount_paid`  

---

## 🧩 Explainability (SHAP)
- **Auto-renewal** sharply decreases churn probability.  
- **Longer inactivity gaps** strongly increase churn risk.  
- SHAP plots highlight **individual predictions** and **global drivers** of churn.  

---

## 🚀 How to Run
1. Clone the repo:
   ```bash
   git clone https://github.com/your-username/kkbox-churn-prediction.git
   cd kkbox-churn-prediction
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Run the notebooks in order:
   - `01_data_preparation.ipynb` → Cleaning & feature engineering  
   - `02_exploratory_data_analysis.ipynb` → EDA & visualization  
   - `03_churn_prediction_modeling.ipynb` → Predictive models (LogReg, XGBoost)  
   - `04_causal_insights.ipynb` → Causal analysis (Local Effect, Mediation)  
   - `05_wrapup_summary.ipynb` → Project summary & insights  

---

## 🎯 Causal Insights (beyond prediction)

- **Question asked:** *Does auto-renewal itself prevent churn, or is it just a proxy for engagement?*  
- **Local Effect Analysis (IPW):** Auto-renew reduces churn in the overlap region (~26 pp).  
- **Mediation Analysis:** Engagement directly reduces churn; auto-renew does not mediate this effect.  
- **Conclusion:** Auto-renew is predictive but not causal; true actionable levers are engagement drivers (activity gaps, listening frequency).  

---

## 📌 Business Recommendations
- Focus on **increasing engagement** (shorter listening gaps, frequent plays) rather than relying solely on billing settings.  
- Use churn prediction models to **flag at-risk users early**, but follow up with **engagement-focused interventions** (playlists, recommendations, discounts).  
- Auto-renew is useful administratively, but **retention strategy must target behavior**.  

---

## 📂 Repository Structure
```
kkbox-churn-prediction/
│
├── 01_data_preparation.ipynb
├── 02_exploratory_data_analysis.ipynb
├── 03_churn_prediction_modeling.ipynb
├── 04_causal_insights.ipynb
├── requirements.txt
└── README.md
```

