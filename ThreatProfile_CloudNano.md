# TARGET THREAT PROFILE: CloudNano 
**Classification:** Passive Security Audit
**Operator:** ## 1. Subdomain Discovery 
* **Tool Used:** Sublist3r
* **Subdomains Found:** * [staging-pilot.ucollect.uber.com] 
  * [appsec-analysis.uber.com] *[auth.uber.com] 

## 2. Tech Stack Mapping 
* **Tool Used:** BuiltWith / Wappalyzer
* **Identified Technologies (CMS/CDN/Backend):** * [Salesforce] 
  * [Mixpanel] 

## 3. Major Exposure Points & Dangers 
*(List three major exposure points discovered during your OSINT audit and explain why they are dangerous)*
1. **[Subdomains]:** [Discovered an exposed staging environment (staging-pilot.ucollect.uber.com). Danger: Staging environments often lack the strict firewall rules and monitoring of production servers, making them an easy entry point for attackers to exploit unpatched development code.] 
2. **[Tech Stack]:** [Identified the use of third-party platforms like Salesforce via BuiltWith. Danger: If the integration between Uber's custom app and Salesforce is misconfigured, it could lead to an API data leak, exposing customer or employee records.] 
3. **[Shodan/Ports]:** [identified servers exposing RDP (Port 3389) in the wild. Danger: Exposed Remote Desktop Protocol is a primary vector for Cyber Criminals to brute-force their way into a network and establish a foothold.] 
