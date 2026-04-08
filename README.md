# Hospital Readmission ML

## Overview
This repo combines two machine learning workflows built from the hospital dataset: a supervised classification project and an unsupervised clustering and PCA project. Together, they show breadth across predictive modeling and pattern discovery in healthcare data.

## Coursework Context
This repository packages work originally completed as part of Western Governors University's (WGU) M.S. in Data Analytics program and reorganizes it into a public portfolio format. Screenshots extracted from the original written submissions are preserved in `assets/task1-report-extracts/` and `assets/task2-report-extracts/`.

## What It Shows
- classification modeling for hospital outcome analysis
- data preparation and encoded feature sets
- clustering workflow for segmentation
- PCA-based dimensionality reduction and visualization

## Included Files
- `notebooks/Task-1.ipynb`
- `notebooks/Task-2.ipynb`
- `data/medical_clean.csv`
- `requirements.txt`

## Results

- Random Forest classification achieved test accuracy of `0.979`, precision of `0.963`, recall of `0.980`, F1-score of `0.971`, and ROC-AUC of `0.999` after tuning.
- The clustering workflow used the Elbow Method to select `k = 3` as the optimal number of patient segments.
- PCA visualization showed three distinguishable clusters with reasonable separation rather than randomly mixed groupings.
- The resulting cluster profiles represented lower-risk younger patients with shorter stays, moderate-risk patients with longer stays and higher charges, and higher-risk older patients with more chronic conditions and higher additional charges.

## Selected Visuals

![Classification report visual](assets/task1-report-extracts/report_image_01.png)

![Clustering and PCA report visual](assets/task2-report-extracts/report_image_01.png)
