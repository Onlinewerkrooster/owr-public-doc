## Employee API

Employee API is intended to be able to retrieve employee info from the Onlinewerkrooster.be application. 

### Endpoint

https://services.onlinewerkrooster.be/api/employees

## GET /:id 

### Use cases

- Retrieve a list of employees
- Retrieve a single employee

### Example Request

#### Header

| Name   | Required | Value                            | Remarks                                                      |
| ------ | -------- | -------------------------------- | ------------------------------------------------------------ |
| Apikey | Yes      | 3fdae2c8b32348a3855af9f0377191d4 | Unique ID to identify the source to query data. (provided by onlinewerkrooster.be team) |

#### URL Parameters

Add the id to the end of the URL to retrieve the data for a single employee.

**https://owr-public-services-prod.herokuapp.com/api/employees/1** would retrieve the employee data for employee ID **1**

#### Body

N/A

#### CURL
```
curl --request GET \
  --url https://owr-public-services-prod.herokuapp.com/api/employees/ \
  --header 'apikey: 8689DB67-D12C-46A5-B4F9-74E70D1B37CF' \
  --header 'content-type: application/json'
```

### Example Response (Success)

```json
[
	{
		"id": 1,
		"nationalInsuranceNumber": "",
		"employeeNumber": "",
		"firstName": "admin",
		"lastName": "Onlinewerkrooster",
		"workspaces": [
			"Westpunt"
		],
		"function": "",
		"costPerHour": 0,
		"wagePerHour": 1,
		"hoursPerWeek": 40
	},
	{
		"id": 4,
		"nationalInsuranceNumber": "92.06.17-317.80",
		"employeeNumber": "314428",
		"firstName": "Michael",
		"lastName": "Van kessel",
		"workspaces": [
			"Westpunt"
		],
		"function": "",
		"costPerHour": 0,
		"wagePerHour": 1,
		"hoursPerWeek": 11.483333333333333
	}]
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

[back to overview](OnlineWerkroosterAPI.md)