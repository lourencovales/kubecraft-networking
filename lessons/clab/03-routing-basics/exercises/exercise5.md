1.

```bash
$ 03-routing-basics sudo docker exec clab-routing-basics-host1 traceroute -n -w 2 10.1.5.2
traceroute to 10.1.5.2 (10.1.5.2), 30 hops max, 60 byte packets
 1  10.1.1.1  1.153 ms  1.135 ms  1.125 ms
 2  10.1.2.2  0.495 ms  0.498 ms  0.496 ms
 3  10.1.2.1  1.075 ms  1.069 ms  1.059 ms
 4  10.1.2.2  1.397 ms  1.396 ms  1.390 ms
 5  * * *
 6  10.1.2.2  1.340 ms  0.991 ms  0.974 ms
 7  * * *
 8  10.1.2.2  1.182 ms * *
 9  * * *
10  * * *
11  * * *
12  10.1.2.2  1.566 ms  1.571 ms  1.697 ms
13  * * *
14  10.1.2.2  2.373 ms  2.376 ms  2.374 ms
15  * * *
16  10.1.2.2  2.335 ms  2.332 ms  1.264 ms
17  * * *
18  10.1.2.2  0.962 ms * *
19  * * *
20  * 10.1.2.2  1.533 ms  1.533 ms
21  * * *
22  10.1.2.2  1.492 ms  1.489 ms  1.487 ms
23  * * *
24  10.1.2.2  2.279 ms  2.282 ms  2.278 ms
25  * * *
26  10.1.2.2  1.925 ms  1.920 ms *
```

2. TTL is "time to live", is a hop limit, and that's why it eventually stops (I didn't wait for it). So, when it reaches the limit, the package is "discarded"

3/4.

```bash
$ 03-routing-basics sudo docker exec -it clab-routing-basics-srl1 sr_cli
Using configuration file(s): []
Welcome to the srlinux CLI.
Type 'help' (and press <ENTER>) if you need any help using this.
--{ + running }--[  ]--
A:srl1# enter candidate
--{ + candidate shared default }--[  ]--
A:srl1# set / network-instance default next-hop-groups group nhg-10-1-5-0-24 nexthop 1 ip-address 10.1.3.2
--{ +* candidate shared default }--[  ]--
A:srl1# commit now
All changes have been committed. Leaving candidate mode.
--{ + running }--[  ]--
A:srl1# exit
--{ + running }--[  ]--
A:srl1#
EOF encountered
$ 03-routing-basics sudo docker exec clab-routing-basics-host1 ping -c 3 10.1.5.2
PING 10.1.5.2 (10.1.5.2) 56(84) bytes of data.
64 bytes from 10.1.5.2: icmp_seq=1 ttl=62 time=0.411 ms
64 bytes from 10.1.5.2: icmp_seq=2 ttl=62 time=0.184 ms
64 bytes from 10.1.5.2: icmp_seq=3 ttl=62 time=0.230 ms

--- 10.1.5.2 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2073ms
rtt min/avg/max/mdev = 0.184/0.275/0.411/0.097 ms
```
