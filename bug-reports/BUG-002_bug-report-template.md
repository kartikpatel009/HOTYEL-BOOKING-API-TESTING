# BUG-002: <API accepts empty firstname when creating a booking>

- **Status:** 
- **Severity:** Medium
- **Environment:** QA / Test
- **Endpoint / build:** POST /booking

## Summary
The Create Booking API accepts an empty firstname value and successfully creates a new booking. Since the first name is expected to be a required field for a booking, the API should validate the input and reject the request when firstname is empty.

## Steps to reproduce

1. Open Postman.
2. Select the POST Create Booking request.
3. Use the endpoint:
   https://restful-booker.herokuapp.com/booking
4. Set the request header:
   Content-Type: application/json
5. Select Body → raw → JSON.
   Enter the following request body:
   {
    "firstname": "",
    "lastname": "Patel",
    "totalprice": 2500,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2026-11-10",
        "checkout": "2026-11-15"
    },
    "additionalneeds": "Breakfast"
   }
6. Click Send.
7. Observe the HTTP status code and response body.
8. Check whether a new bookingid is generated.

## Expected result

The API should validate the firstname field and reject the request because the value is empty.

The booking should not be created.

A 400 Bad Request or another appropriate validation error would be expected if firstname is a mandatory field.

## Actual result

The API accepts the empty firstname value and creates a new booking.

The response returns a successful status code and a newly generated bookingid.

Example:

Status: 200 OK

## Evidence

<img width="1692" height="1012" alt="Screenshot 2026-10-07 155240" src="https://github.com/user-attachments/assets/6dd32bc0-6841-4e16-8341-faaeef7f6d92" />

