# Day 13: Wi-Fi Networking (802.11 Standards)

Today i am learning about Wi-Fi networking, which is the wireless technology that connects devices without cables.
> Aaj main Wi-Fi networking seekh raha hoon, jo bina taron ke devices ko internet se jorti hai.

Until now, we discussed computers connected through wires (cables). But today, almost every home and office uses internet through the air, which we call Wi-Fi. In networking, Wi-Fi's technical name is IEEE 802.11.
> Abhi tak humne computers ko wires (cables) ke zariye jura hua parha. Lekin aaj kal har ghar aur office mein internet hawa ke zariye chalta hai, jise Wi-Fi kehte hain. Networking ki dunya mein Wi-Fi ka asli naam IEEE 802.11 hai.

For both hackers and defenders, understanding data flowing through the air is crucial, because to touch wires you need to enter the building physically, but Wi-Fi signals travel outside the building to the streets!
> Hacker aur defender dono ke liye hawa mein behte hue data ko samajhna bohot zaroori hai, kyunki wires ko hath lagane ke liye aapko building ke andar ghusna parta hai, lekin Wi-Fi ke signals building se baher road tak ja rahe hote hain!

---

## 1. How Wi-Fi Works? (SSID, BSSID & Channels)

When you turn on Wi-Fi on your mobile, you see nearby network names. The technical story behind them is:
> Jab aap apne mobile par Wi-Fi on karte ho, toh aapko aaju-baju ke networks ke naam dikhte hain. Inke peeche technical kahani yeh hai:

**SSID (Service Set Identifier)**
This is simply your Wi-Fi's Name (e.g., "PTCL-BB" or "Home-WiFi").
> Yeh simple aapke Wi-Fi ka Naam hota hai (jaise: "PTCL-BB" ya "Home-WiFi").

**BSSID (Basic Service Set Identifier)**
This is the real MAC Address of the Router/Access Point that is broadcasting signals. The name (SSID) can be changed, but the BSSID (MAC) is fixed.
> Yeh us Router/Access Point ka asli MAC Address hota hai jo signals phenk raha hai. Naam (SSID) badla ja sakta hai, lekin BSSID (MAC) fix hota hai.

**Frequencies & Channels (Paths)**
Wi-Fi generally runs on two frequencies:
> Wi-Fi aam taur par do frequencies par chalta hai:

**2.4 GHz:** This goes far but has slightly slower speed. It has channels 1 to 11.
> Yeh door tak jata hai lekin speed thori kam hoti hai. Ismein 1 se 11 tak channels (raste) hote hain.

**5 GHz:** This doesn't go as far but has rocket-fast speed.
> Yeh paas tak jata hai lekin speed ek dum rocket hoti hai.

---

## 2. Wi-Fi Security Walls (WPA2 vs WPA3)

Since data is traveling through the air, anyone can catch it. So it's essential to lock (Encrypt) the data:
> Hawa mein data ja raha hai, toh koi bhi use hawa se catch kar sakta hai. Isliye data ko tala (Encryption) lagana zaroori hai:

**WPA2 (Pre-Shared Key)**
This has been used in almost every home for the last 15-20 years. When you enter the password, the router and your mobile perform a 4-Way Handshake (they cryptographically shake hands and confirm the password is correct).
> Yeh pichle 15-20 saal se har ghar mein chal raha hai. Iska asool yeh hai ke jab aap password dalte ho, toh router aur aapke mobile ke darmayan ek 4-Way Handshake hota hai (yani dono aapas mein cryptographic tareeqay se hath milate hain aur confirm karte hain ke password sahi hai).

**WPA3**
This is the newest and most advanced standard. Security has been tightened further to eliminate the weaknesses of old WPA2.
> Yeh sab se naya aur advanced standard hai. Ismein security ko mazeed tight kiya gaya hai taake purane WPA2 ki kamzoriyon ko khatam kiya ja sake.

---

## 3. Hacker's Mindset vs Defensive Mode

Wi-Fi is the most fun target for hackers because they don't need to enter the target's building — they can scan from their car outside!
> Hacker ke liye Wi-Fi sab se mazedaar target hota hai kyunki use target ke ghar ya office ke andar nahi jana parta, woh baher gari mein baith kar bhi scan kar sakta hai.

### Hacker's Attack: The Deauthentication Attack

Imagine a user is connected to the router and using the internet.
> Maan lo ek user router se connect hokar internet chala raha hai.

