# Week 5 – Rare-Class Classification and Model Improvement

## Project Overview

This project focuses on improving a machine learning classification model when the dataset contains an imbalanced target variable.

The main objective was to identify why a model fails to detect minority-class examples, analyze its classification errors, experiment with different improvement strategies, and evaluate the final model using appropriate performance metrics.

The project uses the **Student Performance Factors** dataset and a Random Forest classifier to identify students belonging to a score-defined support category.

## Dataset

**Dataset:** [Student Performance Factors – Kaggle](https://www.kaggle.com/datasets/lainguyn123/student-performance-factors)

- Total records: 6,607
- Original features: 20
- Target variable: `Needs_Support`
- Missing values: 235
- Duplicate records: 0

### Target Variable

The target variable was created using `Exam_Score`:

| Class | Description | Records | Percentage |
|---|---|---:|---:|
| 0 | No Support (score ≥ 65) | 5,155 | 78.02% |
| 1 | Needs Support (score < 65) | 1,452 | 21.98% |

The `Exam_Score` column was excluded from the input features to prevent target leakage.

Two additional features were engineered:

- `Study_Attendance_Interaction`
- `Study_Sleep_Ratio`

## Project Workflow

The assignment was completed in the following stages:

### 1. Data Preparation
- Inspected missing values and duplicate records.
- Handled numerical missing values using median imputation.
- Handled categorical missing values using most frequent imputation.
- Applied One-Hot Encoding to categorical features.
- Analyzed target class distribution.
- Split the data into training and testing sets using stratification (80/20).

### 2. Baseline Model Evaluation

Two baseline models were evaluated:

- Dummy Classifier (`most_frequent`)
- Random Forest Classifier (default settings)

The baseline Random Forest achieved 91.45% accuracy in five-fold out-of-fold training predictions, but its minority-class Recall was only 69.51%.

It missed 354 minority-class cases, demonstrating why accuracy alone is not sufficient for an imbalanced classification problem.

### 3. Error Analysis

The model's predictions were analyzed to identify:

- True Positives
- True Negatives
- False Positives
- False Negatives

Numerical and categorical feature values were compared across prediction groups to identify patterns associated with classification errors.

### 4. Model Improvement Experiments

The following strategies were tested:

1. Class weight balancing using `class_weight="balanced"`.
2. Decision threshold tuning using 0.5, 0.4, 0.3, 0.2, and 0.1.
3. Random oversampling applied to training folds only.

Threshold tuning provided the strongest improvement in minority-class Recall.

### 5. Feature Importance and Selection

Random Forest feature importance was used to identify the most influential features.

The top three features were:

| Feature | Importance |
|---|---:|
| Attendance | 0.2304 |
| Study_Attendance_Interaction | 0.2108 |
| Hours_Studied | 0.0895 |

The five least important features were removed in a separate validation experiment. However, the reduced feature set performed worse, so all 21 features were retained.

### 6. Final Model Evaluation

The baseline and improved models were evaluated on the reserved test set.

| Metric | Baseline RF (0.5) | Improved RF (0.3) |
|---|---:|---:|
| Accuracy | 90.62% | 90.24% |
| Precision | 85.53% | 72.38% |
| Recall | 69.07% | 90.03% |
| F1-score | 76.43% | 80.25% |
| False Negatives | 90 | 29 |
| False Positives | 34 | 100 |

### Final Result

The improved Random Forest using a decision threshold of **0.3** achieved:

- **90.03% Recall** for the minority class.
- Reduced False Negatives from 90 to 29.
- Improved F1-score from 76.43% to 80.25%.

Although Precision decreased and False Positives increased, the improved model was selected because identifying more minority-class cases was the primary objective.

## Repository Structure

```text
week5-model-improvement/
│
├── week5_classification.ipynb
├── README.md
├── requirements.txt
│
├── report/
│   └── Week5_Assignment_Report.pdf
│
└── screenshots/
    ├── class_distribution.png
    ├── error_analysis.png
    ├── feature_importance.png
    └── final_results.png
```

## Installation and Usage

### Requirements

The project uses Python and the following libraries:

- pandas
- numpy
- matplotlib
- scikit-learn
- Jupyter Notebook

Install the dependencies using:

```bash
pip install -r requirements.txt
```

### Running the Notebook

1. Download or clone this repository.
2. Open `week5_classification.ipynb` in Jupyter Notebook or Kaggle.
3. Attach the Student Performance Factors dataset.
4. Run the notebook cells in order.

**Note:** The notebook uses Kaggle's input directory to locate the dataset. If running locally, update the dataset-loading cell to point to your local CSV file.

## Key Learning Outcomes

Through this assignment, I learned how to:

- Identify and handle class imbalance.
- Understand why accuracy can be misleading.
- Use Precision, Recall, and F1-score for minority-class evaluation.
- Perform false positive and false negative analysis.
- Improve classification performance through class weighting, threshold tuning, and oversampling.
- Interpret Random Forest feature importance.
- Compare model performance using validation data and an untouched test set.

## Limitations

The `Needs_Support` target is defined using an exam-score threshold of 65. It represents a score-based classification label, not an independently verified measure of a student's actual support needs.

The final model also introduces more false positives in exchange for fewer false negatives. This trade-off should be considered before any real-world use.

## Author

**Aiman**  
BS Software Engineering Student  
GitHub: [Aiman-rafiq](https://github.com/Aiman-rafiq)

---

*This project was completed as part of the Week 5 Machine Learning Internship Assignment.*
