# VI: All Major Network Device Brands Covered by a Dynatrace Extension

**Jira:** PRODUCT-17512
**Type:** Customer-facing
**State target:** Problem Stated → Use Case Defined

---

## Short Abstract / Blogline

Dynatrace delivers out-of-the-box monitoring extensions for every major enterprise network device category — firewalls, routers, switches, load balancers, VPN/ZTNA gateways, SD-WAN platforms, wireless LAN controllers, and access points — so network and IT operations teams can observe their entire infrastructure from a single platform, no gaps, no extra tooling.

The scope of the extension includes basis observability: control plane, Interface, network neighbor so all fields are populated in the I&O and/or Network App.

---

## Customer Zero

EDE: a number of devices deployed by the Dynatrace for its internal network have no matching extension in Dynatrace.

A large enterprise with a mixed-vendor network running Dynatrace for application observability and wanting to extend that coverage to the underlying network layer. Example profile: Palo Alto firewalls, Cisco + Juniper routers/switches, F5 load balancers, Cisco SD-WAN, and a mix of HPE Aruba + Meraki wireless.



---

## Target Audience

- **Network engineers / NetOps** responsible for enterprise WAN, campus, and data-centre infrastructure
- **NOC / IT Operations teams** using Dynatrace for unified observability and Davis AI root-cause analysis
- **Enterprise architects** evaluating Dynatrace as a single-pane-of-glass replacement for NMS tools (SolarWinds, PRTG, Auvik)

---

## WHY

Enterprise networks are inherently multi-vendor. A typical large enterprise today runs:

| Category | Common vendors |
|---|---|
| Firewalls | Palo Alto, Check Point, Fortinet FortiGate, Forcepoint |
| Routers / Switches | Cisco (IOS-XE, NX-OS), Juniper (EX/QFX/MX), HPE/H3C |
| Load Balancers / ADC | F5 BIG-IP, Citrix NetScaler |
| SD-WAN | Cisco Viptela, Meraki MX, Fortinet, Palo Alto Prisma, HPE Aruba EdgeConnect, Versa, VMware VeloCloud |
| Remote Access VPN / ZTNA | Cisco AnyConnect/ASA, Palo Alto GlobalProtect, Ivanti Connect Secure, Zscaler ZPA, Netskope NPA |
| Wireless LAN Controllers | Cisco Catalyst Center, Meraki, HPE Aruba, Juniper Mist, Extreme, CommScope RUCKUS |
| Wireless Access Points | Meraki, Cisco Catalyst, HPE Aruba, Juniper Mist, Extreme, Fortinet FortiAP, RUCKUS, Cambium |

Dynatrace already provides strong coverage for some brands (Palo Alto, Cisco SNMP, Fortinet FortiGate, F5 BIG-IP, Meraki, Cisco SD-WAN), but **significant gaps remain**:

1. **VPN / ZTNA**: No Hub extension for Cisco AnyConnect/ASA, Ivanti Connect Secure, Zscaler Private Access, or Netskope Private Access.
2. **SD-WAN**: No Hub extension for Fortinet Secure SD-WAN, Palo Alto Prisma SD-WAN, HPE Aruba EdgeConnect, Versa Networks, or VMware/Broadcom VeloCloud.
3. **Wireless LAN Controllers**: No Hub extension for HPE Aruba, Juniper Mist, Extreme Networks ExtremeCloud IQ, or CommScope RUCKUS SmartZone.
4. **Wireless Access Points**: No Hub extension for HPE Aruba, Juniper Mist, Extreme, Fortinet FortiAP, RUCKUS, or Cambium APs.
5. **Fortinet FortiGate as router**: The existing extension covers firewall/VPN feature sets but is missing Advanced Interfaces, Control Plane, HA, routing protocols (OSPF/BGP), and SD-WAN member visibility.

These gaps force customers to run specialised NMS or NPM tools alongside Dynatrace, splitting observability across platforms and blocking Davis AI from correlating network degradation with application-layer impact.

---

## Functional Requirements / Solution Journey

All new extensions follow the established Dynatrace Extension Framework v2 (EF2) taxonomy. Vendor-specific feature sets are documented in the `docs/devices/` subdirectories of this repository.

### VPN / ZTNA — 4 new extensions

- Cisco AnyConnect / ASA (SNMP)
- Ivanti Connect Secure (REST + SNMP)
- Zscaler Private Access (REST)
- Netskope Private Access (REST)

### SD-WAN — 5 new extensions

