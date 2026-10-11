# Lab 02 — ARP and MAC Address Analysis

## Objective
Investigate how computers discover MAC addresses and how switches learn and forward Ethernet frames within a Local Area Network (LAN).

## Lab Environment
- Cisco Packet Tracer
- Cisco 2960 Switch
- Two PCs connected using Ethernet cables
- Network: 192.168.10.0/24

## Device Configuration

| Device | IPv4 Address | MAC Address | Switch Port |
|---|---|---|---|
| PC-01 | 192.168.10.10 | 000A.F3B3.B655 | Fa0/1 |
| PC-02 | 192.168.10.11 | 0001.C9EA.E13B | Fa0/2 |

## Commands Used

**On PC-01:**
- `ping 192.168.10.11` — Verified communication.
- `arp -a` — Examined learned IP-to-MAC mappings.
- `arp -d` — Cleared ARP entries for testing.

**On the Cisco switch:**
- `enable` — Entered privileged EXEC mode.
- `show mac address-table` — Examined the switch's learned MAC addresses.

## Analysis

**ARP Request:** PC-01 broadcasts a request using destination MAC address FFFF.FFFF.FFFF to discover PC-02's physical address.

**ARP Reply:** PC-02 responds directly to PC-01 using its MAC address, 000A.F3B3.B655.

**Switch MAC Learning:** The switch learns source MAC addresses from incoming Ethernet frames and associates them with switch ports.

**ICMP Communication:** After address resolution, PC-01 can send ICMP Echo Requests to PC-02 using its destination MAC address.

## Troubleshooting Observation
Initially, the switch's MAC address table appeared empty. After generating network traffic with a ping, the switch displayed two dynamically learned MAC addresses.

This demonstrated the importance of generating traffic when inspecting dynamically learned MAC address entries.

## Results
Successfully examined ARP behavior, verified MAC address learning, and distinguished broadcast traffic from known-unicast communication.

## Lessons Learned
- ARP resolves IPv4 addresses to MAC addresses on the local network.
- Switches use MAC address tables to forward Ethernet frames.
- ARP requests are normally broadcast.
- ARP replies are normally unicast.
- Dynamic MAC address entries may age out without traffic.