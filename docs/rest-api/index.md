# Refersion REST API 

The Refersion API is organized around REST, which is easily accessible using most modern programming languages. Our API is designed to have predictable, resource-oriented URLs and to use HTTP response codes to indicate API errors. In addition, valid JSON will be returned in all responses from the API, including errors.


> **Note:** The API is still in beta.  This document will be updated as new endpoints are released to our users.


## Authentication

Most API endpoints require authentication, which is done using your public and private API keys. You can generate new API keys right from your account settings. Your public key may be used in client-side implementations, but your private key should be kept secure and never be visible to end users.

All API requests must be made over HTTPS.

> **Note:** The API keys used in the examples in this documentation are not registered to your account and are inactive.

## Check API Keys

First, check that your API keys are correc.t  Succesful responses will get an empty JSON array.

### HTTPS Request

`POST httpsL//www.refersion.com/api/check_account`

### Query Parameters


**Field**     | **Description** |
----------|-------------|
refersion\_public\_key | Your public API key |
refersion\_public\_key | Your private API key |

`{
  "refersion_public_key": "pub_foo9034da4fsegea123",
  "refersion_secret_key": "sec_bar8abbb7ed4a7db456"
}`

## Affiliates

### New Affiliate
Create a new affiliate. Returns the affiliate ID and their referral link.

**Tip:** When creating affilates using this endpoint, we recommend that you save the `id` from the response in order to map your user to their affiliate account in Refersion.

#### HTTPS Request

`POST https://www.refersion.com/api/new_affiliate`

#### Query Parameters

**Field** | **Required** | **Special Notes** |
----------|--------------|-------------------|
refersion\_public\_key	| Yes | Your public API key |
refersion\_secret\_key	| Yes | Your private API key |
offer	| Optional | Specifc Offer ID to opt affiliate into, otherwise your default offer is used. |
first_name |	Yes | | 	
last_name	| Yes | |
company | Optional | |	
email | Yes | Must be a valid email. |
paypal_email | Optional | If included, must be a valid email.|
password | Yes | At least 6 characters. |
address1 | Optional | |	
address2 | Optional | |	
city | Optional | |	
zip	 | Optional | |	
country | Optional	| Country Code (two letter abbreviation) must match one of: US, UK, CA, AU, FR, GR, MX, NO, NL, NZ, ES |
state	| Optional | State abbreviation.|
phone	| Optional | |	
send_welcome	| Optional | Should Refersion send our welcome email? Otions: TRUE / FALSE; Default = FALSE |

> **Note:** If you want to send custom fields, please contact us for detailed instructions.

#### Example Request

`{
  "refersion_public_key": "pub_foo9034da4fsegea123",
  "refersion_secret_key": "sec_bar8abbb7ed4a7db456",
  "order_id":"123",
  "first_name":"Bill",
  "last_name":"Smith",
  "company":"Refersion",
  "email":"testing@refersion.com",
  "paypal_email":"testing@refersion.com",
  "password":"testing",
  "address1":"123 Street Road",
  "address2":"Suite 123",
  "city":"New York",
  "zip":"10010",
  "country":"US",
  "state":"NY",
  "phone":"2122425252",
  "send_welcome":"TRUE"
}`

#### Example Response - Success

`{
  "id":"a3y7",
  "link":"https:\/\/site.refersion.com\/c\/a3y7"
}`

#### Example Response - Failure

`{
  "errors":[
    "The First Name field is required.",
    "The email you have entered is taken by another Affiliate."
  ]
}`

### Get Affiliate 

Get information about an affiliate

#### HTTPS Request

> POST https://www.refersion.com/api/get_affiliate

#### Query Parameters

**Field** | **Required** | **Special Notes** |
----------|--------------|-------------------|
refersion\_public\_key	| Yes	| Your public API key. |
refersion\_secret\_key	| Yes	| Your private API key. |
affiliate_code | Yes | The Refersion affiliate identifier. You would have captured this from the new_affiliate endpoint response. |

#### Example Request 

`{
  "refersion_public_key": "pub_foo9034da4fsegea123",
  "refersion_secret_key": "sec_bar8abbb7ed4a7db456",
  "affiliate_code": "a3y7"
}`

#### Example Response - Success

