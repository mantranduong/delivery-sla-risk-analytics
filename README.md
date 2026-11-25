# Delivery SLA Risk Analytics & Prediction

**Individual academic project | Dương Mẫn Trân | Python · Scikit-learn · Tableau**

An end-to-end academic study of delivery-delay risk, combining exploratory analysis, statistical testing, classification and operational visualization. The public Amazon Delivery Dataset is used as a proxy for an instant-delivery business problem; this is not a deployment or analysis of internal company data.

[View interactive Tableau dashboard](https://public.tableau.com/app/profile/d.ng.tr.n7982/viz/NHOM_6/Yutriro?publish=yes) · [Business process diagram](reports/business_process.png)

## Business objective

Identify potentially late deliveries to support proactive monitoring and reduce missed delay alerts. The study prioritizes recall while considering false alarms.

## Interactive Dashboards 
<img width="1199" height="699" alt="Tổng quan" src="https://github.com/user-attachments/assets/d33abc35-8280-43f7-818f-a77e51ffcc3a" />
<img width="1199" height="699" alt="Yếu tố rủi ro" src="https://github.com/user-attachments/assets/a6a39119-2bdb-453d-bee9-586666ffba9b" />

[Xem Interactive Dashboard trên Tableau Public](https://public.tableau.com:9443/views/DeliverySLARiskAnalysisOperationalRiskDashboard/Tngquan?:language-en-US&:sid=&:redirect-auth&:display_count=n&:origin=viz_share_link)
## Data and methodology

- 43,739 original delivery records; 43,648 records in the modeling split (34,918 train / 8,730 evaluation).
- Clean missing values, standardize categories, engineer time and geographic features, and construct two illustrative SLA definitions.
- Explore operational factors using descriptive analysis, chi-square tests and ANOVA.
- Compare Logistic Regression, Decision Tree and Random Forest using 15 predictors and stratified splitting; examine five-fold cross-validation.
- Explore a decision threshold targeting recall of at least 80% and visualize operational risk in Tableau.

## Recorded model results

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | .7072 | .7309 | .7646 | .7473 | .7758 |
| Decision Tree | .7514 | .7747 | .7913 | .7829 | .8120 |
| Random Forest | .7834 | .8221 | .7880 | .8047 | .8680 |
| Random Forest (threshold .4848) | .7849 | .8163 | .8002 | .8082 | .8680 |

Random Forest five-fold ROC-AUC: 0.8727 ± 0.0021 (recorded notebook output).

![Recorded confusion matrix](assets/confusion_matrix.png)

**Interpretation:** lowering the threshold increases recall at the expense of precision. The tuned threshold was selected on the same evaluation split used to report its metrics, so these scores are exploratory, not an unbiased final test result. A separate validation split and untouched test set are recommended for future work.

## Repository guide

| Path | Purpose |
|---|---|
| `notebooks/01_preprocessing.ipynb` | Data preparation and SLA target construction |
| `notebooks/02_eda.ipynb` | Exploratory and statistical analysis |
| `notebooks/03_modeling.ipynb` | Model comparison, threshold exploration and export |
| `data/README.md` | Dataset setup and publication restrictions |
| `models/model_metadata.json` | Original model configuration |
| `reports/` | Business process diagram and dashboard link |
| `assets/` | Recorded visual output |

## How to run locally

Use Python 3.10+ and create a virtual environment. From the repository root:

```bash
python -m venv .venv
# Activate the environment for your operating system
pip install -r requirements.txt
jupyter notebook
```

Place the authorized original `amazon_delivery.csv` in `data/unprocessed/`. Run notebooks 01, 02 and 03 in order. Processed CSVs are generated in `data/processed/`; model comparison output is saved in `results/`; notebook 03 exports the model and metadata in `models/`.

This portfolio edition standardizes paths and export code. Saved historical outputs are retained; the complete notebook workflow has not been rerun. Dependencies are minimum requirements, not a verified lockfile.

## Limitations

- SLA labels are constructed using assumed rules, not actual company contractual targets. Some predictors also contribute to target construction, creating structural dependence.
- Threshold selection requires independent validation before operational use.
- The original dataset's redistribution terms are unverified; raw and processed CSVs are excluded.
- The trained binary and incomplete script templates are excluded from the public edition. No production deployment is claimed.
- Dashboard findings are illustrative and require validation against real operational data.

## Author

Dương Mẫn Trân — Data Science & Business Analytics student, University of Economics – The University of Danang. Sole contributor to this academic project.

[LinkedIn](https://www.linkedin.com/in/m%E1%BA%ABn-tr%C3%A2n-d%C6%B0%C6%A1ng-0b593a301/) · [Email](mailto:duongmantran848@gmail.com)
