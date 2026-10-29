# Integrative Multi-Omics ML for Breast Cancer Stage Prediction (TCGA)

Can breast cancer **stage** be predicted from molecular data? This project
builds machine learning models on RNA-seq and DNA methylation data from The
Cancer Genome Atlas and tests whether omics features carry stage information
beyond what clinical variables already provide.

Main project- **Payal Priyadarshini**, **Leon Igal Inselberg Barbut**, and
**Renk Asik** (equal contribution), Freie Universität Berlin.

## Result

**Clinical-only models performed best; omics-only models performed worst.**
Trained on gene expression and methylation alone, all three classifiers were
weak — SVM was the strongest at 0.53 accuracy and 0.38 F1, with logistic
regression and random forest below it. Adding omics to clinical features made
performance *slightly worse* than clinical features alone.

That result is not a failure, and the report argues why: cancer stage is
**defined** by the TNM system from tumour size, lymph node involvement and
metastasis — all clinical and anatomical. Clinical features are not merely
predictive of the target, they are essentially the ground truth for it, so
clinical-only models have a structural advantage. Meanwhile the high
dimensionality of omics data introduces noise and invites overfitting on a
cohort this size.

Pathway enrichment on the top features of the omics models did surface
biologically plausible processes related to tumour progression and immune
interaction, but those findings are exploratory and are reported as such, given
how weak the underlying models are.

## Pipeline

Run the scripts in this order. Each takes the previous step's output.

| Step | Script | What it does |
|---|---|---|
| 1 | [`import_preprocess_data.ipynb`](import_preprocess_data.ipynb) | Imports the multi-omics and phenotype data and writes preprocessed expression, methylation and clinical tables. **Splits clinical data into train and test here**, before any feature selection, to avoid leakage |
| 2 | [`exploratory_analysis.ipynb`](exploratory_analysis.ipynb) | Exploratory analysis of the preprocessed files |
| 3 | [`methyl_qc.ipynb`](methyl_qc.ipynb) | Quality control on the methylation data |
| 4 | [`find_dmrs.Rmd`](find_dmrs.Rmd) | Differentially methylated regions, from the **training** clinical and methylation data |
| 5 | [`diff_exp_analysis.ipynb`](diff_exp_analysis.ipynb) | Differentially expressed genes between stages, from the **training** samples |
| 6 | [`machine_learning_methods.ipynb`](machine_learning_methods.ipynb) | Trains and evaluates logistic regression, SVM and random forest; outputs each model's top features |
| 7 | [`pre-annotation.ipynb`](pre-annotation.ipynb) | Splits each model's important-feature list into genes and methylation sites |
| 8 | [`annotation.Rmd`](annotation.Rmd) | Gene annotation for differentially methylated probes, plus pathway enrichment by ORA and GSEA |

### A note on leakage

Both feature-selection steps (4 and 5) read `preprocessed_clinical_train.csv`
and intersect to training samples only, so the differentially expressed genes
and methylated probes are chosen without ever seeing test labels. In step 6,
`SelectKBest` and `StandardScaler` are fit on the training set and only applied
to the test set. The train/test split happens once, at step 1.

### What goes into `X`

The feature matrix is **gene expression plus methylation**. Clinical variables
are used for the stage labels, not as model features — the clinical-feature
branch was explored and set aside. The clinical-only and clinical-plus-omics
comparisons quoted above are reported in the final report.

## Data

Not included — download from UCSC Xena and place alongside the scripts:

- [Methylation (TCGA-BRCA.methylation450.tsv)](https://xenabrowser.net/datapages/?dataset=TCGA-BRCA.methylation450.tsv&host=https%3A%2F%2Fgdc.xenahubs.net)
- [Gene expression (TCGA-BRCA.star_tpm.tsv)](https://xenabrowser.net/datapages/?dataset=TCGA-BRCA.star_tpm.tsv&host=https%3A%2F%2Fgdc.xenahubs.net)
- [Clinical (TCGA-BRCA.clinical.tsv)](https://xenabrowser.net/datapages/?dataset=TCGA-BRCA.clinical.tsv&host=https%3A%2F%2Fgdc.xenahubs.net)

## Reports

- [`reports/final_report.pdf`](reports/final_report.pdf) — the full 29-page report
- [`reports/project_pitch.pdf`](reports/project_pitch.pdf) — the project pitch

**Stack:** scikit-learn, pandas, NumPy, R/Bioconductor (limma, minfi, clusterProfiler)
