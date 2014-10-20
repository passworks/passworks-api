Boarding Passes
================

Boarding passes can be **airplane**, **bus**, **train**, or **boat tickets**. You also can create generic boarding passes.

Examples of Boarding Passes
------------


| ![img1](https://raw.githubusercontent.com/passworks/passworks-api/master/assets/images/boarding_pass/boarding_pass_2x.png) | ![img2](https://raw.githubusercontent.com/passworks/passworks-api/master/assets/images/boarding_pass/skyport_airways_boarding_pass_guidelines.png) |
|---|---|
| Generic Boarding Schematic | Skyport Airways (Flight 815) | 


Creating a Airplane Boarding Pass "Campaign" for "Skyport Airways" fight 815
------------

````shell
POST /v1/boarding_passes/
```

Payload:

```json
{
  "boarding_pass": {
    "name": "Skyport Airways flight 815",
    "icon_id": "cecd7470-2ba8-4737-afe0-30d0cd4fd00c",
    "logo_id": "eb66127b-cbb7-41f4-b7ea-a6b8c106fead",
    "barcode": "pdf417",
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
{
  "id": "3ca93a6c-c822-4dee-b867-5c9f4b25a2a5",
  "name": "Skyport Airways flight 815",
  "description": "Skyport Airways flight 815",
  "icon_id": "cecd7470-2ba8-4737-afe0-30d0cd4fd00c",
  "logo_id": "eb66127b-cbb7-41f4-b7ea-a6b8c106fead",
  "organization_name": "passworks",
  "transit_type": "air",
  "logo_text": "Skyport Airways",
  "background_color": "#325bb9",
  "text_color": null,
  "label_color": "",
  "header_fields": [
    {
      "key": "gate",
      "value": "23",
      "label": "GATE"
    }
  ],
  "primary_fields": [
    {
      "key": "depart",
      "value": "SFO",
      "label": "SAN FRANCISCO"
    },
    {
      "key": "arrive",
      "value": "JFK",
      "label": "NEW YORK"
    }
  ],
  "secondary_fields": [
    {
      "key": "passenger",
      "value": "",
      "label": "PASSENGER"
    }
  ],
  "auxiliary_fields": [
    {
      "key": "boardingTime",
      "value": "",
      "label": "DEPART"
    },
    {
      "key": "flightNewName",
      "value": "815",
      "label": "FLIGHT"
    },
    {
      "key": "class",
      "value": "",
      "label": "DESIG."
    },
    {
      "key": "date",
      "value": "7/22",
      "label": "DATE"
    }
  ],
  "back_fields": [],
  "locations": [],
  "beacons": [],
  "created_at": "2014-09-26T16:05:13Z",
  "updated_at": "2014-09-26T16:05:13Z"
}
```


##### Available fields

|  Field name  | Type | Description  |
|-------------|------|-----------------------------------
| name | string | Required. Must be unique, it's used to identify the Boarding Pass "Campaign"
| description | string | Optional. Brief description of the pass, used by the iOS accessibility technologies. If the description is not provided the *name* field value is used instead.
| transit_type | string | Required. Must be one of the following values `air`, `boat`, `train`, `boat` or `generic`
| icon_id | uuid | Required. Icon  id (the id of a icon type asset)
| logo_id | uuid | Optional. Logo image id (the id of a logo type asset)
| footer_id | uuid | Optional. Footer image id (the id of a logo type asset)
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



Creating a Boarding Pass for "John Appleseed"
------------


```shell
POST /v1/boarding_passes/{boarding_passes_id}/passes
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
{
  "id": "a42d3503-11c2-4b4f-adfc-9e4ed6e146ba",
  "boarding_pass_id": "3ca93a6c-c822-4dee-b867-5c9f4b25a2a5",
  "voided": false,
  "authentication_token": "_fVGtDHG1oRm9QY5tml_0Q",
  "serial_number": "778161b7-4fc6-47df-9ec8-65d0b2d24244",
  "transit_type": "air",
  "header_fields": [
    {
      "key": "gate",
      "label": "GATE",
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
      "label": "PASSENGER",
      "value": "John Appleseed"
    }
  ],
  "auxiliary_fields": [
    {
      "key": "boardingTime",
      "label": "DEPART",
      "value": "2:25 PM"
    },
    {
      "key": "flightNewName",
      "label": "FLIGHT",
      "value": "815"
    },
    {
      "key": "class",
      "label": "DESIG.",
      "value": "Coach"
    },
    {
      "key": "date",
      "label": "DATE",
      "value": "7/22"
    }
  ],
  "back_fields": [],
  "barcode": {
    "format": "pdf417",
    "message": "0000001",
    "alt_text": "0000001"
  },
  "beacons": [],
  "locations": [],
  "redeemed_count": 0,
  "donwload_page_link": "https://get.passworks.io/1lV7wnDr8Q/fb9-_LvhFtBYuN5D5Vgi7g",
  "direct_link": "https://get.passworks.io/1lV7wnDr8Q/fb9-_LvhFtBYuN5D5Vgi7g.pkpass",
  "expiration_date": null,
  "redeemed_at": null,
  "created_at": "2014-09-26T16:24:45Z",
  "updated_at": "2014-09-26T16:24:45Z"
}
```

Updating the Boarding Pass
------------


```shell
POST /v1/boarding_passes/{boarding_passes_id}/passes/{pass_id}
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
{
  "id": "a42d3503-11c2-4b4f-adfc-9e4ed6e146ba",
  "boarding_pass_id": "3ca93a6c-c822-4dee-b867-5c9f4b25a2a5",
  "voided": false,
  "authentication_token": "_fVGtDHG1oRm9QY5tml_0Q",
  "serial_number": "778161b7-4fc6-47df-9ec8-65d0b2d24244",
  "transit_type": "air",
  "header_fields": [
    {
      "key": "gate",
      "label": "GATE",
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
      "label": "PASSENGER",
      "value": "John Appleseed"
    }
  ],
  "auxiliary_fields": [
    {
      "key": "boardingTime",
      "label": "DEPART",
      "value": "3:25 PM"
    },
    {
      "key": "flightNewName",
      "label": "FLIGHT",
      "value": "815"
    },
    {
      "key": "class",
      "label": "DESIG.",
      "value": "Coach"
    },
    {
      "key": "date",
      "label": "DATE",
      "value": "7/22"
    }
  ],
  "back_fields": [],
  "barcode": {
    "format": "pdf417",
    "message": "0000001",
    "alt_text": "0000001"
  },
  "beacons": [],
  "locations": [],
  "redeemed_count": 0,
  "donwload_page_link": "https://get.passworks.io/1lV7wnDr8Q/fb9-_LvhFtBYuN5D5Vgi7g",
  "direct_link": "https://get.passworks.io/1lV7wnDr8Q/fb9-_LvhFtBYuN5D5Vgi7g.pkpass",
  "expiration_date": null,
  "redeemed_at": null,
  "created_at": "2014-09-26T16:24:45Z",
  "updated_at": "2014-09-26T16:29:42Z"
}
```

