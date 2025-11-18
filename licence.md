# License Analytics Drill-Down Endpoints

## Overview Drill-Down

### Get All License Details
**GET** `/analytics/license/overview/details`

Returns all active licenses with full details.

**Response:**
```json
{
  "licenses": [
    {
      "id": 1,
      "nameTranslations": {"en": "Oracle Database", "ar": "..."},
      "descriptionTranslations": {...},
      "vendorName": {"en": "Oracle", "ar": "..."},
      "productName": "Database Enterprise",
      "applicationName": "",
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

## Cost Overview Drill-Down

### Get Cost Breakdown Details
**GET** `/analytics/license/cost-overview/details`

Returns cost breakdown by vendor and product family with percentages.

**Response:**
```json
{
  "vendors": [
    {
      "vendorId": 1,
      "vendorName": {"en": "Microsoft", "ar": "..."},
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
      "productFamilyName": {"en": "Office 365", "ar": "..."},
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

## Cost Breakdown Drill-Downs

### Get Licenses by Vendor
**GET** `/analytics/license/cost-breakdown/vendor/{vendorId}/details`

Returns all licenses for a specific vendor.

**Path Parameters:**
- `vendorId` (Long) - Vendor ID

**Response:**
```json
{
  "categoryType": "vendor",
  "categoryId": 1,
  "categoryName": {"en": "Microsoft", "ar": "..."},
  "licenses": [
    {
      "id": 5,
      "nameTranslations": {"en": "Office 365 E5", "ar": "..."},
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

### Get Licenses by Product Family
**GET** `/analytics/license/cost-breakdown/product-category/{productFamilyId}/details`

Returns all licenses for a specific product family.

**Path Parameters:**
- `productFamilyId` (Long) - Product family ID

**Response:** Same structure as vendor endpoint, with `categoryType: "product-category"`

### Get Licenses by Application
**GET** `/analytics/license/cost-breakdown/application/{applicationId}/details`

Returns all licenses for a specific application.

**Path Parameters:**
- `applicationId` (Long) - Application ID

**Response:** Same structure as vendor endpoint, with `categoryType: "application"`

---

## Notes

- All endpoints filter for `status_code = 'ACTIVE'`
- Excludes licenses with status `Expired` or `Inactive`
- Costs calculated as: `licenseCost = cost_per_license × quantity_purchased`
- Results ordered by total cost descending
