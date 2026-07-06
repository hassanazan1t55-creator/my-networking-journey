# Day 1: Computer Network Architecture

Today I am learning the core architecture of computer networks.

A network connects two or more devices to process and share data.

The real purpose of a network is resource sharing and distributed computing.

---

## Network Classification (LAN vs WAN)

**LAN (Local Area Network):** This is for small areas like a house or an office. It is very fast.

**WAN (Wide Area Network):** This connects multiple LANs across cities or countries. The internet is the best example.

---

## Network Topologies and Weak Points

### 1. Bus Topology
All computers connect to a single main cable called the backbone.

**Flaw:** If the main cable breaks, the entire network goes down instantly.

### 2. Star Topology
All devices connect to a central device called a switch.

**Flaw:** If the central switch fails, the whole network stops working.

### 3. Mesh Topology
Every computer is directly connected to every other computer. It has high redundancy.

---

## Day 1 Task: Bank Network Design Scenario

**Scenario:** Design a network for a bank where downtime can cause millions of dollars in losses. Should we use star or mesh topology?

### My Analysis and Solution:

For critical bank infrastructure, i will use a **mesh topology** for the core system.

In Star topology, if the central switch fails, everything goes down. This is too risky.

Mesh topology provides alternative paths. If one wire fails, data automatically takes another route.

For better efficiency, we can connect normal employee PCs using **star topology**, but core servers must use **mesh topology**.

---

## What I Messed Up Today

Initially, i thought mesh topology is always best for everything because it is safe.

But then i realized it is very expensive and difficult to manage for a whole building. That is why a hybrid layout is better.
