# Getting Started

!!! Important
    This is a Beta API and is subject to change.

## Endpoint

Unlike Refersion’s REST API which has a variety of endpoints, the GraphQL API has a single endpoint:

<b>
```bash
POST https://graphql.refersion.com
```
</b>

## Authentication
The GraphQL API requires an access token for making authenticated requests.



##### Getting your access token 

Refersion merchants can obtain access token by logging into your Refersion account and navigating to [Account/Settings/Refersion API/GraphQL](https://www.refersion.com/base/settings/integrations/api). 

If you are a [Refersion Marketplace](https://marketplace.refersion.com/) user and would like to use GraphQL, please email us at [helpme@refersion.com](mailto:helpme@refersion.com) to request access. Once GraphQL has been enabled on your account, the token will be available on your [Marketplace Profile](https://marketplace.refersion.com/profile) page.

## Making your first query
You can access the GraphQL API endpoint using cURL or any other HTTP client. For the following test example, make sure to replace `<ACCESS_TOKEN>` with the token you obtained from the Authentication section.  


#### curl
To make a query using curl, send a POST request with your query as the JSON payload.

```bash
curl -X POST \
"https://graphql.refersion.com" \
-H "X-Refersion-Key: <OUR_ACCESS_TOKEN>" \
-H "Content-Type: application/json" \
```


#### Example Query
```json
{
	"query": "{  
	 	offers { 
	 	 	offer_name, 
	 	 	commission, 
	 	 	type 
	 	} 
	}"
}
```