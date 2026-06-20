# Google Advanced Data Analytics Capstone

**Salifort Motors Workforce Analysis: Employee Turnover Prediction**

## Background Information

Salifort Motors is a fictional French-based alternative energy vehicle manufacturer. Its global workforce of over 100,000 employees research, design, construct, validate, and distribute electric, solar, algae, and hydrogen-based vehicles. Salifort's end-to-end vertical integration model has made it a global leader at the intersection of alternative energy and automobiles.

### Business Case

As a data specialist working for Salifort Motors, you have received the results of a recent employee survey. The senior leadership team has tasked you with analyzing the data to come up with ideas for how to increase employee retention. To help with this, they would like you to design a model that predicts whether an employee will leave the company based on their department, number of projects, average monthly hours, and any other data points you deem helpful.

---

## Approach

This project uses **Logistic Regression** to predict employee turnover. The PACE (Plan, Analyze, Construct, Execute) framework structures the workflow.

1. Data Cleaning — removed 3,008 duplicate rows (20% of data), identified and removed tenure outliers (824 rows) via IQR
2. EDA — boxplots, scatterplots, histograms, and correlation heatmap to explore variable relationships
3. Feature Engineering — ordinal-encoded salary, dummy-encoded department
4. Modeling — logistic regression with 75/25 stratified train-test split
5. Evaluation — confusion matrix, classification report, ROC curve, AUC

---

## Results

| Metric | Weighted Avg | Class 0 (Stayed) | Class 1 (Left) |
|--------|-------------|-------------------|----------------|
| Precision | 0.79 | 0.86 | 0.44 |
| Recall | 0.82 | 0.93 | 0.26 |
| F1 | 0.80 | 0.90 | 0.33 |
| AUC | 0.88 | — | — |
| Accuracy | 0.82 | — | — |

The model catches most employees who stay but misses a large portion of employees who leave (recall 26% on Class 1).

---

## Key Findings

- All employees assigned 7 projects left the company
- A group of employees working 240–315 hours/month had satisfaction near zero
- Employees at the 4-year tenure mark showed unusually low satisfaction
- Promotions were extremely rare and almost never went to employees who left
- No single department had a disproportionately high turnover rate

## Suggestions

- Cap the number of projects at 4–5 per employee
- Investigate the satisfaction drop at the 4-year tenure mark
- Decouple evaluation scores from raw hours worked
- Review and expand promotion pathways
- Clarify overtime expectations through policy or compensation

## Next Steps

Tree-based models (decision tree, random forest, XGBoost) could improve recall on the minority class. Feature engineering (e.g., `overworked` flag) could also help.

---

## Dataset

This project uses the [HR capstone dataset](https://www.kaggle.com/datasets/mfaisalqureshi/hr-analytics-and-job-prediction?select=HR_comma_sep.csv). 14,999 rows, 10 columns.

| Column | Type | Description |
|--------|------|-------------|
| satisfaction_level | float64 | Employee-reported job satisfaction level [0–1] |
| last_evaluation | float64 | Score of employee's last performance review [0–1] |
| number_project | int64 | Number of projects employee contributes to |
| average_monthly_hours | int64 | Average number of hours employee worked per month |
| tenure | int64 | How long the employee has been with the company (years) |
| work_accident | int64 | Whether or not the employee experienced an accident while at work |
| left | int64 | Whether or not the employee left the company |
| promotion_last_5years | int64 | Whether or not the employee was promoted in the last 5 years |
| department | str | The employee's department |
| salary | str | The employee's salary (low, medium, or high) |
