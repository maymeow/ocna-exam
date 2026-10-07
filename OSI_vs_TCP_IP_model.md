# OSI vs TCP/IP Model

There are two major reference models used to describe computer networking:

- **OSI model** — developed by ISO
- **TCP/IP model** — developed from the U.S. Department of Defense (DoD) networking architecture and used as the foundation of the modern Internet

---

## 1. Layer Comparison

### Traditional 4-layer TCP/IP model

| OSI | OSI Layer | TCP/IP | TCP/IP Layer |
|---:|---|---:|---|
| 7 | Application | 4 | Application |
| 6 | Presentation | 4 | Application |
| 5 | Session | 4 | Application |
| 4 | Transport | 3 | Transport |
| 3 | Network | 2 | Internet |
| 2 | Data Link | 1 | Network Access |
| 1 | Physical | 1 | Network Access |

The TCP/IP model combines several OSI layers:

```text
OSI                         TCP/IP

7  Application  ───────┐
6  Presentation  ──────┼──► Application
5  Session ────────────┘

4  Transport ─────────────► Transport

3  Network ───────────────► Internet

2  Data Link ──────────┐
1  Physical ───────────┴──► Network Access
```

---

## 2. The 5-layer version

In networking education, you will also often see a **5-layer TCP/IP / Internet model**:

| Layer | Name | Rough OSI equivalent |
|---:|---|---|
| 5 | Application | OSI 5–7 |
| 4 | Transport | OSI 4 |
| 3 | Network | OSI 3 |
| 2 | Data Link | OSI 2 |
| 1 | Physical | OSI 1 |

This version is particularly convenient because it keeps **Physical** and **Data Link** separate, just like OSI.

---

# 3. Main Philosophical Difference

### OSI

OSI is primarily a **reference model** designed to describe networking in a clean, modular and vendor-independent way.

It deliberately separates functions:

```text
Application
Presentation
Session
Transport
Network
Data Link
Physical
```

Each layer has a clearly defined conceptual role.

### TCP/IP

TCP/IP is much more **protocol-oriented**.

It was developed around real networking protocols such as:

```text
HTTP
DNS
TCP
UDP
IP
Ethernet
Wi-Fi
```

Rather than asking:

> "What should a theoretically perfect networking architecture look like?"

TCP/IP is closer to:

> "What protocols and mechanisms do we actually need to build an interoperable network?"

---

# 4. Advantages of the OSI Model

### Clear separation of responsibilities

Each layer has a relatively well-defined purpose.

For example:

```text
L1 → signals
L2 → frames / MAC
L3 → packets / IP
L4 → segments/datagrams / ports
L5 → sessions
L6 → representation
L7 → applications
```

This makes it useful for **learning and troubleshooting**.

### Vendor independent

OSI is not tied to a particular protocol suite or vendor.

It provides a common vocabulary for discussing networking.

### Excellent for troubleshooting

A common troubleshooting approach is:

```text
L1 → Is the link physically working?
L2 → Is the local network working?
L3 → Is IP connectivity/routing working?
L4 → Are ports/TCP/UDP working?
L7 → Is the application working?
```

For example:

> "It's a Layer 2 problem."

immediately narrows down the possible causes.

### Good conceptual separation

OSI makes it easy to understand why a:

- switch is primarily L2
- router is primarily L3
- TCP operates at L4
- HTTP operates at L7

---

# 5. Disadvantages of the OSI Model

### It is more theoretical than practical

The biggest criticism is that the OSI model was designed as a **general reference architecture**, while the Internet evolved around TCP/IP.

The Internet did not simply implement OSI layer by layer.

### Layers 5 and 6 are rarely visible as separate layers

In real-world TCP/IP networking, the functions described by:

```text
L5 – Session
L6 – Presentation
```

are frequently handled by applications, libraries or protocols rather than by distinct networking layers.

For example, encryption and data representation may be handled by:

```text
TLS
JSON
HTTP
application libraries
```

rather than by a dedicated "Presentation Layer" protocol.

### Some protocols do not fit neatly into one layer

Real protocols often cross conceptual layer boundaries.

For example, **ARP** is commonly associated with L2/L3, but does not fit perfectly into the OSI model.

Similarly, modern protocols such as QUIC blur some traditional boundaries.

### More layers can mean more complexity

Seven layers are excellent for teaching concepts, but can sometimes make real-world networking appear more rigid than it actually is.

---

# 6. Advantages of the TCP/IP Model

### It reflects the real Internet

