# Customers API

Customers API is intended to be able to retrieve and create customer info from the Onlinewerkrooster.be application.  A list of error codes is documented below in this document.

## Endpoint

https://owr-public-services-prod.herokuapp.com/api/customers

## POST api/customers

### Example Request

#### Header

| Name         | Required | Value                                | Remarks                                                      |
| ------------ | -------- | ------------------------------------ | ------------------------------------------------------------ |
| apikey       | Yes      | 3fdae2c8b32348a3855af9f0377191d4     | Unique ID to identify the requester (provided by onlinewerkrooster.be team) |
| content-type | Yes      | application/json                     | JSON data                                                    |

#### Body

```
{
 "extCustomerId": 1001,
 "extCustomerNumber": "1001",
 "enterpriseNumber": "BE01234567899",
 "name": "OWR.GG.1001",
 "address": {
   "street": "Louis Pasteurstraat",
   "streetNumber": "15B",
   "city": "Lommel",
   "postalCode": "3920",
        "country": "belgium"
 }
}
```

| Field name           | Type    | Required | Value                | Remarks                                                      |
| -------------------- | ------- | -------- | -------------------- | ------------------------------------------------------------ |
| extCustomerId        | Numeric | Yes      | 100001               | Numeric (unique) identifier of customer in the 3rd party system. |
| extCustomerNumber    | String  | Yes      | 100001               | Alphanumeric (unique) identifier of customer in the 3rd party system. |
| name                 | String  | Yes      | OWR.TESTEVENT.100001 | Name of customer                                             |
| enterpriseNumber     | String  | Yes      | BE0123456789         | VAT Number                                                   |
| address.street       | String  | No       |                      |                                                              |
| address.streetNumber | String  | No       |                      |                                                              |
| address.city         | String  | Yes      |                      |                                                              |
| address.postalCode   | String  | No       |                      |                                                              |
| address.country      | String  | Yes      |                      |                                                              |

#### CURL

```
curl --request POST \
  --url https://owr-public-services-dev.herokuapp.com/api/customers/ \
  --header 'apikey: 4C6086B2-4201-4CD6-A94A-BB89684FD0BD' \
  --header 'content-type: application/json' \
  --data '{
 "extCustomerId": 1001,
 "extCustomerNumber": "1001",
 "enterpriseNumber": "BE01234567899",
 "name": "OWR.GG.1001",
 "address": {
   "street": "Louis Pasteurstraat",
   "streetNumber": "15B",
   "city": "Lommel",
   "postalCode": "3920",
        "country": "belgium"
 }
}	
```

### Example Response (Success)

```json
{
	"companyId": 2,
	"customerId": 10,
	"extCustomerId": 1001
}
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

[back to overview](README.md)
