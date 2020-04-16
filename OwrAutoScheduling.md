# Auto Scheduling

The AutoScheduling endpoint is intended to fetch auto scheduling from OWR, or create/update auto scheduling related data into OWR.

### Endpoint

https://services.onlinewerkrooster.be/api/auto-scheduling/

### Use cases

- Create resource needs (shift demands) 

## POST /resource-needs/daily

This API is intended to create *resource needs* on a daily basis. The resource need is an object that contains the information about a single shift:

- Business date
- Effective datetime
- Workarea (skill/location)
- Amount of people needed

### Example Request

#### Header

| Name         | Required | Value                            | Remarks                                                      |
| ------------ | -------- | -------------------------------- | ------------------------------------------------------------ |
| Apikey       | Yes      | 3fdae2c8b32348a3855af9f0377191d4 | Unique ID to identify the source to query data. (provided by onlinewerkrooster.be team) |
| content-type | Yes      | application/json                 | JSON data                                                    |

#### Body

| Field name                        | Type    | Required | Value      | Remarks                                                      |
| --------------------------------- | ------- | -------- | ---------- | ------------------------------------------------------------ |
| overwrite                         | boolean | No       | true/false | If set to true, existing data is overwritten                 |
| shiftDurationInMinutes            | number  | Yes      | 15/30/60   | The duration of a single shift. Used to determine end time.  |
| businessDate                      | Date    | Yes      |            | Effective business date. 01:00 after midnight may belong to the previous day b/c active workhours are 06:00-02:00 |
| needs                             | array   | Yes      |            | List of shifts                                               |
| need[].effectiveDatetime          | Date    | Yes      |            | Start datetime of shift                                      |
| need[].totalAmount                | Number  | Yes      |            | Total amount of people needed for shift (for ALL workareas)  |
| need[].expectedRevenuePerGuest    | Number  | No       |            | Amount of expected revenue per guest during the shift.       |
| need[].expectedGuestAmount        | Number  | No       |            | Amount of guests expected during the shift.                  |
| need[].expectedRevenue            | Number  | No       |            | Amount of revenue during the shift.                          |
| need[].workareas                  | array   | Yes      |            | List of workares                                             |
| need[].workareas[].externalNumber | String  | Yes      |            | Unique alphanumeric number to identify workarea              |
| need[].workareas[].amount         | Number  | Yes      |            | Amount of people needed during the shift for given workarea. |

##### JSON

```json
{
	"overwrite": true,
	"shiftDurationInMinutes": 60,
	"businessDate": "2020-02-01",
	"needs": [
		{
			"effectiveDatetime": "2020-02-01T10:00:00Z",
			"totalAmount": 3,
			"expectedRevenuePerGuest": 15.5,
			"expectedGuestAmount": 3,
			"expectedRevenue": 46.5,
			"workareas": [
				{
					"externalNumber": "100",
					"amount": 2
				},
				{
					"externalNumber": "102",
					"amount": 1
				}
			]
		},
		{
			"effectiveDatetime": "2020-02-01T11:00:00Z",
			"totalAmount": 4,
			"expectedRevenuePerGuest": 15.5,
			"expectedGuestAmount": 4,
			"expectedRevenue": 62,
			"workareas": [
				{
					"externalNumber": "100",
					"amount": 2
				},
				{
					"externalNumber": "102",
					"amount": 2
				}
			]
		}
	]
}
```

#### CURL

```
curl --request POST \
  --url https://services.onlinewerkrooster.be/api/auto-scheduling/resource-needs/daily \
  --header 'apikey: 0BDF3878-1A5D-4CEA-52D8-310C94A87440' \
  --header 'cache-control: no-cache' \
  --header 'content-type: application/json' \
  --data '{
	"overwrite": true,
	"shiftDurationInMinutes": 60,
	"businessDate": "2020-02-01",
	"needs": [
		{
			"effectiveDatetime": "2020-02-01T10:00:00Z",
			"totalAmount": 3,
			"expectedRevenuePerGuest": 15.5,
			"expectedGuestAmount": 3,
			"expectedRevenue": 46.5,
			"workareas": [
				{
					"externalNumber": "100",
					"amount": 2
				},
				{
					"externalNumber": "102",
					"amount": 1
				}
			]
		},
		{
			"effectiveDatetime": "2020-02-01T11:00:00Z",
			"totalAmount": 4,
			"expectedRevenuePerGuest": 15.5,
			"expectedGuestAmount": 4,
			"expectedRevenue": 62,
			"workareas": [
				{
					"externalNumber": "100",
					"amount": 2
				},
				{
					"externalNumber": "102",
					"amount": 2
				}
			]
		}
	]
}'
```

### Example Response (Success)

```json
[
  {
    "id": 25033,
    "workarea": {
      "id": 66,
      "name": "Productief",
      "externalId": 100,
      "externalNumber": "100",
      "workspaceId": null
    },
    "businessDate": "2020-02-01T00:00:00.000Z",
    "effectiveDatetime": "2020-02-01T10:00:00.000Z",
    "startDatetime": "2020-02-01T10:00:00.000Z",
    "endDatetime": "2020-02-01T10:59:59.000Z",
    "amount": 2
  },
  {
    "id": 25034,
    "workarea": {
      "id": 65,
      "name": "Frietjes",
      "externalId": 102,
      "externalNumber": "102",
      "workspaceId": null
    },
    "businessDate": "2020-02-01T00:00:00.000Z",
    "effectiveDatetime": "2020-02-01T10:00:00.000Z",
    "startDatetime": "2020-02-01T10:00:00.000Z",
    "endDatetime": "2020-02-01T10:59:59.000Z",
    "amount": 1
  },
  {
    "id": 25035,
    "workarea": {
      "id": 66,
      "name": "Productief",
      "externalId": 100,
      "externalNumber": "100",
      "workspaceId": null
    },
    "businessDate": "2020-02-01T00:00:00.000Z",
    "effectiveDatetime": "2020-02-01T11:00:00.000Z",
    "startDatetime": "2020-02-01T11:00:00.000Z",
    "endDatetime": "2020-02-01T11:59:59.000Z",
    "amount": 2
  },
  {
    "id": 25036,
    "workarea": {
      "id": 65,
      "name": "Frietjes",
      "externalId": 102,
      "externalNumber": "102",
      "workspaceId": null
    },
    "businessDate": "2020-02-01T00:00:00.000Z",
    "effectiveDatetime": "2020-02-01T11:00:00.000Z",
    "startDatetime": "2020-02-01T11:00:00.000Z",
    "endDatetime": "2020-02-01T11:59:59.000Z",
    "amount": 2
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

[back to overview](README.md)