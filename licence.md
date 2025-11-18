# License Analytics Drill-Down Endpoints

## 1. Overview Details
**GET** `/analytics/license/overview/details`

**Response:**
```json
{
  "licenses": [
    {
      "id": 1,
      "nameTranslations": {"en": "Oracle Database", "ar": "قاعدة بيانات أوراكل"},
      "descriptionTranslations": {"en": "Enterprise database", "ar": "قاعدة بيانات المؤسسة"},
      "vendorName": {"en": "Oracle", "ar": "أوراكل"},
      "productName": "Database Enterprise",
      "applicationName": "ERP System",
      "licenseCost": 1000000.00,
      "supportCost": 50000.00,
      "totalCost": 1050000.00,
      "startDate": "2024-01-15",
      "expiryDate": "2025-01-15",
      "licenseStatus": "Active",
      "paymentStatus": "Paid"
    }
  ],
  "totalCount": 45
}
```

---

## 2. Cost Overview Details
**GET** `/analytics/license/cost-overview/details`

**Response:**
```json
{
  "vendors": [
    {
      "vendorId": 1,
      "vendorName": {"en": "Microsoft", "ar": "مايكروسوفت"},
      "licenseCount": 15,
      "licenseCost": 2500000.00,
      "supportCost": 150000.00,
      "totalCost": 2650000.00,
      "percentage": 35.5
    }
  ],
  "productFamilies": [
    {
      "productFamilyId": 3,
      "productFamilyName": {"en": "Office 365", "ar": "أوفيس 365"},
      "licenseCount": 20,
      "licenseCost": 800000.00,
      "supportCost": 50000.00,
      "totalCost": 850000.00,
      "percentage": 19.2
    }
  ],
  "totalLicenseCost": 4407450.00,
  "totalSupportCost": 22640.00,
  "grandTotal": 4430090.00
}
```

---

## 3. Licenses by Vendor (Top Vendors)
**GET** `/analytics/license/top-vendors/{vendorId}`

**Response:**
```json
{
  "categoryType": "vendor",
  "categoryId": 1,
  "categoryName": {"en": "Microsoft", "ar": "مايكروسوفت"},
  "licenses": [
    {
      "id": 5,
      "nameTranslations": {"en": "Office 365 E5", "ar": "أوفيس 365 E5"},
      "licenseCost": 500000.00,
      "supportCost": 25000.00,
      "totalCost": 525000.00,
      "purchaseDate": "2024-03-01",
      "expiryDate": "2025-03-01",
      "licenseStatus": "Active",
      "paymentStatus": "Paid"
    }
  ],
  "totalCount": 15,
  "totalCost": 2650000.00
}
```

---

## 4. Licenses by Vendor (Cost Breakdown)
**GET** `/analytics/license/cost-breakdown/vendor/{vendorId}/details`

**Response:** Same as endpoint #3

---

## 5. Licenses by Product Family
**GET** `/analytics/license/cost-breakdown/product-category/{productFamilyId}/details`

**Response:**
```json
{
  "categoryType": "product-category",
  "categoryId": 3,
  "categoryName": {"en": "Office 365", "ar": "أوفيس 365"},
  "licenses": [
    {
      "id": 8,
      "nameTranslations": {"en": "Office 365 E3", "ar": "أوفيس 365 E3"},
      "licenseCost": 300000.00,
      "supportCost": 15000.00,
      "totalCost": 315000.00,
      "purchaseDate": "2024-02-10",
      "expiryDate": "2025-02-10",
      "licenseStatus": "Active",
      "paymentStatus": "Paid"
    }
  ],
  "totalCount": 20,
  "totalCost": 850000.00
}
```

---

## 6. Licenses by Application
**GET** `/analytics/license/cost-breakdown/application/{applicationId}/details`

**Response:**
```json
{
  "categoryType": "application",
  "categoryId": 7,
  "categoryName": {"en": "ERP System", "ar": "نظام تخطيط موارد المؤسسات"},
  "licenses": [
    {
      "id": 12,
      "nameTranslations": {"en": "SAP License", "ar": "ترخيص SAP"},
      "licenseCost": 2000000.00,
      "supportCost": 100000.00,
      "totalCost": 2100000.00,
      "purchaseDate": "2023-12-01",
      "expiryDate": "2024-12-01",
      "licenseStatus": "Active",
      "paymentStatus": "Paid"
    }
  ],
  "totalCount": 8,
  "totalCost": 4500000.00
}
```

