# License Analytics API Documentation

## Overview
REST API for License Analytics Dashboard providing comprehensive insights into software licenses, costs, vendor statistics, and lifecycle management.

## Base Path
```
/analytics/license
```

---

## Endpoints

### 1. License Overview
Get overall license statistics with status breakdown.

**Endpoint:**
```http
GET /analytics/license/overview
```

**Description:** Card 1 - Shows total number of licenses registered with breakdown by status (Active, Expiring Soon, Expired)

**Response:**
```json
{
    "totalLicenses": 16,
    "activeLicenses": 7,
    "expiringSoonLicenses": 4,
    "expiredLicenses": 1
}
```


---

### 2. License Cost Overview
Get total license and support costs.

**Endpoint:**
```http
GET /analytics/license/cost-overview
```

**Description:** Card 2 - Total License Cost (License cost + Support cost in OMR)

**Response:**
```json
{
    "totalLicenseCost": 4407450,
    "totalSupportCost": 22640,
    "grandTotal": 4430090,
    "currency": "OMR"
}
```


---

### 3. Top Vendors by License Count
Get vendors ranked by number of licenses.

**Endpoint:**
```http
GET /analytics/license/top-vendors?limit=3
```

**Description:** Card 3 - Shows top vendors with their license counts

**Parameters:**
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `limit` | int | No | 3 | Maximum number of vendors to return |

**Response:**
```json
[
  {
    "vendorName": {
      "en": "Microsoft",
      "ar": "مايكروسوفت"
    },
    "licenseCount": 45,
    "percentage": 30.0
  },
  {
    "vendorName": {
      "en": "Oracle",
      "ar": "أوراكل"
    },
    "licenseCount": 30,
    "percentage": 20.0
  }
]
```

**Response Type:** `List<TopVendorsByLicenseDto>`

---

### 4. Licenses Expiring Soon
Get licenses expiring within specified timeframe.

**Endpoint:**
```http
GET /analytics/license/expiring-soon?days=90
```

**Description:** Card 4 - Shows individual licenses with expiration dates approaching

**Parameters:**
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `days` | int | No | 90 | Number of days to look ahead |

**Response:**
```json
[
    {
        "licenseId": 122,
        "licenseName": {
            "ar": "ترخيص SAP S/4HANA",
            "de": "SAP S/4HANA-Lizenz",
            "en": "SAP S/4HANA license",
            "fr": "Licence SAP S/4HANA",
            "sw": "SAP S/4HANA Leseni"
        },
        "expirationDate": "2025-11-17",
        "daysUntilExpiration": 5,
        "vendorName": {
            "ar": "ساب",
            "de": "Saft",
            "en": "SAP",
            "fr": "Sève",
            "sw": "SAP"
        }
    },
    {
        "licenseId": 127,
        "licenseName": {
            "ar": "OVM",
            "de": "OVM",
            "en": "OVM",
            "fr": "OVM",
            "sw": "Ovm"
        },
        "expirationDate": "2025-11-21",
        "daysUntilExpiration": 9,
        "vendorName": {
            "ar": "أوراكل",
            "de": "Orakel",
            "en": "Oracle",
            "fr": "Oracle",
            "sw": "Oracle"
        }
    },
    {
        "licenseId": 1,
        "licenseName": {
            "ar": "bitdefender - قائم على الخادم",
            "de": "Bitdefender",
            "en": "Bitdefender - Server Based",
            "fr": "Bitdefender",
            "sw": "Bitdefender"
        },
        "expirationDate": "2025-12-22",
        "daysUntilExpiration": 40,
        "vendorName": {
            "ar": "غير مسمى",
            "en": "Unnamed"
        }
    },
    {
        "licenseId": 2,
        "licenseName": {
            "ar": "Bitdefender - صندوق البريد",
            "de": "Bitdefnder - Mailbox",
            "en": "Bitdefender - Mailbox",
            "fr": "BitDefnder - boîte aux lettres",
            "sw": "Bitdefnder - sanduku la barua"
        },
        "expirationDate": "2025-12-22",
        "daysUntilExpiration": 40,
        "vendorName": {
            "ar": "غير مسمى",
            "en": "Unnamed"
        }
    }
]
```

