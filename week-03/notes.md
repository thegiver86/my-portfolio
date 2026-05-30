# Week 3: Python Scripting for Security
**Commands & Logic Used:**
- `subprocess.run(["grep", ...])`: I used this Python module to pass native bash commands to the Linux subsystem from within my script, capturing the output for analysis.
- `json.dump()`: I used this to format our extracted threat actor IPs into a clean, machine-readable JSON dictionary for SIEM ingestion.
**TLAB-03 (Operation Automated Hunt):** Completed. Built an end-to-end Python pipeline to detect brute force attacks in `auth.log` and export the alerts.
