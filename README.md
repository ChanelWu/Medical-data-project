# Medical Data Analysis — Hospital Readmission Study

Every year, millions of patients are discharged from hospitals — and then come back within 30 days. These readmissions cost the U.S. healthcare system over $26 billion annually and, more importantly, often signal that something went wrong the first time around.

This project asks a simple but important question: **are certain health conditions statistically linked to a patient being readmitted to the hospital?** If so, hospitals could use that information to identify high-risk patients before they leave — and intervene earlier.

To answer that, this project takes a raw medical dataset, cleans it up so it can be trusted, and then runs statistical tests to find which conditions (out of 10 tested) show a meaningful relationship with readmission.

---

## What This Project Does

1. **Cleans messy real-world data** — the raw dataset had missing values, unnamed columns, and extreme outliers that would skew any analysis. The first notebook fixes all of that.

2. **Tests 10 health conditions against readmission rates** — using chi-square tests (a statistical method that checks whether two things are genuinely related, or just coincidentally appear together), the second notebook finds which conditions are statistically linked to patients being readmitted.

3. **Visualizes the patterns** — charts make the relationships visible at a glance, showing how readmitted and non-readmitted patients differ across demographics, lab values, and health history.

---

## The Two Notebooks

### `Cleaning_Medical_data.ipynb` — Making the Data Trustworthy

Before any analysis can be meaningful, the data has to be clean. This notebook handles everything that was wrong with the raw dataset:

- **Unnamed columns** — leftover junk from the original export, dropped entirely
- **Vague survey labels** — 8 patient survey columns were named `Item1` through `Item8`, which tells you nothing. These were renamed to reflect what they actually measure.
- **Missing values** — some patients had no recorded age, income, number of children, or length of stay. Rather than delete those rows, the missing values were filled in using the median (the middle value of everyone else's data — more reliable than the average when data is skewed)
- **Binary fields with gaps** — columns like `Overweight`, `Anxiety`, and `Soft_drink` are yes/no flags. Missing entries were set to 0 (no), which is the appropriate default for these fields
- **Extreme outliers** — a few patients had values so far from everyone else (e.g., unusually high income or vitamin D levels) that they would distort the results. These were identified using the IQR method (a way of measuring how spread out the middle 50% of the data is) and then capped at a reasonable limit using the 3-standard-deviation rule, so the data stays usable without throwing anyone out entirely

By the end of this notebook, the dataset is consistent, complete, and ready to be analyzed.

---

### `Medical_data_EDA_Stats.ipynb` — Finding the Patterns

With clean data in hand, this notebook looks for meaningful relationships.

**The core question:** Is there a statistically significant connection between each health condition and whether a patient was readmitted?

"Statistically significant" means the relationship is unlikely to be a coincidence — the math suggests it's real. The test used here is the **chi-square test**, which compares what we'd expect to see (if readmission and the condition were totally unrelated) to what we actually see in the data. A low p-value (below 0.05, or 5%) means the two are likely genuinely related.

This test was run for 10 health conditions:

| Condition | What It Is |
|---|---|
| High Blood Pressure | Chronically elevated blood pressure |
| Stroke | History of stroke |
| Overweight | Body weight above healthy range |
| Arthritis | Joint inflammation condition |
| Diabetes | Blood sugar regulation disorder |
| Hyperlipidemia | High cholesterol levels |
| Back Pain | Chronic back pain |
| Anxiety | Diagnosed anxiety disorder |
| Reflux Esophagitis | Chronic acid reflux |
| Asthma | Chronic airway condition |

Beyond the statistical tests, the notebook also includes:

- **Distribution charts** (histograms) — showing how values like age, hospital stay length, and vitamin D levels are spread across patients
- **Comparison charts** (box plots, violin plots, strip plots) — showing how readmitted vs. non-readmitted patients differ on key measures
- **Relationship charts** (regression plots, KDE plots) — looking for trends between two numeric variables at once

---

## What This Could Mean for Hospitals

If certain health conditions are reliably linked to readmission, that's actionable information. Hospitals could use findings like these to:

- **Flag high-risk patients before discharge** — a patient with multiple conditions that predict readmission could be automatically surfaced for extra review before they leave
- **Allocate follow-up care more efficiently** — instead of generic post-discharge check-ins for everyone, resources could be directed toward patients who are statistically more likely to return
- **Reduce unnecessary readmissions** — early intervention (a follow-up call, a medication review, a scheduled check-in) is far cheaper and better for the patient than a second hospital stay

This kind of analysis is a stepping stone toward predictive models that could one day be integrated into hospital workflows.

---

## Key Variables

| Variable | Type | Plain English |
|---|---|---|
| `ReAdmis` | Yes/No | Was the patient readmitted to the hospital? |
| `Age` | Number | Patient's age |
| `Income` | Number | Annual household income |
| `Children` | Number | Number of children in the household |
| `Initial_days` | Number | How many days the patient stayed on their first visit |
| `VitD_levels` | Number | Vitamin D level measured in the patient's blood |
| `Soft_drink` | Yes/No | Does the patient regularly drink soft drinks? |
| `Overweight` | Yes/No | Is the patient overweight? |
| `Anxiety` | Yes/No | Does the patient have a diagnosed anxiety disorder? |
| `Item1`–`Item8` | Survey score | Patient responses to satisfaction and health experience questions |

---

## Tech Stack

| Tool | What It's Used For |
|---|---|
| Python 3 | The programming language everything runs in |
| Pandas | Loading, cleaning, and reshaping the data |
| NumPy | Math operations, especially for outlier capping |
| SciPy | Running the chi-square statistical tests |
| Matplotlib | The base layer for creating charts |
| Seaborn | Higher-level charts — boxen plots, violin plots, KDE, regression |
| Jupyter Notebook | Interactive environment for running and documenting the analysis |

---

## How to Run

### What You Need

- Python 3.9 or later
- Jupyter Notebook or JupyterLab

### Setup

```bash
git clone https://github.com/ChanelWu/Medical-data-project.git
cd Medical-data-project

pip install pandas numpy scipy matplotlib seaborn jupyter

jupyter notebook
```

Open the notebooks in this order:

1. `Cleaning_Medical_data.ipynb` — run first to clean the data
2. `Medical_data_EDA_Stats.ipynb` — run second for the analysis and charts

---

## Project Structure

```
Medical-data-project/
├── Cleaning_Medical_data.ipynb     # Data cleaning pipeline
├── Medical_data_EDA_Stats.ipynb    # Statistical analysis and visualizations
└── README.md
```

---

## Built By

**Xueying Wu (Chanel)** — Data Science student, CompTIA Data+ certified.

This project was completed as part of academic coursework in data science and applied statistics.

---

*This project is for educational purposes only. The dataset used is simulated or anonymized and does not represent real patient records. No medical decisions should be made based on this analysis.*
