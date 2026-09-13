# Network Architecture & Security Project — VPN-MPLS, Redundant LAN & Monitoring

Design and implementation of a complete enterprise network for a company with one headquarters and two remote branches, built and validated in **GNS3**. Academic project — TEK-UP University, Network Security & Information Systems (ING4-J SSIR-H).

## Overview

The network is built in three parts, each following the same structure (introduction, technology overview, architecture, work environment, implementation, validation tests, conclusion):

1. **IP/MPLS backbone with VRF** — connects all company sites through a simulated operator network, with full traffic isolation per client.
2. **Redundant headquarters LAN** — keeps the network available even during a failure, using link aggregation and automatic gateway failover.
3. **Monitoring & security solution** — controls network access, monitors devices in real time, and measures link quality.

## 1. VPN-MPLS Backbone

- **MPLS** label switching (RFC 3031) with **LDP** for label distribution (RFC 5036).
- **VRF** (RFC 4364) for per-client traffic isolation on PE routers.
- **MP-BGP** (RFC 4760) to exchange VPNv4 routes between PE routers (iBGP).
- **OSPF** (RFC 2328) in the backbone (Area 0) and in each client site.
- Addressing plan for backbone links, CE–PE links, and loopbacks; label switching (LFIB/LSP) tables documented per router.

## 2. Redundant Enterprise LAN

- **802.1Q** VLAN trunking and **VTP** for automatic VLAN propagation (Server/Client).
- **EtherChannel** (IEEE 802.3ad) for link aggregation between switches.
- **HSRP** (RFC 2281) for gateway high availability between two core switches ("Fédérateurs").
- **DHCP** (RFC 2131) and **inter-Fédérateur OSPF** (VLAN 300).
- Branch router configured as **router-on-a-stick** with local DHCP.
- Validation: HSRP failover, DHCP, OSPF adjacency, inter-/intra-VLAN connectivity, and combined HSRP + EtherChannel failover tests.

## 3. Monitoring & Security

- **AAA / RADIUS** (RFC 2865) centralized authentication.
- Extended **ACL** restricting VTY (SSH) access to two authorized administrators.
- **SNMPv3** (RFC 3411) with authentication and encryption.
- **Syslog** (RFC 5424) centralized logging.
- **NTP** (RFC 5905) time synchronization across all devices.
- **IP SLA** (UDP-Jitter) to measure latency, jitter, and packet loss between branches and headquarters.
- **Zabbix** as the network management system (NMS) for real-time supervision.

## Tools & Environment

| Tool | Purpose |
|---|---|
| GNS3 | Network simulation (Cisco IOS images: routers, Catalyst 3650/3850, 2960 switches) |
| VMware Workstation | Virtual machines for end-user PCs and management servers |
| Zabbix | Network monitoring / NMS |
| Cisco IOS (MPLS/LDP/MP-BGP/VRF-capable images) | Routing and switching |

## Report Structure

The full report (French, LaTeX/PDF, 53 pages) includes:
- Table of contents, list of figures, list of tables
- General introduction
- Three chapters (MPLS backbone, redundant LAN, monitoring & security), each with configuration excerpts and validation tests
- Bibliography and a glossary of networking acronyms (MPLS, VRF, BGP, HSRP, AAA, SNMP, etc.)

## Authors

- **Hamdi Maïssa**
- **Reguigui Aymen**
- Supervised by M. Tarek Hdiji — TEK-UP University, 2025–2026
