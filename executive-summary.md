---
title: Executive Summary — Predictive Analytics for Student Success
layout: default
---

# Executive Summary — Predictive Analytics for Student Success  
Using Virtual Learning Environment (VLE) Data

**Project purpose.**  
I built an early-warning framework that uses simple VLE behavior signals to flag students at risk early enough for outreach to matter. The institutional goal is prevention. The operational goal is a clear trigger that advising and course teams can use without debating model details.

**Data basis.**  
The analysis uses 32,044 student–module records. The dataset includes clickstream activity and academic outcomes (Distinction, Pass, Fail, Withdrawn). For intervention logic, I grouped outcomes into “Success” (Pass/Distinction) versus “At-Risk” (Fail/Withdrawn) because that maps cleanly to student-success workflows.

---

## What leadership can act on immediately
**Early-warning metric.**  
Days Active is the strongest, most actionable engagement signal. It performs better than Total Clicks because it captures consistency rather than bursts of activity.

**Operational threshold.**  
A decision-tree split identifies a tipping point at about 32.5 active days. In practice, I treat this as ~33 days. Students who have not reached ~33 active days by mid-module fall into a high-risk zone.

**Model performance (for risk triage).**  
A logistic regression classifying “Success vs At-Risk” reaches about 74% accuracy and about 77% recall for the at-risk group. Recall is emphasized because missing a struggling student is costlier than sending an extra check-in message.

---

## Key results in plain language
**1) Engagement shows a “ladder of success.”**  
Average total clicks rise sharply as outcomes improve. Mean clicks are about 3,106 for Distinction, 2,171 for Pass, 840 for Fail, and 888 for Withdrawn. The behavioral gap between Pass and Fail is large enough to support early identification.

**2) Consistency beats intensity.**  
Days Active relates more strongly to outcome than Total Clicks. In correlation terms, Days Active relates to Result Score at r = 0.55, while Total Clicks relates at r = 0.35. When both enter a model, Days Active remains strongly positive, while Total Clicks becomes slightly negative, reflecting a “cramming penalty.”

**3) A simple, explainable trigger exists.**  
The probability of success rises steadily with Days Active. The ~33-day threshold is a usable decision point for advisors and instructors because it is interpretable and stable.

**4) Digital effort gaps exist by socioeconomic context (IMD).**  
Students in the least deprived areas average about 2,465 clicks. Students in the most deprived areas average about 2,192 clicks. That is a 12.5% effort gap, suggesting digital friction for lower-income students that may require institutional support rather than purely academic intervention.

---

## Key metrics (ready to copy into a slide)
**Dataset.** 32,044 student–module records.  
**Mean clicks (by final result).** Distinction 3,106; Pass 2,171; Fail 840; Withdrawn 888.  
**Engagement–outcome correlations.** Days Active vs Result Score r = 0.55; Total Clicks vs Result Score r = 0.35.  
**Risk model performance.** ~74% accuracy; ~77% recall for at-risk students.  
**Tipping point.** ~32.5 Days Active (use ~33 operationally).  
**IMD effort gap.** 2,465 vs 2,192 clicks (12.5% lower in most deprived band).

---

## Recommended institutional actions
**1) Implement a Days Active dashboard with a mid-module checkpoint.**  
Track Days Active per student per module. Automatically flag students below ~33 Days Active at the midpoint. Route flags to advisors and course teams.

**2) Build interventions that increase “days present,” not clicks.**  
Design nudges that push frequent, lightweight engagement. Examples include weekly study-plan prompts, “missed week” alerts, and instructor announcements that create predictable touchpoints.

**3) Treat IMD engagement gaps as a leading indicator.**  
Monitor Days Active and clicks by IMD band. If gaps widen, deploy targeted supports like device/connectivity assistance, digital-skills micro-support, and proactive advising for affected cohorts.

---

## What success looks like after deployment
Risk moves from end-of-term discovery to mid-module prevention. Advisors get a concrete trigger to triage outreach. Leadership gets an engagement-based leading indicator that can be tracked over time and disaggregated by socioeconomic context.

---

## Figures used in the report
- VLE Engagement vs Final Result (boxplot)  
- Correlation matrix (engagement vs outcome)  
- Standardized coefficients (Days Active vs Total Clicks)  
- Probability of success vs Days Active  
- Digital effort gap by IMD band
