# Sorting

Passworks API supports sorting for the most common attributes via query string.

Here is an example searching for a Coupon campaign with the name equal (name_eq) to "Una Salus Victus"

```
GET https://api.passworks.io/v2/coupons/?q[name_eq]=Una Salus Victus
```

> You can ignore the trailing slash in the end of the URL.

The following predicates are also available:

| Sort predicate | Description |
|-------|-------|
| *_eq | equal |
| *\_not\_eq | not equal |
| *\_match | matches with LIKE, e.g. q[email_matches]=%@gmail.com |
| *\_lt | less than |
| *\_lteq | less than or equal |
| *\_gt | greater than |
| *\_gteq | greater than or equal |
| *\_cont | contains |

So if you wish to search for the attribute "name" containing the word "House" you will have

```
GET https://api.passworks.io/v2/coupons/?q[name_cont]=House
```

### Best pratices: Escaping query parameters

Don't forget to escape the URL query parameters before submiting them to the API endpoint.

```
GET  https://api.passworks.io/v2/coupons/q%5Bname_cont%5D%3DHouse
```

### Ordering

Ordering attributes is also simple to accomplish see the following example ordering the `created_at` attribute in ascending order (asc)

```
GET https://api.passworks.io/v2/coupons/?q[s]=created_at+asc
```

To request ordering from a given attribute with a direction (ascending or descending) you need to to use the `q[s]=` following the attribute that you wish to order `created_at` following with a plus (+) signal and the direction of sorting `asc` or `desc`

So sorting the for the attribute name in descending order would be doing the following:


```
https://api.passworks.io/v2/coupons/?q[s]=name+desc
```

### Sorting multiple with parameters ordering and using pagination at the same time

You can append one or more filters to the query string then event apply the desired sort and finally specify a given page to be retrieved.

See the following example filtering for two parameters "name" (equal) and "redeem_count" (equal) and then asking for the results sorted by "created_at" in descending order and finally asking for the second page (page=2) of the results displaying 4 results per page (per_page=4).

```
GET https://api.passworks.io/v2/coupons/?q[name_eq]=Una Salus Victus&q[redeem_count_eq]=0&q[s]=created_at+desc&page=2&per_page=4
```

You can mix and match the query parameters the order doesn't matter.


### Sortable endpoints

You can sort and order the attributes inside the following endpoints:

Sort campaign collection attributes

- https://api.passworks.io/v2/coupons/
- https://api.passworks.io/v2/event_tickets/
- https://api.passworks.io/v2/generics/
- https://api.passworks.io/v2/store_cards/
- https://api.passworks.io/v2/boarding_passes/

Sort passes collection side a specific campaign

- https://api.passworks.io/v2/coupons/campaign_id/passes
- https://api.passworks.io/v2/event_tickets/campaign_id/passes
- https://api.passworks.io/v2/generics/campaign_id/passes
- https://api.passworks.io/v2/store_cards/campaign_id/passes
- https://api.passworks.io/v2/boarding_passes/campaign_id/passes

Sort registrations collection inside a specific campaign

- https://api.passworks.io/v2/coupons/campaign_id/registrations
- https://api.passworks.io/v2/event_tickets/campaign_id/registrations
- https://api.passworks.io/v2/generics/campaign_id/registrations
- https://api.passworks.io/v2/store_cards/campaign_id/registrations
- https://api.passworks.io/v2/boarding_passes/campaign_id/registrations

Sort redeems collection inside a specific campaign

- https://api.passworks.io/v2/coupons/campaign_id/redeems
- https://api.passworks.io/v2/event_tickets/campaign_id/redeems
- https://api.passworks.io/v2/generics/campaign_id/redeems
- https://api.passworks.io/v2/store_cards/campaign_id/redeems
- https://api.passworks.io/v2/boarding_passes/campaign_id/redeems

Sort registrations collection inside a specific campaign and pass

- https://api.passworks.io/v2/coupons/campaign_id/passes/pass_id/registrations
- https://api.passworks.io/v2/event_tickets/campaign_id/passes/pass_id/registrations
- https://api.passworks.io/v2/generics/campaign_id/passes/pass_id/registrations
- https://api.passworks.io/v2/store_cards/campaign_id/passes/pass_id/registrations
- https://api.passworks.io/v2/boarding_passes/campaign_id/passes/pass_id/registrations

Sort redeems collection inside a specific campaign and pass

- https://api.passworks.io/v2/coupons/campaign_id/passes/pass_id/redeems
- https://api.passworks.io/v2/event_tickets/campaign_id/passes/pass_id/redeems
- https://api.passworks.io/v2/generics/campaign_id/passes/pass_id/redeems
- https://api.passworks.io/v2/store_cards/campaign_id/passes/pass_id/redeems
- https://api.passworks.io/v2/boarding_passes/campaign_id/passes/pass_id/redeems

> Please replace the `campaign_id` and `pass_id` with the appropriate resource ID from your side.
