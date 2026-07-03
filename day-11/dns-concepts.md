# Day 11: DNS (Domain Name System)

Today i am learning about DNS, which translates human-friendly domain names into computer-friendly IP addresses.
> Aaj main DNS seekh raha hoon, jo insanon ke parhne wale naamon (Domain Names) ko computers ke samajhne wale numbers (IP Addresses) mein badalta hai.

Computers only understand numbers (IP addresses like 142.250.181.238), but humans cannot remember IPs for every website. So we remember names like google.com or facebook.com.
> Computers sirf numbers (IP Addresses) samajhte hain, lekin insanon ke liye har website ka IP yaad rakhna namumkin hai. Isliye hum yaad rakhte hain google.com ya facebook.com.

DNS is like a phonebook that matches domain names with their IP addresses.
> DNS bilkul phonebook ki tarah hai jo domain names ko unki IP addresses se match karta hai.

---

## 1. How DNS Works? (The Query Process)

When you type google.com in your browser, your computer performs these steps very quickly:
> Jab aap browser par google.com likhte hain, toh computer background mein yeh steps bohot tezi se karta hai:

**1. DNS Cache Check**
Your computer first checks its own memory (Cache) to see if it has visited google before. If the IP is already saved, the website opens instantly.
> Aapka computer pehle apne dimaag (Cache memory) mein check karta hai ke kya hum pehle google par gae the? Agar IP pehle se bachi hui hai, toh website foran khul jati hai.

**2. DNS Resolver (Your ISP)**
If not found in cache, the request goes to your Internet Service Provider (like PTCL, Nayatel, StormFiber) called a Resolver.
> Agar cache mein nahi milti, toh request aapke internet provider (jaise PTCL, Nayatel, StormFiber) ke paas jati hai jise Resolver kehte hain.

**3. The Root Server**
If the ISP also doesn't know, it goes to the world's biggest Root Server (.) and asks: "Where is google.com?" The Root Server says: "I don't know completely, but go to the .com server."
> Agar ISP ko bhi nahi pata, toh woh dunya ke sab se bare Root Server (.) ke paas jata hai aur bolta hai ke bhai google.com kahan hai? Root server bolta hai: "Mujhe poora toh nahi pata, lekin tum .com wale server ke paas jao."

**4. TLD Server (Top-Level Domain)**
The .com server says: "Yes, google is registered with me, go to its main server (Authoritative Name Server)."
> .com wala server kehta hai: "Haan, google ka address mere paas register hai, tum is ke main server (Authoritative Name Server) ke paas jao."

**5. Authoritative Name Server**
This is the final server that gives the exact and correct IP address (142.250.181.238) to your computer, and the website opens!
> Yeh aakhri server hota hai jo bilkul sahi aur pakki IP address (142.250.181.238) nikal kar aapke computer ko de deta hai, aur website khul jati hai!

---

## 2. Hacker's Mindset vs Defensive Mode

DNS is the backbone of the entire internet. If a hacker controls DNS, they can change the path of the whole internet!
> DNS pure internet ki rereg (backbone) hai. Agar hacker DNS ko control kar le, toh woh poore internet ka rasta badal sakta hai!

### Hacker's Attack: DNS Spoofing / Cache Poisoning (Rasta Badalna)

The hacker thinks: "When a user types mybank.com, their computer will ask the local DNS cache or router for the IP. If I secretly change the bank's real IP to my fake hacker server's IP in their computer or router's DNS table, what will happen?"
> Hacker sochega: "User jab bank ki website mybank.com likhega, toh uska computer pehle local DNS cache ya router se IP poochay ga. Agar main chupke se us ke computer ya router ke DNS table mein bank ki asli IP badal kar apne nakli hacker server ki IP daal doon, toh kya hoga?"

**Hacking Use:** The user types the correct name (mybank.com), but due to the fake DNS entry, they are sent directly to the hacker's fake banking page. The user won't suspect anything because the URL looks exactly correct, and when they login, their password goes straight to the hacker!
> User apne browser par bilkul sahi naam (mybank.com) likhega, lekin DNS ki galat entry ki wajah se woh direct hacker ke banaye hue nakli banking page par pohanch jayega. User ko shak bhi nahi hoga kyunki URL bilkul sahi dikh raha hoga, aur jaise hi woh login karega, password hacker ke paas!

