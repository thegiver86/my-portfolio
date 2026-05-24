# OMNI-PORTAL ASSESSMENT REPORT
**Operator:** **Deadline:** April 5 @ 11:59 PM 

## PHASE 1: AUTH BYPASS (SQLi)
* **Payload Used:** [' OR 1=1 --]
* **Result:** Successfully bypassed login and obtained 'auth_token' cookie.

## PHASE 2: CLIENT-SIDE HIJACK (XSS)
* **Stored XSS Payload:**[ <script>alert(document.cookie)</script>]
* **Secret Cookie Captured:** [session_id=admin_secret_99812_do_not_share; auth_token=SUPPORT_TIER_1_SECRET_TOKEN]

## PHASE 3: API ENUMERATION (BOLA)
* **Insecure Order ID:** [501]
* **Confidential Data Leaked:** [$15,000,00 - Confidential Server Lease]

## PHASE 4: THE REMEDIATION
* **Fix for SQLi:** * **Fix for XSS:**
* **Fix for API BOLA:**
SQLi Fix: use Parameterized Queries (Prepared Statements) so the database engine treats input as data, not executable code
XSS Fix: implement Output Encoding (e.g., converting < to &lt;) to ensure the browser treats user-supplied text as inert data rather than active HTML/JS elements.
API BOLA Fix: implement Resource-Based Authorization (server-side checks). The API will verify that the user_id authenticated in the session matches the owner of the order_id being requested before returning any data.
