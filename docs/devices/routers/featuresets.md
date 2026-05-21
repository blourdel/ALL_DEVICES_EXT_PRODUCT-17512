# Routers — Dynatrace feature sets

Feature sets currently available in the [Dynatrace Hub](https://www.dynatrace.com/hub/)
that apply to enterprise routers listed in [index.md](index.md).

## Generic Cisco Device (SNMP)

[hub/detail/generic-cisco-router-snmp-extension](https://www.dynatrace.com/hub/detail/generic-cisco-router-snmp-extension/)

| Feature set            | What it monitors                                                                 |
|------------------------|----------------------------------------------------------------------------------|
| Default                | System uptime, CPU usage, memory status, interface health                        |
| Advanced Interfaces    | Multicast / broadcast / unicast packet counts and CRC errors                     |
| Interfaces 32-bit      | Standard interface traffic and error counters                                    |
| Interfaces 64-bit      | High-capacity interface bytes / packets                                          |
| Control Plane          | CPU, memory and uptime for the management plane                                  |
| High Availability      | Active-supervisor CPU and HA synchronization state                               |
| Power Supply           | PSU operational status                                                           |
| FRUs                   | Field Replaceable Unit health (PSU, fan tray)                                    |
| Sensors                | Fan state and temperature                                                        |
| Sensors (Advanced)     | Raw sensor values across measurement types                                       |
| OSPF                   | OSPF neighbor adjacency state                                                    |
| BGP                    | BGP peer state and timers                                                        |
| Cisco BGP              | Extended BGP metrics (update counts, peer admin status)                          |
| EIGRP                  | EIGRP peer RTT                                                                   |
| Traffic                | TCP/UDP connection statistics, segment analysis                                  |
| Health                 | SNMP message delivery and error conditions                                       |
| Memory Pools           | 32-bit and 64-bit memory allocation                                              |
| Neighbor-Discovery     | LLDP topology data                                                               |
| Entity-Enrichment      | Physical component state for device-stack details                                |

## Juniper Networks (SNMP)

[hub/detail/juniper-networks-snmp](https://www.dynatrace.com/hub/detail/juniper-networks-snmp/)

| Feature set         | What it monitors                                                  |
|---------------------|-------------------------------------------------------------------|
| default             | Uptime, CPU, memory, interface status                             |
| Interfaces          | Traffic, errors, discards, packet statistics per interface        |
| Advanced interfaces | Multicast / broadcast / unicast and CRC errors                    |
| Routing Engines     | RE memory, CPU, temperature, state                                |
| Routing Info        | IP routing table information                                      |
| Adjacency Info      | IS-IS adjacency / topology discovery                              |
| ARP Table           | ARP table entries                                                 |
| VLAN                | VLAN / portgroup entities (EX devices)                            |
| Bridge              | Bridge / VLAN entities                                            |
| IP Addressing       | IP address entities                                               |
| FRU                 | Field Replaceable Unit state and temperature                      |
| TCP and UDP         | Connection states, transfer and error metrics                     |
| Disks               | Disk capacity / usage                                             |
| Ping Results        | Probe response, RTT, latency                                      |
| Applications        | Installed apps and process resource consumption                   |

## Generic network device (SNMP)

[hub/detail/snmp-generic](https://www.dynatrace.com/hub/detail/snmp-generic/) — vendor-agnostic fallback for any router exposing standard MIBs.

| Feature set         | What it monitors                                       |
|---------------------|--------------------------------------------------------|
| default             | System uptime, interface status                        |
| Interfaces          | Inbound packets discarded and similar IF-MIB counters  |
| Interfaces 32-bit   | Standard octets in / out                               |
| Interfaces 64-bit   | High-speed octets in / out                             |
| Advanced interfaces | Multicast / broadcast / unicast packet counts          |
| Traffic             | TCP / UDP segment activity                             |
| Control Plane       | sysUpTime and management re-initialization timing      |
| SNMP Health         | SNMP transport diagnostics                             |

## Commonality across the three existing router extensions

Theme-by-theme mapping of feature sets that already exist in the Cisco,
Juniper and Generic Network Device extensions on the Hub. Cells marked
"—" indicate the theme is not exposed as a dedicated feature set in
that extension (but may be partially covered by a broader one).

| Theme                                     | Generic Cisco Device    | Juniper Networks                    | Generic network device |
|-------------------------------------------|-------------------------|-------------------------------------|------------------------|
| Baseline health (uptime / CPU / mem / IF) | Default                 | default                             | default                |
| Interface counters (32-bit)               | Interfaces 32-bit       | Interfaces *                        | Interfaces 32-bit      |
| Interface counters (64-bit)               | Interfaces 64-bit       | Interfaces *                        | Interfaces 64-bit      |
| Advanced interfaces (mcast/bcast/CRC)     | Advanced Interfaces     | Advanced interfaces                 | Advanced interfaces    |
| Control / management plane                | Control Plane           | (in Routing Engines)                | Control Plane          |
| Sensors (fan, temperature)                | Sensors / Sensors (Adv) | (in FRU / RE temp)                  | —                      |
| Power Supply                              | Power Supply            | (in FRU)                            | —                      |
| Field Replaceable Units                   | FRUs                    | FRU                                 | —                      |
| High availability                         | High Availability       | —                                   | —                      |
| Memory pools / heap detail                | Memory Pools            | (in default)                        | —                      |
| SNMP transport health                     | Health                  | —                                   | SNMP Health            |
| Entity-Enrichment / stack info            | Entity-Enrichment       | (in Routing Engines)                | —                      |
| Routing table info                        | (implicit)              | Routing Info                        | —                      |
| OSPF                                      | OSPF                    | —                                   | —                      |
| BGP                                       | BGP / Cisco BGP         | —                                   | —                      |
| EIGRP                                     | EIGRP                   | —                                   | —                      |
| IS-IS / adjacency                         | —                       | Adjacency Info                      | —                      |
| Neighbor discovery (LLDP / CDP)           | Neighbor-Discovery      | (Adjacency)                         | —                      |
| ARP / VLAN / Bridge / IP entities         | —                       | ARP / VLAN / Bridge / IP Addressing | —                      |
| TCP / UDP traffic statistics              | Traffic                 | TCP and UDP                         | Traffic                |
| Reachability / synthetic probes           | —                       | Ping Results                        | —                      |
| Disks                                     | —                       | Disks                               | —                      |
| Applications / process resources          | —                       | Applications                        | —                      |

\* Juniper consolidates 32-bit and 64-bit counters in a single `Interfaces` feature set.

### Themes present in ≥ 2 of the 3 extensions (consensus core)

These are the universal building blocks any router extension should
expose:

1. **default** — uptime, CPU, memory, interface op-status
2. **Interfaces** — byte / packet counters (32-bit + 64-bit)
3. **Advanced interfaces** — multicast / broadcast / unicast / errors
4. **Control Plane** — management plane CPU / memory / uptime
5. **FRUs** — field replaceable unit state (covers PSU + fan tray)
6. **Sensors** — fan and temperature readings
7. **Traffic** — system-level TCP / UDP segment activity
8. **Health (SNMP Health)** — SNMP transport diagnostics (when polled over SNMP)
9. **Neighbor Discovery** — LLDP / CDP adjacencies
10. **Routing protocols** — OSPF, BGP at minimum

### Themes present in only one extension (vendor-specific)

- Cisco-only: HA (supervisor), Memory Pools, Cisco BGP, EIGRP, Entity-Enrichment
- Juniper-only: Routing Engines, IS-IS Adjacency, ARP / VLAN / Bridge / IP entities, Disks, Applications, Ping Results

## Proposed rationalized feature set — Fortinet as a router

FortiGate already ships in the Hub as a firewall extension
([fortinet-fortigate-1](https://www.dynatrace.com/hub/detail/fortinet-fortigate-1/)) with
five feature sets: `Ping`, `Overview`, `Interfaces`, `default`, `IPSec Tunnels`.
When the same appliance is monitored *as a router* (branch / WAN edge),
the firewall view leaves several router-specific themes uncovered.
The proposal below extends FortiGate to match the consensus router core
identified above, while preserving the FortiGate-specific value
(`Ping`, `Overview`, `IPSec Tunnels`).

Source: FortiGate REST API + SNMP (FORTINET-FORTIGATE-MIB / IF-MIB / OSPF-MIB / BGP4-MIB).

### Consensus core — keep / add

| Feature set         | Status     | What it monitors / would monitor                                          | Modelled on                                      |
|---------------------|------------|---------------------------------------------------------------------------|--------------------------------------------------|
| default             | **exists** | Uptime, CPU, memory, interface bandwidth, errors, status                  | Cisco `Default` / Juniper `default`              |
| Overview            | **exists** | CPU, memory, disk, sessions, connectivity (FortiGate aggregate)           | Fortinet-specific superset of `default`          |
| Interfaces          | **exists** | Traffic, errors, link speed, op-status (32-bit & 64-bit)                  | Cisco `Interfaces 64-bit` / Juniper `Interfaces` |
| Advanced Interfaces | **add**    | Multicast / broadcast / unicast packets, CRC errors per interface         | Cisco / Juniper / Generic `Advanced Interfaces`  |
| Control Plane       | **add**    | Management-VDOM CPU / memory, sysUpTime, re-init timing                   | Cisco / Generic `Control Plane`                  |
| Sensors             | **add**    | Fan speed, temperature (CPU / PSU / chassis), voltage                     | Cisco `Sensors` / Juniper FRU temperature        |
| Power Supply        | **add**    | PSU operational state                                                     | Cisco `Power Supply`                             |
| FRUs                | **add**    | Fan tray, line card, SFP, replaceable module status                       | Cisco `FRUs` / Juniper `FRU`                     |
| Health              | **add**    | SNMP transport diagnostics (when polled over SNMP)                        | Cisco `Health` / Generic `SNMP Health`           |
| High Availability   | **add**    | FGCP / FGSP cluster state, sync status, active vs passive role            | Cisco `High Availability`                        |
| Traffic             | **add**    | System-level TCP / UDP connection statistics                              | Cisco `Traffic` / Juniper `TCP and UDP`          |
| Ping                | **exists** | Synthetic reachability — packet counts, loss, RTT                         | Juniper `Ping Results`                           |

### Routing-specific — add

| Feature set        | Status  | What it would monitor                                                      | Modelled on               |
|--------------------|---------|----------------------------------------------------------------------------|---------------------------|
| Routing Info       | **add** | FIB / RIB size, route count by protocol, default-route presence            | Juniper `Routing Info`    |
| OSPF               | **add** | OSPF neighbor adjacency state, area summary, LSA counts                    | Cisco `OSPF`              |
| BGP                | **add** | BGP peer state, timers, prefix received / advertised                       | Cisco `BGP` / `Cisco BGP` |
| Neighbor Discovery | **add** | LLDP / CDP neighbor table                                                  | Cisco `Neighbor-Discovery`|

### Fortinet-specific — keep / extend

| Feature set     | Status     | What it monitors / would monitor                                                       | Notes                                                  |
|-----------------|------------|----------------------------------------------------------------------------------------|--------------------------------------------------------|
| IPSec Tunnels   | **exists** | Site-to-site tunnel state, traffic, encryption / decryption, proxy state               | Branch routers typically terminate VPN here            |
| SD-WAN Members  | **add**    | When FortiGate runs SD-WAN — member state, bandwidth, SLA (loss / latency / jitter)    | See [sd-wan/featuresets.md](../sd-wan/featuresets.md)  |
| Sessions        | **add**    | Active / peak sessions per VDOM, creation rate, session-table utilization              | Specialises the session count in `Overview`            |

### Themes intentionally omitted

- **Memory Pools**, **Entity-Enrichment**, **EIGRP** — Cisco-platform constructs with no clean FortiGate equivalent.
- **ARP / VLAN / Bridge / IP Addressing** — Juniper-style L2/L3 entity feature sets; FortiGate exposes this data inline with `Interfaces` and the routing table.
- **Routing Engines** — Juniper RE-specific; FortiGate is single-control-plane per appliance.
- **Disks**, **Applications** — partially covered by FortiGate `Overview`; not worth a dedicated feature set on a router profile.

## Related

- [Cisco Catalyst SD-WAN Manager (Viptela)](https://www.dynatrace.com/hub/detail/cisco-catalyst-sd-wan-manager-viptela) — see [sd-wan/featuresets.md](../sd-wan/featuresets.md) for routers operating in SD-WAN mode.
- [Cisco Catalyst Center (DNA Center)](https://www.dynatrace.com/hub/detail/cisco-catalyst-center-dna-center/) — fabric-level view of Catalyst routers.
- [Meraki](https://www.dynatrace.com/hub/detail/meraki/) — MX security appliance acts as branch router.
