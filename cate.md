# Infrastructure Portfolio Drill-Down API Documentation

## Overview

This API provides a three-level hierarchical drill-down navigation for infrastructure portfolio analysis. Users can navigate from root categories down to individual infrastructure items through their subcategories.

## Navigation Flow

```
┌─────────────────────────────────────────────────────────────┐
│  Level 1: Root Categories                                   │
│  GET /analytics/infrastructure/categories                   │
│  Example: Hardware, Software, Security, Cloud Services      │
└──────────────────────┬──────────────────────────────────────┘
                       │ Click on category
                       ↓
┌─────────────────────────────────────────────────────────────┐
│  Level 2: Subcategories                                     │
│  GET /analytics/infrastructure/categories/class             │
│  Example: Servers, Storage, Networking (under Hardware)     │
└──────────────────────┬──────────────────────────────────────┘
                       │ Click on subcategory
                       ↓
┌─────────────────────────────────────────────────────────────┐
│  Level 3: Infrastructure Products                           │
│  GET /analytics/infrastructure/categories/class/product     │
│  Example: Dell PowerEdge R740, HP ProLiant DL380, etc.      │
└─────────────────────────────────────────────────────────────┘
```

---

## Endpoints

### 1. Get Root Categories Distribution

**GET** `/analytics/infrastructure/categories`

Returns the distribution of infrastructure across root-level categories.

#### Response

```json
{
    "totalInfrastructure": 457,
    "categoryDistributions": [
        {
            "categoryId": "21",
            "categoryName": {
                "en": "Security",
                "ar": "الأمن",
                "de": "Sicherheit",
                "fr": "Sécurité",
                "sw": "Usalama"
            },
            "count": 100,
            "percentage": 21.86
        },
        {
            "categoryId": "1",
            "categoryName": {
                "en": "Hardware",
                "ar": "الأجهزة",
                "de": "Geräte",
                "fr": "Dispositifs",
                "sw": "Vifaa"
            },
            "count": 84,
            "percentage": 18.38
        }
    ]
}
```

#### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `totalInfrastructure` | Long | Total count of active infrastructure items |
| `categoryDistributions` | Array | List of root category distributions |
| `categoryId` | String | Unique identifier for the category |
| `categoryName` | Map | Multilingual category name (en, ar, de, fr, sw) |
| `count` | Long | Number of infrastructure items in this category |
| `percentage` | Double | Percentage of total infrastructure (rounded to 2 decimals) |

#### Business Logic

- Uses **recursive CTE** to traverse from infrastructure's assigned category UP to root category
- Root categories are identified by `parent_id IS NULL`
- Includes infrastructure with no category as "Uncategorized" (categoryId = "0")
- Only counts infrastructure with `status_code = 'ACTIVE'`
- Percentages are calculated as: `(count / totalInfrastructure) * 100`

---

### 2. Get Subcategories by Category

**GET** `/analytics/infrastructure/categories/class?categoryId={id}`

Returns the direct subcategories of a selected root category, along with infrastructure counts.

#### Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `categoryId` | String | Yes | ID of the parent category to drill down into |

#### Example Request

```
GET /analytics/infrastructure/categories/class?categoryId=1
```

#### Response

