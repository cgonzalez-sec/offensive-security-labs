# DVWA – SQL Injection

## Target
Damn Vulnerable Web Application (DVWA) – SQL Injection module.  
Web application that retrieves user information based on a user-supplied `id` parameter.

## Scope
Authorized local lab environment (DVWA).

## Recon
- User input controls which user record is retrieved.
- Returned fields:
  - User ID
  - First Name
  - Surname
- HTTP Method: POST
- Vulnerable parameter:
  - id=1&Submit=Submit
- Frontend restrictions observed (dropdown / limited input).
- Backend processes the value received in the POST request.
- Requests intercepted and modified using Burp Suite.

## Vulnerability
The application builds SQL queries by directly concatenating user-controlled input into the query without proper sanitization or parameterized statements.  
This allows manipulation of the SQL query logic (SQL Injection).

## Exploitation

### Low
- No input validation or filtering.
- The backend directly interprets the `id` parameter in the SQL query.
- Altering the parameter changes query behavior, confirming SQL injection.

### Medium
- Frontend input restrictions are present.
- Backend remains vulnerable.
- Modifying the POST request bypasses frontend controls.

### High
- Additional backend checks are implemented.
- Injection capabilities are more limited.
- Backend behavior indicates partial mitigation but remains vulnerable.

### Impossible
- Proper input validation and prepared statements are implemented.
- SQL injection is no longer possible.
- The application behaves securely.

## Result
- SQL Injection was confirmed in Low, Medium, and High security levels.
- The Impossible level correctly mitigates the vulnerability.
- Differences between frontend controls and backend security were clearly identified.

## Mitigation
- Use prepared statements / parameterized queries.
- Enforce strict server-side input validation.
- Never rely on frontend restrictions for security.
