# Incident Response Timeline - NP-INC-2026-001

**Incident:** Credit Scoring Engine Postcode Bias
**Timeline Period:** March 2026 - June 2026

---

## Week 1 (10-14 March 2026): Detection and Immediate Response

### Day 1 - Tuesday 10 March
**Event:** Detection

- Data scientist identifies anomalous postcode-correlated score disparity during routine bias audit
- Initial finding documented and shared with ML Engineering manager
- Informal escalation to Head of Credit Risk begins

**Status:** Detection phase

---

### Day 2 - Wednesday 11 March
**Event:** Escalation and Initial Triage

- Head of Credit Risk convenes emergency call with ML Engineering lead and the data scientist
- Preliminary analysis confirms the finding: the disparity is statistically significant and consistent across 12 postcode districts
- Head of Credit Risk notifies AI Governance Programme Office
- AGPO classifies as Severity 1 incident (NP-INC-2026-001) and initiates formal incident response

**Notifications issued:**
- CRO notified (Day 2, within 24-hour requirement) ✓
- Legal and Compliance notified ✓
- Data Protection Officer notified ✓

**Immediate containment decision:**
AGPO and Head of Credit Risk recommend immediate suspension of automated credit scoring for applications from affected postcodes, pending further investigation. Applications from affected postcodes will be routed to manual underwriting review.

CRO approves containment measure.

---

### Day 3 - Thursday 12 March
**Event:** Containment Implemented; Board Notification

- Credit Scoring Engine output for applications from affected postcode districts suspended as the sole decisioning input
- Applications from affected postcodes (approximately 15-20 per day) routed to manual underwriting queue
- Manual underwriting capacity confirmed adequate for interim volume
- Board Risk and Audit Committee Chair notified by CRO (within 48-hour requirement) ✓
- Extraordinary AI Governance Committee session scheduled for 14 March

**Legal and Compliance begin regulatory disclosure assessment:**
- EU AI Act Article 73 - does this constitute a "serious incident" for a high-risk AI system under Annex III?
- FCA - Consumer Duty notification obligations; supervisory reporting under Principle 11
- ICO - automated decision-making obligations under UK GDPR Article 22; whether affected applicants were informed of AI involvement
- UK Equality Act 2010 - indirect discrimination in provision of financial services

---

### Day 4-5 - Friday-Saturday 13-14 March
**Event:** AI Governance Committee Extraordinary Session

**Agenda:**
1. Incident briefing and confirmed scope
2. Containment status review
3. Regulatory disclosure recommendation
4. Investigation plan approval
5. Customer communication approach

**Decisions made:**
1. Containment measure approved as ongoing, pending model investigation
2. Legal and Compliance to prepare regulatory disclosure recommendation for CRO approval by 21 March
3. Independent external forensic analysis of model commissioned (specialist AI bias consultancy engaged by Monday 16 March)
4. Retrospective review programme initiated: all applications from affected postcodes in the past 48 months to be reviewed
5. Customer communication: no proactive outreach to affected applicants until scope of harm is quantified (target: 28 March for outreach plan)
6. Internal communications: staff in Credit Risk, Customer Experience and Compliance to receive briefing by 18 March

---

## Week 2 (16-20 March 2026): Investigation

### Actions

- External forensic analysis of the Credit Scoring Engine model begins
- Internal data pull: all applications from affected postcodes since model go-live (March 2022 - March 2026)
- Full feature importance analysis commissioned to identify all features contributing to the disparity
- DPO reviews whether UK GDPR Article 22 disclosures were made correctly for past automated credit decisions
- Legal begins drafting regulatory notification letters for FCA and ICO
- Risk team contacted: NP-002 Fraud Detection System also uses postcode as a geographic feature - separate bias review initiated in parallel

**Emerging findings (preliminary):**
- Postcode feature contributes approximately 8% to overall model score in the affected clusters
- The disparity has been present since model go-live; it was not introduced by a recent update or retraining
- Approximately 4 years of applications are in scope for retrospective review
- NP-002 Fraud Detection: Risk Director confirms postcode is used as a geographic risk variable; separate fairness review initiated

---

## Week 3 (23-27 March 2026): Scope Confirmation and Regulatory Engagement

### External Forensic Analysis - Preliminary Findings (24 March)