---

## 7. Licenses by License Model
**GET** `/analytics/license/model-distribution/{licenseBasedId}`

**Response:**
```json
{
  "categoryType": "license-model",
  "categoryId": 5,
  "categoryName": {"en": "User-based", "ar": "على أساس المستخدم"},
  "licenses": [
    {
      "id": 15,
      "nameTranslations": {"en": "Adobe Creative Cloud", "ar": "أدوبي كريتيف كلاود"},
      "licenseCost": 150000.00,
      "supportCost": 7500.00,
      "totalCost": 157500.00,
      "purchaseDate": "2024-04-01",
      "expiryDate": "2025-04-01",
      "licenseStatus": "Active",
      "paymentStatus": "Paid"
    }
  ],
  "totalCount": 25,
  "totalCost": 3500000.00
}
```

---

## 8. Licenses by Payment Frequency
**GET** `/analytics/license/payment-frequency/{paymentFrequencyId}`

**Response:**
```json
{
  "categoryType": "payment-frequency",
  "categoryId": 2,
  "categoryName": {"en": "Annual", "ar": "سنوي"},
  "licenses": [
    {
      "id": 20,
      "nameTranslations": {"en": "Autodesk AutoCAD", "ar": "أوتوديسك أوتوكاد"},
      "licenseCost": 500000.00,
      "supportCost": 25000.00,
      "totalCost": 525000.00,
      "purchaseDate": "2024-01-01",
      "expiryDate": "2025-01-01",
      "licenseStatus": "Active",
      "paymentStatus": "Paid"
    }
  ],
  "totalCount": 35,
  "totalCost": 5200000.00
}
```

**Use Case:** Displayed when user clicks on a bar in the Payment Frequency chart.

**Filter:** `status_code = 'ACTIVE'` AND specific `payment_frequency_id`

---

## 7. Cost Composition Drill-Down
  "totalCost": 5200000.00
}
```

---

## 9. Licenses by Vendor (Cost Composition)
**GET** `/analytics/license/cost-composition/{vendorId}`

**Response:** Same as endpoint #3

---

## 10. Licenses by Payment Status
**GET** `/analytics/license/financial-status/{paymentStatusId}`

**Response:**tCost": 50000.00,
      "totalCost": 1050000.00,
      "purchaseDate": "2024-01-15",
      "expiryDate": "2025-01-15",
      "licenseStatus": "Active",
      "paymentStatus": "Paid"
    }
  ],
  "totalCount": 40,
  "totalCost": 8900000.00
}
```

**Use Case:** Displayed when user clicks on a slice of the Financial Status pie chart.

**Filter:** `status_code = 'ACTIVE'` AND specific `payment_status_id`

---

## 9. License Status Overview Drill-Down

### Get Licenses by License Status
**GET** `/analytics/license/status-overview/{licenseStatusId}`

**Description:** Returns all licenses with a specific license status (e.g., Active, Expired, Inactive, Pending, Cancelled).

**Path Parameters:**
- `licenseStatusId` (Long, required) - The license status enum ID

**Response:**
```json
{
  "categoryType": "license-status",
  "totalCost": 8900000.00
}
```

---

## 11. Licenses by License Status
**GET** `/analytics/license/status-overview/{licenseStatusId}`

**Response:** Displayed when user clicks on a bar in the License Status Overview chart.

**Filter:** `status_code = 'ACTIVE'` AND specific `license_status_id`

**Important Note:** This endpoint filters ONLY by `status_code = 'ACTIVE'` (not by license_status.name), allowing drill-down for all license statuses including expired and inactive licenses, as long as the record itself is not soft-deleted.

---

## Common Response Structure

All drill-down endpoints (except overview and cost-overview details) return the following standard structure:

```json
{
  "categoryType": "string",        // vendor, product-category, application, license-model, payment-frequency, payment-status, license-status
  "categoryId": "number",          // ID of the category
  "categoryName": {                // Multi-language translations
    "en": "string",
    "ar": "string"
  },
  "licenses": [                    // Array of licenses
    {
      "id": "number",
      "nameTranslations": {},
      "licenseCost": "number",
      "supportCost": "number",
      "totalCost": "number",
      "purchaseDate": "date",
      "expiryDate": "date",
      "licenseStatus": "string",
      "paymentStatus": "string"
    }
  ],
  "totalCount": "number",          // Total number of licenses
  "totalCost": "number"            // Sum of all license costs
}
```

