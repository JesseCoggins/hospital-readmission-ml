# Hospital readmission and patient segmentation

**When could a hospital use a readmission score to prioritize follow-up?** I trained a Random Forest on 10,000 hospital records and checked whether its strongest signal would be available when staff made the decision. The full model scored **0.999 ROC-AUC**. Removing length of stay dropped the score to **0.492**, near chance. That makes discharge planning the point at which I would evaluate the model for use.

[Inspect the classification and timing check](notebooks/readmission_classification.ipynb) · [Open the clinical clustering notebook](notebooks/readmission_clustering_pca.ipynb)

## Results

| Held-out test result | With length of stay | Without length of stay |
|---|---:|---:|
| ROC-AUC | 0.999 | 0.492 |
| Accuracy | 97.9% | 63.1% |
| Recall for readmissions | 98.0% | 1.8% |

The classifier used 7,000 training, 1,500 validation and 1,500 test records. I tuned the forest using cross-validation. Its full-model test precision was 96.3% and F1 was 0.971. The comparison above changes the interpretation of those numbers. Staff know the completed stay at discharge. A team deciding whom to contact at admission would need a model validated on information available then. The study measured classification performance. It did not test whether follow-up reduced readmissions.

## What the clustering adds

A separate analysis groups patients by similarities in stay, charges and health history. I standardized seven continuous measures, encoded seven yes/no indicators, inspected the elbow plot, and fit a three-group K-Means model. PCA displays the groups in two dimensions.

- One group averaged **9 days** in hospital and **$3,212** in total charges. Another averaged **60 days** and **$7,401**.
- The oldest group averaged **74 years**, and 95% reported high blood pressure.

Readmission was excluded from clustering. These averages describe differences in the hospital population and can guide questions about service use. Assigning readmission risk to a group would require a separate outcome analysis.

## Review or rerun

Both notebooks use the [included hospital dataset](data/medical_clean.csv). For the verified numerical environment, install [requirements-verified.txt](requirements-verified.txt) (Python 3.13.1). Otherwise install the [requirements](requirements.txt) in a Jupyter environment and use `notebooks/` as the working directory. The classification notebook includes saved evaluation output. The public clustering notebook contains code only and generates its group summaries and plots when run. [Classification report figures](assets/task1-report-extracts/) · [Clustering report figures](assets/task2-report-extracts/)

*WGU M.S. in Data Analytics coursework, D603 Machine Learning.*
