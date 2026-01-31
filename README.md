# Predictive Analytics for Student Success using VLE Data

This project uses Virtual Learning Environment (VLE) interaction data to build an early-warning view of student success and withdrawal risk.

The analysis focuses on two core behavioral markers:
1. How often students are active (Days Active – consistency).
2. How much they click when they are active (Total Clicks – intensity).

The dataset includes 32,044 student–module records and supporting tables from an online program:
`studentInfo.csv`, `studentRegistration.csv`, `courses.csv`, `assessments.csv`, `studentAssessment.csv`, `studentVle.csv`, and `vle.csv`.

Key findings are summarized in `reports/Executive_Summary_Predictive_Analytics.md` and illustrated in the figures in `reports/figures/`.

## Highlights

Withdrawal rate in the sample is 30.1%.  
Students who earn Distinction show much higher engagement than those who fail or withdraw.  
Days Active is a stronger predictor of success than Total Clicks (correlation 0.55 vs 0.35).  
A logistic regression model reaches about 74% accuracy and 77% recall for at-risk students.  
A consistency threshold around 33 active days marks a sharp rise in probability of success.  
Students from more deprived IMD bands show about a 12.5% engagement gap compared with affluent peers.

The goal of the project is to show how a vice provost, dean, or institutional research team could:
- Build an early-warning system around simple digital markers.
- Set hard thresholds for advisor outreach (for example, fewer than 33 active days).
- Audit equity gaps in digital engagement and target support.

## Project layout

`data/raw/` stores the original CSV files for VLE, students, registrations, and assessments.  
`reports/Executive_Summary_Predictive_Analytics.md` contains the narrative report and tables.  
`reports/figures/` contains the visuals used in the report:
- `vle_engagement_vs_final_result_boxplot.png`
- `predictive_power_consistency_vs_volume.png`
- `correlation_heatmap_engagement_vs_outcome.png`
- `probability_of_success_vs_days_active.png`
- `digital_effort_gap_by_imd.png`

`requirements.txt` lists the Python packages used for analysis.

## How to reproduce the analysis (high level)

1. Load the raw CSVs from `data/raw/`.
2. Join student, registration, and VLE tables to build a student–module panel.
3. Engineer engagement features such as Total Clicks and Days Active per module.
4. Derive a Result Score and a binary “Success vs At-Risk” outcome.
5. Explore relationships between engagement and outcomes with the provided visualizations.
6. Fit logistic regression and tree-based models and evaluate performance.
7. Translate thresholds and patterns into policy and advising rules for leadership.
