# Day 26: IDS/IPS Evasion — Bypassing Network Security Controls

Today I am learning about IDS/IPS Evasion techniques, how hackers trick security systems.

When an advanced IPS is sitting on the network, if a hacker sends a direct attack packet, the IPS will recognize its signature and block it. So hackers use Evasion techniques. Let's understand their packet-level logic:

---

## IP Fragmentation (Breaking Into Pieces)

This is the most famous and basic evasion technique.

**How it Works:** IPS checks packets when they are complete. If the hacker breaks their malicious payload (attack code) into small pieces (Fragments) and sends them separately over the network, each small piece looks completely normal.

**How the Trick Works:** The IPS doesn't have a signature for each small packet, so it lets them through. When all these pieces reach the target computer, the target computer's Operating System reassembles them and the attack executes!

**Modern Fix:** Modern IPS now capture packets and reassemble them first, then check. But this puts more load on the IPS.

---

## Out-of-Order Packets (Sending in Wrong Sequence)

This is an advanced version of fragmentation that plays with TCP's brain.

**How it Works:** The hacker fragments the attack, but instead of sending the pieces in sequence, they send them out of order (e.g., Packet 3 first, then Packet 1, then Packet 2).

**How the Trick Works:** The IPS gets confused and if its memory/buffer is small, it can't understand the real meaning of these out-of-order packets and lets them through. When they reach the target computer, it uses the TCP Sequence Numbers to reassemble them perfectly!

---

## Obfuscation & Encoding (Changing the Shape)

If the IPS is looking for a specific word or string (like `/etc/passwd` or `cmd.exe`), the hacker changes its encoding.

**How it Works:** The hacker changes the text using URL Encoding, Hex Encoding, or Base64.

**Example:** The word `admin` can be URL encoded as `%61%64%6d%69%6e`. If the IPS only checks normal English text, it will think this is safe and let it through, but the web server will decode it and understand `admin`!

---

## TTL Evasion / Insertion Attack (Advanced Trick)

This is the technique you solved in the task!

**How it Works:** The hacker inserts a fake packet between the real fragments with a very low TTL (Time-to-Live), so it dies (drops) before reaching the target.

**How the Trick Works:** The IPS sees ALL packets (including the fake one) and reassembles them to check. The IPS sees the fake word and thinks it's normal traffic. But the target computer never receives the fake packet (it dropped), so it reassembles only the real fragments and the attack executes!

---

## MUST MEMORIZE

- **IP Fragmentation:** Breaking attack packets into small pieces so IPS can't match signatures.
- **Out-of-Order:** Sending packets in wrong sequence and reassembling using TCP on the target.
- **Obfuscation:** Changing attack payload encoding (Hex/URL) so text-matching signatures fail.
- **TTL Evasion / Insertion Attack:** Inserting a fake packet with low TTL that drops before target, confusing the IPS but not the target.

---

## Elite Challenge: The TTL Insertion Attack

**Scenario:** A hacker uses IP Fragmentation to bypass an advanced IPS. They split the attack into two fragments:

- Packet 1 contains: **LI**
- Packet 2 contains: **NUX**

On the target system, they combine to form: **LINUX** (Assume LINUX is a banned signature).

The hacker inserts a Fake Packet between the two fragments containing **WINDOWS** with TTL (Time-to-Live) set to 1, so it drops (dies) on the way and never reaches the target computer.

1. If the IPS reassembles and checks all packets along the way, what word will it see (LINUX or LIWINDOWSNUX)?
2. When these packets reach the target computer (where the fake packet has already dropped), what word will the target receive? Will the attack execute?

---

**My Analysis:**

1. The IPS will see **LIWINDOWSNUX** because it reassembles all packets including the fake one. It will think this is normal safe text and let it through.

2. The target computer will only receive **LI** and **NUX** because the WINDOWS packet dropped before reaching it. The target will reassemble them as **LINUX** and the attack will **execute successfully**!

This technique is called **TTL Evasion** or **Insertion Attack** — a master-level evasion technique used by elite hackers.

---

## What I Messed Up Today

Today I learned the three main IDS/IPS evasion techniques and their logic:

- **IP Fragmentation:** Breaking attacks into small pieces to bypass signature detection
- **Out-of-Order:** Sending pieces in wrong sequence to confuse the IPS
- **Obfuscation:** Changing encoding (Hex/URL) to avoid text-matching
- **TTL Evasion:** Inserting a fake packet with low TTL to trick the IPS while the target receives only the real attack

The key insight is that IPS systems have limitations — they must balance security with performance. Evasion techniques exploit these limitations.

The most important takeaway is that modern IPS systems use Deep Packet Inspection and packet reassembly to counter these techniques, but they come with a performance cost.

The TTL Insertion Attack is particularly clever because the IPS sees the fake packet (and gets fooled), but the target never sees it (so it reassembles the real attack).
