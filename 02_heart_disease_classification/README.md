# Heart Disease Classification — Cleveland Dataset

Exploratory data analysis and supervised classification on the Cleveland heart
disease dataset: predicting the presence of heart disease from 13 clinical
measurements.

Group work with **Payal Priyadarshini**, **Leon Igal Inselberg Barbut** and
**Renk Asik**, Freie Universität Berlin.

## Approach

The assignment is in two halves. The first is exploratory: age distributions,
boxplots of the key health parameters, per-feature histograms and a scatter
matrix, to see which measurements separate the classes before any model is
fitted. The second trains several classifiers and compares them on **accuracy,
sensitivity and specificity** side by side — the right framing for a diagnostic
problem, where a false negative and a false positive cost very different things.
Confusion matrices and heatmaps are reported per classifier.

## Contents

| File | What it is |
|---|---|
| [`notebooks/a1_eda_and_classifiers.ipynb`](notebooks/a1_eda_and_classifiers.ipynb) | Full assignment: exploratory analysis plus classifier comparison |
| [`notebooks/a1_exploratory_plots.ipynb`](notebooks/a1_exploratory_plots.ipynb) | Exploratory plots in isolation |
| [`notebooks/in_class_intro.ipynb`](notebooks/in_class_intro.ipynb) | In-class introduction: pandas grouping and plotting on a small fruits dataset |
| [`a1_report.pdf`](a1_report.pdf) | Assignment report |
| [`data/heart_disease_cleveland/`](data/heart_disease_cleveland) | The UCI heart disease data, with the Cleveland, Hungarian, Switzerland and Long Beach VA sets |
| [`data/fruit_data_with_colors.txt`](data/fruit_data_with_colors.txt) | Small teaching dataset for the in-class notebook |

**Stack:** scikit-learn, pandas, seaborn, matplotlib

## Data

The heart disease data is included — it is small and public, from the
[UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/45/heart+disease).
Note the standard caveat: the Cleveland set has 303 instances, and the target is
usually collapsed from five severity levels to a binary present/absent label.
