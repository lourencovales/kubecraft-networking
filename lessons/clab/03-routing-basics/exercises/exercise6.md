How it started:
```bash
$ 03-routing-basics sudo docker exec -it clab-routing-basics-srl1 sr_cli -c "show interface brief"
+---------------------+------------------+------------------+------------------+------------------+------------------+
|        Port         |   Admin State    |    Oper State    |      Speed       |       Type       |   Description    |
+=====================+==================+==================+==================+==================+==================+
| ethernet-1/1        | enable           | up               | 25G              |                  |                  |
| ethernet-1/2        | enable           | up               | 25G              |                  |                  |
| ethernet-1/3        | enable           | up               | 25G              |                  |                  |
| ethernet-1/4        | disable          | down             | 25G              |                  |                  |
| ethernet-1/5        | disable          | down             | 25G              |                  |                  |
| ethernet-1/6        | disable          | down             | 25G              |                  |                  |
| ethernet-1/7        | disable          | down             | 25G              |                  |                  |
| ethernet-1/8        | disable          | down             | 25G              |                  |                  |
| ethernet-1/9        | disable          | down             | 25G              |                  |                  |
| ethernet-1/10       | disable          | down             | 25G              |                  |                  |
| ethernet-1/11       | disable          | down             | 25G              |                  |                  |
| ethernet-1/12       | disable          | down             | 25G              |                  |                  |
| ethernet-1/13       | disable          | down             | 25G              |                  |                  |
| ethernet-1/14       | disable          | down             | 25G              |                  |                  |
| ethernet-1/15       | disable          | down             | 25G              |                  |                  |
| ethernet-1/16       | disable          | down             | 25G              |                  |                  |
| ethernet-1/17       | disable          | down             | 25G              |                  |                  |
| ethernet-1/18       | disable          | down             | 25G              |                  |                  |
| ethernet-1/19       | disable          | down             | 25G              |                  |                  |
| ethernet-1/20       | disable          | down             | 25G              |                  |                  |
| ethernet-1/21       | disable          | down             | 25G              |                  |                  |
| ethernet-1/22       | disable          | down             | 25G              |                  |                  |
| ethernet-1/23       | disable          | down             | 25G              |                  |                  |
| ethernet-1/24       | disable          | down             | 25G              |                  |                  |
| ethernet-1/25       | disable          | down             | 25G              |                  |                  |
| ethernet-1/26       | disable          | down             | 25G              |                  |                  |
| ethernet-1/27       | disable          | down             | 25G              |                  |                  |
| ethernet-1/28       | disable          | down             | 25G              |                  |                  |
| ethernet-1/29       | disable          | down             | 25G              |                  |                  |
| ethernet-1/30       | disable          | down             | 25G              |                  |                  |
| ethernet-1/31       | disable          | down             | 25G              |                  |                  |
| ethernet-1/32       | disable          | down             | 25G              |                  |                  |
| ethernet-1/33       | disable          | down             | 25G              |                  |                  |
| ethernet-1/34       | disable          | down             | 25G              |                  |                  |
| ethernet-1/35       | disable          | down             | 25G              |                  |                  |
| ethernet-1/36       | disable          | down             | 25G              |                  |                  |
| ethernet-1/37       | disable          | down             | 25G              |                  |                  |
| ethernet-1/38       | disable          | down             | 25G              |                  |                  |
| ethernet-1/39       | disable          | down             | 25G              |                  |                  |
| ethernet-1/40       | disable          | down             | 25G              |                  |                  |
| ethernet-1/41       | disable          | down             | 25G              |                  |                  |
| ethernet-1/42       | disable          | down             | 25G              |                  |                  |
| ethernet-1/43       | disable          | down             | 25G              |                  |                  |
| ethernet-1/44       | disable          | down             | 25G              |                  |                  |
| ethernet-1/45       | disable          | down             | 25G              |                  |                  |
| ethernet-1/46       | disable          | down             | 25G              |                  |                  |
| ethernet-1/47       | disable          | down             | 25G              |                  |                  |
| ethernet-1/48       | disable          | down             | 25G              |                  |                  |
| ethernet-1/49       | disable          | down             | 100G             |                  |                  |
| ethernet-1/50       | disable          | down             | 100G             |                  |                  |
| ethernet-1/51       | disable          | down             | 100G             |                  |                  |
| ethernet-1/52       | disable          | down             | 100G             |                  |                  |
| ethernet-1/53       | disable          | down             | 100G             |                  |                  |
| ethernet-1/54       | disable          | down             | 100G             |                  |                  |
| ethernet-1/55       | disable          | down             | 100G             |                  |                  |
| ethernet-1/56       | disable          | down             | 100G             |                  |                  |
| ethernet-1/57       | disable          | down             | 10G              |                  |                  |
| ethernet-1/58       | disable          | down             | 10G              |                  |                  |
| mgmt0               | enable           | up               | 1G               |                  |                  |
+---------------------+------------------+------------------+------------------+------------------+------------------+
```

1.

