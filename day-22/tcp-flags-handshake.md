# Day 22: TCP Three-Way Handshake & Flags — Stealth Scanning Fundamentals

Today I am learning about TCP Flags and how hackers use them for stealth scanning.

We learned before that TCP is a reliable protocol that does a Three-Way Handshake before sending data. Today we will look at the hidden Flags (Control Switches) inside it and understand how hackers use these flags to scan networks.

---

## What are TCP Flags? (The Control Buttons)

In the TCP packet header, there are small switches called Flags. They tell packets what their purpose is. For hacking and security, these 4 flags are the most important:

**1. SYN (Synchronize)**
Used to start a connection (to extend a friendship hand).

**2. ACK (Acknowledgment)**
Used to confirm receipt or give a reply (e.g., "I received your packet").

**3. RST (Reset)**
Used to abruptly close a connection if something goes wrong.

**4. FIN (Finish)**
Used to politely close a connection after work is done.

---

## The Real Handshake Process

When your computer connects to a server, these flags work together like this:

**Step 1 (You -> Server):** Your computer sends a packet with only the SYN flag turned ON.

**Step 2 (Server -> You):** The server accepts the friendship and sends back a packet with both SYN and ACK flags turned ON (SYN-ACK).

**Step 3 (You -> Server):** Your computer sends a final ACK flag. Connection established!

---

## The Hacker's Mindset vs. Defensive Operations

### 1. The Attack: Stealth (SYN) Port Scanning

**Hacker's Logic:** Hackers use this handshake to find open ports on a target computer (using Nmap tool). This is called SYN Scan or Half-Open Scan.

The hacker sends a SYN packet to the target port.

- **If Port is OPEN:** The server sends back SYN-ACK. Now the hacker knows the port is open! But the hacker is smart — instead of sending the third ACK packet, they send a RST (Reset) packet to break the half-open connection so no entry is logged in firewalls.

- **If Port is CLOSED:** The server sends back a RST packet saying "Bro, there is no space here, get lost!"

### 2. The Defense: Stateful Firewalls

**Defensive Action:** Defenders protect against these half-open connections (SYN Flood) by using Stateful Firewalls. These firewalls keep track of the complete handshake. If a device only sends SYN packets and doesn't complete the handshake, the firewall immediately Blocks that IP.

---

## SYN Scan vs SYN Flood (Important Difference)

| Feature | SYN Scan (Stealth Scan) | SYN Flood (DoS Attack) |
|---------|------------------------|------------------------|
| **Purpose** | Check if port is open or closed | Crash/Down the server |
| **Packet Count** | Very few packets | Thousands/millions of SYN packets |
| **Handshake** | Sends RST to close connection | Never completes handshake |
| **Visibility** | Stealthy, hard to detect | Creates huge traffic, easy to detect |

---

## MUST MEMORIZE

- **SYN:** Connection initialization flag.
- **SYN-ACK:** Server's positive response to connection.
- **RST:** Abrupt connection termination signal.
- **FIN:** Polite connection termination signal.
- **Stealth Scan:** Finding open ports with half-handshake without getting caught.

---

## Elite Challenge: Port Scan Analysis

**Scenario:** A hacker runs a SYN Scan on a bank's server on port 80 (HTTP) and port 22 (SSH).

- Port 80 returns a SYN-ACK packet.
- Port 22 returns a RST packet.

1. Which port is Open and which is Closed?
2. Why does the hacker send a RST instead of the third ACK packet when they find an open port?

---

**My Analysis:**

1. **Port 80 is Open** (SYN-ACK received) and **Port 22 is Closed** (RST received).

2. The hacker sends RST instead of ACK because they **don't want to establish a full connection**. If the handshake completes, logs are generated on the application layer and the firewall/system administrator could trace the hacker's IP. Sending RST makes the connection abort immediately, keeping the scan stealthy.

---

## What I Messed Up Today

Today I learned the critical difference between SYN Scan and SYN Flood:

- **SYN Scan** is for stealthily checking ports (few packets, RST to abort)
- **SYN Flood** is for crashing servers (thousands of SYN packets, never completing the handshake)

The key insight is that the hacker's goal in a SYN Scan is to **remain undetected**. By not completing the handshake, they avoid generating logs and triggering alarms.

The most important takeaway is that Stateful Firewalls track the state of connections and can detect incomplete handshakes, making them an effective defense against both SYN scans and SYN flood attacks.
