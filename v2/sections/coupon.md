# Coupon

Coupons can be used to offer customers a discount or promotion, or as a general proximity marketing asset.


## Example of a Coupon

> Attention: please check our
> [Android Pay](https://github.com/passworks/passworks-api/blob/master/v2/sections/android_pay.md)
> documentation for details about the rendering on the Android Pay app.

| ![img1](https://raw.githubusercontent.com/passworks/passworks-api/master/v2/assets/images/coupon/coupon_2x.png) | ![img2](https://raw.githubusercontent.com/passworks/passworks-api/master/v2/assets/images/coupon/paw_planet_coupon_guidelines.png) |
|---|---|
| Generic Coupon Schematic | Paw Planet Coupon |


## Creating a Coupon Campaign for "Paw Planet" Store

We are going to assume that Paw Planet is going to use sequencial barcodes, in this case each barcode numbering will be unique and is going to start from 1 to "unlimited".

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

From the "create coupon" campaign request we get the following response.

The `code_type` indicates the type of numbering that is going to be applied to the barcode, in this case we will be using "sequential"

```json
{
  "id": "a2d82801-e0f7-490e-b06d-548ec26e7c97",
  "name": "Paw Planet",
  "template_id": "24a97b3b-bd00-49c8-9663-e4c0504228fc",
  "organization_name": "Paw Planet, Inc",
  "gwallet_usage": null,
  "gwallet_status": null,
  "gwallet_message": null,
  "barcode": {
    "format": "pdf417",
    "message": "",
    "alt_text": "",
    "alt_text_type": "mirror"
  },
  "barcodes": [],
  "allow_multiple_redeems": false,
  "header_fields": [],
  "primary_fields": [
    {
      "key": "offer",
      "value": "20% off",
      "label": "Any premium dog food",
      "behaviour": "fixed"
    }
  ],
  "secondary_fields": [],
  "auxiliary_fields": [
    {
      "key": "expires",
      "value": "2 weeks",
      "label": "EXPIRES",
      "behaviour": "fixed"
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
  "expiration_date": null,
  "code_type": "sequencial",
  "code_fixed_value": null,
  "created_at": "2016-07-15T09:49:12Z",
  "updated_at": "2016-07-15T09:49:12Z",
  "distributions": [
    {
      "id": "91d464ab-1eb2-475e-b70c-e45719b5de01",
      "distribution_type": "downloadPage",
      "state": "published",
      "page_url": "https://passworks.io/p/5QodxK8VcA",
      "pkpass_url": "https://passworks.io/p/5QodxK8VcA.pkpass",
      "preview_url": "https://passworks.io/p/5QodxK8VcA.png",
      "created_at": "2016-07-15T09:49:12.241Z",
      "updated_at": "2016-07-15T09:49:12.365Z",
      "published_at": "2016-07-15T09:49:12.374Z"
    }
  ]
}
```


### Presentation fields (when template_id is not supplied)

|  Field name  | Type | Description  |
|-------------|------|-----------------------------------
| icon_id | uuid | Required. Icon  id (the id of a icon type asset)
| logo_id | uuid | Optional. Logo image id (the id of a logo type asset)
| strip_id | uuid | Optional. Strip image id (the id of a logo type asset)
| thumbnail_id | uuid | Optional. Strip image id (the id of a logo type asset)
| logo_text | string | Optional. Top card text
| background_color| rgb string | Optional. Color defining the pass background color ranging from `#00000` to `#ffffff`
| text_color | rgb string | Optional. The text color for all the `value` fields except primary_fields, ranging from `#00000` to `#ffffff`
| label_color | rgb string | Optional. The text color for all `label` fields except primary_fields, ranging from `#00000` to `#ffffff`


### Available fields

|  Field name  | Type | Description  |
|-------------|------|-----------------------------------
| name | string | Required. Must be unique, it's used to identify the Event Ticket "Campaign"
| description | string | Optional. Brief description of the pass, used by the iOS accessibility technologies. If the description is not provided the *name* field value is used instead.
| template_id | uuid | Optional. If not supplied, you **must supply the presentation fields presented in the table above!**
| barcode | hash | Optional. A single hash of [barcode hash object](#barcode-hash-object-format).
| header_fields | array | Optional. Collection of *field hash objects*
| secondary_fields | array | Optional. Collection of *field hash objects*
| auxiliary_fields | array | Optional. Collection of *field hash objects*
| back_fields | array | Optional. Collection of *field hash objects* used in the rear part of the pass
| locations | array | Optional. Collection of up to 10 [location hash objects](#location-hash-object-format)
| beacons | array | Optional. Collection of up to 10 [beacon hash objects](#ibeacon-hash-object-format)
| certificate_id | uuid | Optional. **You should provide your own certificate** but in none is provided the passworks.io default certificate is used.
| organization_name | string | Optional. Organization name showned in the unlock screen, if none is supplied the registration organization name is used
| associated_store_identifiers | array | Optional. A list of iTunes Store item identifiers for the associated apps. Only one item in the list is used - the first item identifier for an app compatible with the current device. If the app is not installed, the link opens the App Store and shows the app. If the app is already installed, the link launches the app, [as specified in passbook's documentation](https://developer.apple.com/library/ios/documentation/UserExperience/Reference/PassKit_Bundle/Chapters/TopLevel.html#//apple_ref/doc/uid/TP40012026-CH2-SW7)
| gwallet_usage | boolean | Optional. Activate *Android Pay* for the campaign. Check the [Android Pay](https://github.com/passworks/passworks-api/blob/master/v2/sections/android_pay.md)  for detailed information.
| code_type | string | Optional. By default is sequential. Check the available code_types and their meaning.
| code_fixed_value | string | Optional, default: null


### Code Type (code_type)

|  code_type  | Description  |
|--------------|----------------|
| sequencial | This means that each issued pass will be assign unique and sequencial (sequential) number starting from number 1. eg: 1, 2, 3 ... |
| fixed | For all issued passes use the value inside the `code_fixed_value` attribute as the barcode message |
| list  | Not used in the API for now. |
| per_pass | This means that per pass creation request you need to supply the barcode message that will be used |


### Field hash object format

```json
{
  "key": "name",
  "value": "2 weeks",
  "label": "EXPIRES",
  "behaviour": "fixed"
}
```

|  Field name  | Type |  Description  |
|--------------|------|----------------|
key  | string | Required. A reference key, it must be unique for a campaign.
value  | string | Required. The field's value
label | string | Required. The field's label
behaviour | string | Optional, Options: __fixed__ or __dynamic__. When not set, use __fixed__ as default


#### Understanding behaviour fields (fixed vs dynamic content)

The presentation fields (`primary_fields`, `secondary_fields`, `auxiliary_fields` and `back_fields`) have a `behaviour` attribute. This attribute can have one of two values: `fixed` or `dynamic` _(by default the `behaviour` is set to `fixed`)_.

- fixed

  `fixed` means that the value is `static`: every pass will have the same `label` and `value` for this field.
  So when you call the  `merge` method in the Ruby client this field will be added or overriden (if the field with the same `key` exists) in every pass even if you had previously customized the value per pass. Don't use the type of field for custom fields in your passes eg: __name__, __client id__, __ticket number__ ,etc. This type of _behaviour_ is a good fit for fields that are the same across all passes eg: `event date`, `event location`, `flight number`, etc.

- dynamic

  The `dynamic` _behaviour_ defines the field as a custom updated field that shouldn't be updated on a bulk update when the `merge` method is called.
  This field will only be updated when the user updates that field specifically for that pass. This type of _behaviour_ is a good fit for custom fields like `ticket number`, `user name`, `boarding number`, `seat number`, etc..

### Location hash object format

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


### Beacon hash object format

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

### Barcode hash object format

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
format | string | Optional. Must be one of the following if supplied: **qrcode**, **pdf417**, **aztec**, **ean128** or **none**. | qrcode
message | string | Optional. Message encoded in the barcode. | Pass's redeem code.



## Updating the "Paw Planet" Coupon Campaign

Sometimes you might want to run a special campaign, and update all of your client's passes with the new conditions:

```shell
PATCH /v2/coupons/{campaign_id}
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
  "organization_name": "your company",
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
  "page_url": "http://get.passworks.io/I5dPyf_j2Q",
  "created_at": "2015-03-31T18:01:44Z",
  "updated_at": "2015-03-31T18:22:50Z"
}

```

Now that you've updated your campaign, all the future passes generated from this updated campaign will contain the new changes.

**NOTE:** The following instructions will reset all the issued passes to the base template, removing the personalization fields from all the issued passes.

The correct way of updating the already issued passes while preserving the custom fields (like the name of the pass owner, for example) is to iterate trough the issued pass collection, by collecting the ids from
`GET /v2/coupons/{campaign_id}/passes`

and then [updating each pass](#updating-each-pass) with the fields you wish to change.

Please contact support@passworks.io for advisement on updating a coupon campaign.

If, however any old passes that had already been generated and you wish to reset them to the new changes, you **must**, following a campaign update, issue a push POST request:

```shell
POST /v2/coupons/{campaign_id}/push
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


## Creating a "Paw Planet" Coupon Pass

You can create a boilerplate pass simply by POSTing to the passes route:

```shell
POST /v2/coupons/{campaign_id}/passes
```

If you want to personalize the pass you can supply an hash with the parameters you want to override:


```shell
POST /v2/coupons/{campaign_id}/passes/
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
  "page_url": "http://get.passworks.io/I5dPyf_j2Q/-zGkMq8orhAE1x9l08yLCQ",
  "pkpass_url": "http://get.passworks.io/I5dPyf_j2Q/-zGkMq8orhAE1x9l08yLCQ.pkpass",
  "created_at": "2015-03-31T18:25:20Z",
  "updated_at": "2015-03-31T18:25:20Z"
}
```


## Updating a "The Beat Goes On" Coupon Pass

Imagine that you want to offer a special campaign to your top customer, you can offer a promotion to a specific client, by updating his pass.

```shell
PATCH /v2/coupons/{campaign_id}/passes/{pass_id}
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
  "page_url": "http://get.passworks.io/I5dPyf_j2Q/-zGkMq8orhAE1x9l08yLCQ",
  "pkpass_url": "http://get.passworks.io/I5dPyf_j2Q/-zGkMq8orhAE1x9l08yLCQ.pkpass",
  "created_at": "2015-03-31T18:25:20Z",
  "updated_at": "2015-03-31T18:29:04Z"
}
```


## Forcing a push update of a pass

You can force the update of a pass via push notification by simply calling the following URL:

```shell
POST /v2/coupon/{campaign_id}/passes/{pass_id}/push
```

You can also send a custom message that will be displayed in the lock screen via push notification sending the following content in the above request

```json
{
  "pass": {
      "push_message": "Special offer just for you!"
  }
}
```


## Redeeming a pass

There are two ways you can redeem a pass:

- Redeeming a pass by referencing a redeem code
	You can redeem a pass by referencing a redeem code (instead of the pass_id) by POSTing to the campaign `redeem` route

	```shell
	/v2/coupons/{campaign_id}/redeem
	```
	Issuing a payload with a root element `pass` and with the redeem code in the payload:

	```json
	{
		"pass": {
			"redeem_code": "0000001",
			"comment": "Redeemed in store"
		}
	}
	```
	The method accepts an optional `comment` key where you can specify some information you want to be stored for reference.


- Redeem a pass directly
	You can redeem a pass directly, by POSTing to the pass `redeem` route:

	```shell
	POST /v2/coupons/{campaign_id}/passes/{pass_id}/redeem
	```

	You can supply an optional `comment` key where you can specify some information you want to be stored for reference:

	```json
	{
		"pass": {
			"comment": "redeemed in store"
		}
	}
	```

## Aditional routes available

### Get all the Coupon campaigns:
```shell
GET /v2/coupons/
```

### Get all the passes for a specific Coupon campaign:
```shell
GET /v2/coupons/{campaign_id}/passes
```

### Get a pass's id from its redeem code
```shell
GET /v2/coupons/{campaign_id}/redeem/{redeem_code}
```

### Reports
```shell
GET /v2/coupons/{campaign_id}/reports
```

```shell
GET /v2/coupons/{campaign_id}/reports/totals
```

For more information about the campaign reports, please check our [Reports Documentation](https://github.com/passworks/passworks-api/blob/master/v2/sections/reports.md).
