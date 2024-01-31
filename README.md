# Donorbox API

## Getting Started


You’ll need an API KEY to connect to Donorbox. To create a key, you’ll need to sign up at https://donorbox.org. After you register with Donorbox, click **Account** in the top navigation, click **API & Zapier Integration** on the left, and select **Enable API & Zapier Integration**. After you confirm and add your billing information, select **Set new API Key**.


Please be aware that the **API & Zapier integration** costs $17/month.

Donorbox provides webhooks too for all the API endpoints documented in this guide. Take a look at the following document if you are looking to enable webhooks on your custom endpoints instead of polling the APIs: **[Custom Webhooks Configuration in Donorbox](https://donorbox.zendesk.com/hc/en-us/articles/4733681068820-Custom-Webhooks)**

If you are looking to integrate with **[Zapier](https://zapier.com)**, please follow the guide at https://github.com/donorbox/donorbox-api/wiki/Getting-started-with-Zapier.

![Donorbox Api](https://github.com/donorbox/donorbox-api/blob/master/preview-Donorbox-API.png)


**Copy the generated API key** to a safe place as this key will only be **shown once for security reasons**.

![donorbox api](https://github.com/donorbox/donorbox-api/blob/master/preview-Donorbox-API-key.png)

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

```json
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

### Events

Get information for all your campaigns.

`{GET} /api/v1/events`

Output:

```json
[
  {
    "id": 123123,
    "name": "Concert for a Cure",
    "slug": "concert-for-a-cure",
    "currency": "usd",
    "created_at": "2023-10-03T20:44:18Z",
    "updated_at": "2023-10-23T06:19:43Z",
    "total_raised": 0,
    "formatted_total_raised": "$0",
    "donations_count": 0,
    "tickets_count": 8
  }
]
```

### Tickets

Get information for all your campaigns.

`{GET} /api/v1/tickets`

Output:

```json
[
  {
    "id": 123456,
    "currency": "USD",
    "free_ticket": false,
    "price": 1.04,
    "price_formatted": "$1.04",
    "ticket_type": {
      "id": 15132,
      "name": "General Admission",
      "fair_market_value": 0.4,
      "fair_market_value_formatted": "$0.40",
      "tax_deductible_amount": 0.6,
      "tax_deductible_amount_formatted": "$0.60",
      "tax_amount": 0.04,
      "tax_amount_formatted": "$0.04"
    },
    "event": {
      "id": 123123,
      "name": "Concert for a Cure"
    },
    "transaction": {
      "id": 212321,
      "city": "Alexandria",
      "state": "Viginia",
      "country": "US",
      "zip": "22304",
      "currency": "USD",
      "first_name": "Jimmy",
      "last_name": "Wang",
      "donation_id": null,
      "stripe_charge_id": "py_dhjfkxnh",
      "full_name": "Jimmy Wang",
      "address": "4801 Kenmore Ave",
      "phone": "8509608580",
      "email": "jw@example.org",
      "supporter_id": 9635959,
      "status": "paid",
      "purchase_date": "2023-10-04T16:50:33Z",
      "free_purchase": false,
      "price": 0.82,
      "price_formatted": "$0.82",
      "donation_amount": null,
      "donation_amount_formatted": null,
      "app_fee": 0.01,
      "app_fee_formatted": "$0.01",
      "stripe_fee": 0.33,
      "stripe_fee_formatted": "$0.33",
      "slug": "212321-hsdemhehe",
      "preferences_answer": null
    }
  }
]
```

### Event ticket purchases

Get information for all your campaigns.

`{GET} /api/v1/purchases`

Output:

```json
[
  {
    "id": 231234,
    "currency": "USD",
    "status": "paid",
    "supporter_id": 986732,
    "amount": 0.82,
    "amount_formatted": "$0.82",
    "amount_refunded": 0.82,
    "date": "2023-10-04T16:50:33Z",
    "tickets_count": 1,
    "preferences_answer": null,
    "event": {
      "id": 123123,
      "name": "Concert for a Cure"
    },
    "tickets": [
      {
        "id": 675645,
        "currency": "USD",
        "free_ticket": false,
        "price": 1.04,
        "price_formatted": "$1.04",
        "ticket_type": {
          "id": 87678,
          "name": "General Admission",
          "fair_market_value": 0.4,
          "fair_market_value_formatted": "$0.40",
          "tax_deductible_amount": 0.6,
          "tax_deductible_amount_formatted": "$0.60",
          "tax_amount": 0.04,
          "tax_amount_formatted": "$0.04"
        }
      }
    ]
  }
]
```

## Filters

### Campaign Filters
Use `campaign_id` parameter to narrow down the result by a specific campaign.

e.g. `{GET} /api/v1/campaigns?id=XX`

To filter campaigns by campaign name, use:

`{GET} /api/v1/campaigns?name=XXXXXXXX`


### Plan Filters
Use `email` parameter to filter the plans by a given donor's email address. This filter is valid only for [Plans](#plans) endpoint.

e.g. `{GET} /api/v1/plans?email=XXXX`

Use `date_from` and `date_to` filters to filter plans by started date. The valid date formats include: `YYYY-mm-dd YYYY/mm/dd YYYYmmdd dd-mm-YYYY`

e.g. `{GET} /api/v1/plans?date_from=YYYY-mm-dd&date_to=YYYY-mm-dd`

Use `campaign_id` filter to filter plans by campaign id. This is the Donorbox campaign id.

e.g. `{GET} /api/v1/plans?campaign_id=XXXX`

Use `campaign_name` filter to filter plans by campaign name. This is the Donorbox campaign title that you have defined in Donorbox.

e.g. `{GET} /api/v1/plans?campaign_name=XXXXXXX`

Use `donor_id` filter to filter plans by Donorbox donor id. This is the Donorbox generated donor id.

e.g. `{GET} /api/v1/plans?donor_id=XXXXXXX`

Use `first_name` filter to filter plans by donor's first name.

e.g. `{GET} /api/v1/plans?first_name=XXXXXXX`

Use `last_name` filter to filter plans by donor's last name.

e.g. `{GET} /api/v1/plans?last_name=XXXXXXX`

Use `donor_name` filter to filter plans by donor's full name. Note this filter would be similar to using the first_name and last_name paramters in conjunction like `first_name=XXXX&last_name=YYYYYY` 

e.g. `{GET} /api/v1/plans?last_name=XXXXXXX XXXXX`


### Donor Filters

Use `id` filter to filter donors by Donorbox donor id. This is the Donorbox generated donor id.

e.g. `{GET} /api/v1/donors?id=XXX`

Use `first_name` filter to filter and get donors by donor's first name.

e.g. `{GET} /api/v1/donors?first_name=XXXXXXX`

Use `last_name` filter to filter and get donors by donor's last name.

e.g. `{GET} /api/v1/donors?last_name=XXXXXXX`

Use `donor_name` filter to filter donors by donor's full name. Note this filter would be similar to using the first_name and last_name paramters in conjunction like `first_name=XXXX&last_name=YYYYYY` 

e.g. `{GET} /api/v1/donors?last_name=XXXXXXX XXXXX`

Use `email` filter to filter and get donors by donor's email.

e.g. `{GET} /api/v1/donors?email=XXXXXXX`

### Donation Filters

Use `email` filter to filter and get donations by donor's email.

e.g. `{GET} /api/v1/donations?email=XXXXXXX`

Use `date_from` and `date_to` filters to filter donations by started date. The valid date formats include: `YYYY-mm-dd YYYY/mm/dd YYYYmmdd dd-mm-YYYY`

e.g. `{GET} /api/v1/donations?date_from=YYYY-mm-dd&date_to=YYYY-mm-dd`

Use `campaign_name` filter to filter donations by campaign name. This is the Donorbox campaign title that you have defined in Donorbox.

e.g. `{GET} /api/v1/donations?campaign_name=XXXXXXX`

Use `campaign_id` filter to filter donations by campaign id. This is the Donorbox campaign id.

e.g. `{GET} /api/v1/donations?campaign_id=XXXX`

Use `id` filter to filter donations by Donorbox donation id. This is the Donorbox generated donation id.

e.g. `{GET} /api/v1/donations?id=XXX`

Use `first_name` filter to filter and get donations by donor's first name.

e.g. `{GET} /api/v1/donations?first_name=XXXXXXX`

Use `last_name` filter to filter and get donations by donor's last name.

e.g. `{GET} /api/v1/donations?last_name=XXXXXXX`

Use `donor_id` filter to filter and get donations by donor's id. This is the Donorbox generated donor id

e.g. `{GET} /api/v1/donations?donor_id=XXXXXXX`

Use `amount` filter to filter and get donations by donation amounts.

e.g. `{GET} /api/v1/donations?amount[usd][min]=XXX&amount[usd][max]=YYYY`

Please note that you can use min and max together to fetch donations in a certain range. You can also use min and max params alone if you want to fetch all the donations above or below a certain threshold.


### Ticket filters

Use `payment_status=refunded` to fetch only refunded tickets.

e.g. `{GET} /api/v1/tickets?payment_status=refunded`

### Purchase filters

Use `payment_status` to filter purchases by payment status. Valid values are `succeeded`, `pending`, `failed`, and `refunded`. It defaults to `succeeded` if any invalid value is passed.

e.g. `{GET} /api/v1/purchases?payment_status=refunded`


### Ordering
All Donorbox API endpoints support ordering. Use `order` parameter with `asc|desc` possible values. The default is `desc`.

e.g `{GET} /api/v1/donations?order=asc`


### Pagination
All Donorbox API endpoints support pagination. Provide `page` and `per_page` parameters to split the result accordingly. The default page size (`per_page` parameter's value) is 50, maximum 100 allowed. If it exceeds the maximum, it will fallback to default.

e.g. `{GET} /api/v1/donors?page=2&per_page=18`


#### Combine filters

Of course, you can combine any of the filters described above, taking into account supported endpoints for a specific filter.

e.g. `{GET} /api/v1/donations?order=asc&page=3&per_page=20&campaign_id=XX&&amount[usd][max]=YYYY`

