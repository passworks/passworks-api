Generic Pass
================


Generic passes can be used for anything that don't fit in the other passes categories.


Example of Generic passes
------------

|![img1](https://raw.githubusercontent.com/passworks/passworks-api/master/assets/images/generic/generic_2x.png)|
|:--------------:|
|Generic Pass (schematic)|


| ![img2](https://raw.githubusercontent.com/passworks/passworks-api/master/assets/images/generic/generic_pass_toy_town_guidelines.png) | (missing image) |
|:-------------------:|:----------------:|
| Generic Pass with rectangular barcode | Generic Pass with square barcode |



Creating a Generic "campaign" for the "Toy Town"
------------

For this generic campaign we will have a custom primary field called `member` that will be displaying the child name. A secondary field with the key `subtitle` displaying the signup date and two auxiliary fields displaying the membership level and the favorite toy (called `level `, `favorite `).

In this campaign step we don't include the child's picture because each pass uses it's unique picture of the child.

```shell
POST /v1/generics/
```

```json
{
  "generic": {
    "name": "Toy Town Generic Passes",
    "icon_id": "cecd7470-2ba8-4737-afe0-30d0cd4fd00c",
    "logo_id": "eb66127b-cbb7-41f4-b7ea-a6b8c106fead",
    "logo_text": "Toy Town",
    "barcode": "pdf417",
    "text_color": "#ffffff",
    "background_color": "#c51f1f",
    "primary_fields": [
      {
        "key": "member"
      }
    ],
    "secondary_fields": [
      {
        "key": "subtitle",
        "label": "MEMBER SINCE"
      }
    ],
    "auxiliary_fields": [
      {
        "key": "level",
        "label": "LEVEL"
      },
      {
        "key": "favorite",
        "label": "FAVORITE TOY"
      }
    ]
  }
}
```

Response

```json
{
  "id": "5ba6ad9e-f15d-4fc2-90e7-b2b83a97cf82",
  "name": "Toy Town Generic Passes",
  "description": "Toy Town Generic Passes",
  "icon_id": "cecd7470-2ba8-4737-afe0-30d0cd4fd00c",
  "logo_id": "eb66127b-cbb7-41f4-b7ea-a6b8c106fead",
  "organization_name": "passworks",
  "logo_text": "Toy Town",
  "background_color": "#c51f1f",
  "text_color": "#ffffff",
  "label_color": "#643e2a",
  "header_fields": [],
  "primary_fields": [
    {
      "key": "member",
      "value": "",
      "label": ""
    }
  ],
  "secondary_fields": [
    {
      "key": "subtitle",
      "value": "",
      "label": "MEMBER SINCE"
    }
  ],
  "auxiliary_fields": [
    {
      "key": "level",
      "value": "",
      "label": "LEVEL"
    },
    {
      "key": "favorite",
      "value": "",
      "label": "FAVORITE TOY"
    }
  ],
  "back_fields": [],
  "locations": [],
  "beacons": [],
  "created_at": "2014-09-29T11:36:33Z",
  "updated_at": "2014-09-29T11:36:33Z"
}
```


Creating a Generic Pass for "Johnny Appleseed"
------------

Creating * Johnny's* passe is rather straightforward, we will pass the thumbnail asset (`tumbnaill_id`) with is photo. And supply the remaning \*_fields with the information corresponding to each key.

```shell
POST /v1/generics/{generic_id}/passes
```


```json
{
  "pass": {
    "thumbnail_id": "8de6562c-06dd-4505-8661-280472234ade",
    "primary_fields": [
      {
        "key": "member",
        "value" : "Johnny Appleseed"
      }
    ],
    "secondary_fields": [
      {
        "key": "subtitle",
        "value": "2012"
      }
    ],
    "auxiliary_fields": [
      {
        "key": "level",
        "value": "Platinum"
      },
      {
        "key": "favorite",
        "value": "Trucks"
      }
    ]
  }
}
```

Response:

```json
{
  "id": "523ea1eb-54ff-4759-a0f3-507586aedb40",
  "generic_id": "5ba6ad9e-f15d-4fc2-90e7-b2b83a97cf82",
  "template_id": "53403cc6-8d42-4e81-a422-05f0d99feade",
  "voided": false,
  "authentication_token": "ymWYYmKLyk6WS_hl49hSSg",
  "serial_number": "bf3b7280-f30b-4bd6-9289-d4768744c2eb",
  "header_fields": [],
  "primary_fields": [
    {
      "key": "member",
      "label": "",
      "value": "Johnny Appleseed"
    }
  ],
  "secondary_fields": [
    {
      "key": "subtitle",
      "label": "MEMBER SINCE",
      "value": "2012"
    }
  ],
  "auxiliary_fields": [
    {
      "key": "level",
      "label": "LEVEL",
      "value": "Platinum"
    },
    {
      "key": "favorite",
      "label": "FAVORITE TOY",
      "value": "Trucks"
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
  "download_page_link": "http://get.passworks.io/WuCRpFsXvg/cXVY5Ql4UJ19C0ewlmiDig",
  "direct_link": "http://get.passworks.io/WuCRpFsXvg/cXVY5Ql4UJ19C0ewlmiDig.pkpass",
  "expiration_date": null,
  "redeemed_at": null,
  "created_at": "2014-09-29T11:41:27Z",
  "updated_at": "2014-09-29T11:41:27Z"
}
```

Updating "Johnny Appleseed" Generic Pass
------------
Let's imagine that Johnny's new favorite toys are now *airplanes* so let's update the `favorite` key inside the `auxiliary_fields ` fields with the new value (Airplanes).

```shell
PATCH /v1/generics/{generic_id}/passes/{pass_id}
```

```json
{
	"pass": {
		"auxiliary_fields": [
			{
			 	"key": "favorite",
			 	"value": "Airplanes"
			}
		]
	}
}
```

Response:

```json
{
  "id": "523ea1eb-54ff-4759-a0f3-507586aedb40",
  "generic_id": "5ba6ad9e-f15d-4fc2-90e7-b2b83a97cf82",
  "voided": false,
  "authentication_token": "ymWYYmKLyk6WS_hl49hSSg",
  "serial_number": "bf3b7280-f30b-4bd6-9289-d4768744c2eb",
  "header_fields": [],
  "primary_fields": [
    {
      "key": "member",
      "label": "",
      "value": "Johnny Appleseed"
    }
  ],
  "secondary_fields": [
    {
      "key": "subtitle",
      "label": "MEMBER SINCE",
      "value": "2012"
    }
  ],
  "auxiliary_fields": [
    {
      "key": "level",
      "label": "LEVEL",
      "value": "Platinum"
    },
    {
      "key": "favorite",
      "label": "FAVORITE TOY",
      "value": "Airplanes"
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
  "download_page_link": "http://get.passworks.io/WuCRpFsXvg/cXVY5Ql4UJ19C0ewlmiDig",
  "direct_link": "http://get.passworks.io/WuCRpFsXvg/cXVY5Ql4UJ19C0ewlmiDig.pkpass",
  "assets": {},
  "expiration_date": null,
  "redeemed_at": null,
  "created_at": "2014-09-29T11:41:27Z",
  "updated_at": "2014-09-29T12:58:29Z"
}
```


Deleting "Johnny Appleseed" Generic Pass
------------

```shell
DELETE /v1/generics/{generic_id}/passes/{pass_id}
```

