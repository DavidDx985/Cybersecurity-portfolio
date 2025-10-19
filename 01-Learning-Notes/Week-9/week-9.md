# 🗓️ Week 9 Progress Report

---

This week I moved into **privilege escalation (PrivEsc)** territory — the stage where low-privilege access turns into full system control (if you’re careful and lucky). I also spent time exploring Hack The Box Academy lab/retired machine options so I can practice PrivEsc techniques safely.

---

## 🔐 Privilege Escalation — Overview & Checklist

When you land on a system as a low-priv user, PrivEsc is a process of careful, methodical discovery. My checklist and notes this week:

1. **PrivEsc checklist (what to try first)**  
   - Run safe enumeration (see next item).  
   - Look for SUID binaries, weak `sudo` rules, misconfigured services, world-writeable files/dirs, and running processes with high privileges.  
   - Consult curated resources (HackTricks, PayloadsAllTheThings) for known techniques and quick checks.

2. **Enumeration scripts** — quick automated reconnaissance (use with caution; noisy)  
   - **Linux:** `LinEnum`, `linuxprivchecker` (or similar scripts) — find SUIDs, sudo rights, kernel info, cron jobs, etc.  
   - **Windows:** `Seatbelt`, `JAWS` — gather AD info, local policies, services, scheduled tasks.  
   - ⚠️ *Note:* automated scripts are great for speed but may trigger alarms on real systems. In sensitive environments, manual enumeration is safer.

3. **Kernel exploits**  
   - Older kernels can have local privilege escalation CVEs. If kernel vulnerabilities exist, proceed with extreme caution — test in a VM first and verify impact and stability.

4. **Vulnerable software**  
   - Check installed software versions. Outdated services often have publicly available local exploits.

5. **User privileges & mechanisms**  
   - Look for sudo misconfigurations, SUID binaries, service tokens, or Windows token impersonation techniques that allow command execution as root/SYSTEM.

6. **Exposed credentials (low-hanging fruit)**  
   - Search logs, config files, backup files, user history (`~/.bash_history`), web app config, and home directories for plaintext credentials, API keys, or tokens.

---

## 🧭 Hack The Box Academy — Labs & Machines

- I navigated HTB Academy structure: modules, labs, and the retired/active machine lists.  
- Planning: pick retired/vulnerable boxes that match PrivEsc topics (SUID, sudo, kernel exploits) and practice end-to-end: initial access → enumeration → PrivEsc → post-exploitation notes.

---

## 🎯 Strategy & Study Focus

- I’m pausing CompTIA A+ for now — my uni syllabus includes a Network Security course that maps closer to **Network+** content. It makes sense to prioritize Network+ prep next, then return to A+ later when the timing fits.  
- Lesson learned: sometimes stepping back and aligning priorities saves time and keeps momentum.

---

## ✅ Reflection & Next Steps

- **What went well:** I have a clearer PrivEsc checklist and know which automated tools to use (and when to avoid them).  
- **Challenges:** Balancing safe automated checks vs. stealthy manual enumeration; kernel exploit risk management.  
- **Next week:**  
  - Pick 2–3 retired HTB boxes focused on PrivEsc and run full lab cycles (in VMs).  
  - Practice manual enumeration commands in addition to scripts so I can be stealthy when needed.  
  - Start Network+ topics (routing/subnetting) lightly to align with course schedule.

> **Quote:** “Even your mistakes teach you a lesson or two — realize that and keep going.”
