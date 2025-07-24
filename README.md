# Annual Spending Prediction for E‑Commerce Customers

Predict a customer’s yearly spending based on their behaviour on an e‑commerce platform.  This repo contains the end‑to‑end workflow (data prep → feature selection → modelling → evaluation) implemented in a single, reproducible pipeline.

---

## 📊 Dataset

| Column (example)                            | Description                           |
| ------------------------------------------- | ------------------------------------- |
| `Avg_Session_Length`                        | Avg minutes per session on site       |
| `Time_on_App`                               | Total minutes spent on the mobile app |
| `Time_on_Website`                           | Total minutes on the desktop site     |
| `Length_of_Membership`                      | Years as a customer                   |
| *(… additional engineered or raw features)* |                                       |
| **Target → `Yearly_Amount_Spent`**          | USD a customer spends per year        |

Source: [https://www.kaggle.com/datasets/ejlok1/marketing‑data](https://www.kaggle.com/datasets/ejlok1/marketing‑data)

---

## 🧰 Environment

```bash
python 3.10+
scikit‑learn >= 1.4
pandas >= 2.2
numpy >= 1.25
matplotlib, seaborn  # optional for plots
```

Install everything with

```bash
pip install -r requirements.txt
```

---

## 🚀 Quick‑start (reproduce results)

```bash
# 1. Clone & cd
$ git clone <repo‑url>
$ cd annual‑spending‑prediction

# 2. Create env (optional)
$ python -m venv .venv && source .venv/bin/activate

# 3. Install deps
$ pip install -r requirements.txt

# 4. Run the notebook (Jupyter / VS Code) OR execute the pipeline directly
$ jupyter notebook notebooks/linear-reg.ipynb
# OR
$ python src/pipeline.py --train data/ecommerce_customers.csv --model artefacts/model.pkl
```

---

## 🧪 Modelling Highlights

* **Pre‑processing**: median imputation → standardisation.
* **Feature selection**: `RFECV` (step = 1, 5 folds × 3 repeats).
* **Final model**: Ordinary Least Squares on the selected subset.
* **Hold‑out results**

  | Metric                       | Score      |
  | ---------------------------- | ---------- |
  | RMSE                         | **≈ 9.02** |
  | baseline RMSE (predict mean) | 83.90      |
  | R²                           | **0.988**  |

The model reduces average error by ≈ **89 %** compared with a naïve mean predictor.

---

## 📈 Selected Features & Coefficients (scaled)

| Feature                | β (scaled) | Sign |
| ---------------------- | ---------: | :--: |
| `Time_on_App`          |      +0.84 |   ➚  |
| `Length_of_Membership` |      +0.62 |   ➚  |
| `Time_on_Website`      |      −0.12 |   ➘  |
| *(etc.)*               |            |      |

> *Values above are from the latest notebook run.  Coefficients may shift if you retrain on a different random split.*

---
