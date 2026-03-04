

# 1️⃣ What is Consistency

## 📌 Definition

**Consistency** means that **all users see the same and most recent data at any given time**.

In simple words:

> After a data update, every user reading that data should get the **same updated value**.

---

## 🧠 Example

Suppose a user updates their profile name.

Old value:

```
Name = Ayush
```

After update:

```
Name = Ayush Sharma
```

If another user reads the data:

* If they see **Ayush Sharma** → system is **consistent**
* If they see **Ayush** → system is **inconsistent**

---

## 📊 Simple Flow

```
User A updates data
        ↓
Database updated
        ↓
User B reads same updated data
```

Both users see **same data → Consistency maintained**

---

## 📝 Quick Revision

Consistency ensures that **all reads return the latest written data**.

---

# 2️⃣ Dirty Read

## 📌 Definition

A **Dirty Read** occurs when a transaction reads **data that has been modified but not yet committed** by another transaction.

In simple terms:

> A system reads **temporary or unconfirmed data**.

---

## 🧠 Example

Suppose two transactions occur.

### Step 1

Transaction A updates balance:

```
Balance = 5000 → 3000
```

But the change is **not committed yet**.

---

### Step 2

Transaction B reads the balance:

```
Balance = 3000
```

---

### Step 3

Transaction A fails and rolls back:

```
Balance returns to 5000
```

Now Transaction B already read **incorrect data**.

This is called **Dirty Read**.

---

## 📊 Dirty Read Flow

```
Transaction A writes data
        ↓
Transaction B reads uncommitted data
        ↓
Transaction A rolls back
```

Result → **Inconsistent data**

---

## 📝 Quick Revision

Dirty Read = reading **uncommitted or temporary data**.

---

# 3️⃣ Consistency in Monolithic vs Distributed Systems

## 📌 Consistency in Monolithic Systems

In monolithic systems:

* Usually **one database**
* All modules access same data source

Structure:

```
Application
   ↓
Single Database
```

Because there is only **one data source**, consistency is easier to maintain.

Advantages:

* Immediate updates
* No synchronization issues

Result:

```
Higher consistency
```

---

## 📌 Consistency in Distributed Systems

In distributed systems:

* Data may be stored across **multiple servers**
* Replicated databases exist

Structure:

```
Server 1 → Database Replica
Server 2 → Database Replica
Server 3 → Database Replica
```

Problem:

Updates may take time to propagate.

Example:

```
Server 1 updated
Server 2 not updated yet
```

Users may see **different data temporarily**.

Result:

```
Consistency becomes harder
```

---

## 📊 Comparison

| Feature              | Monolithic   | Distributed       |
| -------------------- | ------------ | ----------------- |
| Database             | Single       | Multiple replicas |
| Data synchronization | Not required | Required          |
| Consistency          | Easier       | Harder            |

---

# 4️⃣ Factors Improving Consistency

Several techniques improve consistency in distributed systems.

---

# 1️⃣ Improve Network Bandwidth

Better network connectivity allows faster data synchronization between servers.

Example:

```
Server 1 update
↓
Server 2 update quickly
```

High bandwidth → faster replication → improved consistency.

---

# 2️⃣ Stop Read Operations Until Update Completes

System temporarily **blocks read operations** until the write operation finishes.

Example:

```
Write operation in progress
↓
Reads paused
↓
Update completed
↓
Reads allowed
```

This ensures users always read **latest data**.

---

# 3️⃣ Distance-Aware Replication Strategy

Replication strategies consider **geographical distance**.

Example:

```
Primary database → nearby replicas updated first
```

This ensures:

* Faster synchronization
* Better consistency for nearby users

Example:

```
India server → India replicas
US server → US replicas
```

---

# 5️⃣ Types of Consistency

Distributed systems support different **consistency models**.

---

# 1️⃣ Strong Consistency

## 📌 Definition

After a data update, **all subsequent reads return the latest value immediately**.

Users always see **latest data**.

---

## 🧠 Example

```
User A updates balance
↓
User B immediately reads updated balance
```

There is **no delay in data propagation**.

---

## 📊 Example Systems

Systems requiring strong consistency:

* Banking systems
* Payment systems
* Financial transactions

---

## ⚠️ Drawback

Strong consistency may increase:

* Latency
* System complexity

---

# 2️⃣ Eventual Consistency

## 📌 Definition

In **eventual consistency**, updates propagate gradually across servers.

All replicas will **eventually become consistent**, but not immediately.

---

## 🧠 Example

```
Server 1 updated
↓
Server 2 updated after few seconds
↓
Server 3 updated later
```

Eventually all servers have **same data**.

---

## 📊 Example Systems

Eventual consistency is common in:

* Social media feeds
* DNS systems
* Distributed databases

Example:

```
Instagram likes
```

Like count may take few seconds to update everywhere.

---

# 3️⃣ Weak Consistency

## 📌 Definition

Weak consistency provides **no guarantee that users will see the latest data immediately**.

Data updates may take **longer time** to appear.

---

## 🧠 Example

```
User updates profile picture
↓
Some users still see old image
```

Eventually it will update.

---

## 📊 Example Systems

Weak consistency is used in:

* Caching systems
* Real-time analytics dashboards
* Non-critical systems

---

# 📊 Comparison of Consistency Types

| Type                 | Guarantee            | Speed   | Use Case        |
| -------------------- | -------------------- | ------- | --------------- |
| Strong Consistency   | Always latest data   | Slower  | Banking         |
| Eventual Consistency | Eventually same data | Faster  | Social media    |
| Weak Consistency     | No strict guarantee  | Fastest | Caching systems |

---

# 📝 Final Quick Revision

**Consistency**

```
All users see same and latest data
```

---

**Dirty Read**

```
Reading uncommitted data
```

---

**Consistency in Systems**

| Monolithic      | Distributed       |
| --------------- | ----------------- |
| Easier          | Harder            |
| Single database | Multiple replicas |

---

**Improving Consistency**

* Improve network bandwidth
* Block reads until write completes
* Distance-aware replication

---

**Consistency Types**

Strong → immediate updates
Eventual → updates propagate over time
Weak → no strict guarantees

---

