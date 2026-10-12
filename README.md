# eICU Hopital Mortality Data Analysis

## Overview

This is a beginner analytics project, primarily done to explore and practise analytics workflow -- data exploration, data quality checks, cohort definition, risk adjustment -- on real healthcare data. 

### Dataset 
This project uses the [eICU Collaborative Research Database](https://physionet.org/content/eicu-crd/2.0/), which covers over 200,000 ICU stays across 208 US hospitals (2014–2015).

Data access requires credentialed access from PhysioNet, so no data is included in this repository, and notebook outputs containing note text have been removed. Only aggregates are included in the notebook.

**Analytics question:** After adjusting for patient severity, do hospitals differ meaningfully in ICU patient mortality?

Note: 
- The results are reported for in-hospital mortality for each patient's first ICU stay in a hospitalisation. Patient severity is adjusted using APACHE IVa. 

## Findings

**1. APACHE IVa over-predicts mortality in this cohort.**
Across all risk groups, fewer patients died than the model predicted (overall observed/expected ratio = 0.76). The model still ranks patients correctly by risk, so hospitals were compared against the cohort average (O/E = 0.76) rather than against 1.

**2. Cohort definition.**
- 18 of 208 hospitals had no APACHE data.
- Hospitals where fewer than 40% of first ICU visits had an APACHE prediction were excluded, since their O/E would describe only a small subset of patients. This threshold was chosen as it sits at a natural break in the coverage distribution plot. 184 hospitals remained, covering 95.8% of first ICU visits.
- Hospitals with fewer than 5 expected deaths were excluded, because their O/E would be unreliable due to a small denominator. 
- 168 remaining hospitals were benchmarked.

**3. Most hospitals perform as expected.**
Using a funnel plot, 14 hospitals fell outside the 99.8% Poisson control limits, far more than chance would predict, which suggested overdispersion. An overdispersion φ = 2.19 was then found. After widening the limits to account for this, **164 of 168 hospitals were within the expected range**.

**4. Four outlier hospitals.**
Two hospitals had higher mortality and two had lower mortality than the others. No significant difference in APACHE coverage, severity of illness or the share of patients transferred from other hospitals was found, so these factors do not explain their results. No significant findings can be concluded. 

**Limitations:** eICU hospitals are not a random sample of US hospitals; discharge destinations were not examined, so some deaths after transfer out of hospital may be missed; and with only four outliers, the profiling is only descriptive.



## References 
1. https://eicu.mit.edu/gettingstarted/overview/ (Overview | eICU Collaborative Research Database)
2. https://pmc.ncbi.nlm.nih.gov/articles/PMC6132188/ (The eICU Collaborative Research Database, a freely available multi-center database for critical care research - PMC)
3. https://casrai.org/guides/observed-to-expected-ratio-risk-adjustment (O/E Ratio & Risk Adjustment, Explained — CASRAI)
4. https://pubmed.ncbi.nlm.nih.gov/16540951/ (Acute Physiology and Chronic Health Evaluation (APACHE) IV: hospital mortality assessment for today's critically ill patients - PubMed)


 
