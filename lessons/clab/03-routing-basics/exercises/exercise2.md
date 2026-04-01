# Routing table for SRL1

```bash
$ 03-routing-basics sudo docker exec -it clab-routing-basics-srl1 sr_cli -c "show network-instance default route-table ipv4-unicast summary"
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
| 10.1.4 | 0      | static | static | True   | defaul | 1      | 5      | 10.1.2 | ethern |        |        |
| .0/24  |        |        | _route |        | t      |        |        | .0/24  | et-    |        |        |
|        |        |        | _mgr   |        |        |        |        | (indir | 1/2.0  |        |        |
|        |        |        |        |        |        |        |        | ect/lo |        |        |        |
|        |        |        |        |        |        |        |        | cal)   |        |        |        |
| 10.1.5 | 0      | static | static | True   | defaul | 1      | 5      | 10.1.3 | ethern |        |        |
| .0/24  |        |        | _route |        | t      |        |        | .0/24  | et-    |        |        |
|        |        |        | _mgr   |        |        |        |        | (indir | 1/3.0  |        |        |
|        |        |        |        |        |        |        |        | ect/lo |        |        |        |
|        |        |        |        |        |        |        |        | cal)   |        |        |        |
+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+
----------------------------------------------------------------------------------------------------------------------
IPv4 routes total                    : 11
IPv4 prefixes with active routes     : 11
IPv4 prefixes with active ECMP routes: 0
----------------------------------------------------------------------------------------------------------------------
```

# Routing table for SRL2

```bash
$ 03-routing-basics sudo docker exec -it clab-routing-basics-srl2 sr_cli -c "show network-instance default route-table ipv4-unicast summary"
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
| 10.1.1 | 0      | static | static | True   | defaul | 1      | 5      | 10.1.2 | ethern |        |        |
| .0/24  |        |        | _route |        | t      |        |        | .0/24  | et-    |        |        |
|        |        |        | _mgr   |        |        |        |        | (indir | 1/1.0  |        |        |
|        |        |        |        |        |        |        |        | ect/lo |        |        |        |
|        |        |        |        |        |        |        |        | cal)   |        |        |        |
| 10.1.2 | 2      | local  | net_in | True   | defaul | 0      | 0      | 10.1.2 | ethern |        |        |
| .0/24  |        |        | st_mgr |        | t      |        |        | .2 (di | et-    |        |        |
|        |        |        |        |        |        |        |        | rect)  | 1/1.0  |        |        |
| 10.1.2 | 2      | host   | net_in | True   | defaul | 0      | 0      | None ( | None   |        |        |
| .2/32  |        |        | st_mgr |        | t      |        |        | extrac |        |        |        |
|        |        |        |        |        |        |        |        | t)     |        |        |        |
| 10.1.2 | 2      | host   | net_in | True   | defaul | 0      | 0      | None ( |        |        |        |
| .255/3 |        |        | st_mgr |        | t      |        |        | broadc |        |        |        |
| 2      |        |        |        |        |        |        |        | ast)   |        |        |        |
| 10.1.3 | 0      | static | static | True   | defaul | 1      | 5      | 10.1.2 | ethern |        |        |
| .0/24  |        |        | _route |        | t      |        |        | .0/24  | et-    |        |        |
|        |        |        | _mgr   |        |        |        |        | (indir | 1/1.0  |        |        |
|        |        |        |        |        |        |        |        | ect/lo |        |        |        |
|        |        |        |        |        |        |        |        | cal)   |        |        |        |
| 10.1.4 | 3      | local  | net_in | True   | defaul | 0      | 0      | 10.1.4 | ethern |        |        |
| .0/24  |        |        | st_mgr |        | t      |        |        | .1 (di | et-    |        |        |
|        |        |        |        |        |        |        |        | rect)  | 1/2.0  |        |        |
| 10.1.4 | 3      | host   | net_in | True   | defaul | 0      | 0      | None ( | None   |        |        |
| .1/32  |        |        | st_mgr |        | t      |        |        | extrac |        |        |        |
|        |        |        |        |        |        |        |        | t)     |        |        |        |
| 10.1.4 | 3      | host   | net_in | True   | defaul | 0      | 0      | None ( |        |        |        |
| .255/3 |        |        | st_mgr |        | t      |        |        | broadc |        |        |        |
| 2      |        |        |        |        |        |        |        | ast)   |        |        |        |
| 10.1.5 | 0      | static | static | True   | defaul | 1      | 5      | 10.1.2 | ethern |        |        |
| .0/24  |        |        | _route |        | t      |        |        | .0/24  | et-    |        |        |
|        |        |        | _mgr   |        |        |        |        | (indir | 1/1.0  |        |        |
|        |        |        |        |        |        |        |        | ect/lo |        |        |        |
|        |        |        |        |        |        |        |        | cal)   |        |        |        |
+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+
----------------------------------------------------------------------------------------------------------------------
IPv4 routes total                    : 9
IPv4 prefixes with active routes     : 9
IPv4 prefixes with active ECMP routes: 0
----------------------------------------------------------------------------------------------------------------------
```

