# Week 8: Exploitation Frameworks
**Commands Used:**
- `sudo awk 'BEGIN {system("/bin/sh")}'`: I ran this GTFOBins exploit to leverage a misconfigured SUID binary and escalate my privileges to root.
- `msfconsole`: Initialized the Metasploit framework to deliver the Samba usermap_script exploit.
**TLAB-08 (Operation Deep Pivot):** Completed. Exploited a vulnerable service, escalated to root, established persistence via crontab, and pivoted to map an internal database.
