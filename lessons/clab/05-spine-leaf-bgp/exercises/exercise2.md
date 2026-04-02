1.
```bash
$ 05-spine-leaf-bgp sudo docker exec -it clab-spine-leaf-bgp-leaf1 sr_cli -c "info network-instance default protocols bgp afi-safi ipv4-unicast multipath"
    network-instance default {
        protocols {
            bgp {
                afi-safi ipv4-unicast {
                    multipath {
                        maximum-paths 2
                    }
                }
            }
        }
    }
```

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
| 2.0/24 |        |        | r      |        | t      |        |        | 1.0/31 | et-    |        |        |
|        |        |        |        |        |        |        |        | (indir | 1/49.0 |        |        |
|        |        |        |        |        |        |        |        | ect/lo | ethern |        |        |
|        |        |        |        |        |        |        |        | cal)   | et-    |        |        |
|        |        |        |        |        |        |        |        | 10.10. | 1/50.0 |        |        |
|        |        |        |        |        |        |        |        | 2.0/31 |        |        |        |
|        |        |        |        |        |        |        |        | (indir |        |        |        |
|        |        |        |        |        |        |        |        | ect/lo |        |        |        |
|        |        |        |        |        |        |        |        | cal)   |        |        |        |
| 10.20. | 0      | bgp    | bgp_mg | True   | defaul | 0      | 170    | 10.10. | ethern |        |        |
| 3.0/24 |        |        | r      |        | t      |        |        | 1.0/31 | et-    |        |        |
|        |        |        |        |        |        |        |        | (indir | 1/49.0 |        |        |
|        |        |        |        |        |        |        |        | ect/lo | ethern |        |        |
|        |        |        |        |        |        |        |        | cal)   | et-    |        |        |
|        |        |        |        |        |        |        |        | 10.10. | 1/50.0 |        |        |
|        |        |        |        |        |        |        |        | 2.0/31 |        |        |        |
|        |        |        |        |        |        |        |        | (indir |        |        |        |
|        |        |        |        |        |        |        |        | ect/lo |        |        |        |
|        |        |        |        |        |        |        |        | cal)   |        |        |        |
| 10.20. | 0      | bgp    | bgp_mg | True   | defaul | 0      | 170    | 10.10. | ethern |        |        |
| 4.0/24 |        |        | r      |        | t      |        |        | 1.0/31 | et-    |        |        |
|        |        |        |        |        |        |        |        | (indir | 1/49.0 |        |        |
|        |        |        |        |        |        |        |        | ect/lo | ethern |        |        |
|        |        |        |        |        |        |        |        | cal)   | et-    |        |        |
|        |        |        |        |        |        |        |        | 10.10. | 1/50.0 |        |        |
|        |        |        |        |        |        |        |        | 2.0/31 |        |        |        |
|        |        |        |        |        |        |        |        | (indir |        |        |        |
|        |        |        |        |        |        |        |        | ect/lo |        |        |        |
|        |        |        |        |        |        |        |        | cal)   |        |        |        |
+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+
----------------------------------------------------------------------------------------------------------------------
IPv4 routes total                    : 10
IPv4 prefixes with active routes     : 10
IPv4 prefixes with active ECMP routes: 3
----------------------------------------------------------------------------------------------------------------------
```

5.
```bash
$ 05-spine-leaf-bgp sudo docker exec clab-spine-leaf-bgp-host1 traceroute -n -w 2 10.20.4.2
traceroute to 10.20.4.2 (10.20.4.2), 30 hops max, 60 byte packets
 1  10.20.1.1  0.560 ms  0.560 ms  0.551 ms
 2  10.10.1.0  0.899 ms  0.896 ms  0.891 ms
 3  10.10.1.7  1.575 ms 10.10.2.7  1.576 ms  1.582 ms
 4  10.20.4.2  0.806 ms  0.749 ms  0.754 ms
$ 05-spine-leaf-bgp sudo docker exec clab-spine-leaf-bgp-host1 traceroute -n -w 2 10.20.4.2
traceroute to 10.20.4.2 (10.20.4.2), 30 hops max, 60 byte packets
 1  10.20.1.1  1.119 ms  1.092 ms  1.085 ms
 2  10.10.2.0  1.111 ms  1.105 ms 10.10.1.0  1.346 ms
 3  10.10.1.7  1.176 ms  1.182 ms 10.10.2.7  1.139 ms
 4  * * 10.20.4.2  0.413 ms
$ 05-spine-leaf-bgp sudo docker exec clab-spine-leaf-bgp-host1 traceroute -n -w 2 10.20.4.2
traceroute to 10.20.4.2 (10.20.4.2), 30 hops max, 60 byte packets
 1  10.20.1.1  1.205 ms  1.184 ms  1.175 ms
 2  10.10.1.0  0.729 ms 10.10.2.0  1.167 ms 10.10.1.0  0.723 ms
 3  10.10.2.7  1.302 ms  1.304 ms  1.306 ms
 4  10.20.4.2  0.844 ms  0.865 ms  0.902 ms
$ 05-spine-leaf-bgp sudo docker exec clab-spine-leaf-bgp-host1 traceroute -n -w 2 10.20.4.2
traceroute to 10.20.4.2 (10.20.4.2), 30 hops max, 60 byte packets
 1  10.20.1.1  0.464 ms  0.443 ms  0.438 ms
 2  10.10.2.0  1.318 ms 10.10.1.0  0.648 ms  0.648 ms
 3  10.10.1.7  1.439 ms 10.10.2.7  1.438 ms 10.10.1.7  1.432 ms
 4  10.20.4.2  0.377 ms * *
```

