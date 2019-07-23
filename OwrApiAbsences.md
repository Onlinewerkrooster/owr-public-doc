## Absences API

Employee API is intended to be able to retrieve/create absence info from the Onlinewerkrooster.be application. 

### Endpoint

https://services.onlinewerkrooster.be/api/absences

## GET /

### Use cases

- Retrieve a list of absences between a period
- Retrieve a list of absences between a period filtered on parameters

### Example Request

#### Header

| Name   | Required | Value                            | Remarks                                                      |
| ------ | -------- | -------------------------------- | ------------------------------------------------------------ |
| Apikey | Yes      | 3fdae2c8b32348a3855af9f0377191d4 | Unique ID to identify the source to query data. (provided by onlinewerkrooster.be team) |

#### URL Parameters

| Field name               | Type                 | Required | Value                       | Remarks                                      |
| ------------------------ | -------------------- | -------- | --------------------------- | -------------------------------------------- |
| dateFrom                 | Timestamp (ISO 8601) | Yes      | 2018-03-15T13:46:50.52      | Start Date/Time of period                    |
| dateTo                   | Timestamp (ISO 8601) | Yes      | 2018-03-15T14:46:50.52      | End Date/Time of period                      |
| status                   | String               | No       | APPROVED/REJECTED/REQUESTED | Absence status from employee's point of view |
| holidayTypeExportPayroll | Boolean              | No       | false                       | Absence applicable for payroll?              |

```
https://owr-public-services-dev.herokuapp.com/api/absences?dateFrom=2019-01-07T22%3A00%3A00Z&dateTo=2019-09-30T22%3A00%3A00Z&status=APPROVED&holidayTypeExportPayroll=true
```

#### Body

N/A

#### CURL

```
curl --request GET \
  --url 'https://owr-public-services-prod.herokuapp.com/api/absences?dateFrom=2019-01-07T22%3A00%3A00Z&dateTo=2019-09-30T22%3A00%3A00Z&status=APPROVED&holidayTypeExportPayroll=true' \
  --header 'apikey: 51703F12-56FC-4AF4-B911-DDADCA2BE6BE' \
  --header 'content-type: application/json'
```

### Example Response (Success)

```json
[
  {
    "id": 1282,
    "employee": {
      "id": 389,
      "nationalInsuranceNumber": "00000000097",
      "externalId": 0,
      "externalNumber": "",
      "employeeNumber": "196"
    },
    "absenceType": {
      "name": "Feestdag",
      "reportingCode": null
    },
    "date": "2019-04-30T22:00:00.000Z",
    "durationInMinutes": 480,
    "dayPart": 0,
    "startTime": "Open"
  },
  {
    "id": 1283,
    "employee": {
      "id": 381,
      "nationalInsuranceNumber": "00000000198",
      "externalId": 0,
      "externalNumber": "",
      "employeeNumber": "188"
    },
    "absenceType": {
      "name": "Feestdag",
      "reportingCode": null
    },
    "date": "2019-04-30T22:00:00.000Z",
    "durationInMinutes": 480,
    "dayPart": 0,
    "startTime": "Open"
  }
]
```

## POST /bulk/

https://services.onlinewerkrooster.be/api/absences/bulk

## Use cases

- Create absence in OWR
- Update absence in OWR

### Example Request

#### Header

| Name   | Required | Value                            | Remarks                                                      |
| ------ | -------- | -------------------------------- | ------------------------------------------------------------ |
| Apikey | Yes      | 3fdae2c8b32348a3855af9f0377191d4 | Unique ID to identify the source to query data. (provided by onlinewerkrooster.be team) |

#### Body

