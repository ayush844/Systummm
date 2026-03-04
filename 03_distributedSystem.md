
# Distributed System – Notes

## 1. Distributed System

A **Distributed System** is a system where multiple independent computers work together and communicate over a network to achieve a common goal.

Each computer (node) performs part of the work and together they behave like a single system to the user.

**Examples**

* Google Search
* Netflix
* Amazon
* Cloud services

**Key Characteristics**

* Multiple machines
* Communication over network
* Workload divided among nodes
* Scalable and fault tolerant

---

# 2. Difference Between Monolithic and Distributed System

| Feature         | Monolithic System               | Distributed System                                |
| --------------- | ------------------------------- | ------------------------------------------------- |
| Architecture    | Single large application        | Multiple services on multiple machines            |
| Deployment      | Deployed as one unit            | Services deployed independently                   |
| Scalability     | Difficult to scale              | Easy to scale horizontally                        |
| Fault tolerance | Single failure can crash system | Failure of one service doesn't stop entire system |
| Communication   | Internal function calls         | Network communication (API, RPC)                  |
| Complexity      | Simpler                         | More complex                                      |
| Maintenance     | Hard to modify large codebase   | Easier to update individual services              |

**Example**

Monolithic:

```
Frontend + Backend + Database in one server
```

Distributed:

```
User Service
Payment Service
Order Service
Inventory Service
All running on different servers
```

---

# 3. Module Replication in Distributed Systems

**Module Replication** means creating **multiple copies of the same service or module** across different servers.

This helps in handling more users and improves reliability.

### Example

Instead of one authentication server:

```
Auth Server 1
Auth Server 2
Auth Server 3
```

A **load balancer** distributes requests between them.

### Types of Replication

1. **Active Replication**

* All replicas process requests simultaneously.

2. **Passive Replication**

* One primary server processes requests.
* Backup servers take over if primary fails.

---

# 4. Advantages of Distributed Architecture

### 1. Scalability

More servers can be added to handle increased load.

### 2. Fault Tolerance

If one server fails, other servers continue working.

### 3. High Performance

Workload is distributed across multiple machines.

### 4. Flexibility

Different services can use different technologies.

### 5. Availability

System remains operational even during failures.

---

# 5. Disadvantages of Distributed Architecture

### 1. High Complexity

System design and debugging are harder.

### 2. Network Dependency

Services rely on network communication.

### 3. Latency Issues

Communication between services takes time.

### 4. Data Consistency Challenges

Maintaining consistent data across services is difficult.

### 5. Deployment Complexity

Multiple services need coordination.

---

# 6. Latency Comparison (Monolithic vs Distributed)

**Latency** is the time taken for a request to travel from client to server and receive a response.

```
Latency = Network Delay + Processing Time
```

---

### Latency in Monolithic System

* Components are in the **same server**.
* Communication happens via **function calls**.
* No network communication between modules.

**Result:**
Low latency

Example flow:

```
User Request
     ↓
Single Server
     ↓
Database
```

---

### Latency in Distributed System

* Services are on **different machines**.
* Communication happens through **network calls (HTTP, RPC)**.

Example flow:

```
User → API Gateway
        ↓
   Auth Service
        ↓
   Order Service
        ↓
   Payment Service
        ↓
   Database
```

Each service call adds **network delay**.

**Result:**
Higher latency compared to monolithic systems.

---

### Summary

| System      | Latency                                     |
| ----------- | ------------------------------------------- |
| Monolithic  | Low latency                                 |
| Distributed | Higher latency due to network communication |

---
