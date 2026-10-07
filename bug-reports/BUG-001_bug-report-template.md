# BUG-001: <API accepts negative totalprice when creating a booking>

> Template only. Replace this document with a defect report after reproducing and verifying an issue. No defect is asserted by this file.

- **Status:** Open
- **Severity:** Medium
- **Environment:** QA / Test
- **Endpoint / build:** POST /booking

## Summary

The Create Booking API accepts a negative value for the totalprice field and creates a new booking successfully. A negative booking price is invalid from a business perspective and should be rejected through input validation.

## Steps to reproduce

1.Open Postman.
2.Select the POST Create Booking request.
3.Use the endpoint:
  https://restful-booker.herokuapp.com/booking
4.Set the request header:
  Content-Type: application/json
5.Select Body → raw → JSON.
6.Enter the following request body:
  {
    "firstname": "Kartik",
    "lastname": "Patel",
    "totalprice": -500,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2026-11-10",
        "checkout": "2026-11-15"
    },
    "additionalneeds": "Breakfast"
  }
7.Click Send.
8.Observe the HTTP status code and response body.

## Expected result

The API should reject the request because totalprice contains an invalid negative value.

A client-side validation error such as 400 Bad Request would be appropriate if negative prices are not allowed by the business rules.

The booking should not be created.

## Actual result

The API accepts the negative totalprice value and returns a successful response with a newly generated booking ID.

Example:

Status: 200 OK

The response contains a new bookingid and the submitted booking data.

## Evidence

![API accepts negative totalprice when creating a booking
](./screenshots/Screenshot 2026-10-07 153213.png)

