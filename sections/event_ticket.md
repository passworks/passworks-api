Event Ticket
================


Event Tickets are passes used for events such as concerts, movie tickets, galas, meetings or other types of activity that happen in a specific time or day.


Example of Event Tickets
------------

|![img1](https://raw.githubusercontent.com/passworks/passworks-api/master/assets/images/event_ticket/event_ticket_2x.png)|
|:--------------:|
|Event Ticket with `background image` and one with a `strip image` (schematic)|



> Note: If you specify a strip image, do not specify a background image nor a thumbnail image.

| ![img2](https://raw.githubusercontent.com/passworks/passworks-api/master/assets/images/event_ticket/the_beat_goes_on_guidelines.png) | (missing image) |
|:-------------------:|:----------------:|
| The Beat Goes On (Event ticket with background and thumbnail image) | Event Ticket with a strip image |



Creating a Event Ticket "Campaign" for "The Beat Goes On" Event
------------

The **Beat Goes On** pass is straightforward example, the pass is the same for all the persons with the minor diference that each issued pass has it's own redeem code (barcode redeem code).

```shell
POST /v1/event_tickets/
```

POST content

```json
{
  "event_ticket": {
    "name": "The Beat Goes On Event",
    "icon_id": "cecd7470-2ba8-4737-afe0-30d0cd4fd00c",
    "thumbnail_id": "8de6562c-06dd-4505-8661-280472234ade",
    "background_id": "3cac4ba6-3f0b-438b-adbf-d0706c6267f8",
    "barcode": "pdf417",
    "text_color": "#ffffff",
    "background_color": "#3c414c",
    "primary_fields": [
      {
        "key": "event_name",
        "label": "EVENT",
        "value": "The Beat Goes On"
      }
    ],
    "secondary_fields": [
      {
        "key": "loc",
        "label": "LOCATION",
        "value": "Moscone West"
      }
    ],
    "locations": [
		{
      		"longitude" : -122.3748889,
      		"latitude" : 37.6189722,
      		"relevant_text": "Welcome! Enjoy the show."
    	}    
    ]
  }
}
```

In case of success HTTP 201 response code is returned with the following body content:

```json
{
    "event_ticket": {
        "id": "6d29a933-98e0-4827-a8ca-9dbccf1474ef",
        "name": "The Beat Goes On Event",
        "description": "The Beat Goes On Event",
        "icon_id": "cecd7470-2ba8-4737-afe0-30d0cd4fd00c",
        "organization_name": "passworks",
        "logo_text": "",
        "background_color": "#3c414c",
        "text_color": "#ffffff",
        "label_color": "",
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
                "latitude": 37.6189722,
                "longitude": -122.3748889,
                "altitude": null,
                "relevant_text": "Welcome! Enjoy the show."
            }
        ],
        "beacons": [],
        "created_at": "2014-09-26T14:16:42Z",
        "updated_at": "2014-09-26T14:16:42Z"
    }
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
| background_id | uuid | Optional. Strip image id (the id of a background type asset)
| thumbnail_id | uuid | Optional. Strip image id (the id of a logo type asset)
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

Required. Must be unique, it's used to identify the Boarding Pass "Campaign"{event_ticket_id}/passes
```

```json
{
  "pass": {
    "barcode": {
      "message": "123456789"
    }
  }
}
```

Response

```json
{
  "pass": {
    "id": "5bf7ff15-0efd-4e5e-9291-4762d8b8a1bd",
    "store_card_id": "6d29a933-98e0-4827-a8ca-9dbccf1474ef",
    "voided": false,
    "authentication_token": "HjEg2ptvS_ZG6xjgXUibqg",
    "serial_number": "35e83baa-df47-4be7-8829-322a37137a4e",
    "header_fields": [],
    "primary_fields": [
      {
        "key": "event_name",
        "label": "EVENT",
        "value": "The Beat Goes On"
      }
    ],
    "secondary_fields": [
      {
        "key": "loc",
        "label": "LOCATION",
        "value": "Moscone West"
      }
    ],
    "auxiliary_fields": [],
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
        "relevant_text": "Welcome! Enjoy the show."
      }
    ],
    "redeemed_count": 0,
    "donwload_page_link": "https://get.passworks.io/gOLp8MFxiA/nopCEC8kUP0kQ6TwC8IZ-g",
    "direct_link": "https://get.passworks.io/gOLp8MFxiA/nopCEC8kUP0kQ6TwC8IZ-g.pkpass",
    "expiration_date": null,
    "redeemed_at": null,
    "created_at": "2014-09-26T14:19:42Z",
    "updated_at": "2014-09-26T14:19:42Z"
  }
}
```

Updating a "The Beat Goes On" Event Ticket
------------

Let's imagine that the location of your event changed, and you wish to update a pass with the new `location`. NOTE: After a successful pass update if you don't pass the `push: false` flag, the system will issue a push notification to that user, notifying him that the pass was updated. 

```shell
PATCH /v1/event_tickets/{event_ticket_id}/passes/{pass_id}
```


```json
{
	"pass": {
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
    "pass": {
        "id": "5bf7ff15-0efd-4e5e-9291-4762d8b8a1bd",
        "store_card_id": "6d29a933-98e0-4827-a8ca-9dbccf1474ef",
        "voided": false,
        "authentication_token": "HjEg2ptvS_ZG6xjgXUibqg",
        "serial_number": "35e83baa-df47-4be7-8829-322a37137a4e",
        "header_fields": [],
        "primary_fields": [
            {
                "key": "event_name",
                "label": "EVENT",
                "value": "The Beat Goes On"
            }
        ],
        "secondary_fields": [
            {
                "key": "loc",
                "label": "LOCATION",
                "value": "Moscone West"
            }
        ],
        "auxiliary_fields": [],
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
                "latitude": 38.725488,
                "longitude": -9.1501,
                "relevant_text": "Welcome! Enjoy the show."
            }
        ],
        "redeemed_count": 0,
        "donwload_page_link": "https://get.passworks.io/gOLp8MFxiA/nopCEC8kUP0kQ6TwC8IZ-g",
        "direct_link": "https://get.passworks.io/gOLp8MFxiA/nopCEC8kUP0kQ6TwC8IZ-g.pkpass",
        "expiration_date": null,
        "redeemed_at": null,
        "created_at": "2014-09-26T14:19:42Z",
        "updated_at": "2014-09-26T14:33:32Z"
    }
}
```

Updating a "The Beat Goes On" Event Ticket
------------

Let's imagine that the location of your event changed, and you wish to update a pass with the new `location`.

```shell
DELETE /v1/event_tickets/{event_ticket_id}/passes/{pass_id}
```

Forcing a push update of a pass
------------

You can force a push notification of a passe (provided that it was changed since the user last fetched it) by using the following URL

```shell
POST /v1/event_tickets/{event_ticket_id}/passes/{pass_id}/push
```
