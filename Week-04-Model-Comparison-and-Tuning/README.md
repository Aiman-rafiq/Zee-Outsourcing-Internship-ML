# Week 4 – Compare, Cross-Validate and Tune Models

## Overview

This assignment focuses on comparing different classification models using 5-Fold Cross-Validation, performing hyperparameter tuning, checking overfitting, and evaluating the final selected model.

Four machine learning algorithms were implemented and compared using the Student Performance Factors dataset.

## Dataset

- **Dataset:** Student Performance Factors
- **Source:** [Kaggle – Student Performance Factors](https://www.kaggle.com/datasets/lainguyn123/student-performance-factors)
- **Total Records:** 6,607
- **Original Features:** 20

### Target Variable

A categorical target variable named `Needs_Support` was created using `Exam_Score`.

- `0` – No Support (Exam_Score ≥ 65)
- `1` – Needs Support (Exam_Score < 65)

The `Exam_Score` column was excluded from the input features to prevent target leakage.

## Data Preparation

The following preprocessing steps were performed:

- Checked and handled missing values.
- Checked duplicate records.
- Created two additional features:
  - `Study_Attendance_Interaction`
  - `Study_Sleep_Ratio`
- Applied median imputation to numerical features.
- Applied most-frequent imputation and One-Hot Encoding to categorical features.
- Applied StandardScaler to the KNN pipeline.
- Split the dataset into 80% training and 20% testing sets using `random_state=42` and stratification.

## Models Implemented

The following classification models were evaluated:

1. K-Nearest Neighbors (KNN)
2. Decision Tree
3. Random Forest
4. Gradient Boosting

Five-fold cross-validation was used to compare their performance.

## Initial Model Comparison

| Model | Mean CV Accuracy | Standard Deviation |
|---|---:|---:|
| KNN | 83.75% | 0.26% |
| Decision Tree | 87.15% | 1.01% |
| Random Forest | 91.45% | 0.56% |
| Gradient Boosting | 94.29% | 0.33% |

## Hyperparameter Tuning

The following hyperparameters were tested:

| Model | Best Parameters | Best CV Accuracy |
|---|---|---:|
| KNN | K = 9 | 84.12% |
| Decision Tree | max_depth = 10 | 87.44% |
| Random Forest | n_estimators = 200, max_depth = None | 91.77% |
| Gradient Boosting | n_estimators = 200, learning_rate = 0.2 | 95.52% |

GridSearchCV was used for Random Forest and Gradient Boosting.

## Overfitting Analysis

Training accuracy was compared with cross-validation accuracy to examine generalization gaps.

| Model | Training Score | CV Score | Gap |
|---|---:|---:|---:|
| KNN | 88.06% | 84.12% | 3.94% |
| Decision Tree | 98.26% | 87.44% | 10.82% |
| Random Forest | 100% | 91.77% | 8.23% |
| Gradient Boosting | 99.51% | 95.52% | 3.99% |

Decision Tree showed the largest generalization gap, while Gradient Boosting achieved the highest cross-validation accuracy with a relatively small gap.

## Final Model Evaluation

**Selected Model:** Gradient Boosting

- Best CV Accuracy: 95.52%
- Test Accuracy: 95.23%
- Precision (Needs Support): 94%
- Recall (Needs Support): 84%
- F1-score (Needs Support): 89%

### Confusion Matrix

| | Predicted No Support | Predicted Needs Support |
|---|---:|---:|
| Actual No Support | 1016 | 15 |
| Actual Needs Support | 48 | 243 |

Gradient Boosting was selected because it achieved the highest cross-validation accuracy and maintained strong performance on the unseen test dataset.

## Repository Contents

- `Week-04-Model-Comparison-and-Tuning.ipynb` – Complete implementation and analysis.
- `Week4_Assignment_Report.docx` – Detailed assignment report.
- `requirements.txt` – Required Python libraries.

## Technologies Used

- Python
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
- Kaggle Notebook

## Conclusion

This assignment provided practical experience in model comparison, cross-validation, hyperparameter tuning, overfitting analysis, and model evaluation.

Gradient Boosting achieved the best overall performance with a test accuracy of 95.23%.

**Note:** The `Needs_Support` target is an assignment-defined category based on an exam score threshold of 65. It does not independently establish a student's actual need for support.
