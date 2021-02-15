# Pin Unlock Locker

Send an unlock request for a specific locker, along with a pin for verification.
This pin will be checked against the pin that was last set with UPDATE_PIN.
If a locker has switched modes to be in storage mode, or is new then this pin has not been set yet and this route will not work.

You are only allowed to unlock a locker this way if you own it and it is set to be in storage mode.

**URL** : `/api/v1/pin_unlock`

**Method** : `POST`

**Auth required** : YES

**Permissions required** : None

**Data constraints**

Provide UUID of the locker to be unlocked and pin defined with UPDATE_PIN.

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

**Condition** : If everything is OK, a locker was found with the uuid and the pin matched.

**Code** : `202 ACCEPTED`

**Content example**

```json
{
    "locker_id": "58df5de0-454d-43f4-ae28-bea02e0fe1f3",
    "locker_status": 1,
    "message": "Successfully unlocked locker.",
    "command": "COMPLETE"
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
    "locker_status": 0,
    "message": "You do not have permission to unlock this locker.",
    "command": "REJECTED"
}
```

---

**Condition** : If the lock IoT device is not registered for locking/unlocking functionality.

**Code** : `404 STATUS NOT FOUND`

**Content example**

```json
{
    "locker_id": "58df5de0-454d-43f4-ae28-bea02e0fe1f3",
    "locker_status": 0,
    "message": "Locker is offline or could not be found.",
    "command": "INCOMPLETE"
}
```

---

**Condition** : If the pin privided with the request does not match what is stored in the database.

**Code** : `406 STATUS NOT ACCEPTABLE`

**Content example**

```json
{    
    "locker_id": "58df5de0-454d-43f4-ae28-bea02e0fe1f3",
    "locker_status": 0,
    "message": "Pin provided does not match the pin stored.",
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
    "locker_status": 0,
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
