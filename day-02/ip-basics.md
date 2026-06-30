# day 2: binary logic and ip basics

today i am learning the true language of computers, which is binary (0 and 1).
> aaj main computer ki buniyaadi zaban seekh raha hoon jise binary kehte hain, ismein sirf 0 aur 1 hota hai.

humans use numbers from 0 to 9, but computers only understand two states.
> insaan 0 se 9 tak ginti use karte hain par computer alag hai, yeh sirf do cheezon ko samajhta hai.

* **1:** power is on (high voltage).
> **1:** bijli on hai (voltage high hai).

* **0:** power is off (low voltage).
> **0:** bijli off hai (voltage low hai).

every single 0 or 1 in networking is called a bit.
> networking ki dunya mein is 0 ya 1 ko ek bit bola jata hai.

---

## the 8-bit base table (the core rule)
> 8-bit ka buniyaadi table aur uske usool

networking works in a group of 8 bits. we call it an octet or a byte.
> networking mein hamesha 8 bits ek sath kaam karte hain, isay octet ya byte kehte hain.

the value doubles from right to left. the numbers are 128, 64, 32, 16, 8, 4, 2, 1.
> seedhe haath se ulte haath ki taraf numbers double hote hain, jaise 128, 64, 32, 16, 8, 4, 2 aur 1.

if we add all numbers: 128+64+32+16+8+4+2+1 it becomes 255.
> agar hum in saare numbers ko jama karte hain toh total 255 banta hai.

so, minimum value is 0 and maximum value is 255 in any octet.
> isiliye ip address ka koi bhi hissa 255 se bada nahi ho sakta, aur sab se chota 0 hota hai.

---

## my binary practice today
> meri aaj ki binary conversion ki practice

i tried to change normal numbers to binary language.
> maine aam numbers ko binary code mein badalne ki koshish ki.

### 1. example for 192
128 + 64 is 192. so code is 11000000.
> 128 aur 64 ko jama karne se 192 banta hai, toh code 11000000 hoga.

### 2. example for 5
4 + 1 is 5. so code is 00000101.
> 4 aur 1 ko jama karne se 5 banta hai, toh code 00000101 hoga.

---

## what i messed up today (meri learning)

today i did a mistake when calculating the binary for number 168.
> aaj maine number 168 ka binary nikalte hue ek choti si galti ki thi.

i wrote 10100100, which means 128 + 32 + 4 = 164. it was wrong.
> maine 10100100 likha tha, jiska matlab 164 ban raha hai. yeh galat tha.

then my ai friend corrected me. for 168, we need 128 + 32 + 8 = 168.
> phir mere ai dost ne meri galti sahi karwayi. 168 ke liye humein 128, 32 aur 8 chahiye.

so the correct binary code for 168 is: 10101000.
> toh 168 ka asli aur sahi binary code 10101000 hai.

i also calculated 255 successfully: 11111111. all bits are on!
> aur maine 255 ka bhi sahi nikala jo 11111111 hai kyunki ismein saare bits on hote hain.
