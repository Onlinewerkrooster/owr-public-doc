## BCMatic Revenue API

BCMatic Revenue API is intended to push revenue data from BCMATIC (= cash desk) to the Onlinewerkrooster.be application. 

### Endpoint

https://www.onlinewerkrooster.be/APIOWR/api/Revenue/BCMaticRevenue

### Use cases

- Push revenue data from BCMatic

### Example Request

#### Header

| Name         | Required | Value                                | Remarks                                                      |
| ------------ | -------- | ------------------------------------ | ------------------------------------------------------------ |
| apikey       | Yes      | 3fdae2c8b32348a3855af9f0377191d4     | Unique ID to identify the requester (provided by onlinewerkrooster.be team) |
| content-type | Yes      | application/json                     | JSON data                                                    |
| userId       | Yes      | 2982D3B5-4059-4D75-8BF7-E8A4296B98A6 | Unique ID to identify the the user who's using the API. (provided by the onlinewerkrooster.be team) |

#### Body

{"TargetDate":"2018-03-03T02:26:38.000Z","TargetTime":1520043998,"BusinessDate":"2018-03-19T00:00:00.000Z","POSID":"DLIGHT","POSName":"KASSA","Reports":{"Turnover":{"turnover":3476.17,"tax":730},"Hourly":[{"time":"2018-03-19T00:00:00.000Z","turnover":186.83,"tax":39.24},{"time":"2018-03-19T01:00:00.000Z","turnover":141.45,"tax":29.71},{"time":"2018-03-19T02:00:00.000Z","turnover":153.61,"tax":32.26},{"time":"2018-03-19T03:00:00.000Z","turnover":77.17,"tax":16.2},{"time":"2018-03-19T04:00:00.000Z","turnover":80.43,"tax":16.89},{"time":"2018-03-19T05:00:00.000Z","turnover":205.07,"tax":43.07},{"time":"2018-03-19T06:00:00.000Z","turnover":4.52,"tax":0.95},{"time":"2018-03-19T07:00:00.000Z","turnover":201.38,"tax":42.29},{"time":"2018-03-19T08:00:00.000Z","turnover":215.56,"tax":45.27},{"time":"2018-03-19T09:00:00.000Z","turnover":187.76,"tax":39.43},{"time":"2018-03-19T10:00:00.000Z","turnover":12.78,"tax":2.68},{"time":"2018-03-19T11:00:00.000Z","turnover":109.98,"tax":23.1},{"time":"2018-03-19T12:00:00.000Z","turnover":228.25,"tax":47.93},{"time":"2018-03-19T13:00:00.000Z","turnover":209.23,"tax":43.94},{"time":"2018-03-19T14:00:00.000Z","turnover":99.31,"tax":20.85},{"time":"2018-03-19T15:00:00.000Z","turnover":254.44,"tax":53.43},{"time":"2018-03-19T16:00:00.000Z","turnover":230.57,"tax":48.42},{"time":"2018-03-19T17:00:00.000Z","turnover":15.65,"tax":3.29},{"time":"2018-03-19T18:00:00.000Z","turnover":251.17,"tax":52.74},{"time":"2018-03-19T19:00:00.000Z","turnover":96.79,"tax":20.33},{"time":"2018-03-19T20:00:00.000Z","turnover":139.2,"tax":29.23},{"time":"2018-03-19T21:00:00.000Z","turnover":203.07,"tax":42.64},{"time":"2018-03-19T22:00:00.000Z","turnover":14.93,"tax":3.13},{"time":"2018-03-19T23:00:00.000Z","turnover":157.02,"tax":32.98}],"Departments":[]}}

| Field name    | Type                 | Required | Value                    | Remarks                                     |
| ------------- | -------------------- | -------- | ------------------------ | ------------------------------------------- |
| TargetDate    | Timestamp (ISO 8601) | Yes      | 2018-04-09T08:23:10.742Z | (not used in OWR)                           |
| TargetTime    | Numeric              | Yes      | 1520043998               | (not used in OWR)                           |
| BusinessDate  | Timestamp (ISO 8601) | Yes      | 2018-04-09T08:23:10.742Z | Date/Time of revenue info (not used in OWR) |
| POSID         | String               | Yes      | DLIGHT                   | (not used in OWR)                           |
| POSTYPE       | String               | Yes      | KASSA                    | (not used in OWR)                           |
| Reports       |                      |          |                          | group element                               |
| --Turnover    |                      |          |                          | group element                               |
| ---turnover   | Numeric              | Yes      |                          | Revenue amount (incl tax)                   |
| ---tax        | Numeric              | Yes      |                          | Tax amount (not used in OWR)                |
| --Hourly      |                      |          |                          | group element                               |
| ---time       | Timestamp (ISO 8601) | Yes      | 2018-04-09T08:23:10.742Z | Date/Time of the revenue object             |
| ---turnover   | Numeric              | Yes      |                          | Revenue amount (incl tax)                   |
| ---tax        | Numeric              | Yes      |                          | Tax amount (not used in OWR)                |
| --Departments |                      | Yes      |                          | group element                               |

