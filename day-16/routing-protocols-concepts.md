# Day 16: Routing Protocols — Internet Ka Asli Google Maps

Today i am learning about Routing Protocols, which are like Google Maps for routers to find the best path.
> Aaj main Routing Protocols seekh raha hoon, jo routers ke liye Google Maps ki tarah hain — sab se acha rasta dhoondne ke liye.

Until now we learned that Routers connect different networks. But think, when millions of routers are connected across the whole world, how do they know which path from Pakistan to America is the fastest?
> Abhi tak humne parha ke Router do alag alag networks ko jorhta hai. Lekin socho, jab poori dunya mein karoron routers aaps mein jure hain, toh unhein kaise pata chalta hai ke Pakistan se bheja hua ek packet America ke server tak kis raste se sab se jaldi pohanchega?

Routers speak special languages with each other called Routing Protocols. These protocols work like Google Maps for the internet — finding the shortest and best path!
> Iske liye routers aaps mein khass zabanein bolte hain, jise hum Routing Protocols kehte hain. Yeh protocols internet ke liye Google Maps ka kaam karte hain—sab se chota aur behtareen rasta dhoondna!

---

## 1. OSPF (Open Shortest Path First) — Ghar Ka Map

OSPF is an Interior Gateway Protocol (IGP). This means it is used to connect routers inside one company, bank, or university.
> OSPF ek Interior Gateway Protocol (IGP) hai. Iska matlab hai ke yeh kisi ek company, bank, ya university ke andar lage routers ko aapas mein jorhne ke liye istemal hota hai.

**How it Works (Logic):** OSPF is a "Link-State" protocol. Every router keeps a complete map (topology) of all nearby routers in its memory.
> OSPF "Link-State" protocol hai. Iska har router apne aaspas ke saare routers ka poora naksha (topology) apne dimaag mein bitha kar rakhta hai.

**Shortest Path Algorithm:** It uses a formula called Dijkstra Algorithm to find the fastest path. It looks at bandwidth (speed) — whichever path is fastest, data is sent that way. If one path breaks, it automatically finds another path within 2 seconds!
> Yeh sab se tez rasta nikalne ke liye ek formula istemal karta hai jise Dijkstra Algorithm kehte hain. Yeh bandwidth (speed) dekhta hai—jo rasta sab se tez hoga, data wahan se bhejega. Agar ek rasta band ho jaye, toh yeh automatic 2 second mein doosra rasta nikal leta hai.

---

## 2. BGP (Border Gateway Protocol) — Dunya Ka Map

BGP is an Exterior Gateway Protocol (EGP). This is the real king of the internet! When two big Networks (like PTCL and Google, or Airtel and Facebook) need to connect, BGP is used.
> BGP ek Exterior Gateway Protocol (EGP) hai. Yeh internet ka asli badshah hai! Jab do bade Networks (jaise PTCL aur Google, ya Airtel aur Facebook) ko aapas mein jorhna ho, toh wahan BGP ka istemal hota hai.

The internet is actually a collection of big networks called Autonomous Systems (AS). BGP connects one AS to another AS.
> Internet asal mein bade bade networks ka majmua hai jise technical zaban mein Autonomous Systems (AS) kehte hain. BGP ek AS ko doosre AS se jorhta hai.

**How it Works (Logic):** BGP doesn't care about speed. It is a Path Vector protocol. It looks at which path has the fewest Autonomous Systems (big networks) to pass through.
> BGP ko speed se farq nahi parta, yeh Path Vector protocol hai. Yeh dekhta hai ke kis raste mein sab se kam Autonomous Systems (bade networks) se guzarna parega.

Its biggest job is to control the politics (policies and routing rules) of internet traffic.
> Iska sab se bada kaam internet par traffic ki siyasat (policies aur routing rules) ko control karna hota hai.

---

## 3. Hacker's Vision vs Defensive Mode

### Hacker Attack: BGP Hijacking

BGP is very old and it blindly trusts other routers without checking.
> BGP protocol bohot purana hai aur yeh aankhein band kar ke doosre routers par bharosa karta hai.

