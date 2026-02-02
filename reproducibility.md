---
title: Reproducibility
layout: default
permalink: /reproducibility/
---

# Reproducibility — Predictive Analytics for Student Success  
Using Virtual Learning Environment (VLE) Data

This page explains how someone can reproduce the analysis and outputs.  
The focus is clarity and auditability.

---

## Reproducible workflow
Step 1. Start from raw Open University VLE tables in `data/raw/`.  
Step 2. Build the student–module analytic file in `data/processed/`.  
Step 3. Recreate figures and tables into `reports/figures/`.  
Step 4. Render the main report page and executive summary pages.

---

## Core transformations
I aggregate clickstream logs to student–module totals.  
I calculate Days Active as distinct activity dates per student per module.

I then join outcomes and context fields (including IMD).  
I validate that each row represents one student–module.

---

## Modeling steps
I define the outcome as “Success vs At-Risk.”  
I fit a logistic regression model using engagement features.

I then fit a simple decision-tree split to surface a human-usable tipping point.  
That threshold lands near ~32.5 Days Active, used as ~33 operationally.

---

## Outputs generated
Figures are saved into `reports/figures/`.  
Tables are copied into the Statistical Tables page for quick executive review.

The executive summary is written to be slide-ready.  
It contains the metrics and thresholds leadership needs.

---

## What makes this reproducible
Everything is deterministic once the data is fixed.  
Feature definitions are stable.

The outputs are file-based.  
That supports version control and review.

If you rerun the pipeline, you should recreate the same figures and tables.  
That is the standard for institutional analytics trust.
