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
