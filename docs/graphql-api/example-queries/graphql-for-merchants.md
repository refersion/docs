# GraphQL for Merchants


#### Get a list of your conversions from May 2018

Request:
```json
{
  "query": "{ 
      conversions (created_from: 1525132800 created_to: 1527202238) { 
          affiliate {
              name, 
              email
          }, 
          total, 
          commission_total, 
          currency, 
          created
      }
  }"
}
```
_Note_: timestamp is in Unix time

<br />

Sample response:
```json
{
    "data": {
        "conversions": [
            {
                "affiliate": {
                    "name": "ABC",
                    "email": "abc@refersion.com"
                },
                "total": "24.00",
                "commission_total": "4.80",
                "currency": "USD",
                "created": "1526674258"
            },
            {
                "affiliate": {
                    "name": "DEF",
                    "email": "def@refersion.com"
                },
                "total": "630.00",
                "commission_total": "346.50",
                "currency": "CAD",
                "created": "1526671881"
            }
        ]
    }
}
```

<br />

#### Get a list of affiliates and their referral parameters

Query: 
```json
{
  "query": "{ 
      affiliates {
          status, 
          name, 
          email, 
          rfsn_parameter
      }
  }"
}
```


Sample response:
```json
{
    "data": {
        "affiliates": [
            {
                "status": "ACTIVE",
                "name": "Affiliate A",
                "email": "affiliate@refersion.com",
                "rfsn_parameter": "&rfsn=123456.1234c"
            },
            {
                "status": "ACTIVE",
                "name": "Influencer B",
                "email": "influencer@refersion.com",
                "rfsn_parameter": "&rfsn=123456.238e5"
            }
        ]
    }
}
```