`{
  "id": "694c",
  "offer_id": "1234",
  "status": "ACTIVE",
  "first_name":"Bill",
  "last_name":"Smith",
  "email":"testing@refersion.com",
  "link":"https:\/\/site.refersion.com\/c\/a3y7",
  "custom_fields": [
      {
          "label": "What is your web site?",
          "value": "https://www.refersion.com"
      },
      {
          "label": "What is your name?",
          "value": "Billy"
      }
  ]
}`

### Search Affiliates

Find affiliates based on email address or ID.

#### HTTPS Request

> POST https://www.refersion.com/api/search_affiliates

#### Query Parameters

**Field** | **Required** | **Special Notes** |
----------|--------------|-------------------|
refersion\_public\_key	| Yes	| Your public API key.
refersion\_secret\_key	| Yes	| Your private API key.
keyword | Yes	 | The keyword to search for. Can be the affiliate ID or registered email address. Affiliate ID must be exact and complete, but email can be a partial string.

#### Example Request

`{
   "refersion_public_key": "pub_foo9034da4fsegea123",
   "refersion_secret_key": "sec_bar8abbb7ed4a7db456",
   "keyword": "testing"
}`

#### Example Response Success

`{
  "total": 2,
  "results": [
     {
        "id": "694c",
        "offer_id": "1234",
        "status": "ACTIVE",
        "first_name": "Barbara",
        "last_name": "Verde",
        "email": "testing1@refersion.com",
        "custom_fields": [
            {
                "label": "What is your web site?",
                "value": "https://www.refersion.com"
            },
            {
                "label": "What is your name?",
                "value": "Billy"
            }
        ]
    },
    {
        "id": "24fb",
        "offer_id": "5678",
        "status": "PENDING",
        "first_name": "Joe",
        "last_name": "Smith",
        "email": "testing2@refersion.com",
        "custom_fields": []
    }
  ]
}`

### List All Affiliates

Get all affiliates in your account.

#### HTTPS Request

> POST https://www.refersion.com/api/list_affiliates

#### Query Parameters

**Field** | **Required** | **Special Notes** |
----------|--------------|-------------------|
refersion\_public\_key	| Yes	| Your public API key.
refersion\_secret\_key	| Yes	| Your private API key.
limit	| No	| Total that should be returned per API call. Maximum of 100 per call.
page	| No	| Page offset.

#### Example Request

`{
  "refersion_public_key": "pub_foo9034da4fsegea123",
  "refersion_secret_key": "sec_bar8abbb7ed4a7db456",
  "limit": "3",
  "page": "1"
}`

#### Example Response Success 

`{
  "total": 3,
  "results": [
     {
        "id": "694c",
        "offer_id": "1234",
        "status": "ACTIVE",
        "first_name": "Barbara",
        "last_name": "Verde",
        "email": "testing1@refersion.com",
        "custom_fields": [
            {
                "label": "What is your web site?",
                "value": "https://www.refersion.com"
            },
            {
                "label": "What is your name?",
                "value": "Billy"
            }
        ]
    },
    {
        "id": "24fb",
        "offer_id": "5678",
        "status": "ACTIVE",
        "first_name": "Joe",
        "last_name": "Smith",
        "email": "testing2@refersion.com",
        "custom_fields": []
    },
    {
        "id": "g23fz",
        "offer_id": "101112",
        "status": "ACTIVE",
        "first_name": "Martha",
        "last_name": "Williams",
        "email": "testing3@refersion.com",
        "custom_fields": []
    }
  ]
}`

### Create Conversion Trigger

Create a Conversion Trigger for a specific affiliate.

#### HTTPS Request

> POST https://www.refersion.com/api/new_affiliate_trigger

#### Query Parameters

**Field** | **Required** | **Special Notes** |
----------|--------------|-------------------|
refersion\_public\_key |	Yes |	Your public API key.
refersion\_secret\_key	| Yes	| Your private API key.
affiliate_code	| Yes	| The Refersion affiliate identifier. You would have captured this from the new_affiliate endpoint response.
type	| Yes	| The type of Conversion Trigger. Accepted values are: COUPON, SKU, EMAIL
trigger	| Yes	| The actual conversion trigger that should be set. For example, an email address for email triggers and a coupon code for coupon triggers.

#### Example Request

`{
  "refersion_public_key": "pub_foo9034da4fsegea123",
  "refersion_secret_key": "sec_bar8abbb7ed4a7db456",
  "affiliate_code": "a3y7",
  "type": "COUPON",
  "trigger":"code100"
}`

#### Example Response Success 

