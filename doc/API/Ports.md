### `get_all_ports`

Get info for all ports on all devices. Strongly recommend that you use
the `columns` parameter to avoid pulling too much data.

Route: `/api/v0/ports`

  -

Input:

- columns: Comma separated list of columns you want returned.

Example:

```curl
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/ports?columns=ifName%2Cport_id
```

Output:

```json
{
  "status": "ok",
  "message": "",
  "ports": [
        {
          "ifName": "Gi0/0/0",
          "port_id": "1"
        },
        {
          "ifName": "Gi0/0/1",
          "port_id": "2"
        },
        ...
        {
          "ifName": "Vlan 3615",
          "port_id": "5488"
        }
    ]
}
```

### `search_ports`

Search for ports matching the query.

Route: `/api/v0/ports/search/:search`

- search string to search in fields: ifAlias, ifDescr, and ifName

Input:

- columns: Comma separated list of columns you want returned.

Example:

```curl
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/ports/search/lo
```

Output:

```json
{
    "status": "ok",
    "ports": [
        {
            "device_id": 1,
            "port_id": 1,
            "ifIndex": 1,
            "ifName": "lo"
        },
        {
            "device_id": 2,
            "port_id": 3,
            "ifIndex": 1,
            "ifName": "lo"
        },
        {
            "device_id": 3,
            "port_id": 5,
            "ifIndex": 1,
            "ifName": "lo"
        }
    ]
}
```

### `search_ports in specific field(s)`

Specific search for ports matching the query.

Route: `/api/v0/ports/search/:field/:search`

- field: comma separated list of field(s) to search
- search: string to search in fields

Input:

- columns: Comma separated list of columns you want returned.

Example:

```curl
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/ports/search/ifName/lo
```

Output:

```json
{
    "status": "ok",
    "ports": [
        {
            "device_id": 1,
            "port_id": 1,
            "ifIndex": 1,
            "ifName": "lo"
        },
        {
            "device_id": 2,
            "port_id": 3,
            "ifIndex": 1,
            "ifName": "lo"
        },
        {
            "device_id": 3,
            "port_id": 5,
            "ifIndex": 1,
            "ifName": "lo"
        }
    ]
}
```


### `ports_with_associated_mac`

Search for ports matching the search mac.

Route: `/api/v0/ports/mac/:search?filter=first`

-  search a mac address in fdb and print the ports ordered by the mac count of the associated port.

Input:

  -

Example:

```curl
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/ports/mac/00:11:22:33:44:55
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/ports/mac/001122.334455?filter=first
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/ports/mac/001122334455?filter=first
```

Output:

```json
{
  "status": "ok",
  "message": "",
  "port": [
    {
      "port_id": "323",
      "device_id": "55",
      "port_descr_type": null,
      "port_descr_descr": null,
      "port_descr_circuit": null,
      "port_descr_speed": null,
      "port_descr_notes": null,
      "ifDescr": "GigabitEthernet0/0/0",
      "ifName": "Gi0/0/0",
      "portName": null,
      "ifIndex": "1",
      "ifSpeed": "1000000000",
      "ifConnectorPresent": "true",
      "ifPromiscuousMode": "false",
      "ifHighSpeed": "1000",
      "ifOperStatus": "up",
      "ifOperStatus_prev": null,
      "ifAdminStatus": "up",
      "ifAdminStatus_prev": null,
      "ifDuplex": "fullDuplex",
      "ifMtu": "1560",
      "ifType": "ethernetCsmacd",
      "ifAlias": "ASR Interconnect Trunk",
      "ifPhysAddress": "84bf20853e00",
      "ifHardType": null,
      "ifLastChange": "42407358",
      "ifVlan": "",
      "ifTrunk": "",
      "ifVrf": "0",
      "counter_in": null,
      "counter_out": null,
      "ignore": "0",
      "disabled": "0",
      "detailed": "0",
      "deleted": "0",
      "pagpOperationMode": null,
      "pagpPortState": null,
      "pagpPartnerDeviceId": null,
      "pagpPartnerLearnMethod": null,
      "pagpPartnerIfIndex": null,
      "pagpPartnerGroupIfIndex": null,
      "pagpPartnerDeviceName": null,
      "pagpEthcOperationMode": null,
      "pagpDeviceId": null,
      "pagpGroupIfIndex": null,
      "ifInUcastPkts": "128518576",
      "ifInUcastPkts_prev": "128517284",
      "ifInUcastPkts_delta": "1292",
      "ifInUcastPkts_rate": "4",
      "ifOutUcastPkts": "128510560",
      "ifOutUcastPkts_prev": "128509268",
      "ifOutUcastPkts_delta": "1292",
      "ifOutUcastPkts_rate": "4",
      "ifInErrors": "0",
      "ifInErrors_prev": "0",
      "ifInErrors_delta": "0",
      "ifInErrors_rate": "0",
      "ifOutErrors": "0",
      "ifOutErrors_prev": "0",
      "ifOutErrors_delta": "0",
      "ifOutErrors_rate": "0",
      "ifInOctets": "12827393730",
      "ifInOctets_prev": "12827276736",
      "ifInOctets_delta": "116994",
      "ifInOctets_rate": "387",
      "ifOutOctets": "14957481766",
      "ifOutOctets_prev": "14957301765",
      "ifOutOctets_delta": "180001",
      "ifOutOctets_rate": "596",
      "poll_time": "1483779150",
      "poll_prev": "1483778848",
      "poll_period": "302"
    }
  ]
}
```

