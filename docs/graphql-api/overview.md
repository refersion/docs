# GraphQL Overview

## Introduction

The Refersion GraphQL API allows you to query your dataset of affiliate activity through a unified interface. You don't have to depend on Refersion creating the insight from the data, you can mine the dataset for exactly what you need.

<div style="text-align: center;">
<iframe width="560" height="315" src="https://www.youtube.com/embed/gdoRAPW7Abc" frameborder="0" gesture="media" allow="encrypted-media" allowfullscreen></iframe>
</div>

## What is GraphQL?

GraphQL is a new way to think about building and querying APIs. Rather than construct several REST requests to fetch data that you’re interested in, you can often make a single call to fetch the information you need. Additionally you can specify exactly which fields you want included in the response.

Example request and response:

<div style="text-align: center;">
<img src="/assets/images/graphql-response-animation.gif" alt="What you request is what you get" />
</div>

GraphQL is, above all, a querying language, and the format of the query you send matches the data you receive. The language has a schema that strongly types the exchange between client and server.

## Running Queries

GraphQL is hierarchical. Fields between curly braces – which are also at the next level of indent – are part of the enclosing type. For example, `id` and `email` are fields available as part of the `affiliate` type and `commission` is a part of `offer`.

## Why GraphQL?

We’re supporting GraphQL because it offers much more flexibility than a traditional REST interface. GraphQL natively supports performing an introspection query which allows the API to more fully discoverable and easier to integrate against. The ability to define and specify precisely the data you want for your integration is a powerful advantage over the existing REST endpoints. Through fragments and template variables it simplifies many aspects of the client-side integration process. Additionally, because it’s a recognized spec, there are many client libraries and tools to assist you in quickly getting up and running.

## Additional Resources

Below is some optional reading material that might help you go deeper into the GraphQL ecosystem:

- [GraphQL Specification](http://facebook.github.io/graphql/)
- [Introduction to GraphQL](http://graphql.org/learn/)
- [The Fullstack Tutorial for GraphQL](https://www.howtographql.com/0)
- [List of GraphQL Tools](https://github.com/chentsulin/awesome-graphql)

