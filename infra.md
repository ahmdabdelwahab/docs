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
    "totalInfrastructure": 21
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
        "vendorName": "Vmware",
        "infrastructureCount": 3
    },
    {
        "vendorName": "Other",
        "infrastructureCount": 3
    },
    {
        "vendorName": "Barracuda",
        "infrastructureCount": 2
    },
    {
        "vendorName": "SAP",
        "infrastructureCount": 2
    },
    {
        "vendorName": "Oracle",
        "infrastructureCount": 2
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
        "rank": 1,
        "categoryName": "Hardware",
        "infrastructureCount": 8
    },
    {
        "rank": 2,
        "categoryName": "Cloud Services",
        "infrastructureCount": 5
    },
    {
        "rank": 3,
        "categoryName": "Networking",
        "infrastructureCount": 2
    },
    {
        "rank": 4,
        "categoryName": "Security",
        "infrastructureCount": 2
    },
    {
        "rank": 5,
        "categoryName": "Software",
        "infrastructureCount": 2
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
    "topUsedApplication": {
        "componentId": "50",
        "componentName": {
            "ar": "تطبيق EPM",
            "de": "EPM-Anwendung",
            "en": "EPM application",
            "fr": "Application EPM",
            "sw": "Maombi ya EPM"
        },
        "usageCount": 4,
        "usagePercentage": 19.05
    },
    "topUsedIntegration": {
        "componentId": "20",
        "componentName": {
            "ar": "تكامل تنبيهات الشبكة والأمن",
            "de": "Integration von Netzwerk- und Sicherheitswarnungen",
            "en": "Network and security alerts integration",
            "fr": "Intégration des alertes réseau et de sécurité",
            "sw": "Ujumuishaji wa Arifa za Mtandao na Usalama"
        },
        "usageCount": 4,
        "usagePercentage": 19.05
    },
    "topUsedLicense": {
        "componentId": "125",
        "componentName": {
            "ar": "اختبار ترخيص قاعدة بيانات أوراكل",
            "de": "Test der Oracle-Datenbanklizenz",
            "en": "Oracle database license test",
            "fr": "Test de licence de base de données Oracle",
            "sw": "Mtihani wa Leseni ya Hifadhidata ya Oracle"
        },
        "usageCount": 4,
        "usagePercentage": 19.05
    }
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
    "totalInfrastructure": 21,
    "categoryDistributions": [
        {
            "categoryId": "1",
            "categoryName": {
                "ar": "الأجهزة",
                "de": "Geräte",
                "en": "Hardware",
                "fr": "Dispositifs",
                "sw": "Vifaa"
            },
            "count": 8,
            "percentage": 38.1
        },
        {
            "categoryId": "5",
            "categoryName": {
                "ar": "الخدمات السحابية",
                "de": "Cloud -Dienste",
                "en": "Cloud Services",
                "fr": "Services cloud",
                "sw": "Huduma za wingu"
            },
            "count": 5,
            "percentage": 23.81
        },
        {
            "categoryId": "2",
            "categoryName": {
                "ar": "البرمجيات",
                "de": "Software",
                "en": "Software",
                "fr": "Logiciel",
                "sw": "Programu"
            },
            "count": 2,
            "percentage": 9.52
        },
        {
            "categoryId": "3",
            "categoryName": {
                "ar": "أمن المعلومات",
                "de": "Informationssicherheit",
                "en": "Security",
                "fr": "Sécurité de l'information",
                "sw": "Usalama wa Habari"
            },
            "count": 2,
            "percentage": 9.52
        },
        {
            "categoryId": "4",
            "categoryName": {
                "ar": "الشبكات",
                "de": "Netzwerke",
                "en": "Networking",
                "fr": "Réseaux",
                "sw": "Mitandao"
            },
            "count": 2,
            "percentage": 9.52
        },
        {
            "categoryId": "0",
            "categoryName": {
                "ar": "غير مصنف",
                "en": "Uncategorized"
            },
            "count": 2,
            "percentage": 9.52
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
GET /analytics/infrastructure/by-category?categoryId=21
```

**Response:**
```json
[
    {
        "infrastructureId": "3",
        "infrastructureName": {
            "ar": "Dell PowerEdge Server",
            "de": "Dell Powerdge Server",
            "en": "Dell PowerEdge Server",
            "fr": "Dell PowerDge Server",
            "sw": "Seva ya Dell Powerdge"
        },
        "model": "PowerEdge FC640",
        "version": null,
        "location": null,
        "vendorName": {
            "en": "Uncategorized",
            "ar": "غير مصنف"
        },
        "categoryName": {
            "ar": "الخوادم",
            "de": "Server",
            "en": "Servers",
            "fr": "Serveurs",
            "sw": "Seva"
        },
        "statusCode": "ACTIVE"
    },
    {
        "infrastructureId": "4",
        "infrastructureName": {
            "ar": "Dell PowerEdge Server",
            "de": "Dell Powerdge Server",
            "en": "Dell PowerEdge Server",
            "fr": "Dell PowerDge Server",
            "sw": "Seva ya Dell Powerdge"
        },
        "model": "PowerEdge FC640",
        "version": null,
        "location": null,
        "vendorName": {
            "en": "Uncategorized",
            "ar": "غير مصنف"
        },
        "categoryName": {
            "ar": "الخوادم",
            "de": "Server",
            "en": "Servers",
            "fr": "Serveurs",
            "sw": "Seva"
        },
        "statusCode": "ACTIVE"
    },
    {
        "infrastructureId": "2",
        "infrastructureName": {
            "ar": "Dell PowerEdge Server",
            "de": "Dell Powerdge Server",
            "en": "Dell PowerEdge Server",
            "fr": "Dell PowerDge Server",
            "sw": "Seva ya Dell Powerdge"
        },
        "model": "PowerEdge FC640",
        "version": null,
        "location": null,
        "vendorName": {
            "ar": "آخر",
            "de": "zuletzt",
            "en": "Other",
            "fr": "dernier",
            "sw": "Mwisho"
        },
        "categoryName": {
            "ar": "الخوادم",
            "de": "Server",
            "en": "Servers",
            "fr": "Serveurs",
            "sw": "Seva"
        },
        "statusCode": "ACTIVE"
    },
    {
        "infrastructureId": "99",
        "infrastructureName": {
            "ar": "Printrer-server",
            "de": "Druckerserver",
            "en": "Printrer-server",
            "fr": "Serveur d'impression",
            "sw": "Printa-seva"
        },
        "model": "PRIMERGY TX1330 M4",
        "version": "6.1",
        "location": "وزارة التنمية الإجتماعية-HQ",
        "vendorName": {
            "ar": "Fujitsu",
            "de": "Fujitsu",
            "en": "Fujitsu",
            "fr": "Fujitsu",
            "sw": "Fujitsu"
        },
        "categoryName": {
            "ar": "الخوادم",
            "de": "Server",
            "en": "Servers",
            "fr": "Serveurs",
            "sw": "Seva"
        },
        "statusCode": "ACTIVE"
    },
    {
        "infrastructureId": "104",
        "infrastructureName": {
            "ar": "خادم حصة",
            "de": "Share-Server",
            "en": "Share server",
            "fr": "Partager le serveur",
            "sw": "Shiriki seva"
        },
        "model": "VMware / Hyper-V",
        "version": "7601",
        "location": "Primary Data Center – HQ",
        "vendorName": {
            "ar": "HP",
            "de": "HP",
            "en": "HP",
            "fr": "HP",
            "sw": "HP"
        },
        "categoryName": {
            "ar": "الخوادم",
            "de": "Server",
            "en": "Servers",
            "fr": "Serveurs",
            "sw": "Seva"
        },
        "statusCode": "ACTIVE"
    },
    {
        "infrastructureId": "102",
        "infrastructureName": {
            "ar": "takaful-db-srv",
            "de": "takaful-db-srv",
            "en": "takaful-db-srv",
            "fr": "takaful-db-srv",
            "sw": "Takaful-db-srv"
        },
        "model": "Oracle 11G",
        "version": "11",
        "location": "Tadafur Data Center – HQ",
        "vendorName": {
            "ar": "OVM",
            "de": "Ovm",
            "en": "OVM",
            "fr": "OVM",
            "sw": "Ovm"
        },
        "categoryName": {
            "ar": "الخوادم",
            "de": "Server",
            "en": "Servers",
            "fr": "Serveurs",
            "sw": "Seva"
        },
        "statusCode": "ACTIVE"
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
        "vendorId": "30",
        "vendorName": {
            "ar": "آخر",
            "de": "zuletzt",
            "en": "Other",
            "fr": "dernier",
            "sw": "Mwisho"
        },
        "infrastructureCount": 3
    },
    {
        "vendorId": "14",
        "vendorName": {
            "ar": "Vmware",
            "de": "VMware",
            "en": "Vmware",
            "fr": "Vmware",
            "sw": "VMware"
        },
        "infrastructureCount": 3
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
        "infrastructureCount": 2
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
        "infrastructureCount": 2
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
        "infrastructureCount": 2
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
        "infrastructureCount": 1
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
        "infrastructureCount": 1
    },
    {
        "vendorId": "20",
        "vendorName": {
            "ar": "CNS",
            "de": "ZNS",
            "en": "CNS",
            "fr": "SNC",
            "sw": "CNS"
        },
        "infrastructureCount": 1
    },
    {
        "vendorId": "21",
        "vendorName": {
            "ar": "Fujitsu",
            "de": "Fujitsu",
            "en": "Fujitsu",
            "fr": "Fujitsu",
            "sw": "Fujitsu"
        },
        "infrastructureCount": 1
    },
    {
        "vendorId": "22",
        "vendorName": {
            "ar": "OVM",
            "de": "Ovm",
            "en": "OVM",
            "fr": "OVM",
            "sw": "Ovm"
        },
        "infrastructureCount": 1
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
        "infrastructureId": "94",
        "infrastructureName": {
            "ar": "WSG",
            "de": "WSG",
            "en": "WSG",
            "fr": "WSG",
            "sw": "Wsg"
        },
        "applicationsCount": 3,
        "integrationsCount": 2,
        "licensesCount": 2,
        "totalComponents": 7
    },
    {
        "infrastructureId": "92",
        "infrastructureName": {
            "ar": "خوادم Microsoft Power BI",
            "de": "Microsoft Power BI-Server",
            "en": "Microsoft Power BI Servers",
            "fr": "Serveurs Microsoft Power BI",
            "sw": "Seva za Microsoft Power BI"
        },
        "applicationsCount": 3,
        "integrationsCount": 1,
        "licensesCount": 3,
        "totalComponents": 7
    },
    {
        "infrastructureId": "89",
        "infrastructureName": {
            "ar": "خوادم Oracle ERP Cloud",
            "de": "Oracle ERP Cloud-Server",
            "en": "Oracle ERP Cloud Servers",
            "fr": "Serveurs cloud Oracle ERP",
            "sw": "Seva za wingu za Oracle ERP"
        },
        "applicationsCount": 2,
        "integrationsCount": 1,
        "licensesCount": 3,
        "totalComponents": 6
    },
    {
        "infrastructureId": "91",
        "infrastructureName": {
            "ar": "خوادم Google Workspace",
            "de": "Google Workspace-Server",
            "en": "Google Workspace servers",
            "fr": "Serveurs Google Workspace",
            "sw": "Seva za Google Workspace"
        },
        "applicationsCount": 2,
        "integrationsCount": 1,
        "licensesCount": 3,
        "totalComponents": 6
    },
    {
        "infrastructureId": "98",
        "infrastructureName": {
            "ar": "جهاز النسخ الاحتياطي",
            "de": "Backup-Gerät",
            "en": "Backup device",
            "fr": "Périphérique de sauvegarde",
            "sw": "Kifaa cha chelezo"
        },
        "applicationsCount": 3,
        "integrationsCount": 2,
        "licensesCount": 1,
        "totalComponents": 6
    },
    {
        "infrastructureId": "103",
        "infrastructureName": {
            "ar": "LBM",
            "de": "LBM",
            "en": "LBM",
            "fr": "LBM",
            "sw": "Lbm"
        },
        "applicationsCount": 1,
        "integrationsCount": 3,
        "licensesCount": 2,
        "totalComponents": 6
    },
    {
        "infrastructureId": "105",
        "infrastructureName": {
            "ar": "eserv-treport-pro-1",
            "de": "eserv-treport-pro-1",
            "en": "eserv-treport-pro-1",
            "fr": "eserv-treport-pro-1",
            "sw": "ESERV-TREPORT-pro-1"
        },
        "applicationsCount": 2,
        "integrationsCount": 3,
        "licensesCount": 1,
        "totalComponents": 6
    },
    {
        "infrastructureId": "104",
        "infrastructureName": {
            "ar": "خادم حصة",
            "de": "Share-Server",
            "en": "Share server",
            "fr": "Partager le serveur",
            "sw": "Shiriki seva"
        },
        "applicationsCount": 2,
        "integrationsCount": 2,
        "licensesCount": 1,
        "totalComponents": 5
    },
    {
        "infrastructureId": "100",
        "infrastructureName": {
            "ar": "EServ-Report-Test",
            "de": "EServ-Report-Test",
            "en": "EServ-Report-Test",
            "fr": "EServ-Rapport-Test",
            "sw": "Mtihani wa EServ-Ripoti"
        },
        "applicationsCount": 1,
        "integrationsCount": 2,
        "licensesCount": 2,
        "totalComponents": 5
    },
    {
        "infrastructureId": "102",
        "infrastructureName": {
            "ar": "takaful-db-srv",
            "de": "takaful-db-srv",
            "en": "takaful-db-srv",
            "fr": "takaful-db-srv",
            "sw": "Takaful-db-srv"
        },
        "applicationsCount": 2,
        "integrationsCount": 3,
        "licensesCount": 0,
        "totalComponents": 5
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
