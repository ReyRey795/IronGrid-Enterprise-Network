# Lab 03 — VLAN Segmentation

## Objective

Configure Virtual Local Area Networks (VLANs) on a Cisco 2960 switch to isolate two departments within the IronGrid enterprise network.

## Lab Environment

- Cisco Packet Tracer
- Cisco 2960 Switch
- Two PCs
- VLAN 10 — Engineering
- VLAN 20 — Operations

## Network Configuration

| Device | IP Address | VLAN | Switch Port |
|---|---|---|---|
| PC-01 | 192.168.10.10 | 10 | Fa0/1 |
| PC-02 | 192.168.10.11 | 20 | Fa0/2 |

Both devices retained addresses from the same subnet for this initial VLAN isolation experiment. Future labs will configure separate subnets for each VLAN.

## Switch Configuration

```text
enable
configure terminal

vlan 10
name ENGINEERING
exit

vlan 20
name OPERATIONS
exit

interface fastEthernet 0/1
switchport mode access
switchport access vlan 10
exit

interface fastEthernet 0/2
switchport mode access
switchport access vlan 20
exit

end
copy running-config startup-config
```

## Verification

The `show vlan brief` command confirmed:

- VLAN 10 (ENGINEERING) was active on Fa0/1.
- VLAN 20 (OPERATIONS) was active on Fa0/2.
- Both ports were removed from the default VLAN 1.

## Connectivity Tests

| Test | Result | Expected |
|---|---|---|
| PC-01 → PC-02 | Failed | Failed |
| PC-02 → PC-01 | Failed | Failed |

Both tests confirmed that traffic could not cross the VLAN boundary using the existing Layer 2 switch configuration.

## Troubleshooting Observation

During testing, connectivity initially appeared inconsistent. We verified the source and destination IP addresses and repeated the tests.

Both cross-VLAN ping attempts failed as expected.

This highlighted the importance of checking test conditions before making configuration changes.

## Lessons Learned

1. A VLAN creates a separate Layer 2 broadcast domain.
2. Switch access ports can be assigned to specific VLANs.
3. VLANs prevent ordinary Layer 2 forwarding between separate broadcast domains.
4. Devices in separate VLANs require an appropriate Layer 3 path to communicate.
5. VLAN separation alone is not a complete security policy; additional controls can be required to restrict routed traffic.

## Final Result

Successfully configured and verified VLAN-based isolation between Engineering and Operations.

**Status:** Completed

**Next Lab:** Lab 04 — Subnet Design and Inter-VLAN Routing