**Hacker's Step:** The hacker puts their Wi-Fi card into Monitor Mode (a mode that captures all packets from the air). They send a fake packet called a Deauth Packet into the air. This packet tells the router "Disconnect the user" and tells the user "Disconnect from the router".
> Hacker apne wifi card ko Monitor Mode (hawa se saare packets pakarne wala mode) par dalta hai. Woh hawa mein ek fake packet phenkta hai jise Deauth Packet kehte hain. Yeh packet router ko kehta hai ke "User ko disconnect karo" aur user ko kehta hai ke "Router se hat jao".

**Result:** The user's internet immediately stops and their mobile automatically tries to reconnect to the router. When it reconnects, the same 4-Way Handshake happens again. The hacker captures (records) that handshake from the air and later tries to crack it.
> User ka internet foran band ho jata hai aur uska mobile dobara automatic router se connect hone ki koshish karta hai. Jab woh dobara connect hota hai, toh unke darmayan wahi 4-Way Handshake dobara hota hai. Hacker us handshake ko hawa mein capture (record) kar leta hai aur baad mein usko crack karne ki koshish karta hai.

### Defender's Counter: Hide SSID & MAC Filtering

What tricks does a network defender use to protect against this?
> Ek network defender is se bachne ke liye kya chalaki karta hai?

**Hide SSID:** The admin goes into the router settings and hides the Wi-Fi name. Now normal people won't see the Wi-Fi name unless they know the exact name.
> Admin router ki setting mein ja kar wifi ka naam chhupa deta hai. Ab aam logon ko wifi ka naam show hi nahi hoga, jab tak unhein sahi naam na pata ho.

**MAC Filtering:** The admin adds a rule in the router: "Only allow these 4 mobiles' MAC addresses from my house to use the internet. Block anyone else."
> Admin router mein rule laga deta hai ke "Sirf mere ghar ke in 4 mobiles ke MAC addresses ko internet do, baqi koi bhi aaye toh use block kar do."

---

## 4. The 4-Way Handshake Explained

When you enter your Wi-Fi password and press connect, the mobile doesn't send the password directly to the router (because if it did, anyone in the air could catch it).
> Jab aap mobile par password daal kar connect dabate ho, toh mobile router ko direct password nahi bhejta (kyunki agar direct bhejega toh hawa mein koi bhi chor pakar lega).

Instead, 4 messages happen in the background:
> Iske bajaye background mein 4 Messages chalte hain:

**Message 1:** Router sends a random code (ANonce) to the mobile.
> Router ek random code (ANonce) mobile ko bhejta hai.

**Message 2:** Mobile combines its own random code (SNonce) + password to create a unique proof (MIC) and sends it back. (This is what hackers capture from the air!)
> Mobile apna random code (SNonce) aur password ko mila kar ek unique proof (MIC) banata hai aur wapas bhejta hai. (Hacker isi ko hawa mein pakarta hai!)

**Message 3:** Router checks the proof and says "Proof is correct, here is the key."
> Router proof check karta hai aur kehta hai "Proof sahi hai, yeh lo chaabi."

**Message 4:** Mobile says "Done! I am now starting encryption."
> Mobile kehta hai "Done! Main ab encryption shuru kar raha hoon."

---

## 5. Wi-Fi MAC Spoofing Bypass — Full Logic

