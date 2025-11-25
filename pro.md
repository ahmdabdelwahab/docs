# Process Dashboard Drill-Down Endpoints

## 1. Process Overview Details

**Endpoint:** `GET /analytics/process-dashboard/overview/details`

**Parameters:**
- `processType` (optional): "AS_IS" or "TO_BE"
- `directorateIds` (optional): Comma-separated IDs
- `departmentIds` (optional): Comma-separated IDs
- `sectionIds` (optional): Comma-separated IDs
- `page` (default: 0)
- `size` (default: 20)
- `sortBy` (default: "id")
- `sortDir` (default: "ASC")

**Response Example:**
```json
{
  "content": [
    {
      "id": 123,
      "name": {"en": "Process Name", "ar": "اسم العملية"},
      "type": "AS_IS",
      "organization": "Organization Name"
    }
  ],
  "totalElements": 50,
  "totalPages": 3,
  "currentPage": 0,
  "pageSize": 20
}
```

---

## 2. Total Activities Details

**Endpoint:** `GET /analytics/process-dashboard/total-activities/details`

**Parameters:**
- `activityType` (optional)
- `isElectronic` (optional): true/false
- `directorateIds` (optional): Comma-separated IDs
- `departmentIds` (optional): Comma-separated IDs
- `sectionIds` (optional): Comma-separated IDs
- `page` (default: 0)
- `size` (default: 20)
- `sortBy` (default: "id")
- `sortDir` (default: "ASC")

**Response Example:**
```json
{
  "content": [
    {
      "id": 456,
      "name": {"en": "Activity Name", "ar": "اسم النشاط"},
      "type": "Type Name",
      "isElectronic": true,
      "processName": {"en": "Process Name", "ar": "اسم العملية"}
    }
  ],
  "totalElements": 120,
  "totalPages": 6,
  "currentPage": 0,
  "pageSize": 20
}
```

---

## 3. Total Roles Details

**Endpoint:** `GET /analytics/process-dashboard/total-roles/details`

**Parameters:**
- `roleType` (optional)
- `isInternal` (optional): true/false
- `directorateIds` (optional): Comma-separated IDs
- `departmentIds` (optional): Comma-separated IDs
- `sectionIds` (optional): Comma-separated IDs
- `page` (default: 0)
- `size` (default: 20)
- `sortBy` (default: "id")
- `sortDir` (default: "ASC")

**Response Example:**
```json
{
  "content": [
    {
      "id": 789,
      "name": {"en": "Role Name", "ar": "اسم الدور"},
      "type": "Type Name",
      "isInternal": true,
      "activityCount": 15
    }
  ],
  "totalElements": 80,
  "totalPages": 4,
  "currentPage": 0,
  "pageSize": 20
}
```

---

## 4. Process-Roles Overview Details

**Endpoint:** `GET /analytics/process-dashboard/process-roles-overview/details`

**Parameters:**
- `roleCountType` (optional)
- `rangeFilter` (optional): "0-5", "6-10", etc.
- `directorateIds` (optional): Comma-separated IDs
- `departmentIds` (optional): Comma-separated IDs
- `sectionIds` (optional): Comma-separated IDs
- `page` (default: 0)
- `size` (default: 20)
- `sortBy` (default: "id")
- `sortDir` (default: "ASC")

**Response Example:**
```json
{
  "content": [
    {
      "processId": 123,
      "processName": {"en": "Process Name", "ar": "اسم العملية"},
      "roleCount": 8,
      "organization": "Organization Name"
    }
  ],
  "totalElements": 45,
  "totalPages": 3,
  "currentPage": 0,
  "pageSize": 20
}
```

---

## 5. Process-Activities Overview Details

**Endpoint:** `GET /analytics/process-dashboard/process-activities-overview/details`

**Parameters:**
- `activityCountType` (optional)
- `rangeFilter` (optional): "0-10", "11-20", etc.
- `directorateIds` (optional): Comma-separated IDs
- `departmentIds` (optional): Comma-separated IDs
- `sectionIds` (optional): Comma-separated IDs
- `page` (default: 0)
- `size` (default: 20)
- `sortBy` (default: "id")
- `sortDir` (default: "ASC")

