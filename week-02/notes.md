# Week 2: Networking & Protocol Analysis
**Commands Used:**
- `ip route add default via 192.168.10.1`: I ran this to manually reconstruct the corrupted Layer 3 routing table so the machine could communicate with the external gateway.
- `ss -tuln`: Used to interrogate the transport layer and find cloaked TCP/UDP services running locally without needing Nmap.
**TLAB-02 (Operation Blackout):** Completed. Remediated subnet isolation, fixed DNS poisoning in `/etc/hosts`, and captured a TCP 3-way handshake.