TCP/IP is based on the protocols that actually power modern networks:

```text
Application
    ↓
TCP / UDP / QUIC
    ↓
IP
    ↓
Ethernet / Wi-Fi
    ↓
Physical medium
```

This makes it highly relevant to practical networking.

### Simpler

The traditional model has only four layers:

```text
Application
Transport
Internet
Network Access
```

It avoids treating Session and Presentation as independent networking layers.

### Protocol-oriented

The model naturally maps to real protocols:

| TCP/IP Layer | Examples |
|---|---|
| Application | HTTP, DNS, SSH, SMTP |
| Transport | TCP, UDP, QUIC |
| Internet | IPv4, IPv6, ICMP |
| Network Access | Ethernet, Wi-Fi |

### Proven in practice

TCP/IP has been deployed at enormous scale and forms the foundation of the Internet.

Its architecture supports interoperability between completely different vendors, operating systems and network technologies.

---

# 7. Disadvantages of the TCP/IP Model

### Less precise separation of functions

The Application layer combines what OSI separates into:

```text
Application
Presentation
Session
```

This is simpler, but conceptually less precise.

For example:

```text
OSI:
Application
Presentation
Session

TCP/IP:
Application
```

You lose some visibility into **which function is actually being performed**.

### Network Access layer is too broad

The traditional TCP/IP model combines:

```text
Data Link
Physical
```

into one Network Access layer.

That can be inconvenient when troubleshooting.

For example:

```text
Cable problem
    ↓
Physical

VLAN problem
    ↓
Data Link
```

Both would technically fall under TCP/IP's Network Access layer.

This is one reason many networking courses use the **5-layer Internet model** instead.

### Less useful as a teaching model

For learning networking concepts, the four-layer model can hide important distinctions.

For example, OSI makes this very obvious:

```text
L1 → physical transmission
L2 → local delivery / MAC
L3 → routing / IP
L4 → end-to-end transport / ports
```

The traditional TCP/IP model compresses some of these concepts.

### Not every modern protocol maps perfectly

Modern protocols and technologies do not always fit neatly into the original TCP/IP layer boundaries.

Examples include:

- QUIC
- TLS
- VPN technologies
- tunneling
- overlays
- SDN
- container networking

Modern networking is often better understood as **a stack of protocols and encapsulations**, rather than a perfectly strict hierarchy.

---

# 8. Which Model Is Better?

Neither is universally "better."

They serve different purposes.

| Situation | Better model |
|---|---|
| Learning networking concepts | **OSI** |
| Troubleshooting | **OSI** |
| Explaining network layers | **OSI** |
| Understanding the Internet | **TCP/IP** |
| Understanding real protocols | **TCP/IP** |
| Protocol implementation | **TCP/IP** |
| Vendor-neutral terminology | **OSI** |
| Practical network engineering | **Both** |

A good network engineer should understand **both**.

---

# 9. Practical Example

Suppose you open:

```text
https://example.com
```

A simplified view using OSI is:

```text
L7  HTTP
    ↓
L6  TLS / data representation
    ↓
L5  session-related mechanisms
    ↓
L4  TCP / QUIC + port
    ↓
L3  IP + routing
    ↓
L2  Ethernet / Wi-Fi + MAC
    ↓
L1  electrical / optical / radio signal
```

The TCP/IP view is simpler:

```text
Application
    HTTP / TLS
       ↓
Transport
    TCP / QUIC
       ↓
Internet
    IP
       ↓
Network Access
    Ethernet / Wi-Fi / Physical medium
```

The **same communication is happening**. The models simply divide the functionality differently.

---

# 10. The Most Important Thing to Remember

Don't think of OSI and TCP/IP as two completely different networking systems.

They are **different ways of describing the same general networking architecture**.

### OSI

> **More detailed, conceptual and educational**

```text
7 Application
6 Presentation
5 Session
4 Transport
3 Network
2 Data Link
1 Physical
```

### TCP/IP

> **Simpler and closer to the protocols used by the Internet**

```text
4 Application
3 Transport
2 Internet
1 Network Access
```

### Exam shortcut

```text
OSI:
L7 → Application
L6 → Presentation
L5 → Session
L4 → Transport
L3 → Network
L2 → Data Link
L1 → Physical

TCP/IP:
Application  → OSI 5–7
Transport    → OSI 4
Internet     → OSI 3
Network Access → OSI 1–2
```

**In one sentence:**

> **OSI is mainly a conceptual reference model; TCP/IP is a practical protocol architecture that reflects how the Internet actually works.**
