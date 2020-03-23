# Store Card

The Passworks API can be used to create loyalty or event tier programs to reward your customers for using your services.


## Example of a Store Card

> Attention: please check our
> [Android Pay](https://github.com/passworks/passworks-api/blob/master/v2/sections/android_pay.md)
> documentation for details about the rendering on the Android Pay app.

| ![img1](https://raw.githubusercontent.com/passworks/passworks-api/master/v2/assets/images/store_card/store_card_2x.png) | ![img2](https://raw.githubusercontent.com/passworks/passworks-api/master/v2/assets/images/store_card/bayroast_coffee_guidelines.png) |
|---|---|
| Generic Loyalty Card Schematic | Bayroast Coffe Loyalty Card |



## Creating a Store Card "campaign" for the "Bayroast Coffee"

```shell
POST /v2/store_cards/
```

POST Content

```json
{
  "store_card": {
    "name": "Bayroast Coffee Store cards",
    "icon_id": "e365088d-27db-4d5e-9915-466d06385426",
    "logo_id": "a798fbf5-033f-4334-99f5-3196751e0595",
    "strip_id": "1f278e8f-7efc-4536-a940-09de39ad8599",
    "logo_text": "Bayroast Coffee esp",
    "background_color": "#764a32",
    "text_color": "#f5f2f0",
    "label_color": "#643e2a",
    "barcode": {
        "format": "pdf417"
    },
    "primary_fields": [
      {
        "key": "balance",
        "label": "$0",
        "value": "remaining balance"
      }
    ],
    "secondary_fields": [
      {
        "key": "level",
        "label": "LEVEL"
      },
      {
        "key": "usual_beverage",
        "label": "THE USUAL"
      }
    ]
  }
}
```

In case of success HTTP 201 response code is returned with the following body content:

```json
{
  "id": "df570ca9-2fd4-462f-8d12-f0882ca38302",
  "name": "Bayroast Coffee Store cards",
  "template_id": "e9e16386-a432-4956-877e-1f5edc999126",
  "organization_name": "your company",
  "barcode": {
    "format": "pdf417",
    "message": "",
    "alt_text": ""
  },
  "header_fields": [],
  "primary_fields": [
    {
      "key": "balance",
      "value": "remaining balance",
      "label": "$0"
    }
  ],
  "secondary_fields": [
    {
      "key": "level",
      "value": null,
      "label": "LEVEL"
    },
    {
      "key": "usual_beverage",
      "value": null,
      "label": "THE USUAL"
    }
  ],
  "auxiliary_fields": [],
  "back_fields": [],
  "locations": [],
  "beacons": [],
  "page_url": "http://get.passworks.io/MqixNhgUdg",
  "gwallet_usage": false,
  "gwallet_status": nil,
  "gwallet_message": nil,
  "created_at": "2015-03-30T11:11:46Z",
  "updated_at": "2015-03-30T11:11:46Z"
}
```

NOTE: The API date fields (e.g `created_at`, `updated_at`) use the [ISO-8601](http://en.wikipedia.org/wiki/ISO_8601) format (e.g:  `2014-09-22T20:51:53+00:00`).


### Presentation fields (when template_id is not supplied)

|  Field name  | Type | Description  |
|-------------|------|-----------------------------------
| icon_id | uuid | Required. Icon  id (the id of a icon type asset)
| logo_id | uuid | Optional. Logo image id (the id of a logo type asset)
| strip_id | uuid | Optional. Strip image id (the id of a logo type asset)
| logo_text | string | Optional. Top card text
| background_color| rgb string | Optional. Color defining the pass background color ranging from `#000000` to `#ffffff`
| text_color | rgb string | Optional. The text color for all the `value` fields except primary_fields, ranging from `#00000` to `#ffffff`
| label_color | rgb string | Optional. The text color for all `label` fields except primary_fields, ranging from `#00000` to `#ffffff`
| barcode | hash | Optional. A single hash of [barcode hash object](#barcode-hash-object-format).


### Available fields

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
| beacons | array | Optional. Collection of up to 10 [beacon hash objects](#beacon-hash-object-format)
| certificate_id | uuid | Optional. **You should provide your own certificate** but in none is provided the passworks.io default certificate is used.
| organization_name | string | Optional. Organization name showned in the unlock screen, if none is supplied the registration organization name is used
| associated\_store\_identifiers | array | Optional. A list of iTunes Store item identifiers for the associated apps. Only one item in the list is used - the first item identifier for an app compatible with the current device. If the app is not installed, the link opens the App Store and shows the app. If the app is already installed, the link launches the app, [as specified in passbook's documentation](https://developer.apple.com/library/ios/documentation/UserExperience/Reference/PassKit_Bundle/Chapters/TopLevel.html#//apple_ref/doc/uid/TP40012026-CH2-SW7)
| og | Boolean | Use Open Graph tags on the download page. Optional, default: true
| og_description | String | Open Graph description. Optional, default: "" (empty string)
| javascript | String | Javascript that will be rendered inside the download page and form, Allows the user to run their own javascript code eg: Google Analytics or Facebook Pixel  |
| stylesheet | String | CSS that will be rendered inside the download page and form, allows users to override the page css |
| user_info | hash | Optional. This field can be used to store user related data. On Apple Wallet this field will be available as a JSON encoded string. |
| remote_form_url | url | Optional. Please see [advanced features](https://github.com/passworks/passworks-api/blob/master/v2/sections/advanced-features.md).  |
| sync_locations_on_merge | boolean | Optional. Default `true`. Allows you to choose if you with that campaign locations are synced or not with the passes when the campaign is updated.|
| sync_beacons_on_merge | boolean | Optional. Default `true`. Allows you to choose if you with that campaign beacons are synced or not with the passes when the campaign is updated.|

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
	"major": 0,
	"minor": 0,
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


## Updating a Store Card "campaign" for the "Bayroast Coffee"

```shell
PATCH /v2/store_cards/{campaign_id}
```

POST Content

```json
{
  "store_card": {
    "primary_fields": [
      {
        "key": "balance",
        "label": "$10",
        "value": "remaining balance"
      }
    ],
    "secondary_fields": [
      {
        "key": "level",
        "label": "1"
      },
      {
        "key": "usual_beverage",
        "label": "NEW BEVERAGE"
      }
    ]
  }
}
```

In case of success HTTP 201 response code is returned with the following body content:

```json
{
  "id": "df570ca9-2fd4-462f-8d12-f0882ca38302",
  "name": "Bayroast Coffee Store cards",
  "template_id": "e9e16386-a432-4956-877e-1f5edc999126",
  "organization_name": "your company",
  "barcode": {
    "format": "pdf417",
    "message": "",
    "alt_text": ""
  },
  "header_fields": [],
  "primary_fields": [
    {
      "key": "balance",
      "value": "remaining balance",
      "label": "$10"
    }
  ],
  "secondary_fields": [
    {
      "key": "level",
      "value": null,
      "label": "1"
    },
    {
      "key": "usual_beverage",
      "value": null,
      "label": "NEW BEVERAGE"
    }
  ],
  "user_info": {},
  "auxiliary_fields": [],
  "back_fields": [],
  "locations": [],
  "beacons": [],
  "page_url": "http://get.passworks.io/MqixNhgUdg",
  "created_at": "2015-03-30T11:11:46Z",
  "updated_at": "2015-03-30T11:11:46Z"
}
```

NOTE: The API date fields (e.g `created_at`, `updated_at`) use the [ISO-8601](http://en.wikipedia.org/wiki/ISO_8601) format (e.g:  `2014-09-22T20:51:53+00:00`).


### Presentation fields (when template_id is not supplied)

|  Field name  | Type | Description  |
|-------------|------|-----------------------------------
| icon_id | uuid | Required. Icon  id (the id of a icon type asset)
| logo_id | uuid | Optional. Logo image id (the id of a logo type asset)
| strip_id | uuid | Optional. Strip image id (the id of a logo type asset)
| logo_text | string | Optional. Top card text
| background_color| rgb string | Optional. Color defining the pass background color ranging from `#000000` to `#ffffff`
| text_color | rgb string | Optional. The text color for all the `value` fields except primary_fields, ranging from `#00000` to `#ffffff`
| label_color | rgb string | Optional. The text color for all `label` fields except primary_fields, ranging from `#00000` to `#ffffff`
| barcode | hash | Optional. A single hash of [barcode hash object](#barcode-hash-object-format).


### Available fields

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
| beacons | array | Optional. Collection of up to 10 [beacon hash objects](#beacon-hash-object-format)
| certificate_id | uuid | Optional. **You should provide your own certificate** but in none is provided the passworks.io default certificate is used.
| organization_name | string | Optional. Organization name showned in the unlock screen, if none is supplied the registration organization name is used
| associated\_store\_identifiers | array | Optional. A list of iTunes Store item identifiers for the associated apps. Only one item in the list is used - the first item identifier for an app compatible with the current device. If the app is not installed, the link opens the App Store and shows the app. If the app is already installed, the link launches the app, [as specified in passbook's documentation](https://developer.apple.com/library/ios/documentation/UserExperience/Reference/PassKit_Bundle/Chapters/TopLevel.html#//apple_ref/doc/uid/TP40012026-CH2-SW7)
| og | Boolean | Use Open Graph tags on the download page. Optional, default: true
| og_description | String | Open Graph description. Optional, default: "" (empty string)
| javascript | String | Javascript that will be rendered inside the download page and form, Allows the user to run their own javascript code eg: Google Analytics or Facebook Pixel  |
| stylesheet | String | CSS that will be rendered inside the download page and form, allows users to override the page css |
| user_info | hash | Optional. This field can be used to store user related data. On Apple Wallet this field will be available as a JSON encoded string. |


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
	"major": 0,
	"minor": 0,
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
format | string | Optional. Must be one of the following if supplied: **qrcode**, **pdf417**, **aztec**, or **none**. | qrcode
message | string | Optional. Message encoded in the barcode. | Pass's redeem code.


**NOTE:** The following instructions will reset all the issued passes to the base template, removing the personalization fields from all the issued passes.

The correct way of updating the already issued passes while preserving the custom fields (like the name of the pass owner, for example) is to iterate trough the issued pass collection, by collecting the ids from
`GET /v2/store_cards/{campaign_id}/passes`

and then [updating each pass](#updating-each-pass) with the fields you wish to change.

Please contact support@passworks.io for advisement on updating a store card campaign.

If, however any old passes that had already been generated and you wish to reset them to the new changes, you **must**, following a campaign update, issue a push POST request:

```shell
POST /v2/store_cards/{campaign_id}/push
```

Along with this push, you may also, optionally, send in a payload with a push message that will be presented to the users when the update is done, shown on the lock screen.

```json
{
  "store_card": {
      "push_message": "New beverage!"
  }
}
```

|  Field name  | Type |  Description   | Default |
|--------------|------|----------------|---------|
push_message | string | Optional. Text shown on the lock screen. | No message sent.

This request will push all existing passes once again, guaranteeing that all that have been downloaded will contain the new changes. Otherwise, there's no guarantee that the users will receive the updated pass.


## Creating a Store Card pass for a customer

You can create a boilerplate pass simply by POSTing to the passes route:

```shell
POST /v2/store_cards/{campaign_id}/passes
```

If you want to personalize the pass you can supply an hash with the parameters you want to override:

```shell
POST /v2/store_cards/{campaign_id}/passes/
```

POST Content

```json
{
  "pass": {
    "primary_fields": [
      {
        "key": "balance",
        "label": "$25,00"
      }
    ],
    "secondary_fields": [
      {
        "key": "level",
        "value": "Gold"
      },
      {
        "key": "usual_beverage",
        "value": "Iced Mocha"
      }
    ]
  }
}
```

In case of success HTTP 201 response code is returned with the following body content:

```json
{
  "id": "abe15069-8326-4d2a-86f9-25fa11229a68",
  "campaign_id": "df570ca9-2fd4-462f-8d12-f0882ca38302",
  "voided": false,
  "serial_number": "878d8095-be05-4799-b697-72cdd9f6449c",
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
      "key": "balance",
      "value": "remaining balance",
      "label": "$25,00"
    }
  ],
  "secondary_fields": [
    {
      "key": "level",
      "value": "Gold",
      "label": "LEVEL"
    },
    {
      "key": "usual_beverage",
      "value": "Iced Mocha",
      "label": "THE USUAL"
    }
  ],
  "auxiliary_fields": [],
  "back_fields": [],
  "locations": [],
  "beacons": [],
  "page_url": "http://get.passworks.io/MqixNhgUdg/AezEnfl4KszrYKM1dLZUng",
  "pkpass_url": "http://get.passworks.io/MqixNhgUdg/AezEnfl4KszrYKM1dLZUng.pkpass",
  "created_at": "2015-03-31T13:55:57Z",
  "updated_at": "2015-03-31T13:55:57Z"
}
```

|  Field name  | Type |  Description  |
|--------------|------|----------------|
loyalty_id | uuid | The loyalty campaign id that the created pass belongs to.
pass_id | uuid | The created pass's ID.
download\_page\_link | string | The HTML page with the download link
direct_link | string | The direct download link for the pass


## Updating the customer pass

```shell
PATCH /v2/store_cards/{campaign_id}/passes/{pass_id}/
```

PATCH Content

```json
{
  "pass": {
    "primary_fields": [
      {
        "key": "balance",
        "label": "$15,00"
      }
    ],
    "merge": true,
    "push": false
  }
}
```

|  Field name  | Type |  Description  |
|--------------|------|----------------|
merge | uuid | Merges the current supplied content with the **current pass** content
push | boolean | Optional (default: *true*). After successul update pushesh the updated pass to the user


In case of success HTTP 201 response code is returned with the complete passe details:

```json
{
  "id": "1b0e0125-184d-4ad3-af4d-86c5e9d8196d",
  "campaign_id": "a9ecf81e-e64e-4ce8-b4fb-33621bb29452",
  "voided": false,
  "authentication_token": "mtS6Ffa9v5wF_x6oQFOniw",
  "serial_number": "bc56c0ec-b639-4f04-a9c6-a04382b80dd5",
  "header_fields": [],
  "primary_fields": [
    {
      "key": "balance",
      "label": "$15,00",
      "value": "remaining balance"
    }
  ],
  "secondary_fields": [
    {
      "key": "level",
      "label": "LEVEL",
      "value": "Gold"
    },
    {
      "key": "usual_beverage",
      "label": "THE USUAL",
      "value": "Iced Mocha"
    }
  ],
  "auxiliary_fields": [],
  "back_fields": [],
  "barcode": {
    "format": "pdf417",
    "message": "0000003",
    "alt_text": "0000003"
  },
  "beacons": [],
  "locations": [],
  "redeemed_count": 0,
  "download_page_link": "http://get.passworks.io/oPDKThBkcg/cpVwFpziwSDqkvcBh0XjVQ",
  "direct_link": "http://get.passworks.io/oPDKThBkcg/cpVwFpziwSDqkvcBh0XjVQ.pkpass",
  "expiration_date": null,
  "redeemed_at": null,
  "created_at": "2014-09-24T17:22:28Z",
  "updated_at": "2014-09-24T17:25:56Z"
}
```


## Sending a push notification (or forcing a pass update)

You can force the retrieval of a pass via push notification by simply calling the following URL:

```shell
POST /v2/store_cards/{campaign_id}/passes/{pass_id}/push
```

You can also send a custom message that will be displayed in the lock screen via push notification sending the following content in the above request

```json
{
	"pass": {
		"push_message": "Hello!"
	}
}
```


## Redeeming a pass

There are two ways you can redeem a pass:

- Redeeming a pass by referencing a redeem code
	You can redeem a pass by referencing a redeem code (instead of the pass_id) by POSTing to the campaign `redeem` route

	```shell
	/v2/store_cards/{campaign_id}/redeem
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
	POST /v2/store_cards/{campaign_id}/passes/{pass_id}/redeem
	```

	You can supply an optional `comment` key where you can specify some information you want to be stored for reference:

	```json
	{
		"pass": {
			"comment": "redeemed in store"
		}
	}
	```

## Reseting a redeem

If your pass was flagged as "void" you can reset the flag calling the "reset_redeem" endpoint

```shell
POST /v2/coupons/{campaign_id}/passes/{pass_id}/reset_redeem
```

## Aditional routes available

### Get all the Store Card campaigns:
```shell
GET /v2/store_cards/
```

### Delete a Store Card campaign

```shell
DELETE /v2/store_cards/{campaign_id}
```

In case of success a HTTP 200 status code is returned with empty error list.
n
```json
{
  "errors": []
}
```

In case of a error a HTTP 412 (Precondition Failed) status code is returned with a array of errors.

```json
{
  "errors": {
    "campaign": "Campaign not found."
  }
}
```

### Changing campaign state via PAUSE, RESUME, ARCHIVE

You can pause, resume and archive campaigns using the following endpoints:

Pausing a campaign disables the ability to issue more passes and changes the campaign state to "paused".

```shell
POST /v2/store_cards/{campaign_id}/pause
```

Resuming a campaign re-enables the issuing of new passes, changes the campaign state to "published" again.

```shell
POST /v2/store_cards/{campaign_id}/resume
```

Archiving stops the issuing of new passes and and hides the campaign from the interface without deleting the campaign. It changes the campaign state to "archived".

```shell
POST /v2/store_cards/{campaign_id}/archive
```

If the campaign state is changed successfully the endpoints return a 200 HTTP status code.

In case of a error a HTTP 412 (Precondition Failed) is returned with a error message, eg:

```
{
  "errors": [
    "Can't resume from archived to publish"
  ]
}
```


### Get all the passes for a specific Store Card campaign:
```shell
GET /v2/store_cards/{campaign_id}/passes
```

### Get a pass's id from its redeem code
```shell
GET /v2/store_cards/{campaign_id}/redeem/{redeem_code}
```

### Reports
```shell
GET /v2/store_cards/{campaign_id}/reports
```

```shell
GET /v2/store_cards/{campaign_id}/reports/totals
```

For more information about the campaign reports, please check our [Reports Documentation](https://github.com/passworks/passworks-api/blob/master/v2/sections/reports.md).
