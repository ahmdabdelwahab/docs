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
