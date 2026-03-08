# CAP Theorem (Consistency, Availability, Partition Tolerance)

### 1. Definition

The **CAP Theorem** states that in a **distributed system**, it is impossible to simultaneously guarantee all three properties:

* **Consistency (C)**
* **Availability (A)**
* **Partition Tolerance (P)**

When a **network partition occurs**, a distributed system must choose **either Consistency or Availability**, but **cannot provide both**.

This theorem was proposed by **Eric Brewer** and later formally proven.

---

# 1. Consistency (C)

### Definition

**Consistency** means that **all nodes return the same latest data**.

After a write operation, **every read request receives the most recent value**.

### Example

Suppose a user updates their email in a distributed database.

```
User updates email → user@gmail.com → user_new@gmail.com
```

With **Consistency**:

* Every server must return **[user_new@gmail.com](mailto:user_new@gmail.com)**
* No server should return the old value.

### Real-world example

Banking systems.

If your balance becomes:

```
₹10,000 → ₹5,000
```

Every server must show **₹5,000 immediately**.

Showing the old balance could cause **serious financial issues**.

---

# 2. Availability (A)

### Definition

**Availability** means that **every request receives a response**, even if the response may contain **stale (old) data**.

The system **never refuses a request**.

### Example

If a user checks their social media likes:

* One server might say **100 likes**
* Another server might say **102 likes**

Both respond successfully.

Even if the data is **not the latest**, the system remains **available**.

### Real-world example

Social media platforms like timelines or likes.

Small inconsistencies are acceptable, but **service must always respond**.

---

# 3. Partition Tolerance (P)

### Definition

**Partition Tolerance** means the system continues to operate **even if network failures occur between nodes**.

A **partition** happens when communication between servers **breaks or becomes delayed**.

Example network partition:

```
Server A  ----X----  Server B
```

The servers **cannot communicate** with each other.

But the system **must continue working**.

### Important point

In modern distributed systems:

> **Partition tolerance is mandatory**

Because **network failures are unavoidable**.

Therefore in real distributed systems the actual choice is:

```
CP  or  AP
```

---

# Why Partition Tolerance is the Most Important

In distributed systems:

* Servers are located in **different data centers**
* Networks can fail
* Latency can occur
* Machines can crash

Because these failures **cannot be avoided**, systems **must tolerate partitions**.

Therefore most real-world systems sacrifice either:

* **Consistency**, or
* **Availability**

but **never Partition Tolerance**.

---

# CAP System Types

## 1. CP System (Consistency + Partition Tolerance)

### Meaning

The system guarantees:

* **Consistent data**
* **Handles network partitions**

But it may sacrifice **Availability**.

### What happens during partition

If nodes cannot communicate:

The system may **reject some requests** to maintain consistency.

### Example

Distributed database:

```
Server A (updated data)
Server B (old data)
```

If a user queries Server B during partition:

Instead of returning **old data**, the system may **deny the request**.

This ensures **Consistency**.

### Real-world examples

* HBase
* MongoDB (in some configurations)
* Zookeeper

### Use cases

Systems where **data correctness is critical**

Examples:

* Banking systems
* Financial transactions
* Inventory management

---

## 2. AP System (Availability + Partition Tolerance)

### Meaning

The system guarantees:

* **Availability**
* **Partition tolerance**

But **Consistency may be temporarily compromised**.

### What happens during partition

Both servers continue responding even if they cannot synchronize.

Example:

```
Server A → value = 10
Server B → value = 8
```

Users may receive **different values**.

Eventually the system resolves the difference using **eventual consistency**.

### Real-world examples

* Cassandra
* DynamoDB
* CouchDB

### Use cases

Systems where **availability is more important than immediate consistency**

Examples:

* Social media
* Product catalogs
* Recommendation systems
* Messaging systems

---

## 3. CA System (Consistency + Availability)

### Meaning

The system guarantees:

* **Consistency**
* **Availability**

But **cannot tolerate partitions**.

### Important note

CA systems are typically **monolithic systems**, not distributed systems.

If network partition occurs, the system **fails**.

### Example

Single database server:

```
Application
     |
Single Database
```

Since there is **no distribution**, partition does not occur.

So the system can maintain **both C and A**.

### Real-world examples

* Traditional relational databases
* Monolithic applications

Examples:

* MySQL (single node)
* PostgreSQL (single node)

---

# When to Choose C or A with P

In real distributed systems we must always have **Partition Tolerance**, so the decision becomes:

```
CP  or  AP
```

The choice depends on **application requirements**.

---

## Choose CP when Consistency is critical

Examples:

* Banking transactions
* Payment systems
* Airline seat booking
* Inventory systems

Reason:

```
Incorrect data is worse than temporary unavailability
```

Example:

Two users booking the **last seat** on a flight.

Consistency prevents **double booking**.

---

## Choose AP when Availability is critical

Examples:

* Social media feeds
* Online messaging
* Product reviews
* Analytics dashboards

Reason:

```
Temporary inconsistency is acceptable
```

Example:

Seeing **98 likes instead of 100 likes** is acceptable.

But the system **must respond quickly**.

---

# Quick Summary (Revision)

| Property            | Meaning                            |
| ------------------- | ---------------------------------- |
| Consistency         | Every read gets the latest data    |
| Availability        | Every request receives a response  |
| Partition Tolerance | System works even if network fails |

In distributed systems:

```
You cannot have C + A + P together
```

You must choose:

```
CP  → Consistency + Partition Tolerance
AP  → Availability + Partition Tolerance
```

Key idea:

```
Partition tolerance is mandatory in distributed systems
```

So the real decision is:

```
Consistency vs Availability
```

based on **application needs**.

---
