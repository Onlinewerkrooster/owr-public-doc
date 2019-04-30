# OWR Query API

The OWR Query API is intended to retrieve data from Onlinewerkrooster for reporting/synchronization purposes. The query API is build in 2 flavours:

**By entity**

Fetch information per entity, filter on properties.

**By report**

Fetch information per **predefined** report. These reports are predefined by onlinewerkrooster and groups separate entities into a logical report. By using these reports you do not have to bother about relationships between entities, applying the correct filters, ...

If needed, you can contact onlinewerkrooster support (support@onlinewerkrooster.be) and to predefine a report that matches your specific business requirements.

## Endpoint

https://owr-public-services-prod.herokuapp.com/api/query/

## GET /api/query/entities

#### List of queryable entities

| Name            | Description                       |
| --------------- | --------------------------------- |
| Company         | Company details                   |
| Workspace       | Workspace details                 |
| Workarea        | Workarea details                  |
| Timeclock       | Timeclock details                 |
| Planning        | Planning details (workday)        |
| Employee        | Employee details                  |
| EmployeeCompany | Employee details on company level |

#### Header

| Name         | Required | Value                            | Remarks                                                      |
| ------------ | -------- | -------------------------------- | ------------------------------------------------------------ |
| apikey       | Yes      | 3fdae2c8b32348a3855af9f0377191d4 | Unique ID to identify the requester (provided by onlinewerkrooster.be team) |
| content-type | Yes      | application/json                 | JSON data                                                    |

#### Body

```
{
	"entities": [
		{
			"name": "Planning",
			"properties": [
				"Id",
				"WorkareaId"
			]
		},
		{
			"name": "Employee",
			"properties": [
				"Id",
				"Email"
			],
			"filters": [
				{
					"property": "Id",
					"operator": ">",
					"value": 1
				}
			]
		}
	],
	"pagination": {
		"page": 0,
		"limit": 2000
	}
}
```

| Field name                    | Type                 | Required | Value | Remarks                                                      |
| ----------------------------- | -------------------- | -------- | ----- | ------------------------------------------------------------ |
| Entities                      | Array                | Yes      |       | One or many                                                  |
| Entities[].name               | String               | Yes      |       | Value of entity                                              |
| Entities[].properties         | Array (String)       | No       |       | List of properties to query. If not defined, all properties of entity are queried. |
| Entities[].filters            | Array                | No       |       | List of filters to apply. If not defined, no filters are used. |
| Entities[].filters[].property | String               | Yes      |       | Name of property you want to apply                           |
| Entities[].filters[].operator | String               | Yes      |       | Operator to use in query. Possible values are:<br /><, <=, =, !=, =>, > |
| Entities[].filters[].value    | String\|Date\|Number | Yes      |       | Value to use as filter                                       |
| Pagination                    |                      | No       |       | Specify pagination                                           |
| Pagination.page               | Number               | Yes      |       | Page x of y to retrieve data                                 |
| Pagination.limit              | Number               | Yes      |       | Amount of records per page                                   |

#### CURL

```
curl --request GET \
  --url https://owr-public-services-prod.herokuapp.com/api/query/entities \
  --header 'apikey: 3CCD0823-F532-4219-8A10-A660992070B7' \
  --header 'content-type: application/json' \
  --data '{
	"entities": [
		{
			"name": "Planning",
			"properties": [
				"Id",
				"WorkareaId"
			]
		},
		{
			"name": "Employee",
			"properties": [
				"Id",
				"Email"
			],
			"filters": [
				{
					"property": "Id",
					"operator": ">w",
					"value": 1
				}
			]
		}
	],
	"pagination": {
		"page": 0,
		"limit": 2000
	}
}'
```

### Example Response (Success)

