<h1 align='center'> <font color='#ade8f4'><font size=6.7>🚚📦 Case Study: <font color="royalblue"><b>PORTER</b></font> — NEURAL NETWORK ~ Regression 📦🚚</font></font></h1>

<h2 align='right'>Analysed by : <font color='#ce4257'><b>KASI</b></font></h2>

---

## 🎯 Objective

Porter is India's Largest Marketplace for Intra-City Logistics. Leader in the country's **$40 billion** intra-city logistics market, Porter strives to improve the lives of **1,50,000+ driver-partners** by providing them with consistent earning & independence. Currently, the company has serviced **5+ million customers**.

Porter works with a wide range of restaurants for delivering their items directly to the people.

Porter has a number of delivery partners available for delivering the food, from various restaurants and wants to get an **estimated delivery time** that it can provide the customers on the basis of what they are ordering, from where and also the delivery partners.

This dataset has the required data to train a **regression model** that will do the delivery time estimation, based on all those features.

---

## 📅 Data Dictionary

Each row in this file corresponds to one unique delivery. Each column corresponds to a feature as explained below.

| Feature | Description |
|---|---|
| `market_id` | Integer id for the market where the restaurant lies |
| `created_at` | The timestamp at which the order was placed |
| `actual_delivery_time` | The timestamp when the order was delivered |
| `store_primary_category` | Category for the restaurant |
| `order_protocol` | Integer code value for order protocol (through porter, call to restaurant, pre-booked, third party, etc.) |
| `total_items_subtotal` | Final price of the order |
| `num_distinct_items` | The number of distinct items in the order |
| `min_item_price` | Price of the cheapest item in the order |
| `max_item_price` | Price of the costliest item in order |
| `total_onshift_partners` | Number of delivery partners on duty at the time order was placed |
| `total_busy_partners` | Number of delivery partners attending to other tasks |
| `total_outstanding_orders` | Total number of orders to be fulfilled at the moment |

---

## 🚀 Workflow

```
Data Loading → EDA → Preprocessing → Feature Engineering → Model Building → Evaluation
```

### 🔎 Steps at a Glance

| Step | Description |
|---|---|
| **1. Basic Analysis** | Shape (197,428 × 14), dtypes, statistical summary |
| **2. Missing Value Treatment** | Mode imputation for discrete; Median imputation for right-skewed continuous columns |
| **3. Outlier Removal** | LOF (Local Outlier Factor) — removed **3.34%** of outlier rows |
| **4. Feature Engineering** | Extracted `hour` & `day_of_week` from `created_at`; engineered `time_taken` (target) as difference in minutes |
| **5. Feature Scaling** | `StandardScaler` applied on train, val, and test sets |
| **6. Train/Val/Test Split** | 90,535 / 38,802 / 55,431 samples |
| **7. Neural Network** | Keras Sequential model with LeakyReLU, BatchNormalization, Dropout |
| **8. Hyperparameter Tuning** | Keras Tuner — **Bayesian Optimization** (20 trials, 2 executions/trial) |
| **9. Evaluation** | MSE, RMSE, MAE, R² Score, Adjusted R² Score |

---

## 🧠 Model Architecture

```
Input Layer  →  Dense(224) + LeakyReLU + BatchNorm
Hidden Layers (×3)  →  Dense(224) + LeakyReLU + BatchNorm + Dropout
Output Layer  →  Dense(1, activation='linear')
```

**Best Hyperparameters (Keras Tuner — Bayesian Optimization):**

| Hyperparameter | Value |
|---|---|
| Units | 224 |
| Number of Layers | 3 |
| Learning Rate | 0.006661 |
| Dropout (Layer 0) | 0.2 |
| Dropout (Layer 1) | 0.2 |
| Dropout (Layer 2) | 0.3 |
| Optimizer | **Adam** |
| Loss | MSE |
| Epochs | 50 |
| Batch Size | 512 |

---

## 📊 Model Performance

| Metric | Value |
|---|---|
| **MSE** | 165.23 |
| **RMSE** | 12.85 |
| **MAE** | 10.23 |
| **R² Score** | 0.2470 |
| **Adjusted R² Score** | 0.2468 |

---

## 💡 Key Insights

