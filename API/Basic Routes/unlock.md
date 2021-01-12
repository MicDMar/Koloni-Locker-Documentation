# Unlock Locker

Send an unlock request for a specific locker.
You are only allowed to unlock a locker this way if you own it and it is set to the proper mode.

**URL** : `/api/v1/create_locker`

**Method** : `POST`

**Auth required** : YES

**Permissions required** : None

**Data constraints**

Provide UUID of the locker to be unlocked.

```json
{
    "locker_id": "[unicode 32 char uuid]"
}
```

**Data example** All fields must be sent.

```json
{
    "locker_id": "58df5de0-454d-43f4-ae28-bea02e0fe1f3"
}
```

## Success Response

**Condition** : If everything is OK and a locker was found with the uuid.

**Code** : `202 ACCEPTED`

**Content example**

```json
{
    "locker_id": "58df5de0-454d-43f4-ae28-bea02e0fe1f3",
    "locker_status": 1,
    "command": "ACCEPTED"
}
```

## Error Responses

**Condition** : If fields are missing or malformed.

**Code** : `400 STATUS BAD REQUEST`

**Content example**

```json
{
}
```

---

**Condition** : If you are not authorized to perform this action.

**Code** : `401 STATUS UNAUTHORIZED`

**Content example**

```json
{
}
```

---

**Condition** : If the lock IoT device is not registered for locking/unlocking functionality.

**Code** : `404 STATUS NOT FOUND`

**Content example**

```json
{
}
```

---

**Condition** : If there is no locker found with that uuid in the database.

**Code** : `410 STATUS GONE`

**Headers** : `{}`

**Content** : `{}`

---

**Condition** : If there is an internal server error parsing JSON or querying the database.

**Code** : `500 STATUS INTERNAL SERVER ERROR`

**Headers** : `{}`

**Content** : `{}`
