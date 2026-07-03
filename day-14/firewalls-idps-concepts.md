# Day 14: Firewalls & IDPS

Today i am learning about Firewalls and IDPS, which are the real security guards of any network.
> Aaj main Firewalls aur IDPS seekh raha hoon, jo network ke asli security guards hain.

Imagine a big VIP event is happening (your network), and thousands of people are standing outside trying to get in. If there is no guard outside, any thief or enemy can enter. In networking, Firewalls and IDPS do this guard work.
> Maan lo ek bohot bada VIP event chal raha hai (aapka network), aur baher hazaaron log andar aane ke liye khare hain. Agar baher koi guard nahi hoga, toh koi bhi chor ya dushman andar ghus jayega. Networking mein isi guard ka kaam Firewalls aur IDPS karte hain.

---

## 1. What is a Firewall? (The Gatekeeper)

A firewall is a security device (or software) that stands like a wall between your safe internal network and the unsafe outside internet world.
> Firewall ek aisi security device (ya software) hoti hai jo aapke internal safe network aur baher ki unsafe internet dunya ke darmayan ek deewar ban kar khadi hoti hai.

Its job is to check every incoming and outgoing packet and allow or block them according to Rules.
> Iska kaam hota hai har aane aur jaane wale packet ko check karna aur unhein Rules ke mutabiq ijazat dena ya block karna.

---

## 2. Two Main Types of Firewalls (Must Memorize)

**1. Packet Filtering Firewall (Stateless)**
This is old and basic firewall. It only looks at the packet's "face" — Source IP, Destination IP, and Port Number. If the rule says "Port 23 is blocked", it throws away the packet without thinking. It does NOT check the inside data of the packet.
> Yeh purani aur basic firewall hoti hai. Yeh packet ka sirf "huliya" dekhti hai—yaani Source IP, Destination IP, aur Port Number. Agar rule likha hai ke "Port 23 block hai", toh yeh bina soche packet ko phenk degi. Yeh packet ke andar ka data check nahi karti.

**2. Stateful Inspection Firewall**
This is advanced and smarter. It doesn't just look at the face, it keeps track (state) of the whole Connection. If you opened google.com from your browser, it knows this request came from inside, so the returning data is safe. If someone from outside suddenly tries to enter without a request, it will block them.
> Yeh advanced aur hoshiyar hoti hai. Yeh sirf huliya nahi dekhti, balki yeh poore Connection ka track (state) rakhti hai. Agar aapne khud browser par google.com khola, toh yeh samajh jayegi ke yeh request andar se gayi thi, isliye iska wapas aane wala data safe hai. Agar baher se koi achanak bina request ke andar ghusne ki koshish karega, toh yeh use block kar degi.

---

## 3. IDPS (Intrusion Detection and Prevention Systems)

Firewall only checks at the door. But if a thief changes identity (like we learned MAC Spoofing) and enters through the door, what happens inside? Inside we need CCTV cameras and Alarms — this is IDPS.
> Firewall sirf darwaze par check karti hai, lekin agar koi chor pehchan badal kar (jaise kal humne MAC spoofing parha) darwaze se andar ghus jaye, toh andar kya hoga? Andar hume chahiye CCTV Cameras aur Alarms—yahi kaam IDPS ka hai.

**IDS (Intrusion Detection System)**
This is the network's CCTV Camera. It only monitors traffic and when it sees suspicious activity (like continuous nmap scan or brute force attack), it sends an Alert (warning) to the admin. It does NOT stop the attack itself, only tells about it.
> Yeh network ka CCTV Camera hai. Yeh sirf traffic ko monitor karta hai aur jaise hi koi suspicious activity (jaise lagatar nmap scan ya brute force attack) dekhta hai, toh admin ko Alert (warning) bhej deta hai. Yeh khud attack ko rokta nahi hai, sirf batata hai.

**IPS (Intrusion Prevention System)**
This is the network's Active Commando. It not only sends alerts, but when it sees an attack, it Auto-Blocks (drops) that traffic and cuts the hacker's connection.
> Yeh network ka Active Commando hai. Yeh sirf alert nahi bhejta, balki jaise hi koi hamla dekhta hai, us traffic ko Auto-Block (drop) kar deta hai aur hacker ka connection kaat deta hai.

---

## 4. Hacker's Vision vs Defender

### Hacker Attack: Firewall Evasion (Fragmentation)

When a hacker sees a firewall in front, they don't attack directly.
> Hacker jab dekhta hai ke samne firewall khadi hai, toh woh direct attack nahi karta.

