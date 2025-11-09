# 🗓️ Week 12 Progress Report

**Focus this week:** I stepped back from exploitation & lateral movement to finish the last two chapters of the **“Getting Started”** module — specifically the **Common Pitfalls** section — and completed the final “Knowledge Check” box for the module.

Short version: lots of practical troubleshooting notes (VPN, Burp, SSH) — the small stuff that breaks labs in real life and wastes time if you don’t know how to fix it.

---

## 🔧 Common Pitfalls — Practical fixes I learned

### 1. VPN issues (HTB VPN)
- **Connect with OpenVPN** (example):
```bash
sudo openvpn ./htb.ovpn
````

* **Verify the tunnel interface** (tun0 is the usual interface):

```bash
ip -4 a show tun0
```

You should see an IP assigned to the `tun0` interface if the VPN is up.

* **Check routing table / default routes**:

```bash
sudo netstat -rn
# or the modern equivalent
ip route show
```

Look for routes pushed by the VPN and make sure traffic to HTB target IPs is routed via `tun0`.

* **HTB VPN notes / gotchas**

  * Only **one** HTB VPN connection per account/device is supported — connecting the same profile from multiple devices will fail.
  * If you experience lag, switch to a **closer regional VPN server** (Europe / US / Singapore / Australia) for lower latency.
  * If the VPN looks connected but you can’t reach labs, re-check routes and `tun0` IP; then try reconnecting.

> Tip: keep a small troubleshooting snippet in your notes to run immediately when a connection acts up.

---

### 2. Browser proxy & Burp Suite

* **Burp Suite** sits between your browser and the web as an intercepting proxy. If Burp is closed but your browser still uses the proxy, the pages won’t load (traffic is routed to a dead local proxy).
* **Fixes**

  * If you use a proxy switcher like **FoxyProxy**, toggle it off after you stop using Burp.
  * Or check the browser's proxy settings manually and disable them:

    * Firefox: `Preferences → Network Settings → Manual proxy configuration` → disable or switch to system settings.
  * If using system proxies (NetworkManager), make sure those are restored to normal after you finish testing.

---

### 3. SSH authentication & key problems

* If SSH auth starts failing (permissions, key mismatch), regenerate or recreate your keys:

```bash
ssh-keygen -t ed25519 -C "you@example.com"    # generate a new key
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

* Verify remote `authorized_keys` entries and ensure the file permissions are correct (`~/.ssh` 700, `~/.ssh/authorized_keys` 600).
* If you changed your private key or password, update the server-side key or credentials and test with:

```bash
ssh -v user@target.ip    # verbose output to debug auth problems
```

---

## 🧪 Knowledge Check box (module final)

* I completed the last HTB “Knowledge Check” box for the Getting Started module — it was still exploitation-based and a good way to validate all the troubleshooting lessons above in a proper lab environment.
---

## ✅ What I documented / pushed

* Added troubleshooting commands and notes to my lab notes so next time I can recover FAST from:

  * VPN connection issues
  * Burp/browser proxy misconfigurations  * SSH key/authentication errors

---

## 🔜 Next steps (Week 13 plan)

* Starting with the "Network Enumeration with nmap" module
***“Discipline is just choosing between what you want now and what you want most.” — Abraham Lincoln"***

