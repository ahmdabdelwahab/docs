# Portfolio Analytics - API Endpoints

## Base URL
```
/analytics/portfolio
```

---

## 1. Get Complete Dashboard

**Endpoint:** `GET /analytics/portfolio/dashboard`

**Parameters:**
- `planYear` (optional): Integer - Annual plan year (default: current year)
- `initiativeIds` (optional): String - Comma-separated initiative IDs (e.g., "1,2,3")
- `projectIds` (optional): String - Comma-separated project IDs (e.g., "16,23,49")
- `quarter` (optional): Integer - Quarter 1-4 (default: cumulative)

**Request Example:**
```http
GET /analytics/portfolio/dashboard?planYear=2025&quarter=2
GET /analytics/portfolio/dashboard?planYear=2025&initiativeIds=1,2,3
GET /analytics/portfolio/dashboard?planYear=2025&projectIds=16,23,49&quarter=1
```

**Response:**
```json
{
  "overallHealth": {
    "overallHealthScore": 75.5,
    "healthStatus": "HEALTHY",
    "progressScore": 68.2,
    "budgetScore": 85.0,
    "indicatorsScore": 72.5,
    "healthSegments": {
      "criticalPercentage": 10.0,
      "watchPercentage": 25.0,
      "healthyPercentage": 65.0
    },
    "totalPrograms": 5,
    "totalInitiatives": 12,
    "totalProjects": 48
  },
  "indicatorsAtRisk": { /* See below */ },
  "budgetConsumption": { /* See below */ },
  "upcomingDeadlines": { /* See below */ },
  "planYear": 2025,
  "quarter": 2
}
```

---

## 2. Get Overall Health

**Endpoint:** `GET /analytics/portfolio/overall-health`

**Parameters:**
- `planYear` (optional): Integer - Annual plan year (default: current year)
- `initiativeIds` (optional): String - Comma-separated initiative IDs
- `projectIds` (optional): String - Comma-separated project IDs
- `quarter` (optional): Integer - Quarter 1-4

**Request Example:**
```http
GET /analytics/portfolio/overall-health?planYear=2025
GET /analytics/portfolio/overall-health?planYear=2025&initiativeIds=5,7&quarter=3
```

**Response:**
```json
{
  "overallHealthScore": 75.5,
  "healthStatus": "HEALTHY",
  "progressScore": 68.2,
  "budgetScore": 85.0,
  "indicatorsScore": 72.5,
  "healthSegments": {
    "criticalPercentage": 10.0,
    "watchPercentage": 25.0,
    "healthyPercentage": 65.0
  },
  "totalPrograms": 5,
  "totalInitiatives": 12,
  "totalProjects": 48
}
```

---

## 3. Get Indicators At Risk

**Endpoint:** `GET /analytics/portfolio/indicators-at-risk`

**Parameters:**
- `planYear` (optional): Integer - Annual plan year (default: current year)
- `initiativeIds` (optional): String - Comma-separated initiative IDs
- `projectIds` (optional): String - Comma-separated project IDs
- `quarter` (optional): Integer - Quarter 1-4

**Request Example:**
```http
GET /analytics/portfolio/indicators-at-risk?planYear=2025
GET /analytics/portfolio/indicators-at-risk?planYear=2025&projectIds=16,23,49
```

**Response:**
```json
{
  "riskLevel": "15 - 31%",
  "totalIndicators": 48,
  "totalAtRisk": 15,
  "totalPrograms": 5,
  "onTrackCount": 33,
  "atRiskCount": 10,
  "offTrackCount": 5,
  "changeVsLastQuarter": 3,
  "trendDirection": "UP",
  "onTrackPercentage": 68.75,
  "atRiskPercentage": 20.83,
  "offTrackPercentage": 10.42
}
```

---

## 4. Get Budget Consumption

**Endpoint:** `GET /analytics/portfolio/budget-consumption`

**Parameters:**
- `planYear` (optional): Integer - Annual plan year (default: current year)
- `initiativeIds` (optional): String - Comma-separated initiative IDs
- `projectIds` (optional): String - Comma-separated project IDs
- `quarter` (optional): Integer - Quarter 1-4

**Request Example:**
```http
GET /analytics/portfolio/budget-consumption?planYear=2025
GET /analytics/portfolio/budget-consumption?planYear=2025&initiativeIds=1,2&quarter=2
```

