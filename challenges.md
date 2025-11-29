# Challenge Analytics API Documentation

## Overview
RESTful API for Innovation Challenge analytics dashboard. Provides 13 endpoints for comprehensive challenge metrics, trends, and drill-down capabilities.

**Base URL:** `/analytics/challenge`

---

## Endpoints

### 1. Active Challenges
**GET** `/active-challenges`

Returns count of active challenges with urgency breakdown.

**Query Parameters:**
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| page | Integer | 1 | Page number |
| size | Integer | 10 | Items per page |
| urgency | String | null | Filter by urgency (CRITICAL, HIGH, MODERATE, LOW, VERY_LOW) |
| sortBy | String | created_at | Sort field: created_at, urgency |
| sortDir | String | DESC | Sort direction: ASC, DESC |

**Response:**
```json
{
  "summary": {
    "totalActiveChallenges": 156,
    "urgencyBreakdown": [
      {"urgency": "CRITICAL", "count": 12, "percentage": 7.69},
      {"urgency": "HIGH", "count": 45, "percentage": 28.85}
    ]
  },
  "details": {
    "items": [
      {
        "id": 101,
        "name": {"en": "AI Integration", "ar": "تكامل الذكاء الاصطناعي"},
        "description": {"en": "Integrate AI capabilities"},
        "urgency": "CRITICAL",
        "createdAt": "2025-11-15T10:30:00"
      }
    ],
    "pagination": {
      "currentPage": 1,
      "pageSize": 10,
      "totalPages": 16,
      "totalItems": 156
    }
  }
}
```

---

### 2. Review Status
**GET** `/review-status`

Returns challenge distribution by review status.

**Query Parameters:**
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| page | Integer | 1 | Page number |
| size | Integer | 10 | Items per page |
| status | String | null | Filter by status (PENDING_REVIEW, APPROVED, REJECTED, UNDER_REVIEW) |
| sortBy | String | created_at | Sort field |
| sortDir | String | DESC | Sort direction |

**Response:**
```json
{
  "summary": {
    "totalChallenges": 200,
    "statusBreakdown": [
      {"status": "PENDING_REVIEW", "count": 45, "percentage": 22.5},
      {"status": "APPROVED", "count": 120, "percentage": 60.0}
    ]
  },
  "details": {
    "items": [...],
    "pagination": {...}
  }
}
```

---

### 3. Top Innovators
**GET** `/top-innovators`

Returns most active contributors ranked by challenges and engagement.

**Query Parameters:**
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| page | Integer | 1 | Page number |
| size | Integer | 10 | Items per page |
| limit | Integer | 3 | Top N innovators in summary |
| sortBy | String | total_score | Sort field: total_score, challenges, engagements |
| sortDir | String | DESC | Sort direction |

**Response:**
```json
{
  "topInnovators": [
    {
      "rank": 1,
      "userId": 1523,
      "userName": "Ahmed Khalil",
      "challengesCreated": 28,
      "totalEngagements": 456,
      "totalScore": 484
    }
  ],
  "details": {
    "items": [...],
    "pagination": {...}
  }
}
```

---

### 4. Approval Rate
**GET** `/approval-rate`

Returns approval rate with quarter-over-quarter comparison.

**Query Parameters:**
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| page | Integer | 1 | Page number |
| size | Integer | 10 | Items per page |
| quarter | Integer | null | Filter by quarter (1-4) |
| year | Integer | null | Filter by year |
| sortBy | String | created_at | Sort field |
| sortDir | String | DESC | Sort direction |

**Response:**
```json
{
  "metrics": {
    "currentRate": 75.5,
    "previousRate": 68.2,
    "change": 7.3,
    "totalReviewed": 150,
    "approved": 113,
    "rejected": 37
  },
  "details": {
    "items": [...],
    "pagination": {...}
  }
}
```

---

### 5. Top Categories
**GET** `/top-categories`

Returns top categories by challenge count.

**Query Parameters:**
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| page | Integer | 1 | Page number |
| size | Integer | 10 | Items per page |
| limit | Integer | 3 | Top N categories in summary |
| categoryId | Long | null | Filter by category ID |
| sortBy | String | count | Sort field: count, name |
| sortDir | String | DESC | Sort direction |

**Response:**
```json
{
  "topCategories": [
    {
      "rank": 1,
      "category": {"en": "Automation", "ar": "الأتمتة"},
      "count": 45,
      "percentage": 22.5
    }
  ],
  "details": {
    "items": [...],
    "pagination": {...}
  }
}
```

---

### 6. Delayed Challenges
**GET** `/delayed-challenges`

Returns overdue challenges with days count.

