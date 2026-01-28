# Payments API - UAPIM

Permits payments of orders if current User has access permissions to it. 
Developed by Andres.

**URL** : `/api/payments/:pk/`

**URL Parameters** : `pk=[integer]` where `pk` is the ID of the Ship on the
server.

**Method** : `GET`

**Auth required** : YES

**Permissions required** :

User is at least one of the following in relation to the Ship requested:

* Owner `OO`
* Admin `AA`
* Viewer `VV`

**Data**: `{}`

## Success Response

**Condition** : If Order exists and Authorized User has required permissions.

**Code** : `200 OK`

**Content example**

```json
{
    "id": 345,
    "description": "Payment with credit card for order 124 done",
    "enterprise": false,
    "url": "http://testserver/api/orders/345/"
}
```

## Error Responses

**Condition** : If Order does not exist with `id` of provided `pk` parameter.

**Code** : `404 NOT FOUND`

**Content** : `{}`

### Or

**Condition** : If Order exists but Authorized User does not have required
permissions.

**Code** : `403 FORBIDDEN`


**Content** :

```json
{"detail": "You do not have permission to perform this action."}
```

## Notes

There are security issues:

* This view allows existing users to test for existence of Order that exist
    but that they do not have access to.
* Order IDs are sequential so an authorized user can count all the orders
    on the system.