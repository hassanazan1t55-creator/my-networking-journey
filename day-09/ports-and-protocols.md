# Day 9: Ports and Protocols (Computer Ke 65,535 Darwaze)

Today i am learning about Ports and Protocols. If IP address is the building location, then ports are the doors to enter that building.
> Aaj main Ports aur Protocols seekh raha hoon. Agar IP address building ka address hai, toh ports us building ke andar jaane ke darwaze hain.

A computer or server has 65,535 ports. Each port runs a specific type of service called a Protocol.
> Ek computer ya server ke andar kul 65,535 ports hote hain. Har port par ek khass kism ka kaam chal raha hota hai jise Protocol kehte hain.

---

## 1. What is the Real Purpose of Ports and Protocols?

When your computer is browsing, emailing, and downloading at the same time, it uses ports to know which data belongs to which app.
> Agar aapka computer ek hi waqt mein website bhi khol raha hai, email bhi bhej raha hai, aur file bhi download kar raha hai, toh computer ko kaise pata chalta hai ke kaun sa data kis app ka hai? Woh in ports ke zariye pehchanta hai.

---

## 2. The Hacker's Mindset: How to Attack Ports

A hacker's first step is always Port Scanning.
> Ek hacker jab target par hamla karna chahta hai, toh uska pehla kadam hota hai Port Scanning.

"IP address mil gaya, ab dekho ke kaun se ports open hain aur unke peeche kya chal raha hai!"
> Hacker sochega: "Building ka address (IP) mil gaya, ab check karo ke 65,535 darwazon mein se kaun sa darwaza khala (Open) hai aur uske peeche kaun sa software chal raha hai!"

---

## 3. The 4 Most Important and Famous Ports

### Port 80 - HTTP (Hypertext Transfer Protocol)

This is for regular websites. Data travels in plain text without any encryption.
> **Asli Kaam:** Yeh aam websites ko kholne ke liye hai. Data ko plain text (bina security ke) bhejta hai.

"If the website is running on Port 80, the data is unencrypted. I can sit on the network and see all data (passwords, emails) clearly."
> **Hacker's Mindset:** "Agar website Port 80 par chal rahi hai, toh data unencrypted hai. Main network par baith kar saara data (passwords, emails) saaf dekh sakta hoon."

Hackers perform Sniffing or Man-in-the-Middle (MITM) attacks here because there is no lock on the data.
> **Hacking Use:** Hackers yahan Sniffing ya Man-in-the-Middle (MITM) attack karte hain kyunki data par koi tala nahi hota.

---

### Port 443 - HTTPS (HTTP Secure)

This is for modern websites like Facebook and Banks. All data is encrypted and secure.
> **Asli Kaam:** Yeh modern websites (Facebook, Google, Banks) ke liye hai. Data Encrypt (code mein) jata hai. URL ke sath taala bana hota hai.

"This door is strong. I will have to downgrade its security to Port 80 or send the user a fake certificate."
> **Hacker's Mindset:** "Yeh darwaza mazboot hai. Mujhe pehle iski security ko down karke Port 80 par lana parega ya user ko fake certificate bhejna parega."

Hackers perform SSL Stripping to downgrade https:// to http:// to read raw passwords.
> **Hacking Use:** Hackers SSL Stripping karte hain taake https:// ko http:// mein badal kar raw passwords parh saken.

---

### Port 21 - FTP (File Transfer Protocol)

This is used to upload and download large files, software, or movies over the network.
> **Asli Kaam:** Yeh network par badi files, software, ya movies ko upload/download karne ke liye hai.

"If this port is open, check if the admin has set password 'admin123'. If yes, I will steal all files."
> **Hacker's Mindset:** "Agar yeh port open hai, toh check karo ke kya admin ne password 'admin123' rakha hai? Agar haan, toh main saari files chura loonga."

Hackers perform Brute Force Attack (trying random passwords) or run a direct exploit if an old software version is running.
> **Hacking Use:** Hackers yahan Brute Force Attack karte hain (andhadhund passwords try karna) ya agar purana software version chal raha ho toh direct exploit chala dete hain.
---

### Port 22 - SSH (Secure Shell)

This is used to remotely control another computer. It is fully secure and encrypted.
> **Asli Kaam:** Yeh kisi doosre computer ko door baith kar control karne (Terminal chalane) ke liye hai. Yeh fully secure aur encrypted hai.

