# Wireless LAN Controller — Dynatrace feature sets

Feature sets currently available in the [Dynatrace Hub](https://www.dynatrace.com/hub/)
that apply to wireless LAN controllers listed in [index.md](index.md).

## Cisco Catalyst Center (DNA Center)

[hub/detail/cisco-catalyst-center-dna-center](https://www.dynatrace.com/hub/detail/cisco-catalyst-center-dna-center/) — single-pane controller and fabric manager covering wired and wireless.

| Feature set      | What it monitors                                                                       |
|------------------|----------------------------------------------------------------------------------------|
| default          | Legacy / generic device metrics — CPU, memory, interface stats                         |
| device           | Per-device health, CPU / memory, temperature, uptime (includes WLCs and APs)           |
| center           | Topology health scores, device counts, client health across the Catalyst Center        |
| site             | Site-level wired and wireless client health, device counts, pending issues             |
| interface        | Operational status, throughput, transmit / receive errors per interface                |
| self-monitoring  | Extension performance — query durations, errors, data-collection efficiency            |

## Meraki (cloud-managed WLC equivalent)

[hub/detail/meraki](https://www.dynatrace.com/hub/detail/meraki/) — the Meraki Dashboard acts as the cloud controller for MR APs.

| Feature set           | What it monitors                                                               |
|-----------------------|--------------------------------------------------------------------------------|
| device-status         | Online / alerting / offline / dormant state per AP                             |
| device-control-plane  | Device uptime, CPU, memory                                                     |
| default               | System uptime, CPU, memory                                                     |
| self-monitoring       | API connectivity, monitored orgs / networks / devices                          |

(`wireless` is documented under [wireless-access-point/featuresets.md](../wireless-access-point/featuresets.md).)

## Generic Cisco Device (SNMP) — Cisco Catalyst 9800 WLC

[hub/detail/generic-cisco-router-snmp-extension](https://www.dynatrace.com/hub/detail/generic-cisco-router-snmp-extension/) — applicable to Catalyst 9800-series WLCs via SNMP.

Relevant feature sets:

| Feature set                  | What it monitors                              |
|------------------------------|-----------------------------------------------|
| Default                      | Uptime, CPU, memory, interface health         |
| Control Plane                | Management-plane CPU, memory, uptime          |
| Power Supply / FRUs          | PSU and fan tray operational status           |
| Sensors / Sensors (Advanced) | Fan state, temperature, raw sensor values     |
| High Availability            | Active-supervisor CPU and HA synchronization  |
| Memory Pools                 | 32-bit / 64-bit memory allocation             |
| Health                       | SNMP transport diagnostics                    |

See [routers/featuresets.md](../routers/featuresets.md) for the full Cisco SNMP feature-set list.

## Drafted feature sets — vendors without a Hub extension

The vendors below have no dedicated WLC extension in the Hub. The
proposals re-use the structure of [Cisco Catalyst Center](https://www.dynatrace.com/hub/detail/cisco-catalyst-center-dna-center/)
(`center`, `site`, `device`, `interface`) and [Meraki](https://www.dynatrace.com/hub/detail/meraki/) (`wireless`,
`device-status`), adjusted to each vendor's controller API.

### HPE Aruba Mobility Conductor / Aruba Central — drafted

Source API: Aruba Central REST API (cloud) or AOS-8 / AOS-10 controller API.

| Feature set      | What it would monitor                                                    |
|------------------|--------------------------------------------------------------------------|
| default          | Controller CPU, memory, uptime, interface status                         |
| center           | Tenant-wide AP / client counts, overall health score                     |
| site             | Per-site (per Aruba "group") AP / client counts, pending alerts          |
| device           | Per-controller and per-AP CPU / memory / uptime / temperature            |
| interface        | Controller uplink op-state, throughput, errors                           |
| radio            | Per-AP radio channel utilization, noise floor, busy %                    |
| client_health    | Connected client count, SNR, retry / drop rates                          |
| ha               | Active / standby controller sync state                                   |
| alarms           | Aruba Central alarms by severity                                         |
| self-monitoring  | Extension query duration and error rate                                  |

### Juniper Mist — drafted

Source API: Mist Cloud REST API.
Reference: cloud-managed shape like Meraki.

| Feature set      | What it would monitor                                                    |
|------------------|--------------------------------------------------------------------------|
| default          | Org-level cloud reachability and API quota                               |
| center           | Org-wide AP / WAN-Edge counts, overall health                            |
| site             | Per-site AP / client counts, SLE scores (Wi-Fi assurance)                |
| device           | Per-AP CPU, memory, uptime, temperature                                  |
| wireless         | Radio channel utilization, noise, interference, coverage SLE             |
| client_health    | Connected client count, throughput SLE, time-to-connect                  |
| alarms           | Mist alerts by severity                                                  |
| self-monitoring  | Extension query duration and error rate                                  |

### Extreme Networks ExtremeCloud IQ / ExtremeWireless — drafted

Source API: ExtremeCloud IQ REST API + SNMP for on-prem controllers.

| Feature set      | What it would monitor                                                    |
|------------------|--------------------------------------------------------------------------|
| default          | Controller CPU, memory, uptime, interface status                         |
| center           | Tenant-wide AP / client counts                                           |
| site             | Per-location AP / client counts, alerts                                  |
| device           | Per-AP / controller CPU, memory, temperature                             |
| radio            | Per-AP radio channel utilization, noise floor                            |
| client_health    | Connected clients, SNR, retry rate                                       |
| alarms           | ExtremeCloud IQ alerts by severity                                       |
| self-monitoring  | Extension query duration and error rate                                  |

### CommScope RUCKUS SmartZone / RUCKUS One — drafted

Source API: RUCKUS SmartZone REST API or RUCKUS One cloud API.

| Feature set      | What it would monitor                                                    |
|------------------|--------------------------------------------------------------------------|
| default          | Controller CPU, memory, uptime, interface status                         |
| center           | Cluster-wide AP / client counts, total throughput                        |
| site             | Per-zone AP / client counts, alarms                                      |
| device           | Per-controller-node and per-AP CPU, memory, uptime                       |
| radio            | Per-AP radio channel utilization, airtime fairness                       |
| client_health    | Connected clients, SNR, dropped associations                             |
| cluster          | SmartZone cluster node state and sync                                    |
| alarms           | SmartZone alarms by severity                                             |
| self-monitoring  | Extension query duration and error rate                                  |

## Fallbacks for any unsupported WLC

- [snmp-generic](https://www.dynatrace.com/hub/detail/snmp-generic/) — generic SNMP coverage for any controller exposing IF-MIB / HOST-RESOURCES-MIB.
- [snmp-autodiscovery](https://www.dynatrace.com/hub/detail/snmp-autodiscovery/) — inventory and reachability for unsupported WLCs.
