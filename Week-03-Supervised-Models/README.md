
# Week 03 - Supervised Machine Learning Models

## Dataset
**Name:** Student Performance Factors

**Source:** [Kaggle Dataset](https://www.kaggle.com/datasets/lainguyn123/student-performance-factors)

**Records:** 6,607

**Target:** Needs_Support (Binary Classification)

## Project Summary
This project compares KNN, Decision Tree, and Logistic Regression for identifying students who may need academic support.
The dataset was cleaned, encoded, scaled, and divided into training and testing sets.
Models were evaluated using accuracy, precision, recall, F1-score, and confusion matrices.

## Model Results

| Model | Test Accuracy |
|---|---|
| KNN (K=7) | 87.97% |
| Decision Tree (Depth=10) | 86.99% |
| Logistic Regression | 98.26% |

**Best Model:** Logistic Regression

**Best Model Accuracy:** 98.26%

## How to Run
1. Open the notebook in Kaggle.
2. Attach the Student Performance Factors dataset linked above.
3. Run all notebook cells in order.
4. Review the model evaluations and comparison.

## Requirements
Install the dependencies listed in requirements.txt.

## Note
Needs_Support is a project-defined label based on Exam_Score below 65. The original Exam_Score is excluded from model inputs to prevent target leakage.
