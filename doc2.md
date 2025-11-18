# Integration Analytics Drill-Down Endpoints Documentation

## Overview
This document describes the newly added drill-down endpoints for the Integration Analytics Dashboard. These endpoints provide detailed data when users click on summary visualizations to explore deeper insights.

---

## New Drill-Down Endpoints

### 1. **Total Integrations Details**
**Endpoint:** `GET /analytics/integration/total/details`

**Description:** Returns detailed information about all active integrations including their authorities and applications.

**Response Structure:**
```json
{
  "integrations": [
    {
      "id": 1,
      "nameTranslations": {"en": "API Integration", "ar": "تكامل API"},
      "descriptionTranslations": {"en": "Description", "ar": "الوصف"},
      "integrationType": {"en": "REST API", "ar": "REST API"},
      "integrationMethod": {"en": "Synchronous", "ar": "متزامن"},
      "accessibilityLevel": {"en": "Public", "ar": "عام"},
      "producingAuthorities": [
        {
          "id": 10,
          "nameTranslations": {"en": "Authority A", "ar": "الجهة أ"}
        }
      ],
      "destinationAuthorities": [
        {
          "id": 20,
          "nameTranslations": {"en": "Authority B", "ar": "الجهة ب"}
        }
      ],
      "applications": [
        {
          "id": 5,
          "nameTranslations": {"en": "App One", "ar": "التطبيق واحد"}
        }
      ]
    }
  ]
}
```

**Use Case:** Displayed when user clicks "Details" on the Total Integrations card.

---

### 2. **Applications in Use Details**
**Endpoint:** `GET /analytics/integration/applications/details`

**Description:** Returns detailed list of applications with their roles (SOURCE/RECEIVING/BOTH) and integration counts.

**Response Structure:**
```json
{
  "applications": [
    {
      "id": 5,
      "nameTranslations": {"en": "App One", "ar": "التطبيق واحد"},
      "descriptionTranslations": {"en": "App description", "ar": "وصف التطبيق"},
      "role": "SOURCE",
      "integrationCount": 12
    },
    {
      "id": 8,
      "nameTranslations": {"en": "App Two", "ar": "التطبيق اثنان"},
      "descriptionTranslations": {"en": "App description", "ar": "وصف التطبيق"},
      "role": "BOTH",
      "integrationCount": 25
    }
  ]
}
```

**Fields:**
- `role`: Can be "SOURCE", "RECEIVING", or "BOTH"
- `integrationCount`: Total number of integrations for this application

**Use Case:** Displayed when user clicks "View Details" on the Applications in Use card.

---

### 3. **Security Access Overview Details**
**Endpoint:** `GET /analytics/integration/security-overview/details`

**Description:** Returns complete breakdown of integration types, methods, and access levels with counts and percentages.

**Response Structure:**
```json
{
  "integrationTypes": [
    {
      "nameTranslations": {"en": "REST API", "ar": "REST API"},
      "count": 45,
      "percentage": 62.5
    },
    {
      "nameTranslations": {"en": "SOAP", "ar": "SOAP"},
      "count": 27,
      "percentage": 37.5
    }
  ],
  "integrationMethods": [
    {
      "nameTranslations": {"en": "Synchronous", "ar": "متزامن"},
      "count": 50,
      "percentage": 69.4
    }
  ],
  "accessLevels": [
    {
      "nameTranslations": {"en": "Public", "ar": "عام"},
      "count": 35,
      "percentage": 48.6
    }
  ]
}
```

**Use Case:** Displayed when user clicks on the Security Overview card to see full distributions.

---

### 4. **Integrations by Application ID**
**Endpoint:** `GET /analytics/integration/usage-by-application/{applicationId}`

**Description:** Returns all integrations associated with a specific application.

**Path Parameters:**
- `applicationId` (Long, required): The ID of the application

**Response Structure:**
```json
{
  "integrations": [
    {
      "id": 1,
      "nameTranslations": {"en": "Integration Name", "ar": "اسم التكامل"},
      "integrationType": {"en": "REST API", "ar": "REST API"},
      "integrationMethod": {"en": "Synchronous", "ar": "متزامن"},
      "accessibilityLevel": {"en": "Public", "ar": "عام"}
    }
  ]
}
```

