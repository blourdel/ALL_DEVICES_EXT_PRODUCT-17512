# Firewall — Dynatrace feature sets

Feature sets currently available in the [Dynatrace Hub](https://www.dynatrace.com/hub/)
that apply to enterprise firewalls listed in [index.md](index.md).

## Palo Alto Firewalls

[hub/detail/palo-alto-firewalls-1](https://www.dynatrace.com/hub/detail/palo-alto-firewalls-1/) (SNMP)

| Feature set         | What it monitors                                                              |
|---------------------|-------------------------------------------------------------------------------|
| default             | Generic network device metrics — health and performance baseline              |
| interface           | Incoming / outgoing octets, packets, errors, discards per interface           |
| generic interfaces  | Standard IF-MIB byte and error / discard counters                             |
| advanced interfaces | Multicast / broadcast / unicast packets and interface status changes          |
| control-plane       | System uptime, management / system CPU, memory allocation                     |
| hardware            | Power consumption, fan speed, temperature sensors                             |
| host-system-usage   | User sessions, running processes, system load averages                        |
| virtual_system      | Active sessions, max session capacity, session utilization                    |
| zone                | Active TCP / UDP and Other-IP connection rates per security zone              |
| gateway             | GlobalProtect — active tunnels, sessions by type, gateway / proxy utilization |
| device-logging      | Incoming and write log rates on the firewall                                  |
| log-collector       | Log write rates, disk usage, log duration on Log Collector devices            |
| pan-sys             | System release date and component version info                                |

## Palo Alto Panorama

[hub/detail/palo-alto-panorama](https://www.dynatrace.com/hub/detail/palo-alto-panorama/) — central management.

| Feature set        | What it monitors                                                       |
|--------------------|------------------------------------------------------------------------|
| Default            | Memory, interface statistics, uptime                                   |
| System             | Uptime, active user sessions, process counts, hardware sensors         |
| CPU                | User / system / I-O-wait / dataplane CPU                               |
| Memory             | Free / used / reclaimable / total, utilization %                       |
| Swap               | Swap allocation, available space, usage %                              |
| Disk               | Capacity, available space, consumption, usage %                        |
| Basic Interface    | Interface errors, discards, in / out octets                            |
| Advanced Interface | Unicast / multicast / broadcast packets                                |
| Sessions           | Active and max sessions by protocol; SSL-proxy and tunnel utilization  |
| VSYS               | Virtual-system session limits, active sessions, utilization %          |
| Packet Drops       | Drops due to ARP failures, routing issues, policy denials, QoS timeouts|

## Check Point Firewall

[hub/detail/check-point-firewall](https://www.dynatrace.com/hub/detail/check-point-firewall/) (SNMP)

| Feature set         | What it monitors                                                          |
|---------------------|---------------------------------------------------------------------------|
| Default             | Uptime, CPU, memory, interface state (5 metrics)                          |
| Check Point Device  | Disk usage, connected users, accepted / rejected packets, connections, memory, CPU (17 metrics) |
| Interfaces          | Bytes in, packets, errors, bandwidth (9 metrics)                          |
| Generic Interfaces  | Interface byte and packet counters plus last-change timestamps            |
| Advanced Interfaces | Packet error, discard, multicast / broadcast / unicast (10 metrics)       |
| Stack Info          | Physical component state of the device stack                              |
| Entity Attributes   | Low-frequency entity attributes for consistent device naming              |

## Fortinet FortiGate

[hub/detail/fortinet-fortigate-1](https://www.dynatrace.com/hub/detail/fortinet-fortigate-1/) — uses the FortiGate HTTP API (not SNMP).

| Feature set    | What it monitors                                                          |
|----------------|---------------------------------------------------------------------------|
| default        | CPU, memory, interface bandwidth, errors, status (8 metrics)              |
| Overview       | CPU, memory, disk, sessions, connectivity (6 metrics)                     |
| Interfaces     | Traffic, errors, link speed, op-status (10 metrics)                       |
| IPSec Tunnels  | VPN tunnel traffic and proxy status (5 metrics)                           |
| Ping           | Reachability — packet counts, loss rate, RTT (5 metrics)                  |

## Forcepoint (SNMP)

[hub/detail/forcepoint-snmp](https://www.dynatrace.com/hub/detail/forcepoint-snmp/)

| Feature set              | What it monitors                                                  |
|--------------------------|-------------------------------------------------------------------|
| Default                  | Uptime, CPU, memory, interface status                             |
| Interfaces               | In / out bytes and interface state changes                        |
| Network Interfaces       | Interface speed, octets, errors, discards                         |
| Advanced Interfaces      | Multicast / broadcast packets and advanced error metrics          |
| CPU                      | Total, user, system, I/O-wait CPU %                               |
| Memory                   | Total / used / unused physical memory, buffers, cache             |
| Swap                     | Total, used, available swap                                       |
| Disks                    | Partition size, used, available                                   |
| Node                     | Clustering state, CPU load, connections, packet handling          |
| Extra Packet Statistics  | Accepted / dropped / logged / rejected packets and bytes          |

## Related

- [vpn/featuresets.md](../vpn/featuresets.md) — VPN-related feature sets exposed by these same firewalls (Palo Alto `gateway`, FortiGate `IPSec Tunnels`, Check Point).
