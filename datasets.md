---
title: Datasets
layout: default
permalink: /datasets/
---

# Datasets — Predictive Analytics for Student Success  
Using Virtual Learning Environment (VLE) Data

This project is based on Open University Virtual Learning Environment data.  
The working unit is student–module, created by aggregating raw clickstream logs.

---

## Dataset overview
The analysis file contains 32,044 student–module records.  
Each record represents one student’s engagement and outcome within one module presentation.

Core elements included in this project:  
- Clickstream activity aggregated to Total Clicks.  
- Daily participation aggregated to Days Active.  
- Registration and student context fields.  
- Final academic outcomes (Distinction, Pass, Fail, Withdrawn).

This structure is ideal for early-warning analytics.  
It aligns directly with the way modules run and interventions are deployed.

---

## Directory structure used in this repository
**Raw data:** `data/raw/`  
Raw source tables and extracts live here.

**Processed data:** `data/processed/`  
Cleaned and merged student–module files live here.

**Outputs:** `reports/`  
Figures, executive summary, and reporting assets live here.

---

## Data preparation summary
I built the student–module analytic file by joining and aggregating VLE event logs.  
I then engineered features that make engagement measurable and comparable across students.

I treated missing engagement as meaningful behavior in many cases.  
In a VLE context, “no clicks” often represents non-participation rather than random missingness.

---

## Output files referenced in the report
**Figures:** `reports/figures/`  
- `vle_engagement_vs_final_result_boxplot.png`  
- `correlation_heatmap_engagement_vs_outcome.png`  
- `predictive_power_consistency_vs_volume.png`  
- `probability_of_success_vs_days_active.png`  
- `digital_effort_gap_by_imd.png`

---

## Notes for reuse
If you want to reproduce this with your institution’s LMS data, the mapping is direct.  
VLE clicks map to LMS event logs, and Days Active maps to distinct login or activity dates.

The key is consistency.  
You do not need perfect click taxonomy to get value from Days Active.
