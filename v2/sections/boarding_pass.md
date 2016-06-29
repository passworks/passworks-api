Boarding Passes
================

> Attention: This pass is not yet supported by Android Pay, please check the
> [Android Pay](https://github.com/passworks/passworks-api/blob/master/v2/sections/android_pay.md)
> documentation for more details.

Boarding passes can be **airplane**, **bus**, **train**, or **boat tickets**. You also can create generic boarding passes.

Examples of Boarding Passes
------------


| ![img1](https://raw.githubusercontent.com/passworks/passworks-api/master/v2/assets/images/boarding_pass/boarding_pass_2x.png) | ![img2](https://raw.githubusercontent.com/passworks/passworks-api/master/v2/assets/images/boarding_pass/skyport_airways_boarding_pass_guidelines.png) |
|---|---|
| Generic Boarding Schematic | Skyport Airways (Flight 815) |


Creating a Airplane Boarding Pass Campaign for "Skyport Airways" flight 815
------------

```shell
POST /v2/boarding_passes/
```

Payload:

```json
{
  "boarding_pass": {
    "name": "Skyport Airways flight 815",
    "icon_id": "ffe0d88f-916d-4a12-8244-9ecd0178ca45",
    "logo_id": "a8d93197-3a26-4b91-9551-6091f42a5be4",
    "barcode": {
    	"format": "pdf417"
    },
    "logo_text": "Skyport Airways",
    "foreground_color": "#6e3716",
    "background_color": "#325bb9",
    "transit_type": "air",
    "header_fields": [
      {
        "label": "GATE",
        "key": "gate",
        "value": "23"
      }
    ],
    "primary_fields": [
      {
        "key": "depart",
        "label": "SAN FRANCISCO",
        "value": "SFO"
      },
      {
        "key": "arrive",
        "label": "NEW YORK",
        "value": "JFK"
      }
    ],
    "secondary_fields": [
      {
        "key": "passenger",
        "label": "PASSENGER"
      }
    ],
    "auxiliary_fields": [
      {
        "label": "DEPART",
        "key": "boardingTime"
      },
      {
        "label": "FLIGHT",
        "key": "flightNewName",
        "value": "815"
      },
      {
        "key": "class",
        "label": "DESIG."
      },
      {
        "key": "date",
        "label": "DATE",
        "value": "7/22"
      }
    ]
  }
}
```

Response:

```json
{
  "id": "485d2a26-efc5-4f85-8855-fa2f4b6cd2e2",
  "name": "Skyport Airways flight 815",
  "template_id": "492d648f-559b-482f-a3c2-2a43aa194aed",
  "organization_name": "foobar",
  "barcode": {
    "format": "pdf417",
    "message": "",
    "alt_text": ""
  },
  "allow_multiple_redeems": false,
  "header_fields": [
    {
      "key": "gate",
      "value": "23",
      "label": "GATE"
    }
  ],
  "primary_fields": [
    {
      "key": "depart",
      "value": "SFO",
      "label": "SAN FRANCISCO"
    },
    {
      "key": "arrive",
      "value": "JFK",
      "label": "NEW YORK"
    }
  ],
  "secondary_fields": [
    {
      "key": "passenger",
      "value": null,
      "label": "PASSENGER"
    }
  ],
  "auxiliary_fields": [
    {
      "key": "boardingTime",
      "value": null,
      "label": "DEPART"
    },
    {
      "key": "flightNewName",
      "value": "815",
      "label": "FLIGHT"
    },
    {
      "key": "class",
      "value": null,
      "label": "DESIG."
    },
    {
      "key": "date",
      "value": "7/22",
      "label": "DATE"
    }
  ],
  "back_fields": [],
  "locations": [],
  "beacons": [],
  "page_url": "http://get.passworks.io/G1mbmsPWkw",
  "gwallet_usage": false,
  "gwallet_status": nil,
  "gwallet_message": nil,
  "created_at": "2015-04-01T10:06:33Z",
  "updated_at": "2015-04-01T10:06:33Z"
}
```


##### Presentation fields (when template_id is not supplied)

|  Field name  | Type | Description  |
|-------------|------|-----------------------------------
| icon_id | uuid | Required. Icon  id (the id of a icon type asset)
| logo_id | uuid | Optional. Logo image id (the id of a logo type asset)
| strip_id | uuid | Optional. Strip image id (the id of a logo type asset)
| background_id | uuid | Optional. Strip image id (the id of a background type asset)
| thumbnail_id | uuid | Optional. Strip image id (the id of a logo type asset)
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
| transit_type | string | Required. Must be one of the following values `air`, `boat`, `train`, `boat` or `generic`
| template_id | uuid | Optional. If not supplied, you **must supply the presentation fields presented in the table above!**
| header_fields | array | Optional. Collection of *field hash objects*
| secondary_fields | array | Optional. Collection of *field hash objects*
| auxiliary_fields | array | Optional. Collection of *field hash objects*
| back_fields | array | Optional. Collection of *field hash objects* used in the rear part of the pass
| locations | array | Optional. Collection of up to 10 [location hash objects](#location-hash-object-format)
| beacons | array | Optional. Collection of up to 10 [beacon hash objects](#ibeacon-hash-object-format)
| certificate_id | uuid | Optional. **You should provide your own certificate** but in none is provided the passworks.io default certificate is used.
| organization_name | string | Optional. Organization name showned in the unlock screen, if none is supplied the registration organization name is used
| associated\_store\_identifiers | array | Optional. A list of iTunes Store item identifiers for the associated apps. Only one item in the list is used - the first item identifier for an app compatible with the current device. If the app is not installed, the link opens the App Store and shows the app. If the app is already installed, the link launches the app, [as specified in passbook's documentation](https://developer.apple.com/library/ios/documentation/UserExperience/Reference/PassKit_Bundle/Chapters/TopLevel.html#//apple_ref/doc/uid/TP40012026-CH2-SW7)

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
format | string | Optional. Must be one of the following if supplied: **qrcode**, **pdf417**, **aztec**, **ean128** or **none**. | qrcode
message | string | Optional. Message encoded in the barcode. | Pass's redeem code.


Updating the "Skyport Airways" flight 815 Campaign
------------

Let's imagine that the gate of the flight changed, and you wish to update all of the campaign's passes. To do so, you will need to issue a PATCH to the following URL with this example payload:

```shell
PATCH /v2/boarding_passes/{campaign_id}
```


```json
{
	"boarding_pass": {
	    "header_fields": [
      {
        "label": "GATE",
        "key": "gate",
        "value": "A3"
      }
    ]
	}
}
```

Response:

```json
{
  "id": "485d2a26-efc5-4f85-8855-fa2f4b6cd2e2",
  "name": "Skyport Airways flight 815",
  "template_id": "492d648f-559b-482f-a3c2-2a43aa194aed",
  "organization_name": "foobar",
  "barcode": {
    "format": "qrcode",
    "message": "",
    "alt_text": ""
  },
  "allow_multiple_redeems": false,
  "header_fields": [
    {
      "key": "gate",
      "value": "A3",
      "label": "GATE"
    }
  ],
  "primary_fields": [
    {
      "key": "depart",
      "value": "SFO",
      "label": "SAN FRANCISCO"
    },
    {
      "key": "arrive",
      "value": "JFK",
      "label": "NEW YORK"
    }
  ],
  "secondary_fields": [
    {
      "key": "passenger",
      "value": null,
      "label": "PASSENGER"
    }
  ],
  "auxiliary_fields": [
    {
      "key": "boardingTime",
      "value": null,
      "label": "DEPART"
    },
    {
      "key": "flightNewName",
      "value": "815",
      "label": "FLIGHT"
    },
    {
      "key": "class",
      "value": null,
      "label": "DESIG."
    },
    {
      "key": "date",
      "value": "7/22",
      "label": "DATE"
    }
  ],
  "back_fields": [],
  "locations": [],
  "beacons": [],
  "page_url": "http://get.passworks.io/G1mbmsPWkw",
  "created_at": "2015-04-01T10:06:33Z",
  "updated_at": "2015-04-01T10:18:15Z"
}
```

Now that you've updated your campaign, all the future passes generated from this updated campaign will contain the new changes.

**NOTE:** The following instructions will reset all the issued passes to the base template, removing the personalization fields from all the issued passes.

The correct way of updating the already issued passes while preserving the custom fields (like the name of the pass owner, for example) is to iterate trough the issued pass collection, by collecting the ids from
`GET /v2/boarding_passes/{campaign_id}/passes`

and then [updating each pass](#updating-each-pass) with the fields you wish to change.

Please contact support@passworks.io for advisement on updating a boarding pass campaign.

If, however any old passes that had already been generated and you wish to reset them to the new changes, you **must**, following a campaign update, issue a push POST request:

```shell
POST /v2/boarding_passes/{campaign_id}/push
```

Along with this push, you may also, optionally, send in a payload with a push message that will be presented to the users when the update is done, shown on the lock screen.

```json
{
	"boarding_pass": {
	    "push_message": "Gate has changed!"
	}
}
```

Response:

You'll get a contextualized message, informing on the start of the pass updates, or that there are no passes to be updated.

```json
{
	"message": "There are no passes to update for campaing 'Skyport Airways flight 815'."
}
```

|  Field name  | Type |  Description   | Default |
|--------------|------|----------------|---------|
push_message | string | Optional. Text shown on the lock screen. | No message sent.

This request will push all existing passes once again, guaranteeing that all that have been downloaded will contain the new changes. Otherwise, there's no guarantee that the users will receive the updated pass.


Creating a Boarding Pass for "John Appleseed"
------------

You can create a boilerplate pass simply by POSTing to the passes route:

```shell
POST /v2/boarding_passes/{campaign_id}/passes
```

If you want to personalize the pass you can supply an hash with the parameters you want to override:

```shell
POST /v2/boarding_passes/{campaign_id}/passes
```

Request payload:

```json
{
  "pass": {
    "secondary_fields": [
      {
        "key": "passenger",
        "value": "John Appleseed"
      }
    ],
    "auxiliary_fields": [
      {
        "key": "boardingTime",
        "value": "2:25 PM"
      },
      {
        "key": "class",
        "value": "Coach"
      }
    ]
  }
}
```

Response:

```json
{
  "id": "7d131a35-66df-4fc2-9d78-b5373558ffd9",
  "campaign_id": "485d2a26-efc5-4f85-8855-fa2f4b6cd2e2",
  "voided": false,
  "serial_number": "51950d75-5d4a-48fc-a187-2f4d5a577ae2",
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
  "header_fields": [
    {
      "key": "gate",
      "value": "A3",
      "label": "GATE"
    }
  ],
  "primary_fields": [
    {
      "key": "depart",
      "value": "SFO",
      "label": "SAN FRANCISCO"
    },
    {
      "key": "arrive",
      "value": "JFK",
      "label": "NEW YORK"
    }
  ],
  "secondary_fields": [
    {
      "key": "passenger",
      "value": "John Appleseed",
      "label": "PASSENGER"
    }
  ],
  "auxiliary_fields": [
    {
      "key": "boardingTime",
      "value": "2:25 PM",
      "label": "DEPART"
    },
    {
      "key": "flightNewName",
      "value": "815",
      "label": "FLIGHT"
    },
    {
      "key": "class",
      "value": "Coach",
      "label": "DESIG."
    },
    {
      "key": "date",
      "value": "7/22",
      "label": "DATE"
    }
  ],
  "back_fields": [],
  "locations": [],
  "beacons": [],
  "page_url": "http://get.passworks.io/G1mbmsPWkw/ajcAj0bCaN4LxN3FjcHn2Q",
  "pkpass_url": "http://get.passworks.io/G1mbmsPWkw/ajcAj0bCaN4LxN3FjcHn2Q.pkpass",
  "created_at": "2015-04-01T10:29:34Z",
  "updated_at": "2015-04-01T10:29:34Z"
}
```

Updating the Boarding Pass of John Appleseed
------------

As mentioned before, updating a specific pass ensures that the personalization you defined at pass creation, will be preserved, unless, of course, you specifically overwrite those fields.


```shell
POST /v2/boarding_passes/{campaign_id}/passes/{pass_id}
```

Request payload:

```json
{
  "pass": {
    "auxiliary_fields": [
      {
        "key": "boardingTime",
        "value": "3:25 PM"
      }
    ]
  }
}
```

Response:

```json
{
  "id": "7d131a35-66df-4fc2-9d78-b5373558ffd9",
  "campaign_id": "485d2a26-efc5-4f85-8855-fa2f4b6cd2e2",
  "voided": false,
  "serial_number": "51950d75-5d4a-48fc-a187-2f4d5a577ae2",
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
  "header_fields": [
    {
      "key": "gate",
      "value": "A3",
      "label": "GATE"
    }
  ],
  "primary_fields": [
    {
      "key": "depart",
      "value": "SFO",
      "label": "SAN FRANCISCO"
    },
    {
      "key": "arrive",
      "value": "JFK",
      "label": "NEW YORK"
    }
  ],
  "secondary_fields": [
    {
      "key": "passenger",
      "value": "John Appleseed",
      "label": "PASSENGER"
    }
  ],
  "auxiliary_fields": [
    {
      "key": "boardingTime",
      "value": "3:25 PM",
      "label": "DEPART"
    },
    {
      "key": "flightNewName",
      "value": "815",
      "label": "FLIGHT"
    },
    {
      "key": "class",
      "value": "Coach",
      "label": "DESIG."
    },
    {
      "key": "date",
      "value": "7/22",
      "label": "DATE"
    }
  ],
  "back_fields": [],
  "locations": [],
  "beacons": [],
  "page_url": "http://get.passworks.io/G1mbmsPWkw/ajcAj0bCaN4LxN3FjcHn2Q",
  "pkpass_url": "http://get.passworks.io/G1mbmsPWkw/ajcAj0bCaN4LxN3FjcHn2Q.pkpass",
  "created_at": "2015-04-01T10:29:34Z",
  "updated_at": "2015-04-01T10:30:41Z"
}
```

Sending a push notification (or forcing a pass update)
------------

You can force the retrieval of a pass via push notification by simply calling the following URL:

```shell
POST /v2/event_tickets/{campaign_id}/passes/{pass_id}/push
```

You can also send a custom message that will be displayed in the lock screen via push notification sending the following content in the above request

```json
{
	"pass": {
		"push_message": "Boarding time changed."
	}
}
```

Response:

You'll get a contextualized message, informing on the start of the pass update, or that there are no passes to be updated.

```json
{
	"message": "push notifications sent for pass with id: 7d131a35-66df-4fc2-9d78-b5373558ffd9 on campaign 'Skyport Airways flight 815'"
}
```


Redeeming a pass
------------

There are two ways you can redeem a pass:

- Redeeming a pass by referencing a redeem code
	You can redeem a pass by referencing a redeem code (instead of the pass_id) by POSTing to the campaign `redeem` route

	```shell
	/v2/boarding_passes/{campaign_id}/redeem
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
	POST /v2/boarding_passes/{campaign_id}/passes/{pass_id}/redeem
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

#####Get all the Boarding Pass campaigns:
```shell
GET /v2/boarding_passes/
```

#####Get all the passes for a specific Boarding Pass campaign:
```shell
GET /v2/boarding_passes/{campaign_id}/passes
```

#####Get a pass's id from its redeem code
```shell
GET /v2/boarding_passes/{campaign_id}/redeem/{redeem_code}
```

#####Get campaigns statistics
```shell
GET /v2/boarding_passes/{campaign_id}/statistics
```

```shell
GET /v2/boarding_passes/{campaign_id}/statistics/totals
```

For more information about the campaign statistcs, please check our [Statistics Documentation](https://github.com/passworks/passworks-api/blob/master/v2/sections/statistics.md).