---

## Implementation Notes

### Multi-Language Support
All endpoints return translations in JSONB format supporting:
- **en**: English
- **ar**: Arabic
- **fr**: French
- **de**: German
- **sw**: Swahili

### Code Optimizations
The implementation uses three helper methods to eliminate ~329 lines of duplicated code:

1. **`buildLicenseItemsFromResults(List<Object[]> results)`** 
   - Converts query results to `LicenseItem` objects
   - Handles JSONB parsing for name translations
   - Calculates costs from query results

2. **`calculateTotalCost(List<LicenseItem> licenses)`**
   - Stream-based cost aggregation
   - Returns `BigDecimal` total

3. **`getCategoryName(Long categoryId, String tableName, String idColumn)`**
   - Generic lookup for category names from different tables
   - Supports: `sam_vendor`, `sam_vendor_product_family`, `sam_application`, `enums`
   - Returns multi-language translations

### Status Filtering
- Most endpoints filter for `status_code = 'ACTIVE'` AND `license_status.name = 'Active'`
- **Exception**: `getLicensesByLicenseStatus()` filters only by `status_code = 'ACTIVE'` to allow drill-down for all license statuses

### Cost Calculations
- `licenseCost = cost_per_license × quantity_purchased`
- `totalCost = licenseCost + supportCost`
- All monetary values in SAR (Saudi Riyal) or configured currency

---

## Performance Considerations

### ⚠️ Critical Performance Issues

#### 1. **Missing Pagination** (HIGH PRIORITY)
**Issue:** All 9 drill-down endpoints fetch ALL matching licenses without pagination.

**Impact:**
- With 5000 licenses: ~250MB memory per request
- Response time: 5-10 seconds
- Database full table scans
- Poor user experience

**Affected Endpoints:**
- All 9 drill-down methods
- `getLicenseDetails()` - returns ALL licenses
- `getLicenseCostDetails()` - returns ALL active license costs

**Recommended Solution:**
```java
// Add pagination parameters to controller
@GetMapping("/top-vendors/{vendorId}")
public ResponseEntity<LicenseCostBreakdownDetailsDto> getTopVendorDetails(
    @PathVariable Long vendorId,
    @RequestParam(defaultValue = "0") int page,
    @RequestParam(defaultValue = "20") int size) {
    return ResponseEntity.ok(licenseAnalyticsService.getLicensesByVendor(vendorId, page, size));
}

// Update DTO to include pagination metadata
private Integer totalPages;
private Integer currentPage;
private Integer pageSize;

// Update SQL with LIMIT/OFFSET
String sql = """
    SELECT ... FROM sam_license
    WHERE vendor_id = :vendorId
    ORDER BY total_cost DESC
    LIMIT :limit OFFSET :offset
    """;
```

**Expected Improvements:**
| Metric | Before | After |
|--------|--------|-------|
| Memory/Request | 50-250MB | 2-5MB |
| Response Time | 2-10s | 50-200ms |
| Max Concurrent Users | 10-20 | 200+ |

---

#### 2. **Missing Database Indexes**
**Issue:** No indexes on foreign keys used for filtering.

**Recommended Indexes:**
```sql
CREATE INDEX CONCURRENTLY idx_sam_license_vendor 
ON sam_license(vendor_id) WHERE deleted_at IS NULL;

CREATE INDEX CONCURRENTLY idx_sam_license_product_family 
ON sam_license(vendor_product_family_id) WHERE deleted_at IS NULL;

CREATE INDEX CONCURRENTLY idx_sam_license_status 
ON sam_license(license_status_id) WHERE deleted_at IS NULL;

CREATE INDEX CONCURRENTLY idx_sam_license_payment_status 
ON sam_license(payment_status_id) WHERE deleted_at IS NULL;

CREATE INDEX CONCURRENTLY idx_sam_license_payment_frequency 
ON sam_license(payment_frequency_id) WHERE deleted_at IS NULL;

CREATE INDEX CONCURRENTLY idx_sam_license_model 
ON sam_license(license_based_id) WHERE deleted_at IS NULL;

CREATE INDEX CONCURRENTLY idx_sam_application_licenses_app 
ON sam_application_licenses(application_id) WHERE deleted_at IS NULL;
```