**Response Type:** `List<LicenseExpiringSoonDto>`

---

### 5. License Cost Breakdown
Get cost breakdown by vendor or category.

**Endpoint:**
```http
GET /analytics/license/cost-breakdown?view=vendor
```

**Parameters:**
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `view` | string | No | vendor | Breakdown view: `vendor` or `product-category` or `application` |

"vendor" (default) - Groups cost breakdown by vendor
"product-category" - Groups cost breakdown by product category
"application" - Groups cost breakdown by application

**Response:**
```json
[
    {
        "id": 2,
        "name": {
            "ar": "أوراكل",
            "de": "Orakel",
            "en": "Oracle",
            "fr": "Oracle",
            "sw": "Oracle"
        },
        "totalCost": 3047100,
        "percentage": 68.78
    },
    {
        "id": 4,
        "name": {
            "ar": "جوجل",
            "de": "Google",
            "en": "Google",
            "fr": "Google",
            "sw": "Google"
        },
        "totalCost": 1202000,
        "percentage": 27.13
    },
]
```


---

### 6. License Utilization
Get license utilization statistics.

**Endpoint:**
```http
GET /analytics/license/utilization
```

**Response:**
```json
{
    "quantityPurchased": 434,
    "quantityUsed": 390,
    "utilizationPercentage": 89.86
}
```


---

### 7. License Model Distribution
Get distribution of licenses by licensing model.

**Endpoint:**
```http
GET /analytics/license/model-distribution
```

**Description:** Shows breakdown by perpetual, subscription, concurrent, etc.

**Response:**
```json

[
    {
        "licenseBasedId": 333,
        "licenseBasedName": {
            "ar": "Subscription-based",
            "de": "Abonnementbasiert",
            "en": "Subscription-based",
            "fr": "Sous-marin",
            "sw": "Usajili-msingi"
        },
        "licenseCount": 6,
        "percentage": 37.5
    },
    {
        "licenseBasedId": 0,
        "licenseBasedName": {
            "ar": "غير محدد",
            "en": "Not Specified"
        },
        "licenseCount": 4,
        "percentage": 25.0
    },
    {
        "licenseBasedId": 335,
        "licenseBasedName": {
            "ar": "Server/Core-based",
            "de": "Server/Kernbasiert",
            "en": "Server/Core-based",
            "fr": "Serveur / base basé sur",
            "sw": "Seva/msingi-msingi"
        },
        "licenseCount": 2,
        "percentage": 12.5
    },
    {
        "licenseBasedId": 330,
        "licenseBasedName": {
            "ar": "User-based",
            "de": "Benutzerbasiert",
            "en": "User-based",
            "fr": "Utilisateur",
            "sw": "Msingi wa watumiaji"
        },
        "licenseCount": 1,
        "percentage": 6.25
    },
    {
        "licenseBasedId": 332,
        "licenseBasedName": {
            "ar": "Perpetual",
            "de": "Ewig",
            "en": "Perpetual",
            "fr": "Perpétuel",
            "sw": "Daima"
        },
        "licenseCount": 1,
        "percentage": 6.25
    },
    {
        "licenseBasedId": 329,
        "licenseBasedName": {
            "ar": "Processor-based",
            "de": "Prozessorbasiert",
            "en": "Processor-based",
            "fr": "Processeur",
            "sw": "Msingi wa processor"
        },
        "licenseCount": 1,
        "percentage": 6.25
    },
    {
        "licenseBasedId": 334,
        "licenseBasedName": {
            "ar": "Device-based",
            "de": "Gerätebasiert",
            "en": "Device-based",
            "fr": "Basé sur l'appareil",
            "sw": "Msingi wa kifaa"
        },
        "licenseCount": 1,
        "percentage": 6.25
    }
]

```


