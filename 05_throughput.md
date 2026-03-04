

# 1️⃣ What is Throughput

## 📌 Definition

**Throughput** is the **amount of work a system can process in a given period of time**.

In system design, it usually means:

> The number of **requests a system can handle per second**.

It is often measured as:

* **Requests per second (RPS)**
* **Transactions per second (TPS)**
* **Data processed per second**

---

## 🧠 Example

Suppose a server handles:

```text
1000 requests per second
```

Then the system throughput is:

```text
Throughput = 1000 RPS
```

Another example:

If a payment system processes:

```text
500 transactions per second
```

Then:

```text
Throughput = 500 TPS
```

---

## 🧠 Simple Way to Understand

| Concept    | Meaning                             |
| ---------- | ----------------------------------- |
| Latency    | Time taken for one request          |
| Throughput | Number of requests handled per time |

Example:

```text
Latency = 100 ms
Throughput = 1000 requests/sec
```

---

## 📝 Quick Revision

**Throughput = number of requests processed per unit time**

---

# 2️⃣ Throughput in Monolithic vs Distributed Systems

## 📌 Throughput in Monolithic Systems

In a monolithic architecture:

* All modules run inside **one application**
* Usually hosted on **one server or limited servers**

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

### Characteristics

* Limited processing capacity
* Throughput depends on **single system resources**

Example:

```
Server capacity = 2000 requests/sec
```

Maximum throughput:

```
2000 RPS
```

To increase throughput you must:

* Upgrade CPU
* Add RAM
* Scale vertically

---

## 📌 Throughput in Distributed Systems

In distributed systems:

* Work is **spread across multiple servers**
* Services run independently

Structure:

```
Client
 ↓
Load Balancer
 ↓
Multiple Servers
 ├ Server 1
 ├ Server 2
 ├ Server 3
```

### Characteristics

* Multiple machines process requests simultaneously
* Throughput increases with number of servers

Example:

```
Server 1 = 2000 RPS
Server 2 = 2000 RPS
Server 3 = 2000 RPS
```

Total throughput:

```
6000 RPS
```

---

## 📊 Comparison

| Feature      | Monolithic       | Distributed        |
| ------------ | ---------------- | ------------------ |
| Architecture | Single system    | Multiple servers   |
| Scaling      | Vertical scaling | Horizontal scaling |
| Throughput   | Limited          | Much higher        |
| Flexibility  | Low              | High               |

---

## 🧠 Key Insight

Distributed systems achieve **higher throughput by parallel processing**.

---

# 3️⃣ Causes of Low Throughput

Throughput can drop due to several factors.

---

## 1️⃣ High Latency

If each request takes longer to process, fewer requests can be processed overall.

Example:

```
Latency = 500 ms
```

Server can process fewer requests per second.

Higher latency → **lower throughput**

---

## 2️⃣ Protocol Overhead

Communication protocols introduce extra processing.

Examples:

* HTTP headers
* Encryption overhead
* Serialization/deserialization

Example:

```
Client → HTTP → Server
```

Extra protocol work slows down request handling.

---

## 3️⃣ Network Congestion

When too many requests travel through the network:

* Packet delays occur
* Data transfer slows

Example:

```
Heavy traffic on server
```

This reduces throughput.

---

## 4️⃣ Limited System Resources

Throughput also depends on:

* CPU
* RAM
* Disk speed
* Network bandwidth

If resources are limited, the system cannot process more requests.

---

# 4️⃣ Improving Throughput

There are several ways to increase throughput.

---

# 1️⃣ Use CDN (Content Delivery Network)

A **CDN stores static content closer to users**.

Examples of static content:

* Images
* CSS
* JavaScript
* Videos

Instead of hitting the main server, requests go to **nearby CDN servers**.

Benefits:

* Reduces load on main server
* Increases system throughput

Example CDNs:

* Cloudflare
* AWS CloudFront
* Akamai

---

# 2️⃣ Use Caching

Caching stores frequently requested data in **fast memory storage**.

Example:

```
Without cache
User → Server → Database
```

With cache:

```
User → Cache → Server
```

Benefits:

* Faster responses
* Reduced database load
* Higher throughput

Common caching tools:

* Redis
* Memcached

---

# 3️⃣ Load Balancing with Distributed Systems

Load balancers distribute incoming requests across multiple servers.

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

Benefits:

* Requests processed in parallel
* System handles more traffic
* Improves throughput

---

# 4️⃣ Upgrade System Infrastructure

Improving hardware improves system performance.

Examples:

* Faster CPU
* More RAM
* SSD storage
* Higher network bandwidth

This increases computational capacity and throughput.

---

# 📊 Summary

## Throughput

```
Throughput = number of requests processed per unit time
```

Example:

```
1000 requests/sec
```

---

## Throughput Comparison

| System      | Throughput |
| ----------- | ---------- |
| Monolithic  | Limited    |
| Distributed | High       |

---

## Causes of Low Throughput

* High latency
* Protocol overhead
* Network congestion
* Limited resources

---

## Improving Throughput

* Use CDN
* Use caching
* Use load balancing
* Upgrade hardware
* Use distributed architecture

---

