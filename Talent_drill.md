# Talent Analytics Drilling API Documentation

## Overview
This document describes the drill-down endpoints for Talent Analytics cards and charts. Each visualization supports drilling down to view detailed information about individual talents based on the selected dimension.

## Base URL
```
/analytics/talent
```

---

## Card Drill-Down Endpoints

### 1. Talent Overview - Drill-Down

#### Endpoint
```
GET /analytics/talent/overview/details
```

#### Description
Retrieves a paginated list of all talents with basic information including name, job title, skills count, projects count, and certifications count.

#### Parameters
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `page` | Integer | No | 0 | Page number (0-indexed) |
| `size` | Integer | No | 20 | Number of items per page |
| `sortBy` | String | No | id | Field to sort by (e.g., id, skillsCount, projectsCount) |
| `sortDir` | String | No | ASC | Sort direction (ASC or DESC) |

#### Request Example
```http
GET /analytics/talent/overview/details?page=0&size=20&sortBy=skillsCount&sortDir=DESC
```

#### Response Structure
```json
{
  "data": [
    {
      "id": 123,
      "nameTranslations": {
        "en": "John Doe",
        "ar": "جون دو"
      },
      "jobTitleTranslations": {
        "en": "Senior Developer",
        "ar": "مطور أول"
      },
      "skillsCount": 15,
      "projectsCount": 12,
      "certificationsCount": 3
    }
  ],
  "paginationMetadata": {
    "currentPage": 0,
    "pageSize": 20,
    "totalPages": 8,
    "totalElements": 156,
    "hasNext": true,
    "hasPrevious": false
  }
}
```

---

### 2. Top Skills - Drill-Down

#### Endpoint
```
GET /analytics/talent/top-skills/details
```

#### Description
Retrieves detailed information about talents who possess a specific skill.

#### Parameters
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `skillId` | Long | Yes | - | The skill ID to filter by |
| `page` | Integer | No | 0 | Page number (0-indexed) |
| `size` | Integer | No | 20 | Number of items per page |
| `sortBy` | String | No | id | Field to sort by |
| `sortDir` | String | No | ASC | Sort direction (ASC or DESC) |

#### Request Example
```http
GET /analytics/talent/top-skills/details?skillId=42&page=0&size=20
```

#### Response Structure
```json
{
  "data": [
    {
      "id": 123,
      "nameTranslations": {
        "en": "John Doe",
        "ar": "جون دو"
      },
      "jobTitleTranslations": {
        "en": "Senior Developer",
        "ar": "مطور أول"
      },
      "skillNameTranslations": {
        "en": "Java",
        "ar": "جافا"
      }
    }
  ],
  "paginationMetadata": {
    "currentPage": 0,
    "pageSize": 20,
    "totalPages": 4,
    "totalElements": 67,
    "hasNext": true,
    "hasPrevious": false
  }
}
```

---

### 3. Skill Category Balance - Drill-Down

#### Endpoint
```
GET /analytics/talent/skill-category-balance/details
```

#### Description
Retrieves detailed information about talents who have skills in a specific skill category.

#### Parameters
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `categoryId` | Long | Yes | - | The skill category ID to filter by |
| `page` | Integer | No | 0 | Page number (0-indexed) |
| `size` | Integer | No | 20 | Number of items per page |
| `sortBy` | String | No | id | Field to sort by |
| `sortDir` | String | No | ASC | Sort direction (ASC or DESC) |

#### Request Example
```http
GET /analytics/talent/skill-category-balance/details?categoryId=5&page=0&size=20
```

#### Response Structure
```json
{
  "data": [
    {
      "id": 123,
      "nameTranslations": {
        "en": "John Doe",
        "ar": "جون دو"
      },
      "jobTitleTranslations": {
        "en": "Senior Developer",
        "ar": "مطور أول"
      },
      "categoryNameTranslations": {
        "en": "Backend Development",
        "ar": "تطوير الخلفية"
      }
    }
  ],
  "paginationMetadata": {
    "currentPage": 0,
    "pageSize": 20,
    "totalPages": 3,
    "totalElements": 52,
    "hasNext": true,
    "hasPrevious": false
  }
}
```

