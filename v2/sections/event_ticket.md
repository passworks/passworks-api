Event Ticket
================

Event Tickets are passes used for events such as concerts, movie tickets, galas, meetings or other types of activity that happen in a specific time or day.


Example of Event Tickets
------------

|![img1](https://raw.githubusercontent.com/passworks/passworks-api/master/v2/assets/images/event_ticket/event_ticket_2x.png)|
|:--------------:|
|Event Ticket with `background image` and one with a `strip image` (schematic)|



> Note: If you specify a strip image, do not specify a background image nor a thumbnail image.

| ![img2](https://raw.githubusercontent.com/passworks/passworks-api/master/v2/assets/images/event_ticket/the_beat_goes_on_guidelines.png) | (missing image) |
|:-------------------:|:----------------:|
| The Beat Goes On (Event ticket with background and thumbnail image) | Event Ticket with a strip image |



Creating a Event Ticket "Campaign" for "The Beat Goes On" Event
------------

The **Beat Goes On** pass is straightforward example, the pass is the same for all the persons with the minor diference that each issued pass has it's own redeem code (barcode redeem code).

```shell
POST /v2/event_tickets/
```

POST content

```json
{
  "event_ticket": {
    "name": "The Beat Goes On Event",
    "icon_id": "e365088d-27db-4d5e-9915-466d06385426",
    "thumbnail_id": "c1c65182-441c-4ecf-bc9f-2783127de070",
    "background_id": "e725642d-00b8-433c-a967-11b712498488",
    "barcode": {
      "format": "pdf417"
    },
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
      "latitude": 37.6189722,
      "longitude": -122.3748889,
      "altitude": null,
      "relevant_text": "Welcome! Enjoy the show."
    }
  ],
  "beacons": [],
  "page_url": "http://get.passworks.io:3000/1VtFTG8YwQ",
  "created_at": "2015-03-27T13:08:57Z",
  "updated_at": "2015-03-27T13:08:57Z"
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
PATCH /v2/event_tickets/{campaign_id}
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
  "page_url": "http://get.passworks.io:3000/1VtFTG8YwQ",
  "created_at": "2015-03-27T13:08:57Z",
  "updated_at": "2015-03-27T17:49:50Z"
}
```

**NOTE:** The following instructions will reset all the issued passes to the base template, removing the personalization fields from all the issued passes.

The correct way of updating the already issued passes while preserving the custom fields (like the name of the pass owner, for example) is to iterate trough the issued pass collection, by collecting the ids from 
`GET /v2/event_tickets/{campaign_id}/passes`

and then [updating each pass](#updating-each-pass) with the fields you wish to change.

Please contact support@passworks.io for advisement on updating a event ticket campaign.

If, however any old passes that had already been generated and you wish to reset them to the new changes,  you **must**, following a campaign update, issue a push POST request:

```shell
POST /v2/event_tickets/{campaign_id}/push
```

Along with this push, you may also, optionally, send in a payload with a push message that will be presented to the users when the update is done, shown on the lock screen.

```json
{
	"event_ticket": {
	    "push_message": "Venue has changed!"
	}
}
```

|  Field name  | Type |  Description   | Default |
|--------------|------|----------------|---------|
push_message | string | Optional. Text shown on the lock screen. | No message sent.

This request will push all existing passes once again, guaranteeing that all that have been downloaded will contain the new changes. Otherwise, there's no guarantee that the users will receive the updated pass.


Creating a "The Beat Goes On" Event Ticket Pass
------------

In order to create passes, you need to issue a POST request to the following URL:

```shell
POST /v2/event_tickets/{campaign_id}/passes/
```

```json
{
	"pass": {}
}
```

Response:

```json
{
  "id": "5bf7ff15-0efd-4e5e-9291-4762d8b8a1bd",
  "campaign_id": "6d29a933-98e0-4827-a8ca-9dbccf1474ef",
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
  "download_page_link": "https://get.passworks.io/gOLp8MFxiA/nopCEC8kUP0kQ6TwC8IZ-g",
  "direct_link": "https://get.passworks.io/gOLp8MFxiA/nopCEC8kUP0kQ6TwC8IZ-g.pkpass",
  "expiration_date": null,
  "redeemed_at": null,
  "created_at": "2014-09-26T14:19:42Z",
  "updated_at": "2014-09-26T14:33:32Z"
}
```

Updating a "The Beat Goes On" Event Ticket Pass
------------

Let's imagine that the location of your event changed, and you wish to update a pass with the new `location`.


```shell
PATCH /v2/event_tickets/{campaign_id}/passes/{pass_id}
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
  "id": "2e997002-6df6-4cfd-849e-16dcb1f5dd02",
  "campaign_id": "c7aab24b-a076-4e59-885a-726e80ca64e7",
  "voided": false,
  "serial_number": "c2070b68-aa87-487a-ae9a-c99e3f2701f8",
  "redeemed_count": 0,
  "barcode": {
    "format": "qrcode",
    "message": "",
    "alt_text": ""
  },
  "expiration_date": null,
  "max_distance": null,
  "relevant_date": null,
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
      "name": null,
      "altitude": null,
      "latitude": 38.725488,
      "longitude": -9.1501,
      "relevant_text": "Welcome! Enjoy the show."
    }
  ],
  "beacons": [],
  "page_url": "http://get.passworks.io:3000/1VtFTG8YwQ/FCgAWVECzDyuLS-kdvNrpA",
  "pkpass_url": "http://get.passworks.io:3000/1VtFTG8YwQ/FCgAWVECzDyuLS-kdvNrpA.pkpass",
  "created_at": "2015-03-27T18:11:49Z",
  "updated_at": "2015-03-27T18:12:20Z"
}
```

Forcing a push update of a pass
------------

You can force the update of a pass via push notification by simply calling the following URL:

```shell
POST /v2/event_tickets/{campaign_id}/passes/{pass_id}/push
```

You can also send a custom message that will be displayed in the lock screen via push notification sending the following content in the above request

```json
{
	"event_ticket": {
	    "push_message": "Venue has changed!"
	}
}
```

Aditional routes available
------------

Get all the Event Ticket campaigns:
```shell
GET /v2/event_tickets/
```

Get all the passes for a specific Event Ticket campaign:
```shell
GET /v2/event_tickets/{campaign_id}/passes
```

