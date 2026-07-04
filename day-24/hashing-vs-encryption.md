# Day 24: Hashing vs Encryption

Today i am learning about Hashing and how websites store passwords securely.
> Aaj main Hashing seekh raha hoon aur websites passwords ko secure tareeqe se kaise store karti hain.

Normal people think passwords are "Encrypted" and stored in databases. But this is completely wrong! In hacking and security, passwords use Hashing. Let's see the real difference between these two.
> Aam log samajhte hain ke passwords ko "Encrypt" kar ke database mein rakha jata hai, lekin yeh bilkul galat hai! Hacking aur security ki dunya mein passwords ke liye Hashing ka istemal hota hai. Aao dekhte hain in dono mein asli farq kya hai.

---

## 1. Encryption (Two-Way Traffic)

As we learned yesterday, encryption is a Two-Way (reversible) process.
> Jaisa humne kal parha, encryption ek Two-Way (dono taraf chalne wala) process hai.

**Logic:** If you have Plain Text (Clear text), you can use a Key to turn it into Cipher Text (Garbage). And if you have the correct key, you can turn that garbage back into Plain Text.
> Agar aapke paas ek Plain Text (Clear text) hai, toh aap chabi (Key) laga kar use Cipher Text (Kachra) bana sakte ho. Aur agar sahi chabi ho, toh us kachray ko wapas Plain Text mein badla ja sakta hai.

**Where is it used?** Where data needs to be read back, like VPN tunnels or chat messages (WhatsApp End-to-End Encryption).
> Kahan use hota hai? Jahan data ko wapas parhna zaroori ho, jaise VPN tunnel mein ya chat messages (WhatsApp End-to-End Encryption) mein.

---

## 2. Hashing (One-Way Street — No Reverse)

Hashing is a One-Way (irreversible) mathematical function. Once data becomes a hash, there is NO reverse gear!
> Hashing ek One-Way (sirf ek taraf chalne wala) mathematical function hai. Ek baar data hash ban gaya, toh back-gear nahi lag sakta!

**Logic:** It takes data of any size (even one character or a whole book) and turns it into a fixed-length weird code called a Hash Value. NO software or hacker in the world can reverse this hash to get the original password.
> Yeh kisi bhi size ke data (chahe ek akshar ho ya poori kitaab) ko ek fixed length ke ajeeb se code mein badal deta hai jise Hash Value kehte hain. Dunya ka koi software ya hacker is hash value ko ulta (reverse) kar ke asli password nahi nikal sakta.

**Where is it used?** To store passwords safely in databases and to check data Integrity (to see if data was tampered with).
> Kahan use hota hai? Passwords ko database mein mahfooz rakhne ke liye aur data ki Integrity (Tampering check karne) ke liye.

**Famous Algorithms:** SHA-256, MD5, SHA-512.
> Mashhoor Algorithms: SHA-256, MD5, SHA-512.

---

## 3. Live Example: How Websites Save Passwords

When you create a new account on a website and set password as `Bhai@123`:
> Jab aap kisi website par naya account banate ho aur password rakhte ho `Bhai@123`:

**1.** The website does NOT save your real password. It puts `Bhai@123` into a hashing algorithm (e.g., SHA-256).
> Website aapka asli password save nahi karti. Woh `Bhai@123` ko ek hashing algorithm (e.g., SHA-256) mein daalti hai.

**2.** A fixed hash is created, like: `5e884898da28047151d0e56f8dc6292773603d0d6aabbdd62a11ef721d1542d8`
> Uska ek fixed hash banta hai, jaise: `5e884898da28047151d0e56f8dc6292773603d0d6aabbdd62a11ef721d1542d8`

**3.** This hash value is stored in the website's database.
> Website ke database mein yeh hash value save ho jati hai.

**4.** At login: When you enter your password again, the website creates its hash again and matches it with the database hash. If they match, you are logged in!
> Login ke waqt: Jab aap dobara password enter karte ho, website phir se uska hash banati hai aur database wale hash se match karti hai. Agar dono match ho jayein, toh aap login ho jate ho!

**Hacker's Nightmare:** Even if a hacker hacks the website's database, they only get hash values (garbage), not real passwords!
> Hacker's Nightmare: Agar koi hacker website ka database hack bhi karle, toh use sirf hash values (kachra) milengi, asli passwords nahi!

---

## 4. How Hackers Crack Hashes (Brute Force / Dictionary Attack)

If a hacker gets the hash and wants the real password, they can't reverse it. So what do they do?
> Agar hacker ko hash mil gaya aur use asli password chahiye, toh woh reverse nahi kar sakta. Toh woh kya karta hai?

