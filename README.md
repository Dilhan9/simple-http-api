# Simple HTTP API

A lightweight, production-ready REST service built using **Java 21**, **Spring Boot 4**, and **Maven**. The service exposes a single endpoint that validates an input name parameter and returns a conditional greeting based on the English alphabet position.

---

## Tech Stack

* **Language:** Java 21
* **Framework:** Spring Boot 3
* **Build Tool:** Maven (Maven Wrapper included)
* **Testing:** JUnit 5, AssertJ, Mockito, Spring MockMvc

---

## Getting Started

### Prerequisites

* JDK 21 installed (`java -version` should show 21+)
* Git

Sample Requests
Valid input (First half of alphabet: A–M):

Bash
curl -i "http://localhost:8080/hello-world?name=Alice"
Response (200 OK):

JSON
{"message": "Hello Alice"}
Invalid input (Second half of alphabet: N–Z):

Bash
curl -i "http://localhost:8080/hello-world?name=Nathan"
Response (400 Bad Request):

JSON
{"error": "Invalid Input"}
Invalid input (Missing parameter / Empty / Non-alphabetic):

Bash
curl -i "http://localhost:8080/hello-world"
curl -i "http://localhost:8080/hello-world?name="
curl -i "http://localhost:8080/hello-world?name=123"
Response (400 Bad Request):

JSON
{"error": "Invalid Input"}
How to Run the Tests
Execute the full suite of unit and integration tests via the Maven wrapper:

Bash
./mvnw clean test
Test Coverage Highlights
GreetingServiceTest: Independent unit tests exercising all edge cases, boundary inputs, whitespace handling, and character classifications across 115+ parameterized test runs.

HelloWorldControllerTest: MockMvc web layer tests verifying HTTP status codes, JSON payload integrity, and controller parameter extraction.

Assumptions Made
Alphabet Boundary Rule:

Letters A–M (and a–m) are considered the first half of the English alphabet.

Letters N–Z (and n–z) are considered the second half.

Whitespace Handling:

Names with leading or trailing whitespace (e.g., "  Alice ") are sanitized via strip(). The first non-whitespace character determines the alphabet check, and the stripped value is returned in the greeting.

Inputs consisting entirely of whitespace are treated as blank and rejected with HTTP 400 Bad Request.

Character Restrictions:

Names beginning with numbers, symbols, punctuation, or non-English characters are deemed invalid inputs and return HTTP 400 Bad Request with {"error": "Invalid Input"}.

Data Transfer Objects:

Implemented using immutable Java 21 record constructs, ensuring thread-safety, minimal boilerplate, and consistent JSON serialization without supplementary metadata or leaky internal fields.