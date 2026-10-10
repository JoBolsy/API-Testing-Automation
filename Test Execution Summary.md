## 1. Test Execution Summary

| Metric | Result |
|---|---|
| Total Test Cases | 14 |
| Passed | 13 |
| Failed | 1 |
| Pass Rate | 92.9% |

## 2. Test Execution Evidence
![alt text](<Test Execution Evidence.png>)

## 3. Defect Summary
| Bug ID | Bug Title | Related Test Case | Status
|---|---|---|---|
| BUG-001 | API Accepts User Creation Without JSON Body | TC-POST-02 | Open

### Defect Description
During negative testing, the ReqRes API returned status code 201 when sending a POST request to /api/users without a JSON request body. The expected status code was 400 Bad Request, but the API accepted the request.

Note: This behavior may be intentional because ReqRes is a dummy API.

## 4. Conclusion
API testing was performed using Postman to validate CRUD operations, authentication, authorization, response status codes, and error handling.

The test results and identified defects are documented in the test cases and bug report.