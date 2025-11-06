# Organization Dashboard API Documentation

## Overview
The Organization Dashboard provides comprehensive analytics endpoints for organizational structure, position management, and workforce distribution. The dashboard consists of two controller types:

1. **Cards Controller**: Key metrics and statistics (total positions, directorates, departments, sections)
2. **Charts Controller**: Detailed visualization data (job rank distribution, department breakdown, specialization analysis)

All endpoints support multi-language translations for category names using JSON translation maps.

## Base URL
```
/analytics/organization-dashboard
```

---

## Controllers & Endpoints

## A. Dashboard Cards Controller
**Base URL:** `/analytics/organization-dashboard`  
**Class:** `OrganizationDashboardCardsController`  
**Service:** `OrganizationDashboardCardsService`

Key metrics and statistics cards for the organization dashboard.

### 1. Total Positions Card
**Endpoint:** `GET /analytics/organization-dashboard/total-positions`

**Description:** Returns the total number of positions/units in the organization and the monthly change.

**Response:**
```json
{
  "totalPositions": 150,
  "monthlyChange": 5
}
```

**Response Fields:**
- `totalPositions` (Long): Total number of positions/units across the organization
- `monthlyChange` (Long): Change in positions this month (can be positive or negative)

**Example Usage:**
```bash
curl -X GET "http://localhost:8080/analytics/organization-dashboard/total-positions"
```

---

### 2. Top Functional Category Card
**Endpoint:** `GET /analytics/organization-dashboard/top-functional-category`

**Description:** Returns the top functional category by percentage and top 3 categories with multi-language support.

**Response:**
```json
{
  "topCategory": {
    "categoryName": {
      "en": "Technical",
      "ar": "تقني"
    },
    "percentage": 35.5,
    "count": 53
  },
  "topThreeCategories": [
    {
      "categoryName": {
        "en": "Technical",
        "ar": "تقني"
      },
      "percentage": 35.5,
      "count": 53
    },
    {
      "categoryName": {
        "en": "Administrative",
        "ar": "إداري"
      },
      "percentage": 28.0,
      "count": 42
    },
    {
      "categoryName": {
        "en": "Management",
        "ar": "إدارة"
      },
      "percentage": 20.0,
      "count": 30
    }
  ],
  "totalCategories": 8
}
```

**Response Fields:**
- `topCategory` (Object): The top functional category
  - `categoryName` (Map): Multi-language category name (en, ar, etc.)
  - `percentage` (Double): Percentage of positions in this category
  - `count` (Long): Number of positions in this category
- `topThreeCategories` (Array): List of top 3 functional categories with same structure
- `totalCategories` (Long): Total number of different functional categories

**Example Usage:**
```bash
curl -X GET "http://localhost:8080/analytics/organization-dashboard/top-functional-category"
```

---

### 3. Directorates Card
**Endpoint:** `GET /analytics/organization-dashboard/directorates`

**Description:** Returns statistics about directorates (active/inactive counts).

**Response:**
```json
{
  "totalDirectorates": 12,
  "activeDirectorates": 10,
  "inactiveDirectorates": 2
}
```

**Response Fields:**
- `totalDirectorates` (Long): Total number of directorates
- `activeDirectorates` (Long): Number of active directorates
- `inactiveDirectorates` (Long): Number of inactive directorates

**Example Usage:**
```bash
curl -X GET "http://localhost:8080/analytics/organization-dashboard/directorates"
```

---

### 4. Departments Card
**Endpoint:** `GET /analytics/organization-dashboard/departments`

**Description:** Returns statistics about departments (active/inactive counts).

**Response:**
```json
{
  "totalDepartments": 35,
  "activeDepartments": 32,
  "inactiveDepartments": 3
}
```

**Response Fields:**
- `totalDepartments` (Long): Total number of departments
- `activeDepartments` (Long): Number of active departments
- `inactiveDepartments` (Long): Number of inactive departments

**Example Usage:**
```bash
curl -X GET "http://localhost:8080/analytics/organization-dashboard/departments"
```

---

### 5. Sections Card
**Endpoint:** `GET /analytics/organization-dashboard/sections`

**Description:** Returns statistics about sections (active/inactive counts).

**Response:**
```json
{
  "totalSections": 89,
  "activeSections": 85,
  "inactiveSections": 4
}
```

**Response Fields:**
- `totalSections` (Long): Total number of sections
- `activeSections` (Long): Number of active sections
- `inactiveSections` (Long): Number of inactive sections