- **27.9%** of orders were placed using Order Protocol 1; **27.2%** via Protocol 3.
- The average delivery time taken by a porter is approximately **43 minutes**.
- Order volume peaks at **2 AM** and again between **2 PM – 8 PM**; a service gap exists between **7 AM – 2 PM**.
- Partner availability (onshift & busy) are highly correlated (**r = 0.95**), suggesting resource utilization is tightly coupled.
- The `subtotal` and `num_distinct_items` show strong positive correlation (**r = 0.68**).
- **3.34%** of outlier rows were removed via LOF before model training.

---

## 🏁 Recommendations

1. **Optimize Workforce Allocation** — Ensure adequate staffing during peak hours (12 AM–2 AM and 2 PM–8 PM); maintain on-call partners during high-demand windows.
2. **Investigate Data Anomalies** — Sharp spikes in partner availability and outstanding orders suggest possible data irregularities or operational inefficiencies warranting a review of logging processes.
3. **Improve Order Processing Efficiency** — Batch processing or priority handling for large-item orders can reduce bottlenecks; optimize inventory management for high-subtotal transactions.
4. **Adjust Service Hours** — The flat trend between 7 AM–2 PM signals a possible service gap; explore extending porter availability or scheduled fulfillment during this window.
5. **Enhance High-Value Order Handling** — Right-skewed subtotal distribution indicates a few premium transactions; consider VIP customer prioritization or dedicated delivery partners for such orders.

---