**Hacker's Trick:** The hacker has a huge list of common passwords (like `123456`, `password`, `admin`). They take each password, create its SHA-256 hash themselves, and compare it with the stolen hash.
> Hacker ke paas aam passwords ki ek badi list hoti hai (jaise `123456`, `password`, `admin`). Woh har password ko le kar khud uska SHA-256 hash banata hai aur stolen hash se match karta hai.

When a password's hash matches the stolen hash, the hacker says: "Aha! Found the real password!"
> Jaise hi kisi password ka hash match ho jata hai, hacker kehta hai: "Aha! Mil gaya asli password!"

**Important:** The hacker did NOT reverse the hash. They just matched Hash with Hash!
> Important: Hacker ne hash reverse nahi kiya. Sirf Hash se Hash match kiya hai!

---

## 5. Advanced Concept: Hash Collision

What if a hacker finds a completely different password that produces the SAME hash?
> Agar hacker koi bilkul alag password dhoond le jiska hash bilkul SAME nikle toh?

**Hash Collision:** If two different passwords produce the same hash, that's a Hash Collision. The hacker could login using the fake password even without knowing the real one!
> Agar do alag alag passwords ka hash ek jaisa ban jaye, toh use Hash Collision kehte hain. Hacker fake password use kar ke login ho sakta hai chahe use asli password na pata ho!

**BUT:** Modern algorithms like SHA-256 are designed so collisions are almost impossible. This only happens in old algorithms like MD5 or SHA-1, which are no longer used for passwords.
> Lekin: Modern algorithms jaise SHA-256 ko is tarah banaya gaya hai ke collisions lagbhag namumkin hain. Yeh sirf purane algorithms jaise MD5 ya SHA-1 mein hota tha, jo ab passwords ke liye use nahi hote.

---

## 6. Encryption vs Hashing (Quick Comparison)

| Feature | Encryption | Hashing |
|---------|-----------|---------|
| **Direction** | Two-Way (Reversible) | One-Way (Irreversible) |
| **Key Needed** | Yes (Key required) | No Key |
| **Can be reversed?** | Yes (with correct key) | No (mathematically impossible) |
| **Used For** | VPN, Chats, Files | Passwords, Integrity Check |
| **Example** | AES, RSA | SHA-256, MD5 |

> Encryption: Two-Way (Reverse ho sakta hai) | Hashing: One-Way (Reverse nahi ho sakta)
> Encryption: Chabi zaroori hai | Hashing: Chabi nahi hoti
> Encryption: Reverse ho sakta hai (sahi chabi se) | Hashing: Reverse nahi ho sakta
> Encryption: VPN, Chats, Files | Hashing: Passwords, Integrity Check
> Encryption: AES, RSA | Hashing: SHA-256, MD5

---

## 7. MUST MEMORIZE

- **Encryption:** Two-Way process (Data can be opened, key needed).
> Two-Way process (Data wapas khul sakta hai, chabi zaroori hoti hai).

- **Hashing:** One-Way process (Data can never be reversed, no key).
> One-Way process (Data kabhi wapas asli shakal mein nahi aa sakta, chabi nahi hoti).

- **SHA-256 / MD5:** Famous hashing functions.
> Mashhoor hashing functions.

- **Hash Cracking:** Brute force / Dictionary attack (making hashes and matching).
> Brute force / Dictionary attack (hash bana kar match karna).

- **Hash Collision:** Two different passwords producing the same hash (almost impossible in modern systems).
> Do alag passwords ka ek hi hash ban jana (modern systems mein namumkin ke barabar).

---

## What I Learned Today

Today I learned Hashing properly. Now I know:
> Aaj maine Hashing sahi se seekh liya. Ab mujhe pata hai:

* Encryption is Two-Way (can be reversed with key)
> Encryption Two-Way hai (key se reverse ho sakta hai)

* Hashing is One-Way (cannot be reversed, no key)
> Hashing One-Way hai (reverse nahi ho sakta, key nahi)

* Websites store password hashes, NOT real passwords
> Websites password hashes store karti hain, asli passwords nahi

* Hackers use Brute Force / Dictionary attack to crack hashes
> Hackers hashes crack karne ke liye Brute Force / Dictionary attack use karte hain

* Hash Cracking = Making hashes of common passwords and matching
> Hash Cracking = Aam passwords ka hash bana kar match karna

* Hash Collision = Two different passwords, same hash (very rare in modern systems)
> Hash Collision = Do alag passwords ka ek hi hash (modern systems mein bohot rare)

* SHA-256 is secure, MD5 is outdated and not safe
> SHA-256 secure hai, MD5 outdated aur safe nahi

> Ab Hashing ka poora game samajh aa gaya hai!
