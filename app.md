# Application Management Analytics API Documentation

## Overview

The Application Analytics module provides comprehensive metrics and insights into the organization's application portfolio. This includes category breakdowns, vendor analysis, deployment models, support coverage, and ecosystem composition.

## Base URL

```
/analytics/applications
```

## Authentication

All endpoints require authentication. Include the authentication token in the request headers.

---

## Endpoints

### 1. Total Applications by Category

Returns total application count grouped by root category with hierarchical resolution.

**Endpoint:** `GET /analytics/applications/total-applications`

**Response:**
```json
{
  "totalApplications": 100,
  "categoryBreakdown": [
    {
      "categoryName": {
        "en": "Business Applications",
        "ar": "تطبيقات الأعمال"
      },
      "count": 45,
      "percentage": 45.0
    },
    {
      "categoryName": {
        "en": "Infrastructure",
        "ar": "البنية التحتية"
      },
      "count": 35,
      "percentage": 35.0
    }
  ]
}
```

**Features:**
- Hierarchical category traversal to find root categories
- Handles up to 3 levels of category hierarchy
- Only includes ACTIVE applications
- Percentage calculated against total active applications

---

### 2. Top Vendors

Returns top 10 vendors by application count.

**Endpoint:** `GET /analytics/applications/top-vendors`

**Response:**
```json
{
  "totalVendors": 25,
  "totalApplications": 100,
  "vendors": [
    {
      "vendorId": "123",
      "vendorName": {
        "en": "Microsoft",
        "ar": "مايكروسوفت"
      },
      "applicationCount": 15,
      "percentage": 15.0
    },
    {
      "vendorId": "124",
      "vendorName": {
        "en": "Oracle",
        "ar": "أوراكل"
      },
      "applicationCount": 12,
      "percentage": 12.0
    }
  ]
}
```

**Features:**
- Top 10 vendors only
- Includes total unique vendor count
- Percentage per vendor
- Excludes applications without vendors from the breakdown

---

### 3. Deployment Model Distribution

Returns application distribution across deployment models (Cloud, On-Premise, Hybrid, etc.).

**Endpoint:** `GET /analytics/applications/deployment-models`

**Response:**
```json
{
  "totalApplications": 100,
  "deploymentBreakdown": [
    {
      "deploymentModel": {
        "en": "Cloud",
        "ar": "السحابة"
      },
      "count": 60,
      "percentage": 60.0
    },
    {
      "deploymentModel": {
        "en": "On-Premise",
        "ar": "في الموقع"
      },
      "count": 30,
      "percentage": 30.0
    },
    {
      "deploymentModel": {
        "en": "Hybrid",
        "ar": "مختلط"
      },
      "count": 10,
      "percentage": 10.0
    }
  ]
}
```

**Features:**
- Groups by deployment model enum
- Handles NULL deployment models
- Sorted by count descending

---

### 4. Support Coverage

Returns count and percentage of applications with support contact information.

**Endpoint:** `GET /analytics/applications/support-coverage`

**Response:**
```json
{
  "applicationsWithSupport": 85,
  "totalApplications": 100,
  "percentage": 85.0
}
```