`{
  "trigger_id": 1097,
  "trigger": "CODE100"
}`

## Offers

### New SKU Level Commission

Add SKU Specific commission rates to a specific offer.  Your plan must support SKU / Product Level Commissions

#### HTTPS Request

> POST https://www.refersion.com/api/offer/new_sku_commission

#### Query Parameters

**Field** | **Required** | **Special Notes** |
----------|--------------|-------------------|
refersion\_public\_key	| Yes	| Your public API key.
refersion\_secret\_key	| Yes	| Your private API key.
offer\_id	| Yes	| The offer ID in which this SKU commission belongs to.
skus	| Yes	| An array of all SKUs to add. Max: 50
sku	 | Yes	| Must match the exact SKU that would be ordered.
product\_description	| Optional	| A custom label for the SKU to give affiliates more detail.
commission_type	| Yes	| Must match exactly one of: FLAT_RATE, PERCENT_OF_SALE
commission_amount	| Yes	| Amount of commission. Must be a numeric value. For example, for 10%, enter 10.

#### Example Request

`{
  "refersion_public_key":"pub_foo9034da4fsegea123",
  "refersion_secret_key":"sec_bar8abbb7ed4a7db456",
  "offer_id":"12345",
  "skus":[
    {
      "sku":"TSHIRT-SMALL-RED",
      "product_description":"T-Shirt Red (Small)",
      "commission_type":"FLAT_RATE",
      "commission_amount":"5"
    },
    {
      "sku":"TSHIRT-SMALL-BLUE",
      "commission_type":"PERCENT_OF_SALE",
      "product_description":"T-Shirt Blue (Small)",
      "commission_amount":"25"
    },
    {
      "sku":"PANTS-LARGE-BLACK",
      "product_description":"Pants Black (Large)",
      "commission_type":"PERCENT_OF_SALE",
      "commission_amount":"10"
    }
  ]
}`

#### Example Response Success

`{
    "duplicate_not_added": [
        "TSHIRT-SMALL-RED"
    ],
    "added": [
        "TSHIRT-SMALL-BLUE",
        "PANTS-LARGE-BLACK"
    ]
}`


## Payments

### Process Manual Payment

Report a manual payment for specific conversions in Refersion.

> POST https://www.refersion.com/api/process_manual_payment

#### Query Parameters

**Field** | **Required** | **Special Notes** |
----------|--------------|-------------------|
refersion\_public\_key	| Yes	| Your public API key.
refersion\_secret\_key	| Yes	| Your private API key.
conversion\_ds	| Yes	| An array containing the Refersion conversion IDs that you want to process payment for.
payment_method	| Yes	| Must be set to MANUAL.

#### Example Request

`{
  "refersion_public_key": "pub_foo9034da4fsegea123",
  "refersion_secret_key": "sec_bar8abbb7ed4a7db456",
  "conversion_ids":[123,456,789],
  "payment_method":"MANUAL"
}
`

## Reporting

### Generate Download Link

Get a public download link for a report.  Links expire in 2 minutes from the time of request for security purposes.

> POST https://www.refersion.com/api/reporting/get_link

#### Query Parameters

**Field** | **Required** | **Special Notes** |
----------|--------------|-------------------|
refersion\_public\_key	| Yes	| Your public API key.
refersion\_secret\_key	| Yes	| Your private API key.
report\_id	| Yes	| The report ID of the report that you want to generate a download link for.

#### Example Request

`{
  "refersion_public_key": "pub_foo9034da4fsegea123",
  "refersion_secret_key": "sec_bar8abbb7ed4a7db456",
  "report_id": 123
}`

#### Example Response Success

`{
  "download_link": "https://www.refersion.com/api/reporting/download/37/87/154ac2e00df1e6275b1a60869ab3123fceea16f5",
  "expire_time": 1452028425
}`

## Errors

The Reference API will pass a response code in all API responses (successful or not).  The chart below details each response code that you may encounter.

**Code** | **Meaning** |
----------|--------------|
401	| Unauthorized – Your API keys are incorrect.
404	 | Not Found – The API endpoint that you’re attempting to access was not found.
422	 | Unprocessable Entity – The data that you’re sending has errors.
429	 | Too Many Requests – You’re making too many API calls. Please limit your usage.
500	 | Internal Server Error – We had a problem with our server. Try again later.
503	 | Service Unavailable – We’re temporarially offline for maintanance. Please try again later.