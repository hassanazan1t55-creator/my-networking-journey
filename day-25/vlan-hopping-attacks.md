# Day 25: VLAN Hopping Attacks

Today i am learning about VLAN Hopping attacks, where hackers jump from one VLAN to another.
> Aaj main VLAN Hopping attacks seekh raha hoon, jahan hackers ek VLAN se doosre VLAN mein chalaang maar dete hain.

On Day 15 we learned that VLANs (Virtual LANs) are used to create hidden and isolated networks (like HR, Finance, IT) inside one physical switch, so traffic from one network cannot go to another.
> Humne Day 15 par parha tha ke VLANs (Virtual LANs) ka maqsad ek hi physical switch ke andar khufia aur alag-alag isolated networks (jaise HR, Finance, IT) banana hai, taake ek network ka traffic doosre mein na ja sake.

But, if there is a loophole in the switch configuration, a hacker can jump from their assigned VLAN to another sensitive VLAN without authorization. This attack is called VLAN Hopping.
> Lekin, agar switch ki configuration mein koi loophole ho, toh ek hacker bina authorization ke apne assigned VLAN se jump kar ke doosre sensitive VLAN mein ghus sakta hai. Is attack ko VLAN Hopping kehte hain.

There are two most important methods for this:
> Iske do sab se VIP tareeqe hote hain:

---

## 1. Switch Spoofing (Tricking to Become Trunk Port)

Switch ports are of two types:
> Switch ke ports do tarah ke hote hain:

**Access Port:** For normal computers (Carries traffic of only ONE VLAN).
> Jo aam computers ke liye hota hai (Sirf ek VLAN ka traffic uthata hai).

**Trunk Port:** Connects two switches together (Carries ALL VLANs traffic together).
> Jo do switches ko aapas mein jorhta hai (Yeh saare VLANs ka traffic ek sath carry karta hai).

**The Loophole:** Cisco switches have a protocol called DTP (Dynamic Trunking Protocol). Its job is to automatically negotiate and make ports "Trunk" ports.
> Cisco switches mein ek protocol hota hai jise DTP (Dynamic Trunking Protocol) kehte hain. Iska kaam automatically ports ko negotiation ke zariye "Trunk" banana hota hai.

**Attack Mechanism:** The hacker connects their laptop to an access port on the switch and crafts DTP packets to tell the switch: "I am not a computer, I am another Switch, create a Trunk link with me!"
> Hacker apne laptop ko switch ke access port par lagata hai aur DTP packets craft kar ke switch ko kehta hai: "Main computer nahi hoon, main ek doosra Switch hoon, mere sath Trunk link banao!"

If the switch port is on auto-negotiate mode, it gets tricked and turns that port into a Trunk Port. As soon as the port becomes trunk, the hacker starts receiving traffic from ALL VLANs directly!
> Agar switch ka port auto-negotiate par ho, toh woh dhoka kha jata hai aur us port ko Trunk Port bana deta hai. Jaise hi port trunk banta hai, hacker ke paas saare VLANs ka traffic direct aana shuru ho jata hai!

---

## 2. Double Tagging (Double Envelope Attack)

This attack happens when the hacker is on the switch's default or native VLAN (mostly VLAN 1). It takes advantage of a weakness in trunk ports.
> Yeh attack tab hota hai jab hacker switch ke default ya native VLAN (mostly VLAN 1) par baitha ho. Ismein trunk ports ki aik kamzori ka faida uthaya jata hai.

**The Logic:** When a switch's trunk port sends a packet from its Native VLAN, it does NOT put any VLAN tag (envelope) on it.
> Jab switch ka trunk port apne Native VLAN ka packet bhejta hai, toh woh us par koi VLAN tag (lifafa) nahi lagata.

**Attack Mechanism:** The hacker creates a packet with TWO Tags (Double Envelopes):
> Hacker ek aisa packet craft karta hai jiske oopar Do Tags (Double Lifafay) hote hain:

**1. Outer Tag (Outside envelope):** Native VLAN (e.g., VLAN 1).
> Outer Tag (Baher wala lifafa): Native VLAN (e.g., VLAN 1).

**2. Inner Tag (Inside envelope):** Target VLAN (e.g., Finance - VLAN 10).
> Inner Tag (Andar wala lifafa): Target VLAN (e.g., Finance - VLAN 10).

**The Process:** When the first switch sees this packet, it reads the outer tag (VLAN 1), removes it (strips it), and sends the packet on the trunk link.
> Jab pehla switch is packet ko dekhta hai, toh woh outer tag (VLAN 1) ko parhta hai, use hata deta hai (strip kar deta hai), aur packet ko trunk link par bhej deta hai.

