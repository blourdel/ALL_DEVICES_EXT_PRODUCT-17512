# VI: Network extensions: SNMP completness

**Jira:** PRODUCT-17512
**Type:** Customer-facing
**State target:** Problem Stated → Use Case Defined


## Short Abstract / Blogline

Dynatrace delivers out-of-the-box monitoring extensions for every major enterprise network device category — firewalls, routers, switches, load balancers, SD-WAN gateway, wireless LAN controllers, and access points — so network and IT operations teams can observe their entire infrastructure, including the network, from a single observability platform..

The scope of the extension includes essential observability: control plane, Interface, network neighbor. It is only focus on devices monitored by SNMP. 

It has the (desired) side effect to provided Demo Live and Playground environments with the I&O and/or Network App device list and details with all fields  populated.


## Customer Zero

- EDE: a number of devices deployed by the Dynatrace for its internal network have no matching extension in Dynatrace (Nexus, Lantronic,etc.)

- Customers with mixed-vendor network running Dynatrace for application observability and wanting to extend that coverage to the underlying network layer.
Potential list from previous engagement: Renault, Kaiser, Rolex.


## Target Audience

- **Network engineers** responsible for enterprise WAN, campus, and data-centre infrastructure
- **IT Operations teams** using Dynatrace for unified observability
- **Enterprise architects** evaluating Dynatrace as a single-pane-of-glass replacement for NMS tools (SolarWinds, PRTG, LogicMonitor)

## WHY

Dynatrace already provides strong coverage for some brands (Palo Alto, Cisco SNMP, Fortinet FortiGate, F5 BIG-IP, Meraki, Cisco SD-WAN), but **significant gaps remain**:


### User pain

As our network device support is not complete, Dynatrace force customers to run specialised NMS or NPM tools alongside Dynatrace, splitting observability across platforms
 and blocking Davis AI from correlating network degradation with application-layer impact.

### Customer pain

This is the generic pain incured when you are forced to have multiple vendors (specialized tools and Dynatrace) for the same unifying function : observability.
You get less value for you money as you dont own a E2E observability solution.

### Dynatrace pain

Without a network device extension coverage of the market leader, customers are not migrating their network to be observed by Dynatrace. Instead of deploying 1000s of devices, they test the waters with a few 10s.
This prevent us to grow the network business by an order of magnitude.

## Customer Journey

### Today (without this VI)

My network has vendors that are not fully supported by Dynatrace extension.
 I resolve to install the SNMP generic extension. Sadly, it does not expose control plane data.
As the lack of control plane data is unbearable, I find resource to create an unsupported custom extension.

### Tomorrow (with this VI)

I have all my netwok vendors covered by a Dynatrace extension. I can compare control plane data between all the device I have in my network.

## Competitive Landscape

Coverage comparison per device category against DataDog (SNMP profiles from `integrations-core/default_profiles`, 234 profiles total as of June 2026).

Legend: ✅ dedicated extension/profile — ⚠️ partial or generic coverage — ❌ no coverage

---

### Routers

| Vendor / Product | DataDog | Dynatrace today | Dynatrace after VI |
| --- | --- | --- | --- |
| Cisco ASR | ✅ cisco-asr | ⚠️ Cisco Generic SNMP | ✅ |
| Cisco ISR / Legacy | ✅ cisco-isr, cisco_isr_4431 | ⚠️ Cisco Generic SNMP | ✅ |
| Huawei NetEngine AR | ✅ huawei-routers | ❌ | ✅ |
| Generic SNMP router | ✅ generic-router | ❌ | ✅ |

---

### Switches

