# Events API

Events API is intended to be able to retrieve and create event info from the Onlinewerkrooster.be application.  A list of error codes is documented below in this document.

## Endpoint

https://owr-public-services-prod.herokuapp.com/api/events

## POST api/events

### Example Request

#### Header

| Name         | Required | Value                                | Remarks                                                      |
| ------------ | -------- | ------------------------------------ | ------------------------------------------------------------ |
| apikey       | Yes      | 3fdae2c8b32348a3855af9f0377191d4     | Unique ID to identify the requester (provided by onlinewerkrooster.be team) |
| content-type | Yes      | application/json                     | JSON data                                                    |

#### Body

```
{
    "extEventId": 10001,
    "extEventNumber": "10001",
    "name": "OWR.TESTEVENT.10001",
    "date":"2018-10-26T00:00:00",
    "extCustomerNumber": "1001",
    "eventPeriod": {
        "start": "2018-10-26T14:00:00",
        "end": "2018-10-26T20:00:00"
    },
    "managerINSS": "99123199999",
    "numOfEmployees": 15
}
```

| Field name        | Type                 | Required | Value                | Remarks                                                      |
| ----------------- | -------------------- | -------- | -------------------- | ------------------------------------------------------------ |
| extEventId        | Numeric              | Yes      | 100001               | Numeric (unique) identifier of event in the 3rd party system. |
| extEventNumber    | String               | Yes      | 100001               | Alphanumeric (unique) identifier of event in the 3rd party system. |
| name              | String               | Yes      | OWR.TESTEVENT.100001 | Name of event                                                |
| date              | Timestamp (ISO 8601) | Yes      | 2018-10-26T00:00:00  | Date/Time of the event                                       |
| extCustomerNumber | String               | Yes      | 1001                 | Alphanumeric identifier of the customer in the 3rd party system. |
| eventPeriod.start | Timestamp (ISO 8601) | Yes      | 2018-10-26T14:00:00  | Start datetime of event                                      |
| eventPeriod.end   | Timestamp (ISO 8601) | Yes      | 2018-10-26T20:00:00  | end datetime of event                                        |
| managerINSS       | String               | Yes      | 99123199999          | National Insurance Number of the manager of the event.       |
| numOfEmployees    | Number               | Yes      | 15                   | Amount of employees needed for event.                        |

#### CURL

```
curl --request POST \
  --url https://owr-public-services-dev.herokuapp.com/api/events/ \
  --header 'apikey: 4C6086B2-4201-4CD6-A94A-BB89684FD0BE' \
  --header 'content-type: application/json' \
  --data '{
    "extEventId": 10001,
    "extEventNumber": "10001",
    "name": "OWR.TESTEVENT.10001",
    "date":"2018-10-26T00:00:00",
    "extCustomerNumber": "10001",
    "eventPeriod": {
        "start": "2018-10-26T14:00:00",
        "end": "2018-10-26T20:00:00"
    },
    "managerINSS": "99.12.31-99999",
    "numOfEmployees": 15
}'
```

### Example Response (Success)

```json
{
	"companyId": 2,
	"eventId": 8138,
	"extEventId": 10001,
	"extEventNumber": "10001"
}
```

## GET api/events/timeClock

### Example Request

#### Header

| Name         | Required | Value                                | Remarks                                                      |
| ------------ | -------- | ------------------------------------ | ------------------------------------------------------------ |
| Apikey       | Yes      | 3fdae2c8b32348a3855af9f0377191d4     | Unique ID to identify the source to query data. (provided by onlinewerkrooster.be team) |
| content-type | Yes      | application/json                     | JSON data                                                    |

#### URL Parameters

| Field name     | Type                 | Required       | Value                  | Remarks                                           |
| -------------- | -------------------- | -------------- | ---------------------- | ------------------------------------------------- |
| extEventNumber | String               | Conditionally* | 10001                  | Unique event number in the 3rd party application. |
| dateFrom       | Timestamp (ISO 8601) | Conditionally* | 2018-03-15T13:46:50.52 | Start Date/Time of period                         |
| dateTo         | Timestamp (ISO 8601) | Conditionally* | 2018-03-15T14:46:50.52 | End Date/Time of period                           |

```
https://owr-public-services-prod.herokuapp.com/api/events/timeclock/?extEventNumber=10001&dateTo=2018-10-14T23%3A59%3A59&dateFrom=2018-10-08
```

#### Body

N/A

#### CURL

```
curl --request GET \
  --url 'https://owr-public-services-prod.herokuapp.com/api/events/timeclock/?extEventNumber=10001&dateTo=2018-10-14T23%3A59%3A59&dateFrom=2018-10-08' \
  --header 'apikey: 4C6086B2-4201-4CD6-A94A-BB89684FD0BD'
```

### Example Response (Success)

