# Service Catalog Analytics - Drill-Down Endpoints Documentation

This document provides detailed documentation for the drill-down endpoints in the Service Catalog Analytics API. These endpoints allow retrieving detailed service lists based on specific filtering criteria from various analytics charts.

## Base URL

```
/analytics/service-catalog
```

---

## 1. Automation Distribution Details

### Endpoint

```
GET /automation-distribution/details
```

### Description

Retrieves a paginated list of services filtered by automation level category. This endpoint provides drill-down functionality for the automation distribution chart.

### Query Parameters

| Parameter | Type   | Required | Default | Description                                           |
|-----------|--------|----------|---------|-------------------------------------------------------|
| category  | String | Yes      | -       | The automation level category to filter by            |
| page      | int    | No       | 0       | Page number (0-indexed)                               |
| size      | int    | No       | 20      | Number of items per page                              |
| sortBy    | String | No       | id      | Field to sort by                                      |
| sortDir   | String | No       | ASC     | Sort direction (ASC or DESC)                          |

### Response

Returns a `ServiceDrillDownDto<ServicesByAutomationLevelDto>` object containing:

#### Response Structure

```json
{
  "services": [
    {
      "id": 123,
      "nameTranslations": {
        "en": "Service Name",
        "ar": "اسم الخدمة"
      },
      "descriptionTranslations": {
        "en": "Service Description",
        "ar": "وصف الخدمة"
      },
      "type": {
        "en": "Service Type",
        "ar": "نوع الخدمة"
      },
      "automationLevel": {
        "en": "Fully Automated",
        "ar": "آلي بالكامل"
      }
    }
  ],
  "pagination": {
    "totalCount": 150,
    "totalPages": 8,
    "currentPage": 0,
    "pageSize": 20
  }
}
```

### Example Request

```http
GET /analytics/service-catalog/automation-distribution/details?category=FULLY_AUTOMATED&page=0&size=20&sortBy=id&sortDir=ASC
```

---

## 2. Process Documentation Details

### Endpoint

```
GET /process-documentation/details
```

### Description

Retrieves a paginated list of services filtered by their process documentation status and reengineering requirements. This endpoint provides drill-down functionality for the process documentation analysis chart.

### Query Parameters

| Parameter              | Type    | Required | Default | Description                                           |
|------------------------|---------|----------|---------|-------------------------------------------------------|
| reengineeringRequired  | Boolean | No       | -       | Filter by whether reengineering is required           |
| hasDocumentation       | Boolean | No       | -       | Filter by whether process has documentation           |
| page                   | int     | No       | 0       | Page number (0-indexed)                               |
| size                   | int     | No       | 20      | Number of items per page                              |
| sortBy                 | String  | No       | id      | Field to sort by                                      |
| sortDir                | String  | No       | ASC     | Sort direction (ASC or DESC)                          |

### Response

Returns a `ServiceDrillDownDto<ServicesByDocumentationStatusDto>` object containing:

#### Response Structure

```json
{
  "services": [
    {
      "id": 123,
      "nameTranslations": {
        "en": "Service Name",
        "ar": "اسم الخدمة"
      },
      "descriptionTranslations": {
        "en": "Service Description",
        "ar": "وصف الخدمة"
      },
      "type": {
        "en": "Service Type",
        "ar": "نوع الخدمة"
      },
      "reengineeringRequired": true,
      "processHasDocumentation": false
    }
  ],
  "pagination": {
    "totalCount": 75,
    "totalPages": 4,
    "currentPage": 0,
    "pageSize": 20
  }
}
```

### Example Requests

```http
# Get services requiring reengineering
GET /analytics/service-catalog/process-documentation/details?reengineeringRequired=true&page=0&size=20

# Get services with documentation
GET /analytics/service-catalog/process-documentation/details?hasDocumentation=true&page=0&size=20

# Get services requiring reengineering but without documentation
GET /analytics/service-catalog/process-documentation/details?reengineeringRequired=true&hasDocumentation=false&page=0&size=20
```

---

## 3. Impact Distribution Details

### Endpoint

```
GET /impact-distribution/details
```

### Description

Retrieves a paginated list of services filtered by impact type and level. This endpoint provides drill-down functionality for the impact distribution chart, supporting both social and economic impact filtering.

