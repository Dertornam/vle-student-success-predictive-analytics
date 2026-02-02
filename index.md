---
title: ## Predictive Analytics for Student Success
layout: default
---

**Tools:** Python (Pandas, NumPy, Scikit-learn, Matplotlib), Jupyter Notebook

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
  <a class="port-btn" href="{{ '/feature-engineering-student-success' | relative_url }}">Feature Engineering</a>
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
The goal of this project was to determine whether early, simple engagement behavior in a Virtual Learning Environment (VLE)—specifically Days Active and Total Clicks—can predict student success outcomes at the student–module level. I aimed to answer the “So What?” for a vice provost or student-success leader: Can we detect risk before mid-module using signals that are easy to track and operationalize?

## Methodology
**Data Acquisition:** The analysis is based on the Open University VLE dataset and includes 32,044 student–module records built from clickstream, registration, and outcome tables.  
**Data Engineering:** I aggregated raw VLE clickstream events to student–module totals and engineered engagement features such as Total Clicks (volume) and Days Active (consistency), then joined those features to final outcomes (Distinction, Pass, Fail, Withdrawn).  
**Modeling Framework:**  
**Descriptive Analysis:** To quantify engagement differences across final result categories.  
**Correlation Analysis:** To compare the strength of consistency (Days Active) versus intensity (Total Clicks) against outcome score.  
**Logistic Regression:** To classify “Success” versus “At-Risk” and quantify interpretable effects.  
**Decision-Tree Thresholding:** To identify a practical tipping point for early-warning workflows.

## Key Findings & Interpretation
### A. Engagement Stratification (Descriptive Results)  
**Results:** Mean clicks rise sharply across outcomes (Distinction 3,106; Pass 2,171; Fail 840; Withdrawn 888).  
**Interpretation:** Engagement forms a clear “ladder of success” from Withdrawn to Distinction.  
**Conclusion:** VLE behavior contains enough separation to support early identification of risk, especially when viewed as consistency rather than raw volume.

### Visual: VLE engagement by final result
![VLE Engagement vs Final Academic Result]({{ '/reports/figures/vle_engagement_vs_final_result_boxplot.png' | relative_url }})

### B. Consistency Dominates Intensity (Correlation + Joint Model)  
**Results:** Days Active relates more strongly to Result Score (r = 0.55) than Total Clicks (r = 0.35).  
**Interpretation:** Showing up across more days matters more than doing many clicks in a few bursts.  
**Conclusion:** Days Active is the better institutional metric because it captures steady participation and is less sensitive to “cramming” behavior.

### Visual: Correlation and relative predictive power
![Correlation Matrix]({{ '/reports/figures/correlation_heatmap_engagement_vs_outcome.png' | relative_url }})

![Predictive Power: Consistency vs Volume]({{ '/reports/figures/predictive_power_consistency_vs_volume.png' | relative_url }})

### C. The Early-Warning Tipping Point (Thresholding)  
**Results:** The logistic model reaches about 74% accuracy and 77% recall for the at-risk group, and a simple tree split identifies a tipping point around 32.5 Days Active.  
**Interpretation:** Students below ~33 active days by mid-module fall into a high-risk zone where the probability of success drops meaningfully.  
**Conclusion:** A single, explainable threshold can anchor advisor workflows and dashboards without requiring complex scoring systems.

### Visual: Probability of success vs Days Active
![Probability of Success vs Days Active]({{ '/reports/figures/probability_of_success_vs_days_active.png' | relative_url }})

### D. Digital Effort Gap (IMD)  
**Results:** Least deprived students average about 2,465 clicks versus about 2,192 clicks in the most deprived group (≈12.5% gap).  
**Interpretation:** Lower-income students may face digital friction that depresses engagement even before academic performance is fully visible.  
**Conclusion:** IMD engagement gaps can be tracked as a leading equity indicator and used to justify targeted digital support.

### Visual: Digital effort by IMD
![Digital Effort Gap]({{ '/reports/figures/digital_effort_gap_by_imd.png' | relative_url }})

## Visual Highlights
**Outcome Ladder:** The boxplot shows a strong monotonic shift in engagement across final results, indicating that VLE activity is not noise but a structured behavioral pattern.  
**Cramming Penalty:** In the joint model, Total Clicks becomes slightly negative once Days Active is controlled, suggesting that last-minute high-volume activity is often a distress signal rather than a strength signal.

## Final Recommendations (The “So What?”)
**Operational Early-Warning:** Use Days Active as the primary metric and adopt the ~33-day threshold at mid-module as a hard trigger for outreach.  
**Consistency-Based Interventions:** Design nudges and course routines to increase “days present” rather than clicks, because consistency is the strongest predictor of success.  
**Digital Equity Monitoring:** Track engagement by IMD as a leading indicator. If gaps widen, respond with targeted support (device access, connectivity support, structured check-ins, digital skills help) before academic damage accumulates.

## Dataset Profile & Data Quality Notes
The analytic file contains 32,044 student–module records derived from raw VLE event logs joined to registration and outcome tables.
Engagement variables are heavy-tailed, so medians are substantially lower than means, which is expected in clickstream data.
For modeling, outcomes were collapsed into a binary operational label: Success (Pass/Distinction) versus At-Risk (Fail/Withdrawn), aligned with student-success intervention goals.

## Additional Quantification of the Visual Story
The mean engagement gradient is large enough to be operationally meaningful. Distinction students average roughly 3.7× the clicks of Fail students, and Pass students average roughly 2.6× the clicks of Fail students, reinforcing that engagement is a leading behavioral marker, not a subtle effect.

The correlation contrast supports the same story using an effect-size lens. Days Active (r = 0.55) is about 57% stronger than Total Clicks (r = 0.35) in its relationship to outcome score, which is why consistency should be the executive-facing metric.

The IMD gap can be expressed as a simple executive ratio. Students in the most deprived band show about 0.89× the click volume of the least deprived band, which points to a measurable engagement disadvantage that can be monitored term-over-term.

## Model Diagnostics & Robustness Checks
Because clickstream engagement is zero-inflated and heavy-tailed, linear assumptions do not hold cleanly for raw counts, which is why the core decision logic is based on a stable consistency feature and a classification framing rather than a single linear outcome model.

The key robustness point is interpretability. The model’s value is not only predictive performance, but the fact that the strongest signal is Days Active, which is straightforward to measure, resistant to outliers, and easily translated into policy and workflow.

## Interaction Insight: Where Risk Concentrates Most
The practical risk concentration shows up when you combine low consistency with weaker socioeconomic context. Students in lower IMD bands who also fail to build routine engagement early in the module represent the highest-yield outreach population because they face both behavioral risk (low Days Active) and structural friction (lower average digital effort).

This is the student-success “pressure point” the visuals are hinting at. It is not only academic ability. It is the combination of low early routine and higher friction that produces the most consistent elevation in risk.

## Practical Interpretation of the ~33-Day Threshold
The ~33-day threshold sounds abstract until you translate it into workflow language. If a module is roughly half complete and a student has not logged meaningful activity on at least 33 distinct days, the probability curve indicates they are already behind the participation rhythm that typically supports passing.

That is why this threshold works as an early-warning trigger. It signals “routine is missing,” which is exactly what advising and course teams can influence with timely outreach.

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
    Other Portfolios
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

This project is designed as a portfolio.
