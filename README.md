# SalaryIQ: The Data Analyst Salary Intelligence Platform

> **An end-to-end data analytics project** from raw Glassdoor job postings to a statistically validated salary intelligence tool with a Tableau dashboard, hypothesis testing, and actionable negotiation insights.


## Project Overview

Most data analysts accept job offers without knowing if the salary is fair. Generic salary sites return ranges so wide (often $45K–$120K) they're useless for negotiating. **SalaryIQ** was built to fix that.

Using 2,253 real Glassdoor job postings, we ran six hypothesis tests to identify which factors *actually* and *statistically significantly* affect a data analyst's salary — then built a Tableau dashboard that lets any candidate benchmark their offer in 30 seconds.


## Key Findings

| Hypothesis | Factor | Result | Effect |
|---|---|---|---|
| H1 | Location (state) | Has significant effect | Up to **$50,000** gap — strongest signal |
| H2 | Industry sector | Has significant effect | Up to **$17,000** gap |
| H3 | Seniority level | Has significant effect | **+$6,000** entry → senior |
| H4 | Skills (Python vs Excel) | Has significant effect | Python **+$3,500** · Excel **−$1,500** |
| H5 | Company size | Not confirmed | 0.03% variance explained — no effect |
| H6 | Company rating | Not confirmed | r = 0.037 — no effect |

**Bottom line:** Where you work and which sector you target matters far more than the size or prestige of the company.



## Repository Structure

```
salaryiq-analyst-salary-study/
│
├── data/
│   └── glassdoor-raw.csv              ← Raw Glassdoor scrape (2,253 postings)
│
├── notebooks/
│   ├── datajobs_dataset_cleaning.ipynb           ← Sprint Cleaning notebook
│   └── salaryiq_datacleaning_qa_pipeline.ipynb   ← EDA + hypothesis testing
│
├── outputs/
│   ├── glassdoor-cleaned.csv          ← Cleaned dataset from Sprint Cleaning Notebook
│   └── salaryiq-glassdoor-cleaned.csv ← Dataset used for Dashboard (further cleaned)
│
├── reports/
│   ├── Salary Intelligence Platform - Pitch Deck.pdf   ← Sprint pitch deck PDF
│   └── jobmarket_exploratory_data_analysis.ipynb       ← EDA + hypothesis testing
│
├── images/
│   ├── dashboard-market-overview.png  ← Tableau dashboard screenshot
│   ├── dashboard-offer-checker.png    ← Offer checker page
│   └── dashboard-full.png             ← Full dashboard view
│
└── README.md
```


## Data Source

**Dataset:** Glassdoor Data Analyst Job Postings (US)  
**Source:** Glassdoor scrape via Kaggle  
**Coverage:** 2,253 job postings across 13 US states  
**Fields:** Job title, salary estimate, company, location, sector, industry, rating, size, founded year  


## Dashboard

🔗 **[View Live on Tableau Public →]**

The SalaryIQ dashboard includes three views:

- **Market Overview** shows salary distribution, geographic gap, experience level comparison, industry bubble chart, and skills impact overview
- **By Location** shows state-by-state salary comparison with cost-of-living adjustment using the MERIC 2025 index
- **Offer Checker** shows input your offer details (state, sector, seniority) and get an instant verdict: Fair / Underpaid / Overpaid, with a negotiation brief


## QA & Data Cleaning Process

The raw Glassdoor dataset had several systematic quality issues that required careful handling before analysis.

### Run the pipeline

```bash
pip install pandas numpy
python qa_pipeline.py
```

### Key issues found and resolved

| # | Issue | Rows affected | Action |
|---|---|---|---|
| QA-01 | Unnamed index column (CSV export artifact) | 2,253 | Dropped |
| QA-02 | -1 sentinel values across 10 columns (Glassdoor encoding) | Up to 2,173 | Converted to NaN |
| QA-03 | Salary stored as string ("$30K-$53K (Glassdoor est.)") | 2,253 | Parsed to salary_min, salary_max, salary_avg |
| QA-04 | Company rating embedded in company name ("Acme Corp\n3.2") | 1,981 | Split into company_clean + rating_from_name |
| QA-05 | Founded year outside plausible range | 28 | Set to NaN |
| QA-06 | No seniority column in raw data | — | Derived from job title keywords |

**Result:** 0 critical issues. All 2,253 rows retained with 17 clean columns.


## Statistical Methods

All hypotheses were tested using non-parametric methods appropriate for non-normally distributed salary data:

| Test | Used for |
|---|---|
| Kruskal-Wallis H-test | Multi-group comparisons (location, sector, seniority, company size) |
| Mann-Whitney U-test | Pairwise comparisons (Python vs no Python, Excel vs no Excel) |
| Bonferroni correction | Multiple comparison correction for pairwise tests |
| Spearman correlation | Company rating vs salary (ordinal vs continuous) |
| Cohen's d / η²_H | Effect size measurement |


## Analysis Highlights

### Python signals technical depth (+$3,500)
Analysts with Python listed in job postings earn a statistically significant median premium of $3,500 (Mann-Whitney U, p=0.006, n=2,253). This held across Finance, IT, and Healthcare sectors — the three highest-paying sectors for Python skills.

### Excel signals generalist (−$1,500)
Despite being the most commonly listed skill (40.1% of postings), Excel listing correlates with a *lower* median salary of −$1,500. The market pays for signal quality, not frequency.

### Location is the dominant salary variable
A $50,902 gap exists between the highest-paying state (CA: $88,432) and lowest (UT: $37,530) — same job title, entirely different compensation. The Kruskal-Wallis H statistic of 563.97 (p = 5×10⁻¹¹³) confirms location as the strongest predictor in the dataset.

### Company size and rating don't matter
Company size explains only 0.03% of salary variance (η²_H = 0.03%). Company rating correlation with salary is r = 0.037 — effectively zero. A great Glassdoor rating does not predict higher pay.


## Tech Stack

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![Tableau](https://img.shields.io/badge/Tableau-E97627?style=for-the-badge&logo=tableau&logoColor=white)
![SciPy](https://img.shields.io/badge/SciPy-8CAAE6?style=for-the-badge&logo=scipy&logoColor=white)


## Skills Demonstrated

- Real-world data quality issues — sentinel values, embedded fields, string parsing
- Non-parametric statistical testing with effect size reporting
- Reproducible Python QA pipeline with documented decisions
- Interactive Tableau dashboard design with multi-page navigation
- Business-focused data storytelling (hypothesis → finding → recommendation)


## About

**Ina Louise Magno** — Data Analyst | Chemical Engineering graduate (UPLB)  
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/ina-louise-magno)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/chimkeninasal)
