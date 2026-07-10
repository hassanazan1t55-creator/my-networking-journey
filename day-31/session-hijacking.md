# Day 31: Session Hijacking — TCP Sequence Prediction Attack

Today I am learning about Session Hijacking, where a hacker takes over an active session between a user and a server.

When you log in to a website or server, you don't have to enter your username and password every time because your computer and the server create a Session together. If a hacker enters that active session and takes your place, that's called Session Hijacking.

Let's understand the most dangerous and architectural-level attack — TCP Sequence Prediction.

---

## TCP Session Hijacking — The Sequence Number Game

As we learned on Day 22, TCP protocol puts a Sequence Number (SEQ) and Acknowledgment Number (ACK) on every packet to ensure data arrives in the correct order.

If a hacker can figure out the mathematical pattern of sequence numbers between two computers (User and Server), they can hijack the active connection.

**Attack Step-by-Step Logic:**

1. **Sniffing:** The hacker first uses MITM (ARP Poisoning) to track packets flowing between the User and Server.

2. **Prediction:** The hacker observes that the last packet had SEQ = 1000 and data size = 50 bytes, so the next expected sequence number will be 1050.

3. **The Desynchronization Attack:** The hacker sends a fake RST (Reset) packet to the User's computer to temporarily disconnect or freeze it.

4. **The Hijack (Identity Theft):** The hacker spoofs the User's IP and sends a new packet to the server with the exact expected sequence number (1050) that the server was waiting for from the user!

5. **Result:** The server thinks this packet is still from the same user, and starts accepting the hacker's packets without asking for any password!

---

## Application Layer Hijacking — Cookie Stealing

This happens in web applications where HTTP Session Cookies are used instead of TCP sequence numbers.

**The Logic:** When you log in to Facebook or Gmail, the server saves a unique token (Cookie) in your browser like `SessionID=XYZ123`.

**The Attack:** The hacker steals your SessionID through XSS (Cross-Site Scripting) or packet sniffing. Then the hacker sets that same SessionID in their own browser. The server thinks it's you, and the hacker enters your account without a password!

---

## MUST MEMORIZE

- **TCP Session Hijacking:** Entering an active TCP connection by predicting expected Sequence Numbers.
- **Desynchronization:** Temporarily disconnecting the real user from the network so the server only focuses on the hacker's packets.
- **Defense (Protection):** The best way to protect against this attack is to use IPSec (Network layer encryption) or TLS/HTTPS. Even if the hacker changes the sequence number, they won't be able to create encrypted data.

---

## Elite Challenge: The ACK Storm Phenomenon

**Scenario:** A hacker performs TCP Session Hijacking between a server and a user. They successfully desynchronize (disconnect) the user and send a malicious packet to the server with the exact expected sequence number. Then the hacker turns the user's internet back on.

1. When the real user's computer becomes active again and sends its old sequence number to the server (which the hacker already used), what will the server's reaction be?
2. In this situation, a major network phenomenon called ACK Storm occurs. Why does this ACK Storm happen and what impact does it have on the network?

---

**My Analysis:**

1. **Server's Reaction:** The server will get completely confused! The hacker already used that sequence number and moved forward. From the server's perspective, that sequence number is now old (expired). The server will reject the user's packet and send back: "Bro, you're behind, I need this new sequence number instead!" (No 404 error — the browser will just hang or spin).

2. **ACK Storm:** When the server tells the user "Give me a new sequence number", the user's computer thinks the server has gone crazy. The user sends another ACK saying "No bro, my sequence number is this!" The server replies again saying "No, you're wrong, listen to me!" This creates a Ping-Pong Loop — both computers start flooding each other with ACK packets trying to correct the sequence numbers. Within seconds, thousands of fake ACK packets travel across the network, jamming the bandwidth and causing a DoS (Denial of Service). This is called an **ACK Storm**.

---

## Summary Check

- **Session Hijacking Error:** No 404 error appears. The connection freezes due to data desynchronization.
- **ACK Storm:** The continuous packet fight (loop) between User and Server when sequence numbers don't match.

---

## What I Messed Up Today

Today I learned the complete TCP Session Hijacking attack chain:

- **Sniffing:** Capturing packets to observe sequence numbers
- **Prediction:** Calculating the next expected sequence number
- **Desynchronization:** Removing the real user from the connection
- **Hijack:** Taking over the session with the predicted sequence number

The key insight is that this attack works because TCP sequence numbers are predictable. Even worse, when the real user comes back, both sides get confused and start an ACK Storm — flooding the network with packets.

The most important takeaway is that **encryption (IPSec/TLS)** is the only real defense. Even if a hacker predicts the sequence number, they can't create encrypted data that the server will accept.
