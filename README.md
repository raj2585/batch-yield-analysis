# Batch Yield Loss Analysis — UPR Resin Manufacturing

Analysis and prediction of batch yield loss across 5 production kettles 
in a specialty resin plant, using 13 months of historical batch data (May 2025 – June 2026).

## Problem

In resin manufacturing, yield loss varies batch to batch due to deviations 
in process step durations. Identifying which steps drive yield loss enables 
tighter process control and reduced material waste.

## Dataset

- 615 batches across 5 UPR production kettles (K9, K12, K13, K15, K16)
- 51 resin grades, anonymized
- Features: per-step deviation from standard time for 10 core process steps
- Target: actual yield loss % per batch

Data collected from plant production records. Grade names anonymized 
for confidentiality.

## Approach

**Feature Engineering**
Step-level downtime columns were positional (D.1, D.2...) and not 
comparable across grades since step order varies by grade. Aggregated 
downtime by function name (Charging, Reaction, Cooling etc.) to create 
grade-agnostic features.

**EDA Findings**
- Dropping Time and Reaction Time show strongest correlation with yield loss (0.20, 0.19)
- Kettle 12 shows consistently higher median yield loss than other kettles
- Monthly average yield loss stable between 0.33–0.70% — no long-term drift

**Model**
Random Forest Regressor on 10 engineered step features.

| Metric | Value |
|--------|-------|
| MAE | 0.437% |
| R² | 0.26 |

Top predictors: Charging_1200_Time, Vacuum_Time, Reaction_Time

R² is moderate — expected for a multi-grade dataset where grade chemistry 
accounts for significant unexplained variance. Model performs best in the 
0–1% yield loss range where 75% of batches fall.

## Structure
| File | Content |
|--------|-------|
| 01_eda.ipynb  | EDA, feature engineering, step-yield correlation |
| 02_model.ipynb | Random Forest model, feature importance, evaluation |
| README.md |  |
| .gitignore |  |

## Skills

Python · pandas · scikit-learn · matplotlib · seaborn  
Domain: UPR resin manufacturing · batch processes · process step analysis