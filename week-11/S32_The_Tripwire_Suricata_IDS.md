**Operation Debrief: "The Tripwire" (Suricata IDS)**
1. The Core Topic: Intrusion Detection vs. Firewalls
While Session 31 focused on building a Firewall (a physical wall that blocks traffic based on ports and IP addresses), Session 32 focused on deploying an IDS (Intrusion Detection System).
An IDS acts as a passive security camera. Instead of just looking at the outside of an envelope (the IP and Port), it performs Deep Packet Inspection (DPI). It opens the envelope, reads the letter inside, and compares the contents against a massive database of known malicious signatures. We used Suricata, which is the industry-standard, multi-threaded engine used by enterprise Security Operations Centers (SOCs).

2. The Problem Faced in the Lab
We faced two distinct layers of problems—one tactical, and one environmental:

The Tactical Problem: Our web server (Port 80) had to be open to the public so legitimate users could access it. However, a threat actor was bypassing our firewall by hiding their malware scanner inside standard Port 80 HTTP traffic.

The Environmental Problem: When we first deployed the IDS, it failed to trigger. We discovered that Suricata is incredibly strict—a single commented # line or formatting error will cause the engine to silently reject the rules. Later, Docker's virtual network switching isolated our host-machine traffic, preventing the passive IDS from "seeing" the packets fly by.

3. What We Looked For
We engineered the IDS to hunt for two specific Indicators of Compromise (IoCs):

Reconnaissance: Any ICMP (ping) packets destined for our web server, which indicates an attacker is mapping our network.

Malicious Payloads: TCP packets containing the exact string Ghost_Scanner_v1 hiding inside the HTTP application layer.

4. The Methodology: Commands, Actions, and Remediation
Here is exactly how you executed the mission and forced the environment to comply:

Writing the Logic (nano custom_ids.rules): We wrote raw Suricata signatures detailing exactly what traffic to look for (alert tcp any any -> 172.90.0.10 80) and what text to search for (content:"Ghost_Scanner_v1").

Engine Diagnostics (docker logs ids_sensor): When the IDS failed to fire, we didn't guess; we interrogated the engine's boot sequence. We found the 0 rules loaded error, identified the syntax formatting issue, corrected the text file, and reloaded the engine memory (docker restart ids_sensor).

Simulating the Attack (ping and curl -A): We acted as the adversary, firing ICMP packets and artificially spoofing our User-Agent header with curl -A to inject the malware signature directly into the web traffic.

Bypassing the Invisible Wall (docker exec ids_sensor): When Docker's network isolation hid our attacks from the sensor, we remediated the issue by forcing the attack to originate from inside the sensor container itself. This guaranteed the traffic crossed the monitored eth0 interface.

Log Analysis (eve.json & fast.log): We bypassed the legacy fast.log file and searched the modern, highly detailed eve.json output (grep -i "alert" eve.json) to definitively prove our custom Deep Packet Inspection rule successfully caught the malware.
