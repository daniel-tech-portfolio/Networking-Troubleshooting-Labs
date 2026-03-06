# Lab 3 – Gateway Misconfiguration

## Scenario

A user reports they can access other computers on the local network but cannot reach the internet or remote resources outside the local subnet.

Shared printers and nearby workstations respond, but websites and cloud services fail to load.

---

## Objective

Determine whether the default gateway is configured correctly and restore communication with external networks.

---

## Step 1 – Verify Local Network Connectivity

Command used:

```powershell
ping 192.168.20.25
```

Sample result:

```text
Reply from 192.168.20.25: bytes=32 time<1ms TTL=128
Reply from 192.168.20.25: bytes=32 time<1ms TTL=128
Reply from 192.168.20.25: bytes=32 time<1ms TTL=128
Reply from 192.168.20.25: bytes=32 time<1ms TTL=128
```

### Analysis

Successful replies confirm that communication within the local subnet is functioning correctly.

This suggests:

- The network adapter is working
- The switch connection is active
- The local subnet configuration is correct

---

## Step 2 – Test Connectivity to the Default Gateway

Command used:

```powershell
ping 192.168.20.254
```

Sample result:

```text
Request timed out.
Request timed out.
Request timed out.
Request timed out.
```

### Analysis

The workstation cannot communicate with the configured default gateway.

Without a reachable gateway, traffic cannot be routed outside the local subnet.

---

## Step 3 – Review Network Configuration

Command used:

```powershell
ipconfig
```

Sample result:

```text
Ethernet adapter Ethernet:

   IPv4 Address. . . . . . . . . . : 192.168.20.45
   Subnet Mask . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . : 192.168.20.254
```

### Analysis

The workstation is configured to use **192.168.20.254** as the gateway.

However, the expected gateway for this subnet should be **192.168.20.1**.

---

## Step 4 – Correct the Gateway Configuration

The network adapter configuration was updated to use the correct gateway.

Correct gateway:

```text
192.168.20.1
```

---

## Step 5 – Verify Gateway Connectivity

Command used:

```powershell
ping 192.168.20.1
```

Sample result:

```text
Reply from 192.168.20.1: bytes=32 time<1ms TTL=64
Reply from 192.168.20.1: bytes=32 time<1ms TTL=64
Reply from 192.168.20.1: bytes=32 time<1ms TTL=64
```

### Analysis

The workstation can now successfully communicate with the gateway.

---

## Step 6 – Verify Internet Connectivity

Command used:

```powershell
ping 8.8.8.8
```

Sample result:

```text
Reply from 8.8.8.8: bytes=32 time=16ms TTL=117
Reply from 8.8.8.8: bytes=32 time=18ms TTL=117
```

### Analysis

External connectivity has been restored.

---

## Step 7 – Trace the Route

Command used:

```powershell
tracert 8.8.8.8
```

Sample result:

```text
1    <1 ms    <1 ms    <1 ms  192.168.20.1
2    10 ms    11 ms    12 ms  10.10.0.1
3    18 ms    17 ms    19 ms  8.8.8.8
```

### Analysis

The route confirms that traffic is now passing through the correct gateway.

---

## Root Cause

The workstation was configured with an incorrect default gateway address.

Because of this misconfiguration, traffic intended for external networks could not be routed properly.

---

## Resolution

The gateway setting was corrected to the appropriate router interface for the subnet, restoring normal network connectivity.

---

## Skills Demonstrated

- Default gateway troubleshooting
- Subnet awareness
- Local vs external connectivity testing
- Route tracing
- Structured troubleshooting documentation
