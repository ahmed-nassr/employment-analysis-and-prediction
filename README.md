# Employment Analysis and Prediction

## Project Overview

This collaborative project analyzes employment-related data for more than 73,000 respondents to explore how technical skills, experience, education, salary, demographics, accessibility, and mental-health status are associated with hiring outcomes.

The project combines:

- Data validation and cleaning
- Exploratory data analysis
- Feature engineering and preprocessing
- Machine-learning classification
- Interactive dashboards built with Excel, Tableau, and Power BI

Two classification models—Random Forest and XGBoost—were trained to predict the dataset’s `Employed` target. XGBoost produced the stronger test performance, reaching approximately **79% accuracy** and a **0.78 macro F1-score**.

## Project Objectives

The project investigates the following questions:

- Which applicant characteristics are most strongly associated with hiring outcomes?
- How do technical skills and coding experience relate to hiring?
- Does professional experience have a different relationship with hiring than total coding experience?
- How do education level and professional background relate to hiring and salary?
- How do hiring outcomes vary across age, gender, and country groups?
- Are accessibility and mental-health status associated with different outcomes?
- How does previous salary vary with education and professional experience?
- How accurately can machine-learning models classify the `Employed` outcome?

## Dataset

The project uses the **70K+ Job Applicants Data (Human Resource)** dataset available on Kaggle:

