Store Card
================


The Passworks API can be used to create loyalty or event tier programs to reward your customers for using your services.


Example of a Store Card
------------


| ![img1](https://raw.githubusercontent.com/passworks/passworks-api/master/assets/images/store_card/store_card_2x.png) | ![img2](https://raw.githubusercontent.com/passworks/passworks-api/master/assets/images/store_card/bayroast_coffee_guidelines.png) |
|---|---|
| Generic Loyalty Card Schematic | Bayroast Coffe Loyalty Card |



Creating a Store Card "campaign" for the "Bayroast Coffee"
------------


```shell
POST /v1/store_cards/
```

POST Content

```json
{
  "store_card": {
    "name": "Bayroast Coffee Store Cards",
    "icon_id": "cecd7470-2ba8-4737-afe0-30d0cd4fd00c",
    "logo_id": "eb66127b-cbb7-41f4-b7ea-a6b8c106fead",
    "strip_id": "a79c77af-9640-4758-ab23-41e2a0f27fa6",    
    "logo_text": "Bayroast Coffee",
    "background_color": "#764a32",
    "text_color": "#f5f2f0",
    "label_color": "#643e2a",
    "barcode": "pdf417",
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
  "store_card": {
    "id": "a9ecf81e-e64e-4ce8-b4fb-33621bb29452",
    "name": "Bayroast Coffee Store Cards",
    "description": "Bayroast Coffee Store Cards",
    "icon_id": "cecd7470-2ba8-4737-afe0-30d0cd4fd00c",
    "strip_id": "a79c77af-9640-4758-ab23-41e2a0f27fa6",
    "logo_id": "eb66127b-cbb7-41f4-b7ea-a6b8c106fead",
    "organization_name": "passworks",
    "logo_text": "Bayroast Coffee",
    "background_color": "#764a32",
    "text_color": "#f5f2f0",
    "label_color": "#643e2a",
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
        "value": "",
        "label": "LEVEL"
      },
      {
        "key": "usual_beverage",
        "value": "",
        "label": "THE USUAL"
      }
    ],
    "auxiliary_fields": [],
    "back_fields": [],
    "locations": [],
    "beacons": [],
    "created_at": "2014-09-24T17:07:38Z",
    "updated_at": "2014-09-24T17:07:38Z"
  }
}
```

NOTE: The API date fields (e.g `created_at`, `updated_at`) use the [ISO-8601](http://en.wikipedia.org/wiki/ISO_8601) format (e.g:  `2014-09-22T20:51:53+00:00`).

##### Available fields

|  Field name  | Type | Description  |
|-------------|------|-----------------------------------
| name | string | Required. Must be unique, it's used to identify the Store Card/Loyalty "Campaign"
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
| background_color| rgb string | Required. Color defining the pass background color ranging from `#00000` to `#ffffff`
| text_color | rgb string | Required. The text color for all the `value` fields except primary_fields, ranging from `#00000` to `#ffffff`
| label_color | rgb string | Required. The text color for all `label` fields except primary_fields, ranging from `#00000` to `#ffffff` 
| certificate_id | uuid | Optional. **You should provide your own certificate** but in none is provided the passworks.io default certificate is used.
| organization_name | string | Optional. Organization name showned in the unlock screen, if none is supplied the registration organization name is used


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


##### iBeacon hash object format

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

Creating a Store Card pass for a customer
------------

```shell
POST /v1/store_cards/{store_card_id}/passes
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
  "pass": {
    "id": "8506a086-0de1-4f67-8258-bbcb6bfab6f9",
    "store_card_id": "a9ecf81e-e64e-4ce8-b4fb-33621bb29452",
    "voided": false,
    "authentication_token": "QWli3jb05oHkdUqQQ2RstA",
    "serial_number": "01ab6ea6-6d82-49f1-b252-e969e449e378",
    "header_fields": [],
    "primary_fields": [
      {
        "key": "balance",
        "label": "$25,00",
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
      "message": "0000001",
      "alt_text": "0000001"
    },
    "beacons": [],
    "locations": [],
    "redeemed_count": 0,
    "donwload_page_link": "http://get.passworks.io/oPDKThBkcg/fUaYHdEvfKKT6KsAAIpokg",
    "direct_link": "http://get.passworks.io/oPDKThBkcg/fUaYHdEvfKKT6KsAAIpokg.pkpass",
    "expiration_date": null,
    "redeemed_at": null,
    "created_at": "2014-09-24T17:10:16Z",
    "updated_at": "2014-09-24T17:10:16Z"
  }
}
```

|  Field name  | Type |  Description  |
|--------------|------|----------------|
loyalty_id | uuid | The loyalty campaign id that the created passe belongs
pass_id | uuid | The created pass that belongs
donwload_page_link | string | The HTML page with the download link
direct_link | string | The direct download link for the pass




Updating the customer pass
------------

```shell
PATCH /v1/store_cards/{store_card_id}/passes/{pass_id}/
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
  "pass": {
    "id": "1b0e0125-184d-4ad3-af4d-86c5e9d8196d",
    "store_card_id": "a9ecf81e-e64e-4ce8-b4fb-33621bb29452",
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
    "donwload_page_link": "http://get.passworks.io/oPDKThBkcg/cpVwFpziwSDqkvcBh0XjVQ",
    "direct_link": "http://get.passworks.io/oPDKThBkcg/cpVwFpziwSDqkvcBh0XjVQ.pkpass",
    "expiration_date": null,
    "redeemed_at": null,
    "created_at": "2014-09-24T17:22:28Z",
    "updated_at": "2014-09-24T17:25:56Z"
  }
}
```


Forcing a push update of a pass
------------

You can force a push notification of a passe (provided that it was changed since the user last fetched it) by using the following URL

```shell
POST /v1/store_cards/{store_card_id}/passes/{pass_id}/push
```

