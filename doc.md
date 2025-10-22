# Program Analytics API
Beautiful, Organized Markdown Reference

Last updated: 2025-10-22

- Base path: /analytics/program
- Date format: ISO-8601 (YYYY-MM-DD)
- Lists: CSV or repeated params (?programIds=10&programIds=20)

Table of Contents
- [Overview](#overview)
- [Endpoints](#endpoints)
  - [GET /list](#get-list)
  - [GET /achievement-summary](#get-achievement-summary)
  - [GET /budget-consumption](#get-budget-consumption)
  - [GET /Initiative-summary](#get-initiative-summary)
  - [GET /at-risk](#get-at-risk)
  - [GET /performance-vs-target](#get-performance-vs-target)
  - [GET /budget-vs-progress](#get-budget-vs-progress)
  - [GET /progress-series](#get-progress-series)
- [Error Handling](#error-handling)
- [Change Log](#change-log)

## Overview
Eight analytics endpoints provide KPIs and chart series for Programs. All are GET and accept optional filters.

## Endpoints

### GET /list
Returns programs for filter dropdowns.

Parameters
- goalIds: List<Long> (optional)
- ids: List<Long> (optional)

Response (ProgramListFilterDto)
```json
{
  "data": [
    {
      "id": 37,
      "name": { "ar": "...", "en": "..." },
      "goalId": 12,
      "goalName": { "ar": "...", "en": "..." },
      "strategyId": 5,
      "strategyName": { "ar": "...", "en": "..." }
    }
  ],
  "totalCount": 1
}
```

Examples
- curl "{BASE}/analytics/program/list"
- curl "{BASE}/analytics/program/list?goalIds=12,15"
- curl "{BASE}/analytics/program/list?ids=37,40"

---

### GET /achievement-summary
Aggregated current achievement, target planned, variance, mini trend, and active programs count.

Parameters
- programIds: List<Long> (optional)

Response (ProgramAchievementSummaryDto)
```json
{
  "currentAchievement": 0.35,
  "targetPlanned": 0.40,
  "variance": -0.05,
  "miniTrend": [ { "date": "2025-06-01", "avgPercent": 0.31 } ],
  "activeGoalsCount": 12
}
```

Example
- curl "{BASE}/analytics/program/achievement-summary?programIds=10,20"

---

### GET /budget-consumption
Budget consumption card with per-program lines.

Parameters
- programIds: List<Long> (optional)

Response (ProgramBudgetConsumptionDto)
```json
{
  "totalBudget": 12000000.00,
  "totalSpent": 4800000.00,
  "totalRemaining": 7200000.00,
  "consumptionPercentage": 40.00,
  "activeGoalsCount": 8,
  "programs": [
    {
      "id": 37,
      "name": { "ar": "...", "en": "..." },
      "timelineFrom": "2024-01-01",
      "timelineTo": "2025-12-31",
      "plannedBudget": 2000000.00,
      "calculatedBudget": 2200000.00,
      "spent": 900000.00,
      "remaining": 1300000.00,
      "consumptionPercentage": 40.91,
      "goalId": 12,
      "goalName": { "ar": "...", "en": "..." }
    }
  ]
}
```

Example
- curl "{BASE}/analytics/program/budget-consumption?programIds=37"

---

### GET /Initiative-summary
On-Time vs Delayed Initiatives for programs (current vs previous quarter) with breakdown.

Parameters
- programIds: List<Long> (optional)

Response (ProgramMilestoneSummaryDto)
```json
{
  "onTimeInitiativesCurrent": 16,
  "delayedInitiativesCurrent": 15,
  "totalInitiativesCurrent": 31,
  "onTimeInitiativesPrevious": 20,
  "totalInitiativesPrevious": 35,
  "onTimeRateChangePercent": -33.0,
  "currentOnTimeRate": 51.6,
  "previousOnTimeRate": 57.1,
  "activeProgramsCount": 14,
  "programs": [
    {
      "programId": 37,
      "programName": { "ar": "...", "en": "..." },
      "currentInitiatives": { "total": 10, "onTime": 6, "delayed": 4, "rate": 60.0 },
      "previousInitiatives": { "total": 12, "onTime": 9, "rate": 75.0 },
      "rateChange": -20.0
    }
  ]
}
```

Example
- curl "{BASE}/analytics/program/Initiative-summary?programIds=37,40"

---

### GET /at-risk
Programs at Risk: counts, range, change vs last quarter.

Parameters
- programIds: List<Long> (optional)

Response (ProgramsAtRiskDto)
```json
{
  "riskScoreRange": "8 - 60%",
  "changeFromLastQuarter": 1,
  "totalPrograms": 14,
  "onTrackCount": 6,
  "atRiskCount": 5,
  "offTrackCount": 3,
  "onTrackPercent": 42.86,
  "atRiskPercent": 35.71,
  "offTrackPercent": 21.43,
  "avgRiskScore": 28.50,
  "combinedRiskPercentage": 57.14
}
```

Example
- curl "{BASE}/analytics/program/at-risk"

---

### GET /performance-vs-target
Per-program actual vs target with overall stats.

Parameters
- programIds: List<Long> (optional)

Response (ProgramPerformanceVsTargetDto)
```json
{
  "programs": [
    {
      "programId": 37,
      "programName": { "ar": "...", "en": "..." },
      "goalId": 12,
      "goalName": { "ar": "...", "en": "..." },
      "actualPercent": 62.50,
      "targetPercent": 70.00,
      "variance": -7.50,
      "status": "on_target"
    }
  ],
  "overallStats": {
    "totalPrograms": 14,
    "avgActualPercent": 58.91,
    "avgTargetPercent": 61.42,
    "overallVariance": -2.51,
    "aboveTargetCount": 4,
    "onTargetCount": 6,
    "belowTargetCount": 4
  }
}
```

Example
- curl "{BASE}/analytics/program/performance-vs-target?programIds=37,40"

---

### GET /budget-vs-progress
Monthly time-series for dual-axis chart: progress line (0–100%) vs monthly budget consumption bars.

Parameters
- programIds: List<Long> (optional)
- startDate: LocalDate (optional; defaults from data)
- endDate: LocalDate (optional; defaults from data)

Response (ProgramBudgetVsProgressSeriesDto)
```json
{
  "start": "2023-01-01",
  "end": "2025-10-21",
  "points": [
    {
      "monthLabel": "Jan",
      "month": "2025-01-31",
      "progressPercentage": 0.59,
      "budgetConsumption": 10000.00
    }
  ]
}
```

Chart Guidance
- X-axis: monthLabel (use month for sorting)
- Left Y-axis: progressPercentage × 100 (0–100%), nulls create gaps
- Right Y-axis: budgetConsumption (currency), zeros when no payments
- Includes all months in range

Examples
- curl "{BASE}/analytics/program/budget-vs-progress?programIds=10,20"
- curl "{BASE}/analytics/program/budget-vs-progress?startDate=2025-01-01&endDate=2025-09-30"

---

### GET /progress-series
Per-program progress series (month/quarter) similar to goal progress-series.

Parameters
- programIds: List<Long> (optional)
- granularity: month | quarter (default: month)
- startDate: LocalDate (optional; defaults from data)
- endDate: LocalDate (optional; defaults from data)

Response (ProgramProgressSeriesDto)
```json
{
  "granularity": "month",
  "start": "2024-01-01",
  "end": "2025-10-21",
  "series": [
    {
      "programId": 37,
      "nameTranslations": { "ar": "...", "en": "..." },
      "points": [
        { "date": "2025-06-30", "percent": 0.63 },
        { "date": "2025-07-31", "percent": 0.64 }
      ]
    }
  ]
}
```

Notes
- percent is normalized to 0..1 and may be null if no progress exists by period end
- date equals the period end (month-end or quarter-end)

Examples
- curl "{BASE}/analytics/program/progress-series?programIds=10,20"
- curl "{BASE}/analytics/program/progress-series?granularity=quarter&startDate=2024-01-01&endDate=2025-12-31"

## Error Handling
- Missing/empty filters aggregate across all programs where applicable
- Numeric fields consistently rounded; percentages normalized
- Dates are ISO date-only; parse accordingly on the client

## Change Log
- 2025-10-22: Beautified Markdown reference created (this file).