"If I get access to Port 22, I will become the owner of that server. I will check if the server is updated or has any old vulnerability."
> **Hacker's Mindset:** "Agar mujhe Port 22 ka access mil gaya, toh main us server ka malik ban jaoonga. Main check karunga ke server updated hai ya koi purani vulnerability hai."

Hackers focus on this port because hacking it means full control of the system.
> **Hacking Use:** Hackers is port par bohot dhyan dete hain kyunki isko hack karne ka matlab hai poore system ka control haath mein aana.

---

## 4. Port States: Open, Closed, and Filtered

When we scan, ports show us 3 types of status. Each has a different meaning for a hacker:
> Jab hum scanning karte hain, toh ports 3 tarah ke status dikhate hain. Hacker ke liye in teenon ka matlab alag hota hai:

**1. Open (Khala)**
Door is open and an application is waiting. This is a green signal for the hacker.
> Darwaza khala hai aur peeche koi application request ka intezar kar rahi hai. Hacker ke liye yeh green signal hai.

**2. Closed (Band)**
Door is closed. But this tells the hacker that the machine is online.
> Darwaza band hai. Computer wahan request accept nahi kar raha. Lekin hacker ko is se yeh pata chal jata hai ke yeh machine zinda (online) hai.

**3. Filtered (Roka Hua)**
This is the biggest headache for a hacker. A firewall or security guard is blocking the packets.
> Yeh hacker ke liye sab se bada sir dard hai. Iska matlab hai ke beech mein koi Firewall ya security guard baitha hai jo aapke packet ko port tak pohanchne hi nahi de raha.

---

## 5. Defensive Mindset: How to Stay Safe

After understanding the hacker's mindset, how does a good security expert defend?
> Hacker ka dimaag samajhne ke baad, achha security expert isko secure kaise karta hai?

**Principle 1: Close Unused Ports**
Close all doors that are not in use.
> Jo darwaza istemal mein nahi hai, use hamesha band rakho. Agar company ko FTP ki zaroorat nahi, toh Port 21 hamesha band hona chahiye.

**Principle 2: Change Default Ports**
Change default ports to hide from automatic attacks.
> SSH ka asli darwaza Port 22 hai. Hackers Port 22 par automatic attack karte hain. Agar hum SSH ka port badal kar 52222 kar dein, toh hackers ko pata nahi chalega ke rasta kahan hai.

**Principle 3: Use Firewalls**
Use firewalls to allow only trusted IPs.
> Firewall laga kar filtered state set karo, taake sirf allowed IPs hi ports par baat kar sakein.

---

## 6. Elite Hacker Scanning Strategy (Two-Step Method)

A hacker never runs a deep scan on all 65,535 ports at once. It takes too long and the firewall catches it.
> Hacker kabhi bhi saare 65,535 ports par ek sath gehra scan nahi chalata. Kyunki zamane lag jayenge aur firewall pakar lega.

**Step 1: The Quick Ping**
First, a fast scan to see which ports are open (without checking version).
> Hacker pehle poore 65,535 ports par ek bohot tez scan bhejta hai (bina version check kiye). Sirf yeh dekhta hai ke kaun sa darwaza khala (Open) hai.

`nmap -p- target.com`

**Step 2: The Deep Focus**
Now the hacker only checks the versions of the open ports.
> Ab hacker ko pata hai ke baqi saare ports band hain. Woh sirf open ports ka version check karta hai.

`nmap -sV -p 80,443,31337 target.com`

---

## What I Learned and Solved Today (My Hacker Analysis)

Today I completely learned the concept of ports and protocols. Now I know:
> Aaj maine ports aur protocols ka poora concept seekh liya. Ab mujhe pata hai:

* 65,535 ports exist on every computer
* Port 80 (HTTP) is unsecure - data in plain text
* Port 443 (HTTPS) is secure - data encrypted
* Port 21 (FTP) is for file transfer
* Port 22 (SSH) is for remote control
* Ports can be Open, Closed, or Filtered
* Hackers use Two-Step Scanning: Quick ping first, then deep focus
* Defenders close unused ports, change default ports, and use firewalls

Now the fear of ports is also gone. Now I know which doors a hacker knocks on and how a defender locks them!
> Ab OSI layers ke baad ports ka bhi darr khatam ho gaya hai. Ab pata hai ke hacker kaun se darwaze par knock karta hai aur defender unhe kaise lock karta hai!
