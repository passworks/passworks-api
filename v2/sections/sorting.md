# Sorting

Passworks API supports sorting for the most common attributes via query string.

Here is an example searching for a Coupon campaign with the name equal (name_eq) to "Una Salus Victus"

```
GET https://api.passworks.io/v2/coupons/?q[name_eq]=Una Salus Victus
```

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

So sorting the for the attribute name in descending order whould be doing the following:


```
https://api.passworks.io/v2/coupons/?q[s]=name+desc
```

### Sortable endpoints

You can sort and order the attributes inside the following endpoints

- https://api.passworks.io/v2/coupons/
- https://api.passworks.io/v2/event_tickets/
- https://api.passworks.io/v2/generics/
- https://api.passworks.io/v2/store_cards/
- https://api.passworks.io/v2/boarding_passes/
- https://api.passworks.io/v2/coupons/\<campaign id>/passes
- https://api.passworks.io/v2/event_tickets/\<campaign id>/passes
- https://api.passworks.io/v2/generics/\<campaign id>/passes
- https://api.passworks.io/v2/store_cards/\<campaign id>/passes
- https://api.passworks.io/v2/boarding_passes/\<campaign id>/passes