When the second switch receives the packet, it only sees the inner tag (VLAN 10). It thinks this packet was meant for VLAN 10, and sends it directly to the Finance department computers!
> Jab doosra switch us packet ko receive karta hai, toh use sirf andar wala tag (VLAN 10) dikhta hai. Woh samajhta hai ke yeh packet VLAN 10 ke liye hi aaya tha, aur use seedha Finance department ke computers ki taraf bhej deta hai!

**Important:** This attack is ONE-WAY only!
> Important: Yeh attack sirf ONE-WAY hai!

The hacker can SEND packets into VLAN 10, but they CANNOT RECEIVE replies from VLAN 10 because the hacker's port is not on VLAN 10, and they can't add double tags to the reply.
> Hacker VLAN 10 mein packets BHEJ sakta hai, lekin VLAN 10 se REPLIES RECEIVE nahi kar sakta kyunki hacker ka port VLAN 10 par nahi hai, aur woh reply mein double tags nahi laga sakta.

---

## 3. Defender's Defense: How to Stop These Attacks

Big companies follow these two golden rules to prevent VLAN Hopping:
> Badi companies mein is attack ko rokne ke liye network admins ko do sunhari rules follow karne hote hain:

**1. Disable DTP on all ports:** Use `switchport nonegotiate` so no one can pretend to be a switch.
> Saare ports par DTP ko disable karo (`switchport nonegotiate`), taake koi fake switch na ban sake.

**2. Change Native VLAN:** Change Native VLAN to an unused VLAN ID (e.g., VLAN 999) and never put normal users in it.
> Native VLAN ko badal kar koi aisi ID rakh do jo koi use na kar raha ho (e.g., VLAN 999), aur aam users ko usmein kabhi mat rakho.

---

## 4. Switch Spoofing vs Double Tagging (Quick Comparison)

| Attack Type | Port Changes? | Traffic Flow | What Hacker Gets |
|-------------|---------------|--------------|------------------|
| **Switch Spoofing** | Port becomes TRUNK | Two-Way | All VLANs traffic |
| **Double Tagging** | Port stays ACCESS | One-Way | Can SEND into other VLANs, but CANNOT receive replies |

> Switch Spoofing: Port TRUNK ban jata hai | Double Tagging: Port ACCESS hi rehta hai
> Switch Spoofing: Two-Way traffic | Double Tagging: One-Way traffic
> Switch Spoofing: Saare VLANs ka traffic | Double Tagging: Sirf packets bhej sakta hai, replies nahi aa sakte

---

## 5. MUST MEMORIZE (Zubani Yaad Rakho)

- **Switch Spoofing:** Using DTP protocol to turn a normal port into a Trunk Port.
> DTP protocol ka faida utha kar aam port ko Trunk Port mein badalna.

- **Double Tagging:** Using Native VLAN weakness to put two tags on a packet so the switch strips the outer tag and the packet enters the target VLAN.
> Native VLAN ka faida utha kar packet par do tags lagana taake switch outer tag ko strip kare aur packet target VLAN mein ghus jaye.

- **DTP (Dynamic Trunking Protocol):** System that automatically negotiates trunking between switches.
> Switches ke beech automatically trunking negotiate karne wala system.

- **One-Way Attack:** Double Tagging is one-way because the hacker cannot receive replies from the target VLAN.
> Double Tagging one-way hai kyunki hacker target VLAN se replies receive nahi kar sakta.

---

## What I Learned Today

Today I learned VLAN Hopping attacks properly. Now I know:
> Aaj maine VLAN Hopping attacks sahi se seekh liya. Ab mujhe pata hai:

* VLAN Hopping is jumping from one VLAN to another
> VLAN Hopping ek VLAN se doosre VLAN mein chalaang maarna hai

* Switch Spoofing tricks the switch into making port Trunk
> Switch Spoofing switch ko dhoka de kar port ko Trunk banata hai

* DTP protocol is the weakness used in Switch Spoofing
> DTP protocol Switch Spoofing mein kamzori hai

* Double Tagging uses two VLAN tags to sneak into other VLAN
> Double Tagging do VLAN tags use karta hai doosre VLAN mein ghusne ke liye

* Double Tagging is ONE-WAY (can send packets, but cannot receive replies)
> Double Tagging ONE-WAY hai (packets bhej sakta hai, lekin replies nahi aa sakte)

* Disable DTP and change Native VLAN to prevent these attacks
> DTP disable karo aur Native VLAN badlo in attacks ko rokne ke liye

* Switch Spoofing is TWO-WAY (can send AND receive all VLANs traffic)
> Switch Spoofing TWO-WAY hai (saare VLANs ka traffic bhej aur receive kar sakta hai)

> Ab VLAN Hopping ka poora game samajh aa gaya hai!
