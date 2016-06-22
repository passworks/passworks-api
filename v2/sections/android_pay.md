Android Pay
================


Supported Passes
------------


So far *Android Pay* has release only 3 types of passes. Their concept is upon `Classes` and
`Objects` however, we can make a correlation between those and `Campaigns` and `Passes`.
Throughout all our documentation the terms `Campaigns` and `Passes` are going to be used instead.

| Pass type     | Support    | Correlation     |
|---------------|------------|-----------------|
| Loyalty cards | &#10003;   | Store card      |
| Gift cards    | N/A        | N/A             |
| Offers        | &#10003;   | Coupon          |

So at our platform you'll find:

| Pass type     | Apple Wallet         | Android Pay | Description |
|---------------|----------------------|-------------|-------------|
| Boarding pass |  Boarding Pass       |  N/A        | Boarding passes (train, bus, flights, etc) |
| Coupon        |  Coupon              |  Offer      | Discounts, special offers, gift card, prepaid cards, return credits |
| Event ticket  |  Event Ticket        |  N/A        | Event admission, season tickets, movie tickets. |
| Generic       |  Generic             |  N/A        | Generic passes |
| Store card    |  StoreCard           |  Loyalty    | Loyalty, membership card, photo id, monthly passes|



> For more information about the passes and availability please check our
> [Android Pay](http://help.passworks.io/introduction-android-pay/) documentation

Example
------------

| ![img1](https://raw.githubusercontent.com/passworks/passworks-api/master/v2/assets/images/android_pass/android_schema.png) | ![img2](https://raw.githubusercontent.com/passworks/passworks-api/master/v2/assets/images/android_pass/climb_gym_android_pass.png) |
|---|---|
| Generic Boarding Schematic | Paw Planet Discount |



Fields
------------

#### Request

The only difference from creating a campaign for *Apple Wallet* is the **flag** `gwallet_usage`
that may receive `true` for the supported pass types.

|  Field name  | Type | Description  |
|-------------|------|-----------------------------------
| gwallet_usage | boolean | Optional. Activate *Android Pay* for the campaign.

#### Response


|  Field name  | Type | Description  |
|-------------|------|-----------------------------------
| gwallet_usage | boolean | Activation for *Android Pay*
| gwallet_status | string  | Syncing status
| gwallet_message | string  | Messages (in case of any error)


##### Available statuses


 * *local* - Just created
 * *updated* - Just updated
 * *failed* - Dync failed (check error message)
 * *sync_done* - the campaign was successfuly synchronized with *Android Pay* services
 * *syncing* - The sync is beign done


Errors
------------

Most of the errors that may happen with the synchronization with the *Android Pay* services
are raised by some missing field. Howerver, we mitigate it by creating default values for some
of these fields and, sometimes, just trying the sync again.

Other are raised by any failing over the communication between our and theirs servers.

> We expect no errors being raised for this synchronization process, if happens that you found
> any, please contact us: api@passworks.io


Android Life Cycle
------------


| ![img1](https://raw.githubusercontent.com/passworks/passworks-api/master/v2/assets/images/android_pass/create_sequence.png) | ![img2](https://raw.githubusercontent.com/passworks/passworks-api/master/v2/assets/images/android_pass/update_sequence.png) |
|---|---|
| Creating Campaigns and Passes | Updating Campaigns and Passes |

