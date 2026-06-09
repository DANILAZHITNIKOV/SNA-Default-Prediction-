# Corporate Default Prediction Using Social Network Analysis and GraphSAGE

This repository contains the final project for the Social Network Analysis course.

## Project idea

The project studies corporate default prediction using financial indicators, Social Network Analysis features, and graph machine learning.

The main research question is whether the position of a company in a corporate network improves the prediction of bankruptcy risk.

## Models

The project compares two approaches:

1. Random Forest with inductively extracted graph features.
2. GraphSAGE graph neural network.

## Main results

### Random Forest + graph features

- Optimal threshold: 0.1100
- ROC-AUC: 0.7871
- PR-AUC: 0.2951
- Accuracy: 0.6054
- Precision: 0.2576
- Recall: 0.9365
- F1-Score: 0.4041

The Random Forest baseline was built without topology data leakage.

## Repository structure

```text
report/      Final technical report
notebooks/   Python notebook with reproducible code
data/        Input datasets
figures/     Generated visualizations
