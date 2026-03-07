
# Lead-to-Revenue Activation Recovery System

Практическая RevOps-система для выявления delayed activations, оценки revenue/CAC exposure и запуска interventions.

## Проблема бизнеса
Часть новых sign-up не активируется в первые 48 часов → отложенная монетизация + растянутый payback CAC.

## Цель
- Раннее выявление рискованных пользователей
- Квантификация Potential MRR/ARR Exposure и CAC at Risk
- Операционная очередь interventions + measurable recovery impact

## Что внутри репо (на данный момент)
- `/docs/Executive_RevOps_Activation_Recovery_Report.pdf` — полный экспорт Power BI отчёта 
- `/powerbi/powerbi_measures_dax.md` — ключевые DAX-меры.

## Core Metrics
- Activation Rate (% в первые 48h)
- Avg Delay to Activation (hours)
- % Delayed >48h
- Potential MRR Exposure (>48h, proxy на основе avg paid MRR activated users)
- What-If Recovery: Recovered MRR, CAC Saved, Remaining Exposure

**Методическая заметка**  
Potential MRR Exposure считается как proxy (avg MRR activated users по сегменту/каналу × delayed users), т.к. на момент sign-up MRR часто = 0 (trial/free).