**Response:**
```json
{
  "totalBudget": 15000000.00,
  "spentAmount": 8750000.00,
  "remainingAmount": 6250000.00,
  "consumptionRate": 58.33,
  "progressRate": 62.50,
  "spendVsProgressGap": -4.17,
  "budgetStatus": "ON_TRACK",
  "monthlyBurnRate": 875000.00,
  "projectedDaysToDepletion": 214
}
```

---

## 5. Get Upcoming Deadlines

**Endpoint:** `GET /analytics/portfolio/upcoming-deadlines`

**Parameters:**
- `planYear` (optional): Integer - Annual plan year (default: current year)
- `initiativeIds` (optional): String - Comma-separated initiative IDs
- `projectIds` (optional): String - Comma-separated project IDs
- `quarter` (optional): Integer - Quarter 1-4
- `limit` (optional): Integer - Max results (default: 10)

**Request Example:**
```http
GET /analytics/portfolio/upcoming-deadlines?planYear=2025&limit=5
GET /analytics/portfolio/upcoming-deadlines?planYear=2025&projectIds=16,23&limit=20
```

**Response:**
```json
{
  "deadlines": [
    {
      "id": 159,
      "itemType": "PROJECT",
      "nameTranslations": {
        "en": "Unified Smart Government Platform",
        "ar": "المنصة الموحدة للحكومة الذكية"
      },
      "dueDate": "2025-11-15",
      "daysRemaining": 20,
      "progressPercent": 45.0,
      "projectId": 159,
      "initiativeId": 12,
      "initiativeNameTranslations": {
        "en": "Digital Transformation",
        "ar": "التحول الرقمي"
      },
      "urgencyStatus": "WARNING",
      "statusColor": "ORANGE"
    }
  ],
  "totalUpcoming": 5,
  "criticalCount": 2,
  "warningCount": 3,
  "healthyCount": 0
}
```

---

## 6. Get Project Achievement Trend

**Endpoint:** `GET /analytics/portfolio/project-achievement-trend`

**Parameters:**
- `planYear` (optional): Integer - Annual plan year (default: current year)
- `initiativeIds` (optional): String - Comma-separated initiative IDs
- `projectIds` (optional): String - Comma-separated project IDs
- `startMonth` (optional): Integer 1-12 (default: 1)
- `endMonth` (optional): Integer 1-12 (default: current month)

**Request Example:**
```http
GET /analytics/portfolio/project-achievement-trend?planYear=2025&startMonth=1&endMonth=6
GET /analytics/portfolio/project-achievement-trend?planYear=2025&projectIds=16,23,49&startMonth=3&endMonth=9
```

**Response:**
```json
{
  "projects": [
    {
      "projectId": 16,
      "nameTranslations": {
        "en": "AI Digital Assistant",
        "ar": "المساعد الرقمي الذكي"
      },
      "color": "#10b981",
      "monthlyData": [
        {
          "month": 1,
          "monthLabel": "Jan",
          "achievementPercent": 10.5,
          "status": "CRITICAL"
        },
        {
          "month": 2,
          "monthLabel": "Feb",
          "achievementPercent": 22.3,
          "status": "AT_RISK"
        },
        {
          "month": 3,
          "monthLabel": "Mar",
          "achievementPercent": 38.7,
          "status": "AT_RISK"
        }
      ],
      "startProgress": 10.5,
      "endProgress": 65.8,
      "averageProgress": 42.3,
      "trend": "IMPROVING"
    }
  ],
  "timeLabels": ["Jan", "Feb", "Mar", "Apr", "May", "Jun"],
  "planYear": 2025,
  "startMonth": 1,
  "endMonth": 6
}
```

---

## 7. Get Budget Consumption Trend

**Endpoint:** `GET /analytics/portfolio/budget-consumption-trend`

**Parameters:**
- `planYear` (optional): Integer - Annual plan year (default: current year)
- `initiativeIds` (optional): String - Comma-separated initiative IDs
- `projectIds` (optional): String - Comma-separated project IDs
- `startMonth` (optional): Integer 1-12 (default: 1)
- `endMonth` (optional): Integer 1-12 (default: current month)

**Request Example:**
```http
GET /analytics/portfolio/budget-consumption-trend?planYear=2025&startMonth=1&endMonth=6
GET /analytics/portfolio/budget-consumption-trend?planYear=2025&initiativeIds=5,7&startMonth=1&endMonth=10
```

