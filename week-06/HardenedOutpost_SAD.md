# Security Architecture Document: The Hardened Outpost
**Engineer:** turtle
**Status:** SECURE

## 1. Perimeter Hardening
* **SSH Configuration:** Disabled `PermitRootLogin` and `PasswordAuthentication` to protect against brute-force attacks.
* **UFW Defense:** Implemented a default-deny ingress policy. Explicitly punched holes for port 22 (Management) and port 8080 (Web Traffic).

## 2. Automated Auditor
* Engineered a Python-based watchdog script utilizing the `os` module.
* The script successfully interacts with the Linux sub-system to monitor disk space (`df -h`) and verify cross-network ICMP connectivity to the Windows Domain Controller, writing the output securely to `/var/log`.

## 3. Containerized Air-Gapped Stack
* **Frontend:** Deployed an Nginx container bound to host port 8080.
* **Backend:** Deployed a MySQL database container entirely isolated on an `internal: true` Docker network. 
* **Verification:** The database has zero external routing, rendering it invisible to perimeter scans and securing it against direct external exploitation.