**Key findings:**
1. Postcode acts as a statistically significant proxy for race and ethnicity in 12 London postcode districts across Hackney, Newham, Tower Hamlets, Southwark and Lambeth
2. The average score depression for affected applicants is 43 points (range: 31-67 points across districts)
3. At NorthPoint's credit policy thresholds, a 43-point depression translates to an increased rejection rate of approximately 12 percentage points for borderline applicants
4. The disparity cannot be explained by underlying creditworthiness differences - the model is introducing a bias, not measuring a real risk differential
5. Root cause (preliminary): postcode was included as a geographic feature without proxy analysis; the training data reflected historical lending patterns in those areas, which themselves reflected past discriminatory lending practices

**Scope confirmed:**
- 4,127 applications from affected postcodes reviewed since March 2022
- 847 rejections that may have been influenced by the bias
- 1,892 approvals at potentially inflated interest rates

**Regulatory disclosure decision (27 March):**
CRO approves regulatory notifications:
- FCA formal notification submitted: 27 March 2026 (under Consumer Duty and Principle 11)
- UK AI Authority notified: 27 March 2026 (serious incident notification under UK AI governance framework)
- ICO notified: 27 March 2026 (UK GDPR Article 22 potential breach)

---

## Week 4 (30 March - 3 April 2026): Customer Impact Assessment and Communication Plan

### Customer Impact Quantification

Finance and Credit Risk teams complete financial impact modelling:
- Total estimated excess interest charged to affected approved applicants: £2.1 million
- Estimated customers who were rejected but would have been approved under a fair model: 234 (based on re-scoring without postcode feature)

### Customer Communication Plan Approved (2 April)

**Decision:** Proactive outreach to all affected customers

Communication approach:
1. **Affected applicants who were rejected** - personal letter acknowledging that their application may have been unfairly assessed, offering a fresh review at no cost with a human underwriter making the final decision
2. **Affected applicants who were approved at higher rates** - personal letter acknowledging potential overcharging, confirming they will receive a calculation of excess interest paid and a refund
3. **General customer notice** - published on NorthPoint website confirming that a bias issue was identified and is being remediated

Legal approves communications. DPO confirms UK GDPR compliance.

**Customer outreach begins: 7 April 2026**

---

## Week 5-6 (6-17 April 2026): Remediation

### Model Remediation Plan (approved 6 April)

**Short-term (immediate):**
- Remove postcode as a feature from the Credit Scoring Engine
- Retrain model on adjusted dataset with postcode excluded
- Validate retrained model against fairness criteria before redeployment

**Medium-term (60 days):**
- Commission full fairness audit of retrained model by independent external evaluator
- Implement ongoing demographic parity monitoring in production
- Establish automated alerts for emerging score disparities correlated with protected characteristic proxy variables

**Model retraining timeline:**
- Postcode removal and retraining: 6 April - 30 April
- Internal validation: 1-14 May
- External fairness audit: 15-31 May
- Redeployment with enhanced monitoring: 1 June 2026

**During remediation period:** All credit decisions processed through manual underwriting

### Retrospective Review Programme

- 847 rejected applications under review by an external underwriting panel (NorthPoint staff with conflict-of-interest recusal applied)
- Target completion: 30 April 2026
- Applicants whose rejections are reversed to be contacted with a new lending offer

---

## Week 8-10 (May 2026): Root Cause Analysis and Lessons Learned

- Formal root cause analysis document completed (see [`root-cause-analysis.md`](root-cause-analysis.md))
- AI Governance Committee reviews RCA and approves corrective action plan: 15 May
- Model retrained and independently validated
- External fairness audit completed

**Model redeployment approved: 2 June 2026** (conditional on enhanced monitoring controls being live at go-live)

---

## Week 12 (9-13 June 2026): Incident Closure

**Closure conditions:**
- [x] All affected customers contacted
- [x] Retrospective review of rejected applications complete
- [x] Refunds calculated and issued
- [x] Retrained model independently validated
- [x] External fairness audit completed
- [x] Regulators updated with closure report
- [x] Root cause analysis and corrective actions documented and approved by AI Governance Committee
- [x] Lessons learned shared with AI governance programme
- [x] Board notified of closure

**Incident closed: 12 June 2026**

---

## Incident Summary - Key Metrics

| Metric | Value |
|---|---|
| Detection to containment | 2 days |
| Detection to regulatory notification | 16 days |
| Affected applications reviewed | 4,127 |
| Rejections under retrospective review | 847 |
| New lending offers issued to previously rejected applicants | 234 |
| Excess interest refunded | £2.1 million |
| Days to model redeployment | 84 |
| Total incident duration | 95 days |

---

*This timeline is a simulation of a well-managed AI incident response. In practice, timelines vary significantly based on investigation complexity, regulatory requirements and organisational capacity.*
