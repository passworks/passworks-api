# Webhooks

## Context

Passworks Platform has the ability to handle [webhooks](https://en.wikipedia.org/wiki/Webhook) per organization.

This allows you to specify an endpoint URL to be called for Pass event inside a given organization (the webkhook URL supports SSL if the URL starts with `https`, it's recommended to **always** use HTTPS endpoints).

Login in to the [Passworks Platform](http://passworks.io/api_index) and set the WebHooks endpoint / URL in the **API & WebHooks** menu.


## Events 

The following events are monitored and sent to the the endpoint via HTTP POST:

| Event name      | Description    |
|-------------|----------------|
| created     | Pass was created |
| installed   | Pass was installed on the user's device |
| uninstalled | Pass was uninstalled from the user's device |
| fetched     | User device fetched the pass from the server |


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
  "campaign_id": "b6179ee0-e753-403c-b0f7-5f4818e65b02",
  "distribution_id": "b792d7fa-193f-4ec7-8dc8-d3069a5b8e1c",
  "pass_id": "b6179ee0-e753-403c-b0f7-5f4818e65b02",
  "voided ": false,
  "serial_number": "4b708882-dfd0-407f-9354-f70aa159008b",
  "redeemed_count": 0,
  "redeemed_at": null,
  "created_at": "2015-07-08T09:13:14Z",
  "updated_at": "2015-07-08T09:13:14Z",
  "last_fetched_at": "2015-07-08T09:13:14Z",
  "action_at": "2015-07-08T09:13:14Z",
  "metadata": {}
}
```


Details of the webhook payload:



| Attribute | Format | Example | Description |
|-----------|--------|---------|-------------|
| event| String | "`installed`" | The `event` that this webhook refers to. It can be "`installed`", "`created`", "`uninstalled`", "`fetched`.
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
| metadata | Hash (default: `{}`) | {} | Reserved for metadata, actually not used, it's always empty. |