```
[
	{
		"companyId": 2,
		"extEventId": 10001,
		"extEventNumber": "10001",
		"timeClock": [
			{
				"time": {
					"start": "2018-10-09T07:10:00.000Z",
					"end": "2018-10-09T21:20:00.000Z"
				},
				"timeActual": {
					"start": "2018-10-09T07:15:00.000Z",
					"end": "2018-10-09T21:21:00.000Z"
				},
				"breakTimeInMinutes": 0,
				"workedTimeInMinutes": 850,
				"employee": {
					"firstName": "Joske",
					"lastName": "Vermeulen",
					"statute": {
						"id": 1,
						"name": "Student"
					}
				}
			}
		]
	},
	{
		"companyId": 2,
		"extEventId": 10002,
		"extEventNumber": "10002",
		"timeClock": [
			{
				"time": {
					"start": "2018-10-10T10:20:00.000Z",
					"end": "2018-10-10T19:40:00.000Z"
				},
				"timeActual": {
					"start": "2018-10-10T10:28:00.000Z",
					"end": "2018-10-10T19:44:00.000Z"
				},
				"breakTimeInMinutes": 0,
				"workedTimeInMinutes": 560,
				"employee": {
					"firstName": "Joske",
					"lastName": "Vermeulen",
					"statute": {
						"id": 1,
						"name": "Student"
					}
				}
			}
   }
]
```

## GET api/events/planning

### Example Request

#### Header

| Name         | Required | Value                                | Remarks                                                      |
| ------------ | -------- | ------------------------------------ | ------------------------------------------------------------ |
| Apikey       | Yes      | 3fdae2c8b32348a3855af9f0377191d4     | Unique ID to identify the source to query data. (provided by onlinewerkrooster.be team) |
| content-type | Yes      | application/json                     | JSON data                                                    |

#### URL Parameters

| Field name     | Type                 | Required       | Value                  | Remarks                                           |
| -------------- | -------------------- | -------------- | ---------------------- | ------------------------------------------------- |
| extEventNumber | String               | Conditionally* | 10001                  | Unique event number in the 3rd party application. |
| dateFrom       | Timestamp (ISO 8601) | Conditionally* | 2018-03-15T13:46:50.52 | Start Date/Time of period                         |
| dateTo         | Timestamp (ISO 8601) | Conditionally* | 2018-03-15T14:46:50.52 | End Date/Time of period                           |

```
https://owr-public-services-prod.herokuapp.com/api/events/planning/?extEventNumber=10001&dateTo=2018-10-14T23%3A59%3A59&dateFrom=2018-10-08
```

#### Body

N/A

#### CURL

```
curl --request GET \
  --url 'https://owr-public-services-prod.herokuapp.com/api/events/planning/?extEventNumber=10001&dateTo=2018-10-14T23%3A59%3A59&dateFrom=2018-10-08' \
  --header 'apikey: 4C6086B2-4201-4CD6-A94A-BB89684FD0BD'
```

### Example Response (Success)

