# Day 24: Hashing vs Encryption — Secure Password Storage

Today I am learning about Hashing and how websites store passwords securely.

Normal people think passwords are "Encrypted" and stored in databases. But this is completely wrong! In hacking and security, passwords use Hashing. Let's see the real difference between these two.

---

## Encryption (Two-Way Process)

As we learned yesterday, encryption is a Two-Way (reversible) process.

**How it Works:** If you have Plain Text (Clear text), you can use a Key to turn it into Cipher Text (Garbage). And if you have the correct key, you can turn that garbage back into Plain Text.

**Where is it used?** Where data needs to be read back, like VPN tunnels or chat messages (WhatsApp End-to-End Encryption).

---

## Hashing (One-Way Process)

Hashing is a One-Way (irreversible) mathematical function. Once data becomes a hash, there is NO reverse gear!

**How it Works:** It takes data of any size (even one character or a whole book) and turns it into a fixed-length weird code called a Hash Value. NO software or hacker in the world can reverse this hash to get the original password.

**Where is it used?** To store passwords safely in databases and to check data Integrity (to see if data was tampered with).

**Famous Algorithms:** SHA-256, MD5, SHA-512.

---

## Live Example: How Websites Save Passwords

When you create a new account on a website and set password as `Bhai@123`:

**1.** The website does NOT save your real password. It puts `Bhai@123` into a hashing algorithm (e.g., SHA-256).

**2.** A fixed hash is created, like: `5e884898da28047151d0e56f8dc6292773603d0d6aabbdd62a11ef721d1542d8`

**3.** This hash value is stored in the website's database.

**4.** At login: When you enter your password again, the website creates its hash again and matches it with the database hash. If they match, you are logged in!

**Hacker's Nightmare:** Even if a hacker hacks the website's database, they only get hash values (garbage), not real passwords!

---

## The Hacker's Mindset vs. Defensive Operations

### 1. The Attack: Hash Cracking (Brute Force / Dictionary)

**Hacker's Logic:** Since hashes cannot be reversed, the hacker uses a Brute Force Attack or Dictionary Attack (using tools like John the Ripper or Hashcat).

The hacker takes a list of common passwords (like `123456`, `password`, `admin`), creates their SHA-256 hashes, and compares them with the stolen hash.

When a password's hash matches the stolen hash, the hacker says: "Aha! Found the real password!"

**Important:** The hacker did NOT reverse the hash. They just matched Hash with Hash!

### 2. The Attack: Hash Collision (Theoretical Risk)

**Hacker's Logic:** What if a hacker finds a completely different password that produces the SAME hash?

If two different passwords produce the same hash, that's a Hash Collision. The hacker could login using the fake password even without knowing the real one!

**BUT:** Modern algorithms like SHA-256 are designed so collisions are almost impossible. This only happens in old algorithms like MD5 or SHA-1, which are no longer used for passwords.

---

## Encryption vs Hashing (Quick Comparison)

| Feature | Encryption | Hashing |
|---------|-----------|---------|
| **Direction** | Two-Way (Reversible) | One-Way (Irreversible) |
| **Key Needed** | Yes (Key required) | No Key |
| **Can be reversed?** | Yes (with correct key) | No (mathematically impossible) |
| **Used For** | VPN, Chats, Files | Passwords, Integrity Check |
| **Example** | AES, RSA | SHA-256, MD5 |

---

## MUST MEMORIZE

- **Encryption:** Two-Way process (Data can be opened, key needed).
- **Hashing:** One-Way process (Data can never be reversed, no key).
- **SHA-256 / MD5:** Famous hashing functions.
- **Hash Cracking:** Brute force / Dictionary attack (making hashes and matching).
- **Hash Collision:** Two different passwords producing the same hash (almost impossible in modern systems).

---

## Elite Challenge: The Hacker's Dilemma

**Scenario:** A hacker hacks an e-commerce website's database. Users' passwords are stored as SHA-256 hashes. The hacker finds the admin's hash:
`5e884898da28047151d0e56f8dc6292773603d0d6aabbdd62a11ef721d1542d8`

Since hashing cannot be reversed, the hacker cannot directly enter this code on the login page (it expects a real password).

1. What technique will the hacker use to find the real password from this hash?
2. If the hacker finds the real password, did they reverse the hash or do something else?

---

**My Analysis:**

1. The hacker will use a **Brute Force / Dictionary Attack**. They will take common passwords, hash them using SHA-256, and compare the results with the stolen hash.

2. The hacker did **NOT reverse the hash**. They just found a password whose hash matches the stolen one. This is called **Hash Matching**, not reversing.

---

## What I Messed Up Today

Today I learned the critical difference between Encryption and Hashing:

- **Encryption** is Two-Way (can be reversed with a key)
- **Hashing** is One-Way (cannot be reversed, no key)

The key insight is that websites store **hashes of passwords**, not the passwords themselves. This protects users even if the database is stolen.

I also learned about **Hash Collisions** — theoretically, two different passwords could produce the same hash. But modern algorithms like SHA-256 make this practically impossible.

The most important takeaway is that hashing is not encryption. Encryption is for confidentiality (keeping data secret), while hashing is for integrity (verifying data hasn't changed) and password storage.