**Example Usage:**
```bash
curl -X GET "http://localhost:8080/analytics/organization-dashboard/sections"
```

---

## B. Dashboard Charts Controller
**Base URL:** `/analytics/organization-dashboard`  
**Class:** `OrganizationDashboardChartsController`  
**Service:** `OrganizationDashboardChartsService`

Detailed visualization data for charts on the organization dashboard.

### 1. Employees by Job Rank Chart
**Endpoint:** `GET /analytics/organization-dashboard/employees-by-job-rank`

**Description:** Returns employee distribution grouped by job level and rank.

**Response:**
```json
{
  "data": [
    {
      "jobRank": 1,
      "jobLevel": {
        "en": "Executive",
        "ar": "تنفيذي"
      },
      "employeeCount": 15,
      "percentage": 10.0
    },
    {
      "jobRank": 2,
      "jobLevel": {
        "en": "Senior",
        "ar": "أول"
      },
      "employeeCount": 45,
      "percentage": 30.0
    }
  ],
  "totalEmployees": 150,
  "jobLevels": [
    {"en": "Executive", "ar": "تنفيذي"},
    {"en": "Senior", "ar": "أول"}
  ],
  "jobRanks": [1, 2, 3, 4, 5]
}
```

**Response Fields:**
- `data` (Array): List of data points with job rank and level information
  - `jobRank` (Integer): Job rank number
  - `jobLevel` (Map): Multi-language job level name
  - `employeeCount` (Long): Number of employees at this rank
  - `percentage` (Double): Percentage of total employees
- `totalEmployees` (Long): Total number of employees
- `jobLevels` (Array): List of unique job levels with translations
- `jobRanks` (Array): List of unique job ranks

**Example Usage:**
```bash
curl -X GET "http://localhost:8080/analytics/organization-dashboard/employees-by-job-rank"
```

---

### 2. Department Size Overview Chart
**Endpoint:** `GET /analytics/organization-dashboard/department-size-overview`

**Description:** Shows employee distribution by job level across organizational units.

**Query Parameters:**
- `viewType` (String, default: "directorates"): View level - `directorates`, `departments`, or `sections`
- `directorateId` (Long, optional): Filter by specific directorate
- `departmentId` (Long, optional): Filter by specific department
- `sectionId` (Long, optional): Filter by specific section

**Response:**
```json
{
  "organizationalUnits": [
    {
      "unitName": {
        "en": "Human Resources",
        "ar": "الموارد البشرية"
      },
      "unitId": 101,
      "jobLevelBreakdown": [
        {
          "jobLevel": {
            "en": "Executive",
            "ar": "تنفيذي"
          },
          "count": 2
        },
        {
          "jobLevel": {
            "en": "Senior",
            "ar": "أول"
          },
          "count": 8
        }
      ],
      "totalEmployees": 25
    }
  ],
  "totalEmployees": 150,
  "jobLevels": [
    {"en": "Executive", "ar": "تنفيذي"},
    {"en": "Senior", "ar": "أول"}
  ]
}
```

**Response Fields:**
- `organizationalUnits` (Array): List of organizational units with breakdown
  - `unitName` (Map): Multi-language unit name
  - `unitId` (Long): Unit identifier
  - `jobLevelBreakdown` (Array): Employee count by job level
  - `totalEmployees` (Long): Total employees in this unit
- `totalEmployees` (Long): Total employees in filtered view
- `jobLevels` (Array): List of all job levels for legend

**Example Usage:**
```bash
curl -X GET "http://localhost:8080/analytics/organization-dashboard/department-size-overview?viewType=directorates"

curl -X GET "http://localhost:8080/analytics/organization-dashboard/department-size-overview?viewType=departments&directorateId=101"
```

---

### 3. Employee Job Level Breakdown Chart
**Endpoint:** `GET /analytics/organization-dashboard/employee-job-level-breakdown`

**Description:** Shows distribution of employees across different job levels with percentages.

**Response:**
```json
{
  "data": [
    {
      "jobLevel": {
        "en": "Executive",
        "ar": "تنفيذي"
      },
      "employeeCount": 15,
      "percentage": 10.0
    },
    {
      "jobLevel": {
        "en": "Senior",
        "ar": "أول"
      },
      "employeeCount": 60,
      "percentage": 40.0
    }
  ],
  "totalEmployees": 150
}
```

