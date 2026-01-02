# 🚚 Self-Correcting Logistics AI: The "Trifecta" Engine

> **Automated Workforce Planning for High-Volatility Logistics Markets (Nigeria)**

## 📖 The Problem
"How many riders do we need tomorrow?"

In dynamic markets like Lagos, using simple averages for workforce planning fails. 
- **Rainy days** spike no-show rates.
- **Traffic jams** destroy efficiency (drops per hour).
- **Payday surges** break static models.

This project moves beyond averages. It uses a **Cascading XGBoost Architecture** to predict:
1. **Demand:** How many orders will we get?
2. **Efficiency (UTR):** How fast can riders deliver *given that volume*?
3. **Reliability:** How many riders will actually show up?

---

## 🧠 The Architecture
The system is built on three interconnected models ("The Trifecta"):

### 1. Demand Engine (Volume)
* **Algorithm:** XGBoost Regressor
* **Features:** Lagged demand (1d, 1w), Momentum ratios, Payday flags.
* **Performance:** ~5% WAPE (Weighted Absolute Percentage Error).

### 2. Dynamic Efficiency Model (The "Physics" Engine)
* **Insight:** Efficiency is not static. High volume creates density, which increases speed (up to a point).
* **Mechanism:** Takes the *predicted volume* from Layer 1 to forecast the specific Drops Per Hour (UTR) for that zone.
* **Constraint:** Clamps predictions between 0.1 and 4.0 UTR to match physical reality.

### 3. Reliability Buffer (No-Show Prediction)
* **Problem:** A perfect plan fails if riders don't log in.
* **Features:** Weather forecasts (rain), Seasonality, Day of Week.
* **Output:** Generates a dynamic safety buffer (e.g., recommends 5% more shifts on rainy Fridays).

---

## 📊 Results & Visualization

### The "Volume Curve" (Physics Check)
*The model learned that riders become more efficient as order volume increases (Blue Line), aligning with actual historical data (Gray Dots).*
![Volume Curve](outputs/volume_curve.jpg)

### Network-Wide Accuracy
*The AI (Dashed Line) correctly tracks the actual required capacity (Solid Line), automatically accounting for "Shadow Capacity" during surges.*
![Network Accuracy](outputs/network_actual_vs_pred.jpg)

---

## 🛠️ How to Run

1. **Install Dependencies**
   ```bash
   pip install -r requirements.txt