# Day 19: MAC Flooding — Switch Ki Memory Ko Full Karna

Today i am learning about MAC Flooding, which is an attack that fills up a switch's memory and breaks it.
> Aaj main MAC Flooding seekh raha hoon, jo switch ki memory ko full kar ke use tabah karne wala attack hai.

Until now we learned that a switch keeps a list in its brain called the MAC Table or CAM Table. This table stores: "Port 1 has laptop A, Port 2 has laptop B."
> Abhi humne parha ke network ke andar Switch data bhejne ke liye apne dimaag mein ek list rakhta hai jise hum MAC Table ya CAM Table kehte hain. Is table mein likha hota hai ke "Port 1 par laptop A hai, Port 2 par laptop B hai."

But a switch is a physical hardware device, meaning its memory (CAM Table) has a limited size. It can only store a few thousand MAC addresses at a time.
> Lekin switch ek physical hardware device hai, iska matlab hai ke uski memory (CAM Table) ka size limited (mehdood) hota hai. Usmein ek waqt mein sirf kuch hazaar MAC addresses hi store ho sakte hain.

---

## 1. Hacker's Vision: MAC Flooding (The Overload)

The hacker takes advantage of this memory weakness in the switch.
> Hacker switch ki isi memory ki kamzori ka faida uthata hai.

**Attack Logic:** The hacker runs an automatic script from their laptop that creates thousands of fake MAC addresses every millisecond and throws them at the switch.
> Hacker apne laptop se ek automatic script chalata hai jo har ek millisecond mein hazaaron nakli (fake) MAC addresses bana kar switch ki taraf phenkna shuru kar deti hai.

**Switch Goes Crazy:** The switch thinks new computers are continuously joining the network. It starts writing all those fake MAC addresses into its list (CAM Table).
> Switch samajhta hai ke network mein naye naye computers aate ja raye hain. Woh un saare fake MAC addresses ko apni list (CAM Table) mein likhna shuru kar deta hai.

**Result:** Within just a few seconds, the switch's brain (CAM Table) becomes completely FULL, and there is no space left to store the real computers' MAC addresses!
> Natija: Sirf kuch hi seconds mein switch ka dimaag (CAM Table) poori tarah Full ho jata hai aur usmein asli computers ke MAC addresses rakhne ki jagah hi nahi bachti.

---

## 2. The Real Damage: Hub Mode

When the switch's memory is completely full, it goes crazy and stops working like a normal Switch. It becomes a Hub!
> Jab switch ki memory completely full ho jati hai, toh woh pagal ho jata hai aur aik normal Switch ki tarah kaam karna band kar deta hai. Woh Hub ban jata hai!

**What is Hub Mode?** Now if Computer A sends data to Computer B, the switch doesn't know where Computer B is because its memory is full. So it throws (Broadcasts) that data packet to EVERY port on the network!
> Hub ka matlab hai ke ab agar Computer A kisi Computer B ko data bhejega, toh switch ko memory full hone ki wajah se pata hi nahi hoga ke Computer B kahan hai. Woh us data packet ko network ki har ek port par phenk dega (Broadcast kar dega).

The hacker sits quietly on their port and captures all that data!
> Hacker chupke se apni port par baith kar woh saara data capture kar leta hai!

---

## 3. Defender's Counter: Port Security (The Guard)

Defenders protect against this disaster by turning on a feature on switch ports called Port Security:
> Defenders is tabaahi se bachne ke liye switch ke ports par ek feature on karte hain jise Port Security kehte hain:

**How Port Security Works?** The admin sets a limit on every switch port: "Only ONE (1) MAC address can be learned on this port at a time."
> Admin switch ki har port par ek limit laga deta hai ke: "Is port par aik waqt mein sirf Ek (1) hi MAC address seekha ja sakta hai."

When the hacker sends thousands of fake MAC addresses from that port, the switch immediately recognizes the limit has been crossed. The switch Auto-Shuts Down (Disables) that port due to security violation and the hacker's connection is cut!
> Jab hacker us port se hazaaron fake MAC addresses bhejta hai, toh switch foran pehchan jata hai ke limit cross ho gayi hai. Switch us port ko security violation ki wajah se Auto-Shutdown (Band) kar deta hai aur hacker ka connection kat jata hai.

---

## 4. MUST MEMORIZE (Zubani Yaad Rakho)

- **CAM/MAC Table:** The switch's memory where port and MAC address records are stored.
> Switch ki memory jahan ports aur MAC addresses ka record hota hai.

- **MAC Flooding:** Filling the switch's memory with fake MAC addresses so it starts broadcasting traffic to everyone (Fail-Open/Hub Mode).
> Switch ki memory ko fake MAC addresses se bhar dena taake woh network traffic ko sab par phenkna (fail-open/hub mode) shuru kar de.

- **Port Security:** The switch feature that sets a limit on maximum allowed MAC addresses per port.
> Switch ka woh feature jo har port par maximum allowed MAC addresses ki limit set karta hai.

- **Fail-Open/Hub Mode:** When MAC Flooding fills the CAM Table, the switch stops being secure and starts broadcasting data to all ports like a normal Hub.
> MAC Flooding se jab switch ki memory (CAM Table) full hoti hai, toh woh security chhor kar normal Hub ki tarah data sab ko phenkna shuru kar deta hai.

---

## 5. ARP Spoofing vs MAC Flooding (The Difference)

| ARP Spoofing | MAC Flooding |
|--------------|--------------|
| Hacker lies to devices (Spoofing) | Hacker fills switch memory (Flooding) |
| Switch still works normally | Switch breaks and becomes Hub |
| Hacker is Man-in-the-Middle | Hacker captures all broadcasted traffic |
| DAI (Dynamic ARP Inspection) blocks it | Port Security blocks it |

> ARP Spoofing mein hacker devices ko jhoot bolta hai | MAC Flooding mein hacker switch ki memory full karta hai
> Switch normal kaam karta hai | Switch toot kar Hub ban jata hai
> Hacker beech mein baith kar data parhta hai | Hacker broadcast ho raha saara data pakarta hai
> DAI (Dynamic ARP Inspection) isko block karta hai | Port Security isko block karti hai

---

## What I Learned Today

Today I learned MAC Flooding properly. Now I know:
> Aaj maine MAC Flooding sahi se seekh liya. Ab mujhe pata hai:

* CAM/MAC Table stores port to MAC address mapping in switch
> CAM/MAC Table switch mein port aur MAC address ka record rakhti hai

* MAC Flooding sends thousands of fake MAC addresses to fill switch memory
> MAC Flooding hazaaron fake MAC addresses bhej kar switch ki memory full kar deta hai

* When switch memory is full, it becomes a Hub (Fail-Open/Hub Mode)
> Jab switch ki memory full hoti hai, toh woh Hub ban jata hai (Fail-Open/Hub Mode)

* In Hub Mode, switch broadcasts all traffic to every port
> Hub Mode mein switch saara traffic har port par broadcast kar deta hai

* Hacker captures all broadcasted traffic without ARP Spoofing
> Hacker bina ARP Spoofing ke saara broadcast traffic capture kar leta hai

* Port Security limits number of MAC addresses per port
> Port Security har port par MAC addresses ki limit set karti hai

* Port Security auto-shutdowns port if limit is violated
> Port Security limit cross hone par port auto-shutdown kar deti hai

* MAC Flooding is different from ARP Spoofing — different attacks, different defenses
> MAC Flooding ARP Spoofing se alag hai — alag attacks, alag defenses

> Ab MAC Flooding ka poora game samajh aa gaya hai!
