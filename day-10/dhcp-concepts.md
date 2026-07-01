# Day 10: DHCP (Dynamic Host Configuration Protocol)

Today i am learning about DHCP, which automatically assigns IP addresses to devices when they join a network.
> Aaj main DHCP seekh raha hoon, jo naye devices ko network se judte hi automatically IP addresses de deta hai.

Imagine a big company where 1,000 people come daily and connect their laptops to Wi-Fi. If a network engineer manually typed IP addresses for everyone, their whole life would be wasted!
> Agar network engineer har bande ke paas ja kar manually IP address, Subnet Mask aur Gateway likhne baith jaye, toh uski poori zindagi isi mein nikal jayegi!

DHCP solves this problem. It is an automatic server that gives a free IP address (Lease) to any new device that connects to the network.
> DHCP network ka woh automatic server hai jo jaise hi koi naya computer network se judta hai, use chupke se khud hi ek khali IP address udhaar (Lease) par de deta hai.

---

## 1. How DHCP Works? (The DORA Process)

In networking, the DHCP working process is called DORA. When your mobile connects to Wi-Fi, these 4 steps happen in seconds:
> Networking ki dunya mein DHCP ke kaam karne ke tariqe ko DORA kehte hain. Jab aapka mobile Wi-Fi se connect hota hai, toh background mein yeh 4 steps seconds ke andar hote hain:

**D - Discover (Dhoondna)**
Your mobile sends a broadcast packet: "Hey, is there a DHCP server on this network? I need an IP address!"
> Aapka mobile network mein aate hi ek chillata hua packet (Broadcast) bhejta hai: "Oye, is network mein koi DHCP server hai? Mujhe IP address chahiye!"

**O - Offer (Peshkash)**
The DHCP server responds: "Yes, I have a free IP 192.168.1.50. Do you want it?"
> DHCP server sunta hai aur jawab deta hai: "Haan bhai, main hoon! Mere paas ek khali IP 192.168.1.50 pari hai, kya tumhein chahiye?"

**R - Request (Guzarish)**
Your mobile says: "Yes! I like this IP, lock it for me."
> Aapka mobile kehta hai: "Haan bilkul! Mujhe yeh IP bohot pasand aayi hai, mere naam par lock kar do."

**A - Acknowledgment (Pakka Waada)**
The DHCP server says: "Okay, this IP is yours for the next 24 hours. Here is the Subnet Mask and Gateway address too."
> DHCP server kehta hai: "Theek hai, yeh IP aglay 24 ghanton ke liye tumhari hui. Yeh lo sath mein Subnet mask aur Router (Gateway) ka address bhi."

---

## 2. Hacker's Mindset vs Defensive Mode

If there is an automatic IP assigning server on the network, how will a hacker exploit it and how will a defender protect it?
> Agar network mein IPs automatic baantne wala ek server majood hai, toh hacker iska faida kaise uthayega aur defender is se kaise bachega?

### Hacker's Attack: DHCP Starvation (Server Ko Bhuka Maarna)

The hacker thinks: "This DHCP server has limited IPs (let's say 200 IPs). If I send thousands of fake requests with fake MAC addresses, the server will give all its IPs to me and there will be none left for normal users!"
> Hacker sochega: "Is DHCP server ke paas limited IPs hain (maan lo 200 IPs). Agar main apne laptop se nakli MAC addresses bana kar hazaron fake requests bhejoon, toh server apni saari IPs mujhe hi de dega aur uske paas aam logon ke liye koi IP bachegi hi nahi!"

**Hacking Use:** When real users come, they will get no IP and their internet will stop (Denial of Service - DoS). Then the hacker sets up a fake DHCP server (Rogue DHCP), and any user who gets an IP from the hacker's server will have all their data pass through the hacker's computer!
> Jab asli users aayenge, toh unhein koi IP nahi milegi aur unka internet thapp ho jayega (Denial of Service - DoS). Phir hacker apna ek nakli DHCP server khol kar baith jayega (Rogue DHCP), aur jo bhi user hacker ke server se IP lega, uska saara data hacker ke computer se ho kar guzray ga!

### Defender's Counter: DHCP Snooping (Ghar Ka Chowkidar)

How does a good network defender stop this theft?
> Ab ek achha network defender is chori ko kaise rokta hai?

Switches have a special feature called DHCP Snooping.
> Switch ke andar ek khass feature hota hai jise DHCP Snooping kehte hain.

The defender marks the port where the real DHCP server is connected as Trusted.
> Defender switch ke us port ko jahan asli DHCP server laga hai, use Trusted (Bharosay mand) mark kar deta hai.

