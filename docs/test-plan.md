# API test plan

## Objective

Verify the Restful Booker demo API's basic availability and core booking lifecycle using Postman, including response status, response structure, data updates, authentication, and deletion behavior.

## Scope

- Health check and token creation
- Booking creation, retrieval, search, full update, partial update, deletion, and post-delete lookup
- Basic success-response shape and status assertions

Out of scope: load/performance testing, security penetration testing, production reliability guarantees, and exhaustive validation of every invalid-input combination.

## Test approach

Import the collection and environment under `postman/`. Execute requests in collection order in Postman's Collection Runner. The authentication and create-booking tests populate `token` and `bookingId`; subsequent requests use those environment values. Update the workbook with the actual run date, result, response details, and defect reference.

## Entry criteria

- The demo API is reachable.
- Postman is installed and both JSON files import successfully.
- The **Restful Booker - Local** environment is selected.

## Exit criteria

- All in-scope cases have a recorded result.
- Failures have reproducible evidence and are distinguished from transient service/network failures.
- Any verified defect has a completed report under `bug-reports/`.

## Risks and assumptions

- The API is publicly shared, rate-limited, and may be temporarily unavailable.
- Other users can modify shared records. The collection creates its own booking and uses the returned ID, but collisions or external deletion remain possible.
- Demo credentials are public service credentials and must not be reused for private systems.
- API status-code expectations reflect the public demo API contract and should be checked against current service behavior when they change.
