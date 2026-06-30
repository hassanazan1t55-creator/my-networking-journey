# Day 1: Computer Network Architecture

Today i am learning the core architecture of computer networks.
> Aaj main computer network ke buniyaadi dhaanche aur uske wajood ko samajh raha hoon.

A network connects two or more devices to process and share data.
> Ek network do ya do se ziyaada devices ko aapas mein data process aur share karne ke liye jorta hai.

The real purpose of a network is resource sharing and distributed computing.
> Network ka asli maqsad resources ko aapas mein baantna aur distributed computing hai.

---

## Network Classification (LAN vs WAN)
> Networks ki do buniyaadi iksaam (LAN aur WAN)

* **LAN (Local Area Network):** This is for small areas like a house or an office. it is very fast.
> **LAN (Local Area Network):** Yeh chote ilaakon jaise ghar ya office tak mehdood hota hai aur iski raftaar bohot tez hoti hai.

* **WAN (Wide Area Network):** This connects multiple LANs across cities or countries. the internet is the best example.
> **WAN (Wide Area Network):** Yeh mukhtalif shehron ya mulkon ke LANs ko aapas mein jorta hai. Internet iski sab se badi misal hai.

---

## Network Topologies and Weak Points
> Network ka physical layout aur unki buniyaadi kamzoriyan

### 1. Bus Topology
All computers connect to a single main cable called the backbone.
> Tamam computers ek hi buniyaadi taar se jure hote hain jise backbone kehte hain.

* **Flaw:** If the main cable breaks, the entire network goes down instantly.
> **Kamzori:** Agar main cable kahin se toot jaye, toh poora network ek jhatke mein band ho jata hai.

### 2. Star Topology
All devices connect to a central device called a switch.
> Tamam devices ek darmiyani device se juri hoti hain jise Switch kehte hain.

* **Flaw:** If the central switch fails, the whole network stops working.
> **Kamzori:** Agar woh darmiyani Switch kharab ho jaye, toh poora network tabah ho jata hai.

### 3. Mesh Topology
Every computer is directly connected to every other computer. it has high redundancy.
> Har computer doosre computer ke sath direct taar se jura hota hai. Ismein redundancy bohot ziyaada hoti hai.

---

## Day 1 Task: Bank Network Design Scenario
> Bank ke network design ka elite level analysis

**Scenario:** Design a network for a bank where downtime can cause millions of dollars in losses. should we use star or mesh topology?
> **Scenario:** Ek bank ke liye network design karna hai jahan ek second ka breakdown bhi nuksan deh ho sakta hai. Wahan Star topology istemal hogi ya Mesh topology?

### My Analysis and Solution:
For critical bank infrastructure, i will use a **mesh topology** for the core system.
> Buniyaadi banking infrastructure ke liye main **Mesh Topology** ka istemal karunga.

In Star topology, if the central switch fails, everything goes down. this is too risky.
> Star topology mein agar central switch kharab ho jaye toh sab kuch ruk jata hai. Yeh bohot bada khatra hai.

Mesh topology provides alternative paths. if one wire fails, data automatically takes another route.
> Mesh topology mukhtalif raste faraham karti hai. Agar ek taar kharab bhi ho jaye, toh data doosre raste se guzar jata hai.

For better efficiency, we can connect normal employee PCs using **star topology**, but core servers must use **mesh topology**.
> Behtar karkardagi ke liye hum aam computers ko **Star Topology** se jor sakte hain, lekin main servers ko **Mesh Topology** par hona chahiye.

---

## What I Messed Up Today (Meri Learning)

Initially, i thought mesh topology is always best for everything because it is safe.
> Shuru mein mujhe laga ke Mesh topology har jagah ke liye behtareen hai kyunki yeh mehfooz hoti hai.

But then i realized it is very expensive and difficult to manage for a whole building. that is why a hybrid layout is better.
> Magar baad mein mujhe samajh aaya ke poori building ke liye yeh bohot mehangi aur mushkil hoti hai. Isiliye hybrid layout ziyaada behtar hai.
