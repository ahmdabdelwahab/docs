# Talent Analytics API Documentation

## Base Path
`/analytics/talent`

## Overview
The Talent Analytics API provides comprehensive insights into talent management, including skill distribution, seniority levels, nationality breakdown, and project involvement metrics.

---

## Endpoints

### 1. Get Talent Overview
Returns high-level statistics about the talent pool.

**Endpoint:** `GET /analytics/talent/overview`


```json
{
    "totalTalents": 12,
    "avgSkillsPerTalent": 1.8,
    "avgProjectsPerEmployee": 1.8
}
```



### 2. Get Top Skills
Returns the most frequently occurring skills among talents.

**Endpoint:** `GET /analytics/talent/top-skills`

**Parameters:**
| Parameter | Type    | Required | Default | Description                           |
|-----------|---------|----------|---------|---------------------------------------|
| `limit`   | Integer | No       | 5       | Number of top skills to return        |


```json
{
    "skills": [
        {
            "skillId": 6,
            "skillNameTranslations": {
                "ar": "التسويق الرقمي",
                "de": "Digitales Marketing",
                "en": "Digital Marketing",
                "fr": "Marketing numérique",
                "sw": "Uuzaji wa dijiti"
            },
            "talentCount": 3,
            "percentage": 25.0
        },
        {
            "skillId": 3,
            "skillNameTranslations": {
                "ar": "تحليل البيانات",
                "de": "Datenanalyse",
                "en": "Data Analysis",
                "fr": "Analyse des données",
                "sw": "Uchambuzi wa data"
            },
            "talentCount": 3,
            "percentage": 25.0
        },
```



### 3. Get Talent By Seniority
Returns talent distribution across seniority levels.

**Endpoint:** `GET /analytics/talent/by-seniority`

```json
{
    "totalTalents": 12,
    "seniorityLevels": [
        {
            "seniorityLevel": 427,
            "seniorityLevelNameTranslations": {},
            "talentCount": 1,
            "percentage": 8.33
        },
        {
            "seniorityLevel": 428,
            "seniorityLevelNameTranslations": {},
            "talentCount": 2,
            "percentage": 16.67
        },
        {
            "seniorityLevel": 639,
            "seniorityLevelNameTranslations": {
                "ar": "حديث التخرج",
                "de": "Redner",
                "en": "Fresh graduate",
                "fr": "Parleur",
                "sw": "Mzungumzaji"
            },
            "talentCount": 1,
            "percentage": 8.33
        },
        {
            "seniorityLevel": 641,
            "seniorityLevelNameTranslations": {
                "ar": "متوسط الخبرة",
                "de": "Durchschnittliche Erfahrung",
                "en": "Mid-level",
                "fr": "Expérience moyenne",
                "sw": "Uzoefu wa wastani"
            },
            "talentCount": 1,
            "percentage": 8.33
        },
        {
            "seniorityLevel": 642,
            "seniorityLevelNameTranslations": {
                "ar": "خبير",
                "de": "Experte",
                "en": "Senior",
                "fr": "expert",
                "sw": "Mtaalam"
            },
            "talentCount": 4,
            "percentage": 33.33
        },
```

4- Get Talent by experience

**Endpoint:** `GET /analytics/talent/by-experience`

```json
{
    "experienceDistribution": [
        {
            "yearsOfExperience": 1,
            "numberOfEmployees": 4
        },
        {
            "yearsOfExperience": 2,
            "numberOfEmployees": 1
        },
        {
            "yearsOfExperience": 9,
            "numberOfEmployees": 1
        },
        {
            "yearsOfExperience": 10,
            "numberOfEmployees": 1
        },
        {
            "yearsOfExperience": 15,
            "numberOfEmployees": 1
        },
        {
            "yearsOfExperience": 18,
            "numberOfEmployees": 1
        },
        {
            "yearsOfExperience": 20,
            "numberOfEmployees": 1
        },
        {
            "yearsOfExperience": 23,
            "numberOfEmployees": 1
        },
        {
            "yearsOfExperience": 30,
            "numberOfEmployees": 1
        }
    ]
}
```


---



### 4. Get Talent By Nationality
Returns talent distribution by nationality.

**Endpoint:** `GET /analytics/talent/by-nationality`



