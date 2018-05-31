# Pagination

Refersion GraphQL currently supports offset-based [pagination](http://graphql.org/learn/pagination/), which let’s you offset the start of each page by the number specified. 

Let’s say you’d like to pull a list of all your May 2018 conversions, and there are 200 results in total. In order to get all 200 results, you’d need to make a total of 4 requests (since each request returns a maximum of 50 results) using offsets. 

### First request:
```json
{
    "query": "{ 
        conversions (created_from: 1525132800 created_to: 1527202238 first: 50) {
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
```json
{
    "query": "{ 
        conversions (created_from: 1525132800 created_to: 1527202238 first: 50, offset: 50) {
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

Notice the offset command, which fetches you the next 50 results starting from record #51

### Third request:
```json
{
    "query": "{ 
        conversions (created_from: 1525132800 created_to: 1527202238 first: 50, offset: 100) { 
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

This gets you records #101-150

### Fourth request:
```json
{
    "query": "{ 
        conversions (created_from: 1525132800 first: 50, offset: 150) { 
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

This gets you records #151-200

Repeat the above for larger number of results until you get all the data returned. 
