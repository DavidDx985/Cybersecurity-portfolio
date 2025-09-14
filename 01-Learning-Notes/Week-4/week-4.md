# 🗓️ Week 4 Progress Report

---

Forward ever, backward never — Week 4 complete. This week I dug deeper into networking basics for A+ (common ports and how they matter) and finished the **Penetration Testing Process** module on Hack The Box, focusing on post-exploitation, lateral movement, and how a professional engagement is wrapped up. I expanded the notes so they’re useful later when I revisit them for writeups or reports.

---

## 💻 CompTIA A+ — Common Ports, Protocols & Port Types (Study Notes)

Knowing ports and protocols is essential for network troubleshooting, firewall rules, and service mapping during recon. Here’s a clearer explanation of what I covered this week.

### Ports & Protocols — what they mean and why they matter
A **port** is a logical endpoint on a host. When data reaches an IP address, the port tells the OS which application or service should handle the traffic. Firewalls often allow/deny traffic by port, so knowing standard ports helps both defenders and attackers map services.

**Common service ports (with brief explanations):**
- **FTP (File Transfer Protocol)**  
  - Data channel: **TCP/20**  
  - Control channel: **TCP/21**  
  - Used for transferring files between hosts. (Note: FTP is largely legacy and plain-text unless wrapped with TLS.)

- **SSH (Secure Shell)** — **TCP/22**  
  - Encrypted remote shell; used to log into servers securely and run commands.

- **Telnet** — **TCP/23**  
  - Plain-text remote shell. It’s insecure and mostly deprecated (don’t use it for production).

- **SMTP (Simple Mail Transfer Protocol)** — **TCP/25**  
  - Used for transferring email between mail servers (server-to-server).

- **DNS (Domain Name System)** — **UDP/53** (queries), sometimes **TCP/53** (zone transfers, larger responses)  
  - Translates hostnames (example.com) into IP addresses.

- **DHCP (Dynamic Host Configuration Protocol)** — **UDP/67/68**  
  - Automatically assigns IP addresses and network config to clients.

- **HTTP / HTTPS** — **TCP/80** / **TCP/443**  
  - HTTP: web traffic in plain text; HTTPS: secure (TLS) web traffic.

- **POP3 / IMAP** — **TCP/110** / **TCP/143**  
  - Protocols for retrieving email from servers (POP3 downloads, IMAP manages mailboxes across clients).

- **SMB / CIFS** — **UDP/137**, **TCP/139**, **TCP/445**  
  - Windows file and printer sharing. Older CIFS variants exist; newer SMB uses TCP/445.

- **LDAP (Lightweight Directory Access Protocol)** — **TCP/389**  
  - Directory services (user accounts, groups, organizational info).

- **RDP (Remote Desktop Protocol)** — **TCP/3389**  
  - Microsoft Remote Desktop service.

### Ephemeral vs Non-ephemeral (well-known) ports
- **Non-ephemeral (well-known) ports**: fixed, standard ports assigned to common services (0–1023 and sometimes up to 49151 by convention). Examples: 22 (SSH), 80 (HTTP), 443 (HTTPS). These are what you map during service enumeration.
- **Ephemeral (dynamic) ports**: high-numbered ports (usually above 1024) temporarily assigned by the OS for client-side connections (e.g., when your browser connects to a web server, the server is at port 80 but your machine uses an ephemeral port to receive responses). These are short-lived and change per session.

**Why this matters:** when designing firewall rules or analyzing packet captures, you need to know which ports are service endpoints vs client ports.

---

## 🔐 Hack The Box — Post-Exploitation, Lateral Movement & Professional Practice

This week I completed the **Penetration Testing Process** module (the whole lifecycle) and focused on the **post-exploitation** phase: what an attacker or tester does after they first gain access.

### Post-Exploitation — what it is
**Post-exploitation** is everything you do *after* getting a foothold. The goal is to gather sensitive information, determine the business impact, move laterally if needed, and test persistence, all while documenting evidence for the final report.

Key activities and explanations:

- **Evasive testing (non-evasive / hybrid / fully evasive)**  
  - *Non-evasive*: minimal stealth; used when detection testing is not the goal (safe and fast).  
  - *Hybrid evasive*: balance between stealth and speed; test both detection and exploitation.  
  - *Fully evasive*: try to avoid IDS/AV/EDR detection as much as possible; used to evaluate defensive controls.  
  - *Why it matters:* some tests should check whether defenses detect an attack — that requires intentional stealth.

