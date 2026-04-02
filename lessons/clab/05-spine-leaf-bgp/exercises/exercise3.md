2.

```bash
$ 05-spine-leaf-bgp sudo docker exec -it clab-spine-leaf-bgp-leaf1 sr_cli -c "show network-instance default route-table ipv4-unicast summary"
----------------------------------------------------------------------------------------------------------------------
IPv4 unicast route table of network instance default
----------------------------------------------------------------------------------------------------------------------
+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+
| Prefix |   ID   | Route  | Route  | Active | Origin | Metric |  Pref  | Next-  | Next-  | Backup | Backup |
|        |        |  Type  | Owner  |        | Networ |        |        |  hop   | hop In | Next-  | Next-  |
|        |        |        |        |        | k Inst |        |        | (Type) | terfac |  hop   | hop In |
|        |        |        |        |        |  ance  |        |        |        |   e    | (Type) | terfac |
|        |        |        |        |        |        |        |        |        |        |        |   e    |
+========+========+========+========+========+========+========+========+========+========+========+========+
| 10.10. | 4      | local  | net_in | True   | defaul | 0      | 0      | 10.10. | ethern |        |        |
| 2.0/31 |        |        | st_mgr |        | t      |        |        | 2.1 (d | et-    |        |        |
|        |        |        |        |        |        |        |        | irect) | 1/50.0 |        |        |
| 10.10. | 4      | host   | net_in | True   | defaul | 0      | 0      | None ( | None   |        |        |
| 2.1/32 |        |        | st_mgr |        | t      |        |        | extrac |        |        |        |
|        |        |        |        |        |        |        |        | t)     |        |        |        |
| 10.20. | 2      | local  | net_in | True   | defaul | 0      | 0      | 10.20. | ethern |        |        |
| 1.0/24 |        |        | st_mgr |        | t      |        |        | 1.1 (d | et-    |        |        |
|        |        |        |        |        |        |        |        | irect) | 1/1.0  |        |        |
| 10.20. | 2      | host   | net_in | True   | defaul | 0      | 0      | None ( | None   |        |        |
| 1.1/32 |        |        | st_mgr |        | t      |        |        | extrac |        |        |        |
|        |        |        |        |        |        |        |        | t)     |        |        |        |
| 10.20. | 2      | host   | net_in | True   | defaul | 0      | 0      | None ( |        |        |        |
| 1.255/ |        |        | st_mgr |        | t      |        |        | broadc |        |        |        |
| 32     |        |        |        |        |        |        |        | ast)   |        |        |        |
| 10.20. | 0      | bgp    | bgp_mg | True   | defaul | 0      | 170    | 10.10. | ethern |        |        |
| 2.0/24 |        |        | r      |        | t      |        |        | 2.0/31 | et-    |        |        |
|        |        |        |        |        |        |        |        | (indir | 1/50.0 |        |        |
|        |        |        |        |        |        |        |        | ect/lo |        |        |        |
|        |        |        |        |        |        |        |        | cal)   |        |        |        |
| 10.20. | 0      | bgp    | bgp_mg | True   | defaul | 0      | 170    | 10.10. | ethern |        |        |
| 3.0/24 |        |        | r      |        | t      |        |        | 2.0/31 | et-    |        |        |
|        |        |        |        |        |        |        |        | (indir | 1/50.0 |        |        |
|        |        |        |        |        |        |        |        | ect/lo |        |        |        |
|        |        |        |        |        |        |        |        | cal)   |        |        |        |
| 10.20. | 0      | bgp    | bgp_mg | True   | defaul | 0      | 170    | 10.10. | ethern |        |        |
| 4.0/24 |        |        | r      |        | t      |        |        | 2.0/31 | et-    |        |        |
|        |        |        |        |        |        |        |        | (indir | 1/50.0 |        |        |
|        |        |        |        |        |        |        |        | ect/lo |        |        |        |
|        |        |        |        |        |        |        |        | cal)   |        |        |        |
+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+
----------------------------------------------------------------------------------------------------------------------
IPv4 routes total                    : 8
IPv4 prefixes with active routes     : 8
IPv4 prefixes with active ECMP routes: 0
----------------------------------------------------------------------------------------------------------------------
```

3.
```bash
$ 05-spine-leaf-bgp sudo docker exec -it clab-spine-leaf-bgp-leaf1 sr_cli -c "show network-instance default protocols bgp neighbor"
----------------------------------------------------------------------------------------------------------------------
BGP neighbor summary for network-instance "default"
Flags: S static, D dynamic, L discovered by LLDP, B BFD enabled, - disabled, * slow
----------------------------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------------------------
+-------------+-------------------+-------------+-----+-------+-----------+-----------+----------+-------------------+
|  Net-Inst   |       Peer        |    Group    | Fla | Peer- |   State   |  Uptime   | AFI/SAFI |  [Rx/Active/Tx]   |
|             |                   |             | gs  |  AS   |           |           |          |                   |
+=============+===================+=============+=====+=======+===========+===========+==========+===================+
| default     | 10.10.1.0         | spines      | S   | 65000 | active    | -         |          |                   |
| default     | 10.10.2.0         | spines      | S   | 65000 | establish | 0d:0h:23m | ipv4-    | [3/3/1]           |
|             |                   |             |     |       | ed        | :29s      | unicast  |                   |
+-------------+-------------------+-------------+-----+-------+-----------+-----------+----------+-------------------+
----------------------------------------------------------------------------------------------------------------------
Summary:
2 configured neighbors, 1 configured sessions are established, 0 disabled peers
0 dynamic peers
```