---

### 8. License Payment Frequency
Get distribution of licenses by payment frequency.

**Endpoint:**
```http
GET /analytics/license/payment-frequency
```

**Description:** Shows breakdown by annual, monthly, one-time, etc.

**Response:**
```json
[
    {
        "paymentFrequencyId": 256,
        "paymentFrequencyName": {
            "ar": "شهريا",
            "de": "monatlich",
            "en": "Monthly",
            "fr": "mensuel",
            "sw": "kila mwezi"
        },
        "totalCost": 2775500
    },
    {
        "paymentFrequencyId": 258,
        "paymentFrequencyName": {
            "ar": "سنويا",
            "de": "jährlich",
            "en": "Annually",
            "fr": "annuellement",
            "sw": "kila mwaka"
        },
        "totalCost": 1628600
    },
    {
        "paymentFrequencyId": 255,
        "paymentFrequencyName": {
            "ar": "مرة واحدة",
            "de": "Einmal",
            "en": "One-Time",
            "fr": "Une fois",
            "sw": "Mara moja"
        },
        "totalCost": 24300
    }
]
```


---

### 9. License Cost Composition
Get composition of license costs vs support costs.

**Endpoint:**
```http
GET /analytics/license/cost-composition
```

**Response:**
```json
{
    "totalLicenseCost": 4407450,
    "totalSupportCost": 22640,
    "grandTotal": 4430090,
    "vendors": [
        {
            "vendorId": 2,
            "vendorName": {
                "ar": "أوراكل",
                "de": "Orakel",
                "en": "Oracle",
                "fr": "Oracle",
                "sw": "Oracle"
            },
            "licenseCost": 3036000,
            "supportCost": 11100,
            "totalCost": 3047100
        },
        {
            "vendorId": 4,
            "vendorName": {
                "ar": "جوجل",
                "de": "Google",
                "en": "Google",
                "fr": "Google",
                "sw": "Google"
            },
            "licenseCost": 1200000,
            "supportCost": 2000,
            "totalCost": 1202000
        },
        {
            "vendorId": 25,
            "vendorName": {
                "ar": "F5",
                "de": "F5",
                "en": "F5",
                "fr": "F5",
                "sw": "F5"
            },
            "licenseCost": 150000,
            "supportCost": 5000,
            "totalCost": 155000
        },
        {
            "vendorId": 18,
            "vendorName": {
                "ar": "Paloalto",
                "de": "Paloalto",
                "en": "Paloalto",
                "fr": "Paloalto",
                "sw": "Paloalto"
            },
            "licenseCost": 10150,
            "supportCost": 1540,
            "totalCost": 11690
        },
        {
            "vendorId": 27,
            "vendorName": {
                "ar": "Fortinet",
                "de": "Fortinet",
                "en": "Fortinet",
                "fr": "Fortinet",
                "sw": "Fortinet"
            },
            "licenseCost": 9800,
            "supportCost": 1500,
            "totalCost": 11300
        },
        {
            "vendorId": 9,
            "vendorName": {
                "ar": "ساب",
                "de": "Saft",
                "en": "SAP",
                "fr": "Sève",
                "sw": "SAP"
            },
            "licenseCost": 1500,
            "supportCost": 1500,
            "totalCost": 3000
        }
    ],
    "currency": "OMR"
}
```


---

### 10. License Financial Status
Get financial status of licenses by payment status.

**Endpoint:**
```http
GET /analytics/license/financial-status
```

