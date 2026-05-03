# Root Cause Analysis - NP-INC-2026-001

**Incident:** Credit Scoring Engine Postcode Bias
**RCA Status:** Final
**Prepared by:** AI Governance Programme Office and ML Engineering
**Review Date:** 15 May 2026
**Approved by:** AI Governance Committee

---

## 1. Incident Summary

The NP-001 Credit Scoring Engine assigned systematically lower credit scores to applicants from 12 London postcode districts correlating with ethnic minority communities, constituting indirect discrimination under the UK Equality Act 2010. The bias was present from model go-live (March 2022) and remained active for approximately four years before being detected through a bias audit conducted under the new AI Governance Programme.

---

## 2. Root Cause Analysis Method

This RCA uses the **5 Whys** method to trace the incident to its root causes, followed by a contributing factors analysis to capture systemic issues. The goal is not to assign individual blame but to identify the conditions that allowed the failure to occur and persist undetected for four years.

---

## 3. Five Whys Analysis

**Problem statement:** The NP-001 Credit Scoring Engine produced discriminatory credit scores for applicants from specific London postcodes, resulting in higher rejection rates and inflated interest rates for applicants from protected groups under the UK Equality Act 2010.

---

**Why 1: Why did the model produce discriminatory scores?**

Because postcode was included as a model feature and acted as a statistically significant proxy for race and ethnicity, depressing scores for applicants in historically ethnic-minority-concentrated postcode districts.

---

**Why 2: Why was postcode included as a feature without recognising its discriminatory potential?**

Because the model development team conducted no formal proxy analysis of the features used. Postcode was treated as a legitimate geographic risk variable reflecting local economic conditions, without any analysis of whether it also encoded protected characteristics.

---

**Why 3: Why was no proxy analysis conducted?**

Because there was no requirement to do so. At the time of model development (2021-2022), NorthPoint had no formal AI governance process, no fairness evaluation standard and no pre-deployment bias assessment requirement. The data science team followed standard credit risk modelling practice, which at that time did not include systematic fairness auditing.

---

**Why 4: Why was there no fairness evaluation requirement?**

Because NorthPoint had no Responsible AI Policy or AI governance programme. The model was developed and deployed in the absence of any structured governance framework. There was no mechanism for identifying the need for a fairness assessment, requiring it as part of the model development lifecycle, or holding anyone accountable for it.

---

**Why 5: Why did the absence of a governance framework go unaddressed for four years?**

Because AI governance was not treated as a priority until regulatory pressure - specifically the EU AI Act entering application for high-risk systems in 2025 - created urgency. Before 2026, AI risk was managed informally within individual teams without cross-functional oversight, executive accountability or a central monitoring function. There was no inventory, no structured review process and no capability that would have detected ongoing bias.

**Root cause:** Absence of an enterprise AI governance programme. The discriminatory model feature was a symptom; the root cause was the absence of the structures, processes and accountability that would have prevented its inclusion, required its testing and detected its effects.

---

## 4. Contributing Factors

### CF-1: Training Data Encoding Historical Discrimination

The model was trained on NorthPoint's historical lending data (2015-2021). That data reflected lending decisions made before the use of AI - and those decisions may themselves have been influenced by geographic biases present in traditional credit assessment. Training on historically discriminatory outcomes can embed that discrimination into a model even without explicit intent.

**Implication:** Retrospective datasets are not neutral. Governance frameworks must require assessment of whether training data encodes historical patterns that would be unacceptable if explicitly designed into the model.

---

### CF-2: Postcode as a Proxy - A Known Risk Not Applied

The risk of using geographic variables as ethnicity proxies in credit models is well-documented in academic literature, FCA supervisory publications and NGO reporting. FCA supervisory work on algorithmic bias in consumer credit, published in 2022, explicitly flagged postcode-ethnicity correlation as a known proxy risk. The data science team building the Credit Scoring Engine was not aware of this guidance and had not been trained to identify proxy discrimination risks in feature selection.

**Implication:** ML practitioners need AI governance training that covers fairness concepts alongside technical skills. Awareness of proxy discrimination risks cannot be assumed - it requires deliberate education and structured checkpoints in the model development process.

---

### CF-3: No Post-Deployment Monitoring for Fairness

Once deployed, the Credit Scoring Engine was monitored for accuracy metrics (default prediction accuracy, AUC) but not for fairness metrics. Demographic parity, equalised odds and disparate impact measures were not tracked. The bias was therefore invisible to the operational monitoring regime for four years, despite active model governance of other dimensions.

**Implication:** Monitoring frameworks for AI systems must include fairness metrics alongside accuracy metrics from the first day of production deployment. A model that is accurate on average can still be discriminatory in specific segments.

