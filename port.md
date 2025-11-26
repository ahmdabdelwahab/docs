# Portfolio Analytics API Documentation

## Overview
Portfolio Analytics provides comprehensive insights into annual plans, combining projects, initiatives, and indicators to deliver actionable health metrics, progress tracking, budget analysis, and KPI performance monitoring.

**Base URL:** `/analytics/portfolio`

---

## Table of Contents
1. [Dashboard & Overview](#dashboard--overview)
2. [Health Analytics](#health-analytics)
3. [Progress Analytics](#progress-analytics)
4. [Indicator & KPI Analytics](#indicator--kpi-analytics)
5. [Budget Analytics](#budget-analytics)
6. [Trend Analytics](#trend-analytics)
7. [Distribution Analytics](#distribution-analytics)

---

## Dashboard & Overview

## Health Analytics

### GET `/overall-health`
Get overall portfolio health score with weighted components.

**Health Status:**
- `HEALTHY`: ≥ 75
- `WATCH`: 60-74
- `CRITICAL`: < 60

**Query Parameters:**
- `planYear` (optional): Target year
- `quarter` (optional): Quarter number (1-4)

**Response:** `PortfolioOverallHealthDto`
```json
{
  "overallHealthScore": 72.5,
  "healthStatus": "WATCH",
  "currentPlanYear": 2025,
  "currentQuarter": 4,
  "currentQuarterTarget": 100.0,
  "totalInitiatives": 17,
  "totalProjects": 42,
  "totalIndicators": 156,
  "progressScore": 65.0,
  "budgetScore": 80.0,
  "indicatorsScore": 70.0
}
```

### GET `/overall-health/details`
Get paginated drill-down of projects and initiatives with individual health scores.

**Query Parameters:**
- `planYear` (optional): Target year
- `quarter` (optional): Quarter number (1-4)
- `healthStatus` (optional): Filter by status (`HEALTHY`, `WATCH`, `CRITICAL`)
- `page` (default: 0): Page number
- `size` (default: 20): Page size
- `sortBy` (default: `healthScore`): Sort field (`name`, `progressPercent`, `budgetConsumptionPercent`, `healthScore`)
- `sortDir` (default: `DESC`): Sort direction (`ASC`, `DESC`)

**Response:** `PortfolioDrillDownDto<PortfolioHealthDetailDto>`
```json
{
  "items": [
    {
      "id": 1,
      "name": { "en": "Project Name", "ar": "اسم المشروع" },
      "type": "PROJECT",
      "initiativeName": { "en": "Parent Initiative", "ar": "المبادرة الأم" },
      "healthScore": 85.5,
      "healthStatus": "HEALTHY",
      "progressPercent": 75.0,
      "budgetConsumptionPercent": 80.0,
      "plannedBudget": 1000000.0,
      "actualSpent": 800000.0,
      "indicatorsCount": 5,
      "indicatorsAchievement": 90.0,
      "startDate": "2024-01-01",
      "endDate": "2025-12-31"
    },
    {
      "id": 100,
      "name": { "en": "Initiative Name", "ar": "اسم المبادرة" },
      "type": "INITIATIVE",
      "initiativeName": null,
      "healthScore": 36.5,
      "healthStatus": "CRITICAL",
      "progressPercent": 0.0,
      "budgetConsumptionPercent": 40.0,
      "plannedBudget": 10000.0,
      "actualSpent": 4000.0,
      "indicatorsCount": 0,
      "indicatorsAchievement": 0.0,
      "startDate": "2024-01-30",
      "endDate": "2025-01-30"
    }
  ],
  "pagination": {
    "totalCount": 59,
    "totalPages": 3,
    "currentPage": 0,
    "pageSize": 20
  }
}
```

---

## Progress Analytics

### GET `/progress-overview`
Get overall progress overview with quarterly targets.

**Query Parameters:**
- `planYear` (optional): Target year
- `quarter` (optional): Quarter number (1-4)

**Response:** `ProgressOverviewDto`
```json
{
  "currentPlanYear": 2025,
  "currentQuarter": 4,
  "currentQuarterTarget": 100.0,
  "totalProjects": 42,
  "totalInitiatives": 17,
  "totalIndicators": 156,
  "averageProgress": 65.5,
  "onTrackCount": 28,
  "atRiskCount": 10,
  "behindScheduleCount": 4
}
```

### GET `/progress-overview/details`
Get paginated progress details for all entities.

**Query Parameters:**
- `planYear` (optional): Target year
- `quarter` (optional): Quarter number (1-4)
- `entityType` (default: `ALL`): Entity filter (`ALL`, `PROJECT`, `INITIATIVE`, `INDICATOR`)
- `page` (default: 0): Page number
- `size` (default: 20): Page size

**Response:** `PortfolioDrillDownDto<ProgressOverviewDetailDto>`
```json
{
  "items": [
    {
      "id": 1,
      "name": { "en": "Entity Name" },
      "entityType": "PROJECT",
      "currentProgress": 75.0,
      "plannedProgress": 80.0,
      "variance": -5.0,
      "status": "AT_RISK",
      "startDate": "2024-01-01",
      "endDate": "2025-12-31"
    }
  ],
  "pagination": { ... }
}
```

### GET `/progress-trend`
Get progress trend comparison across multiple plan years.

**Query Parameters:**
- `planYears` (optional): Comma-separated years (defaults to current and previous year)
- `timeUnit` (default: `MONTHLY`): Time granularity (`MONTHLY`, `QUARTERLY`)
- `startPeriod` (optional): Starting period number
- `endPeriod` (optional): Ending period number

**Response:** `PortfolioProgressTrendDto`
```json
{
  "timeUnit": "MONTHLY",
  "labels": ["Jan", "Feb", "Mar", "Apr", "May", "Jun"],
  "yearTrends": [
    {
      "planYear": 2024,
      "data": [10.5, 25.3, 42.1, 58.7, 71.2, 85.4]
    },
    {
      "planYear": 2025,
      "data": [8.2, 22.5, 38.9, 55.3, 68.1, 80.5]
    }
  ]
}
```

### GET `/progress-trend/details`
Get drill-down details for a specific time period.

**Query Parameters:**
- `planYear` (optional): Target year
- `period` (required): Period number (month 1-12 or quarter 1-4)
- `timeUnit` (default: `MONTHLY`): Time granularity
- `entityType` (default: `ALL`): Entity filter
- `page` (default: 0): Page number
- `size` (default: 20): Page size
- `sortBy` (default: `interpolatedProgress`): Sort field
- `sortDir` (default: `DESC`): Sort direction

**Response:** `PortfolioProgressTrendDrillDownDto`

---

## Indicator & KPI Analytics

### GET `/indicators-at-risk`
Get indicators risk analysis with trend comparison.

**Risk Levels:**
- `ON_TRACK`: ≥ 90% achievement
- `AT_RISK`: 60-89% achievement
- `OFF_TRACK`: < 60% achievement

**Query Parameters:**
- `planYear` (optional): Target year
- `quarter` (optional): Quarter number (1-4)

**Response:** `IndicatorsAtRiskDto`
```json
{
  "totalIndicators": 156,
  "onTrackCount": 98,
  "atRiskCount": 42,
  "offTrackCount": 16,
  "riskLevel": "MODERATE",
  "changeVsLastQuarter": -5,
  "trendDirection": "IMPROVING",
  "onTrackPercentage": 62.8,
  "atRiskPercentage": 26.9,
  "offTrackPercentage": 10.3
}
```

### GET `/indicators-at-risk/details`
Get paginated list of indicators with risk details.

**Query Parameters:**
- `planYear` (optional): Target year
- `quarter` (optional): Quarter number (1-4)
- `riskStatus` (optional): Filter by status (`ON_TRACK`, `AT_RISK`, `OFF_TRACK`)
- `page` (default: 0): Page number
- `size` (default: 10): Page size
- `sortBy` (default: `achievementPercent`): Sort field
- `sortDir` (default: `DESC`): Sort direction

**Response:** `PortfolioDrillDownDto<IndicatorAtRiskDetailDto>`
```json
{
  "items": [
    {
      "indicatorId": 42,
      "name": { "en": "Customer Satisfaction" },
      "measurementUnit": { "en": "Percentage" },
      "targetValue": 90.0,
      "actualValue": 55.0,
      "achievementPercent": 61.1,
      "riskStatus": "AT_RISK",
      "quarter": 4
    }
  ],
  "pagination": { ... }
}
```

### GET `/indicators-by-initiatives`
Get indicator achievement grouped by initiatives.

**Query Parameters:**
- `planYear` (optional): Target year
- `initiativeIds` (optional): Comma-separated initiative IDs

**Response:** `IndicatorsAchievementByInitiativesDto`
```json
{
  "initiatives": [
    {
      "initiativeId": 1,
      "initiativeName": { "en": "Digital Transformation" },
      "programName": { "en": "Technology Program" },
      "totalIndicators": 12,
      "achievedCount": 8,
      "partialCount": 3,
      "laggingCount": 1,
      "achievementPercent": 66.7
    }
  ],
  "totalAchieved": 98,
  "totalPartial": 42,
  "totalLagging": 16,
  "totalIndicators": 156,
  "achievedPercent": 62.8,
  "partialPercent": 26.9,
  "laggingPercent": 10.3
}
```

### GET `/kpi-dashboard`
Get KPI performance dashboard with top/bottom performing indicators.

**Query Parameters:**
- `planYear` (optional): Target year
- `quarter` (optional): Quarter number (1-4)
- `initiativeIds` (optional): Comma-separated initiative IDs
- `sortBy` (default: `TOP_PERFORMING`): Sort order (`TOP_PERFORMING`, `BOTTOM_PERFORMING`)
- `page` (default: 1): Page number
- `size` (default: 10): Page size

**Response:** `KpiPerformanceDashboardDto`
```json
{
  "kpis": [
    {
      "indicatorId": 42,
      "name": { "en": "Customer Satisfaction" },
      "measurementUnit": { "en": "Percentage" },
      "targetValue": 90.0,
      "actualValue": 95.5,
      "achievementPercent": 106.1,
      "performanceStatus": "EXCEEDING",
      "trendDirection": "UP"
    }
  ],
  "totalKpis": 156,
  "avgAchievementPercent": 85.3,
  "pagination": { ... }
}
```

### GET `/kpi-dashboard/details`
Get drill-down for projects/initiatives linked to a specific indicator.

**Query Parameters:**
- `planYear` (optional): Target year
- `quarter` (optional): Quarter number (1-4)
- `indicatorId` (required): Indicator ID
- `entityType` (default: `ALL`): Entity filter (`ALL`, `PROJECT`, `INITIATIVE`)
- `page` (default: 0): Page number
- `size` (default: 20): Page size
- `sortBy` (default: `entityProgress`): Sort field
- `sortDir` (default: `DESC`): Sort direction

**Response:** `KpiDrillDownResponseDto`
```json
{
  "kpiInfo": {
    "indicatorId": 42,
    "name": { "en": "Customer Satisfaction" },
    "measurementUnit": { "en": "Percentage" },
    "targetValue": 90.0,
    "actualValue": 95.5,
    "achievementPercent": 106.1
  },
  "linkedEntities": {
    "items": [
      {
        "entityId": 1,
        "entityName": { "en": "Project Name" },
        "entityType": "PROJECT",
        "entityProgress": 85.0,
        "entityStatus": "ON_TRACK"
      }
    ],
    "pagination": { ... }
  }
}
```

---

## Budget Analytics

### GET `/budget-consumption`
Get overall budget consumption metrics.

**Query Parameters:**
- `planYear` (optional): Target year
- `initiativeIds` (optional): Comma-separated initiative IDs
- `projectIds` (optional): Comma-separated project IDs
- `quarter` (optional): Quarter number (1-4)

**Response:** `BudgetConsumptionDto`
```json
{
  "totalPlannedBudget": 50000000.0,
  "totalActualSpent": 38500000.0,
  "consumptionPercent": 77.0,
  "remainingBudget": 11500000.0,
  "burnRate": 3850000.0,
  "projectedOverrun": 0.0,
  "consumptionStatus": "ON_TRACK"
}
```

### GET `/budget-consumption/details`
Get paginated budget consumption details by entity.

**Query Parameters:**
- `planYear` (optional): Target year
- `page` (default: 0): Page number
- `size` (default: 10): Page size
- `sortBy` (default: `consumption`): Sort field
- `sortDir` (default: `DESC`): Sort direction

**Response:** `PortfolioDrillDownDto<BudgetConsumptionDetailDto>`
```json
{
  "items": [
    {
      "entityId": 1,
      "entityName": { "en": "Project Name" },
      "entityType": "PROJECT",
      "plannedBudget": 1000000.0,
      "actualSpent": 850000.0,
      "consumptionPercent": 85.0,
      "remainingBudget": 150000.0,
      "status": "AT_RISK"
    }
  ],
  "pagination": { ... }
}
```

### GET `/budget-consumption-trend`
Get budget consumption trend over time.

**Query Parameters:**
- `planYear` (optional): Target year
- `initiativeIds` (optional): Comma-separated initiative IDs
- `projectIds` (optional): Comma-separated project IDs
- `startMonth` (optional): Starting month (1-12)
- `endMonth` (optional): Ending month (1-12)

**Response:** `BudgetConsumptionTrendDto`
```json
{
  "months": ["Jan", "Feb", "Mar", "Apr", "May", "Jun"],
  "plannedBudget": [5000000, 10000000, 15000000, 20000000, 25000000, 30000000],
  "actualSpent": [4200000, 8500000, 13200000, 18100000, 23400000, 28900000],
  "consumptionRate": [84.0, 85.0, 88.0, 90.5, 93.6, 96.3]
}
```

### GET `/budget-consumption-trend/details`
Get drill-down for a specific month in the trend.

**Query Parameters:**
- `planYear` (optional): Target year
- `month` (required): Month number (1-12)
- `page` (default: 0): Page number
- `size` (default: 10): Page size
- `sortBy` (default: `consumptionPercent`): Sort field
- `sortDir` (default: `DESC`): Sort direction

**Response:** `PortfolioDrillDownDto<BudgetConsumptionTrendDetailDto>`

### GET `/budget-by-project`
Get budget allocation breakdown by project/initiative.

**Query Parameters:**
- `planYear` (optional): Target year
- `initiativeIds` (optional): Comma-separated initiative IDs
- `projectIds` (optional): Comma-separated project IDs
- `includeProjects` (default: `true`): Include projects
- `includeInitiatives` (default: `true`): Include initiatives

**Response:** `BudgetAllocationByProjectDto`
```json
{
  "entities": [
    {
      "entityId": 1,
      "entityName": { "en": "Project Name" },
      "entityType": "PROJECT",
      "allocatedBudget": 1000000.0,
      "percentageOfTotal": 2.0
    }
  ],
  "totalBudget": 50000000.0
}
```

---

## Trend Analytics

### GET `/project-achievement-trend`
Get project achievement trend over time.

**Query Parameters:**
- `planYear` (optional): Target year
- `initiativeIds` (optional): Comma-separated initiative IDs
- `projectIds` (optional): Comma-separated project IDs
- `startMonth` (optional): Starting month (1-12)
- `endMonth` (optional): Ending month (1-12)
- `entityType` (default: `PROJECTS`): Entity type filter

**Response:** `ProjectAchievementTrendDto`
```json
{
  "months": ["Jan", "Feb", "Mar", "Apr", "May", "Jun"],
  "averageAchievement": [15.5, 32.8, 48.3, 62.7, 75.4, 87.2],
  "targetAchievement": [16.7, 33.3, 50.0, 66.7, 83.3, 100.0]
}
```

### GET `/project-achievement-trend/details`
Get drill-down for a specific month.

**Query Parameters:**
- `planYear` (optional): Target year
- `month` (required): Month number (1-12)
- `projectId` (optional): Filter by project ID
- `initiativeId` (optional): Filter by initiative ID
- `page` (default: 0): Page number
- `size` (default: 10): Page size
- `sortBy` (default: `achievementPercent`): Sort field
- `sortDir` (default: `DESC`): Sort direction

**Response:** `PortfolioDrillDownDto<ProjectAchievementDetailDto>`

---

## Distribution Analytics

### GET `/progress-distribution`
Get progress distribution across status categories.

**Query Parameters:**
- `planYear` (optional): Target year
- `quarter` (optional): Quarter number (1-4)
- `includeProjects` (default: `true`): Include projects
- `includeInitiatives` (default: `false`): Include initiatives

**Response:** `ProgressDistributionDto`
```json
{
  "distribution": [
    {
      "status": "NOT_STARTED",
      "count": 5,
      "percentage": 8.5
    },
    {
      "status": "IN_PROGRESS",
      "count": 42,
      "percentage": 71.2
    },
    {
      "status": "COMPLETED",
      "count": 12,
      "percentage": 20.3
    }
  ],
  "totalEntities": 59
}
```

### GET `/progress-distribution/details`
Get paginated entities for a specific status.

**Query Parameters:**
- `planYear` (optional): Target year
- `quarter` (optional): Quarter number (1-4)
- `status` (optional): Filter by status (`NOT_STARTED`, `IN_PROGRESS`, `COMPLETED`, `ON_HOLD`)
- `entityType` (default: `PROJECT`): Entity type (`PROJECT`, `INITIATIVE`)
- `page` (default: 0): Page number
- `size` (default: 20): Page size
- `sortBy` (default: `progress`): Sort field
- `sortDir` (default: `ASC`): Sort direction

**Response:** `PortfolioDrillDownDto<ProgressDistributionDetailDto>`
```json
{
  "items": [
    {
      "entityId": 1,
      "entityName": { "en": "Project Name" },
      "entityType": "PROJECT",
      "progress": 75.5,
      "status": "IN_PROGRESS",
      "startDate": "2024-01-01",
      "endDate": "2025-12-31"
    }
  ],
  "pagination": { ... }
}
```

### GET `/budget-utilization-vs-achievement`
Get scatter plot data comparing budget utilization vs achievement.

**Query Parameters:**
- `planYear` (optional): Target year
- `initiativeIds` (optional): Comma-separated initiative IDs
- `projectIds` (optional): Comma-separated project IDs
- `includeProjects` (default: `true`): Include projects
- `includeInitiatives` (default: `true`): Include initiatives

**Response:** `BudgetUtilizationVsAchievementDto`
```json
{
  "dataPoints": [
    {
      "entityId": 1,
      "entityName": { "en": "Project Name" },
      "entityType": "PROJECT",
      "budgetUtilization": 85.0,
      "achievementPercent": 78.5
    }
  ]
}
```

---

## Upcoming Deadlines

### GET `/upcoming-deadlines`
Get upcoming project/initiative deadlines.

**Query Parameters:**
- `planYear` (optional): Target year
- `initiativeIds` (optional): Comma-separated initiative IDs
- `projectIds` (optional): Comma-separated project IDs
- `quarter` (optional): Quarter number (1-4)
- `limit` (default: 10): Maximum results

**Response:** `UpcomingDeadlinesDto`
```json
{
  "deadlines": [
    {
      "entityId": 1,
      "entityName": { "en": "Project Name" },
      "entityType": "PROJECT",
      "endDate": "2025-12-31",
      "daysRemaining": 45,
      "currentProgress": 65.5,
      "status": "AT_RISK"
    }
  ]
}
```

---

## Common Data Structures

### Pagination Metadata
```json
{
  "totalCount": 156,
  "totalPages": 8,
  "currentPage": 0,
  "pageSize": 20
}
```

### Multilingual Name
```json
{
  "en": "English Name",
  "ar": "الاسم العربي",
  "fr": "Nom français",
  "de": "Deutscher Name",
  "sw": "Jina la Kiswahili"
}
```

### Entity Types
- `PROJECT`: Project entity
- `INITIATIVE`: Initiative entity
- `INDICATOR`: Indicator/KPI entity

### Health Status
- `HEALTHY`: Health score ≥ 75
- `WATCH`: Health score 60-74
- `CRITICAL`: Health score < 60

### Risk Status
- `ON_TRACK`: Achievement ≥ 90%
- `AT_RISK`: Achievement 60-89%
- `OFF_TRACK`: Achievement < 60%

---

## Notes

1. **Default Year**: If `planYear` is not provided, the current year is used.
2. **Pagination**: All list endpoints support pagination with `page` and `size` parameters.
3. **Sorting**: Most detail endpoints support custom sorting with `sortBy` and `sortDir` parameters.
4. **Filtering**: Endpoints support filtering by various criteria (status, entity type, etc.).
5. **Multilingual Support**: All names and descriptions support multiple languages (EN, AR, FR, DE, SW).
6. **Data Source**: All endpoints use `indicator_per_year` table for indicator data.
7. **Health Formula**: Overall health = (Progress × 35%) + (Budget × 40%) + (Indicators × 25%)

---

## Error Responses

All endpoints return standard HTTP status codes:
- `200 OK`: Successful request
- `400 Bad Request`: Invalid parameters
- `404 Not Found`: Resource not found
- `500 Internal Server Error`: Server error

Error response format:
```json
{
  "timestamp": "2025-11-26T10:30:00Z",
  "status": 400,
  "error": "Bad Request",
  "message": "Invalid quarter parameter: must be between 1 and 4",
  "path": "/analytics/portfolio/overall-health"
}
```
