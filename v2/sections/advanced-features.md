Advanced Features
===============

## Setting up a campaign with a remote\_form\_url

When creating a campaign using one of the existing endpoints, eg: `coupons`, `event_tickets`, `generics` just append the `remote_form_url` parameter to your already existing campaign fields.

See the following example where we will be adding `remote_form_url` attribute with the value **http://example.org**.

### Example

```
POST http://api.passworks.io/v2/coupons/
```
Payload:

```
{
    "coupon": {
        "name": "Remote Form URL Example",
        "template_id": "af61b02d-a89d-4159-8f76-a39c07e5ad4c",
        "remote_form_url": "http://example.org"
    }
}
```

Response:

```
{
  "id": "695b0903-5cb6-4a19-b835-f5d074347f5c",
  "name": "Remote Form URL Example",
  "template_id": "af61b02d-a89d-4159-8f76-a39c07e5ad4c",
  "organization_name": "Luis",
  "barcode": {
    "format": "none",
    "message": "",
    "alt_text": "",
    "alt_text_type": "mirror"
  },
  "render_on_short_url": false,
  "remote_form_url": "http://example.org",
  "created_at": "2016-08-29T14:07:08Z",
  "updated_at": "2016-08-29T14:07:08Z",
  "distributions": [
    {
      "id": "3803869e-9302-4197-a57f-9cb1d3cd405c",
      "distribution_type": "downloadPage",
      "state": "published",
      "page_url": "https://passworks.io/p/PlOKQOhqCg",
      "pkpass_url": "https://passworks.io/p/PlOKQOhqCg.pkpass",
      "preview_url": "https://passworks.io/p/PlOKQOhqCg.png",
      "page_short_url": "https://pass.yt:3000/d/Xr",
      "pkpass_short_url": "http://passs.ly:3000/d/Xr.pkpass",
      "preview_short_url": "http://passs.ly:3000/d/Xr.png",
      "created_at": "2016-08-29T14:07:08.888Z",
      "updated_at": "2016-08-29T14:07:09.010Z",
      "published_at": "2016-08-29T14:07:09.015Z"
    }
  ]
}
```

In the response you can see a `remote_form_url` attribute with the value **http://example.org** as expected.

When redirecting Passworks platform will append a query parameter called campaign_id to the end of the URL turning **http://example.org** in to **http://example.org?campaign_id=<campaign_id>**

So in this case when the user is redirected to the `remote_form_url` the url used will be **http://example.org?campaign_id=695b0903-5cb6-4a19-b835-f5d074347f5c** (NOTE: The redirect is always a GET request).




## Fetching the campaign fields

You can grab the campaign fields calling the `fields` method of the `remote_forms` endpoint and passing as a argument the `campaign_id`.

The `campaign_id` is the ID of a any kind of campaign, eg: `coupon`, `event_ticket`, `boarding_pass`, etc..

```
GET http://api.passworks.io/v2/remote_forms/<campaign_id>/fields
```

The response will always be a hash containing 3 top level keys: `fields`, `dynamic_fields_keys`, `static_fields_keys`

| Key name | Type | Description |
|----------|------|-------------|
| fields   | Hash | Hash of all available campaign fields, static or dynamic, the key of each field is also the key of the hash |
| dynamic\_fields\_keys | Array | The keys of all the dynamic fields |
| static\_fields\_keys | Array | The keys of all static fields |


### Example

Requesting the fields of the campaign `f1eb7fba-392b-489c-a0dd-8bf8892ce349` :

```
http://api.passworks.io/v2/remote_forms/f1eb7fba-392b-489c-a0dd-8bf8892ce349/fields
```

The response

```
{
  "fields": {
    "name": {
      "key": "name",
      "label": "Name",
      "value": "name",
      "behaviour": "dynamic"
    },
    "age": {
      "key": "age",
      "label": "Age",
      "value": "",
      "behaviour": "dynamic"
    },
    "location": {
      "key": "location",
      "label": "Location",
      "value": "Av da Liberdade",
      "behaviour": "fixed"
    }
  },
  "dynamic_fields_keys": [
    "name",
    "age"
  ],
  "static_fields_keys": [
    "location"
  ]
}
```

## Posting the form

Creating a new pass by submiting the dynamic fields is easy, just call the `submit` method of the `remote_forms` endpoint with the `dynamic fields` in the body.

