# Lab 4 – Slow Network Diagnosis

## Scenario

A user reports that websites, cloud applications, and shared folders are loading very slowly.  
The computer still has network connectivity, but performance is inconsistent and significantly slower than normal.

---

## Objective

Use diagnostic networking tools to determine whether the issue is caused by latency, packet loss, or routing problems.

---

## Step 1 – Verify Local Network Connectivity

Command used:

```powershell
ping 192.168.30.1
```

Sample result:

```text
Reply from 192.168.30.1: bytes=32 time<1ms TTL=64
Reply from 192.168.30.1: bytes=32 time<1ms TTL=64
Reply from 192.168.30.1: bytes=32 time<1ms TTL=64
Reply from 192.168.30.1: bytes=32 time<1ms TTL=64
```

### Analysis

The workstation can communicate with the local gateway without delay.  
This indicates the local network connection and switch infrastructure are functioning normally.

---

## Step 2 – Test External Connectivity

Command used:

```powershell
ping 8.8.8.8
```

Sample result:

```text
Reply from 8.8.8.8: bytes=32 time=25ms TTL=117
Reply from 8.8.8.8: bytes=32 time=150ms TTL=117
Reply from 8.8.8.8: bytes=32 time=210ms TTL=117
Reply from 8.8.8.8: bytes=32 time=28ms TTL=117
```

### Analysis

Latency is inconsistent. Some responses are normal while others are significantly delayed.

This suggests possible network congestion or instability somewhere along the route.

---

## Step 3 – Check for Packet Loss

Command used:

```powershell
ping 8.8.8.8 -n 20
```

Sample result:

```text
Packets: Sent = 20, Received = 18, Lost = 2 (10% loss)
```

### Analysis

Packet loss is present. Even small amounts of packet loss can significantly affect application performance.

---

## Step 4 – Trace the Network Path

Command used:

```powershell
tracert 8.8.8.8
```

Sample result:

```text
Tracing route to 8.8.8.8 over a maximum of 30 hops

 1    <1 ms    <1 ms    <1 ms  192.168.30.1
 2    12 ms    10 ms    11 ms  10.10.0.1
 3   118 ms   140 ms   135 ms  203.0.113.5
 4   150 ms   160 ms   148 ms  198.51.100.1
```

### Analysis

Latency increases significantly beyond the local network, suggesting the slowdown may originate outside the LAN.

---

## Step 5 – Check Network Interface Statistics

Command used:

```powershell
netstat -e
```

Sample result:

```text
Interface Statistics

Bytes                   15829483
Unicast packets         22591
Non-unicast packets     188
Discards                0
Errors                  4
Unknown protocols       0
```

### Analysis

A small number of interface errors may indicate minor transmission issues but are not severe enough alone to cause the slowdown.

---

## Step 6 – Perform Extended Path Analysis

Command used:

```powershell
pathping 8.8.8.8
```

### Analysis

This command combines the functionality of ping and tracert to determine where packet loss occurs along the path.

It helps identify whether the issue originates:

- within the local network
- at the ISP
- further upstream on the internet

---

## Root Cause

The investigation indicates that latency and packet loss occur beyond the local gateway, suggesting congestion or instability on an upstream network segment.

---

## Resolution

The issue was documented and escalated to the network administration or ISP support team for further investigation.

---

## Skills Demonstrated

- Latency analysis
- Packet loss detection
- Route tracing
- Network statistics analysis
- Evidence-based escalation
- Structured troubleshooting documentation
