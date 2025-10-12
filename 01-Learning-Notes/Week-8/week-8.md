Absolutely! Here's your full Week 8 progress report formatted entirely in Markdown, including every detail you provided:

```markdown
# Week 8 Progress Report

This is Week 8 and I didn’t take any CompTIA A+ preparations. I spent most of my time understanding some of the tools I used in the lessons last week like **Nmap**, **Gobuster**, and **Netcat**.

---

## Nmap

I understood some of the switches used with Nmap to perform different kinds of network and port analysis. These switches also serve as filters to the type of ports you want to access over a network of a particular device. Some of these parameters include:

- `-sC`
- `-s`
- `-v`
- `-P`

I also learned about **banner grabbing** with Netcat and how you can do the same task with Nmap using the script:

```bash
--script=banner
```

We also have Nmap commands that can scan a list of IP addresses inside a file.

I understood that before Nmap actually brings out the open ports, it conducts a **ping scan** to the target to see if the host is up. We can skip this ping test using the `-PN` switch.

---

## Gobuster

I went deeper with Gobuster and understood how the **directory** and **DNS** modes work.

- It simply does a **brute-force scan** on the destination website to find website directories using a specified word list.
- It does the same with the DNS mode.
- We can then use these details to find sensitive information from the website.

---

## Hack The Box Learnings

From Hack The Box this week, I learned about the **types of shells** and how they are required to enumerate the target system to take further control over it.

We can either use:

- **SSH**
- **WinRM** (on Windows)

to connect to the remote system.

Another way of connecting is through **shells**, which we have 3 types:

1. **Reverse Shell**
2. **Bind Shell**
3. **Web Shell**

---

### Reverse Shell

- Target connects to us.
- We initiate a Netcat listener for a specific port then execute a reverse shell command on the target system.

Example:

```bash
nc -lvnp 1234
```

Explanation of flags:

- `-l`: Netcat listening mode
- `-v`: Verbose mode; lets us know when we receive a connection
- `-n`: Disable DNS resolution so we only connect to IPs
- `-p 1234`: Port number that Netcat is listening on

---

### Bind Shell

- Target waits for us to connect and gives us shell access.
- We run a bind shell command on the compromised system.
- While it listens and waits for a connection, we use Netcat to connect to it.
- When we gain access, we would not be able to fully interact with the arrow keys to edit on the shell.
- So we need to upgrade our TTY using the **Python/stty method**.

---

### Web Shell

- It communicates through a web server and accepts our commands through HTTP parameters.
- They’re typically web scripts (e.g., PHP or ASPX) that accept our commands through HTTP requests like GET or POST parameters.
- These scripts execute our commands and print the output on the web page.

To upload the shell command:

- We place our web shell script into the remote host’s web directory (**webroot**) to execute the script through the web browser.

> **A great benefit of a web shell** is that it would bypass any firewall restriction in place since it opens a connection on the web browser rather than on a port.  
> **But the downside** is that it’s not as interactive as reverse and bind shells.
```

Let me know if you'd like this saved as a file or want help formatting future weeks too!