```bash
$ 03-routing-basics sudo docker exec -it clab-routing-basics-srl1 sr_cli -c "show interface brief"
+---------------------+------------------+------------------+------------------+------------------+------------------+
|        Port         |   Admin State    |    Oper State    |      Speed       |       Type       |   Description    |
+=====================+==================+==================+==================+==================+==================+
| ethernet-1/1        | enable           | up               | 25G              |                  |                  |
| ethernet-1/2        | enable           | up               | 25G              |                  |                  |
| ethernet-1/3        | disable          | down             | 25G              |                  |                  |
| ethernet-1/4        | disable          | down             | 25G              |                  |                  |
| ethernet-1/5        | disable          | down             | 25G              |                  |                  |
| ethernet-1/6        | disable          | down             | 25G              |                  |                  |
| ethernet-1/7        | disable          | down             | 25G              |                  |                  |
| ethernet-1/8        | disable          | down             | 25G              |                  |                  |
| ethernet-1/9        | disable          | down             | 25G              |                  |                  |
| ethernet-1/10       | disable          | down             | 25G              |                  |                  |
| ethernet-1/11       | disable          | down             | 25G              |                  |                  |
| ethernet-1/12       | disable          | down             | 25G              |                  |                  |
| ethernet-1/13       | disable          | down             | 25G              |                  |                  |
| ethernet-1/14       | disable          | down             | 25G              |                  |                  |
| ethernet-1/15       | disable          | down             | 25G              |                  |                  |
| ethernet-1/16       | disable          | down             | 25G              |                  |                  |
| ethernet-1/17       | disable          | down             | 25G              |                  |                  |
| ethernet-1/18       | disable          | down             | 25G              |                  |                  |
| ethernet-1/19       | disable          | down             | 25G              |                  |                  |
| ethernet-1/20       | disable          | down             | 25G              |                  |                  |
| ethernet-1/21       | disable          | down             | 25G              |                  |                  |
| ethernet-1/22       | disable          | down             | 25G              |                  |                  |
| ethernet-1/23       | disable          | down             | 25G              |                  |                  |
| ethernet-1/24       | disable          | down             | 25G              |                  |                  |
| ethernet-1/25       | disable          | down             | 25G              |                  |                  |
| ethernet-1/26       | disable          | down             | 25G              |                  |                  |
| ethernet-1/27       | disable          | down             | 25G              |                  |                  |
| ethernet-1/28       | disable          | down             | 25G              |                  |                  |
| ethernet-1/29       | disable          | down             | 25G              |                  |                  |
| ethernet-1/30       | disable          | down             | 25G              |                  |                  |
| ethernet-1/31       | disable          | down             | 25G              |                  |                  |
| ethernet-1/32       | disable          | down             | 25G              |                  |                  |
| ethernet-1/33       | disable          | down             | 25G              |                  |                  |
| ethernet-1/34       | disable          | down             | 25G              |                  |                  |
| ethernet-1/35       | disable          | down             | 25G              |                  |                  |
| ethernet-1/36       | disable          | down             | 25G              |                  |                  |
| ethernet-1/37       | disable          | down             | 25G              |                  |                  |
| ethernet-1/38       | disable          | down             | 25G              |                  |                  |
| ethernet-1/39       | disable          | down             | 25G              |                  |                  |
| ethernet-1/40       | disable          | down             | 25G              |                  |                  |
| ethernet-1/41       | disable          | down             | 25G              |                  |                  |
| ethernet-1/42       | disable          | down             | 25G              |                  |                  |
| ethernet-1/43       | disable          | down             | 25G              |                  |                  |
| ethernet-1/44       | disable          | down             | 25G              |                  |                  |
| ethernet-1/45       | disable          | down             | 25G              |                  |                  |
| ethernet-1/46       | disable          | down             | 25G              |                  |                  |
| ethernet-1/47       | disable          | down             | 25G              |                  |                  |
| ethernet-1/48       | disable          | down             | 25G              |                  |                  |
| ethernet-1/49       | disable          | down             | 100G             |                  |                  |
| ethernet-1/50       | disable          | down             | 100G             |                  |                  |
| ethernet-1/51       | disable          | down             | 100G             |                  |                  |
| ethernet-1/52       | disable          | down             | 100G             |                  |                  |
| ethernet-1/53       | disable          | down             | 100G             |                  |                  |
| ethernet-1/54       | disable          | down             | 100G             |                  |                  |
| ethernet-1/55       | disable          | down             | 100G             |                  |                  |
| ethernet-1/56       | disable          | down             | 100G             |                  |                  |
| ethernet-1/57       | disable          | down             | 10G              |                  |                  |
| ethernet-1/58       | disable          | down             | 10G              |                  |                  |
| mgmt0               | enable           | up               | 1G               |                  |                  |
+---------------------+------------------+------------------+------------------+------------------+------------------+
```

3. The link still exists, even though it's disabled. The route is configured independently of the admin state of the link.

4/5.

```bash
$ 03-routing-basics sudo docker exec -it clab-routing-basics-srl1 sr_cli
Using configuration file(s): []
Welcome to the srlinux CLI.
Type 'help' (and press <ENTER>) if you need any help using this.
--{ + running }--[  ]--
A:srl1# enter candidate
--{ + candidate shared default }--[  ]--
A:srl1# set / interface ethernet-1/3 admin-state enable
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
64 bytes from 10.1.5.2: icmp_seq=1 ttl=62 time=0.367 ms
64 bytes from 10.1.5.2: icmp_seq=2 ttl=62 time=0.283 ms
64 bytes from 10.1.5.2: icmp_seq=3 ttl=62 time=0.272 ms

--- 10.1.5.2 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2067ms
rtt min/avg/max/mdev = 0.272/0.307/0.367/0.042 ms
```
