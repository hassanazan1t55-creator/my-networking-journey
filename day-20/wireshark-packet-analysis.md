# Day 20: Wireshark & Packet Analysis — The Network X-Ray Machine

Today I am learning about Wireshark, which is like an X-Ray machine for the network.

Until now we learned many protocols (IP, MAC, ARP, DNS, NAT) — they all run in the background as packets through wires or air. Normal people can't see these packets.

But a cyber security expert or hacker has a superpower called Packet Sniffing, and the most famous tool for this is Wireshark!

---

## What is Wireshark?

Wireshark is basically the network's X-Ray Machine or Microscope.

**How it Works:** When you turn it on your computer, your network card (NIC) captures all packets passing through it (whether it's YouTube data, Facebook requests, or a hacker's attack). Wireshark catches all those packets from the air and opens them on your screen.

You can go inside every packet and see: what is its Source IP, Destination IP, which Port is being used, and what data is written inside.

---

## The Hacker's Mindset vs. Defensive Operations

### 1. The Attack: Packet Sniffing

**Hacker's Logic:** Imagine a hacker has redirected all network traffic to their laptop using attacks we learned (ARP Spoofing or MAC Flooding). Now what do they do?

The hacker turns on Wireshark. Now any normal user's data on the network appears live on the hacker's screen.

**HTTP vs HTTPS Difference (Live Proof):**

- If someone uses an old website (HTTP) and types their username and password, Wireshark catches that packet and the hacker sees the password in "Plain Text" (clear words) on the screen (like: password123).

- But if the same person uses HTTPS, the hacker only sees garbage (encrypted characters) in Wireshark, which is impossible to open.

### 2. The Defense: Malicious Traffic Detection

**Defensive Action:** Defenders use Wireshark to catch attacks happening on the network:

**Catching ARP Spoofing:** If ARP Spoofing is happening on the network, Wireshark will suddenly show two different MAC addresses for the same IP. Wireshark gives a warning (Alert) there.

**Catching Ping Flood:** If someone is attacking with ICMP, Wireshark will show thousands of ICMP (Ping) packets in a single second, making the admin realize an attack is happening.

---

## MUST MEMORIZE

- **Wireshark:** The biggest tool for capturing and analyzing network traffic.
- **Packet Sniffing:** Secretly capturing and reading data packets passing through the network.
- **Promiscuous Mode:** A special setting on the network card that, when turned on, makes the card capture not just its own traffic but ALL traffic on the network.

---

## HTTP vs HTTPS in Wireshark

| Feature | HTTP (Unsecure) | HTTPS (Secure) |
|---------|-----------------|----------------|
| **Data Format** | Plain Text | Encrypted |
| **Passwords Visible?** | Yes, clearly visible | No, only garbage/encrypted data |
| **Hacker Can Read?** | Yes, everything | No, nothing readable |

---

## Elite Challenge: Attack Detection

**Scenario:** You turn on Wireshark on your laptop and notice that on your network, some device is continuously sending thousands of fake ARP replies every millisecond, claiming "The router's MAC address is my MAC address".

1. What type of attack is this?
2. If the victim enters their password on `https://www.google.com` during this attack, will you see the actual password in Wireshark or only encrypted garbage?

---

**My Analysis:**

1. This is an **ARP Spoofing** attack. The hacker is poisoning the ARP cache to redirect traffic through their device.

2. I will only see **encrypted garbage**. HTTPS encryption protects the password even if the traffic is intercepted.

---

## What I Messed Up Today

Today I learned that Wireshark is both a hacker's tool and a defender's tool:

- **Hackers** use it to capture and read traffic (especially HTTP plain text passwords)
- **Defenders** use it to detect attacks (ARP Spoofing, Ping Floods, etc.)

The key insight is that **Promiscuous Mode** is what makes Wireshark powerful. Without it, the network card would only capture traffic meant for itself.

I also learned the critical difference between HTTP and HTTPS in Wireshark:
- **HTTP** shows everything in clear text (passwords, usernames, data)
- **HTTPS** shows encrypted garbage that is unreadable

The most important takeaway is that Wireshark is an essential tool for any security professional, but it also highlights why encryption (HTTPS) is so important.