- **Internal information gathering**  
  - With higher privileges you can enumerate local users, scheduled tasks, credentials, local config files, network interfaces, routing tables, DNS cache, ARP tables, and logs. This internal view often reveals sensitive data or pivot points that external recon cannot see.

- **Pillaging**  
  - Collecting sensitive artifacts from the host (password files, API keys, configuration files, tokens). This is the “loot” phase — you identify what an attacker could steal.

- **Persistence**  
  - Techniques that maintain access (e.g., adding backdoors, scheduling tasks, creating new privileged accounts, or manipulating startup scripts). In professional engagements, persistence must be pre-approved and carefully planned because it changes the environment.

- **Vulnerability assessment (internal)**  
  - Reassess the host and network now from an internal view: some vulnerabilities are only visible after access (local misconfigs, weak service credentials, outdated local packages).

- **Privilege escalation**  
  - Techniques to move from a low-privilege user to root/Administrator. Common methods: SUID binaries, weak sudo rules, kernel exploits, services running as root, unquoted service paths, and insecure credential storage.

- **Data exfiltration**  
  - Simulating extraction of sensitive data in a controlled way (e.g., moving a sample file off the network). Important: always follow the rules of engagement and scope; do not exfiltrate real customer data without explicit permission.

---

### Lateral Movement — expanding influence across the network
After mastering a host, testers try to access other systems:

- **Pivoting / tunnelling**: using the compromised host as a jump point to reach internal-only resources (e.g., using SSH/port forwarding or SOCKS proxies).  
- **Repeat the exploitation cycle on other hosts** (info gathering → vuln assessment → exploitation → post-exploit).  
- **Business impact consideration:** lateral movement can expose critical systems (financial servers, HR databases). In real incidents, this can lead to extortion, major data loss, or regulatory fines — so demonstrating the impact is a key deliverable.

---

### Proof of Concept (PoC)
A **PoC** in pentesting proves that a vulnerability is real and exploitable without causing unnecessary damage.

- **Types of PoC:**  
  - *Non-destructive*: step-by-step reproduction or a safe script that demonstrates access (preferred for reports).  
  - *Exploit code*: automated scripts or code that trigger the vulnerability; should be tested in a replica VM first.

- **Best practice:** If no public PoC exists, replicate the target in a VM, test your exploit there, refine it, and then run a controlled PoC against the real target only after confirming safe parameters.

---

### Post-Engagement — clean, report, and leave
Wrap up is as important as the attack:

- **Cleanup** — remove shells, tools, created accounts, scheduled jobs, persistence mechanisms. Leave the environment as you found it (unless remediation is contracted).  
- **Documentation & reporting** — assemble evidence: exact steps, timestamps, artifacts, severity, reproducible PoC, and remediation steps.  
- **Report review meeting** — walk the client through findings, answer questions, and prioritize fixes.  
- **IMPORTANT RULE:** testers should remain impartial third parties and not perform any remediation on the target systems( such as fixing code, patching systems or configuration changes in active directory). Unless contracted to remediate, don’t change or patch client systems — only recommend.

---

## 🧭 Vulnerability Assessment — clearer view of the types
During vulnerability assessment, we don’t just list issues — we analyze and categorize them. Short definitions:

- **Descriptive** — *What* the vulnerability is (a factual listing). Example: “Service X is running version Y.”  
- **Diagnostic** — *Why* it exists (root cause). Example: “Service X is misconfigured because default credentials are present.”  
- **Predictive** — *What could happen* if exploited (likely impact). Example: “If exploited, attackers could gain admin access to customer data.”  
- **Prescriptive** — *How to fix it* (recommended remediation). Example: “Update service to version Z; remove default credentials; apply principle of least privilege.”

Putting all four together produces a useful, actionable assessment for the client.

---

## ✅ Week 4 Wrap-Up

- **HTB:** Completed the *Penetration Testing Process* module and practiced post-exploit thinking (pillaging, persistence, privilege escalation, lateral movement).  
- **A+:** Studied common ports & protocols and understood ephemeral vs non-ephemeral ports — useful for firewall rules and packet analysis.  
- **Outcome:** I finished the first HTB module and feel more comfortable linking technical actions (exploit steps) to business impact and reporting. Also getting better at documenting the technical steps I take — which will make my GitHub writeups stronger.

✨ **Inspiration of the Week:**  
> *“Small consistent progress compounds into big skills. Keep showing up.”*  

On to **Getting Started** next week — more hands-on HTB labs and A+ device troubleshooting. 🚀
