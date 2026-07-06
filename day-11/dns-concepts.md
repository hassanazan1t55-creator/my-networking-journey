# Day 11: DNS — The Internet's Global Directory Service

Today I am learning about DNS, which translates human-friendly domain names into computer-friendly IP addresses.

Computers only understand numbers (IP addresses like 142.250.181.238), but humans cannot remember IPs for every website. So we remember names like google.com or facebook.com.

DNS is like a global phonebook that matches domain names with their IP addresses.

---

## The DNS Query Process: How Names Become Addresses

When you type google.com in your browser, your computer performs these steps very quickly:

**1. Local Cache Check**
Your computer first checks its own memory (Cache) to see if it has visited google before. If the IP is already saved, the website opens instantly.

**2. ISP Resolver Lookup**
If not found in cache, the request goes to your Internet Service Provider's (like PTCL, Nayatel, StormFiber) DNS resolver.

**3. Root Server Query**
If the ISP also doesn't know, it goes to the world's biggest Root Server (.) and asks: "Where is google.com?" The Root Server says: "I don't know completely, but go to the .com server."

**4. TLD Server Query (Top-Level Domain)**
The .com server says: "Yes, google is registered with me, go to its main server (Authoritative Name Server)."

**5. Authoritative Name Server Response**
This is the final server that gives the exact and correct IP address (142.250.181.238) to your computer, and the website opens!

---

## The Hacker's Mindset vs. Defensive Operations

DNS is the backbone of the entire internet. If a hacker controls DNS, they can redirect the entire internet's traffic!

### 1. The Attack: DNS Cache Poisoning (Name Resolution Hijacking)

**Hacker's Logic:** The hacker thinks: "When a user types mybank.com, their computer will first ask the local DNS cache or router for the IP. If I secretly change the bank's real IP to my fake hacker server's IP in their computer or router's DNS table, what will happen?"

**The Impact:** The user types the correct name (mybank.com), but due to the fake DNS entry, they are sent directly to the hacker's fake banking page. The user won't suspect anything because the URL looks exactly correct, and when they login, their password goes straight to the hacker!

### 2. The Defense: DNSSEC (DNS Security Extensions)

**Defensive Action:** The defender adds digital signatures (cryptographic verification) to DNS packets. When the computer receives the DNS response, it checks whether the signature is from the real server or if a hacker changed it in between. If the signature doesn't match, the computer doesn't go to that IP.

**Cache Clearing Command:** If there is any suspicion that the cache has been poisoned, a command is run on the terminal to clear all old fake data:


---

## DNS Records Analysis: The Hacker's Reconnaissance Tool

DNS has a registry with different types of entries called DNS Records. A hacker checks these records deeply when researching a company.

**A Record (Address Record)**
This connects a domain name to an IPv4 address (e.g., google.com → 142.250.181.238).

**AAAA Record**
This connects a domain name to an IPv6 address.

**MX Record (Mail Exchange)**
This tells where the company's all emails are going.

**Hacker's Vision:** If a hacker wants to send phishing emails to company employees, they check the MX record to find the email server and see if it's old or weak.

**TXT Record (Text Record)**
This contains security settings (like SPF or DKIM rules) that tell who can send emails on behalf of the company and who cannot.

---

## Elite Challenge: Security Certificate Validation

**Scenario:** You are sitting on a company's network and performed a DNS Spoofing attack on their router. You set a rule that whenever any employee opens instagram.com, instead of Instagram they should see a fake image hosted on your laptop.

But when the employee opened their browser and typed instagram.com, your fake page didn't open. Instead, the browser showed a big red error: "Your connection is not private / Security Certificate Invalid".

1. Your DNS spoofing attack was successful (the path changed), but which security feature (from the OSI model's Presentation layer) did the browser use to block your fake page?
2. If you are a defensive expert and suspect someone has put fake DNS entries on your computer, what command do you run on the console to clear the DNS cache?

---

**My Analysis:**

1. The browser blocked the fake page because of **HTTPS / SSL Encryption (Presentation Layer)**. Even though the name was instagram.com, my fake page didn't have Instagram's real and verified Security Certificate (SSL). The browser immediately detected that the path had been changed and protected the user.

2. To clear the DNS cache, I would run: **`ipconfig /flushdns`**

---

## Elite Deep Challenge: The Weakest Link Analysis

**Scenario:** A very big company has top-level security on their website. Their Port 80 (HTTP) and Port 443 (HTTPS) are completely up-to-date, so you cannot directly attack the website.

But you scan the company's DNS records and find their MX Record (Mail Server). The scan reveals that their email server hasn't been updated for 3 years and is running on a very old Windows Server.

**Hacker's Logic:** I will focus on the **email server** because it hasn't been updated for 3 years. It will have many vulnerabilities that can be exploited to gain access to the network.

**Defender's Mistake:** The admin secured their website but completely ignored their email server. This is called the "Weakest Link" — and hackers always exploit the weakest point in the system.

---

## What I Messed Up Today

Today I learned the difference between DORA (DHCP) and the DNS Query process. I initially thought they were similar, but now I understand that DORA is for getting IPs and DNS is for finding IPs from domain names.

I also learned about DNS Records like A, AAAA, MX, and TXT. The MX record is especially important because if the email server is outdated, it can be the weakest point in the company's security.

The key lesson is that DNS Cache Poisoning is dangerous because the user thinks they are going to the right website but are actually being redirected to a hacker's fake site. The only protection is DNSSEC and always checking the SSL certificate.

I also realized that `ipconfig /flushdns` is a command every network defender should know to clear any poisoned DNS cache.
