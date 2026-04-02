This is seemingly not working:

```bash
$ 05-spine-leaf-bgp sudo docker exec -it clab-spine-leaf-bgp-leaf1 sr_cli
Using configuration file(s): []
Welcome to the srlinux CLI.
Type 'help' (and press <ENTER>) if you need any help using this.
--{ + running }--[  ]--
A:leaf1# enter candidate
--{ + candidate shared default }--[  ]--
A:leaf1# set / routing-policy prefix-set hijack prefix 10.20.4.0/25 mask-length-range exact
--{ +* candidate shared default }--[  ]--
A:leaf1# set / routing-policy policy export-hijack statement 10 match prefix-set hijack
--{ +* candidate shared default }--[  ]--
A:leaf1# set / routing-policy policy export-hijack statement 10 action policy-result accept
--{ +* candidate shared default }--[  ]--
A:leaf1# set / routing-policy policy export-hijack statement 20 match protocol local
--{ +* candidate shared default }--[  ]--
A:leaf1# set / routing-policy policy export-hijack statement 20 action policy-result accept
--{ +* candidate shared default }--[  ]--
A:leaf1# set / routing-policy policy export-hijack default-action policy-result reject
--{ +* candidate shared default }--[  ]--
A:leaf1# set / network-instance default protocols bgp group spines export-policy [export-hijack]
--{ +* candidate shared default }--[  ]--
A:leaf1# set / network-instance default static-routes route 10.20.4.0/25 admin-state enable
--{ +* candidate shared default }--[  ]--
A:leaf1# set / network-instance default next-hop-groups group nhg-blackhole admin-state enable
--{ +* candidate shared default }--[  ]--
A:leaf1# set / network-instance default next-hop-groups group nhg-blackhole nexthop 1 ip-address 192.0.2.1
--{ +* candidate shared default }--[  ]--
A:leaf1# set / network-instance default static-routes route 10.20.4.0/25 next-hop-group nhg-blackhole
--{ +* candidate shared default }--[  ]--
A:leaf1# commit now
All changes have been committed. Leaving candidate mode.
--{ + running }--[  ]--
A:leaf1# exit
--{ + running }--[  ]--
A:leaf1#
EOF encountered
$ 05-spine-leaf-bgp sudo docker exec clab-spine-leaf-bgp-host2 ping -c 3 -W 5 10.20.4.2
PING 10.20.4.2 (10.20.4.2) 56(84) bytes of data.
64 bytes from 10.20.4.2: icmp_seq=1 ttl=61 time=0.489 ms
64 bytes from 10.20.4.2: icmp_seq=2 ttl=61 time=0.327 ms
64 bytes from 10.20.4.2: icmp_seq=3 ttl=61 time=0.311 ms

--- 10.20.4.2 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2030ms
rtt min/avg/max/mdev = 0.311/0.375/0.489/0.080 ms

```
