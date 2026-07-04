# Day 20: Wireshark & Packet Analysis

Today i am learning about Wireshark, which is like an X-Ray machine for the network.
> Aaj main Wireshark seekh raha hoon, jo network ke liye X-Ray machine ki tarah hai.

Until now we learned many protocols (IP, MAC, ARP, DNS, NAT) — they all run in the background as packets through wires or air. Normal people can't see these packets.
> Abhi tak humne jitne bhi protocols parhe (IP, MAC, ARP, DNS, NAT), woh sab background mein chupi hui taron ya hawa mein packets ki shakal mein daurhte hain. Ek aam bande ko woh packets nazar nahi aate.

But a cyber security expert or hacker has a superpower called Packet Sniffing, and the most famous tool for this is Wireshark!
> Lekin ek cyber security expert ya hacker ke paas ek aisi superpower hoti hai jise Packet Sniffing kehte hain, aur iska sab se mashhoor tool hai Wireshark!

---

## 1. What is Wireshark? (The Logic)

Wireshark is basically the network's X-Ray Machine or Microscope.
> Wireshark asal mein network ka X-Ray Machine ya Microscope hai.

**How it Works?** When you turn it on your computer, your network card (NIC) captures all packets passing through it (whether it's YouTube data, Facebook requests, or a hacker's attack). Wireshark catches all those packets from the air and opens them on your screen.
> Jab aap isey apne computer par on karte ho, toh aapke computer ke network card (NIC) se jitne bhi packets guzar rahe hote hain (chahe woh YouTube ka data ho, Facebook ki request ho, ya kisi hacker ka attack), Wireshark un saare packets ko hawa se pakar kar aapki screen par khol deta hai.

You can go inside every packet and see: what is its Source IP, Destination IP, which Port is being used, and what data is written inside.
> Aap har packet ke andar ghus kar dekh sakte ho ke uski Source IP kya hai, Destination IP kya hai, usmein kaun sa Port use ho raha hai, aur andar kya data likha hua hai.

---

## 2. Hacker's Vision: Packet Sniffing

Imagine a hacker has redirected all network traffic to their laptop using attacks we learned (ARP Spoofing or MAC Flooding). Now what do they do?
> Maan lo ek hacker ne kal wale attacks (ARP Spoofing ya MAC Flooding) ke zariye network ka saara traffic apne laptop ki taraf mor liya hai. Ab woh kya karega?

**The Trap:** The hacker turns on Wireshark. Now any normal user's data on the network appears live on the hacker's screen.
> Hacker Wireshark on karega. Ab network par chalne wale kisi bhi aam bande ka data hacker ki screen par live dikhega.

**HTTP vs HTTPS Difference (Live Proof):**
> HTTP vs HTTPS Ka Farq (Live Proof):

- If someone uses an old website (HTTP) and types their username and password, Wireshark catches that packet and the hacker sees the password in "Plain Text" (clear words) on the screen (like: password123).
> Agar koi banda kisi purani website (HTTP) par ja kar apna username aur password likhega, toh Wireshark us packet ko pakre ga aur hacker ko screen par "Plain Text" (saaf saaf shabdon mein) password dikh jayega (jaise: password123).

- But if the same person uses HTTPS, the hacker only sees garbage (encrypted characters) in Wireshark, which is impossible to open.
> Lekin agar wohi banda HTTPS use kar raha hoga, toh Wireshark mein hacker ko sirf kachra (encrypted characters) dikhega, jise kholna namumkin hai.

---

## 3. Defender's Mode: Finding Malicious Traffic

Defenders use Wireshark to catch attacks happening on the network:
> Defenders Wireshark ka istemal network par chalne wale hamlon ko pakarne ke liye karte hain:

**Catching ARP Spoofing:** If ARP Spoofing is happening on the network, Wireshark will suddenly show two different MAC addresses for the same IP. Wireshark gives a warning (Alert) there.
> ARP Spoofing Pakarna: Agar network mein ARP Spoofing ho rahi hai, toh Wireshark mein achanak aik hi IP ke sath do alag alag MAC addresses dikhna shuru ho jayenge. Wireshark wahan warning (Alert) de deta hai.

**Catching Ping Flood:** If someone is attacking with ICMP, Wireshark will show thousands of ICMP (Ping) packets in a single second, making the admin realize an attack is happening.
> Ping Flood Pakarna: If someone is attacking with ICMP, Wireshark mein ek hi second mein hazaaron ICMP (Ping) packets line se dikh jayenge, jise dekh kar admin samajh jata hai ke koi attack kar raha hai.

---

