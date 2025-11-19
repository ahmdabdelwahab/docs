# Application Analytics API Documentation

## Base URL
```
/analytics/applications
```

---

## Endpoints Overview

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/total-applications` | GET | Get applications count by category |
| `/total-applications/details` | GET | Get paginated list of all applications |
| `/top-vendors` | GET | Get top vendors by application count |
| `/top-vendors/details` | GET | Get applications by specific vendor |
| `/deployment-models` | GET | Get deployment model distribution |
| `/deployment-models/details` | GET | Get applications by deployment model |
| `/support-coverage` | GET | Get support coverage statistics |
| `/support-coverage/details` | GET | Get applications with support contacts |
| `/portfolio-distribution` | GET | Get application portfolio distribution |
| `/portfolio-distribution/apps-drill` | GET | Get applications by portfolio type |
| `/ecosystem-composition` | GET | Get ecosystem composition overview |
| `/ecosystem-composition/details` | GET | Get ecosystem components by type |
| `/distribution-by-attribute` | GET | Get distribution by application attribute |
| `/distribution-by-attribute/details` | GET | Get applications by attribute value |
| `/integration-density` | GET | Get integration density metrics |

---

## Detailed Endpoints

### 1. Total Applications

#### Get Applications List (Drill-down)
```http
GET /analytics/applications/total-applications/details?page=0&size=10
```

**Query Parameters:**
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `page` | integer | No | 0 | Page number (0-indexed) |
| `size` | integer | No | 10 | Number of items per page |

**Response:**
```json
{
    "applications": [
        {
            "id": 60,
            "nameTranslations": {
                "ar": "Bayzat",
                "de": "Bayzat",
                "en": "Bayzat",
                "fr": "Bayzat",
                "sw": "Bayzat"
            },
            "categoryId": null,
            "categoryName": {
                "ar": "غير مصنف",
                "en": "Uncategorized"
            },
            "vendorName": {
                "ar": "آخر",
                "de": "zuletzt",
                "en": "Other",
                "fr": "dernier",
                "sw": "Mwisho"
            },
            "status": "Unknown",
            "deploymentModel": "Unknown"
        },
  ],
  "totalCount": 150,
  "totalPages": 15,
  "currentPage": 0,
  "pageSize": 10
}
```

---

### 2. Top Vendors

#### Get Top Vendors
```http
GET /analytics/applications/top-vendors?limit=10
```

**Query Parameters:**
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `limit` | integer | No | 10 | Number of top vendors to return |

**Response:**
```json
{
    "totalVendors": 10,
    "totalApplications": 29,
    "vendors": [
        {
            "vendorId": null,
            "vendorName": {
                "ar": "غير مصنف",
                "en": "Uncategorized"
            },
            "applicationCount": 9,
            "percentage": 31.03
        },
        {
            "vendorId": "30",
            "vendorName": {
                "ar": "آخر",
                "de": "zuletzt",
                "en": "Other",
                "fr": "dernier",
                "sw": "Mwisho"
            },
            "applicationCount": 6,
            "percentage": 20.69
        },
        {
            "vendorId": "17",
            "vendorName": {
                "ar": "Integrated Systems",
                "de": "Integrierte Systeme",
                "en": "Integrated Systems",
                "fr": "Systèmes intégrés",
                "sw": "Mifumo iliyojumuishwa"
            },
            "applicationCount": 3,
            "percentage": 10.34
        },
        {
            "vendorId": "9",
            "vendorName": {
                "ar": "ساب",
                "de": "Saft",
                "en": "SAP",
                "fr": "Sève",
                "sw": "SAP"
            },
            "applicationCount": 2,
            "percentage": 6.9
        },
        {
            "vendorId": "1",
            "vendorName": {
                "ar": "مايكروسوفت",
                "de": "Microsoft",
                "en": "Microsoft",
                "fr": "Microsoft",
                "sw": "Microsoft"
            },
            "applicationCount": 2,
            "percentage": 6.9
        },
        {
            "vendorId": "2",
            "vendorName": {
                "ar": "أوراكل",
                "de": "Orakel",
                "en": "Oracle",
                "fr": "Oracle",
                "sw": "Oracle"
            },
            "applicationCount": 2,
            "percentage": 6.9
        },
        {
            "vendorId": "3",
            "vendorName": {
                "ar": "إنترناشيونال بزنس ماشينز",
                "de": "Internationale Geschäftsmaschinen",
                "en": "IBM",
                "fr": "Machens internationaux des affaires",
                "sw": "Machens ya Biashara ya Kimataifa"
            },
            "applicationCount": 1,
            "percentage": 3.45
        },
        {
            "vendorId": "19",
            "vendorName": {
                "ar": "Barracuda",
                "de": "Barrakuda",
                "en": "Barracuda",
                "fr": "Barracuda",
                "sw": "Barracuda"
            },
            "applicationCount": 1,
            "percentage": 3.45
        },
        {
            "vendorId": "4",
            "vendorName": {
                "ar": "جوجل",
                "de": "Google",
                "en": "Google",
                "fr": "Google",
                "sw": "Google"
            },
            "applicationCount": 1,
            "percentage": 3.45
        },
        {
            "vendorId": "8",
            "vendorName": {
                "ar": "سيسكو",
                "de": "Cisco",
                "en": "Cisco",
                "fr": "Cisco",
                "sw": "Cisco"
            },
            "applicationCount": 1,
            "percentage": 3.45
        },
        {
            "vendorId": "18",
            "vendorName": {
                "ar": "Paloalto",
                "de": "Paloalto",
                "en": "Paloalto",
                "fr": "Paloalto",
                "sw": "Paloalto"
            },
            "applicationCount": 1,
            "percentage": 3.45
        }
    ]
}
```

#### Get Applications by Vendor (Drill-down)
```http
GET /analytics/applications/top-vendors/details?vendorId=18&page=0&size=10
```

**Query Parameters:**
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `vendorId` | string | Yes | - | Vendor ID |
| `page` | integer | No | 0 | Page number |
| `size` | integer | No | 10 | Items per page |

**Response:** 
```json
{
    "applications": [
        {
            "id": 64,
            "nameTranslations": {
                "ar": "Palo Alto Prisma Cloud",
                "de": "Palo Alto Prisma Cloud",
                "en": "Palo Alto Prisma Cloud",
                "fr": "Palo Alto Prisma Nuage",
                "sw": "Palo Alto Prisma Cloud"
            },
            "categoryId": null,
            "categoryName": {
                "ar": "آخر",
                "de": "zuletzt",
                "en": "Other",
                "fr": "dernier",
                "sw": "Mwisho"
            },
            "vendorName": {
                "ar": "Paloalto",
                "de": "Paloalto",
                "en": "Paloalto",
                "fr": "Paloalto",
                "sw": "Paloalto"
            },
            "status": "Under Review",
            "deploymentModel": "Cloud"
        }
    ],
    "totalCount": 1,
    "totalPages": 1,
    "currentPage": 0,
    "pageSize": 10
}
```
---

### 3. Deployment Models

#### Get Applications by Deployment Model (Drill-down)
```http
GET /analytics/applications/deployment-models/details?modelId=250&page=0&size=10
```

**Query Parameters:**
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `modelId` | string | Yes | - | Deployment model ID |
| `page` | integer | No | 0 | Page number |
| `size` | integer | No | 10 | Items per page |

**Response:** 
```json
{
    "applications": [
        {
            "id": 50,
            "nameTranslations": {
                "ar": "تطبيق EPM",
                "de": "EPM-Anwendung",
                "en": "EPM application",
                "fr": "Application EPM",
                "sw": "Maombi ya EPM"
            },
            "categoryId": null,
            "categoryName": {
                "ar": "Microsoft Dynamics 365",
                "de": "Microsoft Dynamics 365",
                "en": "Microsoft Dynamics 365",
                "fr": "Microsoft Dynamics 365",
                "sw": "Microsoft Dynamics 365"
            },
            "vendorName": {
                "ar": "Integrated Systems",
                "de": "Integrierte Systeme",
                "en": "Integrated Systems",
                "fr": "Systèmes intégrés",
                "sw": "Mifumo iliyojumuishwa"
            },
            "status": "Completed",
            "deploymentModel": "Hybrid"
        },
        {
            "id": 65,
            "nameTranslations": {
                "ar": "GitLab",
                "de": "GitLab",
                "en": "GitLab",
                "fr": "GitLab",
                "sw": "Gitlab"
            },
            "categoryId": null,
            "categoryName": {
                "ar": "آخر",
                "de": "zuletzt",
                "en": "Other",
                "fr": "dernier",
                "sw": "Mwisho"
            },
            "vendorName": {
                "ar": "آخر",
                "de": "zuletzt",
                "en": "Other",
                "fr": "dernier",
                "sw": "Mwisho"
            },
            "status": "Completed",
            "deploymentModel": "Hybrid"
        },
        {
            "id": 54,
            "nameTranslations": {
                "ar": "إيفانتي",
                "de": "Ivanti",
                "en": "Ivanti",
                "fr": "Ivanti",
                "sw": "Ivanti"
            },
            "categoryId": null,
            "categoryName": {
                "ar": "آخر",
                "de": "zuletzt",
                "en": "Other",
                "fr": "dernier",
                "sw": "Mwisho"
            },
            "vendorName": {
                "ar": "Integrated Systems",
                "de": "Integrierte Systeme",
                "en": "Integrated Systems",
                "fr": "Systèmes intégrés",
                "sw": "Mifumo iliyojumuishwa"
            },
            "status": "Unknown",
            "deploymentModel": "Hybrid"
        },
        {
            "id": 58,
            "nameTranslations": {
                "ar": "Odoo ERP",
                "de": "Odoo ERP",
                "en": "Odoo ERP",
                "fr": "Odoo ERP",
                "sw": "ODOO ERP"
            },
            "categoryId": null,
            "categoryName": {
                "ar": "Oracle ERP Cloud",
                "de": "Oracle ERP Cloud",
                "en": "Oracle ERP Cloud",
                "fr": "Cloud Oracle ERP",
                "sw": "Oracle ERP Cloud"
            },
            "vendorName": {
                "ar": "آخر",
                "de": "zuletzt",
                "en": "Other",
                "fr": "dernier",
                "sw": "Mwisho"
            },
            "status": "Approved",
            "deploymentModel": "Hybrid"
        },
        {
            "id": 56,
            "nameTranslations": {
                "ar": "Panorama",
                "de": "Panorama",
                "en": "Panorama",
                "fr": "Panorama",
                "sw": "Panorama"
            },
            "categoryId": null,
            "categoryName": {
                "ar": "Power BI",
                "de": "Power Bi",
                "en": "Power BI",
                "fr": "Power Bi",
                "sw": "Nguvu bi"
            },
            "vendorName": {
                "ar": "أوراكل",
                "de": "Orakel",
                "en": "Oracle",
                "fr": "Oracle",
                "sw": "Oracle"
            },
            "status": "Unknown",
            "deploymentModel": "Hybrid"
        },
        {
            "id": 61,
            "nameTranslations": {
                "ar": "Qlik Sense",
                "de": "Qlik Sense",
                "en": "Qlik Sense",
                "fr": "Qlik Sense",
                "sw": "Qlik akili"
            },
            "categoryId": null,
            "categoryName": {
                "ar": "Power BI",
                "de": "Power Bi",
                "en": "Power BI",
                "fr": "Power Bi",
                "sw": "Nguvu bi"
            },
            "vendorName": {
                "ar": "آخر",
                "de": "zuletzt",
                "en": "Other",
                "fr": "dernier",
                "sw": "Mwisho"
            },
            "status": "Completed",
            "deploymentModel": "Hybrid"
        },
        {
            "id": 59,
            "nameTranslations": {
                "ar": "SAP HCM",
                "de": "SAP HCM",
                "en": "SAP HCM",
                "fr": "SAP HCM",
                "sw": "SAP HCM"
            },
            "categoryId": null,
            "categoryName": {
                "ar": "SAP ERP",
                "de": "SAP ERP",
                "en": "SAP ERP",
                "fr": "SAP ERP",
                "sw": "SAP ERP"
            },
            "vendorName": {
                "ar": "ساب",
                "de": "Saft",
                "en": "SAP",
                "fr": "Sève",
                "sw": "SAP"
            },
            "status": "On Hold",
            "deploymentModel": "Hybrid"
        },
        {
            "id": 46,
            "nameTranslations": {
                "ar": "SAP S/4HANA",
                "de": "SAP S/4HANA",
                "en": "SAP S/4HANA",
                "fr": "SAPS/4HANA",
                "sw": "SAP S/4HANA"
            },
            "categoryId": null,
            "categoryName": {
                "ar": "غير مصنف",
                "en": "Uncategorized"
            },
            "vendorName": {
                "ar": "آخر",
                "de": "zuletzt",
                "en": "Other",
                "fr": "dernier",
                "sw": "Mwisho"
            },
            "status": "Under Review",
            "deploymentModel": "Hybrid"
        }
    ],
    "totalCount": 8,
    "totalPages": 1,
    "currentPage": 0,
    "pageSize": 10
}

