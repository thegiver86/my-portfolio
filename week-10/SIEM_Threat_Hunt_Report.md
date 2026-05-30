SIEM Threat Hunt Report: The Central Nervous System
1. Objective
To deploy a local ELK (Elasticsearch, Logstash, Kibana) stack, ingest enterprise logs, and utilize KQL (Kibana Query Language) to reconstruct a full breach timeline from initial access to data exfiltration.

2. Key Concepts Mastered

SIEM (Security Information and Event Management): The "central nervous system" of a SOC. It aggregates logs from multiple endpoints, firewalls, and servers into a single searchable database.

Elasticsearch & Kibana: Elasticsearch acts as the database that stores and indexes the logs. Kibana is the graphical frontend that allows analysts to query and visualize that data.

Data Views (Index Patterns): Configuration rules that tell Kibana which indices (databases) to pull data from. We used the wildcard enterprise_logs* to capture all relevant mock data.

Log Correlation: The process of taking an isolated indicator (like an external IP from a failed login) and searching it across different log types (Web Server, Windows Security, Firewall) to track lateral movement.

3. Execution & Commands

Port Forwarding: Bypassed the NAT network barrier by using VSCode's built-in port forwarding to map the headless VM's port 5601 to the host machine.

Manual Data Injection: When the database booted too slowly to catch the initial automated log injection, we used raw curl -X POST commands to manually push the JSON formatted evidence directly into the Elasticsearch API (http://localhost:9200/enterprise_logs/_doc/).

4. The Attack Timeline Summary
Using KQL, we traced the attacker's path:

Initial Access: The attacker (198.51.100.44) successfully executed a malicious payload via a Web Server POST request to /api/upload.

Lateral Movement: The attacker pivoted to an internal machine (10.0.5.15) and escalated privileges to Domain Admin (Windows Security Event ID 4624).

Exfiltration: Finally, the attacker used that internal machine to transfer 4.5 GB of data out of the network over port 443 back to their original IP.
