# Organization Dashboard Cards - Drill-Down API

This document describes the drill-down endpoints for Organization Dashboard Cards analytics.

## Endpoints

### 1. Total Positions - Details

**GET** `/analytics/organization-dashboard/total-positions/details`

Returns detailed list of all positions in the organization.

**Query Parameters:**
- `page` (optional, int, default: 0) - Page number
- `size` (optional, int, default: 10) - Page size

**Response:**
```json
        {
            "id": 8086,
            "nameTranslations": {
                "ar": "مكتب الأمن",
                "de": "Sicherheitsbüro",
                "en": "Security Office",
                "fr": "Bureau de sécurité",
                "sw": "Ofisi ya Usalama"
            },
            "nodeType": {
                "ar": "مكتب",
                "de": "Büro",
                "en": "Office",
                "fr": "bureau",
                "sw": "Ofisi"
            },
            "nodeCategory": {
                "ar": "الصحة والسلامة",
                "de": "Gesundheit und Sicherheit",
                "en": "Health and Safety",
                "fr": "Santé et sécurité",
                "sw": "Afya na usalama"
            },
            "statusCode": "ACTIVE",
            "parentId": 8085,
            "parentName": {
                "ar": "الوزير",
                "de": "Minister",
                "en": "Minister",
                "fr": "Ministre",
                "sw": "Waziri"
            },
            "childrenCount": 2
        }
    ],
    "totalCount": 942,
    "totalPages": 95,
    "currentPage": 0,
    "pageSize": 10
}
```

---

### 2. Top Functional Category - Details

**GET** `/analytics/organization-dashboard/top-functional-category/details?categoryId=131`

Returns detailed list of positions for a specific functional category.

**Query Parameters:**
- `categoryId` (required, Long) - Functional category ID (node_category_id)
- `page` (optional, int, default: 0) - Page number
- `size` (optional, int, default: 10) - Page size

**Response:** Same structure as above
```json
        {
            "id": 8120,
            "nameTranslations": {
                "ar": "قسم المتابعة بمكتب الوزير",
                "de": "Follow -up -Abteilung im Büro des Ministers",
                "en": "Performance Follow -up Department at the President's Office",
                "fr": "Suivi du département du bureau du ministre",
                "sw": "Fuata -Up idara katika Ofisi ya Waziri"
            },
            "nodeType": {
                "ar": "قسم",
                "de": "zu teilen",
                "en": "Section",
                "fr": "diviser",
                "sw": "kugawa"
            },
            "nodeCategory": {
                "ar": "العلاقات العامة والاتصالات",
                "de": "Öffentlichkeitsarbeit und Kommunikation",
                "en": "Public Relations and Communications",
                "fr": "Relations publiques et communications",
                "sw": "Mahusiano ya umma na mawasiliano"
            },
            "statusCode": "ACTIVE",
            "parentId": 8199,
            "parentName": {
                "ar": "دائرة التنسيق والمتابعة",
                "de": "Koordination und Follow -up -Abteilung",
                "en": "Strategic Coordination and Follow -up Department",
                "fr": "Coordination et département de suivi",
                "sw": "Uratibu na Idara ya kufuata"
            },
            "childrenCount": 2
        }
    ],
    "totalCount": 123,
    "totalPages": 13,
    "currentPage": 0,
    "pageSize": 10
}
```
---

### 3. Directorates - Details

**GET** `/analytics/organization-dashboard/directorates/details`

Returns detailed list of all directorates in the organization.

**Query Parameters:**
- `page` (optional, int, default: 0) - Page number
- `size` (optional, int, default: 10) - Page size