---

### 4. Certification Completion - Drill-Down

#### Endpoint
```
GET /analytics/talent/certification-completion/details
```

#### Description
Retrieves detailed information about talents with certifications. Can optionally filter by a specific certification ID.

#### Parameters
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `certificationId` | Long | No | - | Optional: Filter by specific certification ID. If omitted, returns all certified talents |
| `page` | Integer | No | 0 | Page number (0-indexed) |
| `size` | Integer | No | 20 | Number of items per page |
| `sortBy` | String | No | id | Field to sort by |
| `sortDir` | String | No | ASC | Sort direction (ASC or DESC) |

#### Request Examples

##### Get all certified talents
```http
GET /analytics/talent/certification-completion/details?page=0&size=20
```

##### Get talents with specific certification
```http
GET /analytics/talent/certification-completion/details?certificationId=101&page=0&size=20
```

#### Response Structure
```json
{
  "data": [
    {
      "id": 123,
      "nameTranslations": {
        "en": "John Doe",
        "ar": "جون دو"
      },
      "jobTitleTranslations": {
        "en": "Senior Developer",
        "ar": "مطور أول"
      },
      "certificationNameTranslations": {
        "en": "AWS Certified Solutions Architect",
        "ar": "معماري حلول AWS معتمد"
      }
    }
  ],
  "paginationMetadata": {
    "currentPage": 0,
    "pageSize": 20,
    "totalPages": 2,
    "totalElements": 34,
    "hasNext": true,
    "hasPrevious": false
  }
}
```

---

## Chart Drill-Down Endpoints

## 1. Talent by Seniority - Drill-Down

### Endpoint
```
GET /analytics/talent/by-seniority/details
```

### Description
Retrieves detailed information about talents filtered by a specific seniority level.

### Parameters
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `seniorityLevel` | Integer | Yes | - | The seniority level to filter by (e.g., 1, 2, 3) |
| `page` | Integer | No | 0 | Page number (0-indexed) |
| `size` | Integer | No | 20 | Number of items per page |
| `sortBy` | String | No | id | Field to sort by (e.g., id, yearsOfExperience) |
| `sortDir` | String | No | ASC | Sort direction (ASC or DESC) |

### Request Example
```http
GET /analytics/talent/by-seniority/details?seniorityLevel=2&page=0&size=20&sortBy=id&sortDir=ASC
```

### Response Structure
```json
{
  "data": [
    {
      "id": 123,
      "nameTranslations": {
        "en": "John Doe",
        "ar": "جون دو"
      },
      "jobTitleTranslations": {
        "en": "Senior Developer",
        "ar": "مطور أول"
      },
      "seniorityLevel": 2,
      "seniorityLevelNameTranslations": {
        "en": "Senior",
        "ar": "أول"
      },
      "yearsOfExperience": 8,
      "skillsCount": 15,
      "projectsCount": 12
    }
  ],
  "paginationMetadata": {
    "currentPage": 0,
    "pageSize": 20,
    "totalPages": 5,
    "totalElements": 87,
    "hasNext": true,
    "hasPrevious": false
  }
}
```

---

## 2. Talent by Nationality - Drill-Down

### Endpoint
```
GET /analytics/talent/by-nationality/details
```

### Description
Retrieves detailed information about talents filtered by nationality.

### Parameters
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `nationalityId` | Long | Yes | - | The nationality ID to filter by |
| `page` | Integer | No | 0 | Page number (0-indexed) |
| `size` | Integer | No | 20 | Number of items per page |
| `sortBy` | String | No | id | Field to sort by |
| `sortDir` | String | No | ASC | Sort direction (ASC or DESC) |

### Request Example
```http
GET /analytics/talent/by-nationality/details?nationalityId=101&page=0&size=20
```

### Response Structure
```json
{
  "data": [
    {
      "id": 456,
      "nameTranslations": {
        "en": "Jane Smith",
        "ar": "جين سميث"
      },
      "jobTitleTranslations": {
        "en": "Software Engineer",
        "ar": "مهندس برمجيات"
      },
      "nationalityTranslations": {
        "en": "American",
        "ar": "أمريكي"
      },
      "skillsCount": 12,
      "projectsCount": 8
    }
  ],
  "paginationMetadata": {
    "currentPage": 0,
    "pageSize": 20,
    "totalPages": 3,
    "totalElements": 45,
    "hasNext": true,
    "hasPrevious": false
  }
}
```

