Passworks API
====================

The Passworks API is based on [REST](http://en.wikipedia.org/wiki/Representational_state_transfer) architecture which makes passworks API predictable and resource oriented. It uses HTTP built-in features, like HTTP authentication, HTTP verbs (GET, POST, PUT, PATCH, DELETE) and HTTP response codes to allow easy access from any programming language via off-the-shelf libraries and tools. 


Making a request
----------------

All URLs start with `https://api.passworks.io/v1/`. **SSL only**. The path is prefixed with the API version. If we change the API in backward-incompatible ways, we'll bump the version number and maintain stable support for the old URLs.

To create objects using the API each request must include the `Content-Type` header with the value `application/json` and the body must contain data in the [JSON](http://en.wikipedia.org/wiki/JSON) format.

```shell
curl -u account_id:api_key \
  -H 'Content-Type: application/json' \
  https://api.passworks.io/v1/loyalty
```

Authentication
--------------

As stated previously Passworks uses [Basic Auth](http://en.wikipedia.org/wiki/Basic_access_authentication) for authentication, this is secure since all requests in made to `https://api.passworks.io` use SSL.


Identify for your account id and api key
-----------------

To use the API you must provide your `account_id` and `api_key` in each request via Basic Auth.

Your `account_id` and `api_key` can be found here [http://www.passworks.io/organizations/roles](http://www.passworks.io/organizations/roles)


Call me JSON
-----------------

We only support [JSON](http://en.wikipedia.org/wiki/JSON) for serialization of data. This means that you have to send `Content-Type: application/json; charset=utf-8` when you're POSTing, PUTing or PATCHing data into Passworks.


Pagination
----------

Most collection APIs paginate their results. The first request returns up to
25 records. Check the next page for more results by adding `&page=2`, then
`&page=3`, and so on until you get an empty response.

Each page returns a maximum of 25 objects you can increse (up to 50 items per page) or decrese (to 1 per item page) this value adding the `&per_page=50` .


Handling errors
---------------

If Passworks is having trouble, you might see a 5xx error. `500` means that the app is entirely down, but you might also see `502 Bad Gateway`, `503 Service Unavailable`, or `504 Gateway Timeout`. It's your responsibility in all of these cases to retry your request later. 


Rate limiting
-------------

```
The rate limit and api trotting are not implemented.
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
X-RateLimit-Limit	| The maximum number of requests that the consumer is permitted to make per hour.
X-RateLimit-Remaining |	The number of requests remaining in the current rate limit window.
X-RateLimit-Reset |	The time at which the current rate limit window resets in [UTC epoch seconds](http://en.wikipedia.org/wiki/Unix_time).

*Note: Unauthenticated requests are associated with your IP address, and not the user making requests. For unauthenticated you have 60 requests per hour.*

Understanding API the workflow
--------------------

Just before you start [creating things](#creating-things-using-the-api) using our API it's important that you understand the API flow.

A pass is composed of at least one asset (a asset is a image) and a bounch of text fields.

So to start creating passes you must first upload an image, usually it's an `icon` since all passes require it (the icon is used in the lock screen's notification).

Second step is creating a "campaign" think of a "campaign" as an aggregator element for all your passes, for example, if you are creating an [event ticket](https://github.com/passworks/passworks-api/blob/master/sections/event_ticket.md) for your birthday you create a "campaing" assign it a ``name`` like "my birthday" and a icon (asset). After that start adding passes to it.

It's easy peasy!


Creating things using the API
-----------------


* [Asset](https://github.com/passworks/passworks-api/blob/master/sections/assets.md)
* [Event Ticket](https://github.com/passworks/passworks-api/blob/master/sections/event_ticket.md) (Event admission, Season tickets, Movie Tickets)
* [Coupons](https://github.com/passworks/passworks-api/blob/master/sections/coupon.md) (Discounts, Special Offers, Ongoing Engagement, Gift Card, Prepaid Cards, Return Credits)
* [Generics](https://github.com/passworks/passworks-api/blob/master/sections/generic.md) (Business cards and and anything else)
* [Store Card](https://github.com/passworks/passworks-api/blob/master/sections/store_card.md) (Loyalty, Membership Card,Photo ID, Monthly Passes)
* [Boarding Pass](https://github.com/passworks/passworks-api/blob/master/sections/boarding_pass.md) (Airplane, Bus, Train, Boat and Generic boarding passes)

API libraries
-------------

* [passworks-php](https://github.com/passworks/passworks-php) - PHP library, composer compatible
* [passworks-ruby](https://github.com/passworks/passworks-ruby) - Ruby gem


Help us make it better
----------------------

Please tell us how we can make the API better. If you have a specific feature request or if you found a bug, please use GitHub issues. Fork these docs and send a pull request with improvements.

To talk with us and other developers about the API [open a support ticket](https://github.com/passworks/passworks-api/issues) or mail us at `api at passworks.io` if you need to talk to us.