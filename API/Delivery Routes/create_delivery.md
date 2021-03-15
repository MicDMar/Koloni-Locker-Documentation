# Create Delivery

Create a delivery request for a specific locker.
Currently the locker will be reserved for a 1 hour time slot. For testing purposes you can overlap these times.
In production you will not be able to overlap deviveries and a delivery will also expire after the unlock button is pressed once.

**URL** : `/api/v1/create_delivery`

**Method** : `POST`

**Auth required** : YES

**Permissions required** : None

**Data constraints**

Provide UUID of the locker which the delivery will take place,
Phone number of the delivery recipient,
Message that will be texted to the user along with the url,
and location id for the delivery sender.

```json
{
    "locker_id": "[unicode 32 char uuid]",
    "phone_number": "[unicode 11-13 int phone number with country code]",
    "message": "[unicode 128 message]",
    "location_id": "[integer]"
}
```

**Data example** All fields must be sent.

```json
{
    "locker_id": "58df5de0-454d-43f4-ae28-bea02e0fe1f3",\
    "phone_number": "+11234567890",
    "message": "Thank you for using Koloni!",
    "location_id": "7"
}
```

## Success Response

**Condition** : If everything is OK, a locker was found with the uuid and a text message was sent to the recipient.

**Code** : `202 ACCEPTED`

**Content example**

```json
{
    "message": "Successfully created delivery.",
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
    "message": "You do not have permission to create deliveries with this locker.",
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
