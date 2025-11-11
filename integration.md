# Integration Analytics API Documentation

Base URL: `/analytics/integration`

## Endpoints

### 1. Total Integrations
**GET** `/analytics/integration/total`

Returns the total count of active integrations in the system.

**Response:**
```json
{
  
    "totalIntegrations": 15,
    "asSourceAuthority": 1,
    "asReceivingAuthority": 14
}

```

---

### 2. Applications in Use
**GET** `/analytics/integration/applications`

Returns the count of applications that are currently using integrations.

**Response:**
```json
{
    "totalApplications": 18,
    "sourceApplications": 1,
    "receivingApplications": 17
}
```

---

### 3. Security Access Overview
**GET** `/analytics/integration/security-overview`

Provides overview of security and access metrics for integrations.

**Response:**
```json
{
    "topIntegrationType": {
        "nameTranslations": {
            "ar": "API",
            "de": "API",
            "en": "API",
            "fr": "API",
            "sw": "API"
        },
        "percentage": 67.0
    },
    "topIntegrationMethod": {
        "nameTranslations": {
            "ar": "REST API",
            "de": "Ruhe -API",
            "en": "REST API",
            "fr": "API REST",
            "sw": "REST API"
        },
        "percentage": 53.0
    },
    "topAccessLevel": {
        "nameTranslations": {
            "ar": "خاص",
            "de": "Privat",
            "en": "Private",
            "fr": "privé",
            "sw": "Privat"
        },
        "percentage": 47.0
    }
}
```

---

### 4. Most Integrated Authorities
**GET** `/analytics/integration/most-integrated-authorities?limit=5`

Returns the top authorities with the most integrations.

**Query Parameters:**
- `limit` (optional, default: 5) - Number of top authorities to return

**Response:**
```json
{
    "authorities": [
        {
            "authorityId": 2221,
            "authorityName": {
                "ar": "جهاز الرقابة المالية والإدارية للدولة",
                "de": "Der finanzielle und administrative Kontrollapparat des Staates",
                "en": "The financial and administrative control apparatus of the state",
                "fr": "L'appareil de contrôle financier et administratif de l'État",
                "sw": "Vifaa vya kudhibiti kifedha na kiutawala vya serikali"
            },
            "integrationCount": 3
        },
        {
            "authorityId": 2156,
            "authorityName": {
                "ar": "وزارة المالية",
                "de": "Finanzministerium",
                "en": "Ministry of Finance",
                "fr": "ministère des Finances",
                "sw": "Wizara ya Fedha"
            },
            "integrationCount": 2
        },
        {
            "authorityId": 2220,
            "authorityName": {
                "ar": "صندوق تقاعد موظفي الخدمة المدنية",
                "de": "Rentenfonds des öffentlichen Dienstes",
                "en": "Civil Service Pension Fund",
                "fr": "Fonds de retraite de la fonction publique",
                "sw": "Mfuko wa pensheni wa huduma ya umma"
            },
            "integrationCount": 2
        },
        {
            "authorityId": 2226,
            "authorityName": {
                "ar": "هيئة الخدمات المالية",
                "de": "Finanzdienstleistungsbehörde",
                "en": "Financial Services Authority",
                "fr": "Autorité des services financiers",
                "sw": "Mamlaka ya huduma za kifedha"
            },
            "integrationCount": 2
        },
        {
            "authorityId": 2204,
            "authorityName": {
                "ar": "وزارة العدل والشؤون القانونية",
                "de": "Justizministerium und rechtliche Angelegenheiten",
                "en": "Ministry of Justice and Legal Affairs",
                "fr": "Ministère de la Justice et des Affaires juridiques",
                "sw": "Wizara ya Haki na Mambo ya Sheria"
            },
            "integrationCount": 1
        }
    ]
}
```

---

### 5. Integration Type Breakdown
**GET** `/analytics/integration/by-type`

Shows distribution of integrations by type (API, Database, File Transfer, etc.).

**Response:**
```json
{
    "items": [
        {
            "nameTranslations": {
                "ar": "API",
                "de": "API",
                "en": "API",
                "fr": "API",
                "sw": "API"
            },
            "percentage": 66.67,
            "count": 10
        },
        {
            "nameTranslations": {
                "ar": "قاعدة بيانات",
                "de": "Datenbank",
                "en": "Database",
                "fr": "Base de données",
                "sw": "Hifadhidata"
            },
            "percentage": 13.33,
            "count": 2
        },
        {
            "nameTranslations": {
                "ar": "نقل الملفات",
                "de": "Dateien übertragen",
                "en": "File Transfer",
                "fr": "Transfert de fichiers",
                "sw": "Kuhamisha faili"
            },
            "percentage": 13.33,
            "count": 2
        },
        {
            "nameTranslations": {
                "en": "Unspecified",
                "ar": "غير محدد",
                "fr": "Non spécifié",
                "de": "Nicht spezifiziert",
                "sw": "Haijafafanuliwi"
            },
            "percentage": 6.67,
            "count": 1
        }
    ]
}
```

