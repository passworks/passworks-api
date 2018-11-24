# CHANGELOG

This file is a manually maintained list of changes for each release. Feel free to add your
changes here when sending pull requests. Also send corrections if you spot any mistakes.

## v0.7.0 (2018-11-24)

* Documentation
  - Added ability to merge campaign and send push message to the customer after each pass is updated. (lmmendes)

## v0.6.0 (2017-01-11)

* Documentation
  - Added more sorting endpoints and improved documentation based on sophatar comments (lmmendes)

## v0.6.1 (2017-01-11)

* Documentation
  - Added sorting documentation (lmmendes)

## v0.5.0 (2016-11-28)

* Documentation
  - Added new attributes "javascript" and "stylesheet" to the campaign model,
  this allows users to render javascript elements and override css in the download page and form page (lmmendes)

## v0.4.0 (2016-11-28)

* Documentation
  - Added new "Registrations" endpoint documentation. (lmmendes)
  - Improved Readme.md content. (lmmendes)
  - Added "Organizations" endpoint documentation. (lmmendes)

## v0.3.0 (2016-11-23)

* Documentation
  - Added Open Graph attributes (`og` and `og_description`) to the campaign. (lmmendes)

## v0.2.1 (2016-08-30)

* Documentation
  - Clear Android Pay usage in the API `gwallet_usage` is `false` by default. (lmmendes)


## v0.2.2 (2016-08-10)

* Documentation
  - Added Webhooks missing events. (Pedro Somsen)
  - Updated Webhooks content example. (Pedro Somsen)
  - Added attributes of the webhook payload. (Pedro Somsen)

## v0.2.1 (2016-07-20)

* Documentation
  - Added missing documentation on how to DELETE campaign, eg: coupons, event_tickets, etc... (lmmendes)

## v0.2.0 (2016-06-30)

* Documentation
  - Added some examples (Pedro Gimenes)
  - Added help for using reports (Pedro Gimenes)

## v0.1.8 (2016-01-28)

* Documentation
  - Barcode types updated, now showing "ean128" (EAN128/GS1) (lmmendes)
  - Webhooks (lmmendes)

## v0.1.7 (2016-01-05)

* Documentation
  - Updated Asset/Templates vertical with DELETE operations. (Tiago Parreira)
  - Updated Ruby SDK (Tiago Parreira)

## v0.1.6 (2015-11-27)

* Documentation
  - Updated SDK's information. (Luís Mendes)
  - Removed API v1 deprecation notice from main page. (Luís Mendes)
  - Updated Ruby SDK (Luís Mendes)

## v0.1.5 (2015-04-13)

* Features
  - Creating boilerplate (template based) passes do not require payload anymore (Miguel Veríssimo)
  - Add the ability to redeem passes, in campaign, through the redeem code, and
    directly in the pass (Miguel Veríssimo)

## v0.1.4 (2015-03-31)

* Documentation
  - Namespaced old API documentation under v1 folder, and new one under v2 folder. (Miguel Veríssimo)
  - Revamped Event Ticket and Store Card vertical pages for our API v2, others are on-going. (Tiago Parreira)

## v0.1.3 (2015-01-23)

* Feature
  - Now able to create campaigns by sending in a custom certificate_id in order to use a specific certificate. (Tiago Parreira)

## v0.1.2 (2014-10-20)

* Feature
  - Campaigns (Coupon, Boarding Pass, Store Card, Generic, Event Ticket) now return `template_id` attribute in there playload.
  - Listing campaigns now return the model payload instead of a reduced version of it:
      GET /boarding_passes
      GET /store_cards
      GET /generics
      GET /event_tickets
      GET /coupons
* Fixed
  - Pass payload returned `download_page_url` with a typo (was `donwload_page_url`)


## v0.1.0 (2014-10-20)

* Feature: Removed root nodes from the returned API elements.
