# Hospital readmission and patient segmentation

**What can hospital records reveal about readmission and patient groups?** I trained a Random Forest on 10,000 hospital records and separately used K-Means and PCA to explore patient segments. The classifier achieved **97.9% held-out accuracy** and **0.999 ROC-AUC**. Its inputs include completed length of stay, so the result applies to discharge-time risk analysis.

[Inspect the classification notebook](notebooks/readmission_classification.ipynb) · [Open the clinical clustering notebook](notebooks/readmission_clustering_pca.ipynb)

## Results

| Held-out test metric | Random Forest |
|---|---:|
| Accuracy | 97.9% |
| Precision for readmissions | 96.3% |
| Recall for readmissions | 98.0% |
| F1 | 0.971 |
| ROC-AUC | 0.999 |

The classifier used 7,000 training, 1,500 validation and 1,500 test records. Five-fold cross-validation searched 216 parameter combinations. The saved search selected 800 trees, unrestricted depth, `max_features='log2'`, a minimum split size of 2 and a minimum leaf size of 1, with mean CV ROC-AUC **0.99817**. The [notebook](notebooks/readmission_classification.ipynb) includes the saved search summary and the held-out evaluation.

## What the clustering adds

A separate analysis groups patients by similarities in stay, charges and health history. I standardized seven continuous measures, encoded seven yes/no indicators, inspected the elbow plot, and fit a three-group K-Means model. PCA displays the groups in two dimensions.

- One group averaged **9 days** in hospital and **$3,212** in total charges. Another averaged **60 days** and **$7,401**.
- The oldest group averaged **74 years**, and 95% reported high blood pressure.

Readmission was excluded from clustering. These averages describe differences in the hospital population and can guide questions about service use. Assigning readmission risk to a group would require a separate outcome analysis.

## Additional validation: feature timing

Completed length of stay (`Initial_days`) is available at discharge. A sensitivity check repeats the selected-model evaluation without that feature.

| Held-out test result | With length of stay | Without length of stay |
|---|---:|---:|
| ROC-AUC | 0.999 | 0.492 |
| Accuracy | 97.9% | 63.1% |
| Recall for readmissions | 98.0% | 1.8% |

The near-chance ROC-AUC without length of stay limits the interpretation of the full model. A team deciding whom to contact at admission would need a model validated on information available then. The study measured classification performance; it did not test whether follow-up reduced readmissions.

## Review or rerun

Both notebooks use the [included hospital dataset](data/medical_clean.csv). For the reproduced held-out evaluation and sensitivity check, install [requirements-verified.txt](requirements-verified.txt) (Python 3.13.1). Otherwise install the [requirements](requirements.txt) in a Jupyter environment and use `notebooks/` as the working directory. The classification notebook retains the saved model-selection summary; per-fit progress logs are omitted. The clustering notebook includes a saved aggregate profile table; other summaries and plots are regenerated when run. [Classification report figures](assets/task1-report-extracts/) · [Clustering report figures](assets/task2-report-extracts/)

## Data and environment

Data: WGU hospital dataset; [source notes](data/README.md).  
Install: `python -m pip install -r requirements.txt`; [environment details](requirements-verified.txt).

*WGU M.S. in Data Analytics coursework, D603 Machine Learning.*
