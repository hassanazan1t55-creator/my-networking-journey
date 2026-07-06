# Day 9: Ports and Protocols

Today I am learning about Ports and Protocols. If the IP address is the building location, then ports are the doors to enter that building.

A computer or server has 65,535 ports. Each port runs a specific type of service called a Protocol.

---

## What is the Real Purpose of Ports and Protocols?

When your computer is browsing, emailing, and downloading at the same time, it uses ports to know which data belongs to which app.

- **The International Mall Analogy:** Think of a large mall (Computer/IP). Inside the mall, there are different shops. Shop No. 80 sells burgers, Shop No. 443 is a clothing showroom with a security guard, and Shop No. 21 is a cargo warehouse. Ports are exactly like these shop numbers.
- **The TV Channels Analogy:** Your home has one TV screen (IP Address). But different channels run on it. Channel 80 shows news, Channel 22 shows sports. Ports are the same channels for the internet.

---

## The Hacker's Mindset: How to Attack Ports

A hacker's first step is always Port Scanning (using tools like Nmap).

The hacker thinks: "I have the building's address (IP). Now let me check which of the 65,535 doors (Ports) are open, and what software is running behind them that has any weakness!"

---

## The 4 Most Important and Famous Ports

### Port 80 - HTTP (Hypertext Transfer Protocol)

**What it does:** This is used for regular and older websites. It sends data in plain text without any encryption.

**Hacker's Mindset:** *"If the target website is running on Port 80, the data is unencrypted. I can sit on this network and see all data (passwords, emails) clearly."*

**Hacking Use:** Hackers perform Sniffing or Man-in-the-Middle (MITM) attacks here because there is no lock on the data.

---

### Port 443 - HTTPS (HTTP Secure)

**What it does:** This is for modern websites (Facebook, Google, Banks). Data is Encrypted here. There is a lock icon with the URL.

**Hacker's Mindset:** *"This door is strong, the data is encrypted. I need to downgrade its security to Port 80 or send the user a fake certificate."*

**Hacking Use:** Hackers try SSL Stripping to bring the website from secure to unsecure.

---

### Port 21 - FTP (File Transfer Protocol)

**What it does:** This is used to upload and download large files, software, or movies over the network.

**Hacker's Mindset:** *"If this port is open, check if the admin has set a weak password like 'admin123'. If yes, I will steal all the server's files."*

**Hacking Use:** Hackers perform Brute Force Attack (trying passwords blindly) or if an old software version is running, they run a direct exploit.

---

### Port 22 - SSH (Secure Shell)

**What it does:** This is used to remotely control another computer or server (Terminal/Command line). It is fully secure and encrypted.

**Hacker's Mindset:** *"If I get access to Port 22, I will become the owner of that server. I will check if the server's software is up-to-date or if there is any old vulnerability."*

**Hacking Use:** Hackers focus heavily on this port because hacking it means full control of the system.

---

## Well-Known Ports vs Random Ports

When your laptop sends a request to a website (Port 80), your computer uses two ports:

