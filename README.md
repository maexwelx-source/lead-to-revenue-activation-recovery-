# Lead-to-Revenue Activation Recovery System

End-to-end RevOps system combining data analysis, BI, and automation to recover lost revenue from delayed user activation.

---

## Business Problem

A significant share of new sign-ups fail to activate within the first 48 hours.

This leads to:

* Delayed monetization
* Increased CAC payback period
* Lost revenue opportunities due to drop-offs during onboarding

---

## Objective

* Detect at-risk users early in the onboarding funnel
* Quantify **Potential Revenue Exposure (MRR/ARR)** and **CAC at Risk**
* Build an **operational intervention layer** to recover users and reduce losses

---

## System Architecture

```
Data (CSV / CRM simulation)
→ SQL (activation delay, CAC exposure, segmentation)
→ Power BI (monitoring & decision layer)
→ Automation (Make):
    - detect risk users
    - route by priority
    - trigger actions (alerts / outreach)
    - update processing state
```

---

## Decision Logic

Users are segmented based on business impact:

**High Priority**

* High CAC or high MRR potential
  → Immediate alert (Ops / Support team)

**Standard Risk**

* Activation delay > 24–48h
  → Automated outreach (email sequence)

All processed users are marked to avoid duplicate interventions.

---

## What I Built

* SQL logic to:

  * calculate activation delay (in hours)
  * classify users (activated vs not activated)
  * estimate revenue exposure

* Power BI dashboard:

  * activation funnel monitoring
  * CAC at risk visibility
  * delay distribution analysis
  * scenario-based recovery estimation

* Automation workflow (Make):

  * detects delayed users
  * prioritizes based on impact
  * routes into different intervention paths
  * tracks processing status

---

## Core Metrics

* Activation Rate (within 48h)
* Average Time to Activation (hours)
* % of Users Delayed >48h
* Potential MRR Exposure
* CAC at Risk
* Recovery Simulation:

  * Recovered MRR
  * CAC Saved
  * Remaining Exposure

---

## Methodology Note

Potential MRR Exposure is calculated as a proxy:

Average MRR of activated users (by segment/channel) × number of delayed users

This approach is used because:

* MRR at sign-up stage is often zero (trial / freemium)
* Real revenue potential becomes visible only after activation

---

## Automation Workflow

<img width="962" height="651" alt="image" src="https://github.com/user-attachments/assets/0edeca17-a593-403d-98a8-7f0c98d5aa2a" />


The automation layer simulates a real RevOps system:

* Continuous monitoring of onboarding performance
* Immediate reaction to high-risk users
* Scalable intervention logic
* Closed-loop tracking (detection → action → status update)

---

## Repository Structure

/automation        → Make scenario (workflow logic)
/data              → source datasets (CSV)
/docs              → business report (Power BI export)
/powerbi           → DAX measures & model logic
/sql               → data transformation & modeling
/notion            → documentation / presentation layer

---

## Business Impact

This system demonstrates how RevOps can:

* Reduce time-to-activation
* Prevent wasted CAC
* Replace manual monitoring with automated workflows
* Enable prioritized, data-driven interventions

---

## Use Case

Applicable for:

* SaaS companies with onboarding funnels
* Subscription-based products
* Growth / RevOps teams optimizing activation and retention

---

## Key Takeaway

Instead of just tracking metrics, this system creates a **decision + action loop**:

Detection → Prioritization → Intervention → Tracking

This is the core of scalable, data-driven operations.