**Response:** Same structure as above (with `nodeType`: "DIRECTORATE")
```json
        {
            "id": 8470,
            "nameTranslations": {
                "ar": "المديرية العامة للمشاريع والصيانة في محافظة ظفار",
                "de": "Die Generaldirektion für Projekte und Wartung in Dhofar Governorate",
                "en": "General Directorate of Projects and Maintenance in Dhofar Governorate",
                "fr": "La Direction générale des projets et de la maintenance dans le gouvernorat du DHOFAR",
                "sw": "Kurugenzi Mkuu wa Miradi na Matengenezo katika Dhofar Gavana"
            },
            "nodeType": {
                "ar": "مديرية",
                "de": "Bezirk",
                "en": "Directorate",
                "fr": "District",
                "sw": "Wilaya"
            },
            "nodeCategory": {},
            "statusCode": "ACTIVE",
            "parentId": 8085,
            "parentName": {
                "ar": "الوزير",
                "de": "Minister",
                "en": "Minister",
                "fr": "Ministre",
                "sw": "Waziri"
            },
            "childrenCount": 15
        }
    ],
    "totalCount": 7,
    "totalPages": 1,
    "currentPage": 0,
    "pageSize": 10
}
```

---

### 4. Departments - Details

**GET** `/analytics/organization-dashboard/departments/details`

Returns detailed list of all departments in the organization.

**Query Parameters:**
- `page` (optional, int, default: 0) - Page number
- `size` (optional, int, default: 10) - Page size

**Response:** Same structure as above (with `nodeType`: "DEPARTMENT")
```json
        {
            "id": 8193,
            "nameTranslations": {
                "ar": "دائرة التواصل والإعلام ",
                "de": "Kommunikations- und Informationsabteilung",
                "en": "Institutional Media and Communication Department",
                "fr": "Département de communication et d'information",
                "sw": "Idara ya Mawasiliano na Habari"
            },
            "nodeType": {
                "ar": "دائرة",
                "de": "Kreis",
                "en": "Department",
                "fr": "cercle",
                "sw": "Mzunguko"
            },
            "nodeCategory": {
                "ar": "العلاقات العامة والاتصالات",
                "de": "Öffentlichkeitsarbeit und Kommunikation",
                "en": "Public Relations and Communications",
                "fr": "Relations publiques et communications",
                "sw": "Mahusiano ya umma na mawasiliano"
            },
            "statusCode": "ACTIVE",
            "parentId": 8085,
            "parentName": {
                "ar": "الوزير",
                "de": "Minister",
                "en": "Minister",
                "fr": "Ministre",
                "sw": "Waziri"
            },
            "childrenCount": 6
        }
    ],
    "totalCount": 71,
    "totalPages": 8,
    "currentPage": 0,
    "pageSize": 10
}
 ```

---

### 5. Sections - Details

**GET** `/analytics/organization-dashboard/sections/details`

Returns detailed list of all sections in the organization.

**Query Parameters:**
- `page` (optional, int, default: 0) - Page number
- `size` (optional, int, default: 10) - Page size

**Response:** Same structure as above (with `nodeType`: "SECTION")
```json
        {
            "id": 8119,
            "nameTranslations": {
                "ar": "قسم التنسيق بمكتب الوزير",
                "de": "Koordinierungsabteilung im Büro des Ministers",
                "en": "Administrative Supervision Department",
                "fr": "Département de coordination au bureau du ministre",
                "sw": "Idara ya uratibu katika ofisi ya waziri"
            },
            "nodeType": {
                "ar": "قسم",
                "de": "zu teilen",
                "en": "Section",
                "fr": "diviser",
                "sw": "kugawa"
            },
            "nodeCategory": {
                "ar": "العلاقات العامة والاتصالات",
                "de": "Öffentlichkeitsarbeit und Kommunikation",
                "en": "Public Relations and Communications",
                "fr": "Relations publiques et communications",
                "sw": "Mahusiano ya umma na mawasiliano"
            },
            "statusCode": "ACTIVE",
            "parentId": 8199,
            "parentName": {
                "ar": "دائرة التنسيق والمتابعة",
                "de": "Koordination und Follow -up -Abteilung",
                "en": "Strategic Coordination and Follow -up Department",
                "fr": "Coordination et département de suivi",
                "sw": "Uratibu na Idara ya kufuata"
            },
            "childrenCount": 2
        }
    ],
    "totalCount": 256,
    "totalPages": 26,
    "currentPage": 0,
    "pageSize": 10
}
```

---
# Organization Dashboard Charts - Drill-Down API

This document describes the drill-down endpoints for Organization Dashboard Charts analytics.

## Endpoints

### 1. Employees by Job Rank - Details

