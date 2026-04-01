1.
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
| default     | 10.1.2.1          | ebgp-peers  | S   | 65099 | active    | -         |          |                   |
| default     | 10.1.6.2          | ebgp-peers  | S   | 65003 | establish | 0d:1h:16m | ipv4-    | [2/1/3]           |
|             |                   |             |     |       | ed        | :5s       | unicast  |                   |
+-------------+-------------------+-------------+-----+-------+-----------+-----------+----------+-------------------+
----------------------------------------------------------------------------------------------------------------------
Summary:
2 configured neighbors, 1 configured sessions are established, 0 disabled peers
0 dynamic peers
```

2.
```bash
$ 04-dynamic-routing-bgp sudo docker exec -it clab-dynamic-routing-bgp-srl1 sr_cli -c "show network-instance default protocols bgp neighbor"
----------------------------------------------------------------------------------------------------------------------
BGP neighbor summary for network-instance "default"
Flags: S static, D dynamic, L discovered by LLDP, B BFD enabled, - disabled, * slow
----------------------------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------------------------
+-------------+-------------------+-------------+-----+-------+-----------+-----------+----------+-------------------+
|  Net-Inst   |       Peer        |    Group    | Fla | Peer- |   State   |  Uptime   | AFI/SAFI |  [Rx/Active/Tx]   |
|             |                   |             | gs  |  AS   |           |           |          |                   |
+=============+===================+=============+=====+=======+===========+===========+==========+===================+
| default     | 10.1.2.2          | ebgp-peers  | S   | 65002 | active    | -         |          |                   |
| default     | 10.1.3.2          | ebgp-peers  | S   | 65003 | active    | -         |          |                   |
+-------------+-------------------+-------------+-----+-------+-----------+-----------+----------+-------------------+
----------------------------------------------------------------------------------------------------------------------
Summary:
2 configured neighbors, 0 configured sessions are established, 0 disabled peers
0 dynamic peers
```

3.
```bash
$ 04-dynamic-routing-bgp sudo docker exec -it clab-dynamic-routing-bgp-srl2 sr_cli
Using configuration file(s): []
Welcome to the srlinux CLI.
Type 'help' (and press <ENTER>) if you need any help using this.
--{ + running }--[  ]--
A:srl2# enter candidate
--{ + candidate shared default }--[  ]--
A:srl2# set / network-instance default protocols bgp neighbor 10.1.2.1 peer-as 65001
--{ +* candidate shared default }--[  ]--
A:srl2# commit now
All changes have been committed. Leaving candidate mode.
--{ + running }--[  ]--
A:srl2# exit
--{ + running }--[  ]--
A:srl2#
EOF encountered
```

4.
```bash
$ 04-dynamic-routing-bgp sudo docker exec -it clab-dynamic-routing-bgp-host2 ping -c 3 10.1.1.2
PING 10.1.1.2 (10.1.1.2) 56(84) bytes of data.
64 bytes from 10.1.1.2: icmp_seq=1 ttl=62 time=0.304 ms
64 bytes from 10.1.1.2: icmp_seq=2 ttl=62 time=0.230 ms
64 bytes from 10.1.1.2: icmp_seq=3 ttl=62 time=0.213 ms

--- 10.1.1.2 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2058ms
rtt min/avg/max/mdev = 0.213/0.249/0.304/0.039 ms
```