### `get_port_info`

Get all info for a particular port.

Route: `/api/v0/ports/:portid?with=vlans`

- portid must be an integer
- it's possible to add allowed associated relations to the port using the `with` option. Allowed: `vlans`,`device`

Input:

  -

Example:

```curl
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/ports/323
```

Output:

```json
{
  "status": "ok",
  "message": "",
  "port": [
    {
      "port_id": "323",
      "device_id": "55",
      "port_descr_type": null,
      "port_descr_descr": null,
      "port_descr_circuit": null,
      "port_descr_speed": null,
      "port_descr_notes": null,
      "ifDescr": "GigabitEthernet0/0/0",
      "ifName": "Gi0/0/0",
      "portName": null,
      "ifIndex": "1",
      "ifSpeed": "1000000000",
      "ifConnectorPresent": "true",
      "ifPromiscuousMode": "false",
      "ifHighSpeed": "1000",
      "ifOperStatus": "up",
      "ifOperStatus_prev": null,
      "ifAdminStatus": "up",
      "ifAdminStatus_prev": null,
      "ifDuplex": "fullDuplex",
      "ifMtu": "1560",
      "ifType": "ethernetCsmacd",
      "ifAlias": "ASR Interconnect Trunk",
      "ifPhysAddress": "84bf20853e00",
      "ifHardType": null,
      "ifLastChange": "42407358",
      "ifVlan": "",
      "ifTrunk": "",
      "ifVrf": "0",
      "counter_in": null,
      "counter_out": null,
      "ignore": "0",
      "disabled": "0",
      "detailed": "0",
      "deleted": "0",
      "pagpOperationMode": null,
      "pagpPortState": null,
      "pagpPartnerDeviceId": null,
      "pagpPartnerLearnMethod": null,
      "pagpPartnerIfIndex": null,
      "pagpPartnerGroupIfIndex": null,
      "pagpPartnerDeviceName": null,
      "pagpEthcOperationMode": null,
      "pagpDeviceId": null,
      "pagpGroupIfIndex": null,
      "ifInUcastPkts": "128518576",
      "ifInUcastPkts_prev": "128517284",
      "ifInUcastPkts_delta": "1292",
      "ifInUcastPkts_rate": "4",
      "ifOutUcastPkts": "128510560",
      "ifOutUcastPkts_prev": "128509268",
      "ifOutUcastPkts_delta": "1292",
      "ifOutUcastPkts_rate": "4",
      "ifInErrors": "0",
      "ifInErrors_prev": "0",
      "ifInErrors_delta": "0",
      "ifInErrors_rate": "0",
      "ifOutErrors": "0",
      "ifOutErrors_prev": "0",
      "ifOutErrors_delta": "0",
      "ifOutErrors_rate": "0",
      "ifInOctets": "12827393730",
      "ifInOctets_prev": "12827276736",
      "ifInOctets_delta": "116994",
      "ifInOctets_rate": "387",
      "ifOutOctets": "14957481766",
      "ifOutOctets_prev": "14957301765",
      "ifOutOctets_delta": "180001",
      "ifOutOctets_rate": "596",
      "poll_time": "1483779150",
      "poll_prev": "1483778848",
      "poll_period": "302"
    }
  ]
}
```

### `get_port_ip_info`

Get all IP info (v4 and v6) for a given port id.

Route: `/api/v0/ports/:portid/ip`

- portid must be an integer

Input:

  -

Example:

```curl
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/ports/323/ip
```

Output:

```json
{
  "status": "ok",
  "message": "",
  "addresses": [
    {
      "ipv4_address_id": "290",
      "ipv4_address": "192.168.99.292",
      "ipv4_prefixlen": "30",
      "ipv4_network_id": "247",
      "port_id": "323",
      "context_name": ""
    }
  ]
}
```

### `get_port_transceiver`

Get transceiver info with metrics

Route: `/api/v0/ports/:portid/transceiver`

- portid must be an integer

Example:

```curl
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/ports/50736/transceiver
```

Output:

```json
{
    "status": "ok",
    "transceivers": [
        {
            "id": 13,
            "created_at": "2024-06-26T23:46:06.000000Z",
            "updated_at": "2024-06-27T00:00:07.000000Z",
            "device_id": 3138,
            "port_id": 50736,
            "index": "51",
            "type": "10G_BASE_SR_SFP",
            "vendor": "HPE",
            "oui": "64 9D 99",
            "model": null,
            "revision": "1",
            "serial": "AAA0000AAA00",
            "date": null,
            "ddm": true,
            "encoding": null,
            "cable": "MM",
            "distance": 300,
            "wavelength": 850,
            "connector": "LC",
            "channels": 1
        }
    ]
}
```

### `get_port_description`

Get the description (`ifAlias`) for a given port id.

Route: `/api/v0/ports/:portid/description`

Example:

```curl
curl -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/ports/323/description
```

Output:

```json
{
    "status": "ok",
    "port_description": "GigabitEthernet14"
}
```

### `update_port_description`

Change the description (`ifAlias`) for a given port id.

Route: `/api/v0/ports/:portid/description`

Input (JSON):

- description: The string data to use as the new port description.
Sending an empty string will reset the description to default.

Example:

```curl
curl -X PATCH -d '{"description": "Out-of-Band Management Link"}' -H 'X-Auth-Token: YOURAPITOKENHERE' https://librenms.org/api/v0/ports/323/description
```

Output:
```json
{
    "status": "ok",
    "message": "Port description updated."
}
```
