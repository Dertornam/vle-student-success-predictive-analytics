---
title: Predictive Analytics for Student Success
layout: default
---

# Predictive Analytics for Student Success  
Using Virtual Learning Environment (VLE) Data

**Tools:** Python (pandas, NumPy, scikit-learn, matplotlib), Jupyter Notebook

<style>
.port-btn{
  display:inline-block;
  padding:.6rem 1rem;
  margin:.25rem .4rem 0 0;
  border-radius:8px;
  background:#0366d6;
  color:#fff !important;
  text-decoration:none !important;
  border:1px solid rgba(0,0,0,.08);
  box-shadow:0 1px 2px rgba(0,0,0,.05);
  font-weight:600;
}
.port-btn:hover{ filter:brightness(0.95); }
</style>

<div style="margin: 1rem 0;">
  <a class="port-btn" href="{{ '/executive-summary-student-success' | relative_url }}">Executive Summary</a>
  <a class="port-btn" href="{{ '/statistical-tables-student-success' | relative_url }}">Statistical Tables</a>
  <a class="port-btn" href="{{ '/datasets-student-success' | relative_url }}">Datasets</a>
  <a class="port-btn" href="{{ '/data-dictionary-student-success' | relative_url }}">Data Dictionary</a>
  <a class="port-btn" href="{{ '/reproducibility-student-success' | relative_url }}">Reproducibility</a>
</div>

<style>
.page-content img{
  max-width: 100%;
  height: auto;
  border-radius: 10px;
  box-shadow: 0 1px 2px rgba(0,0,0,.06);
  margin: .5rem 0 1rem 0;
}
</style>

---

## Introduction & Project Objective
I built a practical early-warning framework using VLE engagement behavior.  
The goal was to detect risk early enough for advising and course teams to act.

This project uses 32,044 student–module records.  
It includes clickstream traces, registration context, and academic outcomes.

The “So what?” is operational.  
If we can quantify “showing up,” we can trigger outreach before grades collapse.

---

## What I built end-to-end
I started from raw Open University VLE tables.  
I cleaned and joined them into an analysis-ready student–module file.

I engineered engagement markers like Total Clicks and Days Active.  
I then modeled “Success vs At-Risk” and translated results into thresholds and workflows.

I treated this as an institutional analytics deliverable.  
Not just a notebook.

---

## Key questions this analysis answers
1. How is VLE engagement related to final academic results?  
2. Is consistency (Days Active) more predictive than raw intensity (Total Clicks)?  
3. Is there a clear tipping point where non-engagement becomes dangerous?  
4. Are there digital-effort gaps by socioeconomic context (IMD)?

---

## Data & outcome definition
Unit of analysis is student–module.  
Each row represents one student in one module presentation.

The academic outcome is the final result category.  
For modeling, I collapsed outcomes into “Success” vs “At-Risk.”

“Success” means the student passes.  
“At-Risk” means fail or withdraw.

This framing matches how student-success teams work.  
They intervene before the final outcome is locked in.

---

## Methodology
**Data engineering.**  
I aggregated click events to student–module totals and daily activity counts.

**Feature engineering.**  
Total Clicks captures volume.  
Days Active captures consistency of participation.

**Exploratory analysis.**  
I compared engagement distributions by outcome.  
I quantified relationships using correlations and group summaries.

**Predictive modeling.**  
I fit logistic regression for interpretability.  
I added a simple tree-based split to surface a usable threshold.

**Evaluation.**  
I prioritized recall for the at-risk group.  
That reflects outreach goals.

---

## Key finding 1: Engagement forms a “ladder of success”
Total VLE clicks rise steadily as final results improve.  
This produces a clean behavioral gradient from Withdrawn to Distinction.

### Visual: VLE engagement by final result
![VLE Engagement vs Final Academic Result]({{ '/reports/figures/vle_engagement_vs_final_result_boxplot.png' | relative_url }})

Students who achieve a Distinction interact far more than students who fail or withdraw.  
This is the behavioral signal an early-warning model can exploit.

### Table: Mean engagement by final result
| Final Result | Mean Clicks | Median Clicks | Std. Deviation |
|--------------|------------:|--------------:|----------------:|
| Distinction  | 3,106.43    | 2,218.0       | 2,978.98        |
| Pass         | 2,171.11    | 1,503.0       | 2,137.91        |
| Fail         |   840.17    |   418.5       | 1,260.85        |
| Withdrawn    |   888.38    |   364.0       | 1,468.34        |

The practical meaning is simple.  
Engagement is not just “nice to have.”  
It is an observable precursor to academic outcomes.

---

## Key finding 2: Consistency beats intensity
Days Active correlates more strongly with outcome than Total Clicks.  
Showing up across more days matters more than bursts of activity.

### Visual: Correlation structure
![Correlation Matrix]({{ '/reports/figures/correlation_heatmap_engagement_vs_outcome.png' | relative_url }})

In this dataset, Days Active relates more strongly to the Result Score (r = 0.55).  
Total Clicks is weaker (r = 0.35).

That reads like a gym analogy.  
Going three times a week beats one intense day a month.

### Visual: Standardized coefficients in a joint model
![Predictive Power: Consistency vs Volume]({{ '/reports/figures/predictive_power_consistency_vs_volume.png' | relative_url }})

