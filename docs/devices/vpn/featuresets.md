# VPN — Dynatrace feature sets

There is no standalone "VPN" extension in the [Dynatrace Hub](https://www.dynatrace.com/hub/);
VPN visibility is delivered through dedicated feature sets inside the
firewall / SD-WAN / ADC extensions listed in [index.md](index.md), plus
drafted proposals for vendors not yet covered.

## Existing Hub extensions

### Fortinet FortiGate

[hub/detail/fortinet-fortigate-1](https://www.dynatrace.com/hub/detail/fortinet-fortigate-1/)

| Feature set    | What it monitors                                                                          |
|----------------|-------------------------------------------------------------------------------------------|
| IPSec Tunnels  | Site-to-site IPsec tunnel traffic, encryption / decryption, proxy state, tunnel up / down |

### Palo Alto Firewalls

[hub/detail/palo-alto-firewalls-1](https://www.dynatrace.com/hub/detail/palo-alto-firewalls-1/)

| Feature set    | What it monitors                                                                          |
|----------------|-------------------------------------------------------------------------------------------|
| gateway        | GlobalProtect — active tunnels, sessions by type, gateway / proxy utilization             |
| virtual_system | Active sessions, max session capacity, session utilization (sizing for remote access)     |
| zone           | Active TCP / UDP and Other-IP connection rates per security zone (incl. VPN zones)        |

### Check Point Firewall

[hub/detail/check-point-firewall](https://www.dynatrace.com/hub/detail/check-point-firewall/)

| Feature set         | What it monitors                                                                                  |
|---------------------|---------------------------------------------------------------------------------------------------|
| Check Point Device  | Connected users, accepted / rejected packets, connections — proxy for VPN client counts           |

### Meraki

[hub/detail/meraki](https://www.dynatrace.com/hub/detail/meraki/) — Meraki MX site-to-site VPN.

| Feature set | What it monitors                                                                          |
|-------------|-------------------------------------------------------------------------------------------|
| vpn         | VPN status, throughput, latency, jitter, loss %, MOS — per MX-to-MX VPN peer              |
| uplink      | MX uplink loss, latency, status, data transferred — pairs with `vpn` end-to-end           |

### F5 BIG-IP — Access Policy Manager (APM)

[hub/detail/f5-big-ip-ltm-1](https://www.dynatrace.com/hub/detail/f5-big-ip-ltm-1/) — F5 APM delivers SSL-VPN / remote-access.

| Feature set    | What it monitors                                              |
|----------------|---------------------------------------------------------------|
| apm-session    | Total and active APM sessions                                 |
| apm-profiles   | Total and active sessions per access profile                  |
| apm-licenses   | Current SSL-VPN connections and available licenses            |

### Cisco SD-WAN

[hub/detail/cisco-catalyst-sd-wan-manager-viptela](https://www.dynatrace.com/hub/detail/cisco-catalyst-sd-wan-manager-viptela) — encrypted overlay tunnels between SD-WAN sites; see [sd-wan/featuresets.md](../sd-wan/featuresets.md).

| Feature set         | What it monitors                                                       |
|---------------------|------------------------------------------------------------------------|
| approute_statistics | Tunnel-level QoS, loss, latency, jitter, throughput across TLOCs       |

## Drafted feature sets — vendors without a Hub extension

The vendors below have no dedicated VPN extension in the Hub. The
proposals re-use the structure of [Palo Alto Firewalls](https://www.dynatrace.com/hub/detail/palo-alto-firewalls-1/) (`gateway`,
`virtual_system`) and [F5 BIG-IP APM](https://www.dynatrace.com/hub/detail/f5-big-ip-ltm-1/) (`apm-session`,
`apm-licenses`).

### Cisco Secure Client / AnyConnect on ASA or Secure Firewall — drafted

Source: SNMP (CISCO-REMOTE-ACCESS-MONITOR-MIB, CISCO-IPSEC-FLOW-MONITOR-MIB) — alongside [Generic Cisco Device](https://www.dynatrace.com/hub/detail/generic-cisco-router-snmp-extension/).

| Feature set     | What it would monitor                                                            |
|-----------------|----------------------------------------------------------------------------------|
| default         | Reuse Cisco SNMP `Default` — uptime, CPU, memory, interface health               |
| ra_sessions     | Active / peak / cumulative remote-access sessions, by IPsec vs SSL               |
| ra_licenses     | AnyConnect Plus / Apex / VPN-Only license usage and ceiling                      |
| ipsec_tunnels   | Site-to-site IPsec tunnel state, IKE / IPsec SA counts, encrypted bytes          |
| ra_users        | Logged-in users, group-policy distribution, per-session bandwidth                |
| ssl_vpn         | SSL-VPN portal sessions, gateway CPU / memory                                    |

### Ivanti Connect Secure (Pulse Secure) — drafted

Source API: Pulse / Ivanti REST API + SNMP.
Reference: Palo Alto `gateway` and F5 `apm-session`.

| Feature set     | What it would monitor                                                            |
|-----------------|----------------------------------------------------------------------------------|
| default         | Appliance CPU, memory, interface status                                          |
| users           | Active / concurrent / peak users, by realm                                       |
| sessions        | Active sessions by type (Network Connect, ESAP), session duration distribution   |
| licenses        | License consumption vs ceiling                                                   |
| ipsec_tunnels   | ESP IPsec tunnel state for road-warrior clients                                  |
| auth            | Authentication success / failure counts by auth server                           |
| cluster         | HA cluster sync state and active node                                            |
| self-monitoring | Extension query duration and error rate                                          |

### Zscaler Private Access (ZPA) — drafted

Source API: Zscaler ZPA Admin REST API.
Reference: cloud-centric — modelled on Cisco SD-WAN (`fabric_infra`, `device_health`).

| Feature set          | What it would monitor                                                            |
|----------------------|----------------------------------------------------------------------------------|
| default              | Tenant-level health and reachability of the ZPA Public Service Edge              |
| app_connectors       | Connector health, version, uptime, public-cloud region                           |
| service_edges        | Private Service Edge load, throughput, active connections                        |
| user_sessions        | Active users, session count, average session duration                            |
| application_segments | Per-application policy hits, allow / block counts                                |
| policy               | Access policy evaluation counts and result distribution                          |
| alarms               | ZPA admin alarms by severity                                                     |
| self-monitoring      | Extension query duration and error rate                                          |

### Netskope Private Access (NPA) — drafted

Source API: Netskope REST API.
Same shape as ZPA above.

| Feature set     | What it would monitor                                                            |
|-----------------|----------------------------------------------------------------------------------|
| default         | Tenant health and reachability of the Netskope cloud                             |
| publishers      | Publisher (private-app connector) health, version, uptime                        |
| user_sessions   | Active users, session count, average session duration                            |
| private_apps    | Per-private-app policy hits, traffic volume                                      |
| policy          | Policy evaluations and result distribution                                       |
| alarms          | Netskope alerts by severity                                                      |
| self-monitoring | Extension query duration and error rate                                          |

## Fallbacks for any unsupported VPN device

- [snmp-generic](https://www.dynatrace.com/hub/detail/snmp-generic/) — IF-MIB / SNMPv2-MIB coverage for basic VPN-appliance health.
- Monitor via the underlying firewall / gateway hosting the VPN service when it already has a Hub extension (see [firewall/featuresets.md](../firewall/featuresets.md)).
