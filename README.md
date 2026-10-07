# HOTEL BOOKING API TESTING
API testing project for the [Restful Booker](https://restful-booker.herokuapp.com/) hotel booking REST API, built with **Postman**. It covers the full booking lifecycle (create, read, update, delete), token-based authentication, and positive, negative and boundary test scenarios, with test cases and execution results tracked in Excel.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Tools and Technologies](#tools-and-technologies)
- [Scope of Testing](#scope-of-testing)
- [Repository Structure](#repository-structure)
- [Getting Started](#getting-started)
- [Test Cases](#test-cases)
- [Sample Boundary Tests: `totalprice`](#sample-boundary-tests-totalprice)
- [Validations Performed](#validations-performed)
- [Defects and Observations](#defects-and-observations)
- [Key Learnings](#key-learnings)
- [Author](#author)

---

## Project Overview

Restful Booker is a public practice API that simulates a hotel booking service. This project validates its endpoints for correct behavior, input handling, authentication and response performance, following a structured test-design approach (positive, negative and boundary testing).

**Objectives**

- Verify that all booking endpoints return the correct status codes and response bodies.
- Validate authentication and authorization using token-based access.
- Identify weaknesses in input validation using negative and boundary data.
- Document test cases and execution results in a clear, reusable format.

## Tools and Technologies

| Category | Tool |
|---|---|
| API testing | Postman (Collections, Environments, Collection Runner) |
| Data format | JSON |
| Test documentation | Microsoft Excel |
| Version control | Git and GitHub |

## Scope of Testing

| Area | Details |
|---|---|
| **CRUD operations** | `POST /booking`, `GET /booking`, `GET /booking/{id}`, `PUT /booking/{id}`, `DELETE /booking/{id}` |
| **Authentication** | Token generation via `POST /auth` and use of the token in protected requests |
| **Positive testing** | Valid inputs and expected successful responses |
| **Negative testing** | Invalid, missing or malformed inputs; missing or invalid token |
| **Boundary testing** | Limit values for numeric and date fields (for example `totalprice`) |
| **Response validation** | Status code, response body, headers and response time |

## Repository Structure

```
restful-booker-api-testing/
├── bug-reports/     # Bug report documents (for example BUG-002)
├── docs/            # Project documentation
├── postman/         # Postman collection and environment files
├── reports/         # Test execution reports
├── test-cases/      # Test case sheets (Excel)
├── test-data/       # Input data used for data-driven and boundary tests
└── README.md
```

| Folder | Purpose |
|---|---|
| `bug-reports/` | Defects found during testing, each documented with steps to reproduce, expected result and actual result |
| `docs/` | Supporting project documentation |
| `postman/` | Postman collection (requests and test scripts) and environment variables |
| `reports/` | Execution reports and test results |
| `test-cases/` | Test case sheets with Test ID, Boundary, Input and Expected Output |
| `test-data/` | Data files used to drive the tests, such as the `totalprice` input values |

## Getting Started

### Prerequisites

- [Postman](https://www.postman.com/downloads/) (desktop app or web)
- Internet access to reach the public Restful Booker API

### Run the Collection

1. Clone the repository:
   ```bash
   git clone https://github.com/kartikpatel009/restful-booker-api-testing.git
   ```
2. Open Postman and choose **Import**.
3. Import the collection (and environment, if present) from the `postman/` folder.
4. Select the imported environment (top-right corner).
5. Run requests individually, or open the collection and click **Run** to execute all tests with the Collection Runner.

### Data-Driven Run (optional)

Use `{{totalprice}}` in the request body and supply a CSV or JSON data file from the `test-data/` folder in the Collection Runner to execute every boundary value in one run.

## Test Cases

Test cases are maintained in Excel in the `test-cases/` folder with the following columns:

| Column | Description |
|---|---|
| Test ID | Unique identifier (for example TC01) |
| Boundary / Test Case | Category or name of the scenario |
| Input | Data sent in the request |
| Expected Output | Expected status code and behavior |

## Sample Boundary Tests: `totalprice`

| Test ID | Scenario | Input | Expected Output |
|---|---|---|---|
| TC01 | Valid value | `2500` | 200 OK; booking created; price returned as 2500 |
| TC02 | Lower boundary (zero) | `0` | 200 OK, or 400 if free bookings are not allowed |
| TC03 | Negative value | `-1` | 400 Bad Request |
| TC04 | Very large value | `999999999` | Stored intact; no overflow or 500 error |
| TC05 | Decimal | `2500.50` | 400, or consistent rounding; no 500 error |
| TC06 | Numeric string | `"2500"` | 400, or coerced to number; behavior documented |
| TC07 | Text | `"abc"` | 400 Bad Request |
| TC08 | Null | `null` | 400 Bad Request |
| TC09 | Empty string | `""` | 400 Bad Request |
| TC10 | Missing field | field omitted | 400 Bad Request |
| TC11 | Negative zero | `-0` | Treated as 0 |
| TC12 | 32-bit overflow | `2147483648` | 400, or stored intact; no 500 error |

## Validations Performed

- **Status codes:** 200, 201, 400, 403, 404 and 405 as applicable
- **Response body:** field presence, data types and values match the request
- **Response time:** requests complete within an acceptable threshold
- **Authentication:** protected endpoints reject requests without a valid token

Example Postman test script:

```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response time is under 1000 ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(1000);
});

pm.test("Price is returned correctly", function () {
    const body = pm.response.json();
    pm.expect(body.booking.totalprice).to.eql(2500);
});
```

## Defects and Observations

Restful Booker applies loose input validation, so some negative and boundary inputs may be accepted instead of rejected. Any difference between expected and actual behavior is documented as a bug report in the `bug-reports/` folder (for example `BUG-002`), including the request, the response and the expected result. Overall results are summarized in the `reports/` folder.

## Key Learnings

- Designing positive, negative and boundary test cases for REST APIs
- Chaining requests and managing variables and environments in Postman
- Writing automated assertions with Postman test scripts
- Running data-driven tests with the Collection Runner
- Documenting test cases, results and defects in a clear, reviewable format

## Author

**Kartik Patel**
B.Tech in Computer Science (AI & ML)
GitHub: [kartikpatel009](https://github.com/kartikpatel009)
