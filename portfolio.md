# Portfolio Analytics API Documentation

## Overview
This document describes the Portfolio Analytics REST API endpoints for the front-end team. All endpoints are under the base path `/analytics/portfolio`.

**Base URL**: `/analytics/portfolio`

**Authentication**: All endpoints require JWT Bearer token in Authorization header.

---

## Table of Contents
1. [Dashboard & Summary Endpoints](#dashboard--summary-endpoints)
2. [Visualization Endpoints](#visualization-endpoints)
3. [Trend & Analysis Endpoints](#trend--analysis-endpoints)
4. [KPI Performance Endpoints](#kpi-performance-endpoints)

---

## Dashboard & Summary Endpoints

### 1. Portfolio Dashboard
**GET** `/dashboard`

Main dashboard endpoint providing comprehensive portfolio overview.

#### Query Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `planYear` | Integer | No | Annual plan year (defaults to current year) |
| `initiativeIds` | String | No | CSV list of initiative IDs to filter (e.g., "1,2,3") |
| `projectIds` | String | No | CSV list of project IDs to filter (e.g., "10,20,30") |
| `quarter` | Integer | No | Quarter number 1-4 (defaults to current quarter) |

#### Response Example
```json
{
  "planYear": 2025,
  "quarter": 2,
  "summary": {
    "totalInitiatives": 15,
    "totalProjects": 42,
    "totalIndicators": 68,
    "overallProgress": 58.3,
    "budgetUtilization": 62.5
  },
  "health": {
    "status": "HEALTHY",
    "score": 78.5
  },
  "trends": {
    "progressChange": 5.2,
    "budgetChange": 8.1
  }
}
```

#### Example
```
GET /analytics/portfolio/dashboard?planYear=2025&quarter=2
GET /analytics/portfolio/dashboard?planYear=2025&initiativeIds=1,5,8&quarter=3
```

---

### 2. Overall Health
**GET** `/overall-health`

Returns overall portfolio health metrics and status indicators.

#### Query Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `planYear` | Integer | No | Annual plan year |
| `initiativeIds` | String | No | CSV list of initiative IDs |
| `projectIds` | String | No | CSV list of project IDs |
| `quarter` | Integer | No | Quarter number 1-4 |

#### Response Example
```json
{
  "overallStatus": "HEALTHY",
  "healthScore": 78.5,
  "metrics": {
    "progressHealth": 82.0,
    "budgetHealth": 75.0,
    "scheduleHealth": 78.5,
    "riskHealth": 68.0
  },
  "summary": {
    "onTrackCount": 35,
    "atRiskCount": 10,
    "criticalCount": 5,
    "totalItems": 50
  }
}
```

#### Example
```
GET /analytics/portfolio/overall-health?planYear=2025&quarter=2
```

---

### 3. Indicators at Risk
**GET** `/indicators-at-risk`

Lists indicators that are at risk or underperforming.

#### Query Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `planYear` | Integer | No | Annual plan year |
| `initiativeIds` | String | No | CSV list of initiative IDs |
| `projectIds` | String | No | CSV list of project IDs |
| `quarter` | Integer | No | Quarter number 1-4 |

#### Response Example
```json
{
  "totalAtRisk": 12,
  "indicators": [
    {
      "indicatorId": 45,
      "indicatorName": "Customer Retention Rate",
      "initiativeId": 5,
      "initiativeName": "Customer Experience Initiative",
      "target": 85.0,
      "actual": 72.0,
      "variance": -13.0,
      "status": "AT_RISK",
      "riskLevel": "HIGH"
    },
    {
      "indicatorId": 67,
      "indicatorName": "System Uptime",
      "projectId": 12,
      "projectName": "Infrastructure Upgrade",
      "target": 99.5,
      "actual": 96.8,
      "variance": -2.7,
      "status": "AT_RISK",
      "riskLevel": "MEDIUM"
    }
  ]
}
```

#### Example
```
GET /analytics/portfolio/indicators-at-risk?planYear=2025&quarter=3
```

---

### 4. Budget Consumption
**GET** `/budget-consumption`

Returns current budget consumption metrics.

#### Query Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `planYear` | Integer | No | Annual plan year |
| `initiativeIds` | String | No | CSV list of initiative IDs |
| `projectIds` | String | No | CSV list of project IDs |
| `quarter` | Integer | No | Quarter number 1-4 |

#### Response Example
```json
{
  "totalBudget": 10000000.00,
  "consumedBudget": 6250000.00,
  "remainingBudget": 3750000.00,
  "consumptionRate": 62.5,
  "projectedConsumption": 95.0,
  "status": "ON_TRACK",
  "breakdown": {
    "initiatives": 4500000.00,
    "projects": 1750000.00
  },
  "monthlyBurn": 520833.33
}
```

#### Example
```
GET /analytics/portfolio/budget-consumption?planYear=2025&quarter=2
```

---

### 5. Upcoming Deadlines
**GET** `/upcoming-deadlines`

Returns list of upcoming deadlines for projects and initiatives.

#### Query Parameters
| Parameter | Type | Required | Description | Default |
|-----------|------|----------|-------------|---------|
| `planYear` | Integer | No | Annual plan year | Current year |
| `initiativeIds` | String | No | CSV list of initiative IDs | All |
| `projectIds` | String | No | CSV list of project IDs | All |
| `quarter` | Integer | No | Quarter number 1-4 | Current quarter |
| `limit` | Integer | No | Maximum number of results | 10 |

#### Response Example
```json
{
  "totalDeadlines": 25,
  "upcomingDeadlines": [
    {
      "entityId": 15,
      "entityName": "Digital Transformation Phase 2",
      "entityType": "PROJECT",
      "deadlineDate": "2025-11-15",
      "daysUntilDeadline": 19,
      "status": "ON_TRACK",
      "progress": 78.5,
      "priority": "HIGH"
    },
    {
      "entityId": 8,
      "entityName": "Customer Experience Initiative",
      "entityType": "INITIATIVE",
      "deadlineDate": "2025-11-30",
      "daysUntilDeadline": 34,
      "status": "AT_RISK",
      "progress": 52.0,
      "priority": "CRITICAL"
    }
  ]
}
```

#### Example
```
GET /analytics/portfolio/upcoming-deadlines?planYear=2025&limit=15
GET /analytics/portfolio/upcoming-deadlines?quarter=4&limit=20
```

---

## Visualization Endpoints

### 6. Progress Distribution (Donut Chart)
**GET** `/progress-distribution`

Distribution of projects/initiatives by progress status for donut chart visualization.

**Visualization**: Donut chart with color-coded segments

**Status Categories**:
- **ON_TRACK**: ≥ 75% progress (green/teal segment)
- **DELAYED**: 50-75% progress (orange segment)
- **CRITICAL**: < 50% progress (red segment)

#### Query Parameters
| Parameter | Type | Required | Description | Default |
|-----------|------|----------|-------------|---------|
| `planYear` | Integer | No | Annual plan year | Current year |
| `initiativeIds` | String | No | CSV list of initiative IDs | All |
| `projectIds` | String | No | CSV list of project IDs | All |
| `includeProjects` | Boolean | No | Include projects in results | true |
| `includeInitiatives` | Boolean | No | Include initiatives in results | true |

#### Response Example
```json
{
  "totalItems": 25,
  "distribution": {
    "onTrack": 15,
    "delayed": 7,
    "critical": 3
  },
  "percentages": {
    "onTrack": 60.0,
    "delayed": 28.0,
    "critical": 12.0
  }
}
```

#### Example
```
GET /analytics/portfolio/progress-distribution?planYear=2025
GET /analytics/portfolio/progress-distribution?planYear=2025&includeProjects=true&includeInitiatives=false
```

---

### 7. Budget by Project (Stacked Bar Chart)
**GET** `/budget-by-project`

Budget allocation and utilization by project for stacked bar chart visualization.

**Visualization**: Stacked bar chart
- Light teal segment: Planned budget
- Coral segment: Consumed budget

#### Query Parameters
| Parameter | Type | Required | Description | Default |
|-----------|------|----------|-------------|---------|
| `planYear` | Integer | No | Annual plan year | Current year |
| `initiativeIds` | String | No | CSV list of initiative IDs | All |
| `projectIds` | String | No | CSV list of project IDs | All |
| `includeProjects` | Boolean | No | Include projects | true |
| `includeInitiatives` | Boolean | No | Include initiatives | true |

#### Response Example
```json
{
  "items": [
    {
      "entityId": 123,
      "entityName": "Digital Transformation",
      "entityType": "PROJECT",
      "plannedBudget": 1000000.00,
      "consumedBudget": 750000.00,
      "utilizationPercent": 75.0
    }
  ],
  "totalPlanned": 5000000.00,
  "totalConsumed": 3500000.00
}
```

#### Example
```
GET /analytics/portfolio/budget-by-project?planYear=2025
GET /analytics/portfolio/budget-by-project?planYear=2025&includeProjects=true&includeInitiatives=false
```

---

### 8. Budget Utilization vs Achievement (Bubble Chart)
**GET** `/budget-utilization-vs-achievement`

Relationship between budget consumption and achievement progress.

**Visualization**: Bubble chart
- X-axis: Budget utilization %
- Y-axis: Achievement %
- Bubble size: Total budget amount

#### Query Parameters
| Parameter | Type | Required | Description | Default |
|-----------|------|----------|-------------|---------|
| `planYear` | Integer | No | Annual plan year | Current year |
| `initiativeIds` | String | No | CSV list of initiative IDs | All |
| `projectIds` | String | No | CSV list of project IDs | All |
| `includeProjects` | Boolean | No | Include projects | true |
| `includeInitiatives` | Boolean | No | Include initiatives | true |

#### Response Example
```json
{
  "items": [
    {
      "entityId": 123,
      "entityName": "Digital Platform",
      "entityType": "PROJECT",
      "budgetUtilization": 75.5,
      "achievement": 82.0,
      "totalBudget": 1500000.00,
      "efficiency": 108.6
    }
  ]
}
```

#### Example
```
GET /analytics/portfolio/budget-utilization-vs-achievement?planYear=2025
GET /analytics/portfolio/budget-utilization-vs-achievement?planYear=2025&includeProjects=true
```

---

### 9. Indicators by Initiatives (Stacked Bar Chart)
**GET** `/indicators-by-initiatives`

Indicator performance across initiatives for stacked bar chart visualization.

**Visualization**: Stacked bar chart showing achievement status distribution per initiative
- Each bar: One initiative
- Colored segments: Achieved, partial, lagging indicators

#### Query Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `planYear` | Integer | No | Annual plan year (defaults to current year) |
| `initiativeIds` | String | No | CSV list of initiative IDs to filter |

#### Response Example
```json
{
  "initiatives": [
    {
      "initiativeId": 5,
      "initiativeName": "Digital Transformation",
      "achieved": 8,
      "partial": 3,
      "lagging": 2,
      "total": 13
    }
  ]
}
```

#### Example
```
GET /analytics/portfolio/indicators-by-initiatives?planYear=2025
GET /analytics/portfolio/indicators-by-initiatives?planYear=2025&initiativeIds=1,5,8
```

---

## Trend & Analysis Endpoints

### 10. Progress Overview (Quarterly Snapshot)
**GET** `/progress-overview`

Quarterly progress snapshot showing current progress vs target.

#### Query Parameters
| Parameter | Type | Required | Description | Default |
|-----------|------|----------|-------------|---------|
| `planYear` | Integer | No | Annual plan year | Current year |
| `quarter` | Integer | No | Quarter number (1-4) | Current quarter |

#### Response Example
```json
{
  "currentProgress": 48.5,
  "quarterlyTarget": 50.0,
  "quarter": 2,
  "planYear": 2025,
  "totalInitiatives": 15,
  "totalProjects": 4,
  "totalIndicators": 30,
  "progressStatus": "ON_TRACK"
}
```

#### Response Fields
- `currentProgress`: Actual progress % for the quarter (0-100)
- `quarterlyTarget`: Expected target (Q1: 25%, Q2: 50%, Q3: 75%, Q4: 100%)
- `progressStatus`: 
  - `AHEAD`: Progress > target
  - `ON_TRACK`: Progress ≥ (target - 5%)
  - `BEHIND`: Progress < (target - 5%)

#### Example
```
GET /analytics/portfolio/progress-overview
GET /analytics/portfolio/progress-overview?planYear=2025&quarter=3
```

---

### 11. Progress Trend (Multi-Year Comparison)
**GET** `/progress-trend`

Comparative progress across multiple years over time (monthly or quarterly).

#### Query Parameters
| Parameter | Type | Required | Description | Default |
|-----------|------|----------|-------------|---------|
| `planYears` | String | No | CSV list of years to compare (e.g., "2024,2025") | Current year |
| `timeUnit` | String | No | "MONTHLY" or "QUARTERLY" | MONTHLY |
| `startPeriod` | Integer | No | Start month (1-12) or quarter (1-4) | 1 |
| `endPeriod` | Integer | No | End month (1-12) or quarter (1-4) | 12 or 4 |

#### Response Example (Monthly)
```json
{
  "timeUnit": "MONTHLY",
  "series": [
    {
      "year": 2025,
      "data": [
        {"period": 1, "label": "Jan", "value": 10.5},
        {"period": 2, "label": "Feb", "value": 18.3}
      ]
    }
  ]
}
```

#### Example
```
GET /analytics/portfolio/progress-trend?planYears=2024,2025&timeUnit=MONTHLY
GET /analytics/portfolio/progress-trend?planYears=2025&timeUnit=QUARTERLY&startPeriod=1&endPeriod=3
```

---

### 12. Project Achievement Trend
**GET** `/project-achievement-trend`

Project achievement trends over time.

#### Query Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `planYear` | Integer | No | Annual plan year |
| `initiativeIds` | String | No | CSV list of initiative IDs |
| `projectIds` | String | No | CSV list of project IDs |
| `startMonth` | Integer | No | Start month (1-12) |
| `endMonth` | Integer | No | End month (1-12) |

#### Response Example
```json
{
  "planYear": 2025,
  "startMonth": 1,
  "endMonth": 6,
  "trend": [
    {
      "month": 1,
      "label": "Jan",
      "averageAchievement": 15.5,
      "projectCount": 42
    },
    {
      "month": 2,
      "label": "Feb",
      "averageAchievement": 28.3,
      "projectCount": 42
    },
    {
      "month": 3,
      "label": "Mar",
      "averageAchievement": 42.8,
      "projectCount": 45
    }
  ]
}
```

#### Example
```
GET /analytics/portfolio/project-achievement-trend?planYear=2025&startMonth=1&endMonth=6
```

---

### 13. Budget Consumption Trend
**GET** `/budget-consumption-trend`

Budget consumption trends over time.

#### Query Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `planYear` | Integer | No | Annual plan year |
| `initiativeIds` | String | No | CSV list of initiative IDs |
| `projectIds` | String | No | CSV list of project IDs |
| `startMonth` | Integer | No | Start month (1-12) |
| `endMonth` | Integer | No | End month (1-12) |

#### Response Example
```json
{
  "planYear": 2025,
  "startMonth": 1,
  "endMonth": 6,
  "totalBudget": 10000000.00,
  "trend": [
    {
      "month": 1,
      "label": "Jan",
      "consumed": 520000.00,
      "cumulativeConsumed": 520000.00,
      "consumptionRate": 5.2,
      "planned": 500000.00
    },
    {
      "month": 2,
      "label": "Feb",
      "consumed": 580000.00,
      "cumulativeConsumed": 1100000.00,
      "consumptionRate": 11.0,
      "planned": 1000000.00
    }
  ]
}
```

#### Example
```
GET /analytics/portfolio/budget-consumption-trend?planYear=2025
GET /analytics/portfolio/budget-consumption-trend?planYear=2025&startMonth=1&endMonth=6
```

---

## KPI Performance Endpoints

### 14. KPI Performance Dashboard
**GET** `/kpi-dashboard`

Q3 snapshot of KPI performance with baseline, targets, actuals, and status.

#### Query Parameters
| Parameter | Type | Required | Description | Default |
|-----------|------|----------|-------------|---------|
| `planYear` | Integer | No | Annual plan year | Current year |
| `quarter` | Integer | No | Quarter number (1-4) | Current quarter |
| `initiativeIds` | String | No | CSV list of initiative IDs | All |
| `sortBy` | String | No | "TOP_PERFORMING" or "LOWEST_PERFORMING" | TOP_PERFORMING |

#### Response Example
```json
{
  "summary": {
    "totalKpis": 30,
    "onTrackCount": 20,
    "atRiskCount": 7,
    "offTrackCount": 3,
    "onTrackPercent": 66.7,
    "atRiskPercent": 23.3,
    "offTrackPercent": 10.0,
    "growthPercent": 5.2
  },
  "kpis": [
    {
      "indicatorId": 101,
      "indicatorName": "Customer Satisfaction",
      "baseline": 75.0,
      "annualTarget": 90.0,
      "quarterlyTarget": 82.5,
      "quarterlyActual": 85.0,
      "variancePercent": 3.0,
      "status": "ON_TRACK"
    }
  ]
}
```

#### Status Determination
- **ON_TRACK**: ≥ 95% achievement (actual/target)
- **AT_RISK**: 80-95% achievement
- **OFF_TRACK**: < 80% achievement

#### Example
```
GET /analytics/portfolio/kpi-dashboard?planYear=2025&quarter=3
GET /analytics/portfolio/kpi-dashboard?planYear=2025&quarter=3&sortBy=LOWEST_PERFORMING
GET /analytics/portfolio/kpi-dashboard?quarter=3&initiativeIds=1,5,8

---

## Common Response Codes

| Code | Description |
|------|-------------|
| 200 | Success |
| 400 | Bad Request - Invalid parameters |
| 401 | Unauthorized - Missing or invalid authentication |
| 403 | Forbidden - Insufficient permissions |
| 404 | Not Found - Resource not found |
| 500 | Internal Server Error |

---

## Authentication

All endpoints require authentication via JWT token in the Authorization header:

```
```

---

## Common Response Codes

| Code | Description |
|------|-------------|
| 200 | Success |
| 400 | Bad Request - Invalid parameters |
| 401 | Unauthorized - Missing or invalid authentication |
| 403 | Forbidden - Insufficient permissions |
| 500 | Internal Server Error |

---

## Authentication

All endpoints require authentication via JWT token in the Authorization header:

```
Authorization: Bearer <your-jwt-token>
```

The tenant schema is automatically determined from the JWT token's `user_schema` claim.

---

## Common Query Parameters

Most endpoints support these common filters:

| Parameter | Type | Format | Description |
|-----------|------|--------|-------------|
| `planYear` | Integer | 2025 | Filter by annual plan year |
| `quarter` | Integer | 1-4 | Filter by quarter |
| `initiativeIds` | String | "1,2,3" | CSV list of initiative IDs |
| `projectIds` | String | "10,20,30" | CSV list of project IDs |

---

## Quick Reference

| Endpoint | Primary Use | Visualization |
|----------|-------------|---------------|
| `/dashboard` | Main dashboard overview | Mixed |
| `/overall-health` | Portfolio health metrics | Cards/Metrics |
| `/indicators-at-risk` | Risk management | List/Table |
| `/budget-consumption` | Budget monitoring | Cards/Metrics |
| `/upcoming-deadlines` | Timeline management | List/Timeline |
| `/progress-overview` | Quarterly snapshot | Cards with comparison |
| `/progress-trend` | Multi-year comparison | Line chart |
| `/project-achievement-trend` | Project progress over time | Line chart |
| `/budget-consumption-trend` | Budget tracking over time | Line/Area chart |
| `/progress-distribution` | Status breakdown | Donut chart |
| `/budget-by-project` | Budget allocation & usage | Stacked bar chart |
| `/budget-utilization-vs-achievement` | Efficiency analysis | Bubble chart |
| `/indicators-by-initiatives` | KPI distribution | Stacked bar chart |
| `/kpi-dashboard` | KPI performance tracking | Table/Cards |

---

## Notes for Front-End Developers

### Multi-Tenancy
All queries automatically use the correct tenant schema based on the JWT token. No need to pass tenant information explicitly.

### Data Filtering
- Use CSV format for multiple IDs: `initiativeIds=1,2,3` or `projectIds=10,20,30`
- Filters are optional and can be combined
- Empty filters return all data for the specified year/quarter

### Progress Calculation
- Progress values are percentages (0-100)
- For quarterly overview, progress is time-based and reflects what should have been achieved by the end of that quarter
- Null progress values are treated as 0

### Date Handling
- All dates are in ISO-8601 format
- Quarter calculation: Q1 (Jan-Mar), Q2 (Apr-Jun), Q3 (Jul-Sep), Q4 (Oct-Dec)
- Month numbers: 1-12
- Quarter numbers: 1-4

### Default Values
- `planYear`: Defaults to current year if not provided
- `quarter`: Defaults to current quarter based on system date
- `timeUnit`: Defaults to "MONTHLY"
- `sortBy`: Defaults to "TOP_PERFORMING"
- Boolean flags (includeProjects, includeInitiatives): Default to `true`

### Performance Considerations
- Results are computed in real-time from the database
- Large date ranges may take longer to process
- Consider implementing client-side caching where appropriate
- Use specific filters to reduce data volume

### Error Handling
- Always check the HTTP status code
- Error responses include a message field with details
- Handle 404s gracefully (e.g., when no data exists for a given year)
- Empty result sets return valid JSON with empty arrays/zero counts

---

## Change Log

### Version 1.0
- Initial API documentation
- 14 endpoints covering dashboard, visualizations, trends, and KPI performance
- Support for multi-tenant architecture
- Flexible filtering by year, quarter, initiatives, and projects
```

The tenant schema is automatically determined from the JWT token's `user_schema` claim.

---

## Examples

### Example 1: Get Progress Distribution
```bash
GET /analytics/portfolio/progress-distribution?planYear=2025
```

### Example 2: Get Monthly Progress Trend
```bash
GET /analytics/portfolio/progress-trend?planYear=2025&period=MONTHLY
```

### Example 3: Get Quarterly Progress Trend for Specific Initiative
```bash
GET /analytics/portfolio/progress-trend?planYear=2025&period=QUARTERLY&initiativeId=123
```

### Example 4: Get Budget Allocation
```bash
GET /analytics/portfolio/budget-allocation-by-project?planYear=2025
```

### Example 5: Get Progress Overview for Q2 2025
```bash
GET /analytics/portfolio/progress-overview?planYear=2025&quarter=2
```

### Example 6: Get Progress Overview for Current Quarter
```bash
GET /analytics/portfolio/progress-overview
```

---

## Notes for Front-End Developers

1. **Multi-Tenancy**: All queries automatically use the correct tenant schema based on the JWT token. No need to pass tenant information.

2. **Progress Calculation**: 
   - Progress values are percentages (0-100)
   - For quarterly overview, progress is time-based and reflects what should have been achieved by the end of that quarter
   - Null progress values are treated as 0

3. **Filtering**: 
   - You can filter by `initiativeId` or `projectId` on most endpoints
   - Filters are optional and can be combined

4. **Date Handling**: 
   - All dates are in ISO-8601 format
   - Quarter calculation: Q1 (Jan-Mar), Q2 (Apr-Jun), Q3 (Jul-Sep), Q4 (Oct-Dec)

5. **Performance**: 
   - Results are computed in real-time from the database
   - Large date ranges may take longer to process
   - Consider implementing client-side caching where appropriate

6. **Error Handling**: 
   - Always check the HTTP status code
   - Error responses include a message field with details
   - Handle 404s gracefully (e.g., when no data exists for a given year)
