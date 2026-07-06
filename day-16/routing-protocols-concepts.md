# Day 16: Routing Protocols — The Internet's Global Navigation System

Today I am learning about Routing Protocols, which are like Google Maps for routers to find the best path.

Until now we learned that Routers connect different networks. But think, when millions of routers are connected across the whole world, how do they know which path from Pakistan to America is the fastest?

Routers speak special languages with each other called Routing Protocols. These protocols work like Google Maps for the internet — finding the shortest and best path!

---

## OSPF (Open Shortest Path First) — Internal Network Mapping

OSPF is an Interior Gateway Protocol (IGP). This means it is used to connect routers inside one company, bank, or university.

**How it Works:** OSPF is a "Link-State" protocol. Every router keeps a complete map (topology) of all nearby routers in its memory.

**Shortest Path Algorithm:** It uses a formula called Dijkstra Algorithm to find the fastest path. It looks at bandwidth (speed) — whichever path is fastest, data is sent that way. If one path breaks, it automatically finds another path within 2 seconds!

---

## BGP (Border Gateway Protocol) — The Internet's Core Routing

BGP is an Exterior Gateway Protocol (EGP). This is the real king of the internet! When two big Networks (like PTCL and Google, or Airtel and Facebook) need to connect, BGP is used.

The internet is actually a collection of big networks called Autonomous Systems (AS). BGP connects one AS to another AS.

**How it Works:** BGP doesn't care about speed. It is a Path Vector protocol. It looks at which path has the fewest Autonomous Systems (big networks) to pass through.

Its biggest job is to control the politics (policies and routing rules) of internet traffic.

---

## The Hacker's Mindset vs. Defensive Operations

### 1. The Attack: BGP Hijacking

**Hacker's Logic:** BGP is very old and it blindly trusts other routers without checking. Imagine a hacker takes control of a bad Internet Service Provider's (ISP) router. That router lies to all BGP routers in the world: "The real path to Twitter/X goes through me." All other routers believe it and all Twitter traffic turns toward the hacker's network.

**The Impact:** This is called BGP Hijacking, where the hacker can read traffic of entire countries!

### 2. The Defense: RPKI Authentication

**Defensive Action:** Defenders use RPKI (Resource Public Key Infrastructure) to protect against this trick. This is a system of digital certificates for routing. Now when a router says "I own this IP network", other routers first check the cryptographic certificate to see if it's telling the truth or if it's a hacker.

---

## MUST MEMORIZE

- **OSPF:** Runs inside one organization/company (IGP). Finds path based on Speed (Bandwidth).
- **BGP:** Connects different Autonomous Systems (big ISPs/Networks) together (EGP). The whole internet runs on this.
- **Autonomous System (AS):** A very big group of routers running under one administration. Every AS has a unique number (ASN).

---

## Elite Challenge: Protocol Selection

**Scenario:** A large multi-national company has two offices — one in Lahore and one in Karachi. Each office has 50 routers that talk to each other internally. Their entire network connects to the internet through PTCL using BGP.

1. Which protocol should be used for the 50 routers inside the Lahore office to find the fastest path between themselves — OSPF or BGP?
2. If a hacker wants to steal the company's internet traffic by sending fake routing advertisements, what security should be configured on the routers to verify certificates and catch the hacker's lies?

---

**My Analysis:**

1. **OSPF** should be used inside the office because it's an Interior Gateway Protocol designed for internal routing based on speed and shortest path.

2. **RPKI (Resource Public Key Infrastructure)** should be configured. It uses digital certificates to verify routing claims and detect BGP Hijacking attempts.

---

## What I Messed Up Today

Today I learned the difference between OSPF and BGP:

- **OSPF** is for internal routing (inside one organization) and focuses on speed
- **BGP** is for external routing (between organizations) and focuses on policies and path selection

I also learned about BGP Hijacking, where a malicious router advertises false paths to redirect traffic. This is a serious threat because BGP trusts other routers by default.

The most important takeaway is that RPKI provides cryptographic verification for routing, making it much harder for hackers to perform BGP Hijacking.

The internet is literally held together by BGP, and securing it with RPKI is critical for preventing large-scale traffic interception.