---

### CF-4: No Mechanism for Affected Individuals to Surface Issues

Between 2022 and 2026, some rejected applicants may have suspected unfairness. However, there was no accessible mechanism for affected individuals to raise concerns specifically about AI-driven credit decisions, and no requirement to inform applicants that an AI system was involved in their assessment. Any concerns that entered the general complaints process were not identified as potential AI fairness issues and were not routed to people with the capability to assess them.

**Implication:** Customer-facing AI systems need accessible mechanisms for individuals to challenge AI-assisted decisions, alongside a defined process for routing those challenges to people who can assess them in a governance context. Article 22 UK GDPR provides a right to human review of automated decisions - NorthPoint's customer-facing processes did not make this right visible or accessible.

---

### CF-5: Governance Programme Established in Response to Regulation, Not Risk

NorthPoint's AI governance programme was established in January 2026, triggered by the EU AI Act entering application for high-risk systems. Had the programme been established earlier - even in 2023, following FCA supervisory publications on algorithmic bias and industry-wide signals about AI governance expectations - the bias audit that detected this incident would have occurred two to three years sooner. Approximately 2,500 fewer applications would have been affected.

**Implication:** Proactive, risk-driven governance produces materially better outcomes than compliance-driven governance. Waiting for regulation to require governance is not the same as managing risk. The corrective action plan should build ongoing detection capability, not just respond to this specific incident.

---

## 5. Corrective Action Plan

| Action | Factor Addressed | Owner | Due Date | Status |
|---|---|---|---|---|
| Remove postcode feature and retrain Credit Scoring Engine | Direct remediation | ML Engineering | 30 April 2026 | Complete |
| Mandate pre-deployment proxy analysis for all geographic and demographic features in new and updated models | CF-1, CF-2 | ML Engineering and AGPO | 30 June 2026 | In progress |
| Implement fairness metrics (demographic parity, disparate impact) in all credit model monitoring dashboards | CF-3 | ML Engineering | 30 June 2026 | In progress |
| Develop and deliver AI fairness training for all ML Engineering and data science staff | CF-2 | AGPO and HR | 31 July 2026 | Not started |
| Implement customer-facing AI disclosure and challenge mechanism for all credit decisions | CF-4 | Legal, Product and Customer Experience | 31 August 2026 | Not started |
| Update model development standards to mandate proxy analysis for any feature capable of encoding protected characteristics | Root cause | AGPO | 30 June 2026 | In progress |
| Conduct retrospective proxy analysis on NP-002 Fraud Detection System and all other production models using geographic features | CF-1, CF-3 | ML Engineering | 31 August 2026 | In progress |
| Include fairness monitoring requirements in standard AI vendor contract terms | CF-3 | Legal and Procurement | 31 July 2026 | Not started |

---

## 6. Lessons Learned

**For the AI governance programme:**

**1. Governance programmes must cover existing systems, not just new deployments.**
The AI governance programme was established in January 2026 but initially focused on new use cases going forward. This incident shows that the most significant governance gaps may be in systems already in production. A retrospective audit programme for models in active deployment should be a standing element of the governance programme, not a one-off exercise triggered by incidents.

**2. Monitoring frameworks must include fairness metrics from day one of production deployment.**
Accuracy alone is insufficient. Every AI system that affects individuals should have defined fairness metrics tracked alongside performance metrics. The absence of fairness monitoring meant four years of discrimination went undetected despite routine model governance activity. What is not measured cannot be managed.

**3. Proxy discrimination is not obvious - it requires deliberate testing.**
Postcode appears to be a legitimate geographic variable. Its discriminatory effect was not visible to the team that built the model and would not have been visible to a standard model review. Governance frameworks must include explicit checkpoints for proxy analysis as part of feature selection and pre-deployment review. It is not enough to prohibit intentional discrimination. Indirect effects require deliberate, structured testing.

**4. Speed of detection determines scale of harm.**
This bias was active for four years. An earlier governance programme - or periodic fairness monitoring - would have detected it sooner. The corrective action plan should prioritise building ongoing detection capability as a permanent operational function, not treat it as remediation that is complete when this incident closes.

**5. Regulatory compliance and proactive governance are not the same thing.**
The EU AI Act did not require a fairness audit of the Credit Scoring Engine in 2022. A risk-driven governance approach would have. Governance programmes should aspire to better-than-minimum standards - because the gap between minimum compliance and good practice is where most AI harm occurs, and where most regulatory exposure accumulates.

---

*RCA approved by AI Governance Committee - 15 May 2026*
*Distribution: AI Governance Committee · Board Risk and Audit Committee · FCA (summary version) · Internal Audit*
