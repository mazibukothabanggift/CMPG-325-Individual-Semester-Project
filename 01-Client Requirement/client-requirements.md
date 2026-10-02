# Client Requirements Analysis

**Client:** Motswaledi Civil & Structural Engineers (Mahikeng)
**Industry:** Engineering (civil & structural consultancy)
**Project ID:CMPG325-2026-064 | **Client ID:CLI-064 
Assigned addressing block: 172.30.40.0/23

## 1. Business context

Motswaledi is a civil and structural engineering consultancy. Day-to-day work centres on
structural design calculations, civil site design, and the production of technical drawings
(CAD/drafting), supported by a survey/field team that spends time away from the office.

## 2. Departments and user needs

| Department | Function | Network needs |
|---|---|---|
| Management / Admin | Firm leadership, HR, finance | Isolated from general staff, moderate reliability |
| Structural Engineering | Design calculations, structural CAD | File sharing, access to server VLAN, room for growth |
| Civil Engineering | Site/civil design work | File sharing, access to server VLAN |
| Drafting & CAD | Drawing production, plotting | Heaviest bandwidth use — large drawing files, plotter access |
| Site Survey / Field | Surveyors, often mobile | Wireless connectivity |
| Reception | Client-facing, visitor point of contact | Light use, no access to sensitive VLANs |
| Servers | Central file server (drawings), print server | Highest protection, restricted access |
| Legacy Devices | Older plotter/scanner without modern security | Must be reachable but isolated |

## 3. Design constraint

Legacy devices without modern security features must still be accommodated safely. Addressed
by placing them in a dedicated VLAN (80) with ACLs on the core switch restricting them to only
the traffic they need (e.g. printing to the file server), rather than open access to the rest
of the network.

## 4. Change request (CR1)

The client will sign 8 additional staff into one department. The network must absorb this
without a redesign. Structural Engineering was chosen to receive the growth allowance, since
it is the largest technical team — its VLAN (20) is sized at a /26 (62 usable addresses) from
the outset, well beyond current headcount, so new staff simply take the next free address.

## 5. Assigned technical challenge

**Default Routing (edge/ISP path design)** — Intermediate difficulty. The edge router (R1)
uses a single static default route out to the simulated ISP for all internet-bound traffic;
the ISP router holds a static route back to the full 172.30.40.0/23 block via R1's WAN
interface. No dynamic routing protocol is required or used for this design.

## 6. Summary of requirements driving the design

- Segment departments into VLANs for security and to control broadcast domains
- Size subnets with realistic headroom, especially where CR1 applies
- Isolate legacy devices behind ACLs while keeping them reachable
- Provide a working default route to the internet at the network edge
- Produce a fully working, testable Packet Tracer implementation