---

## 3. Talent by Experience - Drill-Down

### Endpoint
```
GET /analytics/talent/by-experience/details
```

### Description
Retrieves detailed information about talents filtered by years of experience.

### Parameters
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `yearsOfExperience` | Integer | Yes | - | The years of experience to filter by |
| `page` | Integer | No | 0 | Page number (0-indexed) |
| `size` | Integer | No | 20 | Number of items per page |
| `sortBy` | String | No | id | Field to sort by |
| `sortDir` | String | No | ASC | Sort direction (ASC or DESC) |

### Request Example
```http
GET /analytics/talent/by-experience/details?yearsOfExperience=5&page=0&size=20
```

### Response Structure
```json
{
  "data": [
    {
      "id": 789,
      "nameTranslations": {
        "en": "Ahmed Ali",
        "ar": "أحمد علي"
      },
      "jobTitleTranslations": {
        "en": "Backend Developer",
        "ar": "مطور خلفي"
      },
      "yearsOfExperience": 5,
      "skillsCount": 10,
      "projectsCount": 7
    }
  ],
  "paginationMetadata": {
    "currentPage": 0,
    "pageSize": 20,
    "totalPages": 2,
    "totalElements": 32,
    "hasNext": true,
    "hasPrevious": false
  }
}
```

---

## 4. Talent Involvement - Drill-Down

### Endpoint
```
GET /analytics/talent/involvement/details
```

### Description
Retrieves detailed involvement information for a specific talent, including their skills, projects, and certifications. Supports filtering by category to show only specific involvement types.

### Parameters
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `talentId` | Long | Yes | - | The talent ID to retrieve details for |
| `filterBy` | String | No | - | Filter by category: `skills`, `projects`, or `certifications`. If omitted, returns all categories |
| `page` | Integer | No | 0 | Page number (0-indexed) |
| `size` | Integer | No | 20 | Number of items per page |
| `sortBy` | String | No | id | Field to sort by |
| `sortDir` | String | No | ASC | Sort direction (ASC or DESC) |

### Request Examples

#### Get all involvement data (no filter)
```http
GET /analytics/talent/involvement/details?talentId=123
```

#### Get only skills
```http
GET /analytics/talent/involvement/details?talentId=123&filterBy=skills
```

#### Get only projects
```http
GET /analytics/talent/involvement/details?talentId=123&filterBy=projects
```

#### Get only certifications
```http
GET /analytics/talent/involvement/details?talentId=123&filterBy=certifications
```

### Response Structure (No Filter - All Data)
```json
{
  "data": [
    {
      "talentId": 123,
      "talentNameTranslations": {
        "en": "John Doe",
        "ar": "جون دو"
      },
      "jobTitleTranslations": {
        "en": "Senior Developer",
        "ar": "مطور أول"
      },
      "skills": [
        {
          "id": "1",
          "nameEn": "Java",
          "nameAr": "جافا"
        },
        {
          "id": "2",
          "nameEn": "Spring Boot",
          "nameAr": "سبرينج بوت"
        }
      ],
      "projects": [
        {
          "id": "101",
          "nameEn": "E-Commerce Platform",
          "nameAr": "منصة التجارة الإلكترونية"
        },
        {
          "id": "102",
          "nameEn": "Mobile Banking App",
          "nameAr": "تطبيق الخدمات المصرفية"
        }
      ],
      "certifications": [
        {
          "id": "501",
          "nameEn": "AWS Certified Solutions Architect",
          "nameAr": "معماري حلول AWS معتمد"
        }
      ],
      "yearsOfExperience": 8
    }
  ],
  "paginationMetadata": {
    "currentPage": 0,
    "pageSize": 20,
    "totalPages": 1,
    "totalElements": 1,
    "hasNext": false,
    "hasPrevious": false
  }
}
```

