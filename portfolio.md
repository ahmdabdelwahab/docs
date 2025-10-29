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

### Endpoint
```
GET /analytics/portfolio/project-achievement-trend
```

### Description
Displays achievement progress trends over time for projects or initiatives. Shows monthly progress percentages with trend lines to visualize performance trajectory.

### Query Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `planYear` | Integer | No | Current year | Filter by annual plan year |
| `initiativeIds` | String (CSV) | No | null | Optional comma-separated list of initiative IDs to filter |
| `projectIds` | String (CSV) | No | null | Optional comma-separated list of project IDs to filter |
| `startMonth` | Integer | No | 1 | Start month (1-12) for the trend period |
| `endMonth` | Integer | No | Current month | End month (1-12) for the trend period |
| `entityType` | String | No | `PROJECTS` | Toggle between entity types: `PROJECTS` or `INITIATIVES` |

### Example Requests

**View project achievement trends for 2025:**
```
GET /analytics/portfolio/project-achievement-trend?planYear=2025&entityType=PROJECTS
```

**View initiatives achievement trends from January to June:**
```
GET /analytics/portfolio/project-achievement-trend?planYear=2025&startMonth=1&endMonth=6&entityType=INITIATIVES
```

**View specific projects:**
```
GET /analytics/portfolio/project-achievement-trend?planYear=2025&projectIds=123,456,789&entityType=PROJECTS
```

### Response Structure
```json
{
  "planYear": 2025,
  "startMonth": 1,
  "endMonth": 6,
  "entityType": "PROJECTS",
  "series": [
    {
      "entityId": 123,
      "entityName": "Digital Transformation Project",
      "dataPoints": [
        {
          "month": 1,
          "monthName": "January",
          "achievementPercent": 15.5
        },
        {
          "month": 2,
          "monthName": "February",
          "achievementPercent": 28.3
        }
      ]
    }
  ],
  "totalEntities": 4
}
```

### Use Case
- Track project/initiative progress over time
- Identify trends and patterns in achievement
- Compare multiple projects side-by-side
- Monitor if projects are accelerating or decelerating
- Generate monthly progress reports

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

## KPI Performance endpoint

### Endpoint
```
GET /analytics/portfolio/kpi-dashboard
```

### Description
Comprehensive KPI/Indicator tracking dashboard showing quarterly performance snapshot with baseline values, annual targets, quarterly targets, actual values, variance percentages, and status indicators.

### Query Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `planYear` | Integer | No | Current year | Filter by annual plan year |
| `quarter` | Integer | No | Current quarter | Quarter number (1-4) for performance snapshot |
| `initiativeIds` | String (CSV) | No | null | Optional comma-separated list of initiative IDs to filter |
| `sortBy` | String | No | `TOP_PERFORMING` | Sort order: `TOP_PERFORMING` or `LOWEST_PERFORMING` |
| `page` | Integer | No | 1 | Page number for pagination |
| `size` | Integer | No | 10 | Number of KPIs per page |

### Example Requests

**View Q3 2025 KPI dashboard with top performers:**
```
GET /analytics/portfolio/kpi-dashboard?planYear=2025&quarter=3&sortBy=TOP_PERFORMING
```

**View lowest performing KPIs for specific initiatives:**
```
GET /analytics/portfolio/kpi-dashboard?planYear=2025&quarter=3&initiativeIds=45,67,89&sortBy=LOWEST_PERFORMING
```

**Paginated results (page 2, 20 items per page):**
```
GET /analytics/portfolio/kpi-dashboard?planYear=2025&quarter=3&page=2&size=20
```

### Response Structure
```json
{
  "planYear": 2025,
  "quarter": 3,
  "summary": {
    "totalKpis": 30,
    "onTrackCount": 22,
    "onTrackPercent": 73.3,
    "atRiskCount": 5,
    "atRiskPercent": 16.7,
    "offTrackCount": 3,
    "offTrackPercent": 10.0,
    "growthPercent": 12.5
  },
  "kpis": [
    {
      "kpiId": 101,
      "kpiName": "Customer Satisfaction Score",
      "initiativeName": "Service Excellence Program",
      "baseline": 75.0,
      "annualTarget": 90.0,
      "quarterlyTarget": 85.0,
      "quarterlyActual": 87.5,
      "variancePercent": 2.94,
      "status": "ON_TRACK",
      "unit": "%"
    },
    {
      "kpiId": 102,
      "kpiName": "Process Automation Rate",
      "initiativeName": "Digital Transformation",
      "baseline": 45.0,
      "annualTarget": 80.0,
      "quarterlyTarget": 70.0,
      "quarterlyActual": 65.0,
      "variancePercent": -7.14,
      "status": "AT_RISK",
      "unit": "%"
    }
  ],
  "pagination": {
    "currentPage": 1,
    "totalPages": 3,
    "pageSize": 10,
    "totalItems": 30
  }
}
```