```

---

### 4. Support Coverage
#### Get Applications with Support (Drill-down)
```http
GET /analytics/applications/support-coverage/details?page=0&size=10
```

**Query Parameters:**
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `page` | integer | No | 0 | Page number |
| `size` | integer | No | 10 | Items per page |

**Response:** 
```json
{
    "applications": [
        {
            "id": 60,
            "nameTranslations": {
                "ar": "Bayzat",
                "de": "Bayzat",
                "en": "Bayzat",
                "fr": "Bayzat",
                "sw": "Bayzat"
            },
            "categoryName": {
                "ar": "غير مصنف",
                "en": "Uncategorized"
            },
            "vendorName": {
                "ar": "آخر",
                "de": "zuletzt",
                "en": "Other",
                "fr": "dernier",
                "sw": "Mwisho"
            },
            "status": "Unknown",
            "deploymentModel": "Cloud"
        },
        {
            "id": 63,
            "nameTranslations": {
                "ar": "Cisco SecureX",
                "de": "Cisco SecureX",
                "en": "Cisco SecureX",
                "fr": "Cisco SecureX",
                "sw": "Cisco SalamaX"
            },
            "categoryName": {
                "ar": "آخر",
                "de": "zuletzt",
                "en": "Other",
                "fr": "dernier",
                "sw": "Mwisho"
            },
            "vendorName": {
                "ar": "سيسكو",
                "de": "Cisco",
                "en": "Cisco",
                "fr": "Cisco",
                "sw": "Cisco"
            },
            "status": "Completed",
            "deploymentModel": "Cloud"
        },
        {
            "id": 50,
            "nameTranslations": {
                "ar": "تطبيق EPM",
                "de": "EPM-Anwendung",
                "en": "EPM application",
                "fr": "Application EPM",
                "sw": "Maombi ya EPM"
            },
            "categoryName": {
                "ar": "Microsoft Dynamics 365",
                "de": "Microsoft Dynamics 365",
                "en": "Microsoft Dynamics 365",
                "fr": "Microsoft Dynamics 365",
                "sw": "Microsoft Dynamics 365"
            },
            "vendorName": {
                "ar": "Integrated Systems",
                "de": "Integrierte Systeme",
                "en": "Integrated Systems",
                "fr": "Systèmes intégrés",
                "sw": "Mifumo iliyojumuishwa"
            },
            "status": "Completed",
            "deploymentModel": "Hybrid"
        },
        {
            "id": 65,
            "nameTranslations": {
                "ar": "GitLab",
                "de": "GitLab",
                "en": "GitLab",
                "fr": "GitLab",
                "sw": "Gitlab"
            },
            "categoryName": {
                "ar": "آخر",
                "de": "zuletzt",
                "en": "Other",
                "fr": "dernier",
                "sw": "Mwisho"
            },
            "vendorName": {
                "ar": "آخر",
                "de": "zuletzt",
                "en": "Other",
                "fr": "dernier",
                "sw": "Mwisho"
            },
            "status": "Completed",
            "deploymentModel": "Hybrid"
        },
        {
            "id": 54,
            "nameTranslations": {
                "ar": "إيفانتي",
                "de": "Ivanti",
                "en": "Ivanti",
                "fr": "Ivanti",
                "sw": "Ivanti"
            },
            "categoryName": {
                "ar": "آخر",
                "de": "zuletzt",
                "en": "Other",
                "fr": "dernier",
                "sw": "Mwisho"
            },
            "vendorName": {
                "ar": "Integrated Systems",
                "de": "Integrierte Systeme",
                "en": "Integrated Systems",
                "fr": "Systèmes intégrés",
                "sw": "Mifumo iliyojumuishwa"
            },
            "status": "Unknown",
            "deploymentModel": "Hybrid"
        },
        {
            "id": 58,
            "nameTranslations": {
                "ar": "Odoo ERP",
                "de": "Odoo ERP",
                "en": "Odoo ERP",
                "fr": "Odoo ERP",
                "sw": "ODOO ERP"
            },
            "categoryName": {
                "ar": "Oracle ERP Cloud",
                "de": "Oracle ERP Cloud",
                "en": "Oracle ERP Cloud",
                "fr": "Cloud Oracle ERP",
                "sw": "Oracle ERP Cloud"
            },
            "vendorName": {
                "ar": "آخر",
                "de": "zuletzt",
                "en": "Other",
                "fr": "dernier",
                "sw": "Mwisho"
            },
            "status": "Approved",
            "deploymentModel": "Hybrid"
        },
        {
            "id": 64,
            "nameTranslations": {
                "ar": "Palo Alto Prisma Cloud",
                "de": "Palo Alto Prisma Cloud",
                "en": "Palo Alto Prisma Cloud",
                "fr": "Palo Alto Prisma Nuage",
                "sw": "Palo Alto Prisma Cloud"
            },
            "categoryName": {
                "ar": "آخر",
                "de": "zuletzt",
                "en": "Other",
                "fr": "dernier",
                "sw": "Mwisho"
            },
            "vendorName": {
                "ar": "Paloalto",
                "de": "Paloalto",
                "en": "Paloalto",
                "fr": "Paloalto",
                "sw": "Paloalto"
            },
            "status": "Under Review",
            "deploymentModel": "Cloud"
        },
        {
            "id": 56,
            "nameTranslations": {
                "ar": "Panorama",
                "de": "Panorama",
                "en": "Panorama",
                "fr": "Panorama",
                "sw": "Panorama"
            },
            "categoryName": {
                "ar": "Power BI",
                "de": "Power Bi",
                "en": "Power BI",
                "fr": "Power Bi",
                "sw": "Nguvu bi"
            },
            "vendorName": {
                "ar": "أوراكل",
                "de": "Orakel",
                "en": "Oracle",
                "fr": "Oracle",
                "sw": "Oracle"
            },
            "status": "Unknown",
            "deploymentModel": "Hybrid"
        },
        {
            "id": 61,
            "nameTranslations": {
                "ar": "Qlik Sense",
                "de": "Qlik Sense",
                "en": "Qlik Sense",
                "fr": "Qlik Sense",
                "sw": "Qlik akili"
            },
            "categoryName": {
                "ar": "Power BI",
                "de": "Power Bi",
                "en": "Power BI",
                "fr": "Power Bi",
                "sw": "Nguvu bi"
            },
            "vendorName": {
                "ar": "آخر",
                "de": "zuletzt",
                "en": "Other",
                "fr": "dernier",
                "sw": "Mwisho"
            },
            "status": "Completed",
            "deploymentModel": "Hybrid"
        },
        {
            "id": 59,
            "nameTranslations": {
                "ar": "SAP HCM",
                "de": "SAP HCM",
                "en": "SAP HCM",
                "fr": "SAP HCM",
                "sw": "SAP HCM"
            },
            "categoryName": {
                "ar": "SAP ERP",
                "de": "SAP ERP",
                "en": "SAP ERP",
                "fr": "SAP ERP",
                "sw": "SAP ERP"
            },
            "vendorName": {
                "ar": "ساب",
                "de": "Saft",
                "en": "SAP",
                "fr": "Sève",
                "sw": "SAP"
            },
            "status": "On Hold",
            "deploymentModel": "Hybrid"
        }
    ],
    "totalCount": 14,
    "totalPages": 2,
    "currentPage": 0,
    "pageSize": 10
}

