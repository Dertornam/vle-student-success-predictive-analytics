---
title: Data Dictionary
layout: default
permalink: /data-dictionary/
---

# Data Dictionary — Predictive Analytics for Student Success  
Using Virtual Learning Environment (VLE) Data

This dictionary documents the main fields used in the analysis.  
The analytic unit is student–module.

---

## Identifiers and context
**student_id**  
Unique identifier for a student.

**module_code**  
Identifier for the module.

**presentation_code**  
Module run or term identifier.

**imd_band**  
Index of Multiple Deprivation band.  
Used here as a proxy for socioeconomic context.

---

## Engagement features
**total_clicks**  
Definition: Total number of VLE click events for the student within the module presentation.  
Interpretation: Overall engagement volume.

**days_active**  
Definition: Count of distinct days with at least one VLE interaction during the module presentation.  
Interpretation: Engagement consistency.  
Operational use: Primary early-warning signal.

---

## Outcome variables
**final_result**  
Categorical academic outcome.  
Common categories include Distinction, Pass, Fail, Withdrawn.

**result_score**  
Numeric or ordinal encoding of outcome for correlation work.  
Used to measure direction and strength of association with engagement.

**risk_group**  
Binary outcome for early-warning modeling.  
Definition: “Success” vs “At-Risk.”  
Success = Pass or Distinction.  
At-Risk = Fail or Withdrawn.

---

## Model outputs (reporting fields)
**predicted_risk_probability**  
Predicted probability of being “At-Risk” from the logistic regression model.

**risk_flag_mid_module**  
Operational flag based on the ~33 Days Active threshold at the midpoint.  
Used for dashboarding and advisor workflows.

---

## Practical interpretation notes
Total clicks can be noisy.  
It depends on how a module is designed.

Days Active is more stable.  
It reflects routine participation.

That is why Days Active is prioritized as a metric.  
It supports clean policy and consistent intervention design.