**Response:**
```json
{
    "totalLicenses": 16,
    "paymentStatusBreakdown": [
        {
            "paymentStatusId": 259,
            "paymentStatusName": {
                "ar": "مدفوع",
                "de": "bezahlt",
                "en": "Paid",
                "fr": "payé",
                "sw": "kulipwa"
            },
            "count": 5,
            "percentage": 31.25
        },
        {
            "paymentStatusId": 261,
            "paymentStatusName": {
                "ar": "مدفوع جزئيا",
                "de": "Teilweise bezahlt",
                "en": "Partially Paid",
                "fr": "Partiellement payé",
                "sw": "Kulipwa kidogo"
            },
            "count": 5,
            "percentage": 31.25
        },
        {
            "paymentStatusId": 260,
            "paymentStatusName": {
                "ar": "غير مدفوع",
                "de": "unbezahlt",
                "en": "Unpaid",
                "fr": "non rémunéré",
                "sw": "isiyolipwa"
            },
            "count": 1,
            "percentage": 6.25
        },
        {
            "paymentStatusId": 262,
            "paymentStatusName": {
                "ar": "متأخر",
                "de": "spät",
                "en": "Overdue",
                "fr": "en retard",
                "sw": "marehemu"
            },
            "count": 1,
            "percentage": 6.25
        }
    ]
}
```


---

### 11. License Status Overview
Get detailed status distribution of all licenses.

**Endpoint:**
```http
GET /analytics/license/status-overview
```

**Response:**
```json
{
    "totalLicenses": 16,
    "licenseStatusBreakdown": [
        {
            "licenseStatusId": 250,
            "licenseStatusName": {
                "ar": "نشط",
                "de": "aktiv",
                "en": "Active",
                "fr": "actif",
                "sw": "kazi"
            },
            "count": 7,
            "percentage": 43.75
        },
        {
            "licenseStatusId": 253,
            "licenseStatusName": {
                "ar": "قيد الانتظار",
                "de": "Warten",
                "en": "Pending",
                "fr": "En attendant",
                "sw": "Kusubiri"
            },
            "count": 2,
            "percentage": 12.5
        },
        {
            "licenseStatusId": 251,
            "licenseStatusName": {
                "ar": "غير نشط",
                "de": "Inaktiv",
                "en": "Inactive",
                "fr": "Inactif",
                "sw": "Haifanyi kazi"
            },
            "count": 1,
            "percentage": 6.25
        },
        {
            "licenseStatusId": 252,
            "licenseStatusName": {
                "ar": "منتهي الصلاحية",
                "de": "Abgelaufen",
                "en": "Expired",
                "fr": "Expiré",
                "sw": "Kumalizika muda wake"
            },
            "count": 1,
            "percentage": 6.25
        },
{
 
```


---

### 12. License Renewal Timeline (Gantt Chart)
Get license renewal timeline for Gantt chart visualization.

**Endpoint:**
```http
GET /analytics/license/renewal-timeline?startDate=2024-11-12&endDate=2026-11-12
```

**Description:** Card 12 - Shows licenses on quarterly timeline with expiration tracking for Gantt chart visualization

**Parameters:**
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `startDate` | date (ISO) | No | 1 year ago | Start date for timeline filter |
| `endDate` | date (ISO) | No | 1 year ahead | End date for timeline filter |

