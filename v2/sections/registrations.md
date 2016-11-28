# Registrations

Each time a Pass is installed inside a wallet an Registration event is stored inside the Passworks database.

Each Registration represents an active pass installed inside a wallet so the number of Registrations can change between API requests as users install and remove passes from their wallets.

Registrations are a powerful tool to gatherer insights about the wallets type and operation systems where passes are installed.

Passworks supports the following wallets:

| Wallet Name   | Wallet ID          | URL |
|---------------|------------------|-----------------------------|
| Apple Wallet  | passbook | https://developer.apple.com/wallet/ |
| Android Pay  | google_wallet | https://developers.google.com/save-to-android-pay/ |
| Wallet Passes  | wallet_passes | https://play.google.com/store/apps/details?id=io.walletpasses.android |
| Passworks Wallet*  | passworks_wallet | https://play.google.com/store/apps/details?id=io.passworks.wallet |
| Pass2U Wallet | pass2u | https://play.google.com/store/apps/details?id=com.passesalliance.wallet |
| PassWallet  | passwallet | https://play.google.com/store/apps/details?id=com.attidomobile.passwallet |

* Passworks Wallet has been deprecated in favor of Wallet Passes.


## Registrations per campaign

You can retrieve all registrations for a given campaign (campaign_id) by calling the following endpoint:

```
GET /v2/<campaign_type>/<campaign_id>/registrations
```

The `campaign_type` is one of the following available campaign types: `coupons`,  `event_tickers`, `boarding_passes`, `generics`, `store_cards`


## Registrations per pass

You can also retrieve all registrations tied to specific pass using the following endpoint:


```
GET /v2/<campaign_type>/<campaign_id>/passes/<pass_id>/registrations
```

## Example of registrations response

Calling the campaign registrations or the pass registrations yields a response with the same format.

Here is an example of calling the registrations for a Coupon campaign

```
GET https://api.passworks.io/v2/coupons/bd69162b-8995-4c89-bdca-898fae6050d0/registrations
```

From the example bellow you can see that this campaign as 3 installed passes, two are installed on the "Apple Wallet" (passbook, see the "wallet" attribute) and the third pass is installed on an Android device using the WalletPasses wallet (wallet_passes).

```
[
  {
    "id": "ed2951b4-1127-4a96-a2b1-8a73adb4b2db",
    "pass_id": "22d5b0ed-cc82-4743-a4fb-ee655d928037",
    "wallet": "passbook",
    "device_os": "ios",
    "created_at": "2016-11-09T11:09:00.745Z"
  },
  {
    "id": "01ff7401-ba48-4bc4-90ab-714dac0971fd",
    "pass_id": "b50a5348-27c5-40de-ae4a-5d8436284d65",
    "wallet": "passbook",
    "device_os": "ios",
    "created_at": "2016-11-09T11:11:29.498Z"
  },
  {
    "id": "fe9c5b7a-fd1e-49fd-8467-cd010c28b481",
    "pass_id": "b50a5348-27c5-40de-ae4a-5d8436284d65",
    "wallet": "wallet_passes",
    "device_os": "android",
    "created_at": "2016-11-09T14:29:11.651Z"
  }
]
````
