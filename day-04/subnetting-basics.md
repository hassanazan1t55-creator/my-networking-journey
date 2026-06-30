# Day 4: Subnet Mask and CIDR Notation

Today i am learning the mathematical and practical logic behind Subnet Masks and CIDR notation.
> Aaj main subnet mask aur CIDR notation ka poora mathematical aur practical logic bilkul andar guss kar samajh raha hoon.

We know that an IP address has a Network ID and a Host ID, but the computer needs a way to know where the border is. It uses a Subnet Mask for this.
> IP address ke do hisse hote hain (Network ID aur Host ID), lekin computer ko kaise pata chalta hai ke border kahan par hai? Iske liye woh Subnet Mask ka istemal karta hai.

---

## 1. What is a Subnet Mask?
> Subnet Mask asal mein kya cheez hai?

The golden rule is very simple: wherever you see 1 (or 255) in binary, that part belongs to the Network. Wherever you see 0, that part belongs to the Host.
> Asli rule yeh hai ke subnet mask mein jahan jahan Binary mein 1 (ya decimal mein 255) aayega, woh hissa Network ka hoga. Aur jahan jahan 0 aayega, woh hissa Host ka hoga.

* **The Identity Card Template:** Think of it like a plastic template placed over an ID card that only highlights specific boxes. Subnet mask is that filter that separates network from host.
> **ID Card Sancha:** Yeh IP address ke upar rakha hua ek plastic ka sancha hai jo network aur host ko alag alag dikhata hai.

* **The Postal Zip Code:** Just like a zip code (e.g., 54000) tells the post office which city a letter belongs to, the subnet mask tells the router where the city border ends.
> **Postal Zip Code:** Subnet mask internet ka wahi zip-code rule book hai jo router ko batata hai ke shehar (network) ka border kahan khatam ho raha hai.

---

## 2. AND Gate Operation (How Computers Think)
> AND Gate ka operation aur computer ka dimaag

Computers use a mathematical calculation called an AND Gate to compare the IP address and the Subnet Mask.
> Computer jab IP address aur Subnet Mask ko dekhta hai, toh woh unke darmiyan ek math calculation karta hai jise AND Gate kehte hain.



### The AND Gate Rule:
* 1 and 1 = 1
* 1 and 0 = 0
* 0 and 0 = 0
*(The result is 1 ONLY when both sides are 1, otherwise it is always 0).*

### Real-Life Example (The Double-Key Vault)
Think of a bank vault that only opens when both managers turn their keys at the same time (1 and 1 = Open). If only one turns the key (1 and 0), it stays locked (0).
> Yeh bank ka ek aisa locker hai jo sirf tabhi khulega jab dono manager apni chabi ek sath ghumayein ge.

### The Calculation:
* **IP Address (192.168.1.5):** `11000000 . 10101000 . 00000001 . 00000101`
* **Subnet Mask (255.255.255.0):** `11111111 . 11111111 . 11111111 . 00000000`
* **AND Result:** `11000000 . 10101000 . 00000001 . 00000000`

When we convert this back to decimal, it becomes **`192.168.1.0`**. This is the official Network Address!
> Is result ko decimal mein badlein toh `192.168.1.0` banta hai, jo is network ka asli naam hai.

---

## 3. What is CIDR Notation? (/24, /16, /8)
> CIDR notation kya hai aur iska short-cut logic

Writing `255.255.255.0` repeatedly is too long for advanced tools. Scientists created a short-cut called CIDR (Classless Inter-Domain Routing).
> Advanced tools mein baar baar lamba subnet mask likhna mushkil lagta tha, isliye scientists ne ek short-cut nikala jise CIDR kehte hain.

The number after the slash `/` simply tells how many bits are ON (set to 1) from the start.
> IP ke aage jo slash `/` lagakar number likha hota hai, woh sirf yeh batata hai ke shuru se lekar kitne bits ON (yani 1) hain.

* **`/24` meaning:** First 24 bits are ON ($8+8+8 = 24$ bits). This means `255.255.255.0`.
> Pehle teen octets poore 1 hain, yaani `255.255.255.0`.

* **`/16` meaning:** First 16 bits are ON ($8+8 = 16$ bits). This means `255.255.0.0`.
> Pehle do octets poore 1 hain, yaani `255.255.0.0`.

* **`/8` meaning:** First 8 bits are ON. This means `255.0.0.0`.
> Shuru ka sirf pehla octet poora 1 hai, yaani `255.0.0.0`.

---
## What I Learned and Solved Today (My Practical Task)

I performed a practical task on an IP found during a target scan.
> Aaj maine hacking target scan scenario par ek practical test solve kiya aur concepts clear kiye.

### The Scenario:
Target IP found: **`172.16.10.5/16`**

* **My Analysis for Subnet Mask:** The `/16` short-cut means the first 16 bits are ON. So, the full decimal Subnet Mask is **`255.255.0.0`**.
> `/16` ka matlab shuru ke 16 bits ON hain, yaani poora decimal subnet mask `255.255.0.0` banta hai.

* **My Analysis for Network ID:** According to this mask, the first two octets represent the network. So, the Network ID is **`172.16`**.
> Is subnet mask ke mutabiq pehle do octets network ke hain, toh Network ID `172.16` banta hai.

* **IP Class:** Since the first octet is 172 (which falls between 128 and 191), this belongs to **Class B**.
> Kyunki pehla number 172 hai, isliye yeh Class B ka IP address hai.
