# Donorbox API

## Getting Started

You’ll need a API KEY to connect to Donorbox. To create a key, you’ll need to sign up at https://donorbox.org. After you register in Donorbox click Account click **Account in top navigation**, then click **API Key in left navigation** and click **Set new api key**. 

![Donorbox Api](https://github.com/donorbox/donorbox/wiki/images/zapier/dbox_zap_02_api_key.png)

**Copy the generated API key** to some place safe as this key will only be **shown once for security** reasons.

![donorbox api](https://github.com/donorbox/donorbox/wiki/images/zapier/dbox_zap_03_api_key.png)

## Make API calls to Donorbox

Each HTTP request consists of an HTTP Method and an endpoint. Throughout the documentation, these requests are formatted like the following example.

` {METHOD} https://donorbox.org/{endpoint} `

All the API calls will need a basic authentication, you need to send a username which is your organization email and a password which is your API KEY.
### Campaigns

Get information for all your campaigns.

` {GET} https://donorbox.org//api/v1/campaigns`

Output:

```json
[
  {
    "id":1,
    "name":"Donorbox New Campaign",
    "slug":"donorbox-new-campaign",
    "currency":"usd",
    "created_at":"2017-10-20T22:30:55.620Z",
    "updated_at":"2017-10-20T22:30:55.620Z",
    "goal_amt":"10000.0",
    "formatted_goal_amount":"$1,0000",
    "total_raised":"2000.0",
    "formatted_total_raised":"$2000",
    "donations_count":66
  }
]
```



### Donations

Get all your organization's donations.

` {GET} https://donorbox.org//api/v1/donations`

Output:

```json
[ 
  {
    "campaign":
      {
        "id": 1,
        "name":"Donorbox Campaign"
      },
    "donor":
      {
        "id":1,
        "name":"John Doe",
        "first_name":"John",
        "last_name":"Doe",
        "email":"johndoe@gmail.com",
        "address":"123 6th St. Melbourne, FL 32904",
        "city":"Melbourne",
        "state":"FL",
        "zip_code": "32904",
        "country":"USA",
        "employer":null,
        "occupation":null
      },
    "amount":"100.0",
    "formatted_amount":"$100",
    "recurring":false,
    "first_recurring_donation":false,
    "amount_refunded":"0.0",
    "formatted_amount_refunded":"$0",
    "stripe_charge_id":"ch_1BF94aBku99FiTp3uJM5mSKw",
    "id":1,
    "status":"paid",
    "donation_type":"stripe",
    "donation_date":"2017-10-20T22:34:35.656Z",
    "anonymous_donation":false,
    "gift_aid":false,
    "comment":"thanks",
    "donating_company":null,
    "currency":"USD",
    "processing_fee":"0.59",
    "formatted_processing_fee":"$0.59",
    "questions":[]
  }
]
```
### Donors

Get information for all your donors.

` {GET} https://donorbox.org//api/v1/donors`

Output:

```json
[
  {
    "id":35,
    "created_at":"2017-11-20T14:01:35.597Z",
    "updated_at":"2017-11-28T21:49:25.127Z",
    "first_name":"John",
    "last_name":"Doe",
    "email":"johndoe@email.com",
    "phone":"123456789",
    "address":"123 6th St. Melbourne, FL 32904",
    "city":"Melbourne",
    "state":"FL",
    "zip_code":"32904",
    "country":"USA",
    "employer":null,
    "occupation":null,
    "comment":null,
    "donations_count":2,
    "last_donation_at":"2017-11-28T21:48:51.260Z",
    "total":[
      {
        "currency":"usd",
        "value":100.0
      }
    ]
  }
]
```

## Pagination

Donorbox API supports pagination for all their GET endpoints. The paging mechanism is very easy to use. The default pagination for all end points is 50 records.

Example:

{METHOD} https://donorbox.org/{endpoint}.json?page=2 `



