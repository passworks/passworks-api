# Campaign Reports

There is two ways to retrieve reports about your campaigns. You can have it either by period (grouped by day) or a totalization since the beginning of the campaign.


## Period Report

You can retrieve a daily basis report by request the `/v2/{campaign_type}/{campaign_id}/reports` eg:

#### Without params
```
GET https://api.passworks.io/v2/coupons/86d1772e-ac76-4be0-8844-0f54353307ba/reports
```

#### With params
```
GET https://api.passworks.io/v2/coupons/86d1772e-ac76-4be0-8844-0f54353307ba/reports?start_date=2016-06-01&end_date=2016-06-10
```


### Parameters

| Parameter | Format | Default |
|-----------|--------|---------|
| start_date | YYYY-MM-DD | One month before the current date |
| end_date   | YYYY-MM-DD | The current date |

> Any other format (or an invalid date) is going to raise an error

The output will return as follows:

```
{
  "campaign_id": "86d1772e-ac76-4be0-8844-0f54353307ba",
  "start_date": "2010-10-10",
  "end_date": "2016-06-29",
  "report": {
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

If you need a totalization report for any specific campaign you can request `/v2/{campaign_type}/{campaign_id}/reports/totals` as in:

```
GET https://api.passworks.io/v2/coupons/86d1772e-ac76-4be0-8844-0f54353307ba/reports/totals
```

For this endpoint you don't have to pass any parameter, as it is going to compute all information since the creation of the campaign.

The output will return as follows:

```
{
  "campaign_id": "86d1772e-ac76-4be0-8844-0f54353307ba",
  "report": {
  	 "apple"=>{"installs_count"=>0, "uninstalls_count"=>0},
  	 "android"=>{"installs_count"=>2, "uninstalls_count"=>0},
    "installs_count": 2,
    "uninstalls_count": 0,
    "redeems_count": 0,
    "fetches_count": 0,
    "downloads_count": 0,
    "views_count": 0,
    "creates_count": 2,
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
