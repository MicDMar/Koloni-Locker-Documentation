# Get Locker Info

See all stored information about a specific locker.
You are only allowed to view a locker this way if you own it and it is set to the proper mode.

**URL** : `/api/v1/get_locker_info`

**Method** : `GET`

**Auth required** : YES

**Permissions required** : None

**Data constraints**

Provide UUID of the locker which you want to recieve information for.

```json
{
    "locker_id": "[unicode 32 char uuid]",
}
```

## Success Response

**Condition** : If everything is OK and and the locker was found under your owner id.

**Code** : `200 OK`

**Content example**

```json
{
  "locker": {
    "Id": 26,
    "Partner_id": 2,
    "Owner_id": 2,
    "Mac_addr": "FF:EE:DD:CC:BB:AA",
    "Uuid": "e5b72952-5cae-487f-9d5a-81e169c455e5",
    "Image": 0,
    "Item": "Basketball",
    "Pin": "5555",
    "State": 1,
    "Mode": 0,
    "Latitude": 52,
    "Longitude": 67
  }
}
```

## Error Responses

**Condition** : If you are not authorized to perform this action.

**Code** : `401 STATUS UNAUTHORIZED`

**Content example**

```json
{    
    "message": "You do not have permission to view this locker"
}
```

---

**Condition** : If there are no locks found with your owner id.

**Code** : `404 STATUS NOT FOUND`

**Content example**

```json
{
    "message": "Locker not found."
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