| Vendor / Product | DataDog | Dynatrace today | Dynatrace after VI |
| --- | --- | --- | --- |
| HPE Aruba AOS | ✅ aruba-switch | ❌ | ✅ |
| HPE Aruba AOS-CX | ✅ aruba-cx-switch | ❌ | ✅ |
| Arista EOS | ✅ arista-switch | ❌ | ✅ |
| Juniper EX | ✅ juniper-ex | ❌ | ✅ |
| NVIDIA Mellanox | ✅ nvidia-mellanox-switchx | ❌ | ✅ |
| Extreme Networks | ✅ extreme-switching | ❌ | ✅ |
| HPE FlexFabric / Comware | ✅ hp-h3c-switch | ⚠️ HPE H3C Switch (hub) | ✅ (dedicated Comware extension) |
| Huawei Switches | ✅ huawei-switches | ❌ |  ✅  |

---

### Load Balancers

| Vendor / Product | DataDog | Dynatrace today | Dynatrace after VI |
| --- | --- | --- | --- |
| F5 BIG-IP | ✅ f5-big-ip | ✅ F5 BIG-IP (hub) | — (already covered) |
| A10 Thunder | ✅ a10-thunder | ❌ | ✅ |
| VMware AVI (NSX ALB) | ❌ | ❌ | ✅ |
| Radware Alteon | ❌ | ✅ Radware Alteon (hub) | — (already covered) |
| Citrix NetScaler | ✅ citrix-netscaler | ❌ | ❌ (not in VI scope) |

---

### Firewalls

| Vendor / Product | DataDog | Dynatrace today | Dynatrace after VI |
| --- | --- | --- | --- |
| Palo Alto Networks | ✅ palo-alto | ✅ (hub) | — (already covered) |
| Fortinet FortiGate | ✅ fortinet-fortigate | ✅ (hub) | — (already covered) |
| Cisco Firepower / ASA | ✅ cisco-asa, cisco-firepower | ✅ Cisco Firepower (hub) | — (already covered) |
| Check Point Quantum Force | ✅ checkpoint-firewall | ⚠️ Check Point generic (hub) | ✅ (dedicated model) |
| Check Point Quantum Spark | ✅ checkpoint-firewall | ⚠️ Check Point generic (hub) | ✅ (dedicated model) |
| Juniper SRX | ✅ juniper-srx | ❌ | ✅ |
| Fortinet FortiProxy | ❌ | ❌ | ✅ |

---

### SD-WAN

| Vendor / Product | DataDog | Dynatrace today | Dynatrace after VI |
| --- | --- | --- | --- |
| Cisco SD-WAN (Viptela) | ❌ | ✅ (hub) | — (already covered) |
| Cisco Meraki | ✅ meraki | ✅ (hub) | — (already covered) |
| VMware / Broadcom VeloCloud | ✅ velocloud-edge | ❌ | ✅ |
| Versa Networks | ❌ | ❌ | ✅ |
| HPE Aruba EdgeConnect (SilverPeak) | ✅ silverpeak-edgeconnect | ❌ | ✅ |

---

### Wireless LAN Controllers

| Vendor / Product | DataDog | Dynatrace today | Dynatrace after VI |
| --- | --- | --- | --- |
| Cisco 9800 Series | ✅ cisco-catalyst-wlc | ❌ | ✅ |
| HP Aruba Mobility Controller | ✅ aruba-mobility-controller | ❌ | ✅ |
| Ruckus (SmartZone) | ✅ ruckus, ruckus-unleashed | ❌ | ✅ |
| Fortinet WLAN Controller | ❌ | ❌ | ✅ |
| Extreme Networks WLC | ❌ | ❌ | ✅ |
| Cisco Legacy WLC | ✅ cisco-legacy-wlc | ❌ | ✅  |

---

### Wireless Access Points

| Vendor / Product | DataDog | Dynatrace today | Dynatrace after VI |
| --- | --- | --- | --- |
| HPE Aruba AP | ✅ aruba-access-point | ❌ | ✅ |
| CommScope Ruckus AP | ✅ ruckus-wap | ❌ | ✅ |
| Fortinet FortiAP | ❌ | ❌ | ✅ |
| Extreme Networks AP | ❌ | ❌ | ✅ |
| Cisco AP | ✅ cisco-access-point | ❌ | ✅  |
| Ubiquiti UniFi AP | ✅ ubiquiti-unifi | ❌ |  ✅  |

