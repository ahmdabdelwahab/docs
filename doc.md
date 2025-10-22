━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Program Analytics API
Beautiful Reference & Charting Guide
Last updated: 2025-10-22
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Table of Contents
1) Overview
2) Endpoints Overview
3) Usage Notes
4) Error Handling
5) Change Log

# Program Analytics API — Comprehensive Documentation

NOTE: This documentation has been migrated to PROGRAM_ANALYTICS_API.docx for Google Docs compatibility. If you are collaborating via Google Docs, use the .docx version. The Markdown version is retained here for reference.

This document describes the 8 Program Analytics endpoints exposed under the /analytics/program namespace. It covers each endpoint’s purpose, request parameters, response structure, and example usage. All endpoints are GET and accept optional filters unless otherwise stated.

Base path prefix used below: /analytics/program

Notes
- Multi-tenant and authentication: This document only covers the analytics endpoints and their data contracts. Security/tenancy is configured at the application level.
- Date parameters use ISO-8601 format (YYYY-MM-DD).
- programIds, goalIds, ids are CSV lists when used from a browser; Spring also supports repeated parameters (e.g., ?programIds=10&programIds=20).

Endpoints overview
1. GET /list — Filter list of programs
2. GET /achievement-summary — Program achievement headline + mini trend
3. GET /budget-consumption — Budget consumption card per program
4. GET /Initiative-summary — On-Time vs. Delayed Initiatives (program breakdown)
5. GET /at-risk — Programs at Risk card
6. GET /performance-vs-target — Program performance vs target card
7. GET /budget-vs-progress — Monthly Budget Consumption vs Progress series
8. GET /progress-series — Program Progress time-series (per program)

---

1) GET /list
Purpose
Returns a list of programs for filter dropdowns, optionally filtered by goal IDs and/or program IDs.

Query parameters
- goalIds: List<Long> (optional) — Filter by Goal IDs (program direct parent)
- ids: List<Long> (optional) — Filter by Program IDs

Response (ProgramListFilterDto)
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

Examples
- curl "{BASE}/analytics/program/list"
- curl "{BASE}/analytics/program/list?goalIds=12,15"
- curl "{BASE}/analytics/program/list?ids=37,40"

---

2) GET /achievement-summary
Purpose
Aggregated current achievement, target planned, variance, mini-trend sparkline, and active programs count for the selected set of programs.

Query parameters
- programIds: List<Long> (optional) — If omitted, aggregates across all programs

Response (ProgramAchievementSummaryDto)
{
  "currentAchievement": 0.35,           // 0..1, rounded to 2 decimals
  "targetPlanned": 0.40,               // 0..1, rounded to 2 decimals
  "variance": -0.05,                   // 0..1 (actual - planned), rounded to 2 decimals
  "miniTrend": [                        // last 5 months average progress
    { "date": "2025-06-01", "avgPercent": 0.31 },
    ...
  ],
  "activeGoalsCount": 12
}
Notes
- Percent fields are normalized to 0..1 and rounded to two decimals.

Example
- curl "{BASE}/analytics/program/achievement-summary?programIds=10,20"

---

3) GET /budget-consumption
Purpose
Provides a budget consumption card with per-program lines including budgets, spent, remaining, and consumption percentage.

Query parameters
- programIds: List<Long> (optional) — If omitted, includes all programs

Response (ProgramBudgetConsumptionDto)
{
  "totalBudget": 12000000.00,
  "totalSpent": 4800000.00,
  "totalRemaining": 7200000.00,
  "consumptionPercentage": 40.00,       // percent 0..100 rounded to 2 decimals
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

Example
- curl "{BASE}/analytics/program/budget-consumption?programIds=37"

---

4) GET /Initiative-summary
Purpose
On-Time vs Delayed Initiatives derived from initiatives under each program. Shows current and previous quarter aggregates with per-program breakdown.

Query parameters
- programIds: List<Long> (optional)