### Query Parameters

| Parameter   | Type   | Required | Default | Description                                           |
|-------------|--------|----------|---------|-------------------------------------------------------|
| impactType  | String | Yes      | -       | Type of impact (e.g., "SOCIAL", "ECONOMIC")           |
| impactLevel | String | Yes      | -       | Impact level to filter by (e.g., "HIGH", "MEDIUM", "LOW") |
| page        | int    | No       | 0       | Page number (0-indexed)                               |
| size        | int    | No       | 20      | Number of items per page                              |
| sortBy      | String | No       | id      | Field to sort by                                      |
| sortDir     | String | No       | ASC     | Sort direction (ASC or DESC)                          |

### Response

Returns a `ServiceDrillDownDto<ServicesByImpactLevelDto>` object containing:

#### Response Structure

```json
{
  "services": [
    {
      "id": 123,
      "nameTranslations": {
        "en": "Service Name",
        "ar": "اسم الخدمة"
      },
      "descriptionTranslations": {
        "en": "Service Description",
        "ar": "وصف الخدمة"
      },
      "type": {
        "en": "Service Type",
        "ar": "نوع الخدمة"
      },
      "socialImpact": {
        "en": "High",
        "ar": "عالي"
      },
      "economicImpact": {
        "en": "Medium",
        "ar": "متوسط"
      }
    }
  ],
  "pagination": {
    "totalCount": 100,
    "totalPages": 5,
    "currentPage": 0,
    "pageSize": 20
  }
}
```

### Example Requests

```http
# Get services with high social impact
GET /analytics/service-catalog/impact-distribution/details?impactType=SOCIAL&impactLevel=HIGH&page=0&size=20

# Get services with medium economic impact
GET /analytics/service-catalog/impact-distribution/details?impactType=ECONOMIC&impactLevel=MEDIUM&page=0&size=20
```

---

## 4. Vision 2040 Pillars Details

### Endpoint

```
GET /vision2040-pillars/details
```

### Description

Retrieves a paginated list of services filtered by Vision 2040 pillar. This endpoint provides drill-down functionality for the Vision 2040 pillar distribution chart.

### Query Parameters

| Parameter | Type   | Required | Default | Description                                           |
|-----------|--------|----------|---------|-------------------------------------------------------|
| pillarId  | Long   | Yes      | -       | ID of the Vision 2040 pillar to filter by             |
| page      | int    | No       | 0       | Page number (0-indexed)                               |
| size      | int    | No       | 20      | Number of items per page                              |
| sortBy    | String | No       | id      | Field to sort by                                      |
| sortDir   | String | No       | ASC     | Sort direction (ASC or DESC)                          |

### Response

Returns a `ServiceDrillDownDto<ServicesByVisionPillarDto>` object containing:

#### Response Structure

```json
{
  "services": [
    {
      "id": 123,
      "nameTranslations": {
        "en": "Service Name",
        "ar": "اسم الخدمة"
      },
      "descriptionTranslations": {
        "en": "Service Description",
        "ar": "وصف الخدمة"
      },
      "type": {
        "en": "Service Type",
        "ar": "نوع الخدمة"
      },
      "visionPillar": {
        "en": "Thriving Economy",
        "ar": "اقتصاد مزدهر"
      }
    }
  ],
  "pagination": {
    "totalCount": 85,
    "totalPages": 5,
    "currentPage": 0,
    "pageSize": 20
  }
}
```

### Example Request

```http
GET /analytics/service-catalog/vision2040-pillars/details?pillarId=1&page=0&size=20&sortBy=id&sortDir=ASC
```

---

## 5. Integration Exposure Heatmap Details

### Endpoint

```
GET /integration-exposure-heatmap/details
```

### Description

Retrieves a paginated list of services filtered by automation level and integration count bucket. This endpoint provides drill-down functionality for the integration exposure heatmap, which shows the relationship between automation levels and number of integrations.

### Query Parameters