**Fragmentation:** The hacker breaks their attack packets into very small pieces (fragments). When these small pieces pass through the firewall, basic firewalls can't recognize them and let them through as normal traffic. Once inside, these pieces rejoin on the target computer and the attack executes!
> Hacker apne attack packets ko bohot chote chote tukron (fragments) mein tor deta hai. Jab yeh chote chote tukre firewall se guzarte hain, toh basic firewalls unhein pehchan nahi patin aur normal traffic samajh kar andar jaane deti hain. Andar ja kar target computer par yeh sare tukre dobara judte hain aur attack execute ho jata hai!

**Nmap Switch:** Hackers use `-f` switch in Nmap for this (Packet Fragmentation).
> Hacker iske liye Nmap mein `-f` switch lagata hai (Packet Fragmentation).

### Defender Counter: Deep Packet Inspection (DPI)

Defenders use Next-Generation Firewalls (NGFW) to protect against this:
> Defenders is se bachne ke liye Next-Generation Firewalls (NGFW) lagate hain:

**DPI:** This firewall doesn't just look at the packet header or port. It opens the packet completely and scans the inside data (payload) too. Even if the hacker fragments the packets, NGFW first rejoins them, checks them, and then lets them through.
> Yeh firewall sirf packet ka header ya port nahi dekhti, balki packet ko poora khol kar uske andar ka data (payload) bhi scan karti hai. Agar hacker packet ke tukre bhi kar de, toh NGFW unhein pehle khud jorh kar check karti hai aur phir guzarne deti hai.

---

## 5. MUST MEMORIZE (Zubani Yaad Rakho)

- **Stateless Firewall:** Only checks IP and Port, doesn't remember connection history.
> Sirf IP aur Port dekhti hai, connection ki history nahi rakhti.

- **Stateful Firewall:** Remembers connection history and state.
> Connection ki history aur state yaad rakhti hai.

- **IDS vs IPS:** IDS only finds and alerts (Passive), IPS finds AND blocks (Active).
> IDS sirf dhoondta aur alert karta hai (Passive), IPS dhoondta bhi hai aur block bhi karta hai (Active).

- **Nmap Flag -f:** Used to fragment packets for bypass.
> Packets ko fragmant (tukron mein) karne ke liye bypass switch.

---

## 6. Deep Logic (Samajhna Hai)

**Hacker Vision:** When doing a pentest on an office, if your normal scans are getting blocked, understand that an IPS is sitting in front recognizing your automatic speed. An elite hacker slows their scanning speed (like sending one packet every 5-10 minutes), called Stealth Scanning, so IDPS doesn't trigger alarms.
> Kisi office ko pentest karte waqt agar aapke normal scans block ho rahe hain, toh samajh jao ke samne IPS baitha hai jo aapki automatic speed ko pehchan raha hai. Ek elite hacker apni scanning speed ko ek dum slow kar deta hai (jaise har packet 5-10 minute baad bhejna), jise Stealth Scanning kehte hain, taake IDPS alarm na bajaye.

---

## What I Learned Today

Today I learned Firewalls and IDPS properly. Now I know:
> Aaj maine Firewalls aur IDPS sahi se seekh liya. Ab mujhe pata hai:

* Firewall is the gatekeeper between safe network and unsafe internet
> Firewall safe network aur unsafe internet ke darmayan guard hai

* Packet Filtering Firewall only checks IP and Port (basic)
> Packet Filtering Firewall sirf IP aur Port check karti hai (basic)

* Stateful Firewall remembers connection history (advanced)
> Stateful Firewall connection history yaad rakhti hai (advanced)

* IDS detects and alerts (Passive)
> IDS dhoondti aur alert karti hai (Passive)

* IPS detects AND blocks (Active)
> IPS dhoondti bhi hai aur block bhi karti hai (Active)

* Hacker uses `-f` (fragmentation) to bypass basic firewalls
> Hacker basic firewalls ko bypass karne ke liye `-f` (fragmentation) use karta hai

* Deep Packet Inspection (DPI) checks inside data, stops fragmentation attack
> Deep Packet Inspection (DPI) andar ka data check karti hai, fragmentation attack rok deti hai

* Stealth Scanning: Hacker slows down to avoid IDPS detection
> Stealth Scanning: Hacker speed slow kar deta hai taake IDPS detect na kare

> Ab Firewalls aur IDPS ka poora game samajh aa gaya hai!
