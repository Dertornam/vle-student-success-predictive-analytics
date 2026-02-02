---
title: Statistical Tables — Predictive Analytics for Student Success
layout: default
---

# Statistical Tables — Predictive Analytics for Student Success  
Using Virtual Learning Environment (VLE) Data

This page collects the core tables referenced in the main report.  
All values come from the 32,044 student–module records.

---

## Table 1. Mean engagement by final result

| Final Result | Mean Clicks | Median Clicks | Std. Deviation |
|--------------|------------:|--------------:|----------------:|
| Distinction  | 3,106.43    | 2,218.0       | 2,978.98        |
| Pass         | 2,171.11    | 1,503.0       | 2,137.91        |
| Fail         |   840.17    |   418.5       | 1,260.85        |
| Withdrawn    |   888.38    |   364.0       | 1,468.34        |

Interpretation note.  
The medians are far below the means, showing a heavy right tail where a smaller group clicks a lot.

---

## Table 2. Key correlations (engagement vs outcome)

| Measure Pair | Correlation (r) |
|-------------|-----------------:|
| Days Active vs Result Score | 0.55 |
| Total Clicks vs Result Score | 0.35 |

Interpretation note.  
Consistency has a stronger relationship with performance than raw click volume.

---

## Table 3. Classification performance (Success vs At-Risk)

| Metric | Value |
|--------|------:|
| Accuracy | 0.74 |
| Recall (At-Risk) | 0.77 |

Interpretation note.  
Recall is emphasized because the institutional cost of missing an at-risk student is high.

---

## Table 4. IMD digital effort gap (clicks)

| IMD Band | Mean Clicks |
|----------|------------:|
| Least deprived | 2,465 |
| Most deprived  | 2,192 |

Gap summary.  
Most deprived students show ~12.5% lower click volume than least deprived students.

---

## Table 5. Operational threshold (Days Active)

| Decision Rule | Threshold |
|--------------|----------:|
| High-risk zone by mid-module | ~33 active days |

Interpretation note.  
This is designed to be usable in advising workflows, not just statistically optimal.
