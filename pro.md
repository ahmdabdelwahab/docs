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
