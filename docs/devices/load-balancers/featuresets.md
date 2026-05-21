# Load Balancers — Dynatrace feature sets

Feature sets currently available in the [Dynatrace Hub](https://www.dynatrace.com/hub/)
that apply to load balancers / ADCs listed in [index.md](index.md).

## F5 BIG-IP

[hub/detail/f5-big-ip-ltm-1](https://www.dynatrace.com/hub/detail/f5-big-ip-ltm-1/) — the most granular network-device extension in the Hub, with ~50 feature sets grouped below.

### System / chassis

| Feature set                | What it monitors                                                |
|----------------------------|-----------------------------------------------------------------|
| default                    | Uptime, interface status, CPU, memory                           |
| System                     | System uptime                                                   |
| f5-host-system-usage       | System users, processes, load averages                          |
| instance-cpu-basic         | CPU idle, I/O-wait, interrupt handling                          |
| instance-memory-basic      | Total and used host memory                                      |
| instance-memory-advanced   | Swap, shared, cached memory, buffers                            |
| instance-sync              | Failover and config synchronization status                      |
| chassis-components         | Fan state and speed, PSU state, temperature                     |
| physical-sensors           | Physical sensor measurements                                    |
| disk                       | Block size, total / free blocks per partition                   |
| device-entity-counts       | Total LTM nodes, pools, virtual servers                         |
| device-connection-stats    | Client / server bytes in-out, connection counts                 |
| device-packet-stats        | Dropped packets, packet errors, packet counts                   |
| f5-interface               | Interface status, bytes, packets, drops, errors                 |
| Interfaces                 | Generic IF-MIB byte and error counters                          |
| Advanced interfaces        | Multicast / broadcast / unicast packet counts                   |

### Virtual servers

| Feature set                          | What it monitors                                          |
|--------------------------------------|-----------------------------------------------------------|
| virtualserver-basic                  | Virtual server state                                      |
| virtualserver-advanced               | CPU usage, bytes, packets per virtual server              |
| virtualserver-connectivity-basic     | Connection limits, requests, connection counts            |
| virtualserver-connectivity-advanced  | Ephemeral / slow / evicted connections                    |
| virtualserver-syn-cookies            | Accepted and rejected SYN cookies                         |

### Pools / nodes

| Feature set         | What it monitors                                                      |
|---------------------|-----------------------------------------------------------------------|
| pool-basic          | Total members, active members, pool state                             |
| pool-advanced       | Bytes and packets for pool server-side traffic                        |
| pool-connectivity   | Pool requests, current / queued connections, sessions                 |
| node-basic          | Pool member monitor status and state                                  |
| node-advanced       | Bytes and packets received / transmitted by pool members              |
| node-connectivity   | Requests, current connections, queued connections                     |

### Profiles / rules

| Feature set                              | What it monitors                                              |
|------------------------------------------|---------------------------------------------------------------|
| profile-http                             | HTTP request types and response status code counts            |
| profile-clientssl                        | SSL connections, handshakes, protocol versions (client side)  |
| profile-serverssl                        | SSL connections, handshakes, protocol versions (server side)  |
| profile-serverssl-handshakes-basic       | Secure handshakes and handshake failures (server SSL)         |
| profile-serverssl-handshakes-advanced    | Insecure handshake acceptance / rejection                     |
| rule                                     | iRule execution failures, aborts, total executions            |

### Global Traffic Manager (DNS / GTM)

| Feature set                              | What it monitors                                                  |
|------------------------------------------|-------------------------------------------------------------------|
| gtm-pool-metrics                         | DNS LB methods, dropped messages, DNS resolution counts           |
| gtm-pool-state                           | DNS pool state metrics                                            |
| gtm-pool-member-state                    | F5 DNS (GTM) pool-member state                                    |
| gtm-virtual-server-metrics-lb            | LB method usage for DNS virtual servers                           |
| gtm-virtual-server-metrics-traffic       | Bits / packets / connections for DNS virtual servers              |
| gtm-virtual-server-metrics-resources     | CPU and available memory for DNS virtual servers                  |
| gtm-virtual-server-state                 | DNS virtual server state                                          |
| gtm-wide-ip-metrics                      | DNS resolution requests, LB, message handling                     |
| gtm-wide-ip-state                        | F5 DNS (GTM) Wide-IP metadata                                     |
| gtm-dns-profile-metrics                  | DNS queries, responses, cache requests, error codes               |
| gtm-dns-profile-state                    | DNS profile state and configuration                               |
| gtm-irule                                | Rule execution failures / aborts / executions for DNS rules       |
| gtm-dnssec                               | DNSSEC signature / RRSET failures, DNSKEY queries                 |

### APM (Access Policy Manager)

| Feature set    | What it monitors                                          |
|----------------|-----------------------------------------------------------|
| apm-session    | Total and active APM sessions                             |
| apm-profiles   | Total and active sessions per access profile              |
| apm-licenses   | Current SSL / VPN connections and available licenses      |

## Citrix NetScaler SDX

[hub/detail/citrix-netscaler-sdx](https://www.dynatrace.com/hub/detail/citrix-netscaler-sdx/) — 12 metrics across 6 feature sets, focused on the SDX hardware platform.

| Feature set         | What it monitors                                              |
|---------------------|---------------------------------------------------------------|
| hardware            | Hardware sensor readings and health indicators                |
| software            | Overall software component health status                      |
| storagerepository   | Physical size and utilization of the storage repository       |
| temp                | IPMI temperature sensor measurements and status               |
| voltage             | IPMI voltage sensor measurements and status                   |
| fanspeed            | Fan speed measurements and operational status                 |

## Related

- [vpn/featuresets.md](../vpn/featuresets.md) — F5 APM `apm-licenses` is the SSL-VPN view.
