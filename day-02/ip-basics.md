# Day 2: Binary Logic and IP Addressing Basics

Today I am learning the true language of computers — Binary (0 and 1).

Human brains use numbers from 0 to 9 (the Decimal system). But computers are electronic devices. They only understand two states:

- **1** = Power is ON (High Voltage)
- **0** = Power is OFF (Low Voltage)

In networking, every single 0 or 1 is called a **Bit**.

---

## The 8-Bit Base Table (The Holy Grail of Networking)

In networking, everything is built on groups of 8 bits. We call this an **Octet** or a **Byte**.

The value of each bit doubles from right to left:
**128, 64, 32, 16, 8, 4, 2, 1**

### Mathematical Logic:
If we add all the numbers together: 128 + 64 + 32 + 16 + 8 + 4 + 2 + 1 = 255

This means in networking, the smallest value in any octet is **0** (all bits OFF) and the largest value is **255** (all bits ON). No value can go beyond 255.

---

## How to Convert Decimal to Binary

**Rule:** Look at the numbers in the base table. Pick the ones that add up to the target number. Put a **1** below the numbers you use, and a **0** below the ones you do not use.

### Example 1: Number 192
We need to make 192. Since 128 + 64 = 192, we do not need any other numbers.
* Binary for **192** is: **11000000**

### Example 2: Number 10
We need to make 10. Since 8 + 2 = 10, we only use the 8 and 2 positions.
* Binary for **10** is: **00001010**

---

## Day 2 Task: Binary Conversion Practice

### Challenge Exercises:
1. What is the binary for **192**? (Hint: 128 + 64 = 192)
2. What is the binary for **5**? (Hint: 4 + 1 = 5)

---

## What I Messed Up Today

Today I made a mistake when calculating the binary for the number 168.

I initially wrote **10100100**, which equals 128 + 32 + 4 = 164. That was incorrect.

Then my AI assistant corrected me. For 168, we need 128 + 32 + 8 = 168.
* Correct binary for **168**: **10101000**

### Task Results:
* **255** (All bits ON): **11111111** (Correct)
* **192**: **11000000** (Correct)
* **5**: **00000101** (Correct)

**Lesson Learned:** Mistakes are an essential part of learning. Now my binary conversion logic is solid, and I fully understand how the 8-bit table works.
