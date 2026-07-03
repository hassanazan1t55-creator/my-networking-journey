# Day 13: Wi-Fi Networking

Today i am learning about Wi-Fi, which is internet without wires.
> Aaj main Wi-Fi seekh raha hoon, jo bina taron ke internet hai.

Before this, we only talked about computers with wires. But now every home and office uses air internet. We call it Wi-Fi. In technical language its name is IEEE 802.11.
> Abhi tak humne computers ko wires se jura hua parha. Lekin aaj kal har ghar mein hawa wala internet hai. Use Wi-Fi kehte hain. Technical language mein iska naam IEEE 802.11 hai.

For hackers and defenders, Wi-Fi is very important because wires need you to go inside building. But Wi-Fi signals go outside to the road!
> Hacker aur defender dono ke liye Wi-Fi bohot important hai kyunki wires ko hath lagane ke liye building ke andar jana parta hai. Lekin Wi-Fi ke signals building se baher road tak jaate hain!

---

## 1. How Wi-Fi Works? (SSID, BSSID and Channels)

When you turn on Wi-Fi on your phone, you see network names. Behind them is this:
> Jab aap mobile par Wi-Fi on karte ho, toh aapko network ke naam dikhte hain. Inke peeche yeh hai:

**SSID (Service Set Identifier)**
This is your Wi-Fi name (like "PTCL-BB" or "Home-WiFi").
> Yeh aapke Wi-Fi ka naam hai (jaise "PTCL-BB" ya "Home-WiFi").

**BSSID (Basic Service Set Identifier)**
This is the real MAC address of your Router. The name can change, but BSSID (MAC) stays same.
> Yeh Router ka asli MAC address hai. Naam badal sakte ho, lekin BSSID (MAC) fix hai.

**Frequencies and Channels**
Wi-Fi works on two frequencies:
> Wi-Fi do frequencies par chalta hai:

**2.4 GHz:** Goes far but speed is less. Has channels 1 to 11.
> Door tak jaata hai lekin speed kam hai. Ismein 1 se 11 channels hain.

**5 GHz:** Doesn't go far but speed is very fast.
> Paas tak jaata hai lekin speed bohot tez hai.

---

## 2. Wi-Fi Security (WPA2 vs WPA3)

Because data is in the air, anyone can catch it. So we need to lock (Encrypt) the data.
> Hawa mein data hai, toh koi bhi pakar sakta hai. Isliye data ko tala (Encryption) lagana zaroori hai.

**WPA2 (Pre-Shared Key)**
This is used in every home for last 15-20 years. When you put password, router and your phone do a 4-Way Handshake to check if password is correct.
> Yeh pichle 15-20 saal se har ghar mein chal raha hai. Jab aap password dalte ho, toh router aur mobile 4-Way Handshake karte hain ke password sahi hai ya nahi.

**WPA3**
This is new and more secure. It fixes the weaknesses of old WPA2.
> Yeh naya aur zyada secure hai. Purane WPA2 ki kamzoriyan ismein khatam kar di gayi hain.

---

## 3. Hacker's Mindset vs Defender

For hackers, Wi-Fi is the best target because they don't need to go inside. They can sit in car outside and hack!
> Hacker ke liye Wi-Fi sab se acha target hai kyunki use andar nahi jana parta. Woh baher gari mein baith kar hack kar sakta hai!

### Hacker Attack: Deauthentication Attack

Imagine a user is connected to Wi-Fi and using internet.
> Maan lo ek user Wi-Fi se connect hai aur internet chala raha hai.

**Hacker does this:** Hacker puts their Wi-Fi card in Monitor Mode (this mode catches all packets from air). Then they send a fake packet called Deauth Packet. This packet tells router "Remove the user" and tells user "Leave the router".
> Hacker apna Wi-Fi card Monitor Mode mein dalta hai (yeh mode hawa se saare packets pakarta hai). Phir woh ek fake packet bhejta hai jise Deauth Packet kehte hain. Yeh packet router ko kehta hai "User ko hatao" aur user ko kehta hai "Router se hat jao".

**Result:** User's internet stops and their phone tries to reconnect. When it reconnects, the 4-Way Handshake happens again. Hacker captures that handshake from air and later tries to crack it.
> User ka internet band ho jata hai aur phone dobara connect hone ki koshish karta hai. Jab woh connect hota hai, toh 4-Way Handshake dobara hota hai. Hacker us handshake ko hawa se capture kar leta hai aur baad mein crack karne ki koshish karta hai.

### Defender Tricks: Hide SSID and MAC Filtering

How does a defender protect?
> Defender kaise bachta hai?

**Hide SSID:** Admin goes to router settings and hides Wi-Fi name. Now normal people won't see the name.
> Admin router ki setting mein ja kar Wi-Fi ka naam chhupa deta hai. Ab aam logon ko naam nahi dikhega.

**MAC Filtering:** Admin puts rule in router: "Only allow these MAC addresses. Block everyone else."
> Admin router mein rule lagata hai: "Sirf in MAC addresses ko internet do. Baqi sab ko block kar do."

