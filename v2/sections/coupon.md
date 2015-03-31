Coupon
================


Coupons can be used to offer customers a discount or promotion, or as a general proximity marketing asset.


Example of a Coupon
------------


| ![img1](https://raw.githubusercontent.com/passworks/passworks-api/master/v2/assets/images/coupon/coupon_2x.png) | ![img2](https://raw.githubusercontent.com/passworks/passworks-api/master/v2/assets/images/coupon/paw_planet_coupon_guidelines.png) |
|---|---|
| Generic Coupon Schematic | Paw Planet Coupon |



Creating a Coupon Campaign for "Paw Planet" Store
------------

```shell
POST /v2/coupons/
```

Payload

```json
{
  "coupon": {
    "name": "Paw Planet",
    "icon_id": "ffe0d88f-916d-4a12-8244-9ecd0178ca45",
    "barcode": {
      "format": "pdf417"
    },
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
  "id": "5fd663d1-4ed4-4800-8d5a-caea4131358a",
  "name": "Paw Planetz",
  "template_id": "9bd46ecb-20c8-41cb-a8d8-f848a07c220c",
  "organization_name": "foobar",
  "barcode": {
    "format": "pdf417",
    "message": "",
    "alt_text": ""
  },
  "allow_multiple_redeems": false,
  "header_fields": [],
  "primary_fields": [
    {
      "key": "offer",
      "value": "20% off",
      "label": "Any premium dog food"
    }
  ],
  "secondary_fields": [],
  "auxiliary_fields": [
    {
      "key": "expires",
      "value": "2 weeks",
      "label": "EXPIRES"
    }
  ],
  "back_fields": [],
  "locations": [
    {
      "latitude": 37.6189722,
      "longitude": -122.3748889,
      "altitude": null,
      "relevant_text": null
    }
  ],
  "beacons": [],
  "page_url": "http://get.192.168.1.67.xip.io:3000/I5dPyf_j2Q",
  "created_at": "2015-03-31T18:01:44Z",
  "updated_at": "2015-03-31T18:01:45Z"
}
```


##### Presentation fields (when template_id is not supplied)

|  Field name  | Type | Description  |
|-------------|------|-----------------------------------
| icon_id | uuid | Required. Icon  id (the id of a icon type asset)
| logo_id | uuid | Optional. Logo image id (the id of a logo type asset)
| strip_id | uuid | Optional. Strip image id (the id of a logo type asset)
| logo_text | string | Optional. Top card text
| background_color| rgb string | Optional. Color defining the pass background color ranging from `#00000` to `#ffffff`
| text_color | rgb string | Optional. The text color for all the `value` fields except primary_fields, ranging from `#00000` to `#ffffff`
| label_color | rgb string | Optional. The text color for all `label` fields except primary_fields, ranging from `#00000` to `#ffffff`
| barcode | hash | Optional. A single hash of [barcode hash object](#barcode-hash-object-format).


##### Available fields

|  Field name  | Type | Description  |
|-------------|------|-----------------------------------
| name | string | Required. Must be unique, it's used to identify the Event Ticket "Campaign"
| description | string | Optional. Brief description of the pass, used by the iOS accessibility technologies. If the description is not provided the *name* field value is used instead.
| template_id | uuid | Optional. If not supplied, you **must supply the presentation fields presented in the table above!**
| header_fields | array | Optional. Collection of *field hash objects*
| secondary_fields | array | Optional. Collection of *field hash objects*
| auxiliary_fields | array | Optional. Collection of *field hash objects*
| back_fields | array | Optional. Collection of *field hash objects* used in the rear part of the pass
| locations | array | Optional. Collection of up to 10 [location hash objects](#location-hash-object-format)
| beacons | array | Optional. Collection of up to 10 [beacon hash objects](#ibeacon-hash-object-format)
| certificate_id | uuid | Optional. **You should provide your own certificate** but in none is provided the passworks.io default certificate is used.
| organization_name | string | Optional. Organization name showned in the unlock screen, if none is supplied the registration organization name is used
| associated_store_identifiers | array | Optional. A list of iTunes Store item identifiers for the associated apps. Only one item in the list is used - the first item identifier for an app compatible with the current device. If the app is not installed, the link opens the App Store and shows the app. If the app is already installed, the link launches the app, [as specified in passbook's documentation](https://developer.apple.com/library/ios/documentation/UserExperience/Reference/PassKit_Bundle/Chapters/TopLevel.html#//apple_ref/doc/uid/TP40012026-CH2-SW7)


##### Location hash object format

```json
{
  "altitude": 0.0,
  "latitude": 0.0,
  "longitude": 0.0,
  "relevant_text": "notification to display"
}
```
|  Field name  | Type |  Description  |
|--------------|------|----------------|
altitude  | double | Optional. Altitude, in meters, of the location.
latitude  | double | Required. Latitude, in degrees, of the location.
longitude | double | Required. Longitude, in degrees, of the location.
relevant_text | string | Optional. Text displayed on the lock screen when the pass is currently relevant. For example, a description of the nearby location such as “Store nearby on 1st and Main.”


##### Beacon hash object format

```json
{
  "major": 0.0,
  "minor": 0.0,
  "proximity_uuid": "30b5d792-48c9-4f12-80ff-082cae62e80f",
  "relevant_text": "notification to display"
}
```
|  Field name  | Type |  Description  |
|--------------|------|----------------|
major| 16-bit unsigned integer | Optional. Major identifier of a Bluetooth Low Energy location beacon
minor| 16-bit unsigned integer | Optional. Minor identifier of a Bluetooth Low Energy location beacon
proximity_uuid| string | Required. Unique identifier of a Bluetooth Low Energy location beacon
relevant_text| string | Optional. Text displayed on the lock screen when the pass is currently relevant. For example, a description of the nearby

##### Barcode hash object format

```json
{
  "alt_text": "Text shown below the barcode.",
  "format": "pdf417",
  "message": "Message encoded in the barcode."
}
```

|  Field name  | Type |  Description   | Default |
|--------------|------|----------------|---------|
alt_text | string | Optional. Text shown below the barcode. | Pass's redeem code.
format | string | Optional. Must be one of the following if supplied: **qrcode**, **pdf417**, **aztec**, or **none**. | qrcode
message | string | Optional. Message encoded in the barcode. | Pass's redeem code.


Updating the "The Beat Goes On" Event Ticket Campaign
------------

Let's imagine that the location of your event changed, and you wish to update all of the campaign's passes. To do so, you will need to issue a PATCH to the following URL with this example payload:

```shell
PATCH /v2/event_tickets/{event_ticket_id}
```


```json
{
	"event_ticket": {
	    "secondary_fields": [
	      {
	        "key": "loc",
	        "label": "LOCATION",
	        "value": "Moscone West"
	      }
	    ],
	    "locations": [
	      {
          	"latitude": 38.725488,
             	"longitude": -9.1501,
             	"relevant_text": "Welcome! Enjoy the show."
	      }
	    ]
	}
}
```

Response:

```json
{
  "id": "c7aab24b-a076-4e59-885a-726e80ca64e7",
  "name": "The Beat Goes On Event",
  "template_id": "19293ad0-9ecf-4e31-9c07-b555cb276d13",
  "organization_name": "onomecompany",
  "header_fields": [],
  "primary_fields": [
    {
      "key": "event_name",
      "value": "The Beat Goes On",
      "label": "EVENT"
    }
  ],
  "secondary_fields": [
    {
      "key": "loc",
      "value": "Moscone West",
      "label": "LOCATION"
    }
  ],
  "auxiliary_fields": [],
  "back_fields": [],
  "locations": [
    {
      "latitude": 38.725488,
      "longitude": -9.1501,
      "altitude": null,
      "relevant_text": "Welcome! Enjoy the show."
    }
  ],
  "beacons": [],
  "page_url": "http://get.192.168.1.67.xip.io:3000/1VtFTG8YwQ",
  "created_at": "2015-03-27T13:08:57Z",
  "updated_at": "2015-03-27T17:49:50Z"
}
```

Now that you've updated your campaign, all the future passes generated from this updated campaign will contain the new changes, however any old passes that had already been generated will need to be explicitly pushed out, so you **must**, following a campaign update, issue a push POST request:



Updating the "Paw Planet" Coupon Campaign
------------

Sometimes you might want to run a special campaign, and update all of your client's passes with the new conditions:

```shell
PATCH /v2/coupons/{coupon_id}
```


```json
{
  "coupon": {
    "primary_fields": [
      {
        "key": "offer",
        "label": "Any cat or dog treats",
        "value": "30% off"
      }
    ],
    "auxiliary_fields": [
      {
        "key": "expires",
        "label": "EXPIRES",
        "value": "3 days"
      }
    ]
  }
}
```

Response:

```json
{
  "id": "5fd663d1-4ed4-4800-8d5a-caea4131358a",
  "name": "Paw Planet",
  "template_id": "9bd46ecb-20c8-41cb-a8d8-f848a07c220c",
  "organization_name": "foobar",
  "barcode": {
    "format": "qrcode",
    "message": "",
    "alt_text": ""
  },
  "allow_multiple_redeems": false,
  "header_fields": [],
  "primary_fields": [
    {
      "key": "offer",
      "value": "30% off",
      "label": "Any cat or dog treats"
    }
  ],
  "secondary_fields": [],
  "auxiliary_fields": [
    {
      "key": "expires",
      "value": "3 days",
      "label": "EXPIRES"
    }
  ],
  "back_fields": [],
  "locations": [
    {
      "latitude": 37.6189722,
      "longitude": -122.3748889,
      "altitude": null,
      "relevant_text": null
    }
  ],
  "beacons": [],
  "page_url": "http://get.192.168.1.67.xip.io:3000/I5dPyf_j2Q",
  "created_at": "2015-03-31T18:01:44Z",
  "updated_at": "2015-03-31T18:22:50Z"
}

```

Now that you've updated your campaign, all the future passes generated from this updated campaign will contain the new changes, however any old passes that had already been generated will need to be explicitly pushed out, so you **must**, following a campaign update, issue a push POST request:

```shell
POST /v2/coupons/{coupon_id}/push
```

Along with this push, you may also, optionally, send in a payload with a push message that will be presented to the users when the update is done, shown on the lock screen.

```json
{
  "coupon": {
      "push_message": "New promotion!"
  }
}
```

|  Field name  | Type |  Description   | Default |
|--------------|------|----------------|---------|
push_message | string | Optional. Text shown on the lock screen. | No message sent.

This request will push all existing passes once again, guaranteeing that all that have been downloaded will contain the new changes. Otherwise, there's no guarantee that the users will receive the updated pass.


Creating a "Paw Planet" Coupon Pass
------------

In order to create passes, you need to issue a POST request to the following URL:

```shell
POST /v2/coupons/{coupon_id}/passes/
```

```json
{
  "pass": {}
}
```

Response:

```json
{
  "id": "2df090c4-c272-41ae-904f-727cfbfbf955",
  "campaign_id": "5fd663d1-4ed4-4800-8d5a-caea4131358a",
  "voided": false,
  "serial_number": "22142563-e452-4cfe-825e-650c05a78a5c",
  "redeem_code": "0000001",
  "redeemed_count": 0,
  "barcode": {
    "format": "qrcode",
    "message": "0000001",
    "alt_text": "0000001"
  },
  "expiration_date": null,
  "max_distance": null,
  "relevant_date": null,
  "header_fields": [],
  "primary_fields": [
    {
      "key": "offer",
      "value": "30% off",
      "label": "Any cat or dog treats"
    }
  ],
  "secondary_fields": [],
  "auxiliary_fields": [
    {
      "key": "expires",
      "value": "3 days",
      "label": "EXPIRES"
    }
  ],
  "back_fields": [],
  "locations": [
    {
      "name": null,
      "altitude": null,
      "latitude": 37.6189722,
      "longitude": -122.3748889,
      "relevant_text": null
    }
  ],
  "beacons": [],
  "page_url": "http://get.192.168.1.67.xip.io:3000/I5dPyf_j2Q/-zGkMq8orhAE1x9l08yLCQ",
  "pkpass_url": "http://get.192.168.1.67.xip.io:3000/I5dPyf_j2Q/-zGkMq8orhAE1x9l08yLCQ.pkpass",
  "created_at": "2015-03-31T18:25:20Z",
  "updated_at": "2015-03-31T18:25:20Z"
}
```

Updating a "The Beat Goes On" Coupon Pass
------------

Imagine that you want to offer a special campaign to your top customer, you can offer a promotion to a specific client, by updating his pass.

```shell
PATCH /v2/coupons/{coupon_id}/passes/{pass_id}
```


```json
{
  "pass": {
    "primary_fields": [
      {
        "key": "offer",
        "label": "Any article in the store",
        "value": "30% off"
      }
    ],
    "auxiliary_fields": [
      {
        "key": "expires",
        "label": "EXPIRES",
        "value": "3 days"
      }
    ]
  }
}
```

Response:

```json
{
  "id": "2df090c4-c272-41ae-904f-727cfbfbf955",
  "campaign_id": "5fd663d1-4ed4-4800-8d5a-caea4131358a",
  "voided": false,
  "serial_number": "22142563-e452-4cfe-825e-650c05a78a5c",
  "redeem_code": "0000001",
  "redeemed_count": 0,
  "barcode": {
    "format": "qrcode",
    "message": "0000001",
    "alt_text": "0000001"
  },
  "expiration_date": null,
  "max_distance": null,
  "relevant_date": null,
  "header_fields": [],
  "primary_fields": [
    {
      "key": "offer",
      "value": "30% off",
      "label": "Any article in the store"
    }
  ],
  "secondary_fields": [],
  "auxiliary_fields": [
    {
      "key": "expires",
      "value": "3 days",
      "label": "EXPIRES"
    }
  ],
  "back_fields": [],
  "locations": [
    {
      "name": null,
      "altitude": null,
      "latitude": 37.6189722,
      "longitude": -122.3748889,
      "relevant_text": null
    }
  ],
  "beacons": [],
  "page_url": "http://get.192.168.1.67.xip.io:3000/I5dPyf_j2Q/-zGkMq8orhAE1x9l08yLCQ",
  "pkpass_url": "http://get.192.168.1.67.xip.io:3000/I5dPyf_j2Q/-zGkMq8orhAE1x9l08yLCQ.pkpass",
  "created_at": "2015-03-31T18:25:20Z",
  "updated_at": "2015-03-31T18:29:04Z"
}
```

Forcing a push update of a pass
------------

You can force the update of a pass via push notification by simply calling the following URL:

```shell
POST /v2/coupon/{coupon_id}/passes/{pass_id}/push
```

You can also send a custom message that will be displayed in the lock screen via push notification sending the following content in the above request

```json
{
  "coupon": {
      "push_message": "Special offer just for you!"
  }
}
```
