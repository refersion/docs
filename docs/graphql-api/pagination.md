# Pagination

Refersion GraphQL currently supports offset-based [pagination](http://graphql.org/learn/pagination/), which let’s you offset the start of each page by the number specified. 

Let’s say you’d like to pull a list of all your May 2018 conversions, and there are 800 results in total. In order to get all 800 results, you’d need to make a total of 4 requests (since each request returns a maximum of 200 results) using offsets. 

### First request:

Sample query: 
```json
{
    "query": "{ 
        conversions (created_from: 1525132800 created_to: 1527202238 first: 200) {
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

### Second request:

Sample query: 
```json
{
    "query": "{ 
        conversions (created_from: 1525132800 created_to: 1527202238 first: 200, offset: 200) {
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

Notice the offset command, which fetches you the next 200 results starting from record #201

### Third request:

Sample query: 
```json
{
    "query": "{ 
        conversions (created_from: 1525132800 created_to: 1527202238 first: 200, offset: 400) { 
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

This gets you records #401-600

### Fourth request:

Sample query: 
```json
{
    "query": "{ 
        conversions (created_from: 1525132800 first: 200, offset: 600) { 
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

This gets you records #601-800

Repeat the above for larger number of results until you get all the data returned. 

### Total Pagination Results

It is possible to select the total number of results that can be retrieved using a GraphQL query by adding a `pageInfo` section to your request.  This can be helpful for determining when you have requested all possible pages for a query.

Sample query: 
```json
{
    "query": "{ 
        conversions (created_from: 1525132800 first: 200, offset: 600) { 
            affiliate {
                name, 
                email
            }, 
            total, 
            commission_total, 
            currency, 
            created
        },
        pageInfo {
            total_results {
                conversions
            }
        }
    }"
}
```

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
            ...
        ],
        "pageInfo": {
            "total_results": {
                "conversions": 800
            }
        }
    }
}
```
