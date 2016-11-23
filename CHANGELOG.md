# CHANGELOG

This file is a manually maintained list of changes for each release. Feel free to add your
changes here when sending pull requests. Also send corrections if you spot any mistakes.

## v0.3.0 (2016-11-34) - Luís Mendes

* Documentation
  - Added Open Graph attributes (`og` and `og_description`) to the campaign.

## v0.2.1 (2016-08-30) - Luís Mendes

* Documentation
  - Clear Android Pay usage in the API `gwallet_usage` is `false` by default.


## v0.2.2 (2016-08-10) - Pedro Somsen

* Documentation
  - Added Webhooks missing events.
  - Updated Webhooks content example.
  - Added attributes of the webhook payload.

## v0.2.1 (2016-07-20) - Luís Mendes

* Documentation
  - Added missing documentation on how to DELETE campaign, eg: coupons, event_tickets, etc...

## v0.2.0 (2016-06-30) - Pedro Gimenes

* Documentation
  - Added some examples
  - Added help for using reports

## v0.1.8 (2016-01-28) - Luís Mendes

* Documentation
  - Barcode types updated, now showing "ean128" (EAN128/GS1)
  - Webhooks

## v0.1.7 (2016-01-05) - Tiago Parreira

* Documentation
  - Updated Asset/Templates vertical with DELETE operations.
  - Updated Ruby SDK

## v0.1.6 (2015-11-27) - Luís Mendes

* Documentation
  - Updated SDK's information.
  - Removed API v1 deprecation notice from main page.
  - Updated Ruby SDK

## v0.1.5 (2015-04-13) - Miguel Veríssimo

* Features
  - Creating boilerplate (template based) passes do not require payload anymore
  - Add the ability to redeem passes, in campaign, through the redeem code, and
    directly in the pass

## v0.1.4 (2015-03-31) - Tiago Parreira, Miguel Veríssimo

* Documentation
  - Namespaced old API documentation under v1 folder, and new one under v2 folder.
  - Revamped Event Ticket and Store Card vertical pages for our API v2, others are on-going.

## v0.1.3 (2015-01-23) - Tiago Parreira

* Feature
  - Now able to create campaigns by sending in a custom certificate_id in order to use a specific certificate.

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