**GET** `/analytics/organization-dashboard/employees-by-job-rank/details?jobRank=1&jobLevel=119`

Returns detailed employee list for a specific job level and rank combination.

**Query Parameters:**
- `jobLevel` (required, Long) - Job level ID
- `jobRank` (optional, Integer) - Job rank number (filter by specific rank)
- `page` (optional, int, default: 0) - Page number
- `size` (optional, int, default: 10) - Page size

**Response:**
```json
{
    "employees": [
        {
            "id": 8085,
            "nameTranslations": {
                "ar": "الوزير",
                "de": "Minister",
                "en": "Minister",
                "fr": "Ministre",
                "sw": "Waziri"
            },
            "jobLevelTranslations": {
                "ar": "وزير / رئيس الوحدة",
                "de": "Minister / Leiter der Einheit",
                "en": "Minister / Unit Head",
                "fr": "Ministre / chef de l'unité",
                "sw": "Waziri / Mkuu wa Kitengo"
            },
            "jobRank": 1,
            "unitNameTranslations": {
                "ar": "الجهة التجريبية",
                "de": "Die experimentelle Partei",
                "en": "The experimental party",
                "fr": "La partie expérimentale",
                "sw": "Chama cha majaribio"
            },
            "specializationTranslations": {},
            "statusCode": "ACTIVE"
        }
    ],
    "totalCount": 1,
    "totalPages": 1,
    "currentPage": 0,
    "pageSize": 10
}

```

---

### 2. Department Size Overview - Details

**GET** `/analytics/organization-dashboard/department-size-overview/details?unitId=8203`
```json
        {
            "id": 8962,
            "nameTranslations": {
                "ar": "موظف قسم تراخيص المنشآت الفندقية",
                "de": "Ein Mitarbeiter der Hoteleinrichtungen Lizenzen",
                "en": "Employee of the Project Licensing Department",
                "fr": "Un employé des licences d'établissements d'hôtel",
                "sw": "Mfanyikazi wa leseni za uanzishaji wa hoteli"
            },
            "jobLevelTranslations": {
                "ar": "موظف",
                "de": "Mitarbeiter",
                "en": "Employee",
                "fr": "employé",
                "sw": "mfanyakazi"
            },
            "jobRank": 9,
            "unitNameTranslations": {
                "ar": "قسم تراخيص المنشآت الفندقية",
                "de": "Department of Hotel Facilities Lizenzen",
                "en": "Department of Operating Facilities Licenses",
                "fr": "Licence des installations du Département de l'hôtel",
                "sw": "Idara ya leseni za vifaa vya hoteli"
            },
            "specializationTranslations": {
                "ar": "القانون والامتثال",
                "de": "Gesetz und Konformität",
                "en": "Legal and Compliance",
                "fr": "Droit et conformité",
                "sw": "Sheria na kufuata"
            },
            "statusCode": "ACTIVE"
        }
    ],
    "totalCount": 40,
    "totalPages": 4,
    "currentPage": 0,
    "pageSize": 10
}
```
**Query Parameters:**
- `unitId` (required, Long) - Organizational unit ID
- `jobLevel` (optional, Long) - Filter by job level ID
- `page` (optional, int, default: 0) - Page number
- `size` (optional, int, default: 10) - Page size

**Response:** Same structure as above

---

### 3. Employee Job Level Breakdown - Details

**GET** `/analytics/organization-dashboard/employee-job-level-breakdown/details?jobLevel=120`

Returns detailed employee list for a specific job level.