**Response:**
```json
{
  "months": [
    {
      "month": 1,
      "monthLabel": "Jan",
      "cumulativeActual": 875000.00,
      "cumulativeForecast": 1250000.00,
      "actualPercent": 5.83,
      "forecastPercent": 8.33,
      "variance": -2.50,
      "varianceStatus": "FAVORABLE"
    },
    {
      "month": 2,
      "monthLabel": "Feb",
      "cumulativeActual": 1750000.00,
      "cumulativeForecast": 2500000.00,
      "actualPercent": 11.67,
      "forecastPercent": 16.67,
      "variance": -5.00,
      "varianceStatus": "FAVORABLE"
    }
  ],
  "totalBudget": 15000000.00,
  "finalActualPercent": 58.33,
  "finalForecastPercent": 83.33,
  "overallVariance": -25.00,
  "projectionStatus": "UNDER_BUDGET"
}
```

---

## Quick Reference

| Endpoint | Method | Key Response |
|----------|--------|--------------|
| `/dashboard` | GET | Complete portfolio overview |
| `/overall-health` | GET | Health score & segments |
| `/indicators-at-risk` | GET | KPI performance analysis |
| `/budget-consumption` | GET | Budget utilization metrics |
| `/upcoming-deadlines` | GET | Critical deadlines list |
| `/project-achievement-trend` | GET | Monthly progress trends |
| `/budget-consumption-trend` | GET | Budget burn rate trends |

---

## Common Parameters

All endpoints support these filters:

| Parameter | Type | Required | Default | Description | Example |
|-----------|------|----------|---------|-------------|---------|
| `planYear` | Integer | No | Current year | Annual plan year to analyze | `2025` |
| `initiativeIds` | String (CSV) | No | All initiatives | Filter by specific initiatives | `"1,2,3"` |
| `projectIds` | String (CSV) | No | All projects | Filter by specific projects | `"16,23,49"` |
| `quarter` | Integer | No | Cumulative | Quarter 1-4 for time-specific view | `2` |

**Trend-specific parameters:**

| Parameter | Type | Required | Default | Description | Example |
|-----------|------|----------|---------|-------------|---------|
| `startMonth` | Integer | No | 1 | Start month for trend analysis (1-12) | `3` |
| `endMonth` | Integer | No | Current month | End month for trend analysis (1-12) | `9` |
| `limit` | Integer | No | 10 | Max results for deadlines endpoint | `20` |

---

## Parameter Examples

### Filter by Initiative
```http
GET /analytics/portfolio/overall-health?planYear=2025&initiativeIds=1,2,3
```

### Filter by Projects
```http
GET /analytics/portfolio/budget-consumption?planYear=2025&projectIds=16,23,49
```

### Quarterly Analysis
```http
GET /analytics/portfolio/indicators-at-risk?planYear=2025&quarter=2
```

### Combine Filters
```http
GET /analytics/portfolio/dashboard?planYear=2025&initiativeIds=5,7&quarter=3
GET /analytics/portfolio/project-achievement-trend?planYear=2025&projectIds=16,23&startMonth=1&endMonth=6
```

### All Projects (No Filter)
```http
GET /analytics/portfolio/overall-health?planYear=2025
```

---

## Status Enums

**Health Status:**
- `HEALTHY` - Score ≥ 75%
- `WATCH` - Score 60-74%
- `CRITICAL` - Score < 60%

**Budget Status:**
- `ON_TRACK` - Gap ≤ 5%
- `AT_RISK` - Gap 6-15%
- `OVERRUN` - Gap > 15%

**Trend Direction:**
- `UP` - Worsening (more at risk)
- `DOWN` - Improving (fewer at risk)
- `STABLE` - No significant change

**Urgency Status:**
- `CRITICAL` - Due ≤ 7 days (RED)
- `WARNING` - Due 8-30 days (ORANGE)
- `HEALTHY` - Due > 30 days (GREEN)

**Variance Status:**
- `FAVORABLE` - Under budget (variance < -5%)
- `ON_TARGET` - Within ±5% of forecast
- `UNFAVORABLE` - Over budget (variance > 5%)

**Projection Status:**
- `UNDER_BUDGET` - Overall spending below forecast
- `ON_BUDGET` - Spending aligned with forecast
- `OVER_BUDGET` - Overall spending exceeds forecast
