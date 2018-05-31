# GraphQL for Marketplace Users

#### Get a list of all your merchants and referral parameters
```json
{
    "query": "{ 
        affiliates {
            shop {
                name, 
                url
            }, 
            id, 
            status, 
            rfsn_parameter
        } 
    }"
}
```

<br />

Sample response
```json
{
    "data": {
        "affiliates": [
            {
                "shop": {
                    "name": "refersion-demo",
                    "url": "http://refersion-demo.refersion.com"
                },
                "id": 123456,
                "status": "ACTIVE",
                "rfsn_parameter": "&rfsn=1111110.c4845"
            },
            {
                "shop": {
                    "name": "refersion-test",
                    "url": "http://refersion-test.refersion.com"
                },
                "id": 234578,
                "status": "ACTIVE",
                "rfsn_parameter": "&rfsn=111111.1111a"
            }
        ]
    }
}
```

<br />

#### Get a list of your conversions and payment status in May 2018
```json
{
    "query": "{ 
        conversions (created_from: 1525132800 created_to: 1527202238) { 
            total, 
            commission_total, 
            currency, 
            created, 
            shop {name}, 
            payment {created}
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
                "total": "24.00",
                "commission_total": "4.80",
                "currency": "USD",
                "created": "1526674258",
                "shop": {
                    "name": "refersion-test"
                },
                "payment": {
                    "created": "1527027021"
                }
            },
            {
                "total": "0.00",
                "commission_total": "1.00",
                "currency": "USD",
                "created": "1525717323",
                "shop": {
                    "name": "refersion-test"
                },
                "payment": null
            }
        ]
    }
}
```

<br />

#### Get a list of all payments you received in May 2018
```json
{
    "query": "{ 
        payments (created_from:1525132800 created_to: 1527202238) { 
            id, 
            created, 
            commission_total, 
            total_conversions, 
            shop {name} 
        }
    }"
}
```

<br />

Sample response
```json
{
    "data": {
        "payments": [
            {
                "id": 13453,
                "created": "1527193893",
                "commission_total": "9.40",
                "currency": "USD",
                "total_conversions": 6,
                "shop": {
                    "name": "refersion-test"
                }
            },
            {
                "id": 43543,
                "created": "1527106481",
                "commission_total": "34.00",
                "currency": "CAD",
                "total_conversions": 1,
                "shop": {
                    "name": "refersion-test"
                }
            },
            {
                "id": 46843,
                "created": "1527106481",
                "commission_total": "122.00",
                "currency": "GBP",
                "total_conversions": 1,
                "shop": {
                    "name": "refersion-test"
                }
            }
        ]
    }
}
```

