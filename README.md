# API Testing Automation with Postman

An API testing portfolio project using **Postman** to test REST API CRUD operations, registration, login, and token-based authentication. The project uses [ReqRes](https://reqres.in/) for user-management requests and [DummyJSON](https://dummyjson.com/) for authentication workflows.

## Project Overview

This project demonstrates:

- Positive and negative API testing
- CRUD operations with `GET`, `POST`, `PUT`, `PATCH`, and `DELETE`
- Response status-code assertions using Postman scripts
- API-key and Bearer-token authentication
- Extracting a generated user ID and access token into environment variables
- Running a collection and documenting execution results
- Recording behavior and potential defects

## Tools and APIs

| Tool / API | Purpose |
| --- | --- |
| Postman | API requests, JavaScript test scripts, and Collection Runner |
| ReqRes (`https://reqres.in`) | Users CRUD and registration tests |
| DummyJSON (`https://dummyjson.com`) | Login and authenticated-profile tests |
| Excel | Test cases and bug report |
| Markdown | Test execution summary |

## Test Coverage

| # | Request | Method | Endpoint | Service |
| --- | --- | --- | --- | --- |
| 1 | Get All Users (page 2) | GET | `/api/users?page=2` | ReqRes |
| 2 | Get Single User | GET | `/api/users/2` | ReqRes |
| 3 | Get Nonexistent User | GET | `/api/users/999` | ReqRes |
| 4 | Create User | POST | `/api/users` | ReqRes |
| 5 | Create User with Empty Body | POST | `/api/users` | ReqRes |
| 6 | Update User | PUT | `/api/users/{{userId}}` | ReqRes |
| 7 | Partially Update User | PATCH | `/api/users/{{userId}}` | ReqRes |
| 8 | Delete User | DELETE | `/api/users/{{userId}}` | ReqRes |
| 9 | Register | POST | `/api/register` | ReqRes |
| 10 | Register Without Password | POST | `/api/register` | ReqRes |
| 11 | Login and Extract Token | POST | `/auth/login` | DummyJSON |
| 12 | Login Without Password | POST | `/auth/login` | DummyJSON |
| 13 | Get Current Auth User | GET | `/auth/me` | DummyJSON |
| 14 | Get Current Auth User with Invalid Token | GET | `/auth/me` | DummyJSON |

## Setup and Execution

1. Install [Postman](https://www.postman.com/downloads/).
2. Import `API Testing Automation.postman_collection.json`.
3. Import `My Environment.postman_environment.json`.
4. Select **My Environment** and configure the variables below.
5. Run requests individually or use the Postman **Collection Runner** to execute the collection in order.
6. Inspect test results in the runner and compare them against the test case workbook.

### Environment Variables

| Variable | Purpose | Value |
| --- | --- | --- |
| `base_url` | ReqRes base URL | `https://reqres.in` |
| `base_url_2` | DummyJSON base URL | `https://dummyjson.com` |
| `x-api-key` | ReqRes API key | API Key provided by ReqRes |
| `userId` | User ID captured from ReqRes create-user response | Set automatically by the `Create User` script |
| `token` | DummyJSON access token | Set automatically by the `Login (Extract Token)` script |

## Automation Examples

**Status code assertion:**

```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```

**Capture the user ID after a successful create request:**

```javascript
const response = pm.response.json();
pm.environment.set("userId", response.id);
```

**Capture the access token after a successful DummyJSON login:**

```javascript
const response = pm.response.json();
pm.environment.set("token", response.accessToken);
```

## Test Execution Results

The recorded run executed **14 requests**, with **16 Postman assertions** overall.

| Metric | Result |
| --- | ---: |
| API requests / documented test cases | 14 |
| Requests with all assertions passing | 13 |
| Requests with a failing assertion | 1 |
| Total assertions | 16 |
| Passed assertions | 15 |
| Failed assertions | 1 |
| Request-level pass rate | 92.9% |
| Execution errors reported by runner | 0 |
| Run duration | 5.88 seconds |
| Average response time | 324 ms |

![Postman Collection Runner test execution results](Test%20Execution%20Evidence.png)

### Defect - BUG-001

**Title:** API Accepts User Creation Without JSON Body  
**Test case:** `TC-POST-02`  
**Request:** `POST /api/users` (ReqRes)  
**Expected status code** `400 Bad Request`  
**Actual status code:** `201 Created`  
**Recorded status:** Open 

The API accepted a create-user request with no JSON request body, causing the assertion expecting 400 status code to fail. **This is not necessarily a confirmed product bug** because ReqRes is a dummy API, accepting an empty body may be intentional.
## Repository Files

```text
.
├── README.md
├── API Testing Automation.postman_collection.json
├── My Environment.postman_environment.json
├── Test Cases & Bug Report - API Testing Automation.xlsx
├── Test Execution Summary.md
└── Test Execution Evidence.png
```