```
POST http://api.passworks.io/v2/remote_forms/<campaign_id>/submit
```

## Example

Let's submit the `age` and `name` values using our endpoint, let's assume that the campaign_id is `f1eb7fba-392b-489c-a0dd-8bf8892ce349`

> NOTE: If you supply a `beacons` and/or `locations` array of hashes the beacons and locations will be merged with the pass (overriding any default  `beacons` or `locations` already defined in the campaign).

```
POST http://api.passworks.io/v2/remote_forms/f1eb7fba-392b-489c-a0dd-8bf8892ce349/submit
```

With the following payload:

```
{
    "name": "Kermit the Frog",
    "age": "61",
    "beacons": [
        {
            "proximity_uuid": "ec961b5b-9a63-4eb5-9463-c19bd5aca7ba",
            "major": 1,
            "minor": 1,
            "relevant_text": "Elmo"
        },
        {
            "proximity_uuid": "ec961b5b-9a63-4eb5-9463-c19bd5aca7ba",
            "major": 2,
            "minor": 2,
            "relevant_text": "Big Bird"
        }
    ],
    "locations": [
        {
            "latitude": "38.707739",
            "longitude": "-9.147581",
            "relevant_text": "Grover"
        }    
    ]
}
```

Calling the above endpoint will result in the following answer: (just redirect the user to `page_short_url` from the response).

```
{
  "id": "175d218e-88fb-4af1-afb8-86512dccf9fb",
  "campaign_id": "f1eb7fba-392b-489c-a0dd-8bf8892ce349",
  "voided": false,
  "serial_number": "b3cafaa7-e180-42e0-813f-3025a5be56f2",
  "redeem_code": "00000027",
  "redeemed_count": 0,
  "barcode": {
    "format": "none",
    "message": "",
    "alt_text": "",
    "alt_text_type": "mirror"
  },
  "barcodes": [
    {
      "format": "none",
      "message": "",
      "alt_text": "",
      "alt_text_type": "mirror"
    }
  ],
  "expiration_date": "2016-08-09T14:30:54.000+00:00",
  "max_distance": 30,
  "relevant_date": null,
  "header_fields": [],
  "primary_fields": [],
  "secondary_fields": [
    {
      "key": "name",
      "value": "Kermit the Frog",
      "label": "Name",
      "behaviour": "dynamic"
    },
    {
      "key": "age",
      "value": "61",
      "label": "Age",
      "behaviour": "dynamic"
    }
  ],
  "auxiliary_fields": [],
  "back_fields": [
    {
      "key": "location",
      "value": "Av da Liberdade",
      "label": "Location",
      "behaviour": "fixed"
    }
  ],
  "locations": [
    {
      "name": null,
      "altitude": null,
      "latitude": 38.707739,
      "longitude": -9.147581,
      "relevant_text": "Grover"
    }
  ],
  "beacons": [
    {
      "major": 1,
      "minor": 1,
      "proximity_uuid": "ec961b5b-9a63-4eb5-9463-c19bd5aca7ba",
      "relevant_text": "Elmo"
    },
    {
      "major": 2,
      "minor": 2,
      "proximity_uuid": "ec961b5b-9a63-4eb5-9463-c19bd5aca7ba",
      "relevant_text": "Big Bird"
    }
  ],
  "page_url": "https://passworks.io/p/ZpCCm1MEGA/ff2oP4iHmEQ2p60rQxxWlw",
  "pkpass_url": "https://passworks.io/p/ZpCCm1MEGA/ff2oP4iHmEQ2p60rQxxWlw.pkpass",
  "page_short_url": "http://pass.ly/p/Wr",
  "pkpass_short_url": "http://pass.ly/p/Wr.pkpass",
  "created_at": "2016-08-29T15:25:15Z",
  "updated_at": "2016-08-29T15:25:16Z"
}
```

## Custom barcode

If you wish to specify a custom barcode, make sure that your campaign's "code_type" attribute is set to `per_pass` and when submiting the form just submit the `barcodes` array with the barcode formats that you wish to support, eg:

```
{
    "barcodes": [
        {
            format: "qrcode",
            message: "123456"
        },
        {
            format: "aztec",
            message: "123456"
        }        
    ]
}
```

Use the same message content for all types of barcodes that you support.
