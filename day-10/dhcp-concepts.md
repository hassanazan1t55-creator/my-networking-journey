# Day 10: DHCP — Automated IP Management

Today I am learning about DHCP, which automatically assigns IP addresses to devices when they join a network.

Imagine a big company where 1,000 people come daily and connect their laptops to Wi-Fi. If a network engineer manually typed IP addresses for everyone, their whole life would be wasted!

DHCP solves this problem. It is an automatic server that gives a free IP address (Lease) to any new device that connects to the network.

---

## The DORA Process: How IPs Are Assigned

In networking, the DHCP working process is called DORA. When your mobile connects to Wi-Fi, these 4 steps happen in seconds:

**D - Discover (Dhoondna)**
Your mobile sends a broadcast packet: "Hey, is there a DHCP server on this network? I need an IP address!"

**O - Offer (Peshkash)**
The DHCP server responds: "Yes, I have a free IP 192.168.1.50. Do you want it?"

**R - Request (Guzarish)**
Your mobile says: "Yes! I like this IP, lock it for me."

**A - Acknowledgment (Pakka Waada)**
The DHCP server says: "Okay, this IP is yours for the next 24 hours. Here is the Subnet Mask and Gateway address too."

- **Hotel Room Keys Analogy:** You go to a hotel (Network). The receptionist (DHCP Server) gives you a key to an empty room (IP Address). When your stay ends, you return the key and the room goes to someone else.
- **Token System Analogy:** In a big bank, there is a machine outside that gives every new person a token number so there is no confusion.

---

## The Hacker's Mindset vs. Defensive Operations

If there is an automatic IP assigning server on the network, how will a hacker exploit it and how will a defender protect it?

### 1. The Attack: Resource Exhaustion (DHCP Starvation)

**Hacker's Logic:** The hacker thinks: "This DHCP server has limited IPs (let's say 200 IPs). If I send thousands of fake requests with fake MAC addresses, the server will give all its IPs to me and there will be none left for normal users!"

**The Impact:** When real users come, they will get no IP and their internet will stop (Denial of Service - DoS). Then the hacker sets up a fake DHCP server (Rogue DHCP), and any user who gets an IP from the hacker's server will have all their data pass through the hacker's computer!

### 2. The Defense: Port-Level Access Control (DHCP Snooping)

**Defensive Action:** The switch has a special feature called DHCP Snooping. The defender marks the port where the real DHCP server is connected as Trusted. If a hacker tries to run a fake DHCP server from any other port, the switch will block (drop) those packets immediately!

---

## Additional Defense: MAC Limiting / Port Security

What if the hacker keeps changing MAC addresses to do DHCP Starvation?

**Defensive Action:** The admin sets a rule on every switch port: "Only 1 or 2 unique MAC addresses can connect from this port at a time."

**The Impact:** As soon as the hacker sends a 3rd fake MAC address to request an IP, the switch immediately realizes something is wrong and shuts down (Shutdown) that port. The hacker's laptop is kicked off the network!

---

## Elite Challenge: The Rogue Race Condition

**Scenario:** You are inside a company where Port Security is enabled on the switch (so you cannot send thousands of fake MAC addresses from one port, otherwise the port will shut down). This means you cannot do a DHCP Starvation attack to take down the real server.

But you discover that the real DHCP server is running a bit slow — when a new user sends a "Discover" packet, the real server takes 3-4 seconds to respond.

**Hacker's Logic:** Since I cannot take down the real server, but my fake DHCP server is very fast (responding in microseconds), can I still give fake IPs to normal users without doing a starvation attack? According to the DORA process, the user accepts whoever sends the first "Offer".

**The Impact:** Yes! Since my fake DHCP server responds in microseconds and the real server takes 3-4 seconds, my fake server will always send the first "Offer". The user's device will accept my fake IP without hesitation. All their data will now pass through my laptop. This is called **DHCP Spoofing** or **Rogue DHCP Attack**.

---

## Defender's Countermeasures: Authoritative DHCP & STP Guard

**Defensive Action:** The administrator can set the main DHCP server as Authoritative in Active Directory. This means if any other unofficial DHCP server tries to give out IPs, the real server sends a "Decline" packet across the network to cancel those fake IPs.

**Additional Protection:** As we learned earlier, blocking ports on switches (STP Root Guard & Snooping) is the most important and solid solution to prevent any "Offer" from unauthorized ports.

---

## Challenge Exercise: Security Analysis

**Scenario:** You are sitting in a coffee shop. Their DHCP server is working fine. But you want all the users' data to pass through your laptop instead of going directly to the router. So you turn on a fake DHCP server on your laptop.

1. If the coffee shop's switch has DHCP Snooping enabled, will your fake server be able to give fake IPs to users?
2. For a Starvation attack, what do you need to change repeatedly on your laptop when sending requests? (What does the DHCP server look at to decide if it's a new device?)

---

**My Analysis:**

1. No, it will not work. If DHCP Snooping is enabled, the switch will mark my port as untrusted and block my fake DHCP server's packets.

2. I need to change the **MAC address** every time. The DHCP server looks at the MAC address to identify if it's a new device. By sending thousands of fake MAC addresses, I can exhaust all the IPs.

---

## What I Messed Up Today

Today I learned the DORA process properly. I initially thought DHCP just gave out IPs randomly, but now I understand it's a 4-step process.

I also learned about DHCP Starvation and DHCP Spoofing attacks. The key insight is that if the real DHCP server is slow, the hacker's fake server can win the race and give out fake IPs.

The most important lesson is that DHCP is not just about assigning IPs — it's a whole ecosystem with attacks and defenses. Defenders use DHCP Snooping, Port Security, and Authoritative DHCP to protect against rogue servers.
