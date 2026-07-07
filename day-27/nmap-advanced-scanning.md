# Day 27: Advanced Network Scanning — Nmap Stealth Scans & Packet Analysis

Today I am learning about advanced Nmap scanning techniques and their packet-level logic.

In hacking and penetration testing, network scanning is not just about finding ports — it's about reconnaissance without alerting the target's security mechanisms. Today we will look at three of Nmap's most stealthy scans using Wireshark packet-level analysis.

---

## TCP SYN Scan (-sS) — The Stealth Scan (Half-Open Scan)

This is the world's most famous and default scan. It's called Half-Open Scan because it never completes the TCP connection.

**Wireshark Packet Flow Logic:**

1. **Nmap (Hacker):** Sends a SYN packet to the target port.

2. **Target Port:**
   - If Port is **OPEN:** Target sends back SYN-ACK.
   - If Port is **CLOSED:** Target sends back RST (Reset).

3. **The Stealth Move:** As soon as Nmap receives SYN-ACK from the target, it knows the port is open. But instead of sending ACK to complete the connection, Nmap immediately fires a RST (Reset) packet!

**Advantage:** Because the TCP connection was never fully Established, the target server's application logs (like Apache or Nginx) do not register any record of this scan.

---

## TCP Null Scan (-sN) — Empty Packet Scan

This scan is designed to trick firewall rules.

**Wireshark Packet Flow Logic:**

Nmap sends a packet with NO flags set (All Flags = 0).

**RFC 793 (TCP Rules):** According to standard networking rules:
- If Port is **CLOSED:** The target is forced to reply with a RST packet.
- If Port is **OPEN:** The target will completely Ignore this weird packet (No Reply).

**Hacker's Conclusion:** If there is no reply, Nmap concludes the port is open (or the firewall filtered it).

---

## TCP Xmas Scan (-sX) — Christmas Tree Scan

This scan is called "Xmas" because all the flags light up inside the packet like Christmas tree lights.

**Wireshark Packet Flow Logic:**

Nmap sends a packet with FIN, PSH, and URG — all three flags turned ON simultaneously.

**The Target Reaction:** Like the Null scan, if the port is **CLOSED** it will send RST. If the port is **OPEN**, it will silently Ignore the packet (No Reply).

---

## TCP Flags Deep Dive (FIN, PSH, URG)

### 1. FIN (Finish Flag — Polite Goodbye)

**Purpose:** This flag is used when the data transfer between two computers is complete and both want to politely close the connection.

**Logic:** When you've finished downloading a file from a website, your computer sends a packet with the FIN flag ON. This means: "My work is done, let's close the connection."

### 2. PSH (Push Flag — Send Immediately)

**Purpose:** Normally, when data arrives at a computer, it is stored in a Buffer (Memory storage) first, and when the buffer is full, it is sent to the application (like browser). But the PSH flag bypasses this memory waiting-room.

**Logic:** If a packet has the PSH flag ON, the target computer's operating system immediately pushes the data directly to the application without storing it in the buffer.

**Where it's used:** Real-time applications like online gaming or chat applications, where data needs to arrive immediately and cannot wait.

### 3. URG (Urgent Flag — VIP Emergency)

**Purpose:** This flag tells the computer that the data in this packet is not normal data but very Urgent (VIP), so it should stop all other packets and process this one first!

**Logic:** When the URG flag is ON, another part of the TCP header called the Urgent Pointer becomes active. This pointer tells the computer which part of the packet to read first.

**Where it's used:** For example, if you're running a command in the terminal and it hangs, and you press Ctrl + C to stop it immediately, the computer sends a URG flag packet to terminate the hung command.

---

## Quick Packet Comparison Table

| Scan Type | Nmap Flag | Sent Packet Flags | Target Reply (If Port Open) | Target Reply (If Port Closed) |
|-----------|-----------|-------------------|----------------------------|-------------------------------|
| SYN Scan | -sS | SYN | SYN-ACK (Then Hacker sends RST) | RST |
| Null Scan | -sN | None (0) | No Reply | RST |
| Xmas Scan | -sX | FIN, PSH, URG | No Reply | RST |

---

## MUST MEMORIZE

- **SYN Scan (-sS):** Doesn't let connection complete. Sends RST immediately after receiving SYN-ACK to terminate the connection.
- **Null & Xmas Scans:** If port is OPEN, no reply comes. If CLOSED, RST comes.
- **Firewall Evasion:** Null and Xmas scans are used to bypass old stateful firewalls because they don't contain the SYN flag.

---

## Elite Challenge: Firewall Deception

**Scenario:** A hacker runs an Xmas Scan (-sX) on a corporate network. When they check Wireshark, they see zero reply packets coming back from the target IP. Nmap reports that all ports on the target are Open. But when the hacker tries to open the website, it doesn't load (meaning the ports are actually closed or filtered).

1. If there is a firewall on the route that silently Drops (Ignores) all unknown traffic without sending any reply, how does Nmap get tricked into thinking all ports are open?
2. After this firewall behavior, what will Nmap report the port status as — Open or Open|Filtered?

---

**My Analysis:**

1. Nmap gets tricked because the Xmas Scan rule is: **No Reply = Port Open**. When the firewall silently drops all packets without replying, Nmap assumes all ports are open.

2. Nmap will report the status as **Open|Filtered**. Nmap is smart enough to know that if it gets no reply, either the port is actually open and not replying, OR a firewall is dropping the packets.

---

## Why Did Nmap Use These Flags in Xmas Scan?

Nmap used FIN, PSH, and URG together in the Xmas scan because according to standard networking rules (RFC), when there is no established connection, you cannot directly send FIN (Goodbye) or URG (Urgent) packets to someone!

This is like going to a stranger on the street and saying "Goodbye" without even saying "Hello" first.

Because of this weird behavior, open ports get confused and ignore the packet, while closed ports follow the protocol and send RST.

---

## What I Messed Up Today

Today I learned the three advanced Nmap scans and their packet-level logic:

- **SYN Scan (-sS):** Half-open scan, sends RST after SYN-ACK to avoid logging
- **Null Scan (-sN):** All flags OFF, open ports ignore, closed ports send RST
- **Xmas Scan (-sX):** FIN, PSH, URG all ON, open ports ignore, closed ports send RST

I also learned the three new flags:
- **FIN:** Polite connection termination
- **PSH:** Push data immediately to application (no buffer)
- **URG:** Urgent data, VIP priority

The key insight is that these stealth scans exploit TCP protocol rules to determine port states without completing a full connection, making them harder to detect.
