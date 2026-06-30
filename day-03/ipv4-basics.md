# Day 3: IPv4 Architecture and IP Classes

Today i am learning how IP addresses actually work and how computers are grouped into different networks.
> Aaj main seekh raha hoon ke IP address buniyaadi taur par kaise kaam karta hai aur computers ko mukhtalif networks mein kaise baanta jata hai.

Every computer on the internet has a unique identity called an IP address.
> Internet par majood har computer ki ek makhsoos pehchan hoti hai jise IP address kehte hain.

---

## 1. The 32-Bit Structure of IPv4
> IPv4 ka 32-Bit buniyaadi dhaancha

When we see an IP like `192.168.1.1`, the computer sees a long chain of 32 bits (0 and 1).
> Jab hum `192.168.1.1` jaisa IP address dekhte hain, toh computer use 32 bits (0 aur 1) ka ek lamba silsila dekhta hai.



* **Total Bits:** IPv4 has exactly 32 bits.
> **Total Bits:** IPv4 address mein kul 32 bits hote hain.

* **4 Octets:** These 32 bits are divided into 4 equal parts. Each part has 8 bits ($8 \text{ bits} \times 4 \text{ parts} = 32 \text{ bits}$).
> **4 Octets:** In 32 bits ko 4 barabar hisson mein banta jata hai. Har hissay mein 8 bits hote hain jise octet kehte hain.

* **Dots (.):** Dots are used to separate these four octets so humans can read it easily.
> **Dots (.):** In charo octets ko aapas mein alag karne ke liye darmayan mein dot lagaya jata hai.

---

## 2. Network ID vs Host ID Logic
> Network ID aur Host ID ka asli farq

Every IP address has two main parts. This is the most important rule in networking.
> Kisi bhi IP address ke do buniyaadi hisse hote hain, aur yeh networking ka sab se bada usool hai.



* **Network ID:** This part tells which neighborhood or group the computer belongs to.
> **Network ID:** IP address ka woh hissa jo batata hai ke computer kis network ya mohallay mein baitha hai.

* **Host ID:** This part tells the specific house number of that device inside the network.
> **Host ID:** Yeh batata hai ke us network ke andar is makhsoos device (computer/mobile) ka apna number kya hai.

**The Connection Rule:** If two devices want to talk directly without a router, their Network ID must be completely SAME, but their Host ID must be DIFFERENT.
> **Connection Rule:** Agar do devices ko bina router ke direct baat karni hai, toh unka Network ID bilkul same hona chahiye aur Host ID lazmi alag hona chahiye.

---

## 3. IP Classes Breakdown
> IP classes aur unki ranges ka hisab

IP addresses are divided into different classes according to network size. We only check the first number (First Octet) to find the class.
> Network ke size ke mutabiq IPs ko classes mein banta gaya hai. Kisi bhi IP ka sirf pehla number dekh kar class ka pata chalta hai.

### Class A (The Mega Network)
* **Range:** 1 to 126
* **Architecture:** Network . Host . Host . Host
> **Logic:** Ismein pehla 1 octet Network ka hota hai aur baqi 3 Host ke hote hain. Iske ek network mein karoron ($16,777,214$) computers lag sakte hain. NASA ya Google jaise bade networks ise use karte hain.

### Class B (The Medium Network)
* **Range:** 128 to 191
* **Architecture:** Network . Network . Host . Host
> **Logic:** Iske pehle 2 octets Network ke hote hain aur baqi 2 Host ke. Yeh badi universities ya medium companies mein use hota hai.

### Class C (The Small Local Network)
* **Range:** 192 to 223
* **Architecture:** Network . Network . Network . Host
> **Logic:** Iske pehle 3 octets Network ke hote hain aur aakhri 1 octet Host ka hota hai. Hamare gharon ke Wi-Fi routers isi class mein aate hain. Ismein ek network mein sirf 254 computers lag sakte hain.

*(Note: 127 is missing because 127.0.0.0 is reserved for Loopback/Localhost to check our own computer).*

---

## 4. What is a Switch?
> Switch kya hota hai aur yeh kya kaam karta hai

A Switch is a physical hardware box with many ports where network cables are connected. It connects devices within the same local network (LAN).
> Switch ek physical hardware box hota hai jismein bohot saare ports hote hain jahan cables lagti hain. Iska kaam ek hi local network ke computers ko aapas mein jorna hai.



* **Switch Brain (MAC Address Table):** The switch reads the physical MAC address of every connected device and makes a table inside its memory.
> **Switch ka Dimaag:** Switch har computer ka physical hardware address (MAC Address) parh kar apne dimaag mein ek table bana leta hai.

* **Secure Delivery:** When Computer A sends data to Computer B, the switch checks its table and sends the data only to Computer B's port. It does not leak data to other computers.
> **Secure Delivery:** Jab ek PC doosre ko data bhejta hai, toh switch table dekh kar data sirf us makhsoos computer ke port par bhejta hai, baqi kisi ko nahi dikhata.

---

## What I Messed Up Today (My Mistakes and Learning)

Today i did a few calculation mistakes during the tasks but learned the deep logic.
> Aaj maine tasks ke darmayan calculation mein thodi si chook ki par unse bohot deep concepts seekhe.

### My First Mistake: Network Connection Logic
Initially, i thought that if two computers have different IP addresses, they cannot talk directly.
> Pehle mujhe laga ke agar do computers ki IP address alag hain toh woh aapas mein baat nahi kar sakte.

* **Correction:** My AI friend explained that their whole IP should not be same, but their **Network ID** must be same. For example, `192.168.1.10` and `192.168.1.20` have the exact same Network ID (`192.168.1`), so they can talk directly.
> **Sahi Logic:** Poori IP same nahi honi chahiye par unka Network ID same hona chahiye. Agar Network ID same hai toh woh bilkul direct baat kar sakte hain.

### My Second Mistake: Class Ranges
For IPs starting with 172 (like `172.16.5.10`), i guessed it was Class A.
> Maine `172.16.5.10` ko Class A samajh liya tha.

* **Correction:** I checked the rules again. Class A range is 1 to 126, and Class B range is 128 to 191. Since 172 comes between 128 and 191, it is **Class B**. 
> **Sahi Logic:** 172 Class B ki range mein aata hai. Aur Class B ke rule ke mutabiq iske pehle do octets (`172.16`) iska Network ID hain.

### The Final Test Success
I successfully answered the secret loopback address question. If my PC is not connected to the internet and i want to test my network chip, i will ping **`127.0.0.1`**. This packet stays inside the computer and never goes out on the cable.
> Maine loopback address ka task bilkul sahi clear kiya. Apne hi computer ki networking check karne ke liye hum **`127.0.0.1`** ko ping karte hain aur yeh packet wire par bahar nahi jata.