- Fortinet Secure SD-WAN (FortiGate REST + FortiManager)
- Palo Alto Prisma SD-WAN (CloudGenix API)
- HPE Aruba EdgeConnect (Orchestrator API)
- Versa Networks (Director API)
- VMware / Broadcom VeloCloud (VCO API)

### Wireless LAN Controllers — 4 new extensions

- HPE Aruba Mobility Conductor / Central
- Juniper Mist (cloud API)
- Extreme Networks ExtremeCloud IQ
- CommScope RUCKUS SmartZone / RUCKUS One

### Wireless Access Points — 6 new extensions

- HPE Aruba APs (Aruba Central)
- Juniper Mist APs
- Extreme Networks APs
- Fortinet FortiAP (FortiGate / FortiManager API)
- CommScope RUCKUS APs
- Cambium Networks APs (cnMaestro)



## Non-Functional Requirements

- All extensions published to Dynatrace Hub with documentation.
- Collection methods:  SNMP, REST API

---

## Enablement Requirements

- Dynatrace Hub listing for each new extension with feature-set documentation.
- Solution brief: "Network Observability with Dynatrace" updated to include new coverage.
- Sales / SE enablement: demo environment with at least one device per category.

-

## E2E Acceptance Criteria

- [ ] Every tier-1 network device category has ≥ 1 Hub extension per major vendor — no blank cells in the consensus-core matrix.
- [ ] Each extension activatable from the Hub without custom code; credentials and endpoint are the only required inputs.
- [ ] **Cisco AnyConnect / ASA**: active/peak RA sessions, license usage (Plus/Apex/VPN-Only), IPsec SA counts visible in Dynatrace.
- [ ] **Ivanti Connect Secure**: concurrent users, session counts by type, license ceiling, HA cluster state visible.
- [ ] **ZPA / Netskope**: app-connector health, active user sessions, private-app policy hits visible per tenant.
- [ ] **Fortinet FortiGate (router)**: HA cluster state, OSPF neighbor adjacency, BGP peer state, SD-WAN member SLA (loss/latency/jitter) visible.
- [ ] **Palo Alto Prisma SD-WAN**: per-ION device health, circuit quality metrics (loss/latency/jitter), fabric-wide site/tunnel counts visible.
- [ ] **HPE Aruba WLC + APs**: per-radio channel utilization and noise floor, per-AP client count and SNR visible.
- [ ] **Juniper Mist**: SLE scores (Wi-Fi assurance), per-site client counts, AP connected/disconnected state visible.
- [ ] **Fortinet FortiAP**: rogue AP detection counts, WIDS/WIPS event counts, per-band channel utilization visible.
- [ ] **RUCKUS SmartZone**: cluster node state, per-zone AP/client counts, airtime fairness metric visible.

---

## Customer Zero Planning

| Phase | Activity | Target |
|---|---|---|
| Alpha | Internal Dynatrace  lab — test against lab devices or SNMP test file per category | Weeks 1–4 per extension |
| Beta | 1 Design Partner customer per new extension category | 2 weeks after alpha pass |
| GA | Hub publication | Following beta sign-off |

Design Partner recruitment: leverage existing network monitoring customers who have flagged coverage gaps via support tickets or feature requests.

---

## E2E Demo (for acceptance)

1. **Network  dashboard**: One dashboard per network device type.
2. **Playground and Demo live**: A few device per category with no blank celles (firewall, router, switch, LB, VPN gateway, SD-WAN, WLC, AP).
---

## Out of Scope

- All feature set out of : Control plane, interface.
- All relationship out of "interface CALLS interface"

---

## Success Metrics

| Metric | Target |
|---|---|
| Tier-1 vendor coverage per category | 100% (no mandatory vendor unaddressed) |
| New Hub extensions published | ≥ 19 (4 VPN + 5 SD-WAN + 4 WLC + 6 AP + 1 FortiGate router update) |
| Extensions activated by customers within 6 months of GA | ≥ 10 per extension |
| "Network device not supported" support tickets | Reduction of ≥ 50% YoY after GA |

---

## Cost Analysis

To be amended by the engineering team:

| Work item | Estimate |
|---|---|
| New extension development (— avg x weeks each × 19 | ~x engineering weeks |
| Hub documentation and publishing | ~x weeks per extension (~x weeks) |
| Design Partner onboarding and beta testing | ~x weeks per category (8 categories) = ~x weeks no continuous |
| Sales / SE enablement brief | ~2 weeks |
| **Total estimate** | **~x engineering weeks** |

