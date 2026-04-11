# HR Data Project – Compensation & Data Quality

End-to-end compensation analysis on a real HR CSV dataset: data quality audit, outlier detection, salary analytics, and gender pay gap breakdown.

## Objectives

- Audit data quality (missing values, duplicates, business-rule violations, outliers)
- Analyse compensation across departments, grades, and gender
- Quantify and visualise the gender pay gap at global and granular levels
- Surface absenteeism patterns and their relationship to salary

## Notebook structure

| Section | Description |
|---------|-------------|
| 1. Data Loading & Overview | Shape, dtypes, head, descriptive statistics |
| 2. Data Quality | Missing values & duplicates · IQR salary outlier detection · Business-rule checks (grade salary floors, negative values) |
| 3. Compensation Analysis | Salary distribution · Median salary by grade · Salary by department (table + boxplot) · Salary vs. experience (scatter + Pearson r) |
| 4. Gender Pay Gap | Global gap (mean/median + violin) · Gap by department and grade (diverging bar charts) |
| 5. Absenteeism | Mean absences by department · Absences vs. salary scatter |
| 6. Summary | Key findings table + recommended next steps |

## Dataset

**File:** `hr_dataset.csv` — 300 employees, 7 columns

| Column | Type | Description |
|--------|------|-------------|
| `employee_id` | int | Unique employee identifier |
| `department` | str | Finance, HR, Marketing, Tech |
| `grade` | str | G1 (junior) → G5 (senior) |
| `salary` | int | Annual gross salary (€) |
| `gender` | str | M / F |
| `years_experience` | int | Total years of professional experience |
| `absences` | int | Number of absence days |

## Business rules validated

| Rule | Expected |
|------|----------|
| Salary | > 0 |
| Grade salary floors | G1 ≥ 25k · G2 ≥ 35k · G3 ≥ 45k · G4 ≥ 55k · G5 ≥ 70k |
| years_experience | ≥ 0 |
| absences | ≥ 0 |
| grade | one of G1–G5 |

## Stack

- Python 3
- pandas, numpy
- matplotlib, seaborn

## Files

```
hr_data_project.ipynb   # main notebook
hr_dataset.csv          # source data (300 employees)
```
