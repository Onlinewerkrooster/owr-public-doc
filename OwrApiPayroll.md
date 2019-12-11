# Payroll API

**Payroll** API (formerly known as WorktimeExportData) is intended to be able to export worktime data from the Onlinewerkrooster.be application. 

"Date from" & "Date To" are required parameters to limit the results.

### Endpoint

https://owr-public-services-prod.herokuapp.com/api/payroll?

### Use cases

- Retrieve payroll data for a certain period. (and optional other parameters)

### Example Request

#### Header

| Name         | Required | Value                            | Remarks                                                      |
| ------------ | -------- | -------------------------------- | ------------------------------------------------------------ |
| Apikey       | Yes      | 3fdae2c8b32348a3855af9f0377191d4 | Unique ID to identify the source to query data. (provided by onlinewerkrooster.be team) |
| content-type | Yes      | application/json                 | JSON data                                                    |

#### URL Parameters

| Field name     | Type                 | Required | Value                  | Remarks                    |
| -------------- | -------------------- | -------- | ---------------------- | -------------------------- |
| dateFrom       | Timestamp (ISO 8601) | Yes      | 2018-03-15T13:46:50.52 | Start Date/Time of period  |
| dateTo         | Timestamp (ISO 8601) | Yes      | 2018-03-15T14:46:50.52 | End Date/Time of period    |
| employeeNumber | string               | No       | 10004                  |                            |
| inss           | String               | No       | 87.08.20 209-07        | National Identifier (INSZ) |

```
https://owr-public-services-prod.herokuapp.com/api/payroll?dateFrom=2019-06-01T00%3A00%3A00&dateTo=2019-06-30T23%3A59%3A59
```

#### Body

N/A

#### CURL

```
curl --request GET \
  --url 'https://owr-public-services-prod.herokuapp.com/api/payroll?dateFrom=2019-06-01T00%3A00%3A00&dateTo=2019-06-30T23%3A59%3A59' \
  --header 'apikey: C2903CDE-D440-4327-B20B-41CF6820F3C9'
```

### Example Response (Success)

```
[
  {
    "employeeNumber": "4",
    "inss": "87082020907",
    "date": "2019-06-03",
    "amount": 8.25,
    "wageCode": "1101"
  },
  {
    "employeeNumber": "4",
    "inss": "87082020907",
    "date": "2019-06-04",
    "amount": 10.066666666666666,
    "wageCode": "1101"
  },
```



### Example Response (Error)

It may happen something goes wrong while retrieving payroll data due to various reasons, in the list below you can a list of errors.

In general, when you're sure you specified the correct values, you can always contact the onlinewerkrooster.be support (support@onlinewerkrooster.be)

| Error code                  | Error Message                   | Explanation                 | Solution          |
| --------------------------- | ------------------------------- | --------------------------- | ----------------- |
| 401 - Unauthorized          | Unauthorized                    | Invalid (or missing apikey) | Check the values. |
| 400 - Bad Request           | One or more validations failed. | Invalid query parameters    | Check the values. |
| 500 - Internal server error | Internal Server Error           | Unexpected technical error. | Contact Support   |

# Worktime Export Data (Deprecated)

### Endpoint

https://www.onlinewerkrooster.be/APIOWR/api/WorktimeExport/GetWorktimeExportData?dateFrom=2018-01-01&dateTo=2018-05-30

### Use cases

- Retrieve worktime export data for a certain period. (and optional other parameters)

### Example Request

#### Header

| Name         | Required | Value                                | Remarks                                                      |
| ------------ | -------- | ------------------------------------ | ------------------------------------------------------------ |
| Apikey       | Yes      | 3fdae2c8b32348a3855af9f0377191d4     | Unique ID to identify the source to query data. (provided by onlinewerkrooster.be team) |
| content-type | Yes      | application/json                     | JSON data                                                    |
| UserId       | Yes      | 81ad2f9b-6362-4388-9617-96a18524850c | Unique ID to identify the requester. (provided by the onlinewerkrooster.be team) |

#### URL Parameters

| Field name           | Type                 | Required | Value                  | Remarks                    |
| -------------------- | -------------------- | -------- | ---------------------- | -------------------------- |
| dateFrom             | Timestamp (ISO 8601) | Yes      | 2018-03-15T13:46:50.52 | Start Date/Time of period  |
| dateTo               | Timestamp (ISO 8601) | Yes      | 2018-03-15T14:46:50.52 | End Date/Time of period    |
| companyId            | int                  | No       | 1                      |                            |
| emplIdSocialSecurity | String               | No       | 10004                  | Employee Number            |
| SSN                  | String               | No       | 87.08.20 209-07        | National Identifier (INSZ) |

```
https://www.onlinewerkrooster.be/APIOWR/api/WorktimeExport/GetWorktimeExportData?dateFrom=2018-01-01&dateTo=2018-05-30&companyId=1&emplIdSocialSecurity=1004&ssn=87.08.20 209.07
```

#### Body

N/A

#### CURL
```
curl --request GET \
  --url 'https://www.onlinewerkrooster.be/APIOWR/api/WorktimeExport/GetWorktimeExportData?ssn=87.08.20%20209.07&emplIdSocialSecurity=1004&companyId=1&dateTo=2018-05-30&dateFrom=2018-01-01' \
  --header 'apikey: 3EC0D1A4-21BC-46E9-8318-FC0B4A2A6E71' \
  --header 'content-type: application/json' \
  --header 'userid: 89CFD64D-C63B-48CE-8C0B-FB163097C2BH'
```

### Example Response (Success)

```
[
	{
		"EmplIdSocialSecurity": "1004",
		"INSZ": "87-08-20 209-07",
		"Date": "2018-03-03T00:00:00",
		"NumberOfHours": 8.0,
		"WageCode": "0001"
	},
	{
		"EmplIdSocialSecurity": "1004",
		"INSZ": "87-08-20 209-07",
		"Date": "2018-03-04T00:00:00",
		"NumberOfHours": 3.0,
		"WageCode": "0001"
	}
]
```



### Example Response (Error)

It may happen something goes wrong while exporting worktime data due to various reasons, in the list below you can a list of errors.

In general, when you're sure you specified the correct values, you can always contact the onlinewerkrooster.be support (support@onlinewerkrooster.be)

| Error code                  | Error Message                                                | Explanation                                     | Solution          |
| --------------------------- | ------------------------------------------------------------ | ----------------------------------------------- | ----------------- |
| 500 - Internal Server Error | Unauthorized: Invalid ApiKey/UserId!                         | The combination "ApiKey" & "UserId" is invalid. | Check the values. |
| 400 - Bad Request           | Header ApiKey is required!          .                        | Required field.                                 | Check the values. |
| 400 - Bad Request           | Header ApiKey is required!                                   | Required field.                                 | Check the values. |
| 400 - Bad Request           | Incomplete request: DateFrom empty                           | Required field.                                 | Check the values. |
| 400 - Bad Request           | Incomplete request: DateTo empty                             | Required field.                                 | Check the values. |
| 400 - Bad Request           | The supplied ssn was not linked to an employee               | Unknown INSZ.                                   | Check the values. |
| 400 - Bad Request           | No corresponding records were found.                         | No results for given parameters.                | Check the values. |
| 400 - Bad Request           | An error occurred while executing the command definition. See the inner exception for details. |                                                 | Contact Support   |

[back to overview](README.md)