If a hacker tries to run a fake DHCP server from any other port, the switch will block (drop) those packets immediately!
> Agar hacker kisi aur port se apna nakli DHCP server chala kar IPs baantne ki koshish karega, toh switch uske packets ko raste mein hi block (drop) kar dega!

### Defender's Second Tool: MAC Limiting / Port Security

What if the hacker keeps changing MAC addresses to do DHCP Starvation?
> Agar hacker MAC address badal badal kar DHCP Starvation karne ki koshish kar raha hai toh?

A smart network defender adds another solid defensive tool called Port Security or MAC Limiting.
> Ek hoshiyar network defender DHCP Snooping ke sath ek aur solid defensive tool lagata hai jise Port Security ya MAC Limiting kehte hain.

**Defense Logic:** The admin sets a rule on every switch port: "Only 1 or 2 unique MAC addresses can connect from this port at a time."
> Admin switch ke har ek port par yeh rule laga deta hai ke: "Is port se ek waqt mein sirf 1 ya 2 unique MAC addresses hi connect ho sakte hain."

**Impact on Hacker:** As soon as the hacker sends a 3rd fake MAC address to request an IP, the switch immediately realizes something is wrong and shuts down (Shutdown) that port. The hacker's laptop is kicked off the network!
> Jaise hi hacker apne laptop se teesra (3rd) nakli MAC address bhej kar IP mangne ki koshish karega, switch foran samajh jayega ke dhandli ho rahi hai. Switch us port ko hi Shutdown (band) kar dega. Hacker ka laptop network se hi baher ho jayega!

### Hacker's Second Attack: DHCP Spoofing (Rogue DHCP - Speed Attack)

What if the hacker can't do Starvation because of Port Security, but the real DHCP server is slow?
> Agar Port Security ki wajah se hacker Starvation attack nahi kar sakta, lekin asli DHCP server slow ho toh?

The hacker thinks: "If the real server takes 3-4 seconds to reply, but my fake server replies in microseconds, I don't need to steal all IPs. I just need to be faster!"
> Hacker sochega: "Agar asli server jawab dene mein 3-4 seconds lagata hai, aur mera nakli server micro-seconds mein jawab de deta hai, toh mujhe saari IPs churane ki zaroorat nahi. Mujhe bas tez hona hai!"

**Hacking Use:** In the DORA process, the device accepts the very first "Offer" it receives. If the hacker's fake DHCP server replies first with a fake IP, the user's device will accept it, and all their data will pass through the hacker's computer!
> DORA process mein device sab se pehle aane wali "Offer" ko accept kar leta hai. Agar hacker ka nakli server pehle jawab de kar nakli IP de de, toh user ka device use accept kar lega, aur saara data hacker ke computer se ho kar guzray ga!

### Defender's Additional Protection: Authoritative DHCP

How does a defender stop this speed attack?
> Defender is speed attack ko kaise rokta hai?

**Authoritative DHCP:** In enterprise networks, the main DHCP server is set as Authoritative. If any other unofficial DHCP server tries to give out IPs, the real server sends a "Decline" packet across the network to cancel those fake IPs.
> Active Directory ya main server mein DHCP ko hamesha Authoritative set kiya jata hai. Agar network mein koi aur naya DHCP server un-official IPs baantne ki koshish karega, toh asli server pure network par ek "Decline" packet bhej kar us nakli IP ko cancel karwa dega.

---

## What I Learned and Solved Today (My Hacker Analysis)

Today I completely learned the DORA process and both attack and defense perspectives of DHCP.
> Aaj maine DORA process aur DHCP ke attack aur defense dono angles ko deeply samajh liya.

### My Key Learnings:

* DHCP automatically assigns IPs using the DORA process (Discover, Offer, Request, Acknowledgment)
> DHCP DORA process ke zariye automatically IPs baant ta hai

* DHCP Starvation: Hacker sends fake MAC addresses to exhaust all IPs
> DHCP Starvation: Hacker nakli MAC addresses bhej kar saari IPs khatam kar deta hai

* DHCP Snooping: Switch blocks fake DHCP servers from untrusted ports
> DHCP Snooping: Switch untrusted ports se aane wale fake DHCP servers ko block kar deta hai

* Port Security: Switch limits how many MAC addresses can connect from one port
> Port Security: Switch ek port se sirf limited MAC addresses ko connect karne deta hai

* DHCP Spoofing: Hacker uses a faster fake DHCP server to trick users
> DHCP Spoofing: Hacker tez nakli DHCP server bana kar users ko bewaqoof banata hai

> Ab DHCP ka poora game samajh aa gaya hai. Pata hai ke hacker kaise attack karta hai aur defender kaise bachta hai!
