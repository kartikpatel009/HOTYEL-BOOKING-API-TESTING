# Restful Booker API endpoints

Base URL: `https://restful-booker.herokuapp.com`

The service is a public demo API. Status codes or data may change, and its shared dataset is not suitable for dependable production-like persistence.

| Method | Path | Purpose | Expected response |
| --- | --- | --- | --- |
| `GET` | `/ping` | Health check | `201` |
| `POST` | `/auth` | Create an auth token using JSON `username` and `password` | `200`, JSON with `token` |
| `GET` | `/booking` | List booking IDs; optional `firstname`, `lastname`, `checkin`, `checkout` filters | `200`, JSON array |
| `GET` | `/booking/{id}` | Retrieve a booking | `200`, booking JSON; `404` if absent |
| `POST` | `/booking` | Create a booking | `200`, JSON with `bookingid` and `booking` |
| `PUT` | `/booking/{id}` | Replace a booking; requires `token` cookie or supported auth | `200`, updated booking |
| `PATCH` | `/booking/{id}` | Partially update a booking; requires auth | `200`, updated booking |
| `DELETE` | `/booking/{id}` | Delete a booking; requires auth | `201`; subsequent lookup returns `404` |

## Booking representation

```json
{
  "firstname": "Jim",
  "lastname": "Brown",
  "totalprice": 111,
  "depositpaid": true,
  "bookingdates": {
    "checkin": "2026-10-10",
    "checkout": "2026-10-15"
  },
  "additionalneeds": "Breakfast"
}
```

The `bookingdates` object requires `checkin` and `checkout` date strings. The collection obtains a token from `/auth` and sends it as `Cookie: token={{token}}` for write operations that require authentication.
