# Corporate Default Prediction Using SNA and GraphSAGE

This repository contains the final project for the Social Network Analysis course.

The project studies corporate bankruptcy prediction using company-level financial indicators, Social Network Analysis features, and graph machine learning. The main idea is that a company’s default risk may depend not only on its internal financial condition, but also on its position in the corporate network and its relationships with counterparties.

## Research Goal

The goal of the project is to test whether corporate network structure contains useful predictive information for bankruptcy risk.

In other words, we check whether the use of graph-based features and graph machine learning can improve the analysis of corporate default risk compared with isolated company-level scoring.

## Research Hypothesis

**H1:** The structure of corporate relationships contains additional signal about bankruptcy risk.

If a company is connected to risky counterparties or occupies a vulnerable position in the network, its probability of default may be higher.

## Dataset

The project uses three main data files:

1. `enterprise_nodes_2934.csv`
   This is the company-level dataset. Each row represents one company.
   It contains the target variable and financial indicators.

   Main columns:

   * `enterprise_id`
   * `revenue`
   * `debt_ratio`
   * `liquidity`
   * `legal_cases`
   * `credit_score`
   * `bankrupt`

2. `enterprise_edges_9000.csv`
   This is the corporate relationship dataset. Each row represents an edge between two companies.

   Main columns:

   * `source_id`
   * `target_id`
   * `relationship_type`
   * `weight`
   * `interaction_freq`

3. `enterprise_combined_dataset.csv`
   This is the combined dataset that links company-level information with corporate relationships.

## Network Design

The corporate network is represented as a graph:

* Nodes: companies
* Edges: corporate relationships between companies
* Target variable: `bankrupt`
* Edge types:

  * `supplier`
  * `shared_director`
  * `co-investor`
  * `parent_company`

The graph contains:

* 2,934 companies
* 9,000 original corporate relationships
* 8,993 unique edges after simplification
* 9 connected components
* Largest connected component: 2,926 nodes
* Graph density: 0.00209

The target variable is imbalanced:

* Bankrupt companies: 14.2%
* Non-bankrupt companies: 85.8%

Because of this class imbalance, PR-AUC is used as the main evaluation metric.

## Methodology

The project compares two approaches.

### 1. Random Forest with Graph Features

The first model is a classical machine learning baseline.

It uses:

* financial company-level features;
* graph features extracted from the corporate network.

The graph features include structural indicators such as PageRank, degree centrality, and clustering coefficient.

To avoid data leakage, graph features are extracted using an inductive approach. This means that the model does not use future test information when calculating graph-based features.

### 2. GraphSAGE

The second model is a graph neural network based on GraphSAGE.

GraphSAGE uses:

* node features;
* graph structure;
* information from neighboring companies.

The model is designed to learn whether network position and neighboring companies contain useful information for predicting bankruptcy risk.

## Main Results

### Random Forest + Graph Features

* Optimal threshold: 0.1100
* ROC-AUC: 0.7871
* PR-AUC: 0.2951
* Accuracy: 0.6054
* Precision: 0.2576
* Recall: 0.9365
* F1-Score: 0.4041

The Random Forest model achieved very high Recall. This means that it detected most bankrupt companies, but it also produced more false positives.

### GraphSAGE

* Optimal threshold: 0.6184
* ROC-AUC: 0.7377
* PR-AUC: 0.2956
* Accuracy: 0.7460
* Precision: 0.2906
* Recall: 0.5397
* F1-Score: 0.3778

GraphSAGE achieved higher Accuracy and Precision. However, its Recall was lower, which means that the model classified companies as bankrupt more cautiously.

## Model Comparison

| Model                          | ROC-AUC | PR-AUC | F1-Score |
| ------------------------------ | ------: | -----: | -------: |
| Random Forest + graph features |  0.7871 | 0.2951 |   0.4041 |
| GraphSAGE                      |  0.7377 | 0.2956 |   0.3778 |

| Model                          | Accuracy | Precision | Recall | Threshold |
| ------------------------------ | -------: | --------: | -----: | --------: |
| Random Forest + graph features |   0.6054 |    0.2576 | 0.9365 |    0.1100 |
| GraphSAGE                      |   0.7460 |    0.2906 | 0.5397 |    0.6184 |

GraphSAGE is slightly better by PR-AUC, but the difference is very small. Random Forest performs better by ROC-AUC, Recall, and F1-Score, while GraphSAGE performs better by Accuracy and Precision.

## Conclusion

The project confirms that network analysis is useful for corporate bankruptcy prediction.

The results show that corporate relationships contain predictive information. A company’s position in the network, its links to counterparties, and its local graph structure can help identify bankruptcy risk.

Random Forest with graph features is better for detecting as many risky companies as possible. GraphSAGE provides a more cautious and balanced classification.

Overall, the project supports the idea that corporate default prediction should not rely only on isolated financial indicators. Network-based analysis adds useful information and can improve the understanding of systemic corporate risk.


## Files Description

### `data/`

This folder contains the input datasets used in the project.

* `enterprise_nodes_2934.csv` — company-level data and bankruptcy target.
* `enterprise_edges_9000.csv` — corporate relationships between companies.
* `enterprise_combined_dataset.csv` — combined file linking company information and network relationships.

### `notebooks/`

This folder contains the main Python notebook with the full project pipeline.

* `SNA Project Code.ipynb` — data loading, graph construction, feature extraction, Random Forest model, GraphSAGE model, evaluation, and visualizations.

### `report/`

This folder contains the final written report.

* `SNA Report V1.docx` — final report.


## Requirements

The project is implemented in Python.

Main libraries:

* pandas
* numpy
* scikit-learn
* networkx
* matplotlib
* seaborn
* torch
* torch_geometric

## Team

* Zhitnikov Danila
* Khoshimov Mark
* Panchenko Anastasia

## Course

Social Network Analysis
Master’s Programme in Finance
National Research University Higher School of Economics
Saint Petersburg, 2026
