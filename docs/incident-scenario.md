# Incident Description - NP-INC-2026-001

**Incident ID:** NP-INC-2026-001
**System:** NP-001 · Credit Scoring Engine
**Incident Type:** AI Fairness / Discriminatory Output
**Severity:** 1 - Critical
**Status:** Under Investigation (as of Week 2)
**Incident Owner:** Head of Credit Risk
**Governance Lead:** AI Governance Programme Office

---

## Incident Summary

The NP-001 Credit Scoring Engine, NorthPoint's ML-based credit scoring model, has been found to systematically assign lower credit scores to loan applicants residing in London postcodes that correlate with high concentrations of ethnic minority residents. The effect is statistically significant and cannot be explained by differences in financial history or creditworthiness indicators alone.

The disparity results in affected applicants facing higher rejection rates, higher interest rates or lower loan limits than comparably creditworthy applicants from other postcodes. This constitutes potential indirect discrimination under the UK Equality Act 2010 (protected characteristic: race) and raises serious compliance obligations under the EU AI Act, UK GDPR and FCA Consumer Duty.

---

## How the Incident Was Detected

**Detection source:** Internal - NorthPoint data scientist (ML Engineering team)

**Detection narrative:**

On 10 March 2026, a data scientist in the ML Engineering team was conducting exploratory analysis on the Credit Scoring Engine as part of the new AI Governance Programme's bias audit initiative - one of the first structured activities under the Responsible AI Policy implemented in January 2026 (Phase 3 of the NorthPoint AI Governance Programme). She was examining feature importance and model outputs by geographic segment when she identified an anomaly: applicants from a cluster of East and South London postcodes were receiving scores 35-55 points lower on average than applicants with comparable financial profiles from other postcode districts.

She flagged the finding to her manager, who escalated to the Head of Credit Risk on 11 March 2026.

Initial internal analysis confirmed the finding. The affected postcode cluster corresponds closely with districts that, according to ONS (Office for National Statistics) Census 2021 data, have above-average concentrations of Black British, British Bangladeshi and British Pakistani residents. The affected postcodes include areas across Hackney, Newham, Tower Hamlets, Southwark and Lambeth.

A preliminary assessment indicates that postcode is a significant feature in the model - included in training data as a "geographic risk factor" - and is acting as a proxy for race and ethnicity, producing indirect discrimination.

---

## Scope and Impact Assessment

**Estimated affected population (preliminary):**
- Approximately 2,400 loan applications processed in the affected postcodes in the 12 months preceding discovery
- Of those, approximately 680 resulted in rejection decisions
- Approximately 1,100 resulted in approval at higher interest rates or lower loan limits than a postcode-agnostic model would have produced

**Financial impact to affected customers (preliminary estimate):**
- Excess interest paid due to higher risk pricing: to be quantified during investigation
- Credit access denied: 680 applications - a proportion of which would likely have been approved under a fair model

**Regulatory implications:**

| Regulator / Obligation | Trigger | Status |
|---|---|---|
| EU AI Act, Article 73 | Serious incident involving a deployed high-risk AI system (Annex III, credit scoring) | Under assessment |
| FCA Consumer Duty | Systematic failure to deliver good outcomes; discriminatory impact on customers with protected characteristics | Notification likely required |
| ICO (UK GDPR) | Automated decision-making obligations under Article 22 UK GDPR; applicants may not have been informed of AI involvement | Under assessment |
| UK Equality Act 2010 | Indirect discrimination on grounds of race in the provision of financial services | Legal review in progress |

**Reputational risk:** High. Algorithmic bias in financial services lending is subject to active FCA supervisory scrutiny and significant media attention. Proactive, transparent handling is essential to managing both regulatory and reputational exposure.

---

## Immediate Context

**Why was postcode included in the model?**

Postcode was included as a geographic risk variable on the assumption that it reflected local economic conditions - local unemployment rates, property values and area-level default history. This approach mirrors traditional credit risk modelling practice. However, in the UK context, certain London postcode districts also encode historical patterns of ethnic residential segregation, resulting in the feature functioning as a race proxy in practice.

**Was the risk known?**

The risk assessment conducted at model build time (2021-2022) did not include a formal proxy discrimination analysis of geographic features. The use of postcode was not challenged. The 2021 FCA Guidance on Fair Treatment of Vulnerable Customers, and broader FCA supervisory statements on algorithmic bias, were not applied to this model's feature selection process. This is a finding that the governance programme must address structurally.

**Is this ongoing?**

Yes. The Credit Scoring Engine is processing applications in real time. Every application submitted from the affected postcodes during the current period is potentially subject to the same bias. Immediate containment action is required.

---

## Incident Severity Classification

| Dimension | Assessment |
|---|---|
| Harm to individuals | High - potential financial harm and indirect discrimination against protected groups across multiple postcode districts |
| Regulatory exposure | Critical - multiple reporting obligations likely triggered across FCA, ICO and EU AI Act |
| Reputational risk | High |
| Operational impact | Medium - model suspension would require temporary routing to manual underwriting |
| Reversibility | Medium - past decisions can be reviewed and remediated; model can be retrained with postcode removed |

**Overall severity: 1 - Critical**

Severity 1 incidents under the NorthPoint AI Incident Response Framework require:
- Immediate notification to the AI Governance Programme Office (within 12 hours)
- CRO notification within 24 hours
- Board Risk and Audit Committee notification within 48 hours
- Immediate involvement of Legal and Compliance
- Assessment of regulatory disclosure obligations within 72 hours

---

*Prepared by the AI Governance Programme Office - 12 March 2026. This is a living document updated as the investigation progresses.*
