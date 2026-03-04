

# 1️⃣ What is Latency

## 📌 Definition

**Latency** is the **time taken for a request to travel from the client to the server and back with a response**.

In simple terms:

> Latency = How long a system takes to respond to a request.

It is usually measured in **milliseconds (ms)**.

---

## 🧠 Example

When you open a website:

1. Browser sends request
2. Server processes request
3. Server sends response
4. Page loads

The total time taken = **Latency**

Example:

```
User clicks button
↓
Request goes to server
↓
Server processes data
↓
Response comes back
↓
Page updates
```

If this takes **100 ms**, then latency = **100 ms**.

---

# 2️⃣ Latency Formula

## 📌 Basic Formula

Latency can be expressed as:

```
Latency = Network Delay + Computational Delay
```

---

## 1️⃣ Network Delay

Time taken for data to travel through the **network**.

Includes:

* Internet transmission time
* Routing through multiple servers
* Network congestion

Example:

```
India → US server request
```

This increases network delay.

---

## 2️⃣ Computational Delay

Time taken by the **server to process the request**.

Includes:

* Database queries
* Business logic execution
* API processing
* File processing

Example:

```
Server fetching data from database
```

This adds computational delay.

---

## 🧠 Example Calculation

```
Network delay = 70 ms
Processing time = 30 ms

Total Latency = 100 ms
```

---

## 📝 Quick Revision

Latency = **time taken to receive response from a system**

Formula:

```
Latency = Network delay + Computational delay
```

---

# 3️⃣ Latency in Monolithic vs Distributed Systems

## 📌 Monolithic System Latency

In monolithic systems, modules communicate using **internal function calls**.

Example:

```
Order Service → Payment Service
```

This happens **inside the same application**.

Advantages:

* No network calls
* Faster execution

Typical latency:

```
1–5 ms
```

---

## 📌 Distributed System Latency

In distributed systems, services communicate using **network APIs**.

Example:

```
Order Service
   ↓ HTTP request
Payment Service
```

This requires:

* Network communication
* Request serialization
* Response transfer

Typical latency:

```
20–100 ms or more
```

---

## 📊 Comparison

| Feature       | Monolithic System | Distributed System   |
| ------------- | ----------------- | -------------------- |
| Communication | Function calls    | Network calls        |
| Network delay | None              | Present              |
| Latency       | Low               | Higher               |
| Performance   | Faster internally | Slower communication |

---

## ⚠️ Important Trade-off

Distributed systems have **higher latency**, but they provide:

* Better scalability
* Better fault tolerance
* Better flexibility

---

# 4️⃣ Ways to Reduce Latency

Reducing latency is **one of the main goals of system design**.

### 1️⃣ Caching

Store frequently requested data in **fast storage (cache)** instead of querying database repeatedly.

Example:

```
Database query = 50 ms
Redis cache = 2 ms
```

So caching greatly reduces latency.

Example tools:

* Redis
* Memcached

---

### 2️⃣ Using CDN (Content Delivery Network)

A **CDN stores copies of static content closer to users**.

Example:

```
Images
Videos
CSS files
JavaScript
```

Instead of loading from the main server, they are served from **nearby CDN servers**.

Example CDNs:

* Cloudflare
* AWS CloudFront
* Akamai

---

### 3️⃣ Upgrading System Hardware

Improving infrastructure reduces computational delay.

Examples:

* Faster CPU
* More RAM
* SSD storage
* Faster network bandwidth

---

### 4️⃣ Database Optimization

Improve query performance using:

* Indexing
* Query optimization
* Better schema design

---

### 5️⃣ Load Balancing

Distribute traffic across multiple servers to prevent overload.

---

# 5️⃣ Difference Between Caching and CDN

Although both improve performance, they are **not the same**.

---

## 📌 Caching

Caching stores **frequently accessed data temporarily** in a **fast storage layer**.

Purpose:

Reduce repeated database queries.

Example flow:

```
User Request
↓
Cache (Redis)
↓
If not found → Database
```

Common cached data:

* User sessions
* API responses
* Query results
* Feed data

---

## 📌 CDN (Content Delivery Network)

A **CDN is a network of globally distributed servers** that deliver **static content from the nearest location to the user**.

Example:

```
User in India
↓
Gets image from India CDN server
```

Instead of fetching from:

```
US main server
```

---

## 📊 Key Differences

| Feature      | Caching                              | CDN                              |
| ------------ | ------------------------------------ | -------------------------------- |
| Purpose      | Store frequently used data           | Deliver content closer to users  |
| Location     | Inside backend infrastructure        | Global distributed servers       |
| Type of Data | Dynamic data (API results, sessions) | Static content (images, CSS, JS) |
| Technology   | Redis, Memcached                     | Cloudflare, CloudFront           |
| Use Case     | Reduce database load                 | Reduce network latency           |

---

## 🧠 Simple Way to Remember

Caching → **Store data faster**

CDN → **Deliver data closer**

---

# 📝 Quick Revision

**Latency**

```
Latency = Network delay + Computational delay
```

**Monolithic vs Distributed**

| Monolithic     | Distributed    |
| -------------- | -------------- |
| Internal calls | Network calls  |
| Lower latency  | Higher latency |

**Reducing Latency**

* Caching
* CDN
* Hardware upgrades
* Query optimization
* Load balancing

**Caching vs CDN**

Caching → speeds up backend
CDN → speeds up content delivery globally

---

