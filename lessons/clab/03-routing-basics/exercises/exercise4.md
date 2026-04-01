1. Yes, the route exists:

```bash
$ 03-routing-basics sudo docker exe-it clab-routing-basics-srl1 sr_cli -c "show network-instance default route-table ipv4-unicast summary"
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

2. 

```bash
$ 03-routing-basics sudo docker exec -it clab-routing-basics-srl1 sr_cli -c "show arpnd arp-entries"
+-----------+-----------+----------------+-----------+--------------------+----------------------------------------+
| Interface | Subinterf |    Neighbor    |  Origin   | Link layer address |                 Expiry                 |
|           |    ace    |                |           |                    |                                        |
+===========+===========+================+===========+====================+========================================+
| ethernet- |         0 |       10.1.1.2 |   dynamic | AA:C1:AB:DE:98:24  | 3 hours from now                       |
| 1/1       |           |                |           |                    |                                        |
| ethernet- |         0 |       10.1.2.2 |   dynamic | 1A:D8:04:FF:00:01  | 2 hours from now                       |
| 1/2       |           |                |           |                    |                                        |
| mgmt0     |         0 |    172.20.20.1 |   dynamic | CA:7F:C2:89:22:68  | 2 hours from now                       |
+-----------+-----------+----------------+-----------+--------------------+----------------------------------------+
----------------------------------------------------------------------------------------------------------------------
  Total entries : 3 (0 static, 3 dynamic)
----------------------------------------------------------------------------------------------------------------------
```

3. This happens because we've changed the next hop for that route - we've created a situation where we're routing traffic on that route to an address that doesn't really exist (black hole)

4/5. Fixed arp table:

```bash
$ 03-routing-basics sudo docker exec -it clab-routing-basics-srl1 sr_cli -c "show arpnd arp-entries"
+-----------+-----------+----------------+-----------+--------------------+----------------------------------------+
| Interface | Subinterf |    Neighbor    |  Origin   | Link layer address |                 Expiry                 |
|           |    ace    |                |           |                    |                                        |
+===========+===========+================+===========+====================+========================================+
| ethernet- |         0 |       10.1.1.2 |   dynamic | AA:C1:AB:DE:98:24  | 3 hours from now                       |
| 1/1       |           |                |           |                    |                                        |
| ethernet- |         0 |       10.1.2.2 |   dynamic | 1A:D8:04:FF:00:01  | 2 hours from now                       |
| 1/2       |           |                |           |                    |                                        |
| ethernet- |         0 |       10.1.3.2 |   dynamic | 1A:B8:05:FF:00:01  | 3 hours from now                       |
| 1/3       |           |                |           |                    |                                        |
| mgmt0     |         0 |    172.20.20.1 |   dynamic | CA:7F:C2:89:22:68  | 2 hours from now                       |
+-----------+-----------+----------------+-----------+--------------------+----------------------------------------+
----------------------------------------------------------------------------------------------------------------------
  Total entries : 4 (0 static, 4 dynamic)
----------------------------------------------------------------------------------------------------------------------
```
