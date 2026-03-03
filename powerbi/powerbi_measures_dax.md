GitHub не поддерживает подсветку синтаксиса для DAX (язык Power BI).  
Код показан как есть — он полностью рабочий и читаемый.  
Для цветной подсветки открывайте в Power BI Desktop или VS Code с расширением DAX.

GitHub does not support syntax highlighting for DAX (Power BI language).  
The code is shown as is — it is fully functional and readable.  
For color highlighting, open it in Power BI Desktop or VS Code with the DAX extension.

# Ключевые / Key DAX-меры — RevOps Activation & Recovery

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

## 2. Avg Delay (hrs)

Avg Delay (hrs) = 
AVERAGE(onboarding_user_view[delay_hours])

## 3. Avg Delay (hrs, Per User)
Avg Delay (hrs, Per User) = 
DIVIDE(
    SUM(onboarding_user_view[delay_hours]),
    DISTINCTCOUNT(onboarding_user_view[user_id])
)

## 4. Potential MRR Exposure (>48h) 
Potential MRR Exposure (>48h) = 
[Avg Paid MRR (Activated)] * [Delayed Users >48h (Not Activated)]

## 5. Recovery Rate (What-If) 
Recovery Rate (What-If) = 
VAR X = SELECTEDVALUE('Reduce onboarding delay by X hours'[Reduce onboarding delay by X hours], 0)
RETURN
    SWITCH(TRUE(),
        X < 12, 0.05,
        X < 24, 0.10,
        X < 48, 0.18,
        0.25
    )

## 6. Recovered MRR (What-If)
Recovered MRR (What-If) = 
[MRR at Risk (Proxy)] * [Recovery Rate (What-If)]

## 7. CAC Saved (What-If) 
CAC Saved (What-If) = 
VAR rr = [Recovery Rate (What-If)]
VAR cac_base = [CAC at Risk(Baseline)]
RETURN

    cac_base * rr