### Response Structure (Filtered by Skills)
```json
{
  "data": [
    {
      "talentId": 123,
      "talentNameTranslations": {
        "en": "John Doe",
        "ar": "جون دو"
      },
      "jobTitleTranslations": {
        "en": "Senior Developer",
        "ar": "مطور أول"
      },
      "skills": [
        {
          "id": "1",
          "nameEn": "Java",
          "nameAr": "جافا"
        },
        {
          "id": "2",
          "nameEn": "Spring Boot",
          "nameAr": "سبرينج بوت"
        },
        {
          "id": "3",
          "nameEn": "PostgreSQL",
          "nameAr": "بوستجريسكيو إل"
        }
      ],
      "projects": [],
      "certifications": [],
      "yearsOfExperience": 8
    }
  ],
  "paginationMetadata": {
    "currentPage": 0,
    "pageSize": 20,
    "totalPages": 1,
    "totalElements": 1,
    "hasNext": false,
    "hasPrevious": false
  }
}
```

---

## Common Response Fields

### Pagination Metadata
All drill-down endpoints return pagination metadata with the following structure:

```json
{
  "currentPage": 0,
  "pageSize": 20,
  "totalPages": 5,
  "totalElements": 87,
  "hasNext": true,
  "hasPrevious": false
}
```

| Field | Type | Description |
|-------|------|-------------|
| `currentPage` | Integer | Current page number (0-indexed) |
| `pageSize` | Integer | Number of items per page |
| `totalPages` | Integer | Total number of pages available |
| `totalElements` | Long | Total number of items across all pages |
| `hasNext` | Boolean | Whether there is a next page |
| `hasPrevious` | Boolean | Whether there is a previous page |

---

## Error Responses

### 400 Bad Request
```json
{
  "timestamp": "2025-11-24T10:30:00",
  "status": 400,
  "error": "Bad Request",
  "message": "Required parameter 'talentId' is missing",
  "path": "/analytics/talent/involvement/details"
}
```

### 404 Not Found
```json
{
  "timestamp": "2025-11-24T10:30:00",
  "status": 404,
  "error": "Not Found",
  "message": "No data found for the specified criteria",
  "path": "/analytics/talent/by-seniority/details"
}
```

---

## Usage Examples

### Frontend Integration - React/TypeScript

```typescript
// Service for talent drilling
const talentDrillingService = {
  // Get talents by seniority
  getBySeniorityDetails: async (
    seniorityLevel: number,
    page: number = 0,
    size: number = 20
  ) => {
    const response = await fetch(
      `/analytics/talent/by-seniority/details?seniorityLevel=${seniorityLevel}&page=${page}&size=${size}`
    );
    return response.json();
  },

  // Get talents by nationality
  getByNationalityDetails: async (
    nationalityId: number,
    page: number = 0,
    size: number = 20
  ) => {
    const response = await fetch(
      `/analytics/talent/by-nationality/details?nationalityId=${nationalityId}&page=${page}&size=${size}`
    );
    return response.json();
  },

  // Get talents by experience
  getByExperienceDetails: async (
    yearsOfExperience: number,
    page: number = 0,
    size: number = 20
  ) => {
    const response = await fetch(
      `/analytics/talent/by-experience/details?yearsOfExperience=${yearsOfExperience}&page=${page}&size=${size}`
    );
    return response.json();
  },

  // Get talent involvement details
  getInvolvementDetails: async (
    talentId: number,
    filterBy?: 'skills' | 'projects' | 'certifications',
    page: number = 0,
    size: number = 20
  ) => {
    const filterParam = filterBy ? `&filterBy=${filterBy}` : '';
    const response = await fetch(
      `/analytics/talent/involvement/details?talentId=${talentId}${filterParam}&page=${page}&size=${size}`
    );
    return response.json();
  }
};
```

### Complete Service Implementation