[View the dataset on Kaggle](https://www.kaggle.com/datasets/ayushtankha/70k-job-applicants-data-human-resource)

The data is derived from Stack Overflow Developer Survey responses and contains **73,462 records**.

### Main columns

| Column | Description |
|---|---|
| `AgeAbove35` | Whether the respondent is above 35 years old |
| `Accessibility` | Reported accessibility status |
| `EdLevel` | Highest reported education level |
| `Employment` | Employment status at the time represented by the source data |
| `Gender` | Reported gender |
| `MentalHealth` | Reported mental-health status |
| `MainBranch` | Whether the respondent identifies as a professional developer |
| `YearsCode` | Total years spent coding, including education |
| `YearsCodePro` | Years spent coding professionally |
| `Country` | Respondent’s country |
| `PreviousSalary` | Previous reported salary |
| `HaveWorkedWith` | Technologies and tools used by the respondent |
| `ComputerSkills` | Number of reported technical skills |
| `Employed` | Dataset-defined binary hiring target |

The distinction between `Employment` and `Employed` follows the Kaggle dataset’s framing. Because the derivation of the target is not documented comprehensively, interpretations involving these variables should be made cautiously.

## Project Workflow

### 1. Structural analysis

The raw dataset was inspected to understand:

- Dataset dimensions and column structure
- Data types
- Missing values
- Potential duplicate records
- Categorical values
- Numerical distributions and potential outliers
- Fields requiring transformation

The initial inspection identified:

- An unnecessary index column
- A categorical age field requiring conversion
- 63 missing entries in `HaveWorkedWith`
- A multi-value skills column requiring separation
- Extreme values in coding experience, salary, and skill counts

### 2. Data cleaning

The cleaning process included:

- Renaming the unnamed index as `id`
- Renaming `Age` to `AgeAbove35`
- Encoding the age groups as a binary field
- Converting accessibility and mental-health values into consistent Boolean fields
- Separating the multi-value `HaveWorkedWith` field into a dedicated skills table
- Exporting cleaned respondent and skills datasets

Two cleaned datasets were produced:

- `employment_cleaned.csv`
- `skills.csv`

### 3. Exploratory data analysis

The EDA examined relationships involving:

- Previous salary
- Current employment and the hiring target
- Technical skills
- Total and professional coding experience
- Education level
- Professional-developer status
- Accessibility and mental health
- Age, gender, and country

The analysis used:

- Distribution plots
- Grouped hiring rates
- Correlation analysis
- Cross-tabulations
- Salary comparisons
- Experience bins
- Skill tiers
- Demographic comparisons

### 4. Feature engineering & Preprocessing

The following features were created:

- `Country_grouped`: five most represented countries with remaining countries grouped as `Other`
- `Skills_dist`: low, medium, and high skill tiers
- `has_advanced_degree`: whether the respondent has a master’s degree or PhD
- `skills_x_advanced_degree`: interaction between skill count and advanced education
- `salary_per_year_exp`: previous salary relative to professional experience
- `NoHigherEd`: indicator for respondents without higher education
- `HasTopCountry`: indicator for respondents from one of the most represented countries

Categorical and Boolean variables were then encoded for modeling, and unused or redundant columns were excluded.

The dataset post-preprocessing was produced:
- `employment_preprocessed.csv`

### 5. Machine-learning modeling

The preprocessed data was divided into stratified training and test sets using an 80/20 split.

Two classification models were evaluated:

- Random Forest
- XGBoost

Performance was assessed using:

- Accuracy
- Precision
- Recall
- F1-score
- Class-level performance
- Feature importance

## Model Performance

| Model | Accuracy | Macro F1-score | Weighted F1-score |
|---|---:|---:|---:|
| Random Forest | 76% | 0.76 | 0.76 |
| XGBoost | 79% | 0.78 | 0.79 |

The test set contained **14,693 respondents**.

### XGBoost classification results

| Class | Precision | Recall | F1-score |
|---|---:|---:|---:|
| 0 | 0.79 | 0.73 | 0.76 |
| 1 | 0.78 | 0.84 | 0.81 |

XGBoost produced the stronger overall performance, particularly in recall for the positive class.

## Selected Analytical Findings

- Approximately **53.6%** of respondents have `Employed = 1`.
- Average previous salary is approximately **$67,750**.
- Approximately **88.3%** of respondents were already working according to the `Employment` field.
- The data contains **116 unique reported technologies and skills**.
- Hiring rates generally increase through moderate experience levels before declining among the most experienced groups.
- Greater professional experience is generally associated with higher previous salary.
- Skill level appears more strongly associated with hiring outcomes than years of experience alone.
- Approximately **0.8%** of records report more professional coding experience than total coding experience. These contradictory derived values were treated as inconsistent in analyses of non-professional experience.
- The sample is demographically imbalanced: approximately **93.3%** of respondents are men.
- Approximately **35%** of respondents are above 35 years old.
- Approximately **91.7%** of respondents identify as professional developers.

These findings describe patterns within this dataset and do not establish that any characteristic causes a person to be hired.

## Dashboards

The project includes dashboards created with three business-intelligence tools.

### Excel — Hiring Overview

Provides an overview of:

- Total respondents
- Total hired
- Overall hiring rate
- Average previous salary
- Hiring by education
- Hiring by gender
- Hiring by age group
- Countries with the largest numbers of hired respondents

### Tableau — Education and Experience

Explores:

- Hiring rate across coding-experience levels
- Hiring rate by education
- Most commonly reported skills
- Coding experience versus number of skills
- Differences across hiring and age segments

### Power BI — Salary and Career Analysis

Presents:

- Average and highest previous salary
- Average professional experience
- High-earner percentage
- Average salary by country
- Average salary by education level
- Hiring rate by professional experience
- Salary versus professional experience

The dashboards include filters that allow users to examine selected demographic, educational, geographic, and employment groups.

## Technologies Used

### Data analysis and modeling

- Python
- pandas
- NumPy
- Matplotlib
- Seaborn
- scikit-learn
- XGBoost
- Jupyter Notebook

### Dashboards and reporting

- Microsoft Excel
- Tableau
- Microsoft Power BI
- PDF reporting

## How to Run the Project

### 1. Clone the repository

```bash
git clone https://github.com/ahmed-nassr/employment-analysis-and-prediction.git
cd employment-analysis-and-prediction
```

### 2. Create and activate a virtual environment

```bash
python -m venv .venv
```

On Windows:

```bash
.venv\Scripts\activate
```

### 3. Install the required libraries

```bash
python -m pip install -r requirements.txt
```

### 4. Run the notebooks in order

1. `structural_analysis.ipynb`
2. `data_cleaning.ipynb`
3. `eda.ipynb`
4. `feature_eng_and_preprocessing.ipynb`
5. `modeling.ipynb`

Run the notebooks from the project directory and confirm that their data paths match the local project structure.

### 5. Open the dashboards

- Open `.xlsx` dashboard files with Microsoft Excel.
- Open the `.twbx` workbook with Tableau Desktop or Tableau Reader.
- Open the `.pbix` report with Microsoft Power BI Desktop.

## Limitations

- The Kaggle dataset is derived from survey data and does not represent all applicants or the overall labor market.
- The sample contains substantial demographic and geographic imbalance.
- Survey responses may contain estimation, interpretation, or reporting errors.
- The exact construction of the `Employed` target and some preprocessing performed before publication are not documented comprehensively.
- Approximately 0.8% of respondents reported more professional coding experience than total coding experience.
- Salary comparisons between countries may reflect cost-of-living, currency, economic, and labor-market differences.
- Model predictions identify statistical patterns in the supplied data; they should not be used as automated hiring decisions.
- Demographic, accessibility, and mental-health variables require particular care because predictions involving them may reproduce historical or sampling biases.
- Feature importance does not establish causality.

## Responsible Use

This project is an educational analysis, not a production recruitment system.

A hiring model should not make decisions about real applicants without:

- Clear and validated target definitions
- Representative and relevant training data
- Formal fairness evaluation
- Legal and ethical review
- Explainability and human oversight
- Continuous monitoring for discrimination and performance drift

## Conclusion

This project demonstrates an end-to-end analytical workflow that moves from raw-data inspection and cleaning to exploratory analysis, feature engineering, machine-learning evaluation, and interactive business-intelligence dashboards.

The results suggest that technical skills, experience, education, salary, and demographic factors have different relationships with the dataset’s hiring target. XGBoost achieved the strongest predictive performance, but the dataset’s limitations and the sensitivity of employment decisions make responsible interpretation essential.