```json
{
  "page": 0,
  "limit": 1000,
  "total": "630",
  "items": [
    {
      "PlanningId": 7784,
      "PlanningWorkareaId": 62,
      "EmployeeId": 204,
      "EmployeeEmail": "ageeth.dewaart@hotmail.com"
    },
    {
      "PlanningId": 7785,
      "PlanningWorkareaId": 62,
      "EmployeeId": 204,
      "EmployeeEmail": "ageeth.dewaart@hotmail.com"
    },
    {
      "PlanningId": 7786,
      "PlanningWorkareaId": 62,
      "EmployeeId": 204,
      "EmployeeEmail": "ageeth.dewaart@hotmail.com"
    },
    {
      "PlanningId": 7792,
      "PlanningWorkareaId": 58,
      "EmployeeId": 224,
      "EmployeeEmail": "stefania.corbeanu@gmail.com"
    }
	]
}
```

## GET /api/query/reports

#### List of predefined reports

| Name                | Description                                      |
| ------------------- | ------------------------------------------------ |
| CUMULIO_EMPLOYEES   | Employees (including company details)            |
| CUMULIO_PLANNING    | Planning (+ workspace + workarea)                |
| CUMULIO_TIMECLOCK   | Timeclock (+ workspace + workarea)               |
| CUMULIO_WORKRECORDS | Combination of planning + timeclock (OUTER join) |

#### Header

| Name         | Required | Value                            | Remarks                                                      |
| ------------ | -------- | -------------------------------- | ------------------------------------------------------------ |
| apikey       | Yes      | 3fdae2c8b32348a3855af9f0377191d4 | Unique ID to identify the requester (provided by onlinewerkrooster.be team) |
| content-type | Yes      | application/json                 | JSON data                                                    |

#### Body

```
{
	"name": "CUMULIO_PLANNING",
	"properties": [
		"PlanningId",
		"WorkspaceName"
	],
	"filters": [
		{
			"property": "BusinessDayId",
			"operator": "=",
			"value": 2441
		}
	]
}
```

| Field name         | Type                 | Required | Value | Remarks                                                      |
| ------------------ | -------------------- | -------- | ----- | ------------------------------------------------------------ |
| name               | String               | Yes      |       | Name of the report                                           |
| properties         | Array (String)       | No       |       | List of properties to query. If not defined, all properties of report are queried. |
| filters            | Array                | No       |       | List of filters to apply. If not defined, no filters are used. |
| filters[].property | String               | Yes      |       | Name of property you want to apply                           |
| filters[].operator | String               | Yes      |       | Operator to use in query. Possible values are:<br /><, <=, =, !=, =>, > |
| filters[].value    | String\|Date\|Number | Yes      |       | Value to use as filter                                       |
| Pagination         |                      | No       |       | Specify pagination                                           |
| Pagination.page    | Number               | Yes      |       | Page x of y to retrieve data                                 |
| Pagination.limit   | Number               | Yes      |       | Amount of records per page                                   |

#### CURL

```
curl --request GET \
  --url https://owr-public-services-prod.herokuapp.com/api/query/reports \
  --header 'apikey: 3CCD0823-F532-4219-8A10-A660992070B7' \
  --header 'content-type: application/json' \
  --data '{
	"name": "CUMULIO_PLANNING",
	"properties": [
		"PlanningId",
		"WorkspaceName"
	],
	"filters": [
		{
			"property": "BusinessDayId",
			"operator": "=",
			"value": 2441
		}
	]
}'
```

### Example Response (Success)

```json
{
  "page": 0,
  "limit": 1000,
  "total": "2",
  "items": [
    {
      "PlanningId": 7785,
      "BusinessDayId": 2441,
      "StartWorkingHoursId": 12,
      "EndWorkingHoursId": 44,
      "WorkareaId": 62,
      "WorkspaceName": "Atlantis Hotel Genk",
      "EmployeeCompanyId": 9,
      "EmployeeId": 204
    },
    {
      "PlanningId": 7793,
      "BusinessDayId": 2441,
      "StartWorkingHoursId": 24,
      "EndWorkingHoursId": 44,
      "WorkareaId": 58,
      "WorkspaceName": "Atlantis Hotel Genk",
      "EmployeeCompanyId": 29,
      "EmployeeId": 224
    }
    ]
}
```

