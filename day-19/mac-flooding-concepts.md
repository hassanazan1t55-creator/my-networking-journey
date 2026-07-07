# Day 19: MAC Flooding — CAM Table Overflow Attack

Today I am learning about MAC Flooding, which is an attack that fills up a switch's memory and breaks it.

Until now we learned that a switch keeps a list in its brain called the MAC Table or CAM Table. This table stores: "Port 1 has laptop A, Port 2 has laptop B."

But a switch is a physical hardware device, meaning its memory (CAM Table) has a limited size. It can only store a few thousand MAC addresses at a time.

---

## The Hacker's Mindset vs. Defensive Operations

### 1. The Attack: MAC Flooding (The Overload)

**Hacker's Logic:** The hacker takes advantage of this memory weakness in the switch. They run an automatic script from their laptop that creates thousands of fake MAC addresses every millisecond and throws them at the switch.

The switch thinks new computers are continuously joining the network. It starts writing all those fake MAC addresses into its list (CAM Table).

**The Impact:** Within just a few seconds, the switch's brain (CAM Table) becomes completely FULL, and there is no space left to store the real computers' MAC addresses!

### 2. The Result: Hub Mode (Fail-Open)

When the switch's memory is completely full, it goes crazy and stops working like a normal Switch. It becomes a Hub!

**What is Hub Mode?** Now if Computer A sends data to Computer B, the switch doesn't know where Computer B is because its memory is full. So it throws (Broadcasts) that data packet to EVERY port on the network!

The hacker sits quietly on their port and captures all that data!

---

### 3. The Defense: Port Security (The Guard)

**Defensive Action:** Defenders protect against this disaster by turning on a feature on switch ports called Port Security.

The admin sets a limit on every switch port: "Only ONE (1) MAC address can be learned on this port at a time."

When the hacker sends thousands of fake MAC addresses from that port, the switch immediately recognizes the limit has been crossed. The switch Auto-Shuts Down (Disables) that port due to security violation and the hacker's connection is cut!

---

## ARP Spoofing vs MAC Flooding (The Difference)

| Feature | ARP Spoofing | MAC Flooding |
|---------|--------------|--------------|
| **How it Works** | Hacker lies to devices (Spoofing) | Hacker fills switch memory (Flooding) |
| **Switch State** | Switch still works normally | Switch breaks and becomes Hub |
| **Hacker Position** | Hacker is Man-in-the-Middle | Hacker captures all broadcasted traffic |
| **Defense** | DAI (Dynamic ARP Inspection) | Port Security |

---

## MUST MEMORIZE

- **CAM/MAC Table:** The switch's memory where port and MAC address records are stored.
- **MAC Flooding:** Filling the switch's memory with fake MAC addresses so it starts broadcasting traffic to everyone (Fail-Open/Hub Mode).
- **Port Security:** The switch feature that sets a limit on maximum allowed MAC addresses per port.
- **Fail-Open/Hub Mode:** When MAC Flooding fills the CAM Table, the switch stops being secure and starts broadcasting data to all ports like a normal Hub.

---

## Elite Challenge: Hub Mode Analysis

**Scenario:** A hacker starts a MAC Flooding attack on a bank's switch and fills its memory. The switch has now entered "Hub Mode" and is broadcasting all traffic to every port.

1. Since the switch is now in Hub Mode, does the hacker need to perform ARP Spoofing to steal traffic, or will the data come directly to them?
2. If the company has Port Security enabled with a limit of "1 MAC" per port, what will the switch do as soon as the hacker sends fake packets?

---

**My Analysis:**

1. The hacker **does NOT need ARP Spoofing**. Since the switch is now acting as a Hub, it broadcasts all data to every port, and the data automatically reaches the hacker.

2. The switch will immediately **shut down the port** due to security violation. Port Security detects the excessive MAC addresses and cuts the hacker's connection.

---

## What I Messed Up Today

Today I learned the critical difference between ARP Spoofing and MAC Flooding:

- **ARP Spoofing** is about lying to devices (sending fake ARP replies)
- **MAC Flooding** is about overwhelming the switch's memory (sending fake MAC addresses)

The key insight is that when a switch enters Hub Mode (Fail-Open), it becomes completely insecure because it broadcasts all traffic to every port. This is actually more dangerous than ARP Spoofing because the hacker doesn't need to do any additional work to intercept traffic.

The most important takeaway is that **Port Security** is the best defense against MAC Flooding. By limiting the number of MAC addresses per port, the switch can detect and block flooding attempts immediately.

I also learned that this attack targets the switch itself, not the devices on the network, making it a different type of attack from ARP Spoofing.
