# 🦾 The Apex Data Cleaner
### Meta PyTorch Hackathon 2026 | OpenEnv Track

![Python](https://img.shields.io/badge/Python-3.10-3776AB?style=for-the-badge&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-2.x-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-0.111-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.4-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white)

## 🎬 2-Minute Demo
**[▶ Watch the 2-Minute Architecture & UI Demo Here](LINK)**

---

## 🎯 The Mission

### Project Description
The **Apex Data Cleaner** is an interactive RL environment designed to simulate a Junior Data Engineer's workflow. It trains AI agents to ingest corrupted datasets and execute precise data wrangling operations until the data is machine-learning ready.

Instead of raw CSVs, the agent observes a structured JSON profile of the dataset. It then takes deterministic, Pydantic-enforced actions like `impute_mean` or `one_hot_encode`. The final score is tied directly to the predictive accuracy of a baseline model trained on the agent's output.

### Why This Matters
Data scientists often spend 80% of their time simply cleaning data. Autonomous data cleaning represents a major bottleneck in AI development. By forcing agents to understand column types, handle outliers, and ensure scikit-learn compatibility, we are providing a tool that tests true logical reasoning rather than just pattern matching.

---

## 🏗️ Architecture

The pipeline follows a strict flow: 
`Dirty CSV → JSON Profile → RL Agent → Pydantic Actions → Clean CSV → scikit-learn Grader → Reward`

### 1. Observation
The agent receives a structured JSON profile rather than the raw file. This includes metrics like row counts, null rates, and statistical distributions. This mimics how a human engineer assesses an unfamiliar file.

### 2. Action Space
The agent uses a discrete set of operations validated by Pydantic to prevent hallucinations or silent failures:
* **Numerical Imputation:** Using mean or median strategies.
* **Row Management:** Dropping rows based on specific null constraints.
* **Text Normalization:** Standardizing casing and stripping whitespace.
* **Outlier Control:** Clipping extreme values within specific bounds.
* **Feature Engineering:** Dropping irrelevant columns or applying one-hot encoding.

### 🏆 The Grader
Rewards are computed using a deterministic Random Forest classifier. If the agent's cleaning improves the model's accuracy on the target label (`Is_Profitable`), the reward increases. 
* **Perfect Clean:** ~90%+ accuracy (1.0 reward)
* **Partial Success:** ~60–80% accuracy (0.3 – 0.7 reward)
* **Degraded Data:** < 50% accuracy (0.0 reward)

---

## 📂 The Datasets

All tasks are derived from real-world startup funding and SaaS churn data, with three levels of synthetic corruption:

**Task: Easy**
A warm-up involving 5 missing values in the `Revenue_M` column. The agent simply needs to detect and impute these without affecting other features.

**Task: Medium**
A more realistic scenario with nulls spread across five numerical columns. Additionally, the `Industry` column contains inconsistent casing and typos (e.g., "SaaS " and "Fin Tech") that require normalization.

**Task: Hard**
Controlled chaos featuring extreme statistical outliers and a completely useless `JUNK_COL` filled with noise. This tests the agent’s ability to prune irrelevant features while simultaneously handling a 20% null rate across the entire dataset.

---

## ✅ Hackathon Rubric Assessment

* **Real-world utility:** Models a genuine tech workflow that provides daily value.
* **Grader quality:** Features a deterministic reward system tied directly to ML performance.
* **Environment design:** Uses Pydantic to ensure clean state transitions and zero hallucinations.
* **Creativity:** Tying RL rewards to downstream Auto-ML readiness offers a novel approach to the track.

---

## 💻 Local Installation

```bash
# Installation steps will be finalized upon backend completion.
