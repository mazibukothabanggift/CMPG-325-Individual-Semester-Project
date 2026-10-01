# CMPG-325-Individual-Semester-Project
This repository documents the design, implementation, and testing of a computer network for Motswaledi Civil &amp; Structural Engineers, a civil/structural engineering consultancy based in Mahikeng. The network is designed and simulated in Cisco Packet Tracer as part of the CMPG 325 Computer Networks individual semester project.
CMPG 325 — Individual Semester Project
Client: Motswaledi Civil & Structural Engineers (Mahikeng)
Project ID: CMPG325-2026-064 Client ID: CLI-064 Industry: Engineering Assigned addressing block: 172.30.40.0/23 Assigned networking challenge: Default Routing (edge/ISP path design) — Intermediate

Project overview
This repository documents the design, implementation, and testing of a computer network for Motswaledi Civil & Structural Engineers, a civil/structural engineering consultancy based in Mahikeng. The network is designed and simulated in Cisco Packet Tracer as part of the CMPG 325 Computer Networks individual semester project.

The client scenario, requirements, design constraint, and change request are specified in the official project brief (not reproduced here in full — see docs/01-client-requirements.md for the working analysis).

Assigned networking challenge
Default Routing (edge/ISP path design). The edge router is configured with a static default route toward the simulated ISP, since this is a single-homed small business site with no need for a dynamic routing protocol. Full configuration and verification evidence lives in evidence/testing/ once Milestone 2 work is complete.

Design constraint
Legacy devices without modern security features are accommodated on an isolated VLAN with an access control list restricting them to only the traffic they need (e.g. printing), rather than open access to the rest of the network or the internet.

Change request (CR1)
The client signs 8 additional staff in one department. The network is designed with spare address capacity in that department's subnet so this is absorbed without re-subnetting or redesigning the network. See docs/03-ip-addressing.md for how this is built into the addressing plan.

Repository structure
├── docs/
│   ├── 01-client-requirements.md   — requirements analysis and assumptions
│   ├── 02-network-design.md        — physical & logical topology
│   ├── 03-ip-addressing.md         — VLSM addressing plan
│   └── assumptions.md              — documented design assumptions
├── packet-tracer/                  — .pkt file(s) (Milestone 2)
├── evidence/
│   ├── screenshots/                — config & connectivity evidence
│   └── testing/                    — verification output, troubleshooting notes
├── video/                          — link/notes for the 15–20 min demo
└── README.md
Status
Milestone 1 — Client design review (client requirements, topology, IP plan, initial repo)
Milestone 2 — Client implementation review (working Packet Tracer file, assigned feature, testing evidence)
Final submission — full portfolio, technical report, video demonstration
Author
Rabba Mazibuko — Student Number 35952504 Individual project — CMPG 325, North-West University, Department of Computer Science and Information Systems