**Response:**
```json
{
    "licenses": [
        {
            "licenseId": 91,
            "licenseName": {
                "ar": "خtebaar Google Workspace Enterprise",
                "de": "Kh",
                "en": "اختبار Google Workspace Enterprise",
                "fr": "Kh",
                "sw": "Kh"
            },
            "startDate": "2023-12-20",
            "expirationDate": "2024-12-20",
            "daysUntilExpiration": 0,
            "quantityPurchased": 15,
            "quantityUsed": 12,
            "totalCost": 2270.00,
            "currency": "OMR",
            "status": "Expired"
        },
        {
            "licenseId": 116,
            "licenseName": {
                "ar": "Paloalto-PA-3220-HQ (نشط)",
                "de": "Paloalto-PA-3220-HQ (aktiv)",
                "en": "PaloAlto-PA-3220-HQ(Active)",
                "fr": "Paloalto-PA-3220-HQ (actif)",
                "sw": "Paloalto-PA-3220-HQ (Active)"
            },
            "startDate": "2021-12-23",
            "expirationDate": "2024-12-23",
            "daysUntilExpiration": 0,
            "quantityPurchased": 1,
            "quantityUsed": 1,
            "totalCost": 62000,
            "currency": "OMR",
            "status": "Expired"
        },
        {
            "licenseId": 100,
            "licenseName": {
                "ar": "اختبار أمان شبكة العرعر",
                "de": "Juniper -Netzwerksicherheitstest",
                "en": "اختبار Juniper Network Security",
                "fr": "Test de sécurité du réseau Juniper",
                "sw": "Mtihani wa Usalama wa Mtandao wa Juniper"
            },
            "startDate": "2024-01-05",
            "expirationDate": "2025-01-05",
            "daysUntilExpiration": 0,
            "quantityPurchased": 5,
            "quantityUsed": 4,
            "totalCost": 1650.00,
            "currency": "OMR",
            "status": "Expired"
        },
        {
            "licenseId": 89,
            "licenseName": {
                "ar": "خtbaar ibm cloud pak",
                "de": "TBAAR IBM Cloud Pak",
                "en": "اختبار IBM Cloud Pak",
                "fr": "Tbaar ibm cloud pak",
                "sw": "TBAAR IBM Cloud Pak"
            },
            "startDate": "2024-01-10",
            "expirationDate": "2025-01-10",
            "daysUntilExpiration": 0,
            "quantityPurchased": 8,
            "quantityUsed": 5,
            "totalCost": 2440.00,
            "currency": "OMR",
            "status": "Expired"
        },
        {
            "licenseId": 44,
            "licenseName": {
                "ar": "Paloalto PA-440 Firewall Shinas WC",
                "de": "Paloalto PA-440 Firewall Shinas WC",
                "en": "Paloalto PA-440 Firewall Shinas WC",
                "fr": "PALOALTO PA-440 Firewall Shinas WC",
                "sw": "Paloalto PA-440 Firewall Shinas WC"
            },
            "startDate": "2023-01-15",
            "expirationDate": "2025-01-15",
            "daysUntilExpiration": 0,
            "quantityPurchased": 1,
            "quantityUsed": 1,
            "totalCost": 4000,
            "currency": "OMR",
            "status": "Expired"
        },
        {
            "licenseId": 129,
            "licenseName": {
                "ar": "F-Secure",
                "de": "F-Secure",
                "en": "F-Secure",
                "fr": "F-Secure",
                "sw": "F-Salama"
            },
            "startDate": "2023-11-02",
            "expirationDate": "2025-01-17",
            "daysUntilExpiration": 0,
            "quantityPurchased": 300,
            "quantityUsed": 280,
            "totalCost": 2700000,
            "currency": "OMR",
            "status": "Expired"
        },
        {
            "licenseId": 130,
            "licenseName": {
                "ar": "PAN-PA-440-AHDATH",
                "de": "PAN-PA-440-AHDATH",
                "en": "PAN-PA-440-AHDATH",
                "fr": "PAN-PA-440-AHDATH",
                "sw": "Pan-PA-440-Ahdath"
            },
            "startDate": "2024-03-17",
            "expirationDate": "2025-01-17",
            "daysUntilExpiration": 0,
            "quantityPurchased": 1,
            "quantityUsed": 1,
            "totalCost": 10000,
            "currency": "OMR",
            "status": "Expired"
        },
```


**Status Values:**
- `Active` - More than 90 days until expiration
- `Expiring in 90 days` - 60-90 days until expiration
- `Expiring in 60 days` - Less than 60 days until expiration
- `Expired` - Past expiration date (displays 0 days)

