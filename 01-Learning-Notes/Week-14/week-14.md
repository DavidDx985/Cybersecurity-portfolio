

---

# **Week 14 – Nmap Deep Dive**

This week, I continued progressing through the **Network Enumeration with Nmap** module and focused on saving scan results, service enumeration, NSE scripts, performance optimization, and firewall/IDS evasion.

---

## 🔹 **Saving Nmap Scan Results**

Nmap allows saving scan outputs in different formats:

* **Normal output (`-oN`)** → saves as `.nmap`
* **Grepable output (`-oG`)** → saves as `.gnmap`
* **XML output (`-oX`)** → saves as `.xml`
* **All formats (`-oA`)** → generates all file types at once

### Convert XML → HTML

Using **xsltproc**, we can generate a readable HTML report:

```
xsltproc target.xml -o target.html
```

---

## 🔹 **Service Enumeration**

Useful flags:

* **Version scan:** `-sV`
* **Banner grabbing:** `-v` or `-vv`
* **Periodic stats:** `--stats-every=5s` or `5m`

---

## 🔹 **Nmap Scripting Engine (NSE)**

Nmap has **14 script categories**.
Basic syntax:

```
nmap <target> --script <category>
```

Example (banner grabbing for SMTP):

```
nmap <target> --script smtp-commands
```

This reveals SMTP interaction commands.

---

## 🔹 **Aggressive Scan**

The **`-A`** scan includes:

* OS detection (`-O`)
* Script scan (`-sC`)
* Version detection (`-sV`)
* Traceroute (`--traceroute`)

It’s powerful but noisier.

---

## 🔹 **Performance Optimization**

Nmap allows tuning:

* Timeouts
* Packet rates
* Bandwidth
* Scan delay
* Parallelism

Useful when scanning slow or unstable networks.

---

## 🔹 **Firewall & IDS/IPS Evasion Techniques**

### 🧱 Firewalls

Block untrusted or suspicious packets.

### 🛰 IDS

Detects malicious traffic and alerts.

### 🛡 IPS

Actively blocks suspicious traffic.

---

## **Evasion Methods**

### **1. ACK Scan (`-sA`)**

Used when a firewall drops SYN packets.

* Helps determine whether a firewall is stateful
* Doesn’t complete a full handshake
* Useful for bypassing packet filters

---

### **2. Decoy Scanning**

Mixes your real IP with fake ones inside the packet headers.

Concept:

> Target sees multiple IPs scanning it, making it harder to identify the real source.

Used *only in legal labs*, like HTB.

---

### **3. Scanning Using a Different Source IP**

Spoofing the source IP within the same subnet.

Concept:

> Scan appears to originate from inside the network.

Used in controlled learning environments.

---

### **4. DNS Proxying**

Used to analyze DNS servers and detect versions via **UDP 53**.

Conceptual example:

> Perform a version-related scan by sending packets that appear to originate from port 53.

---

### **5. VPS Rotation for IDS Evasion**

If an IP gets blocked:

* Switch to another VPS
* Retry from a new IP

This is a *defensive learning technique* to understand how systems detect repeated attempts.

And thats the end of the Network enumeration with nmap module. I learned a lot of new things and gain a better mastery of the nmap tool. 
Looking forward to starting the footprinting module next week, even though i don't have enough cubes -_-. But we keep going
---

# ⭐ **Quote of the Day**

**“Mastery isn’t about speed—it’s about clarity. Learn slow, understand deep, and the skills will follow you forever.”**

---