**Use Case:** Displayed when user clicks on a specific application bar in the "Usage by Application" chart.

---

### 5. **Integrations by Type**
**Endpoint:** `GET /analytics/integration/by-type/{typeId}`

**Description:** Returns all integrations of a specific type (e.g., REST API, SOAP).

**Path Parameters:**
- `typeId` (Long, required): The ID of the integration type enum

**Response Structure:**
```json
{
  "integrations": [
    {
      "id": 1,
      "nameTranslations": {"en": "Integration Name", "ar": "اسم التكامل"},
      "descriptionTranslations": {"en": "Description", "ar": "الوصف"},
      "integrationType": {"en": "REST API", "ar": "REST API"},
      "integrationMethod": {"en": "Synchronous", "ar": "متزامن"},
      "accessibilityLevel": {"en": "Public", "ar": "عام"}
    }
  ]
}
```

**Use Case:** Displayed when user clicks on a slice of the "Integration Type Breakdown" pie chart.

**Note:** The `typeId` can be obtained from the `/by-type` summary endpoint which now returns IDs along with names.

---

### 6. **Integrations by Method**
**Endpoint:** `GET /analytics/integration/by-method/{methodId}`

**Description:** Returns all integrations using a specific method (e.g., Synchronous, Asynchronous).

**Path Parameters:**
- `methodId` (Long, required): The ID of the integration method enum

**Response Structure:**
```json
{
  "integrations": [
    {
      "id": 1,
      "nameTranslations": {"en": "Integration Name", "ar": "اسم التكامل"},
      "descriptionTranslations": {"en": "Description", "ar": "الوصف"},
      "integrationType": {"en": "REST API", "ar": "REST API"},
      "integrationMethod": {"en": "Synchronous", "ar": "متزامن"},
      "accessibilityLevel": {"en": "Public", "ar": "عام"}
    }
  ]
}
```

**Use Case:** Displayed when user clicks on a slice of the "Integration Method Breakdown" pie chart.

**Note:** The `methodId` can be obtained from the `/by-method` summary endpoint which now returns IDs along with names.

---

### 7. **Integrations by Access Level**
**Endpoint:** `GET /analytics/integration/access-level/{accessLevelId}`

**Description:** Returns all integrations with a specific access level (e.g., Public, Private, Internal).

**Path Parameters:**
- `accessLevelId` (Long, required): The ID of the access level enum

**Response Structure:**
```json
{
  "integrations": [
    {
      "id": 1,
      "nameTranslations": {"en": "Integration Name", "ar": "اسم التكامل"},
      "descriptionTranslations": {"en": "Description", "ar": "الوصف"},
      "integrationType": {"en": "REST API", "ar": "REST API"},
      "integrationMethod": {"en": "Synchronous", "ar": "متزامن"},
      "accessibilityLevel": {"en": "Public", "ar": "عام"}
    }
  ]
}
```

**Use Case:** Displayed when user clicks on a slice of the "Access Level Breakdown" pie chart.

**Note:** The `accessLevelId` can be obtained from the `/access-level` summary endpoint which now returns IDs along with names.

---

## Enhanced Summary Endpoints

The following existing endpoints have been enhanced to include enum IDs for drill-down navigation:

### **Integration Type Breakdown** (Enhanced)
**Endpoint:** `GET /analytics/integration/by-type`

**Response Structure:**
```json
{
  "items": [
    {
      "id": 101,
      "nameTranslations": {"en": "REST API", "ar": "REST API"},
      "percentage": 62.5,
      "count": 45
    }
  ]
}
```

**What's New:** Added `id` field to enable drill-down navigation.

---

### **Integration Method Breakdown** (Enhanced)
**Endpoint:** `GET /analytics/integration/by-method`

**Response Structure:**
```json
{
  "items": [
    {
      "id": 201,
      "nameTranslations": {"en": "Synchronous", "ar": "متزامن"},
      "percentage": 69.4,
      "count": 50
    }
  ]
}
```

**What's New:** Added `id` field to enable drill-down navigation.

---

### **Access Level Breakdown** (Enhanced)
**Endpoint:** `GET /analytics/integration/access-level`

**Response Structure:**
```json
{
  "items": [
    {
      "id": 301,
      "nameTranslations": {"en": "Public", "ar": "عام"},
      "percentage": 48.6,
      "count": 35
    }
  ]
}
```

