# Day 21: WAN Concepts — Leased Lines, MPLS and VPN Ka Asli Farq

Today i am learning about WAN technologies that connect cities and countries securely.
> Aaj main WAN technologies seekh raha hoon jo shehron aur mulkon ko secure tareeqe se jorti hain.

Yesterday we learned that WAN (Wide Area Network) is the internet or long cables that connect cities and countries (like connecting offices in Lahore and Karachi). But big companies and banks don't use normal internet to transfer data because hackers sit on the normal internet.
> Humne kal padha tha ke WAN (Wide Area Network) internet ya lambi taron ka naam hai jo shehron aur mulkon ko jorhti hai (jaise Lahore aur Karachi ke offices ko jorhna). Lekin dunya ki badi badi companies aur banks aapas mein data transfer karne ke liye aam internet ka istemal nahi karte, kyunki aam internet par hackers baithe hote hain.

Let's see what technologies are used to keep data private and safe in the outside world (WAN).
> Aao dekhte hain ke baher ki dunya (WAN) mein data ko private aur safe rakhne ke liye kaun si technologies use hoti hain.

---

## 1. Leased Lines (Your Own Private Road)

Imagine a bank's main server is in Lahore and one branch is in Karachi.
> Maan lo ek bank ka main server Lahore mein hai aur uski ek branch Karachi mein hai.

**Logic:** The bank pays a big telecom company (ISP) a lot of money and says: "Lay a fiber-optic wire from Lahore to Karachi that ONLY our data travels on. No one else in the world should even touch that wire."
> Bank kisi telecom company (ISP) ko bohot bhari paise deta hai aur kehta hai ke "Lahore se Karachi tak ek aisi fiber-optic tar (wire) bichao jis par sirf aur sirf hamara data chale, dunya ka koi aur banda us wire ko touch bhi na kar sake."

**Advantage:** This network is 100% private. Normal internet traffic doesn't run on it, so it is super-fast and super-secure.
> Yeh network 100% private hota hai, is par aam internet ka traffic nahi hota, isliye yeh super-fast aur super-secure hota hai.

**Disadvantage:** This is very expensive. Not every small company can afford it.
> Yeh bohot zyada mehngi (expensive) hoti hai. Har choti company isay afford nahi kar sakti.

---

## 2. MPLS (Multi-Protocol Label Switching) — ISP's VIP Path

Leased lines are expensive, so telecom companies created a middle path called MPLS.
> Leased line mehngi hoti hai, isliye telecom companies ne ek darmiyana rasta nikala jise MPLS kehte hain.

**Logic:** In this, the wire is shared by everyone (like normal internet), but the ISP puts a special VIP Label (Tag) on your data packet.
> Ismein tar (wire) sab ki shared hoti hai (aam internet ki tarah), lekin ISP aapke data packet ke upar ek khas VIP Label (Tag) laga deta hai.

Routers quickly look at that label and send your packet through a separate, secret path that is different from normal public traffic.
> Router speed mein sirf us label ko dekhta hai aur aapke packet ko ek alag, khufia raste se guzarta hai jo baki aam public traffic se alag hota hai.

**Advantage:** This is cheaper than leased line and still gives great speed.
> Yeh leased line se sasti hoti hai aur speed bhi kamaal milti hai.

---

## 3. VPN (Virtual Private Network) — Secret Tunnel Inside the Internet

If a company doesn't have money for Leased Line or MPLS, they use the cheapest and best method called VPN.
> Agar kisi company ke paas Leased line ya MPLS ke paise na hon, toh woh sab se sasta aur behtareen tareeqa nikalte hain jise VPN kehte hain.

**Logic:** These run on the normal internet, but VPN software creates a Secret Tunnel (Encrypted Pipe) between your computer and the office server inside the internet.
> Yeh chalte aam internet par hi hain, lekin VPN software aapke computer aur office ke server ke beech internet ke andar ek Khufia Tunnel (Encrypted Pipe) bana deta hai.

When your data passes through this tunnel, even if a hacker (or the ISP itself) catches the packet, they only see Crypto-Garbage because the data is completely locked.
> Jab aapka data is tunnel se guzar raha hota hai, toh raste mein baitha koi bhi hacker (ya ISP khud) agar packet ko pakar bhi le, toh use Crypto-Kachra dikhta hai kyunki data poori tarah lock hota hai.

---

## 4. MUST MEMORIZE (Zubani Yaad Rakho)

- **Leased Line:** Physically dedicated and private wire between two locations (Most expensive, most secure).
> Do locations ke beech ki physically dedicated aur private wire (Sab se mehngi, sab se secure).

- **MPLS:** Technology that puts a Label on packets and sends them through a VIP path on the ISP's shared network.
> ISP ke shared network par packets par Label laga kar unhein VIP raste se bhejny ki technology.

- **VPN:** Creating a Virtual Private Tunnel using encryption on top of the public internet.
> Public internet ke upar encryption ka istemal kar ke ek Virtual Private Tunnel banana.

---

## 5. Comparison Table (Quick Revision)

| Technology | Security | Speed | Cost | Privacy |
|------------|----------|-------|------|---------|
| **Leased Line** | Highest | Highest | Highest | 100% Private |
| **MPLS** | High | High | Medium | Semi-Private |
| **VPN** | High (Encrypted) | Medium | Lowest | Encrypted Tunnel |

> Leased Line: Security Highest, Speed Highest, Cost Highest | MPLS: Security High, Speed High, Cost Medium | VPN: Security High (Encrypted), Speed Medium, Cost Lowest

---

## What I Learned Today

Today I learned WAN Concepts properly. Now I know:
> Aaj maine WAN Concepts sahi se seekh liya. Ab mujhe pata hai:

* Leased Line is a dedicated private wire between two locations (most secure, most expensive)
> Leased Line do locations ke beech private wire hai (sab se secure, sab se mehngi)

* MPLS uses Labels on packets to send them through VIP paths on shared network
> MPLS packets par Label laga kar unhein VIP raste se shared network par bhejta hai

* VPN creates an encrypted tunnel inside the public internet
> VPN public internet ke andar encrypted tunnel banata hai

* VPN hides data from hackers even if they capture the packets
> VPN packets capture karne par bhi data hackers se chhupa deta hai

* Leased Line is best when money is not an issue and security is top priority
> Leased Line best hai jab paisa issue nahi aur security top priority ho

* MPLS is a middle option between cost and security
> MPLS cost aur security ke darmayan middle option hai

* VPN is the cheapest option for secure WAN communication
> VPN secure WAN communication ke liye sab se sasta option hai

> Ab WAN Concepts ka poora game samajh aa gaya hai!
