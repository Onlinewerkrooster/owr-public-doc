## Revenue API (v2)

The Revenue API is to query from or send revenue related data to the Onlinewerkrooster.be application. 

### Endpoint

https://services.onlinewerkrooster.be/api/revenue

## POST /daily

### Use cases

- Import daily revenue data into OWR
  - If data already exists in OWR, it will be overwritten. API can be used for both creation as update.

### Example Request

#### Header

| Name   | Required | Value                            | Remarks                                                      |
| ------ | -------- | -------------------------------- | ------------------------------------------------------------ |
| Apikey | Yes      | 3fdae2c8b32348a3855af9f0377191d4 | Unique ID to identify the source to query data. (provided by onlinewerkrooster.be team) |

#### Body

```json
{
	"date": "2020-02-06",
	"revenue": {
		"planned": {
			"net": 1000,
			"tax": 210
		},
		"actual": {
			"net": 1010,
			"tax": 400
		}
	},
	"hours": {
		"planned": 1,
		"actual": 2
	},
	"hoursExtra": {
		"planned": 10,
		"actual": 20
	},
	"employeeCosts": {
		"planned": {
			"net": 500,
			"tax": 10
		},
		"actual": {
			"net": 600,
			"tax": 10
		}
	},
	"employeeCostsExtra": {
		"planned": {
			"net": 200,
			"tax": 100
		},
		"actual": {
			"net": 500,
			"tax": 100
		}
	},
	"employeeCostsPercentage": {
		"effective": 2,
		"target": 2
	},
	"foodCosts": {
		"actual": {
			"net": 3,
			"tax": 1
		}
	},
	"otherCosts": {
		"actual": {
			"net":6,
			"tax": 2
		}
	},
	"totalCostsPercentage": {
		"effective": 2,
		"target": 2
	},
	"remarks": "a"
}
```
**Amount**

>  The amount can be defined in either net, and/or gross. Only 2 of the 3 values (net, tax, gross) are required since the 3rd value will be calculated.

```
{
 "net": 1000,
 "tax": 210,
 "gross": 1210
}
```

**Field descriptions**

| Field name                        | Type   | Required | Value      | Remarks                         |
| --------------------------------- | ------ | -------- | ---------- | ------------------------------- |
| date                              | Date   | Yes      | 2020-02-06 | Date related to the revenue     |
| revenue.planned                   | Amount | No       |            | Planned revenue                 |
| revenue.actual                    | Amount | No       |            | Actual revenue                  |
| hours.planned                     | Number | No       |            | Planned hours                   |
| hours.actual                      | Number | No       |            | Actual hours                    |
| hoursExtra.planned                | Number | No       |            | Planned extra hours             |
| hoursExtra.actual                 | Number | No       |            | Actual extra hours              |
| employeeCosts.planned             | Amount | No       |            | Planned employee costs          |
| employeeCosts.actual              | Amount | No       |            | Actual employee costs           |
| employeeCostsExtra.planned        | Amount | No       |            | Planned employee extra costs    |
| employeeCostsExtra.actual         | Amount | No       |            | Actual employee extra costs     |
| employeeCostsPercentage.effective | Number | No       |            | Effective cost percentage       |
| employeeCostsPercentage.target    | Number | No       |            | Taget cost percentage           |
| foodCosts.actual                  | Amount | No       |            | Actual foodcost                 |
| otherCosts.actual                 | Amount | No       |            | Actual other costs              |
| totalCostsPercentage.effective    | Number | No       |            | Effective total cost percentage |
| totalCostsPercentage.target       | Number | No       |            | Target total cost percentage    |
| remarks                           | String | No       |            | Free text with extra info       |

#### CURL

```
curl --request POST \
  --url https://owr-public-services-prod.herokuapp.com/api/revenue/daily \
  --header 'apikey: BFFB23A4-65ED-4036-9B23-C34EDA8686B0' \
  --header 'content-type: application/json' \
  --data '{
	"date": "2020-02-06",
	"revenue": {
		"planned": {
			"net": 1000,
			"tax": 210
		},
		"actual": {
			"net": 1010,
			"tax": 400
		}
	},
	"hours": {
		"planned": 1,
		"actual": 2
	},
	"hoursExtra": {
		"planned": 10,
		"actual": 20
	},
	"employeeCosts": {
		"planned": {
			"net": 500,
			"tax": 10
		},
		"actual": {
			"net": 600,
			"tax": 10
		}
	},
	"employeeCostsExtra": {
		"planned": {
			"net": 200,
			"tax": 100
		},
		"actual": {
			"net": 500,
			"tax": 100
		}
	},
	"employeeCostsPercentage": {
		"effective": 2,
		"target": 2
	},
	"foodCosts": {
		"actual": {
			"net": 3,
			"tax": 1
		}
	},
	"otherCosts": {
		"actual": {
			"net":6,
			"tax": 2
		}
	},
	"totalCostsPercentage": {
		"effective": 2,
		"target": 2
	},
	"remarks": "a"
}'
```



### Example Response (Success)

```json
[
  "revenue": {
      "planned": {
        "net": 1000,
        "tax": 210,
        "gross": 1210
      },
      "actual": {
        "net": 1010,
        "tax": 400,
        "gross": 1410
      }
    },
    "hours": {
      "planned": 1,
      "actual": 2
    },
    "hoursExtra": {
      "planned": 10,
      "actual": 20
    },
    "employeeCosts": {
      "planned": {
        "net": 500,
        "tax": 10,
        "gross": 510
      },
      "actual": {
        "net": 600,
        "tax": 10,
        "gross": 610
      }
    },
    "employeeCostsExtra": {
      "planned": {
        "net": 200,
        "tax": 100,
        "gross": 300
      },
      "actual": {
        "net": 500,
        "tax": 100,
        "gross": 600
      }
    },
    "employeeCostsPercentage": {
      "effective": 2,
      "target": 2
    },
    "foodCosts": {
      "actual": {
        "net": 6,
        "tax": 2,
        "gross": 8
      }
    },
    "otherCosts": {
      "actual": {
        "net": 6,
        "tax": 2,
        "gross": 8
      }
    },
    "totalCostsPercentage": {
      "effective": 2,
      "target": 2
    },
    "remarks": "a"
  }
]
```

### Example Response (Success)

If revenue is succesfully imported, you will receive `200 - OK`

### Example Response (Error)

It may happen something goes wrong due to various reasons, in the list below you can a list of errors.

In general, when you're sure you specified the correct values, you can always contact the onlinewerkrooster.be support (support@onlinewerkrooster.be)

| Error code                  | Error Message                                    | Explanation                                      | Solution          |
| --------------------------- | ------------------------------------------------ | ------------------------------------------------ | ----------------- |
| 409 - Conflict              | Error code.                                      | Functional error.                                | Check the values. |
| 404 - Not found             | No data found while data was expected.           | URL parameters do not match with data.           | Check the values. |
| 400 - Bad Request           | Invalid request due to wrong/missing parameters. | Invalid request due to wrong/missing parameters. | Check the values. |
| 401 - Bad Request           | Not authorized.                                  | Invalid ApiKey                                   | Check the values. |
| 500 - Internal Server Error | An unexpected (technical) error occurred.        |                                                  | Contact Support   |

[back to overview](README.md)