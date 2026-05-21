# Switches — Dynatrace feature sets

Feature sets currently available in the [Dynatrace Hub](https://www.dynatrace.com/hub/)
that apply to enterprise switches listed in [index.md](index.md).

## Generic Cisco Device (SNMP)

[hub/detail/generic-cisco-router-snmp-extension](https://www.dynatrace.com/hub/detail/generic-cisco-router-snmp-extension/) — also covers Catalyst and Nexus switches.

Relevant feature sets for switching:

| Feature set            | What it monitors                                            |
|------------------------|-------------------------------------------------------------|
| Default                | Uptime, CPU, memory, interface health                       |
| Interfaces 32-bit      | Standard interface traffic and errors                       |
| Interfaces 64-bit      | High-capacity interface bytes / packets                     |
| Advanced Interfaces    | Multicast / broadcast / unicast and CRC errors              |
| Control Plane          | CPU, memory and uptime for the management plane             |
| High Availability      | Active-supervisor CPU and HA synchronization                |
| Power Supply / FRUs    | PSU and fan tray operational status                         |
| Sensors                | Fan state and temperature                                   |
| Memory Pools           | 32-bit and 64-bit memory allocation                         |
| Neighbor-Discovery     | LLDP topology data                                          |
| Entity-Enrichment      | Stack member details                                        |
| Health                 | SNMP transport diagnostics                                  |
| Traffic                | TCP / UDP segment activity                                  |

See [routers/featuresets.md](../routers/featuresets.md) for the full list — the extension is shared.

## HPE H3C Switch

[hub/detail/hpe-h3c-switch](https://www.dynatrace.com/hub/detail/hpe-h3c-switch/)

| Feature set         | What it monitors                                                                |
|---------------------|---------------------------------------------------------------------------------|
| Default             | System uptime, CPU usage, memory, interface status (5 metrics)                  |
| Interfaces          | In/out bytes, errors, discards, link speed, last-change timestamp (8 metrics)   |
| Advanced interfaces | Multicast / broadcast / unicast packet counts (6 metrics)                       |

## Juniper Networks (SNMP)

[hub/detail/juniper-networks-snmp](https://www.dynatrace.com/hub/detail/juniper-networks-snmp/) — covers EX / QFX switching.

Relevant feature sets for switching:

| Feature set         | What it monitors                                          |
|---------------------|-----------------------------------------------------------|
| default             | Uptime, CPU, memory, interface status                     |
| Interfaces          | Traffic, errors, discards, packet stats per interface     |
| Advanced interfaces | Multicast / broadcast / unicast and CRC errors            |
| VLAN                | VLAN / portgroup entities (EX devices)                    |
| Bridge              | Bridge / VLAN entities                                    |
| ARP Table           | ARP table entries                                         |
| Routing Engines     | RE memory, CPU, temperature, state                        |
| FRU                 | Field Replaceable Unit state and temperature              |
| Neighbor Discovery  | (via Adjacency Info / LLDP collection)                    |

## Meraki

[hub/detail/meraki](https://www.dynatrace.com/hub/detail/meraki/) — Meraki MS cloud-managed switches.

| Feature set           | What it monitors                                            |
|-----------------------|-------------------------------------------------------------|
| default               | System uptime, CPU, memory                                  |
| device-status         | Online / alerting / offline / dormant state                 |
| device-control-plane  | Device uptime, CPU, memory for MS switches                  |
| switchport            | Port status, client counts, upstream / downstream usage     |
| interface             | Inbound / outbound bytes                                    |
| powersupply           | PSU availability and connection state                       |
| self-monitoring       | API connectivity, monitored org / network / device counts   |

## Generic network device (SNMP)

[hub/detail/snmp-generic](https://www.dynatrace.com/hub/detail/snmp-generic/) — fallback for any switch exposing IF-MIB / BRIDGE-MIB. See [routers/featuresets.md](../routers/featuresets.md#generic-network-device-snmp).
