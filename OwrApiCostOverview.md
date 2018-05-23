## CostOverview API

CostOverview API is intended to be able to retrieve cost overview info from the Onlinewerkrooster.be application. 

"Date from" & "Date To" are required parameters to limit the results.

### Endpoint

https://www.onlinewerkrooster.be/APIOWR/api/CostOverview/GetCostOverview?dateFrom=2018-03-01T12:00&dateTo=2018-03-01T23:00

### Use cases

- Retrieve cost overview data for a certain period.

### Example Request

#### Header

| Name         | Required | Value                                | Remarks                                                      |
| ------------ | -------- | ------------------------------------ | ------------------------------------------------------------ |
| Apikey       | Yes      | 3fdae2c8b32348a3855af9f0377191d4     | Unique ID to identify the source to query data. (provided by onlinewerkrooster.be team) |
| content-type | Yes      | application/json                     | JSON data                                                    |
| UserId       | Yes      | 81ad2f9b-6362-4388-9617-96a18524850c | Unique ID to identify the requester. (provided by the onlinewerkrooster.be team) |

#### URL Parameters

| Field name | Type                 | Required | Value                  | Remarks                   |
| ---------- | -------------------- | -------- | ---------------------- | ------------------------- |
| dateFrom   | Timestamp (ISO 8601) | Yes      | 2018-03-15T13:46:50.52 | Start Date/Time of period |
| dateTo     | Timestamp (ISO 8601) | Yes      | 2018-03-15T14:46:50.52 | End Date/Time of period   |

```
https://www.onlinewerkrooster.be/APIOWR/api/CostOverview/GetCostOverview?dateFrom=2018-03-01T12:00&dateTo=2018-03-01T23:00
```

#### Body

N/A

#### CURL
```
curl --request GET \
  --url 'https://www.onlinewerkrooster.be/APIOWR/api/CostOverview/GetCostOverview?dateTo=2018-03-01T23%3A00&dateFrom=2018-03-01T12%3A00' \
  --header 'apikey: 4ecc0220-cad5-466b-be0b-5f4cd1ceb28d' \
  --header 'content-type: application/json' \
  --header 'userid: 5C848603-18B5-4EE8-AC3D-88F0E6FC1780'
```

### Example Response (Success)

```
[
	{
		"TransDatetime": "2018-03-01T12:00:00",
		"HoursWorked": 3.0,
		"CostAmount": 63.0
	},
	{
		"TransDatetime": "2018-03-01T13:00:00",
		"HoursWorked": 3.0,
		"CostAmount": 63.0
	},
	{
		"TransDatetime": "2018-03-01T14:00:00",
		"HoursWorked": 1.25,
		"CostAmount": 26.25
	},
	{
		"TransDatetime": "2018-03-01T15:00:00",
		"HoursWorked": 0.0,
		"CostAmount": 0.0
	},
	{
		"TransDatetime": "2018-03-01T16:00:00",
		"HoursWorked": 0.0,
		"CostAmount": 0.0
	},
	{
		"TransDatetime": "2018-03-01T17:00:00",
		"HoursWorked": 1.5,
		"CostAmount": 31.5
	},
	{
		"TransDatetime": "2018-03-01T18:00:00",
		"HoursWorked": 4.0,
		"CostAmount": 84.0
	},
	{
		"TransDatetime": "2018-03-01T19:00:00",
		"HoursWorked": 4.0,
		"CostAmount": 84.0
	},
	{
		"TransDatetime": "2018-03-01T20:00:00",
		"HoursWorked": 4.0,
		"CostAmount": 84.0
	},
	{
		"TransDatetime": "2018-03-01T21:00:00",
		"HoursWorked": 3.0,
		"CostAmount": 63.0
	},
	{
		"TransDatetime": "2018-03-01T22:00:00",
		"HoursWorked": 1.25,
		"CostAmount": 26.25
	},
	{
		"TransDatetime": "2018-03-01T23:00:00",
		"HoursWorked": 0.0,
		"CostAmount": 0.0
	}
]
```



### Example Response (Error)

It may happen something goes wrong while querying cost overview data due to various reasons, in the list below you can a list of errors.

In general, when you're sure you specified the correct values, you can always contact the onlinewerkrooster.be support (support@onlinewerkrooster.be)

| Error code                  | Error Message                                                | Explanation                                     | Solution          |
| --------------------------- | ------------------------------------------------------------ | ----------------------------------------------- | ----------------- |
| 500 - Internal Server Error | Unauthorized: Invalid ApiKey/UserId!                         | The combination "ApiKey" & "UserId" is invalid. | Check the values. |
| 400 - Bad Request           | Header ApiKey is required!          .                        | Required field.                                 | Check the values. |
| 400 - Bad Request           | Header ApiKey is required!                                   | Required field.                                 | Check the values. |
| 400 - Bad Request           | Incomplete request: DateFrom empty                           | Required field.                                 | Check the values. |
| 400 - Bad Request           | Incomplete request: DateTo empty                             | Required field.                                 | Check the values. |
| 400 - Bad Request           | An error occurred while executing the command definition. See the inner exception for details. |                                                 | Contact Support   |

[back to overview](OnlineWerkroosterAPI.md)