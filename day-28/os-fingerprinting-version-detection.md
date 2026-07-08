# Day 28: OS Fingerprinting & Version Detection — Nmap's Reconnaissance Techniques

Today I am learning how Nmap identifies operating systems and software versions without ever entering the target system.

We often see that when we run `nmap -O` (OS Detection) or `-sV` (Version Detection), Nmap clearly tells us whether the target is running Windows 10 or Ubuntu Linux, and what exact version of software (like Apache, SSH) is running.

The question is: how does Nmap extract this secret information from outside without ever entering the system? Let's understand the packet-level magic.

---

## OS Fingerprinting (-O) — Target's TCP/IP DNA Test

Every operating system (Windows, Linux, macOS, iOS) has slight differences in how they build their standard TCP/IP stacks (the way they create packets).

Nmap sends 9 different custom packets to the target (some are valid, some are intentionally malformed with weird flags). When the target replies, Nmap analyzes these 3 things in the reply:

**TTL (Time to Live):** Different OS use different default TTL values. As packets pass through routers, TTL decreases.

- Linux/Android: Default TTL is mostly **64**
- Windows: Default TTL is mostly **128**
- Cisco/Network Devices: Default TTL is mostly **255**

**Window Size:** The Window Size field in the TCP header is set using different mathematical logic by each operating system.

**DF (Don't Fragment) Bit:** Some OS put DF bit = 1 on every packet by default, others put DF bit = 0.

**The Logic:** Nmap has a large database file (`nmap-os-db`). It matches the TTL, Window Size, and Flags from the target's reply against this database and says: "Aha! This reaction can only be from Windows 10!"

---

## Nmap's 9 Fingerprinting Packets (The Complete Set)

When Nmap runs `-O`, it sends these specific packets to test the target's TCP/IP stack under different situations:

### 1. TSeq (Sequence Generation Packets — 6 Packets)

First, Nmap sends 6 separate TCP SYN packets to any OPEN port on the target.

**Purpose:** Nmap checks how random the TCP Sequence Numbers are in the replies.

**Logic:** Windows generates sequence numbers using a different mathematical formula than Linux. This reveals the OS's stability and pattern.

### 2. T2, T3, T4 (The Open Port Probes — 3 Packets)

These three packets are also sent to an OPEN port, but they have weird shapes:

- **T2 (The Null Packet):** No flags are set (All flags = 0) with standard options.
- **T3 (The Chaos Packet):** SYN, FIN, PSH, and URG all flags turned ON together (even weirder than Xmas).
- **T4 (The Fake ACK):** Only the ACK flag is ON, but Nmap changes options that normal computers don't change.

### 3. T5, T6, T7 (The Closed Port Probes — 3 Packets)

These three packets are sent to a CLOSED port on the target:

- **T5:** A standard SYN packet on a closed port. Normally a closed port sends RST, but Nmap checks the data structure inside that RST packet.
- **T6:** An ACK packet on a closed port.
- **T7:** A FIN, PSH, URG (Xmas) packet on a closed port.

### 4. U1 (The UDP Probe — 1 Packet)

Nmap doesn't just rely on TCP. It sends a random data packet to a closed UDP port.

**Logic:** When a packet hits a closed UDP port, the OS sends back an ICMP Port Unreachable error message. Nmap checks the TTL and IP header inside that error message.

---

## Version Detection (-sV) — Probing & Banner Grabbing

When Nmap finds an open port (e.g., Port 80 is open), it uses two methods to figure out what software is running:

### A. Banner Grabbing (Polite Asking)

Nmap makes a simple connection to the target port. Many softwares (like SSH or FTP servers) automatically send their introduction (Banner) when a connection is made.

**Example:** Connecting to Port 22 immediately replies with: `SSH-2.0-OpenSSH_8.2p1 Ubuntu 4ubuntu0.5`. Nmap reads this and knows the software is OpenSSH.

### B. Probing (Poking)

If the software doesn't say anything (like many modern web servers hide their banners), Nmap has a file called `nmap-service-probes`. Nmap sends different commands (Probes) to the software. When the software sends back unique replies or error messages, Nmap recognizes the pattern and extracts the exact version.

---

## MUST MEMORIZE

- **OS Fingerprinting (-O):** Matching the target's TCP/IP stack behaviors (TTL, Window Size) to identify the OS.
- **Default TTLs:** Linux = 64, Windows = 128 (Always remember these!)
- **Version Detection (-sV):** Finding the exact software version through Banner Grabbing and Probes.

---

## Elite Challenge: OS Fingerprint Spoofing

**Scenario:** A clever network admin modifies their Linux web server's (TTL = 64) registry files and changes the default TTL to 128 (which is Windows' default).

A hacker runs `nmap -O <target-ip>` on the server.

1. At first glance, what deception will Nmap face regarding the operating system?
2. If Nmap correctly matches the advanced responses from the other 8 packets (like Window Size and TCP Options), will the admin's TTL change completely fool Nmap or will it still detect the truth?

---

**My Analysis:**

1. At first glance, Nmap will see TTL = 128 and might think the target is running Windows.

2. However, Nmap is not easily fooled. When it checks the other TCP Options (like Window Size, SackOK, Maximum Segment Size) and their unique combinations, Nmap's database will catch the error: "The TTL is Windows, but the rest of the behavior is Linux!"

**Result:** Nmap will either report Linux with 90% accuracy, or show both OS names with percentages (e.g., Linux 95%, Windows 5%). This technique is called **OS Fingerprint Spoofing**, but advanced scanners can easily bypass it.

---

## What I Messed Up Today

Today I learned the complete mechanism behind Nmap's OS Fingerprinting and Version Detection:

- **OS Fingerprinting** works by analyzing 9 different probes that test the TCP/IP stack's unique behaviors (TTL, Window Size, Sequence Numbers, etc.)
- **Version Detection** works through Banner Grabbing (polite asking) and Probing (sending commands to trigger unique error messages)

The key insight is that Nmap doesn't just send one packet — it sends a whole set of weird packets to test how the target's OS reacts under different conditions.

The most important takeaway is that while an admin can spoof TTL values, the combination of all 9 tests makes it nearly impossible to completely fool Nmap's OS detection.