**Response Example:**
```json
{
  "content": [
    {
      "processId": 123,
      "processName": {"en": "Process Name", "ar": "اسم العملية"},
      "activityCount": 25,
      "organization": "Organization Name"
    }
  ],
  "totalElements": 60,
  "totalPages": 3,
  "currentPage": 0,
  "pageSize": 20
}
```

---

## 6. AS_IS vs TO_BE Benchmark Details

**Endpoint:** `GET /analytics/process-dashboard/as-is-vs-to-be/details`

**Parameters:**
- `processIds` (optional): List of process IDs
- `directorateIds` (optional): List of directorate IDs
- `departmentIds` (optional): List of department IDs
- `sectionIds` (optional): List of section IDs

**Response Example:**
```json
{
  "processes": [
    {
      "processId": 123,
      "processName": {"en": "Process Name", "ar": "اسم العملية"},
      "processPurpose": "AS_IS",
      "roleCount": 5,
      "activityCount": 15,
      "ownerOrganization": "Organization Name"
    }
  ],
  "roles": [
    {
      "roleId": 456,
      "roleName": {"en": "Role Name", "ar": "اسم الدور"},
      "processPurpose": "TO_BE",
      "activityCount": 8,
      "ownerOrganization": "Organization Name"
    }
  ],
  "activities": [
    {
      "activityId": 789,
      "activityName": {"en": "Activity Name", "ar": "اسم النشاط"},
      "processPurpose": "AS_IS",
      "ownerOrganization": "Organization Name"
    }
  ]
}
```

---

## 7. Activity Distribution Details

**Endpoint:** `GET /analytics/process-dashboard/activity-distribution/details`

**Parameters:**
- `activityRange` (required): "0", "1-5", "5-15", "15-30", "30-60", "60+"
- `processPurpose` (optional): 1 (AS_IS) or 2 (TO_BE)
- `processIds` (optional): List of process IDs
- `directorateIds` (optional): List of directorate IDs
- `departmentIds` (optional): List of department IDs
- `sectionIds` (optional): List of section IDs

**Response Example:**
```json
{
  "activityRange": "5-15",
  "directProcesses": [
    {
      "processId": 123,
      "processName": {"en": "Process Name", "ar": "اسم العملية"},
      "processPurpose": "AS_IS",
      "activityCount": 12,
      "ownerOrganization": "Organization Name"
    }
  ],
  "endToEndProcesses": [
    {
      "processId": 456,
      "processName": {"en": "Another Process", "ar": "عملية أخرى"},
      "processPurpose": "TO_BE",
      "activityCount": 18,
      "ownerOrganization": "Organization Name"
    }
  ]
}
```

---

## 8. Role Distribution Details

**Endpoint:** `GET /analytics/process-dashboard/role-distribution/details`

**Parameters:**
- `roleRange` (required): "0", "1", "2", "3", "4", "5", "6", "7", "8", "9", "10+"
- `processPurpose` (optional): 1 (AS_IS) or 2 (TO_BE)
- `processIds` (optional): List of process IDs
- `directorateIds` (optional): List of directorate IDs
- `departmentIds` (optional): List of department IDs
- `sectionIds` (optional): List of section IDs

**Response Example:**
```json
{
  "roleRange": "3",
  "directProcesses": [
    {
      "processId": 123,
      "processName": {"en": "Process Name", "ar": "اسم العملية"},
      "processPurpose": "AS_IS",
      "roleCount": 3,
      "ownerOrganization": "Organization Name"
    }
  ],
  "endToEndProcesses": [
    {
      "processId": 456,
      "processName": {"en": "Another Process", "ar": "عملية أخرى"},
      "processPurpose": "TO_BE",
      "roleCount": 8,
      "ownerOrganization": "Organization Name"
    }
  ]
}
```

---

## 9. Activity Duration Details

**Endpoint:** `GET /analytics/process-dashboard/activity-duration/details`

