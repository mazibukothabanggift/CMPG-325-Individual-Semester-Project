# Network Design Decisions

## 1. Topology overview

**Physical hierarchy:** ISP router → Edge router (R1) → Core switch (L3, inter-VLAN routing) →
three access switches (Office, Engineering, Server/Legacy) + a wireless AP for the Site Survey
VLAN.

**Why this shape:** A single edge router gives one clean place to enforce the assigned
Default Routing challenge — everything internal is already known via directly connected
subnets, so R1 only needs one static default route out. A layer-3 core switch handles
inter-VLAN routing internally (router-on-a-stick via trunked subinterfaces would also satisfy
this if a single router is preferred instead of an L3 switch), keeping east-west traffic off
the edge router entirely.

## 2. VLAN and subnet sizing

The 172.30.40.0/23 block is carved with VLSM so each department gets only the space it
realistically needs, while the two departments most likely to grow (Structural Engineering,
plus general future expansion) have real headroom:

- VLAN 20 (Structural Engineering) is sized at /26 (62 hosts) specifically to absorb CR1's
  8 additional staff without touching the addressing scheme.
- Smaller, static departments (Reception, Management) get /28s — enough with some spare
  capacity, not wastefully large.
- Servers, legacy devices, and switch management get tight /29s, since these are fixed,
  small device counts.
- 172.30.40.220 – 172.30.41.255 is left completely unallocated as a reserve block for any
  growth beyond CR1.

Full addressing table: see `03-ip-addressing/ip-addressing-table.md`.

## 3. Handling the legacy device constraint

Legacy devices sit in their own VLAN (80) behind the server switch rather than being mixed
into a general-purpose VLAN. An ACL on the core switch limits VLAN 80 to only the specific
traffic it needs (e.g. reaching the print/file server), so an insecure device can't be used
as a pivot point into the rest of the network. This satisfies "accommodated safely" without
requiring the devices themselves to support anything modern.

## 4. Handling CR1 (change request)

Rather than re-subnetting when the extra 8 staff arrive, Structural Engineering's VLAN was
pre-sized at /26. The change is absorbed purely by assigning new DHCP leases or static
addresses within the existing 172.30.40.0/26 range — no VLAN changes, no re-cabling, no
router configuration changes.

## 5. Default routing design (assigned challenge)

- **R1 (edge router):** one static route, `ip route 0.0.0.0 0.0.0.0 <next-hop-toward-ISP>`,
  sends all non-local traffic out to the ISP.
- **ISP router:** one static route back, `ip route 172.30.40.0 255.255.254.0 <R1-WAN-interface>`,
  so return traffic finds its way to the internal network.
- **Verification plan:** `ping`/`tracert` from an internal host to a simulated external
  address, plus `show ip route` on both routers to confirm the default route is installed
  and being used.


