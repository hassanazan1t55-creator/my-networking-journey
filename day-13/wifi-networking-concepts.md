# Day 13: Wi-Fi Networking — Wireless Communication Fundamentals

Today I am learning about Wi-Fi networking, which is the wireless technology that connects devices without cables.

Until now, we discussed computers connected through wires (cables). But today, almost every home and office uses internet through the air, which we call Wi-Fi. In networking, Wi-Fi's technical name is IEEE 802.11.

For both hackers and defenders, understanding data flowing through the air is crucial, because to touch wires you need to enter the building physically, but Wi-Fi signals travel outside the building to the streets!

---

## How Wi-Fi Works: SSID, BSSID & Channels

When you turn on Wi-Fi on your mobile, you see nearby network names. The technical story behind them is:

**SSID (Service Set Identifier)**
This is simply your Wi-Fi's Name (e.g., "PTCL-BB" or "Home-WiFi").

**BSSID (Basic Service Set Identifier)**
This is the real MAC Address of the Router/Access Point that is broadcasting signals. The name (SSID) can be changed, but the BSSID (MAC) is fixed.

**Frequencies & Channels**
Wi-Fi generally runs on two frequencies:

**2.4 GHz:** This goes far but has slightly slower speed. It has channels 1 to 11.

**5 GHz:** This doesn't go as far but has rocket-fast speed.

---

## Wi-Fi Security Protocols: WPA2 vs WPA3

Since data is traveling through the air, anyone can catch it. So it's essential to lock (Encrypt) the data:

**WPA2 (Pre-Shared Key)**
This has been used in almost every home for the last 15-20 years. When you enter the password, the router and your mobile perform a 4-Way Handshake (they cryptographically shake hands and confirm the password is correct).

**WPA3**
This is the newest and most advanced standard. Security has been tightened further to eliminate the weaknesses of old WPA2.

---

## The Hacker's Mindset vs. Defensive Operations

Wi-Fi is the most fun target for hackers because they don't need to enter the target's building — they can scan from their car outside!

### 1. The Attack: The Deauthentication Attack

**Hacker's Logic:** The hacker puts their Wi-Fi card into Monitor Mode (a mode that captures all packets from the air). They send a fake packet called a Deauth Packet into the air. This packet tells the router "Disconnect the user" and tells the user "Disconnect from the router".

**The Impact:** The user's internet immediately stops and their mobile automatically tries to reconnect to the router. When it reconnects, the same 4-Way Handshake happens again. The hacker captures (records) that handshake from the air and later tries to crack it.

### 2. The Defense: Hidden SSID & MAC Filtering

**Defensive Action:** The admin goes into the router settings and hides the Wi-Fi name. Now normal people won't see the Wi-Fi name unless they know the exact name. Additionally, the admin adds a rule in the router: "Only allow these specific MAC addresses to use the internet. Block everyone else."

---

## The 4-Way Handshake Explained

When you enter your Wi-Fi password and press connect, the mobile doesn't send the password directly to the router (because if it did, anyone in the air could catch it).

Instead, 4 messages happen in the background:

**Message 1:** Router sends a random code (ANonce) to the mobile.

**Message 2:** Mobile combines its own random code (SNonce) + password to create a unique proof (MIC) and sends it back. (This is what hackers capture from the air!)

**Message 3:** Router checks the proof and says "Proof is correct, here is the key."

**Message 4:** Mobile says "Done! I am now starting encryption."

---

## The TCP 3-Way vs Wi-Fi 4-Way Handshake

| Feature | TCP 3-Way Handshake | Wi-Fi 4-Way Handshake |
|---------|---------------------|----------------------|
| **Layer** | OSI Layer 4 (Transport) | OSI Layer 2 (Data Link) |
| **Purpose** | Establishes a connection for data transfer | Confirms Wi-Fi password and generates encryption keys |
| **Process** | SYN → SYN-ACK → ACK | ANonce → SNonce+MIC → Confirmation → Done |
| **Used For** | Internet communication (Google, Facebook) | Wi-Fi authentication (WPA2/WPA3) |

---

## Wi-Fi MAC Spoofing Bypass — Full Logic

Imagine you are outside a company. Their Wi-Fi is Hidden and they have MAC Filtering enabled (only the owner's laptop with MAC AA:BB:CC:DD:EE:FF can connect).

Your laptop is outside and your MAC address is 11:22:33:44:55:66. If you try to connect, the router will reject you because your MAC isn't on the allowed list (Whitelist).

### Step 1: Packet Sniffing (Monitor Mode)

The hacker puts their Wi-Fi card into Monitor Mode. Monitor Mode means your Wi-Fi card captures every packet floating in the air and displays it on the screen. The hacker sees a connected computer and its MAC: **AA:BB:CC:DD:EE:FF**.

### Step 2: MAC Spoofing

The hacker goes to the terminal and changes their own MAC to the employee's MAC: **AA:BB:CC:DD:EE:FF**.

### Step 3: Firewall Bypass

Now the router thinks this is the trusted employee and lets them in. Firewall bypassed!

---

## Important: MAC Spoofing Does NOT Bypass Password

**Technical Fact:** MAC Spoofing does NOT bypass the Wi-Fi password. You must still enter the correct password to complete the 4-Way Handshake.

The router has TWO separate security walls:

**Wall 1: Wi-Fi Encryption (The Password Gate)**
To complete the 4-Way Handshake, you MUST have the Wi-Fi password. Without it, your laptop can't even finish the handshake.

**Wall 2: MAC Filtering (The Guard List)**
After you enter the correct password and complete the handshake, the router checks: "Is this MAC address allowed?"

**Conclusion:**
- Correct Password + Wrong MAC = Blocked 
- No Password + Spoofed MAC = Blocked  (Handshake fails)
- Correct Password + Spoofed MAC = Firewall Bypass! 

---

## Elite Challenge: The MAC Conflict Scenario

**Scenario:** You successfully spoofed the employee's MAC address and entered the network. But as soon as you connected, you realized the internet wasn't working because the employee's real laptop was also on the network at the same time!

When two computers on the same network have the same MAC address (AA:BB:CC:DD:EE:FF), the router gets confused about who to send data to.

**Hacker's Logic:** To solve this, I would either:
1. **Wait** — If I want to stay stealthy and not alert anyone.
2. **Disconnect the real employee** — If I need immediate access, I would use a Deauthentication attack to kick the real employee off the network so only my spoofed connection remains.

---

## What I Messed Up Today

Today I learned the difference between TCP 3-Way Handshake and Wi-Fi 4-Way Handshake. I initially thought they were the same thing, but now I understand:

- **TCP 3-Way** is for establishing internet connections (SYN → SYN-ACK → ACK)
- **Wi-Fi 4-Way** is for authenticating with the Wi-Fi router and generating encryption keys

I also learned that MAC Spoofing does NOT bypass the Wi-Fi password — it only tricks the MAC Filtering list. The 4-Way Handshake still requires the correct password.

The key lesson is that Monitor Mode and MAC Spoofing are powerful tools, but they work within the limits of the Wi-Fi security protocol. Strong passwords (like WPA3) and enterprise authentication (802.1X) make these attacks much harder to execute.
