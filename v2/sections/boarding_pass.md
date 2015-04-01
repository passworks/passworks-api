Boarding Passes
================

Boarding passes can be **airplane**, **bus**, **train**, or **boat tickets**. You also can create generic boarding passes.

Examples of Boarding Passes
------------


| ![img1](https://raw.githubusercontent.com/passworks/passworks-api/master/v2/assets/images/boarding_pass/boarding_pass_2x.png) | ![img2](https://raw.githubusercontent.com/passworks/passworks-api/master/v2/assets/images/boarding_pass/skyport_airways_boarding_pass_guidelines.png) |
|---|---|
| Generic Boarding Schematic | Skyport Airways (Flight 815) |


Creating a Airplane Boarding Pass Campaign for "Skyport Airways" flight 815
------------

````shell
POST /v2/boarding_passes/
```

Payload:

```json
{
  "boarding_pass": {
    "name": "Skyport Airways flight 815",
    "icon_id": "cecd7470-2ba8-4737-afe0-30d0cd4fd00c",
    "logo_id": "eb66127b-cbb7-41f4-b7ea-a6b8c106fead",
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
format | string | Optional. Must be one of the following if supplied: **qrcode**, **pdf417**, **aztec**, or **none**. | qrcode
message | string | Optional. Message encoded in the barcode. | Pass's redeem code.


Updating the "Skyport Airways" flight 815 Campaign
------------

Let's imagine that the gate of the flight changed, and you wish to update all of the campaign's passes. To do so, you will need to issue a PATCH to the following URL with this example payload:

```shell
PATCH /v2/boarding_passes/{boarding_pass_id}
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
    ],
	}
}
```

Response:

```json
```

Now that you've updated your campaign, all the future passes generated from this updated campaign will contain the new changes.

**NOTE:** The following instructions will reset all the issued passes to the base template, removing the personalization fields from all the issued passes.

The correct way of updating the already issued passes while preserving the custom fields (like the name of the pass owner, for example) is to iterate trough the issued pass collection, by collecting the ids from 
`GET /v2/boarding_passes/{campaign_id}/passes`

and then [updating each pass](#updating-each-pass) with the fields you wish to change.

Please contact support@passworks.io for advisement on updating a boarding_pass campaign.

If, however any old passes that had already been generated and you wish to reset them to the new changes, you **must**, following a campaign update, issue a push POST request:

```shell
POST /v2/boarding_passes/{boarding_pass_id}/push
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

```json
```

|  Field name  | Type |  Description   | Default |
|--------------|------|----------------|---------|
push_message | string | Optional. Text shown on the lock screen. | No message sent.

This request will push all existing passes once again, guaranteeing that all that have been downloaded will contain the new changes. Otherwise, there's no guarantee that the users will receive the updated pass.


Creating a Boarding Pass for "John Appleseed"
------------


```shell
POST /v2/boarding_passes/{boarding_passes_id}/passes
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
```

Updating the Boarding Pass of John Appleseed
------------

As mentioned before, updating a specific pass ensures that the personalization you defined at pass creation, will be preserved, unless, of course, you specifically overwrite those fields.


```shell
POST /v2/boarding_passes/{boarding_passes_id}/passes/{pass_id}
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

Aditional routes available
------------

Get all the Boarding Pass campaigns:
```shell
GET /v2/boarding_passes/
```

Get all the passes for a specific Boarding Pass campaign:
```shell
GET /v2/boarding_passes/{campaign_id}/passes
```

