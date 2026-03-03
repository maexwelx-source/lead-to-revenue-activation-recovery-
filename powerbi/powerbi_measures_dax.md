# Ключевые DAX-меры — RevOps Activation & Recovery

## 1. Activation Rate
```dax
Activation Rate = 
VAR total = COUNTROWS(onboarding_user_view)
VAR activated = 
    CALCULATE(
        COUNTROWS(onboarding_user_view),
        onboarding_user_view[activated] = "Yes"
    )
RETURN
    COALESCE(DIVIDE(activated, total), 0)


Avg Delay (hrs) = 
AVERAGE(onboarding_user_view[delay_hours])

Avg Delay (hrs, Per User) = 
DIVIDE(
    SUM(onboarding_user_view[delay_hours]),
    DISTINCTCOUNT(onboarding_user_view[user_id])
)

Potential MRR Exposure (>48h) = 
[Avg Paid MRR (Activated)] * [Delayed Users >48h (Not Activated)]

Recovery Rate (What-If) = 
VAR X = SELECTEDVALUE('Reduce onboarding delay by X hours'[Reduce onboarding delay by X hours], 0)
RETURN
    SWITCH(TRUE(),
        X < 12, 0.05,
        X < 24, 0.10,
        X < 48, 0.18,
        0.25
    )

Recovered MRR (What-If) = 
[MRR at Risk (Proxy)] * [Recovery Rate (What-If)]

CAC Saved (What-If) = 
VAR rr = [Recovery Rate (What-If)]
VAR cac_base = [CAC at Risk(Baseline)]
RETURN
    cac_base * rr