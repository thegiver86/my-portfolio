# Systems Engineering & Cybersecurity Portfolio

## Phase 1: W1D1_Terminal Velocity

* **The Bare-Metal Bypass:** I forced an offline installation of Ubuntu Server when the Linux Kernel failed installing.
* **The Network Forgery:** I manually wrote Netplan YAML files, assigned IP addresses, and reset the virtual interfaces to force the router to establish a connection after an incomplete offline installation.
* **The Tunnel Construction:** I configured NAT Port Forwarding, bypassed the host's strict host-key checking (the SSH bouncer), and SSH'd straight into my headless VM.
* **The Pilot's Seat:** I successfully bridged VS Code directly to my remote Linux server via SSH.
* **The Dark Room Navigation:** I mastered Absolute vs. Relative paths, discovered hidden files (`ls -la`), and extracted system artifacts across the Linux filesystem hierarchy.
* **The Artifact Push:** I authenticated the GitHub CLI directly from the terminal, resolved a Git branch versioning conflict (`master` to `main`), and pushed my discovery.txt file to github, from the terminal.### TLAB-01: Detected 2 Unique Critical Threats


# Operation: S19 The Invisible Scout (Passive Security Audit)

## 📌 Overview
This repository contains the Threat Profile artifact generated during a comprehensive Passive Security Audit. The objective of this operation was to execute the Intelligence Cycle to map the external attack surface of a target organization without directly interacting with their infrastructure (zero-packet reconnaissance). 

*Note: While the simulated scenario targeted a fictitious acquisition named "CloudNano," the actual OSINT methodologies were executed against a live proxy target with a public bug bounty program (Uber) to demonstrate real-world data gathering.*

## 🛠️ Skills & Methodologies Demonstrated

### 1. IoT & Infrastructure Profiling (Shodan)
* **Geographic Targeting:** Filtered global internet-facing devices by specific geographic regions to isolate regional infrastructure.
* **Vulnerability Banner Grabbing:** Bypassed the need for premium vulnerability scanners by querying raw service headers. Successfully identified exposed and historically vulnerable services in the wild, including:
  * Windows Remote Desktop Protocol (`port:3389`) exposures, highlighting ransomware entry points.
  * Backdoored FTP servers (`vsFTPd 2.3.4` on `port:21`).
  * Identified artificial anomaly patterns (Honeypots).

### 2. Subdomain Enumeration
* Utilized **Sublist3r** to query multiple search engines (Baidu, Yahoo, Google, Bing) and public DNS records to uncover hidden organizational infrastructure.
* **Troubleshooting/Pivoting:** Successfully navigated API rate-limiting blocks (from VirusTotal/DNSdumpster) by allowing multi-threaded background processes to complete, ultimately extracting over 60 active subdomains for the proxy target, including sensitive development and authentication portals (`auth`, `staging-pilot`).

### 3. Tech Stack Mapping & Threat Intelligence
* Passively fingerprinted the target's technology stack using **BuiltWith**.
* Identified third-party enterprise integrations (e.g., Salesforce, Mixpanel) to assess supply-chain and misconfiguration risks.
* Synthesized raw OSINT data into a professional **Threat Profile**, articulating not just the technical findings, but the real-world business dangers they pose (e.g., credential stuffing via exposed auth portals, API data leaks via CRM misconfigurations).

## 📁 Artifacts
* `ThreatProfile_CloudNano.md`: The finalized intelligence report detailing discovered subdomains, mapped technology stacks, and prioritized exposure points.

## 💻 Technical Stack Used
* **CLI Tools:** `sublist3r`, `curl`, `bash`, `git`
* **OSINT Platforms:** Shodan.io, BuiltWith.com, crt.sh (Certificate Transparency), Exploit-DB (GHDB)
* **Environment:** Ubuntu Linux VM
