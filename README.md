# hudi-ml-project

A practice project applying machine learning to real-world software engineering data.

Applies ML models to software metrics collected from [Apache Hudi](https://github.com/apache/hudi) (release 0.13.0).

## What this project does

This project trains two machine learning models on Java class and method metrics to answer two questions:

1. How complex is this method? (linear regression)
2. Is this class likely to contain a bug? (logistic regression)

## Dataset

- **class.csv**: 2,152 production class-level CK metrics
- **method.csv**: 18,869 method-level CK metrics
- Collected using [CK](https://github.com/mauricioaniche/ck)

### Features used

| Feature | Description |
|---------|-------------|
| `cbo` | Coupling Between Objects |
| `wmc` | Weighted Methods per Class |
| `rfc` | Response For a Class |
| `fanin` | Number of classes that depend on this class |
| `fanout` | Number of classes this class depends on |
| `dit` | Depth of Inheritance Tree |
| `loc` | Lines of Code |

## Model 1: Method Complexity Predictor (Linear Regression)

**Notebook:** `02_complexity_predictor.ipynb`

Predicts method complexity (`wmc`) from method-level metrics.

| Metric | Score |
|--------|-------|
| RMSE | 1.197 |
| MAE | 0.487 |
| R² | 0.696 |

The model explains ~70% of the variation in method complexity. It struggles with rare, highly complex methods due to the skewed nature of the data.

## Model 2: Defect Predictor (Logistic Regression)

**Notebook:** `03_defect_predictor.ipynb`

Predicts whether a Java class is buggy or clean. Labels were derived from commits between `release-0.13.0` and `release-0.14.0`. Any class touched by a bug fix commit was labeled buggy.

384 buggy classes, 1,768 clean classes (roughly 1:4.6 ratio).

| Metric | Clean | Buggy |
|--------|-------|-------|
| Precision | 0.89 | 0.34 |
| Recall | 0.75 | 0.57 |
| F1 | 0.82 | 0.42 |

Overall accuracy: 72%. The model catches 57% of buggy classes. Results are limited by the class imbalance and the noisy nature of git-derived labels.

## Setup

```bash
uv venv .venv
source .venv/bin/activate
uv pip install jupyterlab numpy pandas matplotlib seaborn scikit-learn
jupyter lab
```

Open the notebooks in order: `01_eda.ipynb`, `02_complexity_predictor.ipynb`, `03_defect_predictor.ipynb`
