# Wireless Access Point — Dynatrace feature sets

Feature sets currently available in the [Dynatrace Hub](https://www.dynatrace.com/hub/)
that apply to enterprise APs listed in [index.md](index.md).

## Meraki (Cisco Meraki MR APs)

[hub/detail/meraki](https://www.dynatrace.com/hub/detail/meraki/) — cloud-managed, the primary source of AP-specific feature sets in the Hub.

| Feature set           | What it monitors                                                              |
|-----------------------|-------------------------------------------------------------------------------|
| wireless              | Radio channel utilization — total, Wi-Fi, and non-Wi-Fi bands                 |
| device-status         | Online / alerting / offline / dormant state per AP                            |
| device-control-plane  | AP uptime, CPU, memory                                                        |
| interface             | Inbound / outbound bytes                                                      |
| default               | System uptime, CPU, memory                                                    |
| self-monitoring       | API connectivity, monitored orgs / networks / devices                         |

## Cisco Catalyst Center (DNA Center)

[hub/detail/cisco-catalyst-center-dna-center](https://www.dynatrace.com/hub/detail/cisco-catalyst-center-dna-center/) — covers Catalyst APs registered to the controller.

| Feature set      | What it monitors                                                                |
|------------------|---------------------------------------------------------------------------------|
| device           | Per-AP health, CPU / memory, temperature, uptime                                |
| site             | Site-level wireless client health and pending issues                            |
| center           | Aggregate client / device health and counts across sites                        |
| interface        | AP interface operational status, throughput, errors                             |
| self-monitoring  | Extension performance — query durations, errors                                 |
| default          | Generic device metrics (CPU, memory, interface stats)                           |

## Generic Cisco Device (SNMP) — Catalyst 9100 / older AireOS-managed APs

[hub/detail/generic-cisco-router-snmp-extension](https://www.dynatrace.com/hub/detail/generic-cisco-router-snmp-extension/) — APs polled directly via SNMP (typically through their WLC).

Most relevant feature sets:

| Feature set            | What it monitors                                          |
|------------------------|-----------------------------------------------------------|
| Default                | Uptime, CPU, memory, interface health                     |
| Sensors                | Temperature                                               |
| Sensors (Advanced)     | Raw sensor values across measurement types                |
| Power Supply           | PoE / PSU operational status                              |
| Neighbor-Discovery     | LLDP / CDP topology data (upstream switch port)           |
| Health                 | SNMP transport diagnostics                                |

See [routers/featuresets.md](../routers/featuresets.md) for the full Cisco SNMP feature-set list.

## Drafted feature sets — vendors without a Hub extension

The vendors below have no dedicated AP extension in the Hub. The
proposals re-use the structure of the [Meraki](https://www.dynatrace.com/hub/detail/meraki/) extension
(`wireless`, `device-status`, `device-control-plane`) and [Cisco Catalyst Center](https://www.dynatrace.com/hub/detail/cisco-catalyst-center-dna-center/)
(`device`, `site`).

### HPE Aruba APs — drafted

Source API: Aruba Central REST API or AOS-10 controller API.

| Feature set     | What it would monitor                                                     |
|-----------------|---------------------------------------------------------------------------|
| default         | Per-AP uptime, CPU, memory                                                |
| device-status   | Online / offline / pending state per AP                                   |
| wireless        | Radio channel utilization, noise floor, busy %, per-band                  |
| client_health   | Connected client count, SNR, retry / drop rates                           |
| interface       | AP uplink op-state, throughput, errors                                    |
| poe             | PoE class negotiated, power drawn, PoE source                             |
| self-monitoring | Extension query duration and error rate                                   |

### Juniper Mist APs — drafted

Source API: Mist Cloud REST API.

| Feature set     | What it would monitor                                                     |
|-----------------|---------------------------------------------------------------------------|
| default         | Per-AP uptime, CPU, memory, temperature                                   |
| device-status   | Connected / disconnected state per AP                                     |
| wireless        | Radio channel utilization, noise, interference, coverage SLE              |
| client_health   | Connected clients, throughput SLE, time-to-connect                        |
| interface       | AP uplink op-state, throughput, errors                                    |
| poe             | PoE class negotiated, power drawn                                         |
| self-monitoring | Extension query duration and error rate                                   |

### Extreme Networks APs — drafted

Source API: ExtremeCloud IQ REST API.

| Feature set     | What it would monitor                                                     |
|-----------------|---------------------------------------------------------------------------|
| default         | Per-AP uptime, CPU, memory                                                |
| device-status   | Online / offline state per AP                                             |
| wireless        | Radio channel utilization, noise floor                                    |
| client_health   | Connected clients, SNR, retry rate                                        |
| interface       | AP uplink op-state, throughput, errors                                    |
| poe             | PoE class, power drawn                                                    |
| self-monitoring | Extension query duration and error rate                                   |

### Fortinet FortiAP — drafted

Source: FortiGate / FortiManager REST API — alongside [Fortinet FortiGate](https://www.dynatrace.com/hub/detail/fortinet-fortigate-1/).

| Feature set     | What it would monitor                                                     |
|-----------------|---------------------------------------------------------------------------|
| default         | Per-AP uptime, CPU, memory                                                |
| device-status   | Online / offline state per FortiAP                                        |
| wireless        | Radio channel utilization per band                                        |
| client_health   | Connected client count, signal strength, retry rate                       |
| security        | Rogue AP detections, WIDS / WIPS event counts (FortiAP)                   |
| interface       | AP LAN uplink op-state, throughput, errors                                |
| self-monitoring | Extension query duration and error rate                                   |

### CommScope RUCKUS APs — drafted

Source API: RUCKUS SmartZone REST API or RUCKUS One cloud API.

| Feature set     | What it would monitor                                                     |
|-----------------|---------------------------------------------------------------------------|
| default         | Per-AP uptime, CPU, memory                                                |
| device-status   | Online / offline state                                                    |
| wireless        | Radio channel utilization, airtime fairness, BeamFlex usage               |
| client_health   | Connected clients, SNR, dropped associations                              |
| interface       | AP uplink op-state, throughput, errors                                    |
| poe             | PoE class, power drawn                                                    |
| self-monitoring | Extension query duration and error rate                                   |

### Cambium Networks APs — drafted

Source API: cnMaestro REST API.

| Feature set     | What it would monitor                                                     |
|-----------------|---------------------------------------------------------------------------|
| default         | Per-AP uptime, CPU, memory                                                |
| device-status   | Online / offline state                                                    |
| wireless        | Radio channel utilization, noise                                          |
| client_health   | Connected clients, SNR                                                    |
| interface       | AP uplink op-state, throughput, errors                                    |
| self-monitoring | Extension query duration and error rate                                   |

## Fallbacks for any unsupported AP

- [snmp-generic](https://www.dynatrace.com/hub/detail/snmp-generic/) — generic SNMP coverage for any AP exposing IF-MIB.
- [snmp-autodiscovery](https://www.dynatrace.com/hub/detail/snmp-autodiscovery/) — inventory and reachability for unsupported APs.

## Related

- [wireless-lan-controller/featuresets.md](../wireless-lan-controller/featuresets.md) — controllers managing these APs.
