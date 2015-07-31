Generic Pass
================


Generic passes can be used for anything that doesn't fit in the other pass categories.


Example of Generic passes
------------

|![img1](https://raw.githubusercontent.com/passworks/passworks-api/master/v2/assets/images/generic/generic_2x.png)|
|:--------------:|
|Generic Pass (schematic)|


| ![img2](https://raw.githubusercontent.com/passworks/passworks-api/master/v2/assets/images/generic/generic_pass_toy_town_guidelines.png) | (missing image) |
|:-------------------:|:----------------:|
| Generic Pass with rectangular barcode | Generic Pass with square barcode |



Creating a Generic "campaign" for the "Toy Town"
------------

For this generic campaign we will have a custom primary field called `member` that will be displaying the child name. A secondary field with the key `subtitle` displaying the signup date and two auxiliary fields displaying the membership level and the favorite toy (called `level `, `favorite `).

In this campaign step we don't include the child's picture because each pass uses it's unique picture of the child.

```shell
POST /v2/generics/
```

```json
{
  "generic": {
    "name": "Toy Town Generic Passes!",
    "icon_id": "e365088d-27db-4d5e-9915-466d06385426",
    "logo_id": "a798fbf5-033f-4334-99f5-3196751e0595",
    "logo_text": "Toy Town",
    "barcode": {
      "format": "pdf417"
    },
    "text_color": "#ffffff",
    "background_color": "#c51f1f",
    "primary_fields": [
      {
        "key": "member"
      }
    ],
    "secondary_fields": [
      {
        "key": "subtitle",
        "label": "MEMBER SINCE"
      }
    ],
    "auxiliary_fields": [
      {
        "key": "level",
        "label": "LEVEL"
      },
      {
        "key": "favorite",
        "label": "FAVORITE TOY"
      }
    ]
  }
}
```

Response

```json
{
  "id": "19a8ca5f-5eb0-4ff6-a7b2-f5a865ad8451",
  "name": "Toy Town Generic Passes!",
  "template_id": "b2651552-5abb-4ff2-b701-d74cd000784f",
  "organization_name": "your company",
  "barcode": {
    "format": "pdf417",
    "message": "",
    "alt_text": ""
  },
  "allow_multiple_redeems": false,
  "header_fields": [],
  "primary_fields": [
    {
      "key": "member",
      "value": null,
      "label": null
    }
  ],
  "secondary_fields": [
    {
      "key": "subtitle",
      "value": null,
      "label": "MEMBER SINCE"
    }
  ],
  "auxiliary_fields": [
    {
      "key": "level",
      "value": null,
      "label": "LEVEL"
    },
    {
      "key": "favorite",
      "value": null,
      "label": "FAVORITE TOY"
    }
  ],
  "back_fields": [],
  "locations": [],
  "beacons": [],
  "page_url": "http://get.passworks.io/ahStMTeuCw",
  "created_at": "2015-03-31T17:27:48Z",
  "updated_at": "2015-03-31T17:27:50Z"
}
```

##### Presentation fields (when template_id is not supplied)

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

##### Available fields

|  Field name  | Type | Description  |
|-------------|------|-----------------------------------
| name | string | Required. Must be unique, it's used to identify the Store Card/Loyalty "Campaign"
| description | string | Optional. Brief description of the pass, used by the iOS accessibility technologies. If the description is not provided the *name* field value is used instead.
| header_fields | array | Optional. Collection of *field hash objects*
| secondary_fields | array | Optional. Collection of *field hash objects*
| auxiliary_fields | array | Optional. Collection of *field hash objects*
| back_fields | array | Optional. Collection of *field hash objects* used in the rear part of the pass
| locations | array | Optional. Collection of up to 10 [location hash objects](#location-hash-object-format)
| beacons | array | Optional. Collection of up to 10 [beacon hash objects](#ibeacon-hash-object-format)
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


##### Beacon hash object format

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



Updating a Generic "campaign" for the "Toy Town"
------------

```shell
PATCH /v2/generics/{campaign_id}
```

```json
{
  "generic": {
  	"background_color": "#facada"
  }
}
```

Response

```json
{
  "id": "5b6168a3-0611-4948-91a4-91f5de730bc3",
  "name": "Toy Town Generic Passes",
  "template_id": "ba808b03-c0f1-4843-84c7-6f6da81c1c69",
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
      "key": "member",
      "value": "Johnny Appleseed",
      "label": null
    }
  ],
  "secondary_fields": [
    {
      "key": "subtitle",
      "value": "2012",
      "label": "MEMBER SINCE"
    }
  ],
  "auxiliary_fields": [
    {
      "key": "level",
      "value": "Platinum",
      "label": "LEVEL"
    },
    {
      "key": "favorite",
      "value": "Trucks",
      "label": "FAVORITE TOY"
    }
  ],
  "back_fields": [],
  "locations": [],
  "beacons": [],
  "page_url": "http://get.passworks.io/IGYIYEydVw",
  "created_at": "2015-03-31T17:03:01Z",
  "updated_at": "2015-03-31T18:01:11Z"
}
```

##### Presentation fields (when template_id is not supplied)

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

##### Available fields

|  Field name  | Type | Description  |
|-------------|------|-----------------------------------
| name | string | Required. Must be unique, it's used to identify the Store Card/Loyalty "Campaign"
| description | string | Optional. Brief description of the pass, used by the iOS accessibility technologies. If the description is not provided the *name* field value is used instead.
| header_fields | array | Optional. Collection of *field hash objects*
| secondary_fields | array | Optional. Collection of *field hash objects*
| auxiliary_fields | array | Optional. Collection of *field hash objects*
| back_fields | array | Optional. Collection of *field hash objects* used in the rear part of the pass
| locations | array | Optional. Collection of up to 10 [location hash objects](#location-hash-object-format)
| beacons | array | Optional. Collection of up to 10 [beacon hash objects](#ibeacon-hash-object-format)
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


##### Beacon hash object format

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


**NOTE:** The following instructions will reset all the issued passes to the base template, removing the personalization fields from all the issued passes.

The correct way of updating the already issued passes while preserving the custom fields (like the name of the pass owner, for example) is to iterate trough the issued pass collection, by collecting the ids from
`GET /v2/generics/{campaign_id}/passes`

and then [updating each pass](#updating-each-pass) with the fields you wish to change.

Please contact support@passworks.io for advisement on updating a generic campaign.

If, however any old passes that had already been generated and you wish to reset them to the new changes, you **must**, following a campaign update, issue a push POST request:

```shell
POST /v2/generics/{campaign_id}/push
```

Along with this push, you may also, optionally, send in a payload with a push message that will be presented to the users when the update is done, shown on the lock screen.

```json
{
	"generic": {
	    "push_message": "Look at your new pass!"
	}
}
```

|  Field name  | Type |  Description   | Default |
|--------------|------|----------------|---------|
push_message | string | Optional. Text shown on the lock screen. | No message sent.

This request will push all existing passes once again, guaranteeing that all that have been downloaded will contain the new changes. Otherwise, there's no guarantee that the users will receive the updated pass.



Creating a Generic Pass for "Johnny Appleseed"
------------
You can create a boilerplate pass simply by POSTing to the passes route:

```shell
POST /v2/generics/{campaign_id}/passes
```

If you want to personalize the pass you can supply an hash with the parameters you want to override:
Following our example, creating Johnny's pass is rather straightforward, we will pass the thumbnail asset (`thumbnail_id`) with his photo. And supply the remaining \*_fields with the information corresponding to each key.

```shell
POST /v2/generics/{campaign_id}/passes
```


```json
{
  "pass": {
    "thumbnail_id": "c1c65182-441c-4ecf-bc9f-2783127de070",
    "primary_fields": [
      {
        "key": "member",
        "value" : "Johnny Appleseed"
      }
    ],
    "secondary_fields": [
      {
        "key": "subtitle",
        "value": "2012"
      }
    ],
    "auxiliary_fields": [
      {
        "key": "level",
        "value": "Platinum"
      },
      {
        "key": "favorite",
        "value": "Trucks"
      }
    ]
  }
}
```

Response:

```json
{
  "id": "ee84e7a7-4cdc-47d6-aa82-8a1de1879380",
  "campaign_id": "5b6168a3-0611-4948-91a4-91f5de730bc3",
  "voided": false,
  "serial_number": "e1d2a302-e8e1-4762-b303-4f2326e6e2cb",
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
      "key": "member",
      "value": "Johnny Appleseed",
      "label": null
    }
  ],
  "secondary_fields": [
    {
      "key": "subtitle",
      "value": "2012",
      "label": "MEMBER SINCE"
    }
  ],
  "auxiliary_fields": [
    {
      "key": "level",
      "value": "Platinum",
      "label": "LEVEL"
    },
    {
      "key": "favorite",
      "value": "Trucks",
      "label": "FAVORITE TOY"
    }
  ],
  "back_fields": [],
  "locations": [],
  "beacons": [],
  "page_url": "http://get.passworks.io/IGYIYEydVw/rzhfuD9mTdiAbGp14PGUoA",
  "pkpass_url": "http://get.passworks.io/IGYIYEydVw/rzhfuD9mTdiAbGp14PGUoA.pkpass",
  "created_at": "2015-03-31T17:33:28Z",
  "updated_at": "2015-03-31T17:33:28Z"
}
```

Updating "Johnny Appleseed" Generic Pass
------------
Let's imagine that Johnny's new favorite toys are now *airplanes* so let's update the `favorite` key inside the `auxiliary_fields ` fields with the new value (Airplanes).

```shell
PATCH /v1/generics/{campaign_id}/passes/{pass_id}
```

```json
{
	"pass": {
		"auxiliary_fields": [
			{
			 	"key": "favorite",
			 	"value": "Airplanes"
			}
		]
	}
}
```

Response:

```json
{
  "id": "ee84e7a7-4cdc-47d6-aa82-8a1de1879380",
  "campaign_id": "5b6168a3-0611-4948-91a4-91f5de730bc3",
  "voided": false,
  "serial_number": "e1d2a302-e8e1-4762-b303-4f2326e6e2cb",
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
      "key": "member",
      "value": "Johnny Appleseed",
      "label": null
    }
  ],
  "secondary_fields": [
    {
      "key": "subtitle",
      "value": "2012",
      "label": "MEMBER SINCE"
    }
  ],
  "auxiliary_fields": [
    {
      "key": "level",
      "value": "Platinum",
      "label": "LEVEL"
    },
    {
      "key": "favorite",
      "value": "Airplanes",
      "label": "FAVORITE TOY"
    }
  ],
  "back_fields": [],
  "locations": [],
  "beacons": [],
  "page_url": "http://get.passworks.io/IGYIYEydVw/rzhfuD9mTdiAbGp14PGUoA",
  "pkpass_url": "http://get.passworks.io/IGYIYEydVw/rzhfuD9mTdiAbGp14PGUoA.pkpass",
  "created_at": "2015-03-31T17:33:28Z",
  "updated_at": "2015-03-31T17:35:33Z"
}
```


Sending a push notification (or forcing a pass update)
------------

You can force the retrieval of a pass via push notification by simply calling the following URL:

```shell
POST /v2/generics/{campaign_id}/passes/{pass_id}/push
```

You can also send a custom message that will be displayed in the lock screen via push notification sending the following content in the above request

```json
  {
    "pass": {
      "push_message": "Hello!"
    }
  }
```

Redeeming a pass
------------

There are two ways you can redeem a pass:

- Redeeming a pass by referencing a redeem code
	You can redeem a pass by referencing a redeem code (instead of the pass_id) by POSTing to the campaign `redeem` route
	
	```shell
	/v2/generics/{campaign_id}/redeem
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
	POST /v2/generics/{campaign_id}/passes/{pass_id}/redeem
	```
	
	You can supply an optional `comment` key where you can specify some information you want to be stored for reference:
	
	```json
	{
		"pass": {
			"comment": "redeemed in store"
		}
	}
	```
	
	


Aditional routes available
------------

#####Get all the Generic campaigns:
```shell
GET /v2/generics/
```

#####Get all the passes for a specific Generic campaign:
```shell
GET /v2/generics/{campaign_id}/passes
```

#####Get a pass's id from its redeem code
```shell
GET /v2/generics/{campaign_id}/redeem/{redeem_code}
```
