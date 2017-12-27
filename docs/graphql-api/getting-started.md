# Getting Started

In order to make API requests, you will need an active Refersion account.  You can start your free trial account [here](https://www.refersion.com/signup) or you can email [helpme@refersion.com](mailto:helmpe@refersion.com) for more details. 

## Base URL

All URLS referenced in the documentation have the following base:

<b>
```bash
https://graphql.refersion.com
```
</b>

## SSL/HTTPS

The Refersion GraphQL API is serveed over HTTPS.  To ensure data privacy, unencrypted HTTP is not supported.

## Authentication

In order to make calls to our API you need to include your API key along with the request.  You may obtain your API key from your [API Settings](https://www.refersion.com/settings) page while logged in.  *Note, if you are not logged in following this link will lead to a 404 error page.*

We look for your API Key in the `X-Refersion-Key` header.

```bash
$ curl "https://graphql.refersion.com"
  -H "X-Refersion-Key: [YOUR KEY]"
  -H 'Content-Type: application/graphql'
```

!!! Important
    It is very important to store your API key in a private and secure location. Sharing your API key is strictly prohibited.

## Quota & Usage

In order to keep our service running a high level of performance, every account has a limit of requests. If you exceed your allotted limits, a `429 Too Many Requests` error code will be returned and future requests may be throttled.

## Example Query

The query below also demonstrates how to used **GraphQL** fragments on *affiliate* to query for information specific to sub-type.  In this case, we request a list of affiliates along with the respective offer that they are assigned to.  

```scss
{
  affiliates(limit:2) {
    id
    email
    offer {
      commission
      type
    }
  }
}
```

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
 
