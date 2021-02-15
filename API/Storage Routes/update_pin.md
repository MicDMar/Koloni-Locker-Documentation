# Update Pin

Update the stored pin for a specific locker

You are only allowed to update this information if you own it and it is set to be in storage mode.

**URL** : `/api/v1/update_pin`

**Method** : `POST`

**Auth required** : YES

**Permissions required** : None

**Data constraints**

Provide UUID of the locker to be unlocked and the new pin to be set.

```json
{
    "locker_id": "[unicode 32 char uuid]",
    "pin": "[unicode 4 integer pin]"
}
```

**Data example** All fields must be sent.

```json
{
    "locker_id": "58df5de0-454d-43f4-ae28-bea02e0fe1f3",
    "pin": "1234"
}
```

## Success Response

**Condition** : If everything is OK, a locker was found with the uuid and the pin was update successfully.

**Code** : `200 OK`

**Content example**

```json
{
    "locker_id": "58df5de0-454d-43f4-ae28-bea02e0fe1f3",
    "Pin": "1234",
    "message": "Locker pin updated successfully.",
    "command": "ACCEPTED"
}
```

## Error Responses

**Condition** : If fields are missing or malformed.

**Code** : `400 STATUS BAD REQUEST`

**Content example**

```json
{
    "message": "Malformed JSON or missing values.",
    "command": "REJECTED"
}
```

---

**Condition** : If you are not authorized to perform this action.

**Code** : `401 STATUS UNAUTHORIZED`

**Content example**

```json
{    
    "locker_id": "58df5de0-454d-43f4-ae28-bea02e0fe1f3",
    "message": "You do not have permission to view this locker.",
    "command": "REJECTED"
}
```

---

**Condition** : If there is no locker found with that uuid in the database.

**Code** : `410 STATUS GONE`

**Content example** :

```json
{
    "locker_id": "58df5de0-454d-43f4-ae28-bea02e0fe1f3",
    "message": "Locker does not exist.",
    "command": "REJECTED"
}
```

---

**Condition** : If there is an internal server error parsing JSON or querying the database.

**Code** : `500 STATUS INTERNAL SERVER ERROR`

**Content example** : 

```json
{
    "message": "Error generating JSON from values.",
    "command": "INCOMPLETE"
}
```