```typescript
// Complete service for talent drilling
const talentDrillingService = {
  // === Card Drill-Downs ===
  
  // Get talent overview details
  getOverviewDetails: async (
    page: number = 0,
    size: number = 20,
    sortBy: string = 'id',
    sortDir: string = 'ASC'
  ) => {
    const response = await fetch(
      `/analytics/talent/overview/details?page=${page}&size=${size}&sortBy=${sortBy}&sortDir=${sortDir}`
    );
    return response.json();
  },

  // Get talents by skill (top skills card)
  getBySkillDetails: async (
    skillId: number,
    page: number = 0,
    size: number = 20
  ) => {
    const response = await fetch(
      `/analytics/talent/top-skills/details?skillId=${skillId}&page=${page}&size=${size}`
    );
    return response.json();
  },

  // Get talents by skill category
  getBySkillCategoryDetails: async (
    categoryId: number,
    page: number = 0,
    size: number = 20
  ) => {
    const response = await fetch(
      `/analytics/talent/skill-category-balance/details?categoryId=${categoryId}&page=${page}&size=${size}`
    );
    return response.json();
  },

  // Get certified talents
  getCertifiedTalentsDetails: async (
    certificationId?: number,
    page: number = 0,
    size: number = 20
  ) => {
    const certParam = certificationId ? `&certificationId=${certificationId}` : '';
    const response = await fetch(
      `/analytics/talent/certification-completion/details?page=${page}&size=${size}${certParam}`
    );
    return response.json();
  },

  // === Chart Drill-Downs ===
  
  // Get talents by seniority
  getBySeniorityDetails: async (
    seniorityLevel: number,
    page: number = 0,
    size: number = 20
  ) => {
    const response = await fetch(
      `/analytics/talent/by-seniority/details?seniorityLevel=${seniorityLevel}&page=${page}&size=${size}`
    );
    return response.json();
  },

  // Get talents by nationality
  getByNationalityDetails: async (
    nationalityId: number,
    page: number = 0,
    size: number = 20
  ) => {
    const response = await fetch(
      `/analytics/talent/by-nationality/details?nationalityId=${nationalityId}&page=${page}&size=${size}`
    );
    return response.json();
  },

  // Get talents by experience
  getByExperienceDetails: async (
    yearsOfExperience: number,
    page: number = 0,
    size: number = 20
  ) => {
    const response = await fetch(
      `/analytics/talent/by-experience/details?yearsOfExperience=${yearsOfExperience}&page=${page}&size=${size}`
    );
    return response.json();
  },

  // Get talent involvement details
  getInvolvementDetails: async (
    talentId: number,
    filterBy?: 'skills' | 'projects' | 'certifications',
    page: number = 0,
    size: number = 20
  ) => {
    const filterParam = filterBy ? `&filterBy=${filterBy}` : '';
    const response = await fetch(
      `/analytics/talent/involvement/details?talentId=${talentId}${filterParam}&page=${page}&size=${size}`
    );
    return response.json();
  }
};
```

### Usage Examples

#### Card Click Handlers

```typescript
// Example: Handling overview card click
const handleOverviewCardClick = async () => {
  try {
    const result = await talentDrillingService.getOverviewDetails(0, 20, 'skillsCount', 'DESC');
    
    // Display results in modal/drawer
    setDrillDownData(result.data);
    setPaginationInfo(result.paginationMetadata);
    setModalOpen(true);
  } catch (error) {
    console.error('Failed to fetch overview details:', error);
  }
};

// Example: Handling top skill item click
const handleTopSkillClick = async (skillId: number, skillName: string) => {
  try {
    const result = await talentDrillingService.getBySkillDetails(skillId);
    
    // Show talents with this skill
    setModalTitle(`Talents with ${skillName}`);
    setDrillDownData(result.data);
    setPaginationInfo(result.paginationMetadata);
    setModalOpen(true);
  } catch (error) {
    console.error('Failed to fetch skill details:', error);
  }
};

// Example: Handling skill category click
const handleSkillCategoryClick = async (categoryId: number, categoryName: string) => {
  try {
    const result = await talentDrillingService.getBySkillCategoryDetails(categoryId);
    
    setModalTitle(`${categoryName} Talents`);
    setDrillDownData(result.data);
    setPaginationInfo(result.paginationMetadata);
    setModalOpen(true);
  } catch (error) {
    console.error('Failed to fetch category details:', error);
  }
};

// Example: Handling certification card click (all certified talents)
const handleCertificationCardClick = async () => {
  try {
    const result = await talentDrillingService.getCertifiedTalentsDetails();
    
    setModalTitle('All Certified Talents');
    setDrillDownData(result.data);
    setPaginationInfo(result.paginationMetadata);
    setModalOpen(true);
  } catch (error) {
    console.error('Failed to fetch certified talents:', error);
  }
};

// Example: Handling specific certification click
const handleSpecificCertificationClick = async (certId: number, certName: string) => {
  try {
    const result = await talentDrillingService.getCertifiedTalentsDetails(certId);
    
    setModalTitle(`Talents with ${certName}`);
    setDrillDownData(result.data);
    setPaginationInfo(result.paginationMetadata);
    setModalOpen(true);
  } catch (error) {
    console.error('Failed to fetch certification details:', error);
  }
};
```

