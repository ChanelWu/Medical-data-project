Medical Data Analysis — Hospital Readmission Study

End-to-end data pipeline: cleaning → statistical testing → exploratory analysis to identify patient factors associated with hospital readmission.


Project Overview
This project analyzes a real-world medical dataset to explore which patient health factors may influence hospital readmission rates. The workflow follows professional data science practice — raw data is cleaned and prepared first, then statistical tests and visualizations are applied to draw evidence-based insights.

Notebooks
1. Cleaning_Medical_data.ipynb — Data Preparation
Transforms raw medical data into an analysis-ready dataset through:

Dropping unnamed index columns and renaming 8 patient survey items (Item1–Item8) to meaningful labels (Timely Admission, Timely Treatment, Reliability, etc.)
Handling missing values using median imputation for skewed continuous variables (Age, Income, Children, Initial Days) and zero-fill for binary flags (Soft Drink, Overweight, Anxiety)
Detecting outliers using the IQR method with boxen plots
Capping outliers using the 3-standard deviation rule for Children, Income, and Vitamin D levels to preserve data without distortion

2. Medical_data_EDA_Stats.ipynb — Statistical Analysis & EDA
Performs hypothesis testing and visualization across three levels:
Chi-Square Tests — tests independence between hospital readmission (ReAdmis) and 10 binary health conditions at 95% confidence level:

High Blood Pressure, Stroke, Overweight, Arthritis, Diabetes, Hyperlipidemia, Back Pain, Anxiety, Reflux Esophagitis, Asthma

Univariate Analysis — distribution analysis of:

Continuous variables: Initial Days, Vitamin D Levels (histograms with KDE)
Categorical variables: Timely Treatment, Hours of Treatment (count plots)

Bivariate Analysis — relationship exploration using:

Regression scatter plots (Initial Days vs Vitamin D Levels)
Box plots, violin plots, strip plots, KDE plots (readmission vs continuous variables)
Bar plots (readmission vs categorical variables)


Key Variables
VariableTypeDescriptionReAdmisBinaryWhether patient was readmittedInitial_daysContinuousLength of initial hospital stayVitD_levelsContinuousPatient Vitamin D levelsHighBloodBinaryHigh blood pressure diagnosisDiabetesBinaryDiabetes diagnosisAnxietyBinaryAnxiety diagnosisTimely_treatmentCategoricalPatient survey scoreHours_of_treatmentCategoricalPatient survey score

Tech Stack
ToolPurposePython 3Core languagePandasData manipulationNumPyNumerical operationsSciPyChi-square statistical testsMatplotlibBase visualizationsSeabornStatistical plots

How to Run
bash# Clone the repo
git clone https://github.com/ChanelWu/Medical-data-project.git
cd Medical-data-project

# Install dependencies
pip install pandas numpy scipy matplotlib seaborn jupyter

# Run notebooks in order
jupyter notebook Cleaning_Medical_data.ipynb
jupyter notebook Medical_data_EDA_Stats.ipynb

Run Cleaning_Medical_data.ipynb first — it produces the cleaned dataset used by the EDA notebook.


Project Structure
Medical-data-project/
├── Cleaning_Medical_data.ipynb    # Data cleaning pipeline
├── Medical_data_EDA_Stats.ipynb   # Statistical analysis & EDA
├── medical_raw_data.csv           # Raw input data (if included)
└── medical_clean.csv              # Cleaned output data (generated)

Skills Demonstrated

Real-world data cleaning with principled missing value handling
Outlier detection and treatment using IQR and standard deviation methods
Chi-square hypothesis testing with p-value interpretation
Univariate and bivariate statistical visualization
End-to-end reproducible data science workflow in Python


Built By
Xueying Wu (Chanel) — Data Science student, CompTIA Data+ certified.

This project is for educational and portfolio purposes only. Data does not represent real patients.