---

### 6. Integration Method Breakdown
**GET** `/analytics/integration/by-method`

Shows distribution of integrations by communication method (HTTP, SOAP, gRPC, etc.).

**Response:**
```json
{
    "items": [
        {
            "nameTranslations": {
                "ar": "REST API",
                "de": "Ruhe -API",
                "en": "REST API",
                "fr": "API REST",
                "sw": "REST API"
            },
            "percentage": 53.33,
            "count": 8
        },
        {
            "nameTranslations": {
                "ar": "FTP",
                "de": "Ftp",
                "en": "FTP",
                "fr": "FTP",
                "sw": "Ftp"
            },
            "percentage": 13.33,
            "count": 2
        },
        {
            "nameTranslations": {
                "ar": "SAML",
                "de": "Saml",
                "en": "SAML",
                "fr": "Saml",
                "sw": "Saml"
            },
            "percentage": 13.33,
            "count": 2
        },
        {
            "nameTranslations": {
                "ar": "SOAP",
                "de": "Seife",
                "en": "SOAP",
                "fr": "Savon",
                "sw": "Sabuni"
            },
            "percentage": 6.67,
            "count": 1
        },
        {
            "nameTranslations": {
                "ar": "آخر",
                "de": "zuletzt",
                "en": "Other",
                "fr": "dernier",
                "sw": "Mwisho"
            },
            "percentage": 6.67,
            "count": 1
        },
        {
            "nameTranslations": {
                "en": "Unspecified",
                "ar": "غير محدد",
                "fr": "Non spécifié",
                "de": "Nicht spezifiziert",
                "sw": "Haijafafanuliwi"
            },
            "percentage": 6.67,
            "count": 1
        }
    ]
}
```

---

### 7. Access Level Breakdown
**GET** `/analytics/integration/access-level`

Shows distribution of integrations by access level (Public, Private, Internal, etc.).

**Response:**
```json
{
    "items": [
        {
            "nameTranslations": {
                "ar": "خاص",
                "de": "Privat",
                "en": "Private",
                "fr": "privé",
                "sw": "Privat"
            },
            "percentage": 46.67,
            "count": 7
        },
        {
            "nameTranslations": {
                "ar": "محمي",
                "de": "geschützt",
                "en": "Protected",
                "fr": "protégé",
                "sw": "kulindwa"
            },
            "percentage": 40.0,
            "count": 6
        },
        {
            "nameTranslations": {
                "ar": "عام",
                "de": "allgemein",
                "en": "Public",
                "fr": "général",
                "sw": "Mkuu"
            },
            "percentage": 6.67,
            "count": 1
        },
        {
            "nameTranslations": {
                "en": "Unspecified",
                "ar": "غير محدد",
                "fr": "Non spécifié",
                "de": "Nicht spezifiziert",
                "sw": "Haijafafanuliwi"
            },
            "percentage": 6.67,
            "count": 1
        }
    ]
}
```

---

### 8. Integration Usage by Application
**GET** `/analytics/integration/usage-by-application`

Shows which applications are using the most integrations.

