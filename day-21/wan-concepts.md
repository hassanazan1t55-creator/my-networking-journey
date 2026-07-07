# Day 21: WAN Concepts — Leased Lines, MPLS & VPN

Today I am learning about WAN technologies that connect cities and countries securely.

Yesterday we learned that WAN (Wide Area Network) is the internet or long cables that connect cities and countries (like connecting offices in Lahore and Karachi). But big companies and banks don't use normal internet to transfer data because hackers sit on the normal internet.

Let's see what technologies are used to keep data private and safe in the outside world (WAN).

---

## Leased Lines — Dedicated Private Connection

Imagine a bank's main server is in Lahore and one branch is in Karachi.

**How it Works:** The bank pays a big telecom company (ISP) a lot of money and says: "Lay a fiber-optic wire from Lahore to Karachi that ONLY our data travels on. No one else in the world should even touch that wire."

**Advantage:** This network is 100% private. Normal internet traffic doesn't run on it, so it is super-fast and super-secure.

**Disadvantage:** This is very expensive. Not every small company can afford it.

---

## MPLS (Multi-Protocol Label Switching) — ISP's VIP Path

Leased lines are expensive, so telecom companies created a middle path called MPLS.

**How it Works:** In this, the wire is shared by everyone (like normal internet), but the ISP puts a special VIP Label (Tag) on your data packet.

Routers quickly look at that label and send your packet through a separate, secret path that is different from normal public traffic.

**Advantage:** This is cheaper than leased line and still gives great speed.

---

## VPN (Virtual Private Network) — Encrypted Tunnel Inside the Internet

If a company doesn't have money for Leased Line or MPLS, they use the cheapest and best method called VPN.

**How it Works:** These run on the normal internet, but VPN software creates a Secret Tunnel (Encrypted Pipe) between your computer and the office server inside the internet.

When your data passes through this tunnel, even if a hacker (or the ISP itself) catches the packet, they only see Crypto-Garbage because the data is completely locked.

---

## MUST MEMORIZE

- **Leased Line:** Physically dedicated and private wire between two locations (Most expensive, most secure).
- **MPLS:** Technology that puts a Label on packets and sends them through a VIP path on the ISP's shared network.
- **VPN:** Creating a Virtual Private Tunnel using encryption on top of the public internet.

---

## Comparison Table

| Technology | Security | Speed | Cost | Privacy |
|------------|----------|-------|------|---------|
| **Leased Line** | Highest | Highest | Highest | 100% Private |
| **MPLS** | High | High | Medium | Semi-Private |
| **VPN** | High (Encrypted) | Medium | Lowest | Encrypted Tunnel |

---

## Elite Challenge: VPN vs Leased Line

**Scenario:** A hacker sits in an ordinary internet cafe in Lahore and starts capturing all network traffic. In the same cafe, a person is connected to their bank's main server through a VPN and submits their admin password.

1. Since the data is passing through normal internet routers and the hacker has captured the traffic, will the hacker see the manager's password clearly, or only encrypted garbage due to the VPN?
2. If the bank has a lot of money and wants zero compromise on security, should they use VPN or get their own Leased Line?

---

**My Analysis:**

1. The hacker will only see **encrypted garbage**. The VPN creates an encrypted tunnel that protects all data passing through it.

2. The bank should get their own **Leased Line**. When money is not an issue and security is the top priority, a dedicated private line is the best option available.

---

## What I Messed Up Today

Today I learned the three main WAN technologies and their trade-offs:

- **Leased Line:** Maximum security and speed, but very expensive
- **MPLS:** Good balance of security and cost, uses labels for VIP routing
- **VPN:** Cheapest option, uses encryption on public internet

The key insight is that security and cost have a direct relationship. As security increases, cost also increases.

The most important takeaway is that VPN encryption protects data even on public networks, but if an organization has the budget and needs absolute security, a Leased Line is the gold standard.
