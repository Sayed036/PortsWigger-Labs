# Short notes

## 🗄️ NoSQL Injection — Quick Notes

### What is it?

Attacking a NoSQL database (like MongoDB) by tampering with queries — similar to SQL injection but for non-relational databases.

### What can an attacker do?

- Bypass login/authentication
- Steal or modify data
- Crash the server (DoS)
- Run code on the server

---

### Two Types

**1. Syntax Injection**
Break the query syntax by injecting special characters (like `'`, `"`, `{`, `;`).

- If the app responds differently → it's likely vulnerable
- Example: inject `'||'1'=='1` to make a condition always true → returns all records

**2. Operator Injection**
Inject MongoDB query operators like `$ne`, `$in`, `$regex`, `$where`.

- Example: `{"username":{"$ne":"invalid"}}` — matches any username that isn't "invalid" → bypasses login

---

### Extracting Data

- Use `$where` with JavaScript to read data character by character
- Use `$regex` to probe field values (e.g., does password start with `a`?)
- Use `Object.keys(this)` to discover unknown field names

---

### Timing-Based Injection

When there's no visible error, inject a sleep payload like `{"$where": "sleep(5000)"}`. If the page loads slowly → injection worked.

---

### Prevention

- **Sanitize inputs** — allowlist accepted characters
- **Use parameterized queries** — never concatenate user input directly
- **Allowlist accepted keys** — to block operator injection