**Response Fields:**
- `data` (Array): List of job level breakdown points
  - `jobLevel` (Map): Multi-language job level name
  - `employeeCount` (Long): Number of employees at this level
  - `percentage` (Double): Percentage of total employees
- `totalEmployees` (Long): Total number of employees

**Example Usage:**
```bash
curl -X GET "http://localhost:8080/analytics/organization-dashboard/employee-job-level-breakdown"
```

---

### 4. Human Capital by Specialization Chart
**Endpoint:** `GET /analytics/organization-dashboard/human-capital-by-specialization`

**Description:** Shows employee distribution by specialization/functional category.

**Query Parameters:**
- `directorateId` (Long, optional): Filter by specific directorate

**Response:**
```json
{
  "specializations": [
    {
      "specializationName": {
        "en": "Software Development",
        "ar": "تطوير البرمجيات"
      },
      "employeeCount": 45,
      "percentage": 30.0
    },
    {
      "specializationName": {
        "en": "Quality Assurance",
        "ar": "ضمان الجودة"
      },
      "employeeCount": 30,
      "percentage": 20.0
    }
  ],
  "totalEmployees": 150,
  "largestCategory": {
    "en": "Software Development",
    "ar": "تطوير البرمجيات"
  },
  "largestCategoryPercentage": 30.0
}
```

**Response Fields:**
- `specializations` (Array): List of specializations with employee distribution
  - `specializationName` (Map): Multi-language specialization name
  - `employeeCount` (Long): Number of employees in this specialization
  - `percentage` (Double): Percentage of total employees
- `totalEmployees` (Long): Total employees in filtered view
- `largestCategory` (Map): Name of the largest specialization category
- `largestCategoryPercentage` (Double): Percentage of largest category

**Example Usage:**
```bash
curl -X GET "http://localhost:8080/analytics/organization-dashboard/human-capital-by-specialization"

curl -X GET "http://localhost:8080/analytics/organization-dashboard/human-capital-by-specialization?directorateId=101"
```

---

---

## Multi-Language Support

All category names and labels in the Organization Dashboard support multi-language translations. Names are returned as JSON maps with language codes as keys:

```json
{
  "categoryName": {
    "en": "Technical",
    "ar": "تقني",
    "fr": "Technique"
  }
}
```

**Supported Languages:**
- `en` - English
- `ar` - Arabic
- `fr` - French (if configured)

---

## HTTP Status Codes

| Status Code | Description |
|-------------|-------------|
| 200 | Success - Data retrieved successfully |
| 400 | Bad Request - Invalid parameters |
| 401 | Unauthorized - Authentication required |
| 403 | Forbidden - Insufficient permissions |
| 404 | Not Found - Endpoint not found |
| 500 | Internal Server Error - Server error |

---

## Error Response Format

```json
{
  "timestamp": "2025-11-06T10:30:00Z",
  "status": 400,
  "error": "Bad Request",
  "message": "Invalid request parameters",
  "path": "/analytics/organization-dashboard/total-positions"
}
```

---

## Implementation Details

### Backend Architecture

**Controllers:**
- `OrganizationDashboardCardsController` - Key metrics and statistics cards
- `OrganizationDashboardChartsController` - Visualization data for charts

**Services:**
- `OrganizationDashboardCardsService` - Business logic for cards
- `OrganizationDashboardChartsService` - Business logic for charts

**Data Access:** Repository pattern with native SQL queries

### Database Schema
- Uses tenant-specific schemas
- Enums table for multi-language translations
- Supports JSONB for translation storage
- Optimized indexes on job level, rank, and specialization columns

### Query Performance
- All queries use aggregation and grouping
- Optimized for dashboard card display
- Caching recommended for high-traffic scenarios
- Filter parameters allow fine-grained control over data scope

---

## Frontend Integration

### Overview
The Organization Dashboard provides 9 API endpoints organized in two controllers:
- **5 Cards endpoints** for key metrics and statistics
- **4 Charts endpoints** for detailed visualization data

### Request & Response Reference

#### Cards Controller

| Endpoint | Method | URL |
|----------|--------|-----|
| Total Positions | GET | `/analytics/organization-dashboard/total-positions` |
| Top Functional Category | GET | `/analytics/organization-dashboard/top-functional-category` |
| Directorates | GET | `/analytics/organization-dashboard/directorates` |
| Departments | GET | `/analytics/organization-dashboard/departments` |
| Sections | GET | `/analytics/organization-dashboard/sections` |

