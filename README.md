# Restful Booker API Testing

An API testing project for the public [Restful Booker API](https://restful-booker.herokuapp.com/). It includes a Postman collection and environment, reusable booking payloads, a test-case workbook, endpoint and test-plan documentation, and bug-report/screenshot placeholders.

## Quick start

1. Import `postman/collections/RestfulBooker.postman_collection.json` and `postman/environments/RestfulBooker.postman_environment.json` into Postman.
2. Select the **Restful Booker - Local** environment.
3. Run the collection in order with the Collection Runner. The collection creates an auth token and booking, then uses the returned booking ID for read, update, and delete checks.
4. Review `test-cases/RestfulBooker_TestCases_and_Execution.xlsx` and record actual results after execution.

The API is public and shared. Its data may be reset or modified by other users; do not use personal or sensitive information.

## Project layout

| Path | Purpose |
| --- | --- |
| `postman/collections/` | Postman API requests and assertions |
| `postman/environments/` | Base URL and demo credentials |
| `test-cases/` | Test cases and execution tracking workbook |
| `test-data/` | Reusable valid and invalid request payloads |
| `bug-reports/` | Bug-report templates; no defects are asserted as verified |
| `docs/` | API endpoint reference and test plan |
| `reports/` | Optional generated Newman reports |
| `screenshots/` | Place actual execution screenshots here |

## Optional command-line run

With Node.js and Newman installed, run:

```sh
npx newman run postman/collections/RestfulBooker.postman_collection.json -e postman/environments/RestfulBooker.postman_environment.json --reporters cli,htmlextra --reporter-htmlextra-export reports/newman-report.html
```

Install the optional HTML reporter first with `npm install --global newman-reporter-htmlextra`. Generated reports are ignored by Git by default.

## Screenshots

Add real Postman screenshots to `screenshots/` after running the collection:

- `01_auth_token.png` — successful authentication and token extraction
- `02_collection_runner_results.png` — Collection Runner summary
- `03_failed_test_example.png` — a genuine failed assertion (do not fabricate failures)
