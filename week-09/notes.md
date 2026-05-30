# Week 9: Web Application Security
**Payloads Used:**
- `' OR 1=1 --`: Inserted this tautology payload into a login field to bypass authentication via SQL Injection.
- `<script>alert(document.cookie)</script>`: Injected this XSS payload to prove client-side code execution and exfiltrate session cookies.
**TLAB-09 (Operation Omni-Portal):** Completed. Audited a full-stack web application, successfully exploiting BOLA, SQLi, and XSS, and provided the necessary engineering fixes (Parameterized Queries and Output Encoding).