**Attack Logic:** Imagine a hacker takes control of a bad Internet Service Provider's (ISP) router. That router lies to all BGP routers in the world: "The real path to Twitter/X goes through me." All other routers believe it and all Twitter traffic turns toward the hacker's network. This is called BGP Hijacking, where the hacker can read traffic of entire countries!
> Maan lo ek hacker kisi badmash Internet Service Provider (ISP) ke router ka control le leta hai. Woh router poori dunya ke BGP routers ko jhoot bolta hai ke "Twitter/X ka asli rasta mere paas se guzarta hai". Dunya ke baqi routers uski baat par yaqeen kar lete hain aur Twitter ka saara traffic hacker ke network ki taraf murh jata hai. Isay BGP Hijacking kehte hain, jahan hacker poore mulk ka traffic mod kar parh sakta hai.

### Defender Counter: RPKI Authentication

Defenders use RPKI (Resource Public Key Infrastructure) to protect against this trick:
> Defenders is dhandli se bachne ke liye RPKI (Resource Public Key Infrastructure) lagate hain:

**RPKI:** This is a system of digital certificates for routing. Now when a router says "I own this IP network", other routers first check the cryptographic certificate to see if it's telling the truth or if it's a hacker.
> Yeh routing mein digital certificates ka nizam hai. Ab jab koi router kehta hai ke "Main is IP network ka maalik hoon", toh baqi routers pehle cryptographic certificate check karte hain ke kya yeh sach bol raha hai ya hacker hai.

---

## 4. MUST MEMORIZE (Zubani Yaad Rakho)

- **OSPF:** Runs inside one organization/company (IGP). Finds path based on Speed (Bandwidth).
> Ek hi organization/company ke andar chalta hai (IGP). Yeh Speed (Bandwidth) ki buniyaad par rasta nikalta hai.

- **BGP:** Connects different Autonomous Systems (big ISPs/Networks) together (EGP). The whole internet runs on this.
> Do alag alag Autonomous Systems (bade ISPs/Networks) ko aapas mein jorhta hai (EGP). Poora internet isi par chalta hai.

- **Autonomous System (AS):** A very big group of routers running under one administration. Every AS has a unique number (ASN).
> Ek hi administration ke andar chalne wale routers ka bohot bada group. Every AS has a unique number (ASN).

---

## 5. KEEP IN MIND (Deep Logic)

**Hacker Vision (BGP Hijacking):** The trick of redirecting internet traffic to wrong paths. Its solution is RPKI which verifies the authenticity of the path.
> Internet par traffic ko ghalat raste par morne ki chalaki. Iska hal RPKI hai jo raste ki asliat ko verify karta hai.

---

## What I Learned Today

Today I learned Routing Protocols properly. Now I know:
> Aaj maine Routing Protocols sahi se seekh liya. Ab mujhe pata hai:

* Routing Protocols are like Google Maps for routers to find best path
> Routing Protocols routers ke liye Google Maps ki tarah hain sab se acha rasta dhoondne ke liye

* OSPF runs inside one company (IGP), finds path based on speed
> OSPF ek company ke andar chalta hai (IGP), speed ke hisaab se rasta nikalta hai

* OSPF uses Dijkstra Algorithm to find fastest path
> OSPF sab se tez rasta nikalne ke liye Dijkstra Algorithm use karta hai

* BGP connects different Autonomous Systems (EGP), whole internet runs on it
> BGP alag alag Autonomous Systems ko jorta hai (EGP), poora internet isi par chalta hai

* BGP doesn't care about speed, it cares about policies and number of ASes
> BGP speed nahi dekhta, yeh policies aur ASes ki ginti dekhta hai

* BGP Hijacking: Hacker lies to redirect internet traffic
> BGP Hijacking: Hacker jhoot bol kar internet traffic ko mod deta hai

* RPKI uses digital certificates to verify routing claims and stop hijacking
> RPKI digital certificates use karta hai routing claims verify karne aur hijacking rokne ke liye

> Ab Routing Protocols ka poora game samajh aa gaya hai!
