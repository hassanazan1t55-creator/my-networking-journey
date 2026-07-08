# Day 29: IP Spoofing & MAC Spoofing — Identity Manipulation on the Network

Today I am learning about IP Spoofing and MAC Spoofing, techniques hackers use to change their identity on the network.

In hacking and penetration testing, when a hacker sends a packet on the network, they don't want their real IP address or MAC address to be logged. So they change their identity inside the packet headers. This process is called Spoofing.

Let's understand MAC Spoofing (Layer 2) and IP Spoofing (Layer 3) — their packet-level logic and the key differences.

---

## MAC Spoofing (Layer 2 — Changing Local Address)

MAC address is the physical address of your network card (NIC).

**How It Works:** Modern operating systems (Windows/Linux) allow you to temporarily write a new MAC address into your Network Interface Card's (NIC) RAM/Driver.

**Network Impact:** When your computer talks to the switch on the Local Area Network (LAN), the switch saves your new spoofed MAC address in its CAM Table.

**Use Cases:**

1. **MAC Filtering Bypass:** If a Wi-Fi or Switch Port only allows specific MAC addresses, the hacker changes their MAC to match an allowed device's MAC.
2. **Anonymity:** On the local network, Wireshark captures won't reveal the hacker's real device manufacturer (e.g., Apple, Dell).

---

## IP Spoofing (Layer 3 — Changing Sender Address)

IP Spoofing happens when a hacker crafts a packet (using tools like Scapy) and changes the Source IP Address field in the IP header to someone else's IP address.

**How It Works:** The hacker sets `src_ip = "1.1.1.1"` and fires the packet at the target `dst_ip = "192.168.1.10"`.

**The Blind Reality (One-Way Problem):**

- The target computer reads the packet and thinks it came from `1.1.1.1`.
- When the target sends a response, the reply does NOT go back to the hacker. It goes to the real IP (`1.1.1.1`) that was spoofed!

**Use Cases:**

1. **DoS/DDoS Attacks:** SYN Flood or UDP Flood attacks where the target shouldn't know where the attack is coming from.
2. **Reflection/Amplification Attacks:** Setting the victim's IP as the target and sending requests to open servers (like DNS/NTP) so the heavy reply goes to the victim.

---

## How Routers Block IP Spoofing (Ingress/Egress Filtering)

Good routers don't forward spoofed packets. They use BGP RFC 2827 (Ingress Filtering).

**Logic:** If a router's Interface Eth0 is connected to IP range `192.168.1.0/24`, and a packet arrives on that interface with Source IP `8.8.8.8`, the router immediately knows the packet is fake (spoofed) and drops it.

---

## Summary Comparison

| Feature | MAC Spoofing | IP Spoofing |
|---------|--------------|-------------|
| **OSI Layer** | Layer 2 (Data Link) | Layer 3 (Network) |
| **Scope** | Only Local Network (LAN) | Internet / Cross-Network |
| **Traffic Return** | Two-Way (Reply comes back) | One-Way (Reply goes to fake IP) |
| **Main Usage** | Access Control bypass, MITM | DoS attacks, Amplification |

---

## MUST MEMORIZE

- **MAC Spoofing:** Layer 2 spoofing — Reply comes back (Two-Way).
- **IP Spoofing:** Layer 3 spoofing — Reply goes to the fake Source IP address (One-Way).
- **Ingress Filtering:** A firewall rule on routers that drops packets with fake Source IP addresses.

---

## Elite Challenge: SYN Flood with IP Spoofing

**Scenario:** A hacker sits on a local Wi-Fi network. There is a Stateful Firewall on the network. The hacker launches a TCP SYN Flood Attack using IP Spoofing, sending thousands of SYN packets to the target server from random fake IP addresses.

1. When the target server sends SYN-ACK replies to those thousands of fake IPs, what will happen to the target server's RAM / Memory?
2. Can the hacker steal (sniff) any sensitive data (like a file download) from the target server using this IP Spoofing attack? Explain why or why not.

---

**My Analysis:**

1. The server's RAM will overflow/crash/hang. For each fake IP, the server reserves space and waits for an ACK. Since the IPs are fake, ACK never arrives. Thousands of connections stay in "Half-Open" state, filling up the server's RAM. Normal users can no longer access the website (Denial of Service - DoS).

2. **NO**, the hacker cannot steal data. To download a file or sniff data, a complete TCP connection is required (SYN → SYN-ACK → ACK). Since the replies are going to the fake IP addresses, the hacker never receives any data. IP Spoofing is only useful for attacks and sabotage, not for data stealing!

---

## What I Messed Up Today

Today I learned the critical difference between MAC Spoofing and IP Spoofing:

- **MAC Spoofing:** Works on Layer 2 (Local Network). Replies come back to the hacker because the switch sees the spoofed MAC.
- **IP Spoofing:** Works on Layer 3 (Internet/Cross-Network). Replies go to the spoofed IP address, NOT the hacker. This makes it One-Way traffic.

The key insight is that IP Spoofing is primarily used for:
1. **DoS/DDoS Attacks** — crashing servers without being traced
2. **Amplification Attacks** — redirecting heavy responses to a victim

The most important takeaway is that IP Spoofing **cannot** be used for data theft because the hacker never receives the replies. It's purely an attack/sabotage technique.

**SYN Flood + IP Spoofing:** Fills the target server's RAM with Half-Open connections, causing it to crash.
**IP Spoofing Restriction:** Can never be used to sniff or steal data because replies don't come back (One-Way Traffic).