```json
{
    "categoryId": "1",
    "categoryName": {
        "ar": "الأجهزة",
        "de": "Geräte",
        "en": "Hardware",
        "fr": "Dispositifs",
        "sw": "Vifaa"
    },
    "totalInfrastructureCount": 8,
    "subcategoriesCount": 6,
    "subcategories": [
        {
            "subcategoryId": "20",
            "subcategoryName": {
                "ar": "الخوادم",
                "de": "Server",
                "en": "Servers",
                "fr": "Serveurs",
                "sw": "Seva"
            },
            "infrastructureCount": 6,
            "percentage": 75.0
        },
        {
            "subcategoryId": "30",
            "subcategoryName": {
                "ar": "أجهزة التخزين",
                "de": "Speichergeräte",
                "en": "Storage Devices",
                "fr": "Dispositifs de stockage",
                "sw": "Vifaa vya kuhifadhi"
            },
            "infrastructureCount": 1,
            "percentage": 12.5
        },
        {
            "subcategoryId": "40",
            "subcategoryName": {
                "ar": "معدات الشبكات",
                "de": "Netzwerkausrüstung",
                "en": "Networking Equipment",
                "fr": "Équipement réseau",
                "sw": "Vifaa vya mtandao"
            },
            "infrastructureCount": 1,
            "percentage": 12.5
        },
        {
            "subcategoryId": "50",
            "subcategoryName": {
                "ar": "معدات مركز البيانات",
                "de": "Rechenzentrumsgeräte",
                "en": "Data Center Equipment",
                "fr": "Équipement de centre de données",
                "sw": "Vifaa vya kituo cha data"
            },
            "infrastructureCount": 0,
            "percentage": 0.0
        },
        {
            "subcategoryId": "56",
            "subcategoryName": {
                "ar": "Security measures",
                "de": "Sicherheitsmessungen",
                "en": "Security measures",
                "fr": "Mesures de sécurité",
                "sw": "Vipimo vya usalama"
            },
            "infrastructureCount": 0,
            "percentage": 0.0
        },
        {
            "subcategoryId": "60",
            "subcategoryName": {
                "ar": "آخر",
                "de": "zuletzt",
                "en": "Other",
                "fr": "dernier",
                "sw": "Mwisho"
            },
            "infrastructureCount": 0,
            "percentage": 0.0
        }
    ]
}
```

#### Response Fields

**Parent Category Information:**

| Field | Type | Description |
|-------|------|-------------|
| `categoryId` | String | ID of the parent category |
| `categoryName` | Map | Multilingual name of the parent category |
| `totalInfrastructureCount` | Long | Total infrastructure count under this category (including all descendants) |
| `subcategoriesCount` | Integer | Number of direct subcategories |

**Subcategory Information:**

| Field | Type | Description |
|-------|------|-------------|
| `subcategoryId` | String | Unique identifier for the subcategory |
| `subcategoryName` | Map | Multilingual subcategory name |
| `infrastructureCount` | Long | Infrastructure count in this subcategory AND all its descendants |
| `percentage` | Double | Percentage relative to parent category's total |

#### Business Logic

- Fetches parent category information from `infrastructure_category` table
- Uses **recursive CTE** to:
  1. Get direct children (WHERE `parent_id = :categoryId`)
  2. Recursively traverse down to all descendants
  3. Track which direct child each descendant belongs to
- Infrastructure count includes:
  - Items directly assigned to the subcategory
  - Items assigned to any descendant category
- Percentages calculated relative to parent's total: `(subcategoryCount / totalInfrastructureCount) * 100`
- Returns empty result with error handling if category not found

---

### 3. Get Infrastructure Products by Category

**GET** `/analytics/infrastructure/categories/class/product?categoryId={id}`

Returns detailed information about all infrastructure items within a category and its descendants.

#### Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `categoryId` | String | Yes | ID of the category (can be root, subcategory, or leaf) |

#### Example Request

```
GET /analytics/infrastructure/categories/class/product?categoryId=21
```

#### Response

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

#### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `infrastructureId` | String | Unique identifier for the infrastructure item |
| `infrastructureName` | Map | Multilingual infrastructure name |
| `model` | String | Model number or identifier |
| `version` | String | Version or generation |
| `location` | String | Physical or logical location |
| `vendorName` | Map | Multilingual vendor/manufacturer name |
| `categoryName` | Map | Multilingual category name (actual assigned category) |
| `statusCode` | String | Status of the infrastructure (always "ACTIVE" in results) |

#### Business Logic

- Uses **recursive CTE** to:
  1. Start with the selected category
  2. Recursively get all child categories (descendants)
  3. Build a complete category tree
- Returns infrastructure where `infrastructure_category_id` is in the category tree
- **LEFT JOIN** on `sam_vendor` to handle infrastructure without assigned vendor
- Filters only `status_code = 'ACTIVE'` infrastructure
- Sorted alphabetically by infrastructure name (English)
- Works for ANY category level:
  - **Root category**: Returns all infrastructure in entire tree
  - **Subcategory**: Returns infrastructure in subcategory + descendants
  - **Leaf category**: Returns infrastructure directly assigned to it

---