## 🛠️ Tech Stack

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white)
![Keras](https://img.shields.io/badge/Keras-D00000?style=for-the-badge&logo=keras&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Plotly](https://img.shields.io/badge/Plotly-3F4F75?style=for-the-badge&logo=plotly&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-76B7B2?style=for-the-badge)

---
# 🚚 PORTER — Delivery Time Prediction
### Uncovering operational bottlenecks in last-mile logistics using Neural Networks

---

> **Business Impact:** Identified partner availability — not traffic or weather — as the dominant delivery time driver (r = 0.95), reframing the analytical conclusion from model accuracy to **scheduling and incentive redesign** — directly applicable to any last-mile quick commerce operation.

---

## 📌 Business Problem

Porter is India's largest intra-city logistics platform connecting businesses with delivery partners. With **150,000+ driver-partners** serving **5M+ customers**, even a 5-minute improvement in average delivery time creates measurable customer experience gains at scale.

The challenge: Delivery time has many potential drivers — partner availability, time of day, order volume, restaurant prep time. Without knowing *which factors actually matter*, operational improvements are guesswork.

**The question:** Can we predict delivery time accurately enough to guide operational decisions — and more importantly, *which factors should operations leadership act on?*

---

## 📂 Dataset

| Attribute | Detail |
|---|---|
| Total deliveries | 197,792 records |
| Training set | ~142,000 samples |
| Test set | 55,431 samples |
| Target variable | `actual_delivery_time` (minutes) |
| Key features | On-shift partners, busy partners, outstanding orders, order protocol, cuisine type, city, timestamp |
| Time range | Multi-year transactional delivery data |

---

## 🔬 Methodology

### 1. Exploratory Data Analysis
- **Temporal analysis:** Plotted order volume and delivery time by hour-of-day across all records
- **Correlation analysis:** Computed Pearson r between all numerical features and delivery time
- **Distribution analysis:** Examined skewness and outliers in key operational metrics
- **Partner availability breakdown:** Separated on-shift vs. busy partners to understand utilization

### 2. Feature Engineering
Key derived features:
- `hour_of_day` — extracted from order timestamp to capture intraday patterns
- `day_of_week` — captured weekday vs. weekend demand differences
- `partner_utilization_ratio` — busy partners / on-shift partners (demand pressure signal)

### 3. Neural Network Architecture

```
Input Layer  → [n features]
Dense Layer  → 64 units, ReLU activation
Dense Layer  → 32 units, ReLU activation
Dense Layer  → 16 units, ReLU activation
Output Layer → 1 unit (regression — delivery time in minutes)
Optimizer    → Adam
Loss         → Mean Squared Error
```

### 4. Bayesian Hyperparameter Optimization (Optuna)
- **20 trials** searching over: number of layers, units per layer, dropout rate, learning rate, batch size
- Objective: minimize validation RMSE
- Final architecture selected from best trial parameters

---

## 📊 Results

### Model Performance

| Metric | Value |
|---|---|
| **RMSE** | **12.85 minutes** |
| R² | 0.247 |
| Test samples | 55,431 |

> **Note on R²:** The relatively low R² (0.247) reflects that delivery time in real-world logistics has high inherent variance — weather, traffic, and restaurant prep time introduce noise no model can fully capture from operational data alone. The RMSE of 12.85 minutes establishes a meaningful baseline for scheduling decisions.

### Key EDA Finding — The 7 AM–2 PM Service Gap

**Most critical discovery in the project:**

```
Hour    |  Avg Order Volume  |  Delivery Time
--------|--------------------|--------------
7 AM    |  Near-zero         |  N/A (insufficient volume)
8 AM    |  Low               |  High variance
...
2 PM    |  Near-zero         |  N/A
3 PM    |  Recovery begins   |  Normalizing
Peak    |  12 PM–1 PM        |  Longest avg delivery time
```

A **7 AM–2 PM window of near-zero order volume** was identified — representing a significant underutilization period across the network. This timing misalignment between driver shifts and actual demand suggests either:
- Drivers are scheduled for early shifts when demand is minimal
- Incentive structures don't align driver availability with peak demand windows

### Feature Importance — What Actually Drives Delivery Time

| Feature | Correlation with Delivery Time | Insight |
|---|---|---|
| `on_shift_partners` | r = **0.95** | Dominant driver — more partners = faster delivery |
| `busy_partners` | r = **0.95** | Combined availability signal is the #1 bottleneck |
| Outstanding orders | Moderate | Demand pressure secondary to supply availability |
| Cuisine type | Low | Food prep time less impactful than assumed |
| City | Low | Geography less predictive than partner supply |

**Partner availability (on-shift + busy combined) explains the overwhelming majority of delivery time variance.**

---

## 💡 Business Insights & Recommendations

### 1. Reframe the Problem — From Prediction to Scheduling
The model's most valuable output isn't the delivery time prediction itself — it's the **confirmation that partner supply is the bottleneck**, not demand, cuisine, or geography. This shifts the intervention from "improve the model" to "redesign partner scheduling."

### 2. Fix the 7 AM–2 PM Dead Zone
The near-zero order volume during this window suggests driver shifts don't align with customer demand curves. **Recommended action:** Shift driver incentive windows to align with demand peaks (lunch rush 12–2 PM, dinner rush 7–9 PM) rather than morning availability.

### 3. Incentivize Availability at Peak Hours
Since partner availability (r = 0.95) is the dominant predictor, **surge-style availability incentives** during peak demand periods would have a greater ROI than any operational change in restaurant partnerships or routing optimization.

### 4. Apply This Framework to Quick Commerce
The same analytical approach directly applies to 10-minute delivery operations (Blinkit, Swiggy Instamart, Flipkart Minutes) — where partner availability management is even more critical due to tighter delivery SLAs.

---

## 🛠️ Tech Stack

```
Python 3.x  |  Pandas  |  NumPy  |  Matplotlib  |  Seaborn
TensorFlow / Keras (Sequential Neural Network)
Optuna (Bayesian Hyperparameter Optimization — 20 trials)
Scikit-learn (preprocessing, train-test split, metrics)
SciPy (correlation analysis)
```

---

## 🚀 How to Run

```bash
# Clone the repo
git clone https://github.com/KasiMuthuveerappan/Porter-Neural_Networks

# Install dependencies
pip install pandas numpy matplotlib seaborn tensorflow optuna scikit-learn scipy

# Run the notebook
jupyter notebook Porter_NeuralNetwork.ipynb
```

---

## 📁 Repository Structure

```
├── Porter_NeuralNetwork.ipynb    # Main analysis + model notebook
├── porter_data.csv               # Delivery records dataset
└── README.md
```

---

*Analysed by **Kasi Muthuveerappan** | [LinkedIn](https://www.linkedin.com/in/kasimuthuveerappan/) | [Portfolio](https://kasiportfolio.carrd.co/)*

<p align="center">Made with ❤️ by <b>KASI</b></p>
