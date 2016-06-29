# Campaign Statistics


There is two ways to retrieve statistics abour your campaign. You can have it either
by period (grouped by day) or a totalization since the beginning of the campaign.

## Period Statistics

You can retrieve a daily basis statistics by request the `campaign_id/statistics` eg:

```
GET http://api.passworks.io/v2/coupons/86d1772e-ac76-4be0-8844-0f54353307ba/statistics
```

```
GET http://api.passworks.io/v2/coupons/86d1772e-ac76-4be0-8844-0f54353307ba/statistics?start_date=2016-06-01&end_date=2016-06-10
```

### Parameters

| Parameter | Format | Default |
|-------------|------|------------
| start_date | YYYY-MM-DD | 1 month before the current date |
| end_date | YYYY-MM-DD | The current date |


> Any other format (or invalid date) is going to raise an error

The output will return as follows:

```
{
  "campaign_id": "86d1772e-ac76-4be0-8844-0f54353307ba",
  "start_date": "2010-10-10",
  "end_date": "2016-06-29",
  "statistics": {
    "2016-06-28": {
      "installs_count": 0,
      "uninstalls_count": 0,
      "redeems_count": 0,
      "fetches_count": 0,
      "downloads_count": 0,
      "views_count": 0,
      "creates_count": 0,
      "expires_count": 0,
      "pushes_count": 0,
      "updates_count": 0,
      "webhooks_count": 0,
      "api_calls_count": 0,
      "distribution_updates_count": 1,
      "i": {
        "ios": 0,
        "android": 0,
        "wp": 0
      },
      "u": {
        "ios": 0,
        "android": 0,
        "wp": 0
      },
      "active_count": 0,
      "removed_count": 0
    }
  }
}
```

> the "i" and "u" stands for __Installs__ and __Uninstalls__ respectively

## Totals

If you need a totalization for any specific campaign you can request `campaign_id/statistics/totals` as:

```
GET http://api.passworks.io/v2/coupons/86d1772e-ac76-4be0-8844-0f54353307ba/statistics/totals
```

For this endpoint you don't have to pass any parameter, as it is going to compute all
information since the creation of the campaign.

The output will return as follows:

```
{
  "campaign_id": "86d1772e-ac76-4be0-8844-0f54353307ba",
  "statistics": {
    "installs_count": 0,
    "uninstalls_count": 0,
    "redeems_count": 0,
    "fetches_count": 0,
    "downloads_count": 0,
    "views_count": 0,
    "creates_count": 0,
    "expires_count": 0,
    "pushes_count": 1,
    "updates_count": 1,
    "webhooks_count": 0,
    "api_calls_count": 0,
    "distribution_updates_count": 1,
    "active_count": 0,
    "removed_count": 0
  }
}
```
