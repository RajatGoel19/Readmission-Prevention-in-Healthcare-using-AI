# Readmission Prevention in Healthcare Using AI

## Research Documentation

This repository serves as the supporting research documentation for the study on hospital readmission prevention using artificial intelligence. It contains the full analytical workflow, source datasets, generated figures, and exported result tables used to examine patterns associated with excess hospital readmissions and to evaluate predictive machine learning models.

The primary research artifact is `Readmission_Prevention_in_Healthcare_Using_AI.ipynb`, which documents the methodology from data acquisition through model evaluation, sensitivity analysis, interpretability, and result export.

## 1. Study Objective

The objective of this study is to investigate whether publicly available Centers for Medicare & Medicaid Services (CMS) hospital data can be used to identify institutional patterns associated with elevated readmission risk and to support the development of AI-driven risk classification models for healthcare quality improvement.

The primary modeling target is facility-level high-risk readmission status, defined from mean Excess Readmission Ratio (ERR) >= 1.0 after aggregation across reported Hospital Readmissions Reduction Program measures.

## 2. Research Scope

This work focuses on hospital-level readmission performance rather than individual patient prediction. The analysis integrates readmission outcomes with hospital characteristics, patient experience measures, infection indicators, and complication data in order to evaluate how structural and quality-related factors relate to excess readmission ratios.

Because the workflow uses public CMS hospital data, the model should be interpreted as a facility-level risk stratification tool rather than a patient-level clinical prediction system.

## 3. Data Sources

The study uses CMS hospital datasets included in this repository:

- `Hospital_Readmissions.csv`
- `Hospital_General_Information.csv`
- `HCAHPS_Hospital.csv`
- `Healthcare_Associated_Infections.csv`
- `Complications_and_Deaths.csv`

These datasets were combined to create a consolidated analytical dataset for descriptive, comparative, and predictive analysis.

## 4. Methodology

The documented workflow in the notebook includes the following research steps:

1. Data loading from multiple CMS source files.
2. Data cleaning and preprocessing, including handling missing values, converting numeric fields, and removing duplicates.
3. Dataset integration using hospital identifier fields to create a merged master dataset.
4. Facility-level aggregation of readmission measures and construction of the high-risk target.
5. Exploratory analysis of readmission performance across hospital type, ownership, star rating, and reporting periods.
6. Descriptive statistical analysis of key variables related to readmission performance.
7. Visualization of major distributional and relational patterns.
8. Development and evaluation of machine learning models for high-risk hospital classification.
9. Baseline comparator analysis, including dummy models, a CMS star-rating-only model, and a same-period ERR rule.
10. Sensitivity analysis removing CMS Overall Star Rating to assess rating dependence.
11. EBM interpretability analysis using feature contributions, shape functions, and interaction plots.
12. Export of structured outputs for research reporting and reproducibility.

## 5. Analytical Outputs

The repository contains the main outputs generated from the study:

- `Figure1_Readmission_Distribution.png`: histogram of excess readmission ratios.
- `Figure2_Readmission_by_Type.png`: comparison of readmission performance by hospital type.
- `Figure3_Correlation_Matrix.png`: correlation matrix of facility-level quality indicators.
- `Figure5_EBM_Shape_Functions.png`: EBM shape-function plots for leading feature effects.
- `Figure6_EBM_Interaction.png`: EBM interaction plot for the strongest detected interaction.
- `model_cv_results.csv`: cross-validation performance metrics for evaluated models.
- `baseline_comparison.csv`: hold-out comparison of trivial baselines, policy-visible comparators, and selected models.
- `ablation_no_star_rating.csv`: cross-validation sensitivity analysis comparing model AUC with and without CMS Overall Star Rating.
- `feature_importance.csv`: readable EBM feature contribution results from the modeling workflow.
- `facility_risk_scores.csv`: facility-level risk classification output.
- `CMS_Research_Analysis_Results.xlsx`: compiled analytical results for reporting.

## 6. Modeling Summary

Several classification models were evaluated to identify hospitals at higher risk of excessive readmissions. Candidate models include Logistic Regression, Random Forest, Gradient Boosting, SVM with RBF kernel, XGBoost, Explainable Boosting Machine (EBM), and a stacking ensemble.

Based on the exported cross-validation results in `model_cv_results.csv`, the EBM produced the strongest mean ROC-AUC among the tested approaches in the current experiment, achieving an **AUC-ROC of 0.729** while preserving full model interpretability. Logistic Regression performed closely behind EBM, while tree-based ensemble and SVM models provided additional comparison points.

The current workflow also includes hold-out baseline comparisons in `baseline_comparison.csv`. These compare the selected model against majority-class and stratified-random dummy classifiers, a CMS Overall Star Rating-only logistic model, a same-period ERR rule comparator, and a full-feature Logistic Regression model.

## 7. Interpretability and Sensitivity Analysis

The inclusion of interpretable modeling is important for healthcare research because it supports both predictive performance and transparency in identifying the variables most associated with elevated institutional readmission risk.

The EBM outputs identify leading feature contributions and visualize selected feature-response patterns through shape functions. The workflow also exports an interaction plot for the strongest detected EBM interaction.

The star-rating ablation analysis in `ablation_no_star_rating.csv` evaluates model performance after removing CMS Overall Star Rating. This check is included because CMS star ratings may reflect readmission-related quality domains, so the analysis separates predictive utility from possible circularity in the public rating feature.

## 8. Research Contribution

This project contributes a reproducible, data-driven framework for studying hospital readmissions using public healthcare quality datasets. It demonstrates how AI and statistical analysis can be combined to:

- identify patterns in institutional readmission outcomes,
- compare healthcare facilities across structural and quality dimensions,
- benchmark predictive models against simple policy-visible comparators,
- generate interpretable risk predictions, and
- support future research in healthcare operations, policy, and quality improvement.

## 9. Repository Purpose

This repository is intended to function as the documentation and computational companion for the research paper. It preserves the analytical process, intermediate outputs, and final result files so that the study workflow can be reviewed, reproduced, and extended in future work.

