# Networking Troubleshooting Commands Cheat Sheet

This reference sheet contains common command-line tools used by IT support technicians and network administrators to diagnose network connectivity problems.

These commands are frequently used when troubleshooting issues such as:

- No internet connectivity
- DNS resolution failures
- Gateway routing problems
- Slow network performance
- Packet loss or latency issues

---

# ipconfig

Displays IP configuration information for all network adapters.

### Common Usage

```powershell
ipconfig
ipconfig /all
ipconfig /release
ipconfig /renew
ipconfig /flushdns
```

### What it Shows

- IP address
- Subnet mask
- Default gateway
- DNS servers
- DHCP server
- MAC address

### Common Troubleshooting Uses

- Verify correct IP address assignment
- Identify APIPA addresses (169.254.x.x)
- Confirm DNS configuration
- Renew DHCP leases
- Clear cached DNS records

---

# ping

Tests network connectivity between devices.

### Common Usage

```powershell
ping 192.168.1.1
ping 8.8.8.8
ping google.com
ping 8.8.8.8 -n 20
```

### What it Shows

- Network reachability
- Round-trip latency
- Packet loss

### Common Troubleshooting Uses

- Verify connectivity to gateway
- Test internet access
- Compare hostname vs IP connectivity
- Detect packet loss

---

# tracert

Displays the route packets take to reach a destination.

### Common Usage

```powershell
tracert 8.8.8.8
tracert google.com
```

### What it Shows

- Each router hop along the path
- Latency between hops
- Where traffic stops or slows down

### Common Troubleshooting Uses

- Identify routing problems
- Locate slow network segments
- Diagnose upstream ISP issues

---

# nslookup

Queries DNS servers for hostname resolution.

### Common Usage

```powershell
nslookup google.com
nslookup server01.company.local
```

### What it Shows

- DNS server used
- Resolved IP address
- DNS query responses

### Common Troubleshooting Uses

- Diagnose DNS failures
- Verify DNS server responses
- Compare DNS resolution between servers

---

# netstat

Displays network statistics and active connections.

### Common Usage

```powershell
netstat
netstat -an
netstat -e
```

### What it Shows

- Active network connections
- Listening ports
- Network interface statistics

### Common Troubleshooting Uses

- Identify suspicious connections
- Monitor network traffic
- Review interface errors

---

# arp

Displays the Address Resolution Protocol table.

### Common Usage

```powershell
arp -a
```

### What it Shows

- IP to MAC address mappings
- Devices discovered on the local network

### Common Troubleshooting Uses

- Confirm device presence on LAN
- Detect duplicate IP issues
- Validate ARP resolution

---

# pathping

Combines ping and tracert to provide detailed network path analysis.

### Common Usage

```powershell
pathping 8.8.8.8
```

### What it Shows

- Packet loss across each network hop
- Latency across network path

### Common Troubleshooting Uses

- Identify where packet loss occurs
- Diagnose slow network segments
- Investigate unstable network routes

---

# Quick Troubleshooting Workflow

When diagnosing network connectivity problems, a typical workflow may look like this:

1. Check IP configuration

```
ipconfig
```

2. Test local gateway

```
ping <gateway IP>
```

3. Test external IP connectivity

```
ping 8.8.8.8
```

4. Test DNS resolution

```
ping google.com
nslookup google.com
```

5. Trace the network path

```
tracert 8.8.8.8
```

6. Investigate packet loss or latency

```
ping 8.8.8.8 -n 20
pathping 8.8.8.8
```

---

# Skills Demonstrated

This cheat sheet demonstrates familiarity with:

- TCP/IP troubleshooting
- DNS diagnostics
- Network latency investigation
- Packet loss analysis
- Structured troubleshooting methodology

These tools are commonly used by:

- IT Support Technicians
- Help Desk Engineers
- Network Administrators
- NOC Analysts