#### Charts Controller

| Endpoint | Method | URL | Parameters |
|----------|--------|-----|-----------|
| Employees by Job Rank | GET | `/analytics/organization-dashboard/employees-by-job-rank` | - |
| Department Size Overview | GET | `/analytics/organization-dashboard/department-size-overview` | `viewType`, `directorateId`, `departmentId`, `sectionId` |
| Employee Job Level Breakdown | GET | `/analytics/organization-dashboard/employee-job-level-breakdown` | - |
| Human Capital by Specialization | GET | `/analytics/organization-dashboard/human-capital-by-specialization` | `directorateId` |

---

## Postman Collection

Import this Postman collection for quick API testing:

```json
{
  "info": {
    "name": "Organization Dashboard API",
    "schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json"
  },
  "item": [
    {
      "name": "Cards",
      "item": [
        {
          "name": "Total Positions",
          "request": {
            "method": "GET",
            "url": "{{baseUrl}}/analytics/organization-dashboard/total-positions"
          }
        },
        {
          "name": "Top Functional Category",
          "request": {
            "method": "GET",
            "url": "{{baseUrl}}/analytics/organization-dashboard/top-functional-category"
          }
        },
        {
          "name": "Directorates",
          "request": {
            "method": "GET",
            "url": "{{baseUrl}}/analytics/organization-dashboard/directorates"
          }
        },
        {
          "name": "Departments",
          "request": {
            "method": "GET",
            "url": "{{baseUrl}}/analytics/organization-dashboard/departments"
          }
        },
        {
          "name": "Sections",
          "request": {
            "method": "GET",
            "url": "{{baseUrl}}/analytics/organization-dashboard/sections"
          }
        }
      ]
    },
    {
      "name": "Charts",
      "item": [
        {
          "name": "Employees by Job Rank",
          "request": {
            "method": "GET",
            "url": "{{baseUrl}}/analytics/organization-dashboard/employees-by-job-rank"
          }
        },
        {
          "name": "Department Size Overview (Directorates)",
          "request": {
            "method": "GET",
            "url": "{{baseUrl}}/analytics/organization-dashboard/department-size-overview?viewType=directorates"
          }
        },
        {
          "name": "Department Size Overview (Departments)",
          "request": {
            "method": "GET",
            "url": "{{baseUrl}}/analytics/organization-dashboard/department-size-overview?viewType=departments"
          }
        },
        {
          "name": "Department Size Overview (Sections)",
          "request": {
            "method": "GET",
            "url": "{{baseUrl}}/analytics/organization-dashboard/department-size-overview?viewType=sections"
          }
        },
        {
          "name": "Employee Job Level Breakdown",
          "request": {
            "method": "GET",
            "url": "{{baseUrl}}/analytics/organization-dashboard/employee-job-level-breakdown"
          }
        },
        {
          "name": "Human Capital by Specialization",
          "request": {
            "method": "GET",
            "url": "{{baseUrl}}/analytics/organization-dashboard/human-capital-by-specialization"
          }
        },
        {
          "name": "Human Capital by Specialization (Filtered)",
          "request": {
            "method": "GET",
            "url": "{{baseUrl}}/analytics/organization-dashboard/human-capital-by-specialization?directorateId=101"
          }
        }
      ]
    }
  ]
}
```

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.1 | 2025-11-06 | Added Charts Controller with 4 visualization endpoints |
| 1.0 | 2025-11-06 | Initial release with 5 dashboard card endpoints |

---

## Support & Troubleshooting

### Common Issues

**Issue:** Empty results from Top Functional Category endpoint
- **Cause:** No functional categories configured or positions not assigned to categories
- **Solution:** Ensure positions have valid functional category assignments in the system

**Issue:** Multi-language translations not displaying
- **Cause:** Missing translation entries in enums table
- **Solution:** Verify that category names have translations in the public schema enums table

**Issue:** Active/Inactive counts don't match total
- **Cause:** Data consistency issues or filtering logic
- **Solution:** Check status_code values in database (should be 'ACTIVE' or 'INACTIVE')

---

## See Also
- [Talent Dashboard API](./PORTFOLIO_ANALYTICS_API.md)
- [Database Schema](./tenant_2292.graphml)
- [Implementation Guide](./README_PORTFOLIO_IMPLEMENTATION.md)
