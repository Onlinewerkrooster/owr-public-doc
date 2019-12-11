# OWR Query API

The OWR Query API is intended to retrieve data from Onlinewerkrooster for reporting/synchronization purposes. The query API is build in 2 flavours:

**By entity**

Fetch information per entity, filter on properties.

**By report**

Fetch information per **predefined** report. These reports are predefined by onlinewerkrooster and groups separate entities into a logical report. By using these reports you do not have to bother about relationships between entities, applying the correct filters, ...

If needed, you can contact onlinewerkrooster support (support@onlinewerkrooster.be) and to predefine a report that matches your specific business requirements.

## Endpoint

https://owr-public-services-prod.herokuapp.com/api/query/

## GET /api/query/entities/meta

GET API to retrieve which entities are queryable and returns detailed information about the entity

#### Header

| Name            | Required | Value                            | Remarks                                                      |
| --------------- | -------- | -------------------------------- | ------------------------------------------------------------ |
| apikey          | Yes      | 3fdae2c8b32348a3855af9f0377191d4 | Unique ID to identify the requester (provided by onlinewerkrooster.be team) |
| Accept-language | No       | nl                               | Language to retrieve label (en,nl,fr)                        |

### Query parameters

| Name     | Required | Value    | Remarks                                 |
| -------- | -------- | -------- | --------------------------------------- |
| entities | No       | Employee | Array of entities to retrieve metadata. |

### CURL

```
curl --request GET \
  --url 'https://owr-public-services-prod.herokuapp.com/api/query/entities/meta?entities=employee&entities=planning' \
  --header 'apikey: 927073B6-3D9E-A2AA-98FA-83573D2CC57E'
```

### Response

```json
[
  {
    "name": "Employee",
    "label": "Medewerker",
    "properties": [
      {
        "key": "Id",
        "type": "number",
        "label": "Id",
        "translations": [
          {
            "lang": "en",
            "description": "Id"
          },
          {
            "lang": "nl",
            "description": "Id"
          },
          {
            "lang": "fr",
            "description": "Id"
          }
        ]
      },
      {
        "key": "Email",
        "type": "string",
        "label": "Email",
        "translations": [
          {
            "lang": "en",
            "description": "Email"
          },
          {
            "lang": "nl",
            "description": "Email"
          },
          {
            "lang": "fr",
            "description": "Email"
          }
        ]
      },
...
]
```



## GET /api/query/entities

#### List of queryable entities

A list of all queryable entities can be retrived with the 'meta' API

```
curl --request GET \
  --url 'https://owr-public-services-dev.herokuapp.com/api/query/entities/meta \
  --header 'apikey: 927073B6-3D9E-A2AA-98FA-83573D2CC57E'
```

#### Header

| Name            | Required | Value                            | Remarks                                                      |
| --------------- | -------- | -------------------------------- | ------------------------------------------------------------ |
| apikey          | Yes      | 3fdae2c8b32348a3855af9f0377191d4 | Unique ID to identify the requester (provided by onlinewerkrooster.be team) |
| content-type    | Yes      | application/json                 | JSON data                                                    |
| Accept-Language | No       | nl                               | Language used to get translatable values.                    |

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

## GET /api/query/reports/meta

GET API to retrieve which reports are queryable and returns detailed information about the entity

#### Header

| Name            | Required | Value                            | Remarks                                                      |
| --------------- | -------- | -------------------------------- | ------------------------------------------------------------ |
| apikey          | Yes      | 3fdae2c8b32348a3855af9f0377191d4 | Unique ID to identify the requester (provided by onlinewerkrooster.be team) |
| Accept-language | No       | nl                               | Language to retrieve label (en,nl,fr)                        |

### Query parameters

| Name    | Required | Value    | Remarks                                |
| ------- | -------- | -------- | -------------------------------------- |
| reports | No       | Employee | Array of reports to retrieve metadata. |

### CURL

```
curl --request GET \
  --url 'https://owr-public-services-prod.herokuapp.com/api/query/reports/meta?reports=CUMULIO_EMPLOYEES&entities=CUMULIO_PLANNING' \
  --header 'apikey: 927073B6-3D9E-A2AA-98FA-83573D2CC57E'
```

### Response

```json
[
  {
    "name": "CUMULIO_PLANNING",
    "label": "Cumul.io Planification",
    "properties": [
      [
        {
          "key": "EmployeeId",
          "type": "number",
          "label": "Id",
          "translations": [
            {
              "lang": "en",
              "description": "Id"
            },
            {
              "lang": "nl",
              "description": "Id"
            },
            {
              "lang": "fr",
              "description": "Id"
            }
          ]
        }
      ],
      [
        {
          "key": "EmployeeCompanyId",
          "type": "number",
          "label": "Id",
          "translations": [
            {
              "lang": "en",
              "description": "Id"
            },
            {
              "lang": "nl",
              "description": "Id"
            },
            {
              "lang": "fr",
              "description": "Id"
            }
          ]
 ...
 ]
```

## GET /api/query/reports

#### List of predefined reports

A list of all queryable reports can be retrived with the 'meta' API

```
curl --request GET \
  --url 'https://owr-public-services-dev.herokuapp.com/api/query/reports/meta \
  --header 'apikey: 927073B6-3D9E-A2AA-98FA-83573D2CC57E'
```

#### Header

| Name           | Required | Value                            | Remarks                                                      |
| -------------- | -------- | -------------------------------- | ------------------------------------------------------------ |
| apikey         | Yes      | 3fdae2c8b32348a3855af9f0377191d4 | Unique ID to identify the requester (provided by onlinewerkrooster.be team) |
| content-type   | Yes      | application/json                 | JSON data                                                    |
| Accept-Langueg | No       | nl                               | Language used to get translatable values.                    |

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

[back to overview](README.md)