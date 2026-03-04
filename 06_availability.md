
# 1️⃣ What is Availability

## 📌 Definition

**Availability** refers to the **percentage of time a system is operational and accessible to users**.

In simple terms:

> Availability measures **how often a system is up and running without failure**.

It is usually expressed as a **percentage of uptime**.

---

## 📊 Example

If a system is operational for **99 out of 100 hours**, then:

```
Availability = 99%
```

Example uptime levels used in real systems:

| Availability | Downtime per Year |
| ------------ | ----------------- |
| 99%          | ~3.65 days        |
| 99.9%        | ~8.7 hours        |
| 99.99%       | ~52 minutes       |
| 99.999%      | ~5 minutes        |

This is often called **“five nines availability”**.

---

## 🧠 Example

When you open:

* Gmail
* Instagram
* Netflix

They are almost always available.

This means they have **very high availability**.

---

## 📝 Quick Revision

**Availability = percentage of time a system is operational**

---

# 2️⃣ Availability in Monolithic vs Distributed Architecture

## 📌 Availability in Monolithic Architecture

In monolithic systems:

* Entire application runs on **one system or a few servers**
* All modules are tightly connected

Structure:

```
Client
 ↓
Single Application
 ├ Auth
 ├ Orders
 ├ Payments
 └ Database
```

### Problem

If the server crashes:

```
Server failure
↓
Entire application goes down
```

This creates a **single point of failure**.

So availability is **lower** compared to distributed systems.

---

## 📌 Availability in Distributed Architecture

In distributed systems:

* System runs across **multiple servers**
* Services are independent

Structure:

```
Client
 ↓
Load Balancer
 ↓
Multiple Services
 ├ Service 1
 ├ Service 2
 ├ Service 3
```

If one service fails:

```
Service 2 fails
↓
Other services continue working
```

System remains available.

Therefore **distributed systems have higher availability**.

---

## 📊 Comparison

| Feature         | Monolithic             | Distributed              |
| --------------- | ---------------------- | ------------------------ |
| Failure impact  | Entire system may fail | Only one component fails |
| Fault tolerance | Low                    | High                     |
| Availability    | Lower                  | Higher                   |

---

# 3️⃣ Fault Tolerance and Availability

## 📌 Definition of Fault Tolerance

**Fault tolerance** is the ability of a system to **continue functioning even when some components fail**.

---

## 🧠 Relationship

Fault tolerance and availability are closely related.

```
Fault Tolerance ↑
Availability ↑
```

This means:

> **Fault tolerance is directly proportional to availability.**

If a system can tolerate failures, it remains operational.

---

## 📊 Example

Suppose a system has **three servers**:

```
Server 1
Server 2
Server 3
```

If **Server 1 fails**, the others handle requests.

Users may not even notice the failure.

This increases **availability**.

---

## 📝 Quick Revision

Fault tolerance allows a system to **continue working despite failures**, which improves **availability**.

---

# 4️⃣ How to Increase Availability

Several techniques improve system availability.

---

# 1️⃣ Replication

Replication means **creating multiple copies of services or data**.

Example:

```
Database 1
Database 2
Database 3
```

If one database fails:

```
Requests → other database
```

System remains operational.

---

# 2️⃣ Distributed Systems

Distributed systems spread services across **multiple machines**.

Example:

```
Auth Service
Payment Service
Notification Service
```

If one fails, others still work.

This improves availability.

---

# 3️⃣ Redundancy

Redundancy means **having backup components ready in case of failure**.

Example:

```
Primary Server
Backup Server
```

If the primary fails:

```
Backup takes over
```

Redundancy ensures system continuity.

---

# 4️⃣ Load Balancing

Load balancers distribute traffic across multiple servers.

Example:

```
Client
 ↓
Load Balancer
 ↓
Server 1
Server 2
Server 3
```

If one server fails, traffic goes to others.

---

# 5️⃣ Auto Scaling

Automatically add more servers during high load.

Example:

```
High traffic → system launches new servers
```

This prevents crashes.

---

# 5️⃣ Replication vs Redundancy

Although they sound similar, they are slightly different.

---

## 📌 Replication

Replication means **creating copies of data or services that operate simultaneously**.

Example:

```
Database replicas
Service replicas
```

All replicas actively serve requests.

Purpose:

* Increase availability
* Improve scalability
* Improve performance

Example:

```
3 database replicas handling queries
```

---

## 📌 Redundancy

Redundancy means **keeping backup components ready for failure situations**.

Example:

```
Primary server
Backup server
```

Backup remains idle until needed.

Purpose:

* Ensure reliability
* Provide backup during failure

---

## 📊 Key Differences

| Feature   | Replication                | Redundancy         |
| --------- | -------------------------- | ------------------ |
| Purpose   | Handle load + reliability  | Backup for failure |
| Operation | Active copies              | Often standby      |
| Usage     | Distributed systems        | Disaster recovery  |
| Example   | Multiple database replicas | Backup server      |

---

## 🧠 Easy Way to Remember

Replication → **Multiple active copies**

Redundancy → **Backup system**

---

# 📝 Final Quick Revision

**Availability**

```
Availability = percentage of system uptime
```

Example:

```
99.99% uptime
```

---

**Monolithic vs Distributed Availability**

| Monolithic              | Distributed         |
| ----------------------- | ------------------- |
| Single point of failure | Multiple nodes      |
| Lower availability      | Higher availability |

---

**Fault Tolerance**

```
Fault tolerance ↑
Availability ↑
```

---

**Increase Availability**

* Replication
* Redundancy
* Distributed systems
* Load balancing
* Auto scaling

---

**Replication vs Redundancy**

Replication → multiple active copies
Redundancy → backup components

---

