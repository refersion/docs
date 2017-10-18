# Getting Started

You’ll need an active Refersion account to make API requests. Start your free trial or contact helpme@refersion.com.

## Base URL

All URLs referenced in the documentation have the following base:

`https://graphql.refersion.com`

## SSL/HTTPS

The Refersion GraphQL API is served over HTTPS. To ensure data privacy, unencrypted HTTP is not supported.

## Authentication

In order to make calls to our API you need to include your API key along with the request. You may obtain your API key from your [API Settings](https://www.refersion.com/settings) page while logged in.

We look for your API key in the Authentication header.

```bash
$ curl "https://graphql.refersion.com"
  -H "Authorization: Bearer [YOUR KEY]"
```

!!! info 
	It is very important to store your API key in a private and secure location. Sharing your API key is strictly prohibited.

## Quota & Usage

Each request will return your current usage in the response headers.

| Header  | Description  |
|---|---|
| X-Quota-Limit |  Your current request limit |
| X-Quota-Remaining  | Number of remainging requests in the current period  |
| X-Quota-Reset  | The unix timestamp (seconds, UTC) of the start of the next quota period.  |

## Example Query

The query below also demonstrates using GraphQL fragments on `affiliate` to query for information specific to a sub-type. In this case, we request a list of affiliates along with the respective offer that they are assigned to.

```
base {
  affiliates(limit: 2) {
    id
    email
    offer {
      commission
      type
    }
  }
}
```

!!! note "Query type must be "base""
	Please make sure to start every query with the "base" query type as seen above. Currenty this is the only supported query type.

This response returns: 

```json
{
    "data": {
        "affiliates": [
            {
                "id": 444,
                "email": "jane.verde@aol.com",
                "offer": {
                    "commission": 10,
                    "type": "FLAT_RATE"
                }
            },
            {
                "id": 419,
                "email": "mike.rogers@hotmail.com",
                "offer": {
                    "commission": 10,
                    "type": "FLAT_RATE"
                }
            }
        ]
    }
}
```