### Defender's Counter: DNSSEC and Secure DNS

How does an elite network defender stop this dangerous theft?
> Ab ek elite network defender is khatarnak chori ko kaise rokta hai?

**1. DNSSEC (DNS Security Extensions)**
The defender adds digital signatures (cryptographic verification) to DNS packets. When the computer receives the DNS response, it checks whether the signature is from the real server or if a hacker changed it in between. If the signature doesn't match, the computer doesn't go to that IP.
> Defender DNS ke packets par digital signatures (cryptographic verification) laga deta hai. Jab computer ke paas DNS ka jawab aata hai, toh woh pehle check karta hai ke yeh signature asli server ka hai ya kisi hacker ne beech mein rasta badla hai. Agar signature match nahi hota, toh computer us IP par nahi jata.

**2. Flush DNS (Clear Cache)**
If there is any suspicion that the cache has been poisoned, a command is run on the terminal to clear all old fake data:
> Agar kabhi shak ho ke cache mein dhandli hui hai, toh terminal par command chalayi jati hai taake purana nakli data saaf ho jaye:

`ipconfig /flushdns`

---

## 3. Important DNS Records (Hacker's Favorite)

DNS has a registry with different types of entries called DNS Records. A hacker checks these records deeply when researching a company.
> DNS ke paas ek register hota hai jahan alag alag kism ki entries hoti hain, jinhein DNS Records kehte hain. Ek hacker jab kisi company par research karta hai, toh woh in records ko deeply check karta hai.

**A Record (Address Record)**
This connects a domain name to an IPv4 address (e.g., google.com → 142.250.181.238).
> Yeh kisi domain name ko IPv4 address se jorhta hai (jaise google.com → 142.250.181.238).

**AAAA Record**
This connects a domain name to an IPv6 address.
> Yeh domain name ko naye IPv6 address se jorhta hai.

**MX Record (Mail Exchange)**
This tells where the company's all emails are going. [Hacker's Favorite!]
> Yeh batata hai ke is company ke saare emails kis server par ja rahe hain.

**Hacker's Vision:** If a hacker wants to send phishing emails to company employees, they check the MX record to find the email server and see if it's old or weak.
> Agar hacker ko company ke employees ko phishing emails bhejni hain, toh woh MX record se unke email server ka pata lagata hai aur check karta hai ke kya unka email system purana hai ya kamzor hai.

**TXT Record (Text Record)**
This contains security settings (like SPF or DKIM rules) that tell who can send emails on behalf of the company and who cannot.
> Ismein company ki mazeed security setting likhi hoti hai (jaise SPF ya DKIM rules) jo batati hain ke kaun unke naam par email bhej sakta hai aur kaun nahi.

---

## What I Learned and Solved Today (My Hacker Analysis)

Today I completely learned the DNS query process, DNS records, and both attack and defense perspectives of DNS.
> Aaj maine DNS query process, DNS records, aur DNS ke attack aur defense dono angles ko deeply samajh liya.

### My Key Learnings:

* DNS translates human-readable domain names to IP addresses like a phonebook
> DNS phonebook ki tarah domain names ko IP addresses mein translate karta hai

* DNS Query Process: Cache → Resolver → Root Server → TLD Server → Authoritative Server
> DNS Query Process: Cache → Resolver → Root Server → TLD Server → Authoritative Server

* DNS Spoofing / Cache Poisoning: Hacker changes DNS records to redirect users to fake sites
> DNS Spoofing / Cache Poisoning: Hacker DNS records badal kar users ko nakli sites par bhejta hai

* DNSSEC: Defender adds digital signatures to DNS packets to verify authenticity
> DNSSEC: Defender DNS packets par digital signatures laga kar authenticity check karta hai

* Flush DNS: `ipconfig /flushdns` command clears fake cache entries
> Flush DNS: `ipconfig /flushdns` command nakli cache entries saaf karti hai

* A, AAAA, MX, TXT records are important for both attackers and defenders
> A, AAAA, MX, TXT records attackers aur defenders dono ke liye important hain

> Ab DNS ka poora game samajh aa gaya hai. Pata hai ke hacker kaise DNS ko target karta hai aur defender kaise secure karta hai!
