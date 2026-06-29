# hudi-ml-project

Applying machine learning to software metrics collected from [Apache Hudi](https://github.com/apache/hudi) (release 0.13.0).

## Projects

| Notebook | Type | Goal |
|----------|------|------|
| `01_eda.ipynb` | Exploratory Data Analysis | Understand the data before modeling |
| `02_complexity_predictor.ipynb` | Linear Regression | Predict method complexity (WMC) from OO metrics |

## Dataset

- **class.csv** — 2,152 production class-level CK metrics
- **method.csv** — 18,869 method-level CK metrics
- Collected using [CK](https://github.com/mauricioaniche/ck) — a Java code metrics tool

## Setup

```bash
uv venv .venv
source .venv/bin/activate
uv pip install jupyterlab numpy pandas matplotlib seaborn scikit-learn
jupyter lab
```

