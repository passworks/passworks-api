Templates
===============

Whenever you create a campaign, a template is automatically generated, based on your parameters. You can verify this in the response, listed as `template_id`.

When you update a campaign and it has modifications to template-related fields, a new template is generated reflecting the changes.

All these templates can be used later, by referring them by their id, and including it on the POST and PATCH calls you make to the campaigns, by including the `template_id` element on your payload.



Listing the templates
----------------

```shell
GET /v2/templates
```

Response:

```json
[
  {
    "id": "9f568e52-4916-4105-8222-1834b5399e65",
    "name": "Template for valid campaign-3",
    "description": "Valid Campaign Description",
    "pass_type": "Coupon",
    "logo_text": "",
    "background_color": "#098765",
    "text_color": "#123456",
    "label_color": "#456789",
    "barcode": {
      "format": "qrcode",
      "message": "",
      "alt_text": ""
    }
  },
  {
    "id": "affa9de3-02e1-4b6f-8811-4c4199c7d332",
    "name": "Template for valid campaign",
    "description": "Valid Campaign Description",
    "pass_type": "Coupon",
    "logo_text": "Valid Campaign",
    "background_color": "#098765",
    "text_color": "#123456",
    "label_color": "#456789",
    "barcode": {
      "format": "none",
      "message": "",
      "alt_text": ""
    }
  },
  {
    "id": "d406d43e-59c8-485b-84b3-52ea37373ca7",
    "name": "Template for valid campaign-1",
    "description": "Valid Campaign Description",
    "pass_type": "Coupon",
    "logo_text": "Valid Campaign",
    "background_color": "#098765",
    "text_color": "#123456",
    "label_color": "#456789",
    "barcode": {
      "format": "qrcode",
      "message": "",
      "alt_text": ""
    }
  },
  {
    "id": "e7785224-1953-49f0-84bb-5372cd2f674c",
    "name": "Template for valid campaign-3-1-1",
    "description": "Valid Campaign Description",
    "pass_type": "Coupon",
    "logo_text": "",
    "background_color": "#098765",
    "text_color": "#123456",
    "label_color": "#456789",
    "barcode": {
      "format": "qrcode",
      "message": "",
      "alt_text": ""
    }
  }
]
```

Getting a specific template
----

```shell
GET /v2/templates/{template_id}
```

Response:

```json
{
  "id": "e7785224-1953-49f0-84bb-5372cd2f674c",
  "name": "Template for valid campaign-3-1-1",
  "description": "Valid Campaign Description",
  "pass_type": "Coupon",
  "logo_text": "",
  "background_color": "#098765",
  "text_color": "#123456",
  "label_color": "#456789",
  "barcode": {
    "format": "qrcode",
    "message": "",
    "alt_text": ""
  }
}
```


Creating a template
----

```shell
POST /v2/templates/
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
| name | string | Required. Must be unique, it's used to identify the Template
| description | string | Optional. Brief description of the template.
| pass_type | string | Required. Can be one of the following: ['boardingPass', 'coupon', 'eventTicket', 'storeCard', 'generic']
| transit_type | string | Required. Only required IF pass_type is 'boardingPass'.

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

Payload:

```json
{
  "template": {
    "name": "Template for valid campaign-3-1-1",
    "description": "My lovely template!",
    "pass_type": "Coupon",
    "icon_id": "e7785224-1953-49f0-84bb-5372cd2f674d"
  }
}
```

Response:

```json
{
  "id": "469ff1fd-04de-494f-bf89-eda4f96c3a80",
  "name": "Template for valid campaign-3-1-1",
  "description": "My lovely template!",
  "pass_type": "coupon",
  "logo_text": null,
  "background_color": null,
  "text_color": null,
  "label_color": null,
  "barcode": {
    "format": "none",
    "message": "",
    "alt_text": "",
    "alt_text_type": "mirror"
  },
  "source": "api",
  "icon_id": "47107096-3f26-4b85-8225-791dcccb4dbb",
  "logo_id": null,
  "strip_id": null
}
```
