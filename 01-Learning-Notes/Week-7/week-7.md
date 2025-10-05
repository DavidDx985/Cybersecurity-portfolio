# 🗓️ Week 7 Progress Report

---

## 💻 CompTIA A+ Prep — IP, Subnets & Networking Tools

This week I dug into IP addressing, subnet basics, connection types, and the physical tools you’ll actually use when wiring stuff up. Short version: IPs let things find each other, and cable testers make sure you didn’t plug the internet into a sandwich.

### 🌐 IPv4 & IPv6 (clear & simple)
- **IPv4** — 32 bits total, written as four octets (e.g., `192.168.0.1`). Each IPv4 address should be unique on a network segment.
- **NAT (Network Address Translation)** — solves IPv4 shortage by letting many private devices share a single public IP. Devices keep private addresses locally; the router translates them when talking to the internet.
- **IPv6** — 128 bits total. Common practice: IPv6 addresses are split into a **64-bit network prefix** and a **64-bit interface identifier** (so you’ll often see a `/64`). This gives a huge address space and eliminates most NAT needs.

### 🧩 IP assignment & DHCP reminders
- **Subnet mask** tells a device which addresses are local vs remote (so it knows when to use the gateway).  
- **Default gateway** is the local router IP used to reach other subnets/internet.  
- **DHCP reservations** let you tie a device’s MAC to a fixed IP (printer gets same IP every time).  
- **APIPA** (Automatic Private IP Addressing) — when DHCP fails, an OS picks an IP in `169.254.0.0/16`. Before using it, the host ARPs the address to avoid collisions with other devices that have the same IP that it wants to use.
- **APIPA** range: "169.254.0.0-169.254.255.255"

### 🔗 Internet connection types & network categories
- Connection types: **Satellite, Fiber, Cable (DOCSIS), DSL/ADSL, Cellular, WISP**.  
- Network types: **LAN / WAN / PAN / MAN / SAN / WLAN**.

### 🔧 Physical tools & cable gear
- Cable crimpers, RJ-45 modular plugs, Wi-Fi analyzer, tone generator, punch down tool, cable testers, loopback plugs — the real life “weapons” of networking.

---

## 🔐 Hack The Box — Web & Service Enumeration (Hands-on)

This week I started real **web enumeration** and practiced the tools & techniques that find things attackers (and defenders) care about.

### 🔎 Directory & Subdomain Enumeration
- **Gobuster** for directory brute forcing (use `dir` mode) and DNS subdomain discovery (use `dns` mode).  
  - HTTP status codes to watch for:
    - `200` → OK (found something)  
    - `403` → Forbidden (found a protected resource)  
    - `301/302` → Redirect (resource moved)  
- **Robots.txt** can leak admin pages or hidden paths — always check it.

### 🛠️ Banner grabbing & fingerprints
- **WhatWeb** → quickly extracts web server / framework info.  
- **Eyewitness** → screenshots web apps to speed triage.  
- Banner grabbing can reveal app names/versions to check for known exploits.

### 🔍 Public exploits & metasploit
- After service/version enumeration, search for public exploits (Google + `exploit` OR use `searchsploit`):  
  - Example: `searchsploit openssh 7.2`  
- **Metasploit (msfconsole)** is a fast way to try curated exploits in a lab — great for prototyping and PoC work.

---

## ✅ Reflection & Next Week Plan

This week I moved from basics into *real* enumeration: directories, subdomains, banners, and public exploit discovery. I can feel the tools clicking together — now it’s time to build muscle memory.

**Next week:** No new lessons — full practice week.
- Master `nmap` flags (`-sC`, `-sV`, `-p`, full port scans)  
- Practice `gobuster` (dir + dns modes) and `whatweb`  
- Use `netcat` for banner grabbing and small shell tests  
- Try at least **5 hands-on labs** on my test site with the above tools, document each step and push writeups to GitHub

> **Quote for the week:** “Skills are built by repetition, not by watching.” — so I’ll repeat until it’s muscle memory.

---

