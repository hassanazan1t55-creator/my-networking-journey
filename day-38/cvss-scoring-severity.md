# Day 38: CVSS Scoring & Bug Severity Logic

Today I am learning about CVSS (Common Vulnerability Scoring System), the international standard for rating vulnerability severity.

In big companies, vulnerabilities are not randomly called "small" or "big." There is an international standard scale called CVSS.

CVSS assigns every vulnerability a mathematical score from 0.0 to 10.0, determining its exact severity.

---

## Severity — 4 Main Categories

CVSS scores divide vulnerabilities into four categories:

1. **Low (0.1 - 3.9):** Minor issues that don't pose a direct threat to the company (e.g., server version being publicly visible).

2. **Medium (4.0 - 6.9):** Some risk exists, but the attacker needs many conditions to exploit it.

3. **High (7.0 - 8.9):** Dangerous flaws that can leak sensitive data (e.g., Stored XSS or IDOR).

4. **Critical (9.0 - 10.0):** The most destructive flaws! Attackers can gain full control of the server without any password (e.g., secure configuration flaws or direct code execution).

---

## How the Score is Calculated — The Main Factors

CVSS scores are not random. Three main metrics are evaluated:

**Attack Vector (AV):** Where does the hacker need to be to launch the attack? If it can be done remotely over the internet, the score is high. If physical access to the server is required, the score is low.

**Attack Complexity (AC):** How easy is the attack? If it can be done with one click, complexity is LOW (meaning risk is HIGH).

**Impact (C-I-A):** How does this flaw affect Confidentiality (data theft), Integrity (data modification), and Availability (server downtime)?

---

## The Balancing Act — Exploitability vs Impact

A vulnerability's CVSS score is determined by balancing two factors:

- **Exploitability:** How easy is it to launch the attack?
- **Impact:** How much damage can the attack cause?

**The Elite Rule:** A bug cannot be Critical (9.0 - 10.0) or High unless BOTH Exploitability AND Impact are high. If one factor is weak, the score drops automatically.

---

## MUST MEMORIZE (Day 38 Summary)

1. **CVSS:** Common Vulnerability Scoring System (Scale: 0.0 to 10.0).

2. **Critical Score:** Flaws between 9.0 and 10.0 are considered Critical, and companies fix them first.

3. **Metrics Logic:** The score depends not just on the flaw itself, but on how easy it is to exploit and how much damage it can cause.

---

## Analytical Concept Check

**Scenario:** You find two different vulnerabilities on a website:

**Flaw A:** The entire database's sensitive data can be leaked, but to execute this attack, the hacker must first know the website's "Admin Password" (High Complexity).

**Flaw B:** Only normal images can be deleted, but this attack can be done by any normal person on the internet in 2 seconds without any password (Low Complexity).

1. Which flaw has the more dangerous impact, and which one should have the higher CVSS base score from a business risk perspective?
2. In a professional environment, is "high damage" alone enough, or does "ease of attack" affect the score?

---

**My Analysis:**

1. **Flaw A** has the more dangerous impact (database leak), but its high complexity lowers the CVSS score. **Flaw B** has low impact (only images) but is extremely easy to exploit.

2. **Both factors matter.** The CVSS score is a balance of Exploitability (how easy) and Impact (how bad). If one factor is weak, the score drops automatically.

- **Flaw A:** High Impact + High Complexity → High Severity (7.0 - 8.9)
- **Flaw B:** Low Impact + Low Complexity → Medium Severity (5.0 - 6.5)

---

## Summary Check

| Flaw | Exploitability (Ease) | Impact (Damage) | Professional CVSS Result |
|------|----------------------|-----------------|--------------------------|
| Flaw A |  Difficult (Admin Req) |  Max (Data Leak) | High Severity |
| Flaw B |  Easy (No Password) |  Min (Images Only) | Medium Severity |

---

## What I Messed Up Today

Today I learned the complete CVSS scoring logic:

- **CVSS is the industry standard** for rating vulnerability severity.
- **Scores range from 0.0 to 10.0**, divided into Low, Medium, High, and Critical categories.
- **Three main metrics** determine the score: Attack Vector, Attack Complexity, and Impact (C-I-A).

The key insight is that **professional vulnerability scoring is a balance of exploitability and impact**. A flaw is not scored purely on damage potential — ease of exploitation matters equally.

The most important takeaway is that **Critical severity (9.0 - 10.0) requires both high impact AND low complexity**. If an attack is difficult to execute, the score drops regardless of potential damage.
