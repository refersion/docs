# Welcome to Refersion

Thank you for being a part of the Refersion developer community.  This isn't a simple referral tracking system.  Refersion is the most powerful Affiliate Program available and it is waiting for **you** to unlock that power.  With the **GraphQL API**, the entire database of information is at your fingertips.  You can track things, generate reports, and view all of the data Refersion has for your Affiliate program. 

There are three parts of the Refersion system.  The first is the [Tracking Documentation](https://www.refersion.com/tracking).  The Tracking Document shows you how to setup refersion  If you follow the link above for the Tracking Documentation, you will learn how to include the Javascript code on your pages, insert your API keys, and track visists.

The second part of the system is the [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) API.  This API allows you to access functions, creating new customers, etc.  REST is easily accessible using most modern programming languages.  Our API is designed to have predictable, resource-orientated URLs and to use HTTP response codes to indicate API eerrors.  In addition, valid [JSON](https://en.wikipedia.org/wiki/JSON) will be returned in all responses from the API, including errors.  Please refer to our [API docs](https://www.refersion.com/api_docs/#introduction) for additional information.  It will have the latest documentation for all end points as the Refersion API is revised over time.

The third part of the system is [GraphQL](http://facebook.github.io/graphql/October2016/).  GraphQL allows you view all of the data inside of the database.  The entire database of information is available to you.  See the [Overview](#overview) section below for additional information.

## Overview
 
### Introduction
 
The Refersion GraphQL API allows you to query your dataset of affiliate activity through a unified interface.  You don't have to depend on Refersion creating the insight from the data, you can mine the dataset for exactly what you need.

### What is GraphQL?

GraphQL is a new way to think about building and querying APIs. Rather than construct several REST requests to fetch data that you’re interested in, you can often make a single call to fetch the information you need. Additionally you can specify exactly which fields you want included in the response.

GraphQL is, above all, a querying language, and the format of the query you send matches the data you receive. The language has a schema that strongly types the exchange between client and server.

### Running Queries

GraphQL is hierarchical. Fields between curly braces – which are also at the next level of indent – are part of the enclosing type. For example, **id** and **email** are fields available as part of the **affiliate** type and **commission** is a part of offer.

### Why GraphQL

We’re supporting GraphQL because it offers much more flexibility than a traditional [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) interface. GraphQL natively supports performing an introspection query which allows the API to more fully discoverable and easier to integrate against. The ability to define and specify precisely the data you want for your integration is a powerful advantage over the existing REST endpoints. Through fragments and template variables it simplifies many aspects of the client-side integration process. Additionally, because it’s a recognized spec, there are many client libraries and tools to assist you in quickly getting up and running.

### Aditional Resources

Below is some optional reading material that might help you go deeper into the GraphQL ecosystem:

 * [GraphQL Specification](http://facebook.github.io/graphql/October2016/)
 * [Introduction to GraphQL](http://graphql.org/learn/)
 * [The Fullstack Tutorial for GraphQL](https://www.howtographql.com/)
 * [List of GraphQL Tools](https://github.com/chentsulin/awesome-graphql)

## Getting Started

In order to make API requests, you will need an active Refersion account.  You can start your free trial account [here](https://www.refersion.com/signup) or you can email [helpme@refersion.com](mailto:helmpe@refersion.com) for more details. 

### Base URL

All URLS referenced in the documentation have the following base:

    https://graphql.refersion.com

### SSL/HTTPS

The Refersion GraphQL API is serveed over HTTPS.  To ensure data privacy, unencrypted HTTP is not supported.

### Authentication

In order to make calls to our API you need to include your API key along with the request.  You may obtain your API key from your [API Settings](https://www.refersion.com/settings) page while logged in.  *Note, if you are not logged in following this link will lead to a 404 error page.*

We look for your API Key in the Authentication header.

    $ curl "https://graphql.refersion.com"
      -H "Authorization: Bearer [YOUR KEY]"

#### INFO
**It is very important to store your API key in a private and secure location. Sharing your API key is strictly prohibited.**

### Quota & Usage
Each request will return your current usage in the response headers.  

Header            | Description             |
------------------|-------------------------|
X-Quota Limit     | Your Current Request Limit |
X-Quota Remaining | Number of Remaining requests in the current period |
X-Quota-Reset     | The unix timestamp (seconds, UTC) of the start of the next quota period |


### Example Query

The query below also demonstrates how to used **GraphQL** fragments on *affiliate* to query for information specific to sub-type.  In this case, we request a list of affiliates along with the respective offer that they are assigned to.  

    base {
      affiliates(limit:2) {
        id
        email
        offer {
          commission
          type
        }
      }
    }

#### QUERY TYPE MUST BE "BASE"
**Please make sure to start every query with the "base" query tupe as seen above. Currently this is the only supported query type.**

This response returns:

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
 
