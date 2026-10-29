# Data Science in the Life Sciences

Coursework and projects from the data science track of the MSc Bioinformatics
programme at Freie Universität Berlin — classification on clinical and imaging
data, statistical analysis, and a multi-omics machine learning study on TCGA.

| # | Project | Data | Question |
|---|---|---|---|
| 01 | [Breast cancer histopathology](01_breast_cancer_histopathology) | BreaKHis slide images | Can a network tell benign from malignant tissue, and does architecture matter? |
| 02 | [Heart disease classification](02_heart_disease_classification) | UCI Cleveland, 13 clinical measurements | Which measurements separate the classes, and how do classifiers trade sensitivity against specificity? |
| 03 | [Statistical analysis worksheets](03_statistics_worksheets) | various | Descriptive statistics through to multiple regression, in R Markdown |
| 04 | [Multi-omics cancer stage prediction](04_tcga_multiomics_stage_prediction) | TCGA-BRCA RNA-seq + methylation + clinical | Do molecular features predict cancer stage beyond what clinical variables already give you? |

## Two results worth reading

**Project 01** compares three architectures on identical data. ResNet-50
reaches 0.920 accuracy and 0.98 AUC; a custom CNN and a deliberately weak
single-hidden-layer network both land at 0.86 AUC. Transfer learning beats
training convolutions from scratch on a dataset this size. The detail that
makes the point sharper: the **shallow network slightly outperformed the custom
CNN** (0.843 vs 0.830 accuracy) despite having no convolutional structure — a
CNN only earns its keep with the depth and data to learn useful filters, and a
simple baseline exposed that this one did not.

Recall sits at 0.94–0.98 across all three, which is the metric that matters: a
false negative means telling a patient with malignant tissue they are clear.

## The one to read

**Project 04** is the most substantial, and its result is a negative one worth
stating plainly: models trained on gene expression and methylation alone
performed poorly (best: SVM at 0.53 accuracy, 0.38 F1), and adding omics data to
clinical features made things slightly *worse* rather than better.

The explanation is structural rather than technical. Cancer stage is **defined**
by the TNM system — tumour size, lymph node involvement, metastasis — so
clinical variables are not just predictive of the label, they largely constitute
it. Molecular data is being asked to recover a quantity that was never defined
at the molecular level. The project's value is in establishing that cleanly,
with a leakage-free pipeline, rather than in reporting a high number.

The full reasoning is in the [29-page report](04_tcga_multiomics_stage_prediction/reports/final_report.pdf).

## Large datasets

Two datasets are too large or too standard to vendor here and are documented
with download links in their project READMEs: **BreaKHis v1** (~4 GB of
histopathology images) and the **TCGA-BRCA** methylation, expression and
clinical tables. The UCI heart disease data is small and is included.

## Attribution

All projects are group work with equal contribution; collaborators are named in
each project README. Reports are written in the Springer Nature and eLife
article templates.
