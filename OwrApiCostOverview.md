## CostOverview API

CostOverview API is intended to be able to retrieve cost overview info from the Onlinewerkrooster.be application. 

"Date from" & "Date To" are required parameters to limit the results.

### Endpoint

https://owr-public-services-prod.herokuapp.com/api/cost-overview?

### Use cases

- Retrieve cost overview data for a certain period.

### Example Request

#### Header

| Name         | Required | Value                            | Remarks                                                      |
| ------------ | -------- | -------------------------------- | ------------------------------------------------------------ |
| Apikey       | Yes      | 3fdae2c8b32348a3855af9f0377191d4 | Unique ID to identify the source to query data. (provided by onlinewerkrooster.be team) |
| content-type | Yes      | application/json                 | JSON data                                                    |

#### URL Parameters

| Field name | Type                 | Required | Value                  | Remarks                   |
| ---------- | -------------------- | -------- | ---------------------- | ------------------------- |
| dateFrom   | Timestamp (ISO 8601) | Yes      | 2018-03-15T13:46:50.52 | Start Date/Time of period |
| dateTo     | Timestamp (ISO 8601) | Yes      | 2018-03-15T14:46:50.52 | End Date/Time of period   |
| page       | number               | No       | 0                      |                           |
| limit      | number               | No       | 10                     |                           |

*Page & limit* are parameters which can be used to paginate the fetched data when a large set of data is expected.

```
https://owr-public-services-prod.herokuapp.com/api/cost-overview?dateFrom=2019-09-01&dateTo=2019-09-30%2023%3A59%3A59%2B0200
```

#### Body

N/A

#### CURL
```
curl --request GET \
  --url 'https://owr-public-services-prod.herokuapp.com/api/cost-overview?dateFrom=2019-09-01&dateTo=2019-09-30%2023%3A59%3A59%2B0200' \
  --header 'apikey: 5E23FA88-11E6-4427-8E8A-A664EEDAF8FD'
```

### Example Response (Success)

```
[
  {
    "TransDatetime": "2019-09-14T22:00:00.000Z",
    "HoursWorked": 1,
    "CostAmount": 10,
    "Workspace": {
      "name": "BRUSSEL",
      "externalNumber": "BXL"
    }
  },
  {
    "TransDatetime": "2019-09-15T22:00:00.000Z",
    "HoursWorked": 2,
    "CostAmount": 60,
    "Workspace": {
      "name": "BRUSSEL",
      "externalNumber": "BXL"
    }
  },
  {
    "TransDatetime": "2019-09-16T22:00:00.000Z",
    "HoursWorked": 1,
    "CostAmount": 15,
    "Workspace": {
      "name": "ANTWERPEN",
      "externalNumber": "ANT"
    }
  }
]
```



### Example Response (Error)

It may happen something goes wrong while querying cost overview data due to various reasons, in the list below you can a list of errors.

In general, when you're sure you specified the correct values, you can always contact the onlinewerkrooster.be support (support@onlinewerkrooster.be)

| Error code                  | Error Message                    | Explanation                                                  | Solution          |
| --------------------------- | -------------------------------- | ------------------------------------------------------------ | ----------------- |
| 401 - Unauthorized          | Unauthorized.                    | An invalid apikey is used.                                   | Check the values. |
| 400 - Bad Request           | Bad request                      | At least one of the query parameters is from a wrong type, or a required parameter is missing. | Check the values. |
| 500 - Internal Server Error | An unexpected error has occured. |                                                              | Contact Support   |

[back to overview](README.md)