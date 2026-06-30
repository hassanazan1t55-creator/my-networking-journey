# Day 2: Binary Logic and IP Basics

Today i am learning the true language of computers, which is binary (0 and 1).
> Aaj main computer ki buniyaadi zaban seekh raha hoon jise binary kehte hain, ismein sirf 0 aur 1 hota hai.

Humans use numbers from 0 to 9, but computers only understand two states.
> Insaan 0 se 9 tak ginti use karte hain par computer alag hai, yeh sirf do cheezon ko samajhta hai.

* **1:** Power is on (high voltage).
> **1:** Bijli on hai (voltage high hai).

* **0:** Power is off (low voltage).
> **0:** Bijli off hai (voltage low hai).

Every single 0 or 1 in networking is called a bit.
> Networking ki dunya mein is 0 ya 1 ko ek bit bola jata hai.

---

## The 8-Bit Base Table (The Core Rule)
> 8-bit ka buniyaadi table aur uske usool

Networking works in a group of 8 bits. we call it an octet or a byte.
> Networking mein hamesha 8 bits ek sath kaam karte hain, isay octet ya byte kehte hain.

The value doubles from right to left. the numbers are 128, 64, 32, 16, 8, 4, 2, 1.
> Seedhe haath se ulte haath ki taraf numbers double hote hain, jaise 128, 64, 32, 16, 8, 4, 2 aur 1.

If we add all numbers: 128+64+32+16+8+4+2+1 it becomes 255.
> Agar hum in saare numbers ko jama karte hain toh total 255 banta hai.

So, minimum value is 0 and maximum value is 255 in any octet.
> Isiliye ip address ka koi bhi hissa 255 se bada nahi ho sakta, aur sab se chota 0 hota hai.

---

## My Binary Practice Today
> Meri aaj ki binary conversion ki practice

I tried to change normal numbers to binary language.
> Maine aam numbers ko binary code mein badalne ki koshish ki.

### 1. Example for 192
128 + 64 is 192. so code is 11000000.
> 128 aur 64 ko jama karne se 192 banta hai, toh code 11000000 hoga.

### 2. Example for 5
4 + 1 is 5. so code is 00000101.
> 4 aur 1 ko jama karne se 5 banta hai, toh code 00000101 hoga.

---

## What I Messed Up Today (Meri Learning)

Today i did a mistake when calculating the binary for number 168.
> Aaj maine number 168 ka binary nikalte hue ek choti si galti ki thi.

I wrote 10100100, which means 128 + 32 + 4 = 164. it was wrong.
> Maine 10100100 likha tha, jiska matlab 164 ban raha hai. yeh galat tha.

Then my ai friend corrected me. for 168, we need 128 + 32 + 8 = 168.
> Phir mere ai dost ne meri galti sahi karwayi. 168 ke liye humein 128, 32 aur 8 chahiye.

So the correct binary code for 168 is: 10101000.
> Toh 168 ka asli aur sahi binary code 10101000 hai.

I also calculated 255 successfully: 11111111. all bits are on!
> Aur maine 255 ka bhi sahi nikala jo 11111111 hai kyunki ismein saare bits on hote hain.
