# Online-Shopper-Purchase-Intent

## Project Overview
This project predicts whether an online shopping session will result in a purchase (`Revenue = True`) using user behavior and session-level information.

The objective is to identify potential purchasers based on browsing patterns, which can support targeted marketing, personalization, and conversion optimization.

---

## Dataset
The analysis uses the **Online Shoppers Purchasing Intention** dataset, which contains aggregated session data collected from an e-commerce website.

### Target Variable
- **Revenue** (True / False)

### Feature Types
- **Numerical features**
  - Page interaction counts
  - Session durations
  - Bounce rates and exit rates
  - Page values

- **Categorical features**
  - Month
  - Visitor type
  - Browser
  - Operating system
  - Region
  - Traffic type
  - Weekend indicator

The dataset is imbalanced, with purchasing sessions representing a smaller portion of the data.

---

## Data Preprocessing
To ensure reproducibility and prevent data leakage, all preprocessing steps were implemented using scikit-learn pipelines.

### Numerical Features
- Missing values imputed using the **median**
- Standard scaling applied

### Categorical Features
- Missing values imputed using the **most frequent category**
- One-hot encoding applied with safe handling of unseen categories

A **stratified train–test split** was used to preserve the target class distribution.

---

## Modeling Approach
Three classification models were trained and compared:

- **Logistic Regression**  
  Used as a baseline model to establish reference performance.

- **Decision Tree**  
  Included as an interpretable, rule-based model for comparison.

- **Random Forest**  
  Used to capture non-linear relationships and interactions between features.

All models shared the same preprocessing pipeline and were evaluated on the same test set.

---

## Evaluation Metrics
Because purchase events are relatively rare, models were evaluated primarily using **PR-AUC (Average Precision)**.

ROC-AUC and accuracy were also reported for reference, but were not used as the main selection criteria.

---

## Results

| Model | Accuracy | ROC-AUC | PR-AUC |
|------|----------|---------|--------|
| Random Forest | 0.888 | 0.909 | **0.727** |
| Decision Tree | 0.897 | 0.907 | 0.674 |
| Logistic Regression | 0.881 | 0.883 | 0.619 |

---

## Final Model Selection
**Random Forest** was selected as the final model based on its superior PR-AUC performance.

While the Decision Tree achieved slightly higher accuracy, Random Forest demonstrated stronger precision–recall performance, which is more appropriate for this imbalanced classification problem where identifying potential purchasers is the primary goal.

---

## Feature Importance
Feature importance analysis from the Random Forest model indicates that user behavior plays a major role in predicting purchase intent.

Key observations include:
- **PageValues** was the most influential feature
- Exit behavior and product-related page interactions were strong predictors
- Visitor type and seasonal effects also contributed meaningfully

These results align with real-world expectations that deeper engagement with high-value pages increases the likelihood of conversion.

---

## Repository Structure
```text
online-shopper-purchase-intent/
├── notebooks/
│   └── online-shopper-purchase-intent.ipynb
├── images/
│   ├── target_distribution.png
│   ├── cm_random_forest.png
│   ├── roc_random_forest.png
│   ├── pr_random_forest.png
│   └── feature_importance.png
├── requirements.txt
└── README.md
```

## Key Takeaways
- Metric selection is critical when working with imbalanced datasets
- Behavioral features provide strong signals for predicting purchase intent
- Random Forest effectively captures complex user behavior patterns in this context

---

## Tools & Libraries
- Python
- pandas, numpy
- scikit-learn
- matplotlib, seaborn

---

## Notes
This project emphasizes clean preprocessing pipelines, appropriate evaluation metrics, and clear model selection criteria suitable for real-world classification tasks.
