### `list_bgp`

List the current BGP sessions.

Route: `/api/v0/bgp`

Input:

- hostname = Either the devices hostname or id.
- asn = The local ASN you would like to filter by
- remote_asn = Filter by remote peer ASN
- remote_address = Filter by remote peer address
- local_address = Filter by local address
- bgp_descr = Filter by BGP neighbor description
- bgp_state = Filter by BGP session state (like established,idle...)
- bgp_state = Filter by BGP admin state (start,stop,running...)
- bgp_family = Filter by BGP address Family (4,6)



Example:

```curl
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/bgp
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/bgp?hostname=host.example.com
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/bgp?asn=1234
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/bgp?remote_asn=1234
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/bgp?local_address=1.1.1.1&remote_address=2.2.2.2
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/bgp?bgp_descr=UPSTREAM
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/bgp?bgp_state=established
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/bgp?bgp_adminstate=start
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/bgp?bgp_family=6
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/bgp?bgp_state=idle&bgp_descr=CORE&bgp_family=4
```

Output:

```json
{
 "status": "ok",
 "message": "",
 "bgp_sessions": [
        {
            "bgpPeer_id": 1260,
            "device_id": 7,
            "vrf_id": null,
            "astext": "Acme Ltd",
            "bgpPeerIdentifier": "2001:0DB8:0000:24cb:0000:0000:0000:0001",
            "bgpPeerRemoteAs": 65432,
            "bgpPeerState": "established",
            "bgpPeerAdminStatus": "start",
            "bgpPeerLastErrorCode": 6,
            "bgpPeerLastErrorSubCode": 2,
            "bgpPeerLastErrorText": "administrative shutdown",
            "bgpPeerIface": 268,
            "bgpLocalAddr": "2001:0DB8:0000:24cb:0000:0000:0000:0002",
            "bgpPeerRemoteAddr": "0.0.0.0",
            "bgpPeerDescr": "Another one #CORE",
            "bgpPeerInUpdates": 283882969,
            "bgpPeerOutUpdates": 7008,
            "bgpPeerInTotalMessages": 283883031,
            "bgpPeerOutTotalMessages": 1386692,
            "bgpPeerFsmEstablishedTime": 1628487,
            "bgpPeerInUpdateElapsedTime": 0,
            "context_name": ""
        },
    ...
    ],
    "count": 100
}
```

### `get_bgp`

Retrieves a BGP session by ID

Route: `/api/v0/bgp/:id`

Input:

-

Example:

```curl
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/bgp/4
```

Output:

```json
{
    "status": "ok",
    "bgp_session": [
        {
            "bgpPeer_id": "4",
            "device_id": "2",
            "astext": "",
            "bgpPeerIdentifier": "1234:1b80:1:12::2",
            "bgpPeerRemoteAs": "54321",
            "bgpPeerState": "established",
            "bgpPeerAdminStatus": "running",
            "bgpLocalAddr": "1234:1b80:1:12::1",
            "bgpPeerRemoteAddr": "0.0.0.0",
            "bgpPeerInUpdates": "3",
            "bgpPeerOutUpdates": "1",
            "bgpPeerInTotalMessages": "0",
            "bgpPeerOutTotalMessages": "0",
            "bgpPeerFsmEstablishedTime": "0",
            "bgpPeerInUpdateElapsedTime": "0",
            "context_name": ""
        }
    ],
    "count": 1
}
```

### `edit_bgp_descr`

This is a POST type request
Set the BGP session description by ID

Route: `/api/v0/bgp/:id`

Input:

- id = The id of the BGP Peer Session.
- bgp_descr = The description for the bgpPeerDescr field on the BGP Session.

Example:

```curl
curl -v -H 'X-Auth-Token: YOURAPITOKENHERE' --data '{"bgp_descr": "Your description here"}' https://librenms.org/api/v0/bgp/4
```

Output:

```json
{
    "status": "ok",
    "message": "BGP description for peer X.X.X.X on device 1 updated to Your description here"
}
```

### `list_cbgp`

List the current BGP sessions counters.

Route: `/api/v0/routing/bgp/cbgp`

Input:

- hostname = Either the devices hostname or id

Example:

```curl
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/routing/bgp/cbgp
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/routing/bgp/cbgp?hostname=host.example.com
```

Output:

