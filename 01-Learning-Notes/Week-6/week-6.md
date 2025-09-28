# 🗓️ Week 6 Progress Report

---

## 💻 CompTIA A+ Prep — Networking Fundamentals & Devices

This week I focused on DHCP, VLANs/VPNs, and a tour of common network devices. Short version: networks are organized chaos, and DHCP is the helpful intern that hands out IP addresses so everything can talk.

### 🧾 DHCP (DORA)
DHCP automates IP assignment using the DORA process:
- **D**iscover — client finds a DHCP server  
- **O**ffer — server offers an IP lease  
- **R**equest — client requests/locks the offered lease  
- **A**cknowledge — server confirms the assignment

A DHCP server has a pool of IPs called the **DHCP scope**. You can **exclude** specific addresses from that pool (useful for printers, servers, devices you want static IPs for). To always give the same IP to a device, bind its **MAC address** to an IP (DHCP reservation).

---

### 🔀 VLANs vs VPNs (short & lucid)
- **VLAN (Virtual LAN)** — logically segments devices on the same physical network into separate broadcast domains. Devices on different VLANs *can't* talk unless you route between them. Good for separating departments (e.g., guest vs staff).
- **VPN (Virtual Private Network)** — securely connects remote networks or clients over the internet (encrypts traffic). Types include **client-based** (a VPN app on your device) and **site-to-site** (connects two networks).

---

### 🖧 Network Devices & Terms I Covered
- **Router** — routes traffic between IP subnets.  
- **Switch** — forwards frames by MAC address; can be **unmanaged** (plug-and-play) or **managed** (supports VLANs, SNMP, redundancy).  
- **Access Point** — bridges wired network to wireless, forwards by MAC.  
- **Patch panels / Cable infra / NICs** — physical wiring and ports (RJ-45).  
- **PoE (Power over Ethernet)** — single cable for power + data (endspan = switch provides power; midspan = injector provides power).  
- **Firewalls** — filter traffic (layer 4 by port/protocol; some inspect application data).  
- **Modems / DSL / ONT** — ISP termination points (cable, digital subscriber line, fiber optical network terminal).  
- **NTP** — time sync across devices.  
- **Syslog & SIEM** — logging standard + central analysis.  

---

## 🔐 Hack The Box — InfoSec Concepts & Tools

This week I moved from theory to **practical enumeration** and some initial hands-on exploration.

### 🔎 Common Terms & Tools
- **Shells**: reverse shell, bind shell, web shell — ways to interact with a target after compromise.  
- **Ports**: logical endpoints (HTTP = 80, HTTPS = 443). TCP is connection-oriented; UDP is connectionless.  
- **Web server**: handles HTTP requests and serves pages.  
- **OWASP**: core web app security reference.

### 🔧 Basic Tools Practiced
- **SSH** — secure remote shell: `ssh user@host`  
- **Netcat** — connect to arbitrary ports, banner grab, simple file transfers: `nc host port`  
- **Tmux** — terminal multiplexer (run many shells in one window).  
- **Vim** — advanced editor for quick edits.

---

## 🛠️ Service Scanning & Hands-on Work

I started doing real enumeration and banner-grabbing — small but meaningful wins:

- **Service scanning with Nmap**
  - Default Nmap scans top 1000 TCP ports unless asked otherwise.
  - Useful flags I used:
    - `-sC` → run default NSE scripts for more info  
    - `-sV` → service/version detection  
    - `-p` → specify ports (e.g., `-p 1-65535` to scan all TCP ports)
- **Banner grabbing** with `netcat` to identify services
- **FTP anonymous login** — I connected to an FTP server, logged in as `anonymous`, discovered credentials in a file and downloaded it using `get`. (Practical: this demonstrates how careless public services can leak secrets.)

**Result:** I successfully connected to an open port with `nc` and `ftp`, pulled a file with credentials, and practiced documenting the steps. First real hands-on exploitation steps — feels good.

---

## ✅ Reflection & Next Steps

- This week felt much more practical: DHCP + VLANs + VPNs on the A+ side, and real enumeration + banner grabbing on the HTB side.  
- Key takeaway: **enumeration is everything** — spend time mapping services, versions, and configs before you try to exploit anything.  
- Next week I’ll:
  - Practice more Nmap scripts and `-sV` fingerprinting.
  - Start the web enumeration chapter on HTB
  - Continue A+ study on routing/subnetting and DHCP edge cases.

> **Inspiration:** “Small daily improvements are the key to staggering long-term results.” — keep stacking blocks.

---

