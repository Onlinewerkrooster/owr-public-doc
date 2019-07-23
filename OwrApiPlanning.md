## Planning API

Planning API is intended to be able to retrieve planning info from the Onlinewerkrooster.be application. 

### Endpoint

https://services.onlinewerkrooster.be/api/planning

## GET /:id

### Use cases

- Retrieve an overview of the planning within a date period.
- Retrieve a single planning record

### Example Request

#### Header

| Name   | Required | Value                            | Remarks                                                      |
| ------ | -------- | -------------------------------- | ------------------------------------------------------------ |
| Apikey | Yes      | 3fdae2c8b32348a3855af9f0377191d4 | Unique ID to identify the source to query data. (provided by onlinewerkrooster.be team) |

#### URL Parameters

| Field name | Type                 | Required | Value                  | Remarks                            |
| ---------- | -------------------- | -------- | ---------------------- | ---------------------------------- |
| dateFrom   | Timestamp (ISO 8601) | Yes      | 2018-03-15T13:46:50.52 | Start Date/Time of period          |
| dateTo     | Timestamp (ISO 8601) | Yes      | 2018-03-15T14:46:50.52 | End Date/Time of period            |
| confirmed  | Boolean              | No       | true                   | Is planning confirmed by employee? |
| rejected   | Boolean              | No       | false                  | Is planning rejected by employee?  |

```
https://owr-public-services-prod.herokuapp.com/api/planning?dateFrom=2018-01-01T00:00:00&dateTo=2018-08-31T23:59:59&confirmed=true
```

Add the id to the end of the URL to retrieve the data for a single record.

**https://owr-public-services-prod.herokuapp.com/api/planning/1** would retrieve the planning data for planning ID **1**

#### Body

N/A

#### CURL
```
curl --request GET \
  --url 'https://owr-public-services-prod.herokuapp.com/api/planning?dateTo=2018-08-31T23%3A59%3A59&dateFrom=2018-08-01T00%3A00%3A00confirmed=true' \
  --header 'apikey: 8689DB67-D12C-46A5-B4F9-74E70D1B37CF' \
  --header 'content-type: application/json'
```

### Example Response (Success)

```json
[
  {
    "id": 27688,
    "time": {
      "start": "2019-07-08T06:00:00.000Z",
      "end": "2019-07-08T11:30:00.000Z"
    },
    "employee": {
      "id": 83,
      "employeeNumber": "83",
      "nationalInsuranceNumber": "00000000097"
    },
    "workspace": {
      "name": "M HKAFE",
      "externalNumber": "MHKAFE"
    },
    "workArea": {
      "name": "bediende M HKAfe",
      "externalId": 0,
      "externalNumber": "WORKAREA.59"
    },
    "isConfirmed": true,
    "isRejected": false,
    "isMailed": false,
    "isSmsSent": false,
    "remarks": "",
    "createdOn": null,
    "modifiedOn": null
  },
  {
    "id": 23280,
    "time": {
      "start": "2019-07-09T09:00:00.000Z",
      "end": "2019-07-09T16:00:00.000Z"
    },
    "employee": {
      "id": 84,
      "employeeNumber": "84",
      "nationalInsuranceNumber": "00000000097"
      "nationalInsuranceNumber": ""
    },
    "workspace": {
      "name": "M HKAFE",
      "externalNumber": "MHKAFE"
    },
    "workArea": {
      "name": "bediende M HKAfe",
      "externalId": 0,
      "externalNumber": "WORKAREA.59"
    },
    "isConfirmed": true,
    "isRejected": false,
    "isMailed": true,
    "isSmsSent": false,
    "remarks": "Keuken",
    "createdOn": null,
    "modifiedOn": null
  }
]
```



### Example Response (Error)

It may happen something goes wrong while querying planning data due to various reasons, in the list below you can a list of errors.

In general, when you're sure you specified the correct values, you can always contact the onlinewerkrooster.be support (support@onlinewerkrooster.be)

| Error code                  | Error Message                                    | Explanation                                      | Solution          |
| --------------------------- | ------------------------------------------------ | ------------------------------------------------ | ----------------- |
| 404 - Not found             | No data found while data was expected.           | URL parameters do not match with data.           | Check the values. |
| 400 - Bad Request           | Invalid request due to wrong/missing parameters. | Invalid request due to wrong/missing parameters. | Check the values. |
| 401 - Bad Request           | Not authorized.                                  | Invalid ApiKey                                   | Check the values. |
| 500 - Internal Server Error | An unexpected (technical) error occurred.        |                                                  | Contact Support   |

[back to overview](OnlineWerkroosterAPI.md)
