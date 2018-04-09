## ETC Timeclock API

ETC Timeclock API is intended to push time clock data from an external system (ETC) to the Onlinewerkrooster.be application. 

The value of "checkIn" or "checkOut" is used to register time clock data, so you register time clock data in the past (or future). This can result in a late declaration in Dimona (if enabled) !!!

### Endpoint

https://www.onlinewerkrooster.be/APIOWR/api/Clock/ETCClock

### Use cases

- Register the start of the working day
  - NationalId, UserKey and CheckIn are specified
  - CheckOut is not specified
- Register the end of the working day
  - NationalId, UserKey and CheckOut are specified
  - CheckIn can be specified, but is not required

### Example Request

#### Header

| Name         | Required | Value                            | Remarks                                                      |
| ------------ | -------- | -------------------------------- | ------------------------------------------------------------ |
| apikey       | Yes      | 3fdae2c8b32348a3855af9f0377191d4 | Unique ID to identify the requester (provided by onlinewerkrooster.be team) |
| content-type | Yes      | application/json                 | JSON data                                                    |
| CustomerKey  | Yes      | N/A                              | Currently not used (but required)                            |

#### Body

{
  "NationalId": "87.08.20-209.07",
  "UserKey": "2982D3B5-4059-4D75-8BF7-E8A4296B98C7",
  "CheckIn": "2018-03-15T13:46:50.523",
  "CheckOut": "2018-03-15T15:46:50.523"
}

| Field name | Type                 | Required      | Value                                | Remarks                                                      |
| ---------- | -------------------- | ------------- | ------------------------------------ | ------------------------------------------------------------ |
| NationalId | String               | Yes           | 87.08.20-209.07                      | National Registration Number of the employee to register time clock data. <br /><br />(dashes(-), points(.) or whitespaces are filtered out) |
| UserKey    | String (Guid)        | Yes           | 1982D3B5-4059-4D75-8BF7-E8A4296B98C7 | Unique ID to identify the the user who's using the API. (provided by the onlinewerkooster.be team) |
| CheckIn    | Timestamp (ISO 8601) | Conditionally | 2018-03-15T13:46:50.52               | Date/Time to register the start of the working day           |
| CheckOut   | Timestamp (ISO 8601) | Conditionally | 2018-03-15T14:46:50.52               | Date/Time to register the end of the working day             |

#### CURL

curl --request POST \
  --url https://www.onlinewerkrooster.be/APIOWR/api/Clock/ETCClock \
  --header 'apikey: 3fdae2c8b32348a3855af9f0377191d4' \
  --header 'content-type: application/json' \
  --header 'customerkey: N/A' \
  --data '{
  "NationalId": "87.08.20-209.07",
  "UserKey": "2982D3B5-4059-4D75-8BF7-E8A4296B98C7",
  "CheckIn": "2018-03-15T13:46:50.523",
  "CheckOut": "2018-03-15T15:46:50.523"
}'

### Example Response (Success)

"Request successfully completed."

### Example Response (Error)

It may happen something goes wrong while registering the time clock data due to various reasons, in the list below you can a list of errors.

In general, when you're sure you specified the correct values, you can always contact the onlinewerkrooster.be support (support@onlinewerkrooster.be)

| Error code                  | Error Message                                                | Explanation                                                  | Solution                                                     |
| --------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 500 - Internal Server Error | No Environment                                               | The combination "ApiKey" & "UserId" is invalid.              | Check the values.                                            |
| 400 - Bad Request           | No employee found for the given INSS                         | NationalId is not known in the onlinewerkrooster application. | Check the values.                                            |
| 400 - Bad Request           | Incomplete request: NationalId empty.                        | Required field.                                              | Check the values.                                            |
| 400 - Bad Request           | Incomplete request: UserKey empty.                           | Required field.                                              | Check the values.                                            |
| 400 - Bad Request           | Invalid UserKey: (32 digits with 4 dashes (xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx)) | Invalid format of user key                                   | Check the values.                                            |
| 400 - Bad Request           | Incomplete request: CheckIn and/or CheckOut empty.           | Required field.                                              | Check the values.                                            |
| 400 - Bad Request           | Invalid headers: at least 1 of the keys is missing.          | Required field.                                              | Check the values.                                            |
| 400 - Bad Request           | The specified type does not exist.                           | Technical validation, should never occur.                    | Contact Support                                              |
| 400 - Bad Request           | The specified Timestamp could not be parsed.                 | Invalid date/time. <br /><br />Correct date format: <br /> yyyy-mm-ddThh:mm:ss[.mmm] | Check date format                                            |
| 400 - Bad Request           | Employee hasn't clocked in yet.                              | Employee is not clocked in, clocking out does not make sense. | Check national registration number, and if employee is clocked in. |
| 400 - Bad Request           | An unexpected error happened with the parameters, please log a support ticket containing the sent request |                                                              | Contact support                                              |
