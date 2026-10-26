# 🛡️ PhishShield AI — Phishing URL Detection

**IBM SkillsBuild Cyber Security 2026 | BharatCares | Final Project**  
**Submitted by:** Brinda Kachchi  
**Category:** Defensive Cybersecurity · Python · Machine Learning

## Project overview

PhishShield AI is an educational phishing-URL detection project. It uses **only features available in a URL string** (lengths, punctuation, subdomains, IP hostname, HTTPS scheme, and similar patterns) to classify URLs as **potential phishing** or **legitimate**. The notebook compares a Logistic Regression baseline with a Random Forest classifier, evaluates held-out hostnames, visualizes the confusion matrix and feature importance, and exports a trained model locally.

**Safety:** This notebook never requests, visits, resolves, clicks, or opens the URLs being classified. A prediction is not a guarantee of safety.

## Dataset — direct source and license

- **Name:** PhiUSIIL Phishing URL (Website)
- **Publisher:** UCI Machine Learning Repository
- **Link:** https://archive.ics.uci.edu/dataset/967/phiusiil+phishing+url+dataset
- **UCI dataset ID:** `967`
- **Original size:** 235,795 URL records (100,945 phishing; 134,850 legitimate).
- **Original class mapping:** `0 = phishing`, `1 = legitimate`.
- **This notebook's class mapping:** `1 = phishing`, `0 = legitimate`.
- **License:** Creative Commons Attribution 4.0 (CC BY 4.0); credit the original authors.
- **Citation:** Prasad, A., & Chandra, S. (2024). *PhiUSIIL Phishing URL (Website)*, UCI Machine Learning Repository. Original paper: https://doi.org/10.1016/j.cose.2023.103545

The dataset is downloaded **when you run the notebook** via `ucimlrepo`. No 54 MB raw CSV is redistributed in this repository. On the first run, **an internet connection is needed**.

## Project files

```text
Brinda_Kachchi_PhishShieldAI_Project.ipynb   # Complete source, training, evaluation and demo
requirements.txt                    # Python dependencies
Brinda_Kachchi_ProjectReport.docx            # Full project documentation
README.md                           # This file
```

## Technologies

Python 3.10+, Jupyter Notebook, pandas, NumPy, scikit-learn, matplotlib, ucimlrepo, joblib, Python standard-library URL parsing.

## Setup and run

```bash
# 1. Download the repository or clone it after publishing to GitHub.
cd IBM_SkillsBuild_Cybersecurity_2026

# 2. Create a virtual environment (recommended).
python -m venv .venv

# Windows PowerShell:
.venv\Scripts\Activate.ps1
# macOS/Linux alternative: source .venv/bin/activate

# 3. Install requirements.
python -m pip install -r requirements.txt

# 4. Launch Jupyter.
python -m notebook
```

Open `Brinda_Kachchi_PhishShieldAI_Project.ipynb` and select **Run > Run All Cells**.

### Outputs

- Data audit: unique URL count and class distribution after cleanup.
- Leakage-reducing hostname-disjoint training and test split.
- Metrics computed on the downloaded dataset: **accuracy, phishing precision, phishing recall, F1, ROC-AUC**.
- Confusion matrix, Random Forest feature-importance plot and harmless example predictions.
- `phishshield_model.joblib` saved locally after a successful run (not part of the four required submission files).

**Reproducibility:** The notebook sets `SEED=42`; by default it samples at most 10,000 examples per class to keep runtime practical. Set `MAX_SAMPLES_PER_CLASS=None` for the full cleaned dataset.

## Method summary

1. Download UCI PhiUSIIL URLs and labels.
2. Remove missing labels, conflicting URL duplicates, and exact duplicate URL strings.
3. Extract 22 numerical lexical/structural URL features **offline**.
4. Use `GroupShuffleSplit` by hostname (75% train, 25% test by group).
5. Fit Logistic Regression and Random Forest; select higher phishing-class F1.
6. Report performance, confusion matrix, and model limitations.
7. Run URL string examples without visiting any site; save the trained model.

## Limitations and ethics

- A model can falsely flag safe links or miss malicious ones. **Never trust predictions as permission to open a URL.**
- The dataset is historical; real-world attackers and benign URLs evolve.
- Grouped holdout does not eliminate all family/domain leakage or sampling bias.
- Raw URL features cannot check page content, redirects or ownership.
- Suspicious keywords and HTTPS are weak signals on their own.
- No scraping, credential collection, scanning or attack simulation is performed.

## Submission checklist

- [x] `Brinda_Kachchi_PhishShieldAI_Project.ipynb`
- [x] `requirements.txt`
- [x] `Brinda_Kachchi_ProjectReport.docx`
- [x] `README.md`

> **Important:** Training metrics are generated when the notebook runs on the real dataset, **not invented in this README or report**. If you submit screenshots/results, execute all notebook cells and capture the actual outputs.

## Publish to GitHub (once a new empty repository exists)

Create an **empty** GitHub repository, suggested name: `ibm-skillsbuild-phishshield-ai`, in account `arceus6667-art`, then run these commands in the folder containing the four files:

```bash
git init
git add Brinda_Kachchi_PhishShieldAI_Project.ipynb requirements.txt Brinda_Kachchi_ProjectReport.docx README.md
git commit -m "Add IBM SkillsBuild PhishShield AI submission"
git branch -M main
git remote add origin https://github.com/arceus6667-art/ibm-skillsbuild-phishshield-ai.git
git push -u origin main
```

The GitHub repository must exist before the push; the repository URL above is a **proposed URL, not a claim it has been created**.
