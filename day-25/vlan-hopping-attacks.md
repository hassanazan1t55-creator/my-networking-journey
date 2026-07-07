# Day 25: VLAN Hopping Attacks — Cross-Segment Exploitation

Today I am learning about VLAN Hopping attacks, where hackers jump from one VLAN to another.

On Day 15 we learned that VLANs (Virtual LANs) are used to create hidden and isolated networks (like HR, Finance, IT) inside one physical switch, so traffic from one network cannot go to another.

But, if there is a loophole in the switch configuration, a hacker can jump from their assigned VLAN to another sensitive VLAN without authorization. This attack is called VLAN Hopping.

There are two most important methods for this:

---

## Switch Spoofing (Tricking to Become Trunk Port)

Switch ports are of two types:

**Access Port:** For normal computers (Carries traffic of only ONE VLAN).

**Trunk Port:** Connects two switches together (Carries ALL VLANs traffic together).

**The Loophole:** Cisco switches have a protocol called DTP (Dynamic Trunking Protocol). Its job is to automatically negotiate and make ports "Trunk" ports.

**Attack Mechanism:** The hacker connects their laptop to an access port on the switch and crafts DTP packets to tell the switch: "I am not a computer, I am another Switch, create a Trunk link with me!"

If the switch port is on auto-negotiate mode, it gets tricked and turns that port into a Trunk Port. As soon as the port becomes trunk, the hacker starts receiving traffic from ALL VLANs directly!

---

## Double Tagging (Double Envelope Attack)

This attack happens when the hacker is on the switch's default or native VLAN (mostly VLAN 1). It takes advantage of a weakness in trunk ports.

**The Logic:** When a switch's trunk port sends a packet from its Native VLAN, it does NOT put any VLAN tag (envelope) on it.

**Attack Mechanism:** The hacker creates a packet with TWO Tags (Double Envelopes):

**1. Outer Tag (Outside envelope):** Native VLAN (e.g., VLAN 1).

**2. Inner Tag (Inside envelope):** Target VLAN (e.g., Finance - VLAN 10).

**The Process:** When the first switch sees this packet, it reads the outer tag (VLAN 1), removes it (strips it), and sends the packet on the trunk link.

When the second switch receives the packet, it only sees the inner tag (VLAN 10). It thinks this packet was meant for VLAN 10, and sends it directly to the Finance department computers!

**Important:** This attack is ONE-WAY only!

The hacker can SEND packets into VLAN 10, but they CANNOT RECEIVE replies from VLAN 10 because the hacker's port is not on VLAN 10, and they can't add double tags to the reply.

---

## Defensive Countermeasures

Big companies follow these two golden rules to prevent VLAN Hopping:

**1. Disable DTP on all ports:** Use `switchport nonegotiate` so no one can pretend to be a switch.

**2. Change Native VLAN:** Change Native VLAN to an unused VLAN ID (e.g., VLAN 999) and never put normal users in it.

---

## Switch Spoofing vs Double Tagging (Quick Comparison)

| Feature | Switch Spoofing | Double Tagging |
|---------|-----------------|----------------|
| **Port Changes?** | Port becomes TRUNK | Port stays ACCESS |
| **Traffic Flow** | Two-Way | One-Way |
| **What Hacker Gets** | All VLANs traffic | Can SEND into other VLANs, but CANNOT receive replies |

---

## MUST MEMORIZE

- **Switch Spoofing:** Using DTP protocol to turn a normal port into a Trunk Port.
- **Double Tagging:** Using Native VLAN weakness to put two tags on a packet so the switch strips the outer tag and the packet enters the target VLAN.
- **DTP (Dynamic Trunking Protocol):** System that automatically negotiates trunking between switches.
- **One-Way Attack:** Double Tagging is one-way because the hacker cannot receive replies from the target VLAN.

---

## Elite Challenge: The One-Way Reality

**Scenario:** A hacker launches a Double Tagging attack on a bank's network. They put the outer tag as VLAN 1 (the native VLAN) and the inner tag as VLAN 5 (the target investment sector). The hacker sends the packet. The target sector (VLAN 5) computer receives the packet successfully and the attack executes.

1. When the target computer (VLAN 5) tries to send a reply back to the hacker, will the reply packet reach the hacker through Double Tagging?
2. Why is Double Tagging called a "One-Way Attack"?

---

**My Analysis:**

1. **No**, the reply will not reach the hacker. The target computer's operating system cannot create double-tagged packets. It only creates standard single-tagged packets.

2. Double Tagging is called a **One-Way Attack** because the hacker can only send packets into the target VLAN, but cannot receive any replies. This makes it useful only for blind attacks (like Denial of Service or executing commands) where the hacker doesn't need to see the response.

---

## What I Messed Up Today

Today I learned the critical difference between Switch Spoofing and Double Tagging:

- **Switch Spoofing:** The port becomes a Trunk Port, allowing TWO-WAY traffic. The hacker can send and receive data from all VLANs.
- **Double Tagging:** The port stays as an Access Port. The hacker can only SEND packets (ONE-WAY) into other VLANs, but cannot receive replies.

The key insight is that Double Tagging exploits the Native VLAN behavior where switches strip outer tags. But since the hacker's port is not on the target VLAN, replies cannot come back.

The most important takeaway is that defenders must **disable DTP** and **change the Native VLAN** to prevent both types of VLAN Hopping attacks.
