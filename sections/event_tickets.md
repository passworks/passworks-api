Event Ticket
================


Event Tickets are passes used for events such as concerts, movie tickets, galas, meetings or other types of activity that happen in a specific time or day.


Example of Event Tickets
------------


Creating a Event Ticket group
------------


```shell
POST /v1/event-tickets/
```

```json
{
	"name": "My birthday party",
	"icon_id": "f2faadec-13f2-4cf2-8297-2b85e8a2cae3"
}
```

|  Field name  | Type | Description  |
|-------------|------|-----------------------------------
| name | string | Required. The loyaty program name must be unique
| icon_id | uuid | Required. Icon  id (the id of a icon type asset)
| logo_id | uuid | Optional. Logo image id (the id of a logo type asset)
| strip_id | uuid | Optional. Strip image id (the id of a logo type asset)
| logo_text | string | Optional. Top card text
| header_fields | array | Optional. Collection of *field hash objects*
| secondary_fields | array | Optional. Collection of *field hash objects*
| auxiliary_fields | array | Optional. Collection of *field hash objects*
| back_fields | array | Optional. Collection of *field hash objects* used in the rear part of the pass
| locations | array | Optional. Collection of up to 10 *location hash objects*
| beacons | array | Optional. Collection of up to 10 *beacon hash objects* 
| background_color| rgb string | Required. Color defining the pass background color ranging from `#00000` to `#ffffff`
| text_color | rgb string | Required. The text color for all the `value` fields except primary_fields, ranging from `#00000` to `#ffffff`
| label_color | rgb string | Required. The text color for all `label` fields except primary_fields, ranging from `#00000` to `#ffffff` 
| certificate_id | uuid | Required. The certificate uuid if not supplied a passworks.io default certificate is used 
| description | string | Required. Used for accessibility reasons, provide a description of your pass


##### Location hash object format

```json
{
	"altitude": 0.0
	"latitude": 0.0
	"longitude": 0.0
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
	"major": 0.0
	"minor": 0.0
	"proximity_uuid": "30b5d792-48c9-4f12-80ff-082cae62e80f"
	"relevant_text": "notification to display"
}
```
|  Field name  | Type |  Description  |
|--------------|------|----------------|
major| 16-bit unsigned integer | Optional. Major identifier of a Bluetooth Low Energy location beacon
minor| 16-bit unsigned integer | Optional. Minor identifier of a Bluetooth Low Energy location beacon
proximity_uuid| string | Required. Unique identifier of a Bluetooth Low Energy location beacon
relevant_text| string | Optional. Text displayed on the lock screen when the pass is currently relevant. For example, a description of the nearby