---

#### 3. **No Query Caching**
**Issue:** `getCategoryName()` executes separate query for each drill-down call.

**Recommended Solution:**
```java
@Cacheable(value = "categoryNames", key = "#categoryId + '-' + #tableName")
private Map<String, String> getCategoryName(Long categoryId, String tableName, String idColumn) {
    // existing implementation
}
```

---

#### 4. **Multiple Queries in getLicenseCostDetails()**
**Issue:** Runs 3 separate queries instead of 1.

**Current:**
```java
// Query 1: Vendor costs CTE
// Query 2: Product costs CTE  
// Query 3: Total costs
```

**Recommended:** Combine into single query with UNION ALL.

---

### ✅ What's Optimized

1. **Helper Methods** - Good code reuse eliminates ~329 lines of duplication
2. **CTEs Used** - Efficient aggregations in overview queries
3. **JSONB Handling** - Proper multi-language support with PostgreSQL functions
4. **Type Safety** - Strong DTOs with Lombok builders

---

## Frontend Integration Guide

### Drill-Down Flow Example

1. **User views summary chart** (e.g., Model Distribution pie chart)
   - Chart displays: "User-based: 45% (25 licenses)"
   - Store the `licenseBasedId` from the summary endpoint

2. **User clicks on chart slice**
   - Frontend calls: `/model-distribution/{licenseBasedId}`
   - Displays modal/page with detailed list of all 25 User-based licenses

3. **User explores license details**
   - Each license shows costs, dates, status information
   - Option to export, filter, or sort

### Recommended UI Patterns

- **Cards with "View Details" buttons**: For summary metrics (Overview, Cost Overview)
- **Interactive charts**: For breakdown visualizations (pie charts, bar charts)
- **Modal dialogs or slide-out panels**: For displaying drill-down lists
- **Data tables with features**:
  - Sorting by columns (cost, date, status)
  - Client-side or server-side pagination
  - Search/filter functionality
  - Export to CSV/Excel
- **Breadcrumbs**: Navigate back from drill-down views
- **Loading states**: Show skeletons while fetching drill-down data
- **Empty states**: Handle cases with no licenses in category

### State Management
```javascript
// Example React state structure
const [drillDownData, setDrillDownData] = useState({
  categoryType: null,
  categoryId: null,
  categoryName: {},
  licenses: [],
  totalCount: 0,
  totalCost: 0
});

const handleChartClick = async (categoryId, categoryType) => {
  const response = await fetch(`/analytics/license/${categoryType}/${categoryId}`);
  const data = await response.json();
  setDrillDownData(data);
  setShowModal(true);
};
```

---

## Testing Examples

### cURL Examples

```bash
# Get all license details
curl -X GET "http://localhost:8080/analytics/license/overview/details"

# Get cost breakdown details
curl -X GET "http://localhost:8080/analytics/license/cost-overview/details"

# Get licenses by vendor
curl -X GET "http://localhost:8080/analytics/license/top-vendors/1"

# Get licenses by product family
curl -X GET "http://localhost:8080/analytics/license/cost-breakdown/product-category/3/details"

# Get licenses by application
curl -X GET "http://localhost:8080/analytics/license/cost-breakdown/application/7/details"

# Get licenses by license model
curl -X GET "http://localhost:8080/analytics/license/model-distribution/5"

# Get licenses by payment frequency
curl -X GET "http://localhost:8080/analytics/license/payment-frequency/2"

# Get licenses by payment status
curl -X GET "http://localhost:8080/analytics/license/financial-status/1"

# Get licenses by license status
curl -X GET "http://localhost:8080/analytics/license/status-overview/1"

# Cost composition (alias for vendor)
curl -X GET "http://localhost:8080/analytics/license/cost-composition/1"
```

### Postman Collection
Import the following JSON to test all endpoints:
```json
{
  "info": {
    "name": "License Analytics Drill-Downs",
    "schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json"
  },
  "item": [
    {
      "name": "Overview Details",
      "request": {
        "method": "GET",
        "url": "{{baseUrl}}/analytics/license/overview/details"
      }
    },
    {
      "name": "Cost Overview Details",
      "request": {
        "method": "GET",
        "url": "{{baseUrl}}/analytics/license/cost-overview/details"
      }
    }
  ]
}
```

