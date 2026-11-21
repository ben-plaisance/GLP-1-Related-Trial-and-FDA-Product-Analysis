# GLP-1-Related Obesity Clinical Trials and FDA Drug Products

A Python-based descriptive analysis of clinical trials identified through a ClinicalTrials.gov obesity/GLP-1 search and corresponding active-ingredient listings in FDA drug product records. This project was prepared for **CHIP 705: Introduction to Programming**.

## Research question

How are clinical trials involving selected GLP-1-related medications distributed across study characteristics, and how do their interventions correspond to FDA-listed drug products?

## Data sources

- **ClinicalTrials.gov:** `ctg-studies.csv` — study information, including trial status, phase, interventions, and start dates (674 study records in this export).
- **Drugs@FDA:** `Products.txt` — tab-delimited FDA product records, including application and product numbers and active ingredients.

The analysis reads these **original files directly in Python**. It does not use the SQLite database or cleaned tables from the separate SQL project.

## Repository contents

```text
GLP-1-Related-Trial-and-FDA-Product-Analysis/
├── README.md
├── Milestone2_Final.ipynb                 # Main analysis notebook
├── data/
│   ├── ctg-studies.csv             # ClinicalTrials.gov export (required)
│   ├── Products.txt                # Drugs@FDA product records (required)
│   ├── Applications.txt            # Additional source file (not used by notebook)
│   └── Submissions.txt             # Additional source file (not used by notebook)
└── results/                        # Generated figures and summary tables
    ├── 01_study_landscape.png
    ├── 02_studies_by_ingredient.png
    ├── 03_fda_product_records.png
    ├── 04_start_years.png
    ├── study_status.csv
    ├── study_phase.csv
    ├── ingredient_studies.csv
    ├── ingredient_fda_comparison.csv
    └── start_years.csv
```

The `results/` files are created or overwritten when the notebook runs. The additional FDA files are included for reference but are not needed to reproduce this analysis.

## Requirements

- Python 3.10 or later (Python 3.11+ recommended for the date-parsing step)
- `pandas` (version 2.0 or later)
- `matplotlib`
- Jupyter Notebook or JupyterLab (only if running the `.ipynb` file)

Install the Python packages:

```bash
python -m pip install "pandas>=2.0" matplotlib notebook
```

## How to run

1. Download or clone the repository, then **extract the ZIP** if downloaded from GitHub. Keep the notebook, `data/` folder, and `results/` folder together in the extracted project directory.
2. Install the packages listed above.
3. Open **`Milestone2_Final.ipynb`** in Jupyter Notebook, JupyterLab, or VS Code.
4. Select **Restart Kernel and Run All Cells**. The notebook locates `ctg-studies.csv` and `Products.txt` in the project's `data/` folder and creates the `results/` folder if necessary.
5. Review the printed summaries and four PNG figures and five CSV summary tables saved to `results/`.

**File-path troubleshooting:** The notebook searches for the project directory from the current working folder and nearby locations. If it cannot find the data files, check that the downloaded repository has been extracted and that `data/ctg-studies.csv` and `data/Products.txt` exist locally. GitHub-hosted files are not automatically available to a local Jupyter session. For reliable execution, open Jupyter from the extracted repository folder.

## Analysis workflow

1. **Load and clean data:** Import the raw CSV and tab-delimited text file, remove records with missing identifiers, and deduplicate studies and FDA products.
2. **Describe the trial landscape:** Count studies by status and reported phase.
3. **Identify selected ingredients:** Split pipe-delimited intervention entries and look for five ingredients: semaglutide, liraglutide, tirzepatide, exenatide, and dulaglutide. Exclude placebo intervention names.
4. **Compare with FDA listings:** Find FDA product records whose active-ingredient text contains the selected ingredients. Count unique products by application number and product number.
5. **Analyze start years:** Summarize study start years, excluding records dated after November 21, 2026.
6. **Export results:** Produce charts, CSV summary tables, and a printed results summary.

## Selected findings

The ClinicalTrials.gov export contains **674 distinct studies**; **343 studies** name at least one of the five selected ingredients. Counts by ingredient are shown below. A study may mention multiple ingredients, so the study counts in this table are **not additive**.

| Ingredient | Distinct studies | FDA product records |
|---|---:|---:|
| Tirzepatide | 133 | 48 |
| Liraglutide | 117 | 14 |
| Semaglutide | 95 | 34 |
| Exenatide | 21 | 9 |
| Dulaglutide | 4 | 4 |

These counts are descriptive and specific to the supplied data exports.

## Limitations

- The clinical trial dataset reflects a particular ClinicalTrials.gov search/export; it is not a comprehensive inventory of all GLP-1 research.
- Ingredient identification uses name-based rules for **five selected medications**, so other drugs and alternative names may be missed.
- FDA correspondence is based on active-ingredient text, **not** a verified link between an individual trial and a specific marketed product.
- FDA product record counts are not counts of unique medications, and the analysis does **not** determine whether each product has an FDA-approved obesity indication.
- Some studies have missing phase information; planned future start dates are excluded from the historical start-year chart.

## Data attribution

- [ClinicalTrials.gov](https://clinicaltrials.gov/) — clinical study records.
- [Drugs@FDA](https://www.accessdata.fda.gov/scripts/cder/daf/index.cfm) — FDA drug product records.