```json
{
    "status": "ok",
    "bgp_counters": [
        {
            "device_id": "9",
            "bgpPeerIdentifier": "192.168.99.31",
            "afi": "ipv4",
            "safi": "multicast",
            "AcceptedPrefixes": "2",
            "DeniedPrefixes": "0",
            "PrefixAdminLimit": "0",
            "PrefixThreshold": "0",
            "PrefixClearThreshold": "0",
            "AdvertisedPrefixes": "11487",
            "SuppressedPrefixes": "0",
            "WithdrawnPrefixes": "10918",
            "AcceptedPrefixes_delta": "-2",
            "AcceptedPrefixes_prev": "2",
            "DeniedPrefixes_delta": "0",
            "DeniedPrefixes_prev": "0",
            "AdvertisedPrefixes_delta": "-11487",
            "AdvertisedPrefixes_prev": "11487",
            "SuppressedPrefixes_delta": "0",
            "SuppressedPrefixes_prev": "0",
            "WithdrawnPrefixes_delta": "-10918",
            "WithdrawnPrefixes_prev": "10918",
            "context_name": ""
        },
        ...
    ],
    "count": 100
}
```

### `list_ip_addresses`

List all IPv4 and IPv6 or only version specific addresses.

Route: `/api/v0/resources/ip/addresses/:address_family`

Input:

- address_family: optional ipv4 or ipv6 for ip version specific list.

Example:

```curl
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/resources/ip/addresses
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/resources/ip/addresses/ipv4
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/resources/ip/addresses/ipv6
```

Output:

```json
{
    "status": "ok",
    "ip_addresses": [
        {
            "ipv4_address_id": "69",
            "ipv4_address": "127.0.0.1",
            "ipv4_prefixlen": "8",
            "ipv4_network_id": "55",
            "port_id": "135",
            "context_name": ""
        },
        ...
    ],
    "count": 55
}

```

### `get_network_ip_addresses`

Get all IPv4 and IPv6 addresses for particular network.

Route: `/api/v0/resources/ip/networks/:id/ip`

- id must be integer

Input:

-

Example:

```curl
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/resources/ip/networks/55/ip
```

Output:

```json
{
    "status": "ok",
    "addresses": [
        {
            "ipv4_address_id": "69",
            "ipv4_address": "127.0.0.1",
            "ipv4_prefixlen": "8",
            "ipv4_network_id": "55",
            "port_id": "135",
            "context_name": ""
        }
    ],
    "count": 1
}
```

### `list_ip_networks`

List all IPv4 and IPv6 or only version specific networks.

Route: `/api/v0/resources/ip/networks/:address_family`

Input:

- address_family: optional ipv4 or ipv6 for ip version specific list.

Example:

```curl
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/resources/ip/networks
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/resources/ip/networks/ipv4
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/resources/ip/networks/ipv6
```

Output:

```json
{
    "status": "ok",
    "ip_networks": [
        {
            "ipv4_network_id": "1",
            "ipv4_network": "127.0.0.0/8",
            "context_name": ""
        },
        ...
    ],
    "count": 100
}
```

### `list_ipsec`

List the current IPSec tunnels which are active.

Route: `/api/v0/routing/ipsec/data/:hostname`

- hostname can be either the device hostname or id

Input:

  -

Example:

```curl
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/routing/ipsec/data/localhost
```

Output:

```json
{
    "status": "ok",
    "message": "",
    "count": 0,
    "ipsec": [
        "tunnel_id": "1",
        "device_id": "1",
        "peer_port": "0",
        "peer_addr": "127.0.0.1",
        "local_addr": "127.0.0.2",
        "local_port": "0",
        "tunnel_name": "",
        "tunnel_status": "active"
    ]
}
```

> Please note, this will only show active VPN sessions not all configured.

### `list_ospf`

List the current OSPF neighbours.

Route: `/api/v0/ospf`

Input:

- hostname = Either the devices hostname or id.

Example:

```curl
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/ospf
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/ospf?hostname=host.example.com
```

Output:

```json
{
 "status": "ok",
 "ospf_neighbours": [
        {
            "device_id": "1",
            "port_id": "0",
            "ospf_nbr_id": "172.16.1.145.0",
            "ospfNbrIpAddr": "172.16.1.145",
            "ospfNbrAddressLessIndex": "0",
            "ospfNbrRtrId": "172.16.0.140",
            "ospfNbrOptions": "82",
            "ospfNbrPriority": "1",
            "ospfNbrState": "full",
            "ospfNbrEvents": "5",
            "ospfNbrLsRetransQLen": "0",
            "ospfNbmaNbrStatus": "active",
            "ospfNbmaNbrPermanence": "dynamic",
            "ospfNbrHelloSuppressed": "false",
            "context_name": ""
        }
    ],
    "count": 1
}
```

