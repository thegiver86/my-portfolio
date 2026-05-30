# Week 11: Network Defense & Perimeter Hardening
**Commands & Logic Used:**
- `iptables -A OUTPUT -d 198.51.100.0/24 -j DROP`: I deployed this egress firewall rule to sever the adversary's outbound connection to their Command & Control (C2) server.
- `alert tcp any any -> 172.90.0.10 80 (msg:"Malware"; content:"Ghost_Scanner";)`: I engineered this Suricata IDS rule to perform deep packet inspection and catch malicious strings bypassing the firewall.
**TLAB-11 (Operation Fortress):** Completed. Architected a multi-layered Defense in Depth strategy utilizing UFW, Suricata, and Sysmon to break an attacker's kill chain at three independent layers.
