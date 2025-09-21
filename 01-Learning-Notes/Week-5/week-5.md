# Week 5 Report  

**A+ Prep**  
This week was all about *wireless wizardry* and *network sorcery*. Here’s what I tackled:  

- **Wireless Network Tech**  
  - Explored **802.11 standards**:  
    - 802.11ac → Wi-Fi 5  
    - 802.11ax → Wi-Fi 6  
    - 802.11be → Wi-Fi 7 (*faster internet than my brain processing Monday mornings*)  
  - **Wi-Fi frequencies**:  
    - **2.4GHz** → Great range, slower speeds. Think “grandma’s Wi-Fi.”  
    - **5GHz** → Faster but shorter range. Think “Wi-Fi sprinter.”  
    - **6GHz** → Even faster, needs line-of-sight. Think “future-proof rocket Wi-Fi.”  
    - These frequencies are given **channel numbers** to make life easier. Example: 2.437GHz = Channel 6.  
  - **Bandwidth** → Amount of frequency in use (20, 40, 80, 160 MHz… bigger pipe, more data).  
  - **Bluetooth** → Uses 2.4GHz in the ISM band. Short range, handy for headsets and controllers.  
  - **RFID** → For badges, pet IDs, and tracking. Works with radar-style tech.  
  - **NFC** → Built on RFID. Think tap-to-pay or quick device pairing.  

- **Network Services**  
  - **DNS** → Converts names ↔ IPs (with fun tools like `dig` and `nslookup`).  
  - **File sharing** → SMB (Windows), AFP (Mac).  
  - **Print servers** → Hook printers to networks using SMB, IPP, or LDP.  
  - **Mail servers** → Store/send emails.  
  - **Syslog** → Standardized message logging (ties into SIEMs).  
  - **Web servers** → Run HTTP/HTTPS.  
  - **Authentication servers (AAA)** → Handle access control.  
  - **Database services** → Relational DBs linked by SQL.  
  - **NTP** → Synchronizes device time.  
  - **Spam gateways** → Email spam filters.  
  - **All-in-one security appliances** → Next-gen firewalls with URL filters, VPNs, malware inspection.  
  - **SCADA/ICS** → Specialized for industrial control and monitoring.  
  - **Legacy systems** → Old but still kicking in many networks.  

- **DNS Deep Dive**  
  - Explored TLDs (.com, .org, .net).  
  - Checked DNS records (A, TXT, SPF, DKIM).  
  - Learned practical configuration using `dig` (Linux/Mac) and `nslookup` (Windows).  

---

**Hack The Box**  

- **Module 2: Getting Started**  
  - Got insights into structuring penetration tests.  
  - **InfoSec overview**: Protecting data from unauthorized access or changes.  

- **Risk Management Cycle**  
  - Identify → Analyze → Evaluate → Deal with → Monitor.  

- **Red vs Blue Team**  
  - **Red team** → Offensive (pentesting, social engineering).  
  - **Blue team** → Defensive (monitoring, strengthening systems).  

- **Linux & Hypervisors**  
  - Reviewed different Linux distros.  
  - Learned about hypervisors for hosting multiple VMs (useful for labs).  

- **Staying Organized**  
  - Keep separate folders for internal vs external pentests.  
  - Use different machines for practice vs client work (no mixing up!).  

- **VPNs**  
  - **Client-based VPN** → Requires extra software.  
  - **SSL VPN** → Software-free, uses browser + SSL gateway, often limited to web apps.

---

## Reflection  

This week was packed: from wireless tech and DNS magic on the A+ side to learning about risk management and VPNs in Hack The Box.

**Quote of the Week:**  
> *“Dream big. Start small. Act now.”* – Robin Sharma  