**Response:**
```json
{
    "applications": [
        {
            "applicationId": 58,
            "nameTranslations": {
                "ar": "Odoo ERP",
                "de": "Odoo ERP",
                "en": "Odoo ERP",
                "fr": "Odoo ERP",
                "sw": "ODOO ERP"
            },
            "integrationCount": 5
        },
        {
            "applicationId": 63,
            "nameTranslations": {
                "ar": "Cisco SecureX",
                "de": "Cisco SecureX",
                "en": "Cisco SecureX",
                "fr": "Cisco SecureX",
                "sw": "Cisco SalamaX"
            },
            "integrationCount": 4
        },
        {
            "applicationId": 52,
            "nameTranslations": {
                "ar": "TADAFUR",
                "de": "TADAFUR",
                "en": "TADAFUR",
                "fr": "TADAFUR",
                "sw": "Tadafur"
            },
            "integrationCount": 4
        },
        {
            "applicationId": 54,
            "nameTranslations": {
                "ar": "إيفانتي",
                "de": "Ivanti",
                "en": "Ivanti",
                "fr": "Ivanti",
                "sw": "Ivanti"
            },
            "integrationCount": 4
        },
        {
            "applicationId": 50,
            "nameTranslations": {
                "ar": "تطبيق EPM",
                "de": "EPM-Anwendung",
                "en": "EPM application",
                "fr": "Application EPM",
                "sw": "Maombi ya EPM"
            },
            "integrationCount": 4
        },
        {
            "applicationId": 65,
            "nameTranslations": {
                "ar": "GitLab",
                "de": "GitLab",
                "en": "GitLab",
                "fr": "GitLab",
                "sw": "Gitlab"
            },
            "integrationCount": 3
        },
        {
            "applicationId": 64,
            "nameTranslations": {
                "ar": "Palo Alto Prisma Cloud",
                "de": "Palo Alto Prisma Cloud",
                "en": "Palo Alto Prisma Cloud",
                "fr": "Palo Alto Prisma Nuage",
                "sw": "Palo Alto Prisma Cloud"
            },
            "integrationCount": 3
        },
        {
            "applicationId": 46,
            "nameTranslations": {
                "ar": "SAP S/4HANA",
                "de": "SAP S/4HANA",
                "en": "SAP S/4HANA",
                "fr": "SAPS/4HANA",
                "sw": "SAP S/4HANA"
            },
            "integrationCount": 3
        },
        {
            "applicationId": 62,
            "nameTranslations": {
                "ar": "Slack",
                "de": "Locker",
                "en": "Slack",
                "fr": "Mou",
                "sw": "Slack"
            },
            "integrationCount": 3
        },
        {
            "applicationId": 60,
            "nameTranslations": {
                "ar": "Bayzat",
                "de": "Bayzat",
                "en": "Bayzat",
                "fr": "Bayzat",
                "sw": "Bayzat"
            },
            "integrationCount": 2
        },
        {
            "applicationId": 56,
            "nameTranslations": {
                "ar": "Panorama",
                "de": "Panorama",
                "en": "Panorama",
                "fr": "Panorama",
                "sw": "Panorama"
            },
            "integrationCount": 2
        },
        {
            "applicationId": 61,
            "nameTranslations": {
                "ar": "Qlik Sense",
                "de": "Qlik Sense",
                "en": "Qlik Sense",
                "fr": "Qlik Sense",
                "sw": "Qlik akili"
            },
            "integrationCount": 2
        },
        {
            "applicationId": 59,
            "nameTranslations": {
                "ar": "SAP HCM",
                "de": "SAP HCM",
                "en": "SAP HCM",
                "fr": "SAP HCM",
                "sw": "SAP HCM"
            },
            "integrationCount": 2
        },
        {
            "applicationId": 48,
            "nameTranslations": {
                "ar": "Google Workspace",
                "de": "Google Workspace",
                "en": "Google Workspace",
                "fr": "Espace de travail Google",
                "sw": "Nafasi ya kazi ya Google"
            },
            "integrationCount": 1
        },
        {
            "applicationId": 47,
            "nameTranslations": {
                "ar": "Microsoft Power BI",
                "de": "Microsoft Power BI",
                "en": "Microsoft Power BI",
                "fr": "Microsoft Power BI",
                "sw": "Microsoft Power BI"
            },
            "integrationCount": 1
        },
        {
            "applicationId": 45,
            "nameTranslations": {
                "ar": "Oracle ERP Cloud",
                "de": "Oracle ERP Cloud",
                "en": "Oracle ERP Cloud",
                "fr": "Oracle ERP Cloud",
                "sw": "Oracle ERP Cloud"
            },
            "integrationCount": 1
        },
        {
            "applicationId": 49,
            "nameTranslations": {
                "ar": "SAP SuccessFactors",
                "de": "SAP SuccessFactors",
                "en": "SAP SuccessFactors",
                "fr": "Facteurs de réussite SAP",
                "sw": "SAP Mafanikio"
            },
            "integrationCount": 1
        }
    ]
}
```

---

### 9. Integration Network Overview
**GET** `/analytics/integration/network-overview`

Provides comprehensive network overview including connections, authorities, and applications.

