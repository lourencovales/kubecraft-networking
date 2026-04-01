1.

```bash
$ 04-dynamic-routing-bgp sudo docker exec clab-dynamic-routing-bgp-host2 traceroute -n -w 2 10.1.5.2
traceroute to 10.1.5.2 (10.1.5.2), 30 hops max, 60 byte packets
 1  10.1.4.1  0.952 ms  0.921 ms  0.914 ms
 2  10.1.2.1  1.354 ms  1.355 ms  1.349 ms
 3  10.1.3.2  0.780 ms  0.781 ms  0.780 ms
 4  10.1.5.2  0.515 ms  0.518 ms  0.517 ms
```

2.
```bash
$ 04-dynamic-routing-bgp gnmic -a clab-dynamic-routing-bgp-srl2:57400 -u admin -p NokiaSrl1! --skip-verify -e json_ietf set --request-file gnmic/configs/srl2-new-link.json
{
  "source": "clab-dynamic-routing-bgp-srl2:57400",
  "timestamp": 1775046367320348748,
  "time": "2026-04-01T14:26:07.320348748+02:00",
  "results": [
    {
      "operation": "UPDATE",
      "path": "interface[name=ethernet-1/3]"
    },
    {
      "operation": "UPDATE",
      "path": "network-instance[name=default]/interface[name=ethernet-1/3.0]"
    }
  ]
}
$ 04-dynamic-routing-bgp gnmic -a clab-dynamic-routing-bgp-srl3:57400 -u admin -p NokiaSrl1! --skip-verify -e json_ietf set --request-file gnmic/configs/srl3-new-link.json
{
  "source": "clab-dynamic-routing-bgp-srl3:57400",
  "timestamp": 1775046378639122157,
  "time": "2026-04-01T14:26:18.639122157+02:00",
  "results": [
    {
      "operation": "UPDATE",
      "path": "interface[name=ethernet-1/3]"
    },
    {
      "operation": "UPDATE",
      "path": "network-instance[name=default]/interface[name=ethernet-1/3.0]"
    }
  ]
}
```

3. 

```bash
$ 04-dynamic-routing-bgp gnmic -a clab-dynamic-routing-bgp-srl2:57400 -u admin -p NokiaSrl1! --skip-verify -e json_ietf set --request-file gnmic/configs/srl2-bgp-srl3.json
{
  "source": "clab-dynamic-routing-bgp-srl2:57400",
  "timestamp": 1775046439120154345,
  "time": "2026-04-01T14:27:19.120154345+02:00",
  "results": [
    {
      "operation": "UPDATE",
      "path": "network-instance[name=default]/protocols/bgp/neighbor[peer-address=10.1.6.2]"
    }
  ]
}
$ 04-dynamic-routing-bgp gnmic -a clab-dynamic-routing-bgp-srl3:57400 -u admin -p NokiaSrl1! --skip-verify -e json_ietf set --request-file gnmic/configs/srl3-bgp-srl2.json
{
  "source": "clab-dynamic-routing-bgp-srl3:57400",
  "timestamp": 1775046461942913439,
  "time": "2026-04-01T14:27:41.942913439+02:00",
  "results": [
    {
      "operation": "UPDATE",
      "path": "network-instance[name=default]/protocols/bgp/neighbor[peer-address=10.1.6.1]"
    }
  ]
}
```

4.

```bash
$ 04-dynamic-routing-bgp sudo docker exec -it clab-dynamic-routing-bgp-srl2 sr_cli -c "show network-instance default protocols bgp neighbor"
----------------------------------------------------------------------------------------------------------------------
BGP neighbor summary for network-instance "default"
Flags: S static, D dynamic, L discovered by LLDP, B BFD enabled, - disabled, * slow
----------------------------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------------------------
+-------------+-------------------+-------------+-----+-------+-----------+-----------+----------+-------------------+
|  Net-Inst   |       Peer        |    Group    | Fla | Peer- |   State   |  Uptime   | AFI/SAFI |  [Rx/Active/Tx]   |
|             |                   |             | gs  |  AS   |           |           |          |                   |
+=============+===================+=============+=====+=======+===========+===========+==========+===================+
| default     | 10.1.2.1          | ebgp-peers  | S   | 65001 | establish | 0d:0h:9m: | ipv4-    | [4/2/4]           |
|             |                   |             |     |       | ed        | 24s       | unicast  |                   |
| default     | 10.1.6.2          | ebgp-peers  | S   | 65003 | establish | 0d:0h:1m: | ipv4-    | [5/1/5]           |
|             |                   |             |     |       | ed        | 38s       | unicast  |                   |
+-------------+-------------------+-------------+-----+-------+-----------+-----------+----------+-------------------+
----------------------------------------------------------------------------------------------------------------------
Summary:
2 configured neighbors, 2 configured sessions are established, 0 disabled peers
0 dynamic peers
```

