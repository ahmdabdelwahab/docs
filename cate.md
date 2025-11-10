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
        "en": "Hardware",
        "ar": "الأجهزة",
        "de": "Geräte",
        "fr": "Dispositifs",
        "sw": "Vifaa"
    },
    "totalInfrastructureCount": 84,
    "subcategoriesCount": 6,
    "subcategories": [
        {
            "subcategoryId": "20",
            "subcategoryName": {
                "en": "Servers",
                "ar": "الخوادم",
                "de": "Server",
                "fr": "Serveurs",
                "sw": "Seva"
            },
            "infrastructureCount": 50,
            "percentage": 59.52
        },
        {
            "subcategoryId": "30",
            "subcategoryName": {
                "en": "Storage Devices",
                "ar": "أجهزة التخزين",
                "de": "Speichergeräte",
                "fr": "Dispositifs de stockage",
                "sw": "Vifaa vya kuhifadhi"
            },
            "infrastructureCount": 20,
            "percentage": 23.81
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
GET /analytics/infrastructure/categories/class/product?categoryId=20
```

#### Response

```json
[
    {
        "infrastructureId": "145",
        "infrastructureName": {
            "en": "Dell PowerEdge R740",
            "ar": "ديل باور ايدج R740",
            "de": "Dell PowerEdge R740",
            "fr": "Dell PowerEdge R740",
            "sw": "Dell PowerEdge R740"
        },
        "model": "R740",
        "version": "Gen 14",
        "location": "Data Center A - Rack 5",
        "vendorName": {
            "en": "Dell Technologies",
            "ar": "ديل تكنولوجيز",
            "de": "Dell Technologies",
            "fr": "Dell Technologies",
            "sw": "Dell Technologies"
        },
        "categoryName": {
            "en": "Physical Servers",
            "ar": "الخوادم الفعلية",
            "de": "Physische Server",
            "fr": "Serveurs physiques",
            "sw": "Seva halisi"
        },
        "statusCode": "ACTIVE"
    },
    {
        "infrastructureId": "146",
        "infrastructureName": {
            "en": "HP ProLiant DL380 Gen10",
            "ar": "اتش بي برولينت DL380 الجيل 10",
            "de": "HP ProLiant DL380 Gen10",
            "fr": "HP ProLiant DL380 Gen10",
            "sw": "HP ProLiant DL380 Gen10"
        },
        "model": "DL380",
        "version": "Gen10",
        "location": "Data Center B - Rack 12",
        "vendorName": {
            "en": "Hewlett Packard Enterprise",
            "ar": "هيوليت باكارد انتربرايز",
            "de": "Hewlett Packard Enterprise",
            "fr": "Hewlett Packard Enterprise",
            "sw": "Hewlett Packard Enterprise"
        },
        "categoryName": {
            "en": "Physical Servers",
            "ar": "الخوادم الفعلية",
            "de": "Physische Server",
            "fr": "Serveurs physiques",
            "sw": "Seva halisi"
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

## SQL Query Patterns

### 1. Root Categories Query Pattern

```sql
WITH RECURSIVE category_hierarchy AS (
    -- Start with infrastructure and their categories
    SELECT i.id as infrastructure_id, ic.id as category_id, ic.parent_id
    FROM sam_infrastructure i
    INNER JOIN infrastructure_category ic ON i.infrastructure_category_id = ic.id
    WHERE i.status_code = 'ACTIVE'
    
    UNION ALL
    
    -- Traverse UP to parent categories
    SELECT ch.infrastructure_id, parent.id, parent.parent_id
    FROM category_hierarchy ch
    INNER JOIN infrastructure_category parent ON ch.parent_id = parent.id
),
root_categories AS (
    -- Filter for root level (parent_id IS NULL)
    SELECT DISTINCT infrastructure_id, category_id
    FROM category_hierarchy
    WHERE parent_id IS NULL
)
SELECT category_id, COUNT(DISTINCT infrastructure_id)
FROM root_categories
GROUP BY category_id
```

### 2. Subcategories Query Pattern

```sql
WITH RECURSIVE category_descendants AS (
    -- Start with direct children
    SELECT ic.id, ic.id as direct_child_id
    FROM infrastructure_category ic
    WHERE ic.parent_id = :categoryId
    
    UNION ALL
    
    -- Traverse DOWN to all descendants
    SELECT child.id, cd.direct_child_id
    FROM infrastructure_category child
    INNER JOIN category_descendants cd ON child.parent_id = cd.id
)
SELECT 
    direct_child_id,
    COUNT(DISTINCT i.id) as count
FROM category_descendants cd
LEFT JOIN sam_infrastructure i ON i.infrastructure_category_id = cd.id
GROUP BY direct_child_id
```

### 3. Infrastructure Products Query Pattern

```sql
WITH RECURSIVE category_tree AS (
    -- Start with selected category
    SELECT id FROM infrastructure_category WHERE id = :categoryId
    
    UNION ALL
    
    -- Get all children
    SELECT child.id
    FROM infrastructure_category child
    INNER JOIN category_tree parent ON child.parent_id = parent.id
)
SELECT i.*, v.name_translations as vendor_name
FROM sam_infrastructure i
INNER JOIN category_tree ct ON i.infrastructure_category_id = ct.id
LEFT JOIN sam_vendor v ON i.vendor_id = v.id
WHERE i.status_code = 'ACTIVE'
```

---

## Data Model

### Entity Relationships

```
infrastructure_category
    ├── id (PK)
    ├── parent_id (FK → infrastructure_category.id)
    ├── name_translations (JSONB)
    └── status_code

sam_infrastructure
    ├── id (PK)
    ├── infrastructure_category_id (FK → infrastructure_category.id)
    ├── vendor_id (FK → sam_vendor.id)
    ├── name_translations (JSONB)
    ├── model
    ├── version
    ├── location
    └── status_code

sam_vendor
    ├── id (PK)
    └── name_translations (JSONB)
```

### Category Hierarchy Example

```
Hardware (id=1, parent_id=NULL)  ← ROOT
    ├── Servers (id=20, parent_id=1)  ← SUBCATEGORY
    │   ├── Physical Servers (id=21, parent_id=20)  ← LEAF
    │   └── Virtual Servers (id=22, parent_id=20)  ← LEAF
    ├── Storage Devices (id=30, parent_id=1)  ← SUBCATEGORY
    │   ├── SAN Storage (id=31, parent_id=30)  ← LEAF
    │   └── NAS Storage (id=32, parent_id=30)  ← LEAF
    └── Networking Equipment (id=40, parent_id=1)  ← SUBCATEGORY
        ├── Switches (id=41, parent_id=40)  ← LEAF
        └── Routers (id=42, parent_id=40)  ← LEAF
```

---

## Error Handling

All endpoints include error handling with:

- **Try-catch blocks** around database queries
- **Logging** of errors with context (category ID, error message)
- **Empty results** returned on error instead of throwing exceptions
- **Default values** for missing optional fields (e.g., uncategorized infrastructure)

### Example Error Scenarios

| Scenario | Behavior |
|----------|----------|
| Category not found | Returns empty subcategories list with default parent info |
| Invalid category ID format | Logs error, returns empty result |
| Database connection failure | Logs error, returns empty result |
| Null vendor | Returns infrastructure with vendor name as empty/null |

---

## Performance Considerations

1. **Indexes Required:**
   - `infrastructure_category(parent_id)`
   - `sam_infrastructure(infrastructure_category_id)`
   - `sam_infrastructure(vendor_id)`
   - `sam_infrastructure(status_code)`

2. **Query Optimization:**
   - Recursive CTEs limited to 10 levels max (prevents infinite loops)
   - Status filtering at query level (not in application)
   - DISTINCT used only where necessary

3. **Caching Recommendations:**
   - Root categories distribution changes infrequently → cache for 5-10 minutes
   - Subcategories relatively stable → cache for 2-5 minutes
   - Infrastructure products change more frequently → cache for 30-60 seconds

---

## Usage Examples

### JavaScript/TypeScript

```typescript
// Level 1: Get root categories
const rootCategories = await fetch('/analytics/infrastructure/categories')
    .then(res => res.json());

// Level 2: Drill down to subcategories
const categoryId = rootCategories.categoryDistributions[0].categoryId;
const subcategories = await fetch(`/analytics/infrastructure/categories/class?categoryId=${categoryId}`)
    .then(res => res.json());

// Level 3: Get infrastructure products
const subcategoryId = subcategories.subcategories[0].subcategoryId;
const products = await fetch(`/analytics/infrastructure/categories/class/product?categoryId=${subcategoryId}`)
    .then(res => res.json());
```

### cURL

```bash
# Get root categories
curl -X GET "http://localhost:8080/analytics/infrastructure/categories"

# Get subcategories for Hardware (id=1)
curl -X GET "http://localhost:8080/analytics/infrastructure/categories/class?categoryId=1"

# Get infrastructure products for Servers (id=20)
curl -X GET "http://localhost:8080/analytics/infrastructure/categories/class/product?categoryId=20"
```

---

## Multilingual Support

All endpoints return multilingual data in JSONB format with the following language codes:

- `en` - English
- `ar` - Arabic
- `de` - German
- `fr` - French
- `sw` - Swahili

Frontend applications should extract the appropriate language based on user preference:

```typescript
const displayName = category.categoryName[userLanguage] || category.categoryName['en'];
```

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2025-11-10 | Initial release with three-level drill-down |

---

## Support

For issues or questions, contact the development team or refer to the main API documentation.