## 4. MUST MEMORIZE (Zubani Yaad Rakho)

- **Wireshark:** The biggest tool for capturing and analyzing network traffic.
> Network traffic ko capture aur analyze karne wala sab se bada tool.

- **Packet Sniffing:** Secretly capturing and reading data packets passing through the network.
> Network se guzre wale data packets ko chupke se pakarna aur parhna.

- **Promiscuous Mode:** A special setting on the network card that, when turned on, makes the card capture not just its own traffic but ALL traffic on the network.
> Network card ki ek khass setting jo on karne se card sirf apne liye nahi, balki network par chalne wale baqi sab ke packets ko bhi capture karna shuru kar deta hai.

---

## 5. HTTP vs HTTPS in Wireshark

| HTTP (Unsecure) | HTTPS (Secure) |
|-----------------|----------------|
| Data is Plain Text | Data is Encrypted |
| Passwords visible in Wireshark | Only garbage/encrypted data visible |
| Hacker can read everything | Hacker cannot read anything |

> HTTP mein data (passwords) Plain Text dikhta hai | HTTPS mein Encrypted Kachra dikhta hai
> HTTP mein passwords Wireshark mein saaf dikhte hain | HTTPS mein sirf kachra dikhta hai
> Hacker saara data parh sakta hai | Hacker kuch nahi parh sakta

---

## What I Learned Today

Today I learned Wireshark and Packet Analysis properly. Now I know:
> Aaj maine Wireshark aur Packet Analysis sahi se seekh liya. Ab mujhe pata hai:

* Wireshark is an X-Ray machine for network traffic
> Wireshark network traffic ke liye X-Ray machine hai

* Packet Sniffing captures packets passing through the network
> Packet Sniffing network se guzre wale packets ko capture karta hai

* Promiscuous Mode lets network card capture ALL network traffic
> Promiscuous Mode network card ko saara network traffic capture karne deta hai

* HTTP traffic shows Plain Text passwords in Wireshark
> HTTP traffic Wireshark mein Plain Text passwords dikhata hai

* HTTPS traffic only shows encrypted garbage in Wireshark
> HTTPS traffic Wireshark mein sirf encrypted kachra dikhata hai

* Defenders use Wireshark to detect ARP Spoofing and Ping Flood attacks
> Defenders Wireshark use karte hain ARP Spoofing aur Ping Flood attacks detect karne ke liye

* Wireshark is used by both hackers (for attacks) and defenders (for detection)
> Wireshark hackers (attacks ke liye) aur defenders (detection ke liye) dono use karte hain

> Ab Wireshark aur Packet Analysis ka poora game samajh aa gaya hai!# Day 20: Wireshark & Packet Analysis — Network Ka X-Ray Machine

Today i am learning about Wireshark, which is like an X-Ray machine for the network.
> Aaj main Wireshark seekh raha hoon, jo network ke liye X-Ray machine ki tarah hai.

Until now we learned many protocols (IP, MAC, ARP, DNS, NAT) — they all run in the background as packets through wires or air. Normal people can't see these packets.
> Abhi tak humne jitne bhi protocols parhe (IP, MAC, ARP, DNS, NAT), woh sab background mein chupi hui taron ya hawa mein packets ki shakal mein daurhte hain. Ek aam bande ko woh packets nazar nahi aate.

But a cyber security expert or hacker has a superpower called Packet Sniffing, and the most famous tool for this is Wireshark!
> Lekin ek cyber security expert ya hacker ke paas ek aisi superpower hoti hai jise Packet Sniffing kehte hain, aur iska sab se mashhoor tool hai Wireshark!

---

## 1. What is Wireshark? (The Logic)

Wireshark is basically the network's X-Ray Machine or Microscope.
> Wireshark asal mein network ka X-Ray Machine ya Microscope hai.

**How it Works?** When you turn it on your computer, your network card (NIC) captures all packets passing through it (whether it's YouTube data, Facebook requests, or a hacker's attack). Wireshark catches all those packets from the air and opens them on your screen.
> Jab aap isey apne computer par on karte ho, toh aapke computer ke network card (NIC) se jitne bhi packets guzar rahe hote hain (chahe woh YouTube ka data ho, Facebook ki request ho, ya kisi hacker ka attack), Wireshark un saare packets ko hawa se pakar kar aapki screen par khol deta hai.

You can go inside every packet and see: what is its Source IP, Destination IP, which Port is being used, and what data is written inside.
> Aap har packet ke andar ghus kar dekh sakte ho ke uski Source IP kya hai, Destination IP kya hai, usmein kaun sa Port use ho raha hai, aur andar kya data likha hua hai.