**Parameters:**
- `timeRange` (required): "0", "1-4", "5-8", "9-24", "24-36", "36+"
- `processPurpose` (optional): 1 (AS_IS) or 2 (TO_BE)
- `processIds` (optional): List of process IDs
- `directorateIds` (optional): List of directorate IDs
- `departmentIds` (optional): List of department IDs
- `sectionIds` (optional): List of section IDs

**Response Example:**
```json
{
  "timeRange": "5-8",
  "directFullTimeActivities": [
    {
      "activityId": 789,
      "activityName": {"en": "Activity Name", "ar": "اسم النشاط"},
      "processId": 123,
      "processName": {"en": "Process Name", "ar": "اسم العملية"},
      "processPurpose": "AS_IS",
      "fullTimeHours": 6.5,
      "netTimeHours": 4.2,
      "ownerOrganization": "Organization Name"
    }
  ],
  "endToEndFullTimeActivities": [
    {
      "activityId": 790,
      "activityName": {"en": "Another Activity", "ar": "نشاط آخر"},
      "processId": 456,
      "processName": {"en": "Process Name", "ar": "اسم العملية"},
      "processPurpose": "TO_BE",
      "fullTimeHours": 7.0,
      "netTimeHours": 5.5,
      "ownerOrganization": "Organization Name"
    }
  ],
  "directNetTimeActivities": [...],
  "endToEndNetTimeActivities": [...]
}
```

---

## 10. Job Level Details

**Endpoint:** `GET /analytics/process-dashboard/roles-by-job-level/details`

**Parameters:**
- `jobLevelId` (required): Job level enum ID
- `processPurpose` (optional): 1 (AS_IS) or 2 (TO_BE)
- `processIds` (optional): List of process IDs
- `directorateIds` (optional): List of directorate IDs
- `departmentIds` (optional): List of department IDs
- `sectionIds` (optional): List of section IDs

**Response Example:**
```json
{
  "jobLevelId": 456,
  "jobLevelName": {"en": "Manager", "ar": "مدير"},
  "roles": {
    "directRoles": [
      {
        "roleId": 789,
        "roleName": {"en": "Role Name", "ar": "اسم الدور"},
        "processPurpose": "AS_IS",
        "activityCount": 8,
        "ownerOrganization": "Organization Name"
      }
    ],
    "endToEndRoles": [
      {
        "roleId": 790,
        "roleName": {"en": "Another Role", "ar": "دور آخر"},
        "processPurpose": "TO_BE",
        "activityCount": 12,
        "ownerOrganization": "Organization Name"
      }
    ]
  },
  "activities": {
    "directActivities": [
      {
        "activityId": 321,
        "activityName": {"en": "Activity Name", "ar": "اسم النشاط"},
        "roleId": 789,
        "roleName": {"en": "Role Name", "ar": "اسم الدور"},
        "processId": 123,
        "processName": {"en": "Process Name", "ar": "اسم العملية"},
        "processPurpose": "AS_IS",
        "ownerOrganization": "Organization Name"
      }
    ],
    "endToEndActivities": [
      {
        "activityId": 322,
        "activityName": {"en": "Another Activity", "ar": "نشاط آخر"},
        "roleId": 790,
        "roleName": {"en": "Another Role", "ar": "دور آخر"},
        "processId": 456,
        "processName": {"en": "Process Name", "ar": "اسم العملية"},
        "processPurpose": "TO_BE",
        "ownerOrganization": "Organization Name"
      }
    ]
  }
}
```

---

## 11. Application Utilization Details

**Endpoint:** `GET /analytics/process-dashboard/utilization/details`

**Parameters:**
- `applicationId` (required): Application ID
- `processPurpose` (optional): 1 (AS_IS) or 2 (TO_BE)
- `processIds` (optional): List of process IDs
- `directorateIds` (optional): List of directorate IDs
- `departmentIds` (optional): List of department IDs
- `sectionIds` (optional): List of section IDs

