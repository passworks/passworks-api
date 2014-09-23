Loyalty
================


The Loyalty API can be used to create loyalty or event tier programs to reward your customers for using your services.


Example of Loyalty passes
------------

PLEASE PLACE HERE THE SAMPLE PASS IMAGES

Creating a Loyalty Group
------------


```shell
POST /v1/loyalty/
```

POST Content

```json
{
  "campaign": {
    "name": "starbucks card",
    "icon_id": "75217291-d227-40d8-a741-4df9a4baf915",
    "logo_text": "Starbucks Card",
    "header_fields": [
      {
        "key": "balance",
        "label": "Balance"
      }
    ],
    "strip_id": "aab705bb-5bf0-4c14-93e0-f5fe01a4d3f5",
    "background_color": "#0505ff",
    "text_color": "#ffffff",
    "label_color": "#cccccc",
    "barcode": "pdf417",
    "secondary_fields": [
      {
        "key": "username",
        "label": "Name"
      }
    ]
  }
}
```

In case of success HTTP 201 response code is returned with the following body content:

```json
{
  "campaign": {
    "id": "0c2272b8-b48b-44b8-b697-37f6fd41d481",
    "name": "starbucks card",
    "logo_text": "Starbucks Card",
    "background_color": "#0505ff ",
    "text_color": "#ffffff ",
    "label_color": "#cccccc ",
    "header_fields": [
      {
        "key": "balance",
        "value": "",
        "label": "Balance"
      }
    ],
    "secondary_fields": [
      {
        "key": "username",
        "value": "",
        "label": "Name"
      }
    ],
    "auxiliary_fields": [],
    "back_fields": [],
    "beacons": [],
    "locations": [],
    "created_at": "2014-09-23T15:20:21Z",
    "updated_at": "2014-09-23T15:20:21Z"
  }
}
```

NOTE: All date fields (`created_at`, `updated_at`) are in the [ISO8601](http://en.wikipedia.org/wiki/ISO_8601) format for example: 2014-09-22T20:51:53+00:00


##### Available fields

|  Field name  | Type | Description  |
|-------------|------|-----------------------------------
| name | string | Required. The loyaty program name must be unique
| description | string | Required. Brief description of the pass, used by the iOS accessibility technologies.
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
| certificate_id | uuid | Required. The certificate uuid if not supplied a passworks.io default certificate is used
| organization_name | string | optional. Organization name showned in the unlock screen, if none is supplied the your current organization name is used


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

Creating a loyaty pass for a customer
------------

```shell
POST /v1/loyalty/{event-ticket-id}/passes
```

POST Content

```json
{
  "pass": {
    "header_fields": [
      {
        "key": "balance",
        "value": "$20.75"
      }
    ],
    "secondary_fields": [
      {
        "key": "user_name",
        "label": "My Card"
      }
    ],
    "merge": true
  }
}
```

In case of success HTTP 201 response code is returned with the following body content:

```json
{
  "loyalty_card": {
    "campaign_id": "75217291-d227-40d8-a741-4df9a4baf915",
    "pass_id": "ce7e7800-d2c5-4080-9032-9b4a06370bcc",
    "donwload_page_link": "http://get.passworks.io/9hpHLuq_TQ/ovm4e5GsAvhhA4Ynt8YMOA",
    "direct_link": "http://get.passworks.io/9hpHLuq_TQ/ovm4e5GsAvhhA4Ynt8YMOA.pkpass"
  }
}
```



