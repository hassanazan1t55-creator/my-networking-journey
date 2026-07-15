# Day 35: IDOR & Broken Access Control — Authorization Logic Flaws

Today I am learning about IDOR (Insecure Direct Object Reference) and Broken Access Control, two critical web application vulnerabilities.

In web application security, there are two important concepts:

1. **Authentication:** Proving to the target website who you are (e.g., logging in).
2. **Authorization:** The system deciding what you are allowed to see or do.

When the backend application fails to properly enforce authorization checks, vulnerabilities like Broken Access Control and IDOR arise.

---

## IDOR — What It Is

IDOR occurs when a website uses direct identifiers (like User IDs, Invoice Numbers) in URLs or parameters to access database records, and the backend server does NOT check whether the requester is the actual owner of that record.

**Practical Logic Example:**

Imagine you view your profile on a website and the URL looks like:

`https://example.com/profile?user_id=1005`

**The Flaw:** The server fetches and displays data for `user_id=1005` without verifying the user's session.

**The Attack:** If a user changes the ID in the URL to `user_id=1006`, and the backend system displays another user's private details (email, phone, address) without verifying identity, that's IDOR.

---

## Real-Life Example: Bank Passbook

Imagine you walk into a bank and say:

"Give me my Bank Passbook (account details)."

**Secure System:** The bank clerk asks for your ID Card or fingerprint. Only after confirming you are the account holder do they give you the passbook.

**IDOR Flaw:** The bank clerk doesn't ask for any ID! You say "Give me Account #101 passbook" and they hand it over. You say "Give me Account #102 passbook" and they give you someone else's passbook without asking!

On websites, when the backend server gives data based only on the Account Number (URL Parameter) without checking the ID Card (Session), that's IDOR.

---

## Why Hiding File Names (Hash/Obscurity) Is Not Enough

If a developer simply hashes the filename (e.g., changing `receipt_101.pdf` to `a8f5c89a.pdf`), this is **Security through Obscurity** — just hiding the file name.

If the backend server doesn't check ownership, then as soon as someone discovers the hashed filename, the server will happily serve the file.

**The Correct Approach:** The backend must always verify from the session cookie/token whether the logged-in user is the actual owner of the requested resource.

---

## Real-World Risk & Impact

Ethical hackers, pentesters, and organizations look for IDOR because the risk is severe:

### 1. Data Theft (Mass Leakage / Privacy Breach)

**Example:** A medical app has report URLs like `app.com/report?id=500`.

**Risk:** If IDOR exists, anyone can write a script to change the ID from 1 to 100000 and download thousands of users' private medical reports in one night!

### 2. Unauthorized Account Actions (Modifying Others' Data)

**Example:** An address change request `POST /update_address` sends `user_id=88` as a parameter.

**Risk:** Due to IDOR, a user can change `user_id=89` and modify another user's home address, phone number, or email without knowing their password.

### 3. Financial Loss

**Example:** An e-commerce website has IDOR on order invoice downloads.

**Risk:** People can download others' purchased digital products, receipts, or sensitive tickets.

---

## Secure Web Development — How to Prevent IDOR

Developers prevent IDOR through proper backend authorization architecture:

### 1. Session-Based Backend Authorization
The server should NEVER trust frontend parameters (`user_id=1005`). Instead, it should always extract the user ID from the logged-in user's Session Cookie / Token:

`// Secure Logic: Use current session ID $current_user = $_SESSION['user_id'];`

### 2. Indirect References (Hashes / UUIDs)
Instead of direct sequential numbers (1, 2, 3...), use random unique strings (UUIDs like `f81d4fae-7dec-11d0-a765-00a0c91e6bf6`) so attackers can't increment IDs to guess them.

---

## MUST MEMORIZE (Day 35 Summary)

1. **Authentication vs Authorization:** Authentication checks identity (who you are); Authorization checks permissions (what you can do). IDOR is an Authorization flaw.

2. **IDOR Root Cause:** No ownership check between the user session context and the requested object/resource in the backend.

3. **Primary Defense:**
   - **Backend-level access control checks:** Always verify if the session user owns the requested resource.
   - **Use unpredictable UUIDs instead of sequential IDs.**

---

## Analytical Concept Check

**Scenario:** An e-commerce website has receipt download URLs like:

`https://shop.com/download_receipt.php?file=receipt_101.pdf`

The developer changes the filename to a secure hash to prevent numeric guessing:

`https://shop.com/download_receipt.php?file=a8f5c89a.pdf`

1. Does simply hashing/randomizing the file name completely eliminate IDOR, or is this just a temporary hide-and-seek method (Security through Obscurity)?
2. If a user somehow discovers the hashed file name, what should the backend server check before allowing the download?

---

**My Analysis:**

1. Hashing the filename is just **Security through Obscurity** (temporary hiding). It does NOT fix IDOR.

2. The backend server should check:
   - Who is the logged-in user (from session cookie/token)?
   - Is this user the actual owner of the requested file?
   - Only if ownership is confirmed should the download be allowed.

---

## What I Messed Up Today

Today I learned the complete IDOR attack chain:

- **Why it happens:** Backend servers blindly trust frontend parameters (IDs, filenames) without verifying ownership.
- **How it's exploited:** Attackers change IDs/parameters to access or modify unauthorized resources.
- **Real-world impact:** Mass data theft, privacy breaches, account takeovers, financial loss.

The key insight is that **Authorization is about ownership**, not just authentication. Even if a user is logged in, they shouldn't be able to access resources they don't own.

The most important takeaway is that **Security through Obscurity is not security** — hashing filenames without backend ownership checks is just delaying the inevitable. Always verify ownership at the backend level.
