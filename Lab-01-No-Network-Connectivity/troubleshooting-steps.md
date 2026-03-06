# Lab 1 – No Network Connectivity

## Scenario

A user reports that their workstation cannot access the internet or internal company resources. Web pages do not load, and shared drives are unreachable.

---

## Objective

Identify the cause of the connectivity problem and restore normal network access.

---

## Step 1 – Check IP Configuration

Command used:

```powershell
ipconfig

Sample Result:
Ethernet adapter Ethernet:

   Connection-specific DNS Suffix  . :
   IPv4 Address. . . . . . . . . . : 169.254.84.22
   Subnet Mask . . . . . . . . . . : 255.255.0.0
   Default Gateway . . . . . . . . :

Analysis

The workstation has an APIPA address (169.254.x.x), which usually means it did not receive a valid IP address from DHCP.

## Step 2 – Check Full Adapter Details

Command used:
ipconfig /all

Analysis

The adapter is enabled, but there is no valid DHCP lease information. This suggests the computer could not communicate with the DHCP server.

## Step 3 – Renew the IP Address

Commands used:
ipconfig /release
ipconfig /renew

Sample result:
Ethernet adapter Ethernet:

   IPv4 Address. . . . . . . . . . : 192.168.10.54
   Subnet Mask . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . : 192.168.10.1

Analysis

The workstation successfully received a valid DHCP-assigned address.

## Step 4 – Test Connectivity to the Gateway

Command used:
ping 192.168.10.1

Sample result:
Reply from 192.168.10.1: bytes=32 time<1ms TTL=64
Reply from 192.168.10.1: bytes=32 time<1ms TTL=64
Reply from 192.168.10.1: bytes=32 time<1ms TTL=64
Reply from 192.168.10.1: bytes=32 time<1ms TTL=64

Analysis

The workstation can now communicate with the local gateway.

## Step 5 – Test External Connectivity

Command used:
ping 8.8.8.8

Sample result:
Reply from 8.8.8.8: bytes=32 time=18ms TTL=117
Reply from 8.8.8.8: bytes=32 time=19ms TTL=117

Analysis

Internet connectivity is working.

## Step 6 – Test DNS Resolution

Command used:
ping google.com

Sample result:
Pinging google.com [142.250.190.14] with 32 bytes of data:
Reply from 142.250.190.14: bytes=32 time=20ms TTL=117

Analysis

DNS name resolution is also working properly.

Root Cause

The workstation failed to obtain a DHCP lease and self-assigned an APIPA address.

Resolution

Released and renewed the IP configuration, which restored a valid address and normal network connectivity.

Skills Demonstrated
  IP address troubleshooting
  DHCP issue identification
  Connectivity verification
  Structured troubleshooting documentation
