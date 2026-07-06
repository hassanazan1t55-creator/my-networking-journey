# Day 10: DHCP (Dynamic Host Configuration Protocol) — Attacks and Defenses

Today I am learning about DHCP, which automatically assigns IP addresses to devices when they join a network. 

Imagine an enterprise environment where 1,000 employees connect their laptops to the Wi-Fi daily. If a network engineer manually assigned static IP addresses for everyone, it would be an impossible administrative nightmare. DHCP solves this problem by acts as an automatic server that leases out free IP addresses to any new device connecting to the network.

---

## How DHCP Works: The DORA Process

The DHCP operational lifecycle is broken down into a 4-step process known as **DORA**. When a mobile phone or laptop connects to Wi-Fi, these steps happen in microseconds:



1. **D - Discover:** The client device sends a network-wide broadcast packet: *"Hey, is there a DHCP server out there? I need an IP address!"*
2. **O - Offer:** The DHCP server responds with a unicast/broadcast packet: *"Yes, I am here. I have a free IP address `192.168.1.50`. Do you want it?"*
3. **R - Request:** The client replies back: *"Yes! I accept this IP address, please lock it for my MAC address."*
4. **A - Acknowledgment:** The DHCP server finalizes the deal: *"Confirmed! This IP is leased to you for the next 24 hours. Here are your Subnet Mask, Default Gateway, and DNS server details."*

* **The Hotel Room Analogy:** You check into a hotel (Network). The receptionist (DHCP Server) hands you a key to an empty room (IP Address). When your stay expires, you return the key, and that room becomes available for the next guest.
* **The Token System Analogy:** In a crowded bank, a machine prints out unique token numbers for every incoming person to prevent chaos and overlapping lines.

---

## The Hacker's Mindset vs. Defensive Operations

Since DHCP automatically handles IP distribution, it presents unique attack surfaces for hackers and critical security requirements for defenders.

### 1. The Attack: DHCP Starvation (Denial of Service)
* **Hacker's Logic:** A DHCP server operates on a finite pool of available IP addresses (e.g., 200 IPs). If I write a script to spoof thousands of fake MAC addresses and flood the server with fake DHCP Discover requests, the server will quickly exhaust its entire pool.
* **The Impact:** When legitimate users attempt to join the network, no IPs are left, causing a total Denial of Service (DoS). The hacker can then set up a **Rogue DHCP Server**. Any victim who receives an IP from this rogue server will have all their internet traffic routed through the hacker's machine (Man-in-the-Middle attack).

### 2. The Defense: DHCP Snooping
* **Defensive Action:** Network administrators configure a layer-2 switch feature called **DHCP Snooping**. 
* **The Logic:** The admin explicitly configures the physical switch port connected to the legitimate DHCP server as **Trusted**. All other user-facing ports are left as **Untrusted**. If an attacker attempts to connect a fake DHCP server to an untrusted port and starts broadcasting DHCP "Offers," the switch immediately drops those malicious packets.

---

## Hardening the Switch: Port Security & MAC Limiting

What if the hacker bypasses standard controls by rotating thousands of fake MAC addresses from a single network jack to trigger DHCP Starvation?

* **Defensive Action:** The defender enables **Port Security** (MAC Limiting) on all access ports.
* **The Logic:** The administrator sets a strict threshold: *"Only 1 or 2 unique MAC addresses are permitted to communicate through this specific switch port."*
* **The Impact:** The moment the hacker's script generates a 3rd unique MAC address from that port, the switch triggers a security violation and instantly forces the interface into a **Shutdown** state, kicking the attacker entirely offline.

---

## Elite Deep Challenge: The Rogue Race Condition

**Scenario:** You are targeting an enterprise environment where Port Security is strictly enforced on the switches, meaning you cannot flood the network with fake MAC addresses to exhaust the DHCP pool. However, during network reconnaissance, you discover that the legitimate DHCP server is slow—taking 3 to 4 seconds to reply to a "Discover" packet.

If you launch an unofficial, optimized Rogue DHCP server on the network that responds in microseconds, can you still intercept user traffic without starving the real server?

### My Analysis and Solution:
* **Yes, absolutely.** According to the core mechanics of the DORA process, a client device will automatically accept whichever DHCP "Offer" reaches it **first**.
* Since the rogue server responds in microseconds and the real server takes seconds, the rogue server will consistently win the race condition.
* The client will bind to the rogue IP configuration, allowing the attacker to seamlessly execute a Man-in-the-Middle (MitM) attack without shutting down the main server.

---

## Advanced Protection: Authoritative DHCP

How do defenders completely shut down this race condition?

* **Authoritative Configuration:** The main enterprise DHCP server is explicitly flagged as **Authoritative**. If it catches another unofficial server distributing invalid IP configurations on its subnet, the authoritative server actively transmits a `DHCPNAK` (Negative Acknowledgment) packet to force the client to drop the rogue lease.
* **Enterprise Snooping:** Ultimately, combining Authoritative settings with strict **DHCP Snooping** on the switching fabric remains the bulletproof standard for blocking unauthorized network layer configurations.

---

## What I Messed Up Today

Today I solidified my understanding of the 4-step DORA lifecycle. Initially, I assumed DHCP was a simple, unstructured query, but analyzing the packet sequence showed me exactly how client-server handshakes take place.

I also made mistakes initially regarding how rogue servers operate. I assumed you *had* to crash the real server to intercept traffic. Learning about the "race condition" dynamic where a faster response wins the client's configuration was a massive eye-opener. 

This lesson proved that DHCP is an entire security ecosystem. Understanding how DHCP Starvation and Spoofing function highlights exactly why mitigation tools like DHCP Snooping and Port Security are mandatory configurations in enterprise security architectures.