**Features:**
- Checks for any support contact field: name, email, or phone
- Simple boolean logic (has support or doesn't)
- Rounded to 2 decimal places

---

### 5. Portfolio Distribution

Returns application distribution by root portfolio types (top-level categories).

**Endpoint:** `GET /analytics/applications/portfolio-distribution`

**Response:**
```json
{
  "totalApplications": 100,
  "portfolioBreakdown": [
    {
      "portfolioTypeId": "1",
      "portfolioTypeName": {
        "en": "Enterprise Applications",
        "ar": "تطبيقات المؤسسة"
      },
      "count": 45,
      "percentage": 45.0
    },
    {
      "portfolioTypeId": "2",
      "portfolioTypeName": {
        "en": "Infrastructure Services",
        "ar": "خدمات البنية التحتية"
      },
      "count": 35,
      "percentage": 35.0
    },
    {
      "portfolioTypeId": null,
      "portfolioTypeName": {
        "en": "Uncategorized",
        "ar": "غير مصنف"
      },
      "count": 20,
      "percentage": 20.0
    }
  ]
}
```

**Features:**
- Uses recursive CTE to find root categories
- Maps all subcategories to their root parent
- Includes uncategorized applications (NULL category)
- Click-through to detailed applications via portfolioTypeId

---

### 6. Applications by Portfolio Type (Drill-down)

Returns detailed list of applications for a specific portfolio type.

**Endpoint:** `GET /analytics/applications/portfolio-distribution/apps-drill`

**Query Parameters:**
- `portfolioTypeId` (optional): The root category ID. Pass `null` or omit for uncategorized applications.

**Example Request:**
```
GET /analytics/applications/portfolio-distribution/apps-drill?portfolioTypeId=1
```

**Response:**
```json
{
  "portfolioTypeId": "1",
  "portfolioTypeName": {
    "en": "Enterprise Applications",
    "ar": "تطبيقات المؤسسة"
  },
  "totalApplications": 12,
  "applications": [
    {
      "applicationId": "60",
      "applicationName": {
        "en": "SAP ERP",
        "ar": "ساب"
      },
      "categoryName": {
        "en": "ERP Systems",
        "ar": "أنظمة تخطيط موارد المؤسسات"
      },
      "version": "S/4HANA 2022",
      "vendorName": {
        "en": "SAP",
        "ar": "ساب"
      },
      "ownerName": {
        "en": "IT Department",
        "ar": "قسم تقنية المعلومات"
      },
      "deploymentModel": {
        "en": "Cloud",
        "ar": "السحابة"
      },
      "statusCode": "ACTIVE"
    }
  ]
}
```

**Features:**
- Recursive CTE includes all descendant categories
- Special handling for uncategorized apps (portfolioTypeId = null)
- Returns full application details with translations
- Sorted alphabetically by English name
- Shows immediate category, not root category

**Uncategorized Applications:**
```
GET /analytics/applications/portfolio-distribution/applications?portfolioTypeId=null
```
or
```
GET /analytics/applications/portfolio-distribution/applications
```

---

### 7. Ecosystem Composition

Returns applications with their ecosystem component counts (services, infrastructure, integrations, licenses).

**Endpoint:** `GET /analytics/applications/ecosystem-composition`

**Response:**
```json
{
  "totalApplications": 100,
  "totalApplicationsWithEcosystem": 100,
  "applications": [
    {
      "applicationId": "60",
      "applicationName": {
        "en": "SAP ERP",
        "ar": "ساب"
      },
      "components": {
        "enabledServices": 15,
        "infrastructureDeployedOn": 5,
        "requiredIntegrations": 25,
        "utilizedIntegrations": 10,
        "usedLicenses": 8
      },
      "totalComponents": 63
    },
    {
      "applicationId": "52",
      "applicationName": {
        "en": "TADAFUR",
        "ar": "تدافر"
      },
      "components": {
        "enabledServices": 0,
        "infrastructureDeployedOn": 0,
        "requiredIntegrations": 0,
        "utilizedIntegrations": 0,
        "usedLicenses": 0
      },
      "totalComponents": 0
    }
  ]
}
```

**Features:**
- Complex query joining 5 junction tables
- Distinct counts to avoid duplicates
- Sorted by most interconnected applications (highest totalComponents)
- Shows ecosystem dependency levels

**Component Definitions:**
- **enabledServices**: Services provided by this application
- **infrastructureDeployedOn**: Infrastructure components hosting this application
- **requiredIntegrations**: Integrations this application requires (as source)
- **utilizedIntegrations**: Integrations this application consumes (as destination)
- **usedLicenses**: Licenses associated with this application

---

### 8. Technology Vendors

Returns all vendors with their application counts (not limited to top 10).

**Endpoint:** `GET /analytics/applications/technology-vendors`

**Response:**
```json
{
  "totalVendors": 25,
  "totalApplications": 100,
  "vendors": [
    {
      "vendorId": "123",
      "vendorName": {
        "en": "Microsoft",
        "ar": "مايكروسوفت"
      },
      "applicationCount": 15,
      "percentage": 15.0
    },
    {
      "vendorId": "124",
      "vendorName": {
        "en": "Oracle",
        "ar": "أوراكل"
      },
      "applicationCount": 12,
      "percentage": 12.0
    }
  ]
}
```

**Features:**
- Returns ALL vendors (no limit)
- Only vendors with applications shown (HAVING COUNT > 0)
- Uses INNER JOIN to exclude applications without vendors
- Sorted by application count descending

---

### 9. Distribution by Attribute

Returns application distribution grouped by a dynamic attribute type.

**Endpoint:** `GET /analytics/applications/distribution-by-attribute`

**Query Parameters:**
- `attributeType` (optional, default: "status"): The attribute to group by

**Supported Attribute Types:**
- `status` - Application Status
- `deploymentModel` - Deployment Models
- `authenticationMechanism` - Authentication Mechanism
- `accessControlMethod` - Access Control Methods
- `applicationSource` - Application Source

**Example Request:**
```
GET /analytics/applications/distribution-by-attribute?attributeType=status
```

**Response:**
```json
{
  "attributeType": "status",
  "totalApplications": 100,
  "attributeBreakdown": [
    {
      "attributeValue": {
        "en": "Production",
        "ar": "الإنتاج"
      },
      "count": 75,
      "percentage": 75.0
    },
    {
      "attributeValue": {
        "en": "Development",
        "ar": "التطوير"
      },
      "count": 20,
      "percentage": 20.0
    },
    {
      "attributeValue": {
        "en": "Retired",
        "ar": "متقاعد"
      },
      "count": 5,
      "percentage": 5.0
    }
  ]
}
```

**Features:**
- Dynamic attribute selection via parameter
- Maps to appropriate enum types automatically
- Validates attribute type (defaults to "status" if invalid)
- Only returns attributes with applications (HAVING COUNT > 0)

---

## Data Model

### Multilingual Support

All text fields support multiple languages via JSONB `name_translations` field:

```json
{
  "en": "English text",
  "ar": "النص العربي",
  "de": "Deutscher Text",
  "fr": "Texte français",
  "sw": "Maandishi ya Kiswahili"
}
```

### Status Filtering

**All queries filter by `status_code = 'ACTIVE'`** to ensure only active applications are counted.

### NULL Handling

When foreign keys are NULL or translation data is missing, the system returns:

```json
{
  "en": "Uncategorized",
  "ar": "غير مصنف"
}
```

For unknown/error cases:
```json
{
  "en": "Unknown",
  "ar": "غير معروف"
}
```

---


## Endpoint

### Get Integration Density

**GET** `/analytics/applications/integration-density`

Returns the integration density metric for the application portfolio.

#### Request

No parameters required.

```http
GET /analytics/applications/integration-density HTTP/1.1
Host: localhost:8080
```

#### Response

```json
{
    "integrationDensity": 4.7,
    "totalApplications": 29,
    "totalIntegrations": 136
}
```

#### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `integrationDensity` | Double | Average number of integrations per application (rounded to 1 decimal) |
| `totalApplications` | Long | Total count of active applications in the portfolio |
| `totalIntegrations` | Long | Total count of all integration relationships (both required and utilized) |

---