| Field name         | Type              | Required       | Value      | Remarks                                          |
| ------------------ | ----------------- | -------------- | ---------- | ------------------------------------------------ |
| period.start       | Date              | Yes            | 2019-08-01 | Start of period.                                 |
| period.end         | Date              | Yes            | 2019-08-31 | End of period.                                   |
| absences[]         | Array of absences | Yes            |            |                                                  |
| .employeeNum       | String            | Yes            | 180        | Employee Number                                  |
| .absenceType       | String            | Yes            | PT-ABSENCE | Name of absence type known in OWR                |
| .date              | Date              | Yes            | 2019-08-11 | Date of absence                                  |
| .durationInMinutes | Number            | Conditionally* | 480        | Duration (**in minutes**)                        |
| .startTime         | String            | Conditionally* | 11:00      | Start time (in HH:MM)                            |
| .dayPart           | Number            | Conditionally* | 0/1/2      | 0 - full day<br />1 - morning<br />2 - afternoon |

**

Either `dayPart`or `startTime + durationInMinutes` is required.

##### JSON

```json
{
	"period": {
		"start": "2019-08-01",
		"end": "2019-08-31"
	},
	"absences": [
		{
			"employeeNum": "180",
			"absenceType": "PT-ABSENCE",
			"date": "2019-08-10",
			"durationInMinutes": 480,
			"startTime": "10:00"
		},
		{
			"employeeNum": "180",
			"absenceType": "PT-ABSENCE",
			"date": "2019-08-11",
			"dayPart": 0
		}
	]
}
```

#### CURL

```
curl --request POST \
  --url https://owr-public-services-dev.herokuapp.com/api/absences/bulk \
  --header 'apikey: 51703F12-56FC-4AF4-B911-DDADCA2BE6BE' \
  --header 'content-type: application/json' \
  --data '{
	"period": {
		"start": "2019-08-01",
		"end": "2019-08-31"
	},
	"absences": [
		{
			"employeeNum": "180",
			"absenceType": "PT-ABSENCE",
			"date": "2019-08-10",
			"durationInMinutes": 480,
			"startTime": "10:00"
		},
		{
			"employeeNum": "180",
			"absenceType": "PT-ABSENCE",
			"date": "2019-08-11",
			"dayPart": 0
		}
	]
}'
```

### Example Response (Success)

```json
[
  {
    "id": 2782,
    "employee": {
      "id": 373,
      "nationalInsuranceNumber": "00000000097",
      "externalId": 0,
      "externalNumber": "",
      "employeeNumber": "180"
    },
    "absenceType": {
      "name": "PT-ABSENCE",
      "reportingCode": "9999"
    },
    "date": "2019-08-10T00:00:00.000Z",
    "durationInMinutes": 480,
    "dayPart": 0,
    "startTime": "10:00",
    "status": "APPROVED"
  },
  {
    "id": 2783,
    "employee": {
      "id": 373,
      "nationalInsuranceNumber": "00000000097",
      "externalId": 0,
      "externalNumber": "",
      "employeeNumber": "180"
    },
    "absenceType": {
      "name": "PT-ABSENCE",
      "reportingCode": "9999"
    },
    "date": "2019-08-11T00:00:00.000Z",
    "durationInMinutes": 0,
    "dayPart": 0,
    "startTime": "04:00",
    "status": "APPROVED"
  }
]
```

### Example Response (Error)

It may happen something goes wrong while querying employee data due to various reasons, in the list below you can a list of errors.

In general, when you're sure you specified the correct values, you can always contact the onlinewerkrooster.be support (support@onlinewerkrooster.be)

| Error code                  | Error Message                                    | Explanation                                      | Solution          |
| --------------------------- | ------------------------------------------------ | ------------------------------------------------ | ----------------- |
| 404 - Not found             | No data found while data was expected.           | URL parameters do not match with data.           | Check the values. |
| 400 - Bad Request           | Invalid request due to wrong/missing parameters. | Invalid request due to wrong/missing parameters. | Check the values. |
| 401 - Bad Request           | Not authorized.                                  | Invalid ApiKey                                   | Check the values. |
| 500 - Internal Server Error | An unexpected (technical) error occurred.        |                                                  | Contact Support   |

[back to overview](OnlineWerkroosterAPI.md)