| Parameter          | Type    | Required | Default | Description                                           |
|--------------------|---------|----------|---------|-------------------------------------------------------|
| automationLevelId  | Long    | Yes      | -       | ID of the automation level to filter by               |
| integrationBucket  | Integer | Yes      | -       | Integration count bucket (0, 1, 2, 3, 4, 5, or 6+)    |
| page               | int     | No       | 0       | Page number (0-indexed)                               |
| size               | int     | No       | 20      | Number of items per page                              |
| sortBy             | String  | No       | id      | Field to sort by                                      |
| sortDir            | String  | No       | ASC     | Sort direction (ASC or DESC)                          |

### Response

Returns a `ServicesByIntegrationExposureDto` object containing:

#### Response Structure

```json
{
  "automationLevelId": 2,
  "automationLevelName": {
    "en": "Partially Automated",
    "ar": "آلي جزئيًا"
  },
  "integrationBucket": 3,
  "services": [
    {
      "id": 123,
      "nameTranslations": {
        "en": "Service Name",
        "ar": "اسم الخدمة"
      },
      "descriptionTranslations": {
        "en": "Service Description",
        "ar": "وصف الخدمة"
      },
      "type": {
        "en": "Service Type",
        "ar": "نوع الخدمة"
      },
      "integrationCount": 3
    }
  ],
  "pagination": {
    "totalCount": 45,
    "totalPages": 3,
    "currentPage": 0,
    "pageSize": 20
  }
}
```

### Integration Buckets

The `integrationBucket` parameter accepts the following values:

- **0**: Services with 0 integrations
- **1**: Services with 1 integration
- **2**: Services with 2 integrations
- **3**: Services with 3 integrations
- **4**: Services with 4 integrations
- **5**: Services with 5 integrations
- **6+**: Services with 6 or more integrations

### Example Requests

```http
# Get partially automated services with 3 integrations
GET /analytics/service-catalog/integration-exposure-heatmap/details?automationLevelId=2&integrationBucket=3&page=0&size=20

# Get fully automated services with no integrations
GET /analytics/service-catalog/integration-exposure-heatmap/details?automationLevelId=1&integrationBucket=0&page=0&size=20

# Get manual services with 6+ integrations
GET /analytics/service-catalog/integration-exposure-heatmap/details?automationLevelId=3&integrationBucket=6&page=0&size=20
```

---

## Common Response Elements

### Pagination Metadata

All drill-down endpoints return pagination metadata with the following structure:

```json
{
  "pagination": {
    "totalCount": 150,
    "totalPages": 8,
    "currentPage": 0,
    "pageSize": 20
  }
}
```

| Field       | Type    | Description                                    |
|-------------|---------|------------------------------------------------|
| totalCount  | Long    | Total number of services matching the criteria |
| totalPages  | Integer | Total number of pages available                |
| currentPage | Integer | Current page number (0-indexed)                |
| pageSize    | Integer | Number of items per page                       |

### Multi-language Support

All service name, description, type, and category fields support multiple languages through translation maps:

```json
{
  "en": "English Text",
  "ar": "النص العربي"
}
```

---

## Error Responses

All endpoints may return the following error responses:

### 400 Bad Request

Invalid query parameters or missing required parameters.

```json
{
  "status": 400,
  "message": "Invalid parameter value",
  "timestamp": "2025-11-23T10:30:00Z"
}
```

### 404 Not Found

Requested resource (e.g., pillarId, automationLevelId) not found.

```json
{
  "status": 404,
  "message": "Resource not found",
  "timestamp": "2025-11-23T10:30:00Z"
}
```

### 500 Internal Server Error

Server error while processing the request.

```json
{
  "status": 500,
  "message": "Internal server error",
  "timestamp": "2025-11-23T10:30:00Z"
}
```

---

## Notes

1. **Pagination**: All endpoints support pagination with 0-indexed page numbers. Default page size is 20 items.
2. **Sorting**: Sorting is supported on multiple fields. Common sortable fields include `id`, `nameTranslations.en`, etc.
3. **Filtering**: Some endpoints support multiple optional filters that can be combined.
4. **Performance**: For large datasets, consider using appropriate page sizes and avoid requesting all data at once.
5. **Localization**: All translatable fields return both English and Arabic translations in a map structure.

---

## Version History

| Version | Date       | Changes                                  |
|---------|------------|------------------------------------------|
| 1.0     | 2025-11-23 | Initial documentation for 5 endpoints    |

