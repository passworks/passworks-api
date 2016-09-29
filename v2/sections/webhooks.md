# Webhooks

## Context

Passworks Platform has the ability to handle [webhooks](https://en.wikipedia.org/wiki/Webhook).

This allows you to specify an endpoint URL to be called for Pass event (the webkhook URL supports SSL if the URL starts with `https`, it's recommended to **always** use HTTPS endpoints).

Login in to the [Passworks Platform](http://passworks.io/api_index) and set the WebHooks endpoint / URL in the **API & WebHooks** menu.


## Events 

The following events are monitored and sent to the the endpoint via HTTP POST:

| Event name      | Description    |
|-------------|----------------|
| created     | Pass was created |
| downloaded  | Pass was downloaded on the user's device |
| installed   | Pass was installed on the user's device |
| fetched     | User device fetched the pass from the server |
| redeemed    | Pass was redeemed |
| uninstalled | Pass was uninstalled from the user's device |


## Authentication

In each webhook POST call Passworks Platfform will send the `Authorization` header with your organizations API key.


The authentication is optional, you can ignore the header and accept all requests to your webhooks endpoint, but this is not recomended.

Please note that you can find your API KEY here `http://passworks.io/api_index` (the API key is the value that we will be sending in the Authorization header).


## Content of the webhook

The content of the the webhook payload is serialized in JSON . This means that you we send the header `Content-Type: application/json; charset=utf-8`.

Please note that the HTTP method that is going to be used is `POST`.

The following text is an example of the webhook payload (body of the POST):


```json
{
  "event": "installed",
  "context": "pass",
  "campaign_id": "cbc3016c-4c55-4564-81e9-a21664817be2",
  "distribution_id": "723ed9c3-5909-4a12-9810-c58047d9feef",
  "pass_id": "d91aef7c-a166-4694-bb91-569714f9c33e",
  "voided": false,
  "serial_number": "9c05fa25-199b-4c5b-9242-4b42103138a7",
  "redeemed_count": 0,
  "redeemed_at": null,
  "created_at": "2016-08-10T11:29:08Z",
  "updated_at": "2016-08-10T11:29:09Z",
  "last_fetched_at": null,
  "event_at": "2016-08-10T11:30:06Z",
  "metadata": {},
  "event_extra": {
    "pass_id": "d91aef7c-a166-4694-bb91-569714f9c33e",
    "registration_id": "00f537be-f153-46ad-a980-bbddcb9002c3",
    "device_os": "ios",
    "device_app_vendor": "passbook",
    "wallet_type": "apple_wallet",
    "ip": "192.168.1.206"
  }
}
```


Details of the webhook payload:



| Attribute | Format | Example | Description |
|-----------|--------|---------|-------------|
| event| String | "`installed`" | The `event` that this webhook refers to. It can be "`created`", "`downloaded`", "`installed`", "`fetched"`, "`redeemed`", "`uninstalled`",.
| context| String | "pass" | The context for now is only "Pass", it's the events context       
| campaign_id| UUIDv4 (String) | "b6179ee0-e753-403c-b0f7-5f4818e65b02" | This is the `campaign_id` there the passe belongs.
| distribution_id| UUIDv4 (String) | "b792d7fa-193f-4ec7-8dc8-d3069a5b8e1c" | This is the `distribution_id`
| pass_id| UUIDv4 (String) | "b6179ee0-e753-403c-b0f7-5f4818e65b02" | 
| voided| Boolean (default: `false`) | false | Indicated if the pass is redeemable, if voided user can't redeem the pass |
| serial_number| UUIDv4 (String) | "4b708882-dfd0-407f-9354-f70aa159008b" | Serial Number of the pass  |
| redeemed_count| Integer (default: `0`) | 1 | Number of this the pass was redeemed.
| redeemed_at| Date Time in `ISO 8601` (default: `null`) | null | Last date that the pass was redeemed. `null` if never redeemed. |
| created_at | Date Time in `ISO 8601` (default: `null`) | 2015-07-08T09:13:14Z | The `datetime` that the pass was created |
| updated_at | Date Time in `ISO 8601` (default: `null`) | 2015-07-08T09:13:14Z | The `datetime` that the pass was updated |
| last\_fetched\_at| Date Time in `ISO 8601` (default: `null`) | 2015-07-08T09:13:14Z | The `datetime` that a device fetched the pass from the server |
| event_at| Date Time in `ISO 8601` (default: `null`) | 2015-07-08T09:13:14Z | The `datetime` that the event happened in the server |
| metadata | Hash (default: `{}`) | {} | Reserved for pass metadata, usually seen when pass is generated using a query string. |
| event_extra | Hash (default: `{}`) | {} | Internal extra arguments passed to the event on trigger. |
