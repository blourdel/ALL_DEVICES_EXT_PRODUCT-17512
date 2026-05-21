# SD-WAN — Dynatrace feature sets

Feature sets currently available in the [Dynatrace Hub](https://www.dynatrace.com/hub/)
that apply to SD-WAN platforms listed in [index.md](index.md), plus drafted
feature sets proposed for vendors not yet covered by a dedicated extension.

## Existing Hub extensions

### Cisco SD-WAN

[hub/detail/cisco-catalyst-sd-wan-manager-viptela](https://www.dynatrace.com/hub/detail/cisco-catalyst-sd-wan-manager-viptela) — uses the vManage REST API to collect metrics for the entire SD-WAN fabric.

| Feature set            | What it monitors                                                                       |
|------------------------|----------------------------------------------------------------------------------------|
| default                | Standard network device metrics — CPU, memory, interface status and traffic            |
| fabric_infra           | Aggregate health counts across sites, devices, hardware, inventory, tunnels            |
| device_health          | Per-device CPU load, memory, health, reachability, quality-of-experience scores        |
| device_statistics      | Detailed CPU, memory, disk and process metrics per SD-WAN device                       |
| interface_statistics   | Interface-level traffic, errors, drops and capacity utilization                        |
| advanced_interface     | Packet counts (multicast / broadcast / unicast) per interface                          |
| approute_statistics    | Tunnel-level QoS, loss, latency, jitter, throughput across TLOCs                       |
| alarms                 | Alarm counts with severity filtering, optional event creation                          |
| self-monitoring        | Query execution times, error tracking for the extension itself                         |

### Meraki (MX security appliance — SD-WAN mode)

[hub/detail/meraki](https://www.dynatrace.com/hub/detail/meraki/)

| Feature set           | What it monitors                                                               |
|-----------------------|--------------------------------------------------------------------------------|
| uplink                | MX uplink status, loss, latency, data transferred                              |
| vpn                   | Auto-VPN status, throughput, latency, jitter, loss %, MOS between MX sites    |
| device-status         | Online / alerting / offline / dormant state per MX appliance                   |
| device-control-plane  | MX device uptime, CPU, memory                                                  |
| cellular              | Cellular uplink status and signal quality for LTE-equipped MX                  |
| interface             | Inbound / outbound bytes                                                       |
| default               | System uptime, CPU, memory                                                     |

## Drafted feature sets — vendors without a Hub extension

The vendors below are not yet covered by a dedicated Hub extension. The
proposals re-use the structure of the Cisco SD-WAN extension (fabric +
device + tunnel layers), adjusted to each vendor's controller API.

### Fortinet Secure SD-WAN — drafted

Source API: FortiGate REST API + FortiManager / FortiAnalyzer.
Reference: [Fortinet FortiGate](https://www.dynatrace.com/hub/detail/fortinet-fortigate-1/) for shared device-level feature sets.

| Feature set           | What it would monitor                                                              |
|-----------------------|------------------------------------------------------------------------------------|
| default               | CPU, memory, interface status — reused from FortiGate `default`                    |
| sdwan_members         | SD-WAN member interface state, bandwidth, packet loss, latency, jitter, MOS        |
| sdwan_rules           | Per-rule traffic steering decisions, hit counts, preferred-member selection        |
| sdwan_health_check    | Health-check probe results per member (response time, success rate)                |
| ipsec_tunnels         | Overlay tunnel status, traffic, SA renegotiations (FortiGate `IPSec Tunnels`)      |
| fabric_infra          | Aggregate counts of sites / hubs / spokes via FortiManager ADOM                    |
| alarms                | FortiAnalyzer event counts with severity filtering                                 |
| self-monitoring       | Extension query duration and error rate                                            |

### Palo Alto Prisma SD-WAN — drafted

Source API: Prisma SD-WAN (CloudGenix) controller API.
Reference: Cisco SD-WAN feature-set shape; device-level metrics modelled on [Palo Alto Firewalls](https://www.dynatrace.com/hub/detail/palo-alto-firewalls-1/).

| Feature set           | What it would monitor                                                              |
|-----------------------|------------------------------------------------------------------------------------|
| default               | ION appliance CPU, memory, interface status                                        |
| device_health         | Per-ION health score, reachability, control-channel status                         |
| fabric_infra          | Site / ION / circuit / tunnel counts                                               |
| circuits              | WAN circuit liveness, bandwidth utilization, packet loss, jitter, latency          |
| application_paths     | App-aware path selection — chosen path, loss / latency per app                     |
| security_zones        | Zone-level session and connection rates                                            |
| alarms                | Prisma SD-WAN alarms by severity                                                   |
| self-monitoring       | Extension query duration and error rate                                            |

### HPE Aruba EdgeConnect (Silver Peak) — drafted

Source API: Aruba Orchestrator REST API.
Reference: Cisco SD-WAN structure for fabric / tunnel split.

| Feature set           | What it would monitor                                                              |
|-----------------------|------------------------------------------------------------------------------------|
| default               | EdgeConnect appliance CPU, memory, interface state                                 |
| device_health         | Per-appliance health, reachability, BIO (Boost) license state                      |
| fabric_infra          | Orchestrator-wide counts of sites, appliances, overlays, tunnels                   |
| overlays              | Per-overlay tunnel state, throughput, packet loss, latency, jitter                 |
| tunnels               | Per-tunnel reachability, encryption status, IPsec SA stats                         |
| boost                 | WAN-optimization (Boost) acceleration, dedup ratio, savings                        |
| interfaces            | LAN / WAN interface octets, errors, discards                                       |
| alarms                | Orchestrator alarm counts by severity                                              |
| self-monitoring       | Extension query duration and error rate                                            |

### Versa Networks — drafted

Source API: Versa Director / Analytics REST API.

| Feature set           | What it would monitor                                                              |
|-----------------------|------------------------------------------------------------------------------------|
| default               | VOS appliance CPU, memory, interface status                                        |
| device_health         | Per-appliance reachability and operational state                                   |
| fabric_infra          | Tenants, sites, appliances and SD-WAN paths in the controller                      |
| paths                 | SLA-class path measurements — loss, latency, jitter, MOS                           |
| applications          | Application-aware steering hits per business policy                                |
| security_services     | Inline NGFW / IPS event counts (Versa SASE)                                        |
| alarms                | Director alarms by severity                                                        |
| self-monitoring       | Extension query duration and error rate                                            |

### VMware / Broadcom VeloCloud — drafted

Source API: VMware SD-WAN Orchestrator (VCO) REST API.

| Feature set           | What it would monitor                                                              |
|-----------------------|------------------------------------------------------------------------------------|
| default               | Edge appliance CPU, memory, interface status                                       |
| device_health         | Per-Edge reachability and Edge service state                                       |
| fabric_infra          | Enterprises, Edges, gateways and links counts                                      |
| links                 | Per-WAN-link quality — loss, latency, jitter, throughput                           |
| business_policies     | Business-policy hits and chosen transport per traffic class                        |
| qoe                   | Quality-of-Experience scores per Edge / link                                       |
| alarms                | VCO event counts by severity                                                       |
| self-monitoring       | Extension query duration and error rate                                            |

## Fallbacks for any unsupported SD-WAN device

- [snmp-generic](https://www.dynatrace.com/hub/detail/snmp-generic/) — IF-MIB / SNMPv2-MIB coverage for basic device + interface health.
- [snmp-autodiscovery](https://www.dynatrace.com/hub/detail/snmp-autodiscovery/) — inventory and reachability for unsupported SD-WAN appliances.
