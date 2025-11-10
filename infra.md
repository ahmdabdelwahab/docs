# InfrastructureAnalyticsController

## Overview

The `InfrastructureAnalyticsController` provides REST API endpoints for retrieving infrastructure analytics data. It serves as the presentation layer for infrastructure-related metrics, statistics, and insights.

**Package:** `dpkass.tadafur.manjam.controller.analytics.infrastructure`

**Base URL:** `/analytics/infrastructure`

## Dependencies

- `InfrastructureAnalyticsService` - Service layer for business logic and data processing

## Endpoints

### 1. Get Infrastructure Overview

**Endpoint:** `GET /analytics/infrastructure/total`

**Description:** Retrieves an overview of the infrastructure metrics.

**Response Type:** `InfrastructureOverviewDto`

**Example:**
```http
GET /analytics/infrastructure/total
```

**Response:**
```json
{
  "totalInfrastructure": 150,
  "activeInfrastructure": 120,
  "inactiveInfrastructure": 30
}
```

---

### 2. Get Top Vendors by Infrastructure

**Endpoint:** `GET /analytics/infrastructure/top-vendors`

**Description:** Retrieves the top vendors ranked by their infrastructure count.

**Parameters:**
- `limit` (optional, default: 5) - Number of top vendors to return

**Response Type:** `List<TopVendorsByInfrastructureDto>`

**Example:**
```http
GET /analytics/infrastructure/top-vendors?limit=10
```

**Response:**
```json
[
  {
    "vendorName": "Vendor A",
    "infrastructureCount": 45
  },
  {
    "vendorName": "Vendor B",
    "infrastructureCount": 38
  }
]
```

---

### 3. Get Top Implemented Infrastructure

**Endpoint:** `GET /analytics/infrastructure/top-implemented`

**Description:** Retrieves the most frequently implemented infrastructure types.

**Parameters:**
- `limit` (optional, default: 5) - Number of top infrastructure types to return

**Response Type:** `List<TopImplementedInfrastructureDto>`

**Example:**
```http
GET /analytics/infrastructure/top-implemented?limit=10
```

**Response:**
```json
[
  {
    "infrastructureName": "Cloud Storage",
    "implementationCount": 67
  },
  {
    "infrastructureName": "Load Balancer",
    "implementationCount": 54
  }
]
```

---

### 4. Get Top Used Components Overview

**Endpoint:** `GET /analytics/infrastructure/top-used`

**Description:** Retrieves an overview of the most frequently used infrastructure components.

**Parameters:**
- `language` (optional, default: "en") - Language code for localization

**Response Type:** `TopUsedComponentsOverviewDto`

**Example:**
```http
GET /analytics/infrastructure/top-used?language=en
```

**Response:**
```json
{
  "components": [
    {
      "componentName": "Component A",
      "usageCount": 123
    }
  ]
}
```

---

### 5. Get Infrastructure Portfolio Distribution

**Endpoint:** `GET /analytics/infrastructure/distribution`

**Description:** Retrieves the distribution of infrastructure across the portfolio.

**Response Type:** `InfrastructurePortfolioDistributionDto`

**Example:**
```http
GET /analytics/infrastructure/distribution
```

**Response:**
```json
{
  "categories": [
    {
      "categoryName": "Network",
      "percentage": 35.5,
      "count": 45
    },
    {
      "categoryName": "Storage",
      "percentage": 28.3,
      "count": 36
    }
  ]
}
```

---

### 6. Get Infrastructure by Category

**Endpoint:** `GET /analytics/infrastructure/by-category`

**Description:** Retrieves detailed infrastructure information filtered by category ID.

**Parameters:**
- `categoryId` (required) - The ID of the category to filter by

**Response Type:** `List<InfrastructureDetailDto>`

**Example:**
```http
GET /analytics/infrastructure/by-category?categoryId=cat-123
```

**Response:**
```json
[
  {
    "infrastructureId": "inf-001",
    "infrastructureName": "Main Server",
    "categoryId": "cat-123",
    "vendor": "Vendor A",
    "status": "active"
  }
]
```

---

### 7. Get Infrastructure Per Vendor

**Endpoint:** `GET /analytics/infrastructure/per-vendor`

**Description:** Retrieves infrastructure distribution grouped by vendor.

**Parameters:**
- `limit` (optional, default: 10) - Number of vendors to return

**Response Type:** `List<InfrastructurePerVendorDto>`

**Example:**
```http
GET /analytics/infrastructure/per-vendor?limit=15
```

**Response:**
```json
[
  {
    "vendorName": "Vendor A",
    "infrastructures": [
      {
        "infrastructureName": "Server A",
        "count": 12
      }
    ],
    "totalCount": 45
  }
]
```

---

### 8. Get Infrastructure Ecosystem Composition

**Endpoint:** `GET /analytics/infrastructure/ecosystem-composition`

**Description:** Retrieves the composition of the infrastructure ecosystem, showing how different infrastructure types are distributed.

**Parameters:**
- `limit` (optional, default: 10) - Number of ecosystem components to return

**Response Type:** `List<InfrastructureEcosystemCompositionDto>`

**Example:**
```http
GET /analytics/infrastructure/ecosystem-composition?limit=20
```

**Response:**
```json
[
  {
    "ecosystemType": "Cloud Infrastructure",
    "count": 78,
    "percentage": 42.5
  },
  {
    "ecosystemType": "On-Premise Infrastructure",
    "count": 56,
    "percentage": 30.5
  }
]
```

---

## Error Handling

All endpoints return standard HTTP status codes:

- `200 OK` - Successful request
- `400 Bad Request` - Invalid parameters
- `404 Not Found` - Resource not found
- `500 Internal Server Error` - Server-side error

## Architecture

This controller follows the layered architecture pattern:

```
Controller (InfrastructureAnalyticsController)
    ↓
Service (InfrastructureAnalyticsService)
    ↓
Repository/DAO Layer
    ↓
Database
```

## Technologies

- **Spring Boot** - Web framework
- **Spring Web** - REST API support
- **Lombok** - Reduces boilerplate code with `@RequiredArgsConstructor`

## Notes

- All endpoints return JSON responses wrapped in `ResponseEntity`
- The controller uses constructor injection via Lombok's `@RequiredArgsConstructor`
- Default parameter values are provided for pagination and localization
- The controller is stateless and thread-safe