```

---

### 6. Ecosystem Composition

#### Get Ecosystem Components by Type (Drill-down)
```http
GET /analytics/applications/ecosystem-composition/details?componentType=enabledServices&applicationId=123&page=0&size=10
```

**Query Parameters:**
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `componentType` | string | Yes | - | Component type (see below) |
| `applicationId` | string | Yes | - | Application ID |
| `page` | integer | No | 0 | Page number |
| `size` | integer | No | 10 | Items per page |

**Valid Component Types:**
- `enabledServices` - Services enabled by this application
- `infrastructure` - Infrastructure components used
- `requiredIntegrations` - Integrations required by application
- `utilizedIntegrations` - Integrations that utilize this application
- `usedLicenses` - Licenses used by application

**Response:**
```json
{
  "components": [
    {
      "componentId": 456,
      "componentName": {
        "en": "Authentication Service",
        "ar": "خدمة المصادقة"
      },
      "componentType": "Service"
    }
  ],
  "totalCount": 5,
  "totalPages": 1,
  "currentPage": 0,
  "pageSize": 10
}
```

---

### 7. Distribution by Attribute
#### Get Applications by Attribute Value (Drill-down)
```http
GET /analytics/applications/distribution-by-attribute/details?attributeType=status&attributeValueId=301&page=0&size=10
```

**Query Parameters:**
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `attributeType` | string | Yes | - | Attribute type: `status`, `deploymentModel`, `authenticationMechanism`, `accessControlMethod`, `applicationSource` |
| `attributeValueId` | string | Yes | - | Attribute value ID (enum ID) |
| `page` | integer | No | 0 | Page number |
| `size` | integer | No | 10 | Items per page |

**Response:** Same as [Applications List Response](#get-applications-list-drill-down)
```json
{
    "applications": [
        {
            "id": 63,
            "nameTranslations": {
                "ar": "Cisco SecureX",
                "de": "Cisco SecureX",
                "en": "Cisco SecureX",
                "fr": "Cisco SecureX",
                "sw": "Cisco SalamaX"
            },
            "categoryId": null,
            "categoryName": {
                "ar": "آخر",
                "de": "zuletzt",
                "en": "Other",
                "fr": "dernier",
                "sw": "Mwisho"
            },
            "vendorName": {
                "ar": "سيسكو",
                "de": "Cisco",
                "en": "Cisco",
                "fr": "Cisco",
                "sw": "Cisco"
            },
            "status": "Completed",
            "deploymentModel": "Cloud"
        },
        {
            "id": 50,
            "nameTranslations": {
                "ar": "تطبيق EPM",
                "de": "EPM-Anwendung",
                "en": "EPM application",
                "fr": "Application EPM",
                "sw": "Maombi ya EPM"
            },
            "categoryId": null,
            "categoryName": {
                "ar": "Microsoft Dynamics 365",
                "de": "Microsoft Dynamics 365",
                "en": "Microsoft Dynamics 365",
                "fr": "Microsoft Dynamics 365",
                "sw": "Microsoft Dynamics 365"
            },
            "vendorName": {
                "ar": "Integrated Systems",
                "de": "Integrierte Systeme",
                "en": "Integrated Systems",
                "fr": "Systèmes intégrés",
                "sw": "Mifumo iliyojumuishwa"
            },
            "status": "Completed",
            "deploymentModel": "Hybrid"
        },
        {
            "id": 65,
            "nameTranslations": {
                "ar": "GitLab",
                "de": "GitLab",
                "en": "GitLab",
                "fr": "GitLab",
                "sw": "Gitlab"
            },
            "categoryId": null,
            "categoryName": {
                "ar": "آخر",
                "de": "zuletzt",
                "en": "Other",
                "fr": "dernier",
                "sw": "Mwisho"
            },
            "vendorName": {
                "ar": "آخر",
                "de": "zuletzt",
                "en": "Other",
                "fr": "dernier",
                "sw": "Mwisho"
            },
            "status": "Completed",
            "deploymentModel": "Hybrid"
        },
        {
            "id": 61,
            "nameTranslations": {
                "ar": "Qlik Sense",
                "de": "Qlik Sense",
                "en": "Qlik Sense",
                "fr": "Qlik Sense",
                "sw": "Qlik akili"
            },
            "categoryId": null,
            "categoryName": {
                "ar": "Power BI",
                "de": "Power Bi",
                "en": "Power BI",
                "fr": "Power Bi",
                "sw": "Nguvu bi"
            },
            "vendorName": {
                "ar": "آخر",
                "de": "zuletzt",
                "en": "Other",
                "fr": "dernier",
                "sw": "Mwisho"
            },
            "status": "Completed",
            "deploymentModel": "Hybrid"
        }
    ],
    "totalCount": 4,
    "totalPages": 1,
    "currentPage": 0,
    "pageSize": 10
}
```

## Common Response Patterns

### Multi-language Support
All name fields support multiple languages:
```json
{
  "en": "English Text",
  "ar": "النص العربي",
  "fr": "Texte Français",
  "de": "Deutscher Text",
  "sw": "Kiswahili Text"
}
```

### Pagination Pattern
All paginated responses follow this structure:
```json
{
  "items": [...],
  "totalCount": 150,
  "totalPages": 15,
  "currentPage": 0,
  "pageSize": 10
}
```

### Error Responses
```json
{
  "timestamp": "2025-11-19T10:30:00",
  "status": 400,
  "error": "Bad Request",
  "message": "Invalid component type",
  "path": "/analytics/applications/ecosystem-composition/details"
}
```

---