**Response Example:**
```json
{
  "applicationId": 123,
  "applicationName": {"en": "SAP System", "ar": "نظام ساب"},
  "directProcesses": [
    {
      "processId": 456,
      "processName": {"en": "Process Name", "ar": "اسم العملية"},
      "processPurpose": "AS_IS",
      "ownerOrganization": "Organization Name"
    }
  ],
  "endToEndProcesses": [
    {
      "processId": 789,
      "processName": {"en": "Another Process", "ar": "عملية أخرى"},
      "processPurpose": "TO_BE",
      "ownerOrganization": "Organization Name"
    }
  ]
}
```

---

## 12. Challenge Category Details

**Endpoint:** `GET /analytics/process-dashboard/challenges-by-category/details`

**Parameters:**
- `challengeCategoryId` (required): Challenge category ID
- `processPurpose` (optional): 1 (AS_IS) or 2 (TO_BE)
- `processIds` (optional): List of process IDs
- `directorateIds` (optional): List of directorate IDs
- `departmentIds` (optional): List of department IDs
- `sectionIds` (optional): List of section IDs

**Response Example:**
```json
{
  "challengeCategoryId": 5,
  "challengeCategoryName": {"en": "Technical Challenges", "ar": "التحديات التقنية"},
  "directChallenges": [
    {
      "challengeId": 101,
      "challengeName": {"en": "System Integration", "ar": "تكامل النظام"},
      "processId": 456,
      "processName": {"en": "Process Name", "ar": "اسم العملية"},
      "processPurpose": "AS_IS",
      "ownerOrganization": "IT Department"
    }
  ],
  "endToEndChallenges": [
    {
      "challengeId": 102,
      "challengeName": {"en": "Data Migration", "ar": "ترحيل البيانات"},
      "processId": 789,
      "processName": {"en": "Another Process", "ar": "عملية أخرى"},
      "processPurpose": "TO_BE",
      "ownerOrganization": "Operations"
    }
  ]
}
```

---

## 13. Direct vs End-to-End Comparison Details

**Endpoint:** `GET /analytics/process-dashboard/direct-vs-endtoend-comparison/details`

**Purpose:** Drill into a specific process bar in the Direct vs End-to-End comparison chart to see the individual activities with their role information.

**Parameters:**
- `processId` (required): The specific process ID
- `processPurpose` (required): 1 for AS_IS, 2 for TO_BE
- `directorateIds` (optional): Comma-separated directorate IDs
- `departmentIds` (optional): Comma-separated department IDs
- `sectionIds` (optional): Comma-separated section IDs

**Response Example:**
```json
{
  "processId": 123,
  "processName": {
    "en": "Employee Onboarding",
    "ar": "إلحاق الموظف",
    "de": "Mitarbeiter-Onboarding",
    "fr": "Intégration des employés",
    "sw": "Uingizaji wa Wafanyakazi"
  },
  "processPurpose": "AS_IS",
  "directItems": [
    {
      "itemId": 456,
      "itemName": {
        "en": "Review Application",
        "ar": "مراجعة الطلب"
      },
      "sourceProcessId": 123,
      "sourceProcessName": {
        "en": "Employee Onboarding",
        "ar": "إلحاق الموظف"
      },
      "roleId": 789,
      "roleName": {
        "en": "HR Manager",
        "ar": "مدير الموارد البشرية"
      },
      "assignedOrgUnit": null
    }
  ],
  "endToEndItems": [
    {
      "itemId": 457,
      "itemName": {
        "en": "Background Check",
        "ar": "فحص الخلفية"
      },
      "sourceProcessId": 124,
      "sourceProcessName": {
        "en": "Security Clearance Process",
        "ar": "عملية التصريح الأمني"
      },
      "roleId": 790,
      "roleName": {
        "en": "Security Officer",
        "ar": "ضابط الأمن"
      },
      "assignedOrgUnit": null
    }
  ]
}
```

**Notes:**
- Always returns activities from `process_activity` table
- `directItems`: Activities directly attached to the main process
- `endToEndItems`: Activities from subprocesses (PART_OF_PROCESS) and complementary processes
- `itemId`: Activity ID
- `itemName`: Activity name translations
- `roleId` and `roleName`: Role assigned to the activity
- `assignedOrgUnit`: Always null for activities
- `sourceProcessId` and `sourceProcessName`: Indicate which process the activity comes from (useful for end-to-end items)

