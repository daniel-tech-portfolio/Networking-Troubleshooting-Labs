
# Lab 2 – DNS Resolution Failure

## Scenario

A user reports that websites will not load when using domain names (for example, google.com), but some applications still appear to have internet connectivity. The workstation can reach external IP addresses but cannot resolve hostnames.

---

## Objective

Determine whether the issue is related to DNS configuration and restore proper name resolution.

---

## Step 1 – Verify Basic Network Connectivity

Command used:

```powershell
ping 8.8.8.8
```

Sample result:

```text
Reply from 8.8.8.8: bytes=32 time=17ms TTL=117
Reply from 8.8.8.8: bytes=32 time=18ms TTL=117
Reply from 8.8.8.8: bytes=32 time=16ms TTL=117
Reply from 8.8.8.8: bytes=32 time=19ms TTL=117
```

### Analysis

The workstation can successfully reach an external IP address.  
This confirms that the network connection and gateway are functioning correctly.

---

## Step 2 – Test Name Resolution

Command used:

```powershell
ping google.com
```

Sample result:

```text
Ping request could not find host google.com. Please check the name and try again.
```

### Analysis

The workstation cannot resolve the domain name to an IP address, indicating a DNS resolution issue.

---

## Step 3 – Check DNS Server Configuration

Command used:

```powershell
ipconfig /all
```

Sample result:

```text
Ethernet adapter Ethernet:

   IPv4 Address. . . . . . . . . . : 192.168.10.60
   Subnet Mask . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . : 192.168.10.1
   DNS Servers . . . . . . . . . . : 192.168.99.99
```

### Analysis

The configured DNS server appears incorrect or unreachable for the local network.

---

## Step 4 – Test DNS Using nslookup

Command used:

```powershell
nslookup google.com
```

Sample result:

```text
DNS request timed out.
timeout was 2 seconds.
Server:  UnKnown
Address: 192.168.99.99
```

### Analysis

The configured DNS server is not responding to requests.

---

## Step 5 – Update the DNS Server

The DNS configuration was updated to a valid DNS server.

Example corrected value:

```text
192.168.10.20
```

Alternatively, a public DNS server such as:

```text
8.8.8.8
```

may be used for testing.

---

## Step 6 – Flush the DNS Cache

Command used:

```powershell
ipconfig /flushdns
```

Sample result:

```text
Successfully flushed the DNS Resolver Cache.
```

### Analysis

Flushing the cache removes any previously stored incorrect DNS records.

---

## Step 7 – Verify DNS Resolution

Command used:

```powershell
nslookup google.com
```

Sample result:

```text
Server:  dns01.contoso.local
Address: 192.168.10.20

Non-authoritative answer:
Name: google.com
Address: 142.250.190.14
```

### Analysis

DNS resolution is now working correctly.

---

## Root Cause

The workstation was configured with an incorrect or unreachable DNS server.

---

## Resolution

Updated the DNS server configuration and cleared the DNS cache, restoring proper hostname resolution.

---

## Skills Demonstrated

- DNS troubleshooting
- IP vs hostname connectivity testing
- Use of `nslookup`
- DNS configuration verification
- Structured troubleshooting documentation
