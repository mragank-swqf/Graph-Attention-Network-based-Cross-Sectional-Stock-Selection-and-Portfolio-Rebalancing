# Graph Attention Network–Based Cross-Sectional Stock Selection and Portfolio Rebalancing 📈

## Overview
This project implements an **end-to-end framework for cross-sectional stock selection and portfolio rebalancing** using **Graph Attention Networks (GATs)**.  
The goal is to model **inter-stock relationships** and leverage cross-asset information to improve **directional prediction** and **portfolio-level performance**.

The pipeline integrates:
- robust technical feature engineering,
- graph-based deep learning,
- extensive model training and tuning,
- and a systematic portfolio rebalancing strategy.

Performance is evaluated against a simple equal-weight benchmark portfolio.

---

## Methodology 🧠

### 1. Data and Universe
- **Equity universe:** 24 stocks  
- **Data frequency:** Daily data (used for monthly portfolio decisions)  
- **Problem setup:** Cross-sectional prediction of next-period relative performance  

Each stock is treated as a **node in a graph**, allowing the model to learn relationships across assets instead of modeling each stock independently.

---

### 2. Technical Feature Engineering
A comprehensive **technical analysis pipeline** is used to extract **12 technical indicators** per stock.  
These features capture trend, momentum, volatility, and price dynamics.

The feature set includes:
- **Moving Averages** (short-term and long-term)
- **MACD (Moving Average Convergence Divergence)**
- **RSI (Relative Strength Index)**
- **ROC (Rate of Change)**
- **Bollinger Bandwidth** (volatility measure)
- **Donchian Channel–based features**
- Additional normalized technical indicators

All features are **standardized using a Standard Scaler** to ensure stable and efficient training of the deep learning model.

---

### 3. Graph Construction
- Each stock is represented as a **node**
- Node features consist of the engineered technical indicators
- Graph structure captures cross-asset relationships

The data is formatted using **PyTorch Geometric**, where inputs are handled as graph objects rather than traditional tabular DataFrames.

---

### 4. Model Architecture
A **Graph Attention Network (GAT)** is used to learn cross-sectional representations.

Key characteristics:
- Attention-based message passing between stocks
- Adaptive weighting of inter-stock relationships
- End-to-end training on historical data

Multiple architectures and hyperparameter configurations were trained and evaluated.

---

### 5. Training and Evaluation
The model is trained to:
- predict **directional movement**, and
- capture **maximum variance** in cross-sectional returns.

Training involved:
- extensive hyperparameter tuning,
- monitoring training stability,
- analyzing performance across different epoch lengths to avoid overfitting.

Model selection was based on:
- directional accuracy,
- variance captured,
- and out-of-sample consistency.

---

### 6. Portfolio Construction and Rebalancing Strategy 💼
A **long-only monthly rebalancing strategy** is implemented:

1. At each rebalance date, the GAT model ranks all 24 stocks.
2. The **top 12 predicted performers** are selected.
3. Capital is allocated **equally** across the selected stocks.
4. The portfolio is rebalanced every **21 trading days**.

---

### 7. Benchmark
The strategy is compared against a baseline:
- **Equal-weight buy-and-hold portfolio**
- Capital equally allocated across all 24 stocks
- No rebalancing

---

## Results 📊
The GAT-based strategy demonstrates consistent outperformance over the benchmark:

- **Validation (in-sample) alpha:** +5.28%
- **Test (out-of-sample) alpha:** +4.16%

These results indicate that modeling cross-asset relationships using graph-based deep learning can enhance portfolio-level performance.

---

## Project Structure 🗂️
├── notebook.ipynb # Main Jupyter notebook (data prep, modeling, evaluation)
├── README.md # Project documentation
├── .gitignore # Git ignore rules


> Note: Raw data and trained model checkpoints are not included due to size constraints.

---

## Limitations ⚠️
- Limited equity universe (24 stocks)
- Transaction costs and slippage are not modeled
- Strategy is long-only
- Results are based on historical backtesting and may not generalize across all market regimes

---

## Tools and Libraries 🛠️
- Python
- PyTorch
- PyTorch Geometric
- NumPy, Pandas
- Scikit-learn
- Matplotlib

---

## Disclaimer
This project is for **educational and research purposes only** and does not constitute financial or investment advice.