```json
{
    "totalTalents": 12,
    "nationalities": [
        {
            "nationalityId": 168,
            "nationalityNameTranslations": {
                "ar": "سلطنة عمان",
                "de": "Sultanat Oman",
                "en": "Sultanate of Oman",
                "fr": "Sultanat d'Oman",
                "sw": "Sultanate wa Oman"
            },
            "talentCount": 6,
            "percentage": 50.0
        },
        {
            "nationalityId": 3,
            "nationalityNameTranslations": {
                "ar": "ألبانيا",
                "de": "Albanien",
                "en": "Albania",
                "fr": "Albanie",
                "sw": "Albania"
            },
            "talentCount": 2,
            "percentage": 16.67
        },
```


---

### 5. Get Talent By Skill
Returns detailed breakdown of talents grouped by their skills.

**Endpoint:** `GET /analytics/talent/by-skill`


```json
{
    "totalTalents": 12,
    "skills": [
        {
            "skillId": 6,
            "skillNameTranslations": {
                "ar": "التسويق الرقمي",
                "de": "Digitales Marketing",
                "en": "Digital Marketing",
                "fr": "Marketing numérique",
                "sw": "Uuzaji wa dijiti"
            },
            "talentCount": 3,
            "percentage": 25.0
        },
        {
            "skillId": 3,
            "skillNameTranslations": {
                "ar": "تحليل البيانات",
                "de": "Datenanalyse",
                "en": "Data Analysis",
                "fr": "Analyse des données",
                "sw": "Uchambuzi wa data"
            },
            "talentCount": 3,
            "percentage": 25.0
        },
```

---

### 6. Get Talent Involvement
Returns metrics about talent involvement in projects and activities.

**Endpoint:** `GET /analytics/talent/involvement`

**Parameters:**
| Parameter  | Type   | Required | Default | Description                                    |
|------------|--------|----------|---------|------------------------------------------------|
| `filterBy` | String | No       | null    | Filter criteria ("certifications", "skills", "projects")   |