```
[
	{
		"companyId": 2,
		"extEventId": null,
		"extEventNumber": null,
		"planning": []
	},
	{
		"companyId": 2,
		"extEventId": null,
		"extEventNumber": null,
		"planning": [
			{
				"time": {
					"start": "2018-11-17T03:00:00.000Z",
					"end": "2018-11-18T01:00:00.000Z"
				},
				"totalBreaktime": 0,
				"totalWorktime": 22,
				"employee": {
					"firstName": "Pieter",
					"lastName": "Peeters",
					"statute": {
						"id": 4,
						"name": "Flexi"
					}
				}
			},
			{
				"time": {
					"start": "2018-11-17T03:00:00.000Z",
					"end": "2018-11-18T01:00:00.000Z"
				},
				"totalBreaktime": 0,
				"totalWorktime": 22,
				"employee": {
					"firstName": "Joske",
					"lastName": "Vermeulen",
					"statute": {
						"id": 1,
						"name": "Student"
					}
				}
			},
			{
				"time": {
					"start": "2018-11-17T03:00:00.000Z",
					"end": "2018-11-18T01:00:00.000Z"
				},
				"totalBreaktime": 0,
				"totalWorktime": 22,
				"employee": {
					"firstName": "Max",
					"lastName": "Verstappen",
					"statute": {
						"id": 4,
						"name": "Flexi"
					}
				}
			},
			{
				"time": {
					"start": "2018-11-17T03:00:00.000Z",
					"end": "2018-11-18T01:00:00.000Z"
				},
				"totalBreaktime": 0,
				"totalWorktime": 22,
				"employee": {
					"firstName": "Maria",
					"lastName": "Peeters",
					"statute": {
						"id": 4,
						"name": "Flexi"
					}
				}
			},
			{
				"time": {
					"start": "2018-11-17T03:00:00.000Z",
					"end": "2018-11-18T01:00:00.000Z"
				},
				"totalBreaktime": 0,
				"totalWorktime": 22,
				"employee": {
					"firstName": "stef",
					"lastName": "Peeters",
					"statute": {
						"id": 4,
						"name": "Flexi"
					}
				}
			},
			{
				"time": {
					"start": "2018-11-17T03:00:00.000Z",
					"end": "2018-11-18T01:00:00.000Z"
				},
				"totalBreaktime": 0,
				"totalWorktime": 22,
				"employee": {
					"firstName": "Wim",
					"lastName": "Vermeulen",
					"statute": {
						"id": 4,
						"name": "Flexi"
					}
				}
			},
			{
				"time": {
					"start": "2018-11-17T14:00:00.000Z",
					"end": "2018-11-18T01:00:00.000Z"
				},
				"totalBreaktime": 0,
				"totalWorktime": 11,
				"employee": {
					"firstName": "Jan",
					"lastName": "Jansen",
					"statute": {
						"id": 4,
						"name": "Flexi"
					}
				}
			}
		]
	},
	{
		"companyId": 2,
		"extEventId": null,
		"extEventNumber": null,
		"planning": []
	},	
	{
		"companyId": 2,
		"extEventId": null,
		"extEventNumber": null,
		"planning": [
			{
				"time": {
					"start": "2018-11-17T03:00:00.000Z",
					"end": "2018-11-18T01:00:00.000Z"
				},
				"totalBreaktime": 0,
				"totalWorktime": 22,
				"employee": {
					"firstName": "Pieter",
					"lastName": "Peeters",
					"statute": {
						"id": 4,
						"name": "Flexi"
					}
				}
			},
			{
				"time": {
					"start": "2018-11-17T03:00:00.000Z",
					"end": "2018-11-18T01:00:00.000Z"
				},
				"totalBreaktime": 0,
				"totalWorktime": 22,
				"employee": {
					"firstName": "Joske",
					"lastName": "Vermeulen",
					"statute": {
						"id": 1,
						"name": "Student"
					}
				}
			},
			{
				"time": {
					"start": "2018-11-17T03:00:00.000Z",
					"end": "2018-11-18T01:00:00.000Z"
				},
				"totalBreaktime": 0,
				"totalWorktime": 22,
				"employee": {
					"firstName": "Max",
					"lastName": "Verstappen",
					"statute": {
						"id": 4,
						"name": "Flexi"
					}
				}
			},
			{
				"time": {
					"start": "2018-11-17T03:00:00.000Z",
					"end": "2018-11-18T01:00:00.000Z"
				},
				"totalBreaktime": 0,
				"totalWorktime": 22,
				"employee": {
					"firstName": "stef",
					"lastName": "Peeters",
					"statute": {
						"id": 4,
						"name": "Flexi"
					}
				}
			},
			{
				"time": {
					"start": "2018-11-17T03:00:00.000Z",
					"end": "2018-11-18T01:00:00.000Z"
				},
				"totalBreaktime": 0,
				"totalWorktime": 22,
				"employee": {
					"firstName": "Maria",
					"lastName": "Peeters",
					"statute": {
						"id": 4,
						"name": "Flexi"
					}
				}
			},
			{
				"time": {
					"start": "2018-11-17T03:00:00.000Z",
					"end": "2018-11-18T01:00:00.000Z"
				},
				"totalBreaktime": 0,
				"totalWorktime": 22,
				"employee": {
					"firstName": "wim",
					"lastName": "Vermeulen",
					"statute": {
						"id": 4,
						"name": "Flexi"
					}
				}
			},
			{
				"time": {
					"start": "2018-11-17T14:00:00.000Z",
					"end": "2018-11-18T01:00:00.000Z"
				},
				"totalBreaktime": 0,
				"totalWorktime": 11,
				"employee": {
					"firstName": "Jan",
					"lastName": "Jansen",
					"statute": {
						"id": 4,
						"name": "Flexi"
					}
				}
			}
		]
	}
]
```



## Errors

It may happen something goes wrong when calling one of the APIs due to various reasons, in the list below you can a list of errors.

In general, when you're sure you specified the correct values, you can always contact the onlinewerkrooster.be support (support@onlinewerkrooster.be)

| Error code                  | Error Message                                    | Explanation                                      | Solution          |
| --------------------------- | ------------------------------------------------ | ------------------------------------------------ | ----------------- |
| 409 - Conflict              | Error code.                                      | Functional error.                                | Check the values. |
| 400 - Bad Request           | Invalid request due to wrong/missing parameters. | Invalid request due to wrong/missing parameters. | Check the values. |
| 401 - Unauthorized          | Not authorized.                                  | Invalid ApiKey                                   | Check the values. |
| 500 - Internal Server Error | An unexpected (technical) error occurred.        |                                                  | Contact Support   |

[back to overview](OnlineWerkroosterAPI.md)
