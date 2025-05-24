# AI Harms: Misclassified Patient Demographics in Clinical ML

This repository supports the analysis in the manuscript **"AI Harms: An Analysis of Demographic Distribution of Misclassified Patients in Clinical ML Settings."** The notebooks in this repo form a rough but modular pipeline for exploring ICU data from the `eICU-CRD` dataset, training clinical prediction models, and analyzing patterns of misclassification by demographic subgroups.

---

## Repository Structure

| Notebook | Purpose |
|----------|---------|
| `load_eICU_example.ipynb` | Minimal working example showing how to query tables from the `eICU-CRD` dataset using BigQuery in Colab. |
| `data_exploration.ipynb` | Explores demographic distribution in the patient cohort (ethnicity, gender, age, etc.) and generates summary plots. |
| `Feature_Selection.ipynb` | Queries lab values, ICD-9 codes, and medication use from BigQuery; selects features for modeling based on clinical literature. |
| `Model_Training.ipynb` | Trains models to predict hospital mortality, AKI, and prolonged length of stay. Adds outcome columns and labels. |
| `Clustering_analysis.ipynb` | Computes misclassification scores per patient across multiple outcomes and prepares data for demographic stratification. |
| `misclassified_demographic_analysis.ipynb` | Aggregates per-patient misclassification counts, merges across outcomes, and analyzes subgroup disparities. |
| `AI_Harms_Mortality.ipynb` | Walkthrough of a baseline decision tree model for predicting mortality from emergency-admitted patients. Serves as a simple reproducible pipeline. |

---

## Usage Instructions

These notebooks are written for use in **Google Colab** and require access to the `eICU-CRD` dataset via BigQuery. Most notebooks will prompt for authentication and expect a valid Google Cloud project ID.

### Setup (run in each notebook as needed)
- Authenticate with BigQuery:
  ```python
  from google.colab import auth
  auth.authenticate_user()
  ```
- Set your GCP project ID:
  ```python
  project_id = 'your-google-cloud-project-id'
  os.environ["GOOGLE_CLOUD_PROJECT"] = project_id
  ```

---

## Suggested Order of Execution

1. **Load & Explore Data**
   - `load_eICU_example.ipynb`
   - `data_exploration.ipynb`

2. **Select Features**
   - `Feature_Selection.ipynb`

3. **Train Models**
   - Prepare CSVs for input to:
     - `Model_Training.ipynb`

4. **Analyze Misclassification**
   - `misclassified_demographic_analysis.ipynb`
   - `Clustering_analysis.ipynb`

5. **Baseline Reproducibility**
   - `AI_Harms_Mortality.ipynb`

---

## Notes

- CSV paths and project IDs are left as placeholders — these must be customized by each user.
- Some packages like `glowyr`, `graphviz`, and `tableone` may need to be installed manually inside Colab cells.
- Outputs like misprediction scores are saved to intermediate CSVs and reused across notebooks.

This codebase is not finalized, but serves as a reproducible scaffold for the analyses in the manuscript.