**What's New:** Added `id` field to enable drill-down navigation.

---

## Implementation Notes

### Multi-Language Support
All endpoints return translations in JSONB format supporting:
- **en**: English
- **ar**: Arabic
- **fr**: French
- **de**: German
- **sw**: Swahili

### Performance Optimizations
1. **Shared Query Helper**: Type, method, and access level breakdown queries use a single parameterized helper method
2. **CTE Usage**: Common Table Expressions for better query performance
3. **JSON Aggregation**: PostgreSQL JSON functions used to minimize database round trips
4. **Index-Friendly**: Queries optimized to use existing indexes on `status_code` and foreign keys

### Error Handling
All endpoints include:
- Try-catch blocks with logging
- Empty array/object fallbacks on errors
- Consistent error logging patterns

---

## Frontend Integration Guide

### Drill-Down Flow Example

1. **User views summary chart** (e.g., `/by-type`)
   - Chart displays: "REST API: 62.5% (45 integrations)"
   - Store the `id: 101` from response

2. **User clicks on chart slice**
   - Frontend calls: `/by-type/101`
   - Displays modal/page with detailed list of all 45 REST API integrations

3. **User explores integration details**
   - Each integration shows type, method, access level, authorities, applications

### Recommended UI Patterns

- **Cards with "View Details" buttons**: For summary metrics (Total, Applications, Security Overview)
- **Interactive charts**: For breakdown visualizations (Type, Method, Access Level)
- **Modal dialogs**: For displaying drill-down lists
- **Data tables**: For drill-down results with sorting/filtering
- **Breadcrumbs**: To navigate back from drill-down views

---

## Testing Examples

### cURL Examples

```bash
# Get total integrations details
curl -X GET "http://localhost:8080/analytics/integration/total/details"

# Get applications in use details
curl -X GET "http://localhost:8080/analytics/integration/applications/details"

# Get security overview details
curl -X GET "http://localhost:8080/analytics/integration/security-overview/details"

# Get integrations by application ID
curl -X GET "http://localhost:8080/analytics/integration/usage-by-application/5"

# Get integrations by type ID
curl -X GET "http://localhost:8080/analytics/integration/by-type/101"

# Get integrations by method ID
curl -X GET "http://localhost:8080/analytics/integration/by-method/201"

# Get integrations by access level ID
curl -X GET "http://localhost:8080/analytics/integration/access-level/301"
```

---

## Change Summary

### Endpoints Added: 7
1. `/total/details` - Total integrations drill-down
2. `/applications/details` - Applications in use drill-down
3. `/security-overview/details` - Security overview drill-down
4. `/usage-by-application/{applicationId}` - Application-specific integrations
5. `/by-type/{typeId}` - Type-specific integrations
6. `/by-method/{methodId}` - Method-specific integrations
7. `/access-level/{accessLevelId}` - Access level-specific integrations

### Endpoints Enhanced: 3
1. `/by-type` - Now includes enum IDs
2. `/by-method` - Now includes enum IDs
3. `/access-level` - Now includes enum IDs

### DTOs Created: 5
1. `IntegrationDetailsDto` - For total integrations details
2. `IntegrationApplicationsDetailsDto` - For applications details
3. `SecurityAccessOverviewDetailsDto` - For security overview details
4. `ApplicationIntegrationsDetailsDto` - For application-specific integrations
5. `CategoryIntegrationsDetailsDto` - Shared DTO for type/method/access level drill-downs

---

## Architecture Overview

```
Controller Layer (IntegrationAnalyticsController)
    ↓
Service Layer (IntegrationAnalyticsService)
    ↓
Repository Layer (IntegrationAnalyticsRepository)
    ↓
Database (PostgreSQL with JPA/Native Queries)
```

All drill-down endpoints follow the same clean architecture pattern with proper separation of concerns.

---

## Status Codes

- **200 OK**: Successful request with data
- **500 Internal Server Error**: Database or server error (logged, returns empty fallback)

All endpoints use `status_code = 'ACTIVE'` filter to ensure only active integrations are returned.

---

## Version Information

- **Branch**: `INTEGRATION_DRILL`
- **Feature**: Integration Analytics Drill-Down Endpoints
- **Date**: November 18, 2025