---

## 2. Hacker's Vision: Packet Sniffing

Imagine a hacker has redirected all network traffic to their laptop using attacks we learned (ARP Spoofing or MAC Flooding). Now what do they do?
> Maan lo ek hacker ne kal wale attacks (ARP Spoofing ya MAC Flooding) ke zariye network ka saara traffic apne laptop ki taraf mor liya hai. Ab woh kya karega?

**The Trap:** The hacker turns on Wireshark. Now any normal user's data on the network appears live on the hacker's screen.
> Hacker Wireshark on karega. Ab network par chalne wale kisi bhi aam bande ka data hacker ki screen par live dikhega.

**HTTP vs HTTPS Difference (Live Proof):**
> HTTP vs HTTPS Ka Farq (Live Proof):

- If someone uses an old website (HTTP) and types their username and password, Wireshark catches that packet and the hacker sees the password in "Plain Text" (clear words) on the screen (like: password123).
> Agar koi banda kisi purani website (HTTP) par ja kar apna username aur password likhega, toh Wireshark us packet ko pakre ga aur hacker ko screen par "Plain Text" (saaf saaf shabdon mein) password dikh jayega (jaise: password123).

- But if the same person uses HTTPS, the hacker only sees garbage (encrypted characters) in Wireshark, which is impossible to open.
> Lekin agar wohi banda HTTPS use kar raha hoga, toh Wireshark mein hacker ko sirf kachra (encrypted characters) dikhega, jise kholna namumkin hai.

---

## 3. Defender's Mode: Finding Malicious Traffic

Defenders use Wireshark to catch attacks happening on the network:
> Defenders Wireshark ka istemal network par chalne wale hamlon ko pakarne ke liye karte hain:

**Catching ARP Spoofing:** If ARP Spoofing is happening on the network, Wireshark will suddenly show two different MAC addresses for the same IP. Wireshark gives a warning (Alert) there.
> ARP Spoofing Pakarna: Agar network mein ARP Spoofing ho rahi hai, toh Wireshark mein achanak aik hi IP ke sath do alag alag MAC addresses dikhna shuru ho jayenge. Wireshark wahan warning (Alert) de deta hai.

**Catching Ping Flood:** If someone is attacking with ICMP, Wireshark will show thousands of ICMP (Ping) packets in a single second, making the admin realize an attack is happening.
> Ping Flood Pakarna: If someone is attacking with ICMP, Wireshark mein ek hi second mein hazaaron ICMP (Ping) packets line se dikh jayenge, jise dekh kar admin samajh jata hai ke koi attack kar raha hai.

---

## 4. MUST MEMORIZE (Zubani Yaad Rakho)

- **Wireshark:** The biggest tool for capturing and analyzing network traffic.
> Network traffic ko capture aur analyze karne wala sab se bada tool.

- **Packet Sniffing:** Secretly capturing and reading data packets passing through the network.
> Network se guzre wale data packets ko chupke se pakarna aur parhna.

- **Promiscuous Mode:** A special setting on the network card that, when turned on, makes the card capture not just its own traffic but ALL traffic on the network.
> Network card ki ek khass setting jo on karne se card sirf apne liye nahi, balki network par chalne wale baqi sab ke packets ko bhi capture karna shuru kar deta hai.

---

---

## What I Learned Today

Today I learned Wireshark and Packet Analysis properly. Now I know:
> Aaj maine Wireshark aur Packet Analysis sahi se seekh liya. Ab mujhe pata hai:

* Wireshark is an X-Ray machine for network traffic
> Wireshark network traffic ke liye X-Ray machine hai

* Packet Sniffing captures packets passing through the network
> Packet Sniffing network se guzre wale packets ko capture karta hai

* Promiscuous Mode lets network card capture ALL network traffic
> Promiscuous Mode network card ko saara network traffic capture karne deta hai

* HTTP traffic shows Plain Text passwords in Wireshark
> HTTP traffic Wireshark mein Plain Text passwords dikhata hai

* HTTPS traffic only shows encrypted garbage in Wireshark
> HTTPS traffic Wireshark mein sirf encrypted kachra dikhata hai

* Defenders use Wireshark to detect ARP Spoofing and Ping Flood attacks
> Defenders Wireshark use karte hain ARP Spoofing aur Ping Flood attacks detect karne ke liye

* Wireshark is used by both hackers (for attacks) and defenders (for detection)
> Wireshark hackers (attacks ke liye) aur defenders (detection ke liye) dono use karte hain

> Ab Wireshark aur Packet Analysis ka poora game samajh aa gaya hai!
