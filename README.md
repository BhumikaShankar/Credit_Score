# Wallet Risk Scoring From Scratch

This project analyzes the on-chain behavior of 100 wallets interacting with the **Compound V2/V3** DeFi protocol and assigns each a **credit score (0–1000)**.

---

##  Objective

To create a **risk score** for each wallet using only **on-chain transaction data**, without using machine learning prediction models. The goal is to:

- Identify good vs risky wallets


---

##  Data

We used:

- **Compound protocol (V2 and V3)** transaction data
- On-chain transaction history of **100 wallet addresses**

Each wallet's transaction history includes:

- Transfer amounts
- Gas prices
- Active days
- Counterparty wallet interactions

---

## Features Extracted

Below are the features created from raw data for each wallet:

| Feature | Description |
|--------|-------------|
| `txn_count` | Total number of transactions |
| `total_value` | Total ETH/token value moved |
| `avg_value` | Average value per transaction |
| `unique_counterparties` | Number of unique addresses interacted with |
| `avg_gas_price` | Mean gas price used |
| `active_days` | Number of unique active days |
| `txn_per_day` | Transactions per day = txn_count / active_days |

---

##  Risk Scoring Logic

We used **KMeans Clustering** to group similar wallets and assign scores.

###  Approach Used:

1. Applied **KMeans clustering** (with `k=3`) to the feature set.
2. Based on the cluster behavior:
   -  **Cluster 2** → High activity → Credit Score: **700–1000**
   -  **Cluster 1** → Medium activity → Credit Score: **400–600**
   -  **Cluster 0** → Low activity → Credit Score: **200–400**
3. Assigned a score to each wallet using a formula based on its cluster and scaled performance.

---

##  Output

A CSV file containing:

- `wallet_id`
- Extracted behavioral features
- Cluster label
- Final `credit_score` between 0 and 1000

---



## 🛠️ Tech Stack

- `Python`
- `pandas`, `numpy`
- `scikit-learn` (for clustering)
- `matplotlib`, `seaborn` (for visualization)

---
