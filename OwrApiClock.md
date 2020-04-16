## Clock API

Clock API is intended to be able to retrieve or manipulate time clock info from the Onlinewerkrooster application. 

### Endpoint

https://services.onlinewerkrooster.be/api/clock/

## GET /registered/:id

URL: **.../api/clock/registered**

### Use cases

- Start working - clockin
- Start break - breakIn
- End break - breakOut
- End working - clockOut

### Example Request

#### Header

| Name   | Required | Value                            | Remarks                                                      |
| ------ | -------- | -------------------------------- | ------------------------------------------------------------ |
| Apikey | Yes      | 3fdae2c8b32348a3855af9f0377191d4 | Unique ID to identify the source to query data. (provided by onlinewerkrooster.be team) |
| content-type | Yes      | application/json | JSON data |

#### URL Parameters

| Field name | Type                 | Required | Value                  | Remarks                   |
| ---------- | -------------------- | -------- | ---------------------- | ------------------------- |
| dateFrom   | Timestamp (ISO 8601) | Yes      | 2018-03-15T13:46:50.52 | Start Date/Time of period |
| dateTo     | Timestamp (ISO 8601) | Yes      | 2018-03-15T14:46:50.52 | End Date/Time of period   |

```
https://services.onlinewerkrooster.be/api/clock/registered?dateFrom=2018-08-01T00:00:00&dateTo=2018-08-31T23:59:59
```

Add the id to the end of the URL to retrieve the data for a single record.

**https://services.onlinewerkrooster.be/api/clock/registered/1** would retrieve the planning data for timeClockData ID **1**

#### Body

N/A

#### CURL
```
curl --request GET \
  --url 'https://services.onlinewerkrooster.be/api/clock/registered?dateTo=2018-08-31T23%3A59%3A59&dateFrom=2018-08-01T00%3A00%3A00' \
  --header 'apikey: 8689DB67-D12C-46A5-B4F9-74E70D1B37CF' \
  --header 'content-type: application/json'
```

### Example Response (Success)

```json
[
	 {
    "id": 18567,
    "time": {
      "start": "2019-05-04T09:05:00.000Z",
      "end": "2019-05-04T16:00:00.000Z"
    },
    "timeActual": {
      "start": "2019-05-04T09:05:00.000Z",
      "end": "2019-05-04T15:58:00.000Z"
    },
    "workedTimeInMinutes": 415,
    "breaks": [],
    "breakTimeInMinutes": 0,
    "employee": {
      "id": 191,
      "employeeNumber": "191",
      "nationalInsuranceNumber": "00000000097"
    },
    "workspace": {
      "name": "M HKA zaal",
      "externalNumber": "MHKAZAAL"
    },
    "workArea": {
      "name": "bediende host",
      "externalId": 0,
      "externalNumber": "WORKAREA.58"
    },
    "createdOn": "2019-05-04T09:05:00.000Z",
    "modifiedOn": null
  },
  {
    "id": 18568,
    "time": {
      "start": "2019-05-04T09:07:00.000Z",
      "end": "2019-05-04T16:00:00.000Z"
    },
    "timeActual": {
      "start": "2019-05-04T09:07:00.000Z",
      "end": "2019-05-04T15:56:00.000Z"
    },
    "workedTimeInMinutes": 399,
    "breaks": [
      {
        "time": {
          "start": "2019-05-04T11:01:00.000Z",
          "end": "2019-05-04T11:15:00.000Z"
        },
        "timeInMinutes": 14
      }
    ],
    "breakTimeInMinutes": 14,
    "employee": {
      "id": 182,
      "employeeNumber": "182",
      "nationalInsuranceNumber": "00000000097"
    },
    "workspace": {
      "name": "M HKA zaal",
      "externalNumber": "MHKAZAAL"
    },
    "workArea": {
      "name": "bediende host",
      "externalId": 0,
      "externalNumber": "WORKAREA.58"
    },
    "createdOn": "2019-05-04T09:07:00.000Z",
    "modifiedOn": null
  },
]
```

## POST /

### Use cases

- Perform a timeclock action for a user (Clock in, Clock out, Break in , Break out)

### Example Request

#### Header

| Name   | Required | Value                            | Remarks                                                      |
| ------ | -------- | -------------------------------- | ------------------------------------------------------------ |
| Apikey | Yes      | 3fdae2c8b32348a3855af9f0377191d4 | Unique ID to identify the source to query data. (provided by onlinewerkrooster.be team) |
| content-type | Yes      | application/json | JSON data |

#### Request body

| Field name              | Type                 | Required | Value                                            | Remarks                                 |
| ----------------------- | -------------------- | -------- | ------------------------------------------------ | --------------------------------------- |
| nationalInsuranceNumber | String               | Yes      | 87082020907                                      | National insurance number               |
| timestamp               | Timestamp (ISO 8601) | Yes      | 2018-03-15T14:46:50.52                           | Date/Time of clocking                   |
| type                    | String               | Yes      | ClockIn<br />BreakIn<br />BreakOut<br />ClockOut | Action to indicate what has to be done. |

#### Body

```
{
	"nationalInsuranceNumber": "87082020907",
	"timestamp": "2019-06-03T16:35:40+0200",
	"type": "clockOut"
}
```

#### CURL

```
curl --request POST \
  --url https://services.onlinewerkrooster.be/api/clock/ \
  --header 'apikey: 48E9970E-641C-83A8-DE77-C0FB70ADB6C4' \
  --header 'content-type: application/json' \
  --data '{
	"nationalInsuranceNumber": "87082020907",
	"timestamp": "2019-06-03T16:35:40+0200",
	"type": "clockIn"
}'
```

### Example Response (Success)

```json
{
  "id": 1,
  "validTo": "2020-01-15T12:04:00.000Z",
  "ssn": "87082020807",
  "pin": "1234",
  "timeStamp": "2020-01-15T11:34:00.000Z",
  "action": 0,
  "message": "John Doe, je bent succesvol ingeklokt omstreeks 15/01/20 12:34 (12:34)"
}
```

### Example Response (Error)

It may happen something goes wrong while querying timeClock data due to various reasons, in the list below you can a list of errors.

In general, when you're sure you specified the correct values, you can always contact the onlinewerkrooster.be support (support@onlinewerkrooster.be)

| Error code                  | Error Message                                    | Explanation                                      | Solution          |
| --------------------------- | ------------------------------------------------ | ------------------------------------------------ | ----------------- |
| 404 - Not found             | No data found while data was expected.           | URL parameters do not match with data.           | Check the values. |
| 400 - Bad Request           | Invalid request due to wrong/missing parameters. | Invalid request due to wrong/missing parameters. | Check the values. |
| 401 - Bad Request           | Not authorized.                                  | Invalid ApiKey                                   | Check the values. |
| 409 - Conflict error        | Short code of what's conflicting.                | Message to indicate what's wrong                 | Check the values. |
| 500 - Internal Server Error | An unexpected (technical) error occurred.        |                                                  | Contact Support   |

[back to overview](README.md)
