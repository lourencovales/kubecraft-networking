Routes before:

```bash
$ 04-dynamic-routing-bgp sudo docker exec -it clab-dynamic-routing-bgp-srl1 sr_cli -c "show network-instance default route-table ipv4-unicast summary"
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
| 10.1.1 | 2      | local  | net_in | True   | defaul | 0      | 0      | 10.1.1 | ethern |        |        |
| .0/24  |        |        | st_mgr |        | t      |        |        | .1 (di | et-    |        |        |
|        |        |        |        |        |        |        |        | rect)  | 1/1.0  |        |        |
| 10.1.1 | 2      | host   | net_in | True   | defaul | 0      | 0      | None ( | None   |        |        |
| .1/32  |        |        | st_mgr |        | t      |        |        | extrac |        |        |        |
|        |        |        |        |        |        |        |        | t)     |        |        |        |
| 10.1.1 | 2      | host   | net_in | True   | defaul | 0      | 0      | None ( |        |        |        |
| .255/3 |        |        | st_mgr |        | t      |        |        | broadc |        |        |        |
| 2      |        |        |        |        |        |        |        | ast)   |        |        |        |
| 10.1.2 | 3      | local  | net_in | True   | defaul | 0      | 0      | 10.1.2 | ethern |        |        |
| .0/24  |        |        | st_mgr |        | t      |        |        | .1 (di | et-    |        |        |
|        |        |        |        |        |        |        |        | rect)  | 1/2.0  |        |        |
| 10.1.2 | 3      | host   | net_in | True   | defaul | 0      | 0      | None ( | None   |        |        |
| .1/32  |        |        | st_mgr |        | t      |        |        | extrac |        |        |        |
|        |        |        |        |        |        |        |        | t)     |        |        |        |
| 10.1.2 | 3      | host   | net_in | True   | defaul | 0      | 0      | None ( |        |        |        |
| .255/3 |        |        | st_mgr |        | t      |        |        | broadc |        |        |        |
| 2      |        |        |        |        |        |        |        | ast)   |        |        |        |
| 10.1.3 | 4      | local  | net_in | True   | defaul | 0      | 0      | 10.1.3 | ethern |        |        |
| .0/24  |        |        | st_mgr |        | t      |        |        | .1 (di | et-    |        |        |
|        |        |        |        |        |        |        |        | rect)  | 1/3.0  |        |        |
| 10.1.3 | 4      | host   | net_in | True   | defaul | 0      | 0      | None ( | None   |        |        |
| .1/32  |        |        | st_mgr |        | t      |        |        | extrac |        |        |        |
|        |        |        |        |        |        |        |        | t)     |        |        |        |
| 10.1.3 | 4      | host   | net_in | True   | defaul | 0      | 0      | None ( |        |        |        |
| .255/3 |        |        | st_mgr |        | t      |        |        | broadc |        |        |        |
| 2      |        |        |        |        |        |        |        | ast)   |        |        |        |
+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+
----------------------------------------------------------------------------------------------------------------------
IPv4 routes total                    : 9
IPv4 prefixes with active routes     : 9
IPv4 prefixes with active ECMP routes: 0
----------------------------------------------------------------------------------------------------------------------
```

After:

