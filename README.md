# Postman API Test Project

This repository contains an **API test automation suite** created using **Postman** and executed through **Newman** and **GitHub Actions CI/CD**. It is designed to validate RESTful API endpoints through functional test scenarios, ensuring data accuracy, proper response codes, and schema validation.

---

## ✨ Features

* **REST API Testing**: Covers GET, POST, PUT, and DELETE methods.
* **Schema Validation**: Verifies the data types and required fields in responses.
* **Negative Testing**: Validates API behavior for invalid inputs or broken endpoints.
* **Postman Scripts**: Uses `pm` scripts for advanced validations and assertions.
* **GitHub Actions CI Integration**: Automatically runs tests upon every commit.
* **Status Code & Content-Type Checks**: Ensures APIs return appropriate status codes and headers.
* **Test Reports**: Newman generates CLI and HTML reports.

---

## 🚀 Getting Started

### Requirements

* [Postman](https://www.postman.com/downloads/)
* [Node.js](https://nodejs.org/)
* Newman (CLI runner for Postman)

---

## 🚧 GitHub Actions CI/CD

* Every push to `main` triggers API tests via the `api-tests.yml` workflow.
* View test output under **Actions** tab in your GitHub repository.

**Workflow file path**: `.github/workflows/api-tests.yml`

```yaml
name: API Tests

on:
  push:
    branches: [ main ]

jobs:
  run-api-tests:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Install Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      - run: npm install -g newman
      - run: newman run collections/restful-booker.postman_collection.json -e environments/restful-booker-env.postman_environment.json
```

---

## 🔍 Sample Test Coverage

* **GET /booking/\:id**

  * Status code 200
  * Valid JSON response
  * `firstname`, `totalprice`, `depositpaid` fields exist

* **POST /booking**

  * Creates a new booking
  * Returns 200 or 201 with booking ID

* **PUT /booking/\:id**

  * Updates booking data
  * Status 200 with updated info

* **GET /booking/-12**

  * Invalid ID returns 404

---

## 📒 Technologies Used

* **Postman**
* **Newman CLI**
* **JavaScript** (`pm.*` scripting)
* **GitHub Actions**

