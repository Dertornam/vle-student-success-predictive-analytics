# Executive Summary: Predictive Analytics for Student Success  
Leveraging Digital Behavioral Markers to Mitigate Academic Risk

## I. The strategic problem

Student retention is a primary challenge in higher education, with this dataset reflecting a withdrawal rate of 30.1%. Traditional methods for identifying struggling students often rely on summative assessments that occur too late in the academic cycle to allow for meaningful intervention. This analysis demonstrates how Virtual Learning Environment (VLE) interaction data can be utilized to build a proactive early-warning system that identifies at-risk students before academic failure occurs.

## II. Descriptive insights and the engagement–grade link

An initial analysis of 32,044 student records revealed a definitive correlation between digital engagement levels and final academic results.

**Table 1. Engagement metrics by final result**

| Final Result | Mean Clicks | Median Clicks | Std. Deviation |
|--------------|------------:|--------------:|----------------:|
| Distinction  | 3,106.43    | 2,218.0       | 2,978.98        |
| Pass         | 2,171.11    | 1,503.0       | 2,137.91        |
| Fail         |   840.17    |   418.5       | 1,260.85        |
| Withdrawn    |   888.38    |   364.0       | 1,468.34        |

The data confirms a “ladder of success.” Students achieving a Distinction interacted with the VLE at a rate nearly four times higher than those who failed. The high standard deviation of engagement (about 2,090.13) indicates significant variance in behavior, suggesting that while high engagement correlates with success, it is not a uniform guarantee.

The figure `reports/figures/vle_engagement_vs_final_result_boxplot.png` (“VLE Engagement vs. Final Academic Result”) illustrates this ladder on a log scale, with median engagement rising sharply across Withdrawn, Fail, Pass, and Distinction.

## III. Correlation analysis: consistency vs intensity

A critical finding of this study is the distinction between the volume of activity and the regularity of that activity.

**Table 2. Feature correlation matrix**

| Variable     | Total Clicks | Days Active | Result Score |
|-------------|-------------:|-----------:|------------:|
| Total Clicks| 1.00         | 0.82       | 0.35        |
| Days Active | 0.82         | 1.00       | 0.55        |
| Result Score| 0.35         | 0.55       | 1.00        |

The correlation between Days Active and the Result Score (r = 0.55) is substantially stronger than the correlation for Total Click volume (r = 0.35). This means consistency is about 57% more predictive of success than intensity. While clicks and days are highly related (r = 0.82), showing up regularly is the more reliable signal for student success.

The figure `reports/figures/correlation_heatmap_engagement_vs_outcome.png` visualizes this matrix. The figure `reports/figures/predictive_power_consistency_vs_volume.png` shows standardized coefficients from a model in which Days Active has a strong positive importance (1.91) while Total Clicks has a negative coefficient (−0.51) once consistency is controlled.

This pattern reflects a “cramming penalty.” High-intensity, low-frequency engagement is not an effective strategy for long-term academic success.

## IV. Predictive modeling and the survival threshold

To turn these insights into actionable policy, a logistic regression model was developed to classify students into “Success” or “At-Risk” categories.

**Table 3. Logistic regression feature importance (standardized)**

| Feature      | Coefficient | Odds Ratio | Interpretation |
|-------------|------------:|----------:|----------------|
| Days Active |  1.9147     | 1.0336    | Every extra active day increases odds of success by about 3.36%. |
| Total Clicks| -0.5183     | 0.9997    | High click volume without consistency has a negligible or slightly negative impact. |
| Intercept   | -1.6143     |    N/A    | Baseline log-odds for inactive students. |

**Table 4. Model classification report**

| Metric    | Class 0 (At-Risk) | Class 1 (Success) | Weighted Avg |
|----------|-------------------:|------------------:|-------------:|
| Precision| 0.71               | 0.78              | 0.74         |
| Recall   | 0.77               | 0.71              | 0.74         |
| F1-score | 0.74               | 0.74              | 0.74         |

The model achieves an overall accuracy of 74% and a recall of 77% for the at-risk group. This means the system successfully identifies nearly four out of five students who require intervention.

Using decision tree logic, the analysis identified a specific tipping point of 32.50 active days. Students who log in fewer than 33 days by the mid-semester point have roughly a 70% probability of failing or withdrawing.

The figure `reports/figures/probability_of_success_vs_days_active.png` (“Probability of Success vs. Days Active”) shows the rapid climb in success probability as a student approaches and crosses this 33-day threshold.

## V. Socioeconomic equity audit

The final phase of the analysis examined student performance through the lens of the Index of Multiple Deprivation (IMD).

**Table 5. Engagement by socioeconomic band (IMD)**

| IMD Band                 | Average Total Clicks |
|--------------------------|---------------------:|
| 0–10% (Most Deprived)    | 2,192.15             |
| 40–50%                   | 2,175.68             |
| 90–100% (Least Deprived) | 2,465.24             |

There is a 12.5% engagement gap between the most and least deprived students. This suggests that students from lower socioeconomic backgrounds may face “digital friction,” such as limited hardware access or less reliable connectivity.

The bar chart `reports/figures/digital_effort_gap_by_imd.png` (“The Digital Effort Gap”) visualizes this gradient across IMD bands.

## VI. Final strategic recommendations

Behavioural redesign. Update institutional “nudge” communications to reward daily login streaks and consistent presence rather than single bursts of activity.

Hard-metric alerts. Establish an automated trigger for academic advisors to reach out to any student who has not reached the 33-day activity threshold by the designated mid-point of a module.

Targeted digital support. Allocate resources such as digital equity grants or offline-accessible learning modules for students in the lowest IMD bands, with the goal of closing the 12.5% engagement gap.
