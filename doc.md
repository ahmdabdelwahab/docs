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


## Endpoints

### GET /list
Returns programs for filter dropdowns.

Parameters
- ids: List<Long> (optional)

Response (ProgramListFilterDto)
```json
{
    "data": [
        {
            "id": 32,
            "name": {
                "en": "The national program to improve government services and simplify procedures",
                "ar": "البرنامج الوطني لتحسين الخدمات الحكومية وتبسيط الإجراءات"
            },
            "goalId": 29,
            "goalName": {
                "en": "Enhancing the efficiency of providing government services and improving the experience of beneficiaries",
                "ar": "تعزيز كفاءة تقديم الخدمات الحكومية وتحسين تجربة المستفيدين"
            },
            "strategyId": 5,
            "strategyName": {
                "en": "Strategic plan for institutional excellence and quality of services",
                "ar": "الخطة الاستراتيجية للتميز المؤسسي وجودة الخدمات"
            }
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


## On-Time vs Delayed Programs

### Endpoint
```
GET /analytics/program/on-time-vs-delayed-programs
```

### Description
Analyzes programs to determine which are on track and which are delayed by comparing actual progress against planned progress (checkpoints).

### Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `programIds` | List<Long> | No | Filter by specific program IDs. If empty, analyzes all programs. |
| `goalIds` | List<Long> | No | Filter programs by their parent goal IDs. |

### Request Example
```http
GET /analytics/program/on-time-vs-delayed-programs?programIds=1,2,3&goalIds=5,6
```

### Response Structure
```json
{
  "totalPrograms": 10,
  "onTimeCount": 7,
  "delayedCount": 3,
  "onTimePercent": 70.00,
  "delayedPercent": 30.00
}
```

### Response Fields
| Field | Type | Description |
|-------|------|-------------|
| `totalPrograms` | Long | Total number of programs analyzed |
| `onTimeCount` | Long | Number of programs where actual >= planned progress |
| `delayedCount` | Long | Number of programs where actual < planned progress |
| `onTimePercent` | BigDecimal | Percentage of programs on time |
| `delayedPercent` | BigDecimal | Percentage of programs delayed |

### Business Logic
- **On Time**: Program is considered on-time if `actual_progress >= planned_progress`
- **Delayed**: Program is considered delayed if `actual_progress < planned_progress`
- Uses latest actual progress from `program_progress_log`
- Uses latest planned progress from `program_checkpoint`

### Use Cases
- Dashboard KPI showing program delivery health
- Executive summary of program performance
- Alert system for delayed programs
- Trend analysis over time

---

## Overall Health Index

### Endpoint
```
GET /analytics/program/overall-health-index
```

### Description
Calculates comprehensive health metrics for programs based on three key components: Progress Health, Budget Health, and Indicator Health.

### Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `programIds` | List<Long> | No | Filter by specific program IDs. If empty, analyzes all programs. |

### Request Example
```http
GET /analytics/program/overall-health-index?programIds=1,2,3
```

### Response Structure
```json
{
  "overallHealthScore": 75.50,
  "healthStatus": "healthy",
  "componentScores": {
    "progressScore": 80.00,
    "budgetScore": 85.00,
    "indicatorsScore": 62.00
  },
  "programs": [
    {
      "programId": 1,
      "programName": {
        "ar": "برنامج التحول الرقمي",
        "en": "Digital Transformation Program"
      },
      "progressHealth": 82.50,
      "budgetHealth": 90.00,
      "indicatorHealth": 70.00,
      "overallHealth": 80.83,
      "healthStatus": "healthy",
      "actualProgress": 45.00,
      "plannedProgress": 40.00,
      "plannedBudget": 5000000.00,
      "actualPayments": 2200000.00,
      "expectedSpending": 2000000.00,
      "budgetAdherenceScore": 100.00,
      "burnRateScore": 90.00,
      "totalIndicators": 10,
      "achievedIndicators": 7
    }
  ]
}
```

### Health Components

#### 1. Progress Health (0-100%)
- Measures actual vs planned progress alignment
- Formula: `(actual_progress / planned_progress) * 100`, capped at 100
- If no planned checkpoints exist, uses actual progress directly

#### 2. Budget Health (0-100%)
- Composite of two sub-scores:
  - **Budget Adherence Score**: Penalizes overspending
  - **Burn Rate Score**: Measures spending pace alignment with timeline
- Formula: `(Budget Adherence + Burn Rate) / 2`

#### 3. Indicator Health (0-100%)
- Percentage of KPIs achieving their targets
- Based on current quarter's actual vs target values
- Only includes active indicators

#### Overall Health Score
- Average of the three component scores
- Only components with available data are included in the average

### Health Status Categories
| Score Range | Status | Description |
|-------------|--------|-------------|
| 75-100 | `healthy` | Program is performing well across all metrics |
| 60-74 | `moderate` | Program has some concerns but manageable |
| 0-59 | `critical` | Program requires immediate attention |

### Use Cases
- Executive dashboard showing program portfolio health
- Risk identification and prioritization
- Resource allocation decisions
- Performance review meetings
- Drill-down analysis for troubled programs

---

## Milestone Status

### Endpoint
```
GET /analytics/program/milestone-status
```

### Description
Analyzes program checkpoints (milestones) to determine which have been achieved on time by comparing actual progress against planned progress at specific dates.

### Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `programIds` | List<Long> | No | Filter by specific program IDs. If empty, analyzes all programs. |

### Request Example
```http
GET /analytics/program/milestone-status?programIds=1,2,3
```

### Response Structure
```json
{
  "programs": [
    {
      "programId": 1,
      "programName": {
        "ar": "برنامج التحول الرقمي",
        "en": "Digital Transformation Program"
      },
      "totalMilestones": 8,
      "onTimeMilestones": 6,
      "delayedMilestones": 2,
      "completionRate": 75.00
    },
    {
      "programId": 2,
      "programName": {
        "ar": "برنامج التميز المؤسسي",
        "en": "Organizational Excellence Program"
      },
      "totalMilestones": 5,
      "onTimeMilestones": 5,
      "delayedMilestones": 0,
      "completionRate": 100.00
    }
  ]
}
```

### Response Fields
| Field | Type | Description |
|-------|------|-------------|
| `programId` | Long | Program identifier |
| `programName` | NameDto | Program name in Arabic and English |
| `totalMilestones` | Long | Total number of checkpoints/milestones for the program |
| `onTimeMilestones` | Long | Number of milestones achieved on or before their target date |
| `delayedMilestones` | Long | Number of milestones not achieved by their target date |
| `completionRate` | BigDecimal | Percentage of milestones achieved on time |

### Business Logic
- Only considers checkpoints up to current date (past checkpoints)
- A milestone is **on-time** if: `actual_progress_at_checkpoint_date >= planned_progress`
- A milestone is **delayed** if: `actual_progress_at_checkpoint_date < planned_progress`
- Uses `program_checkpoint` table for planned milestones
- Uses `program_progress_log` for actual progress tracking

### Use Cases
- Track milestone delivery performance
- Identify programs struggling with checkpoint adherence
- Early warning system for project delays
- Program manager performance review
- Stakeholder reporting on deliverable timelines

---

## Indicator Achievement

### Endpoint
```
GET /analytics/program/indicator-achievement
```

### Description
Analyzes the achievement status of Key Performance Indicators (KPIs) associated with programs, categorized as achieved, partial, or lagging based on current quarter targets.

### Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `programIds` | List<Long> | No | Filter by specific program IDs. If empty, analyzes all programs. |

### Request Example
```http
GET /analytics/program/indicator-achievement?programIds=1,2,3
```

### Response Structure
```json
{
  "programs": [
    {
      "programId": 1,
      "programName": {
        "ar": "برنامج التحول الرقمي",
        "en": "Digital Transformation Program"
      },
      "totalIndicators": 10,
      "achievedCount": 7,
      "partialCount": 2,
      "laggingCount": 1,
      "achievedPercentage": 70.00,
      "partialPercentage": 20.00,
      "laggingPercentage": 10.00
    }
  ]
}
```

### Response Fields
| Field | Type | Description |
|-------|------|-------------|
| `programId` | Long | Program identifier |
| `programName` | NameDto | Program name in Arabic and English |
| `totalIndicators` | Long | Total number of active indicators linked to the program |
| `achievedCount` | Long | Number of indicators meeting or exceeding target |
| `partialCount` | Long | Number of indicators at 50-99% of target |
| `laggingCount` | Long | Number of indicators below 50% of target |
| `achievedPercentage` | BigDecimal | Percentage of indicators fully achieved |
| `partialPercentage` | BigDecimal | Percentage of indicators partially achieved |
| `laggingPercentage` | BigDecimal | Percentage of indicators lagging |

### Achievement Categories
| Category | Criteria | Description |
|----------|----------|-------------|
| **Achieved** | `actual >= target` | Indicator has met or exceeded its quarterly target |
| **Partial** | `0.5 × target <= actual < target` | Indicator is 50-99% of target (making progress) |
| **Lagging** | `actual < 0.5 × target` | Indicator is below 50% of target (needs attention) |

### Business Logic
- Uses current quarter's data (Q1, Q2, Q3, or Q4)
- Only includes indicators with status `ACTIVE`
- Compares actual vs target values from `indicator_per_year` table
- Linked through `spm_program_indicators` junction table

### Use Cases
- KPI dashboard showing program effectiveness
- Identify programs with poor indicator performance
- Resource reallocation based on underperforming KPIs
- Quarterly performance reviews
- Strategic goal alignment tracking

---


---

### GET /performance-variance
Performance variance across quarters/months showing difference between actual and target performance over time.

**Purpose**: Visualizes variance trends for programs with positive (ahead of target) and negative (behind target) indicators. Supports the "Performance Variance Across Quarters" chart with multiple programs.

Parameters
- programIds: List<Long> (optional) - If omitted, includes all programs
- startDate: LocalDate (optional, ISO) - Inclusive start date; defaults to earliest data
- endDate: LocalDate (optional, ISO) - Inclusive end date; defaults to latest data
- granularity: String (optional, default: "quarter") - Time period: "quarter" or "month"

Response (ProgramPerformanceVarianceDto)
```json
{
  "programs": [
    {
      "programId": 37,
      "programName": { "ar": "...", "en": "..." },
      "goalId": 12,
      "goalName": { "ar": "...", "en": "..." },
      "dataPoints": [
        {
          "period": "Q4 2025",
          "periodStart": "2025-10-01",
          "periodEnd": "2025-12-31",
          "actualPercent": 50.00,
          "targetPercent": 57.00,
          "variancePercent": -7.00,
          "absVariance": 7.00,
          "status": "BEHIND"
        },
        {
          "period": "Q1 2026",
          "periodStart": "2026-01-01",
          "periodEnd": "2026-03-31",
          "actualPercent": 60.00,
          "targetPercent": 50.00,
          "variancePercent": 10.00,
          "absVariance": 10.00,
          "status": "ON_TRACK"
        }
      ],
      "averageVariance": -2.50,
      "maxPositiveVariance": 10.00,
      "maxNegativeVariance": -7.00,
      "positivePeriodsCount": 3,
      "negativePeriodsCount": 4
    }
  ],
  "periods": [
    {
      "period": "Q4 2025",
      "periodStart": "2025-10-01",
      "periodEnd": "2025-12-31",
      "order": 1
    }
  ],
  "summary": {
    "totalPrograms": 3,
    "totalPeriods": 6,
    "overallAverageVariance": -1.25,
    "programsAheadCount": 1,
    "programsBehindCount": 1,
    "programsOnTrackCount": 1,
    "maxPositiveVariance": 15.00,
    "maxNegativeVariance": -20.00,
    "bestPeriod": "Q1 2027",
    "worstPeriod": "Q3 2026"
  },
  "granularity": "quarter"
}
```

Variance Status Values
- `AHEAD`: Variance > +10% (significantly ahead of target)
- `ON_TRACK`: Variance within ±5%
- `BEHIND`: Variance < -5% (behind target)
- `CRITICAL`: Variance < -15% (significantly behind)

Chart Guidance
- X-axis: period labels (e.g., "Q4 2025", "Jan 2026")
- Y-axis: variancePercent (-100 to +100)
- Bars: Positive values above zero line, negative values below
- Colors: Differentiate programs with distinct colors
- Zero line: Horizontal line at 0% for visual reference
- Annotations: Display variance value on each bar

Notes
- All percentages are 0-100 scale, rounded to 2 decimals
- Variance = Actual - Target (positive = ahead, negative = behind)
- Missing progress data results in 0 for actual/target
- Automatically fills all periods in date range, even with no data


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