1. **Destination Port (Target's Door):** This is always fixed, like 80 or 443 for websites. These are called Well-Known Ports (0 to 1023).
2. **Source Port (Your Own Door):** When your browser sends a request, it picks any random empty port between 1024 and 65535 (like Port 54321). This way, when the reply comes back, the router knows which computer and which tab to send the data to.

---

## Deep Attack Analysis: How Hacking Happens on Ports

When a hacker works on ports, they have 3 main stages in mind:

### 1. Banner Grabbing (Finding the Software's Identity)

The hacker doesn't just check if the port is open. They send a special packet to that open port to check what software and exact version is running behind it.

**Hacker's Vision:** Port 21 (FTP) is found open. Banner grabbing reveals that the software running is `vsftpd 2.3.4`. Elite hackers know that this specific old version has a known vulnerability (Exploit). The hacker doesn't need to find the password — they directly exploit the software's weakness to get in.

### 2. Service Enumeration (Understanding the Behavior)

The hacker checks how the protocol running on the port behaves. If Port 22 (SSH) is open, does it allow root user to log in directly? If Port 25 (SMTP - Email) is open, can I send fake emails without any login?

### 3. Port Redirection / Port Forwarding

The hacker hacks a small computer inside the company. But that computer is blocked from the outside world. The hacker creates a rule on that computer: "Whatever data comes on Port 443 (which is normally not blocked), secretly send it to my hacker server." The firewall thinks normal internet traffic is happening, but the hacker is secretly stealing data.

---

## Port States: Open, Closed, and Filtered

When we scan, ports show us 3 types of status. Each has a different meaning for a hacker:

**1. Open (Khala)**
The door is open and an application is waiting for requests. This is a green signal for the hacker.

**2. Closed (Band)**
The door is closed. The computer is not accepting requests there. But this tells the hacker that the machine is online.

**3. Filtered (Roka Hua)**
This is the biggest headache for a hacker. A firewall or security guard is blocking packets and dropping them before they reach the port.

---

## Defensive Mindset: How to Stay Safe

After understanding the hacker's mindset, how does a good security expert defend?

**Principle 1: Close Unused Ports**
Close all doors that are not in use. If the company doesn't need FTP, Port 21 should always be closed.

**Principle 2: Change Default Ports**
Change default ports to hide from automatic attacks. SSH's real door is Port 22. Hackers run automatic scripts attacking Port 22 on every computer. If we change SSH port from 22 to 52222, average hackers won't even know where the door is.

**Principle 3: Use Firewalls**
Use firewalls to set filtered state, allowing only specific (allowed) IPs to talk on those ports.

---

## Elite Hacker Scanning Strategy (Two-Step Method)

A hacker never runs a deep scan on all 65,535 ports at once. It takes too long and the firewall catches it.

**Step 1: The Quick Ping**
First, a fast scan to see which ports are open (without checking version). This scan is so fast that it can find all 65,535 ports in seconds or minutes.

**Step 2: The Deep Focus**
Now the hacker only checks the versions of the open ports. Since only a few ports are open, the deep version scan takes only 2-3 seconds.

**Stealth Scanning (Timing Mode):**
If the admin has a rule that blocks fast scanners, the hacker uses T1 or T2 (Sneaky/Polite Mode). This means the scanner waits a few seconds or minutes between checking each port. The firewall thinks this is a normal internet user browsing slowly.

---

## Hacker vs IDS/IPS (The Never-Ending Game)

**Defender's Move (IDS/IPS):**
IDS/IPS deeply inspects every packet on the network. If the same IP repeatedly knocks on different ports, the IDS detects it as a "Port Scanning Attack" and blocks it.

**Hacker's Counter (Decoy Scanning & Fragmentation):**

1. **Decoy Scan (-D Command):** The hacker tells Nmap to mix their IP with 5-10 famous IPs (like Google or Facebook) during the scan. The IDS sees 10 different IPs scanning simultaneously and gets confused about which one is the real hacker.

2. **Packet Fragmentation (-f Command):** The hacker breaks their scanning packets into tiny pieces (fragments). The IDS thinks these tiny pieces are normal network traffic and lets them through. When all the pieces reach the target computer, they reassemble and give the hacker a complete report.

---

## Challenge Exercise: Hacker Practice Task

**Scenario:** You scan a target server and find two ports open:
1. Port 80 (HTTP)
2. Port 443 (HTTPS)

If you want to steal a user's login password (via Sniffing), which port's traffic will you target where data is traveling without encryption or a lock?

---

**My Analysis:**
- I will target **Port 80 (HTTP)**.
- Because Port 80 has no encryption, data travels in plain text through the air or cable.
- If any user types their password there, I can see the exact words in my scan.
- Port 443 has encrypted data which is impossible to read.

---

## What I Messed Up Today

Today I learned that ports are like doors to a computer. I initially thought all ports were the same, but now I understand that different services run on different ports.

I also learned about the Two-Step scanning method. I used to think hackers scanned all 65,535 ports deeply at once, but that would take forever and alert firewalls. The elite way is to do a quick scan first, then only deeply scan the open ports.

I also realized that port security is a constant battle between hackers and defenders. Defenders close ports and change default numbers, while hackers use decoy scans and fragmentation to bypass detection.

The most important takeaway is that if a port is open, it's a potential entry point. But if a port is filtered, that means a firewall is sitting in front of it — which also tells us the target machine is alive and protected.
