3. It needs these policies to 1) accept the routes from the peers; 2) properly advertise the connected subnets and 3) to re-advertise the bgp-learned routes. These 3 are fundamental for a working setup

4. 

e.g. for leaf:

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
| default     | 10.10.1.0         | spines      | S   | 65000 | establish | 0d:0h:3m: | ipv4-    | [3/3/1]           |
|             |                   |             |     |       | ed        | 34s       | unicast  |                   |
| default     | 10.10.2.0         | spines      | S   | 65000 | establish | 0d:0h:3m: | ipv4-    | [3/3/4]           |
|             |                   |             |     |       | ed        | 25s       | unicast  |                   |
+-------------+-------------------+-------------+-----+-------+-----------+-----------+----------+-------------------+
----------------------------------------------------------------------------------------------------------------------
Summary:
2 configured neighbors, 2 configured sessions are established, 0 disabled peers
0 dynamic peers
```

e.g. for spine

```bash
$ 05-spine-leaf-bgp sudo docker exec -it clab-spine-leaf-bgp-spine2 sr_cli -c "show network-instance default protocols bgp neighbor"
----------------------------------------------------------------------------------------------------------------------
BGP neighbor summary for network-instance "default"
Flags: S static, D dynamic, L discovered by LLDP, B BFD enabled, - disabled, * slow
----------------------------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------------------------
+-------------+-------------------+-------------+-----+-------+-----------+-----------+----------+-------------------+
|  Net-Inst   |       Peer        |    Group    | Fla | Peer- |   State   |  Uptime   | AFI/SAFI |  [Rx/Active/Tx]   |
|             |                   |             | gs  |  AS   |           |           |          |                   |
+=============+===================+=============+=====+=======+===========+===========+==========+===================+
| default     | 10.10.2.1         | leaves      | S   | 65001 | establish | 0d:0h:5m: | ipv4-    | [4/1/3]           |
|             |                   |             |     |       | ed        | 11s       | unicast  |                   |
| default     | 10.10.2.3         | leaves      | S   | 65002 | establish | 0d:0h:5m: | ipv4-    | [4/1/3]           |
|             |                   |             |     |       | ed        | 11s       | unicast  |                   |
| default     | 10.10.2.5         | leaves      | S   | 65003 | establish | 0d:0h:5m: | ipv4-    | [4/1/3]           |
|             |                   |             |     |       | ed        | 11s       | unicast  |                   |
| default     | 10.10.2.7         | leaves      | S   | 65004 | establish | 0d:0h:4m: | ipv4-    | [4/1/3]           |
|             |                   |             |     |       | ed        | 36s       | unicast  |                   |
+-------------+-------------------+-------------+-----+-------+-----------+-----------+----------+-------------------+
----------------------------------------------------------------------------------------------------------------------
Summary:
4 configured neighbors, 4 configured sessions are established, 0 disabled peers
0 dynamic peers
```

5.

```bash
$ 05-spine-leaf-bgp sudo docker exec clab-spine-leaf-bgp-host1 ping -c 3 10.20.2.2
PING 10.20.2.2 (10.20.2.2) 56(84) bytes of data.
64 bytes from 10.20.2.2: icmp_seq=1 ttl=61 time=24.9 ms
64 bytes from 10.20.2.2: icmp_seq=2 ttl=61 time=0.294 ms
64 bytes from 10.20.2.2: icmp_seq=3 ttl=61 time=0.326 ms

--- 10.20.2.2 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2066ms
rtt min/avg/max/mdev = 0.294/8.502/24.888/11.586 ms
$ 05-spine-leaf-bgp sudo docker exec clab-spine-leaf-bgp-host1 ping -c 3 10.20.3.2
PING 10.20.3.2 (10.20.3.2) 56(84) bytes of data.
64 bytes from 10.20.3.2: icmp_seq=1 ttl=61 time=23.9 ms
64 bytes from 10.20.3.2: icmp_seq=2 ttl=61 time=0.310 ms
64 bytes from 10.20.3.2: icmp_seq=3 ttl=61 time=0.289 ms

--- 10.20.3.2 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2019ms
rtt min/avg/max/mdev = 0.289/8.166/23.901/11.125 ms
$ 05-spine-leaf-bgp sudo docker exec clab-spine-leaf-bgp-host1 ping -c 3 10.20.4.2
PING 10.20.4.2 (10.20.4.2) 56(84) bytes of data.
64 bytes from 10.20.4.2: icmp_seq=1 ttl=61 time=22.9 ms
64 bytes from 10.20.4.2: icmp_seq=2 ttl=61 time=0.315 ms
64 bytes from 10.20.4.2: icmp_seq=3 ttl=61 time=0.299 ms

--- 10.20.4.2 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2027ms
rtt min/avg/max/mdev = 0.299/7.835/22.893/10.647 ms
$ 05-spine-leaf-bgp sudo docker exec clab-spine-leaf-bgp-host2 ping -c 3 10.20.4.2
PING 10.20.4.2 (10.20.4.2) 56(84) bytes of data.
64 bytes from 10.20.4.2: icmp_seq=1 ttl=61 time=0.404 ms
64 bytes from 10.20.4.2: icmp_seq=2 ttl=61 time=0.300 ms
64 bytes from 10.20.4.2: icmp_seq=3 ttl=61 time=0.298 ms

--- 10.20.4.2 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2036ms
rtt min/avg/max/mdev = 0.298/0.334/0.404/0.049 ms
```


