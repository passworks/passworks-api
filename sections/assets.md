Assets
===============

Assets are the visual elements of the pass.

Passworks supports 6 types of assets (`icon`, `logo`, `strip`, `thumbnail`, `background` and `footer`) each type of passe uses one or more types of assets.

You can reuse assets, meaning that you can assign the same asset to multiple passes, reducing the number of asset operations and also reducing the amount of bandwidth required to create a pass.

Types of assets
----------------

Each pass type (`store card`, `event ticket`, `boarding pass`, `generic pass` and `coupons`) use specific set of assets/images.

| Asset Name |  Used in       | Size
|------------|----------------------------------|----------------------------------|
| icon       | All type of passes               | 118x118 |
| logo		   | All type of passes 		        | 320x100 
| strip	   | Coupon, Event Ticket, Store Card | 640x84 for Event Tickets or 640x246 for other types of passes 
| thumbnail  | Event ticket, Generic | 180x180 The aspect ratio should be in the range of 2:3 to 3:2, otherwise the image is cropped.
| background | Event Ticket | 360x440	        |
| footer	   | Boarding Pass | 286x30           |    

Prefered image format is .png since it supports transparencies.

Maximum upload size if 1 Megabyte (1025 Kb)

Listing the assets
----------------

```shell
GET /v1/assets
```

Response:

```json
{
  "assets": [
    {
      "id": "aab705bb-5bf0-4c14-93e0-f5fe01a4d3f5",
      "asset_type": "strip",
      "created_at": "2014-08-25T14:52:49Z"
    },
    {
      "id": "cecd7470-2ba8-4737-afe0-30d0cd4fd00c",
      "asset_type": "icon",
      "created_at": "2014-09-24T09:38:48Z"
    },
    {
      "id": "eb66127b-cbb7-41f4-b7ea-a6b8c106fead",
      "asset_type": "logo",
      "created_at": "2014-09-24T09:39:40Z"
    }
  ]
}
```

Creating a asset
----------------

Passworks API allows you to upload images in the `.jpg`, `.png` and `.gif` format, note that all the uploads images will be reprocessed and converted to into `png`.

Images must be uploaded using the [base64](http://en.wikipedia.org/wiki/Base64) encoding.


```shell
POST /v1/assets
```

Body payload:


```json
{
  "asset": {
    "filename": "passworks.jpg",
    "content_type": "image/jpeg",
    "base64": "iVBORw0KGgoAAAANSUhEUgAAAA8AAAAPCAMAAAAMCGV4AAAABGdBTUEAALGP\nC/xhBQAAAAFzUkdCAK7OHOkAAAAgY0hSTQAAeiYAAICEAAD6AAAAgOgAAHUw\nAADqYAAAOpgAABdwnLpRPAAAAO1QTFRF/////v//6fbx1O3jzereyOjbyunc\n0ezh3/Lq/P79ltS7VruSZcGbY72YZb6aY76ZZL+aXL6WbsSh7Pfz/v/+/f7+\nzuvfVLqQ5/Xv+/39/v7+fMmqhs2wqNvGgMqswufYbMOgnda/gsut+/79yOnc\nbcai3fHp1u/lacOe5/bwasKeZcCb4/Pt+v38odjC2vDn4/Tt0+3iZsGcrd3J\nKqVzKKRxrd3Kz+vgEpxkhM2vXb6XwubY3/HqYr+ZodjBf8qryOnbqtzHw+fY\nzeveVLmQ5vXve8mpiM6xl9W8Zb6ZW72Vcsak7/n16vbx4PLrTQ8gcgAAAAFi\nS0dEAIgFHUgAAAAJcEhZcwAACxMAAAsTAQCanBgAAACnSURBVAjXbU/XDsIw\nDLyww2qBplBmoZS99y57w/9/DknEE8KWLJ3PPp8BELjcHq/PH6AQQRAMhSNR\nRY3FE9DAoCdTTAOMdCYLyjOXh5hkKJicpyiWYFAGC2WbtzVUqrwIXq8JvXqj\n2Wp3uuihPxB4OBpPprM5FsvV+g//u0+xcWBJ/a0t8c753t+b0t/heBL+KD1f\nBEFw5f5vinp/PKUQwUv+92YcfAAwZRGmNH9JIQAAACV0RVh0ZGF0ZTpjcmVh\ndGUAMjAxNC0wOC0yNlQwNzozMjowOC0wNDowMCJkoiAAAAAldEVYdGRhdGU6\nbW9kaWZ5ADIwMTQtMDgtMjZUMDc6MzI6MDgtMDQ6MDBTORqcAAAAAElFTkSu\nQmCC\n",
    "asset_type": "background"
  }
}
```

| Field Name           | Type      | Description    |
|----------------------|-----------|----------------|
| filename   			   | string    |  Required. The uploaded filename (eg: company-logo.png)
| content_type		   | string	  |  Required. The [mime type](http://en.wikipedia.org/wiki/Internet_media_type) of the uploaded file. Valid mime types are `image/jpeg`, `image/png` and `image/gif`
| base64               | string    | Required. A string in [base64](http://en.wikipedia.org/wiki/Base64) encoding containing the content of the file
| asset_type    		   | string    | Required. The type of asset being uploaded. Valid asset types are `icon`, `logo`, `strip `, `thumbnail`, `background`, `footer`

Response:


```json
{
  "asset": {
    "id": "32f85671-2e12-4a46-9fe2-05435cd5fc14",
    "asset_type": "background",
    "created_at": "2014-09-24T17:41:27Z"
  }
}
```

Deleting a asset
----------------

```shell
DELETE /v1/assets/{asset-id}
```

If the asset is deleted successfully the endpoint returns a HTTP 200.

In case an asset can't be deleted because it's being used by a "campaing" an HTTP 412 error code is returned. 