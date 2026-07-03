# Day 15: VLANs — Ek Switch, Hazaaron Khufia Networks

Today i am learning about VLANs, which let us create multiple virtual networks on one single switch.
> Aaj main VLANs seekh raha hoon, jo ek hi switch par multiple virtual networks banane dete hain.

---

## 1. What is VLAN? (The Logic)

Imagine a big office where HR, Finance, and IT Engineers all sit on the same floor and all their computers are connected to one big switch.
> Maan lo ek bohot bada office hai jahan HR, Finance, aur IT Engineers sab ek hi floor par baithte hain aur sab ke computers ek hi bade Switch se jure hain.

**Problem:** If it's a normal network, HR's computer can send data directly to Finance's computer. If a hacker hacks HR's computer, they can sit there and run nmap scans on the whole office (Finance, IT) and steal everyone's data.
> Masla: Agar normal network hoga, toh HR ka computer, Finance ke computer ko direct data bhej sakega. Agar koi hacker HR ke computer ko hack kar leta hai, toh woh wahin se baithe baithe poore office ke computers (Finance, IT) par nmap scan chala lega aur sab ka data chura lega.

**Solution (VLAN):** Network engineers create virtual walls inside the switch using software. They tell the switch: "Ports 1 to 5 are only HR, Ports 6 to 10 are only Finance." This virtual partition is called VLAN.
> Solution (VLAN): Network engineers switch ke andar software ke zariye virtual (nakli) deewarein khari kar dete hain. Woh switch ko kehte hain: "Port 1 se 5 tak sirf HR hai, Port 6 se 10 tak sirf Finance hai." Is virtual partition ko hum VLAN kehte hain.

Even though all computers are connected to the same switch, HR's computer cannot talk to Finance's computer unless a Router in between gives permission!
> Ab chahe saare computers ek hi switch se jure hon, lekin HR wala computer Finance wale computer se tab tak baat nahi kar sakta jab tak beech mein koi Router ijazat na de!

---

## 2. MUST MEMORIZE (Zubani Yaad Rakho)

These three things should be firmly remembered at elite hacker and network admin level:
> Elite hacker aur network admin level par yeh teen cheezain bilkul paki yaad honi chahiye:

**1. VLAN ID**
Every VLAN has a number (like VLAN 10, VLAN 20). By default, all switch ports are in VLAN 1.
> Har VLAN ka ek number hota hai (jaise VLAN 10, VLAN 20). By default, switch ke saare ports VLAN 1 mein hote hain.

**2. Access Port**
This port connects directly to a single computer or laptop. It can only be part of one VLAN.
> Yeh woh port hota hai jo direct kisi single computer ya laptop se jura hota hai. Yeh sirf ek hi VLAN ka hissa ho sakta hai.

**3. Trunk Port**
This is a VIP port. When data needs to go from one switch to another switch, all VLANs (HR, Finance, IT) data travels through one single wire. That path is called Trunk Link.
> Yeh bohot VIP port hota hai. Jab ek switch se dusre switch tak data le kar jana ho, toh ek hi wire ke andar se saare VLANs (HR, Finance, IT) ka data guzarta hai. Us raaste ko Trunk Link kehte hain.

---

## 3. KEEP IN MIND (Deep Logic)

**VLAN Tagging (802.1Q):**
When HR and Finance data both travel together through the Trunk wire, the switch puts a small Tag (slip) on every packet (like "This packet belongs to VLAN 10"). When the packet reaches the other switch, it reads the tag and sends it to the right department. This protocol is called IEEE 802.1Q.
> Jab Trunk wire ke andar se HR aur Finance dono ka data sath guzar raha hota hai, toh switch har packet ke upar ek choti si Tag (parchi) laga deta hai (jaise: "Yeh packet VLAN 10 ka hai"). Jab woh packet dusre switch par pohanchta hai, toh dusra switch parchi dekh kar use sahi department mein bhej deta hai. Is protocol ka naam IEEE 802.1Q hai.

**Hacker Vision (VLAN Hopping):**
If the company didn't tighten switch security, a hacker tricks the switch by presenting their laptop as a "Fake Switch" and changes an Access Port into a Trunk Port. Then the hacker jumps from one VLAN to another secure VLAN (like Finance) without any router. This attack is called VLAN Hopping. Defenders protect against this by keeping all unused ports closed.
> Agar company ne switch ki security tight nahi ki, toh hacker apne laptop ko chalaki se switch ke samne ek "Fake Switch" bana kar pesh karta hai aur access port ko Trunk Port mein badal deta hai. Phir hacker bina kisi router ke, ek VLAN se doosre secure VLAN (jaise Finance) ke andar chalaang maar jata hai. Is attack ko VLAN Hopping kehte hain, aur defenders is se bachne ke liye saare unused ports ko band rakhte hain.

---

## What I Learned Today

Today I learned VLANs properly. Now I know:
> Aaj maine VLANs sahi se seekh liya. Ab mujhe pata hai:

* VLAN creates virtual walls inside a switch to separate departments
> VLAN switch ke andar virtual deewarein banata hai departments ko alag karne ke liye

* VLAN ID is the number given to each VLAN
> VLAN ID har VLAN ko diya gaya number hai

* Access Port connects to single device, part of one VLAN
> Access Port single device se jorta hai, ek VLAN ka hissa hai

* Trunk Port carries all VLANs data between switches
> Trunk Port switches ke darmayan saare VLANs ka data le jata hai

* 802.1Q Tagging adds label on packets so other switch knows which VLAN
> 802.1Q Tagging packets par label lagata hai taake doosre switch ko pata chale kaun sa VLAN

* VLAN Hopping: Hacker tricks switch to jump between VLANs
> VLAN Hopping: Hacker switch ko dhoka de kar VLANs ke darmayan chalaang maar sakta hai

* Defenders keep unused ports closed to prevent VLAN Hopping
> Defenders unused ports band rakhte hain VLAN Hopping se bachne ke liye

> Ab VLANs ka poora game samajh aa gaya hai!
