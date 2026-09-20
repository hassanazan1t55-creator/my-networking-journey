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

Hash functions are designed to be one-way in the practical sense: there is no general inverse operation that efficiently recovers the original input from a hash. However, an attacker can guess candidate inputs and compare their hashes, which is why password hashing must use a password-specific, deliberately slow scheme.

**How it Works:** A cryptographic hash maps input data to a fixed-length digest. The original input is not recoverable through a simple reverse operation, but weak or predictable passwords can sometimes be recovered by guessing and comparing candidates. Hashing therefore does not make a weak password safe by itself.

**Where is it used?** Hashes are used for integrity checks, fingerprints, signatures, and many other purposes. Passwords should normally be stored with password-hashing/KDF algorithms such as Argon2id, scrypt, or bcrypt rather than plain SHA-256.

**Examples:** SHA-256 and SHA-512 are general-purpose cryptographic hashes. MD5 is considered broken for collision resistance and should not be selected for new security designs.

---

## Live Example: How Websites Save Passwords

When you create a new account on a website and set password as `Bhai@123`:

**1.** The website should not save your plaintext password. It should process the password with a password-hashing function such as Argon2id, scrypt, or bcrypt, using a unique salt.

**2.** The resulting password-hash record includes the algorithm parameters and salt so the server can verify future login attempts without storing the plaintext password.

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
| **Can be reversed?** | Yes (with correct key) | No efficient general inverse; guessing may recover weak inputs |
| **Used For** | VPN, Chats, Files | Password storage/KDFs, Integrity checks, fingerprints |
| **Example** | AES, RSA | SHA-256, MD5 |

---

## MUST MEMORIZE

- **Encryption:** Two-Way process (Data can be opened, key needed).
- **Hashing:** Designed as a one-way process; weak inputs can still be guessed and matched, so secure password storage requires a password-specific KDF and salt.
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

The key insight is that websites should store **password-hash records**, not plaintext passwords. A database breach can still be dangerous, because attackers may attempt offline guessing; unique salts and slow password-hashing functions make that substantially harder.

I also learned about **Hash Collisions** — theoretically, two different passwords could produce the same hash. But modern algorithms like SHA-256 make this practically impossible.

The most important takeaway is that hashing is not encryption. Encryption is for confidentiality (keeping data secret), while hashing is for integrity (verifying data hasn't changed) and password storage.
