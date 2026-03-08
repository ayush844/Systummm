# Lamport Logical Clock

## 1. Introduction

In **distributed systems**, multiple machines (nodes) run independently and communicate through messages. Since there is **no global clock shared by all machines**, it becomes difficult to determine the **order of events** across different nodes.

To solve this problem, **Leslie Lamport** introduced the concept of **Logical Clocks**, which help determine the **happened-before relationship** between events in a distributed system.

Lamport clocks do **not measure actual time**, but instead help **maintain the order of events**.

---

# 2. Problem Without Logical Clocks

Consider a distributed system with two servers:

```
Server A        Server B
```

Events occur on both machines independently.

Example:

```
A1 → A2 → A3
B1 → B2 → B3
```

If **A2 sends a message to B2**, we must ensure that:

```
A2 happened before B2
```

However, without synchronized clocks, we cannot determine the **correct ordering of events**.

This is where **Lamport Logical Clocks** help.

---

# 3. Happened-Before Relationship

Lamport introduced the **happened-before relation (→)** to describe event ordering.

### Rules

#### 1. Same Process Rule

If two events occur in the **same process**, their order defines the happened-before relationship.

Example:

```
A1 → A2 → A3
```

This means:

```
A1 happened before A2
A2 happened before A3
```

---

#### 2. Message Sending Rule

If an event **sends a message**, and another event **receives it**, then:

```
Send → Receive
```

Example:

```
A2 sends message → B1 receives message
```

Therefore:

```
A2 → B1
```

---

#### 3. Transitive Rule

If:

```
A → B
B → C
```

Then:

```
A → C
```

This is called **transitivity**.

---

# 4. Lamport Logical Clock Algorithm

Each process maintains its **own logical clock counter**.

```
Ci = logical clock of process i
```

### Rules

#### Rule 1: Increment before every event

Before executing any event:

```
Ci = Ci + 1
```

---

#### Rule 2: Sending a Message

When a process sends a message:

1. Increment its clock
2. Attach the clock value to the message

Example:

```
send(message, timestamp)
```

---

#### Rule 3: Receiving a Message

When a process receives a message with timestamp **T**:

```
Ci = max(Ci, T) + 1
```

This ensures the **correct event ordering**.

---

# 5. Example of Lamport Logical Clock

### System with Two Processes

```
Process P1          Process P2
```

Initial clocks:

```
P1 = 0
P2 = 0
```

---

### Step 1: Event on P1

```
P1 event A
Clock = 1
```

---

### Step 2: Another Event on P1

```
P1 event B
Clock = 2
```

---

### Step 3: P1 Sends Message to P2

Before sending:

```
Clock = 3
```

Message sent with timestamp **3**.

---

### Step 4: P2 Receives Message

Current P2 clock:

```
P2 = 0
```

Apply rule:

```
P2 = max(0,3) + 1
P2 = 4
```

Now the receive event gets timestamp **4**.

This ensures:

```
Send event (3) → Receive event (4)
```

Correct ordering is maintained.

---

# 6. Example with Multiple Events

Consider the following scenario:

```
P1:  A → B → C(send)
P2:        D(receive) → E
```

Step-by-step clock updates:

| Event       | Process | Clock          |
| ----------- | ------- | -------------- |
| A           | P1      | 1              |
| B           | P1      | 2              |
| C (send)    | P1      | 3              |
| D (receive) | P2      | max(0,3)+1 = 4 |
| E           | P2      | 5              |

Event ordering becomes:

```
A(1) → B(2) → C(3) → D(4) → E(5)
```

---

# 7. Key Property of Lamport Clocks

If:

```
Event A → Event B
```

Then:

```
Clock(A) < Clock(B)
```

However, the **reverse is not always true**.

Example:

```
Clock(A) < Clock(B)
```

does **not necessarily mean** that **A happened before B**.

Because events in different processes may be **independent**.

---

# 8. Advantages

### 1. Simple to implement

Lamport clocks use only **integer counters**.

### 2. Maintains event ordering

Helps determine **causal relationships** between events.

### 3. No need for synchronized clocks

Works even when machines have **different physical clocks**.

---

# 9. Limitations

### 1. Cannot detect concurrency

Two events may have:

```
Clock(A) < Clock(B)
```

but they might still be **independent events**.

Lamport clocks cannot detect **true concurrency**.

### 2. Does not capture full causality

To fully capture causality we need **Vector Clocks**.

---

# 10. Real-World Use Cases

Lamport logical clocks are used in:

* **Distributed databases**
* **Event ordering in distributed systems**
* **Mutual exclusion algorithms**
* **Distributed logging systems**
* **Replication systems**

Example systems:

* Apache Kafka
* Distributed transaction systems
* Distributed locking services

---

# 11. Quick Summary

| Concept         | Meaning                                               |
| --------------- | ----------------------------------------------------- |
| Logical Clock   | A counter used to order events in distributed systems |
| Happened-before | Defines causal relationship between events            |
| Send Rule       | Attach timestamp to message                           |
| Receive Rule    | `Ci = max(Ci, T) + 1`                                 |
| Key Idea        | Maintain event ordering without global clocks         |

Important property:

```
If A → B then Clock(A) < Clock(B)
```

Lamport clocks help **maintain causal ordering of events in distributed systems**.

