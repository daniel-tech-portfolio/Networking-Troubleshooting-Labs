# Lab 1 – No Network Connectivity

## Scenario

A user reports that their workstation cannot access the internet or internal company resources. Web pages fail to load, and internal shared drives are unreachable.

---

## Objective

Identify the cause of the connectivity problem and restore normal network access.

---

## Step 1 – Check IP Configuration

Command used:

```powershell
ipconfig
```

Sample result:

```text
Ethernet adapter Ethernet:

   Connection-specific DNS Suffix  . :
   IPv4 Address. . . . . . . . . . : 169.254.84.22
   Subnet Mask . . . . . . . . . . : 255.255.0.0
   Default Gateway . . . . . . . . :
```

### Analysis

The workstation has an **APIPA address (169.254.x.x)**.  
This indicates the computer did not receive a valid IP address from a DHCP server.

Common causes include:

- DHCP server unreachable
- Network cable unplugged
- Switch port issue
- VLAN misconfiguration

---

## Step 2 – Check Full Network Adapter Details

Command used:

```powershell
ipconfig /all
```

This command displays detailed network configuration including:

- DHCP server
- DNS servers
- MAC address
- lease information

### Analysis

The adapter is active but has no valid DHCP lease, confirming the workstation could not obtain an IP address from DHCP.

---

## Step 3 – Attempt to Renew the DHCP Lease

Commands used:

```powershell
ipconfig /release
ipconfig /renew
```

Sample result:

```text
Ethernet adapter Ethernet:

   IPv4 Address. . . . . . . . . . : 192.168.10.54
   Subnet Mask . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . : 192.168.10.1
```

### Analysis

The workstation successfully obtained a valid DHCP lease and was assigned a proper IP address.

---

## Step 4 – Test Connectivity to the Default Gateway

Command used:

```powershell
ping 192.168.10.1
```

Sample result:

```text
Reply from 192.168.10.1: bytes=32 time<1ms TTL=64
Reply from 192.168.10.1: bytes=32 time<1ms TTL=64
Reply from 192.168.10.1: bytes=32 time<1ms TTL=64
Reply from 192.168.10.1: bytes=32 time<1ms TTL=64
```

### Analysis

Successful replies confirm that the workstation can communicate with the local router or gateway.

---

## Step 5 – Test Internet Connectivity

Command used:

```powershell
ping 8.8.8.8
```

Sample result:

```text
Reply from 8.8.8.8: bytes=32 time=18ms TTL=117
Reply from 8.8.8.8: bytes=32 time=19ms TTL=117
```

### Analysis

Successful responses confirm the workstation can reach external networks.

---

## Step 6 – Test DNS Name Resolution

Command used:

```powershell
ping google.com
```

Sample result:

```text
Pinging google.com [142.250.190.14] with 32 bytes of data:
Reply from 142.250.190.14: bytes=32 time=20ms TTL=117
```

### Analysis

Successful name resolution confirms DNS services are working correctly.

---

## Root Cause

The workstation failed to obtain a DHCP lease and automatically assigned itself an **APIPA address (169.254.x.x)**.

---

## Resolution

Releasing and renewing the IP configuration allowed the workstation to obtain a valid IP address from the DHCP server, restoring network connectivity.

---

## Skills Demonstrated

- TCP/IP troubleshooting
- DHCP diagnostics
- Connectivity testing
- Structured troubleshooting workflow
- Technical documentation