**Query Parameters:**
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| page | Integer | 1 | Page number |
| size | Integer | 10 | Items per page |
| limit | Integer | 5 | Top N delayed in summary |
| minDaysOverdue | Integer | null | Minimum days overdue filter |
| urgency | String | null | Filter by urgency |
| sortBy | String | days_overdue | Sort field: days_overdue, urgency |
| sortDir | String | DESC | Sort direction |

**Response:**
```json
{
  "mostDelayed": [
    {
      "id": 234,
      "name": {"en": "Cloud Migration"},
      "daysOverdue": 45,
      "urgency": "CRITICAL",
      "dueDate": "2025-10-01"
    }
  ],
  "details": {
    "items": [...],
    "pagination": {...}
  }
}
```

---

### 7. Category Breakdown
**GET** `/category-breakdown`

Returns challenge distribution across categories.

**Query Parameters:**
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| page | Integer | 1 | Page number |
| size | Integer | 10 | Items per page |
| categoryId | Long | null | Filter by category ID |
| status | String | null | Filter by status |
| sortBy | String | name | Sort field: name, urgency, status, category |
| sortDir | String | ASC | Sort direction |

**Response:**
```json
{
  "metrics": {
    "totalChallenges": 200,
    "categories": [
      {
        "categoryId": 5,
        "categoryName": {"en": "Automation", "ar": "الأتمتة"},
        "count": 45,
        "percentage": 22.5
      }
    ]
  },
  "details": {
    "items": [
      {
        "id": 101,
        "name": {"en": "AI Integration"},
        "description": {"en": "Integrate AI capabilities"},
        "categoryId": 5,
        "category": {"en": "Automation"},
        "status": "ACTIVE",
        "urgency": "HIGH"
      }
    ],
    "pagination": {...}
  }
}
```

---

### 8. Scope Distribution
**GET** `/scope-distribution`

Returns challenge distribution across organizational scopes.

**Query Parameters:**
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| page | Integer | 1 | Page number |
| size | Integer | 10 | Items per page |
| scope | String | null | Filter by scope (DEPARTMENTAL, ORGANIZATIONAL, NATIONAL, GLOBAL) |
| status | String | null | Filter by status |
| sortBy | String | name | Sort field |
| sortDir | String | ASC | Sort direction |

**Response:**
```json
{
  "metrics": {
    "totalChallenges": 200,
    "scopes": [
      {
        "scopeName": "ORGANIZATIONAL",
        "count": 85,
        "percentage": 42.5
      }
    ]
  },
  "details": {
    "items": [...],
    "pagination": {...}
  }
}
```

---

### 9. Engagement Activity
**GET** `/engagement-activity`

Returns engagement metrics (views + comments + likes) with weekly trends.

**Query Parameters:**
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| startDate | Date | null | Start date (ISO format: YYYY-MM-DD) |
| endDate | Date | null | End date |
| categoryId | Long | null | Filter by category ID |
| minEngagements | Integer | null | Minimum engagement threshold |
| sortBy | String | totalEngagements | Sort field: totalEngagements, views, comments, likes |
| sortDir | String | DESC | Sort direction |
| page | Integer | 1 | Page number |
| size | Integer | 10 | Items per page |

**Response:**
```json
{
  "metrics": {
    "totalEngagements": 1250,
    "avgPerChallenge": 15.6,
    "mostEngagedCategory": {
      "category": {"en": "Automation", "ar": "الأتمتة"},
      "count": 450
    },
    "peakWeek": {
      "weekStart": "2025-10-13",
      "weekEnd": "2025-10-19",
      "count": 285
    }
  },
  "weeklyTrend": [
    {
      "weekStart": "2025-10-13",
      "weekEnd": "2025-10-19",
      "count": 285
    },
    {
      "weekStart": "2025-10-20",
      "weekEnd": "2025-10-26",
      "count": 198
    }
  ],
  "details": {
    "items": [
      {
        "id": 101,
        "name": {"en": "AI Integration"},
        "category": {"en": "Automation"},
        "views": 450,
        "comments": 28,
        "likes": 92,
        "totalEngagements": 570,
        "createdAt": "2025-10-15"
      }
    ],
    "pagination": {...}
  }
}
```

---

### 10. Pending Review by Age
**GET** `/pending-review-by-age`

Returns challenges pending review grouped by age ranges.

**Query Parameters:**
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| categoryId | Long | null | Filter by category ID |
| ageRange | String | null | Filter by range (0-15, 16-30, 31-60, 60+) |
| sortBy | String | daysInReview | Sort field: daysInReview, createdAt |
| sortDir | String | DESC | Sort direction |
| page | Integer | 1 | Page number |
| size | Integer | 10 | Items per page |