---

## 14. Execution Time Comparison Details

**Endpoint:** `GET /analytics/process-dashboard/execution-time-comparison/details`

**Purpose:** Drill into a specific process bar in the Execution Time comparison chart to see the individual activities and their processing times.

**Parameters:**
- `processId` (required): The specific process ID
- `processPurpose` (required): 1 for AS_IS, 2 for TO_BE
- `directorateIds` (optional): Comma-separated directorate IDs
- `departmentIds` (optional): Comma-separated department IDs
- `sectionIds` (optional): Comma-separated section IDs

**Response Example:**
```json
{
  "processId": 123,
  "processName": {
    "en": "Employee Onboarding",
    "ar": "إلحاق الموظف",
    "de": "Mitarbeiter-Onboarding",
    "fr": "Intégration des employés",
    "sw": "Uingizaji wa Wafanyakazi"
  },
  "processPurpose": "AS_IS",
  "directActivities": [
    {
      "activityId": 456,
      "activityName": {
        "en": "Review Application",
        "ar": "مراجعة الطلب"
      },
      "sourceProcessId": 123,
      "sourceProcessName": {
        "en": "Employee Onboarding",
        "ar": "إلحاق الموظف"
      },
      "processingTime": 2.0,
      "processingTimeUnit": "DAYS",
      "netProcessingTime": 0.5,
      "netProcessingTimeUnit": "DAYS",
      "probability": 100.0,
      "roleId": 789,
      "roleName": {
        "en": "HR Manager",
        "ar": "مدير الموارد البشرية"
      }
    }
  ],
  "endToEndActivities": [
    {
      "activityId": 457,
      "activityName": {
        "en": "Background Check",
        "ar": "فحص الخلفية"
      },
      "sourceProcessId": 124,
      "sourceProcessName": {
        "en": "Security Clearance Process",
        "ar": "عملية التصريح الأمني"
      },
      "processingTime": 5.0,
      "processingTimeUnit": "DAYS",
      "netProcessingTime": 1.0,
      "netProcessingTimeUnit": "DAYS",
      "probability": 80.0,
      "roleId": 790,
      "roleName": {
        "en": "Security Officer",
        "ar": "ضابط الأمن"
      }
    }
  ]
}
```

**Notes:**
- `directActivities`: Activities directly attached to the main process
- `endToEndActivities`: Activities from subprocesses (PART_OF_PROCESS) and complementary processes
- `processingTime`: Total execution time for the activity
- `netProcessingTime`: Net/direct processing time (excluding waiting time)
- `processingTimeUnit`: Time unit - "MINUTES", "HOURS", "DAYS", or "MONTHS"
- `probability`: Calculated probability (0-100) for the activity occurring
- Times shown are raw values; convert to days for aggregation using:
  - MINUTES: divide by 1440
  - HOURS: divide by 24
  - DAYS: use as-is
  - MONTHS: multiply by 30

---

## 15. Impact by Job Title Details

**Endpoint:** `GET /analytics/process-dashboard/impact-by-job-title/details`

**Purpose:** Drill into a specific job title bar in the Impact by Job Title chart to see the individual activities and roles assigned to that job title.

**Parameters:**
- `jobTitleId` (required): The org_chart_tree ID for the job title (node_type_id = 103)
- `processPurpose` (required): 1 for AS_IS, 2 for TO_BE
- `directorateIds` (optional): Comma-separated directorate IDs
- `departmentIds` (optional): Comma-separated department IDs
- `sectionIds` (optional): Comma-separated section IDs
- `processIds` (optional): Comma-separated process IDs

