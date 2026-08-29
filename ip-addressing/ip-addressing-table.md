# IP Addressing Plan

**Assigned block:** 172.30.40.0/23 (172.30.40.0 – 172.30.41.255, 512 addresses)
**Method:** VLSM

| VLAN | Name | Subnet | Usable Range | Usable Hosts | Gateway | Broadcast |
|---|---|---|---|---|---|---|
| 20 | Structural Engineering | 172.30.40.0/26 | .1 – .62 | 62 | 172.30.40.1 | 172.30.40.63 |
| 30 | Civil Engineering | 172.30.40.64/27 | .65 – .94 | 30 | 172.30.40.65 | 172.30.40.95 |
| 40 | Drafting & CAD | 172.30.40.96/27 | .97 – .126 | 30 | 172.30.40.97 | 172.30.40.127 |
| 10 | Management / Admin | 172.30.40.128/28 | .129 – .142 | 14 | 172.30.40.129 | 172.30.40.143 |
| 60 | Reception | 172.30.40.144/28 | .145 – .158 | 14 | 172.30.40.145 | 172.30.40.159 |
| 50 | Site Survey (Wireless) | 172.30.40.160/27 | .161 – .190 | 30 | 172.30.40.161 | 172.30.40.191 |
| 70 | Servers | 172.30.40.192/29 | .193 – .198 | 6 | 172.30.40.193 | 172.30.40.199 |
| 80 | Legacy Devices | 172.30.40.200/29 | .201 – .206 | 6 | 172.30.40.201 | 172.30.40.207 |
| 99 | Native / Switch Mgmt | 172.30.40.208/29 | .209 – .214 | 6 | 172.30.40.209 | 172.30.40.215 |
| — | WAN link (R1 ↔ ISP) | 172.30.40.216/30 | .217 – .218 | 2 | — | 172.30.40.219 |

**Reserved for future growth:** 172.30.40.220 – 172.30.41.255 (292 addresses, unallocated)

## Notes

- VLAN 20 is deliberately oversized relative to current headcount to absorb CR1 (8 additional
  staff) without re-addressing.
- VLAN 99 is the native/management VLAN carrying switch-to-switch management traffic — it
  should not be used for end-user devices.
- The WAN link is a point-to-point /30 between R1's ISP-facing interface and the simulated
  ISP router; it is the only subnet in this block not tied to an internal VLAN.
