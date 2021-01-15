# Unlock Locker

Send an unlock request for a specific locker.
You are only allowed to unlock a locker this way if you own it and it is set to the proper mode.

**URL** : `/api/v1/get_all_lockers`

**Method** : `GET`

**Auth required** : YES

**Permissions required** : None

**Data constraints** : None

## Success Response

**Condition** : If everything is OK and and lockers were found under your owner id.

**Code** : `200 OK`

**Content example**

```json
{
  "lockers": [
    {
      "Id": 20,
      "Partner_id": 2,
      "Owner_id": 2,
      "Mac_addr": "AA:BB:CC:DD:EE:FF",
      "Uuid": "e505fa3b-0dcc-464a-ba95-ff61a72efe53",
      "Image": 0,
      "Item": "",
      "Username": "",
      "State": 0,
      "Mode": 0,
      "Latitude": 45.5,
      "Longitude": 51.1
    },
    {
      "Id": 21,
      "Partner_id": 2,
      "Owner_id": 2,
      "Mac_addr": "AA:BB:CC:DD:EE:FF",
      "Uuid": "fc301fc0-d577-40a5-b4f8-b002a6d414c6",
      "Image": 0,
      "Item": "",
      "Username": "",
      "State": 0,
      "Mode": 0,
      "Latitude": 45.5,
      "Longitude": 51.1
    },
    {
      "Id": 22,
      "Partner_id": 2,
      "Owner_id": 2,
      "Mac_addr": "AA:BB:CC:DD:EE:FF",
      "Uuid": "a807946b-773e-498b-8e88-a6502e827e65",
      "Image": 0,
      "Item": "",
      "Username": "",
      "State": 0,
      "Mode": 0,
      "Latitude": 45.5,
      "Longitude": 51.1
    }
  ]
}
```

## Error Responses

**Condition** : If you are not authorized to perform this action.

**Code** : `401 STATUS UNAUTHORIZED`

**Content example**

```json
{    
    "message": "You do not have permission to access this route."
}
```

---

**Condition** : If there are no locks found with your owner id.

**Code** : `404 STATUS NOT FOUND`

**Content example**

```json
{
    "message": "No lockers found."
}
```

---

**Condition** : If there is an internal server error querying the database.

**Code** : `500 STATUS INTERNAL SERVER ERROR`

**Content example** : 

```json
{
    "message": "Error querying information from database."
}
```
