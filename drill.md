# Infrastructure Analytics Drill-Down API

## Overview
Three new drill-down endpoints for Infrastructure Analytics dashboard.

---

## 1. Total Infrastructure Details

**Endpoint:** `GET /analytics/infrastructure/total/details`

**Description:** Drill-down from total infrastructure count

**Response:**
```json
[
  {
    "infrastructureId": "1",
    "infrastructureName": {"en": "Cloud Server", "ar": "خادم سحابي"},
    "model": "AWS EC2",
    "version": "2.0",
    "location": "US-East",
    "vendorName": {"en": "Amazon", "ar": "أمازون"},
    "categoryName": {"en": "Cloud Infrastructure", "ar": "البنية السحابية"}
  }
]
```

---

## 2. Infrastructure by Vendor

**Endpoint:** `GET /analytics/infrastructure/per-vendor/{vendorId}`

**Description:** Drill-down from per-vendor chart

**Path Parameters:**
- `vendorId` (required) - Vendor ID

**Response:**
```json
[
  {
    "infrastructureId": "1",
    "infrastructureName": {"en": "Cloud Server", "ar": "خادم سحابي"},
    "model": "AWS EC2",
    "version": "2.0",
    "location": "US-East",
    "vendorName": {"en": "Amazon", "ar": "أمازون"},
    "categoryName": {"en": "Cloud Infrastructure", "ar": "البنية السحابية"}
  }
]
```

---

## 3. Ecosystem Composition Details

**Endpoint:** `GET /analytics/infrastructure/ecosystem-composition/{infrastructureId}`

**Description:** Drill-down from ecosystem composition bar chart

**Path Parameters:**
- `infrastructureId` (required) - Infrastructure ID

**Response:**
```json
{
  "infrastructureId": "94",
  "infrastructureName": {"en": "Database Server", "ar": "خادم قاعدة البيانات"},
  "applications": [
    {
      "componentId": "1",
      "componentName": {"en": "HR System", "ar": "نظام الموارد البشرية"},
      "description": {"en": "Human Resources Management", "ar": "إدارة الموارد البشرية"},
      "vendorName": {"en": "Oracle", "ar": "أوراكل"},
      "version": "12.2"
    }
  ],
  "integrations": [
    {
      "componentId": "2",
      "componentName": {"en": "API Gateway", "ar": "بوابة API"},
      "description": {"en": "Integration Gateway", "ar": "بوابة التكامل"},
      "vendorName": null,
      "version": null
    }
  ],
  "licenses": [
    {
      "componentId": "3",
      "componentName": {"en": "Database License", "ar": "ترخيص قاعدة البيانات"},
      "description": {"en": "Enterprise License", "ar": "ترخيص المؤسسة"},
      "vendorName": {"en": "Oracle", "ar": "أوراكل"},
      "version": null
    }
  ]
}
```

---

## Notes

- All endpoints return multi-language fields (en, ar, de, fr, sw)
- Only ACTIVE status infrastructures are included
- Empty arrays returned on error or no data
- Integrations and licenses may have null vendor/version fields based on database schema
