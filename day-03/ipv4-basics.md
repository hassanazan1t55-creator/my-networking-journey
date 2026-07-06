# Day 3: IPv4 Architecture and IP Classes

Today I am learning how IP addresses actually work and how computers are grouped into different networks.

Every computer on the internet has a unique identity called an IP address.

---

## The 32-Bit Structure of IPv4

When we see an IP like `192.168.1.1`, the computer sees a long chain of 32 bits (0 and 1).

- **Total Bits:** IPv4 has exactly 32 bits.
- **4 Octets:** These 32 bits are divided into 4 equal parts. Each part has 8 bits.
- **Dots (.):** Dots are used to separate these four octets so humans can read it easily.

**Example:**
IP Address: `192.168.1.5`
Computer sees: `11000000 . 10101000 . 00000001 . 00000101`

---

## Network ID vs Host ID Logic

Every IP address has two main parts. This is the most important rule in networking.

- **Network ID:** This part tells which neighborhood or group the computer belongs to.
- **Host ID:** This part tells the specific house number of that device inside the network.

**The Connection Rule:** If two devices want to talk directly without a router, their Network ID must be completely SAME, but their Host ID must be DIFFERENT.

---

## IP Classes Breakdown

IP addresses are divided into different classes according to network size. We only check the first number (First Octet) to find the class.

### Class A (The Mega Network)
- **Range:** 1 to 126
- **Architecture:** `Network . Host . Host . Host`
- **Logic:** First octet is Network, remaining 3 are Host. One network can have over 16 million computers. Used by NASA or Google.

### Class B (The Medium Network)
- **Range:** 128 to 191
- **Architecture:** `Network . Network . Host . Host`
- **Logic:** First 2 octets are Network, remaining 2 are Host. Used by large universities or medium companies.

*(Note: 127 is missing because 127.0.0.0 is reserved for Loopback/Localhost to check our own computer).*

### Class C (The Small Local Network)
- **Range:** 192 to 223
- **Architecture:** `Network . Network . Network . Host`
- **Logic:** First 3 octets are Network, last 1 is Host. Most home Wi-Fi routers use this. Only 254 computers can be on one network.

---

## What is a Switch?

A Switch is a physical hardware box with many ports where network cables are connected. It connects devices within the same local network (LAN).

- **Switch Brain (MAC Address Table):** The switch reads the physical MAC address of every connected device and makes a table inside its memory.
- **Secure Delivery:** When Computer A sends data to Computer B, the switch checks its table and sends the data only to Computer B's port. It does not leak data to other computers.

---

## Challenge Exercise: Bank Network Analysis

**Scenario:** You have two computers:
- Computer A: `192.168.1.10`
- Computer B: `192.168.1.20`

1. What class do these IPs belong to?
2. What is the Network ID for both?
3. Can they talk directly without a router?

---

**My Analysis:**
- Both are **Class C** because the first number is 192.
- Network ID for both is **192.168.1**.
- Since the Network ID is the same, they **CAN** talk directly without a router. Their Host IDs are different (10 and 20), which is required.

---

## What I Messed Up Today

Today I made a mistake when identifying the class of an IP.

I saw `172.16.5.10` and thought it was Class A because it starts with 172.

But then I checked the rules again:
- Class A range: 1 to 126
- Class B range: 128 to 191
- Since 172 is between 128 and 191, it is **Class B**.

For Class B, the first 2 octets are the Network ID.
- Computer A: `172.16.5.10` → Network ID: **172.16**
- Computer B: `172.20.5.20` → Network ID: **172.20**

Since they have different Network IDs, they are on different networks and **CANNOT** talk directly without a router.

I also learned about the **Switch**, which connects devices inside a local network using MAC addresses. It sends data only to the correct port, keeping the network secure.

I also learned about the **Loopback Address (127.0.0.1)**. This is the computer's own address used to test if the network hardware is working properly, even without an internet connection.
