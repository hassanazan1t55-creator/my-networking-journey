# Day 14: Firewalls & IDPS — Network Security Infrastructure

Today I am learning about Firewalls and IDPS, which are the real security guards of any network.

Imagine a big VIP event is happening (your network), and thousands of people are standing outside trying to get in. If there is no guard outside, any thief or enemy can enter. In networking, Firewalls and IDPS do this guard work.

---

## What is a Firewall? (The Gatekeeper)

A firewall is a security device (or software) that stands like a wall between your safe internal network and the unsafe outside internet world.

Its job is to check every incoming and outgoing packet and allow or block them according to Rules.

---

## Two Main Types of Firewalls

### 1. Packet Filtering Firewall (Stateless)

**Defensive Action:** This is an old and basic firewall. It only looks at the packet's "face" — Source IP, Destination IP, and Port Number. If the rule says "Port 23 is blocked", it throws away the packet without thinking. It does NOT check the inside data of the packet.

### 2. Stateful Inspection Firewall

**Defensive Action:** This is advanced and smarter. It doesn't just look at the face, it keeps track (state) of the whole Connection. If you opened google.com from your browser, it knows this request came from inside, so the returning data is safe. If someone from outside suddenly tries to enter without a request, it will block them.

---

## IDPS — Intrusion Detection and Prevention Systems

Firewall only checks at the door. But if a thief changes identity (like MAC Spoofing) and enters through the door, what happens inside? Inside we need CCTV cameras and Alarms — this is IDPS.

**IDS (Intrusion Detection System)**
This is the network's CCTV Camera. It only monitors traffic and when it sees suspicious activity (like continuous nmap scan or brute force attack), it sends an Alert (warning) to the admin. It does NOT stop the attack itself, only tells about it.

**IPS (Intrusion Prevention System)**
This is the network's Active Commando. It not only sends alerts, but when it sees an attack, it Auto-Blocks (drops) that traffic and cuts the hacker's connection.

---

## The Hacker's Mindset vs. Defensive Operations

### 1. The Attack: Firewall Evasion via Fragmentation

**Hacker's Logic:** When a hacker sees a firewall in front, they don't attack directly. They break their attack packets into very small pieces (fragments). When these small pieces pass through the firewall, basic firewalls can't recognize them and let them through as normal traffic. Once inside, these pieces rejoin on the target computer and the attack executes!

**Nmap Switch:** Hackers use `-f` switch in Nmap for this (Packet Fragmentation).

### 2. The Defense: Deep Packet Inspection (DPI)

**Defensive Action:** Defenders use Next-Generation Firewalls (NGFW) to protect against this. DPI doesn't just look at the packet header or port. It opens the packet completely and scans the inside data (payload) too. Even if the hacker fragments the packets, NGFW first rejoins them, checks them, and then lets them through.

---

## MUST MEMORIZE

- **Stateless Firewall:** Only checks IP and Port, doesn't remember connection history.
- **Stateful Firewall:** Remembers connection history and state.
- **IDS vs IPS:** IDS only finds and alerts (Passive), IPS finds AND blocks (Active).
- **Nmap Flag -f:** Used to fragment packets for bypass.

---

## Elite Challenge: The Source Port Trick

**Scenario:** You are performing a security audit on a website. Behind the website is an old Packet Filtering Firewall with the rule: "Port 80 (HTTP) is open so people can view the website, but Port 22 (SSH Remote Access) is blocked."

1. If you send a direct attack on Port 22, will the firewall let it through?
2. If you change your attack tool's Source Port to 80 (making the firewall think it's normal website traffic) but keep the target port as 22, can this basic packet filtering firewall be tricked?

---

**My Analysis:**

1. No, the firewall will block it because Port 22 is explicitly blocked.
2. Yes! The basic packet filtering firewall only checks the header rules. When I change the source port to 80, it gets tricked. This is why the industry has shifted to Stateful and Next-Generation Firewalls.

---

## What I Messed Up Today

Today I learned the difference between Stateless and Stateful firewalls. The key insight is that Stateless firewalls only check packet headers (IP, Port), while Stateful firewalls track the entire connection state.

I also learned about IDS vs IPS:
- IDS is passive — it detects and alerts
- IPS is active — it detects and blocks

The most important lesson is that attackers use fragmentation (`-f` in Nmap) to bypass basic firewalls, and defenders use Deep Packet Inspection to counter this by reassembling and checking all fragments.

The Source Port trick taught me that basic firewalls are vulnerable because they only check destination ports, not the connection context. This is why Stateful and Next-Gen firewalls are essential.
