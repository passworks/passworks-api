# CHANGELOG

This file is a manually maintained list of changes for each release. Feel free to add your
changes here when sending pull requests. Also send corrections if you spot any mistakes.

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