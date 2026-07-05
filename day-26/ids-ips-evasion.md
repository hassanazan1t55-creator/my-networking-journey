# Day 26: IDS/IPS Evasion

Today i am learning about IDS/IPS Evasion techniques, how hackers trick security systems.
> Aaj main IDS/IPS Evasion techniques seekh raha hoon, hackers security systems ko kaise dhoka dete hain.

When an advanced IPS is sitting on the network, if a hacker sends a direct attack packet, the IPS will recognize its signature and block it. So hackers use Evasion techniques. Let's understand their packet-level logic:
> Jab network mein ek advanced IPS laga ho, toh hacker agar direct koi attack packet bhejega, toh IPS uska signature pehchan kar use block kar dega. Is liye hackers Evasion (Bach nikalne ki) techniques istemal karte hain. Aao inka packet-level logic samajhte hain:

---

## 1. IP Fragmentation (Tukray Tukray Kar Do)

This is the most famous and basic evasion technique.
> Yeh sab se mashhoor aur buniyadi evasion technique hai.

**The Logic:** IPS checks packets when they are complete. If the hacker breaks their malicious payload (attack code) into small pieces (Fragments) and sends them separately over the network, each small piece looks completely normal.
> IPS packets ko check karta hai jab woh poore hote hain. Agar hacker apne malicious payload (attack code) ko chote-chote tukron mein torh de (Fragment kar de) aur unhein network par alag-alag bheje, toh har ek chota tukra dekhne mein bilkul normal lagega.

**How the Trick Works:** The IPS doesn't have a signature for each small packet, so it lets them through. When all these pieces reach the target computer, the target computer's Operating System reassembles them and the attack executes!
> IPS ke paas har chote packet ka koi signature nahi hota, isliye woh unhein guzarne deta hai. Jab yeh saare tukray target computer par pahunchte hain, toh target computer ka Operating System unhein wapas jorh (reassemble) leta hai aur attack chal jata hai!

**Modern Fix:** Modern IPS now capture packets and reassemble them first, then check. But this puts more load on the IPS.
> Modern IPS ab packets ka rasta rokh kar pehle unhein khud reassemble karte hain, phir check karte hain. Lekin isse IPS par load barh jata hai.

---

## 2. Out-of-Order Packets (Aage-Peeche Bhejna)

This is an advanced version of fragmentation that plays with TCP's brain.
> Yeh fragmentation ka hi ek advanced roop hai jahan TCP ke dimaag ke sath khela jata hai.

**The Logic:** The hacker fragments the attack, but instead of sending the pieces in sequence, they send them out of order (e.g., Packet 3 first, then Packet 1, then Packet 2).
> Hacker attack ke tukray toh karta hai, lekin unhein sequence mein bhejne ki bajaye aage-peeche bhejta hai (e.g., Pehle Packet 3, phir Packet 1, phir Packet 2).

**How the Trick Works:** The IPS gets confused and if its memory/buffer is small, it can't understand the real meaning of these out-of-order packets and lets them through. When they reach the target computer, it uses the TCP Sequence Numbers to reassemble them perfectly!
> IPS confuse ho jata hai aur agar uski memory/buffer chota ho, toh woh un aage-peeche aane wale packets ka asli matlab nahi samajh pata aur unhein chord deta hai. Target computer ke paas jab yeh pahunche hain, toh woh unke TCP Sequence Numbers ko dekh kar unhein bilkul sahi tarah jorh leta hai.

---

## 3. Obfuscation & Encoding (Shakal Badal Dena)

If the IPS is looking for a specific word or string (like `/etc/passwd` or `cmd.exe`), the hacker changes its encoding.
> Agar IPS kisi specific word ya string (jaise `/etc/passwd` ya `cmd.exe`) ko dhoond raha hai, toh hacker uski coding hi badal deta hai.

**The Logic:** The hacker changes the text using URL Encoding, Hex Encoding, or Base64.
> Hacker text ko URL Encoding, Hex Encoding, ya Base64 mein badal deta hai.

**Example:** The word `admin` can be URL encoded as `%61%64%6d%69%6e`. If the IPS only checks normal English text, it will think this is safe and let it through, but the web server will decode it and understand `admin`!
> Misal: Word `admin` ko hacker URL encode kar ke `%61%64%6d%69%6e` bana kar bhej sakta hai. Agar IPS sirf normal english text check kar raha hai, toh woh isay safe samajh kar jaane dega, jabki web server isay decode kar ke `admin` samajh lega.

---

## 4. TTL Evasion / Insertion Attack (Advanced Trick)

