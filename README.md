# Red Wine Analysis — Discovering Wine Personalities

Clustering, Quality Prediction & Recommendation Engine on 1,599 Red Wines

---

## Overview

This project explores 1,599 red wines through a complete data science workflow — from cleaning and clustering to quality prediction and building a working recommendation engine.

It demonstrates how raw chemistry data can be turned into actionable business insights for a wine company:
- What "personalities" of wine exist in our portfolio?
- What chemistry makes a wine good?
- Can we predict wine quality automatically?
- Can we recommend wines based on customer preferences?

**Result:** Built a 90% accurate quality classifier, identified the top 3 quality drivers, segmented wines into 4 clear personality groups, and developed a working recommendation engine.

---

## Main Findings

### The 4 Wine Personalities (discovered via K-Means clustering)

| Cluster | Personality | Defining Traits | Avg Quality |
|---------|-------------|-----------------|-------------|
| 1 | Premium Reserve | High alcohol, low preservatives, clean taste | Highest |
| 2 | Smooth & Mellow | Low acidity, balanced, easy-drinking | Average |
| 3 | Tart & Fruity | High acidity, citric notes, refreshing | Average |
| 4 | Mass-Market Preserved | High sulfites, low alcohol | Lowest |

### Top Quality Drivers (from Random Forest)

| Rank | Feature | Effect on Quality |
|------|---------|-------------------|
| 1 | Alcohol | Higher alcohol → better wine |
| 2 | Volatile Acidity | Lower = better (high = vinegar taste) |
| 3 | Sulphates | Moderate amounts improve preservation |

### Key Insights

1. **Alcohol is the #1 quality predictor** — Premium wines consistently have higher alcohol content
2. **Volatile acidity is the #1 quality killer** — keep it low to avoid that vinegary taste
3. **Excessive sulfur dioxide signals cheap wine** — Premium Reserve wines have 24+ units less than mass-market wines
4. **Wine data is mostly homogeneous** — DBSCAN found no sharp natural divisions (one big blob with outliers)
5. **K-Means imposes useful structure** — even without natural clusters, segmentation helps marketing & strategy

**Practical takeaway:** To produce premium wine, focus on higher alcohol fermentation and minimize sulfite preservatives.

---

## Quick Start

### Prerequisites

- Python 3.10 or higher
- pip (Python package manager)
- Jupyter Notebook

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/Gautam-Santosh/Red-Wine-Analysis.git
cd Red-Wine-Analysis

# 2. Install dependencies
pip install -r requirements.txt

# 3. Launch Jupyter
jupyter notebook
```

Open `Red_Wine_Analysis.ipynb` and run all cells.

---

## Dataset

Wine Quality (Red Wine) dataset — 1,599 wines with 11 chemistry features and 1 quality score.

| Feature | Description |
|---------|-------------|
| fixed.acidity | Non-volatile acids (mostly tartaric) |
| volatile.acidity | Vinegar-like acids (high = bad taste) |
| citric.acid | Adds freshness |
| residual.sugar | Sweetness |
| chlorides | Saltiness |
| free.sulfur.dioxide | Active preservation chemical |
| total.sulfur.dioxide | Total preservatives |
| density | Denser = more sugar/alcohol |
| pH | Acidity level (low = sour) |
| sulphates | Preservation aid |
| alcohol | Alcohol percentage (8-15%) |
| quality | Expert score (3-8) — target variable |

### Sample Data

| alcohol | volatile.acidity | pH | sulphates | quality |
|--------:|-----------------:|---:|----------:|--------:|
| 9.4 | 0.70 | 3.51 | 0.56 | 5 |
| 9.8 | 0.88 | 3.20 | 0.68 | 5 |
| 11.4 | 0.42 | 3.30 | 0.74 | 7 |
| 12.5 | 0.32 | 3.40 | 0.82 | 8 |

---

## Workflow

### Analysis Pipeline

| Step | Action | Technique |
|------|--------|-----------|
| 1 | Load and explore | pandas |
| 2 | Drop ID column | pandas |
| 3 | Scale features (0-1) | MinMaxScaler |
| 4 | Reduce dimensions | PCA (11 → 2) |
| 5 | Find optimal K | Elbow method |
| 6 | Cluster wines | K-Means (K=4) |
| 7 | Detect outliers | DBSCAN |
| 8 | Profile clusters | groupby aggregations |
| 9 | Predict quality | Random Forest |
| 10 | Find quality drivers | Feature importance |
| 11 | Validate statistically | ANOVA test |
| 12 | Build recommender | Distance-based ML |
| 13 | Save deliverables | joblib + CSV |

---

## Techniques Used

### Unsupervised Learning
- **PCA** — compress 11 features into 2 visualizable components
- **K-Means** — partition wines into 4 chemistry-based groups
- **DBSCAN** — density-based clustering with outlier detection
- **Elbow method** — finding optimal cluster count

### Supervised Learning
- **Random Forest Classifier** — predict if a wine is "good" (quality ≥ 7)
- **Feature importance** — identify top quality drivers
- Train/test split with stratification

### Statistical Analysis
- Correlation analysis — find feature relationships
- ANOVA test — validate cluster differences statistically
- Descriptive statistics — cluster profiling

### Visualization
- Correlation heatmaps
- Cluster scatterplots
- Box plots for quality comparison
- Feature importance bar charts

---

## Results

### Wine Quality Classifier (Random Forest)

| Metric | Score |
|--------|------:|
| Accuracy | ~90% |
| ROC-AUC | ~0.85 |
| Precision (Good wines) | ~78% |

### Cluster Comparison (Average Quality)
