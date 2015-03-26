Coupon
================



Example of a Coupons
------------


| ![img1](https://raw.githubusercontent.com/passworks/passworks-api/master/v1/assets/images/coupon/coupon_2x.png) | ![img2](https://raw.githubusercontent.com/passworks/passworks-api/master/v1/assets/images/coupon/paw_planet_coupon_guidelines.png) |
|---|---|
| Generic Coupon Schematic | Paw Planet Coupon |



Creating a Coupon "Campaign" for "Paw Planet" Store
------------

```shell
POST /v1/coupons/
```

Payload

```json
{
  "coupon": {
    "name": "Paw Planet",
    "icon_id": "cecd7470-2ba8-4737-afe0-30d0cd4fd00c",
    "barcode": "pdf417",
    "locations": [
      {
        "longitude": -122.3748889,
        "latitude": 37.6189722
      }
    ],
    "logo_text": "Paw Planet",
    "description": "20% off premium dog food",
    "foreground_color": "#ffffff",
    "background_color": "#ce8c46",
    "primary_fields": [
      {
        "key": "offer",
        "label": "Any premium dog food",
        "value": "20% off"
      }
    ],
    "auxiliary_fields": [
      {
        "key": "expires",
        "label": "EXPIRES",
        "value": "2 weeks"
      }
    ]
  }
}
```

Response:

```json
{
  "name": "Paw Planet",
  "icon_id": "cecd7470-2ba8-4737-afe0-30d0cd4fd00c",
  "template_id": "53403cc6-8d42-4e81-a422-05f0d99feade",
  "barcode": "pdf417",
  "locations": [
    {
      "longitude": -122.3748889,
      "latitude": 37.6189722
    }
  ],
  "logo_text": "Paw Planet",
  "description": "20% off premium dog food",
  "foreground_color": "#ffffff",
  "background_color": "#ce8c46",
  "primary_fields": [
    {
      "key": "offer",
      "label": "Any premium dog food",
      "value": "20% off"
    }
  ],
  "auxiliary_fields": [
    {
      "key": "expires",
      "label": "EXPIRES",
      "value": "2 weeks"
    }
  ]
}
```


##### Available fields

|  Field name  | Type | Description  |
|-------------|------|-----------------------------------
| name | string | Required. Must be unique, it's used to identify the Event Ticket "Campaign"
| description | string | Optional. Brief description of the pass, used by the iOS accessibility technologies. If the description is not provided the *name* field value is used instead.
| icon_id | uuid | Required. Icon  id (the id of a icon type asset)
| logo_id | uuid | Optional. Logo image id (the id of a logo type asset)
| strip_id | uuid | Optional. Strip image id (the id of a logo type asset)
| logo_text | string | Optional. Top card text
| header_fields | array | Optional. Collection of *field hash objects*
| secondary_fields | array | Optional. Collection of *field hash objects*
| auxiliary_fields | array | Optional. Collection of *field hash objects*
| back_fields | array | Optional. Collection of *field hash objects* used in the rear part of the pass
| locations | array | Optional. Collection of up to 10 [location hash objects](#location-hash-object-format)
| beacons | array | Optional. Collection of up to 10 [beacon hash objects](#ibeacon-hash-object-format)
| background_color| rgb string | Optional. Color defining the pass background color ranging from `#00000` to `#ffffff`
| text_color | rgb string | Optional. The text color for all the `value` fields except primary_fields, ranging from `#00000` to `#ffffff`
| label_color | rgb string | Optional. The text color for all `label` fields except primary_fields, ranging from `#00000` to `#ffffff`
| certificate_id | uuid | Optional. **You should provide your own certificate** but in none is provided the passworks.io default certificate is used.
| organization_name | string | Optional. Organization name showned in the unlock screen, if none is supplied the registration organization name is used



Creating a Coupon
------------

The "Paw Planet" coupon is so simple that issuing a new one is only passing the barcode redeem code.


```shell
POST /v1/coupons/{coupon_id}/passes
```

POST Content

```json
{
  "pass": {
  	"barcode": {
  		"message": "redeem token"
  	}
  }
}
```

In case of success HTTP 201 response code is returned with the following body content:

```json
{
  "id": "d920fcae-8237-4071-9685-53f7886e821b",
  "coupon_id": "7cd1dbb7-7540-4dc7-b4ae-1f553f3bbf3c",
  "voided": false,
  "authentication_token": "F0u23SVrG_pgkEXr5tC68g",
  "serial_number": "a5f44994-7457-4b00-8448-e862a51ece3d",
  "header_fields": [],
  "primary_fields": [
    {
      "key": "offer",
      "label": "Any premium dog food",
      "value": "20% off"
    }
  ],
  "secondary_fields": [],
  "auxiliary_fields": [
    {
      "key": "expires",
      "label": "EXPIRES",
      "value": "2 weeks"
    }
  ],
  "back_fields": [],
  "barcode": {
    "format": "qrcode",
    "message": "0000001",
    "alt_text": "0000001"
  },
  "beacons": [],
  "locations": [
    {
      "altitude": null,
      "latitude": 37.6189722,
      "longitude": -122.3748889,
      "relevant_text": null
    }
  ],
  "redeemed_count": 0,
  "download_page_link": "https://get.passworks.io:3000/p5QtGY8a4Q/gMV5Lil2OG0DtwQDTdI1aA",
  "direct_link": "https://get.get.passworks.io:3000/p5QtGY8a4Q/gMV5Lil2OG0DtwQDTdI1aA.pkpass",
  "expiration_date": null,
  "redeemed_at": null,
  "created_at": "2014-09-26T17:33:11Z",
  "updated_at": "2014-09-26T17:33:11Z"
}
```

Updating the coupon
------------

Imagine that in the last week the offer changes from 20% to 30%, and the expiration date changes to 1 week.

```shell
PATCH /v1/coupons/{coupon_id}/passes/{pass_id}
```

POST Content

```json
{
  "pass": {
        "primary_fields": [
            {
                "key": "offer",
                "value": "30% off"
            }
        ],
        "auxiliary_fields": [
            {
                "key": "expires",
                "value": "1 week"
            }
        ]
  }
}
```

Response:

```json
{
  "id": "d920fcae-8237-4071-9685-53f7886e821b",
  "coupon_id": "7cd1dbb7-7540-4dc7-b4ae-1f553f3bbf3c",
  "voided": false,
  "authentication_token": "F0u23SVrG_pgkEXr5tC68g",
  "serial_number": "a5f44994-7457-4b00-8448-e862a51ece3d",
  "header_fields": [],
  "primary_fields": [
    {
      "key": "offer",
      "label": "Any premium dog food",
      "value": "30% off"
    }
  ],
  "secondary_fields": [],
  "auxiliary_fields": [
    {
      "key": "expires",
      "label": "EXPIRES",
      "value": "1 week"
    }
  ],
  "back_fields": [],
  "barcode": {
    "format": "qrcode",
    "message": "0000001",
    "alt_text": "0000001"
  },
  "beacons": [],
  "locations": [
    {
      "altitude": null,
      "latitude": 37.6189722,
      "longitude": -122.3748889,
      "relevant_text": null
    }
  ],
  "redeemed_count": 0,
  "download_page_link": "http://get.passworks.io/p5QtGY8a4Q/gMV5Lil2OG0DtwQDTdI1aA",
  "direct_link": "http://get.passworks.io/p5QtGY8a4Q/gMV5Lil2OG0DtwQDTdI1aA.pkpass",
  "expiration_date": null,
  "redeemed_at": null,
  "created_at": "2014-09-26T17:33:11Z",
  "updated_at": "2014-09-26T17:42:18Z"
}
```

Deleting a coupon
----------------

```shell
DELETE /v1/coupons/{coupon_id}/passes/{pass_id}
```

If the coupon is deleted successfully the endpoint returns a HTTP 200.


Sending a push notification (or forcing a pass update)
------------

You can force the retrivel of an pass via push notification by simply calling the following URL:

```shell
POST /v1/event_tickets/{event_ticket_id}/passes/{pass_id}/push
```

You can also send a custom message that will be displayed in the lock screen via push notification sending the following content in the above request

```json
	{ "push_message": "Hello!" }
```