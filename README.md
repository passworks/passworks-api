Passworks API
====================

The Passworks API is based on a [REST](http://en.wikipedia.org/wiki/Representational_state_transfer) architecture which makes Passworks API predictable and resource oriented. It uses HTTP built-in features, like HTTP authentication, HTTP verbs (GET, POST, PUT, PATCH, DELETE) and HTTP response codes to allow easy access from any programming language via off-the-shelf libraries and tools.


Documentation `last updated at 31/Mar/2015` see the [CHANGELOG.md](https://github.com/passworks/passworks-api/blob/master/v2/CHANGELOG.md) for more details.

```shell
Our v1 API has been deprecated, use the new v2 API.
```

Understanding the API workflow
--------------------

Just before you start [creating things](#creating-things-using-the-api) using our API it's important that you understand the API flow.

There are 3 inherent concepts that are at work here:

- The first is the concept of a campaign. A campaign, as viewed in the API, is simply seen as the aggregator for all of the generated passes for a given context.
A campaign can be, in pratical terms, a collection of "[Membership or Loyalty](https://github.com/passworks/passworks-api/blob/master/v2/sections/store_card.md)" passes, a "[Bus Boarding](https://github.com/passworks/passworks-api/blob/master/v2/sections/boarding_pass.md)" pass, and several others. The type of campaign dictates what sort of data and purpose it can serve.

- Then there's the concept of a pass. A pass, by itself, is simply a representation of all the information that your target consumer will see when he installs it on his mobile device, it's the "boarding pass" the "event ticket" or simply a discount "[coupon](https://github.com/passworks/passworks-api/blob/master/v2/sections/coupon.md)".

- Finally, there's the concept of an asset. All of the passes support the insertion of at least 1 or more images, being one of them the 'icon', which is required on all passes, regardless of campaign type. Therefore, in order to start creating any type of campaign, you need to have uploaded at least one asset, which you supply to the campaign upon creation.

It's easy peasy!


Creating things using the API
-----------------


* [Asset](https://github.com/passworks/passworks-api/blob/master/v2/sections/assets.md) (Upload images to use in your passes)
* [Store Card](https://github.com/passworks/passworks-api/blob/master/v2/sections/store_card.md) (Loyalty, Membership Card,Photo ID, Monthly Passes)
* [Coupon](https://github.com/passworks/passworks-api/blob/master/v2/sections/coupon.md) (Discounts, Special Offers, Ongoing Engagement, Gift Card, Prepaid Cards, Return Credits)
* [Event Ticket](https://github.com/passworks/passworks-api/blob/master/v2/sections/event_ticket.md) (Event admission, Season tickets, Movie Tickets)
* [Boarding Pass](https://github.com/passworks/passworks-api/blob/master/v2/sections/boarding_pass.md) (Airplane, Bus, Train, Boat and Generic boarding passes)
* [Generic](https://github.com/passworks/passworks-api/blob/master/v2/sections/generic.md) (Business cards and anything else)
* [Certificate](https://github.com/passworks/passworks-api/blob/master/v2/sections/certificates.md) (List certificates for use in your campaigns)


Making a request
----------------

All URLs start with `https://api.passworks.io/v1/`. **SSL only**. The path is prefixed with the API version. If we change the API in backward-incompatible ways, we'll bump the version number and maintain stable support for the old URLs.

To create objects using the API each request must include the `Content-Type` header with the value `application/json` and the body must contain data in the [JSON](http://en.wikipedia.org/wiki/JSON) format.

```shell
curl -u account_id:api_key \
  -H 'Content-Type: application/json' \
  https://api.passworks.io/v1/ping
```

Authentication
--------------

As stated previously, Passworks uses [Basic Auth](http://en.wikipedia.org/wiki/Basic_access_authentication) for authentication, this is secure since all requests made to `https://api.passworks.io` use SSL.


Identify for your account id and api key
-----------------

To use the API you must provide your `account_id` and `api_key` in each request via Basic Auth.

Your `account_id` and `api_key` can be found here [http://www.passworks.io/organizations/roles](http://www.passworks.io/organizations/roles)


No XML, just JSON
-----------------

We only support [JSON](http://en.wikipedia.org/wiki/JSON) for serialization of data. This means that you have to send `Content-Type: application/json; charset=utf-8` when you're POSTing, PUTing or PATCHing data into Passworks.


Pagination
----------

Most collection call's on our API paginate their results. The first request returns up to
25 records. Check the next page for more results by adding `&page=2`, then
`&page=3`, and so on until you get an empty response.

Each page returns a maximum of 25 objects you can increase (up to 50 items per page) or decrease (to 1 per item page) this value adding the `&per_page=50` .

If a given resource is paginated the API will emit the following headers:

| Header Name       | Description |
|----------------------|-------------|
| X-Total: 42       | Total number of items found |
| X-Total-Pages: 5    | Total number of pages |
| X-Page: 3         | The current page |
| X-Per-Page: 10    | Amount of items displayed per page |
| X-Next-Page: 4    | The number of the next page |
| X-Prev-Page: 2    | The number of the previews page |
| X-Offset: 10      | The offset to start from |


Handling errors
---------------

If Passworks is having trouble, you might see a 5xx error. `500` means that the app is entirely down, but you might also see `502 Bad Gateway`, `503 Service Unavailable`, or `504 Gateway Timeout`. It's your responsibility in all of these cases to retry your request later.


Rate limiting
-------------

```
The rate limit and api throttling are not yet implemented.
```

Authenticated users can make up to **5000** requests per hour, each request is associated with the `account_id`.

You can check the returned HTTP headers of any API request to see your current rate limit status:

```shell
$ curl -i https://api.passworks.io/v1/ping

HTTP/1.1 200 OK
Date: Tue, 23 Sep 2014 09:09:54 GMT
Status: 200 OK
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 59
X-RateLimit-Reset: 1411459677
```

Header Name  | Description
------------- | -------------
X-RateLimit-Limit | The maximum number of requests that the consumer is permitted to make per hour.
X-RateLimit-Remaining | The number of requests remaining in the current rate limit window.
X-RateLimit-Reset | The time at which the current rate limit window resets in [UTC epoch seconds](http://en.wikipedia.org/wiki/Unix_time).

*Note: Unauthenticated requests are associated with your IP address, and not the user making requests. For unauthenticated you have 60 requests per hour.*

Using your own Passbook certificates
-------------
Adding a Passbook certificate (iOS Pass Type ID) is a rather cumbersome task so at the moment you can't do it via an API call.

It's recommended that you add your own certificates via our site [http://www.passworks.io/certificates](http://www.passworks.io/certificates)


API libraries
-------------

_**These libraries currently only work for our API v1!**_

* [passworks-php](https://github.com/passworks/passworks-php) - PHP library, composer compatible
* [passworks-ruby](https://github.com/passworks/passworks-ruby) - Ruby gem


Help us make it better
----------------------

Please tell us how we can make the API better. If you have a specific feature request or if you found a bug, please use GitHub issues. Fork these docs and send a pull request with improvements.

To talk with us and other developers about the API [open a support ticket](https://github.com/passworks/passworks-api/issues) or mail us at `api at passworks.io` if you need to talk to us.