**Key Features:**
- Expired licenses show `displayDaysUntilExpiration: 0` (no negative values)
- Includes purchase date for timeline start point
- Currency hardcoded to "OMR"
- Total cost includes license + support costs
- Sorted by expiration date

---

### 13. Active License Aging Overview
Get aging analysis of active licenses showing time in use.

**Endpoint:**
```http
GET /analytics/license/aging-overview
```

**Description:** Card 13 - Shows how long each active license has been in use (age in months from purchase date)

**Response:**
```json
{
    "licenses": [
        {
            "licenseId": 132,
            "licenseName": {
                "ar": "جدار الحماية Fortinet Maqnaat",
                "de": "Fortinet Maqnaat-Firewall",
                "en": "Fortinet Maqnaat Firewall",
                "fr": "Pare-feu Fortinet Maqnaat",
                "sw": "Fortinet Maqnaat Firewall"
            },
            "ageInMonths": 5,
            "status": "Active"
        },
        {
            "licenseId": 128,
            "licenseName": {
                "ar": "جدار حماية تطبيقات الويب",
                "de": "Webanwendungs-Firewall",
                "en": "Web application firewall",
                "fr": "Pare-feu d'applications Web",
                "sw": "Maombi ya Wavuti Firewall"
            },
            "ageInMonths": 1,
            "status": "Active"
        }
    ]
}
```

**Response Type:** `LicenseAgingOverviewDto`

**Age Calculation:**
```sql
EXTRACT(YEAR FROM AGE(CURRENT_DATE, purchase_date)) * 12 + 
EXTRACT(MONTH FROM AGE(CURRENT_DATE, purchase_date))
```

**Status Values:**
- `Active` - More than 90 days until expiration
- `Expiring soon` - Within 90 days of expiration

**Key Features:**
- Only includes active licenses (status_code = 'ACTIVE')
- Age calculated in months from purchase date
- Sorted by age (newest first)
- Includes vendor translations

---

## Common Response Patterns

### Multi-language Support
All name fields support multiple languages:
```json
{
  "en": "English name",
  "ar": "الاسم بالعربية",
  "de": "Deutscher Name",
  "fr": "Nom français",
  "sw": "Jina la Kiswahili"
}
```

### Percentage Calculations
All percentages are:
- Rounded to 2 decimal places
- Calculated relative to the appropriate total
- Returned as Double type

### Currency
- All monetary values in Omani Rial (OMR)
- Formatted to 2 decimal places

### Date Format
- ISO 8601 format: `YYYY-MM-DD`
- Example: `2025-11-12`

## Data Sources

### Primary Tables
- `sam_license` - Main license records
- `sam_vendor` - Vendor information
- `public.enums` - Status and category enums with translations

### Key Fields
- `purchase_date` - License purchase/start date
- `expiration_date` - License expiration date
- `status_code` - License status (ACTIVE, INACTIVE, etc.)
- `license_cost` - Base license cost
- `support_cost` - Annual support/maintenance cost

## Business Rules

### Status Determination
1. **Active**: `status_code = 'ACTIVE'` and more than 90 days until expiration
2. **Expiring Soon**: Within 90 days of expiration
3. **Expired**: Past expiration date

### Cost Calculations
- Total Cost = License Cost + Support Cost
- All costs normalized to annual amounts
- Support cost may be 0 if not applicable

### Vendor Categorization
- "Uncategorized" used for unmapped vendors
- "Other" used for aggregated small vendors

## Notes

- All queries filter by active tenant
- Empty translations fallback to English or "Unknown"
- Null values handled gracefully in responses
- Percentages sum to 100% within each category
- Timeline defaults to ±1 year from current date
- Aging calculation uses PostgreSQL AGE function for accuracy

## Error Handling

All endpoints return standard HTTP status codes:
- `200 OK` - Successful request
- `400 Bad Request` - Invalid parameters
- `500 Internal Server Error` - Server-side error

Error responses include descriptive messages for troubleshooting.
