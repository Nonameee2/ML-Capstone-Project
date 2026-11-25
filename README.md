# Machine Learning Capstone Project — Heart Disease

**Author:** YOUR NAME  |  **Course/Section:** ______  |  **Instructor:** ______  |  **Date:** ______

## Quick Links
- 📄 **Final report:** [project_report.pdf](project_report.pdf)
- 📓 **Notebook (GitHub):** [notebooks/heart_disease_capstone.ipynb](notebooks/heart_disease_capstone.ipynb)
- ☁️ **Google Colab:** [Open in Colab](https://colab.research.google.com/drive/1g8hbgM5DWF-qVqEmUoxscSB4Lt_stBEA?usp=sharing)
- 💻 **Repository:** https://github.com/Nonameee2/ML-Capstone-Project

## Project Overview
This university capstone demonstrates a complete machine-learning workflow using the processed Cleveland subset of the UCI Heart Disease dataset. It covers data understanding, exploratory data analysis (EDA), preprocessing, regression, classification, clustering, evaluation, visualization, and documentation.

### Three tasks
- **Regression:** Linear Regression predicts age from the other attributes (age is excluded from its inputs). This is a teaching exercise, not the dataset's primary purpose.
- **Classification:** Logistic Regression predicts a binary label derived from the original diagnosis (`0` = no disease; original values `1–4` = disease present).
- **Clustering:** K-Means groups records based on scaled clinical attributes, without using the disease label as an input.

> **Health disclaimer:** This is an educational project, not a diagnostic tool. The dataset is small and historical. Do not use these models for medical decisions.

## Dataset Information
- **Source:** UCI Machine Learning Repository, Heart Disease dataset
- **Subset:** Processed Cleveland dataset
- **Source record count:** 303
- **Columns:** 13 input attributes and one diagnosis attribute
- **DOI:** https://doi.org/10.24432/C52P4C
- **Dataset page:** https://archive.ics.uci.edu/dataset/45/heart+disease

The notebook downloads the data automatically on its first run and stores it in `data/processed.cleveland.data`. If the runtime has no internet access, download the processed Cleveland file from the UCI dataset page and place it in `data/`.

## Repository Structure
```text
ML-Capstone-Project/
├── data/
│   ├── processed.cleveland.data       # downloaded by notebook on first run
│   └── heart_disease_cleaned.csv      # generated after notebook runs
├── notebooks/
│   └── heart_disease_capstone.ipynb
├── results/
│   ├── feature_histograms.png
│   ├── correlation_heatmap.png
│   ├── boxplots.png
│   ├── countplots.png
│   ├── regression_actual_vs_predicted.png
│   ├── confusion_matrix.png
│   ├── kmeans_elbow.png
│   ├── kmeans_clusters_age_thalach.png
│   └── metrics_summary.csv
├── README.md
└── project_report.pdf
```
Result images and CSV files are created by running the notebook.

## Required Libraries
- Python 3.9+
- pandas
- numpy
- scikit-learn
- matplotlib
- seaborn
- jupyter

All libraries are also listed in `requirements.txt`.

## Installation Instructions

### Option A: Local Python environment
```bash
git clone https://github.com/Nonameee2/ML-Capstone-Project.git
cd ML-Capstone-Project

python -m venv .venv
# Windows:
.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate

pip install -r requirements.txt
jupyter notebook
```

Open `notebooks/heart_disease_capstone.ipynb` and run all cells from top to bottom.

### Option B: Google Colab
1. Upload `notebooks/heart_disease_capstone.ipynb` to Google Drive or open it in Google Colab.
2. Run the notebook cells from top to bottom.
3. If using Colab, create the `data/` and `results/` folders in the working directory or adjust the paths in the notebook as needed. The notebook creates these folders relative to its working directory.
4. Download the completed notebook and generated outputs for your submission.
5. The shareable Colab link is in the [Quick Links](#quick-links) section and in the final report.

## How to Run
1. Install the libraries.
2. Open the notebook.
3. Execute every cell in order.
4. Inspect the EDA plots and Elbow curve.
5. If needed, adjust `SELECTED_K` after inspecting the Elbow curve, then rerun the clustering and downstream cells.
6. Review the actual model metrics and saved charts under `results/`.
7. Read the full analysis in [project_report.pdf](project_report.pdf).

## Results Summary
Metrics below were produced by running the notebook and match `results/metrics_summary.csv`.

| Task | Model | Key results |
|---|---|---|
| Regression (predict age) | Linear Regression | MSE = 65.254, RMSE = 8.078 years, R² = 0.117 |
| Classification (disease present) | Logistic Regression | Accuracy = 0.885, Precision = 0.839, Recall = 0.929, F1 = 0.881 |
| Clustering | K-Means (K = 3) | Silhouette = 0.126; cluster sizes 121 / 103 / 79 |

**Confusion matrix (test set, n = 61):** TN = 28, FP = 5, FN = 2, TP = 26.

> Exact values can change if the data or library versions change. If you re-run the notebook, update this table from `results/metrics_summary.csv`.

### Key Findings
- Logistic Regression separates disease from no disease well (about 89% accuracy). It found 26 of 28 disease cases (recall 0.93) and missed 2, which matters most in a medical setting; the trade-off is 5 false alarms among 33 healthy patients (precision 0.84).
- Age is only weakly predictable from the other attributes (R² = 0.12), as expected for an exercise task.
- The clusters overlap heavily (silhouette 0.126), so they are not clearly separated groups.
- EDA: the target is fairly balanced (164 no disease, 139 disease). The features most correlated with disease are `thal` (0.53), `ca` (0.46) and `exang` (0.43); `thalach` is negatively correlated (-0.42). Age is only weakly correlated (0.22), and cholesterol and fasting blood sugar are almost unrelated to the target.

## Interpretation of Metrics
- **MSE:** average squared prediction error; lower is better.
- **RMSE:** square root of MSE, in the target's units; lower is better.
- **R²:** variance explained relative to a mean baseline; higher is generally better.
- **Accuracy:** fraction of classification predictions that are correct.
- **Precision:** fraction of predicted positive cases that are actually positive.
- **Recall:** fraction of actual positive cases found by the model.
- **F1:** harmonic mean of precision and recall.
- **Silhouette Score:** how well-separated and cohesive clusters are; closer to 1 generally indicates better separation, near 0 overlapping clusters, and negative values possible poor assignments.

## Limitations
- Small, historical dataset (303 patients, one hospital), so results may not generalize.
- A single 80/20 split gives a small test set (61 rows); metrics can vary with a different split.
- Missing values (`ca`, `thal`) are imputed, which adds some uncertainty.
- Clusters are mathematical groupings, not validated clinical subtypes.

## Troubleshooting
- **Download fails (no internet):** download `processed.cleveland.data` from the UCI page and put it in `data/`.
- **Different row count or metrics on a second run:** delete `data/processed.cleveland.data` and re-run, or make sure the notebook saves it with `header=False`.
- **Folders not found in Colab:** run the notebook from the working directory; it creates `data/` and `results/` automatically.

## Reproducibility
Install dependencies with `pip install -r requirements.txt`. Random seed: `RANDOM_STATE = 42`.

## References
1. Janosi, A., Steinbrunn, W., Pfisterer, M., & Detrano, R. UCI Heart Disease Dataset. UCI Machine Learning Repository. https://doi.org/10.24432/C52P4C
2. Pedregosa, F. et al. (2011). Scikit-learn: Machine Learning in Python. *Journal of Machine Learning Research*, 12, 2825–2830. https://jmlr.org/papers/v12/pedregosa11a.html
3. Scikit-learn documentation. https://scikit-learn.org/stable/

## Final Submission Checklist
- [x] Run every notebook cell successfully.
- [x] Review and explain findings from the actual plots.
- [x] Save generated charts and `metrics_summary.csv` in `results/`.
- [x] Update the PDF report with actual metrics and chosen K.
- [x] Upload the notebook to Google Colab and add a viewable link to the PDF.
- [x] Push the complete repository to a public GitHub repository.
- [x] Submit the public repository URL.

## GitHub Repository
This project is available at: https://github.com/Nonameee2/ML-Capstone-Project
