# Day 22: TCP Three-Way Handshake & Flags

Today i am learning about TCP Flags and how hackers use them for stealth scanning.
> Aaj main TCP Flags seekh raha hoon aur hacker in flags ko stealth scanning ke liye kaise use karta hai.

We learned before that TCP is a reliable protocol that does a Three-Way Handshake before sending data. Today we will look at the hidden Flags (Control Switches) inside it and understand how hackers use these flags to scan networks.
> Humne pehle seekha tha ke TCP ek reliable protocol hai jo data bhejne se pehle dosti karta hai jise Three-Way Handshake kehte hain. Aaj hum iske andar chupay hue Flags (Control Switches) ko dekhenge aur yeh samjhenge ke hacker in flags se network ko kaise scan karta hai.

---

## 1. What are TCP Flags? (The Control Buttons)

In the TCP packet header, there are small switches called Flags. They tell packets what their purpose is. For hacking and security, these 4 flags are the most important:
> TCP packet ke header mein chote chote switches hote hain jinhein Flags kehte hain. Yeh packets ko unka maqsad batate hain. Hacking aur security ke liye 4 sab se VIP flags yeh hain:

**1. SYN (Synchronize)**
Used to start a connection (to extend a friendship hand).
> Connection shuru karne (dosti ka hath barhane) ke liye.

**2. ACK (Acknowledgment)**
Used to confirm receipt or give a reply (e.g., "I received your packet").
> Baat maan ne ya reply dene ke liye (e.g., "Mujhe tumhara packet mil gaya").

**3. RST (Reset)**
Used to abruptly close a connection if something goes wrong.
> Connection ko jhatke se band karne ke liye agar koi masla ho jaye.

**4. FIN (Finish)**
Used to politely close a connection after work is done.
> Kaam khatam hone par tameez se connection band karne ke liye.

---

## 2. The Real Handshake Postmortem

When your computer connects to a server, these flags work together like this:
> Jab aapka computer kisi server se connect hota hai, toh unke beech yeh flags is tarah kaam karte hain:

**Step 1 (You -> Server):** Your computer sends a packet with only the SYN flag turned ON.
> Aapka computer sirf SYN flag on kar ke bhejta hai.

**Step 2 (Server -> You):** The server accepts the friendship and sends back a packet with both SYN and ACK flags turned ON (SYN-ACK).
> Server dosti qabool karta hai aur SYN aur ACK dono flags on kar ke bhejta hai (SYN-ACK).

**Step 3 (You -> Server):** Your computer sends a final ACK flag. Connection established!
> Aapka computer aakhri baar ACK flag bhejta hai. Connection established!

---

## 3. Hacker's Trick: Stealth (SYN) Port Scanning

Hackers use this handshake to find open ports on a target computer (using Nmap tool). This is called SYN Scan or Half-Open Scan:
> Hacker is handshake ka faida utha kar target computer ke khule hue ports ka pata lagata hai (Nmap tool ke zariye), jise SYN Scan ya Half-Open Scan kehte hain:

**Hacker's Mindset:** The hacker sends a SYN packet to the target port.
> Hacker target port par SYN packet bhejta hai.

**If Port is OPEN:** The server sends back SYN-ACK. Now the hacker knows the port is open! But the hacker is smart — instead of sending the third ACK packet, they send a RST (Reset) packet to break the half-open connection so no entry is logged in firewalls.
> Agar Port KHULA (Open) ho: Server aage se SYN-ACK bhejega. Hacker ko pata chal gaya ke port khula hai! Lekin hacker chalaki karta hai—woh teesra ACK packet bhejne ki jagah RST (Reset) packet bhej deta hai taake connection adha khula hi toot jaye aur firewalls mein uski entry na ho.

**If Port is CLOSED:** The server sends back a RST packet saying "Bro, there is no space here, get lost!"
> Agar Port BAND (Closed) ho: Server aage se seedha RST packet bhej deta hai ke "Bhai, yahan koi jagah nahi hai, dafa ho jao!"

---

## 4. Defender's Defense: Stateful Firewalls

Defenders protect against these half-open connections (SYN Flood) by using Stateful Firewalls. These firewalls keep track of the complete handshake. If a device only sends SYN packets and doesn't complete the handshake, the firewall immediately Blocks that IP.
> Defenders in adhe khule connections (SYN Flood) se bachne ke liye Stateful Firewalls lagate hain. Yeh firewalls poore handshake ka track rakhti hain. Agar koi device sirf SYN bhej rahi hai aur handshake mukammal nahi kar rahi, toh firewall us IP ko foran Block kar deti hai.

---

## 5. SYN Scan vs SYN Flood (Important Difference)

| SYN Scan (Stealth Scan) | SYN Flood (DoS Attack) |
|-------------------------|------------------------|
| Purpose: Check if port is open or closed | Purpose: Crash/Down the server |
| Sends very few packets | Sends thousands/millions of SYN packets |
| Sends RST to close connection | Never completes handshake |
| Stealthy, hard to detect | Creates huge traffic, easy to detect |

> SYN Scan: Chupke se sirf port check karna (Stealth Scanning) | SYN Flood: Hazaaron packets bhej kar server ko down karna (Attack/Denial of Service)
> SYN Scan: Bohot thore packets bhejta hai | SYN Flood: Hazaaron-lakhon SYN packets bhejta hai
> SYN Scan: RST bhej kar connection torhta hai | SYN Flood: Handshake complete nahi karta
> SYN Scan: Chupke se pata lagana | SYN Flood: Server ko crash karna

---

## 6. MUST MEMORIZE (Zubani Yaad Rakho)

- **SYN:** Connection initialization flag.
> Connection initialization flag.

- **SYN-ACK:** Server's positive response to connection.
> Server's positive response to connection.

- **RST:** Abrupt connection termination signal.
> Foran connection torhne ka signal.

- **FIN:** Polite connection termination signal.
> Tameez se connection band karne ka signal.

- **Stealth Scan:** Finding open ports with half-handshake without getting caught.
> Adha handshake kar ke khule ports ka pata lagana bina pakray gae.

---

## What I Learned Today

Today I learned TCP Flags and Stealth Scanning properly. Now I know:
> Aaj maine TCP Flags aur Stealth Scanning sahi se seekh liya. Ab mujhe pata hai:

* TCP Flags are control switches in packet headers
> TCP Flags packet headers mein control switches hain

* SYN starts connection, ACK confirms, RST resets, FIN finishes
> SYN connection shuru karta hai, ACK confirm karta hai, RST reset karta hai, FIN finish karta hai

* Three-Way Handshake: SYN → SYN-ACK → ACK
> Three-Way Handshake: SYN → SYN-ACK → ACK

* SYN Scan sends SYN, gets SYN-ACK for open ports, RST for closed
> SYN Scan SYN bhejta hai, open ports par SYN-ACK milta hai, closed par RST milta hai

* Hacker sends RST instead of ACK to stay stealthy (no log entry)
> Hacker ACK ki jagah RST bhejta hai taake chupke rahe (no log entry)

* SYN Scan is for checking ports (Stealth)
> SYN Scan ports check karne ke liye hai (Stealth)

* SYN Flood is for crashing servers (DoS Attack)
> SYN Flood servers crash karne ke liye hai (DoS Attack)

* Stateful Firewalls track handshake and block incomplete connections
> Stateful Firewalls handshake track karti hain aur incomplete connections block karti hain

> Ab TCP Flags aur Stealth Scanning ka poora game samajh aa gaya hai!