This is the technique you solved in the task!
> Yeh woh technique hai jo aapne task mein solve ki!

**The Logic:** The hacker inserts a fake packet between the real fragments with a very low TTL (Time-to-Live), so it dies (drops) before reaching the target.
> Hacker real fragments ke darmayan ek fake packet daalta hai jiska TTL (Time-to-Live) bohot low hota hai, taake woh target tak pahunchne se pehle hi drop ho jaye.

**How the Trick Works:** The IPS sees ALL packets (including the fake one) and reassembles them to check. The IPS sees the fake word and thinks it's normal traffic. But the target computer never receives the fake packet (it dropped), so it reassembles only the real fragments and the attack executes!
> IPS ko saare packets (fake wala bhi) dikhte hain aur woh unhein reassemble kar ke check karta hai. IPS ko fake word dikhta hai aur woh normal traffic samajh leta hai. Lekin target computer ko fake packet kabhi milta hi nahi (woh drop ho gaya), toh woh sirf real fragments ko jorh kar attack execute kar deta hai!

---

## 5. MUST MEMORIZE (Zubani Yaad Rakho)

- **IP Fragmentation:** Breaking attack packets into small pieces so IPS can't match signatures.
> Attack packet ko chote tukron mein torhna taake IPS signature match na kar sake.

- **Out-of-Order:** Sending packets in wrong sequence and reassembling using TCP on the target.
> Packets ko galat sequence mein bhejna aur target par TCP ke zariye reassemble karwana.

- **Obfuscation:** Changing attack payload encoding (Hex/URL) so text-matching signatures fail.
> Attack payload ki encoding (Hex/URL) badal dena taake text-matching signatures fail ho jayein.

- **TTL Evasion / Insertion Attack:** Inserting a fake packet with low TTL that drops before target, confusing the IPS but not the target.
> Fake packet daalna jiska TTL low ho taake woh target se pehle drop ho jaye, IPS confuse ho jaye lekin target ko farq na pare.

---

## 6. IPS Evasion Techniques (Quick Recap)

| Technique | How It Works | What IPS Sees | What Target Gets |
|-----------|--------------|---------------|------------------|
| **Fragmentation** | Split attack into small packets | Normal fragments | Reassembled attack |
| **Out-of-Order** | Send fragments in wrong order | Confused, may pass | Reassembled in correct order |
| **Obfuscation** | Change encoding (Hex/URL) | Safe-looking text | Decoded attack |
| **TTL Evasion** | Insert fake packet with low TTL | Normal text (with fake) | Attack (without fake) |

> Fragmentation: Attack ko chote tukron mein torhna | IPS ko normal fragments dikhte hain | Target ko reassembled attack milta hai
> Out-of-Order: Tukron ko galat sequence mein bhejna | IPS confuse ho jata hai | Target correct order mein reassemble kar leta hai
> Obfuscation: Encoding badalna (Hex/URL) | IPS ko safe-looking text dikhta hai | Target decoded attack receive karta hai
> TTL Evasion: Fake packet daalna low TTL ke sath | IPS ko fake word dikhta hai | Target ko fake packet nahi milta, sirf attack milta hai

---

## What I Learned Today

Today I learned IDS/IPS Evasion techniques properly. Now I know:
> Aaj maine IDS/IPS Evasion techniques sahi se seekh liya. Ab mujhe pata hai:

* IPS checks complete packets for attack signatures
> IPS complete packets ko attack signatures ke liye check karta hai

* Fragmentation splits attack into small pieces to bypass IPS
> Fragmentation attack ko chote tukron mein torh kar IPS ko bypass karta hai

* Out-of-Order sends fragments in wrong sequence to confuse IPS
> Out-of-Order tukron ko galat sequence mein bhej kar IPS ko confuse karta hai

* Obfuscation changes encoding (Hex/URL) to avoid text-matching
> Obfuscation encoding (Hex/URL) badal kar text-matching se bachta hai

* TTL Evasion inserts fake packet with low TTL that drops before target
> TTL Evasion fake packet daalta hai jiska TTL low ho, woh target se pehle drop ho jata hai

* IPS sees ALL packets (including fake), target sees only real packets
> IPS ko saare packets dikhte hain (fake wala bhi), target ko sirf real packets milte hain

* Modern IPS reassembles packets before checking, but this increases load
> Modern IPS packets ko pehle reassemble kar ke check karta hai, lekin isse load barh jata hai

> Ab IDS/IPS Evasion ka poora game samajh aa gaya hai!
