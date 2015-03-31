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
  "organization_name": "onomecompany",
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
  "page_url": "http://get.192.168.1.67.xip.io:3000/ahStMTeuCw",
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
PATCH /v2/generics/{generic_id}
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
  "organization_name": "onomecompany",
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
  "page_url": "http://get.192.168.1.67.xip.io:3000/IGYIYEydVw",
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


Creating a Generic Pass for "Johnny Appleseed"
------------

Creating Johnny's pass is rather straightforward, we will pass the thumbnail asset (`tumbnaill_id`) with his photo. And supply the remaining \*_fields with the information corresponding to each key.

```shell
POST /v2/generics/{generic_id}/passes
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
  "page_url": "http://get.192.168.1.67.xip.io:3000/IGYIYEydVw/rzhfuD9mTdiAbGp14PGUoA",
  "pkpass_url": "http://get.192.168.1.67.xip.io:3000/IGYIYEydVw/rzhfuD9mTdiAbGp14PGUoA.pkpass",
  "created_at": "2015-03-31T17:33:28Z",
  "updated_at": "2015-03-31T17:33:28Z"
}
```

Updating "Johnny Appleseed" Generic Pass
------------
Let's imagine that Johnny's new favorite toys are now *airplanes* so let's update the `favorite` key inside the `auxiliary_fields ` fields with the new value (Airplanes).

```shell
PATCH /v1/generics/{generic_id}/passes/{pass_id}
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
  "page_url": "http://get.192.168.1.67.xip.io:3000/IGYIYEydVw/rzhfuD9mTdiAbGp14PGUoA",
  "pkpass_url": "http://get.192.168.1.67.xip.io:3000/IGYIYEydVw/rzhfuD9mTdiAbGp14PGUoA.pkpass",
  "created_at": "2015-03-31T17:33:28Z",
  "updated_at": "2015-03-31T17:35:33Z"
}
```


Sending a push notification (or forcing a pass update)
------------

You can force the retrieval of a pass via push notification by simply calling the following URL:

```shell
POST /v2/generics/{generic_id}/passes/{pass_id}/push
```

You can also send a custom message that will be displayed in the lock screen via push notification sending the following content in the above request

```json
  {
    "pass": {
      "push_message": "Hello!"
    }
  }
```