```bash
$ 04-dynamic-routing-bgp sudo docker exec -it clab-dynamic-routing-bgp-srl1 sr_cli -c "show network-instance default route-table ipv4-unicast summary"
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
| 10.1.1 | 2      | local  | net_in | True   | defaul | 0      | 0      | 10.1.1 | ethern |        |        |
| .0/24  |        |        | st_mgr |        | t      |        |        | .1 (di | et-    |        |        |
|        |        |        |        |        |        |        |        | rect)  | 1/1.0  |        |        |
| 10.1.1 | 2      | host   | net_in | True   | defaul | 0      | 0      | None ( | None   |        |        |
| .1/32  |        |        | st_mgr |        | t      |        |        | extrac |        |        |        |
|        |        |        |        |        |        |        |        | t)     |        |        |        |
| 10.1.1 | 2      | host   | net_in | True   | defaul | 0      | 0      | None ( |        |        |        |
| .255/3 |        |        | st_mgr |        | t      |        |        | broadc |        |        |        |
| 2      |        |        |        |        |        |        |        | ast)   |        |        |        |
| 10.1.2 | 3      | local  | net_in | True   | defaul | 0      | 0      | 10.1.2 | ethern |        |        |
| .0/24  |        |        | st_mgr |        | t      |        |        | .1 (di | et-    |        |        |
|        |        |        |        |        |        |        |        | rect)  | 1/2.0  |        |        |
| 10.1.2 | 3      | host   | net_in | True   | defaul | 0      | 0      | None ( | None   |        |        |
| .1/32  |        |        | st_mgr |        | t      |        |        | extrac |        |        |        |
|        |        |        |        |        |        |        |        | t)     |        |        |        |
| 10.1.2 | 3      | host   | net_in | True   | defaul | 0      | 0      | None ( |        |        |        |
| .255/3 |        |        | st_mgr |        | t      |        |        | broadc |        |        |        |
| 2      |        |        |        |        |        |        |        | ast)   |        |        |        |
| 10.1.3 | 4      | local  | net_in | True   | defaul | 0      | 0      | 10.1.3 | ethern |        |        |
| .0/24  |        |        | st_mgr |        | t      |        |        | .1 (di | et-    |        |        |
|        |        |        |        |        |        |        |        | rect)  | 1/3.0  |        |        |
| 10.1.3 | 4      | host   | net_in | True   | defaul | 0      | 0      | None ( | None   |        |        |
| .1/32  |        |        | st_mgr |        | t      |        |        | extrac |        |        |        |
|        |        |        |        |        |        |        |        | t)     |        |        |        |
| 10.1.3 | 4      | host   | net_in | True   | defaul | 0      | 0      | None ( |        |        |        |
| .255/3 |        |        | st_mgr |        | t      |        |        | broadc |        |        |        |
| 2      |        |        |        |        |        |        |        | ast)   |        |        |        |
| 10.1.4 | 0      | bgp    | bgp_mg | True   | defaul | 0      | 170    | 10.1.2 | ethern |        |        |
| .0/24  |        |        | r      |        | t      |        |        | .0/24  | et-    |        |        |
|        |        |        |        |        |        |        |        | (indir | 1/2.0  |        |        |
|        |        |        |        |        |        |        |        | ect/lo |        |        |        |
|        |        |        |        |        |        |        |        | cal)   |        |        |        |
| 10.1.5 | 0      | bgp    | bgp_mg | True   | defaul | 0      | 170    | 10.1.3 | ethern |        |        |
| .0/24  |        |        | r      |        | t      |        |        | .0/24  | et-    |        |        |
|        |        |        |        |        |        |        |        | (indir | 1/3.0  |        |        |
|        |        |        |        |        |        |        |        | ect/lo |        |        |        |
|        |        |        |        |        |        |        |        | cal)   |        |        |        |
+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+
----------------------------------------------------------------------------------------------------------------------
IPv4 routes total                    : 11
IPv4 prefixes with active routes     : 11
IPv4 prefixes with active ECMP routes: 0
----------------------------------------------------------------------------------------------------------------------
```

```bash
$ 04-dynamic-routing-bgp sudo docker exec clab-dynamic-routing-bgp-host1 ping -c 3 10.1.4.2
PING 10.1.4.2 (10.1.4.2) 56(84) bytes of data.
64 bytes from 10.1.4.2: icmp_seq=1 ttl=62 time=106 ms
64 bytes from 10.1.4.2: icmp_seq=2 ttl=62 time=0.202 ms
64 bytes from 10.1.4.2: icmp_seq=3 ttl=62 time=0.229 ms

--- 10.1.4.2 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2025ms
rtt min/avg/max/mdev = 0.202/35.587/106.332/50.023 ms
$ 04-dynamic-routing-bgp sudo docker exec clab-dynamic-routing-bgp-host1 ping -c 3 10.1.5.2
PING 10.1.5.2 (10.1.5.2) 56(84) bytes of data.
64 bytes from 10.1.5.2: icmp_seq=1 ttl=62 time=101 ms
64 bytes from 10.1.5.2: icmp_seq=2 ttl=62 time=0.217 ms
64 bytes from 10.1.5.2: icmp_seq=3 ttl=62 time=0.236 ms

--- 10.1.5.2 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2034ms
rtt min/avg/max/mdev = 0.217/33.894/101.229/47.613 ms
$ 04-dynamic-routing-bgp sudo docker exec clab-dynamic-routing-bgp-host2 ping -c 3 10.1.5.2
PING 10.1.5.2 (10.1.5.2) 56(84) bytes of data.
64 bytes from 10.1.5.2: icmp_seq=1 ttl=61 time=0.512 ms
64 bytes from 10.1.5.2: icmp_seq=2 ttl=61 time=0.318 ms
64 bytes from 10.1.5.2: icmp_seq=3 ttl=61 time=0.311 ms

--- 10.1.5.2 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2030ms
rtt min/avg/max/mdev = 0.311/0.380/0.512/0.093 ms
```