**Response Example:**
```json
{
  "jobTitleId": 456,
  "jobTitleNameTranslations": {
    "en": "Senior Manager",
    "ar": "مدير أول"
  },
  "processPurpose": 1,
  "processPurposeText": "AS_IS",
  "activities": [
    {
      "activityId": 789,
      "activityName": {
        "en": "Review Application",
        "ar": "مراجعة الطلب"
      },
      "processId": 123,
      "processName": {
        "en": "Employee Onboarding",
        "ar": "إلحاق الموظف"
      },
      "roleId": 321,
      "roleName": {
        "en": "HR Manager",
        "ar": "مدير الموارد البشرية"
      },
      "assignedOrgUnit": "Human Resources"
    }
  ],
  "roles": [
    {
      "roleId": 321,
      "roleName": {
        "en": "HR Manager",
        "ar": "مدير الموارد البشرية"
      },
      "processId": 123,
      "processName": {
        "en": "Employee Onboarding",
        "ar": "إلحاق الموظف"
      },
      "activityCount": 5,
      "assignedOrgUnit": "Human Resources"
    }
  ]
}
```

**Notes:**
- `jobTitleId`: ID from `org_chart_tree` where `node_type_id = 103` (job title nodes)
- `activities`: All activities assigned to roles that are linked to this job title
- `roles`: All roles linked to this job title, with their activity counts
- `assignedOrgUnit`: Owner organization of the process
- Only returns data from root processes (excludes subprocesses)
- Filtered by the specified `processPurpose` (AS_IS or TO_BE)

---

## 16. Job Title Time Details

**Endpoint:** `GET /analytics/process-dashboard/job-title-time/details`

**Purpose:** Drill into a specific job title bar in the Job Title Time Utilization chart to see the time breakdown by individual activities.

**Parameters:**
- `jobTitleId` (required): The org_chart_tree ID for the job title (node_type_id = 103)
- `processPurpose` (required): 1 for AS_IS, 2 for TO_BE
- `directorateIds` (optional): Comma-separated directorate IDs
- `departmentIds` (optional): Comma-separated department IDs
- `sectionIds` (optional): Comma-separated section IDs
- `processIds` (optional): Comma-separated process IDs
- `includeTransactions` (optional, default: false): Whether to multiply time by transaction volume

**Response Example:**
```json
{
  "jobTitleId": 456,
  "jobTitleNameTranslations": {
    "en": "Senior Manager",
    "ar": "مدير أول"
  },
  "processPurpose": 1,
  "processPurposeText": "AS_IS",
  "includeTransactions": false,
  "totalDays": 125.50,
  "activities": [
    {
      "activityId": 789,
      "activityName": {
        "en": "Review Application",
        "ar": "مراجعة الطلب"
      },
      "processId": 123,
      "processName": {
        "en": "Employee Onboarding",
        "ar": "إلحاق الموظف"
      },
      "roleId": 321,
      "roleName": {
        "en": "HR Manager",
        "ar": "مدير الموارد البشرية"
      },
      "netProcessingTime": 2.0,
      "netProcessingTimeUnit": 3,
      "netProcessingTimeUnitText": "DAYS",
      "probability": 85.5,
      "transactionVolume": 100,
      "calculatedMinutes": 14688.0,
      "calculatedDays": 30.60
    }
  ]
}
```

**Notes:**
- `totalDays`: Sum of all calculated days for activities assigned to this job title
- `netProcessingTime`: Net processing time value from the activity
- `netProcessingTimeUnit`: Enum value - 1=MINUTES, 2=HOURS, 3=DAYS, 4=MONTHS
- `netProcessingTimeUnitText`: Human-readable unit text
- `probability`: Calculated probability (0-100)
- `transactionVolume`: Number of transactions (if `includeTransactions` is true, otherwise defaults to 1)
- `calculatedMinutes`: Result of formula: `netProcessingTime * unit_conversion * (probability/100) * transactionVolume`
- `calculatedDays`: `calculatedMinutes / 480` (8-hour working days)
- Unit conversions to minutes: MINUTES=1, HOURS=60, DAYS=1440, MONTHS=43200
- Only returns data from root processes (excludes subprocesses)

---

## 17. Activity Type Distribution Details

**Endpoint:** `GET /analytics/process-dashboard/activity-type-distribution/details`

**Purpose:** Drill into a specific activity type in the Activity Type Distribution chart to see all activities of that type.