Days Active stays strongly positive when both features enter the model.  
Total Clicks turns slightly negative once consistency is accounted for.

This is the “cramming penalty.”  
A lot of clicks in a few late bursts can signal distress, not strength.

---

## Key finding 3: The tipping point is operationally usable
I trained a logistic regression to classify “Success” vs “At-Risk.”  
The model achieves about 74% accuracy and about 77% recall for the at-risk group.

A simple decision split identifies a threshold around 32.5 active days.  
This gives leadership a concrete metric, not an abstract score.

### Visual: Probability of success vs Days Active
![Probability of Success vs Days Active]({{ '/reports/figures/probability_of_success_vs_days_active.png' | relative_url }})

If a student has not reached ~33 active days by mid-module, risk is elevated.  
This is where proactive outreach pays off.

Think of it like a smoke alarm.  
You want the alarm before the fire spreads.

---

## Key finding 4: Digital effort gap by socioeconomic status (IMD)
I examined engagement by Index of Multiple Deprivation (IMD) band.  
The least deprived group shows higher average engagement.

### Visual: Digital effort by IMD band
![Digital Effort Gap]({{ '/reports/figures/digital_effort_gap_by_imd.png' | relative_url }})

Least deprived students average about 2,465 clicks.  
Most deprived students average about 2,192 clicks.

That is a 12.5% effort gap.  
It suggests digital friction that may be outside academic ability.

This is not a “blame the student” story.  
It is a “remove barriers” story.

---

## Dataset profile & data quality notes
The analytic file contains 32,044 student–module records.  
Each record is aggregated from raw clickstream events.

Engagement measures are heavy-tailed.  
That is why medians matter as much as means.

Outcome categories include Distinction, Pass, Fail, and Withdrawn.  
For the risk model, Fail and Withdrawn are treated as “At-Risk.”

If missingness exists in activity logs, it is meaningful.  
It often represents non-participation rather than random gaps.

---

## Diagnostics & robustness checks
Engagement is not normally distributed.  
It clusters near zero with a long right tail.

That makes effect sizes easier to interpret with robust thinking.  
The main conclusions hold because they rely on strong separation patterns and consistency signals.

Total Clicks becoming slightly negative in the joint model is interpretable.  
It reflects time-pattern effects that “Days Active” captures better.

This is why Days Active is the better policy metric.  
It is also harder to game.

---

## Leadership implications
This project supports three institutional moves.  
Each one is easy to implement if you already have LMS logs.

1) Use Days Active as the primary early-warning metric.  
Treat ~33 days by mid-module as a high-risk flag.

2) Build interventions around consistency, not volume.  
Design nudges that increase “days present,” not “click count.”

3) Track digital-effort gaps by IMD as an operational equity signal.  
Use it to justify investments in device access, connectivity, and learning support.

---

## “So what?” for the institution
This framework surfaces risk before mid-module.  
That shifts the institution from reactive to preventive.

Advisors can triage outreach using a simple behavioral threshold.  
Leadership can track risk rates and IMD engagement gaps as leading indicators.

In practice, fewer failures feel “sudden.”  
More support lands while students can still recover.

---

## Methods and tech stack
I used Python in Jupyter notebooks.  
Core libraries were pandas, NumPy, scikit-learn, and matplotlib.

Methods include cleaning and feature engineering from raw VLE tables.  
I used descriptive statistics, correlation analysis, logistic regression, and a simple thresholding tree.

The modeling choice is deliberate.  
Interpretability matters for institutional adoption.

---

## Repository and outputs
All code skeletons, figures, and reports live in this repository.  
Figures and the executive summary are under `reports/`.

Raw or source-like data assets live under `data/raw/`.  
Cleaned and modeled extracts can live under `data/processed/`.

---

## Contact & Links
<div class="contact-links">
   <a class="port-btn"
     href="https://www.linkedin.com/in/derrick-dzormeku-mba-75288644"
     target="_blank" rel="noopener">
    LinkedIn
  </a>

   <a class="port-btn"
     href="https://mail.google.com/mail/?view=cm&fs=1&to=d.double76@icloud.com&su=Portfolio%20inquiry%20%E2%80%93%20Derrick%20Dzormeku&body=Hi%20Derrick,%0D%0A%0D%0AI%27m%20reaching%20out%20about%20your%20analytics%20portfolio.%20Could%20we%20schedule%20a%20brief%20call%3F"
     target="_blank" rel="noopener">
    Email
  </a>

  <a class="port-btn"
     href="https://dertornam.github.io/higher-ed-analytics-portfolio/"
     target="_blank" rel="noopener">
    Main Portfolio
  </a>

  <a class="port-btn" href="{{ '/resume.pdf' | relative_url }}">View Resume</a>
</div>

<style>
.contact-links {
  margin-top: 0.75rem;
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
}

.port-btn {
  display: inline-block;
  background: #0066cc;
  color: #ffffff !important;
  padding: 0.75rem 1.75rem;
  border-radius: 12px;
  font-weight: 700;
  text-decoration: none;
  font-size: 1rem;
  text-align: center;
}

.port-btn:hover {
  background: #0053a6;
}
</style>

This project is designed as a portfolio example of how predictive analytics, institutional research, and student-success strategy can be integrated.