**Response:**
```json
{
  "summary": [
    {
      "ageRange": "0-15",
      "count": 23,
      "percentage": 38.3
    },
    {
      "ageRange": "16-30",
      "count": 18,
      "percentage": 30.0
    },
    {
      "ageRange": "31-60",
      "count": 12,
      "percentage": 20.0
    },
    {
      "ageRange": "60+",
      "count": 7,
      "percentage": 11.7
    }
  ],
  "details": {
    "items": [
      {
        "id": 101,
        "name": {"en": "AI Integration"},
        "category": {"en": "Automation"},
        "status": "PENDING_REVIEW",
        "daysInReview": 12,
        "createdAt": "2025-11-18"
      }
    ],
    "pagination": {...}
  }
}
```

---

### 11. Impact-Urgency Heatmap
**GET** `/impact-urgency-heatmap`

Returns challenge distribution matrix across scope and urgency dimensions.

**Query Parameters:**
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| scope | String | null | Filter by scope (DEPARTMENTAL, ORGANIZATIONAL, NATIONAL, GLOBAL) |
| urgency | String | null | Filter by urgency (CRITICAL, HIGH, MODERATE, LOW, VERY_LOW) |
| sortBy | String | createdAt | Sort field |
| sortDir | String | DESC | Sort direction |
| page | Integer | 1 | Page number |
| size | Integer | 10 | Items per page |

**Response:**
```json
{
  "matrix": [
    {
      "scope": "ORGANIZATIONAL",
      "urgency": "CRITICAL",
      "count": 8
    },
    {
      "scope": "ORGANIZATIONAL",
      "urgency": "HIGH",
      "count": 15
    }
  ],
  "details": {
    "items": [
      {
        "id": 101,
        "name": {"en": "AI Integration"},
        "category": {"en": "Automation"},
        "scope": "ORGANIZATIONAL",
        "urgency": "CRITICAL",
        "createdAt": "2025-11-15"
      }
    ],
    "pagination": {...}
  }
}
```

---

### 12. Rejection by Category
**GET** `/rejection-by-category`

Returns rejection rates and status breakdown per category.

**Query Parameters:**
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| categoryId | Long | null | Filter by category ID |
| status | String | null | Filter by status |
| sortBy | String | createdAt | Sort field |
| sortDir | String | DESC | Sort direction |
| page | Integer | 1 | Page number |
| size | Integer | 10 | Items per page |

**Response:**
```json
{
  "summary": [
    {
      "categoryId": 5,
      "category": {"en": "Automation", "ar": "الأتمتة"},
      "totalSubmitted": 50,
      "rejected": 12,
      "rejectionRate": 24.0
    }
  ],
  "details": {
    "items": [
      {
        "id": 101,
        "name": {"en": "AI Integration"},
        "categoryId": 5,
        "category": {"en": "Automation"},
        "status": "REJECTED",
        "createdAt": "2025-11-15"
      }
    ],
    "pagination": {...}
  }
}
```

---

### 13. Challenge Interconnection
**GET** `/challenge-interconnection`

Returns network graph showing challenge relationships and connections.

**Query Parameters:**
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| startDate | Date | null | Start date (ISO format: YYYY-MM-DD) |
| endDate | Date | null | End date |
| categoryId | Long | null | Filter by category ID |
| status | String | null | Filter by status |
| minConnections | Integer | 0 | Minimum connections threshold |

**Response:**
```json
{
  "nodes": [
    {
      "id": 101,
      "name": {"en": "AI Integration"},
      "category": {"en": "Automation"},
      "connectionCount": 5
    }
  ],
  "edges": [
    {
      "sourceId": 101,
      "targetId": 102,
      "connectionType": "RELATED",
      "weight": 3
    }
  ],
  "metrics": {
    "totalNodes": 45,
    "totalEdges": 78,
    "avgConnections": 3.4
  }
}
```

---

## Common Response Patterns

### Multilingual Names
All text fields support multiple languages:
```json
{
  "en": "English text",
  "ar": "النص العربي",
  "fr": "Texte français",
  "de": "Deutscher Text",
  "sw": "Maandishi ya Kiswahili"
}
```

### Pagination Metadata
Consistent across all paginated endpoints:
```json
{
  "currentPage": 1,
  "pageSize": 10,
  "totalPages": 16,
  "totalItems": 156
}
```

### Error Response
```json
{
  "timestamp": "2025-11-30T10:30:00",
  "status": 400,
  "error": "Bad Request",
  "message": "Invalid parameter value",
  "path": "/analytics/challenge/active-challenges"
}
```