#### Chart Click Handlers

```typescript
// Example: Handling chart bar click
const handleSeniorityBarClick = async (seniorityLevel: number) => {
  try {
    const result = await talentDrillingService.getBySeniorityDetails(
      seniorityLevel,
      0,
      20
    );
    
    // Display results in modal/drawer
    setDrillDownData(result.data);
    setPaginationInfo(result.paginationMetadata);
    setModalOpen(true);
  } catch (error) {
    console.error('Failed to fetch drill-down data:', error);
  }
};

// Example: Handling involvement category filter
const handleInvolvementFilter = async (
  talentId: number,
  category: 'skills' | 'projects' | 'certifications'
) => {
  try {
    const result = await talentDrillingService.getInvolvementDetails(
      talentId,
      category
    );
    
    // Display filtered results
    setInvolvementData(result.data[0]);
  } catch (error) {
    console.error('Failed to fetch involvement data:', error);
  }
};
```

---

## API Summary

### Card Drill-Downs
| Endpoint | Purpose | Required Params |
|----------|---------|----------------|
| `/overview/details` | All talents overview | None |
| `/top-skills/details` | Talents by specific skill | `skillId` |
| `/skill-category-balance/details` | Talents by skill category | `categoryId` |
| `/certification-completion/details` | Certified talents | None (optional: `certificationId`) |

### Chart Drill-Downs
| Endpoint | Purpose | Required Params |
|----------|---------|----------------|
| `/by-seniority/details` | Talents by seniority level | `seniorityLevel` |
| `/by-nationality/details` | Talents by nationality | `nationalityId` |
| `/by-experience/details` | Talents by years of experience | `yearsOfExperience` |
| `/involvement/details` | Talent involvement breakdown | `talentId` (optional: `filterBy`) |

---

## Notes

1. **Pagination**: All endpoints support pagination. Always check `paginationMetadata` to determine if more pages are available.

2. **Sorting**: The `sortBy` parameter accepts field names from the response DTO. Ensure the field exists before using it.

3. **Card vs Chart Drill-Downs**:
   - **Card drill-downs**: Show lists of talents based on card metrics (overview, skills, categories, certifications)
   - **Chart drill-downs**: Show lists of talents based on chart dimensions (seniority, nationality, experience) or detailed breakdown (involvement)

4. **Filtering Logic (Involvement)**:
   - **No `filterBy`**: Returns complete involvement data (skills, projects, certifications)
   - **With `filterBy`**: Returns only the specified category with other arrays empty

5. **Optional Parameters**:
   - `certificationId` in `/certification-completion/details`: When omitted, returns all certified talents
   - `filterBy` in `/involvement/details`: When omitted, returns all categories

6. **Performance**: Default page size is 20 items. Adjust based on UI requirements, but avoid excessively large page sizes.

7. **Translations**: All name fields include English (`en`) and Arabic (`ar`) translations.

8. **IDs**: All entity IDs (talent, nationality, skill, project, certification) are Long values.

---

## Related Documentation
- [Portfolio Analytics API](./PORTFOLIO_ANALYTICS_API.md)
- [Dashboard Analysis](./dashboard-analysis.md)
- [Portfolio Implementation](./README_PORTFOLIO_IMPLEMENTATION.md)