**Parameters:**
- `activityTypeId` (required): The activity type enum ID
- `processType` (optional): "AS_IS" or "TO_BE"
- `directorateIds` (optional): Comma-separated directorate IDs
- `departmentIds` (optional): Comma-separated department IDs
- `sectionIds` (optional): Comma-separated section IDs
- `page` (default: 0)
- `size` (default: 20)
- `sortBy` (default: "id")
- `sortDir` (default: "ASC")

**Response Example:**
```json
{
  "content": [
    {
      "activityId": 123,
      "activityName": {
        "en": "Review Document",
        "ar": "مراجعة الوثيقة"
      },
      "processId": 456,
      "processName": {
        "en": "Document Management",
        "ar": "إدارة الوثائق"
      },
      "processPurpose": "AS_IS",
      "activityTypeName": {
        "en": "Review",
        "ar": "مراجعة"
      },
      "ownerOrganization": "Quality Department"
    }
  ],
  "totalElements": 45,
  "totalPages": 3,
  "currentPage": 0,
  "pageSize": 20
}
```

**Notes:**
- Returns paginated list of activities matching the specified activity type
- Can be filtered by process type (AS_IS/TO_BE)
- Supports organizational unit filters

---

## 18. Execution Mechanism Distribution AS_IS Details

**Endpoint:** `GET /analytics/process-dashboard/execution-mechanism-distribution-as-is/details`

**Purpose:** Drill into a specific execution mechanism in the AS_IS Execution Mechanism Distribution chart to see all activities using that mechanism.

**Parameters:**
- `executionMechanism` (required): "MANUAL", "SEMI_AUTOMATED", or "FULLY_AUTOMATED"
- `directorateIds` (optional): Comma-separated directorate IDs
- `departmentIds` (optional): Comma-separated department IDs
- `sectionIds` (optional): Comma-separated section IDs
- `page` (default: 0)
- `size` (default: 20)
- `sortBy` (default: "id")
- `sortDir` (default: "ASC")

**Response Example:**
```json
{
  "content": [
    {
      "activityId": 123,
      "activityName": {
        "en": "Manual Data Entry",
        "ar": "إدخال البيانات يدويًا"
      },
      "processId": 456,
      "processName": {
        "en": "Data Processing",
        "ar": "معالجة البيانات"
      },
      "executionMechanism": "MANUAL",
      "ownerOrganization": "Data Entry Department"
    }
  ],
  "totalElements": 32,
  "totalPages": 2,
  "currentPage": 0,
  "pageSize": 20
}
```

**Notes:**
- Shows AS_IS activities only (process_purpose = 1)
- `executionMechanism`: Execution method for the activity
- Returns paginated list of activities

---

## 19. Execution Mechanism Distribution TO_BE Details

**Endpoint:** `GET /analytics/process-dashboard/execution-mechanism-distribution-to-be/details`

**Purpose:** Drill into a specific execution mechanism in the TO_BE Execution Mechanism Distribution chart to see all activities using that mechanism.

**Parameters:**
- `executionMechanism` (required): "MANUAL", "SEMI_AUTOMATED", or "FULLY_AUTOMATED"
- `directorateIds` (optional): Comma-separated directorate IDs
- `departmentIds` (optional): Comma-separated department IDs
- `sectionIds` (optional): Comma-separated section IDs
- `page` (default: 0)
- `size` (default: 20)
- `sortBy` (default: "id")
- `sortDir` (default: "ASC")

**Response Example:**
```json
{
  "content": [
    {
      "activityId": 789,
      "activityName": {
        "en": "Automated Data Import",
        "ar": "استيراد البيانات تلقائيًا"
      },
      "processId": 456,
      "processName": {
        "en": "Data Processing",
        "ar": "معالجة البيانات"
      },
      "executionMechanism": "FULLY_AUTOMATED",
      "ownerOrganization": "IT Department"
    }
  ],
  "totalElements": 18,
  "totalPages": 1,
  "currentPage": 0,
  "pageSize": 20
}
```

**Notes:**
- Shows TO_BE activities only (process_purpose = 2)
- `executionMechanism`: Target execution method for the activity
- Returns paginated list of activities
- Useful for tracking automation transformation from AS_IS to TO_BE