```json
{
    "employees": [
        {
            "id": 8089,
            "nameTranslations": {
                "ar": "وكيل الوزارة للمشاريع",
                "de": "Unterstaatssekretär für Projekte",
                "en": "Deputy Minister for Projects",
                "fr": "Sous-secrétaire pour les projets",
                "sw": "Undersecretary kwa miradi"
            },
            "jobLevelTranslations": {
                "ar": "وكيل وزارة",
                "de": "Unterstaatssekretär des Ministeriums",
                "en": "Undersecretary",
                "fr": "Sous-secrétaire du ministère",
                "sw": "Undersecretary ya huduma"
            },
            "jobRank": 2,
            "unitNameTranslations": {
                "ar": "الوزير",
                "de": "Minister",
                "en": "Minister",
                "fr": "Ministre",
                "sw": "Waziri"
            },
            "specializationTranslations": {
                "ar": "الموارد البشرية",
                "de": "Personalwesen",
                "en": "Human Resources",
                "fr": "Ressources humaines",
                "sw": "Rasilimali watu"
            },
            "statusCode": "ACTIVE"
        },
        {
            "id": 8084,
            "nameTranslations": {
                "ar": "وكيل الوزارة للتراث",
                "de": "Unterstaatssekretär des Erbeministeriums",
                "en": "Undersecretary for institutional development",
                "fr": "Sous-secrétaire du ministère du Heritage",
                "sw": "Undersecretary ya Wizara ya Urithi"
            },
            "jobLevelTranslations": {
                "ar": "وكيل وزارة",
                "de": "Unterstaatssekretär des Ministeriums",
                "en": "Undersecretary",
                "fr": "Sous-secrétaire du ministère",
                "sw": "Undersecretary ya huduma"
            },
            "jobRank": 2,
            "unitNameTranslations": {
                "ar": "الوزير",
                "de": "Minister",
                "en": "Minister",
                "fr": "Ministre",
                "sw": "Waziri"
            },
            "specializationTranslations": {},
            "statusCode": "ACTIVE"
        }
    ],
    "totalCount": 2,
    "totalPages": 1,
    "currentPage": 0,
    "pageSize": 10
}

```

**Query Parameters:**
- `jobLevel` (required, Long) - Job level ID
- `page` (optional, int, default: 0) - Page number
- `size` (optional, int, default: 10) - Page size

**Response:** Same structure as above

---

### 4. Human Capital by Specialization - Details

**GET** `/analytics/organization-dashboard/human-capital-by-specialization/details?specializationId=131`

Returns detailed employee list for a specific specialization (node category).

**Query Parameters:**
- `specializationId` (required, Long) - Specialization/category ID (node_category_id)
- `directorateId` (optional, Long) - Filter by directorate ID
- `page` (optional, int, default: 0) - Page number
- `size` (optional, int, default: 10) - Page size

**Response:** Same structure as above
``` json 
            "id": 8477,
            "nameTranslations": {
                "ar": "رئيس قسم التنسيق والمتابعة (المديرية العامة للشئون الإدارية والمالية)",
                "de": "Leiter des Abteilung für Koordination und Follow -up (Generaldirektion für Verwaltungs- und Finanzangelegenheiten)",
                "en": "Director of the Coordination and Follow -up Department",
                "fr": "Chef du ministère de la coordination et du suivi -Up (Direction générale des affaires administratives et financières)",
                "sw": "Mkuu wa Idara ya Uratibu na Kufuata -Up (Kurugenzi Mkuu wa Mambo ya Tawala na Fedha)"
            },
            "jobLevelTranslations": {
                "ar": "رئيس قسم",
                "de": "Kopf",
                "en": "Section Head",
                "fr": "Tête",
                "sw": "Kichwa"
            },
            "jobRank": 8,
            "unitNameTranslations": {
                "ar": "قسم التنسيق والمتابعة (المديرية العامة للشؤون الإدارية والمالية)",
                "de": "Abteilung für Koordination und Follow -up (Generaldirektion für Verwaltungs- und Finanzangelegenheiten)",
                "en": "Administrative Coordination and Follow -up Department",
                "fr": "Département de coordination et de suivi -Up (Direction générale des affaires administratives et financières)",
                "sw": "Idara ya uratibu na kufuata -UP (Kurugenzi Mkuu wa Mambo ya Tawala na Fedha)"
            },
            "specializationTranslations": {
                "ar": "العلاقات العامة والاتصالات",
                "de": "Öffentlichkeitsarbeit und Kommunikation",
                "en": "Public Relations and Communications",
                "fr": "Relations publiques et communications",
                "sw": "Mahusiano ya umma na mawasiliano"
            },
            "statusCode": "ACTIVE"
        }
    ],
    "totalCount": 76,
    "totalPages": 8,
    "currentPage": 0,
    "pageSize": 10
}

```
