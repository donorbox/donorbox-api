# Donorbox API

## Getting Started


You’ll need a API KEY to connect to Donorbox. To create a key, you’ll need to sign up at https://donorbox.org. After you register in Donorbox click **Account in top navigation**, then click **API Key in left navigation** and click **Set new api key**. 

Please be aware the **API & Zapier integration** has a costs of $17/month

If you are looking to integrate with **[Zapier](https://zapier.com)**, please follow the guide at https://github.com/donorbox/donorbox-api/wiki/Getting-started-with-Zapier

![Donorbox Api](https://github.com/donorbox/donorbox-api/wiki/images/dbox_zap_02_api_key.png)


**Copy the generated API key** to some place safe as this key will only be **shown once for security** reasons.

![donorbox api](https://github.com/donorbox/donorbox-api/wiki/images/copy_api_key.png)

## Make API calls to Donorbox

All the API calls will need a basic authentication, you need to send a username which is your organization email and a password which is your API KEY.

To make call using curl use 

`curl --user login@email.com:API_KEY_XXX https://donorbox.org/{endpoint}` 

The general format for basic authentication on Donorbox is

`https://login@email.com:API_KEY_XXX@donorbox.org/{endpoint}`

If your browser does not support this basic authentication url pattern, kindly use the basic endpoint url `https://donorbox.org/{endpoint}` without email and password and provide these credentials on popup. 

Throughout the rest of document we will use example urls without basic authentication format for simplicity, but it should be nothed that all the calls are with Basic authentication. 

Each HTTP request consists of an HTTP Method and an endpoint. Throughout the documentation, these requests are formatted like the following example.

` {METHOD} https://donorbox.org/{endpoint} `

### Campaigns

Get information for all your campaigns.

` {GET} https://donorbox.org/api/v1/campaigns`

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

` {GET} https://donorbox.org/api/v1/donations`

Output:

```json
[
    {
        "campaign": {
            "id": 1,
            "name": "Donorbox Campaign"
        },
        "donor": {
            "id": 59,
            "name": "John Doe",
            "first_name": "John",
            "last_name": "Doe",
            "email": "johndoeemail@hotmail.com",
            "address":"123 6th St. Melbourne, FL 32904",
            "city":"Melbourne",
            "state":"FL",
            "zip_code": "32904",
            "country":"USA",
            "employer":null,
            "occupation":null
        },
        "amount": "100.0",
        "formatted_amount": "$100",
        "converted_amount": "100.0",
        "formatted_converted_amount": "$100",
        "recurring": false,
        "first_recurring_donation": false,
        "amount_refunded": "0.0",
        "formatted_amount_refunded": "$0",
        "stripe_charge_id": "ch_1BF94aBku99FiTp3uJM5mSKw",
        "id": 1,
        "status": "paid",
        "donation_type": "stripe",
        "donation_date": "2017-12-21T17:54:13.432Z",
        "anonymous_donation": false,
        "gift_aid": false,
        "designation": "Designed Cause",
        "join_mailing_list": false,
        "comment": "thanks",
        "donating_company": null,
        "currency": "USD",
        "converted_currency": "USD",
        "processing_fee": 0.59,
        "formatted_processing_fee": "$0.59",
        "questions": [
            {
              "question_type": "radiobutton",
              "question": "Would you like to volunteer?",
              "answer": "Yes"
            },
            {
              "question_type": "text",
              "question": "Why are you donating",
              "answer": "I would like to help"
             },
             {
              "question_type": "check",
              "question": "First/Last Name is correct?",
              "answer": true
             },
             {
              "question_type": "dropdown",
              "question": "Would you like to showcase your donation",
              "answer": "Yes"
             }
        ]
    }
]
```

### Donors

Get information for all your donors.

` {GET} https://donorbox.org/api/v1/donors`

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
## Filters

Donorbox allows you add several filters to your donations. 

### Search by Campaign ID

Get all the donations of a specific campaign:

`{GET} https://donorbox.org/api/v1/donation?campaign_id=XX`

### Number of donations per page

Set up the number of donations that you require per page

`{GET} https://donorbox.org/api/v1/donations?per_page=XX`

### Order Donations

Order your donations ascending or descending

`{GET} https://donorbox.org/api/v1/donations?order=asc`

`{GET} https://donorbox.org/api/v1/donations?order=desc`

### Combine filter

You can combine any of the filters described before. Ex:

`{GET} https://donorbox.org/api/v1/donations?order=asc&per_page=XX&campaign_id=XX`

## Pagination

Donorbox API paging mechanism is very easy to use. The default pagination for the end points is 50 records.

Pagination is supported for the following GET endpoints.

* Donors. Ex: {GET} https://donorbox.org/api/v1/donors?page=2
* Donations. Ex: {GET} https://donorbox.org/api/v1/donations?page=2`
