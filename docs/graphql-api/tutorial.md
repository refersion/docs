# GraphQL Tutorial

## Scenario

Imagine that you wanted to email all of your affiliates outside of Refersion. To do so, you must pull all of the names (first and last), email addresses, and current commission rate of your affiliates so that they may be automatically entered into your email system.

In this tutorial we will setup our GraphQL API call in order to pull the data we need to satisfy the above use case. 

## Initial Steps

To get started, you'll need access to the following:

1. Your Refersion account GraphQL API key. Grab it from your account settings [here]().
2. A GUI like [Postman](https://www.getpostman.com/) (free) so that you may communicate the API and the response.

#### Want to skip ahead?

If you would like to skip the manual process defined below, click the button below to automatically setup Postman. Do not forget to replace the respective header with your actual account API key.

<div class="postman-run-button"
data-postman-action="collection/import"
data-postman-var-1="3c84e7615fcbf046b007"></div>
<script type="text/javascript">
  (function (p,o,s,t,m,a,n) {
    !p[s] && (p[s] = function () { (p[t] || (p[t] = [])).push(arguments); });
    !o.getElementById(s+t) && o.getElementsByTagName("head")[0].appendChild((
      (n = o.createElement("script")),
      (n.id = s+t), (n.async = 1), (n.src = m), n
    ));
  }(window, document, "_pm", "PostmanRunObject", "https://run.pstmn.io/button.js"));
</script>

## Setup Endpoint and Headers

With GraphQL the URL that you post remains consistant with every call. Use this one for Refersion:

**`https://graphql.refersion.com`**

Every request into the API also requires the following headers:

- **`X-Refersion-Key: API-KEY`** <br>This your API key (replace with "API-KEY").
- **`Content-Type: application/graphql`** <br>This is a static header that tells our system that you're sending a valid JSON string.

!!! Info
	A `Content-Type: application/json` header is also supported as an alternative for more advanced users who want more customization. Additional information how this header value interacts with our API is available [here](http://graphql.org/learn/serving-over-http/#post-request).

_Screenshot from Postman:_

<div style="text-align: center;">
<img src="/assets/images/postman-headers.png" alt="Postman headers screenshot" />
</div>

## Building a GraphQL Query

On every request to GraphQL you must define the format of the JSON response that you expect. This is done in the body of the request. For our purposes, we want a JSON array to be returned containing basic information about each affiliate as well as their commission structure in a nested array. To accomplish this, we send the following as the body of our request: 

```scss
{
  affiliates(limit: 2) {
    id
    first_name
    last_name
    email
    offer {
      commission
      type
    }
  }
}
```

!!! Note
	Names in GraphQL are case‐sensitive. That is to say name, Name, and NAME all refer to different names. Underscores are significant, which means other_name and othername are two different names.

## Expected Result

Assuming that you were able get a successful response (code 200), it should look something like this:

```json
{
  "data": {
    "affiliates": [
      {
        "id": 444,
        "first_name": "Jane",
        "last_name": "Verde",
        "email": "jane.verde@aol.com",
        "offer": {
          "commission": "10",
          "type": "FLAT_RATE"
        }
      },
      {
        "id": 419,
        "first_name": "Mike",
        "last_name": "Rogers",
        "email": "mike.rogers@hotmail.com",
        "offer": {
          "commission": "10",
          "type": "FLAT_RATE"
        }
      }
    ]
  }
}
```