### `list_ospf_ports`

List the current OSPF ports.

Route: `/api/v0/ospf_ports`

Example:

```curl
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/ospf_ports
```

Output:

```json
{
 "status": "ok",
 "ospf_ports": [
        {
          "id": 189086,
          "device_id": 43,
          "port_id": 2838,
          "ospf_port_id": "10.10.2.86.0",
          "ospfIfIpAddress": "10.10.2.86",
          "ospfAddressLessIf": 0,
          "ospfIfAreaId": "0.0.0.0",
          "ospfIfType": "pointToPoint",
          "ospfIfAdminStat": "enabled",
          "ospfIfRtrPriority": 128,
          "ospfIfTransitDelay": 1,
          "ospfIfRetransInterval": 5,
          "ospfIfHelloInterval": 10,
          "ospfIfRtrDeadInterval": 40,
          "ospfIfPollInterval": 90,
          "ospfIfState": "pointToPoint",
          "ospfIfDesignatedRouter": "0.0.0.0",
          "ospfIfBackupDesignatedRouter": "0.0.0.0",
          "ospfIfEvents": 33,
          "ospfIfAuthKey": "",
          "ospfIfStatus": "active",
          "ospfIfMulticastForwarding": "unicast",
          "ospfIfDemand": "false",
          "ospfIfAuthType": "0",
          "ospfIfMetricIpAddress": "10.10.2.86",
          "ospfIfMetricAddressLessIf": 0,
          "ospfIfMetricTOS": 0,
          "ospfIfMetricValue": 10,
          "ospfIfMetricStatus": "active",
          "context_name": null
        }
    ],
    "count": 1
}
```
### `list_ospfv3`

List the current OSPFv3 neighbours.

Route: `/api/v0/ospfv3`

Input:

- hostname = Either the devices hostname or id.

Example:

```curl
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/ospfv3
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/ospfv3?hostname=host.example.com
```

Output:

```json
{
    "status": "ok",
    "ospfv3_neighbours": [
        {
            "id": 7,
            "device_id": 14,
            "ospfv3_instance_id": 7,
            "port_id": 2345,
            "router_id": "10.0.43.11",
            "ospfv3NbrIfIndex": 2,
            "ospfv3NbrIfInstId": 0,
            "ospfv3NbrRtrId": 167797515,
            "ospfv3NbrAddressType": "ipv6",
            "ospfv3NbrAddress": "fe80::1d7:101:98cf:af80",
            "ospfv3NbrOptions": 19,
            "ospfv3NbrPriority": 50,
            "ospfv3NbrState": "full",
            "ospfv3NbrEvents": 6,
            "ospfv3NbrLsRetransQLen": 0,
            "ospfv3NbrHelloSuppressed": "false",
            "ospfv3NbrIfId": 14,
            "ospfv3NbrRestartHelperStatus": "notHelping",
            "ospfv3NbrRestartHelperAge": 0,
            "ospfv3NbrRestartHelperExitReason": "none",
            "context_name": ""
        }
    ],
    "count": 1
}
```

### `list_ospfv3_ports`

List the current OSPFv3 ports.

Route: `/api/v0/ospfv3_ports`

Example:

```curl
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/ospfv3_ports
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/ospfv3_ports?hostname=host.example.com
```

Output:

