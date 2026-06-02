# All Network Device Extensions

This is the repo to define PRODUCT-17512.
It defines the network extension  needed to put off the "network device support" topic on network observability deals.
It consists in supporting the following capabilities:
- All current interfaces feature sets: default, interfaces and advanced interfaces.
- Control planes: CPU and Memory
- Interface Network neighbors


This folder (/docs) serves as a knowledge base for this application.

See VI for the product rationale, competitive context, and success metrics behind this VI. Jira: (https://dt-rnd.atlassian.net/browse/PRODUCT-17512)



## Overview

This section contains detailed information about with network devices will be supported by Dynatrace in an effort to support the major network devices vendors with a dedicated extension.

## inclusion criteria
Network devices used by large and small customers

### Device functions
Routers
SWitches
Firewall
Load Balancers
VPN
SD-WAN
Wireless LAN controller
Wireless Access Point


### Vendors

### First priority
Gartner leader quadrant
Recent product lines

## exclusion criteria
Network devices dedicatet to internet service providers.

## Metrics list
bytes_in.count

bytes_out.count

errors_in.count

errors_out.count

discards_in.count

discards _out.count

com.dynatrace.extension.network_device.if.in.multicast_pkts.count

com.dynatrace.extension.network_device.if.out.multicast_pkts.count

com.dynatrace.extension.network_device.if.in.broadcast_pkts.count

com.dynatrace.extension.network_device.if.out.broadcast_pkts.count

com.dynatrace.extension.network_device.if.in.ucast_pkts.count

com.dynatrace.extension.network_device.if.out.ucast_pkts.count

com.dynatrace.extension.network_device.if.lastchange

com.dynatrace.extension.network_device.if.in.crc_errors

## Properties list
All listed in the semantic dictionnary

## Relation list
EXT_NETWORK_INTERFACE CALLS EXT_NETWORK_INTERFACE
