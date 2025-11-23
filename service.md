# Service Catalog Analytics - Drill-Down Endpoints Guide

This document provides comprehensive documentation for all drill-down endpoints in the Service Catalog Analytics system.

---

## Table of Contents

1. [Overview](#overview)
2. [Card-Based Drill-Downs](#card-based-drill-downs)
   - [Overview Card](#1-overview-card-drill-down)
   - [Digital Maturity Card](#2-digital-maturity-card-drill-down)
   - [Cycle Efficiency Card](#3-cycle-efficiency-card-drill-down)
   - [Reengineering Need Card](#4-reengineering-need-card-drill-down)
3. [Chart-Based Drill-Downs](#chart-based-drill-downs)
   - [Document Distribution (By Document ID)](#5-document-distribution-by-document-id)
   - [Required Documents (By Count)](#6-required-documents-by-document-count)
   - [Frequency Distribution](#7-frequency-distribution-drill-down)
4. [Common Patterns](#common-patterns)
5. [Error Handling](#error-handling)
6. [Performance Guidelines](#performance-guidelines)

---

## Overview

The Service Catalog Analytics system provides two types of drill-down capabilities:

1. **Card-Based Drill-Downs** (`ServiceCardsAnalyticsController`)
   - Overview, Digital Maturity, Cycle Efficiency, Reengineering Need
   - Return generic `ServiceDrillDownDto` with card-specific details
   - Support filtering by card-specific criteria

2. **Chart-Based Drill-Downs** (`ServiceChartsAnalyticsController`)
   - Document Distribution, Frequency Distribution
   - Return specialized DTOs with additional metadata
   - Support multi-dimensional filtering

All endpoints support:
- ✅ Pagination (0-indexed)
- ✅ Sorting (multiple fields, ASC/DESC)
- ✅ Multi-language translations (Map<String, String>)
- ✅ Active services filtering

---

## Card-Based Drill-Downs

### 1. Overview Card Drill-Down

**Purpose**: Lists all active services with overview details including cycle time, frequency, social impact, and economic impact.

#### Endpoint
```
GET /analytics/service-catalog/overview/details
```

#### Parameters
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| page | int | No | 0 | Page number (0-indexed) |
| size | int | No | 20 | Number of items per page |
| sortBy | String | No | id | Sort field: `id`, `name`, `nameEnglish`, `nameArabic`, `cycletime` |
| sortDir | String | No | ASC | Sort direction: `ASC` or `DESC` |

#### Example Request
```bash
curl -X GET "http://localhost:8080/analytics/service-catalog/overview/details
```

#### Response Structure
```json
{
{
    "services": [
        {
            "id": 1,
            "nameTranslations": {
                "ar": "الضمان الاجتماعي و المساعدات الاجتماعية",
                "de": "Soziale Sicherheit und Sozialhilfe",
                "en": "Social Security and Social Assistance",
                "fr": "Sécurité sociale et assistance sociale",
                "sw": "Usalama wa Jamii na Msaada wa Jamii"
            },
            "type": {},
            "socialImpact": null,
            "economicImpact": null,
            "processHasDocumentation": null
        },
        {
            "id": 12,
            "nameTranslations": {
                "ar": " ( ملغى ) المتابعة لخدمات رعاية كبير السن ",
                "de": "(Outlook) Follow -up an die Dienste älterer Menschen",
                "en": "( Cancelled ) Follow-up to elderly care services",
                "fr": "(Outlook) Suivez les services des personnes âgées",
                "sw": "(Outlook) Fuata kwa huduma za wazee"
            },
            "type": {},
            "socialImpact": null,
            "economicImpact": null,
            "processHasDocumentation": null
        },
}
```

#### Use Cases
- View all services in the catalog
- Sort services by name or cycle time
- Identify services with high social/economic impact
- Check documentation status across services

---

### 2. Digital Maturity Card Drill-Down

**Purpose**: Lists services filtered by automation level to analyze digital transformation progress.

#### Endpoint
```
GET /analytics/service-catalog/digital-maturity/details
```

#### Parameters
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| automationLevel | String | No | all | Filter: `fully-digitized`, `manual`, `semi-digital`, `all` |
| page | int | No | 0 | Page number (0-indexed) |
| size | int | No | 20 | Number of items per page |
| sortBy | String | No | id | Sort field: `id`, `name`, `nameEnglish`, `nameArabic` |
| sortDir | String | No | ASC | Sort direction: `ASC` or `DESC` |

#### Automation Level Values
- `fully-digitized` - Fully automated services
- `manual` - Manual services requiring human intervention
- `semi-digital` - Partially automated services
- `all` - No filtering (returns all services)

#### Example Requests
```bash
# Get all fully digitized services
curl -X GET "http://localhost:8080/analytics/service-catalog/digital-maturity/details?automationLevel=fully-digitized"

# Get manual services sorted by name
curl -X GET "http://localhost:8080/analytics/service-catalog/digital-maturity/details?automationLevel=manual&sortBy=name"

# Get all services (no filter)
curl -X GET "http://localhost:8080/analytics/service-catalog/digital-maturity/details"
```

#### Response Structure
```json
{
  "services": [
        },
        {
            "id": 100,
            "nameTranslations": {
                "ar": "طلب تقديم حلقات وورش عمل لعمل الدراسات والتقارير والاحصاءات الدورية ",
                "de": "Bitte einreichen, Episoden und Workshops einzureichen, um Studien, Berichte und regelmäßige Statistiken durchzuführen",
                "en": "Request workshops and workshops",
                "fr": "Demande de soumettre des épisodes et des ateliers pour faire des études, des rapports et des statistiques périodiques",
                "sw": "Omba kupeana vipindi na semina za kufanya masomo, ripoti na takwimu za mara kwa mara"
            },
            "automationLevel": {
                "ar": "رقمنة جزئية",
                "de": "Partialdigitalisierung",
                "en": "Semi Digitalization",
                "fr": "Numérisation partielle",
                "sw": "Digitization ya sehemu"
            },
            "type": {
                "ar": "طلب جديد",
                "de": "Neue Anfrage",
                "en": "New Application",
                "fr": "Nouvelle demande",
                "sw": "Ombi mpya"
            },
            "category": {
                "ar": "الحماية الاجتماعية والرعاية الاجتماعية (الأسرة، رعاية الأطفال، تربية الأطفال، الأشخاص ذوي الإعاقة، رعاية المسنين)",
                "de": "Sozialschutz und soziale Wohlbefinden (Familie, Kinderbetreuung, Kindererziehung, Menschen mit Behinderungen, ältere Pflege)",
                "en": "Social Protection And Social Care (Family, Childcare, Parenting, Disabled People, Elderly Care)",
                "fr": "Protection sociale et protection sociale (famille, garde d'enfants, éducation des enfants, personnes handicapées, soins aux personnes âgées)",
                "sw": "Ulinzi wa Jamii na Ustawi wa Jamii (Familia, Huduma ya Watoto, Masomo ya watoto, Watu wenye Ulemavu, Utunzaji wa Wazee)"
            }
        }
    ],
  ],
  "pagination": {
    "totalCount": 45,
    "totalPages": 3,
    "currentPage": 0
  }
}
```

#### Use Cases
- Identify services ready for automation
- Track digital transformation progress
- Find manual services requiring digitization
- Analyze integration patterns by automation level

---

### 3. Cycle Efficiency Card Drill-Down

**Purpose**: Lists services filtered by cycle time duration to identify efficiency bottlenecks.

#### Endpoint
```
GET /analytics/service-catalog/cycle-efficiency/details
```

#### Parameters
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| timeRange | String | No | all | Filter: `less-than-3-days`, `3-to-14-days`, `more-than-2-weeks`, `all` |
| page | int | No | 0 | Page number (0-indexed) |
| size | int | No | 20 | Number of items per page |
| sortBy | String | No | id | Sort field: `id`, `name`, `nameEnglish`, `nameArabic`, `cycletime` |
| sortDir | String | No | ASC | Sort direction: `ASC` or `DESC` |

#### Time Range Values
- `less-than-3-days` - Fast services (< 3 days)
- `3-to-14-days` - Medium duration services (3-14 days)
- `more-than-2-weeks` - Slow services (> 14 days)
- `all` - No filtering (returns all services with cycle time data)

#### Example Requests
```bash
# Get fast services (< 3 days)
curl -X GET "http://localhost:8080/analytics/service-catalog/cycle-efficiency/details?timeRange=less-than-3-days"

# Get slow services sorted by cycle time descending
curl -X GET "http://localhost:8080/analytics/service-catalog/cycle-efficiency/details?timeRange=more-than-2-weeks&sortBy=cycletime&sortDir=DESC"
```

#### Response Structure
```json
{
    "services": [
        {
            "id": 45,
            "nameTranslations": {
                "ar": "خدمة إرشاد وتدريب للأسر في المنزل",
                "de": "Anleitung und Schulungsservice für Familien zu Hause",
                "en": "Guidance and training for families at home",
                "fr": "Service d'orientation et de formation pour les familles à la maison",
                "sw": "Miongozo na huduma ya mafunzo kwa familia nyumbani"
            },
            "type": {
                "ar": "طلب جديد",
                "de": "Neue Anfrage",
                "en": "New Application",
                "fr": "Nouvelle demande",
                "sw": "Ombi mpya"
            },
            "cycleTimeDays": 2.04,
            "frequency": "Monthly"
        },
  ],
  "pagination": {
    "totalCount": 89,
    "totalPages": 5,
    "currentPage": 0
  }
}
```

#### Use Cases
- Identify bottleneck services requiring process improvement
- Find fast-track services for benchmarking
- Analyze cycle time patterns by service type
- Prioritize reengineering efforts

---

### 4. Reengineering Need Card Drill-Down

**Purpose**: Lists services filtered by process documentation status to support reengineering initiatives.

#### Endpoint
```
GET /analytics/service-catalog/reengineering-need/details
```

#### Parameters
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| documented | Boolean | No | null | Filter: `true` (documented), `false` (not documented), `null` (all) |
| page | int | No | 0 | Page number (0-indexed) |
| size | int | No | 20 | Number of items per page |
| sortBy | String | No | id | Sort field: `id`, `name`, `nameEnglish`, `nameArabic` |
| sortDir | String | No | ASC | Sort direction: `ASC` or `DESC` |

#### Documentation Filter Values
- `true` - Services with process documentation
- `false` - Services without process documentation
- `null` or omitted - All services (no filter)

#### Example Requests
```bash
# Get documented services
curl -X GET "http://localhost:8080/analytics/service-catalog/reengineering-need/details?documented=true"

# Get undocumented services (requiring documentation)
curl -X GET "http://localhost:8080/analytics/service-catalog/reengineering-need/details?documented=false"

# Get all services
curl -X GET "http://localhost:8080/analytics/service-catalog/reengineering-need/details"
```

#### Response Structure
```json
{
  "services": [
    {
      "id": 1,
      "nameTranslations": {
        "en": "Service Name",
        "ar": "اسم الخدمة"
      },
      "type": {
        "en": "Type Name",
        "ar": "نوع الخدمة"
      },
      "category": {
        "en": "Category Name",
        "ar": "فئة الخدمة"
      },
      "reengineeringRequired": true,
      "processHasDocumentation": true
    }
  ],
  "pagination": {
    "totalCount": 62,
    "totalPages": 4,
    "currentPage": 0
  }
}
```

#### Use Cases
- Identify services requiring documentation
- Prioritize documentation efforts
- Track documentation completion progress
- Correlate documentation with reengineering needs

---

## Chart-Based Drill-Downs

### 5. Document Distribution (By Document ID)

**Purpose**: Lists all services that require a specific supporting document.

#### Endpoint
```
GET /analytics/service-catalog/document-distribution/details
```

#### Parameters
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| documentId | Long | **Yes** | - | The ID of the document to filter by |
| page | int | No | 0 | Page number (0-indexed) |
| size | int | No | 20 | Number of items per page |
| sortBy | String | No | id | Sort field: `id`, `name`, `nameEnglish`, `nameArabic` |
| sortDir | String | No | ASC | Sort direction: `ASC` or `DESC` |

#### Example Request
```bash
curl -X GET "http://localhost:8080/analytics/service-catalog/document-distribution/details?documentId=123&page=0&size=20"
```

#### Response Structure
```json
{
  "documentId": 123,
  "documentNameTranslations": {
    "en": "National ID Card",
    "ar": "بطاقة الهوية الوطنية"
  },
  "totalServices": 45,
  "services": [
    {
      "id": 1,
      "nameTranslations": {
        "en": "Service Name",
        "ar": "اسم الخدمة"
      },
      "type": {
        "en": "Type Name",
        "ar": "نوع الخدمة"
      },
      "category": {
        "en": "Category Name",
        "ar": "فئة الخدمة"
      },
      "status": "ACTIVE"
    }
  ],
  "pagination": {
    "totalCount": 45,
    "totalPages": 3,
    "currentPage": 0
  }
}
```

#### Use Cases
- Analyze document usage across services
- Identify services affected by document policy changes
- Consolidate similar document requirements
- Simplify citizen document submission

---

### 6. Required Documents (By Document Count)

**Purpose**: Lists services that require exactly N supporting documents.

#### Endpoint
```
GET /analytics/service-catalog/required-documents/by-count
```

#### Parameters
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| documentCount | Integer | **Yes** | - | Number of documents required (0, 1, 2, 3, ...) |
| page | int | No | 0 | Page number (0-indexed) |
| size | int | No | 20 | Number of items per page |
| sortBy | String | No | id | Sort field: `id`, `name`, `nameEnglish`, `nameArabic` |
| sortDir | String | No | ASC | Sort direction: `ASC` or `DESC` |

#### Example Requests
```bash
# Services with no document requirements
curl -X GET "http://localhost:8080/analytics/service-catalog/required-documents/by-count?documentCount=0"

# Services requiring exactly 2 documents
curl -X GET "http://localhost:8080/analytics/service-catalog/required-documents/by-count?documentCount=2"

# Services requiring many documents (sorted by name)
curl -X GET "http://localhost:8080/analytics/service-catalog/required-documents/by-count?documentCount=5&sortBy=name"
```

#### Response Structure
```json
{
  "documentCount": 2,
  "totalServices": 28,
  "services": [
    {
      "id": 1,
      "nameTranslations": {
        "en": "Service Name",
        "ar": "اسم الخدمة"
      },
      "type": {
        "en": "Type Name",
        "ar": "نوع الخدمة"
      },
      "category": {
        "en": "Category Name",
        "ar": "فئة الخدمة"
      },
      "status": "ACTIVE"
    }
  ],
  "pagination": {
    "totalCount": 28,
    "totalPages": 2,
    "currentPage": 0
  }
}
```

#### Use Cases
- Identify services with low/high document burden
- Simplify services with excessive requirements
- Benchmark document requirements
- Track document reduction initiatives

---

### 7. Frequency Distribution Drill-Down

**Purpose**: Lists services filtered by both frequency category and cycle time duration for granular efficiency analysis.

#### Endpoint
```
GET /analytics/service-catalog/frequency-distribution/details
```

#### Parameters
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| frequency | String | **Yes** | - | Frequency: `Daily`, `Monthly`, `Annually`, `Seasonally` |
| durationRange | String | **Yes** | - | Duration range (see below) |
| page | int | No | 0 | Page number (0-indexed) |
| size | int | No | 20 | Number of items per page |
| sortBy | String | No | id | Sort field: `id`, `name`, `nameEnglish`, `nameArabic`, `cycletime`, `frequency` |
| sortDir | String | No | ASC | Sort direction: `ASC` or `DESC` |

#### Duration Range Values
| Value | Description | Cycle Time Condition |
|-------|-------------|---------------------|
| `lessThan1Day` | Very fast | < 1 day |
| `oneToFiveDays` | Fast | 1-5 days |
| `threeToTenDays` | Medium | 3-10 days |
| `oneToFourWeeks` | Slow | 7-28 days |
| `fourPlusWeeks` | Very slow | > 28 days |

**⚠️ Important Note**: Duration ranges are intentionally **overlapping** to match chart aggregation logic. A service with 3 days cycle time will appear in both `oneToFiveDays` and `threeToTenDays` queries.

#### Frequency Values
- `Daily` - Services processed every day
- `Monthly` - Services processed monthly
- `Annually` - Services processed once per year
- `Seasonally` - Services with seasonal processing

#### Example Requests
```bash
# Fast daily services (< 1 day)
curl -X GET "http://localhost:8080/analytics/service-catalog/frequency-distribution/details?frequency=Daily&durationRange=lessThan1Day"

# Monthly services with medium duration (3-10 days)
curl -X GET "http://localhost:8080/analytics/service-catalog/frequency-distribution/details?frequency=Monthly&durationRange=threeToTenDays"

# Annual services taking more than 4 weeks
curl -X GET "http://localhost:8080/analytics/service-catalog/frequency-distribution/details?frequency=Annually&durationRange=fourPlusWeeks&sortBy=cycletime&sortDir=DESC"
```

#### Response Structure
```json
{
  "frequencyName": "Daily",
  "durationRange": "lessThan1Day",
  "totalServices": 73,
  "services": [
    {
      "id": 1,
      "nameTranslations": {
        "en": "Service Name",
        "ar": "اسم الخدمة"
      },
      "type": {
        "en": "Type Name",
        "ar": "نوع الخدمة"
      },
      "category": {
        "en": "Category Name",
        "ar": "فئة الخدمة"
      },
      "frequency": {
        "en": "Daily",
        "ar": "يومي"
      },
      "cycleTimeDays": 0.5,
      "status": "ACTIVE"
    }
  ],
  "pagination": {
    "totalCount": 73,
    "totalPages": 4,
    "currentPage": 0
  }
}
```

#### Use Cases
- Analyze efficiency patterns by frequency
- Identify slow daily services requiring optimization
- Benchmark cycle times within frequency categories
- Track SLA compliance for different service frequencies

---

## Common Patterns

### Translation Maps

All text fields that support multiple languages are returned as `Map<String, String>`:

```json
{
  "nameTranslations": {
    "en": "English Name",
    "ar": "الاسم العربي",
    "fr": "Nom français",
    "de": "Deutscher Name"
  }
}
```

**Accessing translations in your application:**
```javascript
// JavaScript/TypeScript
const englishName = service.nameTranslations.en;
const arabicName = service.nameTranslations.ar;

// Java
String englishName = service.getNameTranslations().get("en");
String arabicName = service.getNameTranslations().get("ar");
```

### Pagination Structure

All endpoints return consistent pagination metadata:

```json
{
  "pagination": {
    "totalCount": 100,    // Total number of items
    "totalPages": 5,      // Total number of pages
    "currentPage": 0      // Current page (0-indexed)
  }
}
```

**Pagination calculations:**
```
totalPages = ceil(totalCount / size)
hasNextPage = currentPage < (totalPages - 1)
hasPreviousPage = currentPage > 0
```

### Sort Fields

Common sort field mappings across endpoints:

| Sort Parameter | Maps To | Description |
|---------------|---------|-------------|
| `id` | `s.id` or `cd.id` | Service ID (numeric) |
| `name` | `s.name_translations->>'en'` | English name (alphabetical) |
| `nameEnglish` | `s.name_translations->>'en'` | English name (explicit) |
| `nameArabic` | `s.name_translations->>'ar'` | Arabic name (alphabetical) |
| `cycletime` | `cycle_days` or `s.cycletime` | Cycle time in days (numeric) |
| `frequency` | `e_freq.name_translations->>'en'` | Frequency name (alphabetical) |

**Invalid sort fields default to `id`**.

### Status Filtering

**All drill-down endpoints filter by `status_code = 'ACTIVE'`** to ensure consistency with chart aggregations. Inactive, draft, or archived services are excluded from results.

To include all statuses (if needed in future), the filter would need to be removed or made configurable.

---

### Handling Empty Results

Endpoints return empty lists (not errors) when no data matches filters:

```json
{
  "documentCount": 99,
  "totalServices": 0,
  "services": [],
  "pagination": {
    "totalCount": 0,
    "totalPages": 0,
    "currentPage": 0
  }
}
```