**Response:**
```json
{
    "currentAuthority": {
        "authorityId": 2292,
        "nameTranslations": {
            "ar": "مؤسسة نموذجية",
            "de": "Typisch",
            "en": "Typical",
            "fr": "Typique",
            "sw": "Kawaida"
        },
        "totalConnections": 15
    },
    "asReceivingAuthority": [],
    "asSourceAuthority": [
        {
            "partnerAuthorityId": 2221,
            "partnerNameTranslations": {
                "ar": "جهاز الرقابة المالية والإدارية للدولة",
                "de": "Der finanzielle und administrative Kontrollapparat des Staates",
                "en": "The financial and administrative control apparatus of the state",
                "fr": "L'appareil de contrôle financier et administratif de l'État",
                "sw": "Vifaa vya kudhibiti kifedha na kiutawala vya serikali"
            },
            "integrationCount": 3
        },
        {
            "partnerAuthorityId": 2226,
            "partnerNameTranslations": {
                "ar": "هيئة الخدمات المالية",
                "de": "Finanzdienstleistungsbehörde",
                "en": "Financial Services Authority",
                "fr": "Autorité des services financiers",
                "sw": "Mamlaka ya huduma za kifedha"
            },
            "integrationCount": 2
        },
        {
            "partnerAuthorityId": 2156,
            "partnerNameTranslations": {
                "ar": "وزارة المالية",
                "de": "Finanzministerium",
                "en": "Ministry of Finance",
                "fr": "ministère des Finances",
                "sw": "Wizara ya Fedha"
            },
            "integrationCount": 2
        },
        {
            "partnerAuthorityId": 2220,
            "partnerNameTranslations": {
                "ar": "صندوق تقاعد موظفي الخدمة المدنية",
                "de": "Rentenfonds des öffentlichen Dienstes",
                "en": "Civil Service Pension Fund",
                "fr": "Fonds de retraite de la fonction publique",
                "sw": "Mfuko wa pensheni wa huduma ya umma"
            },
            "integrationCount": 2
        },
        {
            "partnerAuthorityId": 2232,
            "partnerNameTranslations": {
                "ar": "وزارة التنمية الإجتماعية",
                "de": "Ministerium für soziale Entwicklung",
                "en": "Ministry of Social Development",
                "fr": "Ministère du développement social",
                "sw": "Huduma ya Maendeleo ya Jamii"
            },
            "integrationCount": 1
        },
        {
            "partnerAuthorityId": 2234,
            "partnerNameTranslations": {
                "ar": "هيئة حماية المستهلك",
                "de": "Verbraucherschutzbehörde",
                "en": "Consumer Protection Authority",
                "fr": "Autorité de protection des consommateurs",
                "sw": "Mamlaka ya Ulinzi wa Watumiaji"
            },
            "integrationCount": 1
        },
        {
            "partnerAuthorityId": 110,
            "partnerNameTranslations": {
                "ar": "وزارة التجارة والصناعة وترويج الإستثمار",
                "de": "Ministerium für Handels-, Industrie- und Investitionsförderung",
                "en": "Ministry of Trade, Industry and Investment Promotion",
                "fr": "Ministère du commerce, de l'industrie et de la promotion des investissements",
                "sw": "Wizara ya Biashara, Viwanda na Ukuzaji wa Uwekezaji"
            },
            "integrationCount": 1
        },
        {
            "partnerAuthorityId": 2287,
            "partnerNameTranslations": {
                "ar": "صندوق الحماية الاجتماعية",
                "de": "Sozialschutzfonds",
                "en": "Social Protection Fund",
                "fr": "Fonds de protection sociale",
                "sw": "Mfuko wa Ulinzi wa Jamii"
            },
            "integrationCount": 1
        },
        {
            "partnerAuthorityId": 124,
            "partnerNameTranslations": {
                "ar": "وزارة العمل",
                "de": "Arbeitsministerium",
                "en": "Ministry of Labor",
                "fr": "Ministère du Travail",
                "sw": "Wizara ya Kazi"
            },
            "integrationCount": 1
        },
        {
            "partnerAuthorityId": 2176,
            "partnerNameTranslations": {
                "ar": "وزارة الإعلام",
                "de": "Informationsministerium",
                "en": "Ministry of Information",
                "fr": "Ministère de l'Information",
                "sw": "Wizara ya Habari"
            },
            "integrationCount": 1
        },
        {
            "partnerAuthorityId": 2204,
            "partnerNameTranslations": {
                "ar": "وزارة العدل والشؤون القانونية",
                "de": "Justizministerium und rechtliche Angelegenheiten",
                "en": "Ministry of Justice and Legal Affairs",
                "fr": "Ministère de la Justice et des Affaires juridiques",
                "sw": "Wizara ya Haki na Mambo ya Sheria"
            },
            "integrationCount": 1
        }
    ]
}
```

---

## Notes

- All endpoints return data for active records only (`status_code = 'ACTIVE'`)
- Multilingual support: Response names include translations in English (en) and Arabic (ar)
- Percentages are rounded to 2 decimal places
- All count fields are integers (Long type)
- All percentage fields are decimals (Double type)