---

## Functional Requirements / Solution Journey

For each categories mentioned below, the market is fragmented. Even by capping the market share to 5%, that entails to support 5 to 6 vendors per category.

- Firewalls/VPN
- Routers
- Switches
- Load Balancers
- SD-WAN  
- Remote Access VPN / ZTNA
- Wireless LAN Controllers
- Wireless Access Points

The criteria to plan execution are: 
1. Immediate business: Large customer requests
2. Data-driven business: Application relevant (Load balancer, FW, etc.)
3. Data-driven business, MVP: Device Market Share

### New Router Extensions

- Cisco ASR
- Cisco Legacy
- Cisco Nexus
- Huawei Net Engine AR
- SNMP generic

### New Switch Extensions

- HPE Aruba AOS
- HPE Aruba AOS-CX
- Arista switches EOS/AOS
- Juniper Networks EX
- NVIDIA Mellanox
- Extreme networks
- Huawei
- HPE Flex Fabric (Comware)

### New Load Balancer Extensions

- VMware AVI
- A10

### New Firewall/VPN Extensions

- Juniper Networks SRX
- FortiProxy
- Checkpoint Quantum Force
- Checkpoint Quantum Spark

### New SD-WAN Extensions

- Versa Networks 
- VMware / Broadcom VeloCloud
- HPE Silver Peak

### New Wireless LAN Controller Extensions

- Cisco 9800 series
- Extreme Networks
- Ruckus
- Fortinet
- HP Aruba
- Ubiquiti

### New Wireless Access Point Extensions

- HPE Aruba 
- Cisco
- Extreme Networks
- Fortinet FortiAP
- CommScope Ruckus
- Ubiquity

All new extensions uses generic entities, properties and relations to be able to appear in the I&O and/or Network App.


## Non-Functional Requirements

- All extensions published to Dynatrace Hub with documentation.
- Collection methods:  SNMP, REST API


## Enablement Requirements

- Dynatrace Hub listing for each new extension with feature-set documentation.
- Solution brief: "Network Observability with Dynatrace" updated to include new coverage.
- Sales / SE enablement: demo environment with at least one device per category.


## E2E Acceptance Criteria

- [ ] All device types mention above are monitored with an extension that fill all fields reports in the I&O and/or Network Apps.

Note: some device may not expose  all items defined in the generic network models through SNMP. For these, blank fields are accepted.
It will be mitigated by the ongoing effort to smoothen the user experience when this happen.

## Customer Zero Planning

Exact timing to be refined by the engineering team.

| Phase | Activity | Target |
| --- | --- | --- |
| Alpha | Internal Dynatrace  lab — test against lab devices or SNMP test file per device category | x weeks |
| Beta | 1 Design Partner customer per new extension category | x weeks |
| GA | Hub publication | Following beta sign-off |

Design Partner (Customer) recruitment: leverage existing network monitoring customers who have flagged coverage gaps via support tickets or feature requests.


## E2E Demo (for acceptance)

 **One environment**: A device defined above with no blank fields.


## Out of Scope

- All feature set out of : Control plane, interface
- All relationship out of "interface CALLS interface"


## Success Metrics

| Metric | Target |
|---|---|
| Tier-1 vendor coverage per category | 100% (no  vendor with a market share egal or above 5* unaddressed) |
| New Hub extensions published | 19  |
| Extensions activated by customers within 3 months of GA | ≥ 10 per extension |
| "Network device not supported" support tickets | Reduction of ≥ xx% YoY after GA |


## Cost Analysis

To be amended by the engineering team:

| Work item | Estimate |
|---|---|
| New extension development (— avg x weeks each × 19 | ~x engineering weeks |
| Hub documentation and publishing | ~x weeks per extension (~x weeks) |
| Design Partner onboarding and beta testing | ~x weeks per category (8 categories) = ~x weeks no continuous |
| Sales / SE enablement brief | ~2 weeks |
| **Total estimate** | **~x engineering weeks** |

