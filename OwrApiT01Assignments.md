## T01 Assignments API

Assignments API is intended to be able to retrieve assignment (contract) info from the Onlinewerkrooster.be application. 

### Endpoint

https://services.onlinewerkrooster.be/api/t02/assignments

## GET /

### Use cases

- Retrieve a list of assignments between a period

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

#### Body

N/A

#### CURL

```
curl --request GET \
  --url 'https://services.onlinewerkrooster.be/api/t01/assignments?dateFrom=2018-11-04T00%3A00%3A00Z&dateTo=2018-11-04T23%3A59%3A59Z' \
  --header 'apikey: 193D32CE-97D2-461A-8178-5811A0F5F890' \
  --header 'content-type: application/json'
```

### Example Response (Success)

```json
[
  {
    "id": 356,
    "status": 2,
    "remarks": "624670115000",
    "event_function_id": 356,
    "created_at": "2018-10-25T12:03:49.000Z",
    "updated_at": "2018-10-25T12:03:49.000Z",
    "wage_profile_id": null,
    "event_id": 356,
    "event.start": "2018-11-04T11:00:00.000Z",
    "event.end": "2018-11-04T15:00:00.000Z",
    "start": "2018-11-04T11:00:00.000Z",
    "end": "2018-11-04T15:00:00.000Z",
    "employee_id": 10,
    "IM_EventStatut": 4,
    "IM_EventStatutDescription": "FLEXI",
    "event_function.description": "hulpkelner(in) commis (bediening)",
    "event.name": "Pacific",
    "location": "Grote Markt 4, 3800 St Truiden",
    "UseDefault": "DFLT",
    "ExternalRefId": ""
  },
  {
    "id": 360,
    "status": 2,
    "remarks": "624670110000",
    "event_function_id": 360,
    "created_at": "2018-10-25T12:03:50.000Z",
    "updated_at": "2018-10-25T12:03:50.000Z",
    "wage_profile_id": null,
    "event_id": 360,
    "event.start": "2018-11-04T09:00:00.000Z",
    "event.end": "2018-11-04T18:45:00.000Z",
    "start": "2018-11-04T09:00:00.000Z",
    "end": "2018-11-04T18:45:00.000Z",
    "employee_id": 18,
    "IM_EventStatut": 1,
    "IM_EventStatutDescription": "STUDENT",
    "event_function.description": "hulpkelner(in) commis (bediening)",
    "event.name": "Pacific",
    "location": "Grote Markt 4, 3800 St Truiden",
    "UseDefault": "DFLT",
    "ExternalRefId": ""
  }
]
```

## GET /:id

https://services.onlinewerkrooster.be/api/t01/assignments/;id

## Use cases

- Get details of a single assignment (contract) in OWR

#### URL Parameters

N/A

### Body

N/A

#### CURL

```
curl --request GET \
  --url 'https://services.onlinewerkrooster.be/api/t01/assignments/356' \
  --header 'apikey: 193D32CE-97D2-461A-8178-5811A0F5F800' \
  --header 'content-type: application/json'
```

### Example Response (Success)

```json
{
  "id": 356,
  "status": 10,
  "remarks": "624670115700",
  "event_function_id": 356,
  "created_at": "2018-10-25T12:03:49.000Z",
  "updated_at": "2018-10-25T12:03:49.000Z",
  "wage_profile_id": null,
  "event_id": 356,
  "event.start": "2018-11-04T11:00:00.000Z",
  "event.end": "2018-11-04T15:00:00.000Z",
  "start": "2018-11-04T11:00:00.000Z",
  "end": "2018-11-04T15:00:00.000Z",
  "employee_id": 10,
  "IM_EventStatut": 4,
  "IM_EventStatutDescription": "FLEXI",
  "event_function.description": "hulpkelner(in) commis (bediening)",
  "event.name": "Pacific",
  "location": "Grote Markt 4, 3800 St Truiden",
  "UseDefault": "DFLT",
  "ExternalRefId": ""
}
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
