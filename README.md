# Donorbox API

## Getting Started


You’ll need an API KEY to connect to Donorbox. To create a key, you’ll need to sign up at https://donorbox.org. After you register with Donorbox, click **Account** in the top navigation, click **API & Zapier Integration** on the left, and select **Enable API & Zapier Integration**. After you confirm and add your billing information, select **Set new API Key**.


Please be aware that the **API & Zapier integration** costs $17/month.

If you are looking to integrate with **[Zapier](https://zapier.com)**, please follow the guide at https://github.com/donorbox/donorbox-api/wiki/Getting-started-with-Zapier.

![Donorbox Api](https://github.com/donorbox/donorbox-api/blob/master/preview-lightbox-API2.jpg)


**Copy the generated API key** to a safe place as this key will only be **shown once for security reasons**.

![donorbox api](https://github.com/donorbox/donorbox-api/wiki/images/copy_api_key.png)

## Make API calls to Donorbox

Donorbox API uses basic authentication as our authorization method. Use your organization login email as your authorization username and the API Key as your password.

Here is the general format using cURL:

`curl -X METHOD --user login@email.com:YOUR_API_KEY https://donorbox.org/{endpoint}` 

To test our API endpoints directly in a web browser, use the following format:

`https://login@email.com:API_KEY_XXX@donorbox.org/{endpoint}`

If your browser does not support this basic authentication URL pattern, use the endpoint URL `https://donorbox.org/{endpoint}` without email & password and provide these credentials on popup.

------------------------------------------------------------------

This is the Donorbox API endpoints URL with appropriate HTTP method:

`{METHOD} https://donorbox.org{endpoint}`

Throughout the documentation we will omit the host name, mentioning only the HTTP `METHOD` and the `endpoint` e.g. `{GET} /api/v1/campaigns`. 


## Donorbox API endpoints
### Campaigns

Get information for all your campaigns.

`{GET} /api/v1/campaigns`

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

`{GET} /api/v1/donations`

Output (Stripe):

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
            "address":"123 6th St.",
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
        "utm_campaign": "google_ads",
        "utm_source": "Adwords",
        "utm_medium": "cpc",
        "utm_term": "nonprofit fundraising",
        "utm_content": "np1",
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

Output (PayPal):

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
            "address":"123 6th St.",
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
        "paypal_transaction_id": "RANDOMPAYPALID",
        "id": 1,
        "status": "paid",
        "donation_type": "paypal",
        "donation_date": "2017-12-21T17:54:13.432Z",
        "anonymous_donation": false,
        "gift_aid": false,
        "comment": "thanks",
        "donating_company": null,
        "currency": "USD",
        "converted_currency": "USD",
        "utm_campaign": "google_ads",
        "utm_source": "Adwords",
        "utm_medium": "cpc",
        "utm_term": "nonprofit fundraising",
        "utm_content": "np1",
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

### Plans

Get information for all your plans.

`{GET} /api/v1/plans`


Output:

```
[
  {
    "id": 168,
    "campaign": {
        "id": 61,
        "name": "Save the jungle campaign"
    },
    "donor": {
        "id": 384,
        "name": "Bruce Waine",
        "first_name": "Bruce",
        "last_name": "Waine",
        "email": "bruce@email.com",
        "phone": "8038984624",
        "address": "123 6th St.",
        "city":"Melbourne",
        "state":"FL",
        "zip_code":"32904",
        "country": "USA",
        "employer": "Waine Industries",
        "occupation": "CEO"
    },
    "type": "monthly",
    "amount": "10.0",
    "formatted_amount": "$10",
    "payment_method": "Stripe",
    "started_at": "2018-07-25",
    "last_donation_date": "2018-07-25T05:00:00.000Z",
    "next_donation_date": "2018-08-25",
    "status": "active"
  }
]
```

### Donors

Get information for all your donors.

`{GET} /api/v1/donors`

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
    "address":"123 6th St.",
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

### Filter by campaign
Use `campaign_id` parameter to narrow down the result by a specific campaign. This filter is valid for [Donations](#donations) and [Plans](#plans) endpoints.

e.g. `{GET} /api/v1/donation?campaign_id=XX`


### Filter by email
Use `email` parameter to filter the result by a given email address. This filter is valid only for [Plans](#plans) endpoint.

e.g. `{GET} /api/v1/plans?email=XXXX`


### Ordering
All Donorbox API endpoints support ordering. Use `order` parameter with `asc|desc` possible values. The default is `desc`.

e.g `{GET} /api/v1/donations?order=asc`


### Pagination
All Donorbox API endpoints support pagination. Provide `page` and `per_page` parameters to split the result accordingly. The default page size (`per_page` parameter's value) is 50, maximum 100 allowed. If it exceeds the maximum, it will fallback to default.

e.g. `{GET} /api/v1/donors?page=2&per_page=18`


#### Combine filters

Of course, you can combine any of the filters described above, taking into account supported endpoints for a specific filter.

e.g. `{GET} /api/v1/donations?order=asc&page=3&per_page=20&campaign_id=XX`