4.

```bash
$ 05-spine-leaf-bgp sudo docker exec clab-spine-leaf-bgp-host1 traceroute -n -w 2 10.20.4.2
traceroute to 10.20.4.2 (10.20.4.2), 30 hops max, 60 byte packets
 1  10.20.1.1  0.663 ms  0.638 ms  0.631 ms
 2  10.10.2.0  0.674 ms  0.676 ms  0.675 ms
 3  10.10.2.7  0.738 ms  0.749 ms  0.748 ms
 4  10.20.4.2  0.559 ms  0.556 ms  0.561 ms
```

6.
```bash
$ 05-spine-leaf-bgp sudo docker exec -it clab-spine-leaf-bgp-leaf1 sr_cli -c "show network-instance default route-table ipv4-unicast summary"
----------------------------------------------------------------------------------------------------------------------
IPv4 unicast route table of network instance default
----------------------------------------------------------------------------------------------------------------------
+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+
| Prefix |   ID   | Route  | Route  | Active | Origin | Metric |  Pref  | Next-  | Next-  | Backup | Backup |
|        |        |  Type  | Owner  |        | Networ |        |        |  hop   | hop In | Next-  | Next-  |
|        |        |        |        |        | k Inst |        |        | (Type) | terfac |  hop   | hop In |
|        |        |        |        |        |  ance  |        |        |        |   e    | (Type) | terfac |
|        |        |        |        |        |        |        |        |        |        |        |   e    |
+========+========+========+========+========+========+========+========+========+========+========+========+
| 10.10. | 3      | local  | net_in | True   | defaul | 0      | 0      | 10.10. | ethern |        |        |
| 1.0/31 |        |        | st_mgr |        | t      |        |        | 1.1 (d | et-    |        |        |
|        |        |        |        |        |        |        |        | irect) | 1/49.0 |        |        |
| 10.10. | 3      | host   | net_in | True   | defaul | 0      | 0      | None ( | None   |        |        |
| 1.1/32 |        |        | st_mgr |        | t      |        |        | extrac |        |        |        |
|        |        |        |        |        |        |        |        | t)     |        |        |        |
| 10.10. | 4      | local  | net_in | True   | defaul | 0      | 0      | 10.10. | ethern |        |        |
| 2.0/31 |        |        | st_mgr |        | t      |        |        | 2.1 (d | et-    |        |        |
|        |        |        |        |        |        |        |        | irect) | 1/50.0 |        |        |
| 10.10. | 4      | host   | net_in | True   | defaul | 0      | 0      | None ( | None   |        |        |
| 2.1/32 |        |        | st_mgr |        | t      |        |        | extrac |        |        |        |
|        |        |        |        |        |        |        |        | t)     |        |        |        |
| 10.20. | 2      | local  | net_in | True   | defaul | 0      | 0      | 10.20. | ethern |        |        |
| 1.0/24 |        |        | st_mgr |        | t      |        |        | 1.1 (d | et-    |        |        |
|        |        |        |        |        |        |        |        | irect) | 1/1.0  |        |        |
| 10.20. | 2      | host   | net_in | True   | defaul | 0      | 0      | None ( | None   |        |        |
| 1.1/32 |        |        | st_mgr |        | t      |        |        | extrac |        |        |        |
|        |        |        |        |        |        |        |        | t)     |        |        |        |
| 10.20. | 2      | host   | net_in | True   | defaul | 0      | 0      | None ( |        |        |        |
| 1.255/ |        |        | st_mgr |        | t      |        |        | broadc |        |        |        |
| 32     |        |        |        |        |        |        |        | ast)   |        |        |        |
| 10.20. | 0      | bgp    | bgp_mg | True   | defaul | 0      | 170    | 10.10. | ethern |        |        |
| 2.0/24 |        |        | r      |        | t      |        |        | 2.0/31 | et-    |        |        |
|        |        |        |        |        |        |        |        | (indir | 1/50.0 |        |        |
|        |        |        |        |        |        |        |        | ect/lo |        |        |        |
|        |        |        |        |        |        |        |        | cal)   |        |        |        |
| 10.20. | 0      | bgp    | bgp_mg | True   | defaul | 0      | 170    | 10.10. | ethern |        |        |
| 3.0/24 |        |        | r      |        | t      |        |        | 2.0/31 | et-    |        |        |
|        |        |        |        |        |        |        |        | (indir | 1/50.0 |        |        |
|        |        |        |        |        |        |        |        | ect/lo |        |        |        |
|        |        |        |        |        |        |        |        | cal)   |        |        |        |
| 10.20. | 0      | bgp    | bgp_mg | True   | defaul | 0      | 170    | 10.10. | ethern |        |        |
| 4.0/24 |        |        | r      |        | t      |        |        | 2.0/31 | et-    |        |        |
|        |        |        |        |        |        |        |        | (indir | 1/50.0 |        |        |
|        |        |        |        |        |        |        |        | ect/lo |        |        |        |
|        |        |        |        |        |        |        |        | cal)   |        |        |        |
+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+
----------------------------------------------------------------------------------------------------------------------
IPv4 routes total                    : 10
IPv4 prefixes with active routes     : 10
IPv4 prefixes with active ECMP routes: 0
----------------------------------------------------------------------------------------------------------------------
```
