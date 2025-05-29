<p align="center">
  <img src="assets/logo 1.png" alt="TouriSpend Logo" width="180"/>
</p>

# 🧳 TouriSpend – Predicting Tourism Spend in Tanzania 🇹🇿

> A machine learning solution for forecasting tourist spending using real-world data provided by Zindi.

---

## 📌 Introduction

**TouriSpend** aims to predict how much a tourist will spend when visiting Tanzania, based on personal, behavioral, and trip-related features. Our model leverages gradient boosting (CatBoost) and well-structured preprocessing to achieve robust performance.

---

## 🎯 Motivation & Objectives

Tourism is one of Tanzania's key economic sectors. Accurate cost prediction helps:
- The Ministry of Tourism better forecast revenue
- Businesses plan offers and logistics
- Improve tourist experience

Our goal: **Build a model with minimal error (MAE) on test data submitted to Zindi**.

---

## 🗂️ Dataset Description

The dataset includes:
- **Demographics** (country, age group, gender)
- **Trip details** (main activity, nights stayed, tour arrangement)
- **Costs** (target: total_cost)

Files used:
- `Train.csv`, `Test.csv`, `VariableDefinitions.csv`

---

## 📊 Evaluation Metric

The competition uses:

**📉 Mean Absolute Error (MAE)**  
MAE = (1/n) * Σ | yᵢ - ŷᵢ |

---

## ⚙️ Data Processing

✅ Handled:
- Missing values (mode for categoricals, 0 for numerics)
- Outliers (target clipped at 25M max)
- Feature interactions (e.g., `people_x_nights`, `purpose_x_activity`)
- Log-transformation of target: `log1p(total_cost)`

---

## 📊 Data Exploration (EDA)

🔍 We explored:
- Distributions of spend across country, activity, and age
- Relationships between nights stayed and cost
- Outlier distribution in target

📊 *(see `notebooks/final_model.ipynb` for visualizations)*

---

## 🤖 Model Implementation

✅ We used:
- **CatBoostRegressor** with `Quantile:alpha=0.6` loss for robustness against outliers
- StratifiedKFold based on cost quantiles
- Extensive feature engineering: binary flags, ratios, age × nights
- Early stopping + clipping for final output

---

## 📈 Results

| Stage                 | MAE (Validation) |
|-----------------------|------------------|
| Raw model             | ~8.6M            |
| After preprocessing   | ~5.0M            |
| Final CatBoost        | **~3.3M**        |

🏆 **Zindi Leaderboard Rank:** 41st out of 294  
📈 **Percentile:** Top **13.9%**

---

## 👥 Team TouriSpend Members

| Name                          | Registration No. |
|-------------------------------|------------------|
| [@Mohamed Abdallah Eldairouty](https://github.com/MohamedEldairouty)  | 221001719 |  
| [@Rimas Emad](https://github.com/rimaseldib)    | 221001067         | 
| Moaz Aly      | 221001970         | 
| Jasmine Ashraf | 221000990        | 

---

## 🚀 Project Deliverables Checklist

- [x] Data Processing (missing values, outliers, transforms)
- [x] Handle challenges (categorical explosion, cost skew)
- [x] Data Exploration (see notebook)
- [x] Model Implementation (CatBoost with preprocessing)
- [x] Structured Report (this README 🎯)
- [x] Code (in `/notebooks/`)
- [x] Predictions submitted to Zindi

---

## 📦 How to Run

```bash
git clone https://github.com/MohamedEldairouty/TouriSpend.git 
cd TouriSpend
pip install -r requirements.txt
jupyter notebook notebooks/final_model.ipynb
```
---

## 🏁 Final Notes
This project was developed as part of a Machine Learning competition hosted on Zindi. All work was completed by our team using open-source tools and documented clearly for reproducibility.

<p align="center"> 🚀 Powered by CatBoost • Crafted with ❤️ by Team TouriSpend </p>
