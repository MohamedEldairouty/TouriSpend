<p align="center">
  <img src="assets/logo 1.png" alt="TouriSpend Logo" width="180"/>
</p>

# 🧳 TouriSpend – Predicting Tourism Spend in Tanzania 🇹🇿

> A machine learning solution for forecasting tourist spending using real-world data provided by Zindi.

---

## 📌 Introduction

**TouriSpend** aims to predict how much a tourist will spend when visiting Tanzania, based on personal, behavioral, and trip-related features. Our model leverages gradient boosting (CatBoost) and thorough preprocessing to achieve competitive results.

---

## 🎯 Motivation & Objectives

Tourism is one of Tanzania's key economic sectors. Accurate cost prediction helps:
- The Ministry of Tourism better forecast revenue
- Businesses plan offers and logistics
- Improve tourist experience

Our goal: **Build a model with minimal error (MAE) on test data submitted to Zindi.**

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

## ⚙️ Data Preprocessing

✅ Handled:
- Missing values: imputed using mode (categoricals) and zeros (numericals)
- Clipping outliers: capped `total_cost` at 25 million
- Target transformation: `log1p(total_cost)` to reduce skewness
- Feature engineering:
  - Ratios and interactions: `people_x_nights`, `people_x_mainland`, `nights_per_person`, etc.
  - Binary indicators: `has_spouse`, `has_children`, `solo_traveler`
  - Categorical simplification: `region` mapping from `country`
  - Target Encoding: `country_te`, `activity_te`, `payment_te`

---

## 📊 Data Exploration & Visualization

We analyzed the data before modeling using EDA techniques:

### 🔹 Target Distribution
- Raw total cost was heavily right-skewed
- Log-transformed version is nearly normal

<p float="left">
  <img src="assets/Histogram of Total Cost (Raw).png" width="360"/>
  <img src="assets/Histogram of log (Total Cost +1).png" width="360"/>
</p>

### 🔹 Feature Distributions

<p float="left">
  <img src="assets/Distribution of night mainland.png" width="270"/>
  <img src="assets/Distribution of night zanzibar.png" width="270"/>
  <img src="assets/Distribution of total female.png" width="270"/>
  <img src="assets/Distribution of total male.png" width="270"/>
</p>

### 🔹 Categorical Insights

<p float="left">
  <img src="assets/top categ in country.png" width="280"/>
  <img src="assets/top categ in age group.png" width="280"/>
  <img src="assets/top categ in main_activity.png" width="280"/>
  <img src="assets/top categ in info source.png" width="280"/>
  <img src="assets/top categ in purpose.png" width="280"/>
  <img src="assets/top categ in travel with.png" width="280"/>
  <img src="assets/top categ in payment mode.png" width="280"/>
</p>

---

## 🧬 PCA Analysis

To understand the feature space:

### 🔹 Cumulative Explained Variance

<img src="assets/comulative explained variance.png" width="480"/>

➡️ **95% variance** was retained with 10 components.

### 🔹 PCA Projection (2D)

<img src="assets/pca projection.png" width="400"/>

This helped us visually assess how quantiles of `log_total_cost` spread across feature space.

---

## 📈 Feature Relationships

We visualized key scatter plots between target and engineered features:

<p float="left">
  <img src="assets/log total cost vs night mainland.png" width="300"/>
  <img src="assets/log total cost vs night zanzibar.png" width="300"/>
  <img src="assets/log total cost vs total female.png" width="300"/>
  <img src="assets/log total cost vs total male.png" width="300"/>
  <img src="assets/log total cost vs nights per person.png" width="300"/>
  <img src="assets/log total cost vs people x nights.png" width="300"/>
</p>

---

## 🤖 Model Implementation

✅ We used:
- **CatBoostRegressor** with `Quantile:alpha=0.6` loss for robustness
- StratifiedKFold (5-fold) based on cost bins using `pd.qcut`
- No log transform on features, only the target
- Post-inference clipping for stability

---

## 🧠 Final Model Settings

| Parameter         | Value              |
|------------------|--------------------|
| Model             | CatBoostRegressor  |
| Loss Function     | Quantile:alpha=0.6 |
| Depth             | 9                  |
| Learning Rate     | 0.022              |
| Iterations        | 1750               |
| L2 Leaf Reg       | 6                  |
| Subsample         | 0.85               |
| Early Stopping    | 100 rounds         |
| CV Strategy       | StratifiedKFold (5-fold) on cost bins |
| Prediction Clipping | [50,000, 25,000,000] |

---

## 📈 Results

| Stage                 | MAE (Validation) |
|-----------------------|------------------|
| Raw baseline          | ~8.6M            |
| After preprocessing   | ~5.0M            |
| **Final CatBoost**    | **3.35M** |

🏆 **Zindi Leaderboard Rank:** **27th out of 302**          
📉 **Leaderboard Score (MAE):** **4,862,550.945**         
📈 **Percentile:** Top **8.9%**

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
- [x] EDA with Visualizations (see `assets/` folder and notebook)
- [x] PCA Explained Variance Analysis
- [x] Model Implementation (CatBoost with feature engineering)
- [x] Submission to Zindi
- [x] Structured Report (this README ✅)
- [x] Jupyter Notebook with all code and outputs

---

## 💻 How to Run

```bash
git clone https://github.com/MohamedEldairouty/TouriSpend.git 
cd TouriSpend
pip install -r requirements.txt
jupyter notebook notebooks/final_model.ipynb

```
---

<p align="center"> 🚀 Powered by CatBoost • Crafted with ❤️ by Team TouriSpend </p>
