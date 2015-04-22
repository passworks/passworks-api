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
    "name": "Template for Campaign 1",
    "description": "The description of Template for Campaign 1",
    "pass_type": "coupon",
    "logo_text": "",
    "background_color": "#098765",
    "text_color": "#123456",
    "label_color": "#456789",
    "barcode": {
      "format": "qrcode",
      "message": "",
      "alt_text": ""
    },
    "icon_id": "0e63925f-da0b-46d7-81c4-56fdc78d6120"
  },
  {
    "id": "affa9de3-02e1-4b6f-8811-4c4199c7d332",
    "name": "Template for Campaign 2",
    "description": "The description of Template for Campaign 2",
    "pass_type": "coupon",
    "logo_text": "Valid Campaign",
    "background_color": "#098765",
    "text_color": "#123456",
    "label_color": "#456789",
    "barcode": {
      "format": "none",
      "message": "",
      "alt_text": ""
    },
    "icon_id": "0e63925f-da0b-46d7-81c4-56fdc78d6120",
  },
  {
    "id": "d406d43e-59c8-485b-84b3-52ea37373ca7",
    "name": "Template for Campaign 3",
    "description": "The description of Template for Campaign 3",
    "pass_type": "coupon",
    "logo_text": "Valid Campaign",
    "background_color": "#098765",
    "text_color": "#123456",
    "label_color": "#456789",
    "barcode": {
      "format": "qrcode",
      "message": "",
      "alt_text": ""
    },
    "icon_id": "0e63925f-da0b-46d7-81c4-56fdc78d6120"
  },
  {
    "id": "e7785224-1953-49f0-84bb-5372cd2f674c",
    "name": "Template for Campaign 4",
    "description": "The description of Template for Campaign 4",
    "pass_type": "coupon",
    "logo_text": "",
    "background_color": "#098765",
    "text_color": "#123456",
    "label_color": "#456789",
    "barcode": {
      "format": "qrcode",
      "message": "",
      "alt_text": ""
    },
    "icon_id": "0e63925f-da0b-46d7-81c4-56fdc78d6120"
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
  "name": "Template for Campaign 5",
  "description": "The description of Template for Campaign 5",
  "pass_type": "coupon",
  "logo_text": "",
  "background_color": "#098765",
  "text_color": "#123456",
  "label_color": "#456789",
  "barcode": {
    "format": "qrcode",
    "message": "",
    "alt_text": ""
  },
  "icon_id": "0e63925f-da0b-46d7-81c4-56fdc78d6120"
}
```



Creating a template
----

```shell
POST /v2/templates
```

```json
{
  "id": "b5f3d710-6d02-43b7-880a-75d4e719cbaa",
  "name": "My New Coupon Campaign",
  "description": "My New Coupon Campaign",
  "pass_type": "coupon",
  "logo_text": "",
  "background_color": "#44b084",
  "text_color": "#ffffff",
  "label_color": "#ffffff",
  "barcode": {
    "format": "qrcode",
    "message": "",
    "alt_text": ""
  },
  "icon_id": "0e63925f-da0b-46d7-81c4-56fdc78d6120",
  "logo_id": "dfbd0f8f-c72f-4a1f-95cb-ef293967f02b"
}
```


##### Available fields

|  Field name  | Type | Description  |
|-------------|------|-----------------------------------
| name | string | Required. Must be unique, it's used to identify the Template
| description | string | Optional. Brief description of the pass, used by the iOS accessibility technologies. If the description is not provided the *name* field value is used instead.
| pass_type | String | Required. It must be one of the following values `boardingPass`, `cooupon`, `eventTicket`, `generic` or `storeCard` (for more detail refere to this table [Assets for each pass_type](#assets-for-each-pass_type))
| transit_type | string | Required if `pass_type` is `boardingPass`. Must be one of the following values `air`, `boat`, `train`, `boat` or `generic`.
| icon_id | uuid | Required. Icon  id (the id of a icon type asset)
| logo_id | uuid | Optional. Logo image id (the id of a logo type asset)
| strip_id | uuid | Optional. Strip image id (the id of a logo type asset)
| background_id | uuid | Optional. Background image id (the id of a background type asset)
| footer_id | uuid | Optional. Footer image id (the id of a footer type asset)
| thumbnail_id | uuid | Optional. Thumbnail image id (the id of a thumbnail type asset)
| logo_text | string | Optional. Top card text
| background_color| rgb string | Optional. Color defining the pass background color ranging from `#00000` to `#ffffff`
| text_color | rgb string | Optional. The text color for all the `value` fields except primary_fields, ranging from `#00000` to `#ffffff`
| label_color | rgb string | Optional. The text color for all `label` fields except primary_fields, ranging from `#00000` to `#ffffff`
| barcode | hash | Optional. A single hash of [barcode hash object](#barcode-hash-object-format).


##### Assets for each pass_type 

This table specifies the available assets that you can use for each pass type. (eg: Coupon, Boarding Pass, Store Ticket, Generic, Event Ticket).


| Pass style    | pass_type field  | Supported images     |  Layout           |
| --------------|------------------|-----------------------|----------------- |
| Boarding pass | boardingPass     | logo, icon, footer    |See [Boarding pass](boarding_pass.md)    |
| Coupon        | coupon           | logo, icon, strip     | See [Coupon](coupon.md)   |
| Event ticket  | eventTicket      | logo, icon, strip, background, thumbnail If you specify a strip image, do not specify a background image or a thumbnail.   |  See [Event ticket](event_ticket.md)  |
| Generic       | generic          | logo, icon, thumbnail | See [Generic](generic.md)   |
| Store card    | storeCard        | logo, icon, strip     | See [Store card](store_card.md)   |

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