```json
{
    "status": "ok",
    "ospfv3_ports": [
        {
            "id": 13,
            "device_id": 14,
            "ospfv3_instance_id": 7,
            "ospfv3_area_id": 43,
            "port_id": 2390,
            "ospfv3IfIndex": 2,
            "ospfv3IfInstId": 0,
            "ospfv3IfAreaId": 0,
            "ospfv3IfType": "broadcast",
            "ospfv3IfAdminStatus": "enabled",
            "ospfv3IfRtrPriority": 1,
            "ospfv3IfTransitDelay": 1,
            "ospfv3IfRetransInterval": 5,
            "ospfv3IfHelloInterval": 10,
            "ospfv3IfRtrDeadInterval": 40,
            "ospfv3IfPollInterval": 10,
            "ospfv3IfState": "backupDesignatedRouter",
            "ospfv3IfDesignatedRouter": "10.0.43.11",
            "ospfv3IfBackupDesignatedRouter": "10.7.9.254",
            "ospfv3IfEvents": 7,
            "ospfv3IfDemand": "false",
            "ospfv3IfMetricValue": 10,
            "ospfv3IfLinkScopeLsaCount": 2,
            "ospfv3IfLinkLsaCksumSum": 64455,
            "ospfv3IfDemandNbrProbe": "false",
            "ospfv3IfDemandNbrProbeRetransLimit": 0,
            "ospfv3IfDemandNbrProbeInterval": 0,
            "ospfv3IfTEDisabled": "true",
            "ospfv3IfLinkLSASuppression": "false",
            "context_name": ""
        }
    ],
    "count": 1
}
```

### `list_vrf`

List the current VRFs.

Route: `/api/v0/routing/vrf`

Input:

- hostname = Either the devices hostname or id

**OR**

- vrfname = The VRF name you would like to filter by

Example:

```curl
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/routing/vrf
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/routing/vrf?hostname=host.example.com
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/routing/vrf?vrfname=Mgmt-vrf
```

Output:

```json
{
    "status": "ok",
    "vrfs": [
        {
            "vrf_id": "2",
            "vrf_oid": "8.77.103.109.116.45.118.114.102",
            "vrf_name": "Mgmt-vrf",
            "mplsVpnVrfRouteDistinguisher": "",
            "mplsVpnVrfDescription": "",
            "device_id": "8"
        },
        ...
    ],
    "count": 100
}
```

### `get_vrf`

Retrieves VRF by ID

Route: `/api/v0/routing/vrf/:id`

Input:

-

Example:

```curl
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/routing/vrf/2
```

Output:

```json
{
    "status": "ok",
    "vrf": [
        {
            "vrf_id": "2",
            "vrf_oid": "8.77.103.109.116.45.118.114.102",
            "vrf_name": "Mgmt-vrf",
            "mplsVpnVrfRouteDistinguisher": "",
            "mplsVpnVrfDescription": "",
            "device_id": "8"
        }
    ],
    "count": 1
}
```

### `list_mpls_services`

List MPLS services

Route: `/api/v0/routing/mpls/services`

Input:

- hostname = Either the devices hostname or id

Example:

```curl
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/routing/mpls/services
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/routing/mpls/services?hostname=host.example.com

```

Output:

```json
{
    "status": "ok",
    "mpls_services": [
        {
            "svc_id": 1671,
            "svc_oid": 27,
            "device_id": 4,
            "svcRowStatus": "active",
            "svcType": "tls",
            "svcCustId": 1,
            "svcAdminStatus": "up",
            "svcOperStatus": "up",
            "svcDescription": "",
            "svcMtu": 9008,
            "svcNumSaps": 1,
            "svcNumSdps": 0,
            "svcLastMgmtChange": 2,
            "svcLastStatusChange": 168,
            "svcVRouterId": 0,
            "svcTlsMacLearning": "enabled",
            "svcTlsStpAdminStatus": "disabled",
            "svcTlsStpOperStatus": "down",
            "svcTlsFdbTableSize": 250,
            "svcTlsFdbNumEntries": 0,
            "hostname": "host.example.com"
        }
    ],
    "count": 1
}
```

### `list_mpls_saps`

List MPLS SAPs

Route: `/api/v0/routing/mpls/saps`

Input:

- hostname = Either the devices hostname or id

Example:

```curl
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/routing/mpls/saps
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/routing/mpls/saps?hostname=host.example.com
```

Output:

```json
{
    "status": "ok",
    "saps": [
        {
            "sap_id": 1935,
            "svc_id": 1660,
            "svc_oid": 7,
            "sapPortId": 16108921125,
            "ifName": "1/1/c2/1",
            "device_id": 3,
            "sapEncapValue": "0",
            "sapRowStatus": "active",
            "sapType": "epipe",
            "sapDescription": "",
            "sapAdminStatus": "up",
            "sapOperStatus": "down",
            "sapLastMgmtChange": 2,
            "sapLastStatusChange": 0,
            "hostname": "hostname=host.example.com"
         }
    ],
    "count": 1
}
```
