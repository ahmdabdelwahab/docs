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

**Endpoint:** `GET /analytics/applications/portfolio-distribution/applications`

**Query Parameters:**
- `portfolioTypeId` (optional): The root category ID. Pass `null` or omit for uncategorized applications.

**Example Request:**
```
GET /analytics/applications/portfolio-distribution/applications?portfolioTypeId=1
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

## Database Schema

### Main Tables

- **sam_application**: Main application table
  - `id`: Primary key
  - `name_translations`: JSONB application name
  - `application_category_id`: FK to application_category
  - `vendor_id`: FK to sam_vendor
  - `owner_id`: FK to authority
  - `deployment_model`: FK to enums
  - `status_code`: Application status ('ACTIVE', 'INACTIVE', etc.)
  - `version`: Application version
  - `support_contact_name`: Support contact name
  - `support_contact_email`: Support email
  - `support_contact_phone`: Support phone

- **application_category**: Hierarchical category structure
  - `id`: Primary key
  - `parent_id`: Self-referencing FK for hierarchy
  - `name_translations`: JSONB category name
  - `status_code`: Category status

- **sam_vendor**: Vendor master data
  - `id`: Primary key
  - `name_translations`: JSONB vendor name

- **authority**: Organization/department master data
  - `id`: Primary key
  - `name_translations`: JSONB authority name

- **enums**: System enumerations
  - `id`: Primary key
  - `enum_type`: Type of enum (e.g., 'Deployment Models')
  - `name_translations`: JSONB enum value name

### Junction Tables (Many-to-Many)

- **sam_application_services**: Links applications to services
- **sam_application_infrastructure**: Links applications to infrastructure
- **sam_application_integrations**: Links applications to required integrations
- **sam_integration_utilizedapplication**: Links applications to consumed integrations
- **sam_application_licenses**: Links applications to licenses

---

## Performance Considerations

### Query Complexity

| Endpoint | Complexity | Notes |
|----------|-----------|-------|
| Total Applications | O(n) | Simple aggregation |
| Top Vendors | O(n) | GROUP BY with LIMIT 10 |
| Deployment Models | O(n) | Simple GROUP BY |
| Support Coverage | O(n) | Single scan with FILTER |
| Portfolio Distribution | O(n × log n) | Recursive CTE + aggregation |
| Applications by Type | O(n × log n) | Recursive CTE + sorting |
| Ecosystem Composition | O(n × m) | 5 LEFT JOINs with aggregation |
| Technology Vendors | O(n) | GROUP BY all vendors |
| Distribution by Attribute | O(n) | GROUP BY with enum join |

### Recommended Indexes

```sql
-- Critical indexes for performance
CREATE INDEX idx_sam_application_status 
  ON sam_application(status_code);

CREATE INDEX idx_sam_application_category 
  ON sam_application(application_category_id) 
  WHERE status_code = 'ACTIVE';

CREATE INDEX idx_sam_application_vendor 
  ON sam_application(vendor_id) 
  WHERE status_code = 'ACTIVE';

-- For hierarchical queries
CREATE INDEX idx_category_parent 
  ON application_category(parent_id);

-- For ecosystem composition
CREATE INDEX idx_app_services 
  ON sam_application_services(application_id);

CREATE INDEX idx_app_infrastructure 
  ON sam_application_infrastructure(application_id);

CREATE INDEX idx_app_integrations 
  ON sam_application_integrations(application_id);

CREATE INDEX idx_app_licenses 
  ON sam_application_licenses(application_id);

-- For JSONB sorting
CREATE INDEX idx_app_name_en 
  ON sam_application((name_translations->>'en'));
```

---

## Error Handling

### Common HTTP Status Codes

- `200 OK`: Successful request
- `400 Bad Request`: Invalid parameters
- `401 Unauthorized`: Missing or invalid authentication
- `403 Forbidden`: Insufficient permissions
- `500 Internal Server Error`: Server-side error

### Empty Results

When no data is found, endpoints return empty arrays with zero counts:

```json
{
  "totalApplications": 0,
  "categoryBreakdown": []
}
```

---

## Use Cases

### 1. Portfolio Management Dashboard

Use these endpoints to build a comprehensive dashboard:
- Total Applications by Category (pie chart)
- Top Vendors (bar chart)
- Deployment Model Distribution (donut chart)
- Support Coverage (gauge)

### 2. Application Discovery

Use Portfolio Distribution → Applications by Portfolio Type for drill-down navigation:
1. Show high-level categories
2. Click to see detailed applications
3. View individual application details

### 3. Ecosystem Mapping

Use Ecosystem Composition to:
- Identify highly interconnected applications
- Find applications with no dependencies
- Plan decommissioning based on dependency impact

### 4. Vendor Analysis

Use Top Vendors + Technology Vendors to:
- Identify vendor concentration risks
- Plan vendor consolidation
- Track vendor relationships

### 5. Compliance Reporting

Use Distribution by Attribute to:
- Track deployment model compliance (cloud vs on-premise)
- Monitor authentication mechanism adoption
- Report on access control methods

---

## Examples

### Building a Portfolio Dashboard

```javascript
// Fetch overview metrics
const totalApps = await fetch('/analytics/applications/total-applications');
const topVendors = await fetch('/analytics/applications/top-vendors');
const deployment = await fetch('/analytics/applications/deployment-models');
const support = await fetch('/analytics/applications/support-coverage');

// Fetch portfolio distribution for navigation
const portfolio = await fetch('/analytics/applications/portfolio-distribution');

// When user clicks a portfolio type, fetch detailed applications
const apps = await fetch(
  `/analytics/applications/portfolio-distribution/applications?portfolioTypeId=${portfolioId}`
);
```

### Finding Uncategorized Applications

```javascript
// Get uncategorized applications
const uncategorized = await fetch(
  '/analytics/applications/portfolio-distribution/applications?portfolioTypeId=null'
);

console.log(`Found ${uncategorized.totalApplications} uncategorized applications`);
```

### Analyzing Application Ecosystem

```javascript
// Get all applications with their ecosystem
const ecosystem = await fetch('/analytics/applications/ecosystem-composition');

// Find applications with no dependencies
const standalone = ecosystem.applications.filter(app => app.totalComponents === 0);

// Find highly interconnected applications
const critical = ecosystem.applications
  .filter(app => app.totalComponents > 50)
  .sort((a, b) => b.totalComponents - a.totalComponents);
```

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2025-11-09 | Initial release with 9 endpoints |

---

## Support

For issues or questions, contact the platform team or refer to the main application documentation.