5. 

```bash
$ 04-dynamic-routing-bgp sudo docker exec clab-dynamic-routing-bgp-host2 traceroute -n -w 2 10.1.5.2
traceroute to 10.1.5.2 (10.1.5.2), 30 hops max, 60 byte packets
 1  10.1.4.1  0.608 ms  0.570 ms  0.559 ms
 2  10.1.6.2  0.462 ms  0.459 ms  0.456 ms
 3  10.1.5.2  0.329 ms  0.342 ms  0.380 ms
```

6.

```bash
$ 04-dynamic-routing-bgp sudo docker exec -it clab-dynamic-routing-bgp-srl2 sr_cli -c "show network-instance default protocols bgp routes ipv4 summary"
----------------------------------------------------------------------------------------------------------------------
Show report for the BGP route table of network-instance "default"
----------------------------------------------------------------------------------------------------------------------
Status codes: u=used, *=valid, >=best, x=stale, b=backup
Origin codes: i=IGP, e=EGP, ?=incomplete
----------------------------------------------------------------------------------------------------------------------
+-----+-------------+-------------------+-----+-----+-------------------------------------+
| Sta |   Network   |     Next Hop      | MED | Loc |              Path Val               |
| tus |             |                   |     | Pre |                                     |
|     |             |                   |     |  f  |                                     |
+=====+=============+===================+=====+=====+=====================================+
| u*> | 10.1.1.0/24 | 10.1.2.1          |     |     | [65001] i                           |
| *   | 10.1.1.0/24 | 10.1.6.2          |     |     | [65003, 65001] i                    |
| u*> | 10.1.2.0/24 | 0.0.0.0           |     |     |  i                                  |
| *   | 10.1.2.0/24 | 10.1.2.1          |     |     | [65001] i                           |
| *   | 10.1.2.0/24 | 10.1.6.2          |     |     | [65003, 65001] i                    |
| u*> | 10.1.3.0/24 | 10.1.2.1          |     |     | [65001] i                           |
| *   | 10.1.3.0/24 | 10.1.6.2          |     |     | [65003] i                           |
| u*> | 10.1.4.0/24 | 0.0.0.0           |     |     |  i                                  |
| *   | 10.1.5.0/24 | 10.1.2.1          |     |     | [65001, 65003] i                    |
| u*> | 10.1.5.0/24 | 10.1.6.2          |     |     | [65003] i                           |
| u*> | 10.1.6.0/24 | 0.0.0.0           |     |     |  i                                  |
| *   | 10.1.6.0/24 | 10.1.6.2          |     |     | [65003] i                           |
+-----+-------------+-------------------+-----+-----+-------------------------------------+
----------------------------------------------------------------------------------------------------------------------
12 received BGP routes: 6 used, 12 valid, 0 stale
6 available destinations: 6 with ECMP multipaths
----------------------------------------------------------------------------------------------------------------------
```

7.

```bash
$ 04-dynamic-routing-bgp sudo docker exec -it clab-dynamic-routing-bgp-srl2 sr_cli -c "show network-instance default protocols bgp routes ipv4 prefix 10.1.5.0/24 detail"
----------------------------------------------------------------------------------------------------------------------
Show report for the BGP routes to network "10.1.5.0/24" network-instance  "default"
----------------------------------------------------------------------------------------------------------------------
Network: 10.1.5.0/24
Received Paths: 2
  Path 1: <Valid,>
    Route source    : neighbor 10.1.2.1
    Route Preference: MED is -, No LocalPref
    BGP next-hop    : 10.1.2.1
    Path            :  i [65001, 65003]
    Communities     : None
    RR Attributes   : No Originator-ID, Cluster-List is [ - ]
    Aggregation     : Not an aggregate route
    Unknown Attr    : None
    Invalid Reason  : None
    Tie Break Reason: as-path-length
  Path 2: <Best,Valid,Used,>
    Route source    : neighbor 10.1.6.2
    Route Preference: MED is -, No LocalPref
    BGP next-hop    : 10.1.6.2
    Path            :  i [65003]
    Communities     : None
    RR Attributes   : No Originator-ID, Cluster-List is [ - ]
    Aggregation     : Not an aggregate route
    Unknown Attr    : None
    Invalid Reason  : None
    Tie Break Reason: none

Path 2 was advertised to:
[ 10.1.2.1 ]
Route Preference: MED is -, No LocalPref
Path            :  i [65002, 65003]
Communities     : None
RR Attributes   : No Originator-ID, Cluster-List is [ - ]
Aggregation     : Not an aggregate route
Unknown Attr    : None
----------------------------------------------------------------------------------------------------------------------
```