# Routing table for SRL3

```bash
$ 03-routing-basics sudo docker exec -it clab-routing-basics-srl3 sr_cli -c "show network-instance default route-table ipv4-unicast summary"
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
| 10.1.1 | 0      | static | static | True   | defaul | 1      | 5      | 10.1.3 | ethern |        |        |
| .0/24  |        |        | _route |        | t      |        |        | .0/24  | et-    |        |        |
|        |        |        | _mgr   |        |        |        |        | (indir | 1/1.0  |        |        |
|        |        |        |        |        |        |        |        | ect/lo |        |        |        |
|        |        |        |        |        |        |        |        | cal)   |        |        |        |
| 10.1.2 | 0      | static | static | True   | defaul | 1      | 5      | 10.1.3 | ethern |        |        |
| .0/24  |        |        | _route |        | t      |        |        | .0/24  | et-    |        |        |
|        |        |        | _mgr   |        |        |        |        | (indir | 1/1.0  |        |        |
|        |        |        |        |        |        |        |        | ect/lo |        |        |        |
|        |        |        |        |        |        |        |        | cal)   |        |        |        |
| 10.1.3 | 2      | local  | net_in | True   | defaul | 0      | 0      | 10.1.3 | ethern |        |        |
| .0/24  |        |        | st_mgr |        | t      |        |        | .2 (di | et-    |        |        |
|        |        |        |        |        |        |        |        | rect)  | 1/1.0  |        |        |
| 10.1.3 | 2      | host   | net_in | True   | defaul | 0      | 0      | None ( | None   |        |        |
| .2/32  |        |        | st_mgr |        | t      |        |        | extrac |        |        |        |
|        |        |        |        |        |        |        |        | t)     |        |        |        |
| 10.1.3 | 2      | host   | net_in | True   | defaul | 0      | 0      | None ( |        |        |        |
| .255/3 |        |        | st_mgr |        | t      |        |        | broadc |        |        |        |
| 2      |        |        |        |        |        |        |        | ast)   |        |        |        |
| 10.1.4 | 0      | static | static | True   | defaul | 1      | 5      | 10.1.3 | ethern |        |        |
| .0/24  |        |        | _route |        | t      |        |        | .0/24  | et-    |        |        |
|        |        |        | _mgr   |        |        |        |        | (indir | 1/1.0  |        |        |
|        |        |        |        |        |        |        |        | ect/lo |        |        |        |
|        |        |        |        |        |        |        |        | cal)   |        |        |        |
| 10.1.5 | 3      | local  | net_in | True   | defaul | 0      | 0      | 10.1.5 | ethern |        |        |
| .0/24  |        |        | st_mgr |        | t      |        |        | .1 (di | et-    |        |        |
|        |        |        |        |        |        |        |        | rect)  | 1/2.0  |        |        |
| 10.1.5 | 3      | host   | net_in | True   | defaul | 0      | 0      | None ( | None   |        |        |
| .1/32  |        |        | st_mgr |        | t      |        |        | extrac |        |        |        |
|        |        |        |        |        |        |        |        | t)     |        |        |        |
| 10.1.5 | 3      | host   | net_in | True   | defaul | 0      | 0      | None ( |        |        |        |
| .255/3 |        |        | st_mgr |        | t      |        |        | broadc |        |        |        |
| 2      |        |        |        |        |        |        |        | ast)   |        |        |        |
+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+
----------------------------------------------------------------------------------------------------------------------
IPv4 routes total                    : 9
IPv4 prefixes with active routes     : 9
IPv4 prefixes with active ECMP routes: 0
----------------------------------------------------------------------------------------------------------------------

``````

- Path from host2 to host3:
    host2 > srl2 > srl1 > srl3 > host3
- Path from host3 to host2:
    host3 > srl3 > srl1 > srl2 > host2
