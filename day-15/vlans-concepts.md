# Day 15: VLANs — Virtual Network Segmentation

Today I am learning about VLANs, which let us create multiple virtual networks on one single switch.

---

## What is a VLAN? (The Logic)

Imagine a big office where HR, Finance, and IT Engineers all sit on the same floor and all their computers are connected to one big switch.

**The Problem:** If it's a normal network, HR's computer can send data directly to Finance's computer. If a hacker hacks HR's computer, they can sit there and run nmap scans on the whole office (Finance, IT) and steal everyone's data.

**The Solution (VLAN):** Network engineers create virtual walls inside the switch using software. They tell the switch: "Ports 1 to 5 are only HR, Ports 6 to 10 are only Finance." This virtual partition is called VLAN.

Even though all computers are connected to the same switch, HR's computer cannot talk to Finance's computer unless a Router in between gives permission!

---

## Core VLAN Concepts (Must Memorize)

**1. VLAN ID**
Every VLAN has a number (like VLAN 10, VLAN 20). By default, all switch ports are in VLAN 1.

**2. Access Port**
This port connects directly to a single computer or laptop. It can only be part of one VLAN.

**3. Trunk Port**
This is a VIP port. When data needs to go from one switch to another switch, all VLANs (HR, Finance, IT) data travels through one single wire. That path is called Trunk Link.

---

## VLAN Tagging (802.1Q)

When HR and Finance data both travel together through the Trunk wire, the switch puts a small Tag (slip) on every packet (like "This packet belongs to VLAN 10"). When the packet reaches the other switch, it reads the tag and sends it to the right department. This protocol is called IEEE 802.1Q.

---

## The Hacker's Mindset vs. Defensive Operations

### 1. The Attack: VLAN Hopping

**Hacker's Logic:** If the company didn't tighten switch security, a hacker tricks the switch by presenting their laptop as a "Fake Switch" and changes an Access Port into a Trunk Port. Then the hacker jumps from one VLAN to another secure VLAN (like Finance) without any router.

**The Impact:** The hacker bypasses VLAN isolation and gains access to sensitive network segments.

### 2. The Defense: Unused Ports Disabled

**Defensive Action:** Defenders protect against VLAN Hopping by keeping all unused ports closed and disabled. They also configure switch ports explicitly as Access or Trunk, rather than leaving them in auto-negotiation mode.

---

## Elite Challenge: VLAN Isolation Test

**Scenario:** You are auditing a bank's network. The admin has placed the IT department in VLAN 10 and Cashier computers in VLAN 20. Both computers are connected to the same switch.

1. If you sit on the IT department computer and try to ping the Cashier computer directly, will the ping get a reply or will the packet be blocked?
2. If the admin wants the IT manager to be able to communicate with the Cashier computer (just for checking), what Layer 3 device needs to be placed above the switch to connect the different VLANs?

---

**My Analysis:**

1. The packet will be **blocked**. The virtual wall of VLANs is so strong that even though both computers are on the same switch, packets cannot cross VLAN boundaries without authorization.

2. A **Router** (Layer 3 device) is needed to connect different VLANs. This is called **Inter-VLAN Routing** or **Router-on-a-Stick**.

---

## What I Messed Up Today

Today I learned that VLANs are a powerful security tool for network segmentation. I initially thought that being on the same switch meant all devices could talk to each other, but VLANs change that completely.

The key concepts I need to remember:
- **VLAN ID** — the number that identifies each virtual network
- **Access Port** — connects to a single device in one VLAN
- **Trunk Port** — carries all VLANs between switches
- **802.1Q Tagging** — the label that identifies which VLAN a packet belongs to

I also learned about VLAN Hopping, where a hacker tricks an Access Port into becoming a Trunk Port to jump between VLANs. Defenders prevent this by disabling unused ports and hardcoding port configurations.

The most important takeaway is that VLANs provide isolation even on the same physical switch, and a Router is needed to allow communication between VLANs.