#### CURL

curl --request POST \
  --url https://www.onlinewerkrooster.be/APIOWR/api/Revenue/BCMaticRevenue \
  --header 'apikey: 3fdae2c8b32348a3855af9f0377191d4' \
  --header 'content-type: application/json' \
  --header 'userid: 2982D3B5-4059-4D75-8BF7-E8A4296B98A6' \
  --data '{"TargetDate":"2018-03-03T02:26:38.000Z","TargetTime":1520043998,"BusinessDate":"2018-03-19T00:00:00.000Z","POSID":"DLIGHT","POSName":"KASSA","Reports":{"Turnover":{"turnover":3476.17,"tax":730},"Hourly":[{"time":"2018-03-19T00:00:00.000Z","turnover":186.83,"tax":39.24},{"time":"2018-03-19T01:00:00.000Z","turnover":141.45,"tax":29.71},{"time":"2018-03-19T02:00:00.000Z","turnover":153.61,"tax":32.26},{"time":"2018-03-19T03:00:00.000Z","turnover":77.17,"tax":16.2},{"time":"2018-03-19T04:00:00.000Z","turnover":80.43,"tax":16.89},{"time":"2018-03-19T05:00:00.000Z","turnover":205.07,"tax":43.07},{"time":"2018-03-19T06:00:00.000Z","turnover":4.52,"tax":0.95},{"time":"2018-03-19T07:00:00.000Z","turnover":201.38,"tax":42.29},{"time":"2018-03-19T08:00:00.000Z","turnover":215.56,"tax":45.27},{"time":"2018-03-19T09:00:00.000Z","turnover":187.76,"tax":39.43},{"time":"2018-03-19T10:00:00.000Z","turnover":12.78,"tax":2.68},{"time":"2018-03-19T11:00:00.000Z","turnover":109.98,"tax":23.1},{"time":"2018-03-19T12:00:00.000Z","turnover":228.25,"tax":47.93},{"time":"2018-03-19T13:00:00.000Z","turnover":209.23,"tax":43.94},{"time":"2018-03-19T14:00:00.000Z","turnover":99.31,"tax":20.85},{"time":"2018-03-19T15:00:00.000Z","turnover":254.44,"tax":53.43},{"time":"2018-03-19T16:00:00.000Z","turnover":230.57,"tax":48.42},{"time":"2018-03-19T17:00:00.000Z","turnover":15.65,"tax":3.29},{"time":"2018-03-19T18:00:00.000Z","turnover":251.17,"tax":52.74},{"time":"2018-03-19T19:00:00.000Z","turnover":96.79,"tax":20.33},{"time":"2018-03-19T20:00:00.000Z","turnover":139.2,"tax":29.23},{"time":"2018-03-19T21:00:00.000Z","turnover":203.07,"tax":42.64},{"time":"2018-03-19T22:00:00.000Z","turnover":14.93,"tax":3.13},{"time":"2018-03-19T23:00:00.000Z","turnover":157.02,"tax":32.98}],"Departments":[]}}'

### Example Response (Success)

Response code "200 - OK".

(No response message body)

### Example Response (Error)

It may happen something goes wrong while registering the revenue data due to various reasons, in the list below you can a list of errors.

In general, when you're sure you specified the correct values, you can always contact the onlinewerkrooster.be support (support@onlinewerkrooster.be)

| Error code                  | Error Message                                                | Explanation                                     | Solution          |
| --------------------------- | ------------------------------------------------------------ | ----------------------------------------------- | ----------------- |
| 500 - Internal Server Error | No Environment                                               | The combination "ApiKey" & "UserId" is invalid. | Check the values. |
| 500 - Internal Server Error | Guid should contain 32 digits with 4 dashes (xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx). | Invalid UserId                                  | Check the values. |
| 400 - Bad Request           | No connection could be made with the supplied credentials.   | At least one of the headers is missing          |                   |

[back to overview](OnlineWerkroosterAPI.md)