## ClockTimeSpecified API

ClockTimeSpecified API is intended to push time clock data from to the Onlinewerkrooster.be application. 

The API works the same as the [ClockTime API](OwrApiClockTime.md) with the difference that this API uses the timestamp of the request message and NOT the current date/time.

### Endpoint

https://www.onlinewerkrooster.be/APIOWR/api/Clock/ClockTimeSpecified

### Use cases

- Register the start of the working day
- Register the start of a break
- Register the end of a break
- Register the end of the working day

### Example Request

#### Header

| Name         | Required | Value                            | Remarks                                                      |
| ------------ | -------- | -------------------------------- | ------------------------------------------------------------ |
| apikey       | Yes      | 3fdae2c8b32348a3855af9f0377191d4 | Unique ID to identify the requester (provided by onlinewerkrooster.be team) |
| content-type | Yes      | application/json                 | JSON data                                                    |

#### Body
```
{
  "UserId": "2982D3B5-4059-4D75-8BF7-E8A4296B98A7",
  "INSS": "870820-20907",
  "ApiKey": "3fdae2c8b32348a3855af9f0377191d4",
 "Timestamp": "2018-04-09T10:30",
  "Type": "ClockIn"
}
```

| Field name | Type                 | Required | Value                                | Remarks                                                      |
| ---------- | -------------------- | -------- | ------------------------------------ | ------------------------------------------------------------ |
| UserId     | String (Guid)        | Yes      | 1982D3B5-4059-4D75-8BF7-E8A4296B98C7 | Unique ID to identify the the user who's using the API. (provided by the onlinewerkrooster.be team) |
| INSS       | String               | Yes      | 87.08.20-209.07                      | National Registration Number of the employee to register time clock data. <br /><br />(dashes(-), points(.) or whitespaces are filtered out) |
| ApiKey     | String               | Yes      | 3fdae2c8b32348a3855af9f0377191d4     | Unique ID to identify the requester                          |
| Timestamp  | Timestamp (ISO 8601) | Yes      | 2018-03-15T13:46:50.52F              | Date/time to register                                        |
| Type       | String               | Required | ClockIn                              | Depending on the action needed, one of the values below should be used:<br />- ClockIn<br />- ClockOut<br />- BreakIn<br />- BreakOut |

#### CURL
```
curl --request POST \
  --url https://www.onlinewerkrooster.be/APIOWR/api/Clock/ClockTimeSpecified \
  --header 'apikey: 3fdae2c8b32348a3855af9f0377191d4' \
  --header 'content-type: application/json' \
  --data '{
  "UserId": "2982D3B5-4059-4D75-8BF7-E8A4296B98A7",
  "INSS": "870820-20907",
  "ApiKey": "3fdae2c8b32348a3855af9f0377191d4",
 "Timestamp": "2018-04-09T10:30",
  "Type": "ClockIn"
}'
```

### Example Response (Success)

| Message                         | Explanation                                |
| ------------------------------- | ------------------------------------------ |
| ClockIn succesfully completed.  | Start of working day correctly registered. |
| BreakIn succesfully completed.  | Start of break correctly registered.       |
| BreakOut succesfully completed. | End of break correctly registered.         |
| ClockOut succesfully completed. | End of working day correctly registered.   |

### Example Response (Error)

It may happen something goes wrong while registering the time clock data due to various reasons, in the list below you can a list of errors.

In general, when you're sure you specified the correct values, you can always contact the onlinewerkrooster.be support (support@onlinewerkrooster.be)

| Error code                  | Error Message                                                | Explanation                                                  | Solution                                                     |
| --------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 500 - Internal Server Error | No Environment                                               | The combination "ApiKey" & "UserId" is invalid.              | Check the values.                                            |
| 400 - Bad Request           | No employee found for the given INSS                         | NationalId is not known in the onlinewerkrooster application. | Check the values.                                            |
| 400 - Bad Request           | The specified type does not exist.                           | Technical validation, should never occur.                    | Contact Support                                              |
| 400 - Bad Request           | The specified Timestamp could not be parsed.                 | Invalid date/time. <br /><br />Correct date format: <br /> yyyy-mm-ddThh:mm:ss[.mmm] | Check date format                                            |
| 400 - Bad Request           | Employee hasn't clocked in yet.                              | Employee is not clocked in, clocking out does not make sense. | Check national registration number, and if employee is clocked in. |
| 400 - Bad Request           | An unexpected error happened with the parameters, please log a support ticket containing the sent request |                                                              | Contact support                                              |

[back to overview](OnlineWerkroosterAPI.md)