Imagine you are outside a company. Their Wi-Fi is Hidden and they have MAC Filtering enabled (only the owner's laptop with MAC AA:BB:CC:DD:EE:FF can connect).
> Maan lo aap ek company ke baher baithe ho. Unka Wi-Fi Hidden hai aur upar se unhone MAC Filtering lagayi hui hai (yaani sirf company ke maalik ka laptop, jiska MAC address AA:BB:CC:DD:EE:FF hai, connect ho sakta hai).

Your laptop is outside and your MAC address is 11:22:33:44:55:66. If you try to connect, the router will reject you because your MAC isn't on the allowed list (Whitelist).
> Aapka laptop abhi baher hai aur aapka MAC address 11:22:33:44:55:66 hai. Agar aap connect hone ki koshish karoge, toh router aapko dhakke maar kar baher nikal dega kyunki aapka MAC address uski ijazat wali list (Whitelist) mein nahi hai.

### Step 1: Sniff the Air (Packet Sniffing)

The hacker puts their Wi-Fi card into Monitor Mode. Monitor Mode means your Wi-Fi card captures every packet floating in the air and displays it on the screen.
> Hacker apne laptop ka Wi-Fi card Monitor Mode par dalta hai. Monitor mode ka matlab hai ke aapka Wi-Fi card hawa mein ghoomte hue har packet ko pakar kar screen par dikhana shuru kar deta hai.

The hacker sees a computer connected to the router sending data. That computer's MAC address appears: **AA:BB:CC:DD:EE:FF**.
> Hacker screen par dekhta hai ke ek computer router ke sath connect hai aur lagatar data bhej raha hai. Us computer ka MAC address dikh jata hai: **AA:BB:CC:DD:EE:FF**.

### Step 2: Change Identity (MAC Spoofing)

Now the hacker has the enemy's real authorized MAC address. The hacker goes to the terminal and runs a simple command (using `macchanger` or `ifconfig` on Linux) and temporarily changes their laptop's real MAC address to the employee's: **AA:BB:CC:DD:EE:FF**.
> Ab hacker ko dushman ka asli aur ijazat wala MAC address mil gaya. Hacker apne terminal par ja kar ek simple command chalata hai (Linux mein `macchanger` ya `ifconfig` ke zariye) aur apne laptop ka asli MAC address badal kar temporary taur par wahi kar leta hai jo us employee ka tha: **AA:BB:CC:DD:EE:FF**.

### Step 3: Direct Entry (Firewall Bypass)

Now when the hacker sends a connection request to the router, the router thinks this is the same trusted employee that connects every day. The router silently lets them in and the firewall is bypassed!
> Ab jab hacker router ko connect karne ki request bhejta hai, toh router samajhta hai ke yeh wahi purana bharosay mand employee hai jo roz connect hota hai. Router chupke se use network ke andar aane deta hai aur firewall bypass ho jati hai!

---

## 6. Important: MAC Spoofing Does NOT Bypass Password

**Important Technical Fact:** MAC Spoofing does NOT bypass the Wi-Fi password. You must still enter the correct password to complete the 4-Way Handshake.
> **Ahem Technical Fact:** MAC Spoofing karne se Wi-Fi ka password bypass NAHI hota. Aapko password phir bhi lazmi dena parega.

The router has TWO separate security walls:
> Router ke andar security ki do alag alag deewarein hoti hain:

**Wall 1: Wi-Fi Encryption (The Password Gate)**
This is the first wall. To complete the 4-Way Handshake, you MUST have the Wi-Fi password. Without it, your laptop can't even finish the handshake.
> Yeh sab se pehli aur asli deewar hai. 4-Way Handshake karne ke liye aapke paas Wi-Fi password hona lazmi hai.

**Wall 2: MAC Filtering (The Guard List)**
This is the second wall. After you enter the correct password and complete the handshake, the router checks: "Is this MAC address allowed?"
> Yeh doosri deewar hai. Sahi password dene aur handshake complete karne ke baad router check karta hai: "Kya is MAC address ko andar aane ki ijazat hai?"

**Conclusion:**
- Correct Password + Wrong MAC  Blocked
- No Password + Spoofed MAC Blocked (Handshake fails)
- Correct Password + Spoofed MAC Firewall Bypass!

---

## What I Learned and Solved Today (My Hacker Analysis)

Today I completely learned Wi-Fi networking, SSID/BSSID, frequencies, WPA2/WPA3, 4-Way Handshake, MAC Spoofing, and both attack and defense perspectives.
> Aaj maine Wi-Fi networking, SSID/BSSID, frequencies, WPA2/WPA3, 4-Way Handshake, MAC Spoofing, aur Wi-Fi ke attack aur defense dono angles ko deeply samajh liya.

### My Key Learnings:

* Wi-Fi is technically called IEEE 802.11, broadcasting through radio waves
> Wi-Fi ka asli naam IEEE 802.11 hai, jo radio waves ke zariye broadcast hota hai

* SSID is the network name, BSSID is the router's MAC address
> SSID network ka naam hai, BSSID router ka MAC address hai

* 2.4 GHz goes far but slower, 5 GHz is faster but shorter range
> 2.4 GHz door tak jaata hai lekin slow hai, 5 GHz tez hai lekin range kam hai

* WPA2 uses 4-Way Handshake for authentication, WPA3 is more secure
> WPA2 4-Way Handshake use karta hai authentication ke liye, WPA3 zyada secure hai

* Deauthentication Attack disconnects users to capture handshake for cracking
> Deauthentication Attack users ko disconnect kar ke handshake capture karta hai

* MAC Spoofing bypasses MAC Filtering but requires correct password first
> MAC Spoofing MAC Filtering ko bypass karta hai lekin pehle sahi password zaroori hai

> Ab Wi-Fi ka poora game samajh aa gaya hai. Pata hai ke hacker kaise Wi-Fi ko target karta hai aur defender kaise secure karta hai!
