---

# **Week 13 Progress Report**

This week, I focused fully on the **Network Enumeration with Nmap** module. The emphasis was on truly understanding how enumeration works and why it is one of the most critical stages in any penetration test.

---

## 🔍 **Enumeration Overview**

Enumeration is the process of identifying **all possible ways we can interact with or attack a target system**. It isn’t just about tools — it’s about observing **every piece of information** the target reveals.

Key things to look for:

1. **Functions or resources** that allow interaction with the target.
2. **Information leaks** that help us access the system or plan an attack.

---

## ⚙️ **Introduction to Nmap (Network Mapper)**

Nmap is written in **C, C++, Python, and Lua**, and is designed for:

* Host discovery
* Port scanning
* Network mapping
* Firewall/IDS testing
* Vulnerability assessment
* Scriptable enumeration (NSE)
* Service/OS detection

It can tell us whether:

* A host is up
* Which ports are open
* What services/software versions are running
* What OS the target is using

---

## 📌 **General Nmap Syntax**

```
nmap <scan type> <options> <target>
```

Most common scan:

* **-sS** (SYN scan)

Response behavior:

* **SYN-ACK → port open**
* **RST → port closed**
* **No response → filtered** (firewall)

Useful options:

* `-oA` → output results to files (all major formats)
* `--packet-trace` → show packets being sent/received
* `--reason` → display why Nmap labeled a port in a particular state

---

## 🚪 **Connect Scan (-sT)**

Uses a full TCP 3-way handshake.

**Pros:**

* Extremely accurate
* Can bypass firewalls in some cases

**Cons:**

* Very noisy (creates logs → easily detected)
* Slower

---

## 🌐 **Host & Port Scanning: What We Want to Learn**

* Open ports
* Services running
* Service versions
* OS information
* Any service misconfigurations or banners that leak info

---

## 🧱 **Nmap Port States**

| State          | Meaning                                |                                   |
| -------------- | -------------------------------------- | --------------------------------- |
| **Open**       | Target accepts connections             |                                   |
| **Closed**     | Responds with **RST**                  |                                   |
| **Filtered**   | Firewall blocks the probe; no response |                                   |
| **Unfiltered** | Host reachable but port state unknown  |                                   |
| **Open         | Filtered**                             | Possible firewall — can’t confirm |
| **Closed       | Filtered**                             | Seen in IP ID idle scans          |

---

## 🔐 **Filtered Ports Behavior**

If a firewall **drops packets**, Nmap rechecks by sending another packet.
If a firewall **rejects**, you may receive an ICMP type 3 error response.

---

## 📡 **UDP Scans:**

```
nmap -sU <target>
```

Useful for discovering services like:

* DNS
* SNMP
* DHCP
* TFTP

Slower but necessary for a complete profile.

---

## 🔍 **Version Scanning**

```
nmap -sV <target>
```

Used to detect:

* Service versions
* Software type
* Potential vulnerabilities

---

## **Quote of the Week**

**"The more you understand the map, the less you fear the terrain."**

Perfect for enumeration — the more you know about the target, the less guesswork you make during exploitation.

---