---

## 4. What is 4-Way Handshake?

When you type Wi-Fi password and press connect, your phone does NOT send password directly to router (because anyone in air can catch it).
> Jab aap Wi-Fi password daal kar connect dabate ho, toh mobile router ko direct password nahi bhejta (kyunki hawa mein koi bhi pakar sakta hai).

Instead, 4 messages happen in background:
> Iske bajaye 4 messages background mein hote hain:

**Message 1:** Router sends random code to phone.
> Router random code phone ko bhejta hai.

**Message 2:** Phone combines its own random code + password to make a proof and sends back. (Hackers capture this from air!)
> Phone apna random code + password ko mila kar proof banata hai aur wapas bhejta hai. (Hackers isi ko hawa mein pakarte hain!)

**Message 3:** Router checks proof and says "Correct, here is the key."
> Router proof check karta hai aur kehta hai "Sahi hai, yeh lo chaabi."

**Message 4:** Phone says "Done! Now starting encryption."
> Phone kehta hai "Done! Ab encryption shuru kar raha hoon."

---

## 5. MAC Spoofing — How Hackers Bypass MAC Filtering

Imagine you are outside a company. Their Wi-Fi is hidden and they have MAC Filtering (only employee's laptop with MAC AA:BB:CC:DD:EE:FF can connect).
> Maan lo aap company ke baher ho. Unka Wi-Fi hidden hai aur MAC Filtering lagi hai (sirf employee ka laptop jiska MAC AA:BB:CC:DD:EE:FF hai connect ho sakta hai).

Your MAC is 11:22:33:44:55:66. If you try to connect, router will block you because your MAC is not in the allowed list.
> Aapka MAC 11:22:33:44:55:66 hai. Agar aap connect karne ki koshish karoge, toh router block kar dega kyunki aapka MAC allowed list mein nahi hai.

### Step 1: Sniff the Air
Hacker puts Wi-Fi card in Monitor Mode. This catches all packets from air. Hacker sees a connected computer and its MAC: **AA:BB:CC:DD:EE:FF**.
> Hacker Wi-Fi card ko Monitor Mode mein dalta hai. Yeh hawa se saare packets pakarta hai. Hacker ko ek connected computer dikhta hai jiska MAC hai: **AA:BB:CC:DD:EE:FF**.

### Step 2: Change MAC (MAC Spoofing)
Hacker goes to terminal and changes their own MAC to the employee's MAC: **AA:BB:CC:DD:EE:FF**.
> Hacker terminal par ja kar apna MAC badal kar employee wala kar deta hai: **AA:BB:CC:DD:EE:FF**.

### Step 3: Enter Network
Now router thinks this is the trusted employee and lets them in. Firewall bypassed!
> Ab router samajhta hai ke yeh wahi employee hai aur andar aane deta hai. Firewall bypass!

---

## 6. Important: MAC Spoofing Does NOT Bypass Password

**Remember:** MAC Spoofing does NOT bypass Wi-Fi password. You must still enter the correct password.
> **Yaad Rakho:** MAC Spoofing se Wi-Fi ka password bypass NAHI hota. Aapko password dena hi parega.

Router has TWO separate walls:
> Router ki do alag deewarein hain:

**Wall 1: Password Gate**
To complete 4-Way Handshake, you MUST have the password. Without it, handshake fails.
> 4-Way Handshake karne ke liye password hona LAZMI hai. Bina password ke handshake fail ho jata hai.

**Wall 2: MAC Filtering**
After correct password, router checks: "Is this MAC allowed?"
> Sahi password dene ke baad router check karta hai: "Kya yeh MAC allowed hai?"

**Conclusion:**
- Correct Password + Wrong MAC Blocked
- No Password + Spoofed MAC Blocked
- Correct Password + Spoofed MAC ENTRY!

---

## What I Learned Today

Today I learned Wi-Fi networking properly. Now I know:
> Aaj maine Wi-Fi networking sahi se seekh liya. Ab mujhe pata hai:

* Wi-Fi is internet without wires, technical name IEEE 802.11
> Wi-Fi bina taron ka internet hai, technical naam IEEE 802.11

* SSID is network name, BSSID is router MAC address
> SSID network naam hai, BSSID router MAC address hai

* 2.4 GHz goes far but slow, 5 GHz fast but short range
> 2.4 GHz door tak jaata hai lekin slow, 5 GHz tez hai lekin range kam

* WPA2 uses 4-Way Handshake, WPA3 is more secure
> WPA2 4-Way Handshake use karta hai, WPA3 zyada secure hai

* Deauth attack disconnects users to capture handshake
> Deauth attack users ko disconnect kar ke handshake capture karta hai

* MAC Spoofing bypasses MAC Filtering but needs password first
> MAC Spoofing MAC Filtering ko bypass karta hai lekin pehle password chahiye

> Ab Wi-Fi ka poora game samajh aa gaya hai!