```json
{
    "talents": [
        {
            "talentId": 3,
            "talentNameTranslations": {
                "ar": "نورة الفارسية",
                "de": "Persische Noura",
                "en": "Noora Al Farsi",
                "fr": "Noura persan",
                "sw": "Uajemi Noura"
            },
            "skillsCount": 3,
            "projectsCount": 3,
            "certificationsCount": 3,
            "yearsOfExperience": 18
        },
        {
            "talentId": 1,
            "talentNameTranslations": {
                "ar": "سعيد الوهيبي",
                "de": "Saeed al -Wahaibi",
                "en": "Saeed Al Wahaibi",
                "fr": "Saeed al -wahaibi",
                "sw": "Saeed al -wahaibi"
            },
            "skillsCount": 3,
            "projectsCount": 2,
            "certificationsCount": 3,
            "yearsOfExperience": 15
        },
...
----



# Talent Skill & Certification Analytics API Documentation

## Overview

This document covers two talent analytics endpoints focused on skill category balance and certification completion tracking.

---

## 1. Skill Category Balance

Returns the distribution and balance of skills across different skill categories within the organization's talent pool.

### Endpoint

```
GET /analytics/talent/skill-category-balance
```

### Description

Analyzes the organization's skill portfolio by categorizing all talent skills into predefined categories (e.g., Technical, Management, Soft Skills, Domain Expertise) and calculating the distribution and balance across these categories. This helps identify skill gaps and areas of strength.

### Request

**HTTP Method:** GET

**No parameters required**

**Headers:**
```
Authorization: Bearer <token>
Content-Type: application/json
```

### Response

**Status Code:** 200 OK

**Response Body:**
```json
{
  "totalSkills": 450,
  "totalCategories": 5,
  "categoryBreakdown": [
    {
      "categoryId": "1",
      "categoryName": {
        "en": "Technical Skills",
        "ar": "المهارات التقنية",
        "de": "Technische Fähigkeiten",
        "fr": "Compétences techniques",
        "sw": "Ujuzi wa Kiufundi"
      },
      "skillCount": 180,
      "talentCount": 145,
      "percentage": 40.0,
      "avgProficiencyLevel": 3.2
    },
    {
      "categoryId": "2",
      "categoryName": {
        "en": "Management Skills",
        "ar": "مهارات الإدارة",
        "de": "Managementfähigkeiten",
        "fr": "Compétences en gestion",
        "sw": "Ujuzi wa Usimamizi"
      },
      "skillCount": 95,
      "talentCount": 78,
      "percentage": 21.1,
      "avgProficiencyLevel": 2.8
    },
    {
      "categoryId": "3",
      "categoryName": {
        "en": "Soft Skills",
        "ar": "المهارات الناعمة",
        "de": "Soft Skills",
        "fr": "Compétences générales",
        "sw": "Ujuzi Laini"
      },
      "skillCount": 85,
      "talentCount": 165,
      "percentage": 18.9,
      "avgProficiencyLevel": 3.5
    },
    {
      "categoryId": "4",
      "categoryName": {
        "en": "Domain Expertise",
        "ar": "الخبرة المجالية",
        "de": "Domänenkompetenz",
        "fr": "Expertise du domaine",
        "sw": "Utaalamu wa Eneo"
      },
      "skillCount": 65,
      "talentCount": 92,
      "percentage": 14.4,
      "avgProficiencyLevel": 3.8
    },
    {
      "categoryId": "5",
      "categoryName": {
        "en": "Language Skills",
        "ar": "المهارات اللغوية",
        "de": "Sprachkenntnisse",
        "fr": "Compétences linguistiques",
        "sw": "Ujuzi wa Lugha"
      },
      "skillCount": 25,
      "talentCount": 110,
      "percentage": 5.6,
      "avgProficiencyLevel": 2.9
    }
  ],
  "balanceScore": 0.72,
  "topCategory": {
    "en": "Technical Skills",
    "ar": "المهارات التقنية"
  },
  "underrepresentedCategory": {
    "en": "Language Skills",
    "ar": "المهارات اللغوية"
  }
}
```



## 2. Certification Completion Card

Returns a summary card showing certification completion statistics and trends within the organization.

### Endpoint

```
GET /analytics/talent/certification-completion
```

### Description

Provides a high-level overview of certification status across the talent pool, including completion rates, in-progress certifications, expiring certifications, and trends over time. This metric is crucial for compliance tracking, professional development monitoring, and certification program effectiveness.

### Request

**HTTP Method:** GET

**No parameters required**

**Headers:**
```
Authorization: Bearer <token>
Content-Type: application/json
```

### Response

**Status Code:** 200 OK

**Response Body:**
```json
{
  "totalCertifications": 450,
  "completedCertifications": 320,
  "inProgressCertifications": 85,
  "expiredCertifications": 45,
  "completionRate": 71.1,
  "avgCompletionTime": 45.5,
  "expiringWithin30Days": 12,
  "expiringWithin90Days": 28,
  "byStatus": {
    "completed": {
      "count": 320,
      "percentage": 71.1
    },
    "inProgress": {
      "count": 85,
      "percentage": 18.9
    },
    "expired": {
      "count": 45,
      "percentage": 10.0
    }
  },
  "byCategory": [
    {
      "categoryName": {
        "en": "IT Certifications",
        "ar": "شهادات تقنية المعلومات"
      },
      "completed": 145,
      "inProgress": 32,
      "completionRate": 81.9
    },
    {
      "categoryName": {
        "en": "Professional Certifications",
        "ar": "الشهادات المهنية"
      },
      "completed": 98,
      "inProgress": 28,
      "completionRate": 77.8
    },
    {
      "categoryName": {
        "en": "Management Certifications",
        "ar": "شهادات الإدارة"
      },
      "completed": 77,
      "inProgress": 25,
      "completionRate": 75.5
    }
  ],
  "topCertifications": [
    {
      "certificationName": {
        "en": "PMP - Project Management Professional",
        "ar": "محترف إدارة المشاريع"
      },
      "completedCount": 45,
      "inProgressCount": 12
    },
    {
      "certificationName": {
        "en": "AWS Certified Solutions Architect",
        "ar": "مهندس حلول أمازون ويب سيرفس المعتمد"
      },
      "completedCount": 38,
      "inProgressCount": 8
    },
    {
      "certificationName": {
        "en": "CISSP - Certified Information Systems Security Professional",
        "ar": "محترف أمن نظم المعلومات المعتمد"
      },
      "completedCount": 28,
      "inProgressCount": 6
    }
  ],
  "monthlyTrend": [
    {
      "month": "2025-05",
      "completed": 12,
      "started": 18
    },
    {
      "month": "2025-06",
      "completed": 15,
      "started": 22
    },
    {
      "month": "2025-07",
      "completed": 18,
      "started": 20
    },
    {
      "month": "2025-08",
      "completed": 22,
      "started": 25
    },
    {
      "month": "2025-09",
      "completed": 20,
      "started": 19
    },
    {
      "month": "2025-10",
      "completed": 25,
      "started": 28
    }
  ],
  "complianceStatus": {
    "mandatoryCertifications": 150,
    "mandatoryCompleted": 142,
    "complianceRate": 94.7
  }
}
```