Response (ProgramMilestoneSummaryDto)
{
  "onTimeInitiativesCurrent": 16,
  "delayedInitiativesCurrent": 15,
  "totalInitiativesCurrent": 31,
  "onTimeInitiativesPrevious": 20,
  "totalInitiativesPrevious": 35,
  "onTimeRateChangePercent": -33.0,     // percentage change vs previous on-time rate
  "currentOnTimeRate": 51.6,            // % in current quarter
  "previousOnTimeRate": 57.1,           // % in previous quarter
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

Example
- curl "{BASE}/analytics/program/Initiative-summary?programIds=37,40"

---

5) GET /at-risk
Purpose
Programs at Risk card with counts by risk status, range, and change vs last quarter.

Query parameters
- programIds: List<Long> (optional)

Response (ProgramsAtRiskDto)
{
  "riskScoreRange": "8 - 60%",
  "changeFromLastQuarter": 1,           // displayed as "+1% vs Last Quarter"
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

Example
- curl "{BASE}/analytics/program/at-risk"

---

6) GET /performance-vs-target
Purpose
Compares actual vs target progress per program, with overall averages and count by status.

Query parameters
- programIds: List<Long> (optional)

Response (ProgramPerformanceVsTargetDto)
{
  "programs": [
    {
      "programId": 37,
      "programName": { "ar": "...", "en": "..." },
      "goalId": 12,
      "goalName": { "ar": "...", "en": "..." },
      "actualPercent": 62.50,            // 0..100, rounded
      "targetPercent": 70.00,            // 0..100, rounded
      "variance": -7.50,                 // actual - target
      "status": "on_target"             // above_target | on_target | below_target
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

Example
- curl "{BASE}/analytics/program/performance-vs-target?programIds=37,40"

---

7) GET /budget-vs-progress
Purpose
Monthly time-series suitable for a dual-axis chart: progress line (left axis, percent 0–100%) vs. monthly budget consumption bars (right axis, currency). Always includes all calendar months in range.

Query parameters
- programIds: List<Long> (optional)
- startDate: LocalDate (optional, ISO) — Inclusive; defaults to earliest data month
- endDate: LocalDate (optional, ISO) — Inclusive; defaults to latest data month

Response (ProgramBudgetVsProgressSeriesDto)
{
  "start": "2023-01-01",
  "end": "2025-10-21",
  "points": [
    {
      "monthLabel": "Jan",              // English short month name
      "month": "2025-01-31",           // period end (month end)
      "progressPercentage": 0.59,        // 0..1, 2 decimals; null if no progress yet
      "budgetConsumption": 10000.00      // currency aggregated from PROGRAM + INITIATIVE payments
    }
  ]
}

Chart guidance
- X-axis: monthLabel (string). Ensure months are rendered in chronological order using "month" as the sort key.
- Left Y-axis (line): progressPercentage × 100 (0–100%). Nulls create gaps.
- Right Y-axis (bars): budgetConsumption (currency). Show zeros when no payments in a month.
- Gaps: All calendar months in [start, end] are included even without data.

Examples
- curl "{BASE}/analytics/program/budget-vs-progress?programIds=10,20"
- curl "{BASE}/analytics/program/budget-vs-progress?startDate=2025-01-01&endDate=2025-09-30"

---

8) GET /progress-series
Purpose
Per-program progress time-series similar to the goal progress-series. Returns latest progress value per period end (month/quarter) for each program.

Query parameters
- programIds: List<Long> (optional)
- granularity: String (optional, default: month) — Allowed: month | quarter
- startDate: LocalDate (optional, ISO) — Inclusive; defaults from data bounds
- endDate: LocalDate (optional, ISO) — Inclusive; defaults from data bounds

Response (ProgramProgressSeriesDto)
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

Notes
- percent is normalized to 0..1 and may be null when no progress exists yet by period end.
- date equals the period end (month-end or quarter-end) for each generated period between start and end.

Examples
- curl "{BASE}/analytics/program/progress-series?programIds=10,20"
- curl "{BASE}/analytics/program/progress-series?granularity=quarter&startDate=2024-01-01&endDate=2025-12-31"

---

Error handling & nulls
- Missing/empty filters return aggregated results where applicable.
- Numeric fields may be 0 when undefined; percentage outputs are consistently rounded.
- Dates are ISO format; ensure your client parses to local time or treats them as date-only.

Change log
- 2025-10-22: Initial consolidated documentation added for the 8 Program Analytics endpoints.