---

## Use Cases

### Dashboard Overview
1. **GET** `/active-challenges` - Show total active challenges card
2. **GET** `/review-status` - Show review status distribution
3. **GET** `/approval-rate` - Show current approval rate with trend
4. **GET** `/top-categories` - Show top 3 categories
5. **GET** `/top-innovators` - Show top 3 contributors
6. **GET** `/delayed-challenges` - Show top 5 overdue challenges

### Drill-Down Analysis

Each analytics endpoint provides two-level data access:

#### Level 1: Summary Metrics
High-level aggregations displayed on dashboard cards:
- Total counts and percentages
- Top N items (categories, innovators, delayed challenges)
- Distribution breakdowns (urgency, status, scope)
- Trend indicators (approval rate change, peak week)

#### Level 2: Detailed Records
Paginated list of individual challenges with full attributes:
- Access via `details` object in response
- Default: First 10 items (configurable via `page` and `size`)
- Includes complete challenge information relevant to the metric

**Drill-Down Workflow:**
1. **Dashboard Display**: Show summary metrics to user
2. **User Interaction**: User clicks on metric/card to explore details
3. **Apply Filters**: Send request with specific filter parameters:
   - `categoryId` - Focus on specific category
   - `status` - Filter by challenge status
   - `urgency` - Filter by urgency level
   - `scope` - Filter by organizational scope
   - `ageRange` - Filter by review age (pending-review-by-age only)
   - `minEngagements` - Filter by engagement threshold
   - `minDaysOverdue` - Filter by days overdue
4. **Sort Results**: Order data by relevant field using `sortBy` and `sortDir`
5. **Navigate Pages**: Use `page` parameter to load more results
6. **Return to Summary**: User can navigate back to dashboard overview

**Example Drill-Down Scenarios:**

**Scenario 1: Investigate High-Urgency Challenges**
```
1. Dashboard shows: 45 CRITICAL urgency challenges
2. User clicks → Send: GET /active-challenges?urgency=CRITICAL&page=1&size=10
3. View 10 critical challenges with full details
4. Sort by creation date → Add: &sortBy=created_at&sortDir=DESC
5. Navigate to page 2 → Update: &page=2
```

**Scenario 2: Analyze Category Performance**
```
1. Dashboard shows: "Automation" category has 45 challenges (22.5%)
2. User clicks category → Send: GET /category-breakdown?categoryId=5&page=1&size=10
3. View all 45 challenges in Automation category
4. Filter by status → Add: &status=PENDING_REVIEW
5. Sort by urgency → Add: &sortBy=urgency&sortDir=DESC
```

**Scenario 3: Review Engagement Leaders**
```
1. Dashboard shows: Top 3 engaged challenges (peak engagement week)
2. User clicks "View All" → Send: GET /engagement-activity?sortBy=totalEngagements&sortDir=DESC&page=1&size=20
3. View top 20 most engaged challenges
4. Filter by category → Add: &categoryId=5
5. Filter by minimum engagement → Add: &minEngagements=100
```

**Scenario 4: Track Overdue Challenges**
```
1. Dashboard shows: 5 most delayed challenges
2. User clicks "View All Overdue" → Send: GET /delayed-challenges?page=1&size=20
3. View all overdue challenges
4. Filter critical only → Add: &urgency=CRITICAL
5. Filter seriously overdue → Add: &minDaysOverdue=30
```

**Benefits of Drill-Down Approach:**
- **Performance**: Dashboard loads quickly with aggregated data
- **Flexibility**: Users explore specific segments without overwhelming UI
- **Context**: Summary provides overview, details enable action
- **Progressive Disclosure**: Show only relevant information at each level
- **Scalability**: Handle large datasets via pagination without memory issues

### Trend Analysis
- **GET** `/engagement-activity` - Weekly engagement trends with date filtering
- **GET** `/approval-rate` - Quarter-over-quarter comparison
- **GET** `/pending-review-by-age` - Identify review bottlenecks

### Strategic Insights
- **GET** `/impact-urgency-heatmap` - Prioritize high-impact, high-urgency challenges
- **GET** `/challenge-interconnection` - Discover related challenges for synergy
- **GET** `/rejection-by-category` - Identify categories needing support
- **GET** `/scope-distribution` - Balance organizational vs departmental initiatives

---

## Performance Notes

- All endpoints support server-side pagination
- Default page size: 10 items
- Recommended max page size: 100 items
- Queries optimized with database indexes
- Response times: < 500ms for typical queries
- Date filters improve performance on large datasets

---

## Version
API Version: 1.0  
Last Updated: November 30, 2025