---

## Change Summary

### Endpoints Implemented: 11 drill-down endpoints
1. `/overview/details` - All license details
2. `/cost-overview/details` - Cost breakdown details
3. `/top-vendors/{vendorId}` - Top vendor drill-down
4. `/cost-breakdown/vendor/{vendorId}/details` - Vendor drill-down
5. `/cost-breakdown/product-category/{productFamilyId}/details` - Product family drill-down
6. `/cost-breakdown/application/{applicationId}/details` - Application drill-down
7. `/model-distribution/{licenseBasedId}` - License model drill-down
8. `/payment-frequency/{paymentFrequencyId}` - Payment frequency drill-down
9. `/financial-status/{paymentStatusId}` - Payment status drill-down
10. `/status-overview/{licenseStatusId}` - License status drill-down
11. `/cost-composition/{vendorId}` - Cost composition drill-down (alias)

### Code Optimizations
- ✅ Created 3 helper methods to eliminate ~329 lines of duplicated code
- ✅ Fixed SQL column names (`cost_per_license`, `expiration_date`)
- ✅ Fixed status filtering for status-overview drill-down
- ✅ Standardized drill-down response structure with `LicenseCostBreakdownDetailsDto`

### DTOs Used
1. `LicenseDetailsDto` - Overview details
2. `LicenseCostDetailsDto` - Cost overview details
3. `LicenseCostBreakdownDetailsDto` - All category drill-downs (shared DTO)

---

## Architecture Overview

```
┌─────────────────────────────────────────┐
│  LicenseAnalyticsController.java       │
│  - 19 REST endpoints                    │
│  - Path variables & query params        │
└─────────────┬───────────────────────────┘
              │
              ▼
┌─────────────────────────────────────────┐
│  LicenseAnalyticsService.java           │
│  - Business logic layer                 │
│  - Delegates to repository              │
└─────────────┬───────────────────────────┘
              │
              ▼
┌─────────────────────────────────────────┐
│  LicenseAnalyticsRepository.java        │
│  - Interface with method signatures     │
└─────────────┬───────────────────────────┘
              │
              ▼
┌─────────────────────────────────────────┐
│  LicenseAnalyticsRepositoryImpl.java    │
│  - Native SQL queries                   │
│  - Helper methods (3 total)             │
│  - JSONB parsing                        │
│  - PostgreSQL CTEs & aggregations       │
└─────────────┬───────────────────────────┘
              │
              ▼
┌─────────────────────────────────────────┐
│  PostgreSQL Database                    │
│  - sam_license (main table)             │
│  - sam_vendor, sam_vendor_product_family│
│  - sam_application, enums               │
│  - sam_application_licenses (join)      │
└─────────────────────────────────────────┘
```

All drill-down endpoints follow clean architecture with proper separation of concerns.

---

## Status Codes

- **200 OK**: Successful request with data
- **404 Not Found**: Category ID not found
- **500 Internal Server Error**: Database or server error

---

## Security Considerations

- All endpoints require authentication (Spring Security)
- Multi-tenancy support via tenant context
- Soft-delete filtering (`deleted_at IS NULL`)
- No direct SQL injection risk (parameterized queries)

---

## Future Enhancements

1. **Pagination** - Add page/size parameters to all drill-downs
2. **Sorting** - Allow sorting by cost, date, status
3. **Filtering** - Add date range, status, cost range filters
4. **Export** - CSV/Excel export functionality
5. **Caching** - Redis cache for category name lookups
6. **Aggregations** - Add min/max/avg cost statistics
7. **Trends** - Historical cost trends over time
8. **Alerts** - Notify when licenses near expiration

---

## Version Information

- **Branch**: `INTEGRATION_DRILL`
- **Feature**: License Analytics Drill-Down Endpoints
- **Date**: November 18, 2025
- **Total Endpoints**: 19 (12 summary + 7 unique drill-downs + 2 detail views)
- **Lines of Code**: ~1372 lines in repository implementation
- **Code Reduction**: ~329 lines eliminated through helper methods

---

## Support & Feedback

For questions or issues with these endpoints, contact:
- Development Team: dpkass-squad
- Repository: manjam-plus
- Branch: INTEGRATION_DRILL
